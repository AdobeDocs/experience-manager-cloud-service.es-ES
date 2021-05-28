---
title: Guía de referencia de componentes
description: Una guía de referencia para desarrolladores sobre los detalles de los componentes y su estructura
exl-id: 45e5265b-39d6-4a5c-be1a-e66bb7ea387d
source-git-commit: f5f2c7c4dfacc113994c380e8caa37508030ee92
workflow-type: tm+mt
source-wordcount: '3657'
ht-degree: 1%

---

# Guía de referencia de componentes {#components-reference-guide}

Los componentes son la base de la creación de una experiencia en AEM. Los [Componentes principales](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=es) y el [AEM tipo de archivo del proyecto](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html) facilitan la introducción de un conjunto de herramientas de componentes sólidos y listos para usar. El [Tutorial de WKND](/help/implementing/developing/introduction/develop-wknd-tutorial.md) explica al desarrollador cómo utilizar estas herramientas y cómo crear componentes personalizados para crear un nuevo sitio de AEM.

>[!TIP]
>
>Antes de hacer referencia a este documento, asegúrese de haber completado el [Tutorial WKND](/help/implementing/developing/introduction/develop-wknd-tutorial.md) y, por lo tanto, estar familiarizado con los [Componentes principales](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html) y el [Tipo de archivo del proyecto de AEM.](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html)

Dado que el tutorial de WKND cubre la mayoría de los casos de uso, este documento solo está diseñado como un complemento de esos recursos. Proporciona información técnica detallada sobre cómo se estructuran y configuran los componentes en AEM y no está pensado como guía de introducción.

## Información general {#overview}

Esta sección trata los conceptos y problemas clave como una introducción a los detalles necesarios para desarrollar sus propios componentes.

### Planificación {#planning}

Antes de empezar a configurar o codificar realmente su componente, debe preguntar:

* ¿Qué necesita exactamente el nuevo componente para hacer?
* ¿Necesita crear el componente desde cero o puede heredar los conceptos básicos de un componente existente?
* ¿Necesitará lógica el componente para seleccionar o manipular el contenido?
   * La lógica debe mantenerse separada de la capa de la interfaz de usuario. HTL está diseñado para ayudar a garantizar que esto suceda.
* ¿Necesitará su componente el formato CSS?
   * El formato CSS debe mantenerse separado de las definiciones de componentes. Defina convenciones para asignar nombres a los elementos HTML de modo que pueda modificarlos a través de archivos CSS externos.
* ¿Qué implicaciones de seguridad puede presentar su nuevo componente?

### Reutilización de componentes existentes {#reusing-components}

Antes de invertir tiempo en la creación de un componente completamente nuevo, considere la posibilidad de personalizar o ampliar los componentes existentes. [Los ](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html) componentes principales ofrecen un conjunto de componentes flexibles, sólidos y bien probados listos para la producción.

#### Ampliación de componentes principales {#extending-core-components}

Los componentes principales también ofrecen [patrones de personalización claros](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/customizing.html) que puede utilizar para adaptarlos a las necesidades de su propio proyecto.

#### Superposición de componentes {#overlying-components}

Los componentes también se pueden redefinir con una [superposición](/help/implementing/developing/introduction/overlays.md) basada en la lógica de ruta de búsqueda. Sin embargo, en este caso, la [fusión de recursos de Sling](/help/implementing/developing/introduction/sling-resource-merger.md) no se activará y `/apps` debe definir la superposición completa.

#### Ampliación de los cuadros de diálogo de componentes {#extending-component-dialogs}

También es posible anular un cuadro de diálogo de componente utilizando la fusión de recursos de Sling y definiendo la propiedad `sling:resourceSuperType`.

Esto significa que solo necesita redefinir las diferencias necesarias, en lugar de redefinir todo el cuadro de diálogo.

### Lógica de contenido y marcado de renderización {#content-logic-and-rendering-markup}

El componente se procesará con [HTML.](https://www.w3schools.com/htmL/html_intro.asp) El componente debe definir el HTML necesario para tomar el contenido requerido y luego procesarlo según sea necesario, tanto en el entorno de autor como de publicación.

Se recomienda mantener el código responsable del marcado y el procesamiento separado del código que controla la lógica utilizada para seleccionar el contenido del componente.

Esta filosofía es compatible con [HTL](https://experienceleague.adobe.com/docs/experience-manager-htl/using/overview.html?lang=es), un lenguaje de plantilla limitado a propósito para garantizar que se utilice un lenguaje de programación real para definir la lógica empresarial subyacente. Este mecanismo resalta el código que se llama para una vista determinada y, si es necesario, permite una lógica específica para diferentes vistas del mismo componente.

Esta lógica (opcional) se puede implementar de diferentes maneras y se invoca desde HTL con comandos específicos:

* Al utilizar Java - [La HTL Java Use-API](https://helpx.adobe.com/experience-manager/htl/using/use-api-java.html) permite que un archivo HTL acceda a los métodos de ayuda en una clase Java personalizada. Esto le permite utilizar código Java para implementar la lógica de selección y configuración del contenido del componente.
* Uso de JavaScript: [La API de uso de JavaScript de HTL](https://experienceleague.adobe.com/docs/experience-manager-htl/using/htl/use-api-javascript.html) permite que un archivo HTL acceda al código de ayuda escrito en JavaScript. Esto le permite utilizar código JavaScript para implementar la lógica de selección y configuración del contenido del componente.
* Uso de bibliotecas del lado del cliente : los sitios web modernos dependen en gran medida del procesamiento del lado del cliente impulsado por código CSS y JavaScript complejo. Consulte el documento [Uso de bibliotecas del lado del cliente en AEM como Cloud Service](/help/implementing/developing/introduction/clientlibs.md) para obtener más información.

## Estructura de componentes {#structure}

La estructura de un componente AEM es potente y flexible. Las principales partes son:

* [Tipo de medio](#resource-type)
* [Definición de componentes](#component-definition)
* [Propiedades y nodos secundarios de un componente](#properties-and-child-nodes-of-a-component)
* [Cuadros de diálogo](#dialogs)
* [Cuadros de diálogo de diseño](#design-dialogs)

### Tipo de medio {#resource-type}

Un elemento clave de la estructura es el tipo de recurso.

* La estructura de contenido declara intenciones.
* El tipo de recurso los implementa.

Esta es una abstracción que ayuda a garantizar que, incluso cuando la apariencia cambie con el tiempo, la intención se mantenga en el tiempo.

### Definición de componente {#component-definition}

La definición de un componente se puede desglosar de la siguiente manera:

* AEM componentes se basan en [Sling.](https://sling.apache.org/documentation.html)
* AEM componentes se encuentran en `/libs/core/wcm/components`.
* Los componentes específicos del proyecto/sitio se encuentran en `/apps/<myApp>/components`.
* AEM componentes estándar se definen como `cq:Component` y tienen los elementos clave:
   * propiedades de jcr - Una lista de propiedades de jcr. Son variables y algunas pueden ser opcionales, aunque la estructura básica de un nodo de componente, sus propiedades y subnodos se definen mediante la definición `cq:Component`.
   * Recursos : definen los elementos estáticos utilizados por el componente.
   * Secuencias de comandos : se utilizan para implementar el comportamiento de la instancia resultante del componente.

#### Propiedades vitales {#vital-properties}

* **Nodo raíz**:
   * `<mycomponent> (cq:Component)` - Nodo de jerarquía del componente.
* **Propiedades** vitales:
   * `jcr:title` - Título del componente; por ejemplo, se utiliza como etiqueta cuando el componente aparece enumerado en el navegador de  [componentes ](/help/sites-cloud/authoring/fundamentals/environment-tools.md#components-browser) y en la consola  [Componentes](/help/sites-cloud/authoring/features/components-console.md)
   * `jcr:description` - Descripción del componente; se utiliza como guía de pase de ratón en la consola Componentes y explorador de componentes
   * Consulte la sección [Icono de componente](#component-icon) para obtener más información
* **Nodos** secundarios vitales:
   * `cq:editConfig (cq:EditConfig)` - Define las propiedades de edición del componente y permite que el componente aparezca en el navegador de componentes
      * Si el componente tiene un cuadro de diálogo, aparecerá automáticamente en el navegador de componentes o en la barra de tareas, aunque cq:editConfig no exista.
   * `cq:childEditConfig (cq:EditConfig)` - Controla los aspectos de la interfaz de usuario del autor para los componentes secundarios que no definen los suyos propios  `cq:editConfig`.
   * `cq:dialog (nt:unstructured)` - Cuadro de diálogo para este componente. Define la interfaz que permite al usuario configurar el componente o editar contenido.
   * `cq:design_dialog (nt:unstructured)` - Edición de diseño para este componente

#### Icono de componente {#component-icon}

El icono o la abreviatura del componente se definen mediante las propiedades JCR del componente cuando el desarrollador crea el componente. Estas propiedades se evalúan en el siguiente orden y se utiliza la primera propiedad válida encontrada.

1. `cq:icon` : propiedad de cadena que señala a un icono estándar en la  [biblioteca de Coral UI ](https://opensource.adobe.com/coral-spectrum/examples/#icon) para mostrarlo en el navegador de componentes
   * Utilice el valor del atributo HTML del icono Coral.
1. `abbreviation` - Propiedad de cadena para personalizar la abreviatura del nombre del componente en el navegador de componentes
   * La abreviatura debe limitarse a dos caracteres.
   * Si se proporciona una cadena vacía, la abreviatura se genera a partir de los dos primeros caracteres de la propiedad `jcr:title`.
      * Por ejemplo, &quot;Im&quot; para &quot;Image&quot;
      * El título localizado se utilizará para crear la abreviatura.
   * La abreviación solo se traduce si el componente tiene una propiedad `abbreviation_commentI18n`, que luego se utiliza como indicio de traducción.
1. `cq:icon.png` o  `cq:icon.svg`  - Icono para este componente, que se muestra en el navegador de componentes
   * 20 x 20 píxeles es el tamaño de los iconos de los componentes estándar.
      * Los iconos más grandes se reducirán de tamaño (lado del cliente).
   * El color recomendado es rgb(112, 112, 112) > #707070
   * El fondo de los iconos de componente estándar es transparente.
   * Solo se admiten archivos `.png` y `.svg`.
   * Si se importa desde el sistema de archivos a través del complemento Eclipse, los nombres de archivo deben omitirse como `_cq_icon.png` o `_cq_icon.svg`, por ejemplo.
   * `.png` tiene precedencia sobre  `.svg` si ambas están presentes.

Si no se encuentra ninguna de las propiedades anteriores (`cq:icon`, `abbreviation`, `cq:icon.png` o `cq:icon.svg`) en el componente:

* El sistema buscará las mismas propiedades en los supercomponentes que siguen a la propiedad `sling:resourceSuperType`.
* Si no se encuentra nada o una abreviatura vacía en el nivel de supercomponente, el sistema creará la abreviatura a partir de las primeras letras de la propiedad `jcr:title` del componente actual.

Para cancelar la herencia de los iconos de los supercomponentes, si se configura una propiedad vacía `abbreviation` en el componente, se volverá al comportamiento predeterminado.

La [Consola de componentes](/help/sites-cloud/authoring/features/components-console.md#component-details) muestra cómo se define el icono de un componente en particular.

#### Ejemplo de icono SVG {#svg-icon-example}

```xml
<?xml version="1.0" encoding="utf-8"?>
<!DOCTYPE svg PUBLIC "-//W3C//DTD SVG 1.1//EN" "https://www.w3.org/Graphics/SVG/1.1/DTD/svg11.dtd">
<svg version="1.1" id="Layer_1" xmlns="https://www.w3.org/2000/svg" xmlns:xlink="https://www.w3.org/1999/xlink" x="0px" y="0px"
     width="20px" height="20px" viewBox="0 0 20 20" enable-background="new 0 0 20 20" xml:space="preserve">
    <ellipse cx="5" cy="5" rx="3" ry="3" fill="#707070"/>
    <ellipse cx="15" cy="5" rx="4" ry="4" fill="#707070"/>
    <ellipse cx="5" cy="15" rx="5" ry="5" fill="#707070"/>
    <ellipse cx="15" cy="15" rx="4" ry="4" fill="#707070"/>
</svg>
```

### Propiedades y nodos secundarios de un componente {#properties-and-child-nodes-of-a-component}

Muchos de los nodos o propiedades necesarios para definir un componente son comunes a ambas IU, con diferencias que permanecen independientes para que el componente pueda funcionar en ambos entornos.

Un componente es un nodo de tipo `cq:Component` y tiene las siguientes propiedades y nodos secundarios:

| Nombre | Tipo | Descripción |
|---|---|---|
| `.` | `cq:Component` | Representa el componente actual. Un componente es de tipo nodo `cq:Component`. |
| `componentGroup` | `String` | Representa el grupo en el que se puede seleccionar el componente en el explorador de componentes [.](/help/sites-cloud/authoring/fundamentals/environment-tools.md#components-browser) Un valor que comienza por  `.` se utiliza para los componentes que no están disponibles para su selección en la interfaz de usuario, como los componentes base de los que heredan otros componentes. |
| `cq:isContainer` | `Boolean` | Esto indica si el componente es un componente contenedor y, por lo tanto, puede contener otros componentes, como un sistema de párrafos. |
| `cq:dialog` | `nt:unstructured` | Esta es la definición del cuadro de diálogo de edición para el componente. |
| `cq:design_dialog` | `nt:unstructured` | Esta es la definición del cuadro de diálogo de diseño para el componente. |
| `cq:editConfig` | `cq:EditConfig` | Esto define la [configuración de edición del componente.](#edit-behavior) |
| `cq:htmlTag` | `nt:unstructured` | Esto devuelve atributos de etiqueta adicionales que se agregan a la etiqueta HTML que los rodea. Habilita la adición de atributos a los divs generados automáticamente. |
| `cq:noDecoration` | `Boolean` | Si es true, el componente no se procesa con clases div y css generadas automáticamente. |
| `cq:template` | `nt:unstructured` | Si se encuentra, este nodo se utilizará como plantilla de contenido cuando el componente se añada desde el explorador de componentes. |
| `jcr:created` | `Date` | Esta es la fecha de creación del componente. |
| `jcr:description` | `String` | Esta es la descripción del componente. |
| `jcr:title` | `String` | Este es el título del componente. |
| `sling:resourceSuperType` | `String` | Cuando se configura, el componente hereda de este componente. |
| `component.html` | `nt:file` | Este es el archivo de script HTL del componente. |
| `cq:icon` | `String` | Este valor apunta al icono [del componente](#component-icon) y aparece en el explorador de componentes. |

Si miramos el componente **Texto**, podemos ver varios de estos elementos:

![Estructura del componente de texto](assets/components-text.png)

Entre las propiedades de particular interés se incluyen:

* `jcr:title` : Este es el título del componente utilizado para identificar el componente dentro del explorador de componentes.
* `jcr:description` - Esta es la descripción del componente.
* `sling:resourceSuperType` : indica la ruta de herencia al ampliar un componente (anulando una definición).

Los nodos secundarios de interés particular incluyen:

* `cq:editConfig` : controla los aspectos visuales del componente al editar.
* `cq:dialog` - Define el cuadro de diálogo para editar el contenido de este componente.
* `cq:design_dialog` : especifica las opciones de edición de diseño para este componente.

### Cuadros de diálogo {#dialogs}

Los cuadros de diálogo son un elemento clave del componente, ya que proporcionan una interfaz para que los autores configuren el componente en una página de contenido y proporcionen entradas para dicho componente. Consulte la [documentación de creación](/help/sites-cloud/authoring/fundamentals/editing-content.md) para obtener más información sobre cómo interactúan los autores de contenido con los componentes.

Según la complejidad del componente, el cuadro de diálogo puede necesitar una o más fichas.

Cuadros de diálogo para AEM componentes:

* Son nodos `cq:dialog` de tipo `nt:unstructured`.
* Se encuentran debajo de sus nodos `cq:Component` y junto a sus definiciones de componentes.
* Defina el cuadro de diálogo para editar el contenido de este componente.
* Se definen mediante los componentes de la interfaz de usuario de Granite.
* Se procesan en el lado del servidor (como componentes de Sling), según su estructura de contenido y la propiedad `sling:resourceType` .
* Contiene una estructura de nodo que describe los campos del cuadro de diálogo
   * Estos nodos son `nt:unstructured` con la propiedad `sling:resourceType` requerida.

![Definición de cuadro de diálogo del componente Título](assets/components-title-dialog.png)

Dentro del cuadro de diálogo, se definen los campos individuales:

![Campos de la definición de cuadro de diálogo del componente Título](assets/components-title-dialog-items.png)

### Diálogo de diseño {#design-dialogs}

Los cuadros de diálogo de diseño son similares a los cuadros de diálogo utilizados para editar y configurar contenido, pero proporcionan la interfaz para que los autores de plantillas proconfiguren y proporcionen detalles de diseño para ese componente en una plantilla de página. Los autores de contenido utilizan las plantillas de página para crear páginas de contenido. Consulte la [documentación de plantilla](/help/sites-cloud/authoring/features/templates.md) para obtener más información sobre cómo se crean las plantillas.

[Los cuadros de diálogo Diseño se utilizan al editar una plantilla](/help/sites-cloud/authoring/features/templates.md) de página, aunque no son necesarios para todos los componentes. Por ejemplo, los **Título** y **Componentes de imagen** tienen cuadros de diálogo de diseño, mientras que el **Componente de uso compartido de medios sociales** no lo tiene.

### Interfaz de usuario de Coral y Granite {#coral-and-granite}

La IU de Coral y la interfaz de usuario de Granite definen el aspecto de AEM.

* [La ](https://opensource.adobe.com/coral-spectrum/documentation/) interfaz de usuario de Coral proporciona una interfaz de usuario coherente en todas las soluciones de la nube.
* [La ](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/index.html) interfaz de usuario de Granite proporciona un marcado de Coral UI dentro de los componentes de Sling para crear consolas de IU y cuadros de diálogo.

La interfaz de usuario de Granite proporciona una amplia gama de widgets básicos necesarios para crear el cuadro de diálogo en el entorno de creación. Si es necesario, puede ampliar esta selección y crear su propio widget.

Para obtener más información, consulte los siguientes recursos:

* [Estructura de la interfaz de usuario de AEM](/help/implementing/developing/introduction/ui-structure.md)

### Personalización de campos de cuadro de diálogo {#customizing-dialog-fields}

<!--
Content not found

>[!TIP]
>
>See the [AEM Gems session](https://docs.adobe.com/content/ddc/en/gems/customizing-dialog-fields-in-touch-ui.html) on customizing dialog fields.
-->

Para crear un nuevo widget para utilizarlo en un cuadro de diálogo de componentes, es necesario crear un nuevo componente de campo de Granite UI .

Si considera el cuadro de diálogo como un contenedor simple para un elemento de formulario, también puede ver el contenido principal del contenido del cuadro de diálogo como campos de formulario. La creación de un nuevo campo de formulario requiere la creación de un tipo de recurso; esto equivale a crear un componente nuevo. Para ayudarle en esa tarea, la interfaz de usuario de Granite ofrece un componente de campo genérico del que heredar (mediante `sling:resourceSuperType`):

`/libs/granite/ui/components/coral/foundation/form/field`

Más específicamente, la interfaz de usuario de Granite proporciona una serie de componentes de campo que se pueden usar en cuadros de diálogo o, de forma más general, en [formularios.](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/components/foundation/form/index.html)

Una vez creado el tipo de recurso, puede crear una instancia del campo añadiendo un nuevo nodo en el cuadro de diálogo. La propiedad `sling:resourceType` hace referencia al tipo de recurso que acaba de introducir.

#### Acceso a los campos de cuadro de diálogo {#access-to-dialog-fields}

También puede utilizar condiciones de procesamiento (`rendercondition`) para controlar quién tiene acceso a pestañas/campos específicos en el cuadro de diálogo; por ejemplo:

```text
+ mybutton
  - sling:resourceType = granite/ui/components/coral/foundation/button
  + rendercondition
    - sling:resourceType = myapp/components/renderconditions/group
    - groups = ["administrators"]
```

## Uso de componentes {#using-components}

Una vez que haya creado un componente, debe activarlo para utilizarlo. Su uso muestra cómo la estructura del componente se relaciona con la estructura del contenido resultante en el repositorio.

### Adición del componente a la plantilla {#adding-your-component-to-the-template}

Una vez definido un componente, debe estar disponible para su uso. Para que un componente esté disponible para su uso en una plantilla, debe habilitar el componente en la política del contenedor de diseño de la plantilla.

Consulte la [documentación de plantilla](/help/sites-cloud/authoring/features/templates.md) para obtener más información sobre cómo se crean las plantillas.

### Componentes y el contenido que crean {#components-and-the-content-they-create}

Si creamos y configuramos una instancia del componente **Title** en la página: `/content/wknd/language-masters/en/adventures/extreme-ironing.html`

![Cuadro de diálogo de edición de títulos](assets/components-title-dialog.png)

A continuación, podemos ver la estructura del contenido creado dentro del repositorio:

![Estructura del nodo del componente Título](assets/components-title-content-nodes.png)

En particular, si observa el texto real de un **Componente de título**:

* El contenido contiene una propiedad `jcr:title` que contiene el texto real del título que escribió el autor.
* También contiene una referencia `sling:resourceType` a la definición del componente.

Las propiedades definidas dependen de las definiciones individuales. Aunque pueden ser más complejos que arriba, siguen los mismos principios básicos.

## Jerarquía y herencia de componentes {#component-hierarchy-and-inheritance}

Los componentes dentro de AEM están sujetos a la **Jerarquía de tipo de recurso**. Se utiliza para ampliar componentes con la propiedad `sling:resourceSuperType`. Esto permite que el componente herede de otro componente.

Consulte la sección [Reutilización de componentes](#reusing-components) para obtener más información.

## Editar comportamiento {#edit-behavior}

En esta sección se explica cómo configurar el comportamiento de edición de un componente. Esto incluye atributos como acciones disponibles para el componente, características del editor in.place y oyentes relacionados con eventos en el componente.

El comportamiento de edición de un componente se configura añadiendo un nodo `cq:editConfig` de tipo `cq:EditConfig` debajo del nodo del componente (de tipo `cq:Component`) y añadiendo propiedades específicas y nodos secundarios. Están disponibles las siguientes propiedades y nodos secundarios:

* `cq:editConfig` propiedades de nodo
* [`cq:editConfig` nodos](#configuring-with-cq-editconfig-child-nodes) secundarios:
   * `cq:dropTargets` (tipo de nodo  `nt:unstructured`): define una lista de destinos de colocación que pueden aceptar una colocación desde un recurso del buscador de contenido (se permite un solo destino de colocación)
   * `cq:inplaceEditing` (tipo de nodo  `cq:InplaceEditingConfig`): define una configuración de edición in situ para el componente
   * `cq:listeners` (tipo de nodo  `cq:EditListenersConfig`): define lo que sucede antes o después de que se produzca una acción en el componente

Hay muchas configuraciones existentes en AEM. Puede buscar fácilmente propiedades específicas o nodos secundarios utilizando la herramienta Consulta en **CRXDE Lite**.

### Marcadores de posición de componente {#component-placeholders}

Los componentes siempre deben representar algún HTML que sea visible para el autor, incluso cuando el componente no tenga contenido. De lo contrario, podría desaparecer visualmente de la interfaz del editor, haciendo que esté técnicamente presente pero invisible en la página y en el editor. En tal caso, los autores no podrán seleccionar ni interactuar con el componente vacío.

Por este motivo, los componentes deben representar un marcador de posición siempre que no muestren ningún resultado visible cuando la página se procese en el editor de páginas (cuando el modo WCM sea `edit` o `preview`).
El marcado HTML típico de un marcador de posición es el siguiente:

```HTML
<div class="cq-placeholder" data-emptytext="Component Name"></div>
```

El script HTL típico que procesa el marcador de posición HTML anterior es el siguiente:

```HTML
<div class="cq-placeholder" data-emptytext="${component.properties.jcr:title}"
     data-sly-test="${(wcmmode.edit || wcmmode.preview) && isEmpty}"></div>
```

En el ejemplo anterior, `isEmpty` es una variable que solo es verdadera cuando el componente no tiene contenido y es invisible para el autor.

Para evitar la repetición, Adobe recomienda que los implementadores de componentes utilicen una plantilla HTL para estos marcadores de posición, [como la proporcionada por los componentes principales.](https://github.com/adobe/aem-core-wcm-components/blob/master/content/src/content/jcr_root/apps/core/wcm/components/commons/v1/templates.html)

El uso de la plantilla en el vínculo anterior se realiza con la siguiente línea de HTL:

```HTML
<sly data-sly-use.template="core/wcm/components/commons/v1/templates.html"
     data-sly-call="${template.placeholder @ isEmpty=!model.text}"></sly>
```

En el ejemplo anterior, `model.text` es la variable que solo tiene el valor &quot;True&quot; cuando el contenido tiene contenido y es visible.

Se puede ver un ejemplo de uso de esta plantilla en los componentes principales, [como en el componente Título.](https://github.com/adobe/aem-core-wcm-components/blob/master/content/src/content/jcr_root/apps/core/wcm/components/title/v2/title/title.html#L27)

### Configuración con nodos secundarios cq:EditConfig {#configuring-with-cq-editconfig-child-nodes}

#### Colocación de recursos en un cuadro de diálogo - cq:dropTargets {#cq-droptargets}

El nodo `cq:dropTargets` (tipo de nodo `nt:unstructured`) define el objetivo de colocación que puede aceptar una colocación de un recurso arrastrado desde el buscador de contenido. Es un nodo de tipo `cq:DropTargetConfig`.

El nodo secundario de tipo `cq:DropTargetConfig` define un destino de colocación en el componente.

### Edición in situ: cq:inplaceEditing {#cq-inplaceediting}

Un editor in situ permite al usuario editar contenido directamente en el flujo de contenido, sin necesidad de abrir un cuadro de diálogo. Por ejemplo, los componentes estándar **Text** y **Title** tienen un editor de entrada.

Un editor in situ no es necesario ni significativo para cada tipo de componente.

El nodo `cq:inplaceEditing` (tipo de nodo `cq:InplaceEditingConfig`) define una configuración de edición in situ para el componente. Puede tener las siguientes propiedades:

| Nombre de propiedad | Tipo de propiedad | Valor de propiedad |
|---|---|---|
| `active` | `Boolean` | `true` para permitir la edición in situ del componente. |
| `configPath` | `String` | Ruta de la configuración del editor, que puede especificarse mediante un nodo de configuración |
| `editorType` | `String` | Los tipos disponibles son: `plaintext` para contenido no HTML, `title` convierte los títulos gráficos en un texto sin formato antes de que comience la edición y `text` utiliza el Editor de texto enriquecido |

La siguiente configuración habilita la edición de entrada del componente y define `plaintext` como el tipo de editor:

```text
    <cq:inplaceEditing
        jcr:primaryType="cq:InplaceEditingConfig"
        active="{Boolean}true"
        editorType="plaintext"/>
```

### Gestión de eventos de campo - cq:listeners {#cq-listeners}

El método para gestionar eventos en campos de diálogo se realiza con oyentes en una [biblioteca de cliente personalizada.](/help/implementing/developing/introduction/clientlibs.md)

Para insertar lógica en el campo, debe:

* Marque el campo con una clase CSS determinada (el vínculo ).
* Defina en la biblioteca de cliente un oyente JS conectado a ese nombre de clase CSS (esto garantiza que la lógica personalizada tenga ámbitos únicamente en el campo y no afecte a otros campos del mismo tipo).

Para conseguirlo, debe conocer la biblioteca de widgets subyacente con la que desea interactuar. [Consulte la ](https://opensource.adobe.com/coral-spectrum/documentation/) documentación de la interfaz de usuario de Coral para identificar el evento al que desea reaccionar.

El nodo `cq:listeners` (tipo de nodo `cq:EditListenersConfig`) define lo que sucede antes o después de una acción en el componente. La tabla siguiente define sus posibles propiedades.

| Nombre de propiedad | Valor de propiedad |
|---|---|
| `beforedelete` | El controlador se activa antes de que se elimine el componente. |
| `beforeedit` | El controlador se activa antes de editar el componente. |
| `beforecopy` | El controlador se activa antes de que se copie el componente. |
| `beforeremove` | El controlador se activa antes de mover el componente. |
| `beforeinsert` | El controlador se activa antes de que se inserte el componente. |
| `beforechildinsert` | El controlador se activa antes de que el componente se inserte dentro de otro componente (solo contenedores). |
| `afterdelete` | El controlador se activa después de eliminar el componente. |
| `afteredit` | El controlador se activa después de editar el componente. |
| `aftercopy` | El controlador se activa después de copiar el componente. |
| `afterinsert` | El controlador se activa después de insertar el componente. |
| `aftermove` | El controlador se activa después de mover el componente. |
| `afterchildinsert` | El controlador se activa después de que el componente se inserte dentro de otro componente (solo contenedores). |

>[!NOTE]
>
>En el caso de los componentes anidados, existen ciertas restricciones en las acciones definidas como propiedades en el nodo `cq:listeners`. Para los componentes anidados, los valores de las siguientes propiedades **deben** ser `REFRESH_PAGE`:
>
>* `aftermove`
>* `aftercopy`


El controlador de eventos se puede implementar con una implementación personalizada. Por ejemplo (donde `project.customerAction` es un método estático):

`afteredit = "project.customerAction"`

El siguiente ejemplo equivale a la configuración `REFRESH_INSERTED`:

`afterinsert="function(path, definition) { this.refreshCreated(path, definition); }"`

Con la siguiente configuración, la página se actualiza después de que el componente se haya eliminado, editado, insertado o movido:

```text
    <cq:listeners
        jcr:primaryType="cq:EditListenersConfig"
        afterdelete="REFRESH_PAGE"
        afteredit="REFRESH_PAGE"
        afterinsert="REFRESH_PAGE"
        afterMove="REFRESH_PAGE"/>
```

### Validación de campos {#field-validation}

La validación de campos en la interfaz de usuario de Granite y los widgets de la interfaz de usuario de Granite se realiza mediante la API `foundation-validation`. Consulte la [`foundation-valdiation` documentación de Granite](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/components/coral/foundation/clientlibs/foundation/js/validation/index.html) para obtener más información.

### Detección de disponibilidad del cuadro de diálogo {#dialog-ready}

Si tiene un JavaScript personalizado que debe ejecutarse únicamente cuando el cuadro de diálogo esté disponible y listo, debe escuchar el evento `dialog-ready` .

Este evento se activa cada vez que se carga (o recarga) el cuadro de diálogo y está listo para utilizarse, lo que significa que siempre que haya un cambio (crear/actualizar) en el DOM del cuadro de diálogo.

`dialog-ready` se puede utilizar para conectar en código personalizado JavaScript que realiza personalizaciones en los campos dentro de un cuadro de diálogo o tareas similares.

## Comportamiento de vista previa {#preview-behavior}

La cookie [WCM Mode](https://experienceleague.adobe.com/docs/experience-manager-cloud-service-javadoc/com/day/cq/wcm/api/WCMMode.html) se establece al cambiar al modo de vista previa incluso cuando la página no se actualiza.

Para los componentes con una renderización que son sensibles al modo WCM, deben definirse para actualizarse específicamente y luego depender del valor de la cookie.

## Documentación de componentes {#documenting-components}

Como desarrollador, desea acceder fácilmente a la documentación de componentes para que pueda comprender rápidamente los siguientes aspectos del componente:

* Descripción
* Uso previsto
* Estructura y propiedades del contenido
* API y puntos de extensión expuestos
* Etc.

Por este motivo, es bastante fácil hacer cualquier desglose de documentación existente que tenga disponible dentro del propio componente.

Todo lo que debe hacer es colocar un archivo `README.md` en la estructura de componentes.

![README.md en la estructura de componentes](assets/components-documentation.png)

Este marcador se mostrará en la [Consola de componentes.](/help/sites-cloud/authoring/features/components-console.md)

![README.md visible en la consola Componentes](assets/components-documentation-console.png)

El marcado admitido es el mismo que para los [fragmentos de contenido.](/help/assets/content-fragments/content-fragments.md)
