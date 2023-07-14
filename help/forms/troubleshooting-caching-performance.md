---
title: Resolución de problemas de rendimiento del almacenamiento en caché
seo-title: Troubleshooting caching performance
description: Resolución de problemas de rendimiento del almacenamiento en caché
seo-description: Troubleshooting caching performance
contentOwner: khsingh
exl-id: eae44a6f-25b4-46e9-b38b-5cec57b6772c
source-git-commit: f7525b6b37e486a53791c2331dc6000e5248f8af
workflow-type: ht
source-wordcount: '360'
ht-degree: 100%

---

# Rendimiento del almacenamiento en caché {#caching-performance}

Puede experimentar algunos de los siguientes problemas al configurar o utilizar la caché de los formularios adaptables en un entorno de Cloud Service:

## Algunos formularios adaptables que contienen imágenes o vídeos no se invalidan automáticamente en la caché de Dispatcher {#images-videos-not-invalidated}

Puede seleccionar y agregar imágenes o vídeos desde el Explorador de recursos a un formulario adaptable. Cuando estas imágenes se editan en el Editor de recursos, la versión en caché del formulario adaptable que contiene dichas imágenes no se invalida. El formulario adaptable sigue mostrando las imágenes antiguas.

Para resolver el problema, después de publicar las imágenes y los vídeos, cancele la publicación del formulario adaptable que hace referencia a estos recursos y vuelva a publicarlo explícitamente.

## Algunos formularios adaptables que contienen fragmentos de contenido o fragmentos de experiencias no se invalidan automáticamente en la caché de Dispatcher {#content-fragments-experience-fragments-not-invalidated}

Puede agregar un fragmento de contenido o un fragmento de experiencia a un formulario adaptable. Cuando estos fragmentos se editan y publican de forma independiente, la versión en caché del formulario adaptable que contiene estos fragmentos no se invalida. El formulario adaptable sigue mostrando los fragmentos antiguos.

Para resolver el problema, después de publicar el fragmento de contenido o el fragmento de experiencia actualizado, cancele la publicación del formulario adaptable que utiliza estos recursos y vuelva a publicarlo explícitamente.

## Solo se almacena en caché la primera instancia de un formulario adaptable {#only-first-instance-cached}

Cuando la URL del formulario adaptable no contiene información de localización y la opción Usar configuración regional del explorador está activada en el Administrador de configuración, se proporciona una versión localizada del formulario adaptable y se almacena en caché y se envía a todos los usuarios posteriores una instancia del formulario adaptable basada en la primera solicitud (configuración regional del explorador solicitada).

Siga estos pasos para resolver el problema:

1. Abra el proyecto de Experience Manager.
1. Abra `dispatcher/scr/conf.d/rewrites/rewrite.rules` para editarlo.
1. Abra `conf.d/httpd-dispatcher.conf` o cualquier otro archivo de configuración configurado para cargarse durante la ejecución.
1. Agregue el siguiente código al archivo y guárdelo. Es un código de ejemplo, puede modificarlo para adaptarlo a su entorno.

```shellscript
    # Handle actual URL convention (just pass through)
    RewriteRule "^/content/forms/af/(.*)[.](.*).html$" "/content/forms/af/$1.$2.html" [PT]
    
    # Handle selector-based redirection based on browser language
    <VirtualHost *:80>
            # Handle actual URL convention (just pass through)
    RewriteRule "^/content/forms/af/(.*)[.](.*).html$" "/content/forms/af/$1.$2.html" [PT]

    # Handle selector based redirection basded on browser language
    # The Rewrite Condition is looking for the Accept-Language header and if found takes the first two characters which most likely are the desired language selector.
    RewriteCond %{HTTP:Accept-Language} ^(..).*$ [NC]
    RewriteRule "^/content/forms/af/(.*).html$" "/content/forms/af/$1.%1.html" [R]
    RewriteRule "^/content/forms/af/(.*).html$" "/content/forms/af/$1.%1.html" [R]
```

## El almacenamiento en caché de CDN deja de funcionar pasados 300 segundos {#cdn-caching-stops-working-after-300-seconds}

El almacenamiento en caché de CDN deja de funcionar pasados 300 segundos y todas las solicitudes de caché en CDN se redirigen a Dispatcher.

Para resolver el problema, establezca el encabezado age en 0:

1. Cree un archivo en `src\conf.d\available_vhosts`. 

1. Añada lo siguiente al archivo para establecer el encabezado age.

   ```shellscript
       <IfModule mod_headers.c>
               Header add X-Vhost "publish"
               Header set age 0
       </IfModule>
   ```

1. Guarde y cierre el archivo.
1. Modifique el vínculo de software de `src\conf.d\enabled_vhosts\default.vhost` para que apunte al nuevo archivo.
