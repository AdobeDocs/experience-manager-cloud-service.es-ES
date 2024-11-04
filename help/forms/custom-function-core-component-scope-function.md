---
title: Introducción a los objetos de ámbito en funciones personalizadas
description: El formulario admite objetos de ámbito en funciones personalizadas que se pasan como último argumento a funciones cuando se ejecuta la regla.
keywords: objetos scope en funciones personalizadas, objetos globales, objetos field.
feature: Adaptive Forms, Core Components
role: User, Developer
source-git-commit: af211649a4f22d06f4e8669335a8267ee948a408
workflow-type: tm+mt
source-wordcount: '406'
ht-degree: 0%

---


# Objeto Scope en funciones personalizadas

En Forms adaptable, se pasa un objeto de ámbito como el último argumento a las funciones cuando se ejecuta una regla. Se puede utilizar para leer las propiedades del formulario/campo y modificar el formulario desde las funciones. El objeto de ámbito contiene un objeto proxy de solo lectura para el formulario, el evento activado y el campo de destino. Se puede tener acceso a las propiedades de formulario y campo mediante el objeto de ámbito adjuntando `$`, por ejemplo, `scope.form.$id` y `scope.field.$id`, respectivamente.

## Funciones de modificación de formularios que utilizan un objeto de ámbito

El objeto de ámbito tiene las siguientes funciones para la modificación del formulario:

| Función | Sintaxis | Descripción | Muestra de código |
|-----------------|----------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------|-----------------------------|
| **setProperty** | `setProperty(any $element, any $payload)` | Establece una propiedad de `$element` mediante `$payload`. | [Haga clic aquí](/help/forms/custom-function-core-components-use-cases.md#show-a-panel-using-the-setproperty-rule) para ver el ejemplo. |
| **validar** | `validate([any $element])` | Ejecuta la validación en `$element`. Si no se proporciona ningún elemento, se valida todo el formulario. | [Haga clic aquí](/help/forms/custom-function-core-components-use-cases.md#validate-the-field) para ver el ejemplo. |
| **restablecer** | `reset([any $element])` | Restablece `$element`. Si no se proporciona ningún elemento, se restablece todo el formulario. | [Haga clic aquí](/help/forms/custom-function-core-components-use-cases.md#reset-a-panel) para ver el ejemplo. |
| **importData** | `importData(any $payload)` | Importa datos al formulario y reemplaza los datos de formulario existentes. | [Haga clic aquí](/help/forms/custom-function-core-components-use-cases.md#pre-fill-the-field-with-a-value-when-the-form-loads) para ver el ejemplo. |
| **exportData** | `exportData()` | Devuelve los datos del formulario. | [Haga clic aquí](/help/forms/custom-function-core-components-use-cases.md#submit-altered-data-to-the-server) para ver el ejemplo. |
| **submitForm** | `submitForm(any $data [, boolean $validate_form = true, string $submit_as = 'multipart/form-data'])` | Déclencheur el envío de un formulario. El parámetro `$data` especifica lo que se va a enviar y `$submit_as` define el tipo de contenido (el valor predeterminado es &quot;multipart/form-data&quot;). El elemento opcional `$validate_form` determina si el formulario debe validarse (valor predeterminado: true). Una vez realizado correctamente, se activa `submitSuccess`; si se produce un error, se activa `submitError`. | [Haga clic aquí](/help/forms/custom-function-core-components-use-cases.md#submit-altered-data-to-the-server) para ver el ejemplo. |
| **setFocus** | `setFocus(any $element [, FocusOption $focusOption])` | Establece el enfoque en `$element`, que puede ser un panel o un campo. Si no se proporciona ningún elemento, el enfoque se establece en el campo que activó la regla. El parámetro `$focusOption` opcional (de tipo enum `FocusOption`) especifica si se debe centrar en &#39;nextItem&#39; o &#39;previousItem&#39; en relación con `$element`. Si se especifica un panel, la navegación se restringe a ese panel; con un campo, la navegación se produce en el panel principal. | [Haga clic aquí](/help/forms/custom-function-core-components-use-cases.md#set-focus-on-the-specific-field) para ver el ejemplo. |
| **EventoEnvío** | `dispatchEvent(any $element, string $eventName [, any $payload])` | Envía un evento de tipo `$eventName` en el elemento especificado por `$element`. Si no se proporciona ningún elemento, el evento se enviará en el formulario. El elemento opcional `$payload` está disponible para las expresiones que administran el evento. | [Haga clic aquí](/help/forms/custom-function-core-components-use-cases.md#add-or-delete-repeatable-panel-using-the-dispatchevent-property) para ver el ejemplo. |
| **markFieldAsInvalid** | `markFieldAsInvalid(string $fieldIdentifier, string $validationMessage [, any $option = {useId: true}])` | Marca el campo identificado por `$fieldIdentifier` como no válido y establece el mensaje de validación en `$validationMessage`. El parámetro opcional `$option` especifica si `$fieldIdentifier` se interpreta como `id`, `name` o `dataRef`. El valor predeterminado es `{useId: true}`, y los valores admitidos son `{useId: true}`, `{useDataRef: true}` y `{useQualifiedName: true}`. | [Haga clic aquí](/help/forms/custom-function-core-components-use-cases.md#to-display-a-custom-message-at-the-field-level-and-marking-the-field-as-invalid) para ver el ejemplo. |

## Consulte también

{{see-also-rule-editor}}