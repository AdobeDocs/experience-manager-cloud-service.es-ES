---
title: Notas de la versión actuales sobre el mantenimiento de [!DNL Adobe Experience Manager] as a Cloud Service.
description: Notas de la versión actuales sobre el mantenimiento de [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: dc7150c6ce971aa6f89fa24f7ca387cbb28db1f2
workflow-type: tm+mt
source-wordcount: '319'
ht-degree: 63%

---


# Notas de la versión de mantenimiento {#maintenance-release-notes}

En la siguiente sección se describen las notas de la versión técnicas actuales sobre el mantenimiento de Experience Manager as a Cloud Service.

## Versión 17258 {#release-17258}

A continuación se resumen las mejoras continuas para la versión de mantenimiento 17258, que se publicó el miércoles, 30 de julio de 2024. La versión de mantenimiento anterior fue la 17098.

La activación de funcionalidades 2024.8.0 proporcionará el conjunto completo de funcionalidades para esta versión de mantenimiento. Consulte la [Hoja de ruta de versiones de Experience Manager](https://experienceleague.adobe.com/es/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap) para obtener más información.

### Mejoras {#enhancements-17258}

* ASSETS-31445: funciones de creación de plantillas iniciales de Dynamic Media
* ASSETS-40399: ajustes de cola de transcripción automática de DM actualizados
* ASSETS-40873: permitir que el máximo de filas exportadas de metadatos se establezca mediante la configuración OSGI

### Problemas solucionados {#fixed-issues-17258}

* ASSETS-30613: Reemplazar recurso no elimina ni agrega recurso en el nuevo nivel de entrega
* ASSETS-31882: está prohibido acceder al archivo de manifiesto de flujo continuo en el autor
* ASSETS-39598: la importación masiva no puede eliminar recursos con caracteres especiales en el nombre del back-end S3
* CNTBF-209 - Mejoras en la cancelación de trabajos de retroceso
* SCRNS-3762: mejore playerLogger en el canal de secuencia para colocar registros en la consola al previsualizar el canal en el navegador
* SCRNS-4455: falta el botón &quot;Administrar publicación&quot; y &quot;Publish rápido&quot; para usuarios QUE NO SON ADMINISTRADORES en el proveedor de contenido para canales
* SITES-22940: no se puede ver el fragmento de contenido como carga útil de flujo de trabajo

### Problemas conocidos {#known-issues-17258}

Ninguno

### Aviso de cambio {#change-notice-17258}

* A partir de septiembre de 2024, AEM as a Cloud Service deshabilitará la serialización de los solucionadores de recursos a través del marco de trabajo Exportador de modelos Sling. Consulte la [documentación](/help/implementing/developing/hybrid/disallow-the-serialization-of-resourceresolvers-via-sling-model-exporter.md) para obtener más información.

### Características y API obsoletas {#deprecated-17258}

Las funciones y API obsoletas y eliminadas de AEM as a Cloud Service se detallan en el documento [Funciones y API obsoletas y eliminadas](/help/release-notes/deprecated-removed-features.md).

### Tecnologías integradas {#embedded-tech-17258}

| Tecnología | Versión | Vínculo |
|---|---|---|
| AEM Oak | 1.66.0 | [API Oak 1.66.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.66.0/index.html?lang=es) |
| API AEM SLING | 2.27.2 | [API de Apache Sling 2.27.2 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.24-1.4.0 | [Especificación de idioma de la plantilla HTML](https://github.com/adobe/htl-spec) |
| Los componentes principales de AEM | 2.25.4 | [Componentes principales de WCM AEM](https://github.com/adobe/aem-core-wcm-components) |
