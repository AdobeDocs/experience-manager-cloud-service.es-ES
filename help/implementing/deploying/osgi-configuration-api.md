---
title: API de configuración OSGi
description: Descripción del AEM como superficie de configuración OSGi Cloud Service
feature: Implementación
source-git-commit: 4be76f19c27aeab84de388106a440434a99a738c
workflow-type: tm+mt
source-wordcount: '389'
ht-degree: 0%

---


# API de configuración OSGi

Las dos listas siguientes reflejan la AEM como una superficie de configuración OSGi Cloud Service, y describen lo que los clientes pueden configurar.

1. Una lista de configuraciones de OSGi que no debe configurar el código de cliente
1. Una lista de configuraciones de OSGi cuyas propiedades pueden configurarse, pero deben cumplir las reglas de validación indicadas. Estas reglas incluyen si la declaración de la propiedad es obligatoria, su tipo y, en algunos casos, su rango permitido de valores.

Si una configuración OSGI no aparece en la lista, puede configurarla el código de cliente.

Estas reglas se validan durante el proceso de creación de Cloud Manager. Pueden agregarse reglas adicionales con el tiempo y la fecha prevista de ejecución se indica en el cuadro. Se espera que los clientes cumplan estas reglas antes de la fecha de aplicación objetivo. Si no se cumplen las reglas después de la fecha de eliminación, se generarán errores en el proceso de creación de Cloud Manager. Los proyectos de Maven deben incluir el [AEM as a Cloud Service SDK Build Analyzer Maven Plugin](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/build-analyzer-maven-plugin.html) para marcar los errores de configuración OSGI durante el desarrollo del SDK local.

Puede encontrar información adicional sobre la configuración OSGI en [esta ubicación](/help/implementing/deploying/configuring-osgi.md).

## Configuraciones de OSGi que no se pueden modificar {#osgi-configurations-that-cannot-be-modified}

* **`org.apache.felix.webconsole.internal.servlet.OsgiManager`** (Fecha del anuncio: 30/4/2021, Fecha de ejecución: 31/7/2021)
* **`com.day.cq.auth.impl.cug.CugSupportImpl`** (Fecha del anuncio: 30/4/2021, Fecha de ejecución: 31/7/2021)
* **`com.day.cq.jcrclustersupport.ClusterStartLevelController`** (Fecha del anuncio: 30/4/2021, Fecha de ejecución: 31/7/2021)
* **`org.apache.felix.http (Factory)`** (Fecha del anuncio: 30/4/2021, Fecha de ejecución: 31/7/2021)

## Configuraciones de OSGi sujetas a reglas de validación de compilación {#osgi-configurations-subject-to-build-validation-rules}

* **`org.apache.felix.eventadmin.impl.EventAdmin`** (Fecha del anuncio: 30/4/2021, Fecha de ejecución: 31/7/2021)
   * `org.apache.felix.eventadmin.ThreadPoolSize`
      * Tipo: integer
      * Intervalo requerido: 2-100
   * `org.apache.felix.eventadmin.AsyncToSyncThreadRatio`
      * Tipo: double
   * `org.apache.felix.eventadmin.Timeout`
      * Tipo: integer
   * `org.apache.felix.eventadmin.RequireTopic`
      * Tipo: booleano
   * `org.apache.felix.eventadmin.IgnoreTimeout`
      * Requerido
      * Tipo: matriz de cadenas
      * Intervalo requerido: Debe incluir al menos todos los `org.apache.felix*`, `org.apache.sling*`, `come.day*`, `com.adobe*`
   * `org.apache.felix.eventadmin.IgnoreTopic`
      * Tipo: matriz de cadenas
* **`org.apache.felix.http`** (Fecha del anuncio: 30/4/2021, Fecha de ejecución: 31/7/2021)
   * `org.apache.felix.http.timeout`
      * Tipo: integer
   * `org.apache.felix.http.session.timeout`
      * Tipo: integer
   * `org.apache.felix.http.jetty.threadpool.max`
      * Tipo: integer
   * `org.apache.felix.http.jetty.headerBufferSize`
      * Tipo: integer
   * `org.apache.felix.http.jetty.requestBufferSize`
      * Tipo: integer
   * `org.apache.felix.http.jetty.responseBufferSize`
      * Tipo: integer
   * `org.apache.felix.http.jetty.maxFormSize`
      * Tipo: integer
   * `org.apache.felix.https.jetty.session.cookie.httpOnly`
      * Tipo: booleano
   * `org.apache.felix.https.jetty.session.cookie.secure`
      * Tipo: booleano
   * `org.eclipse.jetty.servlet.SessionIdPathParameterName`
      * Tipo: string
   * `org.eclipse.jetty.servlet.CheckingRemoteSessionIdEncoding`
      * Tipo: booleano
   * `org.eclipse.jetty.servlet.SessionCookie`
      * Tipo: string
   * `org.eclipse.jetty.servlet.SessionDomain`
      * Tipo: string
   * `org.eclipse.jetty.servlet.SessionPath`
      * Tipo: string
   * `org.eclipse.jetty.servlet.MaxAge`
      * Tipo: integer
   * `org.eclipse.jetty.servlet.SessionScavengingInterval`
      * Tipo: integer
   * `org.apache.felix.jetty.gziphandler.enable`
      * Tipo: booleano
   * `org.apache.felix.jetty.gzip.minGzipSize`
      * Tipo: integer
   * `org.apache.felix.jetty.gzip.compressionLevel`
      * Tipo: integer
   * `org.apache.felix.jetty.gzip.inflateBufferSize`
      * Tipo: integer
   * `org.apache.felix.jetty.gzip.syncFlush`
      * Tipo: booleano
   * `org.apache.felix.jetty.gzip.excludedUserAgents`
      * Tipo: string
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
* **`org.apache.sling.scripting.cache`** (Fecha del anuncio: 30/4/2021, Fecha de ejecución: 31/7/2021)
   * `org.apache.sling.scripting.cache.size`
      * Tipo: integer
      * Intervalo requerido: >= 2048
   * `org.apache.sling.scripting.cache.additional_extensions`
      * Requerido
      * Tipo: matriz de cadenas
      * Intervalo requerido: debe incluir js
* **`com.day.cq.mailer.DefaultMailService`** (Fecha del anuncio: 30/4/2021, Fecha de ejecución: 31/7/2021)
   * `smtp.host`
      * Tipo: string
   * `smtp.port`
      * Tipo: integer
      * Intervalo requerido: 465, 587 o 25
   * `smtp.user`
      * Tipo: string
   * `smtp.password`
      * Tipo: string
   * `from.address`
      * Tipo: string
   * `smtp.ssl`
      * Tipo: string
   * `smtp.starttls`
      * Tipo: booleano
   * `smtp.requiretls`
      * Tipo: booleano
   * `debug.email`
      * Tipo: booleano
   * `oauth.flow`
      * Tipo: booleano
