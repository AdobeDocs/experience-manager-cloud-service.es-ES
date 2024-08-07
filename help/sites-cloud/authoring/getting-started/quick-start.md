---
title: Guía rápida de introducción para la creación de páginas
description: Guía rápida y de alto nivel para empezar a crear contenido de página.
exl-id: d37c9b61-7382-4bf6-8b90-59726b871264
source-git-commit: 0ad9f349c997c35862e4f571b4741ed4c0c947e2
workflow-type: tm+mt
source-wordcount: '1541'
ht-degree: 79%

---


# Guía rápida de introducción para la creación de páginas {#quick-guide-to-authoring-pages}

Este documento está diseñado como guía de inicio rápido de alto nivel para las acciones de creación de páginas clave en AEM. Este documento:

* No incluye una explicación profunda.
* Proporcionan enlaces para una documentación más detallada.

Para obtener más información sobre la creación con AEM, consulte:

* [Conceptos de creación](/help/sites-cloud/authoring/getting-started/concepts.md)
* [Gestión básica](/help/sites-cloud/authoring/getting-started/basic-handling.md)

{{edge-delivery-authoring}}

## Algunas sugerencias rápidas {#a-few-quick-hints}

Antes de comenzar la guía de inicio rápido, aquí hay una pequeña colección de sugerencias generales que debe tener en cuenta, divididas entre las áreas del sistema de creación.

### En la consola Sitios {#sites-console}

* Botón Crear

   * Este botón está disponible en muchas consolas. Las opciones presentadas son sensibles al contexto, por lo que pueden variar en función del escenario.

* Reordenación de páginas

   * Esto se puede hacer en [Vista de lista](/help/sites-cloud/authoring/getting-started/basic-handling.md#list-view). Los cambios se aplican y son visibles en otras vistas.

### Creación de páginas {#page-authoring}

* Vínculos de navegación 

   * **Los vínculos no están disponibles para la navegación** cuando esté en el modo **Editar**. Para navegar con vínculos, debe [previsualizar la página](/help/sites-cloud/authoring/fundamentals/editing-content.md#previewing-pages) mediante lo siguiente:

      * [Modo de vista previa](/help/sites-cloud/authoring/fundamentals/editing-content.md#preview-mode)
      * [Ver como aparece publicado](/help/sites-cloud/authoring/fundamentals/editing-content.md#view-as-published)

* Las versiones no se inician ni se crean desde el editor de páginas. Esto ahora se hace desde la consola **Sitios** (a través de **Crear** o [Cronología](/help/sites-cloud/authoring/getting-started/basic-handling.md#timeline) para un recurso seleccionado).

>[!NOTE]
>
>Existen varios métodos abreviados del teclado que pueden facilitar la experiencia de creación.
>
>* [Métodos abreviados del teclado al editar páginas](/help/sites-cloud/authoring/fundamentals/keyboard-shortcuts.md)
>* [Métodos abreviados del teclado para las consolas](/help/sites-cloud/authoring/getting-started/keyboard-shortcuts.md)

### Encontrar su página {#finding-your-page}

Existen varios aspectos para encontrar una página; puede navegar o buscar:

1. Abra la consola **Sites** (utilizando la opción **Sites** de la [Navegación global](/help/sites-cloud/authoring/getting-started/basic-handling.md#global-navigation): esto se activa (menú desplegable) al seleccionar el vínculo de Adobe Experience Manager (parte superior izquierda).

1. Desplácese hacia abajo en el árbol tocando o haciendo clic en la página correspondiente. La manera en que se representan los recursos de la página depende de la vista que utilice: [Tarjeta, Lista o Columna](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources):

   ![Ver lista desplegable de selección](/help/sites-cloud/authoring/assets/views.png)

1. Desplácese hacia arriba del árbol mediante [la ruta de exploración del encabezado](/help/sites-cloud/authoring/getting-started/basic-handling.md#the-header), que le permite volver a la ubicación seleccionada:

   ![Lista desplegable de ruta de exploración](/help/sites-cloud/authoring/assets/breadcrumb.png)

1. También puede [buscar](/help/sites-cloud/authoring/getting-started/search.md) una página. Puede seleccionar la página en los resultados que se muestran.

   ![Campo de búsqueda](/help/sites-cloud/authoring/assets/search.png)

### Creación de una nueva página {#creating-a-new-page}

Para [crear una página](/help/sites-cloud/authoring/fundamentals/organizing-pages.md#creating-a-new-page):

1. [Desplácese hasta la ubicación en la que desee crear la nueva página.](#finding-your-page)
1. Utilice el icono **Crear** y luego seleccione **Página** en la lista:

   ![Botón Crear](/help/sites-cloud/authoring/assets/create.png)

1. Se abre el asistente que le guiará a través de la recopilación de la información necesaria cuando [cree su nueva página](/help/sites-cloud/authoring/fundamentals/organizing-pages.md#creating-a-new-page). Siga las instrucciones que aparecen en pantalla.

### Seleccionar su página para ejecutar acciones adicionales   {#selecting-your-page-for-further-action}

Puede seleccionar una página para poder actuar en ella. Si se selecciona una página, se actualizará automáticamente la barra de herramientas para que se muestren las acciones relevantes para ese recurso.

La forma de seleccionar una página depende de la vista que utilice en la consola:

1. Vista de columna:

   * Seleccione la miniatura del recurso en cuestión: la miniatura se superpone con una marca de verificación para indicar que se ha seleccionado.

1. Vista en lista:

   * Seleccione la miniatura del recurso en cuestión: la miniatura se superpone con una marca de verificación para indicar que se ha seleccionado.

1. Vista de tarjeta:

   * Indique el modo de selección al [elegir el recurso necesario](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources). El modo de hacerlo depende del dispositivo:

      * En un dispositivo móvil: seleccionar y mantener pulsada la tarjeta
      * En un dispositivo de escritorio: usar la [acción rápida](/help/sites-cloud/authoring/getting-started/basic-handling.md#quick-actions) representada por el icono de visto:

   * En la tarjeta se superpone una marca de verificación que indica que se ha seleccionado la página.

   ![Tarjeta de ejemplo](/help/sites-cloud/authoring/assets/card.png)

### Acciones rápidas (solo vista de tarjeta y escritorio) {#quick-actions-card-view-desktop-only}

Hay [acciones rápidas](/help/sites-cloud/authoring/getting-started/basic-handling.md#quick-actions) disponibles:

1. [Vaya a la página](#finding-your-page) en la que desee actuar.
1. Pase el puntero del ratón sobre la tarjeta que representa el recurso requerido. Se muestran las acciones rápidas:

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

      * Abra la barra de herramientas de componentes seleccionando. Utilice el icono **Editar** (lápiz) para abrir el cuadro de diálogo.
      * Abra el editor en contexto del componente con las funciones Seleccionar y mantener presionadas o Hacer doble clic con el botón lento. Se muestran las acciones disponibles (para algunos componentes se trata de una selección limitada).
      * Para ver todas las acciones disponibles, acceda al modo de pantalla completa mediante:

        ![Botón Pantalla completa](/help/sites-cloud/authoring/assets/full-screen.png)

   * [Configurar las propiedades de un componente existente](/help/sites-cloud/authoring/fundamentals/editing-content.md#component-edit-dialog)

      * Abra la barra de herramientas de componentes seleccionando. Utilice el icono **Configurar** (llave inglesa) para abrir el cuadro de diálogo.

   * [Desplazar un componente](/help/sites-cloud/authoring/fundamentals/editing-content.md#moving-a-component) mediante las siguientes opciones:

      * Arrastre el componente en cuestión a la ubicación nueva.
      * Abra la barra de herramientas de componentes seleccionando. Use los iconos **Cortar** y **Pegar** donde sea necesario.

   * [Copiar (y pegar)](/help/sites-cloud/authoring/fundamentals/editing-content.md#component-toolbar) un componente:

      * Abra la barra de herramientas de componentes seleccionando. Use los iconos **Copiar** y **Pegar** según sea necesario.

   >[!NOTE]
   >
   >Puede **pegar** componentes en la misma página o en otra página. Si pega el componente en una página diferente que ya estaba abierta antes de la operación de cortar o copiar, necesitará actualizar la página.

   * [Eliminar](/help/sites-cloud/authoring/fundamentals/editing-content.md#component-toolbar) un componente:

      * Abra la barra de herramientas de componentes con cualquiera de las opciones seleccionadas y, a continuación, utilice el icono **Eliminar**.

   * [Añadir anotaciones](/help/sites-cloud/authoring/fundamentals/annotations.md#annotations) a la página:

      * Seleccione el modo **Anotar** (icono de burbuja de voz). Añada anotaciones utilizando el icono **Añadir anotación** (signo más). Salga del modo Anotar utilizando la X en la parte superior derecha.

        ![Botón Anotaciones](/help/sites-cloud/authoring/assets/annotations.png)

   * [Vista previa de una página](/help/sites-cloud/authoring/fundamentals/editing-content.md#preview-mode) (para ver cómo aparecerá en el entorno de publicación)

      * Seleccione **Vista previa** en la barra de herramientas.

   * Vuelva al modo de edición (o seleccione otro modo) utilizando **Editar** en el selector desplegable.

   >[!NOTE]
   >
   >Para navegar mediante vínculos en el contenido, debe utilizar el [Modo de vista previa](/help/sites-cloud/authoring/fundamentals/editing-content.md#preview-mode).

### Editar las Propiedades de la página   {#editing-the-page-properties}

Existen dos métodos (principales) para [editar las propiedades de la página](/help/sites-cloud/authoring/fundamentals/page-properties.md):

* Desde la consola **Sitios**:

   1. [Desplácese hasta la página](#finding-your-page) que quiera publicar.
   1. Seleccione el icono **Propiedades** desde:

      * [Acciones rápidas (solo vista de tarjeta y escritorio)](#quick-actions-card-view-desktop-only) para el recurso adecuado.
      * La barra de herramientas cuando [su página se haya seleccionado](#selecting-your-page-for-further-action).

      ![Botón Propiedades](/help/sites-cloud/authoring/assets/properties.png)

   1. Se muestran las propiedades de la página. Puede aplicar actualizaciones según sea necesario y, a continuación, seleccionar Guardar para preservarlas.

* Cuando [edite su página](#editing-your-page-content):

   1. Abra el menú **Información de página**.
   1. Seleccione **Abrir propiedades** para abrir el cuadro de diálogo y editar las propiedades.

      ![Botón Información de página](/help/sites-cloud/authoring/assets/page-information.png)

### Publicar su página (o eliminar la publicación) {#publishing-your-page-or-unpublishing}

Existen dos métodos principales para [publicar la página](/help/sites-cloud/authoring/fundamentals/publishing-pages.md) (y también para eliminar la publicación):

* Desde la consola **Sitios**:

   1. [Desplácese hasta la página](#finding-your-page) que quiera editar.
   1. Seleccione el icono **Publicación rápida** desde:

      * [Acciones rápidas (solo vista de tarjeta y escritorio)](#quick-actions-card-view-desktop-only) para el recurso adecuado.
      * La barra de herramientas cuando su [página se haya seleccionado](#selecting-your-page-for-further-action) (también permite el acceso a [Publicar posteriormente](/help/sites-cloud/authoring/fundamentals/publishing-pages.md)).

      ![Botón Publicación rápida](/help/sites-cloud/authoring/assets/quick-publish.png)

* Cuando [edite la página](#editing-your-page-content):

   1. Abra el menú **Información de página**.
   1. Seleccione **Publicar página**.

* La cancelación de la publicación de una página desde la consola solo se puede realizar mediante la opción **Administrar publicación**, que solo está disponible en la barra de herramientas (no a través de las acciones rápidas).

  ![Botón Administrar publicación](/help/sites-cloud/authoring/assets/manage-publication.png)

  La opción **Cancelar la publicación de páginas** todavía está disponible en el menú **Información de página** en el editor.

  Consulte [Publicación de páginas](/help/sites-cloud/authoring/fundamentals/publishing-pages.md#unpublishing-pages) para obtener más información.

### Mover, copiar y pegar o eliminar su página   {#move-copy-and-paste-or-delete-your-page}

Todas estas acciones pueden activarse del siguiente modo:

1. [Desplácese hasta la página](#finding-your-page) que desea mover, copiar y pegar o eliminar.
1. Seleccione el icono de copiar (y luego pegar), mover o eliminar según sea necesario mediante:

   * [Acciones rápidas (solo vista de tarjeta y escritorio)](#quick-actions-card-view-desktop-only) para el recurso requerido.
   * La barra de herramientas cuando su [página se haya seleccionado](#selecting-your-page-for-further-action).

   A continuación, depende de la acción:

   * [Copiar](/help/sites-cloud/authoring/fundamentals/organizing-pages.md#copying-and-pasting-a-page):

      * Desplácese hasta la nueva ubicación y péguelo allí.

   * [Mover](/help/sites-cloud/authoring/fundamentals/organizing-pages.md#moving-or-renaming-a-page):

      * El asistente se abre para recopilar la información necesaria para mover la página. Siga las instrucciones que aparecen en pantalla.

   * [Eliminar](/help/sites-cloud/authoring/fundamentals/organizing-pages.md#deleting-a-page):

      * Se le solicitará que confirme la acción.

   >[!NOTE]
   >
   >La opción Eliminar no se encuentra disponible como Acción rápida.

### Bloquear y desbloquear su página  {#locking-your-page-then-unlocking}

[Bloquear una página](/help/sites-cloud/authoring/fundamentals/editing-content.md#locking-a-page) impide que otros autores trabajen en ella al mismo tiempo que usted. El icono/botón Bloquear (y Desbloquear) se encuentra en:

* La barra de herramientas cuando su [página se haya seleccionado](#selecting-your-page-for-further-action).
* El menú desplegable [Información de página](#editing-the-page-properties) cuando edita la página.
* Barra de herramientas de la página cuando edita la página (cuando está bloqueada).

Por ejemplo, el icono de bloqueo presenta el siguiente aspecto:

![Botón Bloquear](/help/sites-cloud/authoring/assets/lock.png)

### Acceder a las referencias de la página {#accessing-page-references}

[El acceso rápido a las referencias](/help/sites-cloud/authoring/fundamentals/environment-tools.md#references) hasta/desde una página está disponible en la Barra de referencias.

1. Seleccione **Referencias** mediante el icono de la barra de herramientas (antes o después de [seleccionar su página](#selecting-your-page-for-further-action)): 

   ![Opción de vista Referencias](/help/sites-cloud/authoring/assets/references.png)

   Se muestra una lista de tipos de referencias:

   ![Vista Referencias](/help/sites-cloud/authoring/assets/references-list.png)

1. Seleccione el tipo de referencia necesario para mostrar más detalles y (cuando corresponda) realizar más acciones.

### Crear una versión de su página   {#creating-a-version-of-your-page}

Para crear una [versión](/help/sites-cloud/authoring/features/page-versions.md) de la página:

1. Para abrir el raíl de cronología, seleccione **[Cronología](/help/sites-cloud/authoring/getting-started/basic-handling.md#timeline)** con el icono de la barra de herramientas (antes o después de [seleccionar su página](#selecting-your-page-for-further-action)): 

   ![Opción de vista Cronología](/help/sites-cloud/authoring/assets/timeline.png)

1. Seleccione los puntos suspensivos en la parte inferior derecha de la columna Cronología para mostrar botones adicionales, como **Guardar como versión**.

   ![Vista Cronología](/help/sites-cloud/authoring/assets/timeline-view.png)

1. Seleccione **Guardar como versión**, y después seleccione **Crear**.

### Restablecer o comparar una versión de su página {#restoring-comparing-a-version-of-your-page}

Se utiliza el mismo mecanismo básico cuando se restablecen y/o se comparan versiones de su página:

1. Seleccione **[Línea de tiempo](/help/sites-cloud/authoring/getting-started/basic-handling.md#timeline)** mediante el icono de la barra de herramientas (antes o después de [seleccionar su página](#selecting-your-page-for-further-action)): 

   ![Opción de vista Cronología](/help/sites-cloud/authoring/assets/timeline.png)

   Si ya se ha guardado una versión de su página, se indica en la cronología.

1. Seleccione la versión que desea restaurar. Esto mostrará botones de acción adicionales:

   * **Volver a esta versión**

      * Se restaura la versión.

   * **Mostrar diferencias**

      * La página se abre con las diferencias (entre las dos versiones) resaltadas.
