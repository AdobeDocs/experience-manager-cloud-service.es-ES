---
title: Implementar [!DNL Content Hub]
description: Obtenga información sobre cómo implementar y activar Content Hub y proporcionar acceso a usuarios con diferentes tipos de privilegios (cargar recursos, usuarios de Adobe Express) y cómo proporcionar privilegios de administrador a usuarios.
role: Admin
source-git-commit: 7224cca950e61bea298f246245bdb221fd8fa22e
workflow-type: tm+mt
source-wordcount: '1316'
ht-degree: 0%

---


# Implementación de Content Hub {#deploy-content-hub}

![Implementación de Content Hub](assets/deploy-content-hub.png)

Content Hub está disponible como parte del as a Cloud Service de Experience Manager Assets para democratizar el acceso al contenido en la marca para las organizaciones y sus socios comerciales.

Los recursos que se marcan como Aprobado en el as a Cloud Service de Experience Manager Assets están disponibles para su distribución en Content Hub.

Este artículo proporciona un flujo de trabajo completo para proporcionar acceso a Content Hub a los usuarios, incluidas las variaciones de privilegios según sus necesidades.

Las variaciones de privilegios en Content Hub incluyen:

* [Usuarios de Content Hub](#onboard-content-hub-users): Acceda a los recursos aprobados por la marca en el portal de Content Hub.

* [Administradores de Content Hub](#onboard-content-hub-administrator): acceso a la [Interfaz de usuario de configuración](/help/assets/configure-content-hub-ui-options.md) en Content Hub, además de acceder a recursos aprobados por la marca, cargar recursos en Content Hub, Adobe Express la integración para editar imágenes (si tiene derechos de Adobe Express).

* [Usuarios de Content Hub con derechos para añadir recursos](#onboard-content-hub-users-add-assets): capacidad para [cargar recursos en Content Hub](/help/assets/upload-brand-approved-assets.md) además de acceder a los recursos aprobados por la marca en el portal de Content Hub.

* [Usuarios de Content Hub con derechos para remezclar recursos con nuevas variaciones](#onboard-content-hub-users-remix-assets): [Integración de Adobe Express](/help/assets/edit-images-content-hub.md) (si tiene derechos de Adobe Express) además de acceder a los recursos aprobados por la marca en el portal de Content Hub.

* [Usuarios de Experience Manager Assets](#experience-manager-assets-users): capacidad para aprobar recursos en Experience Manager Assets as a Cloud Service para que estén disponibles en Content Hub.

## Paso 1: Habilitar Content Hub para Experience Manager Assets con Cloud Manager {#enable-content-hub}

Para acceder al portal de Content Hub, los administradores primero deben habilitar el as a Cloud Service de Content Hub para Experience Manager Assets con Cloud Manager. Ejecute los siguientes pasos:

1. Inicie sesión en Cloud Manager. Asegúrese de seleccionar la organización correcta al iniciar sesión. Cloud Manager enumera todos los programas.

1. Vaya al programa as a Cloud Service de Experience Manager Assets, haga clic en el icono Más opciones (...) y seleccione **[!UICONTROL Editar programa]**.

   ![Editar programa en Cloud Manager](assets/edit-program-cloud-manager.png)

1. En el [!UICONTROL Editar programa] , seleccione la **[!UICONTROL Soluciones y complementos]** pestaña.

1. Expandir **[!UICONTROL Assets]** y seleccione **[!UICONTROL Content Hub]**.
   ![Seleccione Content Hub en Cloud Manager](assets/edit-program-cloud-manager-content-hub.png)

   >[!NOTE]
   >
   >If **[!UICONTROL Actualizar]** no está habilitado después de seleccionar Content Hub. Asegúrese de haber especificado la configuración de Go-Live para el programa.

1. Haga clic en **[!UICONTROL Actualizar]**.

Content Hub ahora está habilitado para Experience Manager Assets as a Cloud Service.

>[!NOTE]
>
>Puede acceder a Content Hub y utilizarlo con hasta 250 usuarios de Content Hub. Si tiene más preguntas, póngase en contacto con el representante del Adobe.


Si es su primera vez en Experience Manager Assets, haga clic en **[!UICONTROL Agregar programa]** y, a continuación, proporcione los detalles del programa (Nombre del programa, configurado para la producción) y haga clic en **[!UICONTROL Continuar]**. A continuación, puede seleccionar **[!UICONTROL Assets]** y **[!UICONTROL Content Hub]** en el **[!UICONTROL Soluciones y complementos]** pestaña.

### Instancia de Content Hub y perfil de producto en Admin Console{#content-hub-instance-product-profile}

Después [habilitar Content Hub para el as a Cloud Service de Assets con Cloud Manager](#enable-content-hub), se crea una nueva instancia dentro de AEM Assets as a Cloud Service Admin Console con `contenthub` como sufijo:

![Nueva instancia para Content Hub](assets/new-instance-content-hub.png)

Tenga en cuenta que no hay `author` o `publish` en el nombre de instancia de Content Hub.

Haga clic en el nombre de la instancia para ver el perfil de producto de Content Hub.

![Perfil de producto de Content Hub](assets/content-hub-product-profile.png)

## Paso 2: Incorporar un administrador de Content Hub {#onboard-content-hub-administrator}

Los administradores de Content Hub pueden acceder a [Interfaz de usuario de configuración](/help/assets/configure-content-hub-ui-options.md) en Content Hub, además de acceder a recursos aprobados por la marca, cargar recursos en Content Hub, Adobe Express la integración para editar imágenes (si tiene derechos de Adobe Express).

Para incorporar al administrador de Content Hub:

1. [Acceda al perfil de producto de usuario de Content Hub y haga clic en él](#content-hub-instance-product-profile).

1. Clic **[!UICONTROL Adición de usuarios]** para agregar usuarios o grupos de usuarios al perfil de producto.

1. Clic **[!UICONTROL Guardar]** para guardar los cambios.

1. Después de añadir el usuario al perfil de producto de Content Hub, acceda a los perfiles de producto de Experience Manager Assets haciendo clic en el nombre del producto de AEM as a Cloud Service en la lista de productos en Admin Console.

1. Haga clic en la instancia de autor de producción para AEM as a Cloud Service:
   ![Perfiles de producto para AEM as a Cloud Service](assets/aem-cloud-service-instances.png)

   Admin Console muestra dos perfiles de producto para AEM as a Cloud Service: administradores y usuarios.
1. Haga clic en el perfil de producto Administradores y en **[!UICONTROL Adición de usuarios]** para añadir al usuario al perfil de producto.
   ![Perfil de producto del administrador](assets/aem-cs-admin-product-profile.png)

1. Clic **[!UICONTROL Guardar]** para guardar los cambios.

## Paso 3: Incorporar usuarios de Content Hub {#onboard-content-hub-users}

Los usuarios de Content Hub pueden acceder a los recursos disponibles en el portal, pero no pueden añadir nuevos recursos ni modificar los existentes.

Para incorporar usuarios de Content Hub:

1. [Acceda al perfil de producto de usuario de Content Hub y haga clic en él](#content-hub-instance-product-profile).

1. Clic **[!UICONTROL Adición de usuarios]** para agregar usuarios o grupos de usuarios al perfil de producto.

1. Clic **[!UICONTROL Guardar]** para guardar los cambios.

Estos usuarios ahora pueden acceder a los recursos disponibles en el portal de Content Hub.

>[!NOTE]
>
>Puede utilizar todas las funciones empresariales avanzadas, como la sincronización con proveedores de identidad externos.

### ¿Cómo acceder a Content Hub? {#access-content-hub}

Se puede acceder a Content Hub de las siguientes maneras:

* Acceda a Content Hub mediante el siguiente vínculo:

  `https://experience.adobe.com/#/assets/contenthub`

* Iniciar sesión en `experience.adobe com` y haga clic en **[!UICONTROL Experience Manager Assets Content Hub]** disponible en el **[!UICONTROL Acceso rápido]** sección:
  ![Acceso a Content Hub](assets/access-content-hub.png)

* Iniciar sesión en `experience.adobe com` y haga clic en **[!UICONTROL Experience Manager Assets Content Hub]** disponible en el conmutador de productos:
  ![Método de acceso de Content Hub 3](assets/access-content-hub-alternate.png)

### Deshabilitar notificaciones por correo electrónico a usuarios {#disable-email-notifications}

Si los administradores necesitan deshabilitar las notificaciones por correo electrónico enviadas a los usuarios cuando se añaden al perfil de producto de Content Hub:

Haga clic en el icono de búsqueda junto al nombre del perfil del producto y deshabilite la variable **[!UICONTROL Notificar a los usuarios por correo electrónico]** alternar.

![Deshabilitar notificaciones por correo electrónico](assets/disable-email-notifications.png)


## Paso 4: Incorporar usuarios de Content Hub con derechos para agregar recursos (opcional) {#onboard-content-hub-users-add-assets}

Los usuarios de Content Hub con derechos para agregar recursos pueden [cargar nuevos recursos aprobados por la marca en Content Hub](/help/assets/upload-brand-approved-assets.md).

Para incorporar usuarios de Content Hub con derechos para agregar usuarios:

1. [Después de agregar el usuario al perfil de producto de Content Hub](#onboard-content-hub-users), acceda a los perfiles de producto de Experience Manager Assets haciendo clic en el nombre del producto de AEM as a Cloud Service en la lista de productos en el Admin Console.

1. Haga clic en la instancia de autor de producción para AEM as a Cloud Service:
   ![Perfiles de producto para AEM as a Cloud Service](assets/aem-cloud-service-instances.png)

   Admin Console muestra dos perfiles de producto para AEM as a Cloud Service: administradores y usuarios.
1. Haga clic en el perfil de producto Usuarios y en **[!UICONTROL Adición de usuarios]** para añadir al usuario al perfil de producto.
   ![Perfil de producto del usuario](assets/aem-cs-user-product-profile.png)

1. Clic **[!UICONTROL Guardar]** para guardar los cambios.

## Paso 4: Incorporar usuarios de Content Hub con derechos para remezclar recursos con nuevas variaciones (opcional) {#onboard-content-hub-users-remix-assets}

Los usuarios de Content Hub con derechos para remezclar recursos con nuevas variaciones pueden [modifique los recursos existentes mediante Adobe Express y guárdelo en el repositorio](/help/assets/edit-images-content-hub.md). La edición de recursos mediante Adobe Express solo está disponible si el usuario tiene derechos de Adobe Express.

Para incorporar usuarios de Content Hub con derechos para remezclar recursos con nuevas variaciones:

1. [Después de agregar el usuario al perfil de producto de Content Hub](#onboard-content-hub-users), acceda a los perfiles de producto de Experience Manager Assets haciendo clic en el nombre del producto de AEM as a Cloud Service en la lista de productos en el Admin Console.

1. Haga clic en la instancia de autor de producción para AEM as a Cloud Service:
   ![Perfiles de producto para AEM as a Cloud Service](assets/aem-cloud-service-instances.png)

   Admin Console muestra dos perfiles de producto para AEM as a Cloud Service: administradores y usuarios.
1. Haga clic en el perfil de producto Usuarios y en **[!UICONTROL Adición de usuarios]** para añadir al usuario al perfil de producto.
   ![Perfil de producto del usuario](assets/aem-cs-user-product-profile.png)

1. Clic **[!UICONTROL Guardar]** para guardar los cambios.

## Usuarios de Experience Manager Assets {#experience-manager-assets-users}

Los usuarios de Experience Manager Assets pueden aprobar los recursos en AEM as a Cloud Service para que estén disponibles en Content Hub.

Para configurar usuarios de Experience Manager Assets:

1. Acceda a los perfiles de producto de Experience Manager Assets haciendo clic en el nombre del producto de AEM as a Cloud Service en la lista de productos en el Admin Console.

1. Haga clic en la instancia de autor de producción para AEM as a Cloud Service:
   ![Perfiles de producto para AEM as a Cloud Service](assets/aem-cloud-service-instances.png)

   Admin Console muestra dos perfiles de producto para AEM as a Cloud Service: administradores y usuarios.
1. Haga clic en el perfil de producto Usuarios y en **[!UICONTROL Adición de usuarios]** para añadir al usuario al perfil de producto.
   ![Perfil de producto del usuario](assets/aem-cs-user-product-profile.png)

1. Clic **[!UICONTROL Guardar]** para guardar los cambios.

   >[!NOTE]
   >
   > No es necesario que se le añada al [Perfil de producto de Content Hub](#onboard-content-hub-users) para los usuarios de Experience Manager Assets.



