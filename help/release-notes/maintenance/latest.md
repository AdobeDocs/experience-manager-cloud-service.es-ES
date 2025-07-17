---
title: Notas de la versión actuales sobre el mantenimiento de [!DNL Adobe Experience Manager] as a Cloud Service.
description: Notas de la versión actuales sobre el mantenimiento de [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 2e90e40a0fe439653987a23792a4c1ec612aafd6
workflow-type: tm+mt
source-wordcount: '276'
ht-degree: 63%

---


# Notas de la versión de mantenimiento {#maintenance-release-notes}

En la siguiente sección se describen las notas de la versión técnicas actuales sobre el mantenimiento de Experience Manager as a Cloud Service.

## Versión 21570 {#21570}

A continuación se resumen las mejoras continuas para la versión de mantenimiento 21570, que se publicó el miércoles, 15 de julio de 2025. La versión de mantenimiento anterior fue la 21484.

>[!NOTE]
>
>[La versión 21484](/help/release-notes/maintenance/2025/2025-7-0.md#21484) pasó a ser privada y se reemplazó por la versión 21570.

La activación de funcionalidades 2025.7.0 proporciona el conjunto completo de funcionalidades para esta versión de mantenimiento. Consulte la [Hoja de ruta de versiones de Experience Manager](https://experienceleague.adobe.com/es/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap) para obtener más información.

### Mejoras {#enhancements-21570}

* Se ha migrado a Apache Httpd 2.4.63

### Problemas solucionados {#fixed-issues-21570}

* SKYOPS-112722: se ha corregido un problema que provocaba que fallara la resolución de la URL de vanidad

### Problemas conocidos {#known-issues-21570}

* AEM SDK relacionado lleva un ID de versión (21575) diferente y está disponible a través del Portal de distribución de software.
* La versión 2.4.63 del servidor HTTP Apache introdujo un cambio radical en la forma en que `mod_rewrite` gestiona los signos de interrogación (`?`) en las direcciones URL. Este cambio se implementó para evitar el uso del indicador `UnsafeAllow3F`, que se consideraba un riesgo de seguridad. Esto afecta a cualquier directiva `RewriteRule` que dependa de la detección de signos de interrogación en patrones de URL.

### Características y API obsoletas {#deprecated-21570}

Las funciones y API obsoletas y eliminadas de AEM as a Cloud Service se detallan en el documento [Funciones y API obsoletas y eliminadas](/help/release-notes/deprecated-removed-features.md).

### Correcciones de seguridad {#security-21570}

Ninguno

### Tecnologías integradas {#embedded-tech-21570}

| Tecnología | Versión | Vínculo |
|---|---|---|
| AEM Oak | 1.80.0 | [API Oak 1.80.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.80.0/index.html) |
| API AEM SLING | 2.27.6 | [API de Apache Sling 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.28-1.4.0 | [Especificación de idioma de la plantilla HTML](https://github.com/adobe/htl-spec) |
| Servidor HTTP Apache | 2.4.63 | [Apache Httpd 2.4.63](https://github.com/apache/httpd/blob/2.4.63/CHANGES) |
| Componentes principales de AEM | 2.29.0 | [Componentes principales de WCM AEM](https://github.com/adobe/aem-core-wcm-components) |
