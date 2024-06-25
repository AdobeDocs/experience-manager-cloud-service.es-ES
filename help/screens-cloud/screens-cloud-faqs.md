---
title: Preguntas frecuentes sobre Screens as a Cloud Service
description: En esta página se describen las preguntas más frecuentes sobre Screens as a Cloud Service.
exl-id: 93f2144c-0e64-4012-88c6-86972d8cad9f
feature: Administering Screens
role: Admin, Developer, User
source-git-commit: f9ba9fefc61876a60567a40000ed6303740032e1
workflow-type: ht
source-wordcount: '450'
ht-degree: 100%

---

# Preguntas frecuentes sobre Screens as a Cloud Service {#screens-cloud-faqs}

En la siguiente sección encontrará respuestas a las preguntas más frecuentes (FAQ) relacionadas con el proyecto de Screens as a Cloud Service.

## ¿Qué debo hacer si el Reproductor de AEM Screens que señala a Screens as a Cloud Service no elige el formato clientlibs personalizado con /etc.clientlibs/xxx/clientlibs/clientlib-site.lc-813643788974b0f89d686d9591526d63-lc.min.css?

AEM as a Cloud Service cambia las claves de caché largas con cada implementación. AEM Screens genera las cachés sin conexión cuando se modifica el contenido, en lugar de cuando Cloud Manager ejecuta la implementación. Estas claves de caché largas de los manifiestos no son válidas, por lo que el reproductor no puede descargar la *clientlibs*.

El uso de `longCacheKey="none"` en su carpeta `clientlib` elimina por completo las claves de caché largas de *clientlibs*.


## ¿Qué debo hacer si el manifiesto sin conexión no incluye todos los recursos como estaba previsto? {#offline-manifest}

Las cachés sin conexión se generan mediante el usuario de servicio **bulk-offline-update-screens-service**. Ciertas rutas, no accesibles por `bulk-offline-update-screens-service`, pueden provocar la ausencia de contenido en manifiestos sin conexión.

En su código, es decir, `ui.config or ui.apps`, cree una configuración OSGi en la carpeta de configuración, con el siguiente contenido, y asigne un título al nombre del archivo como `org.apache.sling.jcr.repoinit.RepositoryInitializer-serviceusersandacls-content.config`

```
scripts=[
        "
        set principal ACL for bulk-offline-update-screens-service
                allow jcr:read on /content/mysite
                allow jcr:read on /apps/my-resources
        end
        "] 
```

## ¿Qué formatos de imagen se recomiendan para una representación optimizada de imágenes en un canal de AEM Screens as a Cloud Service?{#screens-cloud-image-format}

Adobe recomienda utilizar imágenes con el formato `.png` y `.jpeg` en un canal AEM Screens as a Cloud Service, para obtener la mejor experiencia de señalización digital.
Las imágenes con el formato `*.tif` (Formato de archivo de imagen de etiqueta) no son compatibles con AEM Screens as a Cloud Service. Si un canal tiene este formato de imagen, en el lado del reproductor la imagen no se procesa.

## ¿Qué debo hacer si un canal en modo de desarrollador (en línea) no se procesa en el reproductor de AEM Screens?{#screens-cloud-online-channel-blank-iframe}

Adobe recomienda utilizar las funcionalidades de almacenamiento en caché de AEM Screens. Sin embargo, si debe ejecutar el canal en el modo de Desarrollador y el reproductor de AEM Screens muestra una pantalla en blanco, compruebe las herramientas para desarrolladores del reproductor y busque los errores `X-Frame-Options` o `frame-ancestors`. La resolución es configurar Dispatcher para permitir que el contenido se ejecute en iFrames. Normalmente, la siguiente configuración funciona de la siguiente manera:

```
Header set Content-Security-Policy "frame-ancestors 'self' file: localhost:*;"
```

## ¿Cuál es el uso del límite de código de registro?

Se recomienda limitar el uso del código de registro. Si un código de registro está comprometido, pero tiene un límite de 100 registros, entonces el atacante puede registrar solo hasta ese número, pero no más. Siempre puede actualizar el límite de uso después de crear el código de registro y de registrar a algunos de los jugadores del cliente. Si el cliente observa una actividad de registro inusual para un código de registro específico, puede reducir el límite en tiempo real mientras investiga. Pueden volver a aumentar el número si se trata de una falsa alarma, sin afectar a los jugadores ya registrados.
