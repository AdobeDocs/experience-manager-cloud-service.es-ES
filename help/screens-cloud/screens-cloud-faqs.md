---
title: Preguntas frecuentes sobre Screens as a Cloud Service
description: En esta página se describen las preguntas más frecuentes de Screens como Cloud Service.
source-git-commit: 7a26bb50a8b95a2358912249e21daeb9c5e9c1a3
workflow-type: tm+mt
source-wordcount: '191'
ht-degree: 0%

---


# Preguntas frecuentes sobre Screens as a Cloud Service {#screens-cloud-faqs}

En la siguiente sección se ofrecen respuestas a las preguntas más frecuentes (FAQ) relacionadas con Screens como proyecto de Cloud Service.

## ¿Qué debo hacer si el reproductor AEM Screens que señala Screens como Cloud Service no elige los clientlibs personalizados con el formato /etc.clientlibs/xxx/clientlibs/clientlib-site.lc-813643788974b0f89d686d9591526d63-lc.min.css?

AEM como Cloud Service cambia las claves de caché largas con cada implementación. AEM Screens genera las cachés sin conexión cuando se modifica el contenido, en lugar de cuando Cloud Manager ejecuta la implementación. Estas claves de caché largas en los manifiestos no son válidas, por lo que el reproductor no puede descargar estas *clientlibs*.

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
