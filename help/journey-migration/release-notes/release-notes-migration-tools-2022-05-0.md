---
title: Notas de la versión de las herramientas de migración en AEM versión as a Cloud Service 2022.5.0
description: Notas de la versión de las herramientas de migración en AEM versión as a Cloud Service 2022.5.0
feature: Release Information
exl-id: 1aa49e85-1914-44d9-bcf7-0a1b03926df0
source-git-commit: 8b7427ff99343741f62c7d0f42a6c4b3ea19bcb3
workflow-type: tm+mt
source-wordcount: '399'
ht-degree: 5%

---

# Notas de la versión de las herramientas de migración en AEM versión as a Cloud Service 2022.5.0 {#release-notes}

Esta página describe las notas de la versión de las herramientas de migración en AEM as a Cloud Service 2022.5.0.

## Analizador de prácticas recomendadas {#bpa-release}

### Fecha de la versión {#release-date-bpa}

La fecha de versión de Best Practices Analyzer v2.1.30 es el 1 de junio de 2022.

### Novedades {#what-is-new-bpa}

* Capacidad para detectar e informar sobre el uso de las utilidades de diálogo personalizadas mediante las utilidades de diálogo CoralUI y Classic. Se recomienda convertir las utilidades de diálogo personalizadas Classic de ExtJS a CoralUI. Los widgets de diálogo de coral personalizados deben actualizarse a CoralUI3.
* Capacidad para detectar e informar sobre el uso y la versión de Assets Share Commons. Asset Share Commons 1.x no es compatible con AEM as a Cloud Service y debe actualizarse a 2.x.
* Capacidad para detectar e informar sobre la cantidad de nodos de las versiones.
* Capacidad para detectar y crear informes sobre agentes de replicación personalizados o agentes de replicación listos para usar que se hayan modificado.

### Correcciones de errores {#bug-fixes-bpa}

* BPA informaba de los resultados de NCC (cambios no compatibles), UMI (Problema de configuración incorrecta de la actualización) y PCX (Complejidad de la página) que son falsos positivos. Se han corregido.
* BPA informaba de errores cuando cualquier longitud de nombre de nodo excedía los 150 bytes. Esto se ha solucionado para detectar estos errores solo cuando la ruta principal del nodo es igual o mayor que 350 bytes.

## Herramienta de transferencia de contenido {#ctt-release}

### Fecha de la versión {#release-date-ctt}

La fecha de versión de la herramienta de transferencia de contenido v2.0.10 es el 2 de junio de 2022.

### Novedades {#what-is-new-ctt}

* La herramienta de transferencia de contenido (CTT) se ha desarrollado para funcionar con Cloud Acceleration Manager con el fin de optimizar todo el proceso de transferencia de contenido. CTT ahora se centra en realizar extracciones de contenido. El servicio de ingesta de CTT ahora está integrado en Cloud Acceleration Manager. Los beneficios que se proporcionan a través de esta evolución son:
   * Método de autoservicio para extraer un conjunto de migración una vez e introducirlo en varios entornos en paralelo.
   * Se ha mejorado la experiencia del usuario mediante una mejor carga de estados, protecciones y gestión de errores.
   * Los registros de ingesta se mantienen y siempre están disponibles para la resolución de problemas.

## Cloud Acceleration Manager {#cam-release}

### Fecha de la versión {#release-date-cam}

La fecha de versión de Cloud Acceleration Manager es el 2 de junio de 2022.

### Novedades {#what-is-new-cam}

* Cloud Acceleration Manager ahora proporciona a los usuarios el inicio y la administración de transferencias de contenido para mover contenido de la instancia de AEM de un cliente (local o Adobe Managed Services) a AEM as a Cloud Service como parte de un proyecto de migración. Consulte [Uso de la tarjeta de transferencia de contenido](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-acceleration-manager/using-cam/cam-implementation-phase.html#content-transfer) para obtener más información.
