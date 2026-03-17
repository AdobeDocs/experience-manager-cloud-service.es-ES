---
title: Notas de la versión actuales sobre el mantenimiento de [!DNL Adobe Experience Manager] as a Cloud Service.
description: Notas de la versión actuales sobre el mantenimiento de [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 2a7b83b99547637e02ec7cef9c92c5dd794a9adc
workflow-type: tm+mt
source-wordcount: '636'
ht-degree: 36%

---


# Notas de la versión de mantenimiento {#maintenance-release-notes}

En la siguiente sección se describen las notas de la versión técnicas actuales sobre el mantenimiento de Experience Manager as a Cloud Service.

## Versión 24893 {#release-24893}

A continuación, se resumen las mejoras continuas para la versión de mantenimiento 24893, publicada el miércoles, 17 de marzo de 2026. La versión de mantenimiento anterior fue la 24678.

La activación de funcionalidades 2026.3.0 proporcionará el conjunto completo de funcionalidades para esta versión de mantenimiento. Consulte la [Hoja de ruta de versiones de Experience Manager](https://experienceleague.adobe.com/es/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap) para obtener más información.

### Mejoras {#enhancements-24893}

* CNTBF-613: Corregir acceso denegado (JCR-101): no se pudieron registrar los tipos de nodo.
* GRANITE-53957: Actualice Azure SDK V8 a V12 para oak-blob-azure.
* GRANITE-57035: utilice Bouncy Castle como proveedor de seguridad predeterminado.
* GRANITE-59249: Evite registrar un proveedor de seguridad en JVM.
* GRANITE-61564: no se puede abrir la configuración de vista de `/security/users.html` para los administradores.
* GRANITE-64748: OIDC: caducidad configurable de la cookie sling.oauth-request-key.
* SITES-39767: admite el valor nonce a través del atributo de solicitud (CSP).
* SKYOPS-129301: establezca el nivel de cumplimiento de API jar javadoc en 17.
* GRANITE-64962: Actualice Apache Jackrabbit Oak a 1.92.0.
* GRANITE-64963: Actualice Apache Jackrabbit Filevault a 4.2.0.
* GRANITE-64764: Actualice el texto de Apache Commons a la versión 1.15.0.
* SKYOPS-131412: Actualice Apache Commons Exec a 1.6.0.
* SKYOPS-131432: Actualice Felix SCR a 2.2.14.
* SKYOPS-131907: actualizar la región de la API de Sling a 1.1.10.
* SKYOPS-131938: Actualice GSON a 2.13.2.
* SKYOPS-132173: Actualice el códec Apache Commons a 1.21.0.
* SKYOPS-132182: actualizar el inquilino de Sling a 1.1.8.
* SKYOPS-132267: actualice org.osgi.service.component a 1.5.1.
* SKYOPS-132272: actualizar el modelo de funciones de Sling a 2.0.4.
* SKYOPS-133689: Actualice Dispatcher para utilizar Apache httpd 2.4.66.

### Problemas solucionados {#fixed-issues-24893}

* GRANITE-64443: `workflow.core` elimina las exportaciones obsoletas de `log4j`.
* GRANITE-64543: La respuesta de restricciones de permisos debe coincidir con el contrato de API.

#### Guías de AEM {#guides-24893}

* GUIDES-38412 : Al editar un archivo de Schematron `(*.sch)` y utilizar la función de buscar y reemplazar, el panel buscar y reemplazar aparece parcialmente fuera de la pantalla en la parte inferior, lo que impide el acceso a sus campos y controles de entrada.
* GUIDES-37806: Cuando se reutiliza el mismo tema en varias asignaciones con diferentes ajustes preestablecidos condicionales, la publicación de la asignación más reciente en Salesforce sobrescribe el contenido del tema, lo que da como resultado que se muestren datos incorrectos a los usuarios de asignaciones publicadas anteriormente.
* GUIDES-39394: Cuando una imagen administrada inicialmente como un recurso específico de un idioma con una versión específica (por ejemplo, en `/en/`) se mueve a una carpeta global con una versión actualizada y se realiza una exportación de línea de base, la nueva línea de base sigue haciendo referencia a versiones obsoletas específicas del idioma de esa imagen, lo que provoca un error en la exportación de línea de base.
* GUIDES-39054: Al crear una línea de base dinámica, el editor a veces deja de responder debido a varias solicitudes de API simultáneas, lo que provoca que todas las demás operaciones se detengan.
* GUIDES-37781: Al asignar un usuario a una tarea de revisión, la lista desplegable muestra todos los usuarios, en lugar de solo aquellos asociados a los proyectos seleccionados, lo que da como resultado opciones de usuario no válidas.
* GUIDES-39385: Al abrir un informe para un mapa, se produce un retraso en la carga del panel Filtros.

Para obtener más información sobre las funciones nuevas y mejoradas y los problemas corregidos en la versión, consulte la [hoja de ruta de la versión de Experience Manager Guides](https://experienceleague.adobe.com/es/docs/experience-manager-guides/using/release-info/aem-guides-releases-roadmap).

### Problemas conocidos {#known-issues-24893}

Ninguna.

### Características y API obsoletas {#deprecated-24893}

Las funciones y API obsoletas y eliminadas de AEM as a Cloud Service se detallan en el documento [Funciones y API obsoletas y eliminadas](/help/release-notes/deprecated-removed-features.md).

### Correcciones de seguridad {#security-24893}

AEM as a Cloud Service se dedica a optimizar la seguridad y el rendimiento de su plataforma. Esta versión de mantenimiento aborda 9 vulnerabilidades identificadas, reforzando nuestro compromiso con una sólida protección del sistema.

### Tecnologías integradas {#embedded-tech-24893}

| Tecnología | Versión | Vínculo |
|---|---|---|
| AEM Oak | 1.92.0 | [API de Oak 1.92.0](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.92.0/index.html) |
| API AEM SLING | 2.27.6 | [API de Apache Sling 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.28-1.4.0 | [Especificación de idioma de la plantilla HTML](https://github.com/adobe/htl-spec) |
| Apache HTTP Server | 2.4.66 | [Apache Httpd 2.4.66](https://apache.googlesource.com/httpd/+/refs/tags/2.4.66/CHANGES) |
| Componentes principales de AEM | 2.30.4 | [Componentes principales de WCM AEM](https://github.com/adobe/aem-core-wcm-components) |
| Node.js | 14 (valor predeterminado) | [Versiones de Node.js compatibles](https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/implementing/developing/developing-with-front-end-pipelines#node-versions) |
