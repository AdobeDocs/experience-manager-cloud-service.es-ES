---
title: Validación y depuración mediante las herramientas de Dispatcher
description: Validación y depuración mediante las herramientas de Dispatcher
feature: Dispatcher
source-git-commit: 5545f7c271137050d522904bfa94e20f0286e059
workflow-type: tm+mt
source-wordcount: '2414'
ht-degree: 1%

---

# Validación y depuración mediante las herramientas de Dispatcher {#Dispatcher-in-the-cloud}

## Introducción {#apache-and-dispatcher-configuration-and-testing}

>[!NOTE]
>Para obtener más información sobre Dispatcher en la nube y cómo descargar las herramientas de Dispatcher, consulte la página [Dispatcher en la nube](/help/implementing/dispatcher/disp-overview.md). Si la configuración de Dispatcher está en modo heredado, consulte la [documentación del modo heredado](/help/implementing/dispatcher/validation-debug-legacy.md).

Las siguientes secciones describen la estructura de archivos en modo flexible, la validación local, la depuración y la migración del modo heredado al modo flexible.

En este artículo se supone que la configuración de Dispatcher del proyecto incluye el archivo `opt-in/USE_SOURCES_DIRECTLY`, lo que hace que el SDK y el tiempo de ejecución validen e implementen la configuración de una manera mejorada en comparación con el modo heredado, eliminando las limitaciones en cuanto al número y el tamaño de los archivos.

Como tal, si la configuración de Dispatcher no incluye el archivo mencionado anteriormente, es **altamente recomendable** que migre del modo heredado al modo flexible como se describe en la sección [Migración del modo heredado al modo flexible](#migrating) .

## Estructura del archivo {#flexible-mode-file-structure}

La estructura de la subcarpeta Dispatcher del proyecto es la siguiente:

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
│── opt-in
│   └── USE_SOURCES_DIRECTLY
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
    │   ├── default_virtualhosts.any
    │   └── virtualhosts.any
    
```

A continuación se muestra una explicación de los archivos importantes que se pueden modificar:

**Archivos personalizables**

Los siguientes archivos se pueden personalizar y se transferirán a la instancia de Cloud en la implementación:

* `conf.d/available_vhosts/<CUSTOMER_CHOICE>.vhost`

Puede tener uno o más de estos archivos. Contienen entradas `<VirtualHost>` que coinciden con los nombres de host y permiten que Apache gestione cada tráfico de dominio con reglas diferentes. Los archivos se crean en el directorio `available_vhosts` y se habilitan con un vínculo simbólico en el directorio `enabled_vhosts`. Desde los archivos `.vhost`, se incluirán otros archivos como reescrituras y variables.

* `conf.d/rewrites/rewrite.rules`

Este archivo se incluye desde dentro de sus `.vhost` archivos. Tiene un conjunto de reglas de reescritura para `mod_rewrite`.

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

* `opt-in/USE_SOURCES_DIRECTLY`

Este archivo permite una configuración de Dispatcher más flexible y elimina las limitaciones anteriores en cuanto al número y el tamaño de los archivos. También hace que el SDK y el tiempo de ejecución validen e implementen la configuración de una forma mejorada.

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

## Módulos Apache compatibles {#apache-modules}

Consulte [Módulos Apache compatibles](/help/implementing/dispatcher/disp-overview.md#supported-directives).

## Validación local {#local-validation-flexible-mode}

>[!NOTE]
>Las secciones siguientes incluyen comandos que utilizan las versiones Mac o Linux del SDK, pero el SDK de Windows también se puede utilizar de forma similar.

Utilice el script `validate.sh` como se muestra a continuación:

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

1. Ejecuta el validador. Si la configuración no es válida, la secuencia de comandos falla.
2. Ejecuta el comando `httpd -t` para comprobar si la sintaxis es correcta, de modo que apache httpd pueda iniciarse. Si la configuración se realiza correctamente, debe estar lista para la implementación.
3. Comprueba que el subconjunto de los archivos de configuración del SDK de Dispatcher, que están pensados para ser inmutables como se describe en la sección [Estructura del archivo](##flexible-mode-file-structure), no se haya modificado.

Durante una implementación de Cloud Manager, la comprobación de sintaxis `httpd -t` también se ejecutará y todos los errores se incluirán en el registro de Cloud Manager `Build Images step failure`.

### Fase 1 {#first-phase}

Si una directiva no está incluida en la lista de permitidos, la herramienta registra un error y devuelve un código de salida distinto de cero. Además, analiza todos los archivos con el patrón `conf.dispatcher.d/enabled_farms/*.farm` y comprueba que:

* No existe ninguna regla de filtro que utilice permite mediante `/glob` (consulte [CVE-2016-0957](https://nvd.nist.gov/vuln/detail/CVE-2016-0957) para obtener más información.
* No se ha expuesto ninguna función de administrador. Por ejemplo, acceso a rutas como `/crx/de or /system/console`.

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

Tenga en cuenta que la primera fase también puede ser **ejecutar por separado**, en lugar de hacerlo desde el script `validate.sh` envolvente.

Cuando se ejecuta con el artefacto maven o su subdirectorio `dispatcher/src`, informará de los errores de validación:

```
$ validator full -relaxed dispatcher/src
Cloud manager validator 1.0.4
2019/06/19 15:41:37 Apache configuration uses non-allowlisted directives:
  conf.d/enabled_vhosts/aem_publish.vhost:46: LogLevel
2019/06/19 15:41:37 Dispatcher configuration validation failed:
  conf.dispatcher.d/enabled_farms/999_ams_publish_farm.any: filter allows access to CRXDE
```

En Windows, el validador de Dispatcher distingue entre mayúsculas y minúsculas. Como tal, puede no validar la configuración si no respeta el uso de mayúsculas en la ruta en la que reside la configuración, por ejemplo:

```
bin\validator.exe -relaxed full src
Cloud manager validator 2.0.xx
2021/03/15 18:15:40 Dispatcher configuration validation failed:
  conf.dispatcher.d\available_farms\default.farm:15: parent directory outside server root: c:\k\a\aem-dispatcher-sdk-windows-symlinks-testing3\dispatcher\src
  
```

Evite este error copiando y pegando la ruta desde el Explorador de Windows y luego en el símbolo del sistema utilizando un comando `cd` en esa ruta.

### Fase 2 {#second-phase}

Esta fase comprueba la sintaxis de Apache iniciando Docker en una imagen. El acoplador debe instalarse localmente, pero tenga en cuenta que no es necesario que AEM se ejecute.

>[!NOTE]
>Los usuarios de Windows deben utilizar Windows 10 Professional u otras distribuciones compatibles con Docker. Este es un requisito previo para ejecutar y depurar Dispatcher en un equipo local.

Esta fase también se puede ejecutar de forma independiente a través de `bin/docker_run.sh src/dispatcher host.internal.docker:4503 8080`.

Durante una implementación de Cloud Manager, la comprobación de sintaxis `httpd -t` también se ejecutará y todos los errores se incluirán en el registro de errores del paso Generar imágenes de Cloud Manager.

### Fase 3 {#third-phase}

Si hay un error en esta fase, implica que el Adobe ha cambiado uno o más archivos inmutables y debe reemplazar los archivos inmutables correspondientes con la nueva versión entregada en el directorio `src` del SDK. El ejemplo de registro siguiente ilustra este problema:

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

Esta fase también se puede ejecutar de forma independiente a través de `bin/docker_immutability_check.sh src/dispatcher`.

## Depuración de la configuración de Apache y Dispatcher {#debugging-apache-and-dispatcher-configuration}

Tenga en cuenta que puede ejecutar apache Dispatcher localmente mediante `./bin/docker_run.sh src/dispatcher docker.for.mac.localhost:4503 8080`.

Como se ha indicado anteriormente, Docker debe instalarse localmente y no es necesario que AEM se ejecute. Los usuarios de Windows deben utilizar Windows 10 Professional u otras distribuciones compatibles con Docker. Este es un requisito previo para ejecutar y depurar Dispatcher en un equipo local.

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

## Visualización de la configuración de Dispatcher en uso por su contenedor Docker {#viewing-dispatcher-configuration-in-use-by-docker-container}

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

## Migración del modo heredado al modo flexible {#migrating}

Con la versión Cloud Manager 2021.7.0, los nuevos programas de Cloud Manager generan estructuras de proyecto maven con [AEM tipo de archivo 28](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=en) o superior, que incluye el archivo **opt-in/USE_SOURCES_DIRECTLY**. Esto elimina las limitaciones anteriores del [modo heredado](/help/implementing/dispatcher/validation-debug-legacy.md) en cuanto al número y el tamaño de los archivos, lo que también provoca que el SDK y el motor de ejecución validen e implementen la configuración de una forma mejorada. Si la configuración de Dispatcher no tiene este archivo, se recomienda migrar. Siga estos pasos para garantizar una transición segura:

1. **Pruebas locales.** Con el SDK de las herramientas de Dispatcher más recientes, añada la carpeta y el archivo  `opt-in/USE_SOURCES_DIRECTLY`. Siga las instrucciones de &quot;validación local&quot; de este artículo para probar que Dispatcher funciona localmente.
2. **Pruebas de desarrollo en la nube:**
   * Transfiera el archivo `opt-in/USE_SOURCES_DIRECTLY` a una rama de Git implementada por la canalización que no es de producción a un entorno de desarrollo de Cloud.
   * Utilice Cloud Manager para implementar en un entorno de desarrollo de Cloud.
   * Haga pruebas exhaustivas. Es fundamental validar que la configuración de Apache y Dispatcher se comporta como espera antes de implementar los cambios en entornos más altos. Compruebe todo el comportamiento relacionado con la configuración personalizada. Presente un ticket de asistencia al cliente si cree que la configuración implementada de Dispatcher no refleja su configuración personalizada.
3. **Implementar en producción:**
   * Convierta el archivo `opt-in/USE_SOURCES_DIRECTLY` en una rama de Git implementada por la canalización de producción en los entornos de producción y etapa de Cloud.
   * Utilice Cloud Manager para implementar en el entorno de ensayo.
   * Haga pruebas exhaustivas. Es fundamental validar que la configuración de Apache y Dispatcher se comporta como espera antes de implementar los cambios en entornos más altos. Compruebe todo el comportamiento relacionado con la configuración personalizada. Presente un ticket de asistencia al cliente si cree que la configuración implementada de Dispatcher no refleja su configuración personalizada.
   * Utilice Cloud Manager para continuar con la implementación en producción.
