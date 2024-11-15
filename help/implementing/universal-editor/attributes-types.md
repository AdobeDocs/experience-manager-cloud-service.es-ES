---
title: Atributos y tipos de elementos
description: Obtenga información sobre los atributos de datos y los tipos de elementos que requiere el Editor universal.
exl-id: 02795a31-244a-42b4-8297-2649125d7777
feature: Developing
role: Admin, Architect, Developer
source-git-commit: edef86c67becf3b8094196d39baa9e69d6c81777
workflow-type: tm+mt
source-wordcount: '574'
ht-degree: 46%

---


# Atributos y tipos {#attributes-types}

Obtenga información sobre los atributos de datos y los tipos de elementos que requiere el Editor universal.

## Introducción {#introduction}

Para que el editor universal pueda editar una aplicación, debe instrumentarse correctamente. Esto incluye introducir los metadatos adecuados para que el editor pueda modificar el contenido de la aplicación. Este documento detalla los atributos y tipos de elementos de esos metadatos.

>[!NOTE]
>
>La validación de contenido se ejecuta en el lado del servidor. El editor universal solo funciona con los atributos de datos. La validación de que se ajustan al modelo o la estructura debe realizarse en el nivel de API.

## Propiedades de datos {#data-properties}

| Propiedad de los datos | Descripción |
|---|---|
| `data-aue-resource` | Para el URN del recurso, consulte la sección [Instrumentación de la página del documento Introducción al editor universal en AEM](getting-started.md#instrument-thepage) |
| `data-aue-prop` | Para el atributo del recurso, consulte la sección [Instrumentación de la página del documento Introducción al editor universal en AEM](getting-started.md#instrument-thepage) |
| `data-aue-type` | [Tipo de elemento editable](#item-types) (por ejemplo, texto, imagen y referencia) |
| `data-aue-filter` | Define:<br>- Qué funcionalidades de RTE están habilitadas<br>- Qué componentes se pueden agregar a un contenedor<br>- Qué recursos se pueden agregar a un tipo de medios |
| `data-aue-label` | Define una etiqueta personalizada para un elemento seleccionable que se muestra en el editor |
| `data-aue-model` | Define un modelo que se utiliza para la edición basada en formularios en el panel de propiedades |
| `data-aue-behavior` | Define el [comportamiento de una instrumentación](#behaviors); por ejemplo, el texto o la imagen independientes también pueden imitar un componente para hacerlo movible o eliminable |

## Tipos de elementos {#item-types}

| `data-aue-type` | Descripción | `data-aue-resource` | `data-aue-prop` | `data-aue-filter` | `data-aue-label` | `data-aue-model` | `data-aue-behavior` |
|---|---|---|---|---|---|---|---|
| `text` | El texto se puede editar dentro de las etiquetas HTML, pero solo en formato de texto simple, no tiene un formato de texto enriquecido disponible. Se suele utilizar en los componentes del título, por ejemplo. | Opcional | Requerido | N/D | Opcional | N/D | Opcional |
| `richtext` | El texto se puede editar con capacidades de texto enriquecido completas. El RTE se muestra en el panel derecho | Opcional | Requerido | N/D | Opcional | N/D | Opcional |
| `media` | El editable es un recurso, por ejemplo, una imagen o un vídeo | Opcional | Requerido | Opcional<br>lista de criterios de filtro de imagen o vídeo que se pasan al selector de recursos | Opcional | N/D | Opcional |
| `container` | El comportamiento editable se comporta como un contenedor para componentes, también conocido como Sistema de párrafos. | Depende <br>consultar más abajo | Depende <br>consultar más abajo | Opcional<br>una lista de componentes permitidos | Opcional | N/D | N/D |
| `component` | El componente editable es un componente. No añade ninguna funcionalidad adicional. Es necesario indicar las partes móviles o eliminables del DOM y para abrir el panel de propiedades y sus campos | Requerido | N/D | N/D | Opcional | Opcional | N/D |
| `reference` | El editable es una referencia, por ejemplo, un fragmento de contenido, un fragmento de experiencia o un producto | Depende <br>consultar más abajo | Depende <br>consultar más abajo | Opcional<br>lista de criterios de filtro de fragmento de contenido, producto o fragmento de experiencia que se pasan al selector de referencia | Opcional | Opcional | N/D |

`data-aue-resource` siempre es necesario, ya que es la clave principal que indica dónde se escriben los cambios de contenido.

* No se requiere directamente en la etiqueta donde está establecido `data-aue-type`.
* En caso de que no se establezca, se utilizará el atributo `data-aue-resource` de como elemento principal más cercano.

`data-aue-prop` es necesario siempre que desee editar en el contexto el, excepto para un contenedor en el que es opcional (si se establece, el contenedor es un fragmento de contenido y la prop apunta a un campo de referencias múltiples).

* `data-aue-prop` es el atributo que se va a actualizar para la clave principal de `data-aue-resource`.

## Comportamientos {#behaviors}

| `data-aue-behavior` | Descripción |
|---|---|
| `component` | Se utiliza para permitir componentes de imitación de texto, texto enriquecido y medios independientes, de modo que también se pueda mover y eliminar en la página |
| `container` | Se utiliza para permitir que los contenedores se traten como sus propios componentes, de modo que se puedan mover y eliminar en la página |
