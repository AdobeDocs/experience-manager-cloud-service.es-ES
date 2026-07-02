---
title: Personalización del editor universal
description: Obtenga información acerca de las distintas opciones para personalizar el editor universal y satisfacer las necesidades de los autores de contenido.
exl-id: 8d6523c8-b266-4341-b301-316d5ec224d7
feature: Developing
role: Admin, Developer
source-git-commit: c20290b92f6abdd602986ddca6e305dabdc13cfc
workflow-type: tm+mt
source-wordcount: '532'
ht-degree: 53%

---


# Personalización del editor universal {#customizing}

Obtenga información acerca de las distintas opciones para personalizar el editor universal y satisfacer las necesidades de los autores de contenido.

>[!TIP]
>
>El editor universal también ofrece muchos [puntos de extensión](/help/implementing/universal-editor/extending.md) que le permiten ampliar su funcionalidad para satisfacer las necesidades de su proyecto.

## Uso de etiquetas de configuración de Meta {#meta-tags}

Algunos flujos de trabajo de creación pueden requerir el uso de algunas funciones del editor universal, no de otras. Para admitir estos casos diversos, hay etiquetas meta disponibles para configurar o deshabilitar determinadas funciones o botones del editor.

### Desactivación de funciones {#disable-features}

Use esta etiqueta en la sección `<head>` de la página para deshabilitar una o más características:

```html
<meta name="urn:adobe:aue:config:disable" content="..." />
```

Si desea deshabilitar varias funciones, proporcione una lista de valores separados por comas.

Los siguientes son los valores compatibles con `content`, es decir, las características que se pueden deshabilitar con las metaetiquetas.

| Valor de contenido | Descripción |
|---|---|
| `publish` | Deshabilite toda la funcionalidad [publishing](/help/sites-cloud/authoring/universal-editor/publishing.md), es decir, los botones [publicar](/help/sites-cloud/authoring/universal-editor/navigation.md#publish) y [cancelar publicación](/help/sites-cloud/authoring/universal-editor/navigation.md#ellipsis) |
| `publish-live` | Deshabilitar publicación [activa](/help/sites-cloud/authoring/universal-editor/publishing.md) |
| `publish-preview` | Deshabilitar la publicación de vista previa (si el [servicio de vista previa](/help/sites-cloud/authoring/sites-console/previewing-content.md) está disponible) |
| `unpublish` | Deshabilitar [botón para cancelar la publicación](/help/sites-cloud/authoring/universal-editor/publishing.md#unpublishing-content) |
| `copy` | Deshabilita [los botones de copiar y pegar](/help/sites-cloud/authoring/universal-editor/authoring.md#copy-paste) |
| `duplicate` | Deshabilita [botón duplicado](/help/sites-cloud/authoring/universal-editor/navigation.md#duplicate) |
| `header-open-page` | Deshabilita [botón Abrir página](/help/sites-cloud/authoring/universal-editor/navigation.md#open-page) |
| `aem-dev-login` | Deshabilita [botón de inicio de sesión de desarrollador](/help/sites-cloud/authoring/universal-editor/navigation.md#local-developer-login) |

### Definición del modo de editor {#defining-mode}

Puede forzar al editor universal a que se abra en un modo concreto. Utilice esta etiqueta en la sección `<head>` de la página para forzar el modo de edición:

```html
<meta name="urn:adobe:aue:config:mode" content="..." />
```

Los siguientes son los valores compatibles con `content`, es decir, las características que se pueden deshabilitar con las metaetiquetas.

| Valor de contenido | Descripción |
|---|---|
| `preview` | El editor se abre en [modo de vista previa.](/help/sites-cloud/authoring/universal-editor/navigation.md#preview-mode) El icono **Vista previa** está oculto y el usuario no puede volver al modo de edición. |
| `readonly` | El editor se abre en modo de solo lectura. El botón [**Propiedades** y el panel](/help/sites-cloud/authoring/universal-editor/navigation.md#properties-rail) están ocultos. Los detalles están disponibles en el árbol de contenido, pero no se pueden realizar cambios. |

Al definir modos mediante metaetiquetas, el usuario no puede anularlos.

### URL de vista previa personalizadas {#custom-preview-urls}

Puede especificar una URL de vista previa personalizada mediante una metaconfiguración `urn:adobe:aue:config:preview`, que se abrirá al hacer clic en el botón **Abrir página** en la [barra de herramientas superior derecha del editor](/help/sites-cloud/authoring/universal-editor/navigation.md#universal-editor-toolbar).

Para ello, basta con incluir la URL de vista previa deseada en una metaetiqueta de la aplicación instrumentada como en el siguiente ejemplo.

```html
<meta name="urn:adobe:aue:config:preview" content="https://wknd.site"/>
```

### Cambio del punto final {#custom-endpoint}

Si no desea utilizar el servicio de editor universal, que aloja Adobe, sino su propia versión alojada, puede establecerlo en una metaetiqueta. Consulte el documento [Introducción al editor universal en AEM](/help/implementing/universal-editor/getting-started.md##configuration-settings) para obtener más información.

## Filtrado de componentes {#filtering-components}

Puede restringir los componentes permitidos por contenedor en el editor universal mediante filtros de componente. Consulte el documento [Filtrado de componentes](/help/implementing/universal-editor/filtering.md) para obtener más información.

## Mostrar y ocultar condicionalmente componentes en el panel de propiedades {#conditionally-hide}

Aunque un componente o componentes suelen estar disponibles para los autores, puede haber ciertas situaciones en las que no tiene sentido. En estos casos, puede ocultar componentes en el panel de propiedades añadiendo un atributo `condition` a los [campos del modelo de componente](/help/implementing/universal-editor/field-types.md#fields).

Las condiciones se pueden definir usando el [esquema JsonLogic](https://jsonlogic.com/). Si la condición es verdadera, se muestra el campo. Si la condición es falsa, el campo estará oculto.

>[!BEGINTABS]

>[!TAB Modelo de muestra]

```json
 {
    "id": "conditionally-revealed-component",
    "fields": [
      {
        "component": "boolean",
        "label": "Shall the text field be revealed?",
        "name": "reveal",
        "valueType": "boolean"
      },
      {
        "component": "text-input",
        "label": "Hidden text field",
        "name": "hidden-text",
        "valueType": "string",
        "condition": { "===": [{"var" : "reveal"}, true] }
      }
    ]
 }
```

>[!TAB Condición falsa]

![Campo de texto oculto](assets/hidden.png)

>[!TAB Condición verdadera]

![Campo de texto mostrado](assets/shown.png)

>[!ENDTABS]
