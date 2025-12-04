---
title: Configuración del RTE para el editor universal
description: Descubra cómo puede configurar el editor de texto enriquecido (RTE) en el editor universal.
feature: Developing
role: Admin, Developer
exl-id: 350eab0a-f5bc-49c0-8e4d-4a36a12030a1
source-git-commit: edcba16831a40bd03c1413b33794268b6466d822
workflow-type: tm+mt
source-wordcount: '462'
ht-degree: 1%

---

# Configuración del RTE para el editor universal {#configure-rte}

Descubra cómo puede configurar el editor de texto enriquecido (RTE) en el editor universal.

## Información general {#overview}

El editor universal proporciona un editor de texto enriquecido (RTE) tanto en el sitio como en el panel de propiedades para permitir a los autores aplicar cambios de formato a medida que editan su texto.

Este RTE se puede configurar usando [filtros de componente.](/help/implementing/universal-editor/filtering.md) Este documento describe qué opciones de configuración están disponibles junto con ejemplos.

## Estructura de configuración {#structure}

La configuración de RTE consta de dos partes:

* [`toolbar`](#toolbar): la configuración de la barra de herramientas controla qué opciones de edición están disponibles en la interfaz de usuario y cómo están organizadas.
* [`actions`](#actions): la configuración de acciones le permite personalizar el comportamiento y el aspecto de las acciones de edición individuales.

Estas configuraciones se pueden definir como parte de un [filtro de componentes](/help/implementing/universal-editor/filtering.md) con la propiedad `rte`.

```json
[
  {
    "id": "richtext",
    "rte": {
      "toolbar": {
        // Toolbar configuration
      },
      "actions": {
        // Action-specific configurations
      }
    },
    "components": [
      "richtext"
    ]
  }
]
```

## Configuración de barra de herramientas {#toolbar}

La configuración de la barra de herramientas controla qué opciones de edición están disponibles en la interfaz de usuario y cómo están organizadas. Estas son las secciones disponibles

```json
{
  "toolbar": {
    // Text formatting options
    "format": ["bold", "italic", "underline", "strike"],
    // Text alignment options
    "alignment": ["left", "center", "right", "justify"],
    // Text direction options, right-to-left or left-to-right
    "direction": ["rtl", "ltr"],
    // Indentation controls
    "indentation": ["indent", "outdent"],
    // Block-level elements
    "blocks": ["paragraph", "h1", "h2", "h3", "h4", "h5", "h6", "code_block"],
    // List options
    "list": ["bullet_list", "ordered_list"],
    // Content insertion
    "insert": ["link", "unlink", "image"],
    // Superscript/subscript
    "sr_script": ["superscript", "subscript"],
    // Editor utilities
    "editor": ["removeformat"],
    // Section ordering (optional)
    "sections": ["format", "alignment", "list"]
  }
}
```

## Configuración de acciones {#actions}

La configuración de acciones permite personalizar el comportamiento y el aspecto de las acciones de edición individuales. Estas son las secciones disponibles.

### Acciones de formato {#format}

Las acciones de formato se utilizan para aplicar formato y admitir el cambio de etiquetas de HTML para elegir entre variantes semánticas. Las secciones disponibles son las siguientes:

```json
{
  "actions": {
    "bold": {
      "tag": "strong",      // Use <strong> instead of <b>
      "shortcut": "Mod-B",  // Custom keyboard shortcut
      "label": "Make Bold"  // Custom button label 
    },
    "italic": {
      "tag": "em",          // Use <em> instead of <i>
      "shortcut": "Mod-I",
      "label": "Italicize"
    },
    "strike": {
      "tag": "del"          // Use <del> instead of <s>
    }
  }
}
```

### Enumerar acciones {#list}

Las acciones de lista admiten el ajuste de contenido para controlar la estructura de HTML. Las secciones disponibles son las siguientes:

```json
{
  "actions": {
    "bullet_list": {
      "wrapInParagraphs": true,    // <ul><li><p>content</p></li></ul>
      "shortcut": "Mod-Shift-8",   // Custom shortcut
      "label": "Bullet List"       // Custom label
    },
    "ordered_list": {
      "wrapInParagraphs": false,   // <ol><li>content</li></ol> (default)
      "shortcut": "Mod-Shift-9"
    }
  }
}
```

### Acciones de vínculo {#link}

Las acciones de vínculo admiten el control de atributos de destino para administrar el comportamiento del vínculo. Las secciones disponibles son las siguientes:

```json
{
  "actions": {
    "link": {
      "hideTarget": false,       // Show target attribute options (default)
      "shortcut": "Mod-K",       // Custom keyboard shortcut
      "label": "Insert Link"     // Custom button label
    },
    "unlink": {
      "shortcut": "Mod-Shift-K", // Custom keyboard shortcut
      "label": "Remove Link"     // Custom button label
    }
  }
}
```

#### Opciones de configuración de vínculos {#link-options}

* `hideTarget`: `false` (predeterminado): incluye el atributo objetivo en los vínculos, lo que permite `_self`, `_blank`, etc.
* `hideTarget`: `true` - Excluir completamente el atributo de destino de los vínculos

La acción `unlink` solo aparece cuando el cursor se coloca dentro de un vínculo existente. Quita el formato del vínculo y conserva el contenido del texto.

### Acciones de imagen {#image}

Las acciones de imagen admiten el ajuste de elementos de imagen para generar un marcado de imagen interactivo. Las secciones disponibles son las siguientes:

```json
{
  "actions": {
    "image": {
      "wrapInPicture": false,     // Use <img> tag (default)
      "shortcut": "Mod-Shift-I",  // Custom keyboard shortcut
      "label": "Insert Image"     // Custom button label
    }
  }
}
```

#### Opciones de configuración de imagen {#image-options}

* `wrapInPicture`: `false` (predeterminado) - Generar elementos `<img>` simples
* `wrapInPicture`: `true`: ajuste de imágenes en `<picture>` elementos para un diseño interactivo

### Otras acciones {#other}

Todas las demás acciones admiten la personalización básica. Las secciones disponibles son las siguientes:

```json
{
  "actions": {
    "h1": {
      "shortcut": "Mod-Alt-1",
      "label": "Large Heading"
    },
    "paragraph": {
      "shortcut": "Mod-Alt-0",
      "label": "Normal Text"
    },
    "link": {
      "shortcut": "Mod-K",
      "label": "Insert Link",
      "hideTarget": false    // Show target attribute options (default: false)
    }
  }
}
```

## Ejemplo completo {#example}

A continuación se muestra un ejemplo de una configuración completa.

```json
[
  {
    "id": "richtext",
    "rte": {
      // Configure which tools appear in toolbar
      "toolbar": {
        "format": [
          "bold",
          "italic"
        ],
        "blocks": [
          "paragraph",
          "h1",
          "h2"
        ],
        "list": [
          "bullet_list",
          "ordered_list"
        ],
        "insert": [
          "link",
          "unlink"
        ],
        "sections": [
          "format",
          "blocks",
          "list",
          "insert"
        ]
      },
      // Customize individual action behavior
      "actions": {
        // Format actions with HTML tag choices
        "bold": {
          "tag": "strong",
          "shortcut": "Mod-B",
          "label": "Bold"
        },
        "italic": {
          "tag": "em",
          "shortcut": "Mod-I"
        },
        // List actions with content wrapping
        "bullet_list": {
          "wrapInParagraphs": true,
          "label": "Bullet List"
        },
        "ordered_list": {
          "wrapInParagraphs": false
        },
        // Link actions with target control
        "link": {
          "hideTarget": false,
          "shortcut": "Mod-K",
          "label": "Add Link"
        },
        "unlink": {
          "label": "Remove Link"
        },
        // Other actions with basic customization
        "h1": {
          "shortcut": "Mod-Alt-1",
          "label": "Main Heading"
        }
      }
    }
  }
]
```

## Detalles de opción de acción {#action-details}

Varias opciones tienen detalles adicionales que son importantes tener en cuenta.

### `wrapInParagraphs` {#wrapInParagraphs}

La opción `wrapInParagraphs` de las listas controla la estructura de HTML.

#### `wrapInParagraphs: false` (predeterminada) {#wrapInParagraphs-false}

```html
<ul>
  <li>Simple text content</li>
  <li>Another item</li>
</ul>
```

#### `wrapInParagraphs: true` {#wrapInParagraphs-true}

```html
<ul>
  <li><p>Text wrapped in paragraphs</p></li>
  <li><p>Supports rich formatting within items</p></li>
</ul>
```

Use `wrapInParagraphs: true` cuando necesite:

* Formato enriquecido en elementos de lista
* Varios párrafos por elemento de lista
* Estilo coherente a nivel de bloque

### Opciones de destino de vínculo {#link-target}

La opción `hideTarget` de los vínculos controla si el atributo `target` se incluye en los vínculos generados y si el cuadro de diálogo para la creación de vínculos incluye un campo para la selección de destinos.

#### `hideTarget: false` (predeterminada) {#hideTarget-false}

```html
<a href="https://example.com" target="_self">Link text</a>
<a href="https://example.com" target="_blank">External link</a>
```

### `hideTarget: true` {#hideTarget-true}

```html
<a href="https://example.com">Link text</a>
```

### Opciones de etiqueta {#tag}

Las acciones de formato permiten cambiar entre las variantes de HTML.

| Acción | Etiqueta predeterminada | Etiquetas alternativas | Caso práctico |
|---|---|---|---|
| `bold` | `<strong>` | `<b>` | Énfasis semántico vs. visual |
| `italic` | `<em>` | `<i>` | Estilo semántico vs. visual |
| `strike` | `<del>` | `<s>` | Eliminación visual frente a semántica |

Elija etiquetas semánticas (`<strong>`, `<em>`, `<del>`) para una mejor accesibilidad y optimización de los motores de búsqueda.

### Métodos abreviados de teclado {#keyboard-shortcuts}

Los métodos abreviados utilizan el formato `Mod-Key`, donde:

* `Mod` = `Cmd` en Mac, `Ctrl` en Windows/Linux
* Ejemplos: `Mod-B`, `Mod-Shift-8`, `Mod-Alt-1`
