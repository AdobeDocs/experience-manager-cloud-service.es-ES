---
title: Notas de la versión de las herramientas de migración en AEM versión as a Cloud Service 2022.1.0
description: Notas de la versión de las herramientas de migración en AEM versión as a Cloud Service 2022.1.0
feature: Release Information
exl-id: cbd0c316-bda3-48fb-89d6-a8f97bad1970
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '134'
ht-degree: 6%

---

# Notas de la versión de las herramientas de migración en AEM versión as a Cloud Service 2022.1.0 {#release-notes}

Esta página describe las notas de la versión de las herramientas de migración en AEM as a Cloud Service 2022.1.0.

## Herramienta de transferencia de contenido {#ctt-release}

### Fecha de la versión {#release-date-ctt}

La fecha de versión de la herramienta de transferencia de contenido v1.7.18 es el 18 de enero de 2022.

### Novedades {#what-is-new-ctt}

* Alternar añadido a la fase de extracción en la herramienta de transferencia de contenido para permitir a los usuarios desactivar [copia previa](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/handling-large-content-repositories.html?lang=en) durante la extracción. Para velocidades de extracción óptimas, la precopia durante la extracción debe deshabilitarse para los pequeños conjuntos de migración o si solo se han añadido unos pocos blobs desde la última extracción.

### Corrección de errores {#bug-fixes-ctt}

* Las configuraciones predeterminadas se actualizan para reducir los tiempos de espera de ejecución durante la extracción.
