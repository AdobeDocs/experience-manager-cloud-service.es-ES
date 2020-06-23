---
title: Configure el Editor de texto enriquecido para que cree contenido [!DNL Adobe Experience Manager] en un Cloud Service.
description: Configure el Editor de texto enriquecido para que cree contenido [!DNL Adobe Experience Manager] en un Cloud Service.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 739dde6f9a6a7f4fe773e27e53f23a395f2881dc
workflow-type: tm+mt
source-wordcount: '1981'
ht-degree: 0%

---


# Configure the Rich Text Editor {#configure-the-rich-text-editor}

El editor de texto enriquecido (RTE) ofrece a los autores una amplia gama de funciones para editar el contenido del texto. Se proporcionan iconos, cuadros de selección, barras de herramientas y menús para una experiencia de edición de texto WYSIWYG. Los administradores configuran RTE para habilitar, deshabilitar y ampliar las funciones disponibles en los componentes de creación. Vea cómo los autores [utilizan RTE para crear](/help/sites-cloud/authoring/fundamentals/rich-text-editor.md) contenido web.

A continuación se enumeran los conceptos y pasos RTE necesarios para configurarlo.

| Comprender los conceptos RTE | Habilitar las funciones necesarias | Configurar funciones individuales |
|---|---|---|
| [Comprender la interfaz](#understand-rte-ui) | [Comprender y establecer ubicaciones de configuración](#understand-the-configuration-paths-and-locations) | [Configurar complementos](#enable-rte-functionalities-by-activating-plug-ins) |
| [Tipos de modos de edición](#editingmodes) | [Activar complementos](/help/implementing/developing/extending/configure-rich-text-editor-plug-ins.md#activateplugin) | [Definir propiedades de funciones](#aboutplugins) |
| [Acerca de los complementos](#aboutplugins) | [Configurar barras de herramientas RTE](#dialogfullscreen) | [Configuración de los modos de pegado](/help/implementing/developing/extending/configure-rich-text-editor-plug-ins.md#textstyles) |

## Comprender la interfaz de usuario disponible para los autores {#understand-rte-ui}

La interfaz RTE oferta un diseño [](/help/sites-cloud/authoring/features/responsive-layout.md) interactivo para el entorno de creación. La interfaz está diseñada para utilizarse en dispositivos táctiles y de escritorio.

![Barra de herramientas del Editor de texto enriquecido](assets/rte-toolbar-full-screen-mode.png)

*Figura: Barra de herramientas del Editor de texto enriquecido con todas las opciones disponibles activadas.*

La barra de herramientas proporciona las opciones para la experiencia de creación WYSIWYG. [!DNL Experience Manager] los administradores pueden configurar las opciones disponibles en la barra de herramientas de la interfaz. De forma predeterminada, hay disponible un conjunto completo de opciones de edición en [!DNL Experience Manager]. Los desarrolladores pueden personalizar [!DNL Experience Manager] para agregar más opciones de edición.

## Diversos modos de edición {#editingmodes}

Los autores pueden crear y editar contenido textual [!DNL Experience Manager] utilizando los distintos modos de componentes. Las opciones de la barra de herramientas para crear y dar formato al contenido y la experiencia del usuario de los componentes habilitados para RTE en diferentes modos de edición varían según las configuraciones de RTE.

| Modo de edición | Área de edición | Funciones recomendadas para habilitarlas |
|--- |--- |--- |
| En línea | Edición in situ para ediciones rápidas y secundarias; Formato sin abrir un cuadro de diálogo. | Características mínimas de RTE. |
| RTE a pantalla completa | Abarca toda la página. | Todas las funciones RTE requeridas. |
| Cuadro de diálogo | Cuadro de diálogo en la parte superior del contenido de la página pero no cubre toda la página. | Activar las funciones de forma juiciosa. |
| Pantalla completa del cuadro de diálogo | Igual que el modo de pantalla completa; contiene campos del cuadro de diálogo junto con RTE. | Todas las funciones RTE requeridas. |

>[!NOTE]
>
>La función de edición de origen no está disponible en el modo de edición en línea. No se pueden arrastrar imágenes en el modo de pantalla completa. Todas las demás funciones funcionan en todos los modos.

### Edición en línea {#inline-editing}

Para editar el contenido dentro de una página, abra el contenido con un doble lento y haga clic en . Se presenta una barra de herramientas compacta con opciones básicas.

![Edición en línea con opciones básicas en la barra de herramientas](assets/inline-editing-mode-basic-options.png)

*Figura: Edición en línea con opciones básicas en la barra de herramientas.*

### Full-screen editing {#full-screen-editing}

[!DNL Experience Manager] los componentes se pueden abrir en una vista de pantalla completa que oculta el contenido de la página y ocupa la pantalla disponible. Considere la posibilidad de editar a pantalla completa con una versión detallada de la edición en línea, ya que oferta la mayoría de las opciones de edición. Se puede abrir haciendo clic en ![Icono para abrir RTE en pantalla](assets/rte_fullscreen.png)completa, desde la barra de herramientas compacta cuando se utiliza el modo de edición en línea.

En el modo de pantalla completa del cuadro de diálogo, junto con una barra de herramientas RTE detallada, también están disponibles las opciones y los componentes disponibles en un cuadro de diálogo. Solo se aplica a un cuadro de diálogo que contenga RTE junto con otros componentes.

![Barra de herramientas RTE detallada al editar en modo de pantalla completa](assets/rte-toolbar-full-screen-mode.png)

*Figura: Barra de herramientas RTE detallada al editar en modo de pantalla completa.*

### Edición de cuadro de diálogo {#dialog-editing}

Cuando se hace clic en un componente mediante doble, se abre un cuadro de diálogo para editar el contenido. El cuadro de diálogo se abre sobre la página existente. En algunos casos específicos, el cuadro de diálogo se abre como una ventana emergente. Por ejemplo, cuando un componente Texto forma parte de una columna en un diseño de página de varias columnas y el área disponible para el cuadro de diálogo es menor.

![Modo de edición de cuadro de diálogo](assets/dialog_editing_modetouchui.png)

*Figura: Modo de edición de cuadro de diálogo.*

## Acerca de los complementos RTE y las funciones asociadas {#aboutplugins}

La funcionalidad está disponible mediante una serie de complementos, cada uno con:

* Una `features` propiedad que es,

   * Se utiliza para activar o desactivar la funcionalidad básica de ese complemento.
   * Configurado mediante un procedimiento estandarizado.

* Cuando proceda, más propiedades y opciones que requieran una configuración especializada.

Las funciones básicas de RTE se activan o desactivan por el valor de la `features` propiedad en un nodo específico del complemento adecuado.

La siguiente tabla lista los complementos actuales y muestra:

* ID de complementos con un vínculo a la documentación de API. El ID se utiliza como nombre de nodo al [activar un complemento](/help/implementing/developing/extending/configure-rich-text-editor-plug-ins.md#activateplugin).
* Valores permitidos para la `features` propiedad.
* Descripción de la funcionalidad proporcionada por el complemento.

| ID del complemento | características | Descripción |
|--- |--- |--- |
| editar | `cut`, `copy`, `paste-default`, `paste-plaintext`, `paste-wordhtml` | [Cortar, copiar y pegar los tres modos](/help/implementing/developing/extending/configure-rich-text-editor-plug-ins.md#textstyles). |
| [findreplace](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.rte.plugins.FindReplacePlugin) | `find`, `replace` | Buscar y reemplazar. |
| [format](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.rte.plugins.FormatPlugin) | `bold`, `italic`, `underline` | [Formato](configure-rich-text-editor-plug-ins.md#textstyles)de texto básico. |
| [image](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.rte.plugins.ImagePlugin) | `image` | Compatibilidad básica con imágenes (arrastre desde el contenido o desde el buscador de contenido). Según el explorador, la compatibilidad con los autores tiene comportamientos diferentes |
| [claves](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.rte.plugins.KeyPlugin) | - | Para definir este valor, consulte Tamaño [de tabulación](configure-rich-text-editor-plug-ins.md#tabsize). |
| [justify](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.rte.plugins.JustifyPlugin) | `justifyleft`, `justifycenter`, `justifyright` | Alineación de párrafo. |
| [vínculos](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.rte.plugins.LinkPlugin) | `modifylink`, `unlink`, `anchor` | [Hipervínculos y anclajes](configure-rich-text-editor-plug-ins.md#linkstyles). |
| [listas](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.rte.plugins.ListPlugin) | `ordered`, `unordered`, `indent`, `outdent` | Este complemento controla tanto la [sangría como las listas](configure-rich-text-editor-plug-ins.md#indentmargin); incluyendo listas anidadas. |
| [misctools](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.rte.plugins.MiscToolsPlugin) | `specialchars`, `sourceedit` | Varias herramientas permiten a los autores introducir caracteres [](configure-rich-text-editor-plug-ins.md#spchar) especiales o editar el origen HTML. Además, puede agregar un [rango de caracteres](configure-rich-text-editor-plug-ins.md#definerangechar) especiales si desea definir su propia lista. |
| Paraformat | `paraformat` | Los formatos de párrafo predeterminados son Párrafo, Encabezado 1, Encabezado 2 y Encabezado 3 (`<p>`, `<h1>`, `<h2>`y `<h3>`). Puede [agregar más formatos](configure-rich-text-editor-plug-ins.md#paraformats) de párrafo o extender la lista. |
| spellcheck | `checktext` | [Corrector ortográfico](configure-rich-text-editor-plug-ins.md#adddict)con conocimiento del idioma. |
| estilos | `styles` | Compatibilidad con estilos mediante una clase CSS. [Añada nuevos estilos](configure-rich-text-editor-plug-ins.md#textstyles) de texto si desea agregar (o ampliar) su propia gama de estilos para utilizarlos con texto. |
| subsuperíndice | `subscript`, `superscript` | Extensiones a los formatos básicos, agregando sub-script y super-script. |
| tabla | `table`, `removetable`, `insertrow`, `removerow`, `insertcolumn`, `removecolumn`, `cellprops`, `mergecells`, `splitcell`, `selectrow`, `selectcolumns` | Consulte [Configuración de estilos](configure-rich-text-editor-plug-ins.md#tablestyles) de tabla para agregar sus propios estilos a tablas enteras o celdas individuales. |
| deshacer | `undo`, `redo` | Tamaño del historial de las operaciones de [deshacer y rehacer](configure-rich-text-editor-plug-ins.md#undohistory) . |

>[!NOTE]
>
>El complemento de pantalla completa no es compatible con el modo de cuadro de diálogo. Uso de la `dialogFullScreen` configuración para configurar la barra de herramientas para el modo de pantalla completa.

## Conocer las rutas y ubicaciones de configuración {#understand-the-configuration-paths-and-locations}

El [modo de edición RTE y la interfaz](#editingmodes) que se proporciona a los autores determinan la ubicación de los detalles de configuración al [activar los complementos](configure-rich-text-editor-plug-ins.md#activateplugin)RTE. Las ubicaciones son:

* Modo en línea: `cq:editConfig/cq:inplaceEditing`.
* Modo de pantalla completa: `cq:editConfig/cq:inplaceEditing`.
* Modo de cuadro de diálogo: `cq:dialog`.
* Modo de cuadro de diálogo de pantalla completa: `cq:dialog`.

>[!NOTE]
>
>No asigne un nombre al nodo en `cq:inplaceEditing` como `config`. En el `cq:inplaceEditing` nodo, defina las siguientes propiedades:
>
>* **Nombre**: `configPath`
>* **Tipo**: `String`
>* **Valor**: ruta del nodo que contiene la configuración real
>
>
No asigne un nombre al nodo de configuración RTE como `config`. De lo contrario, las configuraciones de RTE surtirán efecto únicamente para los administradores y no para los usuarios del grupo `content-author`.

Configure las siguientes propiedades que se aplican en el modo de edición de cuadro de diálogo:

* `useFixedInlineToolbar`:: Puede hacer que la barra de herramientas RTE sea fija en lugar de flotante. Establezca esta propiedad booleana definida en el nodo RTE con sling:resourceType= `cq/gui/components/authoring/dialog/richtext` en `True`. Cuando esta propiedad se establece en `True`, la edición de texto enriquecido se inicia en el `foundation-contentloaded` evento. Para evitarlo, establezca la propiedad `customStart` en `True` y active el `rte-start` evento en inicio RTE. Cuando esta propiedad es `true`, RTE no tiene el inicio de hacer clic y este es el comportamiento predeterminado.

* `customStart`:: Establezca esta propiedad booleana definida en el nodo RTE en `True`, para controlar cuándo se debe activar el inicio RTE activando el evento `rte-start`.

* `rte-start`:: Activar este evento en la `contenteditable-div` parte de RTE, cuándo editar inicio RTE. Funciona sólo si `customStart` se ha establecido en `true`.

Cuando se utiliza RTE en el cuadro de diálogo táctil, establezca la propiedad `useFixedInlineToolbar` para `true` evitar problemas.

## Activar las funcionalidades RTE mediante la activación de complementos {#enable-rte-functionalities-by-activating-plug-ins}

Las funcionalidades RTE están disponibles a través de una serie de complementos, cada uno con propiedad de características. Puede configurar la propiedad features para habilitar o deshabilitar las diversas características de cada complemento.

Para obtener configuraciones detalladas de los complementos RTE, consulte [cómo activar y configurar los complementos](configure-rich-text-editor-plug-ins.md)RTE.

<!-- TBD ENGREVIEW: To confirm if the sample works in CS or not?
**Sample**: Download [this sample configuration](/help/sites-administering/assets/rte-sample-all-features-enabled-10.zip) that illustrates how to configure RTE. In this package all the features are enabled. -->

El componente [de texto Componentes](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/components/text.html#the-text-component-and-the-rich-text-editor) principales permite a los editores de plantillas configurar muchos complementos RTE mediante la interfaz de usuario como políticas de contenido, lo que elimina la necesidad de una configuración técnica. Las políticas de contenido pueden funcionar con las configuraciones de la interfaz de usuario de RTE como se describe en este documento. Para obtener más información, consulte [Creación de plantillas](/help/sites-cloud/authoring/features/templates.md) de página y documentación [para desarrolladores de componentes](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/developing/developing.html)principales.

>Para fines de referencia, los componentes de texto predeterminados (entregados como parte de una instalación estándar) se encuentran en:
>
>* `/libs/wcm/foundation/components/text`
>* `/libs/foundation/components/text`
>
>
Para crear su propio componente de texto, copie el componente anterior en lugar de editar estos componentes.

## Configurar barra de herramientas RTE {#dialogfullscreen}

[!DNL Experience Manager] permite configurar la interfaz para el Editor de texto enriquecido de forma diferente para los distintos modos de edición. A continuación se proporciona la configuración predeterminada. Puede anular estos valores predeterminados según sus necesidades. Solo puede personalizar las funciones de la barra de herramientas que desea proporcionar a los autores. No es necesario especificar todas las configuraciones de la barra de herramientas.

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

Para el modo en línea y el modo de pantalla completa se utilizan diferentes configuraciones de interfaz de usuario. La propiedad toolbar especifica la opción de la barra de herramientas.

Por ejemplo, si la opción es en sí misma una característica (por ejemplo, `Bold`), se especifica como `PluginName#FeatureName` (por ejemplo, `links#modifylink`).

Si la opción es una ventana emergente (que contiene algunas características de un complemento), se especifica como `#PluginName` (por ejemplo, `#format`).

Los separadores (`|`) entre un grupo de opciones se pueden especificar con `-`.

El nodo emergente en el modo en línea o en pantalla completa contiene una lista de las ventanas emergentes que se utilizan. Cada nodo secundario del `popovers` nodo recibe el nombre del complemento (por ejemplo, formato). Tiene una propiedad &#39;items&#39; que contiene una lista de características del complemento (por ejemplo, format#bold).

## Configuración de la interfaz de usuario RTE y directivas de contenido {#rtecontentpolicies}

Los administradores pueden controlar las opciones de RTE mediante políticas de contenido, por ejemplo, en lugar de realizar la configuración como se ha descrito anteriormente. Las políticas de contenido definen las propiedades de diseño de un componente cuando se utilizan como parte de una plantilla [](/help/sites-cloud/authoring/features/templates.md)editable. Por ejemplo, si se utiliza un componente de texto que utiliza RTE con una plantilla editable, la política de contenido puede definir que la opción de negrita esté disponible y que haya algunas opciones de formato de párrafo disponibles. Las políticas de contenido son reutilizables y se pueden aplicar en varias plantillas.

Las opciones disponibles en el flujo RTE desde las configuraciones de la interfaz de usuario hasta las políticas de contenido.

* La configuración de la interfaz de usuario define las opciones disponibles para las directivas de contenido.
* Si la configuración de la interfaz de usuario de RTE se elimina o no activa un elemento, la directiva de contenido no puede configurarlo.
* Un autor solo tiene acceso a la funcionalidad que están disponibles en las configuraciones de la interfaz de usuario y en las políticas de contenido.

Como ejemplo, puede ver la documentación [del componente](https://docs.adobe.com/help/en/experience-manager-core-components/using/components/text.html#the-text-component-and-the-rich-text-editor)Texto principal.

## Personalización de la asignación entre iconos y comandos de la barra de herramientas {#iconstoolbar}

Puede personalizar la asignación entre los iconos de Coral que se muestran en la barra de herramientas de RTE y los comandos disponibles. No puede utilizar ningún otro icono aparte de los iconos de Coral.

1. Cree un nodo con el nombre `icons` debajo de `uiSettings/cui`.

1. Cree nodos para iconos individuales debajo de él.
1. En cada uno de los nodos de icono individuales, especifique un icono de Coral y un comando para asignarlo al icono.

A continuación se muestra un fragmento de ejemplo para asignar el comando `Bold` al icono Coral denominado `textItalic`.

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

* Las funciones RTE solo se admiten en los cuadros de diálogo de [!DNL Experience Manager] componentes. RTE no se admite en asistentes o formularios de base.

* [!DNL Experience Manager] no funciona en dispositivos híbridos. <!-- TBD: Check. This is not mentioned in Known Issue /help/release-notes/known-issues.md-->

* No asigne un nombre al nodo de configuración RTE `config`. De lo contrario, la configuración RTE solo se aplica a los administradores y no a los usuarios del grupo `content-author`.

* RTE no admite la incrustación de contenido en un marco integrado o un iframe.

## Best practices and tips {#best-practices-and-tips}

* Para un cuadro de diálogo flotante, habilite solo los complementos sin un cuadro de diálogo emergente. Los complementos sin ventanas emergentes tienen un tamaño menor y son más adecuados para un cuadro de diálogo flotante.
* Habilite los complementos con ventanas emergentes más grandes, como el `Paste` complemento, solo en el modo de cuadro de diálogo de pantalla completa o en el modo de pantalla completa. Los complementos con ventanas emergentes de gran tamaño necesitan más espacio de pantalla para ofrecer una buena experiencia de creación.
* Si utiliza complementos personalizados para CoralUI3 RTE, utilice `rte.coralui3` library.

>[!MORELIKETHIS]
>
>* [Configuración de complementos RTE](configure-rich-text-editor-plug-ins.md)
>* [Usar editor de texto enriquecido para la creación](/help/sites-cloud/authoring/fundamentals/rich-text-editor.md)
>* [Configurar RTE para sitios accesibles](rte-accessible-content.md)
>* [Ejemplo de tutorial para crear un componente de varios campos compuesto](https://experience-aem.blogspot.com/2019/05/aem-65-touchui-composite-multifield-with-coral3-rte-rich-text.html)

