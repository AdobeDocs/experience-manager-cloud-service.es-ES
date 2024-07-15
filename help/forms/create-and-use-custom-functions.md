---
title: Crear y agregar funciones personalizadas en un formulario adaptable
description: AEM Forms admite funciones personalizadas, que permiten a los usuarios crear y utilizar sus propias funciones dentro del editor de reglas.
keywords: Agregar una función personalizada, utilizar una función personalizada, crear una función personalizada, utilizar una función personalizada en el editor de reglas.
contentOwner: Ruchita Srivastav
content-type: reference
feature: Adaptive Forms, Core Components
exl-id: 24607dd1-2d65-480b-a831-9071e20c473d
role: User, Developer
source-git-commit: 52b87073cad84705b5dc0c6530aff44d1e686609
workflow-type: tm+mt
source-wordcount: '4333'
ht-degree: 4%

---


# Funciones personalizadas en Forms adaptable (componentes principales)

| Versión | Vínculo del artículo |
| -------- | ---------------------------- |
| AEM 6.5 | [Haga clic aquí](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/forms/adaptive-forms-core-components/create-and-use-custom-functions) |
| AEM as a Cloud Service | Este artículo |

## Introducción

AEM Forms admite funciones personalizadas, lo que permite a los usuarios definir funciones de JavaScript para implementar reglas comerciales complejas. Estas funciones personalizadas amplían las capacidades de los formularios al facilitar la manipulación y el procesamiento de los datos introducidos para satisfacer requisitos específicos. También permiten la modificación dinámica del comportamiento del formulario en función de criterios predefinidos.

>[!NOTE]
>
> Asegúrese de que el [componente principal](https://github.com/adobe/aem-core-forms-components) está establecido en la versión más reciente para utilizar las características más recientes.

### Usos de las funciones personalizadas {#uses-of-custom-function}

Las ventajas de utilizar funciones personalizadas en Forms adaptable son:
* **Procesamiento de datos**: las funciones personalizadas ayudan a procesar los datos introducidos en los campos de formulario.
* **Validación de datos**: las funciones personalizadas permiten realizar comprobaciones personalizadas en las entradas del formulario y proporcionar mensajes de error especificados.
* **Comportamiento dinámico**: las funciones personalizadas le permiten controlar el comportamiento dinámico de los formularios en función de condiciones específicas. Por ejemplo, puede mostrar u ocultar campos, modificar valores de campos o ajustar la lógica del formulario de forma dinámica.
* **Integración**: puede usar funciones personalizadas para integrarlas con API o servicios externos. Ayuda a recuperar datos de fuentes externas, enviar datos a extremos REST externos o realizar acciones personalizadas basadas en eventos externos.

Las funciones personalizadas son esencialmente bibliotecas de cliente que se agregan en el archivo JavaScript. Una vez creada una función personalizada, esta estará disponible en el editor de reglas para que la seleccione el usuario en un formulario adaptable. Las funciones personalizadas se identifican mediante las anotaciones de JavaScript en el editor de reglas.

### Anotaciones de JavaScript compatibles con funciones personalizadas {#js-annotations}

Las anotaciones de JavaScript se utilizan para proporcionar metadatos para el código de JavaScript. Incluye comentarios que comienzan con símbolos específicos, por ejemplo, /** y @. Las anotaciones proporcionan información importante sobre funciones, variables y otros elementos del código. El formulario adaptable admite las siguientes anotaciones de JavaScript para funciones personalizadas:

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
   * string[]: Representa una matriz de valores de cadena.
   * number[]: representa una matriz de valores numéricos.
   * boolean[]: Representa una matriz de valores booleanos.
   * date: representa un solo valor de fecha.
   * date[]: representa una matriz de valores de fecha.
   * array: representa una matriz genérica que contiene valores de varios tipos.
   * object: representa un objeto de formulario pasado a una función personalizada en lugar de pasar su valor directamente.
   * ámbito: representa el objeto global, que contiene variables de solo lectura como instancias de formulario, instancias de campo de destino y métodos para realizar modificaciones de formulario dentro de funciones personalizadas. Se declara como el último parámetro en las anotaciones de JavaScript y no es visible en el editor de reglas de un formulario adaptable. El parámetro scope accede al objeto del formulario o componente para almacenar en déclencheur la regla o el evento necesarios para el procesamiento del formulario. Para obtener más información sobre el objeto Globals y cómo utilizarlo, [haga clic aquí](/help/forms/create-and-use-custom-functions.md#support-field-and-global-objects).

El tipo de parámetro no distingue entre mayúsculas y minúsculas y no se permiten espacios en el nombre del parámetro.

`<Parameter Description>` contiene detalles sobre el propósito del parámetro. Puede tener varias palabras.

**Parámetros opcionales**
De forma predeterminada, todos los parámetros son obligatorios. Puede definir un parámetro como opcional agregando `=` después del tipo de parámetro o incluyendo el nombre del parámetro en `[]`. Los parámetros definidos como opcionales en las anotaciones de JavaScript se muestran como opcionales en el editor de reglas.
Para definir una variable como parámetro opcional, puede utilizar cualquiera de las siguientes sintaxis:

* `@param {type=} Input1`

En la línea de código anterior, `Input1` es un parámetro opcional sin ningún valor predeterminado. Para declarar un parámetro opcional con el valor predeterminado:
`@param {string=<value>} input1`

`input1` como parámetro opcional con el valor predeterminado establecido en `value`.

* `@param {type} [Input1]`

En la línea de código anterior, `Input1` es un parámetro opcional sin ningún valor predeterminado. Para declarar un parámetro opcional con el valor predeterminado:
`@param {array} [input1=<value>]`
`input1` es un parámetro opcional de tipo matriz con el valor predeterminado establecido en `value`.
Asegúrese de que el tipo de parámetro está entre llaves {} y el nombre del parámetro está entre corchetes.

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

La siguiente ilustración muestra el uso de la función personalizada `OptionalParameterFunction` en el editor de reglas:

![Parámetros opcionales o requeridos ](/help/forms/assets/optional-default-params.png)

Puede guardar la regla sin especificar un valor para los parámetros necesarios, pero la regla no se ejecuta y muestra un mensaje de advertencia como:

![advertencia de regla incompleta](/help/forms/assets/incomplete-rule.png)

Cuando el usuario deja vacío el parámetro opcional, el valor &quot;Undefined&quot; se pasa a la función personalizada para el parámetro opcional.

Para obtener más información acerca de cómo definir parámetros opcionales en JSDocs, [haga clic aquí](https://jsdoc.app/tags-param).

#### Tipo de devolución

El tipo de valor devuelto especifica el tipo de valor que la función personalizada devuelve después de la ejecución. Las siguientes sintaxis se utilizan para definir un tipo de valor devuelto en una función personalizada:

* `@return {type}`
* `@returns {type}`
  `{type}` representa el tipo devuelto de la función. Los tipos de valor devuelto permitidos son:
   * string: Representa un solo valor de cadena.
   * number: representa un solo valor numérico.
   * boolean: Representa un solo valor booleano (true o false).
   * string[]: Representa una matriz de valores de cadena.
   * number[]: representa una matriz de valores numéricos.
   * boolean[]: Representa una matriz de valores booleanos.
   * date: representa un solo valor de fecha.
   * date[]: representa una matriz de valores de fecha.
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
Si el usuario no agrega ninguna anotación de JavaScript a la función personalizada, se muestra en el editor de reglas por su nombre de función. Sin embargo, se recomienda incluir anotaciones de JavaScript para mejorar la legibilidad de las funciones personalizadas.

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

Si el usuario no agrega ninguna anotación de JavaScript a la función personalizada, la función personalizada no aparece en la lista del editor de reglas de un formulario adaptable.

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

Si el usuario no agrega ninguna anotación de JavaScript a la función personalizada, la función personalizada no aparece en la lista del editor de reglas de un formulario adaptable.

## Creación de una función personalizada {#create-custom-function}

Cree una biblioteca de cliente para llamar a funciones personalizadas en el editor de reglas. Para obtener más información, consulte [Uso de bibliotecas del lado del cliente](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/full-stack/clientlibs.html?lang=es#developing).

Los pasos para crear funciones personalizadas son los siguientes:
1. [Crear una biblioteca de cliente](#create-client-library)
1. [Agregar una biblioteca de cliente a un formulario adaptable](#use-custom-function)


### Requisitos previos para crear una función personalizada

Antes de empezar a agregar una función personalizada a su Forms adaptable, asegúrese de que dispone de lo siguiente:

**Software:**

* **Editor de texto sin formato (IDE)**: Aunque cualquier editor de texto sin formato puede funcionar, un entorno de desarrollo integrado (IDE) como Microsoft Visual Studio Code ofrece características avanzadas para facilitar la edición.

* **Git:** Este sistema de control de versiones es necesario para administrar cambios de código. Si no lo tiene instalado, descárguelo de https://git-scm.com.

### Crear una biblioteca de cliente {#create-client-library}

Puede agregar funciones personalizadas agregando una biblioteca de cliente. Para crear una biblioteca de cliente, realice los siguientes pasos:

**Clonar el repositorio**

Clonar su [repositorio as a Cloud Service de AEM Forms](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html?lang=es#accessing-git):

1. Abra la línea de comandos o la ventana de terminal.

1. Vaya a la ubicación deseada en el equipo donde desee almacenar el repositorio.

1. Ejecute el siguiente comando para clonar el repositorio:

   `git clone [Git Repository URL]`

Este comando descarga el repositorio y crea una carpeta local del repositorio clonado en el equipo. En esta guía, nos referimos a esta carpeta como el [directorio del proyecto AEMaaCS].

**Agregar una carpeta de biblioteca de cliente**

Para agregar una nueva carpeta de biblioteca de cliente al [directorio del proyecto AEMaaCS], siga estos pasos:

1. Abra [el directorio del proyecto AEMaaCS] en un editor.

   ![estructura de carpetas de funciones personalizadas](/help/forms/assets/custom-library-folder-structure.png)

1. Busque `ui.apps`.
1. Añada una carpeta nueva. Por ejemplo, agregue una carpeta denominada como `experience-league`.
1. Vaya a la carpeta `/experience-league/` y agregue un(a) `ClientLibraryFolder`. Por ejemplo, cree una carpeta de biblioteca de cliente llamada `customclientlibs`.

   `Location is: [AEMaaCS project directory]/ui.apps/src/main/content/jcr_root/apps/`

**Agregar archivos y carpetas a la carpeta Biblioteca de cliente**

Agregue lo siguiente a la carpeta de biblioteca de cliente agregada:

* archivo .content.xml
* archivo js.txt
* carpeta js

`Location is: [AEMaaCS project directory]/ui.apps/src/main/content/jcr_root/apps/experience-league/customclientlibs/`

1. En `.content.xml`, agregue las siguientes líneas de código:

   ```javascript
   <?xml version="1.0" encoding="UTF-8"?>
   <jcr:root xmlns:cq="http://www.day.com/jcr/cq/1.0" xmlns:jcr="http://www.jcp.org/jcr/1.0"
   jcr:primaryType="cq:ClientLibraryFolder"
   categories="[customfunctionscategory]"/>
   ```

   >[!NOTE]
   >
   > Puede elegir cualquier nombre para la propiedad `client library folder` y `categories`.

1. En `js.txt`, agregue las siguientes líneas de código:

   ```javascript
         #base=js
       function.js
   ```
1. En la carpeta `js`, agregue el archivo javascript como `function.js`, que incluye las funciones personalizadas:

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
1. Guarde los archivos.

![estructura de carpetas de funciones personalizadas](/help/forms/assets/custom-function-added-files.png)

**Incluir la nueva carpeta en filter.xml**:

1. Vaya al archivo `/ui.apps/src/main/content/META-INF/vault/filter.xml` en su [directorio del proyecto AEMaaCS].

1. Abra el archivo y añada la siguiente línea al final:

   `<filter root="/apps/experience-league" />`
1. Guarde el archivo.

![xml de filtro de función personalizada](/help/forms/assets/custom-function-filterxml.png)

AEM **Implemente la carpeta Client library recién creada en su entorno** de la biblioteca de cliente

Implemente AEM as a Cloud Service, [directorio del proyecto AEMaaCS], en su entorno de Cloud Service. Para implementarlo en el entorno de Cloud Service:

1. Confirme los cambios

   1. Añada, confirme e inserte los cambios en el repositorio mediante los siguientes comandos:

   ```javascript
       git add .
       git commit -a -m "Adding custom functions"
       git push
   ```

1. Implemente el código actualizado:

   1. Almacene en déclencheur una implementación del código a través de la canalización de pila completa existente. Esto crea e implementa automáticamente el código actualizado.

Si aún no ha configurado una canalización, consulte la guía sobre [cómo configurar una canalización para AEM Forms as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html?lang=es#setup-pipeline).

Una vez que la canalización se haya ejecutado correctamente, la función personalizada agregada en la biblioteca de cliente estará disponible en el [editor de reglas de formularios adaptables](/help/forms/rule-editor-core-components.md).

### Agregar una biblioteca de cliente a un formulario adaptable{#use-custom-function}

Una vez que haya implementado la biblioteca de cliente en el entorno de Forms CS, utilice sus funcionalidades en el formulario adaptable. Para agregar la biblioteca de cliente en el formulario adaptable

1. Abra el formulario en modo de edición. Para abrir un formulario en modo de edición, seleccione un formulario y seleccione **[!UICONTROL Editar]**.
1. Abra el Explorador de contenido y seleccione el componente **[!UICONTROL Contenedor de guía]** del formulario adaptable.
1. Haga clic en el icono de propiedades del contenedor de guía ![Propiedades de guía](/help/forms/assets/configure-icon.svg). Se abre el cuadro de diálogo Contenedor de formulario adaptable.
1. Abra la ficha **[!UICONTROL Básico]** y seleccione el nombre de la **[!UICONTROL categoría de biblioteca de cliente]** en la lista desplegable (en este caso, seleccione `customfunctionscategory`).

   ![Agregar la biblioteca de cliente de funciones personalizada](/help/forms/assets/clientlib-custom-function.png)

   >[!NOTE]
   >
   > Se pueden agregar varias categorías especificando una lista separada por comas dentro del campo **[!UICONTROL Categoría de biblioteca de cliente]**.

1. Haga clic en **[!UICONTROL Listo]**.

Puede usar la función personalizada en el [editor de reglas de un formulario adaptable](/help/forms/rule-editor-core-components.md) mediante las [anotaciones de JavaScript](##js-annotations).

## Usar una función personalizada en un formulario adaptable

En un formulario adaptable, puede usar [funciones personalizadas dentro del editor de reglas](/help/forms/rule-editor-core-components.md). Agregue el siguiente código al archivo JavaScript (archivo `Function.js`) para calcular la edad en función de la fecha de nacimiento (DD-MM-AAAA). Cree una función personalizada como `calculateAge()` que tome la fecha de nacimiento como entrada y devuelva la edad:

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

En el ejemplo anterior, cuando el usuario introduce la fecha de nacimiento con el formato (AAAA-MM-DD), se invoca la función personalizada `calculateAge` y se devuelve la edad.

![Calcular función personalizada Agae en el editor de reglas](/help/forms/assets/custom-function-calculate-age.png)

Vamos a previsualizar el formulario para observar cómo se implementan las funciones personalizadas a través del editor de reglas:

![Calcular función personalizada Agae en la vista previa de formulario del Editor de reglas](/help/forms/assets/custom-function-age-calculate-form.png)

>[!NOTE]
>
> Puede hacer referencia a la carpeta [función personalizada](/help/forms/assets//customfunctions.zip) siguiente. AEM Descargue e instale esta carpeta en su instancia de mediante el [Administrador de paquetes](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/developer-tools/package-manager).


### Establecer las opciones de la lista desplegable mediante funciones personalizadas

El editor de reglas de los componentes principales no admite la propiedad **Set Options of** para establecer las opciones de la lista desplegable durante la ejecución. Sin embargo, puede establecer las opciones de la lista desplegable mediante funciones personalizadas.

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

En el código anterior, `setEnums` se usa para establecer la propiedad `enum` y `setEnumNames` se usa para establecer la propiedad `enumNames` de la lista desplegable.

Vamos a crear una regla para el botón `Next`, que establece la opción de valor de la lista desplegable cuando el usuario haga clic en el botón `Next`:

![Opciones de lista desplegable](/help/forms/assets/drop-down-list-options.png)

Consulte la siguiente ilustración para demostrar dónde están configuradas las opciones de la lista desplegable al hacer clic en el botón Mostrar:

![Opciones desplegables en el editor de reglas](/help/forms/assets/drop-down-option-rule-editor.png)



### Compatibilidad con funciones asincrónicas en funciones personalizadas {#support-of-async-functions}

Las funciones personalizadas asincrónicas no aparecen en la lista del editor de reglas. Sin embargo, es posible invocar funciones asincrónicas dentro de funciones personalizadas creadas mediante expresiones de función sincrónicas.

![Función personalizada sincrónica y asincrónica](/help/forms/assets/workflow-for-sync-async-custom-fumction.png)

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

En el ejemplo anterior, la función asyncFunction es un `asynchronous function`. Realiza una operación asincrónica realizando una solicitud `GET` a `https://petstore.swagger.io/v2/store/inventory`. Espera la respuesta con `await`, analiza el cuerpo de la respuesta como JSON con `response.json()` y, a continuación, devuelve los datos. La función `callAsyncFunction` es una función sincrónica personalizada que invoca la función `asyncFunction` y muestra los datos de respuesta en la consola. Aunque la función `callAsyncFunction` es sincrónica, llama a la función asyncFunction asincrónica y controla su resultado con instrucciones `then` y `catch`.

Para ver cómo funciona, vamos a agregar un botón y crear una regla para el botón que invoca la función asincrónica al hacer clic en un botón.

![creando regla para la función asincrónica](/help/forms/assets/rule-for-async-funct.png)

Consulte la ilustración de la ventana de la consola siguiente para demostrar que cuando el usuario hace clic en el botón `Fetch`, se invoca la función personalizada `callAsyncFunction`, que a su vez llama a una función asincrónica `asyncFunction`. Inspect abre la ventana de la consola para ver la respuesta al botón y hacer clic en:

![Ventana de consola](/help/forms/assets/async-custom-funct-console.png)

Vamos a profundizar en las funciones personalizadas.

## Varias funciones para funciones personalizadas

Puede utilizar funciones personalizadas para agregar características personalizadas a los formularios. Estas funciones admiten varias capacidades, como trabajar con campos específicos, utilizar campos globales o almacenar en caché. Esta flexibilidad le permite personalizar formularios según los requisitos de su organización.

### Objetos Field y Global scope en funciones personalizadas {#support-field-and-global-objects}

Los objetos de campo hacen referencia a los componentes o elementos individuales de un formulario, como campos de texto o casillas de verificación. El objeto Globals contiene variables de solo lectura como la instancia de formulario, la instancia del campo de destino y los métodos para realizar modificaciones de formulario dentro de funciones personalizadas.

>[!NOTE]
>
> `param {scope} globals` debe ser el último parámetro y no se mostrará en el editor de reglas de un formulario adaptable.

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

Vamos a aprender cómo las funciones personalizadas utilizan los objetos globales y de campo con la ayuda de un formulario `Contact Us` que utiliza diferentes casos de uso.

![Formulario de contacto](/help/forms/assets/contact-us-form.png)

+++ **Caso de uso**: mostrar un panel con la regla `SetProperty`

Agregue el siguiente código en la función personalizada como se explica en la sección [create-custom-function](#create-custom-function) para establecer el campo del formulario como `Required`.

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

+++

+++ **Caso de uso**: valide el campo.

Agregue el siguiente código en la función personalizada como se explica en la sección [create-custom-function](#create-custom-function) para validar el campo.

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

+++

+++ **Caso de uso**: Restablecer un panel

Agregue el siguiente código en la función personalizada como se explica en la sección [create-custom-function](#create-custom-function) para restablecer el panel.

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

+++

+++ **Caso de uso**: para mostrar un mensaje personalizado en el nivel de campo y marcar el campo como no válido

Puede usar la función `markFieldAsInvalid()` para definir un campo como no válido y establecer un mensaje de error personalizado en el nivel de campo. El valor `fieldIdentifier` puede ser `fieldId`, `field qualifiedName` o `field dataRef`. El valor del objeto denominado `option` puede ser `{useId: true}`, `{useQualifiedName: true}` o `{useDataRef: true}`.
Las sintaxis utilizadas para marcar un campo como no válido y establecer un mensaje personalizado son:

* `globals.functions.markFieldAsInvalid(field.$id,"[custom message]",{useId: true});`
* `globals.functions.markFieldAsInvalid(field.$qualifiedName, "[custom message]", {useQualifiedName: true});`
* `globals.functions.markFieldAsInvalid(field.$dataRef, "[custom message]", {useDataRef: true});`

Agregue el siguiente código en la función personalizada como se explica en la sección [create-custom-function](#create-custom-function) para habilitar un mensaje personalizado en el nivel de campo.

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

+++

+++ **Caso de uso**: enviar datos alterados al servidor

La siguiente línea de código:
`globals.functions.submitForm(globals.functions.exportData(), false);` se usa para enviar los datos del formulario después de la manipulación.
* El primer argumento son los datos que se van a enviar.
* El segundo argumento representa si el formulario se debe validar antes del envío. Es `optional` y se establece como `true` de manera predeterminada.
* El tercer argumento es el `contentType` del envío, que también es opcional con el valor predeterminado `multipart/form-data`. Los otros valores pueden ser `application/json` y `application/x-www-form-urlencoded`.

Agregue el siguiente código en la función personalizada como se explica en la sección [create-custom-function](#create-custom-function) para enviar los datos manipulados en el servidor:

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

![Datos de Inspect en la ventana de la consola](/help/forms/assets/custom-function-submit-data-console-data.png)

+++

+++ **Caso de uso**: invalidar los controladores de éxito y error del envío del formulario

Agregue la siguiente línea de código, tal como se explica en la sección [create-custom-function](#create-custom-function), para personalizar el envío o el mensaje de error para los envíos de formularios y mostrar los mensajes de envío de formularios en un cuadro modal:

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

AEM En caso de que el controlador de envío personalizado no funcione según lo esperado en los formularios o proyectos existentes de la aplicación, consulte la sección [solución de problemas](#troubleshooting).

+++

+++ **Caso de uso**: realice acciones en una instancia específica del panel repetible

Las reglas creadas con el editor de reglas visuales en un panel repetible se aplican a la última instancia del panel repetible. Para escribir una regla para una instancia específica del panel repetible, podemos utilizar una función personalizada.

Vamos a crear otro formulario para recopilar información sobre los viajeros que se dirigen a un destino. Un panel de viajeros se agrega como un panel repetible, donde el usuario puede agregar detalles para 5 viajeros con el botón `Add Traveler`.

![Información del viajero](/help/forms/assets/traveler-info-form.png)

Agregue la siguiente línea de código como se explica en la sección [create-custom-function](#create-custom-function) para realizar acciones en una instancia específica del panel repetible que no sea la última:

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

+++

+++ **Caso de uso**: rellene previamente el campo con un valor cuando se cargue el formulario

Agregue la siguiente línea de código, tal como se explica en la sección [create-custom-function](#create-custom-function), para cargar el valor rellenado previamente en un campo cuando se inicialice el formulario:

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

+++

+++ **Caso de uso**: establezca el enfoque en el campo específico

Agregue la línea de código siguiente, tal como se explica en la sección [create-custom-function](#create-custom-function), para establecer el enfoque en el campo especificado cuando se haga clic en el botón `Submit`.:

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

+++

+++ **Caso de uso**: agregue o elimine un panel repetible con la propiedad `dispatchEvent`

Agregue la línea de código siguiente, tal como se explica en la sección [create-custom-function](#create-custom-function), para agregar un panel cuando se haga clic en el botón `Add Traveler` mediante la propiedad `dispatchEvent`:

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

+++

## Compatibilidad de almacenamiento en caché para función personalizada

Los Forms adaptables implementan el almacenamiento en caché de funciones personalizadas para mejorar el tiempo de respuesta al recuperar la lista de funciones personalizadas en el editor de reglas. Aparece un mensaje como `Fetched following custom functions list from cache` en el archivo `error.log`.

![función personalizada con compatibilidad con caché](/help/forms/assets/custom-function-cache-error.png)

En caso de que se modifiquen las funciones personalizadas, el almacenamiento en caché se invalidará y se analizará.

## Resolución de problemas {#troubleshooting}

* AEM Si el controlador de envío personalizado no funciona como se espera en los formularios o proyectos existentes de la aplicación, realice los siguientes pasos:
   * Asegúrese de que la versión de los componentes principales [se haya actualizado a la versión 3.0.18 y posteriores](https://github.com/adobe/aem-core-forms-components). AEM Sin embargo, para los proyectos y formularios existentes de, hay que seguir algunos pasos adicionales:

   * AEM Para el proyecto de, el usuario debe reemplazar todas las instancias de `submitForm('custom:submitSuccess', 'custom:submitError')` por `submitForm()` e implementar el proyecto a través de la canalización de Cloud Manager.

   * En el caso de los formularios existentes, si los controladores de envío personalizados no funcionan correctamente, el usuario debe abrir y guardar la regla `submitForm` en el botón **Enviar** mediante el Editor de reglas. Esta acción reemplaza la regla existente de `submitForm('custom:submitSuccess', 'custom:submitError')` por `submitForm()` en el formulario.


* Si el archivo JavaScript que contiene código para funciones personalizadas tiene un error, las funciones personalizadas no aparecen en el editor de reglas de un formulario adaptable. Para comprobar la lista de funciones personalizadas, puede desplazarse al archivo `error.log` en busca del error. En caso de error, la lista de funciones personalizadas aparece vacía:

  ![archivo de registro de errores](/help/forms/assets/custom-function-list-error-file.png)

  En caso de que no haya ningún error, las funciones personalizadas se recuperan y aparecen en el archivo `error.log`. Aparece un mensaje como `Fetched following custom functions list` en el archivo `error.log`:

  ![archivo de registro de errores con la función personalizada adecuada](/help/forms/assets/custom-function-list-fetched-in-error.png)

## Consideraciones

* `parameter type` y `return type` no admiten `None`.

* Las funciones que no se admiten en la lista de funciones personalizadas son:
   * Funciones del generador
   * Funciones asíncronas/de espera
   * Definiciones de método
   * Métodos de clase
   * Parámetros predeterminados
   * Parámetros REST

## Consulte también {#see-also}

{{see-also}}


