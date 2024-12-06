---
title: Descarga de recursos desde Content Hub
description: Obtenga información sobre cómo descargar recursos desde el portal de Content Hub
role: User
exl-id: 96d4ffba-4e3e-4496-9da2-6eb36be8331f
source-git-commit: 28424cb184d0378669498c78e571961227f6539a
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Descarga de recursos desde Content Hub {#download-assets}

| [Prácticas recomendadas de búsqueda](/help/assets/search-best-practices.md) | [Prácticas recomendadas de metadatos](/help/assets/metadata-best-practices.md) | [Centro de contenido](/help/assets/product-overview.md) | [Dynamic Media con funciones de OpenAPI](/help/assets/dynamic-media-open-apis-overview.md) | [Documentación de desarrollador de AEM Assets](https://developer.adobe.com/experience-cloud/experience-manager-apis/) |
| ------------- | --------------------------- |---------|----|-----|

<!-- ![Download assets](assets/download-asset.jpg) -->
![Descarga de recursos](assets/download-asset-genstudio.jpeg)

>[!AVAILABILITY]
>
>La guía del centro de contenido ya está disponible en formato de PDF. Descargue la guía completa y utilice el Asistente de IA de Adobe Acrobat para responder sus consultas.
>
>[!BADGE Guía del centro de contenido en PDF]{type=Informative url="https://helpx.adobe.com/content/dam/help/en/experience-manager/aem-assets/content-hub.pdf"}

Content Hub le permite descargar y compartir sus recursos. La interfaz de usuario de Content Hub solo muestra los recursos aprobados. Estos recursos pueden incluir imágenes, vídeos o cualquier otro contenido digital. Content Hub mejora la accesibilidad y la adaptabilidad para una distribución eficaz de los recursos.

Puede descargar uno o varios recursos y sus representaciones disponibles mediante Content Hub.

## Descargar un recurso y sus representaciones {#download-asset-renditions}

Para descargar un recurso y sus representaciones, ejecute los siguientes pasos:

1. Haga clic en el recurso para ver sus propiedades.

1. Haga clic en ![descargar](/help/assets/assets/download-icon.svg) para iniciar el proceso de descarga. El panel Descargar enumera todas las representaciones de recursos disponibles (representaciones originales y otras).

   >[!NOTE]
   >
   Las representaciones se muestran únicamente si su visibilidad está habilitada mediante la interfaz de usuario de [Configuration](/help/assets/configure-content-hub-ui-options.md#renditions-content-hub).

1. Seleccione las representaciones y haga clic en **[!UICONTROL Descargar]**.

   ![Descargar representaciones de recursos individuales](/help/assets/assets/download-single-asset-renditions.png)


Si está descargando un recurso con licencia, seleccione **[!UICONTROL He leído y aceptado los términos y condiciones mencionados anteriormente]** y luego haga clic en **[!UICONTROL Descargar]**. También puede hacer clic en **[!UICONTROL términos y condiciones]** para ver la licencia del recurso. La vista previa de la licencia solo se muestra si el recurso se aprueba mediante el entorno de creación as a Cloud Service de Assets. Para obtener más información, consulte [Administración de recursos con licencia en Content Hub](/help/assets/manage-licensed-assets-on-content-hub.md).

## Descargar varios recursos y sus representaciones {#download-multiple-assets-renditions}

Para descargar varios recursos y sus representaciones, ejecute los siguientes pasos:

1. Seleccione los recursos y haga clic en ![descargar](/help/assets/assets/download-icon.svg) **[!UICONTROL Descargar]**. La pantalla [!UICONTROL Descargar recursos] muestra una lista de todos los recursos seleccionados.
1. Haga clic en **[!UICONTROL Descargar]** para seleccionar entre las distintas opciones de descarga para comenzar la descarga:

   * **Descargar [!UICONTROL originales]**: selecciona esta opción para descargar los recursos seleccionados en el formulario original.
   * **Descargar solo [!UICONTROL representaciones]**: seleccione esta opción para descargar todas las representaciones disponibles de los recursos, excepto los recursos originales.
   * **Descargar [!UICONTROL originales y todas las representaciones]**: seleccione esta opción para descargar tanto el original como las representaciones de los recursos seleccionados.

     ![Descargar varias representaciones](/help/assets/assets/download-multiple-renditions.png)

     >[!NOTE]
     >
     Las representaciones se muestran únicamente si su visibilidad está habilitada mediante la interfaz de usuario de [Configuration](/help/assets/configure-content-hub-ui-options.md#renditions-content-hub).

   Si alguno de los recursos seleccionados es un recurso con licencia, haga clic en la licencia del recurso en el panel izquierdo para ver su vista previa, lo que le permite seleccionar **[!UICONTROL He leído y aceptado los términos y condiciones mencionados anteriormente]** y, a continuación, haga clic en **[!UICONTROL Descargar]**. La vista previa de la licencia solo se muestra si el recurso se aprueba mediante el entorno de creación as a Cloud Service de Assets. Para obtener más información, consulte [Administración de recursos con licencia en Content Hub](/help/assets/manage-licensed-assets-on-content-hub.md).

   ![descargar-múltiples-licencias](/help/assets/assets/download-multiple-license.png)

<!--1. On the Content Hub homepage, select the asset and click **Download**. The **Download assets** dialog box displays a license or list of licenses associated with the selected assets in the left pane. 
1. Click a license in the left pane to see its PDF in the middle pane and the associated assets with it in the right pane. The license PDF preview is displayed only if the license is approved in your Assets as a Cloud Service environment. [Approve the license PDFs](/help/assets/approve-assets-content-hub.md) of the selected assets to see their previews.
1. Optional: Click ![remove-icon](/help/assets/assets/remove-icon.svg) to remove a license from the dialog box.
1. Select **I have read and accept all the terms and conditions mentioned above.** 
1. Click **Download** to download the selected assets.-->

<!---This dialog box displays the list of licenses associated with the selected assets in the left pane. Select a license to preview its terms and conditions (in pdf format) in the middle pane and the preview of the associated assets to the license in the right. Reviewed licenses are highlighted in light blue.


The dialog box that displays depends on whether the download list includes expired assets or only non-expired assets. <br/>
**Download expired assets dialog box:** This dialog box displays the expired assets' preview along with their expiry date in the left pane. The expired assets' count out of total selected displays in the right pane. Click **Proceed with all assets** to download expired assets with other assets (if present). The Download assets dialog box displays. See the [Download assets dialog box](#Download-asset-dialog-box) to proceed further.
    
    >[!NOTE]
    >
    >[Enable the download option for expired assets](/help/assets/configure-content-hub-ui-options.md#expired-assets-content-hub) to download them. Only expired assets that have enabled downloading are available for download.

   <a id="Download-asset-dialog-box"></a> **Download assets dialog box:** This dialog box displays the list of licenses associated with the selected assets in the left pane. Select a license to preview its terms and conditions (in pdf format) in the middle pane and the associated assets' preview and their count in the right pane. Reviewed licenses are highlighted in light blue.

    >[!NOTE]
    >
    > The **Download Asset dialog box** previews licensing terms and conditions only for approved licenses. [Approve the assets' licenses](/help/assets/approve-assets-content-hub.md) before downloading them to preview their licensing terms in the **Download Asset dialog box**.

1. Click  ![remove-icon](/help/assets/assets/remove-icon.svg) to remove a license from the download dialog box. 

1. Accept the terms and conditions and then click **Download** to download assets associated with the available licenses in the left pane.-->
<!--![download-multiple-license](/help/assets/assets/download-multiple-license.png)-->

<!---
### Download non-licensed Assets {#download-non-licensed-assets}

 To download non-licensed assets, select the assets and click ![download](/help/assets/assets/download-icon.svg) from the top rail.-->







