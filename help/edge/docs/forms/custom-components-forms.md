---
title: Creación de componentes personalizados para un formulario EDS
description: Creación de componentes personalizados para un formulario EDS
feature: Edge Delivery Services
hide: true
hidefromtoc: true
exl-id: 77e90657-38db-4a49-9aac-3f3774b62624
role: Admin, Architect, Developer
source-git-commit: 4356fcc73a9c33a11365b1eb3f2ebee5c9de24f0
workflow-type: tm+mt
source-wordcount: '664'
ht-degree: 4%

---

# Crear componentes personalizados

Los Edge Delivery Services de AEM Forms le permiten personalizar [los componentes de formulario nativos para HTML](/help/edge/docs/forms/form-components.md) y crear formularios interactivos y de fácil manejo. Permite modificar los componentes del formulario con marcado predefinido, tal como se explica en [Estilo de los campos de formulario](/help/edge/docs/forms/style-theme-forms.md) mediante CSS personalizado (hojas de estilo en cascada) y código personalizado para decorar el componente, lo que mejora el aspecto de los campos de formulario dentro de un bloque de Forms adaptable.

![Componente personalizado](/help/edge/assets/custom-component-image.png)

Este documento describe los pasos para crear componentes personalizados al aplicar estilo a los componentes de formulario HTML nativos para mejorar la experiencia del usuario y aumentar el atractivo visual del formulario.

Veamos un ejemplo de un componente `range` que muestra `Estimated trip cost` en un formulario. El componente `range` aparece como una línea recta, sin mostrar valores como el valor mínimo, máximo o seleccionado.

![Componente de intervalo nativo](/help/edge/assets/native-range-component.png)

Vamos a empezar a personalizar el campo `range` para mostrar los valores mínimo, máximo y seleccionado en la línea agregando estilo con CSS y agregando una función personalizada para decorar un componente.

![Componente de intervalo personalizado](/help/edge/assets/custom-range-component.png)

Al final de este artículo, aprenderá a crear componentes personalizados añadiendo estilos al archivo CSS y a la función personalizada.

## Requisitos previos

Antes de empezar a crear el componente personalizado, debe:

* Tiene conocimientos básicos de [componentes HTML nativos](/help/edge/docs/forms/form-components.md).
* Obtenga información sobre cómo [aplicar estilo a campos de formulario basados en el tipo de campo mediante selectores CSS](/help/edge/docs/forms/style-theme-forms.md)


## Crear un componente personalizado


![pasos para crear un componente personalizado](/help/edge/docs/forms/assets/steps-to-create-custom-component.png)

Ahora vamos a entender cada paso en detalle.

Consulte la [hoja de cálculo de consulta](/help/edge/docs/forms/assets/enquiry.xlsx) para personalizar el componente `range`, siguiendo los pasos que se explican a continuación.

### Añadir una función personalizada para decorar el componente

La función personalizada agregada en `[../Form Block/components]` consiste en:

* **Declaración de función**: defina el nombre de función y sus parámetros.
* **Implementación lógica**: escriba la lógica para agregar el comportamiento personalizado para el componente.
* **Exportación de funciones**: haga accesible la función en `[Form Block]`.

Vamos a crear un archivo de JavaScript denominado `range.js` para aplicar estilo al componente de intervalo. Para agregar una función personalizada:

1. AEM Vaya a la carpeta Proyecto de la carpeta de la carpeta de la carpeta de la unidad de Google o de SharePoint.
1. Vaya a `[../Form Block/components]`.
1. Agregue un nuevo archivo de nombre `range.js`.
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

### Inyectar el decorador en el bloque de formulario

`[Form Block]` utiliza un HTML semántico para procesar campos de formulario, incluidos campos de entrada, rótulos y texto de ayuda, con atributos estándar para la accesibilidad. Para que `[Form Block]` use un decorador personalizado para un componente especificado, defina el componente en el archivo `mappings.js`. El archivo `mappings.js` importa una función que devuelve el módulo responsable de decorar un componente en particular. La función toma las propiedades del campo y devuelve una función decoradora para el campo de formulario.

En nuestro caso, la función comprueba la propiedad `fieldType` del campo y devuelve el decorador de intervalo personalizado del archivo `range.js` presente en `[../Form Block/components]`.

Para insertar el decorador en el bloque de formulario:

1. Vaya a `[../Form Block/]` y abra `mapping.js`.
1. Añada la siguiente línea de código:

   ```javascript
   export default async function componentDecorator(fd) {
   const { ':type': type = '', fieldType } = fd;
   .... existing code ....
   if (fieldType === 'range') {
   const module = await import('./components/range.js');
   return module.default;
   }
    return null; // null should be returned to use the original markup
   }
   ```

1. Guarde los cambios.

### Añadir estilo para el componente en el archivo CSS

Puede cambiar el aspecto de los campos de formulario en función del tipo de campo y los nombres de campo mediante selectores CSS, lo que permite aplicar un estilo coherente o único en función de los requisitos. Para aplicar estilo al componente, agregue código al archivo `form.css` para modificar el aspecto del componente del formulario.

Para personalizar el estilo del componente `range`, incluya un fragmento de código CSS que aplique estilo a un elemento de entrada `range` y a sus componentes asociados dentro de un formulario. Esto supone un diseño de HTML estructurado con clases como `.form` y `.range-wrapper`.

Para añadir estilo a un componente en el archivo CSS:
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

Implemente los archivos actualizados `range.js`, `mapping.css` y `form.css` en su proyecto de GitHub y verifique que la compilación se haya realizado correctamente.

### AEM Vista previa del formulario con la barra de tareas de la

Use [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content) para obtener una vista previa del formulario con la función recién implementada que aplica estilo al componente `range`.

![Formulario de componente personalizado](/help/edge/assets/custom-componet-form.png)

El nuevo estilo del componente `range` muestra los valores mínimo, máximo y seleccionado en la línea al agregar estilos mediante CSS y una función personalizada que incluye un decorador para el componente.


## Ver también

{{see-more-forms-eds}}



