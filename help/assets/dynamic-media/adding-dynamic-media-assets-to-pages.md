---
title: Adición de recursos de Dynamic Media a las páginas
description: Cómo agregar componentes de Dynamic Media a una página en Adobe Experience Manager como Cloud Service.
contentOwner: Rick Brough
translation-type: tm+mt
source-git-commit: cf607bd27463f23de29d0d6770940a01f3e36c87
workflow-type: tm+mt
source-wordcount: '3082'
ht-degree: 21%

---


# Adición de recursos de Dynamic Media a las páginas{#adding-dynamic-media-assets-to-pages}

Para añadir la funcionalidad Dynamic Media a los recursos que utilice en sus sitios web, puede agregar directamente en la página el componente **Dynamic Media**, **Interactive Media**, **Panoramic Media** o **Video 360 Media**. Puede acceder al modo Diseño y activar los componentes de Dynamic Media. A continuación, agregue estos componentes a la página y agregue recursos al componente. Los componentes de Dynamic Media son inteligentes: saben si va a añadir una imagen o un vídeo y las opciones de configuración disponibles cambian en consecuencia.

Puede agregar recursos de Dynamic Media directamente a la página si utiliza Experience Manager como WCM. Si está utilizando un tercero para su WCM, [link](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md) o [embed](/help/assets/dynamic-media/embed-code.md) sus recursos. Para ver un sitio web interactivo de terceros, consulte [entrega de imágenes optimizadas a un sitio adaptable](/help/assets/dynamic-media/responsive-site.md).

>[!NOTE]
>
>Asegúrese de publicar recursos antes de agregarlos a páginas en Experience Manager. Consulte [Publicación de Dynamic Media Assets](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md).

## Añadir un componente de Dynamic Media en una página {#adding-a-dynamic-media-component-to-a-page}

Añadir un componente de medios 3D, Dynamic Media, Medios interactivos, Medios panorámicas, Vídeo de recorte inteligente o Vídeo 360 a una página es lo mismo que agregar un componente a cualquier página.

**Añadir un componente de Dynamic Media en una página**

1. En Experience Manager, abra la página donde desee agregar el componente Dynamic Media.
1. En el panel izquierdo, toque el icono **[!UICONTROL Componentes]** y luego filtre para Dynamic Media.

   Si no hay ninguna lista de componentes de Dynamic Media disponible, es probable que deba habilitar los componentes de Dynamic Media que desee utilizar. Consulte [Activación de componentes de Dynamic Media](#enabling-dynamic-media-components).

   ![6_5_360video_wcmcomponent](assets/6_5_360video_wcmcomponent.png)

1. Arrastre un componente **[!UICONTROL Dynamic Media]** y colóquelo en la ubicación deseada en la página.

1. Pase el puntero directamente sobre el componente. Cuando el componente esté rodeado por un cuadro azul, toque una vez para mostrar la barra de herramientas del componente. Toque el icono **[!UICONTROL Configuración (llave inglesa)]**.

   ![6_5_360video_wcmcomponentconfigure](assets/6_5_360video_wcmcomponentconfigure.png)

1. Según el componente de Dynamic Media que haya colocado en la página, se abre un cuadro de diálogo de configuración. [Defina las ](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md#dynamic-media-components) opciones del componente según sea necesario.

   El ejemplo siguiente muestra el cuadro de diálogo de componentes **[!UICONTROL Video 360 Media]** de Dynamic Media y las opciones disponibles en la lista desplegable Ajustes preestablecidos de visor.

   ![Vídeo 360: componente multimedia](assets/6_5_360video_wcmcomponentviewerpreset.png)

   Componente de medios de Dynamic Media Video 360.

1. Cuando haya terminado, en la esquina superior derecha del cuadro de diálogo, toque la marca de verificación para guardar los cambios.

### Habilitación de componentes de Dynamic Media {#enabling-dynamic-media-components}

Si no hay componentes de Dynamic Media disponibles para agregar a una página, es probable que deba habilitar los componentes que desee utilizar.

1. En Experience Manager, abra la página donde desee agregar el componente Dynamic Media.
1. A la izquierda de la barra de herramientas, cerca de la parte superior de la página, toque el icono Información de página y, a continuación, toque **[!UICONTROL Editar plantilla]** en la lista desplegable.

   ![edit-template](/help/assets/assets-dm/edit-template.png)

1. En la parte derecha de la barra de herramientas cerca de la parte superior de la página, en la lista desplegable, toque **[!UICONTROL Estructura]**.

   ![Política](/help/assets/assets-dm/structure-mode.png)

1. Cerca de la parte inferior de la página, toque **[!UICONTROL Contenedor de diseño]** para abrir su barra de herramientas y, a continuación, toque el icono de directiva.
1. En la página **[!UICONTROL Contenedor de diseño]**, bajo el encabezado **[!UICONTROL Propiedades]**, asegúrese de que la ficha **[!UICONTROL Componentes permitidos]** está seleccionada.

   ![Componentes permitidos](/help/assets/assets-dm/allowed-components.png)

1. Desplácese hasta que vea **[!UICONTROL Dynamic Media]**.
1. Toque el icono > a la izquierda de **[!UICONTROL Dynamic Media]** y, a continuación, seleccione los componentes de Dynamic Media que desea habilitar.

   ![lista de componentes de Dynamic Media](/help/assets/assets-dm/dm-components-select.png)

1. Cerca de la esquina superior derecha de la página **[!UICONTROL Contenedor de diseño]**, toque el icono Listo (marca de verificación).

1. En la parte derecha de la barra de herramientas cerca de la parte superior de la página, en la lista desplegable, toque **[!UICONTROL Contenido inicial]**.
1. [Añada un componente de Dynamic Media a una ](#adding-a-dynamic-media-component-to-a-page) página como de costumbre.

## Localización de componentes de Dynamic Media {#localizing-dynamic-media-components}

Puede localizar componentes de Dynamic Media de una de estas dos formas:

* En una página web de Sites, abra **[!UICONTROL Propiedades]** y seleccione la pestaña **[!UICONTROL Avanzadas]**. Seleccione el idioma que desee para la localización.

   ![chlimage_1-172](assets/chlimage_1-538.png)

* En el selector de sitios, seleccione la página o el grupo de páginas que desee. Toque **[!UICONTROL Propiedades]** y seleccione la ficha **[!UICONTROL Avanzado]**. Seleccione el idioma que desee para la localización.

   >[!NOTE]
   >
   >No todos los idiomas disponibles en el menú **[!UICONTROL Idioma]** tienen tokens asignados actualmente.

## Componentes de Dynamic Media disponibles {#dynamic-media-components}

Los componentes de Dynamic Media están disponibles al tocar el icono **[!UICONTROL Componentes]** y luego filtrar por **[!UICONTROL Dynamic Media]**.

Los componentes de Dynamic Media disponibles son los siguientes:

* **[!UICONTROL Dynamic Media:]** Se utiliza para recursos como imágenes, vídeos, catálogos electrónicos y conjuntos de giros.
* **[!UICONTROL Medios]**  interactivos: se utiliza para cualquier recurso interactivo, como vídeo interactivo, imágenes interactivas o conjuntos de carrusel.
* **[!UICONTROL Medios]**  panorámicos - Uso para imágenes panorámicas o imágenes panorámicas VR.
* **[!UICONTROL Medios]**  de vídeo 360: uso para recursos de vídeo de 360 y 360 VR.

>[!NOTE]
>
>Estos componentes no están disponibles de forma predeterminada y deben estar disponibles mediante el editor de plantillas antes de su uso. Una vez que estén disponibles en el editor de plantillas, puede agregar los componentes a la página como lo haría con cualquier otro componente de Experience Manager.

![6_5_dynamicmediawcomponents](assets/6_5_dynamicmediawcmcomponents.png)

### Componente: Dynamic Media {#dynamic-media-component}

El componente Dynamic Media es inteligente. Según si agrega una imagen o un vídeo, tiene varias opciones. El componente admite ajustes preestablecidos de imagen, visores basados en imágenes, como conjuntos de imágenes, conjuntos de giros, conjuntos de medios mixtos y vídeo. Además, el visor responde: el tamaño de la pantalla cambia automáticamente en función del tamaño de la pantalla. Todos los visores son visores HTML5.

>[!NOTE]
>
>Si la página web tiene lo siguiente:
>
>* Varias instancias del componente Dynamic Media que se están utilizando en la misma página.
>* Cada instancia utiliza el mismo tipo de recurso.

>
>
No se admite la asignación de un ajuste preestablecido de visor diferente a cada componente de Dynamic Media de esa página.
>
>Sin embargo, puede utilizar el mismo ajuste preestablecido de visor para todos los componentes de Dynamic Media que utilicen recursos del mismo tipo, dentro de la página.

Cuando se añade el componente de Dynamic Media y la opción **[!UICONTROL Configuración de Dynamic Media]** está vacía o no puede añadir un recurso correctamente, compruebe lo siguiente:

* La imagen tiene un archivo TIFF piramidal. Las imágenes importadas antes de que Dynamic Media esté activado no tienen un archivo tiff piramidal.

#### Uso de imágenes {#when-working-with-images}

El componente de Dynamic Media permite añadir imágenes dinámicas, como conjuntos de imágenes, conjuntos de giros y conjuntos de medios mixtos. Puede acercar, alejar y, si procede, girar una imagen en un conjunto de giros o seleccionar una imagen de otro tipo de conjunto.

También puede configurar el ajuste preestablecido de visor, el ajuste preestablecido de imagen o el formato de imagen directamente en el componente. Para que una imagen responda, puede establecer los puntos de interrupción o aplicar un ajuste preestablecido de imagen adaptable.

Puede editar la siguiente Configuración de Dynamic Media tocando el icono **[!UICONTROL Editar]** en el componente y, a continuación, **[!UICONTROL Configuración de Dynamic Media]**.

![dm-settings-image-preset](assets/dm-settings-image-preset.png)

>[!NOTE]
>
>De forma predeterminada, el componente de imagen Dynamic Media es adaptable. Si desea que tenga un tamaño fijo, configúrelo en el componente de la pestaña **[!UICONTROL Avanzado]** con la **[!UICONTROL anchura]** y la **[!UICONTROL altura]** apropiadas.

* **[!UICONTROL Ajuste preestablecido]** de visor: seleccione un ajuste preestablecido de visor existente en la lista desplegable. Si el ajuste preestablecido de visor que está buscando no está visible, debe hacerlo visible. Consulte Administración de ajustes preestablecidos de visor. No puede seleccionar un ajuste preestablecido de visor si utiliza un ajuste preestablecido de imagen y, a la inversa, lo hace.

   Esta opción es la única disponible si está viendo conjuntos de imágenes, conjuntos de giros o conjuntos de medios mixtos. Los ajustes preestablecidos de visor que se muestran también son ajustes preestablecidos de visor relevantes de solo inteligente.

* **[!UICONTROL Modificadores]** de visor: los modificadores de visor adoptan la forma de par nombre=valor con un delimitador &amp; y permiten cambiar los visores como se describe en la Guía de referencia de visores. Un ejemplo de modificador de visor es `posterimage=img.jpg&caption=text.vtt,1`, que establece una imagen diferente para la miniatura de vídeo y asocia un archivo de subtítulo o subtítulo con el vídeo.

* **[!UICONTROL Ajuste preestablecido]** de imagen: seleccione un ajuste preestablecido de imagen existente en la lista desplegable. Si el ajuste preestablecido de imagen que está buscando no está visible, debe hacerlo visible. Consulte Administración de ajustes preestablecidos de imagen. No puede seleccionar un ajuste preestablecido de visor si utiliza un ajuste preestablecido de imagen y, a la inversa, lo hace.

   Esta opción no está disponible si visualiza conjuntos de imágenes, conjuntos de giros o conjuntos de medios mixtos.

* **[!UICONTROL Modificadores]** de imagen: puede aplicar efectos de imagen proporcionando más comandos de imagen. Estos comandos se describen en Ajustes preestablecidos de imagen y en la referencia de comandos de servicio de imágenes.

   Esta opción no está disponible si visualiza conjuntos de imágenes, conjuntos de giros o conjuntos de medios mixtos.

* **[!UICONTROL Puntos de interrupción]**: si utiliza este recurso en un sitio interactivo, debe agregar los puntos de interrupción de la imagen. Los puntos de interrupción de la imagen deben separarse con comas (,). Esta opción funciona cuando no se ha definido ninguna altura o anchura en el ajuste preestablecido de una imagen.

   Esta opción no está disponible si visualiza conjuntos de imágenes, conjuntos de giros o conjuntos de medios mixtos.

   Puede editar la siguiente Configuración avanzada tocando **[!UICONTROL Editar]** en el componente.

* **[!UICONTROL Título]**: permite cambiar el título de la imagen.

* **[!UICONTROL Texto]** alternativo: Añada un título a la imagen para aquellos usuarios que tengan los gráficos desactivados.

   Esta opción no está disponible si visualiza conjuntos de imágenes, conjuntos de giros o conjuntos de medios mixtos.

* **[!UICONTROL URL, Abrir en]**: puede definir un recurso para abrir un vínculo. Defina la dirección URL y, en Abrir en, indique si quiere que se abra en la misma ventana o en una nueva.

   Esta opción no está disponible si visualiza conjuntos de imágenes, conjuntos de giros o conjuntos de medios mixtos.

* **[!UICONTROL Anchura]**: introduzca el valor en píxeles si desea que la imagen tenga un tamaño fijo. Al dejar este valor en blanco, el recurso se adapta.

* **[!UICONTROL Altura]**: introduzca el valor en píxeles si desea que la imagen tenga un tamaño fijo. Al dejar este valor en blanco, el recurso se adapta.


#### Uso de vídeos {#when-working-with-video}

Utilice el componente Dynamic Media para añadir vídeo dinámico a las páginas web. Al editar el componente, puede elegir utilizar un ajuste preestablecido de visor de vídeo para reproducir el vídeo en la página.

![chlimage_1-173](assets/chlimage_1-540.png)

Puede editar la siguiente configuración de Dynamic Media haciendo clic en **[!UICONTROL Editar]** en el componente.

>[!NOTE]
>
>De forma predeterminada, el componente de vídeo de Dynamic Media es adaptable. Si desea que sea un tamaño fijo, configúrelo en el componente con la **[!UICONTROL anchura]** y **[!UICONTROL altura]** en la ficha **[!UICONTROL Avanzado]**.

* **[!UICONTROL Ajuste preestablecido]** de visor: seleccione un ajuste preestablecido de visor de vídeo existente en la lista desplegable. Si el ajuste preestablecido de visor que está buscando no está visible, debe hacerlo visible. Consulte Administración de ajustes preestablecidos de visor. 

* **[!UICONTROL Modificadores]** de visor: los modificadores de visor adoptan la forma de  `name=value` pares con un  `&` delimitador. Permiten cambiar los visores como se describe en la Guía de referencia de visores de Adobe. Un ejemplo de modificador de visor es `posterimage=img.jpg&caption=text.vtt,1`

   Con los modificadores del visor puede, por ejemplo, hacer lo siguiente:

   * Asocie un archivo de subtítulos con un vídeo: [caption](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/video/command-reference-url-video/r-html5-video-viewer-url-caption.html)
   * Asociación de un archivo de navegación con un vídeo: [navegación](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/video/command-reference-url-video/r-html5-video-viewer-url-navigation.html)

      Puede editar la siguiente Configuración avanzada haciendo clic en **[!UICONTROL Editar]** en el componente.

* **[!UICONTROL Título]**: cambie el título del vídeo.

* **[!UICONTROL Anchura]**: introduzca el valor en píxeles si desea que la imagen tenga un tamaño fijo. Al dejar este valor en blanco, el recurso se adapta.

* **[!UICONTROL Altura]**: introduzca el valor en píxeles si desea que la imagen tenga un tamaño fijo. Al dejar este valor en blanco, el recurso se adapta.

#### Al trabajar con Smart Crop {#when-working-with-smart-crop}

Utilice el componente Dynamic Media para añadir recursos de imagen de recorte inteligente a sus páginas web. Al editar el componente, puede elegir utilizar un ajuste preestablecido de visor de vídeo para reproducir el vídeo en la página.

Consulte [Uso de Smart Crop con Recursos Experience Manager Dynamic Media](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/dynamic-media/smart-crop-feature-video-use.html#dynamic-media)

Consulte también [Perfiles de imagen](/help/assets/dynamic-media/image-profiles.md).

![dm-settings-smart-cut](assets/dm-settings-smart-crop.png)

Puede editar la siguiente configuración de Dynamic Media haciendo clic en **[!UICONTROL Editar]** en el componente.

>[!NOTE]
>
>De forma predeterminada, el componente de imagen Dynamic Media es adaptable. Si desea que tenga un tamaño fijo, configúrelo en el componente de la pestaña **[!UICONTROL Avanzado]** con la **[!UICONTROL anchura]** y la **[!UICONTROL altura]** apropiadas.

* **[!UICONTROL Modificadores]** de imagen: puede aplicar efectos de imagen proporcionando más comandos de imagen. Estos comandos se describen en Ajustes preestablecidos de imagen y en la referencia de comandos de servicio de imágenes.

   Esta opción no está disponible si visualiza conjuntos de imágenes, conjuntos de giros o conjuntos de medios mixtos.

   Puede editar la siguiente Configuración avanzada haciendo clic en **[!UICONTROL Editar]** en el componente.

* **[!UICONTROL Habilitar coincidencia]** de relación de aspecto: para permitir que Dynamic Media elija una representación de recorte inteligente con una proporción de aspecto que mejor se ajuste a la proporción de aspecto de la imagen original, seleccione esta opción.

* **[!UICONTROL Título]**: cambie el título de la imagen de recorte inteligente.

* **[!UICONTROL Texto]** alternativo: Añada un título a la imagen de recorte inteligente para los usuarios que tienen gráficos desactivados.

   Esta opción no está disponible si visualiza conjuntos de imágenes, conjuntos de giros o conjuntos de medios mixtos.

* **[!UICONTROL URL, Abrir en]**: puede definir un recurso para abrir un vínculo. Defina la dirección URL y, en Abrir en, indique si quiere que se abra en la misma ventana o en una nueva.

   Esta opción no está disponible si visualiza conjuntos de imágenes, conjuntos de giros o conjuntos de medios mixtos.

* **[!UICONTROL Anchura]**: introduzca el valor en píxeles si desea que la imagen tenga un tamaño fijo. Al dejar este valor en blanco, el recurso se adapta.

* **[!UICONTROL Altura]**: introduzca el valor en píxeles si desea que la imagen tenga un tamaño fijo. Al dejar este valor en blanco, el recurso se adapta.

### Componente: Medios interactivos {#interactive-media-component}

El componente de Medios interactivos es para los recursos que tienen elementos interactivos integrados en ellos, como puntos interactivos o mapas de imágenes. Si tiene una imagen interactiva, un vídeo interactivo o un titular de carrusel, utilice el componente de **[!UICONTROL Medios interactivos]**.

El componente Medios interactivos es inteligente. Según si agrega una imagen o un vídeo, tiene varias opciones. Además, el visor responde: el tamaño de la pantalla cambia automáticamente en función del tamaño de la pantalla. Todos los visores son visores HTML5.

>[!NOTE]
>
>Si la página web tiene lo siguiente:
>
>* Varias instancias del componente Medios interactivos que se están utilizando en la misma página.
>* Cada instancia utiliza el mismo tipo de recurso.

>
>
No se admite la asignación de un ajuste preestablecido de visor diferente a cada componente de medios interactivos de esa página.
>
>Sin embargo, puede utilizar el mismo ajuste preestablecido de visor para todos los componentes de medios interactivos que utilicen recursos del mismo tipo en la página.

![chlimage_1-174](assets/chlimage_1-541.png)

Puede editar la siguiente configuración **[!UICONTROL General]** tocando **[!UICONTROL Editar]** en el componente.

* **[!UICONTROL Ajuste preestablecido]** de visor: seleccione un ajuste preestablecido de visor existente en la lista desplegable. Si el ajuste preestablecido de visor que está buscando no está visible, debe hacerlo visible. Los ajustes preestablecidos de visor se deben publicar para que se puedan usar. Consulte Administración de ajustes preestablecidos de visor. 

* **[!UICONTROL Título]**: cambie el título del vídeo.

* **[!UICONTROL Anchura]**: introduzca el valor en píxeles si desea que la imagen tenga un tamaño fijo. Al dejar este valor en blanco, el recurso se adapta.

* **[!UICONTROL Altura]**: introduzca el valor en píxeles si desea que la imagen tenga un tamaño fijo. Al dejar este valor en blanco, el recurso se adapta.

   Puede editar las siguientes opciones de configuración **[!UICONTROL Añadir a carro]** al hacer clic en **[!UICONTROL Editar]** en el componente.

* **[!UICONTROL Mostrar recurso]** de producto: este valor está seleccionado de forma predeterminada. El recurso del producto muestra una imagen del producto, según se ha definido en el módulo Commerce. Desactive la casilla para no mostrar el recurso del producto.

* **[!UICONTROL Mostrar precio]** del producto: este valor está seleccionado de forma predeterminada. El precio del producto muestra el precio del artículo, según se ha definido en el módulo Commerce. Desactive la casilla para no mostrar el precio del producto.

* **[!UICONTROL Mostrar formulario]** de producto: de forma predeterminada, este valor no está seleccionado. En el formulario del producto se incluye las variantes de producto, como talla y color. Desactive la casilla para no mostrar las variantes del producto.

### Componente: Medios panorámicos {#panoramic-media-component}

El componente de medios panorámicos es para aquellos recursos que son imágenes panorámicas esféricas. Estas imágenes proporcionan una experiencia de visualización de 360° de una habitación, propiedad, ubicación o paisaje. Para que una imagen se considere panorámica esférica, debe tener una O ambas de las opciones siguientes:

* Proporción de aspecto de 2:1.
* Se etiqueta con las palabras clave `equirectangular` o (`spherical` + `panorama`) o (`spherical` + `panoramic`). Consulte [Uso de etiquetas](/help/sites-cloud/authoring/features/tags.md).

Tanto la proporción de aspecto como los criterios de palabra clave se aplican a los recursos panorámicos para la página de detalles de recursos y el componente WCM de **[!UICONTROL medios panorámicas]**.

>[!NOTE]
>
>Si la página web tiene lo siguiente:
>
>* Varias instancias del componente **[!UICONTROL Medios panorámicos]** que se están utilizando en la misma página.
>* Cada instancia utiliza el mismo tipo de recurso.

>
>
No se admite la asignación de un ajuste preestablecido de visor diferente a cada componente **[!UICONTROL de medios panorámicas]** de esa página.
>
>Sin embargo, puede utilizar el mismo ajuste preestablecido de visor para todos los componentes de medios panorámicas que utilicen recursos del mismo tipo en la página.

![panorámico-media-viewer-preset](assets/panoramic-media-viewer-preset.png)

Puede editar la siguiente configuración tocando **[!UICONTROL Configurar]** en el componente.

* **[!UICONTROL Ajuste preestablecido]** de visor: seleccione un visor existente en la lista desplegable de ajustes preestablecidos de visor.

Si el ajuste preestablecido de visor que está buscando no está visible, asegúrese de que se ha publicado. Publique los ajustes preestablecidos de visor antes de utilizarlos. Consulte [Administración de ajustes preestablecidos de visor](/help/assets/dynamic-media/managing-viewer-presets.md). 

### Componente: Medios de video 360 {#video-media-component}

Utilice el componente **[!UICONTROL Video 360 Media]** para procesar un vídeo equirectangular en la página web. Esto garantiza una experiencia de visualización envolvente de una habitación, propiedad, ubicación, paisaje o procedimiento médico.

Durante la reproducción en una pantalla plana, el usuario tiene el control del ángulo de visión; la reproducción en dispositivos móviles suele utilizar sus controles giroscópicos integrados.

El visor incluye compatibilidad nativa con el envío de 360 recursos de vídeo. De forma predeterminada, no es necesaria ninguna configuración adicional para la visualización o reproducción. El vídeo 360 se distribuye con extensiones de vídeo estándar como .mp4, .mkv y .mov. El códec más común es H.264.

![6_5_360video_wcmcomponent-1](assets/6_5_360video_wcmcomponent-1.png)

Puede editar la siguiente configuración tocando **[!UICONTROL Configurar]** en el componente.

* **[!UICONTROL Ajuste preestablecido]** de visor: seleccione un visor existente en la lista desplegable de ajustes preestablecidos de visor. Utilice Video360VR para los usuarios finales que utilicen gafas de realidad virtual. Incluye controles básicos de reproducción de vídeo y funciones de medios sociales. Utilice Video360_social, que incluye controles básicos de reproducción de vídeo. La representación de vídeo se realiza en modo estéreo. El control manual del punto de vista está desactivado, pero el control giroscópico está activado. No hay características de medios sociales.

Si el ajuste preestablecido de visor que está buscando no está visible, asegúrese de que se ha publicado. Publique los ajustes preestablecidos de visor antes de utilizarlos. Consulte [Administración de ajustes preestablecidos de visor](/help/assets/dynamic-media/managing-viewer-presets.md). 

### Uso de HTTP/2 para envío de recursos de Dynamic Media {#using-http-to-delivery-dynamic-media-assets}

HTTP/2 es el nuevo protocolo web actualizado que mejora la forma en que se comunican los exploradores y los servidores. Proporciona una transferencia de información más rápida y reduce la cantidad de potencia de procesamiento necesaria. Ahora, el envío de recursos de Dynamic Media puede realizarse a través de HTTP/2, lo que proporciona una mejor respuesta y tiempos de carga.

Consulte [Envío HTTP2 de contenido](/help/assets/dynamic-media/http2faq.md) para obtener información detallada sobre cómo empezar a utilizar HTTP/2 con su cuenta de Dynamic Media.

>[!MORELIKETHIS]
>
>* [Uso del reproductor de vídeo en Experience Manager Dynamic Media](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/dynamic-media/dynamic-media-video-player-feature-video-use.html#dynamic-media)
>* [Uso de vídeo interactivo con Dynamic Media Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/dynamic-media/dynamic-media-interactive-video-feature-video-use.html#dynamic-media)
>* [Información sobre Asset Viewer con Experience Manager Dynamic Media](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/dynamic-media/dynamic-media-viewer-feature-video-understand.html#dynamic-media)
>* [Uso de miniaturas de vídeo personalizadas con Dynamic Media Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/dynamic-media/dynamic-media-video-thumbnails-feature-video-use.html#dynamic-media)
>* [Explicación de la administración de color con Experience Manager Dynamic Media](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/dynamic-media/dynamic-media-color-management-technical-video-setup.html#dynamic-media)
>* [Uso del enfoque de imagen con Experience Manager Dynamic Media](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/dynamic-media/dynamic-media-image-sharpening-feature-video-use.html#dynamic-media)

