---
title: Creación de plantillas de visualización para fragmentos de contenido
description: Vista previa y publicación de fragmentos de contenido con plantillas de visualización. Descubra cómo puede crear y personalizar las plantillas.
feature: Developing, Content Fragments
role: Admin, Developer
source-git-commit: 9ad53c41534c552f485a2d57d3c81c270180dfaf
workflow-type: tm+mt
source-wordcount: '2142'
ht-degree: 3%

---

# Fragmentos de contenido visual: plantillas {#visual-content-fragments-templates}

En Adobe Experience Manager (AEM) as a Cloud Service, las plantillas de HTML se pueden utilizar para visualizar fragmentos de contenido y entregarlos en formato HTML.

<!-- CQDOC-23232 - remove when GA -->

>[!NOTE]
>
>Los fragmentos de contenido visual y el trabajo de Figma en fragmentos de contenido visuales están actualmente en disponibilidad limitada.
>
>Si desea participar, envíe una solicitud desde su dirección de correo electrónico oficial a [experience-production-agent@adobe.com](mailto:experience-production-agent@adobe.com).

Las plantillas de HTML permiten controlar cómo se muestran los fragmentos de contenido. Puede crear plantillas de HTML en el editor de código que elija, luego cargarlas y asignarlas a modelos de fragmentos de contenido en AEM.  Los marcadores de posición de contenido que utilizan Handlebars.js permiten asignar la plantilla a tipos de datos en el modelo de fragmento de contenido. Una vez asignada a un modelo, una plantilla está disponible para utilizarse con cualquier fragmento de contenido basado en el modelo, para visualizar el fragmento o para enviarlo como una experiencia modular en formato HTML a cualquier canal, por ejemplo web, correo electrónico, aplicación móvil u otros.

Este artículo explica cómo crear plantillas de HTML personalizadas con sintaxis de Handlebars para procesar fragmentos de contenido visual.

Después de crear las plantillas, puede hacer lo siguiente:

* [Uso de las plantillas en AEM](#using-a-content-fragment-html-template-in-aem)

* Use la [URL de publicación de sus fragmentos de contenido visual](#using-the-visual-content-fragment-publish-url)

>[!NOTE]
>
>Consulte [Fragmentos de contenido visual](/help/sites-cloud/administering/content-fragments/visual-content-fragments.md) para cargar, asignar y usar su plantilla en AEM.

>[!NOTE]
>
>Use [Figma en el trabajo de fragmentos de contenido visual](/help/ai-in-aem/agents/brand-experience/experience-production/figma-to-visual-content-fragments.md) para automatizar la carga de un diseño de HTML.

## Lo que aprenderá {#what-you-will-learn}

Después de proporcionar una introducción (muy rápida) a:

* Uso de las plantillas en AEM
* Uso de la URL de publicación

Esta página cubre (con más detalle):

* Handlebars: los conceptos básicos necesarios de la sintaxis
* Cómo acceder a los datos de fragmentos de contenido
* Uso de fragmentos de contenido anidados
* Administrar campos multivalor
* Creación de bucles y lógica condicional
* Prácticas recomendadas de diseño de plantillas para fragmentos de contenido

## Requisitos previos {#prerequisites}

Para comprender y trabajar con las tecnologías aquí tratadas, debería tener lo siguiente:

* Comprensión básica de HTML
* Familiaridad con fragmentos de contenido y modelos de fragmentos de contenido de AEM
* Comprensión de los modelos de fragmentos de contenido

## Uso de una plantilla de HTML de fragmento de contenido {#using-a-content-fragment-html-template}

### Uso de una plantilla de HTML de fragmento de contenido en AEM {#using-a-content-fragment-html-template-in-aem}

Para obtener más información sobre cómo utilizar la plantilla en AEM, consulte:

* [Fragmentos de contenido visual: carga y asignación de plantillas](/help/sites-cloud/administering/content-fragments/visual-content-fragments.md)
* [Acción de previsualización para un fragmento seleccionado: desde la consola](/help/sites-cloud/administering/content-fragments/managing.md#actions-selected-content-fragment)
* [Previsualice el fragmento: desde el editor de fragmentos](/help/sites-cloud/administering/content-fragments/authoring.md#preview-content-fragment)

### Uso de la URL de publicación de fragmento de contenido visual {#using-the-visual-content-fragment-publish-url}

Una vez que haya creado fragmentos de contenido visual utilizando la plantilla, puede usar la [URL de publicación de los fragmentos de contenido visual](/help/implementing/developing/extending/content-fragments-visualization-publish-url.md).

## Manillar: los (muy) conceptos básicos {#handlebars-the-very-basics}

Handlebars es un lenguaje de creación de plantillas simple que usa llaves dobles (corchetes) `{{ }}` para insertar contenido dinámico en HTML.

### Sintaxis básica {#basic-syntax}

Un ejemplo de sintaxis básica de Handlebars:

```handlebars
<!-- Output a variable (HTML-escaped) -->
{{variableName}}

<!-- Output raw HTML (unescaped) -->
{{{htmlContent}}}

<!-- Comment (not rendered) -->
{{! This is a comment }}
```

### Conceptos clave {#key-concepts}

Los conceptos clave de Handlebars:

| Sintaxis | Descripción | Cuándo se usa |
|--- |--- |--- |
| `{{ }}` | Omite los caracteres especiales de HTML | Metadatos, etiquetas, booleanos |
| `{{{ }}}` | Genera HTML sin procesar (sin escape) | Salida de recurso y texto enriquecido |
| `{{! }}` | Comentario solo de Handlebars | Documentación de plantilla |

>[!IMPORTANT]
>
> Utilice llaves triples (`{{{ }}}`) para los valores de campo porque los valores se representan previamente en HTML.

## Referencia de contexto de plantilla {#template-context-reference}

Cuando se representa la plantilla, recibe un objeto de contexto que contiene todos los datos sobre el fragmento de contenido. Esto abarcará:

* el fragmento que ha seleccionado
* todos los demás fragmentos a los que se hace referencia desde ese fragmento seleccionado

  >[!NOTE]
  >
  >Se puede hacer referencia a los fragmentos:
  >
  >* en la IU: hasta la profundidad máxima de 5
  >* al utilizar la API: la profundidad es configurable, hasta la profundidad máxima de 10

### Fragmento de contenido {#content-fragment}

La estructura del objeto de contexto para el fragmento de contenido (seleccionado):

| Variable | Tipo | Descripción |
|--- |--- |--- |
| `properties` | Mapa | Metadatos de fragmento (consulte [Estructura de propiedades](#properties-structure-main-and-referenced-fragments)) |
| `fields` | Mapa | Acceso directo a valores de campo por nombre |
| `allFields` | Lista | Matriz de `{name, value}` para iteración |
| `hasFields` | Booleano | `true` si el fragmento tiene campos |

### Estructura de propiedades {#properties-structure}

El objeto `properties` tiene la misma estructura para el fragmento seleccionado y para cada fragmento referenciado.

| Propiedad | Tipo | Descripción | Ejemplo |
|--- |--- |--- |--- |
| `id` | Cadena | UUID del fragmento | |
| `title` | Cadena | Título del fragmento | Ciclismo en el sur de Utah |
| `description` | Cadena | Descripción del fragmento | Una aventura... |
| `path` | Cadena | Ruta JCR al fragmento | `/content/dam/...` |
| `hasDescription` | Booleano | True si la descripción no está en blanco | `true` |
| `createdDate` | Cadena | Fecha de creación de ISO-8601 | |
| `modifiedDate` | Cadena | Fecha de modificación ISO-8601 | |
| `publishedDate` | Cadena | Fecha de publicación de ISO-8601 | |
| `status` | Cadena | Estado de replicación para el nivel de publicación | `DRAFT` |
| `model` | Mapa | Contiene: `id`, `path`, `name`, `technicalName`, `description` | |
| `validationStatus` | Lista | Entradas como `{property, message}` | |
| `previewReplicationStatus` | Cadena | Estado de replicación para el nivel de previsualización | |
| `tags` | Lista | Etiquetas de nivel de fragmento. Cada elemento: `id`, `title`, `titlePath`, `name`, `path`, `description` | |
| `fieldTags` | Lista | Etiquetas de nivel de campo. La misma estructura que `tags`. | |

Ejemplos: Acceso a plantillas

Para el fragmento de contenido (seleccionado):

```handlebars
{{properties.title}}, {{properties.description}}, {{{fields.field_name}}} 
```

### Fragmentos de contenido referenciados {#referenced-content-fragments}

La estructura del objeto de contexto para cualquier fragmento al que se haga referencia:

| Variable | Tipo | Descripción |
|--- |--- |--- |
| `hasReferencedFragments` | Booleano | `true` cuando existen referencias |
| `referencedFragments` | Lista | Matriz de objetos de fragmento referenciados |
| `referencesError` | Booleano | `true` si se produjo un error al cargar las referencias |
| `referencesErrorMessage` | Cadena | Mensaje de error cuando `referencesError` es `true` |

### Estructura del fragmento de referencia {#referenced-fragment-structure}

Cada elemento de `referencedFragments` contiene:

| Propiedad | Tipo | Descripción |
|--- |--- |--- |
| `anchorId` | Cadena | ID de anclaje seguro para HTML (en el nivel de fragmento; no es una propiedad de fragmento de contenido) |
| `properties` | Mapa | Metadatos de fragmento (la misma estructura que arriba) |
| `hasFields` | Booleano | True si el fragmento tiene campos |
| `fields` | Mapa | Acceso directo a los campos de este fragmento |
| `allFields` | Lista | Matriz de `{name, value}` para iteración |

Ejemplos: Acceso a la plantilla para el primer fragmento de contenido al que se hace referencia (primer elemento de la lista indexada en 0):

```handlebars
{{referencedFragments.[0].anchorId}}, {{referencedFragments.[0].properties.title}}, {{referencedFragments.[0].properties.description}}
```

O desde el mapa de campos:

```handlebars
{{{ fields.referenced_cf_field_name.properties.description }}}
```

## Acceso básico al campo {#basic-field-access}

Se recomienda el acceso directo al campo, si es necesario, puede iterar en todos los campos.

### Acceso directo al campo (recomendado) {#direct-field-access-recommended}

Acceda a los campos directamente por nombre mediante el mapa de campos:

```handlebars
<!DOCTYPE html>
<html>
<head>
  <title>{{properties.title}}</title>
</head>
<body>
  <article>
    <h1>{{{fields.title}}}</h1>
    <p class="subtitle">{{{fields.subtitle}}}</p>
    <div class="content">
      {{{fields.description}}}
    </div>
    <div class="image">
      {{{fields.primaryImage}}}
    </div>
  </article>
</body>
</html>
```

Recuerde:

* Utilice llaves triples `{{{ }}}` para los valores de campo si contienen HTML procesado previamente (texto enriquecido)
* Los nombres de campo (título, subtítulo, descripción, primaryImage) **deben** coincidir con el modelo de fragmento de contenido **exactamente**
* Los campos que faltan no se representan: no se generan errores y la sintaxis de Handlebars permanece presente (y visible) en el fragmento de HTML procesado

### Iterar en todos los campos {#iterate-through-all-fields}

Utilice `allFields` cuando no conozca los nombres de campo por adelantado:

```handlebars
<table>
  <thead>
    <tr>
      <th>Field Name</th>
      <th>Field Value</th>
    </tr>
  </thead>
  <tbody>
    {{#each allFields}}
    <tr>
      <td>{{name}}</td>
      <td>{{{value}}}</td>
    </tr>
    {{/each}}
  </tbody>
</table>
```

Recuerde:

* `{{name}}` usa llaves dobles (etiqueta de texto sin formato)
* `{{{value}}}` usa llaves triples (valor de HTML procesado previamente)

## Fragmentos de contenido anidados {#nested-content-fragments}

Cuando un campo de fragmento de contenido hace referencia a otro fragmento de contenido, puede utilizar la notación de puntos para acceder directamente a los campos del fragmento al que se hace referencia.

### Anidado de un solo nivel {#single-level-nesting}

Un ejemplo de anidamiento de un solo nivel:

```handlebars
<article>
  <h1>{{{fields.title}}}</h1>

  <!-- Access author (a referenced Content Fragment) -->
  <div class="author-info">
    <h3>Author</h3>
    <p>Name: {{{fields.author.name}}}</p>
    <p>Email: {{{fields.author.email}}}</p>
    <p>Bio: {{{fields.author.bio}}}</p>
  </div>

  <div class="content">
    {{{fields.content}}}
  </div>
</article>
```

Patrón: `fields.referenceFieldName.nestedFieldName`

### Anidado de varios niveles {#multi-level-nesting}

El sistema admite una profundidad de anidación ilimitada:

```handlebars
<article>
  <h1>{{{fields.title}}}</h1>

  <div class="author-details">
    <!-- Level 1: Author -->
    <p>Author: {{{fields.author.name}}}</p>

    <!-- Level 2: Author's Organization -->
    <p>Organization: {{{fields.author.organization.name}}}</p>
    <p>Website: {{{fields.author.organization.website}}}</p>

    <!-- Level 3: Organization's Address -->
    <p>Located in: {{{fields.author.organization.address.city}}},
    {{{fields.author.organization.address.country}}}</p>
  </div>

  <div class="content">
    {{{fields.content}}}
  </div>
</article>
```

Patrón: `fields.level1.level2.level3.fieldName` (profundidad limitada; el valor predeterminado es 5, se puede ampliar a 10 cuando se utiliza la API)

### Requisito de parámetro de API: hidratación {#api-parameter-requirements}

Para habilitar el acceso anidado a fragmentos de contenido, debe incluir el parámetro de consulta `hydration` en la llamada de API:

Para habilitar la hidratación:

```http
# Enable hydration with depth=2 for 2 levels of nesting
GET /adobe/sites/cf/fragments/{id}/preview?hydration=%7B%22enabled%22%3Atrue%2C%22maxDepth%22%3A2%7D
```

| `maxDepth` | Qué se carga |
|--- |--- |
| `1` | Fragmento principal + referencias directas |
| `2` | Fragmento principal + referencias directas + sus referencias |
| `3+` | Continuar hasta 10 niveles |

## Campos multivalor {#multi-valued-fields}

Existen varios tipos de campos multivalorados.

### Campos de texto de varios valores {#multi-valued-text-fields}

Los campos de texto, [number](#multi-valued-number-fields), fecha y otros campos simples se convierten en matrices cuando se asignan varios valores:

```handlebars
<article>
  <h1>{{{fields.title}}}</h1>

  <!-- Access individual items by index (use dot before bracket) -->
  <div class="tags">
    <span class="tag">{{{fields.tags.[0]}}}</span>
    <span class="tag">{{{fields.tags.[1]}}}</span>
  </div>

  <!-- Better: Iterate through all tags -->
  <div class="tags">
    {{#each fields.tags}}
    <span class="tag">{{{this}}}</span>
    {{/each}}
  </div>
</article>
```

Recuerde, cuando acceda a elementos de matriz por índice en Handlebars:

* Use:
   * `.[0]` (punto antes del corchete)
* No:
   * `[0]`

### Campos numéricos multivalorados {#multi-valued-number-fields}

Los números se convierten en [cadenas](#multi-valued-text-fields) para su procesamiento:

```handlebars
<div class="pricing">
  <h3>Available Prices:</h3>
  {{#each fields.prices}}
  <span class="price">${{{this}}}</span>
  {{/each}}
</div>
```

### Referencias de fragmentos de contenido multivalor {#multi-valued-content-fragment-references}

Cuando un campo hace referencia a varios fragmentos de contenido:

```handlebars
<div class="authors">
  <h3>Authors:</h3>
  {{#each fields.authors}}
  <div class="author">
    <h4>{{{this.name}}}</h4>
    <p>Email: {{{this.email}}}</p>
    {{#if this.bio}}
    <p class="bio">{{{this.bio}}}</p>
    {{/if}}
  </div>
  {{/each}}
</div>
```

### Referencias de recursos de varios valores {#multi-valued-asset-references}

[Referencia de contenido](/help/sites-cloud/administering/content-fragments/content-fragment-models.md#content-reference) campos configurados para tipos de contenido que son recursos (por ejemplo, imágenes y documentos) se representan previamente como HTML. Los recursos de varios valores se convierten en matrices:

```handlebars
<!-- Single asset -->
<div class="hero-image">
  {{{fields.heroImage}}}
</div>

<!-- Multi-valued: iterate through all images -->
<div class="gallery">
  {{#each fields.gallery}}
  <div class="image">{{{this}}}</div>
  {{/each}}
</div>
```

### Referencias anidadas de varios valores {#nested-multi-valued-references}

Las referencias de varios valores pueden contener referencias de varios valores en cualquier profundidad:

```handlebars
{{#each fields.chapters}}
<div class="chapter">
  <h3>Chapter: {{{this.title}}}</h3>

  {{#each this.authors}}
  <p>Author: {{{this.name}}}</p>

  {{#each this.publications}}
  <p>Publication: {{{this.title}}}</p>
  {{/each}}
  {{/each}}
</div>
{{/each}}
```

## Bucles e iteración {#loops-and-iteration}

Handlebars proporciona el ayudante `{{#each}}` para recorrer en iteración matrices y objetos.

### Iteración en matrices {#iterating-over-arrays}

Un ejemplo de iteración en matrices:

```handlebars
<!-- Simple array iteration -->
{{#each fields.tags}}
<span class="tag">{{{this}}}</span>
{{/each}}

<!-- Array of objects -->
{{#each fields.authors}}
<div class="author">
  <h4>{{{this.name}}}</h4>
  <p>{{{this.email}}}</p>
</div>
{{/each}}

<!-- With empty-state fallback -->
{{#each fields.tags}}
<span class="tag">{{{this}}}</span>
{{else}}
<p>No tags available.</p>
{{/each}}
```

### Variables especiales en bucles {#special-variables-in-loops}

Dentro de bloques de `{{#each}}`, Handlebars proporciona variables especiales:

```handlebars
{{#each fields.items}}
<div class="item">
  <p>Index: {{@index}}</p>     <!-- 0-based index -->
  <p>Number: {{@number}}</p>   <!-- 1-based index -->
  <p>First: {{@first}}</p>     <!-- true for first item -->
  <p>Last: {{@last}}</p>       <!-- true for last item -->
  <p>Value: {{{this}}}</p>     <!-- current item -->
</div>
{{/each}}

<!-- Example: numbered steps with first/last CSS classes -->
<ul>
  {{#each fields.steps}}
  <li class="{{#if @first}}first{{/if}} {{#if @last}}last{{/if}}">
    Step {{@number}}: {{{this}}}
  </li>
  {{/each}}
</ul>
```

### Iteración en fragmentos referenciados {#iterating-over-referenced-fragments}

Ejemplo de iteración en fragmentos referenciados:

```handlebars
{{#if hasReferencedFragments}}
<section class="references">
  <h2>Related Content</h2>
  {{#each referencedFragments}}
  <article id="{{anchorId}}">
    <h3>{{title}}</h3>
    {{#if hasDescription}}
    <p>{{description}}</p>
    {{/if}}
    {{#if hasFields}}
    <ul>
      {{#each allFields}}
      <li><strong>{{name}}:</strong> {{{value}}}</li>
      {{/each}}
    </ul>
    {{/if}}
  </article>
  {{/each}}
</section>
{{/if}}
```

### Bucles anidados {#nested-loops}

Un ejemplo de bucles anidados:

```handlebars
{{#each fields.categories}}
<section class="category">
  <h2>{{{this.name}}}</h2>

  {{#each this.products}}
  <article class="product">
    <h3>{{{this.name}}}</h3>
    <p>{{{this.description}}}</p>
  </article>
  {{/each}}
</section>
{{/each}}
```

## Renderización condicional {#conditional-rendering}

Utilice condicionales para mostrar u ocultar contenido en función de la disponibilidad de los datos.

### If/Else básico {#basic-if-else}

Un ejemplo de una construcción básica if-else:

```handlebars
{{#if hasMainDescription}}
<p class="description">{{properties.description}}</p>
{{else}}
<p class="no-description">No description available.</p>
{{/if}}

<!-- Check field existence before rendering -->
{{#if fields.author}}
<div class="author">
  <p>By {{{fields.author.name}}}</p>
</div>
{{/if}}

{{#if fields.publishDate}}
<time>{{{fields.publishDate}}}</time>
{{/if}}
```

### A menos que (negativo o condicional) {#unless-negative-conditional}

Un asistente de `unless`:

```handlebars
<!-- Show author unless explicitly hidden -->
{{#unless fields.hideAuthor}}
<div class="author">{{{fields.author.name}}}</div>
{{/unless}}
```

### Condiciones anidadas {#nested-conditials}

Un ejemplo de condicional anidado:

```handlebars
{{#if fields.author}}
<div class="author">
  <h3>{{{fields.author.name}}}</h3>

  {{#if fields.author.bio}}
  <p class="bio">{{{fields.author.bio}}}</p>
  {{/if}}

  {{#if fields.author.website}}
  <a href="{{{fields.author.website}}}">Visit Website</a>
  {{/if}}
</div>
{{/if}}
```

## Ayudantes de Handlebars integrados {#built-in-handlebars-helpers}

Handlebars incluye varios ayudantes integrados, más allá de `{{#if}}` y `{{#each}}`.

| Ayudante | Descripción |
|--- |--- |
| `{{#if condition}}` | Procesa el contenido si la condición es verdadera. Valores de False: `false`, `undefined`, `null`, `0`, `""`, `[]` |
| `{{#unless condition}}` | Procesa contenido si la condición es falsa (al contrario de `#if`) |
| `{{#each array}}` | Repite el contenido de cada elemento; admite `{{else}}` para matrices vacías |
| `{{#with object}}` | Crea un nuevo ámbito para un objeto anidado, lo que reduce la repetición de rutas |
| `{{lookup this "key"}}` | Busca dinámicamente una propiedad por su nombre |

### Con el asistente {#with-helper}

Crea un nuevo ámbito para objetos anidados para reducir los prefijos de ruta repetitiva:

```handlebars
{{#with fields.author}}
<div class="author">
  <h3>{{{name}}}</h3>     <!-- same as fields.author.name -->
  <p>{{{email}}}</p>      <!-- same as fields.author.email -->
  <p>{{{bio}}}</p>        <!-- same as fields.author.bio -->
</div>
{{/with}}

<!-- Useful for deeply nested objects -->
{{#with fields.author.organization}}
<div class="organization">
  <h4>{{{name}}}</h4>
  <p>{{{website}}}</p>
  {{#with address}}
  <address>
    {{{street}}}<br/>
    {{{city}}}, {{{country}}}
  </address>
  {{/with}}
</div>
{{/with}}
```

## Avanzar patrones {#advanced-patterns}

A continuación se muestran algunos ejemplos de patrones avanzados.

### Acceso al contexto principal en bucles anidados {#accessing-parent-context-in-nested-loops}

Use `../` para acceder al ámbito principal desde un bucle anidado:

```handlebars
<h1>{{{fields.title}}}</h1>

{{#each fields.chapters}}
<section class="chapter">
  <h2>Chapter {{@number}}: {{{this.title}}}</h2>

  {{#each this.sections}}
  <article>
    <!-- Access parent chapter via ../ -->
    <p>Chapter: {{{../title}}}</p>

    <!-- Access root context via ../../ -->
    <p>Book: {{{../../fields.title}}}</p>

    <h3>{{{this.title}}}</h3>
    <div>{{{this.content}}}</div>
  </article>
  {{/each}}
</section>
{{/each}}
```

### Clases CSS dinámicas {#dynamic-css-classes}

Un ejemplo de clases CSS dinámicas:

```handlebars
<article class="content-fragment {{#if hasMainDescription}}with-description{{/if}} {{#if hasReferencedFragments}}has-refs{{/if}}">
  <h1>{{properties.title}}</h1>
</article>

<ul class="tag-list">
  {{#each fields.tags}}
  <li class="tag {{#if @first}}first{{/if}} {{#if @last}}last{{/if}}">
    {{{this}}}
  </li>
  {{/each}}
</ul>
```

## Ejemplos completos {#complete-examples}

Se proporcionan varios ejemplos completos como referencia.

### Publicación de blog con autor

Una publicación de blog con detalles del autor:

```handlebars
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>{{properties.title}}</title>
  <style>
    body { font-family: Arial, sans-serif; margin: 40px; }
    .author-card { background: #f5f5f5; padding: 20px; border-radius: 8px; }
    .tags { display: flex; gap: 10px; }
    .tag { background: #007bff; color: white; padding: 5px 10px; border-radius: 4px; }
  </style>
</head>
<body>
  <article>
    <header>
      <h1>{{{fields.title}}}</h1>
      {{#if fields.publishDate}}
      <time datetime="{{{fields.publishDate}}}">{{{fields.publishDate}}}</time>
      {{/if}}
      {{#if fields.tags}}
      <div class="tags">
        {{#each fields.tags}}
        <span class="tag">{{{this}}}</span>
        {{/each}}
      </div>
      {{/if}}
    </header>

    {{#if fields.heroImage}}
    <figure>
      {{{fields.heroImage}}}
      {{#if fields.imageCaption}}
      <figcaption>{{{fields.imageCaption}}}</figcaption>
      {{/if}}
    </figure>
    {{/if}}

    <div class="content">
      {{{fields.content}}}
    </div>

    {{#if fields.author}}
    <aside class="author-card">
      <h3>About the Author</h3>
      <h4>{{{fields.author.name}}}</h4>
      {{#if fields.author.profilePicture}}
      <div class="author-image">{{{fields.author.profilePicture}}}</div>
      {{/if}}
      {{#if fields.author.bio}}
      <p>{{{fields.author.bio}}}</p>
      {{/if}}
      {{#if fields.author.email}}
      <p>Contact: <a href="mailto:{{{fields.author.email}}}">{{{fields.author.email}}}</a></p>
      {{/if}}
    </aside>
    {{/if}}
  </article>
</body>
</html>
```

Llamada de API requerida:

```http
GET /adobe/sites/cf/fragments/{id}/preview?hydration=%7B%22enabled%22%3Atrue%2C%22maxDepth%22%3A1%7D
```

### Vista de tabla genérica (sin conocimientos previos de campos) {#generic-table-view-no-prior-knowledge-of-fields}

Una vista de tabla genérica, sin un conocimiento inherente de campos. es similar a la **Plantilla genérica**:

```handlebars
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>{{properties.title}}</title>
  <style>
    body { font-family: Arial, sans-serif; margin: 40px; }
    table { width: 100%; border-collapse: collapse; margin: 20px 0; }
    th, td { border: 1px solid #ddd; padding: 12px; text-align: left; }
    th { background-color: #f4f4f4; font-weight: bold; }
    .ref-section { background: #f9f9f9; padding: 20px; margin: 20px 0; border-radius: 8px; }
  </style>
</head>
<body>
  <header>
    <h1>{{properties.title}}</h1>
    {{#if properties.description}}<p>{{properties.description}}</p>{{/if}}
    <p><small>Path: {{properties.path}}</small></p>
  </header>

  {{#if hasFields}}
  <section>
    <h2>Fields</h2>
    <table>
      <thead>
        <tr><th>Field Name</th><th>Field Value</th></tr>
      </thead>
      <tbody>
        {{#each allFields}}
        <tr>
          <td><strong>{{name}}</strong></td>
          <td>{{{value}}}</td>
        </tr>
        {{/each}}
      </tbody>
    </table>
  </section>
  {{/if}}

  {{#if hasReferencedFragments}}
  <section class="ref-section">
    <h2>Referenced Content Fragments</h2>
    {{#each referencedFragments}}
    <article id="{{anchorId}}" style="margin-bottom: 30px;">
      <h3>{{title}}</h3>
      {{#if hasDescription}}<p>{{description}}</p>{{/if}}
      <p><small>Path: {{path}}</small></p>
      {{#if hasFields}}
      <table>
        <thead>
          <tr><th>Field Name</th><th>Field Value</th></tr>
        </thead>
        <tbody>
          {{#each allFields}}
          <tr>
            <td><strong>{{name}}</strong></td>
            <td>{{{value}}}</td>
          </tr>
          {{/each}}
        </tbody>
      </table>
      {{/if}}
    </article>
    {{/each}}
  </section>
  {{/if}}
</body>
</html>
```

## Prácticas recomendadas {#best-practices}

Las prácticas recomendadas incluyen:

1. Utilice siempre llaves triples para los valores de campo que contengan contenido de marcado de HTML.

   * Los valores de campo se representan previamente en HTML.

     >[!NOTE]
     >
     >Las llaves dobles muestran las etiquetas HTML sin procesar como texto sin formato.

   ```handlebars
   <!-- CORRECT -->
   {{{fields.description}}}
   
   <!-- WRONG - displays HTML tags as text -->
   {{fields.description}}
   ```

1. Compruebe la existencia antes de acceder a los campos anidados.

   ```handlebars
   <!-- GOOD: check before accessing nested fields -->
   {{#if fields.author}}
   <p>By {{{fields.author.name}}}</p>
   {{/if}}
   
   <!-- RISKY: may render empty if author is not set -->
   <p>By {{{fields.author.name}}}</p>
   ```

1. Utilice el acceso directo al campo siempre que sea posible.

   * Es más fácil de leer y de mantener que repetir `allFields` y coincidir por nombre.

1. Estructurar plantillas con comentarios de sección.

   ```handlebars
   {{! ===== HEADER SECTION ===== }}
   <header>
     <h1>{{properties.title}}</h1>
   </header>
   
   {{! ===== MAIN CONTENT ===== }}
   <main>
     {{#if hasFields}}
     <!-- fields rendering -->
     {{/if}}
   </main>
   
   {{! ===== REFERENCES ===== }}
   {{#if hasReferencedFragments}}
   <!-- references rendering -->
   {{/if}}
   ```

1. Gestionar correctamente los datos que faltan con reserva.

   ```handlebars
   {{#if fields.title}}
   <h1>{{{fields.title}}}</h1>
   {{else}}
   <h1>Untitled</h1>
   {{/if}}
   ```

1. Utilice siempre una estructura de documentos de HTML adecuada.

   ```handlebars
   <!DOCTYPE html>
   <html lang="en">
   <head>
     <meta charset="UTF-8">
     <meta name="viewport" content="width=device-width, initial-scale=1">
     <title>{{properties.title}}</title>
   </head>
   <body>
     <!-- your content here -->
   </body>
   </html>
   ```

1. Realice pruebas con una variedad de escenarios de contenido:

   * Todos los campos completados
   * Faltan campos opcionales
   * Campos multivalor vacíos
   * Anidado profundo (varios niveles)
   * Referencias que no se cargan

1. Utilice elementos semánticos de HTML:

   * Para una mejor accesibilidad, use `<article>`, `<header>`, `<main>`, `<footer>`, `<time>`, `<address>` o similar.

1. Mantener estilos en CSS.

   * Utilice etiquetas `<style>` u hojas de estilo externas.
   * Evite los estilos en línea siempre que sea posible.

1. Lógica compleja del documento:

   * Use los comentarios de Handlebars `({{! }})`.
   * No utilice comentarios de HTML, que aparecen en la salida procesada.

## Resolución de problemas {#troubleshooting}

Algunas sugerencias para la solución de problemas incluyen:

| Problema | Síntoma | Solución |
|--- |--- |--- |
| El campo muestra las etiquetas HTML como texto | `<p>Hello World</p>` se muestra literalmente | Usar llaves triples: `{{{fields.description}}}` |
| Los campos de fragmento de contenido anidado están vacíos o muestran [objeto Objeto] | `{{{fields.author.name}}}` está en blanco | Habilite la hidratación en la llamada de API; compruebe la ortografía del nombre del campo; compruebe que `maxDepth` tenga la profundidad suficiente |
| El campo multivalor solo muestra el primer elemento | La matriz con cinco elementos solo procesa uno | Usar `{{#each fields.tags}}` para repetir todos los elementos |
| El acceso al índice de matriz no funciona | `{{{fields.tags[0]}}}` se representa vacío | Usar sintaxis con corchetes: `{{{fields.tags.[0]}}}` |
| Los fragmentos referenciados no aparecen | `hasReferencedFragments` siempre es falso | Habilitar hidratación: `?hydration=%7B%22enabled%22%3Atrue%7D;` también comprobar `{{#if referencesError}}` |
| La plantilla no procesa nada | Página vacía o salida en blanco | Buscar bloques de `{{#if}}` o `{{#each}}` sin cerrar; agregar salida de diagnóstico: `<pre>hasFields: {{hasFields}}`|`title: {{properties.title}}</pre>` |
| Los comentarios aparecen en la página representada | Texto de comentario de HTML visible para los usuarios finales | Use los comentarios de Handlebars `{{! comment }}` en lugar de HTML `<!-- comment -->` |
| El condicional siempre se evalúa como verdadero | `{{#if fields.enabled}}` siempre es verdadero | Nota: la cadena `"false"` es verdadera en Handlebars. Solo los datos reales `false`, `null`, `undefined`, `0`, `""` y `[]` son falsos. |
| Caracteres especiales representados como entidades | `&lt;`, `&amp;` mostrado en lugar de `<`, `&` | Utilice llaves triples para el contenido de HTML procesado previamente: `{{{fields.content}}}` |
| No se puede acceder a la variable de bucle externo desde el bucle interno | La variable del elemento principal `#each` no está definida | Usar `../` para el ámbito principal: `{{{../name}}}`; usar `../../` para el ámbito principal |
| La lista vacía no muestra el mensaje de reserva | El campo multivalor con cero elementos no muestra nada | Usar `{{else}}` dentro de `{{#each}}`: `{{#each fields.tags}}...{{else}}<p>No tags</p>{{/each}}` |

### Uso de recursos {#working-with-assets}

AEM procesa previamente como HTML los fragmentos de contenido a los que se hace referencia en Assets. Por lo tanto, las llaves triples son obligatorias para todas las referencias de recursos.

| Tipo de recurso | Procesado como |
|--- |--- |
| Imágenes | `<img src="..." alt="...">` |
| Vídeos | `<video>` elemento |
| Documentos | `<a href="...">` vínculo |

Recuerde:

* Utilice siempre llaves triples para los campos de recursos.
Si utiliza llaves dobles, se omitirá la etiqueta de HTML generada y se mostrará como texto sin procesar en lugar de representar la imagen, el vídeo o el vínculo.

### Uso del campo de recursos {#asset-field-usage}

Un ejemplo de uso de campos de recursos:

```handlebars
<!-- CORRECT - triple braces render the image -->
{{{fields.heroImage}}}
<!-- Output: <img src="path/to/image.jpg" alt="Hero"> -->

<!-- WRONG - double braces escape the tag, showing it as text -->
{{fields.heroImage}}
<!-- Output: &lt;img src="path/to/image.jpg" alt="Hero"&gt; -->
```

## Ayudantes de plantilla personalizados {#customer-template-helpers}

El sistema proporciona controladores Handlebars personalizados para generar elementos HTML con atributos HTML personalizados. Estos ayudantes le proporcionan control sobre el marcado generado, a la vez que gestionan la complejidad de extraer direcciones URL de origen a partir de contenido procesado previamente.

Ayudantes disponibles:

1. `asset` - Genera etiquetas `<img>` con atributos personalizados
1. `text`: genera `<span>` etiquetas que ajustan el contenido de texto con atributos personalizados

### `asset` asistente {#asset-helper}

Sintaxis:

```handlebars
{{{asset fieldValue attribute1="value1" attribute2="value2"}}}
```

Recuerde:

* Utilice llaves triples `{{{ }}}` con el asistente de recursos, no llaves dobles.

#### Cuatro ejemplos básicos {#four-basic-examples}

Cuatro ejemplos básicos son:

```handlebars
<!-- Add a CSS class to an image -->
{{{asset fields.heroImage class="hero-image"}}}
<!-- Output: <img src="..." alt="..." class="hero-image"> -->

<!-- Add multiple CSS classes -->
{{{asset fields.productImage class="product-img responsive shadow"}}}

<!-- Add id and class -->
{{{asset fields.logo class="brand-logo" id="main-logo"}}}

<!-- Add data attributes -->
{{{asset fields.thumbnail class="thumb" data-category="product" data-id="123"}}}
```

#### Atributos admitidos {#supported-attributes}

Puede añadir cualquier atributo de HTML válido:

| Atributo |  Ejemplo |
|--- |--- |
| `class` | `class="my-class another-class"` |
| `id` | `id="unique-id"` |
| `alt` | `alt="Custom alt text" (overrides existing alt)` |
| `data-*` | `data-index="1" data-type="hero"` |
| `aria-*` | `aria-label="Description" aria-hidden="true"` |
| `width` | `width="300"` |
| `height` | `height="200"` |
| `loading` | `loading="lazy"` |
| `style` | `style="border-radius: 8px;"` |

#### Omitir texto alternativo {#override-alt-text}

Se puede anular el atributo `alt` de la imagen original:

```handlebars
{{{asset fields.photo alt="Custom description for accessibility"}}}
```

#### Ejemplo complejo {#complex-example}

Un ejemplo complejo es:

```handlebars
<article class="blog-post">
<header>
{{{asset fields.featuredImage 
class="featured-image responsive" 
id="post-hero"
loading="lazy"
data-post-id="12345"}}}
</header>
</article>
```

#### Uso de con bucles {#using-with-loops}

Asistente de recursos en bucles:

```handlebars
{{#each fields.galleryImages}}
{{{asset this class="gallery-item" data-index=@index}}}
{{/each}}
```

### `text` asistente {#text-helper}

El asistente de texto genera una etiqueta `<span>` que ajusta el contenido de texto con clases CSS y atributos HTML personalizados. Útil para aplicar estilo a campos de texto individuales.

Sintaxis:

```handlebars
{{{text fieldValue attribute1="value1" attribute2="value2"}}}
```

Recuerde:

* Utilice llaves triples `{{{ }}}` con el asistente de texto, no llaves dobles.

#### Tres ejemplos básicos {#three-basic-examples}

Tres ejemplos básicos son:

```handlebars
<!-- Add a CSS class to text -->
{{{text fields.title class="article-title"}}}
<!-- Output: <span class="article-title">The Title Text</span> -->

<!-- Add multiple attributes -->
{{{text fields.price class="price-tag" id="product-price" data-currency="USD"}}}

<!-- Style inline text -->
{{{text fields.highlightedText class="highlighted" style="background: yellow;"}}}
```

#### Casos de uso comunes {#common-use-cases}

Algunos casos de uso comunes incluyen:

```handlebars
<!-- Styling article metadata -->
<article>
<header>
{{{text fields.category class="category-badge"}}}
<h1>{{{fields.title}}}</h1>
{{{text fields.author class="byline"}}}
{{{text fields.publishDate class="date"}}}
</header>
</article>

<!-- Creating styled labels -->
<div class="product-card">
{{{text fields.productName class="product-name"}}}
{{{text fields.brand class="brand-label" data-brand-id="abc"}}}
{{{text fields.price class="price" id="main-price"}}}
</div>

<!-- Accessibility enhancements -->
{{{text fields.importantNote class="alert" role="alert" aria-live="polite"}}}
```

#### Con bucles {#with-loops}

Un caso de uso común con bucles incluye:

```handlebars
{{#each fields.tags}}
{{{text this class="tag-badge"}}}
{{/each}}
```

### Ayudantes: validación de atributos {#helpers-attribute-validation}

Ambos ayudantes validan los nombres de atributo antes de incluirlos en la salida.

Nombres de atributo válidos:

* Debe comenzar por una letra (a-z, A-Z)
* Solo puede contener letras, dígitos, guiones y guiones bajos; consulte las [Convenciones de nombres](/help/implementing/developing/introduction/naming-conventions.md)
* Sin distinción de mayúsculas y minúsculas
* Por ejemplo:
   * Válido:
      * `class`, `id`, `data-value`, `aria-label`, `my_attr`, `dataIndex1`
   * No válido:
      * `123-attr`, `-class`, `@special`, `$money`

Los nombres de atributo no válidos se omiten silenciosamente con una advertencia en los registros:

```handlebars
{{{asset fields.image class="valid" 123-invalid="skipped" id="also-valid"}}}
<!-- Output: <img src="..." alt="..." class="valid" id="also-valid"> -->
<!-- 123-invalid is skipped because it starts with a number -->
```

Recuerde:

* Compruebe los registros del servidor para ver las advertencias &quot;Formato de nombre de atributo no válido bloqueado&quot;.

## Comparación de la salida directa con los ayudantes {#comparing-direct-output-to-helpers}

Cuándo se debe establecer la salida directa `{{{fields.xxx}}}`:

* No necesita un estilo personalizado
* Desea el resultado predeterminado tal cual
* El campo contiene HTML complejo que no desea modificar

Cuándo usar los ayudantes:

* Debe añadir clases CSS para el estilo
* Debe agregar atributos personalizados de HTML (`data-*`, `aria-*` y otros)
* Desea una estructura de HTML coherente y controlada

Comparación:

```handlebars
<!-- Direct output - uses whatever HTML the system generates -->
{{{fields.heroImage}}}
<!-- Output: <img src="/path/image.jpg" alt="Hero Image"> -->

<!-- With asset helper - full control over attributes -->
{{{asset fields.heroImage class="hero responsive" id="main-hero" loading="lazy"}}}
<!-- Output: <img src="/path/image.jpg" alt="Hero Image" class="hero responsive" id="main-hero" loading="lazy"> -->
```

## Referencia rápida {#quick-reference}

Se proporciona información de referencia rápida como referencia.

### Variables de contexto {#context-variables}

Las variables de contexto:

```handlebars
{{properties}}                <!-- Main fragment metadata -->
{{fields}}                    <!-- Map keyed by field name to rendered values (such as strings, lists, nested maps for Content Fragment references, commerce maps, HTML, and others) -->
{{allFields}}                 <!-- List of { name, value } maps (uniform iteration) -->
{{hasFields}}.                <!-- Boolean -->
{{hasReferencedFragments}}.   <!-- Boolean -->
{{referencedFragments}}       <!-- List of referenced-fragment maps -->
```

### Acceso al campo {#field-access}

Cómo acceder a los campos:

```handlebars
{{{fields.fieldName}}}                    <!-- Direct field -->
{{{fields.author.name}}}                  <!-- Nested Content Fragment field -->
{{{fields.author.org.address.city}}}      <!-- Multi-level nesting -->
{{{fields.tags.[0]}}}                     <!-- Array by index -->
{{#each fields.tags}}...{{/each}}         <!-- Array iteration -->
{{{fields.authors.[0].name}}}             <!-- Multi-valued Content Fragment reference -->
```

### Flujo de control {#control-flow}

Flujo de control:

```handlebars
{{#if condition}}...{{/if}}               <!-- Conditional -->
{{#if condition}}...{{else}}...{{/if}}    <!-- If/else -->
{{#unless condition}}...{{/unless}}       <!-- Negative conditional -->
{{#each array}}...{{/each}}               <!-- Iteration -->
{{#each array}}...{{else}}...{{/each}}    <!-- Iteration with fallback -->
{{#with object}}...{{/with}}              <!-- Change scope -->
```

### Variables de bucle {#loop-variables}

Las variables de bucle:

```handlebars
{{@index}}        <!-- 0-based index -->
{{@number}}       <!-- 1-based index -->
{{@first}}        <!-- true for first item -->
{{@last}}         <!-- true for last item -->
{{@key}}          <!-- Object property name -->
{{this}}          <!-- Current item -->
{{../parent}}     <!-- Access parent scope -->
```

### Ayudantes de plantilla personalizados {#custom-template-helpers}

Los ayudantes de plantilla personalizados:

```handlebars
{{{asset fields.image class="css-class"}}}                <!-- Image with class -->
{{{asset fields.image class="c1" id="my-id"}}}            <!-- Image with multiple attrs -->
{{{asset fields.image alt="Custom alt text"}}}            <!-- Override alt text -->
{{{asset fields.image loading="lazy" data-x="val"}}}      <!-- Custom attributes -->

{{{text fields.title class="title-class"}}}               <!-- Span with class -->
{{{text fields.price class="price" id="p1"}}}             <!-- Span with multiple attrs -->
{{{text this class="item" data-index=@index}}}            <!-- In loops -->
```

## Recursos adicionales {#additional-resources}

Hay recursos adicionales disponibles:

* [Documentación de Handlebars](https://handlebarsjs.com/)
* [Ayudantes integrados de Handlebars](https://handlebarsjs.com/guide/builtin-helpers.html)
* [Documentación de fragmentos de contenido de AEM](/help/sites-cloud/administering/content-fragments/overview.md)

