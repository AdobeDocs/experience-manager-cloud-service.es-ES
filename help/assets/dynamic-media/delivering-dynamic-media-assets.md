---
title: Entrega de recursos de Dynamic Media
description: Obtenga información sobre cómo entregar recursos de Dynamic Media.
contentOwner: Rick Brough
feature: Asset Management
role: User
exl-id: 4557b561-b3c4-4d6f-8044-2069bda41613
source-git-commit: b37ff72dbcf85e5558eb3421b5168dc48e063b47
workflow-type: tm+mt
source-wordcount: '319'
ht-degree: 11%

---

# Entrega de recursos de Dynamic Media{#delivering-dynamic-media-assets}

La forma de distribuir los recursos de Dynamic Media, tanto de vídeo como de imágenes, depende de la implementación del sitio web.

Con Dynamic Media, tiene varias opciones:

* Si el sitio web está alojado en Adobe Experience Manager, quiere añadir los recursos de Dynamic Media directamente a la página.
* Si el sitio web no está en el Experience Manager, puede elegir una de estas opciones:

   * Incrustar el vídeo o la imagen en el sitio web.
   * Vinculación de URL en la aplicación web. Utilice la vinculación cuando desee distribuir un reproductor de vídeo como ventana emergente o modal.
   * Si su sitio es adaptable, puede hacer lo siguiente [ofrecer imágenes optimizadas](/help/assets/dynamic-media/responsive-site.md).

>[!NOTE]
>
>Las imágenes inteligentes funcionan con los ajustes preestablecidos de imagen existentes. Utiliza inteligencia en el último milisegundo de envío para reducir aún más el tamaño del archivo de imagen en función de la velocidad de conexión del explorador o de la red. Consulte [Imágenes inteligentes](/help/assets/dynamic-media/imaging-faq.md) para obtener más información.

Para obtener más información, consulte los temas siguientes:

* [Agregar recursos de Dynamic Media a páginas web](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md)
* [Incrustar el visor de vídeo o de imágenes en una página web](/help/assets/dynamic-media/embed-code.md)
* [Activación de la protección de enlaces interactivos en Dynamic Media](/help/assets/dynamic-media/hotlink-protection.md)
* [Vinculación de URL en la aplicación web](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md)
* [Distribución de imágenes optimizadas para un sitio adaptable](/help/assets/dynamic-media/responsive-site.md)
* [Entrega HTTP2 de contenido](/help/assets/dynamic-media/http2faq.md)
* [Invalidación de la caché de CDN mediante Dynamic Media](/help/assets/dynamic-media/invalidate-cdn-cache-dynamic-media.md)
* [Invalidación de la caché de CDN mediante Dynamic Media Classic](/help/assets/dynamic-media/invalidate-cdn-cache-dm-classic.md)
* [Uso de conjuntos de reglas para transformar URL](/help/assets/dynamic-media/using-rulesets-to-transform-urls.md)

## Envío HTTP/2 de recursos de Dynamic Media {#http-delivery-of-dynamic-media-assets}

Experience Manager ahora admite la entrega de todo el contenido de Dynamic Media (imágenes y vídeo) a través de HTTP/2. Es decir, hay disponible una URL publicada o código incrustado para la imagen o el vídeo que se va a integrar con cualquier aplicación que acepte un recurso alojado. Ese recurso publicado se entrega mediante el protocolo HTTP/2. Este método de entrega mejora la forma en que los navegadores y servidores se comunican, lo que permite una mejor respuesta y tiempos de carga de todos los recursos de Dynamic Media.

Para obtener más información, consulte [Entrega HTTP/2 de preguntas más frecuentes sobre contenido](/help/assets/dynamic-media/http2faq.md).
