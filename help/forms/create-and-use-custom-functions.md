---
title: Crear y agregar funciones personalizadas en un formulario adaptable
description: AEM Forms admite funciones personalizadas que permiten a los usuarios crear y utilizar sus propias funciones dentro del editor de reglas.
keywords: Agregar una función personalizada, utilizar una función personalizada, crear una función personalizada, utilizar una función personalizada en el editor de reglas.
contentOwner: Ruchita Srivastav
content-type: reference
feature: Adaptive Forms, Core Components
source-git-commit: 94a290964a92f8c6ed353d9c77f3dd3b8a5598a4
workflow-type: tm+mt
source-wordcount: '778'
ht-degree: 22%

---


# Funciones personalizadas en Forms adaptable (componentes principales)

## Introducción

AEM Forms admite funciones personalizadas, lo que permite a los usuarios definir funciones de JavaScript para implementar reglas comerciales complejas. Estas funciones personalizadas amplían las capacidades de los formularios al facilitar la manipulación y el procesamiento de los datos introducidos para satisfacer requisitos específicos. También permiten la modificación dinámica del comportamiento del formulario en función de criterios predefinidos.
En Forms adaptable, puede utilizar funciones personalizadas dentro de [Editor de reglas de un formulario adaptable](/help/forms/rule-editor.md#custom-functions) para crear reglas de validación específicas para los campos de formulario.

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

Algunas de las ventajas de utilizar funciones personalizadas en Forms adaptable son:

* **Manipulación de datos**: Las funciones personalizadas manipulan y procesan los datos introducidos en los campos de formulario.
* **Validación de datos**: las funciones personalizadas permiten realizar comprobaciones personalizadas en las entradas del formulario y proporcionar mensajes de error especificados.
* **Comportamiento dinámico**: las funciones personalizadas le permiten controlar el comportamiento dinámico de los formularios en función de condiciones específicas. Por ejemplo, puede mostrar u ocultar campos, modificar valores de campos o ajustar la lógica del formulario de forma dinámica.
* **Integración**: Puede utilizar funciones personalizadas para integrarse con API o servicios externos. Ayuda a recuperar datos de fuentes externas, enviar datos a extremos REST externos o realizar acciones personalizadas basadas en eventos externos.

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

* **Función de flecha con comentario jsdoc obligatorio**

Algunos de los ejemplos para crear funciones de flecha son los siguientes:

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

<!-- 
    * @param {string=} b another parameter description
      /** */
    testFunction1=(a) => (return a)
    /** */
    testFunction2 = a => a + 100;-->

* **Expresión de función con comentario jsdoc obligatorio**

Cree funciones personalizadas en los siguientes formatos para enumerarlas en el editor de reglas de un formulario adaptable. Por ejemplo:

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
> Puede consultar la `error.log` en caso de errores, como las funciones personalizadas, no se enumeran en el editor de reglas.

<!--The `error.log` file also displays the methods and parameters that are not supported for custom functions. -->


## Creación de una función personalizada {#create-custom-function}

Cree una biblioteca de cliente para llamar a funciones personalizadas en el editor de reglas. Para obtener más información, consulte [Uso de bibliotecas del lado del cliente](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/full-stack/clientlibs.html?lang=es#developing).

Los pasos para crear funciones personalizadas son los siguientes:
1. [Crear una biblioteca de cliente](#create-client-library)
1. [Agregar una biblioteca de cliente en un formulario adaptable](#use-custom-function)

### Crear una biblioteca de cliente {#create-client-library}

Puede agregar funciones personalizadas agregando la biblioteca de cliente. Para crear una biblioteca de cliente, realice los siguientes pasos:

1. [Clone su repositorio de AEM Forms as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html?lang=es#accessing-git).
1. Crear una carpeta dentro de la carpeta `[AEM Forms as a Cloud Service repository folder]/apps/`. Por ejemplo, cree una carpeta denominada `experience-league`
1. Vaya a `[AEM Forms as a Cloud Service repository folder]/apps/[AEM Project Folder]/experience-league/` y cree un `ClientLibraryFolder` como `es6clientlibs`.
1. Añadir una propiedad `categories`con valor de tipo de cadena como `es6customfunctions` a la `es6clientlibs` carpeta.

   >[!NOTE]
   >
   >`es6customfunctions` es una categoría de ejemplo. Puede elegir cualquier nombre para la categoría.

1. Cree una carpeta con el nombre `js`.
1. Navegue hasta la carpeta `[AEM Forms as a Cloud Service repository folder]/apps/[AEM Project Folder]/es6clientlibs/js`. 
1. Añada un archivo JavaScript, por ejemplo `function.js`.  El archivo contiene el código de la función personalizada.

   >[!NOTE]
   >
   >* Si el archivo JavaScript que contiene código para funciones personalizadas tiene un error, las funciones personalizadas no aparecen en el editor de reglas de un formulario adaptable. También puede consultar la `error.log` archivo para el error.

   <!-- 
    >* AEM Adaptive Form supports the caching of custom functions. If the JavaScript is modified, the caching becomes invalidated, and it is parsed. You can see a message as `Fetched following custom functions list from cache` in the `error.log` file.  -->

1. Guarde el archivo `function.js`.
1. Navegue hasta la carpeta `[AEM Forms as a Cloud Service repository folder]/apps/[AEM Project Folder]/es6clientlibs/js`. 
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

Una vez que la canalización se ejecute correctamente, la función personalizada agregada en la biblioteca de cliente estará disponible en su [Editor de reglas de formulario adaptable](/help/forms/rule-editor.md).

### Agregar una biblioteca de cliente en un formulario adaptable{#use-custom-function}

Después de agregar la biblioteca de cliente, utilícela en el formulario adaptable. Le permite utilizar su [función personalizada como regla en el formulario](/help/forms/rule-editor.md#custom-functions). Para agregar la biblioteca del cliente en el formulario adaptable, siga estos pasos:

1. Abra el formulario en modo de edición. 
Para abrir un formulario en modo de edición, seleccione un formulario y **[!UICONTROL Ábralo]**.
1. En el modo de edición, seleccione un componente y, a continuación, ![field-level](assets/select_parent_icon.svg) > **[!UICONTROL Contenedor de formulario adaptable]** y ![cmppr](assets/configure-icon.svg).
1. En la barra lateral, bajo Nombre de la biblioteca de cliente, agregue la biblioteca de cliente. (`es6customfunctions` en el ejemplo)

   ![Agregar la biblioteca de cliente de funciones personalizada](/help/forms/assets/clientlib-custom-function.png)

Cree una regla para utilizar una función personalizada en el editor de reglas.

<!--

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





