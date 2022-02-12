---
title: Introducción a AEM sin encabezado
description: Recursos informativos y enlaces a la documentación de Adobe Experience Manager (AEM) sin encabezado. Descubra cómo se utilizan funciones como modelos de contenido, fragmentos de contenido y una API de GraphQL para potenciar las experiencias sin objetivos con AEM.
landing-page-description: Obtenga información sobre cómo utilizar y administrar Experience Manager as a Cloud Service sin encabezado.
exl-id: 24300499-ae9c-49d0-aa25-f51e14d9cf79
source-git-commit: c5d67e0ece40cdf7a9009436ec90305fe81425a2
workflow-type: tm+mt
source-wordcount: '626'
ht-degree: 2%

---


# Introducción a Adobe Experience Manager Headless  {#introduction-aem-headless}

Descubra cómo se utilizan las funciones de Adobe Experience Manager (AEM), como los modelos de contenido, los fragmentos de contenido y una API de GraphQL, para impulsar experiencias sin objetivos a escala.

## Información general {#overview}

AEM sin encabezado es una solución de CMS de Experience Manager que permite que cualquier aplicación a través de HTTP que use GraphQL consuma contenido estructurado (fragmentos de contenido) en AEM. Las implementaciones sin encabezado permiten el envío de experiencias entre plataformas y canales a escala.

La implementación sin encabezado renuncia a la administración de páginas y componentes, ya que es tradicional en soluciones híbridas y de pila completas y se centra en la creación de fragmentos de contenido neutros para el canal y reutilizables y su envío por canales cruzados. Es un patrón de desarrollo moderno y dinámico para implementar experiencias web.

![Modelos de implementación de AEM](assets/aem-implementation-models.png)

## Características de AEM sin encabezado {#aem-headless-features}

AEM as a Cloud Service es una herramienta flexible para el modelo de implementación sin objetivos que ofrece tres potentes características:

1. **Modelos de contenido**
   * Los modelos de contenido son una representación estructurada del contenido.
   * Los modelos de contenido se definen mediante arquitectos de información en el editor del Modelo de fragmentos de contenido de AEM.
   * Los modelos de contenido sirven de base para los fragmentos de contenido.
1. **Fragmentos de contenido**
   * Los fragmentos de contenido se crean en función de un modelo de contenido.
   * Creado por los autores de contenido mediante el editor de fragmentos de contenido de AEM.
   * Los fragmentos de contenido se almacenan en AEM Assets y se administran en la interfaz de usuario del administrador de recursos.
1. **API de contenido para envío**
   * La API de AEM GraphQL es compatible con la entrega de fragmentos de contenido.
   * La API de REST de AEM Assets es compatible con las operaciones de CRUD de fragmento de contenido.
   * La entrega de contenido directo también es posible con el [Exportación JSON del componente principal del fragmento de contenido](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/content-fragment-component.html).

## Sus primeros pasos con AEM sin encabezado {#first-steps}

Hay varios recursos disponibles para empezar a utilizar AEM funciones sin encabezado. Cada guía está diseñada para diferentes casos de uso y audiencias.

| Medio | Descripción | Tipo | Audience | Este. Hora |
|---|---|---|---|---|
| [Recorrido para desarrolladores de Headless](/help/journey-headless/developer/overview.md) | **Para desarrolladores nuevos en AEM y sin encabezado** tecnologías, empiecen aquí por una introducción completa a la AEM y sus características sin cabeza de la teoría de no tener cabeza a través de vivir con su primer proyecto sin cabeza. | Guía | Desarrolladores **nuevo en AEM y sin cabeza** | 1 hora |
| [Configuración sin encabezado](/help/headless/setup/introduction.md) | **Para usuarios AEM con experiencia** para obtener un breve resumen de las funciones principales AEM sin encabezado, consulte esta descripción general de inicio rápido. | Configuración de referencia | Desarrolladores, administradores **con AEM experiencia** | 20 minutos |
| [Tutorial práctico sin encabezado](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/multi-step/overview.html) | **Si prefiere un enfoque práctico y está familiarizado con AEM**, este tutorial se sumerge directamente en la implementación de una aplicación sencilla sin encabezado. | Tutorial | Desarrolladores | 2 horas |
| [Recorrido de arquitectos sin encabezado](/help/journey-headless/architect/overview.md) | **Para arquitectos nuevos a AEM y sin cabeza** , comience aquí para ver una introducción a las potentes y flexibles funciones de Adobe Experience Manager as a Cloud Service y cómo modelar el contenido de su proyecto. | Guía | Arquitectos | 1 hora |
| [Recorrido de creación sin encabezado](/help/journey-headless/author/overview.md) | **Para usuarios empresariales nuevos a AEM y sin periféricos** , comience aquí para ver una introducción a las potentes y flexibles funciones de Adobe Experience Manager as a Cloud Service y cómo modelar el contenido de su proyecto. | Guía | Creadores de contenido | 1 hora |
| [Recorrido de traducción sin encabezado](/help/journey-headless/translation/overview.md) | Para aquellos **interesados en AEM enfoque de traducción hacia los usuarios sin encabezado**. Obtenga información sobre tecnologías sin encabezado y cómo crear y actualizar proyectos de traducción en AEM de A a Z. | Guía | Especialistas en traducción | 1 hora |

## Comparación de encabezados y sin encabezado {#headful-headless}

Esta guía se centra en el modelo completo de implementación sin objetivos de AEM. Sin embargo, la cabeza contra la cabeza no tiene por qué ser una elección binaria en AEM. Las funciones sin encabezado se pueden usar para administrar y entregar contenido a varios puntos de contacto, al tiempo que se permite a los autores de contenido editar aplicaciones de una sola página. Todo en AEM.

>[!TIP]
>
>Consulte el documento [Encabezado y sin cabeza en AEM](/help/implementing/developing/headful-headless.md) para obtener más información.