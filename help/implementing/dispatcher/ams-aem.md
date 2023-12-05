---
title: Migración de la configuración de Dispatcher de AMS a AEM as a Cloud Service
description: Migración de la configuración de Dispatcher de AMS a AEM as a Cloud Service
feature: Dispatcher
exl-id: ff7397dd-b6e1-4d08-8e2d-d613af6b81b3
source-git-commit: 2d4ffd5518d671a55e45a1ab6f1fc41ac021fd80
workflow-type: tm+mt
source-wordcount: '1459'
ht-degree: 7%

---

# Migración de la configuración de Dispatcher de AMS a AEM as a Cloud Service {#Dispatcher-in-the-cloud}

## AEM Diferencias principales entre AMS Dispatcher y el as a Cloud Service de la {#main-differences-between-ams-dispatcher-configuration-and-aem-as-a-cloud-service}

AEM La configuración de Apache y Dispatcher en as a Cloud Service es bastante similar a la de AMS. Las principales diferencias son las siguientes:

* AEM En as a Cloud Service, es posible que no se utilicen algunas directivas de Apache (por ejemplo, `Listen` o `LogLevel`)
* AEM En as a Cloud Service, solo se pueden colocar algunas partes de la configuración de Dispatcher en los archivos de inclusión y su nombre es importante. Por ejemplo, las reglas de filtro que desee reutilizar en distintos hosts deben colocarse en un archivo llamado `filters/filters.any`. Consulte la página de referencia para obtener más información.
* AEM En as a Cloud Service, hay una validación adicional para no permitir reglas de filtro escritas mediante `/glob` para evitar problemas de seguridad. Porque `deny *` se utiliza en lugar de `allow *` (que no se puede utilizar), los clientes se benefician de ejecutar Dispatcher localmente y de realizar pruebas y errores, mirando los registros para saber exactamente qué rutas están bloqueando los filtros de Dispatcher para que se puedan agregar.

## AEM Directrices para migrar la configuración de Dispatcher de AMS a la configuración as a Cloud Service de

La estructura de configuración de Dispatcher tiene diferencias entre Managed Services AEM y as a Cloud Service de la. AEM A continuación, se presenta una guía paso a paso sobre cómo migrar de la versión 2 de configuración de AMS Dispatcher a la versión as a Cloud Service de la.

## AEM Cómo convertir un AMS a una configuración de Dispatcher de servicio en la nube de as a Cloud

En la siguiente sección se proporcionan instrucciones paso a paso sobre cómo convertir una configuración de AMS. Se supone que hay un archivo con una estructura similar a la descrita en [Configuración de Dispatcher de Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/getting-started/dispatcher-configurations.html)

### Extraer el archivo y eliminar un prefijo eventual

Extraiga el archivo en una carpeta y asegúrese de que las subcarpetas inmediatas comiencen por `conf`, `conf.d`,
`conf.dispatcher.d` y `conf.modules.d`. Si no lo hacen, muévalos hacia arriba en la jerarquía.

### Elimine las subcarpetas y archivos que no utilice

Eliminación de subcarpetas `conf` y `conf.modules.d`y archivos que coinciden `conf.d/*.conf`.

### Elimine todos los hosts virtuales que no sean de publicación

Elimine cualquier archivo host virtual de `conf.d/enabled_vhosts` que tiene `author`, `unhealthy`, `health`,
`lc` o `flush` en su nombre. Todos los archivos host virtuales de `conf.d/available_vhosts` que no están vinculados a también se pueden eliminar.

### Quitar o comentar secciones de host virtual que no hagan referencia al puerto 80

Si todavía hay secciones en los archivos host virtuales que hagan referencia exclusivamente a otros puertos que no sean el puerto 80, por ejemplo:

```
<VirtualHost *:443>
...
</VirtualHost>
```

elimínelos o haga comentarios. Las frases de estas secciones no se procesan, pero si se conservan, se pueden editar sin efecto, lo que es confuso.

### Verificar reescrituras

Introducir directorio `conf.d/rewrites`.

Elimine cualquier archivo denominado `base_rewrite.rules` y `xforwarded_forcessl_rewrite.rules` y recuerde quitar `Include` instrucciones en los archivos host virtuales que hacen referencia a ellas.

If `conf.d/rewrites` ahora contiene un solo archivo; debe cambiar el nombre a `rewrite.rules` y no olvide adaptar el `Include` también instrucciones que hacen referencia a ese archivo en los archivos host virtuales.

Sin embargo, si la carpeta contiene varios archivos específicos de host virtual, su contenido debe copiarse en el `Include` referencia a ellos en los archivos host virtuales.

### Comprobar variables

Introducir directorio `conf.d/variables`.

Elimine cualquier archivo denominado `ams_default.vars` y recuerde quitar `Include` instrucciones en los archivos host virtuales que hacen referencia a ellas.

If `conf.d/variables` ahora contiene un solo archivo; debe cambiar el nombre a `custom.vars` y no olvide adaptar el `Include` también instrucciones que hacen referencia a ese archivo en los archivos host virtuales.

Sin embargo, si la carpeta contiene varios archivos específicos de host virtual, su contenido debe copiarse en el `Include` referencia a ellos en los archivos host virtuales.

### Eliminar listas de permitidos

Eliminar la carpeta `conf.d/whitelists` y eliminar `Include` instrucciones en los archivos host virtuales que hacen referencia a algún archivo de esa subcarpeta.

### Reemplace cualquier variable que ya no esté disponible

En todos los archivos host virtuales:

Cambiar nombre `PUBLISH_DOCROOT` hasta `DOCROOT`
Elimine las secciones que hacen referencia a variables denominadas `DISP_ID`, `PUBLISH_FORCE_SSL` o `PUBLISH_WHITELIST_ENABLED`

### Compruebe su estado ejecutando el validador

Ejecute el validador de Dispatcher en el directorio, con la variable `httpd` subcomando:

```
$ validator httpd .
```

Si se observan errores relacionados con la falta de archivos include, comprueba si se ha cambiado correctamente el nombre de esos archivos.

Si hay directivas de Apache que no están incluidas en la lista de permitidos, elimínelas.

### Elimine todas las granjas que no sean para publicar

Elimine cualquier archivo de granja en `conf.dispatcher.d/enabled_farms` que tiene `author`, `unhealthy`, `health`,
`lc` o `flush` en su nombre. Todos los archivos de granja en `conf.dispatcher.d/available_farms` que no están vinculados a también se pueden eliminar.

### Cambiar nombre de archivos de granja

Todas las granjas en `conf.dispatcher.d/enabled_farms` debe cambiarse el nombre para que coincida con el patrón `*.farm`, por ejemplo, un archivo de granja llamado `customerX_farm.any` debería cambiarse el nombre `customerX.farm`.

### Comprobar caché

Introducir directorio `conf.dispatcher.d/cache`.

Elimine cualquier archivo con el prefijo `ams_`.

If `conf.dispatcher.d/cache` ahora está vacío, copie el archivo `conf.dispatcher.d/cache/rules.any`
de la configuración estándar de Dispatcher a esta carpeta. La configuración estándar de Dispatcher se encuentra en la carpeta `src` de este SDK. No se olvide de adaptar el
`$include` declaraciones relativas a la `ams_*_cache.any` archivos de reglas también en los archivos de granja.

Si en su lugar `conf.dispatcher.d/cache` ahora contiene un solo archivo con el sufijo `_cache.any`, debe cambiarse el nombre a `rules.any` y no olvide adaptar el `$include` también instrucciones que hacen referencia a ese archivo en los archivos de la granja.

Sin embargo, si la carpeta contiene varios archivos específicos de la granja con ese patrón, su contenido debe copiarse en la carpeta `$include` al hacer referencia a ellos en los archivos de la granja.

Elimine cualquier archivo que tenga el sufijo `_invalidate_allowed.any`.

Copie el archivo `conf.dispatcher.d/cache/default_invalidate_any` AEM de la configuración predeterminada de la nube de Dispatcher a esa ubicación.

En cada archivo de granja, elimine cualquier contenido de la variable `cache/allowedClients` y reemplácelo por:

```
$include "../cache/default_invalidate.any"
```

### Comprobación de encabezados de cliente

Introducir directorio `conf.dispatcher.d/clientheaders`.

Elimine cualquier archivo con el prefijo `ams_`.

If `conf.dispatcher.d/clientheaders` ahora contiene un solo archivo con el sufijo `_clientheaders.any`, debe cambiarse el nombre a `clientheaders.any` y no olvide adaptar el `$include` también instrucciones que hacen referencia a ese archivo en los archivos de la granja.

Sin embargo, si la carpeta contiene varios archivos específicos de la granja con ese patrón, su contenido debe copiarse en la carpeta `$include` al hacer referencia a ellos en los archivos de la granja.

Copie el archivo `conf.dispatcher/clientheaders/default_clientheaders.any` AEM de la configuración predeterminada de Dispatcher as a Cloud Service de la a esa ubicación.

En cada archivo de granja, reemplace cualquier instrucción include clientheader que tenga el siguiente aspecto:

```
$include "/etc/httpd/conf.dispatcher.d/clientheaders/ams_publish_clientheaders.any"
$include "/etc/httpd/conf.dispatcher.d/clientheaders/ams_common_clientheaders.any"
```

con la frase:

```
$include "../clientheaders/default_clientheaders.any"
```

### Comprobar filtro

Introducir directorio `conf.dispatcher.d/filters`.

Elimine cualquier archivo con el prefijo `ams_`.

If `conf.dispatcher.d/filters` ahora contiene un solo archivo al que se debe cambiar el nombre
`filters.any` y no olvide adaptar el `$include` también instrucciones que hacen referencia a ese archivo en los archivos de la granja.

Sin embargo, si la carpeta contiene varios archivos específicos de la granja con ese patrón, su contenido debe copiarse en la carpeta `$include` al hacer referencia a ellos en los archivos de la granja.

Copie el archivo `conf.dispatcher/filters/default_filters.any` AEM de la configuración predeterminada de Dispatcher as a Cloud Service de la a esa ubicación.

En cada archivo de granja, reemplace cualquier filtro que incluya instrucciones que tengan el siguiente aspecto:

```
$include "/etc/httpd/conf.dispatcher.d/filters/ams_publish_filters.any"
```

con la frase:

```
$include "../filters/default_filters.any"
```

### Comprobar procesamientos

Introducir directorio `conf.dispatcher.d/renders`.

Elimina todos los archivos de esa carpeta.

Copie el archivo `conf.dispatcher.d/renders/default_renders.any` AEM de la configuración predeterminada de Dispatcher as a Cloud Service de la a esa ubicación.

En cada archivo de granja, elimine cualquier contenido de la variable `renders` y reemplácelo por:

```
$include "../renders/default_renders.any"
```

### Comprobar hosts virtuales

Cambie el nombre del directorio `conf.dispatcher.d/vhosts` hasta `conf.dispatcher.d/virtualhosts` e introdúzcala.

Elimine cualquier archivo con el prefijo `ams_`.

If `conf.dispatcher.d/virtualhosts` ahora contiene un solo archivo al que se debe cambiar el nombre
`virtualhosts.any` y no olvide adaptar el `$include` también instrucciones que hacen referencia a ese archivo en los archivos de la granja.

Sin embargo, si la carpeta contiene varios archivos específicos de la granja con ese patrón, su contenido debe copiarse en la carpeta `$include` al hacer referencia a ellos en los archivos de la granja.

Copie el archivo `conf.dispatcher/virtualhosts/default_virtualhosts.any` AEM de la configuración predeterminada de Dispatcher as a Cloud Service de la a esa ubicación.

En cada archivo de granja, reemplace cualquier filtro que incluya instrucciones que tengan el siguiente aspecto:

```
$include "/etc/httpd/conf.dispatcher.d/vhosts/ams_publish_vhosts.any"
```

con la frase:

```
$include "../virtualhosts/default_virtualhosts.any"
```

### Compruebe su estado ejecutando el validador

AEM Ejecute el validador de Dispatcher as a Cloud Service de la en el directorio, con el `dispatcher` subcomando:

```
$ validator dispatcher .
```

Si se observan errores relacionados con la falta de archivos include, comprueba si se ha cambiado correctamente el nombre de esos archivos.

Si hay errores relacionados con la variable no definida `PUBLISH_DOCROOT`, renómbrala a `DOCROOT`.

Para ver todos los demás errores, consulte la sección Resolución de problemas de la documentación de la herramienta de validación.

### Pruebe la configuración con una implementación local (requiere la instalación de Docker).

Uso del script `docker_run.sh` AEM en las herramientas de Dispatcher as a Cloud Service de la, puede probar que la configuración no contiene ningún otro error que solo se mostraría en la implementación:

### Paso 1: Generar información de implementación con el validador

```
validator full -d out .
```

Esto valida la configuración completa y genera la información de implementación en `out`

### Paso 2: Inicie Dispatcher en una imagen de docker con esa información de implementación

AEM Con el servidor de publicación de la en ejecución en el equipo macOS, al escuchar el puerto 4503, se puede ejecutar el inicio de Dispatcher delante de ese servidor de la siguiente manera:

```
$ docker_run.sh out docker.for.mac.localhost:4503 8080
```

Esto inicia el contenedor y expone a Apache en el puerto local 8080.

### Utilice la nueva configuración de Dispatcher

Felicitaciones. Si el validador ya no informa ningún problema y el contenedor de docker se inicia sin errores ni advertencias, está listo para mover la configuración a una `dispatcher/src` subdirectorio del repositorio de Git.

**Los clientes que utilizan la versión 1 de configuración de AMS Dispatcher deben ponerse en contacto con el servicio de atención al cliente para ayudarles a migrar de la versión 1 a la versión 2 y así poder seguir las instrucciones anteriores.**
