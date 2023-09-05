---
title: Participación en flujos de trabajo
description: Los flujos de trabajo incluyen normalmente los pasos que una persona debe llevar a cabo para realizar una actividad en una página o un recurso.
exl-id: 62192da9-0b5b-4997-9c2b-d1aee04b01f9
source-git-commit: 5ad33f0173afd68d8868b088ff5e20fc9f58ad5a
workflow-type: tm+mt
source-wordcount: '1536'
ht-degree: 99%

---

# Participación en flujos de trabajo {#participating-in-workflows}

Los flujos de trabajo incluyen normalmente los pasos que una persona debe llevar a cabo para realizar una actividad en una página o un recurso. El flujo de trabajo selecciona un usuario o grupo para realizar la actividad y asigna un elemento de trabajo a esa persona o grupo. El usuario recibe una notificación y puede realizar las acciones adecuadas:

* [Visualización de notificaciones ](#notifications-of-available-workflow-actions)
* [Finalización de una etapa de participante ](#completing-a-participant-step)
* [Delegación de una etapa de participante ](#delegating-a-participant-step)
* [Realización de una etapa hacia atrás en una etapa de participante ](#performing-step-back-on-a-participant-step)
* [Apertura de un elemento de flujo de trabajo para ver los detalles (y tomar medidas) ](#opening-a-workflow-item-to-view-details-and-take-actions)
* [Visualización de la carga útil del flujo de trabajo (varios recursos) ](#viewing-the-workflow-payload-multiple-resources)

## Notificaciones de acciones de flujo de trabajo disponibles {#notifications-of-available-workflow-actions}

Cuando se le asigna un elemento de trabajo (por ejemplo, **Aprobar contenido**), aparecen varias alertas o notificaciones:

* El indicador de [notificación](/help/sites-cloud/authoring/getting-started/inbox.md) (barra de herramientas) se ha incrementado:

  ![Barra de herramientas de notificaciones](/help/sites-cloud/authoring/assets/workflows-notifications.png)

* El elemento figura en la [Bandeja de entrada](/help/sites-cloud/authoring/getting-started/inbox.md) de notificaciones:

  ![Notificaciones en la bandeja de entrada](/help/sites-cloud/authoring/assets/workflows-inbox.png)

* Cuando utilice el editor de páginas, la barra de estado mostrará lo siguiente:
   * Nombre de los flujos de trabajo que se están aplicando a la página; por ejemplo, Solicitud de activación.
   * Las acciones disponibles para el usuario actual para el paso actual del flujo de trabajo; por ejemplo, Completar, Delegar, Ver detalles.
   * El número de flujos de trabajo a los que está sujeta la página. Puede hacer lo siguiente:
      * utilice las flechas izquierda/derecha para navegar por la información de estado de los distintos flujos de trabajo.
      * haga clic o pulse en el número real para abrir una lista desplegable de todos los flujos de trabajo aplicables y, a continuación, seleccione el flujo de trabajo que desee visualizar en la barra de estado.

  ![Página con varios flujos de trabajo](/help/sites-cloud/authoring/assets/workflows-multiple.png)

  >[!NOTE]
  >
  >La barra de estado solo es visible para los usuarios con privilegios de flujo de trabajo; por ejemplo, los miembros del grupo `workflow-users`.
  >
  >
  >Las acciones se muestran cuando el usuario actual está directamente involucrado en el paso actual del flujo de trabajo.

* Cuando **Cronología** está abierta para el recurso, se muestra el paso del flujo de trabajo. Al hacer clic o pulsar en el titular de alerta, se mostrarán las acciones disponibles:

  ![Flujo de trabajo en la cronología](/help/sites-cloud/authoring/assets/workflows-timeline.png)

### Finalización de una etapa de participante {#completing-a-participant-step}

Puede completar un elemento para permitir que el flujo de trabajo vaya al paso siguiente.

En esta acción puede indicar lo siguiente:

* **Etapa siguiente**: la etapa siguiente que se debe seguir; puede seleccionarla de la lista proporcionada
* **Comentario**: si es necesario

Puede completar un paso de participante desde:

* [La Bandeja de entrada](#completing-a-participant-step-inbox)
* [El Editor de página](#completing-a-participant-step-page-editor)
* [La Cronología](#completing-a-participant-step-timeline)
* Al [abrir un elemento de flujo de trabajo para ver los detalles](#opening-a-workflow-item-to-view-details-and-take-actions).

#### Finalización de una etapa de participante: bandeja de entrada {#completing-a-participant-step-inbox}

Utilice el siguiente procedimiento para completar el elemento de trabajo:

1. Abra la **[Bandeja de entrada AEM](/help/sites-cloud/authoring/getting-started/inbox.md)**.
1. Seleccione el elemento de flujo de trabajo sobre el que desea realizar una acción (pulse o haga clic en la miniatura).
1. Seleccione **Completar** en la barra de herramientas.
1. Se abre el cuadro de diálogo **Completar elemento de trabajo**. Seleccione **Etapa siguiente** del selector desplegable y añada un **Comentario**, si fuera necesario.
1. Utilice **Aceptar** para completar el paso (o **Cancelar** para anular la acción).

#### Finalización de una etapa de participante: editor de la página {#completing-a-participant-step-page-editor}

Utilice el siguiente procedimiento para completar el elemento de trabajo:

1. Abra la [página para editarla](/help/sites-cloud/authoring/fundamentals/organizing-pages.md#opening-a-page-for-editing).
1. Seleccione **Completar** de la barra de estado situada en la parte superior.
1. Se abre el cuadro de diálogo **Completar elemento de trabajo**. Seleccione **Etapa siguiente** del selector desplegable y añada un **Comentario**, si fuera necesario.
1. Utilice **Aceptar** para completar el paso (o **Cancelar** para anular la acción).

#### Finalización de una etapa de participante: cronología {#completing-a-participant-step-timeline}

También puede utilizar la cronología para completar y avanzar un paso:

1. Seleccione la página necesaria y abra **Cronología** (o abra **Cronología** y seleccione la página).

   ![Finalización de un paso](/help/sites-cloud/authoring/assets/workflows-timeline-completing.png)

1. Pulse o haga clic en el titular de la alerta para mostrar las acciones disponibles. Seleccione **Avanzar**:

   ![Avance en el paso](/help/sites-cloud/authoring/assets/workflows-timeline-advance.png)

1. Según el flujo de trabajo, puede seleccionar la siguiente etapa:

   ![Selección del paso siguiente](/help/sites-cloud/authoring/assets/workflows-next-step.png)

1. Seleccione **Asignar** para confirmar la acción.

### Delegación de una etapa de participante  {#delegating-a-participant-step}

Si se le ha asignado un paso, pero por cualquier motivo no puede realizar ninguna acción, puede delegar el paso a otro usuario o grupo.

Los usuarios que están disponibles para la delegación dependen de quién haya sido asignado el elemento de trabajo:

* Si el elemento de trabajo se asignó a un grupo, los miembros del grupo están disponibles.
* Si el elemento de trabajo se ha asignado a un grupo y luego se ha delegado a un usuario, los miembros del grupo y el grupo están disponibles.
* Si el elemento de trabajo se asignó a un único usuario, el elemento de trabajo no se puede delegar.

En esta acción puede indicar lo siguiente:

* **Usuario**: el usuario al que desea delegar; puede seleccionar de una lista proporcionada
* **Comentario**: si es necesario

Puede delegar una etapa de participante desde:

* [La Bandeja de entrada](#delegating-a-participant-step-inbox)
* [El Editor de página](#delegating-a-participant-step-page-editor)
* [La Cronología](#delegating-a-participant-step-timeline)
* Al [abrir un elemento de flujo de trabajo para ver los detalles](#opening-a-workflow-item-to-view-details-and-take-actions).

#### Delegación de una etapa de participante: bandeja de entrada {#delegating-a-participant-step-inbox}

Utilice el siguiente procedimiento para delegar un elemento de trabajo:

1. Abra la **[Bandeja de entrada AEM](/help/sites-cloud/authoring/getting-started/inbox.md)**.
1. Seleccione el elemento de flujo de trabajo sobre el que desea realizar una acción (pulse o haga clic en la miniatura).
1. Seleccione **Delegar** en la barra de herramientas.
1. Se abrirá el cuadro de diálogo. Especifique el **Usuario** del selector desplegable (también puede ser un grupo) y añada un **Comentario** si fuera necesario.
1. Utilice **Aceptar** para completar el paso (o **Cancelar** para anular la acción).

#### Delegación de una etapa de participante: editor de páginas {#delegating-a-participant-step-page-editor}

Utilice el siguiente procedimiento para delegar un elemento de trabajo:

1. Abra la [página para editarla](/help/sites-cloud/authoring/fundamentals/organizing-pages.md#opening-a-page-for-editing).
1. Seleccione **Delegar** de la barra de estado situada en la parte superior.
1. Se abrirá el cuadro de diálogo. Especifique el **Usuario** del selector desplegable (también puede ser un grupo) y añada un **Comentario** si fuera necesario.
1. Utilice **Aceptar** para completar el paso (o **Cancelar** para anular la acción).

#### Delegación de una etapa de participante: cronología {#delegating-a-participant-step-timeline}

También puede utilizar la cronología para delegar o asignar un paso:

1. Seleccione la página necesaria y abra **Cronología** (o abra **Cronología** y seleccione la página).
1. Pulse o haga clic en el titular de la alerta para mostrar las acciones disponibles. Seleccionar **Cambiar asignación**:

   ![Delegar paso](/help/sites-cloud/authoring/assets/workflows-delegate.png)

1. Especifique un nuevo usuario para la asignación:

   ![Cambiar asignación](/help/sites-cloud/authoring/assets/workflows-assignee.png)

1. Seleccione **Asignar** para confirmar la acción.

### Realización de un paso hacia atrás durante el paso de participante {#performing-step-back-on-a-participant-step}

Si descubre que un paso o una serie de pasos debe repetirse, puede retroceder. Esto permite seleccionar una etapa, que se produjo anteriormente en el flujo de trabajo, para volver a procesarla. El flujo de trabajo vuelve al paso especificado y continúa desde ahí.

En esta acción puede indicar lo siguiente:

* **Paso anterior**: el paso al que se va a devolver; puede seleccionar de una lista proporcionada
* **Comentario**: si es necesario

Puede volver a un paso anterior en un paso de participante desde:

* [La Bandeja de entrada](#performing-step-back-on-a-participant-step-inbox)
* [El Editor de página](#performing-step-back-on-a-participant-step-page-editor)
* [La Cronología](#performing-step-back-on-a-participant-step-timeline)
* Al [abrir un elemento de flujo de trabajo para ver los detalles](#opening-a-workflow-item-to-view-details-and-take-actions).

#### Retroceder en un paso de participante: bandeja de entrada {#performing-step-back-on-a-participant-step-inbox}

Utilice el siguiente procedimiento para retroceder:

1. Abra la **[Bandeja de entrada AEM](/help/sites-cloud/authoring/getting-started/inbox.md)**.
1. Seleccione el elemento de flujo de trabajo sobre el que desea realizar una acción (pulse o haga clic en la miniatura).
1. Seleccione **Retroceder** para abrir el cuadro de diálogo. 
1. Especifique un valor en **Etapa anterior** y añada un comentario en el campo **Comentario**, si fuera necesario.
1. Utilice **Aceptar** para completar el paso (o **Cancelar** para anular la acción).

#### Retroceder en un paso de participante: editor de la página {#performing-step-back-on-a-participant-step-page-editor}

Utilice el siguiente procedimiento para retroceder:

1. Abra la [página para editarla](/help/sites-cloud/authoring/fundamentals/organizing-pages.md#opening-a-page-for-editing).
1. Seleccione **Retroceder** de la barra de estado situada en la parte superior.
1. Especifique un valor en **Etapa anterior** y añada un comentario en el campo **Comentario**, si fuera necesario.
1. Utilice **Aceptar** para completar el paso (o **Cancelar** para anular la acción).

#### Retroceder en un paso de participante: cronología {#performing-step-back-on-a-participant-step-timeline}

También puede utilizar la cronología para retroceder a un paso anterior:

1. Seleccione la página necesaria y abra **Cronología** (o abra **Cronología** y seleccione la página).
1. Pulse o haga clic en el titular de la alerta para mostrar las acciones disponibles. Seleccione **Restablecer**:

   ![Retroceder un paso](/help/sites-cloud/authoring/assets/workflows-roll-back.png)

1. Especifique la etapa a la que debe restablecerse el flujo de trabajo:

   ![Especificar paso](/help/sites-cloud/authoring/assets/workflows-roll-back-step.png)

1. Seleccione **Restablecer** para confirmar la acción.

### Apertura de un elemento de flujo de trabajo para ver los detalles (y tomar medidas)  {#opening-a-workflow-item-to-view-details-and-take-actions}

Vea los detalles del elemento de trabajo del flujo de trabajo y realice las acciones adecuadas.

Los detalles del flujo de trabajo se muestran en las pestañas, y las acciones adecuadas están disponibles en la barra de herramientas:

* Ficha **ELEMENTO DE TRABAJO:**

  Ficha ![ELEMENTO DE TRABAJO](/help/sites-cloud/authoring/assets/workflows-work-item.png)

* Pestaña **INFORMACIÓN DEL FLUJO DE TRABAJO**:

  ![Pestaña FLUJO DE TRABAJO](/help/sites-cloud/authoring/assets/workflows-workflow-info.png)

  Si se han configurado etapas de flujo de trabajo para el modelo, puede ver el progreso según los siguientes elementos: <!--If [Workflow Stages](/help/sites-developing/workflows.md#workflow-stages) have been configured for the model, you can view the progress according to these:-->

  ![Etapas de flujo de trabajo](/help/sites-cloud/authoring/assets/workflows-workflow-stages.png)

* Pestaña **COMENTARIOS**:

  ![Pestaña COMENTARIOS](/help/sites-cloud/authoring/assets/workflows-comments.png)

Puede abrir los detalles del elemento de trabajo desde las ubicaciones siguientes:

* [La Bandeja de entrada](#performing-step-back-on-a-participant-step-inbox)
* [El Editor de página](#performing-step-back-on-a-participant-step-page-editor)

#### Apertura de los detalles del flujo de trabajo: bandeja de entrada {#opening-workflow-details-inbox}

Para abrir un elemento de flujo de trabajo y ver los detalles:

1. Abra la **[Bandeja de entrada AEM](/help/sites-cloud/authoring/getting-started/inbox.md)**.
1. Seleccione el elemento de flujo de trabajo sobre el que desea realizar una acción (pulse o haga clic en la miniatura).
1. Seleccione **Abrir** para abrir las pestañas de información. 
1. Si fuera necesario, seleccione la acción adecuada, proporcione los detalles necesarios y confirme con **Aceptar** (o **Cancelar**).
1. Utilice las opciones **Guardar** o **Cancelar** para salir.

#### Apertura de los detalles del flujo de trabajo: editor de página {#opening-workflow-details-page-editor}

Para abrir un elemento de flujo de trabajo y ver los detalles:

1. Abra la [página para editarla](/help/sites-cloud/authoring/fundamentals/organizing-pages.md#opening-a-page-for-editing).
1. Seleccione **Ver detalles** de la barra de estado para abrir las pestañas de información. 
1. Si fuera necesario, seleccione la acción adecuada, proporcione los detalles necesarios y confirme con **Aceptar** (o **Cancelar**).
1. Utilice las opciones **Guardar** o **Cancelar** para salir.

### Visualización de la carga útil del flujo de trabajo (varios recursos)  {#viewing-the-workflow-payload-multiple-resources}

Puede ver los detalles de la carga útil asociada con la instancia de flujo de trabajo. Inicialmente, se muestran los recursos del paquete y luego puede explorar en profundidad para mostrar las páginas individuales.

Para ver la carga útil y los recursos de la instancia del flujo de trabajo:

1. Abra la **[Bandeja de entrada AEM](/help/sites-cloud/authoring/getting-started/inbox.md)**.
1. Seleccione el elemento de flujo de trabajo sobre el que desea realizar una acción (pulse o haga clic en la miniatura).
1. Seleccione **Ver carga útil** de la barra de herramientas para abrir el cuadro de diálogo. 
   * Dado que un paquete de flujo de trabajo es simplemente una colección de punteros a rutas dentro del repositorio, puede añadir, quitar o modificar las entradas aquí para ajustar los elementos a los que el paquete de flujo de trabajo hace referencia. Utilice el componente **Definición de medios** para añadir nuevas entradas.
1. Los vínculos se pueden utilizar para abrir las páginas individuales.
