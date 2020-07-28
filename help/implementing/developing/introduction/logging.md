---
title: Registro
description: Obtenga información sobre cómo configurar los parámetros globales para el servicio de registro central, la configuración específica para los servicios individuales o cómo solicitar el registro de datos.
translation-type: tm+mt
source-git-commit: a7c8e1ab8e0196a3a79d8e0963192775e64a2400
workflow-type: tm+mt
source-wordcount: '386'
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

### Registro de Java AEM {#aem-java-logging}

AEM como Cloud Service proporciona acceso a las sentencias de registro de Java. Los desarrolladores de aplicaciones para AEM deben seguir las optimizaciones generales de registro de Java, registrando afirmaciones pertinentes sobre la ejecución de código personalizado, en los siguientes niveles de registro:

<table>
<tbody>
<tr>
<td> <b>Entorno AEM</b></td>
<td> <b>Nivel de registro</b></td>
<td> <b>Descripción</b></td>
<td> <b>Disponibilidad de estado de registro</b></td>
</tr>
<tr>
<td> Desarrollo</td>
<td> DEPURACIONES</td>
<td> Describe lo que sucede en la aplicación.

Cuando el registro DEBUG está activo, se registran las instrucciones que proporcionan una imagen clara de las actividades que se producen, así como los parámetros clave que afectan al procesamiento.</td>
<td> <ul>
<li> Desarrollo local</li>
<li>Desarrollo</li>
</ul></td>
</tr>
<tr>
<td> Escenario</td>
<td> AVISAR</td>
<td> Describe las condiciones que pueden convertirse en errores.

Cuando el registro de WARN está activo, solo se registran las afirmaciones que indican condiciones que se acercan a la suboptimización.</td>
<td> <ul>
<li> Desarrollo local</li>
<li>Desarrollo</li>
<li>Escenario</li>
</ul></td>
</tr>
<tr>
<td> Producción</td>
<td> ERROR</td>
<td> Describe las condiciones que indican un error y deben resolverse.

Cuando el registro de ERROR está activo, solo se registran las sentencias que indican errores. Las instrucciones del registro de errores indican un problema grave que debe resolverse lo antes posible.</td>
<td> <ul>
<li> Desarrollo local</li>
<li>Desarrollo</li>
<li>Escenario</li>
<li>Producción</li>
</ul></td>
</tr>
</tbody>
</table>