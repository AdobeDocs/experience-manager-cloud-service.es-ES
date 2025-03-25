---
title: Proporcione Dynamic Media Assets
description: Obtenga información sobre cómo enviar recursos de Dynamic Media a sus páginas web a través de imágenes y vídeos incrustados o vinculando direcciones URL a su aplicación web.
contentOwner: Rick Brough
feature: Asset Management
role: User
exl-id: 4557b561-b3c4-4d6f-8044-2069bda41613
source-git-commit: 36ab36ba7e14962eba3947865545b8a3f29f6bbc
workflow-type: tm+mt
source-wordcount: '339'
ht-degree: 7%

---

# Proporcione Dynamic Media Assets{#delivering-dynamic-media-assets}

La forma de entregar los recursos de Dynamic Media, tanto de vídeo como de imágenes, depende de cómo se implemente el sitio web.

Con Dynamic Media, tiene varias opciones:

* Si el sitio web está alojado en Adobe Experience Manager, quiere añadir los recursos de Dynamic Media directamente a la página.
* Si el sitio web no está en Experience Manager, puede elegir una de estas opciones:

   * Incrustar el vídeo o la imagen en el sitio web.
   * Vincule las URL a la aplicación web. Utilice la vinculación cuando desee distribuir un reproductor de vídeo como ventana emergente o modal.
   * Si tu sitio es interactivo, puedes [ofrecer imágenes optimizadas](/help/assets/dynamic-media/responsive-site.md).

>[!NOTE]
>
>Las imágenes inteligentes funcionan con los ajustes preestablecidos de imagen existentes. Utiliza inteligencia en el último milisegundo de envío para reducir aún más el tamaño del archivo de imagen en función de la velocidad de conexión del explorador o de la red. Consulte [Imágenes inteligentes](/help/assets/dynamic-media/imaging-faq.md) para obtener más información.

Para obtener más información, consulte los temas siguientes:

* [Agregar Dynamic Media Assets a las páginas web](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md)
* [Incrustar el visor de vídeo o de imágenes en una página web](/help/assets/dynamic-media/embed-code.md)
* [Activación de la protección de enlaces interactivos en Dynamic Media](/help/assets/dynamic-media/hotlink-protection.md)
* [Vinculación de URL en la aplicación web](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md)
* [Distribución de imágenes optimizadas para un sitio adaptable](/help/assets/dynamic-media/responsive-site.md)
* [Entrega HTTP2 de contenido](/help/assets/dynamic-media/http2faq.md)
* [Invalidación de la caché de CDN mediante Dynamic Media](/help/assets/dynamic-media/invalidate-cdn-cache-dynamic-media.md)
* [Invalidación de la caché de CDN mediante Dynamic Media Classic](/help/assets/dynamic-media/invalidate-cdn-cache-dm-classic.md)
* [Uso de conjuntos de reglas para transformar URL](/help/assets/dynamic-media/using-rulesets-to-transform-urls.md)

## Entrega HTTP/2 de recursos de Dynamic Media {#http-delivery-of-dynamic-media-assets}

Experience Manager ahora admite la entrega de todo el contenido de Dynamic Media (imágenes y vídeo) a través de HTTP/2. Es decir, hay disponible una URL publicada o código incrustado para la imagen o el vídeo que se va a integrar con cualquier aplicación que acepte un recurso alojado. Ese recurso publicado se entrega mediante el protocolo HTTP/2. Este método de envío mejora la forma en que los exploradores y servidores se comunican, lo que permite una mejor respuesta y tiempos de carga de todos los recursos de Dynamic Media.

Para obtener más información, consulte [Preguntas más frecuentes sobre la entrega de contenido HTTP/2](/help/assets/dynamic-media/http2faq.md).
