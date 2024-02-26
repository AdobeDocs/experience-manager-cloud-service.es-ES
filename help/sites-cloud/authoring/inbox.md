---
title: Su bandeja de entrada
description: Aprenda a utilizar las notificaciones que llegan a la bandeja de entrada para administrar sus tareas.
exl-id: 37d0cf43-192f-4a50-b174-42d7dced3b63
source-git-commit: bbd845079cb688dc3e62e2cf6b1a63c49a92f6b4
workflow-type: tm+mt
source-wordcount: '910'
ht-degree: 88%

---

# Su bandeja de entrada {#your-inbox}

Puede recibir notificaciones desde varias áreas de AEM, incluidos flujos de trabajo y proyectos. Por ejemplo, puede recibir notificaciones sobre:

* Tareas:
   * Estas también se pueden crear en distintos puntos de la IU de AEM, por ejemplo, en **Proyectos**.
   * Estas pueden ser el producto del paso **Crear tarea** o **Crear tarea del proyecto** de un flujo de trabajo.
* Flujos de trabajo:
   * Elementos de trabajo que representan acciones que debe realizar en el contenido de la página.
      * Estos pueden ser producto del paso **Participante** del flujo de trabajo.
   * Elementos con errores, que permiten a los administradores volver a intentar realizar un paso que ha fallado.

Recibirá estas notificaciones en su propia bandeja de entrada, donde podrá verlas y actuar en consecuencia.

>[!NOTE]
>
>Para obtener más información acerca de los tipos de elementos, consulte lo siguiente:
>
>* [Proyectos](/help/sites-cloud/authoring/projects/overview.md)
>* [Proyectos: trabajo con tareas](/help/sites-cloud/authoring/projects/tasks.md)
>* [Flujos de trabajo](/help/sites-cloud/authoring/workflows/overview.md)

## Bandeja de entrada en el encabezado {#inbox-in-the-header}

Desde cualquiera de las consolas, en el encabezado se muestra el número actual de elementos de la bandeja de entrada. El indicador también se puede abrir para proporcionar acceso rápido a las páginas que requieren acciones o acceso a la bandeja de entrada:

![Introducción a la bandeja de entrada en el encabezado](/help/sites-cloud/authoring/assets/inbox-header.png)

>[!NOTE]
>
>Algunas acciones también se mostrarán en la [vista de tarjeta del recurso adecuado](/help/sites-cloud/authoring/basic-handling.md#card-view).

## Apertura de la bandeja de entrada    {#opening-the-inbox}

Para abrir la bandeja de entrada de notificaciones AEM:

1. Seleccione el indicador en la barra de herramientas.

1. Seleccione **Ver todo**. El **AEM Bandeja de entrada de** abre. La bandeja de entrada muestra elementos de flujos de trabajo, proyectos y tareas.
1. La vista predeterminada es [Vista de lista](#inbox-list-view), pero también puede cambiar a [Vista de calendario](#inbox-calendar-view). Esto se realiza con el selector de vistas (barra de herramientas, arriba a la derecha).

   Para ambas vistas también puede definir una [Configuración de vista](#inbox-view-settings). Las opciones disponibles dependen de la vista actual.

   ![Configuración de vista de la bandeja de entrada](/help/sites-cloud/authoring/assets/inbox-view-settings.png)

>[!NOTE]
>
>La bandeja de entrada actúa como una consola, por lo que se aconseja utilizar [Navegación global](/help/sites-cloud/authoring/basic-handling.md#global-navigation) o [Buscar](/help/sites-cloud/authoring/search.md) para desplazarse a otra ubicación cuando haya terminado.

### Bandeja de entrada: vista de lista {#inbox-list-view}

En esta vista se muestra una lista de todos los elementos, así como información relevante:

![Vista de lista de la bandeja de entrada](/help/sites-cloud/authoring/assets/inbox-list-view.png)

### Bandeja de entrada: vista de calendario {#inbox-calendar-view}

Esta vista presenta los elementos según su posición en el calendario:

![Vista de calendario de la bandeja de entrada](/help/sites-cloud/authoring/assets/inbox-calendar-view.png)

Puede hacer lo siguiente:

* Seleccionar una vista específica: **Cronología**, **Columna**, **Lista**.
* Especificar las tareas para mostrar según el **Programa**: **Todos**, **Planeado**, **En curso**, **Vence pronto**, **Ya ha vencido**.
* Desplazarse hacia abajo para obtener más información sobre un elemento.
* Seleccionar un intervalo de fechas en el que centrar la vista:

![Intervalo de fechas de vista de calendario de la bandeja de entrada](/help/sites-cloud/authoring/assets/inbox-calendar-range.png)

### Bandeja de entrada: configuración de vista {#inbox-view-settings}

Para ambas vistas (Lista y Calendario) puede definir la siguiente configuración:

* **Vista de calendario**

  Para **Vista de calendario** puede configurar lo siguiente:

   * **Agrupar por**
   * **Programa** o **Ninguno**
   * **Tamaño de la tarjeta**

  ![Ajustes de vista de calendario de la bandeja de entrada](/help/sites-cloud/authoring/assets/inbox-calendar-settings.png)

* **Vista de lista**

  Para **Vista de lista** puede configurar el mecanismo de ordenación:

   * **Ordenar en**
   * **Orden de clasificación**

  ![Ajustes de vista de lista de la bandeja de entrada](/help/sites-cloud/authoring/assets/inbox-list-settings.png)

  También puede delegar el calendario a otros usuarios, así como solicitar la delegación de otros usuarios y administrar sus delegaciones.

  ![Configuración de la delegación de vista de lista de bandeja de entrada](/help/sites-cloud/authoring/assets/inbox-delegation.png)

## Acción en un elemento {#taking-action-on-an-item}

>[!NOTE]
>
>Aunque es posible seleccionar más de un elemento, las acciones solo se pueden realizar en un elemento a la vez.

1. Para realizar una acción sobre un elemento, seleccione la miniatura correspondiente al elemento en cuestión. Los iconos de las acciones aplicables a ese elemento se muestran en la barra de herramientas:

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
   >Para obtener más información, consulte lo siguiente:
   >
   >* Elementos de flujo de trabajo: [Participación en flujos de trabajo](/help/sites-cloud/authoring/workflows/participating.md)

2. Dependiendo del elemento seleccionado, se inicia una acción; por ejemplo:

   * Se abre un cuadro de diálogo apropiado para la acción
   * Se inicia el asistente de acciones
   * Se abre una página de documentación

   Por ejemplo, **Delegar** abre un cuadro de diálogo:

   ![Delegar tarea de bandeja de entrada](/help/sites-cloud/authoring/assets/inbox-assign-task.png)

   En función de si ha abierto un cuadro de diálogo, un asistente o una página de documentación, puede:

   * Confirme la acción adecuada; por ejemplo, reasignar.
   * Cancelar la acción
   * Seleccione la flecha hacia atrás para volver a la bandeja de entrada; por ejemplo, si se ha abierto un asistente de acciones o una página de documentación, puede volver a la bandeja de entrada.

## Creación de una tarea {#creating-a-task}

Desde la bandeja de entrada puede crear las siguientes tareas:

1. Seleccione **Crear** y a continuación, **Tarea**.
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

      * **Nombre**: se utiliza para formar la dirección URL; si está en blanco, se basa en el **Título**.

   ![Opciones avanzadas de añadir tarea en la bandeja de entrada](/help/sites-cloud/authoring/assets/inbox-add-task-advanced.png)

1. Seleccione **Enviar**.

## Creación de un proyecto    {#creating-a-project}

Para determinadas tareas, puede crear un [Proyecto](/help/sites-cloud/authoring/projects/overview.md) basado en esa tarea:

1. Seleccione la tarea adecuada pulsando o haciendo clic en la miniatura.

   >[!NOTE]
   >
   >Para crear un proyecto, solo se pueden utilizar las tareas que se crearon con la opción **Crear** de la **bandeja de entrada**.
   >
   >Los elementos de trabajo (de un flujo de trabajo) no se pueden utilizar para crear un proyecto.

1. Seleccione **Crear proyecto** en la barra de herramientas para abrir el asistente.
1. Seleccione la plantilla apropiada y, a continuación, **Siguiente**.
1. Especifique las propiedades necesarias:

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
   >Consulte [Creación de un proyecto](/help/sites-cloud/authoring/projects/managing.md#creating-a-project) para obtener información completa.

1. Seleccione **Crear** para confirmar la acción.

## Filtrado de elementos en la bandeja de entrada AEM    {#filtering-items-in-the-aem-inbox}

Puede filtrar los elementos enumerados:

1. Abra la **Bandeja de entrada AEM**.

1. Abra el selector de filtros:

   ![Búsqueda en la bandeja de entrada](/help/sites-cloud/authoring/assets/inbox-search.png)

1. Puede filtrar los elementos enumerados según un rango de los criterios, muchos de los cuales se pueden refinar. Por ejemplo:

   ![Filtro de búsqueda de bandeja de entrada](/help/sites-cloud/authoring/assets/inbox-search-filter.png)

   >[!NOTE]
   >
   >Con [Configuración de vista](#inbox-view-settings) también puede configurar el orden cuando se utiliza la [Vista de lista](#inbox-list-view).
