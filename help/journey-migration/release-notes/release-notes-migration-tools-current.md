---
title: Notas de la versión de las herramientas de migración de la versión 2024.07 de AEM as a Cloud Service
description: Notas de la versión de las herramientas de migración de la versión 2024.07.0 de AEM as a Cloud Service
feature: Release Information
exl-id: 52709511-eab2-47a7-8bea-1b707cd568a1
role: Admin
source-git-commit: 4f01ca0076248442fe93161bbc8b98bffb64551b
workflow-type: tm+mt
source-wordcount: '171'
ht-degree: 8%

---

# Notas de la versión de las herramientas de migración de la versión 2024.07.0 de AEM as a Cloud Service {#release-notes}

Esta página describe las notas de la versión de las herramientas de migración de AEM as a Cloud Service 2024.07.0.

## Herramienta de transferencia de contenido {#ctt-release}

### Fecha de la versión {#release-date-ctt}

La fecha de lanzamiento de la herramienta de transferencia de contenido v3.0.16 es julio de 2024.

### Novedades {#what-is-new-ctt}

* Carga automática de registros de extracción de CTT en caso de errores.
* Los usuarios ahora pueden realizar correctamente la ingesta tras la renovación de la clave de extracción.
* Se ha agregado compatibilidad con la realización de extracciones de CTT mediante una clave de acceso de Azure y una clave secreta con AzureDataStore.
* Los usuarios recibirán ahora el mensaje de error correcto cuando se utilice una clave no válida para crear un conjunto de migración.

## Analizador de prácticas recomendadas {#bpa-release}

### Fecha de la versión {#release-date-bpa}

La fecha de lanzamiento del Analizador de prácticas recomendadas v2.1.50 es mayo de 2024.

### Corrección de errores {#bug-fixes-bpa}

* El Analizador de prácticas recomendadas ahora detecta todos los nodos de más de 16 MB
* Condición de la carrera que causa ocurrencias esporádicas de hallazgos del NCC corregidos.
