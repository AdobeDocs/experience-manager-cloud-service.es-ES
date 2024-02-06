---
title: Personalización de la experiencia de creación del editor universal
description: Obtenga información acerca de los diferentes puntos de extensión y otras funciones que le permiten personalizar la interfaz de usuario del editor universal para satisfacer las necesidades de los autores de contenido.
exl-id: 8d6523c8-b266-4341-b301-316d5ec224d7
source-git-commit: f04ab32093371ff425c4e196872738867d9ed528
workflow-type: tm+mt
source-wordcount: '302'
ht-degree: 0%

---


# Personalización de la experiencia de creación del editor universal {#customizing-ue}

Obtenga información acerca de los diferentes puntos de extensión y otras funciones que le permiten personalizar la experiencia de creación del Editor universal para satisfacer las necesidades de los autores de contenido.

## Desactivación de publicación {#disable-publish}

Algunos flujos de trabajo de creación requieren que el contenido se revise antes de publicarse. En estos casos, la opción para publicar no debe estar disponible para ningún autor.

El **Publish** por lo tanto, el botón se puede suprimir por completo en una aplicación añadiendo los siguientes metadatos.

```html
<meta name="urn:adobe:aue:config:disable" content="publish"/>
```

## Filtrado de componentes {#filtering-components}

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

## Mostrar y ocultar condicionalmente componentes en el carril Propiedades {#conditionally-hide}

Aunque un componente o componentes suelen estar disponibles para los autores, puede haber ciertas situaciones en las que no tiene sentido. En estos casos, puede ocultar componentes en el carril de propiedades añadiendo una `condition` atribuir a [campos del modelo de componente.](/help/implementing/universal-editor/field-types.md#fields)

Las condiciones se pueden definir mediante [Esquema JsonLogic.](https://jsonlogic.com/) Si la condición es verdadera, se muestra el campo. Si la condición es falsa, el campo estará oculto.

### Modelo de ejemplo {#sample-model}

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

#### Condición False {#false}

![Campo de texto oculto](assets/hidden.png)

#### Condición verdadera {#true}

![Campo de texto mostrado](assets/shown.png)
