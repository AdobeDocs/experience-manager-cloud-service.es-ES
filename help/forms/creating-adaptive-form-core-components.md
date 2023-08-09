---
title: Cómo crear un formulario adaptable
description: Obtenga información sobre cómo crear un formulario adaptable mediante  [!DNL Experience Manager Forms]. Los formularios adaptables son formularios HTML5 interactivos que agilizan la recopilación y el procesamiento de la información. Descubra más información sobre cómo crear un formulario adaptable basado en un modelo de datos de formulario y un esquema XML o JSON.
feature: Adaptive Forms, Core Components
role: User, Developer
level: Beginner
exl-id: 1e812d93-4ba5-4589-b59b-2f564d754b0f
source-git-commit: 6d9ebc5410f6ffce0f0c7c7f4e9302b30e82b70b
workflow-type: tm+mt
source-wordcount: '2342'
ht-degree: 74%

---

# Crear un formulario adaptable {#creating-an-adaptive-form-core-components}

| Versión | Vínculo del artículo |
| -------- | ---------------------------- |
| AEM 6.5 | [Haga clic aquí.](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-core-components/create-an-adaptive-form-core-components.html) |
| AEM as a Cloud Service | Este artículo |


Los formularios adaptables le permiten crear formularios que son atractivos, receptivos, dinámicos y adaptables. AEM Forms proporciona un asistente fácil de usar para las empresas que crea rápidamente Forms adaptable. El asistente dispone de una navegación rápida por pestañas para seleccionar fácilmente plantillas, estilos, campos y opciones de envío preconfiguradas para crear un formulario adaptable.

Antes de empezar, obtenga información sobre el tipo de componentes de Forms disponibles para usted:

* [Componentes principales de formularios adaptables](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=es): son componentes estandarizados de captura de datos. Estos componentes proporcionan funcionalidades de personalización, un tiempo de desarrollo reducido y costes de mantenimiento más bajos para sus experiencias de inscripción digital. Un desarrollador puede personalizar y aplicar estilo fácilmente a estos componentes. Adobe recomienda aprovechar estos componentes modernos y ampliables para desarrollar formularios adaptables.

* [Componentes de base de formularios adaptables](creating-adaptive-form.md): estos son componentes clásicos (antiguos) de captura de datos. Puede seguir utilizándolos para editar su Formulario adaptable basado en componentes de base existentes. Si está creando formularios nuevos, Adobe recomienda utilizar los [Componentes principales de Formularios adaptables](creating-adaptive-form-core-components.md) para crear Formularios adaptables.

![Asistente para crear un formulario adaptable](/help/release-notes/assets/wizard.png)


## Requisitos previos

Para crear un formulario adaptable, es necesario lo siguiente:

* **Habilitar los componentes principales de formularios adaptables para su entorno**: al crear un nuevo programa, los componentes principales de formularios adaptables ya están habilitados para su entorno. Si tiene un entorno de formularios as a Cloud Service basado en el Arquetipo 39 o anterior, [Habilite los componentes principales de formularios adaptables para su entorno](enable-adaptive-forms-core-components.md). Al habilitar los componentes principales para su entorno, la plantilla y la temática de lienzo **Formularios adaptables (componente principal)** se añaden a su entorno. Si su versión del SDK de AEM es anterior a la 2023.02.0, [compruebe que tiene `prerelease` activado el indicador en su entorno](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/prerelease.html?lang=es#new-features), ya que los componentes principales de formularios adaptables formaban parte de la versión preliminar anterior a la 2023.02.0.

* **Una plantilla de formulario adaptable**: Una plantilla ofrece una estructura básica y define el aspecto (diseños y estilos) de un formulario adaptable. Tiene componentes con formato previo que contienen determinadas propiedades y estructura de contenido. También ofrece opciones para definir una temática y una acción de envío. La temática define la apariencia, y la acción de envío define la acción que debe realizarse al enviar un Formulario adaptable. Por ejemplo, enviar los datos recopilados a una fuente de datos. El servicio en la nube proporciona una plantilla OOTB, denominada en blanco:

   * La plantilla `blank` se incluye con cada nuevo programa as a Cloud Service de AEM Forms.
   * Puede instalar el paquete de referencia mediante el Administrador de paquetes para agregar la plantilla `blank` a su programa as a Cloud Service de AEM Forms.
   * También puede [crear una nueva plantilla de formularios adaptables (componentes principales)](template-editor.md) desde cero.
   * También puede implementar [plantillas de muestra](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/sample-themes-templates-form-data-models-core-components.html) a su entorno. Esto le ayuda a empezar a crear formularios rápidamente.

* **Una temática de formulario adaptable**: Una temática contiene detalles de estilo para los componentes y paneles. Los estilos incluyen propiedades como colores de fondo, colores de estado, transparencia, alineación y tamaño. Al aplicar una temática, el estilo especificado se refleja en los componentes correspondientes.  La plantilla `Canvas` se incluye con cada nuevo programa as a Cloud Service de AEM Forms. También puede implementar [temas de muestra](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/sample-themes-templates-form-data-models-core-components.html) a su entorno. Esto le ayudará a dar estilo a los formularios y le proporcionará una estructura base para crear o personalizar una temática según sus necesidades empresariales.

  <!-- * You can install the reference package, via package manager, to add the `Canvas` template to your AEM Forms as a Cloud Service program.
    * You can also [create a new Adaptive Forms theme (Core Components)](template-editor.md) and deploy it to your AEM Forms as a Cloud Service program. -->

* **Permisos**: añada sus usuarios al grupo [!DNL forms-users]. Los miembros del grupo [!DNL forms-users] tienen permisos para crear un formulario adaptable. Para obtener una lista detallada de los grupos de usuarios específicos de los formularios, consulte [Grupos y permisos](forms-groups-privileges-tasks.md).

<!--
>[!NOTE]
>
>
> In addition to the given themes and templates when you enable Core Components, you can also deploy the latest out-of-the box [sample themes and templates](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/sample-themes-templates-form-data-models-core-components.html) to your AEM environment for use in Core Components based Adaptive Forms.
-->

## Crear un formulario adaptable  {#create-an-adaptive-form-core-components}

1. Inicie sesión en su [!DNL Experience Manager Forms] Instancia de autor. Puede ser una instancia de nube o una instancia de desarrollo local.

1. Introduzca sus credenciales en la página de inicio de sesión de Experience Manager. Cuando haya iniciado sesión, en la esquina superior izquierda, pulse **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Formularios]** > **[!UICONTROL Formularios y documentos]**.

1. Pulse **[!UICONTROL Crear]** > **[!UICONTROL Formularios adaptables]**. Se abre el asistente. En la pestaña Fuente, seleccione una plantilla:

   ![Plantilla de componentes principales](/help/forms/assets/core-components-template.png)

   Al seleccionar una plantilla, se selecciona automáticamente un tema y una acción de envío especificados en la plantilla, y se habilita el botón **[!UICONTROL Crear]**. Puede ir a las pestañas **[!UICONTROL Estilo]** o **[!UICONTROL Envío]** para seleccionar un tema o acción de envío diferente. Si la plantilla seleccionada no especifica ninguna temática, el botón Crear permanece desactivado. Puede ir a la pestaña **[!UICONTROL Estilos]** para seleccionar manualmente una temática.

   >[!NOTE]
   >
   >
   > Si no tiene la plantilla de **Formularios adaptables (componente principal)** en su entorno, [Habilite los componentes principales de formularios adaptables para su entorno](setup-local-development-environment.md#enable-adaptive-forms-core-components-for-an-existing-aem-archetype-based-project). Al habilitar los componentes principales para su entorno, la plantilla de **Formularios adaptables (componente principal)** se agrega al entorno.

1. En la pestaña **[!UICONTROL Estilo]**, seleccione una temática:

   * Cuando la plantilla seleccionada especifica una temática, la temática se selecciona automáticamente en el asistente. También puede elegir una temática diferente de la pestaña Estilo.

   * Si la plantilla seleccionada no especifica ninguna temática, puede utilizar la pestaña Estilo para elegir una temática. El botón **[!UICONTROL Crear]** solo se activa después de seleccionar una temática.

1. (Opcional) En la pestaña Datos, seleccione un modelo de datos:

   * **Modelo de datos de formulario**: A [El modelo de datos de formulario](data-integration.md) permite integrar entidades y servicios de distintas fuentes de datos en un formulario adaptable. Elija modelo de datos de formulario si el formulario adaptable que está creando implica recuperar y escribir datos desde y hacia varias fuentes de datos.

   * **Esquema JSON**: [Esquema JSON](adaptive-form-json-schema-form-model.md) Nuestro formulario adaptable basado en componentes principales permite una integración optimizada con el sistema back-end de su organización al proporcionar la capacidad de asociar un esquema JSON, que representa la estructura de los datos que se producen o consumen. Esta asociación permite a los autores añadir contenido de forma dinámica al formulario adaptable mediante los elementos del esquema. Los elementos del esquema son fácilmente accesibles en la pestaña Objetos del modelo de datos del Explorador de contenido durante el proceso de creación y todos los campos se añaden automáticamente a cualquier formulario adaptable recién creado.

   De forma predeterminada, todos los campos del esquema JSON asociado se seleccionan automáticamente y se convierten en los correspondientes componentes de formulario adaptable, lo que optimiza el proceso de creación. El asistente ofrece la comodidad añadida de permitirle elegir selectivamente qué campos se deben incluir en el formulario adaptable mediante el uso de casillas de verificación.

1. En la pestaña **[!UICONTROL Envío]**, seleccione una acción de envío:

   * Al seleccionar una plantilla, la acción de envío especificada en la plantilla se selecciona automáticamente. Puede seleccionar una acción de envío diferente en la pestaña Envío. La pestaña **[!UICONTROL Envío]** muestra todas las acciones de envío disponibles.

   * Cuando la plantilla seleccionada no especifica una acción de envío, puede utilizar la pestaña **[!UICONTROL Envío]** para seleccionar una acción de envío.

1. (Opcional) En la pestaña **[!UICONTROL Entrega]**, puede especificar una fecha de publicación o cancelación de publicación de un formulario adaptable.

1. Pulse **[!UICONTROL Crear]**. Aparece un cuadro de diálogo para especificar el título, el nombre y la ubicación para guardar el Formulario adaptable:

   * El **[!UICONTROL Título]** especifica el nombre que se muestra en el formulario. El título le ayuda a identificar el formulario en la interfaz de usuario de [!DNL Experience Manager Forms].
   * **[!UICONTROL Nombre:]** Especifica el nombre del formulario. Se crea un nodo con el nombre especificado en el repositorio. A medida que empieza a escribir un título, el valor del campo de nombre se genera automáticamente. Puede cambiar el valor sugerido. El campo de nombre solo puede incluir caracteres alfanuméricos, guiones y guiones bajos. Todas las entradas no válidas se sustituyen por guiones.
   * **[!UICONTROL Ruta:]** Especifica la ubicación en la que se va a guardar el formulario adaptable. Puede guardar el Formulario adaptable directamente en `/content/dam/formsanddocuments` o crear una carpeta como `/content/dam/formsanddocuments/adaptiveforms` para guardar un Formulario adaptable. Asegúrese de crear la carpeta antes de utilizarla en la ruta. El campo **[!UICONTROL Ruta]** no crea una carpeta automáticamente.

1. Pulse **[!UICONTROL Crear]**. Se crea un formulario adaptable que se abre en el editor de formularios adaptables. El editor muestra el contenido disponible en la plantilla.  En base al tipo de formulario adaptable, los elementos del formulario presentes en el <!--XFA form template, XML schema or --> esquema JSON o el modelo de datos de formulario asociado se muestran en la pestaña **[!UICONTROL Objetos del modelo de datos]** del **[!UICONTROL Explorador de contenido]** en la barra lateral. También puede arrastrar y soltar estos elementos para crear su formulario adaptable.

Ahora, puede arrastrar y soltar el [Componentes principales de Forms adaptable](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=es) al contenedor de Forms adaptable para diseñar y crear el formulario. También puede visitar [https://aemcomponents.dev/](https://aemcomponents.dev/) para ver los componentes principales disponibles en acción.

## Configurar la acción de envío para un formulario adaptable {#configure-submit-action-for-form}

Una acción de envío permite elegir el destino de los datos capturados mediante un formulario adaptable. Se activa una acción de envío cuando un usuario hace clic en el botón Enviar en un formulario adaptable. Los formularios adaptables incluyen algunas acciones de envío listas para usar. También puede ampliar las acciones de envío predeterminadas para crear su propia acción de envío personalizada. Para configurar una acción de envío para el formulario:

1. Abra el Explorador de contenido y seleccione **[!UICONTROL Contenedor de guía]** del formulario adaptable.
1. Haga clic en las propiedades del contenedor de guía ![Propiedades de guía](/help/forms/assets/configure-icon.svg) icono. Se abrirá el cuadro de diálogo Contenedor de formulario adaptable.

1. Haga clic en  **[!UICONTROL Envío]** pestaña.

   ![Haga clic en el icono Llave inglesa para abrir el cuadro de diálogo Contenedor de formulario adaptable y configurar una acción de envío](/help/forms/assets/adaptive-forms-submit-message.png)

1. Seleccione y configure un **[!UICONTROL Acción de envío]**, según sus necesidades. Para obtener información detallada sobre las acciones de envío, consulte [Acción de envío del formulario adaptable](/help/forms/configuring-submit-actions.md)

<!--
    
    ![Click the Wrench icon to open Adaptive Form Container dialog box to configure Data Models for the Adaptive Form Container component](/help/forms/assets/adaptive-forms-container.png)

-->

## Redirigir al usuario a una página o mostrar un mensaje de agradecimiento al enviar el formulario

Al enviar un formulario, puede redirigir al usuario a otra página web o a un mensaje. Para redirigir al usuario o configurar el mensaje de agradecimiento:

1. Abra el Explorador de contenido y seleccione **[!UICONTROL Contenedor de guía]** del formulario adaptable.
1. Haga clic en las propiedades del contenedor de guía ![Propiedades de guía](/help/forms/assets/configure-icon.svg) icono. Se abrirá el cuadro de diálogo Contenedor de formulario adaptable.
1. Abra la pestaña **[!UICONTROL Envío]**.

   ![Haga clic en el icono Llave inglesa para abrir el cuadro de diálogo Contenedor de formulario adaptable y configurar una página de redireccionamiento o un mensaje de agradecimiento](/help/forms/assets/adaptive-forms-redirect-message.png)

   * Para configurar una URL de redireccionamiento, por ejemplo, en la opción Enviar, seleccione **[!UICONTROL Redirigir a URL]** y examine y seleccione una página de AEM Sites, o proporcione la URL de una página externa.

   * Para configurar un mensaje personalizado o de agradecimiento, para en la opción Enviar, seleccione **[!UICONTROL Mostrar mensaje]** y proporcione un mensaje en la **[!UICONTROL Contenido del mensaje]** cuadro. Es un cuadro de texto enriquecido, puede utilizar la opción de pantalla completa para ver todos los elementos de texto enriquecido disponibles.

## Configurar un esquema o un modelo de datos de formulario para un formulario adaptable{#configure-schema-or-data-model-for-form}

Puede utilizar el modelo de datos del formulario para conectar un formulario a una fuente de datos para enviar y recibir datos en función de las acciones del usuario. También puede conectar un formulario a un esquema JSON para recibir los datos enviados en un formato predefinido. En función del requisito, conecte el formulario a un esquema JSON o a un modelo de datos de formulario:

* [Crear un esquema JSON y cargarlo en su entorno](/help/forms/adaptive-form-json-schema-form-model.md)
* [Crear modelo de datos de formulario](/help/forms/create-form-data-models.md)

### Configurar un esquema JSON o un modelo de datos de formulario para el formulario

Para configurar un esquema JSON o un modelo de datos de formulario para su formulario:

1. Abra el Explorador de contenido y seleccione **[!UICONTROL Contenedor de guía]** del formulario adaptable.
1. Haga clic en las propiedades del contenedor de guía ![Propiedades de guía](/help/forms/assets/configure-icon.svg) icono. Se abrirá el cuadro de diálogo Contenedor de formulario adaptable.
1. Abra el **[!UICONTROL Modelo de datos]** pestaña.

   ![Haga clic en el icono Llave inglesa para abrir el cuadro de diálogo Contenedor de formulario adaptable y configurar un esquema JSON o un modelo de datos de formulario](/help/forms/assets/adaptive-forms-select-form-data-model-or-json-schema.png)

1. Seleccione y configure un esquema JSON o un modelo de datos de formulario según sus necesidades:

   * Al seleccionar la variable **[!UICONTROL Modelo de formulario]**, utilice la opción **[!UICONTROL Seleccionar modelo de datos de formulario]** para seleccionar un modelo de datos de formulario preconfigurado.
   * Al seleccionar la opción **[!UICONTROL Esquema]**, utilice la opción **[!UICONTROL Esquema]** para seleccionar un esquema JSON para el formulario.

1. Haga clic en **[!UICONTROL Listo]**.

## Configurar un servicio de rellenado previo  {#configure-prefill-service-for-form}

Puede utilizar el servicio de cumplimentación previa para rellenar automáticamente los campos de un formulario adaptable utilizando los datos existentes. Cuando un usuario abre un formulario, los valores de esos campos ya han sido rellenados. Puede hacer lo siguiente:

* [Crear un servicio de rellenado previo personalizado](/help/forms/prepopulate-adaptive-form-fields.md)
* [Servicio de rellenado previo de modelo de datos de formulario](#fdm-prefill-service)

### Utilice el servicio de prerrellenado del modelo de datos de formulario para rellenar previamente los campos de un formulario adaptable {#fdm-prefill-service}

Puede utilizar el servicio de prerrellenado del modelo de datos de formulario para rellenar previamente los campos de un formulario adaptable mediante un modelo de datos de formulario o un servicio de prerrellenado personalizado. El servicio de rellenado previo del modelo de datos de formulario utiliza el [Obtener servicio del modelo de datos de formulario configurado](work-with-form-data-model.md#add-data-model-objects-and-services-add-data-model-objects-and-services) para recuperar datos. Para utilizar el servicio de rellenado previo del modelo de datos de formulario de un formulario adaptable, haga lo siguiente:

1. Abra el Explorador de contenido y seleccione **[!UICONTROL Contenedor de guía]** del formulario adaptable.
1. Haga clic en las propiedades del contenedor de guía ![Propiedades de guía](/help/forms/assets/configure-icon.svg) icono. Se abrirá el cuadro de diálogo Contenedor de formulario adaptable.
1. Haga clic en el icono de las ![Propiedades del contenedor del formulario adaptable](/help/forms/assets/configure-icon.svg). Se abre el cuadro de diálogo Contenedor de formulario adaptable para configurar modelos de datos.
   ![Haga clic en el icono Llave inglesa para abrir el cuadro de diálogo Contenedor de formulario adaptable y configurar una página de redireccionamiento o un mensaje de agradecimiento](/help/forms/assets/adaptive-forms-container-prefill-service.png)
1. Seleccionar modelo de datos de formulario. Abra la pestaña **[!UICONTROL Básico]**. En el servicio de relleno previo, seleccione **[!UICONTROL Servicio de prerrellenado del modelo de datos de formulario]**.
1. Haga clic en **[!UICONTROL Listo]**. El formulario adaptable ahora está configurado para utilizar el prerrellenado del modelo de datos de formulario. Ahora puede usar la variable [editor de reglas](rule-editor.md) para crear reglas para rellenar previamente los campos del formulario.

## Edición de las propiedades del modelo de formulario de un formulario adaptable {#edit-form-model}

1. Seleccione el formulario adaptable y pulse ![Información de página](/help/forms/assets/Smock_Properties_18_N.svg) > **[!UICONTROL Abrir propiedades]**. Se abre la página Propiedades del formulario.

1. Vaya a la pestaña **[!UICONTROL Modelo de formulario]** y elija un modelo de formulario. Si el formulario adaptable no cuenta con un modelo de formulario, tiene la posibilidad de elegir un esquema JSON o un modelo de datos de formulario. Por otro lado, si el formulario adaptable ya se basa en un modelo de formulario, tiene la opción de cambiar a otro modelo de formulario del mismo tipo. Por ejemplo, si el formulario utiliza un esquema JSON, puede cambiar fácilmente a otro esquema JSON y, del mismo modo, si el formulario utiliza un modelo de datos de formulario, puede cambiar a otro modelo de datos de formulario.

1. Pulse **[!UICONTROL Guardar]** para guardar las propiedades.


## Ver siguiente

* [Crear estilos o temáticas para los formularios](using-themes-in-core-components.md)
* [Agregar un comportamiento dinámico a los formularios mediante el editor de reglas](rule-editor.md)
* [Definir la presentación de los formularios para diferentes tamaños de pantalla y tipos de dispositivos](/help/sites-cloud/authoring/features/responsive-layout.md)
* [Plantillas de temáticas de muestra y modelos de datos de formulario](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/sample-themes-templates-form-data-models-core-components.html)


## Artículo relacionado {#related-article}

* [Crear un formulario adaptable independiente basado en componentes principales](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/creating-adaptive-form-core-components.html?lang=es)
