---
title: Diseño adaptable
description: El AEM le permite llevar a cabo un diseño interactivo para sus páginas
exl-id: 87202742-5bed-4e87-a427-456a1a0e72cc
source-git-commit: 47910a27118a11a8add6cbcba6a614c6314ffe2a
workflow-type: tm+mt
source-wordcount: '1766'
ht-degree: 100%

---

# Diseño adaptable  {#responsive-layout}

AEM le permite disponer de un diseño interactivo para sus páginas mediante el uso del componente **Contenedor de diseño**.

Este componente proporciona un sistema de párrafos que le permite colocar componentes en una cuadrícula interactiva. Esta cuadrícula puede reorganizar el diseño en función del tamaño y formato del dispositivo o ventana. Este componente se utiliza en combinación con el modo [**Diseño**](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-modes), que le permite crear y editar el diseño interactivo en función del dispositivo.

El contenedor de diseños:

* Proporciona un ajuste horizontal a la cuadrícula, además de la posibilidad de colocar componentes en la cuadrícula uno al lado de otro y de definir cuándo se deben contraer o redistribuir.
* Usa puntos de interrupción predefinidos (por ejemplo, para un teléfono, una tableta, etc.) que le permiten definir el comportamiento obligatorio del contenido para dispositivos relacionados/su orientación.
   * Por ejemplo, puede personalizar el tamaño del componente o si el componente se puede ver en determinados dispositivos.
* Se puede anidar para permitir el control de columnas.

El usuario puede utilizar el emulador para ver cómo se representará el contenido en determinados dispositivos.

AEM realiza un diseño interactivo para sus páginas mediante una combinación de diferentes mecanismos:

* Componente [**Contenedor de diseño**](#adding-a-layout-container-and-its-content-edit-mode)

   Este componente está disponible en el [navegador de componentes](/help/sites-cloud/authoring/fundamentals/environment-tools.md#components-browser) y proporciona un sistema de párrafos de red que le permite añadir y colocar componentes en una cuadrícula interactiva. También se puede establecer como sistema de párrafos predeterminado en la página.

* [**Modo de diseño**](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-modes)

   Después de colocar el contenedor de diseño en la página, puede usar el modo de **diseño** para colocar el contenido en la red interactiva.

* [**Emulador**](#selecting-a-device-to-emulate) Esta opción le permite crear y editar sitios web interactivos que reorganizan el diseño en función del tamaño del dispositivo o la ventana, mediante el redimensionado activo de los componentes. El usuario puede utilizar el emulador para ver cómo se representará el contenido.

Estos mecanismos de cuadrícula interactiva le permiten:

* Utilizar puntos de interrupción para definir diferentes diseños de contenido según la anchura del dispositivo (en relación con el tipo de dispositivo y la orientación).
* Utilizar estos mismos puntos de interrupción y diseños de contenido para asegurarse de que el contenido es adaptable al tamaño de la ventana del navegador en el escritorio.
* Utilizar el ajuste horizontal a la cuadrícula que le permite colocar componentes en la cuadrícula, cambiar su tamaño según sea necesario y definir cuándo deben contraerse o redistribuirse lateralmente o arriba/abajo.
* Ocultar componentes de diseños de dispositivo específicos.
* Realizar el control de columnas.

En función del proyecto, el contenedor de diseño se puede utilizar como sistema de párrafos predeterminado para las páginas o como componente disponible para añadirse a su página mediante el explorador de componentes (o ambos).

>[!TIP]
>
>Adobe proporciona [documentación de GitHub](https://adobe-marketing-cloud.github.io/aem-responsivegrid/) del diseño interactivo como referencia que se puede entregar a los desarrolladores de interfaces de usuario, lo cual les permite usar la cuadrícula de AEM fuera de AEM como, por ejemplo, para crear maquetas HTML estáticas para un sitio de AEM futuro.

>[!NOTE]
>
>El uso de los mecanismos anteriores se habilita en la configuración de la plantilla. Consulte Configuración de un diseño interactivo para obtener más información. <!-- Use of the above mechanisms is enabled by configuration on the template. See [Configuring Responsive Layout](/help/sites-administering/configuring-responsive-layout.md) for further information.-->

## Definiciones de diseños, emulación de dispositivos y puntos de interrupción {#layout-definitions-device-emulation-and-breakpoints}

Al crear el contenido de su sitio web desea asegurarse de que el contenido se muestre correctamente según el dispositivo utilizado para ello.

AEM le permite definir diseños en función de la anchura del dispositivo:

* El emulador le permite emular estos diseños en una serie de dispositivos. Además del tipo de dispositivo, la orientación, que se selecciona mediante la opción **Rotar dispositivo**, puede afectar al punto de interrupción seleccionado a medida que cambia la anchura.
* Los puntos de interrupción son puntos que separan las definiciones de diseño.
   * Definen efectivamente la anchura máxima (en píxeles) de cualquier dispositivo que utilice un diseño específico.
   * Normalmente, los puntos de interrupción son válidos para una selección de dispositivos, en función del ancho de sus pantallas.
   * El alcance de un punto de interrupción se extiende hacia la izquierda hasta el siguiente punto de interrupción.
   * No puede seleccionar específicamente un punto de interrupción; al seleccionar el dispositivo y la orientación se selecciona automáticamente el punto de interrupción adecuado.

El dispositivo **Escritorio** no tiene una anchura específica y está relacionado con el punto de interrupción predeterminado (p. ej., todo lo que está por encima del último punto de interrupción configurado).

>[!NOTE]
>
>Es posible definir puntos de interrupción para cada dispositivo individual, pero esto incrementaría drásticamente los trabajos de definición de diseño y mantenimiento.

Al seleccionar en el emulador un dispositivo específico para emular y definir el diseño, el punto de interrupción relacionado también quedará resaltado. Todos los cambios que haga en el diseño se aplicarán a otros dispositivos a los que se aplique el punto de interrupción (por ejemplo, cualquier dispositivo posicionado a la izquierda del marcador de punto de interrupción activo, antes del siguiente marcador de punto de interrupción).

Por ejemplo, si selecciona el dispositivo **iPhone 6 Plus** (definido con una anchura de 540 píxeles) para emulación y diseño, se activará también el punto de interrupción **Teléfono** (definido como 768 píxeles). Cualquier cambio de diseño que realice para el **iPhone 6** se aplicará a los demás dispositivos que se encuentren bajo el punto de interrupción **Teléfonos**, como **iPhone 5** (definido como 320 píxeles).

![Emuladores](/help/sites-cloud/authoring/assets/responsive-layout-emulators.png)

## Selección de un dispositivo para emular {#selecting-a-device-to-emulate}

1. Abra la página deseada para editarla. Por ejemplo:

   `http://<host>:<port>/editor.html/content/wknd/en/sports/la-skateparks.html`

1. Seleccione el icono **Emulador** de la barra de herramientas superior:

   ![Botón Emulador](/help/sites-cloud/authoring/assets/emulator.png)

1. Se abrirá la barra de herramientas del emulador.

   ![Barra de herramientas del emulador](/help/sites-cloud/authoring/assets/responsive-layout-emulator-toolbar.png)

   La barra de herramientas del emulador muestra opciones de diseño adicionales:

   * **Rotar dispositivo**: le permite rotar un dispositivo de la orientación vertical a la horizontal y viceversa.

   ![Botón Girar el dispositivo a horizontal](/help/sites-cloud/authoring/assets/responsive-layout-rotate-device-landscape-button.png)
   ![Botón Girar el dispositivo a vertical](/help/sites-cloud/authoring/assets/responsive-layout-rotate-device-portrait-button.png)

   * **Seleccionar dispositivo**: le permite definir un dispositivo específico para emular de una lista (consulte el paso siguiente para obtener detalles)

   ![Botón Seleccionar dispositivo](/help/sites-cloud/authoring/assets/responsive-layout-select-device-button.png)

1. Al seleccionar un dispositivo específico para emular, puede efectuar cualquiera de las siguientes acciones:

   * Utilizar el icono Seleccionar dispositivo y seleccionarlo de un selector desplegable.
   * Tocar o hacer clic en el indicador del dispositivo de la barra de herramientas del emulador.

   ![Menú desplegable Seleccionar dispositivo](/help/sites-cloud/authoring/assets/responsive-layout-select-device-dropdown.png)

1. Una vez que haya seleccionado un dispositivo específico, puede:

   * Ver el marcador activo del dispositivo seleccionado; por ejemplo, **iPad.**
   * Ver el marcador activo del [punto de interrupción](#layout-definitions-device-emulation-and-breakpoints) adecuado; por ejemplo, **Tableta.**
   * La línea discontinua azul representa el *pliegue* para el dispositivo seleccionado (en este caso, un **iPhone 6 Plus** en orientación vertical).

   ![El pliegue](/help/sites-cloud/authoring/assets/responsive-layout-fold.png)

   * El pliegue también se puede considerar el salto de línea de la página (no confundir con los [puntos de interrupción](#layout-definitions-device-emulation-and-breakpoints)) del contenido. Esto se muestra para mostrar qué parte del contenido verá el usuario en el dispositivo antes de efectuar el desplazamiento.
   * La línea del pliegue no se mostrará si la altura del dispositivo que se emula es superior al tamaño de la pantalla.
   * El pliegue se muestra para la comodidad del autor y no aparece en la página publicada.


## Adición de un contenedor de diseño y su contenido (modo de edición) {#adding-a-layout-container-and-its-content-edit-mode}

Un **contenedor de diseño** es un sistema de párrafos que:

* Contiene otros componentes.
* Define el diseño.
* Responde a los cambios.

>[!NOTE]
>
>Si no está disponible, el **contenedor de diseño** debe activarse explícitamente para un sistema de párrafos o una página. <!-- If not already available, the **Layout Container** must be explicitly [activated for a paragraph system/page](/help/sites-administering/configuring-responsive-layout.md).-->

1. El **contenedor de diseño** está disponible como componente estándar en el [navegador de componentes](/help/sites-cloud/authoring/fundamentals/environment-tools.md#components-browser). Desde aquí puede arrastrarlo a la ubicación deseada en la página tras la cual verá el marcador de posición **Arrastrar componentes aquí**.
1. A continuación, puede agregar componentes al contenedor de diseño. Estos componentes albergarán el contenido real:

   ![Contenedor de diseño](/help/sites-cloud/authoring/assets/responsive-layout-add-to-layout-container.png)

## Selección y ejecución de una acción en un contenedor de diseños (modo de edición) {#selecting-and-taking-action-on-a-layout-container-edit-mode}

Al igual que con otros componentes, puede seleccionar un contenedor de diseños (cuando se encuentra en el modo de **edición**) y luego realizar una acción en él (copiar, cortar, eliminar):

>[!CAUTION]
>
>Dado que los contenedores de diseños son un sistema de párrafos, al eliminar el componente, se eliminará la cuadrícula de diseño y todos los componentes (y su contenido) incluidos en el contenedor.

1. Si pasa el puntero del ratón o toca el marcador de posición de la cuadrícula, se mostrará el menú de acciones.

   ![Agregar al contenedor de diseño](/help/sites-cloud/authoring/assets/responsive-layout-container.png)

   Debe seleccionar la opción **Principal**.

   ![Botón Principal](/help/sites-cloud/authoring/assets/responsive-layout-parent-button.png)

1. Si el componente de diseño se encuentra anidado, la selección de la opción **Principal** presenta una lista desplegable de opciones que le permite seleccionar el contenedor de diseños anidado o sus elementos principales.

   Cuando pase el ratón sobre los nombres de contenedor de la lista desplegable, los contornos se mostrarán en la página.

   * El contenedor de diseños anidado en la parte inferior se muestra en color azul.
   * Cada contenedor sucesivo aparece en un tono más claro de azul.

   ![Contenedores anidados](/help/sites-cloud/authoring/assets/responsive-layout-nested.png)

1. De esta forma se resaltará toda la cuadrícula con su contenido. Se muestra la barra de herramientas de acciones, desde donde puede seleccionar una acción, como, por ejemplo, **Eliminar.**

## Definición de diseños (modo de diseño) {#defining-layouts-layout-mode}

>[!NOTE]
>
>Puede definir un diseño distinto para cada [punto de interrupción](#layout-definitions-device-emulation-and-breakpoints) (tal y como determinan el tipo y la orientación del dispositivo emulado).

Para configurar el diseño de una cuadrícula interactiva implementada con el contenedor de diseño, debe usar el modo **Diseño**.

El modo **Diseño** puede iniciarse de dos formas.

* Mediante el uso del [menú de modo de la barra de herramientas](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-modes) y seleccionando el modo **Diseño**.
   * Seleccione el modo **Diseño** del mismo modo que si desea cambiar al modo **Editar** o **Segmentación**.
   * El modo **Diseño** se mantiene y no abandona el modo **Diseño** hasta que se selecciona otro modo a través del selector correspondiente.
* Al [editar un componente individual.](/help/sites-cloud/authoring/fundamentals/editing-content.md#edit-component-layout)
   * Mediante la opción **Diseño** del menú de acciones rápidas del componente, puede cambiar al modo **Diseño**.
   * El modo **Diseño** se mantiene durante la edición del componente, y se vuelve a acceder al modo **Editar** en cuanto el enfoque cambia a otro componente.

En el modo de diseño, puede ejecutar una serie de acciones a una cuadrícula:

* Redimensionar los componentes del contenido utilizando los puntos azules. Al redimensionar siempre se hará un ajuste a la cuadrícula. Al redimensionar se mostrará la cuadrícula de fondo como referencia para la alineación: 

   ![Cambiar el tamaño de los componentes](/help/sites-cloud/authoring/assets/responsive-layout-resizing.png)

   >[!NOTE]
   >
   >Se mantendrán las proporciones y relaciones al cambiar el tamaño de componentes como **Imágenes**.

* Haga clic o toque un componente de contenido. La barra de herramientas le permite efectuar las siguientes acciones:
   * **Principal**: le permite seleccionar todos los componentes del contenedor de diseños para efectuar acciones en conjunto.
   * **Flotar a una línea nueva**: se mueve el componente a una línea nueva, según el espacio disponible en la cuadrícula.
   * **Ocultar componente**: el componente se hace invisible (puede restaurarse desde la barra de herramientas del contenedor de diseños).

   ![Ocultar componente](/help/sites-cloud/authoring/assets/responsive-layout-hide.png)

* En el modo **Diseño** puede pulsar o hacer clic en **Arrastrar componentes aquí** para seleccionar el componente completo. Esto hará que se muestre la barra de herramientas de este modo.

   La barra de herramientas mostrará distintas opciones en función del estado del componente del diseño y de los componentes que pertenecen a él. Por ejemplo:

   * **Principal**: seleccione el componente principal.

      ![Botón Principal](/help/sites-cloud/authoring/assets/responsive-layout-parent-button.png)

   * **Mostrar componentes ocultos**: permite mostrar todos los componentes o cada componente por separado. El número indica cuántos componentes ocultos existen en ese momento. El contador muestra cuántos componentes hay ocultos.

      ![Botón Mostrar componentes ocultos](/help/sites-cloud/authoring/assets/responsive-layout-show-button.png)

   * **Revertir diseño del punto de interrupción**: permite recuperar el diseño predeterminado. Es decir, no se aplicará ningún diseño personalizado.

      ![Botón Revertir diseño de punto de interrupción](/help/sites-cloud/authoring/assets/responsive-layout-revert-button.png)

   * **Flotar hasta una nueva línea**: suba el componente una posición si el espacio lo permite.

      ![Botón Flotar a una línea nueva](/help/sites-cloud/authoring/assets/responsive-layout-float-button.png)

   * **Ocultar componente**: oculte el componente actual.

      ![Ocultar botón de componente](/help/sites-cloud/authoring/assets/responsive-layout-hide-button.png)
   >[!NOTE]
   >
   >En el ejemplo anterior, las acciones de flotar y ocultar están disponibles porque este contenedor de diseño está anidado en un contenedor de diseño principal.

   * **Mostrar los componentes** 
Seleccione los componentes principales para mostrar la barra de herramientas de acciones con la 
Opción **Mostrar componentes ocultos**. En este ejemplo, hay dos componentes ocultos.

      ![Mostrar componentes](/help/sites-cloud/authoring/assets/responsive-layout-unhide.png)
   Si se selecciona la opción **Mostrar componentes ocultos**, se mostrarán en azul los componentes que están ocultos actualmente en sus posiciones originales.

   ![Botón Restaurar todo](/help/sites-cloud/authoring/assets/responsive-layout-restore-all.png)

   La selección de la opción **Restaurar todo** permitirá que se muestren todos los componentes ocultos.
