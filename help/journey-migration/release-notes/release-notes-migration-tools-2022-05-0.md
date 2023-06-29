---
title: AEM Notas de la versión de las herramientas de migración de la versión as a Cloud Service 2022.5.0 de
description: AEM Notas de la versión de las herramientas de migración de la versión as a Cloud Service 2022.5.0 de
feature: Release Information
exl-id: 1aa49e85-1914-44d9-bcf7-0a1b03926df0
source-git-commit: 1994b90e3876f03efa571a9ce65b9fb8b3c90ec4
workflow-type: tm+mt
source-wordcount: '398'
ht-degree: 5%

---

# AEM Notas de la versión de las herramientas de migración de la versión as a Cloud Service 2022.5.0 de {#release-notes}

AEM Esta página describe las notas de la versión para las herramientas de migración de as a Cloud Service 2022.5.0.

## Analizador de prácticas recomendadas {#bpa-release}

### Fecha de la versión {#release-date-bpa}

La fecha de lanzamiento del Analizador de prácticas recomendadas v2.1.30 es el 1 de junio de 2022.

### Novedades {#what-is-new-bpa}

* Capacidad para detectar e informar sobre el uso de widgets de diálogo personalizados con widgets de diálogo clásicos y de CoralUI. Se recomienda convertir los widgets de diálogo clásicos personalizados de ExtJS a CoralUI. Los widgets de diálogo personalizados de Coral deben actualizarse a CoralUI3.
* Capacidad para detectar e informar sobre el uso y la versión de Assets Share Commons. AEM El uso compartido de recursos Commons 1.x no es compatible con el as a Cloud Service de recursos de y debe actualizarse a 2.x.
* Capacidad para detectar y crear informes sobre la cantidad de nodos de las versiones.
* Capacidad para detectar e informar sobre agentes de replicación personalizados o agentes de replicación listos para usar que se han modificado.

### Correcciones de errores {#bug-fixes-bpa}

* BPA informaba de hallazgos de NCC (cambios no compatibles), UMI (problema de configuración incorrecta de la actualización) y PCX (complejidad de la página) que son falsos positivos. Se han corregido.
* BPA informaba de errores cuando cualquier longitud de nombre de nodo superaba los 150 bytes. Esto se ha corregido para detectar estos errores solo cuando la ruta principal del nodo es igual o mayor de 350 bytes.

## Herramienta de transferencia de contenido {#ctt-release}

### Fecha de la versión {#release-date-ctt}

La fecha de lanzamiento de la herramienta de transferencia de contenido v2.0.10 es el 2 de junio de 2022.

### Novedades {#what-is-new-ctt}

* La herramienta de transferencia de contenido (CTT) se ha desarrollado para trabajar con Cloud Acceleration Manager y optimizar todo el proceso de transferencia de contenido. Ahora, CTT se centra en realizar extracciones de contenido. El servicio de ingesta de CTT ahora está integrado en Cloud Acceleration Manager. Los beneficios que se proporcionan a través de esta evolución son:
   * Forma de autoservicio de extraer un conjunto de migración una vez e introducirlo en varios entornos en paralelo.
   * Se ha mejorado la experiencia del usuario mediante mejores estados de carga, protecciones y administración de errores.
   * Los registros de ingesta se mantienen y siempre están disponibles para la resolución de problemas.

## Cloud Acceleration Manager {#cam-release}

### Fecha de lanzamiento {#release-date-cam}

La fecha de lanzamiento de Cloud Acceleration Manager es el 2 de junio de 2022.

### Novedades {#what-is-new-cam}

* AEM AEM Cloud Acceleration Manager ahora proporciona a los usuarios el inicio y la administración de transferencias de contenido para mover contenido de la instancia de un cliente (On-Premise o Adobe Managed Services) a las instancias as a Cloud Service de un cliente como parte de un proyecto de migración. Consulte [Uso de la tarjeta de transferencia de contenido](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-acceleration-manager/using-cam/cam-implementation-phase.html#content-transfer) para obtener más información.
