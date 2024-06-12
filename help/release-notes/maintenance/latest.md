---
title: Notas de la versión actuales sobre el mantenimiento de [!DNL Adobe Experience Manager] as a Cloud Service.
description: Notas de la versión actuales sobre el mantenimiento de [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: c969b78f5e93e15d1f8f57dd409e58a6275069ce
workflow-type: ht
source-wordcount: '422'
ht-degree: 100%

---

# Notas de la versión de mantenimiento {#maintenance-release-notes}

En la siguiente sección se describen las notas de la versión técnicas actuales sobre el mantenimiento de Experience Manager as a Cloud Service.

## Versión 16544 {#release-16544}

A continuación, se resumen las mejoras continuas para la versión de mantenimiento 16544, que se publicó el 4 de junio de 2024. La versión de mantenimiento anterior fue la 16461.

La activación de funcionalidades 2024.6.0 proporcionará el conjunto completo de funcionalidades para esta versión de mantenimiento. Consulte la [Hoja de ruta de versiones de Experience Manager](https://experienceleague.adobe.com/es/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap) para obtener más información.

>[!CAUTION]
>
>Utilice el SDK al que se hace referencia aquí, ya que se ha confirmado una regresión con el SDK anterior:
>`AEM SDK v2024.06.16647.20240607T103723Z-240500`

### Mejoras {#enhancements-16544}

* GRANITE-41133: admite la API Jakarta Servlet 5 y la API OSGi Servlet Whiteboard.
* GRANITE-51355: pone en desuso org.slf4j.event.
* GRANITE-51565: AEM pierde la relación de grupo local con el grupo externo cuando el grupo local se publica desde AEM.
* GRANITE-51707: establece la cookie saml_request_path durante el redireccionamiento de http para autenticación.
* GRANITE-52010: actualiza la versión de Jackrabbit a 2.20.16.
* GRANITE-52057: actualiza Filevault a 3.7.3-T20240514105118-694f6aea solucionando JCRVLT-745.
* SKYOPS-35998: actualiza las dependencias “Sling RepoInit”: Repoinit Parser 1.9.0, Repoinit JCR 1.1.46.

### Problemas solucionados {#fixed-issues-16544}

* GRANITE-51375: idp-sync emite NPE si no se especifica ninguna ruta intermedia.
* GUIDES-17171: la operación de copiar y pegar de temas que superan los 15 KB falla con un error inesperado.
* GUIDES-17088: la funcionalidad para cambiar el estado del documento desde el panel **Propiedades de archivo** no funciona correctamente y cambia al estado *Borrador*.
* GUIDES-16931: las imágenes vinculadas de los temas no aparecen en la línea de base después de la creación de la versión.
* GUIDES-16896: los paneles de contenidos reutilizables no enumeran elementos cuando las **Preferencias de usuario** están configuradas para ver archivos por **Nombre de archivo**.

Para obtener más información sobre las funciones nuevas y mejoradas y los problemas corregidos en Experience Manager Guides, consulte la [hoja de ruta de la versión de Experience Manager Guides](https://experienceleague.adobe.com/es/docs/experience-manager-guides/using/release-info/aem-guides-releases-roadmap).

### Problemas conocidos {#known-issues-16544}

* GRANITE-52573: las solicitudes que contienen una barra doble `//` se rechazan con el código de estado 400. Este comportamiento se revertirá en una versión de mantenimiento posterior.

### Aviso de cambio {#change-notice-16544}

A partir de septiembre de 2024, AEM as a Cloud Service deshabilitará la serialización de los solucionadores de recursos a través del marco de trabajo Exportador de modelos Sling. Consulte la [documentación](/help/implementing/developing/hybrid/disallow-the-serialization-of-resourceresolvers-via-sling-model-exporter.md) para obtener más información.

### Características y API obsoletas {#deprecated-16544}

Para saber qué es lo que está en desuso o se ha eliminado en AEM as a Cloud Service, consulte [Funciones y API obsoletas y eliminadas](/help/release-notes/deprecated-removed-features.md).

### Tecnologías integradas {#embedded-tech-16544}

| Tecnología | Versión | Vínculo |
|---|---|---|
| AEM Oak | 1.64.0 | [API Oak 1.64.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.64.0/index.html) |
| API AEM SLING | 2.27.2 | [API de Apache Sling 2.27.2 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.22-1.4.0 | [Especificación de idioma de la plantilla HTML](https://github.com/adobe/htl-spec) |
| Los componentes principales de AEM | 2.25.4 | [Componentes principales de WCM AEM](https://github.com/adobe/aem-core-wcm-components) |
