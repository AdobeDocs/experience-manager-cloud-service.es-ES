---
title: Administrar recursos de vídeo
description: Carga, previsualización, anotación y publicación de recursos de vídeo en [!DNL Adobe Experience Manager].
contentOwner: AG
feature: Asset Management,Publishing,Collaboration,Video
role: User
exl-id: 91edce4a-dfa0-4eca-aba7-d41ac907b81e
source-git-commit: 038dbc4b0febfa58f69e05f837760162210f8689
workflow-type: tm+mt
source-wordcount: '656'
ht-degree: 6%

---

# Administrar recursos de vídeo {#manage-video-assets}

El formato de vídeo es una parte esencial de los recursos digitales de una organización. [!DNL Adobe Experience Manager] ofrece ofertas y funciones maduras para administrar todo el ciclo de vida de los recursos de vídeo después de su creación.

Obtenga información sobre cómo administrar y editar los recursos de vídeo en [!DNL Adobe Experience Manager Assets]. La codificación y transcodificación de vídeo, por ejemplo, la transcodificación FFmpeg, es posible mediante Perfiles de procesamiento y utilizando [!DNL Dynamic Media] integración. Sin [!DNL Dynamic Media] licencia, [!DNL Experience Manager] proporciona compatibilidad básica con vídeos, como transcodificar mediante FFmpeg, extraer miniaturas de vista previa de los formatos de archivo admitidos y previsualizar en la interfaz de usuario los formatos compatibles con la reproducción directa en el explorador.

## Carga y previsualización de recursos de vídeo {#upload-and-preview-video-assets}

[!DNL Adobe Experience Manager Assets] genera previsualizaciones para recursos de vídeo con la extensión MP4. Puede obtener una vista previa de las representaciones en el [!DNL Assets] interfaz de usuario.

1. En la carpeta o subcarpetas de recursos digitales, vaya a la ubicación donde desee agregar recursos digitales.
1. Para cargar el recurso, haga clic en **[!UICONTROL Crear]** en la barra de herramientas y elija **[!UICONTROL Archivos]**. También puede arrastrar un archivo a la interfaz de usuario. Consulte [cargar recursos](manage-digital-assets.md#uploading-assets) para obtener más información.
1. Para obtener una vista previa de un vídeo en la vista de tarjeta, haga clic en **[!UICONTROL Reproducir]** ![opción de reproducción](assets/do-not-localize/play.png) en el recurso de vídeo. Solo puede pausar o reproducir vídeo en la vista de tarjeta. El [!UICONTROL Reproducir] y [!UICONTROL Pausar] Las opciones de no están disponibles en la vista de lista.
1. Para obtener una vista previa del vídeo en la página de detalles del recurso, seleccione **[!UICONTROL Editar]** en la tarjeta. El vídeo se reproduce en el reproductor de vídeo nativo del explorador. Puede reproducir, pausar, controlar el volumen y ampliar el vídeo a pantalla completa.

## Publicar recursos de vídeo {#publish-video-assets}

Después de la publicación, puede incluir los recursos de vídeo en una página web como una URL o incrustar directamente los recursos. Para obtener más información, consulte [publicar [!DNL Dynamic Media] activos](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md).

## Transcodificar mediante perfil de procesamiento {#transcode-video}

[!DNL Experience Manager] as a [!DNL Cloud Service] permite realizar transcodificaciones básicas de archivos de vídeo MP4 mediante perfiles de procesamiento. La funcionalidad le permite no solo cargar, sino también previsualizar y escalar un archivo de vídeo MP4.

![Creación de un perfil de procesamiento para la transcodificación de vídeo en [!DNL Experience Manager]](assets/video-processing-profile-for-mp4.png)

*Figura: Perfil de procesamiento para la transcodificación de vídeo en [!DNL Experience Manager].*

Si solo se proporciona anchura o altura y se deja en blanco el otro campo, las representaciones mantienen la relación de aspecto. El códec de vídeo H.264 está disponible para transcodificar.

Para procesar recursos mediante un perfil de procesamiento, agregue un perfil a una carpeta. Consulte [uso de perfiles de procesamiento para procesar recursos](/help/assets/asset-microservices-configure-and-use.md#use-profiles).

## Anotar recursos de vídeo {#annotate-video-assets}

Puede añadir anotaciones a recursos de vídeo. Al realizar anotaciones en vídeos, el reproductor realiza pausas para permitirle realizar anotaciones en un fotograma. Para obtener más información, consulte [administración de recursos de vídeo](manage-video-assets.md).

>[!NOTE]
>
>El formato de vídeo MXF aún no es compatible con anotaciones de recursos de vídeo.

1. Desde el [!DNL Assets] consola, seleccione **[!UICONTROL Editar]** en la tarjeta de recursos para mostrar la página de detalles del recurso.
1. Para reproducir el vídeo, haga clic en **[!UICONTROL Previsualizar]**.
1. Para anotar el vídeo, haga clic en **[!UICONTROL Anotar]**. Se añade una anotación en el momento (fotograma) concreto del vídeo. Al realizar anotaciones, puede dibujar en el lienzo e incluir un comentario con el dibujo. Los comentarios se guardan automáticamente. Para salir del asistente de anotaciones, haga clic en **[!UICONTROL Cerrar]**.
1. Busque un punto específico en el vídeo, establezca el tiempo en segundos en el campo de **texto** y haga clic en **Saltar**. Por ejemplo, para omitir los primeros 20 segundos de vídeo, introduzca 20 en el campo de texto.
1. Para verla en la cronología, haga clic en una anotación. Para eliminar la anotación de la cronología, haga clic en **[!UICONTROL Eliminar]**.

## Prácticas recomendadas y limitaciones {#tips-limitations}

* Sin [!DNL Dynamic Media] Con esta licencia, solo puede procesar archivos MP4 mediante perfiles de procesamiento.
* Al transcodificar archivos MP4 mediante perfiles de procesamiento, se aplican las siguientes directrices y limitaciones:

   * Los archivos ProRes de Apple solo pueden transcodificarse a una resolución máxima de 1080p.
   * Si el archivo de origen tiene una velocidad de bits >200 Mbps, solo puede transcodificar a una resolución máxima de 1080p.
   * Si la velocidad de fotogramas de origen >=60 fps, el tamaño máximo del archivo de origen que puede utilizar es,

      * 400 MB para transcodificación de 4k.
      * 800 MB para transcodificación a 1080p.
      * 8 GB para transcodificación a 720p.
   * El tamaño máximo de archivo que puede transcodificar a una resolución de 4k es de 2,55 GB de archivo MP4 con resolución de 4k, velocidad de bits de 12 Mbps y 23 fps.


>[!MORELIKETHIS]
>
>* [Documentación de vídeo de Dynamic Media](/help/assets/dynamic-media/video.md).
>* [Más información sobre el uso, los tipos y la configuración de los perfiles de procesamiento](/help/assets/asset-microservices-configure-and-use.md).

