---
title: Accesibilidad en [!DNL Dynamic Media]
description: Aprenda a trabajar con recursos 3D en Dynamic Media
contentOwner: Rick Brough
topic-tags: introduction
content-type: reference
translation-type: tm+mt
source-git-commit: d992b68d4a015f8f947167b5b1d5f0a1ac5c09ec
workflow-type: tm+mt
source-wordcount: '469'
ht-degree: 0%

---


# Accesibilidad en Dynamic Media {#working-with-three-d-assets-dm}

Dynamic Media admite tecnologías de control de teclado y asistencia, como lectores de pantalla JAWS y NVDA, en la interfaz de usuario de creación.

## Compatibilidad de accesibilidad de teclado en Dynamic Media

Las pulsaciones de teclas admitidas por los elementos individuales de la interfaz de usuario son, en la mayoría de los casos, obvias y fáciles de detectar. El control de teclado en Dynamic Media es de lo siguiente:

* Posibilidad de utilizar `Tab` y `Shift+Tab` pulsaciones de tecla para desplazarse entre los elementos interactivos de la página.
El uso del enfoque de entrada `Tab` avanza al siguiente elemento de interfaz de usuario en el orden de tabulación; el uso `Shift+Tab` devuelve el enfoque de entrada al elemento de interfaz de usuario anterior.
El recorrido de enfoque sigue la ubicación del elemento de interfaz de usuario natural en la pantalla y se mueve de izquierda a derecha y, a continuación, de arriba abajo.
* Posibilidad de utilizar la `Spacebar` tecla y `Enter` para activar elementos de la interfaz de usuario estándar, como botones, lista desplegable, etc.
* Posibilidad de utilizar algunas pulsaciones de teclas personalizadas para interactuar con elementos de interfaz de usuario complejos, como las teclas de flecha del Editor de zonas interactivas.
* Posibilidad de ver el resaltado del enfoque del teclado en el elemento activo. El elemento de interfaz de usuario que tiene foco de entrada puede recibir una indicación de enfoque visual como borde representado alrededor del elemento de interfaz de usuario.

Dado que Dynamic Media es un complemento de AEM Assets, la mayor parte del comportamiento de control de teclado es exactamente el mismo que en AEM Assets. Por ejemplo, el `Cancel` botón de Dynamic Media tiene el mismo resaltado de enfoque que en AEM Assets y reacciona a la `Spacebar` clave que en AEM Assets. Consulte Métodos abreviados [de teclado en Recursos](/help/assets/accessibility.md#keyboard-shortcuts). Las excepciones son el editor de puntos interactivos y los editores de recorte de imagen/recorte inteligente.

<!-- Keyboarding is the same because Dynamic Media is using the same UI library (Coral 3 (AEM 6.5) or Coral Spectrum (in Skyline)) as entire AEM Assets.  -->

En el editor de zonas interactivas, Dynamic Media permite utilizar las teclas de flecha para controlar la posición de un punto interactivo. Consulte Pancartas [de carrusel](/help/assets/dynamic-media/carousel-banners.md##adding-hotspots-or-image-maps-to-an-image-banner) o imágenes [interactivas](/help/assets/dynamic-media/interactive-images.md#adding-hotspots-to-an-image-banner)

En el editor Recorte de imagen/Recorte inteligente, utilice las teclas de flecha para recortar el tamaño del marco o para cambiar la posición de la imagen, o ambas opciones. Consulte [Edición del recorte inteligente o muestra inteligente de una sola imagen](/help/assets/dynamic-media/image-profiles.md#editing-the-smart-crop-or-smart-swatch-of-a-single-image)

<!-- I think we should definitely mention this in the DM-specific area of documentation for keyboard support. -->

<!-- I would not get into much of details of specific keyboard support logic of these editors. One of the reasons - chances are that accessibility support will receive Phase2-like attention, with more holistic approach. -->

## Compatibilidad de accesibilidad de teclado para visores de Dynamic Media {#keyboard-accessibility-for-dm-viewers}

Todos los componentes de visores de Dynamic Media integrados admiten la accesibilidad del teclado para sus clientes.

Consulte Acceso [al teclado y navegación](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/library/c-keyboard-accessibility.html) en la Guía de referencia de visores de Dynamic Media.

## Compatibilidad con tecnología de asistencia para visores de Dynamic Media {#assistive-technology=support-for-dm-viewers}

Todos los componentes del visor de Dynamic Media admiten funciones y atributos ARIA (Aplicaciones de Internet enriquecidas accesibles) para mejorar la integración con tecnologías de asistencia como lectores de pantalla.

Consulte el tema de ayuda sobre la compatibilidad con **la tecnología de** asistencia en cualquier tema de personalización del visor de la Guía de referencia de visores de Dynamic Media. Por ejemplo, consulte [Compatibilidad](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/video/r-html5-video-viewer-20-assistive.html) con tecnología de asistencia para el visor de vídeo o Compatibilidad con [tecnología de](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-images/c-html5-aem-interactive-image-assistive.html?lang=en#viewers-for-aem-assets-only) asistencia para el visor de imágenes interactivo.

>[!MORELIKETHIS]
>
>* [Accesibilidad para las soluciones de Adobe](https://www.adobe.com/accessibility.html)
>* [Accesibilidad en recursos Experience Manager](/help/assets/dynamic-media/accessibility-dm.md)

