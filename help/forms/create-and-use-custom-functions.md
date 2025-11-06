---
title: Usar funciones personalizadas en un formulario adaptable
description: AEM Forms admite funciones personalizadas, que permiten a los usuarios crear y utilizar sus propias funciones dentro del editor de reglas.
keywords: Agregar una función personalizada, utilizar una función personalizada, crear una función personalizada, utilizar una función personalizada en el editor de reglas.
contentOwner: Ruchita Srivastav
content-type: reference
feature: Adaptive Forms, Core Components
exl-id: 24607dd1-2d65-480b-a831-9071e20c473d
role: User, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '1336'
ht-degree: 3%

---


# Introducción a las funciones personalizadas para formularios adaptables basados en componentes principales

| Versión | Vínculo del artículo |
| -------- | ---------------------------- |
| AEM 6.5 | [Haga clic aquí](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/forms/adaptive-forms-core-components/create-and-use-custom-functions-core-components) |
| AEM as a Cloud Service | Este artículo |

AEM Forms admite funciones personalizadas, lo que permite a los usuarios definir funciones de JavaScript para implementar reglas comerciales complejas. Estas funciones personalizadas amplían las capacidades de los formularios al facilitar la manipulación y el procesamiento de los datos introducidos para satisfacer requisitos específicos. Permiten la modificación dinámica del comportamiento del formulario en función de criterios predefinidos. Las funciones personalizadas también permiten a los desarrolladores aplicar una lógica de validación compleja, realizar cálculos dinámicos y controlar la visualización o el comportamiento de los elementos del formulario en función de las interacciones del usuario o los criterios predefinidos.

>[!NOTE]
>
> Asegúrese de que el [componente principal](https://github.com/adobe/aem-core-forms-components) está establecido en la versión más reciente para utilizar las características más recientes.

## Usos de las funciones personalizadas {#uses-of-custom-function}

Las ventajas de utilizar funciones personalizadas en Forms adaptable son:

* **Procesamiento de datos**: las funciones personalizadas ayudan a procesar los datos introducidos en los campos de formulario.
* **Validación de datos**: las funciones personalizadas permiten realizar comprobaciones personalizadas en las entradas del formulario y proporcionar mensajes de error especificados.
* **Comportamiento dinámico**: las funciones personalizadas le permiten controlar el comportamiento dinámico de los formularios en función de condiciones específicas. Por ejemplo, puede mostrar u ocultar campos, modificar valores de campos o ajustar la lógica del formulario de forma dinámica.
* **Integración**: puede usar funciones personalizadas para integrarlas con API o servicios externos. Ayuda a recuperar datos de fuentes externas, enviar datos a extremos REST externos o realizar acciones personalizadas basadas en eventos externos.

Las funciones personalizadas son esencialmente bibliotecas de cliente que se agregan en el archivo JavaScript. Una vez creada una función personalizada, esta estará disponible en el editor de reglas para que la seleccione el usuario en un formulario adaptable. Las funciones personalizadas se identifican mediante las anotaciones de JavaScript en el editor de reglas.

## Anotaciones de JavaScript compatibles con funciones personalizadas {#js-annotations}

Las anotaciones de JavaScript se utilizan para proporcionar metadatos para el código de JavaScript. Incluye comentarios que comienzan con símbolos específicos, por ejemplo, /** y @. Las anotaciones proporcionan información importante sobre funciones, variables y otros elementos del código. El formulario adaptable admite las siguientes anotaciones de JavaScript para funciones personalizadas:

### Nombre

El nombre se utiliza para identificar la función personalizada en el editor de reglas de un formulario adaptable. Se utilizan las siguientes sintaxis para asignar un nombre a una función personalizada:

* `@name [functionName] <Function Name>`
* `@function [functionName] <Function Name>`
* `@func [functionName] <Function Name>`.
  `functionName` es el nombre de la función. No se permiten espacios.
  `<Function Name>` es el nombre para mostrar de la función en el editor de reglas de un formulario adaptable.
Si el nombre de la función es idéntico al nombre de la función en sí, puede omitir `[functionName]` de la sintaxis.

### Parámetro

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
   * ámbito: representa el objeto global, que contiene variables de solo lectura como instancias de formulario, instancias de campo de destino y métodos para realizar modificaciones de formulario dentro de funciones personalizadas. Se declara como el último parámetro en las anotaciones de JavaScript y no es visible en el editor de reglas de un formulario adaptable. El parámetro scope accede al objeto del formulario o componente para almacenar en déclencheur la regla o el evento necesarios para el procesamiento del formulario. Para obtener más información sobre el objeto Globals y cómo utilizarlo, [haga clic aquí](/help/forms/custom-function-core-component-scope-function.md).

El tipo de parámetro no distingue entre mayúsculas y minúsculas y no se permiten espacios en el nombre del parámetro.

`<Parameter Description>` contiene detalles sobre el propósito del parámetro. Puede tener varias palabras.

#### Parámetros opcionales

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

### Tipo de devolución

El tipo de valor devuelto especifica el tipo de valor que la función personalizada devuelve después de la ejecución. Las siguientes sintaxis se utilizan para definir un tipo de valor devuelto en una función personalizada:

* `@return {type}`
* `@returns {type}`
  `{type}` representa el tipo de valor devuelto de la función. Los tipos de valor devuelto permitidos son:
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

### Privado

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

## Problema conocido

* Las funciones personalizadas no admiten literales de expresión regular de JavaScript. El uso de literales regex en una función personalizada provoca errores durante la ejecución. Por ejemplo:
  `const pattern = /^abc$/;`

  Para garantizar la compatibilidad, utilice el constructor RegExp en las funciones personalizadas.

  `const pattern = new RegExp("^abc$");`
Refactorice las expresiones regulares para utilizar el constructor RegExp y garantizar una ejecución coherente y fiable.

## Siguiente paso

Para crear y usar una función personalizada en su formulario adaptable, consulte el artículo [Crear una función personalizada para un formulario adaptable basado en componentes principales](/help/forms/custom-function-core-component-create-function.md).

## Ver también

{{see-also-rule-editor}}