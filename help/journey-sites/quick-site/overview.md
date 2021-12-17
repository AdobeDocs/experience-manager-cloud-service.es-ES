---
title: AEM Recorrido de creación rápida de sitios
description: Comience aquí para obtener un recorrido guiado a través de la herramienta de creación rápida de sitios AEM fácil de usar, para optimizar el desarrollo front-end de su sitio AEM y personalizar rápidamente su sitio sin AEM conocimiento del servidor.
source-git-commit: 5e1a89743c5ac36635a139ada690849507813c30
workflow-type: tm+mt
source-wordcount: '1030'
ht-degree: 1%

---


# AEM Recorrido de creación rápida de sitios {#quick-site-creation-journey}

Comience aquí para obtener un recorrido guiado a través de la herramienta de creación rápida de sitios AEM fácil de usar, para optimizar el desarrollo front-end de su sitio AEM y personalizar rápidamente su sitio sin AEM conocimiento del servidor.

## Introducción {#introduction}

AEM Sites is a powerful tool set for creating and managing digital experiences. Content authors can easily create digital experiences using the sites editor and organize the content using the sites console, all while being able to see the content live as it will be delivered by AEM to your audiences across channels.

The AEM Quick Site Creation tool allows non-developers to quickly create a new site from scratch by using site templates. Once created, the Quick Site Creation tool also enables fast customization of the theme and styling of the AEM site (JavaScript, CSS, and static resources). Esto permite que el desarrollador del front-end, que no necesita ningún conocimiento de AEM, trabaje de forma independiente y paralela a los creadores de contenido. El administrador de AEM simplemente descarga el tema del sitio y lo proporciona al desarrollador de front-end que lo personaliza con sus herramientas favoritas y luego confirma los cambios en el repositorio de código de AEM, que luego se implementa.

By eliminating any developer knowledge for site creation, eliminating AEM knowledge requirements for front end development, and allowing theme development to proceed in parallel with content creation, the AEM Quick Site Creation tool greatly accelerates your site&#39;s time-to-value and increases your site customization and deployment agility.

## Información general del vídeo {#video-overview}

Para obtener una descripción general rápida de esta función en acción, [puede ver esta introducción de cinco minutos.](https://www.youtube.com/watch?v=NQeQ1jZ7ZBw)

This documentation journey will take you through all the features in the video  step-by-step and in detail so you understand the workflow and can recreate the process in your own environment.

## recorridos de documentación de AEM {#documentation-journeys}

[A Documentation Journey](/help/journey-documentation/documentation-journeys.md) ties together many different and perhaps complicated topics and features by providing a narrative that helps the reader, who can be new to AEM, understand and solve a business problem from beginning to end, while assuming minimal prior topic or AEM knowledge.

Los Recorridos de documentación están diseñados en torno a los principios de las mejores prácticas, basados en las últimas investigaciones del Adobe, la experiencia de implementación comprobada de los consultores de Adobe y los comentarios de los proyectos de los clientes.

Si desea saber cómo recomienda Adobe resolver los casos comerciales del sitio con AEM, los Recorridos de AEM Sites son el punto de inicio.

## Audience {#audience}

This journey lays out the requirements, steps, and approach to customize AEM Sites themes. Su audiencia principal es el desarrollador de front-end, que no necesita saber AEM. However, in order to illustrate the entire process, the journey involves administrators, who are assumed to have basic AEM Sites and Cloud Manager knowledge. In practice, multiple people can serve multiple roles and this journey supports perspectives from both admins and front-end developers.

| Grupo de usuarios | Descripción | Role in Journey |
|---|---|---|
| Front-End Developer | Customizes the site theme | Toma el tema proporcionado por el administrador de AEM y lo personaliza para que se pueda implementar en el sitio de AEM. |
| Content Author | Crea y administra el contenido que se entrega como sitios | Los autores de contenido crean contenido en AEM que se representa con el tema personalizado por el desarrollador de front-end. |
| Administrador de AEM | Crea un nuevo sitio AEM | El administrador de AEM crea un nuevo sitio basado en una plantilla y, a continuación, proporciona al desarrollador del front-end un tema que se debe personalizar. |
| Cloud Manager Administrator | Crea canalizaciones y concede acceso | El administrador de Cloud Manager crea la canalización de front-end y concede acceso al desarrollador de front-end para poder realizar personalizaciones en el repositorio de Git de AEM. |

## The AEM Quick Site Creation Journey {#the-journey}

Explorará muchos temas en este recorrido. Los siguientes artículos le proporcionan conocimientos básicos sobre la creación y personalización de sitios AEM mediante la herramienta de creación rápida de sitios y le permiten acceder a documentación técnica detallada.

|#|Article|Description|Responsible Role|
|---|---|---|--|
|0|AEM Quick Site Creation Journey|This document|AEM &amp; Cloud Manager Administrators|
|1|[Understand Cloud Manager and the Quick Site Creation Workflow](cloud-manager.md)|Learn about Cloud Manager and how it ties together the new Quick Site Creation process.|AEM Administrator|
|2|[Create site from template](create-site.md)|Learn how to quickly create a new AEM site using a site template.|AEM administrador| |3|[Configurar la canalización](pipeline-setup.md)|Cree una canalización front-end para administrar la personalización del tema del sitio.|Cloud Manager Administrator|
|4|[Grant access to the front-end developer](grant-access.md)|Onboard the front-end developers into Cloud Manager so they have access to your AEM site git repository and pipeline.|Cloud Manager Administrator|
|5|[Retrieve git repository access information](retrieve-access.md)|Learn how the front-end developer uses Cloud Manager to access git repository information.|Desarrollador front-end| |6|[Personalizar el tema del sitio](customize-theme.md)|Obtenga información sobre cómo se crea un tema de sitio, cómo personalizarlo y cómo probarlo con contenido AEM en directo.|Desarrollador front-end| |7|[Implementar el tema personalizado](deploy-theme.md)|Obtenga información sobre cómo implementar el tema del sitio mediante la canalización.|Desarrollador front-end|

## Siguientes pasos {#what-is-next}

You are now ready to get started on your Adobe Quick Site Creation journey.

* If you are an AEM or Cloud Manager administrator, or if you serve both front-end developer and administrator roles, or if you simply want to understand the end-to-end process in AEM, please start at the beginning of the journey with [Understand Cloud Manager](cloud-manager.md) as laid out below.
* If you are only responsible for front-end development and will interact with the AEM and Cloud Manager administrators, you can skip directly to [Retrieve git repository access information](retrieve-access.md) to get access to the AEM git repository and start customizing.
* If you already understand AEM Sites and Cloud Manager work together and want to start directly with configuration, you can [skip directly to creating a new site from a template.](create-site.md)

## Recursos adicionales {#additional-resources}

Consulte estos recursos adicionales para obtener más información sobre cómo funcionan juntas AEM potentes funciones.

* [AEM documentación técnica as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service.html?lang=es) - Si ya tiene una comprensión firme de AEM, puede que desee consultar directamente los documentos técnicos detallados.
* [Documentación de administración del sitio](/help/sites-cloud/administering/site-creation/create-site.md) - Consulte los documentos técnicos sobre la creación de sitios para obtener más información sobre las funciones de la herramienta de creación rápida de sitios.
