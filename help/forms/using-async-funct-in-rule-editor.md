---
title: ¿Cómo se utilizan las llamadas de función asincrónicas en el Editor de reglas visuales?
description: Llamadas a funciones asincrónicas en el editor de reglas visual
feature: Adaptive Forms, Core Components
role: User, Developer
level: Beginner, Intermediate
exl-id: a240ba26-a6d8-4643-8acb-1d8812dac61f
source-git-commit: 2cae8bb1050bc4538f4645d9f064b227fb947d75
workflow-type: tm+mt
source-wordcount: '1409'
ht-degree: 1%

---

# Usar funciones asincrónicas en un formulario adaptable basado en componentes principales

El editor de reglas [de Forms adaptable](/help/forms/rule-editor-core-components.md) admite funciones asincrónicas, lo que permite integrar y administrar operaciones que requieren esperar procesos externos o recuperar datos sin interrumpir la interacción del usuario con el formulario.

## ¿Qué factores determinan el uso de funciones asincrónicas o sincrónicas?

Gestionar la interacción del usuario de forma eficaz es crucial para crear una experiencia fluida. Dos enfoques comunes para controlar las operaciones son las funciones sincrónicas y asincrónicas.

**Funciones sincrónicas** ejecutan las tareas una tras otra, lo que hace que la aplicación espere a que se complete cada operación antes de continuar. Esto puede provocar retrasos y una experiencia del usuario menos atractiva, especialmente cuando las tareas implican esperar recursos externos, como cargas de archivos o recuperación de datos.

Por ejemplo, en un escenario en el que un usuario carga una imagen, todo el formulario se detiene y espera a que se complete la carga. Esta pausa impide que el usuario interactúe con otros campos, lo que provoca frustración y retrasos. Mientras esperan a que la imagen se procese, cualquier información introducida puede perderse si se aleja o pierde la paciencia, lo que hace que la experiencia sea engorrosa e ineficiente.

**Funciones asincrónicas**, por otro lado, permiten que las tareas se ejecuten simultáneamente. Esto significa que los usuarios pueden seguir interactuando con la aplicación mientras se ejecutan los procesos en segundo plano. Las operaciones asincrónicas mejoran la capacidad de respuesta, lo que permite a los usuarios recibir comentarios inmediatos y mantener la participación sin interrupciones.

Por el contrario, con un enfoque asincrónico, los usuarios pueden cargar imágenes en segundo plano sin dejar de rellenar el resto del formulario. La interfaz sigue siendo adaptable, lo que permite realizar actualizaciones en tiempo real y recibir comentarios de forma inmediata a medida que progresa la carga. Mejora la participación del usuario, lo que garantiza una experiencia fluida sin interrupciones.

![Funciones asincrónicas y sincrónicas](/help/forms/assets/sync-async.png){align=center}

## Implementación de funciones asincrónicas para Forms adaptable

Puede implementar las funciones asincrónicas para Forms adaptable mediante los siguientes tipos de reglas en el editor de reglas:

* [Llamada de función asincrónica](#using-asynchronous-function-calls-in-the-visual-rule-editor)
* [Salida de función](#how-to-use-function-output-rule-type)

## ¿Cómo se utiliza el tipo de regla Llamada a función asincrónica?

Puede escribir las [funciones personalizadas](/help/forms/custom-function-core-component-create-function.md) para operaciones asincrónicas y configurar las funciones asincrónicas usando el tipo de regla **[!UICONTROL Llamada a función asincrónica]** en el editor de reglas.

### Exploración del tipo de regla de llamada a función asincrónica mediante un caso de uso

Considere un formulario de registro en un sitio web en el que los usuarios escriban una contraseña de un solo uso (OTP). El panel para añadir detalles del usuario solo aparece después de introducir el OTP correcto. Si el OTP es incorrecto, el panel permanece oculto y aparece un mensaje de error en la pantalla.

![Formulario de inicio de sesión](/help/forms/assets/rule-editor-login-form.png) {width-50%}

En un formulario de registro, cuando el usuario hace clic en el botón **Confirmar**, se llama a la función `matchOTP()` de forma asincrónica para comprobar el OTP introducido. La función `matchOTP()` se ha implementado como [función personalizada](/help/forms/custom-function-core-component-create-function.md). Con el tipo de regla **[!UICONTROL Llamada de función asíncrona]** en el editor de reglas, puede configurar la función `matchOTP()` en el editor de reglas de un formulario adaptable. También puede implementar las llamadas de retorno de éxito y error en el editor de reglas.

La siguiente ilustración ilustra los pasos para usar el tipo de regla **[!UICONTROL Llamada a función asincrónica]** para invocar funciones asincrónicas para Forms adaptable:

![Flujo de trabajo para agregar funciones asincrónicas](/help/forms/assets/workflow-to-add-async-func.png){width=50%, align=center}

### 1. Escriba una función personalizada para la operación asincrónica en el archivo JS

>[!NOTE]
>
> * El editor de reglas de un formulario muestra solamente funciones con un tipo de valor devuelto de `Promise` cuando selecciona el tipo de regla **Llamada a función asincrónica**.
> * Para aprender a crear una función personalizada, consulte el artículo titulado [Crear una función personalizada para un formulario adaptable basado en componentes principales](/help/forms/custom-function-core-component-create-function.md).

La función `matchOTP()` se ha implementado como una función personalizada. El siguiente código se agrega en el archivo JS de la función personalizada:

```JavaScript
/**
 * generates the otp for success use case
 * @param {string} otp
 * @return {PROMISE}
 */
function matchOTP(otp) {
     return new Promise((resolve, reject) => {
        // Perform some asynchronous operation here
         asyncOperationForOTPMatch(otp, (error, result) => {
            if (error) {
                // On failure, call reject(error)
                reject(error);
            } else {
                // On success, call resolve(result)
                resolve(result);
            }
        });
    });
}

/**
 * generates the otp
 */
function asyncOperationForOTPMatch(otp, callback) {
    setTimeout(() => {
        if(otp === '111') {
            callback( null, {'valid':'true'});    
        } else {
            callback( {'valid':'false'}, null);
        }
    }, 1000);
}
```

El código define una función `matchOTP()` que genera una promesa de validar una contraseña de un solo uso (OTP) de forma asincrónica. Utiliza una función `asyncOperationForOTPMatch()` para simular el proceso de coincidencia de OTP. La función comprueba si el OTP proporcionado es igual a `111`. Si el OTP introducido es correcto, llama a la devolución de llamada con null para el error y un objeto que indica que el OTP es válido `({'valid':'true'})`. Si el OTP no es válido, llama a la devolución de llamada con un objeto de error `({'valid':'false'})` y null para el resultado.

### 2. Configure la función asincrónica en el editor de reglas

Realice los siguientes pasos para configurar la función asincrónica en el editor de reglas:

1. [Cree una regla para utilizar una función asincrónica con el tipo de regla de llamada de función asincrónica](#21-create-a-rule-to-use-asynchronous-function-using-the-async-function-call-rule-type)
1. [Implementar las llamadas de retorno para la función asincrónica](#22-implement-the-callbacks-for-asynchronous-function)

#### 2.1 Crear una regla para utilizar una función asincrónica mediante el tipo de regla de llamada de función asincrónica

Para crear una regla para usar una operación asincrónica, use el tipo de regla **[!UICONTROL Llamada a función asincrónica]**, realice los siguientes pasos:

1. Abra el formulario adaptable en el modo de creación, seleccione cualquier componente del formulario y seleccione **[!UICONTROL Editor de reglas]** para abrir el editor de reglas.
1. Seleccione **[!UICONTROL Crear]**.
1. Cree una condición en la sección **When** de la regla para hacer clic en un botón. Por ejemplo, **al hacer clic en[Confirmar]**.
1. En la sección **Then**, seleccione **[!UICONTROL Llamada a función asincrónica]** de la lista desplegable **Seleccionar acción**.
Cuando selecciona **[!UICONTROL Llamada de función asíncrona]** y aparecen las funciones con el tipo de valor devuelto `Promise`.
1. Seleccione la función asincrónica de la lista. Por ejemplo, seleccione la función `matchOTP()` y sus llamadas de retorno tal y como aparecen `Add success callback` y `add failure callback`.
1. Ahora, seleccione los enlaces **[!UICONTROL Input]**. Por ejemplo, seleccione **[!UICONTROL Input]** como `Form Object` y compárelo con el campo `OTP`.

La siguiente captura de pantalla muestra la regla:

![tipo de regla](/help/forms/assets/asyn-function-rule-type.png)

Ahora puede continuar con la implementación de las llamadas de retorno: `Success` y `Failure` para la función `matchOTP`.

#### 2.2 Implementar las llamadas de retorno para la función asincrónica

Implemente los métodos de devolución de llamada success y failure para la función asincrónica mediante el editor de reglas visual.

**Crear una regla para el método `Add Success callback`**

Vamos a crear una regla para mostrar el panel `userdetails`, si el OTP coincide con el valor `111`.

1. Haga clic en **[!UICONTROL Agregar devolución de llamada correcta]**.
1. Haga clic en **[!UICONTROL Agregar instrucción]** para crear la regla.
1. Cree una condición en la sección **When** de la regla.
1. Seleccione **[!UICONTROL Salida de función]** > **[!UICONTROL Obtener carga útil de evento]**.

   >[!NOTE]
   >
   > La función **[!UICONTROL Obtener carga útil de evento]** recupera datos asociados con un evento específico para administrar interacciones de usuario de forma dinámica.

1. Seleccione sus enlaces correspondientes de la sección **Input**. Por ejemplo, seleccione **[!UICONTROL Cadena]** e introduzca `valid`. Comparar la cadena ingresada con `true`.
1. En la sección **Entonces**, seleccione **[!UICONTROL Mostrar]** de la lista desplegable **Seleccionar acción**. Por ejemplo, mostrar el panel `userdetails`.
1. Haga clic en **[!UICONTROL Agregar instrucción]**.
1. Seleccione **[!UICONTROL Ocultar]** de la lista desplegable **Seleccionar acción**. Por ejemplo, oculte el cuadro de texto `error message`.
1. Haga clic en **[!UICONTROL Listo]**.

![Llamada de éxito](/help/forms/assets/rule-editor-success-callback.png){width=50%, height=50%}

Consulte la captura de pantalla siguiente, en la que el usuario introduce el OTP como `111` y aparece el panel `User Details` cuando se hace clic en el botón `Confirm`.

![Éxito](/help/forms/assets/success.gif)

**Crear una regla para el método `Add Failure callback`**

Vamos a crear una regla para mostrar un mensaje de error si el OTP no coincide con el valor `111`.

1. Haga clic en **[!UICONTROL Agregar devolución de llamada con error]**.

1. Haga clic en **[!UICONTROL Agregar instrucción]** para crear la regla.
1. Cree una condición en la sección **When** de la regla.
1. Seleccione **[!UICONTROL Salida de función]** > **[!UICONTROL Obtener carga útil de evento]**.
1. Seleccione sus enlaces correspondientes de la sección **Input**. Por ejemplo, seleccione **[!UICONTROL Cadena]** e introduzca `valid`. Comparar la cadena ingresada con `false`.
1. En la sección **Entonces**, seleccione **[!UICONTROL Mostrar]** de la lista desplegable **Seleccionar acción**. Por ejemplo, mostrar el cuadro de texto `error message`.
1. Haga clic en **[!UICONTROL Agregar instrucción]**.
1. Seleccione **[!UICONTROL Ocultar]** de la lista desplegable **Seleccionar acción**. Por ejemplo, oculte el panel `userdetails`.
1. Haga clic en **[!UICONTROL Listo]**.

![Método de devolución de llamada con error](/help/forms/assets/rule-editor-failure-callback.png){width=50%, height=50%}

Consulte la captura de pantalla siguiente, donde el usuario introduce el OTP como `123` y aparece el mensaje de error cuando se hace clic en el botón `Confirm`.

![Error](/help/forms/assets/failure.gif)

La captura de pantalla siguiente muestra la regla completa para usar **[!UICONTROL Llamada a función asincrónica]** para implementar una función asincrónica:

![Regla para la llamada de función asincrónica](/help/forms/assets/rule-editor-async-callbacks.png)

También puede editar las llamadas de retorno haciendo clic en **[!UICONTROL Editar devolución de llamada correcta]** y **[!UICONTROL Editar devolución de llamada con error]**.

## Cómo usar el tipo de regla de salida de función

También puede llamar a las funciones asincrónicas indirectamente mediante las funciones sincrónicas. Las funciones sincrónicas se ejecutan utilizando el tipo de regla **[!UICONTROL Salida de función]** en el editor de reglas de un formulario adaptable.

Observe el código siguiente para ver cómo invocar funciones asincrónicas utilizando el tipo de regla **[!UICONTROL Salida de función]**:

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

![creando regla para la función asincrónica](/help/forms/assets/rule-for-async-funct.png){width=50%}

Consulte la captura de pantalla de la ventana de la consola siguiente para demostrar que cuando el usuario hace clic en el botón `Fetch`, se invoca la función personalizada `callAsyncFunction`, que a su vez llama a una función asincrónica `asyncFunction`. Inspeccione la ventana de la consola para ver la respuesta al clic en el botón:

![Ventana de consola](/help/forms/assets/async-custom-funct-console.png)

## Véase también

{{see-also-rule-editor}}
