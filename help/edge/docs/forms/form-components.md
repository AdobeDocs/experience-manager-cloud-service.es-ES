---
title: Componentes de bloque de formulario adaptable y sus propiedades
description: Este documento proporciona información general sobre los componentes de formulario y sus propiedades disponibles en el servicio de entrega perimetral de AEM Forms.
feature: Edge Delivery Services
exl-id: 7d087d41-9313-482a-a905-8955b0999781
source-git-commit: 5eee563a9a425ef187afed69a8159d8b1298dad7
workflow-type: tm+mt
source-wordcount: '938'
ht-degree: 3%

---

# Componentes de bloque de formulario adaptable y sus propiedades

Los servicios de envío perimetral de AEM Forms le permiten crear formularios interactivos y fáciles de usar utilizando varios componentes. Estos componentes se adaptan a diferentes tipos de recopilación de datos y se pueden personalizar fácilmente para adaptarlos a sus necesidades específicas.


![Hoja de cálculo de ejemplo con algunos componentes y propiedades](/help/edge/assets/sample-form-in-spreadsheet.png)

El bloque de Forms adaptable genera un [estructura uniforme del HTML](/help/edge/docs/forms/style-theme-forms.md) para todos los tipos de campo y contenedores (paneles), lo que garantiza la coherencia. Esta estructura coherente facilita la [aplicar estilo a un formulario](/help/edge/docs/forms/style-theme-forms.md).

## Componentes disponibles

A continuación se muestra una descripción general de los componentes disponibles:

### Campos de entrada

* Todos los HTML válidos5 [tipos de entrada](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input#input_types) y [área de texto](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/textarea). Por ejemplo, botón, casilla de verificación, color, fecha, fecha, hora-local, correo electrónico, archivo, oculto, imagen, mes, número, contraseña, radio, intervalo, restablecer, enviar, teléfono, texto, hora, URL y semana.

### Controles de selección

* [Grupos de casillas](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/checkbox): para seleccionar varias opciones.
* [Grupos de radio](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/radio): para seleccionar una sola opción de un grupo.
* [Menús desplegables](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/select): para mostrar un menú de opciones. Por ejemplo, el cuadro desplegable.

### Contenedores

* Paneles/contenedores: para agrupar elementos de formulario relacionados y mejorar su organización. Es una combinación de las [fieldset](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/fieldset) y [leyenda](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/legend).


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

## Consulte también

{{see-more-forms-eds}}
