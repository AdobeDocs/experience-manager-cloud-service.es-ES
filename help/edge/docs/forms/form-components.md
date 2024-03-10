---
title: Componentes y propiedades de formulario
description: Este documento proporciona información general sobre los componentes de formulario y sus propiedades disponibles en el servicio de entrega perimetral de AEM Forms.
feature: Edge Delivery Services
hide: true
hidefromtoc: true
exl-id: 7d087d41-9313-482a-a905-8955b0999781
source-git-commit: 2aa70e78764616f41fe64e324c017873cfba1d5b
workflow-type: tm+mt
source-wordcount: '964'
ht-degree: 3%

---

# Componentes y propiedades de formulario: servicio de entrega perimetral de AEM Forms

Los servicios de envío perimetral de AEM Forms le permiten crear formularios interactivos y fáciles de usar utilizando varios componentes. Estos componentes se adaptan a diferentes tipos de recopilación de datos y se pueden personalizar fácilmente para adaptarlos a sus necesidades específicas.


![Hoja de cálculo de ejemplo con algunos componentes y propiedades](/help/edge/assets/sample-form-in-spreadsheet.png)

El bloque de Forms adaptable genera un [estructura uniforme del HTML](/help/edge/docs/forms/style-theme-forms.md) para todos los tipos de campo y contenedores (paneles), lo que garantiza la coherencia. Esta estructura coherente facilita la [aplicar estilo a un formulario](/help/edge/docs/forms/style-theme-forms.md).

## Componentes disponibles

A continuación se muestra una descripción general de los componentes disponibles:

### Campos de entrada

- Todos los HTML válidos5 [tipos de entrada](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input#input_types) y [área de texto](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/textarea). Por ejemplo, botón, casilla de verificación, color, fecha, fecha, hora-local, correo electrónico, archivo, oculto, imagen, mes, número, contraseña, radio, intervalo, restablecer, enviar, teléfono, texto, hora, URL y semana.

### Controles de selección

- [Grupos de casillas](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/checkbox): para seleccionar varias opciones.
- [Grupos de radio](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/radio): para seleccionar una sola opción de un grupo.
- [Menús desplegables](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/select): para mostrar un menú de opciones. Por ejemplo, el cuadro desplegable.

### Contenedores

- Paneles/contenedores: para agrupar elementos de formulario relacionados y mejorar su organización. Es una combinación de las [fieldset](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/fieldset) y [leyenda](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/legend).






## Propiedades de componentes

Cada componente del formulario incluye varias propiedades que le permiten controlar su comportamiento y apariencia. Estas son las propiedades que admiten los componentes de bloque de Forms adaptable:


| Propiedad | Componentes aplicables | Detalles |
|--------------|------------------------------|----------------------------------------------------------------------|
| Tipo | Todos | Especifica el tipo de componente. Esta propiedad determina el comportamiento y el aspecto del campo de entrada. Por ejemplo, para las entradas de texto, el tipo puede ser &quot;texto&quot;, &quot;correo electrónico&quot; para las entradas de correo electrónico y &quot;contraseña&quot; para las entradas de contraseña. El bloque de Forms adaptable admite  <a href="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input#input_types">todos los tipos de entrada válidos de HTML5</a>, <a href="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/textarea">área de texto</a>, <a href="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/select">select</a>, y <a href="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/fieldset">fieldset</a> como tipo. |
| Tipo | Todos | Especifica el tipo de componente. Esta propiedad determina el comportamiento y el aspecto del campo de entrada. Por ejemplo, para las entradas de texto, el tipo puede ser &quot;texto&quot;, &quot;correo electrónico&quot; para las entradas de correo electrónico y &quot;contraseña&quot; para las entradas de contraseña. El bloque de Forms adaptable admite  <a href="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input#input_types">todos los tipos de entrada válidos de HTML5</a>, <a href="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/textarea">área de texto</a>, <a href="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/select">select</a>, y <a href="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/fieldset">fieldset</a> como tipo. |
| Nombre | Todos | Identifica el componente para el envío de formularios. El atributo name se utiliza cuando se envían los datos del formulario al servidor, asociando la entrada del usuario con un campo específico. |
| Etiqueta | Todos | Proporciona información contextual a los usuarios. La etiqueta es el texto que se muestra junto al componente, lo que orienta a los usuarios sobre qué información introducir. |
| Valor | Texto, Contraseña, Correo electrónico, Número, Intervalo, Fecha y sus variantes (fecha y hora local, mes, semana, hora), Casilla de verificación, Radio, Oculto, Enviar, Botón | Especifica el valor inicial del componente. Para las entradas de texto, el área de texto y los elementos seleccionados, esta es la opción o el texto predeterminado que se muestra. Para los componentes de radio y casilla de verificación, este es el valor/datos enviados cuando se seleccionan. El atributo value es opcional, pero debe considerarse obligatorio para las entradas de casilla de verificación y radio. |
| Marcador de posición | Texto, Tel, Correo electrónico, Contraseña, Fecha (y sus variantes como mes, semana, hora, fecha y hora-local), Número, Intervalo | Ofrece sugerencias para la entrada esperada. El atributo placeholder proporciona una breve sugerencia que describe el valor esperado del campo de entrada. Desaparece una vez que el usuario empieza a escribir. |
| Descripción | Todos | Proporciona información adicional sobre el componente y sirve como texto de ayuda. El campo de descripción permite explicar con más detalle el propósito o las instrucciones para rellenar el componente. Ayuda a los usuarios a comprender el contexto del campo de entrada. |
| Visible | Todos | Controla la visibilidad inicial. El atributo visible es una propiedad booleana que determina si el componente es visible u oculto inicialmente cuando se carga el formulario. Si se establece en true, se muestra el campo; de lo contrario, se oculta. |
| Obligatorio | Texto, Tel, Correo electrónico, Contraseña, Fecha y sus variantes (fecha y hora-local, mes, semana, hora), Número, Casilla de verificación, Radio, Archivo, Seleccionar (desplegable), Área de texto | Indica si el campo debe rellenarse antes del envío. El atributo mandatory es una propiedad booleana que se utiliza para especificar si el usuario debe proporcionar los datos del campo antes de enviar el formulario. |
| Mínimo | Fecha (y sus variantes como mes, semana, hora, fecha y hora local), Número, Intervalo | Especifica el valor mínimo permitido. El atributo min establece el valor mínimo que el usuario puede introducir en el campo. Por ejemplo, para las entradas de número, define el número aceptable más bajo. |
| Max | Fecha (y sus variantes como mes, semana, hora, fecha y hora local), Número, Intervalo | Especifica el valor máximo permitido. El atributo max establece el valor máximo que el usuario puede introducir en el campo. Por ejemplo, para las entradas de fecha, define la fecha aceptable más alta. |
| Aceptar | Archivo | Define los tipos de archivo permitidos. El atributo accept es una lista separada por comas de especificadores de tipo de archivo únicos que restringe los tipos de archivos que los usuarios pueden seleccionar en un campo de entrada de archivo. |
| Múltiple | Archivo | Permite selecciones múltiples. El atributo multiple es una propiedad booleana que se utiliza con los campos de entrada de archivo. Cuando se establece en true, permite a los usuarios seleccionar más de un archivo. |
| Opciones | Lista desplegable | Especifica las opciones para los menús desplegables. La propiedad options es una lista de opciones separadas por comas para los menús desplegables que define las opciones seleccionables que se muestran al usuario. |
| Comprobado | Casilla de verificación, radio | Determina si el campo está seleccionado de forma predeterminada. El atributo activado es una propiedad booleana que se utiliza con las entradas de casilla de verificación y radio. Cuando se establece en true, indica que el campo está seleccionado de forma predeterminada cuando se carga el formulario. |
| Fieldset | Todos | Agrupa campos para crear secciones visualmente distintas dentro de un formulario. El elemento fieldset agrupa los campos relacionados dentro de un formulario, separándolos visualmente para mejorar la organización y la experiencia del usuario. </br> Para organizar un conjunto de campos dentro de un conjunto de campos, simplemente utilice el `fieldset` y especifique su atributo name. En el ejemplo siguiente, demostramos cómo se encapsulan los botones de opción dentro de un solo conjunto de campos para mejorar la organización. ![Ejemplo de conjunto de campos](/help/edge/assets/fieldset-example.png) |



<!--

## Supported HTML 5 input types in Adaptive Forms Block

The Adaptive Forms Block supports a range of HTML 5 input types, and it also seamlessly renders forms created with AEM core components.
Here is the table which outlines how core components correspond to their HTML-5 input types in Edge Delivery:
<table>
 <tbody>
  <tr>
   <td><b>Core Components</b> </td>
   <td><b>HTML 5 input type</b> </td>
   <td><b>Details</b></td>
  </tr>
  <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/form-container.html">Form Container</a></td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input#form">form </td>
   <td> Create a form to capture user inputs.
   </td>
  </tr>
  <tr>
   <td><a herf="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/text-input.html">Text Input</a></td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/text">text</a></td>
   <td> Defines a single-line text input field. </td>
  </tr>
  <tr>
   <td><a href = "https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/number-input.html">Number Input</a></td>
   <td><a href = "https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/number">number</a></td>
   <td>Lets user  enter a number input. You can also add built-in validation to reject non-numerical inputs. Lets user  enter a number input. You can also add built-in validation to reject non-numerical inputs. Initially, the input field is displayed as a number input. If a user applies a display pattern, it changes to text to allow the author to apply number formatting, since HTML 5 lacks support for display patterns. However, when the user clicks it, it returns to typing numbers.</td>
  </tr>
  <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/date-picker.html">Date Picker</a></td>
   <td><a href = "https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/date">date </a></td>
   <td> Create an input field for entering a date. You have the option to input the date either through a text box, which validates the entry, or through a dedicated date picker interface. Initially, the native date input field is displayed. If a user applies a display pattern, it changes to text to allow the user to apply formatting, since HTML 5 lacks support for display patterns. However, when the user clicks it, it returns to typing a date.</td>
  </tr>
  <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/file-attachment.html">File Attachment</a></td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/file">file</a></td>
   <td> Allows user to choose one or more files from the device storage. It supports enhanced file input validations, such as accepted file types, file size restrictions, and minimum/maximum file selection limits. </td>
  </tr>
  <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/drop-down.html"> Dropdown List</a></td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/select">select</a></td>
   <td> Allows users to select one or more options from a list of predefined options. The options can be of type String, Number, or Boolean.</td>
  </tr>
  <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/checkbox-group.html">Checkbox Group</a></td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/checkbox">multiple checkbox</a></td>
   <td> Allow users to select one or more options from a list. Multiple checkboxes are generated with identical names, each corresponding to an item in the enum. </td>
  </tr>
  <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/radio-button.html">Radio Button Group</td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/radio">multiple radio</a></td>
   <td> Allows a user to select one option from a group of related options. Multiple radio buttons are generated with identical names, each corresponding to an item in the enum.</td>
  </tr>
  <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/button.html">Button</td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/button">button</a></td>
   <td>A UI element that allows users to trigger an action when clicked. </td>
  </tr>
  <tr>
   <td><a href =""https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/panel-container.html">Panel</a></td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/fieldset">fieldset with legend</a></td>
   <td> Group sections within a form, where a nested *legend* element adds a caption for the form.</td>
  </tr>
   <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/wizard.html">Wizard</a></td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/fieldset">fieldset</a></td>
   <td>Groups related sections within a form. It also controls the arrangement, supporting display options for positioning them at the top or at the left side. </td>
  </tr>
    <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/text.html">Text</a></td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/p">p</a></td>
   <td>A p tag marks a paragraph. In visual content, paragraphs are chunks of text separated by blank lines or an indented first line</td>
  </tr>
     <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/submit-button.html">Submit button</td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/submit">submit</a></td>
   <td> A UI element that enables users to submit a form to the server upon clicking. If a user adds a submit rule to a button, it functions as the submit button. </td>
  </tr>
     <tr>
   <td><a href = "https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/reset-button.html">Reset button</a></td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/reset">reset</a></td>
   <td>A UI element that resets a form upon clicking. If a user adds a reset rule to a button, it functions as the reset button. </td>
  </tr>
    <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/email-input.html">Email Input</td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/email">email</a></td>
   <td> Allows the user to enter and edit an email address. If the user adds the multiple attributes, a list of email addresses can be added or edited.</td>
  </tr>
   <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/telephone-input.html">Telephone Input</a></td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/tel">tel</a></td>
   <td>Allows user to enter and edit a telephone number.</td>
  </tr>
   <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/header.html">Header</td>
   <td><a href = "https://developer.mozilla.org/en-US/docs/Web/HTML/Element/header"> header</a></td>
   <td>It includes introductory content, typically a group of introductory or navigational aids. It is supported outside Form container. </td>
  </tr>
  <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/footer.html">Footer</td>
   <td><a href = "https://developer.mozilla.org/en-US/docs/Web/HTML/Element/footer">footer</a></td>
   <td> Contains information such as copyright data or links to related documents. It is supported outside Form container.</td>
  </tr>
  <tr>
   <td><a href = "https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/accordion.html">Accordion<a></td>
   <td><i>Not yet supported in Adaptive Forms Block</i></td>
   <td> Allows user to create expandable and collapsible sections in a form. </td>
  </tr>
  <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/horizontal-tabs.html">Horizontal tabs</a></td>
   <td><i>Not yet supported in Adaptive Forms Block</i></td>
   <td>Organizes multiple sections of a form into separate tabs which are displayed horizontally.</td>
  </tr>
  <tr>
   <td><a href = "https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/image.html">Image</a></td>
   <td><i>Not yet supported in Adaptive Forms Block</i></td>
   <td> Allows user to include images in a form.</td>
  </tr><tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/title.html">Title</a></td>
   <td><i>Not yet supported in Adaptive Forms Block</i></td>
   <td> Refers to the text that appears at the top of the form. </td>
  </tr>
  <tr>
   <td><a href = "https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/submit-button.html">Switch</td>
   <td><i>Not yet supported in Adaptive Forms Block</i></td>
   <td> A two-state toggle that allows user to select between two states such as enabling or disabling a feature, setting, or functionality.</td>
  </tr>
 </tbody>
</table> -->

## Más información

- [Creación y previsualización de un formulario](/help/edge/docs/forms/create-forms.md)
- [Habilitar formulario para enviar datos](/help/edge/docs/forms/submit-forms.md)
- [Publicar un formulario en la página de Sites](/help/edge/docs/forms/publish-forms.md)
- [Agregar validaciones a campos de formulario](/help/edge/docs/forms/validate-forms.md)
- [Cambiar temáticas y estilo de formulario](/help/edge/docs/forms/style-theme-forms.md)
