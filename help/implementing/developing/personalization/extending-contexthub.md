---
title: Ampliación de ContextHub
description: Defina nuevos tipos de módulos y tiendas de ContextHub cuando los que se proporcionan no cumplan con los requisitos de su solución
exl-id: ba817c18-f8bd-485d-b043-87593a6a93b5
feature: Developing, Personalization
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '625'
ht-degree: 0%

---

# Ampliación de ContextHub {#extending-contexthub}

Defina nuevos tipos de módulos y tiendas de ContextHub cuando los que se proporcionan no cumplan con los requisitos de su solución.

## Crear candidatos de tienda personalizados {#creating-custom-store-candidates}

Las tiendas de ContextHub se crean a partir de candidatos de tiendas registradas. Para crear un almacén personalizado, debe crear y registrar un candidato de almacén.

El archivo javascript que incluye el código que crea y registra al candidato al almacén debe incluirse en una [carpeta de biblioteca de cliente](/help/implementing/developing/introduction/clientlibs.md). La categoría de la carpeta debe coincidir con el siguiente patrón:

```xml
contexthub.store.[storeType]
```

La parte `storeType` de la categoría es el `storeType` con el que está registrado el candidato de tienda. (Consulte [Registro de un candidato a tienda ContextHub](#registering-a-contexthub-store-candidate)). Por ejemplo, para el storeType de `contexthub.mystore`, la categoría de la carpeta de biblioteca de cliente debe ser `contexthub.store.contexthub.mystore`.

### Creación de un candidato de tienda de ContextHub {#creating-a-contexthub-store-candidate}

Para crear una tienda candidata, utilice la función [`ContextHub.Utils.inheritance.inherit`](contexthub-api.md#inherit-child-parent) para ampliar una de las tiendas base:

* [`ContextHub.Store.PersistedStore`](contexthub-api.md#contexthub-store-persistedstore)
* [`ContextHub.Store.SessionStore`](contexthub-api.md#contexthub-store-sessionstore)
* [`ContextHub.Store.JSONPStore`](contexthub-api.md#contexthub-store-jsonpstore)
* [`ContextHub.Store.PersistedJSONPStore`](contexthub-api.md#contexthub-store-persistedjsonpstore)

Cada almacén base amplía el almacén [`ContextHub.Store.Core`](contexthub-api.md#contexthub-store-core).

En el siguiente ejemplo se crea la extensión más sencilla del candidato de almacén `ContextHub.Store.PersistedStore`:

```javascript
myStoreCandidate = function(){};
ContextHub.Utils.inheritance.inherit(myStoreCandidate,ContextHub.Store.PersistedStore);
```

De forma realista, los candidatos de la tienda personalizada definirán funciones adicionales o anularán la configuración inicial de la tienda. Hay varios [candidatos de almacén de muestra](sample-stores.md) instalados en el repositorio por debajo de `/libs/granite/contexthub/components/stores`.

### Registro de un candidato de tienda de ContextHub {#registering-a-contexthub-store-candidate}

Registre un candidato de tienda para integrarlo con el marco de ContextHub y permitir que se creen tiendas a partir de él. Para registrar un candidato de almacén, utilice la función [`registerStoreCandidate`](contexthub-api.md#registerstorecandidate-store-storetype-priority-applies) de la clase `ContextHub.Utils.storeCandidates`.

Al registrar un candidato de tienda, se proporciona un nombre para el tipo de tienda. Al crear un almacén a partir del candidato, se utiliza el tipo de almacén para identificar el candidato en el que se basa.

Cuando se registra un candidato a tienda, se indica su prioridad. Cuando se registra un candidato de tienda con el mismo tipo de tienda que un candidato de tienda ya registrado, se utiliza el candidato con la prioridad más alta. Por lo tanto, puede anular los candidatos de tienda existentes con nuevas implementaciones.

```javascript
ContextHub.Utils.storeCandidates.registerStoreCandidate(myStoreCandidate,
                                'contexthub.mystorecandidate', 0);
```

En la mayoría de los casos, solo se necesita un candidato y la prioridad se puede establecer en `0`, pero si está interesado, puede obtener información sobre [registros más avanzados](contexthub-api.md#registerstorecandidate-store-storetype-priority-applies), que permite elegir una de las pocas implementaciones de la tienda en función de la condición de javascript (`applies`) y la prioridad del candidato.

## Creación de tipos de módulos de IU de ContextHub {#creating-contexthub-ui-module-types}

Cree tipos de módulos de IU personalizados cuando los que están [instalados con ContextHub](sample-modules.md) no cumplan con sus requisitos. Para crear un tipo de módulo de interfaz de usuario, cree un procesador de módulos de interfaz de usuario ampliando la clase `ContextHub.UI.BaseModuleRenderer` y registrándola después con `ContextHub.UI`.

Para crear un procesador de módulos de IU, cree un objeto `Class` que contenga la lógica que procesa el módulo de IU. Como mínimo, la clase debe realizar las siguientes acciones:

* Extienda la clase `ContextHub.UI.BaseModuleRenderer`. Esta clase es la implementación base para todos los procesadores de módulos de IU. El objeto `Class` define una propiedad denominada `extend` que se usa para asignar a esta clase el nombre que se está extendiendo.
* Proporcione una configuración predeterminada. Crear una propiedad `defaultConfig`. Esta propiedad es un objeto que incluye las propiedades definidas para el módulo de interfaz de usuario [`contexthub.base`](sample-modules.md#contexthub-base-ui-module-type) y cualquier otra propiedad que necesite.

El origen de `ContextHub.UI.BaseModuleRenderer` se encuentra en `/libs/granite/contexthub/code/ui/container/js/ContextHub.UI.BaseModuleRenderer.js`.  Para registrar el procesador, utilice el método [`registerRenderer`](contexthub-api.md#registerrenderer-moduletype-renderer-dontrender) de la clase `ContextHub.UI`. Debe proporcionar un nombre para el tipo de módulo. Cuando los administradores crean un módulo de interfaz de usuario basado en este procesador, especifican este nombre.

Cree y registre la clase de procesador en una función anónima de ejecución automática. El siguiente ejemplo se basa en el código fuente del módulo de interfaz de usuario `contexthub.browserinfo`. Este módulo de interfaz de usuario es una extensión simple de la clase `ContextHub.UI.BaseModuleRenderer`.

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

El archivo javascript que incluye el código que crea y registra el procesador debe incluirse en una [carpeta de biblioteca de cliente](/help/implementing/developing/introduction/clientlibs.md). La categoría de la carpeta debe coincidir con el siguiente patrón:

```javascript
contexthub.module.[moduleType]
```

La parte `[moduleType]` de la categoría es el `moduleType` con el que está registrado el procesador de módulos. Por ejemplo, para `moduleType` de `contexthub.browserinfo`, la categoría de la carpeta de la biblioteca de cliente debe ser `contexthub.module.contexthub.browserinfo`.
