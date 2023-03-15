---
title: Recorrido para desarrolladores de CMS sin encabezado de AEM
description: Obtenga información sobre el desarrollo sin encabezado mediante Adobe Experience Manager (AEM) como un CMS sin encabezado. Aprender a utilizar funciones como modelos de contenido, fragmentos de contenido y una API de GraphQL para potenciar la entrega de contenido sin encabezado.
landing-page-description: Obtenga información sobre la entrega e implementación del contenido sin encabezado. Obtenga más información sobre el desarrollo de su estrategia dentro de su empresa.
exl-id: d14a1e30-dd04-49a8-8cda-27c80a4bb0f5
source-git-commit: d4edec4448fd1b044875271cdcef3c7ada56cfe5
workflow-type: tm+mt
source-wordcount: '1083'
ht-degree: 97%

---

# Recorrido para desarrolladores de CMS sin encabezado de AEM {#aem-headless-developer-journey}

Bienvenidos a la documentación para los desarrolladores que son nuevos en CMS de Adobe Experience Manager sin encabezado.

Obtenga información sobre las funciones potentes y flexibles sin encabezado, sus capacidades y cómo aprovecharlas en su primer proyecto de desarrollo sin encabezado. Este recorrido proporciona toda la información necesaria para desarrollar su primera aplicación sin encabezado.

>[!CONTEXTUALHELP]
>id="aemcloud_headless_developer_resources"
>title="AEM Recursos para desarrolladores sin objetivos y documentación avanzada"
>abstract="Todo lo que necesita para aprender sobre AEM CMS sin objetivos y construir y enviar mejores aplicaciones y experiencias más rápidas."
>additional-url="https://experienceleague.adobe.com/landing/experience-manager/headless/developer.html?lang=es" text="AEM Recursos para desarrolladores sin encabezado"

## Introducción {#introduction}

La implementación sin encabezado de AEM utiliza modelos de fragmentos de contenido y fragmentos de contenido para centrarse en la creación de fragmentos de contenido estructurados, de canal neutro y reutilizables, así como su entrega en varios canales. Para lograrlo, renuncia a la administración de páginas y componentes, como es habitual en las soluciones de pila completas. Es un patrón de desarrollo moderno y dinámico para implementar experiencias digitales.

Esta guía le conduce por los temas de implementación sin encabezado en AEM, por lo que cuando haya terminado:

* Comprenderá perfectamente qué es la entrega de contenido sin encabezado y sus ventajas.
* Comprenderá las funciones sin encabezado de AEM y cómo trabajan conjuntamente para ofrecer una experiencia sin encabezado.
* Tendrá la posibilidad de realizar los primeros pasos en la implementación de su primer proyecto AEM sin encabezado.

>[!TIP]
>
> Si prefiere **aprender haciendo** y si tiene conocimientos de AEM, visite los tutoriales de AEM sin encabezado, organizados por la API y el marco de trabajo disponibles en la [sección Recursos adicionales](#additional-resources) al final de este documento.

## Audiencia {#audience}

Este recorrido está diseñado para el desarrollador y expone los requisitos, pasos y enfoque de un proyecto de AEM sin encabezado desde la perspectiva del desarrollador. El recorrido define las personas adicionales con las que el desarrollador debe interactuar para que un proyecto tenga éxito, pero el punto de vista del recorrido es el del desarrollador.

Los siguientes son los perfiles que interactúan en este recorrido.

| Grupo de usuarios | Descripción | Función en este recorrido |
|---|---|---|
| Desarrollador (audiencia de destino) | Tiene experiencia en el desarrollo de aplicaciones sin encabezado que consumen contenido de diferentes fuentes | Audiencia de destino de este recorrido |
| Autor de contenido | Crea y gestiona contenido que se suministra sin encabezado | Los autores de contenido crean contenido que el desarrollador entrega sin encabezado. |
| Administrador | Gestiona la configuración base de AEM | El desarrollador trabaja con el administrador para realizar los cambios de configuración necesarios para el desarrollo. |
| Arquitecto de contenido | Analiza los requisitos de los datos que deben entregarse sin encabezado y define la estructura de estos datos | Los desarrolladores trabajan con el arquitecto de contenido para comprender la estructura de los datos y los requisitos para ofrecerlos sin encabezado. |

## Recorrido para los desarrolladores de contenido sin encabezado {#the-journey}

Trataremos muchos temas en este recorrido, que le proporcionarán los conocimientos básicos del concepto de ausencia de encabezado en AEM.

Si bien puede ir directamente a una parte específica del recorrido, muchos conceptos se basan en los que se indican en los artículos anteriores. Le recomendamos que comience por el principio y avance secuencialmente.

| # | Artículo | Descripción |
|---|---|---|
| 0 | Recorrido para desarrolladores de AEM sin encabezado | Este documento |
| 1 | [Obtenga información acerca del desarrollo sin encabezado de CMS](learn-about.md) | Obtenga información sobre la tecnología sin encabezado y cuándo utilizarla. |
| 2 | [Introducción a AEM Headless as a Cloud Service](getting-started.md) | Aprenda sobre los requisitos previos de AEM sin encabezado |
| 3 | [Ruta hacia la primera experiencia al usar AEM sin encabezado](path-to-first-experience.md) | Configurar su entorno de desarrollo y aprender a integrar una aplicación sencilla con AEM sin encabezado |
| 4 | [Cómo modelar el contenido](model-your-content.md) | Aprenda a modelar la estructura de contenido. |
| 5 | [Cómo acceder al contenido a través de las API de entrega de AEM](access-your-content.md) | Aprenda a utilizar las consultas de GraphQL para acceder al contenido de los fragmentos de contenido. |
| 6 | [Actualización del contenido mediante las API de AEM Asset](update-your-content.md) | Descubra cómo utilizar la API de REST para acceder y actualizar el contenido de los fragmentos de contenido. |
| 7 | [Cómo ponerlo todo junto: su aplicación y su contenido en AEM sin encabezado](put-it-all-together.md) | Aprenda a gestionar su proyecto AEM y prepararlo para su lanzamiento con el SDK de AEM sin encabezado. |
| 8 | [Publicación de la aplicación sin encabezado](go-live.md) | Descubra cómo implementar la aplicación en directo, conseguir el código local en Git y trasladarlo a Cloud Manager Git para la canalización CI/CD. |
| 9 | [Opcional: cómo crear aplicaciones de una sola página (SPA) con AEM](create-spa.md) | Explore cómo combinar entregas completas y sin encabezado, y aprenda a crear SPA editables con el marco de trabajo del editor de SPA de AEM. |

{style="table-layout:auto"}

## Siguientes pasos {#what-is-next}

Empiece consultando el siguiente artículo: [Obtenga información sobre el desarrollo de CMS sin encabezado](learn-about.md).

### Elija su propia aventura {#choose-your-path}

¿Prefiere aprender a su ritmo? Consulte estas opciones:

* Si prefiere seguir **obteniendo información sobre conceptos sin encabezado y tecnologías sin encabezado de AEM**, debe continuar con su recorrido de AEM sin encabezado como se recomienda en la próxima revisión del documento [Modelar el contenido como modelos de contenido de AEM](model-your-content.md), donde aprenderá a modelar la estructura de contenido en AEM.
* Si prefiere **aprender de forma práctica**, puede ir al [Tutorial práctico de introducción a AEM sin encabezado](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/multi-step/overview.html?lang=es), donde pasará directamente al desarrollo de AEM sin encabezado implementando un proyecto simple para exponer contenido sin encabezado de AEM.

## Recursos adicionales {#additional-resources}

Los recorridos de documentación muestran cómo AEM resuelve un problema de la empresa al proporcionar una narrativa que le guía a través de los procesos y las funciones relacionados. Un recorrido ilustra cómo varias funciones trabajan juntas para satisfacer una sola necesidad empresarial.

Consulte estos recorridos adicionales para obtener más información sobre cómo las potentes funciones de AEM trabajan juntas.

* [Tutoriales de AEM sin encabezado](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/overview.html?lang=es): si prefiere aprender de forma práctica y tiene conocimientos sobre AEM, siga nuestros tutoriales prácticos organizados por API y marco de trabajo y explore la creación y el uso de aplicaciones creadas en AEM sin encabezado.
* [Recorrido de traducción de AEM sin encabezado](/help/journey-headless/translation/overview.md): este recorrido de documentación le ofrece un amplio conocimiento sobre la tecnología sin encabezado, cómo proporciona AEM contenido sin encabezado y cómo puede traducirlo.
* [Recorrido de creación sin encabezado](/help/journey-headless/author/overview.md). Empiece aquí para obtener un recorrido guiado a través de las potentes y flexibles funciones sin encabezado de AEM, sus capacidades y cómo modelar su contenido en su primer proyecto sin encabezado.
* [Recorrido de arquitectos Headless](/help/journey-headless/architect/overview.md): empiece aquí para ver una introducción a las potentes y flexibles funciones headless de Adobe Experience Manager as a Cloud Service y cómo diseñar contenido para su proyecto.
* [Documentación técnica de AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service.html?lang=es): si ya tiene una comprensión firme sobre las tecnologías AEM y sin encabezado, consulte directamente nuestros documentos técnicos detallados.
