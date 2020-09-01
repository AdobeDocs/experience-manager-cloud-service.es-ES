---
title: Estructura de la IU AEM
description: La IU AEM tiene varios principios subyacentes y está formada por varios elementos clave
translation-type: tm+mt
source-git-commit: 0799a817095558edd49b53ddc915c9474181fef7
workflow-type: tm+mt
source-wordcount: '915'
ht-degree: 2%

---


# Estructura de la IU AEM {#structure-of-the-aem-ui}

La IU AEM tiene varios principios subyacentes y está formada por varios elementos clave:

## Consolas {#consoles}

### Diseño básico y cambio de tamaño {#basic-layout-and-resizing}

La interfaz de usuario se ocupa de los dispositivos móviles y de escritorio, aunque en lugar de crear dos estilos, AEM utiliza un estilo que funciona para todas las pantallas y dispositivos.

Todos los módulos utilizan el mismo diseño básico, en AEM esto puede verse como:

![AEM Sites console](assets/ui-sites-console.png)

El diseño se ajusta a un estilo de diseño interactivo y se adapta al tamaño del dispositivo o ventana que se esté utilizando.

Por ejemplo, cuando la resolución es inferior a 1024 px (como en un dispositivo móvil), la pantalla se ajustará en consecuencia:

![Vista móvil de la consola Sitios](assets/ui-sites-mobile.png)

### Barra de encabezado {#header-bar}

![Barra de encabezado AEM](assets/ui-header-bar.png)

La barra de encabezado muestra elementos globales que incluyen:

* El logotipo y el producto o solución específicos que está utilizando actualmente; para AEM esto también forma un vínculo a la navegación global
* Búsqueda  
* Icono para acceder a los recursos de ayuda
* Icono para acceder a otras soluciones
* Un indicador (y acceso a) cualquier alerta o elemento de la Bandeja de entrada que le esté esperando
* El icono de usuario, junto con un vínculo a la administración de perfiles

### Barra de herramientas {#toolbar}

La barra de herramientas es contextual para su ubicación y superpone las herramientas relevantes para controlar la vista o los recursos en la página siguiente. La barra de herramientas es específica del producto, pero los elementos tienen algunas características comunes.

En cualquier ubicación, la barra de herramientas muestra las acciones disponibles actualmente:

![Barra de herramientas de AEM Sites](assets/ui-sites-toolbar.png)

También depende de si un recurso está seleccionado actualmente:

![Barra de herramientas de AEM Sites seleccionada](assets/ui-sites-toolbar-selected.png)

### Carril izquierdo {#left-rail}

El carril izquierdo se puede abrir u ocultar según sea necesario para mostrar:

* **Solo contenido**
* **Árbol de contenido**
* **Escala de tiempo**
* **Referencias**
* **Filtro**

El valor predeterminado es Solo **** contenido (carril oculto).

![Carril izquierdo](assets/ui-left-rail.png)

## Creación de páginas {#page-authoring}

Al crear páginas, las áreas estructurales son las siguientes.

### Marco de contenido {#content-frame}

El contenido de la página se representa en el marco de contenido. El marco de contenido es completamente independiente del editor para garantizar que no haya conflictos debido a CSS o javascript.

El marco de contenido se encuentra en la sección derecha de la ventana, debajo de la barra de herramientas.

![Marco de contenido](assets/ui-content-frame.png)

### Marco del editor {#editor-frame}

El marco del editor activa las funciones de edición.

El marco del editor es un contenedor (abstracto) para todos los elementos de creación de páginas. Vive sobre el marco de contenido e incluye:

* Barra de herramientas superior
* Panel lateral
* Todas las superposiciones
* Cualquier otro elemento de creación de páginas; por ejemplo, la barra de herramientas de componentes

![Marco del editor](assets/ui-editor-frame.png)

### Panel lateral {#side-panel}

Contiene tres fichas predeterminadas. Las fichas **Recursos** y **Componentes** permiten seleccionar dichos elementos y arrastrarlos desde el panel y colocarlos en la página. La ficha **Árbol** de contenido permite inspeccionar la jerarquía de contenido de la página.

El panel lateral está oculto de forma predeterminada. Cuando se selecciona, se muestra en el lado izquierdo o se desliza para cubrir toda la ventana cuando el tamaño de la ventana es inferior a una anchura de 1024 píxeles; como, por ejemplo, en un dispositivo móvil.

![Panel lateral](assets/ui-side-panel.png)

### Panel lateral - Recursos {#side-panel-assets}

En la ficha Recursos, puede seleccionar entre el rango de recursos. También puede filtrar por un término específico o seleccionar un grupo.

![Ficha Recursos](assets/ui-side-panel-assets.png)

### Panel lateral - Grupos de recursos {#side-panel-asset-groups}

En la ficha Recursos hay una lista desplegable que puede utilizar para seleccionar los grupos de recursos específicos.

![Grupos de recursos](assets/ui-side-panel-asset-groups.png)

### Panel lateral - Componentes {#side-panel-components}

En la ficha Componentes puede seleccionar entre el rango de componentes. También puede filtrar por un término específico o seleccionar un grupo.

![Ficha Componentes](assets/ui-side-panel-components.png)

### Panel lateral: árbol de contenido {#side-panel-content-tree}

En la ficha Árbol de contenido puede vista la jerarquía de contenido de la página. Al hacer clic en una entrada de la ficha, se le salta y se selecciona el elemento de la página dentro del editor.

![Árbol de contenido](assets/ui-side-panel-content-tree.png)

### Superposiciones {#overlays}

Estas superposiciones superponen el marco de contenido y las [capas](#layer) las utilizan para realizar la mecánica de cómo interactuar (de forma completamente transparente) con los componentes y su contenido.

Las superposiciones se encuentran en el marco del editor (con todos los demás elementos de creación de páginas), aunque en realidad superponen los componentes adecuados en el marco de contenido.

![Superposiciones](assets/ui-overlays.png)

### Capa {#layer}

Una capa es un paquete de funcionalidad independiente que se puede activar para:

* Proporcionar una vista diferente de la página
* Permite manipular una página o interactuar con ella

Las capas proporcionan una funcionalidad sofisticada para toda la página, en lugar de acciones específicas para un componente individual.

AEM viene con varias capas ya implementadas para la creación de páginas; por ejemplo, editar, previsualización y anotar capas.

>[!NOTE]
>
>Las capas son un concepto potente que afecta a la vista del usuario y a la interacción con el contenido de la página. Al desarrollar sus propias capas, debe asegurarse de que la capa se limpia al salir.

### Conmutador de capas {#layer-switcher}

El mezclador de capas le permite elegir la capa que desea utilizar. Cuando se cierra, indica la capa que se está utilizando.

El mezclador de capas está disponible como una lista desplegable desde la barra de herramientas (en la parte superior de la ventana, dentro del marco del editor).

![Conmutador de capas](assets/ui-layer-switcher.png)

### Barra de herramientas del componente {#component-toolbar}

Cada instancia de un componente mostrará su barra de herramientas cuando se haga clic en él (una vez o con un doble lento al hacer clic). La barra de herramientas contiene las acciones específicas (por ejemplo, copiar, pegar, editor abierto) disponibles para la instancia de componente en la página.

Según el espacio disponible, las barras de herramientas del componente se colocan en la esquina superior o inferior derecha del componente correspondiente.

![Barra de herramientas Componente](assets/ui-component-toolbar.png)

## Información adicional {#further-information}

<!--For more details about the concepts around the touch-enabled UI, continue to the article [Concepts of the AEM Touch-Enabled UI](/help/sites-developing/touch-ui-concepts.md).-->

Para obtener más información técnica, consulte el conjunto [de documentación de](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/jsdoc/ui-touch/editor-core/index.html) JS para el editor de páginas.
