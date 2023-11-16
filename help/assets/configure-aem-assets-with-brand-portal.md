---
title: Configuración de AEM Assets as a [!DNL Cloud Service] con Brand Portal
description: Obtenga información sobre cómo configurar AEM Assets con Brand Portal. AEM La configuración le permite publicar recursos de marca aprobados de una instancia de en Brand Portal y distribuirlos a los usuarios de Brand Portal.
contentOwner: AK
feature: Brand Portal,Asset Distribution,Configuration
role: Admin
exl-id: 078e522f-bcd8-4734-95db-ddc8772de785
source-git-commit: a3e79441d46fa961fcd05ea54e84957754890d69
workflow-type: tm+mt
source-wordcount: '2585'
ht-degree: 12%

---

# Configuración de Experience Manager Assets con Brand Portal {#configure-aem-assets-with-brand-portal}

| Versión | Vínculo del artículo |
| -------- | ---------------------------- |
| AEM 6.5 | [Haga clic aquí](https://experienceleague.adobe.com/docs/experience-manager-65/assets/brandportal/configure-aem-assets-with-brand-portal.html?lang=es) |
| AEM as a Cloud Service | Este artículo |

La configuración de Adobe Experience Manager Assets Brand Portal permite publicar recursos de marca aprobados desde Adobe Experience Manager Assets como [!DNL Cloud Service] instancia de a Brand Portal y distribuirlas a los usuarios de Brand Portal.

## Activar Brand Portal mediante Cloud Manager {#activate-brand-portal}

El usuario de Cloud Manager activa Brand Portal for an Experience Manager Assets as a [!DNL Cloud Service] ejemplo. El flujo de trabajo de activación crea las configuraciones necesarias (token de autorización, configuración de IMS y servicio en la nube de Brand Portal) en el back-end y refleja el estado del inquilino de Brand Portal en Cloud Manager. La activación de Brand Portal permite a los usuarios de Experience Manager Assets publicar recursos en Brand Portal y distribuirlos a los usuarios de Brand Portal.

**Requisitos previos**

Para activar Brand Portal en su Experience Manager Assets as a, necesita lo siguiente [!DNL Cloud Service] instancia:

* Un Experience Manager Assets as a en funcionamiento [!DNL Cloud Service] ejemplo.
* Un usuario con acceso a Cloud Manager asignado a Perfiles del producto Cloud Manager. Consulte [acceso a Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/security/ims-support.html#accessing-cloud-manager) para obtener más información.

>[!NOTE]
>
>Se requiere un entorno de producción configurado para configurar un Experience Manager Assets as a [!DNL Cloud Service] instancia para conectarse con el inquilino de Brand Portal.

**Pasos para activar Brand Portal**

Puede activar Brand Portal al crear los entornos de producción para su Experience Manager Assets as a [!DNL Cloud Service] por ejemplo, o por separado. Supongamos que el entorno ya se ha creado y que ahora es necesario activar Brand Portal.

1. Inicie sesión en Adobe Cloud Manager y navegue hasta **[!UICONTROL Entornos]**.

   El **[!UICONTROL Entornos]** Esta página muestra la lista de todos los entornos existentes.

1. Seleccione los entornos (uno a uno) de la lista para ver los detalles del entorno.

   Brand Portal tiene derecho a uno de los entornos disponibles y se refleja en la **[!UICONTROL Información del entorno]**.

   Cuando encuentre el entorno asociado a Brand Portal, haga clic en **[!UICONTROL Activar Brand Portal]** para iniciar el flujo de trabajo de activación.

   ![Activar Brand Portal](assets/create-environment4.png)

1. Se tarda unos minutos en activar el inquilino de Brand Portal, ya que el flujo de trabajo de activación crea las configuraciones necesarias en el back-end. Una vez activado el inquilino de Brand Portal, el estado cambia a Activado.

   ![Ver estado](assets/create-environment5.png)


>[!NOTE]
>
>Brand Portal debe activarse en la misma organización de IMS que de Experience Manager Assets como [!DNL Cloud Service] ejemplo.
>
>Si tiene una configuración de nube de Brand Portal existente ([configurado manualmente con la consola de Adobe Developer](#manual-configuration)) para una organización de IMS (org1-existing) y su Experience Manager Assets as a [!DNL Cloud Service] está configurada para otra organización de IMS (org2-new), la activación de Brand Portal desde Cloud Manager restablece la organización de IMS de Brand Portal a `org2-new`. Aunque la configuración de nube configurada manualmente en `org1-existing` es visible en la instancia de autor de Experience Manager Assets, pero ya no estará en uso después de activar Brand Portal desde Cloud Manager.
>
>Si la configuración de nube de Brand Portal existente y Experience Manager Assets as a [!DNL Cloud Service] Las instancias de utilizan la misma organización de IMS (org1), solo debe activar Brand Portal desde Cloud Manager.
>
>No modifique ninguna configuración generada automáticamente.

**Consulte también**:

* [Agregar usuarios y funciones en Experience Manager Assets as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/requirements/setting-up-users-and-roles.html)

* [Administrar entornos en Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/manage-environments.html#adding-environments)


**Inicie sesión en su inquilino de Brand Portal**:

Después de la activación del inquilino de Brand Portal en Cloud Manager, puede iniciar sesión en Brand Portal desde el Admin Console o directamente mediante la URL del inquilino.

La URL predeterminada del inquilino de Brand Portal es: `https://<tenant-id>.brand-portal.adobe.com/`.

Donde, el ID de inquilino es la organización de IMS.

Realice los siguientes pasos si no está seguro de la dirección URL de Brand Portal:

1. Inicie sesión en [Admin Console](https://adminconsole.adobe.com/) y vaya a **[!UICONTROL Productos]**.
1. En el panel izquierdo, seleccione **[!UICONTROL ADOBE EXPERIENCE MANAGER BRAND PORTAL - BRAND PORTAL]**.
1. Clic **[!UICONTROL Ir a Brand Portal]** para abrir directamente Brand Portal en el explorador.

   O bien copie la URL del inquilino de Brand Portal desde el **[!UICONTROL Ir a Brand Portal]** y péguelo en el explorador para abrir la interfaz de Brand Portal.

   ![Acceso a Brand Portal](assets/access-bp-on-cloud.png)


**Probar conexión**

Realice los siguientes pasos para validar la conexión entre su Experience Manager Assets as a [!DNL Cloud Service] instancia e inquilino de Brand Portal:

1. Inicie sesión en Experience Manager Assets.

1. Desde el **Herramientas** panel, vaya a **[!UICONTROL Implementación]** > **[!UICONTROL Distribución]**.

   ![Vaya a la opción de distribución](assets/test-bpconfig1.png)

   Un agente de distribución de Brand Portal (**[!UICONTROL bpdistributionagent0]**) se crea en **[!UICONTROL Publicar en Brand Portal]**.

   ![Crear agente de distribución](assets/test-bpconfig2.png)

1. Clic **[!UICONTROL Publicar en Brand Portal]** para abrir el agente de distribución.

   Puede ver las colas de distribución debajo de **[!UICONTROL Estado]** pestaña.

   Un agente de distribución contiene dos colas:
   * **processing-queue**: para la distribución de recursos a Brand Portal.

   * **error-queue**: para los recursos en los que la distribución ha fallado.

   >[!NOTE]
   >
   >Se recomienda revisar los errores y borrar la **cola de errores** periódicamente.

   ![Cola de procesamiento para la distribución de recursos](assets/test-bpconfig3.png)

1. Para comprobar la conexión entre Experience Manager Assets as a [!DNL Cloud Service] y Brand Portal, haga clic en **[!UICONTROL Probar conexión]** icono.

   ![AEM Verificación de la conexión entre la aplicación y Brand Portal](assets/test-bpconfig4.png)

   Aparece un mensaje que indica que su *el paquete de prueba se entregó correctamente*.

   >[!NOTE]
   >
   >Evite desactivar el agente de distribución, ya que puede provocar errores en la distribución de los recursos (que se ejecutan en la cola).

Para comprobar la conexión entre su Experience Manager Assets as a [!DNL Cloud Service] y el inquilino de Brand Portal, publique un recurso de Experience Manager Assets en Brand Portal. Si la conexión se realiza correctamente, el recurso publicado se podrá ver en la interfaz de Brand Portal.


Ahora puede:

* [Publicación de recursos de Experience Manager Assets en Brand Portal](publish-to-brand-portal.md)
* [Publicar carpetas desde Experience Manager Assets en Brand Portal](publish-to-brand-portal.md#publish-folders-to-brand-portal)
* [Publicar colecciones desde Experience Manager Assets en Brand Portal](publish-to-brand-portal.md#publish-collections-to-brand-portal)
* [Publicación de recursos de Brand Portal en Experience Manager Assets](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/asset-sourcing-in-brand-portal/brand-portal-asset-sourcing.html?lang=es) - Abastecimiento de recursos en Brand Portal
* [Publicar ajustes preestablecidos, esquemas y facetas en Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/publish/publish-schema-search-facets-presets.html)
* [Publicar etiquetas en Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/publish/brand-portal-publish-tags.html)

Consulte [Documentación de Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/home.html) para obtener más información.

**Registros de distribución**

Puede monitorizar los registros del agente de distribución para el flujo de trabajo de publicación de recursos.

Ahora vamos a publicar un recurso de Experience Manager Assets en Brand Portal y ver los registros.

1. Siga los pasos (de 1 a 4) que se muestran en la **Probar conexión** y vaya a la página del agente de distribución.
1. Clic **[!UICONTROL Registros]** para ver los registros de procesamiento y de errores.

   ![Registros de procesamiento y errores](assets/test-bpconfig5.png)

El agente de distribución ha generado los siguientes registros:

* INFORMACIÓN: Es un registro generado por el sistema que está en déclencheur con la configuración correcta del agente de distribución.
* DSTRQ1 (Solicitud 1): Se activa en comprobar la conexión.

Al publicar el recurso, se generan los siguientes registros de solicitud y respuesta:

**Solicitud del agente de distribución**:

* DSTRQ2 (Solicitud 2): Se activa la solicitud de publicación de recursos.
* DSTRQ3 (Solicitud 3): El sistema déclencheur otra solicitud para publicar la carpeta Experience Manager Assets (en la que existe el recurso) y replica la carpeta en Brand Portal.

**Respuesta del agente de distribución**:

* queue-bpdistributionagent0 (DSTRQ2): El recurso se publica en Brand Portal.
* queue-bpdistributionagent0 (DSTRQ3): El sistema replica la carpeta Experience Manager Assets (que contiene el recurso) en Brand Portal.

En el ejemplo anterior, se activa una solicitud y una respuesta adicionales. El sistema no pudo encontrar la carpeta principal (Agregar ruta) en Brand Portal porque el recurso se publicó por primera vez, por lo tanto se activó una solicitud adicional para crear una carpeta principal con el mismo nombre en Brand Portal en la que se publica el recurso.

>[!NOTE]
>
>Se genera una solicitud adicional si la carpeta principal no existe en Brand Portal o si se ha modificado en Experience Manager Assets.

Junto con el flujo de trabajo de automatización para activar Brand Portal en Experience Manager Assets as a [!DNL Cloud Service], existe otro método para configurar manualmente Experience Manager Assets como [!DNL Cloud Service] con Brand Portal mediante la consola de Adobe Developer, que ya no se recomienda.

>[!NOTE]
>
>Póngase en contacto con Asistencia al cliente si tiene algún problema al activar el inquilino de Brand Portal.

## Configuración manual mediante la consola de Adobe Developer {#manual-configuration}

En la siguiente sección se describe cómo configurar manualmente Experience Manager Assets as a [!DNL Cloud Service] con Brand Portal mediante la consola de Adobe Developer.

Antes, Experience Manager Assets as a [!DNL Cloud Service] se configuró manualmente con Brand Portal a través de la consola de Adobe Developer, que obtiene un token de cuenta de Adobe de Identity Management Services (IMS) para la autorización del inquilino de Brand Portal. Requiere configuraciones tanto en Experience Manager Assets como en la consola de Adobe Developer.

1. En Experience Manager Assets, cree una cuenta de IMS y genere una clave pública (certificado).
1. En la consola de Adobe Developer, cree un proyecto para el inquilino (organización) de Brand Portal.
1. En el proyecto, configure una API con la clave pública para crear una conexión de cuenta de servicio.
1. Obtenga las credenciales de la cuenta de servicio y la información de carga útil del token web JSON (JWT).
1. En Experience Manager Assets, configure la cuenta de IMS con las credenciales de la cuenta de servicio y la carga útil JWT.
1. En Experience Manager Assets, configure el servicio en la nube de Brand Portal con la cuenta de IMS y el punto final de Brand Portal (URL de la organización).
1. Pruebe la configuración publicando un recurso de Experience Manager Assets en Brand Portal.

>[!NOTE]
>
>Un Experience Manager Assets as a [!DNL Cloud Service] solo se debe configurar con un inquilino de Brand Portal.

**Requisitos previos**

Para configurar Experience Manager Assets con Brand Portal, es necesario lo siguiente:

* Un Experience Manager Assets as a en funcionamiento [!DNL Cloud Service] instancia
* Una URL de inquilino de Brand Portal
* Un usuario con privilegios de administrador del sistema en la organización IMS del inquilino de Brand Portal

## Crear configuración {#create-new-configuration}

Siga estos pasos en la secuencia especificada para configurar Experience Manager Assets con Brand Portal.

1. [Obtener un certificado público](#public-certificate)
1. [Crear una conexión de cuenta de servicio (JWT)](#createnewintegration)
1. [Configuración de la cuenta IMS](#create-ims-account-configuration)
1. [Configurar el servicio en la nube de ](#configure-the-cloud-service)

### Crear la configuración de IMS {#create-ims-configuration}

La configuración de IMS autentica su Experience Manager Assets como [!DNL Cloud Service] con el inquilino de Brand Portal.

La configuración de IMS incluye dos pasos:

* [Obtener un certificado público](#public-certificate)
* [Configuración de la cuenta IMS](#create-ims-account-configuration)

### Obtener un certificado público {#public-certificate}

La clave pública (certificado) autentica el perfil en la consola de Adobe Developer.

1. Inicie sesión en Experience Manager Assets.
1. Desde el **Herramientas** panel, vaya a **[!UICONTROL Seguridad]** > **[!UICONTROL Configuraciones de IMS de Adobe]**.
1. En la página Configuraciones de IMS de Adobe, haga clic en **[!UICONTROL Crear]**. Se redireccionará a la variable **[!UICONTROL Configuración de cuenta técnica de IMS de Adobe]** página. De forma predeterminada, la variable **Certificado** se abre.
1. Seleccionar **[!UICONTROL Adobe Brand Portal]** en el **[!UICONTROL Solución de nube]** lista desplegable.
1. Seleccione el **[!UICONTROL Crear nuevo certificado]** y especifique una **alias** para la clave pública. El alias sirve como nombre de la clave pública.
1. Haga clic en **[!UICONTROL Crear certificado]**. A continuación, haga clic en **[!UICONTROL OK]** para generar la clave pública.

   ![Crear certificado](assets/ims-config2.png)

1. Haga clic en **[!UICONTROL Descargar clave pública]** y guarde el archivo de clave pública (CRT) en el equipo.

   La clave pública se utiliza más adelante para configurar la API del inquilino de Brand Portal y generar credenciales de cuenta de servicio en la consola de Adobe Developer.

   ![Descargar certificado](assets/ims-config3.png)

1. Haga clic en **[!UICONTROL Siguiente]**. 

   En el **Cuenta** pestaña, se crea la cuenta de Adobe IMS que requiere las credenciales de la cuenta de servicio generadas en la consola de Adobe Developer. Mantenga esta página abierta por ahora.

   Abra una pestaña nueva y [crear una conexión de cuenta de servicio (JWT) en la consola de Adobe Developer](#createnewintegration) para obtener las credenciales y la carga útil JWT para configurar la cuenta de IMS.

### Crear una conexión de cuenta de servicio (JWT) {#createnewintegration}

En la consola de Adobe Developer, los proyectos y las API se configuran en el nivel de inquilino (organización) de Brand Portal. Al configurar una API, se crea una conexión de cuenta de servicio (JWT). Existen dos métodos para configurar la API: generar un par de claves (claves pública y privada) o cargar una clave pública. Para configurar Experience Manager Assets con Brand Portal, debe generar una clave pública (certificado) en Experience Manager Assets y crear credenciales en la consola de Adobe Developer cargando la clave pública. Estas credenciales son necesarias para configurar la cuenta de IMS en Experience Manager Assets. Una vez configurada la cuenta de IMS, puede configurar el servicio en la nube de Brand Portal en Experience Manager Assets.

Realice los siguientes pasos para generar las credenciales de la cuenta de servicio y la carga útil JWT:

1. Inicie sesión en la consola de Adobe Developer con privilegios de administrador del sistema en la organización IMS (inquilino de Brand Portal). La URL predeterminada es [https://www.adobe.com/go/devs_console_ui](https://www.adobe.com/go/devs_console_ui).


   >[!NOTE]
   >
   >Asegúrese de haber seleccionado la organización IMS correcta (inquilino de Brand Portal) en la lista desplegable (organización) situada en la esquina superior derecha.

1. Clic **[!UICONTROL Crear nuevo proyecto]**. Se crea un proyecto en blanco con un nombre generado por el sistema para su organización.

   Clic **[!UICONTROL Editar proyecto]** para actualizar el **[!UICONTROL Título del proyecto]** y **[!UICONTROL Descripción]** y haga clic en **[!UICONTROL Guardar]**.

1. En el **[!UICONTROL Resumen del proyecto]** pestaña, haga clic en **[!UICONTROL Añadir API]**.

1. En el **[!UICONTROL Añadir una ventana de API]**, seleccione **[!UICONTROL AEM Brand Portal]** y haga clic en **[!UICONTROL Siguiente]**.

   Asegúrese de que tiene acceso al servicio Experience Manager Brand Portal.

1. En el **[!UICONTROL Configurar API]** , haga clic en **[!UICONTROL Cargar la clave pública]**. A continuación, haga clic en **[!UICONTROL Seleccionar un archivo]** y cargue la clave pública (archivo .crt) descargada en el [obtener un certificado público](#public-certificate) sección.

   Haga clic en **[!UICONTROL Siguiente]**.

   ![Cargar clave pública](assets/service-account3.png)

1. Compruebe la clave pública y haga clic en **[!UICONTROL Siguiente]**.

1. Seleccionar **[!UICONTROL Assets Brand Portal]** como perfil de producto predeterminado y haga clic en **[!UICONTROL Guardar API configurada]**.

   ![Seleccionar perfil de producto](assets/service-account4.png)

1. Una vez configurada la API, se le redirigirá a la página de información general de la API. Desde la parte inferior de navegación izquierda **[!UICONTROL Credenciales]**, haga clic en **[!UICONTROL Cuenta de servicio (JWT)]** opción.

   >[!NOTE]
   >
   >Puede ver las credenciales y realizar acciones como generar tokens JWT, copiar detalles de credenciales, recuperar secretos de cliente, etc.

1. Desde el **[!UICONTROL Credenciales del cliente]** pestaña, copie el **[!UICONTROL ID de cliente]**.

   Clic **[!UICONTROL Recuperar secreto de cliente]** y copie el **[!UICONTROL secreto de cliente]**.

   ![Credenciales de cuenta de servicio](assets/service-account5.png)

1. Vaya a **[!UICONTROL Generar JWT]** y copie la pestaña **[!UICONTROL Carga útil JWT]** información.

Ahora puede utilizar el ID de cliente (clave de API), el secreto de cliente y la carga útil JWT para [configuración de la cuenta de IMS](#create-ims-account-configuration) en Experience Manager Assets.

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

   The API Key, Client Secret key, and JWT payload information is used to create IMS account configuration.

-->

### Configuración de la cuenta IMS {#create-ims-account-configuration}

Asegúrese de haber realizado los siguientes pasos:

* [Obtener un certificado público](#public-certificate)
* [Crear una conexión de cuenta de servicio (JWT)](#createnewintegration)

Siga estos pasos para configurar la cuenta de IMS.

1. Abra la Configuración de IMS y vaya a **[!UICONTROL Cuenta]** pestaña. La página se ha mantenido abierta mientras [obtención del certificado público](#public-certificate).

1. Especifique un **[!UICONTROL Título]** para la cuenta de IMS.

   En el **[!UICONTROL Servidor de autorización]** , especifique la dirección URL: [https://ims-na1.adobelogin.com/](https://ims-na1.adobelogin.com/)

   Especifique el ID de cliente en la **[!UICONTROL Clave de API]** field, **[!UICONTROL Secreto del cliente]**, y **[!UICONTROL Carga útil]** (Carga útil JWT) que ha copiado mientras [creación de la conexión de cuenta de servicio (JWT)](#createnewintegration).

   Haga clic en **[!UICONTROL Crear]**.

   La cuenta de IMS está configurada.

   ![Configuración de cuenta de IMS](assets/create-new-integration6.png)


1. Seleccione la configuración de cuenta de IMS y haga clic en **[!UICONTROL Comprobar estado]**.

   Clic **[!UICONTROL Marque]** en el cuadro de diálogo. Si la configuración se realiza correctamente, aparecerá un mensaje que indica que la variable *Token recuperado correctamente*.

   ![Configuración de IMS de Adobe: Comprobar estado.](assets/create-new-integration5.png)

>[!CAUTION]
>
>Sólo debe tener una configuración de IMS.
>
>Asegúrese de que la configuración de IMS pase la comprobación de estado. Si la configuración no pasa la comprobación de estado, no es válida. Debe eliminarla y crear una configuración nueva y válida.

### Configurar el servicio en la nube de  {#configure-the-cloud-service}

Siga estos pasos para configurar el servicio en la nube de Brand Portal:

1. Inicie sesión en Experience Manager Assets.

1. Desde el **Herramientas** panel, vaya a **[!UICONTROL Cloud Service]** > **[!UICONTROL AEM Brand Portal]**.

1. En la página Configuraciones de Brand Portal, haga clic en **[!UICONTROL Crear]**.

1. Especifique un **[!UICONTROL Título]** para la configuración.

   Seleccione la configuración de IMS que creó durante [configuración de la cuenta de IMS](#create-ims-account-configuration).

   En el **[!UICONTROL URL de servicio]** , especifique la URL de su inquilino de Brand Portal (organización).

   ![Cuadro de diálogo Configuración de Brand Portal.](assets/create-cloud-service.png)

1. Haga clic en **[!UICONTROL Guardar y cerrar]**. Se crea la configuración de la nube.

   Su Experience Manager Assets as a [!DNL Cloud Service] ahora está configurada con el inquilino de Brand Portal.

Ahora puede probar la configuración comprobando el agente de distribución y publicando los recursos en Brand Portal.

**IP de salida de lista de permitidos en SPS si la previsualización segura está habilitada**
Si se usa Dynamic Media-Scene7 con [vista previa segura habilitada](#https://experienceleague.adobe.com/docs/dynamic-media-classic/using/upload-publish/testing-assets-making-them-public.html?lang=en) para una empresa), se aconseja que el administrador de la empresa de Scene7 [lista de permitidos de las IP de salida pública](#https://experienceleague.adobe.com/docs/dynamic-media-classic/using/upload-publish/testing-assets-making-them-public.html?lang=en#testing-the-secure-testing-service) para las regiones respectivas mediante la IU de Flash de SPS (Scene7 Publishing System).
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
* [Publish assets from Brand Portal to AEM Assets](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/asset-sourcing-in-brand-portal/brand-portal-asset-sourcing.html) - Asset Sourcing in Brand Portal
* [Publish presets, schemas, and facets to Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/publish/publish-schema-search-facets-presets.html)
* [Publish tags to Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/publish/brand-portal-publish-tags.html)

See [Brand Portal documentation](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/home.html) for more information.

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
