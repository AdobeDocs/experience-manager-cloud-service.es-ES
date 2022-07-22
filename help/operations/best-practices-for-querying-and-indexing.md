---
title: Prácticas recomendadas para consultas e indexación
seo-title: Best Practices for Queries and Indexing
description: Este artículo proporciona directrices sobre cómo optimizar los índices y las consultas.
seo-description: This article provides guidelines on how to optimize your indexes and queries.
topic-tags: best-practices
source-git-commit: 85cbdaa6e6d01856005cb47f289d391fb44bd65e
workflow-type: tm+mt
source-wordcount: '1573'
ht-degree: 0%

---


# Prácticas recomendadas para consultas e indexación{#best-practices-for-queries-and-indexing}

A diferencia de las versiones anteriores en AEM as a Cloud Service, todos los aspectos operativos relativos a la indexación son automatizados. Esto permite a los desarrolladores centrarse en la creación de consultas eficientes y sus correspondientes definiciones de índice.

## Cuándo utilizar consultas {#when-to-use-queries}

Las consultas son una forma de obtener acceso al contenido, pero no la única. Por este motivo, debe evaluarse si las consultas son la forma mejor y más eficaz de acceder al contenido. En muchas situaciones, se puede acceder al contenido del repositorio de forma más eficaz por otros medios.

### Diseño de Repositorio y Taxonomía {#repository-and-taxonomy-design}

Al diseñar la taxonomía de un repositorio, es necesario tener en cuenta varios factores. Estos incluyen controles de acceso, localización, herencia de propiedades de componentes y páginas, entre otros.

Al diseñar una taxonomía que aborde estas preocupaciones, también es importante considerar la &quot;transferibilidad&quot; del diseño de indexación. En este contexto, la transferibilidad es la capacidad de una taxonomía que permite acceder al contenido de forma predecible en función de su ruta. Esto hará que el sistema sea más eficaz y fácil de mantener que uno que requiera ejecutar muchas consultas.

Además, al diseñar una taxonomía, es importante considerar si el orden es importante. En los casos en los que no se requiere orden explícito y se espera un gran número de nodos del mismo nivel, se prefiere utilizar un tipo de nodo no ordenado como `sling:Folder` o `oak:Unstructured`. En los casos en que se requiera la orden, `nt:unstructured` y `sling:OrderedFolder` sería más apropiado.

### Consultas en componentes {#queries-in-components}

Dado que las consultas pueden ser una de las operaciones más gravosas realizadas en un sistema AEM, es aconsejable evitarlas en los componentes. A menudo, hacer que se ejecuten varias consultas cada vez que se procesa una página puede degradar el rendimiento del sistema. Existen dos estrategias que se pueden utilizar para evitar ejecutar consultas al procesar componentes: **atravesar nodos** y **recuperación previa de resultados**.

### Recorrer nodos {#traversing-nodes}

Si el repositorio está diseñado de tal manera que permita un conocimiento previo de la ubicación de los datos requeridos, el código que recupera estos datos de las rutas necesarias se puede implementar sin tener que ejecutar consultas para encontrarlos.

Un ejemplo de esto sería la representación de contenido que se ajuste a una determinada categoría. Un método sería organizar el contenido con una propiedad de categoría que se pueda consultar para rellenar un componente que muestre elementos en una categoría.

Un mejor enfoque sería estructurar este contenido en una taxonomía por categoría para que se pueda recuperar manualmente.

Por ejemplo, si el contenido se almacena en una taxonomía similar a:

```xml
/content/myUnstructuredContent/parentCategory/childCategory/contentPiece
```

el `/content/myUnstructuredContent/parentCategory/childCategory` simplemente se puede recuperar, sus elementos secundarios se pueden analizar y utilizar para procesar el componente.

Además, cuando se trata de un conjunto de resultados pequeño o homogéneo, puede ser más rápido atravesar el repositorio y recopilar los nodos necesarios, en lugar de crear una consulta para devolver el mismo conjunto de resultados. Como consideración general, deben evitarse las consultas siempre que sea posible.

### Recuperación previa de resultados {#prefetching-results}

A veces, el contenido o los requisitos relacionados con el componente no permiten el uso de la transversal de nodos como método para recuperar los datos necesarios. En estos casos, es necesario ejecutar las consultas necesarias antes de procesar el componente para garantizar un rendimiento óptimo.

Si los resultados necesarios para el componente se pueden calcular en el momento en que se crea y no hay expectativa de que el contenido cambie, la consulta se puede ejecutar después de que se haya realizado un cambio.

Si los datos o el contenido cambian con regularidad, la consulta se puede ejecutar en una programación o a través de un oyente para buscar actualizaciones de los datos subyacentes. A continuación, los resultados se pueden escribir en una ubicación compartida del repositorio. Cualquier componente que necesite estos datos puede extraer los valores de este nodo único sin necesidad de ejecutar una consulta en tiempo de ejecución.
Se puede utilizar una estrategia similar para mantener el resultado en una caché en memoria, que se rellena al inicio y se actualiza cada vez que se realizan cambios (mediante un JCR ObservationListener o un Sling ResourceChangeListener).

## Optimización de consultas {#optimizing-queries}

La documentación de Oak proporciona un [información general de alto nivel sobre cómo se ejecutan las consultas](https://jackrabbit.apache.org/oak/docs/query/query-engine.html#query-processing). Esto forma la base de todas las actividades de optimización descritas en este documento.

AEM as a Cloud Service proporciona la herramienta de rendimiento de consultas, que está diseñada para admitir la implementación de consultas eficientes.
* Muestra consultas ya ejecutadas con sus características de rendimiento relevantes y el plan de consultas.
* Permite realizar consultas ad hoc en varios niveles, desde mostrar el plan de consultas hasta ejecutar la consulta completa.

Se puede acceder a la herramienta Rendimiento de las consultas a través de la [Developer Console en Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/developer-console.html?lang=es#queries). A diferencia de la herramienta de rendimiento Consulta de versiones anteriores de AEM 6.x, la herramienta de consulta de rendimiento proporcionada para AEM as a Cloud Service ofrece más información sobre los detalles de la ejecución de la consulta, que son útiles para mejorar una consulta.


En este gráfico se describe el enfoque general sobre cómo utilizar la herramienta de rendimiento de consultas para optimizar las consultas.
![Flujo de optimización de consulta](assets/query-optimization-flow.png)



### Uso de un índice {#use-an-index}

Cada consulta debe utilizar un índice para ofrecer un rendimiento óptimo. En la mayoría de los casos, los índices predefinidos existentes deberían ser suficientes para gestionar consultas.
A veces es necesario agregar propiedades personalizadas a un índice existente, por lo que se pueden consultar restricciones adicionales mediante este índice. Consulte [Búsqueda de contenido e indexación](/help/operations/indexing.md#changing-an-index) para obtener más información. La variable [Hoja de referencia de consultas JCR](#jcr-query-cheatsheet) describe cómo debe aparecer una definición de propiedad en un índice para admitir un tipo de consulta específico.



### Use los criterios adecuados

La restricción principal en cualquier consulta debe ser una coincidencia de propiedad, ya que este es el tipo más eficiente. Si se agregan más restricciones de propiedad, el resultado se limita aún más.
El motor de consulta solo tiene en cuenta un índice único; esto significa que un índice existente se puede y se debe personalizar agregándole más propiedades de índice personalizadas.

La variable [Hoja de referencia de consultas JCR](#jcr-query-cheatsheet) enumera las restricciones disponibles y también describe cómo debe aparecer una definición de índice para que se recoja. Utilice la variable [Herramienta Rendimiento de consulta](#query-performance-tool) para probar la consulta y asegurarse de que se utiliza el índice correcto y de que el motor de consulta no necesita evaluar restricciones fuera del índice.


### Solicitud

Si se solicita un orden específico del resultado, existen dos maneras de que el motor de consulta logre esto:

1. O el índice puede entregar el resultado completamente y en el orden correcto; esto funciona si las propiedades que se utilizan para la ordenación están anotadas con ```ordered=true``` en la definición de índice.
2. Si el motor de consulta debe realizar filtros fuera del índice o si la propiedad de orden no está anotada con la variable ```ordered=true``` , el motor de consulta también realiza el proceso de solicitud. Este caso requiere que el conjunto de resultados completo se lea en la memoria para la ordenación, lo que es mucho más lento que la primera opción.





### Restringir el tamaño del resultado

El tamaño recuperado del resultado de la consulta es un factor importante en el rendimiento de la consulta. Como el resultado se obtiene de forma diferida, existe una diferencia en solo obtener los primeros 20 resultados comparados con obtener 10 000 resultados, tanto en tiempo de ejecución como en uso de memoria.

Esto también significa que el tamaño del conjunto de resultados solo se puede determinar correctamente si se recuperan todos los resultados. Por este motivo, el conjunto de resultados recuperados siempre debe estar limitado, ya sea aumentando la consulta (consulte [Hoja de referencia de consultas JCR](#jcr-query-cheatsheet) para detalles) o limitando las lecturas de los resultados.
Este límite también evita que el motor de consultas acceda al **límite transversal** de 100.000 nodos, lo que conduce a una parada forzada de la consulta.

Consulte la sección [Consultas con resultados grandes](#queries-with-large-result-sets) a continuación si un conjunto de resultados potencialmente grande debe procesarse completamente.


## Hoja de referencia de consultas JCR

Para apoyar la creación de consultas JCR eficientes y definiciones de índices, la variable [Hoja de referencia de consulta JCR](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/practices/best-practices-for-queries-and-indexing.html#jcrquerycheatsheet) está disponible para su descarga y uso como referencia durante el desarrollo. Contiene consultas de ejemplo para QueryBuilder, XPath y SQL-2, que abarcan varios escenarios que se comportan de forma diferente en términos del rendimiento de la consulta. También proporciona recomendaciones sobre cómo crear o personalizar índices Oak. El contenido de esta hoja de referencia se aplica a AEM 6.5 y AEM as a Cloud Service.


## Consultas con grandes conjuntos de resultados

Aunque se recomienda evitar consultas con un conjunto de resultados grande, hay casos válidos en los que se debe procesar un resultado grande. A menudo se desconoce por adelantado el tamaño del resultado, por lo que deben tomarse algunas precauciones para que el procesamiento sea fiable.

* la consulta no debe ejecutarse dentro de una solicitud; en su lugar, la consulta debe ejecutarse como parte de un trabajo de Sling o de un flujo de trabajo de AEM. Estas no tienen limitaciones en su tiempo de ejecución total y se reinician en caso de que la instancia se reduzca durante el procesamiento de la consulta y sus resultados.
* Para superar el límite de consultas de 100.000 nodos, lea debe considerar utilizar [Paginación de conjunto de claves](https://jackrabbit.apache.org/oak/docs/query/query-engine.html#Keyset_Pagination) y dividir la consulta en varias subconsultas.



## Consulta a través del repositorio

Las consultas que atraviesan el repositorio no utilizan un índice y están registrando mensajes como este:

```text
28.06.2022 13:32:52.804 *WARN* [127.0.0.1 [1656415972414] POST /libs/settings/granite/operations/diagnosis/granite_queryperformance.explain.json HTTP/1.1] org.apache.jackrabbit.oak.plugins.index.Cursors$TraversingCursor Traversed 98000 nodes with filter Filter(query=select [jcr:path], [jcr:score], * from [nt:base] as a /* xpath: //* */, path=*) called by com.adobe.granite.queries.impl.explain.query.ExplainQueryServlet.getHeuristics; consider creating an index or changing the query
```

Este fragmento de registro contiene información relevante:

* la consulta en sí: ```//* ```
* el código java que ejecutó esta consulta: ```com.adobe.granite.queries.impl.explain.query.ExplainQueryServlet::getHeuristics```; esto ayuda a identificar al creador de esta consulta.

Con esta información es posible optimizar esta consulta utilizando los métodos descritos en [Optimización de consultas](#optimizing-queries).