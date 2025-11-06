---
title: Personalización de la creación de páginas
description: Obtenga información sobre los mecanismos que proporciona AEM as a Cloud Service para personalizar la funcionalidad de creación de páginas.
exl-id: 98d3c7ab-46d2-4e8d-b0da-5c8a7b398135
feature: Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '936'
ht-degree: 4%

---

# Personalización de la creación de páginas {#customizing-page-authoring}

Adobe Experience Manager as a Cloud Service proporciona mecanismos que le permiten personalizar la funcionalidad de creación de páginas (y las [consolas](/help/implementing/developing/extending/consoles.md)) de su instancia de creación.

## Clientlibs {#clientlibs}

Clientlibs permite ampliar la implementación predeterminada para habilitar nuevas funciones, al tiempo que se reutilizan las funciones, los objetos y los métodos estándar.

Al personalizar, puede crear su propia clientlib en `/apps.`. La nueva clientlib debe:

* Depender de la clientlib `cq.authoring.editor.sites.page` de creación.
* Forme parte de la categoría `cq.authoring.editor.sites.page.hook` apropiada.

Ver [Uso de bibliotecas del lado del cliente en AEM as a Cloud Service](/help/implementing/developing/introduction/clientlibs.md).

## Superposiciones {#overlays}

Las superposiciones se basan en definiciones de nodo y le permiten superponer la funcionalidad estándar de `/libs` con su propia funcionalidad personalizada en `/apps`.

Al crear una superposición, no se requiere una copia 1:1 del original, ya que la [fusión de recursos de sling](/help/implementing/developing/introduction/sling-resource-merger.md) permite la herencia.

Para obtener más información, consulte [Conjunto de documentación de JS](https://developer.adobe.com/experience-manager/reference-materials/6-5/jsdoc/ui-touch/editor-core/index.html).

Para obtener más información sobre las superposiciones, consulte [Superposiciones para Adobe Experience Manager as a Cloud Service](/help/implementing/developing/introduction/overlays.md).

## Añadir nueva capa (modo) {#add-new-layer-mode}

Cuando está editando una página, hay varios [modos](/help/sites-cloud/authoring/page-editor/introduction.md#page-modes) disponibles. Estos modos se implementaron usando [layers](/help/implementing/developing/introduction/ui-structure.md#layer). Permiten acceder a diferentes tipos de funcionalidades para el mismo contenido de página. Los modos de AEM estándar incluyen Edición, Diseño, Desarrollador, Deformación de tiempo, Estado de Live Copy y Segmentación.

### Ejemplo de capa: estado de Live Copy {#layer-example-live-copy-status}

Una instancia estándar de AEM proporciona la capa MSM. Esto accede a los datos relacionados con la [administración de varios sitios](/help/sites-cloud/administering/msm/overview.md) y los resalta en la capa.

Para verlo en acción, puede editar cualquier copia de idioma en el [contenido de muestra WKND](/help/implementing/developing/introduction/develop-wknd-tutorial.md) y seleccionar el modo **Estado de Live Copy**.

Puede encontrar la definición de capa de MSM (para referencia) en:

`/libs/wcm/msm/content/touch-ui/authoring/editor/js/msm.Layer.js`

### Ejemplo de código {#code-sample}

Este es un paquete de ejemplo que muestra cómo crear una capa (modo) para la vista MSM.

Puedes encontrar el código de esta página en [GitHub](https://github.com/Adobe-Marketing-Cloud/aem-authoring-new-layer-mode).

## Añadir nueva categoría de selección al navegador de recursos {#add-new-selection-category-to-asset-browser}

El explorador de recursos muestra recursos de varios tipos o categorías (por ejemplo, imágenes y documentos). Los recursos también se pueden filtrar por estas categorías de recursos.

### Ejemplo de código {#code-sample-1}

`aem-authoring-extension-assetfinder-flickr` es un paquete de muestra que muestra cómo agregar un grupo al buscador de recursos. Este ejemplo se conecta al flujo público de [Flickr](https://www.flickr.com) y los muestra en el panel lateral.

Puedes encontrar el código de esta página en [GitHub](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-assetfinder-flickr).

## Filtrado de recursos {#filtering-resources}

Al crear páginas, el usuario debe seleccionar a menudo entre los recursos de una lista.

Para mantener la lista a un tamaño razonable y también relevante para el caso de uso, se puede implementar un filtro en forma de predicado personalizado. Por ejemplo, si el componente Granite `pathbrowser` se utiliza para permitir que el usuario seleccione la ruta a un recurso en particular, las rutas presentadas se pueden filtrar de la siguiente manera:

* Implemente el predicado personalizado implementando la interfaz [`com.day.cq.commons.predicate.AbstractNodePredicate`](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/commons/predicate/package-summary.html).
* Especifique un nombre para el predicado y haga referencia a ese nombre cuando use `pathbrowser`.

Para obtener más información sobre cómo crear un predicado personalizado, vea [este artículo](/help/implementing/developing/introduction/query-builder-custom-predicate.md).

## Agregar una nueva acción a una barra de herramientas de componentes {#add-new-action-to-a-component-toolbar}

Cada componente suele tener una barra de herramientas que proporciona acceso a una serie de acciones que se pueden realizar en ese componente.

### Ejemplo de código {#code-sample-2}

`aem-authoring-extension-toolbar-screenshot` es un paquete de ejemplo que muestra cómo crear una acción personalizada de la barra de herramientas para procesar componentes.

Puedes encontrar el código de esta página en [GitHub](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-toolbar-screenshot).

## Añadir nuevo editor en contexto {#add-new-in-place-editor}

### Editor in situ estándar {#standard-in-place-editor}

En una instalación estándar de AEM:

1. `/libs/cq/gui/components/authoring/editors/clientlibs/core/js/editors/editorExample.js` contiene definiciones de los distintos editores disponibles.

1. Existe una conexión entre el editor y cada tipo de recurso (como en el componente ) que puede utilizarlo:

   * `cq:inplaceEditing`

     por ejemplo:

      * `/libs/foundation/components/text/cq:editConfig`
      * `/libs/foundation/components/image/cq:editConfig`

         * propiedad: `editorType`

           Define el tipo de editor en línea que se utiliza cuando se activa la edición in situ para ese componente; por ejemplo, `text`, `textimage`, `image`, `title`.

1. Se pueden configurar detalles de configuración adicionales del editor mediante un nodo `config` que contenga configuraciones y un nodo `plugin` que contenga los detalles de configuración del complemento necesarios.


A continuación se muestra un ejemplo de definición de relaciones de aspecto para el complemento de recorte de imágenes del componente de imagen.

```xml
   <cq:inplaceEditing
           jcr:primaryType="cq:InplaceEditingConfig"
           active="{Boolean}true"
           editorType="image">
           <config jcr:primaryType="nt:unstructured">
               <plugins jcr:primaryType="nt:unstructured">
                   <crop jcr:primaryType="nt:unstructured">
                       <aspectRatios jcr:primaryType="nt:unstructured">
                           <_x0031_6-10
                               jcr:primaryType="nt:unstructured"
                               name="16 : 10"
                               ratio="0.625"/>
                       </aspectRatios>
                   </crop>
               </plugins>
           </config>
   </cq:inplaceEditing>
```

>[!NOTE]
>
>Las proporciones de recorte de AEM establecidas por la propiedad `ratio` se definen como **altura/anchura**. Esto es distinto de la definición convencional de anchura/altura y se realiza por motivos de compatibilidad con sistemas anteriores. Los usuarios autores no notarán ninguna diferencia siempre que defina claramente la propiedad `name`, ya que esto es lo que se muestra en la interfaz de usuario.

#### Creación de un nuevo editor in situ {#creating-a-new-in-place-editor}

Para implementar un nuevo editor in situ (dentro de la clientlib):

1. Implementar:

   * `setUp`
   * `tearDown`

1. Registre el editor (incluye el constructor):

   * `editor.register`

1. Proporcione la conexión entre el editor y cada tipo de recurso (como en el componente) que pueda utilizarlo.

#### Ejemplo de código para crear un nuevo editor en contexto {#code-sample-for-creating-a-new-in-place-editor}

`aem-authoring-extension-inplace-editor` es un paquete de muestra que muestra cómo crear un editor local en AEM.

Puedes encontrar el código de esta página en [GitHub](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-inplace-editor).

## Añadir una acción de nueva página {#add-a-new-page-action}

Para agregar una nueva acción de página a la barra de herramientas de la página, por ejemplo, una acción **Volver a sitios** (consola).

### Ejemplo de código {#code-sample-3}

`aem-authoring-extension-header-backtosites` es un paquete de ejemplo que muestra cómo crear una acción personalizada de la barra de encabezado para volver a la consola Sitios.

Puedes encontrar el código de esta página en [GitHub](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-header-backtosites).

## Personalizar el flujo de trabajo de solicitud de activación {#customizing-the-request-for-activation-workflow}

El flujo de trabajo predeterminado, **Solicitud de activación**:

* Aparecerá automáticamente en el menú apropiado cuando un autor de contenido **no tenga** los derechos de replicación adecuados, pero **sí tiene** miembros de Usuarios y autores DAM.

* De lo contrario, no se muestra nada, ya que se han eliminado los derechos de replicación.

Para tener un comportamiento personalizado en dicha activación, puede superponer el flujo de trabajo **Solicitud de activación**:

1. En `/apps` se superpone el asistente **Sitios** `/libs/wcm/core/content/common/managepublicationwizard`

   * Esto mismo reemplaza la instancia común de `/libs/cq/gui/content/common/managepublicationwizard`.

1. Actualice el modelo de flujo de trabajo y las configuraciones/scripts relacionados según sea necesario.
1. Elimine el derecho a la acción `replicate` de todos los usuarios adecuados para todas las páginas relevantes. Para que este flujo de trabajo se active como una acción predeterminada cuando cualquiera de los usuarios intente publicar (o replicar) una página.
