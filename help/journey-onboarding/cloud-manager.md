---
title: Acceso a Cloud Manager
description: Obtenga información sobre cómo acceder a Cloud Manager para configurar los recursos del proyecto.
role: Admin, User, Developer
source-git-commit: 709a80683357b0d56280ff14aa5f4ba6bf2c6b23
workflow-type: tm+mt
source-wordcount: '1025'
ht-degree: 1%

---


# Acceso a Cloud Manager {#cloud-resources}

En esta parte del [recorrido de incorporación,](overview.md) aprenderá a acceder a Cloud Manager para poder configurar sus recursos de proyecto.

## Objetivo {#objective}

En el artículo anterior de este recorrido de incorporación, [Asignación de miembros del equipo a perfiles de producto de Cloud Manager,](assign-profiles-cloud-manager.md) ha concedido a su equipo de AEMaaCS las funciones adecuadas. Ahora aprenda a acceder a Cloud Manager para poder configurar los recursos de su proyecto que utilizará su equipo.

Desde que ha completado el paso anterior en este recorrido, su equipo puede acceder a Cloud Manager. Cloud Manager se utiliza para crear y administrar los recursos de sus proyectos, como programas y entornos.

Después de leer este documento debe comprender:

* Que un administrador del sistema asignado al **Propietario empresarial** debe ser la primera en su organización en iniciar sesión y acceder a Cloud Manager.
* Cómo iniciar sesión en Cloud Manager.

## Cloud Manager {#cloud-manager}

Cloud Manager es un componente esencial de AEM as a Cloud Service y sirve como punto de entrada único para su equipo. Soporta a los clientes con configuraciones de desarrollo empresarial con sus canalizaciones de CD/CI creadas específicamente, que están equipadas para garantizar pruebas exhaustivas y la máxima calidad de código para ofrecer experiencias excepcionales. Cloud Manager proporciona todo lo necesario para comenzar de forma autoservicio, incluida la capacidad de crear los recursos y entornos de la nube.

Normalmente, un miembro del equipo asignado al **Propietario empresarial** el perfil de producto es responsable de añadir los recursos de la nube, como programas y entornos. Esta persona comprende las necesidades comerciales y completa la configuración inicial de Cloud Manager.

A efectos de este recorrido de incorporación, usted, como administrador del sistema, ya se ha asignado a la función **Propietario empresarial** perfil de producto y configurará los recursos de la nube. Dependiendo de los requisitos reales del proyecto, los propietarios del negocio pueden ser o no iguales que el administrador del sistema.

## Acceso a Cloud Manager como administrador del sistema y propietario empresarial {#access-sysadmin-bo}

Antes de los integrantes del equipo que asignó al **Propietario empresarial** La función puede acceder a cloud manager y comenzar a crear recursos en la nube, debe asignarse al administrador del sistema la función **Propietario empresarial** e inicie sesión en Cloud Manager como lo hizo en el paso anterior de este recorrido de integración.

1. Asegúrese de que, como administrador del sistema, tiene la variable **Propietario empresarial** función asignada.

   * Regrese al paso anterior de este recorrido, [Asignar miembros del equipo a perfiles de producto de Cloud Manager,](assign-profiles-cloud-manager.md) para obtener más información sobre cómo asignar la variable **Propietario empresarial** al administrador del sistema si aún no lo ha hecho.

1. Inicie sesión en Cloud Manager en [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) y se le presentará con la página de aterrizaje normal.

Al iniciar sesión correctamente como administrador del sistema con el **Propietario empresarial** , inicialice Cloud Manager para que lo utilicen los demás usuarios con la función **Propietario empresarial** función. No recibirá ninguna confirmación de este mensaje ni de ningún otro. Simplemente, iniciar sesión es suficiente.

Hasta que inicie sesión en Cloud Manager como administrador del sistema con el **Propietario empresarial** , otros usuarios con la función **Propietario empresarial** no podrá crear programas en Cloud Manager aunque se les asignen las funciones correctas.

## Vaya a Cloud Manager {#navigate-cloud-manager}

Los usuarios con la variable **Propietario empresarial** recibirá un correo electrónico de bienvenida con un vínculo para empezar. Siga los pasos a continuación para navegar a Cloud Manager mediante este correo electrónico de bienvenida.

1. En el correo electrónico de bienvenida, haga clic en **Introducción**, como se muestra en la figura siguiente.
   ![Ejemplo de correo electrónico](/help/journey-onboarding/assets/get-started-email.png)

1. Navegará a la página de Cloud Manager **Programas y productos** página.

   >[!TIP]
   >
   >También puede navegar directamente a la página de inicio de sesión de Cloud Manager desde `[my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/)`. Marque esta página para referencia futura.

1. Se le dirigirá a la página de aterrizaje de Cloud Manager.

También puede navegar hasta el informe de Cloud Manager **Programas y productos** en la página de inicio de Adobe Experience Cloud siguiendo estos pasos

1. Vaya directamente a [Adobe Experience Cloud](https://experience.adobe.com) e inicie sesión con su Adobe ID.

1. En la página de inicio de Adobe Experience Cloud, seleccione **Experience Manager**.

   ![página principal del Experience Cloud](/help/journey-onboarding/assets/setup-resources2.png)

1. Esto lo llevará a la página principal de AEM. Desde aquí, haga clic en **Launch** en el **Cloud Manager** mosaico.

   ![AEM página principal](/help/journey-onboarding/assets/setup-resources3.png)

1. Una vez que el inicio de sesión se haya realizado correctamente, se le dirigirá a la página de aterrizaje de Cloud Manager. Consulte [Visualización de los programas de Cloud Manager](#viewing-programs) para obtener más información.

La forma de acceder a sus programas y productos a través de Cloud Manager depende de usted y no tiene ningún efecto en cómo utiliza Cloud Manager ni en cómo administra sus programas.

>[!NOTE]
>
>Según las funciones asignadas en Cloud Manager y el estado de la aplicación, verá diferentes pantallas mientras utiliza la interfaz de usuario de Cloud Manager.

## Visualización de programas {#viewing-programs}

Una vez que acceda correctamente a Cloud Manager, lo que vea dependerá del estado de sus programas, tal como se detalla en las secciones siguientes.

### Cuando no existen programas {#no-programs}

Si su organización no cuenta con ningún programa, la página de aterrizaje le indicará que cree su primer programa.

![Sin programas](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/first_timelogin0.png)

### Cuando los programas ya existen {#programs-exist}

Si los programas ya existen en su organización, la página de aterrizaje muestra los programas existentes y también ofrece un botón para agregar programas adicionales.

![Existen programas](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/first_timelogin1.png)

### Cuando existe un programa y usted es administrador del sistema {#programs-exist-sysadmin}

Si los programas ya existen en su organización y usted es administrador del sistema, se muestra la página de aterrizaje **Administrar acceso** junto con **Agregar programa** .

![Vista del administrador del sistema](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/admin-console-4.png)

## Verificación de las funciones del usuario {#verify-user-roles}

Una vez que haya iniciado sesión correctamente en Cloud Manager, puede verificar que se le ha asignado la variable **Propietario empresarial** perfil de producto.

1. Seleccione el perfil en la parte superior derecha de la ventana.

   ![Perfil de usuario](/help/journey-onboarding/assets/setup-resources5.png)

1. Select **Funciones del usuario** para mostrar las funciones asignadas al usuario.

   ![Funciones de usuario](/help/journey-onboarding/assets/setup-resources6.png)

1. El cuadro de diálogo debe confirmar que el usuario tiene la variable **Propietario empresarial** función.

   ![Lista de funciones de usuario](/help/journey-onboarding/assets/setup-resources7.png)

Ha iniciado sesión correctamente en Cloud Manager como propietario empresarial. Si no tiene asignado el **Propietario empresarial** , póngase en contacto con el administrador del sistema.

## Siguientes pasos {#whats-next}

Ahora que puede acceder a Cloud Manager como administrador del sistema, está listo para crear su primer programa.

Debe continuar con su recorrido de incorporación revisando el documento [Crear un programa](create-program.md) donde aprenderá a hacerlo.

## Recursos adicionales {#additional-resources}

Siga los recursos adicionales para obtener más información:

* [Introducción a Cloud Manager](/help/onboarding/cloud-manager-introduction.md) : Obtenga información sobre Cloud Manager, los programas de Cloud Manager y los entornos.
