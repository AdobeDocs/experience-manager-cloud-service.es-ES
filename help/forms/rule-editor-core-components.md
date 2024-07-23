---
title: ¿Cómo se utiliza el editor de reglas para agregar reglas a los campos de formulario para agregar un comportamiento dinámico y generar una lógica compleja a un formulario adaptable basado en componentes principales?
description: El editor de reglas de formularios adaptables permite agregar un comportamiento dinámico y generar una lógica compleja en los formularios sin codificación ni scripts.
feature: Adaptive Forms, Core Components
role: User, Developer
level: Beginner, Intermediate
exl-id: 1292f729-c6eb-4e1b-b84c-c66c89dc53ae
source-git-commit: 780c68f0c21ef94ff6a73ce991370100b1a88db9
workflow-type: tm+mt
source-wordcount: '1176'
ht-degree: 65%

---


# Introducción al Editor de reglas para formularios adaptables basados en componentes principales

| Versión | Vínculo del artículo |
| -------- | ---------------------------- |
| AEM as a Cloud Service (componentes principales) | Este artículo |
| AEM as a Cloud Service (componentes de base) | [Haga clic aquí](/help/forms/rule-editor.md) |
| AEM 6.5 | [Haga clic aquí](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-advanced-authoring/rule-editor.html?lang=es) |

En un formulario adaptable basado en componentes principales, la función de editor de reglas permite a los usuarios y desarrolladores escribir reglas para objetos de formulario adaptable. Estas reglas definen las acciones que se deben habilitar en los objetos del formulario en función de los ajustes preestablecidos, las entradas del usuario y las acciones del usuario en el formulario. Esta capacidad ayuda a optimizar aún más la experiencia de cumplimentación de formularios, lo que garantiza tanto la precisión como la velocidad.

El editor de reglas proporciona una interfaz de usuario intuitiva y simplificada para escribir reglas. Ofrece un editor visual que se adapta a todos los usuarios, lo que les permite crear y administrar reglas sin necesidad de tener amplios conocimientos técnicos. Este enfoque visual facilita a los usuarios comprender e implementar la lógica deseada en sus formularios.

Algunas de las acciones clave que se pueden realizar en objetos de formulario adaptable mediante reglas son las siguientes:

* Mostrar u ocultar un objeto
* Habilitar o deshabilitar un objeto
* Establecer un valor para un objeto
* Validar el valor de un objeto
* Ejecutar funciones para calcular el valor de un objeto
* Invocar un servicio del modelo de datos de formulario (FDM) y realizar una operación
* Establecer la propiedad de un objeto

<!-- Rule editor replaces the scripting capabilities in [!DNL Experience Manager 6.1 Forms] and earlier releases. However, your existing scripts are preserved in the new rule editor. For more information about working with existing scripts in the rule editor, see [Impact of rule editor on existing scripts](rule-editor.md#p-impact-of-rule-editor-on-existing-scripts-p). -->

Los usuarios agregados al grupo `forms-power-users` pueden crear scripts y editar los existentes. Los usuarios del grupo [!DNL forms-users] pueden utilizar los scripts, pero no crearlos o editarlos.

Consulte el artículo [Diferencia entre el editor de reglas de base y el editor de reglas de componentes principales](/help/forms/rule-editor-core-components-difference-tables.md) para obtener una comparación detallada.

<!--
## Difference between Rule editor in Core Components and Rule Editor in Foundation Components

{{rule-editor-diff}}

>[!NOTE]
>
> To see how to create and use custom functions in detail, refer to [Custom functions in Adaptive Forms (Core Components)](/help/forms/create-and-use-custom-functions.md) article.

-->

## Explicación de una regla {#understanding-a-rule}

Una regla es una combinación de acciones y condiciones. En el editor de reglas, las acciones incluyen actividades como ocultar, mostrar, habilitar, deshabilitar o calcular el valor de un objeto en un formulario. Las condiciones son expresiones booleanas que se evalúan realizando comprobaciones y operaciones en el estado, el valor o la propiedad de un objeto de formulario. Las acciones se realizan según el valor devuelto (`True` o `False`) mediante la evaluación de una condición.

El editor de reglas proporciona un conjunto de tipos de reglas predefinidas, como When, Show, Hide, Enable, Disable, Set Value Of y Validate para ayudarle a escribir reglas. Cada tipo de regla permite definir condiciones y acciones en una regla. El documento explica cada tipo de regla en detalle.

Una regla suele seguir una de las siguientes construcciones:

**Condición-acción**. En esta construcción, una regla primero define una condición seguida de una acción que activar. La construcción es comparable a la instrucción if-then en lenguajes de programación.

En el editor de reglas, el tipo de regla **When** aplica la construcción de condición-acción.

**Acción-condición**. En esta construcción, una regla primero define una acción que activar seguida de condiciones para la evaluación. Otra variación de esta construcción es acción-condición-acción alternativa, que también define una acción alternativa que activar si la condición devuelve un valor False.

Los tipos de reglas Show, Hide, Enable, Disable, Set Value Of y Validate del editor de reglas aplican la construcción de reglas acción-condición. De forma predeterminada, la acción alternativa para Show es Hide y para Enable es Disable y viceversa. No se puede cambiar la acción alternativa predeterminada.

>[!NOTE]
>
>Los tipos de reglas disponibles, incluidas las condiciones y las acciones definidas en el editor de reglas, también dependen del tipo de objeto de formulario en el que se vaya a crear una regla. El editor de reglas solo muestra tipos de reglas y opciones válidas para escribir condiciones e instrucciones de acción para un tipo de objeto de formulario concreto. Por ejemplo, no ve los tipos Validar y Establecer valor de para un objeto panel.

Para obtener más información sobre los tipos de reglas disponibles en el editor de reglas, consulte [Tipos de reglas disponibles en el editor de reglas](rule-editor.md#p-available-rule-types-in-rule-editor-p).

### Pautas para elegir una construcción de regla {#guidelines-for-choosing-a-rule-construct}

Aunque puede lograr la mayoría de los casos de uso utilizando cualquier construcción de regla, estas son algunas pautas para elegir una construcción antes que otra. Para obtener más información sobre las reglas disponibles en el editor de reglas, consulte [Tipos de reglas disponibles en el editor de reglas](rule-editor.md#p-available-rule-types-in-rule-editor-p).

* Una regla general típica al crear una regla es pensarla en el contexto del objeto en el que quiere escribirla. Tenga en cuenta que desea ocultar o mostrar el campo B en función del valor que un usuario especifique en el campo A. En este caso, quiere evaluar una condición en el campo A y, en función del valor que se devuelva, se debe activar una acción en el campo B.

  Por lo tanto, si está escribiendo una regla en el campo B (el objeto sobre el que se evalúa una condición), utilice la construcción condición-acción o el tipo de regla When. Del mismo modo, utilice la construcción acción-condición o el tipo de regla Show o Hide en el campo A.

* A veces, debe realizar varias acciones en función de una condición. En estos casos, se recomienda utilizar la construcción condición-acción. En esta construcción, puede evaluar una condición una vez y especificar varias instrucciones de acción.

  Por ejemplo, para ocultar los campos B, C y D en función de la condición que comprueba el valor que un usuario especifica en el campo A, escriba una regla con la estructura condición-acción o el tipo de regla When en el campo A y especifique acciones para controlar la visibilidad de los campos B, C y D. De lo contrario, necesitará tres reglas independientes en los campos B, C y D, donde cada regla comprueba la condición y muestra u oculta el campo respectivo. En este ejemplo, es más eficaz escribir el tipo de regla When en un objeto, en lugar de Show o Hide en tres objetos.

* Para almacenar en déclencheur una acción basada en varias condiciones, se recomienda utilizar una construcción acción-condición. Por ejemplo, para mostrar y ocultar el campo A mediante la evaluación de condiciones en los campos B, C y D, utilice el tipo de regla Show o Hide en el campo A.
* Utilice la construcción condición-acción o acción-condición si la regla contiene una acción para una condición.
* Si una regla comprueba la existencia de una condición y realiza una acción inmediatamente al proporcionar un valor en un campo o al salir de un campo, se recomienda escribir una regla con una construcción condición-acción o el tipo de regla When en el campo en el que se evalúa la condición.
* La condición de la regla When se evalúa cuando un usuario cambia el valor del objeto en el que se aplica dicha regla. Sin embargo, si desea que la acción se active cuando el valor cambia en el servidor, como para rellenar previamente el valor, se recomienda escribir una regla When que active la acción cuando el campo se inicialice.
* Al escribir reglas para objetos de menús desplegables, botones de opción o casillas de verificación, las opciones o los valores de estos objetos de formulario en el mismo se rellenan previamente en el editor de reglas.

## Siguiente paso

Para comprender cómo usar la interfaz de usuario para escribir y administrar reglas en un editor de reglas, consulte el artículo [Interfaz de usuario del editor de reglas para Forms adaptable basado en componentes principales](/help/forms/rule-editor-core-components-user-interface.md).

## Consulte también

{{see-also-rule-editor}}