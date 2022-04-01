---
title: Configurar el servicio de transcripción
seo-title: Configure transcription service
description: Adobe Experience Manager Assets está configurado con [!DNL Azure Media Services] que genera automáticamente la transcripción textual del idioma hablado en un archivo de audio o vídeo compatible en formato WebVTT (Vtt).
seo-description: When an audio or video asset is processed in Experience Manager Assets, the AI-based transcription service automatically generates the text transcript rendition of the audio or video asset and stores it at the same location within your Assets repository where the original asset resides. The Experience Manager Assets transcription service allows marketers to effectively manage their audio and video content with added discoverability of the text content as well as increase the ROI of these assets by supporting accessibility and localization.
products: SG_EXPERIENCEMANAGER/ASSETS and Experience Manager as a Cloud Service
sub-product: assets
content-type: reference
contentOwner: Vishabh Gupta
topic-tags: Configuration
feature: Asset Management, Configuration
role: Admin
source-git-commit: feef8159a01393baebe11c014ae6093b79df72d1
workflow-type: tm+mt
source-wordcount: '1666'
ht-degree: 0%

---


# Configure la transcripción en [!DNL Experience Manager Assets] {#configure-transcription-service}

La transcripción es el proceso de traducir el audio de un archivo de audio o vídeo a texto (de voz a texto) utilizando la tecnología de reconocimiento de voz.
[!DNL Adobe Experience Manager Assets] está configurado con [!DNL Azure Media Services] que genera automáticamente la transcripción textual del idioma hablado en un archivo de audio o vídeo compatible en formato WebVTT (.vtt). Cuando se procesa un recurso de audio o vídeo en [!DNL Experience Manager Assets], el servicio de transcripción genera automáticamente la representación de transcripción de texto del recurso de audio o vídeo y la almacena en la misma ubicación del repositorio de Assets en la que reside el recurso original. La variable [!DNL Experience Manager Assets] el servicio de transcripción permite a los especialistas en marketing administrar de forma eficaz el contenido de audio y vídeo con una mayor capacidad de detección del contenido de texto, así como aumentar el ROI de estos recursos al admitir la accesibilidad y la localización.

Las transcripciones son versiones textuales de contenido hablado; un ejemplo es una película que está viendo en cualquier plataforma OTT y que a menudo incluye subtítulos o subtítulos para facilitar la accesibilidad o consumir el contenido en otros idiomas. O cualquier archivo de audio o vídeo que se utilice con fines de marketing, aprendizaje o entretenimiento. Estas experiencias comienzan con una transcripción a la que luego se les aplica formato o se traduce según corresponda. La transcripción de audio o vídeo es un proceso intensivo de tiempo y propenso a errores cuando se realiza manualmente. También es un desafío escalar el proceso manual, dada la necesidad cada vez mayor de contenido de audio-vídeo. [!DNL Experience Manager Assets] utiliza la transcripción basada en IA de Azure, que permite un procesamiento a gran escala de los recursos de audio y vídeo y genera las transcripciones de texto (archivos .vtt) junto con los detalles de la marca de tiempo. Junto con Assets, la función de transcripción también es compatible con Dynamic Media.

La función de transcripción está disponible sin ningún coste en [!DNL Experience Manager Assets]. Sin embargo, los administradores requieren las credenciales de Azure del usuario para configurar el servicio de transcripción en [!DNL Experience Manager Assets]. También puede [obtener las credenciales de prueba](https://azure.microsoft.com/en-us/pricing/details/media-services/) directamente desde Microsoft® para experimentar la función de transcripción de audio o vídeo en Assets.

## Requisitos previos de transcripción {#prerequisites}

1. Un proceso de puesta en marcha [!DNL Experience Manager Assets as a Cloud Service] instancia.
1. Se requieren las siguientes credenciales de Azure para la configuración en [!DNL Experience Manager Assets]:

   * ID de cliente (clave de API)
   * Clave secreta del cliente
   * Punto final del inquilino (dominio)
   * Cuenta de medios
   * Grupo de recursos
   * ID de suscripción

   Consulte [Documentación de Azure](https://docs.microsoft.com/en-us/azure/media-services/latest/access-api-howto?tabs=portal) para obtener credenciales para acceder a la API de Azure Media Services.

1. Asegúrese de que la cuenta de Azure tenga suficiente crédito para procesar nuevas solicitudes.

## Configure la transcripción en [!DNL Experience Manager Assets] {#configure-transcription}

A continuación se indican las configuraciones necesarias para habilitar la función de transcripción en [!DNL Experience Manager Assets]:

1. [Configurar Azure Media Services](#configure-azure-media-service)
1. [Configuración del perfil de procesamiento para la transcripción de audio/vídeo](#configure-processing-profile-for-transcription)


### Configurar Azure Media Services {#configure-azure-media-services}

[!DNL Experience Manager Assets] utiliza la variable [!DNL Azure Media Services] que genera automáticamente transcripciones de texto del idioma hablado en un [archivo de audio o vídeo admitido](#supported-file-formats-for-transcription) en el formato WebVTT (.vtt). Los administradores pueden configurar [!DNL Azure Media Services] en [!DNL Experience Manager Assets] usando las credenciales de Azure. La variable [requisitos previos de transcripción](#transcription-prerequisites) la lista [!DNL Azure] credenciales necesarias para la configuración. Si no tiene [!DNL Azure] cuenta y credenciales, consulte [Documentación de Azure Media Services](https://azure.microsoft.com/en-us/pricing/details/media-services/) para obtener las credenciales de prueba.

![configure-transcription-service](assets/configure-transcription-service.png)

Vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Configuración de Azure Media Services]**. Seleccione una carpeta (ubicación) en el carril izquierdo y haga clic en el botón [!UICONTROL Crear] para configurar la conexión con su [!DNL Azure] cuenta. Esta carpeta es la ubicación donde [!DNL Azure] la configuración de nube se almacena en Experience Manager Assets. Introduzca la variable [!DNL Azure] credenciales y haga clic en **[!UICONTROL Guardar y cerrar]**.

### Configuración del perfil de procesamiento para la transcripción {#configure-processing-profile}

Una vez que la variable [!DNL Azure Media Services] está configurado en Experience Manager Assets, el siguiente paso es crear un perfil de procesamiento de recursos para generar una transcripción basada en AI de los recursos de audio y vídeo. El perfil de procesamiento basado en IA genera transcripciones de la variable [recurso de audio o vídeo admitido](#supported-file-formats-for-transcription) como una representación en Experience Manager Assets y almacena la transcripción (archivo .vtt) en la misma carpeta en la que reside el recurso original. Por lo tanto, es más fácil para los usuarios buscar y localizar el recurso y su representación de transcripción.

Vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Recursos]** > **[!UICONTROL Perfiles de procesamiento]** y haga clic en el botón **[!UICONTROL Crear]** para crear un perfil de procesamiento basado en IA que genere la transcripción de sus archivos de audio y vídeo. De forma predeterminada, la página de procesamiento de perfiles refleja solo tres fichas (Imagen, Vídeo y Personalizado). Sin embargo, un **[!UICONTROL AI de contenido]** está visible si ha configurado [!DNL Azure Media Services] en su [!DNL Experience Manager Assets] instancia. Compruebe su [!DNL Azure] credenciales si no ve la variable **[!UICONTROL AI de contenido]** al crear un perfil de procesamiento.

En el **[!UICONTROL AI de contenido]** , haga clic en la pestaña **[!UICONTROL Agregar nuevo]** para configurar la transcripción. Aquí puede incluir y excluir los formatos de archivo (tipos MIME) para generar transcripciones seleccionando tipos de archivo en la lista desplegable. En la siguiente ilustración, se incluyen todos los archivos de audio y vídeo compatibles y se excluyen los archivos de texto.

Active la variable **[!UICONTROL Crear transcripción VTT en el mismo directorio]** alterne para crear y almacenar la representación de la transcripción (archivo .vtt) en la misma carpeta en la que reside el recurso original. Las demás representaciones también se generan mediante el flujo de trabajo predeterminado de procesamiento de recursos DAM, independientemente de esta configuración.

![configure-transcription-service](assets/configure-transcription-profile.png)

La siguiente ilustración detalla un perfil de vídeo personalizado que se crea en Experience Manager Assets.

![configure-transcription-service](assets/video-processing-profile.png)

El perfil de vídeo también contiene las siguientes configuraciones personalizadas. Consulte [documentación del perfil de procesamiento](/help/assets/asset-microservices-configure-and-use.md) para obtener más información sobre cómo crear un perfil de procesamiento personalizado.

![configure-transcription-service](assets/video-processing-profile2.png)

Ahora vamos a configurar la transcripción en este perfil de vídeo. Vaya a la **[!UICONTROL AI de contenido]** y haga clic en **[!UICONTROL Agregar nuevo]** botón. Incluya todos los archivos de audio y vídeo y excluya los archivos de imagen y aplicación. Active la variable **[!UICONTROL Crear transcripción VTT en el mismo directorio]** alterne y guarde la configuración.

![configure-transcription-service](assets/video-processing-profile1.png)

Una vez configurado el perfil de procesamiento para la transcripción de archivos de audio y vídeo, puede aplicar este perfil de procesamiento a las carpetas mediante uno de los métodos siguientes:

* Seleccione una definición de perfil de procesamiento en **[!UICONTROL Herramientas]** > **[!UICONTROL Recursos]** > **[!UICONTROL Perfiles de procesamiento]** y utilice **[!UICONTROL Aplicar perfil a carpetas]** acción. El navegador de contenido le permite desplazarse a una carpeta específica, seleccionar una carpeta y confirmar la aplicación del perfil.
* Seleccione una carpeta en la interfaz de usuario de Assets y haga clic en **[!UICONTROL Propiedades]** para abrir las propiedades de la carpeta. Haga clic en el **[!UICONTROL Procesamiento de recursos]** y seleccione el perfil de procesamiento adecuado para la carpeta en la pestaña **[!UICONTROL Perfil de procesamiento]** lista. Para guardar los cambios, haga clic en **[!UICONTROL Guardar y cerrar]**.

   ![configure-transcription-service](assets/video-processing-profile3.png)

* Los usuarios pueden seleccionar carpetas o recursos específicos en la interfaz de usuario de Assets para aplicar un perfil de procesamiento y, a continuación, seleccionar **[!UICONTROL Volver a procesar recursos]** en las opciones disponibles en la parte superior.

>[!TIP]
>Solo se puede aplicar un perfil de procesamiento a una carpeta.
>
>Después de aplicar un perfil de procesamiento a una carpeta, todos los recursos nuevos cargados (o actualizados) en esta carpeta o en cualquiera de sus subcarpetas se procesan con el perfil de procesamiento adicional configurado. Este procesamiento se suma al perfil predeterminado estándar.

>[!NOTE]
>
>Un perfil de procesamiento aplicado a una carpeta funciona para todo el árbol, sin embargo, se puede sobrescribir con otro perfil aplicado a una subcarpeta.
>
>Cuando los recursos se cargan en una carpeta, el Experience Manager se comunica con las propiedades de la carpeta contenedora para identificar el perfil de procesamiento. Si no se aplica ninguno, se comprueba la existencia de un perfil de procesamiento en una carpeta principal de la jerarquía.


## Genere la transcripción de sus activos de audio o vídeo {#generate-transcription}

Al procesar un recurso de vídeo, la variable [Perfil de procesamiento basado en IA](#configure-processing-profile-for-transcription) genera automáticamente la transcripción (archivo .vtt) como una representación junto con el recurso original en la misma carpeta.

![configure-transcription-service](assets/transcript1.png)

También puede ver la representación de la transcripción accediendo a las Representaciones del recurso de vídeo original. Para acceder a la **[!UICONTROL Representaciones]** seleccione el recurso de vídeo original y abra el carril izquierdo. Puede ver que la representación de la transcripción (archivo .vtt) está visible en la sección **[!UICONTROL TRANSCRIPTVTT]** cabeza.

![configure-transcription-service](assets/transcript.png)

Puede descargar la transcripción (archivo de texto .vtt) directamente desde la carpeta como una representación de recursos independiente o desde la **[!UICONTROL Representaciones]** del recurso original descargando todas las representaciones del recurso.

Actualmente, el Experience Manager no admite la vista previa o edición de texto completo de archivos VTT de forma nativa. Sin embargo, puede descargar la representación de la transcripción y utilizar cualquier editor de texto para editar o verificar la transcripción. La transcripción refleja el idioma hablado como texto en la marca de tiempo dada en el vídeo con la puntuación de confianza (precisión) de la transcripción.

![configure-transcription-service](assets/transcript-text.png)

## Uso de la transcripción en Dynamic Media {#using-transcription-in-dynamic-media}

Si tiene [Dynamic Media configurado](/help/assets/dynamic-media/config-dm.md) en la instancia de Experience Manager Assets, puede publicar el recurso (archivo de audio o vídeo) y su transcripción (archivo .vtt) en Dynamic Media. Al hacerlo, el recurso original (archivo de audio o vídeo) y su representación transcrita (archivo .vtt) se publican en Dynamic Media en la misma carpeta. El administrador de Dynamic Media puede [activar la experiencia CC Closed Caption](/help/assets/dynamic-media/video.md#adding-captions-to-video) para el archivo de audio o vídeo que utiliza la representación de transcripción (archivo .vtt).

Consulte también:

* [Tutorial de vídeo sobre cómo añadir subtítulos CC a Dynamic Media](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/dynamic-media/dynamic-media-overview-feature-video-use.html#add-cc-closed-captioning-to-dynamic-media-video)
* [Publicar vídeos de Dynamic Media en YouTube](/help/assets/dynamic-media/video.md#publishing-videos-to-youtube)

En la siguiente ilustración, la URL refleja la parte del rótulo que hace referencia a la transcripción (archivo .vtt). El vídeo refleja el idioma hablado (texto transcrito) como un **[!UICONTROL Subtítulos]** en la marca de tiempo determinada del vídeo. El usuario puede habilitar o deshabilitar el rótulo utilizando la variable **[!UICONTROL CC]** botón.

![configure-transcription-service](assets/transcript-example.png)

## Formatos de archivo compatibles con la transcripción {#supported-file-format}

Se admiten los siguientes formatos de archivo de audio y vídeo para la transcripción:

| Formatos de audio y vídeo compatibles | Extensiones |
|----|----|
| FLV (con códecs H.264 y AAC) | (.flv) |
| MXF | (.mxf) |
| MPEG2-PS, MPEG2-TS, 3GP | (.ts, .ps, .3gp, .3gpp, .mpg) |
| Vídeo de Windows Media (WMV)/ASF | (.wmv, .asf) |
| AVI (sin comprimir 8 bits/10 bits) | (.avi) |
| MP4 | (.mp4, .m4a, .m4v) |
| Grabación de vídeo digital Microsoft® (DVR-MS) | (.dvr-ms) |
| Matroska/WebM | (.mkv) |
| WAVE/WAV | (.wav) |
| QuickTime | (.mov) |


>[!NOTE]
>
>Los recursos (archivos de audio o vídeo) del tipo aplicación no son compatibles con la transcripción.

## Limitaciones conocidas {#known-limitations}

* La función de transcripción es compatible con vídeos de hasta 10 minutos de duración.
* El título del vídeo debe tener menos de 80 caracteres.
* El tamaño de archivo admitido es de hasta 15 GB.
* La duración máxima de procesamiento admitida es de 60 minutos.
* En un [!DNL Azure] cuenta, puede cargar hasta 50 películas por minuto. Sin embargo, en una cuenta de prueba puede cargar hasta cinco películas por minuto.

## Sugerencias de resolución de problemas {#troubleshooting}

Inicie sesión en su [!DNL Azure Media Services] cuenta con las mismas credenciales (que ha utilizado para la configuración) para verificar el estado de la solicitud. Contacto [!DNL Azure] compatibilidad si la solicitud no se ha procesado correctamente.



