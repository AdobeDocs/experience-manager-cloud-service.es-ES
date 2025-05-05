---
title: Prácticas recomendadas de consulta e indexación
description: Aprenda a optimizar los índices y las consultas en función de las directrices de prácticas recomendadas de Adobe.
topic-tags: best-practices
exl-id: 37eae99d-542d-4580-b93f-f454008880b1
feature: Operations
role: Admin
source-git-commit: 10580c1b045c86d76ab2b871ca3c0b7de6683044
workflow-type: tm+mt
source-wordcount: '3088'
ht-degree: 0%

---

# Prácticas recomendadas de consulta e indexación {#query-and-indexing-best-practices}

En AEM as a Cloud Service, todos los aspectos operativos relacionados con la indexación están automatizados. Esto permite a los desarrolladores centrarse en crear consultas eficientes y sus definiciones de índice correspondientes.

## Cuándo usar consultas {#when-to-use-queries}

Las consultas son una forma de acceder al contenido, pero no son la única posibilidad. En muchas situaciones, se puede acceder al contenido del repositorio de forma más eficaz por otros medios. Debe tener en cuenta si las consultas son la forma mejor y más eficaz de acceder al contenido para su caso de uso.

### Diseño de repositorios y taxonomías {#repository-and-taxonomy-design}

Al diseñar la taxonomía de un repositorio, se deben tener en cuenta varios factores. Estos incluyen controles de acceso, localización, herencia de componentes y propiedades de página, etc.

Al diseñar una taxonomía que aborde estas preocupaciones, también es importante tener en cuenta la &quot;transitabilidad&quot; del diseño de indexación. En este contexto, la transitabilidad es la capacidad de una taxonomía para permitir que se acceda al contenido de forma predecible en función de su ruta. Esto ofrece un sistema más eficiente, fácil de mantener, que uno que requiere que se ejecuten varias consultas.

Además, al diseñar una taxonomía, es importante tener en cuenta si la ordenación es importante. En los casos en los que no se requiere el orden explícito y se espera un gran número de nodos del mismo nivel, se prefiere utilizar un tipo de nodo sin ordenar como `sling:Folder` o `oak:Unstructured`. En los casos en los que se requiere ordenar, `nt:unstructured` y `sling:OrderedFolder` serían más apropiados.

### Consultas en componentes {#queries-in-components}

AEM Dado que las consultas pueden ser una de las operaciones más gravosas realizadas en un sistema de, es aconsejable evitarlas en los componentes. Tener varias consultas ejecutándose cada vez que se procesa una página puede a menudo degradar el rendimiento del sistema. Hay dos estrategias que se pueden usar para evitar la ejecución de consultas al procesar componentes: **[nodos de recorrido](#traversing-nodes)** y **[resultados de recuperación previa](#prefetching-results)**.

### Recorrido de nodos {#traversing-nodes}

Si el repositorio está diseñado de manera que permita un conocimiento previo de la ubicación de los datos necesarios, se puede implementar un código que recupere estos datos de las rutas necesarias sin tener que ejecutar consultas para encontrarlos.

Un ejemplo de esto sería procesar contenido que se ajuste a una categoría determinada. Un método sería organizar el contenido con una propiedad category que se pueda consultar para rellenar un componente que muestre los elementos de una categoría.

Un mejor enfoque sería estructurar este contenido en una taxonomía por categoría para que se pueda recuperar manualmente.

Por ejemplo, si el contenido se almacena en una taxonomía similar a:

```xml
/content/myUnstructuredContent/parentCategory/childCategory/contentPiece
```

el nodo `/content/myUnstructuredContent/parentCategory/childCategory` simplemente se puede recuperar, sus elementos secundarios se pueden analizar y utilizar para procesar el componente.

Además, cuando se trata de un conjunto de resultados pequeño u homogéneo, puede ser más rápido atravesar el repositorio y recopilar los nodos necesarios, en lugar de crear una consulta para devolver el mismo conjunto de resultados. Como consideración general, las consultas deben evitarse siempre que sea posible hacerlo.

### Resultados de recuperación previa {#prefetching-results}

A veces, el contenido o los requisitos relacionados con el componente no permiten el uso del recorrido de nodos como método para recuperar los datos necesarios. En estos casos, es necesario ejecutar las consultas necesarias antes de procesar el componente para garantizar un rendimiento óptimo.

Si los resultados necesarios para el componente se pueden calcular en el momento en que se crea y no hay expectativas de que el contenido cambie, la consulta se puede ejecutar después de realizar un cambio.

Si los datos o el contenido cambian con regularidad, la consulta se puede ejecutar en una programación o a través de un oyente para actualizaciones de los datos subyacentes. A continuación, los resultados se pueden escribir en una ubicación compartida del repositorio. Cualquier componente que necesite estos datos puede extraer los valores de este nodo único sin necesidad de ejecutar una consulta en tiempo de ejecución.

Se puede utilizar una estrategia similar para mantener el resultado en una caché en memoria, que se rellena al inicio y se actualiza cada vez que se realizan cambios (con un JCR `ObservationListener` o un Sling `ResourceChangeListener`).

## Optimización de consultas {#optimizing-queries}

La documentación de Oak proporciona [información general de alto nivel sobre cómo se ejecutan las consultas](https://jackrabbit.apache.org/oak/docs/query/query-engine.html#query-processing). Esto forma la base de todas las actividades de optimización descritas en este documento.

AEM as a Cloud Service proporciona la [Herramienta de rendimiento de consultas](#query-performance-tool), diseñada para admitir la implementación de consultas eficientes.

* Muestra las consultas ya ejecutadas con sus características de rendimiento relevantes y el plan de consulta.
* Permite realizar consultas ad hoc en varios niveles, desde mostrar el plan de la consulta hasta ejecutar la consulta completa.

Se puede acceder a la herramienta de rendimiento de consultas a través de [Developer Console en Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/developer-console.html?lang=es#queries). La herramienta de rendimiento de consultas de AEM as a Cloud Service AEM ofrece más información sobre los detalles de la ejecución de consultas a lo largo de la versión 6.x de la misma en la que se ejecuta la consulta de la manera más sencilla posible.

Este gráfico ilustra el flujo general para utilizar la herramienta de rendimiento de consultas para optimizar las consultas.

![Flujo de optimización de consultas](assets/query-optimization-flow.png)

### Uso de un índice {#use-an-index}

Cada consulta debe utilizar un índice para ofrecer un rendimiento óptimo. En la mayoría de los casos, los índices existentes listos para usar deberían ser suficientes para gestionar consultas.

A veces, es necesario agregar propiedades personalizadas a un índice existente, por lo que se pueden consultar restricciones adicionales mediante el índice. Consulte el documento [Búsqueda e indexación de contenido](/help/operations/indexing.md#changing-an-index) para obtener más información. La sección [Hoja de trucos de consultas JCR](#jcr-query-cheatsheet) de este documento describe el aspecto que debe tener una definición de propiedad en un índice para admitir un tipo de consulta específico.

### Uso de los criterios adecuados {#use-the-right-criteria}

La restricción principal de cualquier consulta debe ser una coincidencia de propiedad, ya que es el tipo más eficaz. Añadir más restricciones de propiedad limita aún más el resultado.

El motor de consultas considera un solo índice. Esto significa que un índice existente puede y debe personalizarse añadiéndole más propiedades de índice personalizadas.

La sección [Hoja de referencia de consultas JCR](#jcr-query-cheatsheet) de este documento enumera las restricciones disponibles y también describe el aspecto que debe tener una definición de índice para que se seleccione. Use la [Herramienta de rendimiento de consultas](#query-performance-tool) para probar la consulta y asegurarse de que se utiliza el índice correcto y de que el motor de consultas no necesita evaluar las restricciones fuera del índice.

### Pedidos {#ordering}

Si se solicita un orden específico del resultado, el motor de consultas puede hacerlo de dos formas:

1. El índice puede entregar el resultado por completo y en el orden correcto.
   * Esto funciona si las propiedades que se utilizan para ordenar se anotan con `ordered=true` en la definición del índice.
1. El motor de consultas realiza el proceso de ordenación.
   * Esto puede ocurrir cuando el motor de consulta realiza un filtrado fuera del índice o cuando la propiedad de ordenación no está anotada con la propiedad `ordered=true`.
   * Esto requiere que el conjunto de resultados completo se lea en la memoria para ordenarlo, lo que es mucho más lento que la primera opción.

### Restringir el tamaño del resultado {#restrict-result-size}

El tamaño recuperado del resultado de la consulta es un factor importante en el rendimiento de la consulta. Como el resultado se obtiene de forma diferida, existe una diferencia entre recuperar los 20 primeros resultados y recuperar 10 000 resultados, tanto en tiempo de ejecución como en uso de memoria.

Esto también significa que el tamaño del conjunto de resultados solo se puede determinar correctamente si se recuperan todos los resultados. Por este motivo, el conjunto de resultados recuperado siempre debe limitarse, ya sea aumentando la consulta (consulte la sección [hoja de trucos de consultas JCR](#jcr-query-cheatsheet) de este documento para obtener detalles) o limitando las lecturas de los resultados.

Este límite también evita que el motor de consultas alcance el **límite de recorrido** de 100 000 nodos, lo que lleva a una detención forzada de la consulta.

Consulte la sección [Consultas con grandes conjuntos de resultados](#queries-with-large-result-sets) de este documento si un conjunto de resultados potencialmente grande debe procesarse por completo.

## Herramienta de rendimiento de consultas {#query-performance-tool}

La herramienta de rendimiento de consultas (ubicada en `/libs/granite/operations/content/diagnosistools/queryPerformance.html` y disponible a través de [Developer Console en Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/developer-console.html?lang=es#queries)) proporciona:
* Una lista de cualquier &quot;Consulta lenta&quot;; definida actualmente como aquellas que leen o analizan más de 5000 filas.
* Una lista de &#39;Consultas populares&#39;
* La herramienta &quot;Explicar consulta&quot; para comprender cómo Oak ejecutará una consulta en particular.

![Herramienta de rendimiento de consultas](assets/query-performance-tool.png)

Las tablas &quot;Consultas lentas&quot; y &quot;Consultas populares&quot; incluyen:
* La propia instrucción de consulta.
* Detalles del último subproceso que ejecutó la consulta, lo que permite identificar la página o función de la aplicación que ejecuta la consulta.
* Una puntuación de &quot;Optimización de lectura&quot; para la consulta.
   * Se calcula como la relación entre el número de filas/nodos analizados para ejecutar la consulta y el número de resultados coincidentes leídos.
   * Una consulta para la que cada restricción (y cualquier orden) se puede administrar en el índice tendrá una puntuación del 90 % o superior.
* Detalles del número máximo de filas -
   * Lectura: indica que se incluyó una fila como parte de un conjunto de resultados.
   * Analizado: indica que se incluyó una fila en los resultados de la consulta de índice subyacente (en el caso de una consulta indexada) o que se leyó desde el almacén de nodos (en el caso de un recorrido de repositorio).

Estas tablas ayudan a identificar consultas que no están totalmente indizadas (consulte [Usar un índice](#use-an-index) o que están leyendo demasiados nodos (consulte también [Recorrido del repositorio](#repository-traversal) e [Recorrido del índice](#index-traversal)). Estas consultas se resaltarán, con las áreas de preocupación apropiadas marcadas en rojo.

Se proporciona la opción `Reset Statistics` para eliminar todas las estadísticas existentes recopiladas en las tablas. Esto permite ejecutar una consulta determinada (a través de la propia aplicación o de la herramienta Explicar consulta) y analizar las estadísticas de ejecución.

### Explicar la consulta

La herramienta de consulta Explicar permite a los desarrolladores comprender el plan de ejecución de la consulta (consulte [Leer el plan de ejecución de la consulta](#reading-query-execution-plan)), incluidos detalles de cualquier índice utilizado al ejecutar la consulta. Esto puede utilizarse para comprender la eficacia con la que se indexa una consulta para predecir o analizar de forma retrospectiva su rendimiento.

#### Explicación de una consulta

Para explicar una consulta, haga lo siguiente:

* Seleccione el idioma de consulta adecuado mediante la lista desplegable `Language`.
* Escriba la instrucción de consulta en el campo `Query`.
* Si es necesario, seleccione cómo se ejecutará la consulta utilizando las casillas de verificación proporcionadas.
   * De forma predeterminada, no es necesario ejecutar las consultas JCR para identificar el plan de ejecución de la consulta (este no es el caso de las consultas de QueryBuilder).
   * Se proporcionan tres opciones para ejecutar la consulta:
      * `Include Execution Time` - ejecutar la consulta pero no intentar leer ningún resultado.
      * `Read first page of results` - ejecute la consulta y lea la primera &quot;página&quot; de 20 resultados (replicando las prácticas recomendadas para ejecutar consultas).
      * `Include Node Count`: ejecute la consulta y lea todo el conjunto de resultados (generalmente no se recomienda; consulte [Recorrido del índice](#index-traversal)).

#### Ventana emergente Explicación de la consulta {#query-explanation-popup}

![Ventana emergente de explicación de la consulta](./assets/query-explanation-popup.png)

Después de seleccionar `Explain`, aparece una ventana emergente que describe el resultado de la explicación de la consulta (y la ejecución, si está seleccionada).
Esta ventana emergente incluye detalles de lo siguiente:
* Los índices utilizados al ejecutar la consulta (o ningún índice si la consulta se ejecutaría usando [Recorrido del repositorio](#repository-traversal)).
* El tiempo de ejecución (si se marcó la casilla de verificación `Include Execution Time`) y el recuento de resultados leídos (si se marcaron las casillas de verificación `Read first page of results` o `Include Node Count`).
* El plan de ejecución, que permite un análisis detallado de cómo se ejecuta la consulta. Consulte [Leyendo el plan de ejecución de la consulta](#reading-query-execution-plan) para saber cómo interpretar esto.
* Las rutas de los primeros 20 resultados de la consulta (si se marcó la casilla `Read first page of results`)
* Los registros completos de la planificación de la consulta, que muestran los costes relativos de los índices que se consideraron para la ejecución de esta consulta (el índice con el coste más bajo será el elegido).

#### Lectura del Plan de ejecución de consultas {#reading-query-execution-plan}

El plan de ejecución de consultas contiene todo lo necesario para predecir (o explicar) el rendimiento de una consulta determinada. Comprenda la eficacia con la que se ejecutará la consulta comparando las restricciones y el orden de la consulta JCR (o Query Builder) original con la consulta ejecutada en el índice subyacente (Lucene, Elastic o Property).

Tenga en cuenta la siguiente consulta:

```
/jcr:root/content/dam//element(*, dam:Asset) [jcr:content/metadata/dc:title = "My Title"] order by jcr:created
```

... que contiene -
* 3 restricciones
   * Tipo de nodo (`dam:Asset`)
   * Ruta (descendientes de `/content/dam`)
   * Propiedad (`jcr:content/metadata/dc:title = "My Title"`)
* Ordenando por la propiedad `jcr:created`

Explicar esta consulta resulta en el siguiente plan:

```
[dam:Asset] as [a] /* lucene:damAssetLucene-9(/oak:index/damAssetLucene-9) +:ancestors:/content/dam +jcr:content/metadata/dc:title:My Title ordering:[{ propertyName : jcr:created, propertyType : UNDEFINED, order : ASCENDING }] where ([a].[jcr:content/metadata/dc:title] = 'My Title') and (isdescendantnode([a], [/content/dam])) */
```

Dentro de este plan, la sección que describe la consulta ejecutada en el índice subyacente es -

```
lucene:damAssetLucene-9(/oak:index/damAssetLucene-9) +:ancestors:/content/dam +jcr:content/metadata/dc:title:My Title ordering:[{ propertyName : jcr:created, propertyType : UNDEFINED, order : ASCENDING }]
```

Esta sección del plan establece que:
* Se utiliza un índice para ejecutar esta consulta:
   * En este caso, se utilizará el índice Lucene `/oak:index/damAssetLucene-9`, por lo que el resto de la información se encuentra en Sintaxis de consultas de Lucene.
* Las 3 restricciones se gestionan mediante el índice:
   * La restricción del tipo de nodo
      * implícito, ya que `damAssetLucene-9` solo indexa nodos de tipo dam:Asset.
   * La restricción de ruta
      * porque `+:ancestors:/content/dam` aparece en la consulta de Lucene.
   * La restricción de propiedad
      * porque `+jcr:content/metadata/dc:title:My Title` aparece en la consulta de Lucene.
* El índice gestiona el orden
   * porque `ordering:[{ propertyName : jcr:created, propertyType : UNDEFINED, order : ASCENDING }]` aparece en la consulta de Lucene.

Es probable que una consulta de este tipo funcione bien, ya que los resultados devueltos por la consulta de índice no se filtrarán más en el motor de consultas (aparte del filtrado de Control de acceso). Sin embargo, aún es posible que una consulta de este tipo se ejecute lentamente si no se siguen las prácticas recomendadas; consulte [Índice de recorrido](#index-traversal) a continuación.

Consideración de una consulta diferente:

```
/jcr:root/content/dam//element(*, dam:Asset) [jcr:content/metadata/myProperty = "My Property Value"] order by jcr:created
```

... que contiene -
* 3 restricciones
   * Tipo de nodo (`dam:Asset`)
   * Ruta (descendientes de `/content/dam`)
   * Propiedad (`jcr:content/metadata/myProperty = "My Property Value"`)
* Ordenando por la propiedad `jcr:created`**

Explicar esta consulta resulta en el siguiente plan:

```
[dam:Asset] as [a] /* lucene:damAssetLucene-9-custom-1(/oak:index/damAssetLucene-9-custom-1) :ancestors:/content/dam ordering:[{ propertyName : jcr:created, propertyType : UNDEFINED, order : ASCENDING }] where ([a].[jcr:content/metadata/myProperty] = 'My Property Value') and (isdescendantnode([a], [/content/dam])) */
```

Dentro de este plan, la sección que describe la consulta ejecutada en el índice subyacente es -

```
lucene:damAssetLucene-9(/oak:index/damAssetLucene-9) :ancestors:/content/dam ordering:[{ propertyName : jcr:created, propertyType : UNDEFINED, order : ASCENDING }]
```

Esta sección del plan establece que:
* Solo 2 (de las 3) restricciones son manejadas por el índice -
   * La restricción del tipo de nodo
      * implícito, ya que `damAssetLucene-9` solo indexa nodos de tipo dam:Asset.
   * La restricción de ruta
      * porque `+:ancestors:/content/dam` aparece en la consulta de Lucene.
* La restricción de propiedad `jcr:content/metadata/myProperty = "My Property Value"` no se ejecuta en el índice, sino que se aplicará como filtrado del motor de consulta en los resultados de la consulta de Lucene subyacente.
   * Esto se debe a que `+jcr:content/metadata/myProperty:My Property Value` no aparece en la consulta de Lucene, ya que esta propiedad no está indizada en el índice `damAssetLucene-9` utilizado para esta consulta.

Este plan de ejecución de consultas hará que todos los recursos por debajo de `/content/dam` se lean desde el índice y luego se filtren más por el motor de consultas (que solo incluirá los que coincidan con la restricción de propiedad no indizada en el conjunto de resultados).

Aunque solo un pequeño porcentaje de recursos coincida con la restricción `jcr:content/metadata/myProperty = "My Property Value"`, la consulta debe leer un gran número de nodos para (intentar) rellenar la &quot;página&quot; de resultados solicitada. Esto puede dar como resultado una consulta de bajo rendimiento, que se mostrará con una puntuación baja de `Read Optimization` en la herramienta Rendimiento de la consulta) y puede generar mensajes ADVERTENCIA que indiquen que se está atravesando un gran número de nodos (consulte [Recorrido del índice](#index-traversal)).

Para optimizar el rendimiento de esta segunda consulta, cree una versión personalizada del índice `damAssetLucene-9` (`damAssetLucene-9-custom-1`) y agregue la siguiente definición de propiedad:

```
"myProperty": {
  "jcr:primaryType": "nt:unstructured",
  "propertyIndex": true,
  "name": "jcr:content/metadata/myProperty"
}
```

## Hoja de características clave de consulta JCR {#jcr-query-cheatsheet}

Para admitir la creación de consultas JCR y definiciones de índice eficientes, la [Hoja de referencia de consultas JCR](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/practices/best-practices-for-queries-and-indexing.html?lang=es#jcrquerycheatsheet) está disponible para su descarga y uso como referencia durante el desarrollo.

Contiene consultas de ejemplo para QueryBuilder, XPath y SQL-2, que cubren varios escenarios que se comportan de forma diferente en términos de rendimiento de la consulta. También proporciona recomendaciones sobre cómo crear o personalizar índices de Oak. El contenido de esta hoja de referencia se aplica a AEM as a Cloud Service AEM y a la versión 6 5.

## Prácticas recomendadas de definición de índice {#index-definition-best-practices}

A continuación se presentan algunas prácticas recomendadas a tener en cuenta al definir o ampliar índices.

* Para los tipos de nodo que tienen índices existentes (como `dam:Asset` o `cq:Page`) prefieren la extensión de los índices OOTB a la adición de nuevos índices.
   * Se desaconseja agregar nuevos índices, especialmente índices de texto completo, en el tipo de nodo `dam:Asset` (consulte [esta nota](/help/operations/indexing.md##index-names-index-names)).
* Al añadir nuevos índices
   * Defina siempre índices del tipo &quot;lucene&quot;.
   * Use una etiqueta de índice en la definición de índice (y en la consulta asociada) y `selectionPolicy = tag` para asegurarse de que el índice solo se utiliza para las consultas deseadas.
   * Asegúrese de que se proporcionan `queryPaths` y `includedPaths` (normalmente con los mismos valores).
   * Utilice `excludedPaths` para excluir las rutas que no contendrán resultados útiles.
   * Utilice las propiedades `analyzed` únicamente cuando sea necesario; por ejemplo, cuando necesite utilizar una restricción de consulta de texto completo únicamente para esa propiedad.
   * Especifique siempre `async = [ async, nrt ] `, `compatVersion = 2` y `evaluatePathRestrictions = true`.
   * Especifique solamente `nodeScopeIndex = true` si necesita un índice de texto completo de ámbito de nodo.

>[!NOTE]
>
>Para obtener más información, consulte [Documentación del índice Oak Lucene](https://jackrabbit.apache.org/oak/docs/query/lucene.html).

Las comprobaciones automatizadas de canalización de Cloud Manager aplicarán algunas de las prácticas recomendadas descritas anteriormente.

## Consultas con conjuntos de resultados grandes {#queries-with-large-result-sets}

Aunque se recomienda evitar consultas con grandes conjuntos de resultados, hay casos válidos en los que deben procesarse grandes conjuntos de resultados. A menudo, el tamaño del resultado no se conoce por adelantado, por lo que se deben tomar algunas precauciones para que el procesamiento sea fiable.

* La consulta no debe ejecutarse dentro de una solicitud. AEM En su lugar, la consulta debe ejecutarse como parte de un trabajo de Sling o de un flujo de trabajo de. No tienen limitaciones en su tiempo de ejecución total y se reinician en caso de que la instancia se desactive durante el procesamiento de la consulta y sus resultados.
* Para superar el límite de consultas de 100 000 nodos, debería considerar la posibilidad de usar [Paginación del conjunto de claves](https://jackrabbit.apache.org/oak/docs/query/query-engine.html#Keyset_Pagination) y dividir la consulta en varias subconsultas.

## Recorrido del repositorio {#repository-traversal}

Las consultas que atraviesan el repositorio no utilizan un índice y se registran con un mensaje similar al siguiente.

```text
28.06.2022 13:32:52.804 *WARN* [127.0.0.1 [1656415972414] POST /libs/settings/granite/operations/diagnosis/granite_queryperformance.explain.json HTTP/1.1] org.apache.jackrabbit.oak.plugins.index.Cursors$TraversingCursor Traversed 98000 nodes with filter Filter(query=select [jcr:path], [jcr:score], * from [nt:base] as a /* xpath: //* */, path=*) called by com.adobe.granite.queries.impl.explain.query.ExplainQueryServlet.getHeuristics; consider creating an index or changing the query
```

Con este fragmento de registro puede determinar lo siguiente:

* La consulta en sí: `//*`
* El código Java que ejecutó esta consulta: `com.adobe.granite.queries.impl.explain.query.ExplainQueryServlet::getHeuristics` para ayudar a identificar al creador de la consulta.

Con esta información, es posible optimizar esta consulta utilizando los métodos descritos en la sección [Optimización de consultas](#optimizing-queries) de este documento.

### Índice de recorrido {#index-traversal}

Las consultas que utilizan un índice, pero que siguen leyendo un gran número de nodos, se registran con un mensaje similar al siguiente (observe el término `Index-Traversed` en lugar de `Traversed`).

```text
05.10.2023 10:56:10.498 *WARN* [127.0.0.1 [1696502982443] POST /libs/settings/granite/operations/diagnosis/granite_queryperformance.explain.json HTTP/1.1] org.apache.jackrabbit.oak.plugins.index.search.spi.query.FulltextIndex$FulltextPathCursor Index-Traversed 60000 nodes with filter Filter(query=select [jcr:path], [jcr:score], * from [dam:Asset] as a where isdescendantnode(a, '/content/dam') order by [jcr:content/metadata/unindexedProperty] /* xpath: /jcr:root/content/dam//element(*, dam:Asset) order by jcr:content/metadata/unindexedProperty */, path=/content/dam//*)
```

Esto puede ocurrir por varias razones:

1. No todas las restricciones de la consulta se pueden controlar en el índice.
   * En este caso, se está leyendo un superconjunto del conjunto de resultados final desde el índice y, a continuación, se está filtrando en el motor de consultas.
   * Esto es muchas veces más lento que aplicar restricciones en la consulta de índice subyacente.
1. La consulta se ordena por una propiedad que no está marcada como &quot;ordenada&quot; en el índice.
   * En este caso, el motor de consulta debe leer todos los resultados devueltos por el índice y ordenarlos en memoria.
   * Esto es muchas veces más lento que aplicar la ordenación en la consulta de índice subyacente.
1. El ejecutor de la consulta está intentando repetir un conjunto de resultados grande.
   * Esta situación puede ocurrir por varias razones, como se enumera a continuación:

| Causa | Mitigación |
|----------|--------------|
| La omisión de `p.guessTotal` (o el uso de un guessTotal muy grande) que hace que QueryBuilder itere una gran cantidad de resultados contando resultados | Proporcionar a `p.guessTotal` un valor apropiado |
| El uso de un límite grande o ilimitado en Query Builder (por ejemplo `p.limit=-1`) | Usar un valor apropiado para `p.limit` (idealmente 1000 o inferior) |
| El uso de un predicado de filtrado en el Generador de consultas, que filtra grandes cantidades de resultados de la consulta JCR subyacente | Reemplace los predicados de filtrado por restricciones que se puedan aplicar en la consulta JCR subyacente |
| Uso de un orden basado en Comparator en QueryBuilder | Reemplazar por el orden basado en propiedades en la consulta JCR subyacente (mediante propiedades indizadas como ordenadas) |
| Filtrado de una gran cantidad de resultados debido al control de acceso | Aplique una propiedad indizada o una restricción de ruta adicional a la consulta para reflejar el control de acceso |
| El uso de &quot;paginación de desplazamiento&quot; con un desplazamiento grande | Considere utilizar [Paginación del conjunto de claves](https://jackrabbit.apache.org/oak/docs/query/query-engine.html#Keyset_Pagination) |
| Iteración de números de resultados grandes o ilimitados | Considere utilizar [Paginación del conjunto de claves](https://jackrabbit.apache.org/oak/docs/query/query-engine.html#Keyset_Pagination) |
| Índice elegido incorrecto | Utilice Etiquetas en la consulta y la definición del índice para asegurarse de que se utiliza el índice esperado |
