---
title: Banner de carrusel
description: Aprenda a trabajar con los titulares de carrusel en Dynamic Media.
contentOwner: Rick Brough
feature: Carousel Banners
role: User
exl-id: 34541302-6610-4f5e-af93-c95328dda910
source-git-commit: 35caac30887f17077d82f3370f1948e33d7f1530
workflow-type: tm+mt
source-wordcount: '4535'
ht-degree: 1%

---

# Banner de carrusel{#carousel-banners}

Los banners de carrusel permiten a los especialistas en marketing impulsar la conversión creando fácilmente contenido promocional giratorio interactivo y entregándolo a cualquier pantalla.

La creación y modificación del contenido de los titulares promocionales puede llevar mucho tiempo, lo que limita su capacidad de publicar rápidamente contenido nuevo o de dirigirlo mejor. Los banners de carrusel le permiten crear o modificar rápidamente banners giratorios y añadir interactividad, como la vinculación de puntos interactivos a los detalles del producto o recursos relacionados. Puede enviarlos a cualquier pantalla, lo que le permite llevar el nuevo contenido promocional al mercado más rápido.

Los titulares de carrusel se designan mediante un banner con la palabra **[!UICONTROL CAROUSELSET]**:

![chlimage_1-438](assets/chlimage_1-438.png)

En su sitio web, un banner de carrusel puede tener el siguiente aspecto:

![chlimage_1-439](assets/chlimage_1-439.png)

Aquí puede navegar por las imágenes seleccionando los números. Además, las diapositivas giran automáticamente en función de un intervalo de tiempo que se pueda personalizar. Las imágenes de un banner de carrusel admiten zonas interactivas y mapas de imágenes. Los usuarios pueden seleccionar o ir a un hipervínculo o acceder a una ventana de vista rápida.

En este ejemplo, un usuario ha seleccionado un mapa de imagen y accedió a la ventana Vista rápida para guantes:

![chlimage_1-440](assets/chlimage_1-440.png)

## Ver cómo se crean los titulares de carrusel {#watch-how-carousel-banners-are-created}

Mire este tutorial en [cómo se crean los titulares de carrusel](https://s7d5.scene7.com/s7viewers/html5/VideoViewer.html?videoserverurl=https://s7d5.scene7.com/is/content/&amp;emailurl=https://s7d5.scene7.com/s7/emailFriend&amp;serverUrl=https://s7d5.scene7.com/is/image/&amp;config=Scene7SharedAssets/Universal_HTML5_Video_social&amp;contenturl=https://s7d5.scene7.com/skins/&amp;asset=S7tutorials/InteractiveCarouselBanner) (Duración: 10 minutos y 33 segundos). También aprenderá a previsualizar, editar y enviar banners de carrusel.

>[!NOTE]
>
>Los usuarios no administrativos deben agregarse al **[!UICONTROL dam-users]** para poder crear o editar banners de carrusel. Si tiene problemas para crear o editar, consulte con el administrador del sistema, que puede agregarle al **d[!UICONTROL am-users]** grupo.

## Inicio rápido: Banner de carrusel {#quick-start-carousel-banners}

Para ponerle en marcha rápidamente:

1. [Identificar las variables de zona interactiva y mapa de imagen](#identifying-hotspot-and-image-map-variables) (solo para clientes que utilizan Adobe Experience Manager Assets + Dynamic Media)

   Comience por identificar las variables dinámicas que utiliza la implementación de vista rápida existente. De este modo, podrá introducir los puntos interactivos y los datos de mapas de imágenes correctamente durante el proceso de creación de banners de carrusel en Experience Manager Assets.

<!-- LEAVE; COMMERCE BEING ADDED AGAIN IN THE FUTURE

   >[!NOTE]
   >
   >If you are an Experience Manager Sites or Ecommerce customer, you can use the built-in feature to navigate to product pages and lookup the existing skus in the product catalog. You do not need to manually enter hotspot or image map variables.
   >
   >
   >If you are an Experience ManagerAssets and Dynamic Media customer, you will manually enter data for hotspots and image maps, and then integrate the published URL or Embed code with your third-party content management system.

-->

1. Opcional: [Cree un ajuste preestablecido de visualizador de conjuntos de carrusel](/help/assets/dynamic-media/managing-viewer-presets.md), según sea necesario.

   Si es administrador, puede personalizar el comportamiento y el aspecto del carrusel creando su propio ajuste preestablecido de visualizador de carrusel. La principal ventaja es que puede reutilizar este ajuste preestablecido de visualizador personalizado para varios carruseles. Sin embargo, los usuarios pueden personalizar de forma opcional el comportamiento y el aspecto del carrusel directamente durante la creación del carrusel. Se prefiere este enfoque cuando se desea un diseño específico para un carrusel determinado.

1. [Cargar un titular de imagen](#uploading-image-banners).

   Cargue banners de imagen que desee hacer interactivos.

1. [Crear un conjunto de carrusel](#creating-carousel-sets).

   En Conjuntos de carruseles, los usuarios navegan por las imágenes de banner y seleccionan zonas interactivas o mapas de imágenes para acceder al contenido relevante.

   Para crear un conjunto de carrusel en Assets, seleccione **[!UICONTROL Crear]** y, a continuación, seleccione **[!UICONTROL Conjuntos de carrusel]**. Agregue recursos a las diapositivas y seleccione **[!UICONTROL Guardar]**. También puede editar el aspecto y el comportamiento del carrusel directamente en el editor.

1. [Agregar zonas interactivas o mapas de imágenes a un titular de imagen](#adding-hotspots-or-image-maps-to-an-image-banner).

   Agregue una o más zonas interactivas o mapas de imágenes a un banner de imagen. A continuación, asocie cada uno de ellos a una acción, como un vínculo, una vista rápida o un fragmento de experiencia. Después de agregar zonas interactivas o mapas de imágenes, para finalizar esta tarea, publique el conjunto de carrusel. La publicación crea el código incrustado que puede utilizar para copiar y aplicar a la página de aterrizaje del sitio web.

   Consulte [(Opcional) Vista previa de letreros de carrusel](#optional-previewing-carousel-banners) - Opcional. Si lo desea, puede ver una representación del conjunto de carrusel y probar su interactividad.

1. [Publicar titulares de carrusel](#publishing-carousel-banners).

   Puede publicar un conjunto de carrusel como lo haría con cualquier recurso. En Assets, vaya al conjunto de carrusel, selecciónelo y seleccione **[!UICONTROL Publicación]**. Al publicar un conjunto de carrusel, se activa la dirección URL y la cadena Incrustar.

1. Realice una de las siguientes acciones:

   * [Agregue un banner de carrusel a la página de su sitio web](#adding-a-carousel-banner-to-your-website-page)Puede añadir la URL del banner de carrusel o incrustar el código que ha copiado en la página del sitio web.

      * [Integrar el banner de carrusel con una vista rápida existente](#integrating-the-carousel-banner-with-an-existing-quickview). Si utiliza un sistema de administración de contenido web de terceros, debe integrar el nuevo titular de carrusel con la implementación de vista rápida existente en el sitio web.
   * [Agregue un banner de carrusel a su sitio web en Experience Manager](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md). Si es cliente de Experience Manager Sites, puede añadir el conjunto de carrusel directamente a la página mediante el componente Medios interactivos.


Si debe editar los conjuntos de carrusel, consulte [Editar conjuntos de carrusel](#editing-carousel-sets). Además, puede ver y editar [Propiedades del conjunto de carrusel](/help/assets/manage-digital-assets.md#editing-properties).

## Identificar variables de zona interactiva y mapa de imagen {#identifying-hotspot-and-image-map-variables}

Comience por identificar las variables dinámicas que utiliza la implementación de vista rápida existente. Este método le ayuda a introducir correctamente puntos interactivos o datos de mapa de imagen durante el proceso de creación de conjuntos de carrusel en Experience Manager Assets.

Al agregar zonas interactivas o mapas de imágenes a una imagen de titular, se asigna un SKU (unidad de mantenimiento de existencias). También puede asignar variables adicionales opcionales a cada zona interactiva o mapa de imagen. Estas variables se utilizan más adelante para hacer coincidir puntos interactivos o mapas de imágenes con contenido de vista rápida.

<!-- LEAVE; COMMERCE BEING ADDED LATER

>[!NOTE]
>
>If you are an Experience Manager Sites and/or Experience Manager Ecommerce customer, skip this step. You do not need to manually identify hotspot or image map variables; you can use the integration with Ecommerce for product integration. See information on [setting up eCommerce](/help/sites-cloud/administering/generic.md). In addition, you can use the Interactive component and add it to your web page.
>
>If you are an Experience Manager Assets or Media customer, you publish the URL or Embed code and then integrate with your third-party content management system and identify hotspots and image maps manually.

-->

Es importante identificar correctamente el número y el tipo de variables que se asociarán con los datos de zona interactiva o mapa de imagen. Cada zona interactiva o mapa de imagen que se añada a una imagen de banner debe contener suficiente información para identificar sin ambigüedades el producto en el sistema back-end existente. Al mismo tiempo, asegúrese de que cada zona interactiva o mapa de imagen no incluya más datos de los necesarios. El motivo es que esto haría que el proceso de entrada de datos sea demasiado complejo y en curso, o la administración de mapas de imágenes sea más propensa a errores.

Existen diferentes maneras de identificar un conjunto de variables que se utilizarán para los datos de zona interactiva o mapa de imagen.

A veces es suficiente consultar a los especialistas de TI responsables de la implementación de Quickview existente. Es probable que sepan cuál es el conjunto mínimo de datos para identificar la vista rápida en el sistema. Sin embargo, es posible simplemente analizar el comportamiento existente del código front-end.

La mayoría de las implementaciones de vista rápida utilizan el siguiente paradigma:

* El usuario activa un elemento de interfaz de usuario en el sitio web. Por ejemplo, si selecciona un **[!UICONTROL Vista rápida]** botón.
* El sitio web envía una solicitud de Ajax al back-end para cargar los datos o el contenido de la vista rápida, si es necesario.
* Los datos de vista rápida se traducen al contenido como preparación para su renderización en la página web.
* Por último, el código front-end procesa visualmente dicho contenido en la pantalla.

El método entonces es visitar diferentes áreas del sitio web existente donde se implementa la función Vista rápida. A continuación, déclencheur la vista rápida y adquiera la URL de Ajax que envía la página web para cargar los datos o el contenido de la vista rápida.

Normalmente no es necesario que utilice ninguna herramienta de depuración especializada. Los navegadores web modernos cuentan con inspectores web que realizan un trabajo adecuado. A continuación se indican algunos ejemplos de exploradores web que incluyen inspectores web:

* Para ver todas las solicitudes HTTP salientes en Google Chrome, pulse F12 (Windows®) o Comando-Opción-I (Mac) para abrir el panel de herramientas para desarrolladores. Seleccione la pestaña Red.
* En Firefox, puede activar el complemento Firebug pulsando F12 (Windows®) o Comando-Opción-I (Mac). Utilice su ficha Red o la herramienta Inspector integrada y su pestaña Red.

Cuando la supervisión de red está activada en el explorador, ponga en déclencheur la vista rápida en la página.

Ahora, busque la URL de Ajax de vista rápida en el registro de red y copie la URL grabada para su análisis futuro. Por lo general, cuando se déclencheur la vista rápida hay numerosas solicitudes que se envían al servidor. Normalmente, la URL de Ajax de vista rápida es una de las primeras de la lista. Tiene una ruta o porción de cadena de consulta compleja y su tipo MIME de respuesta es `text/html`, `text/xml`o `text/javascript`.

Durante este proceso, es importante visitar diferentes áreas del sitio web, con diferentes tipos y categorías de productos. El motivo es que las direcciones URL de vista rápida tienen partes que son comunes para una categoría de sitio web determinada, pero cambian solo si visita un área diferente del sitio web.

En el caso más simple, la única parte de la variable en la URL de vista rápida es el SKU del producto. En este caso, el valor SKU es la única pieza de datos que necesita para agregar zonas interactivas o mapas de imagen a la imagen del banner.

Sin embargo, en casos complejos, la URL de vista rápida tiene diferentes elementos además del SKU. Algunos de estos elementos incluyen ID de categoría, código de color, código de tamaño, etc. En estos casos, cada elemento es una variable independiente en la definición de datos de zona interactiva o mapa de imagen en la función de titular de carrusel.

Veamos los siguientes ejemplos de direcciones URL de vista rápida y las variables de zona interactiva o mapa de imagen que se obtienen:

<table>
 <tbody>
  <tr>
   <td>SKU único, que se encuentra en la cadena de consulta.</td>
   <td><p>Las direcciones URL de vista rápida registradas incluyen lo siguiente:</p>
    <ul>
     <li><p><code>https://server/json?productId=866558&amp;source=100</code></p> </li>
     <li><p><code>https://server/json?productId=1196184&amp;source=100</code></p> </li>
     <li><p><code>https://server/json?productId=1081492&amp;source=100</code></p> </li>
     <li><p><code>https://server/json?productId=1898294&amp;source=100</code></p> </li>
    </ul> <p>La única parte variable de la dirección URL es el valor de la variable <code>productId=</code> parámetro de cadena de consulta, y es claramente un valor de SKU. Por lo tanto, las zonas interactivas o los mapas de imágenes solo necesitan campos SKU rellenados con valores como <code>866558,</code> <code>1196184,</code> <code>1081492,</code> <code>1898294.</code></p> </td>
  </tr>
  <tr>
   <td>SKU único, que se encuentra en la ruta de URL.</td>
   <td><p>Las direcciones URL de vista rápida registradas incluyen lo siguiente:</p>
    <ul>
     <li><p><code>https://server/product/6422350843</code></p> </li>
     <li><p><code>https://server/product/1607745002</code></p> </li>
     <li><p><code>https://server/product/0086724882</code></p> </li>
    </ul> <p>La parte variable se encuentra en la última parte de la ruta y se convierte en el valor SKU de las zonas interactivas o los mapas de imágenes:<strong><code>6422350843</code>, <code>1607745002,</code> </strong><code>0086724882.</code></p> </td>
  </tr>
  <tr>
   <td>SKU e ID de categoría en la cadena de consulta.</td>
   <td><p>Las direcciones URL de vista rápida registradas incluyen lo siguiente:</p>
    <ul>
     <li><p><code>https://server/quickView/product/?category=1100004&amp;prodId=305466</code></p> </li>
     <li><p><code>https://server/quickView/product/?category=1100004&amp;prodId=310181</code></p> </li>
     <li><p><code>https://server/quickView/product/?category=1740148&amp;prodId=308706</code></p> </li>
    </ul> <p>En este caso, hay dos partes diferentes en la dirección URL. El SKU se almacena en la variable <code>prodId</code> y el ID de categoría se almacena en la variable <code>category=</code>parámetro.</p> <p>Como tal, las definiciones de zona interactiva/mapa de imagen son pares. Es decir, un valor de SKU y una variable adicional llamada <code>categoryId</code>. Los pares resultantes son los siguientes:</p>
    <ul>
     <li><p>SKU <strong><code>305466</code></strong> y <code>categoryId</code> es <code>1100004</code>.</p> </li>
     <li><p>SKU <strong><code>310181</code></strong> y <code>categoryId</code> es <strong><code>1100004</code></strong>.</p> </li>
     <li><p>SKU <strong><code>308706</code></strong> y <code>categoryId</code> es <strong><code>1740148</code></strong>.</p> </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## Cargar titulares de imagen {#uploading-image-banners}

Si ya ha cargado las imágenes que desea utilizar, avance al siguiente paso, [Crear conjuntos de carrusel](#creating-carousel-sets). Las imágenes utilizadas en el carrusel deben cargarse una vez que Dynamic Media se haya habilitado.

Para cargar titulares de imagen, consulte [Cargar recursos](/help/assets/manage-digital-assets.md).

## Crear conjuntos de carrusel {#creating-carousel-sets}

>[!NOTE]
>
>Los usuarios no administrativos deben agregarse al **[!UICONTROL dam-users]** para poder crear o editar banners de carrusel. Si tiene problemas para crear o editar, consulte con el administrador del sistema, que puede agregarle al **[!UICONTROL dam-users]** grupo.

**Para crear conjuntos de carrusel:**

1. En Assets, vaya a la carpeta en la que desea crear el conjunto de carrusel y vaya a **[!UICONTROL Crear > Conjunto de carrusel]**.
1. En la página Editor de banners de carrusel , seleccione **[!UICONTROL Toque para abrir el Selector de recursos]** para seleccionar la imagen de la primera diapositiva.

   En la página Editor de banners de carrusel , realice una de las acciones siguientes:

   * Cerca de la esquina superior izquierda de la página, seleccione **[!UICONTROL Agregar diapositiva]** icono.

   * Cerca del centro de la página, seleccione **[!UICONTROL Toque para abrir el Selector de recursos]**.
   Seleccione para seleccionar los recursos que desea incluir en el conjunto de carrusel. Los recursos seleccionados tienen un icono de marca de verificación sobre ellos. Cuando haya terminado, seleccione , cerca de la esquina superior derecha de la página **[!UICONTROL Select]**.

   Con el Selector de recursos, puede buscar recursos escribiendo una palabra clave y seleccionando **[!UICONTROL Devuelve]**. También puede aplicar filtros para restringir los resultados de búsqueda. Puede filtrar por ruta, colección, tipo de archivo y etiqueta. Seleccione el filtro y, a continuación, el **[!UICONTROL Filtro]** en la barra de herramientas. Para cambiar la vista, seleccione el icono Ver y seleccione **[!UICONTROL Vista de columna]**, **[!UICONTROL Vista de tarjeta]** o **[!UICONTROL Vista de lista]**.

   Consulte [Trabajar con selectores](/help/assets/dynamic-media/working-with-selectors.md) para obtener más información.

1. Siga agregando diapositivas hasta que haya añadido todas las imágenes que desee rotar en el conjunto de carrusel.
1. (Opcional) Realice cualquiera de las siguientes acciones:

   * Si es necesario, arrastre las diapositivas para reordenar las imágenes en la lista de conjuntos.
   * Para eliminar una imagen, seleccione la imagen y, a continuación, seleccione **[!UICONTROL Eliminar diapositiva]** en la barra de herramientas.

   * Para aplicar un ajuste preestablecido, cerca de la esquina superior derecha de la página, seleccione la lista desplegable de ajustes preestablecidos y, a continuación, seleccione un ajuste preestablecido para aplicarlo al conjunto a la vez.
   Para eliminar una diapositiva, selecciónela. En la barra de herramientas, seleccione **[!UICONTROL Eliminar diapositiva]** en la barra de herramientas. Para mover una diapositiva, seleccione el icono de reordenación y desplácese a la ubicación deseada.

1. Después de agregar las imágenes en las diapositivas, puede agregar un punto interactivo, un mapa de imágenes o ambos a la imagen. Consulte [Agregar zonas interactivas o mapas de imágenes a un titular de imagen](#adding-hotspots-or-image-maps-to-an-image-banner).
1. Puede cambiar el diseño visual y el comportamiento de los conjuntos de carrusel. Seleccione el **[!UICONTROL Comportamiento]** y **[!UICONTROL Aspecto]** fichas si desea ajustar el aspecto del titular de carrusel o el comportamiento de componentes específicos. Consulte [Administrar ajustes preestablecidos de visor](/help/assets/dynamic-media/viewer-presets.md) para obtener más información sobre cómo utilizar el editor de visores.

   >[!NOTE]
   >
   >Para los titulares de carrusel, puede ajustar lo siguiente:
   >
   >* Duración que muestra una imagen. De forma predeterminada, cada imagen se muestra durante 9 segundos.
   >* Animación. De forma predeterminada, cada transición de diapositiva es un fundido. Puede cambiarlo a una transición de diapositiva.
   >* Estilo de los botones. Los usuarios pueden rotar por los banners seleccionando cada punto o número. Puede cambiar dónde aparecen los botones del indicador de conjunto (y si son numéricos o de un estilo punteado) y su tamaño.
   >* Cambie el estilo de resaltado de un mapa de imagen o el icono utilizado para las zonas interactivas.
   >* Antes de editar un ajuste preestablecido de visualizador, elija el estilo en el que desea basar el ajuste preestablecido. Si no elige un estilo, al comenzar a editar el ajuste preestablecido de visualizador, perderá todos los cambios si cambia a otro ajuste preestablecido.


   También puede previsualizar el aspecto del banner de carrusel. Consulte [(Opcional) Vista previa de letreros de carrusel](#optional-previewing-carousel-banners).

1. Select **[!UICONTROL Guardar]** cuando termine.

## Agregar zonas interactivas o mapas de imágenes a un titular de imagen {#adding-hotspots-or-image-maps-to-an-image-banner}

Puede agregar zonas interactivas o mapas de imágenes a un banner mediante el editor de conjuntos de carrusel.

Al agregar zonas interactivas o mapas de imágenes, puede definirlas como una visualización emergente de vista rápida, como un hipervínculo o un fragmento de experiencia.

Consulte [Fragmento de experiencia](/help/sites-cloud/authoring/fundamentals/experience-fragments.md).

>[!NOTE]
>
>Las herramientas de uso compartido de redes sociales en Carousel Banner no son compatibles cuando se incrusta el visor en un fragmento de experiencia.
>
>Para solucionar este problema, puede utilizar o crear ajustes preestablecidos de visualizador que no tengan herramientas de uso compartido en redes sociales. Estos ajustes preestablecidos de visor permiten incrustarlos correctamente en fragmentos de experiencias.

Cuando agregue zonas interactivas o mapas de imágenes a una imagen, recuerde guardar su trabajo. Las opciones Deshacer y Rehacer, cerca de la esquina superior derecha de la página, son compatibles durante la sesión de creación/edición actual.

Cuando termine de crear el banner de carrusel, puede usar la opción Vista previa para ver una representación de cómo el banner de carrusel aparece para los clientes.

Consulte [(Opcional) Vista previa de letreros de carrusel](#optional-previewing-carousel-banners).

>[!NOTE]
>
>Cuando se añaden zonas interactivas a un banner de imagen, la información del punto interactivo se almacena en la misma ubicación de metadatos, en relación con la ubicación de la imagen. Este punto es verdadero independientemente de si es una imagen interactiva o un titular de carrusel. Esta funcionalidad significa que puede reutilizar fácilmente la misma imagen (junto con sus datos de puntos interactivos definidos) en cualquier visor.
No obstante, tenga en cuenta que los carrusel Banners admiten mapas de imágenes en imágenes que también pueden contener zonas interactivas; una imagen interactiva no. Tenga en cuenta esta sugerencia si desea crear una imagen interactiva o un titular de carrusel que utilice la misma imagen. Considere la posibilidad de crear imágenes interactivas y titulares de carrusel utilizando copias independientes de la misma imagen.

>[!NOTE]
Si edita imágenes interactivas con zonas interactivas y recorta la imagen, se eliminarán las zonas interactivas.

<!-- See also [Adding Image Maps](/help/assets/image-maps.md). -->

**Para agregar zonas interactivas o mapas de imágenes a un titular de imagen:**

1. En Assets, desplácese hasta el conjunto de carrusel que desee interactuar.
1. Seleccione el conjunto de carrusel y seleccione **[!UICONTROL Editar]**. Se abre el Editor del visualizador de carrusel.
1. Seleccione la diapositiva que desee convertir en interactiva.
1. Cerca de la esquina superior izquierda de la página, seleccione **[!UICONTROL Zona interactiva]** o **[!UICONTROL Mapa de imágenes]**.
1. Realice una de las siguientes acciones:

   * Para zonas interactivas: En la imagen, seleccione una ubicación en la que desee que aparezca el punto interactivo.
   * Para mapas de imágenes: En la imagen, arrastre desde la parte superior izquierda a la parte inferior derecha para crear el área del mapa de imagen. Para ajustar el tamaño del mapa de imagen, arrastre las esquinas.

   Si es necesario, arrastre el punto interactivo o el mapa de imagen a una nueva ubicación. O bien, utilice las teclas de flecha del teclado para controlar la posición de una zona interactiva seleccionada. Agregue más zonas interactivas o mapas de imágenes según sea necesario.

   Para eliminar una zona interactiva o un mapa de imagen, seleccione la opción **[!UICONTROL Acciones]** pestaña . En el **[!UICONTROL Mapas y zonas interactivas]** del **[!UICONTROL Tipo seleccionado]** lista desplegable, seleccione el nombre del punto interactivo o del mapa de imagen que desea eliminar. Seleccione el **[!UICONTROL Papelera]** junto al menú y, a continuación, seleccione **[!UICONTROL Eliminar]**.

1. En el campo de texto Nombre , escriba el nombre del punto interactivo o del mapa de imagen. Este nombre también aparece en la sección **[!UICONTROL Mapas y puntos interactivos]** lista desplegable. Proporcionar un nombre facilita la identificación del punto interactivo o del mapa de imagen si decide cambiarlo en el futuro.
1. Realice una de las siguientes acciones en la sección **[!UICONTROL Acciones]** pestaña:

   * Select **[!UICONTROL Vista rápida]**.

      * Si es un Experience Manager Sites <!-- and Ecommerce--> cliente, seleccione el icono Selector de producto (lupa) para abrir la página Seleccionar producto . Para volver al Editor de letreros de carrusel, seleccione el producto que desee utilizar y, a continuación, seleccione la marca de verificación en la esquina superior derecha de la página.
      * Si no es un Experience Manager Sites <!-- or Ecommerce --> cliente:

         * Defina las variables. Consulte [Identificación de variables de zona interactiva](#identifying-hotspot-and-image-map-variables).
         * A continuación, introduzca manualmente el valor de SKU. En el campo de texto Valor de SKU , escriba el SKU del producto (unidad de mantenimiento de stock), que es un identificador único para cada producto o servicio distinto que ofrezca. El valor SKU introducido rellena automáticamente la parte variable de la plantilla de vista rápida. El sistema ahora sabe que asocia la zona interactiva seleccionada con la vista rápida de un SKU concreto.
         * (Opcional) Si hay otras variables dentro de la vista rápida que debe utilizar para identificar un producto, seleccione **[!UICONTROL Agregar variable genérica]**. En el campo de texto, especifique una variable adicional. Por ejemplo, category=Mens es una variable agregada.

         * Consulte [Trabajar con selectores](/help/assets/dynamic-media/working-with-selectors.md) para obtener más información.
   * Select **[!UICONTROL Hipervínculo]**.

      * Si es cliente de Experience Manager Sites, seleccione el icono Selector de sitio (carpeta) para desplazarse a una dirección URL.

         >[!NOTE]
         El método de vinculación basado en URL no es posible si el contenido interactivo tiene vínculos con direcciones URL relativas, especialmente vínculos a páginas de Experience Manager Sites.

      * Si es un cliente independiente, en el campo de texto href , especifique la ruta de URL completa a una página web vinculada.

   Asegúrese de especificar si desea abrir el vínculo en una nueva pestaña del explorador (opción predeterminada recomendada) o en la misma pestaña.

   Consulte [Trabajar con selectores](/help/assets/dynamic-media/working-with-selectors.md) para obtener más información.

   * Select **[!UICONTROL Fragmento de experiencia]**.

      * Si es cliente de Experience Manager Sites, seleccione el icono de búsqueda (lupa) para abrir la página Fragmento de experiencia . Para volver a la página de administración de puntos interactivos, seleccione el fragmento de experiencia que desee utilizar y, en la esquina superior derecha de la página, seleccione **[!UICONTROL Select]**.
Consulte [Fragmentos de experiencias](/help/sites-cloud/authoring/fundamentals/experience-fragments.md).

      * Especifique la anchura y la altura del fragmento de experiencia tal como aparece en el banner.

         >[!NOTE]
         Las herramientas de uso compartido de redes sociales en Carousel Banner no son compatibles cuando se incrusta el visor en un fragmento de experiencia.
         Para solucionar este problema, puede utilizar o crear ajustes preestablecidos de visualizador que no tengan herramientas de uso compartido en redes sociales. Estos ajustes preestablecidos de visor permiten incrustarlos correctamente en fragmentos de experiencias.
   ![experience_fragment-carouselbanner](assets/experience_fragment-carouselbanner.png)

   También puede previsualizar el aspecto del banner de carrusel. Consulte [(Opcional) Vista previa de letreros de carrusel](#optional-previewing-carousel-banners).

1. Seleccione **[!UICONTROL Guardar]**.
1. Publique el conjunto de carrusel. La publicación crea el código incrustado o la URL que puede usar en la página del sitio web. Si es cliente de Experience Manager Sites, agregue el conjunto de carrusel directamente a su página web.

   Consulte [Publicar recursos](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md).

   Consulte [Agregar un conjunto de carrusel a la página de aterrizaje del sitio web](#adding-a-carousel-banner-to-your-website-page)

## Editar conjuntos de carrusel {#editing-carousel-sets}

>[!NOTE]
Los usuarios no administrativos deben agregarse al **[!UICONTROL dam-users]** para poder crear o editar banners de carrusel. Si tiene problemas para crear o editar, consulte con el administrador del sistema, que puede agregarle al **[!UICONTROL dam-users]** grupo.

Puede realizar varias tareas de edición en conjuntos de carrusel, como las siguientes:

* Agregue diapositivas a un conjunto de carrusel. Consulte también [Trabajar con selectores](/help/assets/dynamic-media/working-with-selectors.md).
* Vuelva a ordenar las diapositivas en el conjunto de carrusel.
* Eliminar recursos del conjunto de carrusel.
* Aplique un ajuste preestablecido de visualizador.
* Eliminar el conjunto de carrusel.
* Agregue o edite zonas interactivas y mapas de imágenes. Consulte también [Trabajar con selectores](/help/assets/dynamic-media/working-with-selectors.md).

**Para editar conjuntos de carrusel:**

1. Realice una de las siguientes acciones:

   * Pase el ratón sobre un recurso de conjunto de carrusel y, a continuación, seleccione **[!UICONTROL Editar]** (icono de lápiz).
   * Pase el ratón sobre un recurso de conjunto de carrusel y seleccione **[!UICONTROL Select]** (icono de marca de verificación) y, en la barra de herramientas, seleccione **[!UICONTROL Editar]**.

   * Seleccione un recurso de conjunto de carrusel y, a continuación, en la esquina superior izquierda de la página, seleccione **[!UICONTROL Editar]** (icono de lápiz).

1. Para editar el conjunto de carrusel, realice una de las acciones siguientes:

   * Para añadir una diapositiva, seleccione **[!UICONTROL Agregar diapositiva]** icono. Vaya al recurso que desea agregar a esa diapositiva y, a continuación, seleccione la marca de verificación.
   * Para reordenar las diapositivas, arrastre una diapositiva a una nueva ubicación (seleccione el icono de reordenar para mover elementos).
   * Para añadir una zona interactiva o un mapa de imagen, seleccione los iconos de zona interactiva o mapa de imagen y consulte [Agregar zonas interactivas y mapas de imágenes a un titular de imagen](#adding-hotspots-or-image-maps-to-an-image-banner).
   * Para editar el aspecto o el comportamiento del conjunto de carrusel, seleccione la opción **[!UICONTROL Aspecto]** o **[!UICONTROL Comportamiento]** y, a continuación, defina las opciones que desee.
   * Para editar zonas interactivas o mapas de imágenes, en la diapositiva adecuada, seleccione una zona interactiva o un mapa de imágenes. En el **[!UICONTROL Acciones]** , realice los cambios.
   * Para eliminar una diapositiva, selecciónela y luego seleccione **[!UICONTROL Eliminar diapositiva]** en la barra de herramientas.
   * Para aplicar un ajuste preestablecido, cerca de la esquina superior derecha de la página, seleccione la opción **[!UICONTROL Ajuste preestablecido]** lista desplegable y, a continuación, seleccione un ajuste preestablecido de visualizador.
   * Para eliminar un conjunto de carrusel completo, vaya al conjunto de carrusel, selecciónelo y, a continuación, seleccione **[!UICONTROL Eliminar]**.

   >[!NOTE]
   Si edita imágenes interactivas con zonas interactivas y recorta la imagen, se eliminarán las zonas interactivas.

## (Opcional) Vista previa de letreros de carrusel {#optional-previewing-carousel-banners}

Puede utilizar Vista previa para ver cómo aparece el banner de carrusel para los clientes. El uso de Vista previa también permite probar las zonas interactivas y los mapas de imágenes del banner de carrusel para asegurarse de que se comportan del modo esperado.

Cuando esté satisfecho con el banner de carrusel, puede publicarlo.
Consulte [Incrustar el visualizador de imágenes o vídeos en una página web](/help/assets/dynamic-media/embed-code.md).
Consulte [Vincular URL a la aplicación web](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md). El método de vinculación basado en URL no es posible si el contenido interactivo tiene vínculos con direcciones URL relativas, especialmente vínculos a páginas de Experience Manager Sites.
Consulte [Agregar recursos de Dynamic Media a páginas](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md).

Puede obtener una vista previa de los banners de carrusel desde el Editor de carrusel (método preferido) o desde el **[!UICONTROL Visualizadores]** lista.

**Para previsualizar de forma opcional los titulares de carrusel:**

1. En **[!UICONTROL Recursos]**, vaya a un banner de carrusel existente que haya creado y seleccione para abrirlo.
1. Seleccione **[!UICONTROL Editar]**.
1. En la lista de ajustes preestablecidos de visor situada en la esquina derecha de la barra de herramientas, seleccione un visor para previsualizar el titular del carrusel.

   ![experience_fragment-carouselbanner-viewerdropdown](assets/experience_fragment-carouselbanner-viewerdropdown.png)

1. Seleccione **[!UICONTROL Vista previa]**.
1. Para probar las acciones asociadas, seleccione las zonas interactivas o los mapas de imagen de la imagen.

**Para previsualizar los banners de carrusel desde la lista Visualizadores:**

1. En **[!UICONTROL Recursos]**, vaya a un banner de carrusel existente que haya creado y seleccione para abrirlo.
1. Cerca de la esquina superior izquierda de la página Vista previa, seleccione el icono Contenido .
1. En el **[!UICONTROL Visualizadores]** en el panel de la izquierda de la página, seleccione el nombre del ajuste preestablecido de visor de banners de carrusel que desee utilizar.
1. Para probar las acciones asociadas, seleccione las zonas interactivas o los mapas de imagen de la imagen.

## Publicar titulares de carrusel {#publishing-carousel-banners}

Para utilizar el carrusel, debe publicarlo. Al publicar un conjunto de carrusel, se activa la dirección URL y el código incrustado. También publica el carrusel en la nube de Dynamic Media, que está integrada con una CDN para una entrega escalable y con rendimiento.

>[!NOTE]
Si utiliza una imagen interactiva existente con zonas interactivas para el banner de carrusel, debe publicar la imagen interactiva por separado después de publicar el banner de carrusel.
Además, si modifica una imagen interactiva publicada previamente que utiliza en un banner de carrusel, publique la imagen interactiva para que esos cambios se reflejen en el banner de carrusel.

Consulte [Publicar recursos de Dynamic Media](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md) para obtener información sobre cómo publicar banners de carrusel.

## Agregar un titular de carrusel a la página web {#adding-a-carousel-banner-to-your-website-page}

Después de cargar imágenes de banner para crear un carrusel, agregar zonas interactivas o mapas de imágenes, o ambos, al banner. Se ha publicado el conjunto de carrusel. Ya está listo para agregarlo a la página de sitio web existente.

>[!NOTE]
Si es cliente de Experience Manager Sites, puede agregar el banner de carrusel directamente a la página arrastrando el componente Medios interactivos a la página. Consulte [Agregar recursos de Dynamic Media a páginas](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md).

Sin embargo, si es cliente independiente de Experience Manager Assets, puede añadir manualmente el banner de carrusel a la página de aterrizaje de su sitio web.

1. Copie el código incrustado del conjunto de carrusel publicado.
Consulte [Incrustar el visualizador de imágenes o vídeos en una página web](/help/assets/dynamic-media/embed-code.md).

1. Agregue el código incrustado que copió de Experience Manager Assets a la página web.
El código incrustado copiado es interactivo, por lo que se ajusta automáticamente al área de incrustación de la página.

## Integración del titular de carrusel con una vista rápida existente {#integrating-the-carousel-banner-with-an-existing-quickview}

Nota: este paso solo se aplica si es cliente independiente de Experience Manager Assets.

El último paso de este proceso es la integración del titular de carrusel con una implementación de vista rápida existente en su sitio web. Cada implementación de Quick View es única y se necesita un enfoque específico que normalmente involucre la asistencia de una persona de TI de front-end.

La implementación de vista rápida existente representa normalmente una cadena de acciones interrelacionadas que se producen en la página web en el siguiente orden:

1. Un usuario déclencheur un elemento en la interfaz de usuario del sitio web.
1. El código front-end obtiene una URL de vista rápida basada en el elemento de la interfaz de usuario que se activó en el paso 1.
1. El código front-end envía una solicitud de Ajax utilizando la URL obtenida en el paso 2.
1. La lógica back-end devuelve los datos o el contenido de vista rápida correspondientes al código front-end.
1. El código front-end carga los datos o el contenido de la vista rápida.
1. De forma opcional, el código front-end convierte los datos de Quick View cargados en una representación de HTML.
1. El código front-end muestra un cuadro de diálogo modal o panel y representa el contenido del HTML en la pantalla para el usuario final.

Estas llamadas no representan llamadas de API públicas independientes a las que la lógica de página web puede llamar desde un paso arbitrario. En su lugar, se trata de una llamada encadenada en la que cada paso siguiente se oculta en la última fase (llamada de retorno) del paso anterior.

Al mismo tiempo que el titular del carrusel sustituye al paso 1 y al paso 2 parcialmente, cuando un usuario selecciona un punto interactivo o un mapa de imagen, el visor gestiona esta interacción. El visor devuelve un evento a la página web que contiene todos los datos de zona interactiva o mapa de imagen agregados anteriormente.

En un controlador de eventos de este tipo, el código front-end hace lo siguiente:

* Escucha un evento emitido por el titular de carrusel.
* Crea una URL de vista rápida basada en los datos de zona interactiva o mapa de imagen.
* Déclencheur el proceso de carga de la vista rápida desde el back-end y de renderización en la pantalla para su visualización.

El código incrustado devuelto por Experience Manager Assets ya tiene un controlador de eventos listo para usar en su lugar con comentarios.

Por lo tanto, solo es necesario descomentar el código y reemplazar el cuerpo del controlador ficticio con el código específico de la página web en particular.

El proceso de construcción de la URL de vista rápida es opuesto al proceso utilizado para identificar las variables de zona interactiva y mapa de imagen que se abarcaron anteriormente.

Consulte [Identificar las variables de zona interactiva y mapa de imagen](#identifying-hotspot-and-image-map-variables).

El último paso para almacenar en déclencheur la URL de vista rápida y activar el panel de vista rápida requiere, muy probablemente, la asistencia de una persona de TI de front-end de su departamento de TI. Tienen conocimientos para saber mejor cómo realizar déclencheur precisas de la implementación de la vista rápida desde el paso adecuado, teniendo una URL de vista rápida lista para usar.

## Crear ventanas emergentes personalizadas con Quickview {#using-quickviews-to-create-custom-pop-ups}

Consulte [Crear ventanas emergentes personalizadas con Quickview](/help/assets/dynamic-media/custom-pop-ups.md).
