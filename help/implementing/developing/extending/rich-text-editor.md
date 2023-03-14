---
title: Configure el Editor de texto enriquecido para crear contenido en [!DNL Adobe Experience Manager] as a Cloud Service.
description: Configuración del editor de texto enriquecido para crear contenido en [!DNL Adobe Experience Manager] as a Cloud Service.
contentOwner: AG
exl-id: 1f0ff800-5e95-429a-97f2-221db0668170
source-git-commit: f5f2c7c4dfacc113994c380e8caa37508030ee92
workflow-type: tm+mt
source-wordcount: '1964'
ht-degree: 1%

---

# Configuración del editor de texto enriquecido {#configure-the-rich-text-editor}

El Editor de texto enriquecido (RTE) proporciona a los autores una amplia gama de funcionalidades para editar contenido de texto. Se proporcionan iconos, cuadros de selección, barras de herramientas y menús para una experiencia de edición de texto WYSIWYG. Los administradores configuran el RTE para habilitar, deshabilitar y ampliar las funciones disponibles en los componentes de creación. Ver cómo trabajan los autores [utilizar RTE para la creación](/help/sites-cloud/authoring/fundamentals/rich-text-editor.md) contenido web.

A continuación se enumeran los conceptos y pasos de RTE necesarios para configurarlo.

| Comprender los conceptos de RTE | Habilitar las funciones requeridas | Configuración de funcionalidades individuales |
|---|---|---|
| [Explicación de la interfaz](#understand-rte-ui) | [Comprender y establecer ubicaciones de configuración](#understand-the-configuration-paths-and-locations) | [Configuración de complementos](#enable-rte-functionalities-by-activating-plug-ins) |
| [Tipos de modos de edición](#editingmodes) | [Activación de complementos](/help/implementing/developing/extending/configure-rich-text-editor-plug-ins.md#activateplugin) | [Definir propiedades de características](#aboutplugins) |
| [Acerca de los complementos](#aboutplugins) | [Configurar las barras de herramientas RTE](#dialogfullscreen) | [Configuración de los modos de pegado](/help/implementing/developing/extending/configure-rich-text-editor-plug-ins.md#textstyles) |

## Comprender la interfaz de usuario disponible para los autores {#understand-rte-ui}

La interfaz RTE ofrece un [diseño interactivo](/help/sites-cloud/authoring/features/responsive-layout.md) para el entorno de creación. La interfaz está diseñada para su uso en dispositivos táctiles y de escritorio.

![Barra de herramientas Editor de texto enriquecido](assets/rte-toolbar-full-screen-mode.png)

*Imagen: barra de herramientas del Editor de texto enriquecido con todas las opciones disponibles habilitadas.*

La barra de herramientas proporciona las opciones para la experiencia de creación WYSIWYG. [!DNL Experience Manager] los administradores pueden configurar las opciones disponibles en la barra de herramientas de la interfaz de. Hay disponible un completo conjunto de opciones de edición de forma predeterminada en [!DNL Experience Manager]. Los desarrolladores pueden personalizar [!DNL Experience Manager] para añadir más opciones de edición.

## Varios modos de edición {#editingmodes}

Los autores pueden crear y editar contenido de texto en [!DNL Experience Manager] uso de los diferentes modos de componentes. Las opciones de la barra de herramientas para crear y dar formato al contenido, así como la experiencia del usuario con componentes con RTE en diferentes modos de edición, varían en función de las configuraciones de RTE.

| Modo de edición | Área de edición | Funciones recomendadas que se deben habilitar |
|--- |--- |--- |
| En línea | Edición in situ para realizar ediciones rápidas y secundarias; Formato sin abrir un cuadro de diálogo. | Funciones RTE mínimas. |
| RTE de pantalla completa | Abarca toda la página. | Todas las funciones RTE requeridas. |
| Cuadro de diálogo | Cuadro de diálogo en la parte superior del contenido de la página, pero no cubre toda la página. | Habilite las funciones con prudencia. |
| Pantalla completa de diálogo | Igual que el modo de pantalla completa; contiene campos del cuadro de diálogo junto con RTE. | Todas las funciones RTE requeridas. |

>[!NOTE]
>
>La función de edición de código fuente no está disponible en el modo de edición en línea. No puede arrastrar imágenes en el modo de pantalla completa. Todas las demás funciones funcionan en todos los modos.

### Edición en línea {#inline-editing}

Para editar el contenido de una página, ábralo con un doble clic lento Se presenta una barra de herramientas compacta con opciones básicas.

![Edición en línea con opciones básicas en la barra de herramientas](assets/inline-editing-mode-basic-options.png)

*Imagen: edición en línea con opciones básicas en la barra de herramientas.*

### Edición en pantalla completa {#full-screen-editing}

[!DNL Experience Manager] los componentes se pueden abrir en la vista de pantalla completa que oculta el contenido de la página y ocupa la pantalla disponible. Considere la posibilidad de editar a pantalla completa una versión detallada de la edición en línea, ya que ofrece la mayoría de las opciones de edición. Se puede abrir haciendo clic en ![Icono para abrir RTE en pantalla completa](assets/rte_fullscreen.png), en la barra de herramientas compacta cuando se utiliza el modo de edición en línea.

En el modo de pantalla completa del cuadro de diálogo, junto con una barra de herramientas RTE detallada, también están disponibles las opciones y los componentes disponibles en un cuadro de diálogo. Solo es aplicable a un cuadro de diálogo que contenga RTE junto con otros componentes.

![La barra de herramientas RTE detallada al editar en modo de pantalla completa](assets/rte-toolbar-full-screen-mode.png)

*Imagen: barra de herramientas RTE detallada al editar en modo de pantalla completa.*

### Edición de diálogos {#dialog-editing}

Al hacer doble clic en un componente, se abre un cuadro de diálogo para editar el contenido. El cuadro de diálogo se abre sobre la página existente. En algunos casos específicos, el cuadro de diálogo se abre como una ventana emergente. Por ejemplo, cuando un componente Texto forma parte de una columna en un diseño de página de varias columnas y el área disponible para el cuadro de diálogo es menor.

![Modo de edición de diálogo](assets/dialog_editing_modetouchui.png)

*Imagen: modo de edición de cuadros de diálogo.*

## Acerca de los complementos RTE y las funciones asociadas {#aboutplugins}

La funcionalidad está disponible a través de una serie de complementos, cada uno con:

* A `features` propiedad que es,

   * Se utiliza para activar o desactivar la funcionalidad básica de ese complemento.
   * Se configura con un procedimiento estandarizado.

* Si procede, más propiedades y opciones que requieran una configuración especializada.

Las funciones básicas del RTE se activan o desactivan mediante el valor del `features` en un nodo específico del complemento correspondiente.

En la tabla siguiente se enumeran los complementos actuales, mostrando:

* ID de complemento con un vínculo a la documentación de la API. El ID se utiliza como nombre de nodo cuando [activación de un complemento](/help/implementing/developing/extending/configure-rich-text-editor-plug-ins.md#activateplugin).
* Valores permitidos para `features` propiedad.
* Una descripción de la funcionalidad proporcionada por el complemento.

| ID de complemento | características | Descripción |
|--- |--- |--- |
| editar | `cut`, `copy`, `paste-default`, `paste-plaintext`, `paste-wordhtml` | [Cortar, copiar y pegar los tres modos](/help/implementing/developing/extending/configure-rich-text-editor-plug-ins.md#textstyles). |
| [findreplace](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.rte.plugins.FindReplacePlugin) | `find`, `replace` | Buscar y reemplazar. |
| [format](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.rte.plugins.FormatPlugin) | `bold`, `italic`, `underline` | [Formato de texto básico](configure-rich-text-editor-plug-ins.md#textstyles). |
| [imagen](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.rte.plugins.ImagePlugin) | `image` | Compatibilidad con imágenes básica (arrastre desde contenido o Buscador de contenido). Según el explorador, la compatibilidad tiene comportamientos diferentes para los autores |
| [teclas](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.rte.plugins.KeyPlugin) | - | Para definir este valor, consulte [tamaño de ficha](configure-rich-text-editor-plug-ins.md#tabsize). |
| [justify](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.rte.plugins.JustifyPlugin) | `justifyleft`, `justifycenter`, `justifyright` | Alineación de párrafo. |
| [vínculos](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.rte.plugins.LinkPlugin) | `modifylink`, `unlink`, `anchor` | [Hipervínculos y anclajes](configure-rich-text-editor-plug-ins.md#linkstyles). |
| [listas](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.rte.plugins.ListPlugin) | `ordered`, `unordered`, `indent`, `outdent` | Este complemento controla ambos [sangría y listas](configure-rich-text-editor-plug-ins.md#indentmargin); incluyendo listas anidadas. |
| [herramientas diversas](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.rte.plugins.MiscToolsPlugin) | `specialchars`, `sourceedit` | Varias herramientas permiten a los autores introducir [caracteres especiales](configure-rich-text-editor-plug-ins.md#spchar) o editar el origen del HTML. Además, puede agregar un [intervalo de caracteres especiales](configure-rich-text-editor-plug-ins.md#definerangechar) si desea definir su propia lista. |
| Paraformato | `paraformat` | Los formatos de párrafo predeterminados son Párrafo, Encabezado 1, Encabezado 2 y Encabezado 3 (`<p>`, `<h1>`, `<h2>`, y `<h3>`). Puede [agregar más formatos de párrafo](configure-rich-text-editor-plug-ins.md#paraformats) o ampliar la lista. |
| revisión ortográfica | `checktext` | [Corrector ortográfico según el idioma](configure-rich-text-editor-plug-ins.md#adddict). |
| estilos | `styles` | Compatibilidad con el estilo mediante una clase CSS. [Añadir nuevos estilos de texto](configure-rich-text-editor-plug-ins.md#textstyles) si desea agregar (o ampliar) su propia gama de estilos para utilizarlos con texto. |
| subíndice | `subscript`, `superscript` | Extensiones a los formatos básicos, añadiendo subíndice y superscript. |
| tabla | `table`, `removetable`, `insertrow`, `removerow`, `insertcolumn`, `removecolumn`, `cellprops`, `mergecells`, `splitcell`, `selectrow`, `selectcolumns` | Consulte [configurar estilos de tabla](configure-rich-text-editor-plug-ins.md#tablestyles) para agregar sus propios estilos para tablas completas o celdas individuales. |
| deshacer | `undo`, `redo` | Tamaño del historial de [deshacer y rehacer](configure-rich-text-editor-plug-ins.md#undohistory) operaciones. |

>[!NOTE]
>
>El complemento de pantalla completa no es compatible con el modo de diálogo. Uso del `dialogFullScreen` configuración para configurar la barra de herramientas para el modo de pantalla completa.

## Comprender las rutas y ubicaciones de configuración {#understand-the-configuration-paths-and-locations}

El [modo de edición RTE y la interfaz](#editingmodes) que proporcione para que los autores decidan la ubicación de los detalles de configuración cuando [activación de los complementos RTE](configure-rich-text-editor-plug-ins.md#activateplugin). Las ubicaciones son:

* Modo en línea: `cq:editConfig/cq:inplaceEditing`.
* Modo de pantalla completa: `cq:editConfig/cq:inplaceEditing`.
* Modo de diálogo: `cq:dialog`.
* Modo de diálogo de pantalla completa: `cq:dialog`.

>[!NOTE]
>
>No asigne un nombre al nodo en `cq:inplaceEditing` as `config`. Activado `cq:inplaceEditing` , defina las siguientes propiedades:
>
>* **Nombre**: `configPath`
>* **Tipo**: `String`
>* **Valor**: ruta del nodo que contiene la configuración real
>
>No asigne un nombre al nodo de configuración RTE como `config`. De lo contrario, las configuraciones de RTE se aplican solo para los administradores y no para los usuarios del grupo `content-author`.

Configure las siguientes propiedades que se aplican en el modo de edición del cuadro de diálogo:

* `useFixedInlineToolbar`: puede hacer que la barra de herramientas RTE sea fija en lugar de flotante. Establezca esta propiedad booleana definida en el nodo RTE con sling:resourceType= `cq/gui/components/authoring/dialog/richtext` hasta `True`. Cuando esta propiedad se establece en `True`, la edición de texto enriquecido se inicia en la `foundation-contentloaded` evento. Para evitarlo, establezca la propiedad `customStart` hasta `True` y déclencheur el `rte-start` evento para iniciar la edición RTE. Cuando esta propiedad es `true`, RTE no comienza haciendo clic en y este es el comportamiento predeterminado.

* `customStart`: establezca esta propiedad booleana definida en el nodo RTE en `True`, para controlar cuándo iniciar RTE activando el evento `rte-start`.

* `rte-start`: Almacene en Déclencheur este evento en la `contenteditable-div` de RTE, cuándo iniciar la edición de RTE. Solo funciona si `customStart` se ha establecido en `true`.

Cuando se utiliza RTE en el cuadro de diálogo táctil, establezca la propiedad `useFixedInlineToolbar` hasta `true` para evitar problemas.

## Habilitar las funcionalidades de RTE activando complementos {#enable-rte-functionalities-by-activating-plug-ins}

Las funcionalidades de RTE están disponibles a través de una serie de complementos, cada uno con la propiedad features. Puede configurar la propiedad features para habilitar o deshabilitar las distintas funciones de cada complemento.

Para obtener configuraciones detalladas de los complementos RTE, consulte [Cómo activar y configurar los complementos RTE](configure-rich-text-editor-plug-ins.md).

<!-- TBD ENGREVIEW: To confirm if the sample works in CS or not?
**Sample**: Download [this sample configuration](/help/sites-administering/assets/rte-sample-all-features-enabled-10.zip) that illustrates how to configure RTE. In this package all the features are enabled. -->

El [Componente de texto de los componentes principales](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/text.html#the-text-component-and-the-rich-text-editor) permite a los editores de plantillas configurar muchos complementos RTE utilizando la interfaz de usuario como directivas de contenido, lo que elimina la necesidad de configuración técnica. Las políticas de contenido pueden funcionar con configuraciones de IU RTE como se describe en este documento. Para obtener más información, consulte [crear plantillas de página](/help/sites-cloud/authoring/features/templates.md) y el [Documentación para desarrolladores de componentes principales](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/developing.html).

>Para fines de referencia, los componentes de texto predeterminados (entregados como parte de una instalación estándar) se encuentran en:
>
>* `/libs/wcm/foundation/components/text`
>* `/libs/foundation/components/text`
>
>Para crear su propio componente de texto, copie el componente anterior en lugar de editar estos componentes.

## Configuración de la barra de herramientas RTE {#dialogfullscreen}

[!DNL Experience Manager] permite configurar la interfaz del Editor de texto enriquecido de forma diferente para los distintos modos de edición. A continuación se proporcionan los ajustes predeterminados. Puede sustituir estos valores predeterminados según sus necesidades. Puede personalizar únicamente las características de la barra de herramientas que desea proporcionar a los autores. No es necesario especificar todas las configuraciones de la barra de herramientas.

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

Se utilizan diferentes configuraciones de interfaz de usuario para el modo en línea y el modo de pantalla completa. La propiedad toolbar especifica la opción de la barra de herramientas.

Por ejemplo, si la opción es en sí misma una función (por ejemplo, `Bold`), se especifica como `PluginName#FeatureName` (por ejemplo, `links#modifylink`).

Si la opción es una ventana emergente (que contiene algunas funciones de un complemento), se especifica como `#PluginName` (por ejemplo, `#format`).

Separadores (`|`) entre un grupo de opciones se puede especificar con `-`.

El nodo emergente bajo el modo en línea o de pantalla completa contiene una lista de las ventanas emergentes que se están utilizando. Cada nodo secundario bajo el `popovers` Este nodo recibe el nombre del complemento (por ejemplo, formato). Tiene una propiedad &quot;items&quot; que contiene una lista de funciones del complemento (por ejemplo, format#bold).

## Configuración de la interfaz de usuario de RTE y políticas de contenido {#rtecontentpolicies}

Los administradores pueden controlar las opciones de RTE mediante políticas de contenido, por ejemplo, en lugar de realizar la configuración como se ha descrito anteriormente. Las políticas de contenido definen las propiedades de diseño de un componente cuando se utilizan como parte de una [plantilla editable](/help/sites-cloud/authoring/features/templates.md). Por ejemplo, si un componente de texto que utiliza RTE se utiliza con una plantilla editable, la política de contenido puede definir que la opción de negrita esté disponible y que haya algunas opciones de formato de párrafo disponibles. Las políticas de contenido se pueden reutilizar y aplicar en varias plantillas.

Las opciones disponibles en RTE fluyen hacia abajo desde las configuraciones de interfaz de usuario hasta las políticas de contenido.

* Las opciones de configuración de la interfaz de usuario definen qué opciones están disponibles para las directivas de contenido.
* Si la configuración de interfaz de usuario de RTE se ha eliminado o no habilita un elemento, la directiva de contenido no puede configurarlo.
* Un autor solo tiene acceso a las funciones que están disponibles en las configuraciones de interfaz de usuario y en las directivas de contenido.

A modo de ejemplo, puede ver el [Documentación del componente principal Texto](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/text.html#the-text-component-and-the-rich-text-editor).

## Personalizar la asignación entre los iconos y comandos de la barra de herramientas {#iconstoolbar}

Puede personalizar la asignación entre los iconos de Coral que se muestran en la barra de herramientas RTE y los comandos disponibles. No se puede usar ningún otro icono aparte de los iconos de Coral.

1. Cree un nodo llamado `icons` bajo `uiSettings/cui`.

1. Cree nodos para los iconos individuales debajo de ella.
1. En cada uno de los nodos de icono individuales, especifique un icono de Coral y un comando para asignarlo al icono.

A continuación se muestra un fragmento de ejemplo para asignar el comando `Bold` al icono de Coral denominado `textItalic`.

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

* Las capacidades de RTE solo son compatibles en [!DNL Experience Manager] cuadros de diálogo de componentes. RTE no es compatible con asistentes ni formularios base.

* [!DNL Experience Manager] no funciona en dispositivos híbridos. <!-- TBD: Check. This is not mentioned in Known Issue /help/release-notes/known-issues.md-->

* No asigne un nombre al nodo de configuración RTE `config`. De lo contrario, la configuración de RTE se aplica solo para los administradores y no para los usuarios del grupo `content-author`.

* RTE no admite la incrustación de contenido en un marco dentro de la línea o en un iframe.

## Prácticas recomendadas y sugerencias {#best-practices-and-tips}

* Para un cuadro de diálogo flotante, habilite solo los complementos sin cuadro de diálogo emergente. Los complementos sin ventanas emergentes son de menor tamaño y son los más adecuados para un cuadro de diálogo flotante.
* Habilite los complementos con ventanas emergentes de mayor tamaño, como `Paste` complemento, solo en el modo de diálogo de pantalla completa o en el modo de pantalla completa. Los complementos con ventanas emergentes grandes necesitan más espacio en la pantalla para proporcionar una buena experiencia de creación.
* Si utiliza complementos personalizados para CoralUI3 RTE, utilice `rte.coralui3` biblioteca.

>[!MORELIKETHIS]
>
>* [Configuración de complementos RTE](configure-rich-text-editor-plug-ins.md)
>* [Uso del Editor de texto enriquecido para la creación](/help/sites-cloud/authoring/fundamentals/rich-text-editor.md)
>* [Configuración de RTE para sitios accesibles](rte-accessible-content.md)

