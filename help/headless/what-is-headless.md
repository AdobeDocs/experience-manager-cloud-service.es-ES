---
title: ¿Qué es un CMS sin cabeza?
description: Obtenga información sobre CMS sin encabezado. ¿Cómo funcionan? ¿Cuáles son las alternativas y diferencias? ¿Por qué querría utilizar un CMS sin encabezado?
source-git-commit: 35064ef7d9a4a3f2368667be02b11840b29d56f0
workflow-type: tm+mt
source-wordcount: '754'
ht-degree: 0%

---


# ¿Qué es un CMS sin cabeza? {#what-is-a-headless-cms}

La administración de contenido sin encabezado es un desarrollo clave para el diseño web actual que desvincula las aplicaciones de cliente y front-end del sistema de administración de contenido y back-end. Por lo tanto, un CMS sin encabezado es responsable de los servicios de administración de contenido (back-end), junto con los mecanismos que permiten a las aplicaciones (front-end) acceder a ese contenido.

Pero, ¿qué significa realmente el término? Aquí ofrecemos una introducción (muy rápida) a los conceptos clave.

## ¿Qué es un sistema de administración de contenido (CMS)? {#content-management-system}

Empecemos con lo básico: ¿qué es un sistema de administración de contenido?

Un sistema de administración de contenido (CMS) almacena, administra y ofrece el contenido utilizado para ofrecer sus experiencias en línea.

## CMS tradicional {#traditional-cms}

Tradicionalmente, un CMS ha incluido la funcionalidad back-end para el almacenamiento y la entrega de contenido, junto con la tecnología de front-end utilizada para representar el marcado de una experiencia que mostrará su navegador (la capa de presentación).

Muy potente, que le permite un control total del contenido y del formato, pero que carece de la flexibilidad necesaria en el entorno de movimiento rápido actual; por ejemplo, al interconectar con aplicaciones externas.

## CMS sin encabezado {#headless-cms}

Con un sistema de administración de contenido sin objetivos, el back-end y el front-end están ahora disociados.

La parte sin encabezado es el back-end de contenido.

* &quot;*Un sistema de administración de contenido sin encabezado, o CMS sin encabezado, es un sistema de administración de contenido (CMS) de back-end creado desde cero como repositorio de contenido que hace que el contenido sea accesible a través de una API para su visualización en cualquier dispositivo.*

   Consulte [Wikipedia](https://en.wikipedia.org/wiki/Headless_content_management_system).

El front-end, que se desarrolla y mantiene de forma independiente, obtiene contenido del backend sin encabezado mediante una API de envío de contenido, normalmente en formato JSON. Por ejemplo, esto podría ser como una aplicación React o Angular (Aplicación de una sola página (SPA)).

Un backend CMS sin encabezado generalmente requiere que el contenido esté estructurado, basado en un modelo o esquema. Esto facilita a las aplicaciones cliente que solicitan el contenido adecuado para procesar una experiencia. Algunos CMS pueden exponer contenido estructurado y no estructurado en formato JSON.

Una característica clave de esta topología es que el contenido servido por el CMS sin encabezado en formato JSON es contenido puro, sin información de diseño o diseño. En una implementación sin encabezado de CMS, todo el formato y el diseño se mantienen en la aplicación de front-end desacoplada.

Una ventaja clave de una topología CMS sin objetivos es la capacidad de reutilizar contenido en varios canales, que pueden utilizar diferentes implementaciones de front-end del lado del cliente. Esto puede hacer que el proceso de desarrollo de front-end sea más eficiente. Pero también significa que el proceso de desarrollo de experiencias de vanguardia puede convertirse en un proceso centrado en el código y la TI, y que, básicamente, la TI es la propietaria de la experiencia.

## API de envío de contenido {#content-delivery-apis}

Un CMS sin encabezado puede proporcionar una o varias formas de exponer el contenido a aplicaciones del lado del cliente. Normalmente, las API de HTTP REST, las API de GraphQL o ambas.

Aunque una API de REST a menudo parece una forma más sencilla de solicitar contenido (por ejemplo, proporcionando JSON para todo el contenido que coincida con un criterio), normalmente envía demasiado contenido a una aplicación cliente. Esto puede hacer que el cliente tenga que analizar y filtrar el contenido que realmente se necesita para la renderización.

GraphQL, por el contrario, es un mecanismo más centrado para permitir que las aplicaciones cliente consulten exactamente el contenido necesario para procesar una experiencia.

## CMS de pila completa {#fullstack-cms}

Un CMS de pila completa normalmente representa la topología tradicional para la administración y entrega de contenido, al incluir la tecnología de back-end y front-end de contenido para la representación de experiencias. La entrega de contenido en CMS de pila completa suele ocurrir en las API de entrega de contenido interno. La funcionalidad de front-end suele ser específica del CMS de pila completa. Este acoplamiento de tecnología de front-end con el back-end de contenido permite la creación de experiencias (WYSIWYG) como una ventaja clave.

## CMS híbrido {#hybrid-cms}

Una evolución moderna del CMS de pila completa puede ser un CMS híbrido. Esto pretende combinar lo mejor de ambos mundos:

* desarrollo eficiente del front-end en los canales mediante herramientas de front-end modernas,
* conservando la creación de experiencias WYSIWYG para potenciar a los usuarios no técnicos y evitar que la TI se convierta en un obstáculo para la gestión de contenido y experiencia entre organizaciones.

Esto se logra adoptando marcos de front-end modernos como React, pero manteniendo un mínimo esencial de acoplamiento con el back-end de contenido.

## CMS desempañado {#decoupled-cms}

Aunque el término CMS disociado a veces se utiliza de forma independiente, esencialmente describe un servidor CMS remoto al resaltar su característica clave de estar desunido de la aplicación de front-end del lado del cliente.

## CMS con encabezado {#headful-cms}

Este es otro término para un CMS tradicional.

## Lectura adicional {#further-reading}

Puede leer más sobre el uso de AEM en una topología CMS sin encabezado aquí:

* [Introducción a Adobe Experience Manager as a Headless CMS](/help/headless/introduction.md)
