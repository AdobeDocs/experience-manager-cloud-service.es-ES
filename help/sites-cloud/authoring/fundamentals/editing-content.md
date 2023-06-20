---
title: Edición del contenido de una página
description: Una vez creada la página, puede editar el contenido para realizar las actualizaciones que requiera
exl-id: 8af0f621-14e8-4605-a51a-a3be21f19092
source-git-commit: 635f4c990c27a7646d97ebd08b453c71133f01b3
workflow-type: tm+mt
source-wordcount: '3004'
ht-degree: 61%

---

# Edición del contenido de una página{#editing-page-content}

Después de crear una página (nueva o como parte de un lanzamiento o Live Copy), puede editar el contenido para realizar las actualizaciones que requiera.

El contenido se añade mediante [componentes](/help/sites-cloud/authoring/features/components-console.md) (apropiado para el tipo de contenido) que se puede arrastrar hasta la página. Después estos se pueden editar local, mover o eliminar.

>[!NOTE]
>
>Su cuenta debe disponer de los privilegios de acceso y los permisos apropiados para editar páginas.
>
>Si se producen problemas, le sugerimos que se ponga en contacto con el administrador del sistema.
<!--
>Your account needs the [appropriate access rights](/help/sites-administering/security.md) and [permissions](/help/sites-administering/security.md#permissions) to edit pages.
-->

>[!NOTE]
>
>Si la página o plantilla se han configurado correctamente, podrá utilizar el [diseño interactivo](/help/sites-cloud/authoring/features/responsive-layout.md) cuando esté editando.

>[!TIP]
>
>En el modo de **edición** puede ver los vínculos en el contenido, pero no puede **acceder** a ellos. Utilice el [modo de vista previa](#previewing-pages) si desea navegar utilizando los vínculos del contenido.

## Barra de herramientas de página {#page-toolbar}

La barra de herramientas de página ofrece acceso a las funciones correspondientes, en función de la configuración de la página.

![Barra de herramientas de página](/help/sites-cloud/authoring/assets/editing-page-toolbar.png)

La barra de herramientas ofrece acceso a numerosas opciones. Según el contexto y la configuración actuales, algunas opciones pueden no estar disponibles.

* **Alternar panel lateral**

  Esto abre o cierra el panel lateral, que contiene el [Explorador de recursos](/help/sites-cloud/authoring/fundamentals/environment-tools.md#assets-browser), [Navegador de componentes](/help/sites-cloud/authoring/fundamentals/environment-tools.md#components-browser), y [Árbol de contenido](/help/sites-cloud/authoring/fundamentals/environment-tools.md#content-tree).

  ![Alternar panel lateral](/help/sites-cloud/authoring/assets/side-panel-toggle.png)

* **Información de la página**

  Proporciona acceso al [Información de página](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-information) menú que incluye detalles de página y acciones que se pueden realizar en la página, incluida la visualización y edición de información de página, la visualización de propiedades de página y la publicación/cancelación de publicación de la página.

  ![Botón Información de página](/help/sites-cloud/authoring/assets/page-information-icon.png)

* **Emulador**

  Alterna el [barra de herramientas del emulador](/help/sites-cloud/authoring/features/responsive-layout.md#selecting-a-device-to-emulate), que se utiliza para emular el aspecto de la página en otro dispositivo. Esto se activa automáticamente en el modo de diseño.

  ![Botón Emulador](/help/sites-cloud/authoring/assets/emulator.png)

* **ContextHub**

  Abre [ContextHub](/help/sites-cloud/authoring/personalization/contexthub.md). Solo está disponible en el modo de vista previa.

  ![Botón Context Hub](/help/sites-cloud/authoring/assets/context-hub.png)

* **Título de página**

  Esto es puramente informativo.

  ![Título de página](/help/sites-cloud/authoring/assets/page-title.png)

* **Selector de modo**

  Muestra el actual [modo](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-modes) y permite seleccionar otro modo, como edición, diseño, deformación de tiempo o segmentación.

  ![Botón Selector de modo](/help/sites-cloud/authoring/assets/mode-selector.png)

* **Vista previa**

  Habilita [modo de previsualización](#preview-mode). Esto muestra la página tal como aparecerá cuando se publique.

  ![Botón Vista previa](/help/sites-cloud/authoring/assets/preview.png)

* **Anotar**

  Permite agregar [anotaciones](/help/sites-cloud/authoring/fundamentals/annotations.md) a la página cuando revise una página. Después de la primera anotación, el icono cambia a un número que indica el número de anotaciones en la página.

  ![Botón Anotación](/help/sites-cloud/authoring/assets/annotations.png)

### Notificación de estado {#status-notification}

Si una página es parte de uno o varios [flujos de trabajo](/help/sites-cloud/authoring/workflows/overview.md), esta información se muestra en una barra de notificación situada en la parte superior de la pantalla cuando edita la página.

![Notificaciones del flujo de trabajo](/help/sites-cloud/authoring/assets/editing-workflow-notification.png)

>[!NOTE]
>
>La barra de estado solo es visible para las cuentas de usuario con los privilegios adecuados.

La notificación enumera el flujo de trabajo que se ejecuta en la página. Si el usuario está implicado en el paso del flujo de trabajo actual, las opciones son [afectar al estado del flujo de trabajo](/help/sites-cloud/authoring/workflows/participating.md) y también dispone de más información sobre el flujo de trabajo, como:

* **Completar**: abre el cuadro de diálogo **Completar elemento de trabajo**.
* **Delegar**: abre el cuadro de diálogo **Completar elemento de trabajo**.
* **Ver detalles**: abre la ventana **Detalles** del flujo de trabajo.

Completar y delegar los pasos del flujo de trabajo mediante la barra de notificaciones funciona igual que al [participar en flujos de trabajo](/help/sites-cloud/authoring/workflows/participating.md) desde la bandeja de entrada de notificaciones.

Si la página está sujeta a varios flujos de trabajo, el número de los mismos se muestra en el extremo derecho de la notificación, junto a dos botones de flecha que permiten desplazarse por los flujos de trabajo.

![Varias notificaciones del flujo de trabajo](/help/sites-cloud/authoring/assets/editing-workflow-notification-multiple.png)

## Marcador de posición de componente {#component-placeholder}

El marcador de posición de componente es un indicador que muestra dónde se coloca un componente al soltarlo, sobre el componente sobre el que está pasando el ratón actualmente.

* Al añadir un componente nuevo a la página (arrastrando desde el explorador de componentes):

  ![Marcador de posición al añadir un componente nuevo a una página](/help/sites-cloud/authoring/assets/editing-component-placeholder.png)

* Al mover un componente existente:

  ![Marcador de posición al mover un componente ya existente en una página](/help/sites-cloud/authoring/assets/editing-component-placeholder-existing.png)

## Insertar un componente {#inserting-a-component}

### Inserción de un componente desde el navegador de componentes {#inserting-a-component-from-the-components-browser}

Puede seleccionar un componente nuevo mediante el [navegador de componentes](/help/sites-cloud/authoring/fundamentals/environment-tools.md#components-browser). El [marcador de posición de componente](#component-placeholder) muestra dónde se encuentra el componente:

1. Asegúrese de que la página se encuentra en el modo de [**edición**.](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-modes)
1. Abra el [navegador de componentes](/help/sites-cloud/authoring/fundamentals/environment-tools.md#components-browser).
1. Arrastre el componente en cuestión hasta la [posición deseada](#component-placeholder).
1. [Editar](#edit-content) el componente.

>[!NOTE]
>
>En un dispositivo móvil, el navegador de componentes llenará toda la pantalla. Una vez que comience a arrastrar un componente, el explorador se cerrará para mostrar de nuevo la página y así poder colocar el componente.

### Inserción de un componente desde el sistema de párrafos {#inserting-a-component-from-the-paragraph-system}

Puede agregar un componente nuevo mediante el cuadro **Arrastrar componentes aquí** del sistema de párrafos:

1. Asegúrese de que la página se encuentra en el modo de [**edición**.](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-modes)
1. Existen dos formas de seleccionar y agregar un componente nuevo desde el sistema de párrafos:

   * Seleccione el **Insertar componente** opción (+) de la barra de herramientas de un componente existente o de la **Arrastre los componentes aquí** cuadro.

     ![Insertar un componente](/help/sites-cloud/authoring/assets/editing-insert-component.png)

   * En un dispositivo de escritorio puede hacer doble clic en el cuadro **Arrastrar componentes aquí**.

   * Se abrirá el cuadro de diálogo **Insertar nuevo componente** para que pueda seleccionar el componente requerido: 

     ![Cuadro de diálogo Insertar nuevo componente](/help/sites-cloud/authoring/assets/editing-insert-component-selection.png)

1. El componente seleccionado se añade en la parte inferior de la página. [Editar](#edit-content) Seleccione el componente según sea necesario.

### Inserción de un componente mediante el navegador de recursos   {#inserting-a-component-using-the-assets-browser}

También puede agregar un componente nuevo a la página arrastrando un recurso desde el [explorador de recursos](/help/sites-cloud/authoring/fundamentals/environment-tools.md#assets-browser). Esto creará automáticamente un nuevo componente del tipo adecuado (y que contenga el recurso).

Puede configurar este comportamiento en su instalación. Para obtener más detalles, consulte Configurar un sistema de párrafos de manera que, al arrastrar un activo, se cree una instancia de componente. <!--This behavior can be configured for your installation. See [Configuring a Paragraph System so that Dragging an Asset Creates a Component Instance](/help/sites-developing/developing-components.md#configuring-a-paragraph-system-so-that-dragging-an-asset-creates-a-component-instance) for further details.-->

Para crear un componente arrastrando uno de los tipos de activo anteriores:

1. Asegúrese de que la página se encuentra en el modo de [**edición**.](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-modes)
1. Abra el [explorador de recursos](/help/sites-cloud/authoring/fundamentals/environment-tools.md#assets-browser).
1. Arrastre el recurso en cuestión a la posición deseada. El [marcador de posición de componente](#component-placeholder) muestra dónde se encuentra el componente.

   Se crea un componente, adecuado para el tipo de recurso, en la ubicación requerida; contiene el recurso seleccionado.

1. [Editar](#edit-content) el componente, si es necesario.

>[!NOTE]
>
>En un dispositivo móvil, el explorador de recursos rellenará toda la pantalla. Una vez que comience a arrastrar un recurso, el explorador se cerrará para mostrar de nuevo la página y poder colocarlo.

Si al examinar los recursos descubre que necesita realizar algún cambio rápido en alguno de ellos, puede iniciar el [editor de recursos](/help/assets/manage-digital-assets.md) directamente desde el explorador, haciendo clic en el icono de edición situado junto al nombre del recurso.

![Botón Editar recursos](/help/sites-cloud/authoring/assets/asset-edit-button.png)

## Barra de herramientas del componente {#component-toolbar}

Si se selecciona un componente, se abrirá la barra de herramientas, que proporciona acceso a distintas acciones que se pueden realizar en el componente.

Las acciones disponibles para el usuario se muestran según corresponda y es posible que no todas las acciones se describan aquí.

![Barra de herramientas del componente](/help/sites-cloud/authoring/assets/editing-component-toolbar.png)

* **Editar**

  [Depende del tipo de componente](/help/sites-cloud/authoring/fundamentals/components.md), esto le permite [editar el contenido del componente](#edit-content). A menudo se proporciona una barra de herramientas.

  Botón ![Editar](/help/sites-cloud/authoring/assets/editing-component-toolbar-edit.png)

* **Configurar**

  [Depende del tipo de componente](/help/sites-cloud/authoring/fundamentals/components.md), esto permite editar y configurar las propiedades del componente. A menudo se abre un cuadro de diálogo.

  ![Botón Configurar](/help/sites-cloud/authoring/assets/editing-component-toolbar-configure.png)

* **Copiar**

  Esto copiará el componente en el portapapeles. Después de la acción de pegar, el componente original se mantiene.

  ![Botón Copiar](/help/sites-cloud/authoring/assets/editing-component-toolbar-copy.png)

* **Cortar**

  Esto copiará el componente en el portapapeles. Después de la acción de pegar, se quita el componente original.

  ![Botón Cortar](/help/sites-cloud/authoring/assets/editing-component-toolbar-cut.png)

* **Eliminar**

  Esto eliminará el componente de la página con su confirmación.

  ![Botón Eliminar](/help/sites-cloud/authoring/assets/editing-component-toolbar-delete.png)

* **Insertar componente**

  Esto abre el cuadro de diálogo a [añadir un componente nuevo](/help/sites-cloud/authoring/fundamentals/editing-content.md#inserting-a-component-from-the-paragraph-system).

  ![Botón Insertar](/help/sites-cloud/authoring/assets/editing-component-toolbar-insert.png)

* **Pegar**

  Esto pegará el componente del portapapeles en la página. Si el original permanece, depende de si ha utilizado copiar o cortar.

   * Puede pegar en la misma página o en otra página.
   * El elemento pegado se pegará encima del elemento donde seleccione la acción de pegado.
   * La acción Pegar solo se mostrará si hay contenido en el portapapeles.

  ![Botón Pegar](/help/sites-cloud/authoring/assets/editing-component-toolbar-paste.png)

  >[!NOTE]
  >
  >Si pega en una página diferente que ya estaba abierta antes de la operación de cortar o copiar, debe actualizar la página para ver el contenido pegado.

* **Grupo**

  Esto le permite seleccionar varios componentes a la vez. En un dispositivo de escritorio puede conseguir lo mismo haciendo **Control + clic** o **Comando + clic**.

  ![Botón Agrupar](/help/sites-cloud/authoring/assets/editing-component-toolbar-group.png)

* **Principal**

  Permite seleccionar el componente principal del componente seleccionado.

  ![Botón Principal](/help/sites-cloud/authoring/assets/editing-component-toolbar-parent.png)

* **Diseño**

  Esto le permite modificar el [layout](/help/sites-cloud/authoring/fundamentals/editing-content.md#edit-component-layout) del componente seleccionado. Esto solo se aplica al componente seleccionado y no activa el [Modo Diseño](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-modes) para toda la página.

  ![Botón Diseño](/help/sites-cloud/authoring/assets/editing-component-toolbar-layout.png)

* **Conversión en una variación de fragmento de experiencia**

  Esto permite crear un nuevo [fragmento de experiencia](/help/sites-cloud/authoring/fundamentals/experience-fragments.md) a partir del componente seleccionado o añadirlo a un fragmento de experiencia. 

  ![Convertir para el botón Fragmentos de experiencias](/help/sites-cloud/authoring/assets/editing-component-toolbar-xf.png)

## Editar contenido {#edit-content}

Hay dos métodos para añadir y/o editar contenido en los componentes:

* Abra el [cuadro de diálogo de componentes para editar](#component-edit-dialog).
* [Arrastrar y soltar un recurso](#drag-and-drop-assets-into-component) desde el explorador de recursos para añadir contenido directamente.

### Cuadro de diálogo de edición de contenido   {#component-edit-dialog}

Puede abrir un componente para editar el contenido mediante el icono [Editar (lápiz) de la barra de herramientas](#component-toolbar) del componente.

Las opciones de edición exactas dependerán del componente. Para algunos componentes [todas las acciones solo estarán disponibles en modo de pantalla completa](#edit-content-full-screen-mode). Por ejemplo:

* Componente de texto

  ![Barra de herramientas del componente de texto](/help/sites-cloud/authoring/assets/editing-text-component-toolbar.png)

* Componente de imagen

  ![Barra de herramientas del componente de imagen](/help/sites-cloud/authoring/assets/editing-image-component-toolbar.png)

  >[!NOTE]
  >
  >La edición no funciona con un componente de imagen vacío.
  >
  >Debe arrastrar o cargar una imagen al componente para poder iniciar la edición.

* Componente de imagen: pantalla completa

  [La introducción del modo de pantalla completa](#edit-content-full-screen-mode) para el componente de imagen permite disponer de más espacio para editar la imagen y mostrar opciones de edición adicionales como **Iniciar mapa** y **Restablecer zoom**. Además, la pantalla completa permite seleccionar ajustes preestablecidos de recorte.

  ![Modo de pantalla completa del componente de imagen](/help/sites-cloud/authoring/assets/editing-image-component-full-screen.png)

* Los componentes construidos a partir de más de un componente básico primero le piden que confirme qué conjunto de opciones de edición desea utilizar:

### Arrastrar y colocar recursos en un componente {#drag-and-drop-assets-into-component}

Para tipos de componentes específicos (como imágenes) puede arrastrar y colocar recursos del explorador de recursos directamente en el componente para actualizar el contenido.

## Editar contenido: modo de pantalla completa {#edit-content-full-screen-mode}

Se puede acceder y salir del modo de pantalla completa de todos los componentes con la siguiente opción:

![Botón Pantalla completa](/help/sites-cloud/authoring/assets/editing-full-screen.png)

Por ejemplo, el componente **Texto**:

![Componente de texto en pantalla completa](/help/sites-cloud/authoring/assets/editing-text-full-screen.png)

>[!NOTE]
>
>Para algunos componentes, el modo de pantalla completa tendrá más opciones disponibles que el editor local básico.

## Mover un componente {#moving-a-component}

Para mover un componente de párrafo:

1. Seleccione el párrafo que desea mover pulsando y manteniendo pulsado o pulsando y manteniendo pulsado.
1. Arrastre el párrafo a la nueva ubicación. AEM Indica dónde se puede depositar el párrafo. Colóquelo en la ubicación que desee.

   ![Mover un componente](/help/sites-cloud/authoring/assets/editing-moving-component.png)

1. Se mueve el párrafo.

>[!TIP]
>
>También puede utilizar [Cortar y pegar](#component-toolbar) para mover un componente.

## Editar diseño de componente {#edit-component-layout}

En vez de pasar repetidamente de la edición al [modo de diseño](/help/sites-cloud/authoring/features/responsive-layout.md) para ajustar un componente, puede seleccionar la acción **Diseño** del mismo. Podrá cambiar su diseño sin tener que abandonar el modo de edición, por lo que ahorrará tiempo.

1. En el modo de **edición** de la consola del sitio, si se selecciona un componente, aparece su barra de herramientas.

   ![La barra de herramientas de componentes de un componente de página](/help/sites-cloud/authoring/assets/editing-layout-toolbar.png)

   Pulse o haga clic en la acción **Diseño** para ajustar el diseño del componente.

   ![Botón Diseño de la barra de herramientas de componentes](/help/sites-cloud/authoring/assets/editing-component-toolbar-layout.png)

1. Una vez seleccionada la acción Diseño:

   * Se muestran los controladores de tamaño del componente.
   * La barra de herramientas del emulador se muestra en la parte superior de la pantalla.
   * Las acciones de diseño en lugar de las acciones de edición estándar se muestran en la barra de herramientas de componentes.

   ![Un componente en modo de diseño](/help/sites-cloud/authoring/assets/editing-layout-mode.png)

   Ahora puede modificar el diseño del componente como haría en el [modo de diseño](/help/sites-cloud/authoring/features/responsive-layout.md#defining-layouts-layout-mode).

1. Después de realizar los cambios necesarios, haga clic en el botón **Cerrar** del menú de acciones del componente para detener la edición del diseño. La barra de herramientas del componente recuperará su estado de edición normal.

   ![La barra de herramientas de componentes de un componente de página](/help/sites-cloud/authoring/assets/editing-layout-exit.png)

>[!TIP]
>
>El ámbito de la acción Diseño se reduce al componente seleccionado. Por ejemplo, si está editando el diseño de un componente y hace clic en otro componente, se mostrará la barra de herramientas de edición estándar del componente recién seleccionado (no la barra de herramientas de diseño) y desaparecerán tanto los controles de cambio de tamaño como la barra de herramientas del emulador.
>
>Si necesita editar el diseño general de la página y modificar múltiples componentes, cambie al [modo de diseño](/help/sites-cloud/authoring/features/responsive-layout.md).

## Componentes heredados {#inherited-components}

La herencia es el mecanismo por el que el contenido se puede insertar automáticamente de un componente a otro. Los componentes heredados pueden ser el producto de distintos escenarios, como por ejemplo:

* [Administración de varios sitios](/help/sites-cloud/administering/msm/overview.md)
* [Lanzamientos](/help/sites-cloud/authoring/launches/overview.md) (cuando se basan en una Live Copy).

Puede cancelar (y volver a habilitar) la herencia. Según el componente, esto puede estar disponible en la barra de herramientas del componente, si el componente está en una página que forma parte de una Live Copy o Launch (basado en una Live Copy).

![Una barra de herramientas de componentes que muestra la relación de herencia](/help/sites-cloud/authoring/assets/editing-component-toolbar-inheritance.png)

Por ejemplo:

* Cancelar herencia

  ![Botón Cancelar herencia](/help/sites-cloud/authoring/assets/editing-cancel-inheritance.png)

* Volver a habilitar la herencia (si la herencia se ha cancelado)

  ![Botón Volver a activar herencia](/help/sites-cloud/authoring/assets/editing-reenable-inheritance.png)

* La acción de despliegue también está disponible en el modelo o en el origen de Live Copy.

  ![Botón Desplegar](/help/sites-cloud/authoring/assets/editing-rollout.png)

## Edición de las plantilla de página {#editing-the-page-template}

Puede cambiar fácilmente al [editor de plantillas](/help/sites-cloud/authoring/features/templates.md#editing-templates-template-authors) seleccionando **Editar plantilla** en el menú [Información de página](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-information).

Puede ver fácilmente en qué plantilla se basa la página al seleccionar la página en la vista [Columna](/help/sites-cloud/authoring/getting-started/basic-handling.md#column-view) o en la [vista Lista](/help/sites-cloud/authoring/getting-started/basic-handling.md#list-view).

## Estado de Live Copy   {#live-copy-status}

El [Modo de página Estado de Live Copy](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-modes) permite obtener una descripción general rápida del estado de live copy y de los componentes que se heredan o no:

* Borde verde: heredado
* Borde rosa: se ha cancelado la herencia

Por ejemplo:

![Ejemplo del estado de la Live Copy que se muestra](/help/sites-cloud/authoring/assets/editing-live-copy-status.png)

## Agregar anotaciones {#adding-annotations}

[Anotaciones](/help/sites-cloud/authoring/fundamentals/annotations.md) permite que los revisores y otros autores proporcionen comentarios sobre el contenido. A menudo se utilizan con fines de revisión y validación.

## Previsualizar páginas   {#previewing-pages}

Existen dos métodos para visualizar la vista previa de una página:

* [Modo de vista previa](#preview-mode): una vista previa rápida y en el sitio
* [Ver como aparece publicado](#view-as-published) : una vista previa completa que abre la página en una nueva pestaña

>[!TIP]
>
>* Los vínculos del contenido son visibles, pero no se puede acceder a ellos en el modo de edición.
>* Utilice cualquiera de las opciones de vista previa si desea navegar mediante sus vínculos.
>* Utilice el [atajo de teclado](/help/sites-cloud/authoring/getting-started/keyboard-shortcuts.md) `Ctrl-Shift-M` para cambiar entre la vista previa y el último modo seleccionado.

>[!NOTE]
>
>La cookie del modo WCM está establecida para las dos opciones.

### Modo de vista previa {#preview-mode}

Al editar contenido, puede obtener una vista previa de la página mediante la vista previa [modo](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-modes). Este modo:

* Oculta los distintos mecanismos de edición para ofrecerle una vista rápida del aspecto que tendrá la página cuando se publique.
* Permite utilizar vínculos para navegar.
* Does **no** actualice el contenido de la página.

Durante la creación, el modo de vista previa está disponible mediante el icono situado en la parte superior derecha del editor de páginas:

![Botón Vista previa](/help/sites-cloud/authoring/assets/preview.png)

### Ver como aparece publicado {#view-as-published}

El **Ver como aparece publicado** La opción está disponible en [Información de página](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-information) menú. Esta opción abre la página en una nueva pestaña, actualiza el contenido y muestra la página exactamente como aparecerá en el entorno de publicación.

## Bloquear una página   {#locking-a-page}

AEM le permite bloquear páginas para que nadie más pueda modificar su contenido. Esta función es útil cuando realice muchas ediciones en una página concreta o cuando tenga que congelar una página durante un rato.

Las páginas se pueden bloquear desde las ubicaciones siguientes:

* consola **Sitios**

   1. Seleccione la página con [modo de selección](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources).
   1. Seleccione el icono de bloqueo.

      ![Botón Bloquear](/help/sites-cloud/authoring/assets/lock.png)

* **Editor de página**

   1. Seleccione el **Información de página** para abrir el menú.
   1. Seleccione el **Bloquear página** opción.

Una vez bloqueada, se actualiza la información de la vista de la consola y, al editar, se muestra un símbolo de bloqueo en la barra de herramientas.

![Ejemplo de página bloqueada](/help/sites-cloud/authoring/assets/editing-locked-page.png)

>[!CAUTION]
>
>El bloqueo de páginas se puede realizar al suplantar a un usuario. Sin embargo, una página bloqueada de esta forma solo puede desbloquearse (por clientes) con el usuario que se ha suplantado.
>
>Las páginas no se pueden desbloquear al suplantar al usuario que ha bloqueado la página.
>
>Si el usuario que bloqueó la página no está disponible para desbloquearla, póngase en contacto con Asistencia al cliente para evaluar las opciones para quitar el bloqueo.

## Desbloquear una página {#unlocking-a-page}

Desbloquear una página es muy similar a [bloquearla](#locking-a-page). Cuando una página está bloqueada, las opciones de bloqueo se sustituyen con las acciones de desbloqueo.

El menú Información de página muestra la opción **Desbloquear** y el icono Bloquear de la consola Sitios se reemplaza con el icono **Desbloquear**.

![Botón Desbloquear](/help/sites-cloud/authoring/assets/unlock.png)

>[!CAUTION]
>
>El bloqueo de páginas se puede realizar al suplantar a un usuario. Sin embargo, una página bloqueada de este modo solo se puede desbloquear (por clientes) utilizando el usuario que se ha suplantado.
>
>Las páginas no se pueden desbloquear al suplantar al usuario que ha bloqueado la página.
>
>Si el usuario que bloqueó la página no está disponible para desbloquearla, póngase en contacto con Asistencia al cliente para evaluar las opciones para quitar el bloqueo.

<!--
>[!CAUTION]
>
>Locking a page can be performed when impersonating a user. However a page locked in this way can only then be unlocked by the user who was impersonated, or by a user with admin rights (a member of AEM Administrator IMS profile).
>
>Pages can not be unlocked by impersonating the user who locked the page.
-->

<!--
>Locking a page can be performed when [impersonating a user](/help/sites-administering/security.md#impersonating-another-user). However a page locked in this way can only then be unlocked by the user who was impersonated or by the admin user.
-->

## Deshacer y rehacer modificaciones de páginas {#undoing-and-redoing-page-edits}

Los iconos siguientes le permiten deshacer o rehacer una acción. Se muestran en la barra de herramientas cuando corresponde:

![Botones Deshacer y Rehacer](/help/sites-cloud/authoring/assets/redo.png)

>[!TIP]
>
>* También dispone del [atajo de teclado](/help/sites-cloud/authoring/getting-started/keyboard-shortcuts.md) `Ctrl-Z` para deshacer las acciones de edición de página.
>* También dispone del atajo de teclado `Ctrl-Y` para rehacer las acciones de edición de página.

>[!NOTE]
>
>Consulte [Deshacer y rehacer ediciones de página: la teoría](#undoing-and-redoing-page-edits-the-theory) para ver toda la información sobre las posibilidades de deshacer y rehacer ediciones de página.

## Deshacer y rehacer ediciones de página: la teoría {#undoing-and-redoing-page-edits-the-theory}

AEM almacena un historial de las acciones que realiza y la secuencia en que las realizó, de modo que puede deshacer varias acciones en el orden en que se realizaron, y también rehacerlas para volver a aplicar una o más acciones.

Si hay un elemento seleccionado en la página de contenido (por ejemplo, un componente de texto), el comando para deshacer o rehacer se aplica a dicho elemento.

El comportamiento de los comandos Deshacer y Rehacer es similar al de otros programas. Utilice los comandos para restaurar el estado reciente de la página web a medida que toma decisiones sobre el contenido. Por ejemplo, si mueve un párrafo de texto a una ubicación diferente en la página, puede usar el comando Deshacer para mover el párrafo a la posición original. Si, a continuación, decide que la posición anterior es mejor, utilice el comando Rehacer para &quot;deshacer la operación de deshacer&quot;.

Por ejemplo, puede:

* Rehacer acciones siempre que no haya realizado una edición de página desde que utilizó Deshacer.
* Deshacer un máximo de 20 acciones de edición (configuración predeterminada).
* También utilice [Métodos abreviados del teclado](/help/sites-cloud/authoring/getting-started/keyboard-shortcuts.md) para deshacer y rehacer.

Puede utilizar las funciones Deshacer y Rehacer para los siguientes tipos de cambios de página:

* Adición, edición, eliminación y movimiento de párrafos
* Edición in situ del contenido del párrafo
* Copiar, cortar y pegar elementos dentro de una página

>[!NOTE]
>
>* Se necesitan permisos especiales para deshacer y rehacer cambios en archivos e imágenes.
>* El historial de cambios en archivos e imágenes dura un mínimo de diez horas. Sin embargo, más allá de este tiempo, no se garantiza la anulación de los cambios. El administrador puede cambiar el tiempo predeterminado de diez horas.
>* El administrador del sistema puede configurar varios aspectos de las funciones de Deshacer/Rehacer según los requisitos de la instancia.
<!--* Your system administrator can [configure various aspects of the Undo/Redo features](/help/sites-administering/config-undo.md) according to the requirements for your instance.-->
