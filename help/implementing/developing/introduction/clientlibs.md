---
title: Uso de bibliotecas del lado del cliente en AEM as a Cloud Service
description: AEM proporciona Carpetas de biblioteca del lado del cliente, que le permiten almacenar el código del lado del cliente (clientlibs) en el repositorio, organizarlo en categorías y definir cuándo y cómo se debe servir cada categoría de código al cliente
exl-id: 370db625-09bf-43fb-919d-4699edaac7c8
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 10580c1b045c86d76ab2b871ca3c0b7de6683044
workflow-type: tm+mt
source-wordcount: '2497'
ht-degree: 1%

---


# Uso de bibliotecas del lado del cliente en AEM as a Cloud Service {#using-client-side-libraries}

Las experiencias digitales dependen en gran medida del procesamiento del lado del cliente impulsado por código CSS y JavaScript complejo. AEM Las bibliotecas del lado del cliente (clientlibs) le permiten organizar y almacenar de forma centralizada estas bibliotecas del lado del cliente dentro del repositorio. AEM AEM Junto con el proceso de compilación del front-end [en el tipo de archivo del proyecto de](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/uifrontend.html?lang=es), la administración del código del front-end para el proyecto de la aplicación se vuelve sencilla.

AEM Entre las ventajas de usar clientlibs en la práctica se incluyen las siguientes:

* El código del lado del cliente se almacena en el repositorio como el resto del código y el contenido de la aplicación
* AEM Clientlibs en la puede agregar todos los CSS y JS en un archivo
* Exponer clientlibs a través de una ruta a la que se pueda acceder mediante [Dispatcher](/help/implementing/dispatcher/disp-overview.md)
* Permite la reescritura de rutas para archivos o imágenes referenciados

Clientlibs es la solución integrada para ofrecer CSS y JavaScript AEM desde el punto de vista de los clientes

>[!TIP]
>
>Los desarrolladores de front-end que estén creando CSS y JavaScript AEM AEM para proyectos de también deben familiarizarse con el [Arquetipo de proyecto de y su proceso automatizado de compilación de front-end](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/uifrontend.html?lang=es).

## Qué son las bibliotecas del lado del cliente {#what-are-clientlibs}

Los sitios requieren JavaScript y CSS, y recursos estáticos como iconos y fuentes web para procesarlos en el lado del cliente. AEM Una clientlib es el mecanismo de referencia que se utiliza para hacer referencia a (por categoría si es necesario) y para servir dichos recursos.

AEM el CSS y el JavaScript del sitio en un solo archivo, en una ubicación central, para garantizar que solo se incluya una copia de cualquier recurso en la salida del HTML. Esto maximiza la eficacia de la entrega y permite que estos recursos se mantengan centralmente en el repositorio a través de proxy, manteniendo el acceso seguro.

## Desarrollo front-end para AEM as a Cloud Service {#fed-for-aemaacs}

Todos los recursos de JavaScript AEM, CSS y otros recursos front-end deben mantenerse en el módulo [ui.frontend del tipo de archivo del proyecto de](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/uifrontend.html?lang=es). La flexibilidad del tipo de archivo permite utilizar las herramientas web modernas que elija para crear y administrar estos recursos.

A continuación, el tipo de archivo puede compilar los recursos en archivos CSS y JS únicos, incrustándolos automáticamente en un `cq:clientLibraryFolder` del repositorio.

## Estructura de carpetas de biblioteca del lado del cliente {#clientlib-folders}

Una carpeta de biblioteca del lado del cliente es un nodo de repositorio de tipo `cq:ClientLibraryFolder`. Su definición en [notación CND](https://jackrabbit.apache.org/node-type-notation.html) es

```text
[cq:ClientLibraryFolder] > sling:Folder
  - dependencies (string) multiple
  - categories (string) multiple
  - embed (string) multiple
  - channels (string) multiple
```

* `cq:ClientLibraryFolder` nodos se pueden colocar en cualquier lugar dentro del subárbol `/apps` del repositorio.
* Utilice la propiedad `categories` del nodo para identificar las categorías de biblioteca a las que pertenece.

Cada `cq:ClientLibraryFolder` se rellena con un conjunto de archivos JS o CSS, junto con algunos archivos auxiliares (ver a continuación). Las propiedades importantes de `cq:ClientLibraryFolder` se configuran de la siguiente manera:

* `allowProxy`: dado que todos los clientlibs deben almacenarse en `apps`, esta propiedad permite el acceso a las bibliotecas de cliente a través del servlet proxy. Consulte la sección [Localización de una carpeta de biblioteca de cliente y uso del servlet de bibliotecas de cliente proxy](#locating-a-client-library-folder-and-using-the-proxy-client-libraries-servlet) a continuación.
* `categories`: identifica las categorías en las que se encuentra el conjunto de archivos JS y/o CSS dentro de este(a) `cq:ClientLibraryFolder`. La propiedad `categories`, al ser de varios valores, permite que una carpeta de biblioteca forme parte de más de una categoría (vea a continuación para ver cómo puede resultar de utilidad).

Si la carpeta de la biblioteca cliente contiene uno o varios archivos de código fuente que, en tiempo de ejecución, se combinan en un solo archivo JS o CSS. El nombre del archivo generado es el nombre del nodo con la extensión de nombre de archivo `.js` o `.css`. Por ejemplo, el nodo de biblioteca denominado `cq.jquery` genera el archivo generado denominado `cq.jquery.js` o `cq.jquery.css`.

Las carpetas de la biblioteca de cliente contienen los siguientes elementos:

* Los archivos de origen JS o CSS
* Recursos estáticos compatibles con los estilos CSS, como iconos, fuentes web, etc.
* Un archivo `js.txt` o un archivo `css.txt` que identifican los archivos de origen que se van a combinar en los archivos JS o CSS generados

![Arquitectura Clientlib](assets/clientlib-architecture.drawio.png)

## Creación de carpetas de biblioteca del lado del cliente {#creating-clientlib-folders}

Las bibliotecas de cliente deben encontrarse en `/apps`. Esta regla es necesaria para aislar mejor el código del contenido y la configuración.

Para que se pueda acceder a las bibliotecas de cliente de `/apps`, se utiliza un servlet proxy. Las ACL siguen aplicándose en la carpeta de biblioteca del cliente, pero el servlet permite que el contenido se lea a través de `/etc.clientlibs/` si la propiedad `allowProxy` está establecida en `true`.

1. Abra el CRXDE Lite en un explorador web (`https://<host>:<port>/crx/de`).
1. Seleccione la carpeta `/apps` y haga clic en **Crear > Crear nodo**.
1. Escriba un nombre para la carpeta de la biblioteca y en la lista **Type** seleccione `cq:ClientLibraryFolder`. Haz clic en **Aceptar** y luego haz clic en **Guardar todo**.
1. Para especificar la categoría o categorías a las que pertenece la biblioteca, seleccione el nodo `cq:ClientLibraryFolder`, agregue la siguiente propiedad y, a continuación, haga clic en **Guardar todo**:
   * Nombre: `categories`
   * Tipo: cadena
   * Valor: Nombre de la categoría
   * Múltiple: seleccionado
1. Para que las bibliotecas de cliente sean accesibles a través del proxy bajo `/etc.clientlibs`, seleccione el nodo `cq:ClientLibraryFolder`, agregue la siguiente propiedad y, a continuación, haga clic en **Guardar todo**:
   * Nombre: `allowProxy`
   * Tipo: booleano
   * Valor: `true`
1. Si necesita administrar recursos estáticos, cree una subcarpeta con el nombre `resources` debajo de la carpeta de la biblioteca de cliente.
   * Si almacena recursos estáticos en cualquier lugar que no sea la carpeta `resources`, no se podrá hacer referencia a ellos en una instancia de publicación.
1. Añada los archivos de origen a la carpeta de la biblioteca.
   * AEM Esto generalmente lo hace el proceso de compilación del front-end de [Arquetipo de proyecto de ](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/uifrontend.html?lang=es).
   * Si lo desea, puede organizar los archivos de origen en subcarpetas.
1. Seleccione la carpeta de la biblioteca de cliente y haga clic en **Crear > Crear archivo**.
1. En el cuadro de nombre de archivo, escriba uno de los siguientes nombres de archivo y haga clic en Aceptar:
   * **`js.txt`:** Use este nombre de archivo para generar un archivo de JavaScript.
   * **`css.txt`:** Use este nombre de archivo para generar una hoja de estilos en cascada.
1. Abra el archivo y escriba el siguiente texto para identificar la raíz de la ruta de los archivos de origen:
   * `#base=*[root]*`
   * Reemplace `[root]` por la ruta de acceso a la carpeta que contiene los archivos de origen, relativa al archivo TXT. Por ejemplo, utilice el siguiente texto cuando los archivos de origen estén en la misma carpeta que el archivo TXT:
      * `#base=.`
   * El siguiente código establece la raíz como la carpeta denominada mobile debajo del nodo `cq:ClientLibraryFolder`:
      * `#base=mobile`
1. En las líneas por debajo de `#base=[root]`, escriba las rutas de acceso de los archivos de origen relativos a la raíz. Coloque cada nombre de archivo en una línea independiente.
1. Haga clic en **Guardar todo**.

## Servicio de bibliotecas del lado del cliente {#serving-clientlibs}

Una vez que la carpeta de la biblioteca de cliente esté [configurada según se requiera](#creating-clientlib-folders), se podrán solicitar los clientlibs a través de un proxy. A modo de ejemplo:

* Tiene una clientlib en `/apps/myproject/clientlibs/foo`
* Tiene una imagen estática en `/apps/myprojects/clientlibs/foo/resources/icon.png`

La propiedad `allowProxy` le permite solicitar:

* La clientlib mediante `/etc.clientlibs/myprojects/clientlibs/foo.js`
* La imagen estática mediante `/etc.clientlibs/myprojects/clientlibs/foo/resources/icon.png`

### Carga de bibliotecas de cliente mediante HTL {#loading-via-htl}

Una vez que los clientlibs se hayan almacenado y administrado correctamente en la carpeta de biblioteca de cliente, se puede acceder a ellos a través de HTL.

AEM Las bibliotecas de cliente se cargan a través de una plantilla de ayuda proporcionada por, a la cual se puede tener acceso mediante `data-sly-use`. Las plantillas de ayuda están disponibles en este archivo, al que se puede llamar mediante `data-sly-call`.

Cada plantilla de ayuda espera una opción `categories` para hacer referencia a las bibliotecas de cliente deseadas. Esa opción puede ser una matriz de valores de cadena o una cadena que contenga una lista de valores separados por comas.

[Consulte la documentación de HTL](https://experienceleague.adobe.com/docs/experience-manager-htl/using/getting-started/getting-started.html?lang=es#loading-client-libraries) para obtener más información sobre cómo cargar clientlibs a través de HTL.

<!--
### Setting Cache Timestamps {#setting-cache-timestamps}

This is possible. Still need detail.
-->

## Bibliotecas de cliente en Author y Publish {#clientlibs-author-publish}

AEM La mayoría de los clientlibs son obligatorios en la instancia de publicación de la. Es decir, la mayoría de los propósitos de los clientlibs son producir la experiencia del usuario final del contenido. Para clientlibs en instancias de publicación, [herramientas de compilación del front-end](#fed-for-aemaacs) se pueden usar e implementar a través de [carpetas de biblioteca de cliente como se describe más arriba](#creating-clientlib-folders).

Sin embargo, hay ocasiones en que puede ser necesario usar bibliotecas de cliente para personalizar la experiencia de creación. AEM Por ejemplo, la personalización de un cuadro de diálogo puede requerir la implementación de pequeños bits de CSS o JS en la instancia de creación de la aplicación de la instancia de creación de la.

### Administración de bibliotecas de cliente en Author {#clientlibs-on-author}

Si necesita usar bibliotecas de cliente en Author, puede crear sus bibliotecas de cliente en `/apps` utilizando los mismos métodos que para Publish, pero escríbalo directamente en `/apps/.../clientlibs/foo` en lugar de crear un proyecto completo para administrarlo.

A continuación, puede &quot;conectar&quot; al JS de creación añadiendo las bibliotecas de cliente a una categoría de biblioteca de cliente predeterminada.

## Herramientas de depuración {#debugging-tools}

AEM proporciona varias herramientas para depurar y probar carpetas de la biblioteca de cliente.

### Descubrir bibliotecas de cliente {#discover-client-libraries}

El componente `/libs/cq/granite/components/dumplibs/dumplibs` genera una página de información sobre todas las carpetas de la biblioteca de cliente del sistema. El nodo `/libs/granite/ui/content/dumplibs` tiene el componente como tipo de recurso. Para abrir la página, utilice la siguiente URL (cambiando el host y el puerto según sea necesario):

`https://<host>:<port>/libs/granite/ui/content/dumplibs.test.html`

La información incluye la ruta y el tipo de la biblioteca (CSS o JS) y los valores de los atributos de la biblioteca, como las categorías y dependencias. Las tablas posteriores de la página muestran las bibliotecas de cada categoría y canal.

### Consulte Salida generada {#see-generated-output}

El componente `dumplibs` incluye un selector de prueba que muestra el código fuente generado para las etiquetas `ui:includeClientLib`. La página incluye código para diferentes combinaciones de atributos js, css y temáticos.

1. Utilice uno de los siguientes métodos para abrir la página Resultados de la prueba:
   * En la página `dumplibs.html`, haga clic en el vínculo del texto **Haga clic aquí para probar la salida**.
   * Abra la siguiente URL en el explorador web (utilice un host y un puerto diferentes según sea necesario):
      * `http://<host>:<port>/libs/granite/ui/content/dumplibs.html`
   * La página predeterminada muestra el resultado de las etiquetas sin valor para el atributo categories.
1. Para ver el resultado de una categoría, escriba el valor de la propiedad `categories` de la biblioteca de cliente y haga clic en **Enviar consulta**.

## Funciones adicionales de carpeta de biblioteca de cliente {#additional-features}

AEM Hay otras funciones compatibles con las carpetas de biblioteca de cliente en la documentación de la biblioteca de. Sin embargo, no son necesarios en AEM as a Cloud Service y, por lo tanto, se desaconseja su uso. Se enumeran aquí para completar la información.

>[!WARNING]
>
>Estas funciones adicionales de las carpetas de la biblioteca de clientes no son necesarias en AEM as a Cloud Service y, por lo tanto, se desaconseja su uso. Se enumeran aquí para completar la información.

### Adobe Granite HTML LIbrary Manager {#html-library-manager}

Se puede controlar la configuración adicional de la biblioteca de cliente a través del panel **Administrador de bibliotecas de Adobe Granite HTML** de la consola del sistema en `https://<host>:<port>/system/console/configMgr`).

### Propiedades de carpeta adicionales {#additional-folder-properties}

Las propiedades de carpeta adicionales incluyen permitir el control de dependencias e incrustaciones, pero generalmente ya no son necesarias y se desaconseja su uso:

* `dependencies`: es una lista de otras categorías de bibliotecas de cliente de las que depende esta carpeta de biblioteca. Por ejemplo, dados dos nodos `cq:ClientLibraryFolder` `F` y `G`, si un archivo de `F` requiere otro archivo de `G` para funcionar correctamente, al menos uno de los `categories` de `G` debe estar entre los `dependencies` de `F`.
* `embed`: se usa para incrustar código de otras bibliotecas. Si el nodo `F` incrusta los nodos `G` y `H`, el HTML resultante es una concatenación de contenido de los nodos `G` y `H`.

### Vinculación a dependencias {#linking-to-dependencies}

Cuando el código de la carpeta de la biblioteca de cliente haga referencia a otras bibliotecas, identifique las demás bibliotecas como dependencias. La etiqueta `ui:includeClientLib` que hace referencia a la carpeta de biblioteca de cliente hace que el código del HTML incluya un vínculo al archivo de biblioteca generado y a las dependencias.

Las dependencias deben ser otras `cq:ClientLibraryFolder`. Para identificar dependencias, agregue una propiedad al nodo `cq:ClientLibraryFolder` con los atributos siguientes:

* **Nombre:** dependencias
* **Tipo:** Cadena[]
* **Valores:** El valor de la propiedad categories del nodo cq:ClientLibraryFolder del que depende la carpeta de biblioteca actual.

Por ejemplo, `/etc/clientlibs/myclientlibs/publicmain` depende de la biblioteca `cq.jquery`. La página que hace referencia a la biblioteca de cliente principal genera un HTML que incluye el siguiente código:

```xml
<script src="/etc/clientlibs/foundation/cq.jquery.js" type="text/javascript">
<script src="/etc/clientlibs/mylibs/publicmain.js" type="text/javascript">
```

### Incrustar Código De Otras Bibliotecas {#embedding-code-from-other-libraries}

Puede incrustar código de una biblioteca de cliente en otra biblioteca de cliente. En tiempo de ejecución, los archivos JS y CSS generados de la biblioteca de incrustación incluyen el código de la biblioteca incrustada.

La incrustación de código resulta útil para proporcionar acceso a bibliotecas almacenadas en áreas seguras del repositorio.

#### Carpetas de la biblioteca de clientes específicas de la aplicación {#app-specific-client-library-folders}

Se recomienda mantener todos los archivos relacionados con la aplicación en la carpeta de su aplicación por debajo de `/apps`. También se recomienda denegar el acceso a los visitantes del sitio web a la carpeta `/apps`. Para satisfacer ambas prácticas recomendadas, cree una carpeta de biblioteca de cliente debajo de la carpeta `/etc` que incruste la biblioteca de cliente debajo de `/apps`.

Utilice la propiedad categories para identificar la carpeta de biblioteca de cliente que se va a incrustar. Para incrustar la biblioteca, agregue una propiedad al nodo `cq:ClientLibraryFolder` que se está incrustando, utilizando los siguientes atributos de propiedad:

* **Nombre:** incrustado
* **Tipo:** Cadena[]
* **Valor:** Valor de la propiedad categories del nodo `cq:ClientLibraryFolder` que se va a incrustar.

#### Uso de la incrustación para minimizar las solicitudes {#using-embedding-to-minimize-requests}

En algunos casos, es posible que el HTML final que genera la instancia de publicación para la página típica incluya un número relativamente grande de `<script>` elementos.

En estos casos, puede resultar útil combinar todo el código de biblioteca de cliente necesario en un solo archivo para reducir el número de solicitudes de ida y vuelta al cargar la página. Para ello, puede `embed` las bibliotecas necesarias en su biblioteca de cliente específica de la aplicación mediante la propiedad embed del nodo `cq:ClientLibraryFolder`.

#### Rutas en archivos CSS {#paths-in-css-files}

Al incrustar archivos CSS, el código CSS generado utiliza rutas a recursos relativos a la biblioteca de incrustación. Por ejemplo, la biblioteca de acceso público `/etc/client/libraries/myclientlibs/publicmain` incrusta la biblioteca de cliente `/apps/myapp/clientlib`:

El archivo `main.css` contiene el siguiente estilo:

```javascript
body {
  padding: 0;
  margin: 0;
  background: url(images/bg-full.jpg) no-repeat center top;
  width: 100%;
}
```

El archivo CSS que genera el nodo `publicmain` contiene el siguiente estilo, con la dirección URL de la imagen original:

```javascript
body {
  padding: 0;
  margin: 0;
  background: url(../../../apps/myapp/clientlib/styles/images/bg-full.jpg) no-repeat center top;
  width: 100%;
}
```

#### Consulte Archivos incrustados en la salida del HTML {#see-embedded-files}

Para realizar un seguimiento del origen del código incrustado o para asegurarse de que las bibliotecas de cliente incrustadas producen los resultados esperados, puede ver los nombres de los archivos que se están incrustando durante la ejecución. Para ver los nombres de archivo, agregue el parámetro `debugClientLibs=true` a la dirección URL de la página web. La biblioteca que se genera contiene `@import` instrucciones en lugar del código incrustado.

En el ejemplo de la sección [Incrustar código de otras bibliotecas](#embedding-code-from-other-libraries) anterior, la carpeta de biblioteca de cliente `/etc/client/libraries/myclientlibs/publicmain` incrusta la carpeta de biblioteca de cliente `/apps/myapp/clientlib`. Al anexar el parámetro a la página web, se produce el siguiente vínculo en el código fuente de la página web:

```xml
<link rel="stylesheet" href="/etc/clientlibs/mycientlibs/publicmain.css">
```

Al abrir el archivo `publicmain.css`, se muestra el siguiente código:

```javascript
@import url("/apps/myapp/clientlib/styles/main.css");
```

1. En el cuadro de la dirección del navegador web, añada el siguiente texto a la dirección URL del HTML:
   * `?debugClientLibs=true`
1. Cuando se cargue la página, vea el origen de la página.
1. Haga clic en el vínculo proporcionado como href para el elemento de vínculo para abrir el archivo y ver el código fuente.

### Uso de preprocesadores {#using-preprocessors}

El preprocesador [YUI Compressor](https://github.com/yui/yuicompressor#yui-compressor---the-yahoo-javascript-and-css-compressor) para CSS y JavaScript y [Google Closure Compiler (GCC)](https://developers.google.com/closure/compiler/) para JavaScript con YUI establecido como preprocesador predeterminado para la conexión permite que los preprocesadores se puedan conectar y los envíos con soporte para YUI Compressor para CSS y AEM y AEM Closure Compiler (GCC) para con YUI establecido como preprocesador predeterminado para la conexión.

Los preprocesadores conectables permiten un uso flexible que incluye:

* Definición de ScriptProcessors que pueden procesar las fuentes de los scripts
* Los procesadores se pueden configurar con opciones
* Los procesadores se pueden utilizar para la minificación, pero también para casos no minificados
* La clientlib puede definir qué procesador utilizar

>[!NOTE]
>
>AEM De forma predeterminada, utiliza el compresor YUI. Consulte la [documentación de GitHub del compresor YUI](https://github.com/yui/yuicompressor/issues) para obtener una lista de problemas conocidos. Cambiar al compresor GCC para clientlibs particulares puede resolver algunos problemas observados al utilizar YUI.

>[!CAUTION]
>
>No coloque ninguna biblioteca minificada en una biblioteca de cliente. En su lugar, proporcione la biblioteca sin procesar y, si se requiere la minificación, utilice las opciones de los preprocesadores.

#### Uso {#usage}

Puede elegir configurar la configuración de preprocesadores por biblioteca de cliente o en todo el sistema.

* Agregar las propiedades de varios valores `cssProcessor` y `jsProcessor` en el nodo clientlibrary
* O defina la configuración predeterminada del sistema mediante la configuración OSGi **Administrador de bibliotecas de HTML**

Una configuración de preprocesador en el nodo clientlib tiene prioridad sobre la configuración OSGI.

#### Formato y ejemplos {#format-and-examples}

##### Formato {#format}

```javascript
config:= mode ":" processorName options*;
mode:= "default" | "min";
processorName := "none" | <name>;
options := ";" option;
option := name "=" value;
```

##### Compresor YUI para minificación de CSS y GCC para JS {#yui-compressor-for-css-minification-and-gcc-for-js}

```javascript
cssProcessor: ["default:none", "min:yui"]
jsProcessor: ["default:none", "min:gcc;compilationLevel=advanced"]
```

##### Escriba un script para preprocesar y luego GCC para minimizar y proteger {#typescript-to-preprocess-and-then-gcc-to-minify-and-obfuscate}

```javascript
jsProcessor: [
   "default:typescript",
   "min:typescript",
   "min:gcc;obfuscate=true"
]
```

##### Opciones adicionales de GCC {#additional-gcc-options}

```javascript
failOnWarning (defaults to "false")
languageIn (defaults to "ECMASCRIPT5")
languageOut (defaults to "ECMASCRIPT5")
compilationLevel (defaults to "simple") (can be "whitespace", "simple", "advanced")
```

Para obtener más información sobre las opciones de GCC, consulte [Documentación de GCC](https://developers.google.com/closure/compiler/docs/compilation_levels).

#### Establecer minificador predeterminado del sistema {#set-system-default-minifier}

AEM YUI se establece como el minificador predeterminado en la interfaz de usuario de. Para cambiar esto a GCC, siga estos pasos.

1. Vaya al Administrador de configuración de Apache Felix en (`http://<host>:<port/system/console/configMgr`)
1. Busque y edite el **Administrador de bibliotecas de Granite HTML de Adobe**.
1. Habilitar la opción **Minify** (si no está habilitada).
1. Establezca el valor **Configuraciones predeterminadas del procesador JS** en `min:gcc`.
   * Las opciones se pueden pasar si se separan con punto y coma, por ejemplo, `min:gcc;obfuscate=true`.
1. Haga clic en **Guardar** para guardar los cambios.
