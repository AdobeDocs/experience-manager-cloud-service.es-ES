---
title: Introducción al Recorrido de incorporación a AEM as a Cloud Service
description: Comience aquí para obtener una descripción general del recorrido guiado a través del proceso de incorporación para AEM as a Cloud Service.
exl-id: 892577db-05dc-49ff-bb2c-203efdb89c8c
source-git-commit: 98eff568686c72c626d2bf77d82e8c3f224eda42
workflow-type: tm+mt
source-wordcount: '1172'
ht-degree: 59%

---


# Recorrido de incorporación {#onboarding-journey}

¡Felicidades por elegir AEM as a Cloud Service! Este documento es el punto de partida para un recorrido guiado a través del proceso de incorporación. Tanto si va a implementar una aplicación nueva como si va a migrar una existente, este recorrido de incorporación garantiza que sus equipos estén configurados y tengan acceso a AEM as a Cloud Service.

## Introducción {#introduction}

La incorporación es el proceso durante el cual un administrador designado del sistema configura AEM as a Cloud Service para su organización. Este proceso incluye el aprovisionamiento inicial de recursos de la nube y la asignación de usuarios a funciones en función de sus responsabilidades de trabajo. Como resultado, cada miembro puede iniciar sesión y acceder a su recurso en AEM as a Cloud Service.

![El recorrido de incorporación](/help/journey-onboarding/assets/onboarding-journey.png)

Esta guía le guía por los temas de incorporación más importantes, de modo que al completarse tenga lo siguiente:

* Una comprensión total de los distintos términos, servicios y usuarios implicados en el proceso de incorporación.
* A su equipo listo para ponerse en marcha y dar los primeros pasos con el objetivo de aprender a crear y desarrollar contenido para su aplicación de AEM as a Cloud Service.

Como resultado:

* Su equipo está configurado y tiene acceso a los recursos de la nube.
* AEM autores tienen acceso a AEM as a Cloud Service y pueden empezar a crear contenido.
* AEM desarrolladores y administradores de implementación tienen acceso a AEM as a Cloud Service y pueden empezar a crear e implementar aplicaciones personalizadas.

## Conceptos y objetivo {#concepts}

Aunque puede parecer que hay mucho que aprender cuando se empieza con AEM as a Cloud Service, conceptualmente solo hay unas pocas piezas lógicas.

* **El contrato** - Debe estar familiarizado con su contrato de Adobe, ya que define aspectos del proceso de incorporación.
* **Admin Console** - Dónde se administran los usuarios y se asignan las funciones.
* **Cloud Manager** - La herramienta para configurar recursos como programas y entornos. También es donde puede acceder a Git y crear canalizaciones para administrar e implementar su código personalizado.

Estos conceptos se describen detalladamente en este recorrido de incorporación. El objetivo es que al final del recorrido haya conseguido lo siguiente:

* Han concedido al usuario el acceso necesario a AEM as a Cloud Service.
* Haya configurado los primeros recursos de nube para su proyecto.
* Sepa cómo implementar su primer código y crear su primer contenido.

Básicamente, usted dio en marcha con su nuevo proyecto as a Cloud Service AEM!

## Audiencia {#audience}

El recorrido de incorporación está escrito específicamente para el **administrador del sistema** de los clientes nuevos de AEM as a Cloud Service y de AEM en general. El administrador del sistema es la persona a la que el Adobe se pone en contacto por primera vez tras firmar el contrato as a Cloud Service AEM. Normalmente, son la primera persona en acceder a los recursos y configurarlos en AEM as a Cloud Service. Si está leyendo este tema, es probable que sea el administrador del sistema.

El administrador del sistema administra todos los aspectos de los usuarios de AEMaaCS de su organización, desde el acceso a los permisos. Sin embargo, el administrador del sistema debe interactuar con otras personas a lo largo del camino.

| Grupo de usuarios | Descripción | Rol en el recorrido |
|---|---|---|
| Administrador del sistema | Es el destinatario de este recorrido, proporciona un aprovisionamiento inicial de recursos en la nube y asigna usuarios a roles adecuados en base a sus responsabilidades laborales. | Administra todos los aspectos de sus usuarios desde el acceso a los permisos |
| Autor de contenido | Crea y revisa el contenido en AEM | Una vez que el administrador del sistema ha concedido los permisos, los autores pueden iniciar su propio recorrido y crear contenido |
| Desarrollador | Desarrolla aplicaciones de AEM que consumen contenido de diferentes fuentes | Una vez que el administrador del sistema ha concedido los permisos, los desarrolladores pueden iniciar su propio recorrido y desarrollar soluciones |
| Administrador de implementación | Agrega o actualiza un entorno, ejecuta la canalización e implementa un código para un entorno de AEM o con fines de calidad del código. | Una vez que el administrador del sistema haya concedido los permisos, los administradores de implementación pueden iniciar su propio recorrido y administrar las implementaciones |

Esta guía de incorporación ilustra el proceso completo de incorporación como administrador del sistema. Los roles de los usuarios, desarrolladores y administradores de implementación de AEM se exploran brevemente como partes adicionales y opcionales del recorrido.

>[!TIP]
>
>Si es nuevo en AEM as a Cloud Service y está familiarizado con AEM y está migrando desde on-premise o Adobe Managed Services, asegúrese de consultar la [recorrido de migración as a Cloud Service de AEM](/help/journey-migration/getting-started.md).

## Información general sobre el recorrido de incorporación {#overview}

Los siguientes artículos describen en detalle los conceptos básicos de incorporación y le proporcionan conocimientos básicos de AEM as a Cloud Service. Aunque puede ir directamente a una parte concreta del recorrido, muchos conceptos se basan en los de artículos anteriores. Por lo tanto, si es nuevo en la incorporación, Adobe recomienda que comience al principio y que avance secuencialmente.

| # | Artículo | Descripción | Audiencia |
|---|---|---|---|
| 0 | Recorrido de incorporación | Este documento | Administrador del sistema |
| 1 | [Preparación de la incorporación](preparation.md) | Antes de iniciar el proceso de incorporación, hay que realizar una serie de pasos preparatorios que el administrador del sistema debe conocer antes de iniciar sesión en el sistema. | Administrador del sistema |
| 2 | [Terminología de AEM as a Cloud Service](terminology.md) | Antes de iniciar sesión en AEMaaCS por primera vez, resulta útil conocer parte de la terminología del sistema y su estructura básica. | Administrador del sistema |
| 3 | [Admin Console](admin-console.md) | Obtenga información sobre qué es Admin Console, cómo iniciar sesión y cómo comprobar el perfil como administrador del sistema. | Administrador del sistema |
| 4 | [Asignar perfiles de producto de Cloud Manager](assign-profiles-cloud-manager.md) | Revise los perfiles de producto de Cloud Manager y aprenda a asignarle miembros del equipo a perfiles de producto. | Administrador del sistema |
| 5 | [Acceder a Cloud Manager](cloud-manager.md) | Obtenga información sobre cómo acceder a Cloud Manager para configurar los recursos del proyecto. | Administrador del sistema |
| 6 | [Crear un programa](create-program.md) | Obtenga información sobre cómo crear un programa mediante Cloud Manager. | Administrador del sistema |
| 7 | [Crear entornos](create-environments.md) | Obtenga información sobre cómo crear un entorno con Cloud Manager. | Administrador del sistema |
| 8 | [Asignar perfiles de producto de AEM](assign-profiles-aem.md) | Obtenga información sobre cómo el administrador del sistema asigna a los miembros del equipo perfiles de producto en AEM as a Cloud Service. | Administrador del sistema |
| 9 | [Tareas del desarrollador y del administrador de implementación](developers.md) | Opcional: Como desarrollador, aprenda a acceder y administrar Cloud Manager Git y a configurar canalizaciones e implementar código en Cloud Manager como administrador de implementación. | Desarrolladores y administradores de implementación |
| 10 | [Tareas del usuario de AEM](aem-users.md) | Opcional: como autor AEM, aprenda a acceder a AEM instancia as a Cloud Service y a familiarizarse con la creación de contenido para AEM as a Cloud Service. | Usuarios de AEM  |

## Siguientes pasos {#what-is-next}

Ya está listo para iniciar su recorrido de incorporación de AEM as a Cloud Service. Se le anima a continuar con la siguiente parte del recorrido y leer el artículo [Preparación de la incorporación](preparation.md)

## Recorridos de documentación de AEM {#documentation-journeys}

[Un Recorrido de documentación](/help/journey-documentation/documentation-journeys.md) une muchos temas y características diferentes y complicados. Proporciona una narrativa que ayuda a un lector nuevo a AEM entender y resolver un problema comercial de principio a fin, mientras asume un tema previo mínimo o conocimientos AEM.

Los recorridos de documentación están diseñados en torno a los principios de las prácticas recomendadas, basados en las últimas investigaciones de Adobe, la experiencia de implementación comprobada de los consultores de Adobe y los comentarios sobre los proyectos de los clientes.

Si desea saber qué recomienda el Adobe sobre cómo incorporar a su equipo a su nueva aplicación as a Cloud Service de AEM, comience aquí!

<!-- ERROR: Not Found (HTTP error 404)
## Additional Resources {#additional-resources}

The following are additional, optional resources if you would like to go beyond the content of the onboarding journey.

* [AEM Champion Tips and Tricks - Cloud Manager Onboarding Playbook](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/expert-resources/aem-champions/onboarding-playbook.md) - Watch this video to learn Cloud Manager onboarding tips and trick from an AEM champion. -->


