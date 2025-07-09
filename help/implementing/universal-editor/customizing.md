---
title: Personalización del editor universal
description: Obtenga información acerca de las distintas opciones para personalizar el Editor universal para satisfacer las necesidades de los autores de contenido.
exl-id: 8d6523c8-b266-4341-b301-316d5ec224d7
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 32b3a125d6370dd591252fde342843d5f9e33cf1
workflow-type: tm+mt
source-wordcount: '409'
ht-degree: 2%

---


# Personalización del editor universal {#customizing}

Obtenga información acerca de las distintas opciones para personalizar el Editor universal para satisfacer las necesidades de los autores de contenido.

>[!TIP]
>
>El editor universal también ofrece muchos [puntos de extensión](/help/implementing/universal-editor/extending.md) que le permiten ampliar su funcionalidad para satisfacer las necesidades de su proyecto.

## Desactivación de publicación {#disable-publish}

Algunos flujos de trabajo de creación requieren que el contenido se revise antes de publicarse. En estos casos, la opción para publicar no debe estar disponible para ningún autor.

Por lo tanto, el botón **Publicar** se puede suprimir por completo en una aplicación añadiendo los siguientes metadatos.

```html
<meta name="urn:adobe:aue:config:disable" content="publish"/>
```

## Desactivación de la publicación para previsualización {#publish-preview}

Algunos flujos de trabajo de creación podrían impedir la publicación en el [servicio de vista previa](/help/sites-cloud/authoring/sites-console/previewing-content.md) (si está disponible).

Por lo tanto, la opción **Preview** de la ventana de publicación se puede suprimir por completo en una aplicación si agrega los siguientes metadatos.

```html
<meta name="urn:adobe:aue:config:disable" content="publish-preview"/>
```

## Desactivación de Abrir página {#open-page}

El botón **Abrir página** se puede eliminar por completo en una aplicación si agrega los siguientes metadatos.

```html
<meta name="urn:adobe:aue:config:disable" content="header-open-page" />
```

## Desactivación del botón Duplicar {#duplicate-button}

Es posible que algunos flujos de trabajo de creación deban limitar la capacidad del autor de contenido para duplicar componentes. Puede deshabilitar el [icono duplicado](/help/sites-cloud/authoring/universal-editor/navigation.md#duplicate) agregando los siguientes metadatos.

```html
<meta name="urn:adobe:aue:config:disable" content="duplicate"/>
```

## Cambio del punto de conexión {#custom-endpoint}

Si no desea utilizar el servicio de editor universal, que aloja Adobe, sino su propia versión alojada, puede establecerlo en una metaetiqueta. Consulte el documento [Introducción al editor universal en AEM](/help/implementing/universal-editor/getting-started.md##configuration-settings) para obtener más información.

## Filtrado de componentes {#filtering-components}

Puede restringir los componentes permitidos por contenedor en el Editor universal mediante filtros de componente. Consulte el documento [Componentes de filtrado](/help/implementing/universal-editor/filtering.md) para obtener más información.

## Mostrar y ocultar condicionalmente componentes en el panel Propiedades {#conditionally-hide}

Aunque un componente o componentes suelen estar disponibles para los autores, puede haber ciertas situaciones en las que no tiene sentido. En estos casos, puede ocultar componentes en el panel de propiedades agregando un atributo `condition` a los [campos del modelo de componente](/help/implementing/universal-editor/field-types.md#fields).

Las condiciones se pueden definir usando [JsonLogic schema](https://jsonlogic.com/). Si la condición es verdadera, se muestra el campo. Si la condición es falsa, el campo estará oculto.

>[!BEGINTABS]

>[!TAB Modelo de ejemplo]

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

Puede especificar una URL de vista previa personalizada mediante una metaconfiguración de `urn:adobe:aue:config:preview`, que se abrirá al hacer clic en el botón **Abrir página** en la barra de herramientas superior derecha del [editor](/help/sites-cloud/authoring/universal-editor/navigation.md#universal-editor-toolbar).

Para ello, simplemente incluya la URL de vista previa deseada en una metaetiqueta de la aplicación instrumentada como en el siguiente ejemplo.

```html
<meta name="urn:adobe:aue:config:preview" content="https://wknd.site"/>
```
