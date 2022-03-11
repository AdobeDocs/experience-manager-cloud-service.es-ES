---
title: Notas de la versión para Cloud Manager en AEM versión as a Cloud Service 2022.02.0
description: Estas son las notas de la versión de Cloud Manager de AEM versión as a Cloud Service 2022.02.0.
feature: Release Information
exl-id: da0643a0-78f8-4e9d-9cc9-a1a17067a08c
source-git-commit: 8162d1d6ddeff867507f749f223c0111b6856122
workflow-type: tm+mt
source-wordcount: '287'
ht-degree: 2%

---

# Notas de la versión para Cloud Manager en Adobe Experience Manager as a Cloud Service 2022.02.0 {#release-notes}

Esta página describe las notas de la versión de Cloud Manager en AEM as a Cloud Service 2022.02.0.

>[!NOTE]
>
>Consulte [esta página](/help/release-notes/release-notes-cloud/release-notes-current.md) para las notas de la versión actuales de Adobe Experience Manager as a Cloud Service.

## Fecha de la versión {#release-date}

La fecha de la versión de Cloud Manager en AEM as a Cloud Service 2022.02.0 es el 10 de febrero de 2022. The next release is planned for 10 March 2022.

## Novedades {#what-is-new}

* New accelerated [Web Tier Config pipelines](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#web-tier-config-pipelines) have been introduced to exclusively deploy HTTPD/dispatcher configuration.
   * You must be on AEM version `2021.12.6151.20211217T120950Z` or newer and [opt in to the flexible mode of the dispatcher tools](/help/implementing/dispatcher/disp-overview.md#validation-debug) to use this feature.
   * This feature will be rolled out in a phased approach over the two weeks following the 2022.02.0 release.
* La experiencia de página de aterrizaje de Cloud Manager se ha actualizado para ofrecer una navegación mejorada, un fácil cambio entre las vistas de cuadrícula/mosaico y ventanas emergentes para obtener un resumen rápido del programa.
* Un nuevo umbral fallido (`< D`) se ha agregado a la variable [métrica de clasificación de fiabilidad.](/help/implementing/cloud-manager/code-quality-testing.md#understanding-code-quality-rules)
   * Los clientes con problemas de calidad graves que afectan a la estabilidad del sistema, relacionados principalmente con índices no válidos y procesos de flujo de trabajo, no podrán realizar implementaciones hasta que se resuelvan dichos problemas.
* La gravedad de la variable `BannedPath` [regla de calidad](/help/implementing/cloud-manager/code-quality-testing.md#understanding-code-quality-rules) se ha cambiado de bloqueador a crítico.
* The pipeline wizard will inform the user when an AEM environment update may be needed before configuring a [Web Tier Config pipelines](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#web-tier-config-pipelines) associated with it.

## Corrección de errores {#bug-fixes}

* Las contraseñas antiguas del repositorio de Git ahora siempre se invalidan cuando se genera una nueva contraseña.
* La actualización de variables de entorno a través de la API ya no interfiere con la ejecución de una canalización en situaciones excepcionales.
