---
title: Notas de la versión de las herramientas de migración en AEM versión as a Cloud Service 2022.3.0
description: Notas de la versión de las herramientas de migración en AEM versión as a Cloud Service 2022.3.0
feature: Release Information
exl-id: ab43605d-d46e-43de-b71f-fab610609550
source-git-commit: 87e3291b4a72c24fc6cf8df488df305f1a078ea5
workflow-type: tm+mt
source-wordcount: '366'
ht-degree: 86%

---

# Notas de la versión de las herramientas de migración en AEM versión as a Cloud Service 2022.3.0 {#release-notes}

Esta página describe las notas de la versión de las herramientas de migración en AEM as a Cloud Service 2022.3.0.

## Analizador de prácticas recomendadas {#bpa-release}

### Fecha de la versión {#release-date-bpa}

El 16 de marzo de 2022 es la fecha de lanzamiento del Analizador de prácticas recomendadas versión 2.1.26.

### Novedades {#what-is-new-bpa}

* Capacidad para detectar recursos no procesados. Si se detectan recursos no procesados, estos deben configurarse para procesarse o deben eliminarse del conjunto de migración durante la transferencia de contenido para evitar tener problemas durante la ingesta de contenido.
* Capacidad para detectar si el contenido tiene más de 1000 URL personalizadas. No se recomienda utilizar un número elevado de URL personalizadas, ya que suponen una carga en los servidores de Dispatcher y Publish.
* Capacidad para identificar problemas relacionados con las definiciones de índices de Oak y detectar incompatibilidades con AEM as a Cloud Service.
* Capacidad para detectar e informar sobre el uso de configuraciones de externalizador. En AEM as a Cloud Service, la configuración de externalizador la establece Cloud Manager. Por lo tanto, las configuraciones de externalizador existentes deben refactorizarse para mantener la compatibilidad.

### Correcciones de errores {#bug-fixes-bpa}

* En algunos casos, BPA no se pudo ejecutar debido a que FormsSelectiveFeaturesAnalysis arrojó un error de aserción. Esto se ha corregido.
* BPA informaba de conclusiones relacionadas con el patrón de WRK como IMPORTANTE en lugar de como CRÍTICO. Esto se ha corregido.
* BPA informaba incorrectamente de conclusiones relacionadas con las definiciones de índice OAK en ui.apps como CRÍTICO. Esto se ha corregido..

## Herramienta de transferencia de contenido {#ctt-release}

### Fecha de la versión {#release-date-ctt}

La fecha de lanzamiento de la herramienta de transferencia de contenido versión 1.9.0 es el 28 de febrero de 2022.

### Novedades {#what-is-new-ctt}

* Comprobar protecciones de tamaño: la función de comprobación de tamaño de la herramienta de transferencia de contenido ayuda a reducir las transferencias de contenido fallidas.  Con la función de comprobación de tamaño, los usuarios pueden 1) determinar si tienen suficiente espacio en disco en el subdirectorio `crx-quickstart` antes de la extracción, y 2) estimar el tamaño del conjunto de migración y verificar si es compatible. Si se infringen una o ambas comprobaciones, los usuarios verán advertencias en la IU de CTT. Con esta protección, puede evitar errores en la transferencia de contenido y discutir de forma proactiva las opciones de migración con el Servicio de atención al cliente de Adobe. Consulte [Determinación del tamaño del conjunto de migración y el espacio en disco](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/getting-started-content-transfer-tool.html?lang=es#migration-set-size) para obtener más información.
