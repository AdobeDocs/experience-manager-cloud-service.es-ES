---
title: 'Asignar miembros del equipo a AEM como perfiles de producto del Cloud Service '
description: Siga esta página para obtener información sobre cómo asignar integrantes del equipo a AEM como perfiles de producto del Cloud Service
hide: true
index: false
source-git-commit: 4a6408c498b093fc8b3baf4bdf1798b4281c90c2
workflow-type: tm+mt
source-wordcount: '833'
ht-degree: 2%

---


# Asignar miembros del equipo a AEM como perfiles de producto del Cloud Service {#assign-team-members-cloud-service}

## Objetivo {#objective}

Este documento le ayuda a comprender los pasos que debe seguir el administrador del sistema para asignar los integrantes del equipo a AEM como perfiles de producto Cloud Service y por qué es crucial permitir que los autores de AEM inicien su recorrido con AEM.

Después de leer esta sección debe comprender:

* Por qué y cómo se asignan los miembros de su equipo a AEM como perfiles de producto de Cloud Service.
* Cómo añadir integrantes del equipo a AEM perfil de producto Usuario.
* Cómo añadir integrantes del equipo al perfil de producto de AEM administradores.


## Introducción {#introduction}

Para que se le conceda acceso a AEM como Cloud Service, los usuarios deben pertenecer a uno de los dos perfiles de producto:  `AEM Users` o `AEM Administrators`. Los integrantes del equipo deben tener permisos para la instancia de AEM, ya que los permisos para administrar Cloud Manager no serán suficientes.

>[!NOTE]
>Todos los usuarios asignados a AEM perfil de producto Usuario por el administrador del sistema tendrán acceso (solo lectura) a Cloud Manager.

## Requisitos previos {#prerequisites}

Antes de comenzar a leer esta sección, debe considerar la posibilidad de seguir estos requisitos previos:

* Comprender [AEM como perfiles de producto del Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/aem-cs-team-product-profiles.html?lang=en#aem-product-profiles)
* Familiarícese con [Admin Console](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/admin-console.html?lang=en)
* Los perfiles de producto de Cloud Manager se han asignado a los miembros de su equipo según corresponda, y se han configurado los recursos de la nube
* Detalles sobre el miembro del equipo: El administrador del sistema debe tener los nombres y las direcciones de correo electrónico, así como las funciones y responsabilidades de los integrantes del equipo que necesitan tener acceso a AEM como Cloud Service.

   >[!NOTE]
   >Con el fin de incorporarlo, le recomendamos que agregue inicialmente usuarios que participarán en las tareas inmediatas, como administradores, desarrolladores y autores de contenido. Puede continuar con el resto de la incorporación sin agregar todos los usuarios. Una vez que haya terminado la incorporación, puede escalar a un mayor número de usuarios más adelante.


   >[!IMPORTANT]
   >Antes de empezar a revisar los pasos para asignar integrantes del equipo a AEM como perfiles de producto de Cloud Service, asegúrese de seguir estos dos pasos:
   >
   >1. Inicie sesión en [Adobe Admin Console](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/admin-console.html?lang=en). Consulte Inicio de sesión en Admin Console para obtener más información.
      >
      >
   1. Revise [AEM como Cloud Service de perfiles de producto](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/aem-cs-team-product-profiles.html?lang=en#aem-product-profiles).


Siga los pasos a continuación para ver la lista de perfiles de Cloud Manager de Adobe Admin Console:

1. Inicie sesión en [Adobe Admin Console](https://adminconsole.adobe.com/). En la página **Información general**, seleccione **Adobe Experience Manager as a Cloud Service** en la tarjeta **Productos y servicios**.

   ![](/help/onboarding/onboarding-journey/assets/assign-team1.png)

1. Desplácese y seleccione la instancia (instancia de autor del entorno de desarrollo) como se muestra en la imagen siguiente.

   ![](/help/onboarding/onboarding-journey/assets/cloud-profiles-1.png)


1. Verá la lista de AEM como perfiles de producto de Cloud Service que se deben asignar a un usuario según su función.

   >[!NOTE]
   >Para obtener más información sobre estos parámetros, consulte [AEM as a Cloud Service Product Profiles](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/aem-cs-team-product-profiles.html?lang=en#aem-product-profiles).

   ![](/help/onboarding/onboarding-journey/assets/cloud-profiles-2.png)


## Agregar integrantes del equipo a AEM perfil de usuario o administrador de producto de AEM {#add-team-members}

Para obtener acceso a AEM como instancia de Cloud Service, los usuarios deben pertenecer a uno de los dos perfiles de producto `AEM Users` o `AEM Administrators`.

>[!NOTE]
>Se le deben conceder permisos para la instancia, los permisos para administrar Cloud Manager no serán suficientes. Más información.

Los pasos siguientes deben ser seguidos por un administrador del sistema que también esté en la función Propietario empresarial .

1. Vaya al programa desde Cloud Manager y seleccione el botón **Administrar acceso** en el contexto del entorno de interés, como se muestra a continuación.

   ![](/help/onboarding/onboarding-journey/assets/add-team1.png)

1. Una nueva ficha le lleva a Adobe Admin Console desde donde tiene acceso a la instancia de autor del entorno. Seleccione **AEM Administradores** o **AEM Usuarios** en función de los permisos que se le deben dar a esta persona. Obtenga más información sobre [AEM as a Cloud Service product profiles](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/aem-cs-team-product-profiles.html?lang=en#aem-product-profiles).

   ![](/help/onboarding/onboarding-journey/assets/add-team2.png)

1. Seleccione `AEM Administrator` o `AEM User` y haga clic en **Agregar usuario** como se muestra a continuación y envíe los detalles necesarios para completar la adición del miembro del equipo.

   ![](/help/onboarding/onboarding-journey/assets/add-team3.png)

   El usuario que ha agregado ahora tendrá acceso al AEM como Cloud Service Author services!

   >[!NOTE]
   >Estos pasos se repetirán para todos los entornos, incluidos Desarrollo, Fase y Producción, si tiene disponible la información de los integrantes del equipo que necesitan tener acceso.


## Siguientes pasos {#whats-next}

Los usuarios que asignó a AEM como perfiles de producto Cloud Service ahora están listos para aprender a acceder a Author y familiarizarse con la creación de páginas en AEM como Cloud Service. Debe seguir la ruta, revisando el documento Ruta de aprendizaje para [AEM usuarios](/help/onboarding/onboarding-journey/learning-path-aem-users.md) o para [desarrolladores y gestores de implementación](/help/onboarding/onboarding-journey/learning-path-developers-deploymentmanagers.md).

## Recursos adicionales {#additional-resources}

* [Administración de productos y acceso de usuarios en Admin Console](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/security/ims-support.html?lang=en#managing-products-and-user-access-in-admin-console)
* [Configuración del acceso a AEM](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/accessing/walk-through.html?lang=en)
* [Guía rápida para la creación de páginas](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/sites/authoring/getting-started/quick-start.html?lang=en)