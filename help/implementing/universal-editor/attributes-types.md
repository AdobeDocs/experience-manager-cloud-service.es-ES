---
title: Atributos y tipos
description: Obtenga información sobre los atributos y tipos de datos que requiere el Editor universal.
source-git-commit: 0e66c379e10d275610d85a699da272dc0c32a9a8
workflow-type: tm+mt
source-wordcount: '661'
ht-degree: 7%

---


# Atributos y tipos {#attributes-types}

Obtenga información sobre los atributos y tipos de datos que requiere el Editor universal.

## Introducción {#introduction}

Para que el Editor universal pueda editar una aplicación, debe instrumentarse correctamente. Esto incluye incluir los metadatos adecuados para que el editor pueda editar el contenido de la aplicación. Este documento detalla los atributos y tipos de esos metadatos.

>[!NOTE]
>
>La validación de contenido se realiza en el servidor. El editor universal solo funciona con los atributos de datos. La validación que se ajusta al modelo o la estructura debe abordarse en el nivel de API.

## Propiedades de datos {#data-properties}

| Propiedad Data | Descripción |
|---|---|
| `itemid` | URL del recurso, consulte la sección [Instrumente la página del documento Introducción al Editor universal en AEM](getting-started.md#instrument-thepage) |
| `itemprop` | Atributo del recurso, consulte la sección [Instrumente la página del documento Introducción al Editor universal en AEM](getting-started.md#instrument-thepage) |
| `itemtype` | Tipo del elemento editable (por ejemplo, texto, imagen, referencia, etc.) |
| `data-editor-itemfilter` | Define qué referencias se pueden utilizar |
| `data-editor-itemlabel` | Define una etiqueta personalizada para un elemento seleccionable que se muestra en el editor <br>En el caso `itemmodel` está configurado, la etiqueta se recupera mediante el modelo |
| `data-editor-itemmodel` | Define un modelo que se utilizará para la edición basada en formularios en el carril de propiedades |
| `data-editor-behavior` | Define el comportamiento de una instrumentación, por ejemplo, el texto independiente o la imagen también pueden imitar un componente para que se pueda mover o eliminar |

## Tipos de elementos {#item-types}

| `itemtype` | Descripción | `itemid` | `itemprop` | `data-editor-itemfilter` | `data-editor-itemlabel` | `data-editor-itemmodel` | `data-editor-behvior` |
|---|---|---|---|---|---|---|---|
| `text` | El texto se puede editar dentro de las etiquetas del HTML, pero solo en formato de texto simple, sin formato de texto enriquecido disponible, este formato se suele utilizar en los componentes del título, por ejemplo | Opcional | Requerido | N/D | Opcional | N/D | Opcional |
| `richtext` | El texto es editable con capacidades de texto enriquecido completas. RTE se mostrará en el panel derecho | Opcional | Requerido | N/D | Opcional | N/D | Opcional |
| `media` | El elemento editable es un recurso, por ejemplo, una imagen o un vídeo | Opcional | Requerido | Opcional<br>lista de criterios de filtro de imagen o vídeo que se pasan al selector de recursos | Opcional | N/D | Opcional |
| `container` | El comportamiento editable se comporta como contenedor para componentes, también conocido como Sistema de párrafos. | Depende <br>consulte más abajo | Depende <br>consulte más abajo | Opcional<br>una lista de componentes permitidos | Opcional | N/D | N/D |
| `component` | El componente editable es un componente. No agrega funcionalidad adicional, será necesario para indicar partes móviles/eliminables del DOM y para abrir el carril de propiedades y sus campos | Requerido | N/D | N/D | Opcional | Opcional | N/D |
| `reference` | La editable es una referencia, por ejemplo: fragmento de contenido, fragmento de experiencia o producto | Depende <br>consulte más abajo | Depende <br>consulte más abajo | Opcional<br>lista de criterios de filtro de fragmento de contenido, producto o fragmento de experiencia que se pasan al selector de referencia | Opcional | Opcional | N/D |

Dependiendo del caso de uso `itemprop` o `itemid` puede o no ser obligatorio. Por ejemplo:

* `itemid` es necesario si consulta los fragmentos de contenido a través de GraphQL y desea que la lista sea editable en contexto.
* `itemprop` es necesario en caso de que tenga un componente que procese el contenido de un fragmento de contenido al que se hace referencia y desee actualizar la referencia dentro del componente.

## Comportamientos {#behaviors}

| `data-editor-behavior` | Descripción |
|---|---|
| `component` | Se puede utilizar para permitir que los componentes de texto independiente, texto enriquecido y medios imiten, de modo que también se puedan mover y eliminar en la página. |

## Recursos adicionales {#additional-resources}

Para obtener más información sobre el Editor universal, consulte estos documentos.

* [Introducción al Editor universal](introduction.md) : Descubra cómo el Editor universal permite editar cualquier aspecto de cualquier contenido en cualquier implementación para ofrecer experiencias excepcionales, aumentar la velocidad de contenido y proporcionar una experiencia de desarrollador de última generación.
* [Creación de contenido con el editor universal](authoring.md) : Aprenda lo fácil e intuitivo que es para los autores de contenido crear contenido con el Editor universal.
* [Publicación de contenido con el Editor universal](publishing.md) : Descubra cómo el Editor visual universal publica contenido y cómo sus aplicaciones pueden gestionar el contenido publicado.
* [Introducción al Editor universal en AEM](getting-started.md) : Obtenga información sobre cómo acceder al Editor universal y cómo instrumentar la primera aplicación de AEM para utilizarla.
* [Arquitectura de editor universal](architecture.md) - Obtenga información sobre la arquitectura del Editor universal y cómo fluyen los datos entre sus servicios y capas.
* [Autenticación del editor universal](authentication.md) - Obtenga información sobre cómo se autentica el editor universal.
