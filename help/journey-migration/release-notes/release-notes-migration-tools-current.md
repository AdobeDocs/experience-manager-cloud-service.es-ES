---
title: AEM Notas de la versión de las herramientas de migración de la versión as a Cloud Service 2023.03.0 de
description: AEM Notas de la versión de las herramientas de migración de la versión as a Cloud Service 2022.03.0 de
feature: Release Information
exl-id: 2f787321-f156-480d-bbe8-1a6d04f110c5
source-git-commit: 5815dacd2806cc7886aa0c7c5c9fd329306b3e1b
workflow-type: tm+mt
source-wordcount: '150'
ht-degree: 15%

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