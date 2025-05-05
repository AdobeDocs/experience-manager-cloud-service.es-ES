---
title: Notas de la versión para las herramientas de migración en la versión 2022.5.0 de AEM as a Cloud Service
description: Notas de la versión para las herramientas de migración en la versión 2022.5.0 de AEM as a Cloud Service
feature: Release Information
exl-id: 1aa49e85-1914-44d9-bcf7-0a1b03926df0
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '399'
ht-degree: 5%

---

# Notas de la versión para las herramientas de migración en la versión 2022.5.0 de AEM as a Cloud Service {#release-notes}

Esta página describe las notas de la versión de las herramientas de migración de AEM as a Cloud Service 2022.5.0.

## Analizador de prácticas recomendadas {#bpa-release}

### Fecha de la versión {#release-date-bpa}

La fecha de lanzamiento del Analizador de prácticas recomendadas v2.1.30 es el 1 de junio de 2022.

### Novedades {#what-is-new-bpa}

* Capacidad para detectar e informar sobre el uso de widgets de diálogo personalizados con widgets de diálogo clásicos y de CoralUI. Se recomienda convertir los widgets de diálogo clásicos personalizados de ExtJS a CoralUI. Los widgets de diálogo personalizados de Coral deben actualizarse a CoralUI3.
* Capacidad para detectar e informar sobre el uso y la versión de Assets Share Commons. Uso compartido de recursos Commons 1.x no es compatible con AEM as a Cloud Service y debe actualizarse a 2.x.
* Capacidad para detectar y crear informes sobre la cantidad de nodos de las versiones.
* Capacidad para detectar e informar sobre agentes de replicación personalizados o agentes de replicación listos para usar que se han modificado.

### Correcciones de errores {#bug-fixes-bpa}

* BPA informaba de hallazgos de NCC (cambios no compatibles), UMI (problema de configuración incorrecta de la actualización) y PCX (complejidad de la página) que son falsos positivos. Se han corregido.
* BPA informaba de errores cuando cualquier longitud de nombre de nodo superaba los 150 bytes. Esto se ha corregido para detectar estos errores solo cuando la ruta principal del nodo es igual o mayor de 350 bytes.

## Herramienta de transferencia de contenido {#ctt-release}

### Fecha de la versión {#release-date-ctt}

La fecha de lanzamiento de la herramienta de transferencia de contenido v2.0.10 es el 2 de junio de 2022.

### Novedades {#what-is-new-ctt}

* La herramienta de transferencia de contenido (CTT) se ha desarrollado para trabajar con Cloud Acceleration Manager y optimizar todo el proceso de transferencia de contenido. Ahora, CTT se centra en realizar extracciones de contenido. El servicio de ingesta CTT ahora está integrado en Cloud Acceleration Manager. Los beneficios que se proporcionan a través de esta evolución son:
   * Forma de autoservicio de extraer un conjunto de migración una vez e introducirlo en varios entornos en paralelo.
   * Se ha mejorado la experiencia del usuario mediante mejores estados de carga, protecciones y administración de errores.
   * Los registros de ingesta se mantienen y siempre están disponibles para la resolución de problemas.

## Cloud Acceleration Manager {#cam-release}

### Fecha de lanzamiento {#release-date-cam}

La fecha de lanzamiento de Cloud Acceleration Manager es el 2 de junio de 2022.

### Novedades {#what-is-new-cam}

* Cloud Acceleration Manager AEM ahora proporciona a los usuarios el inicio y la administración de transferencias de contenido para mover contenido de la instancia de de un cliente (On-Premise o Adobe Managed Services) a AEM as a Cloud Service como parte de un proyecto de migración. Consulte [Usar la tarjeta de transferencia de contenido](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-acceleration-manager/using-cam/cam-implementation-phase.html?lang=es#content-transfer) para obtener más información.
