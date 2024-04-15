---
title: Crear y agregar funciones personalizadas en un formulario adaptable
description: AEM Forms admite funciones personalizadas que permiten a los usuarios crear y utilizar sus propias funciones dentro del editor de reglas.
keywords: Agregar una función personalizada, utilizar una función personalizada, crear una función personalizada, utilizar una función personalizada en el editor de reglas.
contentOwner: Ruchita Srivastav
content-type: reference
feature: Adaptive Forms, Core Components
exl-id: 24607dd1-2d65-480b-a831-9071e20c473d
source-git-commit: 593a2b2930093d29a22f6c1ff391c11db9bda7dc
workflow-type: tm+mt
source-wordcount: '3104'
ht-degree: 4%

---


<span class="preview"> Este artículo incluye contenido para algunas funciones previas al lanzamiento. Solo se puede acceder a estas funciones previas al lanzamiento a través de nuestra [canal previo al lanzamiento](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/prerelease.html?lang=es#new-features). Las funciones del programa previo al lanzamiento son las siguientes:
* Compatibilidad con parámetros opcionales en funciones personalizadas
* Función de almacenamiento en caché para funciones personalizadas
* Los objetos de campo y objeto de ámbito global admiten funciones personalizadas
* Compatibilidad con funciones modernas de JavaScript como las funciones izquierda y flecha (compatibilidad con ES10).
Asegúrese de que la variable [El componente principal está configurado en la versión 3.0.8.](https://github.com/adobe/aem-core-forms-components) para utilizar funciones previas al lanzamiento en funciones personalizadas. </span>

# Funciones personalizadas en Forms adaptable (componentes principales)

## Introducción

AEM Forms admite funciones personalizadas, lo que permite a los usuarios definir funciones de JavaScript para implementar reglas comerciales complejas. Estas funciones personalizadas amplían las capacidades de los formularios al facilitar la manipulación y el procesamiento de los datos introducidos para satisfacer requisitos específicos. También permiten la modificación dinámica del comportamiento del formulario en función de criterios predefinidos.

### Usos de las funciones personalizadas {#uses-of-custom-function}

Las ventajas de utilizar funciones personalizadas en Forms adaptable son:
* **Procesamiento de datos**: Las funciones personalizadas ayudan a procesar los datos introducidos en los campos de formulario.
* **Validación de datos**: las funciones personalizadas permiten realizar comprobaciones personalizadas en las entradas del formulario y proporcionar mensajes de error especificados.
* **Comportamiento dinámico**: las funciones personalizadas le permiten controlar el comportamiento dinámico de los formularios en función de condiciones específicas. Por ejemplo, puede mostrar u ocultar campos, modificar valores de campos o ajustar la lógica del formulario de forma dinámica.
* **Integración**: Puede utilizar funciones personalizadas para integrarse con API o servicios externos. Ayuda a recuperar datos de fuentes externas, enviar datos a extremos REST externos o realizar acciones personalizadas basadas en eventos externos.

Las funciones personalizadas son esencialmente bibliotecas de cliente que se agregan en el archivo JavaScript. Una vez creada una función personalizada, esta estará disponible en el editor de reglas para que la seleccione el usuario en un formulario adaptable. Las funciones personalizadas se identifican mediante anotaciones JavaScript en el editor de reglas.

### Anotaciones JavaScript compatibles con la función personalizada {#js-annotations}

Las anotaciones de JavaScript se utilizan para proporcionar metadatos para el código JavaScript. Incluye comentarios que comienzan con símbolos específicos como, por ejemplo, /** y @. Las anotaciones proporcionan información importante sobre funciones, variables y otros elementos del código. El formulario adaptable admite las siguientes anotaciones de JavaScript para funciones personalizadas:

#### Nombre

El nombre se utiliza para identificar la función personalizada en el editor de reglas de un formulario adaptable. Las siguientes sintaxis se utilizan para asignar un nombre a una función personalizada:

* `@name [functionName] <Function Name>`
* `@function [functionName] <Function Name>`
* `@func [functionName] <Function Name>`.
  `functionName` es el nombre de la función. No se permiten espacios.
  `<Function Name>` es el nombre para mostrar de la función en el editor de reglas de un formulario adaptable.
Si el nombre de la función es idéntico al nombre de la función en sí, puede omitir `[functionName]` de la sintaxis. <!-- For example,  in the `calculateAge` custom function, the name is defined as:
`* @name calculateAge` -->

#### Parámetro

El parámetro es una lista de argumentos que utilizan las funciones personalizadas. Una función puede admitir varios parámetros. Las siguientes sintaxis se utilizan para definir un parámetro en una función personalizada:

* `@param {type} name <Parameter Description>`
* `@argument` `{type} name <Parameter Description>`
* `@arg` `{type}` `name <Parameter Description>`.
  `{type}` representa el tipo de parámetro.  Los tipos de parámetros permitidos son:
   * string: Representa un solo valor de cadena.
   * number: representa un solo valor numérico.
   * boolean: Representa un solo valor booleano (true o false).
   * cadena[]: Representa una matriz de valores de cadena.
   * número[]: representa una matriz de valores numéricos.
   * booleano[]: Representa una matriz de valores booleanos.
   * date: representa un solo valor de fecha.
   * fecha[]: representa una matriz de valores de fecha.
   * array: representa una matriz genérica que contiene valores de varios tipos.
   * object: representa un objeto de formulario pasado a una función personalizada en lugar de pasar su valor directamente.
   * ámbito: representa el objeto global, que contiene variables de solo lectura como instancias de formulario, instancias de campo de destino y métodos para realizar modificaciones de formulario dentro de funciones personalizadas. Se declara como el último parámetro en anotaciones de JavaScript y no es visible en el editor de reglas de un formulario adaptable. El parámetro scope accede al objeto del formulario o componente para almacenar en déclencheur la regla o el evento necesarios para el procesamiento del formulario. Para obtener más información sobre el objeto Globals y cómo utilizarlo, [haga clic aquí](/help/forms/create-and-use-custom-functions.md#support-field-and-global-objects).

El tipo de parámetro no distingue entre mayúsculas y minúsculas y no se permiten espacios en el nombre del parámetro.

`<Parameter Description>` contiene detalles sobre el propósito del parámetro. Puede tener varias palabras.

**Parámetros opcionales**
De forma predeterminada, todos los parámetros son obligatorios. Puede definir un parámetro como opcional añadiendo `=` después del tipo de parámetro o de incluir el nombre del parámetro en  `[]`. Los parámetros definidos como opcionales en anotaciones de JavaScript se muestran como opcionales en el editor de reglas.
Para definir una variable como parámetro opcional, puede utilizar cualquiera de las siguientes sintaxis:

* `@param {type=} Input1`

En la línea de código anterior, `Input1` es un parámetro opcional sin ningún valor predeterminado. Para declarar un parámetro opcional con el valor predeterminado:
`@param {string=<value>} input1`

`input1` como parámetro opcional con el valor predeterminado establecido en `value`.

* `@param {type} [Input1]`

En la línea de código anterior, `Input1` es un parámetro opcional sin ningún valor predeterminado. Para declarar un parámetro opcional con el valor predeterminado:
`@param {array} [input1=<value>]`
`input1` es un parámetro opcional de tipo matriz con el valor predeterminado establecido en `value`.
Asegúrese de que el tipo de parámetro esté entre llaves {} y el nombre del parámetro se escribe entre corchetes [].

Considere el siguiente fragmento de código, donde input2 se define como un parámetro opcional:

```javascript
        /**
         * optional parameter function
         * @name OptionalParameterFunction
         * @param {string} input1 
         * @param {string=} input2 
         * @return {string}
        */
        function OptionalParameterFunction(input1, input2) {
        let result = "Result: ";
        result += input1;
        if (input2 !== null) {
            result += " " + input2;
        }
        return result;
        }
```

La siguiente ilustración muestra el uso de la variable `OptionalParameterFunction` función personalizada en el editor de reglas:

![Parámetros opcionales o requeridos ](/help/forms/assets/optional-default-params.png)

Puede guardar la regla sin especificar un valor para los parámetros necesarios, pero la regla no se ejecuta y muestra un mensaje de advertencia como:

![advertencia de regla incompleta](/help/forms/assets/incomplete-rule.png)

Cuando el usuario deja vacío el parámetro opcional, el valor &quot;Undefined&quot; se pasa a la función personalizada para el parámetro opcional.

Para obtener más información sobre cómo definir parámetros opcionales en JSDocs, [haga clic aquí](https://jsdoc.app/tags-param).

#### Tipo de devolución

El tipo de valor devuelto especifica el tipo de valor que la función personalizada devuelve después de la ejecución. Las siguientes sintaxis se utilizan para definir un tipo de valor devuelto en una función personalizada:

* `@return {type}`
* `@returns {type}`
  `{type}` representa el tipo devuelto de la función. Los tipos de valor devuelto permitidos son:
   * string: Representa un solo valor de cadena.
   * number: representa un solo valor numérico.
   * boolean: Representa un solo valor booleano (true o false).
   * cadena[]: Representa una matriz de valores de cadena.
   * número[]: representa una matriz de valores numéricos.
   * booleano[]: Representa una matriz de valores booleanos.
   * date: representa un solo valor de fecha.
   * fecha[]: representa una matriz de valores de fecha.
   * array: representa una matriz genérica que contiene valores de varios tipos.
   * object: representa el objeto de formulario en lugar de su valor directamente.

  El tipo de valor devuelto no distingue entre mayúsculas y minúsculas.

#### Privado

La función personalizada, declarada como privada, no aparece en la lista de funciones personalizadas del editor de reglas de un formulario adaptable. De forma predeterminada, las funciones personalizadas son públicas. La sintaxis para declarar la función personalizada como privada es `@private`.


## Directrices al crear funciones personalizadas {#considerations}

Para enumerar las funciones personalizadas en el editor de reglas, puede utilizar cualquiera de los siguientes formatos:

* **Instrucción de función con o sin comentarios jsdoc**

Puede crear una función personalizada con o sin comentarios jsdoc.

```javascript
    function functionName(parameters) 
        {
            // code to be executed
        }
```
Si el usuario no agrega anotaciones JavaScript a la función personalizada, aparece en el editor de reglas por su nombre de función. Sin embargo, se recomienda incluir anotaciones de JavaScript para mejorar la legibilidad de las funciones personalizadas.

* **Función de flecha con anotaciones o comentarios JavaScript obligatorios**

Puede crear una función personalizada con una sintaxis de función de flecha:

```javascript
    /**
    * test function
    * @name testFunction 
    * @param {string} a parameter description
    * @param {string=} b parameter description
    * @return {string}
    */
    testFunction = (a, b) => {
    return a + b;
    };
    /** */
    testFunction1=(a) => (return a)
    /** */
    testFunction2 = a => a + 100;
    
```

Si el usuario no agrega anotaciones JavaScript a la función personalizada, esta no aparece en la lista del editor de reglas de un formulario adaptable.

* **Expresión de función con anotaciones o comentarios JavaScript obligatorios**

Para enumerar funciones personalizadas en el editor de reglas de un formulario adaptable, cree funciones personalizadas en el siguiente formato:

```javascript
    /**
    * test function
    * @name testFunction 
    * @param {string} input1 parameter description
    * @param {string=} input2 parameter description
    * @return {string}
    */
    testFunction = function(input1,input2)
        {
            // code to be executed
        }
```

Si el usuario no agrega anotaciones JavaScript a la función personalizada, esta no aparece en la lista del editor de reglas de un formulario adaptable.

## Creación de una función personalizada {#create-custom-function}

Cree una biblioteca de cliente para llamar a funciones personalizadas en el editor de reglas. Para obtener más información, consulte [Uso de bibliotecas del lado del cliente](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/full-stack/clientlibs.html?lang=es#developing).

Los pasos para crear funciones personalizadas son los siguientes:
1. [Crear una biblioteca de cliente](#create-client-library)
1. [Agregar una biblioteca de cliente a un formulario adaptable](#use-custom-function)

### Crear una biblioteca de cliente {#create-client-library}

Puede agregar funciones personalizadas agregando la biblioteca de cliente. Para crear una biblioteca de cliente, realice los siguientes pasos:

1. [Clone su repositorio de AEM Forms as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html?lang=es#accessing-git).
1. Crear una carpeta dentro de la carpeta `[AEM Forms as a Cloud Service repository folder]/apps/`. Por ejemplo, cree una carpeta denominada como `experience-league`.
1. Vaya a `[AEM Forms as a Cloud Service repository folder]/apps/[AEM Project Folder]/experience-league/` y cree un `ClientLibraryFolder`. Por ejemplo, cree una carpeta de biblioteca de cliente como `customclientlibs`.
1. Añadir una propiedad `categories` con valor de tipo cadena. Por ejemplo, asigne el valor `customfunctionscategory` a la `categories` propiedad para `customclientlibs` carpeta.

   >[!NOTE]
   >
   > Puede elegir cualquier nombre para `client library folder` y `categories` propiedad.

1. Cree una carpeta con el nombre `js`.
1. Navegue hasta la carpeta `[AEM Forms as a Cloud Service repository folder]/apps/[AEM Project Folder]/customclientlibs/js`. 
1. Añada un archivo JavaScript, por ejemplo `function.js`.  El archivo contiene el código de la función personalizada.
1. Guarde el archivo `function.js`.
1. Navegue hasta la carpeta `[AEM Forms as a Cloud Service repository folder]/apps/[AEM Project Folder]/customclientlibs/js`. 
1. Añada un archivo de texto como `js.txt`. El archivo contiene lo siguiente:

   ```javascript
       #base=js
       functions.js
   ```

1. Guarde el archivo `js.txt`.
1. Añada, confirme e inserte los cambios en el repositorio mediante los siguientes comandos:

   ```javascript
       git add .
       git commit -a -m "Adding custom functions"
       git push
   ```

1. [Ejecutar la canalización](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html?lang=es#setup-pipeline) para implementar la función personalizada.

Una vez que la canalización se ejecute correctamente, la función personalizada agregada en la biblioteca de cliente estará disponible en su [Editor de reglas de formulario adaptable](/help/forms/rule-editor-core-components.md).

### Agregar una biblioteca de cliente a un formulario adaptable{#use-custom-function}

Una vez que haya implementado la biblioteca de cliente en el entorno de Forms CS, utilice sus funcionalidades en el formulario adaptable. Para agregar la biblioteca de cliente en el formulario adaptable

1. Abra el formulario en modo de edición. Para abrir un formulario en modo de edición, seleccione un formulario y seleccione **[!UICONTROL Editar]**.
1. Abra el Explorador de contenido y seleccione el componente **[!UICONTROL Contenedor de guía]** del formulario adaptable.
1. Haga clic en el icono de propiedades del contenedor de guía ![Propiedades de guía](/help/forms/assets/configure-icon.svg). Se abre el cuadro de diálogo Contenedor de formulario adaptable.
1. Abra el **[!UICONTROL Básico]** y seleccione el nombre de la **[!UICONTROL categoría de biblioteca de cliente]** en la lista desplegable (en este caso, seleccione `customfunctionscategory`).

   ![Agregar la biblioteca de cliente de funciones personalizada](/help/forms/assets/clientlib-custom-function.png)

   >[!NOTE]
   >
   > Se pueden agregar varias categorías especificando una lista separada por comas dentro de **[!UICONTROL Categoría de biblioteca de cliente]** field.

1. Haga clic en **[!UICONTROL Listo]**.

Puede utilizar la función personalizada en la variable [Editor de reglas de un formulario adaptable](/help/forms/rule-editor-core-components.md) uso del [Anotaciones de JavaScript](##js-annotations).

## Usar una función personalizada en un formulario adaptable

En un formulario adaptable, puede utilizar [funciones personalizadas dentro del editor de reglas](/help/forms/rule-editor-core-components.md). Agregue el siguiente código al archivo JavaScript (`Function.js` file) para calcular la edad en función de la fecha de nacimiento (AAAA-MM-DD). Crear una función personalizada como `calculateAge()` que toma la fecha de nacimiento como entrada y devuelve la edad:

```javascript
    /**
        * Calculates Age
        * @name calculateAge
        * @param {object} field
        * @return {string} 
    */

    function calculateAge(field) {
    var dob = new Date(field);
    var now = new Date();

    var age = now.getFullYear() - dob.getFullYear();
    var monthDiff = now.getMonth() - dob.getMonth();

    if (monthDiff < 0 || (monthDiff === 0 && now.getDate() < dob.getDate())) {
    age--;
    }

    return age;
    }
```

En el ejemplo anterior, cuando el usuario introduce la fecha de nacimiento en el formato (AAAA-MM-DD), la función personalizada `calculateAge` se invoca y devuelve la página.

![Función personalizada Calcular edad en el editor de reglas](/help/forms/assets/custom-function-calculate-age.png)

Vamos a previsualizar el formulario para observar cómo se implementan las funciones personalizadas a través del editor de reglas:

![Función personalizada Calcular edad en el editor de reglas de vista previa de formularios](/help/forms/assets/custom-function-age-calculate-form.png)

>[!NOTE]
>
> Puede hacer referencia a lo siguiente [función personalizada](/help/forms/assets//customfunctions.zip) carpeta. AEM Descargue e instale esta carpeta en su instancia de mediante el [Administrador de paquetes](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/developer-tools/package-manager).

### Compatibilidad con funciones asincrónicas en funciones personalizadas {#support-of-async-functions}

Las funciones personalizadas asincrónicas no aparecen en la lista del editor de reglas. Sin embargo, es posible invocar funciones asincrónicas dentro de funciones personalizadas creadas mediante expresiones de función sincrónicas.

![Función personalizada Sincronizar y asincrónica](/help/forms/assets/workflow-for-sync-async-custom-fumction.png)

>[!NOTE]
>
> La ventaja de llamar a funciones asincrónicas en funciones personalizadas es que las funciones asincrónicas permiten la ejecución simultánea de varias tareas, con el resultado de cada función utilizada dentro de las funciones personalizadas.

Consulte el siguiente código para ver cómo se pueden invocar funciones asincrónicas mediante funciones personalizadas:

```javascript
    
    async function asyncFunction() {
    const response = await fetch('https://petstore.swagger.io/v2/store/inventory');
    const data = await response.json();
    return data;
    }

    /**
    * callAsyncFunction
    * @name callAsyncFunction callAsyncFunction
    */
    function callAsyncFunction() {
    asyncFunction()
        .then(responseData => {
        console.log('Response data:', responseData);
        })
        .catch(error => {
         console.error('Error:', error);
    });
}
```

En el ejemplo anterior, la función asyncFunction es un `asynchronous function`. Realiza una operación asincrónica realizando una `GET` solicitud a `https://petstore.swagger.io/v2/store/inventory`. Espera la respuesta utilizando `await`, analiza el cuerpo de la respuesta como JSON utilizando `response.json()`y, a continuación, devuelve los datos. El `callAsyncFunction` es una función personalizada sincrónica que invoca el método `asyncFunction` y muestra los datos de respuesta en la consola. Aunque la variable `callAsyncFunction` es sincrónica, llama a la función asyncFunction asincrónica y controla su resultado con `then` y `catch` extractos.

Para ver cómo funciona, vamos a agregar un botón y crear una regla para el botón que invoca la función asincrónica al hacer clic en un botón.

![crear una regla para una función asincrónica](/help/forms/assets/rule-for-async-funct.png)

Consulte la ilustración de la ventana de la consola siguiente para demostrar que cuando el usuario hace clic en el botón `Fetch` botón, la función personalizada `callAsyncFunction` se invoca a, que a su vez llama a una función asincrónica `asyncFunction`. Inspect utiliza la ventana de la consola para ver la respuesta tras hacer clic en el botón:

![Ventana de consola](/help/forms/assets/async-custom-funct-console.png)

Vamos a profundizar en las funciones personalizadas.

## Varias funciones para funciones personalizadas

Puede utilizar funciones personalizadas para agregar características personalizadas a los formularios. Estas funciones admiten varias capacidades, como trabajar con campos específicos, utilizar campos globales o almacenar en caché. Esta flexibilidad le permite personalizar formularios según los requisitos de su organización.

### Objetos Field y Global scope en funciones personalizadas {#support-field-and-global-objects}

Objetos de campo hace referencia a los componentes o elementos individuales de un formulario, como campos de texto o casillas de verificación. El objeto Globals contiene variables de solo lectura como la instancia de formulario, la instancia del campo de destino y los métodos para realizar modificaciones de formulario dentro de funciones personalizadas.

>[!NOTE]
>
> El `param {scope} globals` debe ser el último parámetro y no se mostrará en el editor de reglas de un formulario adaptable.

<!-- Let us look at the following code snippet:

```JavaScript
   
    /**
    * updateDateTime
    * @name updateDateTime
    * @param {object} field
    * @param {scope} globals
    */
    function updateDateTime(field, globals) {
    // Accessing the Date object from the global scope
    var currentDate = new Date();
    // Formatting the date and time
    var formattedDateTime = currentDate.toLocaleString();
    // Updating the field value with the formatted date and time using setProperty.
    globals.functions.setProperty(field, {value: formattedDateTime});
    }
```

In the above code snippet, a custom function named `updateDateTime` takes parameters such as a field object and a global object. The field represents the textbox object where the formatted date and time value is displayed within the form. -->

Vamos a aprender cómo las funciones personalizadas utilizan los objetos globales y de campo con la ayuda de un `Contact Us` mediante diferentes casos de uso.

![Formulario de contacto](/help/forms/assets/contact-us-form.png)

#### **Caso de uso**: mostrar un panel con `SetProperty` regla

Agregue el siguiente código en la función personalizada como se explica en la [create-custom-function](#create-custom-function) , para establecer el campo de formulario como `Required`.

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
> * Modificaciones realizadas en el formulario mediante `setProperty` del objeto Globals son de naturaleza asincrónica y no se reflejan durante la ejecución de la función personalizada.

En este ejemplo, la validación del `personaldetails` Este panel aparece al hacer clic en el botón. Si no se detectan errores en el panel, en otro panel, en el `feedback` , se vuelve visible al hacer clic en el botón.

Vamos a crear una regla para el `Next` , que valida el `personaldetails` y crea el `feedback`  panel visible cuando el usuario hace clic en `Next` botón.

![Set Property](/help/forms/assets/custom-function-set-property.png)

Consulte la siguiente ilustración para demostrar dónde se encuentra el `personaldetails` El panel se valida al hacer clic en `Next` botón. En caso de que todos los campos dentro de `personaldetails` se validan, las variables `feedback` el panel se vuelve visible.

![Establecer vista previa de formulario de propiedad](/help/forms/assets/set-property-form-preview.png)

Si hay errores en los campos del `personaldetails` , se muestran en el nivel de campo al hacer clic en el `Next` y el botón `feedback` el panel permanece invisible.

![Establecer vista previa de formulario de propiedad](/help/forms/assets/set-property-panel.png)

#### **Caso de uso**: valide el campo.

Agregue el siguiente código en la función personalizada como se explica en la [create-custom-function](#create-custom-function) , para validar el campo.

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
> Si no se pasa ningún argumento en `validate()` función, valida el formulario.

En este ejemplo, se aplica un motivo de validación personalizado a `contact` field. Los usuarios deben introducir un número de teléfono que comience por `10` seguido de `8` dígitos. Si el usuario introduce un número de teléfono que no empieza por `10` o contiene más o menos que `8` dígitos, aparece un mensaje de error de validación al hacer clic en el botón:

![Patrón de validación de direcciones de correo electrónico](/help/forms/assets/custom-function-validation-pattern.png)

Ahora, el siguiente paso es crear una regla para `Next` que valida el `contact` en el botón, haga clic en.

![Patrón de validación](/help/forms/assets/custom-function-validate.png)

Consulte la siguiente ilustración para demostrar que si el usuario introduce un número de teléfono que no comience por `10`, aparecerá un mensaje de error en el nivel de campo:

![Patrón de validación de direcciones de correo electrónico](/help/forms/assets/custom-function-validate-error-message.png)

Si el usuario introduce un número de teléfono válido y todos los campos del `personaldetails` se validan los paneles, `feedback` el panel aparece en la pantalla:

![Patrón de validación de direcciones de correo electrónico](/help/forms/assets/validate-form-preview-form.png)

#### **Caso de uso**: restablecer un panel

Agregue el siguiente código en la función personalizada como se explica en la [create-custom-function](#create-custom-function) , para restablecer el panel.

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
> Si no se pasa ningún argumento en `reset()` función, valida el formulario.

En este ejemplo, la variable `personaldetails` el panel se restablece al hacer clic en `Clear` botón. El siguiente paso es crear una regla para `Clear` que restablece el panel al hacer clic en el botón.

![Botón Borrar](/help/forms/assets/custom-function-reset-field.png)

Consulte la siguiente ilustración para mostrar que si el usuario hace clic en `clear` botón, el `personaldetails` el panel se restablece:

![Restablecer formulario](/help/forms/assets/custom-function-reset-form.png)

#### **Caso de uso**: para mostrar un mensaje personalizado en el nivel de campo y marcar el campo como no válido

Puede usar el complemento `markFieldAsInvalid()` para definir un campo como no válido y establecer un mensaje de error personalizado en el nivel de campo. El `fieldIdentifier` el valor puede ser `fieldId`, o `field qualifiedName`, o `field dataRef`. El valor del objeto denominado `option` puede ser `{useId: true}`, `{useQualifiedName: true}`, o `{useDataRef: true}`.
Las sintaxis utilizadas para marcar el campo como no válido y establecer mensajes personalizados son:

* `globals.functions.markFieldAsInvalid(field.$id,"[custom message]",{useId: true});`
* `globals.functions.markFieldAsInvalid(field.$qualifiedName, "[custom message]", {useQualifiedName: true});`
* `globals.functions.markFieldAsInvalid(field.$dataRef, "[custom message]", {useDataRef: true});`

Agregue el siguiente código en la función personalizada como se explica en la [create-custom-function](#create-custom-function) , para habilitar el mensaje personalizado en el nivel de campo.

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

El siguiente paso es crear una regla para `comments` campo:

![Marcar campo como no válido](/help/forms/assets/custom-function-invalid-field.png)

Consulte la siguiente demostración para mostrar que al introducir comentarios negativos en la `comments` el campo déclencheur la visualización de un mensaje personalizado en el nivel de campo:

![Marcar campo como formulario de vista previa no válido](/help/forms/assets/custom-function-invalidfield-form.png)

Si el usuario introduce más de 15 caracteres en el cuadro de texto de comentarios, el campo se valida y se envía el formulario:

![Marcar campo como formulario de vista previa válido](/help/forms/assets/custom-function-validfield-form.png)


#### **Caso de uso**: enviar datos modificados al servidor

La siguiente línea de código:
`globals.functions.submitForm(globals.functions.exportData(), false);` se utiliza para enviar los datos del formulario después de su manipulación.
* El primer argumento son los datos que se van a enviar.
* El segundo argumento representa si el formulario se debe validar antes del envío. Lo es `optional` y se establece como `true` de forma predeterminada.
* El tercer argumento es el `contentType` del envío, que también es opcional con el valor predeterminado como `multipart/form-data`. Los demás valores pueden ser `application/json` y `application/x-www-form-urlencoded`.

Agregue el siguiente código en la función personalizada como se explica en la [create-custom-function](#create-custom-function) , para enviar los datos manipulados en el servidor:

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

En este ejemplo, si el usuario deja el `comments` textbox vacío, el `NA` se envía al servidor al enviar el formulario.

Ahora cree una regla para `Submit` botón que envía datos:

![Envío de datos](/help/forms/assets/custom-function-submit-data.png)

Consulte la ilustración del `console window` siguiente para demostrar que si el usuario abandona el `comments` textbox vacío, luego el valor como `NA` se envía en el servidor:

![Enviar datos en la ventana de la consola](/help/forms/assets/custom-function-submit-data-form.png)

También puede inspeccionar la ventana de la consola para ver los datos enviados al servidor:

![Datos de Inspect en la ventana de la consola](/help/forms/assets/custom-function-submit-data-console-data.png)

## Compatibilidad de almacenamiento en caché para función personalizada

Los Forms adaptables implementan el almacenamiento en caché de funciones personalizadas para mejorar el tiempo de respuesta al recuperar la lista de funciones personalizadas en el editor de reglas. Un mensaje como `Fetched following custom functions list from cache` aparece en la `error.log` archivo.

![función personalizada compatible con caché](/help/forms/assets/custom-function-cache-error.png)

En caso de que se modifiquen las funciones personalizadas, el almacenamiento en caché se invalidará y se analizará.

## Solución de problemas

Si el archivo JavaScript que contiene código para funciones personalizadas tiene un error, las funciones personalizadas no aparecen en el editor de reglas de un formulario adaptable. Para comprobar la lista de funciones personalizadas, puede desplazarse a la `error.log` archivo para el error. En caso de error, la lista de funciones personalizadas aparece vacía:

![archivo de registro de errores](/help/forms/assets/custom-function-list-error-file.png)

En caso de que no haya ningún error, las funciones personalizadas se recuperan y aparecen en la `error.log` archivo. Un mensaje como `Fetched following custom functions list` aparece en la `error.log` archivo:

![archivo de registro de errores con la función personalizada adecuada](/help/forms/assets/custom-function-list-fetched-in-error.png)

## Consideraciones

* El `parameter type` y `return type` no admiten `None`.

* Las funciones que no se admiten en la lista de funciones personalizadas son:
   * Funciones del generador
   * Funciones asíncronas/de espera
   * Definiciones de método
   * Métodos de clase
   * Parámetros predeterminados
   * Parámetros REST

## Consulte también {#see-also}

{{see-also}}


