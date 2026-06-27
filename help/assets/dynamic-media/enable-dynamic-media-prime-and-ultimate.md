---
title: Habilitar [!DNL Dynamic Media] Prime y Ultimate
description: Obtenga información sobre cómo habilitar  [!DNL Dynamic Media] ofertas de Prime y Ultimate.
feature: Asset Management
role: User, Admin
badgeSaas: label="AEM Assets" type="Positive" tooltip="(Se aplica a los AEM Assets)."
exl-id: 0ee161f5-bf44-41f1-928e-c07574fd43cc
source-git-commit: 6861ae63c85ca2e10638a7f2128783eae02cc2b6
workflow-type: tm+mt
source-wordcount: '2380'
ht-degree: 4%

---

# Habilitar [!DNL Dynamic Media] Prime y Ultimate {#enable-dynamic-media-prime-and-ultimate}

[!DNL Adobe Experience Manager] as a Cloud Service le permite acceder a las ofertas de [!DNL Dynamic Media] Prime y Ultimate para optimizar sus flujos de trabajo digitales y la administración de contenido. Consulte [Dynamic Media Prime y Ultimate](/help/assets/dynamic-media/dm-prime-ultimate.md) para conocer sus ventajas y las principales diferencias entre ellos.

Este artículo proporciona un flujo de trabajo completo para habilitar las ofertas de Prime y Ultimate de [!DNL Dynamic Media].

## Habilitar [!DNL Dynamic Media] Ultimate {#enable-dynamic-media-ultimate}

Para habilitar [!DNL Dynamic Media] Ultimate:

1. [Activar [!DNL Dynamic Media with OpenAPI]](#activate-dynamic-media-with-openapi)
1. [Configurar  [!DNL Dynamic Media] soluciones](#configure-dynamic-media-solutions)
1. [Acceder a las API de Dynamic Media](#access-dynamic-media-apis)
1. [Crear y enumerar  [!DNL Dynamic Media] empresas](#create-and-list-dynamic-media-companies)
1. [Configurar dominio personalizado en el nivel de entrega](#configure-custom-domain-in-delivery-tier)

<!--
1. [Onboard API keys using the [!DNL AEM] [!DNL Dynamic Media] API card](#onboarding-api-keys)
-->

Si necesita habilitar [!DNL Dynamic Media Prime], vea los vínculos rápidos proporcionados en [Habilitar [!DNL Dynamic Media Prime]](#enable-dynamic-media-prime).

### Activar [!DNL Dynamic Media with OpenAPI] {#activate-dynamic-media-with-openapi}

[!DNL Dynamic Media] con capacidades de OpenAPI coloca a DAM en el centro de un ecosistema de supply chain de contenido ágil y eficiente para garantizar el gobierno y la entrega de los recursos.

El primer paso en el proceso de habilitar [!DNL Dynamic Media] Ultimate es activar [[!DNL Dynamic Media] con OpenAPI](/help/assets/dynamic-media-open-apis-overview.md) para tu entorno de Cloud Service.

#### Prepárese para empezar {#prerequisites}

Asegúrese de cumplir los siguientes requisitos antes de iniciar el proceso de activación:

1. [Acceso a Cloud Manager](https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/onboarding/journey/cloud-manager).
1. [Su programa incluye [!DNL Dynamic Media] soluciones](#configure-dynamic-media-solutions).
1. Tiene [!DNL Dynamic Media] licencia de Prime o Ultimate.

#### Habilitar las capacidades de [!DNL Dynamic Media with OpenAPI] en su entorno de Cloud Service {#enable-dynamic-media-with-openapi-capabilites-in-your-CS-environment}

Ejecute estos pasos para habilitar [!DNL Dynamic Media with OpenAPI] para su entorno de servicio en la nube:

1. [Vaya a la interfaz de usuario de Cloud Manager](https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/onboarding/journey/cloud-manager).

1. [Crear un entorno](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/onboarding/journey/create-environments), si no tiene acceso a uno existente.

1. Seleccione **[!UICONTROL Haga clic para activar]** en la fila **[!UICONTROL Dynamic Media]** de la sección **[!UICONTROL Información del entorno]** de la página Detalles del entorno.

   ![activar medios dinámicos con capacidades OpenAPI](/help/assets/assets/activate-adv-capabiliites-of-dm-openAPI.png)

1. Haga clic en **[!UICONTROL Activar]** en el cuadro de diálogo de confirmación para iniciar el proceso de activación de [!DNL Dynamic Media with OpenAPI]. Después de la activación correcta, Cloud Manager muestra las siguientes actualizaciones de estado:
   1. **[!UICONTROL Fase de entorno]**: **[!UICONTROL En ejecución]**
   1. ![Medios dinámicos activados por DM](/help/assets/assets/Images_icon.svg)**[!UICONTROL Dynamic Media ]**:**[!UICONTROL  Las capacidades de OpenAPI están activadas ]**

      ![activación correcta](/help/assets/assets/activation-successful.png){width="700"}

#### Reintentar activación {#retry-activation}

Si la activación falla, Cloud Manager muestra las siguientes actualizaciones de estado:

* **[!UICONTROL Fase de entorno]**: **[!UICONTROL error de DM con OpenAPI]**
* ![DM activado](/help/assets/assets/Images_icon.svg)**[!UICONTROL Dynamic Media ]**:**[!UICONTROL  No se pudieron activar las capacidades de OpenAPI ]**

  ![reintentar activación](/help/assets/assets/retry-dm-openapi-failed-activation.png){width="700"}

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

1. [Cree un nuevo programa](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/onboarding/journey/create-program) o navegue a un programa existente y haga clic en **[!UICONTROL Editar]**. La página **[!UICONTROL Configurar para producción]** muestra la pestaña **[!UICONTROL Soluciones y complementos]**.

1. Seleccione **[!UICONTROL Assets]**, **[!UICONTROL Assets Prime]**, **[!UICONTROL Assets Ultimate]** o **[!UICONTROL Sites]** para agregar la solución **[!UICONTROL Dynamic Media]** a su programa.

1. Seleccione la solución **[!UICONTROL Dynamic Media]** y haga clic en **[!UICONTROL Continuar]** para agregar la solución **[!UICONTROL Dynamic Media]** a su programa. Esta acción reinicia todos los entornos existentes en el programa y les agrega la solución [!DNL Dynamic Media]. Además, cualquier entorno nuevo que cree en su programa obtendrá automáticamente [!DNL Dynamic Media].

   ![configurado para producción](/help/assets/assets/set-up-for-prod.png)

Vea [Activar [!DNL Dynamic Media with OpenAPI]](#activate-dynamic-media-with-openapi) para empezar a usar las capacidades de [!DNL Dynamic Media] con las capacidades de OpenAPI en su entorno.

### Acceso a las API de Dynamic Media {#access-dynamic-media-apis}

Después de [habilitar Dynamic Media con OpenAPI](#activate-dynamic-media-with-openapi), se crea una instancia de `delivery`. Haga clic en la instancia de envío para ver el perfil de producto `AEM Assets DM OpenAPI Users - delivery  - Program xxxx - Environment yyyy`. El perfil de producto ya tiene **AEM Dynamic Media habilitado para los servicios de API** habilitados de manera predeterminada.

![Servicios de API de Dynamic Media](/help/assets/assets/dynamic-media-api-services.png)

Cree un nuevo proyecto en [Adobe Developer Console](https://developer.adobe.com/console) y use la tarjeta de API de Dynamic Media de AEM para obtener acceso a Dynamic Media con las funcionalidades de OpenAPI.

![API de Dynamic Media](/help/assets/assets/dynamic-media-apis.png)

Puede usar la autenticación de [servidor a servidor](https://experienceleague.adobe.com/es/docs/experience-manager-learn/cloud-service/aem-apis/openapis/invoke-api-using-oauth-s2s) o la autenticación de usuario mediante [credenciales de aplicación web](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/aem-apis/openapis/invoke-api-using-oauth-web-app) o [credenciales de SPA](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/aem-apis/openapis/invoke-api-using-oauth-single-page-app).

Antes de acceder a la API, se le debe agregar al perfil de producto `AEM Assets DM OpenAPI Users - delivery  - Program xxxx - Environment yyyy`.

Una vez que se obtenga el token de acceso mediante cualquiera de los métodos de autenticación, puede [definir el ID de cliente como la clave de API en la solicitud cURL](/help/assets/search-assets-api.md) y comenzar a usar [Dynamic Media con OpenAPI](https://developer.adobe.com/experience-cloud/experience-manager-apis/).

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

   ![Crear empresa de Dynamic Media](/help/assets/assets/create-dynamic-media-company.png){width="500"}

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
1. Certificado de tipo EV u OV para el dominio que se va a utilizar para el nivel de entrega. Consulte [Introducción a los certificados SSL](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/manage-ssl-certificates/introduction-to-ssl-certificates) para obtener más información.

#### Configuración de dominios personalizados en el nivel de envío mediante Cloud Manager {#configure-custom-domain-in-delivery-tier-using-cloud-manager}

Ejecute los siguientes pasos en Cloud Manager para configurar un dominio personalizado en el nivel de entrega:

1. [Agregar un certificado SSL administrado por el cliente](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/manage-ssl-certificates/add-ssl-certificate#add-customer-managed-ssl-cert).

1. [Agregar un nombre de dominio personalizado](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/custom-domain-names/add-custom-domain-name#adding-cdn-settings).

1. Vaya a la página de detalles del entorno y [agregue una configuración de CDN](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/domain-mappings/add-domain-mapping). Al agregar la configuración, seleccione **[!UICONTROL Delivery]** en el campo **[!UICONTROL Tier]** del cuadro de diálogo **[!UICONTROL Configurar CDN]**.

   ![Configurar CDN](/help/assets/assets/select-delivery-tier-in-configure-cdn-form.png)

   Después de agregar las configuraciones, el **[!UICONTROL ESTADO]** de **[!UICONTROL Configuraciones de CDN]** se actualiza a **[!UICONTROL Aplicado]**.

   ![Configurar el estado de implementación de CDN](/help/assets/assets/cdn-configuration-deployment-status.png)

1. Haga clic en más opciones (![más opciones](/help/assets/assets/three-dots.svg)) y seleccione **[!UICONTROL Preparación para el lanzamiento]** para mostrar el cuadro de diálogo **[!UICONTROL Preparación para el lanzamiento]**.

   ![opción de preparación para el lanzamiento](/help/assets/assets/go-live-readiness-option.png)

1. Ejecute los pasos de **[!UICONTROL Configurar CNAME]** para asignar `cdn.adobeaemcloud.com` (registro CNAME) en el registro DNS del proveedor de servicios DNS. Esta asignación garantiza que las solicitudes recibidas en el dominio personalizado se redirijan a la CDN de Adobe.

   ![cuadro de diálogo de preparación para lanzamiento](/help/assets/assets/go-live-readiness-dialogbox.png){width="500"}

1. Haz clic en **[!UICONTROL Aceptar]**, el **[!UICONTROL ESTADO]** se actualiza a **[!UICONTROL Verificado]**. El dominio personalizado está listo para usarse en la dirección URL de envío.


   ![Configurar CDN](/help/assets/assets/cdn-configurations-varified.png)



<!--
### Onboard API keys {#onboarding-api-keys}

Create an API key to access [!DNL Dynamic Media] with OpenAPIs and the delivery tier backed Asset Selector.

#### Prepare yourself for API keys onboarding process {#prerequisites-for-onboarding-api-keys} 

To start the API keys onboarding process, ensure you have:

1. [Access to Cloud Manager](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/onboarding/journey/cloud-manager).
1. [Activated [!DNL Dynamic Media with OpenAPI] in your environment](#activate-dynamic-media-with-openapi).
1. [Access to the Adobe Developer Console](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/aem-apis/invoke-openapi-based-aem-apis#create-adobe-developer-console-adc-project).

#### Onboard the API keys using [!DNL AEM Dynamic Media] API card {#onboarding-api-keys-using-aem-dynamic-media-api-card}

Use the [Adobe Developer Console](https://developer.adobe.com/developer-console/) to onboard the API keys to:

1. [Access Dynamic Media APIs](#access-dynamic-media-apis)
1. [Access Delivery tier backed Asset Selector](#access-delivery-tier-backed-asset-selector)

#### Create an API key to access [!DNL Dynamic Media] with OpenAPIs

Execute the following steps to create an API key to access [!DNL Dynamic Media] with OpenAPIs:

1. Navigate to the **[!UICONTROL Admin Console]**. The Admin Console displays the **[!UICONTROL author]**, **[!UICONTROL delivery]** and **[!UICONTROL publish]** instances.
![instances on admin console](/help/assets/assets/delivery-instance-admin-console.png)
1. Select the **[!UICONTROL delivery]** instance to display the product profile with **[!UICONTROL AEM Dynamic Media enable API Services]** enabled by default. The product profile looks like this: **[!UICONTROL AEM Assets DM OpenAPI Users - delivery  - Program [ID Number] - Environment [ID Number]]**. 

   ![product profile on admin console](/help/assets/assets/admin-console-product-profile.png)

   >[!NOTE]
   >
   >This delivery instance is common for [!DNL Content Hub] and [!DNL Dynamic Media] with OpenAPI capabilities.

1. Navigate to the [Adobe Developer console](https://developer.adobe.com/console) and [create a new project](https://developer.adobe.com/dep/guides/dev-console/create-project/). See [Invoke OpenAPI-based AEM APIs for server to server authentication](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/aem-apis/invoke-openapi-based-aem-apis) to learn about creating a new project.
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
See [Search Assets API](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/dynamicmedia/dynamic-media-open-apis/search-assets-api#search-assets-api-header) for more information.

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

## Preguntas frecuentes {#frequently-asked-questions-dynamic-media-prime-ultimate}

### ¿Cuáles son los requisitos previos para activar Dynamic Media con OpenAPI? {#dynamic-media-openapi-prerequisites}

La activación de Dynamic Media con OpenAPI requiere tres requisitos previos: acceso a Cloud Manager, un programa que incluye soluciones de Dynamic Media y una licencia válida de Dynamic Media Prime o Ultimate. Si no hay ningún entorno existente disponible en Cloud Manager, se debe crear un nuevo entorno antes de que pueda comenzar la activación. La solución Dynamic Media debe agregarse al programa antes de ejecutar el paso de activación en la página de detalles del entorno.

### ¿Cómo activo Dynamic Media con OpenAPI en mi entorno de Cloud Service? {#activate-dynamic-media-openapi}

Para activar Dynamic Media con OpenAPI, vaya a la interfaz de usuario de Cloud Manager y abra la página de detalles del entorno. En la sección Información del entorno, busque la fila Dynamic Media y haga clic en Haga clic para activar. Haga clic en Activar en el cuadro de diálogo de confirmación para iniciar el proceso de activación. Después de la activación correcta, Cloud Manager muestra el escenario del entorno como En ejecución y el estado de Dynamic Media como Funcionalidades de OpenAPI activadas.

### ¿Qué debo hacer si falla la activación de Dynamic Media con OpenAPI? {#dynamic-media-openapi-activation-failure}

Si falla la activación de Dynamic Media con OpenAPI, Cloud Manager muestra el escenario del entorno como DM con un error de OpenAPI y el estado de Dynamic Media como capacidades de OpenAPI no se pudo activar. Para volver a intentarlo, haga clic en para volver a intentarlo en la página de detalles del entorno. También puede navegar a la página que enumera todos los entornos, hacer clic en el icono de más opciones al final de la fila del entorno y seleccionar Reintentar DM con activación de OpenAPI para reiniciar el proceso.

### ¿Cuáles son los requisitos previos para configurar las soluciones de Dynamic Media? {#configure-dynamic-media-solutions-prerequisites}

La configuración de soluciones de Dynamic Media requiere acceso a Cloud Manager y una licencia válida de Dynamic Media Ultimate. Dynamic Media Prime no requiere este paso: solo es aplicable a los clientes de Dynamic Media Ultimate que necesitan agregar la solución Dynamic Media a un programa existente o nuevo en Cloud Manager.

### ¿Cómo añado la solución Dynamic Media a un programa de AEM Cloud Service? {#add-dynamic-media-solution-program}

Para agregar la solución Dynamic Media a un programa, cree un nuevo programa o vaya a un programa existente en Cloud Manager y haga clic en Editar. En la página Configurar para producción, seleccione la pestaña Soluciones y complementos y, a continuación, seleccione Assets, Assets Prime, Assets Ultimate o Sites para que la solución Dynamic Media esté disponible. Seleccione Dynamic Media y haga clic en Continuar para añadirlo al programa. Esta acción reinicia todos los entornos existentes en el programa y agrega la solución Dynamic Media. Todos los entornos nuevos creados con el programa reciben Dynamic Media automáticamente.

### ¿Cómo puedo acceder a las API de Dynamic Media después de habilitar Dynamic Media con OpenAPI? {#dynamic-media-apis-faqs}

Después de habilitar Dynamic Media con OpenAPI, se crea una instancia de envío en Adobe Admin Console. Haga clic en la instancia de envío para ver el perfil de producto Usuarios de DM OpenAPI de AEM Assets, que tiene habilitados los servicios de API de activación de Dynamic Media de AEM de forma predeterminada. Para acceder a las API, cree un nuevo proyecto en Adobe Developer Console y utilice la tarjeta de API de Dynamic Media de AEM. Las opciones de autenticación incluyen autenticación de servidor a servidor, credenciales de aplicación web o credenciales de SPA. Antes de acceder a la API, el usuario debe añadirse al perfil de producto de entrega de los usuarios de DM OpenAPI de los AEM Assets para el programa y el entorno relevantes.

### ¿Cuáles son los requisitos previos para crear una empresa de Dynamic Media? {#create-dynamic-media-company-prerequisites}

La creación de una empresa de Dynamic Media requiere acceso a Cloud Manager y una licencia válida de Dynamic Media Ultimate. La empresa se crea a partir de la página de licencia de Cloud Manager y representa una cuenta que se puede configurar dentro del entorno de AEM Cloud Service. La creación de empresas de Dynamic Media es un paso específico de Dynamic Media Ultimate y no es necesario para Dynamic Media Prime.

### ¿Cómo creo una nueva compañía de Dynamic Media en mi organización IMS? {#create-dynamic-media-company}

Para crear una nueva empresa de Dynamic Media, vaya a la página de licencia de Cloud Manager y haga clic en Agregar empresa. En el cuadro de diálogo Crear empresa de Dynamic Media, especifique un nombre de empresa único, seleccione una región de empresa y agregue ID de correo electrónico de administrador de empresa separados por comas. Haga clic en Crear para iniciar la creación de la empresa: se agrega una nueva fila a la sección de empresas de Dynamic Media con el estado Configuración. Cuando se completa la creación, el estado se actualiza a Listo. El administrador de Dynamic Media recibe un correo electrónico de bienvenida con los pasos para configurar la empresa de Dynamic Media en el entorno de AEM Cloud Service.

### ¿Qué debo hacer si falla la creación de la empresa de Dynamic Media? {#dynamic-media-company-creation-failure}

Si la creación de la empresa de Dynamic Media falla, la acción que se debe realizar depende del estado mostrado. Si el estado es Pendiente, plantee el problema con el equipo de asistencia al cliente de Adobe para que lo resuelva. Si el estado es Failed, vuelva a intentar la creación en función del motivo del error mostrado. El error de creación de la empresa es independiente del error de activación: ambos tienen sus propios mecanismos de reintento en Cloud Manager.

### ¿Cuáles son los requisitos previos para configurar un dominio personalizado en el nivel de entrega de Dynamic Media? {#custom-domain-delivery-tier-prerequisites}

La configuración de un dominio personalizado en el nivel de entrega de Dynamic Media requiere cuatro requisitos previos: acceso a Cloud Manager, Dynamic Media con OpenAPI ya activado y en estado listo en el entorno y un certificado SSL de tipo EV u OV para el dominio que se va a utilizar en el nivel de entrega. La configuración de dominio personalizada es opcional tanto para Dynamic Media Prime como para Dynamic Media Ultimate.

### ¿Cómo configuro un dominio personalizado para la entrega de Dynamic Media con Cloud Manager? {#configure-custom-domain-delivery-tier}

Para configurar un dominio personalizado para la entrega de Dynamic Media, complete tres pasos en Cloud Manager: añadir un certificado SSL administrado por el cliente, añadir un nombre de dominio personalizado y añadir una configuración de CDN desde la página de detalles del entorno: seleccione Entrega en el campo Nivel del cuadro de diálogo Configurar CDN. Después de añadir la configuración de CDN, el estado se actualiza a Aplicado. Haga clic en más opciones y seleccione Preparación para el lanzamiento y, a continuación, siga los pasos de Configuración de CNAME para asignar cdn.adobeaemcloud.com como un registro CNAME en el proveedor de servicios DNS. Una vez confirmada la asignación DNS, haga clic en Aceptar y el estado del dominio se actualizará a Verificado, con lo que el dominio personalizado estará listo para su uso en las direcciones URL de envío.
