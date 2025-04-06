---
title: Administrar [!DNL Adobe Stock] recursos en [!DNL Assets].
description: Busque, recupere, conceda licencias y administre  [!DNL Adobe Stock] recursos dentro de [!DNL Adobe Experience Manager]. Utilice los recursos con licencia como cualquier otro recurso digital.
contentOwner: Vishabh Gupta
feature: Adobe Stock
role: Admin, User
exl-id: 13f21d79-2a8d-4cb1-959e-c10cc44950ea
source-git-commit: deab7ac707527e62f7a0fa3581080171e499cd32
workflow-type: tm+mt
source-wordcount: '2258'
ht-degree: 5%

---

# Usar [!DNL Adobe Stock] recursos en [!DNL Adobe Experience Manager Assets] {#use-adobe-stock-assets-in-aem-assets}

<table>
    <tr>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nuevo</i></sup> <a href="/help/assets/dynamic-media/dm-prime-ultimate.md"><b>Dynamic Media Prime y Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nuevo</i></sup> <a href="/help/assets/assets-ultimate-overview.md"><b>AEM Assets Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nuevo</i></sup> <a href="/help/assets/integrate-aem-assets-edge-delivery-services.md"><b>Integración de AEM Assets con Edge Delivery Services</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>New</i></sup> <a href="/help/assets/aem-assets-view-ui-extensibility.md"><b>Extensibilidad de la IU</b></a>
        </td>
          <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nuevo</i></sup> <a href="/help/assets/dynamic-media/enable-dynamic-media-prime-and-ultimate.md"><b>Habilitar Dynamic Media Prime y Ultimate</b></a>
        </td>
    </tr>
    <tr>
        <td>
            <a href="/help/assets/search-best-practices.md"><b>Prácticas recomendadas de búsqueda</b></a>
        </td>
        <td>
            <a href="/help/assets/metadata-best-practices.md"><b>Prácticas recomendadas de metadatos</b></a>
        </td>
        <td>
            <a href="/help/assets/product-overview.md"><b>Centro de contenido</b></a>
        </td>
        <td>
            <a href="/help/assets/dynamic-media-open-apis-overview.md"><b>Dynamic Media con funciones de OpenAPI</b></a>
        </td>
        <td>
            <a href="https://developer.adobe.com/experience-cloud/experience-manager-apis/"><b>Documentación de desarrollador de AEM Assets</b></a>
        </td>
    </tr>
</table>

<!--
| Version | Article link |
| -------- | ---------------------------- |
| AEM 6.5  |    [Click here](https://experienceleague.adobe.com/docs/experience-manager-65/assets/using/aem-assets-adobe-stock.html?lang=en)                  |
| AEM as a Cloud Service     | This article         |
-->
El servicio [!DNL Adobe Stock] proporciona a diseñadores y empresas acceso a millones de fotografías, vectores, ilustraciones, vídeos, plantillas y recursos 3D de alta calidad, depurados y libres de derechos para todos sus proyectos creativos.

[!DNL Adobe Stock] para la oferta empresarial, de forma predeterminada, incluye derechos de uso compartido en toda la organización. Una vez que un usuario de la organización ha concedido una licencia a un recurso, otros usuarios de la organización pueden identificar, descargar y utilizar este recurso sin tener que volver a obtener la licencia. Una vez que su organización ha concedido una licencia a un recurso, el derecho a utilizarlo es perpetuo.

Las organizaciones pueden integrar su plan empresarial [!DNL Adobe Stock] con [!DNL Experience Manager Assets] para garantizar que los recursos con licencia estén ampliamente disponibles para sus proyectos creativos y de marketing, con las potentes capacidades de administración de recursos de [!DNL Experience Manager]. Los usuarios de [!DNL Experience Manager] pueden buscar, obtener una vista previa y obtener una licencia rápidamente de los recursos de Adobe Stock guardados en [!DNL Experience Manager], sin salir de la interfaz de [!DNL Experience Manager].

## Requisitos previos para integrar [!DNL Experience Manager] y [!DNL Adobe Stock] {#integrate-aem-and-adobe-stock}

[!DNL Experience Manager Assets] ofrece a los usuarios la capacidad de buscar, obtener una vista previa, guardar y conceder licencias a [!DNL Adobe Stock] recursos directamente desde [!DNL Experience Manager].

Cumplan los siguientes requisitos para habilitar esta integración:

* Se está ejecutando [!DNL Experience Manager Assets] como instancia de [!DNL Cloud Service]
* Un [plan de empresa [!DNL Adobe Stock] 2}](https://stockenterprise.adobe.com/)
* Un usuario con permisos en [!DNL Admin Console] para el perfil de producto de Stock predeterminado
* Un usuario con permisos para [!DNL Developer Access profile] para crear la integración en [!DNL Adobe Developer Console]

Un plan de [!DNL Adobe Stock] de empresa,

* Proporciona derechos de producto para [!DNL Adobe Stock] (existencias conectadas a Experience Manager)
* Créditos comprados en [!DNL Adobe Admin Console] por su asignación de acciones
* Habilita la administración de créditos y licencias globalmente desde [!DNL Adobe Admin Console]

Dentro del derecho, existe un perfil de producto predeterminado para [!DNL Adobe Stock] en [!DNL Admin Console]. Se pueden crear varios perfiles, que determinan quién puede obtener la licencia de los recursos de Stock. Un usuario que tenga acceso directo al perfil del producto puede acceder a [https://stock.adobe.com/](https://stock.adobe.com/) y obtener la licencia de los recursos de Stock. Mientras que hay otro método para utilizar el acceso de desarrollador para crear una integración (API). Esta integración autentica la comunicación entre [!DNL Experience Manager Assets] y [!DNL Adobe Stock].

<!--
### Create an IMS configuration {#create-an-ims-configuration}

1. In the [!DNL Experience Manager] user interface, navigate to **[!UICONTROL Tools]** > **[!UICONTROL Security]** > **[!UICONTROL Adobe IMS Configurations]**. Click **[!UICONTROL Create]** and select **[!UICONTROL Cloud Solution]** > **[!UICONTROL Adobe Stock]**.
1. Either reuse an existing certificate or select **[!UICONTROL Create new certificate]**.
1. Click **[!UICONTROL Create certificate]**. Once created, download the public key. Click **[!UICONTROL Next]**. Leave the [!UICONTROL Adobe IMS Technical Account Configuration] screen open to provide the required values shortly.
1. Access [Adobe Developer Console](https://console.adobe.io). Ensure that your account has administrator permissions for the organization for which the integration is required.
1. Click **[!UICONTROL Create new project]** and click **[!UICONTROL Add API]**. Select **[!UICONTROL Adobe Stock]** from the list of APIs that are available to you. Select [!UICONTROL OAUTH 2.0 Web].
1. Provide **[!UICONTROL Default redirect URI]** and **[!UICONTROL Redirect URI pattern]** values. Click **[!UICONTROL Save configured API]**. Copy the generated ID and secret.
1. In [!UICONTROL Adobe IMS Technical Account Configuration] screen, provide the values in the boxes titled **[!UICONTROL Title]**, **[!UICONTROL Authorization Server]**, **[!UICONTROL API Key]**, **[!UICONTROL Client Secret]**, and **[!UICONTROL Payload]**. For detailed information about these values, see [JWT authentication quick start](https://www.adobe.io/authentication/auth-methods.html#!AdobeDocs/adobeio-auth/master/JWT/JWT.md).

-->
<!-- TBD: Update the URL to update the terminology when AIO team updates their documentation URL. Logged issue github.com/AdobeDocs/adobeio-auth/issues/63.
-->

<!--
### Create [!DNL Adobe Stock] configuration in [!DNL Experience Manager] {#create-adobe-stock-configuration-in-aem}

1. In the [!DNL Experience Manager], navigate to **[!UICONTROL Tools]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Adobe Stock]**.
1. Click **[!UICONTROL Create]** to create a configuration and associate it with your existing IMS Configuration. Select `PROD` as the environment parameter.
1. In **[!UICONTROL Licensed Assets Path]** field, leave a location as is. Do not change the location where you want to store the [!DNL Adobe Stock] assets.
1. Complete creation by adding all the required properties. Click **[!UICONTROL Save & Close]**.
1. Add [!DNL Experience Manager] users or groups, who can license the assets.

>[!NOTE]
>
>If there are multiple [!DNL Adobe Stock] configurations, select the desired configuration in User Preferences panel. To access the panel from Experience Manager home page, click the user icon and then click **[!UICONTROL User Preferences]** > **[!UICONTROL Stock Configuration]**.
-->

## Integrar [!DNL Experience Manager] y [!DNL Adobe Stock] {#integrate-adobe-stock-with-aem-assets}

Como desarrollador, ejecute los siguientes pasos para integrar [!DNL Adobe Experience Manager] y [!DNL Adobe Stock].

<!--
1. [Obtain public certificate](#public-certificate)
   
   In [!DNL Experience Manager], create an IMS account and generate a public certificate (public key).

1. [Create service account (JWT) connection](#createnewintegration) 
   
   In [!DNL Adobe Developer Console], create a project for your [!DNL Adobe Stock] organization. Under the project, configure an API using the public key to create a service account (JWT) connection. Get the service account credentials and JWT payload information.

1. [Configure IMS account](#create-ims-account-configuration)

   In [!DNL Experience Manager], configure the IMS account using the service account credentials and JWT payload.

1. [Configure cloud service](#configure-the-cloud-service)

   In [!DNL Experience Manager], configure an [!DNL Adobe Stock] cloud service using the IMS account.


### Create an IMS configuration {#create-an-ims-configuration}

The IMS configuration authenticates your [!DNL Experience Manager Assets] author instance with the [!DNL Adobe Stock] entitlement. 

IMS configuration includes two steps:

* [Obtain public certificate](#public-certificate) 
* [Configure IMS account](#create-ims-account-configuration)

### Obtain public certificate {#public-certificate}

The public key (certificate) authenticates your product profile in Adobe Developer Console.

1. Log in to your [!DNL Experience Manager Assets] cloud instance.

1. From the **[!UICONTROL Tools]** panel, navigate to **[!UICONTROL Security]** > **[!UICONTROL Adobe IMS Configurations]**.

1. In Adobe IMS Configurations page, click **[!UICONTROL Create]**. The **[!UICONTROL Adobe IMS Technical Account Configuration]** page opens. 

1. In the **[!UICONTROL Certificate]** tab, select **[!UICONTROL Adobe Stock]** from the **[!UICONTROL Cloud Solution]** drop-down list.  

1. You can create a certificate or reuse an existing certificate for the configuration. 

   To create a certificate, select the **[!UICONTROL Create new certificate]** check box and specify an **alias** for the public key. The alias serves as name of the public key. 

1. Click **[!UICONTROL Create certificate]**. Then, click **[!UICONTROL OK]** to generate the public key.

1. Click the **[!UICONTROL Download Public Key]** icon and save the public key (.crt) file on your machine. The public key is used later to configure API for your Brand Portal tenant and generate service account credentials in Adobe Developer Console.

   Click **[!UICONTROL Next]**.

   ![generate-certificate](assets/stock-integration-ims-account.png)

1. In the **Account** tab, Adobe IMS account is created which requires the service account credentials.

   Open a new tab and [create a service account (JWT) connection in Adobe Developer Console](#createnewintegration). 

### Create service account (JWT) connection {#createnewintegration}

In Adobe Developer Console, projects and APIs are configured at organization level. Configuring an API creates a service account (JWT) connection. There are two methods to configure API, by generating a key pair (private and public keys) or by uploading a public key. In this example, the service account credentials are generated by uploading the public key.

To generate the service account credentials and JWT payload:

1. Log in to Adobe Developer Console with system administrator privileges. The default URL is [https://www.adobe.com/go/devs_console_ui](https://www.adobe.com/go/devs_console_ui).


   Ensure that you have selected the correct IMS organization (Stock entitlement) from the drop-down (organization) list.

1. Click **[!UICONTROL Create new project]**. A blank project with a system-generated name is created for your organization. 

   Click **[!UICONTROL Edit project]**. Update the **[!UICONTROL Project Title]** and **[!UICONTROL Description]**, and then click **[!UICONTROL Save]**.
   
1. In the **[!UICONTROL Project overview]** tab, click **[!UICONTROL Add API]**.

1. In the **[!UICONTROL Add an API window]**, select **[!UICONTROL Adobe Stock]**. Click **[!UICONTROL Next]**. 

1. In the **[!UICONTROL Configure API]** window, select **[!UICONTROL Service Account (JWT)]** authentication. Click **[!UICONTROL Next]**.

   ![create-jwt-credentials](assets/aem-stock-jwt.png)

1. Click **[!UICONTROL Upload your public key]**. Click **[!UICONTROL Select a File]** and upload the public key (.crt file) that you have downloaded in the [obtain public certificate](#public-certificate) section. Click **[!UICONTROL Next]**.

1. Verify the public key and click **[!UICONTROL Next]**.

1. Select the default **[!UICONTROL Adobe Stock]** product profile and click **[!UICONTROL Save configured API]**. 

1. Once the API is configured, you are redirected to the API overview page. From the left navigation under **[!UICONTROL Credentials]**, click the **[!UICONTROL Service Account (JWT)]** option. Here, you can view the credentials and perform actions such as generate JWT tokens, copy credential details, and retrieve client secret.

1. From the **[!UICONTROL Client Credentials]** tab, copy the **[!UICONTROL client ID]**. 

   Click **[!UICONTROL Retrieve Client Secret]** and copy the **[!UICONTROL client secret]**.

   ![generate-jwt-credentials](assets/aem-stock-jwt-credential.png)

1. Navigate to the **[!UICONTROL Generate JWT]** tab and copy the **[!UICONTROL JWT Payload]** information. 

You can now use the client ID (API key), client secret, and JWT payload to [configure the IMS account](#create-ims-account-configuration) in [!DNL Experience Manager Assets].

### Configure IMS account {#create-ims-account-configuration}

You must have the [certificate](#public-certificate) and [service account (JWT) credentials](#createnewintegration) to configure the IMS account.

To configure the IMS account: 

1. Open the IMS Configuration and navigate to the **[!UICONTROL Account]** tab. You kept the page open while [obtaining the public certificate](#public-certificate).

1. Specify a **[!UICONTROL Title]** for the IMS account.

   In the **[!UICONTROL Authorization Server]** field, enter the URL: [https://ims-na1.adobelogin.com/](https://ims-na1.adobelogin.com/).  

   Enter the client ID in the **[!UICONTROL API key]** field, **[!UICONTROL Client Secret]**, and **[!UICONTROL Payload]** (JWT payload) that you have copied while [creating the service account (JWT) connection](#createnewintegration).

1. Click **[!UICONTROL Create]**. An IMS account configuration is created. 

   ![configure-ims-acount](assets/aem-stock-ims-config.png)
   
1. Select the IMS account configuration and click **[!UICONTROL Check Health]**.

   Click **[!UICONTROL Check]** in the dialog box. On successful configuration, a message appears that the *Token is retrieved successfully*.

   ![health-check](assets/aem-stock-healthcheck.png)
-->

1. [Configurar un programa en  [!DNL Developer Console]](#set-up-a-program-in-developer-console)
1. [Agregar configuración en la instancia de autor  [!DNL AEM] ](#add-configuration-in-the-aem-author-instance)

### Configurar un programa en [!DNL Developer Console] {#set-up-a-program-in-developer-console}

Ejecute los siguientes pasos para configurar un programa en [!DNL Developer Console]:
1. Vaya a [[!DNL Adobe Developer Console]](https://developer.adobe.com/console/14431/user/servicesandapis) e inicie sesión en su organización.
1. Seleccione **[!UICONTROL Crear nuevo proyecto]** disponible en el tablero **[!UICONTROL Proyectos]**.
   ![integrar aem assets con adobe stock](/help/assets/assets/create-new-project-in-adobe-dev-console.png)
1. Haga clic en **[!UICONTROL Agregar al proyecto]** y seleccione **[!UICONTROL API]**.
1. Seleccione **[!UICONTROL Adobe Stock]** y haga clic en **[!UICONTROL Siguiente]**.
1. Especifique un **[!UICONTROL nombre de credencial]**, compruebe que está seleccionado **[!UICONTROL Servidor a servidor OAuth]** y haga clic en **[!UICONTROL Siguiente]**.
1. Seleccione **[!UICONTROL AEM Assets]** **[!UICONTROL Perfil del producto]** y haga clic en **[!UICONTROL Guardar la API configurada]**. Aparece un mensaje de confirmación para confirmar que creó un proyecto en [!DNL Developer Console]. Se abre el tablero del proyecto, con el nombre del proyecto en la parte superior, **[!UICONTROL Adobe Stock]** en **[!UICONTROL API]** y **[!UICONTROL AEM Assets]** en **[!UICONTROL Perfil del producto]** y la tarjeta de credenciales de **[!UICONTROL OAuth de servidor a servidor]** en **[!UICONTROL Credenciales conectadas]**.
   ![integrar aem assets y adobe stock](/help/assets/assets/adc-project-name.png)
1. Seleccione la tarjeta de credenciales **[!UICONTROL OAuth Server-to-Server]** y se mostrarán los **[!UICONTROL detalles de credenciales]**. Use estos [!DNL OAuth Server-to-Server] detalles de credenciales de su proyecto, como **[!UICONTROL ID de cliente]**, **[!UICONTROL Secreto de cliente]**, **[!UICONTROL Ámbito]**, **[!UICONTROL Nombre de credencial]**, **[!UICONTROL ID de cuenta técnica]**, **[!UICONTROL ID de organización]** para [agregar configuración en la instancia de autor de AEM](#add-configuration-in-the-aem-author-instance).
   ![recursos aem y adobe stock](/help/assets/assets/oauth-server-server-credentials-details-page.png)

### Agregar configuración en la instancia de autor [!DNL AEM] {#add-configuration-in-the-aem-author-instance}

Ejecute los siguientes pasos para agregar la configuración en su instancia de autor de [!DNL AEM]:

1. [Configurar un nuevo [!DNL Adobe Stock IMS configuration] en su [!DNL AEM] instancia de autor](#set-up-adobe-stock-ims-configuration-in-aem-author-instance)
1. [Agregar la configuración de nube para conectarse a  [!DNL Adobe Stock]](#add-cloud-configuration-to-connect-adobe-stock)

#### Configurar un(a) nuevo(a) [!DNL Adobe Stock IMS configuration] en su instancia [!DNL AEM author] {#set-up-adobe-stock-ims-configuration-in-aem-author-instance}

Ejecute los siguientes pasos para configurar un nuevo [!DNL Adobe Stock IMS configuration] en su instancia de autor de [!DNL AEM]:
1. Vaya a la instancia de autor [!DNL AEM].
1. Haga clic en ![recursos de AEM y Adobe Stock](/help/assets/assets/Hammer.svg), seleccione **[!UICONTROL Seguridad]** y **[!UICONTROL Configuraciones de IMS de Adobe]**.
1. Haga clic en **[!UICONTROL Crear]** para crear una nueva configuración de IMS. La página **[!UICONTROL Configuración de cuenta técnica de Adobe IMS]** muestra varios campos, como **[!UICONTROL Solución en la nube]**, **[!UICONTROL Título]**, **[!UICONTROL Servidor de autorización]**, **[!UICONTROL ID de cliente]**, **[!UICONTROL Secreto de cliente]**, **[!UICONTROL Ámbito]** e **[!UICONTROL ID de organización]**. Siga estas instrucciones para especificar los detalles en estos campos:
   * **[!UICONTROL Solución de nube]**: Seleccione **[!UICONTROL Adobe Stock]**.
   * **[!UICONTROL Título]**: especifique un nombre para esta integración.
   * **[!UICONTROL Servidor de autorización]**: Agregue [https://ims-na1.adobelogin.com/](https://ims-na1.adobelogin.com/) como servidor de autorización.
   * **[!UICONTROL ID de cliente]**: vaya a la página de **[!UICONTROL detalles de credenciales de servidor a servidor de OAuth]** de su proyecto, copie el **[!UICONTROL ID de cliente]** y péguelo aquí (consulte el paso 7 de la sección [Configurar un programa en Developer Console](#set-up-a-program-in-developer-console)).
   * **[!UICONTROL Secreto de cliente]**: Vaya a la página **[!UICONTROL Detalles de credencial de servidor a servidor OAuth]** de su proyecto y haga clic en **[!UICONTROL Recuperar secreto de cliente]**, copie el **[!UICONTROL secreto de cliente]** y péguelo aquí (consulte el paso 7 en la sección [Configurar un programa en Developer Console](#set-up-a-program-in-developer-console)).
   * **[!UICONTROL Ámbito]**: vaya a la página de **[!UICONTROL detalles de credenciales de servidor a servidor de OAuth]** de su proyecto, copie el **[!UICONTROL ámbito]** y péguelo aquí (consulte el paso 7 de la sección [Configurar un programa en Developer Console](#set-up-a-program-in-developer-console)).
   * **[!UICONTROL ID de organización]**: vaya a la página de **[!UICONTROL detalles de credenciales de servidor a servidor de OAuth]** de su proyecto, copie el **[!UICONTROL ID de organización]** y péguelo aquí (consulte el paso 7 de la sección [Configurar un programa en Developer Console](#set-up-a-program-in-developer-console)).
     ![recursos aem y adobe stock](/help/assets/assets/adobe-ims-technical-account-configuration.png)
1. Haga clic en **[!UICONTROL Crear]**, se abrirá la página **[!UICONTROL Configuraciones de IMS de Adobe]** y se mostrará la integración de [!DNL Adobe Stock] que ha creado.

#### Agregar la configuración de nube para conectarse a [!DNL Adobe Stock] {#add-cloud-configuration-to-connect-adobe-stock}

Ejecute los siguientes pasos para agregar la configuración de nube para conectarse a [!DNL Adobe Stock]:

1. Vaya a la instancia de [!DNL AEM author].
1. Haga clic en ![aem assets y Adobe Stock](/help/assets/assets/Hammer.svg), seleccione **[!UICONTROL Cloud Services]**, examine y seleccione **[!UICONTROL Adobe Stock]**.
   ![usando adobe stock con aem](/help/assets/assets/adding-cloud-config-to-adobe-stock.png)
1. Haga clic en **[!UICONTROL Crear]** y la página **[!UICONTROL Configuración de Adobe Stock]** mostrará varios campos. Siga estas instrucciones para especificar los detalles en estos campos:
   * **[!UICONTROL Título]**: especifique el mismo nombre de título utilizado en la página **[!UICONTROL Configuración de cuenta técnica de Adobe IMS]** al [configurar la configuración de Adobe Stock IMS en su instancia de autor de AEM](#set-up-adobe-stock-ims-configuration-in-aem-author-instance).
   * **[!UICONTROL Configuración de Adobe IMS asociada]**: seleccione la integración [!DNL Adobe Stock] que creó.
   * **[!UICONTROL Configuración regional]**: seleccione **[!UICONTROL Inglés (Estados Unidos)]**.
1. Haga clic en **[!UICONTROL Guardar y cerrar]**.
   ![usando adobe stock con aem](/help/assets/assets/adobe-stock-config-page.png)

<!--
### Configure cloud service {#configure-the-cloud-service}

To configure the [!DNL Adobe Stock] cloud service:

1. In the [!DNL Experience Manager] user interface, navigate to **[!UICONTROL Tools]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Adobe Stock]**.

1. In the [!DNL Adobe Stock Configurations] page, click **[!UICONTROL Create]**.

1. Specify a **[!UICONTROL Title]** for the cloud configuration. 

   Select the IMS configuration that you have created while [configuring the IMS account](#create-ims-account-configuration).

   Select your locale from the drop-down list.

   ![aem-stock-cloud-config](assets/aem-stock-cloud-config.png)

1. Click **[!UICONTROL Save & Close]**. 
-->
Su instancia de autor de [!DNL Experience Manager Assets] ahora está integrada con [!DNL Adobe Stock]. Puede crear varias configuraciones de [!DNL Adobe Stock] (por ejemplo, configuraciones basadas en la configuración regional). Ahora puede obtener acceso, buscar y obtener una licencia de los recursos de [!DNL Adobe Stock] desde la interfaz de usuario de [!DNL Experience Manager].

![search-stock-assets](assets/aem-stock-searchstocks.png)

>[!NOTE]
>
>En esta fase de integración, solamente los administradores pueden acceder a los recursos de [!DNL Adobe Stock], buscar recursos de Stock (mediante omnisearch) y obtener una licencia de los recursos de [!DNL Adobe Stock].
>
>Los administradores pueden agregar más usuarios o grupos al servicio en la nube [!DNL Adobe Stock] y dar permisos a estos usuarios que no son administradores en [!DNL Experience Manager] para que tengan acceso a la configuración de Stock.

1. Para agregar usuarios o grupos, seleccione la configuración de nube [!DNL Adobe Stock] y haga clic en **[!UICONTROL Propiedades]**.

1. Busque y añada los usuarios o grupos a los que ha asignado permisos para acceder a la configuración de Adobe Stock. Consulte [asignar permisos al grupo de usuarios](#assign-permissions-to-group).


## Asignar permisos al grupo de usuarios {#assign-permissions-to-group}

Los administradores pueden crear grupos de usuarios y conceder permisos a determinados usuarios o grupos para acceder al servicio en la nube [!DNL Adobe Stock].

A continuación se indican los permisos necesarios para que un usuario busque y conceda licencias a recursos de Adobe Stock:

* Configurar la ruta: `/conf/global/settings/stock`
* Privilegios: `jcr:read`
* Tipo de permiso: `Allow`

Puede crear un grupo de usuarios o asignar permisos a un grupo de usuarios existente. Los permisos se pueden asignar desde la interfaz [!DNL Experience Manager Assets] o desde la consola [!DNL User Admin].

**Para proporcionar acceso a un grupo de usuarios desde [!DNL Experience Manager]:**

1. En la interfaz de usuario de [!DNL Experience Manager], vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Seguridad]** > **[!UICONTROL Grupos]**. Crear un grupo de usuarios para [!DNL Adobe Stock].

1. Vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Seguridad]** > **[!UICONTROL Permisos]**.

1. Busque el grupo de usuarios en el panel izquierdo y agregue la nueva **[!UICONTROL Entrada de control de acceso (ACE)]** para Adobe Stock.

   * Configurar la ruta: `/conf/global/settings/stock`
   * Privilegios: `jcr:read`
   * Tipo de permiso: `Allow`

   Haga clic en **[!UICONTROL Agregar]**.

   ![permisos de usuario](assets/aem-stock-user-permissions.png)

1. Vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Adobe Stock]**. Seleccione la configuración de nube [!DNL Adobe Stock] y haga clic en **[!UICONTROL Propiedades]**.

1. Agregue el grupo de usuarios creado a la configuración [!DNL Adobe Stock]. Haga clic en **[!UICONTROL Guardar y cerrar]**.

   ![asignar-usuario](assets/aem-stock-adduser.png)

**Para proporcionar acceso a un usuario desde [!DNL User Admin Console]:**

1. Abra el Admin Console de usuario [!DNL Experience Manager]. La URL predeterminada es `http://localhost:4502/userdamin`.

1. En el panel izquierdo, busque el usuario al escribir `user_id` o `name`. Haga doble clic para abrir las propiedades del usuario.

1. Vaya a la pestaña **[!UICONTROL Permisos]** y permita los permisos de `read` para la configuración de nube de [!DNL Adobe Stock]: `/conf/global/settings/stock`.

   >[!CAUTION]
   >
   >Si no se permite la configuración en la nube, el usuario solo podrá obtener acceso a **[!UICONTROL Assets]** en la interfaz [!DNL Experience Manager].
   >
   >Para permitir el acceso a los recursos [!UICONTROL Assets] y [!DNL Adobe Stock], asegúrese de que la configuración de nube esté permitida para el usuario.

1. Haga clic en **[!UICONTROL Guardar]** para actualizar los permisos.

   ![assign-user-in-user-admin](assets/aem-stock-user-admin-console.png)

1. Agregue el usuario o el grupo a la configuración de nube [!DNL Adobe Stock].


## Acceso a recursos de Adobe Stock {#access-stock-assets}

Un usuario no administrador que tenga permisos para la configuración de nube de [!DNL Adobe Stock] puede buscar y obtener una licencia de los recursos de [!DNL Adobe Stock] desde la interfaz de [!DNL Experience Manager].

El usuario debe realizar un paso adicional para activar la configuración de nube de [!DNL Adobe Stock] antes de acceder a los recursos de [!DNL Adobe Stock]. Es una actividad única. Si al usuario se le asignan permisos en varias configuraciones de nube de [!DNL Adobe Stock], puede seleccionar la configuración que desee en **[!UICONTROL Preferencias de usuario]**.

Para activar la configuración de nube [!DNL Adobe Stock]:

1. Inicie sesión en [!DNL Experience Manager].

1. Haga clic en el icono de usuario en la esquina superior derecha y, a continuación, haga clic en **[!UICONTROL Mis preferencias]**. Se abre la ventana **[!UICONTROL Preferencias de usuario]**.

1. Seleccione la **[!UICONTROL Configuración de Stock]** que desee en la lista desplegable y haga clic en **[!UICONTROL Aceptar]** para activar la configuración.

   ![preferencias de usuario](assets/aem-stock-preferences.png)

1. Vaya a **[!UICONTROL Assets]** > **[!UICONTROL Adobe Stock]**. Ahora puede ver, buscar y obtener licencia de [!DNL Adobe Stock] recursos.

En la tabla siguiente se explica cómo funcionan los permisos de usuario al obtener acceso a los recursos de [!DNL Adobe Stock]:

| Usuario | Grupo | Permisos | Aceptar configuración de Stock en Preferencias de usuario | Acceso a Assets | Acceso a Adobe Stock |
| --- | --- | --- | --- | --- | --- |
| administrador | N/D | Todos | N/D | Sí | Sí |
| test-doc1 | Usuario DAM | /conf/global/settings/stock/cloud-config | Sí | Sí | Sí |
| test-doc1 | Usuario DAM | /conf/global/settings/stock/cloud-config | No | Error: Error al cargar los datos | No |
| test-doc1 | Usuario DAM | **permitir**: /conf/global/settings/stock **denegar**: /cloud-config | La configuración de Stock no es visible | Sí | No |

## Usar y administrar [!DNL Adobe Stock] recursos en [!DNL Experience Manager] {#usemanage}

Con esta capacidad, las organizaciones pueden permitir que sus usuarios trabajen con [!DNL Adobe Stock] recursos en [!DNL Experience Manager Assets]. Desde la interfaz de usuario de [!DNL Experience Manager], los usuarios pueden buscar [!DNL Adobe Stock] recursos y obtener la licencia de los recursos necesarios.

Una vez que un recurso de [!DNL Adobe Stock] tiene licencia en [!DNL Experience Manager], se puede usar y administrar como un recurso típico. En [!DNL Experience Manager], los usuarios pueden buscar y obtener una vista previa de los recursos; copiar y publicar los recursos; compartir los recursos en [!DNL Brand Portal]; acceder a los recursos y utilizarlos mediante la aplicación de escritorio de [!DNL Experience Manager], etc.

![Busque [!DNL Adobe Stock] recursos y filtre los resultados de su [!DNL Adobe Experience Manager] espacio de trabajo](assets/adobe-stock-search-results-workspace.png)

**A.** Busque recursos similares a los recursos cuyo identificador [!DNL Adobe Stock] se ha proporcionado. **B.** Busque recursos que coincidan con la selección de forma u orientación. **C.** Busque uno de los tipos de recurso **D.** más admitidos. Abra o contraiga la licencia del panel de filtros **E.** y guarde el recurso seleccionado en [!DNL Experience Manager] **F.** Guarde el recurso en [!DNL Experience Manager] con la marca de agua **G.** Explore los recursos del sitio web [!DNL Adobe Stock] que sean similares al recurso seleccionado **H.** Vea los recursos seleccionados en el sitio web [!DNL Adobe Stock]I.**Número de recursos seleccionados de los resultados de la búsqueda** J.**Cambiar entre la vista de tarjeta y la vista de lista**

### Buscar recursos {#find-assets}

Los usuarios de [!DNL Experience Manager] pueden buscar recursos en [!DNL Experience Manager] y [!DNL Adobe Stock]. Cuando la ubicación de búsqueda no está limitada a [!DNL Adobe Stock], se muestran los resultados de búsqueda de [!DNL Experience Manager] y [!DNL Adobe Stock].

* Para buscar [!DNL Adobe Stock] recursos, haga clic en **[!UICONTROL Navegación]** > **[!UICONTROL Assets]** > **[!UICONTROL Buscar Adobe Stock]**.

* Para buscar recursos en [!DNL Adobe Stock] y [!DNL Experience Manager Assets], haga clic en buscar ![buscar](assets/do-not-localize/search_icon.png).

También puede empezar a escribir `Location: Adobe Stock` en la barra de búsqueda para seleccionar [!DNL Adobe Stock] recursos. [!DNL Experience Manager] ofrece capacidades de filtrado avanzadas en los recursos buscados, lo que permite a los usuarios centrarse rápidamente en los recursos necesarios mediante filtros, como tipos de recursos admitidos, orientación de la imagen y estado con licencia.

>[!NOTE]
>
>Assets buscado desde [!DNL Adobe Stock] se muestra en [!DNL Experience Manager]. [!DNL Adobe Stock] recursos se recuperan y almacenan en el repositorio [!DNL Experience Manager] solo después de que un usuario [guarde un recurso](/help/assets/aem-assets-adobe-stock.md#saveassets) o [conceda licencias y guarde un recurso](/help/assets/aem-assets-adobe-stock.md#licenseassets). Las Assets que ya están almacenadas en [!DNL Experience Manager] se muestran y resaltan para facilitar la referencia y el acceso. Además, los recursos [!DNL Stock] se guardan con algunos metadatos adicionales para indicar el origen como [!DNL Stock].

![Filtros de búsqueda en [!DNL Experience Manager] y [!DNL Adobe Stock] recursos resaltados en los resultados de búsqueda](assets/aem-search-filters2.jpg)

### Guarde y vea los recursos necesarios {#saveassets}

Seleccione un recurso que desee guardar en [!DNL Experience Manager]. Haga clic en [!UICONTROL Guardar] en la barra de herramientas de la parte superior y proporcione el nombre y la ubicación del recurso. Los recursos sin licencia se guardan localmente con una marca de agua.

La próxima vez que busque recursos, los recursos guardados se resaltarán con un distintivo para indicar que están disponibles en [!DNL Experience Manager Assets].

>[!NOTE]
>
>Los recursos añadidos recientemente muestran un distintivo Nuevo en lugar de Distintivo con licencia.

### Recursos de licencia {#licenseassets}

Los usuarios pueden conceder licencias a [!DNL Adobe Stock] recursos mediante la cuota de su plan de empresa [!DNL Adobe Stock]. Al obtener la licencia de un recurso, este se guarda sin marca de agua y está disponible para buscarlo y utilizarlo en [!DNL Experience Manager Assets].

![Diálogo para autorizar y guardar [!DNL Adobe Stock] recursos en [!DNL Experience Manager Assets]](assets/aem-stock_licenseandsave.jpg)


### Acceso a metadatos y propiedades de recursos {#access-metadata-and-asset-properties}

Los usuarios pueden obtener acceso a los metadatos y obtener una vista previa de ellos, incluidas las propiedades de metadatos de [!DNL Adobe Stock] para los recursos guardados en [!DNL Experience Manager], y agregar **[!UICONTROL referencias de licencia]** para un recurso. Sin embargo, las actualizaciones de la referencia de licencia no se sincronizan entre [!DNL Experience Manager] y el sitio web [!DNL Adobe Stock].

Los usuarios pueden ver las propiedades de los recursos con y sin licencia.

![Ver y acceder a metadatos y referencias de licencia de recursos guardados](assets/metadata_properties.jpg)


## Limitaciones conocidas {#known-limitations}

* **La funcionalidad para restringir las licencias de los usuarios no funciona correctamente**: Todos los usuarios que tengan `read` permisos para la configuración de existencias pueden buscar y obtener licencias de los recursos [!DNL Adobe Stock].

* **Los usuarios que no son administradores tienen que activar manualmente la configuración en la nube de [!DNL Adobe Stock]**: en la ventana **[!UICONTROL Preferencias de usuario]**, la **[!UICONTROL Configuración de stock]** muestra la configuración en la nube de [!DNL Adobe Stock] como habilitada, pero no funciona para un usuario que no es administrador. El usuario debe hacer clic en el botón **[!UICONTROL Aceptar]** para activar la configuración de Stock. Si no se da este paso, el sistema mostrará un mensaje de error al acceder a **[!UICONTROL Assets]**.

* **No se muestra la advertencia de imagen editorial**: al autorizar una imagen, los usuarios no pueden comprobar si una imagen es de uso editorial solamente. Para evitar un posible uso incorrecto, los administradores pueden desactivar el acceso a los recursos editoriales desde Admin Console.

* **Se muestra un tipo de licencia incorrecto**: Es posible que se muestre un tipo de licencia incorrecto en [!DNL Experience Manager] para un recurso. Los usuarios pueden iniciar sesión en el sitio web de [!DNL Adobe Stock] para ver el tipo de licencia.

* **Los campos de referencia y los metadatos no están sincronizados**: Cuando un usuario actualiza un campo de referencia de licencia, la información de referencia de licencia se actualiza en [!DNL Experience Manager] pero no en el sitio web [!DNL Adobe Stock]. Del mismo modo, si el usuario actualiza los campos de referencia del sitio web [!DNL Adobe Stock], las actualizaciones no se sincronizan en [!DNL Experience Manager].

<!--
## Use and manage [!DNL Adobe Stock] assets in [!DNL Experience Manager] {#usemanage}

Using this capability, organizations users can work using [!DNL Adobe Stock] assets in [!DNL Experience Manager Assets]. From within the [!DNL Experience Manager] user interface, users can search [!DNL Adobe Stock] assets and license the required assets.

Once an [!DNL Adobe Stock] asset is licensed in [!DNL Experience Manager], it can be used and managed like a typical asset. In [!DNL Experience Manager], the users can search and preview the assets; copy and publish the assets; share the assets on [!DNL Brand Portal]; access and use the assets via [!DNL Experience Manager] desktop app; and so on.
-->

<!--  ![Search for Adobe Stock assets and filter results from your Adobe Experience Manager workspace](assets/adobe-stock-search-results-workspace.png)

*Figure: Search for [!DNL Adobe Stock] assets and filter results from your [!DNL Experience Manager] interface.*

**A.** Search assets similar to the assets whose [!DNL Adobe Stock] ID is provided. **B.** Search assets that match your selection of shape or orientation. **C.** Search for one of more supported asset types **D.** Open or collapse the filters pane **E.** License and save the selected asset in [!DNL Experience Manager] **F.** Save the asset in [!DNL Experience Manager] with watermark **G.** Explore assets on [!DNL Adobe Stock] website that are similar to the selected asset **H.** View the selected assets on [!DNL Adobe Stock] website **I.** Number of selected assets from the search results **J.** Switch between Card view and List view -->

<!--
### Find assets {#find-assets}

Your [!DNL Experience Manager] users, can search for assets in both, [!DNL Experience Manager] and [!DNL Adobe Stock]. When the search location is not limited to [!DNL Adobe Stock], the search results from [!DNL Experience Manager] and [!DNL Adobe Stock] are displayed.

* To search for [!DNL Adobe Stock] assets, click **[!UICONTROL Navigation]** > **[!UICONTROL Assets]** > **[!UICONTROL Search Adobe Stock]**.

* To search for assets across [!DNL Adobe Stock] and [!DNL Experience Manager Assets], click search ![search](assets/do-not-localize/search_icon.png).

Alternatively, start typing `Location: Adobe Stock` in the search bar to select [!DNL Adobe Stock] assets. [!DNL Experience Manager] offers advanced filtering capabilities on the searched assets, allowing users to quickly zero-in on the required assets using filters, such as types of supported assets, image orientation, and licensed state.

>[!NOTE]
>
>Assets searched from [!DNL Adobe Stock] are just displayed in [!DNL Experience Manager]. [!DNL Adobe Stock] assets are fetched and stored in [!DNL Experience Manager] repository only after a user either [saves an asset](/help/assets/aem-assets-adobe-stock.md#saveassets) or [licenses and saves an asset](/help/assets/aem-assets-adobe-stock.md#licenseassets). Assets that are already stored in [!DNL Experience Manager] are displayed and highlighted for ease of reference and access. Also, the [!DNL Stock] assets are saved with some additional metadata to indicate the source as [!DNL Stock].

![Search filters in Experience Manager and highlighted Adobe Stock assets in search results](assets/aem-search-filters2.jpg)

*Figure: Search filters in [!DNL Experience Manager] and highlighted [!DNL Adobe Stock] assets in search results.*

### Save and view the required assets {#saveassets}

Select an asset that you want to save in [!DNL Experience Manager]. Click [!UICONTROL Save] in the toolbar at the top and provide the name and location of the asset. The unlicensed assets are saved locally with a watermark.

Next time when you search for assets, the saved assets are highlighted with a badge, to indicate that such assets are available in [!DNL Experience Manager Assets].

>[!NOTE]
>
>The recently added assets display a New badge instead of Licensed badge.

### License assets {#licenseassets}

Users can license [!DNL Adobe Stock] assets by using the quota of their [!DNL Adobe Stock] enterprise plan. When you license an asset, it is saved without a watermark and is available for searching and using in [!DNL Experience Manager Assets].

![Dialog to license and save Adobe Stock assets in Experience Manager Assets](assets/aem-stock_licenseandsave.jpg)

*Figure: Dialog to license and save [!DNL Adobe Stock] assets in [!DNL Experience Manager Assets].*

### Access metadata and asset properties {#access-metadata-and-asset-properties}

Users can access and preview the metadata, including the [!DNL Adobe Stock] metadata properties for the assets saved in [!DNL Experience Manager], and add **[!UICONTROL License References]** for an asset. However, the updates to license reference are not synced between [!DNL Experience Manager] and [!DNL Adobe Stock] website.

Users can see the properties for both, licensed and unlicensed assets.

![View and access metadata and license references of saved assets](assets/metadata_properties.jpg)

*Figure: View and access metadata and license references of saved assets.*

## Known limitations {#known-limitations}

* **Editorial image warning is not displayed**: When licensing an image, users cannot check if an image is Editorial Use Only. To prevent possible misuse, the administrators can turn off the access to editorial assets from the Admin Console.

* **Wrong license type is displayed**: It is possible that an incorrect license type is displayed in [!DNL Experience Manager] for an asset. Users can log into the [!DNL Adobe Stock] website to see the license type.

* **Reference fields and metadata are not synced**: When a user updates a license reference field, the license reference information is updated in [!DNL Experience Manager] but not on the [!DNL Adobe Stock] website. Similarly, if the user updates the reference fields on the [!DNL Adobe Stock] website, the updates are not synchronized in [!DNL Experience Manager].
-->

**Consulte también**

* [Traducir recursos](translate-assets.md)
* [API HTTP de recursos](mac-api-assets.md)
* [Formatos de archivo compatibles con recursos](file-format-support.md)
* [Buscar recursos](search-assets.md)
* [Recursos de red](use-assets-across-connected-assets-instances.md)
* [Informes de recurso](asset-reports.md)
* [Esquemas de metadatos](metadata-schemas.md)
* [Descarga de recursos](download-assets-from-aem.md)
* [Administración de metadatos](manage-metadata.md)
* [Facetas de búsqueda](search-facets.md)
* [Administrar colecciones](manage-collections.md)
* [Importación masiva de metadatos](metadata-import-export.md)
* [Publicación de recursos en AEM y Dynamic Media](/help/assets/publish-assets-to-aem-and-dm.md)

>[!MORELIKETHIS]
>
>* [Tutorial de vídeo sobre el uso de recursos de Adobe Stock con Experience Manager Assets](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/creative-workflows/adobe-stock.html)
>* [Ayuda del plan empresarial de Adobe Stock](https://helpx.adobe.com/enterprise/using/adobe-stock-enterprise.html)
>* [Preguntas frecuentes sobre Adobe Stock](https://helpx.adobe.com/stock/faq.html)
