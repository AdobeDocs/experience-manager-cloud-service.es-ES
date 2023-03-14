---
title: Conversión de AMS a una configuración de Dispatcher de Adobe Experience Manager as a Cloud Service
description: Conversión de AMS a una configuración de Dispatcher de Adobe Experience Manager as a Cloud Service
source-git-commit: 47910a27118a11a8add6cbcba6a614c6314ffe2a
workflow-type: tm+mt
source-wordcount: '1342'
ht-degree: 95%

---


# Conversión de AMS a una configuración de Dispatcher de Adobe Experience Manager (AEM) as a Cloud Service

## Introducción {#introduction}

Esta sección proporciona las instrucciones paso a paso sobre cómo convertir una configuración de AMS.

>[!NOTE]
>Se supone que hay un archivo con una estructura similar a la descrita en [Administrar las configuraciones de Dispatcher.](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/getting-started/dispatcher-configurations.html)

## Pasos para la configuración de Dispatcher para convertir un AMS a AEM as a Cloud Service

1. **Extraer el archivo y eliminar un prefijo eventual**

   Extraiga el archivo en una carpeta y asegúrese de que las subcarpetas inmediatas comiencen con conf, conf.d, conf.dispatcher.d y conf.module.d. Si no lo hacen, muévalas arriba en la jerarquía.

1. **Elimine las subcarpetas y archivos que no utilice**

   Elimine las subcarpetas conf y conf.module.d, así como los archivos que contengan conf.d/*.conf.

1. **Elimine todos los hosts virtuales que no sean de publicación**

1. **Elimine cualquier archivo host virtual**

   En conf.d/enabled_vhosts que tengan las palabras author, unhealthy, health, lc o flush en su nombre. También se pueden eliminar todos los archivos de host virtuales en conf.d/available_vhosts a los que no se vincula.

1. Quitar o comentar secciones de host virtual que no hagan referencia al puerto 80

   Si todavía hay secciones en los archivos host virtuales que hagan referencia exclusivamente a otros puertos que no sean el puerto 80, por ejemplo,

   `<VirtualHost *:443>`
   `...`
   `</VirtualHost>`
elimínelos o haga comentarios. Las frases de estas secciones no se procesan, pero si se conservan, se pueden editar sin efecto, lo que es confuso.

1. **Verificar reescrituras**

   * Introduzca el directorio conf.d/rewrites.

   * Elimine cualquier archivo denominado base_rewrite.rules y xforwarded_forcesl_rewrite.rules, y recuerde eliminar las frases con Include en los archivos host virtuales que hacen referencia a ellas.

   * Si conf.d/rewrites contiene un solo archivo, debe cambiar el nombre a rewrite.rules y no olvidar adaptar también las frases con Include que hacen referencia a ese archivo en los archivos host virtuales.

   * Sin embargo, si la carpeta contiene varios archivos específicos de host virtual, el contenido debe copiarse en la frase Include, que hace referencia a ellos en los archivos de host virtual.

1. **Comprobar variables**

   1. Introduzca el directorio conf.d/variables.

   1. Elimine cualquier archivo denominado ams_default.vars y recuerde eliminar las frases con Include en los archivos host virtuales que hacen referencia a ellas.

   1. Si conf.d/variables contiene un solo archivo, debe cambiar el nombre a custom.vars y no olvidar adaptar también las frases con Include que hacen referencia a ese archivo en los archivos host virtuales.

   1. Sin embargo, si la carpeta contiene varios archivos específicos de host virtual, el contenido debe copiarse en la frase Include, que hace referencia a ellos en los archivos de host virtual.

1. **Elimine las listas blancas**

   Elimine la carpeta conf.d/whitelists y las frases Include de los archivos host virtuales que hacen referencia a algún archivo de esa subcarpeta.

1. **Reemplace cualquier variable que ya no esté disponible**

   En todos los archivos host virtuales:

   Cambie el nombre de PUBLISH_DOCROOT a DOCROOT
Elimine las secciones que hagan referencia a variables denominadas DISP_ID, PUBLISH_FORCE_SSL o PUBLISH_WHITELIST_ENABLED

1. **Comprueba el estado ejecutando el validador**

   Ejecuta el validador de Dispatcher en el directorio, con el subcomando httpd:

   `$ validator httpd`
Si se observan errores en cuanto a la falta de archivos include, comprueba si se ha cambiado correctamente el nombre de esos archivos.

   Si hay directivas de Apache que no están en la lista blanca, elimínalas.

1. **Elimine todas las granjas que no sean para publicar**

   Elimine cualquier archivo de granja en conf.dispatcher.d/enabled_farms que tenga las palabras author, unhealthy, health, lc o flush en el nombre. También se pueden eliminar todos los archivos de granja en conf.dispatcher.d/available_farms que no estén vinculados.

1. **Cambiar el nombre de los archivos**

   Se debe cambiar el nombre de todas las granjas en conf.dispatcher.d/enabled_farms para que coincidan con el patrón *.farm, por ejemplo, un archivo de granja llamado customerX_farm.any debe cambiarse por el nombre customerX.farm.

1. **Compruebe la caché**

   Introduce el directorio conf.dispatcher.d/cache.

   Elimine cualquier archivo con el prefijo ams_.

   Si conf.dispatcher.d/cache está ahora vacío, copie el archivo conf.dispatcher.d/cache/rules.any de la configuración estándar de Dispatcher a esta carpeta. La configuración de Dispatcher estándar se encuentra en la carpeta src de este SDK. No olvides adaptar las frases $include que hacen referencia a los archivos de regla ams_*_cache.any en los archivos de granja.

   Si en lugar de conf.dispatcher.d/cache contiene ahora un solo archivo con el sufijo _cache.any, debería ser renombrado a rules.any y no se olvide de adaptar las frases $include que se refieren a ese archivo en los archivos de la granja también.

   Sin embargo, si la carpeta contiene varios archivos de granja específicos con ese patrón, su contenido debe copiarse en la frase $include que se refiere a ellos en los archivos de granja.

   Elimine cualquier archivo que tenga el sufijo _invalidate_permission.any.

   Copie el archivo conf.dispatcher.d/cache/default_invalidate_any de la configuración predeterminada de Dispatcher a esa ubicación.

   En cada archivo de granja, elimina cualquier contenido de la sección cache/allowClients y reemplázalo por:

   $include &quot;../cache/default_invalidate.any&quot;

1. **Compruebe los encabezados de cliente**

   Introduce el directorio conf.dispatcher.d/clientheaders.

   Elimine cualquier archivo con el prefijo ams_.

   Si conf.dispatcher.d/clientheaders contiene ahora un solo archivo con el sufijo_clientheaders.any, debería ser renombrado a clientheaders.any y no se olvide de adaptar las frases $include que se refieren a ese archivo en los archivos de la granja.

   Sin embargo, si la carpeta contiene varios archivos de granja específicos con ese patrón, su contenido debe copiarse en la frase $include que se refiere a ellos en los archivos de granja.

   Copie el archivo conf.dispatcher/clientheaders/default_clientheaders.any de la configuración predeterminada de Dispatcher a esa ubicación.

   En cada archivo de granja, reemplace cualquier clientheader que incluya instrucciones que tengan el siguiente aspecto:

   `$include "/etc/httpd/conf.dispatcher.d/clientheaders/ams_publish_clientheaders.any"`

   `$include "/etc/httpd/conf.dispatcher.d/clientheaders/ams_common_clientheaders.any"`

   con la frase:

   `$include "../clientheaders/default_clientheaders.any"`

1. **Comprueba el filtro**

   * Introduce el directorio conf.dispatcher.d/filters.

   * Elimine cualquier archivo con el prefijo ams_.

   * Si conf.dispatcher.d/filters contiene ahora un solo archivo debe renombrarse a filters.any y no se olvide de adaptar las frases $include que se refieren a ese archivo en los archivos de la granja.

   * Sin embargo, si la carpeta contiene varios archivos de granja específicos con ese patrón, su contenido debe copiarse en la frase $include que se refiere a ellos en los archivos de granja.

   * Copie el archivo conf.dispatcher/filters/default_filters.any de la configuración predeterminada de Dispatcher a esa ubicación.

   * En cada archivo de granja, reemplace cualquier filtro que incluya instrucciones que tengan el siguiente aspecto:

   * $include `"/etc/httpd/conf.dispatcher.d/filters/ams_publish_filters.any"`
con la frase:

      `$include "../filters/default_filters.any"`

1. **Compruebe las representaciones**

   * Introduce el directorio conf.dispatcher.d/renders.

   * Elimina todos los archivos de esa carpeta.

   * Copia el archivo conf.dispatcher.d/renders/default_renders.any desde la configuración predeterminada de Dispatcher a esa ubicación.

   * En cada archivo de granja, elimina cualquier contenido de la sección de representaciones y reemplázalo por:

      `$include "../renders/default_renders.any"`

1. **Comprueba los hosts virtuales**

   * Cambia el nombre del directorio a`conf.dispatcher.d/vhosts to conf.dispatcher.d/virtualhosts` e ingrésalo.

   * Elimine cualquier archivo con el prefijo `ams_`.

   * Si conf.dispatcher.d/virtualhosts contiene ahora un solo archivo debe renombrarse a virtualhosts.any y no olvidar adaptar las frases $include que se refieren a ese archivo en los archivos de la granja.

   * Sin embargo, si la carpeta contiene varios archivos de granja específicos con ese patrón, su contenido debe copiarse en la frase $include que se refiere a ellos en los archivos de granja.

   * Copie el archivo conf.dispatcher/virtualhosts/default_virtualhosts.any de la configuración predeterminada de Dispatcher a esa ubicación.

   * En cada archivo de granja, reemplace cualquier filtro que incluya instrucciones que tengan el siguiente aspecto:

      `$include "/etc/httpd/conf.dispatcher.d/vhosts/ams_publish_vhosts.any"`
con la frase:

      `$include "../virtualhosts/default_virtualhosts.any"`


1. **Comprueba el estado ejecutando el validador**

   * Ejecuta el validador de Dispatcher en el directorio, con el subcomando Dispatcher:

      `$ validator dispatcher`

   * Si se observan errores en cuanto a la falta de archivos include, comprueba si se ha cambiado correctamente el nombre de esos archivos.

   * Si hay errores relacionados con la variable no definida `PUBLISH_DOCROOT`, renómbrala a `DOCROOT`.

   * Para consulta por cualquier otro error, consulte la sección Resolución de problemas de la documentación de la herramienta de validación.

## Prueba de la configuración con una implementación local {#testing-config-local-deployment}

>[!IMPORTANT]
>
>La prueba de la configuración con una implementación local requiere la instalación de Docker.

Con la secuencia de comandos `docker_run.sh` en el SDK de Dispatcher, se puede probar que la configuración no contiene ningún otro error que solo se mostraría en la implementación:

1. Generación de la información de implementación con el validador

   `validator full -d out`
Esto valida la configuración completa y genera la información de implementación en su totalidad.

1. Inicio del Dispatcher en una imagen de docker con la información de la implementación

   Con el servidor de publicación de AEM en ejecución en el equipo MacOS, al escuchar el puerto 4503, se puede ejecutar el inicio de Dispatcher delante de ese servidor de la siguiente manera:

   `$ docker_run.sh out docker.for.mac.localhost:4503 8080`

   Esto inicia el contenedor y expone a Apache en el puerto local 8080.

## Uso de la nueva configuración de Dispatcher {#using-dispatcher-config}

Si el validador ya no informa ningún problema y el contenedor de docker se inició sin errores ni advertencias, está listo para mover la configuración al subdirectorio d`ispatcher/src` del repositorio de Git.