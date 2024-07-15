---
title: Publicación de recursos de Dynamic Media
description: Obtenga información sobre cómo publicar recursos de vídeo e imagen de Dynamic Media para que pueda incluirlos en una página web mediante una URL o código incrustado en una página web.
contentOwner: Rick Brough
feature: Asset Management
role: User
exl-id: 8ee759dc-cb8f-4e80-8175-2c3ba06da862
source-git-commit: 0e452bd94d75609ecc3c20ab6b56ded968ed0a70
workflow-type: tm+mt
source-wordcount: '490'
ht-degree: 4%

---

# Publicación de recursos de Dynamic Media {#publishing-dynamic-media-assets}

Para publicar los recursos de Dynamic Media, selecciona los que ya has cargado y selecciona **[!UICONTROL Publish]** o **[!UICONTROL Quick Publish]**. Una vez publicados los recursos de Dynamic Media, estará disponible para incluirlos en una página web mediante una URL o incrustando código en la página.

También puede publicar al instante los recursos que carga, sin ninguna intervención del usuario. O bien, puede publicar esos recursos de forma selectiva. Consulte [Configuración de Dynamic Media](config-dm.md). O bien, puede publicar recursos de forma selectiva en Dynamic Media o Adobe Experience Manager, mutuamente excluyentes, mediante **[!UICONTROL Publish selectivo]** a nivel de carpeta. Ver [Trabajar con Publish selectivo en Dynamic Media](/help/assets/dynamic-media/selective-publishing.md).

En la **[!UICONTROL vista de tarjeta]**, aparece un pequeño icono de globo terráqueo directamente debajo del nombre de un recurso y a la izquierda de la fecha y la hora para indicar que se ha publicado. En la **[!UICONTROL vista de lista]**, una columna **[!UICONTROL Publicada]** indica qué recursos se publican o cuáles no.

>[!NOTE]
>
>Si un recurso ya se ha publicado, lo mueve a otra carpeta y lo vuelve a publicar desde su nueva ubicación, la ubicación del recurso publicado original aún estará disponible junto con el recurso recién publicado. Sin embargo, el recurso publicado original se &quot;pierde&quot; para el Experience Manager y no se puede cancelar su publicación. Por lo tanto, como práctica recomendada, cancele la publicación de los recursos primero antes de moverlos a una carpeta diferente.

Si tiene intención de publicar recursos de vídeo inmediatamente después de codificarlos, asegúrese de que la codificación está completada. Cuando se codifican vídeos, el sistema le permite saber que hay un flujo de trabajo de procesamiento de vídeo en curso. Cuando se haya completado la codificación de vídeo, puede obtener una vista previa de las representaciones de vídeo. En ese punto, es seguro para usted publicar los vídeos sin incurrir en ningún error de publicación.

Ver también [URL de vínculo a su aplicación web](linking-urls-to-yourwebapplication.md).

Ver también [Incrustar el visor de vídeo o de imágenes de Dynamic Media en una página web](embed-code.md).

>[!NOTE]
>
>* Assets debe publicarse para utilizar la dirección URL. Si los recursos no se publican, no funcionará copiar y pegar la dirección URL en un explorador web.
>* Los ajustes preestablecidos de imagen y de visualizador se deben activar y publicar para la entrega en directo.
>

Para obtener información detallada sobre cómo publicar un conjunto o recurso, consulte [Publicar Assets](/help/assets/manage-digital-assets.md).

## Envío HTTP/2 de recursos de Dynamic Media {#http-delivery-of-dynamic-media-assets}

Experience Manager ahora admite la entrega de todo el contenido de Dynamic Media (imágenes y vídeo) a través de HTTP/2. Es decir, hay disponible una URL publicada o código incrustado para la imagen o el vídeo que se va a integrar con cualquier aplicación que acepte un recurso alojado. Ese recurso publicado se entrega mediante el protocolo HTTP/2. Este método de entrega mejora la forma en que los navegadores y servidores se comunican, lo que permite una mejor respuesta y tiempos de carga de todos los recursos de Dynamic Media.

Ver [preguntas más frecuentes sobre la entrega de contenido HTTP/2](/help/assets/dynamic-media/http2faq.md).

<!--this md file used to reside under sites-administering-->
