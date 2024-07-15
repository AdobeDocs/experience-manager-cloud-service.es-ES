---
title: Creación de ventanas emergentes personalizadas con Quickview
description: Obtenga información sobre cómo se utiliza la vista rápida predeterminada en las experiencias de comercio electrónico, mediante la cual se muestra una ventana emergente con información del producto para impulsar una compra. Puede almacenar en déclencheur el contenido personalizado para que se muestre en la ventana emergente.
contentOwner: Rick Brough
feature: Interactive Images,Interactive Videos,Carousel Banners
role: Admin,User
exl-id: c2bc6ec8-d46e-4681-ac3e-3337b9e6ae5c
source-git-commit: bae9a5178c025b3bafa8ac2da75a1203206c16e1
workflow-type: tm+mt
source-wordcount: '944'
ht-degree: 2%

---

# Creación de ventanas emergentes personalizadas con Quickview {#using-quickviews-to-create-custom-pop-ups}

La vista rápida predeterminada se utiliza en las experiencias de comercio electrónico, donde se muestra una ventana emergente con información del producto para impulsar una compra. Sin embargo, puede almacenar en déclencheur el contenido personalizado para que se muestre en los elementos emergentes. Según el visualizador que utilice, los clientes pueden seleccionar un punto interactivo, una imagen en miniatura o un mapa de imagen para ver información o contenido relacionado.

Quickview es compatible con los siguientes visores en Dynamic Media:

* Imágenes interactivas (zonas interactivas seleccionables)
* Vídeo interactivo (imágenes en miniatura seleccionables durante la reproducción de vídeo)
* Banners de carrusel (zonas interactivas seleccionables o mapas de imagen)

Aunque la funcionalidad de cada visualizador es diferente, el proceso de creación de una vista rápida es el mismo en los tres visualizadores admitidos.

**Para crear ventanas emergentes personalizadas con la vista rápida:**

1. Crear una vista rápida para un recurso cargado.

   Normalmente, crea una vista rápida el mismo tiempo que edita un recurso para utilizarlo con el visor que está utilizando.

   <table>
    <tbody>
    <tr>
    <td><strong>Visor que está utilizando</strong></td>
    <td><strong>Para crear la vista rápida, complete estos pasos</strong></td>
    </tr>
    <tr>
    <td>Imágenes interactivas</td>
    <td><a href="/help/assets/dynamic-media/interactive-images.md#adding-hotspots-to-an-image-banner" target="_blank">Agregando puntos interactivos a un titular de imagen</a>.</td>
    </tr>
    <tr>
    <td>Vídeos interactivos</td>
    <td><a href="/help/assets/dynamic-media/interactive-videos.md#adding-interactivity-to-your-video" target="_blank">Agregando interactividad al vídeo</a>.</td>
    </tr>
    <tr>
    <td>Banner de carrusel</td>
    <td><a href="/help/assets/dynamic-media/carousel-banners.md#adding-hotspots-or-image-maps-to-an-image-banner" target="_blank">Agregar puntos interactivos o mapas de imagen a un titular</a>.<br /> </td>
    </tr>
    </tbody>
   </table>

1. Obtenga el código incrustado del visualizador para integrar el visualizador en el sitio web.

   <table>
    <tbody>
    <tr>
    <td><strong>Visor que está usando</strong><br /> </td>
    <td><strong>Para integrar el visor con su sitio web, complete estos pasos</strong></td>
    </tr>
    <tr>
    <td>Imagen interactiva</td>
    <td><a href="/help/assets/dynamic-media/interactive-images.md#integrating-an-interactive-image-with-your-website" target="_blank">Integrando una imagen interactiva con su sitio web</a>.<br /> </td>
    </tr>
    <tr>
    <td>Vídeo interactivo<br /> </td>
    <td><a href="/help/assets/dynamic-media/interactive-videos.md#integrating-an-interactive-video-with-your-website" target="_blank">Integrando un vídeo interactivo con su sitio web</a>.<br /> </td>
    </tr>
    <tr>
    <td>Titular de carrusel</td>
    <td><a href="/help/assets/dynamic-media/carousel-banners.md#adding-a-carousel-banner-to-your-website-page" target="_blank">Agregando un banner de carrusel a la página del sitio web</a>.<br /> </td>
    </tr>
    </tbody>
   </table>

1. El visualizador que utilice debe saber cómo utilizar la vista rápida.

   El visor usa un controlador denominado `QuickViewActive`.

   **Ejemplo**
Supongamos que está utilizando el siguiente código incrustado de muestra en la página web para una imagen interactiva:

   ![chlimage_1-291](assets/chlimage_1-291.png)

   El controlador se ha cargado en el visor mediante `setHandlers`:

   `*viewerInstance*.setHandlers({ *handler 1*, *handler 2*}, ...`

   **Utilizando el ejemplo de código incrustado de ejemplo anterior, tiene el siguiente código:**

   ```xml {.line-numbers}
   s7interactiveimageviewer.setHandlers({
       quickViewActivate": function(inData) {
           var sku=inData.sku;
           var genericVariable1=inData.genericVariable1;
           var genericVariable2=inData.genericVariable2;
          loadQuickView(sku,genericVariable1,genericVariable2);
       }
   })
   ```

   Obtenga más información acerca del método `setHandlers()` en los siguientes enlaces:

   * Visor de imágenes interactivo - [sethandlers](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-images/jsapi-interactive-image/r-html5-aem-int-image-viewer-javascriptapiref-sethandlers.html)
   * Visor de vídeo interactivo: [sethandlers](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-video/jsapi-interactive-video/r-html5-aem-int-video-javascriptapiref-sethandlers.html)

1. Ahora configure el controlador `quickViewActivate`.

   El controlador `quickViewActivate` controla la vista rápida en el visor. El controlador contiene la lista de variables y las llamadas a funciones para su uso con la vista rápida. El código incrustado proporciona asignación para la variable SKU establecida en la vista rápida. También realiza una llamada a la función `loadQuickView` de ejemplo.

   **Asignación de variables**
Asigne variables para su uso en la página web al valor SKU y a las variables genéricas contenidas en la vista rápida:

   `var *variable1*= inData.*quickviewVariable*`

   El código incrustado proporcionado tiene una asignación de muestra para la variable SKU:

   `var sku=inData.sku`

   Asigne otras variables de la vista rápida a, como en los siguientes casos:

   ```xml {.line-numbers}
   var <i>variable2</i>= inData.<i>quickviewVariable2</i>
    var <i>variable3</i>= inData.<i>quickviewVariable3</i>
   ```

   **Llamada de función**
El controlador también requiere una llamada a la función para que funcione la vista rápida. La página host supone que puede acceder a la función. El código incrustado proporciona una llamada a una función de ejemplo:

   `loadQuickView(sku)`

   La llamada a la función de ejemplo supone que la función `loadQuickView()` existe y es accesible.

   Obtenga más información acerca del método `quickViewActivate` en los siguientes enlaces:

   * Visor de imágenes interactivo - [Devoluciones de llamadas de evento](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-images/c-html5-aem-interactive-image-event-callbacks.html)
   * Visor de vídeo interactivo - [Devoluciones de llamadas de evento](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-video/c-html5-aem-int-video-event-callbacks.html)
   * Compatibilidad con datos interactivos en el visor de vídeo interactivo: [compatibilidad con datos interactivos](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-video/c-html5-aem-int-video-int-data-support.html)

1. Haga lo siguiente:

   * Elimine los comentarios de la sección setHandlers del código incrustado.
   * Asigne cualquier variable adicional contenida en la vista rápida.

      * Actualice la llamada a `loadQuickView(sku,*var1*,*var2*)` si agrega más variables.

   * Cree una función `loadQuickView` () simple en la página, fuera del visor.

     Por ejemplo, lo siguiente escribe el valor de SKU en la consola del explorador:

   ```xml {.line-numbers}
   function loadQuickView(sku){
       console.log ("quickview sku value is " + sku);
   }
   ```

   * Cargue una página de HTML de pruebas en un servidor web y ábrala.

     Las variables de la vista rápida están asignadas. La llamada a la función está configurada. Y la consola del explorador escribe el valor de la variable en la consola del explorador. Para ello, utiliza la función de ejemplo proporcionada.

1. Ahora puede utilizar una función para invocar una ventana emergente simple en la vista rápida. El siguiente ejemplo usa un `DIV` para una ventana emergente.
1. Establezca el estilo de la ventana emergente `DIV` de la siguiente manera. Añada un estilo adicional como desee.

   ```xml {.line-numbers}
   <style type="text/css">
       #quickview_div{
           position: absolute;
           z-index: 99999999;
           display: none;
       }
   </style>
   ```

1. Coloque la ventana emergente `DIV` en el cuerpo de la página de HTML.

   Uno de los elementos se configura con un ID que se actualiza con el valor SKU cuando el usuario invoca una vista rápida. El ejemplo también incluye un botón simple para ocultar de nuevo la ventana emergente una vez que esté visible.

   ```xml {.line-numbers}
   <div id="quickview_div" >
       <table>
           <tr><td><input id="btnClosePopup" type="button" value="Close"        onclick='document.getElementById("quickview_div").style.display="none"' /><br /></td></tr>
           <tr><td>SKU</td><td><input type="text" id="txtSku" name="txtSku"></td></tr>
       </table>
   </div>
   ```

1. Para actualizar el valor SKU en la ventana emergente, añada una función. Para que la ventana emergente sea visible, reemplace la función simple creada en el paso 5 por lo siguiente:

   ```xml {.line-numbers}
   <script type="text/javascript">
       function loadQuickView(sku){
           document.getElementById("txtSku").setAttribute("value",sku); // write sku value
           document.getElementById("quickview_div").style.display="block"; // show pop-up
       }
   </script>
   ```

1. Cargue una página del HTML de pruebas en el servidor web y abra. El visor muestra la ventana emergente `DIV` cuando un usuario invoca una vista rápida.
1. **Cómo mostrar la ventana emergente personalizada en modo de pantalla completa**

   Algunos visores, como el visualizador de vídeo interactivo, admiten la visualización en modo de pantalla completa. Sin embargo, el uso de la ventana emergente como se describe en los pasos anteriores hace que se muestre detrás del visor mientras está en modo de pantalla completa.

   Para que la ventana emergente se muestre en los modos de pantalla estándar y pantalla completa, adjunte la ventana emergente al contenedor del visor. En este caso, use un segundo método de controlador, `initComplete`.

   Se invoca el controlador `initComplete` después de inicializar el visor.

   ```xml {.line-numbers}
   "initComplete":function() { code block }
   ```

   Obtenga más información acerca del método `init()` en los siguientes enlaces:

   * Visor de imágenes interactivo: [init](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-images/jsapi-interactive-image/r-html5-aem-int-image-viewer-javascriptapiref-init.html)
   * Visor de vídeo interactivo: [init](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-video/jsapi-interactive-video/r-html5-aem-int-video-javascriptapiref-init.html)

1. Para adjuntar la ventana emergente (descrita en los pasos anteriores) al visor, utilice el siguiente código:

   ```xml {.line-numbers}
   "initComplete":function() {
       var popup = document.getElementById('quickview_div');
       popup.parentNode.removeChild(popup);
       var sdkContainerId = s7interactivevideoviewer.getComponent("container").getInnerContainerId();
       var inner_container = document.getElementById(sdkContainerId);
       inner_container.appendChild(popup);
   }
   ```

   En el código anterior, ha hecho lo siguiente:

   * Se ha identificado la ventana emergente personalizada.
   * Se ha eliminado del DOM.
   * Se ha identificado el contenedor del visor.
   * Se ha adjuntado la ventana emergente al contenedor del visor.

1. Todo el código de setHandlers es similar al siguiente (se ha utilizado el visualizador de vídeo interactivo):

   ```xml {.line-numbers}
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

   **Ejemplo**
Este ejemplo utiliza el visualizador de imágenes interactivo.

   `s7interactiveimageviewer.init()`

   Después de incrustar el visor en la página host, asegúrese de que se ha creado la instancia del visor. Además, asegúrese de que los controladores se carguen antes de que se invoque el visor con `init()`.
