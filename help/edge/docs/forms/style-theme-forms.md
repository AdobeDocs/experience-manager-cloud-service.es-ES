---
title: Personalización del tema y el estilo de un formulario de servicio de entrega de AEM Forms Edge
description: Personalización del tema y el estilo de un formulario de servicio de entrega de AEM Forms Edge
feature: Edge Delivery Services
hide: true
hidefromtoc: true
source-git-commit: 4a3ebcf7985253ebca24e90ab57ae7eaf3e924e9
workflow-type: tm+mt
source-wordcount: '1285'
ht-degree: 0%

---


# Estilo de campos de formulario

Forms es crucial para la interacción de los usuarios en los sitios web, ya que les permite introducir datos. Esta guía explica los aspectos básicos del diseño de varios campos de formulario en la [Bloque de formulario](/help/edge/docs/forms/create-forms.md), lo que le ayuda a crear formularios visualmente atractivos y fáciles de usar.

## Explicación de tipos de campos de formulario

Antes de profundizar en el estilo, vamos a revisar los tipos de campos de formulario comunes admitidos por el bloque de formulario:

* Campos de entrada: Incluyen entradas de texto, entradas de correo electrónico, entradas de contraseña y mucho más.
* Grupos de casillas de verificación: se utiliza para seleccionar varias opciones.
* Grupos de radio: se utiliza para seleccionar solo una opción de un grupo.
* Desplegables: también conocidos como cuadros de selección, que se utilizan para seleccionar una opción de una lista.
* Paneles/contenedores: se utiliza para agrupar elementos de formulario relacionados.

## Principios básicos de estilo

Comprender los conceptos fundamentales de CSS es crucial antes de aplicar estilo a campos de formulario específicos:

* Selectores: los selectores de CSS permiten seleccionar elementos de HTML específicos para el estilo. Puede utilizar selectores de elementos, selectores de clases o selectores de ID.
* Propiedades: las propiedades CSS definen el aspecto visual de los elementos. Las propiedades comunes para aplicar estilo a los campos de formulario incluyen color, color de fondo, borde, relleno, margen y más.
* Modelo de cuadro: El modelo de cuadro CSS describe la estructura de los elementos del HTML como un área de contenido rodeada de relleno, bordes y márgenes.
* Flexbox/Grid: Los diseños de Flexbox y Grid CSS son herramientas potentes para crear diseños adaptables y flexibles.

## Estilo de un formulario para un bloque de formulario

El bloque de formulario ofrece una estructura de HTML estandarizada que simplifica el proceso de selección y estilo de los componentes del formulario:

* **Actualizar estilos predeterminados**: Puede modificar los estilos predeterminados de un formulario si edita la variable `/blocks/form/form.css file`. Este archivo proporciona un estilo completo para un formulario, que admite formularios de asistente de varios pasos. Hace hincapié en el uso de variables CSS personalizadas para facilitar la personalización, el mantenimiento y el estilo uniforme en todos los formularios. Para obtener instrucciones sobre cómo agregar el bloque de formulario al proyecto, consulte [creación de un formulario](/help/edge/docs/forms/create-forms.md).

* **Personalización**: utilice el valor predeterminado `forms.css` como base y personalícelo para modificar el aspecto de los componentes del formulario, lo que lo hace visualmente atractivo y fácil de usar. La estructura del archivo alienta la organización y mantiene los estilos de los formularios, lo que promueve diseños coherentes en todo el sitio web.

## Desglose de la estructura de forms.css

* **Variables globales:** Definido en el `:root` nivel, estas variables (`--variable-name`) almacene valores utilizados en toda la hoja de estilo para mantener la coherencia y facilitar las actualizaciones. Estas variables definen colores, tamaños de fuente, relleno y otras propiedades. Puede declarar sus propias variables globales o modificar las existentes para cambiar el estilo del formulario.

* **Estilos de selector universal:** El `*` El selector de coincide con todos los elementos del formulario, lo que garantiza que los estilos se apliquen a todos los componentes de forma predeterminada, incluida la configuración de `box-sizing` propiedad a `border-box`.

* **Estilo de formulario:** Esta sección se centra en el estilo de los componentes del formulario mediante selectores para dirigirse a elementos de HTML específicos. Define estilos para campos de entrada, áreas de texto, casillas de verificación, botones de opción, entradas de archivo, etiquetas de formulario y descripciones.

* **Estilo del asistente (si corresponde):** Esta sección está dedicada a aplicar estilo al diseño del asistente, un formulario de varios pasos en el que cada paso se muestra de uno en uno. Define estilos para el contenedor del asistente, conjuntos de campos, leyendas, botones de navegación y diseños adaptables.

* **Consultas de medios:** Proporcionan estilos para diferentes tamaños de pantalla, ajustando el diseño y el estilo en consecuencia.

* **Estilo variado:**: Esta sección describe los estilos para los mensajes de éxito o error, las áreas de carga de archivos y otros elementos que pueden encontrarse en un formulario.


## Estructura de componentes

El bloque de formulario ofrece una estructura de HTML coherente para varios elementos de formulario, lo que garantiza un estilo y una administración más sencillos. Puede manipular los componentes mediante CSS con fines de estilo.

### Componentes generales (excepto desplegables, grupos de opciones y grupos de casillas de verificación):

Todos los campos de formulario, excepto los desplegables, los grupos de opción y los grupos de casillas de verificación, tienen la siguiente estructura de HTML:

#### Estructura del HTML

```HTML
<div class="form-{Type}-wrapper form-{Name} field-wrapper" data-required={Required}>
  <label for="{FieldId}" class="field-label">Field Label</label>
  <input type="{Type}" placeholder="{Placeholder}" maxlength="{Max}" id="{FieldId}" name="{Name}" aria-describedby="{FieldId}-description">
  <div class="field-description" aria-live="polite" id="{FieldId}-description">
    Hint - Description of the field.
  </div>
</div>
```

* Clases: el elemento div tiene varias clases para dirigirse a elementos y estilos específicos. Necesita el `form-{Type}-wrapper` o `form-{Name}` para desarrollar un selector CSS para aplicar estilo a un campo de formulario:
   * {Type}: identifica el componente por tipo de campo. Por ejemplo, texto (form-text-wrapper), número (form-number-wrapper), fecha (form-date-wrapper).
   * {Name}: identifica el componente por su nombre. El nombre del campo solo puede tener caracteres alfanuméricos. Los múltiples guiones consecutivos del nombre se sustituyen por un solo guión `(-)`, y los guiones inicial y final del nombre de un campo se eliminarán. Por ejemplo, first-name (form-first-name field-wrapper).
   * {FieldId}: es el identificador único del campo, generado automáticamente.
   * {Required}: es un booleano que indica si el campo es obligatorio.
* Etiqueta: La `label` proporciona un texto descriptivo para el campo y lo asocia al elemento input mediante el `for` atributo.
* Entrada: El `input` define el tipo de datos que se van a introducir. Por ejemplo, texto, número, correo electrónico.
* Descripción (Opcional): La `div` con clase `field-description` proporciona información o instrucciones adicionales para el usuario.

**Ejemplo**

```HTML
<div class="form-text-wrapper form-first-name field-wrapper" data-required="true">
  <label for="firstName" class="field-label">First Name</label>
  <input type="text" placeholder="Enter your first name" maxlength="50" id="firstName" name="firstName" aria-describedby="firstName-description">
  <div class="field-description" aria-live="polite" id="firstName-description">
    Please enter your legal first name.
  </div>
</div>
```

#### Selector de CSS para componentes generales

```CSS
.form-{Type}-wrapper input {
  /* Add your styles here */
  border: 1px solid #ccc;
  padding: 8px;
  border-radius: 4px;
}


.form-{Name} input {
  /* Add your styles here */
  border: 1px solid #ccc;
  padding: 8px;
  border-radius: 4px;
}
```

* `.form-{Type}-wrapper`: segmenta el `div` basado en el tipo de campo. Por ejemplo, `.form-text-wrapper` selecciona todos los campos de entrada de texto.
* `.form-{Name}`: selecciona además el elemento en función del nombre de campo específico. Por ejemplo, `.form-first-name` se dirige al campo de texto &quot;Nombre&quot;.

**Ejemplo:**

```CSS
/*Target all text input fields */

.form-text-wrapper input {
  border: 1px solid #ccc;
  padding: 8px;
  border-radius: 4px;
}

/*Target all fields with name first-name*/

.form-first-name input {
  border: 1px solid #ccc;
  padding: 8px;
  border-radius: 4px;
}
```


### Componente desplegable

Para los menús desplegables, la variable `select` se utiliza en lugar de un `input` elemento:


#### Estructura del HTML

```HTML
<div class="form-drop-down-wrapper form-{Name} field-wrapper" data-required={required}>
  <label for="{FieldId}" class="field-label">First Name</label>
  <select id="{FieldId}" name="{Name}"><option></option><option></option></select>
  <div class="field-description" aria-live="polite" id="{FieldId}-description">
    Hint - First name should be minimum 3 characters and a maximum of 10 characters.
  </div>
</div>
```

**Ejemplo**

```HTML
    <div class="form-drop-down-wrapper form-country field-wrapper" data-required="true">
      <label for="country" class="field-label">Country</label>
      <select id="country" name="country">
         <option value="">Select Country</option>
         <option value="US">United States</option>
         <option value="CA">Canada</option>
    </select>
   <div class="field-description" aria-live="polite" id="country-description">Please select your country of residence.</div>
   </div>
```

#### Selectores CSS para el componente desplegable

```CSS
/* Target the outer wrapper */
.form-drop-down-wrapper {
  /* Add your styles here */
  display: flex;
  flex-direction: column;
  margin-bottom: 15px;
}

/* Style the label */
.form-drop-down-wrapper .field-label {
  margin-bottom: 5px;
  font-weight: bold;
}

/* Style the dropdown itself */
.form-drop-down-wrapper select {
  border: 1px solid #ccc;
  padding: 8px;
  border-radius: 4px;
  background-color: white; /* Ensure a consistent background */
  /* Adjust arrow appearance as needed */
  -webkit-appearance: none;
  -moz-appearance: none;
  appearance: none;
}

/* Optional: Style the dropdown arrow */
.form-drop-down-wrapper select::-ms-expand {
  display: none; /* Hide the default arrow for IE11 */
}

.form-drop-down-wrapper select::after {
  content: "\25BC";
  font-size: 12px;
  color: #ccc;
  /* Adjust positioning as needed */
  position: absolute;
  right: 10px;
  top: 50%;
  transform: translateY(-50%);
}
```

* Oriente el envoltorio: el primer selector (`.form-drop-down-wrapper`) tiene como destino el elemento envolvente exterior, lo que garantiza que los estilos se apliquen a todo el componente desplegable.
* Diseño de la Estructura: La Estructura organiza la etiqueta, la lista desplegable y la descripción verticalmente para conseguir un diseño limpio.
* Estilo de etiqueta: La etiqueta destaca por su grosor de fuente más negrita y un ligero margen.
* Estilo desplegable: el elemento seleccionado recibe un borde, un relleno y esquinas redondeadas para lograr un aspecto pulido.
* Color de fondo: se establece un color de fondo coherente para una armonía visual.
* Personalización de flechas: los estilos opcionales ocultan la flecha desplegable predeterminada y crean una flecha personalizada utilizando un carácter Unicode y una posición determinada.

### Grupos de radio y casilla de verificación

De forma similar a los componentes desplegables, los grupos de radio y casilla de verificación tienen su propia estructura de HTML y consideraciones CSS:

#### Estructura del HTML del grupo de radio

```HTML
<div class="form-checkbox-group-wrapper form-{Name} field-wrapper" data-required={required}>
  <label class="field-label">{Label Text}</label>
  <div class="checkbox-group">
    <input type="checkbox" id="{FieldId}-1" name="{Name}" value="{Value1}">
    <label for="{FieldId}-1">{Option 1 Text}</label>
    <input type="checkbox" id="{FieldId}-2" name="{Name}" value="{Value2}">
    <label for="{FieldId}-2">{Option 2 Text}</label>
    </div>
  <div class="field-description" aria-live="polite" id="{FieldId}-description">
    Hint - Select multiple options (if applicable).
  </div>
</div>
```


#### Estructura del HTML del grupo de radio

```HTML
<div class="form-checkbox-group-wrapper form-{Name} field-wrapper" data-required={required}>
  <label class="field-label">{Label Text}</label>
  <div class="checkbox-group">
    <input type="checkbox" id="{FieldId}-1" name="{Name}" value="{Value1}">
    <label for="{FieldId}-1">{Option 1 Text}</label>
    <input type="checkbox" id="{FieldId}-2" name="{Name}" value="{Value2}">
    <label for="{FieldId}-2">{Option 2 Text}</label>
    </div>
  <div class="field-description" aria-live="polite" id="{FieldId}-description">
    Hint - Select multiple options (if applicable).
  </div>
</div>
```

#### Selectores CSS para grupos de radio y casillas de verificación

**Segmentación del envoltorio exterior**


```CSS
   /* Targets all radio group wrappers */
.form-radio-group-wrapper {
  margin-bottom: 20px; /* Adds space between radio groups */
}

/* Targets all checkbox group wrappers */
.form-checkbox-group-wrapper {
  margin-bottom: 20px; /* Adds space between checkbox groups */
}
```

Estos selectores se dirigen a los contenedores más externos de los grupos de radio y casilla de verificación, lo que permite aplicar estilos generales a toda la estructura del grupo. Esto resulta útil para establecer el espaciado, la alineación u otras propiedades relacionadas con el diseño.

**Etiquetas de grupo de destino**

```CSS
.form-radio-group-wrapper .field-label,
.form-checkbox-group-wrapper .field-label {
 font-weight: bold; /* Makes the group label bold */
}
```

Este selector se dirige a `.field-label` dentro de los contenedores de grupo de casilla de verificación y radio. Esto le permite aplicar estilo a las etiquetas específicamente para estos grupos, lo que podría hacerlos destacar más.

**Segmentación de entradas y etiquetas individuales**

```CSS
/* Styling radio buttons */
.form-radio-group-wrapper input[type="radio"] {
  margin-right: 5px; /* Adds space between the input and its label */
} 

/* Styling radio button labels */
.form-radio-group-wrapper label {
  font-size: 15px; /* Changes the label font size */
}

/* Styling checkboxes */
.form-checkbox-group-wrapper input[type="checkbox"] {
  margin-right: 5px;  /* Adds space between the input and its label */ 
}

/* Styling checkbox labels */
.form-checkbox-group-wrapper label {
  font-size: 15px; /* Changes the label font size */
}
```

Estos selectores proporcionan un control más granular sobre los botones de opción individuales, las casillas de verificación y sus etiquetas asociadas. Puede utilizarlas para ajustar el tamaño, el espaciado o aplicar estilos visuales más distintos.


**Personalizar el aspecto de los botones de opción y las casillas de verificación**

```CSS
/* Hide the default radio button or checkbox */
.form-radio-group-wrapper input[type="radio"],
.form-checkbox-group-wrapper input[type="checkbox"] {
  opacity: 0; 
  position: absolute; 
}

/* Create a custom radio button */
.form-radio-group-wrapper input[type="radio"] + label::before { 
  content: "";
  display: inline-block;
  width: 16px; 
  height: 16px; 
  border: 2px solid #ccc; 
  border-radius: 50%;
  margin-right: 5px;
}

.form-radio-group-wrapper input[type="radio"]:checked + label::before {
  background-color: #007bff; 
}

/* Create a custom checkbox */
/* Similar styling as above, with adjustments for a square shape */
```

Esta técnica oculta la entrada predeterminada y utiliza los pseudoelementos :before y :after para crear imágenes personalizadas que cambian de aspecto en función del estado &quot;activado&quot;.


## Estilo de campos

Además de las técnicas de estilo generales tratadas anteriormente, también puede aplicar estilo a los campos de formulario en función de su tipo específico o nombres individuales. Esto permite un control y una personalización más granulares del aspecto del formulario.

### Estilo basado en el tipo de campo

Puede utilizar selectores de CSS para segmentar tipos de campo específicos y aplicar estilos de forma coherente.

**Ejemplo de estructura del HTML**

```HTML
<div class="form-text-wrapper form-name field-wrapper" data-required="true">
  <label for="name" class="field-label">Name</label>
  <input type="text" placeholder="Enter your name" maxlength="50" id="name" name="name">
</div>

<div class="form-number-wrapper form-age field-wrapper" data-required="true">
  <label for="age" class="field-label">Age</label>
  <input type="number" placeholder="Enter your age" id="age" name="age">
</div>

<div class="form-email-wrapper form-email field-wrapper" data-required="true">
  <label for="email" class="field-label">Email Address</label>
  <input type="email" placeholder="Enter your email" id="email" name="email">
</div>
```

* Cada campo está envuelto en una `div` elemento con varias clases:
   * `form-{Type}-wrapper`: Identifica el tipo de campo. Por ejemplo, `form-text-wrapper`, `form-number-wrapper`, `form-email-wrapper`.
   * `form-{Name}`: Identifica el campo por su nombre. Por ejemplo `form-name`, `form-age`, `form-email`.
   * `field-wrapper`: una clase genérica para todos los contenedores de campo.
* El `data-required` El atributo indica si el campo es obligatorio u opcional.
* Cada campo tiene una etiqueta correspondiente, un elemento de entrada y posibles elementos adicionales como marcadores de posición y descripciones.

Por ejemplo:

```CSS
/* Target all text input fields */
.form-text-wrapper input {
  /* Add your styles here */
}

/* Target all number input fields */
.form-number-wrapper input {
  /* Add your styles here */
  letter-spacing: 2px; /* Example for adding letter spacing to all number fields */
}
```

### Estilo de tipos de campo específicos

También puede segmentar campos individuales por nombre para aplicar estilos únicos.

**Ejemplo de estructura del HTML**

```HTML
<div class="form-number-wrapper form-otp field-wrapper" data-required="true">
  <label for="otp" class="field-label">OTP</label>
  <input type="number" placeholder="Enter your OTP" maxlength="6" id="otp" name="otp">
</div>
```

**Selector de CSS**

```CSS
.form-otp input {
   letter-spacing: 2px
}
```

* Selector: este CSS se dirige a todos los elementos de entrada ubicados dentro de un elemento que tiene la clase `form-otp`. La estructura del HTML sigue las convenciones del bloque de formulario, lo que implica que hay un contenedor marcado con la clase &quot;form-top&quot; que contiene el campo con el nombre &quot;otp&quot;.

* Propiedad y valor: se aplica el código `letter-spacing: 2px`. Esta propiedad CSS controla el espaciado entre letras individuales dentro del contenido de texto del campo de entrada.