---
title: Notas de la versión para Cloud Manager en AEM versión as a Cloud Service 2021.8.0
description: Notas de la versión para Cloud Manager en AEM versión as a Cloud Service 2021.8.0
feature: Release Information
exl-id: cf1d5c4f-404a-4ced-90f2-273c710adc0f
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '293'
ht-degree: 4%

---

# Notas de la versión para Cloud Manager en Adobe Experience Manager as a Cloud Service 2021.8.0 {#release-notes}

Esta página describe las notas de la versión de Cloud Manager en AEM as a Cloud Service 2021.8.0.

>[!NOTE]
>Para ver las notas de la versión actuales de Adobe Experience Manager as a Cloud Service, haga clic en [here](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/release-notes-current.html?lang=es).

## Fecha de la versión {#release-date}

La fecha de versión de Cloud Manager en AEM as a Cloud Service 2021.8.0 es el 12 de agosto de 2021.

### Novedades {#what-is-new}

* Los clientes Cloud Service ahora pueden ver los informes de Acuerdo de nivel de servicio (SLA) en Cloud Manager. Esto estará disponible progresivamente en los próximos meses.
Consulte [Informes de SLA](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/sla-reporting.html) para obtener más información.

* Tipo y gravedad del IndexType y `IndexDamAssetLucene` se han cambiado las reglas de calidad. Estos son ahora los dos errores de Blocker *serverity*.

* Se han introducido nuevas reglas de calidad de índice Oak para cubrir configuraciones asincrónicas y tika.

* Aumente el número máximo de certificados SSL por programa a 50.

* Capacidad de autoservicio para permitir a los usuarios crear y administrar varios repositorios a través de la interfaz de usuario de Cloud Manager.

* SonarQube leía innecesariamente los datos del historial de Git. En bases de código grandes, esto podría provocar una penalización innecesaria del rendimiento de la compilación.

* Ahora hay una API disponible para invalidar la caché de dependencias de Maven por canalización.

* La versión del tipo de archivo del proyecto AEM utilizado por Cloud Manager se ha actualizado a la versión 29.

### Corrección de errores {#bug-fixes}

* Actualizar el estado disponible no se debe mostrar cuando la última versión sea menor que la versión actual.

* La incorporación inicial estaba fallando para nuevas organizaciones con nombres muy largos.

* En ocasiones, cuando una canalización se activa dos veces por alguna razón, el resultado es que una de las ejecuciones falla con *no se puede actualizar el estado de ejecución de la canalización* error.
