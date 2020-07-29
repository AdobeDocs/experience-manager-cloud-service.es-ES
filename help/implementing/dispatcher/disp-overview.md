---
title: Dispatcher en la nube
description: 'Dispatcher en la nube '
translation-type: tm+mt
source-git-commit: fe4202cafcab99d22e05728f58974e1a770a99ed
workflow-type: tm+mt
source-wordcount: '3824'
ht-degree: 9%

---


# Dispatcher en la nube {#Dispatcher-in-the-cloud}

## Apache and Dispatcher configuration and testing {#apache-and-dispatcher-configuration-and-testing}

En esta sección se describe cómo estructurar el AEM como una configuración de Dispatcher y Apache Cloud Service, así como cómo validarlo y ejecutarlo localmente antes de implementarlo en entornos de nube. También se describe la depuración en entornos de nube. Para obtener información adicional sobre Dispatcher, consulte la documentación [](https://docs.adobe.com/content/help/es-ES/experience-manager-dispatcher/using/dispatcher.html)AEM de Dispatcher.

>[!NOTE]
>
>Los usuarios de Windows necesitarán utilizar Windows 10 Professional u otras distribuciones que admitan Docker. Se trata de un requisito previo para ejecutar y depurar Dispatcher en un equipo local. Las secciones siguientes incluyen comandos que utilizan las versiones Mac o Linux del SDK, pero el SDK de Windows se puede utilizar de forma similar.

>[!WARNING]
>
>Usuarios de Windows: la versión actual de AEM como Cloud Service local de Dispatcher Tools (v2.0.20) no es compatible con Windows. Póngase en contacto con el servicio de asistencia técnica [de](https://daycare.day.com/home.html) Adobe para recibir actualizaciones sobre la compatibilidad con Windows.

## Herramientas de Dispatcher {#dispatcher-sdk}

Las herramientas de Dispatcher forman parte del AEM general como SDK de Cloud Service y proporcionan:

* Una estructura de archivos de vainilla que contiene los archivos de configuración que se incluirán en un proyecto determinado para el despachante;
* Agrupación para que los clientes validen localmente una configuración de despachante;
* Imagen de acoplamiento que muestra el despachante localmente.

## Descarga y extracción de las herramientas {#extracting-the-sdk}

Las herramientas de Dispatcher se pueden descargar desde un archivo zip en el portal de distribución [de](https://downloads.experiencecloud.adobe.com/content/software-distribution/en/aemcloud.html) software. Tenga en cuenta que el acceso a los listados de SDK está limitado a aquellos con AEM Managed Services o AEM como entornos de Cloud Service. Cualquier nueva configuración disponible en esa nueva versión de herramientas de distribuidor se puede utilizar para implementar en entornos de nube que ejecuten esa versión de AEM en la nube o posterior.

**Para macOS y Linux**, descargue la secuencia de comandos shell en una carpeta de su equipo, haga que sea ejecutable y ejecútela. Se extraerán los archivos de herramientas de Dispatcher debajo del directorio en el que se almacenó (donde `version` es la versión de las herramientas de distribución).

```bash
$ chmod +x DispatcherSDKv<version>.sh
$ ./DispatcherSDKv<version>.sh
Verifying archive integrity...  100%   All good.
Uncompressing DispatcherSDKv<version>  100% 
```

**Para Windows**, descargue el archivo zip y extráigalo.

## Estructura de archivos {#file-structure}

La estructura de la subcarpeta de despachantes del proyecto se describe a continuación y debe copiarse en la carpeta del despachante del proyecto principal:

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

Los siguientes archivos se pueden personalizar y se transferirán a su instancia de Cloud durante la implementación:

* `conf.d/available_vhosts/<CUSTOMER_CHOICE>.vhost`

Puede tener uno o más de estos archivos. Contienen `<VirtualHost>` entradas que coinciden con nombres de host y permiten a Apache manejar cada tráfico de dominio con reglas diferentes. Los archivos se crean en el `available_vhosts` directorio y se activan con un vínculo simbólico en el `enabled_vhosts` directorio. Desde los `.vhost` archivos, se incluirán otros archivos como reescrituras y variables.

* `conf.d/rewrites/rewrite.rules`

Este archivo se incluye dentro de `.vhost` los archivos. Tiene un conjunto de reglas de reescritura para `mod_rewrite`.

>[!NOTE]
>
>En este momento, se debe utilizar un solo archivo de reescritura en lugar de archivos específicos del sitio. Ese tamaño de archivo debe ser inferior a 1 MB.

* `conf.d/variables/custom.vars`

Este archivo se incluye dentro de `.vhost` los archivos. Puede colocar las definiciones para las variables Apache en esta ubicación.

* `conf.d/variables/global.vars`

Este archivo se incluye desde dentro del `dispatcher_vhost.conf` archivo. Puede cambiar el distribuidor y reescribir el nivel de registro en este archivo.

* `conf.dispatcher.d/available_farms/<CUSTOMER_CHOICE>.farm`

Puede tener uno o más de estos archivos, que contienen granjas que coincidan con los nombres de host y permiten que el módulo de despachante gestione cada granja con reglas diferentes. Los archivos se crean en el `available_farms` directorio y se activan con un vínculo simbólico en el `enabled_farms` directorio. Desde los `.farm` archivos, se incluirán otros archivos como filtros, reglas de caché y otros.

* `conf.dispatcher.d/cache/rules.any`

Este archivo se incluye dentro de `.farm` los archivos. Especifica las preferencias de almacenamiento en caché.

* `conf.dispatcher.d/clientheaders/clientheaders.any`

Este archivo se incluye dentro de `.farm` los archivos. Especifica qué encabezados de solicitud deben reenviarse al servidor.

* `conf.dispatcher.d/filters/filters.any`

Este archivo se incluye dentro de `.farm` los archivos. Tiene un conjunto de reglas que cambian el tráfico que debe filtrarse y no llegar al servidor.

* `conf.dispatcher.d/virtualhosts/virtualhosts.any`

Este archivo se incluye dentro de `.farm` los archivos. Tiene una lista de nombres de host o rutas de URI para que coincidan con la coincidencia de glob. Esto determina el servidor que se utilizará para proporcionar una solicitud.

Los archivos anteriores hacen referencia a los archivos de configuración inmutables que se enumeran a continuación. Los cambios en los archivos inmutables no serán procesados por los distribuidores en los entornos de la nube.

**Archivos de configuración inmutables**

Estos archivos forman parte del marco de base y hacen cumplir las normas y las prácticas recomendadas. Los archivos se consideran inmutables porque modificarlos o eliminarlos localmente no afectará a su implementación, ya que no se transferirán a su instancia de Cloud.

Se recomienda que los archivos anteriores hagan referencia a los archivos inmutables que se enumeran a continuación, seguidos de cualquier declaración o anulación adicional. Cuando se implementa la configuración del distribuidor en un entorno de nube, se utilizará la versión más reciente de los archivos inmutables, independientemente de la versión que se haya utilizado en el desarrollo local.

* `conf.d/available_vhosts/default.vhost`

Contiene un host virtual de muestra. Para su propio host virtual, cree una copia de este archivo, personalícelo, vaya a `conf.d/enabled_vhosts` y cree un vínculo simbólico a su copia personalizada.

* `conf.d/dispatcher_vhost.conf`

Parte de la estructura base, utilizada para ilustrar cómo se incluyen los hosts virtuales y las variables globales.

* `conf.d/rewrites/default_rewrite.rules`

Reglas de reescritura predeterminadas adecuadas para un proyecto estándar. Si necesita personalización, modifique `rewrite.rules`. En la personalización, puede incluir primero las reglas predeterminadas, si se adaptan a sus necesidades.

* `conf.dispatcher.d/available_farms/default.farm`

Contiene un conjunto de distribuidores de muestra. Para su propio conjunto de servidores, cree una copia de este archivo, personalícelo, vaya a `conf.d/enabled_farms` y cree un vínculo simbólico a su copia personalizada.

* `conf.dispatcher.d/cache/default_invalidate.any`

Parte del marco base, se genera al inicio. Es **necesario** incluir este archivo en cada conjunto de servidores que defina, en la `cache/allowedClients` sección .

* `conf.dispatcher.d/cache/default_rules.any`

Reglas de caché predeterminadas adecuadas para un proyecto estándar. Si necesita personalización, modifique `conf.dispatcher.d/cache/rules.any`. En la personalización, puede incluir primero las reglas predeterminadas, si se adaptan a sus necesidades.

* `conf.dispatcher.d/clientheaders/default_clientheaders.any`

Encabezados de solicitud predeterminados para reenviar al servidor, adecuados para un proyecto estándar. Si necesita personalización, modifique `clientheaders.any`. En la personalización, puede incluir primero los encabezados de solicitud predeterminados si se adaptan a sus necesidades.

* `conf.dispatcher.d/dispatcher.any`

Parte del marco base, utilizado para ilustrar cómo se incluyen las granjas de despachantes.

* `conf.dispatcher.d/filters/default_filters.any`

filtros predeterminados adecuados para un proyecto estándar. Si necesita personalización, modifique `filters.any`. En la personalización, puede incluir primero los filtros predeterminados si se adaptan a sus necesidades.

* `conf.dispatcher.d/renders/default_renders.any`

Este archivo, que forma parte del marco base, se genera al iniciar. Es **necesario** incluir este archivo en cada conjunto de servidores que defina, en la `renders` sección .

* `conf.dispatcher.d/virtualhosts/default_virtualhosts.any`

Globalización de host predeterminada adecuada para un proyecto estándar. Si necesita personalización, modifique `virtualhosts.any`. En la personalización, no debe incluir la globalización de host predeterminada, ya que coincide con **cada** solicitud entrante.

>[!NOTE]
>
>El AEM como arquetipo hecho por Cloud Service generará la misma estructura de archivos de configuración del despachante.

Las secciones a continuación describen cómo validar la configuración localmente para que pueda pasar la puerta de calidad asociada en Cloud Manager al implementar una versión interna.

## Validación local de la configuración de Dispatcher {#local-validation-of-dispatcher-configuration}

La herramienta de validación está disponible en el SDK `bin/validator` como un archivo binario de Mac OS, Linux o Windows, lo que permite a los clientes ejecutar la misma validación que Cloud Manager realizará durante la creación e implementación de una versión.

Se invoca como: `validator full [-d folder] [-w whitelist] zip-file | src folder`

La herramienta valida la configuración de Apache y dispatcher. Analiza todos los archivos con un patrón `conf.d/enabled_vhosts/*.vhost` y comprueba que solo se utilizan las directivas permitidas. Las directivas permitidas en los archivos de configuración de Apache se pueden enumerar ejecutando el comando de lista de permitidos del validador:

```
$ validator whitelist
Cloud manager validator 2.0.4
 
Whitelisted directives:
  <Directory>
  ...
  
```

La siguiente tabla muestra los módulos apache admitidos:

| Nombre del módulo | Página de referencia |
|---|---|
| `core` | [https://httpd.apache.org/docs/2.4/mod/core.html](https://httpd.apache.org/docs/2.4/mod/core.html) |
| `mod_access_compat` | [https://httpd.apache.org/docs/2.4/mod/mod_access_compat.html](https://httpd.apache.org/docs/2.4/mod/mod_access_compat.html) |
| `mod_alias` | [https://httpd.apache.org/docs/2.4/mod/mod_alias.html](https://httpd.apache.org/docs/2.4/mod/mod_alias.html) |
| `mod_allowmethods` | [https://httpd.apache.org/docs/2.4/mod/mod_allowmethods.html](https://httpd.apache.org/docs/2.4/mod/mod_allowmethods.html) |
| `mod_auth_basic` | [https://httpd.apache.org/docs/2.4/mod/mod_auth_basic.html](https://httpd.apache.org/docs/2.4/mod/mod_auth_basic.html) |
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
| `mod_remoteip` | [https://httpd.apache.org/docs/2.4/mod/mod_remoteip.html](https://httpd.apache.org/docs/2.4/mod/mod_remoteip.html) |
| `mod_reqtimeout` | [https://httpd.apache.org/docs/2.4/mod/mod_reqtimeout.html](https://httpd.apache.org/docs/2.4/mod/mod_reqtimeout.html) |
| `mod_rewrite` | [https://httpd.apache.org/docs/2.4/mod/mod_rewrite.html](https://httpd.apache.org/docs/2.4/mod/mod_rewrite.html) |
| `mod_security` | [https://modsecurity.org/](https://modsecurity.org/) |
| `mod_setenvif` | [https://httpd.apache.org/docs/2.4/mod/mod_setenvif.html](https://httpd.apache.org/docs/2.4/mod/mod_setenvif.html) |
| `mod_substitute` | [https://httpd.apache.org/docs/2.4/mod/mod_substitute.html](https://httpd.apache.org/docs/2.4/mod/mod_substitute.html) |
| `mod_userdir` | [https://httpd.apache.org/docs/2.4/mod/mod_userdir.html](https://httpd.apache.org/docs/2.4/mod/mod_userdir.html) |

Los clientes no pueden agregar módulos arbitrarios, sin embargo se puede considerar incluir módulos adicionales en el producto en el futuro. Los clientes pueden encontrar la lista de directivas disponibles para una versión de Dispatcher determinada ejecutando el comando de lista de permitidos del validador en el SDK, tal como se describe anteriormente.

La lista de permitidos contiene una lista de directivas Apache que se permiten en una configuración de cliente. Si no se permite una directiva, la herramienta registra un error y devuelve un código de salida distinto de cero. Si no se proporciona ninguna lista de permitidos en la línea de comandos (que es la forma de invocarla), la herramienta utiliza una lista de permitidos predeterminada que Cloud Manager utilizará para la validación antes de implementarla en entornos de nube.

Además, analiza todos los archivos con patrones `conf.dispatcher.d/enabled_farms/*.farm` y comprueba que:

* No existe ninguna regla de filtro que utilice las permisiones mediante `/glob` (consulte [CVE-2016-0957](https://nvd.nist.gov/vuln/detail/CVE-2016-0957) para obtener más información)
* No se expone ninguna función de administración. Por ejemplo, el acceso a rutas como `/crx/de or /system/console`.

Cuando se ejecuta con el artefacto original o con el `dispatcher/src` subdirectorio, se notificarán los errores de validación:

```
$ validator full dispatcher/src
Cloud manager validator 1.0.4
2019/06/19 15:41:37 Apache configuration uses non-whitelisted directives:
  conf.d/enabled_vhosts/aem_publish.vhost:46: LogLevel
2019/06/19 15:41:37 Dispatcher configuration validation failed:
  conf.dispatcher.d/enabled_farms/999_ams_publish_farm.any: filter allows access to CRXDE
```

Tenga en cuenta que la herramienta de validación informa solamente sobre el uso prohibido de directivas Apache que no se han permitido. No informa de problemas sintácticos o semánticos con la configuración de Apache, ya que esta información sólo está disponible para los módulos Apache en un entorno en ejecución.

Cuando no se notifican errores de validación, la configuración está lista para la implementación.

A continuación se presentan técnicas de solución de problemas para depurar errores de validación comunes que genera la herramienta:

**no se puede encontrar una`conf.dispatcher.d`subcarpeta en el archivo**

El archivo debe contener las carpetas `conf.d` y `conf.dispatcher.d`. Tenga en cuenta que **no debe** usar el prefijo `etc/httpd` en el archivo.

**no se pudo encontrar ninguna granja en`conf.dispatcher.d/enabled_farms`**

Las granjas habilitadas deben ubicarse en la subcarpeta mencionada.

**el archivo incluido (...) debe tener el nombre: ...**

Hay dos secciones en la configuración del conjunto de servidores que **deben** incluir un archivo específico: `/renders` y `/allowedClients` en la `/cache` sección. Estas secciones deben tener el siguiente aspecto:

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

Hay cuatro secciones en la configuración del conjunto de servidores donde puede incluir su propio archivo: `/clientheaders`, `filters`, `/rules` en `/cache` la sección y `/virtualhosts`. Los archivos incluidos deben nombrarse de la siguiente manera:

| Sección | Incluir nombre de archivo |
|------------------|--------------------------------------|
| `/clientheaders` | `../clientheaders/clientheaders.any` |
| `/filters` | `../filters/filters.any` |
| `/rules` | `../cache/rules.any` |
| `/virtualhosts` | `../virtualhosts/virtualhosts.any` |

También puede incluir la versión **predeterminada** de esos archivos, cuyos nombres van precedidos de la palabra `default_`, por ejemplo `../filters/default_filters.any`.

**incluir instrucción en (...), fuera de cualquier ubicación conocida: ...**

Aparte de las seis secciones mencionadas en los párrafos anteriores, no se le permite utilizar la `$include` instrucción, por ejemplo: lo siguiente generaría este error:

```
/invalidate {
    $include "../cache/invalidate.any"
}
```

**los clientes/procesamientos permitidos no se incluyen desde: ...**

Este error se genera cuando no se especifica una inclusión para `/renders` y `/allowedClients` en la `/cache` sección. Consulte el nombre del **archivo incluido (...): ...** para obtener más información.

**el filtro no debe utilizar el patrón de glob para permitir solicitudes**

No es seguro permitir solicitudes con una regla de `/glob` estilo, que se compara con la línea de solicitud completa, por ejemplo:

```
/0100 {
    /type "allow" /glob "GET *.css *"
}
```

Esta instrucción está pensada para permitir solicitudes de `css` archivos, pero también permite solicitudes a **cualquier** recurso seguido de la cadena de consulta `?a=.css`. Por lo tanto, está prohibido utilizar estos filtros (véase también CVE-2016-0957).

**el archivo incluido (...) no coincide con ningún archivo conocido**

Existen dos tipos de archivos en la configuración del host virtual Apache que se pueden especificar como incluye: reescribe y variables.
Los archivos incluidos deben nombrarse de la siguiente manera:

| Tipo | Incluir nombre de archivo |
|-----------|---------------------------------|
| Reescribe | `conf.d/rewrites/rewrite.rules` |
| Variables | `conf.d/variables/custom.vars` |

También puede incluir la versión **predeterminada** de las reglas de reescritura, cuyo nombre es `conf.d/rewrites/default_rewrite.rules`.
Tenga en cuenta que no hay una versión predeterminada de los archivos de variables.

**Se detectó un diseño de configuración obsoleto, habilitando el modo de compatibilidad**

Este mensaje indica que la configuración tiene el diseño de la versión 1 en desuso, que contiene una configuración completa de Apache y archivos con `ams_` prefijos. Aunque esto aún es compatible con la compatibilidad con versiones anteriores, debe cambiar al nuevo diseño.

## Prueba de la configuración de Apache y Dispatcher localmente {#testing-apache-and-dispatcher-configuration-locally}

También es posible probar la configuración local de Apache y Dispatcher. Requiere que el acoplador se instale localmente y que la configuración pase la validación como se describe anteriormente.

Al utilizar el parámetro &quot;`-d`&quot;, el validador genera una carpeta con todos los archivos de configuración que necesita el despachante.

A continuación, la `docker_run.sh` secuencia de comandos puede apuntar a esa carpeta, comenzando el contenedor con la configuración.

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

Esto inicio al despachante en un contenedor con su back-end que apunta a una instancia de AEM que se ejecuta en el equipo local de Mac OS en el puerto 4503.

## Depuración de la configuración de Apache y Dispatcher {#debugging-apache-and-dispatcher-configuration}

Los niveles de registro están definidos por las variables `DISP_LOG_LEVEL` y `REWRITE_LOG_LEVEL` en `conf.d/variables/global.var`s&quot;. See the [Logging documentation](/help/implementing/developing/introduction/logging.md#apache-web-server-and-dispatcher-logging) for more information.

## Diferentes configuraciones de Dispatcher por entorno {#different-dispatcher-configurations-per-environment}

En este momento, la misma configuración de despachante se aplica a todos los AEM como entornos de Cloud Service. El motor de ejecución tendrá una variable de entorno `ENVIRONMENT_TYPE` que contiene el modo de ejecución actual (dev, stage o prod), así como una definición. La definición puede ser `ENVIRONMENT_DEV`, `ENVIRONMENT_STAGE` o `ENVIRONMENT_PROD`. En la configuración de Apache, la variable puede utilizarse directamente en una expresión. También se puede usar la definición para generar lógica:

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

En la configuración de Dispatcher, está disponible la misma variable de entorno. Si se requiere más lógica, defina las variables como se muestra en el ejemplo anterior y úselas en la sección de configuración de Dispatcher:

```
/virtualhosts {
  { "${VIRTUALHOST}" }
}
```

Al probar la configuración localmente, puede simular diferentes tipos de entornos pasando la variable `DISP_RUN_MODE` a la secuencia de comandos `docker_run.sh` directamente:

```
$ DISP_RUN_MODE=stage docker_run.sh out docker.for.mac.localhost:4503 8080
```

El modo de ejecución predeterminado cuando no se pasa un valor para DISP_RUN_MODE es &quot;dev&quot;.
Para obtener una lista completa de las opciones y variables disponibles, ejecute la secuencia de comandos `docker_run.sh` sin argumentos.

## Visualización de la configuración de Dispatcher utilizada por el contenedor de Docker {#viewing-dispatcher-configuration-in-use-by-docker-container}

Con configuraciones específicas de entorno, puede resultar difícil determinar el aspecto de la configuración real de Dispatcher. Después de haber iniciado el contenedor del docker con `docker_run.sh` él, puede verterse de la siguiente manera:

* Determinar la ID del contenedor del docker en uso:

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

Como se describe en la página de referencia anterior, la configuración de Apache y Dispatcher en AEM como Cloud Service es muy similar a la de AMS. Las principales diferencias son:

* En AEM como Cloud Service, es posible que algunas directivas Apache no se utilicen (por ejemplo `Listen` o `LogLevel`)
* En AEM como Cloud Service, sólo se pueden incluir algunos fragmentos de la configuración de Dispatcher en los archivos de inclusión y su nombre es importante. Por ejemplo, las reglas de filtro que desee reutilizar en diferentes hosts deben colocarse en un archivo llamado `filters/filters.any`. Consulte la página de referencia para obtener más información.
* En AEM como Cloud Service hay una validación adicional para no permitir reglas de filtro escritas `/glob` para evitar problemas de seguridad. Dado que `deny *` se usará en lugar de `allow *` (que no se puede usar), los clientes se beneficiarán de ejecutar el Dispatcher localmente y de realizar pruebas y errores, mirando los registros para saber exactamente qué rutas bloquean los filtros de Dispatcher para que se puedan agregar.

## Pautas para migrar la configuración del despachante de AMS a AEM como Cloud Service

La estructura de configuración del despachante tiene diferencias entre Managed Services y AEM como Cloud Service. A continuación se presenta una guía paso a paso sobre cómo migrar de la versión 2 de la configuración de AMS Dispatcher a AEM como Cloud Service.

## Cómo convertir un AMS en una configuración de AEM como distribuidor de servicios en la nube

En la siguiente sección se proporcionan instrucciones paso a paso sobre cómo convertir una configuración de AMS. It assumes
that you have an archive with a structure similar to the one described in [Cloud Manager dispatcher configuration](https://docs.adobe.com/content/help/es-ES/experience-manager-cloud-manager/using/getting-started/dispatcher-configurations.html)

### Extraer el archivo y eliminar un prefijo eventual

Extraiga el archivo en una carpeta y asegúrese de que las subcarpetas inmediatas inicio con `conf`, `conf.d``conf.dispatcher.d` y `conf.modules.d`. Si no lo hacen, muévalos arriba en la jerarquía.

### Elimine las subcarpetas y archivos que no utilice

Remove subfolders `conf` and `conf.modules.d`, as well as files matching `conf.d/*.conf`.

### Elimine todos los hosts virtuales que no sean de publicación

Elimine cualquier archivo host virtual en `conf.d/enabled_vhosts` que tenga `author`, `unhealthy`, `health``lc` o `flush` su nombre. All virtual host files in `conf.d/available_vhosts` that are not
linked to can be removed as well.

### Quitar o comentar secciones de host virtual que no hagan referencia al puerto 80

Si aún hay secciones en los archivos host virtuales que se refieran exclusivamente a otros puertos que no sean el puerto 80, p. ej.

```
<VirtualHost *:443>
...
</VirtualHost>
```


elimínelos o haga comentarios. Las frases de estas secciones no se procesan, pero si se conservan, se pueden editar sin efecto, lo que es confuso.

### Verificar reescrituras

Enter directory `conf.d/rewrites`.

Remove any file named `base_rewrite.rules` and `xforwarded_forcessl_rewrite.rules` and remember to
remove `Include` statements in the virtual host files referring to them.

If `conf.d/rewrites` now contains a single file, it should be renamed to `rewrite.rules` and don&#39;t
forget to adapt the `Include` statements referring to that file in the virtual host files as well.

If the folder however contains multiple, virtual host specific files, their contents should be
copied to the `Include` statement referring to them in the virtual host files.

### Comprobar variables

Enter directory `conf.d/variables`.

Remove any file named `ams_default.vars` and remember to remove `Include` statements in the virtual
host files referring to them.

If `conf.d/variables` now contains a single file, it should be renamed to `custom.vars` and don&#39;t
forget to adapt the `Include` statements referring to that file in the virtual host files as well.

If the folder however contains multiple, virtual host specific files, their contents should be
copied to the `Include` statement referring to them in the virtual host files.

### Eliminar listas de permitidos

Remove the folder `conf.d/whitelists` and remove `Include` statements in the virtual host files referring to
some file in that subfolder.

### Reemplace cualquier variable que ya no esté disponible

En todos los archivos host virtuales:

Cambiar el nombre `PUBLISH_DOCROOT` a `DOCROOT`Eliminar secciones que hacen referencia a variables denominadas `DISP_ID`, `PUBLISH_FORCE_SSL` o `PUBLISH_WHITELIST_ENABLED`

### Comprueba el estado ejecutando el validador

Run the dispatcher validator in your directory, with the `httpd` subcommand:

```
$ validator httpd .
```

Si se observan errores en cuanto a la falta de archivos include, comprueba si se ha cambiado correctamente el nombre de esos archivos.

Si ve directivas de Apache que no están permitidas, elimínelas.

### Elimine todas las granjas que no sean para publicar

Remove any farm file in `conf.dispatcher.d/enabled_farms` that has `author`, `unhealthy`, `health`,
`lc` or `flush` in its name. All farm files in `conf.dispatcher.d/available_farms` that are not
linked to can be removed as well.

### Cambiar el nombre de los archivos

All farms in `conf.d/enabled_farms` must be renamed to match the pattern `*.farm`, so e.g. a
farm file called `customerX_farm.any` should be renamed `customerX.farm`.

### Compruebe la caché

Enter directory `conf.dispatcher.d/cache`.

Elimine cualquier archivo con el prefijo `ams_`.

If `conf.dispatcher.d/cache` is now empty, copy the file `conf.dispatcher.d/cache/rules.any`
from the standard dispatcher configuration to this folder. The standard dispatcher
configuration can be found in the folder `src` of this SDK. Don&#39;t forget to adapt the
`$include` statements referring to the `ams_*_cache.any` rule files  in the farm files
as well.

If instead `conf.dispatcher.d/cache` now contains a single file with suffix `_cache.any`,
it should be renamed to `rules.any` and don&#39;t forget to adapt the `$include` statements
referring to that file in the farm files as well.

If the folder however contains multiple, farm specific files with that pattern, their contents
should be copied to the `$include` statement referring to them in the farm files.

Remove any file that has the suffix `_invalidate_allowed.any`.

Copie el archivo `conf.dispatcher.d/cache/default_invalidate_any` desde el AEM predeterminado en la configuración del despachante de nube a esa ubicación.

In each farm file, remove any contents in the `cache/allowedClients` section and replace it
with:

```
$include "../cache/default_invalidate.any"
```

### Compruebe los encabezados de cliente

Enter directory `conf.dispatcher.d/clientheaders`.

Elimine cualquier archivo con el prefijo `ams_`.

If `conf.dispatcher.d/clientheaders` now contains a single file with suffix `_clientheaders.any`,
it should be renamed to `clientheaders.any` and don&#39;t forget to adapt the `$include` statements
referring to that file in the farm files as well.

If the folder however contains multiple, farm specific files with that pattern, their contents
should be copied to the `$include` statement referring to them in the farm files.

Copie el archivo `conf.dispatcher/clientheaders/default_clientheaders.any` desde la configuración predeterminada de AEM como distribuidor de Cloud Service a esa ubicación.

En cada archivo de granja, reemplace cualquier clientheader que incluya instrucciones que tengan el siguiente aspecto:

```
$include "/etc/httpd/conf.dispatcher.d/clientheaders/ams_publish_clientheaders.any"
$include "/etc/httpd/conf.dispatcher.d/clientheaders/ams_common_clientheaders.any"
```

con la frase:

```
$include "../clientheaders/default_clientheaders.any"
```

### Comprueba el filtro

Enter directory `conf.dispatcher.d/filters`.

Elimine cualquier archivo con el prefijo `ams_`.

If `conf.dispatcher.d/filters` now contains a single file it should be renamed to
`filters.any` and don&#39;t forget to adapt the `$include` statements referring to that
file in the farm files as well.

If the folder however contains multiple, farm specific files with that pattern, their contents
should be copied to the `$include` statement referring to them in the farm files.

Copie el archivo `conf.dispatcher/filters/default_filters.any` desde la configuración predeterminada de AEM como distribuidor de Cloud Service a esa ubicación.

En cada archivo de granja, reemplace cualquier filtro que incluya instrucciones que tengan el siguiente aspecto:

```
$include "/etc/httpd/conf.dispatcher.d/filters/ams_publish_filters.any"
```

con la frase:

```
$include "../filters/default_filters.any"
```

### Compruebe las representaciones

Enter directory `conf.dispatcher.d/renders`.

Elimina todos los archivos de esa carpeta.

Copie el archivo `conf.dispatcher.d/renders/default_renders.any` desde la configuración predeterminada de AEM como distribuidor de Cloud Service a esa ubicación.

In each farm file, remove any contents in the `renders` section and replace it
with:

```
$include "../renders/default_renders.any"
```

### Comprueba los hosts virtuales

Rename the directory `conf.dispatcher.d/vhosts` to `conf.dispatcher.d/virtualhosts` and enter it.

Elimine cualquier archivo con el prefijo `ams_`.

If `conf.dispatcher.d/virtualhosts` now contains a single file it should be renamed to
`virtualhosts.any` and don&#39;t forget to adapt the `$include` statements referring to that
file in the farm files as well.

If the folder however contains multiple, farm specific files with that pattern, their contents
should be copied to the `$include` statement referring to them in the farm files.

Copie el archivo `conf.dispatcher/virtualhosts/default_virtualhosts.any` desde la configuración predeterminada de AEM como distribuidor de Cloud Service a esa ubicación.

En cada archivo de granja, reemplace cualquier filtro que incluya instrucciones que tengan el siguiente aspecto:

```
$include "/etc/httpd/conf.dispatcher.d/vhosts/ams_publish_vhosts.any"
```

con la frase:

```
$include "../virtualhosts/default_virtualhosts.any"
```

### Comprueba el estado ejecutando el validador

Ejecute el AEM como un validador de despachantes de Cloud Service en el directorio, con el `dispatcher` subcomando:

```
$ validator dispatcher .
```

Si se observan errores en cuanto a la falta de archivos include, comprueba si se ha cambiado correctamente el nombre de esos archivos.

Si hay errores relacionados con la variable no definida `PUBLISH_DOCROOT`, renómbrala a `DOCROOT`.

Para consulta por cualquier otro error, consulte la sección Resolución de problemas de la documentación de la herramienta de validación.

### Pruebe la configuración con una implementación local (requiere la instalación de Docker)

Using the script `docker_run.sh` in the AEM as a Cloud Service Dispatcher Tools, you can test that
your configuration does not contain any other error that would only show up in
deployment:

### Paso 1: Generar información de implementación con el validador

```
validator full -d out .
```

This validates the full configuration and generates deployment information in `out`

### Paso 2: Inicio del despachante en una imagen de acoplador con esa información de implementación

Con el servidor de publicación de AEM en ejecución en el equipo MacOS, al escuchar el puerto 4503, se puede ejecutar el inicio de Dispatcher delante de ese servidor de la siguiente manera:

```
$ docker_run.sh out docker.for.mac.localhost:4503 8080
```

Esto inicia el contenedor y expone a Apache en el puerto local 8080.

### Usar la nueva configuración del despachante

¡Felicitaciones! If the validator no longer reports any issue and the
docker container starts up without any failures or warnings, you&#39;re
ready to move your configuration to a `dispatcher/src` subdirectory
of your git repository.

**Los clientes que utilicen la versión 1 de configuración de AMS Dispatcher deben ponerse en contacto con el servicio de asistencia al cliente para ayudarles a migrar de la versión 1 a la versión 2, de modo que se puedan seguir las instrucciones anteriores.**
