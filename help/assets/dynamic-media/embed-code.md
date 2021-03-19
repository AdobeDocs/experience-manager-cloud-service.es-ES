---
title: Incrustación del visualizador de imágenes o vídeos de Dynamic Media en una página web
description: Aprenda a incrustar recursos de imagen o vídeo de Dynamic Media en una página web.
feature: Administración de activos
topic: Profesional empresarial
translation-type: tm+mt
source-git-commit: 0f2b7176b44bb79bdcd1cecf6debf05bd652a1a1
workflow-type: tm+mt
source-wordcount: '376'
ht-degree: 21%

---


# Incrustación del vídeo de Dynamic Media, el visor de imágenes o el visor dimensional en una página web {#embedding-the-video-or-image-viewer-on-a-web-page}

Utilice la función **[!UICONTROL Código incrustado]** cuando desee reproducir el vídeo o ver un recurso incrustado en una página web. El código incrustado se copia en el portapapeles para pegarlo en las páginas web. No se permite la edición del código en el cuadro de diálogo **[!UICONTROL Código incrustado]**.

Las direcciones URL incrustadas solo se pueden incrustar si está _no_ usando AEM como WCM. Si utiliza AEM como WCM, [los recursos se añaden directamente en la página.](adding-dynamic-media-assets-to-pages.md)

Consulte [Vinculación de URL a la aplicación web.](linking-urls-to-yourwebapplication.md)

Consulte [Entrega de imágenes optimizadas para un sitio interactivo.](responsive-site.md)

>[!NOTE]
>
>El código incrustado no está disponible para copiar hasta que no haya publicado el recurso seleccionado. Además, también debe publicar el ajuste preestablecido de visualizador o de imagen.
>
>Consulte [Publicación de recursos](publishing-dynamicmedia-assets.md).
>
>Consulte [Ajustes preestablecidos del visualizador de publicaciones](managing-viewer-presets.md#publishing-viewer-presets).
>
>Consulte [Publicar ajustes preestablecidos de imagen](managing-image-presets.md#publishing-image-presets).

**Incrustación del visualizador de imágenes o vídeos de Dynamic Media en una página web**

1. Vaya al vídeo o recurso de imagen *publicado* cuyo código incrustado desee copiar.

   Recuerde que el código incrustado solo está disponible para copiar *después* de *publicar* los recursos por primera vez. Además, también se debe publicar el ajuste preestablecido de visualizador o de imagen.

   Consulte [Publicación de recursos.](publishing-dynamicmedia-assets.md)

   Consulte [Ajustes preestablecidos del visualizador de publicaciones](managing-viewer-presets.md#publishing-viewer-presets).

   Consulte [Publicar ajustes preestablecidos de imagen](managing-image-presets.md#publishing-image-presets).

1. En el carril izquierdo, seleccione la lista desplegable y pulse **[!UICONTROL Visualizadores]**.
1. En el carril izquierdo, pulse un nombre de ajuste preestablecido de visualizador. El ajuste preestablecido de visualizador se aplica al recurso.
1. Pulse **[!UICONTROL Incrustar]**.
1. En el cuadro de diálogo **[!UICONTROL Código incrustado]**, copie todo el código en el portapapeles y, a continuación, pulse **[!UICONTROL Cerrar]**.
1. Pegue el código incrustado en las páginas web.

## Uso de HTTP/2 para enviar los recursos de Dynamic Media {#using-http-to-deliver-your-dynamic-media-assets}

HTTP/2 es el nuevo protocolo web actualizado que mejora la forma en que se comunican los exploradores y los servidores. Proporciona una transferencia de información más rápida y reduce la cantidad de potencia de procesamiento necesaria. La entrega de recursos de Dynamic Media ahora puede realizarse a través de HTTP/2, lo que proporciona una mejor respuesta y tiempos de carga.

Consulte [Entrega HTTP2 de contenido](http2faq.md) para obtener información detallada sobre cómo empezar a utilizar HTTP/2 con su cuenta de Dynamic Media.
