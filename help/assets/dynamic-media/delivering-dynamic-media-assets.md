---
title: Envío de recursos de Dynamic Media
description: Aprenda a distribuir recursos de medios dinámicos
translation-type: tm+mt
source-git-commit: ea6a1bddaab6819d1f89268ceba3c4d4981729a2
workflow-type: tm+mt
source-wordcount: '315'
ht-degree: 15%

---


# Envío de recursos de Dynamic Media{#delivering-dynamic-media-assets}

El modo de distribuir los recursos de medios dinámicos, tanto de vídeo como de imágenes, depende de cómo se implemente el sitio web.

Con Dynamic Media dispone de varias opciones:

* Si el sitio web se aloja en AEM, lo más recomendable es añadir recursos de Dynamic Media directamente a la página.
* Si su sitio web no está en AEM, puede elegir entre:

   * Incrustación de vídeo o imagen en el sitio web.
   * Vincular direcciones URL a la aplicación web. Utilice la vinculación cuando desee distribuir un reproductor de vídeo como ventana emergente o modal.
   * Si el sitio responde, puede [entregar imágenes optimizadas.](/help/assets/dynamic-media/responsive-site.md)

>[!NOTE]
>
>Las imágenes inteligentes funcionan con los ajustes preestablecidos de imagen existentes y utilizan la inteligencia en el último milisegundo de envío para reducir aún más el tamaño del archivo de imagen en función de la velocidad de conexión de red o del navegador. Consulte Imágenes [inteligentes](/help/assets/dynamic-media/imaging-faq.md) para obtener más información.

Para obtener más información, consulte los temas siguientes:

* [Añadir recursos de Dynamic Media en páginas Web](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md)
* [Incrustación del visor de imágenes o vídeos en una página web](/help/assets/dynamic-media/embed-code.md)
* [Activar la protección de los vínculos interactivos de Dynamic Media](/help/assets/dynamic-media/hotlink-protection.md)
* [Vinculación de direcciones URL a la Aplicación web](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md)
* [Envío de imágenes optimizadas para un sitio interactivo](/help/assets/dynamic-media/responsive-site.md)
* [ENVÍO de contenido HTTP2](/help/assets/dynamic-media/http2faq.md)
* [Invalidación de la caché de CDN mediante Dynamic Media](/help/assets/dynamic-media/invalidate-cdn-cache-dynamic-media.md)
* [Invalidación de la caché de CDN mediante Dynamic Media Classic](/help/assets/dynamic-media/invalidate-cdn-cache-dm-classic.md)
* [Uso de conjuntos de reglas para transformar direcciones URL](/help/assets/dynamic-media/using-rulesets-to-transform-urls.md)

## ENVÍO HTTP/2 de recursos de Dynamic Media {#http-delivery-of-dynamic-media-assets}

AEM ahora admite el envío de todo el contenido de Dynamic Media (imágenes y vídeo) a través de HTTP/2. Es decir, una URL publicada o código incrustado para la imagen o el vídeo está disponible para integrarse con cualquier aplicación que acepte un recurso alojado. Ese recurso publicado se entrega a través del protocolo HTTP/2. Este método de envío mejora la forma en que se comunican los exploradores y los servidores, lo que permite una mejor respuesta y tiempos de carga de todos los recursos de Dynamic Media.

Consulte Envío [HTTP/2 de las preguntas](/help/assets/dynamic-media/http2faq.md) más frecuentes sobre el contenido para obtener más información.
