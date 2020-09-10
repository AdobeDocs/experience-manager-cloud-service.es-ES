---
title: Ampliación de ContextHub
description: Defina nuevos tipos de almacenes y módulos de ContextHub cuando los proporcionados no cumplan con los requisitos de la solución
translation-type: tm+mt
source-git-commit: ddfdcf74977adf00bc0ab01b0b1a669781f0d730
workflow-type: tm+mt
source-wordcount: '624'
ht-degree: 0%

---


# Ampliación de ContextHub {#extending-contexthub}

Defina nuevos tipos de almacenes y módulos de ContextHub cuando los proporcionados no cumplan con los requisitos de la solución.

## Creación de candidatos de tienda personalizados {#creating-custom-store-candidates}

Las tiendas de ContextHub se crean a partir de los candidatos de las tiendas registradas. Para crear una tienda personalizada, debe crear y registrar un candidato a la tienda.

<!--The javascript file that includes the code that creates and registers the store candidate must be included in a [client library folder](/help/sites-developing/clientlibs.md#creating-client-library-folders). The category of the folder must match the following pattern:-->

El archivo javascript que incluye el código que crea y registra al candidato de la tienda debe incluirse en una carpeta de la biblioteca del cliente. La categoría de la carpeta debe coincidir con el siguiente patrón:

```xml
contexthub.store.[storeType]
```

La `storeType` parte de la categoría es la `storeType` con la que está registrado el candidato a la tienda. (Consulte [Registro de un candidato](#registering-a-contexthub-store-candidate)a la tienda de ContextHub). Por ejemplo, para el valor storeType de `contexthub.mystore`, la categoría de la carpeta de la biblioteca del cliente debe ser `contexthub.store.contexthub.mystore`.

### Creación de un candidato de la tienda de ContextHub {#creating-a-contexthub-store-candidate}

Para crear un candidato a tienda, utilice la [`ContextHub.Utils.inheritance.inherit`](contexthub-api.md#inherit-child-parent) función para ampliar uno de los almacenes base:

* [`ContextHub.Store.PersistedStore`](contexthub-api.md#contexthub-store-persistedstore)
* [`ContextHub.Store.SessionStore`](contexthub-api.md#contexthub-store-sessionstore)
* [`ContextHub.Store.JSONPStore`](contexthub-api.md#contexthub-store-jsonpstore)
* [`ContextHub.Store.PersistedJSONPStore`](contexthub-api.md#contexthub-store-persistedjsonpstore)

Tenga en cuenta que cada almacén base extiende la [`ContextHub.Store.Core`](contexthub-api.md#contexthub-store-core) tienda.

El ejemplo siguiente crea la extensión más simple del candidato de `ContextHub.Store.PersistedStore` tienda:

```javascript
myStoreCandidate = function(){};
ContextHub.Utils.inheritance.inherit(myStoreCandidate,ContextHub.Store.PersistedStore);
```

De forma realista, los candidatos de la tienda personalizada definirán funciones adicionales o anularán la configuración inicial de la tienda. En el repositorio siguiente se instalan varios candidatos [a tiendas de](sample-stores.md) muestra `/libs/granite/contexthub/components/stores`.

### Registro de un candidato a la tienda de ContextHub {#registering-a-contexthub-store-candidate}

Registre un candidato a la tienda para integrarlo con el marco de trabajo de ContextHub y habilitar la creación de tiendas a partir de él. Para registrar un candidato de tienda, utilice la [`registerStoreCandidate`](contexthub-api.md#registerstorecandidate-store-storetype-priority-applies) función de la `ContextHub.Utils.storeCandidates` clase.

Al registrar un candidato a tienda, debe proporcionar un nombre para el tipo de tienda. Al crear una tienda a partir del candidato, se utiliza el tipo de tienda para identificar al candidato en el que se basa.

Al registrar un candidato a tienda, usted indica su prioridad. Cuando un candidato a tienda se registra con el mismo tipo de tienda que un candidato a tienda ya registrado, se utiliza el candidato con mayor prioridad. Por lo tanto, puede omitir los candidatos de tienda existentes con nuevas implementaciones.

```javascript
ContextHub.Utils.storeCandidates.registerStoreCandidate(myStoreCandidate,
                                'contexthub.mystorecandidate', 0);
```

En la mayoría de los casos solo se necesita un candidato y la prioridad se puede establecer en `0`, pero si le interesa puede obtener información sobre registros [más avanzados,](contexthub-api.md#registerstorecandidate-store-storetype-priority-applies) lo que permite elegir una de las pocas implementaciones de tiendas en función de la condición (`applies`) de javascript y la prioridad del candidato.

## Creación de tipos de módulos de interfaz de usuario de ContextHub {#creating-contexthub-ui-module-types}

Cree tipos de módulos de interfaz de usuario personalizados cuando los que se [instalan con ContextHub](sample-modules.md) no cumplan con sus requisitos. Para crear un tipo de módulo de interfaz de usuario, cree un nuevo procesador de módulos de interfaz de usuario ampliando la `ContextHub.UI.BaseModuleRenderer` clase y, a continuación, registrándola con `ContextHub.UI`.

Para crear un procesador de módulos de interfaz de usuario, cree un `Class` objeto que contenga la lógica que procesa el módulo de interfaz de usuario. Como mínimo, la clase debe realizar las siguientes acciones:

* Extender la `ContextHub.UI.BaseModuleRenderer` clase. Esta clase es la implementación básica para todos los procesadores de módulos de interfaz de usuario. El `Class` objeto define una propiedad denominada `extend` que se utiliza para asignar a esta clase el nombre que se está extendiendo.
* Proporcione una configuración predeterminada. Cree una `defaultConfig` propiedad. Esta propiedad es un objeto que incluye las propiedades definidas para el módulo de [`contexthub.base`](sample-modules.md#contexthub-base-ui-module-type) interfaz de usuario y cualquier otra propiedad que necesite.

La fuente de `ContextHub.UI.BaseModuleRenderer` se encuentra en `/libs/granite/contexthub/code/ui/container/js/ContextHub.UI.BaseModuleRenderer.js`.  Para registrar el procesador, utilice el [`registerRenderer`](contexthub-api.md#registerrenderer-moduletype-renderer-dontrender) método de la `ContextHub.UI` clase. Debe proporcionar un nombre para el tipo de módulo. Cuando los administradores crean un módulo de interfaz de usuario basado en este procesador, especifican este nombre.

Cree y registre la clase de procesador en una función anónima de ejecución automática. El siguiente ejemplo se basa en el código fuente del módulo de `contexthub.browserinfo` interfaz de usuario. Este módulo de interfaz de usuario es una simple extensión de la `ContextHub.UI.BaseModuleRenderer` clase.

```javascript
;(function() {

    var SurferinfoRenderer = new Class({
        extend: ContextHub.UI.BaseModuleRenderer,

        defaultConfig: {
            icon: 'coral-Icon--globe',
            title: 'Browser/OS Information',

            storeMapping: {
                surferinfo: 'surferinfo'
            },

            template:
                '<p>{{surferinfo.browser.family}} {{surferinfo.browser.version}}</p>' +
                '<p>{{surferinfo.os.name}} {{surferinfo.os.version}}</p>'
        }
    });

    ContextHub.UI.registerRenderer('contexthub.browserinfo', new SurferinfoRenderer());

}());
```

<!--The javascript file that includes the code that creates and registers the renderer must be included in a [client library folder](/help/sites-developing/clientlibs.md#creating-client-library-folders). The category of the folder must match the following pattern:-->

El archivo javascript que incluye el código que crea y registra el procesador debe incluirse en una carpeta de la biblioteca del cliente. La categoría de la carpeta debe coincidir con el siguiente patrón:

```javascript
contexthub.module.[moduleType]
```

La `[moduleType]` parte de la categoría es la `moduleType` con la que está registrado el procesador de módulos. Por ejemplo, para `moduleType` el caso de `contexthub.browserinfo`, la categoría de la carpeta de la biblioteca del cliente debe ser `contexthub.module.contexthub.browserinfo`.
