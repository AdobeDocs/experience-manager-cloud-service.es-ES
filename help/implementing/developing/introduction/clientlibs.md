---
title: Uso de las bibliotecas del lado del cliente en AEM como Cloud Service
description: AEM proporciona Carpetas de biblioteca del lado del cliente, que le permiten almacenar el código del lado del cliente (clientlibs) en el repositorio, organizarlo en categorías y definir cuándo y cómo se debe proporcionar cada categoría de código al cliente
translation-type: tm+mt
source-git-commit: d4c031e17c0c83e44b687474502252c89ed37922
workflow-type: tm+mt
source-wordcount: '2571'
ht-degree: 1%

---


# Uso de las bibliotecas del lado del cliente en AEM como Cloud Service {#using-client-side-libraries}

Las experiencias digitales dependen en gran medida del procesamiento del lado del cliente impulsado por código CSS y JavaScript complejo. AEM bibliotecas del lado del cliente (clientlibs) le permiten organizar y almacenar centralmente estas bibliotecas del lado del cliente dentro del repositorio. Junto con el [proceso de generación de front-end en el arquetipo de proyecto de AEM,](https://docs.adobe.com/content/help/es-ES/experience-manager-core-components/using/developing/archetype/uifrontend.html) administrar el código de front-end para el proyecto de AEM resulta sencillo.

Las ventajas de usar clientlibs en AEM incluyen:

* El código del lado del cliente se almacena en el repositorio como el resto del código y el contenido de la aplicación
* Los clientes de AEM pueden acumulados todos los CSS y JS en un solo archivo
* Exponga clientlibs mediante una ruta a la que se pueda acceder a través del [despachante](/help/implementing/dispatcher/disp-overview.md)
* Permite la reescritura de rutas para archivos o imágenes a los que se hace referencia

Clientlibs es la solución integrada para ofrecer CSS y Javascript desde AEM.

>[!TIP]
>
>Los desarrolladores de front-end que crean CSS y Javascript para AEM proyectos también deben familiarizarse con el [AEM arquetipo del proyecto y su proceso automatizado de generación de front-end.](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/developing/archetype/uifrontend.html)

## ¿Qué son las bibliotecas del lado del cliente {#what-are-clientlibs}?

Los sitios requieren JavaScript y CSS, así como recursos estáticos, como iconos y fuentes web, para que se procesen en el lado del cliente. Una clientlib es AEM mecanismo de referencia (por categoría si es necesario) y sirve a esos recursos.

AEM recopila el código CSS y Javascript del sitio en un único archivo, en una ubicación central, para garantizar que solo se incluya una copia de cualquier recurso en la salida HTML. Esto maximiza la eficacia del envío y permite que esos recursos se mantengan centralmente en el repositorio mediante proxy, manteniendo el acceso seguro.

## Desarrollo front-end para AEM como Cloud Service {#fed-for-aemaacs}

Todos los recursos de JavaScript, CSS y otros recursos front-end deben mantenerse en el módulo [ui.front del arquetipo del proyecto AEM.](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/developing/archetype/uifrontend.html) La flexibilidad del arquetipo le permite utilizar sus modernas herramientas web para crear y administrar estos recursos.

A continuación, el arquetipo puede compilar los recursos en archivos CSS y JS únicos, incorporándolos automáticamente en un `cq:clientLibraryFolder` del repositorio.

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

Cada `cq:ClientLibraryFolder` se rellena con un conjunto de archivos JS y/o CSS, junto con algunos archivos de soporte (ver más abajo). Las propiedades importantes de `cq:ClientLibraryFolder` se configuran de la siguiente manera:

* `allowProxy`:: Dado que todos los clientes deben almacenarse en  `apps`, esta propiedad permite el acceso a clientlibrary mediante servlet proxy. Consulte [Localización de una carpeta de biblioteca de cliente y Uso del servlet de bibliotecas de cliente proxy](#locating-a-client-library-folder-and-using-the-proxy-client-libraries-servlet) a continuación.
* `categories`:: Identifica las categorías en las que  `cq:ClientLibraryFolder` cae el conjunto de archivos JS y/o CSS. La propiedad `categories`, que tiene varios valores, permite que una carpeta de biblioteca forme parte de más de una categoría (vea a continuación cómo puede resultar útil).

Si la carpeta de la biblioteca del cliente contiene uno o varios archivos de origen que, en tiempo de ejecución, se combinan en un único archivo JS y/o CSS. El nombre del archivo generado es el nombre del nodo con la extensión de nombre de archivo `.js` o `.css`. Por ejemplo, el nodo de biblioteca llamado `cq.jquery` resulta en el archivo generado llamado `cq.jquery.js` o `cq.jquery.css`.

Las carpetas de la biblioteca del cliente contienen los siguientes elementos:

* Los archivos de origen JS y/o CSS
* Recursos estáticos que admiten estilos CSS, como iconos, fuentes web, etc.
* Un archivo `js.txt` y/o un archivo `css.txt` que identifique los archivos de origen que se van a combinar en los archivos JS o CSS generados

![Arquitectura de Clientlib](assets/clientlib-architecture.drawio.png)

## Creación de carpetas de bibliotecas de cliente {#creating-clientlib-folders}

Las bibliotecas de cliente deben ubicarse en `/apps`. Esto sirve para aislar mejor el código del contenido y la configuración.

Para que las bibliotecas cliente bajo `/apps` sean accesibles, se utiliza un servidor proxy. Las ACL aún se aplican en la carpeta de la biblioteca del cliente, pero el servlet permite que el contenido se lea mediante `/etc.clientlibs/` si la propiedad `allowProxy` se establece en `true`.

1. Abra el CRXDE Lite en un explorador web (`https://<host>:<port>/crx/de`).
1. Seleccione la carpeta `/apps` y haga clic en **Crear > Crear nodo**.
1. Escriba un nombre para la carpeta de la biblioteca y, en la lista **Tipo**, seleccione `cq:ClientLibraryFolder`. Haga clic en **Aceptar** y, a continuación, haga clic en **Guardar todo**.
1. Para especificar la categoría o categorías a las que pertenece la biblioteca, seleccione el nodo `cq:ClientLibraryFolder`, agregue la siguiente propiedad y haga clic en **Guardar todo**:
   * Nombre: `categories`
   * Tipo: Cadena
   * Valor: El nombre de la categoría
   * Múltiple: Seleccionado
1. Para que las bibliotecas cliente sean accesibles mediante proxy en `/etc.clientlibs`, seleccione el nodo `cq:ClientLibraryFolder`, agregue la siguiente propiedad y haga clic en **Guardar todo**:
   * Nombre: `allowProxy`
   * Tipo: Boolean (booleano)
   * Value: `true`
1. Si necesita administrar recursos estáticos, cree una subcarpeta con el nombre `resources` debajo de la carpeta de la biblioteca del cliente.
   * Si almacena recursos estáticos en la carpeta `resources`, no se puede hacer referencia a ellos en una instancia de publicación.
1. Añada los archivos de origen a la carpeta de la biblioteca.
   * Esto generalmente se realiza mediante el proceso de compilación front-end del arquetipo de proyecto [AEM.](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/developing/archetype/uifrontend.html)
   * Si lo desea, puede organizar los archivos de origen en subcarpetas.
1. Seleccione la carpeta de la biblioteca del cliente y haga clic en **Crear > Crear archivo**.
1. En el cuadro Nombre de archivo, escriba uno de los siguientes nombres de archivo y haga clic en Aceptar:
   * **`js.txt`:** Utilice este nombre de archivo para generar un archivo JavaScript.
   * **`css.txt`:** Utilice este nombre de archivo para generar una hoja de estilo en cascada.
1. Abra el archivo y escriba el siguiente texto para identificar la raíz de la ruta de los archivos de origen:
   * `#base=*[root]*`
   * Reemplace `[root]` por la ruta de la carpeta que contiene los archivos de origen, en relación con el archivo TXT. Por ejemplo, utilice el siguiente texto cuando los archivos de origen estén en la misma carpeta que el archivo TXT:
      * `#base=.`
   * El siguiente código establece la raíz como la carpeta denominada mobile debajo del nodo `cq:ClientLibraryFolder`:
      * `#base=mobile`
1. En las líneas siguientes `#base=[root]`, escriba las rutas de los archivos de origen relativas a la raíz. Coloque cada nombre de archivo en una línea independiente.
1. Haga clic en **Guardar todo**.

## Servicio de bibliotecas del lado del cliente {#serving-clientlibs}

Una vez configurada la carpeta de la biblioteca de cliente [según sea necesario,](#creating-clientlib-folders) los clientes pueden solicitarse mediante proxy. Como ejemplo:

* Tiene una clientlib en `/apps/myproject/clientlibs/foo`
* Tiene una imagen estática en `/apps/myprojects/clientlibs/foo/resources/icon.png`

La propiedad `allowProxy` le permite solicitar:

* La clientlib a través de j`/etc.clientlibs/myprojects/clientlibs/foo.js`
* La imagen estática mediante `/etc.clientlibs/myprojects/clientlibs/foo/resources/icon.png`

### Cargando bibliotecas de clientes mediante HTL {#loading-via-htl}

Una vez que los clientes se almacenan y administran correctamente en la carpeta de la biblioteca del cliente, se puede acceder a ellos a través de HTL.

Las bibliotecas cliente se cargan mediante una plantilla de ayuda proporcionada por AEM, a la que se puede acceder a través de `data-sly-use`. Las plantillas de ayuda están disponibles en este archivo, al que se puede llamar a través de `data-sly-call`.

Cada plantilla de ayuda espera una opción `categories` para hacer referencia a las bibliotecas de cliente deseadas. Esa opción puede ser una matriz de valores de cadena o una cadena que contenga una lista de valores separados por comas.

[Consulte la ](https://docs.adobe.com/content/help/en/experience-manager-htl/using/getting-started/getting-started.html#loading-client-libraries) documentación de HTL para obtener más información sobre cómo cargar clientes a través de HTL.

<!--
### Setting Cache Timestamps {#setting-cache-timestamps}

This is possible. Still need detail.
-->

## Bibliotecas de clientes en Autor y Publicación {#clientlibs-author-publish}

La mayoría de los clientes serán obligatorios en la instancia de publicación de AEM. Es decir, la mayoría de los objetivos de clientlibs son producir la experiencia del usuario final del contenido. Para clientlibs en instancias de publicación, [herramientas de compilación front-end](#fed-for-aemaacs) se pueden utilizar e implementar mediante [carpetas de biblioteca de cliente como se describe anteriormente.](#creating-clientlib-folders)

Sin embargo, en algunas ocasiones es posible que las bibliotecas de cliente sean necesarias para personalizar la experiencia de creación. Por ejemplo, la personalización de un cuadro de diálogo puede requerir la implementación de pequeños fragmentos de CSS o JS en la instancia de creación de AEM.

### Administración de bibliotecas de cliente en el autor {#clientlibs-on-author}

Si necesita utilizar bibliotecas de cliente en el autor, puede crear sus bibliotecas de cliente en `/apps` utilizando los mismos métodos que para la publicación, pero escribirlas directamente en `/apps/.../clientlibs/foo` en lugar de crear un proyecto completo para administrarlo.

A continuación, puede &quot;conectar&quot; a la JS de creación agregando las bibliotecas de cliente a una categoría de biblioteca de cliente lista para usar.

## Herramientas de depuración {#debugging-tools}

AEM proporciona varias herramientas para depurar y probar las carpetas de la biblioteca del cliente.

### Bibliotecas de clientes de Discover {#discover-client-libraries}

El componente `/libs/cq/granite/components/dumplibs/dumplibs` genera una página de información sobre todas las carpetas de la biblioteca de cliente del sistema. El nodo `/libs/granite/ui/content/dumplibs` tiene el componente como tipo de recurso. Para abrir la página, utilice la siguiente URL (cambiando el host y el puerto según sea necesario):

`https://<host>:<port>/libs/granite/ui/content/dumplibs.test.html`

La información incluye la ruta y el tipo de biblioteca (CSS o JS), así como los valores de los atributos de la biblioteca, como categorías y dependencias. Las tablas posteriores de la página muestran las bibliotecas de cada categoría y canal.

### Consulte Salida generada {#see-generated-output}

El componente `dumplibs` incluye un selector de prueba que muestra el código fuente que se genera para las etiquetas `ui:includeClientLib`. La página incluye código para diferentes combinaciones de js, css y atributos temáticos.

1. Utilice uno de los siguientes métodos para abrir la página Resultados de la prueba:
   * En la página `dumplibs.html`, haga clic en el vínculo del texto **Haga clic aquí para probar el resultado**.
   * Abra la siguiente URL en el explorador web (utilice un host y puerto diferentes según sea necesario):
      * `http://<host>:<port>/libs/granite/ui/content/dumplibs.html`
   * La página predeterminada muestra el resultado de las etiquetas sin valor para el atributo categorías.
1. Para ver el resultado de una categoría, escriba el valor de la propiedad `categories` de la biblioteca del cliente y haga clic en **Enviar Consulta**.

## Características adicionales de la carpeta de la biblioteca del cliente {#additional-features}

Hay otras funciones que son compatibles con las carpetas de la biblioteca del cliente en AEM. Sin embargo, no se requieren en AEM como Cloud Service y, como tal, se desaconseja su uso. Se enumeran aquí para obtener información completa.

>[!WARNING]
>
>Estas funciones adicionales de las carpetas de la biblioteca de clientes no son necesarias en AEM como Cloud Service y, por lo tanto, se desaconseja su uso. Se enumeran aquí para obtener información completa.

### Adobe Granite HTML LIbrary Manager {#html-library-manager}

La configuración adicional de la biblioteca del cliente se puede controlar mediante el **Administrador de biblioteca HTML de Adobe Granite** panel de la Consola del sistema en `https://<host>:<port>/system/console/configMgr`).

### Propiedades de carpeta adicionales {#additional-folder-properties}

Las propiedades de carpeta adicionales incluyen permitir el control de dependencias e incrustaciones, pero generalmente ya no son necesarias y se desaconseja su uso:

* `dependencies`:: Esta es una lista de otras categorías de la biblioteca de cliente de las que depende esta carpeta de biblioteca. Por ejemplo: dados dos `cq:ClientLibraryFolder` nodos `F` y `G`, si un archivo en `F` requiere otro archivo en `G` para funcionar correctamente, al menos uno de los `categories` de `G` debe estar entre los `dependencies` de `F`.
* `embed`:: Se utiliza para incrustar código de otras bibliotecas. Si el nodo `F` incrusta nodos `G` y `H`, el HTML resultante será una concatenación de contenido de los nodos `G` y `H`.

### Vinculación a dependencias {#linking-to-dependencies}

Cuando el código de la carpeta de la biblioteca del cliente haga referencia a otras bibliotecas, identifique las demás bibliotecas como dependencias. La etiqueta `ui:includeClientLib` que hace referencia a la carpeta de la biblioteca de cliente hace que el código HTML incluya un vínculo al archivo de biblioteca generado, así como las dependencias.

Las dependencias deben ser otro `cq:ClientLibraryFolder`. Para identificar dependencias, agregue una propiedad al nodo `cq:ClientLibraryFolder` con los atributos siguientes:

* **Nombre:** dependencias
* **Tipo:** Cadena[]
* **Valores:** el valor de la propiedad categorías del nodo cq:ClientLibraryFolder del que depende la carpeta de biblioteca actual.

Por ejemplo, `/etc/clientlibs/myclientlibs/publicmain` tiene una dependencia en la biblioteca `cq.jquery`. La página que hace referencia a la biblioteca principal del cliente genera HTML que incluye el siguiente código:

```xml
<script src="/etc/clientlibs/foundation/cq.jquery.js" type="text/javascript">
<script src="/etc/clientlibs/mylibs/publicmain.js" type="text/javascript">
```

### Incrustación de código desde otras bibliotecas {#embedding-code-from-other-libraries}

Puede incrustar código de una biblioteca de cliente en otra biblioteca de cliente. En tiempo de ejecución, los archivos JS y CSS generados de la biblioteca de incrustación incluyen el código de la biblioteca incrustada.

La incrustación de código es útil para proporcionar acceso a bibliotecas almacenadas en áreas seguras del repositorio.

#### Carpetas de biblioteca de cliente específicas de la aplicación {#app-specific-client-library-folders}

Se recomienda mantener todos los archivos relacionados con la aplicación en la carpeta de la aplicación por debajo de `/app`. También se recomienda denegar el acceso de los visitantes del sitio Web a la carpeta `/app`. Para cumplir ambas prácticas recomendadas, cree una carpeta de biblioteca de cliente debajo de la carpeta `/etc` que incrusta la biblioteca de cliente que se encuentra por debajo de `/app`.

Utilice la propiedad categorías para identificar la carpeta de biblioteca de cliente que desea incrustar. Para incrustar la biblioteca, agregue una propiedad al nodo `cq:ClientLibraryFolder` de incrustación mediante los atributos de propiedad siguientes:

* **Nombre:** embed
* **Tipo:** Cadena[]
* **Valor:** el valor de la propiedad categorías del  `cq:ClientLibraryFolder` nodo que se va a incrustar.

#### Uso de la incrustación para minimizar solicitudes {#using-embedding-to-minimize-requests}

En algunos casos, es posible que el HTML final generado para una página típica por la instancia de publicación incluya un número relativamente grande de elementos `<script>`.

En estos casos, puede resultar útil combinar todo el código de biblioteca de cliente necesario en un solo archivo para reducir el número de solicitudes de retorno y de avance al cargar la página. Para ello, puede `embed` las bibliotecas necesarias en la biblioteca de cliente específica de la aplicación mediante la propiedad embed del nodo `cq:ClientLibraryFolder`.

#### Rutas en archivos CSS {#paths-in-css-files}

Al incrustar archivos CSS, el código CSS generado utiliza rutas a los recursos que son relativas a la biblioteca de incrustación. Por ejemplo, la biblioteca accesible al público `/etc/client/libraries/myclientlibs/publicmain` incrusta la biblioteca de cliente `/apps/myapp/clientlib`:

El archivo `main.css` contiene el siguiente estilo:

```javascript
body {
  padding: 0;
  margin: 0;
  background: url(images/bg-full.jpg) no-repeat center top;
  width: 100%;
}
```

El archivo CSS que genera el nodo `publicmain` contiene el siguiente estilo, utilizando la dirección URL de la imagen original:

```javascript
body {
  padding: 0;
  margin: 0;
  background: url(../../../apps/myapp/clientlib/styles/images/bg-full.jpg) no-repeat center top;
  width: 100%;
}
```

#### Consulte Archivos incrustados en salida HTML {#see-embedded-files}

Para rastrear el origen de código incrustado o para asegurarse de que las bibliotecas de cliente incrustadas están produciendo los resultados esperados, puede ver los nombres de los archivos que se incrustan durante la ejecución. Para ver los nombres de archivo, anexe el parámetro `debugClientLibs=true` a la dirección URL de la página web. La biblioteca que se genera contiene `@import` instrucciones en lugar del código incrustado.

En el ejemplo de la sección anterior [Incrustar código de otras bibliotecas](#embedding-code-from-other-libraries), la carpeta de biblioteca de cliente `/etc/client/libraries/myclientlibs/publicmain` incrusta la carpeta de biblioteca de cliente `/apps/myapp/clientlib`. La adición del parámetro a la página web produce el siguiente vínculo en el código fuente de la página web:

```xml
<link rel="stylesheet" href="/etc/clientlibs/mycientlibs/publicmain.css">
```

Al abrir el archivo `publicmain.css` se muestra el siguiente código:

```javascript
@import url("/apps/myapp/clientlib/styles/main.css");
```

1. En el cuadro de dirección del navegador web, anexe el siguiente texto a la dirección URL del HTML:
   * `?debugClientLibs=true`
1. Cuando se cargue la página, vista el origen de la página.
1. Haga clic en el vínculo que se proporciona como href para que el elemento link abra el archivo y vista el código fuente.

### Uso de preprocesadores {#using-preprocessors}

AEM permite preprocesadores y envíos conectables con compatibilidad con [YUI Compressor](https://github.com/yui/yuicompressor#yui-compressor---the-yahoo-javascript-and-css-compressor) para CSS y JavaScript y [Google Closure Compiler (GCC)](https://developers.google.com/closure/compiler/) para JavaScript con YUI definido como AEM preprocesador predeterminado.

Los preprocesadores conectables permiten un uso flexible que incluye:

* Definición de procesadores de secuencias de comandos que pueden procesar orígenes de secuencias de comandos
* Los procesadores son configurables con opciones
* Los procesadores se pueden utilizar para la minimización, pero también para casos no minimizados
* La clientlib puede definir qué procesador utilizar

>[!NOTE]
>
>De forma predeterminada, AEM utiliza el Compresor YUI. Consulte la [documentación de GitHub del Compresor YUI](https://github.com/yui/yuicompressor/issues) para obtener una lista de los problemas conocidos. Cambiar al compresor GCC para clientes particulares puede resolver algunos problemas observados al usar YUI.

>[!CAUTION]
>
>No coloque una biblioteca minimizada en una biblioteca de cliente. En su lugar, proporcione la biblioteca sin procesar y, si se requiere la minimización, utilice las opciones de los preprocesadores.

#### Uso {#usage}

Puede configurar la configuración de preprocesadores por biblioteca de clientes o por todo el sistema.

* Añada las propiedades de varios valores `cssProcessor` y `jsProcessor` en el nodo clientlibrary
* O defina la configuración predeterminada del sistema mediante la configuración OSGi de **Administrador de biblioteca HTML**

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

##### Compresor YUI para la minimización de CSS y GCC para JS {#yui-compressor-for-css-minification-and-gcc-for-js}

```javascript
cssProcessor: ["default:none", "min:yui"]
jsProcessor: ["default:none", "min:gcc;compilationLevel=advanced"]
```

##### Escritura para preprocesar y luego GCC para minimizar y ocultar {#typescript-to-preprocess-and-then-gcc-to-minify-and-obfuscate}

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

Para obtener más información sobre las opciones del CCG, consulte la [documentación del CCG](https://developers.google.com/closure/compiler/docs/compilation_levels).

#### Definir el minificador predeterminado del sistema {#set-system-default-minifier}

La IU se establece como el minificador predeterminado en AEM. Para cambiar esto a GCC, siga estos pasos.

1. Vaya al Administrador de configuración Apache Felix en (`http://<host>:<portY/system/console/configMgr`)
1. Busque y edite el **Administrador de biblioteca HTML de Adobe Granite**.
1. Habilite la opción **Minificar** (si no está habilitada).
1. Establezca el valor **Configuraciones predeterminadas del procesador JS** en `min:gcc`.
   * Las opciones se pueden pasar si se separan con un punto y coma, por ejemplo `min:gcc;obfuscate=true`.
1. Haga clic en **Guardar** para guardar los cambios.
