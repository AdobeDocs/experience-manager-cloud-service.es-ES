---
title: Expresiones de formulario adaptables
seo-title: Adaptive Form Expressions
description: Utilice expresiones de Forms adaptables para añadir validación automática, cálculo y activar o desactivar la visibilidad de una sección.
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '2696'
ht-degree: 0%

---


# Expresiones de formulario adaptables {#adaptive-form-expressions}

Adaptive Forms ofrece una experiencia de cumplimentación de formularios optimizada y simplificada para los usuarios finales con funciones de secuencias de comandos dinámicas. Permite escribir expresiones para añadir varios comportamientos, como mostrar u ocultar campos y paneles dinámicos. También permite agregar campos calculados, hacer campos de solo lectura, agregar lógica de validación y muchos más. El comportamiento dinámico se basa en los datos introducidos por el usuario o rellenados previamente.

JavaScript™ es el lenguaje de expresión de Forms adaptable. Todas las expresiones son expresiones JavaScript™ válidas y utilizan API del modelo de secuencias de comandos de Forms adaptable. Estas expresiones devuelven valores de ciertos tipos. Para obtener la lista completa de clases, eventos, objetos y API públicas de Forms adaptable, consulte [Referencia de la API de la biblioteca JavaScript™ para Forms adaptable](https://helpx.adobe.com/experience-manager/6-5/forms/javascript-api/index.html).

## Prácticas recomendadas para escribir expresiones {#best-practices-for-writing-expressions}

* Al escribir expresiones, para acceder a campos y paneles, puede utilizar el nombre del campo o panel. Para acceder al valor de un campo, utilice la propiedad value . Por ejemplo, `field1.value`
* Utilice nombres únicos para campos y paneles de todo el formulario. Ayuda a evitar posibles conflictos con los nombres de campo utilizados al escribir expresiones.
* Cuando escriba expresiones de varias líneas, utilice un punto y coma para finalizar una instrucción.

## Prácticas recomendadas para expresiones que implican un panel de repetición {#best-practices-for-expressions-involving-repeating-panel}

Los paneles de repetición son instancias de un panel que se añaden o eliminan dinámicamente mediante API de secuencias de comandos o datos rellenados previamente. <!--  For detailed information about using repeating panel, see [creating forms with repeatable sections](creating-forms-repeatable-sections.md). -->

* Para crear un panel de repetición, en el cuadro de diálogo del panel, abra la configuración y establezca el valor del campo de recuento máximo en más de 1.
* El valor de recuento mínimo de la configuración de repetición del panel puede ser uno o más, pero no puede ser superior al valor de recuento máximo.
* Cuando una expresión hace referencia a un campo de panel de repetición, los nombres de campo de la expresión se resuelven en el elemento de repetición más cercano.
* Adaptive Forms proporciona algunas funciones especiales para simplificar el cálculo de paneles repetibles, como suma, recuento, mínimo, máximo, filtro y muchas más. Para obtener la lista completa de funciones, consulte [Referencia de la API de la biblioteca JavaScript™ para Forms adaptable](https://helpx.adobe.com/aem-forms/6/javascript-api/af.html)
* Las API para manipular instancias de panel repetitivo son:

   * Para añadir una instancia de panel: `panel1.instanceManager.addInstance()`
   * Para obtener un índice de repetición de panel: `panel1.instanceIndex`
   * Para obtener el instanceManager de un panel: `_panel1 or panel1.instanceManager`
   * Para quitar una instancia de un panel: `_panel1.removeInstance(panel1.instanceIndex)`

## Tipos de expresión {#expression-types}

En Forms adaptable, puede escribir expresiones para añadir comportamientos como mostrar/ocultar campos y paneles dinámicos. También puede escribir expresiones para agregar campos calculados, convertir campos en de solo lectura, lógica de validación y muchos más. Forms adaptable admite las expresiones siguientes:

* **[Expresiones de acceso](#access-expression-enablement-expression)**: para activar o desactivar un campo.
* **[Calcular expresiones](#calculate-expression)**: para calcular automáticamente el valor de un campo.
* **[Expresión de clics](#click-expression)**: para controlar las acciones al hacer clic en un botón.
* **[Secuencia de comandos de inicialización](#initialization-script):** realice una acción sobre la inicialización de un campo.
* **[Expresión de opciones](#options-expression)**: para rellenar dinámicamente una lista desplegable.
* **[Expresión de resumen](#summary)**: para calcular dinámicamente el título de un acordeón.
* **[Validar expresiones](#validate-expression)**: para validar un campo.
* **[Secuencia de comandos de confirmación de valor](#value-commit-script):** para cambiar los componentes de un formulario después de cambiar el valor de un campo.
* **[Expresión de visibilidad](#visibility-expression)**: para controlar la visibilidad de un campo y un panel.
* **[Expresión de finalización de paso](#step-completion-expression)**: para evitar que un usuario vaya al siguiente paso de un asistente.

### Expresión de acceso (expresión de habilitación) {#access-expression-enablement-expression}

Puede utilizar la expresión access para habilitar o deshabilitar un campo. Si la expresión utiliza el valor de un campo, cada vez que cambie el valor del campo, se recuperará la expresión.

**Se aplica a**: campos

**Tipo de devolución**: La expresión devuelve un valor booleano, que representa si el campo está habilitado o deshabilitado. **true** representa que el campo está habilitado y **false** representa el campo desactivado.

**Ejemplo**: Para habilitar un campo solo cuando el valor de **field1** está configurado como **X**, la expresión de acceso es: `field1.value == "X"`

### Calcular expresión {#calculate-expression}

La expresión calculate se utiliza para calcular automáticamente el valor de un campo mediante una expresión. Normalmente, esta expresión utiliza la propiedad value de otros campos. Por ejemplo, `field2.value + field3.value`. Valor siempre de la variable `field2`o `field3`cambia, se recupera la expresión y se vuelve a calcular el valor.

**Se aplica a**: campos

**Tipo de devolución**: La expresión devuelve un valor compatible con el campo en el que se muestra el resultado de la expresión (por ejemplo, decimal).

**Ejemplo**: La expresión calculate para mostrar la suma de dos campos en **field1** es:
`field2.value + field3.value`

### Expresión de clic {#click-expression}

La expresión click gestiona las acciones realizadas en el suceso click de un botón. De serie, GuideBridge proporciona API para realizar diversas funciones, como enviar y validar, que se utilizan junto con la expresión de clic. Para obtener una lista completa de las API, consulte [API de GuideBridge](https://helpx.adobe.com/aem-forms/6/javascript-api/GuideBridge.html).

**Se aplica a**: Campos de botón

**Tipo de devolución**: La expresión click no devuelve ningún valor. Si alguna expresión devuelve un valor, se ignora el valor.

**Ejemplo**: Rellenado de un cuadro de texto **textbox1** en la acción click de un botón con valor **AEM Forms**, la expresión de clic del botón es `textbox1.value="AEM Forms"`

### Script de inicialización {#initialization-script}

La secuencia de comandos de inicialización se activa cuando se inicializa un formulario adaptable. Según los escenarios, la secuencia de comandos de inicialización se comporta de la siguiente manera:

* Cuando se procesa un formulario adaptable sin un relleno previo de datos, la secuencia de comandos de inicialización se ejecuta después de que se inicialice el formulario.
* Cuando se procesa un formulario adaptable con un relleno previo de datos, la secuencia de comandos se ejecuta una vez finalizada la operación de rellenado previo.
* Cuando se activa la revalidación del lado del servidor de un formulario adaptable, se ejecuta la secuencia de comandos de inicialización.

**Se aplica a:** campos y panel

**Tipo de devolución:** La expresión de secuencia de comandos de inicialización no devuelve ningún valor. Si alguna expresión devuelve un valor, se ignora el valor.

**Ejemplo:** En un escenario de rellenado previo de datos, para rellenar campos con valor predeterminado `'Adaptive Forms'` cuando su valor se guarda como nulo, la expresión de secuencia de comandos de inicialización es:
`if(this.value==null) this.value='Adaptive Forms';`

### Expresión de opciones {#options-expression}

La expresión options se utiliza para rellenar dinámicamente las opciones de un campo de lista desplegable.

**Se aplica a**: campos de lista desplegable

**Tipo de devolución**: La expresión options devuelve una matriz de valores de cadena. Cada valor puede ser una cadena simple, como **Hombre**, o en un formato de par clave-valor, como **1=Hombre**

**Ejemplo**: Para rellenar el valor de un campo, en función del valor de otro campo, proporcione una expresión de opciones simple. Por ejemplo, para rellenar un campo, **Número de niños**, en función de la variable **Estado civil** expresado en otro campo, la expresión es:

**`marital_status.value == "married" ? ["1=One", "2=two"] : ["0=Zero"]`.**

Siempre que el valor de **marital_status** cambia, se recupera la expresión. También puede rellenar el menú desplegable desde un servicio REST. <!-- For detailed information, see [Dynamically populating dropdowns](dynamically-populate-dropdowns.md). -->

### Expresión de resumen {#summary}

La expresión Resumen calcula dinámicamente el título de un panel secundario de un panel de diseño de acordeón. Puede especificar la expresión Resumen en una regla, que utiliza un campo de formulario o una lógica personalizada para evaluar el título. La expresión se ejecuta cuando se inicializa el formulario. Si va a incluir un formulario como prefijo, la expresión se ejecuta después de que los datos se hayan rellenado previamente o cuando cambie el valor de los campos dependientes utilizados en la expresión.

La expresión Resumen se utiliza generalmente para repetir elementos secundarios de un panel de diseño de acordeón para proporcionar un título significativo a cada panel secundario.

**Se aplica a:** Paneles que son secundarios directos de un panel cuyo diseño está configurado como acordeón.

**Tipo de devolución:** La expresión devuelve un valor String que se convierte en el título del acordeón.

**Ejemplo:** &quot;Número de cuenta : &quot;+ textbox1.value

### Validar expresión {#validate-expression}

La expresión validate se utiliza para validar los campos utilizando la expresión dada. Normalmente, estas expresiones utilizan expresiones regulares junto con el valor del campo para validar un campo. La expresión se recupera y el estado de validación del campo se vuelve a calcular en cualquier cambio en el valor de un campo.

**Se aplica a**: campos

**Tipo de devolución**: La expresión devuelve un valor booleano, que representa el estado de validación del campo. El valor **false** representa que el campo no es válido y **true** representa que el campo es válido.
**Ejemplo**: Para un campo que representa el código postal del Reino Unido, la expresión de validación es:

(**this.value** &amp;&amp; `this.value.match(/^(GIR 0AA|[A-Z]{1,2}\d[A-Z0-9]? ?[0-9][A-Z]{2}\s*)$/i) == null) ? false : true`

En el ejemplo anterior, si el valor no vacío no coincide con el patrón, la expresión devuelve **false** para indicar que el campo no es válido.

>[!NOTE]
>
>Si escribe una expresión de validación para un campo no obligatorio u obligatorio, la expresión se evalúa independientemente del estado de visibilidad del campo. Para detener la validación de los campos ocultos, establezca la propiedad validationsDisabled en el script de inicialización o confirmación de valor en true. Por ejemplo, `this.validationsDisabled=true`

### Script de implementación de valor {#value-commit-script}

La secuencia de comandos de confirmación de valores se activa cuando:

* Un usuario cambia el valor de un campo de la IU.
* El valor de un campo cambia programáticamente debido a cambios en otro campo.

**Se aplica a:** campos

**Tipo de devolución:** El valor commit script expression no devuelve ningún valor. Si alguna expresión devuelve un valor, se ignora el valor.

**Ejemplo:** Para convertir las mayúsculas y minúsculas de los alfabetos introducidos en el campo a mayúsculas en la confirmación, el valor de la expresión de confirmación es:
`this.value=this.value.toUpperCase()`

>[!NOTE]
>
>Puede desactivar la ejecución del script de confirmación de valores cuando el valor de un campo se cambie mediante programación. Para ello, vaya a https://&#39;[server]:[puerto]&#39;/system/console/configMgr y cambiar **Versión adaptable de Forms para compatibilidades** a **AEM Forms 6.1**. A partir de entonces, el script de confirmación de valores solo se ejecuta cuando el usuario cambia el valor del campo de la interfaz de usuario.

### Expresión de visibilidad {#visibility-expression}

La expresión Visibilidad se utiliza para controlar la visibilidad del campo o panel. Normalmente, la expresión visibility utiliza la propiedad value de un campo y se recupera cada vez que cambia ese valor.

**Se aplica a**: campos y panel

**Tipo de devolución**: Expression devuelve un valor booleano, que representa el campo/panel visible o no. **false** representa que el campo o panel no está visible y true representa que el campo o panel es visible.

**Ejemplo**: Para un panel que se vuelve visible solo si el valor de **field1** está configurado como **Hombre**, la expresión de visibilidad es: `field1.value == "Male"`

### Expresión de finalización de paso {#step-completion-expression}

La expresión de finalización de paso se utiliza para evitar que un usuario vaya al siguiente paso de un diseño de asistente. Estas expresiones se utilizan cuando los paneles tienen una presentación de asistente (formularios de varios pasos que muestran un paso a la vez). El usuario puede pasar al siguiente paso, panel o subsección solo si todos los valores requeridos de la sección actual están rellenados y son válidos.

**Se aplica a**: Paneles con diseño de elemento definido en asistente.

**Tipo de devolución**: Expression devuelve un valor booleano, que representa que el panel actual es válido o no. **True** representa que el panel actual es válido y el usuario puede navegar al panel siguiente.

**Ejemplo**: En un formulario organizado en varios paneles, antes de navegar al panel siguiente, se valida el panel actual. En estos casos, se utilizan las expresiones de finalización de paso. Por lo general, estas expresiones utilizan la API de validación de GuideBridge. Un ejemplo de expresión de finalización de paso es:
`window.guideBridge.validate([],this.panel.navigationContext.currentItem.somExpression)`

## Validaciones en forma adaptable {#validations-in-adaptive-form}

Existen varios métodos para agregar la validación de campos a un formulario adaptable. Si se añade una comprobación de validación en un campo, **True** representa que el valor introducido en el campo es válido. **False** representa que el valor no es válido. Si inserta y sale de un campo, no se genera el mensaje de error.

Los métodos para agregar validaciones en un campo son:

### Requerido {#required}

Para hacer que un componente sea obligatorio, en la sección **Editar** del componente, puede seleccionar la opción **Título y texto > Requerido**. También puede añadir el mensaje necesario correspondiente (opcional) . .

### Patrones de validación {#validation-patterns}

Hay varios patrones de validación predeterminados disponibles para un campo. Para seleccionar un patrón de validación, en la sección **Editar** del componente, busque el **Patrones** y seleccione **patrones**. Puede crear su propio patrón de validación personalizado en una **Patrón** cuadro de texto. Se devuelve el estado de validación **True** solo si los datos rellenados cumplen el patrón de validación, de lo contrario **False** se devuelve. <!-- To write your own custom validation pattern, see [Picture clause support for HTML5 forms](picture-clause-support.md). -->

### Expresiones de validación {#validation-expressions}

La validación de un campo también se puede calcular mediante expresiones en diferentes campos. Estas expresiones se escriben dentro de **Secuencia de comandos de validación** del campo **Secuencia de comandos** pestaña **Editar** del componente. El estado de validación de un campo depende del valor que devuelva la expresión. Para obtener información sobre cómo escribir estas expresiones, consulte [Validar expresión](adaptive-form-expressions.md#p-validate-expression-p).

## Información adicional {#additional-information}

### Uso del formato de visualización de campo {#using-field-display-format}

El formato de visualización puede utilizarse para mostrar los datos en distintos formatos. Por ejemplo, puede utilizar el formato de visualización para mostrar un número de teléfono con guiones, aplicar formato a código postal o un selector de fechas. Estos patrones de visualización se pueden seleccionar desde el **Patrones** del cuadro de diálogo Editar de un componente. Puede escribir patrones de visualización personalizados similares a los patrones de validación mencionados anteriormente.

### GuideBridge: API y eventos {#guidebridge-apis-and-events}

GuideBridge es una colección de API que se pueden usar para interactuar con Forms adaptable en el modelo de memoria en un explorador. Para obtener una introducción detallada a la API de Guide Bridge, los métodos de clase y los eventos expuestos, consulte [Referencia de la API de la biblioteca JavaScript™ para Forms adaptable](https://helpx.adobe.com/aem-forms/6/javascript-api/).

>[!NOTE]
>
>Se recomienda no utilizar los oyentes de eventos GuideBridge en las expresiones.

#### Uso de GuideBridge en varias expresiones {#guidebridge-usage-in-various-expressions}

* Para restablecer los campos del formulario, puede realizar déclencheur `guideBridge.reset()` API en la expresión de clic de un botón. Del mismo modo, existe una API de envío que puede llamarse expresión de clic `guideBridge.submit()`**.**

* Puede usar la variable `setFocus()` API para definir el enfoque en varios campos o paneles (para el enfoque del panel, se establece automáticamente en el primer campo). `setFocus()`proporciona una amplia gama de opciones para navegar, como la navegación entre paneles, la travesía anterior/siguiente, la definición del enfoque en un campo concreto y muchas más. Por ejemplo, para desplazarse al panel siguiente, puede utilizar: `guideBridge.setFocus(this.panel.somExpression, 'nextItem').`

* Para validar un formulario adaptable o sus paneles específicos, utilice `guideBridge.validate(errorList, somExpression).`

#### Uso de GuideBridge fuera de las expresiones  {#using-guidebridge-outside-expressions-nbsp}

También puede utilizar las API de GuideBridge fuera de las expresiones. Por ejemplo, puede utilizar la API de GuideBridge para establecer la comunicación entre el HTML de página que aloja el formulario adaptable y el modelo de formulario. Además, puede establecer el valor que proviene del elemento principal de Iframe que aloja el formulario.

Para utilizar la API de GuideBridge para el ejemplo mencionado anteriormente, capture una instancia de GuideBridge. Para capturar la instancia, escuche `bridgeInitializeStart`evento de `window`objeto:

```javascript
window.addEventListener("bridgeInitializeStart", function(evnt) {

     // get hold of the guideBridge object

     var gb = evnt.detail.guideBridge;

     //wait for the completion of AF

     gb.connect(function (){

        //this function will be called after Adaptive Form is initialized

     })

})
```

>[!NOTE]
>
>En AEM, es recomendable escribir código en clientLib e incluirlo en su página (header.jsp o footer.jsp de la página)

Para utilizar GuideBridge después de inicializar el formulario (la variable `bridgeInitializeComplete` ), obtenga la instancia de GuideBridge mediante `window.guideBridge`. Puede comprobar el estado de inicialización de GuideBridge mediante el `guideBride.isConnected` API.

#### Eventos de GuideBridge {#guidebridge-events}

GuideBridge también proporciona ciertos eventos para secuencias de comandos externas en la página de alojamiento. Los scripts externos pueden escuchar estos eventos y realizar diversas operaciones. Por ejemplo, cada vez que cambia el nombre de usuario en un formulario, también cambia el nombre que se muestra en el encabezado de la página. Para obtener más información sobre estos eventos, consulte [Referencia de la API de la biblioteca JavaScript™ para Forms adaptable](https://helpx.adobe.com/aem-forms/6/javascript-api/GuideBridge.html).

Utilice el siguiente código para registrar los controladores:

```javascript
guideBridge.on("elementValueChanged", function (event, data)  {

      // execute some logic when value of a field is changed

});
```

### Creación de patrones personalizados para un campo {#creating-custom-patterns-for-a-field}

Como se ha mencionado anteriormente, Adaptive Forms permite al autor proporcionar patrones para los formatos de validación o visualización. Además de utilizar patrones predeterminados, puede definir patrones personalizados reutilizables para un componente Formulario adaptable. Por ejemplo, puede definir un campo de texto o un campo numérico. Una vez definidos, se pueden utilizar estos patrones en todos los formularios para un tipo de componente específico. Por ejemplo, puede crear un patrón personalizado para un campo de texto y utilizarlo en los campos de texto de su Forms adaptable. Puede seleccionar el patrón personalizado accediendo a la sección Patrón del cuadro de diálogo de edición de un componente. <!-- For details about Pattern definition or format, see [Picture clause support for HTML5 forms](picture-clause-support.md).-->

Realice los siguientes pasos para crear un patrón personalizado para un tipo de campo específico y reutilizarlo para otros campos del mismo tipo:

1. Vaya al CRXDE Lite de la instancia de creación.
1. Cree una carpeta para mantener los patrones personalizados. En el directorio /apps, cree un nodo de tipo sling:folder. Por ejemplo, cree un nodo con el nombre `customPatterns`. Bajo este nodo, cree otro nodo de tipo `nt:unstructed` y asígnele un nombre `textboxpatterns`. Este nodo contiene los distintos patrones personalizados que desea agregar.
1. Abra la pestaña Propiedades del nodo creado. Por ejemplo, abra la ficha Propiedades de `textboxpatterns`. Agregue la variable `guideComponentType` propiedad en este nodo y establezca su valor en *fd/af/components/formatter/guideTextBox*.

1. El valor de esta propiedad varía según el campo para el que desee definir los patrones. Para el campo numérico, el valor de la variable `guideComponentType` la propiedad es *fd/af/components/formatter/guideNumericBox*. El valor del campo Marcador de datos es *fd/af/components/formatter/guideDatepicker*. &quot;
1. Puede agregar un patrón personalizado asignando una propiedad al `textboxpatterns` nodo . Agregar una propiedad con un nombre (por ejemplo `pattern1`) y establezca su valor en el patrón que desee añadir. Por ejemplo, añadir una propiedad `pattern1` con el valor Fax=text{99-999-9999999}. El patrón está disponible para todos los cuadros de texto que utilice en Forms adaptable.

   ![Creación de patrones personalizados para campos en CrxDe](assets/creating-custom-patterns.png)

   Creación de patrones personalizados

