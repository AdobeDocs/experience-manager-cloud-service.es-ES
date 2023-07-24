---
title: Notas de la versión 2023.7.0 para Cloud Manager en Adobe Experience Manager as a Cloud Service
description: Estas son las notas de la versión 2023.7.0 para Cloud Manager en AEM as a Cloud Service.
feature: Release Information
exl-id: 9c73d7ab-c2c2-4803-a07b-e9054220c6b2
source-git-commit: 2721cb20083eeda7546513817f1ddfe12e9cb43a
workflow-type: tm+mt
source-wordcount: '265'
ht-degree: 38%

---


# Notas de la versión 2023.7.0 para Cloud Manager en Adobe Experience Manager as a Cloud Service {#release-notes}

Esta página documenta las notas de la versión 2023.7.0 para Cloud Manager en AEM as a Cloud Service.

>[!NOTE]
>
>Consulte [esta página](/help/release-notes/release-notes-cloud/release-notes-current.md) para las notas de la versión actuales de Adobe Experience Manager as a Cloud Service.

## Fecha de lanzamiento {#release-date}

La fecha de lanzamiento de Cloud Manager versión 2023.7.0 en AEM as a Cloud Service es el 29 de junio de 2023. La próxima versión está planificada para el 10 de agosto de 2023.

## Novedades {#what-is-new}

* Las tarjetas de la página de aterrizaje de Cloud Manager ahora indican si [seguridad mejorada](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md) está habilitado para sus programas.
* Si es un desarrollo [canalización](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md) no contiene pasos de prueba, los usuarios tienen la opción de incluir pasos de prueba cuando [inicie la canalización.](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md#running-pipelines)
   * Esto se implementará por fases.
* Cuándo [cancelar la ejecución,](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md#view-details) el paso de aprobación de la ejecución de la canalización ahora pide al usuario que proporcione un motivo para la cancelación.
   * Esto se implementará por fases.
* Los usuarios ahora pueden acceder a [registros del proceso de copia de contenido.](/help/implementing/developing/tools/content-copy.md#accessing-logs)
   * AEM Esta opción solo está disponible si los entornos de origen y destino están en la versión de la aplicación de la versión de la aplicación de la versión de la aplicación de datos en la que se ha realizado el `2023.7.12549` o superior.

## Correcciones de errores {#bug-fixes}

* La navegación a la IU de creación desde Cloud Manager ya no falla al redireccionar a Unified Shell después del inicio de sesión.
* La edición de la fecha de go-live mediante el widget de go-live ahora navega al **Go Live** en lugar de la **Seguridad mejorada** pestaña.
* Al iniciar una operación de copia, un usuario ya no podrá seleccionar un entorno en el que ya se haya invocado una operación de copia.
