---
title: AEM as a Cloud Service Uso de bibliotecas del lado del cliente en el uso de
description: AEM proporciona Carpetas de biblioteca del lado del cliente, que le permiten almacenar el código del lado del cliente (clientlibs) en el repositorio, organizarlo en categorías y definir cuándo y cómo se debe servir cada categoría de código al cliente
exl-id: 370db625-09bf-43fb-919d-4699edaac7c8
source-git-commit: 6bb7b2d056d501d83cf227adb239f7f40f87d0ce
workflow-type: tm+mt
source-wordcount: '2551'
ht-degree: 2%

---


# AEM as a Cloud Service Uso de bibliotecas del lado del cliente en el uso de {#using-client-side-libraries}

Las experiencias digitales dependen en gran medida del procesamiento del lado del cliente impulsado por código complejo CSS y JavaScript. AEM Las bibliotecas del lado del cliente (clientlibs) le permiten organizar y almacenar de forma centralizada estas bibliotecas del lado del cliente dentro del repositorio. Junto con el [AEM proceso de versión del front-end en el tipo de archivo del proyecto de,](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/uifrontend.html) AEM la administración del código front-end para el proyecto de resulta más sencilla.

AEM Entre las ventajas de usar clientlibs en la práctica se incluyen las siguientes:

* El código del lado del cliente se almacena en el repositorio como el resto del código y el contenido de la aplicación
* AEM Clientlibs en la puede agregar todos los CSS y JS en un archivo
* Exponga los clientlibs a través de una ruta accesible a través de [dispatcher](/help/implementing/dispatcher/disp-overview.md)
* Permite la reescritura de rutas para archivos o imágenes referenciados

AEM Clientlibs es la solución integrada para ofrecer CSS y JavaScript desde el punto de vista de los usuarios de la aplicación de la interfaz de usuario de.

>[!TIP]
>
>AEM Los desarrolladores de front-end que crean CSS y JavaScript para proyectos de también deben familiarizarse con el [AEM Tipo de archivo del proyecto de y su proceso de compilación automatizada del front-end.](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/uifrontend.html)

## Qué son las bibliotecas del lado del cliente {#what-are-clientlibs}

Los sitios requieren JavaScript y CSS y recursos estáticos como iconos y fuentes web para procesarlos en el lado del cliente. AEM Una clientlib es un mecanismo de referencia para la segmentación de datos (por categoría si es necesario) y el servicio de estos recursos.

AEM el CSS y el JavaScript del sitio en un solo archivo, en una ubicación central, para garantizar que solo se incluya una copia de cualquier recurso en la salida del HTML. Esto maximiza la eficacia de la entrega y permite que estos recursos se mantengan centralmente en el repositorio a través de proxy, manteniendo el acceso seguro.

## AEM Desarrollo front-end para la creación de informes as a Cloud Service de {#fed-for-aemaacs}

Todos los recursos de JavaScript, CSS y otros recursos front-end deben mantenerse en el [AEM Módulo ui.frontend del tipo de archivo del proyecto de.](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/uifrontend.html) La flexibilidad del tipo de archivo permite utilizar las herramientas web modernas que elija para crear y administrar estos recursos.

El tipo de archivo puede compilar los recursos en archivos CSS y JS únicos, incrustándolos automáticamente en una `cq:clientLibraryFolder` en el repositorio.

## Estructura de carpetas de biblioteca del lado del cliente {#clientlib-folders}

Una carpeta de biblioteca del lado del cliente es un nodo de repositorio de tipo `cq:ClientLibraryFolder`. Su definición en [Notación CDN](https://jackrabbit.apache.org/node-type-notation.html) es

```text
[cq:ClientLibraryFolder] > sling:Folder
  - dependencies (string) multiple
  - categories (string) multiple
  - embed (string) multiple
  - channels (string) multiple
```

* `cq:ClientLibraryFolder` Los nodos de se pueden colocar en cualquier lugar dentro de `/apps` subárbol del repositorio.
* Utilice el `categories` del nodo para identificar las categorías de biblioteca a las que pertenece.

Cada `cq:ClientLibraryFolder` se rellena con un conjunto de archivos JS o CSS, junto con algunos archivos auxiliares (ver a continuación). Propiedades importantes de `cq:ClientLibraryFolder` se configuran de la siguiente manera:

* `allowProxy`: ya que todos los clientlibs deben almacenarse en `apps`, esta propiedad permite el acceso a las bibliotecas del cliente a través del servlet proxy. Consulte la sección [Localizar una carpeta de biblioteca de cliente y utilizar el servlet de bibliotecas de cliente proxy](#locating-a-client-library-folder-and-using-the-proxy-client-libraries-servlet) más abajo.
* `categories`: Identifica las categorías en las que el conjunto de archivos JS o CSS dentro de este `cq:ClientLibraryFolder` caer. El `categories` al ser de varios valores, permite que una carpeta de biblioteca forme parte de más de una categoría (consulte a continuación para ver cómo puede resultar de utilidad).

Si la carpeta de la biblioteca cliente contiene uno o varios archivos de código fuente que, en tiempo de ejecución, se combinan en un solo archivo JS o CSS. El nombre del archivo generado es el nombre del nodo con el `.js` o `.css` extensión de nombre de archivo. Por ejemplo, el nodo de biblioteca denominado `cq.jquery` resultados en el archivo generado denominado `cq.jquery.js` o `cq.jquery.css`.

Las carpetas de la biblioteca de cliente contienen los siguientes elementos:

* Los archivos de origen JS o CSS
* Recursos estáticos compatibles con los estilos CSS, como iconos, fuentes web, etc.
* Uno `js.txt` archivo y/o uno `css.txt` que identifican los archivos de origen que se van a combinar en los archivos JS o CSS generados

![Arquitectura de Clientlib](assets/clientlib-architecture.drawio.png)

## Creación de carpetas de biblioteca del lado del cliente {#creating-clientlib-folders}

Las bibliotecas de cliente deben encontrarse en `/apps`. Esta regla es necesaria para aislar mejor el código del contenido y la configuración.

Para que las bibliotecas de cliente en `/apps` para que sea accesible, se utiliza un servlet proxy. Las ACL siguen aplicándose en la carpeta de la biblioteca del cliente, pero el servlet permite leer el contenido a través de `/etc.clientlibs/` si la variable `allowProxy` La propiedad se establece en `true`.

1. Abra el CRXDE Lite en un explorador web (`https://<host>:<port>/crx/de`).
1. Seleccione el `/apps` y haga clic en **Crear > Crear nodo**.
1. Introduzca un nombre para la carpeta de la biblioteca y, en **Tipo** seleccionar lista `cq:ClientLibraryFolder`. Haga clic en **Aceptar** y luego en **Guardar todo**.
1. Para especificar las categorías a las que pertenece la biblioteca, seleccione `cq:ClientLibraryFolder` , agregue la siguiente propiedad y haga clic en **Guardar todo**:
   * Nombre: `categories`
   * Tipo: cadena
   * Valor: Nombre de la categoría
   * Múltiple: seleccionado
1. Para que las bibliotecas de cliente sean accesibles mediante proxy en `/etc.clientlibs`, seleccione la `cq:ClientLibraryFolder` , agregue la siguiente propiedad y haga clic en **Guardar todo**:
   * Nombre: `allowProxy`
   * Tipo: booleano
   * Valor: `true`
1. Si necesita administrar recursos estáticos, cree una subcarpeta denominada `resources` debajo de la carpeta de la biblioteca del cliente.
   * Si almacena recursos estáticos en cualquier lugar que no sea la carpeta `resources`, no se puede hacer referencia a ellas en una instancia de publicación.
1. Añada los archivos de origen a la carpeta de la biblioteca.
   * Esto suele hacerlo el proceso de compilación del front-end de [AEM Arquetipo de proyecto de.](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/uifrontend.html)
   * Si lo desea, puede organizar los archivos de origen en subcarpetas.
1. Seleccione la carpeta de la biblioteca de cliente y haga clic en **Crear > Crear archivo**.
1. En el cuadro de nombre de archivo, escriba uno de los siguientes nombres de archivo y haga clic en Aceptar:
   * **`js.txt`:** Utilice este nombre de archivo para generar un archivo JavaScript.
   * **`css.txt`:** Utilice este nombre de archivo para generar una hoja de estilos en cascada.
1. Abra el archivo y escriba el siguiente texto para identificar la raíz de la ruta de los archivos de origen:
   * `#base=*[root]*`
   * Reemplazar `[root]` con la ruta a la carpeta que contiene los archivos de origen, relativa al archivo TXT. Por ejemplo, utilice el siguiente texto cuando los archivos de origen estén en la misma carpeta que el archivo TXT:
      * `#base=.`
   * El siguiente código establece la raíz como la carpeta denominada mobile debajo de `cq:ClientLibraryFolder` nodo:
      * `#base=mobile`
1. En las líneas siguientes `#base=[root]`, escriba las rutas de los archivos de origen relativas a la raíz. Coloque cada nombre de archivo en una línea independiente.
1. Haga clic en **Guardar todo**.

## Servicio de bibliotecas del lado del cliente {#serving-clientlibs}

Una vez creada la carpeta de la biblioteca de cliente [configurado según sea necesario,](#creating-clientlib-folders) sus clientlibs se pueden solicitar a través de un proxy. A modo de ejemplo:

* Tiene una clientlib en `/apps/myproject/clientlibs/foo`
* Tiene una imagen estática en `/apps/myprojects/clientlibs/foo/resources/icon.png`

El `allowProxy` La propiedad permite solicitar:

* La clientlib mediante `/etc.clientlibs/myprojects/clientlibs/foo.js`
* La imagen estática mediante `/etc.clientlibs/myprojects/clientlibs/foo/resources/icon.png`

### Carga de bibliotecas de cliente mediante HTL {#loading-via-htl}

Una vez que los clientlibs se hayan almacenado y administrado correctamente en la carpeta de biblioteca de cliente, se puede acceder a ellos a través de HTL.

AEM Las bibliotecas de cliente se cargan a través de una plantilla de ayuda proporcionada por, a la que se puede acceder mediante `data-sly-use`. Las plantillas de ayuda están disponibles en este archivo, al que se puede llamar mediante `data-sly-call`.

Cada plantilla de ayuda espera una opción `categories` para hacer referencia a las bibliotecas de cliente deseadas. Esa opción puede ser una matriz de valores de cadena o una cadena que contenga una lista de valores separados por comas.

[Consulte la documentación de HTL](https://experienceleague.adobe.com/docs/experience-manager-htl/using/getting-started/getting-started.html#loading-client-libraries) para obtener más información sobre la carga de clientlibs mediante HTL.

<!--
### Setting Cache Timestamps {#setting-cache-timestamps}

This is possible. Still need detail.
-->

## Bibliotecas de cliente en Autor y publicación {#clientlibs-author-publish}

AEM La mayoría de los clientlibs son obligatorios en la instancia de publicación de la. Es decir, la mayoría de los propósitos de los clientlibs son producir la experiencia del usuario final del contenido. Para clientes en instancias de publicación, [herramientas de versión del front-end](#fed-for-aemaacs) se puede utilizar e implementar mediante [carpetas de la biblioteca de cliente como se describe más arriba.](#creating-clientlib-folders)

Sin embargo, hay ocasiones en que puede ser necesario usar bibliotecas de cliente para personalizar la experiencia de creación. AEM Por ejemplo, la personalización de un cuadro de diálogo puede requerir la implementación de pequeños bits de CSS o JS en la instancia de creación de la aplicación de la instancia de creación de la.

### Administración de bibliotecas de cliente en Author {#clientlibs-on-author}

Si necesita utilizar bibliotecas de cliente en Author, puede crear las bibliotecas de cliente en `/apps` utilice los mismos métodos que para la publicación, pero escríbalo directamente en `/apps/.../clientlibs/foo` en lugar de crear un proyecto completo para administrarlo.

A continuación, puede &quot;conectar&quot; al JS de creación añadiendo las bibliotecas de cliente a una categoría de biblioteca de cliente predeterminada.

## Herramientas de depuración {#debugging-tools}

AEM proporciona varias herramientas para depurar y probar carpetas de la biblioteca de cliente.

### Descubrir bibliotecas de cliente {#discover-client-libraries}

El `/libs/cq/granite/components/dumplibs/dumplibs` Este componente genera una página de información sobre todas las carpetas de la biblioteca de cliente del sistema. El `/libs/granite/ui/content/dumplibs` El nodo tiene el componente como tipo de recurso. Para abrir la página, utilice la siguiente URL (cambiando el host y el puerto según sea necesario):

`https://<host>:<port>/libs/granite/ui/content/dumplibs.test.html`

La información incluye la ruta y el tipo de la biblioteca (CSS o JS) y los valores de los atributos de la biblioteca, como las categorías y dependencias. Las tablas posteriores de la página muestran las bibliotecas de cada categoría y canal.

### Consulte Salida generada {#see-generated-output}

El `dumplibs` El componente incluye un selector de prueba que muestra el código fuente generado para `ui:includeClientLib` etiquetas. La página incluye código para diferentes combinaciones de atributos js, css y temáticos.

1. Utilice uno de los siguientes métodos para abrir la página Resultados de la prueba:
   * Desde el `dumplibs.html` , haga clic en el vínculo en la **Haga clic aquí para ver las pruebas de salida** texto.
   * Abra la siguiente URL en el explorador web (utilice un host y un puerto diferentes según sea necesario):
      * `http://<host>:<port>/libs/granite/ui/content/dumplibs.html`
   * La página predeterminada muestra el resultado de las etiquetas sin valor para el atributo categories.
1. Para ver el resultado de una categoría, escriba el valor de la biblioteca de cliente de `categories` y haga clic en **Enviar consulta**.

## Funciones adicionales de carpeta de biblioteca de cliente {#additional-features}

AEM Hay otras funciones compatibles con las carpetas de biblioteca de cliente en la documentación de la biblioteca de. AEM Sin embargo, estos no son necesarios en los casos as a Cloud Service y, por lo tanto, se desaconseja su uso. Se enumeran aquí para completar la información.

>[!WARNING]
>
>AEM Estas funciones adicionales de las carpetas de la biblioteca del cliente no son necesarias en las carpetas as a Cloud Service de la biblioteca del cliente y, por lo tanto, se desaconseja su uso. Se enumeran aquí para completar la información.

### Adobe Granite HTML LIbrary Manager {#html-library-manager}

La configuración de la biblioteca de cliente adicional se puede controlar mediante el **Administrador de bibliotecas de Adobe Granite HTML** del panel de la consola del sistema en `https://<host>:<port>/system/console/configMgr`).

### Propiedades de carpeta adicionales {#additional-folder-properties}

Las propiedades de carpeta adicionales incluyen permitir el control de dependencias e incrustaciones, pero generalmente ya no son necesarias y se desaconseja su uso:

* `dependencies`: es una lista de otras categorías de bibliotecas de cliente de las que depende esta carpeta de bibliotecas. Por ejemplo, dadas dos `cq:ClientLibraryFolder` nodes `F` y `G`, si hay un archivo en `F` requiere otro archivo en `G` para funcionar correctamente, al menos uno de los `categories` de `G` debería estar entre los `dependencies` de `F`.
* `embed`: se utiliza para incrustar código de otras bibliotecas. Si el nodo `F` incrusta nodos `G` y `H`, el HTML resultante es una concatenación de contenido de nodos `G` y `H`.

### Vinculación a dependencias {#linking-to-dependencies}

Cuando el código de la carpeta de la biblioteca de cliente haga referencia a otras bibliotecas, identifique las demás bibliotecas como dependencias. El `ui:includeClientLib` que hace referencia a la carpeta de la biblioteca de cliente hace que el código del HTML incluya un vínculo al archivo de biblioteca generado y a las dependencias.

Las dependencias deben ser otras `cq:ClientLibraryFolder`. Para identificar dependencias, agregue una propiedad a su `cq:ClientLibraryFolder` nodo con los atributos siguientes:

* **Nombre:** dependencias
* **Tipo:** cadena[]
* **Valores:** El valor de la propiedad categories del nodo cq:ClientLibraryFolder del que depende la carpeta de biblioteca actual.

Por ejemplo, la variable `/etc/clientlibs/myclientlibs/publicmain` depende de la variable `cq.jquery` biblioteca. La página que hace referencia a la biblioteca de cliente principal genera un HTML que incluye el siguiente código:

```xml
<script src="/etc/clientlibs/foundation/cq.jquery.js" type="text/javascript">
<script src="/etc/clientlibs/mylibs/publicmain.js" type="text/javascript">
```

### Incrustar Código De Otras Bibliotecas {#embedding-code-from-other-libraries}

Puede incrustar código de una biblioteca de cliente en otra biblioteca de cliente. En tiempo de ejecución, los archivos JS y CSS generados de la biblioteca de incrustación incluyen el código de la biblioteca incrustada.

La incrustación de código resulta útil para proporcionar acceso a bibliotecas almacenadas en áreas seguras del repositorio.

#### Carpetas de la biblioteca de clientes específicas de la aplicación {#app-specific-client-library-folders}

Se recomienda mantener todos los archivos relacionados con la aplicación en la carpeta de su aplicación a continuación `/apps`. También se recomienda denegar el acceso a los visitantes del sitio web a `/apps` carpeta. Para satisfacer ambas prácticas recomendadas, cree una carpeta de biblioteca de cliente debajo de `/etc` que incrusta la biblioteca de cliente que se encuentra debajo de `/apps`.

Utilice la propiedad categories para identificar la carpeta de biblioteca de cliente que se va a incrustar. Para incrustar la biblioteca, agregue una propiedad a la incrustación `cq:ClientLibraryFolder` mediante los atributos de propiedad siguientes:

* **Nombre:** incrustar
* **Tipo:** cadena[]
* **Valor:** El valor de la propiedad categories de `cq:ClientLibraryFolder` nodo para incrustar.

#### Uso de la incrustación para minimizar las solicitudes {#using-embedding-to-minimize-requests}

En algunos casos, es posible que el HTML final que genera la instancia de publicación para la página típica incluya un número relativamente grande de `<script>` elementos.

En estos casos, puede resultar útil combinar todo el código de biblioteca de cliente necesario en un solo archivo para reducir el número de solicitudes de ida y vuelta al cargar la página. Para ello, puede hacer lo siguiente `embed` Agregue las bibliotecas requeridas a la biblioteca de cliente específica de la aplicación mediante la propiedad embed del `cq:ClientLibraryFolder` nodo.

#### Rutas en archivos CSS {#paths-in-css-files}

Al incrustar archivos CSS, el código CSS generado utiliza rutas a recursos relativos a la biblioteca de incrustación. Por ejemplo, la biblioteca de acceso público `/etc/client/libraries/myclientlibs/publicmain` incrusta el `/apps/myapp/clientlib` biblioteca de cliente:

El `main.css` contiene el siguiente estilo:

```javascript
body {
  padding: 0;
  margin: 0;
  background: url(images/bg-full.jpg) no-repeat center top;
  width: 100%;
}
```

El archivo CSS que el `publicmain` El nodo generado contiene el siguiente estilo, con la dirección URL de la imagen original:

```javascript
body {
  padding: 0;
  margin: 0;
  background: url(../../../apps/myapp/clientlib/styles/images/bg-full.jpg) no-repeat center top;
  width: 100%;
}
```

#### Consulte Archivos incrustados en la salida del HTML {#see-embedded-files}

Para realizar un seguimiento del origen del código incrustado o para asegurarse de que las bibliotecas de cliente incrustadas producen los resultados esperados, puede ver los nombres de los archivos que se están incrustando durante la ejecución. Para ver los nombres de archivo, añada el `debugClientLibs=true` a la URL de su página web. La biblioteca que se genera contiene `@import` en lugar del código incrustado.

En el ejemplo anterior [Incrustar Código De Otras Bibliotecas](#embedding-code-from-other-libraries) , la sección `/etc/client/libraries/myclientlibs/publicmain` la carpeta de biblioteca de cliente incrusta el `/apps/myapp/clientlib` carpeta de la biblioteca del cliente. Al anexar el parámetro a la página web, se produce el siguiente vínculo en el código fuente de la página web:

```xml
<link rel="stylesheet" href="/etc/clientlibs/mycientlibs/publicmain.css">
```

Abriendo el `publicmain.css` revela el siguiente código:

```javascript
@import url("/apps/myapp/clientlib/styles/main.css");
```

1. En el cuadro de la dirección del navegador web, añada el siguiente texto a la dirección URL del HTML:
   * `?debugClientLibs=true`
1. Cuando se cargue la página, vea el origen de la página.
1. Haga clic en el vínculo proporcionado como href para el elemento de vínculo para abrir el archivo y ver el código fuente.

### Uso de preprocesadores {#using-preprocessors}

AEM permite el uso de preprocesadores y naves conectables con soporte para [Compresor YUI](https://github.com/yui/yuicompressor#yui-compressor---the-yahoo-javascript-and-css-compressor) para CSS y JavaScript y [Google Closure Compiler (GCC)](https://developers.google.com/closure/compiler/) AEM para JavaScript con la interfaz de usuario de establecida como preprocesador predeterminado de la interfaz de usuario de.

Los preprocesadores conectables permiten un uso flexible que incluye:

* Definición de ScriptProcessors que pueden procesar las fuentes de los scripts
* Los procesadores se pueden configurar con opciones
* Los procesadores se pueden utilizar para la minificación, pero también para casos no minificados
* La clientlib puede definir qué procesador utilizar

>[!NOTE]
>
>AEM De forma predeterminada, utiliza el compresor YUI. Consulte la [Documentación de GitHub del compresor YUI](https://github.com/yui/yuicompressor/issues) para obtener una lista de problemas conocidos. Cambiar al compresor GCC para clientlibs particulares puede resolver algunos problemas observados al utilizar YUI.

>[!CAUTION]
>
>No coloque ninguna biblioteca minificada en una biblioteca de cliente. En su lugar, proporcione la biblioteca sin procesar y, si se requiere la minificación, utilice las opciones de los preprocesadores.

#### Uso {#usage}

Puede elegir configurar la configuración de preprocesadores por biblioteca de cliente o en todo el sistema.

* Añadir las propiedades de varios valores `cssProcessor` y `jsProcessor` en el nodo clientlibrary
* O defina la configuración predeterminada del sistema mediante la variable **Administrador de biblioteca de HTML** Configuración de OSGi

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

1. Vaya al Administrador de configuración de Apache Felix en (`http://<host>:<portY/system/console/configMgr`)
1. Busque y edite el **Administrador de bibliotecas de Adobe Granite HTML**.
1. Habilite la **Minificar** opción (si no está activada).
1. Establecer el valor **Configuraciones predeterminadas del procesador JS** hasta `min:gcc`.
   * Las opciones se pueden pasar si se separan con punto y coma, por ejemplo, `min:gcc;obfuscate=true`.
1. Clic **Guardar** para guardar los cambios.
