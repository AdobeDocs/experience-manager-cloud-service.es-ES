---
title: ¿Cómo se crea un formulario adaptable?
description: Obtenga información sobre cómo crear un formulario adaptable mediante [!DNL Experience Manager Forms]. Los Forms adaptables son formularios HTML5 interactivos que agilizan la recopilación y el procesamiento de la información. Descubra más información sobre cómo crear un formulario adaptable basado en un modelo de datos de formulario y un esquema XML o JSON.
feature: Adaptive Forms
role: User, Developer
level: Beginner
exl-id: 38ca5eea-793b-420b-ae60-3a0bd83caf00
source-git-commit: bcd9f3cfe6c22a6db51a9e6f96576bb8cdde7d0c
workflow-type: tm+mt
source-wordcount: '1217'
ht-degree: 0%

---

# Creación de un formulario adaptable {#creating-an-adaptive-form}


Forms adaptable le permite crear formularios atractivos, interactivos, dinámicos y adaptables. AEM Forms proporciona un asistente fácil de usar para las empresas que crea rápidamente Forms adaptable. El asistente tiene una navegación por pestañas rápida para seleccionar fácilmente plantillas preconfiguradas, estilos, campos y opciones de envío para crear un formulario adaptable.

<!-- 

You can choose to create an Adaptive Form based on a form model or schema or without a form model. It is important to carefully choose the form model that not only suits your requirements but extends your existing infrastructural investments and assets. You get to choose from the following options to create an Adaptive Form: 

-->

![Asistente para crear un formulario adaptable](/help/release-notes/assets/wizard.png)

<!-- 

Adaptive Forms allow you to create forms that are engaging, responsive, dynamic, and adaptive. [!DNL AEM Forms] provides an intuitive wizard and out-of-the-box components to create Adaptive Forms. You can choose to create an Adaptive Form based on a form model or schema or without a form model. It is important to carefully choose the form model that not only suits your requirements but extends your existing infrastructural investments and assets. You get to choose from the following options to create an Adaptive Form:

* **Using a form data model**
  [Data integration](data-integration.md) lets you integrate entities and services from disparate data sources in to a Form Data Model that you can use to create Adaptive Forms. Choose Form Data Model if the Adaptive Form you are creating involves fetching and write data from and to multiple data source.

  <!--  * **Using an XDP Form Template**
   It is an ideal form model if you have investments in XFA-based or XDP forms. It provides a direct way to convert your XFA-based forms into Adaptive Forms. Any existing XFA rules are retained in the associated Adaptive Forms. The resulting Adaptive Forms support XFA constructs, such as validations, events, properties, and patterns. 

* **Using an XML Schema Definition (XSD) or a JSON Schema**
   XML and JSON schemas represent the structure in which data is produced or consumed by the back-end system in your organization. You can associate the schema to an Adaptive Form and use its elements to add dynamic content to the Adaptive Form. The elements of the schema will be available for use in the Data Model Objects tab of the Content browser when authoring Adaptive Forms.

* **Using none or without a form model**
   Adaptive Forms created with this option don’t use any form model. The data XML generated from such forms has flat structure with fields and corresponding values. -->

## Requisitos previos

Para crear un formulario adaptable, es necesario lo siguiente:

* **Una plantilla de formulario adaptable**: Una plantilla proporciona una estructura básica y define el aspecto (diseños y estilos) de un formulario adaptable. Tiene componentes con formato previo que contienen determinadas propiedades y estructura de contenido. También proporciona las opciones para definir un tema y una acción de envío. El tema define el aspecto y la presentación y la acción de envío define la acción que debe realizarse al presentar un formulario adaptable. Por ejemplo, el envío de los datos recopilados a un origen de datos. El servicio de nube admite dos tipos de plantillas:

   * **Plantilla editable**: Puede [crear una nueva](template-editor.md) o [importar una plantilla editable existente](migrate-to-forms-as-a-cloud-service.md). También puede implementar el [arquetipo más reciente](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/using.html?lang=en#:~:text=The%20AEM%20Archetype%20is%20made%20up%20of%20modules%3A,and%20request%20filters.%20it.testing%3A%20are%20Java-based%20integration%20testing.) para obtener algunas plantillas editables de ejemplo.
   * **Plantilla estática**: Estas son plantillas heredadas y solo se recomiendan para los clientes que migran de Adobe Managed Services (AMS) e instalaciones locales de AEM Forms (AEM 6.5 Forms o anteriores). Esto le permite seguir aprovechando su inversión existente en plantillas estáticas. Cuando se crea un nuevo formulario adaptable, se recomienda utilizar una plantilla editable.

* **Un tema de formulario adaptable**: Un tema contiene detalles de estilo para los componentes y paneles. Los estilos incluyen propiedades como colores de fondo, colores de estado, transparencia, alineación y tamaño. Al aplicar un tema, el estilo especificado se refleja en los componentes correspondientes. Puede [crear un tema nuevo](themes.md) o [importar un tema existente](import-export-forms-templates.md#uploading-a-theme). También puede implementar el [arquetipo más reciente](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/using.html#create-project) para algunos temas de muestra.

* **Permisos**: Agregue los usuarios a [!DNL forms-users] para proporcionarles permisos para crear un formulario adaptable. Para obtener una lista detallada de los formularios y grupos de usuarios específicos, consulte [Grupos y permisos](forms-groups-privileges-tasks.md).

1. Acceso [!DNL Experience Manager Forms] Instancia de autor. Puede ser una instancia de Cloud o una instancia de desarrollo local.

1. Introduzca sus credenciales en la página de inicio de sesión del Experience Manager.

   Cuando haya iniciado sesión, en la esquina superior izquierda, pulse **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms y documentos]**.

1. Toque **[!UICONTROL Crear]**  > **[!UICONTROL Forms adaptable]**. El asistente abre.s
1. En la pestaña Source , seleccione una plantilla:

   * Al seleccionar una plantilla editable, se selecciona automáticamente un tema y una acción de envío especificados en la plantilla, y la variable **[!UICONTROL Crear]** está activado. Puede ir a la **[!UICONTROL Estilo]** o **[!UICONTROL Envío]** fichas para seleccionar un tema diferente o enviar acción. Si la plantilla editable seleccionada no especifica ningún tema, el botón crear permanece desactivado. Puede ir a la **[!UICONTROL Estilos]** para seleccionar manualmente un tema.
   * Al seleccionar una plantilla estática, los datos, el estilo, el envío, la entrega y las opciones de vista previa no están disponibles. Cuando se crea un nuevo formulario adaptable, se recomienda utilizar una plantilla editable.

1. En la ficha Estilo, seleccione un tema:
   * Cuando la plantilla seleccionada especifica un tema, el tema se selecciona automáticamente en el asistente. También puede elegir un tema diferente de la ficha Estilo.
   * Si la plantilla seleccionada no especifica ningún tema, puede utilizar la ficha Estilo para elegir un tema. La variable **[!UICONTROL Crear]** solo se activa después de seleccionar un tema.
1. (Opcional) En la ficha Datos, seleccione un modelo de datos:
   * **Modelo de datos de formulario**: A [Modelo de datos de formulario](data-integration.md) permite integrar entidades y servicios de distintos orígenes de datos en un formulario adaptable. Elija Modelo de datos de formulario si el formulario adaptable que está creando implica recuperar y escribir datos desde y hacia varios orígenes de datos.
   * **Esquema JSON**: [esquema JSON](adaptive-form-json-schema-form-model.md) representa la estructura en la que el sistema back-end de su organización produce o consume datos. Puede asociar el esquema a un formulario adaptable y utilizar sus elementos para agregar contenido dinámico al formulario adaptable. Los elementos del esquema están disponibles para su uso en la pestaña Objetos del modelo de datos del navegador de contenido durante la creación de Forms adaptable y todos los campos también se añaden al formulario adaptable recién creado.

   De forma predeterminada, se seleccionan todos los campos del modelo de datos. Al crear el formulario adaptable, todos los campos del modelo de datos seleccionado se convierten a los componentes correspondientes del formulario adaptable. El asistente le proporciona casillas de verificación para seleccionar solo los campos que deben incluirse en el formulario adaptable.

   <!-- 
   
   If your JSON schema contains a fragment, the fragment is considered a single unit. You can select or deselect a complete fragment and all the fields of the fragment are selected or deselected accordingly. 
   
   -->

1. En la ficha Envío, seleccione una acción de envío:

   * Al seleccionar una plantilla, la acción de envío especificada en la plantilla se selecciona automáticamente. Puede seleccionar una acción de envío diferente en la pestaña Envío . La variable **[!UICONTROL Envío]** muestra todas las acciones de envío disponibles.

   * Cuando la plantilla seleccionada no especifica una acción de envío, puede utilizar la variable **[!UICONTROL Envío]** para seleccionar una acción de envío

1. (Opcional) En la pestaña Delivery , puede especificar una fecha de publicación o cancelación de publicación de un formulario adaptable.

1. Toque **[!UICONTROL Crear]**. Aparece un cuadro de diálogo para especificar el título, el nombre y la ubicación para guardar el formulario adaptable:

   * **[!UICONTROL Título]** Especifica el nombre para mostrar del formulario. El título le ayuda a identificar el formulario en la variable [!DNL Experience Manager Forms] interfaz de usuario.
   * **[!UICONTROL Nombre:]** Especifica el nombre del formulario. Se crea un nodo con el nombre especificado en el repositorio. A medida que empieza a escribir un título, el valor del campo de nombre se genera automáticamente. Puede cambiar el valor sugerido. El campo de nombre solo puede incluir caracteres alfanuméricos, guiones y guiones bajos. Todas las entradas no válidas se sustituyen por guiones.
   * **[!UICONTROL Ruta:]** Especifica la ubicación en la que se va a guardar el formulario adaptable. Puede guardar el formulario adaptable directamente en `/content/dam/formsanddocuments` o crear una carpeta como `/content/dam/formsanddocuments/adaptiveforms` para guardar un formulario adaptable. Asegúrese de crear la carpeta antes de utilizarla en la ruta de acceso. La variable **[!UICONTROL Ruta:]** no crea una carpeta automáticamente.

1. Toque **[!UICONTROL Crear]**. Se crea un formulario adaptable que se abre en el editor de Forms adaptable. El editor muestra el contenido disponible en la plantilla. También muestra la barra lateral para personalizar el formulario recién creado según las necesidades.

   En función del tipo de formulario adaptable, los elementos de formulario presentes en la variable <!--XFA form template, XML schema or --> El esquema JSON o el modelo de datos de formulario se muestran en la sección **[!UICONTROL Objetos del modelo de datos]** de la pestaña **[!UICONTROL Navegador de contenido]** en la barra lateral. También puede arrastrar y soltar estos elementos para crear el formulario adaptable.

<!-- ## Create an Adaptive Form based on a Form Data Model {#fdm}

[Data integration](data-integration.md) lets you integrate multiple data sources and bring their entities and services together to create a form data model. It is an extension of JSON schema. You can use a Form Data Model to create an Adaptive Form. The entities or data model objects configured in a Form Data Model are available as data model objects for form authoring. They are bound to respective data sources and used to prefill a form and write submitted data back to the respective data sources. You can also call services configured in a Form Data Model using Adaptive Form rules.

To use a Form Data Model for creating an Adaptive Form:

1. In Form Model tab on Add Properties screen, select **[!UICONTROL Form Data Model]** in the **[!UICONTROL Select From]** drop-down list.

   ![Create an Adaptive Form](assets/create-af-1-1.png)

1. Tap to expand **[!UICONTROL Select Form Data Model]**. All available form data models are listed.Select a from data model.

>[!NOTE]
>
>You can also change the Form Data Model for an Adaptive Form. For detailed steps, see [Edit Form Model properties of an Adaptive Form](#edit-form-model).

## Create an Adaptive Form based on XML or JSON schema {#create-an-adaptive-form-based-on-xml-or-json-schema}

XML and JSON schemas represent the structure in which data is produced or consumed by the back-end system in your organization. You can associate a schema to an Adaptive Form and use its elements to add dynamic content to the Adaptive Form. The elements of the schema are available in the Data Model Object tab of the content browser for authoring Adaptive Forms. You can drag-drop the schema elements to build the form.

See the following documents to understand how to design XML or JSON schema for authoring Adaptive Forms.

* [Creating Adaptive Forms using XML schema](adaptive-form-xml-schema-form-model.md)
* [Creating Adaptive Forms using JSON schema](adaptive-form-json-schema-form-model.md)

Do the following to use XML or JSON schema as form model for an Adaptive Form:

1. On the **[!UICONTROL Add Properties]** step of Adaptive Form creation page, tap on the **[!UICONTROL Form Model]** tab.
1. In the Form Model tab, select **[!UICONTROL Schema]** from the **[!UICONTROL Select From]** drop-down field.

1. Tap **[!UICONTROL Select Schema]** and do one of the following:

    * **[!UICONTROL Upload from disk]** - Select this option and tap Upload Schema Definition to browse and upload an XML schema or JSON schema from your file system. The uploaded schema file resides with the form and is not accessible to other Adaptive Forms.
    * **[!UICONTROL Search in repository]** - Select this option to select from the list of schema definition files available in the repository. Select the XML or JSON schema file as form model. The selected schema is associated with the form by reference and is accessible for use in other Adaptive Forms.

      Ensure that the JSON schema filename ends with **.schema.json**. For example: mySchema.schema.json

   ![Selecting XML or JSON schema](assets/upload-schema.png)
**Figure:** *Selecting XML or JSON schema*

1. (For XML schema only) After you select or upload an XML Schema, specify a root element of the selected XSD file to map with the Adaptive Form.

   ![Selecting XSD root element](assets/xsd-root-element.png)
**Figure:** *Selecting XSD root element*

>[!NOTE]
>
>You can also change the schema for an Adaptive Form. For detailed steps, see [Edit Form Model properties of an Adaptive Form](#edit-form-model). -->

## Editar propiedades del modelo de formulario de un formulario adaptable {#edit-form-model}

Puede cambiar el modelo de formulario para un formulario adaptable (basado en JSON o en el modelo de datos de formulario). No se puede cambiar de un modelo de formulario a otro.

1. Seleccione el formulario adaptable y pulse el botón **Propiedades** icono.
1. Abra el **[!UICONTROL Modelo de formulario]** y haga una de las siguientes acciones.

   * Si el formulario adaptable no tiene un modelo de formulario, puede elegir otro modelo de formulario y, en consecuencia, seleccionar <!-- a form template, --> Esquema XML o JSON, o modelo de datos de formulario.
   * Si el formulario adaptable se basa en un modelo de formulario, puede elegir otro <!-- form template, --> Esquema XML o JSON, o Modelo de datos de formulario para el mismo modelo de formulario.

1. Toque **[!UICONTROL Guardar]** para guardar las propiedades.
