---
title: Configuración del contenedor y el modo de diseño
description: Aprenda a configurar el contenedor y el modo de diseño para habilitar los diseños adaptables para los autores de contenido.
exl-id: 469e8151-8231-4ccc-b7f6-855545f87440
solution: Experience Manager Sites
feature: Administering
role: Admin
source-git-commit: 7adfe0ca7fbab1f8a5bd488e524a48be62584966
workflow-type: tm+mt
source-wordcount: '1250'
ht-degree: 3%

---

# Configuración del contenedor y el modo de diseño {#configuring-layout-container-and-layout-mode}

[Diseño adaptable](/help/sites-cloud/authoring/page-editor/responsive-layout.md) es un mecanismo para realizar [diseño web adaptable.](https://en.wikipedia.org/wiki/Responsive_web_design): esto permite al autor del contenido crear páginas web con un diseño y dimensiones dependientes de los dispositivos que utilizan sus usuarios.

AEM realiza un diseño interactivo para sus páginas mediante una combinación de diferentes mecanismos:

* **[Contenedor de diseño](/help/sites-cloud/authoring/page-editor/responsive-layout.md#adding-a-layout-container-and-its-content-edit-mode)**: este componente proporciona un sistema de párrafos de cuadrícula que le permite agregar y colocar componentes en una cuadrícula adaptable.
   * Se puede utilizar como parsys predeterminado para la página o estar disponible para los autores en el explorador de componentes.
   * El componente **Contenedor de diseño** predeterminado se define en `/libs/wcm/foundation/components/responsivegrid`.
   * Puede definir contenedores de diseño:
      * Como un componente que el usuario puede agregar a una página.
      * Como parsys predeterminado para la página.
      * Como componente y como parsys predeterminado.
         * Puede tener el contenedor de diseño como estándar para la página, a la vez que permite al usuario agregar más contenedores de diseño dentro de esta página; por ejemplo, para lograr el control de columna.
* **[Modo de diseño](/help/sites-cloud/authoring/page-editor/introduction.md#mode-selector)**: una vez que el contenedor de diseño esté colocado en la página, puede usar el modo **Diseño** para colocar el contenido en la cuadrícula adaptable.
* **[Emulador](/help/sites-cloud/authoring/page-editor/responsive-layout.md#selecting-a-device-to-emulate)**: esto le permite crear y editar sitios web interactivos que reorganizan el diseño según el tamaño del dispositivo o la ventana, mediante el redimensionado activo de los componentes. A continuación, el usuario puede ver cómo se representa el contenido mediante el emulador.

Con estos mecanismos de cuadrícula adaptable puede hacer lo siguiente:

* Utilice puntos de interrupción (que indican la agrupación del dispositivo) para definir un comportamiento de contenido diferente en función del diseño del dispositivo.
* Ocultar componentes basados en grupos de dispositivos (defina en qué punto de interrupción se ocultará un componente).
* Utilice el ajuste horizontal a la cuadrícula (coloque los componentes en la cuadrícula, cambie su tamaño según sea necesario, defina cuándo deben contraerse o redistribuirse lateralmente o arriba/abajo).
* Realizar el control de columnas.

>[!NOTE]
>
>Al crear un sitio a partir del [Tipo de archivo del proyecto](#addlink) o de la [Plantilla de sitio estándar](#addlink), el diseño interactivo suele estar configurado. De lo contrario, debe [activar el componente Contenedor de diseño](#enable-the-layout-container-component-for-page) para sus páginas.

## Activación del emulador {#enabling-emulator}

El [tipo de archivo del proyecto](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=es) y la [plantilla de sitio estándar](/help/sites-cloud/administering/site-creation/site-templates.md#standard-site-template) ya están habilitados para usar el emulador. Si ha desarrollado su propio contenido no basado en los componentes principales o el tipo de archivo, consulte el documento [Diseño interactivo](/help/implementing/developing/introduction/responsive-design.md) para obtener detalles sobre cómo desarrollar los componentes mientras aprovecha estas funciones.

## Activar el modo Diseño para su sitio {#activate-layout-mode-for-your-site}

El modo **Diseño** le permite usar el emulador para ajustar el diseño del contenido para diferentes dispositivos. El sitio de muestra WKND ya está habilitado para el modo **Diseño**. Siga estos pasos para habilitar su propio sitio.

### Configurar puntos de interrupción {#configure-breakpoints}

Los puntos de interrupción son vitales para un diseño interactivo y definen cómo y cuándo se ajusta el contenido al dispositivo de destino. Sin embargo, tenga cuidado, ya que cada punto de interrupción que introduzca generará trabajo adicional para que los autores se adapten al contenido. Muchas veces, dos puntos de interrupción pueden ser suficientes, incluido el punto de interrupción predeterminado, que siempre está ahí. El Adobe recomienda no crear más de tres puntos de interrupción, incluido el predeterminado, es decir, no más de dos nodos por debajo de `cq:responsive/breakpoint`.

* Los puntos de interrupción tienen un título y un ancho:
   * El título describe la agrupación de dispositivos genéricos, con orientación si es necesario.
      * Por ejemplo, `phone`, `tablet`
   * La anchura define la anchura máxima en píxeles para esa agrupación de dispositivos genéricos.
      * Por ejemplo, si el punto de interrupción del teléfono tiene una anchura de 768, indique la anchura máxima del diseño utilizado para un dispositivo móvil.
* Se pueden definir puntos de interrupción:
   * En la plantilla de página, desde donde se copia la configuración a cualquier página creada con esa plantilla.
   * En el nodo de la página, desde donde cualquier página secundaria hereda la configuración.
* Los puntos de interrupción se pueden ver como marcadores en la parte superior del editor de páginas cuando se utiliza el emulador.
* Los puntos de interrupción se heredan de la jerarquía del nodo principal y se pueden anular a voluntad.
* Hay un punto de interrupción predeterminado (predeterminado) que cubre todo lo que está por encima del último punto de interrupción configurado.
* Los puntos de interrupción se pueden definir mediante CRXDE Lite o XML.

Los puntos de interrupción deben tenerse en cuenta tanto para los proyectos nuevos como para los existentes.

* Si está configurando un nuevo proyecto, debe agregar puntos de interrupción a las plantillas.
* Si está migrando un proyecto existente (con contenido existente), debe:
   * Agregue puntos de interrupción a las plantillas.
   * Agregue los mismos puntos de interrupción a las páginas existentes.

Debido a la herencia, solo debe hacerlo para la página raíz del contenido.

#### Configuración de puntos de interrupción mediante CRXDE Lite {#configuring-breakpoints-using-crxde-lite}

1. Con el CRXDE Lite, vaya a:

   * Definición de la plantilla.
   * El nodo `jcr:content` de su página.

1. En `jcr:content`, cree el nodo:

   * Nombre: `cq:responsive`
   * Tipo: `nt:unstructured`

1. En esta sección, cree el nodo:

   * Nombre: `breakpoints`
   * Tipo: `nt:unstructured`

1. Bajo el nodo de puntos de interrupción puede crear cualquier número de puntos de interrupción. Cada definición es un nodo único con las siguientes propiedades:

   * Nombre: `<descriptive name>`
   * Tipo: `nt:unstructured`
   * Título: `String <descriptive title seen in Emulator>`
   * Anchura: `Decimal <value of breakpoint>`

#### Configurar puntos de interrupción mediante XML {#configuring-breakpoints-using-xml}

Los puntos de interrupción se encuentran dentro de la sección `<jcr:content>` de `.context.html` en la carpeta de plantilla (o contenido) adecuada.

Una definición de ejemplo:

```xml
<cq:responsive jcr:primaryType="nt:unstructured">
  <breakpoints jcr:primaryType="nt:unstructured">
    <phone jcr:primaryType="nt:unstructured" title="{String}Phone" width="{Decimal}768"/>
    <tablet jcr:primaryType="nt:unstructured" title="{String}Tablet" width="{Decimal}1200"/>
  </breakpoints>
</cq:responsive>
```

## Habilitar el cambio de tamaño del componente para la página {#enable-component-resizing-for-the-page}

Cambiar el tamaño de los componentes en el modo **Layout** es una parte importante del diseño interactivo que se puede utilizar en el sitio de muestra WKND. Siga estos pasos para habilitar su propio sitio.

### Definir contenedor de diseño como parsys principal {#set-layout-container-as-main-parsys}

Para establecer que el parsys principal de la página sea un contenedor de diseño, defina el parsys como:

`wcm/foundation/components/responsivegrid`

En:

* Componente Página
* Plantilla de página (para uso futuro)

Los dos ejemplos siguientes ilustran la definición:

* **HTL:**

  ```xml
  <sly data-sly-resource="${'par' @ resourceType='wcm/foundation/components/responsivegrid'}/>
  ```

* **JSP:**

  ```xml
  <cq:include path="par" resourceType="wcm/foundation/components/responsivegrid" />
  ```

### Incluir CSS interactivo {#include-the-responsive-css}

#### CSS para puntos de interrupción con LESS {#css-for-breakpoints-using-less}

AEM Utiliza LESS para generar partes del CSS necesario, que deben incluirse para los proyectos.

Debe crear una [biblioteca de cliente](/help/implementing/developing/introduction/clientlibs.md) para proporcionar configuraciones y llamadas a funciones adicionales. El siguiente extracto LESS es un ejemplo del mínimo que debe agregar al proyecto:

```java
@import (once) "/libs/wcm/foundation/clientlibs/grid/grid_base.less";

/* maximum amount of grid cells to be provided */
@max_col: 12;

/* default breakpoint */
.aem-Grid {
  .generate-grid(default, @max_col);
}

/* phone breakpoint */
@media (max-width: 768px) {
  .aem-Grid {
    .generate-grid(phone, @max_col);
  }
}

/* tablet breakpoint */
@media (min-width: 769px) and (max-width: 1200px) {
  .aem-Grid {
    .generate-grid(tablet, @max_col);
  }
}
```

La definición de la cuadrícula base se encuentra en:

`/libs/wcm/foundation/clientlibs/grid/grid_base.less`

#### Consideraciones de estilo {#styling-considerations}

Los componentes contenidos en un contenedor interactivo cambian de tamaño (junto con sus respectivos elementos DOM HTML) según el tamaño de la cuadrícula interactiva. Por lo tanto, en estas circunstancias, se recomienda evitar (o actualizar) las definiciones de elementos DOM de ancho fijo (contenidos).

Por ejemplo:

* Antes:

   * `width=100px`

* Después:

   * `max-width=100px`

#### Cambio de tamaño y compatibilidad con imágenes adaptables {#resizing-and-adaptive-image-compliance}

Cualquier cambio de tamaño de un componente dentro de la cuadrícula almacenará en déclencheur los siguientes oyentes según corresponda:

* `beforeedit`
* `beforechildedit`
* `afteredit`
* `afterchildedit`

Para cambiar el tamaño y actualizar correctamente el contenido de una imagen adaptable incluida en una cuadrícula adaptable, debe agregar un objeto de escucha `afterEdit` establecido en `REFRESH_PAGE` al archivo `EditConfig` de cada componente contenido.

Por ejemplo:

`<cq:listeners jcr:primaryType="cq:EditListenersConfig" afteredit="REFRESH_PAGE" />`

El mecanismo de imagen adaptable está disponible a través de una secuencia de comandos que controla la selección de la imagen correcta para el tamaño actual de la ventana. Se activa después de que el DOM esté listo o cuando se recibe un evento dedicado. Actualmente, la página debe actualizarse para reflejar correctamente el resultado de la acción del usuario.

>[!CAUTION]
>
>Los clientlibs de hojas de estilo personalizadas deben cargarse como parte del encabezado para que funcionen correctamente en la creación y en la publicación.

## Habilitar el componente Contenedor de diseño para la página {#enable-the-layout-container-component-for-page}

Para que el diseño sea eficaz, el autor del contenido debe poder arrastrar instancias del componente Contenedor de diseño a la página. Ya está habilitado para el sitio de muestra WKND. Siga estos pasos para habilitar su propio sitio.

### Habilitar el componente Contenedor de diseño para la edición de páginas {#enable-the-layout-container-component-for-page-editing}

Para permitir que los autores agreguen más cuadrículas adaptables a las páginas de contenido, debe habilitar el componente Contenedor de diseño para su página. Para ello, utilice uno de los métodos siguientes:

* **A través del entorno de creación** - [Edite las plantillas de página](/help/sites-cloud/authoring/page-editor/templates.md) para habilitar el contenedor de diseño para una página.
* **Definición del componente** - Use `allowedComponent` o una inclusión estática al definir el componente.

### Configuración de la cuadrícula del contenedor de diseño {#configure-the-grid-of-the-layout-container}

Puede configurar el número de columnas disponibles para cada instancia específica del contenedor de diseño [editando las plantillas de página.](/help/sites-cloud/authoring/page-editor/templates.md)
