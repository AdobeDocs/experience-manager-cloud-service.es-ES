---
title: recorrido para desarrolladores AEM sin encabezado
description: 'Comience aquí para obtener un recorrido guiado a través de Adobe Experience Manager (AEM) as a Cloud Service cuando se esté utilizando como un sistema de gestión de contenido sin encabezado (CMS). Learn about the powerful and flexible headless features, their capabilities, and how to leverage them on your first headless development project. Este recorrido le proporciona toda la información necesaria para desarrollar su primera aplicación sin periféricos. '
landing-page-description: 'Obtenga información sobre la entrega e implementación de contenido sin encabezado. Learn more about developing your strategy within your business. '
exl-id: d14a1e30-dd04-49a8-8cda-27c80a4bb0f5
source-git-commit: 2ec6b29800867462bbc2e88048c583d4e5eefa57
workflow-type: tm+mt
source-wordcount: '1301'
ht-degree: 12%

---

# AEM Headless Developer Journey {#aem-headless-developer-journey}

Comience aquí para obtener un recorrido guiado a través de [!DNL Adobe Experience Manager as a Cloud Service] (AEM) cuando se utiliza como sistema de gestión de contenido sin encabezado (CMS). Obtenga información sobre las funciones potentes y flexibles sin encabezado, sus capacidades y cómo aprovecharlas en su primer proyecto de desarrollo sin objetivos. This journey provides you with all the information you need to develop your first headless application.

## Introducción {#introduction}

La implementación sin encabezado de AEM utiliza modelos de fragmentos de contenido y fragmentos de contenido para centrarse en la creación de fragmentos de contenido estructurados, neutros en el canal y reutilizables, así como su envío por canales cruzados. Para lograrlo, renuncia a la administración de páginas y componentes, como es tradicional en las soluciones de pila completas. Es un patrón de desarrollo moderno y dinámico para implementar experiencias digitales.

Esta guía le guiará por los temas de implementación más importantes de AEM para que, al completarse:

* Comprenda perfectamente qué es la entrega de contenido sin objetivos y sus ventajas.
* Comprender AEM funciones sin objetivos y cómo trabajan juntos para ofrecer una experiencia sin objetivos.
* Tenga la capacidad de realizar los primeros pasos en la implementación de su primer proyecto AEM sin encabezado.

## Recorridos de documentación de AEM {#documentation-journeys}

[Un recorrido de documentación](/help/journey-documentation/documentation-journeys.md) une muchos temas y características diferentes y tal vez complicados. Proporciona una narrativa que ayuda al lector (que puede ser nuevo en AEM) a entender y resolver un problema empresarial de principio a fin, mientras asume un conocimiento previo mínimo de AEM.

Los recorridos de documentación están diseñados en torno a los principios de las prácticas recomendadas, basados en las últimas investigaciones de Adobe, la experiencia de implementación comprobada de los consultores de Adobe y los comentarios sobre los proyectos de los clientes.

Si desea saber cómo el Adobe recomienda resolver casos empresariales sin objetivos con AEM, [recorridos sin AEM](/help/journey-documentation/documentation-journeys.md) son el punto de inicio.

>[!TIP]
>
> Si prefiere **aprenda haciendo** y están técnicamente inclinados, visite los tutoriales AEM sin encabezado, que están organizados por API y framework y están disponibles en la [Sección Recursos adicionales](#additional-resources) al final de este documento.

## Audiencia {#audience}

Este recorrido está diseñado para el desarrollador, que expone los requisitos, pasos y enfoque de un proyecto sin encabezado AEM desde la perspectiva del desarrollador. El recorrido define las personas adicionales con las que el desarrollador debe interactuar para que un proyecto tenga éxito, pero el punto de vista del recorrido es el del desarrollador.

Los siguientes son los perfiles que interactúan en este recorrido.

| Grupo de usuarios | Descripción | Role in This Journey |
|---|---|---|
| Desarrollador (audiencia de destino) | Has experience developing headless applications which consume content from different sources | Target audience of this journey |
| Autor de contenido | Crea y gestiona el contenido que se entrega sin problemas | Los autores de contenido crean contenido que el desarrollador entrega sin problemas. |
| Administrador | Gestiona la configuración y configuración base de AEM | El desarrollador trabaja con el administrador para realizar los cambios de configuración necesarios para el desarrollo. |
| Arquitecto de contenido | Analiza los requisitos de los datos que deben entregarse sin interrupciones y define la estructura de estos datos | Los desarrolladores trabajan con el arquitecto de contenido para comprender la estructura de los datos y los requisitos para ofrecerlos sin problemas. |

Por supuesto, la información de este recorrido puede ser útil para todas las personas, pero parte de la información puede ser superflua para ciertas funciones. Manténgase atento a [recorridos futuros que cubran funciones adicionales.](/help/journey-documentation/documentation-journeys.md#journeys)

## El Recorrido para desarrolladores sin objetivos {#the-journey}

Explorará muchos temas en este recorrido. Los siguientes artículos le proporcionan conocimientos básicos de AEM y le permiten acceder a documentación técnica detallada.

Aunque puede ir directamente a una parte concreta del recorrido, muchos conceptos se basan en los de artículos anteriores. Por lo tanto, si es nuevo en sin encabezado en AEM, le recomendamos que comience al principio y avance secuencialmente.

| # | Artículo | Descripción |
|---|---|---|
| 0 | recorrido para desarrolladores AEM sin encabezado | Este documento |
| 1 | [Obtenga información acerca del desarrollo sin encabezado de CMS](learn-about.md) | Obtenga información sobre la tecnología sin encabezado y cuándo utilizarla. |
| 2 | [Introducción a AEM Headless as a Cloud Service](getting-started.md) | Obtenga información sobre los requisitos previos sin encabezado de AEM |
| 3 | [Ruta hacia la primera experiencia al usar AEM Headless](path-to-first-experience.md) | Configure su entorno de desarrollo y aprenda a integrar una aplicación sencilla con AEM sin encabezado |
| 4 | [Cómo modelar el contenido](model-your-content.md) | Aprenda a modelar la estructura de contenido. A continuación, observe esa estructura para Adobe Experience Manager (AEM) mediante los modelos de fragmentos de contenido y los fragmentos de contenido, para reutilizarla en todos los canales. |
| 5 | [Cómo acceder al contenido a través de las API de entrega de AEM](access-your-content.md) | Learn how to use GraphQL queries to access your Content Fragments content. |
| 6 | [Actualización del contenido mediante las API de AEM Assets](update-your-content.md) | Learn how to use REST API to access and update your Content Fragments content. |
| 7 | [Cómo ponerlo todo juntos: su aplicación y su contenido en AEM sin encabezado](put-it-all-together.md) | Aprenda a tomar su proyecto AEM y prepararlo para su lanzamiento con el SDK sin encabezado de AEM. |
| 8 | [Publicación de la aplicación sin encabezado](go-live.md) | Obtenga información sobre cómo implementar la aplicación en directo y tome el código local en Git y muévalo a Cloud Manager Git para la canalización CI/CD. |
| 9 | [Opcional: Cómo crear aplicaciones de una sola página (SPA) con AEM](create-spa.md) | Una vez que haya comprendido AEM funciones sin encabezado, explore cómo combinar entregas con encabezado y sin encabezado y aprenda a crear SPA editables con AEM marco SPA Editor. |

## Siguientes pasos {#what-is-next}

Ahora está listo para empezar con su recorrido sin encabezado de Adobe. We encourage you to continue on to the next part of the journey and read the article [Learn about CMS Headless Development.](learn-about.md)

### Elija su propia aventura {#choose-your-path}

Sin embargo, Adobe quiere que tenga éxito a medida que comienza con el proyecto sin encabezado de AEM, independientemente de su estilo de aprendizaje. Así que por favor consideren estas dos opciones.

* Si prefiere continuar **obtenga información sobre conceptos sin encabezado y AEM tecnologías sin encabezado**, debe continuar con su recorrido sin AEM como se recomienda en la próxima revisión del documento [Modelo del contenido como modelos de contenido AEM](model-your-content.md) donde aprende a modelar la estructura de contenido en AEM.
* Si prefiere **aprenda haciendo**, puede ir al [Tutorial práctico Introducción a AEM sin encabezado](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/multi-step/overview.html?lang=es) donde saltará directamente al desarrollo sin encabezado de AEM implementando un proyecto simple para exponer AEM contenido sin encabezado.

## Recursos adicionales {#additional-resources}

Los recorridos de documentación muestran cómo AEM resuelve un problema comercial al proporcionar una narrativa que lo guía a través de procesos y funciones complejos e interrelacionados. Un recorrido ilustra cómo varias funciones trabajan juntas para satisfacer una sola necesidad empresarial.

Como estos recorridos están diseñados para mantenerse por su cuenta. Sin embargo, varios de ellos pueden relacionarse entre sí. Check out these additional journeys for more information on how AEM&#39;s powerful features work together.

* [Tutoriales AEM sin encabezado](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/overview.html?lang=es) - Si prefiere aprender haciendo y está técnicamente inclinado, tome nuestros tutoriales prácticos organizados por API y framework, que exploran la creación y el uso de aplicaciones creadas sobre AEM sin encabezado.
* [recorrido de traducción AEM sin encabezado](/help/journey-headless/translation/overview.md) - Este recorrido de documentación le ofrece una amplia comprensión de la tecnología sin objetivos, AEM sirve contenido sin objetivos y cómo puede traducirlo.
* [Recorrido de creación sin encabezado](/help/journey-headless/author/overview.md) - Empiece aquí para obtener un recorrido guiado a través de las potentes y flexibles funciones de AEM, sus capacidades y cómo modelar su contenido en su primer proyecto sin objetivos.
* [Recorrido de arquitectos sin encabezado](/help/journey-headless/architect/overview.md) - Empiece aquí para ver una introducción a las potentes y flexibles funciones de Adobe Experience Manager as a Cloud Service y a cómo modelar el contenido de su proyecto.
* [AEM documentación técnica as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service.html?lang=es) - Si ya tiene una comprensión firme de las tecnologías AEM y sin objetivos, puede que desee consultar directamente nuestros documentos técnicos.
