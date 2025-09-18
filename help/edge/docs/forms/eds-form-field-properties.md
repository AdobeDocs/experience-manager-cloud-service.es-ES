---
title: Dominio de propiedades de campo de bloque de Forms adaptable
description: Cree formularios potentes más rápido con hojas de cálculo y propiedades de campo de bloque de Forms adaptables. Esta guía enumera todas las propiedades compatibles con el bloque Forms de EDS.
feature: Edge Delivery Services
source-git-commit: ccc6439f68d8199154d4cd664b9cdb6428460a64
workflow-type: tm+mt
source-wordcount: '930'
ht-degree: 4%

---


# Propiedades del campo de bloque de Forms adaptable

Este documento resume cómo se asigna el esquema JSON a HTML procesado en `blocks/form/form.js`, centrándose en cómo se identifican y procesan los campos, los patrones comunes y las diferencias específicas de los campos.

## ¿Cómo Se Identifican Los Campos (`fieldType`)?

Cada campo del esquema JSON tiene una propiedad `fieldType` que determina cómo se procesa. El(la) `fieldType` puede ser:

- **Un tipo especial**\
  Ejemplos: `drop-down`, `radio-group`, `checkbox-group`, `panel`, `plain-text`, `image`, `heading`, etc.
- **Un tipo de entrada de HTML válido**\
  Ejemplos: `text`, `number`, `email`, `date`, `password`, `tel`, `range`, `file`, etc.
- **Un tipo con `-input` sufijo**\
  Ejemplos: `text-input`, `number-input`, etc. (normalizado para el tipo base como `text`, `number`).

Si `fieldType` coincide con un tipo especial, se utiliza un **procesador personalizado**. De lo contrario, se trata como un **tipo de entrada predeterminado**.

Consulte las secciones siguientes para ver la [estructura y propiedades completas de HTML](#common-html-structure) para cada tipo de campo.

## Propiedades comunes utilizadas por los campos

A continuación, se muestran las propiedades utilizadas por la mayoría de los campos:

- `id`: especifica el ID de elemento y admite la accesibilidad.
- `name`: define el atributo `name` para los elementos input, select o fieldset.
- `label.value`, `label.richText`, `label.visible`: especifica el texto de etiqueta/leyenda, el contenido de HTML y la visibilidad.
- `value`: representa el valor actual del campo.
- `required`: agrega el atributo `required` para los datos de validación.
- `readOnly`, `enabled`: controla si el campo es editable o deshabilitado.
- `description`: muestra el texto de ayuda debajo del campo.
- `tooltip`: establece el atributo `title` para las entradas.
- `constraintMessages`: proporciona mensajes de error personalizados como atributos de datos.

## Estructura común de HTML

La mayoría de los campos se representan dentro de un contenedor que incluye una etiqueta y texto de ayuda opcional. El siguiente fragmento muestra la estructura:

```html
<div class="<fieldType>-wrapper field-wrapper field-<name>" data-id="<id>">
<label for="<id>" class="field-label">Label</label>
<!-- Field-specific input/element here -->
<div class="field-description" id="<id>-description">Description or error
message</div>
</div>
```

Para grupos (radio/casilla de verificación) y paneles, se utiliza un `<fieldset>` con un `<legend>` en lugar de un `<div>/<label>`. El texto de ayuda <div> solo está presente si se ha definido una descripción.

## Visualización del mensaje de error

Los mensajes de error se muestran en el mismo elemento `.field-description` utilizado para el texto de ayuda, que se actualiza dinámicamente.

**Cuando un campo no es válido**:

- Al contenedor (por ejemplo, `.field-wrapper`) se le asigna la clase `.field-invalid`.
- El contenido de `.field-description` se reemplaza con el mensaje de error correspondiente.

**Cuando el campo se vuelve válido**:

- Se ha quitado la clase `.field-invalid`.
- `.field-description` se restaura al texto de ayuda original (si está disponible) o se quita si no existe.

Los mensajes de error personalizados se pueden definir usando la propiedad `constraintMessages` en el JSON.\
Se agregan como atributos `data-<constraint>ErrorMessage` en el contenedor (por ejemplo, `data-requiredErrorMessage`).

## Tipos de entrada predeterminados (entrada HTML o `*-input`)

Si `fieldType` no es un tipo especial, se trata como un tipo de entrada de HTML estándar o como `<type>-input`, por ejemplo, `text`, `number`, `email`, `date`, `text-input`, `number-input`.

- El sufijo `-input` se elimina y el tipo base se usa como atributo `type` de entrada.
- Estos tipos se controlan de manera predeterminada en `renderField()`.
Los tipos de entrada predeterminados comunes son `text`, `number`, `email`, `date`, `password`, `tel`, `range`, `file`, etc.  También aceptan `text-input`, `number-input`, etc., que están normalizados para el tipo base.

## Restricciones para tipos de entrada predeterminados

Las restricciones se agregan como atributos en el elemento de entrada en función de las propiedades JSON.

| Propiedad JSON | Atributo HTML | Aplicable a |
|--------------|---------------|------------|
| maxLength | longitud máxima | texto, correo electrónico, contraseña, teléfono |
| minLength | minlength | texto, correo electrónico, contraseña, teléfono |
| patrón | patrón | texto, correo electrónico, contraseña, teléfono |
| maximum | máx. | número, intervalo, fecha |
| minimum | min | número, intervalo, fecha |
| escalón | escalón | número, intervalo, fecha |
| aceptar | aceptar | archivo |
| múltiple | múltiple | archivo |
| maxOccur | data-max | panel |
| minOccur | data-min | panel |

>[!NOTE]
>
> `multiple` es una propiedad booleana. Si es true, se agrega el atributo `multiple`.

Estos atributos los establece automáticamente el procesador de formularios en función de la definición JSON del campo.

## Ejemplo: Estructura de HTML con restricciones

En el siguiente ejemplo se muestra cómo se representa un campo numérico con restricciones de validación y atributos de control de errores.

```html
<div class="number-wrapper field-wrapper field-age" data-id="age"
data-required="true"
data-minimumErrorMessage="Too small" data-maximumErrorMessage="Too large">
<label for="age" class="field-label">Age</label>
<input type="number"
id="age" name="age"
value="30" required min="18"
max="99" step="1"
placeholder="Enter your age" />
<div class="field-description" id="age-description"> Description or error message
</div>
</div>
```

Cada parte de la estructura de HTML desempeña un papel en el enlace de datos, la validación y la visualización de los mensajes de ayuda o error.

## Propiedades específicas de los campos y sus estructuras HTML

### Lista desplegable

**Propiedades adicionales:**

- `enum` / `enumNames`: defina los valores de opción y sus etiquetas de visualización para la lista desplegable.
- `type`: habilita la selección múltiple si se establece en `array`.
- `placeholder`: agrega una opción de marcador de posición deshabilitada para guiar a los usuarios antes de la selección.

Ejemplo:

```html
<div class="drop-down-wrapper field-wrapper field-<name>" data-id="<id>"
data-required="true"
data-requiredErrorMessage="This field is required">
<label for="<id>" class="field-label">Label</label>
<select id="<id>" name="<name>" required title="Tooltip" multiple>
<option disabled selected value="">Placeholder</option>
<option value="opt1">Option 1</option>
<option value="opt2">Option 2</option>
</select>
<div class="field-description" id="<id>-description"> Description or error message
</div>
</div>
```

### Texto sin formato

**Propiedades adicionales**:

- `richText`: si es verdadero, representa HTML en el párrafo.

Ejemplo:

```html
<div class="plain-text-wrapper field-wrapper field-<name>" data-id="<id>">
<label for="<id>" class="field-label">Label</label>
<p>Text or <a href="..." target="_blank">link</a></p>
</div>
```

### Casilla de verificación

**Propiedades adicionales**:

- `enum`: define los valores de los estados activado y desactivado de la casilla de verificación.
- `properties.variant / properties.alignment`: especifica el estilo visual y la alineación de las casillas de verificación de estilo de modificador.

Ejemplo:

```html
<div class="checkbox-wrapper field-wrapper field-<name>" data-id="<id>"
data-required="true"
data-requiredErrorMessage="Please check this box">
<label for="<id>" class="field-label">Label</label>
<input type="checkbox"
id="<id>"
name="<name>" value="on"
required
data-unchecked-value="off" />
<div class="field-description" id="<id>-description"> Description or error message
</div>
</div>
```

### Botón

**Propiedades adicionales**:

- `buttonType`: especifica el comportamiento del botón al establecer su tipo (botón, envío o restablecimiento).

Ejemplo:

```html
<div class="button-wrapper field-wrapper field-<name>" data-id="<id>">
<button id="<id>" name="<name>" type="submit" class="button"> Label
</button>
</div>
```

### Entrada multilínea

**Propiedades adicionales**:

- `minLength`: especifica el número mínimo de caracteres permitidos en una entrada de área de texto o texto.
- `maxLength`: especifica el número máximo de caracteres permitidos en una entrada de área de texto o texto.
- `pattern`: define una expresión regular con la que el valor de entrada debe coincidir para que se considere válido.
- `placeholder`: muestra texto de marcador de posición dentro del área de entrada o de texto hasta que se introduce un valor.

Ejemplo:

```html
<div class="multiline-wrapper field-wrapper field-<name>" data-id="<id>"
data-minLengthErrorMessage="Too short" data-maxLengthErrorMessage="Too long">
<label for="<id>" class="field-label">Label</label>
<textarea id="<id>"
name="<name>" required
minlength="2"
maxlength="100"
pattern="[A-Za-z]+"
placeholder="Type here..."></textarea>
<div class="field-description" id="<id>-description"> Description or error message
</div>
</div>
```

### Panel

**Propiedades adicionales**:

- `repeatable`: especifica si el panel se puede repetir dinámicamente.
- `minOccur`: establece el número mínimo de instancias de panel requeridas.   maxOccur: establece el número máximo de instancias de panel permitidas.
- `properties.variant`: define el estilo visual o la variante del panel.
- `properties.colspan`: especifica cuántas columnas abarca el panel en un diseño de cuadrícula.
- `index`: indica la posición del panel dentro de su contenedor principal.
- `fieldset`: agrupa campos relacionados en un elemento `<fieldset>` con una leyenda o etiqueta.

Ejemplo:

```html
<fieldset class="panel-wrapper field-wrapper field-<name>" data-id="<id>"
name="<name>"
data-repeatable="true" data-index="0">
<legend class="field-label">Label</legend>
<!-- Nested fields here -->
<button type="button" class="add">Add</button>
<button type="button" class="remove">Remove</button>
<div class="field-description" id="<id>-description"> Description or error message
</div>
</fieldset>
```

### Opciones

**Propiedades adicionales**:

- `enum`: define el conjunto de valores permitidos para el campo de opción, utilizado como atributo value para cada opción de botón de opción.

Ejemplo:

```html
<div class="radio-wrapper field-wrapper field-<name>" data-id="<id>"
data-required="true">
<label for="<id>" class="field-label">Label</label>
<input type="radio" id="<id>" name="<name>" value="opt1" required />
<div class="field-description" id="<id>-description"> Description or error message
</div>
</div>
```

### Grupo de opciones

**Propiedades adicionales**:

- `enum`: define la lista de valores de opción para el grupo de opciones, utilizado como valor de cada botón de opción.
- `enumNames`: proporciona etiquetas de visualización para los botones de opción que coinciden con el orden de enumeración.

Ejemplo:

```html
<fieldset class="radio-group-wrapper field-wrapper field-<name>" data-id="<id>"
data-required="true">
<legend class="field-label">Label</legend>
<div>
<input type="radio" id="<id>-0" name="<name>" value="opt1" required />
<label for="<id>-0">Option 1</label>
</div>
<div>
<input type="radio" id="<id>-1" name="<name>" value="opt2" />
<label for="<id>-1">Option 2</label>
</div>
<div class="field-description" id="<id>-description"> Description or error message
</div>
</fieldset>
```

### **Grupo de casillas de verificación**

**Propiedades adicionales**:

- `enum`: define la lista de valores de opción para el grupo de casillas de verificación, utilizado como valor de cada casilla de verificación.
- `enumNames`: proporciona etiquetas de visualización para las casillas de verificación, que coinciden con el orden de enumeración.
- `minItems`: establece el número mínimo de casillas de verificación que se deben seleccionar para la validez.
- `maxItems`: establece el número máximo de casillas de verificación que se pueden seleccionar antes de activar un error.

Ejemplo:

```html
<fieldset class="checkbox-group-wrapper field-wrapper field-<name>" data-id="<id>"
data-required="true" data-minItems="1"
data-maxItems="3">
<legend class="field-label">Label</legend>
<div>
<input type="checkbox" id="<id>-0" name="<name>" value="opt1" required />
<label for="<id>-0">Option 1</label>
</div>
<div>
<input type="checkbox" id="<id>-1" name="<name>" value="opt2" />
<label for="<id>-1">Option 2</label>
</div>
<div class="field-description" id="<id>-description"> Description or error message
</div>
</fieldset>
```

### Imagen

**Propiedades adicionales**:

- `value / properties['fd:repoPath']`: define la ruta de origen de la imagen o la ruta de acceso al repositorio para procesar la imagen.
- `altText`: proporciona texto alternativo para la imagen (atributo alt) para mejorar la accesibilidad.

Ejemplo:

```html
<div class="image-wrapper field-wrapper field-<name>" data-id="<id>">
<picture>
<img src="..." alt="..." />
<!-- Optimized sources -->
</picture>
</div>
```

### Encabezado

**Propiedades adicionales**:

- `value`: especifica el contenido de texto que se mostrará dentro del elemento de encabezado (por ejemplo, `<h2>`).

Ejemplo:

```html
<div class="heading-wrapper field-wrapper field-<name>" data-id="<id>">
<h2 id="<id>">Heading Text</h2>
</div>
```

Para obtener más información, vea la implementación en `blocks/form/form.js` y `blocks/form/util.js`.


<!--Each form field is represented as a dedicated row in the spreadsheet, analogous to fields in a database table. The column headers act as labels for the various properties supported by the form field block.

Think of your form as a table in a spreadsheet, where each line represents a different question or piece of information you want to collect. The table headings tell you what kind of answers you can expect for each section.

The below table lists all the properties that are supported by the Adaptive Forms Block.

**Master Your Forms with These Adaptive Forms Block Field Properties:**

This table details all the properties you can use to customize your Adaptive Forms Block fields:

| Property | Description | Example |
|---|---|---|
| **Type** | [HTML input type](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input#input_types) (text, email, number, etc.), [textarea](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/textarea), [select](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/select), [fieldset](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/fieldset) | `text`, `email`, `radio`, `select` |
| **Name** | This defines the unique identifier for submitted data (e.g., 'email' for an email address field).  Choose a clear and unique name for each field, as the name serves as internal field identifier used for data mapping during submission. | `user_name`, `email_address` |
| **Label** | User-friendly field label | `"Full Name"`, `"Choose your country"` |
| **Value** | Default value displayed | `"John Doe"`, `"United States"` |
| **Placeholder** | Hint text within the field | `"Enter your email address"` |
| **Description** | Help text for users | `"Please enter a valid email address"` |
| **Visible** | Show/hide the field initially | `true`, `false` |
| **Mandatory** | Require a value from the user | `true`, `false` |
| **Min/Max** | Set minimum/maximum values (number, date, text length) | `18` (age), `2025-12-31` (date) |
| **Accept** | Allowed file types for file upload | `"image/jpeg,image/png"` |
| **Multiple** | Allow multiple file selections | `true`, `false` |
| **Options** | Comma-separated list for dropdown menus | `"Option 1, Option 2, Option 3"` |
| **Checked** | Default-selected radio button/checkbox | `true`, `false` |
| **Fieldset** | Group fields together | Fieldset name (e.g., `"Personal Information"`) |-->

