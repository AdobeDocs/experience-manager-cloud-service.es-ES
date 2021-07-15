---
title: Migración de la configuración de Dispatcher de AMS a AEM como Cloud Service
description: 'Migración de la configuración de Dispatcher de AMS a AEM como Cloud Service '
feature: Dispatcher
source-git-commit: 19444aacbb86f93e7a5ea8bda2ca3c03a0a44f98
workflow-type: tm+mt
source-wordcount: '1447'
ht-degree: 14%

---

# Migración de la configuración de Dispatcher de AMS a AEM como Cloud Service {#Dispatcher-in-the-cloud}

## Diferencias principales entre AMS Dispatcher y AEM como Cloud Service {#main-differences-between-ams-dispatcher-configuration-and-aem-as-a-cloud-service}

La configuración de Apache y Dispatcher en AEM como Cloud Service es bastante similar a la de AMS. Las principales diferencias son:

* En AEM como Cloud Service, es posible que algunas directivas de Apache no se utilicen (por ejemplo `Listen` o `LogLevel`)
* En AEM como Cloud Service, solo algunas partes de la configuración de Dispatcher se pueden incluir en los archivos include y su nombre es importante. Por ejemplo, las reglas de filtro que desee reutilizar en diferentes hosts deben colocarse en un archivo llamado `filters/filters.any`. Consulte la página de referencia para obtener más información.
* En AEM como Cloud Service, hay una validación adicional para no permitir reglas de filtro escritas usando `/glob` para evitar problemas de seguridad. Dado que `deny *` se utilizará en lugar de `allow *` (que no se puede usar), los clientes se beneficiarán de ejecutar Dispatcher localmente y de hacer pruebas y errores, mirando los registros para saber exactamente qué rutas están bloqueando los filtros de Dispatcher para que se puedan agregar.

## Directrices para migrar la configuración de Dispatcher de AMS a AEM como Cloud Service

La estructura de configuración de Dispatcher tiene diferencias entre Managed Services y AEM como Cloud Service. A continuación, se presenta una guía paso a paso sobre cómo migrar de la configuración AMS Dispatcher versión 2 a AEM como Cloud Service.

## Conversión de AMS a una configuración de Dispatcher de AEM as a Cloud Service

La siguiente sección proporciona instrucciones paso a paso sobre cómo convertir una configuración de AMS. Supone
que tiene un archivo con una estructura similar a la descrita en la [configuración de Dispatcher de Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/getting-started/dispatcher-configurations.html)

### Extraer el archivo y eliminar un prefijo eventual

Extraiga el archivo en una carpeta y asegúrese de que las subcarpetas inmediatas comiencen por `conf`, `conf.d`,
`conf.dispatcher.d` y `conf.modules.d`. Si no lo hacen, muévalos arriba en la jerarquía.

### Elimine las subcarpetas y archivos que no utilice

Elimine las subcarpetas `conf` y `conf.modules.d`, así como los archivos que coincidan con `conf.d/*.conf`.

### Elimine todos los hosts virtuales que no sean de publicación

Elimine cualquier archivo host virtual en `conf.d/enabled_vhosts` que tenga `author`, `unhealthy`, `health`,
`lc` o `flush` en su nombre. Todos los archivos host virtuales en `conf.d/available_vhosts` que no son
enlazado a también se puede eliminar.

### Quitar o comentar secciones de host virtual que no hagan referencia al puerto 80

Si todavía tiene secciones en los archivos host virtuales que se refieran exclusivamente a otros puertos que no sean el puerto 80, por ejemplo:

```
<VirtualHost *:443>
...
</VirtualHost>
```


elimínelos o haga comentarios. Las frases de estas secciones no se procesan, pero si se conservan, se pueden editar sin efecto, lo que es confuso.

### Verificar reescrituras

Introduzca el directorio `conf.d/rewrites`.

Elimine cualquier archivo denominado `base_rewrite.rules` y `xforwarded_forcessl_rewrite.rules` y recuerde
elimine las instrucciones `Include` en los archivos host virtuales que hacen referencia a ellas.

Si `conf.d/rewrites` ahora contiene un solo archivo, debe cambiarse el nombre a `rewrite.rules` y no
olvide adaptar también las instrucciones `Include` que hacen referencia a ese archivo en los archivos host virtuales.

Sin embargo, si la carpeta contiene varios archivos específicos del host virtual, su contenido debe ser
se ha copiado en la instrucción `Include` que hace referencia a ellas en los archivos host virtuales.

### Comprobar variables

Introduzca el directorio `conf.d/variables`.

Elimine cualquier archivo denominado `ams_default.vars` y recuerde eliminar las frases `Include` en el entorno virtual
archivos host que hacen referencia a ellos.

Si `conf.d/variables` ahora contiene un solo archivo, debe cambiarse el nombre a `custom.vars` y no
olvide adaptar también las instrucciones `Include` que hacen referencia a ese archivo en los archivos host virtuales.

Sin embargo, si la carpeta contiene varios archivos específicos del host virtual, su contenido debe ser
se ha copiado en la instrucción `Include` que hace referencia a ellas en los archivos host virtuales.

### Eliminar listas de permitidos

Elimine la carpeta `conf.d/whitelists` y las instrucciones `Include` de los archivos host virtuales que hacen referencia a
algún archivo de esa subcarpeta.

### Reemplace cualquier variable que ya no esté disponible

En todos los archivos host virtuales:

Cambiar el nombre de `PUBLISH_DOCROOT` a `DOCROOT`
Eliminar secciones que hagan referencia a variables denominadas `DISP_ID`, `PUBLISH_FORCE_SSL` o `PUBLISH_WHITELIST_ENABLED`

### Comprueba el estado ejecutando el validador

Ejecute el validador de Dispatcher en el directorio, con el subcomando `httpd`:

```
$ validator httpd .
```

Si se observan errores en cuanto a la falta de archivos include, comprueba si se ha cambiado correctamente el nombre de esos archivos.

Si ve directivas de Apache que no están incluidas en la lista de permitidos, elimínelas.

### Elimine todas las granjas que no sean para publicar

Elimine cualquier archivo de granja en `conf.dispatcher.d/enabled_farms` que tenga `author`, `unhealthy`, `health`,
`lc` o `flush` en su nombre. Todos los archivos de granja en `conf.dispatcher.d/available_farms` que no son
enlazado a también se puede eliminar.

### Cambiar el nombre de los archivos

Se debe cambiar el nombre de todas las granjas de `conf.d/enabled_farms` para que coincidan con el patrón `*.farm`, por ejemplo, a
debe cambiar el nombre del archivo de granja llamado `customerX_farm.any` a `customerX.farm`.

### Compruebe la caché

Introduzca el directorio `conf.dispatcher.d/cache`.

Elimine cualquier archivo con el prefijo `ams_`.

Si `conf.dispatcher.d/cache` está vacío, copie el archivo `conf.dispatcher.d/cache/rules.any`
desde la configuración estándar de Dispatcher a esta carpeta. El Dispatcher estándar
La configuración de se encuentra en la carpeta `src` de este SDK. No olvide adaptar el
Instrucciones `$include` que hacen referencia a los archivos de regla `ams_*_cache.any` en los archivos de granja
también.

Si en su lugar `conf.dispatcher.d/cache` ahora contiene un solo archivo con el sufijo `_cache.any`,
debe cambiarse el nombre a `rules.any` y no olvide adaptar las afirmaciones de `$include`
también se refiere a ese archivo en los archivos de granja.

Sin embargo, si la carpeta contiene varios archivos específicos de la granja con ese patrón, su contenido
debe copiarse en la instrucción `$include` que hace referencia a ellas en los archivos de granja.

Elimine cualquier archivo que tenga el sufijo `_invalidate_allowed.any`.

Copie el archivo `conf.dispatcher.d/cache/default_invalidate_any` desde el valor predeterminado
AEM en la configuración de Cloud Dispatcher a esa ubicación.

En cada archivo de granja, elimine cualquier contenido de la sección `cache/allowedClients` y reemplácelo
con:

```
$include "../cache/default_invalidate.any"
```

### Compruebe los encabezados de cliente

Introduzca el directorio `conf.dispatcher.d/clientheaders`.

Elimine cualquier archivo con el prefijo `ams_`.

Si `conf.dispatcher.d/clientheaders` ahora contiene un solo archivo con el sufijo `_clientheaders.any`,
debe cambiarse el nombre a `clientheaders.any` y no olvide adaptar las afirmaciones de `$include`
también se refiere a ese archivo en los archivos de granja.

Sin embargo, si la carpeta contiene varios archivos específicos de la granja con ese patrón, su contenido
debe copiarse en la instrucción `$include` que hace referencia a ellas en los archivos de granja.

Copie el archivo `conf.dispatcher/clientheaders/default_clientheaders.any` desde el valor predeterminado
AEM como una configuración de Dispatcher de Cloud Service a esa ubicación.

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

Introduzca el directorio `conf.dispatcher.d/filters`.

Elimine cualquier archivo con el prefijo `ams_`.

Si `conf.dispatcher.d/filters` ahora contiene un solo archivo, debe cambiarse el nombre a
`filters.any` y no olvide adaptar las `$include` frases que hacen referencia a eso
en los archivos de granja.

Sin embargo, si la carpeta contiene varios archivos específicos de la granja con ese patrón, su contenido
debe copiarse en la instrucción `$include` que hace referencia a ellas en los archivos de granja.

Copie el archivo `conf.dispatcher/filters/default_filters.any` desde el valor predeterminado
AEM como una configuración de Dispatcher de Cloud Service a esa ubicación.

En cada archivo de granja, reemplace cualquier filtro que incluya instrucciones que tengan el siguiente aspecto:

```
$include "/etc/httpd/conf.dispatcher.d/filters/ams_publish_filters.any"
```

con la frase:

```
$include "../filters/default_filters.any"
```

### Compruebe las representaciones

Introduzca el directorio `conf.dispatcher.d/renders`.

Elimina todos los archivos de esa carpeta.

Copie el archivo `conf.dispatcher.d/renders/default_renders.any` desde el valor predeterminado
AEM como una configuración de Dispatcher de Cloud Service a esa ubicación.

En cada archivo de granja, elimine cualquier contenido de la sección `renders` y reemplácelo
con:

```
$include "../renders/default_renders.any"
```

### Comprueba los hosts virtuales

Cambie el nombre del directorio `conf.dispatcher.d/vhosts` a `conf.dispatcher.d/virtualhosts` e introdúzcalo.

Elimine cualquier archivo con el prefijo `ams_`.

Si `conf.dispatcher.d/virtualhosts` ahora contiene un solo archivo, debe cambiarse el nombre a
`virtualhosts.any` y no olvide adaptar las `$include` frases que hacen referencia a eso
en los archivos de granja.

Sin embargo, si la carpeta contiene varios archivos específicos de la granja con ese patrón, su contenido
debe copiarse en la instrucción `$include` que hace referencia a ellas en los archivos de granja.

Copie el archivo `conf.dispatcher/virtualhosts/default_virtualhosts.any` desde el valor predeterminado
AEM como una configuración de Dispatcher de Cloud Service a esa ubicación.

En cada archivo de granja, reemplace cualquier filtro que incluya instrucciones que tengan el siguiente aspecto:

```
$include "/etc/httpd/conf.dispatcher.d/vhosts/ams_publish_vhosts.any"
```

con la frase:

```
$include "../virtualhosts/default_virtualhosts.any"
```

### Comprueba el estado ejecutando el validador

Ejecute el AEM como validador de Dispatcher Cloud Service en el directorio, con el subcomando `dispatcher`:

```
$ validator dispatcher .
```

Si se observan errores en cuanto a la falta de archivos include, comprueba si se ha cambiado correctamente el nombre de esos archivos.

Si hay errores relacionados con la variable no definida `PUBLISH_DOCROOT`, renómbrala a `DOCROOT`.

Para consulta por cualquier otro error, consulte la sección Resolución de problemas de la documentación de la herramienta de validación.

### Pruebe la configuración con una implementación local (requiere la instalación de Docker)

Con el script `docker_run.sh` en las herramientas de Dispatcher de AEM as a Cloud Service, puede comprobar que
la configuración no contiene ningún otro error que solo se mostraría en
implementación:

### Paso 1: Generar información de implementación con el validador

```
validator full -d out .
```

Esto valida la configuración completa y genera la información de implementación en `out`

### Paso 2: Inicie Dispatcher en una imagen de docker con esa información de implementación

Con el servidor de publicación de AEM en ejecución en el equipo MacOS, escuchando en el puerto 4503,
puede ejecutar el inicio de Dispatcher delante de ese servidor de la siguiente manera:

```
$ docker_run.sh out docker.for.mac.localhost:4503 8080
```

Esto inicia el contenedor y expone a Apache en el puerto local 8080.

### Usar la nueva configuración de Dispatcher

Felicitaciones! Si el validador ya no informa ningún problema y la variable
el contenedor de docker se inicia sin errores ni advertencias.
listo para mover la configuración a un subdirectorio `dispatcher/src`
de su repositorio de Git.

**Los clientes que usen la versión 1 de la configuración de AMS Dispatcher deben ponerse en contacto con el servicio de atención al cliente para ayudarles a migrar de la versión 1 a la versión 2, de modo que se puedan seguir las instrucciones anteriores.**
