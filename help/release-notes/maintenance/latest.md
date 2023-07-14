---
title: Notas de la versión actuales sobre el mantenimiento de [!DNL Adobe Experience Manager] as a Cloud Service.
description: Notas de la versión actuales sobre el mantenimiento de [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
source-git-commit: 241dcc75e9f2c840be85c34800d8145457baa58d
workflow-type: tm+mt
source-wordcount: '272'
ht-degree: 43%

---

# Notas de la versión de mantenimiento {#maintenance-release-notes}

En la siguiente sección se describen las notas de la versión técnicas actuales sobre el mantenimiento de Experience Manager as a Cloud Service.

## Versión 12697 {#release-12697}

A continuación se resumen las mejoras continuas para la 12697 de la versión de mantenimiento, que se publicó el 14 de julio de 2023. Esta versión de mantenimiento es una actualización de la versión de mantenimiento 12549 anterior. La 12697 de la versión de mantenimiento sustituye a la 12585 para corregir un problema.

La activación de funciones 2023.7.0 proporcionará el conjunto completo de funciones para esta versión de mantenimiento. Consulte la [Roadmap de versiones de Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html?lang=es) para obtener más información.

### Mejoras {#enhancements-12697}

- Mejoras generales de estabilidad RDE (SKYOPS-61133, SKYOPS-55281, SKYOPS-61216 y SKYOPS-61401)
- AEM DXML-12327: Guías para la creación de informes: Compatibilidad con variables de idioma en la publicación de PDF nativos
- AEM DXML-11518: Guías para la creación de informes: Compatibilidad con metadatos mejorada en la publicación de PDF nativos
- AEM DXML-10093: Guías para la administración de datos: Compatibilidad para conectar con fuentes de datos externas e insertar datos en temas de dita
- AEM DXML-10699: Guías de: Compatibilidad con el formato XLIFF en la traducción
- AEM DXML-10141: Guías para la creación de informes: Opción para utilizar la publicación basada en microservicios para tipos de ajustes preestablecidos de PDF (nativo y DITA-OT), HTML y Personalizado
- SKYOPS-61385: actualice el despachante para que utilice libpcre2 al evaluar expresiones regulares en Apache HTTPD

### Problemas corregidos {#fixed-issues-12697}

- AEM Guías de: varias mejoras y correcciones de estabilidad de PDF nativos
- SKYOPS-53130: Mejora el soporte de la herramienta de CA en RDE
- AEM SKYOPS-57146: Corregir el interbloqueo de Sling en el inicio de la

### Problemas conocidos {#known-issues-12697}

Ninguna.

### Tecnologías integradas {#embedded-tech-12697}

| Tecnología | Versión | Vínculo |
|---|---|---|
| AEM OAK | 1,52-T20230629133256-25c01b8 | [API Oak 1.52.0](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.52.0/index.html) |
| API AEM SLING | Versión 2.27.2 | [API de Apache Sling 2.27.2](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | Versión 1.4.20-1.4.0 | [Especificación de idioma de la plantilla HTML](https://github.com/adobe/htl-spec) |
| Los componentes principales de AEM | Versión 2.23.0 | [Componentes principales de WCM de AEM](https://github.com/adobe/aem-core-wcm-components) |
