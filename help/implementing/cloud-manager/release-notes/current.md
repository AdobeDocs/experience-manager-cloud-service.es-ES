---
title: Notas de la versión para Cloud Manager 2025.3.0 en Adobe Experience Manager as a Cloud Service
description: Obtenga información acerca del lanzamiento de Cloud Manager 2025.3.0 en AEM as a Cloud Service.
feature: Release Information
role: Admin
exl-id: 24d9fc6f-462d-417b-a728-c18157b23bbe
source-git-commit: 5983c8579dd8606bc8bedfe6fa2a3838493452cd
workflow-type: tm+mt
source-wordcount: '324'
ht-degree: 31%

---

# Notas de la versión para Cloud Manager 2025.3.0 en Adobe Experience Manager as a Cloud Service {#release-notes}

<!-- https://wiki.corp.adobe.com/display/DMSArchitecture/Cloud+Manager+2025.03.0+Release -->

Obtenga información sobre el lanzamiento de Cloud Manager 2025.3.0 en AEM (Adobe Experience Manager) as a Cloud Service.


Consulte también las [notas de la versión actual de Adobe Experience Manager as a Cloud Service](/help/release-notes/release-notes-cloud/release-notes-current.md).

## Fechas de lanzamiento {#release-date}

La fecha de lanzamiento de Cloud Manager 2025.3.0 en AEM as a Cloud Service es el viernes, 13 de marzo de 2025.

La próxima versión planificada es el viernes, 10 de abril de 2025.

## Novedades {#what-is-new}

* **Ejecutar varias canalizaciones**

  La capacidad de ejecutar varias canalizaciones simultáneamente se ha introducido en la página Canalizaciones. Los usuarios deben seleccionar al menos una canalización, pero no más de diez. Cerca de la esquina superior derecha de la página Canalizaciones, haga clic en **Ejecutar seleccionados (x)**. Aparecerá un cuadro de diálogo modal que enumera cualquier canalización que no se pueda iniciar. Haga clic en **Ejecutar** para iniciar todas las canalizaciones válidas.

  ![Ejecutar cuadro de diálogo de canalizaciones seleccionadas](/help/implementing/cloud-manager/release-notes/assets/run-selected-pipelines.png)

* **Se ha ampliado la compatibilidad a las versiones de Node.js**

  El entorno de compilación del front-end ahora es compatible con las siguientes `Node.js` versiones:

   * 23
   * 22
   * 20

  Consulte también [Desarrollo de sitios con la canalización front-end](/help/implementing/developing/introduction/developing-with-front-end-pipelines.md#node-versions). <!-- CMGR-65307 -->

<!--
## Early adoption program {#early-adoption}

Be a part of Cloud Manager's early adoption program and have a chance to test upcoming features. -->


## Correcciones de errores

* **(IU) Corrección para las actualizaciones &#39;Configuración de red avanzada&#39; en Cloud Manager**

  Se ha resuelto un problema poco frecuente que impedía realizar actualizaciones en la **Configuración avanzada de red** cuando había una notificación &quot;Actualización disponible&quot;. Anteriormente, Cloud Manager bloqueaba las modificaciones de configuración, incluida la configuración avanzada de red, para evitar conflictos durante una actualización. Los clientes ahora pueden almacenar en déclencheur manualmente la actualización pendiente para aplicar los cambios necesarios sin restricciones. <!-- CMGR-65913 and CMGR-65788 -->

* **(IU) Corrección para actualizaciones de lista de permitidos de IP atascadas en estado &quot;Actualizando&quot;**

  Se ha resuelto un problema poco frecuente en el que las actualizaciones de lista de permitidos de IP en Cloud Manager permanecían atascadas en el estado &quot;Actualizando&quot; debido a la configuración de dominio activo duplicado para un entorno. Anteriormente, los clientes experimentaban retrasos de procesamiento indefinidos al actualizar las listas de permitidos IP, lo que impedía realizar los ajustes de acceso a la red necesarios. Esta corrección garantiza que las actualizaciones de la lista de permitidos de IP ahora se puedan completar correctamente sin quedarse atascadas. <!-- CMGR-65786 -->




<!-- ## Known issues {#known-issues} -->
