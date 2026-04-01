---
title: Notas de la versión actuales sobre el mantenimiento de [!DNL Adobe Experience Manager] as a Cloud Service.
description: Notas de la versión actuales sobre el mantenimiento de [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: e035c1c27f652af231034588eb1359354182dcb0
workflow-type: tm+mt
source-wordcount: '341'
ht-degree: 62%

---


# Notas de la versión de mantenimiento {#maintenance-release-notes}

En la siguiente sección se describen las notas de la versión técnicas actuales sobre el mantenimiento de Experience Manager as a Cloud Service.

## Versión 25194 {#25194}

A continuación, se resumen las mejoras continuas para la versión de mantenimiento 25194, que se publicó el jueves, 01 de abril de 2026. La versión de mantenimiento anterior fue la 24678.

La activación de funciones 2026.4.0 proporciona el conjunto completo de funciones para esta versión de mantenimiento. Consulte la [Hoja de ruta de versiones de Experience Manager](https://experienceleague.adobe.com/es/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap) para obtener más información.

>[!NOTE]
>
>La 24893 de la versión se ha convertido en privada.

### Mejoras {#enhancements-25194}

* ASSETS-65127: Metadatos personalizados de eventos: se ha mejorado la administración de los nombres de los metadatos.
* ASSETS-63313: crear automáticamente vínculos relacionados para recursos exportados y principales basados en manifiestos de C2PA.
* ASSETS-10995: limitar el número de recursos en un zip de descarga.

### Problemas solucionados {#fixed-issues-25194}

* ASSETS-62882: vista de administrador: la información sobre herramientas se interrumpe cuando se cargan varios nombres de archivo no válidos.
* ASSETS-63642: El vínculo Compartir no puede procesar recursos en algunos entornos de desarrollo (SLA3).
* ASSETS-59267: NPE al cargar metadatos de aplicación para la carga útil de entrega.
* ASSETS-59227: exportación de metadatos: las propiedades no seleccionadas ya no se incluyen debido a la coincidencia de regex.
* ASSETS-65187: Vista previa del CSV en la nube cuando los datos de columna contienen comas de escape.
* ASSETS-63441: Asegúrese de que todos los usuarios tengan permisos para leer la configuración de Assets Omnisearch.
* SITES-40095: Editor de metadatos: referencias de fragmentos de contenido local más allá de 10 entradas.

### Problemas conocidos {#known-issues-25194}

Ninguna.

### Características y API obsoletas {#deprecated-25194}

Las funciones y API obsoletas y eliminadas de AEM as a Cloud Service se detallan en el documento [Funciones y API obsoletas y eliminadas](/help/release-notes/deprecated-removed-features.md).

### Correcciones de seguridad {#security-25194}

AEM as a Cloud Service se dedica a optimizar la seguridad y el rendimiento de su plataforma. Esta versión de mantenimiento aborda 9 vulnerabilidades identificadas, reforzando nuestro compromiso con una sólida protección del sistema.

### Tecnologías integradas {#embedded-tech-25194}

| Tecnología | Versión | Vínculo |
|---|---|---|
| AEM Oak | 1.90.0 | [API de Oak 1.90.0](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.90.0/index.html) |
| API AEM SLING | 2.27.6 | [API de Apache Sling 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.28-1.4.0 | [Especificación de idioma de la plantilla HTML](https://github.com/adobe/htl-spec) |
| Apache HTTP Server | 2.4.65 | [Apache Httpd 2.4.65](https://apache.googlesource.com/httpd/+/refs/tags/2.4.65/CHANGES) |
| Componentes principales de AEM | 2.30.4 | [Componentes principales de WCM AEM](https://github.com/adobe/aem-core-wcm-components) |
| Node.js | 14 (valor predeterminado) | [Versiones de Node.js compatibles](https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/implementing/developing/developing-with-front-end-pipelines#node-versions) |
