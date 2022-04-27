---
title: recorrido de traducción AEM sin encabezado
description: Comience aquí para obtener un recorrido guiado a través de la traducción de su contenido sin encabezado utilizando AEM poderosas herramientas de traducción.
exl-id: b677f691-5257-43c3-a4b9-c34932577b31
source-git-commit: ad47148237fe8a8b7c0b4fc4eb293f1155dae560
workflow-type: tm+mt
source-wordcount: '1029'
ht-degree: 11%

---

# recorrido de traducción AEM sin encabezado {#aem-headless-translation-journey}

Comience aquí para obtener un recorrido guiado a través de la traducción de su contenido sin encabezado utilizando AEM poderosas herramientas de traducción.

## Introducción {#introduction}

La implementación sin objetivos es cada vez más importante para ofrecer experiencias a su audiencia, independientemente del canal, la región o la configuración regional.

La implementación sin encabezado renuncia a la administración de páginas y componentes, como es tradicional en las soluciones de pila completas, y se centra en la creación de fragmentos de contenido neutros para el canal y reutilizables y su envío por canales cruzados. Mediante AEM potentes herramientas de traducción, estos fragmentos reutilizables se pueden traducir fácilmente y enviar a su audiencia dondequiera que se encuentren.

Esta guía le guía por los temas de traducción sin encabezado más importantes, de modo que al completarse:

* Obtenga información general sobre qué es la entrega de contenido sin encabezado.
* Tener un entendimiento básico AEM características sin encabezado.
* Comprenda AEM funciones de traducción y cómo se relacionan con contenido sin encabezado.
* Tener la capacidad de empezar a traducir su propio contenido sin encabezado.

El objetivo es darles una amplia comprensión de la tecnología sin objetivos, cómo AEM el contenido sin objetivos y cómo traducirlo. Si no está familiarizado con ninguno de estos temas, este es su lugar ideal para empezar.

Si ya está familiarizado con la traducción, la traducción y el AEM, puede que ya tenga el conocimiento fundacional de este recorrido. Considere la posibilidad de consultar nuestra documentación técnica vinculada en el [a continuación, la sección de recursos adicionales.](#additional-resources)

## Recorridos de documentación de AEM {#documentation-journeys}

[Un recorrido de documentación](/help/journey-documentation/documentation-journeys.md) une muchos temas y características diferentes y tal vez complicados. Proporciona una narrativa que ayuda al lector (que puede ser nuevo en AEM) a entender y resolver un problema empresarial de principio a fin, mientras asume un conocimiento previo mínimo de AEM.

Los recorridos de documentación están diseñados en torno a los principios de las prácticas recomendadas, basados en las últimas investigaciones de Adobe, la experiencia de implementación comprobada de los consultores de Adobe y los comentarios sobre los proyectos de los clientes.

Si desea saber cómo el Adobe recomienda resolver casos empresariales sin objetivos con AEM, [recorridos sin AEM](/help/journey-documentation/documentation-journeys.md) son el punto de inicio.

## Audiencia {#audience}

Este recorrido está diseñado para el especialista en traducción, a menudo denominado administrador de proyectos de traducción o TPM. Este recorrido establece los requisitos, pasos y enfoques para traducir contenido sin encabezado en AEM. El recorrido puede definir personalidades adicionales con las que debe interactuar el especialista en traducción, pero el punto de vista del recorrido es el del especialista en traducción.

Este recorrido supone que el lector tiene experiencia traduciendo contenido en un sistema CMS grande, pero no asume ningún conocimiento de tecnología o AEM sin periféricos.

Los siguientes son los perfiles que interactúan en este recorrido.

| Grupo de usuarios | Descripción | Función en el recorrido |
|---|---|---|
| Especialista en traducción | Define qué contenido debe traducirse y gestiona esos flujos de trabajo | Audiencia de este recorrido |
| Autor de contenido | Crea y administra el contenido que se entrega sin problemas | Los autores de contenido crean contenido que el especialista en traducción debe traducir. |
| Administrador | Gestiona la configuración y configuración base de AEM | El especialista en traducción trabaja con el administrador para realizar los cambios de configuración necesarios para la traducción, como instalar un conector de traducción. |
| Arquitecto de contenido | Analiza los requisitos de los datos que deben entregarse sin interrupciones y define la estructura de estos datos | Los especialistas en traducción trabajan con el arquitecto de contenido para definir la organización del contenido y así poder traducirlo fácilmente. |

Por supuesto, la información de este recorrido puede ser útil para todas las personas, pero parte de la información puede ser superflua para ciertas funciones. Manténgase atento a [recorridos futuros que cubran funciones adicionales.](/help/journey-documentation/documentation-journeys.md#journeys)

## El Recorrido de traducción sin encabezado {#the-journey}

Explorará muchos temas en este recorrido. Los siguientes artículos le proporcionan conocimientos básicos sobre la traducción de contenido sin encabezado en AEM y le permiten acceder a documentación técnica detallada.

Aunque puede ir directamente a una parte concreta del recorrido, muchos conceptos se basan en los de artículos anteriores. Por lo tanto, si es nuevo en una traducción sin encabezado en AEM, le recomendamos que comience por el principio y avance secuencialmente.

| # | Artículo | Descripción |
|---|---|---|
| 0 | recorrido de traducción AEM sin encabezado | Este documento |
| 1 | [Obtenga información sobre el contenido sin encabezado y cómo traducirlo en AEM](learn-about.md) | Aprenda conceptos sin objetivos, cómo se asignan a AEM, y la teoría de AEM traducción. |
| 2 | [Introducción a la traducción sin encabezado AEM](getting-started.md) | Conozca cómo organizar su contenido sin encabezado y cómo funcionan AEM herramientas de traducción. |
| 3 | [Configuración del conector de traducción](configure-connector.md) | Aprenda a conectar AEM a un servicio de traducción. |
| 4 | [Traducir contenido](translate-content.md) | Utilice el conector de traducción y las reglas para traducir el contenido sin encabezado. |
| 5 | [Publicar contenido traducido](publish-content.md) | Obtenga información sobre cómo publicar el contenido traducido y actualizar la traducción cuando se actualiza el contenido subyacente. |

## Siguientes pasos {#what-is-next}

Ya está listo para empezar con su recorrido de traducción sin encabezado de Adobe. Le animamos a que continúe con la siguiente parte del recorrido y lea el artículo [Obtenga información sobre el contenido sin encabezado y cómo traducirlo en AEM](learn-about.md)

## Recursos adicionales {#additional-resources}

Los recorridos de documentación muestran cómo AEM resuelve un problema comercial al proporcionar una narrativa que lo guía a través de procesos y funciones complejos e interrelacionados. Un recorrido ilustra cómo varias funciones trabajan juntas para satisfacer una sola necesidad empresarial.

Como estos recorridos están diseñados para mantenerse por su cuenta. Sin embargo, varios de ellos pueden relacionarse entre sí. Consulte estos recorridos adicionales para obtener más información sobre cómo funcionan juntas AEM potentes funciones.

* [Recorrido de creación sin encabezado](/help/journey-headless/author/overview.md) - Empiece aquí para obtener un recorrido guiado a través de las potentes y flexibles funciones de AEM, sus capacidades y cómo modelar su contenido en su primer proyecto sin objetivos.
* [Recorrido de arquitectos sin encabezado](/help/journey-headless/architect/overview.md) - Empiece aquí para ver una introducción a las potentes y flexibles funciones de Adobe Experience Manager as a Cloud Service y a cómo modelar el contenido de su proyecto.
* [recorrido para desarrolladores AEM sin encabezado](/help/journey-headless/developer/overview.md) - Empiece aquí para obtener un recorrido guiado a través de las potentes y flexibles funciones de AEM, sus capacidades y cómo aprovecharlas en su primer proyecto de desarrollo.
* [AEM documentación técnica as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service.html?lang=es) - Si ya tiene una comprensión firme de las tecnologías AEM y sin objetivos, puede que desee consultar directamente nuestros documentos técnicos.
* [Tutoriales AEM sin encabezado](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/overview.html?lang=es) - Si prefiere aprender haciendo y está técnicamente inclinado, tome nuestros tutoriales prácticos organizados por API y framework, que exploran la creación y el uso de aplicaciones creadas sobre AEM sin encabezado.
