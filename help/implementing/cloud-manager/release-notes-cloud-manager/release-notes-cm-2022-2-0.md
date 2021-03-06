---
title: Notas de la versión para Cloud Manager en AEM versión as a Cloud Service 2022.02.0
description: Estas son las notas de la versión de Cloud Manager de AEM versión as a Cloud Service 2022.02.0.
feature: Release Information
exl-id: da0643a0-78f8-4e9d-9cc9-a1a17067a08c
source-git-commit: 0c4a42595800f7f1d0869bf647c3ec99023b12c5
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Notas de la versión para Cloud Manager en Adobe Experience Manager as a Cloud Service 2022.02.0 {#release-notes}

Esta página describe las notas de la versión de Cloud Manager en AEM as a Cloud Service 2022.02.0.

>[!NOTE]
>
>Consulte [esta página](/help/release-notes/release-notes-cloud/release-notes-current.md) para las notas de la versión actuales de Adobe Experience Manager as a Cloud Service.

## Fecha de la versión {#release-date}

La fecha de la versión de Cloud Manager en AEM as a Cloud Service 2022.02.0 es el 10 de febrero de 2022. La próxima versión está planificada para el 10 de marzo de 2022.

## Novedades {#what-is-new}

* Se han introducido nuevas [canalizaciones de configuración de nivel web](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#web-tier-config-pipelines) aceleradas para implementar exclusivamente la configuración de HTTPD/Dispatcher.
   * Debe tener la versión de AEM `2021.12.6151.20211217T120950Z` o una más reciente y optar por su [inclusión en el modo flexible de las herramientas de Dispatcher](/help/implementing/dispatcher/disp-overview.md#validation-debug) para utilizar esta función.
   * Esta función se implementará por fases en las dos semanas siguientes al lanzamiento de la versión 2022.02.0.
* La experiencia de la página de aterrizaje de Cloud Manager se ha actualizado para ofrecer una navegación mejorada, un cambio fácil entre las vistas de cuadrícula/mosaico y ventanas emergentes para obtener un resumen rápido del programa.
* Un nuevo umbral de fallo (`< D`) se ha añadido a la [métrica de clasificación de fiabilidad.](/help/implementing/cloud-manager/code-quality-testing.md#understanding-code-quality-rules)
   * Los clientes con problemas de calidad graves que afectan a la estabilidad del sistema, relacionados sobre todo con índices y procesos de flujo de trabajo no válidos, no podrán realizar implementaciones hasta que se resuelvan dichos problemas.
* La gravedad de la `BannedPath` [regla de calidad](/help/implementing/cloud-manager/code-quality-testing.md#understanding-code-quality-rules) se ha cambiado de bloqueo a crítica.
* El asistente de canalización informará al usuario cuando sea necesario actualizar el entorno de AEM antes de configurar [canalizaciones de configuración de nivel web](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#web-tier-config-pipelines) asociadas a él.

## Correcciones de errores {#bug-fixes}

* Las contraseñas antiguas del repositorio de Git ahora siempre se invalidan cuando se genera una nueva contraseña.
* La actualización de variables de entorno a través de la API ya no interfiere con la ejecución de una canalización en situaciones excepcionales.
