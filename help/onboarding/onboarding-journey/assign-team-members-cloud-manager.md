---
title: 'Asignación de miembros del equipo a perfiles de producto de Cloud Manager '
description: Siga esta página para obtener información sobre cómo asignar miembros del equipo a perfiles de producto de Cloud Manager
hide: true
hidefromtoc: true
index: false
source-git-commit: 57b29f8ef6c65b5a752aca680557e75ba55f64bd
workflow-type: tm+mt
source-wordcount: '1299'
ht-degree: 0%

---


# Asignación de miembros del equipo a perfiles de producto de Cloud Manager {#assign-team-members}

Una vez que haya aprendido a iniciar sesión en [Admin Console](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/admin-console.html?lang=en) y haya visto sus privilegios como [administrador del sistema](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/system-administrator.html?lang=en), ya está listo para asignar miembros del equipo a perfiles de producto de Cloud Manager.

## Objetivo {#objective}

Este documento resume cómo asignar miembros del equipo a perfiles de producto de Cloud Manager desde el Admin Console.

Después de leer esta sección debe poder:

* Comprenda por qué y cómo debe agregar miembros del equipo.
* Obtenga información sobre tres perfiles de producto de Cloud Manager diferentes, como Propietario empresarial, Administrador de implementación y Desarrollador.
* Asigne integrantes del equipo a perfiles de producto de Cloud Manager, como Propietario empresarial, Administrador de implementación y Desarrollador.

## Requisitos previos {#prerequisites}

Los siguientes requisitos previos deben tenerse en cuenta antes de iniciar esta sección. Debe ser:

* Un administrador del sistema y conozca [Cloud Manager Product Profiles](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/aem-cs-team-product-profiles.html?lang=en#cloud-manager-product-profiles).
* Comprenden los conceptos básicos de [Adobe Admin Console](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/admin-console.html?lang=en).
* Debe tener detalles sobre los integrantes del equipo. Un administrador del sistema debe tener los nombres y las direcciones de correo electrónico, así como las funciones y responsabilidades de los integrantes del equipo que necesitan acceder a AEM como Cloud Service.

   >[!NOTE]
   >Con el fin de incorporarlo, le recomendamos que agregue inicialmente usuarios que participarán en las tareas inmediatas, como administradores, desarrolladores y autores de contenido. Puede continuar con el resto de la incorporación sin agregar todos los usuarios. Una vez que haya terminado la incorporación, puede escalar a un mayor número de usuarios más adelante.

## Revisión de los perfiles de producto de Cloud Manager {#review-product-profiles}

Desde el Admin Console puede ver la lista de perfiles de Cloud Manager.

>[!NOTE]
>Antes de revisar los perfiles de producto de Cloud Manager de Admin Console, se recomienda revisar los [Perfiles de producto de Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/aem-cs-team-product-profiles.html?lang=en#cloud-manager-product-profiles) disponibles.

Siga los pasos a continuación para ver la lista de perfiles de Cloud Manager:

1. Inicie sesión en [Adobe Admin Console](https://adminconsole.adobe.com/). En la página **Información general**, seleccione **Adobe Experience Manager as a Cloud Service** en la tarjeta **Productos y servicios**.

   ![](/help/onboarding/onboarding-journey/assets/assign-team1.png)

   >[!NOTE]
   >Consulte Inicio de sesión en Admin Console para obtener información sobre cómo utilizar Admin Console.


1. Vaya a la instancia **Cloud Manager** de la tabla con la lista de todas las instancias.

   ![](/help/onboarding/onboarding-journey/assets/assign-team2.png)

1. Verá la lista de perfiles de producto preconfigurados de [Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/aem-cs-team-product-profiles.html?lang=en#cloud-manager-product-profiles).

   ![](/help/onboarding/onboarding-journey/assets/assign-team3.png)


## Asignación de usuarios al perfil de producto del propietario empresarial {#assign-users-business-owner}

Ya está listo para agregar usuarios y asignarlos al perfil de producto Propietario empresarial de Cloud Manager.

Para hacerlo correctamente, desde Admin Console de Adobe debe agregar un usuario al producto (AEM como Cloud Service en este caso) y al perfil de producto Propietario empresarial de Cloud Manager.

Los siguientes pasos le guían a través de esto:

1. Identifique a los usuarios que administrarán los programas de Cloud Manager y agréguelos al perfil de producto Propietario empresarial . El administrador del sistema debe ser la primera persona en acceder a Cloud Manager e iniciar sesión en él. Primero debe agregarse (administrador del sistema) al perfil de producto Propietario empresarial .

1. En la página Información general de Admin Console , seleccione Adobe Experience Manager como producto Cloud Service en la tarjeta de productos y servicios como se muestra a continuación:

1. Seleccione la ficha Usuarios en la barra de navegación superior y, a continuación, seleccione Agregar usuario.

1. En el cuadro de diálogo agregar usuario, escriba el ID de correo electrónico del usuario que desea agregar. Para el tipo de ID, seleccione Adobe ID si el Federated ID de los integrantes del equipo aún no se ha configurado.

1. En la selección de productos, seleccione &quot;Adobe Experience Manager como Cloud Service&quot; y asigne al usuario el perfil de producto &quot;Propietario empresarial&quot;, como se muestra a continuación. Consulte los perfiles de producto de Cloud Manager para asegurarse de que se asignan las funciones correctas a los usuarios adecuados en el Admin Console, como se ve a continuación.

1. Asigne el usuario al menos a un perfil de producto para que el usuario pueda acceder a Cloud Manager. Recuerde asignarse (administrador del sistema) a &quot;Propietario empresarial&quot;.

1. Haga clic en Guardar. Se envía un correo electrónico de bienvenida al usuario que ha añadido. El usuario invitado puede acceder a Cloud Manager haciendo clic en el vínculo del correo electrónico de bienvenida e iniciando sesión con su Adobe ID.

Felicitaciones! Ahora, se ha configurado su nuevo equipo de Cloud Manager, incluido el que se ha asignado a la función &quot;Propietario empresarial&quot;. Los miembros recibirán un correo electrónico de bienvenida en el que se les invitará a iniciar sesión y acceder a Cloud Manager. En la función Propietario empresarial, ahora está a un paso de iniciar sesión en Cloud Manager y de habilitar la creación de los recursos de la nube.

## Asignación de usuarios al perfil de producto del administrador de implementación {#assign-users-deployment-manager}

1. Identifique a los usuarios que administrarán los programas de Cloud Manager y agréguelos al perfil de producto Propietario empresarial . El administrador del sistema debe ser la primera persona en acceder a Cloud Manager e iniciar sesión en él. Primero debe agregarse (administrador del sistema) al perfil de producto Propietario empresarial .

1. En la página Información general de Admin Console , seleccione Adobe Experience Manager como producto Cloud Service en la tarjeta de productos y servicios como se muestra a continuación:

1. Seleccione la ficha Usuarios en la barra de navegación superior y, a continuación, seleccione Agregar usuario.

1. En el cuadro de diálogo agregar usuario, escriba el ID de correo electrónico del usuario que desea agregar. Para el tipo de ID, seleccione Adobe ID si el Federated ID de los integrantes del equipo aún no se ha configurado.

1. En la selección de productos, seleccione &quot;Adobe Experience Manager como Cloud Service&quot; y asigne el perfil de producto &quot;Gestor de implementación&quot; al usuario, como se muestra a continuación. Consulte los perfiles de producto de Cloud Manager para asegurarse de que se asignan las funciones correctas a los usuarios adecuados en el Admin Console, como se ve a continuación.

   >[!NOTE]
   >El usuario se puede agregar al perfil de producto de Deployment Manager después de crear los recursos de Cloud Manager.

## Asignación de usuarios al perfil de producto del desarrollador {#assign-users-developer}

1. Identifique a los usuarios que administrarán los programas de Cloud Manager y agréguelos al perfil de producto Propietario empresarial . El administrador del sistema debe ser la primera persona en acceder a Cloud Manager e iniciar sesión en él. Primero debe agregarse (administrador del sistema) al perfil de producto Propietario empresarial .

1. En la página Información general de Admin Console , seleccione Adobe Experience Manager como producto Cloud Service en la tarjeta de productos y servicios como se muestra a continuación:

1. Seleccione la ficha Usuarios en la barra de navegación superior y, a continuación, seleccione Agregar usuario.

1. En el cuadro de diálogo agregar usuario, escriba el ID de correo electrónico del usuario que desea agregar. Para el tipo de ID, seleccione Adobe ID si el Federated ID de los integrantes del equipo aún no se ha configurado.

1. En la selección de productos, seleccione &quot;Adobe Experience Manager como Cloud Service&quot; y asigne el perfil de producto &quot;Desarrollador&quot; al usuario, como se muestra a continuación. Consulte los perfiles de producto de Cloud Manager para asegurarse de que se asignan las funciones correctas a los usuarios adecuados en el Admin Console, como se ve a continuación.

   >[!NOTE]
   >El usuario se puede agregar al perfil de producto del desarrollador una vez creados los recursos de Cloud Manager.

## Siguientes pasos {#whats-next}

Como administrador del sistema asignado a la función *Propietario empresarial*, debe acceder a Cloud Manager e iniciar sesión en él.
>[!NOTE]
>Consulte [Navegación a Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/what-is-required/navigate-to-cloud-manager.html?lang=en) para obtener información sobre cómo iniciar sesión y acceder a Cloud Manager.

Un usuario de Cloud Manager con la función Propietario empresarial puede iniciar sesión y configurar los recursos de la nube, incluidos los programas y los entornos. Esto garantizará que su equipo de expertos pueda empezar a acceder a AEM como Cloud Service lo antes posible.
Una vez que su propietario empresarial haya configurado los recursos de la nube, los desarrolladores y los administradores de implementación que se hayan agregado correctamente a los perfiles de producto de Cloud Manager podrán acceder a Cloud Manager y familiarizarse con cómo pueden continuar en su ruta de aprendizaje.

## Recursos adicionales {#additional-resources}

Siga los recursos adicionales para obtener más información:

* Cloud Manager
* Perfiles de producto de Cloud Manager
* Información general sobre la identidad del Admin Console
