---
title: Gestión básica
description: Familiarícese con el desplazamiento por AEM y su uso básico
exl-id: ae87a63a-c6d3-4220-ab3d-07a20b21b93b
source-git-commit: ca849bd76e5ac40bc76cf497619a82b238d898fa
workflow-type: ht
source-wordcount: '2994'
ht-degree: 100%

---

# Gestión básica {#basic-handling}

Este documento se ha diseñado para ofrecer una descripción general de la gestión básica cuando se utiliza el entorno de creación AEM. Utiliza la consola **Sitios** como base. 

>[!NOTE]
>
>* Algunas funciones no están disponibles en todas las consolas y determinadas consolas pueden disponer de funciones adicionales. La información específica sobre consolas concretas y sus funciones se tratará en más detalle en otras páginas.
>* Los métodos abreviados del teclado están disponibles mediante AEM, sobre todo al [utilizar las consolas](/help/sites-cloud/authoring/getting-started/keyboard-shortcuts.md) y [al editar páginas](/help/sites-cloud/authoring/fundamentals/keyboard-shortcuts.md).


## Una interfaz con capacidad táctil {#a-touch-enabled-ui}

La interfaz de usuario de AEM tiene capacidad táctil. Una interfaz con capacidad táctil le permite utilizar el tacto para interactuar con el software mediante gestos como pulsar, pulsar y mantener o deslizar el dedo. Como la interfaz de usuario de AEM es táctil, puede utilizar los gestos táctiles en dispositivos táctiles como el teléfono móvil o la tablet. Sin embargo, también están disponibles las acciones del ratón en un dispositivo de escritorio tradicional, lo que le proporciona flexibilidad en la forma en que elige crear el contenido.

## Primeros pasos {#first-steps}

Inmediatamente después del inicio de sesión llega al [panel Navegación](#navigation-panel). Al hacer clic en una de las opciones, se abre la consola correspondiente.

![Panel de navegación](/help/sites-cloud/authoring/assets/navigation.png)

Para comprender bien el uso básico de AEM, este documento se basa en la consola **Sitios**. Pulse o haga clic en **Sitios** para comenzar.

## Navegación de productos    {#product-navigation}

Cuando un usuario accede por primera vez a una consola, se inicia un tutorial de navegación por el producto. Dedíquele un momento para ver una buena descripción general del funcionamiento básico de AEM.

![Tutorial de navegación](/help/sites-cloud/authoring/assets/tutorial.png)

Toque o haga clic en **Siguiente** para avanzar a la siguiente página de la descripción general. Para cerrar, pulse o haga clic en **Cerrar**, o pulse o haga clic fuera del cuadro de diálogo de la descripción general.

La descripción general se reiniciará la próxima vez que acceda a una consola, a menos que vea todas las diapositivas o marque la opción **No volver a mostrar esto**.

## Navegación global {#global-navigation}

Puede navegar entre las consolas con el panel de navegación global. Se activa como un desplegable a pantalla completa cuando toca o hace clic en el vínculo Adobe Experience Manager, en la parte superior izquierda de la pantalla.

Para volver a la ubicación anterior, puede cerrar el panel de navegación global tocando o haciendo clic en **Cerrar**.

![Barra superior del panel de navegación](/help/sites-cloud/authoring/assets/navigation-bar.png)

La navegación global dispone de dos paneles, representados por iconos en el lado izquierdo de la pantalla:

* **[Navegación](#navigation-panel)**: se representa mediante una brújula    y el panel predeterminado al iniciar sesión en AEM.
* **[Herramientas](#tools-panel)**: se representa mediante un martillo

Las opciones disponibles en estos paneles se describen a continuación.

### Panel de navegación    {#navigation-panel}

El panel Navegación:

![Panel de navegación](/help/sites-cloud/authoring/assets/navigation.png)

El título de la pestaña del navegador se actualizará para reflejar su ubicación a medida que navegue por las consolas y el contenido.

En Navegación, las consolas disponibles son:

| Consola | Función |
|---|---|
| Proyectos | La consola Proyectos le proporciona acceso directo a sus proyectos. [Los proyectos son paneles virtuales](/help/sites-cloud/authoring/projects/overview.md) que se pueden utilizar para crear un equipo. A continuación, puede proporcionar a ese equipo acceso a recursos, flujos de trabajo y tareas, lo que permite a las personas colaborar para lograr un objetivo común. |
| Sitios | La consola Sitios le permite [crear, ver y administrar sitios web](/help/sites-cloud/authoring/fundamentals/organizing-pages.md) que se ejecuten en su instancia de AEM. Mediante esta consola puede crear, editar, copiar, mover y eliminar páginas, iniciar flujos de trabajo y publicar páginas. |
| Fragmentos de experiencias | Un [fragmento de experiencia](/help/sites-cloud/authoring/fundamentals/experience-fragments.md) es una experiencia independiente que puede reutilizarse en diversos canales y tener variaciones, de manera que se evita el problema de copiar y pegar repetidas veces experiencias o partes de experiencias. |
| Assets | La consola Recursos le permite importar y administrar [recursos digitales, como imágenes, vídeos, documentos y archivos de audio](/help/assets/overview.md). Estos recursos se pueden utilizar en cualquier sitio web que ejecute la misma instancia de AEM. También puede crear y administrar [Fragmentos de contenido](/help/assets/content-fragments/content-fragments.md) desde la consola Recursos. |
| Personalización | [Esta consola ofrece un marco de herramientas para crear contenido dirigido y presentar experiencias personalizadas.](/help/sites-cloud/authoring/personalization/overview.md) |
| Fragmentos de contenido | [Los fragmentos de contenido](/help/sites-cloud/administering/content-fragments/content-fragments.md) permiten diseñar, crear, depurar y publicar contenido independiente de cualquier página. Permiten preparar contenido estructurado listo para su uso en varias ubicaciones/en varios canales, y es ideal tanto para la creación de páginas como para la entrega sin encabezado. |

## Panel de herramientas {#tools-panel}

En el panel Herramientas hay un panel lateral que contiene una serie de categorías, que agrupan consolas de herramientas similares. Las consolas Herramientas permiten acceder a toda una serie de consolas y herramientas personalizadas que le ayudan a administrar sus sitios web, recursos digitales y otros aspectos de su repositorio de contenido. <!--The [Tools consoles](/help/sites-administering/tools-consoles.md) provide access to a number of specialized tools and consoles that help you administer your websites, digital assets, and other aspects of your content repository.-->

![Panel de herramientas](/help/sites-cloud/authoring/assets/tools-panel.png)

## Encabezado {#the-header}

El encabezado siempre está presente en la parte superior de la pantalla. Aunque la mayoría de las opciones del encabezado no varían en todo el sistema, algunas dependen del contexto.

![Encabezado de navegación](/help/sites-cloud/authoring/assets/navigation-bar.png)

* [Navegación global](#global-navigation)

   Seleccione el vínculo **Adobe Experience Manager** para navegar entre consolas.

   ![Navegación global](/help/sites-cloud/authoring/assets/global-navigation.png)

* [Búsqueda](/help/sites-cloud/authoring/getting-started/search.md)

   ![Icono de búsqueda](/help/sites-cloud/authoring/assets/search-icon.png)

   También puede utilizar la [tecla de método abreviado](/help/sites-cloud/authoring/getting-started/keyboard-shortcuts.md) `/` (barra inclinada) para iniciar una búsqueda desde cualquier consola.

* [Soluciones](https://www.adobe.com/es/experience-cloud.html)

   ![Botón Soluciones](/help/sites-cloud/authoring/assets/solutions.png)

* [Ayuda](#accessing-help)

   ![Botón Ayuda](/help/sites-cloud/authoring/assets/help.png)

* [Notificaciones](/help/sites-cloud/authoring/getting-started/inbox.md)

   ![Botón Notificaciones](/help/sites-cloud/authoring/assets/notifications.png)

   Este icono se mostrará con la cantidad de notificaciones incompletas asignadas actualmente.

* [Propiedades del usuario](/help/sites-cloud/authoring/getting-started/account-environment.md)

   ![Botón Propiedades del usuario](/help/sites-cloud/authoring/assets/user-properties.png)

* [Selector de raíl](#rail-selector)

   ![Botón Selector de carril](/help/sites-cloud/authoring/assets/rail-selector.png)

   Las opciones presentadas dependen de la consola actual. Por ejemplo, en **Sitios** puede seleccionar contenido solamente (el valor predeterminado), la cronología, las referencias o el panel lateral de filtro.

   ![Ejemplo de selector de carril](/help/sites-cloud/authoring/assets/rail-selector-example.png)

* Rutas de exploración

   ![Rutas de exploración en la barra de navegación](/help/sites-cloud/authoring/assets/breadcrumbs-navigation.png)

   Las rutas de exploración, que se encuentran en el centro del raíl y siempre muestran la descripción del elemento seleccionado, le permiten desplazarse dentro de una consola específica. Desde la consola **Sitios** puede desplazarse por los niveles de su sitio web.

   Solo tiene que hacer clic en el texto de la ruta de exploración para ver una lista desplegable que enumera los niveles de la jerarquía del elemento seleccionado. Haga clic en una entrada para ir a esa ubicación.

   ![Ejemplo de rutas de exploración expandidas](/help/sites-cloud/authoring/assets/breadcrumbs-example.png)

* Botón **Crear**

   ![Botón Crear](/help/sites-cloud/authoring/assets/create.png)

   Una vez que se ha hecho clic, las opciones que se muestran son apropiadas para la consola o el contexto.

* [Vistas](#viewing-and-selecting-resources)

   El icono de vista se encuentra en el extremo derecho de la barra de herramientas de AEM. Como también indica la vista actual, este puede cambiar. Por ejemplo, en la vista predeterminada, la **vista de columna** muestra lo siguiente:

   ![Botón Vistas](/help/sites-cloud/authoring/assets/views-button.png)

   Puede cambiar entre la vista de columna, la vista de tarjeta y la vista de lista. Tenga en cuenta que en la vista de lista también se muestra la configuración de la vista.

   ![Vistas](/help/sites-cloud/authoring/assets/view.png)

   >[!NOTE]
   >
   >La opción **Ver configuración** solo está disponible en el modo **Vista de lista**.

* Navegación por teclado

   Puede navegar por un sitio web utilizando solo el teclado. Utiliza la funcionalidad estándar del navegador de la tecla **TAB** (u **OPT+TAB**) para desplazarlo entre los elementos de la página que se pueden enfocar.

   En la consola **Sites** hay una opción agregada para **Omitir al contenido principal**. Esto se vuelve visible a medida que se desplaza con el tabulador a través de las opciones de encabezado y acelera la navegación permitiéndole omitir los elementos estándar en la barra de herramientas (producto), y lo lleva directamente al contenido principal.

   ![Pasar al contenido principal](/help/sites-cloud/authoring/assets/skip-to-main-content.png)

## Acceso a la Ayuda   {#accessing-help}

Hay varios medios de ayuda disponibles:

* **Barra de herramientas de la consola**

   Según su ubicación, el icono **Ayuda** abrirá los recursos correspondientes.

   ![Icono de ayuda](/help/sites-cloud/authoring/assets/help-console.png)

* **Navegación**

   La primera vez que navega por el sistema, se muestra [una serie de diapositivas en que se presenta la navegación por AEM](#product-navigation).

   ![Tutorial](/help/sites-cloud/authoring/assets/tutorial.png)

* **Editor de página**

   La primera vez que edita una página, un conjunto de diapositivas presenta el editor de páginas.

   ![Tutorial del editor](/help/sites-cloud/authoring/assets/editor-tutorial.png)

   Desplácese por esta descripción general como haría en la [descripción general de navegación de producto](#product-navigation) al acceder por primera vez a una consola.

   En el menú [**Información de página** puede seleccionar **Ayuda**](/help/sites-cloud/authoring/fundamentals/environment-tools.md#accessing-help) para que se vuelva a mostrar esto en cualquier momento.

* **Consola Herramientas**

   Desde la consola **Herramientas** también puede acceder a los **recursos externos**:

   * **Documentación**: ver la documentación de Web Experience Management.
   * **Recursos de desarrollador**: recursos y descargas para desarrolladores.

   >[!NOTE]
   >
   >Puede acceder a una descripción general de las teclas de método abreviado disponibles en cualquier momento mediante la tecla de marcación rápida `?` (signo de interrogación) en una consola.
   >
   >Para obtener información general sobre todos los métodos abreviados del teclado, consulte la documentación siguiente:
   >
   >* [Métodos abreviados del teclado para editar páginas](/help/sites-cloud/authoring/fundamentals/keyboard-shortcuts.md)
   >* [Métodos abreviados del teclado para las consolas](/help/sites-cloud/authoring/getting-started/keyboard-shortcuts.md)


## Barra de herramientas Acciones {#actions-toolbar}

Siempre que se selecciona un recurso (por ejemplo, una página o un recurso), varias acciones aparecen indicadas en la barra de herramientas mediante iconos acompañados por un texto explicativo. Estas acciones dependen de lo siguiente:

* La consola actual
* El contexto actual
* Si se encuentra en el [modo de selección](#viewing-and-selecting-resources)

La acción disponible en la barra de herramientas cambia para reflejar las acciones que se pueden llevar a cabo en los elementos específicos seleccionados.

El modo de [seleccionar un recurso](#viewing-and-selecting-resources) depende de la vista.

Debido a las restricciones de espacio en algunas ventanas, es posible que la barra de herramientas supere rápidamente la longitud disponible. Cuando esto ocurre, aparecen opciones adicionales. Al tocar o hacer clic en el símbolo de elipsis (los tres puntos o **...**), se abre un selector desplegable con el resto de las acciones. Por ejemplo, después de seleccionar una página en la consola **Sitios**: 

![Opciones adicionales](/help/sites-cloud/authoring/assets/additional-options.png)

>[!NOTE]
>
>Los iconos individuales disponibles se documentan de acuerdo con la consola, la función o el escenario en cuestión.

## Acciones rápidas    {#quick-actions}

En la [vista de tarjeta](#card-view), determinadas acciones están disponibles como iconos de acción rápida, además de en la barra de herramientas. Los iconos de acción rápida aparecen disponibles para un único elemento cada vez, con lo que no es necesario preseleccionar. 

Las acciones rápidas se pueden ver al pasar el ratón (dispositivo de escritorio) por encima de la tarjeta de un recurso. Las acciones rápidas disponibles pueden depender de la consola y del contexto. Por ejemplo, estas son las acciones rápidas para una página de la consola **Sitios**:

![Opciones adicionales](/help/sites-cloud/authoring/assets/quick-actions.png)

## Visualización y selección de los recursos {#viewing-and-selecting-resources}

Conceptualmente, la visualización, la navegación y la selección son iguales en todas las vistas, pero existen pequeñas variaciones en el manejo, dependiendo de la vista utilizada.

Puede visualizar, navegar y seleccionar sus recursos (para efectuar una acción posterior) con cualquiera de las vistas disponibles, que se seleccionan mediante el icono en la parte superior derecha:

* [Vista de columna](#column-view)
* [Vista de tarjeta](#card-view)
* [Vista de lista   ](#list-view)

>[!NOTE]
>
>De forma predeterminada, en ninguna de las vistas los recursos de AEM Assets muestran como miniaturas las representaciones originales de los recursos. Un administrador puede utilizar superposiciones para configurar los recursos de AEM Assets de forma que muestren las representaciones originales como miniaturas.

### Selección de recursos    {#selecting-resources}

La selección de un recurso específico depende de la vista y el dispositivo combinados:

| Ver | Seleccionar opción táctil | Seleccionar escritorio | Anular la selección táctil | Anular la selección de escritorio |
|---|---|---|---|---|
| Columna | Pulsar la miniatura | Hacer clic en la miniatura | Pulsar la miniatura | Hacer clic en la miniatura |
| Tarjeta | Pulsar y mantener la tarjeta | Pasar el ratón y, a continuación, utilizar la marca de verificación de acción rápida | Pulsar la tarjeta | Hacer clic en la tarjeta |
| Lista | Pulsar la miniatura | Hacer clic en la miniatura | Pulsar la miniatura | Hacer clic en la miniatura |

#### Seleccionar todo {#select-all}

Puede seleccionar todos los elementos de cualquier vista haciendo clic en la opción **Seleccionar todo** situada en la esquina superior derecha de la consola.

* En **Vista de tarjeta**, se seleccionan todas las tarjetas.
* En **Vista de lista**, se seleccionan todos los elementos de la lista.
* En **Vista de columna**, se seleccionan todos los elementos de la columna situada más a la izquierda.

![Seleccionar todo](/help/sites-cloud/authoring/assets/select-all.png)

#### Anulación de selección de todo {#deselecting-all}

En todos los casos, el número de elementos que tiene seleccionados se muestra en la parte superior derecha de la barra de herramientas.

Para anular la selección de todos los elementos y salir del modo de selección:

* Pulse o haga clic en la **X** situada junto al recuento.
* Uso de la **tecla escape**

![Anular todas las selecciones](/help/sites-cloud/authoring/assets/deselect-all.png)

En todas las vistas, es posible anular la selección de todos los elementos presionando ESC en el teclado si utiliza un equipo de escritorio.

#### Ejemplo de selección {#selecting-example}

1. Por ejemplo, en la vista de tarjeta:

   ![Selección de vista de tarjeta](/help/sites-cloud/authoring/assets/card-view-select.png)

1. Una vez que haya seleccionado un recurso, el encabezado superior se cubre con [acciones de la barra de herramientas](#actions-toolbar) para proporcionar acceso a las acciones aplicables actualmente al recurso seleccionado.

   Para salir del modo de selección, pulse o haga clic en la **X** situada en la parte superior derecha o use la tecla **Esc**.

### Vista de columna {#column-view}

![Vista de columna](/help/sites-cloud/authoring/assets/column-view.png)

La vista de columna permite una navegación visual de un árbol de contenido mediante una serie de columnas en cascada. Esta vista le permite visualizar y recorrer la estructura de árbol de su sitio web.

Si selecciona un recurso en la columna más a la izquierda, en una columna a la derecha se mostrarán los recursos secundarios. A su vez, seleccionar un recurso en esta columna derecha mostrará los recursos secundarios en otra columna a la derecha, y así sucesivamente.

* Puede desplazarse hacia arriba y hacia abajo por el árbol tocando o haciendo clic en el nombre del recurso o en las comillas angulares a la derecha de este nombre.

   * El nombre del recurso y las comillas angulares se resaltarán cuando los toque o haga clic en ellos.
   * Los elementos secundarios del recurso que ha tocado o en el que ha hecho clic se muestran en la columna a la derecha de dicho recurso.
   * Si toca o hace clic en el nombre de un recurso sin elementos secundarios, sus detalles se muestran en la última columna.

* Si toca o hace clic en la miniatura, se selecciona el recurso.

   * Cuando se selecciona una miniatura, sobre ella se superpone una casilla de verificación y el nombre del recurso se muestra resaltado.
   * Los detalles del recurso seleccionado se mostrarán en la última columna.
   * La barra de herramientas de acciones estará disponible.

   Cuando en la vista de columna hay una página seleccionada, esta se muestra en la última columna, junto a los datos siguientes:

   * Título de página
   * Nombre de página (parte de la URL de la página)
   * La plantilla de la página se basa en
   * Detalles de la modificación
   * Idioma de la página
   * Detalles de publicación y previsualización


### Vista de tarjeta {#card-view}

![Vista de tarjeta](/help/sites-cloud/authoring/assets/card-view.png)

* La vista de tarjeta muestra tarjetas de información para cada elemento del nivel actual. Proporcionan información como:

   * Una representación visual del contenido de la página
   * El título de la página
   * Fechas importantes (como la de la última modificación o la última publicación)
   * Si la página está bloqueada u oculta, o si es parte de una Live Copy
   * Si procede, cuando tenga que realizar una acción como parte de un flujo de trabajo
      * Los marcadores que indican las acciones necesarias pueden estar relacionados con elementos en su [bandeja de entrada](/help/sites-cloud/authoring/getting-started/inbox.md).

* En esta vista también hay disponibles [acciones rápidas](#quick-actions) como la selección y otras acciones comunes, por ejemplo la edición.

   ![Acciones rápidas](/help/sites-cloud/authoring/assets/quick-actions.png)

* Se puede navegar hacia abajo en el árbol tocando o haciendo clic en las tarjetas (con cuidado de evitar las acciones rápidas), o hacia arriba de nuevo mediante las [rutas de exploración del encabezado](#the-header).

### Vista de lista    {#list-view}

![Vista de lista](/help/sites-cloud/authoring/assets/list-view.png)

* La vista de lista muestra información sobre cada recurso en el nivel actual.
* Puede navegar hacia abajo en el árbol tocando o haciendo clic en el nombre del recurso, y hacia arriba utilizando las [rutas de exploración en el encabezado](#the-header).
* Para seleccionar fácilmente todos los elementos de la lista, utilice la casilla de verificación que hay en la parte superior izquierda de la misma.

   ![Seleccionar todo en la vista de lista](/help/sites-cloud/authoring/assets/list-view-select-all.png)

   * Si todos los elementos de la lista están seleccionados, la casilla aparece marcada.

      * Toque o haga clic en la casilla para anular todas las selecciones.
   * Cuando solo hay seleccionados algunos elementos, aparece un signo menos.

      * Toque o haga clic en la casilla para seleccionarlo todo.
      * Toque o haga clic en la casilla de nuevo para anular todas las selecciones.


* Seleccione las columnas a mostrar mediante la opción **Ajustes de visualización**, que se encuentra debajo del botón Vistas. Las siguientes columnas están disponibles para la visualización:

   * **Nombre**: nombre de página, que puede resultar útil en un entorno de creación multilingüe, ya que forma parte de la dirección URL de la página y no cambia con el idioma
   * **Modificada**: fecha de la última modificación y el usuario que la efectuó
   * **Publicada**: estado de publicación
   * **Vista previa**: estado de la vista previa
   * **Plantilla**: plantilla en la que se basa la página
   * **Flujo de trabajo**: flujo de trabajo aplicado actualmente en la página. Tiene más información disponible al pasar el ratón o abrir la línea de tiempo.
   * **Análisis de la página**
   * **Visitantes únicos**
   * **Tiempo empleado en la página**

      ![Seleccionar columnas](/help/sites-cloud/authoring/assets/select-columns.png)
   De forma predeterminada se muestra la columna **Nombre**, que es parte de la dirección URL de la página. En algunos casos, el autor puede tener que acceder a páginas en un idioma distinto, y ver el nombre de las mismas (que no suele variar) puede suponer una gran ayuda si se desconoce el idioma de la página.

* Cambie el orden de los elementos mediante la barra vertical de puntos en la parte más a la derecha de cada elemento en la lista.

   >[!NOTE]
   >
   >Solo es posible cambiar el orden en una carpeta ordenada que tiene el valor `jcr:primaryType` establecido como `sling:OrderedFolder`.

   ![Orden de las columnas](/help/sites-cloud/authoring/assets/column-order.png)

   Toque o haga clic en la barra de selección vertical y arrastre el elemento hasta una nueva posición en la lista.

   ![Lista de pedidos](/help/sites-cloud/authoring/assets/order-list.png)

## Selector de carril {#rail-selector}

El **Selector de carril** está disponible en la parte superior izquierda de la ventana y las opciones que muestra dependen de tus consolas actuales.

![Selector de carril expandido](/help/sites-cloud/authoring/assets/rail-selector-expanded.png)

Por ejemplo, en la consola **Sitios** puede seleccionar solo contenido (el valor predeterminado), árboles de contenido, la cronología, referencias o el panel lateral de filtro.

Si se selecciona contenido solamente, después solo aparece el icono de raíl. Cuando se selecciona cualquier otra opción, el nombre de la opción aparece al lado del icono de raíl.

>[!NOTE]
>
>[Los métodos abreviados del teclado](/help/sites-cloud/authoring/getting-started/keyboard-shortcuts.md) están disponibles para cambiar rápidamente entre las opciones de visualización de raíl.

### Árbol de contenido {#content-tree}

El árbol de contenido se puede utilizar para desplazarse con rapidez por la jerarquía del sitio dentro del panel lateral y para ver mucha información sobre las páginas en la carpeta actual.

Al utilizar el panel lateral del árbol de contenido junto con una vista de lista o de tarjetas, los usuarios pueden ver fácilmente la estructura jerárquica del proyecto y navegar con facilidad por la estructura del contenido con el panel lateral del árbol de contenido, así como ver información de página detallada en la vista de lista.

![Árbol de contenido](/help/sites-cloud/authoring/assets/content-tree.png)

>[!NOTE]
>
>Una vez seleccionada una entrada en la vista de jerarquía, las teclas de flecha se pueden utilizar para desplazarse con rapidez por la jerarquía.
>
>Consulte los [métodos abreviados del teclado](/help/sites-cloud/authoring/getting-started/keyboard-shortcuts.md) para obtener más información.

### Escala de cronología {#timeline}

La cronología puede utilizarse para ver o iniciar eventos que se hayan producido en el recurso seleccionado. Para abrir la columna de cronología, utilice el selector del raíl:

![Árbol de cronología](/help/sites-cloud/authoring/assets/timeline.png)

La columna de línea de tiempo le permite:

* Ver varios eventos relacionados con el elemento seleccionado.

   * Los tipos de eventos se pueden seleccionar desde la lista desplegable:

      * Comentarios
      * [Anotaciones](/help/sites-cloud/authoring/fundamentals/annotations.md)
      * [Actividades](/help/sites-cloud/authoring/personalization/activities.md)
      * [Lanzamientos](/help/sites-cloud/authoring/launches/overview.md)
      * [Versiones](/help/sites-cloud/authoring/features/page-versions.md)
      * [Flujos de trabajo](/help/sites-cloud/authoring/workflows/overview.md)
         * Con la excepción de los flujos de trabajo transitorios, ya que para estos no se guarda información de historial <!--With the exception of [transient workflows](/help/sites-developing/workflows.md#transient-workflows) as no history information is saved for these-->
      * Mostrar todos

* Agregar o ver comentarios sobre el elemento seleccionado. El cuadro **Comentario** se muestra en la parte inferior de la lista de eventos. Si se escribe un comentario y se presiona Retorno, el comentario se registra. Se mostrará cuando seleccione **Comentarios** o **Mostrar todo**.

* Determinadas consolas tienen funciones adicionales. Por ejemplo, en la consola Sitios puede:

   * [Guardar una versión](/help/sites-cloud/authoring/features/page-versions.md)
   * [Iniciar un flujo de trabajo](/help/sites-cloud/authoring/workflows/applying.md)

Estas opciones están disponibles mediante las comillas angulares que hay junto al campo **Comentario**.

![Campo Comentario](/help/sites-cloud/authoring/assets/comments.png)

### Referencias {#references}

La sección **Referencias** muestra cualquier conexión con el recurso seleccionado. Por ejemplo, en la consola **Sitios**, [Referencias](/help/sites-cloud/authoring/fundamentals/environment-tools.md#references) muestra lo siguiente para páginas:

* [Lanzamientos](/help/sites-cloud/authoring/launches/overview.md#launches-in-references-sites-console)
* [Live Copies](/help/sites-cloud/administering/msm/overview.md#openingthelivecopyoverviewfromreferences)
* [Copias de idioma](/help/sites-cloud/administering/translation/preparation.md#seeing-the-status-of-language-roots)
* Referencias de contenido:

   * Vínculos de otras páginas a la página seleccionada.
   * Contenido que el componente de referencia extrae de la página seleccionada o que entrega en la misma.

![Ejemplo de referencias](/help/sites-cloud/authoring/assets/references-example.png)

### Sitio {#site}

**Sitio** muestra detalles de sitios [creados mediante una plantilla de sitio.](/help/sites-cloud/administering/site-creation/create-site.md)

![Carril del sitio](../assets/site-rail.png)

Consulte el documento [Uso del carril del sitio para administrar el tema del sitio](/help/sites-cloud/administering/site-creation/site-rail.md) para obtener más información sobre cómo puede utilizar el carril para administrar el [tema del sitio.](/help/sites-cloud/administering/site-creation/site-themes.md)

>[!TIP]
>
>Puede encontrar una descripción completa del proceso de creación de un nuevo sitio a partir de una plantilla y personalizar su tema en el [Recorrido de creación rápida de sitios.](/help/journey-sites/quick-site/overview.md)

### Filtro {#filter}

Se abrirá un panel similar al de [Buscar](/help/sites-cloud/authoring/getting-started/search.md) con filtros de ubicación apropiados ya establecidos, lo que le permite filtrar aún más el contenido que desea ver.

![Ejemplo de filtro](/help/sites-cloud/authoring/assets/filter.png)
