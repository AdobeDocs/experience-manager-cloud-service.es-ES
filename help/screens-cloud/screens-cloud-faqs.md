---
title: Preguntas frecuentes de Screens as a Cloud Service
description: En esta página se describen las preguntas más frecuentes as a Cloud Service de Screens.
exl-id: 93f2144c-0e64-4012-88c6-86972d8cad9f
source-git-commit: bc3c054e781789aa2a2b94f77b0616caec15e2ff
workflow-type: tm+mt
source-wordcount: '454'
ht-degree: 2%

---

# Preguntas frecuentes de Screens as a Cloud Service {#screens-cloud-faqs}

En la siguiente sección encontrará respuestas a las preguntas más frecuentes (FAQ) relacionadas con el proyecto as a Cloud Service de Screens.

## ¿Qué debo hacer si el Reproductor de AEM Screens que señala a Pantallas as a Cloud Service no elige el formato clientlibs personalizado con /etc.clientlibs/xxx/clientlibs/clientlib-site.lc-813643788974b0f89d686d9591526d63-lc.min.css?

AEM as a Cloud Service cambia las claves de caché largas con cada implementación. AEM Screens genera las cachés sin conexión cuando se modifica el contenido, en lugar de cuando Cloud Manager ejecuta la implementación. Estas claves de caché largas de los manifiestos no son válidas, por lo que el reproductor no puede descargar la *clientlibs*.

Uso de `longCacheKey="none"` en su `clientlib` elimina por completo las claves de caché largas de la carpeta *clientlibs*.


## ¿Qué debo hacer si el manifiesto sin conexión no incluye todos los recursos como estaba previsto? {#offline-manifest}

Las cachés sin conexión se generan mediante **bulk-offline-update-screens-service** usuario de servicio. Ciertas rutas, no accesibles por `bulk-offline-update-screens-service`, puede provocar la ausencia de contenido en manifiestos sin conexión.

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

## ¿Qué formatos de imagen se recomiendan para una representación perfecta de imágenes en un canal as a Cloud Service de AEM Screens?{#screens-cloud-image-format}

El Adobe recomienda utilizar imágenes con el formato `.png` y `.jpeg` en un canal as a Cloud Service de AEM Screens, para obtener la mejor experiencia de señalización digital.
Las imágenes con el formato `*.tif` (Formato de archivo de imagen de etiqueta) no son compatibles con AEM Screens as a Cloud Service. Si un canal tiene este formato de imagen, en el lado del reproductor la imagen no se procesa.

## ¿Qué debo hacer si un canal en modo de desarrollador (en línea) no se procesa en el reproductor AEM Screens?{#screens-cloud-online-channel-blank-iframe}

Adobe recomienda utilizar las funcionalidades de almacenamiento en caché de AEM Screens. Sin embargo, si debe ejecutar el canal en el modo de desarrollador y el reproductor de AEM Screens muestra una pantalla en blanco, compruebe las herramientas para desarrolladores del reproductor y busque `X-Frame-Options` o `frame-ancestors` errores. La resolución es configurar Dispatcher para permitir que el contenido se ejecute en iFrames. Normalmente, funciona la siguiente configuración:

```
Header set Content-Security-Policy "frame-ancestors 'self' file: localhost:*;"
```

## ¿Cuál es el uso del límite de código de registro?

Se recomienda limitar el uso del código de registro. Si un código de registro está comprometido, pero tiene un límite de 100 registros, entonces el atacante puede registrar solo hasta ese número, pero no más. Siempre puede actualizar el límite de uso después de crear el código de registro y de registrar a algunos de los jugadores del cliente. Si el cliente observa una actividad de registro inusual para un código de registro específico, puede reducir el límite en tiempo real mientras investiga. Pueden volver a aumentar el número si se trata de una falsa alarma, sin afectar a los jugadores ya registrados.
