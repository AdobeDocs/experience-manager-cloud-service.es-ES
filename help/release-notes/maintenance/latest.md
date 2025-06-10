---
title: Notas de la versión actuales sobre el mantenimiento de [!DNL Adobe Experience Manager] as a Cloud Service.
description: Notas de la versión actuales sobre el mantenimiento de [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: d3cdc3d69c0002c5b124150050f905123457331c
workflow-type: tm+mt
source-wordcount: '380'
ht-degree: 51%

---


# Notas de la versión de mantenimiento {#maintenance-release-notes}

En la siguiente sección se describen las notas de la versión técnicas actuales sobre el mantenimiento de Experience Manager as a Cloud Service.

## Versión 21193 {#21193}

A continuación, se resumen las mejoras continuas para la versión de mantenimiento 21193, que se publicó el miércoles, 10 de junio de 2025. La versión de mantenimiento anterior fue la 21005.

La activación de funcionalidades 2025.6.0 proporciona el conjunto completo de funcionalidades para esta versión de mantenimiento. Consulte la [Hoja de ruta de versiones de Experience Manager](https://experienceleague.adobe.com/es/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap) para obtener más información.

### Mejoras {#enhancements-21193}

* ASSETS-51245: rendimiento mejorado para listas de carpetas grandes en la IU táctil.
* ASSETS-51686: mejoras en el trabajo de operaciones masivas, incluida una cancelación de trabajo más sencilla, un registro mejorado y descargas de auditoría para obtener resultados grandes.
* CQ-4360131: Se ha mejorado la respuesta de error para los puntos de conexión de OpenAPI, lo que permite a los clientes de API recibir información de error estructurada correcta.

### Problemas solucionados {#fixed-issues-21193}

* ASSETS-41007: Los recursos eliminados podrían permanecer visibles en Content Hub.
* ASSETS-50994: AemRequestEventFilter causa una contención excesiva de los subprocesos de Jetty.
* ASSETS-50155: eventos de cambio de metadatos duplicados activados.
* ASSETS-50716: La ordenación por título en la vista de lista de Assets no funciona como se esperaba.
* ASSETS-50820: Asegúrese de que las solicitudes no válidas a la API de relaciones de recursos se rechacen correctamente con un error 400.
* ASSETS-50562: la API de carga de recursos debe crear la versión de forma predeterminada en caso de conflicto de nombres.
* ASSETS-50992: el extremo de la API de Assets launchUpload.json debe devolver el tipo de contenido de &quot;application/json&quot;.
* ASSETS-51322: Eliminación y caducidad automáticas de barricadas asíncronas que permanecen indefinidamente después de un trabajo fallido.
* ASSETS-51809: El editor CSV no mostraba los cambios guardados recientemente debido al almacenamiento en caché del explorador.
* SITES-31678: Los fragmentos de experiencias (XF) con referencias según el contexto no resolvieron la raíz de idioma correcta en la API de publicación de XF.


### Problemas conocidos {#known-issues-21193}

Ninguna.

### Características y API obsoletas {#deprecated-21193}

Las funciones y API obsoletas y eliminadas de AEM as a Cloud Service se detallan en el documento [Funciones y API obsoletas y eliminadas](/help/release-notes/deprecated-removed-features.md).

### Correcciones de seguridad {#security-21193}

AEM as a Cloud Service se dedica a optimizar la seguridad y el rendimiento de su plataforma. Esta versión de mantenimiento aborda 2 vulnerabilidades identificadas, reforzando nuestro compromiso con una sólida protección del sistema.

### Tecnologías integradas {#embedded-tech-21193}

| Tecnología | Versión | Vínculo |
|---|---|---|
| AEM Oak | 1.80.0 | [API Oak 1.80.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.80.0/index.html) |
| API AEM SLING | 2.27.6 | [API de Apache Sling 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.28-1.4.0 | [Especificación de idioma de la plantilla HTML](https://github.com/adobe/htl-spec) |
| Los componentes principales de AEM | 2.29.0 | [Componentes principales de WCM AEM](https://github.com/adobe/aem-core-wcm-components) |
