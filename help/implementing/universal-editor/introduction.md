---
title: Introducción al Editor universal
description: Descubra cómo el Editor universal permite editar cualquier aspecto de cualquier contenido en cualquier implementación para ofrecer experiencias excepcionales, aumentar la velocidad de contenido y proporcionar una experiencia de desarrollador de última generación.
source-git-commit: f454475b65da8f410812bbbe30ca5fc393be410a
workflow-type: tm+mt
source-wordcount: '931'
ht-degree: 0%

---


# Introducción al Editor universal {#introduction}

Descubra cómo el Editor universal permite editar cualquier aspecto de cualquier contenido en cualquier implementación para ofrecer experiencias excepcionales, aumentar la velocidad de contenido y proporcionar una experiencia de desarrollador de última generación.

## Fondo {#background}

La herramienta más potente para el autor de contenido de AEM ha sido el editor de páginas. El editor de páginas ofrece una experiencia de creación WYSIWYG intuitiva, visual y en contexto que requiere una formación mínima y muestra a los autores exactamente cómo aparecerá el contenido.

Sin embargo, el editor de páginas solo puede editar AEM contenido de la página, su estructura y los componentes que contiene. Sin embargo, en la actualidad el contenido rara vez proviene de una ubicación. El editor universal ofrece la misma experiencia de edición in situ que el editor de páginas, pero para cualquier aspecto de cualquier contenido en cualquier implementación.

## Verdaderamente universal {#universal}

El editor universal puede instrumentarse para cualquier implementación, para cualquier contenido y para cualquier aspecto del contenido.

![Lo que hace que sea universal](assets/universal.png)

### Cualquier implementación {#any-implementation}

Dado que las experiencias se pueden crear de muchas formas diferentes, cualquier implementación puede aprovechar el Editor universal para que los autores puedan realizar la edición en contexto.

Los usuarios suelen pensar que una implementación sin encabezado limita a los autores a editar todo el contenido en una interfaz de usuario basada en formularios, pero esto no es cierto con el Editor universal

Los requisitos de una implementación para aprovechar el Editor universal son muy directos y admiten:

* **Cualquier arquitectura** - Renderización del lado del servidor, renderización del lado del borde, renderización del lado del cliente, etc.
* **Cualquier marco** - AEM de vainilla, o cualquier estructura de terceros como React, Next.js, Angular, etc.
* **Cualquier alojamiento** : se puede alojar localmente en AEM o en un dominio remoto

### Cualquier contenido {#any-content}

Un autor de contenido debe tener la misma potente experiencia de edición que ofrecía anteriormente el editor de páginas de AEM. Sin embargo, el Editor universal permite a los autores de contenido editar **any** contenido visual y en contexto y admite:

* **AEM estructuras de página** - Anidado `cq:Components` de `cq:Pages`, incluidos los fragmentos de experiencias
* **AEM fragmentos de contenido** - Editar contenido desde fragmentos de contenido tal como aparecen en el contexto de la experiencia
* **Documentos** : Word, Excel, Google Docs, Markdown o incluso un HTML sin formato persistieron, por ejemplo, en GitHub
* **Contenido de terceros** - Un sistema de complementos permite hacer que cualquier fuente de contenido externo sea editable.

### Cualquier aspecto {#any-aspect}

Para un autor de contenido, el contenido no es solo información contenida, sino también cómo se procesa y recibe. El contenido viene con metadatos adicionales y reglas de instrumentación que el editor universal puede comprender y editar, como por ejemplo:

* **Aplicación de diseño y estilo** - Mediante un sistema de estilos, el profesional de marketing y el autor de contenido pueden aplicar distintos estilos a su contenido y crear diferentes diseños, como columnas, carruseles, pestañas, acordeones, etc.
* **Realización de experimentos** - Al publicar una nueva versión de contenido que desafía el contenido existente, el profesional de marketing puede experimentar con mejoras de contenido y medir el impacto.
* **Personalización de variaciones** : Al crear y administrar variaciones de contenido específicas para audiencias determinadas, los profesionales de marketing pueden personalizar el contenido que se envía.

## Valor {#value}

Al desvincular la experiencia de edición de contenido de cualquier sistema de entrega de contenido en particular, el editor se vuelve verdaderamente universal y flexible, lo que permite al autor de contenido ofrecer experiencias excepcionales, aumentar la velocidad de contenido y proporcionar una experiencia de desarrollador de última generación.

![El valor del Editor universal](assets/value.png)

* **Ofrecer experiencias excepcionales** - Para permitir que los profesionales creen una experiencia atractiva para los visitantes, el Editor universal permite a los profesionales crear y editar el contenido en el contexto de la vista previa. Esto les permite crear contenido que se ajuste al diseño de la experiencia y que constituye un recorrido significativo para los visitantes.
* **Aumentar la velocidad del contenido** - Para simplificar el flujo de trabajo de administración de los profesionales, el Editor universal permite editar contenido en la vista previa para guiar a los profesionales mostrando solo las opciones que son relevantes para ese contexto y hace que el flujo de trabajo sea independiente de las fuentes de contenido.
* **Experiencia para desarrolladores de vanguardia** - Para soportar un panorama de aplicaciones heterogéneo en el mundo real, el editor universal está completamente disociado y no depende de la tecnología, lo que permite a los desarrolladores utilizar su pila de tecnología preferida para implementar la experiencia.

## Editor universal y el editor de fragmentos de contenido {#universal-editor-content-fragment-editor}

A primera vista, puede parecer que el editor universal y el editor de fragmentos de contenido proporcionan funciones de edición similares. Sin embargo, estos editores ofrecen capacidades muy diferentes y realizan diferentes trabajos del profesional de marketing.

### Editor de fragmentos de contenido {#content-fragment-editor}

Un profesional de marketing quiere crear contenido sin tener que preocuparse por su diseño, de modo que se pueda reutilizar en numerosos contextos de la experiencia.

* El trabajo subyacente que se debe realizar es escalar la estrategia de contenido.

### Editor universal {#universal-editor}

Un profesional de marketing quiere crear contenido que esté adaptado al diseño de un contexto determinado para ofrecer una experiencia excepcional.

* El trabajo subyacente que hay que realizar es conectar de manera convincente con los lectores.

## Hoja de ruta {#road-map}

Es importante señalar que el Editor universal es un trabajo en curso y las capacidades que se describen en este documento son una visión del editor final y no necesariamente de sus capacidades actuales.

Hable con su contacto de Adobe para obtener más información sobre las próximas funciones planificadas para el editor universal

## Recursos adicionales {#additional-resources}

Para obtener más información sobre el Editor universal, consulte estos documentos.

* [Creación de contenido con el editor universal](authoring.md) : Aprenda lo fácil e intuitivo que es para los autores de contenido crear contenido con el Editor universal.
* [Introducción al Editor universal en AEM](getting-started.md) : Obtenga información sobre cómo acceder al Editor universal y cómo instrumentar la primera aplicación de AEM para utilizarla.
* [Arquitectura de editor universal](architecture.md) - Obtenga información sobre la arquitectura del Editor universal y cómo fluyen los datos entre sus servicios y capas.
* [Atributos y tipos](attributes-types.md) : Obtenga información sobre los atributos y tipos de datos que requiere el Editor universal.
* [Autenticación del editor universal](authentication.md) - Obtenga información sobre cómo se autentica el editor universal.
