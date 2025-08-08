---
description: Obtenga información sobre cómo crear una configuración de almacenamiento de Azure Blob en AEM Forms y utilizarla en su Forms adaptable para lograr un almacenamiento de datos eficiente.
keywords: Integración de Azure Blob Storage con AEM Forms, envío de datos al almacenamiento de Azure, creación de la configuración de Azure Storage en AEM Forms, uso del almacenamiento de Azure Blob en la acción de envío de formularios adaptables
feature: Adaptive Forms, Foundation Components, Edge Delivery Services, Core Components
exl-id: 0c9f8f85-c4e9-4c79-bd0b-abdcac99a2d4
title: ¿Cómo configurar una acción de envío para un formulario adaptable?
role: User, Developer
source-git-commit: 1be7bafc1d93a65a81eeb2f7e86cac33cde7aa35
workflow-type: tm+mt
source-wordcount: '828'
ht-degree: 65%

---

# Envío de un formulario adaptable a Adobe Blob Storage

La acción de envío **[!UICONTROL Enviar al almacenamiento de Azure Blob]** conecta un formulario adaptable con un portal de Microsoft® Azure. Puede enviar los datos del formulario, archivos, archivos adjuntos o el documento de registro a los contenedores de almacenamiento de Azure conectados. 

AEM as a Cloud Service ofrece varias acciones de envío predeterminadas para gestionar los envíos de formularios. Puede obtener más información sobre estas opciones en el artículo [Acción de envío del formulario adaptable](/help/forms/aem-forms-submit-action.md).

## Ventajas

Algunas de las ventajas de la integración de Azure Blob Storage con AEM Forms son:

* Ayuda a simplificar el proceso de envío de datos de formulario adaptable, archivos, archivos adjuntos y documentos de registro a los contenedores de almacenamiento de Azure.
* Utiliza Azure Blob Storage para el almacenamiento centralizado y organizado de los envíos de formularios adaptables.

## Conecta AEM Forms al almacenamiento de Microsoft® Azure Blob

Para usar el almacenamiento de Azure Blob en la acción de envío de formularios adaptables:

1. [Crear un contenedor de almacenamiento de Azure Blob](#create-a-azure-blob-storage-container-create-azure-configuration): conecta AEM Forms a los contenedores de almacenamiento de Azure.
2. [Usar la configuración de almacenamiento de Azure en un formulario adaptable ](#use-azure-storage-configuration-in-an-adaptive-form-use-azure-storage-configuartion-in-af): conecta su formulario adaptable a los contenedores de almacenamiento de Azure configurados.

### Crear un contenedor de almacenamiento de Azure Blob {#create-azure-configuration}

Para conectar AEM Forms a los contenedores de almacenamiento de Azure:

1. Vaya a su instancia de **Autor de AEM Forms** > **[!UICONTROL Herramientas]** > **[!UICONTROL Servicios de nube]** >  **[!UICONTROL Almacenamiento de Azure]**.
1. Una vez seleccionado el **[!UICONTROL Almacenamiento de Azure]**, se le redirigirá a **[!UICONTROL Explorador de almacenamiento de Azure]**.
1. Seleccione un **Contenedor de configuración** La configuración se almacena en el contenedor de configuración seleccionado.
1. Haga clic en **[!UICONTROL Crear]**. Aparecerá el asistente Crear configuración de almacenamiento de Azure.

   ![Configuración de almacenamiento de Azure](/help/forms/assets/azure-storage-configuration.png)

1. Especifique el **[!UICONTROL Título]**, **[!UICONTROL Cuenta de almacenamiento de Azure]** y **[!UICONTROL Clave de acceso de Azure]**.

   * Puede recuperar el nombre de `Azure Storage Account` y la `Azure Access key` desde las cuentas de almacenamiento en el portal de Microsoft® Azure.
<!--

    >[!NOTE]
    >
    > The URL for **[!UICONTROL Azure Blob Endpoint]** is automatically appended to the textbox when a value is entered for **[!UICONTROL Azure Storage Account]**. You can update the Azure Blob End Point URL with your custom domain. Steps to update URL for **[!UICONTROL Azure Blob End Point]**:
    > 1. [Enable the AEM Advance Networking VPN support](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/networking/advanced-networking.html?lang=es)
    > 1. [Enable dedicated egress IP link](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/networking/advanced-networking.html?lang=es)
    > 1. [Map custom domain to azure blob storage](https://learn.microsoft.com/en-us/azure/storage/blobs/storage-custom-domain-name?tabs=azure-portal)
-->

1. Haga clic en **[!UICONTROL Guardar]**.

Ahora puede utilizar esta configuración del contenedor de almacenamiento de Azure para la acción de envío en un formulario adaptable.

### Uso de la configuración de almacenamiento de Azure en un formulario adaptable {#use-azure-storage-configuartion-in-af}

Puede utilizar la configuración del contenedor de almacenamiento de Azure creada en un formulario adaptable para guardar datos o el documento de registro generado en el contenedor de almacenamiento de Azure.

>[!NOTE]
>
> * Seleccione el mismo [!UICONTROL Contenedor de configuración] para un formulario adaptable, donde ha creado su almacenamiento de OneDrive.
> * Si no se selecciona el [!UICONTROL Contenedor de configuración], a continuación, las carpetas [!UICONTROL Configuración de almacenamiento] globales aparecen en la ventana de propiedades de la acción de envío.

>[!BEGINTABS]

>[!TAB Componente Base]

Realice los siguientes pasos para utilizar la configuración del contenedor de almacenamiento de Azure en un formulario adaptable basado en componentes de base como:

1. Abra el formulario adaptable para editarlo y vaya a la sección **[!UICONTROL Envío]** de las propiedades del contenedor del formulario adaptable.
1. En la lista desplegable **[!UICONTROL Enviar acción]**, seleccione **[!UICONTROL Enviar a Azure Blob Storage]**.

   ![GIF de almacenamiento de blob de Azure](/help/forms/assets/submit-to-azure-blob-fc.png){width=50%,height=50%}

   También puede guardar el documento de registro (DoR) en Azure Blob Storage.

1. Seleccione la **[!UICONTROL Configuración de almacenamiento]**, donde desee guardar los datos.
1. Haga clic en **[!UICONTROL Guardar]** para guardar la configuración de envío.

Al enviar el formulario, los datos se guardan en la configuración especificada del contenedor de almacenamiento de Azure.
La estructura de carpetas para guardar datos es `/configuration_container/form_name/year/month/date/submission_id/data`.

>[!TAB Componente principal]

Realice los siguientes pasos para utilizar la configuración del contenedor de almacenamiento de Azure en un formulario adaptable basado en componentes principales como:

1. Abra el Explorador de contenido y seleccione el componente **[!UICONTROL Contenedor de guía]** del formulario adaptable.
1. Haga clic en el icono de propiedades del contenedor de guía ![Propiedades de guía](/help/forms/assets/configure-icon.svg). Se abre el cuadro de diálogo Contenedor de formulario adaptable.
1. Haga clic en la pestaña **[!UICONTROL Envío]**.
1. En la lista desplegable **[!UICONTROL Enviar acción]**, seleccione **[!UICONTROL Enviar a Azure Blob Storage]**.

   ![GIF de almacenamiento de Azure Blob](/help/forms/assets/azure-submit-video.gif)

   También puede guardar el documento de registro (DoR) en Azure Blob Storage.

1. Seleccione la **[!UICONTROL Configuración de almacenamiento]**, donde desee guardar los datos.
1. Haga clic en **[!UICONTROL Guardar]** para guardar la configuración de envío.

Al enviar el formulario, los datos se guardan en la configuración especificada del contenedor de almacenamiento de Azure.
La estructura de carpetas para guardar datos es `/configuration_container/form_name/year/month/date/submission_id/data`.

>[!TAB Editor universal]

Siga estos pasos para utilizar la configuración del contenedor de almacenamiento de Azure en un formulario adaptable creado en el Editor universal:

1. Abra el formulario adaptable para editarlo.
1. Haga clic en la extensión **Editar propiedades del formulario** en el editor.
Aparecerá el cuadro de diálogo **Propiedades del formulario**.

   >[!NOTE]
   >
   > * Si no ve el icono **Editar propiedades de formulario** en la interfaz de Universal Editor, habilite la extensión **Editar propiedades de formulario** en Extension Manager.
   > * Consulte el artículo [Aspectos destacados de las funciones de Extension Manager](https://developer.adobe.com/uix/docs/extension-manager/feature-highlights/#enablingdisabling-extensions) para obtener información sobre cómo habilitar o deshabilitar extensiones en el editor universal.

1. Haga clic en la pestaña **Envío** y seleccione la acción de envío **[!UICONTROL Enviar al almacenamiento del blob de Azure]**.
   ![Almacenamiento de blob de Azure](/help/forms/assets/azure-blob-storage-ue.png)

   Si selecciona **Guardar archivos adjuntos con el nombre original**, los archivos adjuntos se almacenarán en la carpeta utilizando sus nombres de archivo originales. También puede guardar el documento de registro (DoR) en Azure Blob Storage.

1. Seleccione la **[!UICONTROL Configuración de almacenamiento]**, donde desee guardar los datos.
1. Haga clic en **[!UICONTROL Guardar y cerrar]** para guardar la configuración de envío.

Al enviar el formulario, los datos se guardan en la configuración especificada del contenedor de almacenamiento de Azure.
La estructura de carpetas para guardar datos es `/configuration_container/form_name/year/month/date/submission_id/data`.

>[!ENDTABS]

## Artículos relacionados

{{af-submit-action}}
