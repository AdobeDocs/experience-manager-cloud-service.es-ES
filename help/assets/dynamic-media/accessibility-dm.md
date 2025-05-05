---
title: Accesibilidad en Dynamic Media
description: Aprenda a trabajar con vídeo en Dynamic Media, como prácticas recomendadas para codificar vídeos, publicar vídeos en YouTube y ver informes de vídeo. También aprenderá a añadir subtítulos, subtítulos o marcadores de capítulo a los vídeos.
contentOwner: Rick Brough
topic-tags: introduction
content-type: reference
feature: Accessibility
role: Admin,User
exl-id: f8d2dcbf-f61a-4b27-a3fc-406e3662adcb
source-git-commit: 36ab36ba7e14962eba3947865545b8a3f29f6bbc
workflow-type: tm+mt
source-wordcount: '638'
ht-degree: 1%

---

# Accesibilidad en Dynamic Media {#accessibility-in-dm}

{{work-with-dynamic-media}}

Dynamic Media admite tecnologías de control de teclado y asistencia, como lectores de pantalla JAWS y NVDA, en la interfaz de usuario de creación.

## Compatibilidad de accesibilidad del teclado en Dynamic Media {#keyboard-support-in-dm}

Debido a que Dynamic Media es un complemento de [!DNL Experience Manager Assets], la mayor parte del comportamiento de control de teclado es el mismo que en [!DNL Experience Manager Assets]. Por ejemplo, el botón `Cancel` de Dynamic Media tiene el mismo resaltado de enfoque que en [!DNL Experience Manager Assets]. También reacciona a la clave `Spacebar` como en [!DNL Experience Manager Assets]. Ver [métodos abreviados de teclado en Assets](/help/assets/accessibility.md#keyboard-shortcuts).

Las pulsaciones de tecla admitidas por los elementos de la interfaz de usuario individual en Dynamic Media son, en la mayoría de los casos, obvias y fáciles de encontrar. El control de teclado en Dynamic Media es aproximadamente el siguiente:

* Capacidad para usar `Tab` y `Shift+Tab` pulsaciones de teclas para desplazarse entre los elementos interactivos de la página.
El uso de `Tab` avanza el enfoque de entrada al siguiente elemento de interfaz de usuario en el orden de tabulación; el uso de `Shift+Tab` devuelve el enfoque de entrada al elemento de interfaz de usuario anterior.
La inversión del enfoque sigue la ubicación natural del elemento de la interfaz de usuario en la pantalla y se mueve de izquierda a derecha y, a continuación, de arriba a abajo. Además, si algún campo presenta un error, puede presionar `Tab` para desplazar el enfoque al mismo.
* Capacidad para usar la clave `Spacebar` y `Enter` para activar elementos estándar de la interfaz de usuario, como botones y listas desplegables.
* Posibilidad de ver el resalte de enfoque del teclado en el elemento activo. El elemento de interfaz de usuario que tiene el enfoque de entrada recibió una indicación de enfoque visual como un borde procesado alrededor del elemento de interfaz de usuario.
* En el editor de puntos interactivos, puede utilizar algunas pulsaciones de teclas personalizadas, como las teclas de flecha, para interactuar con elementos complejos de la interfaz de usuario y cambiar la posición de los puntos interactivos.
* En el editor de vídeo interactivo, puede utilizar `Spacebar` para seleccionar una imagen y agregarla a un segmento. Además, puede usar la clave `Backspace` para eliminar el elemento seleccionado de la ficha **[!UICONTROL Contenido]**. Además, si presiona `Tab`, funcionará como desee para desplazarse entre los elementos interactivos de la página.
* En el editor de recorte inteligente/recorte inteligente de imágenes, puede hacer lo siguiente:
   * Utilice las teclas de flecha para recortar el tamaño del marco, cambiar la posición de la imagen o ambas cosas.
   * La primera `Tab` detención resalta todo el marco de imagen. A continuación, puede utilizar las teclas de flecha del teclado para cambiar la posición del marco.
   * Las siguientes cuatro `Tab` paradas son las cuatro esquinas del fotograma. Cuando el enfoque se coloca en una esquina del marco, la esquina se resalta. De nuevo, puede utilizar las teclas de flecha del teclado para mover la esquina enfocada.
Ver [Edición del recorte inteligente o la muestra inteligente de una sola imagen](/help/assets/dynamic-media/image-profiles.md#editing-the-smart-crop-or-smart-swatch-of-a-single-image)

<!-- Keyboarding is the same because Dynamic Media is using the same UI library (Coral 3 (Experience Manager 6.5) or Coral Spectrum (in Skyline)) as entire Experience Manager Assets.  -->

<!-- In the Hotspot editor, Dynamic Media lets you use arrow keys to control the position of a hot spot. See [Carousel Banners](/help/assets/dynamic-media/carousel-banners.md#adding-hotspots-or-image-maps-to-an-image-banner) or [Interactive Images](/help/assets/dynamic-media/interactive-images.md#adding-hotspots-to-an-image-banner)  -->

<!-- I think we should definitely mention this in the DM-specific area of documentation for keyboard support. -->

<!-- I would not get into much of details of specific keyboard support logic of these editors. One of the reasons - chances are that accessibility support will receive Phase2-like attention, with more holistic approach. -->

## Compatibilidad con tecnología de asistencia en Dynamic Media {#assistive-technology=support-for-dm}

Los elementos de la interfaz de usuario de Dynamic Media funcionan con tecnologías de asistencia como lectores de pantalla. Por ejemplo, reconoce los puntos de referencia de una página cuando se navegan por ellos mediante el método abreviado de teclado `D` o regiones mediante el método abreviado de teclado `R`. También narra el encabezado al navegar mediante el método abreviado de teclado de encabezado `H`.

## Compatibilidad con accesibilidad del teclado en visores de Dynamic Media {#keyboard-accessibility-for-dm-viewers}

Todos los componentes listos para usar de los visores de Dynamic Media admiten la accesibilidad del teclado para sus clientes.

Consulte [Navegación y accesibilidad por teclado](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/c-keyboard-accessibility.html?lang=es) en la Guía de referencia de visores de Dynamic Media.

## Compatibilidad con tecnología de asistencia en los visores de Dynamic Media {#assistive-technology=support-for-dm-viewers}

Todos los componentes del visualizador de Dynamic Media admiten los roles y atributos de ARIA (Aplicaciones de Internet enriquecidas accesibles) para mejorar la integración con tecnologías de asistencia como lectores de pantalla.
Consulte el tema de ayuda **Compatibilidad con tecnología de asistencia** en cualquier tema de personalización de visualizadores de la Guía de referencia de visualizadores de Dynamic Media. Por ejemplo, consulte [Compatibilidad con tecnología de asistencia](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/video/r-html5-video-viewer-20-assistive.html?lang=es) para el visor de vídeo o [Compatibilidad con tecnología de asistencia](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-images/c-html5-aem-interactive-image-assistive.html?lang=es#viewers-for-aem-assets-only) para el visor de imágenes interactivas.

## Compatibilidad con subtítulos ocultos en [!DNL Dynamic Media] {#closed-caption-support}

Dynamic Media admite la entrega de vídeos y conjuntos de vídeos adaptables con subtítulos. Los subtítulos deben mostrarse sobre el contenido del vídeo.

Ver [vídeo en Dynamic Media: agregar subtítulos opcionales al vídeo](/help/assets/dynamic-media/video.md#adding-captions-to-video).


>[!MORELIKETHIS]
>
>* [Accesibilidad para las soluciones de Adobe](https://www.adobe.com/accessibility.html)
>* [Accesibilidad en Experience Manager Assets](/help/assets/dynamic-media/accessibility-dm.md)
