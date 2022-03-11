---
title: Configuraciones de Dispatcher en Screens as a Cloud Service
description: Esta página describe las configuraciones de Dispatcher en Screens as a Cloud Service.
exl-id: cc04b480-9310-4975-a7c2-20682c567fa4
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '140'
ht-degree: 0%

---

# Configuraciones de Dispatcher en Screens as a Cloud Service {#dispatcher-configurations-screens-cloud}

En esta sección se describen las configuraciones de Dispatcher para Screens as a Cloud Service.

## Añadir filtros y reglas de caché en Dispatcher para la implementación as a Cloud Service de Screens {#deployment}

Habilite los siguientes filtros y reglas de caché en los distribuidores para las instancias de publicación en Screens as a Cloud Service.

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

* Agregar `/statfileslevel "10"` a `/cache` en `publish_farm.any`/.

   >[!NOTE]
   >Esta regla de caché admite el almacenamiento en caché de hasta 10 niveles desde la raíz de documento de la caché y se invalida cuando se publica contenido en lugar de invalidar todo. Puede cambiar este nivel en función de la profundidad con la que esté configurada la estructura de contenido.

* Agregue lo siguiente a `/invalidate` en `publish_farm.any`.

   ```
   /0003 {
       /glob "*.json"
       /type "allow"
   }
   ```

* Agregue las siguientes reglas a `/rules` en `/cache` en publish_farm.any o en un archivo incluido desde `publish_farm.any`.

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
