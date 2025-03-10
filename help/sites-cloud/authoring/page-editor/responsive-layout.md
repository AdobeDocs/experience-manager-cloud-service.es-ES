---
title: Diseño adaptable
description: AEM le permite crear un diseño adaptable para las páginas mediante el uso del componente Contenedor de diseño.
exl-id: 87202742-5bed-4e87-a427-456a1a0e72cc
solution: Experience Manager Sites
feature: Authoring
role: User
source-git-commit: 70a35cfeb163967b0f627d3ac6495f112d922974
workflow-type: tm+mt
source-wordcount: '1789'
ht-degree: 76%

---


# Diseño adaptable {#responsive-layout}

AEM le permite tener un diseño adaptable para sus páginas mediante el componente **Contenedor de diseño**.

>[!TIP]
>
>Este documento proporciona información general sobre las funciones del contenedor de diseño disponibles para los autores de contenido. Hay recursos adicionales disponibles:
>
>* Para los administradores del sitio, los detalles sobre cómo configurar el contenedor de diseño para sus sitios se describen en el documento [Configuración del contenedor de diseño y el modo de diseño.](/help/sites-cloud/administering/responsive-layout.md)
>* Para los desarrolladores, los detalles del contenedor de diseño y de la cuadrícula adaptable se describen en [El documento de diseño adaptable,](/help/implementing/developing/introduction/responsive-design.md), que proporciona sugerencias y sugerencias para utilizar contenedores de diseño y cuadrícula adaptable al diseñar el sitio.

## Información general {#overview}

El componente **Contenedor de diseño** proporciona un sistema de párrafos que le permite colocar componentes dentro de una cuadrícula adaptable. Esta cuadrícula puede reorganizar el diseño según el tamaño y el formato del dispositivo o la ventana. El componente se usa junto con el modo [**Diseño**](/help/sites-cloud/authoring/page-editor/introduction.md#mode-selector), que le permite crear y editar su diseño interactivo en función del dispositivo.

El contenedor de diseño:

* Proporciona un ajuste horizontal a la cuadrícula, junto con la capacidad de colocar componentes en la cuadrícula en paralelo y definir cuándo deben contraerse o redistribuirse.
* Utiliza puntos de interrupción predefinidos (por ejemplo, para un teléfono, una tableta, etc.) para permitirle definir el comportamiento requerido del contenido para los dispositivos o la orientación relacionados.
   * Por ejemplo, puede personalizar el tamaño del componente o si el componente se puede ver en dispositivos específicos.
* Se puede anidar para permitir el control de columnas.

A continuación, el usuario puede ver cómo se representa el contenido para dispositivos específicos mediante el emulador.

AEM realiza un diseño interactivo para sus páginas mediante una combinación de diferentes mecanismos:

* Componente [**Contenedor de diseño**](#adding-a-layout-container-and-its-content-edit-mode)

  Este componente está disponible en el [navegador de componentes](/help/sites-cloud/authoring/page-editor/editor-side-panel.md#components-browser) y proporciona un sistema de párrafos de red que le permite añadir y colocar componentes en una cuadrícula interactiva. También se puede establecer como sistema de párrafos predeterminado en la página.

* [**Modo de diseño**](/help/sites-cloud/authoring/page-editor/introduction.md#mode-selector)

  Después de colocar el contenedor de diseño en la página, puede usar el modo de **diseño** para colocar el contenido en la red interactiva.

* [**Emulador**](#selecting-a-device-to-emulate)
Esto permite crear y editar sitios web interactivos que reorganizan el diseño según el tamaño del dispositivo o la ventana, mediante el cambio de tamaño de los componentes de forma interactiva. A continuación, el usuario puede ver cómo se representa el contenido mediante el emulador.

Con estos mecanismos de cuadrícula adaptable puede hacer lo siguiente:

* Utilizar puntos de interrupción para definir diferentes diseños de contenido según la anchura del dispositivo (en relación con el tipo y la orientación del dispositivo).
* Utilizar estos mismos puntos de interrupción y diseños de contenido para asegurarse de que el contenido es adaptable al tamaño de la ventana del navegador en el escritorio.
* Utilizar el ajuste horizontal a la cuadrícula que le permite colocar componentes en la cuadrícula, cambiar su tamaño según sea necesario y definir cuándo deben contraerse o redistribuirse lateralmente o arriba/abajo.
* Ocultar componentes de diseños de dispositivo específicos.
* Realizar el control de columnas.

Según el proyecto, el contenedor de diseño se puede utilizar como sistema de párrafos predeterminado para las páginas o como componente disponible para añadirse a su página mediante el explorador de componentes (o ambos).

>[!NOTE]
>
>El uso de los mecanismos anteriores se habilita en la configuración de la plantilla. Consulte el documento [Configuración del diseño interactivo](/help/sites-cloud/administering/responsive-layout.md) para obtener más información.

## Definiciones de diseños, emulación de dispositivos y puntos de interrupción {#layout-definitions-device-emulation-and-breakpoints}

Al crear el contenido de su sitio web desea asegurarse de que el contenido se muestre correctamente según el dispositivo utilizado para ello.

AEM definir diseños según la anchura del dispositivo:

* El emulador permite emular estos diseños en una amplia gama de dispositivos. Además del tipo de dispositivo, la orientación, que se selecciona mediante la opción **Rotar dispositivo**, puede afectar al punto de interrupción seleccionado a medida que cambia la anchura.
* Los puntos de interrupción son puntos que separan las definiciones de diseño.
   * Definen efectivamente la anchura máxima (en píxeles) de cualquier dispositivo que utilice un diseño específico.
   * Normalmente, los puntos de interrupción son válidos para una selección de dispositivos, en función del ancho de sus pantallas.
   * El alcance de un punto de interrupción se extiende hacia la izquierda hasta el siguiente punto de interrupción.
   * No puede seleccionar específicamente un punto de interrupción; al seleccionar el dispositivo y la orientación se selecciona automáticamente el punto de interrupción adecuado.

El dispositivo **Escritorio** no tiene una anchura específica y está relacionado con el punto de interrupción predeterminado (por ejemplo, todo lo que está por encima del último punto de interrupción configurado).

>[!NOTE]
>
>Es posible definir puntos de interrupción para cada dispositivo individual, pero esto incrementaría drásticamente los trabajos de definición de diseño y mantenimiento.

Al seleccionar en el emulador un dispositivo específico para emular y definir el diseño, el punto de interrupción relacionado también queda resaltado. Cualquier cambio de diseño que realice será aplicable a otros dispositivos a los que se aplique el punto de interrupción. Es decir, cualquier dispositivo situado a la izquierda del marcador de punto de interrupción activo, pero antes del marcador de punto de interrupción siguiente.

Por ejemplo, si selecciona el dispositivo **iPhone 6 Plus** (definido con una anchura de 540 píxeles) para emulación y diseño, se activa también el punto de interrupción **Teléfono** (definido como 768 píxeles). Cualquier cambio de diseño que realice en **iPhone 6** es aplicable a otros dispositivos en el punto de interrupción **Teléfonos**, como **iPhone 5** (definido como 320 píxeles).

![Emuladores](/help/sites-cloud/authoring/assets/responsive-layout-emulators.png)

## Selección de un dispositivo para emular {#selecting-a-device-to-emulate}

1. Abra la página necesaria para editarla. Por ejemplo:

   `http://<host>:<port>/editor.html/content/wknd/en/sports/la-skateparks.html`

1. Seleccione el icono **Emulador** de la barra de herramientas superior:

   ![Botón Emulador](/help/sites-cloud/authoring/assets/emulator.png)

1. Se abrirá la barra de herramientas del emulador.

   ![Barra de herramientas del emulador](/help/sites-cloud/authoring/assets/responsive-layout-emulator-toolbar.png)

   La barra de herramientas del emulador muestra opciones de diseño adicionales:

   * **Rotar dispositivo**: permite girar un dispositivo desde la orientación vertical (vertical) a la horizontal (horizontal) y a la inversa.

   ![Botón Girar el dispositivo a horizontal](/help/sites-cloud/authoring/assets/responsive-layout-rotate-device-landscape-button.png)
   ![Botón Girar el dispositivo a vertical](/help/sites-cloud/authoring/assets/responsive-layout-rotate-device-portrait-button.png)

   * **Seleccionar dispositivo**: le permite definir un dispositivo específico para emular de una lista (consulte el paso siguiente para obtener detalles)

   ![Botón Seleccionar dispositivo](/help/sites-cloud/authoring/assets/responsive-layout-select-device-button.png)

1. Para seleccionar un dispositivo específico para emular, puede hacer lo siguiente:

   * Utilizar el icono Seleccionar dispositivo y seleccionarlo desde un selector desplegable.
   * Seleccione el indicador de dispositivo en la barra de herramientas del emulador.

   ![Menú desplegable Seleccionar dispositivo](/help/sites-cloud/authoring/assets/responsive-layout-select-device-dropdown.png)

1. Una vez que haya seleccionado un dispositivo específico, puede:

   * Ver el marcador activo del dispositivo seleccionado; por ejemplo, **iPad.**
   * Ver el marcador activo del [punto de interrupción](#layout-definitions-device-emulation-and-breakpoints) adecuado; por ejemplo, **Tableta.**
   * La línea discontinua azul representa el *pliegue* para el dispositivo seleccionado (en este caso, un **iPhone 6 Plus** en orientación vertical).

   ![El pliegue](/help/sites-cloud/authoring/assets/responsive-layout-fold.png)

   * El pliegue también se puede considerar el salto de línea de la página (no confundir con los [puntos de interrupción](#layout-definitions-device-emulation-and-breakpoints)) del contenido. Esto se muestra para mayor comodidad, a fin de mostrar qué parte del contenido ve el usuario en el dispositivo antes de desplazarse.
   * La línea para el pliegue no se muestra si la altura del dispositivo que se está emulando es mayor que el tamaño de pantalla.
   * El pliegue se muestra para la comodidad del autor y no aparece en la página publicada.

## Adición de un contenedor de diseño y su contenido (modo de edición) {#adding-a-layout-container-and-its-content-edit-mode}

Un **contenedor de diseño** es un sistema de párrafos que:

* Contiene otros componentes.
* Define el diseño.
* Responde a los cambios.

>[!NOTE]
>
>Si no está disponible, el **contenedor de diseño** debe estar [activado explícitamente para un sistema de párrafos o una página](/help/sites-cloud/administering/responsive-layout.md).

1. El **contenedor de diseño** está disponible como componente estándar en el [navegador de componentes](/help/sites-cloud/authoring/page-editor/editor-side-panel.md#components-browser). Desde aquí puede arrastrarlo a la ubicación deseada en la página tras la cual podrá ver el marcador de posición **Arrastrar componentes aquí**.
1. A continuación, puede agregar componentes al contenedor del diseño. Estos componentes contendrán el contenido real:

   ![Contenedor de diseño](/help/sites-cloud/authoring/assets/responsive-layout-add-to-layout-container.png)

## Selección y ejecución de una acción en un contenedor de diseños (modo de edición) {#selecting-and-taking-action-on-a-layout-container-edit-mode}

Al igual que con otros componentes, puede seleccionar un contenedor de diseño (en modo **Editar**) y luego actuar en él (copiar, cortar, eliminar):

>[!CAUTION]
>
>Como un contenedor de diseño es un sistema de párrafos, al eliminar el componente se eliminará tanto la cuadrícula de diseño como todos los componentes (y su contenido) que se encuentren dentro del contenedor.

1. Si pasa el ratón por encima o selecciona el marcador de posición de la cuadrícula, se muestra el menú de acción.

   ![Agregar al contenedor de diseño](/help/sites-cloud/authoring/assets/responsive-layout-container.png)

   Debe seleccionar la opción **Principal**.

   ![Botón Principal](/help/sites-cloud/authoring/assets/responsive-layout-parent-button.png)

1. Si el componente de diseño está anidado, la selección de la opción **Principal** presenta una lista desplegable de opciones que le permite seleccionar el contenedor de diseños anidado o sus elementos principales.

   Cuando pasa el ratón sobre los nombres de contenedor en la lista desplegable, los contornos se muestran en la página.

   * El contenedor de diseños anidado en la parte inferior se muestra en azul.
   * Cada contenedor sucesivo aparece en un tono más claro de azul.

   ![Contenedores anidados](/help/sites-cloud/authoring/assets/responsive-layout-nested.png)

1. Toda la cuadrícula se resalta con su contenido. Se muestra la barra de herramientas de acciones, desde donde puede seleccionar una acción como **Eliminar.**

## Definición de diseños (modo de diseño) {#defining-layouts-layout-mode}

>[!NOTE]
>
>Puede definir un diseño distinto para cada [punto de interrupción](#layout-definitions-device-emulation-and-breakpoints) (tal y como determinan el tipo y la orientación del dispositivo emulado).

Para configurar el diseño de una cuadrícula interactiva implementada con el contenedor de diseño, debe usar el modo **Diseño**.

El modo **Diseño** puede iniciarse de dos formas.

* Mediante el uso del [menú de modo de la barra de herramientas](/help/sites-cloud/authoring/page-editor/introduction.md#mode-selector) y seleccionando el modo **Diseño**.
   * Seleccione el modo **Diseño** del mismo modo que si desea cambiar al modo **Editar** o **Segmentación**.
   * El modo **Diseño** se mantiene y no abandona el modo **Diseño** hasta que se selecciona otro modo a través del selector correspondiente.
* Al [editar un componente individual](/help/sites-cloud/authoring/page-editor/edit-content.md#editing-component-layout).
   * Mediante la opción **Diseño** en el menú de acción rápida del componente, puede cambiar al modo **Diseño**.
   * El modo **Diseño** persiste mientras se edita el componente y vuelve al modo **Editar** en cuanto el enfoque cambia a otro componente.

En el modo de diseño, puede ejecutar una serie de acciones a una cuadrícula:

* Redimensionar los componentes del contenido utilizando los puntos azules. Al redimensionar, siempre se hará un ajuste a la cuadrícula. Al redimensionar, se muestra la cuadrícula de fondo como referencia para la alineación:

  ![Cambiar el tamaño de los componentes](/help/sites-cloud/authoring/assets/responsive-layout-resizing.png)

  >[!NOTE]
  >
  >Se mantienen las proporciones y relaciones al cambiar el tamaño de componentes como **Imágenes**.

* Seleccione un componente de contenido, la barra de herramientas le permite:
   * **Principal**: le permite seleccionar todo el componente del contenedor de diseño para realizar acciones en conjunto.
   * **Flotar a una línea nueva**: se mueve el componente a una línea nueva, según el espacio disponible en la cuadrícula.
   * **Ocultar componente**: el componente se hace invisible (puede restaurarse desde la barra de herramientas del contenedor de diseños).

  ![Ocultar componente](/help/sites-cloud/authoring/assets/responsive-layout-hide.png)

* En el modo **Diseño** puede seleccionar **Arrastrar componentes aquí** para seleccionar todo el componente. La barra de herramientas se muestra para este modo.

  La barra de herramientas tiene diferentes opciones en función del estado del componente de diseño y de los componentes que le pertenecen. Por ejemplo:

   * **Principal**: seleccione el componente principal.

     ![Botón Principal](/help/sites-cloud/authoring/assets/responsive-layout-parent-button.png)

   * **Mostrar componentes ocultos**: permite mostrar todos los componentes o cada componente por separado. El número indica cuántos componentes ocultos existen en ese momento. El contador muestra cuántos componentes hay ocultos.

     ![Botón Mostrar componentes ocultos](/help/sites-cloud/authoring/assets/responsive-layout-show-button.png)

   * **Revertir diseño de punto de interrupción**: volver al diseño predeterminado. No se impone ningún diseño personalizado.

     ![Botón Revertir diseño de punto de interrupción](/help/sites-cloud/authoring/assets/responsive-layout-revert-button.png)

   * **Flotar hasta una nueva línea**: suba el componente una posición si el espacio lo permite.

     ![Botón Flotar a una línea nueva](/help/sites-cloud/authoring/assets/responsive-layout-float-button.png)

   * **Ocultar componente**: oculte el componente actual.

     ![Ocultar botón de componente](/help/sites-cloud/authoring/assets/responsive-layout-hide-button.png)

  >[!NOTE]
  >
  >En el ejemplo anterior, las acciones de flotar y ocultar están disponibles porque este contenedor de diseño está anidado en un contenedor de diseño principal.

   * **Mostrar los componentes:** permite seleccionar los componentes principales para mostrar la barra de herramientas de acciones con la opción **Mostrar componentes ocultos**. En este ejemplo, hay dos componentes ocultos.

     ![Mostrar componentes](/help/sites-cloud/authoring/assets/responsive-layout-unhide.png)

  Si se selecciona la opción **Mostrar componentes ocultos**, se mostrarán en azul los componentes que están ocultos actualmente en sus posiciones originales.

  ![Botón Restaurar todo](/help/sites-cloud/authoring/assets/responsive-layout-restore-all.png)

  La selección de la opción **Restaurar todo** permitirá que se muestren todos los componentes ocultos.
