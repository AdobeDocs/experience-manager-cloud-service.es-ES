---
title: Cómo guardar el formulario adaptable basado en componentes principales como borrador
description: Aprenda a guardar formularios adaptables basados en componentes principales como borrador, a crear un portal de Forms y a utilizar componentes principales listos para usar en una página de AEM Sites.
feature: Adaptive Forms, Core Components
exl-id: c0653bef-afeb-40c1-b131-7d87ca5542bc
role: User, Developer, Admin
source-git-commit: 52b87073cad84705b5dc0c6530aff44d1e686609
workflow-type: tm+mt
source-wordcount: '1053'
ht-degree: 15%

---


# Guardar formulario adaptable basado en componentes principales como borrador {#save-af-form}

Guardar un formulario adaptable como borrador es una función esencial que mejora la eficacia y precisión del usuario. Esta funcionalidad permite a los usuarios guardar el progreso y volver para completar las tareas más adelante sin perder la información introducida. Proporcionar una opción `save-as-draft` garantiza flexibilidad para administrar el tiempo, reduce el riesgo de pérdida de datos y mantiene la precisión de los envíos. Puede guardar los formularios como borradores para completarlos más adelante.

## Consideraciones

* [Habilite los componentes principales de Forms adaptable para su entorno.](/help/forms/enable-adaptive-forms-core-components.md)

* Asegúrese de que el componente principal [está configurado en la versión 3.0.24 o posterior](https://github.com/adobe/aem-core-forms-components) para usar esta característica.
* Asegúrese de tener una cuenta de [Azure Storage y una clave de acceso](https://learn.microsoft.com/en-us/azure/storage/common/storage-account-keys-manage?tabs=azure-portal) para autorizar el acceso a la cuenta de Azure Storage.

## Guardar un formulario adaptable como borrador

La integración de datos [!DNL Experience Manager Forms] (data-integration.md) proporciona la configuración de almacenamiento [!DNL Azure] para integrar formularios con los servicios de almacenamiento [!DNL Azure]. El modelo de datos de formulario (FDM) se puede usar para crear Forms adaptable que interactúe con el servidor [!DNL Azure] para habilitar los flujos de trabajo empresariales.

Para guardar el formulario como borrador, asegúrese de que dispone de una cuenta de almacenamiento de Azure y una clave de acceso para autorizar el acceso a la cuenta de almacenamiento de [!DNL Azure]. Para guardar el formulario como borrador, realice los siguientes pasos:

1. [Crear configuración de almacenamiento de Azure](#create-azure-storage-configuration)
1. [Configuración del conector de almacenamiento unificado para el portal de Forms](#configure-usc-forms-portal)
1. [Crear una regla para guardar un formulario adaptable como borrador](#rule-to-save-adaptive-form-as-draft)


### 1. Crear configuración de almacenamiento de Azure {#create-azure-storage-configuration}

Una vez que tenga una cuenta de almacenamiento de Azure y una clave de acceso para autorizar el acceso a la cuenta de almacenamiento [!DNL Azure], realice los siguientes pasos para crear la configuración de almacenamiento de Azure:

1. Vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Almacenamiento de Azure]**.

   ![Selección de tarjeta de almacenamiento de Azure](/help/forms/assets/save-form-as-draft-azure-card.png)

1. Seleccione una carpeta de configuración para crear la configuración y seleccione **[!UICONTROL Crear]**.

   ![Seleccionar carpeta de configuración de almacenamiento de Azure](/help/forms/assets/save-form-as-draft-select-config-folder.png)

1. Especifique un título para la configuración en el campo **[!UICONTROL Título]**.
1. Especifique el nombre de la cuenta de almacenamiento [!DNL Azure] en los campos **[!UICONTROL Cuenta de almacenamiento de Azure]** y **[!UICONTROL Clave de acceso de Azure]**.

   ![Configuración de almacenamiento de Azure](/help/forms/assets/save-form-as-draft-azure-storage.png)

1. Haga clic en **Guardar**.

>[!NOTE]
>
> Puede recuperar la **[!UICONTROL cuenta de almacenamiento de Azure]** y la **[!UICONTROL clave de acceso de Azure]** del [Portal de Microsoft Azure](https://learn.microsoft.com/en-us/azure/storage/common/storage-account-keys-manage?tabs=azure-portal).


### 2. Configurar el conector de almacenamiento unificado para el portal de Forms {#configure-usc-forms-portal}

Después de crear correctamente la Configuración de almacenamiento de Azure, configure el Conector de almacenamiento unificado para el portal de Forms, para ello, siga estos pasos:

1. Vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Formularios]** > **[!UICONTROL Conector de almacenamiento unificado]**.

   ![Almacenamiento de conector unificado](/help/forms/assets/save-form-as-draft-unified-connector.png)

1. En el **[!UICONTROL portal de Forms]**, seleccione **[!UICONTROL Azure]** de la lista desplegable **[!UICONTROL Almacenamiento]**.
1. Especifique la ruta de configuración [para la configuración del almacenamiento de Azure](#create-azure-storage-configuration) en el campo **[!UICONTROL Ruta de configuración del almacenamiento]**.

   ![Configuración de almacenamiento del conector unificado](/help/forms/assets/save-form-as-draft-unified-connector-storage.png)

1. Seleccione **[!UICONTROL Guardar]** y, a continuación, seleccione **[!UICONTROL Publish]** para publicar la configuración.

### 3. Crear reglas para guardar un formulario adaptable como borrador {#rule-to-save-adaptive-form-as-draft}

Para guardar un formulario como borrador, cree una regla **Guardar formulario** en un componente de formulario, como un botón. Cuando se hace clic en el botón, la regla entra en déclencheur y el formulario se guarda como borrador. Realice los siguientes pasos para crear la regla **Guardar formulario** en un componente de botón:

1. En la instancia Autor, abra un formulario adaptable en modo de edición.
1. En el panel izquierdo, seleccione el icono ![Componentes](assets/components_icon.png) y arrastre el componente **[!UICONTROL Botón]** al formulario.
1. Seleccione el componente **[!UICONTROL Botón]** y, a continuación, seleccione el icono ![Configurar](assets/configure_icon.png).
1. Seleccione el icono **[!UICONTROL Editar reglas]** para abrir el Editor de reglas.
1. Seleccione **[!UICONTROL Crear]** para configurar y crear la regla.
1. En la sección **[!UICONTROL Cuándo]**, seleccione **se hace clic** y en la sección **[!UICONTROL Entonces]**, seleccione la opción **Guardar formulario**.
1. Seleccione **[!UICONTROL Listo]** para guardar la regla.

![Crear regla para el botón](/help/forms/assets/save-form-as-drfat-create-rule.png)

Cuando obtiene una vista previa de un formulario adaptable, lo rellena y hace clic en el botón **Guardar formulario**, el formulario se guarda como borrador para su uso posterior.

## Componente Borradores y envíos para enumerar borradores en la página de AEM Sites

AEM Forms proporciona el componente de portal **Borradores y envíos** de forma predeterminada para mostrar los formularios guardados en las páginas de AEM Sites. El componente **Borradores y envíos** muestra los formularios guardados como borradores para su posterior finalización, así como los formularios enviados. Este componente ofrece una experiencia personalizada para cualquier usuario que haya iniciado sesión con una lista de los borradores y los envíos relacionados con el Forms adaptable creado por el usuario.

Puede utilizar los componentes listos para usar del portal de Forms para enumerar borradores de formulario en la página de AEM Sites. Siga estos pasos para usar el componente de portal **Borradores y envíos**:

1. [Habilitar borradores y envíos en el componente de portal de Forms](#enable-component)
2. [Agregar el componente Borradores y envíos en la página de AEM Sites](#Add-drafts-submissions-component)
3. [Configurar Borradores y envíos](#configure-drafts-submissions-component)

### 1. Habilitar borradores y envíos en el componente del portal de Forms{#enable-component}

Para habilitar el componente **[!UICONTROL Borradores y envíos]** en la directiva de plantillas, realice los siguientes pasos:

1. Abra la página de AEM Sites en modo **Editar**.
1. Vaya a la **[!UICONTROL Información de la página]** > **[!UICONTROL Editar plantilla]**
   ![Editar directiva de plantilla](/help/forms/assets/save-form-as-draft-edit-template.png)

1. AEM Haga clic en la **[!UICONTROL directiva]** y seleccione la casilla de verificación **[!UICONTROL Borradores y envíos]** bajo el **[Nombre de proyecto de tipo de archivo] - Forms y el portal de comunicaciones**.

   ![Selección de directiva](/help/forms/assets/save-form-as-draft-enable-policy.png)

1. Haga clic en **[!UICONTROL Listo]**.

Una vez habilitado un componente del portal, puede utilizarlo en la instancia Autor de la página de AEM Sites.

### 2. Agregar el componente Borradores y envíos en la página de AEM Sites{#Add-drafts-submissions-component}

Puede crear y personalizar el portal de Forms en sitios web creados mediante AEM si agrega y configura los componentes del portal. Asegúrese de que el componente [Borradores y envíos está habilitado](#enable-component) antes de usarlos en la página de AEM Sites.

Para agregar un componente, arrástrelo y suéltelo desde el panel de componentes **Borradores y envíos** al contenedor de diseño de la página, o bien, seleccione el icono Agregar en el contenedor de diseño y agregue el componente desde el cuadro de diálogo **[!UICONTROL Insertar nuevo componente]**.

![Agregar componente de borrador y envío](/help/forms/assets/save-form-as-draft-add-dns.png)

### 3. Configurar el componente Borradores y envíos {#configure-drafts-submissions-component}

El componente **Borradores y envíos** muestra los formularios guardados como borrador para completarlos posteriormente y enviarlos. Para configurar **Borradores y envíos**, realice los siguientes pasos:
1. Seleccione el componente **Borradores y envíos**.
1. Haga clic en el icono ![Configurar](assets/configure_icon.png) y aparecerá el cuadro de diálogo.
1. En el cuadro de diálogo **[!UICONTROL Borradores y envíos]**, especifique lo siguiente:
   * **Título** Para identificar un componente en una página de Sites y de forma predeterminada, el título aparece en la parte superior del componente.
   * **Tipo**: para indicar la lista de formularios como formularios en borrador o enviados.
   * **Diseño**: para mostrar una lista de formularios en borrador o enviados en formato de tarjeta o lista.

   ![Propiedades del componente Borradores y envíos](/help/forms/assets/save-form-as-draft-dns-properties.png)

1. Haga clic en **Listo**.

Cuando se selecciona **[!UICONTROL Seleccionar tipo]** como **Borrador de Forms**, aparecen los formularios guardados como borradores:
![Icono Borradores](assets/drafts-component.png)

Cuando se selecciona **[!UICONTROL Seleccionar tipo]** como **Forms enviado**, aparecen los formularios enviados:

![Icono Envíos](assets/submission-listing.png)

Puede abrir el formulario haciendo clic en el formulario correspondiente.

<!--

### Configure Search & Lister Component {#configure-search-lister-component}

The Search & Lister component is used to list adaptive forms on a page and to implement search on the listed forms. 

![Search and Lister icon](assets/search-and-lister-component.png)

To configure, select the component and then select the ![Configure icon](assets/configure_icon.png). The [!UICONTROL Search and Lister] dialog opens.

1. In the [!UICONTROL Display] tab, configure the following:
    * In **[!UICONTROL Title]**, specify the title for the Search & Lister component. An indicative title enables the users perform quick search across the list of forms.
    * From the **[!UICONTROL Layout]** list, select the layout to represent the forms in card or list format.
    * Select **[!UICONTROL Hide Search]** and **[!UICONTROL Hide Sorting]** to hide the search and sort by features.
    * In **[!UICONTROL Tooltip]**, provide the tooltip that appears when you hover over the component. 
1. In the [!UICONTROL Asset Folder] tab, specify the location from where the forms are pulled and listed on the page. You can configure multiple folder locations.
1. In the [!UICONTROL Results] tab, configure the maximum number of forms to display per page. The default is eight forms per page.

### Configure Link Component {#configure-link-component}

The link component enables you to provide links to an adaptive form on the page. To configure, select the component and then select the ![Configure icon](assets/configure_icon.png). The [!UICONTROL Edit Link Component] dialog opens.

1. In the [!UICONTROL Display] tab, provide the link caption and tooltip to ease identification of the forms represented by the link.
1. In the [!UICONTROL Asset Info] tab, specify the repository path where the asset is stored. 
1. In the [!UICONTROL Query Params] tab, specify the additional parameters in the key-value pair format. When the link is clicked, these additional parameters and passed along with the form.

## Configure Asynchronous Form Submission Using Adobe Sign {#configure-asynchronous-form-submission-using-adobe-sign}

You can configure to submit an adaptive form only when all the recipients have completed the signing ceremony. Follow the steps below to configure the setting using Adobe Sign.

1. In the author instance, open an Adaptive Form in the edit mode.
1. From the left pane, select the Properties icon and expand the **[!UICONTROL ELECTRONIC SIGNTATURE]** option.
1. Select **[!UICONTROL Enable Adobe Sign]**. Various configuration options display. 
1. In the [!UICONTROL Submit the form] section, select the **[!UICONTROL after every recipient completes signing ceremony]** option to configure the Submit Form action, where the form is first sent to all the recipients for signing. Once all the recipients have signed the form, only then the form is submitted. 

## Save Adaptive Forms As Drafts {#save-adaptive-forms-as-drafts}

You can save forms as Drafts for completing them later. There are two ways in which a form is saved as a draft:

* Create a "Save Form" rule on a form component, for example, a button. On clicking the button, the rule triggers and the form are saved a draft.
* Enable Auto-Save feature, which saves the form as per the specified event or after a configured interval of time.

### Create Rules to Save an Adaptive Form as Draft {#rule-to-save-adaptive-form-as-draft}

To create a "Save Form" rule on a form component, for example, a button, follow the steps below:

1. In the author instance, open an Adaptive Form in edit mode.
1. From the left pane, select ![Components icon](assets/components_icon.png) and drag the [!UICONTROL Button] component to the form.
1. Select the [!UICONTROL Button] component and then select the ![Configure icon](assets/configure_icon.png). 
1. Select the [!UICONTROL Edit Rules] icon to open the Rule Editor. 
1. Select **[!UICONTROL Create]** to configure and create the rule.
1. In the [!UICONTROL When] section, select "is clicked" and in the [!UICONTROL Then] section, select the "Save Form" options.
1. Select **[!UICONTROL Done]** to save the rule.

### Enable Auto-save {#enable-auto-save}

You can configure the auto-save feature for an adaptive form as follows:

1. In the author instance, open an Adaptive Form in edit mode.
1. From the left pane, select the ![Properties icon](assets/configure_icon.png) and expand the [!UICONTROL AUTO-SAVE] option.
1. Select the **[!UICONTROL Enable]** check box to enable auto-save of the form. You can configure the following:
* By default, the [!UICONTROL Adaptive Form Event] is set to "true", which implies that the form is auto-saved after every event.
* In [!UICONTROL Trigger], configure to trigger auto-save based on the occurrence of an event or after a specific interval of time.
-->

## Consulte también {#see-also}

{{see-also}}



<!--

>[!MORELIKETHIS]
>
>* [Configure data sources for AEM Forms](/help/forms/configure-data-sources.md)
>* [Configure Azure storage for AEM Forms](/help/forms/configure-azure-storage.md)
>* [Integrate Microsoft Dynamics 365 and Salesforce with Adaptive Forms](/help/forms/configure-msdynamics-salesforce.md)

-->
