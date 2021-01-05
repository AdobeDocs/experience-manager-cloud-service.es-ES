---
title: API de consulta Builder
description: La funcionalidad del Generador de Consultas de uso compartido de recursos se expone mediante una API de Java y una API de REST.
translation-type: tm+mt
source-git-commit: cfd54f0cd84cef72b6f2fad1a85132c312a19348
workflow-type: tm+mt
source-wordcount: '2069'
ht-degree: 0%

---


# API del Generador de consultas {#query-builder-api}

El Generador de Consultas oferta una forma sencilla de consultar el repositorio de contenido de AEM. La funcionalidad se expone mediante una API de Java y una API de REST. Este documento describe estas API.

El generador de consultas del lado del servidor ([`QueryBuilder`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/QueryBuilder.html)) aceptará una descripción de consulta, creará y ejecutará una consulta XPath, opcionalmente filtrará el conjunto de resultados y también extraerá facetas, si lo desea.

La descripción de la consulta es simplemente un conjunto de predicados ([`Predicate`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/Predicate.html)). Algunos ejemplos incluyen un predicado de texto completo, que corresponde a la función `jcr:contains()` en XPath.

Para cada tipo de predicado, hay un componente de evaluador ([`PredicateEvaluator`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/eval/PredicateEvaluator.html)) que sabe cómo manejar ese predicado específico para XPath, filtrado y extracción de facetas. Es muy fácil crear evaluadores personalizados, que se conectan a través del tiempo de ejecución del componente OSGi.

La API de REST proporciona acceso a exactamente las mismas funciones a través de HTTP y las respuestas se envían en JSON.

>[!NOTE]
>
>La API de QueryBuilder se crea mediante la API de JCR. También puede realizar la consulta del JCR AEM mediante la API de JCR desde un paquete OSGi. Para obtener más información, consulte [Consulta de datos de Adobe Experience Manager mediante la API de JCR](https://helpx.adobe.com/experience-manager/using/querying-experience-manager-data-using1.html).

## Sesión de Gem {#gem-session}

[AEM ](https://helpx.adobe.com/experience-manager/kt/eseminars/gems/aem-index.html) Gemsis una serie de inmersiones técnicas profundas en Adobe Experience Manager realizadas por expertos en Adobe.

Puede [revisar la sesión dedicada al creador de consultas](https://helpx.adobe.com/experience-manager/kt/eseminars/gems/aem-search-forms-using-querybuilder.html) para obtener información general y utilizar la herramienta.

## Consultas de muestra {#sample-queries}

Estos ejemplos se proporcionan en notación de estilo de las propiedades Java. Para usarlos con la API de Java, utilice Java `HashMap` como en el ejemplo de API que se muestra a continuación.

Para el servlet `QueryBuilder` JSON, cada ejemplo incluye un vínculo de muestra a una instalación AEM (en la ubicación predeterminada, `http://<host>:<port>`). Tenga en cuenta que debe iniciar sesión en la instancia de AEM antes de utilizar estos vínculos.

>[!CAUTION]
>
>De forma predeterminada, el servlet JSON del generador de consultas muestra un máximo de 10 visitas.
>
>Añadir el siguiente parámetro permite que el servlet muestre todos los resultados de la consulta:
>
>`p.limit=-1`

>[!NOTE]
>
>Para vista de los datos JSON devueltos en el navegador, puede que desee utilizar un complemento como JSONView para Firefox.

### Devolución de todos los resultados {#returning-all-results}

La siguiente consulta **devolverá diez resultados** (o para ser precisos, un máximo de diez), pero le informará del **Número de visitas:** que están realmente disponibles:

`http://<host>:<port>/bin/querybuilder.json?path=/content&1_property=sling:resourceType&1_property.value=wknd/components/structure/page&1_property.operation=like&orderby=path`

```xml
path=/content
1_property=sling:resourceType
1_property.value=wknd/components/structure/page
1_property.operation=like
orderby=path
```

La misma consulta (con el parámetro `p.limit=-1`) **devolverá todos los resultados** (puede ser un número alto según la instancia):

`http://<host>:<port>/bin/querybuilder.json?path=/content&1_property=sling:resourceType&1_property.value=wknd/components/structure/page&1_property.operation=like&orderby=path&p.limit=-1`

```xml
path=/content
1_property=sling:resourceType
1_property.value=wknd/components/structure/page
1_property.operation=like
p.limit=-1
orderby=path
```

### Uso de p.imagestotal para devolver los resultados {#using-p-guesstotal-to-return-the-results}

El propósito del parámetro `p.guessTotal` es devolver el número adecuado de resultados que se pueden mostrar combinando los valores mínimos viables `p.offset` y `p.limit`. La ventaja de utilizar este parámetro es que se ha mejorado el rendimiento con grandes conjuntos de resultados. Esto evita calcular el total completo (por ejemplo, llamando a `result.getSize()`) y leer todo el conjunto de resultados, optimizado hasta el motor OAK y el índice. Esto puede ser una diferencia significativa cuando hay cientos de miles de resultados, tanto en el tiempo de ejecución como en el uso de la memoria.

La desventaja del parámetro es que los usuarios no ven el total exacto. Pero puede establecer un número mínimo como `p.guessTotal=1000` para que siempre lea hasta 1000, de modo que obtenga los totales exactos para los conjuntos de resultados más pequeños, pero si es mayor que eso, sólo puede mostrar &quot;y más&quot;.

Añada `p.guessTotal=true` a la consulta siguiente para ver cómo funciona:

`http://<host>:<port>/bin/querybuilder.json?path=/content&1_property=sling:resourceType&1_property.value=wknd/components/structure/page&1_property.operation=like&p.guessTotal=true&orderby=path`

```xml
path=/content
1_property=sling:resourceType
1_property.value=wknd/components/structure/page
1_property.operation=like
p.guessTotal=true
orderby=path
```

La consulta devolverá el `p.limit` valor predeterminado de `10` resultados con un desplazamiento `0`:

```xml
"success": true,
"results": 10,
"total": 10,
"more": true,
"offset": 0,
```

También puede utilizar un valor numérico para contar hasta un número personalizado de resultados máximos. Utilice la misma consulta que la anterior, pero cambie el valor de `p.guessTotal` a `50`:

`http://<host>:<port>/bin/querybuilder.json?path=/content&1_property=sling:resourceType&1_property.value=wknd/components/structure/page&1_property.operation=like&p.guessTotal=50&orderby=path`

Devolverá un número con el mismo límite predeterminado de 10 resultados con un desplazamiento de 0, pero solo mostrará un máximo de 50 resultados:

```xml
"success": true,
"results": 10,
"total": 50,
"more": true,
"offset": 0,
```

### Implementación de Paginación {#implementing-pagination}

De forma predeterminada, el Generador de Consultas también proporciona el número de visitas. Dependiendo del tamaño del resultado, esto puede llevar mucho tiempo ya que determinar el recuento exacto implica comprobar cada resultado en busca de controles de acceso. Principalmente, el total se utiliza para implementar la paginación para la interfaz de usuario del usuario final. Dado que determinar el recuento exacto puede ser lento, se recomienda utilizar la función adivinar total para implementar la paginación.

Por ejemplo, la interfaz de usuario puede adaptar el siguiente método:

* Obtener y mostrar el recuento preciso del número total de visitas ([SearchResult.getTotalMatches()](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/result/SearchResult.html#gettotalmatches) o total en la respuesta `querybuilder.json`) son menores o iguales a 100;
* Establezca `guessTotal` en 100 mientras realiza la llamada al Generador de Consultas.

* La respuesta puede tener el siguiente resultado:

   * `total=43`,  `more=false` - Indica que el número total de visitas es 43. La interfaz de usuario puede mostrar hasta diez resultados como parte de la primera página y proporcionar paginación para las tres páginas siguientes. También puede utilizar esta implementación para mostrar un texto descriptivo como **&quot;43 results found&quot;**.
   * `total=100`,  `more=true` - Indica que el número total de visitas es bueno a más de 100 y que no se conoce el recuento exacto. La interfaz de usuario puede mostrar hasta diez como parte de la primera página y proporcionar paginación para las diez páginas siguientes. También puede usar esto para mostrar un texto como **&quot;más de 100 resultados encontrados&quot;**. A medida que el usuario va a las páginas siguientes, las llamadas realizadas al Generador de Consultas aumentarán el límite de `guessTotal` y también de los parámetros `offset` y `limit`.

`guessTotal` también debe utilizarse en casos en los que la interfaz de usuario necesite utilizar el desplazamiento infinito, para evitar que el Generador de Consultas determine el recuento exacto de visitas.

### Buscar archivos jar y ordenarlos, los más recientes primero {#find-jar-files-and-order-them-newest-first}

`http://<host>:<port>/bin/querybuilder.json?type=nt:file&nodename=*.jar&orderby=@jcr:content/jcr:lastModified&orderby.sort=desc`

```xml
type=nt:file
nodename=*.jar
orderby=@jcr:content/jcr:lastModified
orderby.sort=desc
```

### Buscar todas las páginas y ordenarlas por última modificación {#find-all-pages-and-order-them-by-last-modified}

`http://<host>:<port>/bin/querybuilder.json?type=cq:Page&orderby=@jcr:content/cq:lastModified`

```xml
type=cq:Page
orderby=@jcr:content/cq:lastModified
```

### Buscar todas las páginas y pedirlas por última modificación, De bajada {#find-all-pages-and-order-them-by-last-modified-but-descending}

`http://<host>:<port>/bin/querybuilder.json?type=cq:Page&orderby=@jcr:content/cq:lastModified&orderby.sort=desc`

```xml
type=cq:Page
orderby=@jcr:content/cq:lastModified
orderby.sort=desc
```

### Búsqueda de texto completo, ordenada por puntuación {#fulltext-search-ordered-by-score}

`http://<host>:<port>/bin/querybuilder.json?fulltext=Management&orderby=@jcr:score&orderby.sort=desc`

```xml
fulltext=Management
orderby=@jcr:score
orderby.sort=desc
```

### Buscar páginas con una etiqueta determinada {#search-for-pages-tagged-with-a-certain-tag}

`http://<host>:<port>/bin/querybuilder.json?type=cq:Page&tagid=wknd:activity/cycling&tagid.property=jcr:content/cq:tags`

```xml
type=cq:Page
tagid=wknd:activity/cycling
tagid.property=jcr:content/cq:tags
```

Utilice el predicado `tagid` como en el ejemplo si conoce el ID de etiqueta explícito.

Utilice el predicado `tag` para la ruta de título de la etiqueta (sin espacios).

Dado que, en el ejemplo anterior, está buscando páginas (`cq:Page` nodos), debe utilizar la ruta relativa desde ese nodo para el predicado `tagid.property`, que es `jcr:content/cq:tags`. De manera predeterminada, el `tagid.property` sería `cq:tags`.

### Buscar varias rutas (mediante grupos) {#search-under-multiple-paths-using-groups}

`http://<host>:<port>/bin/querybuilder.json?fulltext=Experience&group.1_path=/content/wknd/us/en/magazine&group.2_path=/content/wknd/us/en/adventures&group.p.or=true`

```xml
fulltext=Experience
group.p.or=true
group.1_path=/content/wknd/us/en/magazine
group.2_path=/content/wknd/us/en/adventures
```

Esta consulta utiliza un *grupo* (denominado `group`), que actúa para delimitar las subexpresiones dentro de una consulta, de manera similar a como lo hacen los paréntesis en notaciones más estándar. Por ejemplo, la consulta anterior podría expresarse con un estilo más familiar:

`"Experience" and ("/content/wknd/us/en/magazine" or "/content/wknd/us/en/adventures")`

Dentro del grupo en el ejemplo, el predicado `path` se utiliza varias veces. Para diferenciar y ordenar las dos instancias del predicado (se requiere orden para algunos predicados), debe anteponer los predicados con `N_` donde `N` es el índice de pedidos. En el ejemplo anterior, los predicados resultantes son `1_path` y `2_path`.

El `p` en `p.or` es un delimitador especial que indica que lo que sigue (en este caso, un `or`) es un *parámetro* del grupo, en lugar de un subpredicado del grupo, como `1_path`.

Si no se proporciona ningún `p.or`, entonces todos los predicados son ANDed juntos, es decir, cada resultado debe satisfacer todos los predicados.

>[!NOTE]
>
>No se puede utilizar el mismo prefijo numérico en una sola consulta, ni siquiera para predicados diferentes.

### Buscar propiedades {#search-for-properties}

Aquí está buscando todas las páginas de una plantilla determinada, utilizando la propiedad `cq:template`:

`http://<host>:<port>/bin/querybuilder.json?property=cq%3atemplate&property.value=%2fconf%2fwknd%2fsettings%2fwcm%2ftemplates%2fadventure-page-template&type=cq%3aPageContent`

```xml
type=cq:PageContent
property=cq:template
property.value=/conf/wknd/settings/wcm/templates/adventure-page-template
```

Esto tiene el inconveniente de que se devuelven los nodos `jcr:content` de las páginas, no las páginas mismas. Para solucionarlo, puede buscar por ruta relativa:

`http://<host>:<port>/bin/querybuilder.json?property=jcr%3acontent%2fcq%3atemplate&property.value=%2fconf%2fwknd%2fsettings%2fwcm%2ftemplates%2fadventure-page-template&type=cq%3aPage`

```xml
type=cq:Page
property=jcr:content/cq:template
property.value=/conf/wknd/settings/wcm/templates/adventure-page-template
```

### Buscar varias propiedades {#search-for-multiple-properties}

Cuando se utiliza el predicado de propiedades varias veces, hay que volver a agregar los prefijos numéricos:

`http://<host>:<port>/bin/querybuilder.json?1_property=jcr%3acontent%2fcq%3atemplate&1_property.value=%2fconf%2fwknd%2fsettings%2fwcm%2ftemplates%2fadventure-page-template&2_property=jcr%3acontent%2fjcr%3atitle&2_property.value=Cycling%20Tuscany&type=cq%3aPage`

```xml
type=cq:Page
1_property=jcr:content/cq:template
1_property.value=/conf/wknd/settings/wcm/templates/adventure-page-template
2_property=jcr:content/jcr:title
2_property.value=Cycling Tuscany
```

### Buscar varios valores de propiedad {#search-for-multiple-property-values}

Para evitar grupos grandes cuando desee buscar valores múltiples de una propiedad (`"A" or "B" or "C"`), puede proporcionar valores múltiples al predicado `property`:

`http://<host>:<port>/bin/querybuilder.json?property=jcr%3atitle&property.1_value=Cycling%20Tuscany&property.2_value=Ski%20Touring&property.3_value=Whistler%20Mountain%20Biking`

```xml
property=jcr:title
property.1_value=Cycling Tuscany
property.2_value=Ski Touring
property.3_value=Whistler Mountain Biking
```

Para propiedades de varios valores, también puede requerir que coincidan varios valores (`"A" and "B" and "C"`):

`http://<host>:<port>/bin/querybuilder.json?property=jcr%3atitle&property.and=true&property.1_value=Cycling%20Tuscany&property.2_value=Ski%20Touring&property.3_value=Whistler%20Mountain%20Biking`

```xml
property=jcr:title
property.and=true
property.1_value=Cycling Tuscany
property.2_value=Ski Touring
property.3_value=Whistler Mountain Biking
```

## Perfeccionamiento de lo que se devuelve {#refining-what-is-returned}

De forma predeterminada, el servlet JSON de QueryBuilder devolverá un conjunto predeterminado de propiedades para cada nodo del resultado de búsqueda (por ejemplo, ruta, nombre, título, etc.). Para obtener el control sobre qué propiedades se devuelven, puede realizar una de las siguientes acciones:

Especifique

```xml
p.hits=full
```

en cuyo caso se incluirán todas las propiedades de cada nodo:

`http://<host>:<port>/bin/querybuilder.json?p.hits=full&property=jcr%3atitle&property.value=Cycling%20Tuscany`

```xml
property=jcr:title
property.value=Cycling Tuscany
p.hits=full
```

Uso

```xml
p.hits=selective
```

y especifique las propiedades en las que desea entrar

```xml
p.properties
```

separado por un espacio:

`http://<host>:<port>/bin/querybuilder.json?p.hits=selective&p.properties=sling%3aresourceType%20jcr%3aprimaryType&property=jcr%3atitle&property.value=Cycling%20Tuscany`

```xml
property=jcr:title
property.value=Cycling Tuscany
p.hits=selective
p.properties=sling:resourceType jcr:primaryType
```

Otra cosa que puede hacer es incluir nodos secundarios en la respuesta del Generador de Consultas. Para ello, debe especificar

```xml
p.nodedepth=n
```

donde `n` es el número de niveles que desea que la consulta devuelva. Tenga en cuenta que para que se devuelva un nodo secundario, debe especificarlo el selector de propiedades

```xml
p.hits=full
```

Ejemplo:

`http://<host>:<port>/bin/querybuilder.json?p.hits=full&p.nodedepth=5&property=jcr%3atitle&property.value=Cycling%20Tuscany`

```xml
property=jcr:title
property.value=Cycling Tuscany
p.hits=full
p.nodedepth=5
```

## Más predicados {#morepredicates}

Para obtener más predicados, consulte la página [Referencia de predicado del generador de Consultas](query-builder-predicates.md).

También puede comprobar el [Javadoc para las `PredicateEvaluator` clases](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/eval/PredicateEvaluator.html). El Javadoc de estas clases contiene la lista de propiedades que puede utilizar.

El prefijo del nombre de clase (por ejemplo, `similar` en [`SimilarityPredicateEvaluator`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/eval/SimilarityPredicateEvaluator.html)) es la *propiedad principal* de la clase. Esta propiedad también es el nombre del predicado que se va a usar en la consulta (en minúscula).

Para estas propiedades principales, puede reducir la consulta y utilizar `similar=/content/en` en lugar de la variante completa `similar.similar=/content/en`. El formulario completo debe utilizarse para todas las propiedades no principales de una clase.

## Ejemplo de uso de API del Generador de Consultas {#example-query-builder-api-usage}

```java
   String fulltextSearchTerm = "WKND";

    // create query description as hash map (simplest way, same as form post)
    Map<String, String> map = new HashMap<String, String>();

// create query description as hash map (simplest way, same as form post)
    map.put("path", "/content");
    map.put("type", "cq:Page");
    map.put("group.p.or", "true"); // combine this group with OR
    map.put("group.1_fulltext", fulltextSearchTerm);
    map.put("group.1_fulltext.relPath", "jcr:content");
    map.put("group.2_fulltext", fulltextSearchTerm);
    map.put("group.2_fulltext.relPath", "jcr:content/@cq:tags");

    // can be done in map or with Query methods
    map.put("p.offset", "0"); // same as query.setStart(0) below
    map.put("p.limit", "20"); // same as query.setHitsPerPage(20) below

    Query query = builder.createQuery(PredicateGroup.create(map), session);
    query.setStart(0);
    query.setHitsPerPage(20);

    SearchResult result = query.getResult();

    // paging metadata
    int hitsPerPage = result.getHits().size(); // 20 (set above) or lower
    long totalMatches = result.getTotalMatches();
    long offset = result.getStartIndex();
    long numberOfPages = totalMatches / 20;

    //Place the results in XML to return to client
    DocumentBuilderFactory factory = DocumentBuilderFactory.newInstance();
    DocumentBuilder builder = factory.newDocumentBuilder();
    Document doc = builder.newDocument();

    //Start building the XML to pass back to the AEM client
    Element root = doc.createElement( "results" );
    doc.appendChild( root );

    // iterating over the results
    for (Hit hit : result.getHits()) {
       String path = hit.getPath();

      //Create a result element
      Element resultel = doc.createElement( "result" );
      root.appendChild( resultel );

      Element pathel = doc.createElement( "path" );
      pathel.appendChild( doc.createTextNode(path ) );
      resultel.appendChild( pathel );
    }
```

La misma consulta ejecutada a través de HTTP mediante el servlet Consulta Builder (JSON):

`http://<host>:<port>/bin/querybuilder.json?path=/content&type=cq:Page&group.p.or=true&group.1_fulltext=WKND&group.1_fulltext.relPath=jcr:content&group.2_fulltext=WKND&group.2_fulltext.relPath=jcr:content/@cq:tags&p.offset=0&p.limit=20`

## Almacenamiento y carga de Consultas {#storing-and-loading-queries}

Las consultas se pueden almacenar en el repositorio para que pueda usarlas más adelante. El `QueryBuilder` proporciona el método `storeQuery` con la siguiente firma:

```java
void storeQuery(Query query, String path, boolean createFile, Session session) throws RepositoryException, IOException;
```

Al utilizar el método [`QueryBuilder#storeQuery`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/QueryBuilder.html#storequerycomdaycqsearchqueryjavalangstringbooleanjavaxjcrsession), el `Query` dado se almacena en el repositorio como archivo o como propiedad según el valor del argumento `createFile`. El siguiente ejemplo muestra cómo guardar un `Query` en la ruta `/mypath/getfiles` como archivo:

```java
builder.storeQuery(query, "/mypath/getfiles", true, session);
```

Cualquier consulta almacenada anteriormente se puede cargar desde el repositorio mediante el método [`QueryBuilder#loadQuery`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/QueryBuilder.html#loadqueryjavalangstringjavaxjcrsession):

```java
Query loadQuery(String path, Session session) throws RepositoryException, IOException
```

Por ejemplo, un `Query` almacenado en la ruta `/mypath/getfiles` se puede cargar con el siguiente fragmento de código:

```java
Query loadedQuery = builder.loadQuery("/mypath/getfiles", session);
```

## Prueba y depuración {#testing-and-debugging}

Para reproducir y depurar consultas del Generador de Consultas, puede utilizar la consola de depuración de Consulta Builder en

`http://<host>:<port>/libs/cq/search/content/querydebug.html`

o bien, el servlet JSON de Consulta Builder en

`http://<host>:<port>/bin/querybuilder.json?path=/tmp`

`path=/tmp` es sólo un ejemplo.

### Depuración general de Recommendations {#general-debugging-recommendations}

### Obtenga XPath explicable mediante el registro {#obtain-explain-able-xpath-via-logging}

Explicar **todas** consultas durante el ciclo de desarrollo con respecto al conjunto de índices de destinatario.

1. Habilitar los registros DEBUG para QueryBuilder para obtener la consulta XPath subyacente y explicable
   * Ir a `https://<host>:<port>/system/console/slinglog`. Cree un nuevo registrador para `com.day.cq.search.impl.builder.QueryImpl` en **DEBUG**.
1. Una vez que DEBUG se haya habilitado para la clase anterior, los registros mostrarán el XPath generado por el Generador de Consultas.
1. Copie la consulta XPath de la entrada de registro de la consulta asociada del Generador de Consultas. Por ejemplo:
   * `com.day.cq.search.impl.builder.QueryImpl XPath query: /jcr:root/content//element(*, cq:Page)[(jcr:contains(jcr:content, "WKND") or jcr:contains(jcr:content/@cq:tags, "WKND"))]`
1. Pegue la consulta XPath en Explicar Consulta como XPath para obtener el plan de consulta.

### Obtenga XPath explicable mediante el depurador del Generador de Consultas {#obtain-explain-able-xpath-via-the-query-builder-debugger}

Utilice el depurador AEM Consulta Builder para generar una consulta XPath explicable.

![Consulta Builder Debugger](assets/query-builder-debugger.png)

1. Proporcione la consulta del Generador de Consultas en el depurador del Generador de Consultas
1. Ejecutar la búsqueda
1. Obtenga el XPath generado
1. Pegue la consulta XPath en Explicar Consulta como XPath para obtener el plan de consulta

>[!NOTE]
>
>Las consultas que no son de Consulta Builder (XPath, JCR-SQL2) se pueden proporcionar directamente para explicar la Consulta.

## Depuración de Consultas con Registro {#debugging-queries-with-logging}

>[!NOTE]
>
>La configuración de los registradores se describe en el documento [Registro](/help/implementing/developing/introduction/logging.md).

Salida de registro (nivel INFO) de la implementación del generador de consultas al ejecutar la consulta descrita en la sección anterior [Pruebas y depuración:](#testing-and-debugging)

```xml
com.day.cq.search.impl.builder.QueryImpl executing query (predicate tree):
null=group: limit=20, offset=0[
    {group=group: or=true[
        {1_fulltext=fulltext: fulltext=WKND, relPath=jcr:content}
        {2_fulltext=fulltext: fulltext=WKND, relPath=jcr:content/@cq:tags}
    ]}
    {path=path: path=/content}
    {type=type: type=cq:Page}
]
com.day.cq.search.impl.builder.QueryImpl XPath query: /jcr:root/content//element(*, cq:Page)[(jcr:contains(jcr:content, "WKND") or jcr:contains(jcr:content/@cq:tags, "WKND"))]
com.day.cq.search.impl.builder.QueryImpl no filtering predicates
com.day.cq.search.impl.builder.QueryImpl query execution took 69 ms
```

Si tiene una consulta que utiliza evaluadores predicados que filtren o que utilizan un orden personalizado por comparador, esto también se anotará en la consulta:

```xml
com.day.cq.search.impl.builder.QueryImpl executing query (predicate tree):
null=group: [
    {nodename=nodename: nodename=*.jar}
    {orderby=orderby: orderby=@jcr:content/jcr:lastModified}
    {type=type: type=nt:file}
]
com.day.cq.search.impl.builder.QueryImpl custom order by comparator: jcr:content/jcr:lastModified
com.day.cq.search.impl.builder.QueryImpl XPath query: //element(*, nt:file)
com.day.cq.search.impl.builder.QueryImpl filtering predicates: {nodename=nodename: nodename=*.jar}
com.day.cq.search.impl.builder.QueryImpl query execution took 272 ms
```

## Vínculos Javadoc {#javadoc-links}

| **Javadoc** | **Descripción** |
|---|---|
| [com.day.cq.search](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/package-summary.html) | Generador de Consultas básico y API de Consulta |
| [com.day.cq.search.result](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/result/package-summary.html) | API de resultado |
| [com.day.cq.search.facets](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/facets/package-summary.html) | Facetas |
| [com.day.cq.search.facets.bucket](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/facets/buckets/package-summary.html) | Cubos (contenidos en facetas) |
| [com.day.cq.search.eval](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/eval/package-summary.html) | Predicar evaluadores |
| [com.day.cq.search.facets.extractores](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/facets/extractors/package-summary.html) | Extractores de facetas (para evaluadores) |
| [com.day.cq.search.writer](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/writer/package-summary.html) | Archivo servlet JSON Result Hit Writer para Consulta Builder (`/bin/querybuilder.json`) |
