---
title: Incrustar el visualizador de imágenes o vídeos de Dynamic Media en una página web
description: Obtenga información sobre cómo incrustar recursos de vídeo o imagen de Dynamic Media en una página web.
contentOwner: Rick Brough
feature: Asset Management
role: User
exl-id: 76335781-e39f-4aae-967f-5af8634d8f61
source-git-commit: b37ff72dbcf85e5558eb3421b5168dc48e063b47
workflow-type: tm+mt
source-wordcount: '375'
ht-degree: 21%

---

# Incrustar Dynamic Media Video, el visualizador de imágenes o el visualizador dimensional en una página web {#embedding-the-video-or-image-viewer-on-a-web-page}

Utilice la función **[!UICONTROL Código incrustado]** cuando desee reproducir el vídeo o ver un recurso incrustado en una página web. El código incrustado se copia en el portapapeles para pegarlo en las páginas web. No se permite la edición del código en el cuadro de diálogo **[!UICONTROL Código incrustado]**.

Las direcciones URL incrustadas solo se realizan si _no_ uso de Adobe Experience Manager como WCM. Si utiliza Experience Manager como WCM, [los recursos se agregan directamente en la página](adding-dynamic-media-assets-to-pages.md).

Consulte [Vinculación de URL en la aplicación web](linking-urls-to-yourwebapplication.md).

Consulte [Distribución de imágenes optimizadas para un sitio adaptable](responsive-site.md).

>[!NOTE]
>
>El código incrustado no está disponible para copiar hasta que haya publicado el recurso seleccionado. Además, también debe publicar el ajuste preestablecido de visualizador o de imagen.
>
>Consulte [Publicar recursos](publishing-dynamicmedia-assets.md).
>
>Consulte [Publicar ajustes preestablecidos del visor](managing-viewer-presets.md#publishing-viewer-presets).
>
>Consulte [Publicar ajustes preestablecidos de imagen](managing-image-presets.md#publishing-image-presets).

**Para incrustar el visualizador de imágenes o vídeos de Dynamic Media en una página web:**

1. Vaya a *publicado* recurso de vídeo o imagen cuyo código incrustado desee copiar.

   Recuerde que el código incrustado solo está disponible para copiar *después* de *publicar* los recursos por primera vez. Además, también se debe publicar el ajuste preestablecido de visualizador o de imagen.

   Consulte [Publicar recursos](publishing-dynamicmedia-assets.md).

   Consulte [Publicar ajustes preestablecidos del visor](managing-viewer-presets.md#publishing-viewer-presets).

   Consulte [Publicar ajustes preestablecidos de imagen](managing-image-presets.md#publishing-image-presets).

1. En el carril izquierdo, seleccione la lista desplegable y seleccione **[!UICONTROL Espectadores]**.
1. En el carril izquierdo, seleccione un nombre de ajuste preestablecido de visualizador. El ajuste preestablecido de visualizador se aplica al recurso.
1. Seleccionar **[!UICONTROL Incrustar]**.
1. En el **[!UICONTROL Código incrustado]** , copie todo el código en el portapapeles y seleccione **[!UICONTROL Cerrar]**.
1. Pegue el código incrustado en las páginas web.

## Utilice HTTP/2 para enviar los recursos de Dynamic Media {#using-http-to-deliver-your-dynamic-media-assets}

HTTP/2 es el nuevo protocolo web actualizado que mejora la forma en que los exploradores y servidores se comunican. Proporciona una transferencia de información más rápida y reduce la cantidad de potencia de procesamiento necesaria. La entrega de recursos de Dynamic Media ahora se puede realizar a través de HTTP/2, que proporciona mejores tiempos de respuesta y carga.

Consulte [Entrega HTTP2 de contenido](http2faq.md) para obtener información detallada sobre cómo empezar a utilizar HTTP/2 con su cuenta de Dynamic Media.
