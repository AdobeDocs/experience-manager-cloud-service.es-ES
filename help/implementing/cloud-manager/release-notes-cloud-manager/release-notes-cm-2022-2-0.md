---
title: Notas de la versión para Cloud Manager en AEM versión as a Cloud Service 2022.02.0
description: Estas son las notas de la versión de Cloud Manager de AEM versión as a Cloud Service 2022.02.0.
feature: Release Information
source-git-commit: f89e1942f63db0b1c57a9d87b051b6a3935ee7cd
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

La fecha de la versión de Cloud Manager en AEM as a Cloud Service 2022.02.0 es el 10 de febrero de 2022. La próxima versión está prevista para el 10 de marzo de 2022.

## Novedades {#what-is-new}

* Nueva aceleración [Canalizaciones de configuración de nivel web](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#web-tier-config-pipelines) se han introducido para implementar exclusivamente la configuración de HTTPD/Dispatcher.
   * Debe estar en AEM versión `2021.12.6151.20211217T120950Z` o más reciente y [inclusión en el modo flexible de las herramientas de Dispatcher](/help/implementing/dispatcher/disp-overview.md#validation-debug) para utilizar esta función.
   * Esta función se implementará por fases en las dos semanas siguientes a la versión de 2022.02.0.
* La experiencia de página de aterrizaje de Cloud Manager se ha actualizado para ofrecer una navegación mejorada, un fácil cambio entre las vistas de cuadrícula/mosaico y ventanas emergentes para obtener un resumen rápido del programa.
* Un nuevo umbral fallido (`< D`) se ha agregado a la variable [métrica de clasificación de fiabilidad.](/help/implementing/cloud-manager/code-quality-testing.md#understanding-code-quality-rules)
   * Los clientes con problemas de calidad graves que afectan a la estabilidad del sistema, relacionados principalmente con índices no válidos y procesos de flujo de trabajo, no podrán realizar implementaciones hasta que se resuelvan dichos problemas.
* La gravedad de la variable `BannedPath` [regla de calidad](/help/implementing/cloud-manager/code-quality-testing.md#understanding-code-quality-rules) se ha cambiado de bloqueador a crítico.
* El asistente de canalización informará al usuario cuando sea necesario actualizar el entorno de AEM antes de configurar un [Canalizaciones de configuración de nivel web](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#web-tier-config-pipelines) asociada a él.

## Corrección de errores {#bug-fixes}

* Las contraseñas antiguas del repositorio de Git ahora siempre se invalidan cuando se genera una nueva contraseña.
* La actualización de variables de entorno a través de la API ya no interfiere con la ejecución de una canalización en situaciones excepcionales.
