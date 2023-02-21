---
title: Optimización de consultas de GraphQL
description: Aprenda a optimizar las consultas de GraphQL al filtrar, empaquetar y ordenar los fragmentos de contenido en Adobe Experience Manager as a Cloud Service para la entrega de contenido sin encabezado.
source-git-commit: 0fe0bd301fb09cdc631878926f2e40df51a2cc23
workflow-type: tm+mt
source-wordcount: '1192'
ht-degree: 0%

---


# Optimización de consultas de GraphQL {#optimizing-graphql-queries}

>[!NOTE]
>
>Antes de aplicar estas recomendaciones de optimización, considere [Actualización de los fragmentos de contenido para paginación y ordenación en el filtrado de GraphQL](/help/headless/graphql-api/graphql-optimized-filtering-content-update.md) para obtener el mejor rendimiento.

En una instancia de AEM con un número elevado de fragmentos de contenido que comparten el mismo modelo, las consultas de listas de GraphQL pueden resultar costosas (en términos de recursos).

Esto se debe a que *all* los fragmentos que comparten un modelo utilizado en la consulta de GraphQL deben cargarse en la memoria. Esto consume tiempo y memoria. El filtrado, que puede reducir el número de elementos del conjunto de resultados (final), solo se puede aplicar **after** cargando todo el conjunto de resultados en la memoria.

Esto puede dar la impresión de que incluso los conjuntos de resultados pequeños (pueden) dar lugar a un rendimiento incorrecto. Sin embargo, en realidad la lentitud es causada por el tamaño del conjunto de resultados inicial, ya que debe gestionarse internamente antes de poder aplicar el filtrado.

Para reducir los problemas de rendimiento y memoria, este conjunto de resultados inicial debe mantenerse lo más pequeño posible.

AEM ofrece dos métodos para optimizar las consultas de GraphQL:

* [Filtro híbrido](#hybrid-filtering)
* [Paginación](#paging) (o paginación)

   * [Ordenar](#sorting) no está directamente relacionado con la optimización, pero está relacionado con la paginación

Cada enfoque tiene sus propios casos de uso y limitaciones. Este documento proporciona información sobre el filtrado y paginación híbridos, con algunos [prácticas recomendadas](#best-practices) para optimizar las consultas de GraphQL.

## Filtro híbrido {#hybrid-filtering}

El filtrado híbrido combina el filtrado JCR con el filtrado AEM.

Aplica un filtro JCR (en forma de restricción de consulta) antes de cargar el conjunto de resultados en la memoria para AEM filtrado. Esto es para reducir el conjunto de resultados cargado en la memoria, ya que el filtro JCR elimina los resultados superfluos antes de esto.

>[!NOTE]
>
>Por motivos técnicos (por ejemplo, flexibilidad, anidación de fragmentos), AEM no puede delegar todo el filtrado a JCR.

Esta técnica mantiene la flexibilidad que proporcionan los filtros de GraphQL, al tiempo que delega la mayor cantidad posible de filtros en JCR.

## Paginación {#paging}

GraphQL en AEM es compatible con dos tipos de paginación:

* [paginación basada en límites/desvíos](/help/headless/graphql-api/content-fragments.md#list-offset-limit)
Se utiliza para consultas de lista; estos terminan con 
`List`; por ejemplo, `articleList`.
Para utilizarla, debe proporcionar la posición del primer elemento que se va a devolver (la variable `offset`) y el número de elementos que se van a devolver (la variable `limit`o tamaño de página).

* [paginación basada en el cursor](/help/headless/graphql-api/content-fragments.md#paginated-first-after) (representado por `first`y `after`) Proporciona un identificador único para cada elemento; también se conoce como cursor.
En la consulta, se especifica el cursor del último elemento de la página anterior, además del tamaño de la página (el número máximo de elementos que se van a devolver).

   Como la paginación basada en el cursor no se ajusta a las estructuras de datos de las consultas basadas en listas, AEM ha introducido `Paginated` tipo de consulta; por ejemplo, `articlePaginated`. Las estructuras de datos y los parámetros utilizados siguen la [Especificación de conexión del cursor de GraphQL](https://relay.dev/graphql/connections.htm).

   >[!NOTE]
   >
   >AEM admite actualmente la paginación hacia adelante (con `after`/`first` parámetros).
   >
   >Paginación hacia atrás (mediante `before`/`last` parámetros) no es compatible.

## Ordenación {#sorting}

La ordenación solo puede ser eficaz si todos los criterios de ordenación están relacionados con fragmentos de nivel superior.

Si el orden de clasificación incluye uno o más campos ubicados en un fragmento anidado, todos los fragmentos que compartan el modelo de nivel superior deben cargarse en la memoria. Esto causa un impacto negativo en el rendimiento.

>[!NOTE]
>
>La ordenación en campos de nivel superior también tiene un impacto (aunque pequeño) en el rendimiento.

## Prácticas recomendadas {#best-practices}

El objetivo principal de todas las optimizaciones es reducir el conjunto de resultados inicial. Las prácticas recomendadas que se enumeran aquí ofrecen formas de hacerlo. Pueden (y deben) combinarse.

### Filtrar solo en propiedades de nivel superior {#filter-top-level-properties-only}

Actualmente, el filtrado en el nivel JCR solo funciona para fragmentos de nivel superior.

Si un filtro se dirige a los campos de un fragmento anidado, AEM debe volver a cargar (en la memoria) todos los fragmentos que comparten el modelo subyacente.

Puede optimizar dichas consultas de GraphQL combinando expresiones de filtro en campos de fragmentos de nivel superior y los de campos de fragmentos anidados con el [operador AND](#logical-operations-in-filter-expressions).

### Usar la estructura de contenido {#use-content-structure}

En AEM, generalmente se considera una buena práctica utilizar la estructura del repositorio para reducir el alcance del contenido que se va a procesar.

Este método también debe aplicarse a las consultas de GraphQL.

Esto se puede hacer aplicando un filtro a la variable `_path` del fragmento de nivel superior:

```graphql
{
  someList(filter: {
    _path: {
      _expressions: [ 
        {
          value: "/content/dam/some/sub/path/",
          _operator: STARTS_WITH
        }
      ]
    }
  }) {
    items {
      # ...
    }
  }
}
```

>[!NOTE]
>
>La `/` en `value` para obtener el mejor rendimiento.

### Uso de paginación {#use-paging}

También puede utilizar la paginación para reducir el conjunto de resultados inicial; especialmente si las solicitudes no utilizan ningún filtro y clasificación.

Si filtra u ordena los fragmentos anidados, las consultas paginadas pueden seguir siendo lentas, ya AEM puede que tenga que cargar grandes cantidades de fragmentos en la memoria. Por lo tanto, si combina el filtrado y la paginación, tenga en cuenta las reglas de filtrado (como se ha mencionado anteriormente).

Para la paginación, la ordenación es igual de importante, ya que los resultados paginados siempre se ordenan, ya sea de forma explícita o implícita.

Si le interesa principalmente recuperar las primeras páginas, no hay diferencia significativa entre usar la variable `...List` o `...Paginated` consultas. Sin embargo, si su aplicación está interesada en leer más de una o dos páginas, debe tener en cuenta la `...Paginated` , ya que ofrece un mejor rendimiento con las páginas posteriores.

### Operaciones lógicas en expresiones de filtro {#logical-operations-in-filter-expressions}

Si está filtrando en fragmentos anidados, aún puede aprovechar el filtrado JCR proporcionando un filtro de acompañamiento en un campo de nivel superior que se combina utilizando la variable `AND` operador.

Un caso de uso típico sería restringir el ámbito de la consulta mediante un filtro en la variable `_path` del fragmento de nivel superior y, a continuación, filtre los campos adicionales que puedan estar en el nivel superior o en un fragmento anidado.

En este caso, las diferentes expresiones de filtro se combinarían con `AND`. Por lo tanto, el filtro de `_path` puede limitar efectivamente el conjunto de resultados inicial. Todos los demás filtros de los campos de nivel superior también pueden ayudar a reducir el conjunto de resultados inicial, siempre y cuando se combinen con `AND`.

Filtrar expresiones combinadas con `OR` no se puede optimizar si hay fragmentos anidados implicados. `OR` las expresiones solo se pueden optimizar si *no* están implicados los fragmentos anidados.

### Evitar el filtrado en campos de texto multilínea {#avoid-filtering-multiline-textfields}

Los campos de un campo de texto multilínea (html, markdown, texto sin formato, json) no se pueden filtrar mediante una consulta JCR, ya que el contenido de estos campos debe calcularse sobre la marcha.

Si todavía necesita filtrar en un campo de texto multilínea, considere la posibilidad de limitar el tamaño del conjunto de resultados inicial añadiendo expresiones de filtro adicionales y combinándolas con `AND`. Limitación del ámbito mediante el filtrado en la variable `_path` field también es un buen enfoque.

### Evitar el filtrado en campos virtuales {#avoid-filtering-virtual-fields}

Campos virtuales (la mayoría de los campos comienzan con `_`) se calculan mientras se ejecuta una consulta de GraphQL y, por lo tanto, están fuera del ámbito del filtrado basado en JCR.

Una excepción importante es la `_path` , que se puede utilizar de forma eficaz para reducir el tamaño del conjunto de resultados inicial, si el contenido está estructurado en consecuencia (consulte [Usar la estructura de contenido](#use-content-structure)).

### Filtrado: Exclusiones {#filtering-exclusions}

Hay otras situaciones en las que una expresión de filtro no se puede evaluar en el nivel JCR (y por lo tanto debe evitarse para lograr el mejor rendimiento):

* Filtrado de expresiones en un `Float` que utilizan la variable `_sensitiveness` opción de filtro y donde `_sensitiveness` se configura en cualquier valor que no sea `0.0` .

* Filtrado de expresiones en un `String` usando la variable `_ignoreCase` filtro .

* Filtrado en `null` valores.

* Filtros en matrices con `_apply: ALL_OR_EMPTY`.

* Filtros en matrices con `_apply: INSTANCES`, `_instances: 0`.

* Filtre expresiones utilizando la variable `CONTAINS_NOT` operador.

* Filtrado de expresiones en un `Calendar`, `Date` o `Time` que utilizan la variable `NOT_AT` operador.
