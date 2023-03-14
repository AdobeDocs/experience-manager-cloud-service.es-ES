---
title: Herramientas y entorno de creación
description: El entorno de creación AEM ofrece varios mecanismos para organizar y editar el contenido
exl-id: cc3bd4cf-93bd-429d-9a2a-4a02a7b42f7c
source-git-commit: 47910a27118a11a8add6cbcba6a614c6314ffe2a
workflow-type: tm+mt
source-wordcount: '2157'
ht-degree: 100%

---

# Herramientas y entorno de creación {#authoring-the-environment-and-tools}

El entorno de creación AEM ofrece varios mecanismos para organizar y editar el contenido. Se puede acceder a las herramientas desde varios editores de páginas y consolas.

## Administración del sitio {#managing-your-site}

La consola **Sitios** le permite desplazarse por su sitio web y administrarlo mediante la barra de encabezado, la barra de herramientas, los iconos de acción (aplicables al recurso seleccionado), las rutas de exploración y, si se seleccionan, los carriles secundarios (por ejemplo, referencias y cronología).

Por ejemplo, la vista de columna:

![Vista de columna](/help/sites-cloud/authoring/assets/column-view.png)

## Edición del contenido de una página {#editing-page-content}

Puede editar una página con el editor. Por ejemplo:

`http://<host>:<port>/editor.html/content/wknd/en/sports/la-skateparks.html`

![Editor de página](/help/sites-cloud/authoring/assets/page-editor.png)

>[!NOTE]
>
>La primera vez que abra una página para editarla, aparecerá una serie de diapositivas donde se verán las funciones.
>
>Si lo desea, puede omitir la visita y repetirla cuando le convenga seleccionando una opción del menú **Información de página**.

## Acceso a la Ayuda   {#accessing-help}

Al editar una página, se puede acceder a la **Ayuda** desde los siguientes puntos:

* El selector [**Información de página**](/help/sites-cloud/authoring/fundamentals/page-properties.md#page-properties) muestra las diapositivas introductorias (tal y como se muestran la primera vez que se accede al editor).
* El cuadro de diálogo [Configuración](/help/sites-cloud/authoring/fundamentals/editing-content.md#component-toolbar) de componentes específicos (utilizando el icono ? en la barra de herramientas del cuadro de diálogo), que ofrece ayuda contextual.

Encontrará [más recursos relacionados con la ayuda en las consolas](/help/sites-cloud/authoring/getting-started/basic-handling.md#accessing-help).

## Navegador de componentes   {#components-browser}

Los componentes son la base del contenido de AEM. Puede colocar varios componentes en una página y configurar sus opciones para crear la página de contenido con AEM.

El navegador de componentes muestra todos los componentes que se pueden utilizar en la página actual. Se pueden arrastrar a la ubicación apropiada y editarse para añadir contenido.

El navegador de componentes es una pestaña del panel lateral (junto con el [explorador de recursos](#assets-browser) y el [árbol de contenido](#content-tree)). Para abrir (o cerrar) el panel lateral, utilice el icono de la parte superior izquierda de la barra de herramientas:

![Alternar panel lateral](/help/sites-cloud/authoring/assets/side-panel-toggle.png)

Cuando abra el panel lateral, se deslizará para abrirse de izquierda a derecha (seleccione la pestaña **Componentes** si es necesario). Cuando se abra, podrá navegar por todos los componentes disponibles para su página.

El aspecto y el control dependerán del tipo de dispositivo que esté utilizando:

* **Dispositivo móvil (por ejemplo, iPad)**

   El navegador de componentes cubre totalmente la página que se esté editando.

   Para añadir un componente a la página mantenga pulsado el componente requerido y muévalo a la derecha; el navegador de componentes se cerrará para volver a mostrar la página, donde puede colocar el componente.

   ![Navegador de componentes en dispositivos móviles](/help/sites-cloud/authoring/assets/component-browser-mobile.png)

* **Dispositivo de escritorio**

   El navegador de componentes se abre en la parte izquierda de la ventana.

   Para añadir un componente a la página, haga clic en el componente requerido y arrástrelo a la ubicación que desee.

   ![Navegador de componentes en dispositivos de escritorio](/help/sites-cloud/authoring/assets/component-browser-desktop.png)

   Los componentes se representan mediante los siguientes elementos:

   * Nombre del componente
   * Grupo de componentes (en gris)
   * Icono o abreviatura
      * Los iconos de componentes estándar son monocromo.
      * Las abreviaturas siempre están formadas por los dos primeros caracteres del nombre del componente.

   Desde la barra de herramientas superior del explorador de **componentes**, puede realizar las siguientes acciones:

   * Filtrar componentes por su nombre.
   * Restringir la visualización a un grupo específico mediante la selección desplegable.

   Para obtener una descripción más detallada del componente, puede hacer clic o pulsar el icono de información situado junto al componente en el navegador de **componentes** (si está disponible). Por ejemplo, para el **fragmento de contenido**:

   ![Información del explorador de componentes](/help/sites-cloud/authoring/assets/component-browser-information.png)

   Para obtener más información sobre los componentes disponibles, consulte la [Consola de componentes](/help/sites-cloud/authoring/features/components-console.md).

>[!NOTE]
>
>Se detectará un dispositivo móvil si la anchura es inferior a 1024 píxeles. Esto puede ser también una ventana de escritorio pequeña.

## Navegador de recursos {#assets-browser}

El navegador de recursos muestra todos los [recursos](/help/assets/home.md) que se pueden utilizar directamente en la página actual.

El explorador de recursos es una pestaña del panel lateral que está situada junto al [explorador de componentes](#components-browser) y al [árbol de contenido](#content-tree). Para abrir o cerrar el panel lateral, utilice el icono de la parte superior izquierda de la barra de herramientas:

![Alternar panel lateral](/help/sites-cloud/authoring/assets/side-panel-toggle.png)

Cuando abra el panel lateral, se deslizará para abrirse de izquierda a derecha. Seleccione la pestaña **Recursos** si es necesario.

![Botón Explorador de recursos](/help/sites-cloud/authoring/assets/assets-browser-button.png)

Cuando el navegador de recursos esté abierto, podrá explorar todos los recursos disponibles para la página. Si es necesario, puede utilizarse el desplazamiento indefinido para ampliar la lista.

![Navegador de recursos](/help/sites-cloud/authoring/assets/assets-browser.png)

Para añadir un recurso a la página, selecciónelo y arrástrelo a la ubicación deseada, que puede ser:

* Un componente existente del tipo adecuado.
   * Por ejemplo, puede arrastrar un recurso de tipo imagen hacia un componente de imagen.
* Un [marcador de posición](/help/sites-cloud/authoring/fundamentals/editing-content.md#component-placeholder) en el sistema de párrafos para crear un componente nuevo del tipo correspondiente.
   * Por ejemplo, puede arrastrar un recurso de tipo imagen al sistema de párrafos para crear un componente de imagen.

>[!NOTE]
>
>Esta opción está disponible para determinados recursos y tipos de componente. Consulte [Inserción de un componente con el navegador de recursos](/help/sites-cloud/authoring/fundamentals/editing-content.md#inserting-a-component-using-the-assets-browser) para obtener más información detallada.

Desde la barra de herramientas superior del navegador de recursos puede filtrar los recursos por:

* Nombre
* Ruta
* Tipos de recursos como imágenes, vídeos, documentos, párrafos, fragmentos de contenido y fragmentos de experiencias.
* Características del recurso como orientación y estilo.
   * Disponible solo para determinados tipos de recursos

El aspecto y el control dependerán del tipo de dispositivo que esté utilizando:

* **Dispositivo móvil**

   El navegador de recursos cubre totalmente la página que se esté editando.

   Para añadir un recurso a la página mantenga pulsado el recurso requerido y muévalo a la derecha; el navegador de recursos se cerrará para volver a mostrar la página, donde puede agregar el recurso al componente deseado.

   ![Explorador de recursos en dispositivos móviles](/help/sites-cloud/authoring/assets/assets-browser-mobile.png)

* **Dispositivo de escritorio**

   El navegador de recursos se abre en la parte izquierda de la ventana.

   Para añadir un recurso a la página, haga clic en el recurso en cuestión y arrástrelo al componente o a la ubicación correspondiente.

   ![Explorador de recursos en dispositivos de escritorio](/help/sites-cloud/authoring/assets/assets-browser-desktop.png)

>[!NOTE]
>
>Se detectará un dispositivo móvil cuando la anchura sea menor a 1024 píxeles; es decir, también cuando la ventana de escritorio sea pequeña.

Si necesita realizar rápidamente un cambio en un recurso, puede iniciar el [editor de recursos](/help/assets/manage-digital-assets.md) directamente desde el explorador de recursos haciendo clic en el icono de edición que se muestra al lado del nombre del recurso.

![Botón Editar recursos](/help/sites-cloud/authoring/assets/asset-edit-button.png)

## Árbol de contenido {#content-tree}

El **árbol de contenido** proporciona información general de todos los componentes de la página formando una jerarquía para que pueda ver a simple vista cómo está compuesta la página.

El árbol de contenido es una pestaña del panel lateral (junto con el explorador de recursos y componentes). Para abrir (o cerrar) el panel lateral, utilice el icono de la parte superior izquierda de la barra de herramientas:

![Botón Árbol de contenido](/help/sites-cloud/authoring/assets/content-tree-button.png)

Cuando abra el panel lateral, se deslizará para abrirse (de izquierda a derecha). Seleccione la pestaña **Árbol de contenido** si es necesario. Cuando la abra, podrá ver una representación en forma de árbol de la página o la plantilla, para que resulte más fácil de entender cómo está estructurado jerárquicamente su contenido. Además, en una página compleja, hace que sea más fácil saltar de un componente de página a otro.

![Árbol de contenido](/help/sites-cloud/authoring/assets/content-tree-editor.png)

Una página puede estar compuesta fácilmente por muchos componentes del mismo tipo, por lo que el árbol de contenido (componentes) muestra un texto descriptivo (en gris) después del nombre del tipo de componente (en negro). El texto descriptivo viene de las propiedades comunes del componente, como el título o el texto.

Los tipos de componente se mostrarán en el idioma del usuario, mientras que el texto con la descripción del componente se muestra en el idioma de la página.

Al hacer clic en el elemento situado junto a un componente, se contraerá o desplegará dicho nivel.

![Ampliación de la cadena del árbol de contenido](/help/sites-cloud/authoring/assets/content-tree-chevron.png)

Si hace clic en el componente, se resalta en el editor de páginas. Las acciones disponibles dependen del estado de la página:

* Por ejemplo, una página básica:

   ![Árbol de contenido resaltado](/help/sites-cloud/authoring/assets/content-tree-highlighted.png)

   Los componentes de una página básica tienen las opciones habituales.

   Si el componente en el que se hace clic en el árbol es editable, aparecerá un icono de una llave inglesa a la derecha del nombre. Al hacer clic en este icono, se iniciará directamente el cuadro de diálogo Editar del componente.

   ![Botón Editar árbol de contenido](/help/sites-cloud/authoring/assets/content-tree-edit.png)

* Una página que forma parte de una [Live Copy](/help/sites-cloud/administering/msm/overview.md), donde los componentes se heredan de otra página.

>[!NOTE]
>
>Si edita una página en un dispositivo móvil, el árbol de contenido no está disponible (si el valor de la anchura del explorador es inferior a 1024 píxeles).

## Fragmentos: navegador de contenido asociado {#fragments-associated-content-browser}

Si la página contiene fragmentos de contenido, también podrá acceder al [navegador de contenido asociado](/help/sites-cloud/authoring/fundamentals/content-fragments.md#using-associated-content). 

## Referencias {#references}

**Referencias** muestra las conexiones a la página seleccionada:

* Planes
* Lanzamientos
* Live Copies
* Copias de idioma
* Vínculos entrantes
* Utilización del componente de referencia: contenido prestado

Abra la consola en cuestión, desplácese hasta el recurso y abra **Referencias** con el procedimiento siguiente:

![Opción Referencias](/help/sites-cloud/authoring/assets/references.png)

[Seleccione el recurso necesario](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources) para mostrar una lista de tipos de datos relevantes para ese recurso:

![Detalles de referencias](/help/sites-cloud/authoring/assets/references-detail.png)

Seleccione el tipo de referencia apropiado para obtener más información. En determinadas situaciones, hay disponibles acciones adicionales al seleccionar una referencia específica, como:

* La opción **Vínculos entrantes** proporciona una lista de páginas que hacen referencia a la página, así como un acceso directo a la opción **Editar** de una de esas páginas, al seleccionar un vínculo específico
* Instancias de contenido prestado mediante el componente de **referencia**; desde aquí puede navegar hasta la página de referencia o a la que se hace referencia
* [Lanzamientos](/help/sites-cloud/authoring/launches/overview.md), que proporciona acceso a lanzamientos relacionados.
* [Live Copies](/help/sites-cloud/administering/msm/overview.md) muestra las rutas de todas las Live Copies que se basan en el recurso seleccionado.
* [Modelo](/help/sites-cloud/administering/msm/best-practices.md), proporciona detalles y diversas acciones
* [Copias de idiomas](/help/sites-cloud/administering/translation/managing-projects.md#creating-translation-projects-using-the-references-panel), proporciona detalles y diversas acciones

## Eventos: línea de tiempo {#events-timeline}

Para obtener los recursos adecuados (por ejemplo, páginas de la consola **Sitios** o activos de la consola **Activos**) se [puede utilizar la cronología para mostrar la actividad reciente de cualquier elemento seleccionado](/help/sites-cloud/authoring/getting-started/basic-handling.md#timeline).

Abra la consola en cuestión, desplácese hasta el recurso y abra **Cronología** con el procedimiento siguiente:

![Opción cronología](/help/sites-cloud/authoring/assets/timeline.png)

[Seleccione el recurso en cuestión](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources) mediante **Mostrar todo** o **Actividades** para enumerar las acciones recientes en los recursos seleccionados:

![Detalles de la cronología](/help/sites-cloud/authoring/assets/timeline-detail.png)

## Información de la página {#page-information}

La Información de página (icono de ecualizador) abre un menú que también muestra detalles de la última edición y la última publicación. En función de las características de la página, del sitio y de su instancia, habrá más o menos opciones disponibles:

![Opción Información de página](/help/sites-cloud/authoring/assets/page-information.png)

* [Abrir propiedades](/help/sites-cloud/authoring/fundamentals/page-properties.md)
* [Desplegar página](/help/sites-cloud/administering/msm/overview.md#msm-from-the-ui)
* [Iniciar flujo de trabajo](/help/sites-cloud/authoring/workflows/applying.md#starting-a-workflow-from-the-page-editor)
* [Bloquear página](/help/sites-cloud/authoring/fundamentals/editing-content.md#locking-a-page)
* [Publicar página](/help/sites-cloud/authoring/fundamentals/publishing-pages.md#publishing-pages-1)
* [Cancelar la publicación de la página](/help/sites-cloud/authoring/fundamentals/publishing-pages.md#unpublishing-pages)
* [Editar plantilla](/help/sites-cloud/authoring/features/templates.md)
* [Ver como aparece publicado](/help/sites-cloud/authoring/fundamentals/editing-content.md#view-as-published)
* [Ver en administración](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources)
* [Ayuda](/help/sites-cloud/authoring/getting-started/basic-handling.md#accessing-help)
* [Promocionar lanzamiento](/help/sites-cloud/authoring/launches/promoting.md) (solo si la página es nueva)

Además, **Información de página** puede proporcionar acceso a análisis y recomendaciones cuando es necesario.

## Modos de página   {#page-modes}

Al editar una página, existen modos que permiten acciones diferentes:

* [Editar](/help/sites-cloud/authoring/fundamentals/editing-content.md): el modo que se debe emplear al editar el contenido de la página.
* [Diseño](/help/sites-cloud/authoring/features/responsive-layout.md): permite crear y editar su diseño interactivo en función del dispositivo (si la página está basada en un contenedor de diseños).
* [Segmentación:](/help/sites-cloud/authoring/personalization/targeted-content.md) aumente la relevancia del contenido mediante la segmentación y efectuando mediciones en todos los canales.
* [Deformación de tiempo](/help/sites-cloud/authoring/features/page-versions.md#timewarp): le permite ver el estado de las páginas en un punto específico en el tiempo.
* [Estado de Live Copy](/help/sites-cloud/authoring/fundamentals/editing-content.md#live-copy-status): le permite echar un vistazo al estado de la Live Copy y ver los componentes que se han heredado o no.
* [Modo de desarrollador](/help/implementing/developing/tools/developer-mode.md)
* [Vista previa](/help/sites-cloud/authoring/fundamentals/editing-content.md#previewing-pages): se utiliza para ver la página tal como se mostrará en el entorno de publicación; o para navegar mediante vínculos en el contenido. 
* [Anotar:](/help/sites-cloud/authoring/fundamentals/annotations.md) se utiliza para añadir o ver anotaciones en la página.

Puede acceder a estas opciones a través de los iconos de la esquina superior derecha; el icono cambiará para reflejar el modo que esté utilizando:

![Modos de página](/help/sites-cloud/authoring/assets/page-modes.png)

>[!NOTE]
>
>* En función de las características de la página, es posible que algunos modos no estén disponibles.
>* El acceso a algunos modos requiere los permisos/privilegios correspondientes.
>* El modo de desarrollador no está disponible en dispositivos móviles debido a limitaciones de espacio.
>* Existe un [método abreviado de teclado](/help/sites-cloud/authoring/getting-started/keyboard-shortcuts.md) (`Ctrl-Shift-M`) para alternar entre **Vista previa** y el modo seleccionado actualmente (por ejemplo, **Editar**, **Diseño**, etc.).
>


## Selección de la ruta {#path-selection}

A menudo, durante la creación, es necesario seleccionar otro recurso, como cuando se define un vínculo a otra página o recurso o bien cuando se selecciona una imagen. Para poder seleccionar una ruta con facilidad, los [campos de rutas](#path-fields) ofrecen la opción de completado automático y el [navegador de rutas](#path-browser) permite una selección más sólida.

### Campos de rutas   {#path-fields}

El ejemplo que se utiliza aquí a modo de ilustración se corresponde con el componente de imagen. Para obtener más información sobre el uso y edición de componentes, consulte [Componentes para la creación de páginas](/help/sites-cloud/authoring/fundamentals/components.md).

Los campos de rutas de acceso disponen de las funciones de completado automático y de predicción de texto para que la localización de recursos resulte más sencilla.

Al hacer clic en el botón **Abrir cuadro de diálogo de selección**, en el campo de rutas de acceso se abrirá el cuadro de diálogo del [navegador de rutas de acceso](#path-browser), en el que dispondrá de opciones de selección más detalladas.

![Botón Abrir cuadro de diálogo de selección](/help/sites-cloud/authoring/assets/open-selection-dialog-button.png)

También puede empezar a escribir en el campo de rutas, y AEM le ofrecerá rutas coincidentes a medida que vaya escribiendo.

![Botón Abrir cuadro de diálogo de selección](/help/sites-cloud/authoring/assets/path-selection-completion.png)

### Navegador de rutas {#path-browser}

El navegador de rutas está organizado como la [vista de columna](/help/sites-cloud/authoring/getting-started/basic-handling.md#column-view) de la consola Sitios, lo que permite efectuar una selección más detallada de los recursos.

![Navegador de rutas](/help/sites-cloud/authoring/assets/path-browser.png)

* Una vez que se selecciona un recurso, el botón **Seleccionar** de la esquina superior derecha del cuadro de diálogo se activa. Toque o haga clic para confirmar la selección o en **Cancelar** para anular la operación.
* Si el contexto permite la selección de varios recursos, al seleccionar un recurso también se activa el botón **Seleccionar**, pero también se agrega un recuento del número de recursos seleccionados a la esquina superior derecha de la ventana. Haga clic en la **X** junto al número para anular toda la selección.
* Al navegar por el árbol, la ubicación se refleja en la ruta de exploración situada en la parte superior del cuadro de diálogo. Las rutas de exploración también se pueden usar para saltar rápidamente dentro de la jerarquía del recurso.
* El campo de búsqueda situado en la parte superior del cuadro de diálogo se puede usar en cualquier momento. Haga clic en la **X** que aparece en el campo de búsqueda para borrar la búsqueda.
* Para limitar la búsqueda, puede mostrar las opciones de filtro y filtrar los resultados en función de una ruta determinada.

   ![Opción Filtros](/help/sites-cloud/authoring/assets/filters-option.png)

## Métodos abreviados de teclado {#keyboard-shortcuts}

Hay varios [métodos abreviados del teclado](/help/sites-cloud/authoring/getting-started/keyboard-shortcuts.md) disponibles.
