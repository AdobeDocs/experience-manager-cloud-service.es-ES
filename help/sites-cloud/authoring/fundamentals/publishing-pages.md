---
title: Publicar páginas
description: Publicar y cancelar la publicación de páginas con AEM
exl-id: 89f2363c-7922-4ca5-92cb-cbee6a393ee3
source-git-commit: ca849bd76e5ac40bc76cf497619a82b238d898fa
workflow-type: ht
source-wordcount: '1812'
ht-degree: 100%

---

# Publicar páginas {#publishing-pages}

Cuando haya creado y revisado el contenido en el entorno de creación, el objetivo consiste en que [esté disponible en su sitio web público](/help/sites-cloud/authoring/getting-started/concepts.md) (su entorno de publicación).

Esta acción se conoce como publicar una página. Si desea quitar una página del entorno de publicación, la acción es la de cancelar la publicación. Tanto al publicar como al cancelar la publicación, la página permanece disponible en el entorno de creación para realizar cualquier cambio, hasta que decida eliminarla.

Puede publicar una página (o cancelar su publicación) inmediatamente o en un momento posterior predefinido.

>[!NOTE]
>
>La publicación de un fragmento de experiencia básicamente sigue el mismo procedimiento que para publicar una página, aunque desde la consola o el editor de fragmentos de experiencias.

## Terminología {#terminology}

Puede encontrar diferentes términos relacionados con la publicación al trabajar con Adobe Experience Manager (AEM) as a Cloud Service.

* **Publicar o cancelar la publicación**
   * Estos son los términos principales de las acciones que harán que el contenido esté disponible o no para los visitantes en su entorno de publicación.
   * Estos son los términos utilizados en la documentación de AEM.
* **Activar o desactivar**
   * Estos términos son sinónimos de publicar y cancelar la publicación.
   * Estos términos se utilizaban en versiones anteriores de AEM.
* **Replicar o replicación**
   * Son los términos técnicos que describen el movimiento de datos (por ejemplo, contenido de páginas, archivos, códigos o comentarios de usuarios) de un entorno a otro cuando publica una página.
   * Los desarrolladores son quienes, principalmente, utilizan estos términos.

## Publicar páginas {#publishing-pages-1}

En función de su ubicación, puede publicar:

* [Desde el editor de páginas](#publishing-from-the-editor)
* [Desde la consola Sitios](#publishing-from-the-console)

>[!NOTE]
>
>Si no dispone de los privilegios necesarios para publicar en una página concreta:
>
>* Se activará un flujo de trabajo para notificar a la persona adecuada la solicitud de publicación.
>* Este flujo de trabajo puede haber sido personalizado por el equipo de desarrollo.
>* Se mostrará brevemente un mensaje para notificarle que el flujo de trabajo se ha activado.


>[!NOTE]
>
> Para obtener más información, consulte **Tiempo de activación** y **Tiempo de inactividad** en la [pestaña Básico de Propiedades de página](/help/sites-cloud/authoring/fundamentals/page-properties.md#basic)

### Publicar desde el editor {#publishing-from-the-editor}

Si está editando una página, puede publicarla directamente desde el editor.

1. Seleccione el icono **Información de página** para abrir el menú y, a continuación, elija la opción **Publicar página**.

   ![Publicación de una página mediante las opciones de página](/help/sites-cloud/authoring/assets/publishing-page-options.png)

1. En función de si la página tiene referencias que es necesario publicar:

   * La página se publicará directamente si no hay ninguna referencia por publicar.
   * Si la página tiene referencias que es necesario publicar, estas se enumerarán en el asistente **Publicar**, donde puede:
      * Especificar qué recurso/etiqueta/etc. desea publicar junto con la página y, a continuación, utilizar **Publicar** para completar el proceso.
      * Utilizar **Cancelar** para anular la acción.

   ![Publicación de referencias con la página](/help/sites-cloud/authoring/assets/publishing-references.png)

1. Si selecciona **Publicar**, se replicará la página en el entorno de publicación. En el editor de páginas se mostrará un mensaje que confirma la acción de publicación.

   ![Mensaje de información de estado de publicación](/help/sites-cloud/authoring/assets/publishing-info.png)

   Al ver la misma página en la consola, se muestra el estado actualizado de publicación.

   ![Estado de publicación de la página en la vista de columna de la consola Sitios](/help/sites-cloud/authoring/assets/publishing-status-console-column.png)

>[!NOTE]
>
>La publicación desde el editor no es profunda; es decir, solo se publica la página o páginas seleccionadas y no las páginas secundarias.

>[!NOTE]
>
>No se pueden publicar páginas a las que se accede mediante [alias](/help/sites-cloud/authoring/fundamentals/page-properties.md#advanced) en el editor. Las opciones de publicación del editor solo están disponibles para las páginas a las que se accede mediante sus rutas reales.

### Publicar desde la consola {#publishing-from-the-console}

En la consola Sitios hay dos opciones para la publicación:

* [Publicación rápida ](#quick-publish)
* [Administrar publicación    ](#manage-publication)

#### Publicación rápida  {#quick-publish}

**Publicación rápida** es para casos sencillos y publica las páginas seleccionadas inmediatamente, sin más interacción. Por este motivo, cualquier referencia no publicada se publica también automáticamente.

Para publicar una página con Publicación rápida:

1. Seleccione la página o páginas en la consola Sitios y haga clic en el botón **Publicación rápida**.

   ![Selección de páginas para publicación](/help/sites-cloud/authoring/assets/publishing-select-pages.png)

1. En el cuadro de diálogo Publicación rápida, confirme la publicación haciendo clic en **Publicar** o cancele la acción haciendo clic en **Cancelar**. Recuerde que cualquier referencia sin publicar se publicará también automáticamente.

   ![Confirmación de publicación rápida](/help/sites-cloud/authoring/assets/publishing-quick-publish.png)

1. Cuando la página esté publicada, se mostrará un aviso de confirmación.

>[!NOTE]
>
>La Publicación rápida no es profunda; es decir, solo se publica la página o páginas seleccionadas, y no las páginas secundarias.

#### Administrar publicación     {#manage-publication}

**Administrar publicación** ofrece más opciones que **Publicación rápida**, pues permite incluir páginas secundarias, personalizar las referencias e iniciar cualquier flujo de trabajo aplicable, además de poder publicar en un momento posterior.

Para publicar o cancelar la publicación de una página con Administrar publicación:

1. Seleccione la página o páginas en la consola Sitios y haga clic en el botón **Administrar publicación**.

   ![Selección de páginas para publicación](/help/sites-cloud/authoring/assets/publishing-select-pages.png)

1. Se inicia el asistente **Administrar publicación**. El primer paso, **Opciones**, le permite:

   * **Acción**

      Elija si publica o cancela la publicación de las páginas seleccionadas.

   * **Programación**

      Elija si la acción se realizará ahora o en una fecha posterior.

      Posponer la publicación inicia un flujo de trabajo que publicará la página o páginas seleccionadas en el momento especificado. Por su parte, cancelar la publicación inicia un flujo de trabajo para anular la publicación de la página o páginas seleccionadas en un momento especificado.

      >[!NOTE]
      >
      >Si desea cancelar una acción de publicación/cancelación de la publicación posteriormente, vaya a la [consola Flujo de trabajo](/help/sites-cloud/administering/workflows-administering.md#suspending-resuming-and-terminating-a-workflow-instance) para finalizar el flujo de trabajo correspondiente.

   ![Administrar opciones de publicación](/help/sites-cloud/authoring/assets/publishing-manage-publication-options.png)

1. Haga clic en **Siguiente** para continuar.

1. En el siguiente paso del asistente de Administrar publicación, **Ámbito**, puede definir el ámbito de la publicación o la cancelación de la publicación, por ejemplo, si se incluyen páginas secundarias o referencias.

   ![Administrar ámbito de publicación](/help/sites-cloud/authoring/assets/publishing-manage-publication-scope.png)

   **Añadir contenido**

   Puede utilizar el botón **Añadir contenido** para añadir páginas adicionales a la lista de páginas que se publicarán, en caso de que olvidara seleccionar alguna antes de iniciar el asistente de Administrar publicación.

   Al hacer clic en el botón **Añadir contenido**, se inicia el [explorador de rutas](/help/sites-cloud/authoring/fundamentals/environment-tools.md#path-browser) para que pueda seleccionar contenido.

   Seleccione las páginas necesarias y, a continuación, haga clic en **Seleccionar** para añadir el contenido al asistente, o **Cancelar** para cancelar la selección y volver al asistente.

   **Eliminar la selección**

   En el asistente, puede seleccionar un elemento de la lista para eliminarlo de la selección.

   ![Administrar páginas de selección de publicación](/help/sites-cloud/authoring/assets/publishing-manage-publication-select.png)

   **Referencias publicadas**

   Puede ver y modificar las referencias que se van a publicar o dejar de publicar para una página: haga clic en la página y, a continuación, haga clic en el botón **Referencias publicadas**.

   ![Administrar opciones de publicación](/help/sites-cloud/authoring/assets/publishing-manage-publication-references.png)

   El cuadro de diálogo **Referencias publicadas** muestra las referencias para el contenido seleccionado. De forma predeterminada, todas se seleccionan y se publican o dejan de publicar, pero puede anular la marca de selección de las que no desee, de modo que no se incluyan en la acción.

   Haga clic en **Listo** para guardar los cambios o en **Cancelar** para cancelar la selección y volver al asistente.

   En el asistente, la columna **Referencias** se actualizará para reflejar su selección de referencias a publicar o dejar de publicar.

   ![Administrar páginas de selección de publicación](/help/sites-cloud/authoring/assets/publishing-manage-publication-select.png)

   **Incluir elementos secundarios**

   >[!NOTE]
   >
   >Consulte [Publicación y cancelación de publicación de un árbol](#publishing-and-unpublishing-a-tree)

   Al hacer clic en **Incluir elementos secundarios** se abre un cuadro de diálogo que le permite lo siguiente:

   * **Incluir elementos secundarios**
   * **Incluir solo los elementos secundarios inmediatos**
   * **Incluir solo las páginas modificadas**
   * **Incluir solo las páginas ya publicadas**

   Active las opciones necesarias y confirme con **Aceptar** para añadir las páginas secundarias a la lista de páginas que se van a publicar o dejar de publicar, según las opciones de selección. Haga clic en **Cancelar** para cancelar la selección y volver al asistente.

   ![Administrar publicación, incluidos los elementos secundarios](/help/sites-cloud/authoring/assets/publishing-include-children.png)

1. Haga clic en **Publicar** para completar la acción.

   En la consola Sitios, un mensaje de notificación confirmará la publicación.

1. Si las páginas publicadas están asociadas a flujos de trabajo, estos se pueden mostrar en un último paso, **Flujos de trabajo**, del asistente de publicación.

   ![Administrar páginas de selección de publicación](/help/sites-cloud/authoring/assets/publishing-manage-publication-workflow.png)

   >[!NOTE]
   >
   >El paso **Flujos de trabajo** se muestra o no en función de los derechos del usuario. Para obtener más información, consulte la nota anterior en esta página respecto a los privilegios de publicación, así como Administración del acceso a los flujos de trabajo y [Aplicación de flujos de trabajo a páginas](/help/sites-cloud/authoring/workflows/applying.md).

   Los recursos se agrupan por los flujos de trabajo activados y cada uno ofrece opciones para:

   * Definir el título del flujo de trabajo.
   * Mantener el paquete del flujo de trabajo, siempre que este sea compatible con varios recursos.
   * Definir un título para el paquete de flujos de trabajo si se eligió la opción para mantener dicho paquete.

1. Haga clic en **Publicar** o **Publicar más tarde** para completar la publicación.

## Cancelar la publicación de páginas {#unpublishing-pages}

Si se cancela la publicación de una página, se eliminará del entorno de publicación (o [previsualización](/help/sites-cloud/authoring/fundamentals/previewing-content.md)) y ya no estará disponible para los lectores.

De [forma similar a la publicación](#publishing-pages), se puede cancelar la publicación de una o varias páginas del destino deseado:

* [Desde el editor de páginas](#unpublishing-from-the-editor)
* [Desde la consola Sitios](#unpublishing-from-the-console)

### Cancelación de la publicación desde el editor     {#unpublishing-from-the-editor}

Si desea cancelar la publicación de una página que está editando, seleccione **Cancelar publicación de página** en el menú **Información de página**, de un modo similar a como haría para [publicar la página](#publishing-from-the-editor).

>[!NOTE]
>
>No se puede cancelar la publicación en el editor de las páginas a las que se accede mediante [alias](/help/sites-cloud/authoring/fundamentals/page-properties.md#advanced). Las opciones de publicación del editor solo están disponibles para las páginas a las que se accede mediante sus rutas reales.

### Cancelación de la publicación desde la consola     {#unpublishing-from-the-console}

Al igual que [utiliza la opción Administrar publicación para publicar](#manage-publication), puede usarla para cancelar la publicación.

1. Seleccione la página o páginas en la consola Sitios y haga clic en el botón **Administrar publicación**.
1. Se inicia el asistente **Administrar publicación**. En el primer paso, **Opciones**, seleccione **Cancelar publicación** en lugar de la opción predeterminada **Publicar**.

   ![Cancelación de la publicación: opciones](/help/sites-cloud/authoring/assets/publishing-unpublish.png)

   Igual que posponer la publicación inicia un flujo de trabajo para publicar esta versión de la página en el momento especificado, desactivar más tarde inicia un flujo de trabajo para cancelar la publicación de la página o páginas seleccionadas en un momento concreto.

   >[!NOTE]
   >
   >Si desea cancelar una acción de publicación/cancelación de la publicación posteriormente, vaya a la [consola Flujo de trabajo](/help/sites-cloud/administering/workflows-administering.md#suspending-resuming-and-terminating-a-workflow-instance) para finalizar el flujo de trabajo correspondiente.

   >[!NOTE]
   >Si tiene una [Vista previa](/help/sites-cloud/authoring/fundamentals/previewing-content.md) del entorno, puede seleccionar **Destino** durante Administrar publicación.

1. Para completar la cancelación de la publicación, complete el asistente como haría para [publicar la página](#manage-publication).

   ![Cancelación de la publicación: ámbito](/help/sites-cloud/authoring/assets/publishing-unpublish-scope.png)

## Publicar y cancelar la publicación de un árbol {#publishing-and-unpublishing-a-tree}

Cuando haya introducido o actualizado una cantidad considerable de páginas de contenido (todas ellas residentes dentro de la misma página raíz), puede ser más fácil publicar el árbol entero con una sola acción.

Para hacerlo, puede utilizar la opción [Administrar publicación](#manage-publication) de la consola Sitios.

1. En la consola Sitios, seleccione la página raíz de árbol que desea publicar o dejar de publicar y seleccione **Administrar publicación**.
1. Se inicia el asistente **Administrar publicación**. Elija si desea publicar o cancelar la publicación, y cuándo debe producirse la acción, y seleccione **Siguiente** para continuar.
1. En el paso **Ámbito**, elija la página raíz y seleccione **Incluir elementos secundarios**.

   ![Administrar páginas de selección de publicación](/help/sites-cloud/authoring/assets/publishing-manage-publication-select.png)

1. En el cuadro de diálogo **Incluir tareas secundarias**:

   * seleccione **Incluir tareas secundarias**
   * deseleccione **Incluir solo las tareas secundarias inmediatas**
   * deseleccione **Incluir solo las páginas ya publicadas**
   * configure **Incluir solo páginas modificadas** según se requiera

   Estas opciones están seleccionadas de forma predeterminada, por lo que debe acordarse de configurar su selección. Confirme la selección con **OK** para agregar el contenido a la publicación/cancelación de publicación.

   ![Inclusión de tareas secundarias para la publicación de árboles](/help/sites-cloud/authoring/assets/publishing-include-children-tree.png)

1. En el asistente **Administrar publicación** puede personalizar aún más la selección añadiendo páginas adicionales o eliminando las seleccionadas.

   Recuerde que también puede revisar las referencias que se publican mediante la opción **Referencias publicadas**.

1. [Continúe con el asistente Administrar publicación](#manage-publication) para completar la publicación o la cancelación de publicación del árbol.

## Determinar el estado de publicación {#determining-publication-status}

Puede determinar el estado de la publicación de una página:

* En la [información general de recursos de la consola Sitios](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources)

   ![Estado de publicación en la vista de tarjeta](/help/sites-cloud/authoring/assets/publishing-status-console-card.png)

   El estado de publicación se indica en las vistas de [tarjeta](/help/sites-cloud/authoring/getting-started/basic-handling.md#card-view), [columna](/help/sites-cloud/authoring/getting-started/basic-handling.md#column-view) y [lista](/help/sites-cloud/authoring/getting-started/basic-handling.md#list-view) de la consola Sitios.

* En la [cronología](/help/sites-cloud/authoring/getting-started/basic-handling.md#timeline)

   ![Estado de publicación en la vista de cronología](/help/sites-cloud/authoring/assets/publishing-status-timeline.png)

* En el [menú Información de página](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-information) cuando se edita una página.

   ![Estado de publicación en el menú Información de página](/help/sites-cloud/authoring/assets/publishing-status-page-information.png)
