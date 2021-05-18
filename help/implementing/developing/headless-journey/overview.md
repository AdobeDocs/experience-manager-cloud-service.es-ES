---
title: recorrido para desarrolladores AEM sin encabezado
description: Comience aquí para obtener un recorrido guiado a través de las potentes y flexibles funciones de AEM, sus capacidades y cómo aprovecharlas en su primer proyecto de desarrollo.
hide: true
hidefromtoc: true
index: false
exl-id: 4524c92a-8f19-497a-b4f2-c3e23f555d37
source-git-commit: 83ed6295d2b29581025f5410236f2618ceb59012
workflow-type: tm+mt
source-wordcount: '782'
ht-degree: 2%

---

# AEM Recorrido para desarrolladores sin encabezado {#aem-headless-developer-journey}

>[!CAUTION]
>
>TRABAJO EN CURSO - La creación de este documento está en curso y no debe entenderse como completo o definitivo ni debe utilizarse con fines de producción.

Empiece aquí por un recorrido guiado a través de las potentes y flexibles funciones de AEM, sus capacidades y cómo aprovecharlas en su primer proyecto de desarrollo sin objetivos.

## Introducción {#introduction}

La implementación sin objetivos es cada vez más importante para ofrecer experiencias a su audiencia, independientemente del canal y dónde se encuentren.

La implementación sin encabezado renuncia a la administración de páginas y componentes, como es tradicional en las soluciones de pila completas, y se centra en la creación de fragmentos de contenido neutros para el canal y reutilizables y su envío por canales cruzados. Es un patrón de desarrollo moderno y dinámico para implementar experiencias web.

Esta guía le guiará por los temas más importantes para que al completarlo:

* Comprenda perfectamente qué es la entrega de contenido sin objetivos y sus ventajas.
* Comprender AEM funciones sin objetivos y cómo trabajan juntos para ofrecer una experiencia sin objetivos.
* Tenga la capacidad de realizar los primeros pasos en la implementación de su primer proyecto AEM sin encabezado.

## Audience {#audience}

Este recorrido está diseñado para el desarrollador, que expone los requisitos, pasos y enfoque de un proyecto sin encabezado AEM desde la perspectiva del desarrollador. El recorrido definirá las personas adicionales con las que el desarrollador debe interactuar para que un proyecto tenga éxito, pero el punto de vista del recorrido es el del desarrollador.

La información de este recorrido puede ser útil para otras personas, pero cierta información será superflua para ciertas funciones. Manténgase atento a los próximos recorridos que cubran funciones adicionales.

## El Recorrido para desarrolladores sin encabezado {#the-journey}

Explorará muchos temas en este recorrido. Los siguientes artículos le proporcionan conocimientos básicos de AEM y le permiten acceder a documentación técnica detallada.

Aunque puede ir directamente a una parte concreta del recorrido, muchos conceptos se basan en los de artículos anteriores. Por lo tanto, si es nuevo en sin encabezado en AEM, le recomendamos que comience al principio y avance secuencialmente.

| # | Artículo | Descripción |
|---|---|---|
| 0 | recorrido para desarrolladores AEM sin encabezado | Este documento |
| 1 | [Obtenga información sobre el desarrollo sin encabezado de CMS](learn-about.md) | Obtenga información sobre la tecnología sin encabezado y cuándo utilizarla. |
| 2 | [Introducción a AEM Headless como Cloud Service](getting-started.md) | Obtenga información sobre los requisitos previos sin encabezado de AEM |
| 3 | [Ruta a la primera experiencia usando AEM sin encabezado](path-to-first-experience.md) | Configure su entorno de desarrollo y aprenda a integrar una aplicación sencilla con AEM sin encabezado |
| 4 | [Cómo modelar el contenido](model-your-content.md) | Aprenda a modelar la estructura de contenido. A continuación, observe esa estructura para Adobe Experience Manager (AEM) mediante los modelos de fragmentos de contenido y los fragmentos de contenido, para reutilizarla en todos los canales. |
| 5 | [Cómo acceder al contenido a través de las API de envío de AEM](access-your-content.md) | Aprenda a utilizar las consultas de GraphQL para acceder al contenido de los fragmentos de contenido. |
| 6 | [Actualización del contenido mediante las API de recursos de AEM](update-your-content.md) | Aprenda a utilizar la API de REST para acceder y actualizar el contenido de los fragmentos de contenido. |
| 7 | [Cómo ponerlo todo juntos: su aplicación y su contenido en AEM sin encabezado](put-it-all-together.md) | Aprenda a tomar su proyecto de AEM, incluidos los fragmentos de contenido, las llamadas de GraphQL, las llamadas a la API de REST y la aplicación, y a prepararlo para su lanzamiento. |
| 8 | [Activación de la aplicación sin cabeza](go-live.md) | Obtenga información sobre cómo implementar la aplicación en directo y tome el código local en Git y muévalo a Cloud Manager Git para la canalización CI/CD. |
| 9 | [Publicar lanzamiento](post-launch.md) | Aprenda a mantener su experiencia sin encabezado. |
| 10 | [Opcional: Cómo crear aplicaciones de una sola página (SPA) con AEM](create-spa.md) | Una vez que haya comprendido AEM funciones sin encabezado, explore cómo combinar envíos con encabezado y sin encabezado y aprenda a crear SPA editables con AEM marco SPA Editor. |

## Siguientes {#what-is-next}

Ahora está listo para empezar con su recorrido sin encabezado de Adobe. Le recomendamos que continúe con la siguiente parte del recorrido y lea el artículo [Más información sobre el desarrollo sin encabezado de CMS.](learn-about.md)

### Elija su propia aventura {#choose-your-path}

Sin embargo, Adobe quiere que tenga éxito a medida que comienza con el proyecto sin encabezado de AEM, independientemente de su estilo de aprendizaje. Así que por favor consideren estas dos opciones.

* Si prefiere continuar **aprendiendo sobre conceptos sin encabezado y AEM tecnologías sin encabezado**, debe continuar con el recorrido sin encabezado AEM recomendado al revisar el documento [Cómo modelar su contenido como modelos de contenido AEM](model-your-content.md), donde aprenderá a modelar su estructura de contenido en AEM.
* Si prefiere **aprender haciendo**, puede ir al [Tutorial práctico Introducción a AEM sin encabezado](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/multi-step/overview.html), donde saltará directamente a AEM desarrollo sin encabezado implementando un proyecto simple para exponer AEM contenido sin encabezado.
