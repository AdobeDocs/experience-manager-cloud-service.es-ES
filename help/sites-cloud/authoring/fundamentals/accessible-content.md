---
title: Creación de contenido accesible para Adobe Experience Manager como servicio de nube (conformidad con WCAG 2.1)
description: Ayude a que las personas con discapacidades puedan acceder al contenido web y utilizarlo
translation-type: tm+mt
source-git-commit: 6d905c5a29b71c9d05dba910a20ffef21a4eceec

---


# Crear contenido accesible (Conformidad con WCAG 2.1) {#creating-accessible-content-wcag-conformance}

Las Directrices de Accesibilidad al Contenido [Web (WCAG) 2.1](https://www.w3.org/TR/WCAG/), elaboradas por [un grupo de trabajo del World Wide Wec Consortium](https://www.w3.org/Consorcio/actividades#Accessibility_Guidelines_Working_Group), consisten en un conjunto de directrices y criterios de éxito independientes de la tecnología para ayudar a las personas con discapacidad a tener acceso al contenido web y utilizarlos.

Como introducción, el consorcio ofrece una serie de secciones y documentos de apoyo:

* [Nuevas funciones de WCAG 2.1](https://www.w3.org/TR/WCAG/#new-features-in-wcag-2-1)
* [Cómo cumplir con WCAG 2.1](https://www.w3.org/WAI/WCAG21/quickref/)
* [Explicación de WCAG 2.1](https://www.w3.org/WAI/WCAG21/Understanding/)
* [Técnicas para WCAG 2.1](https://www.w3.org/WAI/WCAG21/Techniques/)
* [Los Documentos WCAG](https://www.w3.org/WAI/standards-guidelines/wcag/docs/)

Además, consulte:
* Our [Quick Guide to WCAG 2.1](/help/onboarding/accessibility/quick-guide-wcag.md) for further details

<!-- 
>* [Configuring the Rich Text Editor for producing accessible conten](/help/sites-administering/rte-accessible-content.md)
-->

Las directrices se clasifican según tres niveles de conformidad: Nivel A (más bajo), Nivel AA y Nivel AAA (más alto). Brevemente, los niveles se definen de la siguiente manera:

* **Nivel A:** El sitio alcanza un nivel básico y mínimo de accesibilidad. Para alcanzar este nivel, se cumplen todos los criterios de éxito del nivel A.
* **Nivel AA:** Se trata de un nivel ideal de accesibilidad en el que su página alcanza un nivel mejorado de accesibilidad, por lo que resulta accesible para mucha gente, en muchas situaciones y utilizando distintas tecnologías. Para alcanzar este nivel, se deben cumplir todos los criterios de éxito de los niveles A y niveles AA.
* **Nivel AAA:** Su sitio alcanza un nivel muy alto de accesibilidad. Para alcanzar este nivel, se cumplen todos los criterios de éxito de los niveles A, AA y AAA.

Al crear su sitio, debe determinar el nivel general en el que desea que se ajuste.

La siguiente sección presenta las [directrices WCAG 2.1](https://www.w3.org/TR/WCAG/#wcag-2-layers-of-guidance) con criterios de éxito vinculados a los [niveles de conformidad](https://www.w3.org/TR/WCAG/#conformance-to-wcag-2-1) de los niveles A y AA.

>[!NOTE]
>
>Como no se pueden satisfacer todos los criterios de éxito del Nivel AAA para ciertos tipos de contenido, no es recomendable pedir este nivel de conformidad como política general.

>[!NOTE]
>
>En este documento utilizamos:
>
>* The short names for the [WCAG 2.1 Guidelines](https://www.w3.org/TR/WCAG/#wcag-2-layers-of-guidance).
>* The numbering used in the [WCAG 2.1 Guidelines](https://www.w3.org/TR/WCAG/#wcag-2-layers-of-guidance) to aid cross-referencing with the WCAG website.
>



## Principio 1: perceptible  {#principle-perceivable}

[Principio 1: perceptible. Los componentes de la interfaz de usuario y de la información se deben presentar a los usuarios de forma perceptible.](https://www.w3.org/TR/WCAG/#perceivable)

### Alternativas de texto (1.1)  {#text-alternatives}

[Directrices 1.1 Alternativas de texto: proporciona alternativas de texto para cualquier contenido no textual para cambiarlo por otras formas según sea necesario, como letras grandes, braille, voz, símbolos o lenguaje más sencillo.](https://www.w3.org/TR/WCAG/#text-alternatives)

### Contenido no textual (1.1.1)  {#non-text-content}

* Criterios de éxito 1.1.1
* Nivel A
* Contenido no textual: todo contenido no textual que se presenta al usuario tiene una alternativa de texto que cumple el objetivo equivalente, excepto para las situaciones que se detallan a continuación

#### Objetivo: Contenido no textual (1.1.1) {#purpose-non-text-content}

La información en una página web se puede proporcionar en muchos formatos no textuales distintos, como fotografías, vídeos, animaciones, tablas y gráficos. Las personas ciegas o con deficiencias visuales graves no pueden ver el contenido no textual, pero pueden acceder al contenido textual si lo lee en voz alta un lector de pantalla o si se presenta en un formato táctil a través de un dispositivo de visualización braille. Por ello, al proporcionar alternativas textuales para el contenido en formato gráfico, quienes no puedan ver el contenido gráfico podrán acceder a una versión equivalente de la información que proporcione el contenido.

Un beneficio útil adicional es que las alternativas textuales permiten indexar contenido no textual mediante una tecnología de buscadores.

#### Cómo cumplir: Contenido no textual (1.1.1)  {#how-to-meet-non-text-content}

Para gráficos estáticos, el requisito principal es proporcionar una alternativa textual equivalente para el gráfico. Esto se puede llevar a cabo en el campo **Texto alternativo:**

>[!NOTE]
>
>Algunos componentes listos para usar, como **Carrusel** y **Presentación de diapositivas,** no proporcionan los medios para añadir descripciones de texto alternativas a las imágenes. Cuando se implementan versiones de estos componentes para su instancia de AEM, su equipo de desarrollo debe configurarlos para dar soporte al atributo `alt` y para que así los autores puedan añadirlo al contenido (consulte Añadir soporte para elementos y atributos HTML adicionales).

<!--
>Some out-of-the-box components, such as **Carousel** and **Slideshow** do not provide a means for adding alternate text descriptions to images. When implementing versions of these for your AEM instance, your development team will need to configure such components to support the `alt` attribute so that authors can add it to the content (see [Adding Support for Additional HTML Elements and Attributes](/help/sites-administering/rte-accessible-content.md#adding-support-for-additional-html-elements-and-attributes)).
-->

De forma predeterminada, AEM requiere que el campo **Texto alternativo** se rellene. Si la imagen es puramente decorativa y el texto alternativo carecería de sentido, se puede marcar la opción **La imagen es decorativa**.

#### Crear buenas alternativas de texto {#creating-good-text-alternatives}

Existen distintos tipos de contenido no textual, por lo que el valor de la alternativa textual depende del papel que juegue el elemento gráfico en la página web. Algunas de las normas generales a seguir incluyen:

* Las alternativas textuales deben ser precisas pero también deben recoger con claridad la información esencial proporcionada por el contenido no textual. 
* Deben evitarse las descripciones demasiado largas (que superen los 100 caracteres). Si una alternativa textual requiere más detalle:
   * proporcione una breve descripción en el texto alternativo
   * y añada una descripción más larga en el texto en cualquier otra parte, en la misma página o en una página web aparte. Cree un vínculo a esta descripción en la imagen o a través de un texto vinculante adyacente a la imagen.
* El texto alternativo no debe repetir el contenido proporcionado en el texto de la misma página. Muchas imágenes son ilustraciones de puntos que ya se han cubierto en el texto de la página, por lo que puede que ya exista una alternativa textual detallada.
* Si el contenido no textual es un vínculo a otra página o documento y no hay otro texto que forme parte del mismo vínculo, entonces el texto alternativo para la imagen debe indicar el destino del vínculo en lugar de describir la imagen.
* Si el contenido no textual está contenido en un botón y no hay texto que forme parte del mismo botón, entonces el texto alternativo de la imagen debe indicar la funcionalidad del botón, en lugar de describir la imagen.
* Es perfectamente aceptable que se dé a una imagen un texto alternativo vacío (nulo), pero solo si la imagen no tiene texto alternativo (por ejemplo, si es un elemento gráfico puramente decorativo) o si el texto equivalente ya existe en la página textual.

<!--
The [W3C draft: HTML5 Techniques for providing useful text alternatives](https://dev.w3.org/html5/alt-techniques/) has more details and examples of appropriate alternative text provision for images of different types.
-->

Los tipos específicos de contenido no textual que requieren alternativas textuales pueden incluir:

* Fotos ilustrativas:
Imágenes de personas, objetos o lugares. Considere el papel que juega la fotografía en la página; un texto equivalente apropiado puede ser `Photo of [object]`, pero puede depender del texto que lo rodea.
* Iconos:
Pequeños pictogramas (gráficos) que transmiten información específica. Se deben utilizar de manera consistente en una página o sitio. Todos los ejemplos del icono en una página o sitio deben contener el mismo texto alternativo, corto y preciso, a menos que se duplique innecesariamente el texto adyacente.
* Tablas y gráficos: Normalmente representan datos numéricos. Una opción para proporcionar una alternativa textual podría ser incluir un breve resumen de las tendencias principales que se muestran en la tabla o en el gráfico. Si es necesario, proporcione también una descripción más detallada en formato texto utilizando el campo **Descripción** en la pestaña de Propiedades de la imagen **avanzadas**. Además, puede proporcionar los datos de origen en formato tabulado en cualquier otra parte de la página o sitio.
* Mapas, diagramas y organigramas: Para los gráficos que proporcionan datos espaciales (por ejemplo para apoyar las relaciones descritas entre objetos o un proceso), es importante asegurarse de que el mensaje clave se proporciona en formato textual. Para los mapas, puede ser poco práctico proporcionar un equivalente textual extenso, pero si el mapa se proporciona como una manera de ayudar al usuario a encontrar el camino hasta un lugar concreto, el texto alternativo de la imagen del mapa se puede indicar brevemente como *Mapa de X*, y después proporcionar las instrucciones para llegar al lugar en formato textual en cualquier otra parte de la página o a través del campo **Descripción** en la pestaña **Avanzado** del componente **Imagen**.
* CAPTCHA: CAPTCHA se refiere a una *prueba de Turing pública completamente automática que distingue entre ordenadores y humanos*. Es una medida de seguridad que se utiliza en páginas web para distinguir a humanos de software maligno, pero que puede originar barreras de accesibilidad. Se trata de imágenes que requieren que los usuarios describan lo que ven para pasar una prueba de seguridad. Como obviamente no es posible proporcionar una alternativa textual para la imagen, en lugar de ello tendrá que considerar una solución alternativa que no sea gráfica.‪
W3C proporciona varias sugerencias como: Cada uno de estos enfoques tiene sus propias ventajas e inconvenientes.‪
   * Rompecabezas de lógica
   * Salida de sonido en lugar de imágenes
   * Cuentas de uso limitado y filtros de spam
* Imágenes de fondo: Se consiguen utilizando hojas de estilo en cascada (CSS) en lugar de HTML. Esto quiere decir que no se puede especificar un valor de texto alternativo. Por ello, las imágenes de fondo no deben proporcionar información textual importante: si lo hacen, dicha información se debe proporcionar en el texto de la página.
Sin embargo, es importante que se muestre un fondo alternativo cuando la imagen no se pueda mostrar.

>[!NOTE]
>
>Debe haber un nivel adecuado de contraste entre el fondo y el texto en primer plano; este es un tema que se analiza en detalle en [Contraste (Mínimo) (1.4.3)](#contrast-minimum).

#### Más información: contenido no textual (1.1.1)  {#more-information-non-text-content}

* [Entender los criterios de éxito 1.1.1](https://www.w3.org/WAI/WCAG21/Understanding/non-text-content.html)
* [Cumplir los criterios de éxito 1.1.1](https://www.w3.org/WAI/WCAG21/quickref/#non-text-content)
* [Explicación de W3C y alternativas para CAPTCHA](https://www.w3.org/TR/turingtest/)

<!--
* [W3C: HTML5 Techniques for providing useful text alternatives (draft)](https://dev.w3.org/html5/alt-techniques/)
-->

### Medios basados en el tiempo (1.2)  {#time-based-media}

[Directrices 1.2 Medios basados en el tiempo: proporcionar alternativas para medios basados en el tiempo.](https://www.w3.org/TR/WCAG/#time-based-media)

Trata el contenido de la página web *basado en el tiempo*. Abarca el contenido que puede reproducir el usuario (como vídeos, audios y contenido animado) y se puede pregrabar o reproducir en vivo.

### Audio-only and Video-only (Prerecorded) (1.2.1) {#audio-only-and-video-only-prerecorded}

* Criterios de éxito 1.2.1
* Nivel A
* Solo audio y Solo vídeo (pregrabado): para medios de solo audio y solo vídeo pregrabado, la siguiente información es cierta, excepto cuando el audio o el vídeo es una alternativa para texto y se etiqueta claramente como:
   * Solo audio pregrabado: se proporciona una alternativa para medios basados en el tiempo que presenta información equivalente para contenido de solo audio pregrabado.
   * Solo vídeo pregrabado: se proporciona una alternativa para medios basados en el tiempo o una pista de audio que presenta información equivalente para contenido de solo vídeo pregrabado.

#### Purpose - Audio-only and Video-only (Prerecorded) (1.2.1) {#purpose-audio-only-and-video-only-prerecorded}

Se pueden dar problemas de accesibilidad para vídeo y audio a través de:

* Personas con discapacidades visuales cuando no hay banda sonora o cuando la banda sonora no basta para informar de lo que está sucediendo en el vídeo o animación;
* Personas con discapacidades auditivas o sordera, que no pueden oír la banda sonora;
* Personas que pueden oír la banda sonora, pero que no entienden lo que se dice (por ejemplo, porque está en un idioma que no entienden).

También puede que el vídeo o el audio no se encuentre disponible para las personas que utilizan navegadores o dispositivos en los que no se puede reproducir contenido en formatos específicos, como Adobe Flash.

Proporcionar esta información en un formato diferente, como texto (o audio para vídeo sin audio) puede ser una manera accesible para personas que no pueden acceder al contenido original.

#### How to Meet - Audio-only and Video-only (Prerecorded) (1.2.1) {#how-to-meet-audio-only-and-video-only-prerecorded}

* Si el contenido es audio pregrabado sin vídeo (como podcast):
   * Proporcione un enlace inmediatamente antes o después del contenido para una transcripción textual del contenido del audio.
La transcripción debe ser una página HTML con un texto equivalente a todo el contenido hablado o no hablado importante, además de una indicación de quién habla, una descripción del escenario, expresiones vocales y una descripción de cualquier otro audio significativo.
* Si el contenido es una animación o un vídeo pregrabado sin audio:
   * Proporcione un vínculo inmediatamente antes o después del contenido para una descripción textual equivalente de la información proporcionada por el vídeo.
   * O bien, una descripción de audio equivalente en un formato de audio comúnmente utilizado, como un MP3.

>[!NOTE]
>
>Si el contenido del audio o vídeo se proporciona como una alternativa que ya existe en otro formato en una página web, no es necesario seguir los requisitos descritos anteriormente. Por ejemplo, si un vídeo ilustra una lista de instrucciones textuales, este vídeo no requiere ninguna alternativa ya que las instrucciones del texto funcionan ya como alternativa para el vídeo.

Insertar contenido multimedia, en concreto contenido Flash, en sus páginas web AEM es parecido a insertar una imagen. Sin embargo, como el contenido multimedia es mucho más que una imagen fija, existe una gran variedad de opciones y escenarios para controlar cómo se reproduce el contenido multimedia.

>[!NOTE]
>
>Al utilizar contenido multimedia con contenido informativo, también se deben crear vínculos a opciones alternativas. Por ejemplo, para incluir una transcripción textual, cree una página HTML para reproducir la transcripción y añada un vínculo debajo o junto al contenido del audio.

#### More Information - Audio-only and Video-only (Prerecorded) (1.2.1) {#more-information-audio-only-and-video-only-prerecorded}

* [Entender los criterios de éxito 1.2.1](https://www.w3.org/WAI/WCAG21/Understanding/audio-only-and-video-only-prerecorded.html)
* [Cumplir los criterios de éxito 1.2.1](https://www.w3.org/WAI/WCAG21/quickref/#audio-only-and-video-only-prerecorded)

### Subtítulos (pregrabados) (1.2.2) {#captions-prerecorded}

* Criterios de éxito 1.2.2
* Nivel A
* Subtítulos (pregrabados): se proporcionan los subtítulos para todo el contenido de audio pregrabado en medios sincronizados, excepto cuando los medios son una alternativa para el texto y se etiquetan claramente como tal.

#### Objetivo: Subtítulos (pregrabados) (1.2.2) {#purpose-captions-prerecorded}

Las personas sordas o con dificultades auditivas no podrán acceder, o tendrán grandes dificultades para acceder, al contenido de audio. Los subtítulos son equivalentes textuales para audio verbal y no verbal que se muestran en la pantalla en el momento apropiado durante el vídeo. Permiten entender lo que está ocurriendo a las personas que no pueden oír el audio.

>[!NOTE]
>
>No se requieren subtítulos donde los equivalentes textuales o no textuales (que directamente proporcionan información equivalente) se muestran disponibles en la misma página que el vídeo o la animación.

#### How to Meet - Captions (Prerecorded) (1.2.2) {#how-to-meet-captions-prerecorded}

Los subtítulos pueden ser:

* Abrir: siempre visible cuando se reproduce el vídeo
* Cerrados: el usuario puede activar o desactivar los subtítulos

Utilice subtítulos cerrados siempre que sea posible, ya que proporciona a los usuarios la opción de verlos o de no verlos.

Para los subtítulos cerrados necesitará crear y proporcionar un archivo de subtítulos sincronizados en un formato adecuado (como [SMIL](https://www.w3.org/AudioVideo/)) a lo largo del archivo de vídeo (los detalles de cómo hacerlo van más allá de esta guía, pero hemos proporcionado enlaces a varios tutoriales en [Más información: Subtítulos (pregrabados) (1.2.2)](#more-information-captions-pre-recorded)). Proporcione una nota a los usuarios para que sepan que los subtítulos están disponibles para el vídeo.

Si necesita utilizar subtítulos abiertos, incorpore el texto en la pista de vídeo. Esto se puede conseguir utilizando aplicaciones de edición de vídeo que permiten superponer títulos en el vídeo.

#### More Information - Captions (PreRecorded) (1.2.2) {#more-information-captions-prerecorded}

* [Entender los criterios de éxito 1.2.2](https://www.w3.org/WAI/WCAG21/Understanding/captions-prerecorded.html):
* [Cumplir los criterios de éxito 1.2.2](https://www.w3.org/WAI/WCAG21/quickref/#captions-prerecorded)

<!--
* [W3C: Synchronized Multimedia](https://www.w3.org/AudioVideo/)
* [Captions, Transcripts, and Audio Descriptions - by WebAIM](https://webaim.org/techniques/captions/)
-->

### Audio Description or Media Alternative (Prerecorded) (1.2.3) {#audio-description-or-media-alternative-prerecorded}

* Criterios de éxito 1.2.3
* Nivel A
* Descripción del audio o medios alternativos (pregrabados): se proporciona una alternativa para medios basados en el tiempo o descripción del audio del contenido de vídeo pregrabado para medios sincronizados, excepto cuando el medio es una alternativa para el texto y se etiqueta claramente como tal

#### Purpose - Audio Description or Media Alternative (Prerecorded) (1.2.3) {#purpose-audio-description-or-media-alternative-prerecorded}

Las personas ciegas o con dificultades de visión experimentarán barreras de accesibilidad si la información en un vídeo o animación solo se proporciona de manera visual, o si la banda sonora no proporciona información suficiente para poder entender lo que está pasando visualmente.

#### How to Meet - Audio Description or Media Alternative (Prerecorded) (1.2.3) {#how-to-meet-audio-description-or-media-alternative-prerecorded}

Se pueden adoptar dos métodos para cumplir este criterio de éxito. Cualquiera de los dos es aceptable:

1. Incluir una descripción de audio adicional para el contenido del vídeo. Esto se puede lograr de una de las tres maneras siguientes:
   * Durante pausas en el diálogo existente, proporcionando información sobre los cambios en la escena que no se presentan como parte de la pista de audio existente;
   * Proporcionando una pista de audio nueva, adicional y optativa, que contenga la banda sonora original, pero incluyendo también información de audio adicional sobre los cambios en la escena.
      * Esto permitirá a los usuarios cambiar de la pista de audio existente (que *no* contiene una descripción del audio) a la nueva pista de audio (que *sí* contiene una descripción del audio).
      * Evita interrupciones a los usuarios que no necesitan la descripción adicional.
   * Creando una segunda versión del contenido del vídeo que permita descripciones de audio extendidas. Reduce las dificultades que se asocian al proporcionar descripciones de audio detalladas en los huecos entre el diálogo existente, mediante pausas temporales en el audio y en el vídeo en puntos adecuados. El resultado es una descripción del audio mucho más larga antes de que se retomen las acciones. Como en el ejemplo anterior, esta opción resulta mejor como una pista de audio adicional y opcional para prevenir interrupciones a los usuarios que no necesitan la descripción adicional.
1. Proporcionar una transcripción del texto que sea adecuada al equivalente textual del audio y a los elementos visuales del vídeo o animación. Donde resulte necesario se deberá incluir una indicación de quién está hablando, una descripción del entorno y de las expresiones vocales. Según la longitud, se puede colocar la transcripción en la misma página del vídeo o de la animación o en una página aparte; si se elige esta última opción, se debe proporcionar un vínculo a la transcripción adyacente al vídeo o animación.

Los detalles exactos de cómo crear vídeos descritos por audio quedan fuera del alcance de esta guía. Crear descripciones de vídeo y audio puede llevar mucho tiempo, pero otros productos de Adobe pueden ayudarle a realizar estas tareas. Al crear contenido con Adobe Flash Professional, también se debe crear un guión para recordar al usuario que puede descargar el programa adicional adecuado y proporcionar una alternativa textual a través del elemento `<noscript>`.

#### More Information - Audio Description or Media Alternative (Prerecorded) (1.2.3) {#more-information-audio-description-or-media-alternative-prerecorded}

* [Entender los criterios de éxito 1.2.3](https://www.w3.org/WAI/WCAG21/Understanding/audio-description-or-media-alternative-prerecorded.html)
* [Cumplir los criterios de éxito 1.2.3](https://www.w3.org/WAI/WCAG21/quickref/#audio-description-or-media-alternative-prerecorded)
* [Adobe Encore](https://www.adobe.com/products/encore.html)

### Subtítulos (en vivo) (1.2.4)    {#captions-live}

* Criterios de éxito 1.2.4
* Nivel AA
* Subtítulos (en vivo): se proporcionan subtítulos para todo el contenido de audio en vivo en medios sincronizados.

#### Objetivo: Subtítulos (en vivo) (1.2.4)  {#purpose-captions-live}

Este criterio de éxito es idéntico al de [Subtítulos (pregrabados)](#captions-pre-recorded) puesto que se enfrenta a las barreras de accesibilidad que experimentan las personas sordas o que sufren deficiencias auditivas, excepto por el hecho de que este criterio de éxito trata las presentaciones en vivo tales como retransmisiones vía Internet.

#### Cómo cumplir: Subtítulos (en vivo) (1.2.4) {#how-to-meet-captions-live}

Follow the guidance provided for [Captions (Prerecorded)](#captions-prerecorded) above. However, due to the live nature of the media, caption provision has to be created as quickly as possible and in response to what is happening. Therefore, you should consider using real time captioning or speech-to-text tools.

Las instrucciones detalladas van más allá del alcance de este documento, pero los siguientes recursos proporcionan información útil:

* [WebAIM: Subtítulos a tiempo real](https://www.webaim.org/techniques/captions/realtime.php)

<!--
* [AccessIT (University of Washington): Can captions be generated automatically using speech recognition?](https://www.washington.edu/accessit/articles?1209)
-->

#### Más información: Subtítulos (en vivo) (1.2.4)     {#more-information-captions-live}

* [Entender los criterios de éxito 1.2.4](https://www.w3.org/WAI/WCAG21/Understanding/captions-live.html)
* [Cumplir los criterios de éxito 1.2.4](https://www.w3.org/WAI/WCAG21/quickref/#captions-live)

### Descripción del audio (pregrabado) (1.2.5) {#audio-description-prerecorded}

* Criterios de éxito 1.2.5
* Nivel AA
* Descripción del audio (pregrabado): la descripción del audio se proporciona para todos los contenidos de vídeo pregrabados en medios sincronizados

#### Purpose - Audio Description (Prerecorded) (1.2.5) {#purpose-audio-description-prerecorded}

This success criterion is identical to [Audio Description or Media Alternative (Prerecorded)](#audio-description-or-media-alternative-prerecorded), except that authors must provide a much more detailed audio description to conform to Level AA.

#### How to Meet - Audio Description (Prerecorded) (1.2.5) {#how-to-meet-audio-description-prerecorded}

Follow the guidance provided for [Audio Description or Media Alternative (Prerecorded)](#audio-description-or-media-alternative-prerecorded).

#### More Information - Audio Description (Prerecorded) (1.2.5) {#more-information-audio-description-prerecorded}

* [Entender los criterios de éxito 1.2.5](https://www.w3.org/WAI/WCAG21/Understanding/audio-description-prerecorded.html)
* [Cumplir los criterios de éxito 1.2.5](https://www.w3.org/WAI/WCAG21/quickref/#audio-description-prerecorded)

### Adaptable (1.3)     {#adaptable}

[Directrices 1.3 Adaptable: crear contenido que se pueda presentar de distintas maneras (por ejemplo en un diseño sencillo) sin que pierda información o estructura.](https://www.w3.org/TR/WCAG/#adaptable)

Estas directrices engloban los requisitos necesarios para apoyar a quienes:

* no pueden acceder a la información de la manera en que la presenta el autor, con un diseño estándar de dos dimensiones, varias columnas y en una página web a color;

* utilizan una representación de solo audio o una alternativa visual, como un texto largo o un gran contraste.

### Información y relaciones (1.3.1)          {#info-and-relationships}

* Criterios de éxito 1.3.1
* Nivel A
* Información y relaciones: la información, estructura y relaciones en presentaciones se puede determinar mediante un programa o puede estar disponible en formato texto

#### Objetivo: Información y relaciones (1.3.1)     {#purpose-info-and-relationships}

Muchas tecnologías de asistencia que utilizan las personas con discapacidades cuentan con información estructural para que se pueda reproducir el contenido de salida de manera eficaz. Esta información estructural se puede presentar en forma de titulares de página, titulares en tablas o columnas y en lista. Por ejemplo, un lector de pantalla permite a un usuario navegar por una página de titular en titular. Sin embargo, cuando el contenido de una página solo parece contener una estructura a través de un estilo visual, en lugar de un formato HTML subyacente, quiere decir que no existe ninguna información estructural disponible para tecnologías de asistencia, lo que limita su capacidad de proporcionar una búsqueda más sencilla.

Este criterio de éxito pretende asegurar que esta información estructural se proporciona a través de HTML para que los buscadores y las tecnologías de asistencia puedan acceder a la información y aprovecharla.

#### Cómo cumplir: Información y relaciones (1.3.1)  {#how-to-meet-info-and-relationships}

AEM facilita construir páginas web utilizando los elementos HTML adecuados. Abra el contenido de su página en RTE (un componente de texto) y utilice el menú **Paraformato** (símbolo de párrafo) para especificar el elemento estructural adecuado (por ejemplo, párrafos, titulares, etc.).

Puede comprobar que sus páginas web contienen la estructura adecuada mediante:

* **Uso de encabezados:** Siempre y cuando tenga las funciones de accesibilidad de RTE activadas, AEM ofrece 3 niveles de encabezado de página. Puede utilizarlas para identificar secciones y subsecciones de contenido. El encabezado 1 es el nivel más alto, mientras que el encabezado 3 es el más bajo. El administrador del sistema puede configurar el sistema para permitir el uso de más niveles de encabezado.
* **Texto enfatizado**: Utilice el elemento `<strong>` o `<em>` para indicar el énfasis. No utilice encabezados o texto enfatizado en los párrafos.
   * Enfatice el texto que quiera remarcar;
   * Haga clic en el icono **B** (para `<strong>`) o en el icono **I** (para `<em>`) que se muestra en el panel de **Propiedades** (asegúrese de que está seleccionada la opción HTML).

      >[!NOTE]
      >
      >RTE en una instalación AEM estándar está configurada para utilizar:
      >
      >* `<b>` para `<strong>`
      >* `<i>` para `<em>`
      >
      >Aunque son igual de eficaces, `<strong>` y `<em>` son preferibles porque son HTML semánticamente correctos. Su equipo de desarrollo puede configurar el RTE para utilizar `<strong>` y `<em>` (en lugar de `<b>` y `<i>`) cuando desarrolle su proyecto.


* **Utilizar listas**:
Es posible utilizar HTML para especificar tres tipos de listas distintas.
   * El elemento `<ul>` se utiliza para listas *desordenadas* (o listas con viñetas). Los elementos de listas individuales se identifican utilizando el elemento `<li>`. En RTE, utilice el icono de **Lista con viñetas**.
   * El elemento `<ol>` se utiliza para listas *numeradas*. Los elementos de listas individuales se identifican utilizando el elemento `<li>`. En RTE, utilice el icono **Lista numerada** .
   Si desea cambiar contenido existente por un tipo de lista específica, remarque el texto adecuado y seleccione el tipo de lista adecuado. Como en el ejemplo anterior, en el que se mostraba cómo se introducía texto en formato párrafo, los elementos de la lista adecuada se añaden automáticamente a su HTML.

   En el modo de pantalla completa, están visibles los iconos individuales **Lista con viñetas** y **Lista numerada**. Cuando no se encuentra en modo de pantalla completa, las dos opciones están disponibles detrás del icono de una **Listas**.
* **Use tablas**: las tablas de datos deben identificarse utilizando elementos de tablas HTML:
   * un elemento `<table>`
   * un elemento `<tr>` para cada fila de la tabla
   * un elemento `<th>` para cada titular de fila y columna
   * un elemento `<td>` para cada celda de datos
   Además, las tablas accesibles utilizan los siguientes elementos y atributos:

   * El elemento `<caption>` se utiliza para proporcionar un subtítulo visible para la tabla. Los subtítulos por defecto aparecen centrados debajo de la tabla, pero se pueden posicionar de cualquier otra manera adecuada utilizando CSS. El subtítulo está asociado programáticamente con la tabla, por lo que se trata de un método útil para proporcionar una introducción al contenido.
   * El elemento `<summary>` ayuda a los usuarios que carecen de visión para que entiendan con mayor facilidad la información que se presenta en la tabla mediante una sinopsis de lo que el usuario puede ver. Resulta particularmente útil cuando se utilizan diseños de la tabla complejos o poco convencionales (este atributo no se muestra en el buscador, solo se lee en voz alta para tecnologías de asistencia).
   * El atributo `scope` del elemento `<th>` se utiliza para indicar si una celda representa el encabezado de una fila en concreto o de una columna en concreto. Un enfoque similar es el de utilizar el encabezado y los atributos de identificación en tablas complejas, donde las celdas de datos se pueden asociar con uno o más encabezados.
   >[!NOTE]
   >
   >Por defecto, estos elementos y atributos no se encuentran disponibles directamente, aunque es posible que el administrador del sistema añada cierta ayuda para estos valores en el cuadro de diálogo **Propiedades de la tabla** (consulte Agregar ayuda para elementos y atributos HTML adicionales).

<!-- removed link syntax for ExL - Bob Bringhurst
>By default, these elements and attributes are not directly available, though it is possible for the system administrator to add support for these values in the **Table properties** dialog box (see Adding Support for Additional HTML Elements and Attributes /help/sites-administering/rte-accessible-content.md#adding-support-for-additional-html-elements-and-attributes).
-->

Para abrir el cuadro de diálogo **Tabla**, seleccione la pestaña **Propiedades de la tabla**:

* Defina un **subtítulo** adecuado.
* Idealmente, elimine los valores predeterminados de **anchura**, **altura**, **borde**, **relleno de celda** y **espaciado de celda**, ya que estas propiedades se pueden definir en una hoja de estilo global.

Puede utilizar las **propiedades de la celda** para decidir si la celda es una celda de datos o de encabezado:

* **Tablas de datos complejos**: en algunos casos en los que hay tablas complejas con dos o más niveles de encabezados, las Propiedades de la tabla básicas pueden no ser suficientes para proporcionar toda la información estructural necesaria. Para este tipo de tablas complejas es necesario crear relaciones directas entre los encabezados y sus celdas utilizando el **encabezado** y **atributos de identificación**. Por ejemplo, en la tabla siguiente, los encabezados y las identificaciones se comparan para crear una asociación programática para los usuarios de tecnología de asistencia.

   >[!NOTE]
   >
   >El atributo de identificación no se encuentra disponible en una instalación lista para usar. Se puede activar configurando las normas HTML y el serializador en RTE.

```xml
 <table>
    <tr>
      <th rowspan="2" id="h">Homework</th>
      <th colspan="3" id="e">Exams</th>
      <th colspan="3" id="p">Projects</th>
    </tr>
    <tr>
      <th id="e1" headers="e">1</th>
      <th id="e2" headers="e">2</th>
      <th id="ef" headers="e">Final</th>
      <th id="p1" headers="p">1</th>
      <th id="p2" headers="p">2</th>
      <th id="pf" headers="p">Final</th>
    </tr>
    <tr>
     <td headers="h">15%</td>
     <td headers="e e1">15%</td>
     <td headers="e e2">15%</td>
     <td headers="e ef">20%</td>
     <td headers="p p1">10%</td>
     <td headers="p p2">10%</td>
     <td headers="p pf">15%</td>
    </tr>
   </table>
```

Para conseguirlo en AEM, añada las especificaciones directamente utilizando el modo de edición de la fuente.

>[!NOTE]
>
>Esta funcionalidad no está inmediatamente disponible en una instalación estándar. Requiere una configuración de RTE, normas HTML y un serializador.

#### Más información: Información y relaciones (1.3.1) {#more-information-info-and-relationships}

* [Entender los criterios de éxito 1.3.1](https://www.w3.org/WAI/WCAG21/Understanding/info-and-relationships.html)
* [Cumplir los criterios de éxito 1.3.1](https://www.w3.org/WAI/WCAG21/quickref/#info-and-relationships)

### Secuencia significativa (1.3.2) {#meaningful-sequence}

* Criterios de éxito 1.3.2
* Nivel A
* Secuencia significativa: Cuando la secuencia en la que se presenta el contenido afecta a su significado, se puede determinar mediante programación una secuencia de lectura correcta.

#### Objetivo: Secuencia significativa (1.3.2) {#purpose-meaningful-sequence}

El propósito de este criterio de éxito es permitir que un agente de usuario proporcione una presentación alternativa del contenido, preservando al mismo tiempo el orden de lectura necesario para comprender el significado. Es importante que sea posible determinar mediante programación al menos una secuencia del contenido que tenga sentido. El contenido que no cumpla estos criterios de éxito puede confundir o desorientar a los usuarios cuando la tecnología de asistencia lee el contenido en un orden incorrecto, o cuando se aplican hojas de estilo alternativas u otros cambios de formato.

#### Secuencia significativa (1.3.2) {#how-to-meet-meaningful-sequence}

Siga las directrices de [Cumplir los criterios de éxito 1.3.2](https://www.w3.org/WAI/WCAG21/quickref/#meaningful-sequence).

#### Más información: Secuencia significativa (1.3.2) {#more-information-meaningful-sequence}

* [Entender los criterios de éxito 1.3.2](https://www.w3.org/WAI/WCAG21/Understanding/meaningful-sequence.html)
* [Cumplir los criterios de éxito 1.3.2](https://www.w3.org/WAI/WCAG21/quickref/#meaningful-sequence)

### Características sensoriales (1.3.3)          {#sensory-characteristics}

* Criterios de éxito 1.3.3
* Nivel A
* Características sensoriales: las instrucciones que se proporcionan para entender el contenido y operar con él no se basan solo en características sensoriales de componentes como la forma, el tamaño, la ubicación visual, la orientación o el sonido

#### Objetivo: Características sensoriales (1.3.3)     {#purpose-sensory-characteristics}

Los diseñadores normalmente se centran en características de diseño visuales tales como el color, la forma, el estilo del texto o una parte de la ubicación absoluta o relativa del contenido donde se presenta la información. Estas pueden ser técnicas de diseño muy poderosas para transmitir información, pero las personas ciegas o con limitaciones de visión puede que no consigan acceder a la información que requiere identificación visual de atributos como la ubicación, el color o la forma.

De la misma manera, la información que requiere distinguir entre sonidos distintos (como contenido cuya voz es masculina o femenina) presentará barreras de accesibilidad para las personas que sufran limitaciones auditivas si el contenido del audio no se refleja en un texto alternativo.

>[!NOTE]
>
>Para los requisitos relativos a las alternativas de color, consulte [Uso del color](#use-of-color).

#### Cómo cumplir: Características sensoriales (1.3.3)  {#how-to-meet-sensory-characteristics}

Asegúrese de que cualquier información relativa a las características visuales del contenido de una página se presente también en un formato alternativo.

* Es importante no basarse en la posición visual para dar información. Por ejemplo, para dirigir a los usuarios hacia un menú a la derecha de la página para que accedan a más información, no se debe hacer referencia al *menú de la derecha*; en lugar de eso, es preferible nombrar el menú (por ejemplo mediante un encabezado) y hacer referencia a ese nombre en el texto.
* También es importante no basarse en el estilo del texto (por ejemplo si se trata de texto en negrita o en cursiva) como la única manera de transmitir la información.

>[!NOTE]
>
>El uso de términos descriptivos se puede considerar aceptable si estos se entienden por su significado en un contexto no visual. Por ejemplo, utilizar *arriba* y *abajo* generalmente estaría aceptado, porque respectivamente implican contenido antes y después de un elemento particular del contexto; tendría sentido cuando el contenido se lee en voz alta.

#### Más información: Características sensoriales (1.3.3)     {#more-information-sensory-characteristics}

* [Entender los criterios de éxito 1.3.3](https://www.w3.org/WAI/WCAG21/Understanding/sensory-characteristics.html)
* [Cumplir los criterios de éxito 1.3.3](https://www.w3.org/WAI/WCAG21/quickref/#sensory-characteristics)

### Distinguible (1.4)     {#distinguishable}

[Directrices 1.4 Distinguible: Facilitar a los usuarios ver y oír el contenido incluyendo la posibilidad de separar el primer plano del fondo.](https://www.w3.org/TR/WCAG/#distinguishable)

### Uso del color (1.4.1)          {#use-of-color}

* Criterios de éxito 1.4.1
* Nivel A
* Uso del color: el color no es el único medio visual para transmitir información, indicar una acción, una respuesta o distinguir un elemento visual

>[!NOTE]
>
>Este criterio de éxito se dirige específicamente a la percepción del color. Otras formas de percepción se tratan en [Adaptable (1.3)](#adaptable); incluyendo el acceso programático al color y otros códigos de presentación visual.

#### Objetivo: Uso del color (1.4.1)     {#purpose-use-of-color}

El color es, obviamente, una manera efectiva de resaltar el atractivo estético de las páginas web y también resulta útil para transmitir información. Sin embargo, existe una variedad de impedimentos visuales, desde la ceguera hasta la deficiencia de la percepción del color, que supone que hay personas que no pueden distinguir entre ciertos colores. Esto hace que la codificación de colores sea una manera poco fiable de transmitir información.

Por ejemplo, una persona con una deficiencia de la percepción entre el color rojo y el verde no podrá distinguir entre las gamas de verdes y las gamas de rojos. Puede que esta persona vea ambos colores como un tercer color (por ejemplo, marrón), en cuyo caso no podrá distinguir entre el verde, el rojo y el marrón.

Además, las personas que utilizan navegadores de solo texto, dispositivos de pantallas monocromáticas o páginas en blanco y negro no pueden percibir el color.

#### Cómo cumplir: Uso del color (1.4.1)  {#how-to-meet-use-of-color}

En todos los casos donde el color se utilice para transmitir información, es importante asegurarse de que la información se encuentra disponible sin necesidad de ver el color.

Por ejemplo, asegúrese de que la información que proporciona el color también esté explícita en el texto.

Si el color se utiliza como señal para proporcionar información, debe proporcionar una señal visual adicional, como un cambio de estilo (por ejemplo, negrita, cursiva) o de fuente. Esto ayuda a las personas con problemas de visión o a la hora de percibir el color a identificar la información. Sin embargo, no se puede confiar en esta medida totalmente puesto que no ayudaría a aquellos que no puedan ver la página.

#### Más información: Uso del color (1.4.1) {#more-information-use-of-color}

* [Entender los criterios de éxito 1.4.1](https://www.w3.org/WAI/WCAG21/Understanding/use-of-color.html)
* [Cumplir los criterios de éxito 1.4.1](https://www.w3.org/WAI/WCAG21/quickref/#use-of-color)

<!-- [Guidance on meeting a 3:1 contrast ratio, containing a list of “web safe” colors](https://www.w3.org/TR/2008/NOTE-WCAG20-TECHS-20081211/working-examples/G183/link-contrast.html)
-->

### Control de audio (1.4.2) {#audio-control}

* Criterios de éxito 1.4.2
* Nivel A
* Control de audio: Si el audio de una página Web se reproduce automáticamente durante más de 3 segundos, hay un mecanismo disponible para pausar o detener el audio, o bien un mecanismo para controlar el volumen del audio independientemente del nivel de volumen total del sistema.

#### Objetivo: Control de audio (1.4.2) {#purpose-audio-control}

A las personas que utilizan software de lectura de pantalla les resulta difícil escuchar la salida de voz si se reproduce otro audio al mismo tiempo. Esta dificultad se agrava cuando la salida de voz del lector de pantalla se basa en software (como la mayoría de los actuales) y se controla mediante el mismo control de volumen que el sonido. Por lo tanto, es importante que el usuario pueda desactivar el sonido de fondo. Nota: Tener el control del volumen incluye poder reducir su volumen a cero.

#### Control de audio (1.4.2) {#how-to-meet-audio-control}

Siga las directrices de [Cumplir los criterios de éxito 1.4.2](https://www.w3.org/WAI/WCAG21/quickref/#audio-control).

#### Más información: Control de audio (1.4.2) {#more-information-audio-control}

* [Entender los criterios de éxito 1.4.2](https://www.w3.org/WAI/WCAG21/Understanding/audio-control.html)
* [Cumplir los criterios de éxito 1.4.2](https://www.w3.org/WAI/WCAG21/quickref/#audio-control)

### Contraste (mínimo) (1.4.3)     {#contrast-minimum}

* Criterios de éxito 1.4.3
* Nivel AA
* Contraste (mínimo): la presentación visual del texto y las imágenes de texto tiene una relación de contraste de al menos 4.5:1, excepto los siguientes:
   * Texto grande: el texto y las imágenes de texto a gran escala mantienen una relación de contraste de al menos 3:1.
   * Secundario: el texto o las imágenes de texto que forman parte de un componente de interfaz de usuario inactivo, que son puramente decorativos, que no son visibles para nadie o que forman parte de una fotografía que contiene otro contenido visual significativo no cuentan con requisitos de contraste.
   * Logotipos: el texto que forma parte de un logotipo o del nombre de una marca no cuenta con un requisito mínimo de contraste.

#### Objetivo: Contraste (mínimo) (1.4.3)     {#purpose-contrast-minimum}

Las personas con ciertas deficiencias visuales quizá no puedan distinguir entre ciertas parejas de colores de poco contraste. Estas personas pueden sufrir problemas de accesibilidad si:

* El texto contrasta poco con el color del fondo.
* El código de color del texto (como el texto con vínculo y el texto sin vínculo) es importante para distinguir la información.

>[!NOTE]
>
>El texto que se utiliza con fines puramente decorativos se excluye de estos criterios de éxito.

#### Cómo cumplir: Cumplir los criterios de contraste (Mínimo) (1.4.3)  {#how-to-meet-contrast-minimum}

Asegúrese de que el texto contrasta lo suficiente con el fondo. Las relaciones de contraste dependen del tamaño y del estilo del texto en cuestión:

* Para los textos cuyo tamaño es menor de 18 puntos (o 14 puntos en negrita), la relación de contraste entre el texto o las imágenes del texto y el fondo debería ser de al menos 4.5:1.
* Para los textos cuyo tamaño es de al menos 18 puntos (o 14 puntos en negrita), la relación de contraste debería ser de al menos 3:1.
* Ante un fondo estampado, el fondo alrededor de cualquier texto debería estar sombreado para que la relación 4.5:1 o 3:1 se mantenga.

Para comprobar los niveles de contraste, utilice una herramienta de contraste de color como el programa [Paciello Group Color Contrast Analyser](https://www.paciellogroup.com/resources/contrast-analyser.html) o el [verificador de contraste de color WebAIM](https://www.webaim.org/resources/contrastchecker/). Estas herramientas permiten comprobar las parejas de color e informar de cualquier problema de contraste.

Alternativamente, si no le preocupa especificar la apariencia de su página, puede optar por no especificar el color del fondo o del texto en primer plano. No es necesario comprobar el contraste, ya que el navegador del usuario determinará los colores del texto y del fondo.

Si no se pueden cumplir los niveles de contraste recomendados tendrá que proporcionar un vínculo a una versión alternativa y equivalente de la página (que no presente problemas de contraste de color) o permitir al usuario ajustar el contraste del esquema de color de la página bajo su propio criterio.

#### Más información: Contraste (mínimo) (1.4.3)     {#more-information-contrast-minimum}

* [Entender los criterios de éxito 1.4.3](https://www.w3.org/WAI/WCAG21/Understanding/contrast-minimum.html)
* [Cumplir los criterios de éxito 1.4.3](https://www.w3.org/WAI/WCAG21/quickref/#contrast-minimum)

### Cambiar el tamaño del texto (1.4.4) {#resize-text}

* Criterios de éxito 1.4.4
* Nivel A
* Cambiar el tamaño del texto: Excepto para rótulos e imágenes de texto, el texto puede cambiarse de tamaño sin tecnología de asistencia hasta un 200 por ciento sin pérdida de contenido o funcionalidad.

#### Objetivo: Cambiar el tamaño del texto (1.4.4) {#purpose-resize-text}

El propósito de este criterio de éxito es garantizar que el texto procesado visualmente, incluidos los controles basados en texto (caracteres de texto que se han mostrado para que se puedan ver [vs. caracteres de texto que siguen en formato de datos como ASCII]), se pueda escalar correctamente para que pueda ser leído directamente por personas con discapacidades visuales leves, sin necesidad de utilizar tecnología de asistencia como un ampliador de pantalla. Los usuarios pueden beneficiarse de la escala de todo el contenido de la página Web, pero el texto es muy importante.

#### Redimensionar texto (1.4.4) {#how-to-meet-resize-text}

Siga las directrices de [Cumplir los criterios de éxito 1.4.4](https://www.w3.org/WAI/WCAG21/quickref/#resize-text).

#### Más información: Cambiar el tamaño del texto (1.4.4) {#more-information-resize-text}

* [Entender los criterios de éxito 1.4.4](https://www.w3.org/WAI/WCAG21/Understanding/resize-text.html)
* [Cumplir los criterios de éxito 1.4.4](https://www.w3.org/WAI/WCAG21/quickref/#resize-text)

### Imágenes de texto (1.4.5)     {#images-of-text}

* Criterios de éxito 1.4.5
* Nivel AA
* Imágenes de texto: si las tecnologías que se utilizan consiguen la presentación visual, el texto se utiliza para proporcionar información (y no las imágenes de texto), excepto en los casos siguientes:
   * Personalizable: la imagen de texto se puede personalizar visualmente bajo los requisitos del usuario;
   * Esencial: una presentación de texto en concreto resulta esencial para que se transmita la información.

>[!NOTE]
>
>Logotipos (texto que forma parte de un logotipo o del nombre de la marca) se consideran esenciales.

#### Objetivo: Imágenes de texto (1.4.5)     {#purpose-images-of-text}

Las imágenes de texto normalmente se utilizan cuando se prefiere un tipo de texto en particular; por ejemplo un logotipo, o si un texto se ha generado desde otra fuente (por ejemplo un documento físico escaneado). Sin embargo, comparadas con el texto presentado en HTML y cuyo estilo utiliza CSS, las imágenes de texto carecen de la flexibilidad de cambiar su tamaño o apariencia que podría resultar necesaria para las personas con deficiencias visuales o dificultades de lectura.

#### Cómo cumplir: Imágenes de texto (1.4.5)  {#how-to-meet-images-of-text}

Si es necesario utilizar imágenes de texto, utilice CSS para reemplazar las imágenes de texto con texto equivalente en HTML y así el texto estará disponible en un modo personalizable. Para mostrar un ejemplo de cómo se puede conseguir, consulte [C30: Utilizar CSS para reemplazar texto con imágenes de texto y proporcionar al usuario controles de interfaz que pueda cambiar](https://www.w3.org/TR/2008/NOTE-WCAG20-TECHS-20081211/C30).

#### Más información: Imágenes de texto (1.4.5)     {#more-information-images-of-text}

* [Entender los criterios de éxito 1.4.5](https://www.w3.org/WAI/WCAG21/Understanding/images-of-text.html)
* [Cumplir los criterios de éxito 1.4.5](https://www.w3.org/WAI/WCAG21/quickref/#images-of-text)

## Principio 2: operable     {#principle-operable}

[Principio 2: operable. Los componentes y la navegación de interfaz de usuario deben ser operables.](https://www.w3.org/TR/WCAG/#operable)

### Teclado accesible (2.1) {#keyboard-accessible}

[Teclado de guía 2.1 accesible: Haga que toda la funcionalidad esté disponible desde un teclado.](https://www.w3.org/TR/WCAG/#keyboard-accessible)

Se trata de garantizar que los usuarios puedan acceder a todas las funciones mediante un teclado.

### Teclado (2.1.1) {#keyboard}

* Criterios de éxito 2.1.1
* Nivel A
* Teclado: Toda la funcionalidad del contenido se puede utilizar mediante una interfaz de teclado sin necesidad de tiempos específicos para pulsaciones de teclas individuales, excepto cuando la función subyacente requiere una entrada que depende de la ruta del movimiento del usuario y no sólo de los extremos.

#### Objetivo: Teclado (2.1.1) {#purpose-keyboard}

El propósito de este criterio de éxito es garantizar que, siempre que sea posible, el contenido se pueda utilizar mediante un teclado o una interfaz de teclado (de modo que se pueda utilizar un teclado alternativo). Cuando el contenido se puede utilizar mediante un teclado o un teclado alternativo, lo pueden utilizar personas sin visión (que no pueden utilizar dispositivos como ratones que requieren coordinación visual), así como personas que deben utilizar teclados alternativos o dispositivos de entrada que actúen como emuladores de teclado. Los emuladores de teclado incluyen software de entrada de voz, software para sortear y sacar, teclados en pantalla, software de digitalización y una variedad de tecnologías de asistencia y teclados alternativos. Las personas con visión reducida también pueden tener problemas para rastrear un puntero y encontrar el uso de software mucho más fácil (o sólo posible) si pueden controlarlo desde el teclado.

#### Teclado (2.1.1) {#how-to-meet-keyboard}

Siga las directrices de [Cumplir los criterios de éxito 2.1.1](https://www.w3.org/WAI/WCAG21/quickref/#keyboard).

#### Más información: Teclado (2.1.1) {#more-information-keyboard}

* [Entender los criterios de éxito 2.1.1](https://www.w3.org/WAI/WCAG21/Understanding/no-keyboard-trap.html)
* [Cumplir los criterios de éxito 2.1.1](https://www.w3.org/WAI/WCAG21/quickref/#keyboard)

### Sin captura de teclado (2.1.2) {#no-keyboard-trap}

* Criterios de éxito 2.1.2
* Nivel A
* Sin reventado de teclado: Si el enfoque del teclado se puede mover a un componente de la página mediante una interfaz de teclado, el enfoque se puede alejar de ese componente utilizando sólo una interfaz de teclado y, si requiere más teclas de flecha o tabulación sin modificar u otros métodos de salida estándar, se informará al usuario del método para desplazar el enfoque.

#### Objetivo: Sin reventado del teclado (2.1.2) {#purpose-no-keyboard-trap}

El propósito de este criterio de éxito es garantizar que el contenido no *atrape* el enfoque del teclado dentro de subsecciones de contenido en una página Web. Este es un problema común cuando se combinan varios formatos dentro de una página y se procesan con complementos o aplicaciones incrustadas.

Puede haber ocasiones en las que la funcionalidad de la página Web restrinja el enfoque a una subsección del contenido, siempre y cuando el usuario sepa cómo dejar ese estado y *anular la captura* del enfoque.

#### Cumplir: sin trampa de teclado (2.1.2) {#how-to-meet-no-keyboard-trap}

Siga las directrices de [Cumplir los criterios de éxito 2.1.2](https://www.w3.org/WAI/WCAG21/quickref/#no-keyboard-trap).

#### Más información: Sin captura de teclado (2.1.2) {#more-information-no-keyboard-trap}

* [Entender los criterios de éxito 2.1.2](https://www.w3.org/WAI/WCAG21/Understanding/no-keyboard-trap.html)
* [Cumplir los criterios de éxito 2.1.2](https://www.w3.org/WAI/WCAG21/quickref/#no-keyboard-trap)

### Tiempo suficiente (2.2) {#enough-time}

[Directrices 2.2 Tiempo suficiente: Proporcione a los usuarios tiempo suficiente para leer y utilizar el contenido.](https://www.w3.org/TR/WCAG/#enough-time)

Esto se centra en garantizar que los usuarios tengan tiempo suficiente para leer y realizar acciones.

### Temporización ajustable (2.2.1) {#timing-adjustable}

* Criterios de éxito 2.2.1
* Nivel A
* Teclado: Proporcione a los usuarios tiempo suficiente para leer y utilizar el contenido.

#### Objetivo: Temporización ajustable (2.2.1) {#purpose-timing-adjustable}

El propósito de este criterio de éxito es garantizar que los usuarios con discapacidades tengan tiempo suficiente para interactuar con el contenido web siempre que sea posible. Las personas con discapacidades como ceguera, visión reducida, impedimentos de destreza y limitaciones cognitivas pueden requerir más tiempo para leer contenido o para realizar funciones como rellenar formularios en línea. Si las funciones Web dependen del tiempo, algunos usuarios tendrán dificultades para realizar la acción necesaria antes de que se produzca un límite de tiempo. Esto puede hacer que el servicio sea inaccesible para ellos. El diseño de funciones que no dependen del tiempo ayudará a las personas con discapacidades a completar estas funciones. El suministro de opciones para deshabilitar los límites de tiempo, personalizar la duración de los límites de tiempo o solicitar más tiempo antes de que se produzca un límite de tiempo ayuda a los usuarios que necesitan más tiempo del esperado para completar correctamente las tareas. Estas opciones se enumeran en el orden que resultará más útil para el usuario. Deshabilitar los límites de tiempo es mejor que personalizar la longitud de los límites de tiempo, lo que es mejor que solicitar más tiempo antes de que se produzca un límite de tiempo.

#### Calendario ajustable (2.2.1) {#how-to-meet-timing-adjustable}

Siga las directrices de [Cumplir los criterios de éxito 2.2.1](https://www.w3.org/WAI/WCAG21/quickref/#timing-adjustable).

#### Más información: Temporización ajustable (2.2.1) {#more-information-timing-adjustable}

* [Entender los criterios de éxito 2.2.1](https://www.w3.org/WAI/WCAG21/Understanding/timing-adjustable.html)
* [Cumplir los criterios de éxito 2.2.1](https://www.w3.org/WAI/WCAG21/quickref/#timing-adjustable)

### Pausar, parar, ocultar (2.2.2)          {#pause-stop-hide}

* Criterios de éxito 2.2.2
* Nivel A
* Pausar, parar, ocultar: Para mover, cerrar, desplazar o actualizar automáticamente la información, los siguientes criterios son verdaderos:  
   * Mover, cerrar, desplazar: Para mover, cerrar o desplazar cualquier tipo de información que (a) empiece de manera automática, (b) dure más de cinco segundos y (c) se presente en paralelo con otro contenido, existe un mecanismo que el usuario puede utilizar para pausar, parar u ocultar la información, a menos que mover, cerrar o desplazar dicha información forme parte de una actividad en la que sea esencial;
   * Actualizar automáticamente: Para actualizar de manera automática cualquier tipo de información que (a) empiece de manera automática y (b) se presente en paralelo con otro contenido, existe un mecanismo que el usuario puede utilizar para pausar, parar u ocultar la información, o para controlar la frecuencia de la actualización, a menos que actualizar automáticamente dicha información forme parte de una actividad en la que sea esencial.

Puntos que se deben tener en cuenta:

1. Para ver los requisitos relacionados con contenidos que parpadean, consulte No diseñar contenido de manera que cause parpadeos (2.3).
1. Ya que cualquier contenido que no cumpla estos criterios de éxito puede interferir en la capacidad de un usuario para utilizar toda una página, todo el contenido de la página web (tanto si se utiliza para cumplir otros criterios como si no) debe cumplir este criterio de éxito. Consulte [Requisito de conformidad 5: no interferencia](https://www.w3.org/TR/WCAG20/#cc5).
1. El contenido que se actualiza periódicamente a través del software o que se transmite al usuario no necesita preservar o presentar la información que se genera o se recibe entre la iniciación de la pausa y la reanudación de la presentación, puesto que puede no ser técnicamente posible y en muchas situaciones podría ser engañoso.
1. Una animación en una fase de precarga o en una situación similar se consideraría esencial si la interacción no se pudiera dar durante dicha fase para todos los usuarios, y si no indicara el progreso podría confundirlos o llevarles a pensar que el contenido se ha congelado o se ha estropeado.

#### Objetivo: Pausar, parar, ocultar (2.2.2)     {#purpose-pause-stop-hide}

Algunos usuarios pueden considerar que el contenido que se mueve les distrae o les dificulta a la hora de concentrarse en otras partes de la página. Además, dicho contenido puede ser difícil de leer para quienes tienen problemas para seguir el texto que se mueve.

#### Cómo cumplir: Pausar, parar, ocultar (2.2.2)  {#how-to-meet-pause-stop-hide}

Según la naturaleza del contenido, se puede aplicar una o varias de las siguientes sugerencias al crear páginas web con contenido que se mueve o parpadea:

* Proporcionar la manera de pausar el movimiento del contenido y dar a los usuarios tiempo suficiente para leerlo. Por ejemplo, lectores de noticias o texto que se actualiza de manera automática.
* Asegurarse de que el contenido que parpadea deja de hacerlo tras cinco segundos.
* Utilizar tecnologías adecuadas para mostrar el contenido parpadeante que se puede mostrar en el navegador. Por ejemplo, archivos de Formato de intercambio de gráficos (GIF) o Gráficos de red portátiles animados (APNG).
* Proporcionar un formulario de control en la página web para permitir a los usuarios desactivar cualquier contenido que parpadee en la página.
* Si no es posible ninguno de los anteriores, proporcionar un vínculo a la página que contenga todo el contenido pero sin parpadeos.

#### Más información: Pausar, parar, ocultar (2.2.2)     {#more-information-pause-stop-hide}

* [Entender los criterios de éxito 2.2.2](https://www.w3.org/WAI/WCAG21/Understanding/pause-stop-hide.html)
* [Cumplir los criterios de éxito 2.2.2](https://www.w3.org/WAI/WCAG21/quickref/#pause-stop-hide)

### Convulsiones y reacciones físicas (2.3) {#seizures-and-physcial-reactions}

[Directriz 2.3 Convulsiones: No diseñe el contenido de una manera que se sepa que causa convulsiones o reacciones físicas.](https://www.w3.org/TR/WCAG/#seizures-and-physical-reactions)

### Tres parpadeos o por debajo de los límites (2.3.1)     {#three-flashes-or-below-threshold}

* Criterios de éxito 2.3.1
* Nivel A
* Tres parpadeos o Por debajo de los límites: las páginas web no contienen ningún elemento que parpadee más de tres veces en el período de un segundo o que esté por debajo del parpadeo general y los indicadores del parpadeo rojo

>[!NOTE]
>
>Ya que cualquier contenido que no cumpla estos criterios de éxito puede interferir en la capacidad de un usuario para utilizar toda una página, todo el contenido de la página web (tanto si se utiliza para cumplir otros criterios como si no) debe cumplir este criterio de éxito. Consulte [Requisito de conformidad 5: no interferencia](https://www.w3.org/TR/WCAG/#cc5).

#### Objetivo: Tres parpadeos o Por debajo de los límites (2.3.1) {#purpose-three-flashes-or-below-threshold}

En ciertos casos, el contenido que parpadea puede causar parpadeos fotosensibles. Este criterio de éxito permite a los usuarios acceder y experimentar todo el contenido sin tener que preocuparse por el contenido parpadeante.

#### Cómo cumplir: Tres parpadeos o por debajo de los límites (2.3.1)  {#how-to-meet-three-flashes-or-below-threshold}

Siga estos pasos para asegurarse de que se aplican las siguientes técnicas:

* Asegúrese de que los componentes no parpadean más de tres veces durante el período de un segundo;
* Si no se cumple la condición anterior, muestre el contenido parpadeante en una zona *pequeña y segura* en píxeles en la pantalla. Esta zona se calcula utilizando una fórmula compleja que se recoge en [G176: Hacer que la zona parpadeante sea lo suficientemente reducida](https://www.w3.org/TR/2008/NOTE-WCAG20-TECHS-20081211/G176), por lo que esta técnica solo se debe utilizar si el contenido que parpadea es *absolutamente* necesario.

#### Más información: Tres parpadeos o por debajo de los límites (2.3.1) {#more-information-three-flashes-or-below-threshold}

* [Entender los criterios de éxito 2.3.1](https://www.w3.org/WAI/WCAG21/Understanding/three-flashes-or-below-threshold.html)
* [Cumplir los criterios de éxito 2.3.1](https://www.w3.org/WAI/WCAG21/quickref/#three-flashes-or-below-threshold)

### Navegable (2.4) {#navigable}

[Directrices 2.4 Navegable: Proporcione formas de ayudar a los usuarios a navegar, encontrar contenido y determinar dónde se encuentran.](https://www.w3.org/TR/WCAG/#navigable)

Esto garantiza que el contenido sea fácil y sencillo de navegar para los usuarios.

### Omitir bloques (2.4.1) {#bypass-blocks}

* Criterios de éxito 2.4.1
* Nivel A
* Omitir bloques: Existe un mecanismo disponible para evitar bloques de contenido que se repiten en varias páginas Web.

#### Objetivo: Omitir bloques (2.4.1) {#purpose-bypass-blocks}

El propósito de este criterio de éxito es permitir que las personas que navegan secuencialmente a través del contenido tengan un acceso más directo al contenido principal de la página Web. Las páginas Web y las aplicaciones suelen tener contenido que aparece en otras páginas o pantallas. Algunos ejemplos de bloques repetidos de contenido son, entre otros, los vínculos de navegación, los gráficos de encabezados y los marcos publicitarios. Las secciones pequeñas repetidas, como palabras individuales, frases o vínculos únicos, no se consideran bloques a los efectos de esta disposición.

#### Cómo cumplir: Omitir bloques (2.4.1) {#how-to-meet-bypass-blocks}

Siga las directrices de [Cumplir los criterios de éxito 2.4.1](https://www.w3.org/WAI/WCAG21/quickref/#bypass-blocks).

#### Más información: Omitir bloques (2.4.1) {#more-information-bypass-blocks}

* [Entender los criterios de éxito 2.4.1](https://www.w3.org/WAI/WCAG21/Understanding/bypass-blocks.html)
* [Cumplir los criterios de éxito 2.4.1](https://www.w3.org/WAI/WCAG21/quickref/#bypass-blocks)

### Página titulada (2.4.2)          {#page-titled}

* Criterios de éxito 2.4.2
* Nivel A
* Página titulada: las páginas web tienen títulos que describen el tema o el objetivo de estas

#### Objetivo: Página titulada (2.4.2)     {#purpose-page-titled}

Este criterio de éxito ayuda a todo el mundo, independientemente de cualquier discapacidad en concreto, a identificar de manera rápida el contenido de una página web sin tener que leerla entera. Es particularmente útil cuando se abren varias páginas web en pestañas del navegador, ya que el título de la página se muestra en la pestaña y por eso se puede localizar rápidamente.

#### Cómo cumplir: Página titulada (2.4.2)  {#how-to-meet-page-titled}

Al crear una página HTML nueva en AEM, se puede especificar el título de la página. Asegúrese de que el título describe adecuadamente el contenido de la página para que los usuarios puedan identificar rápidamente si el contenido es relevante o no para sus necesidades.

También puede editar el título de página al editarla. Se puede acceder a él mediante **Información de página** - **Propiedades.**

#### Más información: Página titulada (2.4.2) {#more-information-page-titled}

* [Entender los criterios de éxito 2.4.2](https://www.w3.org/WAI/WCAG21/Understanding/page-titled.html)
* [Cumplir los criterios de éxito 2.4.2](https://www.w3.org/WAI/WCAG21/quickref/#page-titled)

### Orden de enfoque (2.4.3) {#focus-order}

* Criterios de éxito 2.4.3
* Nivel A
* Orden de enfoque: Si una página Web se puede navegar secuencialmente y las secuencias de navegación afectan al significado o al funcionamiento, los componentes enfocables reciben atención en un orden que preserva el significado y la operabilidad.

#### Objetivo: Orden de enfoque (2.4.3) {#purpose-focus-order}

El propósito de este criterio de éxito es garantizar que, cuando los usuarios navegan secuencialmente por el contenido, encuentren información en un orden que sea coherente con el significado del contenido y se pueda utilizar desde el teclado. Esto reduce la confusión al permitir que los usuarios formen un modelo mental consistente del contenido. Puede haber diferentes pedidos que reflejen las relaciones lógicas en el contenido. Por ejemplo, si se desplaza por los componentes de una tabla una fila a la vez o una columna a la vez, ambas reflejan las relaciones lógicas del contenido. Cualquiera de los dos pedidos puede cumplir estos criterios de éxito.

#### Orden de enfoque (2.4.3) {#how-to-meet-focus-order}

Siga las directrices de [Cumplir los criterios de éxito 2.4.3](https://www.w3.org/WAI/WCAG21/quickref/#focus-order).

#### Más información: Orden de enfoque (2.4.3) {#more-information-focus-order}

* [Entender los criterios de éxito 2.4.3](https://www.w3.org/WAI/WCAG21/Understanding/focus-order.html)
* [Cumplir los criterios de éxito 2.4.3](https://www.w3.org/WAI/WCAG21/quickref/#focus-order)

### Objetivo del vínculo (en contexto) (2.4.4)          {#link-purpose-in-context}

* Criterios de éxito 2.4.4
* Nivel A
* Objetivo del vínculo (en contexto): el objetivo de cada vínculo se puede determinar por el texto del vínculo en sí o por el texto del vínculo junto al contexto del vínculo determinado programáticamente, excepto cuando el objetivo del vínculo sea ambiguo para los usuarios en general

#### Objetivo: Objetivo del vínculo (en contexto) (2.4.4)     {#purpose-link-purpose-in-context}

Es muy importante indicar claramente la dirección del vínculo a través del texto del vínculo adecuado para todos los usuarios, independientemente de cualquier discapacidad. Esto ayuda a los usuarios a decidir si quieren seguir el vínculo o no. Para los usuarios con visión normal, un texto para el vínculo con sentido es extremadamente útil cuando hay varios vínculos en una página (particularmente si la página está muy cargada de texto), ya que el texto del vínculo proporciona una indicación más clara de la función del destino de la página. Mientras que los usuarios que utilizan tecnologías de asistencia, que pueden generar una lista de todos los vínculos en una misma página, pueden entender más fácilmente el texto del vínculo por el contexto.

#### Cómo cumplir: Objetivo del vínculo (en contexto) (2.4.4)  {#how-to-meet-link-purpose-in-context}

Sobre todo, es importante asegurarse de que el objetivo de un vínculo se describe con claridad en el texto del vínculo.

* Ejemplo incorrecto:
   * Texto: para obtener más información sobre las clases nocturnas de otoño de 2010, haga clic aquí.
   * Motivo: no indica el destino claramente y resulta ambiguo.
* Ejemplo correcto:
   * Texto: Clases nocturnas de otoño de 2010, más información.
   * Motivo: ajustando ligeramente el texto y la posición del vínculo se puede mejorar el texto del vínculo.

Los vínculos se tienen que redactar con coherencia en todas las páginas, especialmente en las barras de navegación. Por ejemplo, si un vínculo a una página en concreto se nombra como **Publicaciones** en una página, utilice ese mismo texto en otras páginas para mantener la coherencia.

Sin embargo, en el momento de escribir, existen varios problemas en cuanto al uso de los títulos:

* El texto del atributo en el título generalmente se encuentra disponible solamente para los usuarios que utilizan el ratón como un consejo de herramienta emergente y no se puede acceder a él mediante el teclado. 
* Los lectores de pantalla pueden leer en voz alta los atributos de título, pero esta funcionalidad puede que no se permita por defecto, por lo que los usuarios pueden no estar al tanto de que existe un atributo de título.
* Es difícil cambiar la apariencia del texto del título, lo que quiere decir que puede resultar difícil o imposible de leer para algunas personas.

Por eso, mientras el atributo del título se puede utilizar para proporcionar contenido adicional a un vínculo, es importante tener en cuenta las limitaciones y no utilizarlo como alternativa para un texto de vínculo adecuado.

Cuando el vínculo esté formado por una imagen, asegúrese de que el texto alternativo de la imagen describe el destino del vínculo. Por ejemplo, si la imagen de una estantería es el vínculo a las publicaciones de una persona, el texto alternativo debería ser algo como **Publicaciones de John Smith** y no **Estantería**.

Alternativamente, si el anclaje del vínculo contiene texto que describe el objetivo del vínculo además de la imagen (y por ello el texto aparece junto a la imagen), utilice un atributo alternativo vacío para la imagen:

```xml
<a href="publications.html">
<img src = "bookshelf.jpg" alt = "" />
John Smith’s publications
</a>
```

>[!NOTE]
>
>El fragmento anterior representa una ilustración; es recomendable utilizar el componente **Imagen**.

Aunque es aconsejable proporcionar un texto para el vínculo que identifique su objetivo sin necesidad de contexto adicional, no siempre es posible. Los vínculos de contexto libre se pueden utilizar en los casos siguientes, cuyos ejemplos HTML se pueden encontrar en [Cumplir los criterios de éxito 2.4.4](https://www.w3.org/WAI/WCAG21/quickref/#link-purpose-in-context).

* Cuando el texto del vínculo forme parte de una lista de vínculos relacionados y cuando el elemento de la lista que incluye el vínculo proporcione contexto suficiente.
* Cuando el objetivo del vínculo se pueda identificar claramente gracias al párrafo *anterior* (y no gracias al siguiente).
* Cuando el vínculo aparezca incluido en una tabla de datos y el objetivo se pueda identificar claramente en los encabezados asociados.
* Cuando una lista de vínculos esté incluida en un conjunto de encabezados y el encabezado mismo proporcione un contexto adecuado.
* Cuando una lista de vínculos esté incluida en un vínculo alojado y el elemento de la lista superior encima del vínculo alojado proporcione un contexto adecuado.

En algunos casos en los que hay varios vínculos en una misma página (cada uno de los cuales proporciona la dirección de un vínculo con detalles complejos pero necesarios), puede resultar adecuado proporcionar una versión alternativa de la página web que muestre exactamente el mismo contenido pero donde el texto del vínculo no se detalle tanto.

Alternativamente, los guiones se pueden utilizar para proporcionar una cantidad mínima de texto en el vínculo, pero al activar un control adecuado orientado hacia la parte superior de la página, el texto del vínculo se *expande* hacia más detalles. Un enfoque similar sería utilizar CSS para *ocultar* el vínculo de la vista del usuario, pero imprimirlo en su totalidad para los usuarios del lector de pantalla. Esta cuestión queda fuera del ámbito de este documento, pero existe más información sobre cómo conseguirlo en la sección [Más información: Objetivo del vínculo (en contexto) (2.4.4)](#more-information-link-purpose-in-context).

#### Más información: Objetivo del vínculo (en contexto) (2.4.4) {#more-information-link-purpose-in-context}

* [Entender los criterios de éxito 2.4.4](https://www.w3.org/WAI/WCAG21/Understanding/link-purpose-in-context.html)
* [Cumplir los criterios de éxito 2.4.4](https://www.w3.org/WAI/WCAG21/quickref/#link-purpose-in-context)

<!--
* [C7: Using CSS to hide a portion of the link text](https://www.w3.org/TR/2008/NOTE-WCAG20-TECHS-20081211/C7)
-->

### Múltiples maneras (2.4.5) {#multiple-ways}

* Criterios de éxito 2.4.5
* Nivel AA
* Múltiples maneras: Hay más de una manera de localizar una página Web dentro de un conjunto de páginas Web, excepto cuando la página Web es el resultado de un proceso o un paso en él.

#### Objetivo: Múltiples maneras (2.4.5) {#purpose-multiple-ways}

El propósito de este criterio de éxito es hacer posible que los usuarios localicen el contenido de la manera que mejor se adapte a sus necesidades. Los usuarios pueden encontrar una técnica más fácil o comprensible de usar que otra.

Incluso los sitios pequeños deberían proporcionar a los usuarios algunos medios de orientación. Para un sitio de tres o cuatro páginas, con todas las páginas vinculadas desde la página de inicio, puede ser suficiente simplemente proporcionar vínculos desde y hacia la página de inicio donde los vínculos en la página de inicio también pueden servir como mapa del sitio.

#### Cumplir varias formas (2.4.5) {#how-to-meet-multiple-ways}

Siga las directrices de [Cumplir los criterios de éxito 2.4.5](https://www.w3.org/WAI/WCAG21/quickref/#multiple-ways).

#### Más información: varias formas (2.4.5) {#more-information-multiple-ways}

* [Entender los criterios de éxito 2.4.5](https://www.w3.org/WAI/WCAG21/Understanding/multiple-ways.html)
* [Cumplir los criterios de éxito 2.4.5](https://www.w3.org/WAI/WCAG21/quickref/#multiple-ways)

### Encabezados y etiquetas (2.4.6) {#headings-and-labels}

* Criterios de éxito 2.4.6
* Nivel AA
* Encabezados y etiquetas: Los encabezados y las etiquetas describen el tema o el propósito.

#### Objetivo: Encabezados y etiquetas (2.4.6) {#purpose-headings-and-labels}

El propósito de este criterio de éxito es ayudar a los usuarios a comprender qué información se incluye en las páginas Web y cómo se organiza dicha información. Cuando los encabezados son claros y descriptivos, los usuarios pueden encontrar la información que buscan más fácilmente y pueden comprender las relaciones entre las diferentes partes del contenido con mayor facilidad. Las etiquetas descriptivas ayudan a los usuarios a identificar componentes específicos dentro del contenido.

#### Encabezados y etiquetas (2.4.6) {#how-to-meet-headings-and-labels}

Siga las directrices de [Cumplir los criterios de éxito 2.4.6](https://www.w3.org/WAI/WCAG21/quickref/#headings-and-labels).

#### Más información: Encabezados y etiquetas (2.4.6) {#more-information-headings-and-labels}

* [Entender los criterios de éxito 2.4.6](https://www.w3.org/WAI/WCAG21/Understanding/headings-and-labels.html)
* [Cumplir los criterios de éxito 2.4.6](https://www.w3.org/WAI/WCAG21/quickref/#headings-and-labels)

### Enfoque visible (2.4.7) {#focus-visible}

* Criterios de éxito 2.4.7
* Nivel AA
* Enfoque visible: Cualquier interfaz de usuario operable con el teclado tiene un modo de funcionamiento en el que el indicador de selección del teclado está visible.

#### Objetivo: Enfoque visible (2.4.7) {#purpose-focus-visible}

El propósito de este criterio de éxito es ayudar a una persona a saber qué elemento tiene el enfoque del teclado.

Debe ser posible que una persona sepa qué elemento de varios elementos tiene el enfoque del teclado. Si solo hay un control accionable por teclado en la pantalla, el criterio de éxito se cumpliría porque el diseño visual presenta sólo un elemento procesable por teclado.

Cuando el criterio de éxito indica &quot;modo de funcionamiento&quot;, se tiene en cuenta para las plataformas que no siempre muestran un indicador de enfoque. En la mayoría de los casos solo hay un modo de funcionamiento, por lo que se aplican estos criterios de éxito.

#### Enfoque visible (2.4.7) {#how-to-meet-focus-visible}

Siga las directrices de [Cumplir los criterios de éxito 2.4.7](https://www.w3.org/WAI/WCAG21/quickref/#focus-visible).

#### Más información: Enfoque visible (2.4.7) {#more-information-focus-visible}

* [Entender los criterios de éxito 2.4.7](https://www.w3.org/WAI/WCAG21/Understanding/focus-visible.html)
* [Cumplir los criterios de éxito 2.4.7](https://www.w3.org/WAI/WCAG21/quickref/#focus-visible)

## Principio 3: comprensible     {#principle-understandable}

[Principio 3: Comprensible: la información y el funcionamiento de la interfaz del usuario deben ser comprensibles.](https://www.w3.org/TR/WCAG/#understandable)

### Hacer que el contenido del texto sea legible y comprensible (3.1)     {#make-text-content-readable-and-understandable}

[Directrices 3.1 Legible: hacer que el contenido del texto sea legible y comprensible.](https://www.w3.org/TR/WCAG/#readable)

### Idioma de la página (3.1.1)     {#language-of-page}

* Criterios de éxito 3.1.1
* Nivel A
* Idioma de la página: el lenguaje humano por defecto de cada página web se puede determinar programáticamente

#### Objetivo: Idioma de la página (3.1.1)     {#purpose-language-of-page}

El objetivo de este criterio de éxito es asegurarse de que el texto y cualquier otro contenido lingüístico se introduce de manera correcta. Para los usuarios de lectores de pantalla, esto garantiza que el contenido se pronuncia de manera correcta, mientras que los navegadores visuales tienden a mostrar ciertos conjuntos de caracteres de manera correcta.

#### Cómo cumplir: Idioma de la página (3.1.1)  {#how-to-meet-language-of-page}

Para cumplir este criterio de éxito, el idioma por defecto de una página web se puede identificar utilizando el atributo `lang` en el elemento `<html>` en la parte superior de la página. Por ejemplo:

* Si una página está escrita en inglés británico, el elemento `<html>` debería ser:
   `<html lang = “en-gb”>`

* Mientras que una página en inglés americano debería adoptar el estándar siguiente:
   `<html lang = “en-us”>`

En AEM, el idioma predeterminado de la página se define al crear la página, pero también se puede cambiar al editarla. Puede hacerlo desde la **barra de tareas** - pestaña **Página** - **Propiedades de página…** - pestaña **Avanzadas**.

#### Más información: Idioma de la página (3.1.1) {#more-information-language-of-page}

* [Entender los criterios de éxito 3.1.1](https://www.w3.org/WAI/WCAG21/Understanding/language-of-page.html)
* [Cumplir los criterios de éxito 3.1.1](https://www.w3.org/WAI/WCAG21/quickref/#language-of-page)
* Los códigos se basan en ISO 639-1. Encontrará una lista más extensa de códigos para cada idioma en [W3 Schools](https://www.w3schools.com/tags/ref_language_codes.asp).

### Idioma de las partes (3.1.2)          {#language-of-parts}

* Criterios de éxito 3.1.2
* Nivel AA
* Idioma de las partes: se puede determinar programáticamente el idioma de cada pasaje o frase en el contenido excepto en casos de nombres propios, términos técnicos, palabras de lenguaje indeterminado y palabras o expresiones que hayan formado parte de la lengua vernácula del texto que lo rodea

#### Objetivo: Idioma de las partes (3.1.2)     {#purpose-language-of-parts}

El objetivo de este criterio de éxito es parecido al del criterio de éxito del [Idioma de la página](#language-of-page), excepto por el hecho de que se refiere a páginas web con contenido en idiomas múltiples en una misma página (por ejemplo, por las citas o préstamos poco frecuentes).

Las páginas que aplican este criterio de éxito permiten:

* Software de transición en braille para insertar caracteres acentuados.
* Lectores de pantalla para pronunciar las palabras que no aparecen en el idioma por defecto de manera correcta.
* Herramientas de traducción como Google Translate para traducir el contenido de manera correcta de un idioma a otro.

#### Cómo cumplir: Idioma de las partes (3.1.2)  {#how-to-meet-language-of-parts}

El atributo `lang` se puede utilizar para identificar los cambios en el idioma del contenido. Por ejemplo, una cita en alemán (ISO 639-1 código “de”) se puede mostrar de la manera siguiente:

```xml
<blockquote cite = "John F. Kennedy" lang = "de">
     <p>Ich bin ein Berliner</p>
 </blockquote>
```

>[!NOTE]
>
>Los bloques de citas no funcionan en una situación fácil de usar. Se podría desarrollar un componente personalizado para admitir el atributo.

De manera similar, el navegador puede mostrar un préstamo poco común o una expresión correcta si el elemento `span` se utiliza de la manera siguiente:

```xml
<p>The only French phrase I know is <span lang = “fr”>je ne sais quoi</code>.</p>
```

>[!NOTE]
>
>No es necesario seguir este criterio de éxito cuando se incluyen nombres o ciudades en distintos idiomas, o cuando se utilizan préstamos o expresiones que ya son comunes en el idioma por defecto (como *schadenfreude* en inglés).

Para añadir el elemento “span” (extensión), con un idioma adecuado, puede editar manualmente sus especificaciones HTML en el modo de edición de la fuente de RTE para que se lea como puede ver arriba. Alternativamente, el atributo `lang` se puede incluir en RTE a través de un administrador del sistema (consulte Añadir ayuda para elementos y atributos HTML adicionales).
<!--
To add the span element, with an appropriate language, you can manually edit your HTML markup in the source edit mode of the RTE so that it reads as above. Alternatively the `lang` attribute can be included in the RTE by a system administrator (see [Adding Support for Additional HTML Elements and Attributes](/help/sites-administering/rte-accessible-content.md#adding-support-for-additional-html-elements-and-attributes)).
-->

#### Más información: Idioma de las partes (3.1.2) {#more-information-language-of-parts}

* [Entender los criterios de éxito 3.1.2](https://www.w3.org/WAI/WCAG21/Understanding/language-of-parts.html)
* [Cumplir los criterios de éxito 3.1.2](https://www.w3.org/WAI/WCAG21/quickref/#language-of-parts)

### Predecible (3.2) {#predictable}

[Directriz 3.2 Predecible: Hacer que las páginas Web aparezcan y funcionen de manera predecible.](https://www.w3.org/TR/WCAG/#predictable)

Esto se centra en garantizar que las páginas web tengan un aspecto y un funcionamiento coherentes.

### Enfoque (3.2.1) {#on-focus}

* Criterios de éxito 3.2.1
* Nivel A
* Enfoque: Cuando se selecciona cualquier componente de interfaz de usuario, no se inicia un cambio de contexto.

#### Objetivo: Enfoque (3.2.1) {#purpose-on-focus}

El propósito de este criterio de éxito es garantizar que la funcionalidad sea predecible a medida que los visitantes navegan por un documento. Cualquier componente que pueda desencadenar un evento cuando se selecciona no debe cambiar el contexto. Algunos ejemplos de cambio de contexto cuando un componente recibe el enfoque son, entre otros:

* formularios enviados automáticamente cuando un componente recibe el enfoque;
* nuevas ventanas iniciadas cuando un componente recibe el enfoque;
* el enfoque se cambia a otro componente cuando ese componente recibe el enfoque;

El enfoque se puede mover a un control mediante el teclado (por ejemplo, mediante la tabulación a un control) o el ratón (por ejemplo, haciendo clic en un campo de texto). Mover el ratón sobre un control no mueve el enfoque a menos que las secuencias de comandos implementen este comportamiento. Tenga en cuenta que para algunos tipos de controles, hacer clic en un control también puede activar el control (por ejemplo, botón), lo que a su vez puede iniciar un cambio en el contexto.

#### Enfoque (3.2.1) {#how-to-meet-on-focus}

Siga las directrices de [Cumplir los criterios de éxito 3.2.1](https://www.w3.org/WAI/WCAG21/quickref/#on-focus).

#### Más información: On Focus (3.2.1) {#more-information-on-focus}

* [Entender los criterios de éxito 3.2.1](https://www.w3.org/WAI/WCAG21/Understanding/on-focus.html)
* [Cumplir los criterios de éxito 3.2.1](https://www.w3.org/WAI/WCAG21/quickref/#on-focus)

### On Input (3.2.2) {#on-input}

* Criterios de éxito 3.2.2
* Nivel A
* En la entrada: Cambiar la configuración de cualquier componente de interfaz de usuario no provoca automáticamente un cambio de contexto a menos que se haya informado al usuario del comportamiento antes de utilizar el componente.

#### Objetivo: Entrada (3.2.2) {#purpose-on-input}

El propósito de este criterio de éxito es garantizar que la introducción de datos o la selección de un control de formulario tengan efectos predecibles. Cambiar la configuración de cualquier componente de interfaz de usuario está cambiando algún aspecto del control que persistirá cuando el usuario ya no interactúe con él. De este modo, si se activa una casilla de verificación, se introduce texto en un campo de texto o se cambia la opción seleccionada en un control de lista, se cambia su configuración, pero si se activa un vínculo o un botón no. Los cambios en el contexto pueden confundir a los usuarios que no perciben fácilmente el cambio o que se distraen fácilmente con los cambios. Los cambios de contexto solo son adecuados cuando está claro que tal cambio se producirá en respuesta a la acción del usuario.

#### Entrada de respuesta (3.2.2) {#how-to-meet-on-input}

Siga las directrices de [Cumplir los criterios de éxito 3.2.2](https://www.w3.org/WAI/WCAG21/quickref/#on-input).

#### Más información: On Input (3.2.2) {#more-information-on-input}

* [Entender los criterios de éxito 3.2.2](https://www.w3.org/WAI/WCAG21/Understanding/on-input.html)
* [Cumplir los criterios de éxito 3.2.2](https://www.w3.org/WAI/WCAG21/quickref/#on-input)

### Navegación coherente (3.2.3) {#consistent-navigation}

* Criterios de éxito 3.2.3
* Nivel AA
* Navegación coherente: Los mecanismos de navegación que se repiten en varias páginas Web dentro de un conjunto de páginas Web se producen en el mismo orden relativo cada vez que se repiten, a menos que el usuario inicie un cambio.

#### Objetivo: navegación coherente (3.2.3) {#purpose-consistent-navigation}

El propósito de este criterio de éxito es fomentar el uso de una presentación y un diseño coherentes para los usuarios que interactúan con contenido repetido dentro de un conjunto de páginas Web y necesitan localizar información o funcionalidad específicas más de una vez. Las personas con visión reducida que utilizan la ampliación de la pantalla para mostrar una pequeña parte de la pantalla a la vez suelen utilizar indicaciones visuales y límites de página para localizar rápidamente contenido repetido. La presentación de contenido repetido en el mismo orden también es importante para los usuarios visuales que utilizan memoria espacial o señales visuales dentro del diseño para localizar contenido repetido.

Es importante tener en cuenta que el uso de la frase &quot;el mismo orden&quot; en esta sección no implica que no se puedan utilizar los menús de subnavegación o que no se puedan utilizar bloques de navegación secundaria o de estructura de página. En su lugar, este criterio de éxito está diseñado para ayudar a los usuarios que interactúan con el contenido repetido en las páginas Web a poder predecir la ubicación del contenido que buscan y encontrarlo más rápidamente cuando lo encuentran de nuevo.

Los usuarios pueden iniciar un cambio en el orden utilizando agentes de usuario adaptables o estableciendo preferencias para que la información se presente de una manera que les resulte más útil.

#### Navegación coherente (3.2.3) {#how-to-meet-consistent-navigation}

Siga las directrices de [Cumplir los criterios de éxito 3.2.3](https://www.w3.org/WAI/WCAG21/quickref/#consistent-navigation).

#### Más información: navegación coherente (3.2.3) {#more-information-consistent-navigation}

* [Entender los criterios de éxito 3.2.3](https://www.w3.org/WAI/WCAG21/Understanding/consistent-navigation.html)
* [Cumplir los criterios de éxito 3.2.3](https://www.w3.org/WAI/WCAG21/quickref/#consistent-navigation)

### Identificación coherente (3.2.4) {#consistent-identification}

* Criterios de éxito 3.2.4
* Nivel A
* Identificación consistente: Los componentes que tienen la misma funcionalidad dentro de un conjunto de páginas Web se identifican de manera consistente.

#### Objetivo: Identificación coherente (3.2.4) {#purpose-consistent-identification}

El propósito de este criterio de éxito es garantizar la identificación coherente de los componentes funcionales que aparecen repetidamente dentro de un conjunto de páginas Web. Una estrategia que las personas que utilizan lectores de pantalla cuando administran un sitio Web consiste en confiar en gran medida en su familiaridad con las funciones que pueden aparecer en diferentes páginas Web. Si funciones idénticas tienen etiquetas diferentes (o, más generalmente, un nombre accesible diferente) en páginas Web diferentes, el sitio será considerablemente más difícil de usar. También puede ser confuso y aumentar la carga cognitiva para las personas con limitaciones cognitivas. Por lo tanto, un etiquetado coherente ayudará.

Esta coherencia se extiende a las alternativas textuales. Si los iconos u otros elementos no textuales tienen la misma funcionalidad, las alternativas textuales también deberían ser coherentes.

Si hay dos componentes en una página web que tienen la misma funcionalidad que un componente en otra página en un conjunto de páginas web, entonces los 3 deben ser coherentes. Por lo tanto, los dos en la misma página serán coherentes.

Aunque es deseable y la práctica recomendada siempre ser coherente dentro de una sola página web, 3.2.4 sólo aborda la coherencia dentro de un conjunto de páginas web en las que algo se repite en más de una página del conjunto.

#### Identificación coherente (3.2.4) {#how-to-meet-consistent-identification}

Siga las directrices de [Cumplir los criterios de éxito 3.2.4](https://www.w3.org/WAI/WCAG21/quickref/#consistent-identification).

#### Más información: Identificación consistente (3.2.4) {#more-information-consistent-identification}

* [Entender los criterios de éxito 3.2.4](https://www.w3.org/WAI/WCAG21/Understanding/consistent-identification.html)
* [Cumplir los criterios de éxito 3.2.4](https://www.w3.org/WAI/WCAG21/quickref/#consistent-identification)

### Asistencia de entrada (3.3) {#input-assistance}

[Directrices 3.3 Asistencia de la entrada: ayudar a los usuarios a evitar y corregir errores.](https://www.w3.org/TR/WCAG/#input-assistance)

### Identificación de error (3.3.1) {#error-identification}

* Criterios de éxito 3.3.1
* Nivel A
* Identificación del error: Si se detecta automáticamente un error de entrada, se identifica el elemento que está en error y el error se describe al usuario en el texto.

#### Objetivo: Identificación de error (3.3.1) {#purpose-error-identification}

El propósito de este criterio de éxito es garantizar que los usuarios sean conscientes de que se ha producido un error y puedan determinar lo que está mal. El mensaje de error debe ser lo más específico posible. En caso de que el envío de un formulario no se haya realizado correctamente, la visualización del formulario y la indicación de los campos en los que se ha producido un error no bastan para que algunos usuarios perciban que se ha producido un error. Los usuarios del lector de pantalla, por ejemplo, no sabrán que hubo un error hasta que encuentren uno de los indicadores. Es posible que abandonen la forma por completo antes de encontrar el indicador de error, pensando que la página simplemente no funciona. Según la definición de WCAG 2.0, un &quot;error de entrada&quot; es la información proporcionada por el usuario que no se acepta. Esto incluye:

información requerida por la página web pero omitida por el usuario, o información proporcionada por el usuario pero que se encuentra fuera del formato de datos requerido o de los valores permitidos.
Por ejemplo:

* el usuario no puede introducir la abreviatura adecuada en estado, provincia, región, etc. field;
* el usuario introduce una abreviatura de estado que no es un estado válido;
* el usuario introduce un código postal o código postal inexistente;
* el usuario introduce una fecha de nacimiento 2 años en el futuro;
* el usuario introduce caracteres alfabéticos o paréntesis en su campo de número de teléfono que solo acepta números;
* el usuario introduce una oferta que está por debajo de la oferta anterior o del incremento mínimo de la oferta.

#### Identificación de errores (3.3.1) {#how-to-meet-error-identification}

Siga las directrices de [Cumplir los criterios de éxito 3.3.1](https://www.w3.org/WAI/WCAG21/quickref/#error-identification).

#### Más información: Identificación de error (3.3.1) {#more-information-error-identification}

* [Entender los criterios de éxito 3.3.1](https://www.w3.org/WAI/WCAG21/Understanding/error-identification.html)
* [Cumplir los criterios de éxito 3.3.1](https://www.w3.org/WAI/WCAG21/quickref/#error-identification)

### Etiquetas o instrucciones (3.3.2)     {#labels-or-instructions}

* Criterios de éxito 3.3.2
* Nivel A
* Etiquetas o instrucciones: las etiquetas o instrucciones se proporcionan cuando el contenido requiere entradas de usuarios

#### Objetivo: Etiquetas o instrucciones (3.3.2)     {#purpose-labels-or-instructions}

Proporcionar instrucciones para ayudar a los usuarios a completar formularios es una parte fundamental para la buena práctica en la funcionalidad de la interfaz. Hacer esto es particularmente beneficioso para quienes sufren discapacidades visuales o cognitivas, ya que de otra manera experimentarían dificultades para entender la estructura de un formulario y el tipo de datos que se proporcionan en un campo del formulario en concreto.

En AEM, se añade una etiqueta por defecto al añadir un componente de formulario, como **Cuadro de texto**, a la página. Este título por defecto depende del tipo de componente, puede añadir su propio título en la pestaña **Título y texto** del diálogo de edición para ese campo. Es importante asegurarse de que las etiquetas ayudan a los usuarios a entender los datos que se asocian con cada componente del formulario.

El campo **Título** se debe utilizar para elementos de campo porque proporciona una etiqueta disponible para la tecnología de asistencia. No basta con escribir una etiqueta en el texto, al lado del campo.

Para algunos componentes de formulario también se pueden ocultar las etiquetas utilizando la casilla **Ocultar título**. Las etiquetas ocultas de esta forma siguen estando disponibles para la tecnología de asistencia, pero no se muestran en la pantalla. Aunque puede ser una medida adecuada en algunas situaciones, normalmente es mejor incluir una etiqueta que sea visual siempre que se pueda, ya que posiblemente algunos usuarios se fijen en una sección muy pequeña de la pantalla (que miren los campos uno por uno) y necesiten las etiquetas para identificar el campo de manera correcta.

#### Botones de imagen {#image-buttons}

Cuando se utilizan botones de imagen (por ejemplo, el componente **Botón de imagen**) el campo **Título** en la pestaña **Título y texto** del cuadro de diálogo de edición, proporciona el texto alternativo para la imagen, en lugar de la etiqueta. Por eso, en el ejemplo siguiente, la imagen con el texto `Submit` contiene el texto alternativo `Submit`, que se ha añadido utilizando el campo **Título** en el diálogo de edición.

#### Grupos de campos de formulario {#groups-of-form-fields}

Cuando hay un grupo de controles relacionados, como el **Grupo de radio**, puede ser necesario un título para el grupo, así como controles individuales. Al agregar un conjunto de botones de radio en AEM, el campo **Título** proporciona este título de grupo, mientras que los títulos individuales se especifican a medida que se crean los botones de radio (**Elementos**).

Sin embargo, no existe una asociación programática entre el título del grupo y los botones de opción. Los editores de plantillas necesitarían rodear el título en los `fieldset` necesarios y las etiquetas `legend` para crear esta asociación, que solo se puede hacer editando el código fuente de la página. Alternativamente, un administrador del sistema puede añadir soporte a estos elementos para que aparezcan en el diálogo **Propiedades del campo** (consulte Añadir ayuda para elementos y atributos HTML adicionales).

<!--
However, there is no programmatic association between the group title and the radio buttons themselves. Template editors would need to wrap the title in the necessary `fieldset` and `legend` tags to create this association and this can only be done by editing the page source code. Alternatively, a system administrator can add support for these elements so that they appear in the **Field Properties** dialog (see [Adding Support for Additional HTML Elements and Attributes](/help/sites-administering/rte-accessible-content.md#adding-support-for-additional-html-elements-and-attributes)).
-->

#### Consideraciones adicionales para Formularios {#additional-considerations-for-forms}

Si se introducen datos en un formato concreto, especifíquelo en el texto de la etiqueta. Por ejemplo, si se tiene que introducir una fecha en formato `DD-MM-YYYY`, especifíquelo como parte de la etiqueta. Esto significa que cuando los usuarios de los lectores de pantalla se encuentren con este campo, la etiqueta se anunciará automáticamente junto con la información adicional sobre el formato.

Si es obligatorio introducir datos en un campo de formulario, especifíquelo utilizando la palabra obligatorio como parte de la etiqueta. AEM añade un asterisco cuando un campo es obligatorio, pero sería ideal incluir la palabra `required` en la etiqueta (en el campo **Título** del diálogo de edición).

La colocación de las etiquetas también es importante ya que ayuda a localizar campos adecuados. Esto es de particular importancia cuando el usuario se encuentra con un formulario complejo. Siga la convención siguiente:

* Casillas o botones de opciones: 
Las etiquetas se colocan inmediatamente a la derecha del campo.
* Otros componentes del formulario (por ejemplo los cuadros de texto o los cuadros combinados): 
Las etiquetas se colocan inmediatamente encima o bien a la izquierda del campo.

En formularios simples con una funcionalidad muy limitada, etiquetar de manera correcta un botón de `Submit` puede actuar como una etiqueta para el campo adyacente (por ejemplo: `Search`). Resulta útil cuando puede ser difícil encontrar espacio para el texto de una etiqueta.

#### Más información: Etiquetas o instrucciones (3.3.2)     {#more-information-labels-or-instructions}

* [Entender los criterios de éxito 3.3.2](https://www.w3.org/WAI/WCAG21/Understanding/labels-or-instructions.html)
* [Cumplir los criterios de éxito 3.3.2](https://www.w3.org/WAI/WCAG21/quickref/#labels-or-instructions)

### Sugerencia de error (3.3.3) {#error-suggestion}

* Criterios de éxito 3.3.3
* Nivel AA
* Teclado: Si se detecta automáticamente un error de entrada y se conocen sugerencias para la corrección, las sugerencias se proporcionan al usuario, a menos que ello ponga en peligro la seguridad o el propósito del contenido.

#### Objetivo: Sugerencia de error (3.3.3) {#purpose-error-suggestion}

El propósito de este criterio de éxito es garantizar que los usuarios reciban las sugerencias adecuadas para la corrección de un error de entrada si es posible. La definición de WCAG 2.0 de &quot;error de entrada&quot; dice que es &quot;información proporcionada por el usuario que no es aceptada&quot; por el sistema. Algunos ejemplos de información que no se acepta incluyen la información necesaria pero omitida por el usuario y la información proporcionada por el usuario, pero que no corresponde al formato de datos requerido o a los valores permitidos.

Los criterios de éxito 3.3.1 permiten la notificación de errores. Sin embargo, a las personas con limitaciones cognitivas les puede resultar difícil entender cómo corregir los errores. Es posible que las personas con discapacidades visuales no puedan averiguar exactamente cómo corregir el error. En el caso de un envío de formulario fallido, los usuarios pueden abandonar el formulario porque pueden no estar seguros de cómo corregir el error aunque sepan que se ha producido.

El autor del contenido puede proporcionar la descripción del error o el agente de usuario puede proporcionar la descripción del error en función de la información específica de la tecnología y determinada mediante programación.

#### Sugerencia de error (3.3.3) {#how-to-meet-error-suggestion}

Siga las directrices de [Cumplir los criterios de éxito 3.3.3](https://www.w3.org/WAI/WCAG21/quickref/#error-suggestion).

#### Más información: Sugerencia de error (3.3.3) {#more-information-error-suggestion}

* [Entender los criterios de éxito 3.3.3](https://www.w3.org/WAI/WCAG21/Understanding/error-suggestion.html)
* [Cumplir los criterios de éxito 3.3.3](https://www.w3.org/WAI/WCAG21/quickref/#error-suggestion)

### Prevención de errores (legal, financiera, de datos) (3.3.4) {#error-prevention-legal-financial-data}

* Criterios de éxito 3.3.4
* Nivel AA
* Prevención de errores (legal, financiera, datos): Para las páginas Web que provocan compromisos legales o transacciones financieras para el usuario, que modifican o eliminan datos controlables por el usuario en sistemas de almacenamiento de datos o que envían respuestas de prueba del usuario, al menos una de las siguientes opciones es verdadera:

   * ReversibleSubmission son reversibles.
   * CheckedData introducida por el usuario se comprueba si hay errores de entrada y se le ofrece al usuario la oportunidad de corregirlos.
   * ConfirmadoExiste un mecanismo disponible para revisar, confirmar y corregir la información antes de finalizar la presentación.

#### Objetivo: Prevención de errores (legal, financiera, de datos) (3.3.4) {#purpose-error-prevention-legal-financial-data}

El propósito de este criterio de éxito es ayudar a los usuarios con discapacidades a evitar consecuencias graves como resultado de un error al realizar una acción que no se puede revertir. Por ejemplo, la compra de pasajes aéreos no reembolsables o la presentación de una orden de compra de acciones en una cuenta de corretaje son transacciones financieras con graves consecuencias. Si un usuario ha cometido un error en la fecha del viaje aéreo, podría terminar con un billete para el día equivocado que no se puede intercambiar. Si el usuario cometiera un error en el número de acciones que se comprarían, podría terminar comprando más acciones de las que se pretendía. Estos dos tipos de errores implican transacciones que tienen lugar inmediatamente y que no pueden modificarse posteriormente, y pueden resultar muy costosas. Del mismo modo, puede ser un error irrecuperable que los usuarios modifiquen o eliminen involuntariamente los datos almacenados en una base de datos a la que posteriormente deban acceder, como por ejemplo todo su perfil de viajes en un sitio Web de servicios de viajes. Al referirse a la modificación o eliminación de datos &#39;controlables por el usuario&#39;, la intención es evitar la pérdida masiva de datos, como eliminar un archivo o registro. No es la intención requerir una confirmación para cada comando de guardado ni la simple creación o edición de documentos, registros u otros datos.

Los usuarios con discapacidades pueden tener más probabilidades de cometer errores. Las personas con discapacidades de lectura pueden transponer números y letras, y las personas con discapacidades motoras pueden golpear las llaves por error. Proporcionar la capacidad de revertir acciones permite a los usuarios corregir un error que podría tener consecuencias graves. La capacidad de revisar y corregir la información ofrece al usuario la oportunidad de detectar un error antes de realizar una acción que tenga graves consecuencias.

Los datos controlables por el usuario son datos visualizables por el usuario que el usuario puede cambiar o eliminar mediante una acción intencionada. Algunos ejemplos de usuarios que controlan estos datos son la actualización del número de teléfono y la dirección de la cuenta del usuario o la eliminación de un registro de facturas anteriores de un sitio web. No hace referencia a datos como los registros de Internet y los datos de supervisión de motores de búsqueda con los que el usuario no puede interactuar ni realizar vistas directamente.

#### Prevención de errores (legal, financiera, de datos) (3.3.4) {#how-to-meet-error-prevention-legal-financial-data}

Siga las directrices de [Cumplir los criterios de éxito 3.3.4](https://www.w3.org/WAI/WCAG21/quickref/#error-prevention-legal-financial-data).

#### Más información: Prevención de errores (legal, financiera, de datos) (3.3.4) {#more-information-error-prevention-legal-financial-data}

* [Entender los criterios de éxito 3.3.4](https://www.w3.org/WAI/WCAG21/Understanding/error-prevention-legal-financial-data.html)
* [Cumplir los criterios de éxito 3.3.4](https://www.w3.org/WAI/WCAG21/quickref/#error-prevention-legal-financial-data)

## Principio 4: Sólido {#principle-robust}

[Principio 4: Sólido: el contenido debe ser lo suficientemente robusto como para que pueda ser interpretado por una amplia variedad de agentes de usuario, incluidas las tecnologías de asistencia.](https://www.w3.org/TR/WCAG/#robust)

### Compatible (4.1) {#compatible}

[Directrices 4.1 Compatible: Maximice la compatibilidad con los agentes de usuario actuales y futuros, incluidas las tecnologías de asistencia.](https://www.w3.org/TR/WCAG/#compatible)

Maximice la compatibilidad con los agentes de usuario actuales y futuros, incluidas las tecnologías de asistencia.

### Análisis (4.1.1) {#parsing}

* Criterios de éxito 4.1.1
* Nivel A
* Analizando: En el contenido implementado mediante lenguajes de marcado, los elementos tienen etiquetas inicio y final completas, los elementos se anidan según sus especificaciones, los elementos no contienen atributos de duplicado y cualquier ID es único, excepto cuando las especificaciones permiten estas características.

#### Objetivo: Análisis (4.1.1) {#purpose-parsing}

El propósito de este criterio de éxito es garantizar que los agentes de usuario, incluidas las tecnologías de asistencia, puedan interpretar y analizar el contenido con precisión. Si el contenido no se puede analizar en una estructura de datos, es posible que distintos agentes de usuario lo presenten de forma diferente o que no puedan analizarlo por completo. Algunos agentes de usuario utilizan &quot;técnicas de reparación&quot; para representar contenido mal codificado.

Dado que las técnicas de reparación varían entre los agentes de usuario, los autores no pueden suponer que el contenido se analizará con precisión en una estructura de datos o que los agentes de usuario especializados, incluidas las tecnologías de asistencia, lo procesarán correctamente, a menos que el contenido se cree según las reglas definidas en la gramática formal de esa tecnología. En los lenguajes de marcado, los errores en la sintaxis de elementos y atributos y el no proporcionar las etiquetas inicio/final anidadas correctamente producen errores que impiden que los agentes de usuario analicen el contenido de forma fiable. Por lo tanto, el Criterio de éxito requiere que el contenido se pueda analizar usando solamente las reglas de la gramática formal.

#### Análisis (4.1.1) {#how-to-meet-parsing}

Siga las directrices de [Cumplir los criterios de éxito 4.1.1](https://www.w3.org/WAI/WCAG21/quickref/#parsing).

#### Más información: análisis (4.1.1) {#more-information-parsing}

* [Entender los criterios de éxito 4.1.1](https://www.w3.org/WAI/WCAG21/Understanding/parsing.html)
* [Cumplir los criterios de éxito 4.1.1](https://www.w3.org/WAI/WCAG21/quickref/#parsing)

### Nombre, Función, Valor (4.1.2) {#name-role-value}

* Criterios de éxito 4.1.2
* Nivel A
* Nombre, Función, Valor: Para todos los componentes de la interfaz de usuario (incluidos, entre otros: elementos de formulario, vínculos y componentes generados por secuencias de comandos), el nombre y la función pueden determinarse mediante programación; los estados, las propiedades y los valores que el usuario puede establecer se pueden definir mediante programación; y la notificación de los cambios en estos artículos está disponible para los agentes de usuario, incluidas las tecnologías de asistencia.

#### Objetivo: Nombre, Función, Valor (4.1.2) {#purpose-ame-role-value}

El objetivo de este criterio de éxito es garantizar que las tecnologías de asistencia (AT) puedan recopilar información sobre, activar o establecer y mantener al día el estado de los controles de interfaz de usuario en el contenido.

Cuando se utilizan controles estándar de tecnologías accesibles, este proceso es sencillo. Si los elementos de la interfaz de usuario se utilizan de acuerdo con las especificaciones, se cumplirán las condiciones de esta disposición. (Ver ejemplos de Criterios de éxito 4.1.2 más adelante)

Sin embargo, si se crean controles personalizados o si se programan elementos de interfaz (en código o secuencia de comandos) para que tengan una función o función distinta de la habitual, es necesario adoptar medidas adicionales para garantizar que los controles proporcionen información importante a las tecnologías de asistencia y permitan que se controlen mediante tecnologías de asistencia.

Un estado particularmente importante de un control de interfaz de usuario es si está o no enfocado. El estado de enfoque de un control se puede determinar mediante programación y las notificaciones sobre el cambio de enfoque se envían a los agentes de usuario y a la tecnología de asistencia. Otros ejemplos del estado de control de la interfaz de usuario son si se ha seleccionado o no una casilla de verificación o un botón de radio, o si un árbol o nodo de lista contraíble está expandido o contraído.

#### Nombre, función, valor (4.1.2) {#how-to-meet-ame-role-value}

Siga las directrices de [Cumplir los criterios de éxito 4.1.2](https://www.w3.org/WAI/WCAG21/quickref/#name-role-value).

#### Más información: Nombre, Función, Valor (4.1.2) {#more-information-ame-role-value}

* [Entender los criterios de éxito 4.1.2](https://www.w3.org/WAI/WCAG21/Understanding/name-role-value.html)
* [Cumplir los criterios de éxito 4.1.2](https://www.w3.org/WAI/WCAG21/quickref/#name-role-value)
