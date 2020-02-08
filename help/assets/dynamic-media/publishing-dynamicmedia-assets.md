---
title: Publicación de recursos de Dynamic Media
description: Cómo publicar recursos de medios dinámicos
translation-type: tm+mt
source-git-commit: 6224d193adfb87bd9b080f48937e0af1f03386d6

---


# Publicación de recursos de Dynamic Media {#publishing-dynamic-media-assets}

Para publicar los recursos de Dynamic Media, selecciónelos y toque **[!UICONTROL Publicar]**. Una vez publicados los recursos de medios dinámicos, estarán disponibles para incluirlos en una página web mediante URL o mediante incrustación.

También puede publicar instantáneamente recursos que cargue, sin intervención del usuario. See [Configuring Dynamic Media](config-dm.md).

En la vista **[!UICONTROL de]** tarjeta, aparece un pequeño icono de globo terráqueo directamente debajo del nombre de un recurso para indicar que se ha publicado. En la vista **[!UICONTROL de]** lista, una columna **[!UICONTROL Publicada]** indica qué recursos se publican o cuáles no.

>[!NOTE]
>
>Si ya se ha publicado un recurso, utilice AEM para moverlo a otra carpeta y volver a publicarlo desde su nueva ubicación, la ubicación original del recurso publicado seguirá estando disponible, junto con el recurso recién republicado. Sin embargo, el recurso publicado original se &quot;pierde&quot; en AEM y no se puede cancelar la publicación. Por lo tanto, se recomienda cancelar la publicación de los recursos antes de moverlos a una carpeta diferente.

Si tiene intención de publicar recursos de vídeo inmediatamente después de codificarlos, asegúrese de que la codificación está completa. Cuando se siguen codificando los vídeos, el sistema le permite saber que hay un flujo de trabajo de procesamiento de vídeo en curso. Cuando haya terminado la codificación de vídeo, debería poder previsualizar las representaciones de vídeo. En ese momento, puede publicar los vídeos sin incurrir en errores de publicación.

Consulte también [Vinculación de direcciones URL a la aplicación](linking-urls-to-yourwebapplication.md)Web.

Consulte también [Incrustación del visor de vídeos en una página web.](embed-code.md)

>[!NOTE]
>
>* Los recursos deben publicarse para poder utilizar la dirección URL. Si no se publican los recursos, no funcionará copiar y pegar la URL en un explorador web.
>* Los ajustes preestablecidos de imagen y los ajustes preestablecidos de visor deben activarse y publicarse para la publicación en directo.
>



Para obtener información detallada sobre la publicación de un conjunto o recurso, consulte [Publicación de recursos.](/help/assets/manage-digital-assets.md)

## Entrega HTTP/2 de recursos de Dynamic Media {#http-delivery-of-dynamic-media-assets}

AEM ahora admite la entrega de todo el contenido de Dynamic Media (imágenes y vídeo) a través de HTTP/2. Es decir, una URL publicada o código incrustado para la imagen o el vídeo está disponible para integrarse con cualquier aplicación que acepte un recurso alojado. Ese recurso publicado se entrega a través del protocolo HTTP/2. Este método de entrega mejora la forma en que se comunican los exploradores y los servidores, lo que permite una mejor respuesta y tiempos de carga de todos los recursos de Dynamic Media.

Consulte la entrega [HTTP/2 de contenido de preguntas](/help/assets/dynamic-media/scene7-http2faq.md) más frecuentes para obtener más información.
<!--this md file used to reside under sites-administering-->
