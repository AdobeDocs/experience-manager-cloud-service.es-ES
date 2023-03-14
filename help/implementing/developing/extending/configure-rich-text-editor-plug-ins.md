---
title: Configuración de los complementos del Editor de texto enriquecido en [!DNL Adobe Experience Manager].
description: Aprenda a configurar las [!DNL Adobe Experience Manager] Complementos del Editor de texto enriquecido.
contentOwner: AG
mini-toc-levels: 1
exl-id: 91619662-e865-47d1-8bec-0739f402353a
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '4301'
ht-degree: 4%

---

# Configuración de los complementos del Editor de texto enriquecido {#configure-the-rich-text-editor-plug-ins}

Las funcionalidades de RTE están disponibles a través de una serie de complementos, cada uno con la propiedad features. Puede configurar la propiedad features para activar o desactivar una o varias funciones RTE. Este artículo describe cómo configurar específicamente los complementos RTE.

Para obtener más información sobre las otras configuraciones de RTE, consulte [Configuración del editor de texto enriquecido](/help/implementing/developing/extending/rich-text-editor.md).

>[!NOTE]
>
>Al trabajar con CRXDE Lite, se recomienda guardar los cambios regularmente mediante [!UICONTROL Guardar todo] opción.

## Activar un complemento y configurar la propiedad features {#activateplugin}

Para activar un complemento, siga estos pasos. Algunos pasos solo son necesarios cuando configura un complemento por primera vez, ya que los nodos correspondientes no existen.

De forma predeterminada, `format`, `link`, `list`, `justify`, y `control` Los complementos y todas sus funciones están habilitados en RTE.

>[!NOTE]
>
>Las respectivas `rtePlugins` El nodo se denomina `<rtePlugins-node>` para evitar duplicaciones en este artículo.

1. Con CRXDE Lite, busque el componente de texto para su proyecto.
1. Cree el nodo principal de `<rtePlugins-node>` si no existe, antes de configurar cualquier complemento RTE:

   * Según el componente, los nodos principales son:

      * `config: .../text/cq:editConfig/cq:inplaceEditing/config`
      * un nodo de configuración alternativo: `.../text/cq:editConfig/cq:inplaceEditing/inplaceEditingTextConfig`
      * `text: .../text/dialog/items/tab1/items/text`
   * Son del tipo: **jcr:primaryType** `cq:Widget`
   * Ambos tienen la siguiente propiedad:

      * **Nombre** `name`
      * **Tipo** `String`
      * **Valor** `./text`


1. Según la interfaz que configure para, cree un nodo `<rtePlugins-node>`, si no existe:

   * **Nombre** `rtePlugins`
   * **Tipo** `nt:unstructured`

1. A continuación, cree un nodo para cada complemento que desee activar:

   * **Tipo** `nt:unstructured`
   * **Nombre** el ID de complemento del complemento requerido

Después de activar un complemento, siga estas directrices para configurar el `features` propiedad.

|  | Habilitar todas las funciones | Active algunas funciones específicas. | Deshabilite todas las funciones. |
|---|---|---|---|
| Nombre | características | características | características |
| Tipo | Cadena | `String` (multi-string; establezca Type en `String` y haga clic en `Multi` en CRXDE Lite) | Cadena |
| Valor | `*` (un asterisco) | Defina uno o más valores de función. | - |

## Comprensión del complemento findreplace {#findreplace}

El `findreplace` no necesita ninguna configuración. Funciona de forma predeterminada.

Al utilizar la funcionalidad de reemplazo, la cadena de reemplazo que se va a reemplazar debe introducirse al mismo tiempo que la cadena de búsqueda. Sin embargo, puede hacer clic en Buscar para buscar la cadena antes de reemplazarla. Si se introduce la cadena de reemplazo después de hacer clic en Buscar, la búsqueda se restablecerá al principio del texto.

El cuadro de diálogo buscar y reemplazar se volverá transparente cuando se haga clic en buscar y se volverá opaco cuando se haga clic en reemplazar. El comportamiento permite al autor revisar el texto que se va a reemplazar. Si los usuarios hacen clic en reemplazar todo, el cuadro de diálogo se cierra y muestra el número de reemplazos realizados.

## Configuración de los modos de pegado {#pastemodes}

Al utilizar RTE, los autores pueden pegar el contenido en uno de los tres modos siguientes:

* **Modo de explorador**: Pegue texto con la implementación de pegado predeterminada del explorador. No es un método recomendado, ya que puede introducir marcado no deseado.

* **Modo de texto sin formato**: pegue el contenido del portapapeles como texto sin formato. Elimina todos los elementos de estilo y formato del contenido copiado antes de insertarlo en [!DNL Experience Manager] componente.

* **Modo MS Word**: pegue el texto, incluidas las tablas, con formato al copiar desde MS Word. No se admite la copia y pegado de texto desde otro origen, como una página web o MS Excel, y sólo conserva un formato parcial.

### Configurar las opciones de pegado disponibles en la barra de herramientas RTE  {#configure-paste-options-available-on-the-rte-toolbar}

Puede proporcionar algunos, todos o ninguno de estos tres iconos a los autores en la barra de herramientas RTE:

* **[!UICONTROL Pegar (Ctrl+V)]**: Se puede preconfigurar para que se corresponda con uno de los tres modos de pegado anteriores.

* **[!UICONTROL Pegar como texto]**: Proporciona funcionalidad de modo de texto sin formato.

* **[!UICONTROL Pegar desde Word]**: proporciona la funcionalidad del modo MS Word.

Para configurar RTE para que muestre los iconos necesarios, siga estos pasos.

1. Vaya al componente, por ejemplo `/apps/<myProject>/components/text`.
1. Vaya al nodo `rtePlugins/edit`. Consulte [activación de un complemento](#activateplugin) si el nodo no existe.
1. Cree el `features` propiedad en el `edit` y agregue una o más de las funciones. Guarde todos los cambios.

### Configure el comportamiento del icono Pegar (Ctrl+V) y del acceso directo {#configure-the-behavior-of-the-paste-ctrl-v-icon-and-shortcut}

Puede preconfigurar el comportamiento del **[!UICONTROL Pegar (Ctrl+V)]** mediante los pasos siguientes. Esta configuración también define el comportamiento del método abreviado de teclado Ctrl+V que los autores utilizan para pegar contenido.

La configuración permite los siguientes tres tipos de casos de uso:

* Pegue texto con la implementación de pegado predeterminada del explorador. No es un método recomendado, ya que puede introducir marcado no deseado. Configurado mediante `browser` más abajo.

* Pegue el contenido del portapapeles como texto sin formato. Elimina todos los elementos de estilo y formato del contenido copiado antes de insertarlo en [!DNL Experience Manager] componente. Configurado mediante `plaintext` más abajo.

* Pegue el texto, incluidas las tablas, con formato al copiar desde MS Word. No se admite la copia y pegado de texto desde otro origen, como una página web o MS Excel, y sólo conserva un formato parcial. Configurado mediante `wordhtml` más abajo.

1. En el componente, navegue hasta `<rtePlugins-node>/edit` nodo. Cree los nodos si estos no existen. Para obtener más información, consulte [activación de un complemento](#activateplugin).
1. En el `edit` nodo cree una propiedad con los siguientes detalles:

   * **Nombre** `defaultPasteMode`
   * **Tipo** `String`
   * **Valor** es uno de los modos de pegado requeridos de `browser`, `plaintext`, o `wordhtml` modos.

### Configurar los formatos permitidos al pegar contenido {#pasteformats}

La función pegar como Microsoft Word (`paste-wordhtml`) el modo se puede configurar para que pueda permitir explícitamente algunos estilos al pegar [!DNL Experience Manager] de otro programa, como [!DNL Microsoft Word].

Por ejemplo, si solo se deben permitir formatos en negrita y listas al pegar en [!DNL Experience Manager], puede filtrar los demás formatos. Esto se denomina filtrado de pegado configurable y se puede hacer para lo siguiente:

* [Texto](#pastemodes)
* [Vínculos](#linkstyles)

En el caso de los vínculos, también puede definir los protocolos que se aceptan automáticamente.

Para configurar qué formatos se permiten al pegar texto en [!DNL Experience Manager] de otro programa:

1. En el componente, vaya al nodo `<rtePlugins-node>/edit`. Cree los nodos si el nodo no existe. Para obtener más información, consulte [activación de un complemento](#activateplugin).
1. Cree un nodo en `edit` nodo en el que se guardarán las reglas de pegado de HTML:

   * **Nombre** `htmlPasteRules`
   * **Tipo** `nt:unstructured`

1. Cree un nodo en `htmlPasteRules`, para contener detalles de los formatos básicos permitidos:

   * **Nombre** `allowBasics`
   * **Tipo** `nt:unstructured`

1. Para controlar los formatos individuales aceptados, cree una o más de las siguientes propiedades en la `allowBasics` nodo:

   * **Nombre** `bold`
   * **Nombre** `italic`
   * **Nombre** `underline`
   * **Nombre** `anchor` (tanto para vínculos como para anclajes con nombre)
   * **Nombre** `image`

   Todas las propiedades son de **Tipo** `Boolean`, por lo que en el **Valor** puede seleccionar o quitar la marca de verificación para habilitar o deshabilitar la funcionalidad.

   >[!NOTE]
   >
   >Si no se define explícitamente, se utiliza el valor predeterminado de true y se acepta el formato.

1. Otros formatos también se pueden definir mediante una serie de otras propiedades o nodos, también aplicados a la variable `htmlPasteRules` nodo:

| Propiedad | Tipo | Descripción |
|--- |--- |--- |
| `allowBlockTags` | `String` | Define la lista de etiquetas de bloque permitidas. Algunas etiquetas de bloque posibles incluyen titulares (h1, h2, h3), párrafos (p), listas (ol, ul), tablas (tabla). |
| `fallbackBlockTag` | `String` | Define la etiqueta de bloque utilizada para cualquier bloque que tenga una etiqueta de bloque no incluida en `allowBlockTags`. Normalmente, `p` es suficiente. |
| `table` | `nt:unstructured` | Define el comportamiento al pegar tablas. Este nodo debe tener la propiedad allow (tipo booleano) para definir si se permite pegar tablas. Si allow se establece en false, debe especificar la propiedad ignoreMode (tipo String) para definir cómo se administra el contenido de la tabla pegada. Los valores válidos para ignoreMode son `remove` para eliminar contenido de tabla y `paragraph` para convertir celdas de tabla en párrafos. |
| `list` | `nt:unstructured` | Define el comportamiento al pegar listas. Debe tener la propiedad `allow` (tipo booleano) para definir si se permite pegar listas. If `allow` se establece en `false`, especifique la propiedad `ignoreMode` (tipo) `String`) para definir cómo gestionar cualquier contenido de lista pegado. Los valores válidos para ignoreMode son `remove` que elimina el contenido de la lista y `paragraph` que convierte los elementos de la lista en párrafos. |

Un ejemplo de un válido `htmlPasteRules` La estructura es la siguiente:

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

## Configurar estilos de texto {#textstyles}

Los autores pueden aplicar estilos para cambiar el aspecto de una parte del texto. Los estilos se basan en clases CSS predefinidas en la hoja de estilos CSS. El contenido estilizado se adjunta como `span` etiquetas con el `class` para hacer referencia a la clase CSS. Por ejemplo:

`<span class=monospaced>Monospaced Text Here</span>`

Cuando el complemento Estilos está habilitado por primera vez, no hay estilos predeterminados disponibles. La lista emergente está vacía. Para proporcionar estilos a los autores, haga lo siguiente:

* Active el selector desplegable Estilo.
* Especifique una o varias ubicaciones de las hojas de estilo.
* Especifique los estilos individuales que se pueden seleccionar en la lista emergente Estilo.

Para reconfiguraciones posteriores, por ejemplo, para agregar más estilos, siga sólo las instrucciones para hacer referencia a una nueva hoja de estilos y para especificar los estilos adicionales.

>[!NOTE]
>
>Los estilos también se pueden definir para [tablas o celdas de tabla](configure-rich-text-editor-plug-ins.md#tablestyles). Estas configuraciones requieren procedimientos independientes.

### Habilitar la lista desplegable de selectores de estilo {#styleselectorlist}

Para ello, habilite el complemento estilos.

1. En el componente, vaya al nodo `<rtePlugins-node>/styles`. Cree los nodos si estos no existen. Para obtener más información, consulte [activación de un complemento](#activateplugin).
1. Cree el `features` propiedad en el `styles` nodo:

   * **Nombre** `features`
   * **Tipo** `String`
   * **Valor** `*` (asterisco)

1. Guarde todos los cambios.

>[!NOTE]
>
>Una vez habilitado el complemento Estilos, la lista desplegable Estilo se muestra en el cuadro de diálogo de edición. Sin embargo, la lista está vacía, ya que no se ha configurado ningún estilo.

### Especificar la ubicación de la hoja de estilos {#locationofstylesheet}

A continuación, especifique las ubicaciones de las hojas de estilos a las que desea hacer referencia:

1. Vaya al nodo raíz del componente de texto, por ejemplo `/apps/<myProject>/components/text`.
1. Añadir la propiedad `externalStyleSheets` al nodo principal de `<rtePlugins-node>`:

   * **Nombre** `externalStyleSheets`
   * **Tipo** `String[]` (varias cadenas; haga clic en **Múltiple** en CRXDE)
   * **Valor(es)** Ruta de acceso y nombre de archivo de cada hoja de estilos que desee incluir. Utilice las rutas del repositorio.

   >[!NOTE]
   >
   >Se pueden agregar referencias a hojas de estilos adicionales en cualquier momento posterior.

1. Guarde todos los cambios.

Al utilizar RTE en un cuadro de diálogo (IU clásica) Puede especificar hojas de estilo optimizadas para la edición de texto enriquecido. Debido a restricciones técnicas, el contexto CSS se pierde en el editor, por lo que puede emular este contexto para mejorar la experiencia WYSIWYG.

El editor de texto enriquecido utiliza un elemento DOM contenedor con un ID de `CQrte` que proporciona diferentes estilos para ver y editar:

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

1. En la definición del componente, vaya al nodo `<rtePlugins-node>/styles`, tal como se crea en [Activación del selector desplegable de estilo](#styleselectorlist).
1. En el nodo `styles`, cree un nodo (también llamado `styles`) para que la lista esté disponible:

   * **Nombre** `styles`
   * **Tipo** `cq:WidgetCollection`

1. Cree un nodo en `styles` para representar un estilo individual:

   * **Nombre**, puede especificar el nombre, pero debe ser adecuado para el estilo
   * **Tipo** `nt:unstructured`

1. Añadir la propiedad `cssName` Vaya a este nodo para hacer referencia a la clase CSS:

   * **Nombre** `cssName`
   * **Tipo** `String`
   * **Valor** El nombre de la clase CSS (sin &#39;.&#39; anterior; por ejemplo, `cssClass` en lugar de `.cssClass`)

1. Añadir la propiedad `text` al mismo nodo; define el texto mostrado en el cuadro de selección:

   * **Nombre** `text`
   * **Tipo** `String`
   * **Valor** Descripción del estilo; aparece en el cuadro de selección desplegable Estilo.

1. Guarde los cambios.

   Repita los pasos anteriores para cada estilo necesario.

### Configuración de RTE para saltos de palabra óptimos en japonés {#jpwordwrap}

Autores que utilizan [!DNL Experience Manager] Para crear contenido en japonés, puede aplicar un estilo a los caracteres para evitar saltos de línea donde no sea necesario. Esto permite a los autores dejar que las frases se rompan en la posición deseada. El estilo de esta funcionalidad se basa en la clase CSS predefinida en la hoja de estilos CSS.

Para crear el estilo que los autores pueden aplicar al texto en japonés, siga estos pasos:

1. Cree un nodo en el nodo Estilos. Consulte [especificar un estilo](#stylesindropdown).
   * Nombre: `jpn-word-wrap`
   * Tipo: `nt:unstructure`

1. Añadir la propiedad `cssName` al nodo para hacer referencia a la clase CSS. Este nombre de clase es un nombre reservado para la función de ajuste de línea en japonés.
   * Nombre: `cssName`
   * Tipo: `String`
   * Valor: `jpn-word-wrap` (sin un precedente `.`)

1. Añada el texto de la propiedad al mismo nodo. El valor es el nombre del estilo que ven los autores al seleccionar el estilo.
   * Nombre: `text`
*Tipo: 
`String`
   * Valor: `Japanese word-wrap`

1. Cree una hoja de estilos y especifique su ruta. Consulte [especificar la ubicación de la hoja de estilo](#locationofstylesheet). Añada el siguiente contenido a la hoja de estilo. Cambie el color de fondo como desee.

   ```css
   .text span.jpn-word-wrap {
       display:inline-block;
   }
   .is-edited span.jpn-word-wrap {
       background-color: #ffddff;
   }
   ```

   ![Hoja de estilo para que la función de ajuste de línea en japonés esté disponible para los autores](assets/rte_jpwordwrap_stylesheet.jpg)

## Configuración de los formatos de párrafo {#paraformats}

Cualquier texto creado en RTE se coloca dentro de una etiqueta de bloque, siendo el valor predeterminado `<p>`. Al habilitar la variable `paraformat` , puede especificar etiquetas de bloque adicionales que se pueden asignar a los párrafos mediante una lista de selección desplegable. Los formatos de párrafo determinan el tipo de párrafo asignando la etiqueta de bloque correcta. El autor puede seleccionarlos y asignarlos mediante el selector de formato. Entre las etiquetas de bloque de ejemplo se incluye el párrafo estándar &lt;p> y encabezados &lt;h1>, &lt;h2>, etc.

>[!CAUTION]
>
>Este complemento no es adecuado para contenido con una estructura compleja, como listas o tablas.

>[!NOTE]
>
>Si se usa una etiqueta de bloque, por ejemplo, un `<hr>` , no se puede asignar a un párrafo, no es un caso de uso válido para `paraformat` plug-in.

Cuando el complemento Formatos de párrafo se activa por primera vez, no hay disponibles formatos de párrafo predeterminados. La lista emergente está vacía. Para proporcionar a los autores formatos de párrafo, haga lo siguiente:

* Habilite la [!UICONTROL Formato] lista de selectores emergentes.
* Especifique las etiquetas de bloque que se pueden seleccionar como formatos de párrafo en el menú emergente.

Para reconfiguraciones posteriores, por ejemplo, para agregar más formatos, siga solo la parte correspondiente de las instrucciones.

### Habilite el selector desplegable Formato {#formatselectorlist}

Para habilitar la variable `paraformat` complemento, siga estos pasos:

1. En el componente, vaya al nodo `<rtePlugins-node>/paraformat`. Cree los nodos si estos no existen. Para obtener más información, consulte [activación de un complemento](#activateplugin).
1. Cree el `features` propiedad en el `paraformat` nodo:

   * **Nombre** `features`
   * **Tipo** `String`
   * **Valor** `*` (asterisco)

>[!NOTE]
>
>Si el complemento no se sigue configurando, los formatos predeterminados habilitados son Párrafo ( `<p>`), Encabezado 1 ( `<h1>`), Encabezado 2 ( `<h2>`), Encabezado 3 ( `<h3>`).

>[!CAUTION]
>
>Al configurar los formatos de párrafo del RTE, no elimine la etiqueta de párrafo &lt;p> como opción de formato. Si la variable `<p>` Si se elimina la etiqueta, el autor del contenido no puede seleccionar [!UICONTROL Formatos de párrafo] opción incluso si hay formatos adicionales configurados.

### Especificar los formatos de párrafo disponibles {#paraformatsindropdown}

Los formatos de párrafo están disponibles para su selección por:

1. En la definición del componente, vaya al nodo `<rtePlugins-node>/paraformat`, tal como se crea en [Activación del selector desplegable de formato](#styleselectorlist).
1. En el `paraformat` nodo crear un nodo, para guardar la lista de formatos:

   * **Nombre** `formats`
   * **Tipo** `cq:WidgetCollection`

1. Cree un nodo en `formats` , contiene detalles de un formato individual:

   * **Nombre**, puede especificar el nombre, pero debe ser adecuado para el formato (por ejemplo, myparagraph, myheading1).
   * **Tipo** `nt:unstructured`

1. A este nodo, agregue la propiedad para definir la etiqueta de bloque utilizada:

   * **Nombre** `tag`
   * **Tipo** `String`
   * **Valor** La etiqueta de bloque para el formato; por ejemplo: p, h1, h2, etc.

      No es necesario introducir los corchetes angulares delimitadores.

1. Al mismo nodo, agregue otra propiedad para que el texto descriptivo aparezca en la lista desplegable:

   * **Nombre** `description`
   * **Tipo** `String`
   * **Valor** Texto descriptivo para este formato; por ejemplo, Párrafo, Encabezado 1, Encabezado 2, etc. Este texto se muestra en la lista de selección Formato.

1. Guarde los cambios.

   Repita los pasos para cada formato requerido.

>[!CAUTION]
Si define formatos personalizados, los formatos predeterminados (`<p>`, `<h1>`, `<h2>`, y `<h3>`) se han eliminado. Volver a crear `<p>` formato, ya que es el formato predeterminado.

## Configuración de caracteres especiales {#spchar}

En un estándar [!DNL Experience Manager] instalación, cuando la variable `misctools` está habilitado para caracteres especiales (`specialchars`) una selección predeterminada está disponible inmediatamente para su uso; por ejemplo, los símbolos de copyright y marca comercial.

Puede configurar el RTE para que la selección de caracteres esté disponible; ya sea definiendo caracteres distintos o una secuencia completa.

>[!CAUTION]
Al agregar los caracteres especiales, se anula la selección predeterminada. Si es necesario, vuelva a definir estos caracteres en la selección.

### Definir un solo carácter {#definesinglechar}

1. En el componente, vaya al nodo `<rtePlugins-node>/misctools`. Cree los nodos si estos no existen. Para obtener más información, consulte [activación de un complemento](#activateplugin).
1. Cree el `features` propiedad en el `misctools` nodo:

   * **Nombre** `features`
   * **Tipo** `String[]`
   * **Valor** `specialchars`

          (o `String / *` si aplica todas las funciones para este complemento)

1. En `misctools` cree un nodo que contenga las configuraciones de caracteres especiales:

   * **Nombre** `specialCharsConfig`
   * **Tipo** `nt:unstructured`

1. En `specialCharsConfig` cree otro nodo que contenga la lista de caracteres:

   * **Nombre** `chars`
   * **Tipo** `nt:unstructured`

1. En `chars` añada un nodo para guardar una definición de carácter individual:

   * **Nombre** puede especificar el nombre, pero debe reflejar el carácter; por ejemplo, la mitad.
   * **Tipo** `nt:unstructured`

1. A este nodo, agregue la siguiente propiedad:

   * **Nombre** `entity`
   * **Tipo** `String`
   * **Valor** la representación HTML del carácter requerido; por ejemplo, `&189;` para la fracción la mitad.

1. Guarde los cambios.

En CRXDE, una vez guardada la propiedad, se muestra el carácter representado. Consulte a continuación el ejemplo de la mitad. Repita los pasos anteriores para que los autores tengan acceso a caracteres más especiales.

![En CRXDE, añada un solo carácter para que esté disponible en la barra de herramientas RTE](assets/chlimage_1-106.png "En CRXDE, añada un solo carácter para que esté disponible en la barra de herramientas RTE")

### Definir un intervalo de caracteres {#definerangechar}

1. Siga los pasos del 1 al 3 de [Definir un solo carácter](#definesinglechar).
1. En `chars` agregue un nodo para guardar la definición del intervalo de caracteres:

   * **Nombre** puede especificar el nombre, pero debe reflejar el intervalo de caracteres; por ejemplo, lápices.
   * **Tipo** `nt:unstructured`

1. Bajo este nodo (denominado según su intervalo especial de caracteres), agregue las dos propiedades siguientes:

   * **Nombre** `rangeStart`

      **Tipo** `Long`
      **Valor** el [Unicode](https://unicode.org/) representación (decimal) del primer carácter del intervalo

   * **Nombre** `rangeEnd`

      **Tipo** `Long`
      **Valor** el [Unicode](https://unicode.org/) representación (decimal) del último carácter del intervalo

1. Guarde los cambios.

   Por ejemplo, defina un intervalo de 9998 10000 le proporcione los siguientes caracteres.

   ![En CRXDE, defina un rango de caracteres que estará disponible en RTE](assets/chlimage_1-107.png)

   *Imagen: en CRXDE, defina un intervalo de caracteres que deben estar disponibles en RTE*

   ![Los caracteres especiales disponibles en RTE se muestran a los autores en una ventana emergente](assets/rtepencil.png "Los caracteres especiales disponibles en RTE se muestran a los autores en una ventana emergente")

## Configurar estilos de tabla {#tablestyles}

Los estilos suelen aplicarse en el texto, pero también se puede aplicar un conjunto independiente de estilos en una tabla o en algunas celdas de la tabla. Estos estilos están disponibles para los autores desde el cuadro Selector de estilo en el cuadro de diálogo Propiedades de celda o Propiedades de tabla. Los estilos están disponibles al editar una tabla dentro de un componente Texto (o derivado) y no en el componente Tabla estándar.

>[!NOTE]
Puede definir estilos para tablas y celdas solo para la IU clásica.

>[!NOTE]
La copia y el pegado de tablas en o desde el componente RTE depende del explorador. No es compatible de serie con todos los exploradores. Puede obtener resultados variados según la estructura de la tabla y el explorador. Por ejemplo, cuando copia y pega una tabla en un componente RTE en Mozilla Firefox en la IU clásica y la IU táctil, el diseño de la tabla no se conserva.

1. En el componente, vaya al nodo `<rtePlugins-node>/table`. Cree los nodos si estos no existen. Para obtener más información, consulte [activación de un complemento](#activateplugin).
1. Cree el `features` propiedad en el `table` nodo:

   * **Nombre** `features`
   * **Tipo** `String`
   * **Valor** `*`

   >[!NOTE]
   Si no desea activar todas las funciones de tabla, puede crear el `features` propiedad como:
   * **Tipo** `String[]`
   * **Valor**(s) uno, o ambos, de los siguientes, según sea necesario:
      * `table` para permitir la edición de propiedades de tabla; incluidos los estilos.
      * `cellprops` para permitir la edición de las propiedades de la celda, incluidos los estilos.


1. Defina la ubicación de las hojas de estilos CSS para hacer referencia a ellas. Consulte [Especificar la ubicación de la hoja de estilos](#locationofstylesheet) ya que es lo mismo que al definir [estilos para texto](#textstyles). La ubicación puede definirse si ha definido otros estilos.
1. En el `table` nodo cree los siguientes nodos según sea necesario:

   * Para definir estilos para toda la tabla (disponible en **[!UICONTROL Propiedades de tabla]**):

      * **Nombre** `tableStyles`
      * **Tipo** `cq:WidgetCollection`
   * Para definir estilos para celdas individuales (disponible en **[!UICONTROL Propiedades de celda]**),

      * **Nombre** `cellStyles`
      * **Tipo** `cq:WidgetCollection`


1. Cree un nodo (en la variable `tableStyles` o `cellStyles` (según corresponda) para representar un estilo individual,

   * **Nombre** puede especificar el nombre, pero debe reflejar el estilo.
   * **Tipo** `nt:unstructured`

1. En este nodo, cree las propiedades:

   * Para definir el estilo CSS al que se hace referencia,

      * **Nombre** `cssName`
      * **Tipo** `String`
      * **Valor** el nombre de la clase CSS (sin un `.`, por ejemplo, `cssClass` en lugar de `.cssClass`)
   * Para definir un texto descriptivo que aparecerá en el selector emergente,

      * **Nombre** `text`
      * **Tipo** `String`
      * **Valor** el texto que aparecerá en la lista de selección


1. Guarde todos los cambios.

Repita los pasos anteriores para cada estilo necesario.

### Configuración de encabezados ocultos en tablas para fines de accesibilidad {#hiddenheader}

A veces, puede crear tablas de datos sin texto visual en un encabezado de columna suponiendo que el propósito del encabezado está implícito en la relación visual de la columna con otras columnas. En este caso, es necesario proporcionar texto interno oculto dentro de la celda en la celda del encabezado para permitir que los lectores de pantalla y otras tecnologías de asistencia ayuden a los lectores con diversas necesidades a comprender el propósito de la columna.

Para mejorar la accesibilidad en estos casos, RTE admite celdas de encabezado ocultas. Además, proporciona opciones de configuración relacionadas con encabezados ocultos en tablas. Esta configuración permite aplicar estilos CSS a encabezados ocultos en los modos de edición y vista previa. Para ayudar a los autores a identificar los encabezados ocultos en el modo de edición, incluya los siguientes parámetros en el código:

* `hiddenHeaderEditingCSS`: especifica el nombre de la clase CSS que se aplica en la celda de encabezado oculto, cuando se edita RTE.
* `hiddenHeaderEditingStyle`: especifica una cadena Style que se aplica en la celda de encabezado oculto cuando se edita RTE.

Si especifica las cadenas CSS y Style en el código, la clase CSS tiene prioridad sobre la cadena de estilo y puede sobrescribir cualquier cambio de configuración que realice la cadena Style.

Para ayudar a los autores a aplicar CSS en encabezados ocultos en el modo de vista previa, puede incluir los siguientes parámetros en el código:

* `hiddenHeaderClassName`: especifica el nombre de la clase CSS que se aplica en la celda de encabezado oculta en el modo de vista previa.
* `hiddenHeaderStyle`: especifica una cadena Style que se aplica en la celda de encabezado oculto en el modo de vista previa.

Si especifica las cadenas CSS y Style en el código, la clase CSS tiene prioridad sobre la cadena de estilo y puede sobrescribir cualquier cambio de configuración que realice la cadena Style.

## Agregar diccionarios para el corrector ortográfico {#adddict}

Cuando se activa el complemento corrector ortográfico, RTE utiliza diccionarios para cada idioma adecuado. A continuación, se seleccionan según el idioma del sitio web tomando la propiedad language del subárbol o extrayendo el idioma de la dirección URL; por ejemplo. el `/en/` La rama de se marca como Inglés, la `/de/` sucursal en alemán.

>[!NOTE]
El mensaje &quot;Fallo en la revisión ortográfica&quot;. se ve si se prueba una comprobación para un idioma que no está instalado.

Una instalación de Experience Manager estándar incluye los diccionarios para:

* Inglés (en_us)
* Inglés británico (en_gb)

>[!NOTE]
Los diccionarios estándar se encuentran en `/libs/cq/spellchecker/dictionaries`, junto con los archivos Léame correspondientes. No modifique los archivos.

Para agregar más diccionarios, si es necesario, siga estos pasos.

1. Navegue hasta la página [https://extensions.openoffice.org/](https://extensions.openoffice.org/).
1. Seleccione el idioma necesario y descargue el archivo ZIP con las definiciones ortográficas. Extraiga el contenido del archivo en su sistema de archivos.

   >[!CAUTION]
   Solo los diccionarios de `MySpell` es compatible con el formato de OpenOffice.org v2.0.1 o anterior. Como los diccionarios ahora son archivos de almacenamiento, se recomienda verificarlos después de la descarga.

1. Busque los archivos .aff y .dic. Mantenga el nombre del archivo en minúsculas. Por ejemplo, `de_de.aff` y `de_de.dic`.
1. Cargue los archivos .aff y .dic en el repositorio en `/apps/cq/spellchecker/dictionaries`.

>[!NOTE]
El corrector ortográfico RTE está disponible bajo demanda. No se ejecuta automáticamente cuando empieza a escribir texto.
Para ejecutar el corrector ortográfico, pulse o haga clic en el botón Corrector ortográfico de la barra de herramientas. RTE revisa la ortografía de las palabras y resalta las palabras mal escritas.
Si incorpora cualquier cambio que sugiera el corrector ortográfico, el estado del texto cambiará y las palabras mal escritas dejarán de resaltarse. Para ejecutar el corrector ortográfico, toque o haga clic en el botón Corrector ortográfico de nuevo.

## Configuración del tamaño del historial para acciones de deshacer y rehacer {#undohistory}

RTE permite a los autores deshacer o rehacer algunas ediciones últimas. De forma predeterminada, se almacenan 50 ediciones en el historial. Puede configurar este valor según sea necesario.

1. En el componente, vaya al nodo `<rtePlugins-node>/undo`. Cree estos nodos si no existen. Para obtener más información, consulte [activación de un complemento](#activateplugin).
1. En el `undo` nodo crear la propiedad:

   * **Nombre** `maxUndoSteps`
   * **Tipo** `Long`
   * **Valor** número de pasos de deshacer que desea guardar en el historial. El valor predeterminado es 50. Uso `0` para desactivar por completo deshacer/rehacer.

1. Guarde los cambios.

## Configuración del tamaño de la pestaña {#tabsize}

Cuando se presiona el carácter de tabulación dentro de cualquier texto, se inserta un número predefinido de espacios; de forma predeterminada, son tres espacios sin saltos y un espacio.

Para definir el tamaño de la pestaña:

1. En el componente, vaya al nodo `<rtePlugins-node>/keys`. Cree los nodos si estos no existen. Para obtener más información, consulte [activación de un complemento](#activateplugin).
1. En el `keys` nodo crear la propiedad:

   * **Nombre** `tabSize`
   * **Tipo** `String`
   * **Valor** el número de caracteres de espacio que se utilizarán para el tabulador.

1. Guarde los cambios.

## Establecer margen de sangría {#indentmargin}

Cuando la sangría está activada (predeterminada), puede definir el tamaño de la sangría:

>[!NOTE]
Este tamaño de sangría solo se aplica a párrafos (bloques) de texto; no afecta a la sangría de listas reales.

1. En el componente, vaya al nodo `<rtePlugins-node>/lists`. Cree estos nodos si no existen. Para obtener más información, consulte [activación de un complemento](#activateplugin).
1. En el `lists` nodo crear el `identSize` parámetro:

   * **Nombre**: `identSize`
   * **Tipo**: `Long`
   * **Valor**: número de píxeles necesarios para el margen de sangría.

## Configurar la altura del espacio editable {#editablespace}

Puede definir la altura del espacio editable que se muestra en el cuadro de diálogo del componente. La configuración solo es aplicable cuando se utiliza RTE en un cuadro de diálogo. La configuración no cambia la altura de la ventana de diálogo.

1. En el `../items/text` , en la definición del cuadro de diálogo del componente, cree una propiedad:

   * **Nombre** `height`
   * **Tipo** `Long`
   * **Valor** altura del lienzo de edición en píxeles.

1. Guarde los cambios.

## Configuración de estilos y protocolos para vínculos {#linkstyles}

Al añadir vínculos en [!DNL Experience Manager], puede definir los estilos CSS que se van a utilizar y los protocolos que se van a aceptar automáticamente. Para configurar cómo se añaden los vínculos en [!DNL Experience Manager] desde otro programa, defina las reglas del HTML.

1. Con CRXDE Lite, busque el componente de texto para su proyecto.
1. Cree un nodo en el mismo nivel que `<rtePlugins-node>`, es decir, cree el nodo en el nodo principal de `<rtePlugins-node>`:

   * **Nombre** `htmlRules`
   * **Tipo** `nt:unstructured`

   >[!NOTE]
   El `../items/text` tiene la propiedad:
   * **Nombre** `xtype`
   * **Tipo** `String`
   * **Valor** `richtext`

   La ubicación del `../items/text` El nodo puede variar, según la estructura del cuadro de diálogo. Dos ejemplos son `/apps/myProject>/components/text/dialog/items/text` y `/apps/<myProject>/components/text/dialog/items/panel/items/text`.

1. En `htmlRules`, cree un nodo.

   * **Nombre** `links`
   * **Tipo** `nt:unstructured`

1. En el `links` nodo, defina las propiedades según sea necesario:

   * Estilo CSS para vínculos internos:

      * **Nombre** `cssInternal`
      * **Tipo** `String`
      * **Valor** el nombre de la clase CSS (sin &#39;.&#39;); por ejemplo, `cssClass` en lugar de `.cssClass`)
   * Estilo CSS para vínculos externos

      * **Nombre** `cssExternal`
      * **Tipo** `String`
      * **Valor** el nombre de la clase CSS (sin &#39;.&#39;); por ejemplo, `cssClass` en lugar de `.cssClass`)
   * Matriz de válidos **[!UICONTROL protocolos]** incluyendo `https://`, `https://`, `file://`, `mailto:`, y otros,

      * **Nombre** `protocols`
      * **Tipo** `String[]`
      * **Valor**(s) uno o más protocolos
   * **defaultProtocol** (propiedad de tipo **Cadena**): Protocolo que se utilizará si el usuario no ha especificado ninguno explícitamente.

      * **Nombre** `defaultProtocol`
      * **Tipo** `String`
      * **Valor**(s) uno o más protocolos predeterminados
   * Definición de cómo gestionar el atributo de destino de un vínculo. Cree un nodo:

      * **Nombre** `targetConfig`
      * **Tipo** `nt:unstructured`

      En el nodo `targetConfig`: defina las propiedades requeridas:

      * Especifique el modo de destino:

         * **Nombre** `mode`
         * **Tipo** `String`)
         * **Valor**(s) :

            * `auto`: significa que se elige un destinatario automático

               (especificado por el `targetExternal` para vínculos externos o `targetInternal` para vínculos internos).

            * `manual`: no aplicable en este contexto
            * `blank`: no aplicable en este contexto
      * El destino de los vínculos internos:

         * **Nombre** `targetInternal`
         * **Tipo** `String`
         * **Valor** el destino de los vínculos internos (solo se utiliza cuando el modo sea `auto`)
      * El destino de los vínculos externos:

         * **Nombre** `targetExternal`
         * **Tipo** `String`
         * **Valor** el destino de los vínculos externos (solo se utiliza cuando el modo es `auto`).








1. Guarde todos los cambios.
