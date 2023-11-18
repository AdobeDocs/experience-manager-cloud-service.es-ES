---
title: Atributos y tipos
description: Obtenga información acerca de los atributos y tipos de datos que requiere el editor universal.
exl-id: 02795a31-244a-42b4-8297-2649125d7777
source-git-commit: 6bb7b2d056d501d83cf227adb239f7f40f87d0ce
workflow-type: tm+mt
source-wordcount: '682'
ht-degree: 85%

---


# Atributos y tipos {#attributes-types}

Obtenga información acerca de los atributos y tipos de datos que requiere el editor universal.

## Introducción {#introduction}

Para que el editor universal pueda editar una aplicación, debe instrumentarse correctamente. Esto incluye introducir los metadatos adecuados para que el editor pueda modificar el contenido de la aplicación. Este documento detalla los atributos y tipos de esos metadatos.

>[!NOTE]
>
>La validación de contenido se ejecuta en el lado del servidor. El editor universal solo funciona con los atributos de datos. La validación de que se ajustan al modelo o la estructura debe realizarse en el nivel de API.

## Propiedades de datos {#data-properties}

| Propiedad de los datos | Descripción |
|---|---|
| `itemid` | Para el URN del recurso, consulte la sección [Instrumentación de la página del documento Introducción al editor universal en AEM](getting-started.md#instrument-thepage) |
| `itemprop` | Para el atributo del recurso, consulte la sección [Instrumentación de la página del documento Introducción al editor universal en AEM](getting-started.md#instrument-thepage) |
| `itemtype` | Tipo del elemento editable (por ejemplo, texto, imagen, referencia, etc.) |
| `data-editor-itemfilter` | Define qué referencias se pueden utilizar |
| `data-editor-itemlabel` | Define una etiqueta personalizada para un elemento seleccionable que se muestra en el editor. <br>Si `itemmodel` está configurado, la etiqueta se recupera mediante el modelo |
| `data-editor-itemmodel` | Define un modelo que se usa para la edición basada en formularios en el carril de propiedades |
| `data-editor-behavior` | Define el comportamiento de una instrumentación; por ejemplo, el texto o la imagen independientes también pueden imitar un componente para hacerlo móvil o eliminable |

## Tipos de elementos {#item-types}

| `itemtype` | Descripción | `itemid` | `itemprop` | `data-editor-itemfilter` | `data-editor-itemlabel` | `data-editor-itemmodel` | `data-editor-behvior` |
|---|---|---|---|---|---|---|---|
| `text` | El texto se puede editar dentro de las etiquetas HTML, pero solo en formato de texto simple, no tiene un formato de texto enriquecido disponible. Se suele utilizar en los componentes del título, por ejemplo. | Opcional | Requerido | N/D | Opcional | N/D | Opcional |
| `richtext` | El texto se puede editar con capacidades de texto enriquecido completas. El RTE se muestra en el panel derecho | Opcional | Requerido | N/D | Opcional | N/D | Opcional |
| `media` | El editable es un recurso, por ejemplo, una imagen o un vídeo | Opcional | Requerido | Opcional<br>lista de criterios de filtro de imagen o vídeo que se pasan al selector de recursos | Opcional | N/D | Opcional |
| `container` | El comportamiento editable se comporta como un contenedor para componentes, también conocido como Sistema de párrafos. | Depende <br>consultar más abajo | Depende <br>consultar más abajo | Opcional<br>una lista de componentes permitidos | Opcional | N/D | N/D |
| `component` | El componente editable es un componente. No añade ninguna funcionalidad adicional. Es necesario para indicar partes móviles o eliminables del DOM y para abrir el carril de propiedades y sus campos | Requerido | N/D | N/D | Opcional | Opcional | N/D |
| `reference` | El editable es una referencia, por ejemplo, un fragmento de contenido, un fragmento de experiencia o un producto | Depende <br>consultar más abajo | Depende <br>consultar más abajo | Opcional<br>lista de criterios de filtro de fragmento de contenido, producto o fragmento de experiencia que se pasan al selector de referencia | Opcional | Opcional | N/D |

Dependiendo del caso de uso, `itemprop` o `itemid` pueden no ser obligatorios. Por ejemplo:

* `itemid` es necesario si consulta los fragmentos de contenido a través de GraphQL y desea que la lista sea editable en contexto.
* `itemprop` es necesario en caso de que tenga un componente que procese el contenido del fragmento de contenido al que se hace referencia y desee actualizar la referencia.

## Comportamientos {#behaviors}

| `data-editor-behavior` | Descripción |
|---|---|
| `component` | Se utiliza para permitir componentes de imitación de texto, texto enriquecido y medios independientes, de modo que también se pueda mover y eliminar en la página |
| `container` | Se utiliza para permitir que los contenedores se traten como sus propios componentes, de modo que se puedan mover y eliminar en la página |

## Recursos adicionales {#additional-resources}

Para obtener más información acerca del editor universal, consulte estos documentos.

* [Introducción al editor universal](introduction.md): descubra cómo el editor universal permite editar cualquier aspecto de los contenidos en varias implementaciones para ofrecer experiencias excepcionales, aumentar la velocidad de contenido y proporcionar una experiencia de desarrollador de última generación.
* [Creación de contenido con el editor universal](authoring.md): aprenda lo fácil e intuitivo que es para los autores de contenido crearlo con el editor universal.
* [Publicación de contenido con el editor universal](publishing.md): descubra cómo el editor universal publica contenido y cómo sus aplicaciones pueden gestionar el publicado.
* [Introducción al editor universal en AEM](getting-started.md): obtenga información sobre cómo acceder al editor universal y cómo instrumentar la primera aplicación de AEM para utilizarlo.
* [Arquitectura del editor universal](architecture.md): obtenga información acerca de la arquitectura del editor universal y cómo fluyen los datos entre sus servicios y capas.
* [Autenticación del editor universal](authentication.md): obtenga información sobre cómo se autentica el editor universal.
