---
title: Este artículo describe varios casos de uso para un editor de reglas en un formulario adaptable basado en componentes principales.
description: El artículo describe varios casos de uso para un editor de reglas en un formulario adaptable basado en componentes principales.
feature: Adaptive Forms, Core Components
role: User, Developer
level: Beginner, Intermediate
exl-id: 8191e113-f768-4b1e-a191-e3c722f19054
source-git-commit: bcf8f9e5273819eaee09875ec81251fe4330701c
workflow-type: tm+mt
source-wordcount: '1561'
ht-degree: 42%

---

# Diferentes casos de uso del Editor de reglas

El artículo proporciona ejemplos detallados del Editor de reglas para un formulario adaptable basado en componentes principales, y proporciona perspectivas sobre su implementación adecuada para diferentes escenarios. El editor de reglas permite a los desarrolladores definir y administrar la lógica que controla el comportamiento de los formularios.
Ahora, analicemos las diferentes implementaciones de un editor de reglas.

## Definir el enfoque en otro panel al hacer clic en el botón si el primer panel es válido

<span class="preview"> Esta es una función previa al lanzamiento y se puede acceder a ella a través de nuestro [canal previo al lanzamiento](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/prerelease.html?lang=es#new-features). </span>

El editor de reglas permite validar diseños de panel, como pestañas horizontales, pestañas verticales, acordeones o el asistente al hacer clic en un botón y establecer el enfoque en un objeto de formulario en otro panel. Puede utilizar esta funcionalidad para mejorar la navegación del formulario y la experiencia del usuario.

Imagine un formulario de aplicación de varios pasos con un diseño Asistente. Debe completar el panel `Personal Information` antes de pasar a `Employment Details`. Al hacer clic en el botón `Next`, el editor de reglas valida el panel `Personal Information`. Si todos los campos obligatorios se rellenan correctamente, el formulario cambiará automáticamente el enfoque al panel `Employment Details`. De lo contrario, muestra un mensaje de error que pide a los usuarios que completen los campos que faltan.

Puede crear una regla en el botón `Next` para validar el primer panel:

![Regla para el botón Siguiente](/help/forms/assets/next-rule.png){width=50%}

Al hacer clic en el botón **Siguiente**, se valida el panel **Información personal**. Si los detalles introducidos son correctos, el enfoque cambia al panel **Seguridad de la cuenta**; de lo contrario, un mensaje de error le pedirá que rellene los detalles que faltan.

<!--![Video]()-->

## Desplazamiento entre paneles mediante el botón

El editor de reglas permite agregar botones de navegación a los diseños de panel, como pestañas horizontales, pestañas verticales, acordeones o asistente. Estos botones mejoran la experiencia del usuario al simplificar las transiciones entre los distintos paneles de un formulario, desplazando el enfoque al panel seleccionado.

Imagine que está interactuando con la sección de configuración de perfil de una aplicación, donde la navegación se facilita mediante botones en lugar de pestañas. Al ingresar la configuración del perfil desde el panel principal, se encuentra con una serie de paneles dedicados a diferentes aspectos de su perfil: **Información personal**, **Seguridad de la cuenta** y **Preferencias de notificación**.

Cada panel contiene campos y opciones relevantes para actualizar información específica. Los botones de navegación, como `Next` y `Back`, están colocados de forma destacada para permitirle moverse entre estos paneles. Haga clic en `Next` para avanzar al usuario al panel **Seguridad de la cuenta** y haga clic en `Back` para volver al panel **Información personal**. Este método de navegación garantiza una transición sin problemas entre secciones sin perder contexto, lo que proporciona una experiencia de usuario fluida e intuitiva. El uso de botones de navegación simplifica el proceso de administración de la configuración del perfil, lo que hace que la interacción sea más organizada y fácil de usar.

Puede usar la regla `Navigate among the panels` para crear reglas de navegación para botones que permitan cambiar entre paneles diferentes.  Seleccione el atributo `Shift focus to the next item` para mover el enfoque al siguiente panel del diseño.

![Regla del panel siguiente](/help/forms/assets/rule-editor-navigate-in-panel-next.png){width=50%}

Cuando se hace clic en el botón `Next`, el enfoque se desplaza al panel siguiente del diseño.

![Desplazarse por el panel utilizando el botón Siguiente](/help/forms/assets/navigate-in-panel.gif)

Del mismo modo, puede crear una regla para el botón `Previous` para desplazar el enfoque al panel anterior.

![Regla de panel anterior](/help/forms/assets/rule-editor-navigate-in-panel-previous.png){width=50%}

## Optimización de cálculos complejos en paneles repetibles con funciones

El editor de reglas permite utilizar funciones integradas, como Suma, Mín, Máx y Unir, directamente en los campos de los paneles repetibles. También puede pasar un valor de campo de panel repetible a la función que acepte matriz de números, matriz de cadenas, matriz booleana, etc. Esto desbloquea una potente automatización, lo que le permite implementar una lógica empresarial compleja sin código personalizado.

Imagine un formulario con un panel repetible, donde cada instancia del panel recopila información sobre el valor declarado de los recursos.

![Formulario repetible](/help/forms/assets/ootb-function-support-repeatable-panel-form.png)

Puede usar la función `Sum` para calcular automáticamente el valor de los recursos totales en todos los paneles, lo que elimina la necesidad de realizar cálculos manuales y reduce la posibilidad de que se produzcan errores.

![Compatibilidad con campos de panel repetibles en funciones OOTB](/help/forms/assets/ootb-function-support-repeatable-panel.png)

Cuando rellena un formulario y agrega instancias para declarar los valores de los recursos, el botón `Calculate Asset Value` calcula la suma total de todos los valores de recursos declarados y muestra el resultado en el cuadro de texto total de `assetvalue`.

![Compatibilidad con campos de panel repetibles en funciones OOTB](/help/forms/assets/ootb-function-support-repeatable-panel-form-preview.png)

>[!NOTE]
>
> Si el valor del campo del panel repetible se pasa a una función que no acepta una matriz, el valor del campo de la última instancia del panel repetible se pasa a la función.

¡Este es solo un ejemplo! Explore las [funciones](#b-form-objects-and-functions-br) disponibles para simplificar los flujos de trabajo y mejorar la precisión de los datos en los formularios.

## Expresiones anidadas {#nestedexpressions}

El editor de reglas permite utilizar varios operadores AND y OR para crear reglas anidadas. Puede combinar varios operadores AND y OR en las reglas.

A continuación se muestra un ejemplo de una regla anidada que muestra un mensaje al usuario sobre la elegibilidad para la custodia de un niño cuando se cumplen las condiciones requeridas.

![Expresión compleja](assets/complexexpression.png)

También puede arrastrar y soltar condiciones dentro de una regla para editarla. Seleccione y pase el ratón por encima del controlador (![controlador](assets/drag-handle.svg)) antes de una condición. Una vez que el puntero se convierta en el símbolo de mano como se muestra a continuación, arrastre y suelte la condición en cualquier lugar dentro de la regla. La estructura de la regla cambia.

![Arrastrar y soltar](assets/drag-and-drop.png)

## Condiciones de expresión de fecha {#dateexpression}

El editor de reglas permite usar comparaciones de fechas para crear condiciones.

A continuación se muestra una condición de ejemplo que muestra un objeto de texto estático si la hipoteca de la casa ya está cogida, lo que el usuario indica rellenando el campo de la fecha.

Cuando la fecha de la hipoteca de la propiedad tal como la ha rellenado el usuario es anterior, el formulario adaptable muestra una nota sobre el cálculo de ingresos. La siguiente regla compara la fecha rellenada por el usuario con la fecha actual y si la fecha rellenada por el usuario es anterior a la fecha actual, el formulario muestra el mensaje de texto, denominada Income (ingresos).

![Condición de expresión de fecha](assets/dateexpressioncondition.png)

Cuando la fecha de rellenado es anterior a la fecha actual, el formulario muestra el mensaje de texto (Income) de la siguiente manera:

![Se cumple la condición de expresión de fecha](assets/dateexpressionconditionmet.png)

## Condiciones de comparación de números {#number-comparison-conditions}

El editor de reglas permite crear condiciones que comparen dos números.

A continuación verá una condición de ejemplo que muestra un objeto de texto estático si el número de meses que un solicitante permanece en la dirección actual es inferior a 36.

![Condición de comparación de números](assets/numbercomparisoncondition.png)

Si el usuario indica que lleva menos de 36 meses viviendo en su actual domicilio, el formulario muestra una notificación en la que se indica que se pueden solicitar más pruebas de residencia.

![Se solicitan más pruebas](assets/additionalproofrequested.png)

<!-- ## Impact of rule editor on existing scripts {#impact-of-rule-editor-on-existing-scripts}

In [!DNL Experience Manager Forms] versions prior to [!DNL Experience Manager 6.1 Forms] feature pack 1, form authors and developers used to write expressions in the Scripts tab of the Edit component dialog to add dynamic behavior to Adaptive Forms. The Scripts tab is now replaced by the rule editor.

Any scripts or expressions that you must have written in the Scripts tab are available in the rule editor. While you cannot view or edit them in visual editor, if you are a part of the forms-power-users group you can edit scripts in code editor. -->

### Invocar servicio de modelo de datos de formulario {#invoke}

Piense en un servicio web `GetInterestRates` que toma el importe del préstamo, el ejercicio y la puntuación crediticia del solicitante como entrada y devuelve un plan de préstamo que incluye el importe del EMI y el tipo de interés. Puede crear un modelo de datos de formulario (FDM) utilizando el servicio web como fuente de datos. Se agregan objetos del modelo de datos y un servicio `get` al modelo de formulario. El servicio aparece en la pestaña Servicios del modelo de datos de formulario (FDM). A continuación, cree un formulario adaptable que incluya campos de los objetos del modelo de datos para capturar las entradas del usuario para el importe del préstamo, el ejercicio y la puntuación crediticia. Agregue un botón que active el servicio web para obtener detalles del plan. La salida se rellena en los campos adecuados.

La regla siguiente muestra cómo configurar la acción Invocar servicio para que se realice el escenario de ejemplo.

![Example-invoke-services](assets/example-invoke-services.png)

>[!NOTE]
>
>Si la entrada es de tipo matriz, los campos que admiten matrices se pueden ver en la sección desplegable Output.

### Activación de varias acciones mediante la regla When {#triggering-multiple-actions-using-the-when-rule}

En un formulario de solicitud de préstamo, se desea capturar si el solicitante del préstamo es o no un cliente existente. En función de la información que proporcione el usuario, el campo ID de cliente debería mostrarse u ocultarse. Además, desea centrarse en el campo ID del cliente si el usuario es un cliente existente. El formulario de solicitud de préstamo tiene los siguientes componentes:

* Un botón de opción, **[!UICONTROL Are you an existing Geometrixx customer? (¿Es cliente de Geometrixx?)]**, que proporciona las opciones [!UICONTROL Yes] (sí) y [!UICONTROL No]. El valor de Yes es **0** y No es **1**.

* Un campo de texto, **[!UICONTROL Geometrixx customer ID]** (ID de cliente de Geometrixx), para especificar el ID de cliente.

Cuando escriba una regla When en el botón de radio para implementar este comportamiento, la regla aparecerá de la siguiente manera en el editor de reglas visuales.

![When-rule-example](assets/when-rule-example.png)

En la regla de ejemplo, la instrucción de la sección When es la condición que, cuando devuelve el valor True, ejecuta las acciones especificadas en la sección Then.

<!-- The rule appears as follows in the code editor.

![when-rule-example-code](assets/when-rule-example-code.png) 

Rule in the code editor -->

### Uso de una salida de función en una regla {#using-a-function-output-in-a-rule}

En un formulario de pedido de compra, tiene la siguiente tabla, en la que los usuarios rellenan sus pedidos. En esta tabla:

* La primera fila es repetible, por lo que los usuarios pueden solicitar varios productos y especificar cantidades diferentes. Su nombre de elemento es `Row1`.
* El título de la celda de la columna Product Quantity (cantidad de producto) de la fila repetible es Quantity (cantidad). El nombre de elemento de esta celda es `productquantity`.
* La segunda fila de la tabla es no repetible y el título de la celda de la columna Product Quantity de esta fila es Total Quantity (cantidad total).

![Example-function-table](assets/example-function-table.png)

**A.** Row1 **B.** Quantity **C.** Total Quantity

Ahora, desea agregar cantidades especificadas en la columna Product Quantity para todos los productos y mostrar la suma en la celda Total Quantity. Puede obtener esta suma escribiendo una regla Set Value Of en la celda Total Quantity como se muestra a continuación.

![Example-function-output](assets/example-function-output.png)

### Validación de un valor de campo mediante una expresión {#validating-a-field-value-using-expression}

En el formulario de pedido de compra que se explica en el ejemplo anterior, se desea restringir el pedido de más de una cantidad de cualquier producto con un precio superior al 10000. Para realizar esta validación, puede escribir una regla de validación como se muestra a continuación.

![Example-validate](assets/example-validate.png)

## Véase también

{{see-also-rule-editor}}
