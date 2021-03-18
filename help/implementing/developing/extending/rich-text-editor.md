---
title: Configure el Editor de texto enriquecido para que cree contenido en [!DNL Adobe Experience Manager] como Cloud Service.
description: Configure el Editor de texto enriquecido para que cree contenido en [!DNL Adobe Experience Manager] como Cloud Service.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 96aa0ef43613e6ae72bf4c454be46329abb19a0c
workflow-type: tm+mt
source-wordcount: '1969'
ht-degree: 0%

---


# Configuración del Editor de texto enriquecido {#configure-the-rich-text-editor}

El Editor de texto enriquecido (RTE) proporciona a los autores una amplia gama de funciones para editar contenido de texto. Se proporcionan iconos, cuadros de selección, barras de herramientas y menús para una experiencia de edición de texto WYSIWYG. Los administradores configuran RTE para habilitar, deshabilitar y ampliar las funciones disponibles en los componentes de creación. Consulte cómo los autores [utilizan RTE para crear contenido web](/help/sites-cloud/authoring/fundamentals/rich-text-editor.md).

A continuación se enumeran los conceptos y pasos de RTE necesarios para configurarlo.

| Comprender los conceptos de RTE | Habilitar las funciones necesarias | Configuración de funcionalidades individuales |
|---|---|---|
| [Explicación de la interfaz](#understand-rte-ui) | [Comprender y establecer ubicaciones de configuración](#understand-the-configuration-paths-and-locations) | [Configuración de complementos](#enable-rte-functionalities-by-activating-plug-ins) |
| [Tipos de modos de edición](#editingmodes) | [Activación de complementos](/help/implementing/developing/extending/configure-rich-text-editor-plug-ins.md#activateplugin) | [Definir propiedades de características](#aboutplugins) |
| [Acerca de los complementos](#aboutplugins) | [Configuración de las barras de herramientas RTE](#dialogfullscreen) | [Configuración de los modos de pegado](/help/implementing/developing/extending/configure-rich-text-editor-plug-ins.md#textstyles) |

## Comprender la interfaz de usuario disponible para los autores {#understand-rte-ui}

La interfaz RTE ofrece un [diseño interactivo](/help/sites-cloud/authoring/features/responsive-layout.md) para el entorno de creación. La interfaz está diseñada para utilizarse en dispositivos táctiles y de escritorio.

![Barra de herramientas del Editor de texto enriquecido](assets/rte-toolbar-full-screen-mode.png)

*Figura: Barra de herramientas del Editor de texto enriquecido con todas las opciones disponibles activadas.*

La barra de herramientas proporciona las opciones para la experiencia de creación WYSIWYG. [!DNL Experience Manager] los administradores pueden configurar las opciones disponibles en la barra de herramientas de la interfaz. De forma predeterminada, hay disponible un conjunto completo de opciones de edición en [!DNL Experience Manager]. Los desarrolladores pueden personalizar [!DNL Experience Manager] para agregar más opciones de edición.

## Varios modos de edición {#editingmodes}

Los autores pueden crear y editar contenido textual en [!DNL Experience Manager] utilizando los distintos modos de componentes. Las opciones de la barra de herramientas para crear y dar formato al contenido y la experiencia del usuario de los componentes habilitados para RTE en diferentes modos de edición varían según las configuraciones de RTE.

| Modo de edición | Área de edición | Funciones recomendadas para habilitarlas |
|--- |--- |--- |
| En línea | Edición in situ para ediciones rápidas y secundarias; Formato sin abrir un cuadro de diálogo. | Características mínimas de RTE. |
| Pantalla completa RTE | Cubre toda la página. | Todas las funciones RTE requeridas. |
| Cuadro de diálogo | Cuadro de diálogo sobre el contenido de la página, pero no cubre toda la página. | Habilite las funciones de forma juiciosa. |
| Diálogo de pantalla completa | Igual que el modo de pantalla completa; contiene campos del cuadro de diálogo junto con RTE. | Todas las funciones RTE requeridas. |

>[!NOTE]
>
>La función de edición de origen no está disponible en el modo de edición en línea. No se pueden arrastrar imágenes en el modo de pantalla completa. Todas las demás funciones funcionan en todos los modos.

### Edición en línea {#inline-editing}

Para editar el contenido dentro de una página, abra el contenido con un doble clic lento . Se presenta una barra de herramientas compacta con opciones básicas.

![Edición en línea con opciones básicas en la barra de herramientas](assets/inline-editing-mode-basic-options.png)

*Figura: Edición en línea con opciones básicas en la barra de herramientas.*

### Edición en pantalla completa{#full-screen-editing}

[!DNL Experience Manager] los componentes se pueden abrir en la vista de pantalla completa que oculta el contenido de la página y ocupa la pantalla disponible. Considere la posibilidad de editar en pantalla completa una versión detallada de la edición en línea, ya que ofrece las opciones de edición más interesantes. Se puede abrir haciendo clic en ![Icon para abrir RTE en pantalla completa](assets/rte_fullscreen.png), desde la barra de herramientas compacta cuando se utiliza el modo de edición en línea.

En el modo de pantalla completa del cuadro de diálogo, junto con una barra de herramientas RTE detallada, también están disponibles las opciones y los componentes disponibles en un cuadro de diálogo. Solo es aplicable a un cuadro de diálogo que contenga RTE junto con otros componentes.

![La barra de herramientas detallada de RTE al editar en modo de pantalla completa](assets/rte-toolbar-full-screen-mode.png)

*Figura: La barra de herramientas detallada de RTE al editar en modo de pantalla completa.*

### Edición del cuadro de diálogo {#dialog-editing}

Cuando se hace doble clic en un componente, se abre un cuadro de diálogo para editar el contenido. El cuadro de diálogo se abre sobre la página existente. En algunos casos específicos, el cuadro de diálogo se abre como una ventana emergente. Por ejemplo, cuando un componente Texto forma parte de una columna en un diseño de página de varias columnas y el área disponible para el cuadro de diálogo es menor.

![Modo de edición de cuadro de diálogo](assets/dialog_editing_modetouchui.png)

*Figura: Modo de edición del cuadro de diálogo.*

## Acerca de los complementos RTE y las funciones asociadas {#aboutplugins}

La funcionalidad está disponible a través de una serie de complementos, cada uno con:

* Una propiedad `features` que es,

   * Se utiliza para activar o desactivar la funcionalidad básica de ese complemento.
   * Configurado mediante un procedimiento estandarizado.

* Cuando proceda, más propiedades y opciones que requieran una configuración especializada.

Las funciones básicas de RTE se activan o desactivan según el valor de la propiedad `features` en un nodo específico del complemento apropiado.

La tabla siguiente muestra los complementos actuales:

* ID de complemento con un vínculo a la documentación de la API. El ID se utiliza como nombre de nodo cuando [se activa un complemento](/help/implementing/developing/extending/configure-rich-text-editor-plug-ins.md#activateplugin).
* Valores permitidos para la propiedad `features`.
* Descripción de la funcionalidad proporcionada por el complemento.

| ID del complemento | características | Descripción |
|--- |--- |--- |
| editar | `cut`,  `copy`,  `paste-default`,  `paste-plaintext`,  `paste-wordhtml` | [Corte, copie y, los tres modos](/help/implementing/developing/extending/configure-rich-text-editor-plug-ins.md#textstyles) de pegado. |
| [findreplace](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.rte.plugins.FindReplacePlugin) | `find`, `replace` | Busque y reemplace. |
| [format](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.rte.plugins.FormatPlugin) | `bold`, `italic`, `underline` | [Formato de texto básico](configure-rich-text-editor-plug-ins.md#textstyles). |
| [image](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.rte.plugins.ImagePlugin) | `image` | Compatibilidad con imágenes básicas (arrastre desde el contenido o el Buscador de contenido). En función del explorador, la compatibilidad con tiene comportamientos diferentes para los autores |
| [keys](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.rte.plugins.KeyPlugin) | - | Para definir este valor, consulte [tab size](configure-rich-text-editor-plug-ins.md#tabsize). |
| [justify](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.rte.plugins.JustifyPlugin) | `justifyleft`,  `justifycenter`,  `justifyright` | Alineación del párrafo. |
| [vínculos](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.rte.plugins.LinkPlugin) | `modifylink`,  `unlink`,  `anchor` | [Hipervínculos y anclajes](configure-rich-text-editor-plug-ins.md#linkstyles). |
| [listas](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.rte.plugins.ListPlugin) | `ordered`,  `unordered`,  `indent`,  `outdent` | Este complemento controla la [sangría y las listas](configure-rich-text-editor-plug-ins.md#indentmargin); incluir listas anidadas. |
| [misctools](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.rte.plugins.MiscToolsPlugin) | `specialchars`,  `sourceedit` | Las herramientas varias permiten a los autores introducir [caracteres especiales](configure-rich-text-editor-plug-ins.md#spchar) o editar el origen HTML. Además, puede agregar un [rango de caracteres especiales](configure-rich-text-editor-plug-ins.md#definerangechar) si desea definir su propia lista. |
| Paraformato | `paraformat` | Los formatos de párrafo predeterminados son Párrafo, Encabezado 1, Encabezado 2 y Encabezado 3 (`<p>`, `<h1>`, `<h2>` y `<h3>`). Puede [añadir más formatos de párrafo](configure-rich-text-editor-plug-ins.md#paraformats) o ampliar la lista. |
| ortografía | `checktext` | [Corrector ortográfico según la lengua](configure-rich-text-editor-plug-ins.md#adddict). |
| estilos | `styles` | Compatibilidad con estilos mediante una clase CSS. [Añada un nuevo ](configure-rich-text-editor-plug-ins.md#textstyles) estilo de texto si desea añadir (o ampliar) su propio rango de estilos para utilizarlo con el texto. |
| subsuperíndice | `subscript`,  `superscript` | Extensiones a los formatos básicos, adición de sub-script y super-script. |
| tabla | `table`,  `removetable`,  `insertrow`,  `removerow`,  `insertcolumn`,  `removecolumn`,  `cellprops`,  `mergecells`,  `splitcell`,  `selectrow`,  `selectcolumns` | Consulte [configurar estilos de tabla](configure-rich-text-editor-plug-ins.md#tablestyles) para agregar sus propios estilos para tablas completas o celdas individuales. |
| deshacer | `undo`,  `redo` | Tamaño del historial de operaciones [deshacer y rehacer](configure-rich-text-editor-plug-ins.md#undohistory). |

>[!NOTE]
>
>El complemento de pantalla completa no es compatible con el modo de diálogo. Uso de la configuración `dialogFullScreen` para configurar la barra de herramientas para el modo de pantalla completa.

## Comprender las rutas y ubicaciones de configuración {#understand-the-configuration-paths-and-locations}

El modo [de edición de RTE y la interfaz](#editingmodes) que proporcione a sus autores deciden la ubicación de los detalles de configuración cuando está [activando los complementos de RTE](configure-rich-text-editor-plug-ins.md#activateplugin). Las ubicaciones son:

* Modo en línea: `cq:editConfig/cq:inplaceEditing`.
* Modo de pantalla completa: `cq:editConfig/cq:inplaceEditing`.
* Modo de cuadro de diálogo: `cq:dialog`.
* Modo de diálogo de pantalla completa: `cq:dialog`.

>[!NOTE]
>
>No asigne al nodo `cq:inplaceEditing` el nombre `config`. En el nodo `cq:inplaceEditing`, defina las siguientes propiedades:
>
>* **Nombre**: `configPath`
>* **Tipo**: `String`
>* **Valor**: ruta del nodo que contiene la configuración real

>
>
No asigne al nodo de configuración RTE el nombre `config`. De lo contrario, las configuraciones de RTE surten efecto solo para los administradores y no para los usuarios del grupo `content-author`.

Configure las siguientes propiedades que se aplican en el modo de edición de cuadro de diálogo:

* `useFixedInlineToolbar`: Puede hacer que la barra de herramientas RTE sea fija en lugar de flotante. Establezca esta propiedad booleana definida en el nodo RTE con sling:resourceType= `cq/gui/components/authoring/dialog/richtext` en `True`. Cuando esta propiedad se establece en `True`, la edición del texto enriquecido se inicia en el evento `foundation-contentloaded`. Para evitarlo, establezca la propiedad `customStart` en `True` y déclencheur el evento `rte-start` para iniciar la edición de RTE. Cuando esta propiedad es `true`, RTE no comienza al hacer clic y este es el comportamiento predeterminado.

* `customStart`: Establezca esta propiedad booleana definida en el nodo RTE en  `True`, para controlar cuándo iniciar RTE activando el evento  `rte-start`.

* `rte-start`: Déclencheur este evento en el  `contenteditable-div` de RTE, cuándo iniciar la edición de RTE. Solo funciona si `customStart` se ha establecido en `true`.

Cuando se utiliza RTE en el cuadro de diálogo táctil, establezca la propiedad `useFixedInlineToolbar` en `true` para evitar problemas.

## Habilitar las funcionalidades RTE activando los complementos {#enable-rte-functionalities-by-activating-plug-ins}

Las funcionalidades de RTE están disponibles a través de una serie de complementos, cada uno con propiedad de características. Puede configurar la propiedad features para habilitar o deshabilitar las distintas funciones de cada complemento.

Para obtener configuraciones detalladas de los complementos RTE, consulte [cómo activar y configurar los complementos RTE](configure-rich-text-editor-plug-ins.md).

<!-- TBD ENGREVIEW: To confirm if the sample works in CS or not?
**Sample**: Download [this sample configuration](/help/sites-administering/assets/rte-sample-all-features-enabled-10.zip) that illustrates how to configure RTE. In this package all the features are enabled. -->

El [componente de texto Componentes principales](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/components/text.html#the-text-component-and-the-rich-text-editor) permite a los editores de plantillas configurar muchos complementos RTE utilizando la interfaz de usuario como políticas de contenido, lo que elimina la necesidad de una configuración técnica. Las políticas de contenido pueden funcionar con las configuraciones de la interfaz de usuario de RTE como se describe en este documento. Para obtener más información, consulte [crear plantillas de página](/help/sites-cloud/authoring/features/templates.md) y la [documentación para desarrolladores de componentes principales](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/developing/developing.html).

>Para fines de referencia, los componentes de texto predeterminados (entregados como parte de una instalación estándar) se pueden encontrar en:
>
>* `/libs/wcm/foundation/components/text`
>* `/libs/foundation/components/text`

>
>
Para crear su propio componente de texto, copie el componente anterior en lugar de editar estos componentes.

## Configurar la barra de herramientas RTE {#dialogfullscreen}

[!DNL Experience Manager] permite configurar la interfaz del Editor de texto enriquecido de forma diferente para los distintos modos de edición. A continuación se proporciona la configuración predeterminada. Puede anular estos valores predeterminados según sus necesidades. Personalice solo las funciones de la barra de herramientas que desea proporcionar a los autores. No es necesario especificar todas las configuraciones de la barra de herramientas.

Para configurar la barra de herramientas para `dialogFullScreen`, utilice la siguiente configuración de ejemplo.

```java
<uiSettings jcr:primaryType="nt:unstructured">
  <cui jcr:primaryType="nt:unstructured">
    <inline
      jcr:primaryType="nt:unstructured"
      toolbar="[format#bold,format#italic,format#underline,#justify,#lists,links#modifylink,links#unlink,#paraformat]">
      <popovers jcr:primaryType="nt:unstructured">
        <justify
          jcr:primaryType="nt:unstructured"
          items="[justify#justifyleft,justify#justifycenter,justify#justifyright,justify#justifyjustify]"
          ref="justify"/>
        <lists
          jcr:primaryType="nt:unstructured"
          items="[lists#unordered,lists#ordered,lists#outdent,lists#indent]"
          ref="lists"/>
        <paraformat
          jcr:primaryType="nt:unstructured"
          items="paraformat:getFormats:paraformat-pulldown"
          ref="paraformat"/>
      </popovers>
    </inline>
    <dialogFullScreen
      jcr:primaryType="nt:unstructured"
      toolbar="[format#bold,format#italic,format#underline,justify#justifyleft,justify#justifycenter,justify#justifyright,justify#justifyjustify,lists#unordered,lists#ordered,lists#outdent,lists#indent,links#modifylink,links#unlink,table#createoredit,#paraformat,image#imageProps]">
      <popovers jcr:primaryType="nt:unstructured">
        <paraformat
          jcr:primaryType="nt:unstructured"
          items="paraformat:getFormats:paraformat-pulldown"
          ref="paraformat"/>
      </popovers>
    </dialogFullScreen>
    <tableEditOptions
      jcr:primaryType="nt:unstructured"
      toolbar="[table#insertcolumn-before,table#insertcolumn-after,table#removecolumn,-,table#insertrow-before,table#insertrow-after,table#removerow,-,table#mergecells-right,table#mergecells-down,table#mergecells,table#splitcell-horizontal,table#splitcell-vertical,-,table#selectrow,table#selectcolumn,-,table#ensureparagraph,-,table#modifytableandcell,table#removetable,-,undo#undo,undo#redo,-,table#exitTableEditing,-]">
    </tableEditOptions>
  </cui>
</uiSettings>
```

Para el modo en línea y el modo de pantalla completa se usan diferentes configuraciones de interfaz de usuario. La propiedad toolbar especifica la opción de la barra de herramientas.

Por ejemplo, si la opción es en sí misma una función (por ejemplo, `Bold`), se especifica como `PluginName#FeatureName` (por ejemplo, `links#modifylink`).

Si la opción es una ventana emergente (que contiene algunas características de un complemento), se especifica como `#PluginName` (por ejemplo, `#format`).

Los separadores (`|`) entre un grupo de opciones se pueden especificar con `-`.

El nodo emergente en modo en línea o pantalla completa contiene una lista de las ventanas emergentes que se están utilizando. Cada nodo secundario del nodo `popovers` recibe el nombre del complemento (por ejemplo, formato). Tiene una propiedad &quot;items&quot; que contiene una lista de características del complemento (por ejemplo, format#bold).

## Configuración de la interfaz de usuario RTE y políticas de contenido {#rtecontentpolicies}

Los administradores pueden controlar las opciones de RTE mediante políticas de contenido, por ejemplo, en lugar de realizar la configuración como se ha descrito anteriormente. Las políticas de contenido definen las propiedades de diseño de un componente cuando se utilizan como parte de una [plantilla editable](/help/sites-cloud/authoring/features/templates.md). Por ejemplo, si se utiliza un componente de texto que utilice el editor de texto enriquecido con una plantilla editable, la política de contenido puede definir que la opción en negrita esté disponible y que haya algunas opciones de formato de párrafo disponibles. Las políticas de contenido se pueden reutilizar y se pueden aplicar en varias plantillas.

Las opciones disponibles en el flujo RTE descenden desde las configuraciones de la interfaz de usuario hasta las políticas de contenido.

* Los ajustes de configuración de la interfaz de usuario definen qué opciones están disponibles para las políticas de contenido.
* Si la configuración de la interfaz de usuario del RTE se ha eliminado o no permite un elemento, la directiva de contenido no puede configurarlo.
* Un autor solo tiene acceso a las funciones que están disponibles en las configuraciones de interfaz de usuario y en las políticas de contenido.

A modo de ejemplo, puede ver la [documentación de los componentes principales de texto](https://docs.adobe.com/help/en/experience-manager-core-components/using/components/text.html#the-text-component-and-the-rich-text-editor).

## Personalización de la asignación entre iconos de barra de herramientas y comandos {#iconstoolbar}

Puede personalizar la asignación entre los iconos de Coral que se muestran en la barra de herramientas de RTE y los comandos disponibles. No puede utilizar ningún otro icono aparte de los iconos de Coral.

1. Cree un nodo denominado `icons` en `uiSettings/cui`.

1. Cree nodos para iconos individuales debajo de él.
1. En cada uno de los nodos de icono individuales, especifique un icono de Coral y un comando para asignarlo al icono.

A continuación se muestra un fragmento de ejemplo para asignar el comando `Bold` al icono Coral llamado `textItalic`.

```java
<text jcr:primaryType="nt:unstructured" sling:resourceType="cq/gui/components/authoring/dialog/richtext" name="./text" useFixedInlineToolbar="{Boolean}true">
    <rtePlugins jcr:primaryType="nt:unstructured">
        <format jcr:primaryType="nt:unstructured" features="bold,italic"/>
    </rtePlugins>
    <uiSettings jcr:primaryType="nt:unstructured">
        <cui jcr:primaryType="nt:unstructured">
            <inline jcr:primaryType="nt:unstructured"
                toolbar="[format#bold,format#italic,format#underline,links#modifylink,links#unlink]">
            </inline>
            <icons jcr:primaryType="nt:unstructured">
                <bold jcr:primaryType="nt:unstructured"
                    command="format#bold"
                    icon="textItalic"/>
            </icons>
        </cui>
    </uiSettings>
</text>
```

## Limitaciones conocidas {#known-limitations}

[!DNL Experience Manager] La capacidad RTE tiene las siguientes limitaciones:

* Las capacidades de RTE solo se admiten en los cuadros de diálogo de componentes [!DNL Experience Manager]. RTE no es compatible con asistentes o formularios base.

* [!DNL Experience Manager] no funciona en dispositivos híbridos.  <!-- TBD: Check. This is not mentioned in Known Issue /help/release-notes/known-issues.md-->

* No asigne un nombre al nodo de configuración RTE `config`. De lo contrario, la configuración de RTE surte efecto solo para los administradores y no para los usuarios del grupo `content-author`.

* RTE no admite la incrustación de contenido en un marco en línea o en un iframe.

## Prácticas recomendadas y sugerencias {#best-practices-and-tips}

* Para un cuadro de diálogo flotante, habilite solo los complementos sin un cuadro de diálogo emergente. Los complementos sin ventanas emergentes tienen un tamaño menor y son más adecuados para un diálogo flotante.
* Habilite los complementos con ventanas emergentes de mayor tamaño, como el complemento `Paste`, solo en el modo de diálogo de pantalla completa o en modo de pantalla completa. Los complementos con ventanas emergentes de gran tamaño necesitan más espacio de pantalla para ofrecer una buena experiencia de creación.
* Si está utilizando complementos personalizados para CoralUI3 RTE, utilice la biblioteca `rte.coralui3`.

>[!MORELIKETHIS]
>
>* [Configuración de complementos RTE](configure-rich-text-editor-plug-ins.md)
>* [Usar el Editor de texto enriquecido para la creación](/help/sites-cloud/authoring/fundamentals/rich-text-editor.md)
>* [Configuración de RTE para sitios accesibles](rte-accessible-content.md)

