---
title: Adición de recursos de Dynamic Media a las páginas
description: Aprenda a añadir componentes de Dynamic Media a una página en Adobe Experience Manager as a Cloud Service.
contentOwner: Rick Brough
feature: Asset Management
topic: Business Practitioner
role: Business Practitioner
translation-type: tm+mt
source-git-commit: 497952b1b6679eca301839d1435924e16a2e2438
workflow-type: tm+mt
source-wordcount: '3089'
ht-degree: 21%

---


# Adición de recursos de Dynamic Media a las páginas{#adding-dynamic-media-assets-to-pages}

Para añadir la funcionalidad Dynamic Media a los recursos que utilice en sus sitios web, puede agregar directamente en la página el componente **Dynamic Media**, **Interactive Media**, **Panoramic Media** o **Video 360 Media**. Introduzca el modo Diseño y active los componentes de Dynamic Media. A continuación, agregue estos componentes a la página y agregue recursos al componente. Los componentes de Dynamic Media son inteligentes: saben si va a añadir una imagen o un vídeo y las opciones de configuración disponibles cambian en consecuencia.

Los recursos de Dynamic Media se añaden directamente a la página si utiliza Experience Manager como WCM. Si utiliza un tercero para su WCM, [link](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md) o [incruste](/help/assets/dynamic-media/embed-code.md) sus recursos. Para ver un sitio web interactivo de terceros, consulte [Distribución de imágenes optimizadas en un sitio interactivo](/help/assets/dynamic-media/responsive-site.md).

>[!NOTE]
>
>Asegúrese de publicar los recursos antes de agregarlos a las páginas en el Experience Manager. Consulte [Publicación de recursos de Dynamic Media](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md).

## Adición de un componente Dynamic Media a una página {#adding-a-dynamic-media-component-to-a-page}

Añadir un componente de medios 3D, Dynamic Media, Medios interactivos, Medios panorámicos, Recorte inteligente de vídeo o Vídeo 360 a una página es lo mismo que añadir un componente a cualquier página.

**Adición de un componente de Dynamic Media a una página**

1. En el Experience Manager, abra la página a la que desee añadir el componente Dynamic Media.
1. En el panel izquierdo, pulse el icono **[!UICONTROL Componentes]** y, a continuación, filtre para Dynamic Media.

   Si no hay ninguna lista de componentes de Dynamic Media disponible, es probable que deba habilitar los componentes de Dynamic Media que desee utilizar. Consulte [Habilitación de componentes de Dynamic Media](#enabling-dynamic-media-components).

   ![6_5_360video_wcmcomponent](assets/6_5_360video_wcmcomponent.png)

1. Arrastre un componente **[!UICONTROL Dynamic Media]** y suéltelo en la ubicación deseada de la página.

1. Pase el puntero directamente sobre el componente. Cuando el componente esté rodeado por un cuadro azul, pulse una vez para mostrar la barra de herramientas del componente. Pulse el icono **[!UICONTROL Configuration (wFrench)]**.

   ![6_5_360video_wcmcomponentconfigure](assets/6_5_360video_wcmcomponentconfigure.png)

1. Según el componente Dynamic Media que haya colocado en la página, se abre un cuadro de diálogo de configuración. [Defina las ](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md#dynamic-media-components) opciones del componente según sea necesario.

   El ejemplo siguiente muestra el cuadro de diálogo del componente **[!UICONTROL Vídeo 360 Media]** de Dynamic Media y las opciones disponibles en la lista desplegable Ajuste preestablecido de visor .

   ![Componente de medios de vídeo 360](assets/6_5_360video_wcmcomponentviewerpreset.png)

   Componente de medios de Dynamic Media Video 360.

1. Cuando haya terminado, en la esquina superior derecha del cuadro de diálogo, pulse la marca de verificación para guardar los cambios.

### Habilitación de componentes de Dynamic Media {#enabling-dynamic-media-components}

Si no hay componentes de Dynamic Media disponibles para agregarlos a una página, es probable que deba habilitar los componentes que desee utilizar.

1. En el Experience Manager, abra la página a la que desee añadir el componente Dynamic Media.
1. A la izquierda de la barra de herramientas, cerca de la parte superior de la página, pulse el icono Información de página y, a continuación, pulse **[!UICONTROL Editar plantilla]** en la lista desplegable.

   ![edit-template](/help/assets/assets-dm/edit-template.png)

1. En el lado derecho de la barra de herramientas, cerca de la parte superior de la página, en la lista desplegable, pulse **[!UICONTROL Estructura]**.

   ![Política](/help/assets/assets-dm/structure-mode.png)

1. Cerca de la parte inferior de la página, pulse **[!UICONTROL Contenedor de diseño]** para abrir su barra de herramientas y, a continuación, pulse el icono Política .
1. En la página **[!UICONTROL Contenedor de diseño]**, en el encabezado **[!UICONTROL Propiedades]**, asegúrese de que la pestaña **[!UICONTROL Componentes permitidos]** está seleccionada.

   ![Componentes permitidos](/help/assets/assets-dm/allowed-components.png)

1. Desplácese hasta que vea **[!UICONTROL Dynamic Media]**.
1. Pulse el icono > a la izquierda de **[!UICONTROL Dynamic Media]** y, a continuación, seleccione los componentes de Dynamic Media que desea habilitar.

   ![Lista de componentes de Dynamic Media](/help/assets/assets-dm/dm-components-select.png)

1. Cerca de la esquina superior derecha de la página **[!UICONTROL Contenedor de diseño]**, pulse el icono Listo (marca de verificación).

1. En el lado derecho de la barra de herramientas, cerca de la parte superior de la página, en la lista desplegable, pulse **[!UICONTROL Contenido inicial]**.
1. [Añada un componente Dynamic Media a una ](#adding-a-dynamic-media-component-to-a-page) página como de costumbre.

## Localización de componentes de Dynamic Media {#localizing-dynamic-media-components}

Puede localizar los componentes de Dynamic Media de una de las dos maneras siguientes:

* En una página web de Sites, abra **[!UICONTROL Propiedades]** y seleccione la pestaña **[!UICONTROL Avanzadas]**. Seleccione el idioma que desee para la localización.

   ![chlimage_1-172](assets/chlimage_1-538.png)

* En el selector de sitio, seleccione la página o el grupo de páginas que desee. Pulse **[!UICONTROL Properties]** y seleccione la pestaña **[!UICONTROL Advanced]**. Seleccione el idioma que desee para la localización.

   >[!NOTE]
   >
   >No todos los idiomas disponibles en el menú **[!UICONTROL Idioma]** tienen tokens asignados actualmente.

## Componentes de Dynamic Media disponibles {#dynamic-media-components}

Los componentes de Dynamic Media están disponibles cuando toca el icono **[!UICONTROL Componentes]** y luego filtra en **[!UICONTROL Dynamic Media]**.

Los componentes de Dynamic Media disponibles son los siguientes:

* **[!UICONTROL Dynamic Media:]** Se utiliza para recursos como imágenes, vídeos, catálogos electrónicos y conjuntos de giros.
* **[!UICONTROL Medios interactivos]** : se utiliza para cualquier recurso interactivo, como vídeo interactivo, imágenes interactivas o conjuntos de carrusel.
* **[!UICONTROL Medios panorámicos]** : se utilizan para imágenes panorámicas o recursos de imagen panorámica VR.
* **[!UICONTROL Medios de vídeo 360]** : utilice para recursos de vídeo de 360 y vídeo de 360 VR.

>[!NOTE]
>
>Estos componentes no están disponibles de forma predeterminada y deben estar disponibles mediante el editor de plantillas antes de su uso. Una vez que estén disponibles en el editor de plantillas, puede añadir los componentes a la página como lo haría con cualquier otro componente de Experience Manager.

![6_5_dynamicmediawcmcomponents](assets/6_5_dynamicmediawcmcomponents.png)

### Componente: Dynamic Media {#dynamic-media-component}

El componente Dynamic Media es inteligente. Según si agrega una imagen o un vídeo, tiene varias opciones. El componente admite ajustes preestablecidos de imagen, visores basados en imágenes, como conjuntos de imágenes, conjuntos de giros, conjuntos de medios mixtos y vídeo. Además, el visor es interactivo: el tamaño de la pantalla cambia automáticamente según el tamaño de la pantalla. Todos los visores son visores HTML5.

>[!NOTE]
>
>Si la página web tiene lo siguiente:
>
>* Varias instancias del componente Dynamic Media que se utilizan en la misma página.
>* Cada instancia utiliza el mismo tipo de recurso.

>
>
No se admite la asignación de un ajuste preestablecido de visualizador diferente a cada componente de Dynamic Media de esa página.
>
>Sin embargo, puede utilizar el mismo ajuste preestablecido de visualizador para todos los componentes de Dynamic Media que utilicen recursos del mismo tipo en la página.

Cuando se añade el componente de Dynamic Media y la opción **[!UICONTROL Configuración de Dynamic Media]** está vacía o no puede añadir un recurso correctamente, compruebe lo siguiente:

* La imagen tiene un archivo TIFF piramidal. Las imágenes importadas antes de que Dynamic Media esté habilitado no tienen un archivo tiff piramidal.

#### Uso de imágenes {#when-working-with-images}

El componente de Dynamic Media permite añadir imágenes dinámicas, como conjuntos de imágenes, conjuntos de giros y conjuntos de medios mixtos. Puede acercar, alejar y, si procede, girar una imagen en un conjunto de giros o seleccionar una imagen de otro tipo de conjunto.

También puede configurar el ajuste preestablecido de visor, el ajuste preestablecido de imagen o el formato de imagen directamente en el componente. Para que una imagen sea interactiva, puede establecer puntos de interrupción o aplicar un ajuste preestablecido de imagen interactiva.

Puede editar la siguiente Configuración de Dynamic Media tocando el icono **[!UICONTROL Editar]** en el componente y luego **[!UICONTROL Configuración de Dynamic Media]**.

![dm-settings-image-preset](assets/dm-settings-image-preset.png)

>[!NOTE]
>
>De forma predeterminada, el componente de imagen Dynamic Media es adaptable. Si desea que tenga un tamaño fijo, configúrelo en el componente de la pestaña **[!UICONTROL Avanzado]** con la **[!UICONTROL anchura]** y la **[!UICONTROL altura]** apropiadas.

* **[!UICONTROL Ajuste preestablecido de visor]**: seleccione un ajuste preestablecido de visor existente en la lista desplegable. Si el ajuste preestablecido de visualizador que está buscando no está visible, debe hacerlo visible. Consulte Administración de ajustes preestablecidos de visor. No se puede seleccionar un ajuste preestablecido de visualizador si se utiliza un ajuste preestablecido de imagen y, a la inversa,

   Esta opción es la única disponible si visualiza conjuntos de imágenes, conjuntos de giros o conjuntos de medios mixtos. Los ajustes preestablecidos de visor que se muestran también son ajustes preestablecidos de visor relevantes de solo inteligencia.

* **[!UICONTROL Modificadores del visualizador]**: los modificadores del visualizador toman la forma de par nombre=valor con un delimitador &amp; y permiten cambiar los visualizadores como se describe en la Guía de referencia del visualizador. Un ejemplo de modificador de visor es `posterimage=img.jpg&caption=text.vtt,1`, que establece una imagen diferente para la miniatura del vídeo y asocia un archivo de subtítulo/subtítulo/subtítulo cerrado con el vídeo.

* **[!UICONTROL Ajuste preestablecido de imagen]**: seleccione un ajuste preestablecido de imagen existente en la lista desplegable. Si el ajuste preestablecido de imagen que está buscando no está visible, debe hacerlo visible. Consulte Administración de ajustes preestablecidos de imagen. No se puede seleccionar un ajuste preestablecido de visualizador si se utiliza un ajuste preestablecido de imagen y, a la inversa,

   Esta opción no está disponible si visualiza conjuntos de imágenes, conjuntos de giros o conjuntos de medios mixtos.

* **[!UICONTROL Modificadores de imagen]**: puede aplicar efectos de imagen suministrando más comandos de imagen. Estos comandos se describen en Ajustes preestablecidos de imagen y en la referencia Comando de servicio de imágenes .

   Esta opción no está disponible si visualiza conjuntos de imágenes, conjuntos de giros o conjuntos de medios mixtos.

* **[!UICONTROL Puntos de interrupción]**: si utiliza este recurso en un sitio interactivo, debe agregar los puntos de interrupción de la imagen. Los puntos de interrupción de la imagen deben separarse con comas (,). Esta opción funciona cuando no se ha definido ninguna altura o anchura en el ajuste preestablecido de una imagen.

   Esta opción no está disponible si visualiza conjuntos de imágenes, conjuntos de giros o conjuntos de medios mixtos.

   Puede editar la siguiente Configuración avanzada tocando **[!UICONTROL Editar]** en el componente.

* **[!UICONTROL Título]**: permite cambiar el título de la imagen.

* **[!UICONTROL Texto alternativo]**: Agregue un título a la imagen para los usuarios que tengan los gráficos desactivados.

   Esta opción no está disponible si visualiza conjuntos de imágenes, conjuntos de giros o conjuntos de medios mixtos.

* **[!UICONTROL URL, Abrir en]**: puede configurar un recurso para abrir un vínculo. Defina la dirección URL y, en Abrir en, indique si quiere que se abra en la misma ventana o en una nueva.

   Esta opción no está disponible si visualiza conjuntos de imágenes, conjuntos de giros o conjuntos de medios mixtos.

* **[!UICONTROL Anchura]**: introduzca el valor en píxeles si desea que la imagen tenga un tamaño fijo. Dejar este valor en blanco hace que el recurso sea adaptable.

* **[!UICONTROL Altura]**: introduzca el valor en píxeles si desea que la imagen tenga un tamaño fijo. Dejar este valor en blanco hace que el recurso sea adaptable.


#### Uso de vídeos {#when-working-with-video}

Utilice el componente Dynamic Media para añadir vídeo dinámico a las páginas web. Al editar el componente, puede elegir utilizar un ajuste preestablecido de visualizador de vídeo predefinido para reproducir el vídeo en la página.

![chlimage_1-173](assets/chlimage_1-540.png)

Puede editar la siguiente Configuración de Dynamic Media haciendo clic en **[!UICONTROL Editar]** en el componente.

>[!NOTE]
>
>De forma predeterminada, el componente de vídeo de Dynamic Media es adaptable. Si desea que tenga un tamaño fijo, configúrelo en el componente con la **[!UICONTROL Anchura]** y **[!UICONTROL Altura]** en la pestaña **[!UICONTROL Avanzado]**.

* **[!UICONTROL Ajuste preestablecido de visualizador]**: seleccione un ajuste preestablecido de visualizador de vídeo existente en la lista desplegable. Si el ajuste preestablecido de visualizador que está buscando no está visible, debe hacerlo visible. Consulte Administración de ajustes preestablecidos de visor. 

* **[!UICONTROL Modificadores del visor]**: los modificadores del visor toman la forma de  `name=value` pares con un  `&` delimitador. Permiten cambiar los visores como se describe en la Guía de referencia de visores de Adobe. Un ejemplo de modificador de visor es `posterimage=img.jpg&caption=text.vtt,1`

   Con los modificadores del visor puede, por ejemplo, hacer lo siguiente:

   * Asocie un archivo de rótulo con un vídeo: [subtítulo](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/video/command-reference-url-video/r-html5-video-viewer-url-caption.html)
   * Asocie un archivo de navegación con un vídeo: [navegación](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/video/command-reference-url-video/r-html5-video-viewer-url-navigation.html)

      Puede editar la siguiente Configuración avanzada haciendo clic en **[!UICONTROL Editar]** en el componente.

* **[!UICONTROL Título]**: permite cambiar el título del vídeo.

* **[!UICONTROL Anchura]**: introduzca el valor en píxeles si desea que la imagen tenga un tamaño fijo. Dejar este valor en blanco hace que el recurso sea adaptable.

* **[!UICONTROL Altura]**: introduzca el valor en píxeles si desea que la imagen tenga un tamaño fijo. Dejar este valor en blanco hace que el recurso sea adaptable.

#### Al trabajar con Recorte inteligente {#when-working-with-smart-crop}

Utilice el componente Dynamic Media para añadir recursos de imagen de recorte inteligente a sus páginas web. Al editar el componente, puede elegir utilizar un ajuste preestablecido de visualizador de vídeo predefinido para reproducir el vídeo en la página.

Consulte [Uso de Recorte inteligente con recursos Experience Manager Dynamic Media](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/dynamic-media/smart-crop-feature-video-use.html#dynamic-media)

Consulte también [Perfiles de imagen](/help/assets/dynamic-media/image-profiles.md).

![dm-settings-smart-crop](assets/dm-settings-smart-crop.png)

Puede editar la siguiente configuración de Dynamic Media haciendo clic en **[!UICONTROL Editar]** en el componente.

>[!NOTE]
>
>De forma predeterminada, el componente de imagen Dynamic Media es adaptable. Si desea que tenga un tamaño fijo, configúrelo en el componente de la pestaña **[!UICONTROL Avanzado]** con la **[!UICONTROL anchura]** y la **[!UICONTROL altura]** apropiadas.

* **[!UICONTROL Modificadores de imagen]**: puede aplicar efectos de imagen suministrando más comandos de imagen. Estos comandos se describen en Ajustes preestablecidos de imagen y en la referencia Comando de servicio de imágenes .

   Esta opción no está disponible si visualiza conjuntos de imágenes, conjuntos de giros o conjuntos de medios mixtos.

   Puede editar la siguiente Configuración avanzada haciendo clic en **[!UICONTROL Editar]** en el componente.

* **[!UICONTROL Habilitar coincidencia de relación de aspecto]**: para permitir que Dynamic Media elija una representación de recorte inteligente con una relación de aspecto que coincida mejor con la relación de aspecto de la imagen original, seleccione esta opción.

* **[!UICONTROL Título]**: permite cambiar el título de la imagen de recorte inteligente.

* **[!UICONTROL Texto alternativo]**: Agregue un título a la imagen de recorte inteligente para los usuarios que tengan los gráficos desactivados.

   Esta opción no está disponible si visualiza conjuntos de imágenes, conjuntos de giros o conjuntos de medios mixtos.

* **[!UICONTROL URL, Abrir en]**: puede configurar un recurso para abrir un vínculo. Defina la dirección URL y, en Abrir en, indique si quiere que se abra en la misma ventana o en una nueva.

   Esta opción no está disponible si visualiza conjuntos de imágenes, conjuntos de giros o conjuntos de medios mixtos.

* **[!UICONTROL Anchura]**: introduzca el valor en píxeles si desea que la imagen tenga un tamaño fijo. Dejar este valor en blanco hace que el recurso sea adaptable.

* **[!UICONTROL Altura]**: introduzca el valor en píxeles si desea que la imagen tenga un tamaño fijo. Dejar este valor en blanco hace que el recurso sea adaptable.

### Componente: Medios interactivos {#interactive-media-component}

El componente de Medios interactivos es para los recursos que tienen elementos interactivos integrados en ellos, como puntos interactivos o mapas de imágenes. Si tiene una imagen interactiva, un vídeo interactivo o un titular de carrusel, utilice el componente de **[!UICONTROL Medios interactivos]**.

El componente de Medios interactivos es inteligente. Según si agrega una imagen o un vídeo, tiene varias opciones. Además, el visor es interactivo: el tamaño de la pantalla cambia automáticamente según el tamaño de la pantalla. Todos los visores son visores HTML5.

>[!NOTE]
>
>Si la página web tiene lo siguiente:
>
>* Varias instancias del componente de Medios interactivos que se utilizan en la misma página.
>* Cada instancia utiliza el mismo tipo de recurso.

>
>
No se admite la asignación de un ajuste preestablecido de visualizador diferente a cada componente de Medios interactivos de esa página.
>
>Sin embargo, puede utilizar el mismo ajuste preestablecido de visualizador para todos los componentes de Medios interactivos que utilicen recursos del mismo tipo en la página.

![chlimage_1-174](assets/chlimage_1-541.png)

Puede editar la siguiente configuración **[!UICONTROL General]** tocando **[!UICONTROL Editar]** en el componente.

* **[!UICONTROL Ajuste preestablecido de visor]**: seleccione un ajuste preestablecido de visor existente en la lista desplegable. Si el ajuste preestablecido de visualizador que está buscando no está visible, debe hacerlo visible. Los ajustes preestablecidos de visor se deben publicar para que se puedan usar. Consulte Administración de ajustes preestablecidos de visor. 

* **[!UICONTROL Título]**: permite cambiar el título del vídeo.

* **[!UICONTROL Anchura]**: introduzca el valor en píxeles si desea que la imagen tenga un tamaño fijo. Dejar este valor en blanco hace que el recurso sea adaptable.

* **[!UICONTROL Altura]**: introduzca el valor en píxeles si desea que la imagen tenga un tamaño fijo. Dejar este valor en blanco hace que el recurso sea adaptable.

   Puede editar las siguientes opciones de configuración **[!UICONTROL Añadir a carro]** al hacer clic en **[!UICONTROL Editar]** en el componente.

* **[!UICONTROL Mostrar recurso de producto]**: de forma predeterminada, este valor está seleccionado. El recurso del producto muestra una imagen del producto, según se ha definido en el módulo Commerce. Desactive la casilla para no mostrar el recurso del producto.

* **[!UICONTROL Mostrar precio del producto]**: de forma predeterminada, este valor está seleccionado. El precio del producto muestra el precio del artículo, según se ha definido en el módulo Commerce. Desactive la casilla para no mostrar el precio del producto.

* **[!UICONTROL Mostrar formulario de producto]**: de forma predeterminada, este valor no está seleccionado. En el formulario del producto se incluye las variantes de producto, como talla y color. Desactive la casilla para no mostrar las variantes del producto.

### Componente: Medios panorámicos {#panoramic-media-component}

El componente Panoramic Media es para aquellos recursos que son imágenes panorámicas esféricas. Estas imágenes proporcionan una experiencia de visualización de 360° de una habitación, propiedad, ubicación o paisaje. Para que una imagen pueda calificarse como panorama esférico, debe tener una o ambas de las siguientes opciones:

* Una relación de aspecto de 2:1.
* Etiquetado con las palabras clave `equirectangular` o (`spherical` + `panorama`) o (`spherical` + `panoramic`). Consulte [Uso de etiquetas](/help/sites-cloud/authoring/features/tags.md).

Tanto la proporción de aspecto como los criterios de palabra clave se aplican a los recursos panorámicos para la página de detalles de recursos y el componente WCM de **[!UICONTROL medios panorámicas]**.

>[!NOTE]
>
>Si la página web tiene lo siguiente:
>
>* Varias instancias del componente **[!UICONTROL Panoramic Media]** que se están utilizando en la misma página.
>* Cada instancia utiliza el mismo tipo de recurso.

>
>
No se admite la asignación de un ajuste preestablecido de visualizador diferente a cada componente **[!UICONTROL Medios panorámicos]** de esa página.
>
>Sin embargo, puede utilizar el mismo ajuste preestablecido de visualizador para todos los componentes de medios panorámicos que utilicen recursos del mismo tipo dentro de la página.

![panorámico-media-viewer-preset](assets/panoramic-media-viewer-preset.png)

Puede editar la siguiente configuración tocando **[!UICONTROL Configurar]** en el componente.

* **[!UICONTROL Ajuste preestablecido de visualizador]**: seleccione un visualizador existente en la lista desplegable Ajuste preestablecido de visualizador .

Si el ajuste preestablecido de visualizador que está buscando no está visible, compruebe que se ha publicado. Publicar ajustes preestablecidos de visualizador antes de usarlos. Consulte [Administración de ajustes preestablecidos de visor](/help/assets/dynamic-media/managing-viewer-presets.md). 

### Componente: Medios de vídeo 360 {#video-media-component}

Utilice el componente **[!UICONTROL Video 360 Media]** para procesar un vídeo equirectangular en la página web. Al hacerlo, se garantiza una experiencia de visualización inmersiva de una habitación, propiedad, ubicación, paisaje o procedimiento médico.

Durante la reproducción en una pantalla plana, el usuario controla el ángulo de visualización; la reproducción en dispositivos móviles suele utilizar sus controles giroscópicos integrados.

El visor incluye compatibilidad nativa con la entrega de 360 recursos de vídeo. De forma predeterminada, no es necesaria ninguna configuración adicional para la visualización o reproducción. El vídeo 360 se entrega con extensiones de vídeo estándar como .mp4, .mkv y .mov. El códec más común es H.264.

![6_5_360video_wcmcomponent-1](assets/6_5_360video_wcmcomponent-1.png)

Puede editar la siguiente configuración tocando **[!UICONTROL Configurar]** en el componente.

* **[!UICONTROL Ajuste preestablecido de visualizador]**: seleccione un visualizador existente en la lista desplegable Ajuste preestablecido de visualizador . Utilice Video360VR para usuarios finales que utilicen lentes de realidad virtuales. Incluye controles básicos de reproducción de vídeo y funciones de medios sociales. Utilice Video360_social, que incluye controles básicos de reproducción de vídeo. El procesamiento de vídeo se realiza en modo estéreo. El control de punto de vista manual está desactivado, pero el control giroscópico está activado. No hay características de medios sociales.

Si el ajuste preestablecido de visualizador que está buscando no está visible, compruebe que se ha publicado. Publicar ajustes preestablecidos de visualizador antes de usarlos. Consulte [Administración de ajustes preestablecidos de visor](/help/assets/dynamic-media/managing-viewer-presets.md). 

### Uso de HTTP/2 para enviar recursos de Dynamic Media {#using-http-to-delivery-dynamic-media-assets}

HTTP/2 es el nuevo protocolo web actualizado que mejora la forma en que se comunican los exploradores y los servidores. Proporciona una transferencia de información más rápida y reduce la cantidad de potencia de procesamiento necesaria. La entrega de recursos de Dynamic Media ahora puede realizarse a través de HTTP/2, lo que proporciona una mejor respuesta y tiempos de carga.

Consulte [Entrega HTTP2 de contenido](/help/assets/dynamic-media/http2faq.md) para obtener información detallada sobre cómo empezar a utilizar HTTP/2 con su cuenta de Dynamic Media.

>[!MORELIKETHIS]
>
>* [Uso del reproductor de vídeo en Experience Manager Dynamic Media](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/dynamic-media/dynamic-media-video-player-feature-video-use.html#dynamic-media)
>* [Uso de vídeo interactivo con Experience Manager Dynamic Media](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/dynamic-media/dynamic-media-interactive-video-feature-video-use.html#dynamic-media)
>* [Explicación del visualizador de recursos con Experience Manager Dynamic Media](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/dynamic-media/dynamic-media-viewer-feature-video-understand.html#dynamic-media)
>* [Uso de la miniatura de vídeo personalizada con Experience Manager Dynamic Media](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/dynamic-media/dynamic-media-video-thumbnails-feature-video-use.html#dynamic-media)
>* [Explicación de la administración de color con Experience Manager Dynamic Media](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/dynamic-media/dynamic-media-color-management-technical-video-setup.html#dynamic-media)
>* [Uso del enfoque de imagen con Experience Manager Dynamic Media](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/dynamic-media/dynamic-media-image-sharpening-feature-video-use.html#dynamic-media)

