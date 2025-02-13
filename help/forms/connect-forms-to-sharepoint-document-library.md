---
Title: How to integrate Adaptive Form to a SharePoint Document Library?
Description: This article explains how to send data from your Adaptive Form to a SharePoint  Document library when you submit the form.
keywords: Cómo conectar la biblioteca de documentos de SharePoint para un formulario adaptable, Enviar a SharePoint, Crear una configuración de biblioteca de documentos de SharePoint, Utilizar la acción de envío Enviar a SharePoint en un formulario adaptable, Biblioteca de documentos de SharePoint del modelo de datos de AEM Forms, Biblioteca de documentos de SharePoint del modelo de datos de Forms, Integrar el modelo de datos de Forms a la biblioteca de documentos de SharePoint
feature: Adaptive Forms, Core Components
role: User, Developer
source-git-commit: 55e8f142e242f5f4010653a155a241ffcf801470
workflow-type: tm+mt
source-wordcount: '604'
ht-degree: 82%

---


# Conectar un formulario adaptable a la biblioteca de documentos de Microsoft® SharePoint {#connect-af-sharepoint-doc-library}

>[!VIDEO](https://video.tv.adobe.com/v/3444368/formautomation-productivitytools-adaptiveforms--sharepointintegration-documentlibrary/?quality=12&learn=on)

Para usar la acción de envío **[!UICONTROL Enviar a Biblioteca de documentos de SharePoint]** en un formulario adaptable:

1. [Crear una configuración de Biblioteca de documentos de SharePoint](#1-create-a-sharepoint-document-library-configuration): conecta AEM Forms a su almacenamiento de Microsoft® SharePoint.
2. [Utilice la acción de envío Enviar a SharePoint en un formulario adaptable](#2-use-sharepoint-document-library-configuration-in-an-adaptive-form): conecta el formulario adaptable al Microsoft® SharePoint configurado.

## 1. Cree una configuración de SharePoint Document Library

Para conectar AEM Forms a su almacenamiento de la biblioteca de documentos de Microsoft® Sharepoint:

1. Vaya a su instancia de **AEM Forms Author** > **[!UICONTROL Herramientas]** > **[!UICONTROL Cloud Services]** >  **[!UICONTROL Microsoft® SharePoint]**.
1. Una vez seleccionada la variable **[!UICONTROL Microsoft® SharePoint]**, se le redirigirá a **[!UICONTROL Explorador SharePoint]**.
1. Seleccione un **Contenedor de configuración**. La configuración se almacena en el contenedor de configuración seleccionado.
1. Haga clic en **[!UICONTROL Crear]** > **[!UICONTROL Biblioteca de documentos de SharePoint]** en la lista desplegable. Aparecerá el asistente de configuración de SharePoint.

   ![Configuración de SharePoint](/help/forms/assets/sharepoint_configuration.png)

1. Especifique el **[!UICONTROL Título]**, **[!UICONTROL ID de cliente]**, **[!UICONTROL Secreto del cliente]** y **[!UICONTROL URL de OAuth]**. Para obtener información sobre cómo recuperar el ID de cliente, el secreto de cliente o el ID de inquilino para la URL de OAuth, consulte [Documentación de Microsoft®](https://learn.microsoft.com/es-es/graph/auth-register-app-v2).
   * Puede recuperar la variable `Client ID` y `Client Secret` de su aplicación desde el portal de Microsoft® Azure.
   * En el portal de Microsoft® Azure, añada el URI de redireccionamiento como `https://[author-instance]/libs/cq/sharepoint/content/configurations/wizard.html`. Reemplace `[author-instance]` por la URL de su instancia de autor.
   * Añada los permisos de API `offline_access` y `Sites.Manage.All` para proporcionar permisos de lectura y escritura. `Sites.Manage.All` es un ámbito de permisos en la API de Graph de Microsoft que concede a una aplicación la posibilidad de administrar todos los aspectos de los sitios de SharePoint, como eliminar o modificar sitios.

     >[!NOTE]
     >
     > También puede [configurar los sitios de SharePoint con acceso limitado](/help/forms/configure-sharepoint-site-limited-access.md) mediante el ámbito de permisos `Sites.Selected` en la API de Microsoft Graph. `Sites.Selected` es un ámbito de permisos en la API de Graph de Microsoft que permite un acceso más granular y restringido a los sitios de SharePoint.

   * Use la URL de OAuth: `https://login.microsoftonline.com/tenant-id/oauth2/v2.0/authorize`. Reemplace `<tenant-id>` por el `tenant-id` de su aplicación desde el portal de Microsoft® Azure.

     >[!NOTE]
     >
     > El campo **secreto de cliente** es obligatorio u opcional dependiendo de su configuración de la aplicación de Azure Active Directory. Si la aplicación está configurada para utilizar un secreto de cliente, es obligatorio proporcionar dicho secreto.

1. Ámbito de permiso `offline_access Sites.Selected` en la API de Graph de Microsoft que permite un acceso más granular y restringido a los sitios de SharePoint. Ámbito de permiso `offline_access Sites.Manage.All` en la API de Graph de Microsoft que permite el acceso completo a los sitios de SharePoint.
1. Haga clic en **[!UICONTROL Conectar]**. Si la conexión se realiza correctamente, aparece el mensaje `Connection Successful`.

1. Ahora, seleccione **Sitio de SharePoint** > **Biblioteca de documentos** > **Carpeta de SharePoint**, para guardar los datos.

   >[!NOTE]
   >
   >* De forma predeterminada, `forms-ootb-storage-adaptive-forms-submission` está presente en el sitio de SharePoint seleccionado.
   >* Cree una carpeta como `forms-ootb-storage-adaptive-forms-submission` si no está presente en la biblioteca `Documents` del sitio de SharePoint seleccionado haciendo clic en **Crear carpeta**.

Ahora puede utilizar esta configuración de SharePoint Sites para la acción de envío en un formulario adaptable.

### 2. Utilizar la configuración de la biblioteca de documentos de SharePoint en un formulario adaptable

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

## Artículos relacionados

{{af-submit-action}}