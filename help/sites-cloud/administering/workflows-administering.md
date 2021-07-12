---
title: Administración de instancias de flujo de trabajo
description: Obtenga información sobre cómo administrar instancias de flujo de trabajo
feature: Administración
role: Admin
exl-id: d2adb5e8-3f0e-4a3b-b7d0-dbbc5450e45f
source-git-commit: 24a4a43cef9a579f9f2992a41c582f4a6c775bf3
workflow-type: tm+mt
source-wordcount: '935'
ht-degree: 1%

---

# Administración de instancias de flujo de trabajo {#administering-workflow-instances}

La consola de flujo de trabajo proporciona varias herramientas para administrar instancias de flujo de trabajo a fin de garantizar que se ejecuten según lo esperado.

Hay una serie de consolas disponibles para administrar los flujos de trabajo. Utilice la [navegación global](/help/sites-cloud/authoring/getting-started/basic-handling.md#global-navigation) para abrir el panel **Herramientas** y, a continuación, seleccione **Flujo de trabajo**:

* **Modelos**: Administrar definiciones de flujo de trabajo
* **Instancias**: Ver y administrar las instancias de flujo de trabajo en ejecución
* **Lanzadores**: Administrar cómo se van a iniciar los flujos de trabajo
* **Archivo**: Ver el historial de flujos de trabajo que se completaron correctamente
* **Errores**: Ver el historial de flujos de trabajo que se completaron con errores
* **Asignación** automática: Configuración de la asignación automática de flujos de trabajo a plantillas

## Monitorización del estado de las instancias de flujo de trabajo {#monitoring-the-status-of-workflow-instances}

1. Mediante Navegación, seleccione **Herramientas** y luego **Flujo de trabajo**.
1. Seleccione **Instances** para mostrar la lista de instancias de flujo de trabajo en curso.

   ![wf-97](/help/sites-cloud/administering/assets/wf-97.png)


## Buscar instancias de flujo de trabajo {#search-workflow-instances}

1. Mediante Navegación, seleccione **Herramientas** y luego **Flujo de trabajo**.
1. Seleccione **Instances** para mostrar la lista de instancias de flujo de trabajo en curso. En el carril superior, en la esquina izquierda, seleccione **Filters**. Como alternativa, puede utilizar las pulsaciones de teclas alt+1. Se muestra el cuadro de diálogo siguiente:

   ![wf-99-1](/help/sites-cloud/administering/assets/wf-99-1.png)

1. En el cuadro de diálogo Filtro, seleccione los criterios de búsqueda del flujo de trabajo. Puede buscar según estas entradas:

   * Ruta de carga útil: Seleccionar una ruta específica
   * Modelo de flujo de trabajo: Seleccionar un modelo de flujo de trabajo
   * Usuario asignado: Seleccione un usuario asignado del flujo de trabajo
   * Tipo: Tarea, elemento de flujo de trabajo o error de flujo de trabajo
   * Estado de la tarea: Activo, completado o finalizado
   * Donde Estoy: Propietario Y asignado, solo propietario, solo usuario asignado
   * Fecha de inicio: Fecha de inicio antes o después de una fecha especificada
   * Fecha final: Fecha final anterior o posterior a una fecha especificada
   * Fecha de vencimiento: Fecha de vencimiento antes o después de una fecha especificada
   * Fecha de actualización: Fecha actualizada antes o después de una fecha especificada

## Suspender, reanudar y finalizar una instancia de flujo de trabajo {#suspending-resuming-and-terminating-a-workflow-instance}

1. Mediante Navegación, seleccione **Herramientas** y luego **Flujo de trabajo**.
1. Seleccione **Instances** para mostrar la lista de instancias de flujo de trabajo en curso.

   ![wf-96-1](/help/sites-cloud/administering/assets/wf-96-1.png)

1. Seleccione un elemento específico y, a continuación, utilice **Terminar**, **Suspender** o **Reanudar**, según corresponda; confirmación o más detalles:

   ![wf-97-1](/help/sites-cloud/administering/assets/wf-97-1.png)

## Visualización de flujos de trabajo archivados {#viewing-archived-workflows}

1. Mediante Navegación, seleccione **Herramientas** y luego **Flujo de trabajo**.

1. Seleccione **Archive** para mostrar la lista de instancias de flujo de trabajo que se completaron correctamente.

   ![wf-98](/help/sites-cloud/administering/assets/wf-98.png)

   >[!NOTE]
   >El estado de anulación se considera una terminación satisfactoria, ya que ocurre como resultado de la acción del usuario; por ejemplo:
   >
   >* uso de la acción **Terminate**
   >* cuando se elimina una página sujeta a un flujo de trabajo, este se cierra y el flujo de trabajo finaliza


1. Seleccione un elemento específico y luego **Abrir historial** para ver más detalles:

   ![wf-99](/help/sites-cloud/administering/assets/wf-99.png)

## Corrección de errores de instancias de flujo de trabajo {#fixing-workflow-instance-failures}

Cuando falla un flujo de trabajo, AEM proporciona la consola **Fallos** para que pueda investigar y tomar las medidas adecuadas una vez que se haya manejado la causa original:

* **Detalles del**
errorAbre una ventana para mostrar la variable 
**Mensaje** De Error,  **** Paso Y  **Pila De Errores**.

* **Abrir**
historialMuestra detalles del historial del flujo de trabajo.

* **Reintentar** pasoEjecuta de nuevo la instancia del componente Paso de secuencia de comandos. Utilice el comando Paso de reintento después de haber corregido la causa del error original. Por ejemplo, vuelva a intentar el paso después de corregir un error en el script que ejecuta el paso de proceso.
* **** FinalizarFinalice el flujo de trabajo si el error ha causado una situación irreconciliable para el flujo de trabajo. Por ejemplo, el flujo de trabajo puede depender de condiciones ambientales como la información del repositorio que ya no son válidas para la instancia de flujo de trabajo.
* **Terminar y** ReintentarSimilar a  **** Terminar, excepto que una nueva instancia de flujo de trabajo se inicia usando la carga útil, el título y la descripción originales.

Para investigar los errores y luego reanudar o finalizar el flujo de trabajo posteriormente, siga los siguientes pasos:

1. Mediante Navegación, seleccione **Herramientas** y luego **Flujo de trabajo**.

1. Seleccione **Errors** para mostrar la lista de instancias de flujo de trabajo que no se completaron correctamente.
1. Seleccione un elemento específico y luego la acción apropiada:

   ![wf-47](/help/sites-cloud/administering/assets/wf-47.png)

## Depuración regular de instancias de flujo de trabajo {#regular-purging-of-workflow-instances}

Al minimizar el número de instancias de flujo de trabajo, aumenta el rendimiento del motor de flujo de trabajo, por lo que puede depurar con regularidad las instancias de flujo de trabajo completadas o en ejecución desde el repositorio.

Configure la **configuración de purga del flujo de trabajo de Granite de Adobe** para purgar las instancias de flujo de trabajo según su edad y estado. También puede depurar instancias de flujo de trabajo de todos los modelos o de un modelo específico.

También puede crear varias configuraciones del servicio para depurar instancias de flujo de trabajo que cumplan distintos criterios. Por ejemplo, cree una configuración que depure las instancias de un modelo de flujo de trabajo concreto cuando se ejecuten durante mucho más tiempo del esperado. Cree otra configuración que depure todos los flujos de trabajo completados después de un determinado número de días para minimizar el tamaño del repositorio.

Para configurar el servicio, puede configurar los archivos de configuración OSGi ver [archivos de configuración OSGi](/help/implementing/deploying/configuring-osgi.md). En la tabla siguiente se describen las propiedades que necesita para cualquiera de los métodos.

>[!NOTE]
>Para añadir la configuración al repositorio, el PID de servicio es:
>`com.adobe.granite.workflow.purge.Scheduler`
>Dado que el servicio es un servicio de fábrica, el nombre del nodo `sling:OsgiConfig` requiere un sufijo de identificador, por ejemplo:
>`com.adobe.granite.workflow.purge.Scheduler-myidentifier`

<table>
 <tbody>
  <tr>
   <th>Nombre de propiedad (consola web)</th>
   <th>Nombre de propiedad OSGi</th>
   <th>Descripción</th>
  </tr>
  <tr>
   <td>Nombre del trabajo</td>
   <td>scheduledpurge.name</td>
   <td>Un nombre descriptivo para la depuración programada.</td>
  </tr>
  <tr>
   <td>Estado de flujo de trabajo</td>
   <td>scheduledpurge.workflowStatus</td>
   <td><p>Estado de las instancias de flujo de trabajo que se van a purgar. Los siguientes valores son válidos:</p>
    <ul>
     <li>FINALIZADO: Las instancias de flujo de trabajo completadas se depuran.</li>
     <li>EJECUTANDO: La ejecución de instancias de flujo de trabajo se depura.</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Modelos Para Purgar</td>
   <td>scheduledpurge.modelIds</td>
   <td><p>ID de los modelos de flujo de trabajo que se van a depurar. El ID es la ruta al nodo del modelo, por ejemplo:<br /> /conf/global/settings/workflow/models/dam/update_asset/jcr:content/model<br /> No especifique ningún valor para depurar instancias de todos los modelos de flujo de trabajo.</p> <p>Para especificar varios modelos, haga clic en el botón + de la consola web. </p> </td>
  </tr>
  <tr>
   <td>Edad del flujo de trabajo</td>
   <td>scheduledpurge.daysold</td>
   <td>La edad de las instancias de flujo de trabajo que se van a purgar, en días.</td>
  </tr>
 </tbody>
</table>

## Configuración del tamaño máximo de la bandeja de entrada {#setting-the-maximum-size-of-the-inbox}

Puede configurar el tamaño máximo de la bandeja de entrada configurando el **Adobe Granite Workflow Service**, consulte [añadir una configuración OSGi al repositorio](/help/implementing/deploying/configuring-osgi.md). En la tabla siguiente se describe la propiedad que se configura.

>[!NOTE]
>Para añadir la configuración al repositorio, el PID de servicio es:
>`com.adobe.granite.workflow.core.WorkflowSessionFactory`.

| Nombre de propiedad (consola web) | Nombre de propiedad OSGi |
|---|---|
| Tamaño máximo de consulta de la bandeja de entrada | granite.workflow.inboxQuerySize |
