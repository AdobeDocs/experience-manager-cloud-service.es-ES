---
title: Dispatcher en la nube
description: 'Dispatcher en la nube '
feature: Dispatcher
exl-id: 6d78026b-687e-434e-b59d-9d101349a707
source-git-commit: cf42e530136d5eb8afe7204ae0af1353b1f31cbd
workflow-type: tm+mt
source-wordcount: '4247'
ht-degree: 6%

---

# Dispatcher en la nube {#Dispatcher-in-the-cloud}

>[!CONTEXTUALHELP]
>id="aemcloud_nonbpa_dispoverview"
>title="Dispatcher en la nube"
>abstract="En esta sección se describe cómo estructurar el AEM como una configuración de Apache y Dispatcher Cloud Service, así como cómo validarlo y ejecutarlo localmente antes de implementarlo en entornos en la nube. También describe la depuración en entornos de Cloud."

## Configuración y prueba de Apache y Dispatcher {#apache-and-dispatcher-configuration-and-testing}

En esta sección se describe cómo estructurar el AEM como una configuración de Apache y Dispatcher Cloud Service, así como cómo validarlo y ejecutarlo localmente antes de implementarlo en entornos en la nube. También describe la depuración en entornos de Cloud. Para obtener más información sobre Dispatcher, consulte la [AEM documentación de Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html?lang=es).

>[!NOTE]
>Los usuarios de Windows deben utilizar Windows 10 Professional u otras distribuciones compatibles con Docker. Este es un requisito previo para ejecutar y depurar Dispatcher en un equipo local. Las secciones siguientes incluyen comandos que utilizan las versiones Mac o Linux del SDK, pero el SDK de Windows se puede utilizar de forma similar.

## Herramientas de Dispatcher {#dispatcher-sdk}

Las herramientas de Dispatcher forman parte del AEM general como SDK de Cloud Service y proporcionan:

* Una estructura de archivos vainilla que contiene los archivos de configuración que se van a incluir en un proyecto maven para Dispatcher.
* Herramientas para que los clientes validen que la configuración de Dispatcher incluye solo AEM como directivas admitidas por el Cloud Service.        Además, la herramienta también valida que la sintaxis es correcta para que Apache pueda iniciarse correctamente.
* Imagen de Docker que muestra Dispatcher localmente.

## Descarga y extracción de las herramientas {#extracting-the-sdk}

Las herramientas de Dispatcher, que forman parte del [AEM as a Cloud Service SDK](/help/implementing/developing/introduction/aem-as-a-cloud-service-sdk.md), se pueden descargar desde un archivo zip en el portal [Software Distribution](https://downloads.experiencecloud.adobe.com/content/software-distribution/en/aemcloud.html). Cualquier configuración nueva disponible en esa nueva versión de las herramientas de Dispatcher se puede usar para implementar en entornos de nube que ejecuten esa versión de AEM en la nube o posterior.

Descomprima el SDK, que agrupa las herramientas de Dispatcher para macOS, Linux y Windows.

**Para macOS/Linux**, haga ejecutable el artefacto de la herramienta Dispatcher y ejecútelo. Extraerá los archivos de herramientas de Dispatcher debajo del directorio en el que los almacenó (donde `version` es la versión de las herramientas de Dispatcher).

```bash
$ chmod +x aem-sdk-dispatcher-tools-<version>-unix.sh
$ ./aem-sdk-dispatcher-tools-<version>-unix.sh
Verifying archive integrity...  100%   All good.
Uncompressing aem-sdk-dispatcher-tools-<version>-unix.sh 100%
```

**Para Windows**, extraiga el archivo zip de la herramienta Dispatcher.

## Estructura de archivos {#file-structure}

La estructura de la subcarpeta Dispatcher del proyecto se describe a continuación y debe copiarse en la carpeta Dispatcher del proyecto maven:

```bash
./
├── conf.d
│   ├── available_vhosts
│   │   └── default.vhost
│   ├── dispatcher_vhost.conf
│   ├── enabled_vhosts
│   │   ├── README
│   │   └── default.vhost -> ../available_vhosts/default.vhost
│   └── rewrites
│   │   ├── default_rewrite.rules
│   │   └── rewrite.rules
│   └── variables
|       ├── custom.vars
│       └── global.vars
└── conf.dispatcher.d
    ├── available_farms
    │   └── default.farm
    ├── cache
    │   ├── default_invalidate.any
    │   ├── default_rules.any
    │   └── rules.any
    ├── clientheaders
    │   ├── clientheaders.any
    │   └── default_clientheaders.any
    ├── dispatcher.any
    ├── enabled_farms
    │   ├── README
    │   └── default.farm -> ../available_farms/default.farm
    ├── filters
    │   ├── default_filters.any
    │   └── filters.any
    ├── renders
    │   └── default_renders.any
    └── virtualhosts
        ├── default_virtualhosts.any
        └── virtualhosts.any
```

A continuación se muestra una explicación de los archivos importantes que se pueden modificar:

**Archivos personalizables**

Los siguientes archivos se pueden personalizar y se transferirán a la instancia de Cloud en la implementación:

* `conf.d/available_vhosts/<CUSTOMER_CHOICE>.vhost`

Puede tener uno o más de estos archivos. Contienen entradas `<VirtualHost>` que coinciden con los nombres de host y permiten que Apache gestione cada tráfico de dominio con reglas diferentes. Los archivos se crean en el directorio `available_vhosts` y se habilitan con un vínculo simbólico en el directorio `enabled_vhosts`. Desde los archivos `.vhost`, se incluirán otros archivos como reescrituras y variables.

* `conf.d/rewrites/rewrite.rules`

Este archivo se incluye desde dentro de sus `.vhost` archivos. Tiene un conjunto de reglas de reescritura para `mod_rewrite`.

>[!NOTE]
>
>Actualmente, se debe utilizar un solo archivo de reescritura en lugar de archivos específicos del sitio. Como regla, la suma del contenido de los archivos personalizables debe ser inferior a 1 MB.

* `conf.d/variables/custom.vars`

Este archivo se incluye desde dentro de sus `.vhost` archivos. Puede añadir definiciones para variables de Apache en esta ubicación.

* `conf.d/variables/global.vars`

Este archivo se incluye desde el archivo `dispatcher_vhost.conf`. Puede cambiar el nivel de Dispatcher y reescribir el registro en este archivo.

* `conf.dispatcher.d/available_farms/<CUSTOMER_CHOICE>.farm`

Puede tener uno o más de estos archivos y contienen granjas que coinciden con los nombres de host y permiten que el módulo de Dispatcher gestione cada granja con reglas diferentes. Los archivos se crean en el directorio `available_farms` y se habilitan con un vínculo simbólico en el directorio `enabled_farms`. Desde los archivos `.farm`, se incluirán otros archivos como filtros, reglas de caché y otros.

* `conf.dispatcher.d/cache/rules.any`

Este archivo se incluye desde dentro de sus `.farm` archivos. Especifica las preferencias de almacenamiento en caché.

* `conf.dispatcher.d/clientheaders/clientheaders.any`

Este archivo se incluye desde dentro de sus `.farm` archivos. Especifica qué encabezados de solicitud se deben reenviar al servidor.

* `conf.dispatcher.d/filters/filters.any`

Este archivo se incluye desde dentro de sus `.farm` archivos. Tiene un conjunto de reglas que cambian qué tráfico debe filtrarse y no llegar al servidor.

* `conf.dispatcher.d/virtualhosts/virtualhosts.any`

Este archivo se incluye desde dentro de sus `.farm` archivos. Tiene una lista de nombres de host o rutas de URI a las que se debe hacer coincidir mediante la coincidencia global. Esto determina qué servidor utilizar para servir una solicitud.

Los archivos anteriores hacen referencia a los archivos de configuración inmutables enumerados a continuación. Dispatcher no procesará los cambios en los archivos inmutables en los entornos de Cloud.

**Archivos de configuración inmutables**

Estos archivos forman parte del marco base y aplican las normas y prácticas recomendadas. Los archivos se consideran inmutables porque modificarlos o eliminarlos localmente no afectarán a la implementación, ya que no se transferirán a la instancia de Cloud.

Se recomienda que los archivos anteriores hagan referencia a los archivos inmutables que se enumeran a continuación, seguidos de las instrucciones o anulaciones adicionales. Cuando la configuración de Dispatcher se implementa en un entorno de nube, se utilizará la versión más reciente de los archivos inmutables, independientemente de la versión que se haya utilizado en el desarrollo local.

* `conf.d/available_vhosts/default.vhost`

Contiene un host virtual de ejemplo. Para su propio host virtual, cree una copia de este archivo, personalícelo, vaya a `conf.d/enabled_vhosts` y cree un enlace simbólico a su copia personalizada.

* `conf.d/dispatcher_vhost.conf`

Parte del marco base, utilizado para ilustrar cómo se incluyen los hosts virtuales y las variables globales.

* `conf.d/rewrites/default_rewrite.rules`

Reglas de reescritura predeterminadas adecuadas para un proyecto estándar. Si necesita personalización, modifique `rewrite.rules`. En la personalización, puede incluir primero las reglas predeterminadas si se adaptan a sus necesidades.

* `conf.dispatcher.d/available_farms/default.farm`

Contiene una granja de Dispatcher de muestra. Para su propia granja, cree una copia de este archivo, personalícelo, vaya a `conf.d/enabled_farms` y cree un enlace simbólico a su copia personalizada.

* `conf.dispatcher.d/cache/default_invalidate.any`

Parte del marco base, se genera al inicio. Es **necesario** para incluir este archivo en cada granja que defina, en la sección `cache/allowedClients`.

* `conf.dispatcher.d/cache/default_rules.any`

Reglas de caché predeterminadas adecuadas para un proyecto estándar. Si necesita personalización, modifique `conf.dispatcher.d/cache/rules.any`. En la personalización, puede incluir primero las reglas predeterminadas si se adaptan a sus necesidades.

* `conf.dispatcher.d/clientheaders/default_clientheaders.any`

Encabezados de solicitud predeterminados para reenviar al servidor, adecuados para un proyecto estándar. Si necesita personalización, modifique `clientheaders.any`. En la personalización, puede incluir primero los encabezados de solicitud predeterminados si se adaptan a sus necesidades.

* `conf.dispatcher.d/dispatcher.any`

Parte del marco base, utilizado para ilustrar cómo se incluyen las granjas de Dispatcher.

* `conf.dispatcher.d/filters/default_filters.any`

Filtros predeterminados adecuados para un proyecto estándar. Si necesita personalización, modifique `filters.any`. En la personalización, puede incluir primero los filtros predeterminados si se adaptan a sus necesidades.

* `conf.dispatcher.d/renders/default_renders.any`

Este archivo forma parte del marco base y se genera al inicio. Es **necesario** para incluir este archivo en cada granja que defina, en la sección `renders`.

* `conf.dispatcher.d/virtualhosts/default_virtualhosts.any`

Globalización de host predeterminada adecuada para un proyecto estándar. Si necesita personalización, modifique `virtualhosts.any`. En la personalización, no debe incluir la globalización de host predeterminada, ya que coincide con **cada** solicitud entrante.

>[!NOTE]
>
>El tipo de archivo AEM como Cloud Service maven generará la misma estructura de archivos de configuración de Dispatcher.

Las secciones siguientes describen cómo se valida la configuración localmente para que pueda pasar el control de calidad asociado en Cloud Manager al implementar una versión interna.

## Validación local de directivas compatibles en la configuración {#local-validation-of-dispatcher-configuration} de Dispatcher

La herramienta de validación está disponible en el SDK en `bin/validator` como binario de Mac OS, Linux o Windows, lo que permite a los clientes ejecutar la misma validación que Cloud Manager realizará al crear e implementar una versión.

Se invoca como: `validator full [-d folder] [-w allowlist] zip-file | src folder`

La herramienta valida que la configuración de Dispatcher está utilizando las directivas adecuadas admitidas por AEM as a Cloud Service al analizar todos los archivos con el patrón `conf.d/enabled_vhosts/*.vhost`.

En Windows, el validador de Dispatcher distingue entre mayúsculas y minúsculas. Como tal, puede no validar la configuración si no respeta el uso de mayúsculas en la ruta en la que reside la configuración, por ejemplo:

```
bin\validator.exe full src
Cloud manager validator 2.0.xx
2021/03/15 18:15:40 Dispatcher configuration validation failed:
  conf.dispatcher.d\available_farms\default.farm:15: parent directory outside server root: c:\k\a\aem-dispatcher-sdk-windows-symlinks-testing3\dispatcher\src
  
```

Evite este error copiando y pegando la ruta desde el Explorador de Windows y luego en el símbolo del sistema utilizando un comando `cd` en esa ruta.

Las directivas permitidas en los archivos de configuración de Apache se pueden enumerar ejecutando el comando de lista de permitidos del validador:

```
$ validator allowlist
Cloud manager validator 2.0.4
 
Allowlisted directives:
  <Directory>
  ...
  
```

La tabla siguiente muestra los módulos Apache admitidos:

| Nombre del módulo | Página de referencia |
|---|---|
| `core` | [https://httpd.apache.org/docs/2.4/mod/core.html](https://httpd.apache.org/docs/2.4/mod/core.html) |
| `mod_access_compat` | [https://httpd.apache.org/docs/2.4/mod/mod_access_compat.html](https://httpd.apache.org/docs/2.4/mod/mod_access_compat.html) |
| `mod_alias` | [https://httpd.apache.org/docs/2.4/mod/mod_alias.html](https://httpd.apache.org/docs/2.4/mod/mod_alias.html) |
| `mod_allowmethods` | [https://httpd.apache.org/docs/2.4/mod/mod_allowmethods.html](https://httpd.apache.org/docs/2.4/mod/mod_allowmethods.html) |
| `mod_authn_core` | [https://httpd.apache.org/docs/2.4/mod/mod_authn_core.html](https://httpd.apache.org/docs/2.4/mod/mod_authn_core.html) |
| `mod_authn_file` | [https://httpd.apache.org/docs/2.4/mod/core.html](https://httpd.apache.org/docs/2.4/mod/mod_authn_file.html) |
| `mod_authz_core` | [https://httpd.apache.org/docs/2.4/mod/core.html](https://httpd.apache.org/docs/2.4/mod/mod_authz_core.html) |
| `mod_authz_groupfile` | [https://httpd.apache.org/docs/2.4/mod/mod_authz_groupfile.html](https://httpd.apache.org/docs/2.4/mod/mod_authz_groupfile.html) |
| `mod_deflate` | [https://httpd.apache.org/docs/2.4/mod/mod_deflate.html](https://httpd.apache.org/docs/2.4/mod/mod_deflate.html) |
| `mod_dir` | [https://httpd.apache.org/docs/2.4/mod/mod_dir.html](https://httpd.apache.org/docs/2.4/mod/mod_dir.html) |
| `mod_env` | [https://httpd.apache.org/docs/2.4/mod/mod_env.html](https://httpd.apache.org/docs/2.4/mod/mod_env.html) |
| `mod_filter` | [https://httpd.apache.org/docs/2.4/mod/mod_filter.html](https://httpd.apache.org/docs/2.4/mod/mod_filter.html) |
| `mod_headers` | [https://httpd.apache.org/docs/2.4/mod/mod_headers.html](https://httpd.apache.org/docs/2.4/mod/mod_headers.html) |
| `mod_mime` | [https://httpd.apache.org/docs/2.4/mod/mod_mime.html](https://httpd.apache.org/docs/2.4/mod/mod_mime.html) |
| `mod_proxy` | [https://httpd.apache.org/docs/2.4/mod/mod_proxy.html](https://httpd.apache.org/docs/2.4/mod/mod_proxy.html) |
| `mod_proxy_http` | [https://httpd.apache.org/docs/2.4/mod/mod_proxy_http.html](https://httpd.apache.org/docs/2.4/mod/mod_proxy_http.html) |
| `mod_remoteip` | [https://httpd.apache.org/docs/2.4/mod/mod_remoteip.html](https://httpd.apache.org/docs/2.4/mod/mod_remoteip.html) |
| `mod_reqtimeout` | [https://httpd.apache.org/docs/2.4/mod/mod_reqtimeout.html](https://httpd.apache.org/docs/2.4/mod/mod_reqtimeout.html) |
| `mod_rewrite` | [https://httpd.apache.org/docs/2.4/mod/mod_rewrite.html](https://httpd.apache.org/docs/2.4/mod/mod_rewrite.html) |
| `mod_security` | [https://modsecurity.org/](https://modsecurity.org/) |
| `mod_setenvif` | [https://httpd.apache.org/docs/2.4/mod/mod_setenvif.html](https://httpd.apache.org/docs/2.4/mod/mod_setenvif.html) |
| `mod_ssl (only the SSLProxyEngine directive)` | [https://httpd.apache.org/docs/2.4/mod/mod_ssl.html#sslproxyengine](https://httpd.apache.org/docs/2.4/mod/mod_ssl.html#sslproxyengine) |
| `mod_substitute` | [https://httpd.apache.org/docs/2.4/mod/mod_substitute.html](https://httpd.apache.org/docs/2.4/mod/mod_substitute.html) |
| `mod_userdir` | [https://httpd.apache.org/docs/2.4/mod/mod_userdir.html](https://httpd.apache.org/docs/2.4/mod/mod_userdir.html) |

Los clientes no pueden añadir módulos arbitrarios, sin embargo, se pueden considerar módulos adicionales para su inclusión en el producto en el futuro. Los clientes pueden encontrar la lista de directivas disponibles para una versión de Dispatcher determinada ejecutando el comando de lista de permitidos del validador en el SDK, tal como se ha descrito anteriormente.

La lista de permitidos contiene una lista de directivas de Apache que se permiten en una configuración de cliente. Si una directiva no está incluida en la lista de permitidos, la herramienta registra un error y devuelve un código de salida distinto de cero. Si no se proporciona ninguna lista de permitidos en la línea de comandos (que es la forma en que debe invocarse), la herramienta utiliza una lista de permitidos predeterminada que Cloud Manager utilizará para la validación antes de la implementación en entornos de Cloud.

Además, analiza todos los archivos con el patrón `conf.dispatcher.d/enabled_farms/*.farm` y comprueba que:

* No existe ninguna regla de filtro que utilice permite mediante `/glob` (consulte [CVE-2016-0957](https://nvd.nist.gov/vuln/detail/CVE-2016-0957) para obtener más información)
* No se ha expuesto ninguna función de administrador. Por ejemplo, acceso a rutas como `/crx/de or /system/console`.

Cuando se ejecuta con el artefacto maven o su subdirectorio `dispatcher/src`, informará de los errores de validación:

```
$ validator full dispatcher/src
Cloud manager validator 1.0.4
2019/06/19 15:41:37 Apache configuration uses non-allowlisted directives:
  conf.d/enabled_vhosts/aem_publish.vhost:46: LogLevel
2019/06/19 15:41:37 Dispatcher configuration validation failed:
  conf.dispatcher.d/enabled_farms/999_ams_publish_farm.any: filter allows access to CRXDE
```

Tenga en cuenta que la herramienta de validación solo informa del uso prohibido de las directivas de Apache que no se han incluido en la lista de permitidos. No informa de problemas sintácticos o semánticos con la configuración de Apache, ya que esta información solo está disponible para módulos Apache en un entorno en ejecución.

A continuación se presentan técnicas de resolución de problemas para depurar errores de validación comunes que la herramienta genera:

**no se puede localizar una  `conf.dispatcher.d` subcarpeta en el archivo**

El archivo debe contener las carpetas `conf.d` y `conf.dispatcher.d`. Tenga en cuenta que **no debe** usar el prefijo `etc/httpd` en el archivo.

**no se puede encontrar ninguna granja en`conf.dispatcher.d/enabled_farms`**

Las granjas habilitadas deben encontrarse en la subcarpeta mencionada.

**el archivo incluido (...) debe tener el nombre: ...**

Hay dos secciones en la configuración de granja que **debe** incluir un
archivo específico: `/renders` y `/allowedClients` en la sección `/cache`. Esos
las secciones deben tener el siguiente aspecto:

```
/renders {
    $include "../renders/default_renders.any"
}
```

y:

```
/allowedClients {
    $include "../cache/default_invalidate.any"
}
```

**archivo incluido en una ubicación desconocida: ...**

Hay cuatro secciones en la configuración de la granja en las que puede incluir su propio archivo: `/clientheaders`, `filters`, `/rules` en la sección `/cache` y `/virtualhosts`. Los archivos incluidos deben tener el siguiente nombre:

| Sección | Incluir nombre de archivo |
|------------------|--------------------------------------|
| `/clientheaders` | `../clientheaders/clientheaders.any` |
| `/filters` | `../filters/filters.any` |
| `/rules` | `../cache/rules.any` |
| `/virtualhosts` | `../virtualhosts/virtualhosts.any` |

También puede incluir la versión **predeterminada** de esos archivos, cuyos nombres van precedidos de la palabra `default_`, por ejemplo `../filters/default_filters.any`.

**include en (...), fuera de cualquier ubicación conocida: ...**

Aparte de las seis secciones mencionadas en los párrafos anteriores, no está permitido
para utilizar la instrucción `$include`, por ejemplo, lo siguiente generaría este error:

```
/invalidate {
    $include "../cache/invalidate.any"
}
```

**los clientes/renderizadores permitidos no se incluyen desde: ...**

Este error se genera cuando no especifica una inclusión para `/renders` y `/allowedClients` en la sección `/cache`. Consulte la
El nombre del archivo **incluido (...) debe ser: ...** para obtener más información.

**El filtro no debe utilizar el patrón glob para permitir solicitudes**

No es seguro permitir solicitudes con una regla de estilo `/glob`, que se compara con la línea de solicitud completa, por ejemplo

```
/0100 {
    /type "allow" /glob "GET *.css *"
}
```

Esta instrucción está pensada para permitir solicitudes para archivos `css`, pero también permite solicitudes para **cualquier** recurso seguido de la cadena de consulta `?a=.css`. Por lo tanto, está prohibido utilizar estos filtros (véase también CVE-2016-0957).

**el archivo incluido (...) no coincide con ningún archivo conocido**

Hay dos tipos de archivos en la configuración del host virtual Apache que se pueden especificar como incluye: reescrituras y variables.
Los archivos incluidos deben tener el siguiente nombre:

| Tipo | Incluir nombre de archivo |
|-----------|---------------------------------|
| Reescrituras | `conf.d/rewrites/rewrite.rules` |
| Variables | `conf.d/variables/custom.vars` |

Como alternativa, puede incluir la versión **predeterminada** de las reglas de reescritura, cuyo nombre es `conf.d/rewrites/default_rewrite.rules`.
Tenga en cuenta que no hay una versión predeterminada de los archivos de variables.

**Se detectó un diseño de configuración obsoleto, habilitando el modo de compatibilidad**

Este mensaje indica que la configuración tiene el diseño de versión 1 obsoleto, que contiene una
Configuración de Apache y archivos con prefijos `ams_`. Aunque esto sigue siendo compatible con versiones anteriores
compatibilidad, debe cambiar al nuevo diseño.

## Validación local de la sintaxis de configuración de Dispatcher para que apache httpd pueda iniciarse {#local-validation}

Una vez que se haya establecido que la configuración del módulo de Dispatcher incluye solo directivas compatibles, debe comprobar que la sintaxis sea correcta para que Apache pueda iniciarse. Para probar esto, el docker debe estar instalado localmente. Y tenga en cuenta que no es necesario que AEM esté corriendo.

Utilice el script `validate.sh` como se muestra a continuación:

```
$ validate.sh src/dispatcher
Phase 1: Dispatcher validator
2019/06/19 16:02:55 No issues found
Phase 1 finished
Phase 2: httpd -t validation in docker image
Running script /docker_entrypoint.d/10-create-docroots.sh
Running script /docker_entrypoint.d/20-wait-for-backend.sh
Waiting until aemhost is available
aemhost resolves to xx.xx.xx.xx
Running script /docker_entrypoint.d/30-allowed-clients.sh
# Dispatcher configuration: (/etc/httpd/conf.dispatcher.d/dispatcher.any)
/farms {
...
}
Syntax OK
Phase 2 finished
```

La secuencia de comandos hace lo siguiente:

1. Ejecuta el validador de la sección anterior para asegurarse de que solo se incluyen las directivas compatibles. Si la configuración no es válida, la secuencia de comandos falla.
2. Ejecuta el `httpd -t command` para comprobar si la sintaxis es correcta, de modo que apache httpd pueda iniciarse. Si la configuración se realiza correctamente, debe estar lista para la implementación.
3. Comprueba que el subconjunto de los archivos de configuración del SDK de Dispatcher, que están pensados para ser inmutables como se describe en la sección [Estructura del archivo](#file-structure), no se haya modificado. Esta es una nueva comprobación, introducida con AEM versión v2021.1.4738 del SDK que también incluye la versión 2.0.36 de las herramientas de Dispatcher. Antes de esta actualización, los clientes podían haber asumido incorrectamente que cualquier modificación del SDK local de esos archivos inmutables también se aplicaría al entorno de Cloud.

Durante una implementación de Cloud Manager, la comprobación `httpd -t syntax` también se ejecutará y cualquier error se incluirá en el registro de Cloud Manager `Build Images step failure`.

## Prueba de la configuración de Apache y Dispatcher localmente {#testing-apache-and-dispatcher-configuration-locally}

También es posible probar la configuración local de Apache y Dispatcher. Requiere que el docker se instale localmente y su configuración para pasar la validación como se describe anteriormente.

Ejecute la herramienta de validación (tenga en cuenta que es diferente de la `validator.sh` mencionada anteriormente), utilizando el parámetro `-d` que genera una carpeta con todos los archivos de configuración de Dispatcher. A continuación, ejecute la secuencia de comandos `docker_run.sh` pasando esa carpeta como argumento. Proporcionando el número de puerto (aquí: 8080) para exponer el extremo de Dispatcher, se inicia un contenedor Docker, ejecutando Dispatcher con su configuración.

```
$ validator full -d out src/dispatcher
2019/06/19 16:02:55 No issues found
$ docker_run.sh out docker.for.mac.localhost:4503 8080
Running script /docker_entrypoint.d/10-create-docroots.sh
Running script /docker_entrypoint.d/20-wait-for-backend.sh
Waiting until aemhost is available
aemhost resolves to xx.xx.xx.xx
Running script /docker_entrypoint.d/30-allowed-clients.sh
Starting httpd server
...
```

Esto inicia Dispatcher en un contenedor con su backend que señala a una instancia de AEM que se ejecuta en su equipo Mac OS local en el puerto 4503.

## Depuración de la configuración de Apache y Dispatcher {#debugging-apache-and-dispatcher-configuration}

La siguiente estrategia se puede utilizar para aumentar la salida de registro para el módulo Dispatcher y ver los resultados de la evaluación `RewriteRule` en entornos locales y de nube.

Los niveles de registro para esos módulos se definen mediante las variables `DISP_LOG_LEVEL` y `REWRITE_LOG_LEVEL`. Se pueden configurar en el archivo `conf.d/variables/global.vars`. Su parte pertinente es la siguiente:

```
# Log level for the dispatcher
#
# Possible values are: Error, Warn, Info, Debug and Trace1
# Default value: Warn
#
# Define DISP_LOG_LEVEL Warn
 
# Log level for mod_rewrite
#
# Possible values are: Error, Warn, Info, Debug and Trace1 - Trace8
# Default value: Warn
#
# To debug your RewriteRules, it is recommended to raise your log
# level to Trace2.
#
# More information can be found at:
# https://httpd.apache.org/docs/current/mod/mod_rewrite.html#logging
#
# Define REWRITE_LOG_LEVEL Warn
```

Al ejecutar Dispatcher localmente, los registros se imprimen directamente en la salida de terminal. La mayoría de las veces, desea que estos registros estén en DEBUG, lo que se puede hacer pasando el nivel de depuración como parámetro al ejecutar Docker. Por ejemplo: `DISP_LOG_LEVEL=Debug ./bin/docker_run.sh out docker.for.mac.localhost:4503 8080`.

Los registros para entornos de nube se exponen a través del servicio de registro disponible en Cloud Manager.

## Diferentes configuraciones de Dispatcher por entorno {#different-dispatcher-configurations-per-environment}

Actualmente, la misma configuración de Dispatcher se aplica a todos los AEM como entornos de Cloud Service. El motor de ejecución tendrá una variable de entorno `ENVIRONMENT_TYPE` que contiene el modo de ejecución actual (dev, stage o prod), así como una definición. La definición puede ser `ENVIRONMENT_DEV`, `ENVIRONMENT_STAGE` o `ENVIRONMENT_PROD`. En la configuración de Apache, la variable se puede utilizar directamente en una expresión. Como alternativa, la definición se puede utilizar para generar lógica:

```
# Simple usage of the environment variable
ServerName ${ENVIRONMENT_TYPE}.company.com
 
# When more logic is required
<IfDefine ENVIRONMENT_STAGE>
  # These statements are for stage
  Define VIRTUALHOST stage.example.com
</IfDefine>
<IfDefine ENVIRONMENT_PROD>
  # These statements are for production
  Define VIRTUALHOST prod.example.com
</IfDefine>
```

En la configuración de Dispatcher, está disponible la misma variable de entorno. Si se requiere más lógica, defina las variables como se muestra en el ejemplo anterior y, a continuación, utilícelas en la sección de configuración de Dispatcher:

```
/virtualhosts {
  { "${VIRTUALHOST}" }
}
```

Al probar la configuración localmente, puede simular diferentes tipos de entorno pasando la variable `DISP_RUN_MODE` al script `docker_run.sh` directamente:

```
$ DISP_RUN_MODE=stage docker_run.sh out docker.for.mac.localhost:4503 8080
```

El modo de ejecución predeterminado cuando no se pasa un valor para DISP_RUN_MODE es &quot;dev&quot;.
Para obtener una lista completa de las opciones y variables disponibles, ejecute el script `docker_run.sh` sin argumentos.

## Visualización de la configuración de Dispatcher en uso por su contenedor de Docker {#viewing-dispatcher-configuration-in-use-by-docker-container}

Con configuraciones específicas del entorno, puede resultar difícil determinar cómo se ve la configuración real de Dispatcher. Después de haber iniciado su contenedor de docker con `docker_run.sh` puede volcarse de la siguiente manera:

* Determine el ID del contenedor de docker en uso:

```
$ docker ps
CONTAINER ID       IMAGE
d75fbd23b29        adobe/aem-ethos/dispatcher-publish:...
```

* Ejecute la siguiente línea de comandos con ese ID de contenedor:

```
$ docker exec d75fbd23b29 httpd-test
# Dispatcher configuration: (/etc/httpd/conf.dispatcher.d/dispatcher.any)
/farms {
  /publishfarm {
    /clientheaders {
...
```

## Diferencias principales entre AMS Dispatcher y AEM como Cloud Service {#main-differences-between-ams-dispatcher-configuration-and-aem-as-a-cloud-service}

Como se describe en la página de referencia anterior, la configuración de Apache y Dispatcher en AEM como Cloud Service es bastante similar a la de AMS. Las principales diferencias son:

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
