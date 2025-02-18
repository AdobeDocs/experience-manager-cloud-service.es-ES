---
title: Publicar páginas
description: Obtenga información sobre cómo publicar y cancelar la publicación de páginas mediante varios mecanismos en AEM.
exl-id: 89f2363c-7922-4ca5-92cb-cbee6a393ee3
solution: Experience Manager Sites
feature: Authoring
role: User
source-git-commit: c738a123eccbb9b8c011f75ac60d79aba7a2a2d8
workflow-type: tm+mt
source-wordcount: '1926'
ht-degree: 75%

---

# Publicar páginas {#publishing-pages}

Cuando haya creado y revisado el contenido en el entorno de creación, el objetivo consiste en [que esté disponible en su sitio web público](/help/sites-cloud/authoring/author-publish.md) (su entorno de publicación).

Es lo que se denomina publicar una página. Quitar una página del entorno de publicación, se denomina cancelar la publicación. Al publicar y cancelar la publicación, la página permanece disponible en el entorno de creación para realizar más cambios hasta que la elimine.

Puede publicar una página (o cancelar su publicación) inmediatamente o en un momento posterior predefinido.

>[!NOTE]
>
>La publicación de un [fragmento de experiencia](/help/sites-cloud/authoring/fragments/experience-fragments.md) básicamente sigue el mismo procedimiento que para publicar una página, aunque desde la consola o el editor de fragmentos de experiencias.

## Terminología {#terminology}

Puede encontrar diferentes términos relacionados con la publicación al trabajar con Adobe Experience Manager (AEM) as a Cloud Service.

* **Publicar o cancelar la publicación**
   * Estos son los términos principales de las acciones que hacen que el contenido esté disponible o no para los entornos de publicación o vista previa.
   * Estos son los términos utilizados en la documentación de AEM.
* **Activar o desactivar**
   * Estos términos son sinónimos de publicar y cancelar la publicación.
   * Estos términos se utilizaban en versiones anteriores de AEM.
* **Replicar o replicación**
   * Son los términos técnicos que describen el movimiento de datos (por ejemplo, contenido de página, archivos, código, comentarios del usuario) de un servicio a otro cuando publica una página (por ejemplo, de autor a vista previa).
   * Los desarrolladores son quienes, principalmente, utilizan estos términos.

## Publicar páginas {#publishing-pages-1}

En función de su ubicación, puede publicar lo siguiente:

* [Desde el editor de páginas](#publishing-from-the-page-editor)
* [Desde el ](#publishing-from-the-sites-console)
* [Desde el editor universal](/help/sites-cloud/authoring/universal-editor/publishing.md)

>[!NOTE]
>
>Si no dispone de los privilegios necesarios para publicar una página específica:
>
>* Se activa un flujo de trabajo para notificar a la persona adecuada su solicitud de publicación.
>* Este flujo de trabajo puede haber sido personalizado por el equipo de desarrollo.
>* Se muestra brevemente un mensaje para notificarle que el flujo de trabajo se ha activado.

>[!NOTE]
>
>Si desea conservar el orden de las páginas, debe usar [Administrar publicación](#manage-publication) para publicar la página principal junto con las páginas secundarias en una sola acción.
>
>No se garantiza el orden de las páginas:
>
>* si solo se seleccionan páginas secundarias para la publicación (ya que la información de pedido se mantiene en la página principal)
>* si las páginas principales y secundarias se publican en acciones independientes

### Publicar desde el editor de páginas {#publishing-from-the-page-editor}

Si está editando una página en el [editor de páginas](/help/sites-cloud/authoring/page-editor/introduction.md), puede publicarla directamente desde el editor.

1. Seleccione el icono **Información de página** para abrir el menú y, a continuación, elija la opción **Publicar página**.

   ![Publicación de una página mediante las opciones de página](/help/sites-cloud/authoring/assets/publishing-page-options.png)

1. En función de si la página tiene referencias que es necesario publicar:

   * La página se publica directamente si no hay ninguna referencia por publicar.
   * Si la página tiene referencias que es necesario publicar, se enumeran en el asistente **Publicar**, donde puede:
      * Especifique cuál de los recursos, o etiquetas, etc., desea publicar junto con la página y, a continuación, utilice **Publicar** para completar el proceso.
      * Utilizar **Cancelar** para anular la acción.

   ![Publicación de referencias con la página](/help/sites-cloud/authoring/assets/publishing-references.png)

1. Si selecciona **Publicar**, se replicará la página en el entorno de publicación. En el editor de páginas se muestra un mensaje que confirma la acción de publicación.

   ![Mensaje de información de estado de publicación](/help/sites-cloud/authoring/assets/publishing-info.png)

   Al ver la misma página en la consola, se muestra el estado actualizado de publicación.

   ![Estado de publicación de la página en la vista de columna de la consola Sitios](/help/sites-cloud/authoring/assets/publishing-status-console-column.png)

>[!NOTE]
>
>La publicación desde el editor de páginas es superficial; es decir, solo se publica la página o páginas seleccionadas y no las páginas secundarias.

>[!NOTE]
>
>No se pueden publicar las páginas a las que se tiene acceso mediante [alias](/help/sites-cloud/authoring/sites-console/page-properties.md#advanced) en el editor. Las opciones de publicación del editor solo están disponibles para las páginas a las que se accede mediante sus rutas reales.

### Publicar desde la consola del sitio {#publishing-from-the-sites-console}

En la consola **Sites** hay dos opciones para la publicación:

* [Publicación rápida ](#quick-publish)
* [Administrar publicación    ](#manage-publication)

#### Publicación rápida  {#quick-publish}

**Publicación rápida** es para casos sencillos y publica las páginas seleccionadas inmediatamente, sin más interacción. Debido a esto, cualquier referencia no publicada también se publicará automáticamente.

Para publicar una página con Publicación rápida:

1. Seleccione la página o páginas en la consola Sitios y haga clic en el botón **Publicación rápida**.

   ![Selección de páginas para publicación](/help/sites-cloud/authoring/assets/publishing-select-pages.png)

1. En el cuadro de diálogo Publicación rápida, confirme la publicación haciendo clic en **Publicar** o cancele la acción haciendo clic en **Cancelar**. Recuerde que cualquier referencia sin publicar se publicará también automáticamente.

   ![Confirmación de publicación rápida](/help/sites-cloud/authoring/assets/publishing-quick-publish.png)

1. Cuando se publica la página, se muestra una alerta que confirma la publicación.

>[!NOTE]
>
>La Publicación rápida es una publicación superficial, es decir, solo se publica la página o páginas seleccionadas y no las páginas secundarias.

#### Administrar publicación     {#manage-publication}

**Administrar publicación** ofrece más opciones que **Publicación rápida**, ya que permite incluir páginas secundarias, personalizar las referencias, publicar en un servicio de vista previa (si está disponible) e iniciar cualquier flujo de trabajo aplicable, además de poder publicar en un momento posterior.

Para publicar o cancelar la publicación de una página con Administrar publicación:

1. Seleccione la página o páginas en la consola Sitios y haga clic en el botón **Administrar publicación**.

   ![Selección de páginas para publicación](/help/sites-cloud/authoring/assets/publishing-select-pages.png)

1. Se inicia el asistente **Administrar publicación**. El primer paso, **Opciones**, le permite:

   * **Acción**

     Elija si publica o cancela la publicación de las páginas seleccionadas.

   * **Destino**

     Seleccione si desea publicar en el servicio de publicación (predeterminado) o en el servicio de vista previa. Solo está disponible si tiene configurado un servicio de [vista previa.](/help/sites-cloud/authoring/sites-console/previewing-content.md)

   * **Programación**

     Elija realizar esa acción ahora o en una fecha posterior.

     Posponer la publicación inicia un flujo de trabajo para publicar la página o páginas seleccionadas en el momento especificado. Por el contrario, cancelar la publicación más adelante inicia un flujo de trabajo para cancelar la publicación de la página o páginas seleccionadas en un momento específico.

     >[!NOTE]
     >
     >Si desea cancelar una acción de publicación/cancelación de la publicación posteriormente, vaya a la [consola Flujo de trabajo](/help/sites-cloud/administering/workflows-administering.md#suspending-resuming-and-terminating-a-workflow-instance) para finalizar el flujo de trabajo correspondiente.

     >[!NOTE]
     >
     >Programar contenido para la publicación no es lo mismo que [**Tiempo de activación** y **Tiempo de inactividad** disponibles en las propiedades de la página,](/help/sites-cloud/authoring/sites-console/page-properties.md#basic), pero se pueden usar en circunstancias similares.

   ![Administrar opciones de publicación](/help/sites-cloud/authoring/assets/publishing-manage-publication-options.png)

1. Haga clic en **Siguiente** para continuar.

1. En el siguiente paso del asistente de Administrar publicación, **Ámbito**, puede definir el ámbito de la publicación o la cancelación de la publicación, por ejemplo, si se incluyen páginas secundarias o referencias.

   ![Administrar ámbito de publicación](/help/sites-cloud/authoring/assets/publishing-manage-publication-scope.png)

   **Añadir contenido**

   Puede utilizar el botón **Añadir contenido** para añadir páginas adicionales a la lista de páginas que se publicarán, en caso de que olvidara seleccionar alguna antes de iniciar el asistente de Administrar publicación.

   Al hacer clic en el botón **Añadir contenido**, se inicia el [explorador de rutas](/help/sites-cloud/authoring/path-selection.md) para que pueda seleccionar contenido.

   Seleccione las páginas necesarias y, a continuación, haga clic en **Seleccionar** para añadir el contenido al asistente, o **Cancelar** para cancelar la selección y volver al asistente.

   **Eliminar la selección**

   En el asistente, puede seleccionar un elemento de la lista para eliminarlo de la selección.

   ![Administrar páginas de selección de publicación](/help/sites-cloud/authoring/assets/publishing-manage-publication-select.png)

   **Referencias publicadas**

   Puede ver y modificar las referencias que se van a publicar o dejar de publicar para una página: haga clic en la página y, a continuación, haga clic en el botón **Referencias publicadas**.

   ![Administrar opciones de publicación](/help/sites-cloud/authoring/assets/publishing-manage-publication-references.png)

   El cuadro de diálogo **Referencias publicadas** muestra las referencias para el contenido seleccionado. De forma predeterminada, todas se seleccionan y se publican o dejan de publicar, pero puede anular la marca de selección de las que no desee, de modo que no se incluyan en la acción.

   Haga clic en **Listo** para guardar los cambios o en **Cancelar** para cancelar la selección y volver al asistente.

   En el asistente, la columna **Referencias** se actualiza para reflejar su selección de referencias a publicar o dejar de publicar.

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
   >El paso **Flujos de trabajo** se muestra en función de los derechos que tenga o no su usuario o usuaria. Para obtener más información, consulte la nota anterior en esta página respecto a los privilegios de publicación, así como la administración del acceso a los flujos de trabajo y [aplicación de flujos de trabajo a páginas](/help/sites-cloud/authoring/workflows/applying.md).

   Los recursos se agrupan por los flujos de trabajo activados y a cada uno se le ofrecen opciones para:

   * Definir el título del flujo de trabajo.
   * Mantener el paquete del flujo de trabajo, siempre que este sea compatible con varios recursos.
   * Definir un título para el paquete de flujos de trabajo si se eligió la opción para mantener dicho paquete.

1. Haga clic en **Publicar** o **Publicar más tarde** para completar la publicación.



## Cancelar la publicación de páginas {#unpublishing-pages}

Si se cancela la publicación de una página, se eliminará del entorno de publicación (o [previsualización](/help/sites-cloud/authoring/sites-console/previewing-content.md)) y ya no estará disponible para los lectores.

De [forma similar a la publicación](#publishing-pages), se puede cancelar la publicación de una o varias páginas del destino deseado:

* [Desde el editor de páginas](#unpublishing-from-the-editor)
* [Desde la consola Sitios](#unpublishing-from-the-console)

### Cancelación de la publicación desde el editor     {#unpublishing-from-the-editor}

Al editar una página, si desea cancelar la publicación de esa página, seleccione **Cancelar la publicación de la página** en el menú **Información de la página**, de forma parecida a como lo haría [publicar la página](#publishing-from-the-editor).

>[!NOTE]
>
>No se puede cancelar la publicación de las páginas a las que se accede mediante [alias](/help/sites-cloud/authoring/sites-console/page-properties.md#advanced) en el editor. Las opciones de publicación del editor solo están disponibles para las páginas a las que se accede mediante sus rutas reales.

### Cancelación de la publicación desde la consola     {#unpublishing-from-the-console}

Al igual que [utiliza la opción Administrar publicación para publicar](#manage-publication), puede usarla para cancelar la publicación.

1. Seleccione la página o páginas en la consola Sitios y haga clic en el botón **Administrar publicación**.
1. Se inicia el asistente **Administrar publicación**. En el primer paso, **Opciones**, seleccione **Cancelar publicación** en lugar de la opción predeterminada **Publicar**.

   ![Cancelación de la publicación: opciones](/help/sites-cloud/authoring/assets/publishing-unpublish.png)

   Igual que posponer la publicación inicia un flujo de trabajo para publicar esta versión de la página en el momento especificado, desactivar más tarde inicia un flujo de trabajo para cancelar la publicación de la página o páginas seleccionadas en un momento concreto.

   >[!NOTE]
   >
   >Si desea cancelar una acción de publicación/cancelación de la publicación posteriormente, vaya a la [consola Flujo de trabajo](/help/sites-cloud/administering/workflows-administering.md#suspending-resuming-and-terminating-a-workflow-instance) para finalizar el flujo de trabajo correspondiente.

   >[!NOTE]
   >Si tiene una [Vista previa](/help/sites-cloud/authoring/sites-console/previewing-content.md) del entorno, puede seleccionar **Destino** durante Administrar publicación.

1. Para completar la cancelación de la publicación, complete el asistente como haría para [publicar la página](#manage-publication).

   ![Cancelación de la publicación: ámbito](/help/sites-cloud/authoring/assets/publishing-unpublish-scope.png)

## Publicar y cancelar la publicación de un árbol {#publishing-and-unpublishing-a-tree}

Cuando haya introducido o actualizado un número considerable de páginas de contenido, todas ellas residentes dentro de la misma página raíz, puede resultar más fácil publicar todo el árbol en una acción.

Para hacerlo, puede utilizar la opción [Administrar publicación](#manage-publication) de la consola Sitios.

1. En la consola Sitios, seleccione la página raíz del árbol que desea publicar o cancelar la publicación y seleccione **Administrar publicación**.
1. Se inicia el asistente **Administrar publicación**. Elija si desea publicar o cancelar la publicación y cuándo debe producirse, y seleccione **Siguiente** para continuar.
1. En el paso **Ámbito**, seleccione la página raíz y seleccione **Incluir tareas secundarias**.

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

* En la [información general de recursos de la consola Sitios](/help/sites-cloud/authoring/basic-handling.md#viewing-and-selecting-resources)

  ![Estado de publicación en la vista de tarjeta](/help/sites-cloud/authoring/assets/publishing-status-console-card.png)

  El estado de publicación se indica en las vistas de [tarjeta](/help/sites-cloud/authoring/basic-handling.md#card-view), [columna](/help/sites-cloud/authoring/basic-handling.md#column-view) y [lista](/help/sites-cloud/authoring/basic-handling.md#list-view) de la consola Sitios.

* En la [cronología](/help/sites-cloud/authoring/basic-handling.md#timeline)

  ![Estado de publicación en la vista de cronología](/help/sites-cloud/authoring/assets/publishing-status-timeline.png)

* En el [menú Información de página](/help/sites-cloud/authoring/page-editor/introduction.md#page-information) cuando se edita una página.

  ![Estado de publicación en el menú Información de página](/help/sites-cloud/authoring/assets/publishing-status-page-information.png)
