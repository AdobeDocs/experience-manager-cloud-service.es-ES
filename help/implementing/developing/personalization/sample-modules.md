---
title: Tipos de módulos de interfaz de usuario de ContextHub de muestra
description: ContextHub proporciona varios módulos de interfaz de usuario de muestra que puede utilizar en sus soluciones
translation-type: tm+mt
source-git-commit: 2a589ff554a5cced3d7ad45d981697debb73992f
workflow-type: tm+mt
source-wordcount: '1128'
ht-degree: 0%

---


# Tipos de módulos de interfaz de usuario de ContextHub de muestra {#sample-contexthub-ui-module-types}

ContextHub proporciona varios módulos de interfaz de usuario de muestra que puede utilizar en sus soluciones. Se proporciona la siguiente información:

* Funciones principales del módulo de interfaz de usuario.
* Dónde encontrar el código fuente para poder abrirlo con fines de aprendizaje.
* Cómo configurar el módulo de interfaz de usuario.

Para obtener información sobre cómo agregar módulos de interfaz de usuario a ContextHub, consulte [Añadir un módulo](configuring-contexthub.md#adding-a-ui-module)de interfaz de usuario. Para obtener información sobre el desarrollo de módulos de interfaz de usuario, consulte [Creación de tipos](extending-contexthub.md#creating-contexthub-ui-module-types)de módulos de interfaz de usuario de ContextHub.

## Tipo de módulo de interfaz de usuario contexthub.base {#contexthub-base-ui-module-type}

El tipo de módulo de interfaz de usuario contexthub.base es el tipo base para todos los demás tipos de módulos de interfaz de usuario. De este modo, proporciona funciones genéricas para procesar los datos del almacén.

Están disponibles las siguientes funciones:

* **Título e icono:** Especifique un título para el módulo de interfaz de usuario y un icono. Se puede hacer referencia al icono mediante una URL o desde la biblioteca de iconos de la interfaz de usuario de Coral.
* **Almacenar datos:** Identifique uno o más almacenes desde los cuales recuperar datos.
* **Contenido:** Especifique el contenido que aparece en el módulo de interfaz de usuario tal como aparece en la barra de herramientas de ContextHub.
* **Contenido emergente:** Especifique el contenido que aparece en una ventana emergente cuando se hace clic o se toca el módulo de la interfaz de usuario.
* **Modo de pantalla completa:** Controlar si se permite el modo de pantalla completa.

El código fuente se encuentra en `/libs/granite/contexthub/code/ui/container/js/ContextHub.UI.BaseModuleRenderer.js`.

### Configuración {#configuration}

Configure el módulo de interfaz de usuario contexthub.base con un objeto Javascript en formato JSON. Incluya cualquiera de las siguientes propiedades para configurar las funciones del módulo de interfaz de usuario:

* **image:** Dirección URL de una imagen para mostrarla como icono.
* **icono:** Nombre de una clase de icono [de](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/coral-ui/coralui3/Coral.Icon.html) Coral UI. Si especifica un valor tanto para las propiedades de icono como de imagen, se utilizará la imagen.
* **title:** Un título para el módulo de interfaz de usuario. El título aparece cuando el puntero se pone en pausa sobre el icono del módulo de la interfaz de usuario.
* **pantalla completa:** Valor booleano que indica si el módulo de interfaz de usuario admite el modo de pantalla completa. Se utiliza `true` para admitir la pantalla completa y `false` para evitar el modo de pantalla completa.
* **plantilla:** Plantilla [Handlebars](https://handlebarsjs.com/) que especifica el contenido que se va a procesar en la barra de herramientas de ContextHub. Utilice como máximo dos `<p>` etiquetas.
* **storeMapping:** Asignación de clave/tienda. Utilice la clave de las plantillas de la barra de control para acceder a los datos asociados del almacén de ContextHub.
* **lista:** Matriz de elementos que se mostrarán como listas en una ventana emergente cuando se haga clic en el módulo de la interfaz de usuario. Si incluye este elemento, no incluya popoverTemplate. El valor es una matriz de objetos con las siguientes claves:
   * title: Texto que se va a mostrar para este elemento
   * image: (Opcional) Dirección URL de una imagen que debe mostrarse a la izquierda
   * icono: (Opcional) Una clase de icono CUI que debe mostrarse a la izquierda; se omite si se especifica una imagen
   * seleccionado: (Opcional) Un valor booleano que especifica si este elemento debe mostrarse como seleccionado (true=seleccionado). De forma predeterminada, los elementos seleccionados aparecen con una fuente en negrita. Utilice una `listType` propiedad para configurar otros aspectos visuales (consulte a continuación).
* **listType:** Estilo que se va a utilizar para los elementos de lista de la ventana emergente. Utilice uno de los siguientes valores:
   * marca de verificación
   * casilla de verificación
   * radio
* **poverTemplate:** Una plantilla de Handlebars que especifica el contenido que se procesará en la ventana emergente cuando se haga clic en el módulo de la interfaz de usuario. Si incluye este elemento, no incluya el `list` .

### Ejemplo {#example}

En el ejemplo siguiente se configura un módulo de IU c`ontexthub.base` para mostrar información de una tienda [contexthub.emulators](sample-stores.md#granite-emulators-sample-store-candidate) . El `template` elemento muestra cómo obtener datos del almacén utilizando la clave que establece el `storeMapping` elemento.

```javascript
{
   "icon": "coral-Icon--move",
    "title": "Screen Resolution",
    "storeMapping": {
      "emulator": "emulators"
    },
    "template": "<p>{{{ i18n \"Resolution\"}}}</p><p>{{{emulator.currentDevice.width}}} x {{{emulator.currentDevice.height}}}</p>"
}
```

![módulo contexthub.base](assets/base-module.png)

## contexthub.browserinfo Tipo de módulo de interfaz de usuario {#contexthub-browserinfo-ui-module-type}

El módulo `contexthub.browserinfo` UI muestra información sobre el explorador web y el sistema operativo del cliente. La información se obtiene de la tienda surferinfo, basada en el [candidato de la tienda contexthub.surferinfo](sample-stores.md#contexthub-surferinfo-sample-store-candidate) .

![módulo contexthub.browserinfo](assets/browserinfo-module.png)

El código fuente del módulo de interfaz de usuario se encuentra en `/libs/granite/contexthub/components/modules/browserinfo`. Aunque `contexthub.browserinfo` amplía el módulo de la `contexthub.base` interfaz de usuario, no reemplaza ni proporciona funciones adicionales. La implementación proporciona una configuración predeterminada para procesar la información del explorador.

### Configuración {#configuration-1}

Las instancias del módulo de interfaz de usuario contexthub.browserinfo no requieren un valor para la Configuración de detalles. El siguiente texto JSON representa la configuración predeterminada del módulo.

```javascript
{
   "icon":"coral-Icon--globe",
   "title":"Browser/OS Information",
   "storeMapping":{"surferinfo":"surferinfo"},
   "template":"<p>{{surferinfo.browser.family}} {{surferinfo.browser.version}}</p><p>{{surferinfo.os.name}} {{surferinfo.os.version}}</p>"
}
```

## Tipo de módulo de interfaz de usuario contexthub.datetime {#contexthub-datetime-ui-module-type}

El módulo `contexthub.datetime` UI muestra la fecha y la hora almacenadas en una tienda denominada datetime que se basa en el candidato del almacén [contexthub.datetime](sample-stores.md#contexthub-datetime-sample-store-candidate) .

![módulo contexthub.datetime](assets/datetime-module.png)

El módulo proporciona un formulario emergente que le permite cambiar la fecha y la hora en la tienda.

El origen del módulo de la `contexthub.datetime` interfaz de usuario se encuentra en `/libs/granite/contexthub/components/modules/datetime`.

### Configuración {#configuration-2}

Las instancias del módulo de interfaz de usuario contexthub.datetime no requieren un valor para la Configuración de detalles. El siguiente texto JSON representa la configuración predeterminada del módulo.

```javascript
{
   "icon":"coral-Icon--clock",
   "title":"DATE&TIME",
   "clickable":true,
   "storeMapping":{"d":"datetime"},
   "template":"<p class=\"contexthub-module-line1\">{{i18n \"Date&Time\"}}</p><p class=\"contexthub-module-line2\">{{d.formatted.locale.date}} {{d.formatted.locale.time}}</p>",
   "popoverTemplate":"<div class=\"datetime center\"><div class=\"coral-DatePicker-calendar\" data-init=\"datepicker\"><input class=\"coral-Textfield\" type=\"datetime\" value=\"{{d.formatted.iso}}\"><button class=\"coral-Button coral-Button--secondary coral-Button--square\" title=\"{{i18n \"Datetime picker\"}}\"><i class=\"coral-Icon coral-Icon--calendar coral-Icon--sizeS\"></i></button></div></div>"
}
```

## Tipo de módulo de interfaz de usuario contexthub.location {#contexthub-location-ui-module-type}

El módulo `contexthub.location` UI muestra la longitud y la latitud del cliente. El módulo proporciona una ventana emergente que muestra un mapa de Google en el que puede hacer clic para cambiar la ubicación actual. El módulo obtiene información de una tienda de ContextHub llamada geolocalización basada en el [candidato de la tienda de contexto.geolocalización](sample-stores.md#contexthub-geolocation-sample-store-candidate) .

![módulo contexthub.location](assets/location-module.png)

El origen del módulo de interfaz de usuario se encuentra en `/etc/cloudsettings/default/contexthub/geolocation`.

### Configuración {#configuration-4}

Las instancias del módulo de interfaz de usuario contexthub.location no requieren un valor para la Configuración de detalles. El siguiente texto JSON representa la configuración predeterminada del módulo.

```javascript
{
 "icon":"coral-Icon--compass",
 "title":"Location",
 "clickable":true,
 "editable":{"key":"/geolocation","disabled":[],"hidden":["/geolocation/generatedThumbnail","/geolocation/city","/geolocation/country"]},
 "fullscreen":true,
 "storeMapping":{"g":"geolocation"},
 "template":"<p>{{i18n \"Location\"}}</p><p>{{g.address.postalCode}} {{g.address.city}}{{#if g.address.city}}{{#if g.address.region}},{{/if}}{{/if}} {{g.address.region}}</p>",
 "list":[
  {"title":"Basel, Switzerland",
  "data":{"longitude":7.58929,"latitude":47.554746,"city":"Basel","country":"Switzerland"}},
  {"title":"Melbourne, Australia",
  "data":{"longitude":144.96328,"latitude":-37.814107,"city":"Melbourne","country":"Australia"}},
  {"title":"Beijing, China",
  "data":{"longitude":116.407526,"latitude":39.90403,"city":"Beijing","country":"China"}},
  {"title":"New York, NY, USA",
  "data":{"longitude":-74.005973,"latitude":40.714353,"city":"New York","country":"United States"}},
  {"title":"Paris, France",
  "data":{"longitude":2.352222,"latitude":48.856614,"city":"Paris","country":"France"}},
  {"title":"Rio de Janeiro, Brazil",
  "data":{"longitude":-43.20071,"latitude":-22.913395,"city":"Rio","country":"Brazil"}},
  {"title":"San Jose, CA, USA",
  "data":{"longitude":-121.894955,"latitude":37.339386,"city":"San Jose","country":"United States"}},
  {"title":"Tokyo, Japan",
  "data":{"longitude":139.691706,"latitude":35.689487,"city":"Shinjuku","country":"Japan"}}
 ],
 "listType":"checkmark"
}
```

## contexthub.screen-orientation UI Tipo de módulo {#contexthub-screen-orientation-ui-module-type}

El módulo `contexthub.screen-orientation` UI muestra la orientación actual de la pantalla del cliente. Aunque está deshabilitado de forma predeterminada, el módulo proporciona una ventana emergente que le permite seleccionar una orientación. El módulo obtiene información de una tienda de ContextHub denominada emuladores que se basa en el candidato de la tienda [granite.emulators](sample-stores.md#granite-emulators-sample-store-candidate) .

![módulo contexthub.screen-orientation](assets/screen-orientation-module.png)

El origen del módulo de interfaz de usuario se encuentra en `/libs/granite/contexthub/components/modules/screen-orientation`.

### Configuración {#configuration-5}

Las instancias del módulo `contexthub.screen-orientation` UI no requieren un valor para la Configuración de detalles. El siguiente texto JSON representa la configuración predeterminada del módulo. Tenga en cuenta que la `clickable` propiedad está `false` predeterminada. Si anula la configuración predeterminada en la que desea configurarla, `clickable` al hacer clic en `true`el módulo se abre una ventana emergente en la que puede seleccionar la orientación.

```javascript
{
   "icon":"coral-Icon--rotateRight",
   "title":"Screen Orientation",
   "clickable":false,
   "storeMapping":{"emulator":"emulators"},
   "template":"<p>{{{ i18n \"Screen Orientation\" }}}</p><p>{{{ emulator.currentDevice.orientation }}}",
   "listReference":"/emulators/orientations",
   "listType":"checkmark"
}
```

## Tipo de módulo de interfaz de usuario contexthub.tagcloud {#contexthub-tagcloud-ui-module-type}

El módulo `contexthub.tagcloud` UI muestra información sobre las etiquetas. En la barra de herramientas, el módulo UI muestra el número de etiquetas. La ventana emergente muestra un tagcloud y un cuadro de texto para agregar nuevas etiquetas. El módulo UI obtiene información de una tienda de ContextHub denominada tagcloud basada en el candidato a la tienda [contexthub.tagcloud](sample-stores.md#contexthub-tagcloud-sample-data-store) .

![módulo ContextHub.tagcloud](assets/tagcloud-module.png)

El origen del módulo de interfaz de usuario se encuentra en `/libs/granite/contexthub/components/modules/tagcloud`.

### Configuración {#configuration-6}

Las instancias del módulo `contexthub.tagcloud` UI no requieren un valor para la Configuración de detalles. El siguiente texto JSON representa la configuración predeterminada del módulo.

```javascript
{
   "icon":"coral-Icon--tag",
   "title":"TagCloud",
   "clickable":true,
   "storeMapping":{"t":"tagcloud"},
   "maxTags":20,
   "template":"<p class=\"contexthub-module-line1\">{{i18n \"TagCloud\"}}</p><p class=\"contexthub-module-line2\">{{stats.total}} {{i18n \"Tags\"}}</p>",
   "popoverTemplate":"<div class=\"contexthub-popover-content center\"><p class=\"stats\">{{stats.total}} {{i18n \"Tags\"}} | {{stats.hits}} {{i18n \"Hits\"}} | {{i18n \"Last tag\"}}: {{#if stats.recent}}{{stats.recent}}{{else}}{{i18n \"Unknown\"}}{{/if}}</p><p class=\"tagcloud\">{{#each tags}}<span class=\"tag{{this.weight}}\">{{this.name}}</span> {{/each}}</p><div class=\"coral-InputGroup\"><input type=\"text\" class=\"coral-InputGroup-input coral-Textfield tag-name\" placeholder=\"{{i18n \"Add a namespace:my/tag\"}}\" pattern=\"^[A-Za-z0-9_\\-]+(:[A-Za-z0-9_\\-\\/]+)?$\" title=\"{{i18n \"namespace:my/tag\"}}\"><span class=\"coral-InputGroup-button\"><button class=\"coral-Button coral-Button--secondary coral-Button--square contexthub-new-tag\" type=\"button\" title=\"{{i18n \"increment\"}}\"><i class=\"coral-Icon coral-Icon--sizeS coral-Icon--add\"></i></button></span></div></div>"
}
```

## tipo de módulo de interfaz de usuario de granite.perfil {#granite-profile-ui-module-type}

El módulo de IU de `granite.profile` ContextHub muestra el nombre para mostrar del usuario actual. La ventana emergente revela el nombre de inicio de sesión del usuario y le permite cambiar el valor del nombre para mostrar. El módulo de interfaz de usuario obtiene información de una tienda de ContextHub denominada perfil basada en el candidato de la tienda [granite.perfil](sample-stores.md#granite-profile-sample-store-candidate) .

![módulo granite.perfil](assets/profile-module.png)

El origen del módulo de interfaz de usuario se encuentra en `/libs/granite/contexthub/components/modules/profile`.

### Configuración {#configuration-7}

Las instancias del módulo `granite.profile` UI no requieren un valor para la Configuración de detalles. El siguiente texto JSON representa la configuración predeterminada del módulo.

```javascript
{
   "icon":"coral-Icon--user",
   "title":"Profile",
   "clickable":true,
   "editable":{
      "key":"/profile",
      "disabled":["/profile/authorizableId"],
      "hidden":["/profile/avatar","/profile/path"]},
   "storeMapping":{"p":"profile"},
   "template":"<p class=\"contexthub-module-line1\">{{i18n \"Persona\"}}</p><p class=\"contexthub-module-line2\">{{p.displayName}}</p>",
   "listType":"checkmark"
}
```
