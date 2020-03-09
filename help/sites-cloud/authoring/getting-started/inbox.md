---
title: Su bandeja de entrada
description: Administración de las tareas con la bandeja de entrada
translation-type: ht
source-git-commit: 16725342c1a14231025bbc1bafb4c97f0d7cfce8

---


# Su bandeja de entrada   {#your-inbox}

Puede recibir notificaciones desde varias áreas de AEM, incluidos flujos de trabajo y proyectos. Por ejemplo, puede recibir notificaciones sobre:

* Tareas:
   * Estas también se pueden crear en distintos puntos de la IU de AEM, por ejemplo, en **Proyectos**.
   * Estas pueden ser el producto del paso **Crear tarea** o **Crear tarea del proyecto** de un flujo de trabajo.
* Flujos de trabajo:
   * Elementos de trabajo que representan acciones que debe realizar en el contenido de la página.
      * Estos pueden ser producto del paso **Participante** del flujo de trabajo.
   * Elementos con errores, que permiten a los administradores volver a intentar realizar un paso que ha fallado.

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

## Apertura de la bandeja de entrada   {#opening-the-inbox}

Para abrir la bandeja de entrada de notificaciones AEM:

1. Toque o haga clic en el indicador de la barra de herramientas.

1. Seleccione **Ver todo**. Se abrirá la **bandeja de entrada AEM.** La bandeja de entrada muestra elementos de flujos de trabajo, proyectos y tareas.
1. La vista predeterminada es [Vista de lista](#inbox-list-view), pero también puede cambiar a [Vista de calendario](#inbox-calendar-view). Esto se lleva a cabo con el selector de vista (barra de herramientas, en la parte superior derecha).

   Para ambas vistas también puede definir una [Configuración de vista](#inbox-view-settings). Las opciones disponibles dependen de la vista actual.

   ![Configuración de vista de la bandeja de entrada](/help/sites-cloud/authoring/assets/inbox-view-settings.png)

>[!NOTE]
>
>La bandeja de entrada actúa como una consola, por lo que se aconseja utilizar [Navegación global](/help/sites-cloud/authoring/getting-started/basic-handling.md#global-navigation) o [Buscar](/help/sites-cloud/authoring/getting-started/search.md) para desplazarse a otra ubicación cuando haya terminado.

### Bandeja de entrada: Vista de lista {#inbox-list-view}

En esta vista se muestra una lista de todos los elementos, así como información relevante:

![Vista de lista de la bandeja de entrada](/help/sites-cloud/authoring/assets/inbox-list-view.png)

### Bandeja de entrada: Vista de calendario {#inbox-calendar-view}

Esta vista presenta los elementos según su posición en el calendario:

![Vista de calendario de la bandeja de entrada](/help/sites-cloud/authoring/assets/inbox-calendar-view.png)

Puede hacer lo siguiente:

* Seleccionar una vista específica: **Cronología**, **Columna**, **Lista**.
* Especificar las tareas para mostrar según el **Programa**: **Todos**, **Planeado**, **En curso**, **Vence pronto**, **Ya ha vencido**.
* Desplazarse hacia abajo para obtener más información sobre un elemento.
* Seleccionar un intervalo de fechas en el que centrar la vista:

![Intervalo de fechas de vista de calendario de la bandeja de entrada](/help/sites-cloud/authoring/assets/inbox-calendar-range.png)

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
   ![Ajustes de vista de lista de la bandeja de entrada](/help/sites-cloud/authoring/assets/inbox-list-settings.png)

   También puede delegar el calendario a otros usos, así como solicitar la delegación de otros usuarios y administrar las delegaciones.

   ![Configuración de delegación de vista de lista de bandeja de entrada](/help/sites-cloud/authoring/assets/inbox-delegation.png)

## Acción en un elemento {#taking-action-on-an-item}

1. Para realizar una acción en un elemento, seleccione la miniatura correspondiente al elemento en cuestión. En la barra de herramientas se mostrarán iconos para las acciones aplicables a dicho elemento:

   ![Seleccionar elemento de bandeja de entrada](/help/sites-cloud/authoring/assets/inbox-select-item.png)

   Las acciones son apropiadas para el elemento y entre ellas se incluyen:

   * Acción **Completar**.
   * **Delegar** un elemento.
   * **Abrir** un elemento; en función del tipo de elemento, esta acción puede:

      * Mostrar las propiedades del elemento.
      * Abrir un tablero o un asistente apropiado para llevar a cabo acciones adicionales.
      * Abrir documentación relacionada.
   * **Retroceder** a una etapa anterior
   * Consultar la carga útil de un flujo de trabajo
   * Crear un proyecto a partir de un elemento
   >[!NOTE]
   >
   >Para obtener más información, consulte:
   >
   >* Elementos del flujo de trabajo - [Participación en flujos de trabajo](/help/sites-cloud/authoring/workflows/participating.md)


1. Dependiendo del elemento seleccionado, se inicia una acción; por ejemplo:

   * Se abre un cuadro de diálogo apropiado para la acción.
   * Se inicia un asistente de acciones.
   * Se abre una página de documentación.
   Por ejemplo, la opción **Delegar** abre el siguiente cuadro de diálogo:

   ![Delegar tarea de bandeja de entrada](/help/sites-cloud/authoring/assets/inbox-assign-task.png)

   En función de si ha abierto un cuadro de diálogo, un asistente o una página de documentación, puede:

   * Confirmar la acción adecuada; por ejemplo, Reasignar.
   * Cancelar la acción
   * Seleccione la flecha hacia atrás para volver a la bandeja de entrada; por ejemplo, si se ha abierto un asistente de acciones o una página de documentación, puede volver a la bandeja de entrada.


## Creación de una tarea {#creating-a-task}

Desde la bandeja de entrada, puede crear tareas:

1. Seleccione **Crear** y, a continuación, **Tarea**.
1. Complete los campos necesarios en las pestañas **Básico** y **Avanzado** (el único campo obligatorio es **Título**, el resto son opcionales):

   * **Básico**:

      * **Título**
      * **Proyecto**
      * **Usuario asignado**
      * **Contenido**: similar a Carga útil, es una referencia de la tarea a una ubicación del repositorio
      * **Descripción**
      * **Prioridad de tareas**
      * **Fecha de inicio**
      * **Fecha de vencimiento**
   ![Añadir tarea en la bandeja de entrada](/help/sites-cloud/authoring/assets/inbox-create-task.png)

   * **Avanzado**

      * **Nombre:**: este se usa para crear la dirección URL; si está en blanco, se basa en el **Título**.
   ![Opciones avanzadas de añadir tarea en la bandeja de entrada](/help/sites-cloud/authoring/assets/inbox-add-task-advanced.png)

1. Seleccione **Enviar**.

## Creación de un proyecto   {#creating-a-project}

Para determinadas tareas, puede crear un [proyecto](/help/sites-cloud/authoring/projects/overview.md) basado en dicha tarea:

1. Seleccione la tarea adecuada haciendo clic/tocando la miniatura correspondiente.

   >[!NOTE]
   >
   >Para crear un proyecto, solo se pueden utilizar las tareas que se crearon con la opción **Crear** de la **bandeja de entrada**.
   >
   >Los elementos de trabajo (de un flujo de trabajo) no se pueden utilizar para crear un proyecto.

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

## Filtrado de elementos en la bandeja de entrada AEM   {#filtering-items-in-the-aem-inbox}

Puede filtrar los elementos enumerados:

1. Abra la **Bandeja de entrada AEM**.

1. Abra el selector de filtros:

   ![Búsqueda en la bandeja de entrada](/help/sites-cloud/authoring/assets/inbox-search.png)

1. Puede filtrar los elementos enumerados según un rango de los criterios, muchos de los cuales se pueden refinar. Por ejemplo:

   ![Filtro de búsqueda de bandeja de entrada](/help/sites-cloud/authoring/assets/inbox-search-filter.png)

   >[!NOTE]
   >
   >Con [Configuración de vista](#inbox-view-settings) también puede configurar el orden cuando se utiliza la [Vista de lista](#inbox-list-view).
