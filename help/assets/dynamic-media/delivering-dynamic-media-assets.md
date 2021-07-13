---
title: Enviar recursos de Dynamic Media
description: Obtenga información sobre cómo distribuir recursos de Dynamic Media.
feature: Administración de activos
role: User
exl-id: 4557b561-b3c4-4d6f-8044-2069bda41613
source-git-commit: 6933f053e11320d8201922723879983084c52209
workflow-type: tm+mt
source-wordcount: '321'
ht-degree: 2%

---

# Enviar recursos de Dynamic Media{#delivering-dynamic-media-assets}

El modo de distribuir los recursos de Dynamic Media (vídeos e imágenes) depende de cómo se implemente el sitio web.

Con Dynamic Media, tiene varias opciones:

* Si el sitio web está alojado en Adobe Experience Manager, quiere agregar los recursos de Dynamic Media directamente a la página.
* Si el sitio web no está en Experience Manager, puede elegir una de las opciones siguientes:

   * Incrustar el vídeo o la imagen en el sitio web.
   * Vincule las URL a la aplicación web. Utilice la vinculación cuando desee enviar un reproductor de vídeo como ventana emergente o modal.
   * Si su sitio es interactivo, puede [entregar imágenes optimizadas](/help/assets/dynamic-media/responsive-site.md).

>[!NOTE]
>
>Las imágenes inteligentes funcionan con los ajustes preestablecidos de imagen existentes. Utiliza inteligencia en el último milisegundo de envío para reducir aún más el tamaño del archivo de imagen en función de la velocidad de conexión de red o del explorador. Consulte [Imágenes inteligentes](/help/assets/dynamic-media/imaging-faq.md) para obtener más información.

Para obtener más información, consulte los temas siguientes:

* [Agregar recursos de Dynamic Media a páginas web](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md)
* [Incrustar el visualizador de imágenes o vídeos en una página web](/help/assets/dynamic-media/embed-code.md)
* [Activar la protección de los vínculos interactivos en Dynamic Media](/help/assets/dynamic-media/hotlink-protection.md)
* [Vincular URL a la aplicación web](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md)
* [Entregar imágenes optimizadas para un sitio interactivo](/help/assets/dynamic-media/responsive-site.md)
* [Entrega HTTP2 de contenido](/help/assets/dynamic-media/http2faq.md)
* [Invalidar la caché de CDN mediante Dynamic Media](/help/assets/dynamic-media/invalidate-cdn-cache-dynamic-media.md)
* [Invalidar la caché de CDN mediante Dynamic Media Classic](/help/assets/dynamic-media/invalidate-cdn-cache-dm-classic.md)
* [Usar conjuntos de reglas para transformar direcciones URL](/help/assets/dynamic-media/using-rulesets-to-transform-urls.md)

## Entrega HTTP/2 de recursos de Dynamic Media {#http-delivery-of-dynamic-media-assets}

Ahora, el Experience Manager admite la entrega de todo el contenido de Dynamic Media (imágenes y vídeo) a través de HTTP/2. Es decir, una URL publicada o un código incrustado para la imagen o el vídeo están disponibles para integrarse con cualquier aplicación que acepte un recurso alojado. Ese recurso publicado se entrega mediante el protocolo HTTP/2. Este método de envío mejora la forma en que se comunican los exploradores y los servidores, lo que permite mejorar los tiempos de respuesta y carga de todos los recursos de Dynamic Media.

Para obtener más información, consulte [HTTP/2 Entrega de contenido preguntas más frecuentes](/help/assets/dynamic-media/http2faq.md).
