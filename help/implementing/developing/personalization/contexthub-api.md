---
title: Referencia de la API de JavaScript de ContextHub
description: La API de JavaScript de ContextHub está disponible para los scripts cuando se agrega el componente ContextHub a la página
exl-id: ec35bef5-610c-4e85-a43a-d4201b5eb03e
feature: Developing, Personalization
role: Admin, Architect, Developer
source-git-commit: bdf3e0896eee1b3aa6edfc481011f50407835014
workflow-type: tm+mt
source-wordcount: '4602'
ht-degree: 2%

---

# Referencia de la API de JavaScript de ContextHub {#contexthub-javascript-api-reference}

La API de JavaScript de ContextHub está disponible para los scripts cuando se agrega el componente [ContextHub a la página](adding-contexthub.md).

## Constantes de ContextHub {#contexthub-constants}

Valores constantes que define la API de JavaScript de ContextHub.

### Constantes de evento {#event-constants}

En la tabla siguiente se enumeran los nombres y eventos que se producen en las tiendas de ContextHub. Ver también [ContextHub.Utils.Eventing](#contexthub-utils-eventing).

| Constante | Descripción | Valor |
|---|---|---|
| `ContextHub.Constants.EVENT_NAMESPACE` | Área de nombres de evento de ContextHub | `ch` |
| `ContextHub.Constants.EVENT_ALL_STORES_READY` | Indica que todas las tiendas requeridas están registradas, inicializadas y listas para consumirse | `all-stores-ready` |
| `ContextHub.Constants.EVENT_STORES_PARTIALLY_READY` | Indica que no todos los almacenes se inicializaron dentro de un tiempo de espera determinado | `stores-partially-ready` |
| `ContextHub.Constants.EVENT_STORE_REGISTERED` | Se activa cuando se registra una tienda | `store-registered` |
| `ContextHub.Constants.EVENT_STORE_READY` | Indica que las tiendas están listas para funcionar. Se activa inmediatamente después del registro, excepto en los almacenes JSONP, donde se activa cuando se recuperan datos). | `store-ready` |
| `ContextHub.Constants.EVENT_STORE_UPDATED` | Se activa cuando una tienda actualiza su persistencia | `store-updated` |
| `ContextHub.Constants.PERSISTENCE_CONTAINER_NAME` | Nombre de contenedor de persistencia | `ContextHubPersistence` |
| `ContextHub.Constants.SERVICE_RAW_RESPONSE_KEY` | Almacena el nombre de clave de persistencia específico donde se almacena el resultado JSON sin procesar | `/_/raw-response` |
| `ContextHub.Constants.SERVICE_RESPONSE_TIME_KEY` | Almacena la marca de tiempo específica que indica cuándo se recuperaron los datos de JSON | `/_/response-time` |
| `ContextHub.Constants.SERVICE_LAST_URL_KEY` | Almacena la URL específica del servicio JSON utilizado durante la última llamada | `/_/url` |
| `ContextHub.Constants.IS_CONTAINER_EXPANDED` | Indica si la IU de ContextHub está expandida | `/_/container-expanded` |

### Constantes de evento de IU {#ui-event-constants}

En la tabla siguiente se enumeran los nombres de los eventos que se producen en la interfaz de usuario de ContextHub.

| **Constante** | **Descripción** | **Valor** |
|---|---|---|
| `ContextHub.Constants.EVENT_UI_MODE_REGISTERED` | Se activa cuando se registra un modo | `ui-mode-registered` |
| `ContextHub.Constants.EVENT_UI_MODE_UNREGISTERED` | Se activa cuando un modo no está registrado | `ui-mode-unregistered` |
| `ContextHub.Constants.EVENT_UI_MODE_RENDERER_REGISTERED` | Se activa cuando se registra un procesador en modo | `ui-mode-renderer-registered` |
| `ContextHub.Constants.EVENT_UI_MODE_RENDERER_UNREGISTERED` | Se activa cuando un procesador en modo no está registrado | `ui-mode-renderer-unregistered` |
| `ContextHub.Constants.EVENT_UI_MODE_ADDED` | Se activa cuando se añade un nuevo modo | `ui-mode-added` |
| `ContextHub.Constants.EVENT_UI_MODE_REMOVED` | Se activa cuando se elimina un modo | `ui-mode-removed` |
| `ContextHub.Constants.EVENT_UI_MODE_SELECTED` | Se activa cuando el usuario selecciona un modo | `ui-mode-selected` |
| `ContextHub.Constants.EVENT_UI_MODULE_REGISTERED` | Se activa cuando se registra un módulo nuevo | `ui-module-registered` |
| `ContextHub.Constants.EVENT_UI_MODULE_UNREGISTERED` | Se activa cuando un módulo no está registrado | `ui-module-unregistered` |
| `ContextHub.Constants.EVENT_UI_MODULE_RENDERER_REGISTERED` | Se activa cuando se registra un procesador de módulos | `ui-module-renderer-registered` |
| `ContextHub.Constants.EVENT_UI_MODULE_RENDERER_UNREGISTERED` | Se activa cuando un procesador de módulos no está registrado. | `ui-module-renderer-unregistered` |
| `ContextHub.Constants.EVENT_UI_MODULE_ADDED` | Se activa cuando se añade un módulo nuevo | `ui-module-added` |
| `ContextHub.Constants.EVENT_UI_MODULE_REMOVED` | Se activa cuando se elimina un módulo | `ui-module-removed` |
| `ContextHub.Constants.EVENT_UI_CONTAINER_ADDED` | Se activa cuando se añade el contenedor de IU a la página | `ui-container-added` |
| `ContextHub.Constants.EVENT_UI_CONTAINER_OPENED` | Se activa al abrir la interfaz de usuario de ContextHub | `ui-container-opened` |
| `ContextHub.Constants.EVENT_UI_CONTAINER_CLOSED` | Se activa cuando la interfaz de usuario de ContextHub está contraída | `ui-container-closed` |
| `ContextHub.Constants.EVENT_UI_PROPERTY_MODIFIED` | Se activa cuando se modifica una propiedad | `ui-property-modified` |
| `ContextHub.Constants.EVENT_UI_RENDERED` | Se activa cada vez que se procesa la interfaz de usuario de ContextHub (por ejemplo, después de un cambio de propiedad) | `ui-rendered` |
| `ContextHub.Constants.EVENT_UI_INITIALIZED` | Se activa cuando se inicializa el contenedor de IU | `ui-initialized` |
| `ContextHub.Constants.ACTIVE_UI_MODE` | Indica el modo de IU activo | `/_/active-ui-mode` |

## Referencia de la API de JavaScript de ContextHub {#contexthub-javascript-api-reference-2}

El objeto ContextHub proporciona acceso a todas las tiendas.

### Funciones (ContextHub) {#functions-contexthub}

#### getAllStores() {#getallstores}

Devuelve todas las tiendas registradas de ContextHub.

Esta función no tiene parámetros.

##### Devuelve {#returns-}

Un objeto que contiene todos los almacenes de ContextHub. Cada almacén es un objeto que utiliza el mismo nombre que el almacén.

##### Ejemplos {#example-}

El ejemplo siguiente recupera todos los almacenes y, a continuación, recupera el almacén de geolocalización:

```javascript
var allStores = ContextHub.getAllStores();
var geoloc = allStores.geolocation
```

#### getStore(nombre) {#getstore-name}

Recupera un almacén como un objeto JavaScript.

##### Parámetros {#parameters-}

* **`name`:** Nombre con el que se registró el almacén.

##### Devuelve {#returns-getstore-name}

Un objeto que representa el almacén.

##### Ejemplos {#example-getstore-name}

El siguiente ejemplo recupera el almacén de geolocalización:

```javascript
var geoloc = ContextHub.getStore("geolocation");
```

## ContextHub.SegmentEngine.Segment {#contexthub-segmentengine-segment}

Representa un segmento de ContextHub. Use `ContextHub.SegmentEngine.SegmentManager` para obtener segmentos.

### Funciones (ContextHub.ContextEngine.Segment) {#functions-contexthub-contextengine-segment}

#### getName() {#getname}

Devuelve el nombre del segmento como un valor de tipo String.

#### getPath() {#getpath}

Devuelve la ruta del repositorio de la definición del segmento como un valor de tipo String.

## ContextHub.SegmentEngine.SegmentManager {#contexthub-segmentengine-segmentmanager}

Proporciona acceso a los segmentos de ContextHub.

### Funciones (ContextHub.SegmentEngine.SegmentManager) {#functions-contexthub-segmentengine-segmentmanager}

#### getResolvedSegments() {#getresolvedsegments}

Devuelve los segmentos resueltos en el contexto actual. Esta función no tiene parámetros.

##### Devuelve {#returns-getresolvedsegments}

Matriz de `ContextHub.SegmentEngine.Segment` objetos.

## ContextHub.Store.Core {#contexthub-store-core}

La clase base para las tiendas de ContextHub.

### Propiedades (ContextHub.Store.Core) {#properties-contexthub-store-core}

#### evento {#eventing}

Un objeto [`ContextHub.Utils.Eventing`](#contexthub-utils-eventing). Utilice este objeto para enlazar funciones para almacenar eventos. Para obtener información acerca del valor predeterminado y la inicialización, vea [`init(name,config)`](#init-name-config).

#### name {#name}

El nombre de la tienda.

#### persistencia {#persistence}

Un objeto `ContextHub.Utils.Persistence`. Para obtener información acerca del valor predeterminado y la inicialización, vea [`init(name,config)`](#init-name-config).

### Funciones (ContextHub.Store.Core) {#functions-contexthub-store-core}

#### addAllItems(árbol, opciones) {#addallitems-tree-options}

Combina un objeto de datos o una matriz con los datos almacenados. Cada par clave/valor del objeto o matriz se agrega al almacén (mediante la función `setItem`):

* **Objeto:** Las claves son los nombres de propiedad.
* **Matriz:** Las claves son los índices de la matriz.

Los valores pueden ser objetos.

##### Parámetros {#parameters-addallitems}

* **`tree`:** (objeto o matriz) Los datos que se van a agregar al almacén.
* **`options`:** (objeto) Un objeto opcional de opciones que se pasa a la función setItem. Para obtener más información, vea el parámetro `options` de [`setItem(key,value,options)`](#setitem-key-value-options).

##### Devuelve {#returns-addallitems}

Un valor `boolean`:

* El valor `true` indica que se almacenó el objeto de datos.
* El valor `false` indica que el almacén de datos no ha cambiado.

#### addReference(key, otherKey) {#addreference-key-anotherkey}

Crea una referencia de una clave a otra. Una clave no puede hacer referencia a sí misma.

##### Parámetros {#parameters-addreference}

* **`key`:** La clave que hace referencia a `anotherKey`.

* **`anotherkey`:** Son claves a las que hace referencia `key`.

##### Devuelve {#returns-addreference}

Un valor `boolean`:

* El valor `true` indica que se agregó la referencia.
* El valor `false` indica que no se agregó ninguna referencia.

#### announcementReadiness() {#announcereadiness}

Almacena en déclencheur el evento `ready` para este almacén. Esta función no tiene parámetros y no devuelve ningún valor.

#### clean() {#clean}

Quita todos los datos del almacén. La función no tiene parámetros ni valor devuelto.

#### getItem(key) {#getitem-key}

Devuelve el valor asociado a una clave.

##### Parámetros {#parameters-getitem}

* **`key`:** (String) Clave para la que se devuelve el valor.

##### Devuelve {#returns-getitem}

Object que representa el valor de la clave.

#### getKeys(includeInternals) {#getkeys-includeinternals}

Recupera las claves del almacén. Opcionalmente, puede recuperar las claves que utiliza internamente el marco de trabajo de ContextHub.

##### Parámetros {#parameters-getkeys}

* **`includeInternals`:** Un valor de `true` incluye claves usadas internamente en los resultados. Estas claves comienzan por el carácter de subrayado (`_`). El valor predeterminado es `false`.

##### Devuelve {#returns-getkeys}

Una matriz de nombres de claves (`string` valores).

#### getReferences() {#getreferences}

Recupera las referencias del almacén.

##### Devuelve {#returns-getreferences}

Matriz que utiliza claves de referencia como índices para las claves a las que se hace referencia:

* Las claves de referencia corresponden al parámetro `key` de la función `addReference`.
* Las claves a las que se hace referencia se corresponden con el parámetro `anotherKey` de la función `addReference`.

#### getTree(includeInternals) {#gettree-includeinternals}

Recupera el árbol de datos del almacén. Opcionalmente, puede incluir los pares clave/valor que utiliza internamente el marco de trabajo de ContextHub.

##### Parámetros {#parameters-gettree}

* `includeInternals:` Un valor de `true` incluye pares clave/valor usados internamente en los resultados. Las claves de estos datos comienzan con el carácter de subrayado (`_`). El valor predeterminado es `false`.

##### Devuelve {#returns-gettree}

Objeto que representa el árbol de datos. Las claves son los nombres de propiedad del objeto.

#### init(nombre, configuración) {#init-name-config}

Inicializa el almacén.

* Establece los datos de almacén en un objeto vacío.
* Establece las referencias de almacén en un objeto vacío.
* `eventChannel` es `data:<name>`, donde `<name>` es el nombre del almacén.
* `storeDataKey` es `/store/<name>`, donde `<name>` es el nombre del almacén.

##### Parámetros {#parameters-init}

* **`name`:** El nombre del almacén.
* **`config`:** Un objeto que contiene propiedades de configuración:
   * `eventDeferring`: el valor predeterminado es 32.
   * `eventing`: el objeto [ContextHub.Utils.Eventing](#contexthub-utils-eventing) para este almacén. El valor predeterminado es el objeto `ContextHub.eventing` que utiliza.
   * `persistence`: el objeto `ContextHub.Utils.Persistence` para este almacén. El valor predeterminado es el objeto `ContextHub.persistence`.

#### isEventingPaused() {#iseventingpaused}

Determina si el evento está en pausa para este almacén.

##### Devuelve {#returns-iseventingpaused}

Un valor booleano:

* `true`: el evento está en pausa para que no se desencadenen eventos para este almacén.
* `false`: el evento no está en pausa para que se activen eventos para este almacén.

#### pauseEventing() {#pauseeventing}

Pausa los eventos del almacén para que no se desencadene ningún evento. Esta función no requiere parámetros y no devuelve ningún valor.

#### removeItem(key, options) {#removeitem-key-options}

Quita un par clave/valor del almacén.

Cuando se quita una clave, la función almacena en déclencheur el evento `data`. Los datos del evento incluyen el nombre del almacén, el nombre de la clave que se eliminó, el valor que se eliminó, el nuevo valor de la clave (nulo) y el tipo de acción &quot;quitar&quot;.

Opcionalmente, puede evitar que se active el evento `data`.

##### Parámetros {#parameters-removeitem}

* **`key`:** (String) El nombre de la clave que se va a quitar.
* **`options`:** (objeto) Un objeto de opciones. Las siguientes propiedades de objeto son válidas:
   * silencioso: un valor de `true` impide que se active el evento `data`. El valor predeterminado es `false`.

##### Devuelve {#returns-removeitem}

Un valor `boolean`:

* El valor `true` indica que se quitó el par clave/valor.
* El valor `false` indica que el almacén de datos no se ha modificado porque la clave no se encontró en el almacén.

#### removeReference(key) {#removereference-key}

Quita una referencia del almacén.

##### Parámetros {#parameters-removereference}

* **`key`:** La referencia de clave que se va a quitar. Este parámetro corresponde al parámetro `key` de la función `addReference`.

##### Devuelve {#returns-removereference}

Un valor `boolean`:

* El valor `true` indica que se quitó la referencia.
* El valor `false` indica que la clave no era válida y que el almacén no se ha modificado.

#### reset(keepRemainingData) {#reset-keepremainingdata}

Restablece los valores iniciales de los datos persistentes del almacén. De forma opcional, puede eliminar todos los demás datos del almacén. El evento se detiene para este almacén mientras se restablece el almacén. Esta función no devuelve ningún valor.

Los valores iniciales se proporcionan en la propiedad `initialValues` del objeto de configuración que se utiliza para crear una instancia del objeto de almacén.

##### Parámetros {#parameters-reset}

* **`keepRemainingData`**: (Booleano) Un valor de true hace que se mantengan los datos no iniciales. El valor false hace que se eliminen todos los datos excepto los valores iniciales.

#### resolveReference(key, retry) {#resolvereference-key-retry}

Recupera una clave referenciada. De forma opcional, puede especificar el número de iteraciones que se utilizarán para resolver la mejor coincidencia.

##### Parámetros {#parameters-resolvereference}

* **`key`:** (String) Clave para la que se va a resolver la referencia. Este parámetro `key` corresponde al parámetro `key` de la función `addReference`.
* **`retry`:** (Número) El número de iteraciones que se van a utilizar.

##### Devuelve {#returns-resolvereference}

Un valor `string` que representa la clave a la que se hace referencia. Si no se resuelve ninguna referencia, se devuelve el valor del parámetro `key`.

#### resumeEventing() {#resumeeventing}

Reanuda los eventos de este almacén para que se activen eventos. Esta función no define parámetros y no devuelve ningún valor.

#### setItem(clave, valor, opciones) {#setitem-key-value-options}

Agrega un par clave/valor al almacén.

Almacena en déclencheur el evento `data` solo si el valor de la clave es diferente del valor almacenado actualmente para la clave. Opcionalmente, puede evitar que se active el evento `data`.

Los datos del evento incluyen el nombre del almacén, la clave, el valor anterior, el nuevo valor y el tipo de acción de `set`.

##### Parámetros {#parameters-setitem}

* **`key`:** (String) El nombre de la clave.
* **`options`:** (objeto) Un objeto de opciones. Las siguientes propiedades de objeto son válidas:
   * `silent`: un valor de `true` impide que se active el evento `data`. El valor predeterminado es `false`.
* **`value`:** (objeto) valor que se va a asociar con la clave.

##### Devuelve {#returns-setitem}

Un valor `boolean`:

* El valor `true` indica que se almacenó el objeto de datos.
* El valor `false` indica que el almacén de datos no ha cambiado.

## ContextHub.Store.JSONPStore {#contexthub-store-jsonpstore}

Un almacén que contiene datos JSON. Los datos se recuperan de un servicio JSONP externo o, opcionalmente, de un servicio que devuelve datos JSON. Especifique los detalles del servicio mediante la función [`init`](#init-name-config) al crear una instancia de esta clase.

El almacén utiliza la persistencia en memoria (variable JavaScript). Los datos de almacenamiento solo están disponibles durante la duración de la página.

ContextHub.Store.JSONPStore amplía [ContextHub.Store.Core](#contexthub-store-core) y hereda las funciones de esa clase.

### Funciones (ContextHub.Store.JSONPStore) {#functions-contexthub-store-jsonpstore}

#### configureService(serviceConfig, override) {#configureservice-serviceconfig-override}

Configura los detalles para conectarse al servicio JSONP que utiliza este objeto. Puede actualizar o reemplazar la configuración existente. La función no devuelve ningún valor.

##### Parámetros {#parameters-configureservice}

* **`serviceConfig`:** Un objeto que contiene las siguientes propiedades:
   * `host`: (Cadena) El nombre del servidor o la dirección IP.
   * `jsonp`: (Booleano) Un valor de true indica que el servicio es un servicio JSONP; en caso contrario, false. Cuando es true, la llamada de retorno {callback}: &quot;ContextHub.Callbacks.El objeto *Object.name*} se ha agregado al objeto service.params.
   * `params`: parámetros de URL (objeto) representados como propiedades de objeto. Los nombres de parámetro son nombres de propiedad y los valores de parámetro son valores de propiedad.
   * `path`: (Cadena) Ruta de acceso al servicio.
   * `port`: (Número) El número de puerto del servicio.
   * `secure`: (Cadena o Booleano) Determina el protocolo que se utilizará para la URL del servicio:
      * `auto`: //
      * `true`: https://
      * `false`: http://
* **invalidación:** (booleano). Un valor de `true` hace que la configuración del servicio existente se reemplace por las propiedades de `serviceConfig`. Un valor de `false` hace que las propiedades de configuración del servicio existentes se combinen con las propiedades de `serviceConfig`.

#### getRawResponse() {#getrawresponse}

Devuelve la respuesta sin procesar almacenada en caché desde la última llamada al servicio JSONP. La función no requiere parámetros.

##### Devuelve {#returns-getrawresponse}

Un objeto que representa la respuesta sin procesar.

#### getServiceDetails() {#getservicedetails}

Recupera el objeto de servicio para este objeto ContextHub.Store.JSONPStore. El objeto de servicio contiene la información necesaria para crear la dirección URL del servicio.

##### Devuelve {#returns-getservicedetails}

Un objeto con las siguientes propiedades:

* **`host`:** (String) El nombre del servidor o la dirección IP.
* **`jsonp`:** (Booleano) Un valor de true indica que el servicio es un servicio JSONP, false en caso contrario. Cuando es true, la llamada de retorno {callback}: &quot;ContextHub.Callbacks.El objeto *Object.name*} se ha agregado al objeto service.params.
* **`params`:** parámetros de URL (objeto) representados como propiedades de objeto. Los nombres de parámetro son nombres de propiedad y los valores de parámetro son valores de propiedad.
* **`path`:** (String) La ruta de acceso al servicio.
* **`port`:** (Número) El número de puerto del servicio.
* **`secure`:** (cadena o booleano) Determina el protocolo que se utilizará para la URL del servicio:
   * `auto`: //
   * `true`: https://
   * `false`: http://

#### getServiceURL(resolve) {#getserviceurl-resolve}

Recupera la dirección URL del servicio JSONP.

##### Parámetros {#parameters-getserviceurl}

* **`resolve`:** (booleano) Determina si se deben incluir los parámetros resueltos en la dirección URL. Un valor de `true` resuelve los parámetros y `false` no.

##### Devuelve {#returns-getserviceurl}

Valor `string` que representa la dirección URL del servicio.

#### init(nombre, configuración) {#init-name-config-1}

inicializa el objeto `ContextHub.Store.JSONPStore`.

##### Parámetros {#parameters-init-1}

* **`name`:** (String) El nombre del almacén.
* **`config`:** (objeto) Un objeto que contiene la propiedad del servicio. El objeto JSONPStore utiliza las propiedades del objeto `service` para construir la dirección URL del servicio JSONP:
   * `eventDeferring`: 32.
   * `eventing`: el objeto ContextHub.Utils.Eventing de este almacén. El valor predeterminado es el objeto `ContextHub.eventing`.
   * `persistence`: el objeto ContextHub.Utils.Persistence de este almacén. De forma predeterminada, se utiliza la persistencia de la memoria (objeto JavaScript).
   * `service`: (objeto)
      * `host`: (Cadena) El nombre del servidor o la dirección IP.
      * `jsonp`: (Booleano) Un valor de true indica que el servicio es un servicio JSONP; en caso contrario, false. Cuando es verdadero, el objeto `{callback: "ContextHub.Callbacks.*Object.name*}` se agrega a `service.params`.
      * `params`: parámetros de URL (objeto) representados como propiedades de objeto. Los nombres y valores de parámetro son los nombres y valores de las propiedades de objeto, respectivamente.
      * `path`: (Cadena) Ruta de acceso al servicio.
      * `port`: (Número) El número de puerto del servicio.
      * `secure`: (Cadena o Booleano) Determina el protocolo que se utilizará para la URL del servicio:
         * `auto`: //
         * `true`: https://
         * `false`: http://
      * `timeout`: (Número) Cantidad de tiempo que se debe esperar para que el servicio JSONP responda antes de que se agote el tiempo de espera, en milisegundos.
         * `ttl`: cantidad mínima de tiempo en milisegundos que transcurre entre llamadas al servicio JSONP. (Consulte la función [queryService](#queryservice-reload)).

#### queryService(reload) {#queryservice-reload}

Consulta el servicio JSONP remoto y almacena en caché la respuesta. Si el tiempo desde la llamada anterior a esta función es menor que el valor de `config.service.ttl`, no se llama al servicio y la respuesta almacenada en caché no cambia. De forma opcional, puede forzar la llamada al servicio. La propiedad `config.service.ttl`se establece al llamar a la función [init](#init-name-config) para inicializar el almacén.

Almacena en déclencheur el evento ready cuando finaliza la consulta. Si no se establece la dirección URL del servicio JSONP, la función no hace nada.

##### Parámetros {#parameters-queryservice}

* **`reload`:** (Booleano) Un valor de true quita la respuesta almacenada en caché y fuerza la llamada al servicio JSONP.

#### restablecer {#reset}

Restablece los valores iniciales de los datos persistentes del almacén y, a continuación, llama al servicio JSONP. De forma opcional, puede eliminar todos los demás datos del almacén. El evento se detiene para este almacén mientras se restablecen los valores iniciales. Esta función no devuelve ningún valor.

Los valores iniciales se proporcionan en la propiedad initialValues del objeto de configuración que se utiliza para crear una instancia del objeto de almacén.

##### Parámetros {#parameters-reset-1}

* **`keepRemainingData`:** (Booleano) Un valor de true hace que persistan los datos no iniciales. El valor false hace que se eliminen todos los datos excepto los valores iniciales.

#### resolveParameter(f) {#resolveparameter-f}

Resuelve el parámetro dado.

## ContextHub.Store.PersistedJSONPStore {#contexthub-store-persistedjsonpstore}

`ContextHub.Store.PersistedJSONPStore` amplía [ContextHub.Store.JSONPStore](#contexthub-store-jsonpstore), de modo que hereda todas las funciones de esa clase. Sin embargo, los datos recuperados del servicio JSONP se conservan según la configuración de persistencia de ContextHub. (Consulte [Modos de persistencia:](adding-contexthub.md#persistence-modes))

## ContextHub.Store.PersistedStore {#contexthub-store-persistedstore}

`ContextHub.Store.PersistedStore` amplía [ContextHub.Store.Core](#contexthub-store-core) de modo que hereda todas las funciones de esa clase. Los datos de este almacén se conservan según la configuración de persistencia de ContextHub.

## ContextHub.Store.SessionStore {#contexthub-store-sessionstore}

`ContextHub.Store.SessionStore` amplía [ContextHub.Store.Core](#contexthub-store-core) de modo que hereda todas las funciones de esa clase. Los datos de este almacén se conservan utilizando la persistencia en memoria (objeto JavaScript).

## ContextHub.UI {#contexthub-ui}

Administra los módulos de IU y los procesadores de módulos de IU.

### Funciones (ContextHub.UI) {#functions-contexthub-ui}

#### registerRenderer(moduleType, renderer, dontRender) {#registerrenderer-moduletype-renderer-dontrender}

Registra un procesador de módulos de IU con ContextHub. Una vez registrado el procesador, se puede usar para [crear módulos de IU](configuring-contexthub.md#adding-a-ui-module). Utilice esta función cuando esté [ampliando `ContextHub.UI.BaseModuleRenderer`](extending-contexthub.md#creating-contexthub-ui-module-types) para crear un procesador de módulos de IU personalizado.

##### Parámetros {#parameters-registerrenderer}

* **`moduleType`:** (Cadena) Identificador del procesador del módulo de interfaz de usuario. Si un procesador ya está registrado con el valor especificado, el procesador existente no estará registrado antes de que se registre este procesador.
* **`renderer`:** (String) Nombre de la clase que procesa el módulo de interfaz de usuario.
* **`dontRender`:** (booleano) Se establece en `true` para evitar que la interfaz de usuario de ContextHub se represente después de registrar el procesador. El valor predeterminado es `false`.

##### Ejemplos {#example-registerrenderer}

En el ejemplo siguiente se registra un procesador como tipo de módulo `contexthub.browserinfo`.

```javascript
ContextHub.UI.registerRenderer('contexthub.browserinfo', new SurferinfoRenderer());
```

## ContextHub.Utils.Cookie {#contexthub-utils-cookie}

Una clase de utilidad para interactuar con cookies.

### Funciones (ContextHub.Utils.Cookie) {#functions-contexthub-utils-cookie}

#### exists(key) {#exists-key}

Determina si existe una cookie.

##### Parámetros {#parameters-exists}

* **`key`:** Un `String` que contiene la clave de la cookie que está probando.

##### Devuelve {#returns-exists}

El valor `boolean` true indica que la cookie existe.

##### Ejemplos {#example-exists}

```javascript
if (ContextHub.Utils.Cookie.exists("name")) {
   // conditionally-executed code
}
```

#### getAllItems(filtro) {#getallitems-filter}

Devuelve todas las cookies que tienen claves que coinciden con un filtro.

##### Parámetros {#parameters-getallitems}

* **`filter`:** (opcional) criterios para claves de cookies coincidentes. Para devolver todas las cookies, no especifique ningún valor. Se admiten los siguientes tipos:
   * Cadena: La cadena se compara con la clave de la cookie.
   * Matriz: cada elemento de la matriz es un filtro.
   * Un objeto RegExp: la función de prueba del objeto se utiliza para hacer coincidir claves de cookie.
   * Una función: Una función que prueba una clave de cookie para detectar una coincidencia. La función debe tomar la clave de cookie como parámetro y devolver true si la prueba confirma una coincidencia.

##### Devuelve {#returns-getallitems}

Un objeto de cookies. Las propiedades de objeto son claves de cookie y los valores de clave son valores de cookie.

##### Ejemplos {#example-getallitems}

```javascript
ContextHub.Utils.Cookie.getAllItems([/^cq-authoring/, /^cq-editor/])
```

#### getItem(key) {#getitem-key-1}

Devuelve un valor de cookie.

##### Parámetros {#parameters-getitem-1}

* **`key`:** La clave de la cookie para la que desea obtener el valor.

##### Devuelve {#returns-getitem-1}

El valor de la cookie o `null` si no se encontró ninguna cookie para la clave.

##### Ejemplos {#example-getitem-1}

```javascript
ContextHub.Utils.Cookie.getItem("name");
```

#### getKeys(filtro) {#getkeys-filter}

Devuelve una matriz de claves de cookies existentes que coinciden con un filtro.

##### Parámetros {#parameters-getkeys-1}

* **`filter`:** Criterios para claves de cookies coincidentes. Se admiten los siguientes tipos:
   * Cadena: La cadena se compara con la clave de la cookie.
   * Matriz: cada elemento de la matriz es un filtro.
   * Un objeto RegExp: la función de prueba del objeto se utiliza para hacer coincidir claves de cookie.
   * Una función: Una función que prueba una clave de cookie para detectar una coincidencia. La función debe tomar la clave de cookie como parámetro y devolver `true` si la prueba confirma una coincidencia.

##### Devuelve {#returns-getkeys-1}

Matriz de cadenas en la que cada cadena es la clave de una cookie que coincide con el filtro.

##### Ejemplos {#example-getkeys-1}

```javascript
ContextHub.Utils.Cookie.getKeys([/^cq-authoring/, /^cq-editor/])
```

#### removeItem(key, options) {#removeitem-key-options-1}

Quita una cookie. Para eliminar la cookie, el valor se establece en una cadena vacía y la fecha de caducidad se establece en el día anterior a la fecha actual.

##### Parámetros {#parameters-removeitem-1}

* **`key`:** Un valor `String` que representa la clave de la cookie que se va a quitar.
* **`options`:** Un objeto que contiene valores de propiedad para configurar los atributos de la cookie. Consulte la función [`setItem`](#setitem-key-value-options) para obtener información. La propiedad `expires` no tiene ningún efecto.

##### Devuelve {#returns-removeitem-1}

Esta función no devuelve un valor.

##### Ejemplos {#example-removeitem-1}

```javascript
ContextHub.Utils.Cookie.vanish([/^cq-authoring/, 'cq-scrollpos']);
```

#### setItem(clave, valor, opciones) {#setitem-key-value-options-1}

Crea una cookie de la clave y el valor dados y agrega la cookie al documento actual. Opcionalmente, puede especificar opciones que configuren los atributos de la cookie.

##### Parámetros {#parameters-setitem-1}

* **`key`:** Una cadena que contiene la clave de la cookie.
* **`value`:** Una cadena que contiene el valor de la cookie.
* **`options`:** (opcional) un objeto que contiene cualquiera de las siguientes propiedades que configuran los atributos de la cookie:
   * `expires`: un valor `date` o `number` que especifica cuándo caduca la cookie. Un valor de fecha especifica la hora absoluta de caducidad. Un número (en días) establece la hora de caducidad para la hora actual más el número. El valor predeterminado es `undefined`.
   * `secure`: un valor `boolean` que especifica el atributo `Secure` de la cookie. El valor predeterminado es `false`.
   * `path`: un valor `String` para usar como atributo `Path` de la cookie. El valor predeterminado es `undefined`.

##### Devuelve {#returns-setitem-1}

La cookie con el valor establecido.

##### Ejemplos {#example-setitem-1}

```javascript
ContextHub.Utils.Cookie.setItem("name", "mycookie", {
    expires: 3,
    domain: 'localhost',
    path: '/some/directory',
    secure: true
});
```

#### desvanecer(filtro, opciones) {#vanish-filter-options}

Elimina todas las cookies que coinciden con un filtro determinado. Las cookies se comparan mediante la función `getKeys` y se eliminan mediante la función `removeItem`.

##### Parámetros {#parameters-vanish}

* **`filter`:** Argumento `filter` que se va a usar en la llamada a la función [`getKeys`](#getkeys-filter).
* **`options`:** Argumento `options` que se va a usar en la llamada a la función [`removeItem`](#removeitem-key-options).

##### Devuelve {#returns-vanish}

Esta función no devuelve un valor.

## ContextHub.Utils.Eventing {#contexthub-utils-eventing}

Permite enlazar y desenlazar funciones a eventos de tienda de ContextHub. Tener acceso a `ContextHub.Utils.Eventing` objetos de un almacén mediante la propiedad [eventing](#eventing) del almacén.

### Funciones (ContextHub.Utils.Eventing) {#functions-contexthub-utils-eventing}

#### off(nombre, selector) {#off-name-selector}

Desenlaza una función de un evento.

##### Parámetros {#parameters-off}

* **`name`:** El [nombre del evento](#contexthub-utils-eventing) para el que está desenlazando la función.
* **`selector`:** El selector que identifica el enlace. (Consulte el parámetro `selector` para las funciones [`on`](#on-name-handler-selector-triggerforpastevents) y [`once`](#once-name-handler-selector-triggerforpastevents)).

##### Devuelve {#returns-off}

Esta función no devuelve ningún valor.

#### on(nombre, controlador, selector, triggerForPastEvents) {#on-name-handler-selector-triggerforpastevents}

Enlaza una función a un evento. Se llama a la función cada vez que se produce el evento. De forma opcional, se puede llamar a la función para eventos que se han producido en el pasado, antes de que se establezca el enlace.

##### Parámetros {#parameters-on}

* **`name`:** (String) El [nombre del evento](#contexthub-utils-eventing) al que está enlazando la función.
* **`handler`:** (Función) La función para enlazar al evento.
* **`selector`:** (String) Identificador único del enlace. Necesita el selector para identificar el enlace si desea utilizar la función `off` para quitar el enlace.
* **`triggerForPastEvents`:** (booleano) indica si el controlador debe ejecutarse para los eventos que ocurrieron anteriormente. Un valor de `true` llama al controlador para eventos anteriores. Un valor de `false` llama al controlador para eventos futuros. El valor predeterminado es `true`.

##### Devuelve {#returns-on}

Cuando el argumento `triggerForPastEvents` es `true`, esta función devuelve un valor `boolean` que indica si el evento se produjo en el pasado:

* `true`: el evento se produjo anteriormente y se llamó al controlador.
* `false`: el evento no se ha producido anteriormente.

Si `triggerForPastEvents` es `false`, esta función no devuelve ningún valor.

##### Ejemplos {#example-on}

En el ejemplo siguiente se enlaza una función al evento de datos del almacén de geolocalización. La función rellena un elemento de la página con el valor del elemento de datos de latitud del almacén.

```html
<div class="location">
    <p>latitude: <span id="lat"></span></p>
</div>

<script>
    var geostore = ContextHub.getStore("geolocation");
    geostore.eventing.on(ContextHub.Constants.EVENT_DATA_UPDATE,getlat,"getlat");

    function getlat(){
       latitude = geostore.getItem("latitude");
       $("#lat").html(latitude);
    }
</script>
```

#### once(nombre, controlador, selector, triggerForPastEvents) {#once-name-handler-selector-triggerforpastevents}

Enlaza una función a un evento. La función se llama solo una vez, para la primera aparición del evento. De forma opcional, se puede llamar a la función para el evento que se ha producido en el pasado, antes de que se establezca el enlace.

##### Parámetros {#parameters-once}

* **`name`:** (String) El [nombre del evento](#contexthub-utils-eventing) al que está enlazando la función.
* **`handler`:** (Función) La función para enlazar al evento.
* **`selector`:** (String) Identificador único del enlace. Necesita el selector para identificar el enlace si desea utilizar la función `off` para quitar el enlace.
* **`triggerForPastEvents`:** (booleano) indica si el controlador debe ejecutarse para los eventos que ocurrieron anteriormente. Un valor de `true` llama al controlador para eventos anteriores. Un valor de `false` llama al controlador para eventos futuros. El valor predeterminado es `true`.

##### Devuelve {#returns-once}

Cuando el argumento `triggerForPastEvents` es `true`, esta función devuelve un valor `boolean` que indica si el evento se produjo en el pasado:

* `true`: el evento se produjo anteriormente y se llamó al controlador.
* `false`: el evento no se ha producido anteriormente.

Si `triggerForPastEvents` es `false`, esta función no devuelve ningún valor.

## ContextHub.Utils.inheritance {#contexthub-utils-inheritance}

Clase de utilidad que permite a un objeto heredar las propiedades y los métodos de otro objeto.

### Funciones (ContextHub.Utils.inheritance) {#functions-contexthub-utils-inheritance}

#### inherit(secundario, principal) {#inherit-child-parent}

Hace que un objeto herede las propiedades y métodos de otro objeto.

##### Parámetros {#parameters-inherit}

* **`child`:** (objeto) El objeto que hereda.
* **`parent`:** (objeto) objeto que define las propiedades y los métodos heredados.

## ContextHub.Utils.JSON {#contexthub-utils-json}

Proporciona funciones para serializar objetos en formato JSON y deserializar cadenas JSON en objetos.

### Funciones (ContextHub.Utils.JSON) {#functions-contexthub-utils-json}

#### parse(datos) {#parse-data}

Analiza un valor de cadena como JSON y lo convierte en un objeto javascript.

##### Parámetros {#parameters-parse}

* **`data`:** Un valor de cadena en formato JSON.

##### Devuelve {#returns-parse}

Un objeto JavaScript.

##### Ejemplos {#example-parse}

El código:

```javascript
ContextHub.Utils.JSON.parse("{'city':'Basel','country':'Switzerland','population':'173330'}");
```

Devuelve el siguiente objeto:

```javascript
Object {
   city: "Basel",
   country: "Switzerland",
   population: 173330
}
```

#### stringify(data) {#stringify-data}

Serializa valores y objetos JavaScript en valores de cadena en formato JSON.

##### Parámetros {#parameters-stringify}

* **`data`:** Valor u objeto que se va a serializar. Esta función admite valores booleanos, de matriz, numéricos, de cadena y de fecha.

##### Devuelve {#returns-stringify}

El valor de cadena serializado. Cuando `data` es un valor R `egExp`, esta función devuelve un objeto vacío. Cuando `data` es una función, devuelve `undefined`.

##### Ejemplos {#example-stringify}

El siguiente código:

```javascript
ContextHub.Utils.JSON.stringify({
   city: "Basel",
   country: "Switzerland",
   population: 173330
});
```

Devuelve:

```javascript
"{'city':'Basel','country':'Switzerland','population':'173330'}":
```

## ContextHub.Utils.JSON.tree {#contexthub-utils-json-tree}

Esta clase facilita la manipulación de los objetos de datos que se van a almacenar o recuperar de los almacenes de ContextHub.

### Funciones (ContextHub.Utils.JSON.tree) {#functions-contexthub-utils-json-tree}

#### addAllItems() {#addallitems}

Crea una copia de un objeto de datos y le agrega el árbol de datos a partir de un segundo objeto. La función devuelve la copia y no modifica ninguno de los objetos originales. Cuando los árboles de datos de los dos objetos contienen claves idénticas, el valor del segundo objeto sobrescribe el valor del primer objeto.

##### Parámetros {#parameters-addallitems-1}

* **`tree`:** El objeto que se copia.
* **`secondTree`:** El objeto que se combina con la copia del objeto `tree`.

##### Devuelve {#returns-addallitems-1}

Objeto que contiene los datos combinados.

#### cleanup() {#cleanup}

Crea una copia de un objeto, busca y quita elementos en el árbol de datos que no contienen valores, valores nulos o valores indefinidos, y devuelve la copia.

##### Parámetros {#parameters-cleanup}

* **`tree`:** El objeto que se va a limpiar.

##### Devuelve {#returns-cleanup}

Una copia del árbol que se ha limpiado.

#### getItem() {#getitem}

Recupera el valor de un objeto para la clave.

##### Parámetros {#parameters-getitem-2}

* **`tree`:** El objeto de datos.
* **`key`:** Clave del valor que desea recuperar.

##### Devuelve {#returns-getitem-2}

El valor que corresponde a la clave. Cuando la clave tiene claves secundarias, esta función devuelve un objeto complejo. Cuando el tipo del valor de la clave es `undefined`, se devuelve `null`.

##### Ejemplos {#example-getitem-2}

Considere el siguiente objeto de JavaScript:

```javascript
myObject {
  user: {
    location: {
      city: "Basel",
        details: {
          population: 173330,
          elevation: 260
        }
      }
    }
  }
```

El siguiente código de ejemplo devuelve el valor `260`:

```javascript
ContextHub.Utils.JSON.tree.getItem(myObject, "/user/location/details/elevation");
```

El siguiente código de ejemplo recupera el valor de una clave que tiene claves secundarias:

```javascript
ContextHub.Utils.JSON.tree.getItem(myObject, "/user");
```

La función devuelve el siguiente objeto:

```javascript
Object {
  location: {
    city: "Basel",
    details: {
      population: 173330,
      elevation: 260
    }
  }
}
```

#### getKeys() {#getkeys}

Recupera todas las claves del árbol de datos de un objeto. De forma opcional, puede recuperar únicamente las claves secundarias de una clave específica. Si lo desea, también puede especificar un orden de las claves recuperadas.

##### Parámetros {#parameters-getkeys-2}

* **`tree`:** El objeto del que se recuperarán las claves del árbol de datos.
* **`parent`:** (opcional) clave de un elemento del árbol de datos del que desea recuperar las claves de los elementos secundarios.
* **`order`:** (opcional) una función que determina el orden de las claves devueltas. (Consulte [`Array.prototype.sort`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/sort) en Mozilla Developer Network).

##### Devuelve {#returns-getkeys-2}

Una matriz de claves.

##### Ejemplos {#example-getkeys-2}

Considere el siguiente objeto:

```javascript
myObject {
  location: {
    weather: {
      temperature: "28C",
      humidity: "77%",
      precipitation: "10%",
      wind: "8km/h"
    },
    city: "Basel",
    country: "Switzerland",
    longitude: 7.5925727,
    latitude: 47.557421
  }
}
```

El script `ContextHub.Utils.JSON.tree.getKeys(myObject);` devuelve la siguiente matriz:

```javascript
["/location", "/location/city", "/location/country", "/location/latitude", "/location/longitude", "/location/weather", "/location/weather/humidity", "/location/weather/precipitation", "/location/weather/temperature", "/location/weather/wind"]
```

#### removeItem() {#removeitem}

Crea una copia de un objeto determinado, quita la rama especificada del árbol de datos y devuelve la copia modificada.

##### Parámetros {#parameters-removeitem-2}

* **`tree`:** Un objeto de datos.
* **`key`:** La clave que se va a quitar.

##### Devuelve {#returns-removeitem-2}

Una copia del objeto de datos original sin la clave.

##### Ejemplos {#example-removeitem-2}

Considere el siguiente objeto:

```javascript
myObject {
  one: {
    foo: "bar",
    two: {
      three: {
        four: {
          five: 5,
          six: 6
        }
      }
    }
  }
}
```

La siguiente secuencia de comandos de ejemplo elimina la rama /uno/dos/tres/cuatro del árbol de datos:

```javascript
myObject = ContextHub.Utils.JSON.tree.removeItem(myObject, "/one/two/three/four");
```

La función devuelve el siguiente objeto:

```javascript
myObject {
  one: {
    foo: "bar"
  }
}
```

#### sanitizeKey(key) {#sanitizekey-key}

Sanea los valores de cadena para que se puedan utilizar como claves. Para sanear una cadena, esta función realiza las siguientes acciones:

* Reduce varias barras diagonales consecutivas a una sola barra.
* Elimina los espacios en blanco del principio y del final de la cadena.
* Divide el resultado en una matriz de cadenas delimitadas por barras oblicuas.

Utilice la matriz resultante para crear una clave utilizable.

##### Parámetros {#parameters-sanitizekey}

* **`key`:** `string` para sanear.

##### Devuelve {#returns-sanitizekey}

Matriz de `string` valores donde cada cadena es la parte de `key` que fue demarcada con barras oblicuas. representa la clave saneada. Si la matriz saneada tiene una longitud de cero, esta función devuelve `null`.

##### Ejemplos {#example-sanitizekey}

El siguiente código sanea una cadena para producir la matriz `["this", "is", "a", "path"]` y, a continuación, genera la clave `"/this/is/a/path"` de la matriz:

```javascript
var key = " / this////is/a/path ";
ContextHub.Utils.JSON.tree.sanitizeKey(key)
"/" + ContextHub.Utils.JSON.tree.sanitizeKey(key).join("/");
```

#### setItem(árbol, clave, valor) {#setitem-tree-key-value}

Agrega un par clave/valor al árbol de datos de una copia de un objeto. Para obtener información acerca de los árboles de datos, vea [Persistencia.](contexthub.md#persistence)

##### Parámetros {#parameters-setitem-2}

* **`tree`:** Un objeto de datos.
* **`key`:** Clave que se va a asociar con el valor que está agregando. La clave es la ruta al elemento en el árbol de datos. Esta función llama a `ContextHub.Utils.JSON.tree.sanitize` para sanear la clave antes de agregarla.
* **`value`:** Valor que se agregará al árbol de datos.

##### Devuelve {#returns-setitem-2}

Una copia del objeto `tree` que incluye el par `key`/ `value`.

##### Ejemplos {#example-setitem-2}

Considere el siguiente código JavaScript:

```javascript
var myObject = {
     user: {
        location: {
           city: "Basel"
           }
        }
     };

var myKey = "/user/location/details";

var myValue = {
      population: 173330,
      elevation: 260
     };

myObject = ContextHub.Utils.JSON.tree.setItem(myObject, myKey, myValue);
```

## ContextHub.Utils.storeCandidates {#contexthub-utils-storecandidates}

Permite registrar candidatos de tienda y obtener candidatos de tienda registrados.

### Funciones (ContextHub.Utils.storeCandidates) {#functions-contexthub-utils-storecandidates}

#### getRegisteredCandidates(storeType) {#getregisteredcandidates-storetype}

Devuelve los tipos de almacén que están registrados como candidatos de almacén. Recupere los candidatos registrados de un tipo de tienda específico o de todos los tipos de tienda.

##### Parámetros {#parameters-getregisteredcandidates}

* **`storeType`:** (String) El nombre del tipo de almacén. Ver el parámetro `storeType` de la función [`ContextHub.Utils.storeCandidates.registerStoreCandidate`](#contexthub-utils-storecandidates).

##### Devuelve {#returns-getregisteredcandidates}

Un objeto de tipos de almacén. Las propiedades de objeto son los nombres de tipo de almacén y los valores de propiedad son una matriz de candidatos de almacén registrados.

#### getStoreFromCandidates(storeType) {#getstorefromcandidates-storetype}

Devuelve un tipo de almacén de los candidatos registrados. Si se registra más de un tipo de almacén con el mismo nombre, la función devuelve el tipo de almacén con la prioridad más alta.

##### Parámetros {#parameters-getstorefromcandidates}

* `storeType`: (Cadena) Nombre del candidato de la tienda. Ver el parámetro `storeType` de la función [`ContextHub.Utils.storeCandidates.registerStoreCandidate`](#registerstorecandidate-store-storetype-priority-applies).

##### Devuelve {#returns-getstorefromcandidates}

Un objeto que representa el candidato de almacén registrado. Si el tipo de almacén solicitado no está registrado, se genera un error.

#### getSupportedStoreTypes() {#getsupportedstoretypes}

Devuelve los nombres de los tipos de almacén que están registrados como candidatos de almacén. Esta función no requiere parámetros.

##### Devuelve {#returns-getsupportedstoretypes}

Una matriz de valores de cadena, donde cada cadena es el tipo de tienda con el que se registró un candidato a tienda. Ver el parámetro `storeType` de la función [`ContextHub.Utils.storeCandidates.registerStoreCandidate`](#contexthub-utils-storecandidates).

#### registerStoreCandidate(store, storeType, priority, applies) {#registerstorecandidate-store-storetype-priority-applies}

Registra un objeto de almacén como candidato de almacén mediante un nombre y una prioridad.

La prioridad es un número que indica la importancia de las tiendas con el mismo nombre. Cuando un candidato a tienda se registra con el mismo nombre que un candidato a tienda ya registrado, se utiliza el candidato con la prioridad más alta. Al registrar un candidato a tienda, la tienda se registra solo si la prioridad es mayor que la de los candidatos a tienda registrados con el mismo nombre.

##### Parámetros {#parameters-registerstorecandidate}

* **`store`:** (objeto) El objeto de almacén que se va a registrar como candidato de almacén.
* **`storeType`:** (String) El nombre del candidato de la tienda. Este valor es necesario al crear una instancia del candidato de tienda.
* **`priority`:** (Número) Prioridad del candidato a almacén.
* **`applies`:** (Función) La función a invocar que evalúa la aplicabilidad del almacén en el entorno actual. La función debe devolver `true` si el almacén es aplicable y `false` en caso contrario. El valor predeterminado es una función que devuelve true: `function() {return true;}`

##### Ejemplos {#example-registerstorecandidate}

```javascript
ContextHub.Utils.storeCandidates.registerStoreCandidate(myStoreCandidate,
                                'contexthub.mystorecandiate', 0);
```
