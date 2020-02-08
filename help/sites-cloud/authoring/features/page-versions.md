---
title: Uso de versiones de página
description: Cree, compare y restaure versiones de una página
translation-type: tm+mt
source-git-commit: 16725342c1a14231025bbc1bafb4c97f0d7cfce8

---


# Uso de versiones de página {#working-with-page-versions}

Al generar una versión, se crea una “instantánea” de una página en un punto específico del tiempo. Con la función de versiones, se pueden realizar las siguientes operaciones:

* Crear una versión de la página.
* Restaurar una página a una versión anterior, por ejemplo, para deshacer un cambio realizado en ella.
* Comparar la versión actual de una página con una versión anterior resaltando las diferencias en el texto y las imágenes. 

## Creación de una nueva versión {#creating-a-new-version}

Puede crear una versión de su recurso desde:

* The [Timeline rail](#creating-a-new-version-timeline)
* The [Create](#creating-a-new-version-create-with-a-selected-resource) option (when a resource is selected)

### Crear una nueva versión: línea de tiempo {#creating-a-new-version-timeline}

1. Desplácese para mostrar la página para la que desea crear una versión.
1. Seleccione la página en [modo de selección](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources).
1. Open the **Timeline** rail.
1. Toque o haga clic en los puntos suspensivos junto al campo de comentarios para mostrar las opciones:

   ![Versiones en el carril de la línea de tiempo](/help/sites-cloud/authoring/assets/versions-timeline-rail.png)

1. Seleccione **Guardar como versión**.
1. Si procede, introduzca un valor en **Etiqueta** y en **Comentario**.

   ![Agregar etiqueta para una versión](/help/sites-cloud/authoring/assets/versions-add-label.png)

1. Confirme la nueva versión con **Crear**.

   La información en la línea de tiempo se actualizará para indicar la nueva versión.

### Crear una nueva versión: creación con un recurso seleccionado {#creating-a-new-version-create-with-a-selected-resource}

1. Desplácese para mostrar la página para la que desea crear una versión.
1. Seleccione la página en [modo de selección](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources).
1. Seleccione la opción **Crear** en la barra de herramientas.
1. Se abrirá el mismo cuadro de diálogo. Si procede, puede introducir un valor **Etiqueta** y **Comentario.**
1. Confirme la nueva versión con **Crear**.

La línea de tiempo se abrirá con información actualizada para indicar la nueva versión. 

## Reversión a una versión de la página {#reverting-to-a-page-version}

Cuando haya creado una versión, puede volver a dicha versión si es necesario.

>[!NOTE]
>
>Al restaurar una página, la versión creada formará parte de una rama nueva.
>
>Como ejemplo:
>
>1. Cree una versión de una página cualquiera.
>1. Las etiquetas y los nombres de nodo iniciales serán 1.0., 1.1, 1.2, etc.
>1. Restaure la primera versión; p. ej. 1.0.
>1. Vuelva a crear versiones nuevas.
>1. Las etiquetas generadas y los nombres de nodo ahora serán 1.0.0, 1.0.1, 1.0.2, etc.


Para volver a una versión anterior:

1. Desplácese para mostrar la página que quiere revertir a una versión anterior.
1. Seleccione la página en [modo de selección](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources).
1. Abra la columna **Línea de tiempo** y seleccione **Mostrar todos** o **Versiones**. Se indicarán las versiones de página para la página seleccionada.
1. Seleccione la versión a la que desee revertir. Se mostrarán las opciones posibles:

   ![Revertir versión](/help/sites-cloud/authoring/assets/versions-revert.png)

1. Seleccione **Revertir a esta versión**. Se restaurará la versión seleccionada y se actualizará la información en la línea de tiempo.

## Vista previa de una versión {#previewing-a-version}

Puede previsualizar una versión específica:

1. Desplácese para mostrar la página que desea comparar.
1. Seleccione la página en [modo de selección](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources).
1. Abra la columna **Línea de tiempo** y seleccione **Mostrar todos** o **Versiones**. 
1. Se enumerarán las versiones de la página. Seleccione la versión que quiere previsualizar:

   ![Versión de vista previa](/help/sites-cloud/authoring/assets/versions-revert.png)

1. Seleccione **Vista previa**. La página se muestra en una nueva ficha.

   >[!CAUTION]
   >
   >Si se ha movido una página, ya no podrá realizar vistas previas en ninguna versión realizada antes del movimiento.
   >
   >Si tiene problemas con una vista previa, compruebe la [línea de tiempo](/help/sites-cloud/authoring/getting-started/basic-handling.md#timeline) para ver si la página se ha movido.

## Comparar una versión con la página actual {#comparing-a-version-with-current-page}

Para comparar una versión anterior con la página actual:

1. Desplácese para mostrar la página que desea comparar.
1. Seleccione la página en [modo de selección](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources).
1. Abra la columna **Línea de tiempo** y seleccione **Mostrar todos** o **Versiones**. 
1. Se enumerarán las versiones de la página. Seleccione la versión que desee comparar:

   ![Comparar versiones](/help/sites-cloud/authoring/assets/versions-revert.png)

1. Seleccione **Comparar con actual**. Se abrirá [Diferencias de página](/help/sites-cloud/authoring/features/page-diff.md) para mostrar las diferencias.

## Deformación de tiempo {#timewarp}

Deformación de tiempo es una función diseñada para simular el estado *publicado* de una página en periodos específicos en el pasado.

Debido a que la creación de contenido es un proceso continuo y colaborativo, el propósito de Deformación de tiempo es permitir que los autores rastreen el sitio web publicado con el paso del tiempo para comprender cómo ha cambiado el contenido. Esta función utiliza las versiones de página para determinar el estado del entorno de publicación.

Para ello:

* El sistema busca la versión de la página activa en el tiempo seleccionado.
* Esto significa que la versión mostrada se creó o activó *antes del* punto temporal seleccionado en Timewarp.
* Al navegar a una página que se ha eliminado, también se procesará, siempre que las versiones antiguas de la página sigan estando disponibles en el repositorio.
* Si no se encuentran versiones publicadas, Deformación de tiempo volverá al estado actual de la página en el entorno de creación (para evitar una página de error/404, lo que impediría el examen).

### Utilizar la Deformación de tiempo {#using-timewarp}

Deformación de tiempo es un [modo](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-modes) del editor de páginas. Para iniciarlo, basta con activarlo como cualquier otro modo.

1. Inicie el editor de la página donde desee comenzar Deformación de tiempo y, a continuación, elija **Deformación de tiempo** en la selección de modo.

   ![Modo Deformación de tiempo](/help/sites-cloud/authoring/assets/versions-timewarp-mode.png)

1. En el cuadro de diálogo, establezca una fecha y una hora de destino y toque o haga clic en **Establecer fecha**. Si no selecciona una hora, el valor predeterminado será la hora actual.

   ![Fecha objetivo de Deformación de tiempo](/help/sites-cloud/authoring/assets/versions-timewarp-target.png)

1. La página se muestra en función de la fecha establecida. El modo Deformación de tiempo se indica mediante la barra de estado azul en la parte superior de la ventana. Utilice los vínculos de la barra de estado para seleccionar una nueva fecha de destino o para salir del modo Deformación de tiempo.

   ![En modo Deformación de tiempo](/help/sites-cloud/authoring/assets/versions-timewarp.png)

### Limitaciones de Deformación de tiempo {#timewarp-limitations}

Deformación de tiempo realiza el mejor esfuerzo para reproducir una página en un punto temporal seleccionado. Sin embargo, debido a las complejidades de la creación continua de contenido en AEM, esto no siempre es posible. Estas limitaciones deben tenerse en cuenta al utilizar Deformación de tiempo.

* **Deformación de tiempo funciona en función de las páginas** publicadas: Deformación de tiempo solo funcionará completamente si ya ha publicado la página. En caso contrario, Deformación de tiempo mostrará la página actual en el entorno de creación.
* **Deformación de tiempo utiliza versiones** de página: si se desplaza a una página que se ha eliminado del repositorio, se procesará correctamente si las versiones anteriores de la página siguen estando disponibles en el repositorio.
* **Las versiones eliminadas afectan a Deformación de tiempo** : si se eliminan versiones del repositorio, Deformación de tiempo no puede mostrar la vista correcta.
* **Deformación de tiempo es de solo** lectura: no se puede editar la versión antigua de la página. tan solo pueden visualizarse. Si desea restaurar la versión anterior, deberá hacerlo manualmente mediante la [restauración](#reverting-to-a-page-version).
* **Deformación de tiempo solo se basa en el contenido** de la página. Si los elementos (como código, css, recursos/imágenes, etc.) para procesar el sitio web han cambiado, la vista será diferente de la original, ya que dichos elementos no tienen versiones en el repositorio.

>[!CAUTION]
>
>Deformación de tiempo está diseñada como una herramienta para ayudar a los autores a comprender y crear su contenido. No se trata de un registro de auditoría ni de un registro jurídico.
