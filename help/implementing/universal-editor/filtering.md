---
title: Filtrado de componentes
description: Descubra cómo puede restringir los componentes permitidos por contenedor en el Editor universal mediante filtros de componente.
feature: Developing
role: Admin, Architect, Developer
exl-id: eeae8d7c-c563-4d9b-8c54-1098a4e98c18
source-git-commit: cdad4954b13f5582bebfd604220da90529231ccd
workflow-type: tm+mt
source-wordcount: '153'
ht-degree: 3%

---

# Filtrado de componentes {#filtering-components}

Descubra cómo puede restringir los componentes permitidos por contenedor en el Editor universal mediante filtros de componente.

## Filtros {#filters}

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

Al establecer el atributo `components` en una definición de filtro en `null`, se permiten todos los componentes, como si no hubiera ningún filtro.

```json
[
  {
    "id": "another-container-filter",
     "components": null
   }
]
```

>[!TIP]
>
>Obtenga información acerca de otras opciones de personalización y extensión disponibles en el editor universal en los siguientes documentos:
>
>* [Personalización del editor universal](/help/implementing/universal-editor/customizing.md)
>* [Ampliación del editor universal](/help/implementing/universal-editor/extending.md)
