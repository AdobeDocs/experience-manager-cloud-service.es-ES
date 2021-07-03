---
title: Administrar recursos de vídeo
description: Cargar, previsualizar, anotar y publicar recursos de vídeo en [!DNL Adobe Experience Manager].
contentOwner: AG
feature: Administración de recursos,Publicación,Colaboración,Vídeo
role: User
exl-id: 91edce4a-dfa0-4eca-aba7-d41ac907b81e
source-git-commit: a2c2a1f4ef4a8f0cf1afbba001d24782a6a2a24e
workflow-type: tm+mt
source-wordcount: '624'
ht-degree: 6%

---

# Administrar recursos de vídeo {#manage-video-assets}

El formato de vídeo es una parte fundamental de los recursos digitales de una organización. [!DNL Adobe Experience Manager] ofrece ofertas y funciones maduras para administrar todo el ciclo de vida de los recursos de vídeo tras su creación.

Obtenga información sobre cómo administrar y editar los recursos de vídeo en [!DNL Adobe Experience Manager Assets]. La codificación y transcodificación de vídeo, por ejemplo, la transcodificación FFmpeg, es posible mediante Perfiles de procesamiento y mediante la integración [!DNL Dynamic Media]. Sin la licencia [!DNL Dynamic Media], [!DNL Experience Manager] proporciona compatibilidad básica con los vídeos, como la transcodificación mediante FFmpeg, la extracción de miniaturas de vista previa para los formatos de archivo compatibles y la vista previa en la interfaz de usuario para los formatos compatibles con la reproducción directa en el explorador.

## Cargar y previsualizar recursos de vídeo {#upload-and-preview-video-assets}

[!DNL Adobe Experience Manager Assets] genera vistas previas para recursos de vídeo con la extensión MP4. Puede obtener una vista previa de las representaciones en la interfaz de usuario [!DNL Assets].

1. En la carpeta o subcarpetas de recursos digitales, vaya a la ubicación en la que desee agregar recursos digitales.
1. Para cargar el recurso, haga clic en **[!UICONTROL Create]** en la barra de herramientas y seleccione **[!UICONTROL Files]**. También puede arrastrar un archivo en la interfaz de usuario. Consulte [carga de recursos](manage-digital-assets.md#uploading-assets) para obtener más información.
1. Para obtener una vista previa de un vídeo en la vista de tarjeta, haga clic en la opción **[!UICONTROL Reproducir]** ![reproducir](assets/do-not-localize/play.png) del recurso de vídeo. Puede pausar o reproducir vídeo solo en la vista de tarjeta. Las opciones [!UICONTROL Play] y [!UICONTROL Pause] no están disponibles en la vista de lista.
1. Para obtener una vista previa del vídeo en la página de detalles del recurso, seleccione **[!UICONTROL Editar]** en la tarjeta. El vídeo se reproduce en el reproductor de vídeo nativo del explorador. Puede reproducir, pausar, controlar el volumen y hacer zoom en el vídeo hasta la pantalla completa.

## Publicar recursos de vídeo {#publish-video-assets}

Después de la publicación, puede incluir los recursos de vídeo en una página web como URL o incrustar directamente los recursos. Para obtener más información, consulte [publish [!DNL Dynamic Media] assets](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md).

## Transcodificar mediante un perfil de procesamiento {#transcode-video}

[!DNL Experience Manager] as a  [!DNL Cloud Service] permite realizar la transcodificación básica de archivos de vídeo MP4 utilizando Perfiles de procesamiento. La funcionalidad permite no solo cargar, sino también previsualizar y escalar un archivo de vídeo MP4.

![Crear perfil de procesamiento para la transcodificación de vídeo en  [!DNL Experience Manager]](assets/video-processing-profile-for-mp4.png)

*Figura: Un perfil de procesamiento para la transcodificación de vídeo en  [!DNL Experience Manager].*

Si proporciona solo anchura o altura y deja el otro campo en blanco, las representaciones mantienen la relación de aspecto. El códec de vídeo H.264 está disponible para la transcodificación.

Para procesar recursos mediante un perfil de procesamiento, agregue un perfil a una carpeta. Consulte [Uso de perfiles de procesamiento para procesar recursos](/help/assets/asset-microservices-configure-and-use.md#use-profiles).

## Anotar recursos de vídeo {#annotate-video-assets}

1. En la consola [!DNL Assets], seleccione **[!UICONTROL Editar]** en la tarjeta de recursos para mostrar la página de detalles del recurso.
1. Para reproducir el vídeo, haga clic en **[!UICONTROL Preview]**.
1. Para realizar anotaciones en el vídeo, haga clic en **[!UICONTROL Anotar]**. Se añade una anotación en el momento (fotograma) concreto del vídeo. Al anotar, puede dibujar en el lienzo e incluir un comentario con el dibujo. Los comentarios se guardan automáticamente. Para salir del asistente de anotaciones, haga clic en **[!UICONTROL Cerrar]**.
1. Busque un punto específico en el vídeo, establezca el tiempo en segundos en el campo de **texto** y haga clic en **Saltar**. Por ejemplo, para omitir los primeros 20 segundos de vídeo, introduzca 20 en el campo de texto.
1. Para verla en la línea de tiempo, haga clic en una anotación. Para eliminar la anotación de la cronología, haga clic en **[!UICONTROL Eliminar]**.

## Prácticas recomendadas y limitaciones {#tips-limitations}

* Sin la licencia [!DNL Dynamic Media], solo puede procesar archivos MP4 mediante perfiles de procesamiento.
* Al transcodificar archivos MP4 utilizando Perfiles de procesamiento, se aplican las siguientes directrices y limitaciones:

   * Los archivos Apple ProRes solo pueden transcodificarse a una resolución máxima de 1080p.
   * Si el archivo de origen tiene una velocidad de bits >200 Mbps, solo puede transcodificar a una resolución máxima de 1080p.
   * Si la velocidad de bits de origen >=60 fps entonces, el tamaño máximo del archivo de origen que puede usar es,

      * 400 MB para transcodificación de 4 k.
      * 800 MB para la transcodificación 1080p.
      * 8 GB para transcodificación de 720p.
   * El tamaño máximo de archivo que puede transcodificar a una resolución de 4 k es de 2,55 GB de archivo MP4 de resolución de 4 k, velocidad de bits de 12 Mbps y 23 fps.


>[!MORELIKETHIS]
>
>* [Documentación de vídeo de Dynamic Media](/help/assets/dynamic-media/video.md).
>* [Obtenga más información sobre el uso, los tipos y la configuración de perfiles](/help/assets/asset-microservices-configure-and-use.md) de procesamiento.

