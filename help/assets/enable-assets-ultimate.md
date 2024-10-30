---
title: Enable Assets Ultimate
description: Learn how to enable Assets Ultimate for new and existing customers.
feature: Asset Management
role: User, Admin
source-git-commit: 16ce83409044ad54140754112eb4d35b97883b44
workflow-type: tm+mt
source-wordcount: '1420'
ht-degree: 2%

---

# [!DNL Assets] {#enable-assets-cloud-service-ultimate}

| [Prácticas recomendadas de búsqueda](/help/assets/search-best-practices.md) | [Prácticas recomendadas de metadatos](/help/assets/metadata-best-practices.md) | [Centro de contenido](/help/assets/product-overview.md) | [Dynamic Media con funciones de OpenAPI](/help/assets/dynamic-media-open-apis-overview.md) | [Documentación de desarrollador de AEM Assets](https://developer.adobe.com/experience-cloud/experience-manager-apis/) |
| ------------- | --------------------------- |---------|----|-----|

![](/help/assets/assets/upgrade-assets-cs-ultimate-package-banner.png)

Assets as a Cloud Service Ultimate enables you to perform various key DAM capabilities, such as, asset management and library services, security and rights management, Creative and Experience Cloud connections, UI extensibility, API-driven automation, integrations with Adobe and non-Adobe applications, custom code deployment and many more. [](/help/assets/assets-ultimate-overview.md)

## Enable Assets Ultimate {#enable-assets-ultimate}

New Assets as a Cloud Service customers must first enable Assets Ultimate by creating a new program using Cloud Manager.

Ejecute los siguientes pasos:

1. As a system administrator, log on to Cloud Manager. Ensure that you select the right organization while logging in.

   >[!NOTE]
   >
   >Ensure that you are added to the appropriate Cloud Manager product profile to add a new program. [](/help/onboarding/cloud-manager-introduction.md#role-based-permissions)

1. [](/help/journey-onboarding/create-program.md)[](/help/journey-onboarding//create-environments.md)

   ******** ********[](/help/assets/product-overview.md)

   ![](assets/aem-assets-ultimate-solutions.png)

1. Haga clic en **[!UICONTROL Crear]** para crear la programa. Assets Ultimate ahora está habilitado para Experience Manager Assets como Cloud Service.

El administrador del sistema tiene derecho automáticamente como administrador de AEM en Assets Ultimate y recibe un correo electrónico para navegar a Admin Console para administrar los perfiles de productos disponibles.

Su AEM como Cloud Service instancia en Admin Console comprende los siguientes perfiles de producto:

* AEM Administradores de

* Usuarios de AEM 

* [Recursos AEM usuarios colaboradores](#onboard-collaborator-users)

* [Usuarios avanzados de Recursos AEM](#onboard-power-users)

  ![Recursos AEM perfiles de producto](assets/aem-assets-product-profiles.png)

Si ha habilitado el Centro de contenido para Assets como Cloud Service, hay una nueva instancia creada dentro de Recursos AEM como un Cloud Service en Admin Console con `delivery` como sufijo:

![Nuevo instancia para el Centro de contenido](assets/new-instance-content-hub.png)

>[!NOTE]
>
>Si ha aprovisionado el Centro de contenido antes del 14 de agosto de 2024, la nueva instancia se crea `contenthub` con el sufijo.

Tenga en cuenta que no hay `author` ni `publish` en el nombre de instancia de Content Hub.

Haga clic en el nombre de la instancia para ver el perfil de producto de Content Hub `AEM Assets Limited Users`.

![](assets/content-hub-product-profile.png)

You can start adding users or user groups to this product profile to provide them access to Content Hub.

>[!NOTE]
>
>`contenthub``Limited Users``delivery`

## Habilitar Assets Ultimate para clientes existentes {#enable-assets-ultimate-existing-customers}

Los clientes existentes de Assets as a Cloud Service pueden actualizar a Assets Ultimate ejecutando dos sencillos pasos. Puede navegar al programa as a Cloud Service de Assets en Cloud Manager y ver el estado de actualización en la tarjeta de programa en función de la disponibilidad de los créditos de Assets Ultimate. Si hay suficientes créditos disponibles para actualizar a Assets Ultimate, puede ver el estado como `Assets license upgrade required`, como se muestra en la siguiente imagen:

![Actualización de AEM Assets a Assets Ultimate](assets/aem-assets-upgrade-status-ultimate.png)

Si un cliente existente compra una nueva licencia para Assets Ultimate, el estado de actualización se muestra como `Assets license upgrade available`.

### Requisitos previos para la actualización {#prerequisites-assets-upgrade}

`2024.10.18175` If you do not meet the minimum requirements, contact your Adobe representative to switch to the required AEM release version.

### Actualizar a Assets Ultimate {#upgrade-assets-ultimate}

Ejecute los siguientes pasos:

1. After switching to the minimum requirements for the AEM release version, click the program name. ****

   ![](assets/aem-assets-upgrade-card.png)

1. Haga clic en **[!UICONTROL Agregar perfiles de producto]**. Cloud Manager muestra las opciones para agregar nuevos perfiles de producto a todos los entornos disponibles en el programa o en entornos individuales.

   ![Opciones de actualización de AEM Assets](assets/aem-assets-upgrade-options.png)

1. Haga clic en **[!UICONTROL Todos los entornos]** para agregar los nuevos perfiles de producto a todos los entornos del programa o en **[!UICONTROL Entornos individuales]** para agregar los nuevos perfiles de producto a los entornos seleccionados.

   ****

1. Haga clic en el icono de Más opciones correspondiente a un entorno y seleccione **[!UICONTROL Agregar perfiles de producto]** para agregar los nuevos perfiles de producto al entorno seleccionado.

   ![AEM Assets selecciona entornos individuales](assets/aem-assets-individual-environments.png)

   También puede agregar perfiles de producto a entornos seleccionados si navega hasta la sección **[!UICONTROL Entornos]**, hace clic en el icono Más opciones correspondiente a un entorno y selecciona **[!UICONTROL Agregar perfiles de producto]**.

   El estado del entorno muestra `Adding Product Profiles` mientras se agregan los nuevos perfiles de producto y, posteriormente, muestra `Running` cuando se completa el proceso.

   Debe agregar perfiles de producto a todos los entornos disponibles en el programa, individualmente o en todos los entornos juntos, antes de ejecutar el siguiente paso.

1. Haga clic en **[!UICONTROL Actualizar]**. ****

   ![](assets/aem-assets-upgrade-button.png)

   The upgrade process is complete and you have successfully upgraded your Assets as a Cloud Service to Assets Ultimate. `Assets Ultimate`

   ![](assets/program-status-post-upgrade.png)

Your AEM as a Cloud Service instance on Admin Console now comprises the following product profiles:

* AEM Administrators

* Usuarios de AEM 

* [AEM Assets Collaborator Users](#onboard-collaborator-users)

* [AEM Assets Power Users](#onboard-power-users)

![](assets/aem-assets-product-profiles.png)

**** ******** This step enables the Content Hub for Assets Ultimate. `delivery`

![](assets/new-instance-content-hub.png)

>[!NOTE]
>
>`contenthub`

`author``publish`

`AEM Assets Limited Users`

![](assets/content-hub-product-profile.png)

You can start adding users or user groups to this product profile to provide them access to Content Hub.

>[!NOTE]
>
>`contenthub``Limited Users``delivery`

## Onboard AEM Assets Collaborator users {#onboard-collaborator-users}

AEM Assets Collaborator users can work with assets from Experience manager via integrations of Assets available to your organization in other Adobe products and non-Adobe applications, create and edit assets using built-in Adobe Express and Firefly leveraging professionally designed templates, brand kits, Adobe Stock assets, and so on, and access and leverage approved assets from your organization using AEM Assets Content Hub portal.

Para incorporar usuarios colaboradores:

1. Para acceder a Experience Manager Assets perfiles de producto, haga clic en la AEM como nombre de producto Cloud Service en la lista de productos en Admin Console.

1. Haga clic en la instancia de autor de producción para AEM como Cloud Service:
   ![Perfiles de producto para AEM como Cloud Service](assets/aem-cloud-service-instances.png)

1. Haga clic en el perfil de producto Usuarios de Collaborators y luego en **[!UICONTROL Agregar usuarios]** para agregar usuarios o grupos de usuarios al perfil de producto.
   ![Perfil de producto de usuario](assets/aem-assets-collaborator-user-permissions.png)

1. Haga clic en **[!UICONTROL Guardar]** para guardar los cambios.

También puede acceder y vista los servicios asignados a los usuarios colaboradores, como se muestra en la siguiente imagen:

![Servicios para usuarios colaboradores](assets/aem-assets-collaborator-users.png)

`Adobe Express` y `AEM Assets Collaborator Users` los servicios están habilitados de forma predeterminada.

>[!NOTE]
>
>Puede desactivar y activar para habilitar o deshabilitar los servicios disponibles, según sus requisitos, sin embargo, Adobe Systems recomienda utilizar los servicios predeterminados habilitados para los perfiles de producto.


## Incorporación de usuarios avanzados de AEM Assets {#onboard-power-users}

Los usuarios avanzados de AEM Assets pueden acceder a todas las funciones de AEM Assets, incluida la administración de recursos, permisos, metadatos y al control y la automatización generales de los recursos digitales, trabajar con recursos de Experience Manager mediante integraciones de Assets disponibles para su organización en otras aplicaciones de Adobe y que no sean de Adobe, crear y editar recursos con Adobe Express y Firefly integrados aprovechando las plantillas diseñadas profesionalmente, los kits de marca, los recursos de Adobe Stock, etc., y acceder y aprovechar los recursos aprobados de su organización mediante AEM Assets Content Hub Portal.

To onboard Power users:

1. Access Experience Manager Assets product profiles by clicking the AEM as a Cloud Service product name in the list of products on Admin Console.

1. Click the production author instance for AEM as a Cloud Service:
   ![](assets/aem-cloud-service-instances.png)

1. Haga clic en el perfil de producto Usuarios avanzados y haga clic en **[!UICONTROL Agregar usuarios]** para agregar usuarios o grupos de usuarios al perfil de producto.
   ![perfil del producto del usuario](assets/aem-assets-power-user-permissions.png)

1. Haga clic en **[!UICONTROL Guardar]** para guardar los cambios.

También puede acceder y vista los servicios asignados a los usuarios avanzados, como se muestra en la siguiente imagen:

![Servicios para usuarios avanzados](assets/aem-assets-power-users.png)

`Adobe Express` y `AEM Assets Power Users` los servicios están habilitados de forma predeterminada.

>[!NOTE]
>
>Puede desactivar y activar para habilitar o deshabilitar los servicios disponibles, según sus requisitos, sin embargo, Adobe Systems recomienda utilizar los servicios predeterminados habilitados para los perfiles de producto.
