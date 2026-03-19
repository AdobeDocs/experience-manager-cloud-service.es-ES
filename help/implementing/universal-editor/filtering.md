---
title: Filtros
description: Aprenda a definir filtros para limitar las opciones disponibles en el editor, como componentes disponibles, opciones de RTE y selección de recursos.
feature: Developing
role: Admin, Developer
exl-id: eeae8d7c-c563-4d9b-8c54-1098a4e98c18
source-git-commit: 8d9d162ec5bba99afb1ae86252a49a9880be4e68
workflow-type: tm+mt
source-wordcount: '325'
ht-degree: 15%

---


# Filtros {#filters}

Aprenda a definir filtros para limitar las opciones disponibles en el editor, como componentes disponibles, opciones de RTE y selección de recursos.

## Configuración de filtros {#configuring-filters}

Al utilizar el Editor universal, puede restringir las opciones permitidas para determinadas funciones definiendo un filtro. Un filtro es una lista de elementos o acciones disponibles para el contexto específico. Por ejemplo, puede filtrar los componentes disponibles para insertarlos en un contenedor, puede [filtrar las opciones disponibles en RTE,](/help/implementing/universal-editor/configure-rte.md) y puede [filtrar los recursos disponibles](/help/implementing/universal-editor/configure-assets-selector.md) en el selector de recursos.

Todos los filtros deben definirse de manera similar.

1. [Agregar etiqueta de script para que apunte a la definición del filtro](#add-tag)
1. [Definición del filtro](#define-filter)
1. [Hacer referencia al filtro](#reference-filter)

Veamos un ejemplo de filtrado de componentes por componente de contenedor.

## Definición de filtro de referencia {#add-tag}

En primer lugar, introduzca una etiqueta de script adicional, que señale a la definición del filtro.

Para que nuestro ejemplo filtre los componentes permitidos por contenedor, la etiqueta podría tener un aspecto similar al siguiente.

```html
<script type="application/vnd.adobe.aue.filter+json" src="/static/filter-definition.json"></script>
```

## Definición del filtro {#define-filter}

Una definición de filtro contiene un JSON con un ID único para el filtro y los criterios de filtro.

Para que nuestro ejemplo filtre los componentes permitidos por contenedor, puede tener el siguiente aspecto, que restringiría un contenedor para que solo permita agregar texto e imágenes.

```json
[
  {
    "id": "container-filter",
    "components": ["text", "image"]
   }
]
```

Al establecer el atributo `components` en una definición de filtro en `null`, se permiten todos los componentes, como si no hubiera ningún filtro.

```json
[
  {
    "id": "another-container-filter",
     "components": null
   }
]
```

## Hacer referencia al filtro {#reference-filter}

Para utilizar el filtro, debe hacer referencia a su definición. Para ello, haga lo siguiente:

* Haciendo referencia al filtro desde el componente contenedor agregando la propiedad `data-aue-filter`, pasando el ID del filtro.

  ```html
  data-aue-filter="container-filter"
  ```

* Haciendo referencia al filtro desde su [definición de componente,](/help/implementing/universal-editor/component-definition.md) pasando el ID del filtro.

  ```json
  {
     "title":"My Container",
     "id":"my-container",
     "model": "my-model",
     "filter": "container-filter",
     ...
  }
  ```

## Recursos adicionales {#additional-resources}

Obtenga información acerca de otras opciones de personalización y extensión disponibles en el editor universal en los siguientes documentos:

* [Configuración del RTE para el editor universal](/help/implementing/universal-editor/configure-rte.md)
* [Configuración de filtros para el selector de Assets](/help/implementing/universal-editor/configure-assets-selector.md)
* [Personalización del editor universal](/help/implementing/universal-editor/customizing.md)
* [Ampliación del editor universal](/help/implementing/universal-editor/extending.md)
