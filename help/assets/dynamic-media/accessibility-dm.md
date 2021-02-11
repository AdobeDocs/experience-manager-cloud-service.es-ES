---
title: Accesibilidad en Dynamic Media
description: Obtenga información sobre la accesibilidad en los visores de Dynamic Media y Dynamic Media.
contentOwner: Rick Brough
topic-tags: introduction
content-type: reference
translation-type: tm+mt
source-git-commit: cf607bd27463f23de29d0d6770940a01f3e36c87
workflow-type: tm+mt
source-wordcount: '611'
ht-degree: 0%

---


# Accesibilidad en Dynamic Media {#accessibility-in-dm}

Dynamic Media admite tecnologías de control de teclado y asistencia, como lectores de pantalla JAWS y NVDA, en la interfaz de usuario de creación.

## Compatibilidad con accesibilidad de teclado en Dynamic Media {#keyboard-support-in-dm}

Dado que Dynamic Media es un complemento de Recursos Experience Manager, la mayoría del control de teclado es el mismo que en Recursos Experience Manager. Por ejemplo, el botón `Cancel` de Dynamic Media tiene el mismo resaltado de enfoque que en Recursos Experience Manager. También reacciona a la clave `Spacebar` como en Recursos Experience Manager. Consulte [combinaciones de teclas en Recursos](/help/assets/accessibility.md#keyboard-shortcuts).

Las pulsaciones de teclas admitidas por los elementos de interfaz de usuario individuales en Dynamic Media son, en la mayoría de los casos, obvias y fáciles de encontrar. El control de teclado en Dynamic Media es de lo siguiente:

* Posibilidad de utilizar pulsaciones de tecla `Tab` y `Shift+Tab` para navegar entre los elementos interactivos de la página.
Al utilizar `Tab` se pasa el enfoque de entrada al siguiente elemento de interfaz de usuario en el orden de tabulación; el uso de `Shift+Tab` devuelve el enfoque de entrada al elemento de interfaz de usuario anterior.
El recorrido de enfoque sigue la ubicación del elemento de interfaz de usuario natural en la pantalla y se mueve de izquierda a derecha y, a continuación, de arriba abajo. Además, si algún campo tiene un error, puede presionar `Tab` para mover el enfoque a él.
* Posibilidad de utilizar la clave `Spacebar` y `Enter` para activar elementos de interfaz de usuario estándar, como botones y listas desplegables.
* Posibilidad de ver el resaltado del enfoque del teclado en el elemento activo. El elemento de interfaz de usuario que tiene foco de entrada recibió una indicación de enfoque visual como borde representado alrededor del elemento de interfaz de usuario.
* En el editor de zonas interactivas, puede utilizar algunas pulsaciones de teclas personalizadas, como las teclas de flecha, para interactuar con elementos complejos de la interfaz de usuario y cambiar la posición de las zonas interactivas.
* En el editor de vídeo interactivo, puede utilizar `Spacebar` para seleccionar una imagen y agregarla a un segmento. Además, puede utilizar la clave `Backspace` para eliminar el elemento seleccionado de la ficha **[!UICONTROL Contenido]**. Además, al pulsar `Tab` se actúa como se desea para navegar entre los elementos interactivos de la página.
* En el editor Recorte de imagen/Recorte inteligente, puede hacer lo siguiente:
   * Utilice las teclas de flecha para recortar el tamaño del marco, cambiar la posición de la imagen o ambas opciones.
   * La primera detención `Tab` resalta todo el marco de la imagen. A continuación, puede utilizar las teclas de flecha del teclado para cambiar la posición del marco.
   * Las cuatro paradas siguientes `Tab` son las cuatro esquinas del marco. Cuando el enfoque se coloca en una esquina de marco, la esquina se resalta. De nuevo, puede utilizar las teclas de flecha del teclado para mover la esquina seleccionada.
Consulte [Edición del recorte inteligente o muestra inteligente de una sola imagen](/help/assets/dynamic-media/image-profiles.md#editing-the-smart-crop-or-smart-swatch-of-a-single-image)

<!-- Keyboarding is the same because Dynamic Media is using the same UI library (Coral 3 (AEM 6.5) or Coral Spectrum (in Skyline)) as entire AEM Assets.  -->

<!-- In the Hotspot editor, Dynamic Media lets you use arrow keys to control the position of a hot spot. See [Carousel Banners](/help/assets/dynamic-media/carousel-banners.md##adding-hotspots-or-image-maps-to-an-image-banner) or [Interactive Images](/help/assets/dynamic-media/interactive-images.md#adding-hotspots-to-an-image-banner)  -->

<!-- I think we should definitely mention this in the DM-specific area of documentation for keyboard support. -->

<!-- I would not get into much of details of specific keyboard support logic of these editors. One of the reasons - chances are that accessibility support will receive Phase2-like attention, with more holistic approach. -->

## Soporte de tecnología de asistencia en Dynamic Media {#assistive-technology=support-for-dm}

Los elementos de la interfaz de usuario de Dynamic Media funcionan con tecnologías de asistencia, como lectores de pantalla. Por ejemplo, reconoce los puntos de referencia en una página cuando se navega por los puntos de referencia mediante el método abreviado de teclado `D` o las regiones mediante el método abreviado de teclado `R`. También narra el encabezado al navegar mediante el método abreviado de teclado de encabezado `H`.

## Compatibilidad de accesibilidad de teclado en visores de Dynamic Media {#keyboard-accessibility-for-dm-viewers}

Todos los componentes de visores de Dynamic Media integrados admiten la accesibilidad del teclado para sus clientes.

Consulte [Navegación y accesibilidad del teclado](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/c-keyboard-accessibility.html) en la Guía de referencia de visores de Dynamic Media.

## Compatibilidad con tecnología de asistencia en visores de Dynamic Media {#assistive-technology=support-for-dm-viewers}

Todos los componentes del visor de Dynamic Media admiten funciones y atributos ARIA (Aplicaciones de Internet enriquecidas accesibles) para mejorar la integración con tecnologías de asistencia como lectores de pantalla.
Consulte el tema de ayuda **Compatibilidad con tecnología de asistencia** en cualquier tema de personalización del visor de la Guía de referencia de visores de Dynamic Media. Por ejemplo, consulte [Compatibilidad con tecnología de asistencia](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/video/r-html5-video-viewer-20-assistive.html) para el visor de vídeo o [Compatibilidad con tecnología de asistencia](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-images/c-html5-aem-interactive-image-assistive.html?lang=en#viewers-for-aem-assets-only) para el visor de imágenes interactivo.

>[!MORELIKETHIS]
>
>* [Accesibilidad para las soluciones de Adobe](https://www.adobe.com/accessibility.html)
>* [Accesibilidad en recursos Experience Manager](/help/assets/dynamic-media/accessibility-dm.md)

