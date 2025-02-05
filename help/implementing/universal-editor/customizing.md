---
title: Personalizar y ampliar el editor universal
description: Obtenga información acerca de los diferentes puntos de extensión y otras funciones que le permiten personalizar la interfaz de usuario del editor universal para satisfacer las necesidades de los autores de contenido.
exl-id: 8d6523c8-b266-4341-b301-316d5ec224d7
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 10580c1b045c86d76ab2b871ca3c0b7de6683044
workflow-type: tm+mt
source-wordcount: '579'
ht-degree: 1%

---


# Personalizar y ampliar el editor universal {#customizing-extending}

Obtenga información acerca de los diferentes puntos de extensión y otras funciones que le permiten personalizar la experiencia de creación del Editor universal para satisfacer las necesidades de los autores de contenido.

## Información general {#overview}

El editor universal permite dos tipos de adaptación para las necesidades de su proyecto.

* [Personalización del editor universal](#customizing): la funcionalidad estándar del editor universal se puede adaptar mediante varias configuraciones de personalización.
* [Ampliación de la interfaz de usuario del editor universal](#extending): la interfaz de usuario del editor universal también se puede ampliar con App Builder para satisfacer las necesidades de sus proyectos.

Ambos tipos se detallan en las secciones siguientes.

## Personalización del editor universal {#customizing}

El editor universal ofrece varias opciones integradas para personalizar su funcionalidad.

### Desactivación de publicación {#disable-publish}

Algunos flujos de trabajo de creación requieren que el contenido se revise antes de publicarse. En estos casos, la opción para publicar no debe estar disponible para ningún autor.

Por lo tanto, el botón **Publish** se puede suprimir por completo en una aplicación añadiendo los siguientes metadatos.

```html
<meta name="urn:adobe:aue:config:disable" content="publish"/>
```

### Filtrado de componentes {#filtering-components}

Puede restringir los componentes permitidos por contenedor en el Editor universal mediante filtros de componente. Consulte el documento [Componentes de filtrado](/help/implementing/universal-editor/filtering.md) para obtener más información.

### Mostrar y ocultar condicionalmente componentes en el panel Propiedades {#conditionally-hide}

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

### URL de vista previa personalizadas {#custom-preview-urls}

Puede especificar una URL de vista previa personalizada mediante una metaconfiguración de `urn:adobe:aue:config:preview`, que se abrirá al hacer clic en el botón **Abrir página** en la barra de herramientas superior derecha del [editor](/help/sites-cloud/authoring/universal-editor/navigation.md#universal-editor-toolbar).

Esto es particularmente útil para aplicaciones con requisitos de vista previa específicos, como las que [usan Edge Delivery Services con WYSIWYG Authoring](/help/edge/wysiwyg-authoring/authoring.md).

Para ello, simplemente incluya la URL de vista previa deseada en una metaetiqueta de la aplicación instrumentada como en el siguiente ejemplo.

```html
<meta name="urn:adobe:aue:config:preview" content="https://wknd.site"/>
```

## Ampliación de la IU del editor universal {#extending}

Como servicio de Adobe Experience Cloud, la interfaz de usuario del editor universal se puede ampliar con el Experience Manager y App Builder.

Las extensiones de interfaz de usuario son aplicaciones de JavaScript creadas con Adobe App Builder que se pueden incrustar en aplicaciones de interfaz de usuario que se ejecutan en el shell unificado de Adobe Experience Cloud, como el editor universal. Puede agregar sus propios botones y acciones al menú de encabezado y al panel de propiedades, así como crear sus propios eventos para el editor universal.

Si desea explorar estas posibilidades, consulte los siguientes recursos:

1. [Extensibilidad de la interfaz de usuario](https://developer.adobe.com/uix/docs/): esta es la documentación para desarrolladores para la extensión de la interfaz de usuario.
1. [Guías de extensibilidad de la IU](https://developer.adobe.com/uix/docs/guides/): instrucciones paso a paso sobre cómo desarrollar su propia extensión
1. [Puntos de extensión de editor universal](https://developer.adobe.com/uix/docs/services/aem-universal-editor/): documentación de punto de extensión específica de editor universal

>[!TIP]
>
>AEM Si prefiere aprender con el ejemplo, consulte el [tutorial de extensibilidad de la interfaz de usuario de ](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/developing/extensibility/ui/overview). Aunque se centra en ampliar la consola de fragmentos de contenido, los conceptos para implementar una extensión de interfaz de usuario en el editor universal son los mismos.

[Con Extension Manager en AEM Sites](https://developer.adobe.com/uix/docs/extension-manager/), puede habilitar o deshabilitar las extensiones por instancia, tener acceso a las extensiones de origen de Adobe, incluidas las del editor universal, y mucho más.
