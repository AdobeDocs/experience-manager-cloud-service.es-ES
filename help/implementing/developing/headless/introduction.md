---
title: Desarrollo sin cabeza para AEM Sites como Cloud Service
description: El uso de potentes funciones como modelos de contenido, fragmentos de contenido y la API de GraphQL, AEM como Cloud Service, le permite administrar sus experiencias de forma centralizada y ofrecerlas en distintos canales.
translation-type: tm+mt
source-git-commit: e1db93e8f4cf8ef881b274879e800c9993753a66
workflow-type: tm+mt
source-wordcount: '573'
ht-degree: 2%

---


# Desarrollo sin cabeza para AEM Sites como Cloud Service {#headless-development}

El uso de potentes funciones como modelos de contenido, fragmentos de contenido y la API de GraphQL, AEM como Cloud Service, le permite administrar sus experiencias de forma centralizada y ofrecerlas en distintos canales.

## Información general {#overview}

La implementación sin objetivos se está volviendo cada vez más importante para ofrecer experiencias a su audiencia, donde quiera que estén y sin importar el canal.

La implementación sin cabezales evita la administración de páginas y componentes, al igual que las soluciones híbridas y de pila completas tradicionales, y se centra en la creación de fragmentos de contenido neutros para el canal y reutilizables y su envío entre canales. Es un modelo de desarrollo moderno y dinámico para la implementación de experiencias web.

![Modelos de implementación de AEM](assets/aem-implementation-models.png)

## Comparación de encabezados y sin cabeza {#headful-headless}

Este documento se centra en el modelo completo de implementación sin cabeza de AEM. Sin embargo, la cabeza contra la cabeza no tiene por qué ser una opción binaria en AEM. Las funciones sin encabezado se pueden utilizar para administrar y entregar el contenido a una variedad de extremos, a la vez que se permite a los autores de contenido editar aplicaciones de una sola página. Todo en AEM.

>[!TIP]
>
>Consulte el documento [Encabezado y sin cabeza en AEM](/help/implementing/developing/headful-headless.md) para obtener más información.

## AEM como Cloud Service y sin cabeza {#aem-headless}

AEM como Cloud Service es una herramienta flexible para el modelo de implementación sin cabeza que ofrece tres potentes servicios:

1. Modelos de contenido
   * Los modelos de contenido son una representación estructurada del contenido.
   * Estos son definidos por arquitectos de información en el editor del Modelo de fragmentos de contenido de AEM.
   * Los modelos de contenido sirven de base para los fragmentos de contenido.
1. Fragmentos de contenido
   * Los fragmentos de contenido son instancias de modelos de contenido.
   * Los crean los autores de contenido mediante el editor de fragmentos de contenido de AEM.
   * Se almacenan en AEM Assets y se administran en la interfaz de usuario del administrador de recursos.
1. Content API for envío
   * La API de AEM GraphQL admite el envío de fragmentos de contenido.
   * La API de AEM Assets REST admite operaciones de CRUD de fragmento de contenido.
   * También es posible el envío de contenido directo con la exportación JSON del componente principal del [fragmento de contenido.](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/components/content-fragment-component.html)

## Guías de introducción sin cabeza {#getting-started}

Las guías de introducción sin encabezado establecen una ruta sencilla para crear, administrar y distribuir experiencias con AEM como Cloud Service en cinco pasos. Cada guía se basa en la anterior, por lo que se recomienda explorarlas a fondo y en orden.

1. [Creación de una configuración](getting-started/create-configuration.md)
1. [Creación de un modelo de fragmento de contenido](getting-started/create-content-model.md)
1. [Creación de una carpeta de recursos](getting-started/create-assets-folder.md)
1. [Creación de un fragmento de contenido](getting-started/create-content-fragment.md)
1. [Acceso y entrega de fragmentos de contenido](getting-started/create-api-request.md)

## Audience {#audience}

Las tareas que se describen en las [Guías de introducción sin cabeza](#getting-started) son necesarias para una demostración básica end-to-end de AEM capacidades sin cabeza. Cualquier persona con acceso de administrador a una instancia de AEM de prueba puede seguir estas guías para comprender el envío sin encabezado en AEM, aunque alguien con experiencia de desarrollador es ideal.

Sin embargo, en una situación de producción, las tareas serán llevadas a cabo por diferentes personalidades varias veces. Por ejemplo:

* **Los** administradores deberán configurar la configuración inicial y la estructura de carpetas para el contenido normalmente solo una vez o de forma esporádica.
* **Las** arquitecturas de información generalmente añadirán nuevos modelos a medida que evolucionen las necesidades de la organización.
* **Los** autores de contenido crearán continuamente contenido nuevo como fragmentos de contenido en función de los modelos definidos por los arquitectos.

Las guías de introducción sin encabezado señalan quién generalmente realizará las tareas descritas y con qué frecuencia.

## Etapa siguiente {#next-step}

¿Listo para aprender más? A continuación, lea la primera parte de la Guía de introducción sin cabeza: [Creación de una configuración.](getting-started/create-configuration.md)
