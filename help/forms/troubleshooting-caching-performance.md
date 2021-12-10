---
title: 'Resolución de problemas de rendimiento del almacenamiento en caché  '
seo-title: Troubleshooting caching performance
description: 'Resolución de problemas de rendimiento del almacenamiento en caché  '
seo-description: Troubleshooting caching performance
contentOwner: khsingh
exl-id: eae44a6f-25b4-46e9-b38b-5cec57b6772c
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '360'
ht-degree: 0%

---

# Rendimiento de almacenamiento en caché {#caching-performance}

Puede encontrar algunos de los siguientes problemas al configurar o utilizar la caché de Forms adaptable en un entorno de Cloud Service:

## Algunos Forms adaptables que contienen imágenes o vídeos no se invalidan automáticamente de la caché de Dispatcher {#images-videos-not-invalidated}

Puede seleccionar y agregar imágenes o vídeos desde el navegador de recursos a un formulario adaptable. Cuando se editan estas imágenes en el editor de Assets, la versión en caché de un formulario adaptable que contenga dichas imágenes no se invalida. El formulario adaptable sigue mostrando imágenes antiguas.

Para resolver el problema, después de publicar las imágenes y el vídeo, cancele la publicación y publicación explícitamente de la Forms adaptable que hace referencia a estos recursos.

## Algunas Forms adaptables que contienen fragmentos de contenido o fragmentos de experiencia no se invalidan automáticamente de la caché de Dispatcher {#content-fragments-experience-fragments-not-invalidated}

Puede agregar un fragmento de contenido o un fragmento de experiencia a un formulario adaptable. Cuando estos fragmentos se editan y publican de forma independiente, la versión en caché de un formulario adaptable que contenga dichos fragmentos no se invalida. El formulario adaptable sigue mostrando fragmentos más antiguos.

Para resolver el problema, después de publicar un fragmento de contenido actualizado o un fragmento de experiencia, cancele la publicación y la publicación explícitas del Forms adaptable que utiliza estos recursos.

## Solo se almacena en caché la primera instancia de Forms adaptable {#only-first-instance-cached}

Cuando la URL del formulario adaptable no contiene información de localización y la opción Usar configuración regional del explorador está activada, se proporciona una versión localizada del formulario adaptable y una instancia del formulario adaptable, basada en la primera solicitud (configuración regional del explorador solicitada), se almacena en caché y se envía a todos los usuarios posteriores.

Siga estos pasos para resolver el problema:

1. Abra el proyecto de Experience Manager.
1. Abra el `dispatcher/scr/conf.d/rewrites/rewrite.rules` para editar.
1. Abra el `conf.d/httpd-dispatcher.conf` o cualquier otro archivo de configuración configurado para cargarse durante la ejecución.
1. Agregue el siguiente código al archivo y guárdelo. Es un código de ejemplo, puede modificarlo para adaptarlo a su entorno.

```shellscript
    # Handle actual URL convention (just pass through)
    RewriteRule "^/content/forms/af/(.*)[.](.*).html$" "/content/forms/af/$1.$2.html" [PT]
    
    # Handle selector-based redirection based on browser language
    <VirtualHost *:80>
            # Handle actual URL convention (just pass through)
    RewriteRule "^/content/forms/af/(.*)[.](.*).html$" "/content/forms/af/$1.$2.html" [PT]

    # Handle selector based redirection basded on browser language
    # The Rewrite Condition is looking for the Accept-Language header and if found takes the first two character which most likely will be the desired language selector.
    RewriteCond %{HTTP:Accept-Language} ^(..).*$ [NC]
    RewriteRule "^/content/forms/af/(.*).html$" "/content/forms/af/$1.%1.html" [R]
    RewriteRule "^/content/forms/af/(.*).html$" "/content/forms/af/$1.%1.html" [R]
```

## El almacenamiento en caché de CDN deja de funcionar tras 300 segundos {#cdn-caching-stops-working-after-300-seconds}

El almacenamiento en caché de CDN deja de funcionar después de 300 segundos y todas las solicitudes de caché en CDN se redirigen a Dispatcher.

Para resolver el problema, establezca el encabezado de página en 0:

1. Cree un archivo en `src\conf.d\available_vhosts`

1. Añada lo siguiente al archivo para establecer el encabezado de página

   ```shellscript
       <IfModule mod_headers.c>
               Header add X-Vhost "publish"
               Header set age 0
       </IfModule>
   ```

1. Guarde y cierre el archivo.
1. Modifique el vínculo de software para `src\conf.d\enabled_vhosts\default.vhost` para que apunten a un nuevo archivo.
