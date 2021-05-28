---
title: Uso de bibliotecas del lado del cliente en AEM como Cloud Service
description: AEM proporciona carpetas de biblioteca del lado del cliente, que le permiten almacenar el código del lado del cliente (clientlibs) en el repositorio, organizarlo en categorías y definir cuándo y cómo se debe servir cada categoría de código al cliente
exl-id: 370db625-09bf-43fb-919d-4699edaac7c8
source-git-commit: 856266faf4cb99056b1763383d611e9b2c3c13ea
workflow-type: tm+mt
source-wordcount: '2561'
ht-degree: 0%

---

# Uso de bibliotecas del lado del cliente en AEM como Cloud Service {#using-client-side-libraries}

Las experiencias digitales dependen en gran medida del procesamiento del lado del cliente impulsado por código CSS y JavaScript complejo. AEM bibliotecas del lado del cliente (clientlibs) le permiten organizar y almacenar de forma centralizada estas bibliotecas del lado del cliente dentro del repositorio. Junto con el proceso de [compilación del front-end en el arquetipo de proyecto de AEM,](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/uifrontend.html) administrar el código del front-end para el proyecto de AEM se vuelve sencillo.

Las ventajas de usar clientlibs en AEM incluyen:

* El código del lado del cliente se almacena en el repositorio como el resto del código y el contenido de la aplicación
* Clientlibs en AEM puede agregar todos los CSS y JS en un archivo
* Exponga clientlibs a través de una ruta a la que se puede acceder a través de [Dispatcher](/help/implementing/dispatcher/disp-overview.md)
* Permite la reescritura de rutas para archivos o imágenes a los que se hace referencia

Clientlibs es la solución integrada para ofrecer CSS y Javascript desde AEM.

>[!TIP]
>
>Los desarrolladores de front-end que crean CSS y Javascript para AEM proyectos también deben familiarizarse con el [AEM tipo de archivo del proyecto y su proceso automatizado de compilación de front-end.](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/uifrontend.html)

## ¿Qué son las bibliotecas del lado del cliente {#what-are-clientlibs}

Los sitios requieren JavaScript y CSS, así como recursos estáticos como iconos y fuentes web, para que se procesen en el lado del cliente. Una clientlib es AEM mecanismo al que hacer referencia (por categoría si es necesario) y al que se sirven esos recursos.

AEM recopila el código CSS y el código Javascript del sitio en un solo archivo, en una ubicación central, para garantizar que solo se incluya una copia de cualquier recurso en la salida HTML. Esto maximiza la eficacia de la entrega y permite que esos recursos se mantengan centralmente en el repositorio a través de un proxy, lo que mantiene el acceso seguro.

## Desarrollo front-end para AEM como Cloud Service {#fed-for-aemaacs}

Todos los recursos JavaScript, CSS y otros recursos front-end deben mantenerse en el módulo [ui.frontend del tipo de archivo del proyecto AEM.](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/uifrontend.html) La flexibilidad del tipo de archivo le permite utilizar sus modernas herramientas web para crear y administrar estos recursos.

A continuación, el tipo de archivo puede compilar los recursos en archivos CSS y JS únicos, incrustándolos automáticamente en un `cq:clientLibraryFolder` en el repositorio.

## Estructura de carpetas de la biblioteca del cliente {#clientlib-folders}

Una carpeta de biblioteca del lado del cliente es un nodo de repositorio de tipo `cq:ClientLibraryFolder`. Su definición en [notación CND](https://jackrabbit.apache.org/node-type-notation.html) es

```text
[cq:ClientLibraryFolder] > sling:Folder
  - dependencies (string) multiple
  - categories (string) multiple
  - embed (string) multiple
  - channels (string) multiple
```

* `cq:ClientLibraryFolder` los nodos se pueden colocar en cualquier lugar dentro del  `/apps` subárbol del repositorio.
* Utilice la propiedad `categories` del nodo para identificar las categorías de biblioteca a las que pertenece.

Cada `cq:ClientLibraryFolder` se rellena con un conjunto de archivos JS y/o CSS, junto con algunos archivos de apoyo (ver a continuación). Las propiedades importantes de `cq:ClientLibraryFolder` se configuran de la siguiente manera:

* `allowProxy`: Dado que todas las clientlibs deben almacenarse en  `apps`, esta propiedad permite el acceso a clientlibrary a través del servlet proxy. Consulte [Localización de una carpeta de biblioteca de cliente y Uso del servlet ](#locating-a-client-library-folder-and-using-the-proxy-client-libraries-servlet) de bibliotecas de cliente proxy a continuación.
* `categories`: Identifica las categorías en las que  `cq:ClientLibraryFolder` se encuentra el conjunto de archivos JS o CSS dentro de este. La propiedad `categories`, que tiene varios valores, permite que una carpeta de biblioteca forme parte de más de una categoría (consulte a continuación cómo puede ser útil).

Si la carpeta de la biblioteca del cliente contiene uno o más archivos de origen que, durante la ejecución, se combinan en un solo archivo JS o CSS. El nombre del archivo generado es el nombre del nodo con la extensión de nombre de archivo `.js` o `.css`. Por ejemplo, el nodo de biblioteca llamado `cq.jquery` resulta en el archivo generado llamado `cq.jquery.js` o `cq.jquery.css`.

Las carpetas de la biblioteca de cliente contienen los siguientes elementos:

* Los archivos de origen JS o CSS
* Recursos estáticos que admiten estilos CSS, como iconos, fuentes web, etc.
* Un archivo `js.txt` o un archivo `css.txt` que identifique los archivos de origen que se combinarán en los archivos JS o CSS generados

![Arquitectura Clientlib](assets/clientlib-architecture.drawio.png)

## Creación de carpetas de biblioteca del lado del cliente {#creating-clientlib-folders}

Las bibliotecas de cliente deben encontrarse en `/apps`. Esto sirve para aislar mejor el código del contenido y la configuración.

Para que las bibliotecas de cliente en `/apps` sean accesibles, se utiliza un servidor proxy. Las ACL siguen aplicándose en la carpeta de la biblioteca del cliente, pero el servlet permite que el contenido se lea mediante `/etc.clientlibs/` si la propiedad `allowProxy` está establecida en `true`.

1. Abra el CRXDE Lite en un explorador web (`https://<host>:<port>/crx/de`).
1. Seleccione la carpeta `/apps` y haga clic en **Crear > Crear nodo**.
1. Introduzca un nombre para la carpeta de la biblioteca y, en la lista **Type**, seleccione `cq:ClientLibraryFolder`. Haga clic en **Aceptar** y, a continuación, haga clic en **Guardar todo**.
1. Para especificar la categoría o categorías a las que pertenece la biblioteca, seleccione el nodo `cq:ClientLibraryFolder`, añada la siguiente propiedad y, a continuación, haga clic en **Guardar todo**:
   * Nombre: `categories`
   * Tipo: Cadena
   * Valor: El nombre de la categoría
   * Varios: Seleccionado
1. Para que las bibliotecas de cliente sean accesibles a través del proxy en `/etc.clientlibs`, seleccione el nodo `cq:ClientLibraryFolder`, añada la siguiente propiedad y, a continuación, haga clic en **Guardar todo**:
   * Nombre: `allowProxy`
   * Tipo: Boolean (booleano)
   * Value: `true`
1. Si necesita administrar recursos estáticos, cree una subcarpeta denominada `resources` debajo de la carpeta de biblioteca del cliente.
   * Si almacena recursos estáticos en la carpeta `resources`, no se puede hacer referencia a ellos en una instancia de publicación.
1. Agregue archivos de origen a la carpeta de la biblioteca.
   * Esto lo suele hacer el proceso de compilación del front-end del [AEM tipo de archivo del proyecto.](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/uifrontend.html)
   * Si lo desea, puede organizar los archivos de origen en subcarpetas.
1. Seleccione la carpeta de la biblioteca del cliente y haga clic en **Crear > Crear archivo**.
1. En el cuadro de nombre de archivo, escriba uno de los siguientes nombres de archivo y haga clic en Aceptar:
   * **`js.txt`:** Utilice este nombre de archivo para generar un archivo JavaScript.
   * **`css.txt`:** Utilice este nombre de archivo para generar una hoja de estilo en cascada.
1. Abra el archivo y escriba el siguiente texto para identificar la raíz de la ruta de los archivos de origen:
   * `#base=*[root]*`
   * Reemplace `[root]` por la ruta de acceso a la carpeta que contiene los archivos de origen, en relación con el archivo TXT. Por ejemplo, use el siguiente texto cuando los archivos de origen estén en la misma carpeta que el archivo TXT:
      * `#base=.`
   * El siguiente código establece la raíz como la carpeta denominada mobile debajo del nodo `cq:ClientLibraryFolder`:
      * `#base=mobile`
1. En las líneas inferiores a `#base=[root]`, escriba las rutas de los archivos de origen relativas a la raíz. Coloque cada nombre de archivo en una línea independiente.
1. Haga clic en **Guardar todo**.

## Servir bibliotecas del lado del cliente {#serving-clientlibs}

Una vez que la carpeta de la biblioteca del cliente esté [configurada según sea necesario,](#creating-clientlib-folders) los clientlibs se pueden solicitar mediante proxy. Por ejemplo:

* Tiene una clientlib en `/apps/myproject/clientlibs/foo`
* Tiene una imagen estática en `/apps/myprojects/clientlibs/foo/resources/icon.png`

La propiedad `allowProxy` permite solicitar:

* La clientlib a través de j`/etc.clientlibs/myprojects/clientlibs/foo.js`
* La imagen estática a través de `/etc.clientlibs/myprojects/clientlibs/foo/resources/icon.png`

### Carga de bibliotecas de cliente mediante HTL {#loading-via-htl}

Una vez que los clientlibs se almacenan y administran correctamente en la carpeta de la biblioteca del cliente, se puede acceder a ellos a través de HTL.

Las bibliotecas de cliente se cargan a través de una plantilla de ayuda proporcionada por AEM, a la que se puede acceder mediante `data-sly-use`. Las plantillas de ayuda están disponibles en este archivo, al que se puede llamar mediante `data-sly-call`.

Cada plantilla de ayuda espera una opción `categories` para hacer referencia a las bibliotecas de cliente deseadas. Esa opción puede ser una matriz de valores de cadena o una cadena que contenga una lista de valores separados por comas.

[Consulte la ](https://experienceleague.adobe.com/docs/experience-manager-htl/using/getting-started/getting-started.html#loading-client-libraries) documentación de HTL para obtener más información sobre cómo cargar clientlibs a través de HTL.

<!--
### Setting Cache Timestamps {#setting-cache-timestamps}

This is possible. Still need detail.
-->

## Bibliotecas de cliente en Author y Publicar {#clientlibs-author-publish}

La mayoría de clientlibs serán necesarios en la instancia de publicación de AEM. Es decir, la mayoría de los objetivos de clientlibs son producir la experiencia del usuario final del contenido. Para clientlibs en instancias de publicación, [front-end build tools](#fed-for-aemaacs) se puede usar e implementar a través de [carpetas de biblioteca de cliente como se describe anteriormente.](#creating-clientlib-folders)

Sin embargo, en ocasiones pueden ser necesarias bibliotecas de cliente para personalizar la experiencia de creación. Por ejemplo, la personalización de un cuadro de diálogo puede requerir la implementación de pequeños bits de CSS o JS en la instancia de creación de AEM.

### Administración de bibliotecas de cliente en Author {#clientlibs-on-author}

Si necesita utilizar bibliotecas de cliente en author, puede crear sus bibliotecas de cliente en `/apps` utilizando los mismos métodos que para publicar, pero escribirlas directamente en `/apps/.../clientlibs/foo` en lugar de crear un proyecto completo para administrarlo.

A continuación, puede &quot;conectar&quot; al JS de creación añadiendo las bibliotecas de cliente a una categoría de biblioteca de cliente predeterminada.

## Herramientas de depuración {#debugging-tools}

AEM proporciona varias herramientas para depurar y probar carpetas de biblioteca de cliente.

### Descubra las bibliotecas de cliente {#discover-client-libraries}

El componente `/libs/cq/granite/components/dumplibs/dumplibs` genera una página de información sobre todas las carpetas de la biblioteca del cliente en el sistema. El nodo `/libs/granite/ui/content/dumplibs` tiene el componente como tipo de recurso. Para abrir la página, use la siguiente dirección URL (cambie el host y el puerto según sea necesario):

`https://<host>:<port>/libs/granite/ui/content/dumplibs.test.html`

La información incluye la ruta y el tipo de biblioteca (CSS o JS), así como los valores de los atributos de biblioteca, como las categorías y dependencias. Las tablas posteriores de la página muestran las bibliotecas de cada categoría y canal.

### Consulte Salida generada {#see-generated-output}

El componente `dumplibs` incluye un selector de prueba que muestra el código fuente generado para las etiquetas `ui:includeClientLib`. La página incluye código para diferentes combinaciones de js, css y atributos temáticos.

1. Utilice uno de los métodos siguientes para abrir la página Salida de prueba :
   * En la página `dumplibs.html`, haga clic en el vínculo del texto **Haga clic aquí para probar los resultados**.
   * Abra la siguiente URL en su explorador web (use un host y puerto diferentes según sea necesario):
      * `http://<host>:<port>/libs/granite/ui/content/dumplibs.html`
   * La página predeterminada muestra resultados para etiquetas sin valor para el atributo categories .
1. Para ver el resultado de una categoría, escriba el valor de la propiedad `categories` de la biblioteca del cliente y haga clic en **Submit Query**.

## Funciones adicionales de la carpeta de la biblioteca de cliente {#additional-features}

Hay otras funciones que son compatibles con las carpetas de biblioteca de cliente en AEM. Sin embargo, no son necesarios en AEM como Cloud Service y, como tal, se desaconseja su uso. Se enumeran aquí para que sean completas.

>[!WARNING]
>
>Estas funciones adicionales de las carpetas de la biblioteca del cliente no son necesarias en AEM como Cloud Service y, como tal, se desaconseja su uso. Se enumeran aquí para que sean completas.

### Adobe Granite HTML LIbrary Manager {#html-library-manager}

Se pueden controlar configuraciones adicionales de la biblioteca del cliente mediante el **Administrador de bibliotecas HTML de Granite de Adobe** panel de la consola del sistema en `https://<host>:<port>/system/console/configMgr`).

### Propiedades de carpeta adicionales {#additional-folder-properties}

Las propiedades de carpeta adicionales incluyen el control de dependencias e incrustaciones, pero generalmente ya no son necesarias y se desaconseja su uso:

* `dependencies`: Esta es una lista de otras categorías de biblioteca de cliente de las que depende esta carpeta de biblioteca. Por ejemplo, dados dos nodos `cq:ClientLibraryFolder` `F` y `G`, si un archivo en `F` requiere otro archivo en `G` para funcionar correctamente, al menos uno de los `categories` de `G` debe estar entre los `dependencies` de `F`.
* `embed`: Se utiliza para incrustar código de otras bibliotecas. Si el nodo `F` incrusta los nodos `G` y `H`, el HTML resultante será una concatenación de contenido de los nodos `G` y `H`.

### Vinculación a dependencias {#linking-to-dependencies}

Cuando el código de la carpeta de la biblioteca de cliente haga referencia a otras bibliotecas, identifique las demás bibliotecas como dependencias. La etiqueta `ui:includeClientLib` que hace referencia a la carpeta de la biblioteca del cliente hace que el código HTML incluya un vínculo al archivo de biblioteca generado, así como las dependencias.

Las dependencias deben ser otro `cq:ClientLibraryFolder`. Para identificar dependencias, agregue una propiedad al nodo `cq:ClientLibraryFolder` con los atributos siguientes:

* **Nombre:** dependencias
* **Tipo:** String[]
* **Valores:** El valor de la propiedad categories del nodo cq:ClientLibraryFolder del que depende la carpeta de biblioteca actual.

Por ejemplo, el `/etc/clientlibs/myclientlibs/publicmain` tiene una dependencia de la biblioteca `cq.jquery`. La página que hace referencia a la biblioteca de cliente principal genera un HTML que incluye el siguiente código:

```xml
<script src="/etc/clientlibs/foundation/cq.jquery.js" type="text/javascript">
<script src="/etc/clientlibs/mylibs/publicmain.js" type="text/javascript">
```

### Incrustación de código desde otras bibliotecas {#embedding-code-from-other-libraries}

Puede incrustar código de una biblioteca de cliente en otra biblioteca de cliente. Durante el tiempo de ejecución, los archivos JS y CSS generados de la biblioteca de incrustación incluyen el código de la biblioteca incrustada.

La incrustación de código es útil para proporcionar acceso a las bibliotecas almacenadas en áreas seguras del repositorio.

#### Carpetas de biblioteca de cliente específicas de la aplicación {#app-specific-client-library-folders}

Se recomienda mantener todos los archivos relacionados con la aplicación en su carpeta de aplicación debajo de `/app`. También se recomienda denegar el acceso a la carpeta `/app` a los visitantes del sitio web. Para satisfacer ambas prácticas recomendadas, cree una carpeta de biblioteca de cliente debajo de la carpeta `/etc` que incrusta la biblioteca de cliente que se encuentra debajo de `/app`.

Utilice la propiedad categories para identificar la carpeta de biblioteca de cliente que desea incrustar. Para incrustar la biblioteca, agregue una propiedad al nodo `cq:ClientLibraryFolder` de incrustación mediante los siguientes atributos de propiedad:

* **Nombre:** incrustar
* **Tipo:** String[]
* **Valor:** el valor de la propiedad categories del  `cq:ClientLibraryFolder` nodo que se va a incrustar.

#### Usar la incrustación para minimizar las solicitudes {#using-embedding-to-minimize-requests}

En algunos casos, es posible que el HTML final generado para la página típica por la instancia de publicación incluya un número relativamente grande de elementos `<script>`.

En estos casos, puede resultar útil combinar todo el código de biblioteca de cliente necesario en un solo archivo para reducir el número de solicitudes de retorno y de adelante al cargar la página. Para ello, puede `embed` las bibliotecas necesarias en su biblioteca de cliente específica de la aplicación mediante la propiedad embed del nodo `cq:ClientLibraryFolder`.

#### Rutas en archivos CSS {#paths-in-css-files}

Al incrustar archivos CSS, el código CSS generado utiliza rutas a los recursos que son relativas a la biblioteca de incrustación. Por ejemplo, la biblioteca de acceso público `/etc/client/libraries/myclientlibs/publicmain` incrusta la biblioteca de cliente `/apps/myapp/clientlib`:

El archivo `main.css` contiene el siguiente estilo:

```javascript
body {
  padding: 0;
  margin: 0;
  background: url(images/bg-full.jpg) no-repeat center top;
  width: 100%;
}
```

El archivo CSS que genera el nodo `publicmain` contiene el siguiente estilo, utilizando la URL de la imagen original:

```javascript
body {
  padding: 0;
  margin: 0;
  background: url(../../../apps/myapp/clientlib/styles/images/bg-full.jpg) no-repeat center top;
  width: 100%;
}
```

#### Consulte Archivos incrustados en salida HTML {#see-embedded-files}

Para rastrear el origen del código incrustado o para asegurarse de que las bibliotecas de cliente incrustadas producen los resultados esperados, puede ver los nombres de los archivos que se están incrustando durante la ejecución. Para ver los nombres de los archivos, añada el parámetro `debugClientLibs=true` a la dirección URL de la página web. La biblioteca que se genera contiene instrucciones `@import` en lugar del código incrustado.

En el ejemplo de la sección anterior [Código de incrustación de otras bibliotecas](#embedding-code-from-other-libraries), la carpeta de biblioteca de cliente `/etc/client/libraries/myclientlibs/publicmain` incrusta la carpeta de biblioteca de cliente `/apps/myapp/clientlib`. Añadir el parámetro a la página web produce el siguiente vínculo en el código fuente de la página web:

```xml
<link rel="stylesheet" href="/etc/clientlibs/mycientlibs/publicmain.css">
```

Al abrir el archivo `publicmain.css` se muestra el siguiente código:

```javascript
@import url("/apps/myapp/clientlib/styles/main.css");
```

1. En el cuadro de dirección de su explorador web, añada el siguiente texto a la dirección URL del HTML:
   * `?debugClientLibs=true`
1. Cuando se carga la página, vea el origen de la página.
1. Haga clic en el vínculo que se proporciona como href para que el elemento del vínculo abra el archivo y vea el código fuente.

### Uso de preprocesadores {#using-preprocessors}

AEM permite preprocesadores y envíos conectables con compatibilidad con [YUI Compressor](https://github.com/yui/yuicompressor#yui-compressor---the-yahoo-javascript-and-css-compressor) para CSS y JavaScript y [Google Closure Compiler (GCC)](https://developers.google.com/closure/compiler/) para JavaScript con YUI establecido como preprocesador predeterminado AEM.

Los preprocesadores conectables permiten un uso flexible, que incluye:

* Definición de procesadores de secuencias de comandos que pueden procesar orígenes de secuencias de comandos
* Los procesadores son configurables con opciones
* Los procesadores pueden utilizarse para la minificación, pero también para casos no minificados
* La clientlib puede definir qué procesador utilizar

>[!NOTE]
>
>De forma predeterminada, AEM utiliza el compresor YUI. Consulte la [documentación de GitHub del compresor YUI](https://github.com/yui/yuicompressor/issues) para obtener una lista de los problemas conocidos. Cambiar al compresor GCC para clientlibs particulares puede resolver algunos problemas observados al usar YUI.

>[!CAUTION]
>
>No coloque una biblioteca minimizada en una biblioteca cliente. En su lugar, proporcione la biblioteca sin procesar y, si es necesario minificar, utilice las opciones de los preprocesadores.

#### Uso {#usage}

Puede elegir configurar la configuración de los preprocesadores por clientlibrary o por todo el sistema.

* Agregue las propiedades de multivalor `cssProcessor` y `jsProcessor` en el nodo clientlibrary
* O bien, defina la configuración predeterminada del sistema a través de la configuración OSGi del **Administrador de biblioteca HTML**

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

##### Compresor YUI para la minificación de CSS y GCC para JS {#yui-compressor-for-css-minification-and-gcc-for-js}

```javascript
cssProcessor: ["default:none", "min:yui"]
jsProcessor: ["default:none", "min:gcc;compilationLevel=advanced"]
```

##### Escrito previamente y luego GCC para minimizar y ofuscar {#typescript-to-preprocess-and-then-gcc-to-minify-and-obfuscate}

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

Para obtener más información sobre las opciones de GCC, consulte la [documentación de GCC](https://developers.google.com/closure/compiler/docs/compilation_levels).

#### Definir minificador predeterminado del sistema {#set-system-default-minifier}

YUI se establece como minificador predeterminado en AEM. Para cambiar esto a GCC, siga estos pasos.

1. Vaya al Administrador de configuración de Apache Felix en (`http://<host>:<portY/system/console/configMgr`)
1. Busque y edite el **Adobe Granite HTML Library Manager**.
1. Active la opción **Minify** (si no está activada).
1. Establezca el valor **JS Processor Default Configs** en `min:gcc`.
   * Las opciones se pueden pasar si se separan con un punto y coma, por ejemplo `min:gcc;obfuscate=true`.
1. Haga clic en **Guardar** para guardar los cambios.
