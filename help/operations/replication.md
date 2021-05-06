---
title: Replicación
description: Distribución y Resolución de problemas de replicación.
exl-id: c84b4d29-d656-480a-a03a-fbeea16db4cd
translation-type: tm+mt
source-git-commit: eb92c66f2b9e8e6ec859114da2de049747ec251e
workflow-type: tm+mt
source-wordcount: '786'
ht-degree: 2%

---

# Replicación {#replication}

Adobe Experience Manager as a Cloud Service utiliza la capacidad [Sling Content Distribution](https://sling.apache.org/documentation/bundles/content-distribution.html) para mover el contenido a un servicio de canalización que se ejecute en un Adobe I/O que esté fuera del tiempo de ejecución de AEM.

>[!NOTE]
>
>Lea [Distribución](/help/core-concepts/architecture.md#content-distribution) para obtener más información.

## Métodos de publicación de contenido {#methods-of-publishing-content}

### Cancelación/publicación rápida: cancelación/publicación planeada {#publish-unpublish}

Estas funcionalidades de AEM estándar para los autores no cambian con AEM Cloud Service.

### Tiempos de activación y desactivación: Configuración de Déclencheur {#on-and-off-times-trigger-configuration}

Las posibilidades adicionales de **Tiempo de activación** y **Tiempo de inactividad** están disponibles en la pestaña [Básico de Propiedades de página](/help/sites-cloud/authoring/fundamentals/page-properties.md#basic).

Para realizar la replicación automática para esto, debe habilitar **Replicación automática** en la [configuración OSGi](/help/implementing/deploying/configuring-osgi.md) **Configuración del Déclencheur desactivado**:

![Configuración del Déclencheur de activación de OSGi](/help/operations/assets/replication-on-off-trigger.png)

### Activación de árbol {#tree-activation}

Para realizar una activación de árbol:

1. En el menú Inicio de AEM, vaya a **Herramientas > Implementación > Distribución**
2. Seleccione la tarjeta **forwardPublisher**
3. Una vez en la interfaz de usuario de la consola web de forwardPublisher, **seleccione Distribuir**

   ![](assets/distribute.png "DistribuirDistribuir")
4. Seleccione la ruta en el navegador de rutas, elija añadir un nodo, árbol o eliminar según sea necesario y seleccione **Submit**

### Flujo de trabajo del árbol de contenido {#publish-content-tree-workflow}

Puede almacenar en déclencheur una replicación de árbol seleccionando **Tools - Workflow - Models** y copiando el modelo de flujo de trabajo **Publish Content Tree** listo para usar, como se muestra a continuación:

![](/help/operations/assets/publishcontenttreeworkflow.png)

No modifique ni invoque el modelo original. En su lugar, asegúrese de copiar primero el modelo y luego modificar o invocar esa copia.

Al igual que todos los flujos de trabajo, también se puede invocar mediante API. Para obtener más información, consulte [Interacción con flujos de trabajo mediante programación](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/extending-workflows/workflows-program-interaction.html?lang=en#extending-aem).

También puede conseguirlo creando un modelo de flujo de trabajo que utilice el paso de proceso `Publish Content Tree`:

1. Desde la página de inicio de AEM as a Cloud Service, vaya a **Herramientas - Flujo de trabajo - Modelos**
1. En la página Modelos de flujo de trabajo , pulse **Crear** en la esquina superior derecha de la pantalla
1. Añada un título y un nombre al modelo. Para obtener más información, consulte [Creación de modelos de flujo de trabajo](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/extending-workflows/workflows-models.html)
1. Seleccione el modelo recién creado de la lista y pulse **Editar**
1. En la siguiente ventana, arrastre y suelte el paso de proceso en el flujo del modelo actual:

   ![Etapa del proceso](/help/operations/assets/processstep.png)

1. Haga clic en el paso Proceso del flujo y seleccione **Configurar** pulsando el icono de la llave inglesa
1. Haga clic en la pestaña **Process** y seleccione `Publish Content Tree` en la lista desplegable

   ![Activación mediante árbol](/help/operations/assets/newstep.png)

1. Establezca cualquier parámetro adicional en el campo **Arguments**. Los argumentos separados por comas múltiples se pueden agrupar. Por ejemplo:

   `enableVersion=true,agentId=publish`


   >[!NOTE]
   >
   >Para obtener la lista de parámetros, consulte la sección **Parameters** a continuación.

1. Pulse **Listo** para guardar el modelo de flujo de trabajo.

**Parámetros**

* `replicateAsParticipant` (valor booleano, predeterminado:  `false`). Si se configura como `true`, la replicación utiliza el `userid` del principal que realizó el paso del participante.
* `enableVersion` (valor booleano, predeterminado:  `true`). Este parámetro determina si se crea una nueva versión tras la replicación.
* `agentId` (valor de cadena, predeterminado significa que se utilizan todos los agentes habilitados).
* `filters` (valor de cadena, predeterminado significa que todas las rutas están activadas). Los valores disponibles son:
   * `onlyActivated` - sólo se activarán las rutas que no estén marcadas como activadas.
   * `onlyModified` - activar solo las rutas que ya están activadas y que tienen una fecha de modificación posterior a la fecha de activación.
   * Lo anterior puede ser Oed con una barra vertical &quot;|&quot;. Por ejemplo, `onlyActivated|onlyModified`.

**Registro**

Cuando se inicie el paso del flujo de trabajo de activación del árbol, registrará sus parámetros de configuración en el nivel de registro INFO. Cuando se activan las rutas, también se registra una instrucción INFO.

A continuación, se registra una instrucción INFO final después de que el paso del flujo de trabajo haya duplicado todas las rutas.

Además, puede aumentar el nivel de registro de los registradores por debajo de `com.day.cq.wcm.workflow.process.impl` a DEBUG/TRACE para obtener aún más información de registro.

En caso de errores, el paso del flujo de trabajo finaliza con un `WorkflowException`, que ajusta la excepción subyacente.

A continuación, se muestran ejemplos de registros generados durante un flujo de trabajo de árbol de contenido de publicación de muestra:

```
21.04.2021 19:14:55.566 [cm-p123-e456-aem-author-797aaaf-wkkqt] *INFO* [JobHandler: /var/workflow/instances/server60/2021-04-20/brian-tree-replication-test-2_1:/content/wknd/us/en/adventures] com.day.cq.wcm.workflow.process.impl.treeactivation.TreeActivationWorkflowProcess TreeActivation options: replicateAsParticipant=false(userid=workflow-process-service), agentId=publish, chunkSize=100, filter=, enableVersion=false
```

```
21.04.2021 19:14:58.541 [cm-p123-e456-aem-author-797aaaf-wkkqt] *INFO* [JobHandler: /var/workflow/instances/server60/2021-04-20/brian-tree-replication-test-2_1:/content/wknd/us/en/adventures] com.day.cq.wcm.workflow.process.impl.ChunkedReplicator closing chunkedReplication-VolatileWorkItem_node1_var_workflow_instances_server60_2021-04-20_brian-tree-replication-test-2_1, 17 paths replicated in 2971 ms
```

**Reanudar compatibilidad**

El flujo de trabajo procesa el contenido en fragmentos, cada uno de los cuales representa un subconjunto del contenido completo que se va a publicar. Si, por cualquier motivo, el sistema detiene el flujo de trabajo, se reiniciará y procesará el fragmento que aún no se haya procesado. Una sentencia de registro indicará que el contenido se ha reanudado desde una ruta específica.

## Solución de problemas {#troubleshooting}

Para solucionar problemas de replicación, vaya a las colas de replicación en la interfaz de usuario web del servicio de autor de AEM:

1. En el menú Inicio de AEM, vaya a **Tools > Deployment > Distribution**
2. Seleccione la tarjeta **forwardPublisher**
   ![](assets/status.png "StatusStatus")
3. Comprobar el estado de la cola que debería ser verde
4. Puede probar la conexión con el servicio de replicación
5. Seleccione la pestaña **Logs** que muestra el historial de publicaciones de contenido

![](assets/logs.png "LogsLogs")

Si no se pudo publicar el contenido, toda la publicación se revierte desde el servicio de publicación de AEM.
En ese caso, las colas deben revisarse para identificar qué elementos causaron la cancelación de la publicación. Al hacer clic en una cola que muestra un estado rojo, se mostraría la cola con elementos pendientes, desde la cual se pueden borrar todos o uno de los elementos si es necesario.
