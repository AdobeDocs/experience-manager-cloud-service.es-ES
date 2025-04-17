---
title: ¿Cuáles son las mejoras del VRE del servicio de invocación para formularios basados en componentes principales?
description: Mejoras en el servicio de invocación del editor de reglas
feature: Adaptive Forms, Core Components
role: User, Developer
level: Beginner, Intermediate
keywords: invocar mejoras del servicio en VRE, rellenar opciones desplegables utilizando invocar servicio, establecer panel repetible utilizando la salida del servicio de invocación, establecer panel utilizando la salida del servicio de invocación, usar el parámetro de salida del servicio de invocación para validar otro campo.
exl-id: 2ff64a01-acd8-42f2-aae3-baa605948cdd
source-git-commit: 2cae8bb1050bc4538f4645d9f064b227fb947d75
workflow-type: tm+mt
source-wordcount: '1566'
ht-degree: 3%

---

# Usar Invocar servicio en el Editor de reglas visuales para formularios basados en componentes principales

El Editor de reglas visuales de un formulario adaptable admite la característica **Invocar servicio**, que le permite seleccionar un servicio de la lista de modelos de datos de formulario (FDM) configurados para su instancia. Puede asignar campos de formulario directamente a los parámetros de entrada del servicio. Para asignar campos de formulario a los parámetros de salida, utilice la opción de carga útil de evento para el servicio del modelo de datos de formulario especificado. Además, el editor de reglas visual le permite crear reglas para los controladores de éxito y de error para las operaciones **Invoke Service** en función de sus respuestas de salida. Los controladores de éxito administran la ejecución correcta de la operación **Invocar servicio**, mientras que los controladores de error resuelven cualquier error que se produzca.

### Ventajas de utilizar el servicio de invocación en el editor de reglas del formulario

Estas son algunas ventajas de utilizar la operación Invocar servicio en el editor de reglas de un formulario adaptable:

* **Integración optimizada**: el Editor de reglas visuales simplifica el proceso de integración de servicios externos o API en su Forms adaptable. Al usar **Invocar servicio**, puede conectar fácilmente formularios a varias fuentes de datos y servicios sin necesidad de codificación compleja, lo que hace que la integración de formularios sea más eficiente.

* **Gestión dinámica de respuestas**: puede administrar las respuestas de éxito y error en función de las respuestas de salida de **Invocar servicio**, lo que permite que los formularios reaccionen dinámicamente a diferentes escenarios. Garantiza que los formularios gestionen varias condiciones de forma adecuada, lo que mejora la flexibilidad y el control.

* **Interacción mejorada del usuario**: El uso de **Invocar servicio** en el editor de reglas habilita la validación en tiempo real en los formularios, lo que mejora la experiencia del usuario. También garantiza que los datos se validen con precisión en el servidor, reduciendo los errores y mejorando la fiabilidad del formulario.

## Invocar los controladores de servicio para las respuestas de éxito y error

>[!NOTE]
>
> Puede usar los controladores de éxito y de error **Invocar servicio** solo para formularios basados en componentes principales. Forms basado en componentes de base no admite los controladores de éxito y de error **Invoke Service**.

El editor de reglas visual permite crear reglas para los controladores de éxito y de error para las operaciones **Invocar servicio** en función de sus respuestas de salida. La siguiente imagen muestra **Invocar servicio** en el editor de reglas visuales para un formulario adaptable:

![Invocar controladores de servicio](/help/forms/assets/invoke-service-rule-editor.png)

Para agregar el controlador de éxito o de error, haga clic en **[!UICONTROL Agregar controlador de éxito]** o en **[!UICONTROL Agregar controlador de error]**, respectivamente.

Al hacer clic en **[!UICONTROL Agregar controlador de éxito]**, aparece el editor de reglas **[!UICONTROL Invocar controlador de éxito de servicio]**, que le permite especificar reglas o lógica para administrar la respuesta de salida **Invocar servicio** cuando la operación se realiza correctamente. Puede especificar reglas incluso sin definir condiciones; sin embargo, puede agregar condiciones para el controlador de éxito haciendo clic en la opción **[!UICONTROL Agregar condición]**.

![Invocar controlador de éxito del servicio](/help/forms/assets/invoke-service-success-handler.png)

Puede agregar varias reglas para controlar las respuestas correctas para la operación **Invocar servicio**:

![Controlador de éxito múltiple](/help/forms/assets/invoke-service-multiple-success-handlers.png){width=50%, height=50%}

Del mismo modo, puede agregar reglas para controlar la respuesta de salida **Invocar servicio** cuando la operación no se realice correctamente. La siguiente imagen muestra el editor de reglas **[!UICONTROL Invocar controlador de errores del servicio]**:

![Invocar controlador de error de servicio](/help/forms/assets/invoke-service-failue-handler.png)

También puede agregar varias reglas para controlar las respuestas erróneas de la operación **Invocar servicio**.

La característica **Habilitar validación de errores en el servidor** permite que el autor agregue validaciones al diseñar un formulario adaptable para que también se ejecute en el servidor.

## Requisitos previos para utilizar Invoke Service en el editor de reglas

A continuación se muestran los requisitos previos que debe cumplir antes de usar **Invocar servicio** en el editor de reglas:

* Asegúrese de haber configurado una fuente de datos. Para obtener instrucciones sobre cómo configurar un origen de datos, [haga clic aquí](/help/forms/configure-data-sources.md).
* Crear un modelo de datos de formulario con la fuente de datos configurada. Para obtener instrucciones sobre cómo crear un modelo de datos de formulario, [haga clic aquí](/help/forms/create-form-data-models.md).
* Asegúrese de que los componentes principales estén habilitados para su entorno. Para obtener instrucciones detalladas sobre cómo habilitar los componentes principales para su entorno, [haga clic aquí](/help/forms/enable-adaptive-forms-core-components.md).

## Exploración del servicio de invocación mediante diferentes casos de uso

**Invocar servicio** del editor de reglas visual le permite realizar varias operaciones útiles. Puede usarlo para rellenar opciones desplegables, establecer paneles simples o repetibles y validar campos de formulario, todo en función de la respuesta de salida de **Invocar servicio**. De este modo, se mejora la flexibilidad y la interactividad de los formularios.

La tabla siguiente describe algunos escenarios en los que se puede usar **Invocar servicio**:

| **Caso práctico** | **Descripción** |
|----------------------------------------------------------|-------------------------------------------------------------------------------------------------------|
| **Rellenar opciones desplegables usando el resultado de Invocar servicio** | Rellena opciones desplegables dinámicamente en función de los datos recuperados de la salida de Invocar servicio. [Haga clic aquí](#use-case-1-populate-dropdown-values-using-the-output-of-invoke-service) para ver la implementación. |
| **Establecer panel repetible con el resultado de Invocar servicio** | Configura un panel repetible mediante los datos de la salida Invocar servicio, lo que permite el uso de paneles dinámicos. [Haga clic aquí](#use-case-2-set-repeatable-panel-using-output-of-invoke-service) para ver la implementación. |
| **Establecer panel con el resultado de Invocar servicio** | Establece el contenido o la visibilidad de un panel utilizando valores específicos de la salida Invocar servicio. [Haga clic aquí](#use-case-3-set-panel-using-output-of-invoke-service) para ver la implementación. |
| **Use el parámetro de salida de Invocar servicio para validar otros campos** | Utiliza parámetros de salida específicos del servicio de invocación para validar los campos del formulario. [Haga clic aquí](#use-case-4-use-output-parameter-of-invoke-service-to-validate-other-fields) para ver la implementación. |

Cree un formulario `Get Information` que recupere valores según la entrada escrita en el cuadro de texto `Pet ID`. La captura de pantalla siguiente muestra el formulario utilizado en estos casos de uso:

![Obtener información del formulario](/help/forms/assets/get-information-form.png)

**Campos de formulario**

Agregue los campos siguientes al formulario:
* **Introducir ID de mascota**: Cuadro de texto
* **Seleccionar URL de fotos**: desplegable
* **Etiquetas**: Panel
   * Nombre: Textbox
   * ID: Textbox
* **Categoría**: Panel
   * Nombre: Textbox
* **Enviar**: botón Enviar

>[!NOTE]
>
> En el campo **Referencia de enlace** del cuadro de diálogo **Propiedades** de los campos de formulario, seleccione ![foldersearch_18](assets/folder-search-icon.svg) y desplácese hasta seleccionar la propiedad binaria que agregó en el modelo de datos de formulario (FDM).

**Configurar paneles**

Defina los paneles como repetitivos con las restricciones siguientes:
* Valor mínimo: 1
* Valor máximo: 4

Puede ajustar los valores de los paneles repetitivos para adaptarlos a sus necesidades.

**Origen de datos**

En este ejemplo, la API [Swagger Petstore](https://petstore.swagger.io/) se usa para configurar un origen de datos. El modelo de datos de formulario [Form](/help/forms/create-form-data-models.md) está configurado para el servicio [getPetById](https://petstore.swagger.io/#/pet/getPetById), que recupera los detalles del animal doméstico en función del ID ingresado.

Publicemos el siguiente JSON usando el servicio [addPet](https://petstore.swagger.io/#/pet/addPet) en la API de [Swagger Petstore](https://petstore.swagger.io/):

```
{
        "id": 101,
        "category": {
            "id": 1,
            "name": "Labrador"
        },
        "name": "Lisa",
        "photoUrls": [
            "https://example.com/photos/lisa1.jpg",
            "https://example.com/photos/lisa2.jpg"
        ],
        "tags": [
            {
                "id": 1,
                "name": "vaccinated"
            },
            {
                "id": 2,
                "name": "friendly"
            },
            {
                "id": 3,
                "name": "house-trained"
            }
        ],
        "status": "available"
    }
```


Las reglas y la lógica se implementan mediante la acción **Invocar servicio** en el editor de reglas del cuadro de texto `Pet ID` para mostrar los casos de uso mencionados.

Ahora vamos a explorar en detalle la implementación de cada caso de uso.

### Caso de uso 1: Rellenar valores desplegables utilizando la salida de Invocar servicio

Este caso de uso muestra cómo rellenar opciones desplegables de forma dinámica en función del resultado de `Invoke Service`.

#### Implementación

Para conseguirlo, cree una regla en el cuadro de texto `Pet ID` para invocar el servicio `getPetById`. En la regla, establezca la propiedad `enum` de la lista desplegable `photo-url` en `photoUrls` en **[!UICONTROL Agregar controlador de éxito]**.

![Establecer valor desplegable](/help/forms/assets/set-dropdownoption.png)

#### Salida

Escriba `101` en el cuadro de texto `Pet ID` para rellenar dinámicamente las opciones desplegables en función del valor introducido.

![Resultado](/help/forms/assets/output1.png)

### Caso de uso 2: Establecer un panel repetible con la salida del servicio de invocación

Este caso de uso muestra cómo rellenar paneles repetibles de forma dinámica basándose en el resultado de un **servicio Invoke**.

#### Consideraciones

* Asegúrese de que el nombre del panel repetible coincida con el parámetro del **Servicio de invocación** para el que desea establecer el panel.
* El panel se repite para el número de valores devueltos por el campo **Invocar servicio** correspondiente.

#### Implementación

Cree una regla en el cuadro de texto `Pet ID` para invocar el servicio `getPetById`. En **[!UICONTROL Agregar controlador de éxito]**, agregue otra respuesta de controlador de éxito. Establezca el valor del panel `tags` en `tags` en la regla.

![Crear regla para el panel repetible](/help/forms/assets/create-rule-repeatable-panel.png)

#### Salida

Escriba `101` en el cuadro de texto `Pet ID` para rellenar dinámicamente el panel repetible en función del valor de entrada.

![Salida](/help/forms/assets/output2.png)

### Caso de uso 3: Configurar el panel mediante la salida del servicio de invocación

Este caso de uso muestra cómo establecer dinámicamente el valor de un panel en función del resultado de **Invocar servicio**.

#### Consideraciones

* Asegúrese de que el nombre del panel coincida con el parámetro del **Servicio de invocación** para el que desea establecer el panel.
* El panel se repite para el número de valores devueltos por el campo Invocar servicio correspondiente.

#### Implementación

Cree una regla en el cuadro de texto `Pet ID` para invocar el servicio `getPetById`. En **[!UICONTROL Agregar controlador de éxito]**, agregue otra respuesta de controlador de éxito. Establezca el valor del cuadro de texto `categoryname` en `category.name` en la regla.

![Crear regla para el panel repetible](/help/forms/assets/set-panel-values.png)

#### Salida

Escriba `101` en el cuadro de texto `Pet ID` para rellenar dinámicamente el panel en función del valor de entrada.

![Salida](/help/forms/assets/output3.png)

### Caso de uso 4: Usar el parámetro de salida de Invocar servicio para validar otros campos

Este caso de uso muestra cómo usar el resultado de **Invocar servicio** para validar dinámicamente otros campos de formulario.

#### Implementación

Cree una regla en el cuadro de texto `Pet ID` para invocar el servicio `getPetById`. En **[!UICONTROL Agregar controlador de errores]**, agregue una respuesta de controlador de errores. Ocultar el botón **Enviar** si se escribe un `Pet ID` incorrecto.

![Controlador de errores](/help/forms/assets/create-rule-failure-handler.png)

#### Salida

Escriba `102` en el cuadro de texto `Pet ID` y el botón **Enviar** estará oculto.

![Salida](/help/forms/assets/output4.png)

## Preguntas frecuentes

**Q: ¿Qué sucede si he creado una regla con el servicio de invocación y luego actualizo a la última versión de los componentes principales?**

**A:** Al actualizar a la última versión de los componentes principales, la regla **Invocar servicio** se actualiza automáticamente a la interfaz de usuario más reciente, ya que es compatible con versiones anteriores.

**Q: ¿Puedo agregar varias reglas para controlar las respuestas correctas o de error para la operación Invocar servicio?**

**A:** Sí, puede agregar varias reglas para controlar las respuestas correctas o de error para la operación **Invocar servicio**.

## Artículos relacionados

* [Configuración de las fuentes de datos](configure-data-sources.md)
* [Crear modelo de datos de formulario (FDM)](create-form-data-models.md)
* [Trabajar con el modelo de datos de formulario (FDM)](work-with-form-data-model.md)
* [Uso del modelo de datos de formulario (FDM)](using-form-data-model.md)


## Recursos adicionales

{{see-also-rule-editor}}
