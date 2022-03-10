---
title: Notas de la versión para Cloud Manager 2022.3.0 en Adobe Experience Manager as a Cloud Service
description: Estas son las notas de la versión de Cloud Manager 2022.3.0 en AEM as a Cloud Service.
feature: Release Information
exl-id: 9c73d7ab-c2c2-4803-a07b-e9054220c6b2
source-git-commit: 428bba062fcfb44ebfbbf3c1d05ce1a4634fb429
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 2%

---


# Notas de la versión para Cloud Manager 2022.3.0 en Adobe Experience Manager as a Cloud Service {#release-notes}

Esta página documenta las notas de la versión de Cloud Manager 2022.3.0 en AEM as a Cloud Service.

>[!NOTE]
>
>Consulte [esta página](/help/release-notes/release-notes-cloud/release-notes-current.md) para las notas de la versión actuales de Adobe Experience Manager as a Cloud Service.

## Fecha de la versión {#release-date}

La fecha de la versión de Cloud Manager 2022.3.0 en AEM as a Cloud Service del 10 de marzo de 2022. La próxima versión está prevista para el 7 de abril de 2022.

## Novedades {#what-is-new}

* Un usuario con la variable **Desarrollador** ahora puede acceder al registro de entorno de AEM.
* [La variable `reliability_rating` métrica crítica](/help/implementing/cloud-manager/code-quality-testing.md) se ha desactivado.
* Ahora un usuario puede ordenar las columnas de la **Canalizaciones** en Cloud Manager.

## Corrección de errores {#bug-fixes}

* Un subconjunto de repositorios git creados manualmente tenía valores de nombre incorrectos que afectaban a [la función de reutilización de artefactos de compilación.](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/setting-up-project.md#build-artifact-reuse) Los nombres de esos repositorios se han cambiado y los usuarios verán el nombre corregido en la interfaz de usuario/API de Cloud Manager.
* [Al añadir o editar una canalización de calidad de código,](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md) el **Comportamiento de errores de métricas importantes** ya no se muestran.
* Las configuraciones de variables de canalización inesperadas ya no causan errores en el paso de compilación.
