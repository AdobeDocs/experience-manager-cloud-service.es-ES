---
title: Validación y depuración mediante las herramientas de Dispatcher
description: Obtenga información sobre la validación local, la depuración, la estructura de archivos en modo flexible y cómo migrar del modo heredado al modo flexible.
feature: Dispatcher
exl-id: 9e8cff20-f897-4901-8638-b1dbd85f44bf
role: Admin
source-git-commit: 0e328d013f3c5b9b965010e4e410b6fda2de042e
workflow-type: tm+mt
source-wordcount: '3028'
ht-degree: 1%

---

# Validación y depuración mediante las herramientas de Dispatcher {#Dispatcher-in-the-cloud}

## Introducción {#apache-and-dispatcher-configuration-and-testing}

>[!NOTE]
>Para obtener más información sobre Dispatcher en la nube y cómo descargar las herramientas de Dispatcher, consulte la página [Dispatcher en la nube](/help/implementing/dispatcher/disp-overview.md). Si la configuración de Dispatcher está en modo heredado, consulte [documentación sobre el modo heredado](/help/implementing/dispatcher/validation-debug-legacy.md).

Las siguientes secciones describen la estructura de archivos en modo flexible, la validación local, la depuración y la migración del modo heredado al modo flexible.

Este artículo supone que la configuración de Dispatcher del proyecto incluye el archivo `opt-in/USE_SOURCES_DIRECTLY`. Este archivo hace que el SDK y el tiempo de ejecución validen e implementen la configuración de una manera mejorada en comparación con el modo heredado, lo que elimina las limitaciones en torno al número y el tamaño de los archivos.

Si la configuración de Dispatcher no incluye el archivo mencionado anteriormente, Adobe recomienda migrar del modo heredado al flexible, tal como se describe en la sección [Migración del modo heredado al modo flexible](#migrating).

## Estructura de archivos {#flexible-mode-file-structure}

La estructura de la subcarpeta Dispatcher del proyecto es la siguiente:

```bash
./
├── conf.d
│   ├── available_vhosts
│   │   ├── my_site.vhost # Created by customer
│   │   └── default.vhost
│   ├── dispatcher_vhost.conf
│   ├── enabled_vhosts
│   │   ├── README
│   │   └── my_site.vhost -> ../available_vhosts/my_site.vhost  # Created by customer
│   └── rewrites
│   │   ├── default_rewrite.rules
│   │   └── rewrite.rules
│   └── variables
|       ├── custom.vars
│       └── global.vars
│── opt-in
│   └── USE_SOURCES_DIRECTLY
└── conf.dispatcher.d
    ├── available_farms
    │   ├── my_farm.farm # Created by customer
    │   └── default.farm
    ├── cache
    │   ├── default_invalidate.any
    │   ├── default_rules.any
    │   ├── marketing_query_parameters.any
    │   └── rules.any
    ├── clientheaders
    │   ├── clientheaders.any
    │   └── default_clientheaders.any
    ├── dispatcher.any
    ├── enabled_farms
    │   ├── README
    │   └── my_farm.farm -> ../available_farms/my_farm.farm  # Created by customer
    ├── filters
    │   ├── default_filters.any
    │   └── filters.any
    ├── renders
    │   └── default_renders.any
    └── virtualhosts
    │   ├── default_virtualhosts.any
    │   └── virtualhosts.any
    
```

A continuación se muestra una explicación de los archivos notables que se pueden modificar:

**Archivos personalizables**

Los siguientes archivos se pueden personalizar y se transfieren a la instancia de Cloud en la implementación:

* `conf.d/available_vhosts/<CUSTOMER_CHOICE>.vhost`

Puede tener uno o más de estos archivos. Contienen `<VirtualHost>` entradas que coinciden con los nombres de host y permiten a Apache gestionar cada tráfico de dominio con reglas diferentes. Los archivos se crean en el directorio `available_vhosts` y se habilitan con un vínculo simbólico en el directorio `enabled_vhosts`. Desde los archivos `.vhost`, se incluyen otros archivos, como reescrituras y variables.

>[!NOTE]
>
>En el modo flexible, debe utilizar rutas relativas en lugar de rutas absolutas.

Asegúrese de que siempre hay disponible al menos un host virtual que coincida con los ServerAlias `\*.local`, `localhost` y `127.0.0.1` necesarios para la invalidación de Dispatcher. Los alias de servidor `*.adobeaemcloud.net` y `*.adobeaemcloud.com` también son necesarios en al menos una configuración vhost y son necesarios para los procesos de Adobe internos.

Si desea buscar coincidencias con el host exacto porque tiene varios archivos vhost, puede seguir el siguiente ejemplo:

```
<VirtualHost *:80>
    ServerName    "example.com"
    # Put names of which domains are used for your published site/content here
    ServerAlias     "*example.com" "\*.local" "localhost" "127.0.0.1" "*.adobeaemcloud.net" "*.adobeaemcloud.com"
    # Use a document root that matches the one in conf.dispatcher.d/default.farm
    DocumentRoot "${DOCROOT}"
    # URI dereferencing algorithm is applied at Sling's level, do not decode parameters here
    AllowEncodedSlashes NoDecode
    # Add header breadcrumbs for help in troubleshooting which vhost file is chosen
    <IfModule mod_headers.c>
        Header add X-Vhost "publish-example-com"
    </IfModule>
  ...
</VirtualHost>
```

* `conf.d/enabled_vhosts/<CUSTOMER_CHOICE>.vhost`

Esta carpeta contiene vínculos simbólicos relativos a archivos en conf.Dispatcher.d/available_vhosts.

Comandos de ejemplo necesarios para crear estos vínculos simbólicos:

Apple macOS, Linux y WSL

```
ln -s ../available_vhosts/wknd.vhost wknd.vhost
```

Microsoft Windows

```
mklink wknd.vhost ..\available_vhosts\wknd.vhost
```

>[!NOTE]
>
> Cuando trabaje con vínculos simbólicos en Windows, debería estar ejecutando un símbolo del sistema elevado, en el Subsistema de Windows para Linux o tener asignado el privilegio [Crear vínculos simbólicos](https://learn.microsoft.com/en-us/windows/security/threat-protection/security-policy-settings/create-symbolic-links).

* `conf.d/rewrites/rewrite.rules`

El archivo se incluye desde dentro de sus `.vhost` archivos. Tiene un conjunto de reglas de reescritura para `mod_rewrite`.

* `conf.d/variables/custom.vars`

El archivo se incluye desde dentro de sus `.vhost` archivos. Puede agregar definiciones para variables de Apache en esta ubicación.

* `conf.d/variables/global.vars`

El archivo se incluye desde dentro del archivo `dispatcher_vhost.conf`. Puede cambiar el Dispatcher y reescribir el nivel de registro en este archivo.

* `conf.dispatcher.d/available_farms/<CUSTOMER_CHOICE>.farm`

Puede tener uno o más de estos archivos, que contienen granjas para que coincidan con los nombres de host y permiten al módulo de Dispatcher gestionar cada granja con reglas diferentes. Los archivos se crean en el directorio `available_farms` y se habilitan con un vínculo simbólico en el directorio `enabled_farms`. De los archivos de `.farm`, se incluyen otros archivos como filtros, reglas de caché y otros.

* `conf.dispatcher.d/enabled_farms/<CUSTOMER_CHOICE>.farm`

Esta carpeta contiene vínculos simbólicos relativos a archivos en conf.Dispatcher.d/available_farms.

Comandos de ejemplo necesarios para crear estos vínculos simbólicos:

Apple macOS, Linux y WSL

```
ln -s ../available_farms/wknd.farm wknd.farm
```

Microsoft Windows

```
mklink wknd.farm ..\available_farms\wknd.farm
```

>[!NOTE]
>
> Cuando trabaje con vínculos simbólicos en Windows, debería estar ejecutando un símbolo del sistema elevado, en el Subsistema de Windows para Linux o tener asignado el privilegio [Crear vínculos simbólicos](https://learn.microsoft.com/en-us/windows/security/threat-protection/security-policy-settings/create-symbolic-links).

* `conf.dispatcher.d/cache/rules.any`

El archivo se incluye desde dentro de sus `.farm` archivos. Especifica las preferencias de almacenamiento en caché.

* `conf.dispatcher.d/clientheaders/clientheaders.any`

El archivo se incluye desde dentro de sus `.farm` archivos. Especifica qué encabezados de solicitud deben reenviarse al servidor.

* `conf.dispatcher.d/filters/filters.any`

El archivo se incluye desde dentro de sus `.farm` archivos. Tiene un conjunto de reglas que cambian el tráfico que debe filtrarse y no llegar al servidor.

* `conf.dispatcher.d/virtualhosts/virtualhosts.any`

El archivo se incluye desde dentro de sus `.farm` archivos. Tiene una lista de nombres de host o rutas URI que deben coincidir con la coincidencia glob. Esta coincidencia determina qué back-end utilizar para servir una solicitud.

* `opt-in/USE_SOURCES_DIRECTLY`

Este archivo permite una configuración de Dispatcher más flexible y elimina las limitaciones anteriores en cuanto al número y el tamaño de los archivos. También hace que el SDK y el tiempo de ejecución validen e implementen la configuración de una manera mejorada.

Los archivos anteriores hacen referencia a los archivos de configuración inmutables que se enumeran a continuación. Los cambios en los archivos inmutables no los procesan los Dispatcher en los entornos de la nube.

**Archivos de configuración inmutables**

Estos archivos forman parte del marco base y aplican estándares y prácticas recomendadas. Los archivos se consideran inmutables porque modificarlos o eliminarlos localmente no tiene ningún impacto en la implementación, ya que no se transfieren a la instancia de Cloud.

Se recomienda que los archivos anteriores hagan referencia a los archivos inmutables que se enumeran a continuación, seguidos de cualquier instrucción o anulación adicional. Cuando la configuración de Dispatcher se implementa en un entorno de nube, se utiliza la versión más reciente de los archivos inmutables, independientemente de la versión que se haya utilizado en el desarrollo local.

* `conf.d/available_vhosts/default.vhost`

Contiene un host virtual de ejemplo. Para su propio host virtual, cree una copia de este archivo, personalícelo, vaya a `conf.d/enabled_vhosts` y cree un vínculo simbólico a su copia personalizada.
No copie el archivo default.vhost directamente en `conf.d/enabled_vhosts`.

Asegúrese de que siempre hay disponible un host virtual que coincida con ServerAlias `\*.local`, `localhost` y `127.0.0.1`, necesarios para la invalidación de Dispatcher. Los alias de servidor `*.adobeaemcloud.net` y `*.adobeaemcloud.com` son necesarios para los procesos de Adobe internos.

* `conf.d/dispatcher_vhost.conf`

Forma parte del marco base, que se utiliza para ilustrar cómo se incluyen los hosts virtuales y las variables globales.

* `conf.d/rewrites/default_rewrite.rules`

Las reglas de reescritura predeterminadas son adecuadas para un proyecto estándar. Si necesita personalizar, modifique `rewrite.rules`. En la personalización, aún puede incluir primero las reglas predeterminadas si se adaptan a sus necesidades.

* `conf.dispatcher.d/available_farms/default.farm`

Contiene un conjunto de servidores de Dispatcher de ejemplo. Para su propia granja de servidores, cree una copia de este archivo, personalícelo, vaya a `conf.d/enabled_farms` y cree un vínculo simbólico a su copia personalizada.

* `conf.dispatcher.d/cache/default_invalidate.any`

Forma parte del marco base y se genera al iniciar. Se **requiere** que incluya este archivo en cada granja que defina, en la sección `cache/allowedClients`.

* `conf.dispatcher.d/cache/default_rules.any`

Reglas de caché predeterminadas adecuadas para un proyecto estándar. Si necesita personalizar, modifique `conf.dispatcher.d/cache/rules.any`. En la personalización, aún puede incluir primero las reglas predeterminadas si se adaptan a sus necesidades.

* `conf.dispatcher.d/clientheaders/default_clientheaders.any`

Encabezados de solicitud predeterminados para reenviar al back-end, adecuados para un proyecto estándar. Si necesita personalizar, modifique `clientheaders.any`. En la personalización, aún puede incluir primero los encabezados de solicitud predeterminados, si se adaptan a sus necesidades.

* `conf.dispatcher.d/dispatcher.any`

Forma parte del marco base, se utiliza para ilustrar cómo se incluyen las granjas de Dispatcher.

* `conf.dispatcher.d/filters/default_filters.any`

Filtros predeterminados adecuados para un proyecto estándar. Si necesita personalizar, modifique `filters.any`. En la personalización, aún puede incluir primero los filtros predeterminados si se adaptan a sus necesidades.

* `conf.dispatcher.d/renders/default_renders.any`

Como parte del marco base, este archivo se genera durante el inicio. Se **requiere** que incluya este archivo en cada granja que defina, en la sección `renders`.

* `conf.dispatcher.d/virtualhosts/default_virtualhosts.any`

Globbing de host predeterminado adecuado para un proyecto estándar. Si necesita personalizar, modifique `virtualhosts.any`. En su personalización, no debe incluir la globalización de host predeterminada, ya que coincide con **cada** solicitud entrante.

## Módulos Apache compatibles {#apache-modules}

Consulte [Módulos Apache compatibles](/help/implementing/dispatcher/disp-overview.md#supported-directives).

## Validación local {#local-validation-flexible-mode}

>[!NOTE]
>
>Las secciones siguientes incluyen comandos que utilizan las versiones Mac o Linux® del SDK, pero el SDK de Windows también se puede utilizar de forma similar.

Usar el script `validate.sh` como se muestra a continuación:

```
$ validate.sh src/dispatcher
opt-in USE_SOURCES_DIRECTLY marker file detected
Phase 1: Dispatcher validator
Cloud manager validator 2.0.32
Phase 1 finished
Phase 2: httpd -t validation in docker image
values.csv not found in deployment folder: /Users/foo/src - using files in 'conf.d' and 'conf.dispatcher.d' subfolders directly
processing configuration subfolder: conf.d
processing configuration subfolder: conf.dispatcher.d
Running script /docker_entrypoint.d/10-check-environment.sh
Running script /docker_entrypoint.d/20-create-docroots.sh
Running script /docker_entrypoint.d/30-wait-for-backend.sh
Waiting until localhost is available
localhost resolves to ::1
Running script /docker_entrypoint.d/40-generate-allowed-clients.sh
Running script /docker_entrypoint.d/50-check-expiration.sh
Running script /docker_entrypoint.d/60-check-loglevel.sh
Running script /docker_entrypoint.d/70-check-forwarded-host-secret.sh
# Dispatcher configuration: (/etc/httpd/conf.dispatcher.d/dispatcher.any)
/farms {

... 

}
Syntax OK
Phase 2 finished
Phase 3: Immutability check
reading immutable file list from /etc/httpd/immutable.files.txt

...

no immutable file has been changed - check is SUCCESSFUL
Phase 3 finished
```

La secuencia de comandos tiene las tres fases siguientes:

1. Ejecuta el validador. Si la configuración no es válida, se produce un error en el script.
2. Ejecuta el comando `httpd -t` para comprobar si la sintaxis es correcta de modo que Apache httpd pueda iniciarse. Si se realiza correctamente, la configuración debe estar lista para la implementación.
3. Comprueba que el subconjunto de los archivos de configuración del SDK de Dispatcher, que se pretende que sean inmutables tal como se describe en la [sección Estructura de archivos](##flexible-mode-file-structure), no se haya modificado y coincida con la versión actual del SDK.

Durante una implementación de Cloud Manager, también se ejecuta la comprobación de sintaxis `httpd -t` y los errores se incluyen en el registro `Build Images step failure` de Cloud Manager.

>[!NOTE]
>
>Consulte la sección [Validación y recarga automáticas](#automatic-loading) para obtener una alternativa eficaz a ejecutar `validate.sh` después de cada modificación de la configuración.

### Fase 1 {#first-phase}

Si una directiva no está incluida en la lista de permitidos, la herramienta registra un error y devuelve un código de salida distinto de cero. Además, analiza más a fondo todos los archivos con el patrón `conf.dispatcher.d/enabled_farms/*.farm` y comprueba lo siguiente:

* No existe ninguna regla de filtro que utilice que permita a través de `/glob` (consulte [CVE-2016-0957](https://nvd.nist.gov/vuln/detail/CVE-2016-0957)) para obtener más detalles.
* No se expone ninguna función de administrador. Por ejemplo, acceso a rutas como `/crx/de or /system/console`.

La herramienta de validación informa únicamente del uso prohibido de directivas de Apache que no se han incluido en la lista de permitidos. No informa de problemas sintácticos o semánticos con la configuración de Apache, ya que esta información solo está disponible para los módulos Apache en un entorno en ejecución.

A continuación se presentan las técnicas de solución de problemas para depurar errores de validación comunes que genera la herramienta:

**No se puede encontrar una subcarpeta `conf.dispatcher.d` en el archivo**

El archivo debe contener las carpetas `conf.d` y `conf.dispatcher.d`. Tenga en cuenta que **no debe** usar el prefijo `etc/httpd` en el archivo.

**No se encuentra ninguna granja en`conf.dispatcher.d/enabled_farms`**

Las granjas habilitadas deben estar en la subcarpeta mencionada.

**El nombre del archivo incluido (...) debe ser: ...**

Hay dos secciones en la configuración de su granja que **debe** incluir
archivo específico: `/renders` y `/allowedClients` en la sección `/cache`. Esos
Las secciones deben tener el siguiente aspecto:

```
/renders {
    $include "../renders/default_renders.any"
}
```

Y:

```
/allowedClients {
    $include "../cache/default_invalidate.any"
}
```

**Archivo incluido en ubicación desconocida: ...**

Hay cuatro secciones en la configuración de la granja en las que se le permite incluir sus propios archivos: `/clientheaders`, `filters`, `/rules` en la sección `/cache` y `/virtualhosts`. Los archivos incluidos deben tener el siguiente nombre:

| Sección | Incluir nombre de archivo |
|------------------|--------------------------------------|
| `/clientheaders` | `../clientheaders/clientheaders.any` |
| `/filters` | `../filters/filters.any` |
| `/rules` | `../cache/rules.any` |
| `/virtualhosts` | `../virtualhosts/virtualhosts.any` |

También puede incluir la versión **default** de esos archivos, cuyos nombres van precedidos de la palabra `default_`, por ejemplo, `../filters/default_filters.any`.

**Instrucción Include en (...), fuera de cualquier ubicación conocida: ...**

Aparte de las seis secciones mencionadas en los párrafos anteriores, no está permitido
para usar la instrucción `$include`, por ejemplo, se generaría este error:

```
/invalidate {
    $include "../cache/invalidate.any"
}
```

**Los clientes/procesamientos permitidos no se incluyen en: ...**

Este error se genera cuando no se especifica una &quot;inclusión&quot; para `/renders` y `/allowedClients` en la sección `/cache`. Consulte la
**el archivo incluido (...) debe tener el nombre: ...** sección para obtener más información.

**El filtro no debe usar el patrón glob para permitir solicitudes**

No es seguro permitir solicitudes con una regla de estilo `/glob`, que coincide con la línea de solicitud completa, por ejemplo,

```
/0100 {
    /type "allow" /glob "GET *.css *"
}
```

Esta instrucción está diseñada para permitir solicitudes para `css` archivos, pero también permite solicitudes a **cualquier** recurso seguido de la cadena de consulta `?a=.css`. Por lo tanto, está prohibido utilizar estos filtros (véase también CVE-2016-0957).

**El archivo incluido (...) no coincide con ningún archivo conocido**

De forma predeterminada, se pueden especificar dos tipos de archivos en la configuración de host virtual de Apache, como incluye: reescrituras y variables.

| Tipo | Incluir nombre de archivo |
|-----------|---------------------------------|
| Reescribe | `conf.d/rewrites/rewrite.rules` |
| Variables | `conf.d/variables/custom.vars` |

En modo flexible, también se pueden incluir otros archivos, siempre y cuando se encuentren en subdirectorios (en cualquier nivel) del directorio `conf.d` con el prefijo siguiente.

| Incluir prefijo de directorio superior de archivo |
|-------------------------------------|
| `conf.d/includes` |
| `conf.d/modsec` |
| `conf.d/rewrites` |

Por ejemplo, puede incluir un archivo en algún directorio creado bajo el directorio `conf.d/includes` de la siguiente manera:

```
Include conf.d/includes/mynewdirectory/myincludefile.conf
```

También puede incluir la versión **default** de las reglas de reescritura, cuyo nombre es `conf.d/rewrites/default_rewrite.rules`.
Tenga en cuenta que no hay una versión predeterminada de los archivos de variables.

**Se ha detectado un diseño de configuración obsoleto, lo que habilita el modo de compatibilidad**

Este mensaje indica que la configuración tiene el diseño de la versión 1 obsoleta, que contiene un
Configuración de Apache y archivos con prefijos `ams_`. Mientras que esta configuración sigue siendo compatible con versiones anteriores
compatibilidad, debe cambiar al nuevo diseño.

La primera fase también puede **ejecutarse por separado**, en lugar de hacerlo desde el script `validate.sh` del contenedor.

Cuando se ejecuta con el artefacto de Maven o el subdirectorio `dispatcher/src`, informa de errores de validación:

```
$ validator full -relaxed dispatcher/src
Cloud manager validator 1.0.4
2019/06/19 15:41:37 Apache configuration uses non-allowlisted directives:
  conf.d/enabled_vhosts/aem_publish.vhost:46: LogLevel
2019/06/19 15:41:37 Dispatcher configuration validation failed:
  conf.dispatcher.d/enabled_farms/999_ams_publish_farm.any: filter allows access to CRXDE
```

En Windows, el validador de Dispatcher distingue entre mayúsculas y minúsculas. Como tal, puede fallar en validar la configuración si no respeta la escritura en mayúsculas de la ruta donde reside la configuración, por ejemplo:

```
bin\validator.exe -relaxed full src
Cloud manager validator 2.0.xx
2021/03/15 18:15:40 Dispatcher configuration validation failed:
  conf.dispatcher.d\available_farms\default.farm:15: parent directory outside server root: c:\k\a\aem-dispatcher-sdk-windows-symlinks-testing3\dispatcher\src
```

Para evitar este error, copie y pegue la ruta de acceso desde el Explorador de Windows y, a continuación, en el símbolo del sistema con un comando `cd` en dicha ruta de acceso.

### Fase 2 {#second-phase}

Esta fase comprueba la sintaxis de Apache iniciando Apache HTTPD en un contenedor de docker. AEM Docker debe estar instalado localmente, pero tenga en cuenta que no es necesario para que se ejecute el programa de instalación de la aplicación de la red de distribución de datos de.

>[!NOTE]
>
>Los usuarios de Windows deben utilizar Windows 10 Professional u otras distribuciones compatibles con Docker. Este requisito es necesario para ejecutar y depurar Dispatcher en un equipo local.
>Para Windows y macOS, Adobe recomienda utilizar Docker Desktop.

Esta fase también se puede ejecutar de forma independiente mediante `bin/docker_run.sh src/dispatcher host.docker.internal:4503 8080`.

Durante una implementación de Cloud Manager, también se ejecuta la comprobación de sintaxis `httpd -t` y los errores se incluyen en el registro de errores de pasos de imágenes de Cloud Manager Build.

### Fase 3 {#third-phase}

Si hay un error en esta fase, implica que el Adobe ha cambiado uno o más archivos inmutables. En tal caso, debe reemplazar los archivos inmutables correspondientes con la nueva versión entregada en el directorio `src` del SDK. La muestra de registro siguiente ilustra este problema:

```
Phase 3: Immutability check
reading immutable file list from /etc/httpd/immutable.files.txt
(...)
checking existing 'conf.dispatcher.d/clientheaders/default_clientheaders.any' for changes
immutable file 'conf.dispatcher.d/clientheaders/default_clientheaders.any' has been changed:
--- /etc/httpd/conf.dispatcher.d/clientheaders/default_clientheaders.any
+++ /etc/httpd-actual/conf.dispatcher.d/clientheaders/default_clientheaders.any
@@ -40,4 +40,3 @@
"Sling-uploadmode"
"x-requested-with"
"If-Modified-Since"
-"Authorization"
** error: immutable file 'conf.dispatcher.d/clientheaders/default_clientheaders.any' has been changed!
  
```

Esta fase también se puede ejecutar de forma independiente mediante `bin/docker_immutability_check.sh src/dispatcher`.

Los archivos inmutables locales se pueden actualizar ejecutando el script `bin/update_maven.sh src/dispatcher` en la carpeta Dispatcher, donde `src/dispatcher` es el directorio de configuración de Dispatcher. Este script también actualiza cualquier archivo `pom.xml` en el directorio principal para que las comprobaciones de inmutabilidad de Maven también se actualicen.

## Depuración de la configuración de Apache y Dispatcher {#debugging-apache-and-dispatcher-configuration}

Puede ejecutar Apache Dispatcher localmente mediante `./bin/docker_run.sh src/dispatcher docker.for.mac.localhost:4503 8080`.

AEM Como se ha indicado anteriormente, Docker debe instalarse localmente y no es necesario para que se ejecute el programa de instalación de la plataforma de datos de la plataforma de datos de la plataforma de datos de la plataforma de datos de. Los usuarios de Windows deben utilizar Windows 10 Professional u otras distribuciones compatibles con Docker. Este requisito es necesario para ejecutar y depurar Dispatcher en un equipo local.

La siguiente estrategia se puede usar para aumentar la salida del registro para el módulo Dispatcher y ver los resultados de la evaluación `RewriteRule` tanto en entornos locales como de nube.

Las variables `DISP_LOG_LEVEL` y `REWRITE_LOG_LEVEL` definen los niveles de registro de esos módulos. Se pueden establecer en el archivo `conf.d/variables/global.vars`. La parte pertinente es la siguiente:

```
# Log level for the dispatcher
#
# Possible values are: error, warn, info, debug and trace1
# Default value: warn
#
# Define DISP_LOG_LEVEL warn
 
# Log level for mod_rewrite
#
# Possible values are: error, warn, info, debug and trace1 - trace8
# Default value: warn
#
# To debug your RewriteRules, it is recommended to raise your log
# level to trace2.
#
# More information can be found at:
# https://httpd.apache.org/docs/current/mod/mod_rewrite.html#logging
#
# Define REWRITE_LOG_LEVEL warn
```

Cuando se ejecuta Dispatcher localmente, los registros se imprimen directamente en la salida del terminal. La mayoría de las veces, desea que estos registros estén en DEPURACIÓN, lo que se puede hacer pasando el nivel de Depuración como parámetro al ejecutar Docker. Por ejemplo: `DISP_LOG_LEVEL=Debug ./bin/docker_run.sh src docker.for.mac.localhost:4503 8080`.

Los registros para entornos de nube se exponen a través del servicio de registro disponible en Cloud Manager.

>[!NOTE]
>
>Para los entornos de AEM as a Cloud Service, la depuración es el nivel de detalle máximo. El nivel de registro de seguimiento no es compatible, por lo que debe evitar configurarlo cuando trabaje en entornos de nube.

### Recarga y validación automáticas {#automatic-reloading}

>[!NOTE]
>
>Debido a una limitación del sistema operativo Windows, esta función solo está disponible para usuarios de macOS y Linux®.

En lugar de ejecutar la validación local (`validate.sh`) e iniciar el contenedor de docker (`docker_run.sh`) cada vez que se modifique la configuración, puede ejecutar el script `docker_run_hot_reload.sh`. La secuencia de comandos observa cualquier cambio en la configuración y la vuelve a cargar automáticamente y vuelve a ejecutar la validación. Con esta opción, puede ahorrar una cantidad de tiempo considerable durante la depuración.

Puede ejecutar el script mediante el siguiente comando: `./bin/docker_run_hot_reload.sh src/dispatcher host.docker.internal:4503 8080`

Las primeras líneas de salida tienen un aspecto similar al que se ejecutaría para `docker_run.sh`. Por ejemplo:

```
~ bin/docker_run_hot_reload.sh src host.docker.internal:8081 8082
opt-in USE_SOURCES_DIRECTLY marker file detected
Running script /docker_entrypoint.d/10-check-environment.sh
Running script /docker_entrypoint.d/15-check-pod-name.sh
Running script /docker_entrypoint.d/20-create-docroots.sh
Running script /docker_entrypoint.d/30-wait-for-backend.sh
Waiting until host.docker.internal is available
host.docker.internal resolves to 192.168.65.2
Running script /docker_entrypoint.d/40-generate-allowed-clients.sh
Running script /docker_entrypoint.d/50-check-expiration.sh
Running script /docker_entrypoint.d/60-check-loglevel.sh
Running script /docker_entrypoint.d/70-check-forwarded-host-secret.sh
Running script /docker_entrypoint.d/80-frontend-domain.sh
Running script /docker_entrypoint.d/zzz-import-sdk-config.sh
WARN Mon Jul  4 09:53:54 UTC 2022: Pseudo symlink conf.d seems to point to a non-existing file!
INFO Mon Jul  4 09:53:55 UTC 2022: Copied customer configuration to /etc/httpd.
INFO Mon Jul  4 09:53:55 UTC 2022: Start testing
Cloud manager validator 2.0.43
2022/07/04 09:53:55 No issues found
INFO Mon Jul  4 09:53:55 UTC 2022: Testing with fresh base configuration files.
INFO Mon Jul  4 09:53:55 UTC 2022: Apache httpd informationServer version: Apache/2.4.54 (Unix)
```

### Inserción de variables de entorno personalizadas {#environment-variables}

Las variables de entorno personalizadas se pueden usar con el SDK de Dispatcher configurándolas en un archivo independiente y haciendo referencia a ellas en la variable de entorno `ENV_FILE` antes de iniciar Dispatcher local.

Un archivo con variables de entorno personalizadas tendría este aspecto:

```
COMMERCE_ENDPOINT=commerce-host
AEM_HTTP_PROXY_HOST=host.docker.internal
AEM_HTTP_PROXY_PORT=8000
```

Y se puede utilizar en el SDK local de Dispatcher con los siguientes comandos:

```
export ENV_FILE=custom.env
./bin/docker_run.sh src/dispatcher docker.for.mac.localhost:4503 8080
```

## Diferentes configuraciones de Dispatcher por entorno {#different-dispatcher-configurations-per-environment}

Actualmente, la misma configuración de Dispatcher se aplica a todos los entornos de AEM as a Cloud Service. El motor en tiempo de ejecución tiene una variable de entorno `ENVIRONMENT_TYPE` que contiene el modo de ejecución actual (desarrollo, fase o producción) y un elemento &quot;define&quot;. La definición puede ser `ENVIRONMENT_DEV`, `ENVIRONMENT_STAGE` o `ENVIRONMENT_PROD`. En la configuración de Apache, la variable se puede utilizar directamente en una expresión. Alternativamente, se puede utilizar la opción &quot;definir&quot; para generar lógica:

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

En la configuración de Dispatcher, está disponible la misma variable de entorno. Si se requiere más lógica, defina las variables como se muestra en el ejemplo anterior y, a continuación, utilícelas en la sección Configuración de Dispatcher:

```
/virtualhosts {
  { "${VIRTUALHOST}" }
}
```

Como alternativa, puede utilizar variables de entorno de Cloud Manager en la configuración de httpd/Dispatcher, aunque no secretos de entorno. Este método es especialmente importante si un programa tiene varios entornos de desarrollo y algunos de esos entornos de desarrollo tienen valores diferentes para la configuración de httpd/dispatcher. Se usaría la misma sintaxis ${VIRTUALHOST} que en el ejemplo anterior, pero no se usarían las declaraciones Define del archivo de variables anterior. Lea la [documentación de Cloud Manager](/help/implementing/cloud-manager/environment-variables.md) para obtener instrucciones sobre cómo configurar variables de entorno de Cloud Manager.

Al probar la configuración localmente, puede simular distintos tipos de entorno pasando directamente la variable `DISP_RUN_MODE` al script `docker_run.sh`:

```
$ DISP_RUN_MODE=stage docker_run.sh src docker.for.mac.localhost:4503 8080
```

El modo de ejecución predeterminado cuando no se pasa un valor para DISP_RUN_MODE es &quot;dev&quot;.
Para obtener una lista completa de las opciones y variables disponibles, ejecute el script `docker_run.sh` sin argumentos.

## Visualización de la configuración de Dispatcher que utiliza su contenedor Docker {#viewing-dispatcher-configuration-in-use-by-docker-container}

Con las configuraciones específicas del entorno, puede resultar difícil determinar el aspecto real de la configuración de Dispatcher. Después de haber iniciado el contenedor de docker con `docker_run.sh`, se puede volcar de la siguiente manera:

* Determine el ID del contenedor de Docker en uso:

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

## Migración del modo heredado al modo flexible {#migrating}

Con la versión Cloud Manager 2021.7.0, los nuevos programas de Cloud Manager AEM generan estructuras de proyecto Maven con [tipo de archivo 28](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=es) o superior, que incluye el archivo **opt-in/USE_SOURCES_DIRECTLY**. Elimina las limitaciones anteriores del [modo heredado](/help/implementing/dispatcher/validation-debug-legacy.md) en cuanto al número y el tamaño de los archivos, lo que también provoca que el SDK y el tiempo de ejecución validen e implementen la configuración de forma mejorada. Si la configuración de Dispatcher no tiene este archivo, se recomienda migrar. Siga estos pasos para garantizar una transición segura:

1. **Pruebas locales.**: usando el SDK de herramientas de Dispatcher más reciente, agregue la carpeta y el archivo `opt-in/USE_SOURCES_DIRECTLY`. Siga las instrucciones de &quot;validación local&quot; de este artículo para poder probar que Dispatcher funciona localmente.
1. **Pruebas de desarrollo en la nube:**
   * Confirme el archivo `opt-in/USE_SOURCES_DIRECTLY` en una rama de Git implementada por la canalización que no sea de producción en un entorno de desarrollo de Cloud.
   * Utilice Cloud Manager para implementar en un entorno de desarrollo de Cloud.
   * Pruebe a fondo. Es fundamental validar que la configuración de Apache y Dispatcher se comporta como espera antes de implementar cambios en entornos más altos. Compruebe todo el comportamiento relacionado con la configuración personalizada. Presente un ticket de asistencia al cliente si cree que la configuración implementada de Dispatcher no refleja su configuración personalizada.

   >[!NOTE]
   >
   >En el modo flexible, debe utilizar rutas relativas en lugar de rutas absolutas.
1. **Implementar en producción:**
   * Confirme el archivo `opt-in/USE_SOURCES_DIRECTLY` en una rama de Git implementada por la canalización de producción en los entornos de ensayo y producción de la nube.
   * Utilice Cloud Manager para implementarlo en el ensayo.
   * Pruebe a fondo. Es fundamental validar que la configuración de Apache y Dispatcher se comporta como espera antes de implementar cambios en entornos más altos. Compruebe todo el comportamiento relacionado con la configuración personalizada. Presente un ticket de asistencia al cliente si cree que la configuración implementada de Dispatcher no refleja su configuración personalizada.
   * Utilice Cloud Manager para continuar con la implementación en producción.
