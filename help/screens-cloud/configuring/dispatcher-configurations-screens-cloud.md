---
title: Configuraciones de Dispatcher en Pantallas as a Cloud Service
description: En esta página se describen las configuraciones de Dispatcher en Pantallas as a Cloud Service.
exl-id: cc04b480-9310-4975-a7c2-20682c567fa4
source-git-commit: f0e9fe0bdf35cc001860974be1fa2a7d90f7a3a9
workflow-type: tm+mt
source-wordcount: '140'
ht-degree: 0%

---

# Configuraciones de Dispatcher en Pantallas as a Cloud Service {#dispatcher-configurations-screens-cloud}

En esta sección se describen las configuraciones de Dispatcher para Pantallas as a Cloud Service.

## Adición de filtros y reglas de caché en Dispatcher para la implementación as a Cloud Service de Screens {#deployment}

Permitir los siguientes filtros y reglas de caché en Dispatcher para las instancias de publicación en Pantallas as a Cloud Service.

### Filtros de AEM Screens {#filters}

```
## # Content Configurations
/0200 { /type "allow" /method '(GET|HEAD)' /url "/content/screens/*" }
#/0201 { /type "allow" /method '(GET|HEAD)' /url "/content/experience-fragments/*" } ## uncomment this, if you are using experience-fragments
## add any other formats required for your project here
/0202 { /type "allow" /extension '(css|eot|gif|ico|jpeg|jpg|js|gif|pdf|png|svg|swf|ttf|woff|woff2|html|mp4|mov|m4v)' /path "/content/dam/*" }
/0203 { /type "allow" /method 'GET' /url "/screens/channels.json" }
## # Enable clientlibs proxy servlet
/0210 { /type "allow" /method "GET" /url "/etc.clientlibs/*" }
```

### Reglas de caché {#cache-rules}

* Añadir `/statfileslevel "10"` hasta `/cache` sección en `publish_farm.any`/.

  >[!NOTE]
  >Esta regla de caché admite el almacenamiento en caché de hasta 10 niveles desde la caché docroot e invalida cuando se publica contenido en lugar de invalidarlo todo. Puede cambiar este nivel en función de la profundidad con que se haya configurado la estructura de contenido.

* Agregue lo siguiente a `/invalidate` sección en `publish_farm.any`.

  ```
  /0003 {
      /glob "*.json"
      /type "allow"
  }
  ```

* Añada las siguientes reglas a `/rules` sección en `/cache` en publish_farm.any o en un archivo incluido en `publish_farm.any`.

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
