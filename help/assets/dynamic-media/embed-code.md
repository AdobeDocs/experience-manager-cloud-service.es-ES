---
title: Incrustar Dynamic Media Video o el visualizador de imágenes en una página web
description: Obtenga información sobre cómo incrustar recursos de vídeo o imagen de Dynamic Media en una página web.
contentOwner: Rick Brough
feature: Asset Management
role: User
exl-id: 76335781-e39f-4aae-967f-5af8634d8f61
source-git-commit: c82f84fe99d8a196adebe504fef78ed8f0b747a9
workflow-type: tm+mt
source-wordcount: '424'
ht-degree: 23%

---

# Incrustar Dynamic Media Video, el visualizador de imágenes o el visualizador dimensional en una página web {#embedding-the-video-or-image-viewer-on-a-web-page}

<table>
    <tr>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nuevo</i></sup> <a href="/help/assets/dynamic-media/dm-prime-ultimate.md"><b>Dynamic Media Prime y Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nuevo</i></sup> <a href="/help/assets/assets-ultimate-overview.md"><b>AEM Assets Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nueva</i></sup> integración de <a href="/help/assets/integrate-aem-assets-edge-delivery-services.md"><b>AEM Assets con Edge Delivery Services</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nueva</i></sup> <a href="/help/assets/aem-assets-view-ui-extensibility.md"><b>extensibilidad de la interfaz de usuario</b></a>
        </td>
          <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nuevo</i></sup> <a href="/help/assets/dynamic-media/enable-dynamic-media-prime-and-ultimate.md"><b>Habilitar Dynamic Media Prime y Ultimate</b></a>
        </td>
    </tr>
    <tr>
        <td>
            <a href="/help/assets/search-best-practices.md"><b>Prácticas recomendadas de búsqueda</b></a>
        </td>
        <td>
            <a href="/help/assets/metadata-best-practices.md"><b>Prácticas recomendadas de metadatos</b></a>
        </td>
        <td>
            <a href="/help/assets/product-overview.md"><b>Centro de contenido</b></a>
        </td>
        <td>
            <a href="/help/assets/dynamic-media-open-apis-overview.md"><b>Dynamic Media con funciones de OpenAPI</b></a>
        </td>
        <td>
            <a href="https://developer.adobe.com/experience-cloud/experience-manager-apis/"><b>Documentación de desarrollador de AEM Assets</b></a>
        </td>
    </tr>
</table>

Utilice la función **[!UICONTROL Código incrustado]** cuando desee reproducir el vídeo o ver un recurso incrustado en una página web. El código incrustado se copia en el portapapeles para pegarlo en las páginas web. No se permite la edición del código en el cuadro de diálogo **[!UICONTROL Código incrustado]**.

Solo puede incrustar direcciones URL si _no_ usa Adobe Experience Manager como WCM. Si usa Experience Manager como WCM, [agrega los recursos directamente en la página](adding-dynamic-media-assets-to-pages.md).

Ver [URL de vínculo a su aplicación web](linking-urls-to-yourwebapplication.md).

Ver [Enviar imágenes optimizadas para un sitio adaptable](responsive-site.md).

>[!NOTE]
>
>El código incrustado no está disponible para copiar hasta que haya publicado el recurso seleccionado. Además, también debe publicar el ajuste preestablecido de visualizador o de imagen.
>
>Ver [Publicar Assets](publishing-dynamicmedia-assets.md).
>
>Consulte [Publicar ajustes preestablecidos del visor](managing-viewer-presets.md#publishing-viewer-presets).
>
>Consulte [Publicar ajustes preestablecidos de imagen](managing-image-presets.md#publishing-image-presets).

**Para incrustar el visualizador de imágenes o vídeos de Dynamic Media en una página web:**

1. Vaya al vídeo o recurso de imagen *publicado* cuyo código incrustado desee copiar.

   Recuerde que el código incrustado solo está disponible para copiar *después* de *publicar* los recursos por primera vez. Además, también se debe publicar el ajuste preestablecido de visualizador o de imagen.

   Ver [Publicar Assets](publishing-dynamicmedia-assets.md).

   Consulte [Publicar ajustes preestablecidos del visor](managing-viewer-presets.md#publishing-viewer-presets).

   Consulte [Publicar ajustes preestablecidos de imagen](managing-image-presets.md#publishing-image-presets).

1. En el carril izquierdo, seleccione la lista desplegable y seleccione **[!UICONTROL Visualizadores]**.
1. En el carril izquierdo, seleccione un nombre de ajuste preestablecido de visualizador. El ajuste preestablecido de visualizador se aplica al recurso.
1. Seleccionar **[!UICONTROL Incrustar]**.
1. En el cuadro de diálogo **[!UICONTROL Código incrustado]**, copie todo el código en el portapapeles y, a continuación, seleccione **[!UICONTROL Cerrar]**.
1. Pegue el código incrustado en las páginas web.

## Utilice HTTP/2 para entregar los recursos de Dynamic Media {#using-http-to-deliver-your-dynamic-media-assets}

HTTP/2 es el nuevo protocolo web actualizado que mejora la forma en que los exploradores y servidores se comunican. Proporciona una transferencia de información más rápida y reduce la cantidad de potencia de procesamiento necesaria. La entrega de recursos de Dynamic Media ahora se puede realizar a través de HTTP/2, que proporciona mejores tiempos de respuesta y carga.

Consulte [Entrega HTTP2 de contenido](http2faq.md) para obtener información detallada sobre cómo empezar a usar HTTP/2 con su cuenta de Dynamic Media.
