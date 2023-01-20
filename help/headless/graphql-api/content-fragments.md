---
title: API de GraphQL de AEM para su uso con fragmentos de contenido
description: Aprenda a utilizar los fragmentos de contenido en Adobe Experience Manager (AEM) as a Cloud Service con la API de GraphQL de AEM para la entrega de contenido sin encabezado.
feature: Content Fragments,GraphQL API
exl-id: bdd60e7b-4ab9-4aa5-add9-01c1847f37f6
source-git-commit: 20e54ff697c0dc7ab9faa504d9f9e0e6ee585464
workflow-type: tm+mt
source-wordcount: '4174'
ht-degree: 59%

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

AEM proporciona funciones para convertir consultas (de ambos tipos) a [Consultas persistentes, que se pueden almacenar en caché](/help/headless/graphql-api/persisted-queries.md) por Dispatcher y la CDN.

### Prácticas recomendadas para consultas de GraphQL (Dispatcher y CDN) {#graphql-query-best-practices}

La variable [Consultas persistentes](/help/headless/graphql-api/persisted-queries.md) son el método recomendado para usar en instancias de publicación como:

* Se almacenan en caché.
* Se administran centralmente mediante AEM as a Cloud Service.

>[!NOTE]
>
>Normalmente no hay ningún Dispatcher/CDN en el autor, por lo que no hay ganancia en el uso de consultas persistentes allí; aparte de probarlas.

No se recomiendan las consultas de GraphQL que utilizan solicitudes de POST, ya que no se almacenan en caché, por lo que en una instancia predeterminada, Dispatcher está configurado para bloquear dichas consultas.

Aunque GraphQL también admite solicitudes de GET, estas pueden alcanzar límites (por ejemplo, la longitud de la dirección URL) que se pueden evitar mediante consultas persistentes.

>[!NOTE]
>
>Para permitir consultas directas o POST en Dispatcher, puede pedir al administrador del sistema que realice lo siguiente:
>
>* Cree un [Variable de entorno de Cloud Manager](/help/implementing/cloud-manager/environment-variables.md) llamado `ENABLE_GRAPHQL_ENDPOINT`
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

Las consultas de GraphQL se ejecutan con el permiso del usuario AEM de la solicitud subyacente. Si el usuario no tiene acceso de lectura a algunos fragmentos (almacenados como activos), no pasará a formar parte del conjunto de resultados.

Además, el usuario debe tener acceso a un extremo de GraphQL para poder ejecutar consultas de GraphQL.

## Generación de esquemas {#schema-generation}

GraphQL es una API muy tipificada, lo que significa que los datos deben estar claramente estructurados y organizados por tipo.

La especificación de GraphQL proporciona una serie de directrices sobre cómo crear una API robusta para buscar datos en una instancia determinada. Para ello, un cliente debe recuperar el [Esquema](#schema-generation), que contiene todos los tipos necesarios para una consulta.

Para los fragmentos de contenido, los esquemas (estructura y tipos) de GraphQL se basan en [Modelos de fragmentos de contenido](/help/sites-cloud/administering/content-fragments/content-fragments-models.md) **habilitados** y sus tipos de datos.

>[!CAUTION]
>
>Todos los esquemas de GraphQL (derivados de los modelos de fragmentos de contenido que se han **habilitado**) se pueden leer a través del punto de conexión de GraphQL.
>
>Esto significa que debe asegurarse de que no hay datos confidenciales disponibles, ya que podrían filtrarse de esta manera; por ejemplo, esto incluye información que podría estar presente como nombres de campo en la definición del modelo.

Por ejemplo, si un usuario crea un modelo de fragmento de contenido denominado `Article`, luego AEM genera un tipo de GraphQL `ArticleModel`. Los campos dentro de este tipo corresponden a los campos y tipos de datos definidos en el modelo. Además, crea algunos puntos de entrada para las consultas que funcionan en este tipo, como `articleByPath` o `articleList`.

1. Un modelo de fragmento de contenido:

   ![Modelo de fragmento de contenido para usar con GraphQL](assets/cfm-graphqlapi-01.png "Modelo de fragmento de contenido para usar con GraphQL")

1. El esquema correspondiente de GraphQL (salida de la documentación automática de GraphiQL):
   ![Esquema de GraphQL basado en el modelo de fragmento de contenido](assets/cfm-graphqlapi-02.png "Esquema de GraphQL basado en el modelo de fragmento de contenido")

   Esto muestra que el tipo generado `ArticleModel` contiene varios [campos](#fields).

   * Tres de ellos han sido controlados por el usuario: `author`, `main` y `referencearticle`.

   * Los demás campos los agregó automáticamente AEM y representan métodos útiles para proporcionar información sobre un determinado fragmento de contenido; en este ejemplo, (la variable [campos de ayuda](#helper-fields)) `_path`, `_metadata`, `_variations`.

1. Después de que un usuario cree un fragmento de contenido basado en el modelo de artículo, se puede buscar a través de GraphQL. Para ver ejemplos, consulte las [Consultas de muestra](/help/headless/graphql-api/sample-queries.md#graphql-sample-queries) (basadas en una [estructura de fragmentos de contenido de muestra para usar con GraphQL](/help/headless/graphql-api/sample-queries.md#content-fragment-structure-graphql)).

En GraphQL para AEM, el esquema es flexible. Esto significa que se genera automáticamente cada vez que se crea, actualiza o elimina un modelo de fragmento de contenido. Las cachés del esquema de datos también se refrescan al actualizar el modelo de fragmento de contenido.

<!-- move the following to a separate "in depth" page -->

Las cachés del esquema de datos también se refrescan al actualizar el modelo de fragmento de contenido.

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

<!-- move through to here to a separate "in depth" page -->

### Generación de esquemas: modelos no publicados {#schema-generation-unpublished-models}

Cuando los fragmentos de contenido están anidados, puede ocurrir que se publique un modelo de fragmento de contenido principal, pero no un modelo al que se hace referencia.

>[!NOTE]
>
>La IU de AEM evita que esto ocurra, pero si la publicación se realiza mediante programación o con paquetes de contenido, puede ocurrir.

Cuando esto sucede, AEM genera un esquema *incompleto* del modelo de fragmento del contenido principal. Esto significa que la referencia de fragmento, que depende del modelo no publicado, se elimina del esquema.

## Campos {#fields}

Dentro del esquema hay campos individuales, de dos categorías básicas:

* Campos que genera usted.

   Una selección de [Tipos de datos](#Data-types) se utilizan para crear campos en función de cómo configure el modelo de fragmento de contenido. Los nombres de campo se toman de la variable **Nombre de propiedad** del campo **Tipo de datos** pestaña .

   * También hay **Representar como** , ya que los usuarios pueden configurar ciertos tipos de datos. Por ejemplo, se puede configurar un campo de texto de una sola línea para que contenga varios textos de una sola línea eligiendo `multifield` en la lista desplegable .

* GraphQL para AEM también genera una serie de [campos de ayuda](#helper-fields).

### Tipos de datos {#data-types}

GraphQL para AEM admite una lista de tipos. Se representan todos los tipos de datos del modelo de fragmento de contenido compatibles y los tipos de GraphQL correspondientes:

| Modelo de fragmento de contenido: tipo de datos | Tipo de GraphQL | Descripción |
|--- |--- |--- |
| Texto de línea única | Cadena, [Cadena] |  Se utiliza para cadenas simples como nombres de autor, nombres de ubicación, etc. |
| Texto multilínea | Cadena, [Cadena] |  Se utiliza para generar texto como el cuerpo de un artículo |
| Número |  Flotante, [Flotante] | Se utiliza para mostrar números de coma flotante y números regulares |
| Booleano |  Booleano |  Se utiliza para mostrar casillas de verificación → instrucciones simples verdaderas/falsas |
| Fecha y hora | Calendario |  Se utiliza para mostrar la fecha y la hora en formato ISO 8601. Según el tipo seleccionado, hay tres variantes disponibles para usar en AEM GraphQL: `onlyDate`, `onlyTime`, `dateTime` |
| Lista desglosada |  Cadena |  Se utiliza para mostrar una opción de una lista de opciones definidas en la creación del modelo |
|  Etiquetas |  [Cadena] |  Se utiliza para mostrar una lista de cadenas que representan las etiquetas utilizadas en AEM |
| Referencia de contenido |  Cadena, [Cadena] |  Se utiliza para mostrar la ruta hacia otro recurso en AEM |
| Referencia al fragmento |  *Un tipo de modelo* |  Se utiliza para hacer referencia a otro fragmento de contenido de un tipo de modelo determinado, definido cuando se creó el modelo |

### Campos de ayuda {#helper-fields}

Además de los tipos de datos de los campos generados por el usuario, GraphQL para AEM también genera una serie de campos de *ayuda* para ayudar a identificar un fragmento de contenido o para proporcionar información adicional acerca de un fragmento de contenido.

Estos [campos de ayuda](#helper-fields) se marcan con un `_` que los precede para distinguir entre lo que ha definido el usuario y lo que se ha generado automáticamente.

#### Ruta  {#path}

El campo de ruta se utiliza como identificador en AEM GraphQL. Representa la ruta del recurso de fragmento de contenido dentro del repositorio de AEM. Hemos elegido esto como el identificador de un fragmento de contenido, ya que:

* es único dentro de AEM,
* se puede recuperar fácilmente.

El siguiente código muestra las rutas de todos los fragmentos de contenido creados en función del modelo de fragmento de contenido `Author`, tal como proporciona el tutorial de WKND.

```graphql
{
  authorList {
    items {
      _path
    }
  }
}
```

Para recuperar un solo fragmento de contenido de un tipo específico, también debe determinar primero su ruta. Por ejemplo:

```graphql
{
  authorByPath(_path: "/content/dam/wknd-shared/en/contributors/sofia-sj-berg") {
    item {
      _path
      firstName
      lastName
    }
  }
}
```

Consulte [Consulta de muestra: un solo fragmento de ciudad específico](/help/headless/graphql-api/sample-queries.md#sample-single-specific-city-fragment).

#### Metadatos {#metadata}

A través de GraphQL, AEM también expone los metadatos de un fragmento de contenido. Los metadatos son la información que describe un fragmento de contenido, como el título de un fragmento de contenido, la ruta de vista en miniatura, la descripción de un fragmento de contenido, la fecha en la que se creó, entre otros.

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
| `booleanArrayMetadata:[booleanArrayMetadata]!` |
| `calendarMetadata:[CalendarMetadata]!` |
| `calendarArrayMetadata:[CalendarArrayMetadata]!` |

Cada tipo escalar representa un único par nombre-valor o una matriz de pares nombre-valor, donde el valor de ese par es del tipo en el que se agrupó.

Por ejemplo, si desea recuperar el título de un fragmento de contenido, sabemos que esta propiedad es de cadena, por lo que consultaremos todos los metadatos de cadena:

Para consultar metadatos:

```graphql
{
  authorByPath(_path: "/content/dam/wknd-shared/en/contributors/sofia-sj-berg") {
    item {
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

```graphql
{
  authorByPath(_path: "/content/dam/wknd-shared/en/contributors/ian-provo") {
    item {
      _variations
    }
  }
}
```

>[!NOTE]
>
>Tenga en cuenta que `_variations` el campo no contiene un `master` como técnicamente los datos originales (referenciados como *Maestro* en la interfaz de usuario) no se considera una variación explícita.

Consulte [Consulta de muestra: todas las ciudades con una variación con nombre](/help/headless/graphql-api/sample-queries.md#sample-cities-named-variation).

>[!NOTE]
>
>Si la variación dada no existe para un fragmento de contenido, los datos originales (también conocidos como la variación maestra) se devolverán como predeterminados (alternativa).

<!--
## Security Considerations {#security-considerations}
-->

## Variables de GraphQL {#graphql-variables}

GraphQL permite colocar variables en la consulta. Para obtener más información, consulte la [Documentación de GraphQL para variables](https://graphql.org/learn/queries/#variables).

Por ejemplo, para obtener todos los fragmentos de contenido del tipo `Author` en una variación específica (si está disponible), puede especificar el argumento `variation` en GraphiQL.

![Variables de GraphQL](assets/cfm-graphqlapi-03.png "Variables de GraphQL")

**Consulta**:

```graphql
query($variation: String!) {
  authorList(variation: $variation) {
    items {
      _variation
      lastName
      firstName
    }
  }
}
```

**Variables de consulta**:

```json
{
  "variation": "another"
}
```

Esta consulta devolverá la lista completa de autores. Autores sin el `another` volverá a los datos originales (`_variation` informe `master` en este caso).

Si desea restringir la lista a autores que proporcionen la variación especificada (y omitir autores que vuelvan a los datos originales), deberá aplicar una [filter](#filtering):

```graphql
query($variation: String!) {
  authorList(variation: $variation, filter: {
    _variation: {
      _expressions: {
        value: $variation
      }
    }
  }) {
    items {
      _variation
      lastName
      firstName
    }
  }
}
```

## Directivas de GraphQL {#graphql-directives}

En GraphQL existe la posibilidad de cambiar la consulta en función de variables, denominadas Directivas de GraphQL.

Por ejemplo, puede incluir el campo `adventurePrice` en una consulta para todos los `AdventureModels`, en función de una variable `includePrice`.

![Directivas de GraphQL](assets/cfm-graphqlapi-04.png "Directivas de GraphQL")

**Consulta**:

```graphql
query GetAdventureByType($includePrice: Boolean!) {
  adventureList {
    items {
      title
      price @include(if: $includePrice)
    }
  }
}
```

**Variables de consulta**:

```json
{
    "includePrice": true
}
```

## Filtrado {#filtering}

También puede utilizar el filtrado en las consultas de GraphQL para devolver datos específicos.

El filtrado utiliza una sintaxis basada en operadores lógicos y expresiones.

La parte más atómica es una sola expresión que se puede aplicar al contenido de un campo determinado. Compara el contenido del campo con un valor constante determinado.

Por ejemplo, la expresión

```graphql
{
  value: "some text"
  _op: EQUALS
}
```

compararía el contenido del campo con el valor `some text` y se ejecuta correctamente si el contenido es igual al valor. De lo contrario, la expresión fallará.

El

Los siguientes operadores pueden utilizarse para comparar campos con un determinado valor:

| Operador | Tipo(s) | La expresión se realiza correctamente si ... |
|--- |--- |--- |
| `EQUALS` | `String`, `ID`, `Boolean` | ... el valor es exactamente el mismo que el contenido del campo |
| `EQUALS_NOT` | `String`, `ID` | ... el valor es *not* igual que el contenido del campo |
| `CONTAINS` | `String` | ... el contenido del campo contiene el valor (`{ value: "mas", _op: CONTAINS }` coincidirá `Christmas`, `Xmas`, `master`, ...) |
| `CONTAINS_NOT` | `String` | ... el contenido del campo sí *not* contiene el valor |
| `STARTS_WITH` | `ID` | ... el ID empieza con un determinado valor (`{ value: "/content/dam/", _op: STARTS_WITH` coincidirá `/content/dam/path/to/fragment`, pero no `/namespace/content/dam/something` |
| `EQUAL` | `Int`, `Float` | ... el valor es exactamente el mismo que el contenido del campo |
| `UNEQUAL` | `Int`, `Float` | ... el valor es *not* igual que el contenido del campo |
| `GREATER` | `Int`, `Float` | ... el contenido del campo es bueno que el valor |
| `GREATER_EQUAL` | `Int`, `Float` | ... el contenido del campo es bueno o igual al valor |
| `LOWER` | `Int`, `Float` | ... el contenido del campo es menor que el valor |
| `LOWER_EQUAL` | `Int`, `Float` | ... el contenido del campo es menor o igual que el valor |
| `AT` | `Calendar`, `Date`, `Time` | ... el contenido del campo es exactamente el mismo que el valor (incluida la configuración de zona horaria) |
| `NOT_AT` | `Calendar`, `Date`, `Time` | ... el contenido del campo es *not* igual que el valor |
| `BEFORE` | `Calendar`, `Date`, `Time` | ... el punto en el tiempo indicado por el valor es anterior al punto en el tiempo indicado por el contenido del campo |
| `AT_OR_BEFORE` | `Calendar`, `Date`, `Time` | ... el punto en el tiempo indicado por el valor es anterior o en el mismo punto en el tiempo indicado por el contenido del campo |
| `AFTER` | `Calendar`, `Date`, `Time` | ... el punto en el tiempo indicado por el valor es después del punto en el tiempo indicado por el contenido del campo |
| `AT_OR_AFTER` | `Calendar`, `Date`, `Time` | ... el punto en el tiempo indicado por el valor es después o en el mismo punto en el tiempo indicado por el contenido del campo |

Algunos tipos también permiten especificar opciones adicionales que modifican cómo se evalúa una expresión:

| Opción | Tipo(s) | Descripción |
|--- |--- |--- |
| `_ignoreCase` | `String` | Omite las mayúsculas y minúsculas de una cadena, por ejemplo, un valor de `time` coincidirá `TIME`, `time`, `tImE`, ... |
| `_sensitiveness` | `Float` | Permite un determinado margen para `float` para evitar limitaciones técnicas debidas a la representación interna de `float` valores; debe evitarse, ya que esta opción puede tener un impacto negativo en el rendimiento |

Las expresiones se pueden combinar en un conjunto con la ayuda de un operador lógico (`_logOp`):

* `OR` - el conjunto de expresiones tendrá éxito si al menos una expresión se realiza correctamente
* `AND` : el conjunto de expresiones se realizará correctamente si todas las expresiones se realizan correctamente (opción predeterminada).

Cada campo se puede filtrar por su propio conjunto de expresiones. Los conjuntos de expresiones de todos los campos mencionados en el argumento filter se combinarán finalmente con su propio operador lógico.

Una definición de filtro (que se transfiere como la variable `filter` argumento a una consulta) contiene:

* Una subdefinición para cada campo (se puede acceder al campo a través de su nombre, por ejemplo, hay un `lastName` en el filtro para la variable `lastName` en el campo Tipo de datos (campo)
* Cada subdefinición contiene la variable `_expressions` matriz, proporcionando el conjunto de expresiones y el `_logOp` campo que define el operador lógico con el que se deben combinar las expresiones
* Cada expresión está definida por el valor (`value` ) y el operador (`_operator` ) el contenido de un campo debe compararse con

Tenga en cuenta que puede omitir `_logOp` si desea combinar elementos con `AND` y `_operator` si desea comprobar la igualdad, ya que estos son los valores predeterminados.

El siguiente ejemplo muestra una consulta completa que filtra todas las personas que tienen un `lastName` de `Provo` o `sjö`, independientemente del caso:

```graphql
{
  authorList(filter: {
    lastname: {
      _logOp: OR
      _expressions: [
        {
          value: "sjö",
          _operator: CONTAINS,
          _ignoreCase: true
        },
        {
          value: "Provo"
        }
      ]
    }
  }) {
    items {
      lastName
      firstName
    }
  }
}
```

Aunque también puede filtrar por campos anidados, no se recomienda, ya que puede provocar problemas de rendimiento.

Para ver más ejemplos, consulte lo siguiente:

* detalles de [GraphQL para extensiones de AEM](#graphql-extensions)

* [Ejemplos de consultas que utilizan este contenido y estructura de muestra](/help/headless/graphql-api/sample-queries.md#graphql-sample-queries-sample-content-fragment-structure)

   * Y el [Contenido y estructura de muestra](/help/headless/graphql-api/sample-queries.md#content-fragment-structure-graphql) preparados para su uso en consultas de muestra

* [Consultas de muestra basadas en el proyecto WKND](/help/headless/graphql-api/sample-queries.md#sample-queries-using-wknd-project)

## Ordenación {#sorting}

Esta función permite ordenar los resultados de la consulta según un campo especificado.

Los criterios de clasificación:

* es una lista de valores separados por comas que representa la ruta del campo
   * el primer campo de la lista define el criterio de ordenación principal, el segundo campo se utiliza si dos valores del criterio de ordenación principal son iguales, el tercero si los dos primeros criterios son iguales, etc.
   * notación punteada, es decir, field1.subfield.subfield, etc...
* con una dirección de pedido opcional
   * ASC (ascendente) o DESC (descendente); como ASC predeterminado se aplica
   * se puede especificar la dirección por campo; esto significa que puede ordenar un campo en orden ascendente y otro en orden descendente (nombre, nombre DESC)

Por ejemplo:

```graphql
query {
  authorList(sort: "lastName, firstName") {
    items {
      firstName
      lastName
    }
  }
}
```

Y también:

```graphql
{
  authorList(sort: "lastName DESC, firstName DESC") {
    items {
        lastName
        firstName
    }
  }
}
```

<!-- to be included? -->

También puede ordenar un campo dentro de un fragmento anidado, utilizando el formato de `nestedFragmentname.fieldname`.

>[!NOTE]
>
>Esto puede tener un impacto negativo en el rendimiento.

Por ejemplo:

```graphql
query {
  articleList(sort: "authorFragment.lastName")  {
    items {
      title
      authorFragment {
        firstName
        lastName
        birthDay
      }
      slug
    }
  }
}
```

## Paginación {#paging}

Esta función le permite realizar paginación en tipos de consulta que devuelven una lista. Se proporcionan dos métodos:

* `offset` y `limit` en un `List` query
* `first` y `after` en un `Paginated` query

### Consulta de lista: desplazamiento y límite {#list-offset-limit}

En un `...List`consulta que puede utilizar `offset` y `limit` para devolver un subconjunto específico de resultados:

* `offset`: Especifica el primer conjunto de datos que se va a devolver
* `limit`: Especifica el número máximo de conjuntos de datos que se van a devolver

Por ejemplo, para generar la página de resultados que contiene hasta cinco artículos, a partir del quinto artículo de la sección *complete* lista de resultados:

```graphql
query {
   articleList(offset: 5, limit: 5) {
    items {
      authorFragment {
        lastName
        firstName
      }
    }
  }
}
```

<!-- When available link to BP and replace "JCR query level" with a more neutral term. -->

<!-- When available link to BP and replace "JCR query result set" with a more neutral term. -->

>[!NOTE]
>
>* La paginación requiere un orden de clasificación estable para funcionar correctamente en varias consultas que soliciten diferentes páginas del mismo conjunto de resultados. De forma predeterminada, utiliza la ruta del repositorio de cada elemento del conjunto de resultados para asegurarse de que el orden sea siempre el mismo. Si se utiliza un criterio de ordenación diferente y si esa ordenación no se puede realizar en el nivel de consulta JCR, habrá un impacto negativo en el rendimiento, ya que todo el conjunto de resultados debe cargarse en la memoria antes de que se puedan determinar las páginas.
>
>* Cuanto mayor sea el desplazamiento, más tiempo tardará en omitir los elementos del conjunto de resultados de la consulta JCR completa. Una solución alternativa para grandes conjuntos de resultados es utilizar la consulta paginada con `first` y `after` método.


### Consulta paginada: primero y después {#paginated-first-after}

La variable `...Paginated` el tipo de consulta reutiliza la mayoría de las `...List` funciones de tipo de consulta (filtrado, clasificación), pero en lugar de usar `offset`/`limit` argumentos, utiliza la variable `first`/`after` los argumentos definidos por [Especificación de las conexiones del cursor de GraphQL](https://relay.dev/graphql/connections.htm). Puede encontrar una introducción menos formal en la [Introducción a GraphQL](https://graphql.org/learn/pagination/#pagination-and-edges).

* `first`: La variable `n` los primeros artículos que se van a devolver.
El valor predeterminado es `50`.
El número máximo es `100`.
* `after`: El cursor que determina el comienzo de la página solicitada; tenga en cuenta que el elemento representado por el cursor no se incluye en el conjunto de resultados; el cursor de un elemento se determina mediante la variable `cursor` del campo `edges` estructura.

Por ejemplo, mostrar la página de resultados que contienen hasta cinco aventuras, empezando por el elemento de cursor dado en la variable *complete* lista de resultados:

```graphql
query {
    adventurePaginated(first: 5, after: "ODg1MmMyMmEtZTAzMy00MTNjLThiMzMtZGQyMzY5ZTNjN2M1") {
        edges {
          cursor
          node {
            title
          }
        }
        pageInfo {
          endCursor
          hasNextPage
        }
    }
}
```

<!-- When available link to BP -->
<!-- Due to internal technical constraints, performance will degrade if sorting and filtering is applied on nested fields. Therefore it is recommended to use filter/sort fields stored at root level. For more information, see the [Best Practices document](link). -->

>[!NOTE]
>
>* De forma predeterminada, la paginación utiliza el UUID del nodo del repositorio que representa el fragmento para ordenar a fin de garantizar que el orden de los resultados sea siempre el mismo. When `sort` se utiliza, el UUID se utiliza implícitamente para garantizar un orden único; incluso para dos elementos con claves de ordenación idénticas.
>
>* Debido a limitaciones técnicas internas, el rendimiento se degradará si se aplican ordenación y filtrado en los campos anidados. Por lo tanto, se recomienda utilizar filtrar/ordenar campos almacenados en el nivel raíz. Esta es también la forma recomendada si desea consultar grandes conjuntos de resultados paginados.


## GraphQL para AEM: resumen de extensiones {#graphql-extensions}

El funcionamiento básico de las consultas con GraphQL para AEM se adhiere a la especificación estándar de GraphQL. Para las consultas de GraphQL con AEM hay algunas extensiones:

* Si espera una lista de resultados:
   * añada `List` al nombre del modelo; por ejemplo, `cityList`
   * Consulte [Consulta de muestra: toda la información acerca de todas las ciudades](/help/headless/graphql-api/sample-queries.md#sample-all-information-all-cities)

   Podrá:

   * [Ordenar los resultados](#sorting)

      * `ASC` : ascendente
      * `DESC` : descendente
   * Devolver una página de resultados mediante:

      * [Una consulta de lista con desplazamiento y límite](#list-offset-limit)
      * [Una consulta paginada con primero y después](#paginated-first-after)
   * Consulte [Consulta de muestra: toda la información acerca de todas las ciudades](/help/headless/graphql-api/sample-queries.md#sample-all-information-all-cities)



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
         >Si la variación dada no existe para un Fragmento de contenido, la variación principal se devolverá como una predeterminada (alternativa).

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

## Preguntas frecuentes {#faqs}

Preguntas que han surgido:

1. **P**: “*¿En qué se diferencia la API de GraphQL para AEM de la API Generador de consultas?*”

   * **R**: “*La API de GraphQL de AEM ofrece control total sobre la salida JSON y es un estándar en la industria para consultar contenido.
En adelante, AEM tiene previsto invertir en la API de GraphQL de AEM”.*

## Tutorial: Introducción a AEM Headless y GraphQL {#tutorial}

¿Busca un tutorial práctico? Consulte el tutorial completo [Introducción a AEM Headless y GraphQL](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/overview.html?lang=es), que ilustra cómo crear y exponer contenido mediante las API de GraphQL de AEM y consumido por una aplicación externa, en un escenario de CMS sin encabezado.