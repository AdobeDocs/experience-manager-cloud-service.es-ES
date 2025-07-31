---
Title: How to send data to a SharePoint List storage on submission of an Adaptive Form?
Description: Learn how to send data from your Adaptive Form to a SharePoint storage like a SharePoint list when you submit the form.
keywords: ¿Cómo conectar la lista de SharePoint para un formulario adaptable?, Enviar a SharePoint, Crear una configuración de lista de SharePoint, Utilizar la acción de envío Enviar a SharePoint en un formulario adaptable, Conectar un formulario adaptable a Microsoft&reg; Lista de SharePoint.
feature: Adaptive Forms, Core Components, Foundation Components, Edge Delivery Services
title: ¿Cómo configurar una acción de envío para un formulario adaptable?
role: User, Developer
exl-id: 9ac3e7be-c6fa-4dbc-9aba-b81741ba6c55
source-git-commit: 64edcfe1bf94638ae5d9510a5a6ac660cf1bcd0a
workflow-type: tm+mt
source-wordcount: '438'
ht-degree: 87%

---

# Conectar un formulario adaptable a la lista de Microsoft® SharePoint {#connect-af-sharepoint-list}

>[!VIDEO](https://video.tv.adobe.com/v/3424820/connect-aem-adaptive-form-to-sharepointlist/?quality=12&learn=on)

Para usar la acción de envío [!UICONTROL Enviar a lista de SharePoint] en un formulario adaptable, haga lo siguiente:

1. [Crear una configuración de lista de SharePoint](#1-create-a-sharepoint-list-configuration): conecta AEM Forms a su almacenamiento de de lista de Sharepoint de Microsoft®.
1. [Utilice la acción de envío Enviar con un modelo de datos de formulario (FDM) en un formulario adaptable](#2-use-the-submit-using-form-data-model-fdm-in-an-adaptive-form-use-submit-using-fdm): conecta el formulario adaptable a Microsoft® SharePoint configurado.

## &#x200B;1. Crear una configuración de lista de SharePoint

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


## &#x200B;2. Utilizar Enviar mediante el modelo de datos de formulario (FDM) en un formulario adaptable {#use-submit-using-fdm}

Puede utilizar la configuración de lista de SharePoint creada en un formulario adaptable para guardar datos o el documento de registro generado en una lista de SharePoint. Siga estos pasos para usar una lista de SharePoint en un formulario adaptable como:

1. [Cree un modelo de datos de formulario (FDM) con Microsoft](/help/forms/create-form-data-models.md)
1. [Configure el modelo de datos de formulario (FDM) para recuperar y enviar datos](/help/forms/work-with-form-data-model.md#configure-services)
1. [Creación de un formulario adaptable](/help/forms/creating-adaptive-form-core-components.md)
1. [Configure la acción de envío mediante un modelo de datos de formulario (FDM)](/help/forms/using-form-data-model.md)

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
