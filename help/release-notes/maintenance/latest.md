---
title: Notas de la versión actuales sobre el mantenimiento de [!DNL Adobe Experience Manager] as a Cloud Service.
description: Notas de la versión actuales sobre el mantenimiento de [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
source-git-commit: cf8b5d8b11452268b2839053c1e05cc2ec107a91
workflow-type: tm+mt
source-wordcount: '222'
ht-degree: 53%

---

# Notas de la versión de mantenimiento {#maintenance-release-notes}

En la siguiente sección se describen las notas de la versión técnicas actuales sobre el mantenimiento de Experience Manager as a Cloud Service.

## Versión 13173 {#release-13173}

A continuación se resumen las mejoras continuas para la 13173 de la versión de mantenimiento, que se publicó el 18 de agosto de 2023. Esta versión de mantenimiento es una actualización de la versión de mantenimiento 13099 anterior.

La activación de funciones 2023.8.0 proporcionará el conjunto completo de funciones para esta versión de mantenimiento. Consulte la [Roadmap de versiones de Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html?lang=es) para obtener más información.

### Mejoras {#enhancements-13173}

Ninguna.

### Problemas corregidos {#fixed-issues-13173}

- SITES-15463: plantillas de sitios: las plantillas no se pueden publicar.

### Problemas conocidos {#known-issues-13173}

- SITES-15359: Fragmentos de contenido: el patrón de nombre de variación no coincide correctamente con las variaciones que tienen ```'_'``` en sus nombres de recursos.
- FORMS-10444: Plantillas de Forms adaptables: las plantillas no se pueden publicar (solución alternativa: utilice la consola de distribución).
- CQ-4354191: Flujos de trabajo: el iniciador personalizado puede entrar en déclencheur muchas veces debido a los metadatos de replicación presentes en los nodos nt:unstructured (solución alternativa: actualice los iniciadores para excluir las propiedades de metadatos de replicación para evitar la superposición).

### Tecnologías integradas {#embedded-tech-13173}

| Tecnología | Versión | Vínculo |
|---|---|---|
| AEM OAK | 1,52-T20230629133256-25c01b8 | [API Oak 1.52.0](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.52.0/index.html) |
| API AEM SLING | Versión 2.27.2 | [API de Apache Sling 2.27.2](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | Versión 1.4.20-1.4.0 | [Especificación de idioma de la plantilla HTML](https://github.com/adobe/htl-spec) |
| Los componentes principales de AEM | Versión 2.23.2 | [Componentes principales de WCM de AEM](https://github.com/adobe/aem-core-wcm-components) |
