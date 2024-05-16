---
title: Personalizar y ampliar el editor universal
description: Obtenga información acerca de los diferentes puntos de extensión y otras funciones que le permiten personalizar la interfaz de usuario del editor universal para satisfacer las necesidades de los autores de contenido.
exl-id: 8d6523c8-b266-4341-b301-316d5ec224d7
source-git-commit: bdd67fb383bf20399eacaf9b9c086ea8468ea742
workflow-type: tm+mt
source-wordcount: '578'
ht-degree: 1%

---


# Personalizar y ampliar el editor universal {#customizing-extending}

Obtenga información acerca de los diferentes puntos de extensión y otras funciones que le permiten personalizar la experiencia de creación del Editor universal para satisfacer las necesidades de los autores de contenido.

## Información general {#overview}

El editor universal permite dos tipos de adaptación para las necesidades de su proyecto.

* [Personalización del editor universal](#customizing) - La funcionalidad estándar del editor universal se puede adaptar mediante varias configuraciones de personalización.
* [Ampliación de la IU del editor universal](#extending) : La IU del editor universal también se puede ampliar con el Generador de aplicaciones para satisfacer las necesidades de sus proyectos.

Ambos tipos se detallan en las secciones siguientes.

## Personalización del editor universal {#customizing}

El editor universal ofrece varias opciones integradas para personalizar su funcionalidad.

### Desactivación de publicación {#disable-publish}

Algunos flujos de trabajo de creación requieren que el contenido se revise antes de publicarse. En estos casos, la opción para publicar no debe estar disponible para ningún autor.

El **Publish** por lo tanto, el botón se puede suprimir por completo en una aplicación añadiendo los siguientes metadatos.

```html
<meta name="urn:adobe:aue:config:disable" content="publish"/>
```

### Filtrado de componentes {#filtering-components}

Al utilizar el Editor universal, puede restringir los componentes permitidos por componente de contenedor. Para ello, debe introducir una etiqueta de script adicional, que apunte a la definición del filtro.

```html
<script type="application/vnd.adobe.aue.filter+json" src="/static/filter-definition.json"></script>
```

Una definición de filtro puede tener el aspecto siguiente, que restringiría un contenedor para permitir únicamente agregar texto e imágenes.

```json
[
  {
    "id": "container-filter",
     "components": ["text", "image"]
   }
]
```

A continuación, puede hacer referencia a la definición del filtro desde el componente contenedor agregando la propiedad `data-aue-filter`, pasando el ID del filtro definido anteriormente.

```html
data-aue-filter="container-filter"
```

Configuración de la `components` en una definición de filtro a `null` permite todos los componentes, como si no hubiera ningún filtro.

```json
[
  {
    "id": "another-container-filter",
     "components": null
   }
]
```

### Mostrar y ocultar condicionalmente componentes en el carril Propiedades {#conditionally-hide}

Aunque un componente o componentes suelen estar disponibles para los autores, puede haber ciertas situaciones en las que no tiene sentido. En estos casos, puede ocultar componentes en el carril de propiedades añadiendo una `condition` atribuir a [campos del modelo de componente.](/help/implementing/universal-editor/field-types.md#fields)

Las condiciones se pueden definir mediante [Esquema JsonLogic.](https://jsonlogic.com/) Si la condición es verdadera, se muestra el campo. Si la condición es falsa, el campo estará oculto.

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

>[!TAB Condición False]

![Campo de texto oculto](assets/hidden.png)

>[!TAB Condición verdadera]

![Campo de texto mostrado](assets/shown.png)

>[!ENDTABS]

## Ampliación de la IU del editor universal {#extending}

Como servicio de Adobe Experience Cloud, la interfaz de usuario del editor universal se puede ampliar con el Generador de aplicaciones y el Experience Manager.

Las extensiones de interfaz de usuario son aplicaciones JavaScript creadas con el Generador de aplicaciones de Adobe que se pueden incrustar en aplicaciones de interfaz de usuario que se ejecutan en el shell unificado de Adobe Experience Cloud, como el Editor universal. Puede agregar sus propios botones y acciones al menú de encabezado y al carril de propiedades, así como crear sus propios eventos para el editor universal.

Si desea explorar estas posibilidades, consulte los siguientes recursos:

1. [Extensibilidad de IU](https://developer.adobe.com/uix/docs/) : Documentación para desarrolladores para la extensión de la interfaz de usuario.
1. [Guías de extensibilidad de IU](https://developer.adobe.com/uix/docs/guides/) - Instrucciones paso a paso sobre cómo desarrollar su propia extensión
1. [Los puntos de extensión de Universal Editor](https://developer.adobe.com/uix/docs/services/aem-universal-editor/) - Documentación del punto de extensión universal específica del editor

>[!TIP]
>
>Si prefiere aprender con el ejemplo, consulte la [AEM Tutorial de extensibilidad de la IU de.](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/developing/extensibility/ui/overview) Aunque se centra en ampliar la consola de fragmentos de contenido, los conceptos para implementar una extensión de interfaz de usuario en el editor universal son los mismos.

[Uso del Extension Manager en AEM Sites,](https://developer.adobe.com/uix/docs/extension-manager/) puede habilitar o deshabilitar las extensiones por instancia, acceder a las extensiones de origen de Adobe, incluidas las del editor universal, y mucho más.
