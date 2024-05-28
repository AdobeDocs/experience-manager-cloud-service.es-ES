---
title: Atributos y tipos de elementos
description: Obtenga información sobre los atributos de datos y los tipos de elementos que requiere el Editor universal.
exl-id: 02795a31-244a-42b4-8297-2649125d7777
source-git-commit: b42390dcecb546853380d64808bcf009680c89a3
workflow-type: tm+mt
source-wordcount: '538'
ht-degree: 72%

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
| `data-aue-type` | [Tipo del elemento editable](#item-types) (por ejemplo, texto, imagen y referencia) |
| `data-aue-filter` | Define qué referencias se pueden utilizar |
| `data-aue-label` | Define una etiqueta personalizada para un elemento seleccionable que se muestra en el editor. <br>Si `data-aue-model` está configurado, la etiqueta se recupera mediante el modelo |
| `data-aue-model` | Define un modelo que se usa para la edición basada en formularios en el carril de propiedades |
| `data-aue-behavior` | Define el [comportamiento de una instrumentación](#behaviors)Por ejemplo, el texto o la imagen independientes también pueden imitar un componente para hacerlo móvil o eliminable |

## Tipos de elementos {#item-types}

| `data-aue-type` | Descripción | `data-aue-resource` | `data-aue-prop` | `data-aue-filter` | `data-aue-label` | `data-aue-model` | `data-aue-behavior` |
|---|---|---|---|---|---|---|---|
| `text` | El texto se puede editar dentro de las etiquetas HTML, pero solo en formato de texto simple, no tiene un formato de texto enriquecido disponible. Se suele utilizar en los componentes del título, por ejemplo. | Opcional | Requerido | N/D | Opcional | N/D | Opcional |
| `richtext` | El texto se puede editar con capacidades de texto enriquecido completas. El RTE se muestra en el panel derecho | Opcional | Requerido | N/D | Opcional | N/D | Opcional |
| `media` | El editable es un recurso, por ejemplo, una imagen o un vídeo | Opcional | Requerido | Opcional<br>lista de criterios de filtro de imagen o vídeo que se pasan al selector de recursos | Opcional | N/D | Opcional |
| `container` | El comportamiento editable se comporta como un contenedor para componentes, también conocido como Sistema de párrafos. | Depende <br>consultar más abajo | Depende <br>consultar más abajo | Opcional<br>una lista de componentes permitidos | Opcional | N/D | N/D |
| `component` | El componente editable es un componente. No añade ninguna funcionalidad adicional. Es necesario para indicar partes móviles o eliminables del DOM y para abrir el carril de propiedades y sus campos | Requerido | N/D | N/D | Opcional | Opcional | N/D |
| `reference` | El editable es una referencia, por ejemplo, un fragmento de contenido, un fragmento de experiencia o un producto | Depende <br>consultar más abajo | Depende <br>consultar más abajo | Opcional<br>lista de criterios de filtro de fragmento de contenido, producto o fragmento de experiencia que se pasan al selector de referencia | Opcional | Opcional | N/D |

Dependiendo del caso de uso, `data-aue-prop` o `data-aue-resource` pueden no ser obligatorios. Por ejemplo:

* `data-aue-resource` es necesario si consulta los fragmentos de contenido a través de GraphQL y desea que la lista sea editable en contexto.
* `data-aue-prop` es necesario en caso de que tenga un componente que procese el contenido del fragmento de contenido al que se hace referencia y desee actualizar la referencia.

## Comportamientos {#behaviors}

| `data-aue-behavior` | Descripción |
|---|---|
| `component` | Se utiliza para permitir componentes de imitación de texto, texto enriquecido y medios independientes, de modo que también se pueda mover y eliminar en la página |
| `container` | Se utiliza para permitir que los contenedores se traten como sus propios componentes, de modo que se puedan mover y eliminar en la página |
