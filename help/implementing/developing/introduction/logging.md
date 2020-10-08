---
title: Registro
description: Obtenga información sobre cómo configurar los parámetros globales para el servicio de registro central, la configuración específica para los servicios individuales o cómo solicitar el registro de datos.
translation-type: tm+mt
source-git-commit: 0b648e1a0da141f8393c62cb269e5498e2ecd23f
workflow-type: tm+mt
source-wordcount: '2219'
ht-degree: 3%

---


# Registro {#logging}

AEM como Cloud Service es una plataforma para que los clientes incluyan código personalizado para crear experiencias únicas para su base de clientes. Teniendo esto en cuenta, el registro es una función crítica para depurar y entender la ejecución del código en el desarrollo local y los entornos de nube, especialmente el AEM como entornos de desarrolladores de Cloud Service.

Los niveles de registro y registro de AEM se administran en archivos de configuración que se almacenan como parte del proyecto de AEM en Git y se implementan como parte del proyecto de AEM mediante Cloud Manager. El inicio de sesión en AEM como Cloud Service se puede dividir en dos conjuntos lógicos:

* Registro de AEM, que realiza el registro en el nivel de aplicación AEM
* El registro Apache HTTPD Web Server/Dispatcher, que realiza el registro del servidor web y Dispatcher en el nivel Publicar.

## Registro de AEM {#aem-loggin}

El registro en el nivel de aplicación AEM se administra mediante tres registros:

1. Registros de Java de AEM, que representan las sentencias de registro de Java para la aplicación AEM.
1. Registros de solicitudes HTTP, que registran información sobre solicitudes HTTP y sus respuestas servidas por AEM
1. Registros de acceso HTTP, que registran información resumida y solicitudes HTTP servidas por AEM

>[!NOTE]
>
>Las solicitudes HTTP que se envían desde la caché Dispatcher del nivel de publicación o desde la CDN de flujo ascendente no se reflejan en estos registros.

## Registro de Java AEM {#aem-java-logging}

AEM como Cloud Service proporciona acceso a las sentencias de registro de Java. Los desarrolladores de aplicaciones para AEM deben seguir las optimizaciones generales de registro de Java, registrando afirmaciones pertinentes sobre la ejecución de código personalizado, en los siguientes niveles de registro:

<table>
<tr>
<td>
<b>entorno AEM</b></td>
<td>
<b>Nivel de registro</b></td>
<td>
<b>Descripción</b></td>
<td>
<b>Disponibilidad de estado de registro</b></td>
</tr>
<tr>
<td>
Desarrollo</td>
<td>
DEPURACIONES</td>
<td>
Describe lo que sucede en la aplicación.<br>
Cuando el registro DEBUG está activo, se registran las instrucciones que proporcionan una imagen clara de las actividades que se producen, así como los parámetros clave que afectan al procesamiento.</td>
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
Cuando el registro de WARN está activo, solo se registran las afirmaciones que indican condiciones que se acercan a la suboptimización.</td>
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
Describe las condiciones que indican un error y deben resolverse.<br>
Cuando el registro de ERROR está activo, solo se registran las sentencias que indican errores. Las instrucciones del registro de errores indican un problema grave que debe resolverse lo antes posible.</td>
<td>
<ul>
<li> Desarrollo local</li>
<li>Desarrollo</li>
<li>Escenario</li>
<li>Producción</li>
</ul></td>
</tr>
</table>

Aunque el registro de Java admite otros niveles de granularidad de registro, AEM como un Cloud Service recomienda usar los tres niveles descritos anteriormente.

AEM Los niveles de registro se establecen por tipo de entorno mediante la configuración OSGi, que a su vez se asignan a Git, y se implementan mediante Cloud Manager para AEM como Cloud Service. Debido a esto, lo mejor es mantener las declaraciones de registro coherentes y bien conocidas para los tipos de entornos, a fin de garantizar que los registros disponibles a través de AEM como Cloud Service estén disponibles en el nivel de registro óptimo sin necesidad de reimplementar la aplicación con la configuración actualizada del nivel de registro.

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
<td>AEM como ID de nodo de Cloud Service</td>
<td>[cm-p1234-e5678-aem-author-59555cb5b8-q7l9s]</td>
</tr>
<tr>
<td>Nivel de registro</td>
<td>DEPURACIONES</td>
</tr>
<tr>
<td>Subproceso</td>
<td>qtp2130572036-1472</td>
</tr>
<tr>
<td>Clase Java</td>
<td>com.example.approval.workflow.impl.CustomApprovalWorkflow</td>
</tr>
<tr>
<td>Mensaje de registro</td>
<td>No se especificó un aprobador, el valor predeterminado es [ grupo de usuarios de aprobadores creativos ]</td>
</tr>
</tbody>
</table>

### Registros de configuración {#configuration-loggers}

Los registros de Java AEM se definen como configuración OSGi y, por lo tanto, son AEM específicos de destinatario como entornos de Cloud Service que utilizan carpetas en modo de ejecución.

Configure el registro de Java para paquetes Java personalizados mediante configuraciones OSGi para la fábrica Sling LogManager. Existen dos propiedades de configuración admitidas:

| OSGi Configuration, propiedad | Descripción |
|---|---|
| org.apache.sling.commons.log.names | Los paquetes Java para los que se recopilan las sentencias de registro. |
| org.apache.sling.commons.log.level | El nivel de registro en el que se registran los paquetes Java, especificado por org.apache.sling.commons.log.names |

Cambiar otras propiedades de configuración de OSGi de LogManager puede provocar problemas de disponibilidad en AEM como Cloud Service.

Los siguientes son ejemplos de las configuraciones de registro recomendadas (mediante el paquete de `com.example`Java del marcador de posición) para los tres AEM como tipos de entorno de Cloud Service.

### Desarrollo {#development}

/apps/my-app/config/org.apache.sling.commons.log.LogManager.Factory.config-example.cfg.json

```
{
    "org.apache.sling.commons.log.names": ["com.example"],
    "org.apache.sling.commons.log.level": "debug"
}
```

### Escenario {#stage}

/apps/my-app/config.stage/org.apache.sling.commons.log.LogManager.Factory.config-example.cfg.json

```
{
    "org.apache.sling.commons.log.names": ["com.example"],
    "org.apache.sling.commons.log.level": "warn"
}
```

### Producción {#productiomn}

/apps/my-app/config.prod/org.apache.sling.commons.log.LogManager.Factory.config-example.cfg.json

```
{
    "org.apache.sling.commons.log.names": ["com.example"],
    "org.apache.sling.commons.log.level": "error"
}
```

## Registro de solicitudes HTTP AEM {#aem-http-request-logging}

AEM como registro de solicitud HTTP de Cloud Service proporciona una perspectiva de las solicitudes HTTP realizadas a AEM y sus respuestas HTTP en orden temporal. Este registro es útil para comprender las solicitudes HTTP realizadas a AEM y el orden en que se procesan y responden.

La clave para comprender este registro es la asignación de los pares de solicitud y respuesta HTTP por sus ID, marcados por el valor numérico entre corchetes. Tenga en cuenta que a menudo las solicitudes y sus respuestas correspondientes tienen otras solicitudes HTTP y respuestas insertadas entre ellas en el registro.

**Registro de ejemplo**

```
29/Apr/2020:19:14:21 +0000 [137] -> POST /conf/global/settings/dam/adminui-extension/metadataprofile/ HTTP/1.1 [cm-p1234-e5678-aem-author-59555cb5b8-q7l9s]
...
29/Apr/2020:19:14:22 +0000 [139] -> GET /mnt/overlay/dam/gui/content/processingprofilepage/metadataprofiles/editor.html/conf/global/settings/dam/adminui-extension/metadataprofile/main HTTP/1.1 [cm-p1234-e5678-aem-author-59555cb5b8-q7l9s]
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
<td>Id. de pares de solicitud/respuesta</td>
<td><code>[137]</code></td>
</tr>
<tr>
<td>Método HTTP</td>
<td>POST</td>
</tr>
<tr>
<td>URL</td>
<td>/conf/global/settings/dam/adminui-extension/metadata aprofile/</td>
</tr>
<tr>
<td>Protocolo</td>
<td>HTTP/1.1
</td>
</tr>
<tr>
<td>AEM como ID de nodo de Cloud Service</td>
<td>[cm-p1234-e5678-aem-author-59555cb5b8-q7l9s]</td>
</tr>
</tbody>
</table>

### Configuración del registro {#configuring-the-log}

El registro de solicitud HTTP AEM no se puede configurar en AEM como Cloud Service.

## Registro de acceso HTTP AEM {#aem-http-access-logging}

AEM como registro de acceso HTTP Cloud Service muestra las solicitudes HTTP en orden temporal. Cada entrada de registro representa la solicitud HTTP que accede a AEM.

Este registro es útil para comprender rápidamente qué solicitudes HTTP se están realizando a AEM, si tienen éxito al consultar el código de estado de respuesta HTTP correspondiente y cuánto tiempo tardó en completarse la solicitud HTTP. Este registro también puede resultar útil para depurar la actividad de un usuario específico filtrando las entradas de registro por usuarios.

**Ejemplo de salida de registro**

```
cm-p1234-e26813-aem-author-59555cb5b8-8kgr2 - example@adobe.com 30/Apr/2020:17:37:14 +0000  "GET /libs/granite/ui/references/clientlibs/references.lc-5188e85840c529149e6cd29d94e74ad5-lc.min.css HTTP/1.1" 200 1141 "https://author-p10711-e26813.adobeaemcloud.com/mnt/overlay/dam/gui/content/assets/metadataeditor.external.html?item=/content/dam/en/images/example.jpeg&_charset_=utf8" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_4) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/81.0.4044.122 Safari/537.36"
cm-p1234-e26813-aem-author-59555cb5b8-8kgr2 - example@adobe.com 30/Apr/2020:17:37:14 +0000  "GET /libs/dam/gui/coral/components/admin/customthumb/clientlibs.lc-60e4443805c37afa0c74b674b141f1df-lc.min.css HTTP/1.1" 200 809 "https://author-p10711-e26813.adobeaemcloud.com/mnt/overlay/dam/gui/content/assets/metadataeditor.external.html?item=/content/dam/en/images/example.jpeg&_charset_=utf8" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_4) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/81.0.4044.122 Safari/537.36"
cm-p1234-e26813-aem-author-59555cb5b8-8kgr2 - example@adobe.com 30/Apr/2020:17:37:14 +0000  "GET /libs/dam/gui/coral/components/admin/metadataeditor/clientlibs/metadataeditor.lc-4a2226d8232f8b7ab27d24820b9ddd64-lc.min.js HTTP/1.1" 200 7965 "https://author-p10711-e26813.adobeaemcloud.com/mnt/overlay/dam/gui/content/assets/metadataeditor.external.html?item=/content/dam/en/images/example.jpeg&_charset_=utf8" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_4) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/81.0.4044.122 Safari/537.36"
```

**Formato de registro**

<table>
<tbody>
<tr>
<td>AEM como ID de nodo de Cloud Service</td>
<td>cm-p1235-e2644-aem-author-59555cb5b8-8kgr2</td>
</tr>
<tr>
<td>Dirección IP del cliente</td>
<td>-</td>
</tr>
<tr>
<td>Usuario</td>
<td>myuser@adobe.com</td>
</tr>
<tr>
<td>Fecha y hora</td>
<td>30/Abr/2020:17:37:14 +0000</td>
</tr>
<tr>
<td>Método HTTP</td>
<td>GET</td>
</tr>
<tr>
<td>URL</td>
<td>/libs/granite/ui/references/clientlibs/references.lc-5188e85840c529149e6cd29d94e74ad5-lc.min.css</td>
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
<td>Tiempo de solicitud HTTP en milisegundos</td>
<td>1141</td>
</tr>
<tr>
<td>Referencia</td>
<td><code>"https://author-p1234-e4444.adobeaemcloud.com/mnt/overlay/dam/gui/content/assets/metadataeditor.external.html?item=/content/dam/wknd/en/adventures/surf-camp-in-costa-rica/adobestock_266405335.jpeg&_charset_=utf8"</code></td>
</tr>
<tr>
<td>Agente de usuario</td>
<td>"Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_4) AppleWebKit/537.36 (KHTML, como Gecko) Chrome/81.0.4044.122 Safari/537.36"</td>
</tr>
</tbody>
</table>

### Configuración del registro de acceso HTTP {#configuring-the-http-access-log}

El registro de acceso HTTP no se puede configurar en AEM como Cloud Service.

## Registro de Apache Web Server y Dispatcher {#apache-web-server-and-dispatcher-logging}

AEM como Cloud Service proporciona tres registros para los servidores web Apache y la capa de distribuidor en la publicación:

* Registro de acceso al servidor web Apache HTTPD
* Registro de errores del servidor web Apache HTTPD
* Registro de Dispatcher

Tenga en cuenta que estos registros solo están disponibles para el nivel Publicar.

Este conjunto de registros proporciona perspectivas sobre las solicitudes HTTP al AEM como un nivel de publicación Cloud Service antes de que dichas solicitudes lleguen a la aplicación AEM. Esto es importante de comprender, ya que, idealmente, la mayoría de las solicitudes HTTP a los servidores del nivel Publicar se proporcionan con contenido almacenado en caché por Apache HTTPD Web Server y AEM Dispatcher, y nunca llegan a la aplicación AEM misma. Por lo tanto, no hay instrucciones de registro para estas solicitudes en los registros de Java, solicitud o acceso AEM.

### Registro de acceso al servidor web Apache HTTPD {#apache-httpd-web-server-access-log}

El registro de acceso al servidor web HTTP Apache proporciona instrucciones para cada solicitud HTTP que llega al servidor web o al despachante del nivel de publicación. Tenga en cuenta que las solicitudes que se proporcionan desde una CDN de flujo ascendente no se reflejan en estos registros.

Consulte la información sobre el formato de registro de errores en la documentación [](https://httpd.apache.org/docs/2.4/logs.html#accesslog)oficial de apache.

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
<td>AEM como ID de nodo del servicio de nube</td>
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
<td>01/Mayo/2020:00:09:46 +0000</td>
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

### Configuración del registro de acceso al servidor web Apache HTTPD {#configuring-the-apache-httpd-webs-server-access-log}

Este registro no se puede configurar en AEM como Cloud Service.

## Registro de errores del servidor web Apache HTTPD {#apache-httpd-web-server-error-log}

El registro de errores del servidor web HTTP Apache proporciona instrucciones para cada error en el servidor web o distribuidor del nivel de publicación.

Consulte la información sobre el formato de registro de errores en la documentación [](https://httpd.apache.org/docs/2.4/logs.html#errorlog)oficial de apache.

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
<td>Jul. vie. 17 02:16:42.608913 2020</td>
</tr>
<tr>
<td>Nivel de evento</td>
<td>[mpm_worker:notice]</td>
</tr>
<tr>
<td>ID de proceso</td>
<td>[pid 1:tid 140715149343624]</td>
</tr>
<tr>
<td>Nombre del pod</td>
<td>[cm-p1234-e56789-aem-publish-b86c6b466-qpfvp]</td>
</tr>
<tr>
<td>Mensaje</td>
<td>AH00094: Línea de comandos: 'httpd -d /etc/httpd -f /etc/httpd/conf/httpd.conf -D FOREGROUND -D </td>
</tr>
</tbody>
</table>

### Configuración del registro de errores del servidor web Apache HTTPD {#configuring-the-apache-httpd-web-server-error-log}

Los niveles de registro mod_rewrite están definidos por la variable REWRITE_LOG_LEVEL en el archivo `conf.d/variables/global.var`.

Se puede establecer en Error, Advertir, Información, Depurar y Rastrear1 - Rastrear8, con un valor predeterminado de Advertir. Para depurar RewriteRules, se recomienda elevar el nivel de registro a Trace2.

Consulte la documentación [del módulo](https://httpd.apache.org/docs/current/mod/mod_rewrite.html#logging) mod_rewrite para obtener más información.

Para establecer el nivel de registro por entorno, utilice la rama condicional adecuada en el archivo global.var, como se describe a continuación:

```
Define REWRITE_LOG_LEVEL Debug
  
<IfDefine ENVIRONMENT_STAGE>
  ...
  Define REWRITE_LOG_LEVEL Warn
  ...
</IfDefine>
<IfDefine ENVIRONMENT_PROD>
  ...
  Define REWRITE_LOG_LEVEL Error
  ...
</IfDefine>
```

## Registro del despachante {#dispatcher-log}

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
<td>Nombre del pod</td>
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
<td>1949ms</td>
</tr>
<tr>
<td>Granja</td>
<td>[publisher-granja/0]</td>
</tr>
<tr>
<td>Estado de caché</td>
<td>[acción faltante]</td>
</tr>
<tr>
<td>Host</td>
<td>"publish-p12904-e25628.adobeaemcloud.com"</td>
</tr>
</tbody>
</table>

### Configuración del registro de errores de Dispatcher {#configuring-the-dispatcher-error-log}

Los niveles de registro del despachante están definidos por la variable DISP_LOG_LEVEL en el archivo `conf.d/variables/global.var`.

Se puede establecer en Error, Advertir, Información, Depurar y Rastrear1, con un valor predeterminado de Advertir.

Aunque el registro de Dispatcher admite varios otros niveles de granularidad de registro, el AEM como Cloud Service recomienda usar los niveles que se describen a continuación.

Para establecer el nivel de registro por entorno, utilice la rama condicional adecuada en el `global.var` archivo, como se describe a continuación:

```
Define DISP_LOG_LEVEL Debug
  
<IfDefine ENVIRONMENT_STAGE>
  ...
  Define DISP_LOG_LEVEL Warn
  ...
</IfDefine>
<IfDefine ENVIRONMENT_PROD>
  ...
  Define DISP_LOG_LEVEL Error
  ...
</IfDefine>
```

## Cómo acceder a los registros {#how-to-access-logs}

### Entornos de nube {#cloud-environments}

Se puede acceder a los registros de AEM como Cloud Service para los servicios en la nube mediante la descarga a través de la interfaz del Administrador de nubes o mediante los registros de cola en la línea de comandos mediante la interfaz de línea de comandos de E/S de Adobe. Para obtener más información, consulte la documentación [de registro de](/help/implementing/cloud-manager/manage-logs.md)Cloud Manager.

### SDK local {#local-sdk}

AEM como Cloud Service SDK proporciona archivos de registro para admitir el desarrollo local.

Los registros de AEM se encuentran en la carpeta `crx-quickstart/logs`, donde se pueden ver los siguientes registros:

* Registro de Java AEM: `error.log`
* Registro de solicitud HTTP AEM: `request.log`
* Registro de acceso HTTP AEM: `access.log`

Los registros de capas de Apache, incluido el despachante, se encuentran en el contenedor de Docker que contiene el despachante. Consulte la documentación [de](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/content-delivery/disp-overview.html) Dispatcher para obtener información sobre cómo inicio del despachante.

Para recuperar los registros:

1. En la línea de comandos, escriba `docker ps` para lista de los contenedores
1. Para iniciar sesión en el contenedor, escriba &quot;`docker exec -it <container> /bin/sh`&quot;, donde `<container>` es el identificador de contenedor del despachante del paso anterior
1. Vaya a la raíz de caché en `/mnt/var/www/html`
1. Los registros están en `/etc/httpd/logs`
1. Inspect los registros: se puede acceder a ellos en la carpeta XYZ, donde se pueden ver los siguientes registros:
   * Registro de acceso al servidor web Apache HTTPD - `httpd_access.log`
   * Registros de errores del servidor web Apache HTTPD - `httpd_error.log`
   * Registros de Dispatcher: `dispatcher.log`

Los registros también se imprimen directamente en la salida de terminal. La mayoría de las veces, estos registros deben ser DEBUG, lo que se puede lograr pasando el nivel de depuración como parámetro al ejecutar Docker. Por ejemplo:

`DISP_LOG_LEVEL=Debug ./bin/docker_run.sh out docker.for.mac.localhost:4503 8080`

## Depuración de producción y etapa {#debugging-production-and-stage}

En circunstancias excepcionales, es necesario cambiar los niveles de registro para que se registren con una granularidad más precisa en entornos de fase o producción.

Aunque esto es posible, requiere cambios en los niveles de registro de los archivos de configuración en Git de Advertencia y Error a Depurar, y realizar una implementación en AEM como Cloud Service para registrar estos cambios de configuración con los entornos.

Según el tráfico y la cantidad de instrucciones de registro escritas por Debug, esto puede tener un impacto negativo en el rendimiento del entorno, por lo que se recomienda que los cambios en los niveles de depuración de fase y producción sean:

* Hecho juiciosamente, y sólo cuando sea absolutamente necesario
* Se volvió a los niveles adecuados y se volvió a implementar lo antes posible

## Registros de esperma {#splunk-logs}

Los clientes que tengan cuentas de Splunk pueden solicitar mediante ticket de asistencia al cliente que sus registros de Cloud Service de AEM se reenvíen al índice correspondiente. Los datos de registro equivalen a lo que está disponible a través de las descargas de registros de Cloud Manager, pero a los clientes les puede resultar conveniente aprovechar las funciones de consulta disponibles en el producto Splunk.

El ancho de banda de red asociado con los registros enviados a Splunk se considera parte del uso de E/S de red del cliente.

### Activación del reenvío de fragmento {#enabling-splunk-forwarding}

En la solicitud de soporte, los clientes deben indicar:

* Dirección del extremo HEC del fragmento
* El índice Splunk
* El puerto Splunk
* El token HEC del fragmento. Consulte [esta página](https://docs.splunk.com/Documentation/Splunk/8.0.4/Data/HECExamples) para obtener más información.

Las propiedades anteriores deben especificarse para cada combinación de tipo de programa/entorno pertinente.  Por ejemplo, si un cliente quería entornos de desarrollo, ensayo y producción, debe proporcionar tres conjuntos de información, como se indica a continuación.

>[!NOTE]
>
>No se admite el reenvío de fragmentos para entornos de programa de entorno limitado.

A continuación encontrará una muestra de la solicitud de asistencia al cliente:

Programa 123, Env de producción

* Dirección del extremo HEC del fragmento: `splunk-hec-ext.acme.com`
* Índice de fragmentos: acme_123prod (el cliente puede elegir la convención de nombres que desee)
* Puerto de fragmento: 443
* Distintivo HEC de fragmento: ABC123

Programa 123, Etapa Env

* Dirección del extremo HEC del fragmento: `splunk-hec-ext.acme.com`
* Índice de fragmentos: acme_123stage
* Puerto de fragmento: 443
* Distintivo HEC de fragmento: ABC123

Programa 123, Dev Envs

* Dirección del extremo HEC del fragmento: `splunk-hec-ext.acme.com`
* Índice de fragmentos: acme_123dev
* Puerto de fragmento: 443
* Distintivo HEC de fragmento: ABC123

Puede ser suficiente que se utilice el mismo índice Splunk para cada entorno, en cuyo caso puede utilizarse cualquiera de los `aem_env_type` campos para diferenciar según los valores dev, stage y prod. Si hay varios entornos de desarrollo, también se puede utilizar el `aem_env_id` campo. Algunas organizaciones pueden elegir un índice independiente para los registros del entorno de producción si el índice asociado limita el acceso a un conjunto reducido de usuarios de Splunk.

A continuación se muestra un ejemplo de entrada de registro:

```
aem_env_id: 1242
aem_env_type: dev
aem_program_id: 12314
aem_tier: author
file_path: /var/log/aem/error.log
host: 172.34.200.12 
level: INFO
msg: [FelixLogListener] com.adobe.granite.repository Service [5091, [org.apache.jackrabbit.oak.api.jmx.SessionMBean]] ServiceEvent REGISTERED
orig_time: 16.07.2020 08:35:32.346
pod_name: aemloggingall-aem-author-77797d55d4-74zvt
splunk_customer: true
```
