---
title: Recorrido para desarrolladores de CMS sin encabezado de AEM
description: Obtenga información sobre el desarrollo sin encabezado mediante Adobe Experience Manager (AEM) como un CMS sin encabezado. Aprender a utilizar funciones como modelos de contenido, fragmentos de contenido y una API de GraphQL para potenciar la entrega de contenido sin encabezado.
landing-page-description: Obtenga información sobre la entrega e implementación del contenido sin encabezado. Obtenga más información sobre el desarrollo de su estrategia dentro de su empresa.
exl-id: d14a1e30-dd04-49a8-8cda-27c80a4bb0f5
solution: Experience Manager
feature: Headless, Content Fragments,GraphQL API
role: Admin, Architect, Developer
source-git-commit: 2ccca86a0e611b93c273e37abb6e0fd7870421d4
workflow-type: tm+mt
source-wordcount: '930'
ht-degree: 95%

---

# Recorrido para desarrolladores de CMS sin encabezado de AEM {#aem-headless-developer-journey}

Bienvenidos a la documentación para los desarrolladores que son nuevos en CMS de Adobe Experience Manager sin encabezado.

Obtenga información sobre las funciones potentes y flexibles sin encabezado, sus capacidades y cómo utilizarlas en su primer proyecto de desarrollo sin encabezado. Este recorrido proporciona toda la información necesaria para desarrollar su primera aplicación sin encabezado.

>[!CONTEXTUALHELP]
>id="aemcloud_headless_developer_resources"
>title="Recursos para desarrolladores sin encabezado y documentación avanzada de AEM"
>abstract="Todo lo que necesita para aprender acerca de CMS sin encabezado de AEM y crear y enviar mejores aplicaciones y experiencias más rápidas."
>additional-url="https://experienceleague.adobe.com/landing/experience-manager/headless/developer.html?lang=es" text="Recursos para desarrolladores sin encabezado de AEM"


## Introducción {#introduction}

La implementación sin encabezado de AEM utiliza modelos de fragmentos de contenido y fragmentos de contenido para centrarse en la creación de fragmentos de contenido estructurados, de canal neutro y reutilizables, así como su entrega en varios canales. Para lograrlo, renuncia a la administración de páginas y componentes, como es habitual en las soluciones de pila completas. Es un patrón de desarrollo moderno y dinámico para implementar experiencias digitales.

Esta guía le conduce por los temas de implementación sin encabezado en AEM, por lo que cuando haya terminado podrá hacer lo siguiente:

* Comprenderá perfectamente qué es la entrega de contenido sin encabezado y sus ventajas.
* Comprenderá las funciones sin encabezado de AEM y cómo trabajan conjuntamente para ofrecer una experiencia sin encabezado.
* Realizar los primeros pasos en la implementación de su primer proyecto sin encabezado de AEM.

## Público {#audience}

Este recorrido está diseñado para el desarrollador y expone los requisitos, pasos y enfoque de un proyecto de AEM sin encabezado desde la perspectiva del desarrollador. El recorrido define las personas adicionales con las que el desarrollador debe interactuar para que un proyecto tenga éxito, pero el punto de vista del recorrido es el del desarrollador.

Los siguientes son los perfiles que interactúan en este recorrido.

| Grupo de usuarios | Descripción | Función en este recorrido |
|---|---|---|
| Desarrollador (público destinatario) | Tiene experiencia en el desarrollo de aplicaciones sin encabezado que consumen contenido de diferentes fuentes | Público destinatario de este recorrido |
| Autor de contenido | Crea y gestiona contenido que se suministra sin encabezado | Los autores de contenido crean contenido que el desarrollador entrega sin encabezado. |
| Administrador | Gestiona la configuración base de AEM | El desarrollador trabaja con el administrador para realizar los cambios de configuración necesarios para el desarrollo. |
| Arquitecto de contenido | Analiza los requisitos de los datos que deben entregarse sin encabezado y define la estructura de estos datos | Los desarrolladores trabajan con el arquitecto de contenido para comprender la estructura de los datos y los requisitos para ofrecerlos sin encabezado. |

## Recorrido para los desarrolladores de contenido sin encabezado {#the-journey}

Trataremos muchos temas en este recorrido, que le proporcionarán los conocimientos básicos del concepto de ausencia de encabezado en AEM.

Si bien puede ir directamente a una parte específica del recorrido, muchos conceptos se basan en los que se indican en los artículos anteriores. Adobe le recomienda que comience por el principio y avance secuencialmente.

| # | Artículo | Descripción |
|---|---|---|
| 0 | Recorrido para desarrolladores de AEM sin encabezado | Este documento |
| 1 | [Obtenga información acerca del desarrollo sin encabezado de CMS](learn-about.md) | Obtenga información sobre la tecnología sin encabezado y cuándo utilizarla. |
| 2 | [Introducción a AEM Headless as a Cloud Service](getting-started.md) | Aprenda sobre los requisitos previos de AEM sin encabezado |
| 3 | [Ruta hacia la primera experiencia al usar AEM sin encabezado](path-to-first-experience.md) | Configurar su entorno de desarrollo y aprender a integrar una aplicación sencilla con AEM sin encabezado |
| 4 | [Cómo modelar el contenido](model-your-content.md) | Aprenda a modelar la estructura de contenido. |
| 5 | [Cómo acceder al contenido a través de las API de entrega de AEM](access-your-content.md) | Aprenda a utilizar las consultas de GraphQL para acceder al contenido de los fragmentos de contenido. |
| 6 | [Actualización del contenido mediante las API de AEM Assets](update-your-content.md) | Descubra cómo utilizar la API de REST para acceder y actualizar el contenido de los fragmentos de contenido. |
| 7 | [Cómo ponerlo todo junto: su aplicación y su contenido en AEM sin encabezado](put-it-all-together.md) | Aprenda a gestionar su proyecto AEM y prepararlo para su lanzamiento con el SDK de AEM sin encabezado. |
| 8 | [Publicación de la aplicación sin encabezado](go-live.md) | Descubra cómo implementar la aplicación en directo, conseguir el código local en Git y trasladarlo a Cloud Manager Git para la canalización CI/CD. |
| 9 | [Opcional: cómo crear aplicaciones de una sola página (SPA) con AEM](create-spa.md) | Explore cómo combinar entregas completas y sin encabezado, y aprenda a crear SPA editables con el marco de trabajo del editor de SPA de AEM. |

{style="table-layout:auto"}

## Siguientes pasos {#what-is-next}

Empiece consultando el siguiente artículo: [Obtenga información sobre el desarrollo de CMS sin encabezado](learn-about.md).

## Recursos adicionales {#additional-resources}

Los recorridos de documentación muestran cómo AEM resuelve un problema de la empresa al proporcionar una narrativa que le guía a través de los procesos y las funciones relacionados. Un recorrido ilustra cómo varias funciones trabajan juntas para satisfacer una sola necesidad empresarial.

Si prefiere aprender con la práctica y tiene conocimientos actuales de AEM, siga nuestros tutoriales prácticos organizados por API y framework, que exploran la creación y el uso de aplicaciones creadas en AEM Headless. Vea [Tutoriales para Headless en AEM](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/overview.html?lang=es).

Consulte estos recorridos adicionales para obtener más información sobre cómo las potentes funciones de AEM trabajan juntas.

* El [Portal para desarrolladores de AEM](https://experienceleague.adobe.com/landing/experience-manager/headless/developer.html?lang=es)
* [Recorrido de traducción de AEM sin encabezado](/help/journey-headless/translation/overview.md). Este recorrido de documentación te ofrece una amplia comprensión de la tecnología sin encabezado, cómo AEM presenta el contenido sin encabezado y cómo puedes traducirlo.
* [Recorrido de creación sin encabezado](/help/journey-headless/author/overview.md). Empiece aquí para obtener un recorrido guiado a través de las potentes y flexibles funciones sin encabezado de AEM, sus capacidades y cómo modelar su contenido en su primer proyecto sin encabezado.
* [Recorrido de arquitectos Headless](/help/journey-headless/architect/overview.md): empiece aquí para ver una introducción a las potentes y flexibles funciones headless de Adobe Experience Manager as a Cloud Service y cómo diseñar contenido para su proyecto.
* [Documentación técnica de AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service.html?lang=es): si ya tiene una comprensión firme sobre las tecnologías AEM y sin encabezado, consulte directamente nuestros documentos técnicos detallados.
   * [Introducción a AEM como CMS sin encabezado](/help/headless/introduction.md)
