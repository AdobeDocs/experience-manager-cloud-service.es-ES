---
title: Notas de la versión de las herramientas de migración de la versión 2023.03.0 de AEM as a Cloud Service
description: Notas de la versión de las herramientas de migración de la versión 2023.03.0 de AEM as a Cloud Service
feature: Release Information
exl-id: cdc57cca-e10a-4b0d-b803-910ccc9350a6
role: Admin
source-git-commit: fecbebde808c545a84889da5610a79c088f2f459
workflow-type: tm+mt
source-wordcount: '297'
ht-degree: 21%

---

# Notas de la versión de las herramientas de migración de la versión 2023.03.0 de AEM as a Cloud Service {#release-notes}

Esta página describe las notas de la versión de las herramientas de migración de AEM as a Cloud Service 2023.03.0.

## Analizador de prácticas recomendadas {#bpa-release}

### Fecha de la versión {#release-date-bpa}

La fecha de lanzamiento del Analizador de prácticas recomendadas v2.1.40 es el 3 de marzo de 2023.

### Novedades {#what-is-new-bpa}

* Ahora, BPA puede detectar y crear informes sobre nodos en conflicto: nodos con el mismo `jcr:uuid`. Estos resultados se marcan como críticos, ya que pueden provocar errores de ingesta de contenido al mover contenido a AEM as a Cloud Service.
* Ahora, BPA puede detectar e informar sobre el uso de detectores de eventos. Se recomienda refactorizar este tipo de mecanismo de gestión de eventos a los trabajos de Sling al pasar a AEM as a Cloud Service.

### Correcciones de errores {#bug-fixes-bpa}

* BPA informaba de falsos positivos en `grouprendercondition`. Esto se ha corregido.

## Herramienta de transferencia de contenido {#ctt-release}

### Fecha de la versión {#release-date-ctt}

La fecha de versión de la herramienta de transferencia de contenido v2.0.16 es el 8 de marzo de 2023.

### Novedades {#what-is-new-ctt}

* La asignación de usuarios se ha optimizado e integrado en el paso de extracción de contenido. No es necesario realizar ninguna configuración y, de forma predeterminada, la asignación de usuarios se realiza automáticamente cuando el usuario inicia la extracción de contenido. El usuario tiene la opción de deshabilitar la asignación de usuarios si es necesario.
* El paso de precopia usando [AzCopy](https://learn.microsoft.com/en-us/azure/storage/common/storage-use-azcopy-v10) se ha integrado con la herramienta de transferencia de contenido para acelerar las extracciones de contenido de manera significativa. La precopia se configura e instala automáticamente cuando se instala esta versión de CTT. De forma predeterminada, cuando se inicia la extracción, la precopia se ejecutará automáticamente para los conjuntos de migración de más de 200 GB. El usuario tiene la opción de desactivarla si es necesario. Más información [aquí](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/handling-large-content-repositories.html).
* Ahora, CTT se puede utilizar en servidores de Windows.

### Correcciones de errores {#bug-fixes-ctt}

* Varias correcciones de errores para mejorar la resistencia de la extracción de contenido.
