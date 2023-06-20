---
title: Guía rápida de introducción para la creación de páginas
description: Guía rápida y de alto nivel para empezar a crear contenido de página.
exl-id: d37c9b61-7382-4bf6-8b90-59726b871264
source-git-commit: 635f4c990c27a7646d97ebd08b453c71133f01b3
workflow-type: tm+mt
source-wordcount: '1572'
ht-degree: 62%

---

# Guía rápida de introducción para la creación de páginas {#quick-guide-to-authoring-pages}

Este documento está diseñado como guía de inicio rápido de alto nivel para las acciones de creación de páginas clave en AEM. Este documento:

* No incluye una explicación profunda.
* Proporcionan enlaces para una documentación más detallada.

Para obtener más información sobre la creación con AEM, consulte:

* [Conceptos de creación](/help/sites-cloud/authoring/getting-started/concepts.md)
* [Gestión básica](/help/sites-cloud/authoring/getting-started/basic-handling.md)

## Algunas sugerencias rápidas {#a-few-quick-hints}

Antes de comenzar la guía de inicio rápido, aquí hay una pequeña colección de sugerencias generales que debe tener en cuenta, divididas entre las áreas del sistema de creación.

### En la consola Sitios {#sites-console}

* Botón Crear

   * Este botón está disponible en muchas consolas. Las opciones presentadas son sensibles al contexto, por lo que pueden variar en función del escenario.

* Reordenación de páginas

   * Esto se puede hacer en [Vista de lista](/help/sites-cloud/authoring/getting-started/basic-handling.md#list-view). Los cambios se aplican y son visibles en otras vistas.

### Creación de páginas {#page-authoring}

* Vínculos de navegación 

   * **Los vínculos no están disponibles para la navegación** cuando esté en **Editar** modo. Para navegar con vínculos, debe hacer lo siguiente [previsualizar la página](/help/sites-cloud/authoring/fundamentals/editing-content.md#previewing-pages) mediante:

      * [Modo de vista previa](/help/sites-cloud/authoring/fundamentals/editing-content.md#preview-mode)
      * [Ver como aparece publicado](/help/sites-cloud/authoring/fundamentals/editing-content.md#view-as-published)

* Las versiones no se inician ni se crean en el editor de páginas; ahora se realiza desde la consola **Sitios** (a través de la opción **Crear** o la [cronología](/help/sites-cloud/authoring/getting-started/basic-handling.md#timeline) de un recurso seleccionado).

>[!NOTE]
>
>Existen varios métodos abreviados del teclado que pueden facilitar la experiencia de creación.
>
>* [Atajos de teclado al editar páginas](/help/sites-cloud/authoring/fundamentals/keyboard-shortcuts.md)
>* [Métodos abreviados del teclado para las consolas](/help/sites-cloud/authoring/getting-started/keyboard-shortcuts.md)

### Encontrar su página {#finding-your-page}

Existen varios aspectos para encontrar una página; puede navegar o buscar:

1. Abra la consola **Sitios** (con la opción **Sitios** de [Navegación global](/help/sites-cloud/authoring/getting-started/basic-handling.md#global-navigation): esto se activa (menú desplegable) al seleccionar el vínculo de Adobe Experience Manager (parte superior izquierda).

1. Desplácese por el árbol y toque o haga clic en la página adecuada. La manera en la que se presentan los recursos de la página depende de la vista que utilice: [Tarjeta, Lista o Columnas](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources):

   ![Ver lista desplegable de selección](/help/sites-cloud/authoring/assets/views.png)

1. Desplácese hacia arriba en el árbol mediante [la ruta de exploración del encabezado](/help/sites-cloud/authoring/getting-started/basic-handling.md#the-header); esto permite volver a la ubicación seleccionada:

   ![Lista desplegable de ruta de exploración](/help/sites-cloud/authoring/assets/breadcrumb.png)

1. También puede [Buscar](/help/sites-cloud/authoring/getting-started/search.md) para una página. Puede seleccionar su página de entre los resultados mostrados.

   ![Campo de búsqueda](/help/sites-cloud/authoring/assets/search.png)

### Creación de una nueva página {#creating-a-new-page}

Para [crear una nueva página](/help/sites-cloud/authoring/fundamentals/organizing-pages.md#creating-a-new-page):

1. [Desplácese hasta la ubicación en la que desee crear la nueva página.](#finding-your-page)
1. Utilice el **Crear** y luego seleccione **Página** de la lista:

   ![Botón Crear](/help/sites-cloud/authoring/assets/create.png)

1. Se abre el asistente que le guiará a través de la recopilación de la información necesaria cuando [creación de la nueva página](/help/sites-cloud/authoring/fundamentals/organizing-pages.md#creating-a-new-page). Siga las instrucciones que aparecen en pantalla.

### Seleccionar su página para ejecutar acciones adicionales   {#selecting-your-page-for-further-action}

Puede seleccionar una página para poder realizar acciones en ella. Si se selecciona una página, se actualizará automáticamente la barra de herramientas para que se muestren las acciones relevantes para ese recurso.

La forma de seleccionar una página depende de la vista que utilice en la consola:

1. Vista de columna:

   * Pulse o haga clic en la miniatura del recurso en cuestión: la miniatura muestra una marca de verificación para mostrar que se ha seleccionado.

1. Vista en lista:

   * Pulse o haga clic en la miniatura del recurso en cuestión: la miniatura muestra una marca de verificación para mostrar que se ha seleccionado.

1. Vista de tarjeta:

   * Indique el modo de selección al [elegir el recurso necesario](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources). El modo de hacerlo depende del dispositivo:

      * En un dispositivo móvil: pulsar y mantener pulsada la tarjeta.
      * En un dispositivo de escritorio: usar la [acción rápida](/help/sites-cloud/authoring/getting-started/basic-handling.md#quick-actions) representada por el icono de visto:

   * La tarjeta se superpone con una marca de verificación para mostrar que se ha seleccionado la página.

   ![Tarjeta de ejemplo](/help/sites-cloud/authoring/assets/card.png)

### Acciones rápidas (solo vista de tarjeta y escritorio) {#quick-actions-card-view-desktop-only}

Hay [acciones rápidas](/help/sites-cloud/authoring/getting-started/basic-handling.md#quick-actions) disponibles:

1. [Desplácese hasta la página](#finding-your-page) sobre la que quiera llevar a cabo una acción.
1. Pase el puntero del ratón sobre la tarjeta que representa el recurso necesario. Se muestran las acciones rápidas:

   ![Acciones de tarjeta](/help/sites-cloud/authoring/assets/card-actions.png)

### Edición del contenido de la página {#editing-your-page-content}

Para editar la página:

1. [Desplácese hasta la página](#finding-your-page) que quiera editar.
1. [Abra la página que quiera editar](/help/sites-cloud/authoring/fundamentals/organizing-pages.md#opening-a-page-for-editing) con el icono Editar (lápiz):

   Botón ![Editar](/help/sites-cloud/authoring/assets/edit.png)

   Puede acceder desde:

   * [Acciones rápidas (solo vista de tarjeta y escritorio)](#quick-actions-card-view-desktop-only) para el recurso adecuado.
   * La barra de herramientas cuando [su página se haya seleccionado](#selecting-your-page-for-further-action).

1. Cuando se abra el editor, podrá hacer lo siguiente:

   * [Añadir un componente nuevo a su página](/help/sites-cloud/authoring/fundamentals/editing-content.md#inserting-a-component) mediante las siguientes opciones:

      * Abrir el panel lateral.
      * Seleccionar la pestaña de componentes (el [buscador de componentes](/help/sites-cloud/authoring/fundamentals/environment-tools.md#components-browser)).
      * Arrastrar el componente requerido a su página.

     El panel lateral se puede abrir (y cerrar) con:

     ![Botón de alternador del panel lateral](/help/sites-cloud/authoring/assets/side-panel-toggle.png)

   * [Editar el contenido de un componente existente](/help/sites-cloud/authoring/fundamentals/editing-content.md#component-toolbar) en la página:

      * Abra la barra de herramientas de componentes haciendo clic sobre ella. Utilice el **Editar** (lápiz) para abrir el cuadro de diálogo.
      * Abra el editor en contexto del componente pulsando y manteniendo pulsado o haciendo doble clic lentamente. Se muestran las acciones disponibles (para algunos componentes, es una selección limitada).
      * Para ver todas las acciones disponibles, acceda al modo de pantalla completa mediante:

        ![Botón Pantalla completa](/help/sites-cloud/authoring/assets/full-screen.png)

   * [Configurar las propiedades de un componente existente](/help/sites-cloud/authoring/fundamentals/editing-content.md#component-edit-dialog)

      * Abra la barra de herramientas de componentes haciendo clic sobre ella. Utilice el **Configurar** (llave inglesa) para abrir el cuadro de diálogo.

   * [Mover un componente](/help/sites-cloud/authoring/fundamentals/editing-content.md#moving-a-component) o bien:

      * Arrastre el componente en cuestión a su nueva ubicación.
      * Abra la barra de herramientas de componentes haciendo clic sobre ella. Utilice los iconos **Cortar** y **Pegar** donde sea necesario.

   * [Copiar (y pegar)](/help/sites-cloud/authoring/fundamentals/editing-content.md#component-toolbar) un componente:

      * Abra la barra de herramientas de componentes haciendo clic sobre ella. Utilice los iconos **Copiar** y **Pegar** cuando sea necesario.

   >[!NOTE]
   >
   >Puede **pegar** componentes en la misma página o en otra página. Si pega el componente en una página diferente que ya estaba abierta antes de la operación de cortar o copiar, tendrá que actualizase la página. 

   * [Eliminar](/help/sites-cloud/authoring/fundamentals/editing-content.md#component-toolbar) un componente:

      * Abra la barra de herramientas de componentes haciendo clic sobre ella y utilice el icono **Eliminar.**

   * [Añadir anotaciones](/help/sites-cloud/authoring/fundamentals/annotations.md#annotations) a la página:

      * Seleccione el **Anotar** modo (icono de burbuja de voz). Añadir anotaciones mediante el **Añadir anotación** Icono (más). Salga del modo Anotar utilizando la X en la parte superior derecha.

        ![Botón Anotaciones](/help/sites-cloud/authoring/assets/annotations.png)

   * [Previsualización de una página](/help/sites-cloud/authoring/fundamentals/editing-content.md#preview-mode) (para ver cómo aparecerá en el entorno de publicación)

      * Seleccionar **Previsualizar** en la barra de herramientas.

   * Vuelva al modo de edición (o seleccione otro modo) utilizando **Editar** selector desplegable.

   >[!NOTE]
   >
   >Para navegar mediante vínculos en el contenido, debe utilizar [Modo de previsualización](/help/sites-cloud/authoring/fundamentals/editing-content.md#preview-mode).

### Editar las Propiedades de la página   {#editing-the-page-properties}

Existen dos métodos (principales) de [editar propiedades de página](/help/sites-cloud/authoring/fundamentals/page-properties.md):

* Desde la consola **Sitios**:

   1. [Navegue hasta la página](#finding-your-page) que desea publicar.
   1. Seleccione el **Propiedades** icono de:

      * [Acciones rápidas (solo vista de tarjeta y escritorio)](#quick-actions-card-view-desktop-only) para el recurso adecuado.
      * La barra de herramientas cuando [su página se haya seleccionado](#selecting-your-page-for-further-action).

      ![Botón Propiedades](/help/sites-cloud/authoring/assets/properties.png)

   1. Se muestran las propiedades de la página. Puede aplicar actualizaciones según sea necesario y, a continuación, seleccionar Guardar para preservarlas.

* Cuándo [editar su página](#editing-your-page-content):

   1. Abra el **Información de página** menú.
   1. Seleccionar **Abrir propiedades** para abrir el cuadro de diálogo y editar las propiedades.

      ![Botón Información de página](/help/sites-cloud/authoring/assets/page-information.png)

### Publicar su página (o eliminar la publicación) {#publishing-your-page-or-unpublishing}

Existen dos métodos principales de [publicación de la página](/help/sites-cloud/authoring/fundamentals/publishing-pages.md) (y también de cancelar la publicación):

* Desde la consola **Sitios**:

   1. [Navegue hasta la página](#finding-your-page) que desea publicar.
   1. Seleccione el icono **Publicación rápida** desde:

      * [Acciones rápidas (solo vista de tarjeta y escritorio)](#quick-actions-card-view-desktop-only) para el recurso adecuado.
      * La barra de herramientas cuando su [página se haya seleccionado](#selecting-your-page-for-further-action) (también permite el acceso a [Publicar posteriormente](/help/sites-cloud/authoring/fundamentals/publishing-pages.md)).

      ![Botón Publicación rápida](/help/sites-cloud/authoring/assets/quick-publish.png)

* Cuándo [editar su página](#editing-your-page-content):

   1. Abra el **Información de página** menú.
   1. Seleccionar **Publicar página**.

* La cancelación de la publicación de una página desde la consola solo se puede realizar mediante la opción **Administrar publicación**, que solo está disponible en la barra de herramientas (no a través de las acciones rápidas).

  ![Botón Administrar publicación](/help/sites-cloud/authoring/assets/manage-publication.png)

  El **Cancelar publicación de página** sigue estando disponible a través de la opción **Información de página** en el editor.

  Consulte [Publicación de páginas](/help/sites-cloud/authoring/fundamentals/publishing-pages.md#unpublishing-pages) para obtener más información.

### Mover, copiar y pegar o eliminar su página   {#move-copy-and-paste-or-delete-your-page}

Todas estas acciones se pueden activar mediante:

1. [Navegue hasta la página](#finding-your-page) desea mover, copiar y pegar o eliminar.
1. Seleccione el icono de copiar (y luego pegar), mover o eliminar según sea necesario mediante:

   * [Acciones rápidas (solo vista de tarjeta y escritorio)](#quick-actions-card-view-desktop-only) para el recurso requerido.
   * La barra de herramientas cuando su [página se haya seleccionado](#selecting-your-page-for-further-action).

   A continuación, depende de la acción:

   * [Copiar](/help/sites-cloud/authoring/fundamentals/organizing-pages.md#copying-and-pasting-a-page):

      * Desplácese hasta la nueva ubicación y péguelo allí.

   * [Mover](/help/sites-cloud/authoring/fundamentals/organizing-pages.md#moving-or-renaming-a-page):

      * Se abrirá el asistente para recoger la información necesaria para mover la página. Siga las instrucciones que aparecen en la pantalla.

   * [Eliminar](/help/sites-cloud/authoring/fundamentals/organizing-pages.md#deleting-a-page):

      * Se le pedirá que confirme la acción.

   >[!NOTE]
   >
   >La opción Eliminar no se encuentra disponible como Acción rápida.

### Bloquear y desbloquear su página  {#locking-your-page-then-unlocking}

[Bloquear una página](/help/sites-cloud/authoring/fundamentals/editing-content.md#locking-a-page) impide que otros autores trabajen en ella al mismo tiempo que usted. El icono/botón Bloquear (y Desbloquear) se encuentra en:

* La barra de herramientas cuando su [página se haya seleccionado](#selecting-your-page-for-further-action).
* Menú desplegable [Información de la página](#editing-the-page-properties) cuando edita la página.
* Barra de herramientas de la página cuando edita la página (cuando está bloqueada).

Por ejemplo, el icono de bloqueo presenta el siguiente aspecto:

![Botón Bloquear](/help/sites-cloud/authoring/assets/lock.png)

### Acceder a las referencias de la página {#accessing-page-references}

[El acceso rápido a las referencias](/help/sites-cloud/authoring/fundamentals/environment-tools.md#references) hasta/desde una página está disponible en la Barra de referencias.

1. Seleccione **Referencias** mediante el icono de la barra de herramientas (antes o después de [seleccionar su página](#selecting-your-page-for-further-action)): 

   ![Opción de vista Referencias](/help/sites-cloud/authoring/assets/references.png)

   Se muestra una lista de tipos de referencias:

   ![Vista Referencias](/help/sites-cloud/authoring/assets/references-list.png)

1. Pulse o haga clic en el tipo de referencia requerido para mostrar más detalles y (cuando corresponda) realizar más acciones.

### Crear una versión de su página   {#creating-a-version-of-your-page}

Para crear una [versión](/help/sites-cloud/authoring/features/page-versions.md) de la página:

1. Para abrir el raíl de cronología, seleccione **[Cronología](/help/sites-cloud/authoring/getting-started/basic-handling.md#timeline)** con el icono de la barra de herramientas (antes o después de [seleccionar su página](#selecting-your-page-for-further-action)): 

   ![Opción de vista Cronología](/help/sites-cloud/authoring/assets/timeline.png)

1. Haga clic o pulse en los puntos suspensivos, en la parte inferior derecha de la columna Cronología, para mostrar botones adicionales; como, por ejemplo, **Guardar como versión**.

   ![Vista Cronología](/help/sites-cloud/authoring/assets/timeline-view.png)

1. Seleccione **Guardar como versión**, y después seleccione **Crear**.

### Restablecer o comparar una versión de su página {#restoring-comparing-a-version-of-your-page}

Se utiliza el mismo mecanismo básico cuando se restablecen y/o se comparan versiones de su página:

1. Seleccione **[Línea de tiempo](/help/sites-cloud/authoring/getting-started/basic-handling.md#timeline)** mediante el icono de la barra de herramientas (antes o después de [seleccionar su página](#selecting-your-page-for-further-action)): 

   ![Opción de vista Cronología](/help/sites-cloud/authoring/assets/timeline.png)

   Si ya se ha guardado una versión de la página, aparecerá en la línea de tiempo.

1. Pulse o haga clic en la versión que desea restaurar. Esto mostrará botones de acción adicionales:

   * **Volver a esta versión**

      * Se restaura la versión.

   * **Mostrar diferencias**

      * La página se abre con las diferencias (entre las dos versiones) resaltadas.
