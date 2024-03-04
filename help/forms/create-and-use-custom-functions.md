---
title: Crear y agregar funciones personalizadas en un formulario adaptable
description: AEM Forms admite funciones personalizadas que permiten a los usuarios crear y utilizar sus propias funciones dentro del editor de reglas.
keywords: Agregar una función personalizada, utilizar una función personalizada, crear una función personalizada, utilizar una función personalizada en el editor de reglas.
contentOwner: Ruchita Srivastav
content-type: reference
feature: Adaptive Forms, Core Components
source-git-commit: 46fbed98a806f62dd1882eb0085d4338c5cd51a7
workflow-type: tm+mt
source-wordcount: '1108'
ht-degree: 26%

---


# Funciones personalizadas en Forms adaptable (componentes principales)

## Introducción

AEM Forms admite funciones personalizadas, lo que permite a los usuarios definir funciones de JavaScript para implementar reglas comerciales complejas. Estas funciones personalizadas amplían las capacidades de los formularios al facilitar la manipulación y el procesamiento de los datos introducidos para satisfacer requisitos específicos. También permiten la modificación dinámica del comportamiento del formulario en función de criterios predefinidos.
En Forms adaptable, puede utilizar funciones personalizadas dentro de [Editor de reglas de un formulario adaptable](/help/forms/rule-editor-core-components.md) para crear reglas de validación específicas para los campos de formulario.

Comprendamos el uso de la función personalizada en la que los usuarios escriben la dirección de correo electrónico y desea asegurarse de que la dirección de correo electrónico introducida sigue un formato específico (contiene un símbolo &quot;@&quot; y un nombre de dominio). Cree una función personalizada como &quot;ValidateEmail&quot; que tome la dirección de correo electrónico como entrada y devuelva el valor &quot;True&quot; si es válido y el valor &quot;False&quot; en caso contrario.

```javascript
function ValidateEmail(inputText)
{
    var email = /^\w+([\.-]?\w+)*@\w+([\.-]?\w+)*(\.\w{2,3})+$/;
    if(inputText.value.match(email))
        {
            alert("Valid email address!");
            return true;
        }
    else
    {
        alert("Invalid email address!");
        return false;
    }
}
```

En el ejemplo anterior, cuando el usuario intenta enviar el formulario, se invoca la función personalizada &quot;ValidateEmail&quot; para comprobar si la dirección de correo electrónico introducida es válida.

### Usos de las funciones personalizadas {#uses-of-custom-function}

Las ventajas de utilizar funciones personalizadas en Forms adaptable son:

* **Manipulación de datos**: Las funciones personalizadas manipulan y procesan los datos introducidos en los campos de formulario.
* **Validación de datos**: las funciones personalizadas permiten realizar comprobaciones personalizadas en las entradas del formulario y proporcionar mensajes de error especificados.
* **Comportamiento dinámico**: las funciones personalizadas le permiten controlar el comportamiento dinámico de los formularios en función de condiciones específicas. Por ejemplo, puede mostrar u ocultar campos, modificar valores de campos o ajustar la lógica del formulario de forma dinámica.
* **Integración**: Puede utilizar funciones personalizadas para integrarse con API o servicios externos. Ayuda a recuperar datos de fuentes externas, enviar datos a extremos REST externos o realizar acciones personalizadas basadas en eventos externos.

## Anotaciones JS admitidas

Asegúrese de que la función personalizada que escriba esté acompañada de la variable `jsdoc` por encima de ella.

Etiquetas `jsdoc` compatibles:

* **Sintaxis**
privada: `@private`
una función privada no se incluye como función personalizada.

* **Sintaxis**
de nombre: `@name funcName <Function Name>`
O bien, `,` puede usar: `@function funcName <Function Name>` **o** `@func` `funcName <Function Name>`.
  `funcName` es el nombre de la función (no se permiten espacios).
  `<Function Name>` es el nombre para mostrar de la función.

* **Sintaxis**
de parámetro: `@param {type} name <Parameter Description>`
O bien, puede usar: `@argument` `{type} name <Parameter Description>` **o** `@arg` `{type}` `name <Parameter Description>`.
Muestra los parámetros utilizados por la función. Una función puede tener varias etiquetas de parámetro, una etiqueta para cada parámetro en el orden de ocurrencia.
  `{type}` representa el tipo de parámetro. Los tipos de parámetros permitidos son:

   1. cadena
   2. número
   3. booleano
   4. ámbito
   5. cadena[]
   6. número[]
   7. booleano[]
   8. fecha
   9. fecha[]
   10. matriz
   11. objeto

  `scope` hace referencia a un objeto especial globals proporcionado por el motor de ejecución de formularios. Debe ser el último parámetro y no debe ser visible para el usuario en el editor de reglas. Puede utilizar el ámbito para acceder a un formulario legible y a un objeto proxy de campo para leer las propiedades, el evento que activó la regla y un conjunto de funciones para manipular el formulario.

  `object` type se utiliza para pasar un objeto de campo legible en parámetro a una función personalizada en lugar de pasar el valor.

  Todos los tipos de parámetros se clasifican en una de las categorías anteriores. Ninguno no es compatible. Asegúrese de seleccionar uno de los tipos anteriores. Los tipos no distinguen entre mayúsculas y minúsculas. No se permiten espacios en el nombre del parámetro.  La descripción del parámetro puede tener varias palabras.

* **Parámetro opcional**
Sintaxis: `@param {type=} name <Parameter Description>`
Como alternativa, puede utilizar: `@param {type} [name] <Parameter Description>`
De forma predeterminada, todos los parámetros son obligatorios. Puede marcar un parámetro como opcional añadiendo `=` en el tipo del parámetro o colocando el nombre del parámetro entre corchetes.
Por ejemplo, vamos a declarar `Input1` como parámetro opcional:
   * `@param {type=} Input1`
   * `@param {type} [Input1]`

* **Sintaxis**
de tipo de retorno: `@return {type}`
O bien, puede usar `@returns {type}`.
Agrega información sobre la función, como su objetivo. 
{type} representa el tipo de valor devuelto de la función. Los tipos de valor devuelto permitidos son:

   1. cadena
   2. número
   3. booleano
   4. cadena[]
   5. número[]
   6. booleano[]
   7. fecha
   8. fecha[]
   9. matriz
   10. objeto

Todos los demás tipos de valor devuelto se clasifican en una de las categorías anteriores. Ninguno no es compatible. Asegúrese de seleccionar uno de los tipos anteriores. Los tipos de valor devuelto no distinguen entre mayúsculas y minúsculas.

## Consideraciones al crear funciones personalizadas {#considerations}

Para enumerar las funciones personalizadas en el editor de reglas, puede declararlas en cualquiera de los siguientes formatos:

* **Instrucción de función con o sin comentarios jsdoc**

Puede crear una función personalizada con o sin comentarios jsdoc.

```javascript
    function functionName(parameters) 
        {
            // code to be executed
        }
```
<!--

* **Arrow function with mandatory jsdoc comment**

Some of the examples to create Arrow functions are:
```javascript
    /**
    * test function
    * @name testFunction test function
    * @param {string} a some parameter description
    * @param {string} b another parameter description
    * @return {string}
    */
    testFunction = (a, b) => {
    return a + b;
    };
```

    * @param {string=} b another parameter description
      /** */
    testFunction1=(a) => (return a)
    /** */
    testFunction2 = a => a + 100;-->

* **Expresión de función con comentario jsdoc obligatorio**

Para enumerar funciones personalizadas en el editor de reglas de un formulario adaptable, cree funciones personalizadas en el siguiente formato:

```javascript
    /**
    * test function
    * @name testFunction test function
    * @param {string} input1 parameter description
    * @param {string} input2 another parameter description
    * @return {string}
    */
    testFunction = function(input1,input2)
        {
            // code to be executed
        }
```

<!--
* @param {string=} input2 another parameter description
The functions that are not supported in the custom function list are:
* Generator functions
* Async/Await functions 
* Method definitions
* Class methods
* Default parameters
* Rest parameters -->

>[!NOTE]
>
> Puede consultar la `error.log` para cualquier error, como funciones personalizadas que no aparecen en el editor de reglas.

<!--The `error.log` file also displays the methods and parameters that are not supported for custom functions. -->


## Creación de una función personalizada {#create-custom-function}

Cree una biblioteca de cliente para llamar a funciones personalizadas en el editor de reglas. Para obtener más información, consulte [Uso de bibliotecas del lado del cliente](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/full-stack/clientlibs.html?lang=es#developing).

Los pasos para crear funciones personalizadas son los siguientes:
1. [Crear una biblioteca de cliente](#create-client-library)
1. [Agregar una biblioteca de cliente en un formulario adaptable](#use-custom-function)

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

   >[!NOTE]
   >
   > Si el archivo JavaScript que contiene código para funciones personalizadas tiene un error, las funciones personalizadas no aparecen en el editor de reglas de un formulario adaptable. También puede consultar la `error.log` archivo para el error.

   <!-- 
    >* AEM Adaptive Form supports the caching of custom functions. If the JavaScript is modified, the caching becomes invalidated, and it is parsed. You can see a message as `Fetched following custom functions list from cache` in the `error.log` file.  -->

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

1. [Ejecutar la canalización.](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html?lang=es#setup-pipeline)

Una vez que la canalización se ejecute correctamente, la función personalizada agregada en la biblioteca de cliente estará disponible en su [Editor de reglas de formulario adaptable](/help/forms/rule-editor-core-components.md).

### Agregar una biblioteca de cliente en un formulario adaptable{#use-custom-function}

Una vez que haya implementado la biblioteca de cliente en el entorno de Forms CS, utilice sus funcionalidades en el formulario adaptable. Para agregar la biblioteca de cliente en el formulario adaptable

1. Abra el formulario en modo de edición. Para abrir un formulario en modo de edición, seleccione un formulario y seleccione **[!UICONTROL Editar]**.
1. Abra el Explorador de contenido y seleccione el componente **[!UICONTROL Contenedor de guía]** del formulario adaptable.
1. Haga clic en el icono de propiedades del contenedor de guía ![Propiedades de guía](/help/forms/assets/configure-icon.svg). Se abre el cuadro de diálogo Contenedor de formulario adaptable.
1. Abra el **[!UICONTROL Básico]** y seleccione el nombre de la **[!UICONTROL categoría de biblioteca de cliente]** en la lista desplegable (en este caso, seleccione `customfunctionscategory`).

   ![Agregar la biblioteca de cliente de funciones personalizada](/help/forms/assets/clientlib-custom-function.png)

1. Clic **[!UICONTROL Listo]** .

Ahora puede crear una regla para utilizar funciones personalizadas en el editor de reglas.

<!--

Create a rule to use custom function in the rule editor. 

### Support for the optional parameters in custom functions{#support-for-optional-parameter}

AEM supports including optional parameters in JSDocs. These parameters are displayed as optional in the rule editor. There are two ways to add optional parameters in JSDocs:
*  `@param {string=abc} b -- some description for b which is optional`

    In the above line of code, `b` is an optional parameter with the default value set to `abc`. 
    Alternatively, you can define `b` as an optional parameter without assigning any default value as `@param {string=} b -- some description for b which is optional`

* `@param {array} [z=[def,xyz]] - - some description for z which is optional`

    In the above line of code, `z` is an optional parameter of array type with the default value set to `[def , xyz]`. 
    Alternatively, you can define `z` as an optional parameter without assigning any default value as `@param {array} [z=] - - some description for z which is optional`

>[!NOTE]
>
> Ensure that the parameter name is enclosed in square brackets [] and the parameter type is enclosed in curly brackets {}. 

To learn more about how to define optional parameters in JSDocs, [click here](https://jsdoc.app/tags-param).

In the rule editor of an Adaptive Form, the parameters are displayed as `required`. By default the parameters are `required`, if not defined as optional in JSDocs.

  ![Optional or required parameters](/help/forms/assets/optional-default-params.png) 

  You can save the rule without specifying a value for required parameters, but the rule is not executed and displays a warning message as:

  ![incomplete rule warning message](/help/forms/assets/incomplete-rule.png) 
  
  The rule is executed even if you do not specify a value for optional parameters. Undefined values are passed for optional parameters on executing the rule.

  ### Support for field and globals objects in custom functions {#support-field-and-global-objects}

  needs to be discussed

  -->

## Consulte también {#see-also}

{{see-also}}





