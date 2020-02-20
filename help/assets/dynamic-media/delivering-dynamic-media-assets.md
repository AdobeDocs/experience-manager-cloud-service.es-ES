---
title: Envío de recursos de Dynamic Media
description: Aprenda a distribuir recursos de medios dinámicos
translation-type: tm+mt
source-git-commit: 218afb360ec3a13f2f4562a703ca3184083fa7f6

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
>Las imágenes inteligentes funcionan con los ajustes preestablecidos de imagen existentes y utilizan la inteligencia en el último milisegundo de la publicación para reducir aún más el tamaño del archivo de imagen en función de la velocidad de conexión de red o del navegador. Consulte Imágenes [inteligentes](/help/assets/dynamic-media/imaging-faq.md) para obtener más información.

Para obtener más información, consulte los temas siguientes:

* [Adición de recursos de Dynamic Media a páginas Web](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md)
* [Incrustación del visor de imágenes o vídeos en una página web](/help/assets/dynamic-media/embed-code.md)
* [Activación de la protección de los enlaces interactivos en Dynamic Media](/help/assets/dynamic-media/hotlink-protection.md)
* [Vinculación de direcciones URL a la aplicación web](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md)
* [Envío de imágenes optimizadas para un sitio interactivo](/help/assets/dynamic-media/responsive-site.md)
* [Envío de contenido HTTP2](/help/assets/dynamic-media/http2faq.md)
* [Invalidación del contenido en caché de CDN](/help/assets/dynamic-media/invalidate-cdn-cached-content.md)
* [Uso de conjuntos de reglas para transformar direcciones URL](/help/assets/dynamic-media/using-rulesets-to-transform-urls.md)

## Entrega HTTP/2 de recursos de Dynamic Media {#http-delivery-of-dynamic-media-assets}

AEM ahora admite la entrega de todo el contenido de Dynamic Media (imágenes y vídeo) a través de HTTP/2. Es decir, una URL publicada o código incrustado para la imagen o el vídeo está disponible para integrarse con cualquier aplicación que acepte un recurso alojado. Ese recurso publicado se entrega a través del protocolo HTTP/2. Este método de entrega mejora la forma en que se comunican los exploradores y los servidores, lo que permite una mejor respuesta y tiempos de carga de todos los recursos de Dynamic Media.

Consulte [HTTP/2 Entrega de contenido Preguntas](/help/assets/dynamic-media/http2faq.md) más frecuentes para obtener más información.
