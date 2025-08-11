---
title: Personalice el tema y el estilo de un Edge Delivery Services para AEM Forms
description: Personalice de forma eficaz el tema y el estilo de los formularios de AEM que se entregan a través de Edge Delivery Services, lo que garantiza una experiencia del usuario coherente y con marca.
feature: Edge Delivery Services
role: Admin, Architect, Developer
exl-id: ac780399-34fe-457d-aaf4-b675656c024d
source-git-commit: cfff846e594b39aa38ffbd3ef80cce1a72749245
workflow-type: tm+mt
source-wordcount: '2493'
ht-degree: 55%

---

# Personalización del aspecto de los formularios

El estilo de los formularios en Edge Delivery Services para AEM Forms requiere una comprensión sofisticada de las propiedades personalizadas de CSS, la arquitectura basada en bloques y las estrategias de segmentación específicas de componentes. A diferencia de los enfoques tradicionales de estilo de formulario, el bloque de Forms adaptable implementa un sistema de token de diseño sistemático que permite una temática coherente y, al mismo tiempo, mantiene las ventajas de rendimiento y accesibilidad de Edge Delivery Services.

La arquitectura de bloques de Forms adaptable genera estructuras de HTML estandarizadas en todos los componentes del formulario, lo que crea patrones predecibles para la segmentación y personalización de CSS. Esta coherencia permite a los desarrolladores implementar sistemas de estilo completos que se escalan en implementaciones de formularios complejos, al tiempo que preservan las optimizaciones de rendimiento basadas en bloques que hacen que Edge Delivery Services sea excepcionalmente rápido.

Esta guía completa cubre los fundamentos técnicos del estilo de los formularios dentro del ecosistema de Edge Delivery Services, incluidos los sistemas de propiedades personalizadas CSS, los patrones de estructura HTML de componentes y las técnicas avanzadas de estilo. La documentación proporciona comprensión teórica y orientación práctica sobre la implementación para crear experiencias de formulario sofisticadas y con marca.

## Lo que dominarás

**Dominio de propiedades personalizadas de CSS**: Comprenda el sistema de variables completo que controla el aspecto del formulario, incluidos los esquemas de color, las escalas tipográficas, los sistemas de espaciado y los parámetros de diseño. Aprenda a anular y ampliar estas propiedades para implementar temas de marca completos.

**Comprensión de la arquitectura del componente**: obtenga información detallada sobre los patrones de estructura de HTML que usa cada tipo de componente de formulario, lo que permite una personalización y un direccionamiento CSS precisos sin romper la funcionalidad subyacente ni las características de accesibilidad.

**Técnicas de estilo avanzadas**: Implemente patrones de estilo sofisticados, incluidos el estilo basado en estados, la integración de diseño interactivo y las estrategias de personalización optimizadas para el rendimiento que mantienen las características de carga rápida de Edge Delivery Services.

**Estrategias de implementación profesionales**: conozca los enfoques estándar del sector para el estilo de formularios, incluida la integración del sistema de diseño, la arquitectura CSS mantenible y las técnicas de solución de problemas para escenarios de estilo complejos.

## Explicación de los tipos de campo de formulario

Antes de sumergirse en el estilo, vamos a revisar los [tipos de campo](/help/edge/docs/forms/universal-editor/create-custom-component.md#supported-fieldtypes) del formulario común compatibles con el Bloque de formularios adaptables:

- Campos de entrada: incluyen entradas de texto, entradas de correo electrónico, entradas de contraseña y mucho más.
- Grupos de casillas de verificación: se utilizan para seleccionar varias opciones.
- Grupos de radio: se utilizan para seleccionar solo una opción de un grupo.
- Desplegables: también conocidos como casillas de selección, que se utilizan para seleccionar una opción de una lista.
- Paneles/contenedores: se utilizan para agrupar elementos de formulario relacionados.

## Principios básicos de estilo

Entender los [conceptos fundamentales de CSS](https://www.w3schools.com/css/css_intro.asp) es esencial antes de aplicar estilo a campos de formulario específicos:

- [Selectores](https://www.w3schools.com/css/css_selectors.asp): los selectores CSS permiten aplicar estilos a elementos HTML específicos. Puede utilizar selectores de elementos, selectores de clases o selectores de ID.
- [Propiedades](https://www.w3schools.com/css/css_syntax.asp): las propiedades CSS definen el aspecto visual de los elementos. Las propiedades comunes para aplicar estilo a los campos de formulario incluyen color, color de fondo, borde, relleno, margen y más.
- [Modelo de cuadro](https://www.w3schools.com/css/css_boxmodel.asp): el modelo de cuadro CSS describe la estructura de los elementos HTML como un área de contenido rodeada de relleno, bordes y márgenes.
- Caja flexible/Cuadrícula: [Caja flexible](https://www.w3schools.com/css/css3_flexbox.asp) CSS y [Diseños de cuadrícula](https://www.w3schools.com/css/css_grid.asp) son herramientas potentes para crear diseños adaptables y flexibles.




## Estilo de formulario completo con propiedades personalizadas de CSS

El bloque de Forms adaptable utiliza una sofisticada arquitectura CSS basada en propiedades personalizadas (variables CSS) que permite aplicar un tema sistemático y un estilo coherente a todos los componentes del formulario. Comprender esta estructura es esencial para personalizar y personalizar eficazmente el formulario.

### Explicación de la arquitectura de forms.css

Los estilos de formulario predeterminados se encuentran en el repositorio del proyecto en `/blocks/form/form.css` y siguen un enfoque estructurado que da prioridad al mantenimiento, la coherencia y la flexibilidad de personalización. La arquitectura consta de varios componentes clave:

**Base de propiedades personalizadas de CSS**: el sistema de estilo se basa en propiedades personalizadas de CSS definidas en el nivel `:root`, lo que proporciona un sistema de temas centralizado que se aplica en cascada a todos los componentes del formulario. Estas variables establecen tokens de diseño para colores, tipografía, espaciado y propiedades de diseño.

**Estructura CSS basada en bloques**: Edge Delivery Services emplea una arquitectura basada en bloques en la que la clase `.form` sirve como el área de nombres principal para todos los estilos relacionados con el formulario, lo que garantiza un aislamiento adecuado del ámbito y evita conflictos de CSS con otros componentes de la página.

**Estilo específico del componente**: los componentes de formulario individuales están diseñados con patrones de contenedor coherentes (`.{Type}-wrapper`) que proporcionan un direccionamiento predecible para distintos tipos de campo a la vez que mantienen la integridad general del sistema de diseño.

### Referencia y personalización de propiedades personalizadas de CSS

El sistema de estilo de formularios incluye más de 50 propiedades personalizadas de CSS que controlan todos los aspectos de la apariencia y el comportamiento del formulario. La comprensión de estas propiedades permite una personalización completa y, al mismo tiempo, mantiene la coherencia del diseño.

+++ Variables de color y temática

El sistema de colores establece una base visual completa para los formularios a través de propiedades personalizadas cuidadosamente organizadas:

```css
:root {
    /* Primary color system */
    --background-color-primary: #fff;
    --label-color: #666;
    --border-color: #818a91;
    --form-error-color: #ff5f3f;
    
    /* Button color system */
    --button-primary-color: #5F8DDA;
    --button-secondary-color: #666;
    --button-primary-hover-color: #035fe6;
    
    /* Form-specific color applications */
    --form-background-color: var(--background-color-primary);
    --form-input-border-color: var(--border-color);
    --form-invalid-border-color: #ff5f3f;
    --form-label-color: var(--label-color);
}
```

**Ejemplo práctico de personalización**: Para implementar un tema oscuro en los formularios, reemplace las variables de color base:

```css
:root {
    --background-color-primary: #1a1a1a;
    --label-color: #e0e0e0;
    --border-color: #404040;
    --form-error-color: #ff6b6b;
    --button-primary-color: #4a9eff;
}
```

Este cambio único se propaga por todos los componentes del formulario porque el sistema utiliza referencias variables en lugar de valores codificados.

+++

+++ Variables de tipografía y espaciado

Las variables de tipografía y espaciado proporcionan un control exhaustivo sobre la presentación del texto y el espaciado del diseño:

```css
:root {
    /* Font size system */
    --form-font-size-m: 22px;
    --form-font-size-s: 18px;
    --form-font-size-xs: 16px;
    
    /* Component-specific typography */
    --form-label-font-size: var(--form-font-size-s);
    --form-label-font-weight: 400;
    --form-title-font-weight: 600;
    --form-input-font-size: 1rem;
    
    /* Spacing system */
    --form-field-horz-gap: 40px;
    --form-field-vert-gap: 20px;
    --form-input-padding: 0.75rem 0.6rem;
    --form-padding: 0 10px;
}
```

**Ejemplo práctico de personalización**: Para crear un diseño de formulario más compacto con una tipografía más pequeña:

```css
:root {
    --form-font-size-m: 18px;
    --form-font-size-s: 14px;
    --form-font-size-xs: 12px;
    --form-field-horz-gap: 20px;
    --form-field-vert-gap: 15px;
    --form-input-padding: 0.5rem 0.4rem;
}
```

+++

+++ Variables de diseño y estructura

Las variables de diseño controlan las dimensiones del formulario, el comportamiento de la cuadrícula y la disposición de componentes:

```css
:root {
    /* Form layout */
    --form-width: 100%;
    --form-columns: 12;
    --form-submit-width: 100%;
    
    /* Card-based components */
    --form-card-border-radius: 4px;
    --form-card-padding: 0.6rem 0.8rem;
    --form-card-shadow: 0 1px 2px rgb(0 0 0 / 3%);
    --form-card-hover-shadow: 0 2px 4px rgb(0 0 0 / 6%);
    
    /* Wizard-specific layout */
    --form-wizard-padding: 0px;
    --form-wizard-padding-bottom: 160px;
    --form-wizard-step-legend-padding: 10px;
}
```

**Ejemplo práctico de personalización**: Para crear un formulario de estilo de tarjeta con una profundidad visual mejorada:

```css
:root {
    --form-card-border-radius: 12px;
    --form-card-padding: 1.5rem 2rem;
    --form-card-shadow: 0 4px 12px rgb(0 0 0 / 8%);
    --form-card-hover-shadow: 0 8px 24px rgb(0 0 0 / 12%);
    --form-background-color: #f8f9fa;
}

.form {
    background: var(--form-background-color);
    border-radius: var(--form-card-border-radius);
    box-shadow: var(--form-card-shadow);
    padding: var(--form-card-padding);
    max-width: 600px;
    margin: 2rem auto;
}
```

+++

### Patrones de estilo CSS y prácticas recomendadas

El bloque de Forms adaptable sigue patrones CSS específicos que garantizan un mantenimiento, un rendimiento y un estilo coherente en todos los componentes.

+++ Patrones de estilo principales

**Contenedor de formulario de nivel de bloque**: establezca como destino el contenedor de formulario principal para el diseño general y el estilo de fondo:

```css
.form {
    /* Form-wide styles */
    max-width: 800px;
    margin: 0 auto;
    background-color: var(--form-background-color);
    padding: var(--form-padding);
    border-radius: var(--form-card-border-radius);
}
```

**Patrones de contenedor de componentes**: Dirija tipos de campo específicos usando clases de contenedor coherentes:

```css
/* Text input fields */
.form .text-wrapper input {
    padding: var(--form-input-padding);
    border: var(--form-input-border-size) solid var(--form-input-border-color);
    font-size: var(--form-input-font-size);
    border-radius: 4px;
    width: 100%;
}

/* Email input fields */
.form .email-wrapper input {
    padding: var(--form-input-padding);
    border: var(--form-input-border-size) solid var(--form-input-border-color);
    font-size: var(--form-input-font-size);
}

/* Button styling */
.form .button-wrapper button {
    background-color: var(--form-button-background-color);
    color: var(--form-button-color);
    padding: var(--form-button-padding);
    border: var(--form-button-border);
    font-size: var(--form-button-font-size);
    border-radius: 4px;
    cursor: pointer;
    transition: background-color 0.2s ease;
}

.form .button-wrapper button:hover {
    background-color: var(--form-button-background-hover-color);
}
```

+++

+++ Patrones de personalización avanzados

**Segmentación específica de campo**: Segmente los campos individuales por nombre para los requisitos de estilo únicos:

```css
/* Style specific fields */
.form .field-email input {
    background-image: url('data:image/svg+xml;...'); /* Email icon */
    background-repeat: no-repeat;
    background-position: right 12px center;
    padding-right: 40px;
}

.form .field-phone input {
    text-align: center;
    letter-spacing: 1px;
    font-family: monospace;
}
```

**Estilo basado en estado**: Implementar estados de validación e interacción:

```css
/* Validation states */
.form .field-wrapper[data-valid="false"] input {
    border-color: var(--form-error-color);
    box-shadow: 0 0 0 2px rgba(255, 95, 63, 0.1);
}

.form .field-wrapper[data-valid="true"] input {
    border-color: #28a745;
    box-shadow: 0 0 0 2px rgba(40, 167, 69, 0.1);
}

/* Focus states */
.form .text-wrapper input:focus,
.form .email-wrapper input:focus {
    outline: none;
    border-color: var(--button-primary-color);
    box-shadow: 0 0 0 2px rgba(95, 141, 218, 0.2);
}
```

+++


## Estructura de componentes

El bloque de formularios adaptables ofrece una estructura HTML coherente para varios elementos de formulario, lo que garantiza una gestión y un estilo más sencillos. Puede modificar los componentes mediante CSS con fines de estilo.

+++ Componentes generales (excepto menús desplegables, grupos de opciones y grupos de casillas de verificación):

Todos los campos de formulario, excepto los menús desplegables, los grupos de opción y los grupos de casillas de verificación, tienen la siguiente estructura HTML:

#### Estructura HTML de los componentes generales

```HTML
  <div class="{Type}-wrapper field-{Name}   field-wrapper" data-required={Required}>
     <label for="{FieldId}" class="field-label">First   Name</label>
     <input type="{Type}" placeholder="{Placeholder}"   maxlength="{Max}" id={FieldId}" name="{Name}"   aria-describedby="{FieldId}-description">
     <div class="field-description" aria-live="polite"  id="{FieldId}-description">
      Hint - First name should be minimum 3 characters  and a maximum of 10 characters.
     </div>
  </div>
```

- Clases: el elemento div tiene varias clases para dirigirse a elementos y estilos específicos. Necesita las clases `{Type}-wrapper` o `field-{Name}` para desarrollar un selector de CSS para aplicar estilo a un campo de formulario:
- {Type}: identifica el componente por el tipo de campo. Por ejemplo, texto (ajustador de texto), número (ajustador de número), fecha (ajustador de fecha).
- {Name}: identifica el componente por su nombre. El nombre del campo solo puede tener caracteres alfanuméricos. Los múltiples guiones consecutivos del nombre se sustituyen por un solo guion `(-)`, y los guiones inicial y final del nombre de un campo se eliminan. Por ejemplo, nombre (campo-nombre ajustador de campo).
- {FieldId}: es un identificador único para el campo, se genera automáticamente.
- {Required}: es un valor booleano que indica si el campo es obligatorio.
- Etiqueta: el elemento `label` proporciona un texto descriptivo para el campo y lo asocia al elemento de entrada mediante el atributo `for`.
- Entrada: el elemento `input` define el tipo de datos que se van a introducir. Por ejemplo, texto, número, correo electrónico.
- Descripción (opcional): la `div` con clase `field-description` proporciona información o instrucciones adicionales para el usuario.

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

#### Selector de CSS para componentes generales

```css
/* Primary Pattern: Target field wrapper by type */
.form .{Type}-wrapper {
    /* Container styling for specific field types */
    margin-bottom: 1rem;
    border-radius: 4px;
}

/* Primary Pattern: Target input fields within wrapper */
.form .{Type}-wrapper input {
    /* Input field styling using CSS custom properties */
    border: var(--form-input-border-size) solid var(--form-input-border-color);
    padding: var(--form-input-padding);
    border-radius: 4px;
    width: 100%;
    font-size: var(--form-input-font-size);
}

/* Context-specific: Target element by field name when higher specificity needed */
.form .field-{Name} input {
    /* Field-specific customizations */
    /* Use this pattern for unique styling requirements */
}
```

- `.form .{Type}-wrapper`: segmenta el elemento envolvente de campo en función del tipo de campo. Por ejemplo, `.form .text-wrapper` identifica todos los contenedores de campo de texto.
- `.form .{Type}-wrapper input`: segmenta los elementos de entrada reales dentro del contenedor. Este es el patrón recomendado para aplicar estilo a las entradas del formulario.
- `.form .field-{Name}`: elementos de destino basados en el nombre de campo específico. Por ejemplo, `.form .field-first-name` se dirige al contenedor de campos &quot;Nombre&quot;. Use `.form .field-{Name} input` para dirigirse específicamente al elemento de entrada.
- **Evitar**: `main .form form .{Type}-wrapper`: esto crea una especificidad CSS innecesaria y es más difícil de mantener.

**Ejemplo de selectores CSS para componentes generales**

```css
/* Primary Pattern: Target all text input fields */
.form .text-wrapper input {
    border: var(--form-input-border-size) solid var(--form-input-border-color);
    padding: var(--form-input-padding);
    border-radius: 4px;
    width: 100%;
    font-size: var(--form-input-font-size);
    background-color: var(--form-input-background-color);
}

/* Context-specific: Target field by name when higher specificity needed */
.form .field-first-name input {
    text-transform: capitalize;
    border-color: var(--button-primary-color);
}

/* Alternative with main context if needed */
main .form .text-wrapper input {
    /* Use only when you need higher specificity */
    color: var(--form-label-color);
}
```

+++

+++ Componente desplegable

Para los menús desplegables, se utiliza el elemento `select` en lugar de un elemento `input`:

#### Estructura HTML del componente desplegable

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

#### Selectores CSS para componentes desplegables

En la siguiente CSS se enumeran algunos selectores CSS de ejemplo para los componentes desplegables.

```css
/* Primary Pattern: Target the dropdown wrapper */
.form .drop-down-wrapper {
    /* Container layout using flexbox */
    display: flex;
    flex-direction: column;
    margin-bottom: var(--form-field-vert-gap);
}

/* Target the select element */
.form .drop-down-wrapper select {
    border: var(--form-input-border-size) solid var(--form-input-border-color);
    padding: var(--form-input-padding);
    border-radius: 4px;
    background-color: var(--form-input-background-color);
    font-size: var(--form-input-font-size);
    color: var(--form-label-color);
}

/* Style the label */
.form .drop-down-wrapper .field-label {
    margin-bottom: 5px;
    font-weight: var(--form-label-font-weight);
    color: var(--form-label-color);
    font-size: var(--form-label-font-size);
}
```

- Segmentar el envolvente: el primer selector (`.drop-down-wrapper`) segmenta el elemento envolvente exterior, lo que garantiza que los estilos se apliquen a todo el componente desplegable.
- Diseño del Flexbox: este organiza la etiqueta, la lista desplegable y la descripción verticalmente para conseguir un diseño limpio.
- Estilo de etiqueta: la etiqueta destaca por su grosor de fuente más negrita y un margen ligero.
- Estilo desplegable: el elemento `select` recibe un borde, un relleno y esquinas redondeadas para obtener un aspecto pulido.
- Color de fondo: se establece un color de fondo coherente para armonía visual.
- Personalización de flechas: los estilos opcionales ocultan la flecha desplegable predeterminada y crean una flecha personalizada con un carácter Unicode y una posición determinada.

+++

+++ Grupos de radio

Al igual que los componentes desplegables, los grupos de radio tienen su propia estructura HTML y estructura CSS:

#### Estructura HTML del grupo de radio

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

**Ejemplo de estructura HTML**

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

#### Selectores CSS para grupos de radio

- Segmentación del Fieldset

```css
/* Target radio group container */
.form .radio-group-wrapper {
    border: var(--form-input-border-size) solid var(--form-input-border-color);
    padding: var(--form-input-padding);
    border-radius: 4px;
    margin-bottom: var(--form-field-vert-gap);
}
```

Este selector se dirige a cualquier fieldset con la clase radio-group-wrapper. Esto sería útil para aplicar estilos generales a todo el grupo de radio.

- Segmentación de etiquetas de botones de radio

```css
/* Target radio button labels */
.form .radio-wrapper label {
    font-weight: var(--form-label-font-weight);
    margin-right: 10px;
    color: var(--form-label-color);
    font-size: var(--form-label-font-size);
    cursor: pointer;
}
```

- Segmente todas las etiquetas de botones de radio de un fieldset específico en función de su nombre

```css
/* Target all radio button labels within a specific fieldset based on its name */
.form .field-color .radio-wrapper label {
    /* Field-specific radio label customizations */
    /* Add your custom styles here */
}
```

+++

+++ Grupos de casillas de verificación

#### Estructura HTML del grupo de casillas de verificación

```HTML
<fieldset class="checkbox-group-wrapper field-{Name} field-wrapper" id="{FieldId}" name="{Name}" data-required="{Required}">
   <legend for="{FieldId}" class="field-label">....</legend>
   <% for each radio in Group %>
   <div class="checkbox-wrapper field-{Name}">
      <input type="checkbox" value="" id="{UniqueId}" data-field-type="checkbox-group" name="{FieldId}">
      <label for="{UniqueId}" class="field-label">...</label>
   </div>
   <% end for %>
</fieldset>
```

**Ejemplo de estructura HTML**

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

#### Selectores CSS para grupos de casillas de verificación

- Segmentación del contenedor exterior: estos selectores se dirigen a los contenedores más externos de los grupos de radio y de la casilla de verificación, lo que permite aplicar estilos generales a toda la estructura del grupo. Esto resulta útil para establecer el espaciado, la alineación u otras propiedades relacionadas con el diseño.

```css
/* Primary Pattern: Targets radio group wrappers */
.form .radio-group-wrapper {
    margin-bottom: var(--form-field-vert-gap); /* Adds space between radio groups */
    display: flex;
    flex-direction: column;
    border: var(--form-fieldset-border);
    padding: var(--form-input-padding);
}

/* Primary Pattern: Targets checkbox group wrappers */
.form .checkbox-group-wrapper {
    margin-bottom: var(--form-field-vert-gap); /* Adds space between checkbox groups */
    display: flex;
    flex-direction: column;
    border: var(--form-fieldset-border);
    padding: var(--form-input-padding);
}
```

- Etiquetas de grupos de segmentación: este selector se dirige al elemento `.field-label` dentro de los contenedores de grupo de casilla de verificación y radio. Esto le permite aplicar estilo a las etiquetas específicamente para estos grupos, lo que podría hacerlas destacar más.

```css
/* Primary Pattern: Target group labels */
.form .radio-group-wrapper legend,
.form .checkbox-group-wrapper legend {
    font-weight: var(--form-title-font-weight); /* Makes the group label bold */
    margin-bottom: 0.5rem;
    font-size: var(--form-fieldset-legend-font-size);
    color: var(--form-fieldset-legend-color);
    padding: var(--form-fieldset-legend-padding);
    border: var(--form-fieldset-legend-border);
}
```

- Segmentación de entradas y etiquetas individuales: estos selectores proporcionan un control más granular sobre los botones de opción individuales, casillas de verificación y sus etiquetas asociadas. Puede utilizarlos para ajustar el tamaño, el espaciado o aplicar estilos visuales más distintos.

```css
/* Primary Pattern: Styling radio buttons */
.form .radio-group-wrapper input[type="radio"] {
    margin-right: 8px; /* Adds space between the input and its label */
    margin-bottom: 4px;
    cursor: pointer;
}

/* Primary Pattern: Styling radio button labels */
.form .radio-group-wrapper label {
    font-size: var(--form-label-font-size); /* Changes the label font size */
    color: var(--form-label-color);
    font-weight: var(--form-label-font-weight);
    display: flex;
    align-items: center;
    cursor: pointer;
}

/* Primary Pattern: Styling checkboxes */
.form .checkbox-group-wrapper input[type="checkbox"] {
    margin-right: 8px; /* Adds space between the input and its label */
    margin-bottom: 4px;
    cursor: pointer;
}

/* Primary Pattern: Styling checkbox labels */
.form .checkbox-group-wrapper label {
    font-size: var(--form-label-font-size); /* Changes the label font size */
    color: var(--form-label-color);
    font-weight: var(--form-label-font-weight);
    display: flex;
    align-items: center;
    cursor: pointer;
}
```

- Personalización del aspecto de los botones de opción y las casillas de verificación: esta técnica oculta la entrada predeterminada y utiliza los pseudoelementos `:before` y `:after` para crear imágenes personalizadas que cambian de aspecto en función del estado “activado”.

```css
/* Hide the default radio button or checkbox */
.form .radio-group-wrapper input[type="radio"],
.form .checkbox-group-wrapper input[type="checkbox"] {
    opacity: 0;
    position: absolute;
    width: 1px;
    height: 1px;
}

/* Create a custom radio button */
.form .radio-group-wrapper input[type="radio"] + label::before {
    content: '';
    display: inline-block;
    width: 16px;
    height: 16px;
    border: 2px solid var(--form-input-border-color);
    border-radius: 50%;
    margin-right: 8px;
    background-color: var(--form-input-background-color);
    transition: all 0.2s ease;
}

.form .radio-group-wrapper input[type="radio"]:checked + label::before {
    background-color: var(--button-primary-color);
    border-color: var(--button-primary-color);
    box-shadow: inset 0 0 0 3px var(--form-input-background-color);
}

/* Create a custom checkbox */
.form .checkbox-group-wrapper input[type="checkbox"] + label::before {
    content: '';
    display: inline-block;
    width: 16px;
    height: 16px;
    border: 2px solid var(--form-input-border-color);
    border-radius: 2px;
    margin-right: 8px;
    background-color: var(--form-input-background-color);
    transition: all 0.2s ease;
}

.form .checkbox-group-wrapper input[type="checkbox"]:checked + label::before {
    background-color: var(--button-primary-color);
    border-color: var(--button-primary-color);
    background-image: url('data:image/svg+xml;utf8,<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 16 16"><path fill="white" d="M13.854 3.646a.5.5 0 0 1 0 .708l-7 7a.5.5 0 0 1-.708 0l-3.5-3.5a.5.5 0 1 1 .708-.708L6.5 10.293l6.646-6.647a.5.5 0 0 1 .708 0z"/></svg>');
    background-repeat: no-repeat;
    background-position: center;
}
```

+++

+++ Componentes de panel/contenedor

#### Estructura HTML de los componentes de panel/contenedor

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
- El elemento de leyenda (`<legend>`) sirve como título del panel con el texto &quot;Información de inicio de sesión&quot; y la etiqueta de campo de clase. El atributo data-visible=&quot;false&quot; se puede utilizar con JavaScript para controlar la visibilidad del título.
- Dentro del fieldset, varios.Los elementos {Type}-wrapper (.text-wrapper y .password-wrapper en este caso) representan campos de formulario individuales dentro del panel.
- Cada contenedor contiene una etiqueta, un campo de entrada y una descripción, similares a los ejemplos anteriores.


#### Ejemplo de selectores CSS para componentes de panel/contenedor

1. Segmentación del panel:

```CSS
  /- Target the entire panel container */
  main .form form .panel-wrapper {
    /- Add your styles here (e.g., border, padding, background color) */
    border: 1px solid #ccc;
    padding: 15px;
    border-radius: 4px;
    margin-bottom: 20px;
 }
```

- El selector `.panel-wrapper` aplica estilo a todos los elementos con el contenedor de paneles de clase, lo que proporciona un aspecto coherente a todos los paneles.

1. Segmentación del título del panel:

```CSS
  /- Target the legend element (panel title) */
  .panel-wrapper legend {
    /- Add your styles here (e.g., font-weight, font-size) */
    font-weight: bold;
    font-size: 16px;
    padding-bottom: 5px;
    margin-bottom: 10px;
    border-bottom: 1px solid #ddd; /- Optional: create a separation line */
  }
```

- El selector `.panel-wrapper legend` aplica estilos al elemento de leyenda del panel, lo que hace que el título se destaque visualmente.


1. Segmentación de campos individuales dentro del panel:

```CSS
/- Target all form field wrappers within a panel */
main .form form .panel-wrapper .{Type}-wrapper {
  /- Add your styles here (e.g., margin) */
  margin-bottom: 10px;
}
```

- El selector `.panel-wrapper .{Type}-wrapper` se dirige a todos los contenedores con la clase `.{Type}-wrapper` dentro del panel, lo que le permite aplicar estilo al espaciado entre los campos del formulario.

1. Segmentación de campos específicos (opcional):

```CSS
  /- Target the username field wrapper */
  main .form form .panel-wrapper .text-wrapper.field-username {
    /- Add your styles here (specific to username field) */
  }

  /- Target the password field wrapper */
  main .form form .panel-wrapper .password-wrapper.field-password {
    /- Add your styles here (specific to password field) */
  }
```

- Estos selectores opcionales le permiten segmentar contenedores de campo específicos dentro del panel para aplicar un estilo único, como resaltar el campo de nombre de usuario.


+++

+++ Panel repetible

#### Estructura HTML de un panel repetible

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


#### Selectores CSS para un panel repetible

- Segmentación de todos los paneles repetibles:

```CSS
  /- Target all panels with the repeatable attribute */
 main .form form .panel-wrapper[data-repeatable="true"] {
    /- Add your styles here (e.g., border, margin) */
    border: 1px solid #ccc;
    padding: 15px;
    border-radius: 4px;
    margin-bottom: 20px;
  }
```

El selector aplica estilo a todos los paneles que se pueden repetir, lo que garantiza una apariencia uniforme.


- Segmentación de campos individuales dentro de un panel:

```CSS
/- Target all form field wrappers within a repeatable panel */
main .form form .panel-wrapper[data-repeatable="true"] .{Type}-wrapper {
  /- Add your styles here (e.g., margin) */
  margin-bottom: 10px;
}
```

Este selector aplica estilo a todos los contenedores de campo dentro de un panel repetible, manteniendo un espaciado coherente entre los campos.

- Segmentación de campos específicos (dentro de un panel):

```CSS
/- Target the name field wrapper within the first panel */
main .form form .panel-wrapper[data-repeatable="true"][data-index="0"] .text-wrapper.field-name {
  /- Add your styles here (specific to first name field) */
}

/- Target all
```


+++


+++ Adjuntar archivos

#### Estructura HTML para adjuntar archivos 

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


#### Selectores CSS para el componente Archivo adjunto

- Segmentación de todo el componente Archivo adjunto:

```CSS
/- Target the entire file attachment component */
main .form form .file-wrapper {
  /- Add your styles here (e.g., border, padding) */
  border: 1px solid #ccc;
  padding: 15px;
  border-radius: 4px;
  margin-bottom: 20px;
}
```

Este selector aplica estilo a todo el componente archivo adjunto, incluida la leyenda, el área de arrastre, el campo de entrada y la lista.

- Elementos específicos de segmentación:

```CSS
/- Target the drag and drop area */
main .form form .file-wrapper .file-drag-area {
  /- Add your styles here (e.g., background color, border) */
  background-color: #f0f0f0;
  border: 1px dashed #ddd;
  padding: 10px;
  text-align: center;
}

/- Target the file input element */
main .form form .file-wrapper input[type="file"] {
  /- Add your styles here (e.g., hide the default input) */
  display: none;
}

/- Target individual file descriptions within the list (populated dynamically) */
main .form form .file-wrapper .files-list .file-description {
  /- Add your styles here (e.g., margin, display) */
  display: flex;
  justify-content: space-between;
  margin-bottom: 5px;
}

/- Target the file name within the description */
main .form form .file-wrapper .files-list .file-description .file-description-name {
  /- Add your styles here (e.g., font-weight) */
  font-weight: bold;
}
```

Estos selectores permiten aplicar estilo a varias partes del componente de archivo adjunto de forma individual. Puede ajustar los estilos para que coincidan con sus preferencias de diseño.

+++



## Estilo de componentes

Puede aplicar estilo a los campos de formulario en función de su tipo específico (`{Type}-wrapper`) o nombres individuales (`field-{Name}`). Esto permite un control y una personalización más granulares del aspecto del formulario.

+++ Estilo basado en el tipo de campo

Puede utilizar selectores de CSS para segmentar tipos de campo específicos y aplicar estilos de forma coherente.

#### Estructura HTML

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




#### Ejemplo de selectores CSS

```CSS
/- Primary Pattern: Target all text input fields */
.form .text-wrapper input {
  /- Add your styles here */
  width: 100%;
  padding: var(--form-input-padding);
}

/- Primary Pattern: Target all number input fields */
.form .number-wrapper input {
  /- Add your styles here */
  letter-spacing: 2px; /- Example for adding letter spacing to all number fields */
  text-align: center;
}
```

+++

+++ Estilo basado en el nombre del campo

También puede segmentar campos individuales por nombre para aplicar estilos únicos.

#### Estructura HTML

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


#### Ejemplo de selector de CSS

```CSS
/- Primary Pattern: Target specific field by name */
.form .field-otp input {
   letter-spacing: 2px;
   text-align: center;
   font-family: monospace;
}

/- Context-specific: Use higher specificity when needed */
main .form .field-otp input {
   /- Use only when you need to override other styles */
   font-weight: bold;
}
```

Este CSS identifica todos los elementos de entrada que se encuentran dentro de un elemento que tiene la clase `field-otp`. La estructura del formulario de Edge Delivery Services sigue las convenciones de bloque de Forms adaptable, donde los contenedores se marcan con clases específicas del campo como &quot;field-top&quot; para campos con el nombre &quot;otp&quot;.


## Implementación y estructura de archivos CSS

### **Implementación de referencia**

La referencia de estilo del formulario completo está disponible en el repositorio de plantillas de AEM Forms:

```
https://github.com/adobe-rnd/aem-boilerplate-forms/blob/main/blocks/form/form.css
```

Este archivo sirve como implementación canónica del sistema de propiedades personalizadas CSS y proporciona la base para todo el estilo del formulario. Incluye definiciones completas para todas las variables CSS, patrones de estilo de componentes e implementaciones de diseño interactivo.

+++

+++ Integración de proyectos

En el proyecto de Edge Delivery Services, implemente el estilo de los formularios mediante este método estructurado:

```
/blocks/form/form.css          // Core form block styles (copied from boilerplate)
/styles/styles.css             // Global site styles and CSS variable overrides
/styles/lazy-styles.css        // Additional component enhancements
```

+++

+++ Estrategia de implementación

**Anulaciones de propiedades personalizadas de CSS**: invalide las variables de formulario en los estilos globales para implementar temas específicos de la marca:

```css
/* In /styles/styles.css */
:root {
    /* Brand-specific overrides */
    --button-primary-color: #your-brand-color;
    --form-background-color: #your-background;
    --label-color: #your-text-color;
}
```

**Personalizaciones específicas de componentes**:
Añada un estilo específico del componente y mantenga el sistema de variables CSS:

```css
/* Enhanced component styling */
.form .text-wrapper input {
    border-radius: var(--form-card-border-radius);
    transition: all 0.2s ease;
}

.form .text-wrapper input:focus {
    transform: translateY(-1px);
    box-shadow: 0 0 0 3px rgba(var(--button-primary-color), 0.1);
}
```

**Integración de diseño interactivo**: utilice propiedades personalizadas de CSS en consultas de medios para obtener un comportamiento interactivo coherente:

```css
@media (max-width: 768px) {
    :root {
        --form-input-padding: 0.875rem;
        --form-field-vert-gap: 1rem;
        --form-padding: 1rem;
    }
}
```

+++

### Ejemplo de implementación de estilo completa

En esta sección se muestra cómo crear un formulario moderno con marca mediante propiedades personalizadas de CSS. La implementación se desglosa en subsecciones claras para facilitar la comprensión y navegación.



+++ &#x200B;1. Variables de tema de marca

Defina la paleta de colores, el espaciado y la tipografía de su marca con propiedades personalizadas de CSS.

```css
/* Custom brand theme */
:root {
  /* Brand color system */
  --brand-primary: #2563eb;
  --brand-secondary: #64748b;
  --brand-success: #059669;
  --brand-error: #dc2626;
  --brand-background: #f8fafc;
  
  /* Override form variables */
  --background-color-primary: #ffffff;
  --button-primary-color: var(--brand-primary);
  --button-primary-hover-color: #1d4ed8;
  --form-error-color: var(--brand-error);
  --form-background-color: var(--brand-background);
  --label-color: var(--brand-secondary);
  --border-color: #d1d5db;
  
  /* Enhanced spacing */
  --form-input-padding: 1rem;
  --form-field-vert-gap: 1.5rem;
  --form-padding: 2rem;
  
  /* Modern typography */
  --form-font-size-s: 16px;
  --form-label-font-weight: 500;
}
```


+++

+++ &#x200B;2. Estilo del contenedor del formulario

Aplique un fondo moderno, un radio de borde y una sombra al contenedor de formularios para obtener un diseño visualmente atractivo.


```css
/* Enhanced form container */
.form {
    background: linear-gradient(135deg, #f8fafc 0%, #f1f5f9 100%);
    border-radius: 12px;
    box-shadow: 0 10px 25px rgba(0, 0, 0, 0.05);
    max-width: 600px;
    margin: 2rem auto;
    overflow: hidden;
}
```




+++

+++ &#x200B;3. Estilo del campo de entrada

Defina un estilo limpio y moderno en los campos de entrada de texto, correo electrónico y número.


```css
/* Modern input styling */
.form .text-wrapper input,
.form .email-wrapper input,
.form .number-wrapper input {
    background: white;
    border: 2px solid var(--border-color);
    border-radius: 8px;
    padding: var(--form-input-padding);
    font-size: 16px;
    transition: all 0.2s ease;
    width: 100%;
}
```


+++

+++ &#x200B;4. Personalización adicional

Puede ampliar aún más el estilo del formulario segmentando campos, estados o componentes específicos según sea necesario. Consulte las secciones anteriores para ver patrones avanzados.

```css
/* Custom brand theme */
:root {
    /* Brand color system */
    --brand-primary: #2563eb;
    --brand-secondary: #64748b;
    --brand-success: #059669;
    --brand-error: #dc2626;
    --brand-background: #f8fafc;
    
    /* Override form variables */
    --background-color-primary: #ffffff;
    --button-primary-color: var(--brand-primary);
    --button-primary-hover-color: #1d4ed8;
    --form-error-color: var(--brand-error);
    --form-background-color: var(--brand-background);
    --label-color: var(--brand-secondary);
    --border-color: #d1d5db;
    
    /* Enhanced spacing */
    --form-input-padding: 1rem;
    --form-field-vert-gap: 1.5rem;
    --form-padding: 2rem;
    
    /* Modern typography */
    --form-font-size-s: 16px;
    --form-label-font-weight: 500;
}

/* Enhanced form container */
.form {
    background: linear-gradient(135deg, #f8fafc 0%, #f1f5f9 100%);
    border-radius: 12px;
    box-shadow: 0 10px 25px rgba(0, 0, 0, 0.05);
    max-width: 600px;
    margin: 2rem auto;
    overflow: hidden;
}

/* Modern input styling */
.form .text-wrapper input,
.form .email-wrapper input,
.form .number-wrapper input {
    background: white;
    border: 2px solid var(--border-color);
    border-radius: 8px;
    padding: var(--form-input-padding);
    font-size: 16px;
    transition: all 0.2s ease;
    width: 100%;
}

.form .text-wrapper input:focus,
.form .email-wrapper input:focus,
.form .number-wrapper input:focus {
    border-color: var(--brand-primary);
    box-shadow: 0 0 0 3px rgba(37, 99, 235, 0.1);
    transform: translateY(-1px);
}

/* Enhanced button styling */
.form .button-wrapper button[type="submit"] {
    background: linear-gradient(135deg, var(--brand-primary) 0%, #1d4ed8 100%);
    color: white;
    border: none;
    border-radius: 8px;
    padding: 1rem 2rem;
    font-size: 16px;
    font-weight: 600;
    cursor: pointer;
    transition: all 0.2s ease;
    width: 100%;
    box-shadow: 0 4px 12px rgba(37, 99, 235, 0.3);
}

.form .button-wrapper button[type="submit"]:hover {
    transform: translateY(-2px);
    box-shadow: 0 6px 20px rgba(37, 99, 235, 0.4);
}
```

Este completo enfoque muestra cómo las propiedades personalizadas de CSS permiten una temática sofisticada, a la vez que mantienen las funciones de integridad estructural y accesibilidad del sistema de bloques de Forms adaptable.

+++

## Solución de problemas de CSS

+++ Problemas de especificidad de CSS

```css
/- ❌ Problem: Styles not applying */
.text-wrapper input {
  color: red;
}

/- ✅ Solution: Match or exceed existing specificity */
.form .text-wrapper input {
  color: red;
}

/- ✅ Alternative: Use higher specificity when needed */
main .form .text-wrapper input {
  color: red;
}
```

+++

+++ Problemas de anulación de variables CSS

```css
/- ❌ Problem: Variables not working */
.form {
  --form-border-color: blue; /- Local scope only */
}

/- ✅ Solution: Define in root scope */
:root {
  --form-border-color: blue; /- Global scope */
}
```

+++

+++ Estilo de estado de formulario

```css
/- Validation states */
.form .field-wrapper.error input {
  border-color: var(--form-error-color);
}

.form .field-wrapper.success input {
  border-color: var(--form-success-color);
}

/- Loading state */
.form[data-submitting="true"] {
  opacity: 0.7;
  pointer-events: none;
}

/- Disabled state */
.form input:disabled {
  background-color: var(--form-input-disabled-background);
  cursor: not-allowed;
}
```

+++

+++ Errores del selector común

```css
/- ❌ Incorrect: Assumes direct nesting */
.form form input {
  /- This might miss inputs in wrappers */
}

/- ✅ Correct: Target actual structure */
.form .text-wrapper input {
  /- Targets actual HTML structure */
}

/- ❌ Avoid: Unnecessary specificity */
main .form form .text-wrapper input {
  /- Too specific, harder to override */
}

/- ✅ Preferred: Balanced specificity */
.form .text-wrapper input {
  /- Easier to maintain and override */
}
```

+++



### **Prácticas recomendadas específicas de componentes**


+++ Estilo de botón

```css
/- Primary buttons */
.form .button-wrapper button[type="submit"] {
  background-color: var(--form-focus-color);
  color: white;
  border: none;
  padding: var(--form-input-padding);
  border-radius: var(--form-border-radius);
}

/- Secondary buttons */
.form .button-wrapper button[type="reset"] {
  background-color: transparent;
  color: var(--form-text-color);
  border: 1px solid var(--form-border-color);
}
```

+++

+++ Diseño de formulario adaptable

```css
/- Mobile-first approach */
.form {
  width: 100%;
  padding: 1rem;
}

/- Tablet and up */
@media (min-width: 768px) {
  .form {
    max-width: var(--form-max-width);
    padding: var(--form-padding);
  }
}
```

+++

## Resumen de las prácticas recomendadas

1. **Usar propiedades personalizadas de CSS**: aproveche las variables para lograr una temática coherente
2. **Seguir arquitectura basada en bloques**: usar `.form` como selector de bloques principal
3. **Evitar la sobreespecificidad**: No use `main .form form` a menos que sea necesario
4. **Contenedores de destino**: use `.{Type}-wrapper` patrones para la segmentación de componentes
5. **Mantener coherencia**: utilice los mismos patrones de selector en todo el proyecto
6. **Realizar pruebas en todos los dispositivos**: Asegúrese de que los formularios funcionan bien en dispositivos móviles, tabletas y de escritorio
7. **Validar accesibilidad**: Asegúrese de que los estilos no interfieran con los lectores de pantalla ni con la navegación mediante el teclado


