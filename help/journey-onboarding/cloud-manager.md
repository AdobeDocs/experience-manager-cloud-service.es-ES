---
title: Acceder a Cloud Manager
description: Obtenga información sobre cómo acceder a Cloud Manager para configurar los recursos del proyecto.
role: Admin, User, Developer
exl-id: c9476ac9-8318-493e-a48d-94ff5a6433a7
source-git-commit: 5c9dbaa25f0142afdae8b09dc18d1e1aaaf4c1fb
workflow-type: tm+mt
source-wordcount: '1044'
ht-degree: 52%

---

# Acceder a Cloud Manager {#cloud-resources}

En esta parte del [recorrido de incorporación,](overview.md) aprenderá a acceder a Cloud Manager para poder configurar sus recursos de proyecto.

## Objetivo {#objective}

En el artículo anterior de este recorrido de incorporación, [Asignar integrantes del equipo a perfiles de producto de Cloud Manager,](assign-profiles-cloud-manager.md) ha concedido a su equipo de AEMaaCS las funciones adecuadas. Ahora aprenda a acceder a Cloud Manager para poder configurar los recursos de su proyecto que utiliza su equipo.

Desde que ha completado el paso anterior en este recorrido, su equipo puede acceder a Cloud Manager. Cloud Manager se utiliza para crear y administrar los recursos de sus proyectos, como programas y entornos.

Después de leer este documento, debe comprender lo siguiente:

* Que un administrador del sistema asignado al **Propietario empresarial** debe ser la primera en su organización en iniciar sesión y acceder a Cloud Manager.
* Iniciar sesión en Cloud Manager.

## Cloud Manager {#cloud-manager}

Cloud Manager es un componente esencial de AEM as a Cloud Service y sirve como punto de entrada único para su equipo. Admite clientes con configuraciones de desarrollo empresarial con sus canalizaciones de CD/CI creadas específicamente, que están equipadas para garantizar pruebas exhaustivas y la máxima calidad de código para ofrecer experiencias excepcionales. Cloud Manager proporciona todo lo necesario para comenzar en forma de autoservicio, incluida la capacidad de crear los recursos y entornos de la nube.

Normalmente, un miembro del equipo asignado al perfil de producto **Propietario empresarial** es responsable de añadir los recursos de la nube, como programas y entornos. Esta persona comprende las necesidades comerciales y completa la configuración inicial de Cloud Manager.

A efectos de este recorrido de incorporación, usted, como administrador del sistema, ya se ha asignado a la función **Propietario empresarial** perfil de producto y puede configurar los recursos de la nube. Dependiendo de los requisitos reales del proyecto, los propietarios del negocio pueden ser o no iguales que el administrador del sistema.

## Acceder a Cloud Manager como administrador del sistema y propietario empresarial {#access-sysadmin-bo}

Antes de los integrantes del equipo que asignó al **Propietario empresarial** La función puede acceder a cloud manager y comenzar a crear recursos en la nube, debe asignarse al administrador del sistema la función **Propietario empresarial** función. También deben iniciar sesión en Cloud Manager como lo hizo en el paso anterior de este recorrido de integración.

1. Asegúrese de que, como administrador del sistema, tiene la función **Propietario empresarial** asignada.

   * Regrese al paso anterior de este recorrido, [Asignar miembros del equipo a perfiles de producto de Cloud Manager,](assign-profiles-cloud-manager.md) para obtener más información sobre cómo asignar la variable **Propietario empresarial** al administrador del sistema.

1. Inicie sesión en Cloud Manager en [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) y aparecerá la página de aterrizaje normal.

Al iniciar sesión correctamente como administrador del sistema con la función **Propietario empresarial**, inicialice Cloud Manager para que lo utilicen los demás usuarios con la función **Propietario empresarial**. No recibe confirmación ni ningún mensaje. Basta con iniciar sesión.

Hasta que inicie sesión en Cloud Manager como administrador del sistema con el **Propietario empresarial** , otros usuarios con la función **Propietario empresarial** no puede crear programas en Cloud Manager. Esta regla es verdadera incluso si se les asignan las funciones correctas.

## Navegar a Cloud Manager {#navigate-cloud-manager}

Los usuarios con la variable **Propietario empresarial** recibir un correo electrónico de bienvenida con un vínculo para empezar. Siga los pasos a continuación para navegar a Cloud Manager mediante este correo electrónico de bienvenida.

1. En el correo electrónico de bienvenida, haga clic en **Introducción**, como se muestra en la figura siguiente.
   ![Ejemplo de correo electrónico](/help/journey-onboarding/assets/get-started-email.png)

1. Vaya a la página de Cloud Manager **Programas y productos** página.

   >[!TIP]
   >
   >También puede navegar directamente a la página de inicio de sesión de Cloud Manager desde `[my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/)`. Marque esta página para referencia futura.

1. Se le dirige a la página de aterrizaje de Cloud Manager.

También puede navegar hasta la página **Programas y productos** de Cloud Manager desde la página de inicio de Adobe Experience Cloud siguiendo estos pasos

1. Vaya directamente a [Adobe Experience Cloud](https://experience.adobe.com) e inicie sesión con su Adobe ID.

1. En la página de inicio de Adobe Experience Cloud, seleccione **Experience Manager** para abrir la página principal de AEM.

   ![Página principal de Experience Cloud](/help/journey-onboarding/assets/setup-resources2.png)

1. En el **Cloud Manager** mosaico, seleccionar **Launch**.

   ![Página principal de AEM](/help/journey-onboarding/assets/setup-resources3.png)

1. Después de iniciar sesión correctamente, se le redirige a la página de aterrizaje de Cloud Manager. Consulte [Visualización de los programas de Cloud Manager](#viewing-programs) para obtener más información.

La forma de acceder a sus programas y productos a través de Cloud Manager depende de usted y no tiene ningún efecto en cómo utiliza Cloud Manager ni en cómo administra sus programas.

>[!NOTE]
>
>Según las funciones asignadas en Cloud Manager y el estado de la aplicación, verá diferentes pantallas mientras utiliza la interfaz de usuario de Cloud Manager.

## Visualización de programas {#viewing-programs}

Después de acceder correctamente a Cloud Manager, lo que ve depende del estado de sus programas, tal como se detalla en las secciones siguientes.

### Cuando no existen programas {#no-programs}

Si su organización no cuenta con ningún programa, la página de aterrizaje le indicará que cree su primer programa.

![Sin programas](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/first_timelogin0.png)

### Cuando los programas ya existen {#programs-exist}

Si hay programas en su organización, la página de aterrizaje muestra los programas existentes y también ofrece un botón para agregar programas adicionales.

![Existen programas](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/first_timelogin1.png)

### Cuando existe un programa y usted es administrador del sistema {#programs-exist-sysadmin}

Si los programas existen en su organización y usted es administrador del sistema, se muestra la página de aterrizaje **Administrar acceso** junto con **Agregar programa** .

![Vista del administrador del sistema](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/admin-console-4.png)

## Verificación de las funciones del usuario {#verify-user-roles}

Una vez que haya iniciado sesión correctamente en Cloud Manager, puede verificar que se le ha asignado el perfil de producto **Propietario empresarial**.

1. Seleccione el perfil en la parte superior derecha de la ventana.

   ![Perfil de usuario](/help/journey-onboarding/assets/setup-resources5.png)

1. Para mostrar las funciones asignadas al usuario, seleccione **Funciones del usuario**.

   ![Roles del usuario](/help/journey-onboarding/assets/setup-resources6.png)

1. El cuadro de diálogo debe confirmar que el usuario tiene la función **Propietario empresarial**.

   ![Lista de funciones de usuario](/help/journey-onboarding/assets/setup-resources7.png)

Ha iniciado sesión correctamente en Cloud Manager como Propietario empresarial. Si no tiene asignada la función **Propietario empresarial**, póngase en contacto con el administrador del sistema.

## Siguientes pasos {#whats-next}

Ahora que puede acceder a Cloud Manager como administrador del sistema, está listo para crear su primer programa.

Continúe con su recorrido de incorporación revisando el documento [Crear un programa](create-program.md) donde aprenda a hacerlo.

## Recursos adicionales {#additional-resources}

Los siguientes son recursos adicionales y opcionales si desea ir más allá del contenido del recorrido de incorporación.

* [Introducción a Cloud Manager](/help/onboarding/cloud-manager-introduction.md): Obtenga información sobre Cloud Manager, los programas de Cloud Manager y los entornos.
* [Perfiles de producto y equipo de AEM as a Cloud Service](/help/onboarding/aem-cs-team-product-profiles.md): aprenda cómo los perfiles de producto y equipo de AEM as a Cloud Service pueden conceder y limitar el acceso a sus soluciones con licencia de Adobe.
<!-- ERROR: Not Found (HTTP error 404) * [AEM Champion Tips and Tricks - Cloud Manager UI](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/expert-resources/aem-champions/cloud-manager-ui.md) - Watch this video for an overview of Cloud Manager's UI from an AEM champion. -->
