---
title: Publicación de recursos de Dynamic Media
description: Cómo publicar recursos de medios dinámicos
contentOwner: Rick Brough
translation-type: tm+mt
source-git-commit: b65ce0af6281f60272322744f0e6f81b7eb6b96a
workflow-type: tm+mt
source-wordcount: '468'
ht-degree: 3%

---


# Publicación de recursos de Dynamic Media {#publishing-dynamic-media-assets}

Para publicar los recursos de Dynamic Media, seleccione los recursos que ya ha cargado y toque **[!UICONTROL Publicar]** o **[!UICONTROL Publicación rápida]**. Una vez publicados los recursos de Dynamic Media, estarán disponibles para su inclusión en una página web mediante una URL o mediante la incrustación de código en la página.

También puede publicar instantáneamente recursos que cargue, sin intervención del usuario. O bien, puede publicar estos recursos de forma selectiva. Consulte [Configuración de Dynamic Media.](config-dm.md) O bien, puede publicar recursos en Dynamic Media o en AEM, mutuamente excluyentes entre sí, mediante  **[!UICONTROL Publicación]** selectiva en el nivel de carpeta. Consulte [Uso de la publicación selectiva en Dynamic Media.](/help/assets/dynamic-media/selective-publishing.md)

En la **[!UICONTROL Vista de tarjeta]**, aparece un pequeño icono de globo terráqueo directamente debajo del nombre de un recurso y a la izquierda de la fecha y hora para indicar que se ha publicado. En la **[!UICONTROL vista de lista]**, una columna **[!UICONTROL Publicada]** indica qué recursos se publican o cuáles no.

>[!NOTE]
>
>Si un recurso ya está publicado, utilice AEM para moverlo a otra carpeta y volver a publicarlo desde su nueva ubicación, la ubicación del recurso publicado original seguirá estando disponible, junto con el recurso recién republicado. Sin embargo, el recurso publicado original se &quot;pierde&quot; por AEM y no se puede cancelar su publicación. Por lo tanto, se recomienda cancelar la publicación de los recursos antes de moverlos a una carpeta diferente.

Si tiene intención de publicar recursos de vídeo inmediatamente después de codificarlos, asegúrese de que la codificación está completa. Cuando se siguen codificando los vídeos, el sistema le permite saber que hay un flujo de trabajo de procesamiento de vídeo en curso. Cuando haya terminado la codificación de vídeo, debería poder realizar la previsualización de las representaciones de vídeo. En ese momento, puede publicar los vídeos sin incurrir en errores de publicación.

Consulte también [Vinculación de direcciones URL a la Aplicación web.](linking-urls-to-yourwebapplication.md)

Consulte también [Incrustación del visor de vídeo o de imagen de Dynamic Media en una página web.](embed-code.md)

>[!NOTE]
>
>* Los recursos deben publicarse para poder utilizar la dirección URL. Si no se publican los recursos, no funcionará copiar y pegar la URL en un explorador web.
>* Los ajustes preestablecidos de imagen y los ajustes preestablecidos de visor deben activarse y publicarse para el envío en directo.

>



Para obtener información detallada sobre la publicación de un conjunto o recurso, consulte [Publishing Assets.](/help/assets/manage-digital-assets.md)

## ENVÍO HTTP/2 de los recursos de Dynamic Media {#http-delivery-of-dynamic-media-assets}

AEM ahora admite el envío de todo el contenido de Dynamic Media (imágenes y vídeo) a través de HTTP/2. Es decir, una URL publicada o código incrustado para la imagen o el vídeo está disponible para integrarse con cualquier aplicación que acepte un recurso alojado. Ese recurso publicado se entrega a través del protocolo HTTP/2. Este método de envío mejora la forma en que se comunican los exploradores y los servidores, lo que permite una mejor respuesta y tiempos de carga de todos los recursos de Dynamic Media.

Consulte [HTTP/2 envío de contenido de preguntas más frecuentes](/help/assets/dynamic-media/http2faq.md) para obtener más información.
<!--this md file used to reside under sites-administering-->
