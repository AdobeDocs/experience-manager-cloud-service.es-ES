---
title: Actualización de los fragmentos de contenido para el filtrado optimizado de GraphQL
description: Obtenga información sobre cómo actualizar los fragmentos de contenido para el filtrado optimizado de GraphQL en Adobe Experience Manager as a Cloud Service para el envío de contenido sin encabezado.
exl-id: 211f079e-d129-4905-a56a-4fddc11551cc
feature: Headless, Content Fragments,GraphQL API
role: Admin, Developer
source-git-commit: 8d14936ad21dc5879c72383defc3db22ce9a24ef
workflow-type: tm+mt
source-wordcount: '867'
ht-degree: 57%

---

# Actualización de los fragmentos de contenido para el filtrado optimizado de GraphQL {#updating-content-fragments-for-optimized-graphql-filtering}

Para optimizar el rendimiento de los filtros de GraphQL, ejecute un procedimiento para actualizar los fragmentos de contenido.

>[!NOTE]
>
>Después de actualizar los fragmentos de contenido, puede seguir las recomendaciones de [Optimización de las consultas de GraphQL](/help/headless/graphql-api/graphql-optimization.md).


## Requisitos previos {#prerequisites}

Hay requisitos previos para esta tarea:

1. Asegúrese de que tiene mínimo la versión 2023.1.0 de AEM as a Cloud Service.

1. Asegúrese de que el usuario que realiza la tarea tiene los permisos necesarios:

   * como mínimo, se requiere el rol `Deployment Manager` en Cloud Manager.

## Actualización de los fragmentos de contenido {#updating-content-fragments}

1. Habilite la actualización estableciendo las siguientes variables para su instancia mediante la IU de Cloud Manager:

   ![Configuración del entorno de Cloud Manager](assets/cfm-graphql-update-01.png "Configuración del entorno de Cloud Manager")

   Las variables disponibles son las siguientes:

   | | Nombre | Value | Valor predeterminado | Servicio | Aplicado | Tipo | Notas |
   |---|---|---|---|---|---|---|---|
   | 1 | `CF_MIGRATION_ENABLED` | `1` | `0` | Todos | | Variable | Habilita (!=0) o deshabilita (0) la activación del trabajo de migración de fragmentos de contenido. |
   | 2 | `CF_MIGRATION_ENFORCE` | `1` | `0` | Todos | | Variable | Aplica (!=0) remigración de fragmentos de contenido. Al establecer este indicador en 0 se realiza una migración incremental de los CF. Esto significa que, si el trabajo se finaliza por cualquier motivo, la siguiente ejecución del trabajo inicia la migración desde el punto en el que se finalizó. Se recomienda realizar la primera migración para la aplicación (valor=1). |
   | 3 | `CF_MIGRATION_BATCH` | `50` | `50` | Todos | | Variable | Tamaño del lote para guardar el número de fragmentos de contenido después de la migración. Esto es relevante para cuántos CF se guardan en el repositorio en un lote y se puede utilizar para optimizar el número de escrituras en el repositorio. |
   | 4 | `CF_MIGRATION_LIMIT` | `1000` | `1000` | Todos | | Variable | Número máximo de fragmentos de contenido para procesar a la vez. Vea también las notas de `CF_MIGRATION_INTERVAL`. |
   | 5 | `CF_MIGRATION_INTERVAL` | `60` | `600` | Todos | | Variable | Intervalo (segundos) para procesar los fragmentos de contenido restantes hasta el siguiente límite. Este intervalo también se considera como un tiempo de espera antes de iniciar el trabajo y un retraso entre el procesamiento de cada número CF_MIGRATION_LIMIT posterior de CF. (*) |

   >[!NOTE]
   >
   >(*)
   >
   >El valor de `CF_MIGRATION_INTERVAL` también puede ayudar a aproximar el tiempo total de ejecución del trabajo de migración.
   >
   >Por ejemplo:
   >
   >* Número total de fragmentos de contenido = 20 000
   >* CF_MIGRATION_LIMIT = 1000
   >* CF_MIGRATION_INTERNAL = 60 (s)
   >* Tiempo aproximado necesario para completar la migración = 60 + (20 000/1000 * 60) = 1260 s = 21 min
   >  Los “60” segundos adicionales añadidos al inicio se deben al retraso inicial al comenzar el trabajo.
   >
   >Este es solo el tiempo *mínimo* necesario para completar el trabajo y no incluye el tiempo de E/S. El tiempo real empleado podría ser superior a esta estimación.

1. Monitorice el progreso y la finalización de la actualización.

   Para ello, monitorice los registros de creación y publicación maestra desde aquí:

   * `com.adobe.cq.dam.cfm.impl.upgrade.UpgradeJob`

      * Registros de creación; por ejemplo:

        ```shell
        23.01.2023 13:13:45.926 *INFO* [sling-threadpool-09cbdb47-4d99-4c4c-b6d5-781b635ee21b-(apache-sling-job-thread-pool)-1-Content Fragment Upgrade Job Queue Config(cfm/upgrader)] com.adobe.cq.dam.cfm.impl.upgrade.UpgradeJob This instance<dd9ffdc1-0c28-4d04-9a96-5d4d223e457e> is the leader, will schedule the upgrade schedule job.
        ...
        23.01.2023 13:13:45.941 *INFO* [sling-threadpool-09cbdb47-4d99-4c4c-b6d5-781b635ee21b-(apache-sling-job-thread-pool)-1-Content Fragment Upgrade Job Queue Config(cfm/upgrader)] com.adobe.cq.dam.cfm.impl.upgrade.UpgradeJob Scheduling content fragments upgrade from version 0 to 1, slingJobId: 2023/1/23/13/13/50e1a575-4cd7-497b-adf0-62cb5768eedb_0, enforce: true, limit: 1000, batch: 50, interval: 60s
        
        23.01.2023 13:20:40.960 *INFO* [sling-threadpool-09cbdb47-4d99-4c4c-b6d5-781b635ee21b-(apache-sling-job-thread-pool)-1-Content Fragment Upgrade Job Queue Config(cfm/upgrader)] com.adobe.cq.dam.cfm.impl.upgrade.UpgradeJob Finished content fragments upgrade in 6m, slingJobId: 2023/1/23/13/13/50e1a575-4cd7-497b-adf0-62cb5768eedb_0, status: MaintenanceJobStatus{jobState=SUCCEEDED, statusMessage='Upgrade to version '1' succeeded.', errors=[], successCount=3781, failedCount=0, skippedCount=0}
        ```

      * Registros de publicación maestra; por ejemplo:

        ```shell
        23.01.2023 12:35:05.150 *INFO* [sling-threadpool-8abcc1bb-cdcb-46d4-8565-942ad8a73209-(apache-sling-job-thread-pool)-1-Content Fragment Upgrade Job Queue Config(cfm/upgrader)] com.adobe.cq.dam.cfm.impl.upgrade.UpgradeJob This instance<ad1b399e-77be-408e-bc3f-57097498fddb> is the leader, will schedule the upgrade schedule job.
        
        23.01.2023 12:35:05.161 *INFO* [sling-threadpool-8abcc1bb-cdcb-46d4-8565-942ad8a73209-(apache-sling-job-thread-pool)-1-Content Fragment Upgrade Job Queue Config(cfm/upgrader)] com.adobe.cq.dam.cfm.impl.upgrade.UpgradeJob Scheduling content fragments upgrade from version 0 to 1, slingJobId: 2023/1/23/12/34/ad1b399e-77be-408e-bc3f-57097498fddb_0, enforce: true, limit: 1000, batch: 50, interval: 60s
        ...
        23.01.2023 12:40:45.180 *INFO* [sling-threadpool-8abcc1bb-cdcb-46d4-8565-942ad8a73209-(apache-sling-job-thread-pool)-1-Content Fragment Upgrade Job Queue Config(cfm/upgrader)] com.adobe.cq.dam.cfm.impl.upgrade.UpgradeJob Finished content fragments upgrade in 5m, slingJobId: 2023/1/23/12/34/ad1b399e-77be-408e-bc3f-57097498fddb_0, status: MaintenanceJobStatus{jobState=SUCCEEDED, statusMessage='Upgrade to version '1' succeeded.', errors=[], successCount=3781, failedCount=0, skippedCount=0}
        ```

   Los clientes que han habilitado el acceso a los registros de entorno mediante Splunk, pueden utilizar la siguiente consulta de ejemplo para supervisar el proceso de actualización. Para obtener más información sobre cómo habilitar el registro de Splunk, consulte [Depuración de la producción y fase](/help/implementing/developing/introduction/logging.md#debugging-production-and-stage).

   ```splunk
   index=<indexName> sourcetype=aemerror aem_envId=<environmentId> msg="*com.adobe.cq.dam.cfm.impl.upgrade.UpgradeJob Finished*" 
   (aem_tier=golden-publish OR aem_tier=author) | table _time aem_tier pod_name msg | sort -_time desc
   ```

   Donde:

   * `environmentId` - un identificador de entorno del cliente; por ejemplo, `e1234`
   * `indexName` - un nombre de índice de cliente, recopilación de eventos `aemerror`

   Ejemplo de salida:

   <table style="table-layout:auto">
     <thead>
       <tr>
       <th>_hora</th>
       <th>aem_tier</th>
       <th>pod_name</th>
       <th>msg</th>
       </tr>
     </thead> 
     <tbody>
       <tr>
         <td>2023-04-21 06:00:35.723</td>
         <td>autor</td>
         <td>cm-p1234-e1234-aem-author-76d6dc4b79-8lsb5</td>
         <td>[sling-threadpool-bb5da4dd-6b05-4230-93ea-1d5cd242e24f-(apache-sling-job-thread-pool)-1-Content Fragment Upgrade Job Queue Config(cfm/upgrader)] com.adobe.cq.dam.cfm.impl.upgrade.upgrade.UpgradeJob Finalizó la actualización de fragmentos de contenido en 391m, slingJobId: 2023/4/20/23/16/db7963df-e267-489b-b69a-5930b0dadb37_0, estado: MaintenanceJobStatus{jobState=SUCCEEDED, statusMessage='Upgrade to version '1' success.', errors=[], successCount=36756, failedCount=0, skippedCount=0}</td>
       </tr>
       <tr>
         <td>2023-04-21 06:05:48.207</td>
         <td>golden-publish</td>
         <td>cm-p1234-e1234-aem-golden-publish-644487c9c5-lvkv2</td>
         <td>[sling-threadpool-284b9a9a-8454-461e-9bdb-44866c6ddfb1-(apache-sling-job-thread-pool)-1-Content Fragment Upgrade Job Queue Config(cfm/upgrader)] com.adobe.cq.dam.cfm.impl upgrade.UpgradeJob Finalizó la actualización de fragmentos de contenido en 211m, slingJobId: 2023/4/20/23/15/66c1690a-cdb7-4e66-bc52-90f33394ddfc_0, estado: MaintenanceJobStatus{jobState=SUCCEEDED, statusMessage='Upgrade to version '1' succeeded succeeded.', errors=[], successCount=19557, failedCount=0, skippedCount=0}</td>
       </tr>
     </tbody>
   <table>

1. Desactive el procedimiento de actualización.

   >[!IMPORTANT]
   >
   >Este paso es necesario para completar la actualización.

   Una vez ejecutado el procedimiento de actualización, restablezca la variable de entorno de la nube `CF_MIGRATION_ENABLED` a “0” para activar el reciclaje de todos los pods.

   | | Nombre | Value | Valor predeterminado | Servicio | Aplicado | Tipo | Notas |
   |---|---|---|---|---|---|---|---|
   | | `CF_MIGRATION_ENABLED` | `0` | `0` | Todos | | Variable | Deshabilita (0) [o habilita (!=0)] activando el trabajo de migración de fragmentos de contenido. |

   >[!NOTE]
   >
   >Esto es importante para el nivel de publicación, ya que la actualización de contenido solo se realiza en Golden Publish y, cuando se recicla de los pods, todos los pods de publicación normales se basan en Golden Publish.

1. Compruebe que se ha completado el procedimiento de actualización.

   Puede verificar la finalización correcta de la actualización mediante el explorador del repositorio en Developer Console de Cloud Manager para comprobar los datos del fragmento de contenido.

   * Antes de que se complete la primera migración, la propiedad `cfGlobalVersion` no existe.
Por lo tanto, la presencia de esta propiedad en el nodo JCR `/content/dam` con un valor de `1` confirma la finalización de la migración.

   * También puede verificar las siguientes propiedades en los fragmentos de contenido individuales:

      * `_strucVersion` debe tener el valor de `1`
      * La estructura `indexedData` debe existir

     >[!NOTE]
     >
     >El procedimiento actualiza los fragmentos de contenido en instancias de autor y Publish.
     >
     >Por lo tanto, el Adobe recomienda que realice la verificación mediante el explorador del repositorio para *al menos* una instancia de autor *y* una instancia de Publish.

## Limitaciones {#limitations}

Tenga en cuenta las siguientes limitaciones:

* La optimización del rendimiento de los filtros de GraphQL solo es posible después de una actualización completa de todos los fragmentos de contenido (indicada por la presencia de la propiedad `cfGlobalVersion` para el nodo JCR `/content/dam`)

* Si los fragmentos de contenido se importan desde un paquete de contenido (mediante `crx/de`) después de ejecutar el procedimiento de actualización, esos fragmentos de contenido no se tendrán en cuenta en los resultados de la consulta de GraphQL hasta que se vuelva a ejecutar el procedimiento de actualización.
