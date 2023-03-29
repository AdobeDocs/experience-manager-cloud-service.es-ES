---
title: Notas de la versión de mantenimiento actual de [!DNL Adobe Experience Manager] as a Cloud Service.
description: Notas de la versión de mantenimiento actual de [!DNL Adobe Experience Manager] as a Cloud Service.
source-git-commit: 7e66c9f26211bd92119c74f311f3e9b3195a8d98
workflow-type: tm+mt
source-wordcount: '265'
ht-degree: 36%

---


# Notas de la versión de mantenimiento {#maintenance-release-notes}

En la siguiente sección se describen las notas de la versión técnica de la versión de mantenimiento actual de Experience Manager as a Cloud Service.

## Versión 11382 {#release-11382}

A continuación se resumen las mejoras continuas de la versión de mantenimiento 11382, que se publicó el 28 de marzo de 2023. Esta versión de mantenimiento es una actualización de la versión de mantenimiento 11289 anterior.

La activación de funcionalidades para esta versión de mantenimiento le proporcionará el conjunto completo de funcionalidades. Consulte las [notas de la versión actual](/help/release-notes/release-notes-cloud/release-notes-current.md) para obtener información detallada.

### Problemas corregidos {#fixed-issues}

- ASSETS-21023 - Se ha corregido la representación de Recorte inteligente, en la que los clientes podían observar una excepción de puntero nulo en la instancia de Editor de todos los entornos de AEM cuando intentaban acceder a estas representaciones a través de la API.
- SKYOPS-49280 - Al instalar una actualización de configuración o paquete utilizando RDE en Publish, puede que el resultado no se pueda observar porque la caché de Publish Dispatcher no está invalidada

#### Sites {#sites-issues}

- SITES-7796 - Capacidad para que el autor de contenido publique el fragmento de contenido maestro y sus variaciones respectivas al exportar a destino

#### Assets {#assets-issues}

- ASSETS-20076: Añada compatibilidad con la marca de agua de vídeo que coincida con la compatibilidad actual con la marca de agua de imágenes
- ASSETS-21428: Exclusiones añadidas para cambios en CSS

#### Forms {#forms-issues}

- CQ-4351502 - Actualización de la asignación de usuarios del servicio para permitir el acceso de lectura en Sites

#### Plataforma {#platform-issues}

- SITES-11040 - Habilitación condicional del almacenamiento en caché de consultas persistentes de GraphQL en Dispatcher

### Tecnologías integradas {#embedded-tech}

| Tecnología | Versión | Vínculo |
|---|---|---|
| AEM OAK | 1,44-T20221206170501-6d59064 | [API Oak 1.44.0](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.44.0/index.html) |
| API AEM SLING | Versión 2.27.0 | [API de Apache Sling 2.27.0](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | Versión 1.4.20-1.4.0 | [Especificación de idioma de la plantilla HTML](https://github.com/adobe/htl-spec) |
| Los componentes principales de AEM | Versión 2.21.2 | [Componentes principales de WCM de AEM](https://github.com/adobe/aem-core-wcm-components) |
