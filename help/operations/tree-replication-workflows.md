---
title: Flujos de trabajo de replicación de árbol en AEM as a Cloud Service
description: Obtenga información sobre cómo duplicar jerarquías de contenido profundas mediante el paso del flujo de trabajo de activación de árbol y los flujos de trabajo relacionados en AEM as a Cloud Service.
feature: Operations
role: Admin
source-git-commit: d6555eebfa13a400f084ef4edefb92b4471adcac
workflow-type: tm+mt
source-wordcount: '1078'
ht-degree: 24%

---

# Flujos de trabajo de replicación de árbol en AEM as a Cloud Service {#tree-replication-workflows}

Cuando debe publicar una rama grande del árbol de contenido, la publicación página por página estándar puede ser lenta y requerir muchos recursos. AEM as a Cloud Service proporciona enfoques basados en flujos de trabajo que replican jerarquías de contenido profundo en fragmentos manejables, realizan pausas cuando las colas de replicación están ocupadas y se reanudan si se interrumpen.

Use el **Paso del flujo de trabajo de activación de árbol** para la replicación de árbol en masa. Es el método recomendado para cargas útiles grandes. El **Flujo de trabajo Publicar árbol de contenido** permanece documentado para referencia, pero está obsoleto en favor del paso Activación del árbol.

Para ver otros temas de replicación, vea [Replicación](/help/operations/replication.md).

## Etapa de flujo de trabajo de activación de árbol {#tree-activation}

El paso del flujo de trabajo de activación de árbol está diseñado para replicar de forma eficaz una jerarquía profunda de nodos de contenido. Se pone en pausa automáticamente cuando la cola crece demasiado para permitir que otras réplicas se realicen en paralelo con una latencia mínima.

Crear un modelo de flujo de trabajo que utilice el paso de proceso `TreeActivation`:

1. Desde la página de inicio de AEM as a Cloud Service, vaya a **Herramientas - Flujo de trabajo - Modelos**.
1. En la página Modelos de flujo de trabajo, presione **Crear** en la esquina superior derecha de la pantalla.
1. Agregue un título y un nombre al modelo. Para obtener más información, consulte [Creación de modelos de flujo de trabajo](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/extending-workflows/workflows-models.html?lang=es).
1. Seleccione el modelo creado de la lista y pulse **Editar**
1. En la siguiente ventana, elimine el Paso que aparece por defecto
1. Arrastre y suelte el paso Proceso en el flujo del modelo actual:

   ![Etapa del proceso](/help/operations/assets/processstep.png)

1. Seleccione el paso Proceso en el flujo y seleccione **Configurar** pulsando el icono de la llave inglesa.
1. Seleccione la ficha **Proceso**, seleccione `Publish Content Tree` en la lista desplegable y, a continuación, marque la casilla de verificación **Avance del controlador**

   ![Activación mediante árbol](/help/operations/assets/new-treeactivationstep.png)

1. Configure cualquier parámetro adicional en el campo **Argumentos**. Se pueden unir varios argumentos separados por comas. Por ejemplo:

   `enableVersion=false,agentId=publish,chunkSize=50,maxTreeSize=500000,dryRun=false,filters=onlyModified,maxQueueSize=10`

   >[!NOTE]
   >
   >Para obtener la lista de parámetros, consulte la sección **Parámetros** a continuación.

1. Pulse **Listo** para guardar el modelo de flujo de trabajo.

**Parámetros**

| Nombre | predeterminado | descripción |
| -------------- | ------- | --------------------------------------------------------------- |
| path |         | ruta raíz desde la que comenzar |
| agentId | publicación | Agente que recibe la replicación (`publish` o `preview`) |
| chunkSize | 50 | Número de rutas para agrupar en una sola replicación |
| maxTreeSize | 500000 | Número máximo de nodos para que un árbol se considere pequeño |
| maxQueueSize | 10 | Número máximo de elementos en la cola de replicación |
| enableVersion | false | Activar control de versiones |
| dryRun | false | Cuando se establece en true, no se llama a la replicación |
| userId |         | solo para el trabajo. En el flujo de trabajo se utiliza el usuario que llama al flujo de trabajo |
| filtros |         | Lista de nombres de filtros de nodo. Consulte los filtros admitidos a continuación |

**Filtros de soporte**

| Nombre | Descripción |
| ------------- | ------------------------------------------- |
| onlyModified | Nodos: tanto nuevos como preexistentes que se han modificado desde la última publicación |
| onlyActivated | Nodos: que se publicaron antes de la última publicación |


**Reanudar compatibilidad**

El flujo de trabajo procesa el contenido en fragmentos, cada uno de los cuales representa un subconjunto del contenido completo que se va a publicar.  Si el sistema detiene el flujo de trabajo, continuará donde lo dejó.

**Supervisar el progreso del flujo de trabajo**

1. Desde la página de inicio de AEM as a Cloud Service, vaya a **Herramientas - General - Trabajos**.
1. Observe la fila correspondiente al flujo de trabajo. La columna *progreso* proporciona una indicación del progreso de la replicación. Por ejemplo, puede mostrar 41/564 y, al actualizar, puede actualizarse a 52/564.

   ![Progreso de activación del árbol](/help/operations/assets/treeactivation-progress.png)


1. Si se selecciona la fila y se abre, se proporcionan detalles adicionales sobre el estado de ejecución del flujo de trabajo.

   ![Detalles del estado de activación del árbol](/help/operations/assets/treeactivation-progress-details.png)



## Publicación del flujo de trabajo del árbol de contenido {#publish-content-tree-workflow}

>[!NOTE]
>
>Esta función queda obsoleta y prefiere el paso de activación de árbol, que es más eficiente y se puede incluir en un flujo de trabajo personalizado.

+++ Haga clic aquí para obtener más información sobre esta función obsoleta.

Puede activar una replicación de árbol seleccionando **Herramientas - Flujo de trabajo - Modelos** y copiando el modelo de flujo de trabajo integrado **Árbol de contenido de publicación**, como se muestra a continuación:

![La tarjeta de flujo de trabajo para publicar árbol de contenido](/help/operations/assets/publishcontenttreeworkflow.png)

No invoque el modelo original. En su lugar, asegúrese de copiar primero el modelo e invocar esa copia.

Al igual que todos los flujos de trabajo, también se puede invocar mediante una API. Para obtener más información, vea [Interactuar con flujos de trabajo mediante programación](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/extending-workflows/workflows-program-interaction.html#extending-aem).

También puede crear un modelo de flujo de trabajo que utilice el paso de proceso `Publish Content Tree`.

1. Desde la página de inicio de AEM as a Cloud Service, vaya a **Herramientas - Flujo de trabajo - Modelos**.
1. En la página Modelos de flujo de trabajo, presione **Crear** en la esquina superior derecha de la pantalla.
1. Agregue un título y un nombre al modelo. Para obtener más información, consulte [Creación de modelos de flujo de trabajo](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/extending-workflows/workflows-models.html?lang=es).
1. Seleccione el modelo creado de la lista y pulse **Editar**
1. En la siguiente ventana, arrastre y suelte el paso de proceso en el flujo del modelo actual:

   ![Etapa del proceso](/help/operations/assets/processstep.png)

1. Seleccione el paso Proceso en el flujo y seleccione **Configurar** pulsando el icono de la llave inglesa.
1. Seleccione la ficha **Proceso**, seleccione `Publish Content Tree` en la lista desplegable y, a continuación, marque la casilla de verificación **Avance del controlador**

   ![Activación mediante árbol](/help/operations/assets/newstep.png)

1. Configure cualquier parámetro adicional en el campo **Argumentos**. Se pueden unir varios argumentos separados por comas. Por ejemplo:

   `enableVersion=true,agentId=publish,includeChildren=true`


   >[!NOTE]
   >
   >Para obtener la lista de parámetros, consulte la sección **Parámetros** a continuación.

1. Pulse **Listo** para guardar el modelo de flujo de trabajo.

**Parámetros**

* `includeChildren` (valor booleano, predeterminado: `false`). El valor `false` significa que solo se publica la ruta de acceso; `true` significa que también se publican las rutas secundarias.
* `replicateAsParticipant` (valor booleano, predeterminado: `false`). Si está configurado como `true`, la replicación está usando la `userid` del principal que realizó el paso del participante.
* `enableVersion` (valor booleano, predeterminado: `false`). Este parámetro determina si se crea una nueva versión tras la replicación.
* `agentId` (valor de cadena, de forma predeterminada significa que solo se utilizan agentes para la publicación). Especifique el agente de destino de forma explícita; por ejemplo, `publish` para el nivel de publicación activa o `preview` para el de vista previa.
* `filters` (valor de cadena, predeterminado significa que todas las rutas están activadas). Los valores disponibles son los siguientes:
   * `onlyActivated`: activar solo las páginas que ya se han activado. Actúa como una forma de reactivación.
   * `onlyModified` activar solo las rutas que ya están activadas y que tienen una fecha de modificación posterior a la fecha de activación.
   * Lo anterior puede ser ORed con una barra vertical &quot;|&quot;. Por ejemplo, `onlyActivated|onlyModified`.

**Registro**

Cuando se inicia el paso del flujo de trabajo de activación de árbol, registra sus parámetros de configuración en el nivel de registro INFO. Cuando se activan las rutas, también se registra una instrucción INFO.

Se registra una instrucción INFO final después de que el paso del flujo de trabajo haya duplicado todas las rutas.

Además, puede aumentar el nivel de registro de los registradores por debajo de `com.day.cq.wcm.workflow.process.impl` a DEBUG/TRACE para obtener aún más información de registro.

Si hay errores, el paso del flujo de trabajo finaliza con un `WorkflowException`, que ajusta la excepción subyacente.

A continuación se muestran ejemplos de registros generados durante un flujo de trabajo de árbol de contenido de publicación de muestra:

```
21.04.2021 19:14:55.566 [cm-p123-e456-aem-author-797aaaf-wkkqt] *INFO* [JobHandler: /var/workflow/instances/server60/2021-04-20/brian-tree-replication-test-2_1:/content/wknd/us/en/adventures] com.day.cq.wcm.workflow.process.impl.treeactivation.TreeActivationWorkflowProcess TreeActivation options: replicateAsParticipant=false(userid=workflow-process-service), agentId=publish, chunkSize=100, filter=, enableVersion=false
```

```
21.04.2021 19:14:58.541 [cm-p123-e456-aem-author-797aaaf-wkkqt] *INFO* [JobHandler: /var/workflow/instances/server60/2021-04-20/brian-tree-replication-test-2_1:/content/wknd/us/en/adventures] com.day.cq.wcm.workflow.process.impl.ChunkedReplicator closing chunkedReplication-VolatileWorkItem_node1_var_workflow_instances_server60_2021-04-20_brian-tree-replication-test-2_1, 17 paths replicated in 2971 ms
```

+++
