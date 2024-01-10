---
title: Incrustar un formulario adaptable en una página web externa
description: Aprenda a incrustar un formulario adaptable en una página web externa
contentOwner: Khushwant Singh
docset: CloudService
role: Developer
exl-id: 198f6f76-1134-4818-89a0-6ddc84ff956c
source-git-commit: a942e87a33775851631a1fe123fa3e8d2686bb30
workflow-type: ht
source-wordcount: '982'
ht-degree: 100%

---

# Incrustar un formulario adaptable basado en componentes principales en una página web externa {#embed-adaptive-form-in-external-web-page}

| Versión | Vínculo del artículo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | Este artículo |
| AEM 6.5 | [Haga clic aquí](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-basic-authoring/embed-adaptive-form-external-web-page.html?lang=es) |


Puede [integrar formularios adaptables en una página de AEM Sites](/help/forms/embed-adaptive-form-aem-sites.md) o en una página web alojada fuera de AEM. El formulario adaptable incrustado es completamente funcional, y los usuarios pueden rellenarlo y enviarlo sin abandonar la página. Esto permite al usuario mantenerse en el contexto de otros elementos de la página web e interactuar simultáneamente con el formulario.

## Requisitos previos {#prerequisites}

Realice los siguientes pasos antes de incrustar un formulario adaptable en un sitio web externo

* Publique el formulario adaptable que desee integrar en la instancia de publicación del servidor de AEM Forms.
* Cree o identifique una página web en su sitio web para alojar el formulario adaptable. Asegúrese de que la página web pueda [leer archivos jQuery de una CDN](https://ajax.googleapis.com/ajax/libs/jquery/3.3.1/jquery.min.js) o de que tenga una copia local de jQuery incrustada. jQuery es necesario para procesar un formulario adaptable.
* Cuando el servidor de AEM y la página web están en dominios diferentes, realice los pasos que se enumeran en la sección, [permitir que AEM Forms ofrezca formularios adaptables a un sitio de dominios cruzados](#cross-site).

## Incrustar formulario adaptable {#embed-adaptive-form}

Puede incrustar un formulario adaptable si inserta algunas líneas de JavaScript en la página web. La API del código envía una solicitud HTTP al servidor de AEM para obtener recursos de formularios adaptables e inserta el formulario adaptable en el contenedor de formulario especificado.

Para incrustar el formulario adaptable, haga lo siguiente:

1. Cree una página web en su sitio web con el siguiente código:

   ```html
        <!doctype html>
        <html>
          <head>
            <title>This is the title of the webpage!</title>
            <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.3.1/jquery.min.js"></script>
          </head>
          <body>
          <div class="customafsection"/>
            <p>This section is replaced with the adaptive form.</p>
   
         <script>
         var options = {path:"/content/forms/af/myadaptiveform.html", CSS_Selector:".customafsection"};
         alert(options.path);
         var loadAdaptiveForm = function(options){
         //alert(options.path);
            if(options.path) {
                // options.path refers to the path of the adaptive form
                // For Example: /content/forms/af/ABC, where ABC is the adaptive form
                // Note: If AEM server is running on a context path, the adaptive form URL must contain the context path
                var path = options.path;
                $.ajax({
                    url  : path ,
                    type : "GET",
                    data : {
                        // wcmmode=disabled is only required for author instance
                        // wcmmode : "disabled"
                    },
                    async: false,
                    success: function (data) {
                        // If jquery is loaded, set the inner html of the container
                        // If jquery is not loaded, use APIs provided by document to set the inner HTML but these APIs would not        evaluate the script tag in HTML as per the HTML5 spec
                        // For example: document.getElementById().innerHTML
                        if(window.$ && options.CSS_Selector){
                            // HTML API of jquery extracts the tags, updates the DOM, and evaluates the code embedded in the        script tag.
                            $(options.CSS_Selector).html(data);
                        }
                    },
                    error: function (data) {
                        // any error handler
                    }
                });
            } else {
                if (typeof(console) !== "undefined") {
                    console.log("Path of Adaptive Form not specified to loadAdaptiveForm");
                }
            }
         }(options);
   
         </script>
          </body>
        </html>
   ```

1. En el código incrustado:

   * Cambie el valor de la variable *options.path* con la ruta de la URL de publicación del formulario adaptable. Si el servidor de AEM se ejecuta en una ruta de contexto, asegúrese de que la dirección URL incluya la ruta de contexto. Siempre mencione el nombre completo del formulario adaptable, incluida la extensión.   Por ejemplo, el código anterior y el formulario adaptable residen en el mismo servidor de AEM Forms, por lo que el ejemplo utiliza la ruta de contexto del formulario adaptable /content/forms/af/locbasic.html.
   * CSS_Selector es el selector CSS del contenedor de formularios en el que está incrustado el formulario adaptable. Por ejemplo, la clase css .customafsection es el selector de CSS del ejemplo anterior.

El formulario adaptable está incrustado en la página web. Observe lo siguiente en el formulario adaptable integrado:

* Los borradores y los formularios enviados están disponibles en la pestaña Borradores y envíos del portal de formularios.
* La acción de envío configurada en el formulario adaptable original se mantendrá en el formulario incrustado.
* Las reglas de los formularios adaptables se conservarán y funcionarán perfectamente en el formulario incrustado.
* La segmentación de experiencias y las pruebas A/B configuradas en el formulario adaptable original no funcionarán en el formulario incrustado.
* Si Adobe Analytics está configurado en el formulario original, los datos de análisis se capturarán en el servidor de Adobe Analytics. Sin embargo, no estará disponible en el informe de análisis de Forms.
* En Formularios adaptables basados en componentes principales, las bibliotecas de cliente (ClientLibs) se incluyen y cargan junto con los componentes Encabezado y Pie de página de un formulario. Por lo tanto, cuando se incrusta un Formulario adaptable basado en componentes principales en una página web, siempre incluye el encabezado y el pie de página del formulario.

## Topología de ejemplo {#sample-topology}

La página web externa que incrusta el formulario adaptable envía solicitudes al servidor de AEM, que normalmente se encuentra detrás del firewall en una red privada. Para garantizar que las solicitudes se dirijan de forma segura al servidor de AEM, se recomienda configurar un servidor proxy inverso.

Veamos un ejemplo de cómo puede configurar un servidor proxy inverso Apache 2.4 sin Dispatcher. En este ejemplo, alojará el servidor de AEM con la ruta de contexto `/forms` y el mapa `/forms` para el proxy inverso. Garantiza que cualquier solicitud de `/forms` en el servidor de Apache se dirijan a la instancia de AEM. Esta topología ayuda a reducir el número de reglas en la capa de Dispatcher, ya que todas las solicitudes con el prefijo `/forms` se envían al servidor de AEM.

1. Abra el archivo de configuración `httpd.conf` y quite el comentario de las siguientes líneas de código. Como alternativa, puede agregar estas líneas de código en el archivo.

   ```text
   LoadModule proxy_html_module modules/mod_proxy_html.so
   LoadModule proxy_http_module modules/mod_proxy_http.so
   ```

1. Configure las reglas de proxy al agregar las siguientes líneas de código en el archivo de configuración `httpd-proxy.conf`.

   ```text
   ProxyPass /forms https://[AEM_Instance]/forms
   ProxyPassReverse /forms https://[AEM_Instance]/forms
   ```

   Reemplace `[AEM_Instance]` por la URL de publicación del servidor de AEM en las reglas.

Si no monta el servidor AEM en una ruta de contexto, las reglas de proxy en la capa de Apache serán las siguientes:

```text
ProxyPass /content https://<AEM_Instance>/content
ProxyPass /etc https://<AEM_Instance>/etc
ProxyPass /etc.clientlibs https://<AEM_Instance>/etc.clientlibs
# CSRF Filter
ProxyPass /libs/granite/csrf/token.json https://<AEM_Instance>/libs/granite/csrf/token.json

ProxyPassReverse /etc https://<AEM_Instance>/etc
ProxyPassReverse /etc.clientlibs https://<AEM_Instance>/etc.clientlibs
# written for thank you page and other URL present in AF during redirect
ProxyPassReverse /content https://<AEM_Instance>/content
```

>[!NOTE]
>
>Si configura cualquier otra topología, asegúrese de agregar las direcciones URL de envío, de relleno previo y de otro tipo a la lista de permitidos de Dispatcher.

## Prácticas recomendadas {#best-practices}

Al incrustar un formulario adaptable en una página web, tenga en cuenta las siguientes prácticas recomendadas:

* Asegúrese de que las reglas de estilo definidas en la página web de CSS no entren en conflicto con el objeto de formulario de CSS. Para evitar conflictos, puede reutilizar la página web de CSS en la temática del formulario adaptable mediante la biblioteca de cliente de AEM. Para obtener información sobre el uso de la biblioteca de cliente en temáticas de formularios adaptables, consulte [Temáticas en AEM Forms](/help/forms/using-themes-in-core-components.md).
* Haga que el contenedor de formularios de la página web utilice la anchura de toda la ventana. Garantiza que las reglas CSS configuradas para dispositivos móviles funcionen sin ningún cambio. Si el contenedor de formularios no tiene la anchura de toda la ventana, deberá escribir un CSS personalizado para que el formulario se adapte a diferentes dispositivos móviles.
* Use la API `[getData](https://developer.adobe.com/experience-manager/reference-materials/6-5/forms/javascript-api/GuideBridge.html)` para obtener la representación XML o JSON de los datos de formulario en el cliente.
* Use la API `[unloadAdaptiveForm](https://developer.adobe.com/experience-manager/reference-materials/6-5/forms/javascript-api/GuideBridge.html)` para descargar el formulario adaptable desde DOM HTML.
* Configure el encabezado access-control-origin al enviar la respuesta desde el servidor de AEM.

## Permita que AEM Forms ofrezca formularios adaptables a un sitio de dominios cruzados {#cross-site}

1. En la instancia de publicación de AEM, vaya al Administrador de configuración de la consola web de AEM en `https://'[server]:[port]'/system/console/configMgr`.
1. Busque y abra la configuración **Filtro de referencias de Apache Sling**.
1. En el campo Hosts permitidos, especifique el dominio en el que reside la página web. Permita que el host realice peticiones POST al servidor de AEM. También puede utilizar una expresión regular para especificar una serie de dominios de aplicación externos.

<!--

>[!MORELIKETHIS]
>
>* [Embed adaptive form based on core components to AEM sites](/help/forms/embed-adaptive-form-core-components-aem-sites.md)

-->