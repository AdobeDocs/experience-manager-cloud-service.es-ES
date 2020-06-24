---
title: Uso de las vistas rápidas para crear ventanas emergentes personalizadas
description: La vista rápida predeterminada se utiliza en las experiencias de comercio electrónico, por lo que se muestra una ventana emergente con información del producto para dirigir una compra. Puede activar el contenido personalizado para que se muestre en las ventanas emergentes.
translation-type: tm+mt
source-git-commit: 1713cddf713afc24103a841a7dbae923941f6322
workflow-type: tm+mt
source-wordcount: '1023'
ht-degree: 2%

---


# Uso de las vistas rápidas para crear ventanas emergentes personalizadas {#using-quickviews-to-create-custom-pop-ups}

La vista rápida predeterminada se utiliza en las experiencias de comercio electrónico, por lo que se muestra una ventana emergente con información del producto para dirigir una compra. Sin embargo, puede activar el contenido personalizado para que se muestre en las ventanas emergentes. Según el visor que utilice, esta funcionalidad permite a los usuarios hacer clic en un punto interactivo, una imagen en miniatura o en un mapa de imágenes para ver información o contenido relacionado.

Los siguientes visores de Dynamic Media admiten las vistas rápidas:

* Imágenes interactivas (zonas interactivas en las que se puede hacer clic)
* Vídeo interactivo (imágenes en miniatura en las que se puede hacer clic durante la reproducción de vídeo)
* Pancartas de carrusel (zonas interactivas o mapas de imágenes en las que se puede hacer clic)

Aunque la funcionalidad de cada visor es diferente, el proceso de creación de una vista rápida es el mismo en los tres visores admitidos.

**Para utilizar las vistas rápidas para crear ventanas emergentes personalizadas**

1. Cree una vista rápida para un recurso cargado.

   Normalmente, se crea una vista rápida al mismo tiempo que se edita un recurso para utilizarlo con el visor que se utiliza.

   <table>
    <tbody>
    <tr>
    <td><strong>Visor que está utilizando</strong></td>
    <td><strong>Complete estos pasos para crear la vista rápida</strong></td>
    </tr>
    <tr>
    <td>Imágenes interactivas</td>
    <td><a href="/help/assets/dynamic-media/interactive-images.md#adding-hotspots-to-an-image-banner" target="_blank">Añadir zonas interactivas en una pancarta</a>de imagen.</td>
    </tr>
    <tr>
    <td>Vídeos interactivos</td>
    <td><a href="/help/assets/dynamic-media/interactive-videos.md#adding-interactivity-to-your-video" target="_blank">Añadir la interactividad en el vídeo</a>.</td>
    </tr>
    <tr>
    <td>Banner de carrusel</td>
    <td><a href="/help/assets/dynamic-media/carousel-banners.md#adding-hotspots-or-image-maps-to-an-image-banner" target="_blank">Añadir puntos interactivos o mapas de imagen en un letrero</a>.<br /> </td>
    </tr>
    </tbody>
   </table>

1. Obtenga el código incrustado del visor para integrar el visor en el sitio web.

   <table>
    <tbody>
    <tr>
    <td><strong>Visor que está utilizando</strong><br /> </td>
    <td><strong>Complete estos pasos para integrar el visor con el sitio web</strong></td>
    </tr>
    <tr>
    <td>Imagen interactiva</td>
    <td><a href="/help/assets/dynamic-media/interactive-images.md#integrating-an-interactive-image-with-your-website" target="_blank">Integración de una imagen interactiva con el sitio web</a>.<br /> </td>
    </tr>
    <tr>
    <td>Vídeo interactivo<br /> </td>
    <td><a href="/help/assets/dynamic-media/interactive-videos.md#integrating-an-interactive-video-with-your-website" target="_blank">Integración de un vídeo interactivo con el sitio web</a>.<br /> </td>
    </tr>
    <tr>
    <td>Pancarta de carrusel</td>
    <td><a href="/help/assets/dynamic-media/carousel-banners.md#adding-a-carousel-banner-to-your-website-page" target="_blank">Añadir una pancarta de carrusel a la página</a>del sitio web.<br /> </td>
    </tr>
    </tbody>
   </table>

1. El visor que está utilizando ahora necesita saber cómo utilizar la vista rápida.

   Para ello, el visor utiliza un controlador denominado `QuickViewActive`.

   **Ejemplo** Supongamos que estaba utilizando el siguiente código incrustado de muestra en la página web para una imagen interactiva:

   ![chlimage_1-291](assets/chlimage_1-291.png)

   El controlador se carga en el visor mediante `setHandlers`:

   `*viewerInstance*.setHandlers({ *handler 1*, *handler 2*}, ...`

   **Utilizando el ejemplo de código incrustado de ejemplo de arriba, tenemos el siguiente código:**

   ```xml
   s7interactiveimageviewer.setHandlers({
       quickViewActivate": function(inData) {
           var sku=inData.sku;
           var genericVariable1=inData.genericVariable1;
           var genericVariable2=inData.genericVariable2;
          loadQuickView(sku,genericVariable1,genericVariable2);
       }
   })
   ```

   Obtenga más información sobre `setHandlers()` los métodos siguientes:

   * Visor de imágenes interactivo: [sethandlers](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-images/jsapi-interactive-image/r-html5-aem-int-image-viewer-javascriptapiref-sethandlers.html)
   * Visor de vídeo interactivo: [sethandlers](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-video/jsapi-interactive-video/r-html5-aem-int-video-javascriptapiref-sethandlers.html)

1. Ahora debe configurar el `quickViewActivate` controlador.

   El `quickViewActivate` controlador controla las vistas rápidas en el visor. El controlador contiene la lista de variable y las llamadas de función que se utilizarán con la vista rápida. El código incrustado proporciona una asignación para la variable de SKU establecida en la vista rápida, así como una llamada a `loadQuickView` la función de muestra.

   **Asignación** de variables Asigne variables para su uso en la página web al valor de SKU y a las variables genéricas incluidas en la vista rápida:

   `var *variable1*= inData.*quickviewVariable*`

   El código incrustado proporcionado tiene una asignación de muestra para la variable SKU:

   `var sku=inData.sku`

   Asigne variables adicionales desde la vista rápida también, como se muestra a continuación:

   ```
   var <i>variable2</i>= inData.<i>quickviewVariable2</i>
    var <i>variable3</i>= inData.<i>quickviewVariable3</i>
   ```

   **Llamada** a función El controlador también requiere una llamada a la función para que funcione la vista rápida. Se da por hecho que la página host tiene acceso a la función. El código incrustado proporciona una llamada de función de muestra:

   `loadQuickView(sku)`

   La llamada a la función de ejemplo supone que la función `loadQuickView()` existe y es accesible.

   Obtenga más información sobre `quickViewActivate` los métodos siguientes:

   * Visor de imágenes interactivo: rellamadas de [Evento](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-images/c-html5-aem-interactive-image-event-callbacks.html)
   * Visor de vídeo interactivo: rellamadas de [Evento](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-video/c-html5-aem-int-video-event-callbacks.html)
   * Compatibilidad con datos interactivos en el visor de vídeo interactivo: compatibilidad con datos [interactivos](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-video/c-html5-aem-int-video-int-data-support.html)

1. Haga lo siguiente:

   * Quite los comentarios de la sección setHandlers del código incrustado.
   * Asigne cualquier variable adicional contenida en la vista rápida.

      * Actualice la `loadQuickView(sku,*var1*,*var2*)` llamada si va a agregar variables adicionales.
   * Cree una función simple `loadQuickView` () en la página, fuera del visor.

      Por ejemplo, lo siguiente escribe el valor de sku en la consola del explorador:

   ```xml
   function loadQuickView(sku){
       console.log ("quickview sku value is " + sku);
   }
   ```

   * Cargue una página HTML de prueba en un servidor web y ábrala.

      Con las variables de la vista rápida asignadas y la llamada a la función establecida, la consola del explorador escribe el valor de la variable en la consola del explorador mediante la función de ejemplo proporcionada.



1. Ahora puede utilizar una función para abrir una ventana emergente sencilla en la vista rápida. El siguiente ejemplo utiliza un `DIV` para una ventana emergente.
1. Ajuste el estilo de la ventana emergente `DIV` de la siguiente manera. Añada su propio estilo adicional como desee.

   ```xml
   <style type="text/css">
       #quickview_div{
           position: absolute;
           z-index: 99999999;
           display: none;
       }
   </style>
   ```

1. Coloque la ventana emergente `DIV` en el cuerpo de la página HTML.

   Uno de los elementos se establece con un ID que se actualiza con un valor de sku cuando el usuario invoca una vista rápida. El ejemplo también incluye un botón sencillo para volver a ocultar la ventana emergente después de que esté visible.

   ```xml
   <div id="quickview_div" >
       <table>
           <tr><td><input id="btnClosePopup" type="button" value="Close"        onclick='document.getElementById("quickview_div").style.display="none"' /><br /></td></tr>
           <tr><td>SKU</td><td><input type="text" id="txtSku" name="txtSku"></td></tr>
       </table>
   </div>
   ```

1. Añada una función para actualizar el valor de sku en la ventana emergente; haga visible la ventana emergente reemplazando la función simple creada en el paso 5. con lo siguiente:

   ```xml
   <script type="text/javascript">
       function loadQuickView(sku){
           document.getElementById("txtSku").setAttribute("value",sku); // write sku value
           document.getElementById("quickview_div").style.display="block"; // show popup
       }
   </script>
   ```

1. Cargue una página HTML de prueba en el servidor web y ábrala. El visor muestra la ventana emergente `DIV` cuando un usuario invoca una vista rápida.
1. **Cómo mostrar la ventana emergente personalizada en modo de pantalla completa**

   Algunos visores, como el visor de vídeo interactivo, admiten la visualización en modo de pantalla completa. Sin embargo, el uso de la ventana emergente como se describe en los pasos anteriores hace que se muestre detrás del visor mientras se encuentra en modo de pantalla completa.

   Para que la pantalla emergente se muestre tanto en modo estándar como en modo de pantalla completa, debe adjuntar la ventana emergente al contenedor del visor. Para lograrlo, puede utilizar un segundo método de controlador, `initComplete`.

   El `initComplete` controlador se invoca después de inicializar el visor.

   ```xml
   "initComplete":function() { code block }
   ```

   Obtenga más información sobre `init()` los métodos siguientes:

   * Visor de imágenes interactivo: [inicio](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-images/jsapi-interactive-image/r-html5-aem-int-image-viewer-javascriptapiref-init.html)
   * Visor de vídeo interactivo: [inicio](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-video/jsapi-interactive-video/r-html5-aem-int-video-javascriptapiref-init.html)

1. Para adjuntar la ventana emergente (descrita en los pasos anteriores) al visor, utilice el código siguiente:

   ```xml
   "initComplete":function() {
       var popup = document.getElementById('quickview_div');
       popup.parentNode.removeChild(popup);
       var sdkContainerId = s7interactivevideoviewer.getComponent("container").getInnerContainerId();
       var inner_container = document.getElementById(sdkContainerId);
       inner_container.appendChild(popup);
   }
   ```

   En el código anterior, hemos hecho lo siguiente:

   * Identificó la ventana emergente personalizada.
   * Se ha eliminado del DOM.
   * Se ha identificado el contenedor del visor.
   * Se adjuntó la ventana emergente al contenedor del visor.

1. El código setHandlers completo debe tener ahora un aspecto similar al siguiente (se ha utilizado el visor de vídeo interactivo):

   ```xml
   s7interactivevideoviewer.setHandlers({
       "quickViewActivate": function(inData) {
           var sku=inData.sku;
           loadQuickView(sku);
   
       },
       "initComplete":function() {
           var popup = document.getElementById('quickview_div'); // get custom quick view container
           popup.parentNode.removeChild(popup); // remove it from current DOM
           var sdkContainerId = s7interactivevideoviewer.getComponent("container").getInnerContainerId();
           var inner_container = document.getElementById(sdkContainerId);
           inner_container.appendChild(popup);
       }
   });
   ```

1. Una vez cargados los controladores, se inicializa el visor:

   `*viewerInstance.*init()`

   **Ejemplo** Este ejemplo utiliza el visor de imágenes interactivo.

   `s7interactiveimageviewer.init()`

   Después de incrustar el visor en la página de host, asegúrese de que se crea la instancia del visor y que los controladores se cargan antes de que se invoque el visor con `init()`.

