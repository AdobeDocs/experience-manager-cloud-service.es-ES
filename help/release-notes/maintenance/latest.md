---
title: Notas de la versión actuales sobre el mantenimiento de [!DNL Adobe Experience Manager] as a Cloud Service.
description: Notas de la versión actuales sobre el mantenimiento de [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
source-git-commit: 558babc0124a8ee8c1337b91c5ef016ed238c935
workflow-type: tm+mt
source-wordcount: '337'
ht-degree: 48%

---

# Notas de la versión de mantenimiento {#maintenance-release-notes}

En la siguiente sección se describen las notas de la versión técnicas actuales sobre el mantenimiento de Experience Manager as a Cloud Service.

## Versión 16544 {#release-16544}

A continuación, se resumen las mejoras continuas para la versión de mantenimiento 16544, que se publicó el miércoles, 04 de junio de 2024. La versión de mantenimiento anterior fue la 16461.

La activación de funcionalidades 2024.6.0 proporcionará el conjunto completo de funcionalidades para esta versión de mantenimiento. Consulte la [Hoja de ruta de versiones de Experience Manager](https://experienceleague.adobe.com/es/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap) para obtener más información.

### Mejoras {#enhancements-16544}

* GRANITE-41133: admite la API de servlet de Jakarta 5 y la API de pizarra electrónica de servlet OSGi.
* GRANITE-51355: Obsoleto org.slf4j.event.
* AEM AEM GRANITE-51565: La pierde la relación de grupo local con el grupo externo cuando el grupo local se publica desde la publicación de un grupo de un grupo de un grupo de un grupo de un grupo de un grupo de un grupo de un grupo de un grupo de un grupo de un grupo local de un grupo de un grupo de un grupo de.
* GRANITE-51707: establezca la cookie saml_request_path durante el redireccionamiento http para la autenticación.
* GRANITE-52010: Actualice la versión de Jackrabbit a 2.20.16.
* GRANITE-52057: Actualice Filevault a 3.7.3-T20240514105118-694f6aea fijando JCRVLT-745.
* SKYOPS-35998: Actualizar dependencias de &quot;Sling RepoInit&quot; : Repoinit Parser 1.9.0, Repoinit JCR 1.1.46.

### Problemas solucionados {#fixed-issues-16544}

* AEM DXML-17171: Guías de la: La operación de copiar y pegar de temas que exceden los 15 KB falla con un error inesperado.
* AEM DXML-17088: Guías de la aplicación: la funcionalidad para cambiar el estado del documento desde el **Propiedades de archivo** el panel no funciona correctamente y cambia al *Borrador* estado.
* AEM DXML-16931: Guías de: Las imágenes vinculadas de los temas no aparecen en la línea de base después de la creación de la versión.
* AEM DXML-16896: Guías de la aplicación: Los paneles de contenido reutilizables no enumeran elementos cuando la variable **Preferencias de usuario** están configurados para ver archivos por **Nombre de archivo**.
* GRANITE-51375: idp-sync emite NPE si no se especifica ninguna ruta intermedia.

### Problemas conocidos {#known-issues-16544}

Ninguna.

### Características y API obsoletas {#deprecated-16544}

Para saber qué es lo que está en desuso o se ha eliminado en AEM as a Cloud Service, consulte [Funciones y API obsoletas y eliminadas](/help/release-notes/deprecated-removed-features.md).

### Tecnologías integradas {#embedded-tech-16544}

| Tecnología | Versión | Vínculo |
|---|---|---|
| AEM Oak | 1.64.0 | [API Oak 1.64.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.64.0/index.html) |
| API AEM SLING | 2.27.2 | [API de Apache Sling 2.27.2 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.22-1.4.0 | [Especificación de idioma de la plantilla HTML](https://github.com/adobe/htl-spec) |
| Los componentes principales de AEM | 2.25.4 | [Componentes principales de WCM AEM](https://github.com/adobe/aem-core-wcm-components) |
