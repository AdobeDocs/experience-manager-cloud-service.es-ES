---
title: Configure RTE para crear páginas web y sitios accesibles.
description: Aprenda a configurar el Editor de texto enriquecido para crear sitios accesibles en  [!DNL Adobe Experience Manager].
contentOwner: AG
exl-id: 54050fc9-0348-4033-8e2b-b3897588cb62
feature: Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '509'
ht-degree: 1%

---

# Configuración de RTE para crear sitios accesibles {#configure-rte-accessible-sites}

[!DNL Adobe Experience Manager] admite características de accesibilidad estándar, como texto alternativo para imágenes y características adicionales a las que se puede tener acceso al crear contenido. Los autores de contenido utilizan estas funciones con componentes que utilizan el editor de texto enriquecido (RTE). Las funciones incluyen agregar texto alternativo, información estructural a través de encabezados y elementos de párrafo, etc.

Para obtener información sobre las configuraciones típicas de RTE, consulte [configurar RTE](rich-text-editor.md) y [configurar complementos RTE para obtener funcionalidad específica](configure-rich-text-editor-plug-ins.md).

Utilice la configuración de complementos RTE para configurar y personalizar las funciones relacionadas con la accesibilidad. Por ejemplo, use `paraformat` para agregar elementos semánticos de nivel de bloque adicionales, incluyendo la ampliación del número de niveles de encabezado admitidos más allá de los niveles básicos `H1`, `H2` y `H3` proporcionados de forma predeterminada. La edición de texto enriquecido es posible mediante muchos componentes de la interfaz de usuario de creación. Los componentes que se utilizan con más frecuencia son texto, imagen, descarga, etc.

La funcionalidad RTE puede estar disponible en muchos componentes. El componente principal es `Text`.

Para el componente `Text` en [!DNL Experience Manager], la siguiente captura de pantalla muestra el editor de texto enriquecido con un rango de complementos habilitados, incluido `paraformat`:

![Componente de texto RTE en modo de pantalla completa](assets/rte-toolbar-full-screen-mode.png)

## Configuración de las funciones del complemento {#configuring-the-plugin-features}

Para obtener instrucciones para configurar RTE, consulte [configurar la página Editor de texto enriquecido](rich-text-editor.md). El artículo cubre:

* [Complementos y sus funciones](rich-text-editor.md#aboutplugins)
* [Ubicaciones de configuración](rich-text-editor.md#understand-the-configuration-paths-and-locations)
* [Activar un complemento y configurar la propiedad features](rich-text-editor.md#enable-rte-functionalities-by-activating-plug-ins)
* [Configuración de otras funcionalidades de RTE](rich-text-editor.md#enable-rte-functionalities-by-activating-plug-ins)

Para activar algunas o todas las funciones de un complemento, configúrelo en la rama secundaria `rtePlugins` correspondiente de CRXDE Lite.

![CRXDE Lite con rtePlugin de ejemplo](assets/example-rteplugin-crxde-lite.png)

### Ejemplo para especificar formatos de párrafo disponibles en el campo de selección RTE {#example-specifying-paragraph-formats-available-in-rte-selection-field}

Hay nuevos formatos de bloque semántico disponibles para la selección.

1. Según el RTE, determine y vaya a la [ubicación de configuración](rich-text-editor.md#understand-the-configuration-paths-and-locations).
1. [Habilite el campo de selección de párrafos](rich-text-editor.md) al [activar el complemento](rich-text-editor.md#enable-rte-functionalities-by-activating-plug-ins).
1. [Especifique los formatos que desea tener disponibles en el campo de selección de párrafos](rich-text-editor.md).
1. Los formatos de párrafo están disponibles para el autor de contenido desde los campos de selección en RTE.

Con los elementos estructurales disponibles en RTE a través de las opciones de formato de párrafo, [!DNL Experience Manager] proporciona una buena base para el desarrollo de contenido accesible. Los autores de contenido no pueden utilizar RTE para dar formato al tamaño de fuente, los colores u otros atributos relacionados, lo que impide la creación de formato en línea. En su lugar, los autores pueden seleccionar los elementos estructurales adecuados, como encabezados y utilizar estilos globales elegidos desde la opción Estilos para garantizar un marcado limpio y mejores opciones para los usuarios que exploran con sus propias hojas de estilos y contenido estructurado correctamente.

## Uso de la función Source Edit {#use-of-the-source-edit-feature}

En algunos casos, los autores de contenido deberán examinar y ajustar el código fuente de HTML creado con RTE. Por ejemplo, un fragmento de contenido creado dentro de RTE puede requerir más marcado para garantizar el cumplimiento de WCAG 2.0. Esto se puede hacer con la opción [source edit](rich-text-editor.md#aboutplugins) de RTE. Puede especificar la característica [`sourceedit` en el complemento `misctools` &#x200B;](rich-text-editor.md#aboutplugins).

>[!CAUTION]
>
>Utilice la característica `sourceedit` con cuidado. Cualquier error de escritura y las funciones no admitidas pueden introducir problemas.

<!--
TBD ENGREVIEW: Is this only applicable to Classic UI? 

## Adding Support for further HTML Elements and Attributes {#adding-support-for-additional-html-elements-and-attributes}

To further extend the accessibility features of [!DNL Experience Manager], it is possible to extend the existing components based on the RTE (such as the `Text` and `Table` components) with extra elements and attributes.

The following procedure illustrates how to extend the `Table` component with a `Caption` element that provides information about a data table to assistive technology users:

### Example: Add a caption to a table properties dialog {#example-adding-the-caption-to-the-table-properties-dialog}

In the constructor of the `TablePropertiesDialog`, add an extra text input field that is used for editing the caption. Set the `itemId` to `caption` (the DOM attribute’s name) to automatically handle its content.

In a `Table`, set the attribute to the DOM element or or remove it from the DOM element. The dialog in the `config` object passed the value. Set or remove the DOM attributes using the corresponding `CQ.form.rte.Common` methods (`com` is a shortcut for `CQ.form.rte.Common`). Using `CQ.form.rte.Common` methods avoids common pitfalls with browser implementations.

>[!NOTE]
>
>This procedure is only suitable for the classic UI.

### Step-by-step instructions {#step-by-step-instructions}

1. Start CRXDE Lite. For example: [http://localhost:4502/crx/de/](http://localhost:4502/crx/de/)

1. Copy `/libs/cq/ui/widgets/source/widgets/form/rte/commands/Table.js` to `/apps/cq/ui/widgets/source/widgets/form/rte/commands/Table.js`. Create intermediate folders if those do not exist.

1. Copy `/libs/cq/ui/widgets/source/widgets/form/rte/plugins/TablePropertiesDialog.js` to `/apps/cq/ui/widgets/source/widgets/form/rte/plugins/TablePropertiesDialog.js`.

1. Open `/apps/cq/ui/widgets/source/widgets/form/rte/plugins/TablePropertiesDialog.js` file to edit.

1. In the `constructor` method, before the mention of `var dialogRef = this;`, add the following code:

   ```javascript
   editItems.push({
       "itemId": "caption",
       "name": "caption",
       "xtype": "textfield",
       "fieldLabel": CQ.I18n.getMessage("Caption"),
       "value": (this.table && this.table.caption ? this.table.caption.textContent : "")
   });
   ```

1. Open `/apps/cq/ui/widgets/source/widgets/form/rte/commands/Table.js` file.

1. Add the following code at the end of the `transferConfigToTable` method:

   ```javascript
   /**
    * Adds Caption Element
   */
   var captionElement;
   if (dom.firstChild && dom.firstChild.tagName.toLowerCase() == "caption")
   {
      captionElement = dom.firstChild;
   }
   if (config.caption)
   {
       var captionTextNode = document.createTextNode(config.caption)
       if (captionElement)
       {
          dom.replaceNode(captionElement.firstChild,captionTextNode);
       } else
       {
           captionElement = document.createElement("caption");
           captionElement.appendChild(captionTextNode);
           if (dom.childNodes.length>0)
           {
              dom.insertBefore(captionElement, dom.firstChild);
           } else
           {
              dom.appendChild(captionElement);
           }
       }
   } else if (captionElement)
   {
     dom.removeChild(captionElement);
   }
   ```

1. To save your changes, click **[!UICONTROL Save All]**.

## Best practices and limitations {#best-practices-limitations-tips}

* A plain text field is not the only type of input allowed for the value of the caption element. You can use any ExtJS widget, that provides the caption’s value through its `getValue()` method.
* To add editing capabilities for more elements and attributes, ensure that:

  * The `itemId` property for each corresponding field is set to the name of the appropriate DOM attribute (`TablePropertiesDialog`).
  * The attribute is set and/or removed on the DOM element explicitly (`Table`).
-->

>[!MORELIKETHIS]
>
>* [Guía rápida de los estándares WCAG](/help/compliance/accessibility/quick-guide-wcag.md)
>* [Cómo crear contenido accesible en Experience Manager](/help/sites-cloud/authoring/page-editor/accessible-content.md)
