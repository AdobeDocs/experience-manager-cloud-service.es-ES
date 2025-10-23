---
title: Introducción al Recorrido de incorporación a AEM as a Cloud Service
description: Comience aquí para obtener una descripción general del recorrido guiado a través del proceso de incorporación para AEM as a Cloud Service.
exl-id: 892577db-05dc-49ff-bb2c-203efdb89c8c
recommendations: noDisplay
feature: Onboarding
role: Admin, User, Developer
source-git-commit: 858a9c4b61fd3a80a257313e48816b067ca77175
workflow-type: tm+mt
source-wordcount: '1362'
ht-degree: 93%

---


# Recorrido de la incorporación {#onboarding-journey}

¡Felicidades por elegir AEM as a Cloud Service! Este documento es el punto de partida para un recorrido guiado a través del proceso de incorporación. Tanto si va a implementar una aplicación nueva como si va a migrar una existente, este recorrido de incorporación configura los equipos. Esto garantiza que tengan acceso a AEM as a Cloud Service.

## Introducción {#introduction}

Adobe Experience Manager (AEM) proporciona flexibilidad tanto en la entrega de contenido como en los enfoques de creación, lo que permite a los equipos elegir el mejor modelo para sus necesidades.

Use [Edge Delivery Services](https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/edge-delivery/overview) para crear contenido de forma rápida e iterativa y con una alta velocidad, o use el servicio de publicación tradicional para un modelo de publicación empresarial sólido. Cualquier enfoque permite a las organizaciones ofrecer experiencias digitales excepcionales de la manera que mejor se adapte a sus necesidades. Para comenzar con Edge Delivery Services, explore la [Información general de Edge Delivery Services](https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/edge-delivery/overview) y para obtener más información sobre las opciones modernas de creación, consulte la [Guía de creación](https://www.aem.live/docs/authoring-guide).

La incorporación es el proceso durante el cual un administrador designado del sistema configura AEM as a Cloud Service para su organización. Esto incluye el aprovisionamiento inicial de recursos en la nube y la asignación de usuarios a funciones en función de sus responsabilidades laborales. Como resultado, cada miembro puede iniciar sesión y acceder a sus recursos de AEM as a Cloud Service.

![El recorrido de incorporación](/help/journey-onboarding/assets/onboarding-journey.png).

Esta guía le llevará por los temas más importantes de la incorporación para que, al completarla, tenga lo siguiente:

* Una comprensión total de los distintos términos, servicios y usuarios implicados en el proceso de incorporación.
* A su equipo listo para ponerse en marcha y dar los primeros pasos con el objetivo de aprender a crear y desarrollar contenido para su aplicación de AEM as a Cloud Service.

Como resultado:

* Su equipo está configurado y tiene acceso a los recursos de la nube.
* Los autores de AEM tendrán acceso a AEM as a Cloud Service y podrán empezar a crear contenido.
* Los desarrolladores y administradores de implementación de AEM tendrán acceso a AEM as a Cloud Service y podrán empezar a crear e implementar aplicaciones personalizadas.

## Conceptos y objetivo {#concepts}

<!-- Although there may appear to be a lot to learn when getting started with AEM as a Cloud Service, conceptually there are only a few, logical pieces.-->

El recorrido de incorporación para AEM as a Cloud Service se centra en los siguientes elementos principales:

* **Contrato**: revise su contrato de Adobe para comprender los detalles clave del proceso de incorporación.
* **Experience Hub**: utilice [experience.adobe.com](https://experience.adobe.com/) como punto de entrada central para las funciones de AEM. Experience Hub se adapta a su perfil y derechos de perfil para que pueda trabajar de manera eficaz. Desde aquí, vaya a:
   * **Admin Console**: administre usuarios y asigne funciones.
   * **Cloud Manager**: configure programas y entornos, acceda a Git y cree canalizaciones para administrar e implementar código personalizado.
   * **Sites**: cree, administre y entregue experiencias digitales. (Derechos basados en licencias)
   * **Assets**: organice, almacene y distribuya sus recursos digitales. (Derechos basados en licencias)
   * **Forms**: cree y administre formularios adaptables. (Derechos basados en licencias)

Estos conceptos se detallarán en este recorrido de incorporación. El objetivo es que, al final del recorrido, pueda realizar lo siguiente:

* Conceder el acceso necesario al usuario a AEM as a Cloud Service.
* Configurar los primeros recursos de nube para su proyecto.
* Sepa cómo implementar su primer código y crear su primer contenido.

Básicamente, empezará ejecutando su nuevo proyecto AEM as a Cloud Service.

## Público {#audience}

El recorrido de incorporación está escrito específicamente para el **administrador del sistema** de los clientes nuevos de AEM as a Cloud Service y de AEM en general. El administrador del sistema es la primera persona con la que Adobe contacta después de que se firme su contrato de AEM as a Cloud Service. Normalmente, es la primera persona en acceder a sus recursos y configurarlos en AEM as a Cloud Service. Si está leyendo este tema, es probable que usted sea el administrador del sistema.

El administrador del sistema administra todos los aspectos de los usuarios de AEMaaCS de su organización, desde el acceso a los permisos. Sin embargo, el administrador del sistema debe interactuar con otras personas a lo largo del camino.

| Grupo de usuarios | Descripción | Rol en el recorrido |
| --- | --- | --- |
| Administrador del sistema | El destinatario de este recorrido proporciona un aprovisionamiento inicial de recursos en la nube y asigna usuarios a funciones adecuadas en base a sus responsabilidades laborales. | La función le ayuda a administrar todos los aspectos de los usuarios, desde el acceso a los permisos. |
| Autor de contenido | Crea y revisa el contenido en AEM. | Una vez que el administrador del sistema ha concedido los permisos, los autores pueden iniciar su propio recorrido y crear contenido. |
| Desarrollador | Desarrolla aplicaciones de AEM que consumen contenido de diferentes fuentes. | Una vez que el administrador del sistema ha concedido los permisos, los desarrolladores pueden iniciar su propio recorrido y desarrollar soluciones. |
| Administrador de implementación | Agrega o actualiza un entorno, ejecuta la canalización e implementa un código para un entorno de AEM o con fines de calidad del código. | Una vez que el administrador del sistema haya concedido los permisos, los administradores de implementación pueden iniciar su propio recorrido y administrar las implementaciones. |

Esta guía de incorporación ilustra el proceso completo de incorporación como administrador del sistema. Los roles de los usuarios, desarrolladores y administradores de implementación de AEM se exploran brevemente como partes adicionales y opcionales del recorrido.

>[!TIP]
>
>Si es nuevo en AEM as a Cloud Service, está familiarizado con AEM y está migrando desde el modo on-premise o desde Adobe Managed Services, asegúrese de consultar el [Recorrido de migración de AEM as a Cloud Service](/help/journey-migration/getting-started.md).

## Información general sobre el recorrido de incorporación {#overview}

Los siguientes artículos describen en detalle los conceptos básicos de incorporación y le proporcionan conocimientos básicos de AEM as a Cloud Service. Aunque puede ir directamente a una parte concreta del recorrido, muchos conceptos se basan en los de artículos anteriores. Por lo tanto, si es nuevo en la incorporación, Adobe le recomienda que comience por el principio y avance en orden consecutivo.

| | Artículo | Descripción | Público |
| --- | --- | --- | --- |
| 0 | Recorrido de la incorporación | Este documento | Administrador del sistema |
| 1 | [Preparación de la incorporación](preparation.md) | Antes de iniciar el proceso de incorporación, hay que realizar una serie de pasos preparatorios que el administrador del sistema debe conocer antes de iniciar sesión en el sistema. | Administrador del sistema |
| 2 | [Terminología de AEM as a Cloud Service](terminology.md) | Antes de iniciar sesión en AEMaaCS por primera vez, resulta útil conocer parte de la terminología del sistema y su estructura básica. | Administrador del sistema |
| 3 | [Admin Console](admin-console.md) | Obtenga información sobre qué es Admin Console, cómo iniciar sesión y cómo comprobar el perfil como administrador del sistema. | Administrador del sistema |
| 4 | [Asignar perfiles de producto de Cloud Manager](assign-profiles-cloud-manager.md) | Revise los perfiles de producto de Cloud Manager y aprenda a asignarle miembros del equipo a perfiles de producto. | Administrador del sistema |
| 5 | [Acerca de Experience Hub](/help/experience-hub.md) | Utilice Experience Hub, que sirve como punto de entrada unificado y personalizado al ecosistema de AEM. | Usuarios de AEM |
| 6 | [Acceder a Cloud Manager](cloud-manager.md) | Obtenga información sobre cómo acceder a Cloud Manager para configurar los recursos del proyecto. | Administrador del sistema |
| 7 | [Crear un programa](create-program.md) | Obtenga información sobre cómo crear un programa mediante Cloud Manager. | Administrador del sistema |
| 8 | [Crear entornos](create-environments.md) | Obtenga información sobre cómo crear un entorno con Cloud Manager. | Administrador del sistema |
| 9 | [Asignar perfiles de producto de AEM](assign-profiles-aem.md) | Descubra cómo el administrador del sistema asigna los integrantes del equipo a los perfiles de producto en AEM as a Cloud Service. | Administrador del sistema |
| 10 | [Tareas del desarrollador y del administrador de implementación](developers.md) | Opcional: como desarrollador, aprenda a acceder a Git de Cloud Manager y a administrarlo. Como administrador de implementación, aprenda a configurar canalizaciones e implementar su código en Cloud Manager. | Desarrolladores y administradores de implementación |
| 11 | [Tareas del usuario de AEM](aem-users.md) | Opcional: Aprenda, como autor de AEM, cómo puede acceder a la instancia de AEM as a Cloud Service y familiarizarse con la creación de contenido para AEM as a Cloud Service. | Usuarios de AEM |

## Siguientes pasos {#what-is-next}

Ya está listo para iniciar su recorrido de incorporación de AEM as a Cloud Service. Le animamos a que continúe con la siguiente parte del recorrido y lea el artículo [Preparar la incorporación](preparation.md)

## Recorridos de documentación de AEM {#documentation-journeys}

[Un recorrido de documentación](/help/journey-documentation/documentation-journeys.md) reúne muchos temas y características diferentes y complicados. Proporciona una narrativa que ayuda a un lector nuevo en AEM a comprender y resolver un problema empresarial de principio a fin, mientras asume un conocimiento previo mínimo de la materia o de AEM.

Los recorridos de documentación están diseñados en torno a los principios de las prácticas recomendadas. Se les informa mediante las últimas investigaciones de Adobe, la experiencia de implementación comprobada de los consultores de Adobe y los comentarios de los proyectos de los clientes.

Si quiere saber lo que recomienda Adobe sobre cómo incorporar su equipo a su nueva aplicación de AEM as a Cloud Service, aquí es donde debe empezar.

## Recursos adicionales {#additional-resources}

Los siguientes son recursos opcionales adicionales si desea ir más allá del contenido del recorrido de incorporación.

* [Incorporación en AEM as a Cloud Service](https://experienceleague.adobe.com/es/docs/experience-manager-learn/cloud-service/migration/moving-to-aem-as-a-cloud-service/onboarding): en este breve vídeo se ofrece información general del proceso de incorporación de Cloud Service para AEM.
