---
title: Notas de la versión para Cloud Manager en AEM as a Cloud Service Versión 2021.8.0
description: Notas de la versión para Cloud Manager en AEM as a Cloud Service Versión 2021.8.0
feature: Información de la versión
exl-id: 42cc9cab-6e66-4976-a3b1-ecb9dbaaabf4
source-git-commit: 05cd993df7293691a0f8b91e9bde278ec7b7af69
workflow-type: tm+mt
source-wordcount: '289'
ht-degree: 5%

---

# Notas de la versión para Cloud Manager en Adobe Experience Manager as a Cloud Service 2021.8.0 {#release-notes}

Esta página describe las notas de la versión de Cloud Manager en AEM as a Cloud Service 2021.8.0.

>[!NOTE]
>Para ver las notas de la versión actuales de Adobe Experience Manager as a Cloud Service, haga clic [aquí](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/release-notes-current.html?lang=es).

## Fecha de la versión {#release-date}

La fecha de versión de Cloud Manager en AEM as a Cloud Service 2021.8.0 es el 12 de agosto de 2021.
La próxima versión está planificada para el 9 de septiembre de 2021.

### Novedades {#what-is-new}

* Los clientes Cloud Service ahora pueden ver los informes de Acuerdo de nivel de servicio (SLA) en Cloud Manager. Esto estará disponible progresivamente en los próximos meses.

* Se ha cambiado el tipo y la gravedad de las reglas de calidad IndexType y `IndexDamAssetLucene` . Estos son ahora errores del bloqueador *serverity*.

* Se han introducido nuevas reglas de calidad de índice Oak para cubrir configuraciones asincrónicas y tika.

* Aumente el número máximo de certificados SSL por programa a 50.

* Capacidad de autoservicio para permitir a los usuarios crear y administrar varios repositorios a través de la interfaz de usuario de Cloud Manager.

* SonarQube leía innecesariamente los datos del historial de Git. En bases de código grandes, esto podría provocar una penalización innecesaria del rendimiento de la compilación.

* Ahora hay una API disponible para invalidar la caché de dependencias de Maven por canalización.

* La versión del tipo de archivo del proyecto AEM utilizado por Cloud Manager se ha actualizado a la versión 28.

### Corrección de errores {#bug-fixes}

* Actualizar el estado disponible no se debe mostrar cuando la última versión sea menor que la versión actual.

* La incorporación inicial estaba fallando para nuevas organizaciones con nombres muy largos.

* En ocasiones, cuando una canalización se activa dos veces por algún motivo, el resultado es que una de las ejecuciones falla con el error *no puede actualizar el estado de ejecución de la canalización*.


