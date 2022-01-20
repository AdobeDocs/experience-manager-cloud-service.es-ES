---
title: Configuración de recursos de Cloud mediante Cloud Manager
description: Siga esta página para obtener información sobre cómo configurar los recursos de Cloud a través de Cloud Manager
role: Admin, User, Developer
exl-id: de3a33b7-b459-4e47-b232-a0f88e2ce22e
source-git-commit: 7fe39bbc8d5e965af7f339b2a524420c76360552
workflow-type: tm+mt
source-wordcount: '1246'
ht-degree: 0%

---

# Configuración de recursos de Cloud mediante Cloud Manager {#setup-cloud-resources}

El administrador del sistema asignado a la función Propietario empresarial debe acceder a Cloud Manager e iniciar sesión en él. A continuación, un miembro del equipo asignado al perfil de producto Propietario empresarial debe iniciar sesión en Cloud Manager y crear el programa y los entornos de la nube para que su equipo de expertos pueda empezar.

## Objetivo {#objective}

Este documento le ayuda a comprender cómo se crean los recursos de la nube y quién puede hacerlo.

Después de leer esta sección debe comprender:

* Un administrador del sistema asignado a la función Propietario empresarial debe ser el primero en acceder a Cloud Manager e iniciar sesión en él.
* Cómo se crean el programa y los entornos de la nube.

## Introducción {#introduction}

La adición de recursos de nube se realiza mediante Cloud Manager a través de un miembro del equipo asignado al perfil de producto de Cloud Manager Business Owner. Normalmente, esta persona comprende las necesidades comerciales y completa la configuración inicial de Cloud Manager.

Siga las secciones a continuación para aprender a crear su [programas de servicios en la nube](#create-cloud-service-program) y [entornos.](#create-cloud-environments)

### Requisitos previos {#prerequisites}

* El administrador del sistema asignado a la función Propietario empresarial debe acceder a Cloud Manager e iniciar sesión en él.

* Explicación de cómo [desplácese e inicie sesión en Cloud Manager.](/help/onboarding/learn-concepts/cloud-manager-introduction.md)

* Familiarícese con [Perfiles de producto de Cloud Manager.](/help/onboarding/learn-concepts/aem-cs-team-product-profiles.md#cloud-manager-product-profiles)

* Comprender los conceptos de Cloud Manager [programas](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/understand-program-types.md) y [entornos.](/help/implementing/cloud-manager/manage-environments.md)

## Vaya a Cloud Manager {#navigate-cloud-manager}

El usuario propietario del negocio recibirá un correo electrónico de bienvenida con un vínculo para empezar, o si no puede encontrarlo, acceda a [Cloud Manager](https://my.cloudmanager.adobe.com/) directamente iniciando sesión con su Adobe ID.

Siga los pasos a continuación para ir a Cloud Manager:

1. En el correo electrónico de bienvenida, haga clic en **Introducción**, como se muestra en la figura siguiente.
   ![](/help/journey-onboarding/assets/get-started-email.png)

1. Navegará a la página de Cloud Manager **Programas y productos** página.

   >[!IMPORTANT]
   >
   >También puede navegar directamente a la página de inicio de sesión de Cloud Manager desde [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/). Marque esta página para consultarla en el futuro y para ayudarle a navegar directamente a la página de aterrizaje de Cloud Manager.

1. Se le dirigirá a la página de aterrizaje de Cloud Manager. Consulte [Visualización de los programas de Cloud Manager](#viewing-programs) para obtener más información.

Además, puede navegar hasta el **Programas y productos** de la página de inicio de Adobe Experience Cloud. Complete los siguientes pasos:

1. Vaya directamente a [Adobe Experience Cloud](https://experience.adobe.com) e inicie sesión con su Adobe ID.

1. En la página de inicio de Adobe Experience Cloud, seleccione **Experience Manager**.

   ![](/help/journey-onboarding/assets/setup-resources2.png)

1. Esto lo llevará a la página principal de AEM. Desde aquí, inicie **Cloud Manager** .

   ![](/help/journey-onboarding/assets/setup-resources3.png)

1. Una vez que el inicio de sesión se haya realizado correctamente, se le dirigirá a la página de aterrizaje de Cloud Manager. Consulte [Visualización de los programas de Cloud Manager](#viewing-programs) para obtener más información.

   >[!NOTE]
   >
   >Según las funciones asignadas en [!UICONTROL Cloud Manager] y el estado de la aplicación, verá diferentes pantallas mientras utiliza [!UICONTROL Cloud Manager] IU.

### Visualización de programas en la página de aterrizaje de Cloud Manager {#viewing-programs}

Una vez que el inicio de sesión se haya realizado correctamente, se le dirigirá a la página de aterrizaje de Cloud Manager. Verá una de las tres opciones que se describen a continuación:

#### Cuando no hay programas en Cloud Manager {#no-programs}

Si su organización no cuenta con ningún programa, la página de aterrizaje le indicará que cree su primer programa, tal como se muestra en la figura siguiente.

![](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/first_timelogin0.png)

#### Cuando los programas ya existen en Cloud Manager {#programs-exist}

Si los programas ya existen en su organización, la página de aterrizaje le pedirá que agregue otro programa y también mostrará todos los programas existentes, como se muestra en la figura siguiente.

![](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/first_timelogin1.png)

#### Cuando existe un programa y el usuario es administrador del sistema {#programs-exist-sysadmin}

Si los programas ya existen en su organización y usted es administrador del sistema, se muestra la página de aterrizaje **Administrar acceso** junto con **Agregar programa** , tal como se muestra en la figura siguiente.

![](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/admin-console-4.png)


## Verificación de las funciones de usuario {#verify-user-roles}

Una vez que haya iniciado sesión correctamente en Cloud Manager, siga los pasos a continuación para verificar que se le ha asignado el perfil de producto del propietario empresarial:

1. Seleccione su perfil en la parte superior derecha, como se muestra a continuación.

   ![](/help/journey-onboarding/assets/setup-resources5.png)

1. Select **Funciones del usuario** y asegúrese de que está asignado a Propietario empresarial.

   ![](/help/journey-onboarding/assets/setup-resources6.png)

1. Esto confirma la función de usuario como propietario empresarial.

   ![](/help/journey-onboarding/assets/setup-resources7.png)

   ¡bueno trabajo! Ha iniciado sesión correctamente en Cloud Manager como propietario empresarial.

## Crear programa de Cloud Service {#create-cloud-service-program}

Siga los pasos a continuación para crear su programa de servicios en la nube desde Cloud Manager:

1. Vaya a la página de aterrizaje de Cloud Manager, como se muestra a continuación.

   >[!NOTE]
   >
   >Debe ser un miembro del equipo asignado al perfil de producto Propietario empresarial de Cloud Manager para completar correctamente este paso.

   Desde aquí, haga clic en **Agregar programa** para iniciar el asistente Agregar programa .

   ![](/help/journey-onboarding/assets/setup-resources4.png)

   >[!TIP]
   >
   >Observe el [video](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/programs.html) para aprender a crear su programa AEM as a Cloud y obtener más información sobre consideraciones importantes antes de crear su programa.

   >[!TIP]
   >
   >Para obtener instrucciones paso a paso sobre cómo utilizar el asistente Agregar programa, vaya a [here](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-program.md).

1. Una vez creado correctamente su programa de nube, puede navegar hasta su programa para ver la **Información general** del programa, como se muestra a continuación.

   ![](/help/journey-onboarding/assets/setup-resources8.png)

   >[!NOTE]
   >
   >Si aún no lo ha hecho, es un buen momento para agregar sus miembros de desarrollador a su equipo de Cloud Manager. Consulte Añadir usuarios al perfil de producto del desarrollador y siga los pasos descritos.

1. Los miembros asignados al perfil de producto del desarrollador pueden iniciar sesión en Cloud Manager y [Administrar Git de Cloud Manager](/help/implementing/cloud-manager/managing-code/accessing-repos.md).

   ¡bueno trabajo! Ahora que el programa se ha creado correctamente, el Git de Cloud Manager está disponible para que sus desarrolladores tengan acceso a él.


## Crear entornos de Cloud {#create-cloud-environments}

Una vez que haya creado correctamente su programa de nube, cree sus entornos de nube.

Siga los pasos a continuación para crear los entornos de nube desde Cloud Manager:

1. Vaya al **Información general** página y seleccione **Agregar** de la tarjeta de entorno.

   ![](/help/journey-onboarding/assets/setup-resources9.png)

   >[!IMPORTANT]
   >
   >Un usuario de Cloud Manager con la función Propietario empresarial o Administrador de implementación debe iniciar sesión para completar correctamente este paso.

   Además, observe la [video](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/environments.html) tutorial para obtener más información sobre los entornos de Cloud Manager y cómo puede agregarlos a su programa.

1. Esto iniciará el asistente para agregar entorno que lo guiará a través de la adición de su entorno. Agregue primero su entorno de desarrollo para familiarizarse con el asistente. Consulte [Adición de un entorno](/help/implementing/cloud-manager/manage-environments.md#adding-environments) para obtener más información.

   >[!NOTE]
   >
   >Si aún no lo ha hecho, es un buen momento para agregar sus miembros de desarrollador a su equipo de Cloud Manager. Consulte Añadir usuarios al perfil de producto del desarrollador y siga los pasos descritos.

1. Los miembros asignados al perfil de producto del desarrollador pueden iniciar sesión en Cloud Manager y [Git de Cloud Manager.](/help/implementing/cloud-manager/managing-code/accessing-repos.md)

   ¡bueno trabajo! Ahora su programa se ha creado correctamente y su Git de Cloud Manager está disponible para que sus desarrolladores tengan acceso a él.

   Felicitaciones! Ahora, los entornos de sus programas de nube se han creado y los desarrolladores se han añadido al equipo.

## Siguientes pasos {#whats-next}

Los miembros del equipo deben tener permisos para la instancia, ya que los permisos para administrar Cloud Manager no serán suficientes. Ahora que los recursos de la nube se han creado y están listos para que su equipo los pueda acceder, el administrador del sistema debe asignar a los integrantes del equipo AEM perfiles de producto as a Cloud Service de Adobe Admin Console.

>[!NOTE]
>
>Para que se le conceda acceso a AEM usuarios as a Cloud Service, debe pertenecer a uno de los dos perfiles de producto `AEM Users` o `AEM Administrators`. Consulte [Administración de productos y acceso de usuarios en Admin Console](/help/security/ims-support.md#managing-products-and-user-access-in-admin-console) para obtener más información.

Debe continuar con su recorrido de incorporación revisando el documento [Asignación de miembros del equipo a AEM perfiles de producto as a Cloud Service.](/help/journey-onboarding/sysadmin/assign-team-members-aem-cloud-service.md)


## Recursos adicionales {#additional-resources}

Siga los recursos adicionales para obtener más información:

* [Tipos de programas y adición de un programa](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/programs.html)
* [Tipos de entorno y adición de un entorno](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/environments.html)
* [Administración de Git de Cloud Manager](/help/implementing/cloud-manager/managing-code/accessing-repos.md)
* [Configuración del acceso a AEM as a Cloud Service desde el Admin Console](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/accessing/overview.html#adobe-ims-users)
