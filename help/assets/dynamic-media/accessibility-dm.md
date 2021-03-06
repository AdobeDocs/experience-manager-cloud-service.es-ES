---
title: Accesibilidad en Dynamic Media
description: Aprenda a trabajar con vídeo en Dynamic Media, como prácticas recomendadas para codificar vídeos, publicar vídeos en YouTube y ver informes de vídeo. Aprenda también a añadir subtítulos o marcadores de capítulo a los vídeos.
contentOwner: Rick Brough
topic-tags: introduction
content-type: reference
feature: Accessibility
role: Admin,User
exl-id: f8d2dcbf-f61a-4b27-a3fc-406e3662adcb
source-git-commit: 0d3262a3182063e69f764339e7937e2f83ad7bbb
workflow-type: tm+mt
source-wordcount: '665'
ht-degree: 1%

---

# Accesibilidad en Dynamic Media {#accessibility-in-dm}

Dynamic Media admite tecnologías de control de teclado y asistencia, como lectores de pantalla JAWS y NVDA, en la interfaz de usuario de creación.

## Compatibilidad con la accesibilidad del teclado en Dynamic Media {#keyboard-support-in-dm}

Como Dynamic Media es un complemento para [!DNL Experience Manager Assets], la mayoría del comportamiento del control de teclado es el mismo que en [!DNL Experience Manager Assets]. Por ejemplo, la variable `Cancel` en Dynamic Media tiene el mismo resaltado de enfoque que en [!DNL Experience Manager Assets]. También reacciona ante el `Spacebar` clave como en [!DNL Experience Manager Assets]. Consulte [combinaciones de teclas en Assets](/help/assets/accessibility.md#keyboard-shortcuts).

Las pulsaciones de teclas admitidas por los elementos de la interfaz de usuario individual en Dynamic Media son, en la mayoría de los casos, obvias y fáciles de encontrar. El control de teclado en Dynamic Media es sobre lo siguiente:

* Capacidad de uso `Tab` y `Shift+Tab` pulsaciones de teclas para desplazarse entre los elementos interactivos de la página.
Uso `Tab` avanza el enfoque de entrada al siguiente elemento de interfaz de usuario en el orden de tabulación; using `Shift+Tab` devuelve el enfoque de entrada al elemento de interfaz de usuario anterior.
El enfoque transversal sigue la ubicación del elemento de la interfaz de usuario natural en la pantalla y se mueve de izquierda a derecha y, a continuación, de arriba a abajo. Además, si algún campo presenta un error, puede pulsar `Tab` para mover el enfoque a él.
* Capacidad para usar la variable `Spacebar` y `Enter` para activar elementos estándar de la interfaz de usuario, como botones y listas desplegables.
* Posibilidad de ver el resaltado del foco del teclado en el elemento activo. El elemento de interfaz de usuario que tiene foco de entrada recibió una indicación de enfoque visual como borde representado alrededor del elemento de interfaz de usuario.
* En el editor de puntos interactivos, puede utilizar algunas pulsaciones de teclas personalizadas, como teclas de flecha, para interactuar con elementos complejos de la interfaz de usuario con el fin de cambiar la posición de los puntos interactivos.
* En el editor de vídeo interactivo, puede usar la variable `Spacebar` para seleccionar una imagen y añadirla a un segmento. Además, puede usar la variable `Backspace` para eliminar el elemento seleccionado del **[!UICONTROL Contenido]** pestaña . También, presionando `Tab` para desplazarse entre los elementos interactivos de la página.
* En el editor Recorte de imagen/Recorte inteligente, puede hacer lo siguiente:
   * Utilice las teclas de flecha para recortar el tamaño del marco, o para cambiar la posición de la imagen, o ambas.
   * La primera `Tab` stop resalta todo el marco de imagen. A continuación, puede utilizar las teclas de flecha del teclado para cambiar la posición del marco.
   * Las cuatro siguientes `Tab` las paradas son las cuatro esquinas del marco. Cuando el enfoque se coloca en una esquina de marco, la esquina se resalta. De nuevo, puede utilizar las teclas de flecha del teclado para mover la esquina enfocada.
Consulte [Edición del recorte inteligente o de la muestra inteligente de una sola imagen](/help/assets/dynamic-media/image-profiles.md#editing-the-smart-crop-or-smart-swatch-of-a-single-image)

<!-- Keyboarding is the same because Dynamic Media is using the same UI library (Coral 3 (Experience Manager 6.5) or Coral Spectrum (in Skyline)) as entire Experience Manager Assets.  -->

<!-- In the Hotspot editor, Dynamic Media lets you use arrow keys to control the position of a hot spot. See [Carousel Banners](/help/assets/dynamic-media/carousel-banners.md##adding-hotspots-or-image-maps-to-an-image-banner) or [Interactive Images](/help/assets/dynamic-media/interactive-images.md#adding-hotspots-to-an-image-banner)  -->

<!-- I think we should definitely mention this in the DM-specific area of documentation for keyboard support. -->

<!-- I would not get into much of details of specific keyboard support logic of these editors. One of the reasons - chances are that accessibility support will receive Phase2-like attention, with more holistic approach. -->

## Compatibilidad con tecnología de asistencia en Dynamic Media {#assistive-technology=support-for-dm}

Los elementos de la interfaz de usuario de Dynamic Media funcionan con tecnologías de asistencia, como lectores de pantalla. Por ejemplo, reconoce los puntos de referencia en una página cuando se navegan por los puntos de referencia mediante el método abreviado de teclado `D` o regiones que utilicen la combinación de teclas `R`. También narra el encabezado al navegar mediante la combinación de teclas del encabezado `H`.

## Compatibilidad con la accesibilidad del teclado en los visores de Dynamic Media {#keyboard-accessibility-for-dm-viewers}

Todos los componentes de visores de Dynamic Media integrados admiten la accesibilidad del teclado para sus clientes.

Consulte [Navegación y accesibilidad del teclado](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/c-keyboard-accessibility.html) en la Guía de referencia de visores de Dynamic Media.

## Compatibilidad con tecnología de asistencia en los visores de Dynamic Media {#assistive-technology=support-for-dm-viewers}

Todos los componentes del visor de Dynamic Media admiten las funciones y atributos de ARIA (Aplicaciones de Internet enriquecidas accesibles) para mejorar la integración con tecnologías de asistencia, como lectores de pantalla.
Consulte la **Soporte técnico de asistencia** Tema de ayuda de cualquier tema de personalización de visores en la Guía de referencia de visores de Dynamic Media. Por ejemplo, consulte [Soporte técnico de asistencia](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/video/r-html5-video-viewer-20-assistive.html) para el visor de vídeo, o [Soporte técnico de asistencia](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-images/c-html5-aem-interactive-image-assistive.html#viewers-for-aem-assets-only) para el visualizador de imagen interactiva.

## Compatibilidad con subtítulos opcionales en [!DNL Dynamic Media] {#closed-caption-support}

Dynamic Media admite la entrega de conjuntos de vídeos y vídeos adaptables con subtítulos. Los subtítulos deben mostrarse sobre el contenido del vídeo.

Consulte [Vídeo en Dynamic Media: Agregar subtítulos o subtítulos cerrados a un vídeo](/help/assets/dynamic-media/video.md#adding-captions-to-video).


>[!MORELIKETHIS]
>
>* [Accesibilidad para soluciones de Adobe](https://www.adobe.com/accessibility.html)
>* [Accesibilidad en Experience Manager Assets](/help/assets/dynamic-media/accessibility-dm.md)

