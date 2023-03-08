---
title: Últimas notas de la versión de mantenimiento de [!DNL Adobe Experience Manager] as a Cloud Service.
description: Últimas notas de la versión de mantenimiento de [!DNL Adobe Experience Manager] as a Cloud Service.
source-git-commit: edb8949b532b80a55106e706a49e2ada68722a67
workflow-type: tm+mt
source-wordcount: '303'
ht-degree: 6%

---


# Notas de la versión de mantenimiento {#maintenance-release-notes}

En la siguiente sección se describen las rutas técnicas de la última versión de mantenimiento de Experience Manager as a Cloud Service.

## 11289 de versión {#release-11289}

A continuación se resumen las mejoras continuas para la 11289 de la versión de mantenimiento, que se publicó el 7 de marzo de 2023. Esta versión de mantenimiento es una actualización de versiones de mantenimiento 10912.

La activación de funciones para esta versión de mantenimiento le proporcionará el conjunto completo de funciones. Consulte la [notas de la versión actual](/help/release-notes/release-notes-cloud/release-notes-current.md) para obtener información detallada.

### Problemas conocidos {#known-issues}

No actualice si utiliza CORS. En esta versión se identificó un problema que afectaba a la funcionalidad de entrega de contenido de GraphQL. AEM Un cambio en la configuración predeterminada de Dispatcher con respecto a cómo se almacenan en caché las consultas persistentes de GraphQL puede interrumpir la entrega de contenido de GraphQL de dichas consultas. Este problema se solucionará en la próxima versión de mantenimiento.

### Problemas solucionados {#fixed-issues}

#### Sites {#sites-issues}

- SITES-11584 Se ha corregido un problema con Live Copies que no se podía crear para páginas con anotaciones
- Live Copies MSM deshabilitadas 11683 SITES con herencia parcialmente dañada

#### Assets {#assets-issues}

- RECURSOS-20879 Se ha corregido la regresión que impedía que la IU de los informes de recursos funcionara correctamente y daba como resultado resultados incorrectos en los informes generados.
- ASSETS-21020 Se ha corregido un problema con la descarga de recursos dañada: el perfil de imagen no existe después de mover el recurso
- ASSETS-21023 Se ha corregido un problema con las representaciones de imágenes en Dynamic Media que impedía el acceso a través de la API

#### Forms {#forms-issues}

- Ninguno

#### Plataforma {#platform-issues}

- GRANITE-44467: se ha corregido un problema que provocaba que fallara la importación, al actualizar un nodo existente, Filevault en determinadas instancias no conservaba los tipos de mezcla y los nodos secundarios

### Tecnologías integradas {#embedded-tech}

| Tecnología | Versión | Vínculo |
|---|---|---|
| AEM OAK DE LA | 1,44-T20221206170501-6d59064 | [API de Oak 1.44.0](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.44.0/index.html) |
| AEM API DE SLING | Versión 2.27.0 | [API de Apache Sling 2.27.0](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL DE LA | Versión 1.4.20-1.4.0 | [Especificación del lenguaje de plantilla de HTML](https://github.com/adobe/htl-spec) |
| AEM Core Components | Versión 2.21.2 | [AEM Componentes principales de WCM](https://github.com/adobe/aem-core-wcm-components) |
