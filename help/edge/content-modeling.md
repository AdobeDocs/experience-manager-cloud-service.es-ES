---
title: AEM Modelado de contenido para la creación de con proyectos de Edge Delivery Services
description: AEM Aprenda cómo funciona el modelado de contenido para la creación de contenido con proyectos de Edge Delivery Services y para crear su propio contenido.
source-git-commit: e9c882926baee001170bad2265a1085e03cdbedf
workflow-type: tm+mt
source-wordcount: '2097'
ht-degree: 0%

---


# AEM Modelado de contenido para la creación de con proyectos de Edge Delivery Services {#content-modeling}

AEM Aprenda cómo funciona el modelado de contenido para la creación de contenido con proyectos de Edge Delivery Services y para crear su propio contenido.

{{aem-authoring-edge-early-access}}

## Requisitos previos {#prerequisites}

AEM Los proyectos que utilizan la creación de segmentos con Edge Delivery Services heredan la mayoría de los mecanismos de cualquier otro proyecto de Edge Delivery Services, independientemente de la fuente de contenido o [método de creación.](/help/edge/authoring.md)

Antes de empezar a modelar contenido para el proyecto, asegúrese de leer primero la siguiente documentación.

* [Introducción: Tutorial para desarrolladores](/help/edge/developer/tutorial.md)
* [Marcado, secciones, bloques y bloqueo automático](/help/edge/developer/markup-sections-blocks.md)
* [Colección de bloqueos](/help/edge/developer/block-collection.md)

Es esencial comprender estos conceptos para llegar a un modelo de contenido atractivo que funcione de manera independiente de la fuente de contenido. AEM Este documento proporciona detalles sobre la mecánica implementada específicamente para la creación de.

## Contenido predeterminado {#default-content}

**Contenido predeterminado** es el contenido que un autor pondría intuitivamente en una página sin añadir ninguna semántica adicional. Esto incluye texto, encabezados, vínculos e imágenes. Dicho contenido se explica por sí mismo en su función y propósito.

AEM En la práctica, este contenido se implementa como componentes con modelos muy simples y predefinidos, que incluyen todo lo que se puede serializar en Markdown y HTML.

* **Texto**: texto enriquecido (incluidos elementos de lista y texto fuerte o en cursiva)
* **Título**: texto, tipo (h1-h6)
* **Imagen**: origen, descripción
* **Botón**: texto, título, dirección URL, tipo (predeterminado, principal, secundario)

El modelo de estos componentes forma parte del [AEM Plantilla para la creación de experiencias con Edge Delivery Services en la creación de.](https://github.com/adobe-rnd/aem-boilerplate-xwalk/blob/main/component-models.json#L2-L112)

## Bloques {#blocks}

Los bloques se utilizan para crear contenido enriquecido con estilos y funcionalidades específicos. A diferencia del contenido predeterminado, los bloques sí requieren una semántica adicional. Los bloques se pueden comparar con [AEM componentes en el editor de páginas de.](/help/implementing/developing/components/overview.md)

Los bloques son esencialmente fragmentos de contenido decorados por JavaScript y diseñados con una hoja de estilo.

### Definición de modelo de bloque {#model-definition}

AEM Al utilizar la creación de bloques con Edge Delivery Services, el contenido de los bloques debe modelarse explícitamente para proporcionar al autor la interfaz para crear contenido. Básicamente, debe crear un modelo para que la interfaz de usuario de creación sepa qué opciones presentar al autor en función del bloque.

El [`component-models.json`](https://github.com/adobe-rnd/aem-boilerplate-xwalk/blob/main/component-models.json) define el modelo de bloques. AEM Los campos definidos en el modelo de componente se conservan como propiedades en el modelo de datos y se representan como celdas en la tabla que compone un bloque.

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

Tenga en cuenta que no todos los bloques deben tener un modelo. Algunos bloques son simplemente [contenedores](#container) para una lista de elementos secundarios, donde cada elemento secundario tiene su propio modelo.

También es necesario definir qué bloques existen y se pueden añadir a una página con el editor universal. El [`component-definitions.json`](https://github.com/adobe-rnd/aem-boilerplate-xwalk/blob/main/component-definition.json) Este archivo enumera los componentes tal como están disponibles en el editor universal.

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

* Debe utilizar el `core/franklin/components/block/v1/block` AEM tipo de recurso, la implementación genérica de la lógica de bloque en la aplicación de tipo de recurso de tipo de recurso de tipo de.
* Debe definir el nombre del bloque, que se procesará en el encabezado de tabla del bloque.
   * El nombre del bloque se utiliza para recuperar el estilo y la secuencia de comandos adecuados para decorar el bloque.
* Puede definir un [ID de modelo.](/help/implementing/universal-editor/field-types.md#model-structure)
   * El ID de modelo es una referencia al modelo del componente, que define los campos disponibles para el autor en el carril de propiedades.
* Puede definir un [ID de filtro.](/help/implementing/universal-editor/customizing.md#filtering-components)
   * El ID de filtro es una referencia al filtro del componente, que permite cambiar el comportamiento de creación, por ejemplo, limitando qué elementos secundarios se pueden añadir al bloque o la sección, o qué funciones RTE están habilitadas.

AEM Toda esta información se almacena en los datos cuando se agrega un bloque de a una página de la lista de direcciones de correo electrónico. Si falta el tipo de recurso o el nombre del bloque, el bloque no se procesará en la página.

>[!WARNING]
>
>AEM Aunque es posible, no es necesario ni recomendado implementar componentes personalizados de la. Los componentes para los Edge Delivery Services AEM proporcionados por los son suficientes y ofrecen ciertas barandillas de protección para facilitar el desarrollo.
>
>AEM Los componentes proporcionados por el usuario representan un marcado que se puede consumir por [helix-html2md](https://github.com/adobe/helix-html2md) al publicar en Edge Delivery Services y por [aem.js](https://github.com/adobe/aem-boilerplate/blob/main/scripts/aem.js) al cargar una página en el editor universal. AEM El marcado es el contrato estable entre el usuario y las demás partes del sistema, y no permite personalizaciones. Por este motivo, los proyectos no deben cambiar los componentes y no deben utilizar componentes personalizados.

### Estructura del bloque {#block-structure}

Las propiedades de los bloques son [definido en los modelos de componentes](#model-definition) AEM y persistió como tal en el caso de los. Las propiedades se representan como celdas en la estructura de tipo tabla del bloque.

#### Bloques simples {#simple}

En la forma más sencilla, un bloque procesa cada propiedad en una sola fila/columna en el orden en que las propiedades se definen en el modelo.

En el ejemplo siguiente, la imagen se define primero en el modelo y el texto segundo. Por lo tanto, se representan con la imagen primero y el texto segundo.

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

Es posible que observe que algunos tipos de valores permiten inferir semántica en el marcado y que las propiedades se combinan en celdas individuales. Este comportamiento se describe en la sección [Inferencia de tipo.](#type-inference)

#### Bloque clave-valor {#key-value}

En muchos casos, se recomienda decorar el marcado semántico procesado, agregar nombres de clase CSS, agregar nuevos nodos o moverlos por el DOM y aplicar estilos.

Sin embargo, en otros casos, el bloque se lee como una configuración de par clave-valor.

Un ejemplo de esto es el [metadatos de sección.](/help/edge/developer/markup-sections-blocks.md#sections) En este caso de uso, el bloque se puede configurar para que se represente como una tabla de pares clave-valor. Consulte la sección [Secciones y metadatos de sección](#sections-metadata) para obtener más información.

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

Ambas estructuras anteriores tienen una sola dimensión: la lista de propiedades. Los bloques contenedores permiten agregar elementos secundarios (normalmente del mismo tipo o modelo) y, por lo tanto, son bidimensionales. Estos bloques siguen admitiendo sus propias propiedades, representadas como filas con una sola columna en primer lugar. Pero también permiten agregar elementos secundarios, para los que cada elemento se procesa como fila y cada propiedad como columna dentro de esa fila.

En el siguiente ejemplo, un bloque acepta una lista de iconos vinculados como elementos secundarios, donde cada icono vinculado tiene una imagen y un vínculo. Observe el [ID de filtro](/help/implementing/universal-editor/customizing.md#filtering-components) se establece en los datos del bloque para hacer referencia a la configuración del filtro.

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

Con el [mecánica de la estructura de bloques explicada,](#block-structure) AEM es posible crear un modelo de contenido que asigne el contenido persistido en el nivel de envío de uno a uno en el nivel de entrega de la entrega de la aplicación de forma individual de la.

Al principio de cada proyecto, se debe considerar cuidadosamente un modelo de contenido para cada bloque. Debe ser independiente del origen de contenido y de la experiencia de creación para permitir a los autores cambiarlos o combinarlos al reutilizar implementaciones y estilos de bloque. Puede encontrar más información y sugerencias generales en [David&#39;s Model (toma 2).](https://www.aem.live/docs/davidsmodel) Más específicamente, la variable [colección en bloque](/help/edge/developer/block-collection.md) contiene un amplio conjunto de modelos de contenido para casos de uso específicos de patrones de interfaz de usuario comunes.

AEM Para la creación de formularios con Edge Delivery Services, esto plantea la cuestión de cómo servir un modelo de contenido semántico atractivo cuando la información se crea con formularios compuestos de varios campos en lugar de editar marcado semántico en contexto como texto enriquecido.

Para resolver este problema, existen tres métodos que facilitan la creación de un modelo de contenido atractivo:

* [Inferencia de tipo](#type-inference)
* [Contraer campo](#field-collapse)
* [Agrupación de elementos](#element-grouping)

>[!NOTE]
>
>Las implementaciones de bloque pueden deconstruir el contenido y reemplazar el bloque con un DOM procesado por el lado del cliente. Aunque esto es posible e intuitivo para un desarrollador, no es la práctica recomendada para los Edge Delivery Services.

#### Inferencia de tipo {#type-inference}

Para algunos valores podemos inferir el significado semántico a partir de los valores en sí. Estos valores incluyen:

* **Imágenes** AEM : Si una referencia a un recurso en la es un recurso con un tipo MIME que comience por `image/`, la referencia se representa como `<picture><img src="${reference}"></picture>`.
* **Vínculos** AEM - Si una referencia existe en la y no es una imagen, o si el valor empieza por `https?://`  o `#`, la referencia se representa como `<a href="${reference}">${reference}</a>` .
* **Texto enriquecido** - Si un valor recortado comienza con un párrafo (`p`, `ul`, `ol`, `h1`-`h6`, etc.), el valor se representa como texto enriquecido.
* **Nombres de clase** - El `classes` La propiedad se trata como opciones de bloque y se representa en el encabezado de tabla de [bloques simples,](#simple) o como lista de valores para elementos en una [bloque de contenedor.](#container)
* **Listas de valores** : Si un valor es una propiedad de varios valores y el primer valor no es ninguno de los anteriores, todos los valores se concatenan como una lista separada por comas.

Todo lo demás se procesará como texto sin formato.

#### Contraer campo {#field-collapse}

El colapso de campo es el mecanismo para combinar varios valores de campo en un único elemento semántico basado en una convención de nombres que utiliza los sufijos `Title`, `Type`, `Alt`, y `Text` (con distinción de mayúsculas y minúsculas). Cualquier propiedad que termine con cualquiera de esos sufijos no se considerará un valor, sino como un atributo de otra propiedad.

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

No `linkType`, o `linkType=default`

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

While [contracción de campo](#field-collapse) Cuando se trata de combinar varias propiedades en un único elemento semántico, la agrupación de elementos consiste en concatenar varios elementos semánticos en una sola celda. Esto resulta especialmente útil en casos de uso en los que el autor debe estar restringido en el tipo y el número de elementos que puede crear.

Por ejemplo, un componente teaser puede permitir al autor crear únicamente un subtítulo, un título y una descripción de párrafo único combinados con un máximo de dos botones de llamada a la acción. Al agrupar estos elementos, se obtiene un marcado semántico al que se puede dar estilo sin tener que realizar ninguna acción.

La agrupación de elementos utiliza una convención de nombres, en la que el nombre del grupo se separa de cada propiedad del grupo mediante un guion bajo. La contracción de campos de las propiedades de un grupo funciona como se describió anteriormente.

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
| ## Welcome to AEM                               |
| Join us in this ask me everything session ...   |
| [More Details](https://link.to/more-details)    |
| [RSVP](https://link.to/sign-up)                 |
+-------------------------------------------------+
```

>[!ENDTABS]

## Secciones y metadatos de sección {#sections-metadata}

Del mismo modo que un desarrollador puede definir y modelar varios [bloques,](#blocks) pueden definir diferentes secciones.

El modelo de contenido de los Edge Delivery Services permite deliberadamente un solo nivel de anidación, que es cualquier contenido o bloque predeterminado contenido en una sección. Esto significa que, para tener componentes visuales más complejos que puedan contener otros componentes, deben modelarse como secciones y combinarse utilizando el bloqueo automático del lado del cliente. Ejemplos típicos de esto son las pestañas y las secciones contraíbles como los acordeones.

Una sección se puede definir del mismo modo que un bloque, pero con el tipo de recurso de `core/franklin/components/section/v1/section`. Las secciones pueden tener un nombre y un [ID de filtro,](/help/implementing/universal-editor/customizing.md#filtering-components) que utilizan los clientes de [Editor universal](/help/implementing/universal-editor/introduction.md) solo, así como un [ID del modelo,](/help/implementing/universal-editor/field-types.md#model-structure) que se utiliza para procesar los metadatos de la sección. El modelo es, de este modo, el modelo del bloque de metadatos de sección, que se anexará automáticamente a una sección como bloque clave-valor si no está vacío.

El [ID de modelo](/help/implementing/universal-editor/field-types.md#model-structure) y [ID de filtro](/help/implementing/universal-editor/customizing.md#filtering-components) de la sección predeterminada es `section`. Se puede utilizar para modificar el comportamiento de la sección predeterminada. En el siguiente ejemplo se agregan algunos estilos y y una imagen de fondo al modelo de metadatos de sección.

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

Los documentos pueden tener una página [bloque de metadatos,](/help/edge/authoring.md#metadata--seo) que se usa para definir qué `<meta>` Los elementos de se representan en `<head>` de una página. AEM Las propiedades de página de las páginas en las que se realiza la publicación en as a Cloud Service se asignan a aquellas que están disponibles de forma predeterminada para los Edge Delivery Services, como `title`, `description`, `keywords`, etc.

Antes de continuar explorando cómo definir sus propios metadatos, revise los siguientes documentos para comprender primero el concepto de metadatos de página.

* [Metadatos](https://www.aem.live/developer/block-collection/metadata)
* [Metadatos por lotes](/help/edge/docs/bulk-metadata.md)

También es posible definir metadatos de página adicionales de dos formas.

### Hojas de cálculo de metadatos {#metadata-spreadsheets}

AEM Es posible definir metadatos por ruta o por patrón de ruta de una manera similar a una tabla en as a Cloud Service. Hay disponible una interfaz de usuario de creación para datos de tabla similar a las hojas de Excel o Google.

Para crear dicha tabla, cree una página y utilice la plantilla Metadatos en la consola Sitios.

En las propiedades de página de la hoja de cálculo, defina los campos de metadatos que necesite junto con la dirección URL. A continuación, agregue metadatos por ruta de página o patrón de ruta de página.

Asegúrese de que la hoja de cálculo también se añada a la asignación de ruta antes de publicarla.

```json
{
  "mappings": [
    "/content/site/:/",
    "/content/site/metadata:/metadata.json"
  ]
}
```

### Propiedades de página {#page-properties}

También es posible definir un modelo de componente para los metadatos de página, que se pondrán a disposición del autor como pestaña del cuadro de diálogo de propiedades de página de AEM Sites.

Para ello, cree un modelo de componentes con la ID `page-metadata`.

```json
{
  "id": "page-metadata",
  "fields": [
    {
      "component": "text-input",
      "name": "theme",
      "label": "Theme"
    }
  ]
}
```

Hay algunos nombres de campo que tienen un significado especial y que se omitirán al servir a la IU del cuadro de diálogo de creación:

* **`cq:tags`** - De forma predeterminada, `cq:tags` no se añaden a los metadatos. Añadiéndolos al `page-metadata` El modelo agregará los ID de etiqueta como una lista separada por comas `tags` metaetiqueta en la cabeza.
* **`cq:lastModified`** - `cq:lastModified` agregará sus datos como `last-modified` a la cabeza.
