---
title: Desarrollo sin encabezado para AEM Sites as a Cloud Service
description: Descubra cómo AEM como potentes funcionalidades sin objetivos de un Cloud Service, como modelos de contenido, fragmentos de contenido y la API de GraphQL, trabajan juntos para permitirle administrar sus experiencias de forma centralizada y servirlas en todos los canales.
exl-id: 24300499-ae9c-49d0-aa25-f51e14d9cf79
source-git-commit: 816c08b9351b3ce2fd4f31974d707e9d4a4eea27
workflow-type: tm+mt
source-wordcount: '489'
ht-degree: 4%

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

## Sus primeros pasos con AEM sin encabezado {#first-steps}

Hay varios recursos disponibles para que su usuario comience con AEM funciones sin encabezado. Están pensados para diferentes casos de uso, pero todos ofrecen una visión general sólida de AEM funciones sin encabezado.

| Medio | Descripción | Tipo | Audience | Este. Hora |
|---|---|---|---|---|
| [Recorrido para desarrolladores sin objetivos](/help/journey-headless/developer/overview.md) | Para obtener una visión general de AEM características sin objetivos de la teoría de la entrada sin objetivos con su primer proyecto sin cabeza, comience aquí. | Guía | Desarrolladores | 1 hora |
| [Guía de introducción sin encabezado](/help/implementing/developing/headless/getting-started/introduction.md) | Para obtener un breve resumen de las funciones principales AEM sin encabezado, consulte esta descripción general de inicio rápido. | Inicio rápido | Desarrolladores, administradores | 20 minutos |
| [Tutorial práctico Introducción a AEM sin encabezado](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/multi-step/overview.html) | Si prefiere un enfoque práctico, este tutorial se sumerge directamente en la creación de un proyecto sencillo sin encabezado. | Tutorial | Desarrolladores | 2 horas |
