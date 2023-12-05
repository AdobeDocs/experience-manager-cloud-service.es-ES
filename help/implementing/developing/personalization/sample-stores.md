---
title: Candidatos de tienda de ContextHub de muestra
description: ContextHub proporciona varios candidatos de tienda de muestra que puede utilizar en sus soluciones
exl-id: 9493d91e-0b23-4dc4-a014-d8d13687efad
source-git-commit: abe5f8a4b19473c3dddfb79674fb5f5ab7e52fbf
workflow-type: tm+mt
source-wordcount: '457'
ht-degree: 1%

---

# Candidatos de tienda de ContextHub de muestra {#sample-contexthub-store-candidates}

ContextHub proporciona varios candidatos de tienda de muestra que puede utilizar en sus soluciones. Se proporciona la siguiente información para cada muestra:

* Dónde encontrar el código fuente para poder abrirlo con fines de aprendizaje.
* Cómo configurar las tiendas que cree a partir de los candidatos de la tienda.
* Cómo se estructuran los datos de la tienda para que pueda acceder a ellos.

>[!WARNING]
>
>Los candidatos de tienda de muestra se proporcionan como configuraciones de referencia para ayudarle a crear su propia configuración dedicada para su proyecto. No los utilice directamente.

## Aem.segmentation: candidato de tienda de muestra {#aem-segmentation-sample-store-candidate}

Almacenar para segmentos de ContextHub resueltos y no resueltos. Recupera automáticamente segmentos del Administrador de segmentos de ContextHub.

### Ubicación de origen {#source-location-segmentation}

`/libs/settings/cloudsettings/legacy/contexthub/segmentation`

### Implementación de base {#base-implementation-segmentation}

El candidato del almacén de aem.segmentation amplía [`ContextHub.Store.PersistedJSONPStore`](contexthub-api.md#contexthub-store-persistedjsonpstore).

### Configuración {#configuration-segmentation}

Cuando crea un `aem.segmentation` , no es necesario proporcionar una configuración detallada. La configuración predeterminada especifica la ubicación de las definiciones de segmentos de ContextHub.

```xml
{
   "service":{
      "jsonp":false,
      "timeout":1000,
      "path":"/etc/segmentation/contexthub.segment.js"
   }
}
```

## candidato de tienda de muestra contexthub.geolocation {#contexthub-geolocation-sample-store-candidate}

El `contexthub.geolocation` El candidato del almacén de muestra utiliza Google Maps para obtener y almacenar información sobre la ubicación del cliente.

### Ubicación de origen {#source-location-geolocation}

`/libs/settings/cloudsettings/legacy/contexthub/geolocation`

### Implementación de base {#base-implementation-geolocation}

El `contexthub.geolocation` ampliación de candidato de tienda [`ContextHub.Store.PersistedJSONPStore`](contexthub-api.md#contexthub-store-persistedjsonpstore).

### Configuración {#configuration-geolocation}

La configuración predeterminada especifica información sobre el servicio Google y las coordenadas iniciales de latitud y longitud.

```javascript
{
        "service": {
            "jsonp": false,
            "timeout": 1000,
            "ttl": 1800000,
            "secure": false,
            "host": "maps.googleapis.com",
            "port": 80,
            "path": "/maps/api/geocode/json"
        },

        "eventDeferring": 16,

        "html5coordinatesDiscoveryAPI": {
            "timeout": 30000,
            "ttl": 900000,
            "highAccuracy": false
        },

        "initialValues": {
            "latitude": 37.331375,
            "longitude": -121.893992
        }
    }
```

### Elementos de datos {#data-items-geolocation}

El almacén utiliza un árbol de datos similar al siguiente ejemplo:

```javascript
{
   "latitude":"37.331375",
   "longitude":"-121.893992"
}
```

>[!NOTE]
>
>Una política de seguridad introducida en Chrome 50.x requiere que todas las llamadas relacionadas con la geolocalización se realicen a través de una conexión segura. AEM AEM Por lo tanto, se fuerza el uso de https para las llamadas a la API de geolocalización si también se está ejecutando en https, por lo que también se fuerza el uso de https. De lo contrario, http se utiliza para cumplir la directiva del mismo origen.
>
>Consulte [esta publicación de blog de Google](https://developers.google.com/web/updates/2016/04/geolocation-on-secure-contexts-only) para obtener más información sobre el cambio en Chrome.

## contexthub.surferinfo Candidato de tienda de muestra {#contexthub-surferinfo-sample-store-candidate}

Almacena información sobre el entorno del cliente actual, como el dispositivo, la ventana, el explorador, la fecha y la hora.

### Ubicación de origen {#source-location-surferinfo}

`/libs/settings/cloudsettings/legacy/contexthub/surferinfo`

### Implementación de base {#base-implementation-surferinfo}

El `contexthub.surferinfo` ampliación de candidato de tienda [`ContextHub.Store.PersistedStore`](contexthub-api.md#contexthub-store-persistedstore).

### Configuración {#configuration-surferinfo}

La configuración predeterminada se hereda de `ContextHub.Store.PersistedStore`.

### Elementos de datos {#data-items-surferinfo}

Las tiendas que utilizan este candidato de tienda tienen un árbol de datos similar al siguiente ejemplo:

```javascript
{
   "display":{
      "resolution":{
         "width":1440,
         "height":900
      },
      "devicePixelRatio":1,
      "colorDepth":24,
      "nrOfColors":16777216,
      "pixelsPerInch":96,
      "orientation":{
         "mode":"landscape",
         "direction":"normal"
      }
   },
   "window":{
      "dimension":{
         "width":1395,
         "height":652
      },
      "percentageUsage":0.7
   },
   "browser":{
      "version":"39.0",
      "family":"Firefox",
      "userAgent":"Mozilla/5.0 (Macintosh; Intel Mac OS X 10.9; rv:39.0) Gecko/20100101 Firefox/39.0"
   },
   "device":{
      "category":"Desktop",
      "type":"Desktop",
      "model":"PC",
      "version":""
   },
   "isMobile":true,
   "os":{
      "name":"Mac OS X",
      "version":"10"
   },
   "year":2015,
   "month":7,
   "day":22,
   "hour":14,
   "minutes":1
}
```

## granite.emulators Candidato de tienda de muestra {#granite-emulators-sample-store-candidate}

El `granite.emulators` el candidato del almacén de ejemplo almacena información sobre los dispositivos cliente.

### Ubicación de origen {#source-location-emulators}

`/libs/settings/cloudsettings/legacy/contexthub/emulators`

### Implementación de base {#base-implementation-emulators}

El `granite.emulators` ampliación de candidato de tienda [`ContextHub.Store.PersistedStore`](contexthub-api.md#contexthub-store-persistedstore).

### Configuración {#configuration-emulators}

La configuración predeterminada incluye una matriz denominada `defaultEmulators` que contiene información sobre diferentes dispositivos. Cuando cree un almacén, proporcione distintos perfiles de dispositivo en la propiedad Detail Configuration según sea necesario, utilizando el formato que se muestra en el siguiente ejemplo:

```javascript
{
   "defaultEmulators":[
        {
            "id": "iphone-6",
            "title": "iPhone 6",
            "type": "mobile",
            "platform": "iOS",
            "platformVersion": "8.1.3",
            "width": 750,
            "height": 1334,
            "canRotate": true,
            "orientation": "Portrait",
            "device-pixel-ratio": 2
        },
        {
            "id": "iphone-6-plus",
            "title": "iPhone 6 Plus",
            "type": "mobile",
            "platform": "iOS",
            "platformVersion": "8.1.3",
            "width": 1080,
            "height": 1920,
            "canRotate": true,
            "orientation": "Portrait",
            "device-pixel-ratio": 3
        },
        {
            "id": "galaxy-s4",
            "title": "Samsung Galaxy S4",
            "type": "mobile",
            "platform": "Android",
            "platformVersion": "4.4.2 KitKat",
            "width": 1080,
            "height": 1920,
            "canRotate": true,
            "orientation": "Portrait",
            "device-pixel-ratio": 3
        }
    ]
}
```

### Elementos de datos {#data-items-emulators}

El árbol de datos de tienda es similar al siguiente ejemplo:

```javascript
{
   "devices":[
      {"id":"native",
      "title":"Native",
      "type":"screen",
      "width":1395,
      "height":374,
      "orientation":"Landscape",
      "platform":"Mac OS X",
      "platformVersion":"10",
      "canRotate":false
      },
      {"id":"ipad-3",
      "title":"iPad 3 / 4 / Air",
      "type":"tablet",
      "platform":"iOS",
      "platformVersion":"8.1.3",
      "width":1536,
      "height":2048,
      "canRotate":true,
      "orientation":"Portrait",
      "device-pixel-ratio":2
      },
      {"id":"iphone-6",
      "title":"iPhone 6",
      "type":"mobile",
      "platform":"iOS",
      "platformVersion":"8.1.3",
      "width":750,
      "height":1334,
      "canRotate":true,
      "orientation":"Portrait",
      "device-pixel-ratio":2
      },
      {"id":"galaxy-s4",
      "title":"Samsung Galaxy S4",
      "type":"mobile",
      "platform":"Android",
      "platformVersion":"4.4.2 KitKat",
      "width":1080,
      "height":1920,
      "canRotate":true,
      "orientation":"Portrait",
      "device-pixel-ratio":3
      }
   ],
   "currentDeviceId":"native",
   "orientations":[
      {"id":"landscape",
      "title":"Landscape"
      },
      {"id":"portrait",
       "title":"Portrait"
      }
   ],
   "currentDevice":{
      "id":"native",
      "title":"Native",
      "type":"screen",
      "width":1395,
      "height":374,
      "orientation":"Landscape",
      "platform":"Mac OS X",
      "platformVersion":"10",
      "canRotate":false
   }
}
```

## granite.profile Candidato de tienda de muestra {#granite-profile-sample-store-candidate}

Almacena información sobre el usuario actual.

### Ubicación de origen {#source-location-profile}

`/libs/settings/cloudsettings/legacy/contexthub/profile`

### Implementación de base {#base-implementation-profile}

El `granite.profile` ampliación de candidato de tienda [`ContextHub.Store.PersistedJSONPStore`](contexthub-api.md#contexthub-store-persistedjsonpstore).

### Configuración {#configuration-profile}

Se utiliza la siguiente configuración predeterminada. No debe cambiar esta configuración.

```javascript
{
   "service":{
      "jsonp":false,
      "timeout":1000,
      "path":"${contexthub:/store/profile/path}.infinity.json"
   },
   "initialValues":{"path":"/home/users/a/anonymous"}
}
```

### Elementos de datos {#data-items-profile}

Las tiendas que utilizan este candidato de tienda tienen un árbol de datos similar al siguiente ejemplo:

```javascript
{
   "displayName":"anonymous",
   "path":"/home/users/6/6zavE_DGre6Ad9Y5E0Ba",
   "avatar":"/etc/designs/default/images/social/avatar.png",
   "authorizableId":"anonymous"
}
```
