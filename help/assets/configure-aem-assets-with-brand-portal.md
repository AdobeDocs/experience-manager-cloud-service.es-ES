---
title: Configuración de AEM Assets as a [!DNL Cloud Service] con Brand Portal
description: Obtenga información sobre cómo configurar AEM Assets con Brand Portal. La configuración le permite publicar recursos de marca aprobados de una instancia de AEM en Brand Portal y distribuirlos a los usuarios de Brand Portal.
contentOwner: AK
feature: Brand Portal, Asset Distribution, Configuration
role: Admin
exl-id: 078e522f-bcd8-4734-95db-ddc8772de785
source-git-commit: 32fdbf9b4151c949b307d8bd587ade163682b2e5
workflow-type: tm+mt
source-wordcount: '663'
ht-degree: 22%

---

# Configurar Experience Manager Assets con Brand Portal {#configure-aem-assets-with-brand-portal}

| Versión | Vínculo del artículo |
| -------- | ---------------------------- |
| AEM 6.5 | [Haga clic aquí](https://experienceleague.adobe.com/docs/experience-manager-65/assets/brandportal/configure-aem-assets-with-brand-portal.html?lang=es) |
| AEM as a Cloud Service | Este artículo |

La configuración de Adobe Experience Manager Assets Brand Portal permite publicar recursos de marca aprobados de Adobe Experience Manager Assets como una instancia de [!DNL Cloud Service] en Brand Portal y distribuirlos a los usuarios de Brand Portal.

>[!IMPORTANT]
>
> * Brand Portal está en modo de mantenimiento. Todas las innovaciones de productos nuevos están disponibles en [Content Hub](/help/assets/product-overview.md).
> * Si todavía necesita activar Brand Portal, póngase en contacto con su representante de Adobe e incluya información sobre su caso de uso y otros requisitos específicos.
> * Brand Portal no está disponible con [Assets Prime](/help/assets/assets-prime.md) ni con [Assets Ultimate](/help/assets/assets-ultimate-overview.md). Sin embargo, los clientes existentes de Assets as a Cloud Service que ya tienen acceso a Brand Portal pueden conservarlo cuando realicen la transición a Assets Ultimate.

<!--

## Activate Brand Portal using Cloud Manager {#activate-brand-portal}

The Cloud Manager user activates Brand Portal for an Experience Manager Assets as a [!DNL Cloud Service] instance. The activation workflow creates the required configurations (authorization token, IMS configuration, and Brand Portal cloud service) at the backend and reflects the status of the Brand Portal tenant in Cloud Manager. Activating Brand Portal enables the Experience Manager Assets users to publish assets to Brand Portal and distribute them to the Brand Portal users.  

**Prerequisites** 

You require the following to activate Brand Portal on your Experience Manager Assets as a [!DNL Cloud Service] instance:

* An up and running Experience Manager Assets as a [!DNL Cloud Service] instance.
* A user having access to Cloud Manager, assigned to Profiles of the Cloud Manager Product. See [accessing Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/security/ims-support.html?lang=es#accessing-cloud-manager) for more information. 

>[!NOTE]
>
>A configured production environment is required to an Experience Manager Assets as a [!DNL Cloud Service] instance to connect with Brand Portal tenant.

**Steps to activate Brand Portal**

You can activate Brand Portal while creating the production environments for your Experience Manager Assets as a [!DNL Cloud Service] instance, or separately. Let us assume that the environment was already created, and you are now required to activate Brand Portal.

1. Login to Adobe Cloud Manager and navigate to **[!UICONTROL Environments]**.
   
   The **[!UICONTROL Environments]** page displays the list of all the existing environments.

1. Select the environments (one by one) from the list to view the environment details.

   Brand Portal is entitled to one of the available environments and is reflected under the **[!UICONTROL Environment Information]**.

   Once you find the environment associated with Brand Portal, click the **[!UICONTROL Activate Brand Portal]** button to begin the activation workflow.

   ![Activate Brand Portal](assets/create-environment4.png)

1. It takes few mins to activate the Brand Portal tenant as the activation workflow creates the required configurations at the backend. Once the Brand Portal tenant is activated, the status changes to Activated. 

   ![View Status](assets/create-environment5.png)


>[!NOTE]
>
>Brand Portal must be activated on the same IMS org as of the Experience Manager Assets as a [!DNL Cloud Service] instance.
>
>If you have an existing Brand Portal cloud configuration ([manually configured using Adobe Developer Console](#manual-configuration)) for an IMS org (org1-existing) and your Experience Manager Assets as a [!DNL Cloud Service] instance is configured for another IMS org (org2-new), activating Brand Portal from the Cloud Manager resets the Brand Portal IMS org to `org2-new`. Although the manually configured cloud configuration on `org1-existing` is visible in the Experience Manager Assets author instance but will no longer be in use after activating Brand Portal from the Cloud Manager. 
>
>If the existing Brand Portal cloud configuration and Experience Manager Assets as a [!DNL Cloud Service] instance are using the same IMS org (org1), you only have to activate Brand Portal from the Cloud Manager. 
>
>Do not modify any autogenerated settings.

**See also**:

* [Add users and roles in Experience Manager Assets as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/requirements/setting-up-users-and-roles.html?lang=es)

* [Manage environments in Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/manage-environments.html?lang=es#adding-environments)


**Login to your Brand Portal tenant**:

After activation of your Brand Portal tenant in Cloud Manager, you can login to Brand Portal from Admin Console or by directly using the tenant URL.

The default URL of your Brand Portal tenant is: `https://<tenant-id>.brand-portal.adobe.com/`.

Wherein, the Tenant id is the IMS org.


Perform the following steps if you are not sure of the Brand Portal URL:

1. Login to [Admin Console](https://adminconsole.adobe.com/) and navigate to **[!UICONTROL Products]**.
1. From the left panel, select **[!UICONTROL Adobe Experience Manager Brand Portal – Brand Portal]**.
1. Click **[!UICONTROL Go to Brand Portal]** to directly open Brand Portal in the browser.

   Or copy the Brand Portal tenant URL from the **[!UICONTROL Go to Brand Portal]** link and paste it in your browser to open the Brand Portal interface.

   ![Access Brand Portal](assets/access-bp-on-cloud.png)


**Test connection**

Perform the following steps to validate the connection between your Experience Manager Assets as a [!DNL Cloud Service] instance and Brand Portal tenant:

1. Login to Experience Manager Assets.

1. From the **Tools** panel, navigate to **[!UICONTROL Deployment]** > **[!UICONTROL Distribution]**.

    ![Navigate to the distribution option](assets/test-bpconfig1.png)

   A Brand Portal distribution agent (**[!UICONTROL bpdistributionagent0]**) is created under **[!UICONTROL Publish to Brand Portal]**.

   ![Create distribution agent](assets/test-bpconfig2.png)

1. Click **[!UICONTROL Publish to Brand Portal]** to open the distribution agent. 

   You can see the distribution queues under the **[!UICONTROL Status]** tab. 
   
   A distribution agent contains two queues: 
   * **processing-queue**: for the distribution of assets to Brand Portal. 

   * **error-queue**: for the assets where distribution has failed. 
   
   >[!NOTE]
   >
   >It is recommended to review the failures and  clear the **error-queue** periodically.  

   ![Processing queue for the distribution of assets](assets/test-bpconfig3.png)

1. To verify the connection between Experience Manager Assets as a [!DNL Cloud Service] and Brand Portal, click the **[!UICONTROL Test Connection]** icon.

   ![Verify connection between AEM and Brand Portal](assets/test-bpconfig4.png)

   A message appears that your *test package is successfully delivered*.

   >[!NOTE]
   >
   >Avoid disabling the distribution agent, as it can cause the distribution of the assets (running-in-queue) to fail.

To verify the connection between your Experience Manager Assets as a [!DNL Cloud Service] instance and Brand Portal tenant, publish an asset from Experience Manager Assets to Brand Portal. If the connection is successful, the published asset is visible in the Brand Portal interface.


You can now:

* [Publish assets from Experience Manager Assets to Brand Portal](publish-to-brand-portal.md)
* [Publish folders from Experience Manager Assets to Brand Portal](publish-to-brand-portal.md#publish-folders-to-brand-portal)
* [Publish collections from Experience Manager Assets to Brand Portal](publish-to-brand-portal.md#publish-collections-to-brand-portal)
* [Publish assets from Brand Portal to Experience Manager Assets](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/asset-sourcing-in-brand-portal/brand-portal-asset-sourcing.html?lang=es) - Asset Sourcing in Brand Portal
* [Publish presets, schemas, and facets to Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/publish/publish-schema-search-facets-presets.html?lang=es)
* [Publish tags to Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/publish/brand-portal-publish-tags.html?lang=es)

See [Brand Portal documentation](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/home.html?lang=es) for more information.

**Distribution logs**

You can monitor the distribution agent logs for the asset publishing workflow. 

Let us now publish an asset from Experience Manager Assets to Brand Portal and see the logs. 

1. Follow the steps (from 1 to 4) as shown in the **Test connection** section and navigate to the distribution agent page.
1. Click **[!UICONTROL Logs]** to view the processing and error logs.

   ![Processing and error logs](assets/test-bpconfig5.png)

The distribution agent has generated the following logs:

* INFO: It is a system-generated log that triggers on successful configuration of the distribution agent. 
* DSTRQ1 (Request 1): Triggers on test connection.

On publishing the asset, the following request and response logs are generated:

**Distribution agent request**:

* DSTRQ2 (Request 2): The asset publishing request is triggered.
* DSTRQ3 (Request 3): The system triggers another request to publish the Experience Manager Assets folder (in which the asset exists) and replicates the folder in Brand Portal.

**Distribution agent response**:

* queue-bpdistributionagent0 (DSTRQ2): The asset is published to Brand Portal.
* queue-bpdistributionagent0 (DSTRQ3): The system replicates the Experience Manager Assets folder (containing the asset) in Brand Portal.

In the above example, an additional request and response are triggered. The system could not find the parent folder (Add Path) in Brand Portal because the asset was published for the first time, therefore, it triggered an additional request to create a parent folder with the same name in Brand Portal where the asset is published.  

>[!NOTE]
>
>Additional request is generated in case the parent folder does not exist in Brand Portal or has been modified in Experience Manager Assets. 

Along with the automation workflow to activate Brand Portal on Experience Manager Assets as a [!DNL Cloud Service], there exists another method to manually configure Experience Manager Assets as a [!DNL Cloud Service] with Brand Portal using Adobe Developer Console which is not recommended anymore.

>[!NOTE]
>
>Contact Customer Support if you are facing any problem while activating your Brand Portal tenant.
-->

## Configuración manual con Adobe Developer Console {#manual-configuration}

>[!NOTE]
>
> No puede crear nuevas credenciales de JWT a partir de junio de 2024. A partir de ahora, solo se crean credenciales de OAuth.
> &#x200B;> Ver más [creando una configuración de OAuth](https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/security/setting-up-ims-integrations-for-aem-as-a-cloud-service#creating-oauth-configuration:~:text=For%20example%3A-,Creating%20an%20OAuth%20configuration,-To%20create%20a).

En la siguiente sección se describe cómo configurar manualmente Experience Manager Assets as a [!DNL Cloud Service] con Brand Portal mediante Adobe Developer Console.

Anteriormente, Experience Manager Assets as a [!DNL Cloud Service] se configuraba manualmente con Brand Portal a través de Adobe Developer Console, que obtiene un token de cuenta de Adobe Identity Management Services (IMS) para la autorización del inquilino de Brand Portal. Requiere configuraciones tanto en Experience Manager Assets como en Adobe Developer Console.

<!--1. In Experience Manager Assets, create an IMS account and generate a public key (certificate).-->
<!--1. Under the project, configure an API using the public key to create a service account connection.
1. Get the service account credentials and JSON Web Token (JWT) payload information.
1. In Experience Manager Assets, configure the IMS account using the service account credentials and JWT payload.-->
1. En Adobe Developer Console, cree un proyecto para el inquilino (organización) de Brand Portal.
1. En Experience Manager Assets, configure el servicio en la nube de Brand Portal con la cuenta de IMS y el punto final de Brand Portal (URL de la organización).
1. Pruebe la configuración publicando un recurso de Experience Manager Assets en Brand Portal.

>[!NOTE]
>
>Una instancia de Experience Manager Assets as a [!DNL Cloud Service] solo se debe configurar con un usuario de Brand Portal.

**Requisitos previos**

Para configurar Experience Manager Assets con Brand Portal, es necesario lo siguiente:

* Una instancia de Experience Manager Assets como [!DNL Cloud Service] en ejecución
* Una URL de inquilino de Brand Portal
* Un usuario con privilegios de administrador del sistema en la organización IMS del inquilino de Brand Portal

## Crear configuración {#create-new-configuration}

Siga estos pasos en la secuencia especificada para configurar Experience Manager Assets con Brand Portal.

1. [Configuración de las credenciales de OAuth en Adobe Developer Console](#config-oauth)
1. [Creación de una nueva integración de Adobe IMS mediante OAuth](#create-ims-account-configuration)
1. [Configurar el servicio en la nube](#configure-cloud-service)
   <!--1. [Obtain public certificate](#public-certificate)-->
<!--1. [Create service account (JWT) connection](#createnewintegration) 
1. [Configure IMS account](#create-ims-account-configuration)-->

<!--
### Create IMS configuration {#create-ims-configuration}

The IMS configuration authenticates your Experience Manager Assets as a [!DNL Cloud Service] instance with the Brand Portal tenant. 

IMS configuration includes two steps:

* [Obtain public certificate](#public-certificate) 
* [Configure IMS account](#create-ims-account-configuration)
-->
<!--

### Obtain public certificate {#public-certificate}

The public key (certificate) authenticates your profile on Adobe Developer Console.

1. Login to Experience Manager Assets.
1. From the **Tools** panel, navigate to **[!UICONTROL Security]** > **[!UICONTROL Adobe IMS Configurations]**.
1. In Adobe IMS Configurations page, click **[!UICONTROL Create]**. It will redirect to the **[!UICONTROL Adobe IMS Technical Account Configuration]** page. By default, the **Certificate** tab opens.
1. Select **[!UICONTROL Adobe Brand Portal]** in the **[!UICONTROL Cloud Solution]** drop-down list.  
1. Select the **[!UICONTROL Create new certificate]** check box and specify an **alias** for the public key. The alias serves as name of the public key. 
1. Click **[!UICONTROL Create certificate]**. Then, click **[!UICONTROL OK]** to generate the public key.

   ![Create Certificate](assets/ims-config2.png)

1. Click the **[!UICONTROL Download Public Key]** icon and save the public key (CRT) file on your machine.

   The public key is used later to configure API for your Brand Portal tenant and generate service account credentials in Adobe Developer Console.  

   ![Download Certificate](assets/ims-config3.png)

1. Click **[!UICONTROL Next]**.

    In the **Account** tab, Adobe IMS account is created which requires the service account credentials that are generated in Adobe Developer Console. Keep this page open for now.

    Open a new tab and [create a service account (JWT) connection in Adobe Developer Console](#createnewintegration) to get the credentials and JWT payload for configuring the IMS account. 
-->
<!--

### Create service account (JWT) connection {#createnewintegration}

In Adobe Developer Console, projects and APIs are configured at Brand Portal tenant (organization) level. Configuring an API creates a service account (JWT) connection. There are two methods to configure API, by generating a key pair (private and public keys) or by uploading a public key. To configure Experience Manager Assets with Brand Portal, you must generate a public key (certificate) in Experience Manager Assets and create credentials in Adobe Developer Console by uploading the public key. These credentials are required to configure the IMS account in Experience Manager Assets. Once the IMS account is configured, you can configure the Brand Portal cloud service in Experience Manager Assets.

Perform the following steps to generate the service account credentials and JWT payload:

1. Login to Adobe Developer Console with system administrator privileges on the IMS organization (Brand Portal tenant). The default URL is [https://www.adobe.com/go/devs_console_ui](https://www.adobe.com/go/devs_console_ui).


   >[!NOTE]
   >
   >Ensure that you have selected the correct IMS organization (Brand Portal tenant) from the drop-down (organization) list located at the upper-right corner.

1. Click **[!UICONTROL Create new project]**. A blank project with a system-generated name is created for your organization. 

   Click **[!UICONTROL Edit project]** to update the **[!UICONTROL Project Title]** and **[!UICONTROL Description]**, and click **[!UICONTROL Save]**.
   
1. In the **[!UICONTROL Project overview]** tab, click **[!UICONTROL Add API]**.

1. In the **[!UICONTROL Add an API window]**, select **[!UICONTROL AEM Brand Portal]** and click **[!UICONTROL Next]**. 

   Ensure that you have access to the Experience Manager Brand Portal service.

1. In the **[!UICONTROL Configure API]** window, click **[!UICONTROL Upload your public key]**. Then, click **[!UICONTROL Select a File]** and upload the public key (.crt file) that you have downloaded in the [obtain public certificate](#public-certificate) section. 

   Click **[!UICONTROL Next]**.

   ![Upload Public Key](assets/service-account3.png)

1. Verify the public key and click **[!UICONTROL Next]**.

1. Select **[!UICONTROL Assets Brand Portal]** as the default product profile and click **[!UICONTROL Save configured API]**. 

   ![Select Product Profile](assets/service-account4.png)

1. Once the API is configured, you are redirected to the API overview page. From the left navigation under **[!UICONTROL Credentials]**, click the **[!UICONTROL Service Account (JWT)]** option.

   >[!NOTE] 
   >
   >* You can view the credentials and perform actions such as generate JWT tokens, copy credential details, retrieve client secret, and so on.
   >* Currently, only the Adobe's Developer Console Service Account (JWT) credential type is supported. Do not use the `OAuth Server-to-Server` credential type until it is supported in mid-April. Read more at [JWT Credentials Deprecation in Adobe Developer Console](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/security/jwt-credentials-deprecation-in-adobe-developer-console.html?lang=es).

1. From the **[!UICONTROL Client Credentials]** tab, copy the **[!UICONTROL client ID]**. 

   Click **[!UICONTROL Retrieve Client Secret]** and copy the **[!UICONTROL client secret]**.

   ![Service Account Credentials](assets/service-account5.png)

1. Navigate to the **[!UICONTROL Generate JWT]** tab and copy the **[!UICONTROL JWT Payload]** information. 

You can now use the client ID (API key), client secret, and JWT payload to [configure the IMS account](#create-ims-account-configuration) in Experience Manager Assets.
-->
<!--
1. Click **[!UICONTROL Create Integration]**.

1. Select **[!UICONTROL Access an API]**, and click **[!UICONTROL Continue]**.

   ![Create New Integration](assets/create-new-integration1.png)

1. Create an integration page. 
   
   Select your organization from the drop-down list.

   In **[!UICONTROL Experience Cloud]**, Select **[!UICONTROL AEM Brand Portal]** and click **[!UICONTROL Continue]**. 

   If the Brand Portal option is disabled for you, ensure that you have selected correct organization from the drop-down box above the **[!UICONTROL Adobe Services]** option. If you do not know your organization, contact your administrator.

   ![Create Integration](assets/create-new-integration2.png)

1. Specify a name and description for the integration. Click **[!UICONTROL Select a File from your computer]** and upload the `AEM-Adobe-IMS.crt` file downloaded in the [obtain public certificates](#public-certificate) section.

1. Select the profile of your organization. 

   Or, select the default profile **[!UICONTROL Assets Brand Portal]** and click **[!UICONTROL Create Integration]**. The integration is created.

1. Click **[!UICONTROL Continue to integration details]** to view the integration information. 

   Copy the **[!UICONTROL API Key]** 
   
   Click **[!UICONTROL Retrieve Client Secret]** and copy the Client Secret key.

   ![API Key, Client Secret, and payload information of an integration](assets/create-new-integration3.png)

1. Navigate to **[!UICONTROL JWT]** tab, and copy the **[!UICONTROL JWT payload]**.

   The API Key, Client Secret key, and JWT payload information is used to create IMS account configuration.

-->

### Configuración de las credenciales de OAuth en Adobe Developer Console {#config-oauth}

[Configure las credenciales de OAuth en Adobe Developer Console](https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/security/setting-up-ims-integrations-for-aem-as-a-cloud-service#credentials-in-the-developer-console) y seleccione la API de Brand Portal.

### Creación de una nueva integración de Adobe IMS con OAuth {#create-ims-account-configuration}

[Cree una nueva integración de IMS de Adobe con OAuth](https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/security/setting-up-ims-integrations-for-aem-as-a-cloud-service#creating-oauth-configuration) y seleccione Brand Portal en el menú desplegable en Solución de nube.

<!--
Ensure that you have performed the following steps:

* [Obtain public certificate](#public-certificate)
* [Create service account (JWT) connection](#createnewintegration)
-->

<!--1. Open the IMS Configuration and navigate to the **[!UICONTROL Account]** tab. Keep the page open while [obtaining the public certificate](#public-certificate).

1. Specify a **[!UICONTROL Title]** for the IMS account.

   In the **[!UICONTROL Authorization Server]** field, specify the URL: [https://ims-na1.adobelogin.com/](https://ims-na1.adobelogin.com/)  
-->
<!--
1. Complete the configuration based on details from the [Developer Console](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/implementation/). Click **[!UICONTROL Create]**.
-->
<!--Specify client ID in the **[!UICONTROL API key]** field, **[!UICONTROL Client Secret]**, and **[!UICONTROL Payload]** (JWT payload) that you have copied while [creating the service account (JWT) connection](#createnewintegration).

   The IMS account is configured. 

   ![IMS Account configuration](assets/create-new-integration6.png)

 <!--  
1. Select the IMS account configuration and click **[!UICONTROL Check Health]**.

   Click **[!UICONTROL Check]** in the dialog box. On successful configuration, a message appears that the *Token is retrieved successfully*.

   ![Adobe IMS Configurations Check Health.](assets/create-new-integration5.png)
-->
<!--
>[!CAUTION]
>
>You must have only one IMS configuration.
>
>Ensure that the IMS configuration passes the health check. If the configuration does not pass the health check, it is invalid. You must delete it and create another valid configuration.
-->

### Configurar servicio en la nube {#configure-cloud-service}

Siga estos pasos para configurar el servicio en la nube de Brand Portal:

1. Inicie sesión en Experience Manager Assets.

1. En el panel **Herramientas**, vaya a **[!UICONTROL Cloud Services]** > **[!UICONTROL AEM Brand Portal]**.

1. En la página Configuraciones de Brand Portal, haga clic en **[!UICONTROL Crear]**.

1. Especifique un **[!UICONTROL Título]** para la configuración.

   Seleccione la configuración de IMS que creó al [configurar la cuenta de IMS](#create-ims-account-configuration).

   En el campo **[!UICONTROL URL de servicio]**, especifique la URL del inquilino (organización) de Brand Portal.

   ![Cuadro de diálogo Configuración de Brand Portal.](assets/create-cloud-service.png)

1. Haga clic en **[!UICONTROL Guardar y cerrar]**. Se crea la configuración de nube.

   Su instancia de Experience Manager Assets as a [!DNL Cloud Service] ahora está configurada con el inquilino de Brand Portal.

Ahora puede probar la configuración comprobando el agente de distribución y publicando los recursos en Brand Portal.

**IP de salida de Lista de permitidos en SPS si la vista previa segura está habilitada**
Si utiliza Dynamic Media-Scene7 con [vista previa segura habilitada](#https://experienceleague.adobe.com/docs/dynamic-media-classic/using/upload-publish/testing-assets-making-them-public.html?lang=es) para una empresa, se recomienda que el administrador de la empresa de Scene7 [lista de permitidos las IP de salida públicas](#https://experienceleague.adobe.com/docs/dynamic-media-classic/using/upload-publish/testing-assets-making-them-public.html?lang=es#testing-the-secure-testing-service) para las regiones respectivas mediante la interfaz de usuario Flash de SPS (Scene7 Publishing System).
Las direcciones IP de salida son las siguientes:

| **Región** | **IP de salida** |
|--- |--- |
| ND | 130.248.160.68, 20.94.203.130 |
| EMEA | 51.132.146.75, 130.248.244.202, 130.248.244.203, 130.248.244.204, 130.248.244.210, 130.248.244.211, 130.248.244.212 |
| APAC | 63.140.44.54 |

<!--
### Test configuration {#test-configuration}

Perform the following steps to validate the configuration:

1. Login to AEM Assets.

1. From the **Tools** panel, navigate to **[!UICONTROL Deployment]** > **[!UICONTROL Distribution]**.

    ![test-bpconfig1](assets/test-bpconfig1.png)

   A Brand Portal distribution agent (**[!UICONTROL bpdistributionagent0]**) is created under **[!UICONTROL Publish to Brand Portal]**.

   ![test-bpconfig2](assets/test-bpconfig2.png)


1. Click **[!UICONTROL Publish to Brand Portal]** to open the distribution agent. 

   You can see the distribution queues under the **[!UICONTROL Status]** tab. 
   
   A distribution agent contains two queues: 
   * **processing-queue**: for the distribution of assets to Brand Portal. 

   * **error-queue**: for the assets where distribution has failed. 
   
   >[!NOTE]
   >
   >It is recommended to review the failures and  clear the **error-queue** periodically.  

   ![test-bpconfig3](assets/test-bpconfig3.png)

1. To verify the connection between AEM Assets as a [!DNL Cloud Service] and Brand Portal, click the **[!UICONTROL Test Connection]** icon.

   ![test-bpconfig4](assets/test-bpconfig4.png)

   A message appears that your *test package is successfully delivered*.

   >[!NOTE]
   >
   >Avoid disabling the distribution agent, as it can cause the distribution of the assets (running-in-queue) to fail.

You can now:

* [Publish assets from AEM Assets to Brand Portal](publish-to-brand-portal.md)
* [Publish folders from AEM Assets to Brand Portal](publish-to-brand-portal.md#publish-folders-to-brand-portal)
* [Publish collections from AEM Assets to Brand Portal](publish-to-brand-portal.md#publish-collections-to-brand-portal)
* [Publish assets from Brand Portal to AEM Assets](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/asset-sourcing-in-brand-portal/brand-portal-asset-sourcing.html?lang=es) - Asset Sourcing in Brand Portal
* [Publish presets, schemas, and facets to Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/publish/publish-schema-search-facets-presets.html?lang=es)
* [Publish tags to Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/publish/brand-portal-publish-tags.html?lang=es)

See [Brand Portal documentation](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/home.html?lang=es) for more information.

## Distribution logs {#distribution-logs}

You can monitor the distribution agent logs for the asset publishing workflow. 

For example, we have published an asset from AEM Assets to Brand Portal to validate the configuration. 

1. Follow the steps (from 1 to 4) as shown in the [Test Configuration](#test-configuration) section and navigate to the distribution agent page.
1. Click **[!UICONTROL Logs]** to view the processing and error logs.

   ![ctest-bpconfig4](assets/ctest-bpconfig4.png)

The distribution agent has generated the following logs:

* INFO: This is a system-generated log that triggers on successful configuration of the distribution agent. 
* DSTRQ1 (Request 1): Triggers on test connection.

On publishing the asset, the following request and response logs are generated:

**Distribution agent request**:

* DSTRQ2 (Request 2): The asset publishing request is triggered.
* DSTRQ3 (Request 3): The system triggers another request to publish the AEM Assets folder (in which the asset exists) and replicates the folder in Brand Portal.

**Distribution agent response**:

* queue-bpdistributionagent0 (DSTRQ2): The asset is published to Brand Portal.
* queue-bpdistributionagent0 (DSTRQ3): The system replicates the AEM Assets folder (containing the asset) in Brand Portal.

In the above example, an additional request and response is triggered. The system could not find the parent folder (Add Path) in Brand Portal because the asset was published for the first time, therefore, it triggered an additional request to create a parent folder with the same name in Brand Portal where the asset is published.  

>[!NOTE]
>
>Additional request is generated in case the parent folder does not exist in Brand Portal or has been modified in AEM Assets. 
-->

<!--

## Additional information {#additional-information}

Go to `/system/console/slingmetrics` for statistics related to the distributed content:

1. **Counter metrics**
   * sling: `mac_sync_request_failure`
   * sling: `mac_sync_request_received`
   * sling: `mac_sync_request_success`

1. **Time metrics**
   * sling: `mac_sync_distribution_duration`
   * sling: `mac_sync_enqueue_package_duration`
   * sling: `mac_sync_setup_request_duration`

-->

<!--
   Comment Type: draft

   <li> </li>
   -->

<!--
   Comment Type: draft

   <li>Step text</li>
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
