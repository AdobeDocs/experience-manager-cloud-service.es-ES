---
title: ¿Cómo se utiliza el modelo de datos de formulario?
description: Aprenda a crear Forms adaptable y fragmentos de formulario adaptables basados en un modelo de datos de formulario. Profundizar al generar y editar datos de ejemplo para objetos del modelo de datos del formulario. Puede utilizar estos datos para obtener una vista previa y probar Forms adaptable.
feature: Form Data Model
role: User
level: Beginner, Intermediate
exl-id: 827ce457-6585-46fb-8e28-1d970a40d949
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '1010'
ht-degree: 0%

---

# Uso del modelo de datos de formulario {#use-form-data-model}

![integración de datos](do-not-localize/data-integeration.png)

[!DNL Experience Manager Forms] la integración de datos permite utilizar orígenes de datos de backend dispares para crear un Modelo de datos de formulario que se puede utilizar como esquema en varios Forms adaptable <!--and interactive communications--> flujos de trabajo. Requiere configurar los orígenes de datos y crear el Modelo de datos de formulario basado en los objetos y servicios del modelo de datos disponibles en los orígenes de datos. Para obtener más información, consulte:

* [[!DNL Experience Manager Forms] Integración de datos](data-integration.md)
* [Configuración de fuentes de datos](configure-data-sources.md)
* [Crear modelo de datos de formulario](create-form-data-models.md)
* [Trabajo con el modelo de datos de formulario](work-with-form-data-model.md)

Un modelo de datos de formulario es una extensión del esquema JSON que puede utilizar para:

* [Creación de Forms adaptable y fragmentos](#create-af)

<!--* [Create interactive communications and building blocks like text, list, and condition fragments](#create-ic)-->
* [Vista previa con datos de ejemplo](#preview-ic)
* [uso del servicio Modelo de datos de formulario](#prefill)
* [Escribir datos de formulario adaptable enviados de nuevo en orígenes de datos](#write-af)
* [Invocar servicios mediante reglas de formulario adaptable](#invoke-services)

## Creación de Forms adaptable y fragmentos {#create-af}

Puede crear [Forms adaptable](creating-adaptive-form.md) y fragmentos de formulario adaptables <!-- [Adaptive Form Fragments](adaptive-form-fragments.md) --> basado en un modelo de datos de formulario. Para utilizar un modelo de datos de formulario al crear un formulario adaptable o un fragmento de formulario adaptable, haga lo siguiente:

1. En la ficha Modelo de formulario de la pantalla Agregar propiedades, seleccione **[!UICONTROL Modelo de datos de formulario]** en el **[!UICONTROL Seleccionar de]** lista desplegable.

   ![create-af-1-1](assets/create-af-1-1.png)

1. Toque para expandir **[!UICONTROL Seleccionar modelo de datos de formulario]**. Se muestran todos los modelos de datos de formulario disponibles.

   Seleccione un modelo de datos de .

   ![create-af-2-1](assets/create-af-2-1.png)

1. (**Solo fragmentos de formulario adaptables**) Puede crear un fragmento de formulario adaptable basado en un único objeto de modelo de datos en un modelo de datos de formulario. Expandir **[!UICONTROL Definiciones del modelo de datos de formulario]** lista desplegable. Enumera todos los objetos del modelo de datos en el modelo de datos de formulario especificado. Seleccione un objeto del modelo de datos de la lista.

   ![create-af-3](assets/create-af-3.png)

   Una vez creado el formulario adaptable o el fragmento de formulario adaptable basado en un modelo de datos de formulario, los objetos del modelo de datos de formulario aparecen en el **[!UICONTROL Fuentes de datos]** del navegador de contenido en el editor de formularios adaptables.

   >[!NOTE]
   >
   >Para un fragmento de formulario adaptable, solo el objeto de modelo de datos seleccionado en el momento de la creación y los objetos de modelo de datos asociados aparecen en la ficha Fuentes de datos.

   ![data-model-object-tab](assets/data-model-objects-tab.png)

   Puede arrastrar y soltar objetos del modelo de datos en el formulario adaptable o en el fragmento para agregar campos de formulario. Los campos de formulario agregados conservan las propiedades de metadatos y el enlace con las propiedades de objeto del modelo de datos. El enlace garantiza que los valores de los campos se actualicen en los orígenes de datos correspondientes al envío del formulario y se rellenen previamente cuando se procesa el formulario.

<!-- ## Create interactive communications {#create-ic}

You can create an interactive communication based on a Form Data Model that you can use to prefill interactive communication with data from configured data sources. In addition, the building blocks of an interactive communication, such as text, list, and condition document fragments can be based on a form data model.

You can choose a Form Data Model when creating an interactive communication or a document fragment. The following image shows the General tab of the Create Interactive Communication dialog.

![create-ic](assets/create-ic.png)

General tab of Create Interactive Communication dialog

For more information, see:

[Create an interactive communication](create-interactive-communication.md)

[Text in Interactive Communications](texts-interactive-communications.md)

[Conditions in Interactive Communications](conditions-interactive-communications.md)

[List fragments](lists.md) -->

## Vista previa con datos de ejemplo {#preview-ic}

El editor del Modelo de datos de formulario permite generar y editar datos de ejemplo para objetos del modelo de datos en el modelo de datos de formulario. Puede utilizar estos datos para previsualizar y probar <!--interactive communications and--> Forms adaptable. Debe generar los datos de ejemplo antes de realizar la vista previa, tal como se describe en [Trabajo con el modelo de datos de formulario](work-with-form-data-model.md#sample).

<!--To preview an interactive communication with sample Form Data Model data:

1. On [!DNL  Experience Manager] author instance, navigate to **[!UICONTROL Forms > Forms & Documents]**.
1. Select an interactive communication and tap **[!UICONTROL Preview]** in the toolbar to select **[!UICONTROL Web Channel]**, **[!UICONTROL Print Channel]**, or **[!UICONTROL Both Channels]** to preview the interactive communication.
1. In the Preview [*channel*] dialog, ensure that **[!UICONTROL Test Data of Form Data Model]** is selected and tap **[!UICONTROL Preview]**.

The interactive communication opens with prefilled sample data.

![web-preview](assets/web-preview.png)-->

Para obtener una vista previa de un formulario adaptable con datos de ejemplo, abra el formulario adaptable en modo de autor y pulse **[!UICONTROL Vista previa]**.

## Relleno previo mediante el servicio Modelo de datos de formulario {#prefill}

[!DNL Experience Manager Forms] proporciona el servicio de rellenado previo del modelo de datos de formulario listo para usar que puede habilitar para Forms adaptable <!--and interactive communications--> basado en el modelo de datos de formulario. El servicio de rellenado previo consulta los orígenes de datos para los objetos del modelo de datos en el formulario adaptable <!--and interactive communication--> y, en consecuencia, prefieren los datos al procesar el formulario o la comunicación.

Para habilitar el servicio de cumplimentación previa del modelo de datos de formulario para un formulario adaptable, abra las propiedades del contenedor de formularios adaptables y seleccione **[!UICONTROL Servicio de relleno previo del modelo de datos de formulario]** de la variable **[!UICONTROL Servicio de precarga]** en el acordeón Básico . A continuación, guarde las propiedades.

![prefill-service](assets/prefill-service.png)

<!--To configure Form Data Model prefill service in an interactive communication, you can select Form Data Model Prefill Service in the Prefill Service drop-down while creating it or later by modifying the properties.

![edit-ic-props](assets/edit-ic-props.png)

Edit Properties dialog for an interactive communication-->

## Escribir datos de formulario adaptable enviados en fuentes de datos {#write-af}

Cuando un usuario envía un formulario basado en un modelo de datos de formulario, se puede configurar el formulario para que escriba los datos enviados de un objeto del modelo de datos en sus orígenes de datos. Para lograr este caso de uso, [!DNL Experience Manager Forms] proporcione [Acción de envío del modelo de datos de formulario](configuring-submit-actions.md), disponible de forma predeterminada solo para Forms adaptable basado en un modelo de datos de formulario. Escribe los datos enviados para un objeto de modelo de datos en su origen de datos.

Para configurar la acción de envío del modelo de datos de formulario, abra las propiedades del contenedor del formulario adaptable y seleccione **[!UICONTROL Enviar mediante el modelo de datos de formulario]** en la lista desplegable Enviar acción , en el acordeón Envío . A continuación, busque y seleccione un objeto de modelo de datos en el **[!UICONTROL Nombre del objeto del modelo de datos que se va a enviar]** lista desplegable. Guarde las propiedades.

Al enviar el formulario, los datos del objeto del modelo de datos configurado se escriben en el origen de datos correspondiente.

<!--![data-submission](assets/data-submission.png)-->

También puede enviar archivos adjuntos de formulario a un origen de datos mediante la propiedad de objeto del modelo de datos binario. Haga lo siguiente para enviar archivos adjuntos a una fuente de datos JDBC:

1. Agregue un objeto de modelo de datos que incluya una propiedad binaria al modelo de datos del formulario.
1. En el formulario adaptable, arrastre y suelte la **[!UICONTROL Archivo adjunto]** del navegador Componentes al formulario adaptable.
1. Toque para seleccionar el componente añadido y toque ![settings_icon](assets/configure-icon.svg) para abrir el navegador Propiedades del componente.
1. En el campo Referencia de enlace , pulse ![foldersearch_18](assets/folder-search-icon.svg) y desplácese hasta seleccionar la propiedad binaria añadida en el modelo de datos de formulario. Configure otras propiedades según corresponda.

   Toque ![botón de verificación](assets/save_icon.svg) para guardar las propiedades. El campo de datos adjuntos ahora está enlazado a la propiedad binaria del modelo de datos del formulario.

1. En la sección Envío de las propiedades del contenedor de formulario adaptable, active **[!UICONTROL Enviar archivos adjuntos del formulario]**. Envía el archivo adjunto en el campo de propiedad binaria al origen de datos al enviar el formulario.

## Invocar servicios en Forms adaptable mediante reglas {#invoke-services}

En un formulario adaptable basado en un modelo de datos de formulario, puede [crear reglas](rule-editor.md) para invocar servicios configurados en el modelo de datos de formulario. La variable **[!UICONTROL Invocar servicios]** en una regla, se enumeran todos los servicios disponibles en el Modelo de datos de formulario y se pueden seleccionar campos de entrada y salida para el servicio. También puede usar la variable **[!UICONTROL Definir valor]** tipo de regla para invocar un servicio del Modelo de datos de formulario y establecer el valor de un campo en el resultado devuelto por el servicio.

Por ejemplo, la siguiente regla invoca un servicio de obtención que toma el Id de empleado como entrada y los valores devueltos se rellenan en los campos correspondientes Id dependiente, Apellidos, Nombre y Género del formulario.

![invoke-service](assets/invoke-service.png)

Además, puede usar la variable `guidelib.dataIntegrationUtils.executeOperation` API para escribir un JavaScript en el editor de código del editor de reglas. <!-- For API details, see [API to invoke Form Data Model service](invoke-form-data-model-services.md).-->
