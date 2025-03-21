---
title: Distribución de imágenes optimizadas para un sitio adaptable
description: Aprenda a utilizar la función de código interactivo para ofrecer imágenes optimizadas de Dynamic Media.
contentOwner: Rick Brough
feature: Asset Management
role: User
exl-id: 62af6f3f-9c86-44ad-870d-140f572f99c5
source-git-commit: c82f84fe99d8a196adebe504fef78ed8f0b747a9
workflow-type: tm+mt
source-wordcount: '378'
ht-degree: 17%

---

# Distribución de imágenes optimizadas para un sitio adaptable {#delivering-optimized-images-for-a-responsive-site}

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

Utilice la función de código interactivo cuando desee compartir el código para un servicio interactivo con el desarrollador web. Copia el código interactivo (**[!UICONTROL RESS]**) en el portapapeles para poder compartirlo con el desarrollador web.

Esta función tiene sentido si el sitio web se encuentra en un WCM de terceros. Sin embargo, si el sitio web se encuentra en Adobe Experience Manager, un servidor de imágenes fuera del sitio procesará la imagen y la enviará a la página web.

Consulte también [Incrustar el visor de vídeo en una página web](embed-code.md).

Ver también [URL de vínculo a su aplicación web](linking-urls-to-yourwebapplication.md).

**Para ofrecer imágenes optimizadas para un sitio adaptable:**

1. Vaya a la imagen para la que desee proporcionar código interactivo y, en el menú desplegable, seleccione **[!UICONTROL Representaciones]**.

   ![chlimage_1-408](assets/chlimage_1-408.png)

1. Seleccione un ajuste preestablecido de imagen interactivo. Aparecerán los botones **[!UICONTROL URL]** y **[!UICONTROL RESS]**.

   ![chlimage_1-409](assets/chlimage_1-409.png)

   >[!NOTE]
   >
   >El recurso seleccionado *y* el ajuste preestablecido de imagen o visualizador seleccionado deben publicarse para que los botones **[!UICONTROL URL]** o **[!UICONTROL RESS]** estén disponibles.
   >
   >Los ajustes preestablecidos de imagen se publican automáticamente.

1. Seleccione **[!UICONTROL RESS]**.

   ![chlimage_1-410](assets/chlimage_1-410.png)

1. En el cuadro de diálogo **[!UICONTROL Incrustar imagen adaptable]**, seleccione, copie el texto del código adaptable y péguelo en su sitio web para acceder al recurso adaptable.
1. Edite los puntos de interrupción predeterminados en el código incrustado para que coincidan con lo que se encuentra en el sitio web adaptable directamente en el código. Además, pruebe las diferentes resoluciones de imagen que se proporcionan en diferentes puntos de interrupción de página.

## Uso de HTTP/2 para enviar los recursos de Dynamic Media {#using-http-to-delivery-your-dynamic-media-assets}

HTTP/2 es el nuevo protocolo web actualizado que mejora la forma en que los exploradores y servidores se comunican. Proporciona una transferencia de información más rápida y reduce la cantidad de potencia de procesamiento necesaria. La entrega de recursos de Dynamic Media se admite mediante HTTP/2, que proporciona mejores tiempos de respuesta y carga.

Consulte [Entrega HTTP2 de contenido](http2faq.md) para obtener información detallada sobre cómo empezar a usar HTTP/2 con su cuenta de Dynamic Media.
