---
title: Notas de la versión más recientes sobre el mantenimiento de [!DNL Adobe Experience Manager] as a Cloud Service.
description: Notas de la versión más recientes sobre el mantenimiento de [!DNL Adobe Experience Manager] as a Cloud Service.
source-git-commit: edb8949b532b80a55106e706a49e2ada68722a67
workflow-type: tm+mt
source-wordcount: '303'
ht-degree: 100%

---


# Notas de la versión de mantenimiento {#maintenance-release-notes}

En la siguiente sección se describen las notas técnicas de la versión de mantenimiento más reciente de Experience Manager as a Cloud Service.

## Versión 11289 {#release-11289}

A continuación, se resumen las mejoras continuas para la versión de mantenimiento 11289, que se publicó el 7 de marzo de 2023. Esta versión de mantenimiento es una actualización de la versión de mantenimiento anterior 10912.

La activación de funcionalidades para esta versión de mantenimiento le proporcionará el conjunto completo de funcionalidades. Consulte las [notas de la versión actual](/help/release-notes/release-notes-cloud/release-notes-current.md) para obtener información detallada.

### Problemas conocidos {#known-issues}

No actualice si utiliza CORS. En esta versión se identificó un problema que afectaba a la funcionalidad de entrega de contenido de GraphQL. Un cambio en la configuración predeterminada de Dispatcher de AEM con respecto a cómo se almacenan en caché las consultas persistentes de GraphQL puede interrumpir la entrega de contenido de GraphQL de dichas consultas. Este problema se solucionará en la próxima versión de mantenimiento.

### Problemas corregidos {#fixed-issues}

#### Sites {#sites-issues}

- SITES-11584 Se ha corregido un problema con Live Copies que no se podía crear para páginas con anotaciones
- SITES-11683 Se han deshabilitado Live Copies de MSM con herencia parcialmente dañada

#### Assets {#assets-issues}

- ASSETS-20879 Se ha corregido la regresión que impedía que la IU de los informes de recursos funcionara correctamente y daba como resultado resultados incorrectos en los informes generados.
- ASSETS-21020 Se ha corregido un problema con la descarga de recursos dañada: el perfil de imagen no existe después de mover el recurso
- ASSETS-21023 Se ha corregido un problema con las representaciones de imágenes en Dynamic Media que impedía el acceso a través de la API

#### Forms {#forms-issues}

- Ninguno

#### Plataforma {#platform-issues}

- GRANITE-44467 Se ha corregido un problema que provocaba que fallara la importación. Al actualizar un nodo existente, Filevault no conservaba, en determinadas instancias, los tipos de mezcla y los nodos secundarios

### Tecnologías integradas {#embedded-tech}

| Tecnología | Versión | Vínculo |
|---|---|---|
| AEM OAK | 1,44-T20221206170501-6d59064 | [API Oak 1.44.0](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.44.0/index.html) |
| API AEM SLING | Versión 2.27.0 | [API de Apache Sling 2.27.0](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | Versión 1.4.20-1.4.0 | [Especificación de idioma de la plantilla HTML](https://github.com/adobe/htl-spec) |
| Los componentes principales de AEM | Versión 2.21.2 | [Componentes principales de WCM de AEM](https://github.com/adobe/aem-core-wcm-components) |
