---
title: API para invocar el servicio del Modelo de datos de formulario desde Forms adaptable
seo-title: API to invoke Form Data Model service from Adaptive Forms
description: Explica la API de invokeWebServices que puede utilizar para invocar servicios web escritos en WSDL desde un campo Formulario adaptable .
seo-description: Explains the invokeWebServices API that you can use to invoke web services written in WSDL from within an Adaptive Form field.
uuid: 40561086-e69d-4e6a-9543-1eb2f54cd836
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: aa3e50f1-8f5a-489d-a42e-a928e437ab79
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '480'
ht-degree: 0%

---


# API para invocar el servicio del Modelo de datos de formulario desde Forms adaptable {#api-to-invoke-form-data-model-service-from-adaptive-forms}

## Información general {#overview}

[!DNL AEM Forms] permite a los autores de formularios simplificar y mejorar aún más la experiencia de cumplimentación de formularios invocando los servicios configurados en un Modelo de datos de formulario desde un campo Formulario adaptable . Para invocar un servicio de modelo de datos, puede crear una regla en el editor visual o especificar un JavaScript utilizando la variable `guidelib.dataIntegrationUtils.executeOperation` API en el editor de código de la variable [editor de reglas](rule-editor.md).

Este documento se centra en escribir un JavaScript usando la variable `guidelib.dataIntegrationUtils.executeOperation` API para invocar un servicio.

## Uso de la API {#using-the-api}

La variable `guidelib.dataIntegrationUtils.executeOperation` API invoca un servicio desde un campo de formulario adaptable. La sintaxis de la API es la siguiente:

```javascript
guidelib.dataIntegrationUtils.executeOperation(operationInfo, inputs, outputs)
```

La estructura del `guidelib.dataIntegrationUtils.executeOperation` La API especifica detalles sobre la operación del servicio. La sintaxis de la estructura es la siguiente:

```javascript
var operationInfo = {
formDataModelId,
operationTitle,
operationName
};
var inputs = {
inputField1,
inputFieldN
};
var outputs = {
outputField1,
outputFieldN
}
```

La estructura de la API especifica los siguientes detalles sobre la operación del servicio.

<table>
 <tbody>
  <tr>
   <th>Parámetro</th>
   <th>Descripción</th>
  </tr>
  <tr>
   <td><code>operationInfo</code></td>
   <td>Estructura para especificar el identificador del Modelo de datos de formulario, el título de la operación y el nombre de la operación</td>
  </tr>
  <tr>
   <td><code>formDataModelId</code></td>
   <td>Especifica la ruta del repositorio al Modelo de datos de formulario, incluido su nombre</td>
  </tr>
  <tr>
   <td><code>operationName</code></td>
   <td>Especifica el nombre de la operación de servicio que se va a ejecutar</td>
  </tr>
  <tr>
   <td><code>inputs</code></td>
   <td>Asigna uno o varios objetos de formulario a los argumentos de entrada para la operación de servicio</td>
  </tr>
  <tr>
   <td><code>Outputs</code></td>
   <td>Asigna uno o varios objetos de formulario a los valores de salida de la operación de servicio para rellenar los campos de formulario<br /> </td>
  </tr>
  <tr>
   <td><code>success</code></td>
   <td>Devuelve valores basados en los argumentos de entrada para la operación de servicio. Es un parámetro opcional utilizado como función de llamada de retorno.<br /> </td>
  </tr>
  <tr>
   <td><code>failure</code></td>
   <td>Muestra un mensaje de error si la función de llamada de retorno de éxito no muestra los valores de salida en función de los argumentos de entrada. Es un parámetro opcional utilizado como función de llamada de retorno.<br /> </td>
  </tr>
 </tbody>
</table>

## Secuencia de comandos de ejemplo para invocar un servicio {#sample-script-to-invoke-a-service}

El siguiente script de ejemplo utiliza la variable `guidelib.dataIntegrationUtils.executeOperation` API para invocar el `getAccountById` operación de servicio configurada en el `employeeAccount` modelo de datos de formulario.

La variable `getAccountById` toma el valor en la variable `employeeID` campo de formulario como entrada para la variable `empId` y devuelve el nombre del empleado, el número de cuenta y el saldo de cuenta del empleado correspondiente. Los valores de salida se rellenan en los campos de formulario especificados. Por ejemplo, el valor de `name` se rellena en la variable `fullName` elemento de formulario y valor para `accountNumber` argumento en `account` elemento de formulario.

```javascript
var operationInfo = {
"formDataModelId": "/content/dam/formsanddocuments-fdm/employeeAccount",
"operationName": "getAccountDetails"
};
var inputs = {
"empid" : employeeID
};
var outputs = {
"name" : fullName,
"accountNumber" : account,
"balance" : balance
};
guidelib.dataIntegrationUtils.executeOperation(operationInfo, inputs, outputs);
```

## Uso de la API con función de llamada de retorno {#using-the-api-callback}

También puede invocar el servicio Modelo de datos de formulario utilizando la variable `guidelib.dataIntegrationUtils.executeOperation` API con una función de llamada de retorno. La sintaxis de la API es la siguiente:

```javascript
guidelib.dataIntegrationUtils.executeOperation(operationInfo, inputs, outputs, callbackFunction)
```

La función de llamada de retorno puede tener `success` y `failure` funciones de llamada de retorno.

### Secuencia de comandos de ejemplo con funciones de llamada de retorno de éxito y error {#callback-function-success-failure}

El siguiente script de ejemplo utiliza la variable `guidelib.dataIntegrationUtils.executeOperation` API para invocar el `GETOrder` operación de servicio configurada en el `employeeOrder` modelo de datos de formulario.

La variable `GETOrder` toma el valor en la variable `Order ID` campo de formulario como entrada para la variable `orderId` y devuelve el valor de cantidad de pedido en la variable `success` función de llamada de retorno.  Si la variable `success` función de llamada de retorno no devuelve la cantidad de pedido, la función `failure` función callback muestra `Error occured` mensaje.

>[!NOTE]
>
> Si usa la variable `success` función de llamada de retorno, los valores de salida no se rellenan en los campos de formulario especificados.

```javascript
var operationInfo = {
    "formDataModelId": "/content/dam/formsanddocuments-fdm/employeeOrder",
    "operationTitle": "GETOrder",
    "operationName": "GETOrder"
};
var inputs = {
    "orderId" : Order ID
};
var outputs = {};
var success = function (wsdlOutput, textStatus, jqXHR) {
order_quantity.value = JSON.parse(wsdlOutput).quantity;
 };
var failure = function(){
alert('Error occured');
};
guidelib.dataIntegrationUtils.executeOperation(operationInfo, inputs, outputs, success, failure);
```
