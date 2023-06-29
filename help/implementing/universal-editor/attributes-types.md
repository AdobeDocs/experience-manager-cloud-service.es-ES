---
title: Atributos y tipos
description: Obtenga información acerca de los atributos y tipos de datos que requiere el editor universal.
exl-id: 02795a31-244a-42b4-8297-2649125d7777
source-git-commit: 1994b90e3876f03efa571a9ce65b9fb8b3c90ec4
workflow-type: tm+mt
source-wordcount: '662'
ht-degree: 82%

---

# Atributos y tipos {#attributes-types}

Obtenga información acerca de los atributos y tipos de datos que requiere el editor universal.

## Introducción {#introduction}

Para que el editor universal pueda editar una aplicación, debe instrumentarse correctamente. Esto incluye introducir los metadatos adecuados para que el editor pueda modificar el contenido de la aplicación. Este documento detalla los atributos y tipos de esos metadatos.

>[!NOTE]
>
>La validación de contenido se ejecuta en el lado del servidor. El editor universal solo funciona con los atributos de datos. La validación que se ajusta al modelo o la estructura debe abordarse en el nivel de la API.

## Propiedades de datos {#data-properties}

| Propiedad de los datos | Descripción |
|---|---|
| `itemid` | Para el URN del recurso, consulte la sección [Instrumentación de la página del documento Introducción al editor universal en AEM](getting-started.md#instrument-thepage) |
| `itemprop` | Para el atributo del recurso, consulte la sección [Instrumentación de la página del documento Introducción al editor universal en AEM](getting-started.md#instrument-thepage) |
| `itemtype` | Tipo de elemento editable (por ejemplo, texto, imagen y referencia) |
| `data-editor-itemfilter` | Define qué referencias se pueden utilizar |
| `data-editor-itemlabel` | Define una etiqueta personalizada para un elemento seleccionable que se muestra en el editor <br>En caso de `itemmodel` se define, la etiqueta se recupera a través del modelo |
| `data-editor-itemmodel` | Define un modelo que se utiliza para la edición basada en formularios en el carril de propiedades |
| `data-editor-behavior` | Define el comportamiento de una instrumentación, por ejemplo, el texto independiente o la imagen también pueden imitar un componente para que se pueda mover o eliminar |

## Tipos de elementos {#item-types}

| `itemtype` | Descripción | `itemid` | `itemprop` | `data-editor-itemfilter` | `data-editor-itemlabel` | `data-editor-itemmodel` | `data-editor-behvior` |
|---|---|---|---|---|---|---|---|
| `text` | El texto se puede editar dentro de las etiquetas HTML, pero solo en formato de texto simple, no tiene un formato de texto enriquecido disponible. Se suele utilizar en los componentes del título, por ejemplo. | Opcional | Requerido | N/D | Opcional | N/D | Opcional |
| `richtext` | El texto se puede editar con capacidades de texto enriquecido completas. RTE se muestra en el panel derecho | Opcional | Requerido | N/D | Opcional | N/D | Opcional |
| `media` | El elemento editable es un recurso, por ejemplo, una imagen o un vídeo | Opcional | Requerido | Opcional<br>lista de criterios de filtro de imagen o vídeo que se pasan al selector de recursos | Opcional | N/D | Opcional |
| `container` | El comportamiento editable se comporta como un contenedor para componentes, también conocido como Sistema de párrafos. | Depende <br>consultar más abajo | Depende <br>consultar más abajo | Opcional<br>una lista de componentes permitidos | Opcional | N/D | N/D |
| `component` | El componente editable es un componente. No agrega funcionalidad adicional, es necesario para indicar partes móviles/eliminables del DOM y para abrir el carril de propiedades y sus campos | Requerido | N/D | N/D | Opcional | Opcional | N/D |
| `reference` | Lo editable es una referencia, por ejemplo, un fragmento de contenido, de experiencia o producto. | Depende <br>consultar más abajo | Depende <br>consultar más abajo | Opcional<br>lista de criterios de filtro de fragmento de contenido, producto o fragmento de experiencia que se pasan al selector de referencia | Opcional | Opcional | N/D |

Dependiendo del caso de uso, `itemprop` o `itemid` pueden no ser obligatorios. Por ejemplo:

* `itemid` es necesario si consulta los fragmentos de contenido a través de GraphQL y desea que la lista sea editable en contexto.
* `itemprop` es necesario en caso de que tenga un componente que procese el contenido del fragmento de contenido al que se hace referencia y desee actualizar la referencia.

## Comportamientos {#behaviors}

| `data-editor-behavior` | Descripción |
|---|---|
| `component` | Puede utilizarse para que el texto independiente, el texto enriquecido y los medios imiten a los componentes, de modo que también puedan moverse y eliminarse de la página. |

## Recursos adicionales {#additional-resources}

Para obtener más información acerca del editor universal, consulte estos documentos.

* [Introducción al editor universal](introduction.md) - Descubra cómo el editor universal permite editar cualquier aspecto de cualquier contenido en cualquier implementación para que pueda ofrecer experiencias excepcionales, aumentar la velocidad del contenido y proporcionar una experiencia de desarrollador avanzada.
* [Creación de contenido con el editor universal](authoring.md): aprenda lo fácil e intuitivo que es para los autores de contenido crearlo con el editor universal.
* [Publicación de contenido con el editor universal](publishing.md): descubra cómo el editor visual universal publica contenido y cómo sus aplicaciones pueden gestionar el publicado.
* [Introducción al editor universal en AEM](getting-started.md): obtenga información sobre cómo acceder al editor universal y cómo instrumentar la primera aplicación de AEM para utilizarlo.
* [Arquitectura del editor universal](architecture.md): obtenga información acerca de la arquitectura del editor universal y cómo fluyen los datos entre sus servicios y capas.
* [Autenticación del editor universal](authentication.md): obtenga información sobre cómo se autentica el editor universal.
