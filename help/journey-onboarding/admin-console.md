---
title: Acceso al Admin Console
description: Una vez que haya comprendido la preparación necesaria para la incorporación y los conceptos básicos de la estructura de AEMaaCS, ya puede iniciar sesión en el Admin Console por primera vez.
exl-id: 0ccce328-a356-4ba9-b7fe-f67abc25b924
source-git-commit: 097c17b37cc308dc906cd4af7dc7c5d51862bdfa
workflow-type: tm+mt
source-wordcount: '1092'
ht-degree: 2%

---

# Acceso al Admin Console {#accessing-admin-console}

En esta parte del [recorrido de incorporación,](overview.md) aprenderá sobre la preparación necesaria para poder iniciar sesión en el sistema por primera vez.

## Objetivo {#objective}

Ahora que ha leído el artículo [Terminología as a Cloud Service AEM](terminology.md) y comprenda los conceptos básicos de la estructura de AEMaaCS, ya estará listo para iniciar sesión en el Admin Console por primera vez.

Como administrador del sistema, usted es responsable de administrar los usuarios dentro de su organización. Para ello, utilice el Admin Console . Después de leer esta sección debe:

* Comprenda lo que es un Adobe ID.
* Inicie sesión en el Admin Console.
* Obtenga información sobre cómo revisar sus privilegios como administrador del sistema a través del Admin Console.
* Obtenga información sobre cómo ponerse en contacto con el servicio de asistencia técnica de Adobe para obtener ayuda.

## El Admin Console {#admin-console}

Adobe Admin Console es un lugar central para administrar las licencias y los usuarios de productos de Adobe. El Admin Console le permite crear y administrar usuarios en una sola ubicación en lugar de en las distintas soluciones individuales.

## Adobe ID {#adobe-id}

Para iniciar sesión en el Admin Console, necesitará un Adobe ID. Y Adobe ID es una cuenta ligada a una dirección de correo electrónico específica que es necesaria para iniciar sesión y acceder a AEM as a Cloud Service o a cualquiera de sus soluciones de Adobe. Al usar su Adobe ID usted mantiene todos sus planes de Adobe y productos asociados a una sola cuenta.

Cuando usted como administrador del sistema configura su equipo en el Admin Console, usted especifica la dirección de correo electrónico que se utilizará como Adobe ID.

Existen tres tipos de ID de Adobe:

* **ID personal**: Este es el tipo predeterminado de Adobe ID y se crea en adobe.com. Esta cuenta es administrada por Adobe y cualquiera puede crear una cuenta de este tipo.

* **Enterprise ID**: Las organizaciones generalmente desean aumentar el control de las cuentas de usuario. Solo los administradores del sistema pueden crear Enterprise ID y la organización posee estas cuentas con Adobe que solo sirve como host.

* **Federated ID**: Con los Federated ID, la organización asume la propiedad y el control totales de las cuentas. Para ello, su organización debe integrar Adobe Experience Cloud con su sistema de inicio de sesión único (SSO) de SAML2. Esto permite a los usuarios autenticarse en el sistema SSO de su organización en lugar de en una cuenta alojada por Adobe.

Como administrador del sistema, puede decidir incorporarse a usted y a su equipo en AEM as a Cloud Service mediante el uso de ID personales antes de que se configuren Enterprise ID o Federated ID. Una vez configurados los Enterprise ID o Federated ID, los miembros pueden pasar a utilizar esos ID.

## Inicio de sesión en el Admin Console {#steps-admin-console}

Antes de poder usar el Admin Console para administrar usuarios dentro de su equipo, debe asegurarse de que puede acceder a él correctamente y de que dispone de los permisos adecuados.

1. Como administrador del sistema, recibirá varios correos electrónicos de Adobe como parte del proceso de incorporación. Busque el correo electrónico de bienvenida que proporciona la información sobre el nombre de la organización a la que se le ha concedido acceso.

1. Haga clic en el **Introducción** en el correo electrónico de bienvenida para ir al Admin Console. Si no encuentra el correo electrónico, abra un explorador directamente al Admin Console en [`https://adminconsole.adobe.com`](https://adminconsole.adobe.com).

   ![Correo electrónico de bienvenida](/help/journey-onboarding/assets/get-started-email.png)

1. Inicie sesión con su Adobe ID. Una vez que inicie sesión correctamente, verá la variable **Información general** de Adobe Admin Console.

   ![El Admin Console](/help/journey-onboarding/assets/get-started1.png)

1. Si tiene acceso a varias organizaciones, asegúrese de haber iniciado sesión en la organización correcta. Para cambiar su organización, haga clic en el nombre de la organización en la esquina superior derecha y elija la organización a la que necesita acceder.

   ![Cambiar organización](/help/journey-onboarding/assets/admin-console-orgswitch.png)

1. Select **Administradores** de la variable **Usuarios** para comprobar que es administrador del sistema.

   ![Revise los administradores](/help/journey-onboarding/assets/get-started2.png)

1. Una vez que haga clic en **Administradores** de la variable **Usuarios** , puede buscar introduciendo el correo electrónico, el nombre de usuario, el nombre o los apellidos de Adobe ID.

   ![Buscar usuarios](/help/journey-onboarding/assets/get-started3.png)

1. Si todo funciona correctamente, la búsqueda devolverá su registro. Si el valor de la variable **FUNCIÓN DE ADMINISTRADOR** muestra columnas **Sistema**, sabe que usted (o el usuario mostrado) es un administrador del sistema.

   ![Estado del sistema](/help/journey-onboarding/assets/get-started4.png)

¡Felicidades, administrador del sistema!

## Sistema Identity Management de Adobe {#ims}

AEM as a Cloud Service viene preconfigurado con el sistema Identity Management de Adobe (también conocido como IMS) para la autenticación. No es necesario que haga nada como administrador del sistema para habilitarlo.

Al utilizar IMS, AEM as a Cloud Service consolida la experiencia de inicio de sesión entre AEM y el resto de Adobe Experience Cloud. Las organizaciones con varios productos de Adobe se benefician especialmente al crear grupos basados en funciones en el Admin Console y luego asignar acceso a varios productos, incluido AEM as a Cloud Service mediante IMS.

En la siguiente parte de este recorrido de integración, obtendrá más información sobre los perfiles de producto y la asignación de usuarios.

## Contactar con el servicio de asistencia al Adobe {#support}

Si tiene algún problema, se puede acceder a la asistencia de Adobe a través del Admin Console . La variable **Asistencia** permite acceder a varias funciones de soporte de Adobe a través de una interfaz sencilla y fácil de usar.

![Pestaña Asistencia](/help/journey-onboarding/assets/support-menu.png)

La pestaña le permite crear y administrar casos, chatear directamente con los representantes de asistencia al cliente de Adobe y programar sesiones con expertos. Los administradores de sistemas y los administradores de asistencia técnica deben iniciar sesión para acceder a los casos de asistencia técnica y a las opciones de sesión de expertos.

## Siguientes pasos {#whats-next}

Ahora que ha leído este documento, debe:

* Comprender qué es y Adobe ID.
* Inicie sesión en el Admin Console.
* Obtenga información sobre cómo revisar sus privilegios como administrador del sistema a través del Admin Console.
* Obtenga información sobre cómo ponerse en contacto con el servicio de asistencia técnica de Adobe para obtener ayuda.

Está listo para continuar con su recorrido de incorporación aprendiendo a [asignar miembros del equipo a perfiles de producto de Cloud Manager](assign-profiles-cloud-manager.md) para que sus compañeros también puedan acceder a AEMaaCS.

## Recursos adicionales {#additional-resources}

* [Información general del Admin Console](https://helpx.adobe.com/es/enterprise/using/admin-console.html) - Una visión general del Admin Console
* [Crear o actualizar su Adobe ID](https://helpx.adobe.com/ca/manage-account/using/create-update-adobe-id.html#HowtocreateorupdateyourAdobeID) : Obtenga información sobre cómo crear una Adobe ID, cambiarla y administrar varios ID de Adobe.
* [Gestor de autenticación SAML 2.0](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/saml-2-0-authenticationhandler.html) - AEM se envía con un controlador de autenticación SAML. Este controlador proporciona compatibilidad con el protocolo de solicitud de autenticación SAML 2.0 (perfil Web-SSO) mediante el enlace del POST HTTP.
* [Funciones administrativas](https://helpx.adobe.com/enterprise/using/admin-roles.ug.html) - Con Adobe Admin Console, las organizaciones pueden definir una jerarquía administrativa flexible que permita una gestión precisa del acceso y uso de los productos de Adobe.
* [Sesiones de expertos y de asistencia](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/support-for-experience-cloud.ug.html) - Aprenda a acceder a las opciones de asistencia del Admin Console, administrar sus casos de asistencia, programar una sesión de expertos y mucho más.
