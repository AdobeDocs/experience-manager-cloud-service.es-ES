---
title: AEM API de GraphQL para su uso con fragmentos de contenido
description: Aprenda a utilizar los fragmentos de contenido en Adobe Experience Manager (AEM) as a Cloud Service con la API de AEM GraphQL para la entrega de contenido sin encabezado.
feature: Content Fragments,GraphQL API
exl-id: bdd60e7b-4ab9-4aa5-add9-01c1847f37f6
source-git-commit: c5d67e0ece40cdf7a9009436ec90305fe81425a2
workflow-type: tm+mt
source-wordcount: '2569'
ht-degree: 1%

---


# AEM API de GraphQL para su uso con fragmentos de contenido {#graphql-api-for-use-with-content-fragments}

Aprenda a utilizar los fragmentos de contenido en Adobe Experience Manager (AEM) as a Cloud Service con la API de AEM GraphQL para la entrega de contenido sin encabezado.

AEM API as a Cloud Service de GraphQL que se utiliza con fragmentos de contenido se basa principalmente en la API estándar de código abierto de GraphQL.

El uso de la API de GraphQL en AEM permite la entrega eficiente de fragmentos de contenido a clientes JavaScript en implementaciones CMS sin encabezado:

* Evitar solicitudes de API iterativas como con REST,
* Garantizar que la entrega se limite a los requisitos específicos,
* Permitir el envío masivo de exactamente lo que se necesita para procesar como respuesta a una sola consulta de API.

>[!NOTE]
>
>GraphQL se utiliza actualmente en dos escenarios (independientes) en Adobe Experience Manager (AEM) as a Cloud Service:
>
>* [AEM Commerce consume datos de una plataforma de comercio a través de GraphQL](/help/commerce-cloud/integrating/magento.md).
>* AEM fragmentos de contenido trabajan junto con la API de GraphQL de AEM (una implementación personalizada, basada en GraphQL estándar) para ofrecer contenido estructurado para su uso en aplicaciones.


## La API de GraphQL {#graphql-api}

GraphQL es:

* &quot;*...un idioma de consulta para API y un tiempo de ejecución para cumplir esas consultas con los datos existentes. GraphQL proporciona una descripción completa y comprensible de los datos de su API, ofrece a los clientes la posibilidad de preguntar exactamente lo que necesitan y nada más, facilita la evolución de las API con el paso del tiempo y permite potentes herramientas para desarrolladores.*&quot;.

   Consulte [GraphQL.org](https://graphql.org)

* &quot;*...una especificación abierta para una capa de API flexible. Coloque GraphQL sobre los backends existentes para crear productos más rápido que nunca....*&quot;.

   Consulte [Explorar GraphQL](https://www.graphql.com).

* *&quot;...especificación y lenguaje de consulta de datos desarrollados internamente por Facebook en 2012 antes de ser de código abierto público en 2015. Proporciona una alternativa a las arquitecturas basadas en REST con el propósito de aumentar la productividad del desarrollador y minimizar las cantidades de datos transferidos. GraphQL es utilizado en la producción por cientos de organizaciones de todos los tamaños...&quot;*

   Consulte [GraphQL Foundation](https://foundation.graphql.org/).

<!--
"*Explore GraphQL is maintained by the Apollo team. Our goal is to give developers and technical leaders around the world all of the tools they need to understand and adopt GraphQL.*". 
-->

Para obtener más información sobre la API de GraphQL, consulte las siguientes secciones (entre muchos otros recursos):

* At [graphql.org](https://graphql.org):

   * [Introducción a GraphQL](https://graphql.org/learn)

   * [Especificación de GraphQL](https://spec.graphql.org/)

* At [graphql.com](https://graphql.com):

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

   * Los esquemas se generan mediante AEM basados en los modelos de fragmento de contenido.
   * Con sus esquemas, GraphQL presenta los tipos y operaciones permitidos para la implementación de GraphQL AEM.

* **[Campos](https://graphql.org/learn/queries/#fields)**

* **[Extremo de GraphQL](graphql-endpoint.md)**
   * Ruta en AEM que responde a consultas de GraphQL y proporciona acceso a los esquemas de GraphQL.

   * Consulte [Activación del extremo de GraphQL](graphql-endpoint.md) para obtener más información.

Consulte la [(GraphQL.org) Introducción a GraphQL](https://graphql.org/learn/) para obtener información detallada, incluido el [Prácticas recomendadas](https://graphql.org/learn/best-practices/).

### Tipos de consulta de GraphQL {#graphql-query-types}

Con GraphQL puede realizar consultas para devolver:

* A **entrada única**

* A **[lista de entradas](https://graphql.org/learn/schema/#lists-and-non-null)**

También puede realizar:

* [Consultas persistentes, que se almacenan en caché](/help/headless/graphql-api/persisted-queries.md)

### GraphiQL IDE {#graphiql-ide}

Puede probar y depurar consultas de GraphQL usando la variable [GraphiQL IDE](/help/headless/graphql-api/graphiql-ide.md).

## Casos de uso para entornos de creación y publicación {#use-cases-author-publish-environments}

Los casos de uso pueden depender del tipo de entorno as a Cloud Service AEM:

* Entorno de publicación; se usa para:
   * Datos de consulta para la aplicación JS (caso de uso estándar)

* Entorno de creación; se usa para:
   * Datos de consulta para &quot;fines de administración de contenido&quot;:
      * GraphQL en AEM as a Cloud Service es actualmente una API de solo lectura.
      * La API de REST se puede utilizar para operaciones CR(u)D.

## Permisos {#permission}

Los permisos son los necesarios para acceder a Assets.

## Generación de esquemas {#schema-generation}

GraphQL es una API con establecimiento inflexible de tipos, lo que significa que los datos deben estar claramente estructurados y organizados por tipo.

La especificación de GraphQL proporciona una serie de directrices sobre cómo crear una API robusta para interrogar datos en una instancia determinada. Para ello, un cliente debe recuperar la variable [Esquema](#schema-generation), que contiene todos los tipos necesarios para una consulta.

Para los fragmentos de contenido, los esquemas (estructura y tipos) de GraphQL se basan en **Habilitado** [Modelos de fragmento de contenido](/help/assets/content-fragments/content-fragments-models.md) y sus tipos de datos.

>[!CAUTION]
>
>Todos los esquemas de GraphQL (derivados de los modelos de fragmento de contenido que se han **Habilitado**) se pueden leer a través del extremo GraphQL.
>
>Esto significa que debe asegurarse de que no hay datos confidenciales disponibles, ya que podrían filtrarse de esta manera; por ejemplo, esto incluye información que podría estar presente como nombres de campo en la definición del modelo.

Por ejemplo, si un usuario crea un modelo de fragmento de contenido denominado `Article`, luego AEM genera el objeto `article` que es de un tipo `ArticleModel`. Los campos dentro de este tipo corresponden a los campos y tipos de datos definidos en el modelo.

1. Un modelo de fragmento de contenido:

   ![Modelo de fragmento de contenido para usar con GraphQL](assets/cfm-graphqlapi-01.png "Modelo de fragmento de contenido para usar con GraphQL")

1. El esquema correspondiente de GraphQL (salida de la documentación automática de GraphiQL):
   ![Esquema de GraphQL basado en el modelo de fragmento de contenido](assets/cfm-graphqlapi-02.png "Esquema de GraphQL basado en el modelo de fragmento de contenido")

   Esto muestra que el tipo generado `ArticleModel` contiene varios [campos](#fields).

   * Tres de ellos han sido controlados por el usuario: `author`, `main` y `referencearticle`.

   * Los demás campos los agregó automáticamente AEM y representan métodos útiles para proporcionar información sobre un determinado fragmento de contenido; en este ejemplo, `_path`, `_metadata`, `_variations`. Estos [campos de ayuda](#helper-fields) se marcan con un `_` para distinguir entre lo que ha definido el usuario y lo que se ha generado automáticamente.

1. Después de que un usuario crea un fragmento de contenido basado en el modelo de artículo, se puede interrogar a través de GraphQL. Para ver ejemplos, consulte la [Consultas de ejemplo](/help/headless/graphql-api/sample-queries.md#graphql-sample-queries) (basado en un [estructura de fragmento de contenido de ejemplo para usar con GraphQL](/help/headless/graphql-api/sample-queries.md#content-fragment-structure-graphql)).

En GraphQL para AEM, el esquema es flexible. Esto significa que se genera automáticamente cada vez que se crea, actualiza o elimina un modelo de fragmento de contenido. Las cachés del esquema de datos también se actualizan al actualizar el modelo de fragmento de contenido.

El servicio Sites GraphQL escucha (en segundo plano) cualquier modificación realizada en un modelo de fragmento de contenido. Cuando se detectan actualizaciones, solo se regenera esa parte del esquema. Esta optimización ahorra tiempo y proporciona estabilidad.

Por ejemplo, si:

1. Instale un paquete que contenga `Content-Fragment-Model-1` y `Content-Fragment-Model-2`:

   1. Tipos de GraphQL para `Model-1` y `Model-2` se generará.

1. A continuación, modifique `Content-Fragment-Model-2`:

   1. Solo el `Model-2` Se actualizará el tipo de GraphQL.

   1. Considerando `Model-1` seguirá siendo el mismo.

>[!NOTE]
>
>Esto es importante tener en cuenta en caso de que desee realizar actualizaciones masivas en los modelos de fragmento de contenido a través de la api de REST o de otro modo.

El esquema se sirve a través del mismo extremo que las consultas de GraphQL, con el cliente gestionando el hecho de que se llama al esquema con la extensión `GQLschema`. Por ejemplo, realizar un `GET` solicitar en `/content/cq:graphql/global/endpoint.GQLschema` resultará en la salida del esquema con el tipo Content: `text/x-graphql-schema;charset=iso-8859-1`.

### Generación de esquemas: modelos no publicados {#schema-generation-unpublished-models}

Cuando los fragmentos de contenido están anidados, puede ocurrir que se publique un modelo de fragmento de contenido principal, pero no un modelo al que se hace referencia.

>[!NOTE]
>
>La interfaz de usuario de AEM evita que esto ocurra, pero si la publicación se realiza mediante programación o con paquetes de contenido, puede ocurrir.

Cuando esto sucede, AEM genera un *incompleto* Esquema del modelo de fragmento de contenido principal. Esto significa que la referencia de fragmento, que depende del modelo no publicado, se elimina del esquema.

## Fields {#fields}

Dentro del esquema hay campos individuales, de dos categorías básicas:

* Campos que se generan.

   Una selección de [Tipos de campo](#field-types) se utilizan para crear campos en función de cómo configure el modelo de fragmento de contenido. Los nombres de campo se toman de la variable **Nombre de propiedad** del campo **Tipo de datos**.

   * También hay **Representar como** propiedad que se debe tener en cuenta, ya que los usuarios pueden configurar ciertos tipos de datos; por ejemplo, como texto de una sola línea o como campo múltiple.

* GraphQL para AEM también genera una serie de [campos de ayuda](#helper-fields).

   Se utilizan para identificar un fragmento de contenido o para obtener más información sobre un fragmento de contenido.

### Tipos de campo {#field-types}

GraphQL para AEM admite una lista de tipos. Se representan todos los tipos de datos del modelo de fragmento de contenido compatibles y los tipos de GraphQL correspondientes:

| Modelo de fragmento de contenido: tipo de datos | Tipo de GraphQL | Descripción |
|--- |--- |--- |
| Texto de una sola línea | Cadena, [Cadena] |  Se utiliza para cadenas simples como nombres de autor, nombres de ubicación, etc. |
| Texto de varias líneas | String |  Se utiliza para generar texto como el cuerpo de un artículo |
| Número |  Flotante, [Flotante] | Se utiliza para mostrar números de coma flotante y números regulares |
| Booleano |  Booleano |  Se utiliza para mostrar casillas de verificación → instrucciones simples true/false |
| Fecha Y Hora | Calendario |  Se utiliza para mostrar la fecha y la hora en formato ISO 8086. Según el tipo seleccionado, hay tres sabores disponibles para usar en AEM GraphQL: `onlyDate`, `onlyTime`, `dateTime` |
| Enumeración |  String |  Se utiliza para mostrar una opción de una lista de opciones definidas en la creación del modelo. |
|  Etiquetas |  [String] |  Se utiliza para mostrar una lista de cadenas que representan las etiquetas utilizadas en AEM |
| Referencia de contenido |  Cadena |  Se utiliza para mostrar la ruta hacia otro recurso en AEM |
| Referencia al fragmento |  *Un tipo de modelo* |  Se utiliza para hacer referencia a otro fragmento de contenido de un tipo de modelo determinado, definido cuando se creó el modelo |

### Campos de ayuda {#helper-fields}

Además de los tipos de datos de los campos generados por el usuario, GraphQL para AEM también genera una serie de *helper* para ayudar a identificar un fragmento de contenido o para proporcionar información adicional sobre un fragmento de contenido.

#### Ruta {#path}

El campo de ruta se utiliza como identificador en GraphQL. Representa la ruta del recurso de fragmento de contenido dentro del repositorio de AEM. Se ha elegido como identificador de un fragmento de contenido, ya que:

* es único dentro de AEM,
* se pueden recuperar fácilmente.

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

Consulte [Consulta De Muestra: Un Solo Fragmento De Ciudad Específico](/help/headless/graphql-api/sample-queries.md#sample-single-specific-city-fragment).

#### Metadatos {#metadata}

A través de GraphQL, AEM también expone los metadatos de un fragmento de contenido. Los metadatos son la información que describe un fragmento de contenido, como el título de un fragmento de contenido, la ruta de vista en miniatura, la descripción de un fragmento de contenido, la fecha en que se creó, entre otros.

Dado que los metadatos se generan mediante el Editor de esquemas y, como tales, no tienen una estructura específica, la variable `TypedMetaData` El tipo de GraphQL se ha implementado para exponer los metadatos de un fragmento de contenido. `TypedMetaData` expone la información agrupada por los siguientes tipos escalares:

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

Por ejemplo, si desea recuperar el título de un fragmento de contenido, sabemos que esta propiedad es una propiedad de cadena, por lo que consultaremos todos los metadatos de cadena:

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

Puede ver todos los tipos de metadatos de GraphQL si ve el esquema de Generated GraphQL. Todos los tipos de modelo tienen el mismo `TypedMetaData`.

>[!NOTE]
>
>**Diferencia entre metadatos normales y de matriz**
>Tenga en cuenta que `StringMetadata` y `StringArrayMetadata` ambos hacen referencia a lo que se almacena en el repositorio, no a cómo se recuperan.
>
>Por ejemplo, llamando a la función `stringMetadata` , recibirá una matriz de todos los metadatos almacenados en el repositorio como un `String` y si llama a `stringArrayMetadata` recibirá una matriz de todos los metadatos almacenados en el repositorio como `String[]`.

Consulte [Consulta de ejemplo para metadatos: enumera los metadatos de los premios titulados GB](/help/headless/graphql-api/sample-queries.md#sample-metadata-awards-gb).

#### Variaciones {#variations}

La variable `_variations` se ha implementado para simplificar la consulta de las variaciones que tiene un fragmento de contenido. Por ejemplo:

```xml
{
  personByPath(_path: "/content/dam/path/to/fragment/john-doe") {
    item {
      _variations
    }
  }
}
```

Consulte [Consulta de ejemplo: todas las ciudades con una variación con nombre](/help/headless/graphql-api/sample-queries.md#sample-cities-named-variation).

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
    "variation": "uk"
}
```

## Directivas de GraphQL {#graphql-directives}

En GraphQL existe la posibilidad de cambiar la consulta en función de variables, denominadas Directivas de GraphQL.

Por ejemplo, puede incluir el `adventurePrice` en una consulta para todas las variables `AdventureModels`, en función de una variable `includePrice`.

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

Por ejemplo, la siguiente consulta (básica) filtra todas las personas que tienen un nombre de `Jobs` o `Smith`:

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

Para ver más ejemplos, consulte:

* detalles de [GraphQL para extensiones de AEM](#graphql-extensions)

* [Ejemplos de consultas que utilizan este contenido y estructura de ejemplo](/help/headless/graphql-api/sample-queries.md#graphql-sample-queries-sample-content-fragment-structure)

   * Y el [Contenido y estructura de muestra](/help/headless/graphql-api/sample-queries.md#content-fragment-structure-graphql) preparado para su uso en consultas de ejemplo

* [Consultas de muestra basadas en el proyecto WKND](/help/headless/graphql-api/sample-queries.md#sample-queries-using-wknd-project)

## GraphQL para AEM: Resumen de extensiones {#graphql-extensions}

El funcionamiento básico de las consultas con GraphQL para AEM se adhiera a la especificación estándar de GraphQL. Para las consultas de GraphQL con AEM hay algunas extensiones:

* Si necesita un solo resultado:
   * utilizar el nombre del modelo; ciudad del ejemplo

* Si espera una lista de resultados:
   * add `List` al nombre del modelo; por ejemplo,  `cityList`
   * Consulte [Consulta de muestra: toda la información sobre todas las ciudades](#sample-all-information-all-cities)

* Si desea utilizar un OR lógico:
   * use ` _logOp: OR`
   * Consulte [Consulta de muestra: todas las personas que tienen el nombre &quot;Jobs&quot; o &quot;Smith&quot;](#sample-all-persons-jobs-smith)

* AND lógico también existe, pero (a menudo) está implícito

* Puede consultar los nombres de campo que se correspondan con los campos del modelo de fragmento de contenido
   * Consulte [Consulta de muestra: Detalles completos del CEO y los empleados de una empresa](#sample-full-details-company-ceos-employees)

* Además de los campos del modelo, hay algunos campos generados por el sistema (precedidos de guiones bajos):

   * Para el contenido:

      * `_locale` : revelar el idioma; basado en el Administrador de idiomas
         * Consulte [Consulta de ejemplo para varios fragmentos de contenido de una configuración regional determinada](#sample-wknd-multiple-fragments-given-locale)
      * `_metadata` : para mostrar metadatos del fragmento
         * Consulte [Consulta de ejemplo para metadatos: enumera los metadatos de los premios titulados GB](#sample-metadata-awards-gb)
      * `_model` : permitir la consulta de un modelo de fragmento de contenido (ruta y título)
         * Consulte [Consulta de ejemplo para un modelo de fragmento de contenido de un modelo](#sample-wknd-content-fragment-model-from-model)
      * `_path` : la ruta al fragmento de contenido dentro del repositorio
         * Consulte [Consulta De Muestra: Un Solo Fragmento De Ciudad Específico](#sample-single-specific-city-fragment)
      * `_reference` : para revelar referencias; incluir referencias en línea en el Editor de texto enriquecido
         * Consulte [Consulta de ejemplo para varios fragmentos de contenido con referencias de recuperación previa](#sample-wknd-multiple-fragments-prefetched-references)
      * `_variation` : para mostrar variaciones específicas dentro del fragmento de contenido
         * Consulte [Consulta de ejemplo: todas las ciudades con una variación con nombre](#sample-cities-named-variation)
   * Y operaciones:

      * `_operator` : aplicar operadores específicos; `EQUALS`, `EQUALS_NOT`, `GREATER_EQUAL`, `LOWER`, `CONTAINS`, `STARTS_WITH`
         * Consulte [Consulta de muestra: todas las personas que no tienen un nombre de &quot;trabajos&quot;](#sample-all-persons-not-jobs)
         * Consulte [Consulta de ejemplo: todas las aventuras en las que la variable `_path` comienza con un prefijo específico](#sample-wknd-all-adventures-cycling-path-filter)
      * `_apply` : aplicar condiciones específicas; por ejemplo,  `AT_LEAST_ONCE`
         * Consulte [Consulta de muestra: filtre una matriz con un elemento que deba producirse al menos una vez](#sample-array-item-occur-at-least-once)
      * `_ignoreCase` : para ignorar el caso al consultar
         * Consulte [Consulta de muestra: todas las ciudades con SAN en el nombre, independientemente del caso](#sample-all-cities-san-ignore-case)









* Se admiten los tipos de unión de GraphQL:

   * use `... on`
      * Consulte [Consulta de ejemplo para un fragmento de contenido de un modelo específico con una referencia de contenido](#sample-wknd-fragment-specific-model-content-reference)

* Reserva cuando se consultan fragmentos anidados:

   * Si una variación determinada no existe en un fragmento anidado, entonces la variable **Maestro** se devolvería.

## Consulta del extremo de GraphQL desde un sitio web externo {#query-graphql-endpoint-from-external-website}

Para acceder al extremo de GraphQL desde un sitio web externo, debe configurar:

* [Filtro CORS](/help/headless/deployment/cross-origin-resource-sharing.md)
* [Filtro de referente](/help/headless/deployment/referrer-filter.md)

## Autenticación {#authentication}

Consulte [Autenticación para consultas de GraphQL remotas en fragmentos de contenido](/help/headless/security/authentication.md).

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

1. **Q**: &quot;*¿En qué se diferencia la API de GraphQL de la API de Query Builder AEM*&quot;

   * **A**: &quot;*La API de AEM GraphQL ofrece control total sobre la salida JSON y es un estándar del sector para consultar contenido.
En adelante, AEM tiene previsto invertir en la API de AEM GraphQL.*&quot;

## Tutorial: Introducción a AEM sin encabezado y GraphQL {#tutorial}

¿Busca un tutorial práctico? Consulte [Introducción a AEM Headless y GraphQL](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/overview.html) tutorial completo que ilustra cómo crear y exponer contenido mediante las API de GraphQL de AEM y consumido por una aplicación externa, en un escenario de CMS sin encabezado.
