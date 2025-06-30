---
title: Modelado de contenido para la creación WYSIWYG con proyectos de Edge Delivery Services
description: Aprenda cómo funciona el modelado de contenido para la creación WYSIWYG con proyectos de Edge Delivery Services y cómo modelar su propio contenido.
exl-id: e68b09c5-4778-4932-8c40-84693db892fd
feature: Edge Delivery Services
role: Admin, Architect, Developer
index: false
hide: true
hidefromtoc: true
source-git-commit: fecbebde808c545a84889da5610a79c088f2f459
workflow-type: ht
source-wordcount: '2160'
ht-degree: 100%

---


# Modelado de contenido para la creación WYSIWYG con proyectos de Edge Delivery Services {#content-modeling}

Aprenda cómo funciona el modelado de contenido para la creación WYSIWYG con proyectos de Edge Delivery Services y cómo modelar su propio contenido.

## Requisitos previos {#prerequisites}

Los proyectos que utilizan la creación WYSIWYG con Edge Delivery Services heredan la mayoría de los mecanismos de cualquier otro proyecto de Edge Delivery Services, independientemente de la fuente de contenido o del [método de creación](/help/edge/wysiwyg-authoring/authoring.md).

Antes de empezar a modelar el contenido de su proyecto, asegúrese de leer primero la siguiente documentación.

* [Introducción: Tutorial para desarrolladores](/help/edge/developer/tutorial.md)
* [Marcado, secciones, bloques y bloqueo automático](/help/edge/developer/markup-sections-blocks.md)
* [Colección de bloqueos](/help/edge/developer/block-collection.md)

Es esencial comprender estos conceptos para llegar a un modelo de contenido atractivo que funcione de manera independiente de la fuente de contenido. Este documento proporciona detalles sobre los mecanismos implementados específicamente para la creación WYSIWYG.

## Contenido predeterminado {#default-content}

**Contenido predeterminado** es el contenido que un autor colocaría intuitivamente en una página sin añadir ninguna semántica adicional. Esto incluye texto, encabezados, vínculos e imágenes. Dicho contenido se explica por sí mismo en su función y propósito.

En AEM, este contenido se implementa como componentes con modelos muy simples y predefinidos, que incluyen todo lo que se puede serializar en Markdown y HTML.

* **Texto**: texto enriquecido (incluidos elementos de lista y texto fuerte o en cursiva)
* **Título**: texto, tipo (h1-h6)
* **Imagen**: origen, descripción
* **Botón**: texto, título, dirección URL, tipo (predeterminado, principal, secundario)

El modelo de estos componentes forma parte del [elemento repetitivo para la creación WYSIWYG con Edge Delivery Services.](https://github.com/adobe-rnd/aem-boilerplate-xwalk/blob/main/component-models.json#L2-L112)

## Bloques {#blocks}

Los bloques se utilizan para crear contenido enriquecido con estilos y funcionalidades específicos. A diferencia del contenido predeterminado, los bloques sí requieren una semántica adicional.

Los bloques son esencialmente fragmentos de contenido decorados por JavaScript y diseñados con una hoja de estilo.

### Definición de modelo de bloque {#model-definition}

Cuando se utiliza la creación WYSIWYG con Edge Delivery Services, el contenido de los bloques debe modelarse explícitamente para poder proporcionar al autor la interfaz para crear contenido. Básicamente, debe crear un modelo para que la interfaz de usuario de creación de IU sepa qué opciones presentar al autor en función del bloque.

El archivo [`component-models.json`](https://github.com/adobe-rnd/aem-boilerplate-xwalk/blob/main/component-models.json) define el modelo de bloques. Los campos definidos en el modelo de componente se conservan como propiedades en AEM y se representan como celdas en la tabla que compone un bloque.

```json
{
  "id": "hero",
  "fields": [
    {
      "component": "reference",
      "valueType": "string",
      "name": "image",
      "label": "Image",
      "multi": false
    },
    {
      "component": "text-input",
      "valueType": "string",
      "name": "imageAlt",
      "label": "Alt",
      "value": ""
    },
    {
      "component": "text-area",
      "name": "text",
      "value": "",
      "label": "Text",
      "valueType": "string"
    }
  ]
}
```

Tenga en cuenta que no todos los bloques deben tener un modelo. Algunos bloques son simplemente [contenedores](#container) de una lista de tareas secundarias, donde cada elemento secundario tiene su propio modelo.

También es necesario definir qué bloques existen y se pueden añadir a una página con el editor universal. El archivo [`component-definitions.json`](/help/implementing/universal-editor/component-definition.md) enumera los componentes tal como están disponibles en el editor universal.

```json
{
  "title": "Hero",
  "id": "hero",
  "plugins": {
    "xwalk": {
      "page": {
        "resourceType": "core/franklin/components/block/v1/block",
        "template": {
          "name": "Hero",
          "model": "hero"
        }
      }
    }
  }
}
```

Es posible utilizar un modelo para muchos bloques. Por ejemplo, algunos bloques pueden compartir un modelo que define un texto y una imagen.

Para cada bloque, el desarrollador:

* Debe utilizar el tipo de recurso `core/franklin/components/block/v1/block`, la implementación genérica de la lógica de bloque en AEM.
* Debe definir el nombre del bloque, que se procesará en el encabezado de tabla del bloque.
   * El nombre del bloque se utiliza para recuperar el estilo y el script adecuados para decorar el bloque.
* Puede definir un [ID de modelo](/help/implementing/universal-editor/field-types.md#model-structure).
   * El ID de modelo es una referencia al modelo del componente, que define los campos disponibles para el autor en el panel de propiedades.
* Puede definir un [ID de filtro](/help/implementing/universal-editor/filtering.md).
   * El ID de filtro es una referencia al filtro del componente, que permite cambiar el comportamiento de creación, por ejemplo, al limitar qué elementos secundarios se pueden añadir al bloque o a la sección, o qué funciones RTE están habilitadas.

Toda esta información se almacena en AEM cuando se añade un bloque a una página. Si falta el tipo de recurso o el nombre del bloque, el bloque no se procesará en la página.

>[!WARNING]
>
>Si bien es posible, no es necesario o recomendable implementar componentes de AEM personalizados. Los componentes de Edge Delivery Services proporcionados por AEM son suficientes y ofrecen determinados mecanismos de protección para facilitar el desarrollo.
>
>Los componentes proporcionados por AEM representan un marcado que puede consumir [helix-html2md](https://github.com/adobe/helix-html2md) al publicar en Edge Delivery Services y [aem.js](https://github.com/adobe/aem-boilerplate/blob/main/scripts/aem.js) al cargar una página en el editor universal. El marcado es el contrato estable entre AEM y las demás partes del sistema, y no permite personalizaciones. Por este motivo, los proyectos no deben cambiar los componentes y no deben utilizar componentes personalizados.

### Estructura del bloque {#block-structure}

Las propiedades de los bloques se [definen en los modelos de componentes](#model-definition) y persisten como tal en el caso de AEM. Las propiedades se representan como celdas en la estructura de tipo tabla del bloque.

#### Bloques simples {#simple}

En la forma más sencilla, un bloque procesa cada propiedad en una sola fila/columna en el orden en que las propiedades se definen en el modelo.

En el ejemplo siguiente, la imagen se define primero en el modelo y el texto después. Por lo tanto, se representan con la imagen primero y el texto después.

>[!BEGINTABS]

>[!TAB Datos]

```json
{
  "name": "Hero",
  "model": "hero",
  "image": "/content/dam/image.png",
  "imageAlt": "Helix - a shape like a corkscrew",
  "text": "<h1>Welcome to AEM</h1>"
}
```

>[!TAB Marcado]

```html
<div class="hero">
  <div>
    <div>
      <picture>
        <img src="/content/dam/image.png" alt="Helix - a shape like a corkscrew">
      </picture>
    </div>
  </div>
  <div>
    <div>
      <h1>Welcome to AEM</h1>
    </div>
  </div>
</div>
```

>[!TAB Tabla]

```text
+---------------------------------------------+
| Hero                                        |
+=============================================+
| ![Helix - a shape like a corkscrew][image0] |
+---------------------------------------------+
| # Welcome to AEM                            |
+---------------------------------------------+
```

>[!ENDTABS]

Es posible que observe que algunos tipos de valores permiten inferir semántica en el marcado y que las propiedades se combinan en celdas individuales. Este comportamiento se describe en la sección [Inferencia de tipo](#type-inference).

#### Bloque clave-valor {#key-value}

En muchos casos, se recomienda decorar el marcado semántico procesado, añadir nombres de clase CSS, añadir nuevos nodos o moverlos por el DOM y aplicar estilos.

Sin embargo, en otros casos, el bloque se lee como una configuración de par clave-valor.

Un ejemplo de esto son los [metadatos de sección](/help/edge/developer/markup-sections-blocks.md#sections). En este caso de uso, el bloque puede configurarse para que se procese como una tabla de pares clave-valor. Consulte la sección [Secciones y metadatos de sección](#sections-metadata) para obtener más información.

>[!BEGINTABS]

>[!TAB Datos]

```json
{
  "name": "Featured Articles",
  "model": "spreadsheet-input",
  "key-value": true,
  "source": "/content/site/articles.json",
  "keywords": ['Developer','Courses'],
  "limit": 4
}
```

>[!TAB Marcado]

```html
<div class="featured-articles">
  <div>
    <div>source</div>
    <div><a href="/content/site/articles.json">/content/site/articles.json</a></div>
  </div>
  <div>
    <div>keywords</div>
    <div>Developer,Courses</div>
  <div>
  <div>
    <div>limit</div>
    <div>4</div>
  </div>
</div>
```

>[!TAB Tabla]

```text
+-----------------------------------------------------------------------+
| Featured Articles                                                     |
+=======================================================================+
| source   | [/content/site/articles.json](/content/site/articles.json) |
+-----------------------------------------------------------------------+
| keywords | Developer,Courses                                          |
+-----------------------------------------------------------------------+
| limit    | 4                                                          |
+-----------------------------------------------------------------------+
```

>[!ENDTABS]

#### Bloques de contenedor {#container}

Ambas estructuras anteriores tienen una sola dimensión: la lista de propiedades. Los bloques contenedores permiten añadir tareas secundarias (normalmente del mismo tipo o modelo) y, por lo tanto, son bidimensionales. Estos bloques siguen admitiendo sus propias propiedades, representadas como filas con una sola columna en primer lugar. Pero también permiten añadir tareas secundarias, para los que cada elemento se procesa como fila y cada propiedad como columna dentro de esa fila.

En el siguiente ejemplo, un bloque acepta una lista de iconos vinculados como tareas secundarias, donde cada icono vinculado tiene una imagen y un vínculo. Observe que el [ID de filtro](/help/implementing/universal-editor/filtering.md) se establece en los datos del bloque para hacer referencia a la configuración del filtro.

>[!BEGINTABS]

>[!TAB Datos]

```json
{
  "name": "Our Partners",
  "model": "text-only",
  "filter": "our-partners",
  "text": "<p>Our community of partners is ...</p>",
  "item_0": {
    "model": "linked-icon",
    "image": "/content/dam/partners/foo.png",
    "imageAlt": "Icon of Foo",
    "link": "https://foo.com/"
  },
  "item_1": {
    "model": "linked-icon"
    "image": "/content/dam/partners/bar.png",
    "imageAlt": "Icon of Bar",
    "link": "https://bar.com"
  }
}
```

>[!TAB Marcado]

```html
<div class="our-partners">
  <div>
    <div>
        Our community of partners is ...
    </div>
  </div>
  <div>
    <div>
      <picture>
         <img src="/content/dam/partners/foo.png" alt="Icon of Foo">
      </picture>
    </div>
    <div>
      <a href="https://foo.com">https://foo.com</a>
    </div>
  </div>
  <div>
    <div>
      <picture>
         <img src="/content/dam/partners/bar.png" alt="Icon of Bar">
      </picture>
    </div>
    <div>
      <a href="https://bar.com">https://bar.com</a>
    </div>
  </div>
</div>
```

>[!TAB Tabla]

```text
+------------------------------------------------------------ +
| Our Partners                                                |
+=============================================================+
| Our community of partners is ...                            |
+-------------------------------------------------------------+
| ![Icon of Foo][image0] | [https://foo.com](https://foo.com) |
+-------------------------------------------------------------+
| ![Icon of Bar][image1] | [https://bar.com](https://bar.com) |
+-------------------------------------------------------------+
```

>[!ENDTABS]

### Creación de modelos de contenido semántico para bloques {#creating-content-models}

Con la [explicación de la mecánica de la estructura de bloques](#block-structure), es posible crear un modelo de contenido que asigne el contenido persistente en AEM de uno a uno en el nivel de envío.

Al principio de cada proyecto, se debe considerar cuidadosamente un modelo de contenido para cada bloque. Debe ser independiente del origen de contenido y de la experiencia de creación para permitir a los autores cambiarlos o combinarlos al reutilizar implementaciones y estilos de bloque. Puede encontrar más información y sugerencias generales en el [Modelo de David (toma 2)](https://www.aem.live/docs/davidsmodel). Más específicamente, la [colección en bloque](/help/edge/developer/block-collection.md) contiene un amplio conjunto de modelos de contenido para casos de uso específicos de patrones de interfaz de usuario comunes.

Para la creación WYSIWYG con Edge Delivery Services, esto plantea la cuestión de cómo servir un modelo de contenido semántico atractivo cuando la información se crea con formularios compuestos de varios campos en lugar de editar el marcado semántico en contexto como texto enriquecido.

Para resolver este problema, existen tres métodos que facilitan la creación de un modelo de contenido atractivo:

* [Inferencia de tipo](#type-inference)
* [Contraer campo](#field-collapse)
* [Agrupación de elementos](#element-grouping)

>[!NOTE]
>
>Las implementaciones de bloque pueden deconstruir el contenido y reemplazar el bloque con un DOM procesado por el lado del cliente. Aunque esto es posible e intuitivo para un desarrollador, no es la práctica recomendada para los Edge Delivery Services.

#### Inferencia de tipo {#type-inference}

Para algunos valores podemos inferir el significado semántico a partir de los valores en sí. Estos valores incluyen:

* **Imágenes**: si una referencia a un recurso en AEM es un recurso con un tipo MIME que comience por `image/`, la referencia se representa como `<picture><img src="${reference}"></picture>`.
* **Vínculos**: si una referencia existe en AEM y no es una imagen, o si el valor empieza por `https?://`  o `#`, la referencia se representa como `<a href="${reference}">${reference}</a>` .
* **Texto enriquecido**: si un valor recortado comienza con un párrafo (`p`, `ul`, `ol`, `h1`-`h6`, etc.), el valor se representa como texto enriquecido.
* **Nombres de clase**: la propiedad `classes` se trata como [opciones de bloque](/help/edge/developer/markup-sections-blocks.md#block-options) y se representa en el encabezado de tabla para [bloques simples,](#simple) o como lista de valores para elementos en un [bloque de contenedor](#container). Es útil si quiere [dar un estilo diferente a un bloque](/help/edge/wysiwyg-authoring/create-block.md#block-options), pero no necesita crear un bloque completamente nuevo.
* **Listas de valores**: si un valor es una propiedad de varios valores y el primer valor no es ninguno de los anteriores, todos los valores se concatenan como una lista separada por comas.

Todo lo demás se procesará como texto sin formato.

#### Contraer campo {#field-collapse}

La contracción de campo es el mecanismo para combinar varios valores de campo en un único elemento semántico basado en una convención de nomenclatura que utiliza los sufijos `Title`, `Type`, `MimeType`, `Alt` y `Text` (todos con distinción de mayúsculas y minúsculas). Cualquier propiedad que termine con cualquiera de esos sufijos no se considerará un valor, sino un atributo de otra propiedad.

##### Imágenes {#image-collapse}

>[!BEGINTABS]

>[!TAB Datos]

```json
{
  "image": "/content/dam/red-car.png",
  "imageAlt: "A red card on a road"
}
```

>[!TAB Marcado]

```html
<picture>
  <img src="/content/dam/red-car.png" alt="A red car on a road">
</picture>
```

>[!TAB Tabla]

```text
![A red car on a road][image0]
```

>[!ENDTABS]

##### Vínculos y botones {#links-buttons-collapse}

>[!BEGINTABS]

>[!TAB Datos]

```json
{
  "link": "https://www.adobe.com",
  "linkTitle": "Navigate to adobe.com",
  "linkText": "adobe.com",
  "linkType": "primary"
}
```

>[!TAB Marcado]

No `linkType` ni `linkType=default`

```html
<a href="https://www.adobe.com" title="Navigate to adobe.com">adobe.com</a>
```

`linkType=primary`

```html
<strong>
  <a href="https://www.adobe.com" title="Navigate to adobe.com">adobe.com</a>
</strong>
```

`linkType=secondary`

```html
<em>
  <a href="https://www.adobe.com" title="Navigate to adobe.com">adobe.com</a>
</em>
```

>[!TAB Tabla]

```text
[adobe.com](https://www.adobe.com "Navigate to adobe.com")
**[adobe.com](https://www.adobe.com "Navigate to adobe.com")**
_[adobe.com](https://www.adobe.com "Navigate to adobe.com")_
```

>[!ENDTABS]

##### Encabezados {#headings-collapse}

>[!BEGINTABS]

>[!TAB Datos]

```json
{
  "heading": "Getting started",
  "headingType": "h2"
}
```

>[!TAB Marcado]

```html
<h2>Getting started</h2>
```

>[!TAB Tabla]

```text
## Getting started
```

>[!ENDTABS]

#### Agrupación de elementos {#element-grouping}

Mientras que la [contracción de campo](#field-collapse) consiste en combinar varias propiedades en un único elemento semántico, la agrupación de elementos consiste en concatenar varios elementos semánticos en una sola celda. Esto resulta especialmente útil en casos de uso en los que el autor tuviera una restricción en cuanto al tipo y al número de elementos que puede crear.

Por ejemplo, el componente de teaser puede permitir al autor crear solo un subtítulo, un título y una descripción de párrafo único combinados con un máximo de dos botones de llamada a la acción. Al agrupar estos elementos, se obtiene un marcado semántico al que se puede dar estilo sin tener que realizar ninguna otra acción.

La agrupación de elementos utiliza una convención de nomenclatura, en la que el nombre del grupo se separa de cada propiedad del grupo mediante un guion bajo. La contracción de campos de las propiedades de un grupo funciona como se describió anteriormente.

>[!BEGINTABS]

>[!TAB Datos]

```json
{
  "name": "teaser",
  "model": "teaser",
  "image": "/content/dam/teaser-background.png",
  "imageAlt": "A group of people sitting on a stage",
  "teaserText_subtitle": "Adobe Experience Cloud"
  "teaserText_title": "Meet the Experts"
  "teaserText_titleType": "h2"
  "teaserText_description": "<p>Join us in this ask me everything session...</p>"
  "teaserText_cta1": "https://link.to/more-details",
  "teaserText_cta1Text": "More Details"
  "teaserText_cta2": "https://link.to/sign-up",
  "teaserText_cta2Text": "RSVP",
  "teaserText_cta2Type": "primary"
}
```

>[!TAB Marcado]

```html
<div class="teaser">
  <div>
    <div>
      <picture>
        <img src="/content/dam/teaser-background.png" alt="A group of people sitting on a stage">
      </picture>
    </div>
  </div>
  <div>
    <div>
      <p>Adobe Experience Cloud</p>
      <h2>Meet the Experts</h2>
      <p>Join us in this ask me everything session ...</p>
      <p><a href="https://link.to/more-details">More Details</a></p>
      <p><strong><a href="https://link.to/sign-up">RSVP</a></strong></p>
    </div>
  </div>
</div>
```

>[!TAB Tabla]

```text
+-------------------------------------------------+
| Teaser                                          |
+=================================================+
| ![A group of people sitting on a stage][image0] |
+-------------------------------------------------+
| Adobe Experience Cloud                          |
| ## Meet the Experts                             |
| Join us in this ask me everything session ...   |
| [More Details](https://link.to/more-details)    |
| [RSVP](https://link.to/sign-up)                 |
+-------------------------------------------------+
```

>[!ENDTABS]

## Secciones y metadatos de sección {#sections-metadata}

De la misma manera que un desarrollador puede definir y modelar varios [bloques](#blocks), puede definir diferentes secciones.

El modelo de contenido de Edge Delivery Services permite deliberadamente un solo nivel de anidación, que es cualquier contenido o bloque predeterminado contenido en una sección. Esto significa que, para tener componentes visuales más complejos que puedan contener otros componentes, deben modelarse como secciones y combinarse utilizando el bloqueo automático del lado del cliente. Ejemplos típicos de ello son las pestañas y las secciones contraíbles como acordeones.

Una sección se puede definir del mismo modo que un bloque, pero con el tipo de recurso de `core/franklin/components/section/v1/section`. Las secciones pueden tener un nombre y un [ID de filtro](/help/implementing/universal-editor/filtering.md), que solo utiliza el [editor universal](/help/implementing/universal-editor/introduction.md), así como un [ID de modelo](/help/implementing/universal-editor/field-types.md#model-structure), que se utiliza para procesar los metadatos de la sección. El modelo es, de este modo, el modelo del bloque de metadatos de sección, que se anexará automáticamente a una sección como bloque clave-valor si no está vacío.

El [ID de modelo](/help/implementing/universal-editor/field-types.md#model-structure) y [ID de filtro](/help/implementing/universal-editor/filtering.md) de la sección predeterminada es `section`. Se puede utilizar para modificar el comportamiento de la sección predeterminada. En el siguiente ejemplo se agregan algunos estilos y una imagen de fondo al modelo de metadatos de sección.

```json
{
  "id": "section",
  "fields": [
    {
      "component": "multiselect",
      "name": "style",
      "value": "",
      "label": "Style",
      "valueType": "string",
      "options": [
        {
          "name": "Fade in Background",
          "value": "fade-in"
        },
        {
          "name": "Highlight",
          "value": "highlight"
        }
      ]
    },
    {
      "component": "reference",
      "valueType": "string",
      "name": "background",
      "label": "Image",
      "multi": false
    }
  ]
}
```

En el siguiente ejemplo se define una sección de pestañas, que se puede utilizar para crear un bloque de pestañas combinando secciones consecutivas con un atributo de datos de título de pestaña en un bloque de pestañas durante el bloqueo automático.

```json
{
  "title": "Tab",
  "id": "tab",
  "plugins": {
    "xwalk": {
      "page": {
        "resourceType": "core/franklin/components/section/v1/section",
        "template": {
          "name": "Tab",
          "model": "tab",
          "filter": "section"
        }
      }
    }
  }
}
```

## Metadatos de página {#page-metadata}

Los documentos pueden tener un [bloque de metadatos](https://www.aem.live/developer/block-collection/metadata) de página, que se utiliza para definir qué elementos `<meta>` se procesan en el `<head>` de una página. Las propiedades de página de las páginas en AEM as a Cloud Service se asignan a aquellas que están disponibles de forma predeterminada para Edge Delivery Services, como `title`, `description`, `keywords`, etc.

Antes de continuar explorando cómo definir sus propios metadatos, revise los siguientes documentos para comprender primero el concepto de metadatos de página.

* [Metadatos](https://www.aem.live/developer/block-collection/metadata)
* [Metadatos por lotes](/help/edge/docs/bulk-metadata.md)

También es posible definir metadatos de página adicionales de dos formas.

### Hojas de cálculo de metadatos {#metadata-spreadsheets}

Es posible definir metadatos en función de una ruta o un patrón de ruta de una manera similar a una tabla en AEM as a Cloud Service. Hay disponible una interfaz de usuario de creación para datos de tabla similar a Excel o Google Sheets.

Para obtener más información, consulte el documento [Uso de hojas de cálculo para administrar datos tabulares](/help/edge/wysiwyg-authoring/tabular-data.md).

### Propiedades de página {#page-properties}

Muchas de las propiedades de página predeterminadas disponibles en AEM se asignan a los metadatos de página correspondientes de un documento. Esto incluye, por ejemplo, `title`, `description`, `robots`, `canonical url` o `keywords`. También hay disponibles algunas propiedades específicas de AEM, como las siguientes:

* `cq:lastModified` como `modified-time` en formato ISO8601
* La última vez que se publicó el documento como `published-time` en formato ISO8601
* `cq:tags` como `cq-tags` como una lista separada por comas de los ID de etiqueta.

También es posible definir un modelo de componente para los metadatos de página personalizada, que se pondrán a disposición del autor en el editor universal.

Para ello, cree un modelo de componentes con el ID `page-metadata`.

```json
{
  "id": "page-metadata",
  "fields": [
    {
      "component": "text",
      "name": "theme",
      "label": "Theme"
    }
  ]
}
```

## Siguientes pasos {#next-steps}

Ahora que sabe cómo modelar contenido, puede crear bloques para sus propios Edge Delivery Services con el proyecto de creación de WYSIWYG.

Vea el documento [Creación de bloques instrumentados para su uso con el editor universal](/help/edge/wysiwyg-authoring/create-block.md) para aprender a crear bloques instrumentados para su uso con el editor universal en proyectos de creación WYSIWYG con Edge Delivery Services.

Si ya está familiarizado con la creación de bloques, consulte el documento [Guía de introducción para desarrolladores para la creación WYSIWYG con Edge Delivery Services](/help/edge/wysiwyg-authoring/edge-dev-getting-started.md) para ayudarle a poner en marcha un nuevo sitio de Adobe Experience Manager usando Edge Delivery Services y el editor universal para la creación de contenido.
