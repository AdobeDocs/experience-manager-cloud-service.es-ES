---
title: Su bandeja de entrada
description: Administración de las tareas con la bandeja de entrada
translation-type: tm+mt
source-git-commit: 16725342c1a14231025bbc1bafb4c97f0d7cfce8

---


# Su bandeja de entrada {#your-inbox}

Puede recibir notificaciones de varias áreas de AEM, incluidos flujos de trabajo y proyectos. Por ejemplo, puede recibir notificaciones sobre:

* Tareas:
   * These can also be created at various points within the AEM UI, for example, under **Projects**.
   * These can be the product of a workflow **Create Task** or **Create Project Task** step.
* Flujos de trabajo:
   * Elementos de trabajo que representan acciones que debe realizar en el contenido de la página
      * These are the product of workflow **Participant** steps.
   * Elementos de error, para permitir que los administradores reintenten el paso fallido

Estas notificaciones se reciben en su propia bandeja de entrada, donde podrá consultarlas y llevar a cabo las acciones correspondientes.

>[!NOTE]
>
>Para obtener más información sobre los tipos de elemento, consulte también:
>
>* [Proyectos](/help/sites-cloud/authoring/projects/overview.md)
>* [Proyectos: trabajando con tareas](/help/sites-cloud/authoring/projects/tasks.md) 
>* [Flujos de trabajo](/help/sites-cloud/authoring/workflows/overview.md)


## Bandeja de entrada en el encabezado {#inbox-in-the-header}

Desde cualquiera de las consolas, en el encabezado se mostrará el número actual de elementos de su bandeja de entrada. También se puede abrir el indicador para acceder rápidamente a las páginas que requieran acciones o acceder a la bandeja de entrada:

![Introducción a la bandeja de entrada en el encabezado](/help/sites-cloud/authoring/assets/inbox-header.png)

>[!NOTE]
>
>Algunas acciones también se mostrarán en la [vista de tarjeta del recurso adecuado](/help/sites-cloud/authoring/getting-started/basic-handling.md#card-view).

## Apertura de la bandeja de entrada {#opening-the-inbox}

Para abrir la bandeja de entrada de notificaciones AEM:

1. Toque o haga clic en el indicador de la barra de herramientas.

1. Seleccione **Ver todo**. Se abrirá la **bandeja de entrada AEM.** La bandeja de entrada muestra elementos de flujos de trabajo, proyectos y tareas.
1. La vista predeterminada es [Vista de lista](#inbox-list-view), pero también puede cambiar a [Vista de calendario](#inbox-calendar-view). Esto se lleva a cabo con el selector de vista (barra de herramientas, en la parte superior derecha).

   For both views you can also define [View Settings](#inbox-view-settings). The options available are dependent on the current view.

   ![Ajustes de la vista de bandeja de entrada](/help/sites-cloud/authoring/assets/inbox-view-settings.png)

>[!NOTE]
>
>The Inbox operates as a console, so use [Global Navigation](/help/sites-cloud/authoring/getting-started/basic-handling.md#global-navigation) or [Search](/help/sites-cloud/authoring/getting-started/search.md) to navigate to another location when you are finished.

### Bandeja de entrada: Vista de lista {#inbox-list-view}

Esta vista muestra todos los elementos, junto con la información relevante:

![Vista de lista de la bandeja de entrada](/help/sites-cloud/authoring/assets/inbox-list-view.png)

### Bandeja de entrada: Vista de calendario {#inbox-calendar-view}

Esta vista presenta los elementos según su posición en el calendario:

![Vista de calendario de la bandeja de entrada](/help/sites-cloud/authoring/assets/inbox-calendar-view.png)

Puede hacer lo siguiente:

* Select a specific view: **Timeline**, **Column**, **List**
* Specify the tasks to display according to **Schedule**: **All**, **Planned**, **In Progress**, **Due Soon**, **Past Due**
* Explorar para obtener información más detallada sobre un elemento
* Seleccione un intervalo de fechas para enfocar la vista:

![Intervalo de fechas de vista del calendario de la Bandeja de entrada](/help/sites-cloud/authoring/assets/inbox-calendar-range.png)

### Bandeja de entrada: Configuración de vista {#inbox-view-settings}

Puede definir la configuración para ambas vistas (lista y calendario):

* **Vista de calendario**

   Para **Vista de calendario** puede configurar:

   * **Agrupar por**
   * **Programa** o **Ninguno**
   * **Tamaño de la tarjeta**
   ![Ajustes de vista de calendario de la bandeja de entrada](/help/sites-cloud/authoring/assets/inbox-calendar-settings.png)

* **Vista de lista**

   En **Vista de lista** puede configurar el mecanismo de ordenación:

   * **Ordenar en**
   * **Orden**
   ![Ajustes de la vista de lista de la bandeja de entrada](/help/sites-cloud/authoring/assets/inbox-list-settings.png)

   También puede delegar su calendario a otros usos, así como solicitar la delegación de otros usuarios y administrar sus delegaciones.

   ![Configuración de delegación de vista de lista de bandeja de entrada](/help/sites-cloud/authoring/assets/inbox-delegation.png)

## Acción en un elemento {#taking-action-on-an-item}

1. Para realizar una acción en un elemento, seleccione la miniatura correspondiente al elemento en cuestión. En la barra de herramientas se mostrarán iconos para las acciones aplicables a dicho elemento:

   ![Seleccionar elemento de bandeja de entrada](/help/sites-cloud/authoring/assets/inbox-select-item.png)

   Las acciones son apropiadas para el elemento y entre ellas se incluyen:

   * **Acción completa**
   * **Delegar** un elemento
   * **Abra** un elemento, en función del tipo de elemento, esta acción puede:

      * Mostrar las propiedades del elemento
      * Abra un tablero o asistente apropiado para realizar más acciones
      * Abrir documentación relacionada
   * **Retroceder** a una etapa anterior
   * Consultar la carga útil de un flujo de trabajo
   * Crear un proyecto a partir de un elemento
   >[!NOTE]
   >
   >Para obtener más información, consulte:
   >
   >* Elementos del flujo de trabajo - [Participación en flujos de trabajo](/help/sites-cloud/authoring/workflows/participating.md)


1. Según el elemento seleccionado, se iniciará una acción, por ejemplo:

   * Se abrirá un cuadro de diálogo apropiado para la acción
   * Se iniciará un asistente de acciones
   * Se abrirá una página de documentación
   For example, **Delegate** will open a dialog:

   ![Delegar tarea de bandeja de entrada](/help/sites-cloud/authoring/assets/inbox-assign-task.png)

   En función de si ha abierto un cuadro de diálogo, un asistente o una página de documentación, podrá:

   * Confirme la acción adecuada, por ejemplo, reasignar.
   * Cancelar la acción
   * Seleccione la flecha hacia atrás para volver a la bandeja de entrada; por ejemplo, si se ha abierto un asistente de acciones o una página de documentación, puede volver a la Bandeja de entrada.


## Creación de una tarea {#creating-a-task}

Desde la bandeja de entrada, puede crear tareas:

1. Seleccione **Crear** y, a continuación, **Tarea**.
1. Complete the necessary fields in the **Basic** and **Advanced** tabs (only the **Title** is mandatory, all others are optional):

   * **Básico**:

      * **Título**
      * **Proyecto**
      * **Usuario asignado**
      * **Contenido**, similar a Carga útil, es una referencia de la tarea a una ubicación en el repositorio
      * **Descripción**
      * **Prioridad de tareas**
      * **Fecha de inicio**
      * **Fecha de vencimiento**
   ![Bandeja de entrada agregar tarea](/help/sites-cloud/authoring/assets/inbox-create-task.png)

   * **Avanzado**

      * **Nombre**: se utilizará para formar la dirección URL y, si está en blanco, se basará en el **Título**.
   ![Bandeja de entrada agregar tareas opciones avanzadas](/help/sites-cloud/authoring/assets/inbox-add-task-advanced.png)

1. Seleccione **Enviar**.

## Creación de un proyecto {#creating-a-project}

Para determinadas tareas, puede crear un [proyecto](/help/sites-cloud/authoring/projects/overview.md) basado en dicha tarea:

1. Seleccione la tarea adecuada haciendo clic/tocando la miniatura correspondiente.

   >[!NOTE]
   >
   >Only tasks created using the **Create** option of the **Inbox** can be used to create a project.
   >
   >Los elementos de trabajo (de un flujo de trabajo) no se pueden usar para crear un proyecto.

1. Seleccione **Crear proyecto** en la barra de herramientas para abrir el asistente.
1. Seleccione la plantilla adecuada y, a continuación, **Siguiente**.
1. Especifique las propiedades requeridas:

   * **Básico**

      * **Título**
      * **Descripción**
      * **Fecha de inicio**
      * **Fecha de vencimiento**
      * **Usuario** y función
   * **Avanzado**

      * **Nombre**
   >[!NOTE]
   >
   >Consulte [Creación de un proyecto](/help/sites-cloud/authoring/projects/managing.md#creating-a-project) para obtener toda la información.

1. Seleccione **Crear** para confirmar la acción.

## Filtrado de elementos en la bandeja de entrada AEM {#filtering-items-in-the-aem-inbox}

Puede filtrar los elementos enumerados:

1. Abra la **Bandeja de entrada AEM**.

1. Abra el selector de filtros:

   ![Búsqueda en la bandeja de entrada](/help/sites-cloud/authoring/assets/inbox-search.png)

1. Puede filtrar los elementos enumerados según un rango de criterios, muchos de los cuales se pueden refinar.Por ejemplo:

   ![Filtro de búsqueda de bandeja de entrada](/help/sites-cloud/authoring/assets/inbox-search-filter.png)

   >[!NOTE]
   >
   >Con [Configuración de vista](#inbox-view-settings) también puede configurar el orden cuando se utiliza la [Vista de lista](#inbox-list-view).
