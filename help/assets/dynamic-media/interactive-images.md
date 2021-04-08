---
title: Imágenes interactivas
description: Aprenda a trabajar con imágenes interactivas en Dynamic Media.
feature: Imágenes interactivas
topic: Profesional empresarial
role: Business Practitioner
exl-id: 89eef5e6-d508-4f33-b54e-24d4df49f8c3
translation-type: tm+mt
source-git-commit: 6b232ab512a6faaf075faa55c238dfb10c00b100
workflow-type: tm+mt
source-wordcount: '4249'
ht-degree: 2%

---

# Imágenes interactivas{#interactive-images}

Puede hacer que las imágenes estáticas sean ricas y atractivas para los clientes arrastrando y soltando puntos interactivos &quot;de ventas&quot; en una imagen. Los hotspots de ventas combinan información adicional sobre un producto o servicio con una capacidad directa y de punto de venta &quot;Añadir al carro&quot; o &quot;Comprar&quot;. Los clientes pueden pulsar estas zonas interactivas que se vinculan directamente al producto o servicio, agregarlas a un carro de compras o estar vinculadas a una página web. Las experiencias directas como estas aumentan la participación de los clientes y las conversiones en el sitio web.

El siguiente es un banner de ventas con una ventana emergente de vista rápida. Un usuario activa la vista rápida tocando el círculo o la &quot;zona interactiva&quot; del modelo.

![chlimage_1-152](assets/chlimage_1-368.png)

Consulte [imágenes interactivas en acción](https://marketing.adobe.com/resources/help/en_US/dm/shoppable-banner/we-fashion-QVzoom/index2-shoppable.html) en la página web que se muestra arriba.

## Vea cómo se crean los banners de imagen interactivos {#watch-how-interactive-image-banners-are-created}

Mire un tutorial de 10 minutos y 33 segundos sobre [cómo se crean los letreros de imagen interactivos](https://s7d5.scene7.com/s7viewers/html5/VideoViewer.html?videoserverurl=https://s7d5.scene7.com/is/content/&amp;emailurl=https://s7d5.scene7.com/s7/emailFriend&amp;serverUrl=https://s7d5.scene7.com/is/image/&amp;config=Scene7SharedAssets/Universal_HTML5_Video_social&amp;contenturl=https://s7d5.scene7.com/skins/&amp;asset=S7tutorials/InteractiveCarouselBanner). También aprenderá a previsualizar, editar y distribuir banners de imagen interactivos.

## Inicio rápido: Imágenes interactivas {#quick-start-interactive-images}

La siguiente descripción paso a paso del flujo de trabajo está diseñada para ayudarle a poner en marcha las imágenes interactivas con rapidez en AEM Assets.

Busque el encabezado **Example** dentro de algunas de las tareas de inicio rápido. Contiene un breve tutorial basado en un ejemplo de página web [que aún no tiene imágenes interactivas agregadas a ella](https://marketing.adobe.com/resources/help/en_US/dm/shoppable-banner/we-fashion/landing-0.html).



El tutorial ayuda a ilustrar los pasos para integrar imágenes interactivas en su propio sitio web.

Pasos de imágenes interactivas:

1. **(Opcional) Identificación de variables de puntos interactivos**. Si utiliza Adobe Experience Manager Assets y Dynamic Media de forma independiente, identifique las variables dinámicas que utiliza en la implementación de vista rápida existente. De este modo, se garantiza que puede introducir datos de puntos interactivos al crear la imagen interactiva. Consulte [(Opcional) Identificación de variables de puntos interactivos](#optional-identifying-hotspot-variables).
Sin embargo, si utiliza AEM Sites, AEM comercio electrónico o ambos, este paso no es necesario.

1. **(Opcional) Creación de un ajuste preestablecido de visualizador de imagen interactiva**. Personalice la imagen gráfica que se utiliza para representar zonas interactivas. No es necesario crear su propio ajuste preestablecido de visualizador de imagen interactiva si quiere usar el ajuste preestablecido de visualizador de imagen interactiva predeterminado, denominado `Shoppable_Banner` en su lugar.
Consulte [(Opcional) Creación de un ajuste preestablecido de visualizador de imagen interactivo](/help/assets/dynamic-media/managing-viewer-presets.md#creating-a-new-viewer-preset).

1. **Carga de un banner de imagen**. Cargue banners de imagen que desee hacer interactivos.
Consulte [Carga de un banner de imagen](#uploading-an-image-banner).

1. **Adición de zonas interactivas a un titular de imagen**. Agregue una o más zonas interactivas a un banner de imagen. Asocie cada uno de ellos a una acción como un hipervínculo, una vista rápida o un fragmento de experiencia. Después de agregar zonas interactivas, terminará esta tarea publicando la imagen interactiva.
Consulte [Adición de zonas interactivas a un titular de imagen](#adding-hotspots-to-an-image-banner).
Consulte [Vista previa de imágenes interactivas](#optional-previewing-interactive-images) - Opcional. Si lo desea, puede ver una representación del banner de ventas y probar su interactividad.
Consulte [Publicación de recursos](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md) para obtener más información sobre cómo publicar recursos de imagen interactivos.

1. **Añadir una imagen interactiva al sitio web o al sitio web en Experience Manager**. Si utiliza Sitios, Comercio electrónico o ambos, puede agregar imágenes interactivas directamente a una página web en Experience Manager. Arrastre el componente Medios interactivos a la página. Consulte [Adición de recursos de Dynamic Media a páginas](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md).
Si utiliza Experience ManagerAssets y Dynamic Media de forma independiente, copie el código incrustado en el sitio web. A continuación, inclúyalo con la vista rápida existente. Consulte [Integración de una imagen interactiva con su sitio web](#integrating-an-interactive-image-with-your-website).
Si utiliza un WCM de terceros (Web Content Manager), integre el nuevo vídeo interactivo con la vista rápida existente que se utiliza en el sitio web. Consulte [Integración de una imagen interactiva con una vista rápida](#integrating-an-interactive-image-with-an-existing-quickview) existente.

## (Opcional) Identificación de variables de puntos interactivos {#optional-identifying-hotspot-variables}

>[!NOTE]
>
>Esta tarea solo es necesaria si los siguientes son verdaderos:
>
>* Desea agregar interactividad a la imagen activando las vistas rápidas.
>* Su implementación de Experience Manager *no* utiliza un marco de integración de comercio electrónico para extraer datos de productos a Experience Manager desde cualquier solución de comercio electrónico. Estas soluciones incluyen IBM WebSphere® Commerce, Elastic Path, hybris o Intershop.

>
>
Si la implementación de AEM utiliza eCommerce, puede omitir esta tarea y continuar con la siguiente tarea.

Comience identificando las variables dinámicas que usa la implementación de vista rápida existente, de modo que pueda introducir datos de puntos interactivos para crear la imagen interactiva.

Cuando agregue zonas interactivas a una imagen de titular en Recursos de Experience Manager, asigne un SKU (unidad de mantenimiento de existencias). El SKU es un identificador único para cada producto o servicio distinto que ofrezca. Y, agregue cualquier variable opcional adicional a cada zona interactiva. Estas variables de puntos interactivos se utilizan más adelante para hacer coincidir puntos interactivos con el contenido de la vista rápida.

Es importante identificar correctamente el número y el tipo de variables que se asociarán con los datos de puntos interactivos. Cada zona interactiva agregada a una imagen de banner debe contener suficiente información para identificar el producto de forma inequívoca en el sistema back-end existente.

Existen diferentes maneras de identificar un conjunto de variables que se utilizarán para los datos de puntos interactivos.

A veces basta con consultar a los especialistas de TI responsables de la implementación de Quick View existente. Es probable que estas personas sepan cuál es el conjunto mínimo de datos necesario para identificar la vista rápida en el sistema. Sin embargo, también es posible simplemente analizar el comportamiento existente del código front-end.

La mayoría de las implementaciones de la vista rápida utilizan el siguiente paradigma:

* El usuario activa un elemento de interfaz de usuario en el sitio web. Por ejemplo, al hacer clic en el botón &quot;Vista rápida&quot;.
* El sitio web envía una solicitud de Ajax al servidor para cargar los datos o el contenido de la vista rápida, si es necesario.
* Los datos de vista rápida se traducen al contenido como preparación para su renderización en la página web.
* Por último, el código front-end procesa visualmente dicho contenido en la pantalla.

El método entonces es visitar diferentes áreas del sitio web existente donde se implementa la función de vista rápida. A continuación, déclencheur la vista rápida y capture la URL de Ajax que envía la página web para cargar los datos o el contenido de la vista rápida.

Normalmente no es necesario que utilice ninguna herramienta de depuración especializada. Los navegadores web modernos cuentan con inspectores web que realizan un trabajo adecuado. A continuación se indican algunos ejemplos de exploradores web que incluyen inspectores web:

* Para ver todas las solicitudes HTTP salientes en Google Chrome, pulse F12 para abrir el panel Herramientas para desarrolladores y, a continuación, haga clic en la pestaña Red.
En un Mac, pulse Comando+Opción+I para abrir el panel Herramientas para desarrolladores y, a continuación, haga clic en la ficha Red.

* En Firefox, puede activar el complemento Firebug pulsando F12 y utilizando su pestaña Red. O bien, puede utilizar la herramienta Inspector integrada y su pestaña Red.
En un Mac, pulse Comando+Opción+I para abrir el panel Herramientas para desarrolladores y, a continuación, haga clic en la ficha Inspector.

Cuando la supervisión de red está activada en el explorador, ponga en déclencheur la vista rápida en la página.

Ahora, busque la URL de Ajax de vista rápida en el registro de red y copie la URL grabada para su análisis futuro. Por lo general, cuando se déclencheur la vista rápida, hay numerosas solicitudes que se envían al servidor. Normalmente, la URL de Ajax de vista rápida es una de las primeras de la lista. Tiene una ruta o parte de una cadena de consulta compleja y su tipo MIME de respuesta es `text/html`, `text/xml` o `text/javascript`.

Durante este proceso, es importante visitar diferentes áreas del sitio web, con diferentes tipos y categorías de productos. El motivo es que las direcciones URL de vista rápida pueden tener partes comunes para una categoría de sitio web determinada. Sin embargo, solo cambian si se visita un área diferente del sitio web.

En el caso más simple, la única parte variable de la URL de vista rápida es el SKU del producto. En este caso, el valor SKU es la única pieza de datos que necesita para agregar zonas interactivas a la imagen del banner.

Sin embargo, en casos complejos, la URL de vista rápida tiene diferentes elementos además del SKU. Por ejemplo, los distintos elementos pueden incluir el ID de categoría, el código de color y el código de tamaño. En estos casos, cada elemento es una variable independiente en la definición de datos de puntos interactivos de la función de imagen interactiva de ventas en Recursos Experience Manager.

Veamos los siguientes ejemplos de direcciones URL de vista rápida y las variables de puntos interactivos resultantes:

<table>
  <tbody>
  <tr>
    <td><p>SKU único, que se encuentra en la cadena de consulta.</p> </td>
    <td><p>Las direcciones URL de vista rápida registradas incluyen lo siguiente:</p>
    <ul>
      <li><p><code>https://server/json?productId=866558&amp;source=100</code></p> </li>
      <li><p><code>https://server/json?productId=1196184&amp;source=100</code></p> </li>
      <li><p><code>https://server/json?productId=1081492&amp;source=100</code></p> </li>
      <li><p><code>https://server/json?productId=1898294&amp;source=100</code></p> </li>
    </ul> <p>La única parte de variable en la dirección URL es el valor del parámetro de cadena de consulta productId= y es claramente un valor SKU. Por lo tanto, las zonas interactivas solo necesitan campos SKU rellenados con valores como <strong><code>866558</code></strong>, <strong><code>1196184</code></strong>, <strong><code>1081492</code></strong>, <strong><code>1898294</code></strong>.</p> </td>
  </tr>
  <tr>
    <td><p>SKU único, que se encuentra en la ruta de URL.</p> </td>
    <td><p>Las direcciones URL de vista rápida registradas incluyen lo siguiente:</p>
    <ul>
      <li><p><code>https://server/product/6422350843</code></p> </li>
      <li><p><code>https://server/product/1607745002</code></p> </li>
      <li><p><code>https://server/product/0086724882</code></p> </li>
    </ul> <p>La parte variable se encuentra en la última parte de la ruta y se convierte en el valor SKU de las zonas interactivas: <strong><code>6422350843</code></strong>, <strong><code>1607745002</code></strong>, <strong><code>0086724882</code></strong>.</p> </td>
  </tr>
  <tr>
    <td><p>SKU e ID de categoría en la cadena de consulta.</p> </td>
    <td><p>Las direcciones URL de vista rápida registradas incluyen lo siguiente:</p>
    <ul>
      <li><p><code>https://server/quickView/product/?category=1100004&amp;prodId=305466</code></p> </li>
      <li><p><code>https://server/quickView/product/?category=1100004&amp;prodId=310181</code></p> </li>
      <li><p><code>https://server/quickView/product/?category=1740148&amp;prodId=308706</code></p> </li>
    </ul> <p>En este caso, hay dos partes diferentes en la dirección URL. El SKU se almacena en el parámetro <code>prodId</code> y el ID de categoría<code></code> se almacena en el parámetro <code>category=</code>.</p> <p>Como tal, las definiciones de puntos interactivos son pares. Es decir, un valor de SKU y una variable adicional llamada <code>categoryId</code>. Los pares resultantes son los siguientes:</p>
    <ul>
      <li><p>El SKU es <strong><code>305466</code></strong> y <code>categoryId</code> es <code>1100004</code>.</p> </li>
      <li><p>El SKU es <strong><code>310181</code></strong> y <code>categoryId</code> es <strong><code>1100004</code></strong>.</p> </li>
      <li><p>El SKU es <strong><code>308706</code></strong> y <code>categoryId</code> es <strong><code>1740148</code></strong>.</p> </li>
    </ul> <p> </p> </td>
  </tr>
  </tbody>
</table>

**Ejemplo**

Puede aplicar el mismo enfoque utilizado en los tres ejemplos anteriores a la [página web de demostración](https://marketing.adobe.com/resources/help/en_US/dm/shoppable-banner/we-fashion/landing-0.html).

La página web de demostración tiene varias miniaturas de producto, cada una con un botón de vista rápida etiquetado como &quot;Ver más&quot;. Con la herramienta de depuración del explorador web aún activada, haga clic en cada botón y anote las direcciones URL de vista rápida registradas. Después de activar las cuatro vistas rápidas del producto disponibles en la página, tiene la siguiente lista de solicitudes de vista rápida realizadas en el servidor:

* `/datafeed/Men-Windbreaker.json`
* `/datafeed/Men-SimpleHenley.json`
* `/datafeed/Men-CamoPullover.json`
* `/datafeed/Women-QuiltedDownJacket.json`

Al examinar las llamadas al servidor, puede ver que la información específica del producto solo está presente en la ruta de solicitud. También observa que la cadena de consulta no se utiliza en absoluto y que hay dos tipos distintos de fragmentos de datos involucrados:

* El primer tipo es Hombres o Mujeres. Puede llamar a esta &quot;categoría de producto&quot;.
* El segundo tipo es el nombre del producto, como CamoPullover, que probablemente es el SKU del producto.

Dada esta información, toda la URL de vista rápida tiene el siguiente patrón:

`/datafeed/$categoryId$-$SKU$.json`

En función de este análisis, utilizaría `categoryId` y `SKU` para las zonas interactivas.

Ya está listo para cargar un titular de imagen y agregarle zonas interactivas mediante la función de imagen interactiva de ventas de AEM Assets.

## (Opcional) Creación de un ajuste preestablecido de visualizador de imagen interactivo {#optional-creating-an-interactive-image-viewer-preset}

Puede elegir utilizar el ajuste preestablecido predeterminado y listo para usar del visualizador de imágenes interactivo llamado `Shoppable_Banner` que viene con AEM Assets. O puede crear su propio ajuste preestablecido de visualizador personalizado para utilizarlo con imágenes interactivas.

Al crear un ajuste preestablecido personalizado del visualizador de imagen interactiva, puede determinar el aspecto de las zonas interactivas en el banner de imagen. Como parte de la creación del ajuste preestablecido de visualizador, puede elegir utilizar un gráfico de zona interactiva de una galería de imágenes predefinidas.

Después de guardar el ajuste preestablecido de visualizador, se activa automáticamente (se activa) en la página de lista Ajustes preestablecidos de visualizador de AEM Assets. Esta funcionalidad significa que está visible en el componente de Medios interactivos y siempre que se vea un recurso. Sin embargo, para *entregar* un banner interactivo con este ajuste preestablecido de visualizador, *publique* también el ajuste preestablecido de visualizador. Esta regla es verdadera para los ajustes preestablecidos de visor personalizados o predeterminados.

**Para crear un ajuste preestablecido de visualizador de imagen interactivo**

1. En el carril izquierdo, pulse **[!UICONTROL Herramientas > Assets > Ajustes preestablecidos de visor]**.
1. Cerca de la esquina superior derecha de la página, pulse **[!UICONTROL Crear]**.
1. En el cuadro de diálogo Nuevo ajuste preestablecido de visualizador, escriba un nombre para describir el ajuste preestablecido de visualizador de banners interactivo.

   Este título aparece en la página de lista Ajustes preestablecidos de visor después de guardarlo.

1. En el menú desplegable Tipo de medio enriquecido, seleccione **[!UICONTROL Imagen interactiva]**.
1. Toque **[!UICONTROL Crear]**.
1. En la página Editar ajuste preestablecido de visualizador , pulse la pestaña **[!UICONTROL Aspecto]**.
1. Realice una de las acciones siguientes:

   * Para cargar su propia imagen de zona interactiva que desee utilizar en imágenes, pulse el icono Selector de recursos . En la página Seleccionar contenido , vaya a la imagen de zona interactiva que desee utilizar y selecciónela. Pulse el icono de la marca de verificación en la esquina superior derecha.
   * Para seleccionar una imagen de zona interactiva predefinida, pulse el icono Galería de puntos interactivos . En la paleta Galería de puntos interactivos, pulse la imagen de zona interactiva que desee utilizar.

1. Cerca de la esquina superior derecha de la página, pulse **[!UICONTROL Guardar]**.

   Asegúrese de publicar el nuevo ajuste preestablecido de visor.

   Consulte [Ajustes preestablecidos del visualizador de publicaciones](/help/assets/dynamic-media/managing-viewer-presets.md#publishing-viewer-presets).

   Ya está listo para cargar un titular de imagen.

## Carga de un titular de imagen {#uploading-an-image-banner}

Si ya ha cargado las imágenes que desea usar, avance al siguiente paso, [Añadir zonas interactivas a un titular de imagen](#adding-hotspots-to-an-image-banner).

**Para cargar un titular de imagen**

1. Cargue banners de imagen que desee hacer interactivos.

   Consulte [Carga de recursos](/help/assets/manage-digital-assets.md#uploading-assets).

   Ya está listo para agregar zonas interactivas al titular de la imagen; consulte la siguiente tarea a continuación.

## Adición de zonas interactivas a un titular de imagen {#adding-hotspots-to-an-image-banner}

Puede agregar zonas interactivas a un banner de imagen mediante el editor de la página Administración de puntos interactivos .

Al agregar zonas interactivas, puede definirlas como una visualización emergente de vista rápida, como un hipervínculo o un fragmento de experiencia.

Consulte [Fragmentos de experiencias](/help/sites-cloud/authoring/fundamentals/experience-fragments.md).

>[!NOTE]
>
>Las herramientas de uso compartido de medios sociales en Imagen interactiva no son compatibles cuando se incrusta el visor en un fragmento de experiencia. En su lugar, utilice o cree ajustes preestablecidos de visualizador que no tengan herramientas de uso compartido de medios sociales. Estos ajustes preestablecidos de visor permiten incrustarlos correctamente en fragmentos de experiencias.

Las opciones Deshacer y Rehacer, cerca de la esquina superior derecha de la página, son compatibles durante la sesión de creación/edición actual.

Cuando termine de crear la imagen interactiva, puede utilizar Vista previa para ver una representación de cómo la imagen interactiva aparece para los clientes.

Consulte [(Opcional) Vista previa de imágenes interactivas](#optional-previewing-interactive-images).

>[!NOTE]
>
>Cuando se añaden zonas interactivas a una imagen en una imagen interactiva o un titular de carrusel, la información del punto interactivo se almacena en la misma ubicación de metadatos. Esta ubicación es relativa a la ubicación de la imagen, independientemente de si es una imagen interactiva o un titular de carrusel. Esta funcionalidad significa que puede reutilizar fácilmente la misma imagen (junto con sus datos de puntos interactivos definidos) en cualquier visor.
No obstante, tenga en cuenta que los carrusel Banners admiten mapas de imágenes en imágenes que también pueden contener zonas interactivas; una imagen interactiva no. Tenga esto en cuenta si desea crear una imagen interactiva o un titular de carrusel que utilice la misma imagen. En su lugar, puede crear imágenes interactivas y titulares de carrusel utilizando copias independientes de la misma imagen.
Consulte también [Banners de carrusel](/help/assets/dynamic-media/carousel-banners.md).

>[!NOTE]
Si edita imágenes interactivas con zonas interactivas y recorta la imagen, se eliminarán las zonas interactivas.

**Para agregar zonas interactivas a un titular de imagen**

1. En la vista Recursos, desplácese hasta el banner de imagen que desee convertir en interactivo.
1. Realice una de las acciones siguientes:

   * Pase el ratón sobre la imagen y, a continuación, pulse **[!UICONTROL Seleccionar]** (icono de marca de verificación). En la barra de herramientas, pulse **[!UICONTROL Editar]**.

   * Pase el ratón sobre la imagen y, a continuación, pulse **[!UICONTROL Más acciones]** (icono de tres puntos) **[!UICONTROL Editar]**.

   * Para abrirlo en la página Vista de detalles , pulse la imagen. En la barra de herramientas, pulse **[!UICONTROL Editar]**.

1. Cerca de la esquina superior izquierda de la página, pulse **[!UICONTROL Agregar zona interactiva]** (icono con el dedo) para abrir la página de administración de puntos interactivos.
1. Cerca de la esquina superior izquierda de la página, pulse **[!UICONTROL Zona interactiva]**.

   1. Cerca de la esquina superior izquierda de la página Administración de puntos interactivos, pulse **[!UICONTROL Zona interactiva]**.
   1.  En la imagen, pulse una ubicación en la que desee que aparezca el punto interactivo. Si es necesario, arrastre la zona interactiva para ajustar su ubicación. O bien, utilice las teclas de flecha del teclado para controlar la posición de un punto interactivo seleccionado.
   1. Agregue más zonas interactivas según sea necesario repitiendo los pasos a y b.
   1. (Opcional) Para eliminar una zona interactiva, selecciónela en la imagen y, a continuación, pulse **[!UICONTROL Eliminar]** (icono de papelera) en el encabezado **[!UICONTROL Zonas interactivas]**.

1. En el campo de texto Nombre , escriba el nombre de la zona interactiva. Este nombre también aparece en la lista desplegable Zona interactiva seleccionada .
1. Realice una de las acciones siguientes:

   * Pulse **[!UICONTROL Vista rápida]**.

      * Si es cliente de AEM Sites o de comercio electrónico, toque o haga clic en el icono Selector de productos (lupa) para abrir la página Seleccionar producto . Pulse el producto que desee utilizar y, a continuación, pulse **Seleccionar** en la esquina superior derecha de la página. Volverá a la página de administración de puntos interactivos.
      * Si es *no* cliente de Sites Experience Manager o comercio electrónico

         * Consulte [Identificación de variables de puntos interactivos](#optional-identifying-hotspot-variables); debe definir estas variables.
         * A continuación, introduzca manualmente el valor de SKU. En el campo de texto Valor de SKU , escriba el SKU del producto. El valor SKU introducido rellena automáticamente la parte variable de la plantilla de vista rápida. Garantiza que el sistema sepa asociar la zona interactiva utilizada con la vista rápida de un SKU concreto.
         * (Opcional) Si hay otras variables dentro de la vista rápida que se utilizan para identificar un producto, pulse **[!UICONTROL Agregar variable genérica]**. En el campo de texto, especifique una variable adicional. Por ejemplo, `category=Mens` es una variable agregada.
   * Toque **[!UICONTROL Hipervínculo]**.

      * Si es cliente de Sites de Experience Manager, pulse el icono Selector de sitio (carpeta). Vaya a una dirección URL. El método de vinculación basado en URL no es posible si el contenido interactivo tiene vínculos con direcciones URL relativas, especialmente vínculos a páginas de sitios Experience Manager.
      * Si es cliente independiente, en el campo de texto HREF especifique la ruta de URL completa a una página web vinculada.

   Asegúrese de especificar si desea abrir el vínculo en una nueva pestaña del explorador (opción predeterminada recomendada) o en la misma pestaña.

   Consulte [Uso de selectores](/help/assets/dynamic-media/working-with-selectors.md) para obtener más información.

   * Pulse **[!UICONTROL Fragmento de experiencias]**.

      * Si es cliente de AEM Sites, toque o haga clic en el icono de búsqueda (lupa) para abrir la página Fragmento de experiencia . Puntee en el fragmento de experiencia que desee utilizar. A continuación, pulse **[!UICONTROL Seleccionar]** en la esquina superior derecha de la página. Volverá a la página de administración de puntos interactivos.
Consulte [Fragmentos de experiencias](/help/sites-cloud/authoring/fundamentals/experience-fragments.md).

      * Especifique la anchura y la altura del fragmento de experiencia tal como desea que aparezca en el banner.

         >[!NOTE]
         Las herramientas de uso compartido de medios sociales en Imagen interactiva no son compatibles cuando se incrusta el visor en un fragmento de experiencia. En su lugar, utilice o cree ajustes preestablecidos de visualizador que no tengan herramientas de uso compartido de medios sociales. Estos ajustes preestablecidos de visor permiten incrustarlos correctamente en fragmentos de experiencias.



1. Toque **[!UICONTROL Guardar]** para guardar el trabajo y volver a la página Examinar.
1. Publique la imagen interactiva. La publicación entrega el banner a través de la nube y también genera código incrustado que le permite integrarse con un sitio web de terceros.

   Consulte [Publicación de recursos](/help/assets/manage-digital-assets.md#publish-assets).

   Después de agregar zonas interactivas y publicar la imagen interactiva, ya está listo para agregarla al sitio web existente.

   Consulte [Integración de una imagen interactiva con su sitio web](#integrating-an-interactive-image-with-your-website).

   >[!NOTE]
   Si edita imágenes interactivas con zonas interactivas y recorta la imagen, se eliminarán las zonas interactivas.

### (Opcional) Vista previa de imágenes interactivas {#optional-previewing-interactive-images}

Puede utilizar Vista previa para ver una representación del aspecto que tendrá la imagen interactiva para los clientes. La vista previa también permite probar las zonas interactivas de la imagen para asegurarse de que se comportan del modo esperado.

Cuando esté satisfecho con la imagen interactiva, puede publicarla.
Consulte [Incrustación del visualizador de imágenes o vídeos en una página web](/help/assets/dynamic-media/embed-code.md).
Consulte [Vinculación de URL a la aplicación web](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md). El método de vinculación basado en URL no es posible si el contenido interactivo tiene vínculos con direcciones URL relativas, especialmente vínculos a páginas de AEM Sites.
Consulte [Adición de recursos de Dynamic Media a páginas](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md).

**Para previsualizar imágenes interactivas**

1. En la vista Recursos, desplácese a la imagen interactiva existente que haya creado y pulse para abrirla en Vista previa.
1. Cerca de la esquina superior izquierda de la página Vista previa, en la lista desplegable Contenido, pulse **[!UICONTROL Visualizadores]**.
1. En la lista Visualizadores, pulse **[!UICONTROL Shoppable_Banner]** o el nombre del ajuste preestablecido del visualizador de imágenes interactivo que ha creado.
1. Para probar las acciones asociadas de las zonas interactivas, pulse las zonas interactivas de la imagen.

## Publicación de recursos de imagen interactivos {#publishing-interactive-image-assets}

Consulte [Publicación de recursos](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md) para obtener más información sobre cómo publicar recursos de imagen interactivos.

## Integración de una imagen interactiva con su sitio web {#integrating-an-interactive-image-with-your-website}

Después de cargar una imagen de banner, agregar zonas interactivas a ella y publicar la imagen interactiva, está listo para agregarla a la página del sitio web.

Si es cliente de AEM Sites, puede agregar la imagen interactiva arrastrando el componente de Medios interactivos a su página. Consulte [Adición de recursos de Dynamic Media a páginas](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md).

Si es cliente independiente de AEM Assets, puede agregar manualmente la imagen interactiva a su sitio web como se describe en esta sección.

1. Copie el código incrustado de la imagen interactiva publicada.
Consulte [Incrustación del visualizador de imágenes o vídeos en una página web](/help/assets/dynamic-media/embed-code.md).

1. Agregue el código incrustado copiado en la ubicación deseada dentro de la página web.
El código incrustado copiado está configurado para un entorno interactivo, de modo que se ajusta automáticamente al área asignada.

**Ejemplo**

Con el sitio web de la [demostración como ejemplo](https://marketing.adobe.com/resources/help/en_US/dm/shoppable-banner/we-fashion/landing-0.html), observe que la imagen de las tres personas es una etiqueta estática `IMG`:

```xml
<img class="img-responsive" width="100%" title="Hero Image 2" alt="Hero Image 2" src="images/shoppable-banner.jpg">
```

La integración es tan sencilla como eliminar la etiqueta `IMG` y sustituirla por el código incrustado copiado de AEM Assets. Puede ver que el resultado [muestra la imagen interactiva de ventas en la página con tres puntos interactivos de círculo](https://marketing.adobe.com/resources/help/en_US/dm/shoppable-banner/we-fashion/landing-1.html).

>[!NOTE]
En este punto, las zonas interactivas de la imagen interactiva de ventas del sitio web de demostración solo tienen fines de visualización. Todavía no están integrados con las vistas rápidas existentes.

Para aplicar un &quot;recorte&quot; a una imagen interactiva de ventas para un entorno interactivo, incluya el atributo de configuración de imagen interactiva `ZoomView.iscommand` a la ruta. En este caso, se llama al componente `ZoomView` y `iscommand` es el comando de servidor de imágenes &quot;recortar&quot; que se aplica.

Consulte el atributo de configuración [ZoomView.iscommand](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-images/command-reference-configuration-attributes-interactive-images/r-html5-aem-interactive-image-config-attrib-zoomview-iscommand.html).

Consulte el comando [recortar](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-crop.html) servidor de imágenes.

Ya está listo para integrar la imagen interactiva con una vista rápida existente en su sitio web.

## Integración de una imagen interactiva con una vista rápida existente {#integrating-an-interactive-image-with-an-existing-quickview}

>[!NOTE]
Esta tarea solo se aplica si es cliente independiente de AEM Assets.

El último paso de este proceso es integrar la imagen interactiva con una implementación de vista rápida existente en el sitio web. No existe una solución para la integración que funcione en todos los casos. Cada implementación de vista rápida es única y se necesita un enfoque específico. Como tal, la participación de una persona de TI de front-end es útil.

La implementación de vista rápida existente representa normalmente una cadena de acciones interrelacionadas que se producen en la página web en el siguiente orden:

1. Un usuario déclencheur un elemento en la interfaz de usuario del sitio web.
1. El código front-end obtiene una URL de vista rápida basada en el elemento de la interfaz de usuario que se activó en el paso 1.
1. El código front-end envía una solicitud de Ajax utilizando la URL obtenida en el paso 2.
1. La lógica back-end devuelve los datos o el contenido de vista rápida correspondientes al código front-end.
1. El código front-end carga los datos o el contenido de la vista rápida.
1. De forma opcional, el código front-end convierte los datos de Quick View cargados en una representación HTML.
1. El código front-end muestra un cuadro de diálogo modal o panel y representa el contenido HTML en la pantalla para el usuario final.

Estas llamadas no representan necesariamente llamadas de API públicas independientes a las que la lógica de página web llama desde un paso arbitrario. En su lugar, se trata de una llamada encadenada en la que cada paso siguiente se oculta en la última fase (llamada de retorno) del paso anterior.

Cuando la imagen interactiva de la tabla de ventas sustituye al paso 1 y, en parte, al paso 2, un usuario toca una zona interactiva dentro de la imagen de la tabla de compras. El visor gestiona esta interacción de usuario. El visor devuelve un evento a la página web que contiene todos los datos de zona interactiva añadidos anteriormente a AEM Assets.

En un controlador de eventos de este tipo, el código front-end hace lo siguiente:

* Escucha un evento emitido por la imagen interactiva de ventas.
* Crea una URL de vista rápida basada en los datos de zona interactiva.
* Déclencheur el proceso de carga de la vista rápida desde el servidor y de renderización en la pantalla para su visualización.

El código incrustado devuelto por Recursos de Experience Manager tiene un controlador de eventos listo para usar que se comenta, como se ve en el siguiente fragmento de código resaltado:

```xml
        var s7interactiveimageviewer = new s7viewers.InteractiveImage({
            "containerId" : "s7interactiveimage_div",
            "params" : {
                "serverurl" : "https://aodmarketingna.assetsadobe.com/is/image",
                "contenturl" : "https://aodmarketingna.assetsadobe.com/",
                "config" : "/etc/dam/presets/viewer/Shoppable_Media",
                "asset" : "/content/dam/mac/aodmarketingna/shoppable-banner/shoppable-banner.jpg" }
        })
        /* // Example of interactive image event for Quickview.
             s7interactiveimageviewer.setHandlers({
                "quickViewActivate": function(inData) {
                    var sku=inData.sku; //SKU for product ID
                    //To pass other parameter from the hotspot, you will need to add custom parameter during the hotspot setup as parameterName=value
                    loadQuickView(sku); //Replace this call with your Quickview plugin
                    //Please refer to your Quickviewer plugin for the Quickview call
                 },
             });
        */
        s7interactiveimageviewer.init();
```

Por lo tanto, solo es necesario descomentar el código y reemplazar el cuerpo del controlador ficticio con el código específico de la página web en particular.

El proceso de construcción de la URL de vista rápida es opuesto al proceso utilizado para identificar las variables de puntos interactivos que se abarcaron anteriormente.

Consulte [Identificación de variables de puntos interactivos](#optional-identifying-hotspot-variables).

En los ejemplos anteriores de URL de vista rápida se puede ver en los ejemplos siguientes cómo se construye la URL de vista rápida en cada caso:

<table>
 <tbody>
  <tr>
   <td><p>SKU único, que se encuentra en la cadena de consulta</p> </td>
   <td><code class="code">s7interactiveimageviewer.setHandlers({
      "quickViewActivate": function(inData) {
      var quickViewUrl = "https://server/json?productId=" + inData.sku + "&amp;amp;source=100";
      },
      });</code></td>
  </tr>
  <tr>
   <td><p>SKU único, que se encuentra en la ruta de URL</p> </td>
   <td><code class="code">s7interactiveimageviewer.setHandlers({
      "quickViewActivate": function(inData) {
      var quickViewUrl = "https://server/product/" + inData.sku;
      },
      });</code></td>
  </tr>
  <tr>
   <td><p>SKU e ID de categoría en la cadena de consulta</p> </td>
   <td><code class="code">s7interactiveimageviewer.setHandlers({
      "quickViewActivate": function(inData) {
      var quickViewUrl = "https://server/quickView/product/?category=" + inData.categoryId + "&amp;amp;prodId=" + inData.sku;
      },
      });</code></td>
  </tr>
 </tbody>
</table>

El último paso para almacenar en déclencheur la URL de vista rápida y activar el panel de vista rápida requiere la asistencia de una persona de TI de front-end de su empresa. Tienen conocimientos para saber mejor cómo realizar déclencheur precisas de la implementación de la vista rápida desde el paso adecuado, teniendo una URL de vista rápida lista para usar.

Puede ver cómo se aplican estos pasos al sitio web de demostración para integrar completamente una imagen interactiva de ventas con el código de vista rápida. Anteriormente, la estructura de la URL de vista rápida se identificaba como la siguiente:

```xml
/datafeed/$categoryId$-$SKU$.json
```

Para reconstruir esta dirección URL dentro del controlador `quickViewActivate` , puede utilizar los campos `categoryId` y `SKU` . Estos campos están disponibles en el objeto `inData` que el código del visor pasa al controlador:

```xml
var sku=inData.sku;
var categoryId=inData.categoryId;
var quickViewUrl = "datafeed/" + categoryId + "-" + sku + ".json";
```

El sitio web de demostración activa el cuadro de diálogo Vista rápida utilizando una simple llamada de función `loadQuickView()`. Esta función toma solo un argumento, que es la URL de datos de vista rápida. Como tal, el último paso para integrar la imagen interactiva de ventas es agregar la siguiente línea de código al controlador `quickViewActivate`:

```xml
loadQuickView(quickViewUrl);
```

El siguiente es el código fuente completo:

```xml
 var s7interactiveimageviewer = new s7viewers.InteractiveImage({
  "containerId" : "s7interactiveimage_div",
  "params" : {
   "serverurl" : "https://aodmarketingna.assetsadobe.com/is/image",
   "contenturl" : "https://aodmarketingna.assetsadobe.com/",
   "config" : "/etc/dam/presets/viewer/Shoppable_Media",
   "asset" : "/content/dam/mac/aodmarketingna/shoppable-banner/shoppable-banner.jpg" }
 })
   s7interactiveimageviewer.setHandlers({
   "quickViewActivate": function(inData) {
     var sku=inData.sku;
     var categoryId=inData.categoryId;
    var quickViewUrl = "datafeed/" + categoryId + "-" + sku + ".json";
    loadQuickView(quickViewUrl);
    },
   });
 s7interactiveimageviewer.init();
```

El sitio web de la [demostración final con la imagen interactiva completamente integrada](https://marketing.adobe.com/resources/help/en_US/dm/shoppable-banner/we-fashion/landing-3.html).

## Uso de vistas rápidas para crear ventanas emergentes personalizadas {#using-quickviews-to-create-custom-pop-ups}

Consulte [Uso de las vistas rápidas para crear ventanas emergentes personalizadas](/help/assets/dynamic-media/custom-pop-ups.md).
