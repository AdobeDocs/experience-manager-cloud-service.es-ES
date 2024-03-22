---
Title: How to send data to a SharePoint storage on submission of an Adaptive Form?
Description: Learn how to send data from your Adaptive Form to a SharePoint storage like a SharePoint list or Document library when you submit the form.
keywords: ¿Cómo conectar la lista de SharePoint para un formulario adaptable?, Cómo conectar la biblioteca de documentos de SharePoint para un formulario adaptable, Enviar a SharePoint, Crear una configuración de la biblioteca de documentos de SharePoint, Utilizar la acción de envío Enviar a SharePoint en un formulario adaptable, Conectar un formulario adaptable a la lista de Microsoft&reg; SharePoint.
feature: Adaptive Forms, Core Components
source-git-commit: 8784c0bcd05eeae41a472faa5ecad03cbdd8a9b6
workflow-type: ht
source-wordcount: '1037'
ht-degree: 100%

---


# Conectar un formulario adaptable a la lista de Microsoft® SharePoint

La acción de envío **[!UICONTROL Enviar a SharePoint]** le permite conectar sin problemas un formulario adaptable con un almacenamiento de Microsoft® SharePoint. Envía los datos del formulario al almacenamiento de SharePoint que elija después de enviar el formulario.

AEM as a Cloud Service ofrece varias acciones de envío predeterminadas para gestionar los envíos de formularios. Puede obtener más información sobre estas opciones en el artículo [Acción de envío del formulario adaptable](/help/forms/configure-submit-actions-core-components.md).

## Ventajas

Algunas de las ventajas de enviar datos de un formulario adaptable al almacenamiento de SharePoint son las siguientes:

* Facilita el envío directo de datos de formulario a SharePoint, lo que proporciona una ubicación centralizada para almacenar y administrar la información.
* Al aplicar las funciones de control de acceso y permisos de SharePoint, se garantiza que solo las personas autorizadas puedan ver o modificar los datos enviados.

Mediante **[!UICONTROL Enviar a SharePoint]**, puede hacer lo siguiente:

* [Conectar un formulario adaptable a la biblioteca de documentos de SharePoint](#connect-af-sharepoint-doc-library)
* [Conectar un formulario adaptable a la lista de SharePoint](#connect-af-sharepoint-list)

## Conectar un formulario adaptable a la biblioteca de documentos de SharePoint {#connect-af-sharepoint-doc-library}

Para usar la acción de envío **[!UICONTROL Enviar a Biblioteca de documentos de SharePoint]** en un formulario adaptable:

1. [Crear una configuración de Biblioteca de documentos de SharePoint](#create-a-sharepoint-configuration-create-sharepoint-configuration): conecta AEM Forms a su almacenamiento de Microsoft® SharePoint.
2. [Utilice la acción de envío Enviar a SharePoint en un formulario adaptable](#use-sharepoint-configuartion-in-af): conecta el formulario adaptable al Microsoft® SharePoint configurado.

### Crear configuración de biblioteca de documentos de SharePoint {#create-sharepoint-configuration}

Para conectar AEM Forms a su almacenamiento de la biblioteca de documentos de Microsoft® Sharepoint:

1. Vaya a su instancia de **AEM Forms Author** > **[!UICONTROL Herramientas]** > **[!UICONTROL Cloud Services]** >  **[!UICONTROL Microsoft® SharePoint]**.
1. Una vez seleccionada la variable **[!UICONTROL Microsoft® SharePoint]**, se le redirigirá a **[!UICONTROL Explorador SharePoint]**.
1. Seleccione un **Contenedor de configuración**. La configuración se almacena en el contenedor de configuración seleccionado.
1. Haga clic en **[!UICONTROL Crear]** > **[!UICONTROL Biblioteca de documentos de SharePoint]** en la lista desplegable. Aparecerá el asistente de configuración de SharePoint.

   ![Configuración de SharePoint](/help/forms/assets/sharepoint_configuration.png)
1. Especifique el **[!UICONTROL Título]**, **[!UICONTROL ID de cliente]**, **[!UICONTROL Secreto del cliente]** y **[!UICONTROL URL de OAuth]**. Para obtener información sobre cómo recuperar el ID de cliente, el secreto de cliente o el ID de inquilino para la URL de OAuth, consulte [Documentación de Microsoft®](https://learn.microsoft.com/es-es/graph/auth-register-app-v2).
   * Puede recuperar la variable `Client ID` y `Client Secret` de su aplicación desde el portal de Microsoft® Azure.
   * En el portal de Microsoft® Azure, añada el URI de redireccionamiento como `https://[author-instance]/libs/cq/sharepoint/content/configurations/wizard.html`. Reemplace `[author-instance]` por la URL de su instancia de autor.
   * Añada los permisos de API `offline_access` y `Sites.Manage.All` para proporcionar permisos de lectura y escritura.
   * Use la URL de OAuth: `https://login.microsoftonline.com/tenant-id/oauth2/v2.0/authorize`. Reemplace `<tenant-id>` por el `tenant-id` de su aplicación desde el portal de Microsoft® Azure.

   >[!NOTE]
   >
   > El campo **secreto de cliente** es obligatorio u opcional dependiendo de su configuración de la aplicación de Azure Active Directory. Si la aplicación está configurada para utilizar un secreto de cliente, es obligatorio proporcionar dicho secreto.

1. Haga clic en **[!UICONTROL Conectar]**. Si la conexión se realiza correctamente, aparece el mensaje `Connection Successful`.

1. Ahora, seleccione **Sitio de SharePoint** > **Biblioteca de documentos** > **Carpeta de SharePoint**, para guardar los datos.

   >[!NOTE]
   >
   >* De forma predeterminada, `forms-ootb-storage-adaptive-forms-submission` está presente en el sitio de SharePoint seleccionado.
   >* Cree una carpeta como `forms-ootb-storage-adaptive-forms-submission` si no está presente en la biblioteca `Documents` del sitio de SharePoint seleccionado haciendo clic en **Crear carpeta**.

Ahora puede utilizar esta configuración de SharePoint Sites para la acción de envío en un formulario adaptable.

### Uso de la configuración de la biblioteca de documentos de SharePoint en un formulario adaptable {#use-sharepoint-configuartion-in-af}

Puede utilizar la configuración de la biblioteca de documentos de SharePoint creada en un formulario adaptable para guardar datos o el documento de registro generado en una carpeta de SharePoint. Siga estos pasos para usar una configuración de almacenamiento de la biblioteca de documentos de SharePoint en un formulario adaptable como el siguiente:

1. Crear un [Formulario adaptable](/help/forms/creating-adaptive-form-core-components.md).

   >[!NOTE]
   >
   > * Seleccione el mismo [!UICONTROL Contenedor de configuración] para un formulario adaptable, donde haya creado su almacenamiento de la biblioteca de documentos de SharePoint.
   > * Si no se selecciona ningún [!UICONTROL Contenedor de configuración], a continuación, las carpetas globales [!UICONTROL Configuración de almacenamiento] aparecen en la ventana de propiedades de la acción de envío.

1. Seleccionar **Acción de envío** como **[!UICONTROL Enviar a SharePoint]**.
   ![GIF de Sharepoint](/help/forms/assets/sharedrive-video.gif)
1. Seleccione la **[!UICONTROL Configuración de almacenamiento]**, donde desee guardar los datos.
1. Haga clic en **[!UICONTROL Guardar]** para guardar la configuración de envío.

Al enviar el formulario, los datos se guardan en el almacenamiento especificado de la biblioteca de documentos de Microsoft® SharePoint.
La estructura de carpetas para guardar datos es `/folder_name/form_name/year/month/date/submission_id/data`.

## Conectar un formulario adaptable a la lista de Microsoft® SharePoint {#connect-af-sharepoint-list}

>[!VIDEO](https://video.tv.adobe.com/v/3424820/connect-aem-adaptive-form-to-sharepointlist/?quality=12&learn=on)

Para usar la acción de envío [!UICONTROL Enviar a lista de SharePoint] en un formulario adaptable, haga lo siguiente:

1. [Crear una configuración de lista de SharePoint](#create-sharepoint-list-configuration): conecta AEM Forms a su almacenamiento de de lista de Sharepoint de Microsoft®.
1. [Utilice la acción de envío Enviar con un modelo de datos de formulario en un formulario adaptable](#use-submit-using-fdm): conecta el formulario adaptable a Microsoft® SharePoint configurado.

### Crear configuración de lista de SharePoint {#create-sharepoint-list-configuration}

Para conectar AEM Forms a su lista de Sharepoint de Microsoft®:

1. Vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Cloud Services]** >  **[!UICONTROL Microsoft® SharePoint]**.
1. Seleccione un **Contenedor de configuración**. La configuración se almacena en el contenedor de configuración seleccionado.
1. Haga clic en **[!UICONTROL Crear]** > **[!UICONTROL Lista de SharePoint]** en la lista desplegable. Aparecerá el asistente de configuración de SharePoint.
1. Especifique el **[!UICONTROL Título]**, **[!UICONTROL ID de cliente]**, **[!UICONTROL Secreto del cliente]** y **[!UICONTROL URL de OAuth]**. Para obtener información sobre cómo recuperar el ID de cliente, el secreto de cliente o el ID de inquilino para la URL de OAuth, consulte [Documentación de Microsoft®](https://learn.microsoft.com/es-es/graph/auth-register-app-v2).
   * Puede recuperar la variable `Client ID` y `Client Secret` de su aplicación desde el portal de Microsoft® Azure.
   * En el portal de Microsoft® Azure, añada el URI de redireccionamiento como `https://[author-instance]/libs/cq/sharepointlist/content/configurations/wizard.html`. Reemplace `[author-instance]` por la URL de su instancia de autor.
   * Adición de los permisos de API `offline_access` y `Sites.Manage.All` en la pestaña **Microsoft® Graph** para proporcionar permisos de lectura y escritura. Añadir permiso de `AllSites.Manage` en la pestaña **SharePoint** para interactuar de forma remota con los datos de SharePoint.
   * Use la URL de OAuth: `https://login.microsoftonline.com/tenant-id/oauth2/v2.0/authorize`. Reemplace `<tenant-id>` por el `tenant-id` de su aplicación desde el portal de Microsoft® Azure.

     >[!NOTE]
     >
     > El campo **secreto de cliente** es obligatorio u opcional dependiendo de su configuración de la aplicación de Azure Active Directory. Si la aplicación está configurada para utilizar un secreto de cliente, es obligatorio proporcionar dicho secreto.

1. Haga clic en **[!UICONTROL Conectar]**. Si la conexión se realiza correctamente, aparece el mensaje `Connection Successful`.
1. Seleccionar **[!UICONTROL Sitio de SharePoint]** y **[!UICONTROL Lista de SharePoint]** en la lista desplegable.
1. Seleccione **[!UICONTROL Crear]** para crear la configuración de nube para la lista de SharePoint de Microsoft®.


### Usar la acción de envío Enviar con el modelo de datos de formulario en un formulario adaptable {#use-submit-using-fdm}

Puede utilizar la configuración de lista de SharePoint creada en un formulario adaptable para guardar datos o el documento de registro generado en una lista de SharePoint. Siga estos pasos para usar una lista de SharePoint en un formulario adaptable como:

1. [Crear un modelo de datos de formulario con Microsoft](/help/forms/create-form-data-models.md)
1. [Configurar el modelo de datos de formulario para recuperar y enviar datos](/help/forms/work-with-form-data-model.md#configure-services)
1. [Crear un formulario adaptable](/help/forms/creating-adaptive-form-core-components.md)
1. [Configurar la acción de envío mediante un modelo de datos de formulario](/help/forms/using-form-data-model.md)

Al enviar el formulario, los datos se guardan en el almacenamiento de lista de Sharepoint de Microsoft® especificado.

>[!NOTE]
>
> En la lista de Microsoft® SharePoint, no se admiten los siguientes tipos de columnas:
> * columna de imagen
> * columna de metadatos
> * columna de persona
> * columna de datos externos

## Artículos relacionados

{{af-submit-action}}