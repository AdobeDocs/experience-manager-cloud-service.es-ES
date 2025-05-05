---
title: Notas de la versión para las herramientas de migración en la versión 2022.3.0 de AEM as a Cloud Service
description: Notas de la versión para las herramientas de migración en la versión 2022.3.0 de AEM as a Cloud Service
feature: Release Information
exl-id: ab43605d-d46e-43de-b71f-fab610609550
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '349'
ht-degree: 34%

---

# Notas de la versión para las herramientas de migración en la versión 2022.3.0 de AEM as a Cloud Service {#release-notes}

Esta página describe las notas de la versión de las herramientas de migración de AEM as a Cloud Service 2022.3.0.

## Analizador de prácticas recomendadas {#bpa-release}

### Fecha de la versión {#release-date-bpa}

El 16 de marzo de 2022 es la fecha de lanzamiento del Analizador de prácticas recomendadas versión 2.1.26.

### Novedades {#what-is-new-bpa}

* Capacidad para detectar recursos no procesados. Si se detectan recursos no procesados, estos deben configurarse para procesarse o eliminarse del conjunto de migración durante la transferencia de contenido para evitar tener problemas durante la ingesta de contenido.
* Capacidad para detectar si el contenido tiene más de 1000 URL personalizadas. No se recomienda utilizar un número elevado de URL personalizadas, ya que suponen una carga en los servidores de Dispatcher y Publish.
* Capacidad para identificar problemas relacionados con las definiciones de índices de Oak y detectar incompatibilidades con AEM as a Cloud Service.
* Capacidad para detectar e informar sobre el uso de configuraciones de externalizador. En AEM as a Cloud Service Externalizer, Cloud Manager establece las configuraciones. Por lo tanto, las configuraciones de externalizador existentes deben refactorizarse para mantener la compatibilidad.

### Correcciones de errores {#bug-fixes-bpa}

* En algunos casos, BPA no se pudo ejecutar debido a que FormsSelectiveFeaturesAnalysis arrojó un error de aserción.
* BPA informaba de conclusiones relacionadas con el patrón de WRK como IMPORTANTE en lugar de como CRÍTICO.
* BPA informaba incorrectamente de conclusiones relacionadas con las definiciones de índice de Oak en ui.apps como CRÍTICO.

## Herramienta de transferencia de contenido {#ctt-release}

### Fecha de la versión {#release-date-ctt}

La fecha de lanzamiento de la herramienta de transferencia de contenido versión 1.9.0 es el 28 de febrero de 2022.

### Novedades {#what-is-new-ctt}

* Comprobar protecciones de tamaño: la función de comprobación de tamaño de la herramienta de transferencia de contenido ayuda a reducir las transferencias de contenido fallidas. Con la función Comprobar tamaño, los usuarios pueden determinar si tienen suficiente espacio en disco en el subdirectorio `crx-quickstart` antes de la extracción. Además, pueden estimar el tamaño del conjunto de migración y verificar si es compatible. Si se infringen una o ambas comprobaciones, los usuarios ven advertencias en la interfaz de usuario de CTT. Con esta protección, puede evitar errores en la transferencia de contenido y discutir de forma proactiva las opciones de migración con el Servicio de atención al cliente de Adobe. Consulte [Determinación del tamaño del conjunto de migración y el espacio en disco](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/getting-started-content-transfer-tool.html?lang=es#migration-set-size) para obtener más información.
