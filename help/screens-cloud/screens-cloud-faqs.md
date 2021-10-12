---
title: Preguntas frecuentes as a Cloud Service de Screens
description: Esta página describe las preguntas más frecuentes as a Cloud Service de Screens.
exl-id: 93f2144c-0e64-4012-88c6-86972d8cad9f
source-git-commit: cf091056bdb96917a6d22bf1197d9b34ebbf9610
workflow-type: tm+mt
source-wordcount: '275'
ht-degree: 0%

---

# Preguntas frecuentes as a Cloud Service de Screens {#screens-cloud-faqs}

En la siguiente sección encontrará respuestas a las preguntas más frecuentes (FAQ) relacionadas con el proyecto as a Cloud Service de Screens.

## ¿Qué debo hacer si el reproductor AEM Screens que señala a Screens as a Cloud Service no elige los clientlibs personalizados con el formato /etc.clientlibs/xxx/clientlibs/clientlib-site.lc-813643788974b0f89d686d9591526d63-lc.min.css?

AEM as a Cloud Service cambia las claves de caché largas con cada implementación. AEM Screens genera las cachés sin conexión cuando se modifica el contenido, en lugar de cuando Cloud Manager ejecuta la implementación. Estas claves de caché largas en los manifiestos no son válidas, por lo que el reproductor no puede descargar estas *clientlibs*.

El uso de `longCacheKey="none"` en la carpeta `clientlib` elimina por completo las claves de caché largas para estos *clientlibs*.


## ¿Qué debemos hacer si el manifiesto sin conexión no incluye todos los recursos como se pretende? {#offline-manifest}

Las cachés sin conexión se generan mediante el usuario de servicio **bulk-offline-update-screens-service**. Ciertas rutas, a las que no se puede acceder desde `bulk-offline-update-screens-service`, conducen a que falte contenido en manifiestos sin conexión.

En su código, es decir, `ui.config or ui.apps`, cree una configuración OSGi en la carpeta de configuración, con el siguiente contenido, y asigne el nombre de archivo como `org.apache.sling.jcr.repoinit.RepositoryInitializer-serviceusersandacls-content.config`

```
scripts=[
        "
        set principal ACL for bulk-offline-update-screens-service
                allow jcr:read on /content/mysite
                allow jcr:read on /apps/my-resources
        end
        "] 
```

## ¿Qué formatos de imagen se recomiendan para una representación perfecta de imágenes en canales as a Cloud Service de AEM Screens?{#screens-cloud-image-format}

Se recomienda utilizar imágenes con los formatos `.png` y `.jpeg` en un canal as a Cloud Service de AEM Screens para obtener la mejor experiencia de señalización digital.
Las imágenes con el formato `*.tif` (formato de archivo de imagen de etiqueta) no son compatibles con AEM Screens as a Cloud Service. En caso de que un canal tenga este formato de imagen, la imagen no se procesará en el reproductor.