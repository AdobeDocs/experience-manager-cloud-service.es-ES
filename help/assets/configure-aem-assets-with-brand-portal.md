---
title: Configurar AEM Assets como [!DNL Cloud Service] con Brand Portal
description: Configurar AEM Assets con Brand Portal.
contentOwner: Vishabh Gupta
translation-type: tm+mt
source-git-commit: db653daa2d3c271329812b35960f50ee22fb9943
workflow-type: tm+mt
source-wordcount: '1629'
ht-degree: 20%

---


# Configure AEM Assets como [!DNL Cloud Service] con Brand Portal {#configure-aem-assets-with-brand-portal}

La configuración de Adobe Experience Manager Assets Brand Portal le permite publicar recursos de marca aprobados desde Adobe Experience Manager Assets como una instancia [!DNL Cloud Service] en Brand Portal y distribuirlos a los usuarios de Brand Portal.

**Flujo de trabajo de configuración**

AEM Assets como [!DNL Cloud Service] se configura con Brand Portal a través de Adobe Developer Console, que obtiene un token de cuenta de Identity Management Services (IMS) de Adobe para la autorización del inquilino de Brand Portal. Requiere configuraciones tanto en AEM Assets como en Adobe Developer Console.

1. En AEM Assets, cree una cuenta de IMS y genere una clave pública (certificado).
1. En Adobe Developer Console, cree un proyecto para el inquilino (organización) de Brand Portal.
1. En el proyecto, configure una API con la clave pública para crear una conexión de cuenta de servicio.
1. Obtenga las credenciales de la cuenta de servicio y la información de carga útil de JSON Web Token (JWT).
1. En AEM Assets, configure la cuenta IMS con las credenciales de cuenta de servicio y la carga útil JWT.
1. En AEM Assets, configure el servicio en la nube de Brand Portal con la cuenta IMS y el extremo de Brand Portal (dirección URL de la organización).
1. Pruebe la configuración publicando un recurso de AEM Assets en Brand Portal.

>[!NOTE]
>
>Una instancia de AEM Assets como [!DNL Cloud Service] solo se configurará con un inquilino de Brand Portal.

## Requisitos previos {#prerequisites}

Para configurar AEM Assets con Brand Portal, es necesario lo siguiente:

* Un AEM Assets activo y en ejecución como una instancia [!DNL Cloud Service]
* Dirección URL de inquilino de Brand Portal
* Un usuario con privilegios de administrador del sistema en la organización IMS del inquilino de Brand Portal

## Crear configuración {#create-new-configuration}

Realice los siguientes pasos en la secuencia especificada para configurar AEM Assets con Brand Portal.

1. [Obtener un certificado público](#public-certificate)
1. [Crear conexión de cuenta de servicio (JWT)](#createnewintegration)
1. [Configurar cuenta de IMS](#create-ims-account-configuration)
1. [Configurar el servicio en la nube](#configure-the-cloud-service)
1. [Probar la configuración](#test-configuration)

### Crear la configuración de IMS {#create-ims-configuration}

La configuración de IMS autentica su AEM Assets como una instancia [!DNL Cloud Service] con el inquilino de Brand Portal.

La configuración de IMS incluye dos pasos:

* [Obtener un certificado público](#public-certificate)
* [Configurar cuenta de IMS](#create-ims-account-configuration)

### Obtener un certificado público {#public-certificate}

La clave pública (certificado) autentica el perfil en Adobe Developer Console.

1. Inicie sesión en AEM Assets.
1. En el panel **Herramientas**, vaya a **[!UICONTROL Seguridad]** > **[!UICONTROL Configuraciones de IMS de Adobe]**.
1. En la página Configuraciones de IMS de Adobe, haga clic en **[!UICONTROL Crear]**. Redireccionará a la página **[!UICONTROL Configuración de cuenta técnica de IMS de Adobe]**. De forma predeterminada, se abre la ficha **Certificado**.
1. Seleccione **[!UICONTROL Adobe Brand Portal]** en la lista desplegable **[!UICONTROL Cloud Solution]**.
1. Active la casilla de verificación **[!UICONTROL Crear nuevo certificado]** y especifique un **alias** para la clave pública. El alias sirve como nombre de la clave pública.
1. Haga clic en **[!UICONTROL Crear certificado]**. A continuación, haga clic en **[!UICONTROL Aceptar]** para generar la clave pública.

   ![Crear certificado](assets/ims-config2.png)

1. Haga clic en el icono **[!UICONTROL Descargar clave pública]** y guarde el archivo de clave pública (CRT) en su equipo.

   La clave pública se utilizará más adelante para configurar la API para el inquilino de Brand Portal y generar las credenciales de cuenta de servicio en Adobe Developer Console.

   ![Descargar certificado](assets/ims-config3.png)

1. Haga clic en **[!UICONTROL Siguiente]**. 

   En la ficha **Cuenta**, se crea una cuenta IMS de Adobe que requiere las credenciales de cuenta de servicio que se generan en la Consola de programadores de Adobe. Mantenga esta página abierta por ahora.

   Abra una nueva ficha y [cree una conexión de cuenta de servicio (JWT) en Adobe Developer Console](#createnewintegration) para obtener las credenciales y la carga útil JWT para configurar la cuenta de IMS.

### Crear una conexión de cuenta de servicio (JWT) {#createnewintegration}

En Adobe Developer Console, los proyectos y las API se configuran en el nivel de inquilino (organización) de Brand Portal. La configuración de una API crea una conexión de cuenta de servicio (JWT). Existen dos métodos para configurar la API, mediante la generación de un par de claves (claves privadas y públicas) o mediante la carga de una clave pública. Para configurar AEM Assets con Brand Portal, debe generar una clave pública (certificado) en AEM Assets y crear credenciales en Adobe Developer Console cargando la clave pública. Estas credenciales son necesarias para configurar la cuenta de IMS en AEM Assets. Una vez configurada la cuenta de IMS, puede configurar el servicio en la nube de Brand Portal en AEM Assets.

Realice los siguientes pasos para generar las credenciales de cuenta de servicio y la carga útil JWT:

1. Inicie sesión en Adobe Developer Console con privilegios de administrador del sistema en la organización de IMS (inquilino de Brand Portal). La dirección URL predeterminada es [https://www.adobe.com/go/devs_console_ui](https://www.adobe.com/go/devs_console_ui).


   >[!NOTE]
   >
   >Asegúrese de seleccionar la organización de IMS correcta (inquilino de Brand Portal) en la lista desplegable (organización) situada en la esquina superior derecha.

1. Haga clic en **[!UICONTROL Crear nuevo proyecto]**. Se crea un proyecto en blanco con un nombre generado por el sistema para su organización.

   Haga clic en **[!UICONTROL Editar proyecto]** para actualizar el **[!UICONTROL Título del proyecto]** y **[!UICONTROL Descripción]**, y haga clic en **[!UICONTROL Guardar]**.

1. En la ficha **[!UICONTROL Información general del proyecto]**, haga clic en **[!UICONTROL Añadir API]**.

1. En **[!UICONTROL Añada una ventana de API]**, seleccione **[!UICONTROL AEM Brand Portal]** y haga clic en **[!UICONTROL Siguiente]**.

   Asegúrese de tener acceso al servicio AEM Brand Portal.

1. En la ventana **[!UICONTROL Configurar API]**, haga clic en **[!UICONTROL Cargar la clave pública]**. A continuación, haga clic en **[!UICONTROL Seleccione un archivo]** y cargue la clave pública (archivo .crt) que ha descargado en la sección [obtener certificado público](#public-certificate).

   Haga clic en **[!UICONTROL Siguiente]**. 

   ![Cargar clave pública](assets/service-account3.png)

1. Verifique la clave pública y haga clic en **[!UICONTROL Siguiente]**.

1. Seleccione **[!UICONTROL Assets Brand Portal]** como perfil de producto predeterminado y haga clic en **[!UICONTROL Guardar API configurada]**.

   <!-- 
   In Brand Portal, a default profile is created for each organization. The Product Profiles are created in admin console for assigning users to groups (based on the roles and permissions). For configuration with Brand Portal, the OAuth token is created at organization level. Therefore, you must configure the default Product Profile for your organization. 
   -->

   ![Seleccionar Perfil de producto](assets/service-account4.png)

1. Una vez configurada la API, se le redirige a la página de información general de la API. En el panel de navegación izquierdo de **[!UICONTROL Credenciales]**, haga clic en la opción **[!UICONTROL Cuenta de servicio (JWT)]**.

   >[!NOTE]
   >
   >Puede vista de las credenciales y realizar acciones como generar tokens JWT, copiar detalles de credenciales, recuperar el secreto del cliente, etc.

1. En la ficha **[!UICONTROL Credenciales del cliente]**, copie el **[!UICONTROL ID del cliente]**.

   Haga clic en **[!UICONTROL Recuperar secreto de cliente]** y copie el **[!UICONTROL secreto de cliente]**.

   ![Credenciales de cuenta de servicio](assets/service-account5.png)

1. Vaya a la ficha **[!UICONTROL Generar JWT]** y copie la información **[!UICONTROL Carga útil JWT]**.

Ahora puede utilizar el ID de cliente (clave de API), el secreto de cliente y la carga útil JWT para [configurar la cuenta de IMS](#create-ims-account-configuration) en AEM Assets.

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

1. Abra la Configuración de IMS y vaya a la ficha **[!UICONTROL Cuenta]**. La página se mantuvo abierta mientras [obtenía el certificado público](#public-certificate).

1. Especifique un **[!UICONTROL Título]** para la cuenta de IMS.

   En el campo **[!UICONTROL Servidor de autorización]**, especifique la dirección URL: [https://ims-na1.adobelogin.com/](https://ims-na1.adobelogin.com/)

   Especifique el ID de cliente en el campo **[!UICONTROL clave de API]**, **[!UICONTROL Secreto de cliente]** y **[!UICONTROL Carga útil]** (carga útil JWT) que ha copiado mientras [crea la conexión de cuenta de servicio (JWT)](#createnewintegration).

   Haga clic en **[!UICONTROL Crear]**.

   La cuenta de IMS está configurada.

   ![Configuración de cuenta de IMS](assets/create-new-integration6.png)


1. Seleccione la configuración de cuenta de IMS y haga clic en **[!UICONTROL Comprobar estado]**.

   Haga clic en **[!UICONTROL Marcar]** en el cuadro de diálogo. Si la configuración es correcta, aparece un mensaje que indica que el *token se recupera correctamente*.

   ![](assets/create-new-integration5.png)

>[!CAUTION]
>
>Sólo debe tener una configuración de IMS.
>
>Asegúrese de que la configuración de IMS pase la comprobación de estado. Si la configuración no pasa la comprobación de estado, no es válida. Debe eliminarla y crear una configuración nueva y válida.

### Configurar el servicio en la nube {#configure-the-cloud-service}

Siga los pasos siguientes para configurar el servicio en la nube de Brand Portal:

1. Inicie sesión en AEM Assets.

1. En el panel **Herramientas**, vaya a **[!UICONTROL Cloud Services]** > **[!UICONTROL AEM Brand Portal]**.

1. En la página Configuraciones de Brand Portal, haga clic en **[!UICONTROL Crear]**.

1. Especifique un **[!UICONTROL Título]** para la configuración.

   Seleccione la configuración de IMS que creó mientras [configuraba la cuenta de IMS](#create-ims-account-configuration).

   En el campo **[!UICONTROL URL del servicio]**, especifique la dirección URL del inquilino (organización) de Brand Portal.

   ![](assets/create-cloud-service.png)

1. Haga clic en **[!UICONTROL Guardar y cerrar]**. Se crea la configuración de nube.

   El AEM Assets como instancia [!DNL Cloud Service] ahora está configurado con el inquilino de Brand Portal.

### Probar la configuración{#test-configuration}

Realice los siguientes pasos para validar la configuración:

1. Inicie sesión en AEM Assets.

1. En el panel **Herramientas**, vaya a **[!UICONTROL Implementación]** > **[!UICONTROL Distribución]**.

   ![](assets/test-bpconfig1.png)

   Se crea un agente de distribución de Brand Portal (**[!UICONTROL bpdistributionagent0]**) en **[!UICONTROL Publicar en Brand Portal]**.

   ![](assets/test-bpconfig2.png)


1. Haga clic en **[!UICONTROL Publicar en Brand Portal]** para abrir el agente de distribución.

   Puede ver las colas de distribución en la ficha **[!UICONTROL Estado]**.

   Un agente de distribución contiene dos colas:
   * **processing-queue**: para la distribución de recursos a Brand Portal.

   * **error-queue**: para los recursos en los que la distribución ha fallado.
   >[!NOTE]
   >
   >Se recomienda revisar los errores y borrar la **cola de errores** periódicamente.

   ![](assets/test-bpconfig3.png)

1. Para verificar la conexión entre AEM Assets como [!DNL Cloud Service] y Brand Portal, haga clic en el icono **[!UICONTROL Probar conexión]**.

   ![](assets/test-bpconfig4.png)

   Aparece un mensaje que indica que el paquete de prueba *se entrega correctamente*.

   >[!NOTE]
   >
   >Evite desactivar el agente de distribución, ya que puede provocar errores en la distribución de los recursos (que se ejecutan en la cola).

Ahora puede:

* [Publicar recursos desde AEM Assets en Brand Portal](publish-to-brand-portal.md)
* [Publicar carpetas desde AEM Assets en Brand Portal](publish-to-brand-portal.md#publish-folders-to-brand-portal)
* [Publicar colecciones desde AEM Assets en Brand Portal](publish-to-brand-portal.md#publish-collections-to-brand-portal)
* [Publicar ajustes preestablecidos, esquemas y facetas en Brand Portal](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/publish/publish-schema-search-facets-presets.html)
* [Publicar etiquetas en Brand Portal](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/publish/brand-portal-publish-tags.html)

Consulte la [documentación de Brand Portal](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/home.html) para obtener más información.

## Registros de distribución {#distribution-logs}

Puede supervisar los registros del agente de distribución para el flujo de trabajo de publicación de recursos.

Por ejemplo, hemos publicado un recurso de AEM Assets a Brand Portal para validar la configuración.

1. Siga los pasos (del 1 al 4) que se muestran en la sección [Configuración de la prueba](#test-configuration) y vaya a la página del agente de distribución.
1. Haga clic en **[!UICONTROL Registros]** para vista de los registros de procesamiento y error.

   ![](assets/test-bpconfig5.png)

El agente de distribución ha generado los siguientes registros:

* INFORMACIÓN: Es un registro generado por el sistema que déclencheur en una configuración correcta del agente de distribución.
* DSTRQ1 (Solicitud 1): Se activa en comprobar la conexión.

Al publicar el recurso, se generan los siguientes registros de solicitud y respuesta:

**Solicitud del agente de distribución**:

* DSTRQ2 (Solicitud 2): Se activa la solicitud de publicación de recursos.
* DSTRQ3 (Solicitud 3): El sistema déclencheur otra solicitud para publicar la carpeta AEM Assets (en la que el recurso existe) y replica la carpeta en Brand Portal.

**Respuesta del agente de distribución**:

* queue-bpdistributionagent0 (DSTRQ2): El recurso se publica en Brand Portal.
* queue-bpdistributionagent0 (DSTRQ3): El sistema replica la carpeta AEM Assets (que contiene el recurso) en Brand Portal.

En el ejemplo anterior, se activa una solicitud y una respuesta adicionales. El sistema no encontró la carpeta principal (Añadir ruta) en Brand Portal porque el recurso se publicó por primera vez, por lo que activó una solicitud adicional para crear una carpeta principal con el mismo nombre en Brand Portal donde se publica el recurso.

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
