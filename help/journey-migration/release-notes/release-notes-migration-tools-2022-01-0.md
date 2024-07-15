---
title: Notas de la versión de las herramientas de migración de la versión 2022.1.0 de AEM as a Cloud Service
description: Notas de la versión de las herramientas de migración de la versión 2022.1.0 de AEM as a Cloud Service
feature: Release Information
exl-id: cbd0c316-bda3-48fb-89d6-a8f97bad1970
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '133'
ht-degree: 6%

---

# Notas de la versión de las herramientas de migración de la versión 2022.1.0 de AEM as a Cloud Service {#release-notes}

Esta página describe las notas de la versión de las herramientas de migración de AEM as a Cloud Service 2022.1.0.

## Herramienta de transferencia de contenido {#ctt-release}

### Fecha de la versión {#release-date-ctt}

La fecha de lanzamiento de la herramienta de transferencia de contenido versión 1.7.18 es el 18 de enero de 2022.

### Novedades {#what-is-new-ctt}

* Se ha agregado la opción de alternancia a la fase de extracción en la herramienta de transferencia de contenido para permitir que los usuarios deshabiliten la [copia previa](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/handling-large-content-repositories.html) durante la extracción. Para obtener velocidades de extracción óptimas, la copia previa durante la extracción debe deshabilitarse para conjuntos de migración pequeños o si solo se han agregado unos pocos blobs desde la última extracción.

### Correcciones de errores {#bug-fixes-ctt}

* Las configuraciones predeterminadas se actualizan para reducir los tiempos de espera de ejecución durante la extracción.
