---
title: Publicación de recursos de Dynamic Media
description: Obtenga información sobre cómo publicar recursos de Dynamic Media.
contentOwner: Rick Brough
feature: Asset Management
role: User
exl-id: 8ee759dc-cb8f-4e80-8175-2c3ba06da862
source-git-commit: a11529886d4b158c19a97ccbcb7d004cf814178d
workflow-type: tm+mt
source-wordcount: '462'
ht-degree: 5%

---

# Publicación de recursos de Dynamic Media {#publishing-dynamic-media-assets}

Para publicar los recursos de Dynamic Media, seleccione los que ya ha cargado y **[!UICONTROL Publicación]** o **[!UICONTROL Publicación rápida]**. Una vez publicados los recursos de Dynamic Media, quedan disponibles para su inclusión en una página web mediante una URL o mediante la incrustación de código en la página.

También puede publicar recursos instantáneamente que cargue, sin intervención del usuario. O bien, puede publicar estos recursos de forma selectiva. Consulte [Configuración de Dynamic Media](config-dm.md). O bien, puede publicar selectivamente recursos en Dynamic Media o Adobe Experience Manager, mutuamente excluyentes entre sí, utilizando **[!UICONTROL Publicación selectiva]** en el nivel de carpeta. Consulte [Trabajar con publicación selectiva en Dynamic Media](/help/assets/dynamic-media/selective-publishing.md).

En el **[!UICONTROL Vista de tarjeta]**, aparece un pequeño icono de globo terráqueo directamente debajo del nombre de un recurso y a la izquierda de la fecha y la hora para indicar que se ha publicado. En la **[!UICONTROL vista de lista]**, una columna **[!UICONTROL Publicada]** indica qué recursos se publican o cuáles no.

>[!NOTE]
>
>Si un recurso ya está publicado, mueva el recurso a otra carpeta y vuelva a publicarlo desde su nueva ubicación, la ubicación del recurso publicado original seguirá estando disponible, junto con el recurso recién republicado. Sin embargo, el recurso publicado original se &quot;pierde&quot; para el Experience Manager y no se puede cancelar su publicación. Por lo tanto, se recomienda cancelar la publicación de los recursos primero antes de moverlos a una carpeta diferente.

Si tiene intención de publicar recursos de vídeo inmediatamente después de codificarlos, asegúrese de que la codificación esté completa. Cuando se codifican vídeos, el sistema le permite saber que hay un flujo de trabajo de procesamiento de vídeo en curso. Cuando haya terminado la codificación de vídeo, puede obtener una vista previa de las representaciones de vídeo. En este punto, es seguro que publique los vídeos sin incurrir en errores de publicación.

Consulte también [Vincular URL a la aplicación web](linking-urls-to-yourwebapplication.md).

Consulte también [Incrustar el visor de vídeo de Dynamic Media o el visor de imágenes en una página web](embed-code.md).

>[!NOTE]
>
>* Los recursos deben publicarse para utilizar la dirección URL. Si los recursos no se publican, copiar y pegar la URL en un explorador web no funciona.
>* Los ajustes preestablecidos de imagen y los ajustes preestablecidos de visualizador deben activarse y publicarse para que se puedan publicar en directo.
>


Para obtener información detallada sobre la publicación de un conjunto o un recurso, consulte [Publicación de recursos](/help/assets/manage-digital-assets.md).

## Entrega HTTP/2 de recursos de Dynamic Media {#http-delivery-of-dynamic-media-assets}

Ahora, el Experience Manager admite la entrega de todo el contenido de Dynamic Media (imágenes y vídeo) a través de HTTP/2. Es decir, una URL publicada o un código incrustado para la imagen o el vídeo están disponibles para integrarse con cualquier aplicación que acepte un recurso alojado. Ese recurso publicado se entrega mediante el protocolo HTTP/2. Este método de envío mejora la forma en que se comunican los exploradores y los servidores, lo que permite mejorar los tiempos de respuesta y carga de todos los recursos de Dynamic Media.

Consulte [Entrega HTTP/2 de contenido preguntas más frecuentes](/help/assets/dynamic-media/http2faq.md).

<!--this md file used to reside under sites-administering-->
