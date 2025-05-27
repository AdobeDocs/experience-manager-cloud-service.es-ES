---
title: ¿Cómo se utilizan las llamadas a funciones asíncronas en el editor de reglas visuales?
description: Llamadas a funciones asíncronas en el editor de reglas visuales
feature: Adaptive Forms, Core Components
role: User, Developer
level: Beginner, Intermediate
exl-id: a240ba26-a6d8-4643-8acb-1d8812dac61f
source-git-commit: 2cae8bb1050bc4538f4645d9f064b227fb947d75
workflow-type: ht
source-wordcount: '1409'
ht-degree: 100%

---

# Uso de funciones asíncronas en un formulario adaptable basado en componentes principales

El [editor de reglas de formularios adaptables](/help/forms/rule-editor-core-components.md) admite funciones asíncronas, lo que permite integrar y administrar operaciones que requieren esperar procesos externos o recuperar datos sin interrumpir la interacción del usuario con el formulario.

## ¿Qué factores determinan el uso de funciones asíncronas o síncronas?

Gestionar la interacción del usuario de forma eficaz es crucial para crear una experiencia fluida. Dos enfoques comunes para gestionar las operaciones son las funciones síncronas y asíncronas.

Las **Funciones síncronas** ejecutan las tareas una tras otra, lo que hace que la aplicación espere a que se complete cada operación antes de continuar. Esto puede dar lugar a retrasos y una experiencia del usuario menos interesante, especialmente cuando las tareas implican esperar recursos externos, como cargas de archivos o recuperación de datos.

Por ejemplo, en un escenario en el que un usuario carga una imagen, todo el formulario se detiene y espera hasta que se complete la carga. Esta pausa impide que el usuario interactúe con otros campos, lo que provoca frustración y retrasos. Mientras el usuario espera a que la imagen se procese, cualquier información introducida puede perderse si se aleja o pierde la paciencia, lo que hace que la experiencia sea engorrosa e ineficiente.

Las **funciones asíncronas**, por otro lado, permiten que las tareas se ejecuten simultáneamente. Esto significa que los usuarios pueden seguir interactuando con la aplicación mientras los procesos se ejecutan en segundo plano. Las operaciones asíncronas mejoran la capacidad de respuesta, lo que permite a los usuarios recibir comentarios inmediatos y mantener la participación sin interrupciones.

Por el contrario, con un enfoque asíncrono, los usuarios pueden cargar imágenes en segundo plano mientras continúan rellenando el resto del formulario sin interrupciones. La interfaz sigue siendo adaptable, lo que permite realizar actualizaciones en tiempo real y recibir comentarios de forma inmediata a medida que progresa la carga. Mejora la participación del usuario, lo que garantiza una experiencia fluida sin interrupciones.

![Funciones asíncronas y síncronas](/help/forms/assets/sync-async.png){align=center}

## Implementación de funciones asíncronas para formularios adaptables

Puede implementar las funciones asíncronas para formularios adaptables mediante los siguientes tipos de reglas en el editor de reglas:

* [Llamada a función asíncrona](#using-asynchronous-function-calls-in-the-visual-rule-editor)
* [Salida de función](#how-to-use-function-output-rule-type)

## ¿Cómo se utiliza el tipo de regla Llamada a función asíncrona?

Puede escribir las [funciones personalizadas](/help/forms/custom-function-core-component-create-function.md) para operaciones asíncronas y configurar las funciones asíncronas usando el tipo de regla **[!UICONTROL Llamada a función asíncrona]** en el editor de reglas.

### Exploración del tipo de regla Llamada a función asíncrona mediante un caso de uso

Considere un formulario de registro en un sitio web en el que los usuarios escriben una contraseña de un solo uso (OTP). El panel para añadir detalles del usuario solo aparece después de introducir la OTP correcta. Si la OTP es incorrecta, el panel permanece oculto y aparece un mensaje de error en la pantalla.

![Formulario de inicio de sesión](/help/forms/assets/rule-editor-login-form.png) {width-50%}

En un formulario de registro, cuando el usuario hace clic en el botón **Confirmar**, se llama a la función `matchOTP()` de forma asíncrona para comprobar la OTP introducida. La función `matchOTP()` se ha implementado como una [función personalizada](/help/forms/custom-function-core-component-create-function.md). Con el tipo de regla **[!UICONTROL Llamada a función asíncrona]** en el editor de reglas, puede configurar la función `matchOTP()` en el editor de reglas de un formulario adaptable. También puede implementar las llamadas de retorno de éxito y error en el editor de reglas.

En la siguiente figura se muestran los pasos para usar el tipo de regla **[!UICONTROL Llamada a función asíncrona]** para invocar funciones asíncronas para formularios adaptables:

![Flujo de trabajo para añadir funciones asíncronas](/help/forms/assets/workflow-to-add-async-func.png){width=50%, align=center}

### 1. Escribir una función personalizada para la operación asíncrona en el archivo JS

>[!NOTE]
>
> * El editor de reglas de un formulario solo muestra funciones con un tipo de valor devuelto de `Promise` cuando selecciona el tipo de regla **Llamada a función asíncrona**.
> * Para aprender a crear una función personalizada, consulte el artículo titulado [Creación de una función personalizada para un formulario adaptable basado en componentes principales](/help/forms/custom-function-core-component-create-function.md).

La función `matchOTP()` se ha implementado como una función personalizada. El siguiente código se añade en el archivo JS de la función personalizada:

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

El código define una función `matchOTP()` que genera una promesa de validar una contraseña de un solo uso (OTP) de forma asíncrona. Utiliza una función `asyncOperationForOTPMatch()` para simular el proceso de coincidencia de OTP. La función comprueba si la OTP proporcionada es igual a `111`. Si la OTP introducida es correcta, llama a la devolución de llamada con un valor nulo para el error y un objeto que indica que la OTP es válida `({'valid':'true'})`. Si la OTP no es válida, llama a la devolución de llamada con un objeto de error `({'valid':'false'})` y un valor nulo para el resultado.

### 2. Configurar la función asíncrona en el editor de reglas

Realice los siguientes pasos para configurar la función asíncrona en el editor de reglas:

1. [Crear una regla para utilizar una función asíncrona con el tipo de regla de llamada a función asíncrona](#21-create-a-rule-to-use-asynchronous-function-using-the-async-function-call-rule-type)
1. [Implementar las llamadas de retorno para la función asíncrona](#22-implement-the-callbacks-for-asynchronous-function)

#### 2.1 Crear una regla para utilizar la función asíncrona mediante el tipo de regla de llamada a función asíncrona

Para crear una regla para usar la operación asíncrona, use el tipo de regla **[!UICONTROL Llamada a función asíncrona]** y realice los siguientes pasos:

1. Abra el formulario adaptable en el modo de creación, seleccione cualquier componente del formulario y seleccione **[!UICONTROL Editor de reglas]** para abrir el editor de reglas.
1. Seleccione **[!UICONTROL Crear]**.
1. Cree una condición en la sección **When** de la regla para hacer clic en un botón. Por ejemplo, se hace clic en **When[Confirmar]**.
1. En la sección **Then**, seleccione **[!UICONTROL Llamada a función asíncrona]** en la lista desplegable **Seleccionar acción**.
Cuando selecciona **[!UICONTROL Llamada a función asíncrona]** y las funciones con el tipo de valor devuelto `Promise` aparecen.
1. Seleccione la función asíncrona en la lista. Por ejemplo, seleccione la función `matchOTP()` y aparecen sus llamadas de retorno como `Add success callback` y `add failure callback`.
1. Ahora, seleccione los enlaces de **[!UICONTROL Entrada]**. Por ejemplo, seleccione **[!UICONTROL Entrada]** como `Form Object` y compárelo con el campo `OTP`.

La siguiente captura de pantalla muestra la regla:

![tipo de regla](/help/forms/assets/asyn-function-rule-type.png)

Ahora puede continuar con la implementación de las llamadas de retorno: `Success` y `Failure` para la función `matchOTP`.

#### 2.2 Implementar las llamadas de retorno para la función asíncrona

Implemente los métodos de llamada de retorno de éxito y error para la función asíncrona mediante el editor de reglas visuales.

**Crear una regla para el método `Add Success callback`**

Vamos a crear una regla para mostrar el panel `userdetails`, si la OTP coincide con el valor `111`.

1. Haga clic en **[!UICONTROL Añadir llamada de retorno de éxito]**.
1. Haga clic en **[!UICONTROL Añadir declaración]** para crear la regla.
1. Cree una condición en la sección **When** de la regla. 
1. Seleccione **[!UICONTROL Salida de función]** > **[!UICONTROL Obtener carga útil de evento]**.

   >[!NOTE]
   >
   > La función **[!UICONTROL Obtener carga útil de evento]** recupera los datos asociados a un evento específico para administrar interacciones de usuario de forma dinámica.

1. Seleccione los enlaces correspondientes en la sección **Entrada**. Por ejemplo, seleccione **[!UICONTROL Cadena]** e introduzca `valid`. Compare la cadena introducida con `true`.
1. En la sección **Then**, seleccione **[!UICONTROL Mostrar]** en la lista desplegable **Seleccionar acción**. Por ejemplo, muestre el panel `userdetails`.
1. Haga clic en **[!UICONTROL Añadir declaración]**.
1. Seleccione **[!UICONTROL Ocultar]** en la lista desplegable **Seleccionar acción**. Por ejemplo, oculte el cuadro de texto `error message`.
1. Haga clic en **[!UICONTROL Listo]**.

![Llamada de éxito](/help/forms/assets/rule-editor-success-callback.png){width=50%, height=50%}

Consulte la captura de pantalla siguiente, en la que el usuario introduce la OTP como `111` y aparece el panel `User Details` cuando se hace clic en el botón `Confirm`.

![Éxito](/help/forms/assets/success.gif)

**Crear una regla para el método `Add Failure callback`**

Vamos a crear una regla para mostrar un mensaje de error si la OTP no coincide con el valor `111`.

1. Haga clic en **[!UICONTROL Añadir llamada de retorno con error]**.

1. Haga clic en **[!UICONTROL Añadir declaración]** para crear la regla.
1. Cree una condición en la sección **When** de la regla. 
1. Seleccione **[!UICONTROL Salida de función]** > **[!UICONTROL Obtener carga útil de evento]**.
1. Seleccione los enlaces de datos en la sección **Salida**. Por ejemplo, seleccione **[!UICONTROL Cadena]** e introduzca `valid`. Compare la cadena introducida con `false`.
1. En la sección **Then**, seleccione **[!UICONTROL Mostrar]** en la lista desplegable **Seleccionar acción**. Por ejemplo, muestre el cuadro de texto `error message`.
1. Haga clic en **[!UICONTROL Añadir declaración]**.
1. Seleccione **[!UICONTROL Ocultar]** en la lista desplegable **Seleccionar acción**. Por ejemplo, oculte el panel `userdetails`.
1. Haga clic en **[!UICONTROL Listo]**.

![Método de llamada de retorno de error](/help/forms/assets/rule-editor-failure-callback.png){width=50%, height=50%}

Consulte la captura de pantalla siguiente, donde el usuario introduce la OTP como `123` y aparece el mensaje de error cuando se hace clic en el botón `Confirm`.

![Error](/help/forms/assets/failure.gif)

En la siguiente captura de pantalla se muestra la regla completa para usar la **[!UICONTROL Llamada a función asíncrona]** para implementar una función asíncrona:

![Regla para la llamada de función asíncrona](/help/forms/assets/rule-editor-async-callbacks.png)

También puede editar las llamadas de retorno haciendo clic en **[!UICONTROL Editar llamada de retorno de éxito]** y **[!UICONTROL Editar llamada de retorno de error]**.

## ¿Cómo se usa el tipo de regla de salida de función?

También puede llamar a las funciones asíncronas indirectamente mediante las funciones síncronas. Las funciones síncronas se ejecutan utilizando el tipo de regla **[!UICONTROL Salida de función]** en el editor de reglas de un formulario adaptable.

Observe el código siguiente para ver cómo invocar funciones asíncronas utilizando el tipo de regla **[!UICONTROL Salida de función]**:

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

En el ejemplo anterior, la función asyncFunction es una `asynchronous function`. Realiza una operación asíncrona realizando una solicitud `GET` a `https://petstore.swagger.io/v2/store/inventory`. Espera la respuesta con `await`, analiza el cuerpo de la respuesta como JSON con `response.json()` y, a continuación, devuelve los datos. La función `callAsyncFunction` es una función síncrona personalizada que invoca la función `asyncFunction` y muestra los datos de respuesta en la consola. Aunque la función `callAsyncFunction` es síncrona, llama a la función asyncFunction asíncrona y gestiona su resultado con las instrucciones `then` y `catch`.

Para ver cómo funciona, vamos a añadir un botón y crear una regla para el botón que invoca la función asíncrona al hacer clic en un botón.

![creación de la regla para la función asíncrona](/help/forms/assets/rule-for-async-funct.png){width=50%}

Consulte la siguiente captura de pantalla de la ventana de consola para demostrar que cuando el usuario hace clic en el botón `Fetch`, se invoca la función personalizada `callAsyncFunction`, que a su vez llama a una función asíncrona `asyncFunction`. Inspeccione la ventana de la consola para ver la respuesta al clic en el botón:

![Ventana de consola](/help/forms/assets/async-custom-funct-console.png)

## Véase también

{{see-also-rule-editor}}
