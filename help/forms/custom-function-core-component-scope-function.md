---
title: Introducción a los objetos de ámbito en funciones personalizadas
description: El formulario admite objetos de ámbito en funciones personalizadas que se pasan como último argumento a funciones cuando se ejecuta la regla.
keywords: objetos scope en funciones personalizadas, objetos globales, objetos field.
feature: Adaptive Forms, Core Components
role: User, Developer
exl-id: 248c75a5-6335-41d2-aa0a-28a20a710f88
source-git-commit: e2bc958104bd9b75845ad2c213eec18d2560a3a4
workflow-type: tm+mt
source-wordcount: '458'
ht-degree: 1%

---

# Objeto de ámbito en funciones personalizadas

En Forms adaptable, se pasa un objeto de ámbito como el último argumento a las funciones cuando se ejecuta una regla. Se puede utilizar para leer las propiedades del formulario/campo y modificar el formulario desde las funciones. El objeto de ámbito contiene un objeto proxy de solo lectura para el formulario, el evento activado y el campo de destino. Se puede tener acceso a las propiedades de formulario y campo mediante el objeto de ámbito adjuntando `$`, por ejemplo, `scope.form.$id` y `scope.field.$id`, respectivamente.

## Funciones de modificación de formularios que utilizan un objeto de ámbito

El objeto de ámbito tiene las siguientes funciones para la modificación del formulario:

| Función | Sintaxis | Descripción | Muestra de código |
|-----------------|--------|-------------|-------------|
| **setProperty** | `setProperty(any $element, any $payload)` | Establece una propiedad en el campo de destino mediante `$payload`. | [Haga clic aquí](/help/forms/custom-function-core-components-use-cases.md#show-a-panel-using-the-setproperty-rule) para ver el ejemplo. |
| **validar** | `validate([any $element])` | Ejecuta la validación en el campo de destino. Ejecuta la validación en todo el formulario si no se proporciona ningún destino y devuelve una matriz de errores de validación. | [Haga clic aquí](/help/forms/custom-function-core-components-use-cases.md#validate-the-field) para ver el ejemplo. |
| **restablecer** *(obsoleto)* | `reset([any $element])` | Obsoleto. Utilice `dispatchEvent($target, 'reset')` en su lugar. Restablece el campo de destino o, si no se proporciona ningún destino, restablece todo el formulario. | [Haga clic aquí](/help/forms/custom-function-core-components-use-cases.md#reset-a-panel) para ver el ejemplo. |
| **importData** | `importData(any $payload)` | Importa datos al formulario y reemplaza los datos de formulario existentes. Si se especifica `qualifiedName`, los datos solo se importan en ese campo contenedor. | [Haga clic aquí](/help/forms/custom-function-core-components-use-cases.md#pre-fill-the-field-with-a-value-when-the-form-loads) para ver el ejemplo. |
| **exportData** | `exportData()` | Devuelve los datos del formulario. | [Haga clic aquí](/help/forms/custom-function-core-components-use-cases.md#submit-altered-data-to-the-server) para ver el ejemplo. |
| **submitForm** | `submitForm(any $data [, boolean $validate_form = true, string $submit_as = 'multipart/form-data'])` | Déclencheur el envío de un formulario. Puede especificar lo que desea enviar mediante el parámetro `$payload` y establecer el tipo de contenido mediante el parámetro `$contentType`. Los datos se envían como `multipart/form-data` de manera predeterminada. El parámetro opcional `$validateForm` especifica si el formulario debe validarse antes del envío (valor predeterminado: true). Una vez realizado correctamente, se activa `submitSuccess`; si se produce un error, se activa `submitError`. | [Haga clic aquí](/help/forms/custom-function-core-components-use-cases.md#submit-altered-data-to-the-server) para ver el ejemplo. |
| **setFocus** | `setFocus(any $element [, FocusOption $focusOption])` | Establece el enfoque en el campo de destino, que puede ser un panel o un campo de formulario. Si no se proporciona ningún objetivo, el enfoque se establece en el campo que activó la regla. El parámetro opcional `$focusOption` especifica si el elemento siguiente o anterior relativo al destino debe estar enfocado. Valores compatibles: `'nextItem'`, `'previousItem'`. Si se utiliza con un panel, la navegación se restringe a ese panel. Si se utiliza con un campo, la navegación se produce dentro del panel principal de ese campo. | [Haga clic aquí](/help/forms/custom-function-core-components-use-cases.md#set-focus-on-the-specific-field) para ver el ejemplo. |
| **EventoEnvío** | `dispatchEvent(any $element, string $eventName [, any $payload])` | Envía un evento de tipo `$eventName` en el elemento determinado por `$target`. Si no se proporciona ningún destino, el evento se enviará en el formulario. El elemento opcional `$payload` está disponible para las expresiones que administran el evento. El parámetro `$dispatch` opcional controla el comportamiento de propagación de eventos. | [Haga clic aquí](/help/forms/custom-function-core-components-use-cases.md#add-or-delete-repeatable-panel-using-the-dispatchevent-property) para ver el ejemplo. |
| **markFieldAsInvalid** | `markFieldAsInvalid(string $fieldIdentifier, string $validationMessage [, any $option = {useId: true}])` | Marca el campo identificado por `$fieldIdentifier` como no válido y muestra `$validationMessage`. El parámetro opcional `$option` especifica si `$fieldIdentifier` se interpreta como `id`, `dataRef` o `qualifiedName`. El valor predeterminado es `{useId: true}`. Valores compatibles: `{useId: true}`, `{useDataRef: true}`, `{useQualifiedName: true}`. | [Haga clic aquí](/help/forms/custom-function-core-components-use-cases.md#to-display-a-custom-message-at-the-field-level-and-marking-the-field-as-invalid) para ver el ejemplo. |

## Véase también

{{see-also-rule-editor}}

