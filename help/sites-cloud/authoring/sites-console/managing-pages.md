---
title: Administrar páginas
description: Obtenga información sobre cómo administrar las páginas de su sitio web en AEM, como mover, copiar y eliminar.
exl-id: 355b60c5-a82e-4bbb-98ea-bfcc0126b7fd
solution: Experience Manager Sites
feature: Authoring
role: User
source-git-commit: 45805d4baa8b93df2225b44152fee1457b421150
workflow-type: tm+mt
source-wordcount: '1329'
ht-degree: 61%

---

# Administrar páginas {#managing-pages}

Obtenga información sobre cómo administrar las páginas de su sitio web en AEM, como mover, copiar y eliminar.

>[!TIP]
>
>Antes de empezar a administrar las páginas, familiarícese con [la organización de las páginas en AEM](/help/sites-cloud/authoring/sites-console/organizing-pages.md).

>[!TIP]
>
>Hay varios [métodos abreviados de teclado](/help/sites-cloud/authoring/sites-console/keyboard-shortcuts.md) que puede usar desde la consola de sitios web para organizar las páginas de forma más eficaz.

## Privilegios de acceso {#access-privileges}

Su cuenta necesita los derechos de acceso y permisos adecuados para actuar en las páginas, como crear, copiar, mover, eliminar o editar.

Si se producen problemas, le sugerimos que se ponga en contacto con el administrador del sistema.

## Abrir una página para su edición {#opening-a-page-for-editing}

Después de [crear una página](/help/sites-cloud/authoring/sites-console/creating-pages.md) o de navegar a una página existente usando [la consola de **Sites**](/help/sites-cloud/authoring/sites-console/introduction.md), puedes abrirla para editarla.

1. Abra [la consola **Sitios**](/help/sites-cloud/authoring/sites-console/introduction.md).
1. Desplácese hasta encontrar la página que desea editar.
1. Seleccione la página mediante:

   * [Acciones rápidas](/help/sites-cloud/authoring/basic-handling.md#quick-actions)
   * [El modo de selección](/help/sites-cloud/authoring/basic-handling.md#selecting-resources) y la barra de herramientas

1. Toque o haga clic en el icono **Editar**.

   Botón ![Editar](/help/sites-cloud/authoring/assets/edit.png)

1. La página se abre y puede editarla según sea necesario. Dependiendo de cómo se haya creado la página seleccionada, la acción **Editar** abrirá el editor correspondiente.
   * [Editor de páginas](/help/sites-cloud/authoring/page-editor/introduction.md) - Para páginas creadas con el Editor de páginas de AEM
   * [Editor universal](/help/sites-cloud/authoring/universal-editor/authoring.md) - Para páginas creadas con el Editor universal

## Copiar y pegar una página    {#copying-and-pasting-a-page}

Puede copiar una página y todas sus páginas secundarias en una nueva ubicación:

1. Abra [la consola **Sitios**](/help/sites-cloud/authoring/sites-console/introduction.md).
1. Desplácese hasta encontrar la página que desea copiar.
1. Seleccione la página mediante lo siguiente:

   * [Acciones rápidas](/help/sites-cloud/authoring/basic-handling.md#quick-actions)
   * [El modo de selección](/help/sites-cloud/authoring/basic-handling.md#selecting-resources) y la barra de herramientas

1. Toque o haga clic en el icono de página **Copiar**.

   ![Copiar](/help/sites-cloud/authoring/assets/copy.png)

1. Desplácese hasta la ubicación de la copia nueva de la página.
1. Seleccione el icono **Pegar** que se ha puesto a disposición.

   ![Pegar](/help/sites-cloud/authoring/assets/paste.png)

1. El cuadro de diálogo de pegado presenta un resumen de la operación de pegado y las capacidades siguientes:
   * **Nuevo nombre del sitio:** cambie el nombre de la página pegada
   * **Pegar sin elementos secundarios:** omita las páginas secundarias de la página seleccionada al pegar (de forma predeterminada, se pegan)

   ![Cuadro de diálogo de pegado](/help/sites-cloud/authoring/assets/paste-dialog.png)

1. Seleccione el botón **Pegar** para confirmar la operación de pegado y crear las páginas nuevas.

>[!NOTE]
>
>Si copia la página en una ubicación en la que ya existe una página con el mismo nombre que el original, el sistema genera automáticamente una variación del nombre adjuntándole un número. Por ejemplo, si `beach` ya existe, una nueva página con el nombre `beach` se convierte en `beach1`.

>[!NOTE]
>
>Si inicia la acción de pegar en el modo de selección, este se abandona automáticamente en cuanto se copia la página.

## Mover una página o cambiarle el nombre {#moving-or-renaming-a-page}

El procedimiento para mover o cambiar el nombre de una página es básicamente el mismo y ambas acciones las controla el asistente para desplazar páginas. Con este asistente puede:

* Cambiar el nombre de una página sin moverla.
* Mueva la página sin cambiar su nombre.
* Mover y cambiar nombre al mismo tiempo.

AEM le ofrece la funcionalidad de actualizar cualquier vínculo interno que haga referencia a la página que se está moviendo o cambiando de nombre. Esto se puede hacer página por página para proporcionar una flexibilidad total.

1. Abra [la consola **Sitios**](/help/sites-cloud/authoring/sites-console/introduction.md).
1. Desplácese hasta encontrar la página que desea mover.
1. Seleccione la página mediante lo siguiente:

   * [Acciones rápidas](/help/sites-cloud/authoring/basic-handling.md#quick-actions)
   * [El modo de selección](/help/sites-cloud/authoring/basic-handling.md#selecting-resources) y la barra de herramientas

1. Pulse o haga clic en el icono de página **Mover** para abrir el asistente para mover páginas.

   ![Botón Mover](/help/sites-cloud/authoring/assets/move.png)

1. El paso **Rename** del asistente le proporciona **información** sobre la página, incluida la fecha de creación, la ruta y el número de referencias directas. Desde aquí puede hacer lo siguiente:

   * Especifique el nombre que desea que tenga la página cuando se haya movido y, a continuación, seleccione **Siguiente** para continuar.
   * **Haga clic en Cancelar** para anular el proceso.

   ![Mover y cambiar el nombre de la página](/help/sites-cloud/authoring/assets/move-page-rename.png)

   * El nombre de página puede ser el mismo si solo mueve la página.

   >[!NOTE]
   >
   >Si mueve una página a una ubicación en la que ya existe una página con el mismo nombre, el sistema generará automáticamente una variación del nombre adjuntándole un número. Por ejemplo, si `beach` ya existe, una nueva página con el nombre `beach` se convierte en `beach1`.

1. En el paso **Seleccionar destino** del asistente puede:

   * Utilice la [vista de columna](/help/sites-cloud/authoring/basic-handling.md#column-view) para desplazarse a la nueva ubicación de la página:

      * Seleccione el destino haciendo clic en la miniatura de destino.
      * Haga clic en **Siguiente** para continuar.

   * Utilice **Volver** para volver al apartado para especificar el nombre de la página.

   >[!NOTE]
   >
   >De forma predeterminada, el elemento principal de la página que está moviendo o cuyo nombre va a cambiar se selecciona como destino.

   ![Seleccionar destino de movimiento de página](/help/sites-cloud/authoring/assets/move-page-destination.png)

   >[!NOTE]
   >
   >Si mueve una página a una ubicación en la que ya existe una página con el mismo nombre, el sistema generará automáticamente una variación del nombre adjuntándole un número. Por ejemplo, si `winter` ya existe, `winter` se convierte en `winter1`.

1. Si la página está vinculada, si se hace referencia a ella o si se ha publicado, los detalles aparecen en el paso **Ajustar/Volver a publicar**.

   * Puede indicar qué debería ajustarse o volverse a publicar, según proceda.

   >[!NOTE]
   >
   >* Si la página no está vinculada ni se hace referencia a ella, este paso no estará disponible.
   >* En este paso se enumeran las referencias directas e indirectas. Esto puede diferir de la cantidad informada en el paso **Rename** del asistente, así como de las referencias notificadas por el carril de referencias, que solo informan de referencias directas por motivos de rendimiento.

   ![Volver a publicar la página al moverla](/help/sites-cloud/authoring/assets/move-page-republish.png)

1. Pulse o haga clic en **Mover** para definir cuándo se debe producir la acción de mover.

   * **Ahora** almacenará en déclencheur un [trabajo asincrónico](#asynchronous-actions) para mover la página inmediatamente.
   * **Más tarde** le permitirá programar una fecha para que se procese el traslado.

   ![Definir cuándo mover](assets/managing-pages-move-page-now-later.png)

1. Pulse o haga clic en **Continuar** para completar el movimiento de página.

>[!NOTE]
>
>Si la página ya se ha publicado, al mover la página se cancela la publicación automáticamente. De forma predeterminada, se vuelve a publicar una vez finalizado su desplazamiento, pero esto puede cambiar si se desmarca el campo **Volver a publicar** en el paso **Ajustar/volver a publicar**.

>[!NOTE]
>
>Cambiar el nombre de una página también está sujeto a las [Convenciones de nomenclatura de páginas](#page-naming-conventions) al especificar el nuevo nombre de página.

>[!NOTE]
>
>Una página solo se puede mover a una ubicación en la que la plantilla en la que se basa esté permitida. Consulte [Disponibilidad de plantillas](/help/implementing/developing/components/templates.md#template-availability) para obtener más información.

### Acciones asincrónicas {#asynchronous-actions}

Las acciones de movimiento de página siempre se procesan asincrónicamente, lo que permite al usuario continuar la creación en la IU sin impedimentos.

El estado de los trabajos asincrónicos se puede comprobar en [**Estado de los trabajos asincrónicos** panel](/help/operations/asynchronous-jobs.md#monitor-the-status-of-asynchronous-operations) en **Navegación global** > **Herramientas** > **Operaciones** > **Trabajos**

>[!TIP]
>
>Para obtener más información sobre el procesamiento asincrónico de trabajos y cómo configurar el límite para las acciones de mover y cambiar el nombre de la página, consulte el documento [Trabajos asincrónicos](/help/operations/asynchronous-jobs.md) en la guía del usuario Operaciones.

### Eliminar una página {#deleting-a-page}

1. Abra [la consola **Sitios**](/help/sites-cloud/authoring/sites-console/introduction.md).
1. Desplácese hasta la página que desee eliminar.
1. Uso [modo de selección](/help/sites-cloud/authoring/basic-handling.md#viewing-and-selecting-resources) para seleccionar la página requerida, luego utilice **Eliminar** en la barra de herramientas:

   ![Botón Eliminar](/help/sites-cloud/authoring/assets/delete.png)

1. Aparecerá un cuadro de diálogo que le pedirá que confirme la acción.

   ![Cuadro de diálogo Eliminar](/help/sites-cloud/authoring/assets/delete-page.png)

   * **¿Quiere archivar las páginas antes de la eliminación?** Si se selecciona, las versiones de las páginas seleccionadas para su eliminación se crearán al eliminarlas.
      * [Las versiones se pueden restaurar más adelante](/help/sites-cloud/authoring/sites-console/page-versions.md).
      * Las páginas eliminadas sin versiones anteriores no se pueden restaurar.
1. Pulse o haga clic en **Cancelar** para anular la acción o en **Eliminar** para confirmar la acción.
   * Si la página no tiene referencias, se elimina la página.
   * Si la página tiene referencias, un cuadro de mensaje le informará de que se hace referencia a **Una o varias páginas.** Puede seleccionar **Forzar eliminación** o **Cancelar**.

>[!NOTE]
>
>Si la página ya se ha publicado, se cancela su publicación automáticamente antes de eliminarla.

### Bloquear una página   {#locking-a-page}

Puede [bloquear/desbloquear una página](/help/sites-cloud/authoring/page-editor/edit-content.md#locking-a-page) desde una consola o al editar una página individual. La información sobre si una página está bloqueada también se muestra en ambas ubicaciones.

![Botón Bloquear](/help/sites-cloud/authoring/assets/lock.png)
![Botón Desbloquear](/help/sites-cloud/authoring/assets/unlock.png)

### Crear una nueva carpeta {#creating-a-new-folder}

Puede crear carpetas para organizar archivos y páginas.

1. Abra [la consola **Sitios**](/help/sites-cloud/authoring/sites-console/introduction.md).
1. Vaya a la ubicación requerida.
1. Para abrir la lista de opciones, seleccione **Crear** en la barra de herramientas
1. Seleccione **Carpeta** para abrir el cuadro de diálogo. Aquí puede indicar el **Nombre** y el **Título**:

   ![Crear carpeta](/help/sites-cloud/authoring/assets/organizing-create-folder.png)

1. Seleccione **Crear** para crear la carpeta.

>[!NOTE]
>
>* Las carpetas también están sujetas a las [Convenciones de asignación de nombres a páginas](#page-naming-conventions) al especificar el nuevo nombre de carpeta.
>* Las carpetas solo se pueden crear directamente en **Sitios** o en otras carpetas. No se pueden crear en una página.
>* Las acciones estándar mover, copiar, pegar, eliminar, publicar, cancelar publicación y las propiedades de ver/editar se pueden ejecutar en una carpeta.
>* Las carpetas no están disponibles para la selección en una Live Copy.
