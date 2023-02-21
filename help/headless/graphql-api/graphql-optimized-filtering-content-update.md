---
title: Actualización de los fragmentos de contenido para el filtrado optimizado de GraphQL
description: Obtenga información sobre cómo actualizar los fragmentos de contenido para el filtrado optimizado de GraphQL en Adobe Experience Manager as a Cloud Service para la entrega de contenido sin encabezado.
source-git-commit: 1561668046909e88c283145205c16b167c04ca8c
workflow-type: tm+mt
source-wordcount: '738'
ht-degree: 6%

---


# Actualización de los fragmentos de contenido para un filtrado optimizado de GraphQL {#updating-content-fragments-for-optimized-graphql-filtering}

Para optimizar el rendimiento de los filtros de GraphQL, debe ejecutar un procedimiento para actualizar los fragmentos de contenido.

>[!NOTE]
>
>Después de actualizar los fragmentos de contenido, puede seguir las recomendaciones de [Optimización de consultas de GraphQL](/help/headless/graphql-api/graphql-optimization.md).


## Requisitos previos {#prerequisites}

Asegúrese de que tiene como mínimo la versión 2023.1.0 de AEM as a Cloud Service.

## Actualización de los fragmentos de contenido {#updating-content-fragments}

Para ejecutar el procedimiento, siga estos pasos:

1. Habilite la actualización estableciendo las siguientes variables para su instancia mediante la interfaz de usuario de Cloud Manager:

   ![Configuración del entorno de Cloud Manager](assets/cfm-graphql-update-01.png "Configuración del entorno de Cloud Manager")

   Las variables disponibles son:

   <table style="table-layout:auto">
    <tbody>
     <tr>
      <th> </th>
      <th>Nombre</th>
      <th>Value</th>
      <th>Valor predeterminado</th>
      <th>Servicio</th>
      <th>Aplicado</th>
      <th>Tipo</th>
      <th>Notas</th>
     </tr>
     <tr>
      <td>1</td>
      <td>`AEM_RELEASE_CHANNEL` </td>
      <td>`versión preliminar' </td>
      <td> </td>
      <td>Todos </td>
      <td> </td>
      <td>Variable </td>
      <td>Necesario para activar la función. </td>
     </tr>
     <tr>
      <td>2</td>
      <td>`CF_MIGRATION_ENABLED` </td>
      <td>`1` </td>
      <td>`0` </td>
      <td>Todos </td>
      <td> </td>
      <td>Variable </td>
      <td>Habilita(!=0) o deshabilita(0) la activación del trabajo de migración de fragmentos de contenido. </td>
     </tr>
     <tr>
      <td>3</td>
      <td>`CF_MIGRATION_ENFORCE` </td>
      <td>`1` </td>
      <td>`0` </td>
      <td>Todos </td>
      <td> </td>
      <td>Variable </td>
      <td>Aplicar (!=0) remigración de fragmentos de contenido.<br>Si establece este indicador en 0, se realizará una migración incremental de los CF. Esto significa que, si el trabajo termina por cualquier razón, la próxima ejecución del trabajo comenzará la migración desde el punto en el que finalizó. Tenga en cuenta que se recomienda aplicar la primera migración (valor=1). </td>
     </tr>
     <tr>
      <td>4</td>
      <td>`CF_MIGRATION_BATCH` </td>
      <td>`50` </td>
      <td>`50` </td>
      <td>Todos </td>
      <td> </td>
      <td>Variable </td>
      <td>Tamaño del lote para guardar el número de fragmentos de contenido después de la migración.<br>Esto es relevante para cuántos CF se guardarán en el repositorio en un lote y se puede utilizar para optimizar el número de escrituras en el repositorio. </td>
     </tr>
     <tr>
      <td>5</td>
      <td>`CF_MIGRATION_LIMIT` </td>
      <td>`1000` </td>
      <td>`1000` </td>
      <td>Todos </td>
      <td> </td>
      <td>Variable </td>
      <td>Número máximo de fragmentos de contenido que se procesarán a la vez.<br>Consulte también las notas de "CF_MIGRATION_INTERVAL". </td>
     </tr>
     <tr>
      <td>6</td>
      <td>`CF_MIGRATION_INTERVAL` </td>
      <td>"60" </td>
      <td>`600` </td>
      <td>Todos </td>
      <td> </td>
      <td>Variable </td>
      <td>Intervalo (segundos) para procesar los fragmentos de contenido restantes hasta el siguiente límite<br>Este intervalo también se considera como un tiempo de espera antes de iniciar el trabajo, así como un retraso entre el procesamiento de cada número posterior de CF_MIGRATION_LIMIT de CFs.<br>(*)</td>
     </tr>
    </tbody>
   </table>

   >[!NOTE]
   >
   >(*)
   >
   >El valor de `CF_MIGRATION_INTERVAL` también puede ayudar a aproximar el tiempo de ejecución total del trabajo de migración.
   >
   >Por ejemplo:
   >
   >* Número total de fragmentos de contenido = 20 000
   >* CF_MIGRATION_LIMIT = 1000
   >* CF_MIGRATION_INTERNAL = 60 (Sec)
   >* Tiempo aproximado necesario para completar la migración = 60 + (20.000/1000 * 60) = 1.260 Sec = 21 Minutos
      >  Los &quot;60&quot; segundos adicionales añadidos al principio se deben al retraso inicial al iniciar el trabajo.

   >
   >También debe tener en cuenta que esta es solo la variable *mínimo* tiempo necesario para completar el trabajo y no incluye el tiempo de E/S. El tiempo real que se tarda podría ser significativamente mayor que esta estimación.

1. Monitorice el progreso y la finalización de la actualización.

   Para ello, supervise los registros de creación y publicación de oro desde:

   * `com.adobe.cq.dam.cfm.impl.upgrade.UpgradeJob`

      * Registros de autor; por ejemplo:

         ```shell
         23.01.2023 13:13:45.926 *INFO* [sling-threadpool-09cbdb47-4d99-4c4c-b6d5-781b635ee21b-(apache-sling-job-thread-pool)-1-Content Fragment Upgrade Job Queue Config(cfm/upgrader)] com.adobe.cq.dam.cfm.impl.upgrade.UpgradeJob This instance<dd9ffdc1-0c28-4d04-9a96-5d4d223e457e> is the leader, will schedule the upgrade schedule job.
         ...
         23.01.2023 13:13:45.941 *INFO* [sling-threadpool-09cbdb47-4d99-4c4c-b6d5-781b635ee21b-(apache-sling-job-thread-pool)-1-Content Fragment Upgrade Job Queue Config(cfm/upgrader)] com.adobe.cq.dam.cfm.impl.upgrade.UpgradeJob Scheduling content fragments upgrade from version 0 to 1, slingJobId: 2023/1/23/13/13/50e1a575-4cd7-497b-adf0-62cb5768eedb_0, enforce: true, limit: 1000, batch: 50, interval: 60s
         
         23.01.2023 13:20:40.960 *INFO* [sling-threadpool-09cbdb47-4d99-4c4c-b6d5-781b635ee21b-(apache-sling-job-thread-pool)-1-Content Fragment Upgrade Job Queue Config(cfm/upgrader)] com.adobe.cq.dam.cfm.impl.upgrade.UpgradeJob Finished content fragments upgrade in 6m, slingJobId: 2023/1/23/13/13/50e1a575-4cd7-497b-adf0-62cb5768eedb_0, status: MaintenanceJobStatus{jobState=SUCCEEDED, statusMessage='Upgrade to version '1' succeeded.', errors=[], successCount=3781, failedCount=0, skippedCount=0}
         ```
   * Registros de publicación dorada; por ejemplo:

      ```shell
      23.01.2023 12:35:05.150 *INFO* [sling-threadpool-8abcc1bb-cdcb-46d4-8565-942ad8a73209-(apache-sling-job-thread-pool)-1-Content Fragment Upgrade Job Queue Config(cfm/upgrader)] com.adobe.cq.dam.cfm.impl.upgrade.UpgradeJob This instance<ad1b399e-77be-408e-bc3f-57097498fddb> is the leader, will schedule the upgrade schedule job.
      
      23.01.2023 12:35:05.161 *INFO* [sling-threadpool-8abcc1bb-cdcb-46d4-8565-942ad8a73209-(apache-sling-job-thread-pool)-1-Content Fragment Upgrade Job Queue Config(cfm/upgrader)] com.adobe.cq.dam.cfm.impl.upgrade.UpgradeJob Scheduling content fragments upgrade from version 0 to 1, slingJobId: 2023/1/23/12/34/ad1b399e-77be-408e-bc3f-57097498fddb_0, enforce: true, limit: 1000, batch: 50, interval: 60s
      ...
      23.01.2023 12:40:45.180 *INFO* [sling-threadpool-8abcc1bb-cdcb-46d4-8565-942ad8a73209-(apache-sling-job-thread-pool)-1-Content Fragment Upgrade Job Queue Config(cfm/upgrader)] com.adobe.cq.dam.cfm.impl.upgrade.UpgradeJob Finished content fragments upgrade in 5m, slingJobId: 2023/1/23/12/34/ad1b399e-77be-408e-bc3f-57097498fddb_0, status: MaintenanceJobStatus{jobState=SUCCEEDED, statusMessage='Upgrade to version '1' succeeded.', errors=[], successCount=3781, failedCount=0, skippedCount=0}
      ```


1. Desactive el procedimiento de actualización.

   >[!IMPORTANT]
   >
   >Este paso es necesario para completar la actualización.

   Una vez ejecutado el procedimiento de actualización, restablezca la variable de entorno de nube `CF_MIGRATION_ENABLED` a &quot;0&quot;, para déclencheur del reciclado de todos los pods.

   <table>
    <tbody>
     <tr>
      <th> </th>
      <th>Nombre</th>
      <th>Value</th>
      <th>Valor predeterminado</th>
      <th>Servicio</th>
      <th>Aplicado</th>
      <th>Tipo</th>
      <th>Notas</th>
     </tr>
     <tr>
      <td></td>
      <td>`CF_MIGRATION_ENABLED` </td>
      <td>`0` </td>
      <td>`0` </td>
      <td>Todos </td>
      <td> </td>
      <td>Variable </td>
      <td>Deshabilita(0) (o Habilita(!)=0)) activación del trabajo de migración de fragmentos de contenido. </td>
     </tr>
    </tbody>
   </table>

   >[!NOTE]
   >
   >Esto es especialmente importante para el nivel de publicación, ya que la actualización de contenido solo se realiza en la publicación de oro y, cuando se reciclan los pods, todos los pods normales de publicación se basan en la publicación de oro.

1. Verifique que se haya completado el procedimiento de actualización.

   Puede verificar que la actualización se haya completado correctamente mediante el explorador del repositorio en la consola del desarrollador de Cloud Manager para comprobar los datos del fragmento de contenido.

   * Antes de la primera migración completa, la variable `cfGlobalVersion` no existirá.
Por lo tanto, la presencia de esta propiedad, en el nodo JCR `/content/dam` con un valor de `1`, confirma la finalización de la migración.

   * También puede comprobar las siguientes propiedades en los fragmentos de contenido individuales:

      * `_strucVersion` debe tener el valor de `1`
      * `indexedData` estructura debe existir

      >[!NOTE]
      >
      >El procedimiento actualizará los fragmentos de contenido en las instancias de autor y publicación.
      >
      >Por lo tanto, se recomienda realizar la verificación mediante el explorador del repositorio para *al menos* un autor *y* una instancia de publicación.


## Restricciones {#limitations}

Tenga en cuenta las siguientes limitaciones:

* La optimización del rendimiento de los filtros de GraphQL solo será posible después de una actualización completa de todos los fragmentos de contenido (indicada por la presencia del `cfGlobalVersion` propiedad para el nodo JCR `/content/dam`)

* Si los fragmentos de contenido se importan desde un paquete de contenido (mediante `crx/de`) después de ejecutar el procedimiento de actualización, esos fragmentos de contenido no se tendrán en cuenta en los resultados de la consulta de GraphQL hasta que se vuelva a ejecutar el procedimiento de actualización.