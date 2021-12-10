---
title: ¿Cómo se agregan variables en AEM pasos de flujo de trabajo?
description: Obtenga información sobre cómo crear una variable, configurar un valor para la variable y usarlo en [!DNL AEM Forms] Pasos del flujo de trabajo.
exl-id: d9139ea9-2f86-476c-8767-b36766790f2c
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '2059'
ht-degree: 0%

---

# Variables en flujos de trabajo AEM centrados en Forms {#variables-in-aem-forms-workflows}

Una variable en un modelo de flujo de trabajo es una forma de almacenar un valor basado en su tipo de datos. Puede utilizar el nombre de la variable en cualquier paso del flujo de trabajo para recuperar el valor almacenado en la variable . También puede utilizar nombres de variables para definir expresiones para tomar decisiones de enrutamiento.

En AEM modelos de flujo de trabajo, puede:

* [Crear una variable](variable-in-aem-workflows.md#create-a-variable) de un tipo de datos basado en el tipo de información que desea almacenar en él.
* [Configure un valor para la variable](variable-in-aem-workflows.md#set-a-variable) uso del paso de flujo de trabajo Establecer variable .
* [Utilice la variable](variable-in-aem-workflows.md#use-a-variable) en todo [!DNL AEM Forms] Pasos del flujo de trabajo para recuperar el valor almacenado y en los pasos OR Split y Goto para definir una expresión de enrutamiento.

En el siguiente vídeo se muestra cómo crear, establecer y utilizar variables en AEM modelos de flujo de trabajo:

>[!VIDEO](assets/variables_introduction_1_1.mp4)

Las variables son una extensión de la [MetaDataMap](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/metadata/MetaDataMap.html) interfaz. Puede usar [MetaDataMap](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/metadata/MetaDataMap.html) en ECMAScript para acceder a los metadatos guardados con variables.

## Crear una variable {#create-a-variable}

Las variables se crean mediante la sección Variables disponible en la barra de tareas del modelo de flujo de trabajo. AEM Las variables de flujo de trabajo admiten los siguientes tipos de datos:

* **Tipos de datos primitivos**: Long, Double, Boolean, Date y String
* **Tipos de datos complejos**: [Documento](https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/aemfd/docmanager/Document.html), [XML](https://docs.oracle.com/javase/8/docs/api/org/w3c/dom/Document.html), [JSON](https://static.javadoc.io/com.google.code.gson/gson/2.3/com/google/gson/JsonObject.html), y la instancia del Modelo de datos de formulario.

>[!NOTE]
>
>Los flujos de trabajo solo admiten el formato ISO8601 para las variables de tipo Fecha.

Utilice el tipo de datos ArrayList para crear colecciones de variables. Puede crear una variable ArrayList para todos los tipos de datos primitivos y complejos. Por ejemplo, cree una variable ArrayList y seleccione String como subtipo para almacenar varios valores de cadena usando la variable .

Para crear una variable:

1. En una instancia de AEM, vaya a Herramientas ![](assets/hammer-icon.svg) > Flujo de trabajo > Modelos.
1. Toque **[!UICONTROL Crear]** y especifique el título y un nombre opcional para el modelo de flujo de trabajo. Seleccione el modelo y pulse **[!UICONTROL Editar]**.
1. Pulse el icono de variables disponible en la barra de tareas del modelo de flujo de trabajo y pulse **[!UICONTROL Agregar variable]**.

   ![Añadir variable](assets/variables_add_variable_new.png)

1. En el cuadro de diálogo Agregar variable , especifique el nombre y seleccione el tipo de variable.
1. Seleccione el tipo de datos de la variable **[!UICONTROL Tipo]** lista desplegable y especifique los siguientes valores:

   * Tipo de datos primitivo : especifique un valor predeterminado opcional para la variable.
   * JSON o XML : especifique una ruta de esquema JSON o XML opcional. El sistema valida la ruta del esquema al asignar y almacenar las propiedades disponibles en este esquema para otra variable.
   * Modelo de datos de formulario: especifique una ruta del Modelo de datos de formulario.
   * ArrayList : especifique un subtipo para la colección.

1. Especifique una descripción opcional para la variable y pulse ![done_icon](assets/Smock_Checkmark_18_N.svg) para guardar los cambios. La variable se muestra en la lista disponible en el panel izquierdo.

Cuando cree variables, tenga en cuenta las siguientes prácticas:

* Cree tantas variables como requiera un flujo de trabajo. Sin embargo, para conservar los recursos de la base de datos, utilice el número mínimo de variables necesarias y vuelva a utilizar las variables siempre que sea posible.
* Las variables distinguen entre mayúsculas y minúsculas. Asegúrese de hacer referencia a las variables con el mismo caso en el flujo de trabajo.
* Evite utilizar caracteres especiales en el nombre de la variable

## Establecer una variable {#set-a-variable}

Puede utilizar el paso Establecer variable para establecer el valor de una variable y definir el orden en que se configuran los valores. La variable se configura en el orden en que se enumeran las asignaciones de variables en el paso establecer variable .

Los cambios en los valores de las variables afectan únicamente a la instancia del proceso en que se produce el cambio. Por ejemplo, cuando se inicia un flujo de trabajo y cambian los datos de las variables, los cambios afectan únicamente a esa instancia del flujo de trabajo. Los cambios no afectan a otras instancias del flujo de trabajo que se iniciaron anteriormente o que se iniciaron más tarde.

Según el tipo de datos de la variable , puede utilizar las siguientes opciones para establecer el valor de una variable:

* **Literal:** Utilice la opción cuando conozca el valor exacto que desea especificar. También puede utilizar la opción para especificar un JSON en forma de cadena.

* **Expresión:** Utilice la opción cuando el valor que se va a utilizar se calcule en función de una expresión. La expresión se crea en el editor de expresiones proporcionado.

* **Notación de puntos JSON:** Utilice la opción para recuperar un valor de una variable de tipo JSON o FDM.
* **XPATH:** Utilice la opción para recuperar un valor de una variable de tipo XML.

* **En relación con la carga útil:** Utilice la opción cuando el valor que se va a guardar en la variable esté disponible en una ruta relativa a la carga útil.

* **Ruta absoluta:** Utilice la opción cuando el valor que se va a guardar en la variable esté disponible en una ruta absoluta.

También puede actualizar elementos específicos de una variable de tipo JSON o XML utilizando Notación DOT JSON o Notación XPATH.

### Añadir asignación entre variables {#add-mapping-between-variables}

Para agregar asignaciones entre variables:

1. En la página de edición del flujo de trabajo, pulse el icono Pasos disponible en la barra de tareas del modelo de flujo de trabajo.
1. Arrastre y suelte la **[!UICONTROL Establecer variable]** paso al editor de flujo de trabajo, pulse el paso y seleccione ![configure_icon](assets/Smock_Wrench_18_N.svg) (Configurar).
1. En el cuadro de diálogo Establecer variable , seleccione **[!UICONTROL Asignación]** > **[!UICONTROL Agregar asignación]**.
1. En el **Variable de mapa** , seleccione la variable para almacenar datos, seleccione el modo de asignación y especifique un valor para almacenar en la variable . Los modos de asignación varían en función del tipo de variable.
1. Asigne más variables para crear una expresión significativa. Toque ![done_icon](assets/Smock_Checkmark_18_N.svg) para guardar los cambios.

### Ejemplo 1: Consultar una variable XML para establecer el valor de una variable de cadena {#example-query-an-xml-variable-to-set-value-for-a-string-variable}

Seleccione una variable de tipo XML para almacenar un archivo XML. Consulte la variable XML para establecer el valor de una variable de cadena para la propiedad disponible en el archivo XML. Uso **Especificar XPATH para la variable XML** para definir la propiedad que se almacenará en la variable de cadena.

En este ejemplo, seleccione un **formdata** Variable XML para almacenar la variable **cc-app.xml** archivo. Consulte la **formdata** para establecer el valor de la variable **email** variable de cadena para almacenar el valor de la variable **emailAddress** propiedad disponible en la variable **cc-app.xml** archivo.

>[!VIDEO](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-5/forms/using/set_variable_example1.mp4 "Definir el valor de una variable")

### Ejemplo 2: Usar una expresión para almacenar valores según otras variables {#example2}

Utilice una expresión para calcular la suma de las variables y almacenar el resultado en una variable.

En este ejemplo, utilice el editor de expresiones para definir una expresión para calcular la suma de **assetscost** y **balanceamount** y almacenar el resultado en **totalvalue** variable.

>[!VIDEO](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-5/forms/using/variables_expression.mp4)

## Usar editor de expresiones {#use-expression-editor}

También se utilizan expresiones para calcular el valor de una variable en tiempo de ejecución. Las variables proporcionan un editor de expresiones para definir expresiones.

Utilice el editor de expresiones para:

* Establezca el valor de las variables utilizando otras variables de flujo de trabajo, números o expresiones matemáticas.
* Utilice variables de flujo de trabajo, cadena, número o una expresión dentro de una expresión matemática
* Agregue condiciones para establecer los valores de las variables.
* Agregue operadores entre condiciones.

![Editor de expresiones](assets/variables_expression_editor_new.png)

Se basa en el editor de reglas de Forms adaptable con los cambios siguientes. Editor de reglas en variables:

* No admite funciones.
* No proporciona una interfaz de usuario para ver el resumen de las reglas
* No tiene editor de código.
* No admite la activación y desactivación del valor de un objeto.
* No admite la configuración de la propiedad de un objeto.
* No admite llamar a un servicio web.

Para obtener más información, consulte [Editor de reglas de Forms adaptable](rule-editor.md).

## Usar una variable {#use-a-variable}

Puede utilizar variables para recuperar entradas y salidas o guardar el resultado de un paso. El editor de flujo de trabajo proporciona dos tipos de pasos de flujo de trabajo:

* Pasos del flujo de trabajo compatibles con las variables
* Pasos del flujo de trabajo sin compatibilidad con variables

### Pasos del flujo de trabajo compatibles con las variables {#workflow-steps-with-support-for-variables}

El paso Ir a, O Dividir y todo [!DNL AEM Forms] Los pasos del flujo de trabajo admiten variables.

#### Paso dividido OR {#or-split-step}

La división OR crea una división en el flujo de trabajo, tras la cual solo una rama está activa. Este paso le permite introducir rutas de procesamiento condicionales en el flujo de trabajo. Los pasos del flujo de trabajo se agregan a cada rama según sea necesario.

Puede definir la expresión de enrutamiento para una rama mediante una definición de regla, una secuencia de comandos ECMA o una secuencia de comandos externa.

Puede utilizar variables para definir la expresión de enrutamiento mediante el editor de expresiones. Para obtener más información sobre el uso de expresiones de enrutamiento para el paso OR Split , consulte [Paso dividido OR](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/extending-workflows/workflows-step-ref.html#extending-aem#or-split).

En este ejemplo, antes de definir la expresión de enrutamiento, utilice [ejemplo 2](variable-in-aem-workflows.md#example2) para establecer el valor de la variable **totalvalue** variable. La rama 1 está activa si el valor de la variable **totalvalue** es bueno que 50000. Del mismo modo, puede definir una regla para que la Rama 2 esté activa si el valor de la variable **totalvalue** es menor que 50000.

>[!VIDEO](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-5/forms/using/variables_orsplit_example.mp4)

Del mismo modo, seleccione una ruta de script externa o especifique la secuencia de comandos ECMA para las expresiones de enrutamiento para evaluar la rama activa. Toque **[!UICONTROL Cambiar nombre de rama]** para especificar un nombre alternativo para la rama.

<!-- For more examples, see [Create a workflow model](aem-forms-workflow.md#create-a-workflow-model). -->

#### Ir al paso {#go-to-step}

La variable **Ir al paso** permite especificar el paso siguiente en el modelo de flujo de trabajo que se va a ejecutar, según el resultado de una expresión de enrutamiento.

De forma similar al paso OR Split , puede definir la expresión de enrutamiento para el paso Goto mediante una definición de regla, un script ECMA o un script externo.

Puede utilizar variables para definir la expresión de enrutamiento mediante el editor de expresiones. Para obtener más información sobre el uso de expresiones de enrutamiento para el paso Ir a , consulte [Ir al paso](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/extending-workflows/workflows-step-ref.html#extending-aem#goto-step).

![Ir a la regla](assets/variables_goto_rule1_new.png)

En este ejemplo, el paso Ir a especifica la Solicitud de la Tarjeta de Crédito de Revisión como el siguiente paso si el valor de la variable **actiontaken** es igual a **Necesita más información**.

Para obtener más ejemplos sobre el uso de la definición de regla en el paso Ir a , consulte [Simulación de un bucle For](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/extending-workflows/workflows-step-ref.html#extending-aem#simulateforloop).

#### Pasos del flujo de trabajo centrado en Forms {#forms-workflow-centric-workflow-steps}

Todo [!DNL AEM Forms] Los pasos del flujo de trabajo admiten variables. Para obtener más información, consulte [Flujo de trabajo centrado en Forms en OSGi](aem-forms-workflow-step-reference.md).

### Pasos del flujo de trabajo sin compatibilidad con variables {#workflow-steps-without-support-for-variables}

Puede usar [MetaDataMap](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/metadata/MetaDataMap.html) para acceder a variables en pasos de flujo de trabajo que no admiten variables.

#### Recuperar el valor de variable {#retrieve-the-variable-value}

Utilice las siguientes API en el script de ECMA para recuperar los valores de variables existentes en función del tipo de datos:

| Tipo de datos variable | API |
|---|---|
| Primitiva (larga, doble, booleana, fecha y cadena) | workItem.getWorkflowData().getMetaDataMap().get(variableName, type) |
| Documento | Packages.com.adobe.aemfd.docmanager.Document doc = workItem.getWorkflowData().getMetaDataMap().get(&quot;docVar&quot;, Packages.com.adobe.aemfd.docmanager.Document.class); |
| XML | Packages.org.w3c.dom.Document xmlObject = workItem.getWorkflowData().getMetaDataMap().get(variableName, Packages.org.w3c.dom.Document.class); |
| Modelo de datos de formulario | Packages.com.adobe.aem.dermis.api.FormDataModelInstance fdmObject = workItem.getWorkflowData().getMetaDataMap().get(variableName, Packages.com.adobe.aem.dermis.api.FormDataModelInstance.class); |
| JSON | Packages.com.google.gson.JsonObject jsonObject = workItem.getWorkflowData().getMetaDataMap().get(variableName, Packages.com.google.gson.JsonObject.class); |


**Ejemplo**

Recupere el valor del tipo de datos de cadena mediante la siguiente API:

```javascript
workItem.getWorkflowData().getMetaDataMap().get(accname, Packages.java.lang.String)
```

#### Actualizar el valor de la variable {#update-the-variable-value}

Utilice la siguiente API en el script ECMA para actualizar el valor de una variable:

```javascript
workItem.getWorkflowData().getMetaDataMap().put(variableName, value)
```

**Ejemplo**

```javascript
workItem.getWorkflowData().getMetaDataMap().put(salary, 50000)
```

Actualiza el valor de la variable **salario** a 50000.

### Establecer variables para invocar flujos de trabajo {#apiinvokeworkflow}

Puede utilizar una API para establecer variables y pasarlas para invocar instancias de flujo de trabajo.

[workflowSession.startWorkflow](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/WorkflowSession.html#startWorkflow-com.adobe.granite.workflow.model.WorkflowModel-com.adobe.granite.workflow.exec.WorkflowData-java.util.Map-) utiliza model, wfData y metaData como argumentos. Utilice MetaDataMap para establecer el valor de la variable.

En esta API, la variable **variableName** se configura como **value** usando metaData.put(variableName, value);

```javascript
import com.adobe.granite.workflow.model.WorkflowModel;
import com.adobe.granite.workflow.metadata.MetaDataMap;
import com.adobe.aemfd.docmanager.Document;

/*Assume that you already have a workflowSession and modelId along with the payloadType and payload*/
WorkflowData wfData = workflowSession.newWorkflowData(payloadType, payload);
MetaDataMap metaData = wfData.getMetaDataMap();
metaData.put(variableName, value); //Create a variable "variableName" in your workflow model
WorkflowModel model = workflowSession.getModel(modelId);
workflowSession.startWorkflow(model, wfData, metaData);
```

**Ejemplo**

Inicializar el **doc** objeto document a una ruta (&quot;a/b/c&quot;) y establezca el valor de la variable **docVar** a la ruta almacenada en el objeto document.

```javascript
import com.adobe.granite.workflow.WorkflowSession;
import com.adobe.granite.workflow.exec.WorkflowData;
import com.adobe.granite.workflow.model.WorkflowModel;
import com.adobe.granite.workflow.metadata.MetaDataMap;
import com.adobe.aemfd.docmanager.Document;

/*This example assumes that you already have a workflowSession and modelId along with the payloadType and payload */
WorkflowData wfData = workflowSession.newWorkflowData(payloadType, payload);
MetaDataMap metaData = wfData.getMetaDataMap();
Document doc = new Document("/a/b/c");// initialize a document object
metaData.put("docVar",doc); //Assuming that you have created a variable "docVar" of type Document in your workflow model
WorkflowModel model = workflowSession.getModel(modelId);
workflowSession.startWorkflow(model, wfData, metaData);
```

## Editar una variable {#edit-a-variable}

1. En la página Editar flujo de trabajo , pulse el icono Variables disponible en la barra de tareas del modelo de flujo de trabajo. La sección Variables del panel izquierdo muestra todas las variables existentes.
1. Toque . ![editar](assets/edit.svg) (Editar) junto al nombre de la variable que desea editar.
1. Edite la información de la variable y pulse ![done_icon](assets/Smock_Checkmark_18_N.svg) para guardar los cambios. No se puede editar la variable **[!UICONTROL Nombre]** y **[!UICONTROL Tipo]** para una variable.

## Eliminar una variable {#delete-a-variable}

Antes de eliminar la variable , elimine todas las referencias de la variable del flujo de trabajo. Asegúrese de que la variable no se utilice en el flujo de trabajo.

Para eliminar una variable:

1. En la página Editar flujo de trabajo , pulse el icono Variables disponible en la barra de tareas del modelo de flujo de trabajo. La sección Variables del panel izquierdo muestra todas las variables existentes.
1. Pulse el icono Eliminar junto al nombre de la variable que desee eliminar.
1. Toque ![done_icon](assets/Smock_Checkmark_18_N.svg) para confirmar y eliminar la variable.

## Referencias {#references}

Para obtener más ejemplos sobre el uso de variables en [!DNL AEM Forms] Pasos del flujo de trabajo, consulte [Variables en flujos de trabajo AEM](https://helpx.adobe.com/experience-manager/kt/forms/using/authoring_variables_in_aem_forms-workflow1.html).
