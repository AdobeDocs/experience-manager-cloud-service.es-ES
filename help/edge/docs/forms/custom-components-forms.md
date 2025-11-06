---
title: Creación de componentes personalizados para un formulario EDS
description: Creación de componentes personalizados para un formulario EDS
feature: Edge Delivery Services
hide: true
hidefromtoc: true
role: Admin, Developer
exl-id: 77e90657-38db-4a49-9aac-3f3774b62624
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '623'
ht-degree: 100%

---

# Creación de componentes personalizados

Edge Delivery Services para AEM Forms le permite personalizar los [componentes de formulario HTML nativos](/help/edge/docs/forms/form-components.md) y crear formularios interactivos fáciles de usar. Permite modificar los componentes del formulario con marcado predefinido, tal como se explica en [Estilo de los campos del formulario](/help/edge/docs/forms/style-theme-forms.md) mediante CSS (hojas de estilo en cascada) personalizadas y código personalizado para decorar el componente, lo que mejora la apariencia de los campos del formulario dentro de un bloque de formularios adaptables.

![Componente personalizado](/help/edge/assets/custom-component-image.png)

Este documento describe los pasos para crear componentes personalizados mediante la aplicación de estilos a los componentes de formulario HTML nativos para mejorar la experiencia del usuario y aumentar el atractivo visual del formulario.

Veamos un ejemplo de un componente `range` que muestra el `Estimated trip cost` en un formulario. El componente `range` aparece como una línea recta, sin mostrar valores como el valor mínimo, máximo o seleccionado.

![Componente Intervalo nativo](/help/edge/assets/native-range-component.png)

Empecemos por personalizar el campo `range` para que muestre los valores mínimo, máximo y seleccionado en la línea añadiendo un estilo con CSS y añadiendo una función personalizada para decorar un componente.

![Componente Intervalo personalizado](/help/edge/assets/custom-range-component.png)

Al final de este artículo, aprenderá a crear componentes personalizados añadiendo estilos al archivo CSS y a la función personalizada.

## Requisitos previos

Antes de empezar a crear el componente personalizado, debe:

- Tener conocimientos básicos sobre los [componentes HTML nativos](/help/edge/docs/forms/form-components.md).
- Saber cómo [aplicar estilos a los campos del formulario basados en el tipo de campo mediante selectores CSS](/help/edge/docs/forms/style-theme-forms.md)


## Creación de un componente personalizado


![pasos para crear un componente personalizado](/help/edge/docs/forms/assets/steps-to-create-custom-component.png)

Analicemos ahora cada paso en detalle.

<!--Refer to the [enquiry spreadsheet](/help/edge/docs/forms/assets/enquiry.xlsx) to customize the `range` component, by following the steps as explained below.-->

### Añadir una función personalizada para decorar el componente

La función personalizada añadida en `[../Form Block/components]` consta de:

- **Declaración de función**: defina el nombre de la función y sus parámetros.
- **Implementación lógica**: escriba la lógica para añadir el comportamiento personalizado para el componente.
- **Exportación de funciones**: haga accesible la función en `[Form Block]`.

Para añadir una función personalizada:

1. Navegue hasta `[../Form Block/components]`.
1. Localice un archivo con el nombre `range.js`. Si no está, deberá crearlo.
1. Añada la siguiente línea de código:

   ```javascript
   function updateBubble(input, element) {
   const step = input.step || 1;
   const max = input.max || 0;
   const min = input.min || 1;
   const value = input.value || 1;
   const current = Math.ceil((value - min) / step);
   const total = Math.ceil((max - min) / step);
   const bubble = element.querySelector('.range-bubble');
   // during initial render the width is 0. Hence using a default here.
   const bubbleWidth = bubble.getBoundingClientRect().width || 31;
   const left = `${(current / total) * 100}% - ${(current / total) * bubbleWidth}px`;
   bubble.innerText = `${value}`;
   const steps = {
   '--total-steps': Math.ceil((max - min) /    step),
   '--current-steps': Math.ceil((value - min) / step),
   };
   const style = Object.entries(steps).map(([varName, varValue]) => `${varName}:${varValue}`).join(';');
   bubble.style.left = `calc(${left})`;
   element.setAttribute('style', style);
   }
   // eslint-disable-next-line no-unused-vars
   export default function decorateRange(fieldDiv, field) {
   loadCSS('/blocks/form/components/range/range.css');
   const input = fieldDiv.querySelector('input');
   // modify the type in case it is not range.
   input.type = 'range';
   input.min = input.min || 1;
   // create a wrapper div to provide the min/max and current value
   const div = document.createElement('div');
   div.className = 'range-widget-wrapper';
   input.after(div);
   const hover = document.createElement('span');
   hover.className = 'range-bubble';
   const rangeMinEl = document.createElement('span');
   rangeMinEl.className = 'range-min';
   const rangeMaxEl = document.createElement('span');
   rangeMaxEl.className = 'range-max';
   rangeMinEl.innerText = `${input.min || 1}`;
   rangeMaxEl.innerText = `${input.max}`;
   div.appendChild(hover);
   // move the input element within the wrapper div
   div.appendChild(input);
   div.appendChild(rangeMinEl);
   div.appendChild(rangeMaxEl);
   input.addEventListener('input', (e) => {
       updateBubble(e.target, div);
   });
   updateBubble(input, div);
   // as a best practice add a custom css class to apply custom styling
   fieldDiv.classList.add('decorated');
   return fieldDiv;    
   }
   ```

1. Guarde los cambios.

### Insertar el decorador en el bloque de formularios

`[Form Block]` utiliza un HTML semántico para procesar los campos del formulario, incluidos los campos de entrada, etiquetas y texto de ayuda, con atributos estándar para accesibilidad. Para que `[Form Block]` use un decorador personalizado para el componente especificado, defínalo en el archivo `mappings.js`. El archivo `mappings.js` importa una función que devuelve el módulo responsable de decorar un componente en particular. La función toma las propiedades del campo y devuelve la función de decorador para el campo del formulario.

En nuestro caso, la función comprueba la propiedad `fieldType` del campo y devuelve el decorador de intervalo personalizado del archivo `range.js` presente en `[../Form Block/components]`.

Para insertar el decorador en el bloque de formularios:

1. Vaya a `[../Form Block/]` y abra `mapping.js`.
1. Añada la siguiente línea de código:

   ```javascript
   export default async function componentDecorator(fd) {
   const { ':type': type = '', fieldType } = fd;
   .... existing code ....
   if (fieldType === 'range') {
   const module = await import('./components/range.js');
   return module.default(element,fd);
   }
    return null; // null should be returned to use the original markup
   }
   ```

1. Guarde los cambios.

### Añadir estilo para el componente en el archivo CSS

Puede cambiar la apariencia de los campos del formulario según el tipo de campo y los nombres de campo mediante selectores CSS, lo que permitirá aplicar un estilo coherente o único en función de los requisitos. Para aplicar estilo al componente, añada código al archivo `form.css` para modificar la apariencia del componente del formulario.

Para personalizar el estilo del componente `range`, incluya un fragmento de código CSS que aplique estilos a un elemento de entrada `range` y a sus componentes asociados dentro de un formulario. Esto supone un diseño de HTML estructurado con clases como `.form` y `.range-wrapper`.

Para añadir estilos a un componente en el archivo CSS:

1. Vaya a `[../Form Block/]` y abra `form.css`.
1. Añada la siguiente línea de código:

   ```javascript
       /** styling for range */
   main .form .range-wrapper.decorated input[type="range"] {
   margin: unset;
   padding: unset;
   appearance: none;
   height: 5px;
   border-radius: 5px;
   border: none;
   background-image: linear-gradient(to right, var(--button-primary-color) calc(100% * var(--current-steps)/var(--total-steps)), #C5C5C5 calc(100% * var(--current-steps)/var(--total-steps)));
   }
   
   main .form .range-wrapper.decorated input[type="range"]:focus {
   outline: none;
   }
   
   .range-wrapper.decorated input[type="range"]::-webkit-slider-thumb {
   appearance: none;
   width: 25px;
   height: 25px;
   border-radius: 50%;
   background: #fff;
   border: 3px solid var(--button-primary-color);
   cursor: pointer;
   outline: 3px solid #fff;
   }
   
   .range-wrapper.decorated input[type="range"]:focus::-webkit-slider-thumb {
   border-color: var(--button-primary-color);
   }
   
   .range-wrapper.decorated .range-bubble {
   color: #17252e;
   font-size: 20px;
   line-height: 28px;
   position: relative;
   display: inline-block;
   padding-bottom: 12px;
   }
   
   .range-wrapper.decorated .range-min,
   .range-wrapper.decorated .range-max {
   font-size: 14px;
   line-height: 22px;
   color: #494f50;
   margin-top: 16px;
   display: inline-block;
   }
   
   .range-wrapper.decorated .range-max {
   float: right;
   }
   ```

1. Guarde los cambios.

### Implemente los archivos y genere el proyecto

Implemente los archivos `range.js`, `mapping.js` y `form.css` actualizados en el proyecto de GitHub y compruebe que la compilación se ha realizado correctamente.

### Vista previa del formulario con AEM Sidekick

Obtenga una vista previa del formulario con la función recién implementada que aplica estilos al componente `range`.

![Formulario de componente personalizado](/help/edge/assets/custom-componet-form.png)

El nuevo estilo del componente `range` muestra los valores mínimo, máximo y seleccionado en la línea mediante la adición de estilos con CSS y una función personalizada que incluye un decorador para el componente.


