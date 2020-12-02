---
title: Incrustación del visor de vídeo o de imagen de Dynamic Media en una página web
description: Obtenga información sobre cómo incrustar vídeos o imágenes de Dynamic Media en una página web
translation-type: tm+mt
source-git-commit: 7dae5c0ed82687415719cd2d72f98028cf0a8e64
workflow-type: tm+mt
source-wordcount: '371'
ht-degree: 22%

---


# Incrustación del vídeo de Dynamic Media, el visor de imágenes o el visor de dimensiones en una página web {#embedding-the-video-or-image-viewer-on-a-web-page}

Utilice la función **[!UICONTROL Código incrustado]** cuando desee reproducir el vídeo o ver un recurso incrustado en una página web. El código incrustado se copia en el portapapeles para pegarlo en las páginas web. No se permite la edición del código en el cuadro de diálogo **[!UICONTROL Código incrustado]**.

Las direcciones URL solo se incrustan si _no_ utiliza AEM como WCM. Si está utilizando AEM como WCM, [agregue los recursos directamente en la página.](adding-dynamic-media-assets-to-pages.md)

Consulte [Vinculación de direcciones URL a la Aplicación web.](linking-urls-to-yourwebapplication.md)

Consulte [Entrega de imágenes optimizadas para un sitio interactivo.](responsive-site.md)

>[!NOTE]
>
>El código incrustado no está disponible para copiar hasta que haya publicado el recurso seleccionado. Además, también debe publicar el ajuste preestablecido de visor o el ajuste preestablecido de imagen.
>
>Consulte [Publishing Assets](publishing-dynamicmedia-assets.md).
>
>Consulte [Ajustes preestablecidos de visor de publicaciones](managing-viewer-presets.md#publishing-viewer-presets).
>
>Consulte [Ajustes preestablecidos de imagen de publicación](managing-image-presets.md#publishing-image-presets).

**Incrustación del visor de vídeo o de imagen de Dynamic Media en una página web**

1. Vaya al *recurso de imagen o vídeo publicado* cuyo código incrustado desee copiar.

   Recuerde que el código incrustado solo está disponible para copiar *después* de *publicar* los recursos por primera vez. Además, también se debe publicar el ajuste preestablecido de visualizador o de imagen.

   Consulte [Publishing Assets.](publishing-dynamicmedia-assets.md)

   Consulte [Ajustes preestablecidos de visor de publicaciones](managing-viewer-presets.md#publishing-viewer-presets).

   Consulte [Ajustes preestablecidos de imagen de publicación](managing-image-presets.md#publishing-image-presets).

1. En el carril izquierdo, seleccione el menú desplegable y toque **[!UICONTROL Visores]**.
1. En el carril izquierdo, toque un nombre de ajuste preestablecido de visor. El ajuste preestablecido de visor se aplica al recurso.
1. Toque **[!UICONTROL Incrustar]**.
1. En el cuadro de diálogo **[!UICONTROL Código incrustado]**, copie el código completo en el portapapeles y, a continuación, toque **[!UICONTROL Cerrar]**.
1. Pegue el código incrustado en las páginas web.

## Uso de HTTP/2 para distribuir los recursos de Dynamic Media {#using-http-to-deliver-your-dynamic-media-assets}

HTTP/2 es el nuevo protocolo web actualizado que mejora la forma en que se comunican los exploradores y los servidores. Proporciona una transferencia de información más rápida y reduce la cantidad de potencia de procesamiento necesaria. Ahora, el envío de recursos de Dynamic Media puede realizarse a través de HTTP/2, lo que proporciona una mejor respuesta y tiempos de carga.

Consulte [Envío HTTP2 de contenido](http2faq.md) para obtener información detallada sobre cómo empezar a utilizar HTTP/2 con su cuenta de Dynamic Media.
