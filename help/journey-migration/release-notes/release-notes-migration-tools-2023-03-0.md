---
title: AEM Notas de la versión de las herramientas de migración de la versión as a Cloud Service 2023.03.0 de
description: AEM Notas de la versión de las herramientas de migración de la versión as a Cloud Service 2023.03.0 de
feature: Release Information
exl-id: cdc57cca-e10a-4b0d-b803-910ccc9350a6
source-git-commit: ecf4c06fd290d250c14386b3135250633b26c910
workflow-type: tm+mt
source-wordcount: '301'
ht-degree: 7%

---

# AEM Notas de la versión de las herramientas de migración de la versión as a Cloud Service 2023.03.0 de {#release-notes}

AEM Esta página describe las notas de la versión de las herramientas de migración en la versión as a Cloud Service 2023.03.0 de.

## Analizador de prácticas recomendadas {#bpa-release}

### Fecha de la versión {#release-date-bpa}

La fecha de lanzamiento del Analizador de prácticas recomendadas v2.1.40 es el 3 de marzo de 2023.

### Novedades {#what-is-new-bpa}

* Ahora, BPA puede detectar y crear informes sobre nodos en conflicto: nodos con el mismo `jcr:uuid`. AEM Estos hallazgos se marcan como críticos, ya que pueden provocar errores de ingesta de contenido al mover contenido a la posición as a Cloud Service.
* Ahora, BPA puede detectar e informar sobre el uso de detectores de eventos. AEM Se recomienda refactorizar este tipo de mecanismo de gestión de eventos a los trabajos de sling al pasar a as a Cloud Service.

### Correcciones de errores {#bug-fixes-bpa}

* BPA informaba de falsos positivos en `grouprendercondition`. Esto se ha corregido.

## Herramienta de transferencia de contenido {#ctt-release}

### Fecha de la versión {#release-date-ctt}

La fecha de versión de la herramienta de transferencia de contenido v2.0.16 es el 8 de marzo de 2023.

### Novedades {#what-is-new-ctt}

* La asignación de usuarios se ha optimizado e integrado en el paso de extracción de contenido. No es necesario realizar ninguna configuración y, de forma predeterminada, la asignación de usuarios se realiza automáticamente cuando el usuario inicia la extracción de contenido. El usuario tiene la opción de deshabilitar la asignación de usuarios si es necesario. Más información [aquí.](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/user-mapping-and-migration.html#user-mapping-detail)
* El paso de precopia mediante [AzCopy](https://learn.microsoft.com/en-us/azure/storage/common/storage-use-azcopy-v10) se ha integrado con la herramienta de transferencia de contenido para acelerar significativamente las extracciones de contenido. La precopia se configura e instala automáticamente cuando se instala esta versión de CTT. De forma predeterminada, cuando se inicia la extracción, la precopia se ejecutará automáticamente para los conjuntos de migración de más de 200 GB. El usuario tiene la opción de desactivarla si es necesario. Más información [aquí.](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/handling-large-content-repositories.html)
* Ahora, CTT se puede utilizar en servidores de Windows.

### Correcciones de errores {#bug-fixes-ctt}

* Varias correcciones de errores para mejorar la resistencia de la extracción de contenido.
