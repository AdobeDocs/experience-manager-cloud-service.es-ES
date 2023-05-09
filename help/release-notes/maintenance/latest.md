---
title: Notas de la versión de mantenimiento actual de [!DNL Adobe Experience Manager] as a Cloud Service.
description: Notas de la versión de mantenimiento actual de [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
source-git-commit: ea3a476f7f2d7d97a2428c6facf61b746dba7a23
workflow-type: tm+mt
source-wordcount: '208'
ht-degree: 47%

---

# Notas de la versión de mantenimiento {#maintenance-release-notes}

En la siguiente sección se describen las notas de la versión técnica de la versión de mantenimiento actual de Experience Manager as a Cloud Service.

## Versión 11873 {#release-11873}

A continuación se resumen las mejoras continuas de la versión de mantenimiento 11873, que se publicó el 3 de mayo de 2023. Esta versión de mantenimiento es una actualización de la versión de mantenimiento 11835 anterior.

La activación de funcionalidades para esta versión de mantenimiento le proporcionará el conjunto completo de funcionalidades. Consulte las [notas de la versión actual](/help/release-notes/release-notes-cloud/release-notes-current.md) para obtener información detallada.

### Mejoras {#enhancements}

- SITES-1200 - Mejoras en la API de búsqueda con filtrado basado en etiquetas
- GRANITE-42939 - Añada anotaciones y advertencias de desaprobación al código del servidor oauth

### Problemas conocidos {#known-issues-11873}

Ninguna.

### Problemas corregidos {#fixed-issues-11873}

- SKYSI-19884/SKYOPS-53745: Se ha corregido un problema con PublishPageRenderingErrorsHigh
- GRANITE-4388 - Se ha corregido la degradación del rendimiento después de un gran número de escrituras de activos DAM en Mongo
- SITES-11922: Se ha corregido un problema con la cancelación de la publicación de la vista previa que no eliminaba el estado de sincronización
- ASSETS-21648: Se ha corregido un problema de permisos con la funcionalidad de Asset Relate

### Tecnologías integradas {#embedded-tech-11873}

| Tecnología | Versión | Vínculo |
|---|---|---|
| AEM OAK | 1,44-T20221206170501-6d59064 | [API Oak 1.44.0](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.44.0/index.html) |
| API AEM SLING | Versión 2.27.0 | [API de Apache Sling 2.27.0](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | Versión 1.4.20-1.4.0 | [Especificación de idioma de la plantilla HTML](https://github.com/adobe/htl-spec) |
| Los componentes principales de AEM | Versión 2.21.2 | [Componentes principales de WCM de AEM](https://github.com/adobe/aem-core-wcm-components) |
