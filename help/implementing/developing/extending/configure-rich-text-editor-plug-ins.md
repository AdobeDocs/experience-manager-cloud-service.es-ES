---
title: Configure los complementos Editor de texto enriquecido en [!DNL Adobe Experience Manager].
description: Aprenda a configurar [!DNL Adobe Experience Manager] los complementos del editor de texto enriquecido.
contentOwner: AG
mini-toc-levels: 1
translation-type: tm+mt
source-git-commit: 6db201f00e8f304122ca8c037998b363ff102c1f
workflow-type: tm+mt
source-wordcount: '4301'
ht-degree: 3%

---


# Configuración de los complementos del editor de texto enriquecido {#configure-the-rich-text-editor-plug-ins}

Las funcionalidades RTE están disponibles a través de una serie de complementos, cada uno con propiedad de características. Puede configurar la propiedad features para habilitar o deshabilitar una o varias funciones RTE. Este artículo describe cómo configurar específicamente los complementos RTE.

Para obtener más información sobre las demás configuraciones de RTE, consulte [Configuración del editor](/help/implementing/developing/extending/rich-text-editor.md)de texto enriquecido.

>[!NOTE]
>
>Cuando trabaje con CRXDE Lite, se recomienda guardar los cambios de forma regular mediante la opción [!UICONTROL Guardar todo] .

## Activar un complemento y configurar la propiedad features {#activateplugin}

Para activar un complemento, siga estos pasos. Algunos pasos solo son necesarios cuando configura un complemento por primera vez, ya que los nodos correspondientes no existen.

De forma predeterminada, `format`, `link`, `list`, `justify``control` y todos sus complementos y todas sus funciones están activadas en RTE.

>[!NOTE]
>
>El `rtePlugins` nodo respectivo se denomina `<rtePlugins-node>` para evitar la duplicación en este artículo.

1. Con CRXDE Lite, busque el componente de texto para el proyecto.
1. Cree el nodo principal de `<rtePlugins-node>` si no existe, antes de configurar los complementos RTE:

   * Según el componente, los nodos principales son:

      * `config: .../text/cq:editConfig/cq:inplaceEditing/config`
      * un nodo de configuración alternativo: `.../text/cq:editConfig/cq:inplaceEditing/inplaceEditingTextConfig`
      * `text: .../text/dialog/items/tab1/items/text`
   * Son del tipo: **jcr:parentType** `cq:Widget`
   * Ambas tienen la siguiente propiedad:

      * **Nombre** `name`
      * **Tipo** `String`
      * **Valor** `./text`


1. En función de la interfaz para la que esté configurando, cree un nodo `<rtePlugins-node>`, si no existe:

   * **Nombre** `rtePlugins`
   * **Tipo** `nt:unstructured`

1. Debajo de esto, cree un nodo para cada complemento que desee activar:

   * **Tipo** `nt:unstructured`
   * **Asigne un nombre** al ID de complemento del complemento requerido

Después de activar un complemento, siga estas instrucciones para configurar la `features` propiedad.

|  | Habilitar todas las funciones | Habilite algunas funciones específicas. | Desactive todas las funciones. |
|---|---|---|---|
| Nombre | características | características | características |
| Tipo | Cadena | `String` (multi-string; definir Tipo en `String` y hacer clic `Multi` en CRXDE Lite) | Cadena |
| Value | `*` (un asterisco) | Se establece en uno o varios valores de función. | - |

## Comprender el complemento Findreplace {#findreplace}

El `findreplace` complemento no necesita ninguna configuración. Funciona de la caja.

Al utilizar la funcionalidad de reemplazo, la cadena de reemplazo que se va a reemplazar debe introducirse al mismo tiempo que la cadena de búsqueda. Sin embargo, puede seguir haciendo clic en buscar para buscar la cadena antes de reemplazarla. Si se introduce la cadena de reemplazo después de hacer clic en Buscar, la búsqueda se restablece al principio del texto.

El cuadro de diálogo Buscar y reemplazar se vuelve transparente cuando se hace clic en Buscar y se vuelve opaco cuando se hace clic en reemplazar. El comportamiento permite al autor revisar el texto que se va a reemplazar. Si los usuarios hacen clic en reemplazar todo, el cuadro de diálogo se cierra y muestra el número de reemplazos realizados.

## Configuración de los modos de pegado {#pastemodes}

Al utilizar RTE, los autores pueden pegar contenido en uno de los tres modos siguientes:

* **Modo** del explorador: Pegue texto mediante la implementación de pegado predeterminada del explorador. No es un método recomendado, ya que podría introducir marcas no deseadas.

* **Modo** de texto sin formato: Pegue el contenido del portapapeles como texto sin formato. Elimina todos los elementos de estilo y formato del contenido copiado antes de insertarlos en el [!DNL Experience Manager] componente.

* **Modo** MS Word: Pegue el texto, incluidas las tablas, con formato al copiar desde MS Word. No se admite copiar y pegar texto de otro origen, como una página web o MS Excel, y solo se conserva el formato parcial.

### Configure las opciones de pegado disponibles en la barra de herramientas RTE  {#configure-paste-options-available-on-the-rte-toolbar}

Puede proporcionar algunos, todos o ninguno de estos tres iconos a sus autores en la barra de herramientas RTE:

* **[!UICONTROL Pegar (Ctrl+V)]**: Se puede preconfigurar para que se corresponda con uno de los tres modos de pegado anteriores.

* **[!UICONTROL Pegar como texto]**: Proporciona funcionalidad de modo de texto sin formato.

* **[!UICONTROL Pegar desde Word]**: Proporciona funcionalidad de modo MS Word.

Para configurar RTE para que muestre los iconos necesarios, siga estos pasos.

1. Vaya a su componente, por ejemplo `/apps/<myProject>/components/text`.
1. Vaya al nodo `rtePlugins/edit`. Consulte [Activación de un complemento](#activateplugin) si el nodo no existe.
1. Cree la `features` propiedad en el `edit` nodo y agregue una o varias de las funciones. Guarde todos los cambios.

### Configurar el comportamiento del icono Pegar (Ctrl+V) y el acceso directo {#configure-the-behavior-of-the-paste-ctrl-v-icon-and-shortcut}

Puede preconfigurar el comportamiento del icono **[!UICONTROL Pegar (Ctrl+V)]** mediante los siguientes pasos. Esta configuración también define el comportamiento del método abreviado de teclado Ctrl+V que utilizan los autores para pegar contenido.

La configuración permite los siguientes tres tipos de casos de uso:

* Pegue texto mediante la implementación de pegado predeterminada del explorador. No es un método recomendado, ya que podría introducir marcas no deseadas. Configurado usando `browser` abajo.

* Pegue el contenido del portapapeles como texto sin formato. Elimina todos los elementos de estilo y formato del contenido copiado antes de insertarlos en el [!DNL Experience Manager] componente. Configurado usando `plaintext` abajo.

* Pegue el texto, incluidas las tablas, con formato al copiar desde MS Word. No se admite copiar y pegar texto de otro origen, como una página web o MS Excel, y solo se conserva el formato parcial. Configurado usando `wordhtml` abajo.

1. En el componente, desplácese hasta el `<rtePlugins-node>/edit` nodo. Cree los nodos si no existen. Para obtener más información, consulte [Activación de un complemento](#activateplugin).
1. En el `edit` nodo, cree una propiedad con los siguientes detalles:

   * **Nombre** `defaultPasteMode`
   * **Tipo** `String`
   * **El valor** es uno de los modos de pegado requeridos desde `browser`, `plaintext`o `wordhtml` .

### Configurar los formatos permitidos al pegar contenido {#pasteformats}

El modo de pegado como Microsoft Word (`paste-wordhtml`) se puede configurar más para permitir explícitamente algunos estilos al pegar [!DNL Experience Manager] desde otro programa, como [!DNL Microsoft Word].

Por ejemplo, si solo se deben permitir formatos y listas en negrita al pegar en [!DNL Experience Manager], puede filtrar los demás formatos. Esto se denomina filtrado de pegado configurable, que se puede realizar para ambos:

* [Texto](#pastemodes)
* [Vínculos](#linkstyles)

Para los vínculos, también puede definir los protocolos que se aceptan automáticamente.

Para configurar qué formatos se permiten al pegar texto en [!DNL Experience Manager] desde otro programa:

1. En el componente, navegue hasta el nodo `<rtePlugins-node>/edit`. Cree los nodos si el nodo no existe. Para obtener más información, consulte [Activación de un complemento](#activateplugin).
1. Cree un nodo bajo el `edit` nodo para mantener las reglas de pegado HTML:

   * **Nombre** `htmlPasteRules`
   * **Tipo** `nt:unstructured`

1. Cree un nodo en `htmlPasteRules`, para incluir detalles de los formatos básicos permitidos:

   * **Nombre** `allowBasics`
   * **Tipo** `nt:unstructured`

1. Para controlar los formatos individuales aceptados, cree una o varias de las siguientes propiedades en el `allowBasics` nodo:

   * **Nombre** `bold`
   * **Nombre** `italic`
   * **Nombre** `underline`
   * **Nombre** `anchor` (para vínculos y anclajes con nombre)
   * **Nombre** `image`

   Todas las propiedades son de **tipo** `Boolean`, por lo que en el **valor** correspondiente puede seleccionar o quitar la marca de verificación para habilitar o deshabilitar la funcionalidad.

   >[!NOTE]
   >
   >Si no se define explícitamente, se utiliza el valor predeterminado true y se acepta el formato.

1. También se pueden definir otros formatos utilizando un rango de otras propiedades o nodos, también aplicados al `htmlPasteRules` nodo:

| Propiedad | Tipo | Descripción |
|--- |--- |--- |
| `allowBlockTags` | `String` | Define la lista de las etiquetas de bloque permitidas. Algunas etiquetas de bloque posibles incluyen titulares (h1, h2, h3), párrafos (p), listas (ol, ul), tablas (tabla). |
| `fallbackBlockTag` | `String` | Define la etiqueta de bloque utilizada para cualquier bloque que tenga una etiqueta de bloque no incluida en `allowBlockTags`. Normalmente, `p` basta. |
| `table` | `nt:unstructured` | Define el comportamiento al pegar tablas. Este nodo debe tener la propiedad allow (type Boolean) para definir si se permite pegar tablas. Si allow se establece en false, debe especificar la propiedad ignoreMode (type String) para definir cómo se gestiona el contenido de la tabla pegada. Los valores válidos para ignoreMode son `remove` eliminar el contenido de la tabla y `paragraph` convertir las celdas de la tabla en párrafos. |
| `list` | `nt:unstructured` | Define el comportamiento al pegar listas. Debe tener la propiedad `allow` (tipo Boolean) para definir si se permite pegar listas. Si `allow` se establece en `false`, especifique la propiedad `ignoreMode` (tipo `String`) para definir cómo gestionar cualquier contenido de lista pegado. Los valores válidos para ignoreMode son `remove` que elimina el contenido de la lista y `paragraph` que convierte los elementos de la lista en párrafos. |

A continuación se muestra un ejemplo de una `htmlPasteRules` estructura válida:

```xml
"htmlPasteRules": {
    "allowBasics": {
        "italic": true,
        "link": true
    },
    "allowBlockTags": [
        "p", "h1", "h2", "h3"
    ],
    "list": {
        "allow": false,
        "ignoreMode": "paragraph"
    },
    "table": {
        "allow": true,
        "ignoreMode": "paragraph"
    }
}
```

1. Guarde todos los cambios.

## Configuración de estilos de texto {#textstyles}

Los autores pueden aplicar estilos para cambiar el aspecto de una parte del texto. Los estilos se basan en clases CSS predefinidas en la hoja de estilo CSS. El contenido estilizado se incluye en `span` etiquetas mediante el `class` atributo para hacer referencia a la clase CSS. Por ejemplo:

`<span class=monospaced>Monospaced Text Here</span>`

Cuando el complemento Estilos está activado por primera vez, no hay estilos predeterminados disponibles. La lista emergente está vacía. Para proporcionar a los autores estilos, haga lo siguiente:

* Habilite el selector desplegable Estilo.
* Especifique una o varias ubicaciones de las hojas de estilo.
* Especifique los estilos individuales que se pueden seleccionar en la lista emergente de estilo.

Para reconfiguraciones posteriores, por ejemplo, para agregar más estilos, siga solo las instrucciones para hacer referencia a una nueva hoja de estilo y especificar los estilos adicionales.

>[!NOTE]
>
>Los estilos también se pueden definir para [tablas o celdas](configure-rich-text-editor-plug-ins.md#tablestyles)de tabla. Estas configuraciones requieren procedimientos separados.

### Habilitar la lista del selector desplegable Estilo {#styleselectorlist}

Esto se realiza habilitando el complemento de estilos.

1. En el componente, navegue hasta el nodo `<rtePlugins-node>/styles`. Cree los nodos si no existen. Para obtener más información, consulte [Activación de un complemento](#activateplugin).
1. Cree la `features` propiedad en el `styles` nodo:

   * **Nombre** `features`
   * **Tipo** `String`
   * **Valor** `*` (asterisco)

1. Guarde todos los cambios.

>[!NOTE]
>
>Una vez activado el complemento Estilos, la lista desplegable Estilo se muestra en el cuadro de diálogo de edición. Sin embargo, la lista está vacía porque no hay estilos configurados.

### Especificar la ubicación de la hoja de estilo {#locationofstylesheet}

A continuación, especifique las ubicaciones de las hojas de estilo a las que desea hacer referencia:

1. Vaya al nodo raíz del componente de texto, por ejemplo `/apps/<myProject>/components/text`.
1. Añada la propiedad `externalStyleSheets` al nodo principal de `<rtePlugins-node>`:

   * **Nombre** `externalStyleSheets`
   * **Tipo** `String[]` (multicadena; haga clic en **Múltiples** en CRXDE)
   * **Valores** La ruta y el nombre de archivo de cada hoja de estilo que desee incluir. Utilice rutas de repositorio.

   >[!NOTE]
   >
   >Puede agregar referencias a hojas de estilo adicionales más adelante.

1. Guarde todos los cambios.

Al utilizar RTE en un cuadro de diálogo (IU clásica), puede especificar hojas de estilo optimizadas para la edición de texto enriquecido. Debido a restricciones técnicas, el contexto CSS se pierde en el editor, por lo que puede emular este contexto para mejorar la experiencia WYSIWYG.

El Editor de texto enriquecido utiliza un elemento DOM de contenedor con un ID de `CQrte` que proporciona diferentes estilos para la vista y edición:

```css
#CQ td {
// defines the style for viewing
 }
```

```css
#CQrte td {
 // defines the style for editing
 }
```

### Especifique los estilos disponibles en la lista emergente {#stylesindropdown}

1. En la definición del componente, navegue hasta el nodo `<rtePlugins-node>/styles`, tal como se ha creado en [Activación del selector](#styleselectorlist)desplegable de estilos.
1. En el nodo `styles`, cree un nodo (también llamado `styles`) para mantener la lista disponible:

   * **Nombre** `styles`
   * **Tipo** `cq:WidgetCollection`

1. Cree un nodo bajo el `styles` nodo para representar un estilo individual:

   * **Nombre**, puede especificar el nombre, pero debería ser adecuado para el estilo
   * **Tipo** `nt:unstructured`

1. Añada la propiedad `cssName` a este nodo para hacer referencia a la clase CSS:

   * **Nombre** `cssName`
   * **Tipo** `String`
   * **Valor** El nombre de la clase CSS (sin un &#39;.&#39; anterior); for example, `cssClass` instead of `.cssClass`)

1. Añadir la propiedad `text` al mismo nodo; esto define el texto mostrado en el cuadro de selección:

   * **Nombre** `text`
   * **Tipo** `String`
   * **Valor** Descripción del estilo; aparece en el cuadro de selección desplegable Estilo.

1. Guarde los cambios.

   Repita los pasos anteriores para cada estilo requerido.

### Configurar RTE para saltos de palabras óptimos en japonés {#jpwordwrap}

Los autores que utilizan [!DNL Experience Manager] para crear contenido en japonés pueden aplicar un estilo a los caracteres para evitar saltos de línea cuando no se requiera un salto de línea. Esto permite a los autores dejar que las oraciones rompan en la posición deseada. El estilo de esta funcionalidad se basa en la clase CSS predefinida en la hoja de estilo CSS.

Para crear el estilo que los autores pueden aplicar al texto en japonés, siga estos pasos:

1. Cree un nodo bajo el nodo de estilos. Consulte [Especificación de un estilo](#stylesindropdown).
   * Nombre: `jpn-word-wrap`
   * Tipo: `nt:unstructure`

1. Añada la propiedad `cssName` al nodo para hacer referencia a la clase CSS. Este nombre de clase es un nombre reservado para la función de ajuste de palabras en japonés.
   * Nombre: `cssName`
   * Tipo: `String`
   * Valor: `jpn-word-wrap` (sin precedente `.`)

1. Añada el texto de la propiedad al mismo nodo. El valor es el nombre del estilo que los autores ven al seleccionar el estilo.
   * Nombre: `text`
*Tipo: 
`String`
   * Value: `Japanese word-wrap`

1. Cree una hoja de estilo y especifique su ruta. Consulte [Especificación de la ubicación de la hoja de estilo](#locationofstylesheet). Añada el siguiente contenido en la hoja de estilo. Cambie el color de fondo como desee.

   ```css
   .text span.jpn-word-wrap {
       display:inline-block;
   }
   .is-edited span.jpn-word-wrap {
       background-color: #ffddff;
   }
   ```

   ![Hoja de estilo para que la función de ajuste de palabras en japonés esté disponible para los autores](assets/rte_jpwordwrap_stylesheet.jpg)

## Configuración de los formatos de párrafo {#paraformats}

Cualquier texto creado en RTE se coloca dentro de una etiqueta de bloque, siendo la predeterminada `<p>`. Al habilitar el `paraformat` complemento, se especifican etiquetas de bloque adicionales que se pueden asignar a los párrafos mediante una lista de selección desplegable. Los formatos de párrafo determinan el tipo de párrafo asignando la etiqueta de bloque correcta. El autor puede seleccionarlos y asignarlos mediante el selector Formato. Las etiquetas de bloque de ejemplo incluyen, entre otras, el párrafo estándar &lt;p> y los encabezados &lt;h1>, &lt;h2>, etc.

>[!CAUTION]
>
>Este complemento no es adecuado para contenido con estructura compleja, como listas o tablas.

>[!NOTE]
>
>Si una etiqueta de bloque, por ejemplo una `<hr>` etiqueta, no se puede asignar a un párrafo, no es un caso de uso válido para un `paraformat` complemento.

Cuando el complemento Formatos de párrafo está activado por primera vez, no hay disponibles formatos de párrafo predeterminados. La lista emergente está vacía. Para proporcionar a los autores formatos de párrafo, haga lo siguiente:

* Active la lista del selector emergente [!UICONTROL Formato] .
* Especifique las etiquetas de bloque que se pueden seleccionar como formatos de párrafo en el menú emergente.

Para las reconfiguraciones posteriores, digamos para agregar más formatos, siga solamente la parte relevante de las instrucciones.

### Habilitar el selector desplegable Formato {#formatselectorlist}

Para habilitar el `paraformat` complemento, siga estos pasos:

1. En el componente, navegue hasta el nodo `<rtePlugins-node>/paraformat`. Cree los nodos si no existen. Para obtener más información, consulte [Activación de un complemento](#activateplugin).
1. Cree la `features` propiedad en el `paraformat` nodo:

   * **Nombre** `features`
   * **Tipo** `String`
   * **Valor** `*` (asterisco)

>[!NOTE]
>
>Si el complemento no está configurado más, los formatos predeterminados activados son Párrafo ( `<p>`), Encabezado 1 ( `<h1>`), Encabezado 2 ( `<h2>`) y Encabezado 3 ( `<h3>`).

>[!CAUTION]
>
>Al configurar los formatos de párrafo de RTE, no elimine la etiqueta de párrafo &lt;p> como opción de formato. Si se elimina la `<p>` etiqueta, el autor del contenido no puede seleccionar la opción de formatos [!UICONTROL de] párrafo aunque haya otros formatos configurados.

### Especifique los formatos de párrafo disponibles {#paraformatsindropdown}

Los formatos de párrafo están disponibles para su selección mediante:

1. En la definición del componente, navegue hasta el nodo `<rtePlugins-node>/paraformat`, tal como se ha creado en [Activación del selector](#styleselectorlist)desplegable de formato.
1. En el `paraformat` nodo, cree un nodo para mantener la lista de formatos:

   * **Nombre** `formats`
   * **Tipo** `cq:WidgetCollection`

1. Cree un nodo bajo el `formats` nodo; contiene los detalles de un formato individual:

   * **Nombre**, puede especificar el nombre, pero debería ser adecuado para el formato (por ejemplo, mipárrafo, miencabezado1).
   * **Tipo** `nt:unstructured`

1. A este nodo, agregue la propiedad para definir la etiqueta de bloque utilizada:

   * **Nombre** `tag`
   * **Tipo** `String`
   * **Valor** La etiqueta de bloque del formato; por ejemplo: p, h1, h2, etc.

      No es necesario introducir los corchetes angulares delimitadores.

1. Al mismo nodo agregue otra propiedad para que aparezca texto descriptivo en la lista desplegable:

   * **Nombre** `description`
   * **Tipo** `String`
   * **Valor** El texto descriptivo de este formato; por ejemplo, Párrafo, Encabezado 1, Encabezado 2, etc. Este texto se muestra en la lista de selección Formato.

1. Guarde los cambios.

   Repita los pasos para cada formato requerido.

>[!CAUTION]
>
>Si define formatos personalizados, se eliminan los formatos predeterminados (`<p>`, `<h1>`, `<h2>`y `<h3>`). Vuelva a crear `<p>` el formato tal como es el formato predeterminado.

## Configurar caracteres especiales {#spchar}

En una instalación estándar [!DNL Experience Manager] , cuando el `misctools` complemento está habilitado para caracteres especiales (`specialchars`), inmediatamente se puede utilizar una selección predeterminada; por ejemplo, los símbolos de copyright y marca comercial.

Puede configurar el RTE para que su selección de caracteres esté disponible; definiendo caracteres distintos o una secuencia completa.

>[!CAUTION]
>
>Añadir los caracteres especiales anula la selección predeterminada. Si es necesario, redefina estos caracteres en la selección.

### Definir un solo carácter {#definesinglechar}

1. En el componente, navegue hasta el nodo `<rtePlugins-node>/misctools`. Cree los nodos si no existen. Para obtener más información, consulte [Activación de un complemento](#activateplugin).
1. Cree la `features` propiedad en el `misctools` nodo:

   * **Nombre** `features`
   * **Tipo** `String[]`
   * **Valor** `specialchars`

          (o `String / *` si se aplican todas las características de este complemento)

1. En `misctools` Crear un nodo para mantener las configuraciones de caracteres especiales:

   * **Nombre** `specialCharsConfig`
   * **Tipo** `nt:unstructured`

1. En `specialCharsConfig` Crear otro nodo para mantener la lista de caracteres:

   * **Nombre** `chars`
   * **Tipo** `nt:unstructured`

1. En `chars` Agregar un nodo para mantener una definición de carácter individual:

   * **Nombre** puede especificar el nombre, pero debe reflejar el carácter; por ejemplo, la mitad.
   * **Tipo** `nt:unstructured`

1. A este nodo agregue la siguiente propiedad:

   * **Nombre** `entity`
   * **Tipo** `String`
   * **Valore** la representación HTML del carácter requerido; por ejemplo, `&189;` para la fracción una mitad.

1. Guarde los cambios.

En CRXDE, una vez guardada la propiedad, se muestra el carácter representado. Vea el ejemplo de la mitad más abajo. Repita los pasos anteriores para que los autores tengan más caracteres especiales disponibles.

![En CRXDE, agregue un solo carácter para que esté disponible en la](assets/chlimage_1-106.png "barra de herramientas RTEEn CRXDE, agregue un solo carácter para que esté disponible en la barra de herramientas RTE")

### Definir un rango de caracteres {#definerangechar}

1. Utilice los pasos 1 a 3 de [Definir un solo carácter](#definesinglechar).
1. En `chars` Agregar un nodo para mantener la definición del rango de caracteres:

   * **Nombre** puede especificar el nombre, pero debe reflejar el rango de caracteres; por ejemplo, lápices.
   * **Tipo** `nt:unstructured`

1. En este nodo (cuyo nombre depende del rango de caracteres especial) agregue las dos propiedades siguientes:

   * **Nombre** `rangeStart`

      **Tipo** `Long`
      **Valor** de la representación [Unicode](https://unicode.org/) (decimal) del primer carácter del rango

   * **Nombre** `rangeEnd`

      **Tipo** `Long`
      **Valor** de la representación [Unicode](https://unicode.org/) (decimal) del último carácter del rango

1. Guarde los cambios.

   Por ejemplo, si define un intervalo de 9998 a 10000, se proporcionan los siguientes caracteres.

   ![En CRXDE, defina un rango de caracteres para que estén disponibles en RTE](assets/chlimage_1-107.png)

   *Figura: En CRXDE, defina un rango de caracteres para que estén disponibles en RTE*

   ![Los autores pueden ver los caracteres especiales disponibles en RTE en una](assets/rtepencil.png "ventana emergenteLos caracteres especiales disponibles en RTE se muestran a los autores en una ventana emergente")

## Configuración de estilos de tabla {#tablestyles}

Los estilos se suelen aplicar al texto, pero también se puede aplicar un conjunto independiente de estilos a una tabla o a unas pocas celdas de la tabla. Estos estilos están disponibles para los autores en el cuadro de selección Estilo del cuadro de diálogo Propiedades de celda o Propiedades de tabla. Los estilos están disponibles al editar una tabla dentro de un componente Texto (o derivado) y no en el componente Tabla estándar.

>[!NOTE]
>
>Puede definir estilos para tablas y celdas solo para la IU clásica.

>[!NOTE]
>
>La copia y pegado de tablas en o desde el componente RTE depende del explorador. No se admite de forma predeterminada para todos los exploradores. Puede obtener resultados variados según la estructura de tabla y el explorador. Por ejemplo, al copiar y pegar una tabla en un componente RTE en Mozilla Firefox en la IU clásica y la IU táctil, no se conserva el diseño de la tabla.

1. En el componente, navegue al nodo `<rtePlugins-node>/table`. Cree los nodos si no existen. Para obtener más información, consulte [Activación de un complemento](#activateplugin).
1. Cree la `features` propiedad en el `table` nodo:

   * **Nombre** `features`
   * **Tipo** `String`
   * **Valor** `*`

   >[!NOTE]
   >
   >Si no desea habilitar todas las funciones de tabla, puede crear la `features` propiedad como:
   >* **Tipo** `String[]`

   * **Los valores** son uno o ambos de los siguientes, según sea necesario:
      * `table` permitir la edición de propiedades de tabla; incluidos los estilos.
      * `cellprops` para permitir la edición de propiedades de celda, incluidos los estilos.


1. Defina la ubicación de las hojas de estilo CSS para hacer referencia a ellas. Consulte [Especificación de la ubicación de la hoja](#locationofstylesheet) de estilo, ya que es la misma que al definir [estilos para texto](#textstyles). La ubicación se puede definir si se han definido otros estilos.
1. En el `table` nodo, cree los siguientes nodos según sea necesario:

   * Para definir estilos para toda la tabla (disponible en Propiedades **[!UICONTROL de tabla]**):

      * **Nombre** `tableStyles`
      * **Tipo** `cq:WidgetCollection`
   * Definición de estilos para celdas individuales (disponible en Propiedades **[!UICONTROL de celda]**),

      * **Nombre** `cellStyles`
      * **Tipo** `cq:WidgetCollection`


1. Cree un nodo (debajo del nodo `tableStyles` o `cellStyles` según corresponda) para representar un estilo individual,

   * **Nombre** puede especificar el nombre, pero debe reflejar el estilo.
   * **Tipo** `nt:unstructured`

1. En este nodo, cree las propiedades:

   * Para definir el estilo CSS al que se hace referencia,

      * **Nombre** `cssName`
      * **Tipo** `String`
      * **Valor** del nombre de la clase CSS (sin un precedente `.`, por ejemplo, `cssClass` en lugar de `.cssClass`)
   * Para definir un texto descriptivo que aparecerá en el selector emergente,

      * **Nombre** `text`
      * **Tipo** `String`
      * **Valor** del texto que aparecerá en la lista de selección


1. Guarde todos los cambios.

Repita los pasos anteriores para cada estilo requerido.

### Configurar encabezados ocultos en tablas para accesibilidad {#hiddenheader}

A veces, puede crear tablas de datos sin texto visual en un encabezado de columna suponiendo que el propósito del encabezado se vea implicado en la relación visual de la columna con otras columnas. En este caso, es necesario proporcionar texto interno oculto dentro de la celda en la celda de encabezado para permitir que los lectores de pantalla y otras tecnologías de asistencia puedan ayudar a los lectores con diversas necesidades a comprender el propósito de la columna.

Para mejorar la accesibilidad en estos escenarios, RTE admite celdas de encabezado ocultas. Además, proporciona opciones de configuración relacionadas con encabezados ocultos en tablas. Esta configuración permite aplicar estilos CSS a encabezados ocultos en los modos de edición y previsualización. Para ayudar a los autores a identificar encabezados ocultos en el modo de edición, incluya los siguientes parámetros en el código:

* `hiddenHeaderEditingCSS`:: Especifica el nombre de la clase CSS que se aplica en la celda de encabezado oculto cuando se edita RTE.
* `hiddenHeaderEditingStyle`:: Especifica una cadena de estilo que se aplica en la celda de encabezado oculto cuando se edita RTE.

Si especifica la cadena CSS y la cadena de estilo en el código, la clase CSS tiene prioridad sobre la cadena de estilo y puede sobrescribir cualquier cambio de configuración que realice la cadena de estilo.

Para ayudar a los autores a aplicar CSS en encabezados ocultos en el modo de previsualización, puede incluir los siguientes parámetros en el código:

* `hiddenHeaderClassName`:: Especifica el nombre de la clase CSS que se aplica en la celda de encabezado oculto en modo de previsualización.
* `hiddenHeaderStyle`:: Especifica una cadena de estilo que se aplica en la celda de encabezado oculto en modo de previsualización.

Si especifica la cadena CSS y la cadena de estilo en el código, la clase CSS tiene prioridad sobre la cadena de estilo y puede sobrescribir cualquier cambio de configuración que realice la cadena de estilo.

## Añadir diccionarios para el corrector ortográfico {#adddict}

Cuando se activa el complemento de revisión de ortografía, RTE utiliza diccionarios para cada idioma adecuado. A continuación, se seleccionan según el idioma del sitio web tomando la propiedad language del subárbol o extrayendo el idioma de la dirección URL; por ejemplo. la `/en/` rama está marcada como Inglés, la `/de/` rama como Alemán.

>[!NOTE]
>
>El mensaje &quot;Error al revisar la ortografía&quot;. se ve si se intenta comprobar un idioma que no está instalado.

Una instalación de Experience Manager estándar incluye los diccionarios para:

* Inglés americano (en_us)
* Inglés británico (en_gb)

>[!NOTE]
>
>Los diccionarios estándar se encuentran en `/libs/cq/spellchecker/dictionaries`, junto con los archivos Léame correspondientes. No modifique los archivos.

Para agregar más diccionarios, si es necesario, siga estos pasos.

1. Vaya a la página [https://extensions.openoffice.org/](https://extensions.openoffice.org/).
1. Seleccione el idioma requerido y descargue el archivo ZIP con las definiciones de ortografía. Extraiga el contenido del archivo en su sistema de archivos.

   >[!CAUTION]
   >
   >Solo se admiten los diccionarios con el `MySpell` formato OpenOffice.org v2.0.1 o anterior. Dado que los diccionarios ahora son archivos de archivo, se recomienda que verifique el archivo después de descargarlo.

1. Busque los archivos .aff y .dic. Mantenga el nombre del archivo en minúsculas. Por ejemplo, `de_de.aff` y `de_de.dic`.
1. Cargue los archivos .aff y .dic en el repositorio en `/apps/cq/spellchecker/dictionaries`.

>[!NOTE]
>
>El corrector ortográfico RTE está disponible a petición. No se ejecuta automáticamente al escribir texto con inicio.
>Para ejecutar el corrector ortográfico, toque o haga clic en el botón Corrector ortográfico de la barra de herramientas. RTE comprueba la ortografía de las palabras y resalta las palabras mal escritas.
>Si incorpora cualquier cambio que sugiera el corrector ortográfico, el estado del texto cambia y las palabras mal escritas ya no se resaltan. Para ejecutar el corrector ortográfico, toque o haga clic de nuevo en el botón Corrector ortográfico.

## Configurar el tamaño del historial para acciones de deshacer y rehacer {#undohistory}

RTE permite a los autores deshacer o rehacer algunas últimas ediciones. De forma predeterminada, se almacenan 50 ediciones en el historial. Puede configurar este valor según sea necesario.

1. En el componente, navegue al nodo `<rtePlugins-node>/undo`. Cree estos nodos si no existen. Para obtener más información, consulte [Activación de un complemento](#activateplugin).
1. En el `undo` nodo, cree la propiedad:

   * **Nombre** `maxUndoSteps`
   * **Tipo** `Long`
   * **Valore** el número de pasos de deshacer que desea guardar en el historial. El valor predeterminado es 50. Se utiliza `0` para desactivar completamente la acción deshacer/rehacer.

1. Guarde los cambios.

## Configurar el tamaño de la ficha {#tabsize}

Cuando se presiona el carácter de tabulación dentro de cualquier texto, se inserta un número predefinido de espacios; de forma predeterminada, hay tres espacios sin saltos y un espacio.

Para definir el tamaño de la ficha:

1. En el componente, navegue hasta el nodo `<rtePlugins-node>/keys`. Cree los nodos si no existen. Para obtener más información, consulte [Activación de un complemento](#activateplugin).
1. En el `keys` nodo, cree la propiedad:

   * **Nombre** `tabSize`
   * **Tipo** `String`
   * **Valor** el número de caracteres de espacio que se utilizarán para el tabulador.

1. Guarde los cambios.

## Definir margen de sangría {#indentmargin}

Cuando la sangría está activada (opción predeterminada), puede definir el tamaño de la sangría:

>[!NOTE]
>
>Este tamaño de sangría solo se aplica a los párrafos (bloques) de texto; no afecta a la sangría de listas reales.

1. En el componente, navegue al nodo `<rtePlugins-node>/lists`. Cree estos nodos si no existen. Para obtener más información, consulte [Activación de un complemento](#activateplugin).
1. En el `lists` nodo, cree el `identSize` parámetro:

   * **Nombre**: `identSize`
   * **Tipo**: `Long`
   * **Valor**: número de píxeles necesarios para el margen de sangría.

## Configurar la altura del espacio editable {#editablespace}

Puede definir la altura del espacio editable que se muestra en el cuadro de diálogo del componente. La configuración solo se aplica cuando se utiliza RTE en un cuadro de diálogo. La configuración no cambia la altura de la ventana de diálogo.

1. En el `../items/text` nodo, en la definición de cuadro de diálogo del componente, cree una propiedad:

   * **Nombre** `height`
   * **Tipo** `Long`
   * **Valora** la altura del lienzo de edición en píxeles.

1. Guarde los cambios.

## Configuración de estilos y protocolos para vínculos {#linkstyles}

Al agregar vínculos en [!DNL Experience Manager], puede definir los estilos CSS que se utilizarán y los protocolos que se aceptarán automáticamente. Para configurar cómo se agregan vínculos [!DNL Experience Manager] desde otro programa, defina las reglas HTML.

1. Con CRXDE Lite, busque el componente de texto para el proyecto.
1. Cree un nodo en el mismo nivel que `<rtePlugins-node>`, es decir, cree el nodo en el nodo principal de `<rtePlugins-node>`:

   * **Nombre** `htmlRules`
   * **Tipo** `nt:unstructured`

   >[!NOTE]
   >
   >El `../items/text` nodo tiene la propiedad:
   >* **Nombre** `xtype`
   >* **Tipo** `String`
   >* **Valor** `richtext`

   La ubicación del `../items/text` nodo puede variar en función de la estructura del cuadro de diálogo. Dos ejemplos son `/apps/myProject>/components/text/dialog/items/text` y `/apps/<myProject>/components/text/dialog/items/panel/items/text`.

1. En `htmlRules`, cree un nodo.

   * **Nombre** `links`
   * **Tipo** `nt:unstructured`

1. En el `links` nodo, defina las propiedades según sea necesario:

   * Estilo CSS para vínculos internos:

      * **Nombre** `cssInternal`
      * **Tipo** `String`
      * **Valor** del nombre de la clase CSS (sin un &#39;.&#39; anterior); for example, `cssClass` instead of `.cssClass`)
   * Estilo CSS para vínculos externos

      * **Nombre** `cssExternal`
      * **Tipo** `String`
      * **Valor** del nombre de la clase CSS (sin un &#39;.&#39; anterior); for example, `cssClass` instead of `.cssClass`)
   * Matriz de **[!UICONTROL protocolos]** válidos, incluidos `https://`, `https://`, `file://`, `mailto:`etc.,

      * **Nombre** `protocols`
      * **Tipo** `String[]`
      * **Valores** de uno o más protocolos
   * **defaultProtocol** (propiedad de tipo **String**): Protocolo que se utilizará si el usuario no especificó uno explícitamente.

      * **Nombre** `defaultProtocol`
      * **Tipo** `String`
      * **Valores** de uno o más protocolos predeterminados
   * Definición de cómo gestionar el atributo de destinatario de un vínculo. Crear un nodo:

      * **Nombre** `targetConfig`
      * **Tipo** `nt:unstructured`

      En el nodo `targetConfig`: defina las propiedades requeridas:

      * Especifique el modo de destinatario:

         * **Nombre** `mode`
         * **Tipo** `String`)
         * **Valores**:

            * `auto`:: significa que se elige un destinatario automático

               (especificado por la `targetExternal` propiedad para vínculos externos o `targetInternal` para vínculos internos).

            * `manual`:: no aplicable en este contexto
            * `blank`:: no aplicable en este contexto
      * El destinatario para los vínculos internos:

         * **Nombre** `targetInternal`
         * **Tipo** `String`
         * **Valor** del destinatario para los vínculos internos (solo se utiliza cuando el modo es `auto`)
      * Destinatario para vínculos externos:

         * **Nombre** `targetExternal`
         * **Tipo** `String`
         * **Valore** el destinatario de los vínculos externos (solo se utiliza cuando el modo es `auto`).








1. Guarde todos los cambios.
