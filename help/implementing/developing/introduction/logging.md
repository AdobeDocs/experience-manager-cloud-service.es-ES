---
title: Registro para AEM as a Cloud Service
description: Obtenga información sobre cómo utilizar el registro para AEM as a Cloud Service con el fin de configurar parámetros globales para el servicio de registro central, ajustes específicos para los servicios individuales o cómo solicitar el registro de datos.
exl-id: 262939cc-05a5-41c9-86ef-68718d2cd6a9
feature: Log Files, Developing
role: Admin, Architect, Developer
source-git-commit: 60bf6c6077ecfc6700ed9284834cf13e3772e25a
workflow-type: tm+mt
source-wordcount: '2364'
ht-degree: 9%

---

# Registro para AEM as a Cloud Service {#logging-for-aem-as-a-cloud-service}

AEM as a Cloud Service es una plataforma para que los clientes incluyan código personalizado para crear experiencias únicas para su base de clientes. Teniendo esto en cuenta, el servicio de registro es una función esencial para depurar y comprender la ejecución de código en el desarrollo local y en los entornos de nube, especialmente en los entornos de desarrollo de AEM as a Cloud Service.

La configuración de registro y los niveles de registro de AEM as a Cloud Service se administran en archivos de configuración almacenados como parte del proyecto de AEM en Git e implementados como parte del proyecto de AEM a través de Cloud Manager. El inicio de sesión en AEM as a Cloud Service se puede dividir en tres conjuntos lógicos:

* Registro de AEM, que realiza el registro en el nivel de aplicación de AEM
* Registro de Apache HTTPD Web Server/Dispatcher, que realiza el registro del servidor web y Dispatcher en el nivel de publicación.
* El registro de CDN, que como su nombre indica, realiza el registro en CDN.

## Registro de AEM {#aem-logging}

El registro en el nivel de aplicación de AEM se administra mediante tres registros:

1. Registros de Java de AEM, que representan instrucciones de registro de Java para la aplicación de AEM.
1. Registros de solicitudes HTTP, que registran información sobre solicitudes HTTP y sus respuestas proporcionadas por AEM
1. Registros de acceso HTTP, que registran información resumida y solicitudes HTTP proporcionadas por AEM

>[!NOTE]
>
>Las solicitudes HTTP servidas desde la caché de Dispatcher del nivel de publicación o la CDN de flujo ascendente no se reflejan en estos registros.

## Registro de Java en AEM {#aem-java-logging}

El de AEM as a Cloud Service proporciona acceso a las sentencias de registro de Java. Los desarrolladores de aplicaciones para AEM deben seguir las prácticas recomendadas generales de registro de Java, registrando las instrucciones pertinentes sobre la ejecución del código personalizado, en los siguientes niveles de registro:

<table>
<tr>
<td>
<b>Entorno AEM</b></td>
<td>
<b>Nivel de registro</b></td>
<td>
<b>Descripción</b></td>
<td>
<b>Disponibilidad del extracto de registro</b></td>
</tr>
<tr>
<td>
Desarrollo</td>
<td>
DEPURAR</td>
<td>
Describe lo que sucede en la aplicación.<br>
Cuando el registro de DEBUG está activo, se registran las instrucciones que proporcionan una imagen clara de qué actividades se producen y cualquier parámetro clave que afecte al procesamiento.</td>
<td>
<ul>
<li> Desarrollo local</li>
<li>Desarrollo</li>
</ul></td>
</tr>
<tr>
<td>
Escenario</td>
<td>
AVISAR</td>
<td>
Describe las condiciones que pueden convertirse en errores.<br>
Cuando el registro ADVERTENCIA está activo, solo se registran las instrucciones que indican condiciones que se aproximan a la suboptimización.</td>
<td>
<ul>
<li> Desarrollo local</li>
<li>Desarrollo</li>
<li>Escenario</li>
</ul></td>
</tr>
<tr>
<td>
Producción</td>
<td>
ERROR</td>
<td>
Describe las condiciones que indican un error y que deben resolverse.<br>
Cuando el registro de ERRORES está activo, solo se registran las instrucciones que indican errores. Las instrucciones de registro de ERRORES indican un problema grave que debe resolverse lo antes posible.</td>
<td>
<ul>
<li> Desarrollo local</li>
<li>Desarrollo</li>
<li>Escenario</li>
<li>Producción</li>
</ul></td>
</tr>
</table>

Aunque el registro de Java admite varios niveles más de granularidad de registro, AEM as a Cloud Service recomienda utilizar los tres niveles descritos anteriormente.

Los niveles de registro de AEM se establecen por tipo de entorno a través de la configuración OSGi, que a su vez se compromete a Git e implementan mediante Cloud Manager en AEM as a Cloud Service. Debido a esto, es mejor mantener las instrucciones de registro coherentes y bien conocidas para los tipos de entorno para garantizar que los registros disponibles a través de AEM as a Cloud Service estén disponibles en el nivel de registro óptimo sin requerir una reimplementación de la aplicación con la configuración de nivel de registro actualizada.

**Ejemplo de salida de registro**

```
22.06.2020 18:33:30.120 [cm-p12345-e6789-aem-author-86657cbb55-xrnzq] *ERROR* [qtp501076283-1809] io.prometheus.client.dropwizard.DropwizardExports Failed to get value from Gauge
22.06.2020 18:33:30.229 [cm-p12345-e6789-aem-author-86657cbb55-xrnzq] *INFO* [qtp501076283-1805] org.apache.sling.auth.core.impl.SlingAuthenticator getAnonymousResolver: Anonymous access not allowed by configuration - requesting credentials
22.06.2020 18:33:30.370 [cm-p12345-e6789-aem-author-86657cbb55-xrnzq] *INFO* [73.91.59.34 [1592850810364] GET /libs/granite/core/content/login.html HTTP/1.1] org.apache.sling.i18n.impl.JcrResourceBundle Finished loading 0 entries for 'en_US' (basename: <none>) in 4ms
22.06.2020 18:33:30.372 [cm-p12345-e6789-aem-author-86657cbb55-xrnzq] *INFO* [FelixLogListener] org.apache.sling.i18n Service [5126, [java.util.ResourceBundle]] ServiceEvent REGISTERED
22.06.2020 18:33:30.372 [cm-p12345-e6789-aem-author-86657cbb55-xrnzq] *WARN* [73.91.59.34 [1592850810364] GET /libs/granite/core/content/login.html HTTP/1.1] libs.granite.core.components.login.login$jsp j_reason param value 'unknown' cannot be mapped to a valid reason message: ignoring
```

**Formato de registro**

<table>
<tbody>
<tr>
<td>Fecha y hora</td>
<td>29.04.2020 21:50:13.398</td>
</tr>
<tr>
<td>ID del nodo AEM as a Cloud Service</td>
<td>[cm-p1234-e5678-aem-author-59555cb5b8-q7l9s]</td>
</tr>
<tr>
<td>Nivel de registro</td>
<td>DEPURAR</td>
</tr>
<tr>
<td>Hilo</td>
<td>qtp2130572036-1472</td>
</tr>
<tr>
<td>clase Java</td>
<td>com.example.approval.workflow.impl.CustomApprovalWorkflow</td>
</tr>
<tr>
<td>Mensaje de registro</td>
<td>No se ha especificado un aprobador, se establece de forma predeterminada [ grupo de usuarios Aprobadores de Creative ]</td>
</tr>
</tbody>
</table>

### Registradores de configuración {#configuration-loggers}

Los registros de Java de AEM se definen como configuración OSGi y, por lo tanto, se dirigen a entornos de AEM as a Cloud Service específicos mediante carpetas en modo de ejecución.

Configure el registro java para paquetes Java personalizados mediante las configuraciones OSGi para la fábrica de Sling LogManager. Hay tres propiedades de configuración admitidas:

| Propiedad de configuración OSGi | Descripción |
|---|---|
| `org.apache.sling.commons.log.names` | Los paquetes Java para los que se recopilan instrucciones de registro. |
| `org.apache.sling.commons.log.level` | Nivel de registro en el que registrar los paquetes Java, especificado por `org.apache.sling.commons.log.names` |
| `org.apache.sling.commons.log.file` | Especifique el destino de la salida: `logs/error.log` |

El cambio de otras propiedades de configuración de LogManager OSGi puede provocar problemas de disponibilidad en AEM as a Cloud Service.

A continuación se muestran ejemplos de las configuraciones de registro recomendadas (con el paquete Java de marcador de posición de `com.example`) para los tres tipos de entorno de AEM as a Cloud Service.

### Desarrollo {#development}

/apps/my-app/config/org.apache.sling.commons.log.LogManager.factory.config-example.cfg.json

```
{
    "org.apache.sling.commons.log.names": ["com.example"],
    "org.apache.sling.commons.log.level": "debug"
    "org.apache.sling.commons.log.file": "logs/error.log"
}
```

### Escenario {#stage}

/apps/my-app/config.stage/org.apache.sling.commons.log.LogManager.factory.config-example.cfg.json

```
{
    "org.apache.sling.commons.log.names": ["com.example"],
    "org.apache.sling.commons.log.level": "warn"
    "org.apache.sling.commons.log.file": "logs/error.log"
}
```

### Producción {#productiomn}

/apps/my-app/config.prod/org.apache.sling.commons.log.LogManager.factory.config-example.cfg.json

```
{
    "org.apache.sling.commons.log.names": ["com.example"],
    "org.apache.sling.commons.log.level": "error"
    "org.apache.sling.commons.log.file": "logs/error.log"
}
```

## Registro de solicitudes HTTP de AEM {#aem-http-request-logging}

El registro de solicitudes HTTP de AEM as a Cloud Service proporciona una perspectiva de las solicitudes HTTP realizadas a AEM y sus respuestas HTTP en el orden temporal. Este registro es útil para comprender las solicitudes HTTP realizadas a AEM y el orden en que se procesan y responden.

La clave para comprender este registro es asignar los pares de solicitud y respuesta HTTP por sus ID, indicados por el valor numérico entre corchetes. A menudo, las solicitudes y sus respuestas correspondientes tienen otras solicitudes HTTP y respuestas interconectadas entre ellas en el registro.

**Ejemplo de registro**

```
29/Apr/2020:19:14:21 +0000 [137] > POST /conf/global/settings/dam/adminui-extension/metadataprofile/ HTTP/1.1 [cm-p1234-e5678-aem-author-59555cb5b8-q7l9s]
...
29/Apr/2020:19:14:22 +0000 [139] > GET /mnt/overlay/dam/gui/content/processingprofilepage/metadataprofiles/editor.html/conf/global/settings/dam/adminui-extension/metadataprofile/main HTTP/1.1 [cm-p1234-e5678-aem-author-59555cb5b8-q7l9s]
...
29/Apr/2020:19:14:21 +0000 [137] <- 201 text/html 111ms [cm-p1234-e5678-aem-author-59555cb5b8-q7l9s]
...
29/Apr/2020:19:14:22 +0000 [139] <- 200 text/html;charset=utf-8 637ms [cm-p1234-e5678-aem-author-59555cb5b8-q7l9s]
```

**Formato de registro**

<table>
<tbody>
<tr>
<td>Fecha y hora</td>
<td>29/Abr/2020:19:14:21 +0000</td>
</tr>
<tr>
<td>ID de par de solicitud/respuesta</td>
<td><code>[137]</code></td>
</tr>
<tr>
<td>Método HTTP</td>
<td>PUBLICAR</td>
</tr>
<tr>
<td>URL</td>
<td>/conf/global/settings/dam/adminui-extension/metadataprofile/</td>
</tr>
<tr>
<td>Protocolo</td>
<td>HTTP/1.1
</td>
</tr>
<tr>
<td>ID del nodo AEM as a Cloud Service</td>
<td>[cm-p1234-e5678-aem-author-59555cb5b8-q7l9s]</td>
</tr>
</tbody>
</table>

### Configuración del registro {#configuring-the-log}

El registro de solicitudes HTTP de AEM no se puede configurar en AEM as a Cloud Service.

## Registro de acceso HTTP de AEM {#aem-http-access-logging}

El registro de acceso HTTP de AEM as Cloud Service muestra las solicitudes HTTP en el orden temporal. Cada entrada de registro representa la solicitud HTTP que accede a AEM.

Este registro es útil para comprender rápidamente qué solicitudes HTTP se realizan a AEM, si tienen éxito consultando el código de estado de respuesta HTTP adjunto y cuánto tiempo tardó la solicitud HTTP en completarse. Este registro también puede resultar útil para depurar la actividad de un usuario específico filtrando las entradas de registro por usuarios.

**Ejemplo de salida de registro**

```
cm-p1234-e26813-aem-author-59555cb5b8-8kgr2 - example@adobe.com 30/Apr/2020:17:37:14 +0000  "GET /libs/granite/ui/references/clientlibs/references.lc-5188e85840c529149e6cd29d94e74ad5-lc.min.css HTTP/1.1" 200 1141 "https://author-p10711-e26813.adobeaemcloud.com/mnt/overlay/dam/gui/content/assets/metadataeditor.external.html?item=/content/dam/en/images/example.jpeg&_charset_=utf8" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_4) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/81.0.4044.122 Safari/537.36"
cm-p1234-e26813-aem-author-59555cb5b8-8kgr2 - example@adobe.com 30/Apr/2020:17:37:14 +0000  "GET /libs/dam/gui/coral/components/admin/customthumb/clientlibs.lc-60e4443805c37afa0c74b674b141f1df-lc.min.css HTTP/1.1" 200 809 "https://author-p10711-e26813.adobeaemcloud.com/mnt/overlay/dam/gui/content/assets/metadataeditor.external.html?item=/content/dam/en/images/example.jpeg&_charset_=utf8" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_4) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/81.0.4044.122 Safari/537.36"
cm-p1234-e26813-aem-author-59555cb5b8-8kgr2 - example@adobe.com 30/Apr/2020:17:37:14 +0000  "GET /libs/dam/gui/coral/components/admin/metadataeditor/clientlibs/metadataeditor.lc-4a2226d8232f8b7ab27d24820b9ddd64-lc.min.js HTTP/1.1" 200 7965 "https://author-p10711-e26813.adobeaemcloud.com/mnt/overlay/dam/gui/content/assets/metadataeditor.external.html?item=/content/dam/en/images/example.jpeg&_charset_=utf8" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_4) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/81.0.4044.122 Safari/537.36"
```

| ID de nodo de AEM as a Cloud Service | cm-p1235-e2644-aem-author-59555cb5b8-8kgr2 |
|---|---|
| Dirección IP del cliente | - |
| Usuario | myuser@adobe.com |
| Fecha y hora | 30/Abr/2020:17:37:14 +0000 |
| método HTTP | GET |
| URL | `/libs/granite/ui/references/clientlibs/references.lc-5188e85840c529149e6cd29d94e74ad5-lc.min.css` |
| Protocolo | HTTP/1.1 |
| Estado de respuesta HTTP | 200 |
| Tamaño del cuerpo de respuesta en bytes | 1141 |
| Remitente del reenvío | `"https://author-p1234-e4444.adobeaemcloud.com/mnt/overlay/dam/gui/content/assets/metadataeditor.external.html?item=/content/dam/wknd/en/adventures/surf-camp-in-costa-rica/adobestock_266405335.jpeg&_charset_=utf8"` |
| Agente de usuario | `"Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_4) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/81.0.4044.122 Safari/537.36"` |

### Configuración del registro de acceso HTTP {#configuring-the-http-access-log}

El registro de acceso HTTP no se puede configurar en AEM as a Cloud Service.

## Servidor web Apache y registro en Dispatcher {#apache-web-server-and-dispatcher-logging}

AEM as a Cloud Service proporciona tres registros para los servidores web Apache y la capa de Dispatcher en el entorno de publicación:

* Registro de acceso al servidor web Apache HTTPD
* Registro de errores del servidor web Apache HTTPD
* Registro de Dispatcher

Estos registros solo están disponibles para el nivel de publicación.

Este conjunto de registros proporciona información sobre las solicitudes HTTP al nivel de publicación de AEM as a Cloud Service antes de que dichas solicitudes lleguen a la aplicación de AEM. Esto es importante a entender, ya que, idealmente, la mayoría de las solicitudes HTTP a los servidores de nivel de publicación están servidas por contenido que está almacenado en caché por el servidor web Apache HTTPD y AEM Dispatcher, y nunca llegan a la propia aplicación de AEM. Por lo tanto, no hay instrucciones de registro para estas solicitudes en los registros de Java, Solicitud o Acceso de AEM.

### Registro de acceso al servidor web Apache HTTPD {#apache-httpd-web-server-access-log}

El registro de acceso del servidor web HTTP Apache proporciona instrucciones para cada solicitud HTTP que llega al servidor web/Dispatcher del nivel de publicación. Las solicitudes servidas desde una CDN ascendente no se reflejan en estos registros.

Vea información sobre el formato del registro de errores en [documentación oficial de apache](https://httpd.apache.org/docs/2.4/logs.html#accesslog).

**Ejemplo de salida de registro**

```
cm-p1234-e5678-aem-publish-b86c6b466-qpfvp - - 17/Jul/2020:09:14:41 +0000  "GET /etc.clientlibs/wknd/clientlibs/clientlib-site/resources/images/favicons/favicon-32.png HTTP/1.1" 200 715 "-" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10.15; rv:78.0) Gecko/20100101 Firefox/78.0"
cm-p1234-e5678-aem-publish-b86c6b466-qpfvp - - 17/Jul/2020:09:14:41 +0000  "GET /etc.clientlibs/wknd/clientlibs/clientlib-site/resources/images/favicons/favicon-512.png HTTP/1.1" 200 9631 "-" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10.15; rv:78.0) Gecko/20100101 Firefox/78.0"
cm-p1234-e5678-aem-publish-b86c6b466-qpfvp - - 17/Jul/2020:09:14:42 +0000  "GET /etc.clientlibs/wknd/clientlibs/clientlib-site/resources/images/country-flags/US.svg HTTP/1.1" 200 810 "https://publish-p6902-e30226.adobeaemcloud.com/content/wknd/us/en.html" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10.15; rv:78.0) Gecko/20100101 Firefox/78.0"
```

**Formato de registro**

<table>
<tbody>
<tr>
<td>ID del nodo de AEM as a Cloud Service</td>
<td>cm-p1234-e26813-aem-publish-5c787687c-lqlxr</td>
</tr>
<tr>
<td>Dirección IP del cliente</td>
<td>-</td>
</tr>
<tr>
<td>Usuario</td>
<td>-</td>
</tr>
<tr>
<td>Fecha y hora</td>
<td>01/May/2020:00:09:46 +0000</td>
</tr>
<tr>
<td>Método HTTP</td>
<td>GET</td>
</tr>
<tr>
<td>URL</td>
<td>/content/example.html</td>
</tr>
<tr>
<td>Protocolo</td>
<td>HTTP/1.1</td>
</tr>
<tr>
<td>Estado de respuesta HTTP</td>
<td>200</td>
</tr>
<tr>
<td>Tamaño</td>
<td>310</td>
</tr>
<tr>
<td>Referente</td>
<td>-</td>
</tr>
<tr>
<td>Agente de usuario</td>
<td>"Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_4) AppleWebKit/537.36 (KHTML, como Gecko) Chrome/81.0.4044.122 Safari/537.36"</td>
</tr>
</tbody>
</table>

### Configuración del registro de acceso del servidor web Apache HTTPD {#configuring-the-apache-httpd-webs-server-access-log}

Este registro no se puede configurar en AEM as a Cloud Service.

## Registro de errores del servidor web Apache HTTPD {#apache-httpd-web-server-error-log}

El registro de errores del servidor web HTTP Apache proporciona instrucciones para cada error en el servidor web/Dispatcher del nivel de publicación.

Vea información sobre el formato del registro de errores en [documentación oficial de apache](https://httpd.apache.org/docs/2.4/logs.html#errorlog).

**Ejemplo de salida de registro**

```
Fri Jul 17 02:19:48.093820 2020 [mpm_worker:notice] [pid 1:tid 140272153361288] [cm-p1234-e30226-aem-publish-b86c6b466-b9427] AH00292: Apache/2.4.43 (Unix) Communique/4.3.4-20200424 mod_qos/11.63 configured -- resuming normal operations
Fri Jul 17 02:19:48.093874 2020 [core:notice] [pid 1:tid 140272153361288] [cm-p1234-e30226-aem-publish-b86c6b466-b9427] AH00094: Command line: 'httpd -d /etc/httpd -f /etc/httpd/conf/httpd.conf -D FOREGROUND -D ENVIRONMENT_PROD'
Fri Jul 17 02:29:34.517189 2020 [mpm_worker:notice] [pid 1:tid 140293638175624] [cm-p1234-e30226-aem-publish-b496f64bf-5vckp] AH00295: caught SIGTERM, shutting down
```

**Formato de registro**

<table>
<tbody>
<tr>
<td>Fecha y hora</td>
<td>Vie, 17 de julio de 2020 :16:42.608913 de 2020</td>
</tr>
<tr>
<td>Nivel de evento</td>
<td>[mpm_worker:aviso]</td>
</tr>
<tr>
<td>ID de proceso</td>
<td>[pid 1:tid 140715149343624]</td>
</tr>
<tr>
<td>Nombre de pod</td>
<td>[cm-p1234-e56789-aem-publish-b86c6b466-qpfvp]</td>
</tr>
<tr>
<td>Mensaje</td>
<td>AH00094: Línea de comandos: 'httpd -d /etc/httpd -f /etc/httpd/conf/httpd.conf -D PRIMER PLANO -D </td>
</tr>
</tbody>
</table>

### Configuración del registro de errores del servidor web Apache HTTPD {#configuring-the-apache-httpd-web-server-error-log}

Los niveles de registro mod_rewrite los define la variable REWRITE_LOG_LEVEL en el archivo `conf.d/variables/global.var`.

Se puede establecer en error, warn, info, debug y trace1 - trace8, con un valor predeterminado de warn. Para depurar RewriteRules, se recomienda elevar el nivel de registro a trace2. Se recomienda depurar las reglas de reescritura usando [Dispatcher SDK](../../dispatcher/validation-debug.md). El nivel máximo de registro para AEM as a Cloud Service es `debug`. Por lo tanto, actualmente no es posible depurar y reescribir reglas en la nube.

Consulte la [documentación del módulo mod_rewrite](https://httpd.apache.org/docs/current/mod/mod_rewrite.html#logging) para obtener más información.

Para establecer el nivel de registro por entorno, utilice la rama condicional adecuada en el archivo global.var, como se describe a continuación:

```
Define REWRITE_LOG_LEVEL debug
  
<IfDefine ENVIRONMENT_STAGE>
  ...
  Define REWRITE_LOG_LEVEL warn
  ...
</IfDefine>
<IfDefine ENVIRONMENT_PROD>
  ...
  Define REWRITE_LOG_LEVEL error
  ...
</IfDefine>
```

## Registro de Dispatcher {#dispatcher-log}

**Ejemplo**

```
[17/Jul/2020:23:48:06 +0000] [I] [cm-p12904-e25628-aem-publish-6c5f7c9dbd-mzcvr] "GET /content/wknd/us/en/adventures.html" - 475ms [publishfarm/0] [action miss] "publish-p12904-e25628.adobeaemcloud.com"
[17/Jul/2020:23:48:07 +0000] [I] [cm-p12904-e25628-aem-publish-6c5f7c9dbd-mzcvr] "GET /content/wknd/us/en/adventures/climbing-new-zealand/_jcr_content/root/responsivegrid/carousel/item_1571266094599.coreimg.jpeg/1473680817282/sport-climbing.jpeg" 302 10ms [publishfarm/0] [action none] "publish-p12904-e25628.adobeaemcloud.com"
[17/Jul/2020:23:48:07 +0000] [I] [cm-p12904-e25628-aem-publish-6c5f7c9dbd-mzcvr] "GET /content/wknd/us/en/adventures/ski-touring-mont-blanc/_jcr_content/root/responsivegrid/carousel/item_1571168419252.coreimg.jpeg/1572047288089/adobestock-238230356.jpeg" 302 11ms [publishfarm/0] [action none] "publish-p12904-e25628.adobeaemcloud.com"
```

**Formato de registro**

<table>
<tbody>
<tr>
<td>Fecha y hora</td>
<td>[17/Jul/2020:23:48:16 +0000]</td>
</tr>
<tr>
<td>Nombre de pod</td>
<td>[cm-p12904-e25628-aem-publish-6c5f7c9dbd-mzcvr]</td>
</tr>
<tr>
<td>Protocolo</td>
<td>GET</td>
</tr>
<tr>
<td>URL</td>
<td>/content/experience-fragments/wknd/language-masters/en/contributors/sofia-sjoeberg/master/_jcr_content/root/responsivegrid/image.coreimg.100.500.jpeg/1572236359031/ayo-ogunseinde-237739.jpeg</td>
</tr>
<tr>
<td>Código de estado de respuesta de Dispatcher</td>
<td>/content/experience-fragments/wknd/language-masters/en/contributors/sofia-sjoeberg/master/_jcr_content/root/responsivegrid/image.coreimg.100.500.jpeg/1572236359031/ayo-ogunseinde-237739.jpeg</td>
</tr>
<tr>
<td>Duración</td>
<td>1949 ms</td>
</tr>
<tr>
<td>Granja</td>
<td>[publishfarm/0]</td>
</tr>
<tr>
<td>Estado de caché</td>
<td>[falta de acción]</td>
</tr>
<tr>
<td>Host</td>
<td>"publish-p12904-e25628.adobeaemcloud.com"</td>
</tr>
</tbody>
</table>

### Configuración del registro de errores de Dispatcher {#configuring-the-dispatcher-error-log}

Los niveles de registro de Dispatcher los define la variable DISP_LOG_LEVEL en el archivo `conf.d/variables/global.var`.

Se puede establecer en error, warn, info, debug y trace1, con un valor predeterminado de warn.

Aunque el registro de Dispatcher admite varios niveles más de granularidad de registro, AEM as a Cloud Service recomienda utilizar los niveles que se describen a continuación.

Para establecer el nivel de registro por entorno, utilice la rama condicional adecuada en el archivo `global.var`, como se describe a continuación:

```
Define DISP_LOG_LEVEL debug
  
<IfDefine ENVIRONMENT_STAGE>
  ...
  Define DISP_LOG_LEVEL warn
  ...
</IfDefine>
<IfDefine ENVIRONMENT_PROD>
  ...
  Define DISP_LOG_LEVEL error
  ...
</IfDefine>
```

>[!NOTE]
>
>Para entornos de AEM as a Cloud Service, la depuración es el nivel de detalle máximo. El nivel de registro de seguimiento no es compatible, por lo que debe evitar configurarlo cuando trabaje en entornos de nube.

## Registro de CDN {#cdn-log}

AEM as a Cloud Service proporciona acceso a los registros de CDN, que son útiles para casos de uso, incluida la optimización de la proporción de visitas de caché. El formato de registro de CDN no se puede personalizar y no se puede configurar en diferentes modos, como información, advertir o error.

**Ejemplo**

```
{
"timestamp": "2023-05-26T09:20:01+0000",
"ttfb": 19,
"cli_ip": "147.160.230.112",
"cli_country": "CH",
"rid": "974e67f6",
"req_ua": "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/605.1.15 (KHTML, like Gecko) Version/14.0.3 Safari/605.1.15",
"host": "example.com",
"url": "/content/hello.png",
"method": "GET",
"res_ctype": "image/png",
"cache": "PASS",
"status": 200,
"res_age": 0,
"pop": "PAR",
"rules": "match=Enable-SQL-Injection-and-XSS-waf-rules-globally,waf=SQLI,action=blocked"
}
```

**Formato de registro**

Los registros de CDN son diferentes de los otros registros en el sentido de que se adhiere a un formato json.

| **Nombre del campo** | **Descripción** |
|---|---|
| *timestamp* | Hora a la que se inició la solicitud, después de la finalización de TLS |
| *ttfb* | Abreviatura de *Time To First Byte*. Intervalo de tiempo entre el inicio de la solicitud hasta el punto en el que el cuerpo de la respuesta comenzó a transmitirse. |
| *cli_ip* | La dirección IP del cliente. |
| *cli_country* | Código de país [ISO 3166-1](https://en.wikipedia.org/wiki/ISO_3166-1) alpha-2 de dos letras correspondiente al país del cliente. |
| *rid* | El valor del encabezado de la solicitud que se utiliza para identificar la solicitud de forma exclusiva. |
| *req_ua* | El agente de usuario responsable de realizar una petición HTTP determinada. |
| *host* | La autoridad a la que está destinada la solicitud. |
| *URL* | La ruta completa, incluidos los parámetros de consulta. |
| *method* | Método HTTP enviado por el cliente, como &quot;GET&quot; o &quot;POST&quot;. |
| *res_ctype* | Tipo de contenido que se utiliza para indicar el tipo de medio original del recurso. |
| *cache* | Estado de la caché. Los valores posibles son HIT, MISS o PASS |
| *status* | El código de estado HTTP como un valor entero. |
| *res_age* | Cantidad de tiempo (en segundos) que una respuesta se ha almacenado en la caché (en todos los nodos). |
| *pop* | Centro de datos del servidor de caché de CDN. |
| *reglas* | Los nombres de cualquier [regla de filtro de tráfico](/help/security/traffic-filter-rules-including-waf.md) que coincida con los indicadores WAF, también indican si la coincidencia resultó en un bloqueo. Vacío si no coinciden las reglas. |


## Cómo acceder a los registros {#how-to-access-logs}

### Entornos de la nube {#cloud-environments}

Se puede acceder a los registros de AEM as a Cloud Service para servicios en la nube mediante la descarga a través de la interfaz de Cloud Manager o siguiendo los registros en la línea de comandos utilizando la interfaz de línea de comandos de Adobe I/O. Para obtener más información, consulte la [documentación de registro de Cloud Manager](/help/implementing/cloud-manager/manage-logs.md).

### Registros para regiones de publicación adicionales {#logs-for-additional-publish-regions}

Si hay habilitadas regiones de publicación adicionales para un entorno determinado, los registros de cada región estarán disponibles para su descarga desde Cloud Manager, como se mencionó anteriormente.

Los registros de AEM y los registros de Dispatcher para las regiones de publicación adicionales especificarán la región en las tres primeras letras después del ID de entorno, como se muestra en **nld2** en el ejemplo siguiente, que hace referencia a una instancia de publicación de AEM adicional ubicada en los Países Bajos:

```
cm-p7613-e12700-nld2-aem-publish-bcbb77549-5qmmt 127.0.0.1 - 07/Nov/2023:23:57:11 +0000 "HEAD /libs/granite/security/currentuser.json HTTP/1.1" 200 - "-" "Java/11.0.19"
```

### El SDK local {#local-sdk}

AEM as a Cloud Service SDK proporciona archivos de registro para admitir el desarrollo local.

Los registros de AEM se encuentran en la carpeta `crx-quickstart/logs`, donde se pueden ver los siguientes registros:

* Registro Java de AEM: `error.log`
* Registro de solicitudes HTTP de AEM: `request.log`
* Registro de acceso HTTP de AEM: `access.log`

Los registros de capa de Apache, incluido Dispatcher, están en el contenedor Docker que contiene el Dispatcher. Consulte la [documentación de Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/content-delivery/disp-overview.html) para obtener información sobre cómo iniciar Dispatcher.

Para recuperar los registros:

1. En la línea de comandos, escriba `docker ps` para enumerar los contenedores
1. Para iniciar sesión en el contenedor, escriba &quot;`docker exec -it <container> /bin/sh`&quot;, donde `<container>` es el identificador del contenedor de Dispatcher del paso anterior
1. Vaya a la raíz de caché en `/mnt/var/www/html`
1. Los registros están en `/etc/httpd/logs`
1. Inspeccione los registros: se puede acceder a ellos en la carpeta XYZ, donde se pueden ver los siguientes registros:
   * Registro de acceso al servidor web Apache HTTPD - `httpd_access.log`
   * Registros de errores del servidor web Apache HTTPD: `httpd_error.log`
   * Registros de Dispatcher: `dispatcher.log`

Los registros también se imprimen directamente en la salida de terminal. La mayoría de las veces, estos registros deben ser DEBUG, lo que se puede lograr pasando el nivel de Depuración como parámetro al ejecutar Docker. Por ejemplo:

`DISP_LOG_LEVEL=Debug ./bin/docker_run.sh out docker.for.mac.localhost:4503 8080`

## Depuración de producción y ensayo {#debugging-production-and-stage}

En circunstancias excepcionales, es necesario cambiar los niveles de registro para que registren con una granularidad más precisa en los entornos de Ensayo o Producción.

Aunque esto es posible, requiere cambios en los niveles de registro en los archivos de configuración en Git de Advertir y error a depurar y realizar una implementación en AEM as a Cloud Service para registrar estos cambios de configuración con los entornos.

Según el tráfico y la cantidad de instrucciones de registro escritas por Debug, esto puede afectar negativamente al rendimiento del entorno, por lo que se recomienda realizar cambios en los niveles de depuración de Ensayo y Producción:

* Hecho con prudencia, y solo cuando sea absolutamente necesario
* Volver a los niveles adecuados y volver a implementarlos lo antes posible

## Reenvío de registro {#log-forwarding}

Aunque los registros se pueden descargar desde Cloud Manager, para algunas organizaciones resulta beneficioso reenviarlos a un destino de registro preferido. AEM admite registros de flujo continuo a los siguientes destinos:

* Almacenamiento de Azure Blob
* Datadog
* HTTPD
* Elasticsearch (y OpenSearch)
* Splunk

Consulte el [artículo de reenvío de registros](/help/implementing/developing/introduction/log-forwarding.md) para obtener detalles sobre cómo configurar esta característica.

>[!NOTE]
>
>No se admite el reenvío de registros para entornos de programa de zona protegida.
