---
title: Adición de anotaciones de página
description: Utilice el modo de anotación para dejar anotaciones y bocetos en páginas, ya que utilizaría notas adhesivas para ayudarle en el proceso de revisión de contenido
exl-id: a9cb9745-8140-4795-a5f9-fb3a1a299bd8
source-git-commit: 64d801b108229866394e993811a67f983be5df6c
workflow-type: tm+mt
source-wordcount: '699'
ht-degree: 35%

---

# Adición de anotaciones de página {#adding-page-annotations}

La creación de contenido para la experiencia digital suele requerir análisis y comentarios antes de la publicación. Para facilitar este proceso de comentarios, AEM permite añadir anotaciones al contenido.

Una anotación coloca un boceto simple o una nota (piensen en la nota adhesiva del mundo real) en la página. La anotación le permite dejar comentarios o preguntas para otros autores y revisores.

>[!TIP]
>
>No olvide que también dispone de los [comentarios](/help/sites-cloud/authoring/getting-started/basic-handling.md#timeline) para ofrecer opiniones sobre una página.

Se utiliza un modo [especial](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-modes) para crear y ver anotaciones.

>[!TIP]
>
>Según sus necesidades, también puede desarrollar un [flujo de trabajo](/help/sites-cloud/authoring/workflows/overview.md) para enviar notificaciones cuando se añadan, actualicen o eliminen anotaciones.

## Indicador de anotaciones {#annotation-indicator}

Las anotaciones no aparecen en el modo de edición, pero el distintivo de la esquina superior derecha de la barra de herramientas mostrará el número de anotaciones de la página actual. Este distintivo sustituye al icono Anotaciones predeterminado, y además funciona como vínculo rápido que le permite acceder al modo de anotación y salir de él:

![Indicador de anotaciones](/help/sites-cloud/authoring/assets/annotation-indicator.png)

## Modo Anotar {#annotate-mode}

Las anotaciones solo están visibles en el modo Anotar .

1. Puede acceder al modo Anotar mediante el icono de la barra de herramientas (parte superior derecha) al editar una página:

   ![Botón Anotación](/help/sites-cloud/authoring/assets/annotations.png)

   Ahora puede ver todas las anotaciones existentes.

   ![Ejemplos de anotaciones](/help/sites-cloud/authoring/assets/annotation-sketches.png)

1. Toque o haga clic en la anotación para abrir el cuadro de diálogo de anotaciones y ver sus detalles.

   ![Detalles de anotación](/help/sites-cloud/authoring/assets/annotation-adding.png)

1. Para salir del modo Anotar y volver al modo utilizado anteriormente, toque o haga clic en el botón x a la derecha de la barra de herramientas superior.

## Adición y edición de anotaciones {#annotating-a-component}

Además de ver las anotaciones, el modo Anotar permite crear, editar, mover o eliminar anotaciones en el contenido

1. [Iniciar modo Anotar](#annotate-mode) en la página .

1. Toque o haga clic en el icono Añadir anotación (símbolo &quot;+&quot; a la izquierda de la barra de herramientas) para empezar a añadir anotaciones.

1. Toque o haga clic en el componente requerido (los componentes que se pueden anotar se resaltarán con un borde azul) para añadir la anotación y abrir el cuadro de diálogo:

   ![Adición de una anotación](/help/sites-cloud/authoring/assets/annotation-adding.png)

   Aquí podrá utilizar el campo o icono apropiados para:

   * Especificar el texto de la anotación.
   * Crear un boceto (líneas y formas) para resaltar un área del componente.

      ![Botón Boceto de anotación](/help/sites-cloud/authoring/assets/annotation-sketch.png)

      El cursor cambia a una cruz cuando esté creando un boceto. Puede dibujar varias líneas distintas. Las líneas del boceto reflejan el color de la anotación y pueden ser una flecha, un círculo u ovaladas.

   * Elija o cambie el color:

      ![Botón de muestra de color de anotación](/help/sites-cloud/authoring/assets/annotation-color-swatch.png)

1. Para cerrar el cuadro de diálogo de anotaciones, toque o haga clic fuera del mismo. Se muestra una vista truncada de la anotación, junto con los bocetos, si los hay:

   ![Bocetos de anotación](/help/sites-cloud/authoring/assets/annotation-sketches.png)

1. Cuando haya terminado de editar una anotación concreta, puede:

   * Toque o haga clic en el marcador de texto para abrir la anotación. Una vez abierto, puede ver el texto completo, realizar cambios o [elimine la anotación.](#deleting-annotations)
   * Cambiar la posición del marcador de texto.
   * Toque o haga clic en una línea de un boceto para seleccionar el boceto y arrastrarlo a la posición deseada.
   * Mover o copiar un componente
      * Las anotaciones relacionadas y sus bocetos también se moverán o copiarán, pero su posición en relación con el párrafo seguirá siendo la misma.


>[!NOTE]
>
>Las anotaciones no se pueden agregar a una página que otro usuario haya bloqueado.

>[!NOTE]
>
>La definición de un tipo de componente individual determina si se puede añadir una anotación o no en instancias de dicho componente.

## Eliminación de anotaciones y bocetos {#deleting-annotations}

Las anotaciones y sus bocetos asociados se pueden eliminar.

1. [Iniciar modo Anotar](#annotate-mode) en la página .

1. Hacer clic en el marcador de texto, o tocarlo, para abrir la anotación.

1. Toque o haga clic en el icono Eliminar .

   ![Eliminar anotación](/help/sites-cloud/authoring/assets/annotation-delete.png)

1. Se eliminan la anotación y todos los bocetos asociados.

>[!NOTE]
>
>Al eliminar un componente, se eliminan todas las anotaciones y bocetos relacionados con ese recurso, independientemente de su posición en la página en general.

## Eliminación de bocetos solamente {#deleting-sketches}

Solo puede eliminar bocetos específicos en lugar de toda la anotación con todos los bocetos asociados.

1. [Iniciar modo Anotar](#annotate-mode) en la página .

1. Toque o haga clic en el boceto. AEM resalta con un cuadro azul más oscuro.

   ![Seleccionar boceto para eliminación](/help/sites-cloud/authoring/assets/annotation-sketch-delete.png)

1. Presione la tecla Supr del teclado.

1. El boceto se elimina, pero la anotación permanece.

## Anotación de otros recursos {#annotating-other-resources}

Además de en los componentes, puede realizar anotaciones en distintos recursos:

* Anotación de recursos [Anotación de recursos](/help/assets/manage-digital-assets.md#annotating)
* Anotación de recursos de vídeo [Anotación de recursos de vídeo](/help/assets/manage-video-assets.md#annotate-video-assets)
