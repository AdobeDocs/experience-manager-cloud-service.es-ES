---
title: API de configuración OSGi
description: AEM Descripción de la superficie de configuración de OSGi as a Cloud Service de la
feature: Deploying
exl-id: 94d3df65-71d7-4442-8412-fe2cca7e79ff
source-git-commit: cba6648d7ef18f3cccbd9562f3a66d9c683ae852
workflow-type: tm+mt
source-wordcount: '410'
ht-degree: 3%

---

# API de configuración OSGi

AEM Las dos listas siguientes reflejan la superficie de configuración as a Cloud Service de OSGi, describiendo lo que los clientes pueden configurar.

1. Una lista de configuraciones de OSGi que el código de cliente no debe configurar
1. Una lista de configuraciones de OSGi cuyas propiedades pueden configurarse, pero deben cumplir las reglas de validación indicadas. Estas reglas incluyen si la declaración de la propiedad es obligatoria, su tipo y, en algunos casos, su intervalo permitido de valores.

Si la configuración de OSGI no aparece en la lista, puede configurarse mediante el código de cliente.

Estas reglas se validan durante el proceso de compilación de Cloud Manager. Con el tiempo se pueden añadir reglas adicionales y la fecha de aplicación esperada se indica en la tabla. Se espera que los clientes cumplan estas reglas en la fecha objetivo de aplicación. Si no se respetan las reglas después de la fecha de eliminación, se generan errores en el proceso de generación de Cloud Manager. Los proyectos de Maven deben incluir [AEM Complemento Maven de SDK Build Analyzer as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/build-analyzer-maven-plugin.html?lang=es) para marcar los errores de configuración de OSGI durante el desarrollo local del SDK.

Puede encontrar información adicional sobre la configuración de OSGI en [esta ubicación](/help/implementing/deploying/configuring-osgi.md).

## Configuraciones de OSGi que no se pueden modificar {#osgi-configurations-that-cannot-be-modified}

* **`org.apache.felix.webconsole.internal.servlet.OsgiManager`** (Fecha de anuncio: 30/4/2021, fecha de aplicación: 31/7/2021)
* **`com.day.cq.auth.impl.cug.CugSupportImpl`** (Fecha de anuncio: 30/4/2021, fecha de aplicación: 31/7/2021)
* **`com.day.cq.jcrclustersupport.ClusterStartLevelController`** (Fecha de anuncio: 30/4/2021, fecha de aplicación: 31/7/2021)
* **`org.apache.felix.http (Factory)`** (Fecha de anuncio: 30/4/2021, fecha de aplicación: 31/7/2021)
* **`org.apache.sling.jcr.davex.impl.servlets.SlingDavExServlet`** (Fecha de anuncio: 25/8/2021, fecha de aplicación: 26/11/2021)

## Las configuraciones de OSGi están sujetas a reglas de validación de compilación {#osgi-configurations-subject-to-build-validation-rules}

* **`org.apache.felix.eventadmin.impl.EventAdmin`** (Fecha de anuncio: 30/4/2021, fecha de aplicación: 31/7/2021)
   * `org.apache.felix.eventadmin.ThreadPoolSize`
      * Tipo: entero
      * Intervalo requerido: 2-100
   * `org.apache.felix.eventadmin.AsyncToSyncThreadRatio`
      * Tipo: doble
   * `org.apache.felix.eventadmin.Timeout`
      * Tipo: entero
   * `org.apache.felix.eventadmin.RequireTopic`
      * Tipo: booleano
   * `org.apache.felix.eventadmin.IgnoreTimeout`
      * Requerido
      * Tipo: matriz de cadenas
      * Intervalo requerido: debe incluir al menos todos los `org.apache.felix*`, `org.apache.sling*`, `come.day*`, `com.adobe*`
   * `org.apache.felix.eventadmin.IgnoreTopic`
      * Tipo: matriz de cadenas
* **`org.apache.felix.http`** (Fecha de anuncio: 30/4/2021, fecha de aplicación: 31/7/2021)
   * `org.apache.felix.http.timeout`
      * Tipo: entero
   * `org.apache.felix.http.session.timeout`
      * Tipo: entero
   * `org.apache.felix.http.jetty.threadpool.max`
      * Tipo: entero
   * `org.apache.felix.http.jetty.headerBufferSize`
      * Tipo: entero
   * `org.apache.felix.http.jetty.requestBufferSize`
      * Tipo: entero
   * `org.apache.felix.http.jetty.responseBufferSize`
      * Tipo: entero
   * `org.apache.felix.http.jetty.maxFormSize`
      * Tipo: entero
   * `org.apache.felix.https.jetty.session.cookie.httpOnly`
      * Tipo: booleano
   * `org.apache.felix.https.jetty.session.cookie.secure`
      * Tipo: booleano
   * `org.eclipse.jetty.servlet.SessionIdPathParameterName`
      * Tipo: cadena
   * `org.eclipse.jetty.servlet.CheckingRemoteSessionIdEncoding`
      * Tipo: booleano
   * `org.eclipse.jetty.servlet.SessionCookie`
      * Tipo: cadena
   * `org.eclipse.jetty.servlet.SessionDomain`
      * Tipo: cadena
   * `org.eclipse.jetty.servlet.SessionPath`
      * Tipo: cadena
   * `org.eclipse.jetty.servlet.MaxAge`
      * Tipo: entero
   * `org.eclipse.jetty.servlet.SessionScavengingInterval`
      * Tipo: entero
   * `org.apache.felix.jetty.gziphandler.enable`
      * Tipo: booleano
   * `org.apache.felix.jetty.gzip.minGzipSize`
      * Tipo: entero
   * `org.apache.felix.jetty.gzip.compressionLevel`
      * Tipo: entero
   * `org.apache.felix.jetty.gzip.inflateBufferSize`
      * Tipo: entero
   * `org.apache.felix.jetty.gzip.syncFlush`
      * Tipo: booleano
   * `org.apache.felix.jetty.gzip.excludedUserAgents`
      * Tipo: cadena
   * `org.apache.felix.jetty.gzip.includedMethods`
      * Tipo: matriz de cadenas
   * `org.apache.felix.jetty.gzip.excludedMethods`
      * Tipo: matriz de cadenas
   * `org.apache.felix.jetty.gzip.includedPaths`
      * Tipo: matriz de cadenas
   * `org.apache.felix.jetty.gzip.excludedPaths`
      * Tipo: matriz de cadenas
   * `org.apache.felix.jetty.gzip.includedMimeTypes`
      * Tipo: matriz de cadenas
   * `org.apache.felix.jetty.gzip.excludedMimeTypes`
      * Tipo: matriz de cadenas
   * `org.apache.felix.http.session.invalidate`
      * Tipo: booleano
   * `org.apache.felix.http.session.container.attribute`
      * Tipo: matriz de cadenas
   * `org.apache.felix.http.session.uniqueid`
      * Tipo: booleano
* **`org.apache.sling.scripting.cache`** (Fecha de anuncio: 30/4/2021, fecha de aplicación: 31/7/2021)
   * `org.apache.sling.scripting.cache.size`
      * Tipo: entero
      * Intervalo requerido: >= 2048
   * `org.apache.sling.scripting.cache.additional_extensions`
      * Requerido
      * Tipo: matriz de cadenas
      * Intervalo requerido: debe incluir js
* **`com.day.cq.mailer.DefaultMailService`** (Fecha de anuncio: 30/4/2021, fecha de aplicación: 31/7/2021)
   * `smtp.host`
      * Tipo: cadena
   * `smtp.port`
      * Tipo: entero
      * Intervalo requerido: 465, 587 o 25
   * `smtp.user`
      * Tipo: cadena
   * `smtp.password`
      * Tipo: cadena
   * `from.address`
      * Tipo: cadena
   * `smtp.ssl`
      * Tipo: cadena
   * `smtp.starttls`
      * Tipo: booleano
   * `smtp.requiretls`
      * Tipo: booleano
   * `debug.email`
      * Tipo: booleano
   * `oauth.flow`
      * Tipo: booleano
* **`org.apache.sling.commons.log.LogManager.factory.config`** (Fecha de anuncio: 16/11/21, Fecha de aplicación: 2/16/21)
   * `org.apache.sling.commons.log.level`
      * Tipo: enumeración
      * Intervalo requerido: INFO, DEPURACIÓN o TRACE
   * `org.apache.sling.commons.log.names`
      * Tipo: cadena
   * `org.apache.sling.commons.log.file`
      * Tipo: cadena
   * `org.apache.sling.commons.log.additiv`
      * Tipo: booleano