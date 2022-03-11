---
title: Asignar integrantes del equipo a perfiles de producto de AEM as a Cloud Service
description: Siga esta página para obtener información sobre cómo asignar integrantes del equipo a AEM perfiles de producto as a Cloud Service
feature: Onboarding
role: Admin, User, Developer
exl-id: c00f5d28-85af-4bd3-a50c-913d1342241c
source-git-commit: 96a0dacf69f6f9c5744f224d1a48b2afa11fb09e
workflow-type: tm+mt
source-wordcount: '833'
ht-degree: 5%

---

# Asignar integrantes del equipo a perfiles de producto de AEM as a Cloud Service {#assign-team-members-cloud-service}

## Objetivo {#objective}

Este documento le ayuda a comprender los pasos que debe seguir el administrador del sistema para asignar los integrantes del equipo a AEM perfiles de producto as a Cloud Service y por qué es crucial permitir que los autores de AEM inicien su recorrido con AEM.

Después de leer esta sección debe comprender:

* Por qué y cómo se asignan los integrantes del equipo a AEM perfiles de producto as a Cloud Service.
* Cómo añadir integrantes del equipo a AEM perfil de producto Usuario.
* Cómo añadir integrantes del equipo al perfil de producto de AEM administradores.


## Introducción {#introduction}

Para que se le conceda acceso a AEM usuarios as a Cloud Service, debe pertenecer a uno de los dos perfiles de producto:  `AEM Users` o `AEM Administrators`. Los integrantes del equipo deben tener permisos para la instancia de AEM, ya que los permisos para administrar Cloud Manager no serán suficientes.

>[!NOTE]
>Todos los usuarios asignados a AEM perfil de producto Usuario por el administrador del sistema tendrán acceso (solo lectura) a Cloud Manager.

## Requisitos previos {#prerequisites}

Antes de comenzar a leer esta sección, debe considerar la posibilidad de seguir estos requisitos previos:

* Comprender [AEM perfiles de producto as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/aem-cs-team-product-profiles.html?lang=en#aem-product-profiles)
* Familiarícese con [Admin Console](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/admin-console.html?lang=en)
* Los perfiles de producto de Cloud Manager se han asignado a los miembros de su equipo según corresponda, y se han configurado los recursos de la nube
* Detalles sobre el miembro del equipo: El administrador del sistema debe tener los nombres y las direcciones de correo electrónico, así como las funciones y responsabilidades de los integrantes del equipo que necesitan tener acceso a AEM as a Cloud Service.

   >[!NOTE]
   >Con el fin de incorporarlo, le recomendamos que agregue inicialmente usuarios que participarán en las tareas inmediatas, como administradores, desarrolladores y autores de contenido. Puede continuar con el resto de la incorporación sin agregar todos los usuarios. Una vez que haya terminado la incorporación, puede escalar a un mayor número de usuarios más adelante.


   >[!IMPORTANT]
   >Antes de empezar a revisar los pasos para asignar integrantes del equipo a AEM perfiles de producto as a Cloud Service, asegúrese de seguir estos dos pasos:
   >
   >1. Iniciar sesión en [Adobe Admin Console](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/admin-console.html?lang=en). Consulte Inicio de sesión en Admin Console para obtener más información.
   >
   >1. Consulte [Perfiles de producto as a Cloud Service de AEM](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/aem-cs-team-product-profiles.html?lang=en#aem-product-profiles).


Siga los pasos a continuación para ver la lista de perfiles de Cloud Manager de Adobe Admin Console:

1. Iniciar sesión en [Adobe Admin Console](https://adminconsole.adobe.com/). En el **Información general** página, seleccione **Adobe Experience Manager as a Cloud Service** de la variable **Productos y servicios** tarjeta.

   ![](/help/journey-onboarding/assets/assign-team1.png)

1. Desplácese y seleccione la instancia (instancia de autor del entorno de desarrollo) como se muestra en la imagen siguiente.

   ![](/help/journey-onboarding/assets/cloud-profiles-1.png)


1. Verá la lista de AEM perfiles de producto as a Cloud Service que se deben asignar a un usuario según su función.

   >[!NOTE]
   >Para obtener más información sobre estos elementos, consulte [Perfiles de producto as a Cloud Service de AEM](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/aem-cs-team-product-profiles.html?lang=en#aem-product-profiles).

   ![](/help/journey-onboarding/assets/cloud-profiles-2.png)


## Agregar integrantes del equipo a AEM perfil de usuario o administrador AEM producto {#add-team-members}

Para que se le conceda acceso a AEM instancia as a Cloud Service, los usuarios deben pertenecer a uno de los dos perfiles de producto `AEM Users` o `AEM Administrators`.

>[!NOTE]
>Se le deben conceder permisos para la instancia, los permisos para administrar Cloud Manager no serán suficientes. Más información.

Los pasos siguientes deben ser seguidos por un administrador del sistema que también esté en la función Propietario empresarial .

1. Vaya al programa desde Cloud Manager y seleccione la **Administrar acceso** del contexto del entorno de interés como se muestra a continuación.

   ![](/help/journey-onboarding/assets/add-team1.png)

1. Una nueva ficha le lleva a Adobe Admin Console desde donde tiene acceso a la instancia de autor del entorno. Select **Administradores de AEM** o **AEM usuarios** en función de los permisos que se le deben otorgar a esta persona. Más información sobre [AEM perfiles de producto as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/aem-cs-team-product-profiles.html?lang=en#aem-product-profiles).

   ![](/help/journey-onboarding/assets/add-team2.png)

1. Select `AEM Administrator` o `AEM User` y haga clic en **Agregar usuario** como se muestra a continuación, y envíe los detalles necesarios para completar la adición del miembro del equipo.

   ![](/help/journey-onboarding/assets/add-team3.png)

   El usuario que ha agregado ahora tendrá acceso a los AEM servicios de Autor as a Cloud Service.

   >[!NOTE]
   >Estos pasos se repetirán para todos los entornos, incluidos Desarrollo, Fase y Producción, si tiene disponible la información de los integrantes del equipo que necesitan tener acceso.


## Siguientes pasos {#whats-next}

Los usuarios que asignó a AEM perfiles de producto as a Cloud Service ya están listos para aprender a acceder a Author y familiarizarse con la creación de páginas en AEM as a Cloud Service. Debe seguir la ruta, revisando el documento Ruta de aprendizaje para [AEM usuarios](/help/journey-onboarding/sysadmin/learning-path-aem-users.md) o [Desarrolladores y gestores de implementación](/help/journey-onboarding/sysadmin/learning-path-developers-deploymentmanagers.md).

## Recursos adicionales {#additional-resources}

* [Administración de productos y acceso de usuarios en Admin Console](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/security/ims-support.html?lang=en#managing-products-and-user-access-in-admin-console)
* [Configuración del acceso a AEM](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/accessing/walk-through.html?lang=en)
* [Guía rápida para la creación de páginas](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/sites/authoring/getting-started/quick-start.html?lang=en)
