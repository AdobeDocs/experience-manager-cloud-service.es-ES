---
title: Notas de la versión para Cloud Manager 2022.12.0 en Adobe Experience Manager as a Cloud Service
description: Estas son las notas de la versión para Cloud Manager 2022.12.0 en AEM as a Cloud Service.
feature: Release Information
exl-id: 9c73d7ab-c2c2-4803-a07b-e9054220c6b2
source-git-commit: aa7f2175e2a43a318a6171e622d292ed3a8e958b
workflow-type: tm+mt
source-wordcount: '202'
ht-degree: 38%

---


# Notas de la versión para Cloud Manager 2022.12.0 en Adobe Experience Manager as a Cloud Service {#release-notes}

Esta página describe las notas de la versión para Cloud Manager 2022.12.0 en AEM as a Cloud Service.

>[!NOTE]
>
>Consulte [esta página](/help/release-notes/release-notes-cloud/release-notes-current.md) para ver las notas de la versión actuales de Adobe Experience Manager as a Cloud Service.

## Fecha de lanzamiento {#release-date}

La fecha de la versión de Cloud Manager 2022.12.0 en AEM as a Cloud Service es el 29 de noviembre de 2022. La próxima versión está prevista para el 19 de enero de 2023.

## Novedades {#what-is-new}

* Notificaciones para [Actualizaciones de mantenimiento de AEM](/help/overview/what-is-new-and-different.md#aem-updates) se mostrará en la interfaz de usuario de Cloud Manager. Este cambio se implementará de forma gradual en las semanas posteriores a la versión 2022.12.0.
* Cuando una ingesta a través de la variable [Herramienta de transferencia de contenido (CTT)](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/overview-content-transfer-tool.md) está en curso, el estado del entorno tanto en la consola de desarrollador como en Cloud Manager se mostrará como `Ingestion in Progress`.
* Mejoras en la disponibilidad y fiabilidad de [Canalizaciones de Cloud Manager](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md) se hicieron.

## Correcciones de errores {#bug-fixes}

* Se hizo un cambio para evitar [canalizaciones front-end](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#front-end) cuando se está ejecutando una ejecución de canalización en el mismo entorno.
* Se realizó un cambio para evitar una `PATCH /program//environment//variables` solicitud de entornos con el `FAILED` estado.
