---
title: Preguntas frecuentes de Screens as a Cloud Service
description: Esta página describe las preguntas más frecuentes as a Cloud Service de Screens.
exl-id: 93f2144c-0e64-4012-88c6-86972d8cad9f
source-git-commit: 02c9cbff56399ea2ca1baad7d2289d5d4c17c1c5
workflow-type: tm+mt
source-wordcount: '459'
ht-degree: 2%

---

# Preguntas frecuentes de Screens as a Cloud Service {#screens-cloud-faqs}

En la siguiente sección encontrará respuestas a las preguntas más frecuentes (FAQ) relacionadas con el proyecto as a Cloud Service de Screens.

## ¿Qué debo hacer si AEM Screens Player que señala a Screens as a Cloud Service no elige los clientlibs personalizados con el formato /etc.clientlibs/xxx/clientlibs/clientlib-site.lc-813643788974b0f89d686d9591526d63-lc.min.css?

AEM as a Cloud Service cambia las claves de caché largas con cada implementación. AEM Screens genera las cachés sin conexión cuando se modifica el contenido, en lugar de cuando Cloud Manager ejecuta la implementación. Estas claves de caché largas en los manifiestos no son válidas, por lo que el reproductor no puede descargar estas *clientlibs*.

Uso `longCacheKey="none"` en su `clientlib` la carpeta elimina por completo las claves de caché largas para estas *clientlibs*.


## ¿Qué debemos hacer si el manifiesto sin conexión no incluye todos los recursos como se pretende? {#offline-manifest}

Las cachés sin conexión se generan mediante **bulk-offline-update-screens-service** usuario del servicio. Ciertas rutas, a las que no se puede acceder desde `bulk-offline-update-screens-service`, lo que provoca que falte contenido en manifiestos sin conexión.

En el código, es decir, `ui.config or ui.apps`, cree una configuración OSGi en la carpeta de configuración, con el siguiente contenido, y asigne el nombre de archivo como `org.apache.sling.jcr.repoinit.RepositoryInitializer-serviceusersandacls-content.config`

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

Se recomienda utilizar imágenes en el formato . `.png` y `.jpeg` en un canal as a Cloud Service de AEM Screens, para obtener la mejor experiencia de señalización digital.
Las imágenes en formato `*.tif` (Formato de archivo de imagen de etiqueta) no son compatibles con AEM Screens as a Cloud Service. En caso de que un canal tenga este formato de imagen, la imagen no se procesará en el reproductor.

## ¿Qué debo hacer si un canal en modo de desarrollador (en línea) no se está renderizando en AEM Screens Player?{#screens-cloud-online-channel-blank-iframe}

Se recomienda aprovechar las capacidades de almacenamiento en caché de AEM Screens, pero si necesita ejecutar el canal en modo de desarrollador y el reproductor de AEM Screens muestra una pantalla en blanco, compruebe las herramientas para desarrolladores del reproductor y busque `X-Frame-Options` o `frame-ancestors` errores. La resolución es configurar Dispatcher para permitir que el contenido se ejecute en iFrames. Normalmente, la siguiente configuración funcionará:

```
Header set Content-Security-Policy "frame-ancestors ‘self’ file: localhost:*;"
```

## ¿Cuál es el uso del Límite de Código de Registro?

Como práctica recomendada, puede limitar el uso del código de registro. Si un código de registro está comprometido, pero tiene un límite de 100 registros, el atacante puede registrar solamente hasta ese número, pero no más. Siempre puede actualizar el límite de uso después de crear el código de registro y de registrar algunos de los reproductores del cliente. Si el cliente observa una actividad de registro inusual para un código de registro específico, puede reducir el límite en tiempo real mientras investiga y puede aumentar el número de vuelta si se trata de una falsa alarma, sin afectar a los reproductores ya registrados.
