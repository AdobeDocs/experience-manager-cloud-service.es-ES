---
title: Creación de componentes personalizados para un formulario EDS
description: Crear componentes personalizados para un formulario EDS
feature: Edge Delivery Services
role: Admin, Architect, Developer
exl-id: 2bbe3f95-d5d0-4dc7-a983-7a20c93e2906
source-git-commit: 1d59791561fc6148778adccab902c8e727adc641
workflow-type: tm+mt
source-wordcount: '2120'
ht-degree: 4%

---


# Crear un componente de formulario personalizado en un bloque de formulario adaptable

Los formularios de Edge Delivery Services ofrecen personalización, lo que permite a los desarrolladores front-end generar componentes de formulario personalizados. Estos componentes personalizados se integran a la perfección en la experiencia de creación de WYSIWYG, lo que permite a los autores de formularios añadirlos, configurarlos y administrarlos fácilmente dentro del editor de formularios. Con los componentes personalizados, los autores pueden mejorar la funcionalidad a la vez que garantizan un proceso de creación fluido e intuitivo.

Este documento describe los pasos para crear componentes personalizados mediante la aplicación de estilos a los componentes de formulario HTML nativos para mejorar la experiencia del usuario y aumentar el atractivo visual del formulario.

## Información general sobre la arquitectura

El componente personalizado para el bloque de Forms sigue un patrón de arquitectura **MVC (Model-View-Controller)**:

### Modelo

- Definido por el esquema JSON para cada `field/component`.

- Las propiedades autorizables se especifican en el archivo JSON correspondiente (consulte bloques/formulario/modelos/formulario- componentes).

- Estas propiedades están disponibles para los autores en el generador de formularios y se pasan al componente como parte de la definición del campo (fd).

### Ver

- La estructura de HTML para cada tipo de campo se describe en form-field-types.

- Esta es la estructura base del componente que se puede ampliar o modificar.

- La estructura base de HTML para cada componente OOTB se documenta en tipos de campo de formulario.

### Lógica del controlador/componente

- Se implementa en JavaScript, ya sea como componentes OOTB (predeterminados) o personalizados.  - Se encuentra en `blocks/form/components` para componentes personalizados.

## Componentes OOTB

Los componentes **OOTB (predeterminados)** proporcionan la base para el desarrollo personalizado:

- Los componentes OOTB se encuentran en `blocks/form/models/form-components`.

- Cada componente de OOTB tiene un archivo JSON que define sus propiedades legibles (por ejemplo, ` _text-input.json`,`_drop-down.json`).

- Estas propiedades están disponibles para los autores en el generador de formularios y se pasan al componente como parte de la definición del campo (fd).

- La estructura base de HTML para cada componente OOTB se documenta en tipos de campo de formulario.

La ampliación de un componente OOTB existente le permite reutilizar su estructura base, comportamiento y propiedades, a la vez que lo personaliza para adaptarlo a sus necesidades.

- Los componentes personalizados deben extenderse desde un conjunto predefinido de componentes OOTB.

- El sistema identifica qué componente OOTB se va a extender en función de la propiedad `viewType` en el JSON del campo.

- El sistema mantiene un registro de variantes de componentes personalizadas permitidas. Solo se pueden usar las variantes enumeradas en este Registro, por ejemplo, `customComponents[]` en `mappings.js`.

- Al procesar un formulario, el sistema comprueba la propiedad de variante de `:type/fd:viewType` y, si coincide con un componente personalizado registrado, carga los archivos JS y CSS correspondientes de la carpeta `blocks/form/components`.

- A continuación, el componente personalizado se aplica a la estructura base de HTML del componente OOTB, lo que le permite mejorar o anular su comportamiento y apariencia.

## Estructura del componente personalizado

Para crear componentes personalizados, puede usar la **CLI de Scaffolder** para configurar los archivos y carpetas necesarios para el componente y, a continuación, agregar código para el componente personalizado.

- Los componentes personalizados residen en la carpeta `blocks/form/components`.

- Cada componente personalizado debe colocarse en su propia carpeta, con un nombre que corresponda al componente, por ejemplo, las tarjetas. Dentro de la carpeta, los siguientes archivos deben ser:

   - **_cards.json**: archivo JSON que amplía la definición de componente de un componente OOTB, define sus propiedades legibles (modelos[]) y la estructura de contenido al cargar (definiciones[]).
   - **cards.js**: el archivo JavaScript que incluye la lógica principal.
   - **cards.css**: opcional, para estilos.

- El nombre de la carpeta y los archivos JS/CSS deben coincidir.

### Reutilización y ampliación de campos en componentes personalizados

Al definir campos en el JSON del componente personalizado (para cualquier grupo de campos, básico, validación, ayuda, etc.), siga estas prácticas recomendadas para mantener la coherencia y la capacidad de mantenimiento:

- Reutilice campos estándar/compartidos haciendo referencia a contenedores compartidos o definiciones de campo existentes (por ejemplo, `../form-common/_basic-input-placeholder-fields.json#/fields`, `../form-common/_basic- validation-fields.json#/fields`). Esto garantiza que herede todas las opciones estándar sin duplicarlas.

- Agregue solo campos nuevos o personalizados de forma explícita en el contenedor. Esto mantiene su esquema SECO y enfocado.

- Elimine o evite duplicar campos que ya se incluyen mediante referencias. Solo defina campos que sean únicos para la lógica del componente.

- Hacer referencia a contenedores de ayuda y otro contenido compartido (por ejemplo, `../form-common/_help-container.json`) según sea necesario para mantener la coherencia y la capacidad de mantenimiento.

>[!TIP]
>
> - Este patrón facilita la actualización o ampliación de la lógica en el futuro y garantiza que los componentes personalizados permanezcan coherentes con el resto del sistema de formularios.
> - Compruebe siempre los contenedores compartidos existentes o las definiciones de campo antes de agregar nuevas.

### Definición de nuevas propiedades para componentes personalizados

- Si necesita capturar nuevas propiedades para el componente personalizado de los autores, se puede hacer definiendo un campo en la matriz `fields[]` del componente en el JSON del componente.

- El componente personalizado se identifica con la propiedad :type, que se puede establecer como `fd:viewType` en el archivo JSON (por ejemplo, `fd:viewType: cards`). Esto permite al sistema reconocer y cargar el componente personalizado correcto y, por lo tanto, esto es obligatorio para los componentes personalizados

- Todas las propiedades nuevas agregadas en la definición JSON están disponibles en la definición del campo como propiedades. `<propertyName>` en la lógica JS de su componente

## API de JavaScript de componente personalizado

La API de JavaScript de componentes personalizados define cómo controlar el comportamiento, la apariencia y la reactividad del componente de formulario personalizado.

### Función Decorar

La función **decorate** es el punto de entrada para el componente personalizado. Inicializa el componente, lo vincula con su definición JSON y le permite manipular su estructura y comportamiento de HTML.

>[!NOTE]
>
> El archivo JavaScript del componente personalizado debe exportar una función predeterminada como decorar:

#### Firma de función:

```javascript
export default function decorate(element, fieldJson, container, formId) {
// element: The HTML structure of the OOTB component you are extending
// fieldJson: The JSON field definition (all authorable properties)
// container: The parent element (fieldset or form)
// formId: The id of the form
// ... your logic here ...
}
```

Puede:

- **Modifique el elemento**: agregue detectores de eventos, actualice atributos o inserte marcado adicional.

- **Acceder a propiedades JSON**: utilice `fd.properties.<propertyName>` para leer valores definidos en el esquema JSON y aplicarlos dentro de la lógica del componente.

## Función Suscribir

La función **subscribe** permite que su componente reaccione a los cambios en los valores de los campos o a los eventos personalizados. Esto garantiza que el componente permanezca sincronizado con el modelo de datos del formulario y pueda actualizar dinámicamente su interfaz de usuario.

### Firma de función:

```JavaScript
import { subscribe } from '../../rules/index.js';

export default function decorate(fieldDiv, fieldJson, container, formId) {
// Access custom properties defined in the JSON
const { initialText, finalText, time } = fieldJson?.properties;
// ... setup logic ...
subscribe(fieldDiv, formId, (_fieldDiv, fieldModel) => { fieldModel.subscribe(() => {
// React to custom event (e.g., resetCardOption)
// ... logic ...
}, 'resetCardOption');
});
}
```

Puede:

- **Registrar una llamada de retorno**: al llamar a **subscribe(element, formId, callback)**, se registra su llamada de retorno para que se ejecute siempre que cambien los datos del campo.Use dos parámetros de llamada de retorno:
   - **element**: El elemento HTML que representa el campo.
   - **fieldModel**: el objeto que representa el estado y las API de evento del campo.

- **Escuchar cambios o eventos**: Use `fieldModel.subscribe((event) => { ... }, 'eventName')` para ejecutar la lógica cada vez que cambie un valor o se active un evento personalizado. El objeto de evento contiene detalles sobre los cambios.

## Crear un componente personalizado

En esta sección, aprenderá el proceso de crear un **componente personalizado de tarjetas** ampliando el componente de botón de opción OOTB.

![Componente personalizado de tarjeta](/help/edge/docs/forms/universal-editor/assets/cc-ue-card-component.png)

### &#x200B;1. Configuración del código

#### 1.1 Archivos y carpetas

El primer paso es configurar los archivos necesarios del componente personalizado y conectarlo al código del repositorio. Este proceso lo realiza automáticamente **AEM Forms Scaffolder CLI**, lo que agiliza el andamiaje y la transferencia de los archivos necesarios.

1. Abra el terminal y vaya a la raíz del proyecto de formulario.
2. Ejecute los siguientes comandos:

```bash
npm install
npm run create:custom-component
```

![CLI de Scaffolder](/help/edge/docs/forms/universal-editor/assets/scaffolder-cli.png)

Esto hará lo siguiente:

- **Pedirle que nombre** su nuevo componente. Por ejemplo, en este caso utilice tarjetas.
- **Pedirle que elija** un componente base (seleccione el grupo de radio)

Esto crea todas las carpetas y archivos necesarios, incluidos:

```
blocks/form/
└── components/
  └── cards/
    ├── cards.js
    └── cards.css
    └── _cards.json
```

Y lo conecta con el resto del código del repositorio, como se muestra en la salida de la CLI.
Realiza las siguientes funcionalidades automáticamente:

- Agrega tarjetas a los filtros para permitir la adición dentro del bloque de formulario adaptable.
- Actualiza la lista de permitidos de `mappings.js` para incluir el nuevo componente de tarjetas.
- Registra la definición del componente de tarjetas en el listado de **componentes personalizados** del Editor universal.

>[!NOTE]
>
> También puede crear un componente personalizado mediante el método manual (heredado). Consulte [Método manual o heredado](#manual-or-legacy-method-to-create-custom-component) para crear la sección de componentes personalizados y obtener más información.

#### 1.2 Uso del componente en el editor universal

1. **Actualizar el editor universal**: abra el formulario en el editor universal y actualice la página para asegurarse de que carga el código más reciente del repositorio.

2. **Agregar el componente personalizado**

   1. Haga clic en el botón **Agregar (+)** en el lienzo del formulario.
   2. Desplácese hasta la sección Componentes personalizados.
   3. Seleccione el **componente de tarjetas** recién creado para insertarlo en el formulario.

      ![Seleccionar componente personalizado](/help/edge/docs/forms/universal-editor/assets/select-custom-component.png)

Como no hay código presente dentro de `cards.js`, el componente personalizado se representa como un grupo de radio.

#### 1.3 Previsualización y pruebas locales

Ahora que el formulario contiene el componente personalizado, puede representar el formulario y realizar cambios en él localmente para ver los cambios:

1. Vaya a su terminal y ejecute `aem up`.

2. Abrir el servidor proxy iniciado en `http://localhost:3000/{path-to-your-form}` (ejemplo de ruta de acceso: `/content/forms/af/custom-component-form`)


### &#x200B;2. Implementar el comportamiento personalizado para el componente personalizado

#### 2.1 Estilo del componente personalizado

Vamos a agregar una clase **card** al componente para aplicar estilo y agregar una imagen para cada radio; use el siguiente código para esto.

**Aplicar estilo al componente personalizado mediante la función decorar en cards.js**

```javascript
import { createOptimizedPicture } from '../../../../scripts/aem.js';

export default function decorate(element, fieldJson, container, formId) { element.classList.add('card');
element.querySelectorAll('.radio-wrapper').forEach((radioWrapper) => { const image = createOptimizedPicture('https://main--afb--
jalagari.hlx.live/lab/images/card.png', 'card-image'); radioWrapper.appendChild(image);
});
return element;
}
```

**Agregar comportamiento de tiempo de ejecución para el componente personalizado en cards.css**

```javascript
.card .radio-wrapper { min-width: 320px;
/* or whatever width fits your design */ max-width: 340px;
background: #fff;
border-radius: 16px;
box-shadow: 0 2px 8px rgba(0, 0, 0, 0.08);
flex: 0 0 auto;
scroll-snap-align: start; padding: 24px 16px;
margin-bottom: 0;
position: relative;
transition: box-shadow 0.2s; display: flex;
align-items: flex-start; gap: 12px;
}
```

Ahora, el componente Tarjetas aparece de esta manera:

![agregar css y js de tarjeta](/help/edge/docs/forms/universal-editor/assets/add-card-css.png)

#### 2.2 Agregar un comportamiento dinámico mediante la función Suscribirse

Cuando se cambia la lista desplegable, las tarjetas se recuperan y se establecen en la enumeración del grupo de radio. Pero actualmente la vista no maneja esto. Por lo tanto, se procesa como se muestra a continuación:

![función de suscripción](/help/edge/docs/forms/universal-editor/assets/card-subscribe.png)

Cuando se llama a la API, establece el modelo de campo y debe escuchar los cambios y procesar la vista en consecuencia. Esto se logra usando la **función de suscripción**.

Convirtamos el código de vista del paso anterior en una función y llamemos a esto dentro de la función de suscripción en `cards.js` como se muestra a continuación:

```javascript
import { createOptimizedPicture } from '../../../../scripts/aem.js';  

import { subscribe } from '../../rules/index.js';  
function createCard(element, enums) {  

  element.querySelectorAll('.radio-wrapper').forEach((radioWrapper, index) => {  

    if (enums[index]?.name) {  

      let label = radioWrapper.querySelector('label');  

      if (!label) {  

        label = document.createElement('label');  

        radioWrapper.appendChild(label);  

      }  

      label.textContent = enums[index]?.name;  

    }  

    const image = createOptimizedPicture(enums[index].image || 'https://main--afb--jalagari.hlx.page/lab/images/card.png', 'card-image');  

   radioWrapper.appendChild(image);  

  });  

}  
export default function decorate(element, fieldJson, container, formId) {  

    element.classList.add('card');  

    createCard(element, fieldJson.enum);  

    subscribe(element, formId, (fieldDiv, fieldModel) => {  

        fieldModel.subscribe((e) => {  

            const { payload } = e;  

            payload?.changes?.forEach((change) => {  

                if (change?.propertyName === 'enum') {  

                    createCard(element, change.currentValue);  

                }  

            });  

        });  

    });  
    return element;  

} 
```

**Usar la función de suscripción para escuchar los cambios de eventos en cards.js**

Ahora, al cambiar el menú desplegable, las tarjetas se rellenan como se muestra a continuación:

![función de suscripción](/help/edge/docs/forms/universal-editor/assets/card-subscribe-final.png)

#### 2.3 Sincronización de actualizaciones de vista con el modelo de campo

Para sincronizar los cambios de vista con el modelo de campo, debe establecer el valor de la tarjeta seleccionada. Por lo tanto, agregue el siguiente detector de eventos de cambio en cards.js, como se muestra a continuación:

**Usando API de modelo de campo en cards.js**

```javascript
 

import { createOptimizedPicture } from '../../../../scripts/aem.js';  

import { subscribe } from '../../rules/index.js';  

  

  

function createCard(element, enums) {  

  element.querySelectorAll('.radio-wrapper').forEach((radioWrapper, index) => {  

    if (enums[index]?.name) {  

      let label = radioWrapper.querySelector('label');  

      if (!label) {  

        label = document.createElement('label');  

        radioWrapper.appendChild(label);  

      }  

      label.textContent = enums[index]?.name;  

    }  

    radioWrapper.querySelector('input').dataset.index = index;  

    const image = createOptimizedPicture(enums[index].image || 'https://main--afb--jalagari.hlx.page/lab/images/card.png', 'card-image');  

   radioWrapper.appendChild(image);  

  });  

}  
export default function decorate(element, fieldJson, container, formId) {  

    element.classList.add('card');  
    createCard(element, fieldJson.enum);  

    subscribe(element, formId, (fieldDiv, fieldModel) => {  

        fieldModel.subscribe((e) => {  

            const { payload } = e;  

            payload?.changes?.forEach((change) => {  

                if (change?.propertyName === 'enum') {  

                    createCard(element, change.currentValue);  

                }  

            });  

        });  
        element.addEventListener('change', (e) => {  

            e.stopPropagation();  

            const value = fieldModel.enum?.[parseInt(e.target.dataset.index, 10)];  

            fieldModel.value = value.name;  

        });  

    });  

    return element;  
} 
```

Ahora aparece el componente de tarjeta personalizada, como se muestra a continuación:

![Componente personalizado de tarjeta](/help/edge/docs/forms/universal-editor/assets/cc-ue-card-component.png)

## Confirmar y enviar cambios

Una vez que haya implementado JavaScript y CSS para el componente personalizado y lo haya verificado localmente, confirme e inserte los cambios en el repositorio de Git.

```bash
git add . && git commit -m "Add card custom component" && git push
```

Ha creado correctamente un componente de selección de tarjetas personalizado complejo en unos sencillos pasos.

## Método manual o heredado para crear un componente personalizado

La forma heredada de hacerlo es seguir manualmente los pasos que se describen a continuación:

1. **Elija un componente OOTB** para extender (por ejemplo, botón, lista desplegable, entrada de texto, etc.). En este caso, amplíe el componente de radio.

2. **Cree una carpeta** en `blocks/form/components` con el nombre de su componente (en este caso, tarjetas).

3. **Agregar un archivo JS** con el mismo nombre:
   - `blocks/form/components/cards/cards.js`.

4. (Opcional) **Agregue un archivo CSS** para los estilos personalizados:
   - `blocks/form/components/cards/cards.css.`

5. **Defina un nuevo archivo JSON** (por ejemplo,` _cards.json`) en la misma carpeta que el **archivo JS de componente** (`blocks/form/components/cards/_cards.json`). Este JSON debe ampliar un componente existente y, en sus definiciones, establecer `fd:viewType` en el nombre de su componente (en este caso, tarjetas):

   - Para todos los grupos de campos (básico, de validación, de ayuda, etc.), agregue explícitamente los campos personalizados.

6. **Implementar la lógica JS y CSS:**
   - Exporte una función predeterminada como se ha descrito anteriormente.
   - Use el parámetro **element** para modificar la estructura base de HTML.
   - Use el parámetro **fieldJson** si es necesario para los datos de campo estándar.
   - Utilice la función **subscribe** para escuchar los cambios de campo o los eventos personalizados si es necesario.

     >[!NOTE]
     >
     >Implemente la lógica JS y CSS para su componente personalizado como se explica más arriba.

7. Registre el componente como una variante en el generador de formularios y establezca la propiedad de variante o
   `fd:viewType/:type` en el JSON al nombre de su componente, por ejemplo, agregue el valor `fd:viewType` del `definitions[]` como tarjetas a la matriz de componentes del objeto con `id="form`.

   ```javascript
   {
   "definitions": [
   {
   "title": "Cards",
   "id": "cards", "plugins": {
   "xwalk": {
   "page": {
   "resourceType":
   "core/fd/components/form/radiobutton/v1/radiobutton", "template": {
   "jcr:title": "Cards",
   "fieldType": "radio-button", "fd:viewType": "cards",
   "enabled": true, "visible": true}
   }
   } }
   }
   ]}
   ```

8. **Actualizar mappings.js**: agregue el nombre de su componente a **OOTBComponentDecorators** (para componentes de estilo OOTB) o a la lista **customComponents** para que el sistema lo reconozca y lo cargue.

   ```javascript
   let customComponents = ["cards"];
   const OOTBComponentDecorators = [];
   ```

9. **Actualizar _form.json**: agregue el nombre de su componente a la matriz `filters.components` para que se pueda colocar en la interfaz de usuario de creación.

   ```javascript
   "filters": [
   {
       "id": "form",
       "components": [ "cards"]}
       ]
   ```

10. **Actualizar _component-definition.json**: en `models/_component-definition.json`, actualice la matriz dentro del grupo con `id custom-components` con un objeto de la siguiente manera:

    ```javascript
    {
    "...":"../blocks/form/components/cards/_cards.json#/definitions"
    }
    ```

    Esto es para proporcionar la referencia al nuevo componente de tarjetas que se va a crear con el resto de los componentes

11. **Ejecutar la compilación:json script**: Ejecute `npm run build:json` para compilar y combinar todas las definiciones JSON de componentes en un solo archivo que se servirá desde el servidor. Esto garantiza que el esquema del nuevo componente se incluya en la salida combinada.

12. Confirme y envíe los cambios al repositorio de Git.

Ahora puede agregar el componente personalizado al formulario.

## Crear un componente compuesto

Un componente compuesto se crea combinando varios componentes.
Por ejemplo, un componente compuesto Términos y condiciones consta de un panel principal que contiene:

- Campo de texto sin formato para mostrar los términos

- Casilla de verificación para recopilar el acuerdo del usuario

Esta estructura de composición se define como una plantilla dentro del archivo JSON del componente correspondiente. El siguiente ejemplo muestra cómo definir una plantilla para un componente Términos y condiciones:

```javascript
{ 

  "definitions": [ 

    { 

      "title": "Terms and conditions", 

      "id": "tnc", 

      "plugins": { 

        "xwalk": { 

          "page": { 

            "resourceType": "core/fd/components/form/termsandconditions/v1/termsandconditions", 

            "template": { 

              "jcr:title": "Terms and conditions", 

              "fieldType": "panel", 

              "fd:viewType": "tnc", 

              "text": { 

                "value": "Text related to the terms and conditions come here.", 

                "sling:resourceType": "core/fd/components/form/text/v1/text", 

                "fieldType": "plain-text", 

                "textIsRich": true 

              }, 

              "approvalcheckbox": { 

                "name": "approvalcheckbox", 

                "jcr:title": "I agree to the terms & conditions.", 

                "sling:resourceType": "core/fd/components/form/checkbox/v1/checkbox", 

                "fieldType": "checkbox", 

                "required": true, 

                "type": "string", 

                "enum": [ 

                  "true" 

                ] 

              } 

            } 

          } 

        } 

      } 

    } 

  ], 

  ... 

} 
```

## Prácticas recomendadas

Tenga en cuenta los siguientes puntos antes de crear su propio componente personalizado:

- **Mantenga centrada la lógica de su componente**: agregue o anule únicamente lo necesario para el comportamiento personalizado

- **Aprovechar la estructura base**: use el HTML OOTB como punto de partida

- **Usar propiedades autorizables:** Exponer opciones configurables a través del esquema JSON

- **Área de nombres de su CSS**: evite conflictos de estilos utilizando nombres de clase únicos

## Referencias

- form-field-types: Base las estructuras y propiedades de HTML para todos los tipos de campo. [Haga clic aquí](/help/edge/docs/forms/eds-form-field-properties) para ver las estructuras y propiedades detalladas de los campos de formulario.

- **bloques/formulario/modelos/componentes-formulario**: definiciones de propiedades de componentes personalizados y OOTB.

- **bloques/formulario/componentes**: lugar para los componentes personalizados. Por ejemplo: `blocks/form/components/countdown-timer/_countdown-timer.json` muestra cómo extender un componente base y agregar nuevas propiedades.
