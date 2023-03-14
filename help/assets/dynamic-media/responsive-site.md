---
title: Distribución de imágenes optimizadas para un sitio adaptable
description: Aprenda a utilizar la función de código interactivo para ofrecer imágenes optimizadas de Dynamic Media.
contentOwner: Rick Brough
feature: Asset Management
role: User
exl-id: 62af6f3f-9c86-44ad-870d-140f572f99c5
source-git-commit: b37ff72dbcf85e5558eb3421b5168dc48e063b47
workflow-type: tm+mt
source-wordcount: '326'
ht-degree: 15%

---

# Distribución de imágenes optimizadas para un sitio adaptable {#delivering-optimized-images-for-a-responsive-site}

Utilice la función de código interactivo cuando desee compartir el código para un servicio interactivo con el desarrollador web. Puede copiar el archivo adaptable (**[!UICONTROL RESS]**) código en el portapapeles para poder compartirlo con el desarrollador web.

Esta función tiene sentido si el sitio web se encuentra en un WCM de terceros. Sin embargo, si el sitio web se encuentra en Adobe Experience Manager, un servidor de imágenes fuera del sitio procesará la imagen y la enviará a la página web.

Consulte también [Incrustar el Visor de vídeo en una página web](embed-code.md).

Consulte también [Vinculación de URL en la aplicación web](linking-urls-to-yourwebapplication.md).

**Para ofrecer imágenes optimizadas para un sitio interactivo:**

1. Vaya a la imagen para la que desee proporcionar código interactivo y, en el menú desplegable, seleccione **[!UICONTROL Representaciones]**.

   ![chlimage_1-408](assets/chlimage_1-408.png)

1. Seleccione un ajuste preestablecido de imagen interactivo. Aparecerán los botones **[!UICONTROL URL]** y **[!UICONTROL RESS]**.

   ![chlimage_1-409](assets/chlimage_1-409.png)

   >[!NOTE]
   >
   >El recurso seleccionado *y* el ajuste preestablecido de imagen o visualizador seleccionado deben publicarse para que los botones **[!UICONTROL URL]** o **[!UICONTROL RESS]** estén disponibles.
   >
   >Los ajustes preestablecidos de imagen se publican automáticamente.

1. Seleccionar **[!UICONTROL RESS]**.

   ![chlimage_1-410](assets/chlimage_1-410.png)

1. En el **[!UICONTROL Incrustar imagen adaptable]** , seleccione, copie el texto del código adaptable y péguelo en su sitio web para acceder al recurso adaptable.
1. Edite los puntos de interrupción predeterminados en el código incrustado para que coincidan con lo que se encuentra en el sitio web adaptable directamente en el código. Además, pruebe las diferentes resoluciones de imagen que se proporcionan en diferentes puntos de interrupción de página.

## Uso de HTTP/2 para enviar los recursos de Dynamic Media {#using-http-to-delivery-your-dynamic-media-assets}

HTTP/2 es el nuevo protocolo web actualizado que mejora la forma en que los exploradores y servidores se comunican. Proporciona una transferencia de información más rápida y reduce la cantidad de potencia de procesamiento necesaria. La entrega de recursos de Dynamic Media se admite mediante HTTP/2, que proporciona mejores tiempos de respuesta y carga.

Consulte [Entrega HTTP2 de contenido](http2faq.md) para obtener información detallada sobre cómo empezar a utilizar HTTP/2 con su cuenta de Dynamic Media.
