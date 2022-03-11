---
title: Tipos de módulos de interfaz de usuario de ContextHub de muestra
description: ContextHub proporciona varios módulos de IU de ejemplo que puede utilizar en sus soluciones
exl-id: 31ff4444-8d96-4817-9676-ea5ad36dcda5
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '1126'
ht-degree: 0%

---

# Tipos de módulos de interfaz de usuario de ContextHub de muestra {#sample-contexthub-ui-module-types}

ContextHub proporciona varios módulos de IU de ejemplo que puede utilizar en sus soluciones. Se proporciona la siguiente información:

* Funciones principales del módulo de IU.
* Dónde encontrar el código fuente para que pueda abrirlo con fines de aprendizaje.
* Cómo configurar el módulo de IU.

Para obtener información sobre cómo agregar módulos de IU a ContextHub, consulte [Adición de un módulo de IU](configuring-contexthub.md#adding-a-ui-module). Para obtener información sobre el desarrollo de módulos de IU, consulte [Creación de tipos de módulos de IU de ContextHub](extending-contexthub.md#creating-contexthub-ui-module-types).

## Tipo de módulo de interfaz de usuario contexthub.base {#contexthub-base-ui-module-type}

El tipo de módulo de IU contexthub.base es el tipo base para todos los demás tipos de módulos de IU. De este modo, proporciona funciones genéricas para procesar los datos del almacén.

Estas son las funciones disponibles:

* **Título e icono:** Especifique un título para el módulo de IU y un icono. Se puede hacer referencia al icono mediante una dirección URL o desde la biblioteca de iconos de la interfaz de usuario de Coral .
* **Almacenar datos:** Identifique una o más tiendas desde las que recuperar datos.
* **Contenido:** Especifique el contenido que aparece en el módulo de IU tal como aparece en la barra de herramientas de ContextHub.
* **Enviar contenido:** Especifique el contenido que aparece en una ventana emergente cuando se hace clic o se toca el módulo de la interfaz de usuario.
* **Modo de pantalla completa:** Controle si está permitido el modo de pantalla completa.

El código fuente se encuentra en `/libs/granite/contexthub/code/ui/container/js/ContextHub.UI.BaseModuleRenderer.js`.

### Configuración {#configuration}

Configure el módulo de IU contexthub.base utilizando un objeto Javascript en formato JSON. Incluya cualquiera de las siguientes propiedades para configurar las características del módulo de interfaz de usuario:

* **imagen:** Dirección URL de una imagen para mostrarla como icono.
* **icono:** El nombre de un [Icono de Coral UI](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/coral-ui/coralui3/Coral.Icon.html) Clase . Si especifica un valor para las propiedades del icono y de la imagen, se utilizará la imagen.
* **title:** Un título para el módulo de IU. El título aparece cuando el puntero se pone en pausa sobre el icono de módulo de interfaz de usuario.
* **pantalla completa:** Un valor booleano que indica si el módulo de IU es compatible con el modo de pantalla completa. Uso `true` para admitir pantalla completa y `false` para evitar el modo de pantalla completa.
* **plantilla:** A [Manillares](https://handlebarsjs.com/) plantilla que especifica el contenido que se va a procesar en la barra de herramientas de ContextHub. Usar como máximo dos `<p>` etiquetas.
* **storeMapping:** Una asignación de clave/tienda. Utilice la clave de las plantillas de Handlebar para acceder a los datos asociados del almacén de ContextHub.
* **lista:** Matriz de elementos que se mostrarán como una lista en una ventana emergente cuando se haga clic en el módulo de la interfaz de usuario. Si incluye este elemento, no incluya popoverTemplate. El valor es una matriz de objetos con las claves siguientes:
   * title: Texto que se va a mostrar para este elemento
   * imagen: (Opcional) Dirección URL de una imagen que debe mostrarse a la izquierda
   * icono: (Opcional) Una clase de icono CUI que debe mostrarse a la izquierda; ignorado si se especifica una imagen
   * seleccionados: (Opcional) Un valor booleano que especifica si este elemento debe mostrarse como seleccionado (true=seleccionado). De forma predeterminada, los elementos seleccionados aparecen en negrita. Utilice un `listType` para configurar otras apariencias (consulte a continuación).
* **listType:** Estilo que se utilizará para los elementos de la lista de elementos emergentes. Utilice uno de los siguientes valores:
   * marca de verificación
   * casilla de verificación
   * radio
* **popoverTemplate:** Una plantilla Handlebars que especifica el contenido que se procesará en la ventana emergente cuando se haga clic en el módulo de la interfaz de usuario. Si incluye este artículo, no incluya el `list` elemento.

### Ejemplo {#example}

El siguiente ejemplo configura una c`ontexthub.base` Módulo de interfaz de usuario para mostrar información de un [contexthub.emulators](sample-stores.md#granite-emulators-sample-store-candidate) tienda. La variable `template` muestra cómo obtener datos del almacén utilizando la clave de que `storeMapping` establece el elemento.

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

La variable `contexthub.browserinfo` El módulo de IU muestra información sobre el navegador web del cliente y el sistema operativo. La información se obtiene de la tienda surferinfo, basada en la variable [contexthub.surferinfo](sample-stores.md#contexthub-surferinfo-sample-store-candidate) candidato de tienda.

![módulo contexthub.browserinfo](assets/browserinfo-module.png)

El código fuente del módulo UI se encuentra en `/libs/granite/contexthub/components/modules/browserinfo`. Aunque `contexthub.browserinfo` amplía el `contexthub.base` El módulo de IU no anula ni proporciona funciones adicionales. La implementación proporciona una configuración predeterminada para procesar información del explorador.

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

## contexthub.datetime Tipo de módulo de interfaz de usuario {#contexthub-datetime-ui-module-type}

La variable `contexthub.datetime` El módulo de IU muestra la fecha y la hora almacenadas en un almacén denominado datetime basado en la variable `contexthub.datetime` candidato de tienda.

![contexthub.datetime](assets/datetime-module.png)

El módulo proporciona un formulario de introducción que le permite cambiar la fecha y la hora en la tienda.

La fuente de la variable `contexthub.datetime` El módulo de IU se encuentra en `/libs/granite/contexthub/components/modules/datetime`.

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

La variable `contexthub.location` El módulo de IU muestra la longitud y la latitud del cliente. El módulo proporciona una ventana emergente que muestra un mapa de Google en el que puede hacer clic para cambiar la ubicación actual. El módulo obtiene información de un almacén de ContextHub llamado geolocalización basada en la variable [contexthub.geolocation](sample-stores.md#contexthub-geolocation-sample-store-candidate) candidato de tienda.

![módulo contexthub.location](assets/location-module.png)

El origen del módulo de IU se encuentra en `/etc/cloudsettings/default/contexthub/geolocation`.

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

La variable `contexthub.screen-orientation` El módulo de IU muestra la orientación actual de la pantalla del cliente. Aunque está desactivado de forma predeterminada, el módulo proporciona una ventana emergente que le permite seleccionar una orientación. El módulo obtiene información de un almacén de ContextHub denominado emuladores que se basan en la variable [granite.emulators](sample-stores.md#granite-emulators-sample-store-candidate) candidato de tienda.

![contexthub.screen-orientation module](assets/screen-orientation-module.png)

El origen del módulo de IU se encuentra en `/libs/granite/contexthub/components/modules/screen-orientation`.

### Configuración {#configuration-5}

Instancias de `contexthub.screen-orientation` El módulo de IU no requiere un valor para la Configuración de detalles. El siguiente texto JSON representa la configuración predeterminada del módulo. Tenga en cuenta que `clickable` la propiedad es `false` de forma predeterminada. Si anula la configuración predeterminada para establecer `clickable` a `true`, al hacer clic en el módulo se muestra una ventana emergente en la que puede seleccionar la orientación.

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

La variable `contexthub.tagcloud` El módulo de IU muestra información sobre las etiquetas. En la barra de herramientas, el módulo IU muestra el número de etiquetas. La ventana emergente muestra una nube de etiquetas y un cuadro de texto para agregar nuevas etiquetas. El módulo de IU obtiene información de un almacén de ContextHub denominado tagcloud que se basa en la variable `contexthub.tagcloud` candidato de tienda.

![módulo contexthub.tagcloud](assets/tagcloud-module.png)

El origen del módulo de IU se encuentra en `/libs/granite/contexthub/components/modules/tagcloud`.

### Configuración {#configuration-6}

Instancias de `contexthub.tagcloud` El módulo de IU no requiere un valor para la Configuración de detalles. El siguiente texto JSON representa la configuración predeterminada del módulo.

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

## Tipo de módulo de interfaz de usuario de granite.profile {#granite-profile-ui-module-type}

La variable `granite.profile` El módulo de IU de ContextHub muestra el nombre para mostrar del usuario actual. La ventana emergente muestra el nombre de inicio de sesión del usuario y le permite cambiar el valor del nombre para mostrar. El módulo de IU obtiene información de un perfil denominado del almacén de ContextHub basado en la variable [granite.profile](sample-stores.md#granite-profile-sample-store-candidate) candidato de tienda.

![módulo granite.profile](assets/profile-module.png)

El origen del módulo de IU se encuentra en `/libs/granite/contexthub/components/modules/profile`.

### Configuración {#configuration-7}

Instancias de `granite.profile` El módulo de IU no requiere un valor para la Configuración de detalles. El siguiente texto JSON representa la configuración predeterminada del módulo.

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
