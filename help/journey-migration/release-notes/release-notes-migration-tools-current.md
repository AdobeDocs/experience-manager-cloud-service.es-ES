---
title: Notas de la versión de las herramientas de migración en AEM versión as a Cloud Service 2022.1.0
description: Notas de la versión de las herramientas de migración en AEM versión as a Cloud Service 2022.1.0
feature: Release Information
source-git-commit: fec3a69db3b05a6b750ebf718f32f599cac24d0c
workflow-type: tm+mt
source-wordcount: '157'
ht-degree: 10%

---


# Notas de la versión de las herramientas de migración en AEM versión as a Cloud Service 2022.1.0 {#release-notes}

Esta página describe las notas de la versión de las herramientas de migración en AEM as a Cloud Service 2022.1.0.

>[!NOTE]
>Para ver las notas de la versión actuales de Adobe Experience Manager as a Cloud Service, haga clic en [here](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/release-notes-current.html?lang=es).


## Herramienta de transferencia de contenido {#ctt-release}

### Fecha de la versión {#release-date-ctt}

La fecha de versión de la herramienta de transferencia de contenido v1.7.18 es el 18 de enero de 2022.

### Novedades {#what-is-new-ctt}

* Alternar añadido a la fase de extracción en la herramienta de transferencia de contenido para permitir a los usuarios desactivar [copia previa](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/handling-large-content-repositories.html?lang=en) durante la extracción. Para velocidades de extracción óptimas, la precopia durante la extracción debe deshabilitarse para los pequeños conjuntos de migración o si solo se han añadido unos pocos blobs desde la última extracción.

### Corrección de errores {#bug-fixes-ctt}

* Las configuraciones predeterminadas se actualizan para reducir los tiempos de espera de ejecución durante la extracción.
