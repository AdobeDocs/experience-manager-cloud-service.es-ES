---
title: Este artículo describe varios casos de uso para una función personalizada en un formulario adaptable en función de los componentes principales.
description: El artículo describe varios casos de uso para una función personalizada en un formulario adaptable en función de los componentes principales. Las funciones personalizadas se utilizan en el editor de reglas para crear reglas personalizadas para el formulario.
feature: Adaptive Forms, Core Components
role: User, Developer
level: Beginner, Intermediate
exl-id: df92b91e-f3b0-4a08-bd40-e99edc9a50a5
source-git-commit: 5b5b44f8dffc01a75eda464cd7759cf03028c2c6
workflow-type: tm+mt
source-wordcount: '2184'
ht-degree: 0%

---

# Ejemplos de desarrollo y uso de funciones personalizadas

El artículo proporciona ejemplos detallados de funciones personalizadas para un formulario adaptable basadas en componentes principales, lo que ofrece información valiosa sobre su implementación eficaz en varios escenarios. Las funciones personalizadas se utilizan en el editor de reglas de una AEM Forms, lo que permite a los desarrolladores definir y controlar la lógica que rige el comportamiento del formulario.
Este artículo explora diferentes implementaciones de funciones personalizadas, mostrando cómo se pueden utilizar para adaptar los formularios para satisfacer requisitos específicos y mejorar la funcionalidad general.

## Rellenar las opciones de la lista desplegable con funciones personalizadas

El Editor de reglas de los componentes principales no admite la propiedad **Set Options** para rellenar opciones de lista desplegable de forma dinámica durante la ejecución. Sin embargo, puede rellenar las opciones de la lista desplegable con funciones personalizadas, que le permiten recuperar opciones basadas en una lógica específica. Las funciones personalizadas proporcionan una mayor flexibilidad y control sobre cómo y cuándo se rellenan las opciones desplegables, lo que mejora la experiencia del usuario.

Para rellenar las opciones de la lista desplegable con una función personalizada, agregue el siguiente código como se describe en la sección [create-custom-function](/help/forms/custom-function-core-component-create-function.md):


```javascript
    /**
    * @name setEnums
    * @returns {string[]}
    **/
    function setEnums() {
    return ["0","1","2","3","4","5","6"];   
    }

    /**
    * @name setEnumNames
    * @returns {string[]}
    **/
    function setEnumNames() {
    return ["Sunday","Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday"];
    }
```

En el código anterior, `setEnums` se usa para establecer la propiedad `enum` y `setEnumNames` se usa para establecer la propiedad `enumNames` de la lista desplegable.

Vamos a crear una regla para el botón `Next`, que establece la opción de valor de la lista desplegable cuando el usuario haga clic en el botón `Next`:

![Opciones de lista desplegable](/help/forms/assets/drop-down-list-options.png)

Consulte la siguiente ilustración para demostrar dónde están configuradas las opciones de la lista desplegable al hacer clic en el botón Mostrar:

![Opciones desplegables en el editor de reglas](/help/forms/assets/drop-down-option-rule-editor.png)

## Mostrar un panel utilizando la regla `SetProperty`

Vamos a aprender cómo las funciones personalizadas utilizan los objetos globales y de campo con la ayuda de un formulario `Contact Us`.

![Formulario de contacto](/help/forms/assets/contact-us-form.png)

Agregue el siguiente código en la función personalizada como se explica en la sección [create-custom-function](/help/forms/custom-function-core-component-create-function.md) para establecer el campo del formulario como `Required`.

```javascript
    
    /**
    * enablePanel
    * @name enablePanel
    * @param {object} field1
    * @param {object} field2
    * @param {scope} globals 
    */

    function enablePanel(field1,field2, globals)
    {
       if(globals.functions.validate(field1).length === 0)
       {
       globals.functions.setProperty(field2, {visible: true});
       }
    }
```

>[!NOTE]
>
> * Puede configurar las propiedades del campo mediante las propiedades disponibles ubicadas en `[form-path]/jcr:content/guideContainer.model.json`.
> * Las modificaciones realizadas en el formulario mediante el método `setProperty` del objeto Globals son de naturaleza asincrónica y no se reflejan durante la ejecución de la función personalizada.

En este ejemplo, la validación del panel `personaldetails` se produce al hacer clic en el botón. Si no se detectan errores en el panel, otro panel, el panel `feedback`, se vuelve visible al hacer clic en el botón.

Vamos a crear una regla para el botón `Next`, que valida el panel `personaldetails` y hace visible el panel `feedback` cuando el usuario hace clic en el botón `Next`.

![Set Property](/help/forms/assets/custom-function-set-property.png)

Consulte la siguiente ilustración para demostrar dónde se valida el panel `personaldetails` al hacer clic en el botón `Next`. Si se validan todos los campos del `personaldetails`, el panel `feedback` se volverá visible.

![Establecer vista previa de formulario de propiedad](/help/forms/assets/set-property-form-preview.png)

Si hay errores en los campos del panel `personaldetails`, se mostrarán en el nivel de campo al hacer clic en el botón `Next`, y el panel `feedback` permanecerá invisible.

![Establecer vista previa de formulario de propiedad](/help/forms/assets/set-property-panel.png)

## Validación del campo

Vamos a aprender cómo las funciones personalizadas utilizan los objetos globales y de campo para validar el campo con la ayuda de un formulario `Contact Us`.

Agregue el siguiente código en la función personalizada como se explica en la sección [create-custom-function](/help/forms/custom-function-core-component-create-function.md) para validar el campo.

```javascript
    /**
    * validateField
    * @name validateField
    * @param {object} field
    * @param {scope} globals
    */
    function validateField(field,globals)
    {
    
        globals.functions.validate(field);
    
    }   
```

>[!NOTE]
>
> Si no se pasa ningún argumento en la función `validate()`, se valida el formulario.

En este ejemplo, se aplica un motivo de validación personalizado al campo `contact`. Los usuarios deben ingresar un número de teléfono que comience por `10` seguido de `8` dígitos. Si el usuario escribe un número de teléfono que no comienza con `10` o contiene más o menos de `8` dígitos, aparecerá un mensaje de error de validación al hacer clic en el botón:

![Patrón de validación de direcciones de correo electrónico](/help/forms/assets/custom-function-validation-pattern.png)

Ahora, el siguiente paso es crear una regla para el botón `Next` que valide el campo `contact` al hacer clic en el botón.

![Patrón de validación](/help/forms/assets/custom-function-validate.png)

Consulte la siguiente ilustración para demostrar que si el usuario escribe un número de teléfono que no comience por `10`, aparece un mensaje de error en el nivel de campo:

![Patrón de validación de direcciones de correo electrónico](/help/forms/assets/custom-function-validate-error-message.png)

Si el usuario escribe un número de teléfono válido y se validan todos los campos del panel `personaldetails`, aparecerá el panel `feedback` en la pantalla:

![Patrón de validación de direcciones de correo electrónico](/help/forms/assets/validate-form-preview-form.png)

## Restablecer un panel

Vamos a aprender cómo las funciones personalizadas utilizan los objetos globales y de campo para restablecer el campo con la ayuda de un formulario `Contact Us`.

Agregue el siguiente código en la función personalizada como se explica en la sección [create-custom-function](/help/forms/custom-function-core-component-create-function.md) para restablecer el panel.

```javascript
    /**
    * resetField
    * @name  resetField
    * @param {string} input1
    * @param {object} field
    * @param {scope} globals 
    */
    function  resetField(field,globals)
    {
    
        globals.functions.reset(field);
    
    }
```

>[!NOTE]
>
> Si no se pasa ningún argumento en la función `reset()`, se valida el formulario.

En este ejemplo, el panel `personaldetails` se restablece al hacer clic en el botón `Clear`. El siguiente paso es crear una regla para el botón `Clear` que restablezca el panel al hacer clic en el botón.

![Botón Borrar](/help/forms/assets/custom-function-reset-field.png)

Consulte la siguiente ilustración para mostrar que si el usuario hace clic en el botón `clear`, se restablece el panel `personaldetails`:

![Restablecer formulario](/help/forms/assets/custom-function-reset-form.png)

## Para mostrar un mensaje personalizado en el nivel de campo y marcar el campo como no válido

Vamos a aprender cómo las funciones personalizadas utilizan los objetos globales y de campo para mostrar un mensaje personalizado en el nivel de campo y marcar el campo como no válido con la ayuda de un formulario `Contact Us`.

Puede usar la función `markFieldAsInvalid()` para definir un campo como no válido y establecer un mensaje de error personalizado en el nivel de campo. El valor `fieldIdentifier` puede ser `fieldId`, `field qualifiedName` o `field dataRef`. El valor del objeto denominado `option` puede ser `{useId: true}`, `{useQualifiedName: true}` o `{useDataRef: true}`.
Las sintaxis utilizadas para marcar un campo como no válido y establecer un mensaje personalizado son:

* `globals.functions.markFieldAsInvalid(field.$id,"[custom message]",{useId: true});`
* `globals.functions.markFieldAsInvalid(field.$qualifiedName, "[custom message]", {useQualifiedName: true});`
* `globals.functions.markFieldAsInvalid(field.$dataRef, "[custom message]", {useDataRef: true});`

Agregue el siguiente código en la función personalizada como se explica en la sección [create-custom-function](/help/forms/custom-function-core-component-create-function.md) para habilitar un mensaje personalizado en el nivel de campo.

```javascript
    /**
    * customMessage
    * @name customMessage
    * @param {object} field
    * @param {scope} globals 
    */
    function customMessage(field, globals) {
    const minLength = 15;
    const comments = field.$value.trim();
    if (comments.length < minLength) {
        globals.functions.markFieldAsInvalid(field.$id, "Comments must be at least 15 characters long.", { useId: true });
    }
}
```

En este ejemplo, si el usuario introduce menos de 15 caracteres en el cuadro de texto de comentarios, aparece un mensaje personalizado en el nivel de campo.

El siguiente paso es crear una regla para el campo `comments`:

![Marcar campo como no válido](/help/forms/assets/custom-function-invalid-field.png)

Vea la demostración siguiente para mostrar que escribir comentarios negativos en el campo `comments` déclencheur la visualización de un mensaje personalizado en el nivel de campo:

![Marcar campo como formulario de vista previa no válido](/help/forms/assets/custom-function-invalidfield-form.png)

Si el usuario introduce más de 15 caracteres en el cuadro de texto de comentarios, el campo se valida y se envía el formulario:

![Marcar campo como formulario de vista previa válido](/help/forms/assets/custom-function-validfield-form.png)

## Enviar datos modificados al servidor

Vamos a aprender cómo las funciones personalizadas utilizan los objetos globales y de campo para enviar datos manipulados en el servidor con la ayuda de un formulario `Contact Us`.

La siguiente línea de código:
`globals.functions.submitForm(globals.functions.exportData(), false);` se usa para enviar los datos del formulario después de la manipulación.
* El primer argumento son los datos que se van a enviar.
* El segundo argumento representa si el formulario se debe validar antes del envío. Es `optional` y se establece como `true` de manera predeterminada.
* El tercer argumento es el `contentType` del envío, que también es opcional con el valor predeterminado `multipart/form-data`. Los otros valores pueden ser `application/json` y `application/x-www-form-urlencoded`.

Agregue el siguiente código en la función personalizada como se explica en la sección [create-custom-function](/help/forms/custom-function-core-component-create-function.md) para enviar los datos manipulados en el servidor:

```javascript
    /**
    * submitData
    * @name submitData
    * @param {object} field
    * @param {scope} globals 
    */
    function submitData(globals)
    {
    
    var data = globals.functions.exportData();
    if(!data.comments) {
    data.comments = 'NA';
    }
    console.log('After update:{}',data);
    globals.functions.submitForm(data, false);
    }
```

En este ejemplo, si el usuario deja vacío el cuadro de texto `comments`, el `NA` se envía al servidor al enviar el formulario.

Ahora cree una regla para el botón `Submit` que envíe datos:

![Enviar datos](/help/forms/assets/custom-function-submit-data.png)

Consulte la siguiente ilustración de `console window` para demostrar que si el usuario deja vacío el cuadro de texto de `comments`, el valor como `NA` se envía en el servidor:

![Enviar datos en la ventana de la consola](/help/forms/assets/custom-function-submit-data-form.png)

También puede inspeccionar la ventana de la consola para ver los datos enviados al servidor:

![Inspeccionar datos en la ventana de la consola](/help/forms/assets/custom-function-submit-data-console-data.png)

## Anular los controladores de éxito y de error del envío del formulario

Vamos a aprender cómo las funciones personalizadas utilizan los objetos globales y de campo para anular los controladores de envío con la ayuda de un formulario `Contact Us`.

Agregue la siguiente línea de código, tal como se explica en la sección [create-custom-functions](/help/forms/custom-function-core-component-create-function.md), para personalizar el envío o el mensaje de error para los envíos de formularios y mostrar los mensajes de envío de formularios en un cuadro modal:

```javascript
/**
 * Handles the success response after a form submission.
 *
 * @param {scope} globals - This object contains a read-only form instance, target field instance, triggered event, and methods for performing form modifications within custom functions.
 * @returns {void}
 */
function customSubmitSuccessHandler(globals) {
    var event = globals.event;
    var submitSuccessResponse = event.payload.body;
    var form = globals.form;

    if (submitSuccessResponse) {
        if (submitSuccessResponse.redirectUrl) {
            window.location.href = encodeURI(submitSuccessResponse.redirectUrl);
        } else if (submitSuccessResponse.thankYouMessage) {
            showModal("success", submitSuccessResponse.thankYouMessage);
        }
    }
}

/**
 * Handles the error response after a form submission.
 *
 * @param {string} customSubmitErrorMessage - The custom error message.
 * @param {scope} globals - This object contains a read-only form instance, target field instance, triggered event, and methods for performing form modifications within custom functions.
 * @returns {void}
 */
function customSubmitErrorHandler(customSubmitErrorMessage, globals) {
    showModal("error", customSubmitErrorMessage);
}
function showModal(type, message) {
    // Remove any existing modals
    var existingModal = document.getElementById("modal");
    if (existingModal) {
        existingModal.remove();
    }

    // Create the modal dialog
    var modal = document.createElement("div");
    modal.setAttribute("id", "modal");
    modal.setAttribute("class", "modal");

    // Create the modal content
    var modalContent = document.createElement("div");
    modalContent.setAttribute("class", "modal-content");

    // Create the modal header
    var modalHeader = document.createElement("div");
    modalHeader.setAttribute("class", "modal-header");
    modalHeader.innerHTML = "<h2>" + (type === "success" ? "Thank You" : "Error") + "</h2>";

    // Create the modal body
    var modalBody = document.createElement("div");
    modalBody.setAttribute("class", "modal-body");
    modalBody.innerHTML = "<p class='" + type + "-message'>" + message + "</p>";

    // Create the modal footer
    var modalFooter = document.createElement("div");
    modalFooter.setAttribute("class", "modal-footer");

    // Create the close button
    var closeButton = document.createElement("button");
    closeButton.setAttribute("class", "close-button");
    closeButton.innerHTML = "Close";
    closeButton.onclick = function() {
        modal.remove();
    };

    // Append the elements to the modal content
    modalFooter.appendChild(closeButton);
    modalContent.appendChild(modalHeader);
    modalContent.appendChild(modalBody);
    modalContent.appendChild(modalFooter);

    // Append the modal content to the modal
    modal.appendChild(modalContent);

    // Append the modal to the document body
    document.body.appendChild(modal);
}
```

En este ejemplo, cuando el usuario utiliza las funciones personalizadas `customSubmitSuccessHandler` y `customSubmitErrorHandler`, los mensajes de éxito y error se muestran en un modal. La función de JavaScript `showModal(type, message)` se usa para crear y mostrar dinámicamente un cuadro de diálogo modal en una pantalla.

Ahora, cree una regla para el envío correcto de formularios:

![Envío de formulario correcto](/help/forms/assets/form-submission-success.png)

Consulte la siguiente ilustración para demostrar que, cuando el formulario se envía correctamente, el mensaje de éxito se muestra en un modal:

![Mensaje de éxito de envío de formulario](/help/forms/assets/form-submission-success-message.png)

Del mismo modo, vamos a crear una regla para los envíos de formularios fallidos:

![Error al enviar el formulario](/help/forms/assets/form-submission-fail.png)

Consulte la siguiente ilustración para demostrar que, cuando falla el envío del formulario, el mensaje de error se muestra en un modal:

![Mensaje de error en el envío del formulario](/help/forms/assets/form-submission-fail-message.png)

Para mostrar el éxito y el error del envío del formulario de forma predeterminada, las funciones `Default submit Form Success Handler` y `Default submit Form Error Handler` están disponibles de forma predeterminada.

En caso de que el controlador de envío personalizado no funcione según lo esperado en los formularios o proyectos de AEM existentes, consulte la sección [solución de problemas](#troubleshooting).

## Realizar acciones en una instancia específica del panel repetible

Las reglas creadas con el editor de reglas visuales en un panel repetible se aplican a la última instancia del panel repetible. Para escribir una regla para una instancia específica del panel repetible, podemos utilizar una función personalizada.

Vamos a crear otro formulario como `Booking Form` para recopilar información sobre los viajeros que se dirigen a un destino. Un panel de viajeros se agrega como un panel repetible, donde el usuario puede agregar detalles para 5 viajeros con el botón `Add Traveler`.

![Información del viajero](/help/forms/assets/traveler-info-form.png)

Agregue la siguiente línea de código como se explica en la sección [create-custom-function](/help/forms/custom-function-core-component-create-function.md) para realizar acciones en una instancia específica del panel repetible que no sea la última:

```javascript
/**
* @name hidePanelInRepeatablePanel
* @param {scope} globals
*/
function hidePanelInRepeatablePanel(globals)
{    
    var repeatablePanel = globals.form.travelerinfo;
    // hides a panel inside second instance of repeatable panel
    globals.functions.setProperty(repeatablePanel[1].traveler, {visible : false});
}  
```

En este ejemplo, la función personalizada `hidePanelInRepeatablePanel` realiza una acción en una instancia específica del panel repetible. En el código anterior, `travelerinfo` representa el panel repetible. El código `repeatablePanel[1].traveler, {visible: false}` oculta el panel en la segunda instancia del panel repetible.

Vamos a agregar un botón denominado `Hide` y agregar una regla para ocultar la segunda instancia de un panel repetible.

![Ocultar regla de panel](/help/forms/assets/custom-function-hidepanel-rule.png)

Consulte el siguiente vídeo para demostrar que, cuando se hace clic en `Hide`, se oculta el panel de la segunda instancia repetible:

>[!VIDEO](https://video.tv.adobe.com/v/3429554?quality=12&learn=on)

## Rellene previamente el campo con un valor cuando se cargue el formulario

Vamos a aprender cómo las funciones personalizadas utilizan los objetos globales y de campo para rellenar previamente el campo con la ayuda de `Booking Form`.

Agregue la siguiente línea de código, tal como se explica en la sección [create-custom-function](/help/forms/custom-function-core-component-create-function.md), para cargar el valor rellenado previamente en un campo cuando se inicialice el formulario:

```javascript
/**
 * Tests import data
 * @name testImportData
 * @param {scope} globals
 */
function testImportData(globals)
{
    globals.functions.importData(Object.fromEntries([['amount','10000']]));
} 
```

En el código mencionado, la función `testImportData` rellena previamente el campo de cuadro de texto `Booking Amount` cuando se carga el formulario. Supongamos que el formulario de reserva requiere que la cantidad mínima de reserva sea de `10,000`.

Vamos a crear una regla en la inicialización del formulario, donde el valor del campo `Booking Amount` textbox se rellena previamente con un valor especificado cuando se carga el formulario:

![Importar regla de datos](/help/forms/assets/custom-function-import-data.png)

Consulte la captura de pantalla siguiente, que muestra que cuando se carga el formulario, el valor del cuadro de texto `Booking Amount` está rellenado previamente con un valor especificado:

![Importar formulario de reglas de datos](/help/forms/assets/custom-function-prefill-form.png)

## Establecer el enfoque en un campo específico

Vamos a aprender cómo las funciones personalizadas utilizan los objetos globales y de campo para establecer el enfoque en un campo específico con la ayuda de `Booking Form`.

Agregue la línea de código siguiente, tal como se explica en la sección [create-custom-function](/help/forms/custom-function-core-component-create-function.md), para establecer el enfoque en el campo especificado cuando se haga clic en el botón `Submit`.:

```javascript
/**
 * @name testSetFocus
 * @param {object} emailField
 * @param {scope} globals
 */
    function testSetFocus(field, globals)
    {
        globals.functions.setFocus(field);
    }
```

Vamos a agregar una regla al botón `Submit` para establecer el enfoque en el campo de cuadro de texto `Email ID` cuando se hace clic:

![Establecer regla de enfoque](/help/forms/assets/custom-function-set-focus.png)

Consulte la captura de pantalla siguiente, que muestra que cuando se hace clic en el botón `Submit`, el enfoque se establece en el campo `Email ID`:

![Establecer regla de enfoque](/help/forms/assets/custom-function-set-focus-form.png)

>[!NOTE]
>
> Puede usar el parámetro `$focusOption` opcional si desea centrarse en el campo siguiente o anterior en relación con el campo `email`.

## Agregar o eliminar el panel repetible con la propiedad `dispatchEvent`

Vamos a aprender cómo las funciones personalizadas utilizan los objetos globales y de campo para agregar o eliminar paneles repetibles mediante la propiedad `dispatchEvent` con la ayuda de `Booking Form`.

Agregue la línea de código siguiente, tal como se explica en la sección [create-custom-function](/help/forms/custom-function-core-component-create-function.md), para agregar un panel cuando se haga clic en el botón `Add Traveler` mediante la propiedad `dispatchEvent`:

```javascript
/**
 * Tests add instance with dispatchEvent
 * @name testAddInstance
 * @param {scope} globals
 */
function testAddInstance(globals)
{
    var repeatablePanel = globals.form.traveler;
    globals.functions.dispatchEvent(repeatablePanel,'addInstance');
}
```

Vamos a agregar una regla al botón `Add Traveler` para agregar el panel repetible cuando se hace clic:

![Agregar regla de panel](/help/forms/assets/custom-function-add-panel.png)

Consulte el archivo gif siguiente, que muestra que cuando se hace clic en el botón `Add Traveler`, el panel se agrega mediante la propiedad `dispatchEvent`:

![Agregar panel](/help/forms/assets/custom-function-add-panel.gif)

Del mismo modo, agregue la siguiente línea de código, tal como se explica en la sección [create-custom-function](#create-custom-function), para eliminar un panel cuando se haga clic en el botón `Delete Traveler` mediante la propiedad `dispatchEvent`:

```javascript
/**
 
 * @name testRemoveInstance
 * @param {scope} globals
 */
function testRemoveInstance(globals)
{
    var repeatablePanel = globals.form.traveler;
    globals.functions.dispatchEvent(repeatablePanel, 'removeInstance');
} 
```

Vamos a agregar una regla al botón `Delete Traveler` para eliminar el panel repetible cuando se hace clic:

![Eliminar regla de panel](/help/forms/assets/custom-function-delete-panel.png)

Consulte el archivo gif siguiente, que muestra que cuando se hace clic en el botón `Delete Traveler`, el panel del viajero se elimina utilizando la propiedad `dispatchEvent`:

![Eliminar panel](/help/forms/assets/custom-function-delete-panel.gif)

## Problema conocido

* Las funciones personalizadas no admiten literales de expresión regular de JavaScript. El uso de literales regex en una función personalizada provoca errores durante la ejecución. Por ejemplo:
  `const pattern = /^abc$/;`

  Para garantizar la compatibilidad, utilice el constructor RegExp en las funciones personalizadas.

  `const pattern = new RegExp("^abc$");`
Refactorice las expresiones regulares para utilizar el constructor RegExp y garantizar una ejecución coherente y fiable.

## Solución de problemas

* Si el controlador de envío personalizado no funciona como se espera en los formularios o proyectos de AEM existentes, realice los siguientes pasos:
   * Asegúrese de que la versión de los componentes principales [se haya actualizado a la versión 3.0.18 y posteriores](https://github.com/adobe/aem-core-forms-components). Sin embargo, para los proyectos y formularios de AEM existentes, hay que seguir algunos pasos adicionales:

   * Para el proyecto de AEM, el usuario debe reemplazar todas las instancias de `submitForm('custom:submitSuccess', 'custom:submitError')` por `submitForm()` e implementar el proyecto a través de la canalización de Cloud Manager.

   * En el caso de los formularios existentes, si los controladores de envío personalizados no funcionan correctamente, el usuario debe abrir y guardar la regla `submitForm` en el botón **Enviar** mediante el Editor de reglas. Esta acción reemplaza la regla existente de `submitForm('custom:submitSuccess', 'custom:submitError')` por `submitForm()` en el formulario.

## Véase también

{{see-also-rule-editor}}
