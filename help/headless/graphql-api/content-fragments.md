---
title: API de GraphQL de AEM para su uso con fragmentos de contenido
description: Aprenda a utilizar los fragmentos de contenido en Adobe Experience Manager (AEM) as a Cloud Service con la API de GraphQL de AEM para la entrega de contenido sin encabezado.
feature: Content Fragments,GraphQL API
exl-id: bdd60e7b-4ab9-4aa5-add9-01c1847f37f6
source-git-commit: f773671e3c62e2dff6f843d42a5b36211e2d1fc3
workflow-type: tm+mt
source-wordcount: '2708'
ht-degree: 98%

---


# API de GraphQL de AEM para su uso con fragmentos de contenido {#graphql-api-for-use-with-content-fragments}

Aprenda a utilizar los fragmentos de contenido en Adobe Experience Manager (AEM) as a Cloud Service con la API de GraphQL de AEM para la entrega de contenido sin encabezado.

La API de GraphQL de AEM as a Cloud Service que se utiliza con fragmentos de contenido se basa principalmente en la API estándar de código abierto de GraphQL.

El uso de la API de GraphQL en AEM permite la entrega eficiente de fragmentos de contenido a clientes JavaScript en implementaciones de CMS sin encabezado:

* Evita solicitudes de API iterativas como con REST,
* Garantiza que la entrega se limite a los requisitos específicos,
* Permite la entrega masiva de exactamente lo que se necesita para procesar como respuesta a una sola consulta de API.

>[!NOTE]
>
>GraphQL se utiliza actualmente en dos escenarios (independientes) en Adobe Experience Manager (AEM) as a Cloud Service:
>
>* [AEM Commerce consume datos de una plataforma de Commerce a través de GraphQL](/help/commerce-cloud/integrating/magento.md).
>* Los fragmentos de contenido de AEM trabajan junto con la API de GraphQL de AEM (una implementación personalizada, basada en GraphQL estándar) para ofrecer contenido estructurado para su uso en aplicaciones.


## La API de GraphQL {#graphql-api}

GraphQL es:

* “*...un idioma de consulta para API y un tiempo de ejecución para cumplir esas consultas con los datos existentes. GraphQL proporciona una descripción completa y comprensible de los datos de su API, ofrece a los clientes la posibilidad de preguntar exactamente lo que necesitan y nada más, facilita la evolución de las API con el paso del tiempo y habilita potentes herramientas para desarrolladores”.*

   Consulte [GraphQL.org](https://graphql.org)

* “*...una especificación abierta para una capa de API flexible. Coloque GraphQL sobre los back-ends existentes para crear productos más rápido que nunca...*”.

   Consulte [Exploración de GraphQL](https://www.graphql.com).

* *“...una especificación y lenguaje de consulta de datos desarrollado internamente por Facebook en 2012, antes de pasar a ser de código abierto público en 2015. Proporciona una alternativa a las arquitecturas basadas en REST con el propósito de aumentar la productividad del desarrollador y minimizar las cantidades de datos transferidos. Cientos de organizaciones de todos los tamaños utilizan GraphQL en producción...”*

   Consulte [Fundamentos de GraphQL](https://foundation.graphql.org/).

<!--
"*Explore GraphQL is maintained by the Apollo team. Our goal is to give developers and technical leaders around the world all of the tools they need to understand and adopt GraphQL.*". 
-->

Para obtener más información acerca de la API de GraphQL, consulte las siguientes secciones (entre muchos otros recursos):

* En [graphql.org](https://graphql.org):

   * [Introducción a GraphQL](https://graphql.org/learn)

   * [Especificación de GraphQL](https://spec.graphql.org/)

* En [graphql.com](https://graphql.com):

   * [Guías](https://www.graphql.com/guides/)

   * [Tutoriales](https://www.graphql.com/tutorials/)

   * [Casos prácticos](https://www.graphql.com/case-studies/)

La implementación de GraphQL para AEM se basa en la biblioteca Java estándar de GraphQL. Consulte:

* [graphQL.org: Java](https://graphql.org/code/#java)

* [GraphQL Java en GitHub](https://github.com/graphql-java)

### Terminología de GraphQL {#graphql-terminology}

GraphQL utiliza lo siguiente:

* **[Consultas](https://graphql.org/learn/queries/)**

* **[Esquemas y tipos](https://graphql.org/learn/schema/)**:

   * AEM genera los esquemas basándose en los modelos de fragmentos de contenido.
   * Con sus esquemas, GraphQL presenta los tipos y operaciones permitidos para la implementación de GraphQL para AEM.

* **[Campos](https://graphql.org/learn/queries/#fields)**

* **[Punto de conexión de GraphQL](graphql-endpoint.md)**
   * La ruta en AEM que responde a las consultas de GraphQL y proporciona acceso a los esquemas de GraphQL.

   * Consulte [Activación del punto de conexión de GraphQL](graphql-endpoint.md) para obtener más información.

Consulte la [Introducción a GraphQL (GraphQL.org)](https://graphql.org/learn/) para obtener información detallada, incluidas las [Prácticas recomendadas](https://graphql.org/learn/best-practices/).

### Tipos de consulta de GraphQL {#graphql-query-types}

Con GraphQL puede realizar consultas para devolver lo siguiente:

* Una **entrada única**

* Una **[lista de entradas](https://graphql.org/learn/schema/#lists-and-non-null)**

También puede realizar:

* [Consultas persistentes, que se almacenan en caché](/help/headless/graphql-api/persisted-queries.md)

### Prácticas recomendadas para consultas de GraphQL (Dispatcher) {#graphql-query-best-practices}

Las [Consultas persistentes](/help/headless/graphql-api/persisted-queries.md) son el método recomendado ya que:

* Se almacenan en caché.
* Se administran centralmente mediante AEM as a Cloud Service.

No se recomiendan las consultas directas o POST, ya que no se almacenan en caché, por lo que en una instancia predeterminada, Dispatcher está configurado para bloquear dichas consultas.

>[!NOTE]
>
>Para permitir consultas directas o POST en Dispatcher, puede pedir al administrador del sistema que realice lo siguiente:
>
>* Cree una variable de entorno de Cloud Manager llamada `ENABLE_GRAPHQL_ENDPOINT`
>* con el valor `true`.


>[!NOTE]
>
>La capacidad de realizar consultas directas puede quedar obsoleta en algún momento futuro.

### IDE de GraphiQL {#graphiql-ide}

Puede probar y depurar consultas de GraphQL usando el [IDE de GraphiQL](/help/headless/graphql-api/graphiql-ide.md).

## Casos de uso para entornos de creación y publicación {#use-cases-author-publish-environments}

Los casos de uso pueden depender del tipo de entorno de AEM as a Cloud Service:

* Entorno de publicación; se usa para:
   * Datos de consulta para la aplicación JS (caso de uso estándar)

* Entorno de creación; se usa para:
   * Datos de consulta para “fines de administración de contenido”:
      * GraphQL en AEM as a Cloud Service es actualmente una API de solo lectura.
      * La API de REST se puede utilizar para operaciones CR(u)D.

## Permisos {#permission}

Los permisos son los necesarios para acceder a Assets.

## Generación de esquemas {#schema-generation}

GraphQL es una API muy tipificada, lo que significa que los datos deben estar claramente estructurados y organizados por tipo.

La especificación de GraphQL proporciona una serie de directrices sobre cómo crear una API robusta para buscar datos en una instancia determinada. Para ello, un cliente debe recuperar el [Esquema](#schema-generation), que contiene todos los tipos necesarios para una consulta.

Para los fragmentos de contenido, los esquemas (estructura y tipos) de GraphQL se basan en [Modelos de fragmentos de contenido](/help/sites-cloud/administering/content-fragments/content-fragments-models.md) **habilitados** y sus tipos de datos.

>[!CAUTION]
>
>Todos los esquemas de GraphQL (derivados de los modelos de fragmentos de contenido que se han **habilitado**) se pueden leer a través del punto de conexión de GraphQL.
>
>Esto significa que debe asegurarse de que no hay datos confidenciales disponibles, ya que podrían filtrarse de esta manera; por ejemplo, esto incluye información que podría estar presente como nombres de campo en la definición del modelo.

Por ejemplo, si un usuario crea un modelo de fragmentos de contenido denominado `Article`, luego AEM genera el objeto `article`, que es de un tipo `ArticleModel`. Los campos dentro de este tipo corresponden a los campos y tipos de datos definidos en el modelo.

1. Un modelo de fragmento de contenido:

   ![Modelo de fragmento de contenido para usar con GraphQL](assets/cfm-graphqlapi-01.png "Modelo de fragmento de contenido para usar con GraphQL")

1. El esquema correspondiente de GraphQL (salida de la documentación automática de GraphiQL):
   ![Esquema de GraphQL basado en el modelo de fragmento de contenido](assets/cfm-graphqlapi-02.png "Esquema de GraphQL basado en el modelo de fragmento de contenido")

   Esto muestra que el tipo generado `ArticleModel` contiene varios [campos](#fields).

   * Tres de ellos han sido controlados por el usuario: `author`, `main` y `referencearticle`.

   * Los demás campos los añadió automáticamente AEM y representan métodos útiles para proporcionar información acerca de un determinado fragmento de contenido; en este ejemplo, `_path`, `_metadata`, `_variations`. Estos [campos de ayuda](#helper-fields) se marcan con un `_` que los precede para distinguir entre lo que ha definido el usuario y lo que se ha generado automáticamente.

1. Después de que un usuario cree un fragmento de contenido basado en el modelo de artículo, se puede buscar a través de GraphQL. Para ver ejemplos, consulte las [Consultas de muestra](/help/headless/graphql-api/sample-queries.md#graphql-sample-queries) (basadas en una [estructura de fragmentos de contenido de muestra para usar con GraphQL](/help/headless/graphql-api/sample-queries.md#content-fragment-structure-graphql)).

En GraphQL para AEM, el esquema es flexible. Esto significa que se genera automáticamente cada vez que se crea, actualiza o elimina un modelo de fragmento de contenido. Las cachés del esquema de datos también se refrescan al actualizar el modelo de fragmento de contenido.

El servicio Sites de GraphQL escucha (en segundo plano) cualquier modificación realizada en un modelo de fragmento de contenido. Cuando se detectan actualizaciones, solo se regenera esa parte del esquema. Esta optimización ahorra tiempo y proporciona estabilidad.

Por ejemplo, si:

1. Instala un paquete que contenga `Content-Fragment-Model-1` y `Content-Fragment-Model-2`:

   1. Se generarán tipos de GraphQL para `Model-1` y `Model-2`.

1. A continuación, modifique `Content-Fragment-Model-2`:

   1. Solo el tipo de GraphQL `Model-2` se actualizará.

   1. Mientras que `Model-1` seguirá siendo el mismo.

>[!NOTE]
>
>Esto es importante tenerlo en cuenta en caso de que desee realizar actualizaciones masivas en los modelos de fragmento de contenido a través de la API de REST o de otro modo.

El esquema se sirve a través del mismo punto de conexión que las consultas de GraphQL, y el cliente gestiona el hecho de que se llama al esquema con la extensión `GQLschema`. Por ejemplo, realizar una solicitud `GET` simple en `/content/cq:graphql/global/endpoint.GQLschema` resultará en la salida del esquema con el tipo contenido: `text/x-graphql-schema;charset=iso-8859-1`.

### Generación de esquemas: modelos no publicados {#schema-generation-unpublished-models}

Cuando los fragmentos de contenido están anidados, puede ocurrir que se publique un modelo de fragmento de contenido principal, pero no un modelo al que se hace referencia.

>[!NOTE]
>
>La IU de AEM evita que esto ocurra, pero si la publicación se realiza mediante programación o con paquetes de contenido, puede ocurrir.

Cuando esto sucede, AEM genera un esquema *incompleto* del modelo de fragmento del contenido principal. Esto significa que la referencia de fragmento, que depende del modelo no publicado, se elimina del esquema.

## Campos {#fields}

Dentro del esquema hay campos individuales, de dos categorías básicas:

* Campos que genera usted.

   Una selección de [Tipos de campo](#field-types) se utiliza para crear campos en función de cómo configure el modelo de fragmento de contenido. Los nombres de campo se toman del campo **Nombre de propiedad** del **Tipo de datos**.

   * También se debe tener en cuenta la propiedad **Procesar como**, ya que los usuarios pueden configurar ciertos tipos de datos; por ejemplo, como texto de una sola línea o como campo múltiple.

* GraphQL para AEM también genera una serie de [campos de ayuda](#helper-fields).

   Se utilizan para identificar un fragmento de contenido o para obtener más información acerca de uno.

### Tipos de campos {#field-types}

GraphQL para AEM admite una lista de tipos. Se representan todos los tipos de datos del modelo de fragmento de contenido compatibles y los tipos de GraphQL correspondientes:

| Modelo de fragmento de contenido: tipo de datos | Tipo de GraphQL | Descripción |
|--- |--- |--- |
| Texto de línea única | Cadena, [Cadena] |  Se utiliza para cadenas simples como nombres de autor, nombres de ubicación, etc. |
| Texto multilínea | Cadena |  Se utiliza para generar texto como el cuerpo de un artículo |
| Número |  Flotante, [Flotante] | Se utiliza para mostrar números de coma flotante y números regulares |
| Booleano |  Booleano |  Se utiliza para mostrar casillas de verificación → instrucciones simples verdaderas/falsas |
| Fecha y hora | Calendario |  Se utiliza para mostrar la fecha y la hora en formato ISO 8086. Según el tipo seleccionado, hay tres variantes disponibles para usar en AEM GraphQL: `onlyDate`, `onlyTime`, `dateTime` |
| Lista desglosada |  Cadena |  Se utiliza para mostrar una opción de una lista de opciones definidas en la creación del modelo |
|  Etiquetas |  [Cadena] |  Se utiliza para mostrar una lista de cadenas que representan las etiquetas utilizadas en AEM |
| Referencia de contenido |  Cadena |  Se utiliza para mostrar la ruta hacia otro recurso en AEM |
| Referencia al fragmento |  *Un tipo de modelo* |  Se utiliza para hacer referencia a otro fragmento de contenido de un tipo de modelo determinado, definido cuando se creó el modelo |

### Campos de ayuda {#helper-fields}

Además de los tipos de datos de los campos generados por el usuario, GraphQL para AEM también genera una serie de campos de *ayuda* para ayudar a identificar un fragmento de contenido o para proporcionar información adicional acerca de un fragmento de contenido.

#### Ruta {#path}

El campo de ruta se utiliza como identificador en GraphQL. Representa la ruta del recurso de fragmento de contenido dentro del repositorio de AEM. Lo hemos elegido como identificador de un fragmento de contenido, por los motivos siguientes:

* es único dentro de AEM,
* se puede recuperar fácilmente.

El siguiente código muestra las rutas de todos los fragmentos de contenido creados en función del modelo de fragmento de contenido `Person`.

```xml
{
  personList {
    items {
      _path
    }
  }
}
```

Para recuperar un solo fragmento de contenido de un tipo específico, también debe determinar primero su ruta. por ejemplo:

```xml
{
  personByPath(_path: "/content/dam/path/to/fragment/john-doe") {
    item {
      _path
      firstName
      name
    }
  }
}
```

Consulte [Consulta de muestra: un solo fragmento de ciudad específico](/help/headless/graphql-api/sample-queries.md#sample-single-specific-city-fragment).

#### Metadatos {#metadata}

A través de GraphQL, AEM también expone los metadatos de un fragmento de contenido. Los metadatos son la información que describe un fragmento de contenido, como su título, la ruta de la miniatura, la descripción de un fragmento de contenido o la fecha en que se creó, entre otros.

Dado que los metadatos se generan mediante el Editor de esquemas y, como tales, no tienen una estructura específica, el tipo de GraphQL `TypedMetaData` se ha implementado para exponer los metadatos de un fragmento de contenido. `TypedMetaData` expone la información agrupada por los siguientes tipos escalares:

| Campo |
|--- |
| `stringMetadata:[StringMetadata]!` |
| `stringArrayMetadata:[StringArrayMetadata]!` |
| `intMetadata:[IntMetadata]!` |
| `intArrayMetadata:[IntArrayMetadata]!` |
| `floatMetadata:[FloatMetadata]!` |
| `floatArrayMetadata:[FloatArrayMetadata]!` |
| `booleanMetadata:[BooleanMetadata]!` |
| `booleanArrayMetadata:[booleanArrayMetadata]!`  |
| `calendarMetadata:[CalendarMetadata]!` |
| `calendarArrayMetadata:[CalendarArrayMetadata]!` |

Cada tipo escalar representa un único par nombre-valor o una matriz de pares nombre-valor, donde el valor de ese par es del tipo en el que se agrupó.

Por ejemplo, si desea recuperar el título de un fragmento de contenido, sabemos que esta propiedad es de cadena, por lo que consultaremos todos los metadatos de cadena:

Para consultar metadatos:

```xml
{
  personByPath(_path: "/content/dam/path/to/fragment/john-doe") {
    item {
      _path
      _metadata {
        stringMetadata {
          name
          value
        }
      }
    }
  }
}
```

Puede ver todos los tipos de metadatos de GraphQL si ve el esquema de GraphQL generado. Todos los tipos de modelo tienen el mismo `TypedMetaData`.

>[!NOTE]
>
>**Diferencia entre metadatos normales y de matriz**
>Tenga en cuenta que `StringMetadata` y `StringArrayMetadata` hacen referencia a lo que se almacena en el repositorio, no a cómo se recuperan.
>
>Por ejemplo, llamando al campo `stringMetadata`, recibirá una matriz de todos los metadatos almacenados en el repositorio como `String`, y si llama a `stringArrayMetadata` recibirá una matriz de todos los metadatos almacenados en el repositorio como `String[]`.

Consulte [Consulta de muestra para metadatos: enumera los metadatos de los premios titulados GB](/help/headless/graphql-api/sample-queries.md#sample-metadata-awards-gb).

#### Variaciones {#variations}

El campo `_variations` se ha implementado para simplificar la consulta de las variaciones que tiene un fragmento de contenido. Por ejemplo:

```xml
{
  personByPath(_path: "/content/dam/path/to/fragment/john-doe") {
    item {
      _variations
    }
  }
}
```

Consulte [Consulta de muestra: todas las ciudades con una variación con nombre](/help/headless/graphql-api/sample-queries.md#sample-cities-named-variation).

>[!NOTE]
>
>Si la variación dada no existe para un fragmento de contenido, la variación maestra se devolverá como predeterminada (reserva).

<!--
## Security Considerations {#security-considerations}
-->

## Variables de GraphQL {#graphql-variables}

GraphQL permite colocar variables en la consulta. Para obtener más información, consulte la [Documentación de GraphQL para variables](https://graphql.org/learn/queries/#variables).

Por ejemplo, para obtener todos los fragmentos de contenido del tipo `Article` que tienen una variación específica, puede especificar la variable `variation` en GraphiQL.

![Variables de GraphQL](assets/cfm-graphqlapi-03.png "Variables de GraphQL")

```xml
### query
query GetArticlesByVariation($variation: String!) {
    articleList(variation: $variation) {
        items {
            _path
            author
        }
    }
}
 
### in query variables
{
    "variation": "Introduction"
}
```

## Directivas de GraphQL {#graphql-directives}

En GraphQL existe la posibilidad de cambiar la consulta en función de variables, denominadas Directivas de GraphQL.

Por ejemplo, puede incluir el campo `adventurePrice` en una consulta para todos los `AdventureModels`, en función de una variable `includePrice`.

![Directivas de GraphQL](assets/cfm-graphqlapi-04.png "Directivas de GraphQL")

```xml
### query
query GetAdventureByType($includePrice: Boolean!) {
  adventureList {
    items {
      adventureTitle
      adventurePrice @include(if: $includePrice)
    }
  }
}
 
### in query variables
{
    "includePrice": true
}
```

## Filtrado {#filtering}

También puede utilizar el filtrado en las consultas de GraphQL para devolver datos específicos.

El filtrado utiliza una sintaxis basada en operadores lógicos y expresiones.

Por ejemplo, la siguiente consulta (básica) filtra todas las personas que tienen un apellido `Jobs` o `Smith`:

```xml
query {
  personList(filter: {
    name: {
      _logOp: OR
      _expressions: [
        {
          value: "Jobs"
        },
        {
          value: "Smith"
        }
      ]
    }
  }) {
    items {
      name
      firstName
    }
  }
}
```

Para ver más ejemplos, consulte lo siguiente:

* detalles de [GraphQL para extensiones de AEM](#graphql-extensions)

* [Ejemplos de consultas que utilizan este contenido y estructura de muestra](/help/headless/graphql-api/sample-queries.md#graphql-sample-queries-sample-content-fragment-structure)

   * Y el [Contenido y estructura de muestra](/help/headless/graphql-api/sample-queries.md#content-fragment-structure-graphql) preparados para su uso en consultas de muestra

* [Consultas de muestra basadas en el proyecto WKND](/help/headless/graphql-api/sample-queries.md#sample-queries-using-wknd-project)

<!-- CQDOC-19418 -->

<!--
## Sorting {#sorting}

This feature allows you to sort the query results according to a specified field.

For example:

```graphql
query {
  articleList(sort:"author, _uuid DESC") {
    items {
      author
      _path
    }
  }
}
```

## Paging {#paging}

This feature allows you to perform paging on query types that returns a list. Two methods are provided:

* `offset` and `limit` in a `List` query
* `first` and `after` in a `Paginated` query

### List query - offset and limit {#list-offset-limit}

In a `...List`query you can use `offset` and `limit` to return a specific subset of results:

* `offset`: Specifies the first data set to return
* `limit`: Specifies the maximum number of data sets to be returned

For example, to output the page of results containing up to five articles, starting from the fifth article from the *complete* results list:

```graphql
query {
   articleList(offset: 5, limit:5) {
    items {
      author
      _path
    }
  }
}
```

>[!NOTE]
>
>* Paging is impacted by the order to the jcr query result set. By default it uses `jcr:path` to make sure the order is always the same. If a different sort order is used, and if that sorting cannot be done at jcr query level, then there will be a negative performance impact as the paging cannot be done in memory.
>
>* The higher the offset, the more time it will take to skip the items from the complete jcr query result set. An alternative solution for large result sets is to use the Paginated query with `first` and `after` method.

### Paginated query - first and after {#paginated-first-after}

The `...Paginated` query type reuses most of the `...List` query type features (filtering, sorting), but instead of using `offset`/`limit` arguments, it uses the standard `first`/`after` arguments defined by [GraphQL](https://graphql.org/learn/pagination/#pagination-and-edges).

* `first`: The `n` first items to return. The default is `50`.
* `after`: The cursor-id as returned in the complete result set - if `cursor` is selected.

For example, output the page of results containing up to five adventures, starting from the given cursor item in the *complete* results list:

```graphql
query {
    adventurePaginated(first: 5, after: "ODg1MmMyMmEtZTAzMy00MTNjLThiMzMtZGQyMzY5ZTNjN2M1") {
        edges {
          cursor
          node {
            adventureTitle
          }
        }
        pageInfo {
          endCursor
          hasNextPage
        }
    }
}
```

>[!NOTE]
>
>* Paging defaults use `_uuid` for ordering to ensure the order of results is always the same. When `sort` is used, `_uuid` is added as a last order-by field.
>
>* Performance is expected to be degraded if sort/filter parameters cannot be executed at jcr query level, as the query first has to gather the results in memory then sort them, then finally apply paging. Therefore it is recommended to use filter/sort fields stored at root level.
-->

## GraphQL para AEM: resumen de extensiones {#graphql-extensions}

El funcionamiento básico de las consultas con GraphQL para AEM se adhiere a la especificación estándar de GraphQL. Para las consultas de GraphQL con AEM hay algunas extensiones:

<!-- CQDOC-19418 -->

<!--
* If you expect a list of results:
  * add `List` to the model name; for example,  `cityList`
  * See [Sample Query - All Information about All Cities](/help/headless/graphql-api/sample-queries.md#sample-all-information-all-cities)
  
  You can then:
  
  * [Sort the results](#sorting)

  * Return a page of results using either:

    * [A List query with offset and limit](#list-offset-limit)
    * [A Paginated query with first and after](#paginated-first-after)
  * See [Sample Query - All Information about All Cities](/help/headless/graphql-api/sample-queries.md#sample-all-information-all-cities)
-->

* Si necesita un solo resultado:
   * utilice el nombre del modelo; p. ej., ciudad

* Si espera una lista de resultados:
   * añada `List` al nombre del modelo; por ejemplo, `cityList`
   * Consulte [Consulta de muestra: toda la información acerca de todas las ciudades](/help/headless/graphql-api/sample-queries.md#sample-all-information-all-cities)

* Si desea utilizar un OR lógico:
   * use ` _logOp: OR`
   * Consulte [Consulta de muestra: todas las personas que tienen el apellido “Jobs” o “Smith”](/help/headless/graphql-api/sample-queries.md#sample-all-persons-jobs-smith)

* El AND lógico también existe, pero (a menudo) está implícito

* Puede consultar los nombres de campo que se correspondan con los campos del modelo de fragmento de contenido
   * Consulte [Consulta de muestra: detalles completos del CEO y los empleados de una compañía](/help/headless/graphql-api/sample-queries.md#sample-full-details-company-ceos-employees)

* Además de los campos del modelo, hay algunos campos generados por el sistema (precedidos de guiones bajos):

   * Para el contenido:

      * `_locale`: para revelar el idioma; basado en el Administrador de idiomas
         * Consulte [Consulta de muestra para varios fragmentos de contenido de una configuración regional determinada](/help/headless/graphql-api/sample-queries.md#sample-wknd-multiple-fragments-given-locale)
      * `_metadata`: para mostrar los metadatos del fragmento
         * Consulte [Consulta de muestra para metadatos: enumera los metadatos de los premios titulados GB](/help/headless/graphql-api/sample-queries.md#sample-metadata-awards-gb)
      * `_model`: permitir la consulta de un modelo de fragmento de contenido (ruta y título)
         * Consulte [Consulta de muestra para un modelo de fragmento de contenido de un modelo](/help/headless/graphql-api/sample-queries.md#sample-wknd-content-fragment-model-from-model)
      * `_path`: la ruta al fragmento de contenido dentro del repositorio
         * Consulte [Consulta de muestra: un solo fragmento de ciudad específico](/help/headless/graphql-api/sample-queries.md#sample-single-specific-city-fragment)
      * `_reference`: para revelar referencias, incluyendo referencias en línea en el Editor de texto enriquecido
         * Consulte [Consulta de muestra para varios fragmentos de contenido con referencias recuperadas previamente](/help/headless/graphql-api/sample-queries.md#sample-wknd-multiple-fragments-prefetched-references)
      * `_variation`: para mostrar variaciones específicas dentro del fragmento de contenido

         >[!NOTE]
         >
         >Si la variación dada no existe para un fragmento de contenido, la variación maestra se devolverá como predeterminada (reserva).

         * Consulte [Consulta de muestra: todas las ciudades con una variación con nombre](#sample-cities-named-variation)
   * Y operaciones:

      * `_operator`: aplicar operadores específicos; `EQUALS`, `EQUALS_NOT`, `GREATER_EQUAL`, `LOWER`, `CONTAINS`, `STARTS_WITH`
         * Consulte [Consulta de muestra: todas las personas que no tienen el apellido “Jobs”](/help/headless/graphql-api/sample-queries.md#sample-all-persons-not-jobs)
         * Consulte [Consulta de muestra: todas las aventuras en las que la `_path` comienza con un prefijo específico](/help/headless/graphql-api/sample-queries.md#sample-wknd-all-adventures-cycling-path-filter)
      * `_apply`: para aplicar condiciones específicas; por ejemplo, `AT_LEAST_ONCE`
         * Consulte [Consulta de muestra: filtre en una matriz con un elemento que deba producirse al menos una vez](/help/headless/graphql-api/sample-queries.md#sample-array-item-occur-at-least-once)
      * `_ignoreCase`: para ignorar el caso al consultar
         * Consulte [Consulta de muestra: todas las ciudades con SAN en el nombre, sin importar las mayúsculas](/help/headless/graphql-api/sample-queries.md#sample-all-cities-san-ignore-case)









* Se admiten los tipos de unión de GraphQL:

   * use `... on`
      * Consulte [Consulta de muestra para un fragmento de contenido de un modelo específico con una referencia de contenido](/help/headless/graphql-api/sample-queries.md#sample-wknd-fragment-specific-model-content-reference)

* Alternativa cuando se consultan fragmentos anidados:

   * Si una variación determinada no existe en un fragmento anidado, se devolvería la variación **Principal**.

## Consulta del punto de conexión de GraphQL desde un sitio web externo {#query-graphql-endpoint-from-external-website}

Para acceder al punto de conexión de GraphQL desde un sitio web externo, debe configurar lo siguiente:

* [Filtro CORS](/help/headless/deployment/cross-origin-resource-sharing.md)
* [Filtro de referente](/help/headless/deployment/referrer-filter.md)

## Autenticación {#authentication}

Consulte [Autenticación para consultas de GraphQL de AEM remotas en fragmentos de contenido](/help/headless/security/authentication.md).

<!-- to be addressed later -->

<!--
## Sorting {#sorting}
-->

<!-- to be addressed later -->

<!--
## Paging {#paging}
-->

## Preguntas frecuentes {#faqs}

Preguntas que han surgido:

1. **P**: “*¿En qué se diferencia la API de GraphQL para AEM de la API Generador de consultas?*”

   * **R**: “*La API de GraphQL de AEM ofrece control total sobre la salida JSON y es un estándar en la industria para consultar contenido.
En adelante, AEM tiene previsto invertir en la API de GraphQL de AEM”.*

## Tutorial: Introducción a AEM Headless y GraphQL {#tutorial}

¿Busca un tutorial práctico? Consulte el tutorial completo [Introducción a AEM Headless y GraphQL](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/overview.html?lang=es), que ilustra cómo crear y exponer contenido mediante las API de GraphQL de AEM y consumido por una aplicación externa, en un escenario de CMS sin encabezado.
