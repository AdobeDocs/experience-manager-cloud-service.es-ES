---
title: Optimización de consultas de GraphQL
description: Aprenda a optimizar las consultas de GraphQL al filtrar, paginar y ordenar los fragmentos de contenido en Adobe Experience Manager as a Cloud Service para la entrega de contenido sin encabezado.
exl-id: 67aec373-4e1c-4afb-9c3f-a70e463118de
feature: Headless, Content Fragments,GraphQL API
role: Admin, Developer
source-git-commit: bdf3e0896eee1b3aa6edfc481011f50407835014
workflow-type: tm+mt
source-wordcount: '1874'
ht-degree: 64%

---

# Optimización de consultas de GraphQL {#optimizing-graphql-queries}

>[!NOTE]
>
>Antes de aplicar estas recomendaciones de optimización, considere lo siguiente [Actualización de los fragmentos de contenido para paginación y ordenación en el filtrado de GraphQL](/help/headless/graphql-api/graphql-optimized-filtering-content-update.md) para obtener el mejor rendimiento.

Estas directrices se proporcionan para ayudar a evitar problemas de rendimiento con las consultas de GraphQL.

## GraphQL Checklist {#graphql-checklist}

La siguiente lista de comprobación tiene como objetivo ayudarle a optimizar la configuración y el uso de GraphQL en Adobe Experience Manager AEM () as a Cloud Service.

### Primeros principios {#first-principles}

#### Uso de consultas de GraphQL persistentes {#use-persisted-graphql-queries}

**Recomendación**

Se recomienda encarecidamente el uso de consultas GraphQL persistentes.

Las consultas persistentes de GraphQL ayudan a reducir el rendimiento de la ejecución de consultas mediante la red de entrega de contenido (CDN). Las aplicaciones cliente solicitan consultas persistentes con solicitudes de GET para la ejecución rápida habilitada para Edge.

**Referencia adicional**

Consulte:

* [Consultas persistentes de GraphQL](/help/headless/graphql-api/persisted-queries.md).
* [Formación para utilizar GraphQL con AEM: contenido y consultas de muestra](/help/headless/graphql-api/sample-queries.md)

### Estrategia de caché {#cache-strategy}

También se pueden utilizar varios métodos de almacenamiento en caché para la optimización.

#### AEM Habilitar almacenamiento en caché de Dispatcher {#enable-aem-dispatcher-caching}

**Recomendación**

AEM [Dispatcher AEM](/help/implementing/dispatcher/overview.md) es la caché de primer nivel dentro del servicio de la, antes de la caché de la red de distribución de contenido (CDN).

**Referencia adicional**

Consulte:

* [Consultas persistentes de GraphQL: habilitar el almacenamiento en caché en Dispatcher](/help/headless/deployment/dispatcher-caching.md)

#### Uso de una red de distribución de contenido (CDN) {#use-cdn}

**Recomendación**

Las consultas GraphQL y sus respuestas JSON se pueden almacenar en caché si se dirigen como `GET` solicitudes al utilizar una CDN. Por el contrario, las solicitudes sin almacenar en caché pueden ser muy (recursos) costosas y lentas de procesar, con el potencial de tener más efectos perjudiciales en los recursos del origen.

**Referencia adicional**

Consulte:

* [CDN en AEM as a Cloud Service](/help/implementing/dispatcher/cdn.md)

#### Establecer encabezados de control de caché HTTP {#set-http-cache-control-headers}

**Recomendación**

Cuando se utilizan consultas GraphQL persistentes con una CDN, se recomienda establecer los encabezados de control de caché HTTP adecuados.

Cada consulta persistente puede tener su propio conjunto específico de encabezados de control de caché. Los encabezados se pueden establecer a través de la [API de GraphQL AEM](/help/headless/graphql-api/content-fragments.md) o el [IDE de GraphiQL de](/help/headless/graphql-api/graphiql-ide.md).

**Referencia adicional**

Consulte:

* [Almacenamiento en caché de las consultas persistentes](/help/headless/graphql-api/persisted-queries.md#caching-persisted-queries)
* [Administración de la caché para las consultas persistentes](/help/headless/graphql-api/graphiql-ide.md#managing-cache)

#### AEM Usar el almacenamiento en caché previo de GraphQL {#use-aem-graphql-pre-caching}

**Recomendación**

AEM Esta capacidad permite a los usuarios almacenar en caché contenido adicional dentro del ámbito de las consultas de GraphQL que luego se pueden ensamblar como bloques en la salida JSON en lugar de línea a línea.

**Referencia adicional**

Póngase en contacto con el Adobe para habilitar esta capacidad para su programa y entornos de AEM Cloud Service.

### Optimización de consultas de GraphQL {#graphql-query-optimization}

En una instancia de AEM con un número elevado de fragmentos de contenido que comparten el mismo modelo, las consultas de lista de GraphQL pueden resultar costosas (en términos de recursos).

Esto se debe a que *todos* los fragmentos que comparten un modelo que se utiliza en la consulta de GraphQL deben cargarse en la memoria. Esto consume tiempo y memoria. El filtrado, que puede reducir el número de elementos en el conjunto de resultados (final), solo se puede aplicar **después** cargando todo el conjunto de resultados en la memoria.

Esto puede dar la impresión de que incluso los conjuntos de resultados pequeños (pueden) dar lugar a un mal rendimiento. Sin embargo, en realidad la lentitud está causada por el tamaño del conjunto de resultados inicial, ya que debe manejarse internamente antes de aplicar el filtrado.

Para reducir los problemas de rendimiento y memoria, este conjunto de resultados inicial debe mantenerse lo más pequeño posible.

AEM proporciona dos métodos para optimizar las consultas de GraphQL:

* [Filtrado híbrido](#use-aem-graphql-hybrid-filtering)
* [Paginación](#use-aem-graphql-pagination)

   * [Ordenación](#use-graphql-sorting) no está directamente relacionada con la optimización, pero sí con la paginación

Cada método tiene sus propios casos de uso y limitaciones. Esta sección proporciona información sobre el filtrado y la paginación híbridos, junto con algunas de las [prácticas recomendadas](#best-practices) para su uso en la optimización de consultas de GraphQL.

#### AEM Usar filtrado híbrido de GraphQL {#use-aem-graphql-hybrid-filtering}

**Recomendación**

El filtrado híbrido combina el filtrado de JCR con el filtrado de AEM.

Aplica un filtro de JCR (en forma de restricción de consulta) antes de cargar el conjunto de resultados en la memoria para el filtrado de AEM. Esto sirve para reducir el conjunto de resultados cargado en la memoria, ya que el filtro de JCR elimina los resultados superfluos anteriores a este.

>[!NOTE]
>
>Por motivos técnicos (por ejemplo, flexibilidad, anidación de fragmentos), AEM no puede delegar todo el filtrado a JCR.

Esta técnica mantiene la flexibilidad que proporcionan los filtros de GraphQL, al tiempo que delega la mayor parte posible del filtrado a JCR.

>[!NOTE]
>
>AEM El filtrado híbrido requiere la actualización de fragmentos de contenido existentes

**Referencia adicional**

Consulte:

* [Actualización de los fragmentos de contenido para paginación y ordenación en el filtrado de GraphQL](/help/headless/graphql-api/graphql-optimized-filtering-content-update.md)
* [Consulta de muestra con filtrado por ID de _tags y excluyendo variaciones](/help/headless/graphql-api/sample-queries.md#sample-filtering-tag-not-variations)

#### Usar paginación de GraphQL {#use-aem-graphql-pagination}

**Recomendación**

El tiempo de respuesta de las consultas complejas, con grandes conjuntos de resultados, se puede mejorar segmentando las respuestas en fragmentos mediante paginación, un estándar de GraphQL.

GraphQL en AEM ofrece compatibilidad con dos tipos de paginación:

* [paginación basada en límite/desplazamiento](/help/headless/graphql-api/content-fragments.md#list-offset-limit)
Se usa para consultas de lista; terminan con `List`; por ejemplo, `articleList`.
Para utilizarlo, debe proporcionar la posición del primer elemento que se va a devolver (la variable `offset`) y el número de elementos que se van a devolver (la variable `limit`, o tamaño de página).

* [paginación basada en cursor](/help/headless/graphql-api/content-fragments.md#paginated-first-after) (representada por `first`y `after`)
Proporciona un ID único para cada elemento, también conocido como cursor.
En la consulta, se especifica el cursor del último elemento de la página anterior, además del tamaño de página (el número máximo de elementos que se van a devolver).

  Como la paginación basada en cursor no se ajusta a las estructuras de datos de las consultas basadas en listas, AEM ha introducido el tipo de consulta `Paginated`; por ejemplo, `articlePaginated`. Las estructuras de datos y los parámetros utilizados siguen la [Especificación de conexión del cursor de GraphQL](https://relay.dev/graphql/connections.htm).

  >[!NOTE]
  >
  >Actualmente, AEM admite la paginación de reenvío (utilizando los parámetros `after`/`first`).
  >
  >La paginación hacia atrás (utilizando los parámetros `before`/`last`) no es compatible.

**Referencia adicional**

Consulte:

* [Ejemplo de consulta de paginación que utiliza primero y después](/help/headless/graphql-api/sample-queries.md#sample-pagination-first-after)

#### Usar la ordenación de GraphQL {#use-graphql-sorting}

**Recomendación**

Además de ser un estándar de GraphQL, la ordenación permite a los clientes recibir contenido JSON en orden. Esto puede reducir la necesidad de un procesamiento adicional en el cliente.

La ordenación solo puede ser eficaz si todos los criterios de ordenación están relacionados con fragmentos de nivel superior.

Si el orden de clasificación incluye uno o más campos ubicados en un fragmento anidado, todos los fragmentos que compartan el modelo de nivel superior deben cargarse en la memoria. Esto causa un impacto negativo en el rendimiento.

>[!NOTE]
>
>La ordenación en campos de nivel superior también tiene un impacto (aunque pequeño) en el rendimiento.

**Referencia adicional**

Consulte:

* [Consulta de muestra con filtrado por ID de _etiquetas y excluyendo variaciones, y ordenación por nombre](/help/headless/graphql-api/sample-queries.md#sample-filtering-tag-not-variations)

## Prácticas recomendadas {#best-practices}

El objetivo principal de todas las recomendaciones de optimización es reducir el conjunto de resultados inicial. Las prácticas recomendadas enumeradas aquí proporcionan formas de hacerlo. Pueden (y deben) combinarse.

### Filtrar solo por propiedades de nivel superior {#filter-top-level-properties-only}

Actualmente, el filtrado en el nivel JCR solo funciona para fragmentos de nivel superior.

Si un filtro se dirige a los campos de un fragmento anidado, AEM tiene que volver a cargar (en memoria) todos los fragmentos que comparten el modelo subyacente.

Puede seguir optimizando estas consultas de GraphQL combinando expresiones de filtro en campos de fragmentos de nivel superior y aquellos en campos de fragmentos anidados con la variable [AND operator](#logical-operations-in-filter-expressions).

### Uso de la estructura de contenido {#use-content-structure}

En general, en AEM se considera una buena práctica utilizar la estructura del repositorio para reducir el ámbito de contenido que se va a procesar.

Este método también debe aplicarse a las consultas de GraphQL.

Esto se puede hacer aplicando un filtro en el campo `_path` del fragmento de nivel superior:

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
>El final `/` en `value` es obligatorio para lograr el mejor rendimiento.

### Usar paginación {#use-paging}

También puede utilizar la paginación para reducir el conjunto de resultados inicial, sobre todo si las solicitudes no utilizan ningún filtro ni ordenación.

Si filtra u ordena por fragmentos anidados, las consultas paginadas pueden seguir siendo lentas, ya que es posible que AEM aún tenga que cargar cantidades mayores de fragmentos en la memoria. Por lo tanto, si combina filtrado y paginación, tenga en cuenta las reglas de filtrado (como se ha mencionado anteriormente).

Para la paginación, la ordenación es igualmente importante, ya que los resultados paginados siempre se ordenan, ya sea de forma explícita o implícita.

Si le interesa principalmente recuperar solo las primeras páginas, no hay ninguna diferencia significativa entre el uso de consultas `...List` o `...Paginated`. Sin embargo, si a la aplicación le interesa leer más de una o dos páginas, debe tener en cuenta la consulta `...Paginated`, ya que tiene un rendimiento notablemente mejor con las páginas posteriores.

### Operaciones lógicas en expresiones de filtro {#logical-operations-in-filter-expressions}

Si está filtrando en fragmentos anidados, aún puede aplicar el filtrado JCR proporcionando un filtro complementario en un campo de nivel superior que se combina con el operador `AND`.

Un caso de uso típico sería restringir el alcance de la consulta utilizando un filtro en el campo `_path` del fragmento de nivel superior y, a continuación, filtrar en campos adicionales que podrían estar en el nivel superior o en un fragmento anidado.

En este caso, las diferentes expresiones de filtro se combinarían con `AND`. Por lo tanto, el filtro de `_path` puede limitar de forma efectiva el conjunto de resultados inicial. El resto de filtros de los campos de nivel superior también pueden ayudar a reducir el conjunto de resultados inicial, siempre y cuando se combinen con `AND`.

Filtrar expresiones combinadas con `OR` no se puede optimizar si hay fragmentos anidados implicados. Las expresiones `OR` solo se pueden optimizar si *no* están implicados fragmentos anidados.

### Evitar filtrar los campos de texto multilínea {#avoid-filtering-multiline-textfields}

Los campos de un campo de texto multilínea (html, markdown, plaintext, json) no se pueden filtrar a través de una consulta JCR, ya que su contenido debe calcularse sobre la marcha.

Si aun así necesita filtrar por un campo de texto multilínea, considere la posibilidad de limitar el tamaño del conjunto de resultados inicial añadiendo expresiones de filtro adicionales y combinándolas con `AND`. Limitar el ámbito mediante el filtrado en el campo `_path` también es un buen enfoque.

### Evitar el filtrado en campos virtuales {#avoid-filtering-virtual-fields}

Los campos virtuales (la mayoría de los campos que comienzan por `_`) se calculan mientras se ejecuta una consulta de GraphQL y, por lo tanto, están fuera del ámbito del filtrado basado en JCR.

Una excepción importante es el campo `_path`, que se puede utilizar de forma eficaz para reducir el tamaño del conjunto de resultados inicial: si el contenido está estructurado en consecuencia (consulte [Uso de la estructura de contenido](#use-content-structure)).

### Filtrado: exclusiones {#filtering-exclusions}

Hay otras varias situaciones en las que una expresión de filtro no se puede evaluar en el nivel JCR (y, por lo tanto, debe evitarse para lograr el mejor rendimiento):

* Filtrado de expresiones en un valor `Float` que usa la opción de filtro `_sensitiveness`, y donde `_sensitiveness` se establece en cualquier elemento que no sea `0.0`.

* Filtrado de expresiones en un valor `String` mediante la opción de filtro `_ignoreCase`.

* Filtrado en valores `null`.

* Filtros en matrices con `_apply: ALL_OR_EMPTY`.

* Filtros en matrices con `_apply: INSTANCES`, `_instances: 0`.

* Filtrado de expresiones mediante el operador `CONTAINS_NOT`.

* Filtrado de expresiones en un `Calendar`, `Date` u `Time` que utilizan el operador `NOT_AT`.

### Minimizar el anidamiento de fragmentos de contenido {#minimize-content-fragment-nesting}

Anidar fragmentos de contenido es una buena manera de modelar estructuras de contenido personalizadas. Incluso puede tener un fragmento con un fragmento anidado, que también tenga un fragmento anidado, que tenga... etc.

Sin embargo, la creación de una estructura con demasiados niveles puede aumentar los tiempos de procesamiento de una consulta GraphQL, ya que GraphQL debe atravesar toda la jerarquía de todos los fragmentos de contenido anidados.

El anidamiento profundo también puede tener efectos adversos en la gobernanza del contenido. En general, se recomienda limitar el anidamiento de fragmentos de contenido a menos de cinco o seis niveles.

### No generar todos los formatos (elementos de texto multilínea) {#do-not-output-all-formats}

AEM GraphQL puede devolver texto creado en el tipo de datos **[Texto de varias líneas](/help/sites-cloud/administering/content-fragments/content-fragment-models.md#data-types)** en varios formatos: Texto enriquecido, Texto simple y Markdown.

La salida de los tres formatos aumenta el tamaño de la salida de texto en JSON en un factor de tres. Esto, combinado con conjuntos de resultados generalmente grandes de consultas muy amplias, puede producir respuestas JSON muy grandes que, por lo tanto, tardan mucho tiempo en calcularse. Es mejor limitar la salida solo a los formatos de texto necesarios para procesar el contenido.

### Modificación de fragmentos de contenido {#modifying-content-fragments}

AEM Modifique únicamente los fragmentos de contenido y sus recursos mediante la interfaz de usuario o las API de. No realice modificaciones directamente en JCR.

### Prueba de consultas {#test-your-queries}

Procesar consultas de GraphQL GET es similar a procesar consultas de búsqueda, y es significativamente más complejo que las solicitudes de API simples de todo el contenido.

Planificar, probar y optimizar cuidadosamente las consultas en un entorno controlado que no sea de producción es clave para el éxito posterior cuando se utiliza en producción.
