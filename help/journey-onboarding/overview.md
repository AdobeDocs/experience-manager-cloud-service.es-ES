---
title: Introducción al Recorrido de incorporación as a Cloud Service de AEM
description: Comience aquí para obtener una descripción general del recorrido guiado a través del proceso de incorporación para AEM as a Cloud Service.
exl-id: 892577db-05dc-49ff-bb2c-203efdb89c8c
source-git-commit: 75c0e8cbaa409fa48750e794c27ace98eda107d0
workflow-type: tm+mt
source-wordcount: '1175'
ht-degree: 15%

---


# Recorrido de incorporación {#onboarding-journey}

¡Felicidades por elegir AEM as a Cloud Service! Este documento es el punto de partida para un recorrido guiado a través del proceso de incorporación. Tanto si va a implementar una aplicación nueva como si va a migrar una existente, este recorrido de incorporación garantiza que sus equipos estén configurados y tengan acceso a AEM as a Cloud Service.

## Introducción {#introduction}

La incorporación es el proceso durante el cual un administrador designado del sistema configura AEM as a Cloud Service para su organización. Esto incluye el aprovisionamiento inicial de recursos en la nube y la asignación de usuarios a funciones en función de sus responsabilidades laborales. Como resultado, cada miembro puede iniciar sesión y acceder a sus AEM recursos as a Cloud Service.

![El recorrido de incorporación](/help/journey-onboarding/assets/onboarding-journey.png)

Esta guía le guía por los temas de incorporación más importantes para que, una vez finalizada, tenga:

* Comprensión completa de los distintos términos, servicios y usuarios implicados en el proceso de incorporación.
* A su equipo listo para ponerse en marcha y dar los primeros pasos con el objetivo de aprender a crear y desarrollar contenido para su aplicación de AEM as a Cloud Service.

Como resultado:

* Su equipo se configurará y tendrá acceso a los recursos de la nube.
* AEM autores tendrán acceso a AEM as a Cloud Service y pueden empezar a crear contenido.
* AEM desarrolladores y administradores de implementación tendrán acceso a AEM as a Cloud Service y podrán empezar a crear e implementar aplicaciones personalizadas.

## Conceptos y objetivo {#concepts}

Aunque puede parecer que hay mucho que aprender cuando se empieza con AEM as a Cloud Service, conceptualmente sólo hay unas pocas piezas lógicas.

* **El contrato** - Debe estar familiarizado con su contrato de Adobe, ya que define aspectos del proceso de incorporación.
* **Admin Console** : aquí es donde se administran los usuarios y se asignan las funciones.
* **Cloud Manager** - Esta es la herramienta para configurar recursos como programas y entornos. También es donde puede acceder a Git y crear canalizaciones para administrar e implementar su código personalizado.

Estos conceptos se detallarán en este recorrido de incorporación. El objetivo es que al final del recorrido:

* Han concedido a los usuarios necesarios acceso a AEMaaCS
* Han configurado los primeros recursos de nube para su proyecto
* Obtenga información sobre cómo implementar su primer código y crear su primer contenido.

Básicamente, llegará al terreno ejecutando su nuevo proyecto as a Cloud Service AEM!

## Audiencia {#audience}

El recorrido de incorporación está escrito específicamente para el **administrador del sistema** del nuevo cliente a AEM as a Cloud Service y a AEM en general. El administrador del sistema es la persona a la que se contacta por primera vez mediante Adobe después de firmar el contrato as a Cloud Service de AEM y, por lo general, es la primera persona en acceder y configurar los recursos as a Cloud Service de AEM. Si está leyendo esto, es probable que sea el administrador del sistema.

El administrador del sistema gestiona todos los aspectos de los usuarios de AEMaaCS de su organización, desde el acceso a los permisos. Sin embargo, el administrador del sistema debe interactuar con otras personas a lo largo del camino.

| Grupo de usuarios | Descripción | Función en el recorrido |
|---|---|---|
| Administrador del sistema | Target de este recorrido, proporciona aprovisionamiento inicial de recursos en la nube y asignación de usuarios a funciones adecuadas en función de sus responsabilidades de trabajo | Gestiona todos los aspectos del acceso de los usuarios a los permisos |
| Autor de contenido | Crea y revisa el contenido en AEM | Una vez que el administrador del sistema ha concedido los permisos, los autores pueden iniciar su propio recorrido creando contenido |
| Desarrollador | Desarrolla aplicaciones de AEM que consumen contenido de diferentes fuentes | Una vez que el administrador del sistema ha concedido los permisos, los desarrolladores pueden iniciar sus propias soluciones de desarrollo de recorrido |
| Administrador de implementación | Agrega o actualiza un entorno, ejecuta canalizaciones e implementa código para AEM entorno o calidad de código. | Una vez que el administrador del sistema haya concedido los permisos, los administradores de implementación pueden iniciar su propio recorrido y administrar las implementaciones |

Esta guía de incorporación ilustra el proceso completo de incorporación como administrador del sistema. Las funciones de AEM usuarios, desarrolladores y administradores de implementación se exploran brevemente como partes adicionales y opcionales del recorrido.

>[!TIP]
>
>Si es nuevo en AEM as a Cloud Service, pero ya está familiarizado con AEM y está migrando desde on-premise o Adobe Managed Services, asegúrese de consultar la [AEM Recorrido as a Cloud Service de migración.](/help/journey-migration/getting-started.md)

## Información general sobre el Recorrido de incorporación {#overview}

Los siguientes artículos describen en detalle los conceptos básicos de incorporación y le proporcionan conocimientos básicos de AEM as a Cloud Service. Aunque puede ir directamente a una parte concreta del recorrido, muchos conceptos se basan en los de artículos anteriores. Por lo tanto, si es nuevo en la incorporación, le recomendamos que comience por el principio y avance secuencialmente.

| # | Artículo | Descripción | Audiencia |
|---|---|---|---|
| 0 | Recorrido de incorporación | Este documento | Administrador del sistema |
| 1 | [Preparación de la incorporación](preparation.md) | Antes de iniciar el proceso de incorporación, hay que realizar una serie de pasos preparatorios que el administrador del sistema debe conocer antes de iniciar sesión en el sistema. | Administrador del sistema |
| 2 | [Terminología as a Cloud Service AEM](terminology.md) | Antes de iniciar sesión en AEMaaCS por primera vez, resulta útil conocer parte de la terminología del sistema y su estructura básica. | Administrador del sistema |
| 3 | [El Admin Console](admin-console.md) | Obtenga información sobre qué es el Admin Console, cómo iniciar sesión y cómo comprobar el perfil como administrador del sistema. | Administrador del sistema |
| 4 | [Asignación de perfiles de producto de Cloud Manager](assign-profiles-cloud-manager.md) | Revise los perfiles de producto de Cloud Manager y aprenda a asignar miembros del equipo a perfiles de producto de Cloud Manager. | Administrador del sistema |
| 5 | [Acceso a Cloud Manager](cloud-manager.md) | Obtenga información sobre cómo acceder a Cloud Manager para configurar los recursos del proyecto. | Administrador del sistema |
| 6 | [Crear un programa](create-program.md) | Obtenga información sobre cómo crear un programa mediante Cloud Manager. | Administrador del sistema |
| 7 | [Crear entornos](create-environments.md) | Obtenga información sobre cómo crear un entorno con Cloud Manager. | Administrador del sistema |
| 8 | [Asignación AEM perfiles de producto](assign-profiles-aem.md) | Descubra cómo el administrador del sistema asigna a los miembros de su equipo AEM perfiles de producto as a Cloud Service. | Administrador del sistema |
| 9 | [Tareas del desarrollador y del administrador de implementación](developers.md) | Opcional: Obtenga información sobre cómo, como desarrollador, puede acceder a Cloud Manager Git y administrarlo, y cómo, como administrador de implementación, puede configurar canalizaciones e implementar código en Cloud Manager. | Desarrolladores y gestores de implementación |
| 10 | [Tareas del usuario AEM](aem-users.md) | Opcional: Aprenda cómo, como autor AEM, puede acceder a AEM instancia as a Cloud Service y familiarizarse con la creación de contenido para AEM as a Cloud Service. | AEM usuarios |

## Siguientes pasos {#what-is-next}

Ya está listo para iniciar su recorrido de incorporación as a Cloud Service AEM. Le animamos a que continúe con la siguiente parte del recorrido y lea el artículo [Preparación de la incorporación](preparation.md)

## Recorridos de documentación de AEM {#documentation-journeys}

[Un recorrido de documentación](/help/journey-documentation/documentation-journeys.md) une muchos temas y características diferentes y tal vez complicados. Proporciona una narrativa que ayuda al lector (que puede ser nuevo en AEM) a entender y resolver un problema empresarial de principio a fin, mientras asume un conocimiento previo mínimo de AEM.

Los recorridos de documentación están diseñados en torno a los principios de las prácticas recomendadas, basados en las últimas investigaciones de Adobe, la experiencia de implementación comprobada de los consultores de Adobe y los comentarios sobre los proyectos de los clientes.

Si desea saber cómo recomienda Adobe que su equipo se incorpore a su nueva aplicación as a Cloud Service de AEM, aquí es donde debe comenzar.
