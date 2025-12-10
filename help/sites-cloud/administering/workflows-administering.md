---
title: Administración de instancias de flujo de trabajo
description: Obtenga información sobre cómo administrar instancias de flujo de trabajo mediante la consola de flujo de trabajo
feature: Administering
role: Admin
exl-id: d2adb5e8-3f0e-4a3b-b7d0-dbbc5450e45f
solution: Experience Manager Sites
source-git-commit: 372d8969b1939e9a24d7910a1678a17c0dc9f9fd
workflow-type: tm+mt
source-wordcount: '1282'
ht-degree: 90%

---

# Administración de instancias de flujo de trabajo {#administering-workflow-instances}

La consola de flujo de trabajo proporciona varias herramientas para administrar instancias de flujo de trabajo a fin de garantizar que se ejecuten según lo esperado.

Hay una serie de consolas disponibles para administrar los flujos de trabajo. Utilice la variable [navegación global](/help/sites-cloud/authoring/basic-handling.md#global-navigation) para abrir el panel **Herramientas** y, a continuación, seleccione **Flujo de trabajo**:

* **Modelos**: Administrar definiciones de flujo de trabajo
* **Instancias**: Ver y administrar la ejecución de instancias de flujo de trabajo
* **Lanzadores**: Administrar el lanzamiento de los flujos de trabajo
* **Archivo**: Ver el historial de los flujos de trabajo que finalizaron correctamente
* **Errores**: Ver el historial de los flujos de trabajo que finalizaron con errores
* **Autoasignación**: Configurar los flujos de trabajo de autoasignación en las plantillas

## Monitorización del estado de las instancias de flujo de trabajo {#monitoring-the-status-of-workflow-instances}

1. Uso de la selección Navegación **Herramientas**, luego **Flujo de trabajo**.
1. Seleccione **Instancias** para mostrar la lista de instancias de flujo de trabajo actualmente en curso.
1. En el carril superior, en la esquina derecha, las instancias de flujo de trabajo muestran **Flujos de trabajo en ejecución**, **Estado** y **Detalles**.
1. **Flujos de trabajo en ejecución** muestra el número de flujos de trabajo en ejecución y su estado. por ejemplo, en las imágenes especificadas, se muestra el número de **Flujos de trabajo en ejecución** y el **Estado** de la instancia de AEM:

   * **Estado: correcto**
     ![status-healthy](/help/sites-cloud/administering/assets/status-healthy.png)

   * **Estado: incorrecto**
     ![estado-incorrecto](/help/sites-cloud/administering/assets/status-unhealthy.png)

1. En **Detalles del estado** de instancias de flujo de trabajo, haga clic en **Detalles**, para mostrar el **número de instancias de flujos de trabajo en ejecución**, **instancias de flujo de trabajo completadas**, **instancias de flujo de trabajo anuladas**, **instancias de flujo de trabajo fallidas**, etc. por ejemplo, a continuación se muestran las imágenes determinadas que muestran **Detalles del estado** con:

   * **Detalles del estado: correcto**
     ![status-details-healthy](/help/sites-cloud/administering/assets/status-details-healthy.png)

   * **Detalles del estado: incorrecto**
     ![detalles-estado-incorrecto](/help/sites-cloud/administering/assets/status-details-unhealthy.png)

   >[!NOTE]
   >
   > Para mantener la instancia de flujo de trabajo en buen estado, siga las prácticas recomendadas en [depuración regular de las instancias de flujo de trabajo](#regular-purging-of-workflow-instances) o [prácticas recomendadas del flujo de trabajo](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/extending-workflows/workflows-best-practices.html).

## Buscar instancias de flujo de trabajo {#search-workflow-instances}

1. Uso de la selección Navegación **Herramientas**, luego **Flujo de trabajo**.
1. Seleccione **Instancias** para mostrar la lista de instancias de flujo de trabajo en progreso. En el carril superior, en la esquina izquierda, seleccione **Filtros**. Alternativamente, puede utilizar las pulsaciones de teclas alt+1. Se muestra el cuadro de diálogo siguiente:

   ![wf-99-1](/help/sites-cloud/administering/assets/wf-99-1.png)

1. En el cuadro de diálogo Filtro, seleccione los criterios de búsqueda del flujo de trabajo. Puede buscar según estas entradas:

   * Ruta de carga útil: Seleccionar una ruta específica
   * Modelo de flujo de trabajo: Seleccionar un modelo de flujo de trabajo
   * Usuario asignado: Seleccione un usuario asignado del flujo de trabajo
   * Tipo: Tarea, elemento de flujo de trabajo o error de flujo de trabajo
   * Estado de la tarea: activo, completado o terminado
   * Donde Estoy: Propietario AND usuario asignado, solo propietario, solo usuario asignado
   * Fecha de inicio: Fecha de inicio antes o después de una fecha especificada
   * Fecha de finalización: Fecha de finalización anterior o posterior a una fecha especificada
   * Fecha de vencimiento: Fecha de vencimiento antes o después de una fecha especificada
   * Fecha de actualización: Fecha actualizada antes o después de una fecha especificada

## Suspender, reanudar y finalizar una instancia de flujo de trabajo {#suspending-resuming-and-terminating-a-workflow-instance}

1. Uso de la selección Navegación **Herramientas**, luego **Flujo de trabajo**.
1. Seleccione **Instancias** para mostrar la lista de instancias de flujo de trabajo en progreso.

   ![wf-96-1](/help/sites-cloud/administering/assets/wf-96-1.png)

1. Seleccione un elemento específico y, a continuación, utilice **Terminar**, **Suspender** o **Reanudar**, según proceda; confirmación o más detalles:

   ![wf-97-1](/help/sites-cloud/administering/assets/wf-97-1.png)

   >[!NOTE]
   >
   >
   >Para terminar o cancelar un flujo de trabajo, debe encontrarse en un estado de espera de intervención del usuario, como ocurre en la Etapa de participante. Es posible que al intentar anular un flujo de trabajo que está ejecutando trabajos en ese momento (subprocesos activos que están en ejecución) no se produzcan los resultados esperados.


## Visualización de flujos de trabajo archivados {#viewing-archived-workflows}

1. Uso de la selección Navegación **Herramientas**, luego **Flujo de trabajo**.

1. Seleccione **Archivo** para mostrar la lista de instancias de flujo de trabajo que se completaron correctamente.

   ![instancias-archivadas](/help/sites-cloud/administering/assets/archived-instances.png)

   >[!NOTE]
   >
   >
   >El estado de anulación se considera una terminación satisfactoria, ya que ocurre como resultado de la acción del usuario; por ejemplo:
   >
   >* uso de la acción **Terminar**
   >* cuando se elimina (a la fuerza) una página sujeta a un flujo de trabajo, a continuación, el flujo de trabajo termina.

1. Seleccione un elemento específico y luego **Abrir historial** para ver más detalles:

   ![wf-99](/help/sites-cloud/administering/assets/wf-99.png)

## Corrección de errores de instancias de flujo de trabajo {#fixing-workflow-instance-failures}

Cuando falla un flujo de trabajo, AEM proporciona la consola **Errores** para que pueda investigar y tomar las medidas adecuadas una vez que se haya manejado la causa original:

* **Detalles del error**
Abre una ventana para mostrar **Mensaje de error**, **Paso y &#x200B;** Pila de errores**.

* **Abrir historial**
Muestra detalles del historial del flujo de trabajo.

* **Paso de reintento** Ejecuta de nuevo la instancia del componente Paso de script. Utilice el comando Paso de reintento después de haber corregido la causa del error original. Por ejemplo, vuelva a intentar el paso después de corregir un error en el script que ejecuta el Paso de proceso.
* **Terminar** Termine el flujo de trabajo si el error ha provocado una situación irreconciliable. Por ejemplo, el flujo de trabajo puede depender de condiciones ambientales como la información del repositorio, que ya no son válidas para la instancia de flujo de trabajo.
* **Terminar y reintentar** similar a **Terminar**, excepto que se inicia una nueva instancia de flujo de trabajo utilizando la carga útil, el título y la descripción originales.

Para investigar los errores y luego reanudar o terminar el flujo de trabajo más tarde, siga estos pasos:

1. Mediante la Navegación, seleccione **Herramientas** y, luego, **Flujo de trabajo**.

1. Seleccione **Errores** para mostrar la lista de instancias de flujo de trabajo que no se completaron correctamente.
1. Seleccione un elemento específico y luego la acción apropiada:

![error-flujo de trabajo](/help/sites-cloud/administering/assets/workflow-failure.png)

## Depuración regular de instancias de flujo de trabajo {#regular-purging-of-workflow-instances}

Al minimizar el número de instancias de flujo de trabajo, aumenta el rendimiento del motor de flujo de trabajo, por lo que puede depurar con regularidad las instancias de flujo de trabajo completadas o en ejecución desde el repositorio.

Configure **Configuración de depuración del flujo de trabajo de Adobe Granite** para depurar instancias de flujo de trabajo según su antigüedad y estado. También puede depurar instancias de flujo de trabajo de todos los modelos o de uno específico.

También puede crear varias configuraciones del servicio para depurar instancias de flujo de trabajo que cumplan distintos criterios. Por ejemplo, cree una configuración que depure las instancias de un modelo de flujo de trabajo concreto cuando se ejecuten durante mucho más tiempo del esperado. Cree otra configuración que depure todos los flujos de trabajo completados después de un determinado número de días para minimizar el tamaño del repositorio.

Para configurar el servicio, puede configurar los archivos de configuración OSGi. Vea [Archivos de configuración OSGi](/help/implementing/deploying/configuring-osgi.md). En la tabla siguiente, se describen las propiedades que necesita para cualquiera de los métodos.

>[!NOTE]
>Para añadir la configuración al repositorio, el PID de servicio es este:
>`com.adobe.granite.workflow.purge.Scheduler`
>Como el servicio es un servicio de fábrica, el nombre del nodo `sling:OsgiConfig` requiere un sufijo de identificador, por ejemplo:
>`com.adobe.granite.workflow.purge.Scheduler-myidentifier`

| Nombre de propiedad (consola web) | Nombre de propiedad OSGi | Descripción |
|--- |--- |--- |
| Nombre de trabajo  | `scheduledpurge.name` | Un nombre descriptivo para la depuración programada. |
| Estado de flujo de trabajo | `scheduledpurge.workflowStatus` | El estado de las instancias de flujo de trabajo que se van a purgar. Los siguientes valores son válidos:<br><br>- COMPLETADO: Las instancias de flujo de trabajo completadas se purgan.<br>- EN EJECUCIÓN: las instancias de flujo de trabajo en ejecución se purgan. |
| Modelos para purgar | `scheduledpurge.modelIds` | El ID de los modelos de flujo de trabajo que se van a purgar.<br>El identificador es la ruta de acceso al nodo del modelo, por ejemplo:<br> `/conf/global/settings/workflow/models/dam/update_asset/jcr:content/model` <br><br> No especifique ningún valor para purgar instancias de todos los modelos de flujo de trabajo.<br>Para especificar varios modelos, haga clic en el botón `+` de la consola web. |
| Edad del flujo de trabajo | `scheduledpurge.daysold` | La antigüedad de las instancias de flujo de trabajo que se van a purgar, en días. |
| Paquete de carga útil de flujo | `scheduledpurge.purgePackagePayload` | Indica si el paquete de carga útil se debe purgar; `true` o `false`. |


## Configuración del tamaño máximo de la bandeja de entrada {#setting-the-maximum-size-of-the-inbox}

Puede configurar el tamaño máximo de la bandeja de entrada configurando el **Servicio de flujo de trabajo de Adobe Granite**. Consulte [Adición de una configuración OSGi al repositorio](/help/implementing/deploying/configuring-osgi.md). En la tabla siguiente se describe la propiedad que puede configurar.

>[!NOTE]
>Para añadir la configuración al repositorio, el PID de servicio es este:
>`com.adobe.granite.workflow.core.WorkflowSessionFactory`.

| Nombre de propiedad (consola web) | Nombre de propiedad OSGi |
|---|---|
| Tamaño máximo de consulta de la bandeja de entrada | granite.workflow.inboxQuerySize |

## Uso de variables de flujo de trabajo para almacenes de datos propiedad del cliente {#using-workflow-variables-customer-datastore}

Los datos procesados por flujos de trabajo se almacenan en el almacenamiento proporcionado por el Adobe (JCR). Estos datos pueden ser de naturaleza delicada. Es posible que desee guardar todos los metadatos/datos definidos por el usuario en su propio almacenamiento administrado en lugar del almacenamiento proporcionado por Adobe. En estas secciones se describe cómo configurar estas variables para el almacenamiento externo.

### Establecer el modelo para que utilice el almacenamiento externo de metadatos {#set-model-for-external-storage}

En el nivel del modelo de flujo de trabajo, se proporciona un indicador para indicar que el modelo (y sus instancias de tiempo de ejecución) tiene almacenamiento externo de metadatos. Las variables de flujo de trabajo no se mantendrán en JCR para las instancias de flujo de trabajo de los modelos marcados para almacenamiento externo.

La propiedad *userMetadataPersistenceEnabled* se almacena en el nodo *jcr:content* del modelo de flujo de trabajo. Este indicador se mantiene en los metadatos del flujo de trabajo como *cq:userMetaDataCustomPersistenceEnabled*.

La siguiente ilustración muestra cómo establecer el indicador en un flujo de trabajo.

![workflow-externalize-config](/help/sites-cloud/administering/assets/workflow-externalize-config.png)

### API para metadatos en almacenamiento externo {#apis-for-metadata-external-storage}

Para almacenar las variables de forma externa, debe implementar las API que expone el flujo de trabajo.

UserMetaDataPersistenceContext

Los siguientes ejemplos muestran cómo utilizar la API.

```
@ProviderType
public interface UserMetaDataPersistenceContext {
 
    /**
     * Gets the workflow for persistence
     * @return workflow
     */
    Workflow getWorkflow();
 
    /**
     * Gets the workflow id for persistence
     * @return workflowId
     */
    String getWorkflowId();
 
    /**
     * Gets the user metadata persistence id
     * @return userDataId
     */
    String getUserDataId();
}
```

UserMetaDataPersistenceProvider

```
/**
 * This provider can be implemented to store the user defined workflow-data metadata in a custom storage location
 */
@ConsumerType
public interface UserMetaDataPersistenceProvider {
 
   /**
    * Retrieves the metadata using a unique identifier
    * @param userMetaDataPersistenceContext
    * @param metaDataMap of user defined workflow data metaData
    * @throws WorkflowException
    */
   void get(UserMetaDataPersistenceContext userMetaDataPersistenceContext, MetaDataMap metaDataMap) throws WorkflowException;
 
   /**
    * Stores the given metadata to the custom storage location
    * @param userMetaDataPersistenceContext
    * @param metaDataMap metadata map
    * @return the unique identifier that can be used to retrieve metadata. If null is returned, then workflowId is used.
    * @throws WorkflowException
    */
   String put(UserMetaDataPersistenceContext userMetaDataPersistenceContext, MetaDataMap metaDataMap) throws WorkflowException;
 
} 
```
