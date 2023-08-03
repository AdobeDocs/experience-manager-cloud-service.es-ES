---
title: Uso de versiones de página
description: AEM Obtenga información sobre cómo crear, comparar y restaurar versiones de sus páginas en la administración de segmentos de página en la administración de segmentos de la página de.
exl-id: 33d8e43c-594d-4bba-9631-b2c42a1e910f
source-git-commit: 31e6ec8e9977c8787e14481ee3a94df767262aec
workflow-type: tm+mt
source-wordcount: '1507'
ht-degree: 36%

---

# Uso de versiones de página   {#working-with-page-versions}

El control de versiones crea una &quot;captura de pantalla&quot; de una página en un momento específico. Con el control de versiones, puede realizar las siguientes acciones:

* Cree una versión de una página.
* Restablezca una versión anterior de una o varias páginas para:
   * Deshacer los cambios realizados en las páginas.
   * Restaurar páginas eliminadas.
   * Restaurar un árbol (a una fecha y hora especificadas).
* Previsualizar una versión.
* Comparar la versión actual de una página con una versión anterior.
   * Se resaltan las diferencias entre el texto y las imágenes.
* La deformación de tiempo emplea las versiones de página para determinar el estado del entorno de publicación.

## Creación de una nueva versión   {#creating-a-new-version}

Puede crear una versión de su recurso desde:

* el [raíl de la cronología](#creating-a-new-version-timeline)
* la opción [Crear](#creating-a-new-version-create-with-a-selected-resource) (cuando hay un recurso seleccionado)

### Crear una nueva versión: línea de tiempo {#creating-a-new-version-timeline}

1. Desplácese hasta mostrar la página para la que desea crear una versión.
1. Seleccione la página en [modo de selección](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources).
1. Abra el raíl **Cronología**.
1. Pulse o haga clic en los puntos suspensivos junto al campo de comentarios para mostrar las opciones:

   ![Versiones en el reíl de la cronología](/help/sites-cloud/authoring/assets/versions-timeline-rail.png)

1. Seleccionar **Guardar como versión**.
1. Introduzca una **Etiqueta** y **Comentario**, si es necesario.

   ![Añadir etiqueta para una versión](/help/sites-cloud/authoring/assets/versions-add-label.png)

1. Confirme la nueva versión con **Crear**.

   La información de la cronología se actualiza para indicar la nueva versión.

### Crear una nueva versión: creación con un recurso seleccionado {#creating-a-new-version-create-with-a-selected-resource}

1. Desplácese hasta mostrar la página para la que desea crear una versión.
1. Seleccione la página en [modo de selección](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources).
1. Seleccione el **Crear** de la barra de herramientas.
1. Se abre el mismo cuadro de diálogo. Puede introducir un **Etiqueta** y una **Comentario**, si es necesario.
1. Confirme la nueva versión con **Crear**.

La cronología se abre con la información actualizada para indicar la nueva versión.

## Restablecimiento de versiones {#reinstating-versions}

Una vez creada una versión de la página, existen varios métodos para restablecer una versión anterior:

* la opción **Revertir a esta versión** del carril [Cronología](/help/sites-cloud/authoring/getting-started/basic-handling.md#timeline)

  Restablezca una versión anterior de una página seleccionada.

* las opciones **Restaurar** de la parte superior de la [barra de herramientas acciones](/help/sites-cloud/authoring/getting-started/basic-handling.md#actions-toolbar)

   * **Restaurar versión**

     Restablecer versiones de páginas especificadas dentro de la carpeta seleccionada actualmente. También puede incluir la restauración de páginas que se han eliminado anteriormente.

   * **Restaurar árbol**

     Restablecer una versión de todo un árbol en una fecha y hora especificadas. También puede incluir páginas que se han eliminado anteriormente.

>[!NOTE]
>
>Al restablecer una página, la versión creada forma parte de una rama nueva.
>
>Como ejemplo:
>
>1. Cree una versión de una página cualquiera.
>1. Las etiquetas y los nombres de nodo iniciales son 1.0, 1.1, 1.2, etc.
>1. Restablezca la primera versión; es decir, 1.0.
>1. Vuelva a crear versiones.
>1. Las etiquetas y los nombres de nodo generados ahora son 1.0.0, 1.0.1, 1.0.2, etc.

### Volver a esta versión {#revert-to-a-version}

Hasta **Revertir** la página seleccionada a una versión anterior:

1. Desplácese hasta mostrar la página que desea revertir a una versión anterior.
1. Seleccione la página en [modo de selección](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources).
1. Abra la columna **Cronología** y seleccione **Mostrar todo** o **Versiones**. Se muestran las versiones de página de la página seleccionada.
1. Seleccione la versión a la que desea revertir. Se muestran las opciones posibles:

   ![Volver a esta versión](/help/sites-cloud/authoring/assets/versions-revert.png)

1. Seleccionar **Volver a esta versión**. La versión seleccionada se restaura y la información de la cronología se actualiza.

### Restaurar versión {#restore-version}

Este método se puede utilizar para restaurar versiones de páginas especificadas dentro de la carpeta actual. También puede incluir la restauración de páginas que se han eliminado anteriormente:

1. Vaya a, y [seleccione](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources), la carpeta requerida.

1. Seleccione **Restaurar**, luego **Restaurar versión** desde la parte superior de la [barra de herramientas acciones](/help/sites-cloud/authoring/getting-started/basic-handling.md#actions-toolbar).

   >[!NOTE]
   >
   >Si tiene:
   >
   >* seleccionó una sola página que nunca ha tenido páginas secundarias,
   >* o ninguna de las páginas de la carpeta tiene versiones,
   >
   >La pantalla está vacía porque no hay versiones aplicables.

1. Se muestran las versiones disponibles:

   ![Restaurar versión: lista de todas las páginas de la carpeta](/help/sites-cloud/authoring/assets/versions-restore-version-01.png)

1. Para una página específica, utilice el selector desplegable en **RESTAURAR A LA VERSIÓN** para seleccionar la versión requerida para esa página.

   ![Restaurar versión: seleccionar versión](/help/sites-cloud/authoring/assets/versions-restore-version-02.png)

1. En la pantalla principal, seleccione la página requerida para la restauración:

   ![Restaurar versión: seleccionar página](/help/sites-cloud/authoring/assets/versions-restore-version-03.png)

1. Seleccione **Restaurar** para la versión seleccionada, de la página seleccionada, que se restaurará como la versión actual.

>[!NOTE]
>
>El orden en que se selecciona una página requerida y la versión relacionada son intercambiables.

### Restaurar árbol {#restore-tree}

Este método se puede utilizar para restaurar una versión de un árbol en una fecha y hora especificadas. Puede incluir páginas que se han eliminado anteriormente:

1. Vaya a, y [seleccione](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources), la carpeta requerida.

1. Seleccione **Restaurar**, luego **Restaurar árbol** desde la parte superior de la [barra de herramientas acciones](/help/sites-cloud/authoring/getting-started/basic-handling.md#actions-toolbar). Se muestra la última versión del árbol:

   ![Restaurar árbol](/help/sites-cloud/authoring/assets/versions-restore-tree-01.png)

1. Utilice el selector de fecha y hora en **Últimas versiones a la fecha** para que pueda seleccionar otra versión del árbol: la que se va a restaurar.

1. Establecer el indicador **Conservar páginas sin versiones** según sea necesario:

   * Si está activo (seleccionado), las páginas sin versiones se mantienen y no se ven afectadas por la restauración.

   * Si está inactivo (sin seleccionar), las páginas sin versiones se eliminarán, ya que no existían en el árbol con versiones.

1. Seleccione **Restaurar** para que la versión seleccionada del árbol se restaure como la versión *actual*.

## Vista previa de una versión   {#previewing-a-version}

Puede obtener una vista previa de una versión específica:

1. Desplácese hasta mostrar la página que desea comparar.
1. Seleccione la página en [modo de selección](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources).
1. Abra la columna **Línea de tiempo** y seleccione **Mostrar todo** o **Versiones**.
1. Se muestran las versiones de la página. Seleccione la versión que desee previsualizar:

   ![Previsualizar versión](/help/sites-cloud/authoring/assets/versions-revert.png)

1. Seleccionar **Previsualizar**. La página se muestra en una nueva pestaña.

   >[!CAUTION]
   >
   >Si se ha movido una página, ya no puede realizar una previsualización de ninguna versión realizada antes del movimiento.
   >
   >Si tiene problemas con una vista previa, consulte la [Cronología](/help/sites-cloud/authoring/getting-started/basic-handling.md#timeline) para que la página vea si la página se ha movido.

## Comparar una versión con la página actual {#comparing-a-version-with-current-page}

Para comparar una versión anterior con la página actual:

1. Desplácese hasta mostrar la página que desea comparar.
1. Seleccione la página en [modo de selección](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources).
1. Abra la columna **Línea de tiempo** y seleccione **Mostrar todo** o **Versiones**.
1. Se muestran las versiones de la página. Seleccione la versión que desea comparar:

   ![Comparar versiones](/help/sites-cloud/authoring/assets/versions-revert.png)

1. Seleccionar **Comparar con actual**. El [diferencia de página](/help/sites-cloud/authoring/features/page-diff.md) se abre y muestra las diferencias.

## Deformación de tiempo   {#timewarp}

Deformación de tiempo es una función diseñada para simular el estado *publicado* de una página en periodos específicos en el pasado.

>[!TIP]
>
>[La Deformación de tiempo también se puede utilizar con Lanzamientos para previsualizar el futuro](/help/sites-cloud/authoring/launches/preview.md).

Dado que la creación de contenido es un proceso continuo y colaborativo, el propósito de Deformación de tiempo es permitir que los autores rastreen el sitio web publicado con el paso del tiempo para que puedan comprender cómo ha cambiado el contenido. Esta función emplea las versiones de página para determinar el estado del entorno de publicación.

Para usar esta función, haga lo siguiente:

* El sistema busca la versión de página que estaba activa en el momento seleccionado.
* Significa que la versión mostrada se creó o activó *antes* el punto temporal seleccionado en Deformación de tiempo.
* Al navegar a una página que se haya eliminado, también se procesa, siempre que las versiones anteriores de la página estén disponibles en el repositorio.
* Si no se encuentra ninguna versión publicada, Deformación de tiempo vuelve al estado actual de la página en el entorno de creación (el motivo es evitar una página de error/404, lo que impediría el examen).

### Utilizar la Deformación de tiempo {#using-timewarp}

Deformación de tiempo es un [modo](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-modes) del editor de páginas. Para iniciarlo, simplemente cámbielo como lo haría con cualquier otro modo.

1. Inicie el editor de la página donde desea iniciar Deformación de tiempo y, a continuación, seleccione **Deformación de tiempo** en la selección de modo.

   ![Modo Deformación de tiempo](/help/sites-cloud/authoring/assets/versions-timewarp-mode.png)

1. En el cuadro de diálogo, defina una fecha y una hora de destino y haga clic en **Establecer fecha**. Si no selecciona una hora, la hora actual se usará de forma predeterminada.

   ![Fecha objetivo de Deformación de tiempo](/help/sites-cloud/authoring/assets/versions-timewarp-target.png)

1. La página se muestra en función de la fecha establecida. El modo Deformación de tiempo se indica mediante la barra de estado azul en la parte superior de la ventana. Utilice los vínculos de la barra de estado para poder seleccionar una nueva fecha objetivo o salir del modo Deformación de tiempo.

   ![En modo Deformación de tiempo](/help/sites-cloud/authoring/assets/versions-timewarp.png)

### Limitaciones de Deformación de tiempo {#timewarp-limitations}

Deformación de tiempo realiza el mejor esfuerzo para reproducir una página en un punto temporal seleccionado. AEM Sin embargo, debido a las complejidades de la creación continua de contenido en el espacio de trabajo, esta reproducción no siempre es posible. Tenga en cuenta estas limitaciones al utilizar Deformación de tiempo.

* **Deformación de tiempo funciona según las páginas publicadas** : Deformación de tiempo solo funciona a la perfección si ya ha publicado la página. Si no es así, Deformación de tiempo muestra la página actual en el entorno de creación.
* **Deformación de tiempo emplea versiones de página** : Si se desplaza a una página que se ha eliminado del repositorio, se procesa correctamente si aún hay versiones antiguas de la página disponibles en el repositorio.
* **Las versiones eliminadas afectan a la función Deformación de tiempo**: si las versiones se eliminan del repositorio, Deformación de tiempo no puede mostrar resultados correctos.
* **Deformación de tiempo es de solo lectura**: no se puede editar la versión antigua de la página. Tan solo pueden visualizarse. Si desea restaurar la versión anterior, debe hacerlo manualmente mediante [restaurar](#revert-to-a-version).
* **Deformación de tiempo se basa en el contenido de la página** : Si han cambiado los elementos para procesar el sitio web, como código, css y recursos, la vista difiere de la original. Estos elementos no tienen versiones en el repositorio.

>[!CAUTION]
>
>Deformación de tiempo está diseñada como una herramienta para ayudar a los creadores a comprender y crear su contenido. No se trata de un registro de auditoría ni de un registro jurídico.
