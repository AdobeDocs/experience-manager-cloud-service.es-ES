---
title: Migración de la configuración de Dispatcher de AMS a AEM as a Cloud Service
description: Migración de la configuración de Dispatcher de AMS a AEM as a Cloud Service
feature: Dispatcher
exl-id: ff7397dd-b6e1-4d08-8e2d-d613af6b81b3
source-git-commit: 96a0dacf69f6f9c5744f224d1a48b2afa11fb09e
workflow-type: tm+mt
source-wordcount: '1446'
ht-degree: 16%

---

# Migración de la configuración de Dispatcher de AMS a AEM as a Cloud Service {#Dispatcher-in-the-cloud}

## Diferencias principales entre AMS Dispatcher y AEM as a Cloud Service {#main-differences-between-ams-dispatcher-configuration-and-aem-as-a-cloud-service}

La configuración de Apache y Dispatcher en AEM as a Cloud Service es bastante similar a la de AMS. Las principales diferencias son:

* En AEM as a Cloud Service, es posible que algunas directivas de Apache no se utilicen (por ejemplo, `Listen` o `LogLevel`)
* En AEM as a Cloud Service, solo se pueden colocar algunos fragmentos de la configuración de Dispatcher en archivos de inclusión y su nombre es importante. Por ejemplo, las reglas de filtro que desee reutilizar en diferentes hosts deben colocarse en un archivo llamado `filters/filters.any`. Consulte la página de referencia para obtener más información.
* En AEM as a Cloud Service hay una validación adicional para no permitir reglas de filtro escritas usando `/glob` para evitar problemas de seguridad. Since `deny *` se utilizará en lugar de `allow *` (que no se puede usar), los clientes se beneficiarán de ejecutar Dispatcher localmente y hacer pruebas y errores, mirando los registros para saber exactamente qué rutas bloquean los filtros de Dispatcher para que se puedan agregar.

## Directrices para migrar la configuración de Dispatcher de AMS a AEM as a Cloud Service

La estructura de configuración de Dispatcher tiene diferencias entre Managed Services y AEM as a Cloud Service. A continuación se presenta una guía paso a paso sobre cómo migrar de la versión 2 de la configuración de AMS Dispatcher a AEM as a Cloud Service.

## Conversión de AMS a una configuración de Dispatcher de AEM as a Cloud Service

La siguiente sección proporciona instrucciones paso a paso sobre cómo convertir una configuración de AMS. Se supone que tiene un archivo con una estructura similar a la descrita en [Configuración de Cloud Manager Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/getting-started/dispatcher-configurations.html)

### Extraer el archivo y eliminar un prefijo eventual

Extraiga el archivo en una carpeta y asegúrese de que las subcarpetas inmediatas empiecen por `conf`, `conf.d`,
`conf.dispatcher.d` y `conf.modules.d`. Si no lo hacen, muévalos arriba en la jerarquía.

### Elimine las subcarpetas y archivos que no utilice

Eliminar subcarpetas `conf` y `conf.modules.d`, así como los archivos que coinciden `conf.d/*.conf`.

### Elimine todos los hosts virtuales que no sean de publicación

Elimine cualquier archivo host virtual de `conf.d/enabled_vhosts` que `author`, `unhealthy`, `health`,
`lc` o `flush` en su nombre. Todos los archivos host virtuales de `conf.d/available_vhosts` que no están vinculados a se pueden eliminar también.

### Quitar o comentar secciones de host virtual que no hagan referencia al puerto 80

Si todavía tiene secciones en los archivos host virtuales que se refieran exclusivamente a otros puertos que no sean el puerto 80, por ejemplo:

```
<VirtualHost *:443>
...
</VirtualHost>
```


elimínelos o haga comentarios. Las frases de estas secciones no se procesan, pero si se conservan, se pueden editar sin efecto, lo que es confuso.

### Verificar reescrituras

Introducir directorio `conf.d/rewrites`.

Elimine cualquier archivo denominado `base_rewrite.rules` y `xforwarded_forcessl_rewrite.rules` y recuerde quitar `Include` en los archivos host virtuales que hacen referencia a ellos.

If `conf.d/rewrites` ahora contiene un solo archivo, debe cambiarse el nombre a `rewrite.rules` y no olvide adaptar el `Include` también hace referencia a ese archivo en los archivos host virtuales.

Sin embargo, si la carpeta contiene varios archivos específicos del host virtual, su contenido debe copiarse en la variable `Include` que se refiere a ellos en los archivos host virtuales.

### Comprobar variables

Introducir directorio `conf.d/variables`.

Elimine cualquier archivo denominado `ams_default.vars` y recuerde quitar `Include` en los archivos host virtuales que hacen referencia a ellos.

If `conf.d/variables` ahora contiene un solo archivo, debe cambiarse el nombre a `custom.vars` y no olvide adaptar el `Include` también hace referencia a ese archivo en los archivos host virtuales.

Sin embargo, si la carpeta contiene varios archivos específicos del host virtual, su contenido debe copiarse en la variable `Include` que se refiere a ellos en los archivos host virtuales.

### Eliminar listas de permitidos

Eliminar la carpeta `conf.d/whitelists` y quitar `Include` en los archivos host virtuales que hacen referencia a algún archivo de esa subcarpeta.

### Reemplace cualquier variable que ya no esté disponible

En todos los archivos host virtuales:

Cambiar nombre `PUBLISH_DOCROOT` a `DOCROOT`
Eliminar secciones que hagan referencia a variables con nombre `DISP_ID`, `PUBLISH_FORCE_SSL` o `PUBLISH_WHITELIST_ENABLED`

### Comprueba el estado ejecutando el validador

Ejecute el validador de Dispatcher en el directorio, con la variable `httpd` subcomando:

```
$ validator httpd .
```

Si se observan errores en cuanto a la falta de archivos include, comprueba si se ha cambiado correctamente el nombre de esos archivos.

Si ve directivas de Apache que no están incluidas en la lista de permitidos, elimínelas.

### Elimine todas las granjas que no sean para publicar

Elimine cualquier archivo de granja en `conf.dispatcher.d/enabled_farms` que `author`, `unhealthy`, `health`,
`lc` o `flush` en su nombre. Todos los archivos de granja en `conf.dispatcher.d/available_farms` que no están vinculados a se pueden eliminar también.

### Cambiar el nombre de los archivos

Todas las granjas de `conf.d/enabled_farms` debe cambiarse el nombre para que coincida con el patrón `*.farm`, por ejemplo, un archivo de granja llamado `customerX_farm.any` debería cambiarse el nombre `customerX.farm`.

### Compruebe la caché

Introducir directorio `conf.dispatcher.d/cache`.

Elimine cualquier archivo con el prefijo `ams_`.

If `conf.dispatcher.d/cache` ahora está vacío, copie el archivo `conf.dispatcher.d/cache/rules.any`
desde la configuración estándar de Dispatcher a esta carpeta. La configuración estándar de Dispatcher se puede encontrar en la carpeta `src` de este SDK. No olvide adaptar el
`$include` instrucciones que hacen referencia a `ams_*_cache.any` archivos de regla de los archivos de granja.

Si `conf.dispatcher.d/cache` ahora contiene un solo archivo con sufijo `_cache.any`, debe cambiarse el nombre a `rules.any` y no olvide adaptar el `$include` instrucciones que hacen referencia a ese archivo en los archivos de granja también.

Sin embargo, si la carpeta contiene varios archivos específicos de la granja con ese patrón, su contenido debe copiarse en la variable `$include` que se refiere a ellos en los archivos de granja.

Elimine cualquier archivo que tenga el sufijo `_invalidate_allowed.any`.

Copiar el archivo `conf.dispatcher.d/cache/default_invalidate_any` desde la AEM predeterminada de la configuración de Cloud Dispatcher a esa ubicación.

En cada archivo de granja, elimine cualquier contenido del `cache/allowedClients` y sustitúyala por:

```
$include "../cache/default_invalidate.any"
```

### Compruebe los encabezados de cliente

Introducir directorio `conf.dispatcher.d/clientheaders`.

Elimine cualquier archivo con el prefijo `ams_`.

If `conf.dispatcher.d/clientheaders` ahora contiene un solo archivo con sufijo `_clientheaders.any`, debe cambiarse el nombre a `clientheaders.any` y no olvide adaptar el `$include` instrucciones que hacen referencia a ese archivo en los archivos de granja también.

Sin embargo, si la carpeta contiene varios archivos específicos de la granja con ese patrón, su contenido debe copiarse en la variable `$include` que se refiere a ellos en los archivos de granja.

Copiar el archivo `conf.dispatcher/clientheaders/default_clientheaders.any` desde la configuración predeterminada AEM as a Cloud Service de Dispatcher a esa ubicación.

En cada archivo de granja, reemplace cualquier clientheader include instrucción que tenga el siguiente aspecto:

```
$include "/etc/httpd/conf.dispatcher.d/clientheaders/ams_publish_clientheaders.any"
$include "/etc/httpd/conf.dispatcher.d/clientheaders/ams_common_clientheaders.any"
```

con la frase:

```
$include "../clientheaders/default_clientheaders.any"
```

### Comprueba el filtro

Introducir directorio `conf.dispatcher.d/filters`.

Elimine cualquier archivo con el prefijo `ams_`.

If `conf.dispatcher.d/filters` ahora contiene un solo archivo con el que debería cambiarse el nombre a
`filters.any` y no olvide adaptar el `$include` instrucciones que hacen referencia a ese archivo en los archivos de granja también.

Sin embargo, si la carpeta contiene varios archivos específicos de la granja con ese patrón, su contenido debe copiarse en la variable `$include` que se refiere a ellos en los archivos de granja.

Copiar el archivo `conf.dispatcher/filters/default_filters.any` desde la configuración predeterminada AEM as a Cloud Service de Dispatcher a esa ubicación.

En cada archivo de granja, reemplace cualquier filtro que incluya instrucciones que tengan el siguiente aspecto:

```
$include "/etc/httpd/conf.dispatcher.d/filters/ams_publish_filters.any"
```

con la frase:

```
$include "../filters/default_filters.any"
```

### Compruebe las representaciones

Introducir directorio `conf.dispatcher.d/renders`.

Elimina todos los archivos de esa carpeta.

Copiar el archivo `conf.dispatcher.d/renders/default_renders.any` desde la configuración predeterminada AEM as a Cloud Service de Dispatcher a esa ubicación.

En cada archivo de granja, elimine cualquier contenido del `renders` y sustitúyala por:

```
$include "../renders/default_renders.any"
```

### Comprueba los hosts virtuales

Cambiar el nombre del directorio `conf.dispatcher.d/vhosts` a `conf.dispatcher.d/virtualhosts` y escriba.

Elimine cualquier archivo con el prefijo `ams_`.

If `conf.dispatcher.d/virtualhosts` ahora contiene un solo archivo con el que debería cambiarse el nombre a
`virtualhosts.any` y no olvide adaptar el `$include` instrucciones que hacen referencia a ese archivo en los archivos de granja también.

Sin embargo, si la carpeta contiene varios archivos específicos de la granja con ese patrón, su contenido debe copiarse en la variable `$include` que se refiere a ellos en los archivos de granja.

Copiar el archivo `conf.dispatcher/virtualhosts/default_virtualhosts.any` desde la configuración predeterminada AEM as a Cloud Service de Dispatcher a esa ubicación.

En cada archivo de granja, reemplace cualquier filtro que incluya instrucciones que tengan el siguiente aspecto:

```
$include "/etc/httpd/conf.dispatcher.d/vhosts/ams_publish_vhosts.any"
```

con la frase:

```
$include "../virtualhosts/default_virtualhosts.any"
```

### Comprueba el estado ejecutando el validador

Ejecute el validador de Dispatcher as a Cloud Service de AEM en el directorio, con el `dispatcher` subcomando:

```
$ validator dispatcher .
```

Si se observan errores en cuanto a la falta de archivos include, comprueba si se ha cambiado correctamente el nombre de esos archivos.

Si hay errores relacionados con la variable no definida `PUBLISH_DOCROOT`, renómbrala a `DOCROOT`.

Para consulta por cualquier otro error, consulte la sección Resolución de problemas de la documentación de la herramienta de validación.

### Pruebe la configuración con una implementación local (requiere la instalación de Docker)

Uso de la secuencia de comandos `docker_run.sh` en las AEM herramientas as a Cloud Service de Dispatcher, puede probar que la configuración no contiene ningún otro error que solo se mostraría en la implementación:

### Paso 1: Generar información de implementación con el validador

```
validator full -d out .
```

Esto valida la configuración completa y genera la información de implementación en `out`

### Paso 2: Inicie Dispatcher en una imagen de docker con esa información de implementación

Con el servidor de publicación de AEM en ejecución en el equipo macOS, escuchando el puerto 4503, puede ejecutar el inicio de Dispatcher delante de ese servidor de la siguiente manera:

```
$ docker_run.sh out docker.for.mac.localhost:4503 8080
```

Esto inicia el contenedor y expone a Apache en el puerto local 8080.

### Usar la nueva configuración de Dispatcher

Felicitaciones! Si el validador ya no informa ningún problema y el contenedor de docker se inicia sin errores ni advertencias, está listo para mover la configuración a un `dispatcher/src` subdirectorio del repositorio de Git.

**Los clientes que usen la versión 1 de la configuración de AMS Dispatcher deben ponerse en contacto con el servicio de atención al cliente para ayudarles a migrar de la versión 1 a la versión 2, de modo que se puedan seguir las instrucciones anteriores.**
