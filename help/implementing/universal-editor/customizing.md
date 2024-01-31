---
title: Personalización de la IU
description: Obtenga información acerca de los diferentes puntos de extensión que le permiten personalizar la interfaz de usuario del editor universal para satisfacer las necesidades de los autores de contenido.
exl-id: 8d6523c8-b266-4341-b301-316d5ec224d7
source-git-commit: 1bc65e65e6ce074a050e21137ce538b5c086665f
workflow-type: tm+mt
source-wordcount: '194'
ht-degree: 0%

---


# Personalización de la IU {#customizing-ui}

Obtenga información acerca de los diferentes puntos de extensión que le permiten personalizar la interfaz de usuario del editor universal para satisfacer las necesidades de los autores de contenido.

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
