---
title: Registro
description: Obtenga información sobre cómo configurar los parámetros globales para el servicio de registro central, la configuración específica para los servicios individuales o cómo solicitar el registro de datos.
translation-type: tm+mt
source-git-commit: c7100f53ce38cb8120074ec4eb9677fb7303d007
workflow-type: tm+mt
source-wordcount: '873'
ht-degree: 3%

---


# Registro {#logging}

AEM como Cloud Service es una plataforma para que los clientes incluyan código personalizado para crear experiencias únicas para su base de clientes. Teniendo esto en cuenta, el registro es una función crítica para depurar y entender la ejecución del código en el desarrollo local y los entornos de nube, especialmente el AEM como entornos de desarrolladores de Cloud Service.

Los niveles de registro y registro de AEM se administran en archivos de configuración que se almacenan como parte del proyecto de AEM en Git y se implementan como parte del proyecto de AEM mediante Cloud Manager. El inicio de sesión en AEM como Cloud Service se puede dividir en dos conjuntos lógicos:

* Registro de AEM, que realiza el registro en el nivel de aplicación AEM
* El registro de Apache HTTPD Web Server/Dispatcher, que realiza el registro del servidor web y Dispatcher en el nivel de publicación.

## Registro de AEM {#aem-loggin}

El registro en el nivel de aplicación AEM se administra mediante tres registros:

1. Registros de Java de AEM, que representan las sentencias de registro de Java para la aplicación AEM.
1. Registros de solicitudes HTTP, que registran información sobre solicitudes HTTP y sus respuestas servidas por AEM
1. Registros de acceso HTTP, que registran información resumida y solicitudes HTTP servidas por AEM

Tenga en cuenta que las solicitudes HTTP que se envían desde la caché de Dispatcher del nivel de publicación o desde la CDN de flujo ascendente no se reflejan en estos registros.

## Registro de Java AEM {#aem-java-logging}

AEM como Cloud Service proporciona acceso a las sentencias de registro de Java. Los desarrolladores de aplicaciones para AEM deben seguir las optimizaciones generales de registro de Java, registrando afirmaciones pertinentes sobre la ejecución de código personalizado, en los siguientes niveles de registro:

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

AEM Los niveles de registro se establecen por tipo de entorno mediante la configuración OSGi, que a su vez se asignan a Git, y se implementan mediante Cloud Manager para AEM como Cloud Service. Debido a esto, lo mejor es mantener las declaraciones de registro coherentes y bien conocidas para los tipos de entornos, a fin de garantizar que los registros disponibles a través de AEM, como Cloud Service, estén disponibles en el nivel de registro óptimo sin necesidad de reimplementar la aplicación con la configuración de nivel de registro actualizada.

### Formato de registro {#log-format}

| Fecha y hora | AEM como ID de dode Cloud Service | Nivel de registro | Subproceso | Clase Java | Mensaje de registro |
|---|---|---|---|---|---|
| 29.04.2020 21:50:13.398 | `[cm-p1234-e5678-aem-author-59555cb5b8-q7l9s]` | `*DEBUG*` | qtp2130572036-1472 | com.example.approval.workflow.impl.CustomApprovalWorkflow | No se ha especificado ningún aprobador, de forma predeterminada el grupo de usuarios Aprobadores creativos [ ] |

**Ejemplo de salida de registro**

`22.06.2020 18:33:30.120 [cm-p12345-e6789-aem-author-86657cbb55-xrnzq] *ERROR* [qtp501076283-1809] io.prometheus.client.dropwizard.DropwizardExports Failed to get value from Gauge`
`22.06.2020 18:33:30.229 [cm-p12345-e6789-aem-author-86657cbb55-xrnzq] *INFO* [qtp501076283-1805] org.apache.sling.auth.core.impl.SlingAuthenticator getAnonymousResolver: Anonymous access not allowed by configuration - requesting credentials`
`22.06.2020 18:33:30.370 [cm-p12345-e6789-aem-author-86657cbb55-xrnzq] *INFO* [73.91.59.34 [1592850810364] GET /libs/granite/core/content/login.html HTTP/1.1] org.apache.sling.i18n.impl.JcrResourceBundle Finished loading 0 entries for 'en_US' (basename: <none>) in 4ms`
`22.06.2020 18:33:30.372 [cm-p12345-e6789-aem-author-86657cbb55-xrnzq] *INFO* [FelixLogListener] org.apache.sling.i18n Service [5126, [java.util.ResourceBundle]] ServiceEvent REGISTERED`
`22.06.2020 18:33:30.372 [cm-p12345-e6789-aem-author-86657cbb55-xrnzq] *WARN* [73.91.59.34 [1592850810364] GET /libs/granite/core/content/login.html HTTP/1.1] libs.granite.core.components.login.login$jsp j_reason param value 'unknown' cannot be mapped to a valid reason message: ignoring`

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

### Formato de registro {#http-request-logging-format}

| Fecha y hora | Id. de pares de solicitud/respuesta |  | Método HTTP | URL | Protocolo | AEM como ID de nodo de Cloud Service |
|---|---|---|---|---|---|---|
| 29/Abr/2020:19:14:21 +0000 | `[137]` | -> | POST | /conf/global/settings/dam/adminui-extension/metadata aprofile/ | HTTP/1.1 | `[cm-p1234-e5678-aem-author-59555cb5b8-q7l9s]` |

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

### Configuración del registro {#configuring-the-log}

El registro de solicitud HTTP AEM no se puede configurar en AEM como Cloud Service.

## Registro de acceso HTTP AEM {#aem-http-access-logging}

AEM como registro de acceso HTTP Cloud Service muestra las solicitudes HTTP en orden temporal. Cada entrada de registro representa la solicitud HTTP que accede a AEM.

Este registro es útil para comprender rápidamente qué solicitudes HTTP se están realizando a AEM, si tienen éxito al consultar el código de estado de respuesta HTTP correspondiente y cuánto tiempo tardó en completarse la solicitud HTTP. Este registro también puede resultar útil para depurar la actividad de un usuario específico filtrando las entradas de registro por usuarios.

### Formato de registro {#access-log-format}
