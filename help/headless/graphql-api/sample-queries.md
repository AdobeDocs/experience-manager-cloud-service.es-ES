---
title: 'Formación para utilizar GraphQL con AEM: contenido y consultas de muestra'
description: Aprenda a utilizar GraphQL con AEM para ofrecer contenido sin encabezado explorando contenido y consultas de muestra.
feature: Headless, Content Fragments,GraphQL API
exl-id: b60fcf97-4736-4606-8b41-4051b8b0c8a7
role: Admin, Developer
source-git-commit: bdf3e0896eee1b3aa6edfc481011f50407835014
workflow-type: tm+mt
source-wordcount: '1826'
ht-degree: 95%

---

# Formación para utilizar GraphQL con AEM: contenido y consultas de muestra {#learn-graphql-with-aem-sample-content-queries}

Aprenda a utilizar GraphQL con AEM para ofrecer contenido sin encabezado explorando contenido y consultas de muestra.

>[!NOTE]
>
>Lea esta página junto con lo siguiente:
>
>* [Fragmentos de contenido](/help/sites-cloud/administering/content-fragments/overview.md)
>* [Modelos de fragmentos de contenido](/help/sites-cloud/administering/content-fragments/content-fragment-models.md)
>* [API de GraphQL de AEM para su uso con fragmentos de contenido](/help/headless/graphql-api/content-fragments.md)

Para empezar a utilizar las consultas de GraphQL y ver cómo funcionan con fragmentos de contenido de AEM, resulta útil ver algunos ejemplos prácticos.

Para ayudarle con esto, consulte lo siguiente:

* Una [estructura de fragmentos de contenido de muestra](#content-fragment-structure-graphql)

* Y algunas [consultas de muestra de GraphQL](#graphql-sample-queries), en función de la estructura de fragmento de contenido de muestra (modelos de fragmentos de contenido y fragmentos de contenido relacionados).

>[!CONTEXTUALHELP]
>id="aemcloud_headless_graphql_sample"
>title="Formación para utilizar GraphQL con AEM: contenido y consultas de muestra"
>abstract="Aprenda a utilizar GraphQL con AEM para ofrecer contenido sin encabezado explorando contenido y consultas de muestra."

## GraphQL: consultas de muestra con la estructura de fragmentos de contenido de muestra {#graphql-sample-queries-sample-content-fragment-structure}

Vea estas consultas de muestra para ver de forma ilustrada la creación de consultas, junto con resultados de muestra.

>[!NOTE]
>
>Según la instancia, puede acceder directamente a la [interfaz de GraphQL incluida con la API de GraphQL de AEM](/help/headless/graphql-api/graphiql-ide.md) para enviar y probar consultas.
>
>Puede acceder al editor de consultas desde:
>
>* **Herramientas** > **General** > **Editor de consultas de GraphQL**
>* directamente; por ejemplo, `http://localhost:4502/aem/graphiql.html`

>[!NOTE]
>
>Las consultas de muestra se basan en la [Estructura de fragmentos de contenido de muestra para usar con GraphQL](#content-fragment-structure-graphql)

### Consulta de muestra: todos los esquemas y tipos de datos disponibles {#sample-all-schemes-datatypes}

Devuelve todos los `types` para todos los esquemas disponibles.

**Consulta de muestra**

```graphql
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

```json
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

### Consulta de muestra: toda la información acerca de todas las ciudades {#sample-all-information-all-cities}

Para recuperar toda la información acerca de todas las ciudades, puede utilizar la consulta básica:
**Consulta de muestra**

```graphql
{
  cityList {
    items
  }
}
```

Cuando se ejecuta, el sistema expande automáticamente la consulta para incluir todos los campos:

```graphql
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

```json
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

### Consulta de muestra: nombres de todas las ciudades {#sample-names-all-cities}

Esta es una consulta directa para devolver el `name` de todas las entradas del esquema `city`.

**Consulta de muestra**

```graphql
query {
  cityList {
    items {
      name
    }
  }
}
```

**Resultados de muestra**

```json
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

### Consulta de muestra: un solo fragmento de ciudad específico {#sample-single-specific-city-fragment}

Esta es una consulta para devolver los detalles de una sola entrada de fragmento en una ubicación específica del repositorio.

**Consulta de muestra**

```graphql
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

```json
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

### Consulta de muestra: todas las ciudades con una variación con nombre {#sample-cities-named-variation}

Si crea una nueva variación, denominada “Centro de Berlín” (`berlin_centre`), para el `city` de Berlín, puede utilizar una consulta para devolver detalles de la variación.

**Consulta de muestra**

```graphql
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

```json
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

### Consulta de muestra: nombres de todas las ciudades etiquetadas como escapadas {#sample-names-all-cities-tagged-city-breaks}

Si:

* crea varias etiquetas, con el nombre `Tourism`: `Business`, `City Break` y `Holiday`
* y las asigna a la variación Principal de varias instancias de `City`

Entonces puede utilizar una consulta para devolver detalles de la `name` y `tags`de todas las entradas etiquetadas como City Breaks en el `city`esquema.

**Consulta de muestra**

```xml
query {
  cityList(
    includeVariations: true,
    filter: {_tags: {_expressions: [{value: "tourism:city-break", _operator: CONTAINS}]}}
  ){
    items {
      name,
      _tags
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
          "name": "Berlin",
          "_tags": [
            "tourism:city-break",
            "tourism:business"
          ]
        },
        {
          "name": "Zurich",
          "_tags": [
            "tourism:city-break",
            "tourism:business"
          ]
        }
      ]
    }
  }
}
```

### Consulta de muestra: detalles completos del CEO y los empleados de una compañía {#sample-full-details-company-ceos-employees}

Utilizando la estructura de los fragmentos anidados, esta consulta devuelve todos los detalles del CEO de una compañía y de todos sus empleados.

**Consulta de muestra**

```graphql
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

```json
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

### Consulta de muestra: todas las personas que tienen el apellido “Jobs” o “Smith” {#sample-all-persons-jobs-smith}

Una consulta que filtra todas las `persons` al buscar cualquiera que tenga el apellido `Jobs`o `Smith`.

**Consulta de muestra**

```graphql
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

```json
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

### Consulta de muestra: todas las personas que no tienen el apellido “Jobs” {#sample-all-persons-not-jobs}

Una consulta que filtra todas las `persons` al buscar cualquiera que tenga el apellido `Jobs` o `Smith`.

**Consulta de muestra**

```graphql
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

```json
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

### Consulta de muestra: todas las aventuras cuya `_path` comienza con un prefijo específico {#sample-wknd-all-adventures-cycling-path-filter}

Todas las `adventures` en que la `_path` comienza con un prefijo específico (`/content/dam/wknd/en/adventures/cycling`).

**Consulta de muestra**

```graphql
query {
  adventureList(
    filter: {
      _path: {
        _expressions: [
        {
          value: "/content/dam/wknd/en/adventures/cycling"
         _operator: STARTS_WITH
        }]
       }
    })
    {
    items {
      _path
    }
  }
}
```

**Resultados de muestra**

```json
{
  "data": {
    "adventureList": {
      "items": [
        {
          "_path": "/content/dam/wknd/en/adventures/cycling-southern-utah/cycling-southern-utah"
        },
        {
          "_path": "/content/dam/wknd/en/adventures/cycling-tuscany/cycling-tuscany"
        }
      ]
    }
  }
}
```

### Consulta de muestra: todas las ciudades situadas en Alemania o Suiza con una población entre 400 000 y 999 999 {#sample-all-cities-d-ch-population}

Aquí se filtra una combinación de campos. Un `AND` (implícito) se utiliza para seleccionar el rango de `population`, mientras que un `OR` (explícito) se utiliza para seleccionar las ciudades requeridas.

**Consulta de muestra**

```graphql
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

```json
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

### Consulta de muestra: todas las ciudades con SAN en el nombre, sin importar las mayúsculas {#sample-all-cities-san-ignore-case}

Esta consulta busca todas las ciudades que tienen `SAN` en el nombre, sin importar las mayúsculas.

**Consulta de muestra**

```graphql
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

```json
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

### Consulta de muestra: filtro en una matriz con un elemento que deba producirse al menos una vez {#sample-array-item-occur-at-least-once}

Esta consulta filtra una matriz con un elemento (`city:na`) que debe producirse al menos una vez.

**Consulta de muestra**

```graphql
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

```json
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

### Consulta de muestra: filtro de un valor de matriz exacto {#sample-array-exact-value}

Esta consulta filtra un valor de matriz exacto.

**Consulta de muestra**

```graphql
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

```json
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

### Consulta de muestra para fragmentos de contenido anidados: todas las compañías que tienen al menos un empleado con el apellido “Smith” {#sample-companies-employee-smith}

Esta consulta ilustra el filtrado para cualquier `person` de `name` “Smith”, que devuelve información de entre dos fragmentos anidados: `company` y `employee`.

**Consulta de muestra**

```graphql
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

```json
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

### Consulta de muestra para fragmentos de contenido anidados: todas las compañías en las que todos los empleados han ganado el premio “Gamestar” {#sample-all-companies-employee-gamestar-award}

Esta consulta ilustra el filtrado entre tres fragmentos anidados: `company`, `employee` y `award`.

**Consulta de muestra**

```graphql
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

```json
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

### Consulta de muestra para metadatos: enumera los metadatos de los premios titulados GB {#sample-metadata-awards-gb}

Esta consulta ilustra el filtrado entre tres fragmentos anidados: `company`, `employee` y `award`.

**Consulta de muestra**

```graphql
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

```json
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

## Consultas de muestra con el proyecto WKND {#sample-queries-using-wknd-project}

Estas consultas de muestra se basan en el proyecto WKND. Cuenta con lo siguiente:

* Modelos de fragmentos de contenido disponibles en:
  `http://<hostname>:<port>/libs/dam/cfm/models/console/content/models.html/conf/wknd`

* Fragmentos de contenido (y otro contenido) disponibles en:
  `http://<hostname>:<port>/assets.html/content/dam/wknd/en`
  `http://<hostname>:<port>/assets.html/content/dam/wknd-shared/en`

>[!NOTE]
>
>Como los resultados pueden ser extensos, no se reproducen aquí.

### Consulta de muestra para todos los fragmentos de contenido de un determinado modelo con las propiedades especificadas {#sample-wknd-all-model-properties}

Esta consulta de muestra busca lo siguiente:

* para todos los fragmentos de contenido del tipo `article`
* con `_path` y propiedades de `authorFragment`.

**Consulta de muestra**

```graphql
{
  articleList {
    items {
      _path
      authorFragment {
        _path
        firstName
        lastName
        birthDay
      }
    }
 }
}
```

### Consulta de muestra para metadatos {#sample-wknd-metadata}

Esta consulta busca lo siguiente:

* para todos los fragmentos de contenido del tipo `adventure`
* metadatos

**Consulta de muestra**

```graphql
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

Esta consulta de muestra busca lo siguiente:

* para un solo fragmento de contenido de tipo `article` en una ruta específica
   * dentro de ese fragmento, todos los formatos de contenido:
      * HTML
      * Markdown
      * Texto sin formato
      * JSON

**Consulta de muestra**

```graphql
{
  articleByPath(_path: "/content/dam/wknd-shared/en/magazine/alaska-adventure/alaskan-adventures") {
    item {
        _path
        authorFragment {
          _path
          firstName
          lastName
          birthDay
        }
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

### Consulta de muestra para un modelo de fragmento de contenido de un modelo {#sample-wknd-content-fragment-model-from-model}

Esta consulta de muestra busca lo siguiente:

* para un solo fragmento de contenido
   * detalles del modelo de fragmento de contenido subyacente

**Consulta de muestra**

```graphql
{
  adventureByPath(_path: "/content/dam/wknd-shared/en/magazine/western-australia/western-australia-by-camper-van") {
    item {
      _path
      title
      _model {
        _path
        title
      }
    }
  }
}
```

### Consulta de muestra para un fragmento de contenido anidado: tipo de modelo único{#sample-wknd-nested-fragment-single-model}

Esta consulta busca lo siguiente:

* para un solo fragmento de contenido de tipo `article` en una ruta específica
   * dentro de ese fragmento, la ruta y el autor del fragmento (anidado) al que se hace referencia

>[!NOTE]
>
>El campo `referencearticle` tiene el tipo de datos `fragment-reference`.

**Consulta de muestra**

```graphql
{
  adventureByPath(_path: "/content/dam/wknd-shared/en/magazine/western-australia/western-australia-by-camper-van") {
    item {
      _path
      title
      _model {
        _path
        title
      }
    }
  }
}
```

### Consulta de muestra para un fragmento de contenido anidado: tipo de modelo múltiple{#sample-wknd-nested-fragment-multiple-model}

#### Tipo de modelo al que se hace referencia única

Esta consulta busca lo siguiente:

* para varios fragmentos de contenido de tipo `bookmark`
   * con Referencias de fragmento a otros fragmentos de tipos de modelo específicos `Article`

>[!NOTE]
>
>El campo `fragments` tiene el Tipo de datos `fragment-reference`, con el modelo `Article` seleccionado. Entregas de consultas `fragments` como una matriz de `[Article]`.

```graphql
{
  bookmarkList {
    items {
        fragments {
          _path
          author
        }
     }
  }
}
```

#### Varios tipos de modelo a los que se hace referencia

Esta consulta busca lo siguiente:

* para varios fragmentos de contenido de tipo `bookmark`
   * con referencias de fragmento a otros fragmentos de tipos de modelo específicos `Article` y `Adventure`

>[!NOTE]
>
>El campo `fragments` tiene el tipo de datos `fragment-reference`, con los modelos `Article` y `Adventure` seleccionados. Entregas de consultas `fragments` como una matriz de `[AllFragmentModels]`, a la que se hace referencia con el tipo de unión.

```graphql
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

### Consulta de muestra para un fragmento de contenido de un modelo específico con referencias de contenido{#sample-wknd-fragment-specific-model-content-reference}

Hay dos tipos de consulta:

1. Para devolver todas las referencias de contenido.
1. Para devolver referencias de contenido específicas del tipo `attachments`.

Estas consultas buscan:

* para varios fragmentos de contenido de tipo `bookmark`
   * con referencias de contenido a otros fragmentos

#### Consulta de muestra para varios fragmentos de contenido con referencias recuperadas previamente {#sample-wknd-multiple-fragments-prefetched-references}

La siguiente consulta devuelve todas las referencias de contenido utilizando `_references`:

<!-- need replacement query -->

```graphql
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
    items {
        _path
    }
  }
}
```

#### Consulta de muestra para varios fragmentos de contenido con archivos adjuntos {#sample-wknd-multiple-fragments-attachments}

La siguiente consulta devuelve todos los `attachments`, un campo específico (subgrupo) del tipo `content-reference`:

>[!NOTE]
>
>El campo `attachments` tiene el tipo de datos `content-reference`, con varios formularios seleccionados.

<!-- need replacement query -->

```graphql
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

### Consulta de muestra para un solo fragmento de contenido con referencia en línea RTE {#sample-wknd-single-fragment-rte-inline-reference}

Esta consulta busca lo siguiente:

* para un solo fragmento de contenido de tipo `bookmark` en una ruta específica
   * dentro de él, referencias en línea RTE

>[!NOTE]
>
>Las referencias en línea RTE se hidratan en `_references`.

<!-- need replacement query -->

**Consulta de muestra**

```graphql
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

### Consulta de muestra para una única variación de fragmento de contenido de un modelo determinado {#sample-wknd-single-fragment-given-model}

Esta consulta busca lo siguiente:

* para un solo fragmento de contenido de tipo `author` en una ruta específica
   * dentro de ese fragmento, los datos relacionados con la variación: `another`

**Consulta de muestra**

```graphql
{
  authorByPath(_path: "/content/dam/wknd-shared/en/contributors/ian-provo", variation: "another") {
    item {
        _path
        _variation
        firstName
        lastName
        birthDay
    }
  }
}
```

### Consulta de muestra para una variación con nombre de varios fragmentos de contenido de un modelo determinado {#sample-wknd-variation-multiple-fragment-given-model}

Esta consulta busca lo siguiente:

* para fragmentos de contenido de tipo `author` con una variación específica: `another`

>[!NOTE]
>
>Esta consulta demuestra la alternativa para los fragmentos de contenido que no tienen una [variación](/help/headless/graphql-api/content-fragments.md#variations) del nombre especificado.

**Consulta de muestra**

```graphql
{
  authorList(variation: "another") {
    items {
        _path
        _variation
        firstName
        lastName
        birthDay
    }
  }
}
```

### Consulta de muestra para varios fragmentos de contenido y sus variaciones de un modelo dado {#sample-wknd-multiple-fragment-variations-given-model}

Esta consulta busca lo siguiente:

* para fragmentos de contenido de tipo `article` y todas las variaciones

**Consulta de muestra**

```xml
query {
  articleList(
    includeVariations: true  ){
    items {
      _variation
      _path
      _tags
      _metadata {
        stringArrayMetadata {
          name
          value
        }
      }
    }
  }
}
```

### Consulta de muestra para variaciones de fragmentos de contenido de un modelo dado que tienen una etiqueta específica adjunta{#sample-wknd-fragment-variations-given-model-specific-tag}

Esta consulta busca lo siguiente:

* para fragmentos de contenido de tipo `article` con una o más variaciones que tiene la etiqueta `WKND : Activity / Hiking`

**Consulta de muestra**

```xml
{
  articleList(
    includeVariations: true,
    filter: {_tags: {_expressions: [{value: "wknd:activity/hiking", _operator: CONTAINS}]}}
  ){
    items {
      _variation
      _path
      _tags
      _metadata {
        stringArrayMetadata {
          name
          value
        }
      }
    }
  }
}
```

### Consulta de muestra para varios fragmentos de contenido de una configuración regional determinada {#sample-wknd-multiple-fragments-given-locale}

Esta consulta busca lo siguiente:

* para fragmentos de contenido de tipo `article` dentro de la configuración regional `fr`

**Consulta de muestra**

```graphql
{ 
  articleList(_locale: "fr") {
    items {
      _path
      authorFragment {
        _path
        firstName
        lastName
        birthDay
      }
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

### Ejemplo de consulta de lista con desplazamiento y límite {#sample-list-offset-limit}

Esta consulta busca lo siguiente:

* para la página de resultados que contienen hasta cinco artículos, a partir del quinto artículo de la lista de resultados *completa*

**Consulta de muestra**

```graphql
{
   articleList(offset: 5, limit: 5) {
    items {
      authorFragment {
        _path
        firstName
        lastName
        birthDay
      }
      _path
    }
  }
}
```

### Ejemplo de consulta de paginación que utiliza primero y después  {#sample-pagination-first-after}

Esta consulta busca lo siguiente:

* para la página de resultados que contiene hasta cinco aventuras, empezando por el elemento de cursor dado en la lista de resultados *completa*:

**Consulta de muestra**

```graphql
{
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

### Consulta de muestra con filtrado por ID de _tags y excluyendo variaciones {#sample-filtering-tag-not-variations}

Esta consulta busca lo siguiente:

* para fragmentos de contenido de tipo `vehicle` tener la etiqueta `big-block`
* exclusión de variaciones

**Consulta de muestra**

```graphql
query {
  vehicleList(
    filter: {
    _tags: {
      _expressions: [
        {
          value: "vehicles:big-block"
          _operator: CONTAINS
        }
      ]
    }
  }) {
    items {
      _variation
      _path
      type
      name
      model
      fuel
      _tags
    }
  }
} 
```

### Consulta de muestra con filtrado por ID de _tags e incluyendo variaciones {#sample-filtering-tag-with-variations}

Esta consulta busca lo siguiente:

* para fragmentos de contenido de tipo `vehicle` tener la etiqueta `big-block`
* incluyendo variaciones

**Consulta de muestra**

```graphql
{
  enginePaginated(after: "SjkKNmVkODFmMGQtNTQyYy00NmQ4LTljMzktMjhlNzQwZTY1YWI2Cmo5", first: 9 ,includeVariations:true, sort: "name",
    filter: {
    _tags: {
      _expressions: [
        {
          value: "vehicles:big-block"
          _operator: CONTAINS
        }
      ]
    }
  }) {
    edges{
    node {
        _variation
        _path
        name
        type
        size
        _tags
        _metadata {
          stringArrayMetadata {
            name
            value
          }
        }
    }
      cursor
    }
  }
} 
```

## Consultas de muestra para la entrega de DAM y Dynamic Media Assets {#sample-queries-delivery-DAM-DM}

Para la entrega de imágenes optimizadas para la web (de recursos DAM):

* [Consulta de muestra para entrega de imágenes optimizadas para la web con parámetros completos](/help/headless/graphql-api/content-fragments.md#web-optimized-image-delivery-full-parameters)

* [Consulta de muestra para entrega de imágenes optimizadas para la web con un solo parámetro especificado](/help/headless/graphql-api/content-fragments.md#web-optimized-image-delivery-single-query-variable)

Para la entrega de la URL a un recurso de Dynamic Media

* Ver [Consulta de muestra para la entrega de recursos de Dynamic Media por dirección URL: referencia de imagen](/help/headless/graphql-api/content-fragments.md#sample-query-dynamic-media-asset-delivery-by-url-imageref)

* Ver [Consulta de muestra para la entrega de recursos de Dynamic Media por dirección URL: varias referencias](/help/headless/graphql-api/content-fragments.md#sample-query-dynamic-media-asset-delivery-by-url-multiple-refs)

## La estructura del fragmento de contenido de muestra (utilizada con GraphQL) {#content-fragment-structure-graphql}

Las consultas de muestra se basan en la siguiente estructura, que utiliza:

* Uno o más [Modelos de fragmentos de contenido de muestra](#sample-content-fragment-models-schemas) forman la base de los esquemas de GraphQL

* [Fragmentos de contenido de muestra](#sample-content-fragments) basados en los modelos anteriores

### Modelos de fragmentos de contenido de muestra (esquemas) {#sample-content-fragment-models-schemas}

Para las consultas de muestra, se utilizan los siguientes modelos de contenido y sus interrelaciones (referencias ->):

* [Compañía](#model-company)
-> [Persona](#model-person)
-> [Premio](#model-award)

* [Ciudad](#model-city)

#### Compañía {#model-company}

Los campos básicos que definen a la compañía son los siguientes:

| Nombre del campo | Tipo de datos | Referencia |
|--- |--- |--- |
| Nombre de la compañía | Texto de una sola línea | |
| CEO | Referencia de fragmento (único) | [Persona](#model-person) |
| Empleados | Referencia de fragmento (multicampo) | [Persona](#model-person) |

#### Persona {#model-person}

Los campos que definen a una persona, que también puede ser un empleado:

| Nombre del campo | Tipo de datos | Referencia |
|--- |--- |--- |
| Nombre | Texto de una sola línea | |
| Nombre | Texto de una sola línea | |
| Premios | Referencia de fragmento (multicampo) | [Premio](#model-award) |

#### Premio {#model-award}

Los campos que definen un premio son los siguientes:

| Nombre del campo | Tipo de datos | Referencia |
|--- |--- |--- |
| Método abreviado/ID | Texto de una sola línea | |
| Título | Texto de una sola línea | |

#### Ciudad {#model-city}

Los campos para definir una ciudad son los siguientes:

| Nombre del campo | Tipo de datos | Referencia |
|--- |--- |--- |
| Nombre | Texto de una sola línea | |
| País | Texto de una sola línea | |
| Población | Número | |
| Categorías | Etiquetas | |

### Fragmentos de contenido de muestra {#sample-content-fragments}

Los siguientes fragmentos se utilizan para el modelo adecuado.

#### Compañía {#fragment-company}

| Nombre de la compañía | CEO | Empleados |
|--- |--- |--- |
| Apple | Steve Jobs | Duke Marsh<br>Max Caulfield |
| Little Pony Inc. | Adam Smith | Lara Croft<br>Cutter Slade |
| NextStep Inc. | Steve Jobs | Joe Smith<br>Abe Lincoln |

#### Persona {#fragment-person}

| Nombre | Nombre | Premios |
|--- |--- |--- |
| Lincoln | Abe | |
| Smith | Adam | |
| Enclavado | Cutter | Gameblitz<br>Gamestar |
| Marsh | Duke | |
| Smith | Joe | |
| Croft | Lara | Gamestar |
| Caulfield | Max | Gameblitz |
| Trabajos | Steve | |

#### Premio {#fragment-award}

| Método abreviado/ID | Título |
|--- |--- |
| GB | Gameblitz |
| GS | Gamestar |
| OSC | Oscar |

#### Ciudad {#fragment-city}

| Nombre | País | Población | Categorías |
|--- |--- |--- |--- |
| Basilea | Suiza | 172258 | city:emea |
| Berlín | Alemania | 3669491 | city:capital<br>city:emea |
| Bucarest | Rumanía | 1821000 | city:capital<br>city:emea |
| San Francisco | EE. UU. | 883306 | city:beach<br>city:na |
| San José | EE. UU. | 102635 | city:na |
| Stuttgart | Alemania | 634830 | city:emea |
| Zúrich | Suiza | 415367 | city:capital<br>city:emea |
