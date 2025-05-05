---
title: Migración de la configuración de Dispatcher de AMS a AEM as a Cloud Service
description: Migración de la configuración de Dispatcher de AMS a AEM as a Cloud Service
feature: Dispatcher
exl-id: ff7397dd-b6e1-4d08-8e2d-d613af6b81b3
role: Admin
source-git-commit: 0e328d013f3c5b9b965010e4e410b6fda2de042e
workflow-type: tm+mt
source-wordcount: '1499'
ht-degree: 7%

---

# Migración de la configuración de Dispatcher de AMS a AEM as a Cloud Service {#Dispatcher-in-the-cloud}

## Principales diferencias entre AMS Dispatcher y AEM as a Cloud Service {#main-differences-between-ams-dispatcher-configuration-and-aem-as-a-cloud-service}

La configuración de Apache y Dispatcher en AEM as a Cloud Service es bastante similar a la de AMS. Las principales diferencias son las siguientes:

* En AEM as a Cloud Service, algunas directivas de Apache no pueden usarse (por ejemplo, `Listen` o `LogLevel`)
* En AEM as a Cloud Service, solo se pueden colocar algunas partes de la configuración de Dispatcher en archivos de inclusión y su nombre es importante. Por ejemplo, las reglas de filtro que desee reutilizar en hosts diferentes deben colocarse en un archivo denominado `filters/filters.any`. Consulte la página de referencia para obtener más información.
* En AEM as a Cloud Service, hay una validación adicional para no permitir reglas de filtro escritas con `/glob` para evitar problemas de seguridad. Dado que `deny *` se utiliza en lugar de `allow *` (que no se puede usar), los clientes se benefician de ejecutar Dispatcher localmente y realizar pruebas y errores, mirando los registros para saber exactamente qué rutas están bloqueando los filtros de Dispatcher para que se puedan agregar.
* En AEM as a Cloud Service, actualmente se recomienda encarecidamente [incluirse para utilizar el modo de fuente flexible de la configuración de Dispatcher](/help/implementing/dispatcher/disp-overview.md#validation-debug), por ejemplo, para utilizar canalizaciones de configuración de nivel web o tener una mejor flexibilidad en el número y la estructura de los archivos de configuración.

## Directrices para migrar la configuración de Dispatcher de AMS a AEM as a Cloud Service

La estructura de configuración de Dispatcher tiene diferencias entre Managed Services y AEM as a Cloud Service. A continuación se presenta una guía paso a paso sobre cómo migrar de la configuración 2 de AMS Dispatcher a AEM as a Cloud Service.

## AEM Cómo convertir una configuración de AMS a una configuración de Dispatcher de as a Cloud Service de

En la siguiente sección se proporcionan instrucciones paso a paso sobre cómo convertir una configuración de AMS. Supone que
que tiene un archivo con una estructura similar a la descrita en [Configuración de Cloud Manager Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/getting-started/dispatcher-configurations.html?lang=es)

### Extraer el archivo y eliminar un prefijo eventual

Extraiga el archivo en una carpeta y asegúrese de que las subcarpetas inmediatas comiencen con `conf`, `conf.d`,
`conf.dispatcher.d` y `conf.modules.d`. Si no lo hacen, muévalos hacia arriba en la jerarquía.

### Elimine las subcarpetas y archivos que no utilice

Quite las subcarpetas `conf` y `conf.modules.d`, y los archivos que coinciden con `conf.d/*.conf`.

### Elimine todos los hosts virtuales que no sean de publicación

Quitar cualquier archivo host virtual de `conf.d/enabled_vhosts` que tenga `author`, `unhealthy`, `health`,
`lc` o `flush` en su nombre. Todos los archivos host virtuales de `conf.d/available_vhosts` que no están disponibles
enlazado a también se puede eliminar.

### Quitar o comentar secciones de host virtual que no hagan referencia al puerto 80

Si todavía hay secciones en los archivos host virtuales que hagan referencia exclusivamente a otros puertos que no sean el puerto 80, por ejemplo:

```
<VirtualHost *:443>
...
</VirtualHost>
```

elimínelos o haga comentarios. Las instrucciones de estas secciones no se procesarán, pero si
Si se mantienen, es posible que se terminen editando sin ningún efecto, lo que resulta confuso.

### Verificar reescrituras

Escriba el directorio `conf.d/rewrites`.

Elimine cualquier archivo con los nombres `base_rewrite.rules` y `xforwarded_forcessl_rewrite.rules` y recuerde hacerlo
elimine `Include` frases en los archivos host virtuales que hacen referencia a ellas.

Si `conf.d/rewrites` contiene ahora un solo archivo, debería cambiar el nombre a `rewrite.rules` y no lo haga
olvide adaptar también las frases `Include` que hacen referencia a ese archivo en los archivos host virtuales.

Sin embargo, si la carpeta contiene varios archivos específicos de host virtual, su contenido debe ser
se ha copiado en la instrucción `Include` que hace referencia a ellos en los archivos host virtuales.

### Comprobar variables

Escriba el directorio `conf.d/variables`.

Elimine cualquier archivo de nombre `ams_default.vars` y recuerde eliminar las instrucciones `Include` en el archivo virtual
archivos host que hacen referencia a ellos.

Si `conf.d/variables` contiene ahora un solo archivo, debería cambiar el nombre a `custom.vars` y no lo haga
olvide adaptar también las frases `Include` que hacen referencia a ese archivo en los archivos host virtuales.

Sin embargo, si la carpeta contiene varios archivos específicos de host virtual, su contenido debe ser
se ha copiado en la instrucción `Include` que hace referencia a ellos en los archivos host virtuales.

### Eliminar listas de permitidos

Quite la carpeta `conf.d/whitelists` y las instrucciones `Include` de los archivos host virtuales que hacen referencia a
algún archivo en esa subcarpeta.

### Reemplace cualquier variable que ya no esté disponible

En todos los archivos host virtuales:

Cambiar nombre de `PUBLISH_DOCROOT` a `DOCROOT`
Elimine las secciones que hagan referencia a las variables denominadas `DISP_ID`, `PUBLISH_FORCE_SSL` o `PUBLISH_WHITELIST_ENABLED`

### Compruebe su estado ejecutando el validador

Ejecute el validador de Dispatcher en el directorio, con el subcomando `httpd`:

```
$ validator httpd .
```

Si se observan errores relacionados con la falta de archivos include, comprueba si se ha cambiado correctamente el nombre de esos archivos
archivos.

Si hay directivas de Apache que no están incluidas en la lista de permitidos, elimínelas.

### Elimine todas las granjas que no sean para publicar

Quitar cualquier archivo de granja en `conf.dispatcher.d/enabled_farms` que tenga `author`, `unhealthy`, `health`,
`lc` o `flush` en su nombre. Todos los archivos de granja en `conf.dispatcher.d/available_farms` que no están disponibles
enlazado a también se puede eliminar.

### Cambiar nombre de archivos de granja

Se debe cambiar el nombre de todas las granjas de `conf.dispatcher.d/enabled_farms` para que coincidan con el patrón `*.farm`, por ejemplo, a
el nombre del archivo de granja de servidores denominado `customerX_farm.any` debe cambiarse a `customerX.farm`.

### Comprobar caché

Escriba el directorio `conf.dispatcher.d/cache`.

Elimine cualquier archivo con el prefijo `ams_`.

Si `conf.dispatcher.d/cache` está ahora vacío, copie el archivo `conf.dispatcher.d/cache/rules.any`
de la configuración estándar de Dispatcher a esta carpeta. El Dispatcher estándar
La configuración de se encuentra en la carpeta `src` de este SDK. No se olvide de adaptar el
`$include` frases que hacen referencia a los archivos de regla `ams_*_cache.any` en los archivos de granja
y también.

Si en su lugar `conf.dispatcher.d/cache` contiene ahora un solo archivo con el sufijo `_cache.any`,
debe cambiarse el nombre a `rules.any` y no olvidar adaptar las instrucciones `$include`
haciendo referencia a ese archivo en los archivos de la granja.

Sin embargo, si la carpeta contiene varios archivos específicos de la granja con ese patrón, su contenido
debe copiarse a la instrucción `$include` que hace referencia a ellos en los archivos de granja.

Elimine cualquier archivo que tenga el sufijo `_invalidate_allowed.any`.

Copie el archivo `conf.dispatcher.d/cache/default_invalidate_any` del archivo predeterminado
AEM en la configuración de Cloud Dispatcher, a esa ubicación.

En cada archivo de granja, quite el contenido de la sección `cache/allowedClients` y reemplácelo
con:

```
$include "../cache/default_invalidate.any"
```

### Comprobación de encabezados de cliente

Escriba el directorio `conf.dispatcher.d/clientheaders`.

Elimine cualquier archivo con el prefijo `ams_`.

Si `conf.dispatcher.d/clientheaders` contiene ahora un solo archivo con el sufijo `_clientheaders.any`,
debe cambiarse el nombre a `clientheaders.any` y no olvidar adaptar las instrucciones `$include`
haciendo referencia a ese archivo en los archivos de la granja.

Sin embargo, si la carpeta contiene varios archivos específicos de la granja con ese patrón, su contenido
debe copiarse a la instrucción `$include` que hace referencia a ellos en los archivos de granja.

Copie el archivo `conf.dispatcher/clientheaders/default_clientheaders.any` del archivo predeterminado
Configuración de AEM as a Cloud Service Dispatcher en esa ubicación.

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

Escriba el directorio `conf.dispatcher.d/filters`.

Elimine cualquier archivo con el prefijo `ams_`.

Si `conf.dispatcher.d/filters` contiene ahora un solo archivo, se debe cambiar el nombre a
`filters.any` y no se olvide de adaptar las frases `$include` que hacen referencia a eso
también en los archivos de la granja.

Sin embargo, si la carpeta contiene varios archivos específicos de la granja con ese patrón, su contenido
debe copiarse a la instrucción `$include` que hace referencia a ellos en los archivos de granja.

Copie el archivo `conf.dispatcher/filters/default_filters.any` del archivo predeterminado
Configuración de AEM as a Cloud Service Dispatcher en esa ubicación.

En cada archivo de granja, reemplace cualquier filtro que incluya instrucciones que tengan el siguiente aspecto:

```
$include "/etc/httpd/conf.dispatcher.d/filters/ams_publish_filters.any"
```

con la frase:

```
$include "../filters/default_filters.any"
```

### Comprobar procesamientos

Escriba el directorio `conf.dispatcher.d/renders`.

Elimina todos los archivos de esa carpeta.

Copie el archivo `conf.dispatcher.d/renders/default_renders.any` del archivo predeterminado
Configuración de AEM as a Cloud Service Dispatcher en esa ubicación.

En cada archivo de granja, quite el contenido de la sección `renders` y reemplácelo
con:

```
$include "../renders/default_renders.any"
```

### Comprobar hosts virtuales

Cambie el nombre del directorio `conf.dispatcher.d/vhosts` a `conf.dispatcher.d/virtualhosts` e ingréselo.

Elimine cualquier archivo con el prefijo `ams_`.

Si `conf.dispatcher.d/virtualhosts` contiene ahora un solo archivo, se debe cambiar el nombre a
`virtualhosts.any` y no se olvide de adaptar las frases `$include` que hacen referencia a eso
también en los archivos de la granja.

Sin embargo, si la carpeta contiene varios archivos específicos de la granja con ese patrón, su contenido
debe copiarse a la instrucción `$include` que hace referencia a ellos en los archivos de granja.

Copie el archivo `conf.dispatcher/virtualhosts/default_virtualhosts.any` del archivo predeterminado
Configuración de AEM as a Cloud Service Dispatcher en esa ubicación.

En cada archivo de granja, reemplace cualquier filtro que incluya instrucciones que tengan el siguiente aspecto:

```
$include "/etc/httpd/conf.dispatcher.d/vhosts/ams_publish_vhosts.any"
```

con la frase:

```
$include "../virtualhosts/default_virtualhosts.any"
```

### Compruebe su estado ejecutando el validador

Ejecute el validador de AEM as a Cloud Service Dispatcher en el directorio, con el subcomando `dispatcher`:

```
$ validator dispatcher .
```

Si se observan errores relacionados con la falta de archivos include, comprueba si se ha cambiado correctamente el nombre de esos archivos
archivos.

Si hay errores relacionados con la variable no definida `PUBLISH_DOCROOT`, renómbrala a `DOCROOT`.

Para consultar los demás errores, consulte la sección Resolución de problemas de la
documentación de la herramienta de validación.

### Pruebe la configuración con una implementación local (requiere la instalación de Docker).

Con el script `docker_run.sh` en las herramientas de AEM as a Cloud Service Dispatcher, puede probar que
su configuración no contiene ningún otro error que solo se mostraría en
implementación:

### Paso 1: Generar información de implementación con el validador

```
validator full -d out .
```

Esto valida la configuración completa y genera la información de implementación en `out`

### Paso 2: Inicie Dispatcher en una imagen de docker con esa información de implementación

AEM Con el servidor de publicación de la en ejecución en el equipo macOS, escuchando en el puerto 4503,
puede ejecutar el inicio de Dispatcher delante de ese servidor de la siguiente manera:

```
$ docker_run.sh out docker.for.mac.localhost:4503 8080
```

Esto inicia el contenedor y expone a Apache en el puerto local 8080.

### Utilice la nueva configuración de Dispatcher

Enhorabuena. Si el validador ya no informa ningún problema y la variable
el contenedor de docker se inicia sin errores ni advertencias.
listo para mover la configuración a un subdirectorio `dispatcher/src`
del repositorio de Git.

**Los clientes que usen la versión 1 de configuración de Dispatcher de AMS deben ponerse en contacto con el servicio de atención al cliente para ayudarles a migrar de la versión 1 a la versión 2, de modo que se puedan seguir las instrucciones anteriores.**
