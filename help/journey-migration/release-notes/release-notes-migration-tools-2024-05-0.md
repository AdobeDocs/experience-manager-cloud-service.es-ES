---
title: Notas de la versión de las herramientas de migración de la versión 2024.05.0 de AEM as a Cloud Service
description: Notas de la versión de las herramientas de migración de la versión 2024.05.0 de AEM as a Cloud Service
feature: Release Information
role: Admin
exl-id: f50a74fa-ad7d-4837-b0a1-9945c32af02f
source-git-commit: 3b2ed44b438fe8587a9b9603ddfacc41111fb903
workflow-type: tm+mt
source-wordcount: '208'
ht-degree: 6%

---

# Notas de la versión de las herramientas de migración de la versión 2024.05.0 de AEM as a Cloud Service {#release-notes}

Esta página describe las notas de la versión de las herramientas de migración de AEM as a Cloud Service 2024.05.0.

## Analizador de prácticas recomendadas {#bpa-release}

### Fecha de la versión {#release-date-bpa}

La fecha de lanzamiento del Analizador de prácticas recomendadas v2.1.50 es mayo de 2024.

### Novedades {#what-is-new-bpa}

* El Analizador de prácticas recomendadas (BPA) ahora admite la carga automática de informes generados por BPA directamente en Cloud Acceleration Manager (CAM). Los usuarios ya no tendrán que descargar manualmente el informe y cargarlo en CAM. Para obtener más información, consulte [Uso del Analizador de prácticas recomendadas](/help/journey-migration/best-practices-analyzer/using-best-practices-analyzer.md)

### Corrección de errores {#bug-fixes-bpa}

* El Analizador de prácticas recomendadas ahora detecta todos los nodos de más de 16 MB
* Condición de la carrera que causa ocurrencias esporádicas de hallazgos del NCC corregidos.

## Cloud Acceleration Manager {#cam-release}

### Novedades {#what-is-new-cam}

* Cloud Acceleration Manager (CAM) ahora admite la carga automática de informes generados por BPA directamente en CAM. Para obtener más información, consulte [Fase de preparación en Cloud Acceleration Manager - Uso de la tarjeta de análisis de prácticas recomendadas](/help/journey-migration/cloud-acceleration-manager/using-cam/cam-readiness-phase.md#best-practices-analysis)

* Cloud Acceleration Manager ahora proporciona una estimación de cuánto tiempo puede tardar una ingesta, dados factores como el recuento de nodos, el tamaño del almacén de datos, etc. Más información con [Ingesta de contenido en el Cloud Service](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md)
