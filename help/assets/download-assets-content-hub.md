---
title: Descarga de recursos desde Content Hub
description: Obtenga información sobre cómo descargar recursos desde el portal de Content Hub
role: User
exl-id: 96d4ffba-4e3e-4496-9da2-6eb36be8331f
source-git-commit: e108d25f3cdc025e0fbe8010854f245f62786baf
workflow-type: tm+mt
source-wordcount: '938'
ht-degree: 10%

---

# Descarga de recursos desde Content Hub {#download-assets}

<table>
    <tr>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nuevo</i></sup> <a href="/help/assets/dynamic-media/dm-prime-ultimate.md"><b>Dynamic Media Prime y Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nuevo</i></sup> <a href="/help/assets/assets-ultimate-overview.md"><b>AEM Assets Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nuevo</i></sup> <a href="/help/assets/integrate-aem-assets-edge-delivery-services.md"><b>Integración de AEM Assets con Edge Delivery Services</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>New</i></sup> <a href="/help/assets/aem-assets-view-ui-extensibility.md"><b>Extensibilidad de la IU</b></a>
        </td>
          <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nuevo</i></sup> <a href="/help/assets/dynamic-media/enable-dynamic-media-prime-and-ultimate.md"><b>Habilitar Dynamic Media Prime y Ultimate</b></a>
        </td>
    </tr>
    <tr>
        <td>
            <a href="/help/assets/search-best-practices.md"><b>Prácticas recomendadas de búsqueda</b></a>
        </td>
        <td>
            <a href="/help/assets/metadata-best-practices.md"><b>Prácticas recomendadas de metadatos</b></a>
        </td>
        <td>
            <a href="/help/assets/product-overview.md"><b>Centro de contenido</b></a>
        </td>
        <td>
            <a href="/help/assets/dynamic-media-open-apis-overview.md"><b>Dynamic Media con funciones de OpenAPI</b></a>
        </td>
        <td>
            <a href="https://developer.adobe.com/experience-cloud/experience-manager-apis/"><b>Documentación de desarrollador de AEM Assets</b></a>
        </td>
    </tr>
</table>

<!-- ![Download assets](assets/download-asset.jpg) -->
![Descarga de recursos](assets/download-asset-genstudio.jpeg)

>[!AVAILABILITY]
>
>La guía del centro de contenido ya está disponible en formato de PDF. Descargue la guía completa y utilice el Asistente de IA de Adobe Acrobat para responder sus consultas.
>
>[!BADGE Guía del centro de contenido en PDF]{type=Informative url="https://helpx.adobe.com/content/dam/help/en/experience-manager/aem-assets/content-hub.pdf"}

Content Hub le permite descargar y compartir sus recursos. La interfaz de usuario de Content Hub solo muestra los recursos aprobados. Estos recursos pueden incluir imágenes, vídeos o cualquier otro contenido digital. Content Hub mejora la accesibilidad y la adaptabilidad para una distribución eficaz de los recursos.

Puede descargar uno o varios recursos y sus representaciones disponibles mediante Content Hub.

Ver [tipos de representaciones disponibles en Content Hub](#types-of-renditions).

## Descargar un recurso y sus representaciones {#download-asset-renditions}

Para descargar un recurso y sus representaciones, ejecute los siguientes pasos:

1. Haga clic en el recurso para ver sus propiedades.

1. Haga clic en ![descargar](/help/assets/assets/download-icon.svg) para iniciar el proceso de descarga. El panel Descargar enumera todas las representaciones de recursos disponibles.

   >[!NOTE]
   >
   >* Las representaciones se muestran únicamente si su visibilidad está habilitada mediante la interfaz de usuario de [Configuration](/help/assets/configure-content-hub-ui-options.md#renditions-content-hub).
   >* Puede descargar todas las [representaciones de recortes estáticas, dinámicas e inteligentes](#types-of-renditions) al descargar un recurso.

1. Seleccione una o más representaciones y haga clic en **[!UICONTROL Descargar]**.

   ![Descargar representaciones de recursos individuales](/help/assets/assets/download-single-asset-renditions.png)


Si está descargando un recurso con licencia, seleccione **[!UICONTROL He leído y aceptado los términos y condiciones mencionados anteriormente]** y luego haga clic en **[!UICONTROL Descargar]**. También puede hacer clic en **[!UICONTROL términos y condiciones]** para ver la licencia del recurso. La vista previa de la licencia solo se muestra si el recurso se aprueba mediante el entorno de creación de Assets as a Cloud Service. Para obtener más información, consulte [Administración de recursos con licencia en Content Hub](/help/assets/manage-licensed-assets-on-content-hub.md).

>[!NOTE]
>
> Los usuarios con acceso a [Dynamic Media con funciones de API abierta](/help/assets/dynamic-media-open-apis-overview.md) pueden ver y descargar representaciones de recortes dinámicas e inteligentes.

## Descargar varios recursos y sus representaciones {#download-multiple-assets-renditions}

Para descargar varios recursos y sus representaciones, ejecute los siguientes pasos:

1. Seleccione los recursos y haga clic en ![descargar](/help/assets/assets/download-icon.svg) **[!UICONTROL Descargar]**. La pantalla [!UICONTROL Descargar recursos] muestra una lista de todos los recursos seleccionados.
1. Haga clic en **[!UICONTROL Descargar]** para seleccionar entre las distintas opciones de descarga para comenzar la descarga:

   * **Descargar [!UICONTROL originales]**: selecciona esta opción para descargar los recursos seleccionados en el formulario original.
   * **Descargar solo [!UICONTROL representaciones estáticas]**: seleccione esta opción para descargar todas las representaciones estáticas de recursos disponibles, excepto los recursos originales.
   * **Descargar [!UICONTROL originales y representaciones estáticas]**: seleccione esta opción para descargar las representaciones originales y estáticas de los recursos seleccionados.

     ![Descargar varias representaciones](/help/assets/assets/download-multiple-renditions.png)

     >[!NOTE]
     >
     >* Las representaciones se muestran únicamente si su visibilidad está habilitada mediante la interfaz de usuario de [Configuration](/help/assets/configure-content-hub-ui-options.md#renditions-content-hub).
     >* Solo puede descargar [representaciones estáticas](#types-of-renditions) al descargar varios recursos.

   Si alguno de los recursos seleccionados es un recurso con licencia, haga clic en la licencia del recurso en el panel izquierdo para ver su vista previa, lo que le permite seleccionar **[!UICONTROL He leído y aceptado los términos y condiciones mencionados anteriormente]** y, a continuación, haga clic en **[!UICONTROL Descargar]**. La vista previa de la licencia solo se muestra si el recurso se aprueba mediante el entorno de creación de Assets as a Cloud Service. Para obtener más información, consulte [Administración de recursos con licencia en Content Hub](/help/assets/manage-licensed-assets-on-content-hub.md).

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

Más información sobre [ver y administrar representaciones en Experience Manager Assets](/help/assets/renditions.md).

[!DNL Experience Manager Assets] admite los siguientes tipos de representaciones:

* [Representaciones estáticas](/help/assets/renditions.md#static-renditions): las representaciones estáticas son versiones creadas previamente de recursos digitales, que generalmente se generan durante la ingesta o modificación de recursos. Están optimizados para usos y plataformas específicos, como miniaturas web, formatos compatibles con dispositivos móviles para diseños adaptables o archivos de alta resolución para imprimir, lo que proporciona una experiencia optimizada y coherente.

* [Representaciones dinámicas](/help/assets/renditions.md#dynamic-renditions): las representaciones dinámicas son versiones personalizadas en tiempo real de los recursos para realizar diversas acciones, como cambiar el tamaño de las imágenes para distintas resoluciones de dispositivo o recortarlas para adaptarlas a distintas proporciones de aspecto. Estas representaciones le permiten ofrecer experiencias personalizadas y optimizadas para satisfacer requisitos más amplios. Las representaciones dinámicas de recursos se crean en el entorno de creación [!DNL Adobe Experience Manager Assets]. Para obtener información sobre los pasos necesarios para habilitar las representaciones dinámicas, consulte [Habilitar representaciones dinámicas](#enable-dynamic-media-renditions).

* [Recorte inteligente](/help/assets/dynamic-media/image-profiles.md#creating-image-profiles): El recorte inteligente se centra únicamente en la parte esencial de un recurso durante el proceso de recorte. Dynamic media smart crop for aprovecha la inteligencia artificial con tecnología de Adobe Sensei para rastrear el punto de interés, asegurándose de que nuestros recursos se vean como sus mejores en todos los tamaños de pantalla. [!DNL Adobe Experience Manager] recorte inteligente muestra la anchura y la altura de las representaciones de un recurso junto con el título. Ver más en [uso del Recorte inteligente con AEM Assets en Dynamic Media](https://experienceleague.adobe.com/es/docs/experience-manager-learn/assets/dynamic-media/images/smart-crop-feature-video-use).

  Las representaciones de recorte inteligente se muestran y solo están disponibles para su descarga si tiene acceso a [Dynamic Media con capacidades OpenAPI](/help/assets/dynamic-media-open-apis-overview.md). Las representaciones de recorte inteligente solo están disponibles para los recursos de imagen.

  ![Tipos de representaciones](/help/assets/assets/renditions-types.png)

### Habilitar representaciones dinámicas {#enable-dynamic-media-renditions}

Para habilitar las representaciones dinámicas:

1. Asegúrese de tener acceso a [Dynamic Media con capacidades OpenAPI](/help/assets/dynamic-media-open-apis-overview.md).

   Una vez que tenga acceso a Dynamic Media con las capacidades de OpenAPI, todos los recursos marcados como `Approved` estarán disponibles para su envío público mediante Dynamic Media.

1. Establezca el [objetivo de aprobación del recurso](/help/assets/approve-assets-content-hub.md#set-approval-target) en Content Hub para aprobar los recursos solamente para Content Hub.

1. Habilite la opción **[!UICONTROL Habilitar disponibilidad de representaciones]** disponible en la ficha **[!UICONTROL Representaciones]** de la interfaz de usuario de [Configuración](/help/assets/configure-content-hub-ui-options.md#access-configuration-options-content-hub).

1. Vuelva a guardar los ajustes preestablecidos de imagen existentes para que estén disponibles en Content Hub. Solo es aplicable si ha incorporado recientemente a Dynamic Media con OpenAPI.

   Para volver a guardar los ajustes preestablecidos de imagen existentes, vaya a la vista de administración y seleccione **[!UICONTROL Herramientas]** > **[!UICONTROL Assets]** > **[!UICONTROL Ajustes preestablecidos de imagen]**. Seleccione un ajuste preestablecido, haga clic en **[!UICONTROL Editar]** y luego haga clic en **[!UICONTROL Guardar]**.



   >[!NOTE]
   > 
   > Las representaciones dinámicas solo están disponibles para recursos de imagen.



