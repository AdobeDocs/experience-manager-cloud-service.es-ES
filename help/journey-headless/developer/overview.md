---
title: AEM Recorrido para desarrolladores de CMS sin encabezado
description: Obtenga información sobre el desarrollo sin objetivos mediante Adobe Experience Manager (AEM) as a Headless CMS. Aprenda a utilizar funciones como modelos de contenido, fragmentos de contenido y una API de GraphQL para potenciar la entrega de contenido sin encabezado.
landing-page-description: Obtenga información sobre la entrega e implementación de contenido sin encabezado. Obtenga más información sobre el desarrollo de su estrategia dentro de su empresa.
exl-id: d14a1e30-dd04-49a8-8cda-27c80a4bb0f5
source-git-commit: 64862456bfbffe1799a3f0b6ea3353f45e60c52f
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# AEM Recorrido para desarrolladores de CMS sin encabezado {#aem-headless-developer-journey}

Le damos la bienvenida a la documentación para los desarrolladores que son nuevos en Adobe Experience Manager CMS sin encabezado.

Obtenga información sobre las funciones potentes y flexibles sin encabezado, sus capacidades y cómo aprovecharlas en su primer proyecto de desarrollo sin objetivos. Este recorrido le proporciona toda la información necesaria para desarrollar su primera aplicación sin periféricos.

## Introducción {#introduction}

La implementación sin encabezado de AEM utiliza modelos de fragmentos de contenido y fragmentos de contenido para centrarse en la creación de fragmentos de contenido estructurados, neutros en el canal y reutilizables, así como su envío por canales cruzados. Para lograrlo, renuncia a la administración de páginas y componentes, como es tradicional en las soluciones de pila completas. Es un patrón de desarrollo moderno y dinámico para implementar experiencias digitales.

Esta guía le guía por temas de implementación sin encabezado en AEM, por lo que cuando haya terminado, lo hará:

* Comprenda perfectamente qué es la entrega de contenido sin objetivos y sus ventajas.
* Comprender AEM funciones sin objetivos y cómo trabajan juntos para ofrecer una experiencia sin objetivos.
* Tenga la capacidad de realizar los primeros pasos en la implementación de su primer proyecto AEM sin encabezado.

>[!TIP]
>
> Si prefiere **aprenda haciendo** y si tiene conocimientos de AEM, visite los tutoriales sin encabezado de AEM, que están organizados por API y framework y están disponibles en la [Sección Recursos adicionales](#additional-resources) al final de este documento.

## Audiencia {#audience}

Este recorrido está diseñado para el desarrollador, que expone los requisitos, pasos y enfoque de un proyecto sin encabezado AEM desde la perspectiva del desarrollador. El recorrido define las personas adicionales con las que el desarrollador debe interactuar para que un proyecto tenga éxito, pero el punto de vista del recorrido es el del desarrollador.

Los siguientes son los perfiles que interactúan en este recorrido.

| Grupo de usuarios | Descripción | Función en este Recorrido |
|---|---|---|
| Desarrollador (audiencia de destino) | Tiene experiencia en el desarrollo de aplicaciones sin periféricos que consumen contenido de diferentes fuentes | Destinatarios objetivo de este recorrido |
| Autor de contenido | Crea y gestiona el contenido que se entrega sin problemas | Los autores de contenido crean contenido que el desarrollador entrega sin problemas. |
| Administrador | Gestiona la configuración base de AEM | El desarrollador trabaja con el administrador para realizar los cambios de configuración necesarios para el desarrollo. |
| Arquitecto de contenido | Analiza los requisitos de los datos que deben entregarse sin interrupciones y define la estructura de estos datos | Los desarrolladores trabajan con el arquitecto de contenido para comprender la estructura de los datos y los requisitos para ofrecerlos sin problemas. |

## El Recorrido para desarrolladores sin objetivos {#the-journey}

Abarcaremos muchos temas en este recorrido, que le proporcionará el conocimiento fundacional de la ausencia de cabeza en AEM.

Aunque puede ir directamente a una parte concreta del recorrido, muchos conceptos se basan en los de artículos anteriores. Le recomendamos que comience al principio y avance secuencialmente.

| # | Artículo | Descripción |
|---|---|---|
| 0 | recorrido para desarrolladores AEM sin encabezado | Este documento |
| 1 | [Obtenga información acerca del desarrollo sin encabezado de CMS](learn-about.md) | Obtenga información sobre la tecnología sin encabezado y cuándo utilizarla. |
| 2 | [Introducción a AEM Headless as a Cloud Service](getting-started.md) | Obtenga información sobre los requisitos previos sin encabezado de AEM |
| 3 | [Ruta hacia la primera experiencia al usar AEM Headless](path-to-first-experience.md) | Configure su entorno de desarrollo y aprenda a integrar una aplicación sencilla con AEM sin encabezado |
| 4 | [Cómo modelar el contenido](model-your-content.md) | Aprenda a modelar la estructura de contenido. |
| 5 | [Cómo acceder al contenido a través de las API de entrega de AEM](access-your-content.md) | Aprenda a utilizar las consultas de GraphQL para acceder al contenido de los fragmentos de contenido. |
| 6 | [Actualización del contenido mediante las API de AEM Assets](update-your-content.md) | Aprenda a utilizar la API de REST para acceder y actualizar el contenido de los fragmentos de contenido. |
| 7 | [Cómo ponerlo todo juntos: su aplicación y su contenido en AEM sin encabezado](put-it-all-together.md) | Aprenda a tomar su proyecto AEM y prepararlo para su lanzamiento con el SDK sin encabezado de AEM. |
| 8 | [Publicación de la aplicación sin encabezado](go-live.md) | Obtenga información sobre cómo implementar la aplicación en vivo y tome el código local en Git y muévalo a Cloud Manager Git para la canalización CI/CD. |
| 9 | [Opcional: Cómo crear aplicaciones de una sola página (SPA) con AEM](create-spa.md) | Explore cómo combinar envíos completos y sin encabezado y aprenda a crear SPA editables con AEM marco SPA Editor. |

{style=&quot;table-layout:auto&quot;}

## Siguientes pasos {#what-is-next}

Comience por consultar el siguiente artículo: [Obtenga información sobre el desarrollo sin encabezado de CMS.](learn-about.md)

### Elija su propia aventura {#choose-your-path}

¿Prefieres aprender a tu propio ritmo? Consulte estas opciones:

* Si prefiere continuar **obtenga información sobre conceptos sin encabezado y AEM tecnologías sin encabezado**, debe continuar con su recorrido sin AEM como se recomienda en la próxima revisión del documento [Modelo del contenido como modelos de contenido AEM](model-your-content.md) donde aprende a modelar la estructura de contenido en AEM.
* Si prefiere **aprenda haciendo**, puede ir al [Tutorial práctico Introducción a AEM sin encabezado](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/multi-step/overview.html?lang=es) donde saltará directamente al desarrollo sin encabezado de AEM implementando un proyecto simple para exponer AEM contenido sin encabezado.

## Recursos adicionales {#additional-resources}

Los recorridos de documentación muestran cómo AEM resuelve un problema comercial al proporcionar una narrativa que le guía a través de los procesos y funciones relacionados. Un recorrido ilustra cómo varias funciones trabajan juntas para satisfacer una sola necesidad empresarial.

Consulte estos recorridos adicionales para obtener más información sobre cómo funcionan juntas AEM potentes funciones.

* [Tutoriales AEM sin encabezado](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/overview.html?lang=es) - Si prefiere aprender haciendo y tiene conocimientos existentes de AEM, tome nuestros tutoriales prácticos organizados por API y framework, que exploran la creación y el uso de aplicaciones creadas sobre AEM sin encabezado.
* [recorrido de traducción AEM sin encabezado](/help/journey-headless/translation/overview.md) - Este recorrido de documentación le ofrece una amplia comprensión de la tecnología sin objetivos, AEM sirve contenido sin objetivos y cómo puede traducirlo.
* [Recorrido de creación Headless](/help/journey-headless/author/overview.md): empiece aquí para obtener un recorrido guiado a través de las potentes y flexibles funciones headless de AEM, sus capacidades y cómo modelar su contenido en su primer proyecto headless.
* [Recorrido de arquitectos Headless](/help/journey-headless/architect/overview.md): empiece aquí para ver una introducción a las potentes y flexibles funciones headless de Adobe Experience Manager as a Cloud Service y cómo diseñar contenido para su proyecto.
* [AEM documentación técnica as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service.html?lang=es) - Si ya tiene una comprensión firme de AEM y tecnologías sin objetivos, consulte nuestros documentos técnicos.
