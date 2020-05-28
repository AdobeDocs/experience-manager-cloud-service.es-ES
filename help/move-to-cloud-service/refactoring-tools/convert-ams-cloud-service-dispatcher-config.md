---
title: Conversión de un AMS a una configuración de Adobe Experience Manager como distribuidor de servicios en la nube
description: Conversión de un AMS a una configuración de Adobe Experience Manager como distribuidor de servicios en la nube
translation-type: tm+mt
source-git-commit: 3478827949356c4a4f5133b54c6cf809f416efef
workflow-type: tm+mt
source-wordcount: '1342'
ht-degree: 0%

---


# Conversión de un AMS a Adobe Experience Manager (AEM) como una configuración del distribuidor de servicios en la nube

## Introducción {#introduction}

Esta sección proporciona instrucciones paso a paso sobre cómo convertir una configuración de AMS.

>[!NOTE]
>Supone que tiene un archivo con una estructura similar a la descrita en [Administrar las configuraciones](https://docs.adobe.com/content/help/en/experience-manager-cloud-manager/using/getting-started/dispatcher-configurations.html)de Dispatcher.

## Pasos para convertir un AMS a AEM como una configuración del distribuidor de servicios en la nube

1. **Extraer el archivo y eliminar un prefijo eventual**

   Extraiga el archivo en una carpeta y asegúrese de que las subcarpetas inmediatas se inicio con conf, conf.d, conf.dispatcher.d y conf.module.d. Si no lo hacen, muévalos arriba en la jerarquía.

1. **Elimine las subcarpetas y archivos no desinundados**

   Elimine las subcarpetas conf y conf.module.d, así como los archivos que coinciden con conf.d/*.conf.

1. **Elimine todos los hosts virtuales que no sean de publicación**

1. **Quitar cualquier archivo host virtual**

   En conf.d/enabled_vhosts que tiene autor, no saludable, salud, lc o vaciado en su nombre. Todos los archivos de host virtuales en conf.d/available_vhosts a los que no se vincula también se pueden eliminar.

1. Quitar o comentar secciones de host virtual que no hagan referencia al puerto 80

   Si aún tiene secciones en los archivos host virtuales que se refieran exclusivamente a otros puertos que no sean el puerto 80, p. ej.

   `<VirtualHost *:443>`
   `...`
   `</VirtualHost>`
eliminarlos o comentarlos. Las sentencias de estas secciones no se procesarán, pero si las mantiene en el lugar, puede que termine editándolas sin ningún efecto, lo que resulta confuso.

1. **Verificar reescrituras**

   * Introduzca el directorio conf.d/reescribe.

   * Quite cualquier archivo denominado base_rewrite.rules y xforwarded_forcesl_rewrite.rules, y recuerde eliminar las instrucciones Include en los archivos host virtuales que hacen referencia a ellas.

   * Si conf.d/reescribe ahora contiene un solo archivo, debe cambiarse su nombre a rewrite.rules y no olvide adaptar también las sentencias Include que hacen referencia a ese archivo en los archivos host virtuales.

   * Sin embargo, si la carpeta contiene varios archivos específicos de host virtual, su contenido debe copiarse en la instrucción Include, que hace referencia a ellos en los archivos de host virtual.

1. **Comprobar variables**

   1. Introduzca el directorio conf.d/variables.

   1. Elimine cualquier archivo llamado ams_default.vars y recuerde eliminar las instrucciones Include en los archivos host virtuales que hacen referencia a ellos.

   1. Si conf.d/variables ahora contiene un solo archivo, debe cambiarse su nombre a custom.vars y no olvide adaptar también las sentencias Include que hacen referencia a ese archivo en los archivos host virtuales.

   1. Sin embargo, si la carpeta contiene varios archivos específicos de host virtual, su contenido debe copiarse en la instrucción Include, que hace referencia a ellos en los archivos de host virtual.

1. **Eliminar listas blancas**

   Elimine la carpeta conf.d/whitelists y elimine las instrucciones Include de los archivos host virtuales que hacen referencia a algún archivo de esa subcarpeta.

1. **Reemplazar cualquier variable que ya no esté disponible**

   En todos los archivos host virtuales:

   Cambiar el nombre de PUBLISH_DOCROOT a DOCROOTRomitar secciones que hagan referencia a variables denominadas DISP_ID, PUBLISH_FORCE_SSL o PUBLISH_WHITELIST_ENABLED

1. **Compruebe su estado ejecutando el validador**

   Ejecute el validador del despachante en el directorio, con el subcomando httpd:

   `$ validator httpd`
Si observa errores en cuanto a la falta de archivos de inclusión, compruebe si ha cambiado correctamente el nombre de esos archivos.

   Si ve directivas de Apache que no están en la lista de direcciones permitidas, elimínelas.

1. **Elimine todas las granjas que no sean de publicación**

   Elimine cualquier archivo de granja de servidores en conf.dispatcher.d/enabled_Granjas que tenga el nombre de autor, insalubre, sanitario, lc o vaciado. Todos los archivos de granja de archivos en conf.dispatcher.d/available_Granjas a los que no se vincula también se pueden eliminar.

1. **Cambiar el nombre de los archivos de granja de servidores**

   Se debe cambiar el nombre de todas las granjas en conf.dispatcher.d/enabled_granjas para que coincidan con el patrón *.arm, por ejemplo un archivo de granja llamado customerX_arm.any debe cambiarse el nombre de customerX.granja.

1. **Comprobar caché**

   Introduzca el directorio conf.dispatcher.d/cache.

   Elimine cualquier archivo con el prefijo ams_.

   Si conf.dispatcher.d/cache está ahora vacío, copie el archivo conf.dispatcher.d/cache/rules.any de la configuración estándar del despachante a esta carpeta. La configuración del despachante estándar se encuentra en la carpeta src de este SDK. No olvide adaptar las sentencias $include que hacen referencia a ams_*_cache.cualquier archivo de regla en los archivos de granja de servidores.

   Si en su lugar conf.dispatcher.d/cache ahora contiene un solo archivo con el sufijo _cache.any, debe cambiarse el nombre a rules.any y no olvide adaptar también las sentencias $include que hacen referencia a ese archivo en los archivos del conjunto de servidores.

   Sin embargo, si la carpeta contiene varios archivos específicos de conjunto de servidores con ese patrón, su contenido debe copiarse en la instrucción $include que hace referencia a ellos en los archivos de conjunto de servidores.

   Elimine cualquier archivo que tenga el sufijo _invalidate_permission.any.

   Copie el archivo conf.dispatcher.d/cache/default_invalidate_any de la configuración predeterminada del distribuidor a esa ubicación.

   En cada archivo de conjunto de servidores, elimine cualquier contenido de la sección cache/allowClients y reemplácelo por:

   $include &quot;../cache/default_invalidate.any&quot;

1. **Comprobar encabezados de cliente**

   Introduzca el directorio conf.dispatcher.d/clientheaders.

   Elimine cualquier archivo con el prefijo ams_.

   Si conf.dispatcher.d/clientheaders ahora contiene un solo archivo con el sufijo _clientheaders.any, debe cambiarse su nombre a clientheaders.any y no olvide adaptar también las sentencias $include que hacen referencia a ese archivo en los archivos del conjunto de servidores.

   Sin embargo, si la carpeta contiene varios archivos específicos de conjunto de servidores con ese patrón, su contenido debe copiarse en la instrucción $include que hace referencia a ellos en los archivos de conjunto de servidores.

   Copie el archivo conf.dispatcher/clientheaders/default_clientheaders.any desde la configuración predeterminada del despachante a esa ubicación.

   En cada archivo de conjunto de servidores, reemplace cualquier mensaje de cliente que incluya instrucciones que tengan el siguiente aspecto:

   `$include "/etc/httpd/conf.dispatcher.d/clientheaders/ams_publish_clientheaders.any"`

   `$include "/etc/httpd/conf.dispatcher.d/clientheaders/ams_common_clientheaders.any"`

   con la declaración:

   `$include "../clientheaders/default_clientheaders.any"`

1. **Comprobar filtro**

   * Introduzca el directorio conf.dispatcher.d/filtros.

   * Elimine cualquier archivo con el prefijo ams_.

   * Si conf.dispatcher.d/filtros ahora contiene un solo archivo, debe cambiarse su nombre a filtros.any y no olvide adaptar también las afirmaciones $include que hacen referencia a ese archivo en los archivos del conjunto de servidores.

   * Sin embargo, si la carpeta contiene varios archivos específicos de conjunto de servidores con ese patrón, su contenido debe copiarse en la instrucción $include que hace referencia a ellos en los archivos de conjunto de servidores.

   * Copie el archivo conf.dispatcher/filters/default_filters.any desde la configuración predeterminada del despachante a esa ubicación.

   * En cada archivo de conjunto de servidores, reemplace cualquier instrucción de inclusión de filtro que tenga el siguiente aspecto:

   * $include `"/etc/httpd/conf.dispatcher.d/filters/ams_publish_filters.any"`con la declaración:

      `$include "../filters/default_filters.any"`

1. **Comprobar representaciones**

   * Introduzca el directorio conf.dispatcher.d/renders.

   * Quite todos los archivos de esa carpeta.

   * Copie el archivo conf.dispatcher.d/renders/default_renders.any de la configuración predeterminada del despachante a esa ubicación.

   * En cada archivo de conjunto de servidores, elimine cualquier contenido de la sección de procesamiento y reemplácelo por:

      `$include "../renders/default_renders.any"`

1. **Comprobar hosts virtuales**

   * Cambie el nombre del directorio `conf.dispatcher.d/vhosts to conf.dispatcher.d/virtualhosts` e introdúzcalo.

   * Elimine cualquier archivo con el prefijo `ams_`.

   * Si conf.dispatcher.d/virtualhosts ahora contiene un solo archivo, debe cambiarse su nombre a virtualhosts.any y no olvide adaptar también las sentencias $include que hacen referencia a ese archivo en los archivos del conjunto de servidores.

   * Sin embargo, si la carpeta contiene varios archivos específicos de conjunto de servidores con ese patrón, su contenido debe copiarse en la instrucción $include que hace referencia a ellos en los archivos de conjunto de servidores.

   * Copie el archivo conf.dispatcher/virtualhosts/default_virtualhosts.any desde la configuración predeterminada del despachante a esa ubicación.

   * En cada archivo de conjunto de servidores, reemplace cualquier instrucción de inclusión de filtro que tenga el siguiente aspecto:

      `$include "/etc/httpd/conf.dispatcher.d/vhosts/ams_publish_vhosts.any"`
con la declaración:

      `$include "../virtualhosts/default_virtualhosts.any"`


1. **Compruebe su estado ejecutando el validador**

   * Ejecute el validador del despachante en el directorio, con el subcomando dispatcher:

      `$ validator dispatcher`

   * Si observa errores en cuanto a la falta de archivos de inclusión, compruebe si ha cambiado correctamente el nombre de esos archivos.

   * Si ve errores relacionados con variables no definidas `PUBLISH_DOCROOT`, cambie el nombre a `DOCROOT`.

   * Para ver cualquier otro error, consulte la sección Resolución de problemas de la documentación de la herramienta de validación.

## Prueba de la configuración con una implementación local {#testing-config-local-deployment}

>[!IMPORTANT]
> La prueba de la configuración con una implementación local requiere la instalación de Docker.

Con la secuencia de comandos `docker_run.sh` en el SDK de Dispatcher, puede probar que la configuración no contiene ningún otro error que solo se mostraría en la implementación:

1. Generar información de implementación con el validador

   `validator full -d out`
Esto valida la configuración completa y genera la información de implementación en su totalidad

1. Inicio del despachante en una imagen de acoplador con esa información de implementación

   Con el servidor de publicación de AEM en ejecución en el equipo MacOS, escuchando en el puerto 4503, puede ejecutar inicio del despachante delante de ese servidor de la siguiente manera:

   `$ docker_run.sh out docker.for.mac.localhost:4503 8080`

   Esto inicio el contenedor y expondrá Apache en el puerto local 8080.

## Uso de la nueva configuración del despachante {#using-dispatcher-config}

Si el validador ya no informa de ningún problema y el contenedor del acoplador se inicio sin errores ni advertencias, estará listo para mover la configuración a un subdirectorio d`ispatcher/src` del repositorio de Git.