---
title: Prácticas recomendadas de consulta e indexación
description: Aprenda a optimizar los índices y las consultas en función de las directrices de prácticas recomendadas de Adobe.
topic-tags: best-practices
exl-id: 37eae99d-542d-4580-b93f-f454008880b1
source-git-commit: 1994b90e3876f03efa571a9ce65b9fb8b3c90ec4
workflow-type: tm+mt
source-wordcount: '1556'
ht-degree: 1%

---

# Prácticas recomendadas de consulta e indexación {#query-and-indexing-best-practices}

AEM En as a Cloud Service, todos los aspectos operativos relacionados con la indexación están automatizados. Esto permite a los desarrolladores centrarse en crear consultas eficientes y sus definiciones de índice correspondientes.

## Cuándo usar consultas {#when-to-use-queries}

Las consultas son una forma de acceder al contenido, pero no son la única posibilidad. En muchas situaciones, se puede acceder al contenido del repositorio de forma más eficaz por otros medios. Debe tener en cuenta si las consultas son la forma mejor y más eficaz de acceder al contenido para su caso de uso.

### Diseño de repositorios y taxonomías {#repository-and-taxonomy-design}

Al diseñar la taxonomía de un repositorio, se deben tener en cuenta varios factores. Estos incluyen controles de acceso, localización, herencia de componentes y propiedades de página, etc.

Al diseñar una taxonomía que aborde estas preocupaciones, también es importante tener en cuenta la &quot;transitabilidad&quot; del diseño de indexación. En este contexto, la transitabilidad es la capacidad de una taxonomía para permitir que se acceda al contenido de forma predecible en función de su ruta. Esto ofrece un sistema más eficiente, fácil de mantener, que uno que requiere que se ejecuten varias consultas.

Además, al diseñar una taxonomía, es importante tener en cuenta si la ordenación es importante. En los casos en los que no se requiere un orden explícito y se espera un gran número de nodos hermanos, se prefiere utilizar un tipo de nodo sin ordenar como `sling:Folder` o `oak:Unstructured`. En los casos en que sea necesario realizar un pedido, `nt:unstructured` y `sling:OrderedFolder` sería más apropiado.

### Consultas en componentes {#queries-in-components}

AEM Dado que las consultas pueden ser una de las operaciones más gravosas realizadas en un sistema de, es aconsejable evitarlas en los componentes. Tener varias consultas ejecutándose cada vez que se procesa una página puede a menudo degradar el rendimiento del sistema. Existen dos estrategias que se pueden utilizar para evitar la ejecución de consultas al procesar componentes: **[atravesar nodos](#traversing-nodes)** y **[recuperación previa de resultados.](#prefetching-results)**

### Recorrido de nodos {#traversing-nodes}

Si el repositorio está diseñado de manera que permita un conocimiento previo de la ubicación de los datos necesarios, se puede implementar un código que recupere estos datos de las rutas necesarias sin tener que ejecutar consultas para encontrarlos.

Un ejemplo de esto sería procesar contenido que se ajuste a una categoría determinada. Un método sería organizar el contenido con una propiedad category que se pueda consultar para rellenar un componente que muestre los elementos de una categoría.

Un mejor enfoque sería estructurar este contenido en una taxonomía por categoría para que se pueda recuperar manualmente.

Por ejemplo, si el contenido se almacena en una taxonomía similar a:

```xml
/content/myUnstructuredContent/parentCategory/childCategory/contentPiece
```

el `/content/myUnstructuredContent/parentCategory/childCategory` El nodo simplemente se puede recuperar, sus tareas secundarias se pueden analizar y utilizar para procesar el componente.

Además, cuando se trata de un conjunto de resultados pequeño u homogéneo, puede ser más rápido atravesar el repositorio y recopilar los nodos necesarios, en lugar de crear una consulta para devolver el mismo conjunto de resultados. Como consideración general, las consultas deben evitarse siempre que sea posible hacerlo.

### Resultados de recuperación previa {#prefetching-results}

A veces, el contenido o los requisitos relacionados con el componente no permiten el uso del recorrido de nodos como método para recuperar los datos necesarios. En estos casos, es necesario ejecutar las consultas necesarias antes de procesar el componente para garantizar un rendimiento óptimo.

Si los resultados necesarios para el componente se pueden calcular en el momento en que se crea y no hay expectativas de que el contenido cambie, la consulta se puede ejecutar después de realizar un cambio.

Si los datos o el contenido cambian con regularidad, la consulta se puede ejecutar en una programación o a través de un oyente para actualizaciones de los datos subyacentes. A continuación, los resultados se pueden escribir en una ubicación compartida del repositorio. Cualquier componente que necesite estos datos puede extraer los valores de este nodo único sin necesidad de ejecutar una consulta en tiempo de ejecución.

Se puede utilizar una estrategia similar para mantener el resultado en una caché en memoria, que se rellena al inicio y se actualiza cada vez que se realizan cambios (con un JCR) `ObservationListener` o un Sling `ResourceChangeListener`).

## Optimización de consultas {#optimizing-queries}

La documentación de Oak proporciona una [información general de alto nivel sobre cómo se ejecutan las consultas.](https://jackrabbit.apache.org/oak/docs/query/query-engine.html#query-processing) Esto forma la base de todas las actividades de optimización descritas en este documento.

AEM as a Cloud Service proporciona la herramienta de rendimiento de consultas, diseñada para admitir la implementación de consultas eficientes.

* Muestra las consultas ya ejecutadas con sus características de rendimiento relevantes y el plan de consulta.
* Permite realizar consultas ad hoc en varios niveles, desde mostrar el plan de la consulta hasta ejecutar la consulta completa.

Se puede acceder a la herramienta de rendimiento de consultas mediante el [Developer Console en Cloud Manager.](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/developer-console.html?lang=es#queries) AEM La herramienta de rendimiento de consultas de as a Cloud Service AEM proporciona más información sobre los detalles de la ejecución de consultas en la versión 6.x de la misma en la que se ejecuta la consulta de la manera más sencilla posible.

Este gráfico ilustra el flujo general para utilizar la herramienta de rendimiento de consultas para optimizar las consultas.

![Flujo de optimización de consultas](assets/query-optimization-flow.png)

### Uso de un índice {#use-an-index}

Cada consulta debe utilizar un índice para ofrecer un rendimiento óptimo. En la mayoría de los casos, los índices existentes listos para usar deberían ser suficientes para gestionar consultas.

A veces, es necesario agregar propiedades personalizadas a un índice existente, por lo que se pueden consultar restricciones adicionales mediante el índice. Ver el documento [Búsqueda de contenido e indexación](/help/operations/indexing.md#changing-an-index) para obtener más información. El [Hoja de trucos de consulta JCR](#jcr-query-cheatsheet) de este documento describe el aspecto que debe tener una definición de propiedad en un índice para admitir un tipo de consulta específico.

### Uso de los criterios adecuados {#use-the-right-criteria}

La restricción principal de cualquier consulta debe ser una coincidencia de propiedad, ya que es el tipo más eficaz. Añadir más restricciones de propiedad limita aún más el resultado.

El motor de consultas considera un solo índice. Esto significa que un índice existente puede y debe personalizarse añadiéndole más propiedades de índice personalizadas.

El [Hoja de trucos de consulta JCR](#jcr-query-cheatsheet) en la sección de este documento se enumeran las restricciones disponibles y también se describe el aspecto que debe tener una definición de índice para que se recoja. Utilice el [Herramienta de rendimiento de consultas](#query-performance-tool) para probar la consulta y asegurarse de que se utiliza el índice correcto y de que el motor de consultas no necesita evaluar las restricciones fuera del índice.

### Pedidos {#ordering}

Si se solicita un orden específico del resultado, el motor de consultas puede hacerlo de dos formas:

1. El índice puede entregar el resultado por completo y en el orden correcto.
   * Esto funciona si las propiedades que se utilizan para ordenar están anotadas con `ordered=true` en la definición del índice.
1. El motor de consultas realiza el proceso de ordenación.
   * Esto puede ocurrir cuando el motor de consulta realiza un filtrado fuera del índice o cuando la propiedad de ordenación no está anotada con el `ordered=true` propiedad.
   * Esto requiere que el conjunto de resultados completo se lea en la memoria para ordenarlo, lo que es mucho más lento que la primera opción.

### Restringir el tamaño del resultado {#restrict-result-size}

El tamaño recuperado del resultado de la consulta es un factor importante en el rendimiento de la consulta. Como el resultado se obtiene de forma diferida, existe una diferencia entre recuperar los 20 primeros resultados y recuperar 10 000 resultados, tanto en tiempo de ejecución como en uso de memoria.

Esto también significa que el tamaño del conjunto de resultados solo se puede determinar correctamente si se recuperan todos los resultados. Por este motivo, el conjunto de resultados recuperado siempre debe estar limitado, ya sea aumentando la consulta (consulte la [Hoja de trucos de consulta JCR](#jcr-query-cheatsheet) de este documento para obtener más información) o limitando las lecturas de los resultados.

Este límite también evita que el motor de consultas visite **límite de recorrido** de 100 000 nodos, lo que provoca una parada forzada de la consulta.

Consulte la sección [Consultas con resultados grandes](#queries-with-large-result-sets) de este documento si un conjunto de resultados potencialmente grande debe procesarse completamente.

## Hoja de trucos de consulta JCR {#jcr-query-cheatsheet}

Para admitir la creación de consultas JCR y definiciones de índice eficientes, la variable [Hoja de características clave de consulta JCR](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/practices/best-practices-for-queries-and-indexing.html#jcrquerycheatsheet) está disponible para su descarga y uso como referencia durante el desarrollo.

Contiene consultas de ejemplo para QueryBuilder, XPath y SQL-2, que cubren varios escenarios que se comportan de forma diferente en términos de rendimiento de la consulta. También proporciona recomendaciones sobre cómo crear o personalizar índices de Oak. AEM El contenido de esta hoja de referencia se aplica a las versiones as a Cloud Service AEM y 6.5 de la.

## Consultas con conjuntos de resultados grandes {#queries-with-large-result-sets}

Aunque se recomienda evitar consultas con grandes conjuntos de resultados, hay casos válidos en los que deben procesarse grandes conjuntos de resultados. A menudo, el tamaño del resultado no se conoce por adelantado, por lo que se deben tomar algunas precauciones para que el procesamiento sea fiable.

* La consulta no debe ejecutarse dentro de una solicitud. AEM En su lugar, la consulta debe ejecutarse como parte de un trabajo de Sling o de un flujo de trabajo de. No tienen limitaciones en su tiempo de ejecución total y se reinician en caso de que la instancia se desactive durante el procesamiento de la consulta y sus resultados.
* Para superar el límite de consultas de 100 000 nodos, debe considerar la posibilidad de utilizar [Paginación de conjunto de claves](https://jackrabbit.apache.org/oak/docs/query/query-engine.html#Keyset_Pagination) y divida la consulta en varias subconsultas.

## Recorrido del repositorio {#repository-traversal}

Las consultas que atraviesan el repositorio no utilizan un índice y se registran con un mensaje similar al siguiente.

```text
28.06.2022 13:32:52.804 *WARN* [127.0.0.1 [1656415972414] POST /libs/settings/granite/operations/diagnosis/granite_queryperformance.explain.json HTTP/1.1] org.apache.jackrabbit.oak.plugins.index.Cursors$TraversingCursor Traversed 98000 nodes with filter Filter(query=select [jcr:path], [jcr:score], * from [nt:base] as a /* xpath: //* */, path=*) called by com.adobe.granite.queries.impl.explain.query.ExplainQueryServlet.getHeuristics; consider creating an index or changing the query
```

Con este fragmento de registro puede determinar lo siguiente:

* La propia consulta: `//*`
* El código Java que ejecutó esta consulta: `com.adobe.granite.queries.impl.explain.query.ExplainQueryServlet::getHeuristics` para ayudar a identificar al creador de la consulta.

Con esta información, es posible optimizar esta consulta utilizando los métodos descritos en la [Optimización de consultas](#optimizing-queries) de este documento.
