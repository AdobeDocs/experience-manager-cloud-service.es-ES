---
title: Envío de un formulario adaptable a Microsoft&reg; OneDrive
description: Explore el proceso optimizado de conexión de AEM Forms con Microsoft&reg; OneDrive mediante la acción de envío Enviar a OneDrive. Conozca la guía paso a paso para configurar OneDrive y las acciones de envío para lograr un almacenamiento y una recuperación de datos eficientes.
keywords: Integración de AEM Forms OneDrive, Conexión a Microsoft AEM OneDrive, Configuración de OneDrive con formularios de AEM
feature: Adaptive Forms, Core Components, Foundation Components, Edge Delivery Services
exl-id: dbfa4094-1b92-4a7c-a799-f66973d27054
role: User, Developer
source-git-commit: 44a8d5d5fdd2919d6d170638c7b5819c898dcefe
workflow-type: ht
source-wordcount: '921'
ht-degree: 100%

---

# Envío de un formulario adaptable a Microsoft® OneDrive

La acción de envío **[!UICONTROL Enviar a OneDrive]** conecta un formulario adaptable con un Microsoft® OneDrive. Puede enviar los datos del formulario, archivos, archivos adjuntos o el documento de registro al almacenamiento de Microsoft® OneDrive conectado.

AEM as a Cloud Service ofrece varias acciones de envío predeterminadas para gestionar los envíos de formularios. Puede obtener más información sobre estas opciones en el artículo [Acción de envío del formulario adaptable](/help/forms/aem-forms-submit-action.md).

## Ventajas

Algunas de las ventajas de la integración perfecta de AEM Forms y Microsoft® OneDrive son:

* La accesibilidad entre dispositivos de OneDrive garantiza que los datos de formulario almacenados estén fácilmente disponibles en diferentes plataformas. Se puede acceder a los datos enviados, archivos adjuntos y documentos enviados desde equipos de escritorio, portátiles, tabletas y dispositivos móviles, lo que mejora la accesibilidad y la flexibilidad.
* La integración de OneDrive con AEM Forms proporciona una solución fiable y escalable para un almacenamiento de datos eficiente. Todos los envíos de formularios adaptables, como archivos, archivos adjuntos y el documento de registro, se pueden guardar cómodamente en OneDrive, lo que garantiza que los datos estén organizados y sean accesibles.

## Conexión de OneDrive a un formulario adaptable

>[!VIDEO](https://video.tv.adobe.com/v/3424864/connect-aem-adaptive-form-to-onedrive/?quality=12&learn=on)

<span> Este vídeo solo es aplicable a los componentes principales. Para componentes del editor universal o de base, consulte el artículo.</span>

Para configurar OneDrive para el envío de AEM Forms, realice los siguientes pasos:

1. [Crear una configuración de OneDrive](#create-a-onedrive-configuration-create-onedrive-configuration): conecta AEM Forms al almacenamiento de Microsoft® OneDrive.
2. [Utilice la acción de envío Enviar a OneDrive en un formulario adaptable](#use-onedrive-configuration-in-an-adaptive-form-use-onedrive-configuartion-in-af): conecta el formulario adaptable a Microsoft® OneDrive configurado.

### Crear configuración de OneDrive {#create-onedrice-configuration}

Para conectar AEM Forms al almacenamiento de Microsoft® OneDrive:

1. Vaya a su instancia de **Autor de AEM Forms** > **[!UICONTROL Herramientas]** > **[!UICONTROL Servicios de nube]** >  **[!UICONTROL Microsoft® OneDrive]**.
1. Una vez seleccionada la variable **[!UICONTROL Microsoft® OneDrive]**, se le redirigirá a **[!UICONTROL Explorador de OneDrive]**.
1. Seleccione un **Contenedor de configuración** La configuración se almacena en el contenedor de configuración seleccionado.
1. Haga clic en **[!UICONTROL Crear]**. Aparecerá el asistente de configuración de OneDrive.

   ![Pantalla de configuración de OneDrive](/help/forms/assets/onedrive-configuration.png)

1. Especifique el **[!UICONTROL Título]**, **[!UICONTROL ID de cliente]**, **[!UICONTROL Secreto del cliente]** y **[!UICONTROL URL de OAuth]**. Para obtener información sobre cómo recuperar el ID de cliente, el secreto de cliente o el ID de inquilino para la URL de OAuth, consulte [Documentación de Microsoft®](https://learn.microsoft.com/es-es/graph/auth-register-app-v2).
   * Puede recuperar la variable `Client ID` y `Client Secret` de su aplicación desde el portal de Microsoft® Azure.
   * En el portal de Microsoft® Azure, añada el URI de redireccionamiento como `https://[author-instance]/libs/cq/onedrive/content/configurations/wizard.html`. Reemplace `[author-instance]` por la URL de su instancia de autor.
   * Añada los permisos de API `offline_access` y `Files.ReadWrite.All` para proporcionar permisos de lectura y escritura.
   * Use la URL de OAuth: `https://login.microsoftonline.com/tenant-id/oauth2/v2.0/authorize`. Reemplace `<tenant-id>` por el `tenant-id` de su aplicación desde el portal de Microsoft® Azure.

   >[!NOTE]
   >
   > El campo **secreto de cliente** es obligatorio u opcional dependiendo de su configuración de la aplicación de Azure Active Directory. Si la aplicación está configurada para utilizar un secreto de cliente, es obligatorio proporcionar dicho secreto.

1. Haga clic en **[!UICONTROL Conectar]**. Si la conexión se realiza correctamente, aparece el mensaje `Connection Successful`.

1. Ahora, seleccione **[!UICONTROL Contenedor de OneDrive]** > **[Carpeta de OneDrive]** para guardar los datos.

   >[!NOTE]
   >
   >* De forma predeterminada, `forms-ootb-storage-adaptive-forms-submission` está presente en el contenedor de OneDrive.
   > * Cree una carpeta como `forms-ootb-storage-adaptive-forms-submission`, si no está presente haciendo clic en **Crear carpeta**.

Ahora puede usar esta configuración de almacenamiento de OneDrive para la acción de envío en un formulario adaptable.

### Usar la configuración de OneDrive en un formulario adaptable {#use-onedrive-configuartion-in-af}

Puede usar la configuración de almacenamiento de OneDrive creada en un formulario adaptable para guardar datos o el documento de registro generado en una carpeta de OneDrive. 

>[!NOTE]
>
> * Seleccione el mismo [!UICONTROL Contenedor de configuración] para un formulario adaptable, donde ha creado su almacenamiento de OneDrive.
> * Si no se selecciona el [!UICONTROL Contenedor de configuración], a continuación, las carpetas [!UICONTROL Configuración de almacenamiento] globales aparecen en la ventana de propiedades de la acción de envío.

>[!BEGINTABS]

>[!TAB Componente base]

Siga estos pasos para usar la configuración de almacenamiento de OneDrive en un componente de base como:

1. Abra el formulario adaptable para editarlo y vaya a la sección **[!UICONTROL Envío]** de las propiedades del contenedor del formulario adaptable.
1. En la lista desplegable **[!UICONTROL Acción de envío]**, seleccione la opción **[!UICONTROL Enviar a OneDrive]**.
   ![OneDrive GIF](/help/forms/assets/wubmit-to-onedrive-fc.png){width=50%,height=50%}
También puede guardar el documento de registro (DoR) en OneDrive.
1. Seleccione la **[!UICONTROL Configuración de almacenamiento]**, donde desee guardar los datos.
1. Haga clic en **[!UICONTROL Guardar]** para guardar la configuración de envío.

Al enviar el formulario, los datos se guardan en el almacenamiento de Microsoft® OneDrive especificado.
La estructura de carpetas para guardar datos es `/folder_name/form_name/year/month/date/submission_id/data`.

>[!TAB Componente principal]

Siga estos pasos para usar la configuración de almacenamiento de OneDrive en un formulario adaptable basado en un componente principal como:

1. Abra el Explorador de contenido y seleccione el componente **[!UICONTROL Contenedor de guía]** del formulario adaptable.
1. Haga clic en el icono de propiedades del contenedor de guía ![Propiedades de guía](/help/forms/assets/configure-icon.svg). Se abre el cuadro de diálogo Contenedor de formulario adaptable.
1. Haga clic en la pestaña **[!UICONTROL Envío]**.
1. En la lista desplegable **[!UICONTROL Acción de envío]**, seleccione la opción **[!UICONTROL Enviar a OneDrive]**.
   ![OneDrive GIF](/help/forms/assets/onedrive-video.gif)
También puede guardar el documento de registro (DoR) en OneDrive.
1. Seleccione la **[!UICONTROL Configuración de almacenamiento]**, donde desee guardar los datos.
1. Haga clic en **[!UICONTROL Guardar]** para guardar la configuración de envío.

>[!TAB Editor universal]

Siga estos pasos para usar la configuración de almacenamiento de OneDrive en un formulario adaptable creado en el editor universal:

1. Abra el formulario adaptable para editarlo.
1. Haga clic en la extensión **Editar propiedades del formulario** en el editor.
Aparece el cuadro de diálogo **Propiedades del formulario**.

   >[!NOTE]
   >
   > * Si no ve el icono **Editar propiedades del formulario** en la interfaz del edito universal, habilite la extensión **Editar propiedades del formulario** en Extension Manager.
   > * Consulte el artículo [Características destacadas de las funciones de Extension Manager](https://developer.adobe.com/uix/docs/extension-manager/feature-highlights/#enablingdisabling-extensions) para obtener información sobre cómo habilitar o deshabilitar las extensiones del editor universal.
1. Haga clic en la pestaña **Envío** y seleccione **[!UICONTROL Enviar a OneDrive]**.
   ![GIF de OneDrive](/help/forms/assets/submit-to-onedrive-ue.png)
Si selecciona **Guardar archivos adjuntos con el nombre original**, los archivos adjuntos se almacenarán en la carpeta utilizando sus nombres de archivo originales. También puede guardar el documento de registro (DoR) en Azure Blob Storage.
1. Seleccione la **[!UICONTROL Configuración de almacenamiento]**, donde desee guardar los datos.
1. Haga clic en **[!UICONTROL Guardar y cerrar]**.

>[!ENDTABS]

## Artículos relacionados

{{af-submit-action}}
