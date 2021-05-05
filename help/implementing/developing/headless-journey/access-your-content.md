---
title: Cómo acceder al contenido a través de las API de envío de AEM
description: En esta parte del Recorrido para desarrolladores sin encabezado de AEM, aprenda a utilizar las consultas de GraphQL para acceder al contenido de los fragmentos de contenido.
hide: true
hidefromtoc: true
index: false
exl-id: 5ef557ff-e299-4910-bf8c-81c5154ea03f
translation-type: tm+mt
source-git-commit: 7b04ae2bfa75fe3d3af13271efe567a5fc401f49
workflow-type: tm+mt
source-wordcount: '4636'
ht-degree: 1%

---

# Cómo acceder al contenido a través de las API de envío de AEM {#access-your-content}

>[!CAUTION]
>
>TRABAJO EN CURSO - La creación de este documento está en curso y no debe entenderse como completo o definitivo ni debe utilizarse con fines de producción.

En esta parte del [AEM Recorrido para desarrolladores sin encabezado,](overview.md) puede aprender a utilizar las consultas de GraphQL para acceder al contenido de sus fragmentos de contenido.

## La historia hasta ahora {#story-so-far}

En el documento anterior del recorrido AEM sin encabezado, [Cómo modelar el contenido](model-your-content.md) ha aprendido los conceptos básicos del modelado de datos en AEM, por lo que ahora debe comprender cómo modelar la estructura de contenido y, a continuación, comprender esa estructura utilizando AEM modelos de fragmentos de contenido y fragmentos de contenido:

* Reconocer los conceptos y la terminología relacionados con el [modelado de datos](#data-modeling).
* Comprenda [por qué se necesita el modelado de datos para el envío de contenido sin encabezado](#data-modeling-for-aem-headless).
* Comprender [cómo llevar a cabo esta estructura utilizando AEM modelos de fragmento de contenido](#create-structure-content-fragment-models) (y crear contenido con [fragmentos de contenido](#use-content-to-author-content)).
* Comprender [cómo modelar el contenido](#getting-started-examples); principios con muestras básicas.

Este artículo se basa en estos aspectos básicos para que pueda comprender cómo acceder al contenido sin encabezado existente en AEM mediante la API de GraphQL de AEM.

* **Audiencia**: Principiante
* **Objetivo**: Obtenga información sobre cómo acceder al contenido de los fragmentos de contenido mediante AEM consultas de GraphQL:
   * Presente GraphQL y la API de AEM GraphQL.
   * Descubra los detalles de la API de AEM GraphQL.
   * Observe algunas consultas de ejemplo para ver cómo funcionan las cosas en la práctica.

## ¿Desea acceder a sus datos? {#so-youd-like-to-access-your-data}

Así que...tiene todo este contenido, bien estructurado (en fragmentos de contenido) y esperando para alimentar su nueva aplicación. La pregunta es: ¿cómo llegar allí?

Lo que necesita es una forma de segmentar contenido específico, seleccionar lo que necesita y devolverlo a su aplicación para un procesamiento posterior.

Con Adobe Experience Manager (AEM) como Cloud Service, puede acceder selectivamente a sus fragmentos de contenido mediante la API de GraphQL de AEM para devolver solo el contenido que necesita. Esto significa que puede realizar envíos sin objetivos de contenido estructurado para utilizarlo en sus aplicaciones.

>[!NOTE]
>
>AEM API de GraphQL es una implementación personalizada, basada en GraphQL estándar.

## GraphQL: Introducción {#graphql-introduction}

GraphQL es una especificación de código abierto que proporciona:

* lenguaje de consulta que permite seleccionar contenido específico de objetos estructurados.
* un tiempo de ejecución para realizar estas consultas con el contenido estructurado.

GraphQL es una API con *tipos de inflexible*. Esto significa que el contenido de *todo* debe estar claramente estructurado y organizado por tipo, de modo que GraphQL *entienda* a qué acceder y cómo hacerlo. Los campos de datos se definen en los esquemas de GraphQL, que definen la estructura de los objetos de contenido.

Los extremos de GraphQL proporcionan las rutas que responden a las consultas de GraphQL.

Todo esto significa que la aplicación puede seleccionar con precisión, fiabilidad y eficacia los datos que necesita, justo lo que necesita cuando se utiliza con AEM.

>[!NOTE]
>
>Consulte *GraphQL*.org y *GraphQL*.com.

## AEM y GraphQL {#aem-graphql}

GraphQL se utiliza en varias ubicaciones de AEM; por ejemplo:

* Comercio
   * Existen integraciones de GraphQL entre AEM y varias soluciones de comercio de terceros, que se utilizan con los enlaces de extensión proporcionados por los componentes principales del CIF.
* Fragmentos de contenido
   * Se ha desarrollado una API personalizada para este caso de uso.
   * Esta es la API de AEM GraphQL.

>[!NOTE]
>
>Este paso del Recorrido sin encabezado solo se refiere a la API de AEM GraphQL y a los fragmentos de contenido.

## API de AEM GraphQL {#aem-graphql-api}

La API de AEM GraphQL es una versión personalizada de la API estándar de GraphQL, especialmente configurada para permitirle realizar consultas (complejas) en los fragmentos de contenido.

Se utilizan fragmentos de contenido, ya que el contenido está estructurado según los modelos de fragmento de contenido. Esto cumple un requisito básico de GraphQL.

* Un modelo de fragmento de contenido está formado por uno o más campos.
   * Cada campo se define según un Tipo de datos.
* Los modelos de fragmento de contenido se utilizan para generar los esquemas AEM de GraphQL correspondientes.

Para acceder realmente a GraphQL para AEM (y el contenido) se utiliza un punto final para proporcionar la ruta de acceso.

El contenido devuelto, a través de la API de AEM GraphQL, puede ser utilizado por sus aplicaciones.

>[!NOTE]
>
>La implementación de la API de AEM GraphQL se basa en las bibliotecas Java de GraphQL.

### Casos de uso para entornos de autor y publicación {#use-cases-author-publish-environments}

Los casos de uso de la API de AEM GraphQL pueden depender del tipo de AEM como entorno de Cloud Service:

* Entorno de publicación; se usa para:
   * Datos de consulta para la aplicación JS (caso de uso estándar)

* Entorno de creación; se usa para:
   * Datos de consulta para &quot;fines de administración de contenido&quot;:
      * GraphQL en AEM as a Cloud Service es actualmente una API de solo lectura.
      * La API de REST se puede utilizar para operaciones CR(u)D.

## Fragmentos de contenido para usar con la API de AEM GraphQL {#content-fragments-use-with-aem-graphql-api}

Los fragmentos de contenido se pueden usar como base para GraphQL para AEM esquemas y consultas como:

* Permiten diseñar, crear, depurar y publicar contenido independiente de las páginas.
* Se basan en un modelo de fragmento de contenido, que predefine la estructura del fragmento resultante mediante tipos de datos definidos.
* Se pueden lograr capas de estructura adicionales con el tipo de datos Referencia de fragmento , disponible al definir un modelo.

### Modelos de fragmento de contenido {#content-fragments-models}

Estos modelos de fragmento de contenido:

* Se utilizan para generar los esquemas, una vez **Enabled**.

* Proporcione los tipos de datos y campos requeridos para GraphQL. Se aseguran de que la aplicación solo solicita lo que es posible y recibe lo que se espera.

* El tipo de datos **Referencias de fragmento** se puede usar en el modelo para hacer referencia a otro fragmento de contenido y, por lo tanto, introducir niveles adicionales de estructura.

### Referencias de fragmento {#fragment-references}

La **Referencia de fragmento**:

* Es de particular interés en conjunto con GraphQL.

* Es un tipo de datos específico que se puede utilizar al definir un modelo de fragmento de contenido.

* Hace referencia a otro fragmento, según un modelo de fragmento de contenido específico.

* Permite recuperar datos estructurados.

   * Cuando se define como una **fuente múltiple**, el fragmento principal puede hacer referencia (recuperar) a varios subfragmentos.

### Vista previa de JSON {#json-preview}

Para ayudar a diseñar y desarrollar los modelos de fragmento de contenido, puede obtener una vista previa del resultado de JSON en el Editor de fragmentos de contenido.

## Generación de esquemas de GraphQL a partir de fragmentos de contenido {#graphql-schema-generation-content-fragments}

GraphQL es una API con establecimiento inflexible de tipos, lo que significa que los datos deben estar claramente estructurados y organizados por tipo. La especificación de GraphQL proporciona una serie de directrices sobre cómo crear una API robusta para interrogar datos en una instancia determinada. Para ello, un cliente debe recuperar el Esquema , que contiene todos los tipos necesarios para una consulta.

Para los fragmentos de contenido, los esquemas (estructura y tipos) de GraphQL se basan en modelos de **Fragmento de contenido habilitado** y sus tipos de datos.

>[!CAUTION]
>
>Todos los esquemas de GraphQL (derivados de los modelos de fragmento de contenido que han sido **Enabled**) se pueden leer a través del extremo de GraphQL.
>
>Esto significa que debe asegurarse de que no hay datos confidenciales disponibles, ya que podrían filtrarse de esta manera; por ejemplo, esto incluye información que podría estar presente como nombres de campo en la definición del modelo.

Por ejemplo, si un usuario creó un Modelo de fragmento de contenido denominado `Article`, AEM genera el objeto `article` que es de un tipo `ArticleModel`. Los campos dentro de este tipo corresponden a los campos y tipos de datos definidos en el modelo.

1. Un modelo de fragmento de contenido:

   ![Modelo de fragmento de contenido para usar con el Modelo de fragmento de ](assets/graphqlapi-cfmodel.png "GraphQLContent para usar con GraphQL")

1. El esquema correspondiente de GraphQL (salida de la documentación automática de GraphiQL):
   ![Esquema GraphQL basado en el ](assets/graphqlapi-cfm-schema.png "modelo de fragmento de contenidoEsquema de GraphQL basado en el modelo de fragmento de contenido")

   Esto muestra que el tipo generado `ArticleModel` contiene varios [campos](#fields).

   * Tres de ellos han sido controlados por el usuario: `author`, `main` y `referencearticle`.

   * Los demás campos los agregó automáticamente AEM y representan métodos útiles para proporcionar información sobre un determinado fragmento de contenido; en este ejemplo, `_path`, `_metadata`, `_variations`. Estos [campos de ayuda](#helper-fields) están marcados con un `_` anterior para distinguir entre lo que ha definido el usuario y lo que se ha generado automáticamente.

1. Después de que un usuario crea un fragmento de contenido basado en el modelo de artículo, se puede interrogar a través de GraphQL. Para ver ejemplos, consulte Sample Queries.md#graphql-sample-queries) (basado en una estructura de fragmento de contenido de ejemplo para usar con GraphQL.

En GraphQL para AEM, el esquema es flexible. Esto significa que se genera automáticamente cada vez que se crea, actualiza o elimina un modelo de fragmento de contenido. Las cachés del esquema de datos también se actualizan al actualizar el modelo de fragmento de contenido.

El servicio Sites GraphQL escucha (en segundo plano) cualquier modificación realizada en un modelo de fragmento de contenido. Cuando se detectan actualizaciones, solo se regenera esa parte del esquema. Esta optimización ahorra tiempo y proporciona estabilidad.

Por ejemplo, si:

1. Instale un paquete que contenga `Content-Fragment-Model-1` y `Content-Fragment-Model-2`:

   1. Se generarán los tipos de GraphQL para `Model-1` y `Model-2`.

1. A continuación, modifique `Content-Fragment-Model-2`:

   1. Solo se actualizará el tipo `Model-2` GraphQL.

   1. Mientras que `Model-1` permanecerá igual.

>[!NOTE]
>
>Esto es importante tener en cuenta en caso de que desee realizar actualizaciones masivas en los modelos de fragmento de contenido a través de la api de REST o de otro modo.

El esquema se sirve a través del mismo extremo que las consultas de GraphQL, con el cliente manejando el hecho de que se llama al esquema con la extensión `GQLschema`. Por ejemplo, si se realiza una solicitud `GET` simple en `/content/cq:graphql/global/endpoint.GQLschema`, el resultado del esquema será el tipo Content: `text/x-graphql-schema;charset=iso-8859-1`.

### Generación de esquemas: modelos no publicados {#schema-generation-unpublished-models}

Cuando los fragmentos de contenido están anidados, puede ocurrir que se publique un modelo de fragmento de contenido principal, pero no un modelo al que se hace referencia.

>[!NOTE]
>
>La interfaz de usuario de AEM evita que esto ocurra, pero si la publicación se realiza mediante programación o con paquetes de contenido, puede ocurrir.

Cuando esto sucede, AEM genera un esquema *incompleto* para el modelo de fragmento de contenido principal. Esto significa que la referencia de fragmento, que depende del modelo no publicado, se elimina del esquema.

## Puntos finales de AEM GraphQL {#aem-graphql-endpoints}

<!--
need details/examples
-->

Un punto final es la ruta utilizada para acceder a GraphQL para AEM. Al utilizar esta ruta, usted (o su aplicación) pueden:

* acceda a los esquemas de GraphQL,
* envíe sus consultas de GraphQL,
* reciba las respuestas (a sus consultas de GraphQL).

AEM permite:

* Un punto final global - disponible para su uso en todos los sitios.
* Puntos finales del inquilino : que puede configurar, específicos de un sitio o proyecto especificado.

## Permisos    {#permissions}

Los permisos son los necesarios para acceder a Assets.

## Interfaz de GraphiQL de AEM {#aem-graphiql-interface}

Para ayudarle a introducir y probar consultas directamente, una implementación de la interfaz estándar de GraphiQL está disponible para su uso con AEM GraphQL. Esto se puede instalar con AEM.

Proporciona funciones como resaltado de sintaxis, autocompletado, autosugerencia, junto con un historial y documentación en línea.

![Interfaz ](assets/graphiql-interface.png "GraphiQL de GraphiQL")

<!--
new page?
-->

## Uso de la API de AEM GraphQL {#using-aem-graphiql}

### Puntos de conexión {#endpoints}

La ruta del repositorio de GraphQL para AEM punto final global es:

`/content/cq:graphql/global/endpoint`

Para el cual su aplicación puede utilizar la siguiente ruta en la dirección URL de la solicitud:

`/content/_cq_graphql/global/endpoint.json`

Para un extremo de inquilino, las rutas son comparables:

`/content/cq:graphql/your-tenant/endpoint`
`/content/_cq_graphql/your-tenant/endpoint.json`

Antes de usar, todos los extremos deben estar habilitados. Para habilitar un punto final, global o inquilino, para GraphQL para AEM necesita:

* Habilitar el extremo de GraphQL
* Publicación del extremo

>[!CAUTION]
>
>El editor de fragmentos de contenido puede permitir que un fragmento de contenido de un inquilino haga referencia a un fragmento de contenido de otro inquilino (a través de políticas).
>
>En tal caso, no todo el contenido se podrá recuperar mediante un punto final específico del inquilino.
>
>El autor del contenido debe controlar este escenario; por ejemplo, puede resultar útil considerar la posibilidad de colocar los modelos de fragmento de contenido compartido en el inquilino global.

### Activación del extremo {#enabling-graphql-endpoint} de GraphQL

Para habilitar un extremo de GraphQL, primero debe tener una configuración adecuada en el navegador de configuración.

>[!CAUTION]
>
>Si no se ha habilitado el uso de modelos de fragmento de contenido, la opción **Create** no estará disponible.

Para habilitar el punto final correspondiente:

1. Vaya a **Tools**, **Sites** y, a continuación, seleccione **GraphQL**.
1. Seleccione **Crear**.
1. Se abrirá el cuadro de diálogo **Crear nuevo extremo de GraphQL**. Aquí puede especificar:
   * **Nombre**: nombre del extremo; puede escribir cualquier texto.
   * **Utilice el esquema GraphQL proporcionado por**: utilice la lista desplegable para seleccionar el sitio o proyecto requerido.

   >[!NOTE]
   >
   >La siguiente advertencia se muestra en el cuadro de diálogo:
   >
   >* *Los extremos de GraphQL pueden introducir problemas de rendimiento y seguridad de datos si no se administran con cuidado. Asegúrese de definir los permisos adecuados después de crear un extremo.*


1. Confirme con **Crear**.
1. El cuadro de diálogo **Próximos pasos** proporciona un vínculo directo a la consola de seguridad para que pueda asegurarse de que el punto final recién creado tenga los permisos adecuados.

   >[!CAUTION]
   >
   >El punto final es accesible para todos. Esto puede suponer un problema de seguridad, especialmente en las instancias de publicación, ya que las consultas de GraphQL pueden imponer una carga pesada en el servidor.
   >
   >Puede configurar ACL, según su caso de uso, en el punto final.

### Publicación del extremo {#publishing-graphql-endpoint} de GraphQL

Seleccione el nuevo extremo y **Publish** para que esté disponible en todos los entornos.

>[!CAUTION]
>
>El punto final es accesible para todos.
>
>En instancias de publicación esto puede suponer un problema de seguridad, ya que las consultas de GraphQL pueden imponer una carga pesada en el servidor.
>
>Debe configurar las ACL adecuadas para su caso de uso en el punto final.

### Instalación de la interfaz de AEM GraphiQL {#installing-graphiql-interface}

La interfaz de usuario de GraphiQL se puede instalar en AEM con un paquete dedicado: el paquete [GraphiQL Content Package v0.0.6 (2021.3)](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html?package=/content/software-distribution/en/details.html/content/dam/aemcloud/public/aem-graphql/graphiql-0.0.6.zip).

### Esquemas de AEM GraphQL {#aem-graphql-schemas}

Para acceder a los datos, primero debe seleccionar el tipo de modelo de fragmento de contenido requerido, representado por un esquema de GraphQL. AEM esquemas de GraphQL se derivan de los modelos de fragmento de contenido para su uso en consultas de GraphQL.

<!--
Confirm is the schema city or CityModel? -->

Si tiene un modelo de fragmento de contenido llamado `City`, habrá un esquema correspondiente llamado `city`. Puede utilizar la siguiente consulta para enumerar el `name` de todos los fragmentos de contenido basados en este modelo.

```xml
query {
  cityList {
    items {
      name
    }
  }
}
```

Puede utilizar la siguiente consulta para enumerar los `name` y `description` de todos los `types` para todos los esquemas disponibles:

```xml
{
  __schema {
    types {
      name
      description
    }
  }
}
```

### AEM campos de GraphQL {#aem-graphql-fields}

Una vez que haya seleccionado el esquema que necesita, debe acceder a datos específicos, representados por campos en el esquema.

Dentro del esquema hay campos individuales, de dos categorías básicas:

* Campos que se generan.

   Se utiliza una selección de [Tipos de campo](#field-types) para crear campos en función de cómo configure el modelo de fragmento de contenido. Los nombres de los campos se toman del campo **Property Name** del **Data Type**.

   * También está la propiedad **Render As** que se debe tener en cuenta, ya que los usuarios pueden configurar ciertos tipos de datos; por ejemplo, como texto de una sola línea o como campo múltiple.

* GraphQL para AEM también genera varios campos de ayuda.

   Se utilizan para identificar un fragmento de contenido o para obtener más información sobre un fragmento de contenido.

### Tipos de campo {#field-types}

GraphQL para AEM admite una lista de tipos. Se representan todos los tipos de datos del modelo de fragmento de contenido compatibles y los tipos de GraphQL correspondientes:

| Modelo de fragmento de contenido: tipo de datos | Tipo de GraphQL | Descripción |
|--- |--- |--- |
| Texto de una sola línea | Cadena, [Cadena] | Se utiliza para cadenas simples como nombres de autor, nombres de ubicación, etc. |
| Texto de varias líneas | Cadena | Se utiliza para generar texto como el cuerpo de un artículo |
| Número | Flotante, [Flotante] | Se utiliza para mostrar números de coma flotante y números regulares |
| Booleano | Booleano | Se utiliza para mostrar casillas de verificación → instrucciones simples true/false |
| Fecha Y Hora | Calendario | Se utiliza para mostrar la fecha y la hora en formato ISO 8086. Según el tipo seleccionado, hay tres sabores disponibles para usar en AEM GraphQL: `onlyDate`, `onlyTime`, `dateTime` |
| Enumeración | Cadena | Se utiliza para mostrar una opción de una lista de opciones definidas en la creación del modelo. |
| Etiquetas | [Cadena] | Se utiliza para mostrar una lista de cadenas que representan las etiquetas utilizadas en AEM |
| Referencia de contenido | Cadena | Se utiliza para mostrar la ruta hacia otro recurso en AEM |
| Referencia al fragmento | *Un tipo de modelo* | Se utiliza para hacer referencia a otro fragmento de contenido de un tipo de modelo determinado, definido cuando se creó el modelo |

### Campos de ayuda {#helper-fields}

Además de los tipos de datos de los campos generados por el usuario, GraphQL para AEM también genera varios campos *helper* para ayudar a identificar un fragmento de contenido o para proporcionar información adicional sobre un fragmento de contenido.

#### Ruta {#path}

El campo de ruta se utiliza como identificador en GraphQL. Representa la ruta del recurso de fragmento de contenido dentro del repositorio de AEM. Se ha elegido como identificador de un fragmento de contenido, ya que:

* es único dentro de AEM,
* se pueden recuperar fácilmente.

El siguiente código muestra las rutas de todos los fragmentos de contenido que se crearon en función del modelo de fragmento de contenido `Person`.

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

>[!NOTE]
>
>Consulte Consulta De Muestra: Un Solo Fragmento De Ciudad Específico.

#### Metadatos {#metadata}

A través de GraphQL, AEM también expone los metadatos de un fragmento de contenido. Los metadatos son la información que describe un fragmento de contenido, como el título de un fragmento de contenido, la ruta de vista en miniatura, la descripción de un fragmento de contenido, la fecha en que se creó, entre otros.

Como los metadatos se generan mediante el Editor de esquemas y, como no tienen una estructura específica, el tipo `TypedMetaData` GraphQL se implementó para exponer los metadatos de un fragmento de contenido. `TypedMetaData` expone la información agrupada por los siguientes tipos escalares:

| Campo |
|--- |
| `stringMetadata:[StringMetadata]!` |
| `stringArrayMetadata:[StringArrayMetadata]!` |
| `intMetadata:[IntMetadata]!` |
| `intArrayMetadata:[IntArrayMetadata]!` |
| `floatMetadata:[FloatMetadata]!` |
| `floatArrayMetadata:[FloatArrayMetadata]!` |
| `booleanMetadata:[BooleanMetadata]!` |
| `booleanArrayMetadata:[booleanArrayMetadata]!` |
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
>Tenga en cuenta que tanto `StringMetadata` como `StringArrayMetadata` hacen referencia a lo que se almacena en el repositorio, no a cómo se recuperan.
>
>Por ejemplo, si llama al campo `stringMetadata`, recibirá una matriz de todos los metadatos almacenados en el repositorio como `String` y, si llama a `stringArrayMetadata`, recibirá una matriz de todos los metadatos almacenados en el repositorio como `String[]`.

>[!NOTE]
>
>Consulte Consulta de muestra para metadatos: enumere los metadatos para los premios titulados GB.

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

>[!NOTE]
>
>Consulte Consulta de ejemplo: todas las ciudades con una variación con nombre.

### Variables AEM GraphQL {#aem-graphql-variables}

Las variables son útiles en cualquier forma de programación o consulta, ya que permiten almacenar valores diferentes en una ubicación. Para AEM GraphQL esto significa que en lugar de tener que escribir una consulta separada para cada valor, puede escribir la consulta para una variable y el valor de esta variable puede cambiar según sea necesario.

GraphQL permite colocar variables en la consulta.

>[!NOTE]
>
>Para obtener más información, consulte la documentación de GraphQL para las variables.

Por ejemplo, para obtener todos los fragmentos de contenido de tipo `Article` que tengan una variación específica, puede especificar la variable `variation` en GraphiQL. Todas las instancias se recuperarán en `GetArticlesByVariation` y luego se pasarán para su uso en `articleList`.

![Variables ](assets/graphqlapi-variables.png "GraphQL")

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

### Directivas de AEM GraphQL {#aem-graphql-directives}

En GraphQL existe la posibilidad de cambiar la consulta en función de variables, denominadas Directivas de GraphQL.

Por ejemplo, puede incluir el campo `adventurePrice` en una consulta para todos los `AdventureModels`, en función de una variable `includePrice`.

!![GraphQL Directives](assets/graphqlapi-Directivas.png &quot;Directivas de GraphQL&quot;)

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

### Filtros AEM GraphQL {#aem-graphql-filters}

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

* detalles de GraphQL para extensiones de AEM

* Ejemplos de consultas que utilizan este contenido y estructura de ejemplo

### Extensiones de AEM GraphQL {#aem-graphql-extensions}

El funcionamiento básico de las consultas con GraphQL para AEM se adhiera a la especificación estándar de GraphQL. Para las consultas de GraphQL con AEM hay algunas extensiones:

* Si necesita un solo resultado:
   * utilizar el nombre del modelo; ciudad del ejemplo

* Si espera una lista de resultados:
   * añada `List` al nombre del modelo; por ejemplo, `cityList`
   * Consulte [Consulta de muestra: toda la información sobre todas las ciudades](#sample-all-information-all-cities)

* Si desea utilizar un OR lógico:
   * use ` _logOp: OR`
   * Consulte [Consulta de muestra: todas las personas que tienen el nombre &quot;Trabajos&quot; o &quot;Smith&quot;](#sample-all-persons-jobs-smith)

* AND lógico también existe, pero (a menudo) está implícito

* Puede consultar los nombres de campo que se correspondan con los campos del modelo de fragmento de contenido
   * Consulte [Consulta de muestra: detalles completos del CEO y los empleados de una empresa](#sample-full-details-company-ceos-employees)

* Además de los campos del modelo, hay algunos campos generados por el sistema (precedidos de guiones bajos):

   * Para el contenido:

      * `_locale` : revelar el idioma; basado en el Administrador de idiomas
         * Consulte [Consulta de ejemplo para varios fragmentos de contenido de una configuración regional determinada](#sample-wknd-multiple-fragments-given-locale)
      * `_metadata` : para mostrar metadatos del fragmento
         * Consulte [Consulta de muestra para metadatos: enumere los metadatos de los premios titulados GB](#sample-metadata-awards-gb)
      * `_model` : permitir la consulta de un modelo de fragmento de contenido (ruta y título)
         * Consulte [Consulta de ejemplo para un modelo de fragmento de contenido de un modelo](#sample-wknd-content-fragment-model-from-model)
      * `_path` : la ruta al fragmento de contenido dentro del repositorio
         * Consulte [Consulta de muestra: un solo fragmento de ciudad específico](#sample-single-specific-city-fragment)
      * `_reference` : para revelar referencias; incluir referencias en línea en el Editor de texto enriquecido
         * Consulte [Consulta de ejemplo para varios fragmentos de contenido con referencias de recuperación previa](#sample-wknd-multiple-fragments-prefetched-references)
      * `_variation` : para mostrar variaciones específicas dentro del fragmento de contenido
         * Consulte [Consulta de muestra: todas las ciudades con una variación con nombre](#sample-cities-named-variation)
   * Y operaciones:

      * `_operator` : aplicar operadores específicos;  `EQUALS`,  `EQUALS_NOT`,  `GREATER_EQUAL`,  `LOWER`,  `CONTAINS`,  `STARTS_WITH`
         * Consulte [Consulta de muestra: todas las personas que no tienen un nombre de &quot;Trabajos&quot;](#sample-all-persons-not-jobs)
         * Consulte [Consulta de muestra: todas las aventuras en las que el `_path` comienza con un prefijo específico](#sample-wknd-all-adventures-cycling-path-filter)
      * `_apply` : aplicar condiciones específicas; por ejemplo,   `AT_LEAST_ONCE`
         * Consulte [Muestra de consulta - Filtrar en una matriz con un elemento que debe producirse al menos una vez](#sample-array-item-occur-at-least-once)
      * `_ignoreCase` : para ignorar el caso al consultar
         * Consulte [Consulta de muestra: todas las ciudades con SAN en el nombre, independientemente del caso](#sample-all-cities-san-ignore-case)









* Se admiten los tipos de unión de GraphQL:

   * use `... on`
      * Consulte [Consulta de ejemplo para un fragmento de contenido de un modelo específico con una referencia de contenido](#sample-wknd-fragment-specific-model-content-reference)

### Consultas persistentes (almacenamiento en caché) {#persisted-queries-caching}

Después de preparar una consulta con una solicitud de POST, esta se puede ejecutar con una solicitud de GET que se puede almacenar en caché mediante cachés HTTP o una CDN.

Esto es necesario, ya que las consultas de POST generalmente no se almacenan en caché y si se utiliza la GET con la consulta como parámetro, existe un riesgo significativo de que el parámetro sea demasiado grande para los servicios HTTP e intermediarios.

Las consultas persistentes siempre deben utilizar el punto final relacionado con la configuración (inquilino) apropiada; para que puedan usar una o ambas:

* La configuración global y el punto final
La consulta tiene acceso a todos los modelos de fragmento de contenido.
* Configuraciones específicas del inquilino y puntos de conexión
La creación de una consulta persistente para una configuración de inquilino específica requiere un extremo específico del inquilino correspondiente (para proporcionar acceso a los modelos de fragmento de contenido relacionados).
Por ejemplo, para crear una consulta persistente específica para el inquilino WKND, se debe crear de antemano una configuración de inquilino específica de WKND y un extremo específico de WKND.

>[!NOTE]
>
>Consulte Habilitar la funcionalidad de fragmento de contenido en el navegador de configuración para obtener más información.
>
>Las **Consultas de persistencia de GraphQL** deben habilitarse para la configuración apropiada del inquilino.

Por ejemplo, si hay una consulta en particular llamada `my-query`, que utiliza un modelo `my-model` de la configuración del inquilino `my-conf`:

* Puede crear una consulta utilizando el extremo específico `my-conf` y luego la consulta se guardará de la siguiente manera:
   `/conf/my-conf/settings/graphql/persistentQueries/my-query`
* Puede crear la misma consulta utilizando el extremo `global` , pero la consulta se guardará de la siguiente manera:
   `/conf/global/settings/graphql/persistentQueries/my-query`

>[!NOTE]
>
>Estas son dos consultas diferentes: se guardan en rutas diferentes.
>
>Simplemente utilizan el mismo modelo, pero a través de puntos de conexión diferentes.

Estos son los pasos necesarios para mantener una consulta determinada:

1. Prepare la consulta colocándola en la nueva dirección URL de extremo `/graphql/persist.json/<config>/<persisted-label>`.

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

   Por ejemplo, compruebe si se ha realizado correctamente:

   ```xml
   {
     "action": "create",
     "configurationName": "wknd",
     "name": "plain-article-query",
     "shortPath": "/wknd/plain-article-query",
     "path": "/conf/wknd/settings/graphql/persistentQueries/plain-article-query"
   }
   ```

1. A continuación, puede reproducir la consulta persistente obteniendo la dirección URL `/graphql/execute.json/<shortPath>`.

   Por ejemplo, utilice la consulta persistente:

   ```xml
   $ curl -X GET \
       http://localhost:4502/graphql/execute.json/wknd/plain-article-query
   ```

1. Actualice una consulta persistente mediante POST a una ruta de consulta ya existente.

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

1. Cree una consulta sencilla envolvente con control de caché.

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

1. Para ejecutar la consulta en la publicación, es necesario replicar el árbol persistente relacionado

   * Uso de un POST para la replicación:

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
      1. Repita el paquete.
   * Uso de la herramienta de replicación/distribución.
      1. Vaya a la herramienta Distribución.
      1. Seleccione la activación del árbol para la configuración (por ejemplo, `/conf/wknd/settings/graphql/persistentQueries`).
   * Uso de un flujo de trabajo (mediante la configuración del iniciador del flujo de trabajo):
      1. Defina una regla de lanzador de flujo de trabajo para ejecutar un modelo de flujo de trabajo que duplique la configuración en diferentes eventos (por ejemplo, crear, modificar, entre otros).



1. Una vez que la configuración de la consulta está en la publicación, se aplican los mismos principios, solo con el extremo de publicación.

   >[!NOTE]
   >
   >Para el acceso anónimo, el sistema supone que la ACL permite que &quot;todos&quot; tengan acceso a la configuración de la consulta.
   >
   >Si no es así, no podrá ejecutarse.

   >[!NOTE]
   >
   >Debe codificarse cualquier punto y coma (&quot;;&quot;) en las direcciones URL.
   >
   >Por ejemplo, como en la solicitud para ejecutar una consulta persistente:
   >
   >
   ```xml
   >curl -X GET \ "http://localhost:4502/graphql/execute.json/wknd/plain-article-query-parameters%3bapath=%2fcontent2fdam2fwknd2fen2fmagazine2falaska-adventure2falaskan-adventures;withReference=false"
   >```

### Consulta del extremo de GraphQL desde un sitio web externo {#query-graphql-endpoint-from-external-website}

Para acceder al extremo de GraphQL desde un sitio web externo, debe configurar:

* Filtro CORS
* Filtro de referente

#### Filtro CORS {#cors-filter}

>[!NOTE]
>
>Para obtener una descripción detallada de la política de uso compartido de recursos CORS en AEM, consulte Comprender el uso compartido de recursos de origen cruzado (CORS).

Para acceder al extremo de GraphQL, se debe configurar una directiva CORS en el repositorio Git del cliente. Para ello, agregue un archivo de configuración OSGi CORS apropiado para los puntos de conexión deseados.

Esta configuración debe especificar un origen de sitio web de confianza `alloworigin` o `alloworiginregexp` para el que se debe conceder acceso.

Por ejemplo, para conceder acceso al extremo de GraphQL y al extremo de consultas persistentes para `https://my.domain` puede utilizar:

```xml
{
  "supportscredentials":true,
  "supportedmethods":[
    "GET",
    "HEAD",
    "POST"
  ],
  "exposedheaders":[
    ""
  ],
  "alloworigin":[
    "https://my.domain"
  ],
  "maxage:Integer":1800,
  "alloworiginregexp":[
    ""
  ],
  "supportedheaders":[
    "Origin",
    "Accept",
    "X-Requested-With",
    "Content-Type",
    "Access-Control-Request-Method",
    "Access-Control-Request-Headers"
  ],
  "allowedpaths":[
    "/content/_cq_graphql/global/endpoint.json",
    "/graphql/execute.json/.*"
  ]
}
```

Si ha configurado una ruta mnemónica para el extremo, también puede utilizarla en `allowedpaths`.

#### Filtro de referente {#referrer-filter}

Además de la configuración de CORS, se debe configurar un filtro de referente para permitir el acceso desde hosts de terceros.

Para ello, agregue un archivo de configuración de OSGi Referrer Filter apropiado que:

* especifica un nombre de host de sitio web de confianza; `allow.hosts` o `allow.hosts.regexp`,
* concede acceso a este nombre de host.

Por ejemplo, para conceder acceso a solicitudes con el referente `my.domain` puede:

```xml
{
    "allow.empty":false,
    "allow.hosts":[
      "my.domain"
    ],
    "allow.hosts.regexp":[
      ""
    ],
    "filter.methods":[
      "POST",
      "PUT",
      "DELETE",
      "COPY",
      "MOVE"
    ],
    "exclude.agents.regexp":[
      ""
    ]
}
```

>[!CAUTION]
>
>Sigue siendo responsabilidad del cliente:
>
>* solo conceder acceso a dominios de confianza
>* asegúrese de que no se expone ninguna información confidencial
>* no utilice una sintaxis comodín [*]; esto deshabilitará el acceso autenticado al extremo de GraphQL y también lo expondrá a todo el mundo.


>[!CAUTION]
>
>Todos los esquemas de GraphQL (derivados de los modelos de fragmento de contenido que han sido **Enabled**) se pueden leer a través del extremo de GraphQL.
>
>Esto significa que debe asegurarse de que no hay datos confidenciales disponibles, ya que podrían filtrarse de esta manera; por ejemplo, esto incluye información que podría estar presente como nombres de campo en la definición del modelo.

### Autenticación AEM GraphQL {#aem-graphql-authentication}

Un caso de uso principal de la API de Adobe Experience Manager as a Cloud Service (AEM) GraphQL para la entrega de fragmentos de contenido es aceptar consultas remotas desde aplicaciones o servicios de terceros. Estas consultas remotas pueden requerir acceso a API autenticado para asegurar la entrega de contenido sin encabezado.

>[!NOTE]
>
>Para pruebas y desarrollo también puede acceder a la API de AEM GraphQL directamente mediante la interfaz de GraphiQL.

Para la autenticación, el servicio de terceros debe utilizar un token de acceso que luego se pueda utilizar en la solicitud de GraphQL.

#### Recuperación de un token de acceso {#retrieving-access-token}

Consulte Generación de tokens de acceso para API del servidor para obtener más información.

#### Uso del token de acceso en una solicitud de GraphQL {#use-access-token-in-graphql-request}

Para que un servicio de terceros se conecte con una instancia de AEM, debe tener un *Token de acceso*. El servicio debe agregar este token al encabezado `Authorization` en la solicitud del POST.

Por ejemplo, un encabezado de autorización de GraphQL:

```xml
Authorization: Bearer <access_token>
```

#### Requisitos de permisos {#permission-requirements}

Todas las solicitudes realizadas con el token de acceso se realizarán *mediante la cuenta de usuario que generó el token*.

Esto significa que debe comprobar que la cuenta tiene los permisos necesarios para ejecutar consultas de GraphQL.

Puede comprobarlo utilizando GraphiQL en la instancia local.

## Ejemplos de consultas de AEM GraphQL {#samples-aem-graphql-queries}

Consulte Aprendizaje para utilizar GraphQL con AEM: contenido de muestra y consultas para obtener una amplia gama de consultas de ejemplo.

<!--
## Code Samples for AEM GraphQL Queries {#code-samples-aem-graphql-queries}
-->

## Siguientes {#whats-next}

Ahora que ha aprendido a acceder y consultar el contenido sin encabezado mediante la API de AEM GraphQL, ahora puede [aprender a utilizar la API de REST para acceder y actualizar el contenido de sus fragmentos de contenido](/help/implementing/developing/headless-journey/update-your-content.md).

## Recursos adicionales {#additional-resources}

* [GraphQL.org](https://graphql.org)
   * [Esquemas](https://graphql.org/learn/schema/)
   * [Variables](https://graphql.org/learn/queries/#variables)
   * [Bibliotecas Java de GraphQL](https://graphql.org/code/#java)
* [GraphiQL](https://graphql.org/learn/serving-over-http/#graphiql)
* [La estructura de fragmento de contenido de ejemplo](/help/assets/content-fragments/content-fragments-graphql-samples.md#content-fragment-structure-graphql)
* [Aprender a utilizar GraphQL con AEM: contenido de muestra y consultas](/help/assets/content-fragments/content-fragments-graphql-samples.md)
   * [Consulta De Muestra: Un Solo Fragmento De Ciudad Específico](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-single-specific-city-fragment)
   * [Consulta de ejemplo para metadatos: enumera los metadatos de los premios titulados GB](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-metadata-awards-gb)
   * [Consulta de ejemplo: todas las ciudades con una variación con nombre](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-cities-named-variation)
* [Habilitar la funcionalidad de fragmento de contenido en el navegador de configuración](/help/assets/content-fragments/content-fragments-configuration-browser.md#enable-content-fragment-functionality-in-configuration-browser)
* [Trabajar con fragmentos de contenido](/help/assets/content-fragments/content-fragments.md)
   * [Modelos de fragmento de contenido](/help/assets/content-fragments/content-fragments-models.md)
   * [Salida JSON](/help/assets/content-fragments/content-fragments-json-preview.md)
* [Comprender el uso compartido de recursos de origen cruzado (CORS)](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/security/understand-cross-origin-resource-sharing.html?lang=en#understand-cross-origin-resource-sharing-(cors))
* [Generación de tokens de acceso para las API del servidor](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md)
* [Introducción a AEM sin encabezado](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/overview.html) : una breve serie de tutoriales de vídeo que ofrecen información general sobre el uso de AEM funciones sin encabezado, incluidos el modelado de datos y GraphQL.
