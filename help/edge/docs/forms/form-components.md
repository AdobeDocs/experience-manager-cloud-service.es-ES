---
title: Componentes de bloque de formulario adaptable y sus propiedades
description: Este documento proporciona información general sobre los componentes de formulario y sus propiedades disponibles en Edge Delivery Services para AEM Forms.
feature: Edge Delivery Services
exl-id: 7d087d41-9313-482a-a905-8955b0999781
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '1007'
ht-degree: 100%

---

# Componentes de bloque de formulario adaptable y sus propiedades

Edge Delivery Services para AEM Forms permite crear formularios interactivos y de fácil manejo utilizando varios componentes. Estos componentes se adaptan a diferentes tipos de recopilación de datos y se pueden personalizar fácilmente para adaptarlos a sus necesidades específicas.


![Una hoja de cálculo de ejemplo con algunos componentes y propiedades](/help/edge/assets/sample-form-in-spreadsheet.png)

El bloque de formularios adaptables genera una [estructura HTML uniforme](/help/edge/docs/forms/style-theme-forms.md) para todos los tipos de campo y contenedores (paneles), lo que garantiza la coherencia. Esta estructura coherente facilita la [aplicación de estilo a un formulario](/help/edge/docs/forms/style-theme-forms.md).

## Componentes disponibles

A continuación se muestra una descripción general de los componentes disponibles:

### Campos de entrada

- Todos los [tipos de entrada](https://developer.mozilla.org/es-es/docs/Web/HTML/Element/input#input_types) HTML5 válidos y el [área de texto](https://developer.mozilla.org/es-es/docs/Web/HTML/Element/textarea). Por ejemplo, botón, casilla de verificación, color, fecha, fecha, fecha-hora local, correo electrónico, archivo, oculto, imagen, mes, número, contraseña, radio, intervalo, restablecer, enviar, teléfono, texto, hora, URL y semana.

### Controles de selección

- [Grupos de casillas](https://developer.mozilla.org/es-es/docs/Web/HTML/Element/input/checkbox): para seleccionar varias opciones.
- [Grupos de radio](https://developer.mozilla.org/es-es/docs/Web/HTML/Element/input/radio): para seleccionar una sola opción de un grupo.
- [Menús desplegables](https://developer.mozilla.org/es-es/docs/Web/HTML/Element/select): para mostrar un menú de opciones. Por ejemplo, el cuadro desplegable.

### Contenedores

- Paneles/contenedores: para agrupar elementos de formulario relacionados y mejorar su organización. Es una combinación de [fieldset](https://developer.mozilla.org/es-es/docs/Web/HTML/Element/fieldset) y [legend](https://developer.mozilla.org/es-es/docs/Web/HTML/Element/legend).


## Propiedades de componentes

Cada componente del formulario incluye varias propiedades que le permiten controlar su comportamiento y apariencia. Estas son las propiedades que admiten los componentes del bloque de formularios adaptables:


| Propiedad | Componentes aplicables | Detalles |
|--------------|------------------------------|----------------------------------------------------------------------|
| Tipo | Todos | Especifica el estilo del componente. Esta propiedad determina el comportamiento y el aspecto del campo de entrada. Por ejemplo, para las entradas de texto, el tipo puede ser “texto”, “correo electrónico” para las entradas de correo electrónico y “contraseña” para las entradas de contraseña. El bloque de formularios adaptables admite <a href="https://developer.mozilla.org/es-es/docs/Web/HTML/Element/input#input_types">todos los tipos de entrada HTML5 válidos</a>, <a href="https://developer.mozilla.org/es-es/docs/Web/HTML/Element/textarea">textarea</a>, <a href="https://developer.mozilla.org/es-es/docs/Web/HTML/Element/select">seleccionar</a> y <a href="https://developer.mozilla.org/es-es/docs/Web/HTML/Element/fieldset">fieldset</a> como tipo. |
| Nombre | Todos | Identifica el componente para el envío de formularios. El atributo name se utiliza cuando se envían los datos del formulario al servidor, asociando la entrada del usuario con un campo específico. |
| Etiqueta | Todos | Proporciona información contextual a los usuarios. La etiqueta es el texto que se muestra junto al componente, lo que orienta a los usuarios sobre qué información introducir. |
| Valor | Texto, Contraseña, Correo electrónico, Número, Intervalo, Fecha y sus variantes (fecha y hora local, mes, semana, hora), Casilla de verificación, Radio, Oculto, Enviar, Botón | Especifica el valor inicial del componente. Para las entradas de texto, textarea y los elementos seleccionados, esta es la opción o el texto predeterminado que se muestra. Para los componentes de radio y casilla de verificación, este es el valor/datos enviados cuando se seleccionan. El atributo value es opcional, pero debe considerarse obligatorio para las entradas de casilla de verificación y radio. |
| Marcador de posición | Texto, Tel., Correo electrónico, Contraseña, Fecha (y sus variantes como mes, semana, hora, fecha y hora-local), Número, Intervalo | Ofrece sugerencias para la entrada esperada. El atributo placeholder proporciona una breve sugerencia que describe el valor esperado del campo de entrada. Desaparece una vez que el usuario empieza a escribir. |
| Descripción | Todos | Proporciona información adicional sobre el componente y sirve como texto de ayuda. El campo de descripción permite explicar con más detalle el propósito o las instrucciones para rellenar el componente. Ayuda a los usuarios a comprender el contexto del campo de entrada. |
| Visible | Todos | Controla la visibilidad inicial. El atributo visible es una propiedad booleana que determina si el componente es visible o está oculto inicialmente cuando se carga el formulario. Si se establece en true, se muestra el campo; de lo contrario, se oculta. |
| Obligatorio | Texto, Tel., Correo electrónico, Contraseña, Fecha y sus variantes (fecha y hora local, mes, semana, hora), Número, Casilla de verificación, Radio, Archivo, Seleccionar (desplegable), Área de texto | Indica si el campo debe rellenarse antes del envío. El atributo mandatory es una propiedad booleana que se utiliza para especificar si el usuario debe proporcionar los datos del campo antes de enviar el formulario. |
| Mínimo | Fecha (y sus variantes como mes, semana, hora, fecha y hora local), Número, Intervalo | Especifica el valor mínimo permitido. El atributo mín. establece el valor mínimo que el usuario puede introducir en el campo. Por ejemplo, para las entradas de número, define el número aceptable más bajo. |
| Máx. | Fecha (y sus variantes como mes, semana, hora, fecha y hora local), Número, Intervalo | Especifica el valor máximo permitido. El atributo máx. establece el valor máximo que el usuario puede introducir en el campo. Por ejemplo, para las entradas de fecha, define la fecha aceptable más alta. |
| Aceptar | Archivo | Define los tipos de archivo permitidos. El atributo accept es una lista separada por comas de especificadores de tipo de archivo únicos que restringe los tipos de archivos que los usuarios pueden seleccionar en un campo de entrada de archivo. |
| Múltiple | Archivo | Permite selecciones múltiples. El atributo multiple es una propiedad booleana que se utiliza con los campos de entrada de archivo. Cuando se establece en true, permite a los usuarios seleccionar más de un archivo. |
| Opciones | Lista desplegable | Especifica las opciones para los menús desplegables. La propiedad options es una lista de opciones separadas por comas para los menús desplegables que define las opciones seleccionables que se muestran al usuario. |
| Comprobado | Casilla de verificación, radio | Determina si el campo está seleccionado de forma predeterminada. El atributo activado es una propiedad booleana que se utiliza con las entradas de casilla de verificación y radio. Cuando se establece en true, indica que el campo está seleccionado de forma predeterminada cuando se carga el formulario. |
| Fieldset | Todos | Agrupa campos para crear secciones visualmente distintas dentro de un formulario. El elemento fieldset agrupa los campos relacionados dentro de un formulario, separándolos visualmente para mejorar la organización y la experiencia del usuario. </br> Para organizar un conjunto de campos dentro de un fieldset, simplemente utilice la propiedad `fieldset` y especifique su atributo name. En el ejemplo siguiente, demostramos cómo se encapsulan los botones de opción dentro de un solo fieldset para mejorar la organización. ![Ejemplo de fieldset](/help/edge/assets/fieldset-example.png) |
| Repetible | Todos | Una propiedad booleana para `fieldset` indica que un fieldset en particular se puede repetir para `Min` y `Max` las veces especificadas. La propiedad `Min` debe establecerse en 1 o superior. No establezca la propiedad `Min` en 0. |
| Expresión visible | Todos | Una expresión visible hace referencia a una fórmula de hoja de cálculo, indicada por la etiqueta &quot;=&quot;, que se utiliza para controlar la visibilidad de un campo. En esta fórmula, solo se puede emplear la propiedad value de otros campos, lo que permite administrar de forma directa la visibilidad de los campos dentro del sistema. |
| Expresión de valor | Todos | Una expresión de valor hace referencia a una fórmula de hoja de cálculo, indicada por la etiqueta &quot;=&quot;, que se utiliza para controlar el valor de un campo. En esta fórmula, solo se puede utilizar la propiedad value de otros campos, lo que permite una administración directa del valor de campo dentro del sistema. |
