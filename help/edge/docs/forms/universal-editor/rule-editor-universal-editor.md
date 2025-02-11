---
title: Cómo utilizar el editor de reglas para aplicar reglas a los campos de formulario, lo que permite un comportamiento dinámico y una lógica compleja para los formularios creados con la creación de WYSIWYG
description: El editor de reglas de formularios adaptables permite añadir un comportamiento dinámico y generar una lógica compleja en los formularios sin codificación ni scripts.
feature: Edge Delivery Services
role: Admin, Architect, Developer
hide: true
hidefromtoc: true
exl-id: 846f56e1-3a98-4a69-b4f7-40ec99ceb348
source-git-commit: 0410e1d16ad26d3169c01cca3ad9040e3c4bfc9f
workflow-type: ht
source-wordcount: '2111'
ht-degree: 100%

---

# Introducción al Editor de reglas en el Editor universal

Puede añadir el comportamiento del formulario dinámico mediante el Editor de reglas, que le permite crear reglas. Estas reglas habilitan la visibilidad de campo condicional, automatizan los cálculos en función de los datos introducidos por el usuario y mejoran la experiencia general del usuario. Al optimizar el proceso de rellenado de formularios, el Editor de reglas garantiza tanto la precisión como la eficacia.

El Editor de reglas ofrece una interfaz visual intuitiva para crear y administrar reglas. Su enfoque fácil de usar lo hace accesible a todos los usuarios, incluso a aquellos sin amplia experiencia técnica, lo que les permite implementar la lógica sin esfuerzo dentro de sus formularios.

## Qué son las reglas

Las reglas son instrucciones que guían a los usuarios sobre qué acciones realizar en condiciones específicas.

* **Condición**: una condición es una comprobación o regla que evalúa si algo es verdadero o falso. Responde a la pregunta: &quot;¿Cumple esto el requisito?&quot;

* **Acción**: una acción es lo que sucede cuando la condición es verdadera. Es la tarea o el comportamiento activado en función de la evaluación de la condición.

Una regla suele seguir una de las siguientes construcciones:

* **Condición-acción**: compruebe primero una condición y luego realice una acción. En el editor de reglas, el tipo de regla `When` aplica la construcción `condition-action`.
* **Acción-Condición**: realice primero una acción y después compruebe una condición. Los tipos de reglas `Set Value Of` y `Validate` del editor de reglas aplican la construcción `action-condition`.
* **Acción-Condición-Acción alternativa**: realice una acción, compruebe una condición y, a continuación, realice la acción principal o una acción alternativa basada en la condición. Por ejemplo, de forma predeterminada, la acción alternativa para `Show` es `Hide` y para `Enable` es `Disable`.

Por ejemplo, una condición podría comprobar si un usuario ha introducido un determinado valor en un campo y la acción podría ser mostrar u ocultar un campo.
* **Condición**: comprobar si los ingresos son superiores a 50 000 $.
* **Acción**: si la condición es verdadera, muestre el campo `Additional Deduction`; de lo contrario, realice la acción alternativa: oculte el campo `Additional Deduction`.

Para obtener instrucciones detalladas paso a paso, consulte [agregar una regla de condición](#2-add-a-conditional-rule).

## ¿Cómo se habilita la extensión del Editor de reglas?

En el Editor universal, el Editor de reglas no está habilitado de forma predeterminada. Para habilitar la extensión del Editor de reglas para su entorno, envíe un correo electrónico desde su dirección oficial a [aem-forms-ea@adobe.com](mailto:aem-forms-ea@adobe.com) con su solicitud.

Una vez habilitada la extensión del Editor de reglas para su entorno, aparecerá el icono ![edit-rules](/help/forms/assets/edit-rules-icon.svg) en la esquina superior derecha del editor.

![Editor universal de reglas](/help/edge/docs/forms/assets/universal-editor-rule-editor.png)

Seleccione el objeto de formulario para el que desea escribir una regla y haga clic en el icono ![edit-rules](/help/forms/assets/edit-rules-icon.svg).  Aparecerá la interfaz de usuario del editor de reglas.

![Interfaz de usuario del Editor de reglas](/help/edge/docs/forms/assets/rule-editor-for-field.png)

Ahora puede empezar a escribir reglas o lógica empresarial para el campo de formulario seleccionado usando los [tipos de reglas disponibles en el Editor de reglas](#available-rule-types-in-rule-editor).

## Explicación de la interfaz de usuario del Editor de reglas

El editor visual del Editor de reglas se abrirá al hacer clic en el icono ![edit-rules](/help/forms/assets/edit-rules-icon.svg):

![Interfaz de usuario del Editor de reglas](/help/edge/docs/forms/assets/rule-editor-interface.png)

<table border="1">
  <thead>
    <tr>
      <th>Componente del Editor de reglas</th>
      <th>Descripción</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>1. Visualización de la regla del componente</td>
      <td>Muestra el título del objeto del formulario a través del cual se ha iniciado el Editor de reglas y el tipo de regla seleccionado actualmente. </td>
    </tr>
    <tr>
      <td>2. Objetos y funciones de formulario</td>
      <td>La pestaña <b>Objetos de formulario</b> muestra una vista jerárquica de todos los objetos contenidos en el formulario. La ficha <b>Funciones</b> incluye un conjunto de funciones integradas.</td>
    </tr>
    <tr>
      <td>3. Alternar entre funciones y objetos de formulario</td>
      <td>Al pulsar el botón de cambio, se alternan los paneles de funciones y de objetos de formulario.</td>
    </tr>
    <tr>
      <td>4. Editor de reglas visual</td>
      <td>El Editor de reglas visual es el área del modo de editor visual de la interfaz de usuario del Editor de reglas donde se escriben las reglas. </td>
    </tr>
    <tr>
      <td>5. Botones de finalización y cancelación</td>
      <td>El botón <b>Listo</b> se utiliza para guardar una regla. El botón <b>Cancelar</b> descarta los cambios realizados en una regla y cierra el Editor de reglas.</td>
    </tr>
  </tbody>
</table>

Cualquier regla existente en un objeto de formulario se muestra al seleccionar el objeto. Puede ver el título y una vista previa del resumen de reglas en el Editor de reglas visual. Además, puede cambiar el orden de las reglas, editarlas, habilitarlas o deshabilitarlas, o eliminarlas.

![mostrar las reglas disponibles del objeto de formulario](/help/edge/docs/forms/assets/rule-editor15.png)

## Tipos de regla disponibles

El Editor de reglas proporciona un conjunto de tipos de reglas predefinidas que puede utilizar para escribir reglas, como se muestra en la siguiente tabla: 

<table border="1">
  <thead>
    <tr>
      <th>Tipo de regla</th>
      <th>Descripción</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Establecer valor de</td>
      <td>Establece el valor de un objeto de formulario en función de si se cumple la condición especificada.</td>
    </tr>
    <tr>
      <td>Borrar valor de</td>
      <td>Borra el valor del objeto especificado.</td>
    </tr>
    <tr>
      <td>Ocultar/Mostrar</td>
      <td>Oculta o muestra un objeto de formulario en función de si se cumple o no una condición.</td>
    </tr>
    <tr>
      <td>Habilitar/Deshabilitar</td>
      <td>Habilita o deshabilita un objeto de formulario en función de si se cumple o no una condición.</td>
    </tr>
    <tr>
      <td>Validar</td>
      <td>Valida el formulario o un objeto especificado.</td>
    </tr>
    <tr>
      <td>Cuando </td>
      <td>Sigue la construcción de reglas de acción <i>condición-acción-alternativa</i> o la construcción de reglas <i>condición-acción</i>. Especifica una condición para la evaluación seguida de una acción que se activa si se cumple la condición.</td>
    </tr>
    <tr>
      <td>Formato</td>
      <td>Da formato a un objeto de formulario basado en una función o expresión regular.</td>
    </tr>
    <tr>
      <td>Invocar servicio</td>
      <td>Invoca un servicio configurado en un modelo de datos de formulario (FDM). </td>
    </tr>
    <tr>
      <td>Establecer propiedad</td>
      <td>Establece el valor de una propiedad del objeto especificado en función de una condición.</td>
    </tr>
    <tr>
      <td>Establecer enfoque</td>
      <td>Define el enfoque del objeto especificado.</td>
    </tr>
    <tr>
      <td>Guardar formulario</td>
      <td>Guarda el formulario.</td>
    </tr>
    <tr>
      <td>Enviar/Restablecer formulario</td>
      <td>Envía o restablece el formulario.</td>
    </tr>
    <tr>
      <td>Añadir/Quitar instancia</td>
      <td>Añade o quita una instancia del panel repetible o fila de tabla especificados.</td>
    </tr>
    <tr>
      <td>Navegar hasta</td>
      <td>Navega a otros formularios adaptables, otros recursos, como imágenes o fragmentos de documento, o una URL externa.</td>
    </tr>
    <tr>
      <td>Evento de envío</td>
      <td>Activa acciones específicas basadas en condiciones o eventos predefinidos.</td>
    </tr>
    <tr>
      <td>Navegar por los paneles</td>
      <td>Permite cambiar el enfoque entre diferentes paneles de un formulario.</td>
    </tr>
  </tbody>
</table>


Ahora, vamos a explorar cómo [escribir reglas en el Editor de reglas](#write-rules).

## Escribir reglas

Para comprender cómo escribir reglas en el Editor de reglas visual, veamos un ejemplo sencillo de un formulario de cálculo de impuestos:

![Ejemplo del Editor de reglas](/help/edge/docs/forms/assets/rule-editor-1.png)

En el formulario descrito anteriormente, el usuario introduce el salario bruto. En función de esta entrada, se muestra un campo condicional y se calcula el impuesto a pagar.

**Campos del formulario:**
* Salario bruto (entrada del usuario)
* Deducción adicional (campo condicional)
* Ingresos gravables (campo calculado)
* Impuestos a pagar (campo calculado)

**Regla de condición:**
* Condición: salario bruto > 50 000
* Acción: mostrar el campo Deducción adicional

**Reglas de cálculo:**

* Ingresos gravables = Salario bruto - Deducción adicional (si procede)
* Impuesto a pagar = Ingresos gravables * Tipo impositivo (para simplificar, supongamos un tipo fijo del 10 %)

Para escribir las reglas, realice los siguientes pasos:

### 1. Crear un formulario

Para crear un formulario en el Editor universal:

1. Abra un formulario en el Editor universal para editarlo.
1. Añada los siguientes componentes de formulario:
   * Formulario de cálculo de impuestos (título)
   * Salario bruto (entrada de texto)
   * Deducción adicional (entrada de texto)
   * Ingresos gravables (entrada de texto)
   * Impuestos a pagar (introducción de texto)
   * Enviar (botón Enviar)
1. Ocultar el campo de formulario `Additional Deduction` abriendo su `Properties`.

   ![Ejemplo del Editor de reglas](/help/edge/docs/forms/assets/rule-editor2.png)

### 2. Agregar una regla de condición para un campo de formulario

Una vez haya creado el formulario, escriba la primera regla para mostrar el campo `Additional Deduction` solo si el salario bruto supera los 50 000 $. Para añadir una regla de condición:

1. Abra un formulario en el Editor universal para editarlo.
1. Seleccione el componente **[!UICONTROL salario bruto]** en el árbol de contenido y seleccione ![edit-rules](/help/forms/assets/edit-rules-icon.svg).
   ![Ejemplo1 del Editor de reglas](/help/edge/docs/forms/assets/rule-editor3.png)
Aparecerá la interfaz visual del Editor de reglas.
1. A continuación, haga clic en **[!UICONTROL Crear]** para iniciar el Editor de reglas.
   ![Ejemplo2 del Editor de reglas](/help/edge/docs/forms/assets/rule-editor4.png)
De forma predeterminada, el tipo de regla `Set Value Of` está seleccionado. Aunque no puede cambiar ni modificar el objeto seleccionado, puede utilizar la lista desplegable de reglas para seleccionar otro tipo de regla. \
   ![Ejemplo3 del Editor de reglas](/help/edge/docs/forms/assets/rule-editor5.png)
1. Abra la lista desplegable de tipo de regla y seleccione el tipo de regla **[!UICONTROL Cuando]**.
   ![Ejemplo4 del Editor de reglas](/help/edge/docs/forms/assets/rule-editor6.png)
1. Seleccione el menú desplegable **[!UICONTROL Seleccionar estado]** y seleccione **[!UICONTROL es superior a]**. Aparece el campo **[!UICONTROL Escribir un número]**.
   ![Ejemplo5 del Editor de reglas](/help/edge/docs/forms/assets/rule-editor7.png)
1. Escriba `50000` en el campo **[!UICONTROL Escribir un número]** en la regla.
   ![Ejemplo6 del Editor de reglas](/help/edge/docs/forms/assets/rule-editor8.png)
Ha definido la condición como `When Gross Salary is greater than 50000`. A continuación, defina la acción que se realizará si esta condición es `True`.
1. En la instrucción `Then`, seleccione **[!UICONTROL Mostrar]** en el menú desplegable **[!UICONTROL Seleccionar acción]**.
   ![Ejemplo7 del Editor de reglas](/help/edge/docs/forms/assets/rule-editor9.png)
1. Arrastre y suelte el campo **[!UICONTROL Deducción adicional]** de la pestaña Objetos de formulario en el campo **[!UICONTROL Soltar objeto o seleccionar aquí]**. Como alternativa, seleccione el campo **[!UICONTROL Soltar objeto o seleccionar aquí]** y seleccione el campo **[!UICONTROL Deducción adicional]** en el menú emergente, que muestra todos los objetos del formulario.
   ![Ejemplo8 del Editor de reglas](/help/edge/docs/forms/assets/rule-editor10.png)
1. Haga clic en **[!UICONTROL Añadir la sección O]** para añadir otra condición para el campo **[!UICONTROL Salario bruto]**, en caso de que especifique un salario inferior a `50000`.
   ![Ejemplo9 del Editor de reglas](/help/edge/docs/forms/assets/rule-editor11.png)
1. Seleccione **[!UICONTROL Ocultar]** del menú desplegable **[!UICONTROL Seleccionar acción]** en la instrucción `Else`.
   ![Ejemplo10 del Editor de reglas](/help/edge/docs/forms/assets/rule-editor12.png)
1. Arrastre y suelte el campo **[!UICONTROL Deducción adicional]** de la pestaña Objetos de formulario en el campo **[!UICONTROL Soltar objeto o seleccionar aquí]**. Como alternativa, seleccione el campo **[!UICONTROL Soltar objeto o seleccionar aquí]** y seleccione el campo **[!UICONTROL Deducción adicional]** en el menú emergente, que muestra todos los objetos del formulario.
   ![Ejemplo11 del Editor de reglas](/help/edge/docs/forms/assets/rule-editor13.png)
1. Seleccione **[!UICONTROL Listo]** para guardar la regla.
La regla aparece de la siguiente manera en el Editor de reglas.
   ![Ejemplo12 del Editor de reglas](/help/edge/docs/forms/assets/rule-editor14.png)

>[!NOTE]
>
> Como alternativa, puede escribir una regla Show en el campo Deducción adicional, en lugar de una regla When en el campo Salario bruto, para implementar el mismo comportamiento.

### 3. Añadir reglas de cálculo para los campos de formulario

A continuación, escriba una regla para calcular `Taxable Income`, que es la diferencia entre `Gross Salary` y `Additional Deduction` (si corresponde). Para añadir una regla de cálculo en el campo **[!UICONTROL Ingresos gravables]**, realice los siguientes pasos:

1. En el modo de creación, seleccione el campo **[!UICONTROL Ingresos gravables]** y seleccione el icono ![edit-rules](/help/forms/assets/edit-rules-icon.svg). A continuación, seleccione **[!UICONTROL Crear]** para iniciar el Editor de reglas.
   ![Ejemplo13 del Editor de reglas](/help/edge/docs/forms/assets/rule-editor16.png)
1. Seleccione **[!UICONTROL Seleccionar opción]** y seleccione **[!UICONTROL Expresión matemática]**. Se abre un campo para escribir una expresión matemática.
   ![Ejemplo14 del Editor de reglas](/help/edge/docs/forms/assets/rule-editor17.png)

1. En el campo de la expresión matemática:

   * Seleccione o arrastre y suelte desde la pestaña Objeto de formularios el campo **[!UICONTROL Salario bruto]** en el primer campo **[!UICONTROL Soltar objeto o seleccionar aquí]**.

   * Seleccione **[!UICONTROL Menos]** en el campo **[!UICONTROL Seleccionar operador]**.

   * Seleccione o arrastre y suelte desde la pestaña Objeto de formularios el campo **[!UICONTROL Deducción adicional]** en el otro campo **[!UICONTROL Soltar objeto o seleccionar aquí]**.
     ![Ejemplo15 del Editor de reglas](/help/edge/docs/forms/assets/rule-editor18.png)

1. Seleccione **[!UICONTROL Listo]** para guardar la regla.

   Ahora, añada una regla para el campo `Tax Payable `, que se determina multiplicando los ingresos gravables por la tasa de impuestos. Para simplificar, suponga una tasa de impuestos fija de `10%`.

1. En el modo de creación, seleccione el campo **[!UICONTROL Ingresos gravables]** y seleccione el icono ![edit-rules](/help/forms/assets/edit-rules-icon.svg). A continuación, seleccione **[!UICONTROL Crear]** para iniciar el editor de reglas.
   ![Ejemplo16 del Editor de reglas](/help/edge/docs/forms/assets/rule-editor19.png)
1. Seleccione **[!UICONTROL Seleccionar opción]** y seleccione **[!UICONTROL Expresión matemática]**. Se abre un campo para escribir una expresión matemática.
   ![Ejemplo del editor de reglas17](/help/edge/docs/forms/assets/rule-editor20.png)
1. En el campo de la expresión matemática:

   * Seleccione o arrastre y suelte desde la pestaña Objeto de formularios el campo **[!UICONTROL Ingresos gravables]** en el primer campo **[!UICONTROL Soltar objeto o seleccionar aquí]**.

   * Seleccione **[!UICONTROL Multiplicado por]** en el campo **[!UICONTROL Seleccionar operador]**.

   * Seleccione **Número** del campo **[!UICONTROL Seleccionar opción]** e introduzca el valor como `10` en el campo **[!UICONTROL Escribir un número]**.
     ![Ejemplo18 del Editor de reglas](/help/edge/docs/forms/assets/rule-editor21.png)
1. A continuación, seleccione el área resaltada alrededor del campo de expresión y haga clic en **[!UICONTROL Ampliar expresión]**.
   ![Ejemplo19 del Editor de reglas](/help/edge/docs/forms/assets/rule-editor22.png)
1. En el campo para ampliar la expresión, seleccione **[!UICONTROL divided by]** en el campo **[!UICONTROL Seleccionar operador]** y **[!UICONTROL Número]** en el campo **[!UICONTROL Seleccionar opción]**. A continuación, especifique `100` en el campo de número.
   ![Ejemplo20 del Editor de reglas](/help/edge/docs/forms/assets/rule-editor23.png)
1. Seleccione **[!UICONTROL Listo]** para guardar la regla.

### 4. Previsualizar un formulario

Ahora, al obtener una vista previa del formulario e introducir el **Salario bruto** como `60,000`, aparecerá el campo **Deducción adicional**, y se calcularán en consecuencia los **Ingresos gravables** e **Impuestos por pagar**.

![Seleccionar un formulario](/help/edge/docs/forms/assets/rule-editor-form.png)

Aparte de las funciones integradas, como Suma, Promedio, que se muestran en Salida de funciones, puede [escribir funciones personalizadas](#create-a-custom-function) que necesite con frecuencia. 

## Funciones personalizadas en el Editor de reglas

Los formularios de Edge Delivery Services admiten funciones personalizadas, que permiten a los usuarios definir funciones de JavaScript para implementar reglas empresariales complejas. Las funciones personalizadas amplían las capacidades de los formularios al facilitar la manipulación y el procesamiento de los datos introducidos para satisfacer requisitos específicos.

### Creación de una función personalizada

Para crear funciones personalizadas, edite el archivo `../[blocks]/form/functions.js`. El proceso de creación suele incluir los siguientes pasos:

* **Declaración de función**: defina el nombre de la función y sus parámetros (las entradas que acepta).
* **Implementación lógica**: escriba el código que describe los cálculos o manipulaciones específicos realizados por la función.
* **Exportación de funciones**: haga que la función sea accesible dentro de las reglas exportándola desde el archivo correspondiente.


Este ejemplo muestra dos funciones personalizadas como `getFullName` y `days`:

```JavaScript
/**
 * Get Full Name
 * @name getFullName Concats first name and last name
 * @param {string} firstname in Stringformat
 * @param {string} lastname in Stringformat
 * @return {string}
 */
function getFullName(firstname, lastname) {
  return `${firstname} ${lastname}`.trim();
}

/**
 * Calculate the number of days between two dates.
 * @param {*} endDate
 * @param {*} startDate
 * @name days Calculates the numebr of days between two dates
 * @returns {number} returns the number of days between two dates
 */
function days(endDate, startDate) {
  const start = typeof startDate === 'string' ? new Date(startDate) : startDate;
  const end = typeof endDate === 'string' ? new Date(endDate) : endDate;

  // return zero if dates are valid
  if (Number.isNaN(start.getTime()) || Number.isNaN(end.getTime())) {
    return 0;
  }

  const diffInMs = Math.abs(end.getTime() - start.getTime());
  return Math.floor(diffInMs / (1000 * 60 * 60 * 24));
}

// eslint-disable-next-line import/prefer-default-export
export { getFullName, days };
```
![Añadir una función personalizada](/help/edge/docs/forms/assets/create-custom-function.png)

### Uso de una función personalizada en el Editor de reglas

Para utilizar la función personalizada en el Editor de Reglas:

1. **Añadir la función**: incluya la función personalizada en el archivo `../[blocks]/form/functions.js`. Recuerde añadirla a la instrucción de `export` dentro del archivo.
1. **Implementar el archivo**: implemente el archivo `functions.js` actualizado en el proyecto de GitHub y compruebe que la compilación se ha realizado correctamente.
1. **Uso de funciones**: Para acceder a la función desde el Editor de reglas del formulario, seleccione la opción `Function Output` en el campo **[!UICONTROL Seleccionar acción]**.

   ![Funciones personalizadas en el Editor de reglas](/help/edge/docs/forms/assets/custom-function-rule-editor.png)

1. **Previsualizar el formulario**: obtenga una vista previa del formulario con la función recién implementada.

## Artículos relacionados

{{see-also-rule-editor}}

## Consulte también

* [Introducción a Edge Delivery Services para AEM Forms](/help/edge/docs/forms/tutorial.md)
* [Crear un formulario con Google Sheets o Microsoft Excel](/help/edge/docs/forms/create-forms.md)
* [Configurar Google Sheets o los archivos de Microsoft Excel para empezar a aceptar datos](/help/edge/docs/forms/submit-forms.md)
* [Publicar el formulario y empezar a recopilar datos](/help/edge/docs/forms/publish-forms.md)
* [Personalizar el aspecto de los formularios](/help/edge/docs/forms/style-theme-forms.md)
* [Añadir secciones repetibles a un formulario](/help/edge/docs/forms/repeatable-forms.md)
* [Mostrar un mensaje de agradecimiento personalizado después del envío del formulario](/help/edge/docs/forms/thank-you-page-form.md)
* [Componentes de bloque de formulario adaptable y sus propiedades](/help/edge/docs/forms/form-components.md)
* [Monitorización de usuarios reales](https://www.aem.live/developer/rum#authentication)
