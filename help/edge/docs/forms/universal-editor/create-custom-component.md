---
title: Creación de componentes personalizados para un formulario EDS
description: Creación de componentes personalizados para un formulario EDS
feature: Edge Delivery Services
hide: true
hidefromtoc: true
role: Admin, Architect, Developer
exl-id: 2bbe3f95-d5d0-4dc7-a983-7a20c93e2906
source-git-commit: bf70adcb95ddf88d0ea9a496efe3ae47f71f6a1d
workflow-type: tm+mt
source-wordcount: '1725'
ht-degree: 5%

---

# Crear componentes personalizados en WYSIWYG Authoring

Edge Delivery Services Forms ofrece personalización, lo que permite a los desarrolladores de front-end crear componentes de formulario personalizados. Estos componentes personalizados se integran perfectamente en la experiencia de creación de WYSIWYG, lo que permite a los autores de formularios añadirlos, configurarlos y administrarlos fácilmente dentro del editor de formularios. Con los componentes personalizados, los autores pueden mejorar la funcionalidad a la vez que garantizan un proceso de creación suave e intuitivo.

Este documento describe los pasos para crear componentes personalizados mediante la aplicación de estilos a los componentes de formulario HTML nativos para mejorar la experiencia del usuario y aumentar el atractivo visual del formulario.

## Requisitos previos

Antes de empezar a crear el componente personalizado, debe:

* Tener conocimientos básicos sobre los [componentes HTML nativos](/help/edge/docs/forms/form-components.md).
* Saber cómo [aplicar estilos a los campos del formulario basados en el tipo de campo mediante selectores CSS](/help/edge/docs/forms/style-theme-forms.md)

## Creación de un componente personalizado

Añadir un componente personalizado en el editor universal significa que hay un nuevo componente disponible para que los autores de formularios lo utilicen al diseñar formularios. Esto implica registrar el componente, definir sus propiedades y configurar dónde se puede utilizar. Los pasos para crear componentes personalizados son los siguientes:

[1. Agregando estructura para el nuevo componente personalizado ](#1-adding-structure-for-new-custom-component)
[2. Definir las propiedades del componente personalizado para la creación ](#2-defining-the-properties-of-your-custom-component-for-authoring)
[3.  Hacer visible el componente personalizado en la lista de componentes de WYSIWYG](#3-making-your-custom-component-visible-in-the-wysiwyg-component-list)
[4. Registrando el componente personalizado ](#4-registering-your-custom-component)
[5. Agregando el comportamiento de tiempo de ejecución para el componente personalizado ](#5-adding-the-runtime-behaviour-for-your-custom-component)

Veamos un ejemplo de creación de un nuevo componente personalizado denominado **rango**. El componente de rango aparece como una línea recta y muestra valores como el valor mínimo, máximo o seleccionado.

![Estilo de componente de rango](/help/edge/docs/forms/universal-editor/assets/custom-component-range-style.png)

Al final de este artículo, aprenderá a crear componentes personalizados desde cero.

### 1. Agregar una estructura para el nuevo componente personalizado

Para poder utilizar un componente personalizado, debe registrarse para que el Editor universal lo reconozca como una opción disponible. Esto se logra a través de una definición de componente, que incluye un identificador único, propiedades predeterminadas y la estructura del componente. Realice los siguientes pasos para que el componente personalizado esté disponible para la creación de formularios:

1. **Agregar carpeta y archivos nuevos**
Agregue carpetas y archivos nuevos para el nuevo componente personalizado en su proyecto de AEM.
   1. Abra el proyecto de AEM y vaya a `../blocks/form/components/`.
   1. Agregue una carpeta nueva para el componente personalizado en `../blocks/form/components/<component_name>`. En este ejemplo, creamos una carpeta denominada `range`.
   1. Vaya a la carpeta recién creada en `../blocks/form/components/<component_name>`. Por ejemplo, vaya a `../blocks/form/components/range` y agregue los siguientes archivos:
      * `/blocks/form/components/range/_range.json`: contiene la definición del componente personalizado.
      * `../blocks/form/components/range/range.css`: define el estilo del componente personalizado.
      * `../blocks/form/components/range/range.js`: personaliza el componente personalizado durante la ejecución.

        ![Agregando el componente personalizado para la creación](/help/edge/docs/forms/universal-editor/assets/adding-custom-component.png)

        >[!NOTE]
        >
        > Asegúrese de que el archivo json incluye un guion bajo (_) como prefijo en su nombre de archivo.

1. Vaya al archivo `/blocks/form/components/range/_range.json` y agregue la definición del componente para el componente personalizado.

1. **Agregar la definición del componente**

   Para agregar la definición, los campos que deben agregarse en el archivo `_range.json` son:

   * **título**: El título del componente que se muestra en el editor universal.
   * **id**: Un identificador único del componente.
   * **fieldType**: Forms admite varios **fieldType** para capturar tipos específicos de entradas de usuario. Puede encontrar el fieldType [admitido en la sección Byte adicional](#supported-fieldtypes).
   * **resourceType**: cada componente personalizado tiene asociado un tipo de recurso basado en su fieldType. Puede encontrar el resourceType [admitido en la sección Byte adicional](#supported-resourcetype).
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
> Todos los componentes relacionados con formularios siguen el mismo enfoque que Sites al agregar bloques al Editor universal. Puede consultar el artículo [Creación de bloques instrumentados para usar con el editor universal](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/edge-delivery/wysiwyg-authoring/create-block) para obtener más información.

### 2. Definición de las propiedades del componente personalizado para la creación

El componente personalizado incluye un modelo de componente que especifica qué propiedades puede configurar el autor del formulario. Estas propiedades aparecen en el cuadro de diálogo **Propiedades** del Editor universal, lo que permite a los autores ajustar la configuración, como etiquetas, reglas de validación, estilos y otros atributos. Para definir propiedades:

1. Vaya al archivo `/blocks/form/components/range/_range.json` y agregue el modelo de componente para el componente personalizado.

1. **Agregar el modelo de componente**

   Para definir el modelo de componente para el componente personalizado, debe agregar los campos relevantes al archivo `_range.json`.

   1. **Crear nuevo modelo**

      * En la matriz de modelos, agregue un nuevo objeto y establezca `id` del modelo de componente para que coincida con la propiedad `fd:viewType` configurada anteriormente en la definición del componente.
      * Incluya una matriz de campos dentro de este objeto.

   2. **Definir campos para el cuadro de diálogo Propiedad**

      * Cada objeto de la matriz de campos debe ser un componente de tipo contenedor, lo que permite que aparezca como una ficha en el cuadro de diálogo **Propiedad**.
      * Algunos campos pueden hacer referencia a propiedades reutilizables disponibles en `models/form-common`.

   3. **Usar un modelo de componente existente como referencia**

      * Puede copiar el contenido de un modelo de componentes existente que corresponda a su `fieldType` elegido y modificarlo según sea necesario. Por ejemplo, el componente `number-input` se ha ampliado para crear un componente **range**, de modo que podemos usar la matriz de modelos de `models/form-components/_number-input.json` como referencia.

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
   > Para agregar un nuevo campo al cuadro de diálogo **Propiedad** de un componente personalizado, adhiera al [esquema definido](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/developing/universal-editor/field-types#loading-model).

   También puede [agregar propiedades personalizadas](#adding-custom-properties-for-your-custom-component) a un componente personalizado para ampliar su funcionalidad.

#### Añadir propiedades personalizadas al componente personalizado

Las propiedades personalizadas permiten definir comportamientos específicos basados en los valores establecidos en el cuadro de diálogo Propiedad de un componente. Esto ayuda a ampliar las opciones de funcionalidad y personalización del componente.

En este ejemplo, agregamos Step Value como propiedad personalizada al componente Range.

![Propiedad personalizada con valor de paso](/help/edge/docs/forms/universal-editor/assets/customcomponent-stepvalue.png)

Para agregar la propiedad personalizada Valor del paso, anexe el modelo de componente con las siguientes líneas de código en el archivo ` _<component>.json`:

```javascript
      {
      "component": "number",
      "name": "stepValue",
      "label": "Step Value",
      "valueType": "number"
      }
```

El fragmento JSON define una propiedad personalizada llamada **Valor de paso** para un componente **Range**. A continuación se muestra un desglose de cada campo:

* **componente**: especifica el tipo de campo de entrada utilizado en el cuadro de diálogo Propiedad. En este caso, `number` indica que el campo acepta valores numéricos.
* **name**: El identificador de la propiedad, usado para hacer referencia a ella en la lógica del componente. En este caso, `stepValue` representa la configuración del valor de paso para el intervalo.
* **label**: el nombre para mostrar de la propiedad tal como se ve en el cuadro de diálogo Propiedad.
* **valueType**: define el tipo de datos esperado para la propiedad. `number` garantiza que solo se permiten entradas numéricas.

Ahora puede usar `stepValue` como propiedad personalizada en las propiedades JSON de `range.js` e implementar un comportamiento dinámico basado en su valor durante la ejecución.

Por lo tanto, el archivo `_range.json` final, después de agregar la definición del componente, el modelo del componente y las propiedades personalizadas, es el siguiente:

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

Un filtro define en qué sección se puede utilizar el componente personalizado en el Editor universal. Esto garantiza que el componente solo se pueda utilizar en secciones adecuadas, manteniendo la estructura y la facilidad de uso.

Para asegurarse de que el componente personalizado aparece en la lista de componentes disponibles durante la creación de formularios en WYSIWYG:

1. Vaya al archivo `/blocks/form/_form.json`.
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

Para permitir que el bloque de formulario reconozca el componente personalizado y cargue sus propiedades definidas en el modelo de componente durante la creación del formulario, agregue el valor `fd:viewType` de la definición del componente al archivo `mappings.js`.
Para registrar un componente:
1. Vaya al archivo `/blocks/form/mappings.js`.
1. Busque la matriz `customComponents[]`.
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

La captura de pantalla siguiente muestra las propiedades del componente `range` agregado al modelo de componentes, que especifica las propiedades que el autor del formulario puede configurar.:

![Propiedades del componente de intervalo](/help/edge/docs/forms/universal-editor/assets/range-properties.png)

Ahora puede definir el comportamiento en tiempo de ejecución del componente personalizado añadiendo estilo y funcionalidad.

### 5. Añadir el comportamiento de tiempo de ejecución para el componente personalizado

Puede modificar los componentes personalizados mediante marcado predefinido, tal como se explica en [Estilo de los campos de formulario](/help/edge/docs/forms/style-theme-forms.md). Esto se puede lograr con CSS personalizado (hojas de estilo en cascada) y código personalizado para mejorar el aspecto del componente. Para agregar el comportamiento en tiempo de ejecución para el componente:

1. Para agregar el estilo, vaya al archivo `/blocks/form/components/range/range.css` y agregue la siguiente línea de código:

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

1. Para agregar la funcionalidad, vaya al archivo `/blocks/form/components/range/range.js` y agregue la línea de código siguiente:

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

   Controla la manera en que el componente personalizado interactúa con las entradas del usuario, procesa los datos e integra el bloque de formulario en el editor universal.

   Después de incorporar un estilo y una funcionalidad personalizados, se mejora el aspecto y el comportamiento del componente de intervalo. El diseño actualizado refleja los estilos aplicados, mientras que la funcionalidad añadida garantiza una experiencia de usuario más dinámica e interactiva.
La siguiente captura de pantalla ilustra el componente de intervalo actualizado.

![Estilo de componente de rango](/help/edge/docs/forms/universal-editor/assets/custom-component-range-1.png)

## Pregunta más frecuente

* **Si agrego estilo tanto en component.css como en forms.css, ¿cuál tiene prioridad?**
Cuando los estilos se definen en `component.css` y **forms.css**, `component.css` tiene prioridad. Esto se debe a que los estilos de nivel de componente son más específicos y anulan los estilos globales de `forms.css`.

* **Mi componente personalizado no está visible en la lista de componentes disponibles en el Editor universal. ¿Cómo puedo arreglar esto?**
Si el componente personalizado no aparece, compruebe los siguientes archivos para asegurarse de que el componente esté registrado correctamente:
   * **component-definition.json**: compruebe que el componente esté definido correctamente.
   * **component-filters.json**: Asegúrese de que el componente esté permitido en las secciones adecuadas.
   * **component-models.json**: Confirme que el modelo de componente está configurado correctamente.

## Prácticas recomendadas

* Se recomienda [configurar un entorno de desarrollo local de AEM](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#set-up-local-aem-development-environment) para desarrollar estilos y componentes personalizados localmente.


## Byte adicional

### ResourceType admitido

| Tipo de campo | Tipo de medio |
|--------------|------------------------------------------------------------------|
| text-input | core/fd/components/form/textinput/v1/textinput |
| entrada de número | core/fd/components/form/numberinput/v1/numberinput |
| date-input | core/fd/components/form/datepicker/v1/datepicker |
| panel | core/fd/components/form/panelcontainer/v1/panelcontainer |
| casilla de verificación | core/fd/components/form/checkbox/v1/checkbox |
| lista desplegable | core/fd/components/form/dropdown/v1/dropdown |
| grupo de radio | core/fd/components/form/radiobutton/v1/radiobutton |
| texto sin formato | core/fd/components/form/text/v1/text |
| entrada de archivo | core/fd/components/form/fileinput/v2/fileinput |
| correo electrónico | core/fd/components/form/emailinput/v1/emailinput |
| image | core/fd/components/form/image/v1/image |
| botón | core/fd/components/form/button/v1/button |

### Tipos de campo admitidos

Los tipos de campo admitidos para los formularios son:
* text-input
* entrada de número
* date-input
* panel
* casilla de verificación
* lista desplegable
* grupo de radio
* texto sin formato
* entrada de archivo
* correo electrónico
* image
* botón

## Ver también

{{see-more-forms-eds}}
