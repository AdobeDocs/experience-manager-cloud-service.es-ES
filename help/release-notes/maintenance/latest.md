---
title: Notas de la versión actuales sobre el mantenimiento de [!DNL Adobe Experience Manager] as a Cloud Service.
description: Notas de la versión actuales sobre el mantenimiento de [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 3067e88f8adea50f6b6b05e0466974bc57bc4a4e
workflow-type: tm+mt
source-wordcount: '607'
ht-degree: 38%

---


# Notas de la versión de mantenimiento {#maintenance-release-notes}

En la siguiente sección se describen las notas de la versión técnicas actuales sobre el mantenimiento de Experience Manager as a Cloud Service.

## Versión 21994 {#21994}

A continuación se resumen las mejoras continuas para la versión de mantenimiento 21994, que se publicó el miércoles, 19 de agosto de 2025. La versión de mantenimiento anterior fue la 21772.

La activación de funcionalidades 2025.8.0 proporciona el conjunto completo de funcionalidades para esta versión de mantenimiento. Consulte la [Hoja de ruta de versiones de Experience Manager](https://experienceleague.adobe.com/es/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap) para obtener más información.

### Nuevas funciones  {#new-features-21994}

Ninguna.

### Mejoras {#enhancements-21994}

* GRANITE-53488: Mejore la gestión de errores del extremo deleteconf.json.
* GRANITE-59968: permite configurar REPLICATION_FORCE_READY_MILLIES.
* GRANITE-60183: Apache commons-fileupload 1.6.0.
* GRANITE-60306: Apache commons-lang a 3.18.0.
* GRANITE-60637: Apache commons-codec a 1.19.0.
* GRANITE-60645: Apache commons-io 2.20.0.
* GRANITE-60663: Apache commons-text 1.14.0.
* GRANITE-60714: Controlador Java Mongo 5.2.
* GRANITE-60778: Filevault 4.0.0.
* GRANITE-60823: Jackrabbit 2.22.2.
* GRANITE-60967: crea métricas para rastrear el tiempo de compilación de clientlib.
* SKYOPS-105469: Agregar compatibilidad con acsredirectMgr en la API de correcciones automáticas.
* SKYOPS-113929: Agregar métricas para la comprobación de replicación lista.
* SKYOPS-84821: Motor Sling 2.16.6.
* SKYOPS-114322: subir el nivel del compilador de cierre a `ECMASCRIPT_2018`.

### Problemas solucionados {#fixed-issues-21994}

* GRANITE-60167: La actualización asíncrona del índice en Skyline no admite datos CSV.
* GRANITE-60532: No se recoge la modificación de las alternancias de valor.
* SITES-34277: corrija el error de bloqueo en los flujos de trabajo de traducción para páginas.
* SKYOPS-105471: Soporte dambaseredirect fix para también autofix.
* SKYOPS-109532: añadir la función eliminada vínculo como comentario detrás de alternancia.

#### Guías de AEM {#guides-21994}

* GUIDES-26688: Los archivos CSS y de diseño de página de las plantillas nativas de PDF muestran un comportamiento incoherente de bloqueo de archivos, lo que permite realizar ediciones incluso cuando los archivos están bloqueados.
* GUIDES-30900: Copiar una carpeta con un gran número de recursos desde la interfaz de usuario de Assets lleva a un tiempo de espera de API. La operación sigue ejecutándose en el servidor y se completa después de un tiempo, pero no se muestra ningún mensaje de éxito o error ni notificación en la interfaz de usuario.
* GUIDES-29090: en la salida nativa de PDF, la lista de índices (LOI) aparece en un orden no alfabético y los términos de índice anidados no se agrupan correctamente, lo que dificulta la navegación por el índice.
* GUIDES-11227: al copiar un mapa DITA desde la interfaz de usuario de Assets, también se copia la línea de base adjunta al nuevo mapa.
* GUIDES-31506: la página de inicio queda en blanco cuando uno de los archivos enumerados en el widget Archivos recientes se basa en una plantilla cuya plantilla de origen no incluye una miniatura.

Para obtener más información sobre las funciones nuevas y mejoradas y los problemas corregidos en la versión, consulte la [hoja de ruta de la versión de Experience Manager Guides](https://experienceleague.adobe.com/es/docs/experience-manager-guides/using/release-info/aem-guides-releases-roadmap).

### Problemas conocidos {#known-issues-21994}

* Apache HTTPD versión 2.4.65 introduce cambios que pueden afectar a determinadas configuraciones debido a las nuevas restricciones implementadas como parte de las correcciones de seguridad. Estas correcciones corrigen las vulnerabilidades al garantizar que las directivas como `RequestHeader set`, `edit` y `edit_r` utilizadas para modificar el encabezado Content-Type ahora se limiten correctamente a los encabezados de solicitud. Este cambio evita modificaciones no deseadas en los encabezados de respuesta, especialmente para el contenido estático.

### Características y API obsoletas {#deprecated-21994}

Las funciones y API obsoletas y eliminadas de AEM as a Cloud Service se detallan en el documento [Funciones y API obsoletas y eliminadas](/help/release-notes/deprecated-removed-features.md).

### Correcciones de seguridad {#security-21994}

AEM as a Cloud Service se dedica a optimizar la seguridad y el rendimiento de su plataforma. Esta versión de mantenimiento aborda 2 vulnerabilidades identificadas, reforzando nuestro compromiso con una sólida protección del sistema.

### Tecnologías integradas {#embedded-tech-21994}

| Tecnología | Versión | Vínculo |
|---|---|---|
| AEM Oak | 1.84.0 | [API Oak 1.84.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.84/index.html) |
| API AEM SLING | 2.27.6 | [API de Apache Sling 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.28-1.4.0 | [Especificación de idioma de la plantilla HTML](https://github.com/adobe/htl-spec) |
| Apache HTTP Server | 2.4.65 | [Apache Httpd 2.4.65](https://apache.googlesource.com/httpd/+/refs/tags/2.4.65/CHANGES) |
| Componentes principales de AEM | 2.29.0 | [Componentes principales de WCM AEM](https://github.com/adobe/aem-core-wcm-components) |
| Node.js | 14 (valor predeterminado) | [Versiones de Node.js compatibles](https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/implementing/developing/developing-with-front-end-pipelines#node-versions) |
