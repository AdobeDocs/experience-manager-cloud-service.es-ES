---
title: Vídeo 360/VR
description: Aprenda a trabajar con 360 y vídeo de realidad virtual (VR) en Dynamic Media.
contentOwner: Rick Brough
feature: 360 VR Video
role: User
exl-id: ffd092d3-2188-47b0-a475-8bfa660c03c1
source-git-commit: 35caac30887f17077d82f3370f1948e33d7f1530
workflow-type: tm+mt
source-wordcount: '989'
ht-degree: 0%

---

# Vídeo 360/VR {#vr-video}

Los vídeos de 360° graban una vista en todas las direcciones al mismo tiempo. Se graban con una cámara omnidireccional o con una colección de cámaras. Durante la reproducción, en una pantalla plana, el usuario tiene control del ángulo de visualización; reproducción en dispositivos móviles suele aplicar sus controles giroscópicos integrados.

Dynamic Media incluye compatibilidad nativa con la entrega de 360 recursos de vídeo. De forma predeterminada, no es necesaria ninguna configuración adicional para la visualización o reproducción. El vídeo 360 se entrega con extensiones de vídeo estándar como .mp4, .mkv y .mov. El códec más común es H.264.

Puede utilizar el visualizador de vídeo 360/VR para procesar vídeo equirectangular. El resultado es una experiencia de visualización inmersiva de una habitación, propiedad, ubicación, paisaje, procedimiento médico, etc.

Actualmente no se admite audio espacial; si el audio se mezcla en estéreo, el balance (L/R) no cambia a medida que el cliente cambia el ángulo de visualización de la cámara.

Consulte [Uso de vídeos de Dynamic Media 360 y miniaturas de vídeo personalizadas con AEM Assets](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/dynamic-media/dynamic-media-360-video-custom-thumbnail-feature-video-use.html#dynamic-media).

Consulte también [Administración de ajustes preestablecidos de visor](/help/assets/dynamic-media/managing-viewer-presets.md).

## 360 Vídeo en acción {#video-in-action}

Select [Estación espacial 360](https://s7d1.scene7.com/s7viewers/html5/Video360Viewer.html?asset=Viewers/space_station_360-AVS) para abrir una ventana del explorador y ver un vídeo de 360°. Durante la reproducción de vídeo, arrastre el puntero a una nueva ubicación para cambiar el ángulo de visualización.

![Fotograma de vídeo de Space Station 360](assets/6_5_360videoiss_simplified.png)
*Fotograma de vídeo de la estación espacial 360*

## Vídeo y Adobe Premiere Pro 360/VR {#vr-video-and-adobe-premiere-pro}

Puede utilizar Adobe Premier Pro para ver y editar material de archivo 360/VR. Por ejemplo, puede colocar logotipos y texto correctamente en una escena y aplicar efectos y transiciones diseñados específicamente para medios equirectangulares.

Consulte [Editar vídeo 360/VR](https://helpx.adobe.com/premiere-pro/how-to/edit-360-vr-video.html).

## Cargar recursos para usarlos con el visor de vídeos 360 {#uploading-assets-for-use-with-the-video-viewer}

360 recursos de vídeo que se cargan en [!DNL Experience Manager] se etiquetan como **Multimedia** en una página de Asset, similar al recurso de vídeo normal.

![Un recurso de vídeo 360 cargado que se ve en la vista de tarjeta](assets/6_5_360video-selecttopreview.png)
*Recurso de vídeo cargado 360 que se ve en la vista de tarjeta. El recurso está etiquetado como multimedia.*

**Cargue recursos para utilizarlos con el visor de vídeos 360:**

1. Se ha creado una carpeta dedicada al recurso de vídeo 360.
1. [Aplicación de un perfil de vídeo adaptable a la carpeta](/help/assets/dynamic-media/video-profiles.md#applying-a-video-profile-to-folders).

   El procesamiento de contenido de vídeo 360 supone requisitos más altos para la resolución de vídeo de origen y para la resolución de representaciones codificadas que el contenido de vídeo estándar no 360.

   Puede utilizar el perfil de vídeo adaptable incorporado que ya viene con Dynamic Media. Sin embargo, tiene como resultado una calidad de vídeo de 360 perceptiblemente inferior a la que obtendría para los vídeos que no sean 360 codificados con la misma configuración representada con un visor de vídeo que no sea 360. Por lo tanto, si se requiere vídeo 360 de alta calidad, haga lo siguiente:

   * Lo ideal es que el contenido original de 360 vídeos tenga una de las siguientes resoluciones:

      * 1080p - 1920 x 1080, conocida como resolución Full HD o FHD,
      * 2160p - 3840 x 2160, conocida como resolución de alta definición de 4 k, UHD o Ultra. Esta gran resolución de pantalla suele encontrarse en los televisores de gama alta y en los monitores de ordenador. La resolución 2160p a menudo se denomina &quot;4k&quot; porque la anchura es cercana a los 4000 píxeles. En otras palabras, ofrece cuatro veces los píxeles de 1080p.
   * [Crear un perfil de vídeo adaptable personalizado](/help/assets/dynamic-media/video-profiles.md#creating-a-video-encoding-profile-for-adaptive-streaming) con representaciones de mayor calidad. Por ejemplo, puede crear un perfil de vídeo adaptable que contenga las tres configuraciones siguientes:

      * Width=auto; Altura=720; Velocidad de bits=2500 kbps
      * Width=auto; Altura=1080; Velocidad de bits=5000 kbps
      * Width=auto; Altura=1440; Velocidad de bits=6600 kbps
   * Procese contenido de vídeo 360 en una carpeta dedicada exclusivamente a 360 recursos de vídeo.

   Este enfoque impone buenas exigencias a la red y a la CPU del usuario final.

1. [Cargue el vídeo en la carpeta](/help/assets/manage-video-assets.md#upload-and-preview-video-assets).

<!--

## Overriding the default aspect ratio of 360 videos  {#overriding-the-default-aspect-ratio-of-videos}

For an uploaded asset to qualify as a 360 video that you intend to use with the 360 Video viewer, the asset must have an aspect ratio of 2.

By default, AEM detects video as "360" if its aspect ratio (width/height) is 2.0. If you are an Administrator, you can override the default aspect ratio setting of 2 by setting the optional `s7video360AR` property in CRXDE Lite at the following:

* `/conf/global/settings/cloudconfigs/dmscene7/jcr:content`

  * **Property type**: Double
  * **Value**: floating-point aspect ratio, default 2.0.

After you set this property, it takes effect immediately on both existing videos and newly uploaded videos.

The aspect ratio applies to 360 video assets for the asset details page and the [Video 360 Media WCM component](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md#dynamic-media-components).

Start by uploading 360 Videos.

-->

## Vista previa del vídeo 360 {#previewing-video}

Puede usar Vista previa para ver cómo aparece el vídeo 360 para los clientes y asegurarse de que se comporta según lo esperado.

Consulte también [Edición de ajustes preestablecidos de visor](/help/assets/dynamic-media/managing-viewer-presets.md#editing-viewer-presets).

Cuando esté satisfecho con el vídeo 360, puede publicarlo.

Consulte [Incrustación del visualizador de imágenes o vídeos en una página web](/help/assets/dynamic-media/embed-code.md).
Consulte [Vinculación de URL a la aplicación web](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md). El método de vinculación basado en URL no es posible si el contenido interactivo tiene vínculos con direcciones URL relativas, especialmente vínculos a [!DNL Experience Manager Sites] páginas.
Consulte [Adición de Dynamic Media Assets a las páginas](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md).

**Para previsualizar los vídeos 360:**

1. En **[!UICONTROL Recursos]**, vaya a un vídeo de 360 existente que haya creado. Para abrirlo en modo de vista previa, seleccione el recurso de vídeo 360.

   ![Captura de pantalla de un recurso de vídeo cargado 360 como se ve en la vista de tarjeta del Experience Manager.](assets/6_5_360video-selecttopreview-1.png)

   Para previsualizar el vídeo, seleccione el recurso de vídeo de 360.

1. En la página de vista previa, cerca de la esquina superior izquierda de la página, seleccione la lista desplegable y, a continuación, seleccione **[!UICONTROL Visualizadores]**.

   ![Captura de pantalla de la selección de Visualizadores para ver la lista de visualizadores de vídeo disponibles.](assets/6_5_360video-preview-viewers.png)

   En la lista Visualizadores, seleccione **[!UICONTROL Video360_social]** y, a continuación, realice una de las siguientes acciones:

   * Para modificar el ángulo de visualización de la escena estática, arrastre el puntero por el vídeo.
   * Para comenzar la reproducción, seleccione la **[!UICONTROL Play]** botón. A medida que se reproduce el vídeo, arrastre el puntero por el vídeo para modificar su ángulo de visualización.

   ![Captura de pantalla de un usuario que selecciona el visor Video360_Social para previsualizar un vídeo de 360 grados.](assets/6_5_360video-preview-video360-social.png)*Captura de pantalla de 360 videos.*

   * En la lista Visualizadores, seleccione **[!UICONTROL Video360VR]**.

      El vídeo de Realidad virtual (VR) es contenido de vídeo inmersivo al que se accede mediante auriculares de realidad virtual. Al igual que con los vídeos normales, se crean vídeos VR al principio cuando se graba o captura un vídeo con cámaras de vídeo de 360°.
   ![Captura de pantalla de un usuario que pasa el puntero del ratón sobre la opción Visor Video360VR.](assets/6_5_360video-preview-video360vr.png)
   *Captura de pantalla de un video de 360 VR.*

1. Cerca de la parte superior derecha de la página de vista previa, seleccione **[!UICONTROL Cerrar]**.

## Publicar vídeo 360 {#publishing-video}

Para usar el vídeo 360, debe publicarlo. Al publicar un vídeo de 360 se activa la dirección URL y el código incrustado. También publica el vídeo 360 en la nube de Dynamic Media, que está integrado con una CDN para una entrega escalable y con rendimiento.

Consulte [Publicación de recursos de Dynamic Media](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md) para obtener más información sobre cómo publicar vídeos 360.
Consulte también [Incrustación del visualizador de imágenes o vídeos en una página web](/help/assets/dynamic-media/embed-code.md).
Consulte también [Vinculación de URL a la aplicación web](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md). El método de vinculación basado en URL no es posible si el contenido interactivo tiene vínculos con direcciones URL relativas, especialmente vínculos a [!DNL Experience Manager Sites] páginas.
Consulte también [Adición de Dynamic Media Assets a las páginas](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md).
