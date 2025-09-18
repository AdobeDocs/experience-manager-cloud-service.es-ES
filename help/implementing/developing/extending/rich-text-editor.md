---
title: Configure el Editor de texto enriquecido para crear contenido en  [!DNL Adobe Experience Manager] as a Cloud Service.
description: Configure el Editor de texto enriquecido para crear contenido en  [!DNL Adobe Experience Manager] as a Cloud Service.
contentOwner: AG
exl-id: 1f0ff800-5e95-429a-97f2-221db0668170
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 2c1b444d7b7dad94cc9ebda59783f9c6fde84a91
workflow-type: tm+mt
source-wordcount: '1892'
ht-degree: 0%

---


# Configuración del editor de texto enriquecido {#configure-the-rich-text-editor}

El Editor de texto enriquecido (RTE) proporciona a los autores una amplia gama de funcionalidades para editar contenido de texto. Se proporcionan iconos, cuadros de selección, barras de herramientas y menús para una experiencia de edición de texto de WYSIWYG. Los administradores configuran el RTE para habilitar, deshabilitar y ampliar las funciones disponibles en los componentes de creación. Vea cómo los autores [utilizan RTE para crear](/help/sites-cloud/authoring/page-editor/rich-text-editor.md) contenido web.

A continuación se enumeran los conceptos y pasos de RTE necesarios para configurarlo.

| Comprender los conceptos de RTE | Habilitar las funciones requeridas | Configuración de funcionalidades individuales |
|---|---|---|
| [Comprenda la interfaz](#understand-rte-ui) | [Comprender y establecer ubicaciones de configuración](#understand-the-configuration-paths-and-locations) | [Configurar complementos](#enable-rte-functionalities-by-activating-plug-ins) |
| [Tipos de modos de edición](#editingmodes) | [Activar complementos](/help/implementing/developing/extending/configure-rich-text-editor-plug-ins.md#activateplugin) | [Establecer propiedades de características](#aboutplugins) |
| [Acerca de los complementos](#aboutplugins) | [Configurar barras de herramientas RTE](#dialogfullscreen) | [Configurar los modos de pegado](/help/implementing/developing/extending/configure-rich-text-editor-plug-ins.md#textstyles) |

>[!NOTE]
>
>El RTE descrito en este documento describe el que está disponible en el Editor de páginas. Si está usando el editor universal moderno, consulte el documento [Configuración del RTE para el editor universal](/help/implementing/universal-editor/configure-rte.md) para obtener detalles.

## Comprender la interfaz de usuario disponible para los autores {#understand-rte-ui}

La interfaz RTE ofrece un [diseño interactivo](/help/sites-cloud/authoring/page-editor/responsive-layout.md) para el entorno de creación. La interfaz está diseñada para su uso en dispositivos táctiles y de escritorio.

![Barra de herramientas del Editor de texto enriquecido](assets/rte-toolbar-full-screen-mode.png)

*Figura: barra de herramientas del Editor de texto enriquecido con todas las opciones disponibles habilitadas.*

La barra de herramientas proporciona las opciones para la experiencia de creación de WYSIWYG. Los administradores de [!DNL Experience Manager] pueden configurar las opciones disponibles en la barra de herramientas de la interfaz. Hay disponible un conjunto completo de opciones de edición de forma predeterminada en [!DNL Experience Manager]. Los desarrolladores pueden personalizar [!DNL Experience Manager] para agregar más opciones de edición.

## Varios modos de edición {#editingmodes}

Los autores pueden crear y editar contenido textual en [!DNL Experience Manager] mediante los diferentes modos de componentes. Las opciones de la barra de herramientas para crear y dar formato al contenido, así como la experiencia del usuario con componentes con RTE en diferentes modos de edición, varían en función de las configuraciones de RTE.

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

*Figura: Edición en línea con opciones básicas en la barra de herramientas.*

### Edición en pantalla completa {#full-screen-editing}

[!DNL Experience Manager] componentes se pueden abrir en la vista de pantalla completa que oculta el contenido de la página y ocupa la pantalla disponible. Considere la posibilidad de editar a pantalla completa una versión detallada de la edición en línea, ya que ofrece la mayoría de las opciones de edición. Se puede abrir haciendo clic en ![Icono para abrir RTE en pantalla completa](assets/rte_fullscreen.png), desde la barra de herramientas compacta cuando se utiliza el modo de edición en línea.

En el modo de pantalla completa del cuadro de diálogo, junto con una barra de herramientas RTE detallada, también están disponibles las opciones y los componentes disponibles en un cuadro de diálogo. Solo es aplicable a un cuadro de diálogo que contenga RTE junto con otros componentes.

![La barra de herramientas RTE detallada al editar en modo de pantalla completa](assets/rte-toolbar-full-screen-mode.png)

*Imagen: barra de herramientas RTE detallada al editar en modo de pantalla completa.*

### Edición de diálogos {#dialog-editing}

Al hacer doble clic en un componente, se abre un cuadro de diálogo para editar el contenido. El cuadro de diálogo se abre sobre la página existente. En algunos casos específicos, el cuadro de diálogo se abre como una ventana emergente. Por ejemplo, cuando un componente Texto forma parte de una columna en un diseño de página de varias columnas y el área disponible para el cuadro de diálogo es menor.

![Modo de edición de diálogo](assets/dialog_editing_modetouchui.png)

*Figura: Modo de edición de diálogo.*

## Acerca de los complementos RTE y las funciones asociadas {#aboutplugins}

La funcionalidad está disponible a través de una serie de complementos, cada uno con:

* Una propiedad `features` que es,

   * Se utiliza para activar o desactivar la funcionalidad básica de ese complemento.
   * Se configura con un procedimiento estandarizado.

* Si procede, más propiedades y opciones que requieran una configuración especializada.

Las características básicas del RTE se activan o desactivan mediante el valor de la propiedad `features` en un nodo específico del complemento correspondiente.

En la tabla siguiente se enumeran los complementos actuales, mostrando:

* ID de complemento con un vínculo a la documentación de la API. El identificador se usa como nombre de nodo al [activar un complemento](/help/implementing/developing/extending/configure-rich-text-editor-plug-ins.md#activateplugin).
* Valores permitidos para la propiedad `features`.
* Una descripción de la funcionalidad proporcionada por el complemento.

| ID de complemento | características | Descripción |
|--- |--- |--- |
| editar | `cut`, `copy`, `paste-default`, `paste-plaintext`, `paste-wordhtml` | [Cortar, copiar y pegar los tres modos](/help/implementing/developing/extending/configure-rich-text-editor-plug-ins.md#textstyles). |
| findreplace | `find`, `replace` | Buscar y reemplazar. |
| formato | `bold`, `italic`, `underline` | [Formato de texto básico](configure-rich-text-editor-plug-ins.md#textstyles). |
| image | `image` | Compatibilidad con imágenes básica (arrastre desde contenido o Buscador de contenido). Según el explorador, la compatibilidad tiene comportamientos diferentes para los autores |
| teclas | - | Para definir este valor, consulte [tamaño de ficha](configure-rich-text-editor-plug-ins.md#tabsize). |
| justificar | `justifyleft`, `justifycenter`, `justifyright` | Alineación de párrafo. |
| vínculos | `modifylink`, `unlink`, `anchor` | [Hipervínculos y anclajes](configure-rich-text-editor-plug-ins.md#linkstyles). |
| listas | `ordered`, `unordered`, `indent`, `outdent` | Este complemento controla tanto la sangría [como las listas](configure-rich-text-editor-plug-ins.md#indentmargin); incluidas las listas anidadas. |
| herramientas diversas | `specialchars`, `sourceedit` | Varias herramientas permiten a los autores introducir [caracteres especiales](configure-rich-text-editor-plug-ins.md#spchar) o editar el origen de HTML. Además, puede agregar un [rango de caracteres especiales](configure-rich-text-editor-plug-ins.md#definerangechar) si desea definir su propia lista. |
| Paraformato | `paraformat` | Los formatos de párrafo predeterminados son Párrafo, Encabezado 1, Encabezado 2 y Encabezado 3 (`<p>`, `<h1>`, `<h2>` y `<h3>`). Puede [agregar más formatos de párrafo](configure-rich-text-editor-plug-ins.md#paraformats) o ampliar la lista. |
| revisión ortográfica | `checktext` | [corrector ortográfico con reconocimiento de idioma](configure-rich-text-editor-plug-ins.md#adddict). |
| estilos | `styles` | Compatibilidad con el estilo mediante una clase CSS. [Agregue nuevos estilos de texto](configure-rich-text-editor-plug-ins.md#textstyles) si desea agregar (o ampliar) su propio intervalo de estilos para usarlos con texto. |
| subíndice | `subscript`, `superscript` | Extensiones a los formatos básicos, añadiendo subíndice y superscript. |
| tabla | `table`, `removetable`, `insertrow`, `removerow`, `insertcolumn`, `removecolumn`, `cellprops`, `mergecells`, `splitcell`, `selectrow`, `selectcolumns` | Vea [configurar estilos de tabla](configure-rich-text-editor-plug-ins.md#tablestyles) para agregar sus propios estilos para tablas completas o celdas individuales. |
| deshacer | `undo`, `redo` | Tamaño del historial de [deshacer y rehacer](configure-rich-text-editor-plug-ins.md#undohistory) operaciones. |

>[!NOTE]
>
>El complemento de pantalla completa no es compatible con el modo de diálogo. Use la configuración `dialogFullScreen` para configurar la barra de herramientas en el modo de pantalla completa.

## Comprender las rutas y ubicaciones de configuración {#understand-the-configuration-paths-and-locations}

El [modo de edición RTE y la interfaz](#editingmodes) que proporciona a sus autores deciden la ubicación de los detalles de configuración cuando [activa los complementos RTE](configure-rich-text-editor-plug-ins.md#activateplugin). Las ubicaciones son:

* Modo en línea: `cq:editConfig/cq:inplaceEditing`.
* Modo de pantalla completa: `cq:editConfig/cq:inplaceEditing`.
* Modo de diálogo: `cq:dialog`.
* Modo de diálogo de pantalla completa: `cq:dialog`.

>[!NOTE]
>
>No asigne un nombre al nodo bajo `cq:inplaceEditing` como `config`. En el nodo `cq:inplaceEditing`, defina las siguientes propiedades:
>
>* **Nombre**: `configPath`
>* **Tipo**: `String`
>* **Valor**: ruta del nodo que contiene la configuración real
>
>No asigne un nombre al nodo de configuración RTE como `config`. De lo contrario, las configuraciones de RTE sólo surtirán efecto para los administradores y no para los usuarios del grupo `content-author`.

Configure las siguientes propiedades que se aplican en el modo de edición del cuadro de diálogo:

* `useFixedInlineToolbar`: puede hacer que la barra de herramientas RTE sea fija en lugar de flotante. Establezca esta propiedad booleana definida en el nodo RTE con sling:resourceType= `cq/gui/components/authoring/dialog/richtext` en `True`. Cuando esta propiedad se establece en `True`, la edición de texto enriquecido se inicia en el evento `foundation-contentloaded`. Para evitarlo, establezca la propiedad `customStart` en `True` y almacene en déclencheur el evento `rte-start` para iniciar la edición de RTE. Cuando esta propiedad es `true`, RTE no comienza al hacer clic y este es el comportamiento predeterminado.

* `customStart`: establezca esta propiedad booleana definida en el nodo RTE en `True`, para controlar cuándo iniciar RTE activando el evento `rte-start`.

* `rte-start`: Almacene en Déclencheur este evento el `contenteditable-div` de RTE, cuando se inicie la edición de RTE. Solo funciona si `customStart` se ha establecido en `true`.

Cuando se use RTE en el cuadro de diálogo táctil, establezca la propiedad `useFixedInlineToolbar` en `true` para evitar problemas.

## Habilitar las funcionalidades de RTE activando complementos {#enable-rte-functionalities-by-activating-plug-ins}

Las funcionalidades de RTE están disponibles a través de una serie de complementos, cada uno con la propiedad features. Puede configurar la propiedad features para habilitar o deshabilitar las distintas funciones de cada complemento.

Para obtener configuraciones detalladas de los complementos RTE, consulte [cómo activar y configurar los complementos RTE](configure-rich-text-editor-plug-ins.md).

<!-- TBD ENGREVIEW: To confirm if the sample works in CS or not?
**Sample**: Download [this sample configuration](/help/sites-administering/assets/rte-sample-all-features-enabled-10.zip) that illustrates how to configure RTE. In this package all the features are enabled. -->

El [componente de texto de componentes principales](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/text.html#the-text-component-and-the-rich-text-editor) permite a los editores de plantillas configurar muchos complementos RTE usando la interfaz de usuario como directivas de contenido, lo que elimina la necesidad de configuración técnica. Las políticas de contenido pueden funcionar con configuraciones de IU RTE como se describe en este documento. Para obtener más información, consulte [crear plantillas de página](/help/sites-cloud/authoring/page-editor/templates.md) y la [documentación para desarrolladores de componentes principales](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/developing.html).

>Para fines de referencia, los componentes de texto predeterminados (entregados como parte de una instalación estándar) se encuentran en:
>
>* `/libs/wcm/foundation/components/text`
>* `/libs/foundation/components/text`
>
>Para crear su propio componente de texto, copie el componente anterior en lugar de editar estos componentes.

## Configuración de la barra de herramientas RTE {#dialogfullscreen}

[!DNL Experience Manager] le permite configurar la interfaz del Editor de texto enriquecido de forma diferente para los distintos modos de edición. A continuación se proporcionan los ajustes predeterminados. Puede sustituir estos valores predeterminados según sus necesidades. Puede personalizar únicamente las características de la barra de herramientas que desea proporcionar a los autores. No es necesario especificar todas las configuraciones de la barra de herramientas.

Para configurar la barra de herramientas de `dialogFullScreen`, use la siguiente configuración de ejemplo.

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

Por ejemplo, si la opción es en sí misma una característica (por ejemplo, `Bold`), se especifica como `PluginName#FeatureName` (por ejemplo, `links#modifylink`).

Si la opción es una ventana emergente (que contiene algunas características de un complemento), se especifica como `#PluginName` (por ejemplo, `#format`).

Los separadores (`|`) entre un grupo de opciones se pueden especificar con `-`.

El nodo emergente bajo el modo en línea o de pantalla completa contiene una lista de las ventanas emergentes que se están utilizando. Cada nodo secundario bajo el nodo `popovers` recibe el nombre del complemento (por ejemplo, format). Tiene una propiedad &quot;items&quot; que contiene una lista de funciones del complemento (por ejemplo, format#bold).

## Configuración de la interfaz de usuario de RTE y políticas de contenido {#rtecontentpolicies}

Los administradores pueden controlar las opciones de RTE mediante políticas de contenido, por ejemplo, en lugar de realizar la configuración como se ha descrito anteriormente. Las directivas de contenido definen las propiedades de diseño de un componente cuando se utiliza como parte de una [plantilla editable](/help/sites-cloud/authoring/page-editor/templates.md). Por ejemplo, si un componente de texto que utiliza RTE se utiliza con una plantilla editable, la política de contenido puede definir que la opción de negrita esté disponible y que haya algunas opciones de formato de párrafo disponibles. Las políticas de contenido se pueden reutilizar y aplicar en varias plantillas.

Las opciones disponibles en RTE fluyen hacia abajo desde las configuraciones de interfaz de usuario hasta las políticas de contenido.

* Las opciones de configuración de la interfaz de usuario definen qué opciones están disponibles para las directivas de contenido.
* Si la configuración de interfaz de usuario del RTE se ha eliminado o no habilita un elemento, la directiva de contenido no puede configurarlo.
* Un autor solo tiene acceso a las funciones que están disponibles en las configuraciones de interfaz de usuario y en las directivas de contenido.

Por ejemplo, puede ver la [documentación del componente principal Texto](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/text.html#the-text-component-and-the-rich-text-editor).

## Personalizar la asignación entre los iconos y comandos de la barra de herramientas {#iconstoolbar}

Puede personalizar la asignación entre los iconos de Coral que se muestran en la barra de herramientas RTE y los comandos disponibles. No se puede usar ningún otro icono aparte de los iconos de Coral.

1. Cree un nodo denominado `icons` en `uiSettings/cui`.

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

* Las capacidades de RTE solo se admiten en los cuadros de diálogo de componentes [!DNL Experience Manager]. RTE no es compatible con asistentes ni formularios base.

* [!DNL Experience Manager] no funciona en dispositivos híbridos. <!-- TBD: Check. This is not mentioned in Known Issue /help/release-notes/known-issues.md-->

* No asigne un nombre al nodo de configuración de RTE `config`. De lo contrario, la configuración de RTE sólo surte efecto para los administradores y no para los usuarios del grupo `content-author`.

* RTE no admite la incrustación de contenido en un marco dentro de la línea o en un iframe.

## Prácticas recomendadas y sugerencias {#best-practices-and-tips}

* Para un cuadro de diálogo flotante, habilite solo los complementos sin cuadro de diálogo emergente. Los complementos sin ventanas emergentes son de menor tamaño y son los más adecuados para un cuadro de diálogo flotante.
* Habilite los complementos con elementos emergentes de mayor tamaño, como el complemento `Paste`, solo en el modo de diálogo de pantalla completa o en el modo de pantalla completa. Los complementos con ventanas emergentes grandes necesitan más espacio en la pantalla para proporcionar una buena experiencia de creación.
* Si utiliza complementos personalizados para CoralUI3 RTE, utilice la biblioteca `rte.coralui3`.

>[!MORELIKETHIS]
>
>* [Configurar complementos RTE](configure-rich-text-editor-plug-ins.md)
>* [Usar editor de texto enriquecido para la creación](/help/sites-cloud/authoring/page-editor/rich-text-editor.md)
>* [Configurar RTE para sitios accesibles](rte-accessible-content.md)
