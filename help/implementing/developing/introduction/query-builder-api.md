---
title: API del Generador de consultas
description: La funcionalidad del Generador de consultas de Asset Share se expone a través de una API de Java y una API de REST.
exl-id: d5f22422-c9da-4c9d-b81c-ffa5ea7cdc87
source-git-commit: ca849bd76e5ac40bc76cf497619a82b238d898fa
workflow-type: tm+mt
source-wordcount: '2040'
ht-degree: 0%

---

# API del Generador de consultas {#query-builder-api}

El Generador de consultas ofrece una forma sencilla de consultar el repositorio de contenido de AEM. La funcionalidad se expone a través de una API de Java y una API de REST. Este documento describe estas API.

El generador de consultas del lado del servidor ([`QueryBuilder`](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/search/QueryBuilder.html)) aceptará una descripción de consulta, creará y ejecutará una consulta XPath, opcionalmente filtrará el conjunto de resultados y también extraerá facetas, si lo desea.

La descripción de la consulta es simplemente un conjunto de predicados ([`Predicate`](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/search/Predicate.html)). Algunos ejemplos son un predicado de texto completo, que corresponde a la variable `jcr:contains()` en XPath.

Para cada tipo de predicado, hay un componente de evaluador ([`PredicateEvaluator`](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/search/eval/PredicateEvaluator.html)) que sabe cómo manejar ese predicado específico para XPath, filtros y extracción de facetas. Es muy fácil crear evaluadores personalizados, que están conectados a través del tiempo de ejecución del componente OSGi.

La API de REST proporciona acceso a exactamente las mismas funciones a través de HTTP con respuestas enviadas en JSON.

>[!NOTE]
>
>La API de QueryBuilder se crea mediante la API de JCR. También puede consultar el JCR AEM utilizando la API JCR desde un paquete OSGi. Para obtener más información, consulte [Consulta de datos de Adobe Experience Manager mediante la API de JCR](https://helpx.adobe.com/experience-manager/using/querying-experience-manager-data-using1.html).

## Sesión de Gem {#gem-session}

[AEM](https://helpx.adobe.com/experience-manager/kt/eseminars/gems/aem-index.html) es una serie de análisis técnicos en Adobe Experience Manager que ofrecen los expertos en Adobe.

Puede [revise la sesión dedicada al generador de consultas](https://helpx.adobe.com/experience-manager/kt/eseminars/gems/aem-search-forms-using-querybuilder.html) para obtener información general y utilizar la herramienta.

## Consultas de ejemplo {#sample-queries}

Estos ejemplos se proporcionan en notación de estilo de propiedades Java. Para utilizarlos con la API de Java, utilice un Java `HashMap` como en el ejemplo de API que sigue.

Para la variable `QueryBuilder` Servlet JSON, cada ejemplo incluye un vínculo de ejemplo a una instalación AEM (en la ubicación predeterminada, `http://<host>:<port>`). Tenga en cuenta que debe iniciar sesión en la instancia de AEM antes de utilizar estos vínculos.

>[!CAUTION]
>
>De forma predeterminada, el servlet JSON del generador de consultas muestra un máximo de 10 visitas.
>
>Añadir el siguiente parámetro permite que el servlet muestre todos los resultados de la consulta:
>
>`p.limit=-1`

>[!NOTE]
>
>Para ver los datos JSON devueltos en su navegador, es posible que desee utilizar un complemento como JSONView para Firefox.

### Devolver todos los resultados {#returning-all-results}

La siguiente consulta **devolver diez resultados** (o, para ser precisos, un máximo de diez), pero infórmele de la **Número de visitas:** que están realmente disponibles:

`http://<host>:<port>/bin/querybuilder.json?path=/content&1_property=sling:resourceType&1_property.value=wknd/components/structure/page&1_property.operation=like&orderby=path`

```xml
path=/content
1_property=sling:resourceType
1_property.value=wknd/components/structure/page
1_property.operation=like
orderby=path
```

La misma consulta (con el parámetro `p.limit=-1`) **devolver todos los resultados** (puede ser un número elevado en función de la instancia):

`http://<host>:<port>/bin/querybuilder.json?path=/content&1_property=sling:resourceType&1_property.value=wknd/components/structure/page&1_property.operation=like&orderby=path&p.limit=-1`

```xml
path=/content
1_property=sling:resourceType
1_property.value=wknd/components/structure/page
1_property.operation=like
p.limit=-1
orderby=path
```

### Uso de p.supongoTotal para devolver los resultados {#using-p-guesstotal-to-return-the-results}

El propósito del `p.guessTotal` es devolver el número apropiado de resultados que se pueden mostrar combinando el mínimo viable `p.offset` y `p.limit` valores. La ventaja de utilizar este parámetro es que se ha mejorado el rendimiento con grandes conjuntos de resultados. Esto evita calcular el total completo (p. ej., llamar a `result.getSize()`) y leyendo todo el conjunto de resultados, optimizado hasta el motor OAK y el índice. Esto puede ser una diferencia significativa cuando hay cientos de miles de resultados, tanto en el tiempo de ejecución como en el uso de la memoria.

La desventaja del parámetro es que los usuarios no ven el total exacto. Pero puede establecer un número mínimo como `p.guessTotal=1000` así que siempre leerá hasta 1000, por lo que obtendrá totales exactos para conjuntos de resultados más pequeños, pero si es más que eso, solo podrá mostrar &quot;y más&quot;.

Agregar `p.guessTotal=true` consulte la siguiente consulta para ver cómo funciona:

`http://<host>:<port>/bin/querybuilder.json?path=/content&1_property=sling:resourceType&1_property.value=wknd/components/structure/page&1_property.operation=like&p.guessTotal=true&orderby=path`

```xml
path=/content
1_property=sling:resourceType
1_property.value=wknd/components/structure/page
1_property.operation=like
p.guessTotal=true
orderby=path
```

La consulta devolverá el valor `p.limit` predeterminado de `10` resultados con un `0` offset:

```xml
"success": true,
"results": 10,
"total": 10,
"more": true,
"offset": 0,
```

También puede utilizar un valor numérico para contar hasta un número personalizado de resultados máximos. Utilice la misma consulta que la anterior, pero cambie el valor de `p.guessTotal` a `50`:

`http://<host>:<port>/bin/querybuilder.json?path=/content&1_property=sling:resourceType&1_property.value=wknd/components/structure/page&1_property.operation=like&p.guessTotal=50&orderby=path`

Devuelve un número con el mismo límite predeterminado de 10 resultados con un desplazamiento de 0, pero solo muestra un máximo de 50 resultados:

```xml
"success": true,
"results": 10,
"total": 50,
"more": true,
"offset": 0,
```

### Implementación de paginación {#implementing-pagination}

De forma predeterminada, el Generador de consultas también proporcionaría el número de visitas. Dependiendo del tamaño del resultado, esto puede tardar mucho tiempo, ya que determinar el recuento preciso implica comprobar cada resultado para el control de acceso. La mayoría del total se utiliza para implementar la paginación para la interfaz de usuario del usuario final. Como determinar el recuento exacto puede ser lento, se recomienda utilizar la función adivinarTotal para implementar la paginación.

Por ejemplo, la interfaz de usuario puede adaptar el siguiente enfoque:

* Obtenga y muestre el recuento preciso del número total de visitas ([SearchResult.getTotalMatches()](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/search/result/SearchResult.html#getTotalMatches) o total en la variable `querybuilder.json` Respuesta) son inferiores o iguales a 100;
* Establezca `guessTotal` a 100 mientras realiza la llamada al Generador de consultas.

* La respuesta puede tener el siguiente resultado:

   * `total=43`, `more=false` - Indica que el número total de visitas es 43. La interfaz de usuario puede mostrar hasta diez resultados como parte de la primera página y proporcionar paginación para las tres páginas siguientes. También puede utilizar esta implementación para mostrar un texto descriptivo como **&quot;Se encontraron 43 resultados&quot;**.
   * `total=100`, `more=true` - Indica que el número total de visitas es bueno a más de 100 y que no se conoce el recuento exacto. La interfaz de usuario puede mostrar hasta diez como parte de la primera página y proporcionar paginación para las siguientes diez páginas. También se puede usar para mostrar un texto como **&quot;se encontraron más de 100 resultados&quot;**. Mientras el usuario va a las páginas siguientes, las llamadas realizadas al Generador de consultas aumentarían el límite de `guessTotal` y también del `offset` y `limit` parámetros.

`guessTotal` también debe utilizarse en casos en los que la interfaz de usuario necesite utilizar el desplazamiento infinito, para evitar que el Query Builder determine el recuento exacto de visitas.

### Buscar archivos jar y ordenarlos, más recientes primero {#find-jar-files-and-order-them-newest-first}

`http://<host>:<port>/bin/querybuilder.json?type=nt:file&nodename=*.jar&orderby=@jcr:content/jcr:lastModified&orderby.sort=desc`

```xml
type=nt:file
nodename=*.jar
orderby=@jcr:content/jcr:lastModified
orderby.sort=desc
```

### Buscar todas las páginas y ordenarlas por última vez modificadas {#find-all-pages-and-order-them-by-last-modified}

`http://<host>:<port>/bin/querybuilder.json?type=cq:Page&orderby=@jcr:content/cq:lastModified`

```xml
type=cq:Page
orderby=@jcr:content/cq:lastModified
```

### Buscar todas las páginas y ordenarlas por última modificación, descendente {#find-all-pages-and-order-them-by-last-modified-but-descending}

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

Utilice la variable `tagid` predicar como en el ejemplo si conoce el ID de etiqueta explícito.

Utilice la variable `tag` predicado para la ruta de título de la etiqueta (sin espacios).

Porque, en el ejemplo anterior, está buscando páginas (`cq:Page` nodos), debe utilizar la ruta relativa de ese nodo para el `tagid.property` predicado, que es `jcr:content/cq:tags`. De forma predeterminada, la variable `tagid.property` simplemente `cq:tags`.

### Buscar varias rutas (mediante grupos) {#search-under-multiple-paths-using-groups}

`http://<host>:<port>/bin/querybuilder.json?fulltext=Experience&group.1_path=/content/wknd/us/en/magazine&group.2_path=/content/wknd/us/en/adventures&group.p.or=true`

```xml
fulltext=Experience
group.p.or=true
group.1_path=/content/wknd/us/en/magazine
group.2_path=/content/wknd/us/en/adventures
```

Esta consulta utiliza un *grupo* (con nombre `group`), que actúa para delimitar las subexpresiones dentro de una consulta, como lo hacen los paréntesis en las notaciones más estándar. Por ejemplo, la consulta anterior se puede expresar con un estilo más familiar, como:

`"Experience" and ("/content/wknd/us/en/magazine" or "/content/wknd/us/en/adventures")`

Dentro del grupo en el ejemplo, la variable `path` predicado se utiliza varias veces. Para diferenciar y ordenar las dos instancias del predicado (se requiere orden para algunos predicados), se debe prefijar los predicados con `N_` donde `N` es el índice de ordenación. En el ejemplo anterior, los predicados resultantes son `1_path` y `2_path`.

La variable `p` en `p.or` es un delimitador especial que indica lo siguiente (en este caso, un `or`) es un *parameter* del grupo, a diferencia de un subpredicado del grupo, como `1_path`.

Si no `p.or` se da entonces todos los predicados son ANDed juntos, es decir, cada resultado debe satisfacer todos los predicados.

>[!NOTE]
>
>No se puede utilizar el mismo prefijo numérico en una sola consulta, ni siquiera para predicados diferentes.

### Buscar propiedades {#search-for-properties}

Aquí está buscando todas las páginas de una plantilla determinada, utilizando la variable `cq:template` propiedad:

`http://<host>:<port>/bin/querybuilder.json?property=cq%3atemplate&property.value=%2fconf%2fwknd%2fsettings%2fwcm%2ftemplates%2fadventure-page-template&type=cq%3aPageContent`

```xml
type=cq:PageContent
property=cq:template
property.value=/conf/wknd/settings/wcm/templates/adventure-page-template
```

Esto tiene el inconveniente de que la variable `jcr:content` se devuelven los nodos de las páginas, no las páginas en sí. Para resolver esto, puede buscar por ruta relativa:

`http://<host>:<port>/bin/querybuilder.json?property=jcr%3acontent%2fcq%3atemplate&property.value=%2fconf%2fwknd%2fsettings%2fwcm%2ftemplates%2fadventure-page-template&type=cq%3aPage`

```xml
type=cq:Page
property=jcr:content/cq:template
property.value=/conf/wknd/settings/wcm/templates/adventure-page-template
```

### Buscar varias propiedades {#search-for-multiple-properties}

Cuando utilice el predicado de propiedad varias veces, debe añadir de nuevo los prefijos numéricos:

`http://<host>:<port>/bin/querybuilder.json?1_property=jcr%3acontent%2fcq%3atemplate&1_property.value=%2fconf%2fwknd%2fsettings%2fwcm%2ftemplates%2fadventure-page-template&2_property=jcr%3acontent%2fjcr%3atitle&2_property.value=Cycling%20Tuscany&type=cq%3aPage`

```xml
type=cq:Page
1_property=jcr:content/cq:template
1_property.value=/conf/wknd/settings/wcm/templates/adventure-page-template
2_property=jcr:content/jcr:title
2_property.value=Cycling Tuscany
```

### Buscar valores de varias propiedades {#search-for-multiple-property-values}

Para evitar grupos grandes cuando desee buscar valores múltiples de una propiedad (`"A" or "B" or "C"`), puede proporcionar varios valores a la variable `property` predicado:

`http://<host>:<port>/bin/querybuilder.json?property=jcr%3atitle&property.1_value=Cycling%20Tuscany&property.2_value=Ski%20Touring&property.3_value=Whistler%20Mountain%20Biking`

```xml
property=jcr:title
property.1_value=Cycling Tuscany
property.2_value=Ski Touring
property.3_value=Whistler Mountain Biking
```

Para las propiedades de varios valores, también puede requerir que coincidan varios valores (`"A" and "B" and "C"`):

`http://<host>:<port>/bin/querybuilder.json?property=jcr%3atitle&property.and=true&property.1_value=Cycling%20Tuscany&property.2_value=Ski%20Touring&property.3_value=Whistler%20Mountain%20Biking`

```xml
property=jcr:title
property.and=true
property.1_value=Cycling Tuscany
property.2_value=Ski Touring
property.3_value=Whistler Mountain Biking
```

## Refinar lo que se devuelve {#refining-what-is-returned}

De forma predeterminada, el servlet JSON de QueryBuilder devolverá un conjunto predeterminado de propiedades para cada nodo en el resultado de la búsqueda (por ejemplo, ruta, nombre, título, etc.). Para obtener el control sobre qué propiedades se devuelven, puede realizar una de las siguientes acciones:

Especifique

```xml
p.hits=full
```

en cuyo caso se incluirán todas las propiedades para cada nodo:

`http://<host>:<port>/bin/querybuilder.json?p.hits=full&property=jcr%3atitle&property.value=Cycling%20Tuscany`

```xml
property=jcr:title
property.value=Cycling Tuscany
p.hits=full
```

Uso de

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

Otra cosa que puede hacer es incluir nodos secundarios en la respuesta de Query Builder. Para ello, debe especificar

```xml
p.nodedepth=n
```

donde `n` es el número de niveles que desea que devuelva la consulta. Tenga en cuenta que para que se devuelva un nodo secundario, debe especificarlo el selector de propiedades

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

Para obtener más predicados, consulte la [Página de referencia del predicado del generador de consultas](query-builder-predicates.md).

También puede marcar la [Javadoc para la variable `PredicateEvaluator` clases](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/search/eval/PredicateEvaluator.html). El Javadoc para estas clases contiene la lista de propiedades que puede utilizar.

El prefijo del nombre de la clase (por ejemplo, `similar` en [`SimilarityPredicateEvaluator`](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/search/eval/SimilarityPredicateEvaluator.html)) es la variable *principal, propiedad* de la clase. Esta propiedad también es el nombre del predicado que se va a usar en la consulta (en minúsculas).

Para estas propiedades principales, puede abreviar la consulta y utilizar `similar=/content/en` en lugar de la variante completa `similar.similar=/content/en`. El formulario completo debe utilizarse para todas las propiedades no principales de una clase.

## Ejemplo de uso de la API de Query Builder {#example-query-builder-api-usage}

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

La misma consulta ejecutada a través de HTTP mediante el servlet Query Builder (JSON):

`http://<host>:<port>/bin/querybuilder.json?path=/content&type=cq:Page&group.p.or=true&group.1_fulltext=WKND&group.1_fulltext.relPath=jcr:content&group.2_fulltext=WKND&group.2_fulltext.relPath=jcr:content/@cq:tags&p.offset=0&p.limit=20`

## Almacenamiento y carga de consultas {#storing-and-loading-queries}

Las consultas se pueden almacenar en el repositorio para que pueda utilizarlas más adelante. La variable `QueryBuilder` proporciona la variable `storeQuery` con la siguiente firma:

```java
void storeQuery(Query query, String path, boolean createFile, Session session) throws RepositoryException, IOException;
```

Al usar la variable [`QueryBuilder#storeQuery`](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/search/QueryBuilder.html#storeQuery-com.day.cq.search.Query-java.lang.String-boolean-javax.jcr.Session-) el método `Query` se almacena en el repositorio como un archivo o como una propiedad de acuerdo con la variable `createFile` valor de argumento. El siguiente ejemplo muestra cómo guardar un `Query` a la ruta `/mypath/getfiles` como archivo:

```java
builder.storeQuery(query, "/mypath/getfiles", true, session);
```

Las consultas almacenadas anteriormente se pueden cargar desde el repositorio utilizando la variable [`QueryBuilder#loadQuery`](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/search/QueryBuilder.html#loadQuery-java.lang.String-javax.jcr.Session-) método:

```java
Query loadQuery(String path, Session session) throws RepositoryException, IOException
```

Por ejemplo, una `Query` almacenado en la ruta `/mypath/getfiles` se puede cargar mediante el siguiente fragmento de código:

```java
Query loadedQuery = builder.loadQuery("/mypath/getfiles", session);
```

## Pruebas y depuración {#testing-and-debugging}

Para reproducir y depurar consultas de Query Builder, puede utilizar la consola de Debugger de Query Builder en

`http://<host>:<port>/libs/cq/search/content/querydebug.html`

o alternativamente, el servlet JSON de Query Builder en

`http://<host>:<port>/bin/querybuilder.json?path=/tmp`

`path=/tmp` es solo un ejemplo.

### Depuración general de Recommendations {#general-debugging-recommendations}

### Obtener XPath explicable mediante Registro {#obtain-explain-able-xpath-via-logging}

Explicar **all** consulta durante el ciclo de desarrollo con el conjunto de índices de target.

1. Habilite los registros DEBUG para QueryBuilder para obtener una consulta XPath subyacente y explicable
   * Vaya a `https://<host>:<port>/system/console/slinglog`. Crear un nuevo registrador para `com.day.cq.search.impl.builder.QueryImpl` at **DEBUG**.
1. Una vez DEBUG esté habilitado para la clase anterior, los registros mostrarán el XPath generado por Query Builder.
1. Copie la consulta XPath de la entrada de registro para la consulta asociada del Generador de consultas, por ejemplo:
   * `com.day.cq.search.impl.builder.QueryImpl XPath query: /jcr:root/content//element(*, cq:Page)[(jcr:contains(jcr:content, "WKND") or jcr:contains(jcr:content/@cq:tags, "WKND"))]`
1. Pegue la consulta XPath en Explicar consulta como XPath para obtener el plan de consulta.

### Obtener XPath explicable mediante Query Builder Debugger {#obtain-explain-able-xpath-via-the-query-builder-debugger}

Utilice el depurador AEM Query Builder para generar una consulta XPath explicable.

![Depurador del generador de consultas](assets/query-builder-debugger.png)

1. Proporcione la consulta de Query Builder en el depurador de Query Builder
1. Ejecutar la búsqueda
1. Obtener el XPath generado
1. Pegue la consulta XPath en Explicar consulta como XPath para obtener el plan de consulta

>[!NOTE]
>
>Las consultas que no sean de Query Builder (XPath, JCR-SQL2) se pueden proporcionar directamente a Explicar consulta.

## Depuración de consultas con registro {#debugging-queries-with-logging}

>[!NOTE]
>
>La configuración de los registradores se describe en el documento [Registro](/help/implementing/developing/introduction/logging.md).

El resultado del registro (nivel INFO) de la implementación del generador de consultas al ejecutar la consulta descrita en la sección anterior [Pruebas y depuración:](#testing-and-debugging)

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

Si tiene una consulta utilizando evaluadores predicados que filtran o que usan un orden personalizado por comparador, esto también se anotará en la consulta:

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

## Vínculos de Javadoc {#javadoc-links}

| **Javadoc** | **Descripción** |
|---|---|
| [com.day.cq.search](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/search/package-summary.html) | Query Builder básico y API de consulta |
| [com.day.cq.search.result](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/search/result/package-summary.html) | API de resultado |
| [com.day.cq.search.facets](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/search/facets/package-summary.html) | Facetas |
| [com.day.cq.search.facets.buckets](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/search/facets/buckets/package-summary.html) | Contenedores (contenidos dentro de facetas) |
| [com.day.cq.search.eval](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/search/eval/package-summary.html) | Predicar evaluadores |
| [com.day.cq.search.facets.extractores](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/search/facets/extractors/package-summary.html) | Extractores de facetas (para evaluadores) |
| [com.day.cq.search.writer](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/search/writer/package-summary.html) | Escritor de visitas de resultados JSON para el servlet Query Builder (`/bin/querybuilder.json`) |
