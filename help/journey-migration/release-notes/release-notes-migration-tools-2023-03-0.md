---
title: AEM Notas de la versión de las herramientas de migración de la versión as a Cloud Service 2023.03.0 de
description: AEM Notas de la versión de las herramientas de migración de la versión as a Cloud Service 2022.03.0 de
feature: Release Information
source-git-commit: 70061cb1bbaab486f719541e919acb9e462d741c
workflow-type: tm+mt
source-wordcount: '321'
ht-degree: 9%

---

# AEM Notas de la versión de las herramientas de migración de la versión as a Cloud Service 2023.03.0 de {#release-notes}

AEM Esta página describe las notas de la versión de las herramientas de migración de la versión 2022.03.0 de as a Cloud Service.

## Analizador de prácticas recomendadas {#bpa-release}

### Fecha de la versión {#release-date-bpa}

El 03 de marzo de 2023 es la fecha de lanzamiento del Analizador de prácticas recomendadas versión 2.1.40.

### Novedades {#what-is-new-bpa}

* Ahora, BPA puede detectar y crear informes sobre nodos en conflicto: nodos con el mismo `jcr:uuid`. AEM Estos hallazgos se marcan como críticos, ya que pueden provocar errores de ingesta de contenido al mover contenido a la posición as a Cloud Service.
* Ahora, BPA puede detectar e informar sobre el uso de detectores de eventos. AEM Se recomienda refactorizar este tipo de mecanismo de gestión de eventos a los trabajos de sling al pasar a as a Cloud Service.

### Correcciones de errores {#bug-fixes-bpa}

* BPA informaba de falsos positivos en `grouprendercondition`. Esto se ha corregido.

## Herramienta de transferencia de contenido {#ctt-release}

### Fecha de la versión {#release-date-ctt}

La fecha de versión de la herramienta de transferencia de contenido v2.0.16 es el 8 de marzo de 2022.

### Novedades {#what-is-new-ctt}

* La asignación de usuarios se ha optimizado e integrado en el paso de extracción de contenido. No es necesario realizar ninguna configuración y, de forma predeterminada, la asignación de usuarios se realizará automáticamente cuando el usuario inicie la extracción de contenido. El usuario tiene la opción de deshabilitar la asignación de usuarios si es necesario. Más información [aquí.](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/user-mapping-and-migration.html?lang=en#user-mapping-detail)
* El paso de precopia mediante [AzCopy](https://learn.microsoft.com/en-us/azure/storage/common/storage-use-azcopy-v10) se ha integrado con la herramienta de transferencia de contenido para acelerar significativamente las extracciones de contenido. La precopia se configura e instala automáticamente cuando se instala esta versión de CTT. De forma predeterminada, cuando se inicia la extracción, la precopia se ejecutará automáticamente para los conjuntos de migración de más de 200 GB. El usuario tiene la opción de desactivarla si es necesario. Más información [aquí.](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/handling-large-content-repositories.html?lang=en)
* Ahora, CTT se puede utilizar en servidores de Windows.

### Correcciones de errores {#bug-fixes-ctt}

* Varias correcciones de errores para mejorar la resistencia de la extracción de contenido.
