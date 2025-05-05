---
title: Creación de componentes personalizados para un formulario EDS
description: Creación de componentes personalizados para un formulario EDS
feature: Edge Delivery Services
role: Admin, Architect, Developer
exl-id: 2bbe3f95-d5d0-4dc7-a983-7a20c93e2906
source-git-commit: 9127c58a72dc4942312907f9e8f0cdcc8de9aa4b
workflow-type: tm+mt
source-wordcount: '1773'
ht-degree: 98%

---

# Generación de componentes personalizados en creación de WYSIWYG

<span class="preview"> Esta función está disponible a través del programa de acceso rápido. Para solicitar acceso, envíe un correo electrónico con el nombre de su organización de GitHub y el nombre del repositorio desde su dirección oficial a <a href="mailto:aem-forms-ea@adobe.com">aem-forms-ea@adobe.com</a> . Por ejemplo, si la URL del repositorio es https://github.com/adobe/abc, el nombre de la organización es adobe y el nombre del repositorio es abc.</span>


Los formularios de Edge Delivery Services ofrecen personalización, lo que permite a los desarrolladores front-end generar componentes de formulario personalizados. Estos componentes personalizados se integran a la perfección en la experiencia de creación de WYSIWYG, lo que permite a los autores de formularios añadirlos, configurarlos y administrarlos fácilmente dentro del editor de formularios. Con los componentes personalizados, los autores pueden mejorar la funcionalidad a la vez que garantizan un proceso de creación fluido e intuitivo.

Este documento describe los pasos para crear componentes personalizados mediante la aplicación de estilos a los componentes de formulario HTML nativos para mejorar la experiencia del usuario y aumentar el atractivo visual del formulario.

## Requisitos previos

Antes de empezar a crear el componente personalizado, debe:

* Tener conocimientos básicos sobre los [componentes HTML nativos](/help/edge/docs/forms/form-components.md).
* Saber cómo [aplicar estilos a los campos del formulario basados en el tipo de campo mediante selectores CSS](/help/edge/docs/forms/style-theme-forms.md)

## Creación de un componente personalizado

Añadir un componente personalizado en el Editor universal significa que hay un nuevo componente disponible para que los autores de formularios lo utilicen al diseñar formularios. Esto implica registrar el componente, definir sus propiedades y configurar dónde se puede usar. Los pasos para crear componentes personalizados son los siguientes:

[1. Añadir estructura para el nuevo componente personalizado](#1-adding-structure-for-new-custom-component)
[2. Definir las propiedades del componente personalizado para la creación](#2-defining-the-properties-of-your-custom-component-for-authoring)
[3.  Hacer visible el componente personalizado en la lista de componentes de WYSIWYG](#3-making-your-custom-component-visible-in-the-wysiwyg-component-list)
[4. Registrar el componente personalizado](#4-registering-your-custom-component)
[5. Agregar el comportamiento de tiempo de ejecución para el componente personalizado](#5-adding-the-runtime-behaviour-for-your-custom-component)

Veamos un ejemplo de creación de un nuevo componente personalizado denominado **rango**. El componente de rango aparece como una línea recta, sin mostrar valores como el valor mínimo, máximo o seleccionado.

![Estilo del componente de rango](/help/edge/docs/forms/universal-editor/assets/custom-component-range-style.png)

Al final de este artículo, aprenderá a crear componentes personalizados desde cero.

### 1. Añadir una estructura para el nuevo componente personalizado

Para poder utilizar un componente personalizado, debe registrarse para que el Editor universal lo reconozca como una opción disponible. Esto se logra a través de una definición de componente, que incluye un identificador único, propiedades predeterminadas y la estructura del componente. Realice los siguientes pasos para que el componente personalizado esté disponible para la creación de formularios:

1. **Añadir carpetas y archivos nuevos**
Agregue carpetas y archivos nuevos para el nuevo componente personalizado en su proyecto de AEM.
   1. Abra el proyecto de AEM y navegue hasta `../blocks/form/components/`.
   1. Añada una carpeta nueva para el componente personalizado en `../blocks/form/components/<component_name>`. En este ejemplo, creamos una carpeta denominada `range`.
   1. Vaya a la carpeta recién creada en `../blocks/form/components/<component_name>`. Por ejemplo, vaya a `../blocks/form/components/range` y agregue los siguientes archivos:
      * `/blocks/form/components/range/_range.json`: contiene la definición del componente personalizado.
      * `../blocks/form/components/range/range.css`: define el estilo del componente personalizado.
      * `../blocks/form/components/range/range.js`: personaliza el componente personalizado durante la ejecución.

        ![Adición del componente personalizado para la creación](/help/edge/docs/forms/universal-editor/assets/adding-custom-component.png)

        >[!NOTE]
        >
        > Asegúrese de que el archivo JSON incluye un guion bajo (_) como prefijo en su nombre de archivo.

1. Vaya al archivo `/blocks/form/components/range/_range.json` y agregue la definición del componente para el componente personalizado.

1. **Adición de la definición del componente**

   Para añadir la definición, los campos que deben agregarse en el archivo `_range.json` son los siguientes:

   * **title**: el título del componente que se muestra en el Editor universal.
   * **id**: un identificador único del componente.
   * **fieldType**: los formularios admiten varios **fieldType** para capturar tipos específicos de entradas de usuario. Puede encontrar el [fieldType admitido en la sección Byte adicional](#supported-fieldtypes).
   * **resourceType**: cada componente personalizado tiene asociado un tipo de recurso basado en su fieldType. Puede encontrar el [resourceType admitido en la sección Byte adicional](#supported-resourcetype).
   * **jcr:title**: es similar a un título, pero se almacena dentro de la estructura del componente.
   * **fd:viewType**: representa el nombre del componente personalizado. Es el identificador único del componente. Es necesario crear una vista personalizada para el componente.

El archivo `_range.json`, después de agregar la definición del componente, es el siguiente:

```javascript
{
  "definitions": [
    {
      "title": "Range",
      "id": "range",
      "plugins": {
        "xwalk": {
          "page": {
            "resourceType": "core/fd/components/form/numberinput/v1/numberinput",
            "template": {
              "jcr:title": "Range",
              "fieldType": "number-input",
              "fd:viewType": "range",
              "enabled": true,
              "visible": true
            }
          }
        }
      }
    }
  ]
}
```

>[!NOTE]
>
> Todos los componentes relacionados con formularios siguen el mismo enfoque que los sitios al añadir bloques al Editor universal. Consulte el artículo [Creación de bloques instrumentados para su uso con el Editor universal](https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/edge-delivery/wysiwyg-authoring/create-block) para obtener más información.

### 2. Definir las propiedades del componente personalizado para la creación

El componente personalizado incluye un modelo de componente que especifica qué propiedades puede configurar el autor del formulario. Estas propiedades aparecen en el cuadro de diálogo **Propiedades** del Editor universal, lo que permite a los autores ajustar la configuración, como etiquetas, reglas de validación, estilos y otros atributos. Para definir propiedades:

1. Vaya al archivo `/blocks/form/components/range/_range.json` y agregue el modelo de componente para el componente personalizado.

1. **Adición del modelo de componente**

   Para definir el modelo de componente para el componente personalizado, debe añadir los campos relevantes al archivo `_range.json`.

   1. **Creación de un nuevo modelo**

      * En la matriz de modelos, añada un nuevo objeto y establezca el `id` del modelo de componente para que coincida con la propiedad `fd:viewType` configurada antes en la definición del componente.
      * Incluya una matriz de campos dentro de este objeto.

   2. **Definición de campos para el cuadro de diálogo Propiedad**

      * Cada objeto de la matriz de campos debe ser un componente de tipo contenedor, lo que permite que aparezca como una pestaña en el cuadro de diálogo **Propiedad**.
      * Algunos campos pueden hacer referencia a propiedades reutilizables disponibles en `models/form-common`.

   3. **Uso de un modelo de componente existente como referencia**

      * Puede copiar el contenido de un modelo de componente existente que corresponda a su `fieldType` elegido y modificarlo según sea necesario. Por ejemplo, el componente `number-input` se ha ampliado para crear un componente de **rango**, de modo que podemos usar la matriz de modelos de `models/form-components/_number-input.json` como referencia.

   El archivo `_range.json`, después de agregar el modelo de componente, es el siguiente:

   ```javascript
   "models": [
   {
     "id": "range",
     "fields": [
       {
         "component": "container",
         "name": "basic",
         "label": "Basic",
         "collapsible": false,
         "...": "../../../../models/form-common/_basic-input-fields.json"
       },
       {
         "...": "../../../../models/form-common/_help-container.json"
       },
       {
         "component": "container",
         "name": "validation",
         "label": "Validation",
         "collapsible": true,
         "...": "../../../../models/form-common/_number-validation-fields.json"
       }
     ]
   }
   ]
   ```

   >[!NOTE]
   >
   > Para agregar un nuevo campo al cuadro de diálogo **Propiedad** de un componente personalizado, respete el [esquema definido](https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/implementing/developing/universal-editor/field-types#loading-model).

   También puede [añadir propiedades personalizadas](#adding-custom-properties-for-your-custom-component) a un componente personalizado para ampliar su funcionalidad.

#### Adición de propiedades personalizadas al componente personalizado

Las propiedades personalizadas permiten definir comportamientos específicos basados en los valores establecidos en el cuadro de diálogo Propiedad de un componente. Esto ayuda a ampliar las opciones de funcionalidad y personalización del componente.

En este ejemplo, agregamos Valor de paso como propiedad personalizada al componente de rango.

![Propiedad personalizada con Valor de paso](/help/edge/docs/forms/universal-editor/assets/customcomponent-stepvalue.png)

Para añadir la propiedad personalizada Valor de paso, anexe el modelo de componente con las siguientes líneas de código en el archivo ` _<component>.json`:

```javascript
      {
      "component": "number",
      "name": "stepValue",
      "label": "Step Value",
      "valueType": "number"
      }
```

El fragmento JSON define una propiedad personalizada llamada **Valor de paso** para un componente de **rango**. A continuación se muestra un desglose de cada campo:

* **component**: especifica el tipo de campo de entrada utilizado en el cuadro de diálogo Propiedad. En este caso, `number` indica que el campo acepta valores numéricos.
* **name**: el identificador de la propiedad, usado para hacer referencia a ella en la lógica del componente. En este caso, `stepValue` representa la configuración del valor de paso para el intervalo.
* **label**: el nombre para mostrar de la propiedad tal como se ve en el cuadro de diálogo Propiedad.
* **valueType**: define el tipo de dato esperado para la propiedad. `number` garantiza que solo se permitan entradas numéricas.

Ahora puede usar `stepValue` como propiedad personalizada en las propiedades JSON de `range.js` e implementar un comportamiento dinámico basado en su valor durante la ejecución.

Por lo tanto, el archivo `_range.json` final, después de añadir la definición del componente, el modelo del componente y las propiedades personalizadas, es el siguiente:

```javascript
 {
  "definitions": [
    {
      "title": "Range",
      "id": "range",
      "plugins": {
        "xwalk": {
          "page": {
            "resourceType": "core/fd/components/form/numberinput/v1/numberinput",
            "template": {
              "jcr:title": "Range",
              "fieldType": "number-input",
              "fd:viewType": "range",
              "enabled": true,
              "visible": true
            }
          }
        }
      }
    }
  ],
  "models": [
    {
      "id": "range",
      "fields": [
        {
          "component": "container",
          "name": "basic",
          "label": "Basic",
          "collapsible": false,
          "...": "../../../../models/form-common/_basic-input-fields.json"
         {
           "component": "number",
           "name": "stepValue",
            "label": "Step Value",
             "valueType": "number"
}
        },
        {
          "...": "../../../../models/form-common/_help-container.json"
        },
        {
          "component": "container",
          "name": "validation",
          "label": "Validation",
          "collapsible": true,
          "...": "../../../../models/form-common/_number-validation-fields.json"
        }
      ]
    }
  ]
}
```

![definición y modelo del componente](/help/edge/docs/forms/universal-editor/assets/custom-component-json-file.png)


### 3. Hacer visible el componente personalizado en la lista de componentes de WYSIWYG

Un filtro define en qué sección se puede utilizar el componente personalizado en el Editor universal. Esto garantiza que el componente solo se pueda usar en las secciones adecuadas, lo que mantiene la estructura y la facilidad de uso.

Para asegurarse de que el componente personalizado aparece en la lista de componentes disponibles durante la creación de formularios en WYSIWYG:

1. Navegue hasta el archivo `/blocks/form/_form.json`.
1. Busque la matriz de componentes dentro del objeto que tiene `id="form"`.
1. Agregue el valor `fd:viewType` de `definitions[]` a la matriz de componentes del objeto con `id="form"`.

```javascript
 "filters": [
    {
      "id": "form",
      "components": [
        "captcha",
        "checkbox",
        "checkbox-group",
        "date-input",
        "drop-down",
        "email",
        "file-input",
        "form-accordion",
        "form-button",
        "form-fragment",
        "form-image",
        "form-modal",
        "form-reset-button",
        "form-submit-button",
        "number-input",
        "panel",
        "plain-text",
        "radio-group",
        "rating",
        "telephone-input",
        "text-input",
        "tnc",
        "wizard",
        "range"
      ]
    }
  ]
```

![filtro de componente](/help/edge/docs/forms/universal-editor/assets/custom-component-form-file.png)

### 4. Registro del componente personalizado

Para habilitar que el bloque de formulario reconozca el componente personalizado y cargue sus propiedades definidas en el modelo de componente durante la creación del formulario, añada el valor `fd:viewType` de la definición del componente al archivo `mappings.js`.
Para registrar un componente:
1. Navegue hasta el archivo `/blocks/form/mappings.js`.
1. Localice la matriz `customComponents[]`.
1. Agregue el valor `fd:viewType` de la matriz `definitions[]` a la matriz `customComponents[]`.

```javascript
let customComponents = ["range"];
const OOTBComponentDecorators = ['file-input',
                                 'wizard', 
                                 'modal', 'tnc',
                                'toggleable-link',
                                'rating',
                                'datetime',
                                'list',
                                'location',
                                'accordion'];
```

![asignación de componentes](/help/edge/docs/forms/universal-editor/assets/custom-component-mapping-file.png)

Después de completar los pasos anteriores, el componente personalizado aparece en la lista de componentes del formulario en el Editor universal. A continuación, puede arrastrarlo y soltarlo en la sección del formulario.

![componente de rango](/help/edge/docs/forms/universal-editor/assets/custom-component-range.png)

La captura de pantalla siguiente muestra las propiedades del componente `range` agregado al modelo de componentes, que especifica las propiedades que el autor del formulario puede configurar:

![Propiedades del componente de rango](/help/edge/docs/forms/universal-editor/assets/range-properties.png)

Ahora puede definir el comportamiento en tiempo de ejecución del componente personalizado añadiendo estilo y funcionalidad.

### 5. Añadir el comportamiento de tiempo de ejecución para el componente personalizado

Puede modificar los componentes personalizados mediante marcado predefinido, tal como se explica en [Estilo de los campos de formulario](/help/edge/docs/forms/style-theme-forms.md). Esto se puede lograr con CSS personalizado (hojas de estilo en cascada) y código personalizado para mejorar el aspecto del componente. Añada el comportamiento de tiempo de ejecución del componente:

1. Para agregar el estilo, vaya al archivo `/blocks/form/components/range/range.css` y añada la siguiente línea de código:

   ```javascript
   /** Styling for range */
   main .form .range-widget-wrapper.decorated input[type="range"] {
   margin: unset;
   padding: unset;
   appearance: none;
   height: 5px;
   border-radius: 5px;
   border: none;
   background-image: linear-gradient(to right, #ADD8E6 calc(100% * var(--current-steps)/var(--total-steps)), #C5C5C5 calc(100% * var(--current-steps)/var(--total-steps)));
   }
   
   main .form .range-widget-wrapper.decorated input[type="range"]:focus {
   outline: none;
   }
   
   .range-widget-wrapper.decorated input[type="range"]::-webkit-slider-thumb {
   appearance: none;
   width: 25px;
   height: 25px;
   border-radius: 50%;
   background: #00008B; /* Dark Blue */
   border: 3px solid #00008B; /* Dark Blue */
   cursor: pointer;
   outline: 3px solid #fff;
   }
   
   .range-widget-wrapper.decorated input[type="range"]:focus::-webkit-slider-thumb {
   border-color: #00008B; /* Dark Blue */
   }
   
   .range-widget-wrapper.decorated .range-bubble {
   color: #00008B; /* Dark Blue */
   font-size: 20px;
   line-height: 28px;
   position: relative;
   display: inline-block;
   padding-bottom: 12px;
   font-weight: bold;
   }
   
   .range-widget-wrapper.decorated .range-min,
   .range-widget-wrapper.decorated .range-max {
   font-size: 14px;
   line-height: 22px;
   color: #494f50;
   margin-top: 16px;
   display: inline-block;
   }
   
   .range-widget-wrapper.decorated .range-max {
   float: right;
   }
   ```

   El código le ayuda a definir el estilo y el aspecto visual del componente personalizado.

1. Para agregar la funcionalidad, vaya al archivo `/blocks/form/components/range/range.js` y añada la línea de código siguiente:

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
       '--total-steps': Math.ceil((max - min) / step),
       '--current-steps': Math.ceil((value - min) / step),
   };
   const style = Object.entries(steps).map(([varName, varValue]) => `${varName}:${varValue}`).join(';');
   bubble.style.left = `calc(${left})`;
   element.setAttribute('style', style);
   }
   
   export default async function decorate(fieldDiv, fieldJson) {
   console.log('RANGE DIV: ', fieldDiv);
   console.log('RANGE JSON: fieldJson', fieldJson);
    const input = fieldDiv.querySelector('input');
   // modify the type in case it is not range.
   input.type = 'range';
   input.min = input.min || 10;
   input.max = input.max || 1000;
   // create a wrapper div to provide the min/max and current value
   const div = document.createElement('div');
   div.className = 'range-widget-wrapper decorated';
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
   return fieldDiv;
   }
   ```

   Controla la manera en que el componente personalizado interactúa con las entradas del usuario, procesa los datos e integra el bloque de formulario en el Editor universal.

   Después de incorporar un estilo y una funcionalidad personalizados, se mejora el aspecto y el comportamiento del componente de rango. El diseño actualizado refleja los estilos aplicados, mientras que la funcionalidad añadida garantiza una experiencia del usuario más dinámica e interactiva.
La siguiente captura de pantalla ilustra el componente de rango actualizado.

![Estilo del componente de rango](/help/edge/docs/forms/universal-editor/assets/custom-component-range-1.png)

## Preguntas frecuentes

* **Si añado estilo tanto en component.css como en forms.css, ¿cuál tiene prioridad?**
Cuando los estilos se definen en `component.css` y en **forms.css**, `component.css` tiene prioridad. Esto se debe a que los estilos de nivel de componente son más específicos y anulan los estilos globales de `forms.css`.

* **Mi componente personalizado no está visible en la lista de componentes disponibles en el Editor universal. ¿Cómo puedo arreglarlo?**
Si el componente personalizado no aparece, compruebe los siguientes archivos para asegurarse de que el componente esté registrado correctamente:
   * **component-definition.json**: compruebe que el componente esté definido correctamente.
   * **component-filters.json**: asegúrese de que el componente esté permitido en las secciones adecuadas.
   * **component-models.json**: confirme que el modelo de componente está configurado correctamente.

## Prácticas recomendadas

* Se recomienda [configurar un entorno de desarrollo de AEM local](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#set-up-local-aem-development-environment) para desarrollar estilos y componentes personalizados localmente.


## Byte adicional

### resourceType admitido

| Tipo de campo | Tipo de medio |
|--------------|------------------------------------------------------------------|
| text-input | core/fd/components/form/textinput/v1/textinput |
| number-input | core/fd/components/form/numberinput/v1/numberinput |
| date-input | core/fd/components/form/datepicker/v1/datepicker |
| panel | core/fd/components/form/panelcontainer/v1/panelcontainer |
| checkbox | core/fd/components/form/checkbox/v1/checkbox |
| drop-down | core/fd/components/form/dropdown/v1/dropdown |
| radio-group | core/fd/components/form/radiobutton/v1/radiobutton |
| plain-text | core/fd/components/form/text/v1/text |
| file-input | core/fd/components/form/fileinput/v2/fileinput |
| email | core/fd/components/form/emailinput/v1/emailinput |
| image | core/fd/components/form/image/v1/image |
| button | core/fd/components/form/button/v1/button |

### fieldTypes admitidos

Los tipos de campo admitidos para los formularios son los siguientes:
* text-input
* number-input
* date-input
* panel
* checkbox
* drop-down
* radio-group
* plain-text
* file-input
* email
* image
* button

## Consulte también

{{universal-editor-see-also}}
