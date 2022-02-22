---
title: Configuración de recursos de la nube mediante Cloud Manager
description: Aprenda a utilizar Cloud Manager para configurar y administrar sus propios recursos en la nube.
role: Admin, User, Developer
exl-id: de3a33b7-b459-4e47-b232-a0f88e2ce22e
source-git-commit: 0db24518610fccf0d2ea5e0620a0c6a5f8009ea8
workflow-type: tm+mt
source-wordcount: '1369'
ht-degree: 1%

---

# Configuración de recursos de la nube mediante Cloud Manager {#setup-cloud-resources}

Aprenda a utilizar Cloud Manager para configurar y administrar sus propios recursos en la nube.

## Objetivo {#objective}

Este documento le ayuda a comprender cómo se crean los recursos de la nube y quién los puede crear. Después de leer esta sección debe comprender:

* Un administrador del sistema asignado al **Propietario empresarial** debe ser la primera en su organización en iniciar sesión y acceder a Cloud Manager.
* Cómo se crean el programa y los entornos de la nube.

## Introducción {#introduction}

La adición de los recursos de la nube se realiza mediante Cloud Manager a través del miembro del equipo asignado a la función **Propietario empresarial** perfil de producto. Normalmente, esta persona comprende las necesidades comerciales y completa la configuración inicial de Cloud Manager.

Siga las secciones a continuación para aprender a crear su [programas de servicios en la nube](#create-cloud-service-program) y [entornos.](#create-cloud-environments)

### Requisitos previos {#prerequisites}

* El administrador del sistema asignado al **Propietario empresarial** debe haber iniciado sesión en Cloud Manager antes que en cualquier otro usuario con **Propietario empresarial** intenta acceder a Cloud manager para realizar los pasos descritos en este documento.

   * Vuelva a la [Asignar miembros del equipo a perfiles de producto de Cloud Manager](/help/journey-onboarding/sysadmin/assign-team-members-cloud-manager.md) documento de este recorrido para obtener más información.

* Debe comprender cómo [desplácese e inicie sesión en Cloud Manager.](/help/onboarding/learn-concepts/cloud-manager-introduction.md)

* Debe estar familiarizado con [Perfiles de producto de Cloud Manager.](/help/onboarding/learn-concepts/aem-cs-team-product-profiles.md#cloud-manager-product-profiles)

* Debe comprender los conceptos de Cloud Manager [programas](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/program-types.md) y [entornos.](/help/implementing/cloud-manager/manage-environments.md)

## Acceso a Cloud Manager como administrador del sistema y propietario empresarial {#access-sysadmin-bo}

Antes de los integrantes del equipo que asignó al **Propietario empresarial** La función puede acceder a cloud manager y comenzar a crear recursos en la nube, debe asignarse al administrador del sistema la función **Propietario empresarial** e inicie sesión en Cloud Manager.

1. Asegúrese de que, como administrador del sistema, tiene la variable **Propietario empresarial** función asignada.

   * Regrese al paso anterior de este recorrido, [Asignar miembros del equipo a perfiles de producto de Cloud Manager,](/help/journey-onboarding/sysadmin/assign-team-members-cloud-manager.md) para obtener más información sobre cómo asignar la variable **Propietario empresarial** al administrador del sistema si aún no lo ha hecho.

1. Inicie sesión en Cloud Manager en [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) y se le presentará con la página de aterrizaje normal.

Al iniciar sesión correctamente como administrador del sistema con el **Propietario empresarial** , inicialice Cloud Manager para que lo utilicen los demás usuarios con la función **Propietario empresarial** función. No recibirá ninguna confirmación de este mensaje ni de ningún otro. Simplemente, iniciar sesión es suficiente.

Hasta que inicie sesión en Cloud Manager como administrador del sistema con el **Propietario empresarial** , otros usuarios con la función **Propietario empresarial** no podrá crear programas en Cloud Manager aunque se les asignen las funciones correctas.

## Vaya a Cloud Manager {#navigate-cloud-manager}

El usuario con la variable **Propietario empresarial** recibirá un correo electrónico de bienvenida con un vínculo para empezar. Siga los pasos a continuación para navegar a Cloud Manager mediante este correo electrónico de bienvenida.

1. En el correo electrónico de bienvenida, haga clic en **Introducción**, como se muestra en la figura siguiente.
   ![Ejemplo de correo electrónico](/help/journey-onboarding/assets/get-started-email.png)

1. Navegará a la página de Cloud Manager **Programas y productos** página.

   >[!TIP]
   >
   >También puede navegar directamente a la página de inicio de sesión de Cloud Manager desde [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/). Marque esta página para referencia futura.

1. Se le dirigirá a la página de aterrizaje de Cloud Manager. Consulte [Visualización de los programas de Cloud Manager](#viewing-programs) para obtener más información.

También puede navegar hasta el **Programas y productos** en la página de inicio de Adobe Experience Cloud siguiendo estos pasos

1. Vaya directamente a [Adobe Experience Cloud](https://experience.adobe.com) e inicie sesión con su Adobe ID.

1. En la página de inicio de Adobe Experience Cloud, seleccione **Experience Manager**.

   ![página principal del Experience Cloud](/help/journey-onboarding/assets/setup-resources2.png)

1. Esto lo llevará a la página principal de AEM. Desde aquí, haga clic en **Launch** en el **Cloud Manager** mosaico.

   ![AEM página principal](/help/journey-onboarding/assets/setup-resources3.png)

1. Una vez que el inicio de sesión se haya realizado correctamente, se le dirigirá a la página de aterrizaje de Cloud Manager. Consulte [Visualización de los programas de Cloud Manager](#viewing-programs) para obtener más información.

La forma de acceder a sus programas y productos a través de Cloud Manager depende de usted y no tiene ningún efecto en cómo utiliza Cloud Manager ni en cómo administra sus programas.

>[!NOTE]
>
>Según las funciones asignadas en [!UICONTROL Cloud Manager] y el estado de la aplicación, verá diferentes pantallas mientras utiliza [!UICONTROL Cloud Manager] IU.

### Visualización de programas {#viewing-programs}

Una vez que acceda correctamente a Cloud Manager, lo que vea dependerá del estado de sus programas, tal como se detalla en las secciones siguientes.

#### Cuando no existen programas {#no-programs}

Si su organización no cuenta con ningún programa, la página de aterrizaje le indicará que cree su primer programa.

![Sin programas](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/first_timelogin0.png)

#### Cuando los programas ya existen {#programs-exist}

Si los programas ya existen en su organización, la página de aterrizaje muestra los programas existentes y también ofrece un botón para agregar programas adicionales.

![Existen programas](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/first_timelogin1.png)

#### Cuando existe un programa y usted es administrador del sistema {#programs-exist-sysadmin}

Si los programas ya existen en su organización y usted es administrador del sistema, se muestra la página de aterrizaje **Administrar acceso** junto con **Agregar programa** .

![Vista del administrador del sistema](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/admin-console-4.png)


## Verificación de las funciones del usuario {#verify-user-roles}

Una vez que haya iniciado sesión correctamente en Cloud Manager, puede verificar que se le ha asignado la variable **Propietario empresarial** perfil de producto.

1. Seleccione el perfil en la parte superior derecha de la ventana.

   ![Perfil de usuario](/help/journey-onboarding/assets/setup-resources5.png)

1. Select **Funciones del usuario** para mostrar las funciones asignadas al usuario.

   ![Funciones de usuario](/help/journey-onboarding/assets/setup-resources6.png)

1. Confirma que el usuario tiene la variable **Propietario empresarial** función.

   ![Lista de funciones de usuario](/help/journey-onboarding/assets/setup-resources7.png)

Ha iniciado sesión correctamente en Cloud Manager como propietario empresarial. Si no tiene asignado el **Propietario empresarial** , póngase en contacto con el administrador del sistema.

## Crear un programa de Cloud Service {#create-cloud-service-program}

Ahora que se ha asegurado de tener acceso adecuado, puede crear su primer programa.

1. Vaya a la página de aterrizaje de Cloud Manager en [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e inicie sesión.

1. En la página de aterrizaje de Cloud Manager, haga clic en **Agregar programa** para iniciar el asistente Agregar programa .

   ![Página de aterrizaje](/help/journey-onboarding/assets/setup-resources4.png)

   >[!TIP]
   >
   >Para obtener instrucciones paso a paso sobre cómo utilizar el asistente Agregar programa, consulte el documento [Creación de programas de producción](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md) o mire esto [video](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/programs.html) para aprender a crear su programa AEM as a Cloud y obtener más información sobre consideraciones importantes antes de crear su programa.


1. Una vez creado correctamente el programa en la nube, puede navegar hasta el programa desde la página de aterrizaje de Cloud Manager para ver la **Información general** del programa.

   ![Información general del programa](/help/journey-onboarding/assets/setup-resources8.png)

1. Los miembros asignados al perfil de producto del desarrollador pueden iniciar sesión en Cloud Manager y administrar los repositorios de Git de Cloud Manager.

   * Si aún no lo ha hecho, es un buen momento para asignar miembros a la **Desarrollador** en su equipo de Cloud Manager. Vuelva a la [Asignar miembros del equipo a perfiles de producto de Cloud Manager](/help/journey-onboarding/sysadmin/assign-team-members-cloud-manager.md) documento de este recorrido para obtener más información.

Ahora su programa se ha creado correctamente y su repositorio de Git de Cloud Manager está disponible para que sus desarrolladores tengan acceso a él.

## Crear entornos de Cloud {#create-cloud-environments}

Una vez que haya creado correctamente su programa de nube, cree sus entornos de nube.

1. Vaya a la página de aterrizaje de Cloud Manager en [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) y seleccione **Agregar** de la tarjeta de entorno.

   ![Botón Agregar entorno](/help/journey-onboarding/assets/setup-resources9.png)

1. El asistente para agregar entorno se inicia y le guía a través de la adición de su entorno. Agregue primero su entorno de desarrollo para familiarizarse con el asistente.

   >[!TIP]
   >
   >Consulte el documento [Adición de un entorno](/help/implementing/cloud-manager/manage-environments.md#adding-environments) para obtener más información o ver [tutorial de vídeo rápido](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/environments.html) para obtener más información sobre los entornos de Cloud Manager y cómo puede agregarlos a su programa.

1. Miembros asignados al **Desarrollador** el perfil de producto puede iniciar sesión en Cloud Manager y administrar los repositorios de Git de Cloud Manager.

Ahora su programa se ha creado correctamente y su Git de Cloud Manager está disponible para que sus desarrolladores tengan acceso a él.

## Siguientes pasos {#whats-next}

Ahora que los recursos de la nube se han creado y están listos para que su equipo los pueda acceder, el administrador del sistema debe asignar a los integrantes del equipo AEM perfiles de producto as a Cloud Service de Adobe Admin Console para que puedan acceder a esos recursos.

Debe continuar con su recorrido de incorporación revisando el documento [Asignación de miembros del equipo a AEM perfiles de producto as a Cloud Service](/help/journey-onboarding/sysadmin/assign-team-members-aem-cloud-service.md) donde aprenderá a otorgar a los integrantes del equipo los derechos que necesitan para acceder a sus nuevos entornos.

## Recursos adicionales {#additional-resources}

Siga los recursos adicionales para obtener más información:

* [Tipos de programas y adición de un programa](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/programs.html)
* [Tipos de entorno y adición de un entorno](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/environments.html)
* [Administración de Git de Cloud Manager](/help/implementing/cloud-manager/managing-code/accessing-repos.md)
* [Configuración del acceso a AEM as a Cloud Service desde el Admin Console](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/accessing/overview.html#adobe-ims-users)
