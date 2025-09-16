---
title: Atributos y tipos de elementos
description: Obtenga información acerca de los atributos de datos y tipos de elementos que requiere el editor universal.
exl-id: 02795a31-244a-42b4-8297-2649125d7777
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 597315a7d569ebd62243322c543627b7a3535a6b
workflow-type: ht
source-wordcount: '554'
ht-degree: 100%

---


# Atributos y tipos {#attributes-types}

Obtenga información acerca de los atributos de datos y tipos de elementos que requiere el editor universal.

## Introducción {#introduction}

Para que el editor universal pueda editar una aplicación, debe instrumentarse correctamente. Esto incluye introducir los metadatos adecuados para que el editor pueda modificar el contenido de la aplicación. Este documento detalla los atributos y tipos de elementos de esos metadatos.

>[!NOTE]
>
>La validación de contenido se ejecuta en el lado del servidor. El editor universal solo funciona con los atributos de datos. La validación que se ajusta al modelo o la estructura debe abordarse en el nivel de la API.

## Propiedades de datos {#data-properties}

| Propiedad de los datos | Descripción |
|---|---|
| `data-aue-resource` | Para el URN del recurso, consulte la sección [Instrumentación de la página del documento Introducción al editor universal en AEM](getting-started.md#instrument-thepage) |
| `data-aue-prop` | Para el atributo del recurso, consulte la sección [Instrumentación de la página del documento Introducción al editor universal en AEM](getting-started.md#instrument-thepage) |
| `data-aue-type` | [Tipo del elemento editable](#item-types) (por ejemplo, texto, imagen y referencia) |
| `data-aue-filter` | Define:<br>- Qué funcionalidades del RTE están habilitadas<br>- Qué componentes se pueden añadir a un contenedor<br>- Qué recursos se pueden agregar a un tipo de medios |
| `data-aue-label` | Define una etiqueta personalizada para un elemento seleccionable que se muestra en el editor |
| `data-aue-model` | Define un modelo que se usa para la edición basada en formularios en el panel de propiedades |
| `data-aue-behavior` | Obsoleto. En su momento, definía el comportamiento de una instrumentación para permitir que el texto, el texto enriquecido y los medios independientes imitaran componentes que también se pudieran mover y eliminar en la página, lo que ofrecía un solo valor potencial de `component`. Esta propiedad ahora se omite y, cuando un elemento con `data-aue-resource` es un elemento secundario directo de un contenedor, automáticamente se considera un componente. |

## Tipos de elementos {#item-types}

| `data-aue-type` | Descripción | `data-aue-resource` | `data-aue-prop` | `data-aue-filter` | `data-aue-label` | `data-aue-model` |
|---|---|---|---|---|---|---|
| `text` | El texto se puede editar dentro de las etiquetas HTML, pero solo en formato de texto simple, no tiene un formato de texto enriquecido disponible. Se suele utilizar en los componentes del título, por ejemplo. | Opcional | Necesario | N/D | Opcional | N/D |
| `richtext` | El texto se puede editar con capacidades de texto enriquecido completas. El RTE se muestra en el panel derecho | Opcional | Necesario | N/D | Opcional | N/D |
| `media` | El elemento editable es un recurso, por ejemplo, una imagen o un vídeo | Opcional | Necesario | Opcional<br>lista de criterios de filtro de imagen o vídeo que se pasan al selector de recursos | Opcional | N/D |
| `container` | El comportamiento editable se comporta como un contenedor para componentes, también conocido como Sistema de párrafos. | Depende <br>consultar más abajo | Depende <br>consultar más abajo | Opcional<br>una lista de componentes permitidos | Opcional | N/D |
| `component` | El componente editable es un componente. No añade ninguna funcionalidad adicional. Es necesario para indicar partes móviles o eliminables del DOM y para abrir el panel de propiedades y sus campos | Necesario | N/D | N/D | Opcional | Opcional |
| `reference` | Lo editable es una referencia, por ejemplo, un fragmento de contenido, de experiencia o producto | Depende <br>consultar más abajo | Depende <br>consultar más abajo | Opcional<br>lista de criterios de filtro de fragmento de contenido, producto o fragmento de experiencia que se pasan al selector de referencia | Opcional | Opcional |

`data-aue-resource` siempre es necesario, ya que es la clave principal que indica dónde se escriben los cambios de contenido.

* No se requiere directamente en la etiqueta donde está establecido `data-aue-type`.
* En caso de que no se establezca, se utilizará el atributo `data-aue-resource` del elemento principal más cercano.

`data-aue-prop` es necesario siempre que desee editar en contexto, excepto en el caso de un contenedor en el que es opcional (si se establece, el contenedor es un fragmento de contenido y la propiedad apunta a un campo de referencias múltiples).

* `data-aue-prop` es el atributo que se va a actualizar para la clave principal de `data-aue-resource`.
