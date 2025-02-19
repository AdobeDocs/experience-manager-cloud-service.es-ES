---
title: Añadir un controlador de error personalizado en Formularios adaptables basado en componentes principales para Formularios adaptables de AEM
description: AEM Forms proporciona controladores de éxitos y de errores predeterminados para un formulario mediante el punto final REST configurado para invocar un servicio externo. Se puede añadir un controlador de errores predeterminado y otro personalizado en un formulario adaptable de AEM.
keywords: Añadir un controlador de errores personalizado, añadir un controlador de errores predeterminado, añadir un controlador de errores en el formulario, utilizar el servicio de invocación del editor de reglas para añadir un controlador de errores personalizado, configurar el editor de reglas para añadir un controlador de errores personalizado y añadir un controlador de errores personalizado mediante el editor de reglas
contentOwner: Ruchita Srivastav
content-type: reference
feature: Adaptive Forms, Core Components
exl-id: 4496c4cc-a5d7-4f34-91f9-13eded77b362
role: User, Developer
source-git-commit: 10580c1b045c86d76ab2b871ca3c0b7de6683044
workflow-type: ht
source-wordcount: '2332'
ht-degree: 100%

---

# Controladores de errores para formularios adaptables basados en componentes principales {#error-handlers-in-adaptive-form}


| Versión | Vínculo del artículo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | Este artículo |
| AEM 6.5 | [Haga clic aquí](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-core-components/add-custom-error-handler-adaptive-forms-core-components.html?lang=es) |

AEM Forms proporciona controladores de éxito y de error predeterminados para los envíos de formularios. También proporciona una función para personalizar las funciones del controlador de errores. Por ejemplo, puede invocar un flujo de trabajo personalizado en el back-end para códigos de error específicos o informar al cliente de que el servicio está inactivo. Los controladores son funciones del lado del cliente que se ejecutan en función de la respuesta del servidor. Cuando se invoca un servicio externo mediante las API, los datos se transmiten al servidor para su validación, lo que devuelve una respuesta al cliente con información sobre el evento de éxito o error del envío. La información se pasa en forma de parámetros al controlador correspondiente para ejecutar la función. Un controlador de errores ayuda a administrar y mostrar los errores o problemas de validación encontrados.

![flujo de trabajo del controlador de errores para comprender cómo añadir el controlador de errores personalizado en los formularios](/help/forms/assets/error-handler-workflow.png)

El formulario adaptable valida las entradas proporcionadas en los campos en función de criterios de validación predefinidos y comprueba los distintos errores devueltos por el punto final REST configurado para invocar un servicio externo. Puede definir los criterios de validación en función de la fuente de datos que utilice con el formulario adaptable. Por ejemplo, si utiliza los servicios web RESTful como fuente de datos, puede definir los criterios de validación en un archivo de definición Swagger.

Si los valores de entrada cumplen los criterios de validación, los valores se envían al origen de datos; de lo contrario, el formulario adaptable muestra un mensaje de error utilizando un controlador de errores. De forma similar a este enfoque, los formularios adaptables se integran con los controladores de errores personalizados para realizar validaciones de datos. Si los valores de entrada no cumplen los criterios de validación, los mensajes de error se muestran a nivel de campo en el formulario adaptable. Esto ocurre cuando el mensaje de error de validación devuelto por el servidor tiene el formato de mensaje estándar.


## Usos de los controladores de errores {#uses-of-error-handler}

Los controladores de errores se utilizan para varios fines. A continuación se enumeran algunos de los usos de las funciones del controlador de errores:

* **Realizar validación**: la gestión de errores comienza con la validación de las entradas del usuario con reglas o criterios predefinidos. A medida que los usuarios rellenan un formulario adaptable, el controlador de errores valida la entrada para asegurarse de que cumple el formato, la longitud o cualquier otra restricción necesaria.

* **Proporcionar comentarios en tiempo real**: cuando se detecta cualquier error, el controlador de errores muestra comentarios inmediatos al usuario, como mensajes de error en línea debajo de los campos de formulario correspondientes. Estos comentarios ayudan a los usuarios a identificar y corregir errores sin tener que enviar el formulario y esperar una respuesta.


* **Mostrar mensajes de error**: cuando el envío de un formulario adaptable encuentra algún error de validación, el controlador de errores muestra un mensaje de error adecuado. Los mensajes de error deben ser claros, concisos y resaltar los campos específicos que requieren atención.

* **Resalta el campo erróneo**: para llamar la atención del usuario sobre los campos incorrectos específicos, el controlador de errores resalta o diferencia visualmente los campos correspondientes. Se lleva a cabo cambiando el color de fondo, agregando un icono o borde, o cualquier otra señal visual que ayude a los usuarios a localizar rápidamente los errores y solucionarlos.


## Formato de respuesta de errores {#failure-response-format}

Un formulario adaptable muestra los errores en un nivel de campo si los mensajes de error de validación del servidor tienen el siguiente formato estándar.
El siguiente código ilustra la estructura de respuesta a errores existente:

```javascript
   {
    errorCausedBy : "SERVER_SIDE_VALIDATION/SERVICE_INVOCATION_FAILURE"
    errors : [
        {
             errorMessage / errorMessages : <validationMsg> / [<validationMsg>, <validationMsg>]
        }
    ]
    originCode : <target error Code>
    originMessage : <unstructured error message returned by service>
    }
```


Donde:

* `errorCausedBy` describe el motivo del error.
* `errors` menciona la expresión de los campos en los que se han producido errores en los criterios de validación junto con el mensaje de error de validación.
* El campo `originCode` añadido por AEM que contiene el código de estado HTTP devuelto por el servicio externo.
* El campo `originMessage` añadido por AEM que contiene los datos de error sin procesar devueltos por el servicio externo.

Con las mejoras en las funciones y las actualizaciones posteriores en las versiones de AEM Forms, la estructura de respuesta a errores existente ha cambiado a un nuevo formato basado en RFC7807, que es compatible con versiones anteriores de la estructura de respuesta a errores existente:

```javascript
    {
        "type": "SERVER_SIDE_VALIDATION/FORM_SUBMISSION/SERVICE_INVOCATION/FAILURE/VALIDATION_ERROR", (required)
        "title": "Server side validation failed/Third party service invocation failed", (optional)
        "detail": "", (optional)
        "instance": "", (optional)
        "validationErrors" : [ (required)
            {
                "fieldName":"<qualified fieldname of the field whose data sent is invalid>",
                "dataRef":<JSONPath (or XPath) of the data element which is invalid>
                "details": ["Error Message(s) for the field"] (required)
    
            }
        ],
        "originCode": <Origin http status code>, (optional - in case of SERVER_SIDE_VALIDATION)
        "originMessage" : "<unstructured error message returned by service>" (optional - in case of SERVER_SIDE_VALIDATION)
    }
```


>[!NOTE]
>
> * Asegúrese de que la estructura de respuesta de error incluya lo siguiente **fieldName** o **dataRef**.
> * Asegúrese de que el encabezado **ContentType** es **application/problem+json**.

Donde:
* `type (required)` especifica el tipo de error. Puede tener uno de los siguientes valores:
   * `SERVER_SIDE_VALIDATION` indica un error debido a la validación del lado del servidor.
   * `FORM_SUBMISSION` indica un error durante el envío del formulario
   * `SERVICE_INVOCATION` indica un error durante una invocación de servicio de terceros.
   * `FAILURE` indica un error general.
   * `VALIDATION_ERROR` indica un error debido a un error de validación.

* `title (optional)` proporciona un título o una breve descripción del error.
* `detail (optional)` proporciona detalles adicionales sobre el error si es necesario.
* `instance (optional)` representa una instancia o identificador asociado con el error y ayuda a rastrear o identificar la incidencia específica del error.
* `validationErrors (required)` contiene información sobre errores de validación. Incluye los siguientes campos:
   * `fieldname` menciona el nombre de campo cualificado de los campos en los que se han producido errores en los criterios de validación.
   * `dataRef` representa la ruta JSON o XPath de los campos en los que se ha producido un error en la validación.
   * `details` contiene el mensaje de error de validación con el campo erróneo.
* El campo `originCode (optional)` añadido por AEM contiene el código de estado HTTP devuelto por el servicio externo
* El campo `originMessage (optional)` añadido por AEM contiene los datos de error sin procesar devueltos por el servicio externo.

### Formato de respuesta de error de muestra {#sample-error-response-format}

Algunas de las opciones para mostrar las respuestas de error son las siguientes:

+++  Basado en la propiedad fieldName del formulario adaptable


* **`Header:`** `content-type:application/problem+json`
* **`Response:`**

  ```javascript
          {
              "type": "VALIDATION_ERROR",
              "validationErrors": [
              {
              "fieldName": "$form.PetId",
              "dataRef": "",
              "details": [
              "Invalid ID supplied. Provided value is not correct!"
          ]
          }
          ]}
  ```

+++


+++ Basado en la propiedad Referencia de enlace del formulario adaptable

* **`Header:`** `content-type:application/problem+json`
* **`Response:`**

  ```javascript
      {
          "type": "VALIDATION_ERROR",
          "validationErrors": [
          {
              "fieldName": "",
              "dataRef": "$.Pet.id",
              "details": [
              "Invalid ID supplied. Provided value is not correct!"
              ]
              }
      ]}
  ```

Se puede ver el valor de dataRef en la ventana **[!UICONTROL Propiedades]** de un componente del formulario.

+++

## Requisitos para añadir el controlador de error mediante el servicio Invocar del Editor de reglas {#before-you-start-to-add-error-handler}

Antes de añadir un controlador de error mediante el servicio Invocar del Editor de reglas:

* [Habilitar los componentes principales de formularios adaptables para su entorno de AEM Cloud Service](enable-adaptive-forms-core-components.md).

* Obtenga información sobre cómo [crear funciones personalizadas](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/add-rules-and-use-expressions-in-an-adaptive-form/rule-editor.html?lang=es#write-rules).


## Adición de un controlador de error mediante el Editor de reglas {#add-error-handler-using-rule-editor}

Utilizando la acción del [Servicio de invocación del editor de reglas](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/add-rules-and-use-expressions-in-an-adaptive-form/rule-editor.html?lang=es#invoke), se definen los criterios de validación en función de la fuente de datos que se utilice con el formulario adaptable. Por ejemplo, si utiliza los servicios web RESTful como fuente de datos, puede definir los criterios de validación en un archivo de definición Swagger. Gracias a las funciones del controlador de errores y el editor de reglas en los formularios adaptables, se puede administrar y personalizar de forma eficaz la gestión de errores. Las condiciones se definen mediante el Editor de reglas y se configuran las acciones que deben realizarse cuando se activa la regla. Los formularios adaptables validan las entradas que se proporcionan en los campos en función de criterios de validación predefinidos. En caso de que los valores de entrada no cumplan los criterios de validación, los mensajes de error se muestran a nivel de campo en un formulario adaptable.

>[!NOTE]
>
> * Para utilizar los controladores de errores con la acción Invocar servicio del Editor de reglas, configure los formularios adaptables con un modelo de datos de formulario.
> * De forma predeterminada, se proporciona el controlador de errores para mostrar los mensajes de error en los campos si la respuesta de error está en el esquema estándar. También puede llamar al controlador de error predeterminado desde la función del controlador de error personalizado.

Con el editor de reglas, se puede hacer lo siguiente:
* [Añadir la función del controlador de errores predeterminado](#add-default-errror-handler)
* [Añadir función del controlador de errores personalizado](#add-custom-errror-handler)


### Añadir la función del controlador de errores predeterminado {#add-default-errror-handler}

Se admite un controlador de errores predeterminado para mostrar los mensajes de error en los campos si la respuesta de error está en el esquema estándar o en un error de validación del lado del servidor.
Para comprender cómo utilizar un controlador de errores predeterminado con la acción [Invocar servicio del editor de reglas](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/add-rules-and-use-expressions-in-an-adaptive-form/rule-editor.html?lang=es#invoke), vamos a ver un ejemplo de formulario adaptable con dos campos, **ID de mascota** y **Nombre de mascota**. Además, usaremos un controlador de errores predeterminado en el campo **ID de mascota** para comprobar si hay varios errores devueltos por el punto final REST configurado para invocar un servicio externo, por ejemplo, `200 - OK`, `404 - Not Found` y `400 - Bad Request`.  Para añadir un controlador de error predeterminado mediante la acción Invocar servicio del Editor de reglas, ejecute los siguientes pasos:

1. Abra el formulario adaptable en el modo de creación, seleccione cualquier componente del formulario y seleccione **[!UICONTROL Editor de reglas]** para abrir el editor de reglas.
1. Seleccione **[!UICONTROL Crear]**.
1. Crear una condición en la sección **Cuando** de la regla. Por ejemplo, **cuando se cambia[Nombre del campo ID de mascota]**. Seleccione “se ha cambiado” de la lista desplegable **Seleccionar estado**.
1. En la sección **Entonces**, seleccione **[!UICONTROL Invocar servicio]** de la lista desplegable **Seleccionar acción**.
1. Seleccione un **servicio Post** y sus enlaces de datos correspondientes en la sección **Entrada**. Por ejemplo, para validar **ID de mascota**, seleccione un **servicio Post** como **GET /pet/{petId}** y seleccione **ID de mascota** en la sección **Entrada**.
1. Seleccione los enlaces de datos en la sección **Salida**. Seleccione **Nombre de mascota** en la sección **Salida**.
1. Seleccione **[!UICONTROL Controlador de errores personalizado]** en la sección **Controlador de errores**.
1. Haga clic en **[!UICONTROL Listo]**.

![añadir un controlador de error predeterminado para las comprobaciones de validación de campos en un formulario](/help/forms/assets/default-error-handler.png)

Como resultado de esta regla, los valores introducidos para **ID de mascota** comprueban la validación de **Nombre de mascota** utilizando el servicio externo invocado por el punto final REST. Si los criterios de validación basados en la fuente de datos fallan, los mensajes de error se muestran en el nivel de campo.

![mostrar el mensaje de error predeterminado cuando se añade un controlador de error predeterminado en un formulario para controlar las respuestas de error](/help/forms/assets/default-error-message.png)

### Añadir función del controlador de errores personalizado {#add-custom-errror-handler}

Puede añadir una función del controlador de errores personalizado para realizar algunas de las acciones como:

* gestionar respuestas de error que utilizan respuestas de error no estándar o estándar. Es importante tener en cuenta que estas respuestas de error no estándar no cumplen con el [esquema estándar de respuestas de error](#failure-response-format).
* enviar eventos de Analytics a cualquier plataforma de Analytics. Por ejemplo, Adobe Analytics.
* mostrar cuadro de diálogo modal con mensajes de error.

Además de las acciones mencionadas, los controladores de errores predeterminados se pueden utilizar para ejecutar funciones personalizadas que cumplan con los requisitos específicos del usuario.

El controlador de errores personalizado es una función (Biblioteca de cliente) diseñada para responder a los errores devueltos por un servicio externo y proporcionar una respuesta personalizada a los usuarios finales. Cualquier biblioteca de cliente con anotación `@errorHandler` se considera que es una función del controlador de errores personalizado. Esta anotación identifica la función de controlador de errores especificada en el archivo `.js`.
Para comprender cómo crear y utilizar un controlador de errores personalizado con la acción [Invocar servicio del editor de reglas](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/add-rules-and-use-expressions-in-an-adaptive-form/rule-editor.html?lang=es#invoke), vamos a ver un ejemplo de formulario adaptable con dos campos, **ID de mascota** y **Nombre de mascota**. Además, usar un controlador de errores personalizado en el campo **ID de mascota** para comprobar si hay varios errores devueltos por el punto final REST configurado para invocar un servicio externo, por ejemplo, `200 - OK`, `404 - Not Found` y `400 - Bad Request`.

Para añadir y utilizar un controlador de errores personalizado en un formulario adaptable, realice los siguientes pasos:
1. [Crear un controlador de errores personalizado](#create-custom-error-message)
1. [Utilice el Editor de reglas para configurar el controlador de errores personalizado](#use-custom-error-handler)

#### 1. Crear un controlador de errores personalizado {#create-custom-error-message}

Para crear una función de error personalizada, realice los siguientes pasos:

Para crear una función de error personalizada, realice los siguientes pasos:

1. [Clone su repositorio de AEM Forms as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html?lang=es#accessing-git).
1. Crear una carpeta dentro de la carpeta `[AEM Forms as a Cloud Service repository folder]/apps/`. Por ejemplo, cree una carpeta denominada `experience-league`
1. Vaya a `[AEM Forms as a Cloud Service repository folder]/apps/[AEM Project Folder]/experience-league/` y cree un `ClientLibraryFolder` como `clientlibs`.
1. Cree una carpeta con el nombre `js`.
1. Navegue hasta la carpeta `[AEM Forms as a Cloud Service repository folder]/apps/[AEM Project Folder]/clientlibs/js`. 
1. Añada un archivo JavaScript, por ejemplo `function.js`.  El archivo contiene el código del controlador de errores personalizado.
Vamos a añadir el siguiente código al archivo JavaScript para mostrar la respuesta y los encabezados, recibidos del extremo del servicio REST, en la consola del explorador.

   ```javascript
       /** 
       Custom Error handler
       * @name customErrorHandler Custom Error Handler Function
       * @errorHandler
       */
       function customErrorHandler(response, headers, globals)
   {
       console.log("Custom Error Handler processing start...");
       console.log("response:"+JSON.stringify(response));
       console.log("headers:"+JSON.stringify(headers));
       alert("CustomErrorHandler - Enter valid PetId.")
       console.log("Custom Error Handler processing end...");
       return true; // true - call default error handler, false - don't call default error handler.
   }
   ```
   En el código anterior, `return true` invoca automáticamente el controlador de errores predeterminado. Para evitar que se llame al controlador de errores predeterminado de forma predeterminada, incluya `return false`.

   >[!NOTE]
   >
   > En el archivo `.content.xml`, añada `categories = [custom-errorhandler-name]`. Por ejemplo, en este caso, [custom-errorhandler-name] se proporciona como `customfunctionsdemoV2`.


1. Guarde el archivo `function.js`.
1. Navegue hasta la carpeta `[AEM Forms as a Cloud Service repository folder]/apps/[AEM Project Folder]/clientlibs/js`. 
1. Añada un archivo de texto como `js.txt`. El archivo contiene lo siguiente:

   ```javascript
       #base=js
       functions.js
   ```

1. Guarde el archivo `js.txt`.\
   La estructura de carpetas creada tiene este aspecto:

   ![Estructura de carpetas de la biblioteca de cliente creada](/help/forms/assets/customclientlibrary_folderstructure.png)

   >[!NOTE]
   >
   > Para obtener más información sobre cómo crear funciones personalizadas, haga clic en [funciones personalizadas en el Editor de reglas](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/add-rules-and-use-expressions-in-an-adaptive-form/rule-editor.html?lang=es#write-rules).


1. Añada, confirme e inserte los cambios en el repositorio mediante los siguientes comandos:

   ```javascript
       git add .
       git commit -a -m "Adding error handling files"
       git push
   ```

1. [Ejecutar la canalización](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html?lang=es#setup-pipeline). 

Una vez que la canalización se haya ejecutado correctamente, el controlador de errores personalizado estará disponible en el editor de reglas del formulario adaptable. Ahora, vamos a comprender cómo configurar y utilizar un controlador de errores personalizado mediante el servicio Invocar del Editor de reglas de AEM Forms.

#### 2. Utilizar el Editor de reglas para configurar el controlador de errores personalizado {#use-custom-error-handler}

Antes de implementar el controlador de error personalizado en un formulario adaptable, asegúrese de que el nombre de la biblioteca de cliente en la **[!UICONTROL Categoría de biblioteca del cliente]** corresponda con el nombre especificado en la opción de categorías del archivo `.content.xml`.

![Añadir el nombre de la biblioteca de cliente en la configuración del contenedor del formulario adaptable](/help/forms/assets/client-library-category-name-core-component.png)

Para utilizar un controlador de errores personalizado utilizando la acción **[!UICONTROL Invocar servicio del Editor de reglas]**:

1. Abra el formulario adaptable en el modo de creación, seleccione cualquier componente del formulario y seleccione **[!UICONTROL Editor de reglas]** para abrir el editor de reglas.
1. Seleccione **[!UICONTROL Crear]**.
1. Crear una condición en la sección **Cuando** de la regla. Por ejemplo, cuando se ha cambiado el **[Nombre del campo ID de mascota]**, seleccione **se ha cambiado** en la lista desplegable **Seleccionar estado**.
1. En la sección **Entonces**, seleccione **[!UICONTROL Invocar servicio]** de la lista desplegable **Seleccionar acción**.
1. Seleccione un **servicio Post** y sus enlaces de datos correspondientes en la sección **Entrada**. Por ejemplo, para validar **ID de mascota**, seleccione un **servicio Post** como **GET /pet/{petId}** y seleccione **ID de mascota** en la sección **Entrada**.
1. Seleccione los enlaces de datos en la sección **Salida**. Por ejemplo, seleccione **Nombre de mascota** en la sección **Salida**.
1. Seleccione **[!UICONTROL Controlador de errores personalizado]** en la sección **[!UICONTROL Controlador de errores]**.
1. Haga clic en **[!UICONTROL Listo]**.

![añadir un controlador de errores personalizado en un formulario para controlar las respuestas de error](/help/forms/assets/custom-error-handler.png)


Como resultado de esta regla, los valores introducidos para **ID de mascota** comprueban la validación de **Nombre de mascota** utilizando el servicio externo invocado por el punto final REST. Si los criterios de validación basados en la fuente de datos fallan, los mensajes de error se muestran en el nivel de campo.

![añadir un controlador de error personalizado en un formulario para controlar las respuestas de error](/help/forms/assets/custom-error-handler-message-core-component.png)

Abra la consola del explorador y compruebe la respuesta y el encabezado, recibidos del punto final de servicio REST, para el mensaje de error de validación.


La función del controlador de errores personalizado es responsable de ejecutar acciones adicionales, como mostrar un cuadro de diálogo modal o enviar un evento de análisis, en función de la respuesta de error. Una función del controlador de errores personalizado proporciona la flexibilidad para adaptar la gestión de errores a los requisitos específicos del usuario.

<!-- 

## Configure Adaptive Form submission to add custom handlers {#configure-adaptive-form-submission}

If the server validation error message does not display in the standard format, you can enable asynchronous submission and add a custom error handler on Adaptive Form submission to convert the message into a standard format.

### Configure asynchronous Adaptive Form submission {#configure-asynchronous-adaptive-form-submission}

Before adding custom handler, you must configure the adaptive form for asynchronous submission. Execute the following steps:

1. In adaptive form authoring mode, select the Form Container object and select ![adaptive form properties](assets/configure_icon.png) to open its properties.
1. In the **[!UICONTROL Submission]** properties section, enable **[!UICONTROL Use asynchronous submission]**.
1. Select **[!UICONTROL Revalidate on server]** to validate the input field values on server before submission.
1. Select the Submit Action:

    * Select **[!UICONTROL Submit using Form Data Model]** and select the appropriate data model, if you are using RESTful web service based [form data model](work-with-form-data-model.md) as the data source.
    * Select **[!UICONTROL Submit to REST Service endpoint]** and specify the **[!UICONTROL Redirect URL/Path]**, if you are using RESTful web services as the data source.

    ![adaptive form submission properties](assets/af_submission_properties.png)

1. Select ![Save](assets/save_icon.png) to save the properties.

### Add custom error handler on Adaptive Form submission {#add-custom-error-handler-af-submission}

AEM Forms provides out-of-the-box success and error handlers for form submissions. Handlers are client-side functions that execute based on the server response. When an Adaptive Form is submitted, the data is transmitted to the server for validation, which returns a response to the client with information about the success or error event for the submission. The information is passed as parameters to the relevant handler to execute the function.

Execute the following steps to add custom error handler on Adaptive Form submission:

1. Open an Adaptive Form in authoring mode, select any form object, and select  to open the rule editor.
1. Select **[!UICONTROL Form]** in the Form Objects tree and select **[!UICONTROL Create]**.
1. Select **[!UICONTROL Error in Submission]** from the Event drop-down list.
1. Write a rule to convert custom error structure to the standard error structure and select **[!UICONTROL Done]** to save the rule.

The following is a sample code to convert a custom error structure to the standard error structure:

```javascript
var data = $event.data;
var som_map = {
    "id": "guide[0].guide1[0].guideRootPanel[0].Pet[0].id_1[0]",
    "name": "guide[0].guide1[0].guideRootPanel[0].Pet[0].name_2[0]",
    "status": "guide[0].guide1[0].guideRootPanel[0].Pet[0].status[0]"
};

var errorJson = {};
errorJson.errors = [];

if (data) {
    if (data.originMessage) {
        var errorData;
        try {
            errorData = JSON.parse(data.originMessage);
        } catch (err) {
            // not in json format
        }

        if (errorData) {
            Object.keys(errorData).forEach(function(key) {
                var som_key = som_map[key];
                if (som_key) {
                    var error = {};
                    error.somExpression = som_key;
                    error.errorMessage = errorData[key];
                    errorJson.errors.push(error);
                }
            });
        }
        window.guideBridge.handleServerValidationError(errorJson);
    } else {
        window.guideBridge.handleServerValidationError(data);
    }
}
```

The `var som_map` lists the SOM expression of the Adaptive Form fields that you want to transform into the standard format. You can view the SOM expression of any field in an adaptive form by tapping the field and selecting **[!UICONTROL View SOM Expression]**.

Using this custom error handler, the adaptive form converts the fields listed in `var som_map` to standard error message format. As a result, the validation error messages display at field-level in the adaptive form.

 -->

## Información adicional {#additional-information}

* [Crear un formulario adaptable independiente basado en componentes principales](/help/forms/creating-adaptive-form-core-components.md)
* [Creación de estilos o temáticas para los formularios](/help/forms/using-themes-in-core-components.md)
* [Crear o agregar un formulario adaptable a una página de AEM Sites](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md)

## Ver también {#see-also}

{{see-also}}

