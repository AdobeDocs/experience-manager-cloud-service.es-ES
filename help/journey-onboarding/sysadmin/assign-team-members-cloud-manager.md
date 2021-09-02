---
title: 'Asignación de miembros del equipo a perfiles de producto de Cloud Manager '
description: Siga esta página para obtener información sobre cómo asignar miembros del equipo a perfiles de producto de Cloud Manager
feature: Onboarding
role: Admin, User, Developer
source-git-commit: d8ff6f4386ab0e5df4f770cdb566facc1cc0cc98
workflow-type: tm+mt
source-wordcount: '1440'
ht-degree: 0%

---


# Asignar miembros del equipo a perfiles de producto de Cloud Manager {#assign-team-members}

Una vez que haya aprendido a iniciar sesión en [Admin Console](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/admin-console.html?lang=en) y haya visto sus privilegios como [administrador del sistema](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/system-administrator.html?lang=en), ya está listo para asignar miembros del equipo a perfiles de producto de Cloud Manager.

## Objetivo {#objective}

Este documento resume cómo asignar miembros del equipo a perfiles de producto de Cloud Manager desde Adobe Admin Console.

Después de leer esta sección debe poder:

* Comprenda por qué y cómo debe agregar miembros del equipo.
* Obtenga información sobre tres perfiles de producto de Cloud Manager diferentes, como Propietario empresarial, Administrador de implementación y Desarrollador.
* Asigne integrantes del equipo a perfiles de producto de Cloud Manager, como Propietario empresarial, Administrador de implementación y Desarrollador.

## Requisitos previos {#prerequisites}

Los siguientes requisitos previos deben tenerse en cuenta antes de iniciar esta sección. Debe:

* Sea administrador del sistema y comprenda [Cloud Manager Product Profiles](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/aem-cs-team-product-profiles.html?lang=en#cloud-manager-product-profiles).
* Comprender los conceptos básicos de [Adobe Admin Console](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/admin-console.html?lang=en).
* Tener detalles sobre los integrantes del equipo. Un administrador del sistema debe tener los nombres, las direcciones de correo electrónico y las funciones y responsabilidades de los integrantes del equipo que necesitan acceder a AEM como Cloud Service.

   >[!NOTE]
   >Con el fin de incorporarlo, le recomendamos que agregue inicialmente usuarios que participarán en las tareas inmediatas, como administradores, desarrolladores y autores de contenido. Puede continuar con el resto de la incorporación sin agregar todos los usuarios. Una vez que haya terminado la incorporación, puede escalar a un mayor número de usuarios más adelante.

## Revisar perfiles de producto de Cloud Manager {#review-product-profiles}

Desde Adobe Admin Console puede ver la lista de perfiles de Cloud Manager.

>[!NOTE]
>Antes de revisar los perfiles de producto de Cloud Manager de Admin Console, se recomienda revisar los [Perfiles de producto de Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/aem-cs-team-product-profiles.html?lang=en#cloud-manager-product-profiles) disponibles.

Siga los pasos a continuación para ver la lista de perfiles de Cloud Manager:

1. Inicie sesión en [Adobe Admin Console](https://adminconsole.adobe.com/). En la página **Información general**, seleccione **Adobe Experience Manager as a Cloud Service** en la tarjeta **Productos y servicios**.

   ![](/help/journey-onboarding/assets/assign-team1.png)

   >[!NOTE]
   >Consulte Inicio de sesión en Admin Console para obtener información sobre cómo utilizar Admin Console.


1. Vaya a la instancia **Cloud Manager** de la lista de todas las instancias.

   ![](/help/journey-onboarding/assets/assign-team2.png)

1. Verá la lista de perfiles de producto preconfigurados de [Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/aem-cs-team-product-profiles.html?lang=en#cloud-manager-product-profiles).

   ![](/help/journey-onboarding/assets/assign-team3.png)


## Asignar usuarios al perfil de producto del propietario del negocio {#assign-users-business-owner}

Ya está listo para agregar usuarios y asignarlos al perfil de producto Propietario empresarial de Cloud Manager.

>[!NOTE]
>Para hacerlo correctamente, desde la consola de administración de Adobe debe agregar un usuario al producto (AEM como Cloud Service en este caso) y al perfil de producto [Propietario empresarial de Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/aem-cs-team-product-profiles.html?lang=en#cloud-manager-product-profiles).

Los siguientes pasos le guían a través de esto:

1. Identifique a los usuarios que administrarán los programas de Cloud Manager y agréguelos al perfil de producto Propietario empresarial . El administrador del sistema debe ser la primera persona en acceder a Cloud Manager e iniciar sesión en él. Primero debe agregarse (administrador del sistema) al perfil de producto Propietario del negocio .

1. En la página [Admin Console](https://adminconsole.adobe.com/enterprise/overview) **Información general**, seleccione **Adobe Experience Manager as a Cloud Service** producto de la tarjeta **Productos y servicios** como se muestra a continuación.

   ![](/help/journey-onboarding/assets/assign-team1.png)

1. Seleccione la pestaña **Users** en la barra de navegación superior y, a continuación, seleccione **Add User**.

   ![](/help/journey-onboarding/assets/assign-team4.png)

1. En el cuadro de diálogo **Agregar usuarios a su equipo**, escriba el ID de correo electrónico del usuario que desea agregar. Para el tipo de ID, seleccione Adobe ID si el Federated ID de los integrantes del equipo aún no se ha configurado.

   ![](/help/journey-onboarding/assets/assign-team5.png)

1. En la selección Producto, seleccione **Adobe Experience Manager as a Cloud Service** y asigne al usuario el perfil de producto **Propietario del negocio** como se muestra a continuación.

   >[!NOTE]
   >Consulte [Cloud Manager product profiles](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/aem-cs-team-product-profiles.html?lang=en#cloud-manager-product-profiles) para asegurarse de que se asignen a los usuarios adecuados las funciones correctas en el Admin Console, como se muestra a continuación.

   ![](/help/journey-onboarding/assets/assign-team6.png)

   >[!NOTE]
   >Asigne el usuario al menos a un perfil de producto para que el usuario pueda acceder a Cloud Manager. Recuerde asignarse a usted mismo (administrador del sistema) al propietario del negocio.

1. Haga clic en **Guardar**. Se envía un correo electrónico de bienvenida al usuario que ha añadido. El usuario invitado puede acceder a Cloud Manager haciendo clic en el vínculo del correo electrónico de bienvenida e iniciando sesión con su Adobe ID.

   Felicitaciones! Se ha configurado su equipo de Cloud Manager recién formado (incluido el que se ha asignado a la función &quot;Propietario empresarial&quot;). Los miembros recibirán un correo electrónico de bienvenida en el que se les invitará a iniciar sesión y acceder a Cloud Manager. En la función Propietario empresarial, ahora está a un paso de iniciar sesión en Cloud Manager y de habilitar la creación de los recursos de la nube.

## Asignar usuarios al perfil de producto del administrador de implementación {#assign-users-deployment-manager}

1. Identifique a los usuarios que administrarán los programas de Cloud Manager y agréguelos al perfil de producto de Deployment Manager. El administrador del sistema debe ser la primera persona en acceder a Cloud Manager e iniciar sesión en él. Debe agregarse primero (administrador del sistema) al perfil de producto Propietario del negocio (tal como se describe en la sección anterior).

1. En la página [Admin Console](https://adminconsole.adobe.com/enterprise/overview) **Información general**, seleccione **Adobe Experience Manager as a Cloud Service** producto de la tarjeta **Productos y servicios** como se muestra a continuación.

   ![](/help/journey-onboarding/assets/assign-team1.png)

1. Seleccione la pestaña **Users** en la barra de navegación superior y, a continuación, seleccione **Add User**.

   ![](/help/journey-onboarding/assets/assign-team4.png)

1. En el cuadro de diálogo **Agregar usuarios a su equipo**, escriba el ID de correo electrónico del usuario que desea agregar. Para el tipo de ID, seleccione Adobe ID si el Federated ID de los integrantes del equipo aún no se ha configurado.

   ![](/help/journey-onboarding/assets/assign-team5.png)

1. En la selección Producto, seleccione **Adobe Experience Manager as a Cloud Service** y asigne al usuario el perfil de producto **Deployment Manager** como se muestra a continuación.

   >[!NOTE]
   >Consulte [Cloud Manager product profiles](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/aem-cs-team-product-profiles.html?lang=en#cloud-manager-product-profiles) para asegurarse de que se asignen a los usuarios adecuados las funciones correctas en el Admin Console, como se ve a continuación.

   ![](/help/journey-onboarding/assets/assign-team6.png).

   >[!IMPORTANT]
   >El usuario se puede agregar al perfil de producto de Deployment Manager después de crear los recursos de Cloud Manager.

## Asignar usuarios al perfil de producto del desarrollador {#assign-users-developer}

1. Identifique a los usuarios que administrarán los programas de Cloud Manager y agréguelos al perfil de producto del desarrollador. El administrador del sistema debe ser la primera persona en acceder a Cloud Manager e iniciar sesión en él. Primero debe agregarse (administrador del sistema) al perfil de producto Propietario del negocio .

1. En la página [Admin Console](https://adminconsole.adobe.com/enterprise/overview) **Información general**, seleccione **Adobe Experience Manager as a Cloud Service** producto de la tarjeta **Productos y servicios** como se muestra a continuación.

   ![](/help/journey-onboarding/assets/assign-team1.png)

1. Seleccione la pestaña **Users** en la barra de navegación superior y, a continuación, seleccione **Add User**.

   ![](/help/journey-onboarding/assets/assign-team4.png)

1. En el cuadro de diálogo **Agregar usuarios a su equipo**, escriba el ID de correo electrónico del usuario que desea agregar. Para el tipo de ID, seleccione Adobe ID si el Federated ID de los integrantes del equipo aún no se ha configurado.

   >[!NOTE]
   >Para obtener más información sobre los tipos de identidad en Adobe Admin Console, consulte [Información general de identidad](https://helpx.adobe.com/enterprise/using/identity.html).

   ![](/help/journey-onboarding/assets/assign-team5.png)

1. En la selección Producto, seleccione **Adobe Experience Manager as a Cloud Service** y asigne al usuario el perfil de producto **Developer** como se muestra a continuación.

   >[!NOTE]
   >Consulte [Cloud Manager product profiles](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/aem-cs-team-product-profiles.html?lang=en#cloud-manager-product-profiles) para asegurarse de que se asignen a los usuarios adecuados las funciones correctas en el Admin Console, como se ve a continuación.

   ![](/help/journey-onboarding/assets/assign-team6.png).


   >[!IMPORTANT]
   >El usuario se puede agregar al perfil de producto del desarrollador una vez creados los recursos de Cloud Manager.

## Siguientes pasos {#whats-next}

Ha aprendido sobre tres perfiles de producto de Cloud Manager diferentes, como Propietario empresarial, Administrador de implementación y Desarrollador. A continuación, asignó integrantes del equipo a perfiles de producto de Cloud Manager, como Propietario empresarial, Administrador de implementación y Desarrollador. Ya está listo para continuar con el recorrido de integración revisando el documento [Configuración de recursos de la nube a través de Cloud Manager](/help/journey-onboarding/sysadmin/setup-cloud-resources-via-cloud-manager.md), donde aprenderá:

1. Como administrador del sistema asignado a la función *Propietario empresarial*, debe acceder a Cloud Manager e iniciar sesión en él.

1. A continuación, un usuario de Cloud Manager con la función *Propietario empresarial* puede iniciar sesión y configurar los recursos de la nube, incluidos el programa y los entornos de la nube. Esto garantizará que su equipo de expertos pueda empezar a acceder a AEM como Cloud Service lo antes posible.

1. Una vez que su *Propietario del negocio* haya configurado los recursos de la nube, los *Desarrolladores* y los *Administradores de implementación* que se han agregado correctamente a los perfiles de producto de Cloud Manager pueden acceder a Cloud Manager y familiarizarse con cómo pueden continuar en su ruta de aprendizaje.

## Recursos adicionales {#additional-resources}

Siga los recursos adicionales para obtener más información:

* [Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/cloud-manager-introduction.html?lang=en)
* [Perfiles de producto de Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/aem-cs-team-product-profiles.html?lang=en#cloud-manager-product-profiles)
* [Información general sobre la identidad del Admin Console](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/identity.ug.html)
