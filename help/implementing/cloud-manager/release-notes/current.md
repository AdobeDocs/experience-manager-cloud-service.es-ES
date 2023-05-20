---
title: Notas de la versión 2023.5.0 para Cloud Manager en Adobe Experience Manager as a Cloud Service
description: Estas son las notas de la versión 2023.5.0 para Cloud Manager en AEM as a Cloud Service.
feature: Release Information
exl-id: 9c73d7ab-c2c2-4803-a07b-e9054220c6b2
source-git-commit: 4340b957cea86452f916ab615b383aabacc21676
workflow-type: tm+mt
source-wordcount: '206'
ht-degree: 41%

---


# Notas de la versión 2023.5.0 para Cloud Manager en Adobe Experience Manager as a Cloud Service {#release-notes}

Esta página documenta las notas de la versión 2023.5.0 para Cloud Manager en AEM as a Cloud Service.

>[!NOTE]
>
>Consulte [esta página](/help/release-notes/release-notes-cloud/release-notes-current.md) para ver las notas de la versión actuales de Adobe Experience Manager as a Cloud Service.

## Fecha de lanzamiento {#release-date}

AEM La fecha de lanzamiento de la versión 2023.5.0 de Cloud Manager en la versión as a Cloud Service de es el 11 de mayo de 2023. La próxima versión está planificada para el 8 de junio de 2023.

## Novedades {#what-is-new}

* La compatibilidad con las pruebas de productos, funciones e IU se ha ampliado a [prueba de canalización que no sea de producción.](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md)
* Además de habilitar las pruebas en orden ascendente, [La compatibilidad con las pruebas de IU se ha ampliado a las pruebas de Cypress.](/help/implementing/cloud-manager/ui-testing.md)
* [Copia de contenido de autoservicio](/help/implementing/developing/tools/content-copy.md) ahora está disponible desde un entorno superior a uno inferior a través de la IU de Cloud Manager.
* El paso de validación de ejecución de canalización se ha mejorado para validar el estado de las colas de replicación al principio del proceso de ejecución. AEM Esto garantiza que los pasos de implementación no se vean afectados por colas bloqueadas que los usuarios administradores deben abordar directamente desde el entorno de creación de informes.

## Correcciones de errores {#bug-fixes}

* La creación del entorno ya no falla cuando se utilizan caracteres de bytes múltiples en el nombre del entorno.
