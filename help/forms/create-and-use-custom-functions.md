---
title: Crear y agregar funciones personalizadas en un formulario adaptable
description: AEM Forms admite funciones personalizadas, que permiten a los usuarios crear y utilizar sus propias funciones dentro del editor de reglas.
keywords: Agregar una función personalizada, utilizar una función personalizada, crear una función personalizada, utilizar una función personalizada en el editor de reglas.
contentOwner: Ruchita Srivastav
content-type: reference
feature: Adaptive Forms, Core Components
exl-id: 24607dd1-2d65-480b-a831-9071e20c473d
source-git-commit: 05b149c60cb8d05489668b13f63ed5b0e1d0bbfb
workflow-type: tm+mt
source-wordcount: '3522'
ht-degree: 4%

---


<span class="preview"> Este artículo contiene `Override form submission success and error handlers` como función previa al lanzamiento. Solo se puede acceder a la función previa al lanzamiento mediante nuestras [canal previo al lanzamiento](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/prerelease.html?lang=es#new-features).

# Funciones personalizadas en Forms adaptable (componentes principales)

| Versión | Vínculo del artículo |
| -------- | ---------------------------- |
| AEM 6.5 | [Haga clic aquí](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/forms/adaptive-forms-core-components/create-and-use-custom-functions) |
| AEM as a Cloud Service | Este artículo |

## Introducción

AEM Forms admite funciones personalizadas, lo que permite a los usuarios definir funciones de JavaScript para implementar reglas comerciales complejas. Estas funciones personalizadas amplían las capacidades de los formularios al facilitar la manipulación y el procesamiento de los datos introducidos para satisfacer requisitos específicos. También permiten la modificación dinámica del comportamiento del formulario en función de criterios predefinidos.

>[!NOTE]
>
> Asegúrese de que la variable [componente principal](https://github.com/adobe/aem-core-forms-components) se establece en la última versión para utilizar las últimas funciones.

### Usos de las funciones personalizadas {#uses-of-custom-function}

Las ventajas de utilizar funciones personalizadas en Forms adaptable son:
* **Procesamiento de datos**: Las funciones personalizadas ayudan a procesar los datos introducidos en los campos de formulario.
* **Validación de datos**: las funciones personalizadas permiten realizar comprobaciones personalizadas en las entradas del formulario y proporcionar mensajes de error especificados.
* **Comportamiento dinámico**: las funciones personalizadas le permiten controlar el comportamiento dinámico de los formularios en función de condiciones específicas. Por ejemplo, puede mostrar u ocultar campos, modificar valores de campos o ajustar la lógica del formulario de forma dinámica.
* **Integración**: Puede utilizar funciones personalizadas para integrarse con API o servicios externos. Ayuda a recuperar datos de fuentes externas, enviar datos a extremos REST externos o realizar acciones personalizadas basadas en eventos externos.

Las funciones personalizadas son esencialmente bibliotecas de cliente que se agregan en el archivo JavaScript. Una vez creada una función personalizada, esta estará disponible en el editor de reglas para que la seleccione el usuario en un formulario adaptable. Las funciones personalizadas se identifican mediante anotaciones JavaScript en el editor de reglas.

### Anotaciones JavaScript compatibles con la función personalizada {#js-annotations}

Las anotaciones de JavaScript se utilizan para proporcionar metadatos para el código JavaScript. Incluye comentarios que comienzan con símbolos específicos, por ejemplo, /** y @. Las anotaciones proporcionan información importante sobre funciones, variables y otros elementos del código. El formulario adaptable admite las siguientes anotaciones de JavaScript para funciones personalizadas:

#### Nombre

El nombre se utiliza para identificar la función personalizada en el editor de reglas de un formulario adaptable. Se utilizan las siguientes sintaxis para asignar un nombre a una función personalizada:

* `@name [functionName] <Function Name>`
* `@function [functionName] <Function Name>`
* `@func [functionName] <Function Name>`.
  `functionName` es el nombre de la función. No se permiten espacios.
  `<Function Name>` es el nombre para mostrar de la función en el editor de reglas de un formulario adaptable.
Si el nombre de la función es idéntico al nombre de la función en sí, puede omitir `[functionName]` de la sintaxis.

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


## Directrices al crear funciones personalizadas

Para enumerar las funciones personalizadas en el editor de reglas, puede utilizar cualquiera de los siguientes formatos:

### Instrucción de función con o sin comentarios jsdoc

Puede crear una función personalizada con o sin comentarios jsdoc.

```javascript
    function functionName(parameters) 
        {
            // code to be executed
        }
```
Si el usuario no agrega anotaciones JavaScript a la función personalizada, aparece en el editor de reglas por su nombre de función. Sin embargo, se recomienda incluir anotaciones de JavaScript para mejorar la legibilidad de las funciones personalizadas.

### Función de flecha con anotaciones o comentarios JavaScript obligatorios

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

### Expresión de función con anotaciones o comentarios JavaScript obligatorios

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

Puede agregar funciones personalizadas agregando una biblioteca de cliente. Para crear una biblioteca de cliente, realice los siguientes pasos:

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


### Establecer las opciones de la lista desplegable mediante funciones personalizadas

El editor de reglas de los componentes principales no admite **Configurar opciones de** para establecer las opciones de la lista desplegable durante la ejecución. Sin embargo, puede establecer las opciones de la lista desplegable mediante funciones personalizadas.

Consulte el siguiente código para ver cómo podemos establecer las opciones de la lista desplegable con funciones personalizadas:

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

En el código anterior, `setEnums` se utiliza para configurar el `enum` propiedad y `setEnumNames` se utiliza para configurar el `enumNames` propiedad del menú desplegable.

Vamos a crear una regla para el `Next` , que establece el valor de la opción de lista desplegable cuando el usuario hace clic en el botón `Next` botón:

![Opciones de la lista desplegable](/help/forms/assets/drop-down-list-options.png)

Consulte la siguiente ilustración para demostrar dónde están configuradas las opciones de la lista desplegable al hacer clic en el botón Mostrar:

![Opciones desplegables en el editor de reglas](/help/forms/assets/drop-down-option-rule-editor.png)



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

Consulte la ilustración de la ventana de la consola siguiente para demostrar que cuando el usuario hace clic en el botón `Fetch` botón, la función personalizada `callAsyncFunction` se invoca a, que a su vez llama a una función asincrónica `asyncFunction`. Inspect abre la ventana de la consola para ver la respuesta al botón y hacer clic en:

![Ventana de consola](/help/forms/assets/async-custom-funct-console.png)

Vamos a profundizar en las funciones personalizadas.

## Varias funciones para funciones personalizadas

Puede utilizar funciones personalizadas para agregar características personalizadas a los formularios. Estas funciones admiten varias capacidades, como trabajar con campos específicos, utilizar campos globales o almacenar en caché. Esta flexibilidad le permite personalizar formularios según los requisitos de su organización.

### Objetos Field y Global scope en funciones personalizadas {#support-field-and-global-objects}

Los objetos de campo hacen referencia a los componentes o elementos individuales de un formulario, como campos de texto o casillas de verificación. El objeto Globals contiene variables de solo lectura como la instancia de formulario, la instancia del campo de destino y los métodos para realizar modificaciones de formulario dentro de funciones personalizadas.

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

Vamos a aprender cómo las funciones personalizadas utilizan los objetos globales y de campo con la ayuda de un `Contact Us` Uso de diferentes casos de uso.

![Formulario de contacto](/help/forms/assets/contact-us-form.png)

#### Caso de uso: mostrar un panel con la regla SetProperty

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


#### Caso de uso: Validar el campo.

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



#### Caso de uso: Restablecer un panel

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



#### Caso de uso: para mostrar un mensaje personalizado en el nivel de campo y marcar el campo como no válido

Puede usar el complemento `markFieldAsInvalid()` para definir un campo como no válido y establecer un mensaje de error personalizado en el nivel de campo. El `fieldIdentifier` el valor puede ser `fieldId`, o `field qualifiedName`, o `field dataRef`. El valor del objeto denominado `option` puede ser `{useId: true}`, `{useQualifiedName: true}`, o `{useDataRef: true}`.
Las sintaxis utilizadas para marcar un campo como no válido y establecer un mensaje personalizado son:

* `globals.functions.markFieldAsInvalid(field.$id,"[custom message]",{useId: true});`
* `globals.functions.markFieldAsInvalid(field.$qualifiedName, "[custom message]", {useQualifiedName: true});`
* `globals.functions.markFieldAsInvalid(field.$dataRef, "[custom message]", {useDataRef: true});`

Agregue el siguiente código en la función personalizada como se explica en la [create-custom-function](#create-custom-function) , para habilitar un mensaje personalizado en el nivel de campo.

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



#### Caso de uso: Envío de datos modificados al servidor

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

Ahora, cree una regla para `Submit` botón que envía datos:

![Envío de datos](/help/forms/assets/custom-function-submit-data.png)

Consulte la ilustración del `console window` siguiente para demostrar que si el usuario abandona el `comments` textbox vacío, luego el valor como `NA` se envía en el servidor:

![Enviar datos en la ventana de la consola](/help/forms/assets/custom-function-submit-data-form.png)

También puede inspeccionar la ventana de la consola para ver los datos enviados al servidor:

![Datos de Inspect en la ventana de la consola](/help/forms/assets/custom-function-submit-data-console-data.png)



#### Caso de uso: Anular los controladores de éxito y de error del envío del formulario

Añada la siguiente línea de código como se explica en la sección [create-custom-function](#create-custom-function) , para personalizar el envío o el mensaje de error para los envíos de formularios y mostrar los mensajes de envío de formularios en un cuadro modal:

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

En este ejemplo, cuando el usuario utiliza el `customSubmitSuccessHandler` y `customSubmitErrorHandler` funciones personalizadas, los mensajes de éxito y error se muestran en un modal. La función de JavaScript `showModal(type, message)` se utiliza para crear y mostrar dinámicamente un cuadro de diálogo modal en una pantalla.

Ahora, cree una regla para el envío correcto de formularios:

![Envío del formulario correcto](/help/forms/assets/form-submission-success.png)

Consulte la siguiente ilustración para demostrar que, cuando el formulario se envía correctamente, el mensaje de éxito se muestra en un modal:

![Mensaje de éxito de envío de formulario](/help/forms/assets/form-submission-success-message.png)

Del mismo modo, vamos a crear una regla para los envíos de formularios fallidos:

![Error de envío de formulario](/help/forms/assets/form-submission-fail.png)

Consulte la siguiente ilustración para demostrar que, cuando falla el envío del formulario, el mensaje de error se muestra en un modal:

![Mensaje de error de envío de formulario](/help/forms/assets/form-submission-fail-message.png)

Para mostrar el éxito y el fracaso del envío del formulario de forma predeterminada, la variable `Default submit Form Success Handler` y `Default submit Form Error Handler` Las funciones de están disponibles de forma predeterminada.

AEM En caso de que el controlador de envío personalizado no funcione según lo esperado en los formularios o proyectos de la existentes, consulte el [solución de problemas](#troubleshooting) sección.

<!--


#### Use Case:  Perform actions in a specific instance of the repeatable panel 

Rules created using the visual rule editor on a repeatable panel apply to the last instance of the repeatable panel. To write a rule for a specific instance of the repeatable panel, we can use a custom function.

Let's create a form to collect information about travelers heading to a destination. A traveler panel is added as a repeatable panel, where the user can add details for 5 travelers using the Add button.

Add the following line of code as explained in the [create-custom-function](#create-custom-function) section, to perform actions in a specific instance of the repeatable panel, other than the last one:

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
 
In this example, the `hidePanelInRepeatablePanel` custom function performs action in a specific instance of the repeatable panel. In the above code, `travelerinfo` represents the repeatable panel. The `repeatablePanel[1].traveler, {visible: false}` code hides the panel in the second instance of the repeatable panel. 
Let us add a button labeled `Hide` to add a rule to hide a specific panel.

![Hide Panel rule](/help/forms/assets/custom-function-hidepanel-rule.png)

Refer to the video below to demonstrate that when the `Hide` is clicked, the panel in the second repeatable instance hides:




#### **Usecase**: Pre-fill the field with a value when the form loads

Add the following line of code, as explained in the [create-custom-function](#create-custom-function) section, to load the pre-filled value in a field when the form is initialized:

```javascript
/**
 * @name importData
 * @param {scope} globals
 */
function importData(globals)
{
    globals.functions.importData(Object.fromEntries([['amount',200000]]));
} 
```

In the aforementioned code, the `importData` function updates the value in the `amount` textbox field when the form loads.

Let us create a rule for the `Submit` button, where the value in the `amount` textbox field changes to specified value when the form loads:

![Import Data Rule](/help/forms/assets/custom-function-import-data.png)

Refer to the screenshot below, which demonstrates that when the form loads, the value in the amount textbox is pre-filled with a specified value:

![Import Data Rule](/help/forms/assets/cg)



#### **Usecase**: Set focus on the specific field

Add the following line of code, as explained in the [create-custom-function](#create-custom-function) section, to set focus on the specified field when the `Submit` button is clicked.:

```javascript
/**
 * @name setFocus
 * @param {object} field
 * @param {scope} globals
 */
function setFocus(field, globals)
{
    globals.functions.setFocus(field);
}
```

Let us add a rule to the `Submit` button to set focus on the `email` field when it is clicked:

![Set Focus Rule](/help/forms/assets/custom-function-set-focus.png)

Refer to the screenshot below, which demonstrates that when the `Submit` button is clicked, the focus is set on the `email` field:

![Set Focus Rule](/help/forms/assets/custom-function-set-focus-form.png)

>[!NOTE]
>
> You can use the optional `$focusOption` parameter, if you want to focus on the next or previous field relative to the `email` field.

+++

+++ **Usecase**: Add or delete repeatable panel using the `dispatchEvent` property

Add the following line of code, as explained in the [create-custom-function](#create-custom-function) section, to add a panel when the `Add Traveler` button is clicked using the `dispatchEvent` property:

```javascript
/**
 
 * @name addInstance
 * @param {scope} globals
 */
function addInstance(globals)
{
    var repeatablePanel = globals.form.traveler;
    globals.functions.dispatchEvent(repeatablePanel, 'addInstance');
} 

```

Let us add a rule to the `Add Traveler` button to add the repeatable panel when it is clicked:

![Add Panel Rule](/help/forms/assets/custom-function-add-panel.png)

Refer to the screenshot below, which demonstrates that when the `Add Traveler` button is clicked, the traveler panel is added using the `dispatchEvent` property:

![Add Panel](/help/forms/assets/customg)

Similarly, add a button labeled `Delete Traveler` to delete a panel. Add the following line of code, as explained in the [create-custom-function](#create-custom-function) section, to delete a panel when the `Delete Traveler` button is clicked using the `dispatchEvent` property:

```javascript

/**
 
 * @name removeInstance
 * @param {scope} globals
 */
function removeInstance(globals)
{
    var repeatablePanel = globals.form.traveler;
    globals.functions.dispatchEvent(repeatablePanel, 'removeInstance');
} 

```
Let us add a rule to the `Delete Traveler` button to delete the repeatable panel when it is clicked:

![Delete Panel Rule](/help/forms/assets/custom-function-delete-panel.png)

Refer to the screenshot below, which demonstrates that when the `Delete Traveler` button is clicked, the traveler panel is deleted using the `dispatchEvent` property:

![Delete Panel](/help/forms/assets/customg)
-->

## Compatibilidad de almacenamiento en caché para función personalizada

Los Forms adaptables implementan el almacenamiento en caché de funciones personalizadas para mejorar el tiempo de respuesta al recuperar la lista de funciones personalizadas en el editor de reglas. Un mensaje como `Fetched following custom functions list from cache` aparece en la `error.log` archivo.

![función personalizada compatible con caché](/help/forms/assets/custom-function-cache-error.png)

En caso de que se modifiquen las funciones personalizadas, el almacenamiento en caché se invalidará y se analizará.

## Resolución de problemas {#troubleshooting}

* AEM Si el controlador de envío personalizado no funciona como se espera en los formularios o proyectos existentes de la aplicación, realice los siguientes pasos:
   * Asegúrese de que la variable [la versión de los componentes principales se ha actualizado a la 3.0.18 y versiones posteriores](https://github.com/adobe/aem-core-forms-components). AEM Sin embargo, para los proyectos y formularios existentes de, hay que seguir algunos pasos adicionales:

   * AEM Para el proyecto de, el usuario debe reemplazar todas las instancias de `submitForm('custom:submitSuccess', 'custom:submitError')` con `submitForm()` e implementar el proyecto a través de la canalización de Cloud Manager.

   * En el caso de los formularios existentes, si los controladores de envío personalizados no funcionan correctamente, el usuario debe abrir y guardar el `submitForm` regla sobre **Enviar** mediante el Editor de reglas. Esta acción reemplaza la regla existente de `submitForm('custom:submitSuccess', 'custom:submitError')` con `submitForm()` en el formulario.


* Si el archivo JavaScript que contiene código para funciones personalizadas tiene un error, las funciones personalizadas no aparecen en el editor de reglas de un formulario adaptable. Para comprobar la lista de funciones personalizadas, puede desplazarse a la `error.log` archivo para el error. En caso de error, la lista de funciones personalizadas aparece vacía:

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

## Ver también {#see-also}

{{see-also}}


