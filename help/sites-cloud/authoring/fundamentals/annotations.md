---
title: Adición de anotaciones de página
description: Muchos componentes directamente relacionados con contenido le permiten añadir una anotación
translation-type: tm+mt
source-git-commit: 16725342c1a14231025bbc1bafb4c97f0d7cfce8
workflow-type: tm+mt
source-wordcount: '623'
ht-degree: 100%

---


# Adición de anotaciones de página {#adding-page-annotations}

La adición de contenido a las páginas de un sitio web suele someterse a análisis antes de publicarse. Para ayudarle, muchos componentes directamente relacionados con el contenido (en vez de, por ejemplo, el diseño) permiten añadir anotaciones.

Una anotación coloca un boceto o una nota adhesiva de colores en la página. La anotación le permite (a usted o a otros usuarios) dejar comentarios o preguntas para otros autores o revisores.

>[!NOTE]
>
>No olvide que también dispone de los [comentarios](/help/sites-cloud/authoring/getting-started/basic-handling.md#timeline) para ofrecer opiniones sobre una página.

## Anotaciones {#annotations}

Se utiliza un modo [especial](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-modes) para crear y ver anotaciones.

>[!CAUTION]
>
>Al eliminar un recurso (p. ej. un componente), se eliminan todas las anotaciones y bocetos relacionados con ese recurso (independientemente de su posición en la página en general).

>[!NOTE]
>
>En función de sus necesidades, también puede desarrollar un flujo de trabajo para enviar notificaciones cuando estas se añadan, actualicen o eliminen.

### Anotación de un componente {#annotating-a-component}

El modo Anotar permite crear, editar, mover o eliminar anotaciones en el contenido:

1. Puede acceder al modo Anotar mediante el icono de la barra de herramientas (parte superior derecha) al editar una página:

   ![Botón Anotación](/help/sites-cloud/authoring/assets/annotations.png)

   Ahora puede ver todas las anotaciones existentes.

   >[!NOTE]
   >
   >Para salir del modo de anotación toque o haga clic en el icono Anotar (símbolo x), en la parte derecha de la barra de herramientas superior.

1. Haga clic o toque el icono Añadir anotación (símbolo &quot;+&quot; a la izquierda de la barra de herramientas) para empezar a añadir anotaciones.

   >[!NOTE]
   >
   >Para dejar de añadir anotaciones (y volver a la visualización), toque o haga clic en el icono Cancelar (símbolo x en un círculo blanco), en la parte izquierda de la barra de herramientas superior.

1. Haga clic o toque el componente necesario (los componentes que se pueden anotar se resaltarán con un borde azul) para añadir la anotación y abrir el cuadro de diálogo:

   ![Adición de una anotación](/help/sites-cloud/authoring/assets/annotation-adding.png)

   Aquí podrá utilizar el campo o icono apropiados para:

   * Especificar el texto de la anotación.
   * Crear un boceto (líneas y formas) para resaltar un área del componente.

      ![Botón Boceto de anotación](/help/sites-cloud/authoring/assets/annotation-sketch.png)

      El cursor cambia a una cruz cuando esté creando un boceto. Puede dibujar varias líneas distintas. Las líneas del boceto reflejan el color de la anotación y pueden ser una flecha, un círculo u ovaladas.

   * Elegir o cambiar el color:

      ![Botón de muestra de color de anotación](/help/sites-cloud/authoring/assets/annotation-color-swatch.png)

   * Eliminar la anotación.

      ![Botón Eliminar anotación](/help/sites-cloud/authoring/assets/annotation-delete.png)

1. Para cerrar el cuadro de diálogo de anotaciones, toque o haga clic fuera del mismo. Se mostrará una vista truncada (la primara palabra) de la anotación, junto con los bocetos, si los hay:

   ![Bocetos de anotación](/help/sites-cloud/authoring/assets/annotation-sketches.png)

1. Cuando haya terminado de editar una anotación concreta, puede:

   * Hacer clic en el marcador de texto, o tocarlo, para abrir la anotación. Una vez abierto, puede ver el texto completo, realizar cambios o eliminar la anotación.

      * Los bocetos no pueden eliminarse independientemente de la anotación.
   * Cambiar la posición del marcador de texto.
   * Tocar o hacer clic en una línea de un boceto para seleccionar el boceto y arrastrarlo a la posición deseada.
   * Desplazar o copiar un componente

      * Todas las anotaciones relacionadas y sus bocetos también se moverán o copiarán; su posición en relación con el párrafo seguirá siendo la misma.


1. Para salir del modo de anotación y volver al modo anterior, toque o haga clic en el icono Anotar (símbolo x), en la parte derecha de la barra de herramientas superior.

>[!NOTE]
>
>Las anotaciones no se pueden agregar a una página que otro usuario haya bloqueado.

>[!NOTE]
>
>La definición de un tipo de componente individual determina si se puede añadir una anotación o no en instancias de dicho componente.

## Indicador de anotaciones {#annotation-indicator}

Las anotaciones no aparecen en el modo de edición, pero el distintivo de la esquina superior derecha de la barra de herramientas mostrará el número de anotaciones de la página actual. Este distintivo sustituye al icono Anotaciones predeterminado, y además funciona como vínculo rápido que le permite acceder al modo de anotación y salir de él:

![Indicador de anotaciones](/help/sites-cloud/authoring/assets/annotation-indicator.png)

## Anotación de otros recursos {#annotating-other-resources}

Además de en los componentes, puede realizar anotaciones en distintos recursos:

* Anotación de recursos [Anotación de recursos](/help/assets/manage-digital-assets.md#annotating)
* Anotación de recursos de vídeo [Anotación de recursos de vídeo](/help/assets/manage-video-assets.md#annotate-video-assets)
