---
title: Configurar AEM Assets con Brand Portal
description: Configurar AEM Assets con Brand Portal.
contentOwner: Vishabh Gupta
translation-type: tm+mt
source-git-commit: db5299d353d6a5e46f2d1707379cd6c364531e47
workflow-type: tm+mt
source-wordcount: '1664'
ht-degree: 24%

---


# Configurar AEM Assets con Brand Portal {#configure-aem-assets-with-brand-portal}

Adobe Experience Manager (AEM) Assets se configura con Brand Portal a través de Adobe Developer Console, que proporciona un distintivo IMS para la autorización del inquilino de Brand Portal.

**¿Cómo funciona la configuración?**

La configuración de AEM Assets con Brand Portal requiere configuraciones tanto en AEM Assets como en Adobe Developer Console.

1. En AEM Assets, cree una cuenta IMS y genere un certificado público (clave pública).
1. En Adobe Developer Console, cree un proyecto para el inquilino (organización) de Brand Portal.
1. En el proyecto, configure una API con la clave pública para crear una conexión de cuenta de servicio (JWT).
1. Obtenga las credenciales de la cuenta de servicio y la información de carga útil de JWT.
1. En AEM Assets, configure la cuenta IMS con las credenciales de cuenta de servicio y la carga útil JWT.
1. En AEM Assets, configure el servicio en la nube de Brand Portal con la cuenta IMS y el extremo de Brand Portal (dirección URL de la organización).
1. Pruebe la configuración publicando un recurso de AEM Assets en Brand Portal.

>[!NOTE]
>
>Una instancia de AEM Assets solo se configurará con un inquilino de Brand Portal.


## Requisitos previos {#prerequisites}

Para configurar AEM Assets con Brand Portal, es necesario lo siguiente:

* Un AEM Assets activo y en ejecución como una instancia de Cloud Service.
* Dirección URL del inquilino de Brand Portal.
* Un usuario con privilegios de administrador del sistema en la organización IMS del inquilino de Brand Portal.

## Crear configuración {#create-new-configuration}

Realice los siguientes pasos en la secuencia especificada para configurar AEM Assets con Brand Portal.

1. [Obtener un certificado público](#public-certificate)
1. [Crear conexión de cuenta de servicio (JWT)](#createnewintegration)
1. [Configurar cuenta de IMS](#create-ims-account-configuration)
1. [Configurar el servicio en la nube](#configure-the-cloud-service)
1. [Probar la configuración](#test-configuration)

### Crear la configuración de IMS {#create-ims-configuration}

La configuración de IMS autentica el inquilino de Brand Portal con AEM Assets.

La configuración de IMS incluye dos pasos:

* [Obtener un certificado público](#public-certificate)
* [Configurar cuenta de IMS](#create-ims-account-configuration)

### Obtener un certificado público {#public-certificate}

El certificado público le permite autenticar su perfil en Adobe Developer Console.

1. Inicie sesión en AEM Assets.

1. From the **Tools** ![Tools](assets/tools.png) panel, navigate to **[!UICONTROL Security]** > **[!UICONTROL Adobe IMS Configurations]**.

   ![Interfaz de usuario de configuración de cuenta de Adobe IMS](assets/ims-configuration1.png)

1. En la página Configuraciones de IMS de Adobe, haga clic en **[!UICONTROL Crear]**.

1. Se le redirige a la página de configuración **[!UICONTROL de la cuenta técnica de IMS de]** Adobe. By default, the **Certificate** tab opens.

   Seleccione el portal **[!UICONTROL de marcas de]** Adobe de la solución de nube.

1. Mark the **[!UICONTROL Create new certificate]** checkbox and specify an **alias** for the certificate. El alias sirve como nombre del certificado.

1. Haga clic en **[!UICONTROL Crear certificado]**. A continuación, haga clic en **[!UICONTROL Aceptar]** en el cuadro de diálogo para generar el certificado público.

   ![Crear certificado](assets/ims-config2.png)

1. Click **[!UICONTROL Download Public Key]** and save the certificate (.crt) file on your machine.

   El archivo de certificado se utilizará más adelante para configurar la API para el inquilino de Brand Portal y generar las credenciales de cuenta de servicio en Adobe Developer Console.

   ![Descargar certificado](assets/ims-config3.png)

1. Haga clic en **[!UICONTROL Siguiente]**. 

   En la ficha **Cuenta** , se crea la cuenta IMS de Adobe, pero para ello necesitará las credenciales de cuenta de servicio que se generan en la Consola de programadores de Adobe. Mantenga esta página abierta por ahora.

   Abra una nueva ficha y [cree una conexión de cuenta de servicio (JWT) en la consola](#createnewintegration) de desarrollador de Adobe para obtener las credenciales y la carga útil JWT para configurar la cuenta de IMS.

### Crear conexión de cuenta de servicio (JWT) {#createnewintegration}

En Adobe Developer Console, los proyectos y las API se configuran en el nivel de inquilino (organización) de Brand Portal. La configuración de una API crea una conexión de cuenta de servicio (JWT) en la consola de desarrollador de Adobe. Existen dos métodos para configurar la API, mediante la generación de un par de claves (claves privadas y públicas) o mediante la carga de una clave pública. Para configurar AEM Assets con Brand Portal, debe generar un certificado público (clave pública) en AEM Assets y crear credenciales en Adobe Developer Console cargando la clave pública. Esta clave pública se utiliza para configurar la API para el inquilino de Brand Portal seleccionado y genera las credenciales y la carga útil JWT para la cuenta de servicio. Estas credenciales se utilizan además para configurar la cuenta de IMS en AEM Assets. Una vez configurada la cuenta de IMS, puede configurar el servicio en la nube de Brand Portal en AEM Assets.

Realice los siguientes pasos para generar las credenciales de cuenta de servicio y la carga útil JWT:

1. Inicie sesión en Adobe Developer Console con privilegios de administrador del sistema en la organización de IMS (inquilino de Brand Portal). La dirección URL predeterminada es

   [https://www.adobe.com/go/devs_console_ui](https://www.adobe.com/go/devs_console_ui)


   >[!NOTE]
   >
   >Asegúrese de seleccionar la organización de IMS correcta (inquilino de Brand Portal) en la lista desplegable (organización) situada en la esquina superior derecha.

1. Click **[!UICONTROL Create new project]**. Se crea un proyecto en blanco para su organización.

   Haga clic en **[!UICONTROL Editar proyecto]** para actualizar el título **[!UICONTROL y la]** descripción **[!UICONTROL del]** proyecto y, a continuación, haga clic en **[!UICONTROL Guardar]**.

   ![Crear proyecto](assets/service-account1.png)

1. En la ficha Información general **[!UICONTROL del]** proyecto, haga clic en **[!UICONTROL Añadir API]**.

   ![Añadir API](assets/service-account2.png)

1. En la ventana **** Añadir una API, seleccione **[!UICONTROL AEM portal]** de marca y haga clic en **[!UICONTROL Siguiente]**.

   Asegúrese de tener acceso al servicio AEM Brand Portal.

1. En la ventana **[!UICONTROL Configurar API]** , haga clic en **[!UICONTROL Cargar la clave]** pública. A continuación, haga clic en **[!UICONTROL Seleccionar un archivo]** y cargue el certificado público (archivo .crt) que ha descargado en la sección [Obtener certificado](#public-certificate) público.

   Haga clic en **[!UICONTROL Siguiente]**. 

   ![Cargar clave pública](assets/service-account3.png)

1. Compruebe el certificado público y haga clic en **[!UICONTROL Siguiente]**.

1. Seleccione el portal **[!UICONTROL de marca perfil]** Assets del producto predeterminado y haga clic en **[!UICONTROL Guardar API]** configurada.

   <!-- 
   In Brand Portal, a default profile is created for each organization. The Product Profiles are created in admin console for assigning users to groups (based on the roles and permissions). For configuration with Brand Portal, the OAuth token is created at organization level. Therefore, you must configure the default Product Profile for your organization. 
   -->

   ![Seleccionar Perfil de producto](assets/service-account4.png)

1. Con la API configurada, se le redirige a la información general de la API. En el panel de navegación izquierdo, en **[!UICONTROL Credenciales]**, haga clic en Cuenta **[!UICONTROL de servicio (JWT)]**.

   >[!NOTE]
   >
   >Puede vista de las credenciales y realizar otras acciones (generar tokens JWT, copiar detalles de credenciales, recuperar el secreto del cliente, etc.) según sea necesario.

1. En la ficha **[!UICONTROL Credenciales]** de cliente, copie el ID **[!UICONTROL de]** cliente.

   Click **[!UICONTROL Retrieve Client Secret]** and copy the **[!UICONTROL client secret]**.

   ![Credenciales de cuenta de servicio](assets/service-account5.png)

1. Navigate to the **[!UICONTROL Generate JWT]** tab and copy the **[!UICONTROL JWT Payload]**.

Ahora puede utilizar el ID de cliente (clave de API), el secreto de cliente y la carga útil JWT para [configurar la cuenta](#create-ims-account-configuration) IMS en AEM Assets.

<!--
1. Click **[!UICONTROL Create Integration]**.

1. Select **[!UICONTROL Access an API]**, and click **[!UICONTROL Continue]**.

   ![Create New Integration](assets/create-new-integration1.png)

1. Create a new integration page opens. 
   
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

   The API Key, Client Secret key, and JWT payload information will be used to create IMS account configuration.

-->

### Configurar cuenta de IMS {#create-ims-account-configuration}

Asegúrese de haber realizado los siguientes pasos:

* [Obtener un certificado público](#public-certificate)
* [Crear conexión de cuenta de servicio (JWT)](#createnewintegration)

Realice los siguientes pasos para configurar la cuenta de IMS.

1. Abra la Configuración de IMS y vaya a la ficha **[!UICONTROL Cuenta]** . Mantuvo la página abierta mientras [obtenía el certificado](#public-certificate)público.

1. Especifique un **[!UICONTROL Título]** para la cuenta de IMS.

   En **[!UICONTROL Servidor de autorización]**, introduzca la dirección URL: [https://ims-na1.adobelogin.com/](https://ims-na1.adobelogin.com/)

   Pegue la clave **[!UICONTROL de]** API (ID de cliente), **[!UICONTROL Secreto]** de cliente y Carga **[!UICONTROL útil]** (carga útil JWT) que ha copiado al [crear la conexión](#createnewintegration)de cuenta de servicio (JWT).

   Haga clic en **[!UICONTROL Crear]**.

   La cuenta de IMS está configurada.

   ![Configuración de cuenta de IMS](assets/create-new-integration6.png)


1. Select the IMS account configuration and click **[!UICONTROL Check Health]**.

   Haga clic en **[!UICONTROL Proteger]** en el cuadro de diálogo. Si la configuración es correcta, aparece un mensaje que indica que el *token se recupera correctamente*.

   ![](assets/create-new-integration5.png)

>[!CAUTION]
>
>Sólo debe tener una configuración de IMS.
>
>Asegúrese de que la configuración de IMS pase la comprobación de estado. Si la configuración no pasa la comprobación de estado, no es válida. Debe eliminarla y crear una configuración nueva y válida.



### Configurar el servicio en la nube {#configure-the-cloud-service}

Siga los pasos siguientes para configurar el servicio en la nube de Brand Portal:

1. Inicie sesión en AEM Assets.

1. From the **Tools** ![Tools](assets/tools.png) panel, navigate to **[!UICONTROL Cloud Services]** > **[!UICONTROL AEM Brand Portal]**.

1. En la página Configuraciones de Brand Portal, haga clic en **[!UICONTROL Crear]**.

1. Especifique un **[!UICONTROL Título]** para la configuración.

   Seleccione la configuración de IMS que ha creado al [configurar la cuenta](#create-ims-account-configuration)de IMS.

   In the **[!UICONTROL Service URL]**, enter your Brand Portal tenant (organization URL).

   ![](assets/create-cloud-service.png)

1. Haga clic en **[!UICONTROL Guardar y cerrar]**. Se crea la configuración de nube.

   La instancia de AEM Assets como Cloud Service ahora está configurada con el inquilino de Brand Portal.

### Probar la configuración{#test-configuration}

Realice los siguientes pasos para validar la configuración:

1. Inicie sesión en AEM Assets.

1. From the **Tools** ![Tools](assets/tools.png) panel, navigate to **[!UICONTROL Deployment]** > **[!UICONTROL Distribution]**.

   ![](assets/test-bpconfig1.png)

   A Brand Portal distribution agent (**[!UICONTROL bpdistributionagent0]**) is created under **[!UICONTROL Publish to Brand Portal]**.

   ![](assets/test-bpconfig2.png)

   >[!NOTE]
   >
   >De forma predeterminada, se crea un agente de distribución para un inquilino de Brand Portal.

1. Haga clic en **[!UICONTROL Publicar en Brand Portal]** para abrir el agente de distribución.

   Puede ver las colas de distribución en la ficha **[!UICONTROL Estado]** .

   Un agente de distribución contiene dos colas:
   * **processing-queue**: para la distribución de recursos a Brand Portal.

   * **error-queue**: para los recursos en los que la distribución ha fallado.
   >[!NOTE]
   >
   >Se recomienda revisar los errores y borrar la **cola de errores** periódicamente.

   ![](assets/test-bpconfig3.png)

1. Para comprobar la conexión entre AEM Assets y Brand Portal, haga clic en **[!UICONTROL Probar conexión]**.

   ![](assets/test-bpconfig4.png)

   A message appears at the bottom of the page that your *test package is successfully delivered*.

   >[!NOTE]
   >
   >Evite desactivar el agente de distribución, ya que puede provocar errores en la distribución de los recursos (que se ejecutan en la cola).


Ahora puede:

* [Publicar recursos desde AEM Assets en Brand Portal](publish-to-brand-portal.md)
* [Publicar carpetas desde AEM Assets en Brand Portal](publish-to-brand-portal.md#publish-folders-to-brand-portal)
* [Publicar colecciones desde AEM Assets en Brand Portal](publish-to-brand-portal.md#publish-collections-to-brand-portal)

Además de lo anterior, también puede publicar esquemas de metadatos, etiquetas, ajustes preestablecidos de imagen y facetas de búsqueda de AEM Assets en Brand Portal.

* [Publicar ajustes preestablecidos, esquemas y facetas en Brand Portal](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/publish/publish-schema-search-facets-presets.html)
* [Publicar etiquetas en Brand Portal](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/publish/brand-portal-publish-tags.html)


Consulte la [documentación de Brand Portal](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/home.html) para obtener más información.


## Registros de distribución {#distribution-logs}

Puede supervisar los registros del agente de distribución para el flujo de trabajo de publicación de recursos.

Por ejemplo, hemos publicado un recurso de AEM Assets a Brand Portal para validar la configuración.

1. Follow the steps (from 1 to 4) as shown in the [Test Configuration](#test-configuration) section and navigate to the distribution agent page.

1. Haga clic en **[!UICONTROL Registros]** para ver los registros de distribución. Aquí puede ver los registros de procesamiento y de errores.

   ![](assets/test-bpconfig5.png)

El agente de distribución genera los siguientes registros:

* INFORMACIÓN: Es un registro generado por el sistema que se activa en la configuración correcta del agente de distribución.
* DSTRQ1 (Solicitud 1): Se activa en comprobar la conexión.

Al publicar el recurso, se generan los siguientes registros de solicitud y respuesta:

**Solicitud del agente de distribución**:
* DSTRQ2 (Solicitud 2): Se activa la solicitud de publicación de recursos.
* DSTRQ3 (Solicitud 3): El sistema activa otra solicitud para publicar la carpeta AEM Assets (en la que el recurso existe) y replica la carpeta en Brand Portal.

**Respuesta del agente de distribución**:
* queue-bpdistributionagent0 (DSTRQ2): El recurso se publica en Brand Portal.
* queue-bpdistributionagent0 (DSTRQ3): El sistema replica la carpeta AEM Assets (que contiene el recurso) en Brand Portal.

En el ejemplo anterior, se activa una solicitud y una respuesta adicionales. El sistema no pudo encontrar la carpeta principal (denominada ruta de Añado) en Brand Portal porque el recurso se publicó por primera vez, por lo que activó una solicitud adicional para crear una carpeta principal con el mismo nombre en Brand Portal donde se publica el recurso.

>[!NOTE]
>
>Se genera una solicitud adicional en caso de que la carpeta principal no exista en Brand Portal o se haya modificado en AEM Assets.



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
