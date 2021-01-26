---
title: Administrar recursos de vídeo
description: Cargue, previsualización, anote y publique recursos de vídeo en [!DNL Adobe Experience Manager].
contentOwner: AG
translation-type: tm+mt
source-git-commit: deab2183447e64e8a98f3072ceab2ef2216c4528
workflow-type: tm+mt
source-wordcount: '619'
ht-degree: 6%

---


# Administrar recursos de vídeo {#manage-video-assets}

El formato de vídeo es una parte fundamental de los recursos digitales de una organización. [!DNL Adobe Experience Manager] Las ofertas maduran las ofertas y funciones para administrar todo el ciclo de vida de los recursos de vídeo después de crearlos.

Obtenga información sobre cómo administrar y editar los recursos de vídeo en [!DNL Adobe Experience Manager Assets]. La codificación y transcodificación de vídeo, por ejemplo, la transcodificación FFmpeg, es posible mediante Perfiles de procesamiento y mediante la integración [!DNL Dynamic Media]. Sin la licencia [!DNL Dynamic Media], [!DNL Experience Manager] proporciona soporte básico para vídeos, como la transcodificación mediante FFmpeg, la extracción de miniaturas de previsualización para los formatos de archivo admitidos y la previsualización en la interfaz de usuario para los formatos que se admiten para la reproducción directa en el explorador.

## Carga y previsualización de recursos de vídeo {#upload-and-preview-video-assets}

[!DNL Adobe Experience Manager Assets] genera previsualizaciones para recursos de vídeo con la extensión MP4. Puede realizar la previsualización de las representaciones en la interfaz de usuario [!DNL Assets].

1. En la carpeta o subcarpetas de recursos digitales, navegue a la ubicación donde desee agregar recursos digitales.
1. Para cargar el recurso, haga clic en **[!UICONTROL Crear]** en la barra de herramientas y elija **[!UICONTROL Archivos]**. También puede arrastrar un archivo en la interfaz de usuario. Consulte [carga de recursos](manage-digital-assets.md#uploading-assets) para obtener más información.
1. Para previsualización de un vídeo en la vista de la tarjeta, haga clic en la opción **[!UICONTROL Reproducir]** ![reproducir](assets/do-not-localize/play.png) del recurso de vídeo. Puede pausar o reproducir vídeo solo en la vista de la tarjeta. Las opciones [!UICONTROL Reproducir] y [!UICONTROL Pausar] no están disponibles en la vista de lista.
1. Para previsualización del vídeo en la página de detalles del recurso, seleccione **[!UICONTROL Editar]** en la tarjeta. El vídeo se reproduce en el reproductor de vídeo nativo del navegador. Puede reproducir, pausar, controlar el volumen y aplicar zoom en el vídeo a pantalla completa.

## Publicación de recursos de vídeo {#publish-video-assets}

Después de la publicación, puede incluir los recursos de vídeo en una página web como URL o incrustar directamente los recursos. Para obtener más información, consulte [publish [!DNL Dynamic Media] assets](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md).

## Transcodificar mediante el Perfil de procesamiento {#transcode-video}

[!DNL Experience Manager] como  [!DNL Cloud Service] le permite realizar la transcodificación básica de archivos de vídeo MP4 mediante Perfiles de procesamiento. La funcionalidad le permite no solo cargar, sino también previsualización y escalado de un archivo de vídeo MP4.

![Crear Perfil de procesamiento para la transcodificación de vídeo en  [!DNL Experience Manager]](assets/video-processing-profile-for-mp4.png)

*Figura: Un Perfil de procesamiento para la transcodificación de vídeo en  [!DNL Experience Manager].*

Si solo se proporciona anchura o altura y se deja el otro campo en blanco, las representaciones mantienen la proporción de aspecto. El códec de vídeo H.264 está disponible para la transcodificación.

Para procesar recursos con un perfil de procesamiento, agregue un perfil a una carpeta. Consulte [uso de perfiles de procesamiento para procesar recursos](/help/assets/asset-microservices-configure-and-use.md#use-profiles).

## Anotar recursos de vídeo {#annotate-video-assets}

1. En la consola [!DNL Assets], seleccione **[!UICONTROL Editar]** en la tarjeta de recursos para mostrar la página de detalles de recursos.
1. Para reproducir el vídeo, haga clic en **[!UICONTROL Previsualización]**.
1. Para realizar anotaciones en el vídeo, haga clic en **[!UICONTROL Anotar]**. Se agrega una anotación en el tiempo (fotograma) concreto del vídeo. Al realizar anotaciones, puede dibujar en el lienzo e incluir un comentario con el dibujo. Los comentarios se guardan automáticamente. Para salir del asistente para anotaciones, haga clic en **[!UICONTROL Cerrar]**.
1. Busque un punto específico en el vídeo, establezca el tiempo en segundos en el campo de **texto** y haga clic en **Saltar**. Por ejemplo, para omitir los primeros 20 segundos de vídeo, introduzca 20 en el campo de texto.
1. Para vista en la línea de tiempo, haga clic en una anotación. Para eliminar la anotación de la línea de tiempo, haga clic en **[!UICONTROL Eliminar]**.

## Prácticas recomendadas y limitaciones {#tips-limitations}

* Sin la licencia [!DNL Dynamic Media], solo puede procesar archivos MP4 mediante perfiles de procesamiento.
* Al transcodificar archivos MP4 con Perfiles de procesamiento, se aplican las siguientes directrices y limitaciones:

   * Los archivos Apple ProRes solo pueden transcodificarse a una resolución máxima de 1080p.
   * Si el archivo de origen tiene una velocidad de bits superior a 200 Mbps, sólo puede transcodificar a una resolución máxima de 1080p.
   * Si la velocidad de fotogramas de origen >= 60 fps entonces, el tamaño máximo del archivo de origen que puede utilizar es,

      * 400 MB para transcodificación de 4 k.
      * 800 MB para la transcodificación de 1080p.
      * 8 GB para transcodificación de 720p.
   * El tamaño máximo de archivo que se puede transcodificar a 4 k de resolución es de 2,55 GB de archivo MP4 con resolución de 4 k, velocidad de bits de 12 Mbps y 23 fps.


>[!MORELIKETHIS]
>
>* [Documentación](/help/assets/dynamic-media/video.md) de vídeo de Dynamic Media.
>* [Obtenga más información sobre el uso, los tipos y la configuración de perfiles](/help/assets/asset-microservices-configure-and-use.md) de procesamiento.

