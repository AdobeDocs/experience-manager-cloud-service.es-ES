---
title: Desarrollo sin encabezado para AEM Sites as a Cloud Service
description: Descubra cómo AEM como potentes funcionalidades sin objetivos de un Cloud Service, como modelos de contenido, fragmentos de contenido y la API de GraphQL, trabajan juntos para permitirle administrar sus experiencias de forma centralizada y servirlas en todos los canales.
translation-type: tm+mt
source-git-commit: e7ca6dc841ba777384be74021a27d523d530a956
workflow-type: tm+mt
source-wordcount: '583'
ht-degree: 2%

---


# Desarrollo sin encabezado para AEM Sites as a Cloud Service {#headless-development}

Descubra cómo AEM como potentes funcionalidades sin objetivos de un Cloud Service, como modelos de contenido, fragmentos de contenido y la API de GraphQL, trabajan juntos para permitirle administrar sus experiencias de forma centralizada y servirlas en todos los canales.

## Información general {#overview}

La implementación sin objetivos es cada vez más importante para ofrecer experiencias a su audiencia, independientemente del canal y dónde se encuentren.

La implementación sin encabezado renuncia a la administración de páginas y componentes, ya que es tradicional en soluciones híbridas y de pila completas y se centra en la creación de fragmentos de contenido neutros para el canal y reutilizables y su envío por canales cruzados. Es un patrón de desarrollo moderno y dinámico para implementar experiencias web.

![Modelos de implementación de AEM](assets/aem-implementation-models.png)

## Comparación de encabezados y sin encabezado {#headful-headless}

Este documento se centra en el modelo completo de implementación sin objetivos de AEM. Sin embargo, la cabeza contra la cabeza no tiene por qué ser una elección binaria en AEM. Las funciones sin encabezado se pueden usar para administrar y entregar el contenido a una variedad de puntos finales, a la vez que permiten a los autores de contenido editar aplicaciones de una sola página. Todo en AEM.

>[!TIP]
>
>Consulte el documento [Headful and Headless en AEM](/help/implementing/developing/headful-headless.md) para obtener más información.

## AEM como Cloud Service y sin encabezado {#aem-headless}

AEM as a Cloud Service es una herramienta flexible para el modelo de implementación sin objetivos al ofrecer tres servicios potentes:

1. Modelos de contenido
   * Los modelos de contenido son una representación estructurada del contenido.
   * Se definen mediante arquitectos de información en el editor del Modelo de fragmento de contenido de AEM.
   * Los modelos de contenido sirven de base para los fragmentos de contenido.
1. Fragmentos de contenido
   * Los fragmentos de contenido son instancias de modelos de contenido.
   * Los crean los autores de contenido mediante el editor de fragmentos de contenido de AEM.
   * Se almacenan en AEM Assets y se administran en la interfaz de usuario del administrador de recursos.
1. API de contenido para envío
   * La API de AEM GraphQL es compatible con la entrega de fragmentos de contenido.
   * La API de REST de AEM Assets es compatible con las operaciones de CRUD de fragmento de contenido.
   * La entrega directa de contenido también es posible con la exportación JSON del [Componente principal del fragmento de contenido.](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/components/content-fragment-component.html)

## Guías de introducción sin encabezado {#getting-started}

Las guías de introducción sin encabezado establecen una ruta sencilla para crear, administrar y ofrecer experiencias con AEM como Cloud Service en cinco pasos. Cada guía se basa en la anterior, por lo que se recomienda explorarlas a fondo y en orden.

1. [Creación de una configuración](getting-started/create-configuration.md)
1. [Creación de un modelo de fragmento de contenido](getting-started/create-content-model.md)
1. [Creación de una carpeta de recursos](getting-started/create-assets-folder.md)
1. [Creación de un fragmento de contenido](getting-started/create-content-fragment.md)
1. [Acceso a fragmentos de contenido y envío](getting-started/create-api-request.md)

## Audience {#audience}

Las tareas descritas en las [Guías de introducción sin encabezado](#getting-started) son necesarias para una demostración completa básica de AEM capacidades sin encabezado. Cualquier persona con acceso de administrador a una instancia de AEM de prueba puede seguir estas guías para comprender la entrega sin objetivos en AEM, aunque es ideal alguien con experiencia de desarrollador.

Sin embargo, en una situación de producción, las tareas las realizan diferentes personas varias veces. Por ejemplo:

* **** Los administradores tendrán que configurar la configuración inicial y la estructura de carpetas para el contenido normalmente solo una vez o de forma esporádica.
* **En general, los** arquitectos de la información agregarán nuevos modelos a medida que evolucionen las necesidades de la organización.
* **Los** autores de contenido crearán continuamente nuevo contenido como fragmentos de contenido basados en los modelos definidos por los arquitectos.

Las guías de introducción sin encabezado señalan quién realizaría generalmente las tareas descritas y con qué frecuencia.

## Etapa siguiente {#next-step}

¿Listo para obtener más información? A continuación, comience leyendo la primera parte de la Guía de introducción sin encabezado: [Creación de una configuración.](getting-started/create-configuration.md)
