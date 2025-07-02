---
title: Descarga de recursos desde Content Hub
description: Obtenga información sobre cómo descargar uno o varios recursos y sus representaciones desde el portal de Content Hub.
role: User
exl-id: 96d4ffba-4e3e-4496-9da2-6eb36be8331f
source-git-commit: fb7ce7dbb58be9fef5ab087441457770828d73c8
workflow-type: tm+mt
source-wordcount: '814'
ht-degree: 1%

---

# Descarga de recursos desde Content Hub {#download-assets}

[!DNL Content Hub] le permite descargar y compartir sus recursos. La interfaz de usuario [!DNL Content Hub] solo muestra los recursos aprobados. Estos recursos pueden incluir imágenes, vídeos o cualquier otro contenido digital. [!DNL Content Hub] mejora la accesibilidad y la adaptabilidad para una distribución eficaz de los recursos.

Puede descargar uno o varios recursos y sus representaciones disponibles mediante [!DNL Content Hub].

Ver los [tipos de representaciones disponibles en Content Hub](#types-of-renditions).

## Descargar uno o varios recursos y sus representaciones {#download-asset-renditions}

Para descargar uno o varios recursos y sus representaciones, ejecute los siguientes pasos:

1. Para descargar un recurso, seleccione ![descargar](/help/assets/assets/download-icon.svg) disponible en la tarjeta de recursos para obtener una vista previa del recurso, seleccione las representaciones disponibles y haga clic en la opción **[!UICONTROL Descargar]** del cuadro de diálogo para descargar las representaciones seleccionadas como archivo ZIP. Si el cuadro de diálogo muestra una licencia de recurso (para un recurso con licencia), acepte los términos y condiciones de licencia y haga clic en **[!UICONTROL Descargar]**.
   ![](/help/assets/assets/download-an-asset-CH-from-asset-card.png)

   También puede hacer clic en la miniatura del recurso y seleccionar ![descargar](/help/assets/assets/download-icon.svg) para seleccionar y ver las representaciones disponibles en el cuadro de diálogo antes de descargarlas.

1. Para descargar varios recursos, selecciónelos, haga clic en ![descargar](/help/assets/assets/download-icon.svg) **[!UICONTROL Descargar]** y revise la lista de recursos seleccionados en el cuadro de diálogo **[!UICONTROL Descargar recursos]**. Haga clic en ![anular la selección](/help/assets/assets/Close.svg) junto a un recurso para anular su selección en la lista. Seleccione una o más representaciones y haga clic en **[!UICONTROL Descargar]** para descargarlas como un solo archivo ZIP. Al seleccionar **[!UICONTROL Recorte inteligente]** y **[!UICONTROL Representaciones estáticas]**, se descargarán todas las representaciones estáticas y de recorte inteligente disponibles de cada recurso seleccionado.
   ![descargar varios recursos](/help/assets/assets/download-multiple-assets-CH.png)
Puede seguir usando [!DNL Content Hub] mientras la descarga está en curso. Content Hub no interrumpe el flujo de trabajo durante el proceso de descarga.
   ![descargar varios recursos](/help/assets/assets/download-assets-notification-ch.png)
Si el cuadro de diálogo **[!UICONTROL Descargar recursos]** muestra los recursos y las licencias, seleccione cada licencia en el panel izquierdo (sección [!UICONTROL Documentos de T&amp;C]) para obtener una vista previa de la licencia y mostrar los recursos seleccionados asociados con la licencia en el panel central del cuadro de diálogo. Después de revisar cada licencia, selecciona las representaciones, haz clic en **[!UICONTROL He leído y aceptado los términos y condiciones mencionados arriba]** y selecciona **[!UICONTROL Descargar]** para descargarlos.
   ![descargar varios recursos](/help/assets/assets/download-multiple-licensed-assets-CH.png)

   >[!NOTE]
   >
   >* Las representaciones se muestran únicamente si su visibilidad está habilitada mediante la interfaz de usuario de [[!UICONTROL Configuration]](/help/assets/configure-content-hub-ui-options.md#renditions-content-hub).
   >* Los usuarios con acceso a [[!DNL Dynamic Media with Open API capabilities]](/help/assets/dynamic-media-open-apis-overview.md) pueden ver y descargar representaciones de recortes dinámicas e inteligentes.
   >* La vista previa de la licencia solo se mostrará si el recurso se ha aprobado mediante el entorno de creación [!DNL Assets as a Cloud Service]. Para obtener más información, consulte [Administración de recursos con licencia en Content Hub](/help/assets/manage-licensed-assets-on-content-hub.md).

<!--

## Download an asset and its renditions {#download-asset-renditions} 

To download an asset and its renditions, execute the following steps: 

1. Click the asset to view its properties.

1. Click ![download](/help/assets/assets/download-icon.svg) to see the list of available asset renditions in the **[!UICONTROL Download]** panel.

   >[!NOTE]
   >
   >* The renditions display only if their visibility is enabled using the [Configuration](/help/assets/configure-content-hub-ui-options.md#renditions-content-hub) User Interface.
   >* You can download all [static, dynamic, and smart crop renditions](#types-of-renditions) while downloading an asset.

1. Select one or more renditions and click **[!UICONTROL Download]** to download the selected renditions as a zip file. 
While downloading a licensed asset, select **[!UICONTROL I have read and accepted the terms & conditions mentioned above]** before clicking **[!UICONTROL Download]**. You can also click **[!UICONTROL terms & conditions]** to view the asset license. The preview of the license displays only if the asset is approved using Assets as a Cloud Service authoring environment. For more information, see [Manage licensed assets on Content Hub](/help/assets/manage-licensed-assets-on-content-hub.md).

   ![Download single asset renditions](/help/assets/assets/download-single-asset-renditions.png)


If you are downloading a licensed asset, select **[!UICONTROL I have read and accepted the terms & conditions mentioned above]** and then click **[!UICONTROL Download]**. You can also click **[!UICONTROL terms & conditions]** to view the asset license. The preview of the license displays only if the asset is approved using Assets as a Cloud Service authoring environment. For more information, see [Manage licensed assets on Content Hub](/help/assets/manage-licensed-assets-on-content-hub.md).

>[!NOTE]
>
> The users with access to [Dynamic Media with Open API capabilities](/help/assets/dynamic-media-open-apis-overview.md) can view and download dynamic and smart crop renditions.

## Download multiple assets and their renditions {#download-multiple-assets-renditions} 

To download multiple assets and their renditions, execute the following steps: 

1. Select the assets and click ![download](/help/assets/assets/download-icon.svg) **[!UICONTROL Download]**. The [!UICONTROL Download assets] screen displays listing all the selected assets. 
1. Click **[!UICONTROL Download]** to select from the various download options to begin download:

    * **Download [!UICONTROL Originals]**: Select this option to download the selected assets in the original form.
    * **Download [!UICONTROL Static Renditions only]**: Select this option to download all available static renditions of assets except the original assets.
    * **Download [!UICONTROL Originals & Static Renditions]**: Select this option to download both original and static renditions of the selected assets. 

      ![Download multiple renditions](/help/assets/assets/download-multiple-renditions.png)

      >[!NOTE]
      >
      >* The renditions display only if their visibility is enabled using the [Configuration](/help/assets/configure-content-hub-ui-options.md#renditions-content-hub) User Interface.
      >* You can only download [static renditions](#types-of-renditions) while downloading multiple assets.

    If any of the selected asset is a licensed asset, click the license of the asset in left pane to see its preview, which enables you to select **[!UICONTROL I have read and accepted the terms & conditions mentioned above]** and then click **[!UICONTROL Download]**. The preview of the license displays only if the asset is approved using Assets as a Cloud Service authoring environment. For more information, see [Manage licensed assets on Content Hub](/help/assets/manage-licensed-assets-on-content-hub.md).

    <!--![download-multiple-license](/help/assets/assets/download-multiple-license.png)-->

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

## Tipos de representaciones {#types-of-renditions}

Las representaciones de recursos son diferentes representaciones del archivo original de un recurso. Pueden incluir miniaturas, versiones optimizadas para web o móvil, archivos con marca de agua o protegidos por DRM o incluso elementos dinámicos como cultivos inteligentes. No necesitan coincidir con el tipo de archivo original, sino que sirven para representar el recurso en varios casos de uso.

Más información sobre [ver y administrar representaciones en [!DNL Experience Manager Assets]](/help/assets/renditions.md).

[!DNL Experience Manager Assets] admite los siguientes tipos de representaciones:

* [Representaciones estáticas](/help/assets/renditions.md#static-renditions): las representaciones estáticas son versiones creadas previamente de recursos digitales, que generalmente se generan durante la ingesta o modificación de recursos. Están optimizados para usos y plataformas específicos, como miniaturas web, formatos compatibles con dispositivos móviles para diseños adaptables o archivos de alta resolución para imprimir, lo que proporciona una experiencia optimizada y coherente.

* [Representaciones dinámicas](/help/assets/renditions.md#dynamic-renditions): las representaciones dinámicas son versiones personalizadas en tiempo real de los recursos para realizar diversas acciones, como cambiar el tamaño de las imágenes para distintas resoluciones de dispositivo o recortarlas para adaptarlas a distintas proporciones de aspecto. Estas representaciones le permiten ofrecer experiencias personalizadas y optimizadas para satisfacer requisitos más amplios. Las representaciones dinámicas de recursos se crean en el entorno de creación [!DNL Adobe Experience Manager Assets]. Para obtener información sobre los pasos necesarios para habilitar las representaciones dinámicas, consulte [Habilitar representaciones dinámicas](#enable-dynamic-media-renditions).

* [Recorte inteligente](/help/assets/dynamic-media/image-profiles.md#creating-image-profiles): El recorte inteligente se centra únicamente en la parte esencial de un recurso durante el proceso de recorte. El recorte inteligente de Dynamic Media aprovecha la inteligencia artificial con tecnología de Adobe Sensei para rastrear el punto de interés, asegurándose de que nuestros recursos se vean mejor en todos los tamaños de pantalla. [!DNL Adobe Experience Manager] recorte inteligente muestra la anchura y la altura de las representaciones de un recurso junto con el título. Ver más en [uso del Recorte inteligente con AEM Assets en Dynamic Media](https://experienceleague.adobe.com/es/docs/experience-manager-learn/assets/dynamic-media/images/smart-crop-feature-video-use).

  Las representaciones de recorte inteligente se muestran y solo están disponibles para su descarga si tiene acceso a [Dynamic Media con capacidades OpenAPI](/help/assets/dynamic-media-open-apis-overview.md). Las representaciones de recorte inteligente solo están disponibles para los recursos de imagen.

  ![Tipos de representaciones](/help/assets/assets/renditions-types.png)

### Habilitar representaciones dinámicas {#enable-dynamic-media-renditions}

Para habilitar las representaciones dinámicas:

1. Asegúrese de tener acceso a [Dynamic Media con capacidades OpenAPI](/help/assets/dynamic-media-open-apis-overview.md).

   Una vez que tenga acceso a Dynamic Media con las capacidades de OpenAPI, todos los recursos marcados como `Approved` estarán disponibles para su envío público mediante Dynamic Media.

1. Establezca el [objetivo de aprobación del recurso](/help/assets/approve-assets-content-hub.md#set-approval-target) en Content Hub para aprobar los recursos solamente para Content Hub.

1. Habilite la opción **[!UICONTROL Habilitar disponibilidad de representaciones]** disponible en la ficha **[!UICONTROL Representaciones]** de la interfaz de usuario de [Configuración](/help/assets/configure-content-hub-ui-options.md#access-configuration-options-content-hub).

1. Vuelva a guardar los ajustes preestablecidos de imagen existentes para que estén disponibles en Content Hub. Solo es aplicable si ha incorporado recientemente a Dynamic Media con OpenAPI.

   Para volver a guardar los ajustes preestablecidos de imagen existentes, vaya a la vista Administración y seleccione **[!UICONTROL Herramientas]** > **[!UICONTROL Assets]** > **[!UICONTROL Ajustes preestablecidos de imagen]**. Seleccione un ajuste preestablecido, haga clic en **[!UICONTROL Editar]** y luego haga clic en **[!UICONTROL Guardar]**.



   >[!NOTE]
   > 
   > Las representaciones dinámicas solo están disponibles para recursos de imagen.



