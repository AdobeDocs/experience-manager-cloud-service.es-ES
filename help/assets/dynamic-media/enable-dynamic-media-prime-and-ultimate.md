---
title: Habilitar [!DNL Dynamic Media] Prime y Ultimate
description: Obtenga información sobre cómo habilitar  [!DNL Dynamic Media] ofertas de Prime y Ultimate.
feature: Asset Management
role: User, Admin
exl-id: 0ee161f5-bf44-41f1-928e-c07574fd43cc
source-git-commit: 82a3016149645701abe829ad89c493f480956267
workflow-type: tm+mt
source-wordcount: '1075'
ht-degree: 4%

---

# Habilitar [!DNL Dynamic Media] Prime y Ultimate {#enable-dynamic-media-prime-and-ultimate}

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
            <a href="/help/assets/search-best-practices.md"><b>Prácticas recomendadas de búsqueda</b></a>
        </td>
    </tr>
    <tr>
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

[!DNL Adobe Experience Manager] as a Cloud Service le permite acceder a las ofertas de [!DNL Dynamic Media] Prime y Ultimate para optimizar sus flujos de trabajo digitales y la administración de contenido. Consulte [Dynamic Media Prime y Ultimate](/help/assets/dynamic-media/dm-prime-ultimate.md) para conocer sus ventajas y las principales diferencias entre ellos.

Este artículo proporciona un flujo de trabajo completo para habilitar las ofertas de Prime y Ultimate de [!DNL Dynamic Media].

## Habilitar [!DNL Dynamic Media] Ultimate {#enable-dynamic-media-ultimate}

Para habilitar [!DNL Dynamic Media] Ultimate:

1. [Activar [!DNL Dynamic Media with OpenAPI]](#activate-dynamic-media-with-openapi)
1. [Configurar [!DNL Dynamic Media] soluciones](#configure-dynamic-media-solutions)
1. [Crear y enumerar  [!DNL Dynamic Media] empresas](#create-and-list-dynamic-media-companies)
1. [Configurar dominio personalizado en el nivel de entrega](#configure-custom-domain-in-delivery-tier)

<!--
1. [Onboard API keys using the [!DNL AEM] [!DNL Dynamic Media] API card](#onboarding-api-keys)
-->

Si necesita habilitar [!DNL Dynamic Media Prime], vea los vínculos rápidos proporcionados en [Habilitar [!DNL Dynamic Media Prime]](#enable-dynamic-media-prime).

### Activar [!DNL Dynamic Media with OpenAPI] {#activate-dynamic-media-with-openapi}

[!DNL Dynamic Media] con capacidades OpenAPI coloca a DAM en el centro de un ecosistema de cadena de suministro de contenido ágil y eficiente para garantizar la administración y el envío de recursos.

El primer paso en el proceso de habilitar [!DNL Dynamic Media] Ultimate es activar [[!DNL Dynamic Media] con OpenAPI](/help/assets/dynamic-media-open-apis-overview.md) para tu entorno de Cloud Service.

#### Prepárese para empezar {#prerequisites}

Asegúrese de cumplir los siguientes requisitos antes de iniciar el proceso de activación:

1. [Acceso a Cloud Manager](https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/onboarding/journey/cloud-manager).
1. [Su programa incluye [!DNL Dynamic Media] soluciones](#configure-dynamic-media-solutions).
1. Tiene [!DNL Dynamic Media] licencia de Prime o Ultimate.

#### Habilitar las capacidades de [!DNL Dynamic Media with OpenAPI] en su entorno de Cloud Service {#enable-dynamic-media-with-openapi-capabilites-in-your-CS-environment}

Ejecute estos pasos para habilitar [!DNL Dynamic Media with OpenAPI] para su entorno de servicio en la nube:

1. [Vaya a la interfaz de usuario de Cloud Manager](https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/onboarding/journey/cloud-manager).

1. [Crear un entorno](https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/onboarding/journey/create-environments), si no tiene acceso a uno existente.

1. Seleccione **[!UICONTROL Haga clic para activar]** en la fila **[!UICONTROL Dynamic Media]** de la sección **[!UICONTROL Información del entorno]** de la página Detalles del entorno.

   ![activar medios dinámicos con capacidades OpenAPI](/help/assets/assets/activate-adv-capabiliites-of-dm-openAPI.png)

1. Haga clic en **[!UICONTROL Activar]** en el cuadro de diálogo de confirmación para iniciar el proceso de activación de [!DNL Dynamic Media with OpenAPI]. Después de la activación correcta, Cloud Manager muestra las siguientes actualizaciones de estado:
   1. **[!UICONTROL Fase de entorno]**: **[!UICONTROL En ejecución]**
   1. ![Medios dinámicos activados por DM](/help/assets/assets/Images_icon.svg)**[!UICONTROL Dynamic Media &#x200B;]**:**[!UICONTROL &#x200B; Las capacidades de OpenAPI están activadas &#x200B;]**

      ![activación correcta](/help/assets/assets/activation-successful.png){width="700" align="left"}

#### Reintentar activación {#retry-activation}

Si la activación falla, Cloud Manager muestra las siguientes actualizaciones de estado:

* **[!UICONTROL Fase de entorno]**: **[!UICONTROL error de DM con OpenAPI]**
* ![DM activado](/help/assets/assets/Images_icon.svg)**[!UICONTROL Dynamic Media &#x200B;]**:**[!UICONTROL &#x200B; No se pudieron activar las capacidades de OpenAPI &#x200B;]**

  ![reintentar activación](/help/assets/assets/retry-dm-openapi-failed-activation.png){width="700" align="left"}

Seleccione **[!UICONTROL Haga clic para reintentar]** y reiniciar la activación.

Como alternativa, ejecute estos pasos para reiniciar el proceso de activación:

1. Navegue hasta la página que enumera todos los entornos.

1. Haga clic en más opciones (![más opciones](/help/assets/assets/three-dots.svg)) al final de la fila de entorno.

1. Seleccione **[!UICONTROL Reintentar DM con OpenAPI Activation]** para reiniciar la activación.

   ![reintentar la activación desde la página de detalles del entorno](/help/assets/assets/restart-activation-process-from-list-environment-page.png)

### Configurar [!DNL Dynamic Media] soluciones {#configure-dynamic-media-solutions}

Configure las soluciones de [!UICONTROL Dynamic Media] para que usen las capacidades básicas y avanzadas de [Dynamic Media con OpenAPI](/help/assets/dynamic-media-open-apis-overview.md) en los entornos nuevos o existentes disponibles en Cloud Manager.

#### Prepárese para empezar {#prerequisites-to-configure-dynamic-media-solutions}

Asegúrese de que dispone de lo siguiente para configurar las soluciones de [!UICONTROL Dynamic Media]:

1. [Acceso a Cloud Manager](https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/onboarding/journey/cloud-manager).
1. Tiene [!DNL Dynamic Media] licencia de Ultimate.

#### Configurar [!DNL Dynamic Media] soluciones para la entrega de recursos {#configure-dynamic-media-solutions-for-asset-delivery}

Ejecute los siguientes pasos:

1. [Cree un nuevo programa](https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/onboarding/journey/create-program) o navegue a un programa existente y haga clic en **[!UICONTROL Editar]**. La página **[!UICONTROL Configurar para producción]** muestra la pestaña **[!UICONTROL Soluciones y complementos]**.

1. Seleccione **[!UICONTROL Assets]**, **[!UICONTROL Assets Prime]**, **[!UICONTROL Assets Ultimate]** o **[!UICONTROL Sites]** para agregar la solución **[!UICONTROL Dynamic Media]** a su programa.

1. Seleccione la solución **[!UICONTROL Dynamic Media]** y haga clic en **[!UICONTROL Continuar]** para agregar la solución **[!UICONTROL Dynamic Media]** a su programa. Esta acción reinicia todos los entornos existentes en el programa y les agrega la solución [!DNL Dynamic Media]. Además, cualquier entorno nuevo que cree en su programa obtendrá automáticamente [!DNL Dynamic Media].

   ![configurado para producción](/help/assets/assets/set-up-for-prod.png){width="500" align="left"}

Vea [Activar [!DNL Dynamic Media with OpenAPI]](#activate-dynamic-media-with-openapi) para empezar a usar las capacidades de [!DNL Dynamic Media] con las capacidades de OpenAPI en su entorno.

### Crear y listar [!DNL Dynamic Media] empresas {#create-and-list-dynamic-media-companies}

Cree y enumere [!DNL Dynamic Media] empresas en su entorno de servicio de nube AEM para administrar las configuraciones en su entorno de AEM.

#### Prepárese para empezar {#prerequisites-to-create-and-list-dynamic-media-companies}

Para ver las empresas (cuentas) existentes o agregar una nueva empresa (cuenta) [!DNL Dynamic Media] en su organización de IMS, debe tener:

1. [Acceso a Cloud Manager](https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/onboarding/journey/cloud-manager).

1. Tiene [!DNL Dynamic Media] licencia de Ultimate.

#### Crear y listar [!DNL Dynamic Media] empresas en su organización IMS {#create-and-list-dynamic-media-companies-in-your-ims-organisation}

Ejecute estos pasos para crear y listar una nueva compañía (cuenta) de [!DNL Dynamic Media] que se pueda configurar dentro de su entorno de [!DNL AEM]:

1. Vaya a la [página de licencia de Cloud Manager](https://experience-stage.adobe.com/#/@ssahnichstage/cloud-manager/license).

1. Haga clic en **[!UICONTROL Agregar compañía]**, se mostrará el cuadro de diálogo **[!UICONTROL Crear compañía de Dynamic Media]**.

1. Especifique un nombre de empresa [!DNL Dynamic Media] único, seleccione una región de empresa y agregue una lista de ID de correo electrónico de administrador de empresa separados por comas.

   ![Crear empresa de Dynamic Media](/help/assets/assets/create-dynamic-media-company.png){width="500" align="left"}

1. Haga clic en **[!UICONTROL Crear]** para comenzar a crear su compañía. Esta acción agrega una nueva fila a la sección **[!UICONTROL [!DNL Dynamic Media]compañías]** y muestra **[!UICONTROL Configurando]** como el **[!UICONTROL ESTADO]** de la compañía.

   ![inició la creación de la empresa de Dynamic Media](/help/assets/assets/dm-company-creation-initiated.png)

1. **Opcional:** Haga clic en ![icono de información](/help/assets/assets/info-icon-solid-black.svg) para ver los detalles de la compañía. El **[!UICONTROL ESTADO]** se actualiza a **[!UICONTROL Listo]** cuando se crea la compañía.

   ![Información de la empresa de Dynamic Media](/help/assets/assets/dm-company-information.png)

1. Como administrador de Dynamic Media, compruebe si en su buzón hay un correo electrónico de bienvenida que incluya una lista de pasos para [configurar [!DNL Dynamic Media]](/help/assets/dynamic-media/config-dm.md#architecture-diagram-of-dynamic-media) la empresa en su entorno de Cloud Service [!DNL AEM] para comenzar.

   ![correo electrónico de bienvenida](/help/assets/assets/welcome-email.png)

#### Reintentar creación de empresa {#retry-company-creation}

Si falla la creación de la empresa [!DNL Dynamic Media], ejecute los siguientes pasos según el estado del error:

1. Si **[!UICONTROL Estado]** está pendiente, comunica el problema al equipo de atención al cliente para que lo resuelva.


   ![estado pendiente](/help/assets/assets/company-creation-pending-status.png){width="350" align="center"}



1. Si **[!UICONTROL Status]** da error, vuelve a intentarlo según el motivo del error.

   ![estado fallido](/help/assets/assets/company-creation-failure-status.png){width="380" align="center"}

### Opcional: Configurar el dominio personalizado en el nivel de envío {#configure-custom-domain-in-delivery-tier}

Aunque AEM as a Cloud Service viene con un dominio predeterminado, puede personalizarlo según sus necesidades. Adjunte un dominio personalizado al nivel de envío mediante Cloud Manager.

#### Prepárese para empezar {#prerequisites-to-configure-custom-domain-in-delivery-tier}

Asegúrese de cumplir los siguientes requisitos antes de iniciar el proceso de configuración:

1. [Acceso a Cloud Manager](https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/onboarding/journey/cloud-manager).
1. [Ya se ha activado [!DNL Dynamic Media with OpenAPI] en su entorno](#activate-dynamic-media-with-openapi).
1. Se habilitó [!DNL Dynamic Media with OpenAPI] en estado listo.
1. Certificado de tipo EV u OV para el dominio que se va a utilizar para el nivel de entrega. Consulte [Introducción a los certificados SSL](https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/manage-ssl-certificates/introduction-to-ssl-certificates) para obtener más información.

#### Configuración de dominios personalizados en el nivel de envío mediante Cloud Manager {#configure-custom-domain-in-delivery-tier-using-cloud-manager}

Ejecute los siguientes pasos en Cloud Manager para configurar un dominio personalizado en el nivel de entrega:

1. [Agregar un certificado SSL administrado por el cliente](https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/manage-ssl-certificates/add-ssl-certificate#add-customer-managed-ssl-cert).

1. [Agregar un nombre de dominio personalizado](https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/custom-domain-names/add-custom-domain-name#adding-cdn-settings).

1. Vaya a la página de detalles del entorno y [agregue una configuración de CDN](https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/domain-mappings/add-domain-mapping). Al agregar la configuración, seleccione **[!UICONTROL Delivery]** en el campo **[!UICONTROL Tier]** del cuadro de diálogo **[!UICONTROL Configurar CDN]**.

   ![Configurar CDN](/help/assets/assets/select-delivery-tier-in-configure-cdn-form.png)

   Después de agregar las configuraciones, el **[!UICONTROL ESTADO]** de **[!UICONTROL Configuraciones de CDN]** se actualiza a **[!UICONTROL Aplicado]**.

   ![Configurar el estado de implementación de CDN](/help/assets/assets/cdn-configuration-deployment-status.png)

1. Haga clic en más opciones (![más opciones](/help/assets/assets/three-dots.svg)) y seleccione **[!UICONTROL Preparación para el lanzamiento]** para mostrar el cuadro de diálogo **[!UICONTROL Preparación para el lanzamiento]**.

   ![opción de preparación para el lanzamiento](/help/assets/assets/go-live-readiness-option.png)

1. Ejecute los pasos de **[!UICONTROL Configurar CNAME]** para asignar `cdn.adobeaemcloud.com` (registro CNAME) en el registro DNS del proveedor de servicios DNS. Esta asignación garantiza que las solicitudes recibidas en el dominio personalizado se redirijan a la CDN de Adobe.

   ![cuadro de diálogo de preparación para lanzamiento](/help/assets/assets/go-live-readiness-dialogbox.png){width="500" align="left"}

1. Haz clic en **[!UICONTROL Aceptar]**, el **[!UICONTROL ESTADO]** se actualiza a **[!UICONTROL Verificado]**. El dominio personalizado está listo para usarse en la dirección URL de envío.


   ![Configurar CDN](/help/assets/assets/cdn-configurations-varified.png)



<!--
### Onboard API keys {#onboarding-api-keys}

Create an API key to access [!DNL Dynamic Media] with OpenAPIs and the delivery tier backed Asset Selector.

#### Prepare yourself for API keys onboarding process {#prerequisites-for-onboarding-api-keys} 

To start the API keys onboarding process, ensure you have:

1. [Access to Cloud Manager](https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/onboarding/journey/cloud-manager).
1. [Activated [!DNL Dynamic Media with OpenAPI] in your environment](#activate-dynamic-media-with-openapi).
1. [Access to the Adobe Developer Console](https://experienceleague.adobe.com/es/docs/experience-manager-learn/cloud-service/aem-apis/invoke-openapi-based-aem-apis#create-adobe-developer-console-adc-project).

#### Onboard the API keys using [!DNL AEM Dynamic Media] API card {#onboarding-api-keys-using-aem-dynamic-media-api-card}

Use the [Adobe Developer Console](https://developer.adobe.com/developer-console/) to onboard the API keys to:

1. [Access Dynamic Media APIs](#access-dynamic-media-apis)
1. [Access Delivery tier backed Asset Selector](#access-delivery-tier-backed-asset-selector)

#### Create an API key to access [!DNL Dynamic Media] with OpenAPIs {#access-dynamic-media-apis}

Execute the following steps to create an API key to access [!DNL Dynamic Media] with OpenAPIs:

1. Navigate to the **[!UICONTROL Admin Console]**. The Admin Console displays the **[!UICONTROL author]**, **[!UICONTROL delivery]** and **[!UICONTROL publish]** instances.
![instances on admin console](/help/assets/assets/delivery-instance-admin-console.png)
1. Select the **[!UICONTROL delivery]** instance to display the product profile with **[!UICONTROL AEM Dynamic Media enable API Services]** enabled by default. The product profile looks like this: **[!UICONTROL AEM Assets DM OpenAPI Users - delivery  - Program [ID Number] - Environment [ID Number]]**. 

   ![product profile on admin console](/help/assets/assets/admin-console-product-profile.png)

   >[!NOTE]
   >
   >This delivery instance is common for [!DNL Content Hub] and [!DNL Dynamic Media] with OpenAPI capabilities.

1. Navigate to the [Adobe Developer console](https://developer.adobe.com/console) and [create a new project](https://developer.adobe.com/dep/guides/dev-console/create-project/). See [Invoke OpenAPI-based AEM APIs for server to server authentication](https://experienceleague.adobe.com/es/docs/experience-manager-learn/cloud-service/aem-apis/invoke-openapi-based-aem-apis) to learn about creating a new project.
1. Select **[!UICONTROL AEM Dynamic Media API]** to access to the [!DNL Dynamic Media with OpenAPI capabilities] and click **[!UICONTROL Next]**.
![adobe developer console](/help/assets/assets/adobe-developer-console.png)
1. Select **[!UICONTROL Server-to-Server Authentication]** and click **[!UICONTROL Next]**. See [Server to Server authentication](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/) to learn more about this authentication type.
![server-to-server-authentication](/help/assets/assets/server-to-server-authentication.png)
1. Select **[!UICONTROL OAuth Server-to-Server]**, specify a unique **[!UICONTROL Credential name]** and click **[!UICONTROL Next]**.
![oauth server to server credential](/help/assets/assets/oauth-server-server-and-credential-name.png)
1. Select your product profile (mentioned in step 2) to access the APIs using the environment's delivery endpoint and click **[!UICONTROL Save configured API]**.
![select product profile](/help/assets/assets/select-product-profile.png)
1. Select **[!UICONTROL AEM Dynamic Media API]**. Use the **[!UICONTROL OAuth Server-to-Server]** to fetch the **X-API-key** and access the token for the **authorization** header. 
![oauth server to server](/help/assets/assets/oauth-server-to-server-credentials.png)
Execute the below steps to use [Dynamic Media with OpenAPIs](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/assets/delivery/) using the **[!UICONTROL OAuth Server-to-Server]** credentials. 
    1. Copy the **[!UICONTROL API KEY (Client ID)]** and replace the `X-Api-Key` in the cURL.
    1. Click **[!UICONTROL Generate access token]** to generate an access token and replace `YOUR_JWT_HERE` with the token in the cURL.

The cURL looks like this:
```
headers: {
    'Content-Type': 'application/json',
      'X-Adobe-Accept-Experimental': '1',
      Authorization: 'Bearer <YOUR_JWT_HERE>',
      'X-Api-Key': 'YOUR_API_KEY_HERE'
    `},
```
See [Search Assets API](https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/assets/dynamicmedia/dynamic-media-open-apis/search-assets-api#search-assets-api-header) for more information.

### Access Delivery tier backed Asset Selector {#access-delivery-tier-backed-asset-selector}

TBD: Wiki in progress..
-->

## Habilitar [!DNL Dynamic Media] Prime {#enable-dynamic-media-prime}

Para habilitar [!DNL Dynamic Media] Prime:

1. [Activar Dynamic Media con OpenAPI](#activate-dynamic-media-with-openapi)
1. [Opcional: configurar dominio personalizado en el nivel de entrega](#configure-custom-domain-in-delivery-tier)

<!--
1. [Onboard API keys using the AEM Dynamic Media API card](#onboarding-api-keys)
-->
