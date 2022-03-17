---
title: Notas de la versión de las herramientas de migración en AEM versión as a Cloud Service 2022.3.0
description: Notas de la versión de las herramientas de migración en AEM versión as a Cloud Service 2022.3.0
feature: Release Information
source-git-commit: c497424271ea960d22a30b4a6c66432935ec820d
workflow-type: tm+mt
source-wordcount: '366'
ht-degree: 7%

---


# Notas de la versión de las herramientas de migración en AEM versión as a Cloud Service 2022.3.0 {#release-notes}

Esta página describe las notas de la versión de las herramientas de migración en AEM as a Cloud Service 2022.3.0.

## Analizador de prácticas recomendadas {#bpa-release}

### Fecha de la versión {#release-date-bpa}

La fecha de versión de Best Practices Analyzer v2.1.26 es el 16 de marzo de 2022.

### Novedades {#what-is-new-bpa}

* Capacidad para detectar recursos no procesados. Si se detectan recursos no procesados, estos deben configurarse para procesarse o deben eliminarse del conjunto de migración durante la transferencia de contenido para evitar tener problemas durante la ingesta de contenido.
* Capacidad para detectar si el contenido tiene más de 1000 URL de vanidad. No se recomienda utilizar un número elevado de URL de vanidad, ya que pone una carga en los servidores de Dispatcher y Publish.
* Capacidad para identificar problemas relacionados con las definiciones de índices de Oak y detectar incompatibilidades con AEM as a Cloud Service.
* Capacidad para detectar e informar sobre el uso de configuraciones de externalizador. En AEM configuración de externalizador as a Cloud Service la establece Cloud Manager, por lo tanto, las configuraciones de externalizador existentes deben refactorizarse para mantener la compatibilidad.

### Corrección de errores {#bug-fixes-bpa}

* En algunos casos, BPA no se pudo ejecutar debido a que FormsSelectiveFeaturesAnalysis arrojó un error de aserción. Esto se ha solucionado.
* La BPA estaba presentando conclusiones relacionadas con el patrón de trabajo como PRINCIPAL en lugar de CRÍTICO. Esto se ha solucionado.
* BPA informaba incorrectamente de los resultados relacionados con las definiciones de índice OAK en ui.apps como CRITICAL. Esto se ha solucionado.

## Herramienta de transferencia de contenido {#ctt-release}

### Fecha de la versión {#release-date-ctt}

La fecha de versión de la herramienta de transferencia de contenido v1.9.0 es el 28 de febrero de 2022.

### Novedades {#what-is-new-ctt}

* Comprobar protecciones de tamaño : la función Tamaño de comprobación de la herramienta de transferencia de contenido ayuda a reducir las transferencias de contenido fallidas.  Con la función Tamaño de comprobación, los usuarios pueden 1) determinar si tienen suficiente espacio en disco en la variable `crx-quickstart` antes de la extracción y 2) estime el tamaño del conjunto de migración y verifique si es compatible. Si se infringen una o ambas comprobaciones, los usuarios verán advertencias en la interfaz de usuario de CTT. Con esta protección, puede evitar fallos en la transferencia de contenido y discutir de forma proactiva las opciones de migración con el Servicio de atención al cliente de Adobe. Consulte [Determinación del tamaño del conjunto de migración y el espacio en disco](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/getting-started-content-transfer-tool.html?lang=en#migration-set-size) para obtener más información.