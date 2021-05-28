---
title: Registro para AEM como Cloud Service
description: Obtenga información sobre cómo configurar parámetros globales para el servicio de registro central, ajustes específicos para los servicios individuales o cómo solicitar el registro de datos en AEM como Cloud Service.
exl-id: 262939cc-05a5-41c9-86ef-68718d2cd6a9
source-git-commit: 856266faf4cb99056b1763383d611e9b2c3c13ea
workflow-type: tm+mt
source-wordcount: '2330'
ht-degree: 2%

---

# Registro para AEM como Cloud Service {#logging-for-aem-as-a-cloud-service}

AEM como Cloud Service es una plataforma en la que los clientes pueden incluir código personalizado para crear experiencias únicas para su base de clientes. Con esto en mente, el registro es una función crítica para depurar y comprender la ejecución del código en el desarrollo local y los entornos de nube, especialmente los entornos de desarrollo de AEM como Cloud Service.

Los niveles de registro y registro de AEM se administran en archivos de configuración que se almacenan como parte del proyecto de AEM en Git y se implementan como parte del proyecto de AEM mediante Cloud Manager. El inicio de sesión en AEM como Cloud Service se puede dividir en dos conjuntos lógicos:

* Registro de AEM, que realiza el registro en el nivel de aplicación de AEM
* Registro de Apache HTTPD Web Server/Dispatcher, que realiza el registro del servidor web y Dispatcher en el nivel de publicación.

## Registro de AEM {#aem-loggin}

El registro en el nivel de aplicación de AEM se administra mediante tres registros:

1. AEM registros Java, que procesan instrucciones de registro Java para la aplicación AEM.
1. Registros de solicitud HTTP, que registran información sobre solicitudes HTTP y sus respuestas proporcionadas por AEM
1. Registros de acceso HTTP, que registran información resumida y solicitudes HTTP proporcionadas por AEM

>[!NOTE]
>
>Las solicitudes HTTP que se proporcionan desde la caché de Dispatcher del nivel de publicación o la CDN del flujo ascendente no se reflejan en estos registros.

## Registro de Java AEM {#aem-java-logging}

AEM as a Cloud Service proporciona acceso a las instrucciones de registro de Java. Los desarrolladores de aplicaciones para AEM deben seguir las prácticas recomendadas generales de registro de Java y registrar las instrucciones pertinentes sobre la ejecución del código personalizado en los siguientes niveles de registro:

<table>
<tr>
<td>
<b>Entorno AEM</b></td>
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
Describe lo que está sucediendo en la aplicación.<br>
Cuando el registro de DEBUG está activo, se registran instrucciones que proporcionan una imagen clara de las actividades y cualquier parámetro clave que afecte al procesamiento.</td>
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
Describe las condiciones que indican un error y deben resolverse.<br>
Cuando el registro de ERROR está activo, solo se registran las instrucciones que indican que se han producido errores. Las instrucciones de registro de ERROR indican un problema grave que debe resolverse lo antes posible.</td>
<td>
<ul>
<li> Desarrollo local</li>
<li>Desarrollo</li>
<li>Escenario</li>
<li>Producción</li>
</ul></td>
</tr>
</table>

Aunque el registro de Java admite otros niveles de granularidad de registro, AEM como Cloud Service recomienda usar los tres niveles descritos anteriormente.

AEM Los niveles de registro se establecen por tipo de entorno a través de la configuración OSGi, que a su vez se comprometen con Git, y se implementan a través de Cloud Manager para AEM como Cloud Service. Debido a esto, es mejor mantener las instrucciones de registro coherentes y bien conocidas para los tipos de entorno, para garantizar que los registros disponibles a través de AEM como Cloud Service estén disponibles en el nivel de registro óptimo sin requerir la reimplementación de la aplicación con la configuración actualizada del nivel de registro.

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
<td>29.4.2020 21:50:13.398</td>
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
<td>No se ha especificado ningún aprobador, el valor predeterminado es [ grupo de usuarios de aprobadores creativos ]</td>
</tr>
</tbody>
</table>

### Registradores de configuración {#configuration-loggers}

AEM los registros Java se definen como configuración OSGi y, por lo tanto, se dirigen a AEM específicos como entornos de Cloud Service mediante carpetas en modo de ejecución.

Configure el registro de Java para paquetes Java personalizados mediante configuraciones OSGi para la fábrica Sling LogManager. Hay dos propiedades de configuración compatibles:

| OSGi Configuration, propiedad | Descripción |
|---|---|
| org.apache.sling.commons.log.names | Los paquetes Java para los que se recopilan las instrucciones de registro. |
| org.apache.sling.commons.log.level | El nivel de registro en el que se deben registrar los paquetes Java, especificado por org.apache.sling.commons.log.names |

Cambiar otras propiedades de configuración de LogManager OSGi puede dar como resultado problemas de disponibilidad en AEM como Cloud Service.

A continuación se muestran algunos ejemplos de las configuraciones de registro recomendadas (con el paquete Java del marcador de posición `com.example`) para los tres AEM como tipos de entorno de Cloud Service.

### Desarrollo {#development}

/apps/my-app/config/org.apache.sling.commons.log.LogManager.factory.config-example.cfg.json

```
{
    "org.apache.sling.commons.log.names": ["com.example"],
    "org.apache.sling.commons.log.level": "debug"
}
```

### Escenario {#stage}

/apps/my-app/config.stage/org.apache.sling.commons.log.LogManager.factory.config-example.cfg.json

```
{
    "org.apache.sling.commons.log.names": ["com.example"],
    "org.apache.sling.commons.log.level": "warn"
}
```

### Producción {#productiomn}

/apps/my-app/config.prod/org.apache.sling.commons.log.LogManager.factory.config-example.cfg.json

```
{
    "org.apache.sling.commons.log.names": ["com.example"],
    "org.apache.sling.commons.log.level": "error"
}
```

## Registro de solicitudes HTTP AEM {#aem-http-request-logging}

AEM como registro de solicitud HTTP de un Cloud Service proporciona una perspectiva de las solicitudes HTTP realizadas a AEM y sus respuestas HTTP en orden temporal. Este registro es útil para comprender las solicitudes HTTP realizadas a AEM y el orden en que se procesan y responden.

La clave para comprender este registro es asignar los pares de solicitud y respuesta HTTP por sus ID, marcados con el valor numérico entre corchetes. Tenga en cuenta que a menudo las solicitudes y sus respuestas correspondientes tienen otras solicitudes HTTP y respuestas insertadas entre ellas en el registro.

**Registro de ejemplos**

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
<td>ID del par de solicitud/respuesta</td>
<td><code>[137]</code></td>
</tr>
<tr>
<td>Método HTTP</td>
<td>POST</td>
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
<td>AEM como ID de nodo de Cloud Service</td>
<td>[cm-p1234-e5678-aem-author-59555cb5b8-q7l9s]</td>
</tr>
</tbody>
</table>

### Configuración del registro {#configuring-the-log}

El registro de solicitud HTTP de AEM no se puede configurar en AEM como Cloud Service.

## Registro de acceso HTTP AEM {#aem-http-access-logging}

AEM como Cloud Service, el registro de acceso HTTP muestra las solicitudes HTTP en orden temporal. Cada entrada de registro representa la solicitud HTTP a la que se accede AEM.

Este registro es útil para comprender rápidamente a qué solicitudes HTTP se están realizando AEM, si tienen éxito consultando el código de estado de respuesta HTTP que lo acompaña y cuánto tiempo tardó la solicitud HTTP en completarse. Este registro también puede resultar útil para depurar la actividad de un usuario específico filtrando las entradas de registro por parte de los usuarios.

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
<td>método HTTP</td>
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
<td>"Mozilla/5.0 (Macintosh); Intel Mac OS X 10_15_4) AppleWebKit/537.36 (KHTML, como Gecko) Chrome/81.0.4044.122 Safari/537.36"</td>
</tr>
</tbody>
</table>

### Configuración del registro de acceso HTTP {#configuring-the-http-access-log}

El registro de acceso HTTP no se puede configurar en AEM como Cloud Service.

## Registro de Apache Web Server y Dispatcher {#apache-web-server-and-dispatcher-logging}

AEM as a Cloud Service proporciona tres registros para los servidores web Apache y la capa de Dispatcher en la publicación:

* Registro de acceso al servidor web Apache HTTPD
* Registro de errores del servidor web Apache HTTPD
* Registro de Dispatcher

Tenga en cuenta que estos registros solo están disponibles para el nivel Publicar .

Este conjunto de registros proporciona perspectivas sobre las solicitudes HTTP al AEM como un nivel de publicación de Cloud Service antes de que dichas solicitudes lleguen a la aplicación de AEM. Esto es importante de comprender, ya que, idealmente, la mayoría de las solicitudes HTTP a los servidores de nivel Publicar están servidas por contenido almacenado en caché por el servidor web Apache HTTPD y AEM Dispatcher, y nunca llegan a la propia aplicación AEM. Por lo tanto, no hay instrucciones de registro para estas solicitudes en AEM registros de Java, Solicitud o Acceso.

### Registro de acceso al servidor web Apache HTTPD {#apache-httpd-web-server-access-log}

El registro de acceso al servidor web HTTP Apache proporciona instrucciones para cada solicitud HTTP que llega al servidor web o Dispatcher del nivel de publicación. Tenga en cuenta que las solicitudes que se proporcionan desde una CDN de flujo ascendente no se reflejan en estos registros.

Consulte información sobre el formato de registro de errores en la [documentación oficial de Apache](https://httpd.apache.org/docs/2.4/logs.html#accesslog).

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
<td>ID de nodo de AEM as a Cloud Service</td>
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
<td>1/Mayo/2020:00:09:46 +000</td>
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
<td>Referer</td>
<td>-</td>
</tr>
<tr>
<td>Agente de usuario</td>
<td>"Mozilla/5.0 (Macintosh); Intel Mac OS X 10_15_4) AppleWebKit/537.36 (KHTML, como Gecko) Chrome/81.0.4044.122 Safari/537.36"</td>
</tr>
</tbody>
</table>

### Configuración del registro de acceso al servidor web Apache HTTPD {#configuring-the-apache-httpd-webs-server-access-log}

Este registro no se puede configurar en AEM como Cloud Service.

## Registro de errores del servidor web Apache HTTPD {#apache-httpd-web-server-error-log}

El registro de errores del servidor web HTTP Apache proporciona instrucciones para cada error en el servidor web o Dispatcher del nivel de publicación.

Consulte información sobre el formato de registro de errores en la [documentación oficial de Apache](https://httpd.apache.org/docs/2.4/logs.html#errorlog).

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
<td>viernes 17 de julio de 2020:16:42.608913</td>
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
<td>Nombre de la secuencia</td>
<td>[cm-p1234-e56789-aem-publish-b86c6b466-qpfvp]</td>
</tr>
<tr>
<td>Mensaje</td>
<td>AH00094: Línea de comandos: 'httpd -d /etc/httpd -f /etc/httpd/conf/httpd.conf -D FOREGROUND -D </td>
</tr>
</tbody>
</table>

### Configuración del registro de errores del servidor web Apache HTTPD {#configuring-the-apache-httpd-web-server-error-log}

Los niveles de registro mod_rewrite se definen mediante la variable REWRITE_LOG_LEVEL en el archivo `conf.d/variables/global.var`.

Puede configurarse como Error, Advertencia, Información, Depuración y Trace1 - Trace8, con un valor predeterminado de Advertencia. Para depurar las reglas de reescritura, se recomienda elevar el nivel de registro a Trace2.

Consulte la [documentación del módulo mod_rewrite](https://httpd.apache.org/docs/current/mod/mod_rewrite.html#logging) para obtener más información.

Para establecer el nivel de registro por entorno, utilice la rama condicional adecuada en el archivo global.var , como se describe a continuación:

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
<td>[17/Julio/2020:23:48:16 +0000]</td>
</tr>
<tr>
<td>Nombre de la secuencia</td>
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
<td>[publishfarm/0]</td>
</tr>
<tr>
<td>Estado de caché</td>
<td>[omisión de acción]</td>
</tr>
<tr>
<td>Host</td>
<td>"publish-p12904-e25628.adobeaemcloud.com"</td>
</tr>
</tbody>
</table>

### Configuración del registro de errores de Dispatcher {#configuring-the-dispatcher-error-log}

Los niveles de registro de Dispatcher se definen mediante la variable DISP_LOG_LEVEL en el archivo `conf.d/variables/global.var`.

Puede configurarse como Error, Advertencia, Información, Depuración y Seguimiento1, con el valor predeterminado Advertencia.

Aunque el registro de Dispatcher admite otros niveles de granularidad de registro, el AEM como Cloud Service recomienda utilizar los niveles que se describen a continuación.

Para establecer el nivel de registro por entorno, utilice la rama condicional adecuada en el archivo `global.var` como se describe a continuación:

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

Se puede acceder a los registros de AEM as a Cloud Service para servicios en la nube descargando a través de la interfaz de Cloud Manager o adaptando los registros en la línea de comandos utilizando la interfaz de línea de comandos de Adobe I/O. Para obtener más información, consulte la [documentación de registro de Cloud Manager](/help/implementing/cloud-manager/manage-logs.md).

### SDK local {#local-sdk}

AEM como Cloud Service SDK proporciona archivos de registro para admitir el desarrollo local.

AEM registros se encuentran en la carpeta `crx-quickstart/logs`, donde se pueden ver los siguientes registros:

* AEM registro de Java: `error.log`
* Registro AEM solicitud HTTP: `request.log`
* Registro AEM acceso HTTP: `access.log`

Los registros de capa de Apache, incluido Dispatcher, se encuentran en el contenedor Docker que alberga el Dispatcher. Consulte la [documentación de Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/content-delivery/disp-overview.html) para obtener información sobre cómo iniciar Dispatcher.

Para recuperar los registros:

1. En la línea de comandos, escriba `docker ps` para enumerar los contenedores
1. Para iniciar sesión en el contenedor, escriba &quot;`docker exec -it <container> /bin/sh`&quot;, donde `<container>` es el identificador del contenedor de Dispatcher del paso anterior
1. Vaya a la raíz de caché en `/mnt/var/www/html`
1. Los registros están en `/etc/httpd/logs`
1. Inspect los registros: se puede acceder a ellas desde la carpeta XYZ, donde se pueden ver los siguientes registros:
   * Registro de acceso al servidor web HTTP de Apache - `httpd_access.log`
   * Registros de errores del servidor web HTTP de Apache: `httpd_error.log`
   * Registros de Dispatcher - `dispatcher.log`

Los registros también se imprimen directamente en la salida de terminal. La mayoría de las veces, estos registros deben ser DEBUG, lo que se puede lograr pasando el nivel de depuración como parámetro al ejecutar Docker. Por ejemplo:

`DISP_LOG_LEVEL=Debug ./bin/docker_run.sh out docker.for.mac.localhost:4503 8080`

## Depuración de producción y ensayo {#debugging-production-and-stage}

En circunstancias excepcionales, es necesario cambiar los niveles de registro para registrar una granularidad más precisa en entornos de fase o producción.

Aunque esto es posible, requiere cambios en los niveles de registro de los archivos de configuración en Git de Advertencia y Error a Depuración, y realizar una implementación en AEM como Cloud Service para registrar estos cambios de configuración con los entornos.

Según el tráfico y la cantidad de instrucciones de registro escritas por Debug, esto puede tener un impacto negativo en el rendimiento del entorno, por lo que se recomienda que los cambios en los niveles de depuración de fase y producción sean:

* Hecho juiciosamente y sólo cuando sea absolutamente necesario
* Se volvió a los niveles adecuados y se volvió a implementar lo antes posible

## Registros de Splunk {#splunk-logs}

Los clientes que tengan cuentas de Splunk pueden solicitar a través de un ticket de asistencia al cliente que sus registros de Cloud Service de AEM se reenvíen al índice correspondiente. Los datos de registro equivalen a lo que está disponible a través de las descargas de registro de Cloud Manager, pero a los clientes les puede resultar conveniente aprovechar las funciones de consulta disponibles en el producto Splunk.

El ancho de banda de red asociado con los registros enviados a Splunk se considera parte del uso de E/S de red del cliente.

### Activación del reenvío de fragmento {#enabling-splunk-forwarding}

En la solicitud de asistencia, los clientes deben indicar:

* Dirección de extremo HEC de Splunk
* Índice de Splunk
* Puerto de Splunk
* El token HEC de Splunk. Consulte [esta página](https://docs.splunk.com/Documentation/Splunk/8.0.4/Data/HECExamples) para obtener más información.

Las propiedades anteriores deben especificarse para cada combinación de programa/tipo de entorno pertinente.  Por ejemplo, si un cliente desea entornos de desarrollo, ensayo y producción, debe proporcionar tres conjuntos de información, como se indica a continuación.

>[!NOTE]
>
>No se admite el reenvío de fragmentos para entornos de programa de entornos limitados.

Debe asegurarse de que la solicitud inicial incluya todos los entornos de desarrollo que deben habilitarse, además de los entornos de ensayo/producción.

Si cualquier nuevo entorno de desarrollo creado después de la solicitud inicial pretende tener el reenvío de Splunk, pero no lo tiene habilitado, se debe realizar una solicitud adicional.

Tenga en cuenta también que si se han solicitado entornos de desarrollo, es posible que otros entornos de desarrollo que no estén en los entornos de solicitud o incluso de simulación de pruebas tengan habilitado el reenvío de Splunk y compartan un índice de Splunk. Los clientes pueden utilizar el campo `aem_env_id` para distinguir entre estos entornos.

A continuación encontrará una muestra de una solicitud de asistencia al cliente:

Programa 123, Env de producción

* Dirección del extremo HEC de Splunk: `splunk-hec-ext.acme.com`
* Índice de fragmento: acme_123prod (el cliente puede elegir la convención de nomenclatura que desee)
* Puerto de Splunk: 443
* Token de HEC de Splunk: ABC123

Programa 123, Etapa Env

* Dirección del extremo HEC de Splunk: `splunk-hec-ext.acme.com`
* Índice de fragmento: acme_123stage
* Puerto de Splunk: 443
* Token de HEC de Splunk: ABC123

Programa 123, desarrolladores

* Dirección del extremo HEC de Splunk: `splunk-hec-ext.acme.com`
* Índice de fragmento: acme_123dev
* Puerto de Splunk: 443
* Token de HEC de Splunk: ABC123

Puede ser suficiente para que se utilice el mismo índice de Splunk para cada entorno, en cuyo caso se puede utilizar el campo `aem_env_type` para diferenciar en función de los valores dev, stage y prod. Si hay varios entornos de desarrollo, también se puede utilizar el campo `aem_env_id` . Algunas organizaciones pueden elegir un índice separado para los registros del entorno de producción si el índice asociado limita el acceso a un conjunto reducido de usuarios de Splunk.

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
