---
title: Ampliación de ContextHub
description: Defina nuevos tipos de almacenes y módulos de ContextHub cuando los proporcionados no cumplan los requisitos de la solución
exl-id: ba817c18-f8bd-485d-b043-87593a6a93b5
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '628'
ht-degree: 0%

---

# Ampliación de ContextHub {#extending-contexthub}

Defina nuevos tipos de almacenes y módulos de ContextHub cuando los proporcionados no cumplan los requisitos de la solución.

## Creación de candidatos de tienda personalizados {#creating-custom-store-candidates}

Los almacenes de ContextHub se crean a partir de candidatos de tiendas registrados. Para crear una tienda personalizada, debe crear y registrar un candidato a la tienda.

El archivo javascript que incluye el código que crea y registra al candidato de la tienda debe incluirse en un [carpeta de biblioteca cliente](/help/implementing/developing/introduction/clientlibs.md). La categoría de la carpeta debe coincidir con el siguiente patrón:

```xml
contexthub.store.[storeType]
```

La variable `storeType` parte de la categoría es `storeType` con el que está registrado el candidato a la tienda. (Consulte [Registro de un candidato a almacén de ContextHub](#registering-a-contexthub-store-candidate)). Por ejemplo, para storeType de `contexthub.mystore`, la categoría de la carpeta de biblioteca del cliente debe ser `contexthub.store.contexthub.mystore`.

### Creación de un candidato de almacén de ContextHub {#creating-a-contexthub-store-candidate}

Para crear un candidato de tienda, utilice el [`ContextHub.Utils.inheritance.inherit`](contexthub-api.md#inherit-child-parent) para ampliar uno de los almacenes base:

* [`ContextHub.Store.PersistedStore`](contexthub-api.md#contexthub-store-persistedstore)
* [`ContextHub.Store.SessionStore`](contexthub-api.md#contexthub-store-sessionstore)
* [`ContextHub.Store.JSONPStore`](contexthub-api.md#contexthub-store-jsonpstore)
* [`ContextHub.Store.PersistedJSONPStore`](contexthub-api.md#contexthub-store-persistedjsonpstore)

Tenga en cuenta que cada almacén base amplía la variable [`ContextHub.Store.Core`](contexthub-api.md#contexthub-store-core) tienda.

El ejemplo siguiente crea la extensión más simple de la variable `ContextHub.Store.PersistedStore` candidato de tienda:

```javascript
myStoreCandidate = function(){};
ContextHub.Utils.inheritance.inherit(myStoreCandidate,ContextHub.Store.PersistedStore);
```

De forma realista, los candidatos de tiendas personalizadas definirán funciones adicionales o anularán la configuración inicial de la tienda. Varios [candidatos al almacén de muestras](sample-stores.md) están instalados en el repositorio siguiente `/libs/granite/contexthub/components/stores`.

### Registro de un candidato a almacén de ContextHub {#registering-a-contexthub-store-candidate}

Registre un candidato a almacén para integrarlo con el marco de ContextHub y permitir que se creen almacenes a partir de él. Para registrar a un candidato a tienda, use el [`registerStoreCandidate`](contexthub-api.md#registerstorecandidate-store-storetype-priority-applies) de la función `ContextHub.Utils.storeCandidates` Clase .

Al registrar un candidato a tienda, debe proporcionar un nombre para el tipo de tienda. Al crear un almacén a partir del candidato, se utiliza el tipo de almacén para identificar el candidato en el que se basa.

Al registrar un candidato a tienda, usted indica su prioridad. Cuando se registra un candidato de tienda con el mismo tipo de tienda que un candidato de tienda ya registrado, se utiliza el candidato con mayor prioridad. Por lo tanto, puede anular los candidatos de tienda existentes con nuevas implementaciones.

```javascript
ContextHub.Utils.storeCandidates.registerStoreCandidate(myStoreCandidate,
                                'contexthub.mystorecandidate', 0);
```

En la mayoría de los casos, solo es necesario un candidato y la prioridad puede establecerse en `0`, pero si está interesado, puede obtener información sobre [registros más avanzados,](contexthub-api.md#registerstorecandidate-store-storetype-priority-applies) que permite elegir una de las pocas implementaciones de tienda en función de la condición de javascript (`applies`) y prioridad de los candidatos.

## Creación de tipos de módulos de IU de ContextHub {#creating-contexthub-ui-module-types}

Cree tipos de módulos de IU personalizados cuando los que [instalado con ContextHub](sample-modules.md) no cumpla con sus requisitos. Para crear un tipo de módulo de interfaz de usuario, cree un nuevo procesador de módulos de interfaz de usuario ampliando el `ContextHub.UI.BaseModuleRenderer` y luego registrarla con `ContextHub.UI`.

Para crear un procesador de módulos de interfaz de usuario, cree un `Class` objeto que contiene la lógica que procesa el módulo de IU. Como mínimo, la clase debe realizar las siguientes acciones:

* Amplíe el `ContextHub.UI.BaseModuleRenderer` Clase . Esta clase es la implementación base para todos los procesadores de módulos de interfaz de usuario. La variable `Class` define una propiedad denominada `extend` que utiliza para nombrar esta clase como la que se está ampliando.
* Proporcione una configuración predeterminada. Cree un `defaultConfig` propiedad. Esta propiedad es un objeto que incluye las propiedades definidas para la variable [`contexthub.base`](sample-modules.md#contexthub-base-ui-module-type) Módulo de interfaz de usuario y otras propiedades que necesite.

La fuente de `ContextHub.UI.BaseModuleRenderer` se encuentra en `/libs/granite/contexthub/code/ui/container/js/ContextHub.UI.BaseModuleRenderer.js`.  Para registrar el renderizador, utilice el [`registerRenderer`](contexthub-api.md#registerrenderer-moduletype-renderer-dontrender) método de la variable `ContextHub.UI` Clase . Debe proporcionar un nombre para el tipo de módulo. Cuando los administradores crean un módulo de interfaz de usuario basado en este procesador, especifican este nombre.

Cree y registre la clase renderizador en una función anónima de ejecución automática. El siguiente ejemplo se basa en el código fuente de la variable `contexthub.browserinfo` Módulo de interfaz de usuario. Este módulo de interfaz de usuario es una extensión simple de `ContextHub.UI.BaseModuleRenderer` Clase .

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

El archivo javascript que incluye el código que crea y registra el renderizador debe incluirse en una [carpeta de biblioteca cliente](/help/implementing/developing/introduction/clientlibs.md). La categoría de la carpeta debe coincidir con el siguiente patrón:

```javascript
contexthub.module.[moduleType]
```

La variable `[moduleType]` parte de la categoría es `moduleType` con el que está registrado el renderizador del módulo. Por ejemplo, para la variable `moduleType` de `contexthub.browserinfo`, la categoría de la carpeta de biblioteca del cliente debe ser `contexthub.module.contexthub.browserinfo`.
