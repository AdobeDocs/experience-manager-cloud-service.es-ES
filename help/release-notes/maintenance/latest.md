---
title: Notas de la versión actuales sobre el mantenimiento de [!DNL Adobe Experience Manager] as a Cloud Service.
description: Notas de la versión actuales sobre el mantenimiento de [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 33468de99a3e77539f4bdc9435324c9f52a45d9f
workflow-type: tm+mt
source-wordcount: '350'
ht-degree: 67%

---


# Notas de la versión de mantenimiento {#maintenance-release-notes}

En la siguiente sección se describen las notas de la versión técnicas actuales sobre el mantenimiento de Experience Manager as a Cloud Service.

## Versión 22171 {#22171}

A continuación se resumen las mejoras continuas para la versión de mantenimiento 22171, que se publicó el miércoles, 02 de septiembre de 2025. La versión de mantenimiento anterior fue la 21994.

La activación de funcionalidades 2025.9.0 proporciona el conjunto completo de funcionalidades para esta versión de mantenimiento. Consulte la [Hoja de ruta de versiones de Experience Manager](https://experienceleague.adobe.com/es/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap) para obtener más información.

### Nuevas funciones  {#new-features-22171}

* ASSETS-53136: Compatibilidad con ID mnemónicos en Dynamic Media con OpenAPI.

### Mejoras {#enhancements-22171}

Ninguna.

### Problemas corregidos {#fixed-issues-22171}

* ASSETS-52510: Error al detectar nombres de archivo duplicados para los nombres de archivo que contienen Unicode `U+202F`.
* ASSETS-53489: La eliminación de carpetas de la IU de vista de Assets no desaprueba todos los recursos contenidos.
* ASSETS-54821: &quot;Error de servidor&quot; intermitente en Asset Link.
* ASSETS-55024: Imagen rota en la plantilla &quot;Descargar por correo electrónico&quot; de los AEM Assets.
* ASSETS-55325: Las direcciones URL estáticas de Dynamic Media omiten la extensión de archivo después de cambiar el nombre de los recursos.
* ASSETS-55334: el cuadro de diálogo Compartir vínculos parpadea brevemente y desaparece o no aparece nunca.
* ASSETS-55382: los trabajos de recursos asincrónicos reiniciados crean una carpeta de destino duplicada.
* ASSETS-55472: se ha omitido la opción Administrar publicación &quot;Incluir solo las páginas ya publicadas&quot;.
* SITES-31600: error de Contexthub.js al romper la personalización.

Para obtener más información sobre las funciones nuevas y mejoradas y los problemas corregidos en la versión, consulte la [hoja de ruta de la versión de Experience Manager Guides](https://experienceleague.adobe.com/es/docs/experience-manager-guides/using/release-info/aem-guides-releases-roadmap).

### Problemas conocidos {#known-issues-22171}

Ninguna.

### Características y API obsoletas {#deprecated-22171}

Las funciones y API obsoletas y eliminadas de AEM as a Cloud Service se detallan en el documento [Funciones y API obsoletas y eliminadas](/help/release-notes/deprecated-removed-features.md).

### Correcciones de seguridad {#security-22171}

AEM as a Cloud Service se dedica a optimizar la seguridad y el rendimiento de su plataforma. Esta versión de mantenimiento aborda 7 vulnerabilidades identificadas, reforzando nuestro compromiso con una sólida protección del sistema.

### Tecnologías integradas {#embedded-tech-22171}

| Tecnología | Versión | Vínculo |
|---|---|---|
| AEM Oak | 1.84.0 | [API Oak 1.84.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.84/index.html) |
| API AEM SLING | 2.27.6 | [API de Apache Sling 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.28-1.4.0 | [Especificación de idioma de la plantilla HTML](https://github.com/adobe/htl-spec) |
| Apache HTTP Server | 2.4.65 | [Apache Httpd 2.4.65](https://apache.googlesource.com/httpd/+/refs/tags/2.4.65/CHANGES) |
| Componentes principales de AEM | 2.29.0 | [Componentes principales de WCM AEM](https://github.com/adobe/aem-core-wcm-components) |
| Node.js | 14 (valor predeterminado) | [Versiones de Node.js compatibles](https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/implementing/developing/developing-with-front-end-pipelines#node-versions) |
