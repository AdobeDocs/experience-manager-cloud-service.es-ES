---
title: Personalice el tema y el estilo de Edge Delivery Services para AEM Forms
description: Personalice el tema y el estilo de Edge Delivery Services para AEM Forms
feature: Edge Delivery Services
exl-id: c214711c-979b-4833-9541-8e35b2aa8e09
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '1901'
ht-degree: 100%

---


# Personalización del aspecto de los formularios

Los formularios son esenciales para la interacción de los usuarios en los sitios web, ya que les permite introducir datos. Puede utilizar Hojas de estilo en cascada (CSS) para aplicar estilo a los campos de un formulario, mejorar la presentación visual de los formularios y mejorar la experiencia del usuario.

El bloque de formularios adaptables produce una estructura coherente para todos los campos de formulario. La estructura coherente facilita el desarrollo de selectores CSS para seleccionar y aplicar estilo a los campos de formulario en función del tipo de campo y de los nombres de campo.

Este documento describe la estructura del HTML para varios componentes de formulario y le ayuda a comprender cómo crear selectores CSS para varios campos de formulario y aplicar estilo a los campos de formulario de un bloque de formularios adaptables.

Al final de este artículo, podrá hacer lo siguiente:

- Comprender la estructura del archivo CSS predeterminado incluido con el bloque de formularios adaptables.
- Comprender la estructura de HTML de los componentes de formulario que proporciona el bloque de formularios adaptables, incluidos los componentes generales y específicos como los menús desplegables, los grupos de opción y los grupos de casillas de verificación.
- Aprenderá a aplicar estilo a los campos de formulario en función del tipo de campo y los nombres de campo mediante selectores CSS, lo que permitirá aplicar un estilo coherente o único en función de los requisitos.


## Explicación de los tipos de campo de formulario

Antes de sumergirse en el estilo, vamos a revisar los [tipos de campo](/help/edge/docs/forms/form-components.md) del formulario común compatibles con el Bloque de formularios adaptables:

- Campos de entrada: incluyen entradas de texto, entradas de correo electrónico, entradas de contraseña y mucho más.
- Grupos de casillas de verificación: se utilizan para seleccionar varias opciones.
- Grupos de opción: se utilizan para seleccionar solo una opción de un grupo.
- Menús desplegables: también conocidos como casillas de selección, que se utilizan para seleccionar una opción de una lista.
- Paneles/contenedores: se utilizan para agrupar elementos de formulario relacionados.

## Principios básicos de estilo

Entender los [conceptos fundamentales de CSS](https://www.w3schools.com/css/css_intro.asp) es esencial antes de aplicar estilo a campos de formulario específicos:

- [Selectores](https://www.w3schools.com/css/css_selectors.asp): los selectores CSS permiten aplicar estilos a elementos HTML específicos. Puede utilizar selectores de elementos, selectores de clases o selectores de ID.
- [Propiedades](https://www.w3schools.com/css/css_syntax.asp): las propiedades CSS definen el aspecto visual de los elementos. Las propiedades comunes para aplicar estilo a los campos de formulario incluyen color, color de fondo, borde, relleno, margen y más.
- [Modelo de cuadro](https://www.w3schools.com/css/css_boxmodel.asp): el modelo de cuadro CSS describe la estructura de los elementos HTML como un área de contenido rodeada de relleno, bordes y márgenes.
- Caja flexible/cuadrícula: la [caja flexible](https://www.w3schools.com/css/css3_flexbox.asp) y los [diseños de cuadrícula](https://www.w3schools.com/css/css_grid.asp) CSS son herramientas potentes para crear diseños adaptables y flexibles.

## Estilo de un formulario para un Bloque de formularios adaptables

El Bloque de formularios adaptables ofrece una estructura de HTML estandarizada que simplifica el proceso de selección y estilo de los componentes del formulario:

- **Actualizar estilos predeterminados**: puede modificar los estilos predeterminados de un formulario editando el archivo `/blocks/form/form.css`. Este archivo proporciona un estilo completo para un formulario, que admite formularios de asistente de varios pasos. Hace hincapié en el uso de variables CSS personalizadas para facilitar la personalización, el mantenimiento y el estilo uniforme en todos los formularios. Para obtener instrucciones sobre cómo añadir el Bloque de formularios adaptables al proyecto, consulte [creación de un formulario](/help/edge/docs/forms/create-forms.md).

- **Personalización**: utilice el valor predeterminado `forms.css` como base y personalícelo para modificar la apariencia de los componentes del formulario, de modo que sean visualmente atractivos y fáciles de usar. La estructura del archivo fomenta la organización y mantiene los estilos de los formularios, lo que promueve diseños coherentes en todo su sitio web.

## Desglose de la estructura forms.css

- **Variables globales:** definidas en el nivel `:root`, estas variables (`--variable-name`) almacenan los valores utilizados en toda la hoja de estilo para mantener la coherencia y facilitar las actualizaciones. Estas variables definen colores, tamaños de fuente, relleno y otras propiedades. Puede declarar sus propias variables globales o modificar las existentes para cambiar el estilo del formulario.

- **Estilos de selector universal:** el selector `*` coincide con todos los elementos del formulario, lo que garantiza que los estilos se apliquen a todos los componentes de forma predeterminada, incluida la configuración de la propiedad `box-sizing` en `border-box`.

- **Estilo de formulario:** esta sección se centra en el estilo de los componentes del formulario mediante selectores que apunten a elementos HTML específicos. Define estilos para campos de entrada, áreas de texto, casillas de verificación, botones de opción, entradas de archivo, etiquetas de formulario y descripciones.

- **Estilo del asistente (si corresponde):** esta sección está dedicada a aplicar estilo al diseño del asistente, un formulario de varios pasos en el que cada paso se muestra de uno en uno. Define estilos para el contenedor del asistente, conjuntos de campos, leyendas, botones de navegación y diseños adaptables.

- **Consultas de medios:** proporcionan estilos para diferentes tamaños de pantalla, ajustando el diseño y el estilo en consecuencia.

- **Estilo variado:** esta sección describe los estilos para los mensajes de éxito o error, las áreas de carga de archivos y otros elementos que pueden encontrarse en un formulario.


## Estructura de componentes

El bloque de formularios adaptables ofrece una estructura HTML coherente para varios elementos de formulario, lo que garantiza una gestión y un estilo más sencillos. Puede modificar los componentes mediante CSS con fines de estilo.

### Componentes generales (excepto menús desplegables, grupos de opciones y grupos de casillas de verificación):

Todos los campos de formulario, excepto los menús desplegables, los grupos de opción y los grupos de casillas de verificación, tienen la siguiente estructura HTML:

+++ Estructura HTML de los componentes generales

```HTML
<div class="{Type}-wrapper field-{Name} field-wrapper" data-required={Required}>
   <label for="{FieldId}" class="field-label">First Name</label>
   <input type="{Type}" placeholder="{Placeholder}" maxlength="{Max}" id="{FieldId}" name="{Name}" aria-describedby="{FieldId}-description">
   <div class="field-description" aria-live="polite" id="{FieldId}-description">
    Hint - First name should be a minimum of 3 characters and a maximum of 10 characters.
   </div>
</div>
```

- Clases: el elemento div tiene varias clases para segmentar elementos y estilos específicos. Necesita las clases `{Type}-wrapper` o `field-{Name}` para desarrollar un selector de CSS para aplicar estilo a un campo de formulario:
   - {Type}: identifica el componente por el tipo de campo. Por ejemplo, texto (text-wrapper), número (number-wrapper) o fecha (date-wrapper).
   - {Name}: identifica el componente por su nombre. El nombre del campo solo puede tener caracteres alfanuméricos. Los guiones múltiples consecutivos del nombre se sustituyen por un solo guion `(-)`, y los guiones iniciales y finales del nombre de un campo se eliminan. Por ejemplo: first-name (field-first-name field-wrapper).
   - {FieldId}: es un identificador único para el campo, se genera automáticamente.
   - {Required}: es un valor booleano que indica si el campo es obligatorio.
- Etiqueta: el elemento `label` proporciona un texto descriptivo para el campo y lo asocia al elemento de entrada mediante el atributo `for`.
- Entrada: el elemento `input` define el tipo de datos que se van a introducir. Por ejemplo, texto, número o correo electrónico.
- Descripción (opcional): el elemento `div` con clase `field-description` proporciona información o instrucciones adicionales para el usuario.

**Ejemplo de estructura HTML**

```HTML
<div class="text-wrapper field-first-name field-wrapper" data-required="true">
  <label for="firstName" class="field-label">First Name</label>
  <input type="text" placeholder="Enter your first name" maxlength="50" id="firstName" name="firstName" aria-describedby="firstName-description">
  <div class="field-description" aria-live="polite" id="firstName-description">
    Please enter your legal first name.
  </div>
</div>
```

+++

+++ Selector de CSS para componentes generales

```CSS
/* Target all input fields within any .{Type}-wrapper */
.{Type}-wrapper {
  /* Add your styles here */
  border: 1px solid #ccc;
  padding: 8px;
  border-radius: 4px;
}

/* Target all input fields within any .{Type}-wrapper */
.{Type}-wrapper input {
  /* Add your styles here */
  border: 1px solid #ccc;
  padding: 8px;
  border-radius: 4px;
}

/* Target any element with the class field-{Name} */
.field-{Name} {
  /* Add your styles here */
  /* This could be used for styles specific to all elements with field-{Name} class, not just inputs */
}
```

- `.{Type}-wrapper`: selecciona el elemento `div` exterior basado en el tipo de campo. Por ejemplo, `.text-wrapper` selecciona todos los campos de texto.
- `.field-{Name}`: selecciona además el elemento en función del nombre de campo específico. Por ejemplo, `.field-first-name` se dirige al campo de texto “Nombre”. Aunque este selector se puede utilizar para elementos de segmentación con la clase field-{Name}, es importante actuar con precaución. En este caso específico, no sería útil para aplicar estilo a los campos de entrada porque se dirigiría no solo a la entrada en sí, sino también a los elementos de etiqueta y descripción. Se recomienda utilizar selectores más específicos como los que tiene para los campos de entrada de texto (entrada .text-wrapper).

**Ejemplo de selectores CSS para componentes generales**

```CSS
/* Target all text input fields */
.text-wrapper input {
  border: 1px solid #ccc;
  padding: 8px;
  border-radius: 4px;
}

/* Target all fields with name first-name */
.field-first-name input {
  border: 1px solid #ccc;
  padding: 8px;
  border-radius: 4px;
}
```

+++

### Componente desplegable

Para los menús desplegables, se utiliza el elemento `select` en lugar de un elemento `input`:

+++ Estructura HTML del componente desplegable

```HTML
<div class="{Type}-wrapper field-{Name} field-wrapper" data-required={Required}>
   <label for="{FieldId}" class="field-label">Country</label>
   <select id="{FieldId}" name="{Name}"><option></option><option></option></select>
   <div class="field-description" aria-live="polite" id="{FieldId}-description">
    Please select your country from the list.
   </div>
</div>
```

**Ejemplo de estructura HTML**

```HTML
<div class="drop-down-wrapper field-country field-wrapper" data-required="true">
  <label for="country" class="field-label">Country</label>
  <select id="country" name="country">
    <option value="">Select Country</option>
    <option value="US">United States</option>
    <option value="CA">Canada</option>
  </select>
  <div class="field-description" aria-live="polite" id="country-description">
    Please select your country of residence.
  </div>
</div>
```

+++

+++ Selectores CSS para componentes desplegables

```CSS
/* Target the outer wrapper */
.drop-down-wrapper {
  /* Add your styles here */
  display: flex;
  flex-direction: column;
  margin-bottom: 15px;
}

/* Style the label */
.drop-down-wrapper .field-label {
  margin-bottom: 5px;
  font-weight: bold;
}

/* Style the dropdown itself */
.drop-down-wrapper select {
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
.drop-down-wrapper select::-ms-expand {
  display: none; /* Hide the default arrow for IE11 */
}

.drop-down-wrapper select::after {
  content: "\25BC";
}
```

+++

### Grupos de radio

Al igual que los componentes desplegables, los grupos de radio tienen su propia estructura HTML y estructura CSS:

+++ Estructura HTML del grupo de radio 

```HTML
<fieldset class="radio-group-wrapper field-{Name} field-wrapper" id="{FieldId}" name="{Name}" data-required="{Required}">
   <legend for="{FieldId}" class="field-label">....</legend>
   <% for each radio in Group %>
   <div class="radio-wrapper field-{Name}">
      <input type="radio" value="" id="{UniqueId}" data-field-type="radio-group" name="{FieldId}">
      <label for="{UniqueId}" class="field-label">...</label>
   </div>
   <% end for %>
</fieldset>
```

#### Ejemplo de estructura HTML

```HTML
<fieldset class="radio-group-wrapper field-color field-wrapper" id="color_preference" name="color_preference" data-required="true">
  <legend for="color_preference" class="field-label">Favorite Color:</legend>
  <% for each radio in Group %>
    <div class="radio-wrapper field-color">
      <input type="radio" value="red" id="color_red" data-field-type="radio-group" name="color_preference">
      <label for="color_red" class="field-label">Red</label>
    </div>
    <div class="radio-wrapper field-color">
      <input type="radio" value="green" id="color_green" data-field-type="radio-group" name="color_preference">
      <label for="color_green" class="field-label">Green</label>
    </div>
    <div class="radio-wrapper field-color">
      <input type="radio" value="blue" id="color_blue" data-field-type="radio-group" name="color_preference">
      <label for="color_blue" class="field-label">Blue</label>
    </div>
  <% end for %>
</fieldset>
```

+++

+++ Selectores CSS para grupos de radio

- Segmentación del Fieldset

```CSS
  .radio-group-wrapper {
    border: 1px solid #ccc;
    padding: 10px;
  }
```

Este selector se dirige a cualquier fieldset con la clase radio-group-wrapper. Esto sería útil para aplicar estilos generales a todo el grupo de radio.

- Segmentación de etiquetas de botones de radio

```CSS
.radio-wrapper label {
    font-weight: normal;
    margin-right: 10px;
  }
```

- Segmente todas las etiquetas de botones de radio de un fieldset específico en función de su nombre

```CSS
.field-color .radio-wrapper label {
  /* Your styles here */
}
```

+++ 

### Grupos de casillas de verificación

+++ Estructura HTML del grupo de casillas de verificación 

```HTML
<fieldset class="checkbox-group-wrapper field-{Name} field-wrapper" id="{FieldId}" name="{Name}" data-required="{Required}">
   <legend for="{FieldId}" class="field-label">....</legend>
   <% for each radio in Group %>
   <div class="radio-wrapper field-{Name}">
      <input type="checkbox" value="" id="{UniqueId}" data-field-type="checkbox-group" name="{FieldId}">
      <label for="{UniqueId}" class="field-label">...</label>
   </div>
   <% end for %>
</fieldset>
```

#### Ejemplo de estructura HTML

```HTML
<fieldset class="checkbox-group-wrapper field-topping field-wrapper" id="topping_preference" name="topping_preference" data-required="false">
  <legend for="topping_preference" class="field-label">Pizza Toppings:</legend>
  <div class="checkbox-wrapper field-topping">
    <input type="checkbox" value="pepperoni" id="topping_pepperoni" data-field-type="checkbox-group" name="topping_preference">
    <label for="topping_pepperoni" class="field-label">Pepperoni</label>
  </div>
  <div class="checkbox-wrapper field-topping">
    <input type="checkbox" value="mushrooms" id="topping_mushrooms" data-field-type="checkbox-group" name="topping_preference">
    <label for="topping_mushrooms" class="field-label">Mushrooms</label>
  </div>
  <div class="checkbox-wrapper field-topping">
    <input type="checkbox" value="onions" id="topping_onions" data-field-type="checkbox-group" name="topping_preference">
    <label for="topping_onions" class="field-label">Onions</label>
  </div>
</fieldset>
```

+++

+++ Selectores CSS para grupos de casillas de verificación

- Segmentación del contenedor exterior: estos selectores se dirigen a los contenedores más externos de los grupos de radio y de la casilla de verificación, lo que permite aplicar estilos generales a toda la estructura del grupo. Esto resulta útil para establecer el espaciado, la alineación u otras propiedades relacionadas con el diseño.


  ```CSS
     /* Targets radio group wrappers */
       .radio-group-wrapper {
       margin-bottom: 20px; /* Adds space between radio groups */  
     }
  
     /* Targets checkbox group wrappers */
     .checkbox-group-wrapper {
     margin-bottom: 20px; /* Adds space between checkbox groups */
     }
  ```


- Etiquetas de grupos de segmentación: este selector se dirige al elemento `.field-label` dentro de los contenedores de grupo de casilla de verificación y radio. Esto le permite aplicar estilo a las etiquetas específicamente para estos grupos, lo que podría hacerlas destacar más.

  ```CSS
   .radio-group-wrapper legend,
   .checkbox-group-wrapper legend {
     font-weight: bold; /* Makes the group label bold */
   }
  ```



- Segmentación de entradas y etiquetas individuales: estos selectores proporcionan un control más granular sobre los botones de opción individuales, casillas de verificación y sus etiquetas asociadas. Puede utilizarlos para ajustar el tamaño, el espaciado o aplicar estilos visuales más distintos.

  ```CSS
  /* Styling radio buttons */
   .radio-group-wrapper input[type="radio"] {
     margin-right: 5px; /* Adds space between the input and its label */
   }
  
   /* Styling radio button labels */
   .radio-group-wrapper label {
     font-size: 15px; /* Changes the label font size */
   }
  
  /* Styling checkboxes */
   .checkbox-group-wrapper input[type="checkbox"] {
     margin-right: 5px; /* Adds space between the input and its label */
   }
  
   /* Styling checkbox labels */
   .checkbox-group-wrapper label {
     font-size: 15px; /* Changes the label font size */
   }
  ```




- Personalización del aspecto de los botones de opción y las casillas de verificación: esta técnica oculta la entrada predeterminada y utiliza los pseudoelementos `:before` y `:after` para crear imágenes personalizadas que cambian de aspecto en función del estado “activado”.

  ```CSS
  /* Hide the default radio button or checkbox */
     .radio-group-wrapper input[type="radio"],
     .checkbox-group-wrapper input[type="checkbox"] {
       opacity: 0;
       position: absolute;
     }
  
     /* Create a custom radio button */
     .radio-group-wrapper input[type="radio"] + label::before {
       /* ... styles for custom radio button ... */
     }
  
     .radio-group-wrapper input[type="radio"]:checked + label::before {
       /* ... styles for checked radio button ... */
     }
  
     /* Create a custom checkbox */
     /* Similar styling as above, with adjustments for a square shape  */
     .checkbox-group-wrapper input[type="checkbox"] + label::before {
       /* ... styles for custom checkbox ... */
     }
  
     .checkbox-group-wrapper input[type="checkbox"]:checked + label::before {
       /* ... styles for checked checkbox ... */
     }
  ```

+++ 

### Componentes de panel/contenedor

+++ Estructura HTML de los componentes de panel/contenedor

```HTML
<fieldset class="panel-wrapper field-{PanelName} field-wrapper">
  <legend for="{id}" class="field-label" data-visible="false">bannerComponent</legend>
  <div class="{Type}-wrapper field-{Name} field-wrapper">
    <label for="{FieldId}" class="field-label">First Name</label>
    <input type="{Type}" placeholder="{Placeholder}" maxlength="{Max}" id={FieldId}" name="{Name}">
    <div class="field-description" aria-live="polite" id="{FieldId}-description">
      Hint - First name should be minimum 3 characters and a maximum of 10 characters.
    </div>
  </div>
</fieldset>
```

**Ejemplo de estructura HTML**

```HTML
<fieldset class="panel-wrapper field-login field-wrapper">
  <legend for="login" class="field-label" data-visible="false">Login Information</legend>
  <div class="text-wrapper field-username field-wrapper">
    <label for="username" class="field-label">Username</label>
    <input type="text" placeholder="Enter your username" maxlength="50" id="username" name="username">
    <div class="field-description" aria-live="polite" id="username-description">
      Please enter your username or email address.
    </div>
  </div>
  <div class="password-wrapper field-password field-wrapper">
    <label for="password" class="field-label">Password</label>
    <input type="password" placeholder="Enter your password" maxlength="20" id="password" name="password">
    <div class="field-description" aria-live="polite" id="password-description">
      Your password must be at least 8 characters long.
    </div>
  </div>
</fieldset>
```

- El elemento fieldset actúa como contenedor de panel con la clase panel-wrapper y clases adicionales para el estilo basadas en el nombre del panel (field-login).
- El elemento de leyenda (`<legend>`) sirve como título del panel con el texto “Información de inicio de sesión” y la etiqueta de campo de clase. El atributo data-visible=“false” se puede utilizar con JavaScript para controlar la visibilidad del título.
- Dentro del fieldset, varios.Los elementos {Type}-wrapper (.text-wrapper y .password-wrapper en este caso) representan campos de formulario individuales dentro del panel.
- Cada contenedor contiene una etiqueta, un campo de entrada y una descripción, similares a los ejemplos anteriores.

+++ 

+++ Ejemplo de selectores CSS para componentes de panel/contenedor

1. Segmentación del panel:

```CSS
  /* Target the entire panel container */
  .panel-wrapper {
    /* Add your styles here (e.g., border, padding, background color) */
    border: 1px solid #ccc;
    padding: 15px;
    border-radius: 4px;
    margin-bottom: 20px;
 }
```

- El selector `.panel-wrapper` aplica estilo a todos los elementos con el contenedor de paneles de clase, lo que proporciona un aspecto coherente a todos los paneles.

1. Segmentación del título del panel:

```CSS
  /* Target the legend element (panel title) */
  .panel-wrapper legend {
    /* Add your styles here (e.g., font-weight, font-size) */
    font-weight: bold;
    font-size: 16px;
    padding-bottom: 5px;
    margin-bottom: 10px;
    border-bottom: 1px solid #ddd; /* Optional: create a separation line */
  }
```

- El selector `.panel-wrapper legend` aplica estilos al elemento de leyenda del panel, lo que hace que el título se destaque visualmente.


1. Segmentación de campos individuales dentro del panel:

```CSS
/* Target all form field wrappers within a panel */
.panel-wrapper .{Type}-wrapper {
  /* Add your styles here (e.g., margin) */
  margin-bottom: 10px;
}
```

- El selector `.panel-wrapper .{Type}-wrapper` se dirige a todos los contenedores con la clase `.{Type}-wrapper` dentro del panel, lo que le permite aplicar estilo al espaciado entre los campos del formulario.

1. Segmentación de campos específicos (opcional):

```CSS
  /* Target the username field wrapper */
  .panel-wrapper .text-wrapper.field-username {
    /* Add your styles here (specific to username field) */
  }

  /* Target the password field wrapper */
  .panel-wrapper .password-wrapper.field-password {
    /* Add your styles here (specific to password field) */
  }
```

- Estos selectores opcionales le permiten segmentar contenedores de campo específicos dentro del panel para aplicar un estilo único, como resaltar el campo de nombre de usuario.

+++

### Panel repetible

+++ Estructura HTML de un panel repetible

```HTML
<fieldset class="panel-wrapper field-{PanelName} field-wrapper">
  <legend for="{id}" class="field-label" data-visible="false">bannerComponent</legend>
  <div class="{Type}-wrapper field-{Name} field-wrapper">
    <label for="{FieldId}" class="field-label">First Name</label>
    <input type="{Type}" placeholder="{Placeholder}" maxlength="{Max}" id={FieldId}" name="{Name}">
    <div class="field-description" aria-live="polite" id="{FieldId}-description">
      Hint - First name should be minimum 3 characters and a maximum of 10 characters.
    </div>
</fieldset>
```

**Ejemplo de estructura HTML**

```HTML
<fieldset class="panel-wrapper field-contact field-wrapper" data-repeatable="true">
  <legend for="contact-1" class="field-label" data-visible="false">Contact Information</legend>
  <div class="text-wrapper field-name field-wrapper">
    <label for="name-1" class="field-label">Name</label>
    <input type="text" placeholder="Enter your name" maxlength="50" id="name-1" name="contacts[0].name">
    <div class="field-description" aria-live="polite" id="name-1-description">
      Please enter your full name.
    </div>
  </div>
  <div class="email-wrapper field-email field-wrapper">
    <label for="email-1" class="field-label">Email</label>
    <input type="email" placeholder="Enter your email address" maxlength="100" id="email-1" name="contacts[0].email">
    <div class="field-description" aria-live="polite" id="email-1-description">
      Please enter a valid email address.
    </div>
  </div>
</fieldset>

<fieldset class="panel-wrapper field-contact field-wrapper" data-repeatable="true">
  <legend for="contact-2" class="field-label" data-visible="false">Contact Information</legend>
  <div class="text-wrapper field-name field-wrapper">
    <label for="name-2" class="field-label">Name</label>
    <input type="text" placeholder="Enter your name" maxlength="50" id="name-2" name="contacts[1].name">
    <div class="field-description" aria-live="polite" id="name-2-description">
      Please enter your full name.
    </div>
  </div>
  <div class="email-wrapper field-email field-wrapper">
    <label for="email-2" class="field-label">Email</label>
    <input type="email" placeholder="Enter your email address" maxlength="100" id="email-2" name="contacts[1].email">
    <div class="field-description" aria-live="polite" id="email-2-description">
      Please enter a valid email address.
    </div>
  </div>
</fieldset>
```

Cada panel tiene la misma estructura que el ejemplo del panel único, con atributos adicionales:

- data-repeatable=&quot;true&quot;: este atributo indica que el panel se puede repetir dinámicamente mediante JavaScript o un marco de trabajo.

- ID y nombres únicos: cada elemento del panel tiene un ID único (por ejemplo, name-1, email-1) y un atributo de nombre basado en el índice del panel (por ejemplo, name=&quot;contacts[0].name&quot;). Esto permite una recopilación de datos adecuada cuando se envían varios paneles.

+++ 

+++ Selectores CSS para un panel repetible

- Segmentación de todos los paneles repetibles:

```CSS
  /* Target all panels with the repeatable attribute */
  .panel-wrapper[data-repeatable="true"] {
    /* Add your styles here (e.g., border, margin) */
    border: 1px solid #ccc;
    padding: 15px;
    border-radius: 4px;
    margin-bottom: 20px;
  }
```

El selector aplica estilo a todos los paneles que se pueden repetir, lo que garantiza una apariencia uniforme.


- Segmentación de campos individuales dentro de un panel:

```CSS
/* Target all form field wrappers within a repeatable panel */
.panel-wrapper[data-repeatable="true"] .{Type}-wrapper {
  /* Add your styles here (e.g., margin) */
  margin-bottom: 10px;
}
```

Este selector aplica estilo a todos los contenedores de campo dentro de un panel repetible, manteniendo un espaciado coherente entre los campos.

- Segmentación de campos específicos (dentro de un panel):

```CSS
/* Target the name field wrapper within the first panel */
.panel-wrapper[data-repeatable="true"][data-index="0"] .text-wrapper.field-name {
  /* Add your styles here (specific to first name field) */
}

/* Target all
```

+++

### Adjuntar archivos

+++ Estructura HTML para adjuntar archivos 

```HTML
<div class="file-wrapper field-{FileName} field-wrapper">
  <legend for="{id}" class="field-label" data-visible="false"> File Attachment </legend>
  <div class="file-drag-area">
    <div class="file-dragIcon"></div>
    <div class="file-dragText">Drag and Drop To Upload</div>
    <button class="file-attachButton" type="button">Attach</button>
    <input type="file" accept="audio/*, video/*, image/*, text/*, application/pdf" id="{id}" name="{FileName}" autocomplete="off" multiple="" required="required">
  </div>
  <div class="files-list">
    <div data-index="0" class="file-description">
      <span class="file-description-name">ClaimForm.pdf</span>
      <span class="file-description-size">26 kb</span>
      <button class="file-description-remove" type="button"></button>
    </div>
  </div>
</div>
```

**Ejemplo de estructura HTML**


```HTML
<div class="file-wrapper field-claim_form field-wrapper">
  <legend for="claim_form" class="field-label" data-visible="false">File Attachment</legend>
  <div class="file-drag-area">
    <div class="file-dragIcon"></div>
    <div class="file-dragText">Drag and Drop To Upload</div>
    <button class="file-attachButton" type="button">Attach</button>
  </div>
  <input type="file" accept="audio/*, video/*, image/*, text/*, application/pdf" id="claim_form"
         name="claim_form" autocomplete="off" multiple="" required="required" data-max-file-size="2MB">
  <div class="files-list">
    </div>
</div>
```

- El atributo class utiliza el nombre proporcionado para el archivo adjunto (claim_form).
- Los atributos id y name del elemento de entrada coinciden con el nombre del archivo adjunto (claim_form).
- La sección de lista de archivos está vacía inicialmente. Se rellena dinámicamente con JavaScript cuando se cargan los archivos.

+++ 

+++ Selectores CSS para el componente Archivo adjunto

- Segmentación de todo el componente Archivo adjunto:

```CSS
/* Target the entire file attachment component */
.file-wrapper {
  /* Add your styles here (e.g., border, padding) */
  border: 1px solid #ccc;
  padding: 15px;
  border-radius: 4px;
  margin-bottom: 20px;
}
```

Este selector aplica estilo a todo el componente archivo adjunto, incluida la leyenda, el área de arrastre, el campo de entrada y la lista.

- Elementos específicos de segmentación:

```CSS
/* Target the drag and drop area */
.file-wrapper .file-drag-area {
  /* Add your styles here (e.g., background color, border) */
  background-color: #f0f0f0;
  border: 1px dashed #ddd;
  padding: 10px;
  text-align: center;
}

/* Target the file input element */
.file-wrapper input[type="file"] {
  /* Add your styles here (e.g., hide the default input) */
  display: none;
}

/* Target individual file descriptions within the list (populated dynamically) */
.file-wrapper .files-list .file-description {
  /* Add your styles here (e.g., margin, display) */
  display: flex;
  justify-content: space-between;
  margin-bottom: 5px;
}

/* Target the file name within the description */
.file-wrapper .files-list .file-description .file-description-name {
  /* Add your styles here (e.g., font-weight) */
  font-weight: bold;
}

/* Target the file size within the description */
.file-wrapper .files-list .file-description .file-description-size {
  /* Add your styles here (e.g., font-size) */
  font-size: 0.8em;
}

/* Target the remove button within the description */
.file-wrapper .files-list .file-description .file-description-remove {
  /* Add your styles here (e.g., background color, hover effect) */
  background-color: transparent;
  border: none;
  cursor: pointer;
}
```

Estos selectores permiten aplicar estilo a varias partes del componente de archivo adjunto de forma individual. Puede ajustar los estilos para que coincidan con sus preferencias de diseño.

+++


## Estilo de componentes

Puede aplicar estilo a los campos de formulario en función de su tipo específico (`{Type}-wrapper`) o nombres individuales (`field-{Name}`). Esto permite un control y una personalización más granulares del aspecto del formulario.

### Estilo basado en el tipo de campo

Puede utilizar selectores de CSS para segmentar tipos de campo específicos y aplicar estilos de forma coherente.

+++ Estructura HTML

```HTML
<div class="{Type}-wrapper field-{Name} field-wrapper" data-required={Required}>
   <label for="{FieldId}" class="field-label">First Name</label>
   <input type="{Type}" placeholder="{Placeholder}" maxlength="{Max}" id={FieldId}" name="{Name}" aria-describedby="{FieldId}-description">
   <div class="field-description" aria-live="polite" id="{FieldId}-description">
    Hint - First name should be minimum 3 characters and a maximum of 10 characters.
   </div>
</div>
```

**Ejemplo de estructura HTML**

```HTML
<div class="text-wrapper field-name field-wrapper" data-required="true">
  <label for="name" class="field-label">Name</label>
  <input type="text" placeholder="Enter your name" maxlength="50" id="name" name="name">
</div>

<div class="number-wrapper field-age field-wrapper" data-required="true">
  <label for="age" class="field-label">Age</label>
  <input type="number" placeholder="Enter your age" id="age" name="age">
</div>

<div class="email-wrapper field-email field-wrapper" data-required="true">
  <label for="email" class="field-label">Email Address</label>
  <input type="email" placeholder="Enter your email" id="email" name="email">
</div>
```

- Cada campo está envuelto en un elemento `div` con varias clases:
   - `{Type}-wrapper`: identifica el tipo de campo. Por ejemplo, `form-text-wrapper`, `form-number-wrapper` y `form-email-wrapper`.
   - `field-{Name}`: identifica el campo por su nombre. Por ejemplo: `form-name`, `form-age` y `form-email`.
   - `field-wrapper`: una clase genérica para todos los contenedores de campo.
- El atributo `data-required` indica si el campo es obligatorio u opcional.
- Cada campo tiene una etiqueta correspondiente, un elemento de entrada y posibles elementos adicionales como marcadores de posición y descripciones.


+++ 


+++ Ejemplo de selectores CSS

```CSS
/* Target all text input fields */
.text-wrapper input {
  /* Add your styles here */
}

/* Target all number input fields */
.number-wrapper input {
  /* Add your styles here */
  letter-spacing: 2px; /* Example for adding letter spacing to all number fields */
}
```

+++

### Estilo basado en el nombre del campo

También puede segmentar campos individuales por nombre para aplicar estilos únicos.

+++ Estructura HTML

```HTML
<div class="{Type}-wrapper field-{Name} field-wrapper" data-required={Required}>
   <label for="{FieldId}" class="field-label">First Name</label>
   <input type="{Type}" placeholder="{Placeholder}" maxlength="{Max}" id="{FieldId}" name="{Name}" aria-describedby="{FieldId}-description">
   <div class="field-description" aria-live="polite" id="{FieldId}-description">
    Hint - Enter the 6 digit number sent to your mobile number.
   </div>
</div>
```

**Ejemplo de estructura HTML**

```HTML
<div class="number-wrapper field-otp field-wrapper" data-required="true">
  <label for="otp" class="field-label">OTP</label>
  <input type="number" placeholder="Enter your OTP" maxlength="6" id="otp" name="otp" aria-describedby="otp-description">
  <div class="field-description" aria-live="polite" id="otp-description">
    Hint - Enter the 6 digit number sent to your mobile number.
   </div>
</div>
```

+++ 

+++ Ejemplo de selector de CSS

```CSS
.field-otp input {
   letter-spacing: 2px
}
```



Este CSS identifica todos los elementos de entrada que se encuentran dentro de un elemento que tiene la clase `field-otp`. La estructura HTML del formulario sigue las convenciones del bloque de formularios adaptables, lo que implica que hay un contenedor marcado con la clase “field-otp” que contiene el campo con el nombre “otp”.

+++ 

