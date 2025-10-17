---
title: Personalización del editor universal
description: Obtenga información acerca de las distintas opciones para personalizar el editor universal y satisfacer las necesidades de los autores de contenido.
exl-id: 8d6523c8-b266-4341-b301-316d5ec224d7
feature: Developing
role: Admin, Architect, Developer
source-git-commit: a72b4b7921a1a379bcd089682c02b0519fe3af8a
workflow-type: tm+mt
source-wordcount: '522'
ht-degree: 78%

---


# Personalización del editor universal {#customizing}

Obtenga información acerca de las distintas opciones para personalizar el editor universal y satisfacer las necesidades de los autores de contenido.

>[!TIP]
>
>El editor universal también ofrece muchos [puntos de extensión](/help/implementing/universal-editor/extending.md) que le permiten ampliar su funcionalidad para satisfacer las necesidades de su proyecto.

## Desactivación de la publicación {#disable-publish}

Algunos flujos de trabajo de creación requieren que el contenido se revise antes de publicarse. En estos casos, la opción para publicar no debe estar disponible para ningún autor.

Por lo tanto, el botón **Publicar** se puede suprimir por completo en una aplicación añadiendo los siguientes metadatos.

```html
<meta name="urn:adobe:aue:config:disable" content="publish"/>
```

## Desactivación de la publicación en previsualización {#publish-preview}

Algunos flujos de trabajo de creación podrían impedir la publicación en el [servicio de previsualización](/help/sites-cloud/authoring/sites-console/previewing-content.md) (si está disponible).

Por lo tanto, la opción **Previsualizar** de la ventana de publicación se puede suprimir por completo en una aplicación añadiendo los siguientes metadatos.

```html
<meta name="urn:adobe:aue:config:disable" content="publish-preview"/>
```

## Desactivación de la publicación en directo {#publish-live}

Algunos flujos de trabajo de creación pueden impedir la publicación en el servicio activo.

Por lo tanto, la opción **Live** de la ventana de publicación se puede suprimir por completo en una aplicación si agrega los siguientes metadatos.

```html
<meta name="urn:adobe:aue:config:disable" content="publish-live"/>
```

## Desactivación de cancelación de publicación {#unpublish}

Algunos flujos de trabajo de creación requieren un proceso de aprobación antes de cancelar la publicación del contenido. En estos casos, la opción de cancelar la publicación no debe estar disponible para ningún autor.

Por lo tanto, el botón **Cancelar la publicación** se puede suprimir por completo en una aplicación si agrega los siguientes metadatos.

```html
<meta name="urn:adobe:aue:config:disable" content="unpublish"/>
```

## Desactivación de Abrir página {#open-page}

El botón **Abrir página** se puede eliminar por completo en una aplicación añadiendo los siguientes metadatos.

```html
<meta name="urn:adobe:aue:config:disable" content="header-open-page" />
```

## Desactivación del botón Duplicar {#duplicate-button}

Es posible que algunos flujos de trabajo de creación deban limitar la capacidad del autor de contenido para duplicar componentes. Puede deshabilitar el [icono Duplicar](/help/sites-cloud/authoring/universal-editor/navigation.md#duplicate) añadiendo los siguientes metadatos.

```html
<meta name="urn:adobe:aue:config:disable" content="duplicate"/>
```

## Desactivación de Copiar y Pegar {#copy-paste}

Es posible que algunos flujos de trabajo de creación deban limitar la capacidad del autor de contenido para copiar y pegar componentes. Puede deshabilitar [copiar y pegar iconos](/help/sites-cloud/authoring/universal-editor/authoring.md#copy-paste) agregando los siguientes metadatos.

```html
<meta name="urn:adobe:aue:config:disable" content="copy"/>
```

## Cambio del punto final {#custom-endpoint}

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

## URL de vista previa personalizadas {#custom-preview-urls}

Puede especificar una URL de vista previa personalizada mediante una metaconfiguración `urn:adobe:aue:config:preview`, que se abrirá al hacer clic en el botón **Abrir página** en la [barra de herramientas superior derecha del editor](/help/sites-cloud/authoring/universal-editor/navigation.md#universal-editor-toolbar).

Para ello, basta con incluir la URL de vista previa deseada en una metaetiqueta de la aplicación instrumentada como en el siguiente ejemplo.

```html
<meta name="urn:adobe:aue:config:preview" content="https://wknd.site"/>
```
