---
title: Notas de la versión actuales sobre el mantenimiento de [!DNL Adobe Experience Manager] as a Cloud Service.
description: Notas de la versión actuales sobre el mantenimiento de [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: ff500e08e31e53f5452eed6cfe06539cabe2ecdd
workflow-type: tm+mt
source-wordcount: '366'
ht-degree: 62%

---


# Notas de la versión de mantenimiento {#maintenance-release-notes}

En la siguiente sección se describen las notas de la versión técnicas actuales sobre el mantenimiento de Experience Manager as a Cloud Service.

## Versión 21484 {#21484}

A continuación se resumen las mejoras continuas para la versión de mantenimiento 21484, que se publicó el miércoles, 08 de julio de 2025. La versión de mantenimiento anterior fue la 21331.

La activación de funcionalidades 2025.7.0 proporciona el conjunto completo de funcionalidades para esta versión de mantenimiento. Consulte la [Hoja de ruta de versiones de Experience Manager](https://experienceleague.adobe.com/es/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap) para obtener más información.

### Mejoras {#enhancements-21484}

Ninguna.

### Problemas corregidos {#fixed-issues-21484}

Ninguna.

#### Guías de AEM {#guides-21484}

* GUIDES-29781: cuando se agrega un comentario XML dentro de un elemento en la vista de Source, los espacios iniciales y finales alrededor del comentario se pierden al cambiar de vista.
* GUIDES-29078: al abrir un tema en la vista Autor después de actualizar el explorador, las etiquetas aplicadas anteriormente en el panel Propiedades del archivo no se conservan y la adición de nuevas etiquetas sobrescribe las existentes, especialmente cuando hay un gran número de etiquetas disponibles para su selección.
* GUIDES-28214: Los intentos de crear tareas de revisión a través del flujo de trabajo de AEM fallan de forma consistente porque no se crea el nodo de revisión.
* GUIDES-28104: al publicar un mapa DITA con el atributo `chunk=to-content`, se crean nodos JCR duplicados en la nueva salida de AEM Sites, lo que da como resultado una estructura de contenido redundante en AEM Sites.
* GUIDES-29065, GUIDES-28793: Los problemas de rendimiento como tiempos de carga más largos y tiempos de espera intermitentes se observan al trabajar con colecciones grandes.

Para obtener más información sobre las funciones nuevas y mejoradas y los problemas corregidos en la versión, consulte la [hoja de ruta de la versión de Experience Manager Guides](https://experienceleague.adobe.com/es/docs/experience-manager-guides/using/release-info/aem-guides-releases-roadmap).

### Problemas conocidos {#known-issues-21484}

Ninguna.

### Características y API obsoletas {#deprecated-21484}

Las funciones y API obsoletas y eliminadas de AEM as a Cloud Service se detallan en el documento [Funciones y API obsoletas y eliminadas](/help/release-notes/deprecated-removed-features.md).

### Correcciones de seguridad {#security-21484}

AEM as a Cloud Service se dedica a optimizar la seguridad y el rendimiento de su plataforma. Esta versión de mantenimiento aborda 5 vulnerabilidades identificadas, reforzando nuestro compromiso con una sólida protección del sistema.

### Tecnologías integradas {#embedded-tech-21484}

| Tecnología | Versión | Vínculo |
|---|---|---|
| AEM Oak | 1.80.0 | [API Oak 1.80.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.80.0/index.html) |
| API AEM SLING | 2.27.6 | [API de Apache Sling 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.28-1.4.0 | [Especificación de idioma de la plantilla HTML](https://github.com/adobe/htl-spec) |
| Los componentes principales de AEM | 2.29.0 | [Componentes principales de WCM AEM](https://github.com/adobe/aem-core-wcm-components) |
