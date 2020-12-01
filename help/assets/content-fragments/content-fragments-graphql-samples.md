---
title: 'Aprender a utilizar GraphQL con AEM: Contenido y Consultas de muestra'
description: 'Aprender a utilizar GraphQL con AEM: contenido y Consultas de muestra.'
translation-type: tm+mt
source-git-commit: 46e179faa7875c4b3e9da30356d2b82d4b25b130
workflow-type: tm+mt
source-wordcount: '1283'
ht-degree: 6%

---


# Aprender a usar GraphQL con AEM: Contenido de muestra y Consultas {#learn-graphql-with-aem-sample-content-queries}

>[!CAUTION]
>
>La API de AEM GraphQL, para el Envío de fragmentos de contenido, se lanzará a principios de 2021.
>
>La documentación relacionada ya está disponible para fines de previsualización.

Para empezar con las consultas de GraphQL y cómo funcionan con fragmentos de contenido de AEM ayuda ver algunos ejemplos prácticos.

Para obtener ayuda con esto, consulte:

* Una [estructura de fragmento de contenido de muestra](#content-fragment-structure-graphql)

* Y algunas [consultas GraphQL de muestra](#graphql-sample-queries), basadas en la estructura de fragmentos de contenido de muestra (Modelos de fragmento de contenido y fragmentos de contenido relacionados).

## GraphQL para AEM - Algunas extensiones {#graphql-some-extensions}

El funcionamiento básico de las consultas con GraphQL para AEM se adhiere a la especificación GraphQL estándar. Para las consultas de GraphQL con AEM hay algunas extensiones:

* Si necesita un único resultado:
   * utilizar el nombre del modelo; eg city

* Si espera una lista de los resultados:
   * añadir &quot;Lista&quot; al nombre del modelo; por ejemplo, `cityList`

* Si desea utilizar un OR lógico:
   * use &quot; _logOp: OR&quot;

* AND lógico también existe, pero es (a menudo) implícito

* Puede realizar consultas en los nombres de campo que se correspondan con los campos del modelo de fragmento de contenido

* Además de los campos del modelo, hay algunos campos generados por el sistema (precedidos de subrayado):

   * Para contenido:

      * `_locale` :: revelar el idioma; según el Administrador de idiomas

      * `_metadata` :: para mostrar metadatos para el fragmento

      * `_path` :: la ruta de su fragmento de contenido dentro del repositorio

      * `_references` :: revelar referencias; incluir referencias en línea en el Editor de texto enriquecido

      * `_variations` :: para revelar variaciones específicas dentro del fragmento de contenido
   * Y operaciones:

      * `_operator` :: aplicar operadores específicos;  `EQUALS`,  `EQUALS_NOT`,  `GREATER_EQUAL`,  `LOWER`,  `CONTAINS`,

      * `_apply` :: aplicar condiciones específicas; por ejemplo,   `AT_LEAST_ONCE`

      * `_ignoreCase` :: para ignorar el caso al consultar


* Se admiten los tipos de unión de GraphQL:

   * use `...on`


## Una estructura de fragmento de contenido de muestra para su uso con GraphQL {#content-fragment-structure-graphql}

Para un ejemplo sencillo necesitamos:

* Uno o más modelos de fragmento de contenido de muestra [](#sample-content-fragment-models-schemas) - forman la base para los esquemas de GraphQL

* [Ejemplo de ](#sample-content-fragments) fragmentos de contenido basados en los modelos anteriores

### Modelos de fragmento de contenido de muestra (Esquemas) {#sample-content-fragment-models-schemas}

Para las consultas de muestra, utilizaremos los siguientes modelos de contenido y sus interrelaciones (referencias ->):

* [Compañía](#model-company)
->  [Persona](#model-person)
    ->  [Premio](#model-award)

* [Ciudad](#model-city)

#### Empresa {#model-company}

Los campos básicos que definen la compañía son:

| Nombre del campo | Tipo de datos | Referencia |
|--- |--- |--- |
| Nombre de compañía | Texto de línea única |  |
| CEO | Referencia de fragmento (única) | [Person](#model-person) |
| Empleados | Referencia de fragmento (multicampo) | [Persona](#model-person) |

#### Person {#model-person}

Campos que definen a una persona, que también puede ser un empleado:

| Nombre del campo | Tipo de datos | Referencia |
|--- |--- |--- |
| Nombre | Texto de línea única |  |
| Nombre | Texto de línea única |  |
| Premios | Referencia de fragmento (multicampo) | [Premio](#model-award) |

#### Premio {#model-award}

Los campos que definen un premio son:

| Nombre del campo | Tipo de datos | Referencia |
|--- |--- |--- |
| Acceso directo/ID | Texto de línea única |  |
| Título | Texto de línea única |  |

#### Ciudad {#model-city}

Los campos para definir una ciudad son:

| Nombre del campo | Tipo de datos | Referencia |
|--- |--- |--- |
| Nombre | Texto de línea única |  |
| País | Texto de línea única |  |
| Población | Número |  |
| Categorías | Etiquetas |  |

### Fragmentos de contenido de muestra {#sample-content-fragments}

Los siguientes fragmentos se utilizan para el modelo adecuado.

#### Empresa {#fragment-company}

| Nombre de compañía | CEO | Empleados |
|--- |--- |--- |
| Apple | Steve Jobs | Mármoles de duelo<br>Máx. |
|  Little Pony Inc. | Adam Smith | Lara Croft<br>Cutter Slave |
| NextStep Inc. | Steve Jobs | Joe Smith<br>Abe Lincoln |

#### Persona {#fragment-person}

| Nombre | Nombre | Premios |
|--- |--- |--- |
| Lincoln |  Abe |  |
| Smith | Adam |   |
| Esclavo |  Cutter |  Gameblitz<br>Gamestar |
| Marsh |  Duke |   |   |
|  Smith |  Joe |   |
| Recortar |  Lara | Gamestar |
| Caulfield |  Máximo |  Gameblitz |
|  Trabajos |  Steve |   |

#### Premio {#fragment-award}

| Acceso directo/ID | Título |
|--- |--- |
| GB | Gameblitz |
|  GS | Gamestar |
|  OSC | Oscar |

#### Ciudad {#fragment-city}

| Nombre | País | Población | Categorías |
|--- |--- |--- |--- |
| Basilea | Suiza | 172258 | ciudad:emea |
| Berlín | Alemania | 3669491 | ciudad:capital<br>ciudad:emea |
| Bucarest | Rumanía | 1821000 |  ciudad:capital<br>ciudad:emea |
| San Francisco |  EE.UU. |  883306 |  ciudad:playa<br>ciudad:na |
| San José |  EE.UU. |  102635 |  ciudad:na |
| Stuttgart |  Alemania |  634830 |  ciudad:emea |
|  Zúrich |  Suiza |  415367 |  ciudad:capital<br>ciudad:emea |

## GraphQL: Consultas de muestra que usan la estructura de fragmentos de contenido de muestra {#graphql-sample-queries-sample-content-fragment-structure}

Consulte las consultas de muestra para ver ilustraciones de la creación de consultas, junto con resultados de muestra.

>[!NOTE]
>
>Según la instancia, puede acceder directamente a la interfaz [Graph *i* QL incluida con la API de GraphQL](/help/assets/content-fragments/graphql-api-content-fragments.md#graphiql-interface) de AEM para enviar y probar consultas.
>
>Por ejemplo: `http://localhost:4502/content/graphiql.html`

### Consulta de muestra: Todos los Esquemas y tipos de datos disponibles {#sample-all-schemes-datatypes}

Esto devolverá todos los tipos para todos los esquemas disponibles.

**Consulta de muestra**

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

**Resultado de muestra**

```xml
{
  "data": {
    "__schema": {
      "types": [
        {
          "name": "AdventureModel",
          "description": null
        },
        {
          "name": "AdventureModelArrayFilter",
          "description": null
        },
        {
          "name": "AdventureModelFilter",
          "description": null
        },
        {
          "name": "AdventureModelResult",
          "description": null
        },
        {
          "name": "AdventureModelResults",
          "description": null
        },
        {
          "name": "AllFragmentModels",
          "description": null
        },
        {
          "name": "ArchiveRef",
          "description": null
        },
        {
          "name": "ArrayMode",
          "description": null
        },
        {
          "name": "ArticleModel",
          "description": null
        },

...more results...

        {
          "name": "__EnumValue",
          "description": null
        },
        {
          "name": "__Field",
          "description": null
        },
        {
          "name": "__InputValue",
          "description": null
        },
        {
          "name": "__Schema",
          "description": "A GraphQL Introspection defines the capabilities of a GraphQL server. It exposes all available types and directives on the server, the entry points for query, mutation, and subscription operations."
        },
        {
          "name": "__Type",
          "description": null
        },
        {
          "name": "__TypeKind",
          "description": "An enum describing what kind of type a given __Type is"
        }
      ]
    }
  }
}
```

### Consulta de muestra: Detalles completos del director ejecutivo y los empleados de una Compañía {#sample-full-details-company-ceos-employees}

Utilizando la estructura de los fragmentos anidados, esta consulta devuelve todos los detalles del director general de una compañía y de todos sus empleados.

**Consulta de muestra**

```xml
query {
  companyList {
    items {
      name
      ceo {
        _path
        name
        firstName
        awards {
        id
          title
        }
      }
      employees {
       name
        firstName
       awards {
         id
          title
        }
      }
    }
  }
}
```

**Resultados de muestra**

```xml
{
  "data": {
    "companyList": {
      "items": [
        {
          "name": "Apple Inc.",
          "ceo": {
            "_path": "/content/dam/sample-content-fragments/persons/steve-jobs",
            "name": "Jobs",
            "firstName": "Steve",
            "awards": []
          },
          "employees": [
            {
              "name": "Marsh",
              "firstName": "Duke",
              "awards": []
            },
            {
              "name": "Caulfield",
              "firstName": "Max",
              "awards": [
                {
                  "id": "GB",
                  "title": "Gameblitz"
                }
              ]
            }
          ]
        },
        {
          "name": "Little Pony, Inc.",
          "ceo": {
            "_path": "/content/dam/sample-content-fragments/persons/adam-smith",
            "name": "Smith",
            "firstName": "Adam",
            "awards": []
          },
          "employees": [
            {
              "name": "Croft",
              "firstName": "Lara",
              "awards": [
                {
                  "id": "GS",
                  "title": "Gamestar"
                }
              ]
            },
            {
              "name": "Slade",
              "firstName": "Cutter",
              "awards": [
                {
                  "id": "GB",
                  "title": "Gameblitz"
                },
                {
                  "id": "GS",
                  "title": "Gamestar"
                }
              ]
            }
          ]
        },
        {
          "name": "NextStep Inc.",
          "ceo": {
            "_path": "/content/dam/sample-content-fragments/persons/steve-jobs",
            "name": "Jobs",
            "firstName": "Steve",
            "awards": []
          },
          "employees": [
            {
              "name": "Smith",
              "firstName": "Joe",
              "awards": []
            },
            {
              "name": "Lincoln",
              "firstName": "Abraham",
              "awards": []
            }
          ]
        }
      ]
    }
  }
}
```

### Consulta de muestra: Toda la información sobre todas las ciudades {#sample-all-information-all-cities}

Para recuperar toda la información sobre todas las ciudades, puede utilizar la consulta básica:
**Consulta de muestra**

```xml
{
  cityList {
    items
  }
}
```

Cuando se ejecuta, el sistema expandirá automáticamente la consulta para incluir todos los campos:

```xml
{
  cityList {
    items {
      _path
      name
      country
      population
    }
  }
}
```

**Resultados de muestra**

```xml
{
  "data": {
    "cityList": {
      "items": [
        {
          "_path": "/content/dam/sample-content-fragments/cities/basel",
          "name": "Basel",
          "country": "Switzerland",
          "population": 172258
        },
        {
          "_path": "/content/dam/sample-content-fragments/cities/berlin",
          "name": "Berlin",
          "country": "Germany",
          "population": 3669491
        },
        {
          "_path": "/content/dam/sample-content-fragments/cities/bucharest",
          "name": "Bucharest",
          "country": "Romania",
          "population": 1821000
        },
        {
          "_path": "/content/dam/sample-content-fragments/cities/san-francisco",
          "name": "San Francisco",
          "country": "USA",
          "population": 883306
        },
        {
          "_path": "/content/dam/sample-content-fragments/cities/san-jose",
          "name": "San Jose",
          "country": "USA",
          "population": 1026350
        },
        {
          "_path": "/content/dam/sample-content-fragments/cities/stuttgart",
          "name": "Stuttgart",
          "country": "Germany",
          "population": 634830
        },
        {
          "_path": "/content/dam/sample-content-fragments/cities/zurich",
          "name": "Zurich",
          "country": "Switzerland",
          "population": 415367
        }
      ]
    }
  }
}
```

### Consulta de muestra - Nombres de todas las ciudades {#sample-names-all-cities}

Se trata de una consulta directa para devolver el `name`de todas las entradas del esquema `city`.

**Consulta de muestra**

```xml
query {
  cityList {
    items {
      name
    }
  }
}
```

**Resultados de muestra**

```xml
{
  "data": {
    "cityList": {
      "items": [
        {
          "name": "Basel"
        },
        {
          "name": "Berlin"
        },
        {
          "name": "Bucharest"
        },
        {
          "name": "San Francisco"
        },
        {
          "name": "San Jose"
        },
        {
          "name": "Stuttgart"
        },
        {
          "name": "Zurich"
        }
      ]
    }
  }
}
```

### Consulta de muestra: un solo fragmento de ciudad {#sample-single-city-fragment}

Se trata de una consulta para devolver los detalles de una sola entrada de fragmento en una ubicación específica del repositorio.

**Consulta de muestra**

```xml
{
  cityByPath (_path: "/content/dam/sample-content-fragments/cities/berlin") {
    item {
      _path
      name
      country
      population
     categories
    }
  }
}
```

**Resultados de muestra**

```xml
{
  "data": {
    "cityByPath": {
      "item": {
        "_path": "/content/dam/sample-content-fragments/cities/berlin",
        "name": "Berlin",
        "country": "Germany",
        "population": 3669491,
        "categories": [
          "city:capital",
          "city:emea"
        ]
      }
    }
  }
}
```

### Consulta de muestra: Todas las ciudades con una variación con nombre {#sample-cities-named-variation}

Si crea una nueva variación, denominada &quot;Centro de Berlín&quot; (`berlin_centre`), para la `city` Berlín, puede utilizar una consulta para devolver detalles de la variación.

**Consulta de muestra**

```xml
{
  cityList (variation: "berlin_center") {
    items {
      _path
      name
      country
      population
      categories
    }
  }
}
```

**Resultados de muestra**

```xml
{
  "data": {
    "cityList": {
      "items": [
        {
          "_path": "/content/dam/sample-content-fragments/cities/berlin",
          "name": "Berlin",
          "country": "Germany",
          "population": 3669491,
          "categories": [
            "city:capital",
            "city:emea"
          ]
        }
      ]
    }
  }
}
```

### Consulta de muestra: Todas las personas que tienen un nombre de &quot;Trabajos&quot; o &quot;Smith&quot; {#sample-all-persons-jobs-smith}

Esto filtrará todos los `persons` para aquellos que tengan el nombre `Jobs`o `Smith`.

**Consulta de muestra**

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

**Resultados de muestra**

```xml
{
  "data": {
    "personList": {
      "items": [
        {
          "name": "Smith",
          "firstName": "Adam"
        },
        {
          "name": "Smith",
          "firstName": "Joe"
        },
        {
          "name": "Jobs",
          "firstName": "Steve"
        }
      ]
    }
  }
}
```

### Consulta de muestra: Todas las personas que no tienen un nombre de &quot;Trabajos&quot; {#sample-all-persons-not-jobs}

Esto filtrará todos los `persons` para aquellos que tengan el nombre `Jobs`o `Smith`.

**Consulta de muestra**

```xml
query {
  personList(filter: {
    name: {
      _expressions: [
        {
          value: "Jobs"
          _operator: EQUALS_NOT
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

**Resultados de muestra**

```xml
{
  "data": {
    "personList": {
      "items": [
        {
          "name": "Lincoln",
          "firstName": "Abraham"
        },
        {
          "name": "Smith",
          "firstName": "Adam"
        },
        {
          "name": "Slade",
          "firstName": "Cutter"
        },
        {
          "name": "Marsh",
          "firstName": "Duke"
        },
        {
          "name": "Smith",
          "firstName": "Joe"
        },
        {
          "name": "Croft",
          "firstName": "Lara"
        },
        {
          "name": "Caulfield",
          "firstName": "Max"
        }
      ]
    }
  }
}
```

### Consulta de muestra: Todas las ciudades situadas en Alemania o Suiza con una población entre 400000 y 999999 {#sample-all-cities-d-ch-population}

Aquí se filtra una combinación de campos. Se utiliza un `AND` (implícito) para seleccionar el rango `population`mientras que se utiliza un `OR` (explícito) para seleccionar las ciudades requeridas.

**Consulta de muestra**

```xml
query {
  cityList(filter: {
    population: {
      _expressions: [
        {
          value: 400000
          _operator: GREATER_EQUAL
        }, {
          value: 1000000
          _operator: LOWER
        }
      ]
    },
    country: {
      _logOp: OR
      _expressions: [
        {
          value: "Germany"
        }, {
          value: "Switzerland"
        }
      ]
    }
  }) {
    items {
      name
      population
      country
    }
  }
}
```

**Resultados de muestra**

```xml
{
  "data": {
    "cityList": {
      "items": [
        {
          "name": "Stuttgart",
          "population": 634830,
          "country": "Germany"
        },
        {
          "name": "Zurich",
          "population": 415367,
          "country": "Switzerland"
        }
      ]
    }
  }
}
```

### Consulta de muestra: Todas las ciudades con SAN en el nombre, independientemente del caso {#sample-all-cities-san-ignore-case}

Esta consulta interroga a todas las ciudades que tengan `SAN` en el nombre, independientemente del caso.

**Consulta de muestra**

```xml
query {
  cityList(filter: {
    name: {
      _expressions: [
        {
          value: "SAN"
          _operator: CONTAINS
          _ignoreCase: true
        }
      ]
    }
  }) {
    items {
      name
      population
      country
    }
  }
}
```

**Resultados de muestra**

```xml
{
  "data": {
    "cityList": {
      "items": [
        {
          "name": "San Francisco",
          "population": 883306,
          "country": "USA"
        },
        {
          "name": "San Jose",
          "population": 1026350,
          "country": "USA"
        }
      ]
    }
  }
}
```

### Consulta de muestra: filtre en una matriz con un elemento que debe producirse al menos una vez {#sample-array-item-occur-at-least-once}

Esta consulta filtros en una matriz con un elemento (`city:na`) que debe producirse al menos una vez.

**Consulta de muestra**

```xml
query {
  cityList(filter: {
    categories: {
      _expressions: [
        {
          value: "city:na"
          _apply: AT_LEAST_ONCE
        }
      ]
    }
  }) {
    items {
      name
      population
      country
      categories
    }
  }
}
```

**Resultados de muestra**

```xml
{
  "data": {
    "cityList": {
      "items": [
        {
          "name": "San Francisco",
          "population": 883306,
          "country": "USA",
          "categories": [
            "city:beach",
            "city:na"
          ]
        },
        {
          "name": "San Jose",
          "population": 1026350,
          "country": "USA",
          "categories": [
            "city:na"
          ]
        }
      ]
    }
  }
}
```

### Consulta de muestra: filtre un valor de matriz exacto {#sample-array-exact-value}

Esta consulta filtros en un valor de matriz exacto.

**Consulta de muestra**

```xml
query {
  cityList(filter: {
    categories: {
      _expressions: [
        {
          values: [
            "city:beach",
            "city:na"
          ]
        }
      ]
    }
  }) {
    items {
      name
      population
      country
      categories
    }
  }
}
```

**Resultados de muestra**

```xml
{
  "data": {
    "cityList": {
      "items": [
        {
          "name": "San Francisco",
          "population": 883306,
          "country": "USA",
          "categories": [
            "city:beach",
            "city:na"
          ]
        }
      ]
    }
  }
}
```

### Consulta de muestra para fragmentos de contenido anidados: todas las compañías que tienen al menos un empleado con el nombre &quot;Smith&quot; {#sample-companies-employee-smith}

Esta consulta ilustra el filtrado para cualquier `person` de `name` &quot;Smith&quot;, devolviendo información de dos fragmentos anidados: `company` y `employee`.

**Consulta de muestra**

```xml
query {
  companyList(filter: {
    employees: {
      _match: {
        name: {
          _expressions: [
            {
              value: "Smith"
            }
          ]
        }
      }
    }
  }) {
    items {
      name
      ceo {
        name
        firstName
      }
      employees {
        name
        firstName
      }
    }
  }
}
```

**Resultados de muestra**

```xml
{
  "data": {
    "companyList": {
      "items": [
        {
          "name": "NextStep Inc.",
          "ceo": {
            "name": "Jobs",
            "firstName": "Steve"
          },
          "employees": [
            {
              "name": "Smith",
              "firstName": "Joe"
            },
            {
              "name": "Lincoln",
              "firstName": "Abraham"
            }
          ]
        }
      ]
    }
  }
}
```

### Consulta de muestra para fragmentos de contenido anidado: todas las compañías donde todos los empleados han ganado el premio &quot;Gamestar&quot; {#sample-all-companies-employee-gamestar-award}

Esta consulta ilustra el filtrado en tres fragmentos anidados: `company`, `employee` y `award`.

**Consulta de muestra**

```xml
query {
  companyList(filter: {
    employees: {
      _apply: ALL
      _match: {
        awards: {
          _match: {
            id: {
              _expressions: [
                {
                  value: "GS"
                  _operator:EQUALS
                }
              ]
            }
          }
        }
      }
    }
  }) {
    items {
      name
      ceo {
        name
        firstName
      }
      employees {
        name
        firstName
        awards {
          id
          title
        }
      }
    }
  }
}
```

**Resultados de muestra**

```xml
{
  "data": {
    "companyList": {
      "items": [
        {
          "name": "Little Pony, Inc.",
          "ceo": {
            "name": "Smith",
            "firstName": "Adam"
          },
          "employees": [
            {
              "name": "Croft",
              "firstName": "Lara",
              "awards": [
                {
                  "id": "GS",
                  "title": "Gamestar"
                }
              ]
            },
            {
              "name": "Slade",
              "firstName": "Cutter",
              "awards": [
                {
                  "id": "GB",
                  "title": "Gameblitz"
                },
                {
                  "id": "GS",
                  "title": "Gamestar"
                }
              ]
            }
          ]
        }
      ]
    }
  }
}
```

### Consulta de muestra para metadatos: Lista de los metadatos para los premios con el título GB {#sample-metadata-awards-gb}

Esta consulta ilustra el filtrado en tres fragmentos anidados: `company`, `employee` y `award`.

**Consulta de muestra**

```xml
query {
  awardList(filter: {
      id: {
        _expressions: [
          {
            value:"GB"
          }
        ]
    }
  }) {
    items {
      _metadata {
        stringMetadata {
          name,
          value
        }
      }
      id
      title
    }
  }
}
```

**Resultados de muestra**

```xml
{
  "data": {
    "awardList": {
      "items": [
        {
          "_metadata": {
            "stringMetadata": [
              {
                "name": "title",
                "value": "Gameblitz Award"
              },
              {
                "name": "description",
                "value": ""
              }
            ]
          },
          "id": "GB",
          "title": "Gameblitz"
        }
      ]
    }
  }
}
```

## Consultas de muestra que utilizan el proyecto WKND {#sample-queries-using-wknd-project}

Estas consultas de muestra se basan en el proyecto WKND.

>[!NOTE]
>
>Como los resultados pueden ser amplios, no se reproducen aquí.

### Consulta de muestra para todos los fragmentos de contenido de un modelo determinado con las propiedades especificadas {#sample-wknd-all-model-properties}

Esta consulta de muestra interroga:

* para todos los fragmentos de contenido de tipo `article`
* con las propiedades `path`y `author`.

**Consulta de muestra**

```xml
{
  articleList {
    items {
      _path
      author
    }
  }
}
```

### Consulta de muestra para metadatos {#sample-wknd-metadata}

Esta consulta cuestiona:

* para todos los fragmentos de contenido de tipo `adventure`
* metadata

**Consulta de muestra**

```xml
{
  adventureList {
    items {
      _path,
      _metadata {
        stringMetadata {
          name,
          value
        }
        stringArrayMetadata {
          name,
          value
        }
        intMetadata {
          name,
          value
        }
        intArrayMetadata {
          name,
          value
        }
        floatMetadata {
          name,
          value
        }
        floatArrayMetadata {
          name,
          value
        }
        booleanMetadata {
          name,
          value
        }
        booleanArrayMetadata {
          name,
          value
        }
        calendarMetadata {
          name,
          value
        }
        calendarArrayMetadata {
          name,
          value
        }
      }
    }
  }
}
```

### Consulta de muestra para un solo fragmento de contenido de un modelo determinado {#sample-wknd-single-content-fragment-of-given-model}

Esta consulta de muestra interroga:

* para un solo fragmento de contenido de un modelo determinado
* para todos los formatos de contenido:
   * HTML
   * Markdown
   * Texto sin formato
   * JSON

**Consulta de muestra**

```xml
{
  articleByPath (_path: "/content/dam/wknd/en/magazine/alaska-adventure/alaskan-adventures") {
    item {
        _path
        author
        main {
          html
          markdown
          plaintext
          json
        }
    }
  }
}
```

### Consulta de muestra para un fragmento de contenido anidado - Tipo de modelo único{#sample-wknd-nested-fragment-single-model}

**Consulta de muestra**

```xml
{
  articleByPath (_path: "/content/dam/wknd/en/magazine/skitouring/skitouring") {
    item {
        _path
        author
        referencearticle {
          _path
          author
      }
    }
  }
}
```

### Consulta de muestra para un fragmento de contenido anidado - Tipo de modelo múltiple{#sample-wknd-nested-fragment-multiple-model}

```xml
{
  bookmarkList {
    items {
        fragments {
          ... on ArticleModel {
            _path
            author
          }
          ... on AdventureModel {
            _path
            adventureTitle
          }
        }
     }
  }
}
```

### Consulta de muestra para un fragmento de contenido de un modelo específico con una referencia de contenido{#sample-wknd-fragment-specific-model-content-reference}

```xml
{
  bookmarkList {
    items {
      attachments {
        ... on PageRef {
          _path
          type
        }
        ... on ImageRef {
          _path
          width
        }
        ... on MultimediaRef {
          _path
          size
        }
        ... on DocumentRef {
          _path
          author
        }
        ... on ArchiveRef {
          _path
          format
        }
      }
    }
  }
}
```

### Consulta de muestra para varios fragmentos de contenido con referencias de recuperación previa {#sample-wknd-multiple-fragments-prefetched-references}

```xml
{
  bookmarkList {
    _references {
       ... on ImageRef {
        _path
        type
        height
      }
      ... on MultimediaRef {
        _path
        type
        size
      }
      ... on DocumentRef {
        _path
        type
        author
      }
      ... on ArchiveRef {
        _path
        type
        format
      }
    }
  }
}
```

### Consulta de muestra para una única variación de fragmento de contenido de un modelo determinado {#sample-wknd-single-fragment-given-model}

**Consulta de muestra**

```xml
{
  articleByPath (_path: "/content/dam/wknd/en/magazine/alaska-adventure/alaskan-adventures", variation: "variation1") {
    item {
      _path
      author
      main {
        html
        markdown
        plaintext
        json
      }
    }
  }
}
```

### Consulta de muestra para varios fragmentos de contenido de una configuración regional determinada {#sample-wknd-multiple-fragments-given-locale}

**Consulta de muestra**

```xml
{ 
  articleList (_locale: "fr") {
    items {
      _path
      author
      main {
        html
        markdown
        plaintext
        json
      }
    }
  }
}
```

### Consulta de muestra para un único fragmento de contenido con referencia en línea RTE {#sample-wknd-single-fragment-rte-inline-reference}

**Consulta de muestra**

```xml
{
  bookmarkByPath(_path: "/content/dam/wknd/en/bookmarks/skitouring") {
    item {
      _path
      description {
        json
      }
    }
    _references {
      ... on ArticleModel {
        _path
      }
      ... on AdventureModel {
        _path
      }
      ... on ImageRef {
        _path
      }
      ... on MultimediaRef {
        _path
      }
      ... on DocumentRef {
        _path
      }
      ... on ArchiveRef {
        _path
      }
    }
  }
}
```

### Consulta de muestra para una variación con nombre de varios fragmentos de contenido de un modelo determinado {#sample-wknd-variation-multiple-fragment-given-model}

**Consulta de muestra**

```xml
{
  articleList (variation: "variation1") {
    items {
      _path
      author
      main {
        html
        markdown
        plaintext
        json
      }
    }
  }
}
```
