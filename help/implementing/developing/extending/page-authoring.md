---
title: Personalización de la creación de páginas
description: AEM Obtenga información sobre los mecanismos que proporciona el as a Cloud Service para personalizar la funcionalidad de creación de páginas.
exl-id: 98d3c7ab-46d2-4e8d-b0da-5c8a7b398135
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 646ca4f4a441bf1565558002dcd6f96d3e228563
workflow-type: tm+mt
source-wordcount: '937'
ht-degree: 3%

---

# Personalización de la creación de páginas {#customizing-page-authoring}

Adobe Experience Manager as a Cloud Service proporciona mecanismos para permitirle personalizar la funcionalidad de creación de páginas (y la [consolas](/help/implementing/developing/extending/consoles.md)) de la instancia de creación.

## Clientlibs {#clientlibs}

Clientlibs permite ampliar la implementación predeterminada para habilitar nuevas funciones, al tiempo que se reutilizan las funciones, los objetos y los métodos estándar.

Al personalizar, puede crear su propia clientlib en `/apps.` La nueva clientlib debe:

* Depender de la clientlib de creación `cq.authoring.editor.sites.page`.
* Forme parte de las `cq.authoring.editor.sites.page.hook` categoría.

Consulte [AEM as a Cloud Service Uso de bibliotecas del lado del cliente en el uso de](/help/implementing/developing/introduction/clientlibs.md).

## Superposiciones {#overlays}

Las superposiciones se basan en definiciones de nodos y permiten superponer la funcionalidad estándar en `/libs` con su propia funcionalidad personalizada en `/apps`.

Al crear una superposición, no es necesaria una copia 1:1 del original, ya que la función [fusión de recursos de sling](/help/implementing/developing/introduction/sling-resource-merger.md) permite la herencia.

Para obtener más información, consulte la [Conjunto de documentación JS](https://developer.adobe.com/experience-manager/reference-materials/6-5/jsdoc/ui-touch/editor-core/index.html).

Para obtener más información sobre las superposiciones, consulte [Superposiciones para Adobe Experience Manager as a Cloud Service](/help/implementing/developing/introduction/overlays.md).

## Añadir nueva capa (modo) {#add-new-layer-mode}

Al editar una página, hay varias opciones [modos](/help/sites-cloud/authoring/page-editor/introduction.md#page-modes) disponible. Estos modos se implementan mediante [capas](/help/implementing/developing/introduction/ui-structure.md#layer). Permiten acceder a diferentes tipos de funcionalidades para el mismo contenido de página. AEM Los modos estándar incluyen Edición, Diseño, Desarrollador, Deformación de tiempo, Estado de Live Copy y Segmentación.

### Ejemplo de capa: estado de Live Copy {#layer-example-live-copy-status}

AEM Una instancia de estándar proporciona la capa de MSM. Esto accede a los datos relacionados con [administración de varios sitios](/help/sites-cloud/administering/msm/overview.md) y lo resalta en la capa.

Para verlo en acción, puede editar cualquier copia de idioma en la [Contenido de muestra WKND](/help/implementing/developing/introduction/develop-wknd-tutorial.md) y seleccione la **Estado de Live Copy** modo.

Puede encontrar la definición de capa de MSM (para referencia) en:

`/libs/wcm/msm/content/touch-ui/authoring/editor/js/msm.Layer.js`

### Ejemplo de código {#code-sample}

Este es un paquete de ejemplo que muestra cómo crear una capa (modo) para la vista MSM.

Puede encontrar el código de esta página en [GitHub.](https://github.com/Adobe-Marketing-Cloud/aem-authoring-new-layer-mode)

## Añadir nueva categoría de selección al navegador de recursos {#add-new-selection-category-to-asset-browser}

El explorador de recursos muestra recursos de varios tipos o categorías (por ejemplo, imágenes y documentos). Los recursos también se pueden filtrar por estas categorías de recursos.

### Ejemplo de código {#code-sample-1}

`aem-authoring-extension-assetfinder-flickr` es un paquete de muestra que muestra cómo agregar un grupo al buscador de recursos. Este ejemplo conecta con [Flickr](https://www.flickr.com)La emisión pública de y las muestra en el panel lateral.

Puede encontrar el código de esta página en [GitHub.](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-assetfinder-flickr)

## Filtrado de recursos {#filtering-resources}

Al crear páginas, el usuario debe seleccionar a menudo entre los recursos de una lista.

Para mantener la lista a un tamaño razonable y también relevante para el caso de uso, se puede implementar un filtro en forma de predicado personalizado. Por ejemplo, si la variable `pathbrowser` El componente Granite se utiliza para permitir al usuario seleccionar la ruta a un recurso concreto, las rutas presentadas se pueden filtrar de la siguiente manera:

* Implementar el predicado personalizado implementando [`com.day.cq.commons.predicate.AbstractNodePredicate`](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/commons/predicate/package-summary.html) interfaz.
* Especifique un nombre para el predicado y haga referencia a ese nombre cuando utilice la variable `pathbrowser`.

Para obtener más información sobre la creación de un predicado personalizado, consulte [este artículo.](/help/implementing/developing/introduction/query-builder-custom-predicate.md)

## Agregar una nueva acción a una barra de herramientas de componentes {#add-new-action-to-a-component-toolbar}

Cada componente suele tener una barra de herramientas que proporciona acceso a una serie de acciones que se pueden realizar en ese componente.

### Ejemplo de código {#code-sample-2}

`aem-authoring-extension-toolbar-screenshot` es un paquete de ejemplo que muestra cómo crear una acción personalizada de la barra de herramientas para procesar componentes.

Puede encontrar el código de esta página en [GitHub.](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-toolbar-screenshot)

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

1. Se pueden configurar detalles de configuración adicionales del editor mediante una `config` nodo que contiene configuraciones y un `plugin` para contener los detalles de configuración del complemento necesarios.


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
>AEM proporciones de recorte, según lo establecido por el `ratio` , se definen como **alto/ancho**. Esto es distinto de la definición convencional de anchura/altura y se realiza por motivos de compatibilidad con sistemas anteriores. Los usuarios autores no notarán ninguna diferencia siempre que defina la variable `name` claramente, ya que esto es lo que se muestra en la interfaz de usuario.

#### Creación de un nuevo editor in situ {#creating-a-new-in-place-editor}

Para implementar un nuevo editor in situ (dentro de la clientlib):

1. Implementar:

   * `setUp`
   * `tearDown`

1. Registre el editor (incluye el constructor):

   * `editor.register`

1. Proporcione la conexión entre el editor y cada tipo de recurso (como en el componente) que pueda utilizarlo.

#### Ejemplo de código para crear un nuevo editor en contexto {#code-sample-for-creating-a-new-in-place-editor}

`aem-authoring-extension-inplace-editor` AEM es un paquete de muestra que muestra cómo crear un editor in situ en el entorno de trabajo de la.

Puede encontrar el código de esta página en [GitHub.](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-inplace-editor)

## Añadir una acción de nueva página {#add-a-new-page-action}

Para agregar una acción de nueva página a la barra de herramientas de la página, por ejemplo, una **Volver a Sitios** Acción (consola).

### Ejemplo de código {#code-sample-3}

`aem-authoring-extension-header-backtosites` es un paquete de ejemplo que muestra cómo crear una acción personalizada de la barra de encabezado para volver a la consola Sitios.

Puede encontrar el código de esta página en [GitHub.](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-header-backtosites)

## Personalizar el flujo de trabajo de solicitud de activación {#customizing-the-request-for-activation-workflow}

El flujo de trabajo listo para usar, **Solicitud de activación**:

* Aparecerá automáticamente en el menú apropiado cuando un autor de contenido **no tiene** los derechos de replicación adecuados, pero **tiene** Pertenencia a DAM-Users y Authors.

* De lo contrario, no se muestra nada, ya que se han eliminado los derechos de replicación.

Para tener un comportamiento personalizado en dicha activación, puede superponer la variable **Solicitud de activación** flujo de trabajo:

1. Entrada `/apps` superponga el **Sites** asistente `/libs/wcm/core/content/common/managepublicationwizard`

   * Esto en sí, anula la instancia común de `/libs/cq/gui/content/common/managepublicationwizard`.

1. Actualice el modelo de flujo de trabajo y las configuraciones/scripts relacionados según sea necesario.
1. Retire el derecho a la `replicate` acción de todos los usuarios adecuados para todas las páginas relevantes. Para que este flujo de trabajo se active como una acción predeterminada cuando cualquiera de los usuarios intente publicar (o replicar) una página.
