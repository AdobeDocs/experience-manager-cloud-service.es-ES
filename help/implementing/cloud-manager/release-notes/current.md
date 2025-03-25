---
title: Notas de la versión para Cloud Manager 2025.3.0 en Adobe Experience Manager as a Cloud Service
description: Obtenga información acerca del lanzamiento de Cloud Manager 2025.3.0 en AEM as a Cloud Service.
feature: Release Information
role: Admin
exl-id: 24d9fc6f-462d-417b-a728-c18157b23bbe
source-git-commit: 663234640f16e6aa653251399751abf5daa17f82
workflow-type: ht
source-wordcount: '329'
ht-degree: 100%

---

# Notas de la versión para Cloud Manager 2025.3.0 en Adobe Experience Manager as a Cloud Service {#release-notes}

<!-- https://wiki.corp.adobe.com/display/DMSArchitecture/Cloud+Manager+2025.03.0+Release -->

Obtenga información sobre el lanzamiento de Cloud Manager 2025.3.0 en AEM (Adobe Experience Manager) as a Cloud Service.


Consulte también las [notas de la versión actual de Adobe Experience Manager as a Cloud Service](/help/release-notes/release-notes-cloud/release-notes-current.md).

## Fechas de lanzamiento {#release-date}

La fecha de lanzamiento de Cloud Manager 2025.3.0 en AEM as a Cloud Service es el jueves, 13 de marzo de 2025.

La próxima versión planificada es el jueves, 10 de abril de 2025.

## Novedades {#what-is-new}

* **Ejecutar varias canalizaciones**

  Se ha introducido en la página Canalizaciones la posibilidad de ejecutar varias canalizaciones simultáneamente. Los usuarios deben seleccionar al menos una canalización, pero no más de 10. Cerca de la esquina superior derecha de la página Canalizaciones, haga clic en **Ejecutar seleccionadas (x)**. Aparecerá un cuadro de diálogo modal que enumera cualquier canalización que no se pueda iniciar. Haga clic en **Ejecutar** para iniciar todas las canalizaciones válidas.

  ![Cuadro de diálogo Ejecutar canalizaciones seleccionadas](/help/implementing/cloud-manager/release-notes/assets/run-selected-pipelines.png)

  Véase también [Ejecutar varias canalizaciones](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md#run-multiple-pipelines)

* **Compatibilidad ampliada a las versiones de Node.js**

  El entorno de compilación front-end ahora es compatible con las siguientes versiones de `Node.js`:

   * 23
   * 22
   * 20

  Consulte también [Desarrollo de sitios con la canalización front-end](/help/implementing/developing/introduction/developing-with-front-end-pipelines.md#node-versions). <!-- CMGR-65307 -->

<!--
## Early adoption program {#early-adoption}

Be a part of Cloud Manager's early adoption program and have a chance to test upcoming features. -->


## Correcciones de errores

* **(IU) Corrección de las actualizaciones &#39;Configuración de red avanzada&#39; en Cloud Manager**

  Se ha resuelto un problema poco frecuente que impedía realizar actualizaciones en la **Configuración de red avanzada** cuando había una notificación &quot;Actualización disponible&quot;. Anteriormente, Cloud Manager bloqueaba las modificaciones de configuración, incluida la configuración avanzada de red, para evitar conflictos durante una actualización. Ahora los clientes ahora pueden activar manualmente la actualización pendiente para aplicar los cambios necesarios sin restricciones. <!-- CMGR-65913 and CMGR-65788 -->

* **(IU) Corrección de las actualizaciones de la lista de direcciones IP permitidas bloqueadas en el estado &quot;Actualizando&quot;**

  Se ha resuelto un problema poco frecuente en el que las actualizaciones de la lista de direcciones IP permitidas de Cloud Manager permanecían bloqueadas en el estado &quot;Actualizando&quot; debido a la configuración de dominio activo duplicado para un entorno. Anteriormente, los clientes experimentaban retrasos de procesamiento indefinidos al actualizar las listas de IP permitidas, lo que impedía realizar los ajustes de acceso a la red necesarios. Esta corrección garantiza que las actualizaciones de la lista de direcciones IP permitidas ahora se puedan completar correctamente sin quedarse bloqueadas. <!-- CMGR-65786 -->




<!-- ## Known issues {#known-issues} -->
