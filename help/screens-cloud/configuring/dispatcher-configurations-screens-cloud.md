---
title: Configuraciones de Dispatcher en Screens como Cloud Service
description: Esta página describe las configuraciones de Dispatcher en Screens como un Cloud Service.
source-git-commit: b00fd1e3826a7d0b0a4bf80b002fffda8f3983d0
workflow-type: tm+mt
source-wordcount: '140'
ht-degree: 0%

---


# Configuraciones de Dispatcher en Screens como Cloud Service {#dispatcher-configurations-screens-cloud}

En esta sección se describen las configuraciones de Dispatcher para Screens como Cloud Service.

## Añadir filtros y reglas de caché en Dispatcher para Screens como implementación de Cloud Service {#deployment}

Habilite los siguientes filtros y reglas de caché en distribuidores para las instancias de publicación en Screens como Cloud Service.

### Filtros de AEM Screens {#filters}

```
## # Content Configurations
/0200 { /type "allow" /method '(GET|HEAD)' /url "/content/screens/*" }
#/0201 { /type "allow" /method '(GET|HEAD)' /url "/content/experience-fragments/*" } ## uncomment this, if you're using experience-fragments
## add any other formats required for your project here
/0202 { /type "allow" /extension '(css|eot|gif|ico|jpeg|jpg|js|gif|pdf|png|svg|swf|ttf|woff|woff2|html|mp4|mov|m4v)' /path "/content/dam/*" }
/0203 { /type "allow" /method 'GET' /url "/screens/channels.json" }
## # Enable clientlibs proxy servlet
/0210 { /type "allow" /method "GET" /url "/etc.clientlibs/*" }
```

### Reglas de caché {#cache-rules}

* Agregue `/statfileslevel "10"` a la sección `/cache` en `publish_farm.any`/.

   >[!NOTE]
   >Esta regla de caché admite el almacenamiento en caché de hasta 10 niveles desde la raíz de documento de la caché y se invalida cuando se publica contenido en lugar de invalidar todo. Puede cambiar este nivel en función de la profundidad con la que esté configurada la estructura de contenido.

* Agregue lo siguiente a la sección `/invalidate` en `publish_farm.any`.

   ```
   /0003 {
       /glob "*.json"
       /type "allow"
   }
   ```

* Agregue las siguientes reglas a la sección `/rules` en `/cache` en publish_farm.any o en un archivo incluido desde `publish_farm.any`.

   ```
   ## Allow Dispatcher Cache for Screens channels
    /0002
        {
        /glob "/content/screens/*.html"
        /type "allow"
        }
   
   ## Allow Dispatcher Cache for Screens offline manifests
   
   /0003
       {
       /glob "/content/screens/*.manifest.json"
       /type "allow"
       }
   
   ## Allow Dispatcher Cache for Assets
   /0004
       {
       /glob "/content/dam/*"
       /type "allow"
       }
   
   ## Deny Screens Channels json
   /0005
       {
       /glob "/screens/channels.json"
       /type "deny"
       }
   ```
