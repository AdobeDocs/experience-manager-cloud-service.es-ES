---
title: Acceder a Cloud Manager
description: Obtenga información sobre cómo acceder a Cloud Manager para configurar los recursos del proyecto.
role: Admin, User, Developer
exl-id: c9476ac9-8318-493e-a48d-94ff5a6433a7
feature: Onboarding
source-git-commit: 858a9c4b61fd3a80a257313e48816b067ca77175
workflow-type: tm+mt
source-wordcount: '820'
ht-degree: 94%

---

# Acceder a Cloud Manager {#cloud-resources}

En esta parte del [recorrido de incorporación](overview.md), aprenderá a acceder a Cloud Manager para poder configurar sus recursos de proyecto.

## Objetivo {#objective}

En el artículo anterior de este recorrido de incorporación, [Asignar integrantes del equipo a perfiles de producto de Cloud Manager](assign-profiles-cloud-manager.md), ha concedido a su equipo de AEMaaCS las funciones adecuadas. Ahora aprenda a acceder a Cloud Manager para configurar los recursos de su proyecto que su equipo tiene previsto utilizar.

Desde que ha completado el paso anterior en este recorrido, su equipo puede acceder a Cloud Manager. Cloud Manager se utiliza para crear y administrar los recursos de sus proyectos, como programas y entornos.

Después de leer este documento, debería poder comprender lo siguiente:

* Que un administrador del sistema asignado a la función **Propietario empresarial** debe ser la primera persona en su organización en iniciar sesión y acceder a Cloud Manager.
* Iniciar sesión en Cloud Manager.

## Cloud Manager {#cloud-manager}

Cloud Manager es un componente esencial de AEM as a Cloud Service y sirve como punto de entrada único para su equipo. Admite clientes con configuraciones de desarrollo empresarial con sus CI/CD Pipelines creadas específicamente, que están equipadas para garantizar pruebas exhaustivas y la máxima calidad de código para ofrecer experiencias excepcionales. Cloud Manager proporciona todo lo necesario para comenzar en forma de autoservicio, incluida la capacidad de crear los recursos y entornos de la nube.

Normalmente, un miembro del equipo asignado al perfil de producto **Propietario empresarial** es responsable de añadir los recursos de la nube, como programas y entornos. Esta persona comprende las necesidades comerciales y completa la configuración inicial de Cloud Manager.

A efectos de este recorrido de incorporación, usted, como administrador del sistema, ya se ha asignado el perfil de producto **Propietario empresarial** y configurará los recursos de la nube. Dependiendo de los requisitos reales del proyecto, los propietarios del negocio pueden ser o no iguales que el administrador del sistema.

## Acceder a Cloud Manager como administrador del sistema y propietario empresarial {#access-sysadmin-bo}

Antes de los integrantes del equipo que usted asignó a la función **Propietario del negocio** puede acceder a Cloud Manager y empezar a crear recursos en la nube, el administrador del sistema debe tener asignada la función **Propietario del negocio**. También deben iniciar sesión en Cloud Manager como lo hizo en el paso anterior en este recorrido de incorporación.

1. Asegúrese de que, como administrador del sistema, tiene la función **Propietario empresarial** asignada.

   Regrese al paso anterior de este recorrido, [Asignar integrantes del equipo a perfiles de producto de Cloud Manager](assign-profiles-cloud-manager.md), para obtener detalles sobre cómo asignar la función **Propietario del negocio** al administrador del sistema.

1. Inicie sesión en Cloud Manager en [experience.adobe.com](https://experience.adobe.com).
1. En la agrupación Acceso rápido, haga clic en **Experience Manager**.
1. En el panel lateral izquierdo, haga clic en **Cloud Manager**.

   ![Cloud Manager en consola](/help/journey-onboarding/assets/consol-cloud-manager.png)

Un administrador del sistema con el rol **Propietario del negocio** debe iniciar sesión en Cloud Manager primero. Este inicio de sesión inicial permite a otros usuarios con la función **Propietario empresarial** crear programas; no aparece ninguna confirmación.

<!--
By successfully signing in as a system administrator with the **Business Owner** role, you use Cloud Manager for use by the other users with the **Business Owner** role. You do not receive a confirmation or any message. Simply signing in is sufficient.

Until you sign in to Cloud Manager as a system administrator with the **Business Owner** role, other users with the **Business Owner** role cannot create programs in Cloud Manager. This rule is true even if they are assigned the correct roles. -->

## Navegar a Cloud Manager {#navigate-cloud-manager}

1. Vaya a [experience.adobe.com/experiencemanager](https://experience.adobe.com/experiencemanager).
1. En el panel lateral izquierdo, haga clic en **Cloud Manager**.

>[!NOTE]
>
>Según las funciones asignadas en Cloud Manager y el estado de la aplicación, verá diferentes pantallas mientras utiliza la interfaz de usuario de Cloud Manager.

<!--
Users with the **Business Owner** role receive a welcome email with a link to get started. Follow the steps below to navigate to Cloud Manager using this welcome email.

1. From your welcome email, click **Get started**, as shown in the figure below.
    ![Email example](/help/journey-onboarding/assets/get-started-email.png)

1. Navigate to Cloud Manager's **Programs & Products** page.

   >[!TIP]
   >
   >You can also navigate directly to Cloud Manager's login page from `[my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/)`. Bookmark this page for future reference.

1. You are directed to Cloud Manager's landing page. -->

<!-- OLD
Alternatively, you can navigate to Cloud Manager's **Programs and Products** page from the Adobe Experience Cloud home page using these steps.

1. Navigate directly to [Adobe Experience Cloud](https://experience.adobe.com) and login using your Adobe ID.

1. From the Adobe Experience Cloud home page, select **Experience Manager** to open the AEM home page.

   ![Experience Cloud homepage](/help/journey-onboarding/assets/setup-resources2.png)

1. On the **Cloud Manager** tile, select **Launch**.

   ![AEM home page](/help/journey-onboarding/assets/setup-resources3.png)

1. After successfully logging on, you are directed to the Cloud Manager landing page. See [Viewing Cloud Manager's Programs](#viewing-programs) for more details.

How you access your programs and products via Cloud Manager is up to you and has no effect on how you use Cloud Manager or how you manage your programs.

>[!NOTE]
>
>Depending on the roles assigned in Cloud Manager and the state of the application, you see different screens while using the Cloud Manager user interface. -->

## Ver programas {#viewing-programs}

Una vez que acceda correctamente a Cloud Manager, lo que vea dependerá del estado de sus programas, tal como se detalla en las secciones siguientes.

### Cuando no existen programas {#no-programs}

Si su organización no cuenta con ningún programa, la página de destino le indicará que cree su primer programa.

![Sin programas](/help/journey-onboarding/assets/cloud-manager-programs-do-not-exist.png)

### Cuando los programas ya existen {#programs-exist}

Si los programas ya existen en su organización, la página de destino muestra los programas existentes y también ofrece un botón para agregar programas adicionales.

![Existen programas](/help/journey-onboarding/assets/cloud-manager-programs-exist.png)

### Cuando existe un programa y usted es administrador del sistema {#programs-exist-sysadmin}

Si los programas ya existen en su organización y usted es administrador del sistema, su página de destino incluye el botón **Administrar acceso** junto con la opción **Añadir programa**.

![Vista del administrador del sistema](/help/journey-onboarding/assets/cloud-manager-programs-as-sysadmin.png)

## Verificación de las funciones del usuario {#verify-user-roles}

Una vez haya iniciado sesión correctamente en Cloud Manager, puede verificar que se le ha asignado el perfil de producto **Propietario de la empresa**.

1. Cerca de la esquina superior derecha de la página, haga clic en el icono **Cuenta**.

1. Haga clic en **Funciones de usuario**.

   ![Roles del usuario](/help/journey-onboarding/assets/cloud-manager-user-roles.png)

1. En el cuadro de diálogo **Funciones de usuario**, confirme que el usuario tiene la función **Propietario de la empresa**.

   ![Lista de funciones de usuario](/help/journey-onboarding/assets/cloud-manager-user-roles-business-owner.png)

Ha iniciado sesión correctamente en Cloud Manager como Propietario de la empresa. Si no tiene asignada la función **Propietario empresarial**, póngase en contacto con el administrador del sistema.

## Siguientes pasos {#whats-next}

Ahora que puede acceder a Cloud Manager como administrador del sistema, está listo para crear su primer programa.

Debe continuar con su recorrido de incorporación revisando el documento [Crear un programa](create-program.md) donde aprenderá a hacerlo.

## Recursos adicionales {#additional-resources}

Los siguientes son recursos opcionales adicionales si desea ir más allá del contenido del recorrido de incorporación.

* [Introducción a Cloud Manager](/help/onboarding/cloud-manager-introduction.md): 
Obtenga información sobre Cloud Manager, los programas de Cloud Manager y los entornos.
* [Perfiles de producto y equipo de AEM as a Cloud Service](/help/onboarding/aem-cs-team-product-profiles.md): aprenda cómo los perfiles de producto y equipo de AEM as a Cloud Service pueden conceder y limitar el acceso a sus soluciones con licencia de Adobe.
<!-- ERROR: Not Found (HTTP error 404) * [AEM Champion Tips and Tricks - Cloud Manager UI](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/expert-resources/aem-champions/cloud-manager-ui.md) - Watch this video for an overview of Cloud Manager's UI from an AEM champion. -->
