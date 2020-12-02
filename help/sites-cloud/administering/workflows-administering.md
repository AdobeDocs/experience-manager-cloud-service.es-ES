---
title: Administración de instancias de flujo de trabajo
description: Obtenga información sobre cómo administrar instancias de flujo de trabajo
translation-type: tm+mt
source-git-commit: c19079b1be36c4e87962491f263ddf97ab98f831
workflow-type: tm+mt
source-wordcount: '934'
ht-degree: 0%

---


# Administración de instancias de flujo de trabajo {#administering-workflow-instances}

La consola de flujo de trabajo proporciona varias herramientas para administrar instancias de flujo de trabajo a fin de asegurarse de que se ejecutan según lo esperado.

Hay una serie de consolas disponibles para administrar sus flujos de trabajo. Utilice la [navegación global](/help/sites-cloud/authoring/getting-started/basic-handling.md#global-navigation) para abrir el panel **Herramientas** y, a continuación, seleccione **Flujo de trabajo**:

* **Modelos**: Administrar definiciones de flujo de trabajo
* **Instancias**: Vista y administración de instancias de flujo de trabajo en ejecución
* **Lanzadores**: Administrar cómo se deben iniciar los flujos de trabajo
* **Archivo**: Historial de vistas de flujos de trabajo que se completaron correctamente
* **Errores**: Historial de vistas de flujos de trabajo que se completaron con errores
* **Asignación** automática: Configuración de la asignación automática de flujos de trabajo a las plantillas

## Monitoreo del estado de las instancias de flujo de trabajo {#monitoring-the-status-of-workflow-instances}

1. Mediante Navegación, seleccione **Herramientas** y luego **Flujo de trabajo**.
1. Seleccione **Instancias** para mostrar la lista de las instancias de flujo de trabajo que están en curso.

   ![wf-97](/help/sites-cloud/administering/assets/wf-97.png)


## Instancias de flujo de trabajo de búsqueda {#search-workflow-instances}

1. Mediante Navegación, seleccione **Herramientas** y luego **Flujo de trabajo**.
1. Seleccione **Instancias** para mostrar la lista de las instancias de flujo de trabajo que están en curso. En el carril superior, en la esquina izquierda, seleccione **Filtros**. También puede utilizar las pulsaciones de teclas alt+1. Se muestra el siguiente cuadro de diálogo:

   ![wf-99-1](/help/sites-cloud/administering/assets/wf-99-1.png)

1. En el cuadro de diálogo Filtro, seleccione los criterios de búsqueda del flujo de trabajo. Puede realizar búsquedas en función de estas entradas:

   * Ruta de carga útil: Seleccionar una ruta específica
   * Modelo de flujo de trabajo: Seleccionar un modelo de flujo de trabajo
   * Usuario asignado: Seleccionar un usuario asignado de flujo de trabajo
   * Tipo: Tarea, elemento de flujo de trabajo o error de flujo de trabajo
   * Estado de tarea: Activo, Completo o Terminado
   * Dónde estoy: Propietario Y cesionario, solo propietario, solo cesionario
   * Fecha de inicio: Fecha de inicio antes o después de una fecha especificada
   * Fecha final: Fecha de finalización antes o después de una fecha especificada
   * Fecha de vencimiento: Fecha de vencimiento antes o después de una fecha especificada
   * Fecha de actualización: Fecha de actualización antes o después de una fecha especificada

## Suspender, reanudar y finalizar una instancia de flujo de trabajo {#suspending-resuming-and-terminating-a-workflow-instance}

1. Mediante Navegación, seleccione **Herramientas** y luego **Flujo de trabajo**.
1. Seleccione **Instancias** para mostrar la lista de las instancias de flujo de trabajo que están en curso.

   ![wf-96-1](/help/sites-cloud/administering/assets/wf-96-1.png)

1. Seleccione un elemento específico y, a continuación, utilice **Terminar**, **Suspender** o **Reanudar**, según corresponda; se requiere confirmación y/o más detalles:

   ![wf-97-1](/help/sites-cloud/administering/assets/wf-97-1.png)

## Visualización de Flujos de trabajo archivados {#viewing-archived-workflows}

1. Mediante Navegación, seleccione **Herramientas** y luego **Flujo de trabajo**.

1. Seleccione **Archivar** para mostrar la lista de instancias de flujo de trabajo que se completaron correctamente.

   ![wf-98](/help/sites-cloud/administering/assets/wf-98.png)

   >[!NOTE]
   >El estado de anulación se considera una finalización exitosa, ya que se produce como resultado de la acción del usuario; por ejemplo:
   >
   >* uso de la acción **Terminar**
   >* cuando se elimina (forzosamente) una página que está sujeta a un flujo de trabajo, se cierra el flujo de trabajo


1. Seleccione un elemento específico y luego **Abrir historial** para ver más detalles:

   ![wf-99](/help/sites-cloud/administering/assets/wf-99.png)

## Corrección de errores de instancia de flujo de trabajo {#fixing-workflow-instance-failures}

Cuando un flujo de trabajo falla, AEM proporciona la consola **Errores** para permitirle investigar y tomar las medidas adecuadas una vez que se haya manejado la causa original:

* **Detalles**
de errorAbre una ventana para mostrar la variable 
**Mensaje** de error,  **** Pila de  **errores y Pila** de errores.

* **Abrir**
historialMuestra detalles del historial de flujo de trabajo.

* **Reintentar** PasoEjecuta de nuevo la instancia del componente Paso de secuencia de comandos. Utilice el comando Reintentar etapa después de haber corregido la causa del error original. Por ejemplo, vuelva a intentar el paso después de corregir un error en el script que ejecuta el paso de proceso.
* **** FinalizarFinalice el flujo de trabajo si el error ha provocado una situación irreconciliable para el flujo de trabajo. Por ejemplo, el flujo de trabajo puede basarse en condiciones ambientales como la información del repositorio que ya no es válida para la instancia de flujo de trabajo.
* **Terminar y** reintentarSimilar a  **** Terminar, excepto que una nueva instancia de flujo de trabajo se inicia usando la carga útil, el título y la descripción originales.

Para investigar los errores y, a continuación, reanudar o finalizar el flujo de trabajo posteriormente, siga estos pasos:

1. Mediante Navegación, seleccione **Herramientas** y luego **Flujo de trabajo**.

1. Seleccione **Errores** para mostrar la lista de instancias de flujo de trabajo que no se completaron correctamente.
1. Seleccione un elemento específico y, a continuación, la acción adecuada:

   ![wf-47](/help/sites-cloud/administering/assets/wf-47.png)

## Depuración regular de instancias de flujo de trabajo {#regular-purging-of-workflow-instances}

Al minimizar el número de instancias de flujo de trabajo, aumenta el rendimiento del motor de flujos de trabajo, de modo que puede depurar regularmente instancias de flujo de trabajo completadas o en ejecución desde el repositorio.

Configure **Configuración de purga de flujo de trabajo de granito de Adobe** para purgar instancias de flujo de trabajo según su edad y estado. También puede depurar instancias de flujo de trabajo de todos los modelos o de un modelo específico.

También puede crear varias configuraciones del servicio para depurar instancias de flujo de trabajo que cumplan diferentes criterios. Por ejemplo, cree una configuración que purgue las instancias de un modelo de flujo de trabajo concreto cuando se estén ejecutando durante mucho más tiempo del esperado. Cree otra configuración que purgue todos los flujos de trabajo completados después de un determinado número de días para minimizar el tamaño del repositorio.

Para configurar el servicio, puede configurar los archivos de configuración OSGi en [Archivos de configuración OSGi](/help/implementing/deploying/configuring-osgi.md). En la tabla siguiente se describen las propiedades necesarias para cada método.

>[!NOTE]
>Para agregar la configuración al repositorio, el PID de servicio es:
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
     <li>COMPLETADO: Las instancias de flujo de trabajo completadas se purgan.</li>
     <li>EJECUTANDO: Se purgan las instancias de flujo de trabajo en ejecución.</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Modelos que purgar</td>
   <td>scheduledpurge.modelIds</td>
   <td><p>ID de los modelos de flujo de trabajo que se van a purgar. El ID es la ruta al nodo del modelo, por ejemplo:<br /> /conf/global/settings/workflow/models/dam/update_asset/jcr:content/model<br /> No especifique ningún valor para depurar instancias de todos los modelos de flujo de trabajo.</p> <p>Para especificar varios modelos, haga clic en el botón + en la consola web. </p> </td>
  </tr>
  <tr>
   <td>Edad del flujo de trabajo</td>
   <td>scheduledpurge.daysold</td>
   <td>La antigüedad de las instancias de flujo de trabajo que se van a purgar, en días.</td>
  </tr>
 </tbody>
</table>

## Configuración del tamaño máximo de la bandeja de entrada {#setting-the-maximum-size-of-the-inbox}

Puede configurar el tamaño máximo de la bandeja de entrada configurando el **Servicio de flujo de trabajo de granito de Adobe**; consulte [agregar una configuración OSGi al repositorio](/help/implementing/deploying/configuring-osgi.md). En la tabla siguiente se describe la propiedad que se configura.

>[!NOTE]
>Para agregar la configuración al repositorio, el PID de servicio es:
>`com.adobe.granite.workflow.core.WorkflowSessionFactory`.

| Nombre de propiedad (consola web) | Nombre de propiedad OSGi |
|---|---|
| Tamaño máximo de Consulta de la bandeja de entrada | granite.workflow.inboxQuerySize |

