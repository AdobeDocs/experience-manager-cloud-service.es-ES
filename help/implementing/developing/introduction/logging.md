---
title: AEM Registro para la as a Cloud Service
description: AEM Obtenga información sobre cómo utilizar Registro para el registro as a Cloud Service para configurar parámetros globales para el servicio de registro central, ajustes específicos para los servicios individuales o cómo solicitar el registro de datos.
exl-id: 262939cc-05a5-41c9-86ef-68718d2cd6a9
source-git-commit: 1994b90e3876f03efa571a9ce65b9fb8b3c90ec4
workflow-type: tm+mt
source-wordcount: '2375'
ht-degree: 4%

---

# AEM Registro para la as a Cloud Service {#logging-for-aem-as-a-cloud-service}

AEM as a Cloud Service es una plataforma para que los clientes incluyan código personalizado para crear experiencias únicas para su base de clientes. AEM Teniendo esto en cuenta, el servicio de registro es una función esencial para depurar y comprender la ejecución de código en entornos de desarrollo local y en la nube, especialmente en los entornos de desarrollo del as a Cloud Service de la nube, en particular los entornos de desarrollo de la aplicación.

AEM La configuración del registro as a Cloud Service AEM AEM y los niveles de registro se administran en archivos de configuración que se almacenan como parte del proyecto de la en Git y se implementan como parte del proyecto de la a través de Cloud Manager. AEM El inicio de sesión en el as a Cloud Service de la se puede dividir en dos conjuntos lógicos:

* AEM AEM registro de datos, que realiza el registro en el nivel de aplicación de la
* Registro de Apache HTTPD Web Server/Dispatcher, que realiza el registro del servidor web y Dispatcher en el nivel de publicación.

## AEM Registro de {#aem-logging}

AEM El inicio de sesión en el nivel de aplicación de la se gestiona mediante tres registros:

1. AEM AEM Registros de Java, que procesan las sentencias de registro de Java para la aplicación de.
1. AEM Registros de solicitudes HTTP, que registran información sobre las solicitudes HTTP y sus respuestas proporcionadas por los usuarios de la red de servicios de correo electrónico
1. AEM Registros de acceso HTTP, que registran la información resumida y las solicitudes HTTP servidas por los usuarios de la red de servicios de datos de

>[!NOTE]
>
>Las solicitudes HTTP servidas desde la caché de Dispatcher del nivel de publicación o la CDN ascendente no se reflejan en estos registros.

## AEM Registro de Java de {#aem-java-logging}

AEM El de as a Cloud Service proporciona acceso a las sentencias de registro de Java. AEM Los desarrolladores de aplicaciones para la deben seguir las prácticas recomendadas generales de registro de Java, registrando las instrucciones pertinentes acerca de la ejecución del código personalizado, en los siguientes niveles de registro:

<table>
<tr>
<td>
<b>AEM Entorno</b></td>
<td>
<b>Nivel de registro</b></td>
<td>
<b>Descripción</b></td>
<td>
<b>Disponibilidad de extracto de registro</b></td>
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

AEM Aunque el registro de Java admite varios niveles más de granularidad de registro, el as a Cloud Service de la recomienda utilizar los tres niveles descritos anteriormente.

AEM AEM Los niveles de registro se establecen por tipo de entorno a través de la configuración de OSGi, que a su vez se comprometen con Git e implementan mediante Cloud Manager para que se puedan configurar en as a Cloud Service. AEM Debido a esto, es mejor mantener las instrucciones de registro coherentes y bien conocidas para los tipos de entorno para garantizar que los registros disponibles a través de como Cloud Service estén disponibles en el nivel de registro óptimo sin requerir una reimplementación de la aplicación con la configuración de nivel de registro actualizada.

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
<td>AEM ID de nodo as a Cloud Service</td>
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
<td>No se ha especificado un aprobador, se establece de forma predeterminada [ grupo de usuarios de aprobadores creativos ]</td>
</tr>
</tbody>
</table>

### Registradores de configuración {#configuration-loggers}

AEM AEM Los registros de Java se definen como la configuración OSGi y, por lo tanto, se dirigen a entornos as a Cloud Service específicos mediante carpetas en modo de ejecución.

Configure el registro java para paquetes Java personalizados mediante las configuraciones OSGi para la fábrica de Sling LogManager. Hay dos propiedades de configuración admitidas:

| Propiedad de configuración OSGi | Descripción |
|---|---|
| org.apache.sling.commons.log.names | Los paquetes Java para los que se recopilan instrucciones de registro. |
| org.apache.sling.commons.log.level | Nivel de registro en el que se registran los paquetes Java, especificado por org.apache.sling.commons.log.names |

AEM El cambio de otras propiedades de configuración de LogManager OSGi puede provocar problemas de disponibilidad en los as a Cloud Service de la.

A continuación se muestran ejemplos de las configuraciones de registro recomendadas (con el paquete Java de marcador de posición de ) `com.example`AEM ) para los tres tipos de entorno as a Cloud Service de la.

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

## AEM Registro de solicitud HTTP de {#aem-http-request-logging}

AEM as a Cloud Service AEM El registro de solicitudes HTTP de proporciona una perspectiva de las solicitudes HTTP realizadas a los clientes y sus respuestas HTTP en orden de tiempo. AEM Este registro es útil para comprender las solicitudes HTTP realizadas a y el orden en el que se procesan y responden a las que se realizan las solicitudes.

La clave para comprender este registro es asignar los pares de solicitud y respuesta HTTP por sus ID, indicados por el valor numérico entre corchetes. Tenga en cuenta que, a menudo, las solicitudes de y sus respuestas correspondientes tienen otras solicitudes HTTP y respuestas interconectadas entre ellas en el registro.

**Ejemplo de registro**

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
<td>29/abr/2020:19:14:21 +0000</td>
</tr>
<tr>
<td>ID de par de solicitud/respuesta</td>
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
<td>AEM ID de nodo as a Cloud Service</td>
<td>[cm-p1234-e5678-aem-author-59555cb5b8-q7l9s]</td>
</tr>
</tbody>
</table>

### Configuración del registro {#configuring-the-log}

AEM AEM El registro de petición HTTP de la no se puede configurar en as a Cloud Service de la.

## AEM Registro de acceso HTTP de {#aem-http-access-logging}

AEM Como Cloud Service, el registro de acceso HTTP muestra las solicitudes HTTP en orden temporal. AEM Cada entrada de registro representa la petición HTTP que accede a las entradas de la página de acceso a la página de la página de.

AEM Este registro es útil para comprender rápidamente qué solicitudes HTTP se realizan a los clientes, si se realizan correctamente consultando el código de estado de respuesta HTTP que las acompaña y cuánto tiempo tardó la solicitud HTTP en completarse. Este registro también puede resultar útil para depurar la actividad de un usuario específico filtrando las entradas de registro por usuarios.

**Ejemplo de salida de registro**

```
cm-p1234-e26813-aem-author-59555cb5b8-8kgr2 - example@adobe.com 30/Apr/2020:17:37:14 +0000  "GET /libs/granite/ui/references/clientlibs/references.lc-5188e85840c529149e6cd29d94e74ad5-lc.min.css HTTP/1.1" 200 1141 "https://author-p10711-e26813.adobeaemcloud.com/mnt/overlay/dam/gui/content/assets/metadataeditor.external.html?item=/content/dam/en/images/example.jpeg&_charset_=utf8" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_4) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/81.0.4044.122 Safari/537.36"
cm-p1234-e26813-aem-author-59555cb5b8-8kgr2 - example@adobe.com 30/Apr/2020:17:37:14 +0000  "GET /libs/dam/gui/coral/components/admin/customthumb/clientlibs.lc-60e4443805c37afa0c74b674b141f1df-lc.min.css HTTP/1.1" 200 809 "https://author-p10711-e26813.adobeaemcloud.com/mnt/overlay/dam/gui/content/assets/metadataeditor.external.html?item=/content/dam/en/images/example.jpeg&_charset_=utf8" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_4) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/81.0.4044.122 Safari/537.36"
cm-p1234-e26813-aem-author-59555cb5b8-8kgr2 - example@adobe.com 30/Apr/2020:17:37:14 +0000  "GET /libs/dam/gui/coral/components/admin/metadataeditor/clientlibs/metadataeditor.lc-4a2226d8232f8b7ab27d24820b9ddd64-lc.min.js HTTP/1.1" 200 7965 "https://author-p10711-e26813.adobeaemcloud.com/mnt/overlay/dam/gui/content/assets/metadataeditor.external.html?item=/content/dam/en/images/example.jpeg&_charset_=utf8" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_4) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/81.0.4044.122 Safari/537.36"
```

| AEM ID de nodo as a Cloud Service | cm-p1235-e2644-aem-author-59555cb5b8-8kgr2 |
|---|---|
| Dirección IP del cliente | - |
| Usuario | myuser@adobe.com |
| Fecha y hora | 30/abr/2020:17:37:14 +0000 |
| método HTTP | GET |
| URL | `/libs/granite/ui/references/clientlibs/references.lc-5188e85840c529149e6cd29d94e74ad5-lc.min.css` |
| Protocolo | HTTP/1.1 |
| Estado de respuesta HTTP | 200 |
| Tamaño del cuerpo de respuesta en bytes | 1141 |
| Referencia | `"https://author-p1234-e4444.adobeaemcloud.com/mnt/overlay/dam/gui/content/assets/metadataeditor.external.html?item=/content/dam/wknd/en/adventures/surf-camp-in-costa-rica/adobestock_266405335.jpeg&_charset_=utf8"` |
| Agente de usuario | `"Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_4) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/81.0.4044.122 Safari/537.36"` |

### Configuración del registro de acceso HTTP {#configuring-the-http-access-log}

AEM El registro de acceso HTTP no se puede configurar en el as a Cloud Service de la.

## Registro de Apache Web Server y Dispatcher {#apache-web-server-and-dispatcher-logging}

AEM as a Cloud Service proporciona tres registros para los servidores web Apache y la capa de Dispatcher en el entorno de publicación:

* Registro de acceso al servidor web Apache HTTPD
* Registro de errores del servidor web Apache HTTPD
* Registro de Dispatcher

Tenga en cuenta que estos registros solo están disponibles para el nivel de publicación.

AEM Este conjunto de registros proporciona información sobre las solicitudes HTTP al nivel de publicación as a Cloud Service AEM de la antes de que dichas solicitudes lleguen a la aplicación de la. AEM AEM Esto es importante tenerlo en cuenta, ya que, idealmente, la mayoría de las solicitudes HTTP a los servidores de nivel de publicación están servidas por contenido que está almacenado en caché por el servidor web Apache HTTPD y Dispatcher, y nunca llegan a la aplicación en sí misma. AEM Por lo tanto, no hay instrucciones de registro para estas solicitudes en los registros de Java, Solicitud o Acceso de la.

### Registro de acceso al servidor web Apache HTTPD {#apache-httpd-web-server-access-log}

El registro de acceso del servidor web HTTP Apache proporciona instrucciones para cada solicitud HTTP que llega al servidor web/Dispatcher del nivel de publicación. Tenga en cuenta que las solicitudes servidas desde una CDN ascendente no se reflejan en estos registros.

Consulte la información sobre el formato del registro de errores en la [documentación oficial de apache](https://httpd.apache.org/docs/2.4/logs.html#accesslog).

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
<td>AEM ID de nodo de as a Cloud Service</td>
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
<td>1/mayo/2020:00:09:46 +0000</td>
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
<td>"Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_4) AppleWebKit/537.36 (KHTML, como Gecko) Chrome/81.0.4044.122 Safari/537.36"</td>
</tr>
</tbody>
</table>

### Configuración del registro de acceso del servidor web Apache HTTPD {#configuring-the-apache-httpd-webs-server-access-log}

AEM Este registro no se puede configurar en el as a Cloud Service de.

## Registro de errores del servidor web Apache HTTPD {#apache-httpd-web-server-error-log}

El registro de errores del servidor web HTTP Apache proporciona instrucciones para cada error en el servidor web/Dispatcher del nivel de publicación.

Consulte la información sobre el formato del registro de errores en la [documentación oficial de apache](https://httpd.apache.org/docs/2.4/logs.html#errorlog).

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
<td>Vie jul 17 02:16:42.608913 2020</td>
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

La variable REWRITE_LOG_LEVEL del archivo define los niveles de registro mod_rewrite `conf.d/variables/global.var`.

Se puede establecer en error, warn, info, debug y trace1 - trace8, con un valor predeterminado de warn. Para depurar RewriteRules, se recomienda elevar el nivel de registro a trace2.

Consulte la [Documentación del módulo mod_rewrite](https://httpd.apache.org/docs/current/mod/mod_rewrite.html#logging) para obtener más información.

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
<td>[17/jul/2020]:23:48:16 +0000]</td>
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
<td>Código de estado de respuesta del Dispatcher</td>
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
<td>[falta de acción]</td>
</tr>
<tr>
<td>Host</td>
<td>"publish-p12904-e25628.adobeaemcloud.com"</td>
</tr>
</tbody>
</table>

### Configuración del registro de errores de Dispatcher {#configuring-the-dispatcher-error-log}

Los niveles de registro de Dispatcher se definen mediante la variable DISP_LOG_LEVEL en el archivo `conf.d/variables/global.var`.

Se puede establecer en error, warn, info, debug y trace1, con un valor predeterminado de warn.

AEM Aunque el registro de Dispatcher admite varios niveles más de granularidad de registro, el as a Cloud Service recomienda utilizar los niveles que se describen a continuación.

Para establecer el nivel de registro por entorno, utilice la rama condicional adecuada en la variable `global.var` , tal como se describe a continuación:

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
>AEM Para entornos as a Cloud Service, la depuración es el nivel de detalle máximo. El nivel de registro de seguimiento no es compatible, por lo que debe evitar configurarlo cuando trabaje en entornos de nube.

## Cómo acceder a los registros {#how-to-access-logs}

### Entornos de la nube {#cloud-environments}

AEM Se puede acceder a los registros as a Cloud Service para los servicios en la nube mediante la descarga a través de la interfaz de Cloud Manager o siguiendo los registros en la línea de comandos utilizando la interfaz de línea de comandos de Adobe I/O. Para obtener más información, consulte la [Documentación de registro de Cloud Manager](/help/implementing/cloud-manager/manage-logs.md).

### El SDK local {#local-sdk}

AEM El SDK as a Cloud Service de proporciona archivos de registro para admitir el desarrollo local.

AEM Los registros de se encuentran en la carpeta `crx-quickstart/logs`, donde se pueden ver los siguientes registros:

* AEM Registro de Java de: `error.log`
* AEM Registro de petición HTTP: `request.log`
* AEM Registro de acceso HTTP de: `access.log`

Los registros de capa de Apache, incluido Dispatcher, están en el contenedor Docker que contiene Dispatcher. Consulte la [Documentación de Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/content-delivery/disp-overview.html?lang=es) para obtener información sobre cómo iniciar Dispatcher.

Para recuperar los registros:

1. En la línea de comandos, escriba `docker ps` para enumerar los contenedores
1. Para iniciar sesión en el contenedor, escriba &quot;`docker exec -it <container> /bin/sh`&quot;, donde `<container>` es el id del contenedor de Dispatcher del paso anterior
1. Vaya a la raíz de caché en `/mnt/var/www/html`
1. Los registros se encuentran en `/etc/httpd/logs`
1. Inspect los registros: se puede acceder a ellos en la carpeta XYZ, donde se pueden ver los siguientes registros:
   * Registro de acceso al servidor web Apache HTTPD - `httpd_access.log`
   * Registros de errores del servidor web Apache HTTPD - `httpd_error.log`
   * Registros de Dispatcher - `dispatcher.log`

Los registros también se imprimen directamente en la salida de terminal. La mayoría de las veces, estos registros deben ser DEBUG, lo que se puede lograr pasando el nivel de Depuración como parámetro al ejecutar Docker. Por ejemplo:

`DISP_LOG_LEVEL=Debug ./bin/docker_run.sh out docker.for.mac.localhost:4503 8080`

## Depuración de producción y ensayo {#debugging-production-and-stage}

En circunstancias excepcionales, es necesario cambiar los niveles de registro para que registren con una granularidad más precisa en los entornos de Ensayo o Producción.

AEM Aunque esto es posible, se requieren cambios en los niveles de registro en los archivos de configuración en Git de Advertir y error a depurar y realizar una implementación a la que se le asigne un as a Cloud Service para registrar estos cambios de configuración con los entornos de.

Según el tráfico y la cantidad de instrucciones de registro escritas por Debug, esto puede afectar negativamente al rendimiento del entorno, por lo que se recomienda realizar cambios en los niveles de depuración de Ensayo y Producción:

* Hecho con prudencia, y solo cuando sea absolutamente necesario
* Volver a los niveles adecuados y volver a implementarlos lo antes posible

## Registros de Splunk {#splunk-logs}

Los clientes que tengan cuentas de Splunk pueden solicitar a través del ticket de asistencia al cliente que sus registros de AEM Cloud Service se reenvíen al índice adecuado. Los datos de registro son equivalentes a los que están disponibles a través de las descargas de registro de Cloud Manager, pero los clientes pueden encontrar conveniente utilizar las funciones de consulta disponibles en el producto Splunk.

El ancho de banda de red asociado con los registros enviados a Splunk se considera parte del uso de E/S de red del cliente.

### Activación del reenvío de Splunk {#enabling-splunk-forwarding}

En la solicitud de soporte, los clientes deben indicar:

* Dirección de extremo HEC de Splunk. Este extremo debe tener un certificado SSL válido y ser de acceso público.
* El índice de Splunk
* El puerto de Splunk
* El token de HEC de Splunk. Consulte [esta página](https://docs.splunk.com/Documentation/Splunk/8.0.4/Data/HECExamples) para obtener más información.

Las propiedades anteriores deben especificarse para cada combinación de programa/tipo de entorno relevante. Por ejemplo, si un cliente desea entornos de desarrollo, ensayo y producción, debe proporcionar tres conjuntos de información, como se indica a continuación.

>[!NOTE]
>
>No se admite el reenvío de Splunk para entornos de programa de zona protegida.

>[!NOTE]
>
>La capacidad de reenvío de Splunk no es posible desde una dirección IP de salida dedicada.

Debe asegurarse de que la solicitud inicial incluya todos los entornos de desarrollo que deben habilitarse, además de los entornos de ensayo/producción. Splunk debe tener un certificado SSL y ser de acceso público.

Si algún entorno de desarrollo nuevo creado después de la solicitud inicial pretende tener el reenvío de Splunk, pero no lo tiene habilitado, se debe realizar una solicitud adicional.

Tenga en cuenta también que si se han solicitado entornos de desarrollo, es posible que otros entornos de desarrollo que no están en la solicitud o incluso entornos de zona protegida tengan habilitado el reenvío de Splunk y compartan un índice de Splunk. Los clientes pueden utilizar el `aem_env_id` para distinguir entre estos entornos.

A continuación encontrará un ejemplo de solicitud de asistencia al cliente:

Programa 123, Sobre de producción

* Dirección de extremo HEC de Splunk: `splunk-hec-ext.acme.com`
* Índice de Splunk: acme_123prod (el cliente puede elegir la convención de nombres que desee)
* Puerto de Splunk: 443
* Token HEC de Splunk: ABC123

Programa 123, Fase Env

* Dirección de extremo HEC de Splunk: `splunk-hec-ext.acme.com`
* Índice de Splunk: acme_123stage
* Puerto de Splunk: 443
* Token HEC de Splunk: ABC123

Programa 123, Env de desarrollo

* Dirección de extremo HEC de Splunk: `splunk-hec-ext.acme.com`
* Índice de Splunk: acme_123dev
* Puerto de Splunk: 443
* Token HEC de Splunk: ABC123

Puede ser suficiente con que se utilice el mismo índice de Splunk para cada entorno, en cuyo caso ya sea la variable `aem_env_type` El campo se puede utilizar para diferenciar según los valores dev, stage y prod. Si hay varios entornos de desarrollo, la variable `aem_env_id` también se puede utilizar este campo. Algunas organizaciones pueden elegir un índice independiente para los registros del entorno de producción si el índice asociado limita el acceso a un conjunto reducido de usuarios de Splunk.

Este es un ejemplo de entrada de registro:

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
