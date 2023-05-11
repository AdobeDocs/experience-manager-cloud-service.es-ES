---
title: Configure el Editor de texto enriquecido para que cree contenido en [!DNL Adobe Experience Manager] as a Cloud Service.
description: Configure el Editor de texto enriquecido para que cree contenido en [!DNL Adobe Experience Manager] as a Cloud Service.
contentOwner: AG
exl-id: 1f0ff800-5e95-429a-97f2-221db0668170
source-git-commit: e6ab7ba91b52d3479a85870e8ffa8e8d2f1e303e
workflow-type: tm+mt
source-wordcount: '1876'
ht-degree: 0%

---

# Configuración del Editor de texto enriquecido {#configure-the-rich-text-editor}

El Editor de texto enriquecido (RTE) proporciona a los autores una amplia gama de funciones para editar contenido de texto. Se proporcionan iconos, cuadros de selección, barras de herramientas y menús para una experiencia de edición de texto WYSIWYG. Los administradores configuran RTE para habilitar, deshabilitar y ampliar las funciones disponibles en los componentes de creación. Ver cómo los autores [utilizar RTE para la creación](/help/sites-cloud/authoring/fundamentals/rich-text-editor.md) contenido web.

A continuación se enumeran los conceptos y pasos de RTE necesarios para configurarlo.

| Comprender los conceptos de RTE | Habilitar las funciones necesarias | Configuración de funcionalidades individuales |
|---|---|---|
| [Explicación de la interfaz](#understand-rte-ui) | [Comprender y establecer ubicaciones de configuración](#understand-the-configuration-paths-and-locations) | [Configuración de complementos](#enable-rte-functionalities-by-activating-plug-ins) |
| [Tipos de modos de edición](#editingmodes) | [Activación de complementos](/help/implementing/developing/extending/configure-rich-text-editor-plug-ins.md#activateplugin) | [Definir propiedades de características](#aboutplugins) |
| [Acerca de los complementos](#aboutplugins) | [Configurar las barras de herramientas RTE](#dialogfullscreen) | [Configuración de los modos de pegado](/help/implementing/developing/extending/configure-rich-text-editor-plug-ins.md#textstyles) |

## Explicación de la interfaz de usuario disponible para los autores {#understand-rte-ui}

La interfaz RTE ofrece un [diseño interactivo](/help/sites-cloud/authoring/features/responsive-layout.md) para entorno de creación. La interfaz está diseñada para utilizarse en dispositivos táctiles y de escritorio.

![Barra de herramientas del Editor de texto enriquecido](assets/rte-toolbar-full-screen-mode.png)

*Figura: Barra de herramientas del Editor de texto enriquecido con todas las opciones disponibles activadas.*

La barra de herramientas proporciona las opciones para la experiencia de creación WYSIWYG. [!DNL Experience Manager] los administradores pueden configurar las opciones disponibles en la barra de herramientas de la interfaz. De forma predeterminada, hay disponible un conjunto completo de opciones de edición en [!DNL Experience Manager]. Los desarrolladores pueden personalizar [!DNL Experience Manager] para agregar más opciones de edición.

## Varios modos de edición {#editingmodes}

Los autores pueden crear y editar contenido textual en [!DNL Experience Manager] uso de los distintos modos de componentes. Las opciones de la barra de herramientas para crear y dar formato al contenido y la experiencia del usuario de los componentes habilitados para RTE en diferentes modos de edición varían según las configuraciones de RTE.

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

### Edición en pantalla completa {#full-screen-editing}

[!DNL Experience Manager] los componentes se pueden abrir en la vista de pantalla completa que oculta el contenido de la página y ocupa la pantalla disponible. Considere la posibilidad de editar en pantalla completa una versión detallada de la edición en línea, ya que ofrece las opciones de edición más interesantes. Se puede abrir haciendo clic en ![Icono para abrir RTE en pantalla completa](assets/rte_fullscreen.png), en la barra de herramientas compacta al utilizar el modo de edición en línea.

En el modo de pantalla completa del cuadro de diálogo, junto con una barra de herramientas RTE detallada, también están disponibles las opciones y los componentes disponibles en un cuadro de diálogo. Solo es aplicable a un cuadro de diálogo que contenga RTE junto con otros componentes.

![La barra de herramientas detallada de RTE al editar en modo de pantalla completa](assets/rte-toolbar-full-screen-mode.png)

*Figura: La barra de herramientas detallada de RTE al editar en modo de pantalla completa.*

### Edición del cuadro de diálogo {#dialog-editing}

Cuando se hace doble clic en un componente, se abre un cuadro de diálogo para editar el contenido. El cuadro de diálogo se abre sobre la página existente. En algunos casos específicos, el cuadro de diálogo se abre como una ventana emergente. Por ejemplo, cuando un componente Texto forma parte de una columna en un diseño de página de varias columnas y el área disponible para el cuadro de diálogo es menor.

![Modo de edición de cuadro de diálogo](assets/dialog_editing_modetouchui.png)

*Figura: Modo de edición del cuadro de diálogo.*

## Acerca de los complementos RTE y las funciones asociadas {#aboutplugins}

La funcionalidad está disponible a través de una serie de complementos, cada uno con:

* A `features` propiedad que es,

   * Se utiliza para activar o desactivar la funcionalidad básica de ese complemento.
   * Configurado mediante un procedimiento estandarizado.

* Cuando proceda, más propiedades y opciones que requieran una configuración especializada.

Las características básicas del RTE se activan o desactivan por el valor del `features` en un nodo específico del complemento adecuado.

La tabla siguiente muestra los complementos actuales:

* ID de complemento con un vínculo a la documentación de la API. El ID se utiliza como nombre de nodo cuando [activación de un complemento](/help/implementing/developing/extending/configure-rich-text-editor-plug-ins.md#activateplugin).
* Valores permitidos para la variable `features` propiedad.
* Descripción de la funcionalidad proporcionada por el complemento.

| ID del complemento | características | Descripción |
|--- |--- |--- |
| editar | `cut`, `copy`, `paste-default`, `paste-plaintext`, `paste-wordhtml` | [Cortar, copiar y, los tres modos de pegado](/help/implementing/developing/extending/configure-rich-text-editor-plug-ins.md#textstyles). |
| findreplace | `find`, `replace` | Buscar y reemplazar. |
| formato | `bold`, `italic`, `underline` | [Formato de texto básico](configure-rich-text-editor-plug-ins.md#textstyles). |
| image | `image` | Compatibilidad con imágenes básicas (arrastre desde el contenido o el Buscador de contenido). En función del explorador, la compatibilidad con tiene comportamientos diferentes para los autores |
| keys | - | Para definir este valor, consulte [tamaño de la ficha](configure-rich-text-editor-plug-ins.md#tabsize). |
| reasons | `justifyleft`, `justifycenter`, `justifyright` | Alineación del párrafo. |
| vínculos | `modifylink`, `unlink`, `anchor` | [Hipervínculos y anclajes](configure-rich-text-editor-plug-ins.md#linkstyles). |
| listas | `ordered`, `unordered`, `indent`, `outdent` | Este complemento controla ambos [sangría y listas](configure-rich-text-editor-plug-ins.md#indentmargin); incluir listas anidadas. |
| misctools | `specialchars`, `sourceedit` | Las herramientas varias permiten a los autores entrar [caracteres especiales](configure-rich-text-editor-plug-ins.md#spchar) o editar el origen del HTML. Además, puede agregar un [rango de caracteres especiales](configure-rich-text-editor-plug-ins.md#definerangechar) si desea definir su propia lista. |
| Paraformato | `paraformat` | Los formatos de párrafo predeterminados son Párrafo, Encabezado 1, Encabezado 2 y Encabezado 3 (`<p>`, `<h1>`, `<h2>`y `<h3>`). Puede [añadir más formatos de párrafo](configure-rich-text-editor-plug-ins.md#paraformats) o ampliar la lista. |
| ortografía | `checktext` | [Corrector ortográfico según idioma](configure-rich-text-editor-plug-ins.md#adddict). |
| estilos | `styles` | Compatibilidad con estilos mediante una clase CSS. [Agregar nuevos estilos de texto](configure-rich-text-editor-plug-ins.md#textstyles) si desea añadir (o ampliar) su propio rango de estilos para utilizarlo con texto. |
| subsuperíndice | `subscript`, `superscript` | Extensiones a los formatos básicos, adición de sub-script y super-script. |
| tabla | `table`, `removetable`, `insertrow`, `removerow`, `insertcolumn`, `removecolumn`, `cellprops`, `mergecells`, `splitcell`, `selectrow`, `selectcolumns` | Consulte [configurar estilos de tabla](configure-rich-text-editor-plug-ins.md#tablestyles) para agregar sus propios estilos para tablas completas o celdas individuales. |
| deshacer | `undo`, `redo` | Tamaño del historial de [deshacer y rehacer](configure-rich-text-editor-plug-ins.md#undohistory) operaciones. |

>[!NOTE]
>
>El complemento de pantalla completa no es compatible con el modo de diálogo. Uso del `dialogFullScreen` para configurar la barra de herramientas para el modo de pantalla completa.

## Explicación de las rutas y ubicaciones de configuración {#understand-the-configuration-paths-and-locations}

La variable [modo de edición RTE e interfaz](#editingmodes) que proporcione a los autores para que decidan la ubicación de los detalles de configuración cuando [activación de los complementos RTE](configure-rich-text-editor-plug-ins.md#activateplugin). Las ubicaciones son:

* Modo en línea: `cq:editConfig/cq:inplaceEditing`.
* Modo de pantalla completa: `cq:editConfig/cq:inplaceEditing`.
* Modo de cuadro de diálogo: `cq:dialog`.
* Modo de diálogo de pantalla completa: `cq:dialog`.

>[!NOTE]
>
>No asigne un nombre al nodo de `cq:inplaceEditing` como `config`. Activado `cq:inplaceEditing` , defina las siguientes propiedades:
>
>* **Nombre**: `configPath`
>* **Tipo**: `String`
>* **Valor**: ruta del nodo que contiene la configuración real
>
>No asigne al nodo de configuración RTE el nombre `config`. De lo contrario, las configuraciones de RTE surten efecto solo para los administradores y no para los usuarios del grupo `content-author`.

Configure las siguientes propiedades que se aplican en el modo de edición de cuadro de diálogo:

* `useFixedInlineToolbar`: Puede hacer que la barra de herramientas RTE sea fija en lugar de flotante. Establezca esta propiedad booleana definida en el nodo RTE con sling:resourceType= `cq/gui/components/authoring/dialog/richtext` a `True`. Cuando esta propiedad se establece en `True`, la edición de texto enriquecido se inicia en el `foundation-contentloaded` evento. Para evitarlo, establezca la propiedad `customStart` a `True` y el déclencheur de `rte-start` para iniciar la edición de RTE. Cuando esta propiedad `true`, RTE no comienza al hacer clic en y este es el comportamiento predeterminado.

* `customStart`: Establezca esta propiedad booleana definida en el nodo RTE como `True`, para controlar cuándo iniciar RTE activando el evento `rte-start`.

* `rte-start`: Déclencheur este evento en la variable `contenteditable-div` de RTE, cuándo iniciar la edición de RTE. Solo funciona si `customStart` se ha configurado como `true`.

Cuando se utiliza RTE en el cuadro de diálogo táctil, establezca la propiedad `useFixedInlineToolbar` a `true` para evitar problemas.

## Habilitar las funcionalidades RTE activando complementos {#enable-rte-functionalities-by-activating-plug-ins}

Las funcionalidades de RTE están disponibles a través de una serie de complementos, cada uno con propiedad de características. Puede configurar la propiedad features para habilitar o deshabilitar las distintas funciones de cada complemento.

Para obtener configuraciones detalladas de los complementos RTE, consulte [cómo activar y configurar los complementos RTE](configure-rich-text-editor-plug-ins.md).

<!-- TBD ENGREVIEW: To confirm if the sample works in CS or not?
**Sample**: Download [this sample configuration](/help/sites-administering/assets/rte-sample-all-features-enabled-10.zip) that illustrates how to configure RTE. In this package all the features are enabled. -->

La variable [Componente de texto de los componentes principales](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/text.html#the-text-component-and-the-rich-text-editor) permite a los editores de plantillas configurar muchos complementos RTE utilizando la interfaz de usuario como políticas de contenido, lo que elimina la necesidad de una configuración técnica. Las políticas de contenido pueden funcionar con las configuraciones de la interfaz de usuario de RTE como se describe en este documento. Para obtener más información, consulte [crear plantillas de página](/help/sites-cloud/authoring/features/templates.md) y [Documentación para desarrolladores de componentes principales](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/developing.html).

>Para fines de referencia, los componentes de texto predeterminados (entregados como parte de una instalación estándar) se pueden encontrar en:
>
>* `/libs/wcm/foundation/components/text`
>* `/libs/foundation/components/text`
>
>Para crear su propio componente de texto, copie el componente anterior en lugar de editar estos componentes.

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

Separadores (`|`) entre un grupo de opciones se puede especificar con `-`.

El nodo emergente en modo en línea o pantalla completa contiene una lista de las ventanas emergentes que se están utilizando. Cada nodo secundario debajo de `popovers` recibe el nombre del complemento (por ejemplo, format). Tiene una propiedad &quot;items&quot; que contiene una lista de características del complemento (por ejemplo, format#bold).

## Configuración de la interfaz de usuario RTE y políticas de contenido {#rtecontentpolicies}

Los administradores pueden controlar las opciones de RTE mediante políticas de contenido, por ejemplo, en lugar de realizar la configuración como se ha descrito anteriormente. Las políticas de contenido definen las propiedades de diseño de un componente cuando se utilizan como parte de un [plantilla editable](/help/sites-cloud/authoring/features/templates.md). Por ejemplo, si se utiliza un componente de texto que utilice el editor de texto enriquecido con una plantilla editable, la política de contenido puede definir que la opción en negrita esté disponible y que haya algunas opciones de formato de párrafo disponibles. Las políticas de contenido se pueden reutilizar y se pueden aplicar en varias plantillas.

Las opciones disponibles en el flujo RTE descenden desde las configuraciones de la interfaz de usuario hasta las políticas de contenido.

* Los ajustes de configuración de la interfaz de usuario definen qué opciones están disponibles para las políticas de contenido.
* Si la configuración de la interfaz de usuario del RTE se ha eliminado o no permite un elemento, la directiva de contenido no puede configurarlo.
* Un autor solo tiene acceso a las funciones que están disponibles en las configuraciones de interfaz de usuario y en las políticas de contenido.

A modo de ejemplo, puede ver la variable [Documentación del componente principal de texto](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/text.html#the-text-component-and-the-rich-text-editor).

## Personalización de la asignación entre iconos y comandos de la barra de herramientas {#iconstoolbar}

Puede personalizar la asignación entre los iconos de Coral que se muestran en la barra de herramientas de RTE y los comandos disponibles. No puede utilizar ningún otro icono aparte de los iconos de Coral.

1. Creación de un nodo denominado `icons` under `uiSettings/cui`.

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

* Las capacidades de RTE solo son compatibles con [!DNL Experience Manager] cuadros de diálogo de componentes. RTE no es compatible con asistentes o formularios base.

* [!DNL Experience Manager] no funciona en dispositivos híbridos. <!-- TBD: Check. This is not mentioned in Known Issue /help/release-notes/known-issues.md-->

* No asigne un nombre al nodo de configuración RTE `config`. De lo contrario, la configuración de RTE surte efecto solo para los administradores y no para los usuarios del grupo `content-author`.

* RTE no admite la incrustación de contenido en un marco en línea o en un iframe.

## Prácticas recomendadas y sugerencias {#best-practices-and-tips}

* Para un cuadro de diálogo flotante, habilite solo los complementos sin un cuadro de diálogo emergente. Los complementos sin ventanas emergentes tienen un tamaño menor y son más adecuados para un diálogo flotante.
* Habilite los complementos con ventanas emergentes de mayor tamaño, como el `Paste` , solo en el modo de diálogo de pantalla completa o en modo de pantalla completa. Los complementos con ventanas emergentes de gran tamaño necesitan más espacio de pantalla para ofrecer una buena experiencia de creación.
* Si utiliza complementos personalizados para CoralUI3 RTE, utilice `rte.coralui3` biblioteca.

>[!MORELIKETHIS]
>
>* [Configuración de complementos RTE](configure-rich-text-editor-plug-ins.md)
>* [Usar el Editor de texto enriquecido para la creación](/help/sites-cloud/authoring/fundamentals/rich-text-editor.md)
>* [Configuración de RTE para sitios accesibles](rte-accessible-content.md)

