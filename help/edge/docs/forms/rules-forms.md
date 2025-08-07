---
title: Usar reglas para añadir un comportamiento dinámico a un formulario
description: Edge Delivery Services para AEM Forms están diseñados para ofrecer un rendimiento máximo, lo que le permite imaginar el futuro de la recopilación de datos optimizada y la participación del usuario. Usar reglas para añadir un comportamiento dinámico a los formularios.
feature: Edge Delivery Services
exl-id: 58042016-e655-446f-a2bf-83f1811525e3
role: Admin, Architect, Developer
source-git-commit: 2e2a0bdb7604168f0e3eb1672af4c2bc9b12d652
workflow-type: tm+mt
source-wordcount: '2218'
ht-degree: 100%

---

# Usar reglas para añadir un comportamiento dinámico a los formularios

Una de las potentes funciones de creación de formularios mediante una hoja de cálculo es la posibilidad de utilizar funciones de integradas de la hoja de cálculo para crear reglas, lo que le permite mostrar u ocultar condicionalmente campos de formulario, automatizar cálculos basados en los datos introducidos por el usuario y crear una experiencia del usuario más dinámica.

En este artículo se explica cómo utilizar varias propiedades de bloque de formulario adaptable, principalmente [`Visible`](#visible-property), [`Visibility Expression`](#visible-expression-property) y [`Value Expression`](#value-expression-property) junto con las [funciones de hoja de cálculo](#spreadsheet-functions-for-rules) para crear reglas efectivas para los formularios. También analizaremos algunos ejemplos para ilustrar cómo se pueden implementar estas reglas en la práctica.

## Explicación de las construcciones de una regla

Las reglas son como instrucciones que nos dicen qué hacer en diferentes situaciones. Una regla suele tener las siguientes construcciones:

- Condiciones: especifican las circunstancias en las que se aplica la regla. Piense en ellas como si fueran una pregunta que debe responderse (sí o no).

- Acciones: definen lo que sucede cuando se cumple la condición (verdadero) o no se cumple (falso).


Por ejemplo, para mostrar un cuadro de correo electrónico, cuando se selecciona una casilla de verificación:

- Condición: La casilla de verificación &quot;¿Do you like to subscribe for Magazine &amp; Activities?&quot; (Le gustaría suscribirse a Magazine &amp; Activities?) está seleccionada. (¿Sí o no?). Esta condición se establece en la propiedad `Visible` del formulario.
- Acción (Verdadero): se muestra el cuadro de correo electrónico. (Qué sucede si es sí). `Visibility Expression`utiliza la condición definida para la propiedad `visible` para mostrar dinámicamente los campos.
- Acción (Falso): el cuadro de correo electrónico está oculto. (Qué sucede si es no). `Visibility Expression` utiliza la condición definida para que `Value` oculte dinámicamente los campos.

Para obtener instrucciones detalladas paso a paso, consulte [nostrar/ocultar un campo de correo electrónico en función de una condición](#example-1-conditional-email-field)


## Explicación de las propiedades Valor, Visible, Expresión de visibilidad y Expresión de valor

### Propiedad Visible

Imagine un interruptor de luz para su campo de formulario. La propiedad `Visible` es como ese interruptor. Controla si el campo es visible inicialmente en el formulario la primera vez que se carga.

- Verdadero (como si el interruptor de luz estuviera &quot;activado&quot;): el campo se muestra en el formulario.
- Falso (como si el interruptor de luz estuviera &quot;desactivado&quot;): el campo está oculto en el formulario.

Puede utilizar la fórmula SpreadSheet (incluida la etiqueta = ) para escribir una fórmula utilizando una lógica de hoja de cálculo para determinar la visibilidad del campo. Puede utilizar los valores de otros campos del formulario dentro de esta fórmula. Por ejemplo, si un usuario selecciona &quot;Individual&quot; en un campo de tipo de registro, puede ocultar el campo de correo electrónico con una fórmula que compruebe ese valor.

### Propiedad Expresión visible (mostrar/ocultar un campo)

La propiedad `Visible Expression` permite utilizar la regla añadida a la propiedad `Visible` para decidir si mostrar u ocultar el campo en función de las interacciones del usuario.

Utilice `=FORMULATEXT("Address of the corresponding Visible property)` para llevar la fórmula mencionada en la propiedad `Visible` como una cadena al campo de la propiedad `Visible Expression`. Esto es necesario para mostrar u ocultar dinámicamente campos en un formulario publicado.

![Forumaltext](/help/edge/assets/aem-forms-formulatext.png)

### Propiedad Valor (establecer los datos iniciales)

Imagine un valor preestablecido en un regulador de intensidad de la luz de una habitación. La propiedad `Value` es similar. Determina el estado inicial de los datos que un usuario ve en el campo.  Establece o recupera los datos actuales que se muestran en el campo del formulario.

Cuando el formulario se carga por primera vez, la propiedad `Value` determina lo que el usuario ve en el campo antes de que realice algún cambio. A diferencia de las propiedades `Visible` y `Visible Expression` que controlan la visibilidad, la propiedad Valor afecta directamente a los propios datos. Los usuarios pueden modificar este valor escribiendo, seleccionando opciones (menús desplegables) o interactuando con el campo.

Puede utilizar la fórmula de Excel (incluida la etiqueta = ) para escribir una fórmula utilizando una lógica de hoja de cálculo para determinar el valor mostrado en el campo. Puede utilizar los valores de otros campos del formulario dentro de esta fórmula. Por ejemplo, puede calcular un descuento automáticamente basándose en el importe del pedido introducido en otro campo.


### Propiedad Expresión de valor (calcular valores que se mostrarán en un campo)

Esta propiedad permite controlar el valor mostrado dentro de un campo en función de una fórmula, similar a la Expresión visible. Imagine una calculadora integrada en el campo.

Utilice `=FORMULATEXT("Address of the corresponding Value property)` para llevar la fórmula mencionada en la propiedad `Value` como una cadena al campo de la propiedad `Value Expression`. Esto es necesario para calcular y mostrar dinámicamente los valores calculados en un formulario publicado.

![Forumaltext](/help/edge/assets/aem-forms-formulatext-value.png)

A continuación, mostramos una analogía para afianzar estos conceptos:

- Visible: imagine que un formulario es como una casa. La propiedad &quot;Visible&quot; es como el interruptor de la luz de cada habitación (campo). Usted decide si la habitación está inicialmente iluminada (visible) u oscura (oculta) cuando alguien entra en la casa (abre el formulario).
- Expresión visible: es como un interruptor de la luz con un sensor de movimiento. La habitación (campo) puede estar inicialmente oscura (oculta), pero una fórmula (sensor de movimiento) puede activarla (mostrar el campo) si alguien pasa por allí (cambia el valor en otro campo).
- Valor: es como un regulador de intensidad preajustado de la luz (datos iniciales del campo). Los usuarios pueden ajustar el brillo (modificar el valor).
- Expresión de valor: es como una calculadora de lujo integrada en la etiqueta de precio de un producto en la casa (formulario). La etiqueta de precio (campo) muestra el precio final en función de una fórmula (por ejemplo, añadir impuestos al precio base) que utiliza otra información como el precio base (valor de otro campo).

Al combinar estas propiedades con [funciones de hoja de cálculo](#spreadsheet-functions-for-rules), puede lograr una amplia gama de comportamientos dinámicos en sus formularios.

## Funciones de hoja de cálculo para reglas

El bloque de formularios adaptables admite diversas funciones de hoja de cálculo que se pueden utilizar para crear reglas. Estas son las funciones disponibles de forma predeterminada (OOTB):

### Funciones lógicas

- [NOT()](https://docs.oasis-open.org/office/v1.2/os/OpenDocument-v1.2-os-part2.html#__RefHeading__1018452_715980110): invierte el estado lógico (TRUE se convierte en FALSE y viceversa).
- [AND()](https://docs.oasis-open.org/office/v1.2/os/OpenDocument-v1.2-os-part2.html#AND): devuelve TRUE sólo si todas las condiciones especificadas son TRUE.
- [OR()](https://docs.oasis-open.org/office/v1.2/os/OpenDocument-v1.2-os-part2.html#OR): devuelve TRUE si al menos una de las condiciones especificadas es TRUE.

### Funciones condicionales

- [IF()](https://docs.oasis-open.org/office/v1.2/os/OpenDocument-v1.2-os-part2.html#__RefHeading__1018446_715980110): evalúa una condición y devuelve un valor específico si es TRUE y otro valor si es FALSE.

### Funciones matemáticas

- [SUM()](https://docs.oasis-open.org/office/v1.2/os/OpenDocument-v1.2-os-part2.html#SUM): añade valores de un rango de celdas especificado.
- [ROUND()](https://docs.oasis-open.org/office/v1.2/os/OpenDocument-v1.2-os-part2.html#ROUND): redondea un número hasta un número determinado de decimales.
- [MIN()](https://docs.oasis-open.org/office/v1.2/os/OpenDocument-v1.2-os-part2.html#MIN): devuelve el valor más pequeño de un rango de celdas especificado.

## Creación de una regla

Veamos algunos ejemplos prácticos para ilustrar cómo se pueden utilizar las reglas para mejorar los formularios:

## Ejemplo 1: Campo de correo electrónico condicional

En este ejemplo se muestra cómo la casilla de verificación actúa como una condición. Cuando está seleccionada (la condición es verdadera), aparece el cuadro de correo electrónico (acción para verdadero). Si no está seleccionada (la condición es falsa), el cuadro de correo electrónico permanece oculto (acción para falso).

Cree un formulario con una casilla de verificación y un cuadro de correo electrónico, tal como se muestra en la siguiente imagen:

![Formulario de correo electrónico condicional](/help/edge/assets/aem-forms-conditional-email-form.png)


A continuación, se muestra cómo utilizar una regla para mostrar el campo de correo electrónico al seleccionar una casilla de verificación:

1. Establezca la propiedad `Value` del campo del casilla de verificación en `TRUE`.
1. Establezca la propiedad `Checked` del campo de la casilla de verificación en `FALSE`. Esto garantiza que la casilla de verificación no esté seleccionada de forma predeterminada.
1. Establezca la propiedad `Visible` del campo de correo electrónico en `=[address of Checked property of the checkbox field] = true()`. Por ejemplo, `=Q11=TRUE()`. La fórmula evalúa si la casilla de verificación está seleccionada o no. Si la casilla de verificación está seleccionada, la fórmula se evalúa como TRUE. Si la casilla de verificación no está seleccionada, la fórmula se evalúa como FALSE.



   La función `TRUE()`, devuelve el valor lógico, cuando se establece para que apunte a la propiedad `Checked`, si la propiedad `checked = false` devuelve el valor falso. Si `checked=true`, devuelve `true`. Esto garantiza que el campo de correo electrónico esté oculto de forma predeterminada.


1. Establezca la propiedad `Visible Expression` del campo de la casilla de verificación en `=FORMULATEXT ((address of Visible property of the checkbox field))`. Por ejemplo, `=FORMULATEXT((G12))`. La función FORMULATEXT() toma una fórmula como entrada y devuelve la propia fórmula como cadena de texto. Ayuda a utilizar la fórmula en el formulario.

   ![Campo de correo electrónico condicional](/help/edge/assets/aem-forms-visible-expression-formula-text.png)

1. Previsualice y publique el formulario. Ahora, al seleccionar la casilla de verificación, se muestra el campo de correo electrónico, mientras que si se deselecciona, se oculta el campo, lo que proporciona una experiencia del usuario dinámica.

   ![Correo electrónico condicional](/help/edge/assets/aem-forms-coditional-email.gif)


## Ejemplo 2: Cálculo automático

En este ejemplo se muestra cómo un formulario calcula automáticamente el coste estimado del viaje al seleccionar las fechas de viaje en un formulario.

Cree un formulario con un campo de fecha, presupuesto de la habitación, campos del coste estimado del viaje tal como se muestran a continuación y un cuadro de correo electrónico, tal como se muestra en la siguiente imagen:

![Formulario de correo electrónico condicional](/help/edge/assets/aem-forms-automatic-calculations-form.png)

A continuación se indica cómo utilizar un cálculo automático para mostrar el coste estimado del viaje:

1. Establezca la propiedad `Value` del campo `amount` en `=F6*DAYS(F3,F2)`. Esta fórmula calcula el número de días desde `Start Date`  y `End Date`, multiplica el número de días con el presupuesto de la habitación y muestra el resultado en el campo `Estimated Trip Cost`.

1. Establezca la propiedad `Value Expression` del campo `Estimated Trip Cost` en `=FORMULATEXT ((address of value property of the amount field))`. Por ejemplo, `=FORMULATEXT(F7)`. La función FORMULATEXT() toma una fórmula como entrada y devuelve la propia fórmula como cadena de texto. Ayuda a utilizar la fórmula en el formulario.

1. Previsualice y publique el formulario. Ahora, al especificar `Start Date`, `End Date` y el presupuesto de la habitación. El `Estimated Trip Cost` se calcula automáticamente.

## Ejemplos de funciones de hoja de cálculo


Estos son algunos ejemplos de las funciones de hoja de cálculo más utilizadas:

**Funciones lógicas**:

- **NOT():** invierte el estado lógico (TRUE se convierte en FALSE y viceversa).

  Ejemplo: ocultar un campo &quot;Confirmar correo electrónico&quot; si el campo de correo electrónico se deja en blanco.

   1. Establezca la propiedad `Visible` del campo “Confirmar correo electrónico” en `=NOT(if('address of email field'=""))`.

      ![Campo Confirmar correo electrónico de AEM Forms](/help/edge/assets/aem-forms-not-function-hide-email-field.png)


   1. Establezca la expresión visible del campo “Confirmar correo electrónico” en `=FORMULATEXT ((address of visible property of the Confirm Email field))`

      ![Fórmula de expresión visible de AEM Forms](/help/edge/assets/aem-forms-visible-expression-formula-text.png)


- AND(): devuelve TRUE sólo si todas las condiciones especificadas son TRUE.

   - Ejemplo: habilitar un botón de &quot;envío&quot; sólo si se rellenan todos los campos obligatorios.

   1. Establezca la propiedad `Visible` del botón &quot;enviar&quot; en:



      ```JavaScript
      =AND(NOT(address of `value` property of the `name` field = ""), NOT(address of `value` property of the `email` field = ""), NOT(address of `value` property of the `phone` field))
      ```

      Por ejemplo,

      ```JavaScript
      =AND(NOT(F9=""), NOT(F12=""), NOT(F10=""))
      ```

   1. Establezca la expresión visible del campo “Confirmar correo electrónico” en

      ```JavaScript
      =FORMULATEXT ((address of visible property of the Confirm Email field))
      ```

      Por ejemplo,

      ```JavaScript
      =FORMULATEXT(G14)
      ```

      Esta fórmula muestra el botón &quot;Enviar&quot; (TRUE) sólo si se rellenan todos los campos (nombre, correo electrónico, teléfono) (NOT(()) devuelve TRUE para cada uno), de lo contrario oculta el botón (AND(multiple FALSES) = FALSE).

- OR(): devuelve TRUE si al menos una de las condiciones especificadas es TRUE.

   - Ejemplo: Aplicar un descuento si un usuario introduce cualquiera de los códigos del cupón descuento aplicables.

   1. Establezca la propiedad `Visible` del campo “importe final” en:


  ```JavaScript
     =IF(OR(F14="BlackFridaySale", F14="NewYearDiscount"), (F6*DAYS(F3,F2)* 0.7) , (F6*DAYS(F3,F2)))
  ```

   1. Establezca la expresión del valor del campo “Confirmar correo electrónico” en

      ```JavaScript
      =FORMULATEXT ((address of value property of the final amount field))
      ```

      Por ejemplo,

      ```JavaScript
      =FORMULATEXT(F7)
      ```

      Esta fórmula calcula un descuento del 30 %, si el usuario introduce un código de cupón (couponCode = &quot;NewYearDiscount&quot;) O (couponCode = &quot;BlackFridaySale&quot;); de lo contrario, establece el descuento en 0.

**Funciones de texto:**

- IF(): evalúa una condición y devuelve un valor específico si es TRUE y otro valor si es FALSE.

   - Ejemplo: Visualización de un mensaje personalizado basado en una categoría de producto elegida.

   1. Establezca la propiedad `Value` del campo `message` en `Only upto 7 kg check-in lagguage is allowed!`:

   1. Establezca la propiedad `Visible` del campo `message` en:


      ```JavaScript
      =if(address of value property of chosen product category ="Economy", TRUE(), FALSE())
      ```

      Por ejemplo,

      ```JavaScript
      =if(F5="Economy", TRUE(), FALSE())
      ```

   1. Establezca la expresión de valor del campo `message` en

      ```JavaScript
      =FORMULATEXT ((address of value property of the final amount field))
      ```

      Por ejemplo,

      ```JavaScript
      =FORMULATEXT(G15)
      ```

      Esta fórmula muestra el mensaje &quot;Solo se permite facturar hasta 7 kg de equipaje&quot;. si la clase elegida es &quot;Economy&quot;; en caso contrario, deja en blanco el campo de mensaje.

**Funciones matemáticas:**

- SUM(): añade valores desde un rango de celdas especificado.

  Ejemplo: Cálculo del coste total de los artículos de un carro de compras.

  En la expresión de valor del campo &quot;coste total&quot;:
SUM(precio * cantidad)

  Esta fórmula supone que tiene campos separados para &quot;precio&quot; y &quot;cantidad&quot; de cada artículo. Los multiplica y utiliza SUM() para sumar el coste total de todos los artículos del carro de compras.

- ROUND(): redondea un número hasta un número determinado de decimales.

  Ejemplo: Redondear una cantidad de descuento calculada a dos decimales.

  En la expresión de valor del campo &quot;importe del descuento&quot; (suponiendo que un descuento se calcule en otra parte): 
ROUND(descuento, 2)

  Esta fórmula redondea el valor de descuento a dos decimales.

- MIN(): devuelve el valor más pequeño de un rango de celdas especificado.

  Ejemplo: Búsqueda de la edad mínima requerida para un formulario de suscripción basado en un país seleccionado.

  En la expresión de valor de un campo &quot;edad mínima&quot;:
MIN(ageLimits[&quot;US&quot;], ageLimits[&quot;UK&quot;], ageLimits[&quot;France&quot;])

  Esta fórmula supone que tiene una tabla denominada &quot;ageLimits&quot; que almacena los requisitos de edad mínimos para diferentes países. Utiliza MIN() para encontrar el valor más pequeño entre ellos.


Además, el bloque de formularios adaptables le permite hacerse cargo de los formularios al crear [funciones personalizadas](#creating-custom-functions). Las funciones personalizadas le permiten definir sus propias reglas y lógica, lo que le proporciona un control completo sobre el comportamiento de los formularios.


## Creación e implementación de funciones personalizadas

El bloque de formularios adaptables listo para usar (OOTB) proporciona implementaciones para muchas [funciones comunes de hoja de cálculo](#spreadsheet-functions-for-rules). Sin embargo, para un control más preciso sobre los formularios, puede utilizar cualquiera de las funciones OOTB disponibles en Microsoft® Excel o Google Sheets dentro de los bloques de formularios adaptables. El bloque de formularios adaptables no contiene implementación para todas las funciones OOTB disponibles en Microsoft® Excel o Google Sheets. Si necesita cualquiera de estas funciones, puede desarrollar una función personalizada con una sintaxis similar para lograr la funcionalidad que proporcionan Microsoft® Excel o Google Sheets. Por ejemplo, puede implementar la [función Year() de Microsoft® Excel](https://support.microsoft.com/es-es/office/calculate-age-113d599f-5fea-448f-a4c3-268927911b37#) para calcular la edad desde la fecha de nacimiento.


### Creación de una función personalizada

Las funciones personalizadas residen en el archivo `[Adaptive form block]/functions.js`. El proceso de creación suele incluir los siguientes pasos:

- Declaración de función: defina el nombre de la función y sus parámetros (las entradas que acepta).
- Implementación lógica: escriba el código que describe los cálculos o manipulaciones específicos realizados por la función.
- Exportación de funciones: haga que la función sea accesible dentro de las reglas exportándola desde el archivo correspondiente.

### Ejemplo: Función Year

En este ejemplo se muestran dos funciones personalizadas que imitan la función YEAR() de Microsoft® Excel para calcular la edad:


```JavaScript
/**
 - Get the current date and time
 - @name now
 - @returns {Date} The current date and time as a Date object
 */
function now() {
  const today = new Date();
  return today;
}

/**
 - Get the year from a Date object
 - @name year
 - @param {Date} date The date object
 - @throws {TypeError} If the input is not a Date object
 - @returns {number} The year as a number
 */
function year(date) {
  let inputDate = new Date(date)

  if (!(inputDate instanceof Date)) {
    throw new TypeError("Input must be a Date object");
  }

  const year = inputDate.getFullYear();

  return year;
}

// Make the function accessible for use in rules
export { now, year };
```

### Uso de una función personalizada en el formulario

Para utilizar la función personalizada en el formulario:

1. **Añada la función**: incluya la función personalizada en el archivo `[Adaptive form block]/functions.js`. Recuerde añadirla a la instrucción de exportación dentro del archivo.
1. **Implemente el archivo**: implemente el archivo `functions.js` actualizado en el proyecto de GitHub y compruebe que la compilación se ha realizado correctamente.
1. **Uso de la función**: acceda a la función dentro de la hoja de cálculo del formulario mediante las propiedades `Value`, `Value Expression`, `Visible` o `Visible Expression`, de forma similar a cualquier otra función de hoja de cálculo compatible con OOTB.
1. **Previsualice el formulario**: utilice la barra de tareas de AEM para obtener una vista previa del formulario con la función recién implementada.

