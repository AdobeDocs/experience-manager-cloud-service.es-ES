---
title: API de AEM GraphQL para usar con fragmentos de contenido
description: Descubra cómo usar fragmentos de contenido en Adobe Experience Manager (AEM) como Cloud Service con el Envío de contenido sin encabezado de la API de GraphQL de AEM.
translation-type: tm+mt
source-git-commit: 20f90d46d24fa211d51ef4b59bb56f4b9f963bc3
workflow-type: tm+mt
source-wordcount: '3167'
ht-degree: 1%

---


# API de AEM GraphQL para usar con fragmentos de contenido {#graphql-api-for-use-with-content-fragments}

La API de Adobe Experience Manager como Cloud Service (AEM) GraphQL utilizada con fragmentos de contenido se basa en gran medida en la API GraphQL estándar de código abierto.

El uso de la API de GraphQL en AEM permite el envío eficiente de fragmentos de contenido a clientes JavaScript en implementaciones CMS sin encabezado:

* Evitar solicitudes de API iterativas como con REST,
* Garantizar que el envío se limite a los requisitos específicos,
* Permite el envío masivo de exactamente lo que se necesita para el procesamiento como respuesta a una única consulta de API.

## La API de GraphQL {#graphql-api}

GraphQL es:

* &quot;*...un lenguaje de consulta para las API y un tiempo de ejecución para cumplir esas consultas con los datos existentes. GraphQL proporciona una descripción completa y comprensible de los datos de su API, brinda a los clientes la capacidad de preguntar exactamente lo que necesitan y nada más, facilita la evolución de las API con el tiempo y permite herramientas potentes para desarrolladores.*&quot;.

   Consulte [GraphQL.org](https://graphql.org)

* &quot;*...una especificación abierta para una capa de API flexible. Coloque GraphQL sobre los servidores de fondo existentes para crear productos más rápido que nunca....*&quot;.

   Consulte [Explorar GraphQL](https://www.graphql.com).

* *&quot;...un lenguaje de consulta de datos y una especificación desarrollados internamente por Facebook en 2012 antes de ser de código abierto público en 2015. Proporciona una alternativa a las arquitecturas basadas en REST con el propósito de aumentar la productividad del desarrollador y minimizar las cantidades de datos transferidos. GraphQL se utiliza en la producción por cientos de organizaciones de todos los tamaños...&quot;*

   Consulte [GraphQL Foundation](https://foundation.graphql.org/).

<!--
"*Explore GraphQL is maintained by the Apollo team. Our goal is to give developers and technical leaders around the world all of the tools they need to understand and adopt GraphQL.*". 
-->

Para obtener más información sobre la API de GraphQL, consulte las secciones siguientes (entre muchos otros recursos):

* En [graphql.org](https://graphql.org):

   * [Introducción a GraphQL](https://graphql.org/learn)

   * [Especificación GraphQL](http://spec.graphql.org/)

* En [graphql.com](https://graphql.com):

   * [Guías](https://www.graphql.com/guides/)

   * [Tutoriales](https://www.graphql.com/tutorials/)

   * [Casos prácticos](https://www.graphql.com/case-studies/)

La implementación de GraphQL para AEM se basa en la biblioteca Java GraphQL estándar. Consulte:

* [graphQL.org - Java](https://graphql.org/code/#java)

* [GraphQL Java en GitHub](https://github.com/graphql-java)

### Terminología de GraphQL {#graphql-terminology}

GraphQL utiliza lo siguiente:

* **[Consultas](https://graphql.org/learn/queries/)**

* **[Esquemas y tipos](https://graphql.org/learn/schema/)**:

   * Los esquemas se generan mediante AEM basados en los modelos de fragmento de contenido.
   * Con sus esquemas, GraphQL presenta los tipos y operaciones permitidos para la implementación de GraphQL AEM.

* **[Campos](https://graphql.org/learn/queries/#fields)**

* **[Extremo de GraphQL](#graphql-aem-endpoint)**
   * Ruta de AEM que responde a consultas de GraphQL y proporciona acceso a los esquemas de GraphQL.

   * Consulte [Habilitación del Extremo de GraphQL](#enabling-graphql-endpoint) para obtener más detalles.

Consulte la [(GraphQL.org) Introducción a GraphQL](https://graphql.org/learn/) para obtener información detallada, incluidas las [optimizaciones](https://graphql.org/learn/best-practices/).

### Tipos de Consulta de GraphQL {#graphql-query-types}

Con GraphQL puede realizar consultas para devolver una de las acciones siguientes:

* Una **entrada única**

* Una **[lista de entradas](https://graphql.org/learn/schema/#lists-and-non-null)**

También puede realizar:

* [Consultas persistentes que se almacenan en caché](#persisted-queries-caching)

## GraphQL para AEM extremo {#graphql-aem-endpoint}

El punto final es la ruta que se utiliza para acceder a GraphQL para AEM. Con esta ruta usted (o su aplicación) puede:

* acceder al esquema GraphQL,
* enviar sus consultas de GraphQL,
* reciba las respuestas (a sus consultas de GraphQL).

La ruta del repositorio de GraphQL para AEM extremo es:

`/content/cq:graphql/global/endpoint`

La aplicación puede utilizar la siguiente ruta en la dirección URL de la solicitud:

`/content/_cq_graphql/global/endpoint.json`

Para habilitar el punto final de GraphQL para AEM debe:

>[!CAUTION]
>
>Es probable que estos pasos cambien en un futuro próximo.

* [Habilitar el extremo de GraphQL](#enabling-graphql-endpoint)
* [Realizar configuraciones adicionales](#additional-configurations-graphql-endpoint)

### Habilitación del extremo de GraphQL {#enabling-graphql-endpoint}

>[!NOTE]
>
>Consulte [Paquetes de soporte](#supporting-packages) para obtener detalles de los paquetes que Adobe proporciona para ayudar a simplificar estos pasos.

Para habilitar consultas de GraphQL en AEM, cree un punto final en `/content/cq:graphql/global/endpoint`:

* Los nodos `cq:graphql` y `global` deben ser del tipo `sling:Folder`.
* El nodo `endpoint` debe ser de tipo `nt:unstructured` y contener `sling:resourceType` de `graphql/sites/components/endpoint`.

>[!CAUTION]
>
>Actualmente hay un problema conocido con el punto final:
>
>* La entrada `cq:graphql` se ve en la consola **Sites**; en el nivel superior.
   >  No debe usarse.


>[!CAUTION]
>
>Todos pueden acceder al punto final. Esto puede suponer un problema de seguridad, especialmente en las instancias de publicación, ya que las consultas de GraphQL pueden imponer una carga pesada en el servidor.
>
>Puede configurar las ACL, según el caso de uso, en el extremo.

>[!NOTE]
>
>El punto final no funcionará de forma predeterminada. Deberá proporcionar [configuraciones adicionales para el extremo de GraphQL](#additional-configurations-graphql-endpoint) por separado.

>[!NOTE]
>Además, puede probar y depurar consultas de GraphQL con el [IDE de GraphiQL](#graphiql-interface).

### Configuraciones adicionales para el extremo de GraphQL {#additional-configurations-graphql-endpoint}

>[!NOTE]
>
>Consulte [Paquetes de soporte](#supporting-packages) para obtener detalles de los paquetes que Adobe proporciona para ayudar a simplificar estos pasos.

Se requieren configuraciones adicionales:

* Dispatcher:
   * Para permitir direcciones URL requeridas
   * Obligatorio
* URL de vanidad:
   * Asignación de una dirección URL simplificada para el extremo
   * Opcional
* Configuración de OSGi:
   * Configuración del servlet GraphQL:
      * Gestiona las solicitudes al extremo
      * El nombre de la configuración es `org.apache.sling.graphql.core.GraphQLServlet`. Debe proporcionarse como una configuración de fábrica OSGi
      * `sling.servlet.extensions` debe configurarse en  `[json]`
      * `sling.servlet.methods` debe configurarse en  `[GET,POST]`
      * `sling.servlet.resourceTypes` debe configurarse en  `[graphql/sites/components/endpoint]`
      * Obligatorio
   * Configuración del servlet esquema:
      * Crea el esquema GraphQL
      * El nombre de la configuración es `com.adobe.aem.graphql.sites.adapters.SlingSchemaServlet`. Debe proporcionarse como una configuración de fábrica OSGi
      * `sling.servlet.extensions` debe configurarse en  `[GQLschema]`
      * `sling.servlet.methods` debe configurarse en  `[GET]`
      * `sling.servlet.resourceTypes` debe configurarse en  `[graphql/sites/components/endpoint]`
      * Obligatorio
   * Configuración de CSRF:
      * Protección de seguridad para el punto final
      * El nombre de configuración es `com.adobe.granite.csrf.impl.CSRFFilter`
      * Añadir `/content/cq:graphql/global/endpoint` a la lista existente de rutas excluidas (`filter.excluded.paths`)
      * Obligatorio

### Paquetes de soporte {#supporting-packages}

Para simplificar la configuración de un extremo de GraphQL, Adobe proporciona el paquete [Proyecto de muestra de GraphQL](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faemcloud%2Fpublic%2Faem-graphql%2Fgraphql-sample.zip).

Este archivo contiene [la configuración adicional requerida](#additional-configurations-graphql-endpoint) y [el extremo de GraphQL](#enabling-graphql-endpoint). Si se instala en una instancia de AEM sin formato, se mostrará un extremo GraphQL completamente operativo en `/content/cq:graphql/global/endpoint`.

Este paquete está diseñado para ser un modelo para sus propios proyectos GraphQL. Consulte el paquete **README** para obtener más información sobre cómo usar el paquete.

Si prefiere crear manualmente la configuración requerida, Adobe también proporciona un [Paquete de contenido de punto final de GraphQL](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faemcloud%2Fpublic%2Faem-graphql%2Fgraphql-global-endpoint.zip) dedicado. Este paquete de contenido solo contiene el extremo GraphQL, sin ninguna configuración.

## Interfaz GraphiQL {#graphiql-interface}

<!--
AEM Graph API includes an implementation of the standard [GraphiQL](https://graphql.org/learn/serving-over-http/#graphiql) interface. This allows you to directly input, and test, queries.
-->

Hay una implementación de la interfaz estándar [GraphiQL](https://graphql.org/learn/serving-over-http/#graphiql) disponible para su uso con AEM GraphQL. Esto se puede [instalar con AEM](#installing-graphiql-interface).

Esta interfaz le permite introducir directamente y probar consultas.

Por ejemplo:

* `http://localhost:4502/content/graphiql.html`

Esto proporciona funciones como el resaltado de sintaxis, la finalización automática y la sugerencia automática, junto con un historial y documentación en línea:

![Interfaz ](assets/cfm-graphiql-interface.png "de GraphiQL Interfaz de GraphiQL")

### Instalación de la interfaz AEM GraphiQL {#installing-graphiql-interface}

La interfaz de usuario de GraphiQL se puede instalar en AEM con un paquete dedicado: el paquete [GraphiQL Content Package v0.0.4](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faemcloud%2Fpublic%2Faem-graphql%2Fgraphiql-0.0.4.zip).

<!--
See the package **README** for full details; including full details of how it can be installed on an AEM instance - in a variety of scenarios.
-->

## Casos de uso para Entornos de creación y publicación {#use-cases-author-publish-environments}

Los casos de uso pueden depender del tipo de AEM como entorno de Cloud Service:

* Entorno de publicación; utilizado para:
   * Datos de consulta para la aplicación JS (caso de uso estándar)

* Entorno del autor; utilizado para:
   * Datos de consulta con &quot;fines de gestor de contenido&quot;:
      * GraphQL en AEM como Cloud Service es actualmente una API de solo lectura.
      * La API de REST se puede utilizar para operaciones CR(u)D.

## Permisos    {#permission}

Los permisos son los necesarios para acceder a Recursos.

## Generación de esquemas {#schema-generation}

GraphQL es una API con establecimiento inflexible de tipos, lo que significa que los datos deben estar claramente estructurados y organizados por tipo.

La especificación GraphQL proporciona una serie de directrices sobre cómo crear una API sólida para interrogar datos en una instancia determinada. Para ello, un cliente necesita recuperar el [Esquema](#schema-generation), que contiene todos los tipos necesarios para una consulta.

Para los fragmentos de contenido, los esquemas de GraphQL (estructura y tipos) se basan en **Modelos de fragmento de contenido** [Habilitados](/help/assets/content-fragments/content-fragments-models.md) y sus tipos de datos.

>[!CAUTION]
>
>Todos los esquemas de GraphQL (derivados de los modelos de fragmento de contenido que han estado **habilitados**) son legibles a través del extremo de GraphQL.
>
>Esto significa que debe asegurarse de que no hay datos confidenciales disponibles, ya que podrían filtrarse de esta manera; por ejemplo, esto incluye información que podría estar presente como nombres de campo en la definición del modelo.

Por ejemplo, si un usuario ha creado un modelo de fragmento de contenido denominado `Article`, AEM genera el objeto `article` que es de un tipo `ArticleModel`. Los campos dentro de este tipo corresponden a los campos y tipos de datos definidos en el modelo.

1. Un modelo de fragmento de contenido:

   ![Modelo de fragmento de contenido para usar con ](assets/cfm-graphqlapi-01.png "GraphQLContent Fragment Model para GraphQL")

1. El esquema correspondiente de GraphQL (salida de la documentación automática de GraphiQL):
   ![Esquema de GraphQL basado en el ](assets/cfm-graphqlapi-02.png "modelo de fragmento de contenidoEsquema de GraphQL basado en el modelo de fragmento de contenido")

   Esto muestra que el tipo generado `ArticleModel` contiene varios [campos](#fields).

   * Tres de ellos han sido controlados por el usuario: `author`, `main` y `referencearticle`.

   * Los otros campos fueron agregados automáticamente por AEM y representan métodos útiles para proporcionar información sobre un determinado fragmento de contenido; en este ejemplo, `_path`, `_metadata`, `_variations`. Estos [campos de ayuda](#helper-fields) están marcados con un antecedente `_` para distinguir entre lo que el usuario ha definido y lo que se ha generado automáticamente.

1. Después de que un usuario crea un fragmento de contenido basado en el modelo de artículo, se puede interrogarlo a través de GraphQL. Para obtener ejemplos, consulte las [Consultas de muestra](/help/assets/content-fragments/content-fragments-graphql-samples.md#graphql-sample-queries) (basadas en una [estructura de fragmento de contenido de muestra para su uso con GraphQL](/help/assets/content-fragments/content-fragments-graphql-samples.md#content-fragment-structure-graphql)).

En GraphQL para AEM, el esquema es flexible. Esto significa que se genera automáticamente cada vez que se crea, actualiza o elimina un modelo de fragmento de contenido. Las memorias caché de esquema de datos también se actualizan al actualizar un modelo de fragmento de contenido.

El servicio Sites GraphQL escucha (en segundo plano) las modificaciones realizadas en un modelo de fragmento de contenido. Cuando se detectan actualizaciones, solo se regenera esa parte del esquema. Esta optimización ahorra tiempo y proporciona estabilidad.

Por ejemplo, si:

1. Instale un paquete que contenga `Content-Fragment-Model-1` y `Content-Fragment-Model-2`:

   1. Se generarán los tipos GraphQL para `Model-1` y `Model-2`.

1. A continuación, modifique `Content-Fragment-Model-2`:

   1. Solo se actualizará el tipo `Model-2` GraphQL.

   1. Mientras que `Model-1` permanecerá igual.

>[!NOTE]
>
>Esto es importante tener en cuenta en caso de que desee realizar actualizaciones masivas en los modelos de fragmentos de contenido a través de la API de REST o de otro modo.

El esquema se suministra a través del mismo punto final que las consultas de GraphQL, y el cliente se encarga de que se llame al esquema con la extensión `GQLschema`. Por ejemplo: al realizar una solicitud `GET` simple en `/content/cq:graphql/global/endpoint.GQLschema`, se producirá el resultado del esquema con el tipo de contenido: `text/x-graphql-schema;charset=iso-8859-1`.

## Fields {#fields}

Dentro del esquema hay campos individuales, de dos categorías básicas:

* Campos que se generan.

   Se utiliza una selección de [Tipos de campo](#field-types) para crear campos en función de cómo configure el modelo de fragmento de contenido. Los nombres de campo se toman del campo **Nombre de propiedad** del **Tipo de datos**.

   * También hay que tener en cuenta la propiedad **Representar como**, ya que los usuarios pueden configurar determinados tipos de datos; por ejemplo, como un texto de una sola línea o un campo múltiple.

* GraphQL para AEM también genera un número de [campos de ayuda](#helper-fields).

   Se utilizan para identificar un fragmento de contenido o para obtener más información sobre un fragmento de contenido.

### Tipos de campos {#field-types}

GraphQL para AEM admite una lista de tipos. Se representan todos los tipos de datos del modelo de fragmento de contenido admitidos y los correspondientes tipos de GraphQL:

| Modelo de fragmento de contenido: tipo de datos | Tipo GraphQL | Descripción |
|--- |--- |--- |
| Texto de una sola línea | Cadena, [Cadena] |  Se utiliza para cadenas sencillas como nombres de autor, nombres de ubicación, etc. |
| Texto de varias líneas | Cadena |  Se utiliza para escribir texto de salida, como el cuerpo de un artículo |
| Número |  Flotante, [Flotante] | Se utiliza para mostrar números de coma flotante y números regulares |
| Booleano |  Booleano |  Se utiliza para mostrar casillas de verificación → afirmaciones simples true/false |
| Fecha Y Hora | Calendario |  Se utiliza para mostrar la fecha y la hora en formato ISO 8086 |
| Enumeración |  Cadena |  Se utiliza para mostrar una opción de una lista de opciones definidas en la creación del modelo |
|  Etiquetas |  [Cadena] |  Se utiliza para mostrar una lista de cadenas que representan etiquetas utilizadas en AEM |
| Referencia de contenido |  Cadena |  Se utiliza para mostrar la ruta hacia otro recurso en AEM |
| Referencia al fragmento |  *Tipo de modelo* |  Se utiliza para hacer referencia a otro fragmento de contenido de un tipo de modelo determinado, definido cuando se creó el modelo |

### Campos de ayuda {#helper-fields}

Además de los tipos de datos para los campos generados por el usuario, GraphQL para AEM también genera una serie de campos *ayudantes* para ayudar a identificar un fragmento de contenido o para proporcionar información adicional sobre un fragmento de contenido.

#### Ruta {#path}

El campo de ruta se utiliza como identificador en GraphQL. Representa la ruta del recurso Fragmento de contenido dentro del repositorio de AEM. Se ha elegido como identificador de un fragmento de contenido, ya que:

* es único dentro de AEM,
* se puede recuperar fácilmente.

El siguiente código mostrará las rutas de todos los fragmentos de contenido que se crearon en función del modelo de fragmento de contenido `Person`.

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

Consulte [Consulta de muestra: un solo fragmento de ciudad específico](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-single-specific-city-fragment).

#### Metadatos {#metadata}

A través de GraphQL, AEM también expone los metadatos de un fragmento de contenido. Los metadatos son la información que describe un fragmento de contenido, como el título de un fragmento de contenido, la ruta de la miniatura, la descripción de un fragmento de contenido, la fecha en que se creó, entre otros.

Dado que los metadatos se generan a través del Editor de Esquemas y, como tal, no tienen una estructura específica, el tipo `TypedMetaData` GraphQL se implementó para exponer los metadatos de un fragmento de contenido. `TypedMetaData` expone la información agrupada por los siguientes tipos escalares:

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

Cada tipo escalar representa un solo par nombre-valor o una matriz de pares nombre-valor, donde el valor de ese par es del tipo en que se agrupó.

Por ejemplo, si desea recuperar el título de un fragmento de contenido, sabemos que esta propiedad es una propiedad String, por lo que se realizará una consulta de todos los metadatos String:

Para la consulta de metadatos:

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

Puede realizar la vista de todos los tipos GraphQL de los metadatos si realiza la vista del esquema Generated GraphQL. Todos los tipos de modelo tienen el mismo `TypedMetaData`.

>[!NOTE]
>
>**Diferencia entre metadatos normales y de matriz**
>Tenga en cuenta que `StringMetadata` y `StringArrayMetadata` hacen referencia a lo que se almacena en el repositorio, no a cómo se recuperan.
>
>Por ejemplo: al llamar al campo `stringMetadata`, recibirá una matriz de todos los metadatos almacenados en el repositorio como `String` y, si llama a `stringArrayMetadata`, recibirá una matriz de todos los metadatos almacenados en el repositorio como `String[]`.

Consulte [Consulta de muestra para metadatos: Lista de los metadatos de los premios titulados GB](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-metadata-awards-gb).

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

Consulte [Consulta de muestra: Todas las ciudades con una variación con nombre](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-cities-named-variation).

<!--
## Security Considerations {#security-considerations}
-->

## Variables de GraphQL {#graphql-variables}

GraphQL permite colocar variables en la consulta. Para obtener más información, consulte la documentación de [GraphQL para GraphiQL](https://graphql.org/learn/queries/#variables).

Por ejemplo: para obtener todos los fragmentos de contenido de tipo `Article` que tienen una variación específica, puede especificar la variable `variation` en GraphiQL.

![Variables ](assets/cfm-graphqlapi-03.png "GraphQL")

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

En GraphQL existe la posibilidad de cambiar la consulta en función de variables, llamadas Directivas GraphQL.

Por ejemplo: puede incluir el campo `adventurePrice` en una consulta para todos los `AdventureModels`, en base a una variable `includePrice`.

![Directivas ](assets/cfm-graphqlapi-04.png "de GraphQL Directivas de GraphQL")

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

El filtrado utiliza una sintaxis basada en expresiones y operadores lógicos.

Por ejemplo, la siguiente consulta (básica) filtros a todas las personas que tengan un nombre `Jobs` o `Smith`:

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

Para obtener más ejemplos, consulte:

* detalles de [GraphQL para extensiones de AEM](/help/assets/content-fragments/content-fragments-graphql-samples.md#graphql-extensions)

* [Consultas de muestra que utilizan este contenido y estructura de muestra](/help/assets/content-fragments/content-fragments-graphql-samples.md#graphql-sample-queries-sample-content-fragment-structure)

   * Y el [Contenido y estructura de muestra](/help/assets/content-fragments/content-fragments-graphql-samples.md#content-fragment-structure-graphql) se preparan para utilizarse en consultas de muestra

* [Consultas de muestra basadas en el proyecto WKND](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-queries-using-wknd-project)

## Consultas persistentes (almacenamiento en caché) {#persisted-queries-caching}

Después de preparar una consulta con una solicitud de POST, se puede ejecutar con una solicitud de GET que se puede almacenar en caché mediante memorias caché HTTP o CDN.

Esto es necesario, ya que las consultas de POST no suelen almacenarse en caché y, si se utiliza la GET con la consulta como parámetro, existe un riesgo significativo de que el parámetro sea demasiado grande para los servicios HTTP e intermediarios.

Estos son los pasos necesarios para mantener una consulta determinada:

>[!NOTE]
>Antes de esto, las **Consultas de persistencia de GraphQL** deben habilitarse para la configuración adecuada. Consulte [Habilitar la funcionalidad de fragmento de contenido en el navegador de configuración](/help/assets/content-fragments/content-fragments-configuration-browser.md#enable-content-fragment-functionality-in-configuration-browser) para obtener más información.

1. Prepare la consulta agregándola a la nueva dirección URL del extremo `/graphql/persist.json/<config>/<persisted-label>`.

   Por ejemplo, cree una consulta persistente:

   ```xml
   $ curl -X PUT \
       -H 'authorization: Basic YWRtaW46YWRtaW4=' \
       -H "Content-Type: application/json" \
       "http://localhost:4502/graphql/persist.json/wknd/plain-article-query" \
       -d \
   '{
     articleList {
       items{
           _path
           author
           main {
               json
           }
       }
     }
   }'
   ```

1. En este punto, compruebe la respuesta.

   Por ejemplo, compruebe si la operación ha sido correcta:

   ```xml
   {
     "action": "create",
     "configurationName": "wknd",
     "name": "plain-article-query",
     "shortPath": "/wknd/plain-article-query",
     "path": "/conf/wknd/settings/graphql/persistentQueries/plain-article-query"
   }
   ```

1. Luego puede reproducir la consulta persistente obteniendo la dirección URL `/graphql/execute.json/<shortPath>`.

   Por ejemplo, utilice la consulta persistente:

   ```xml
   $ curl -X GET \
       http://localhost:4502/graphql/execute.json/wknd/plain-article-query
   ```

1. Actualice una consulta persistente mediante POSTing a una ruta de consulta ya existente.

   Por ejemplo, utilice la consulta persistente:

   ```xml
   $ curl -X POST \
       -H 'authorization: Basic YWRtaW46YWRtaW4=' \
       -H "Content-Type: application/json" \
       "http://localhost:4502/graphql/persist.json/wknd/plain-article-query" \
       -d \
   '{
     articleList {
       items{
           _path
           author
           main {
               json
           }
         referencearticle {
           _path
         }
       }
     }
   }'
   ```

1. Cree una consulta sin formato ajustada.

   Por ejemplo:

   ```xml
   $ curl -X PUT \
       -H 'authorization: Basic YWRtaW46YWRtaW4=' \
       -H "Content-Type: application/json" \
       "http://localhost:4502/graphql/persist.json/wknd/plain-article-query-wrapped" \
       -d \
   '{ "query": "{articleList { items { _path author main { json } referencearticle { _path } } } }"}'
   ```

1. Cree una consulta sin formato ajustada con control de caché.

   Por ejemplo:

   ```xml
   $ curl -X PUT \
       -H 'authorization: Basic YWRtaW46YWRtaW4=' \
       -H "Content-Type: application/json" \
       "http://localhost:4502/graphql/persist.json/wknd/plain-article-query-max-age" \
       -d \
   '{ "query": "{articleList { items { _path author main { json } referencearticle { _path } } } }", "cache-control": { "max-age": 300 }}'
   ```

1. Cree una consulta persistente con parámetros:

   Por ejemplo:

   ```xml
   $ curl -X PUT \
       -H 'authorization: Basic YWRtaW46YWRtaW4=' \
       -H "Content-Type: application/json" \
       "http://localhost:4502/graphql/persist.json/wknd/plain-article-query-parameters" \
       -d \
   'query GetAsGraphqlModelTestByPath($apath: String!, $withReference: Boolean = true) {
     articleByPath(_path: $apath) {
       item {
         _path
           author
           main {
           plaintext
           }
           referencearticle @include(if: $withReference) {
           _path
           }
         }
       }
     }'
   ```

1. Ejecución de una consulta con parámetros.

   Por ejemplo:

   ```xml
   $ curl -X POST \
       -H 'authorization: Basic YWRtaW46YWRtaW4=' \
       -H "Content-Type: application/json" \
       "http://localhost:4502/graphql/execute.json/wknd/plain-article-query-parameters;apath=%2fcontent2fdam2fwknd2fen2fmagazine2falaska-adventure2falaskan-adventures;withReference=false"
   
   $ curl -X GET \
       "http://localhost:4502/graphql/execute.json/wknd/plain-article-query-parameters;apath=%2fcontent2fdam2fwknd2fen2fmagazine2falaska-adventure2falaskan-adventures;withReference=false"
   ```

1. Para ejecutar la consulta al publicar, es necesario replicar el árbol persistente relacionado

   * Uso de un POST para replicación:

      ```xml
      $curl -X POST   http://localhost:4502/bin/replicate.json \
        -H 'authorization: Basic YWRtaW46YWRtaW4=' \
        -F path=/conf/wknd/settings/graphql/persistentQueries/plain-article-query \
        -F cmd=activate
      ```

   * Uso de un paquete:
      1. Cree una nueva definición de paquete.
      1. Incluya la configuración (por ejemplo, `/conf/wknd/settings/graphql/persistentQueries`).
      1. Cree el paquete.
      1. Replique el paquete.
   * Uso de la herramienta de replicación y distribución.
      1. Vaya a la herramienta Distribución.
      1. Seleccione la activación de árbol para la configuración (por ejemplo, `/conf/wknd/settings/graphql/persistentQueries`).
   * Uso de un flujo de trabajo (mediante la configuración del iniciador del flujo de trabajo):
      1. Defina una regla de inicio de flujo de trabajo para ejecutar un modelo de flujo de trabajo que replique la configuración en diferentes eventos (por ejemplo, crear, modificar, entre otros).



1. Una vez que la configuración de la consulta está en la publicación, se aplican los mismos principios, solo con usar el punto final de publicación.

   >[!NOTE]
   >
   >Para el acceso anónimo, el sistema asume que la ACL permite que &quot;todos&quot; tengan acceso a la configuración de consulta.
   >
   >Si ese no es el caso, no podrá ejecutarse.

   >[!NOTE]
   >
   >Se debe codificar cualquier punto y coma (&quot;;&quot;) en las direcciones URL.
   >
   >Por ejemplo, como en la solicitud para ejecutar una consulta persistente:
   >
   >
   ```xml
   >curl -X GET \ "http://localhost:4502/graphql/execute.json/wknd/plain-article-query-parameters%3bapath=%2fcontent2fdam2fwknd2fen2fmagazine2falaska-adventure2falaskan-adventures;withReference=false"
   >```

## Consulta del extremo de GraphQL desde un sitio Web externo {#query-graphql-endpoint-from-external-website}

>[!NOTE]
>
>Para obtener una descripción detallada de la política de uso compartido de recursos CORS en AEM, consulte [Comprender el uso compartido de recursos entre Orígenes (CORS)](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/security/understand-cross-origin-resource-sharing.html?lang=en#understand-cross-origin-resource-sharing-(cors)).

Para permitir que un sitio web de terceros consuma salida JSON, se debe configurar una directiva CORS en el repositorio Git del cliente. Esto se realiza agregando un archivo de configuración OSGi CORS apropiado para el extremo deseado. Esta configuración debe especificar un nombre de sitio web (o regex) de confianza para el cual se debe conceder acceso.

* Acceso al extremo GraphQL:

   * allowOriginal: [su dominio] o allow originregexp: [su dominio regex]
   * métodos admitidos: [POST]
   * paths permitidos: [&quot;/content/graphql/global/endpoint.json&quot;]

* Acceso al extremo de consultas persistentes de GraphQL:

   * allowOriginal: [su dominio] o allow originregexp: [su dominio regex]
   * métodos admitidos: [GET]
   * paths permitidos: [&quot;/graphql/execute.json/.*&quot;]

>[!CAUTION]
>
>Sigue siendo responsabilidad del cliente:
>
>* solo conceder acceso a dominios de confianza
>* asegúrese de que no se expone ninguna información confidencial
>* no utilizar una sintaxis comodín [*]; esto deshabilitará el acceso autenticado al extremo GraphQL y también lo expondrá a todo el mundo.


>[!CAUTION]
>
>Todos los esquemas de GraphQL [](#schema-generation) (derivados de los modelos de fragmento de contenido que han estado **habilitados**) son legibles a través del extremo de GraphQL.
>
>Esto significa que debe asegurarse de que no hay datos confidenciales disponibles, ya que podrían filtrarse de esta manera; por ejemplo, esto incluye información que podría estar presente como nombres de campo en la definición del modelo.

## Autenticación {#authentication}

Consulte [Autenticación para Consultas GraphQL de AEM remoto en fragmentos de contenido](/help/assets/content-fragments/graphql-authentication-content-fragments.md).

<!-- to be addressed later -->

<!--
## Sorting {#sorting}
-->

<!-- to be addressed later -->

<!--
## Paging {#paging}
-->

## Preguntas más frecuentes {#faqs}

Preguntas que han surgido:

1. **P**: &quot;¿*En qué se diferencia la API de GraphQL para AEM de la API de Consulta Builder?*&quot;

   * **A**: &quot;*La API de GraphQL de AEM oferta el control total de la salida JSON y es un estándar del sector para consultar el contenido.
A partir de ahora, AEM está planeando invertir en la API de GraphQL de AEM.*&quot;

## Tutorial: Introducción a AEM sin encabezado y GraphQL {#tutorial}

¿Busca un tutorial práctico? Consulte [Introducción a AEM sin encabezado y GraphQL](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/overview.html) tutorial completo que ilustra cómo crear y exponer contenido mediante las API de GraphQL de AEM y consumido por una aplicación externa, en un escenario CMS sin encabezado.
