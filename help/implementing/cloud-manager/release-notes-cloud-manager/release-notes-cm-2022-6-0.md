---
title: Notas de la versión para Cloud Manager 2022.6.0 en Adobe Experience Manager as a Cloud Service
description: Estas son las notas de la versión de Cloud Manager 2022.6.0 en AEM as a Cloud Service.
feature: Release Information
exl-id: 0a348836-74cd-4fd4-aef4-6ffbd6483c24
source-git-commit: 097c17b37cc308dc906cd4af7dc7c5d51862bdfa
workflow-type: tm+mt
source-wordcount: '348'
ht-degree: 1%

---

# Notas de la versión para Cloud Manager 2022.6.0 en Adobe Experience Manager as a Cloud Service {#release-notes}

Esta página documenta las notas de la versión de Cloud Manager 2022.6.0 en AEM as a Cloud Service.

>[!NOTE]
>
>Consulte [esta página](/help/release-notes/release-notes-cloud/release-notes-current.md) para las notas de la versión actuales de Adobe Experience Manager as a Cloud Service.

## Fecha de la versión {#release-date}

La fecha de la versión de Cloud Manager 2022.6.0 en AEM as a Cloud Service es el 9 de junio de 2022. La próxima versión está planificada para el 30 de junio de 2022.

## Novedades {#what-is-new}

* La interfaz de usuario de Cloud Manager ahora permite [restauración de contenido autoservicio](/help/operations/backup.md) a un buen estado conocido del entorno de nube AEM.
   * Esta función se implementará por fases en las semanas siguientes a la versión 2022.06.0.
* Una nueva tarjeta de bienvenida en la página de aterrizaje de Cloud Manager permite a los usuarios acceder rápidamente a los tutoriales de incorporación y a las métricas de progreso relacionadas con el inquilino.
   * Esta función se implementará por fases en la semana siguiente a la versión 2022.06.0.
* Los usuarios con los permisos necesarios pueden acceder a un nuevo [Panel de licencias](/help/implementing/cloud-manager/license-dashboard.md) en la página de aterrizaje de Cloud Manager para ver los detalles de las autorizaciones disponibles para el inquilino.
   * AEM Sites es la primera solución para la cual se ofrece disponibilidad y consumo de uso a través del tablero Cloud Manage.
   * Esta función se implementará por fases en las semanas siguientes a la versión 2022.06.0.
* [Nueva subcuenta de reliquia y administración de usuarios autoservicio](/help/implementing/cloud-manager/user-access-new-relic.md) ya está disponible a través de la interfaz de usuario de Cloud Manager .
   * Esta función se implementará por fases en las semanas siguientes a la versión 2022.06.0.
* Un nuevo widget Go Live en la página principal de los programas de producción de Cloud Service ahora proporciona directrices para prepararse para una experiencia de lanzamiento exitosa.
* [Ahora, los artefactos de compilación se pueden reutilizar](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/setting-up-project.md#build-artifact-reuse) al usar la duplicación de Git.

## Cambios en la API {#api-changes}

* La variable [`List Programs`](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/#operation/getPrograms) La API de se ha desaprobado y [`List Programs for Tenant`](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/#operation/getProgramsForTenant) en su lugar.
   * `List Programs` sigue funcionando, pero su uso generará mensajes de advertencia en los registros.
   * Dejará de ser compatible a los tres meses.
