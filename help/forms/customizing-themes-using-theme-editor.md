---
title: Personalizar temáticas de formularios adaptables mediante el Editor de temáticas
description: Aprenda a utilizar el Editor de temáticas para crear y personalizar temáticas visuales para Forms adaptable basado en componentes principales en Adobe Experience Manager.
feature: Adaptive Forms, Core Components
role: User, Developer
source-git-commit: f1b318803b9b854ec2ce800670f6484799113599
workflow-type: tm+mt
source-wordcount: '1951'
ht-degree: 2%

---


# Personalizar temas de formulario {#customizing-form-themes}

| Versión | Vínculo del artículo |
| -------- | ---------------------------- |
| AEM 6.5 | [Haga clic aquí](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-advanced-authoring/themes.html?lang=es) |
| AEM as a Cloud Service | Este artículo |

El editor de temáticas en Adobe Experience Manager (AEM) Forms es una interfaz visual que permite crear y personalizar temáticas para su Forms adaptable sin necesidad de escribir código manualmente. Una temática define el aspecto de los componentes y paneles del formulario, incluidos los colores de fondo, los estilos de fuente, los bordes, las dimensiones y el espaciado. Al aplicar una temática, los estilos especificados se reflejan en los componentes correspondientes y puede reutilizar la misma temática en varios Forms adaptables.

El editor de temáticas elimina la necesidad de contar con un desarrollador dedicado para el estilo básico del formulario. Con solo un conocimiento práctico de CSS, puede aplicar estilo a los formularios mediante la barra lateral visual o escribir anulaciones de CSS avanzadas directamente dentro del editor.

## Requisitos previos {#prerequisites}

* Permisos de nivel de autor en Adobe Experience Manager Forms.
* Comprensión básica de los principios de estilo CSS. Para obtener una referencia CSS completa, consulte la [referencia CSS de documentos web MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/Reference).

## Vaya al directorio de temas {#navigate-to-themes}

1. Inicie sesión en la instancia de autor de AEM.
1. Vaya a **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Temas]**.

   El directorio Temáticas muestra todas las temáticas disponibles, incluidas las temáticas estándar proporcionadas por AEM Canvas, junto con las temáticas personalizadas que usted o su organización hayan creado.

### Crear una temática nueva {#create-a-new-theme}

1. En el directorio Themes, seleccione la carpeta donde desee almacenar la nueva temática.
1. Haga clic en **[!UICONTROL Crear]** > **[!UICONTROL Tema]**.

   ![Crear nuevo tema](/help/forms/assets/custom-theme-create.png)

1. En el cuadro de diálogo **[!UICONTROL Crear tema]**, especifique los siguientes detalles:
   * **[!UICONTROL Título]**: un título descriptivo para el tema.
   * **[!UICONTROL Nombre]**: El nombre de nodo para el tema.
   * **[!UICONTROL Formulario adaptable para obtener una vista previa del tema]**: para un tema de componente principal, seleccione un formulario adaptable basado en componentes principales. **[!UICONTROL Usar formulario adaptable predeterminado]** usa un formulario adaptable base, no componentes principales. El formulario seleccionado aparecerá en el lienzo del editor de temáticas para previsualizarlo en tiempo real mientras lo edita.
   * **[!UICONTROL Descripción]** *(opcional)*: Una breve descripción del tema.
   * **[!UICONTROL Contenedor de configuración]** *(opcional)*: El contenedor de configuración que contiene los detalles de configuración de Adobe Font.
   * **[!UICONTROL Etiquetas]** *(opcional)*: Etiquetas adjuntas al tema para su identificación y búsqueda.
1. Haga clic en **[!UICONTROL Crear]**.

   ![configurando tema personalizado](/help/forms/assets/custom-theme-name.png)

   Se crea la temática. Ahora puede hacer clic en **[!UICONTROL Editar]** para abrirlo en el editor de temáticas.

### Editar una temática existente {#edit-an-existing-theme}

1. En el directorio **Themes**, seleccione el tema que desee modificar.
1. Haga clic en **[!UICONTROL Editar]** en la barra de acciones para abrir el tema en el editor de temáticas.

   ![Editando un tema](/help/forms/assets/custom-theme-edit.png)

### Cargar una temática {#upload-a-theme}

Puede importar un paquete de temáticas (por ejemplo, uno exportado desde otro entorno) en el directorio Temáticas:

1. En el directorio **Themes**, haga clic en **[!UICONTROL Crear]** > **[!UICONTROL Cargar archivos]**.
1. Busque y seleccione el paquete de temáticas (archivo ZIP) en su equipo y luego haga clic en **[!UICONTROL Cargar]**.

   ![Cargar tema - Menú Crear con la opción Cargar archivo](/help/forms/assets/custom-theme-upload.png)

La temática cargada aparece en el directorio Themes y se puede editar como cualquier otra.

### Descargar una temática {#download-a-theme}

Puede exportar una temática como paquete (archivo ZIP) para reutilizarla en otro entorno de AEM Forms o para realizar una copia de seguridad:

1. En el directorio **Themes**, seleccione uno o varios temas (utilice las casillas de verificación de las tarjetas de los temas).
1. Haga clic en **[!UICONTROL Descargar]** en la barra de acciones. Puede aparecer un cuadro de diálogo con detalles de las temáticas seleccionadas.
1. Confirme o haga clic en **[!UICONTROL Descargar]** en el cuadro de diálogo. El paquete de temáticas se descarga como archivo ZIP en el equipo.

   ![Descargar tema: selecciona el tema y haz clic en Descargar](/help/forms/assets/custom-theme-download.png)

Puedes cargar este ZIP más tarde usando [Cargar un tema](#upload-a-theme) en el mismo o en otro entorno.

## Explicación de la interfaz del editor de temáticas {#understand-the-theme-editor}

Cuando abra una temática en el Editor de temáticas, verá dos áreas principales:

![Editor de temas](/help/forms/assets/custom-theme-editor.png)

* **Lienzo** (lado derecho): muestra una vista previa del formulario adaptable vinculado al tema. Todos los cambios de estilo se reflejan aquí instantáneamente, para que pueda ver el impacto de sus ediciones en tiempo real.
* **Barra lateral** (lado izquierdo): Contiene el panel **Selectores** que enumera todos los componentes de formulario con estilo de una estructura de árbol, como Página, Formulario, Campo, Botón, Panel, Imagen, Captcha y reCaptcha.

### Barra de herramientas Lienzo {#canvas-toolbar}

![Barra de herramientas del lienzo del Editor de temáticas con las opciones Alternar panel lateral, Deshacer, Rehacer, Emulador, Editar/Previsualizar y Tema](/help/forms/assets/custom-theme-toolbar-utilities.png)

De izquierda a derecha, la barra de herramientas proporciona lo siguiente:
* **A: alternar panel lateral**: muestra u oculta la barra lateral de selectores. Utilice esto para maximizar el área de vista previa del formulario cuando desee centrarse en el lienzo o volver a mostrar la barra lateral cuando necesite seleccionar o aplicar estilo a componentes.
* **B: opciones de tema** (menú desplegable): abre un menú con cuatro opciones. Haga clic en él cuando necesite cambiar el formulario de vista previa, ver CSS, administrar estilos guardados u obtener ayuda en el editor. Cuando abra el menú desplegable Opciones de la temática, verá lo siguiente:

  ![Menú desplegable Opciones de la temática que muestra las opciones Configurar, Ver temática CSS, Administrar estilos y Ayuda](/help/forms/assets/custom-theme-configure.png)

   * **[!UICONTROL Configurar]**: cambie el formulario que se muestra en el lienzo a otro formulario adaptable. Utilice esto para comprobar el aspecto de la temática en otro formulario sin salir del editor.
     ![Configurar formulario adaptable para vista previa de tema](/help/forms/assets/custom-theme-switch-af.png)
   * **[!UICONTROL Ver tema CSS]**: abra un cuadro de diálogo con el CSS compilado completo para el tema. Para ver CSS solo para el componente seleccionado actualmente, use **[!UICONTROL Ver CSS]** en la barra lateral (útil para depurar o copiar reglas).
     ![Ver CSS final](/help/forms/assets/custom-theme-view-css.png)
   * **[!UICONTROL Administrar estilos]**: abre el cuadro de diálogo para guardar, asignar nombres y reutilizar estilos de texto e imagen. Los estilos guardados se pueden aplicar a otros componentes; los estilos utilizados recientemente también pueden aparecer para su reutilización rápida.
   * **[!UICONTROL Ayuda]**: inicia la visita guiada por imágenes del editor de temáticas.
* **C: Deshacer / Rehacer**: Revierta o vuelva a aplicar los últimos cambios de estilo. Resulta útil si prueba un estilo y desea dar un paso atrás sin perder otras ediciones.
* **D: Emulador**: seleccione un dispositivo o punto de interrupción (por ejemplo, escritorio, tableta o móvil) para obtener una vista previa del formulario con ese tamaño de pantalla. La vista previa del formulario cambia de tamaño para coincidir con el punto de interrupción seleccionado. Los estilos que establezca mientras selecciona un punto de interrupción sólo se aplican a ese punto de interrupción, por lo que puede definir estilos adaptables. Para obtener más información, consulte [Estilo para diferentes tamaños de pantalla](#styling-for-different-screen-sizes).
* **E: editar/previsualizar**: cambiar entre dos modos. **Editar** es la opción predeterminada: puede hacer clic en los componentes del lienzo para seleccionarlos y cambiar su estilo en la barra lateral. **Vista previa** muestra el formulario tal como lo vería un usuario final sin bordes de selección, etiquetas de componentes o la barra lateral de estilo, de modo que puede comprobar el aspecto y el comportamiento del formulario con temas antes de publicarlo.

<!--**3. Bottom of the sidebar: Simulate Error and Simulate Success**

When you style components by state (for example, Error or Success), you can preview that look without submitting the form. In AEM Forms as a Cloud Service, **Simulate Error** and **Simulate Success** are available at the **bottom of the left sidebar**. Scroll down in the sidebar if you don’t see them; they appear when you have a component selected and let you toggle the preview to match the Error or Success state.

* **Simulate Error**: Show the form as if a field failed validation, so you can see your **[!UICONTROL Error]** state styling.
* **Simulate Success**: Show the form as if validation passed, so you can see your **[!UICONTROL Success]** state styling.

Toggle these on or off as you adjust styles for each state. For more on styling by state, see [Style by component state](#style-by-state).-->

### Aplicar estilo a un componente

Puede seleccionar un componente para aplicarle un estilo de dos formas:
* **Desde el lienzo**: haga clic directamente en un componente del formulario (por ejemplo, un campo de texto, un botón o una lista desplegable). El elemento seleccionado se resalta con un borde y aparece una etiqueta de componente (por ejemplo, &quot;Widget de entrada de texto&quot;) encima. Las opciones de estilo de ese componente aparecen en la barra lateral.

  ![Editar tema del lienzo](/help/forms/assets/custom-theme-field-level.png)

* **Desde el panel Selectores**: utilice la estructura de árbol de la barra lateral izquierda para explorar en profundidad componentes específicos. Por ejemplo, expanda **[!UICONTROL Campo]** > **[!UICONTROL Widget]** > **[!UICONTROL Entrada de texto]** para dirigirse específicamente al widget de cuadro de texto.

  ![Editar tema desde el panel Selector](/help/forms/assets/custom-theme-selector.png)

#### Aplicación de estilos a un componente {#apply-styles-to-a-component}

Una vez seleccionado un componente, la barra lateral muestra las propiedades de estilo disponibles organizadas en las siguientes categorías:

* **[!UICONTROL Dimensiones y posición]**: Controle la alineación, el tamaño, el relleno, el margen, la anchura, la altura y el índice Z.
* **[!UICONTROL Texto]**: configure la familia de fuentes, el grosor, el color, el tamaño, el alto de línea, la alineación, el espaciado entre letras, la decoración del texto y la transformación. Para obtener una lista completa de las propiedades de texto CSS admitidas, consulte la [documentación de texto CSS MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_text).
* **[!UICONTROL Fondo]**: establezca un color de fondo, una imagen o un degradado. Consulte la [documentación de fondos CSS MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_backgrounds_and_borders).
* **[!UICONTROL Borde]**: defina el ancho, el estilo, el radio y el color del borde.
* **[!UICONTROL Efectos]**: Agregue opacidad, modos de fusión y sombras.

Para aplicar un estilo:

1. Seleccione el componente del lienzo o del panel Selectores.
1. Establezca las propiedades visuales deseadas en la barra lateral. Por ejemplo, elija un **[!UICONTROL Color de fondo]** y ajuste el **[!UICONTROL Color de fuente]**.
1. Haga clic en el icono de marca de verificación **[!UICONTROL Aceptar]** para confirmar el cambio de propiedad.

   ![Aplicando estilo](/help/forms/assets/custom-theme-applying-style.png)

<!--#### Style by component state {#style-by-state}

Components can have different visual states (for example, default, focus, hover, disabled, error, success). You can style each state separately so the form looks correct during user interaction and validation.

1. Select the component from the canvas or the Selectors panel.
1. In the sidebar, use the **[!UICONTROL State]** dropdown to choose the state you want to style (for example, **[!UICONTROL Default]**, **[!UICONTROL Focus]**, **[!UICONTROL Hover]**, **[!UICONTROL Disabled]**, **[!UICONTROL Error]**, or **[!UICONTROL Success]**).
1. Set the styling properties (Background, Border, Text, and so on) for that state.
1. Click **[!UICONTROL OK]** to confirm.

   ![State dropdown in sidebar for styling Default, Focus, Error, Success, and other states](/help/forms/assets/custom-theme-state-dropdown.png)

The styles you define apply only when the component is in the selected state. For example, if you set a red border and red background for the **[!UICONTROL Error]** state, the field shows that styling when validation fails. If your environment supports it, use **Simulate Error** or **Simulate Success** at the bottom of the sidebar to preview how the component looks in those states without submitting the form.-->

### Estilo de nivel de formulario {#form-level-styling}

El estilo de nivel de formulario aplica un estilo en sentido amplio a todos los componentes del mismo tipo. Por ejemplo, si selecciona **[!UICONTROL Campo]** en el panel **Selectores** y establece el color de fondo en azul, cada campo del formulario (cuadros de texto, cuadros numéricos, selectores de fecha y listas desplegables) heredará ese fondo azul.

**Ejemplo:** Para establecer un color de fondo uniforme en todos los campos del formulario:

1. En el panel **Selectores**, seleccione **[!UICONTROL Campo]**.
1. En la barra lateral, establezca el **[!UICONTROL Color de fondo]** en azul.
1. Haga clic en **[!UICONTROL OK]**.

   ![Estilo de nivel de formulario](/help/forms/assets/custom-theme-form-level-styling.png)

Todos los componentes de campo del formulario ahora muestran un fondo azul.

### Estilo de nivel de componente {#component-level-styling}

El estilo de nivel de componente se dirige a un tipo de componente específico y anula cualquier estilo de nivel de formulario más amplio. Por ejemplo, si desea que solo el widget de cuadro de texto tenga un color de fondo diferente mientras que el resto de los campos permanezcan azules, debe orientar el widget de cuadro de texto específicamente.

**Ejemplo:** Para establecer un fondo verde y una fuente morada solo en el widget de cuadro de texto:

1. En el panel Selectores, expanda **[!UICONTROL Campo]** > **[!UICONTROL Widget]** > **[!UICONTROL Entrada de texto]**.
1. Establezca **[!UICONTROL Color de fuente]** en morado.
   ![Estilo de nivel de campo](/help/forms/assets/custom-theme-field-level-styling1.png)
1. Establezca el **[!UICONTROL Color de fondo]** en verde.
   ![Estilo de nivel de campo](/help/forms/assets/custom-theme-field-level-styling2.png)
1. Haga clic en **[!UICONTROL OK]**.

El widget Cuadro de texto ahora muestra un fondo verde con texto morado, mientras que el resto de los campos permanecen azules con respecto al estilo de nivel de formulario.

>[!NOTE]
>
> El estilo de nivel de componente **siempre tiene prioridad sobre el estilo de nivel de formulario.** Cuando se define un estilo en ambos niveles, el selector más específico de nivel de componente anula el selector de nivel de formulario más amplio. Esto sigue las [reglas de especificidad CSS](https://developer.mozilla.org/en-US/docs/Web/CSS/Specificity) estándar. Por ejemplo, si establece un fondo azul en todos los campos (nivel de formulario) y un fondo verde en el widget de cuadro de texto (nivel de componente), el cuadro de texto mostrará un fondo verde.

## Estilo para diferentes tamaños de pantalla {#styling-for-different-screen-sizes}

Puede definir diferentes estilos para diferentes tamaños de dispositivo de modo que la temática sea adaptable. La barra de herramientas del editor de temáticas muestra **opciones de dispositivo** (por ejemplo, iPhone 5, iPad, Escritorio, Tablet o Pantalla más pequeña) para obtener una vista previa y aplicar estilo al formulario con ese tamaño de pantalla.

1. En la barra de herramientas del lienzo, use el **emulador de dispositivo**: haga clic en una de las etiquetas de dispositivo (por ejemplo, **[!UICONTROL Escritorio]**, **[!UICONTROL Tableta]**, **[!UICONTROL iPad]**, **[!UICONTROL Pantalla más pequeña]**). Una regla encima del formulario muestra el ancho de píxeles del dispositivo seleccionado.
1. Con ese dispositivo seleccionado, utilice la barra lateral para establecer o ajustar estilos. Los estilos solo se aplican a la vista de dispositivo seleccionada.
1. Cambie a otro dispositivo y defina estilos según sea necesario.
1. Haga clic en **[!UICONTROL Aceptar]** y guarde el tema cuando termine.

   ![Emulador de dispositivo en el editor de temáticas: opciones de regla y dispositivo (escritorio, tableta, iPad, pantalla más pequeña)](/help/forms/assets/custom-theme-emulator.png)

Por lo tanto, el mismo tema puede tener diferentes espaciados, tamaños de fuente o estilos relacionados con el diseño por dispositivo, de modo que coincida con el [comportamiento del editor de temáticas de AEM 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-advanced-authoring/themes.html?lang=es) para un estilo interactivo.

## Usar invalidaciones de CSS avanzadas {#use-advanced-css-overrides}

Para los estilos que no están disponibles a través de la barra lateral visual, puede escribir CSS personalizado directamente en el editor.

1. Seleccione el componente.
1. En la barra lateral, expanda la sección **[!UICONTROL Avanzado]**.
1. Escriba sus reglas CSS personalizadas en el área **[!UICONTROL Anulación de CSS]**. Estas reglas reemplazan cualquier propiedad establecida a través de los controles visuales si hay un conflicto.

Para obtener una referencia de propiedad CSS completa, consulte la [referencia CSS de documentos web MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/Reference).

### Añadir pseudoelementos CSS {#add-css-pseudo-elements}

La sección **[!UICONTROL Advanced]** también admite pseudoelementos CSS como `::before` y `::after`. Permiten insertar contenido o estilo decorativo alrededor de un componente sin modificar la estructura del formulario. Por ejemplo, para agregar un indicador visual antes de un componente de cuadro de texto:

1. Seleccione el componente (por ejemplo, `CMP Textbox`).
1. Expanda la sección **[!UICONTROL Avanzado]**.
1. En los campos de pseudoelemento `::before`, agregue propiedades CSS como:

   ```css
   color: #B10DC9;
   ```

   ![Antes de CSS](/help/forms/assets/custom-theme-before-css.png)

1. En los campos de pseudoelemento `::after`, agregue propiedades CSS como:

   ```css
   color: #006400;
   ```

   ![Después de CSS](/help/forms/assets/custom-theme-after-css.png)


Estos pseudoelementos siguen el comportamiento estándar de CSS. Para obtener una referencia completa, consulte [Pseudoelementos CSS MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/Pseudo-elements).

## Prácticas recomendadas {#best-practices}

* **Use el panel Selectores para un objetivo preciso**: Al aplicar estilo a elementos anidados como una etiqueta de campo o una descripción larga, use el panel Selectores a la izquierda en lugar de hacer clic en el lienzo. Esto garantiza que el selector CSS correcto se genere con la especificidad adecuada.
* **Evitar recursos de otras temáticas**: Al editar una temática, no examinar ni agregar recursos (como imágenes) de otras temáticas. Si la temática de origen se mueve o se elimina, se interrumpirá la temática actual.
* **No cambie la anchura del diseño del panel contenedor**: al especificar una anchura fija en los paneles contenedores, estos se vuelven estáticos y no se adaptan a los diferentes tamaños de pantalla.

## Ver también {#see-also}

{{see-also}}