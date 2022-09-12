---
title: Estructura de la IU de AEM
description: La interfaz de usuario de AEM tiene varios principios subyacentes y está formada por varios elementos clave
exl-id: ac211716-d699-4fdb-a286-a0a1122c86c5
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '915'
ht-degree: 4%

---

# Estructura de la IU de AEM {#structure-of-the-aem-ui}

La interfaz de usuario de AEM tiene varios principios subyacentes y está formada por varios elementos clave:

## Consolas {#consoles}

### Diseño básico y cambio de tamaño {#basic-layout-and-resizing}

La interfaz de usuario se ocupa de los dispositivos móviles y de escritorio, aunque en lugar de crear dos estilos, AEM utiliza un estilo que funciona para todas las pantallas y todos los dispositivos.

Todos los módulos utilizan el mismo diseño básico, en AEM esto puede verse como:

![Consola de AEM Sites](assets/ui-sites-console.png)

El diseño se adhiere a un estilo de diseño interactivo y se adapta al tamaño del dispositivo o ventana que esté utilizando.

Por ejemplo, cuando la resolución es inferior a 1024 píxeles (como en un dispositivo móvil), la pantalla se ajustará en consecuencia:

![Vista móvil de la consola Sitios](assets/ui-sites-mobile.png)

### Barra de encabezado {#header-bar}

![AEM barra de encabezado](assets/ui-header-bar.png)

La barra de encabezado muestra elementos globales como:

* el logotipo y el producto/solución específico que está utilizando actualmente; para AEM esto también forma un vínculo a Navegación global
* Búsqueda
* Icono para acceder a los recursos de ayuda
* Icono para acceder a otras soluciones
* Un indicador de (y acceso a) alertas o elementos de la bandeja de entrada que le estén esperando
* El icono de usuario, junto con un vínculo a la administración de perfiles

### Barra de herramientas {#toolbar}

La barra de herramientas es contextual para su ubicación y muestra las herramientas relevantes para controlar la vista o los recursos en la página siguiente. La barra de herramientas es específica del producto, pero los elementos son comunes.

En cualquier ubicación, la barra de herramientas muestra las acciones disponibles actualmente:

![Barra de herramientas de AEM Sites](assets/ui-sites-toolbar.png)

También depende de si un recurso está seleccionado actualmente:

![Barra de herramientas de AEM Sites seleccionada](assets/ui-sites-toolbar-selected.png)

### Carril izquierdo {#left-rail}

El carril izquierdo se puede abrir u ocultar según sea necesario para mostrar:

* **Solo contenido**
* **Árbol de contenido**
* **Escala de cronología**
* **Referencias**
* **Filtro**

El valor predeterminado es **Solo contenido** (carril oculto).

![Carril izquierdo](assets/ui-left-rail.png)

## Creación de páginas {#page-authoring}

Al crear páginas, las áreas estructurales son las siguientes:

### Marco de contenido {#content-frame}

El contenido de la página se representa en el marco de contenido. El marco de contenido es completamente independiente del editor para garantizar que no haya conflictos debido a CSS o javascript.

El marco de contenido se encuentra en la sección derecha de la ventana, debajo de la barra de herramientas.

![Marco de contenido](assets/ui-content-frame.png)

### Marco del editor {#editor-frame}

El marco del editor permite las funciones de edición.

El marco del editor es un contenedor (abstracto) para todos los elementos de creación de páginas. Se encuentra sobre el marco de contenido e incluye:

* La barra de herramientas superior
* El panel lateral
* Todas las superposiciones
* Cualquier otro elemento de creación de páginas; por ejemplo, la barra de herramientas de componentes

![Marco del editor](assets/ui-editor-frame.png)

### Panel lateral {#side-panel}

Contiene tres pestañas predeterminadas. La variable **Recursos** y **Componentes** las pestañas permiten seleccionar estos elementos, arrastrarlos desde el panel y colocarlos en la página. La variable **Árbol de contenido** permite inspeccionar la jerarquía de contenido de la página.

El panel lateral está oculto de forma predeterminada. Cuando se selecciona, se muestra en el lado izquierdo o se desliza para cubrir toda la ventana cuando el tamaño de la ventana es inferior a una anchura de 1024 píxeles; como, por ejemplo, en un dispositivo móvil.

![Panel lateral](assets/ui-side-panel.png)

### Panel lateral: recursos {#side-panel-assets}

En la pestaña Recursos , puede seleccionar entre el rango de recursos. También puede filtrar por un término específico o seleccionar un grupo.

![Ficha Recursos](assets/ui-side-panel-assets.png)

### Panel lateral: Grupos de recursos {#side-panel-asset-groups}

En la ficha Recursos hay una lista desplegable que puede utilizar para seleccionar los grupos de recursos específicos.

![Grupos de recursos](assets/ui-side-panel-asset-groups.png)

### Panel lateral: componentes {#side-panel-components}

En la pestaña Componentes , puede seleccionar entre el rango de componentes. También puede filtrar por un término específico o seleccionar un grupo.

![Ficha Componentes](assets/ui-side-panel-components.png)

### Panel lateral: árbol de contenido {#side-panel-content-tree}

En la pestaña Árbol de contenido puede ver la jerarquía de contenido en la página. Al hacer clic en una entrada de la ficha, se salta a y se selecciona el elemento de la página dentro del editor.

![Árbol de contenido](assets/ui-side-panel-content-tree.png)

### Superposiciones {#overlays}

Estas superposiciones superponen el marco de contenido y las usa el [capas](#layer) para realizar los mecanismos de interacción (completamente transparente) con los componentes y su contenido.

Las superposiciones se encuentran en el marco del editor (con todos los demás elementos de creación de páginas), aunque en realidad superponen los componentes adecuados en el marco de contenido.

![Superposiciones](assets/ui-overlays.png)

### Capa {#layer}

Una capa es un paquete de funcionalidad independiente que puede activarse para:

* Proporcionar una vista diferente de la página
* Permiten manipular una página o interactuar con ella

Las capas proporcionan una funcionalidad sofisticada para toda la página, a diferencia de acciones específicas en un componente individual.

AEM incluye varias capas ya implementadas para la creación de páginas; por ejemplo, editar, previsualizar y anotar capas.

>[!NOTE]
>
>Las capas son un concepto potente que afecta a la vista del usuario y a la interacción con el contenido de la página. Al desarrollar sus propias capas, debe asegurarse de que la capa se limpia cuando se sale.

### Conmutador de capas {#layer-switcher}

El selector de capas le permite elegir la capa que desea utilizar. Cuando está cerrada, indica la capa que se está utilizando.

El selector de capas está disponible como una lista desplegable de la barra de herramientas (en la parte superior de la ventana, dentro del marco del editor).

![Conmutador de capas](assets/ui-layer-switcher.png)

### Barra de herramientas del componente {#component-toolbar}

Cada instancia de un componente muestra su barra de herramientas cuando se hace clic (una vez o con un doble clic lento). La barra de herramientas contiene las acciones específicas (por ejemplo, copiar, pegar, abrir-editor) que están disponibles para la instancia de componente en la página.

Según el espacio disponible, las barras de herramientas de componentes se colocan en la esquina superior derecha o inferior del componente correspondiente.

![Barra de herramientas de componentes](assets/ui-component-toolbar.png)

## Información adicional {#further-information}

<!--For more details about the concepts around the touch-enabled UI, continue to the article [Concepts of the AEM Touch-Enabled UI](/help/sites-developing/touch-ui-concepts.md).-->

Para obtener más información técnica, consulte [Conjunto de documentación de JS](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/jsdoc/ui-touch/editor-core/index.html) para el editor de páginas.
