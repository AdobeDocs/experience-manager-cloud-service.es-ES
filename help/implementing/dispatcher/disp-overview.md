---
title: Dispatcher en la nube
description: Dispatcher en la nube
feature: Dispatcher
exl-id: 6d78026b-687e-434e-b59d-9d101349a707
source-git-commit: 98eff568686c72c626d2bf77d82e8c3f224eda42
workflow-type: tm+mt
source-wordcount: '983'
ht-degree: 74%

---

# Dispatcher en la nube {#Dispatcher-in-the-cloud}

>[!CONTEXTUALHELP]
>id="aemcloud_nonbpa_dispoverview"
>title="Dispatcher en la nube"
>abstract="En esta página se describe cómo descargar y extraer las herramientas de Dispatcher, los módulos Apache compatibles, y se proporciona una información general de alto nivel de los modos heredados y flexibles."

## Introducción {#apache-and-dispatcher-configuration-and-testing}

Esta página describe las herramientas de Dispatcher y cómo descargarlas y extraerlas, los módulos Apache admitidos, y proporciona una amplia descripción general de los modos heredados y flexibles. AEM Además, hay más referencias sobre validación y depuración, y sobre la migración de la configuración de Dispatcher de AMS a la as a Cloud Service de la. <!-- ERROR: NOT FOUND (HTTP ERROR 404) Also, see [this video](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-5/cloud5-aem-dispatcher-cloud.html) for additional details about deploying dispatcher files in a cloud service environment. -->

## Herramientas de Dispatcher {#dispatcher-sdk}

Las herramientas de Dispatcher forman parte del SDK de AEM as a Cloud Service y proporcionan lo siguiente:

* Una estructura de archivos estándar que contiene los archivos de configuración que se van a incluir en un proyecto Maven para Dispatcher.
* AEM Herramientas para que los clientes validen que la configuración de Dispatcher solo incluye directivas compatibles con el as a Cloud Service de la. Además, la herramienta también valida que la sintaxis es correcta para que Apache pueda iniciarse correctamente.
* Una imagen de Docker que muestra Dispatcher localmente.

## Descarga y extracción de las herramientas {#extracting-the-sdk}

Las herramientas de Dispatcher, que forman parte del [SDK de AEM as a Cloud Service](/help/implementing/developing/introduction/aem-as-a-cloud-service-sdk.md), se pueden descargar desde un archivo .zip en el portal de [distribución de software](https://downloads.experiencecloud.adobe.com/content/software-distribution/en/aemcloud.html). Cualquier configuración disponible en esa nueva versión de las herramientas de Dispatcher se puede usar para implementar en entornos de nube que ejecuten esa versión de AEM en la nube o posterior.

Descomprima el SDK, que agrupa las herramientas de Dispatcher para macOS® Linux y Windows.

**Para macOS/Linux**, haga que el artefacto de la herramienta Dispatcher sea ejecutable y ejecútelo. Extrae automáticamente los archivos de herramientas de Dispatcher debajo del directorio en el que lo almacenó (donde `version` es la versión de las herramientas de Dispatcher).

```bash
$ chmod +x aem-sdk-dispatcher-tools-<version>-unix.sh
$ ./aem-sdk-dispatcher-tools-<version>-unix.sh
Verifying archive integrity...  100%   All good.
Uncompressing aem-sdk-dispatcher-tools-<version>-unix.sh 100%
```

**Para Windows**, extraiga el archivo .zip de la herramienta Dispatcher.

## Validación y depuración con las herramientas de Dispatcher {#validation-debug}

Las herramientas de Dispatcher se utilizan para validar y depurar la configuración de Dispatcher del proyecto. Obtenga más información acerca de cómo utilizar esas herramientas en las páginas a las que se hace referencia a continuación, en función de si la configuración de Dispatcher del proyecto está estructurada en modo flexible o en modo heredado:

* **Modo flexible**: el modo recomendado y el valor predeterminado de [AEM arquetipo 28](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=es) y superior, que también utiliza Cloud Manager para los nuevos entornos creados después de la versión 2021.7.0 de Cloud Manager. Los clientes pueden activar este modo añadiendo la carpeta y el archivo `opt-in/USE_SOURCES_DIRECTLY`. Al utilizar este modo más flexible, no hay limitaciones en la estructura de archivos de la carpeta de reescrituras que en el modo heredado requieren un único archivo `rewrite.rules`. Además, no hay limitación en el número de reglas que se pueden agregar. Para obtener más información sobre la estructura de carpetas y la validación local, consulte [Validación y depuración mediante las herramientas de Dispatcher](/help/implementing/dispatcher/validation-debug.md).

* **Modo heredado** : para obtener más información sobre la estructura de carpetas y la validación local del modo heredado de configuración de Dispatcher, consulte [Validación y depuración mediante herramientas de Dispatcher (heredadas)](/help/implementing/dispatcher/validation-debug-legacy.md)

Para obtener más información sobre cómo migrar del modelo de configuración heredado al más flexible, proporcionado con el arquetipo 28 en adelante de AEM, consulte [esta documentación](/help/implementing/dispatcher/validation-debug.md#migrating).

## Disposición de contenido {#content-disposition}

Para el nivel de publicación, el valor predeterminado para los blobs de servicio es como archivo adjunto. Anule esta configuración con el estándar [encabezado de disposición de contenido](https://developer.mozilla.org/es-ES/docs/Web/HTTP/Headers/Content-Disposition) en Dispatcher.

A continuación, se muestra un ejemplo de cómo debería ser la configuración:

```
<LocationMatch "^\/content\/dam.*\.(pdf).*">
 Header unset Content-Disposition
 Header set Content-Disposition inline
</LocationMatch>
```

## Módulos Apache compatibles {#supported-directives}

La siguiente tabla muestra los módulos Apache compatibles:

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
| `mod_macro` | [https://httpd.apache.org/docs/2.4/mod/mod_macro.html](https://httpd.apache.org/docs/2.4/mod/mod_macro.html) |
| `mod_include (no directives supported)` | [https://httpd.apache.org/docs/2.4/mod/mod_include.html](https://httpd.apache.org/docs/2.4/mod/mod_include.html) |


Los clientes no pueden añadir módulos arbitrarios; sin embargo, se puede considerar la inclusión de módulos adicionales en el futuro. Los clientes pueden encontrar la lista de directivas disponibles para una versión de Dispatcher determinada ejecutando el comando de la lista de permitidos del validador en el SDK.

Las directivas permitidas en los archivos de configuración de Apache se pueden enumerar ejecutando el comando de la lista de permitidos del validador:

```
$ validator allowlist
Cloud manager validator 2.0.4
 
Allowlisted directives:
  <Directory>
  ...
  
```

## Estructura de carpetas {#folder-structure}

La estructura de carpetas de Apache y Dispatcher del proyecto difiere ligeramente en función del modo que utilice el proyecto, tal como se describe en la sección [Validación y depuración mediante las herramientas de Dispatcher](#validation-debug) sección anterior.

## Migración de la configuración de Dispatcher desde AMS {#ams-aem}

Para obtener más información sobre cómo migrar la configuración de Dispatcher de AMS a AEM as a Cloud Service, consulte la página [Migración de la configuración de Dispatcher de AMS a AEM](/help/implementing/dispatcher/ams-aem.md) as a Cloud Service.
