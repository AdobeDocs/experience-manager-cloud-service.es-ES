---
title: Notas de la versión de las herramientas de migración de la versión 2023.07.0 de AEM as a Cloud Service
description: Notas de la versión de las herramientas de migración de la versión 2023.07.0 de AEM as a Cloud Service
feature: Release Information
exl-id: 2f787321-f156-480d-bbe8-1a6d04f110c5
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 6%

---

# Notas de la versión de las herramientas de migración de la versión 2023.07.0 de AEM as a Cloud Service {#release-notes}

Esta página describe las notas de la versión de las herramientas de migración de AEM as a Cloud Service 2023.07.0.

## Analizador de prácticas recomendadas {#bpa-release}

### Fecha de la versión {#release-date-bpa}

La fecha de lanzamiento del Analizador de prácticas recomendadas v2.1.42 es el 6 de julio de 2023.

### Novedades {#what-is-new-bpa}

* Se han agregado varios patrones de prácticas recomendadas a esta versión del Analizador de prácticas recomendadas. Entre estas características se incluyen:
   * Identificación de la configuración mínima de tareas de mantenimiento
   * Detección de consultas de larga duración/pesadas
   * Detectar un número elevado de flujos de trabajo de autor en estado de ejecución o anticuado
   * Detectando la configuración del trabajo de OSGI Apache sling
   * Detectar cachés de Guava personalizadas

### Correcciones de errores {#bug-fixes-bpa}

* Se mejoró el BPA para evitar errores de generación de informes sin memoria para informes con un número elevado de resultados.
* Se mejoró BPA para detectar caracteres de escape en las rutas a fin de evitar errores de ingesta de contenido al migrar contenido a AEM as a Cloud Service.
