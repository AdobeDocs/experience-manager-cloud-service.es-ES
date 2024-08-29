---
title: ¿Cómo se enumeran los formularios en una página de Adobe Experience Manager Sites mediante el componente Portal de Forms?
description: Obtenga información sobre cómo enumerar formularios en una página de AEM Sites.
feature: Adaptive Forms, Core Components
role: User, Developer
source-git-commit: 58533d9a950fa4dc0e043ef8cb935d65fc68d233
workflow-type: tm+mt
source-wordcount: '673'
ht-degree: 14%

---


# Mostrar una lista de formularios en la página de Sites

Imagine que un usuario visita el sitio web del banco en busca de un formulario de apertura de cuenta. El banco utiliza el componente Portal de Forms para ayudar a los usuarios a encontrar rápidamente el formulario introduciendo palabras clave específicas o filtrando por categorías como &quot;Nuevas cuentas&quot; o &quot;Banca personal&quot; y permite a los usuarios localizar fácilmente el formulario deseado sin tener que desplazarse por listas largas.

El componente **Buscar y listar** del portal de Forms le permite mostrar y listar formularios en una página de Sites. Los usuarios pueden configurar y presentar una lista completa de formularios basados en criterios específicos para satisfacer los requisitos de la organización. Los usuarios anónimos pueden visitar la página de Sites para ver y examinar los formularios disponibles. Los formularios enumerados se pueden ordenar en orden ascendente o descendente mediante la opción desplegable **Ordenar por** ubicada en la esquina superior derecha de la pantalla.

![Icono Buscar y listar](assets/search-and-lister-component.png){width="250" align="center"}

## Requisito previo

Antes de explorar las distintas funcionalidades de un componente del portal de Forms, asegúrese de que los componentes principales estén habilitados para su entorno. Para obtener instrucciones detalladas sobre cómo habilitar los componentes principales para su entorno, [haga clic aquí](/help/forms/enable-adaptive-forms-core-components.md).

<!--
## Enable Forms Portal components for your existing environment

To enable out-of-the-box Forms Portal components on existing AEM Forms as a Cloud Service, perform the following steps:

1. **Clone Cloud Manager Git repository on your local development instance:**  Your Cloud Manager Git repository contains a default AEM project. It is based on [AEM Archetype](https://github.com/adobe/aem-project-archetype/). Clone your Cloud Manager Git Repository using Self-Service Git Account Management from Cloud Manager UI to bring the project on your local development environment. For details on accessing the repository, see [Accessing Repositories](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/managing-code/accessing-repos.html).  

1. **Create [!DNL Experience Manager Forms] as a [Cloud Service] project:** Create [!DNL Experience Manager Forms] as a [Cloud Service] project based on [AEM Archetype 50](https://github.com/adobe/aem-project-archetype/releases/tag/aem-project-archetype-50) or later. The archetype help developers easily start developing for [!DNL AEM Forms] as a Cloud Service. It also includes some sample themes and templates to help you started quickly.

    To create [!DNL Experience Manager Forms] as a Cloud Service project, open the command prompt and run the below command. To include [!DNL Forms] specific configurations, themes, and templates, set `includeForms=y`.  

    ```shell
    mvn -B archetype:generate -DarchetypeGroupId=com.adobe.aem -DarchetypeArtifactId=aem-project-archetype -DarchetypeVersion=30 -DaemVersion="cloud" -DappTitle="My Site" -DappId="mysite" -DgroupId="com.mysite" -DincludeForms="y"
    ```

    Also, change `appTitle`, `appId`, and `groupId`, in the above command to reflect your environment.

    After the project is ready, update the `<core.forms.components.version>x.y.z</core.forms.components.version>` property in the top-level `pom.xml` of the Archetype project to reflect the latest version of [core-forms-components](https://github.com/adobe/aem-core-forms-components) in your `AEM Archetype` project. 
 
1. **Deploy the project to your local development environment:** You can use the following command to deploy to your local development environment

    `mvn -PautoInstallPackage clean install`

    For the complete list of commands, see [Building and Installing](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/using.html?lang=en#building-and-installing)

1. [Deploy the archetype to your [!DNL AEM Forms] as a Cloud Service environment](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/aem-project-content-package-structure.html#embeddeds). -->

Después de implementar los componentes principales más recientes en su entorno, los componentes del portal de Forms pasan a ser accesibles en el entorno de creación.

## Mostrar una lista de formularios en la página de Sites

Para agregar el componente de portal **Buscar y listar** a su página de Sites, realice los siguientes pasos:

1. Abra la página de AEM Sites en modo **Editar**.
1. Vaya a la **[!UICONTROL Información de la página]** > **[!UICONTROL Editar plantilla]**
   ![Editar directiva de plantilla](/help/forms/assets/save-form-as-draft-edit-template.png){width="250" align="center"}

1. AEM Haga clic en la **[!UICONTROL directiva]** y seleccione la casilla de verificación **[!UICONTROL Buscar y listar]** bajo el **[Nombre de proyecto de tipo de archivo] - Forms y el portal de comunicaciones**.

   ![Selección de directiva](/help/forms/assets/search-lister-enable-policy.png){width="250" align="center"}

1. Haga clic en **[!UICONTROL Listo]**.
1. A continuación, vuelva a abrir la página de AEM Sites en el modo Autor.
1. Busque la sección en el editor de páginas que le permite agregar el componente Portal de Forms.

1. Haga clic en el icono **Agregar**. El icono es un signo más (+) que significa la opción de agregar nuevos componentes.

   Al hacer clic en el icono **Agregar**, se muestra un cuadro de diálogo **Insertar nuevo componente** que muestra varios componentes para su inserción.

   >[!NOTE]
   >
   > También puede arrastrar y soltar el componente.

1. Examine los componentes disponibles en el cuadro de diálogo y seleccione el componente que desee en la lista. Por ejemplo, seleccione el componente **Buscar y listar** de la lista para agregar el componente **Buscar y listar** del portal de Forms.

   ![Componente Buscar y listar](/help/forms/assets/add-search-lister.png){width="250" align="center"}

Ahora, configure las propiedades del componente **Buscar y listar**.

## Comprender las propiedades del componente Buscar y listar

Puede personalizar fácilmente las propiedades del componente **Buscar y listar** mediante el cuadro de diálogo Configurar para una experiencia de usuario perfecta. Para configurarlo, seleccione el componente y, a continuación, seleccione el icono ![Configurar](assets/configure_icon.png). El cuadro de diálogo **[!UICONTROL Buscar y listar]** se abre.

### Pestaña Mostrar

![Ficha de visualización](/help/forms/assets/search-and-lister-display-tab.png){width="250" align="center"}

1. En **[!UICONTROL Título]**, especifique el título del componente Buscar y listar. Un título indicativo permite a los usuarios realizar una búsqueda rápida en toda la lista de formularios.
1. En la lista **[!UICONTROL Diseño]**, seleccione el diseño para representar los formularios en formato de tarjeta o lista.
1. Seleccione **[!UICONTROL Ocultar búsqueda]** y **[!UICONTROL Ocultar orden]** para ocultar la búsqueda y ordenar por características.
1. En **[!UICONTROL Información de objeto]**, proporcione la información de objeto que aparece al pasar el ratón por encima del componente.

### Pestaña Recurso

![Pestaña de recursos](/help/forms/assets/search-and-lister-asset-tab.png){width="250" align="center"}

1. En la ficha **[!UICONTROL Carpeta de recursos]**, especifique la ubicación desde la que se extraen los formularios y se enumeran en la página.
1. Con **[!UICONTROL Agregar otra ubicación]**, puede configurar varias ubicaciones de carpetas.

### Pestaña Resultados

![Ficha de visualización](/help/forms/assets/search-and-lister-result-tab.png){width="250" align="center"}

En la pestaña **[!UICONTROL Resultados]** configure el número máximo de formularios que se mostrarán por página. El valor predeterminado es de ocho formularios por página.

## Ver formularios en la página de Sites mediante el componente Buscar y listar

Para ver la lista de formularios, use el componente **Buscar y listar** del portal de Forms. Previsualice la página de AEM Sites para ver la lista de formularios de la carpeta **Assets** en la pantalla. También puede buscar un formulario específico mediante la barra de búsqueda.

![Icono Buscar y listar](assets/search-and-lister-component.png){width="250" align="center"}

<!--
## Configure Azure Storage for Adaptive Forms {#configure-azure-storage-adaptive-forms}

[[!DNL Experience Manager Forms] Data Integration](data-integration.md) provides [!DNL Azure] storage configuration to integrate forms with [!DNL Azure] storage services. The Form Data Model (FDM) can be used to create Adaptive Forms that interact with [!DNL Azure] server to enable business workflows.

### Create Azure Storage Configuration {#create-azure-storage-configuration}

Before executing these steps, ensure that you have an Azure storage account and an access key to authorize access to the [!DNL Azure] storage account.

1. Navigate to **[!UICONTROL Tools]** &gt; **[!UICONTROL Cloud Services]** &gt; **[!UICONTROL Azure Storage]**.
1. Select a folder to create the configuration and select **[!UICONTROL Create]**.
1. Specify a title for the configuration in the **[!UICONTROL Title]** field.
1. Specify the name of the [!DNL Azure] storage account in the **[!UICONTROL Azure Storage Account]** field.

### Configure Unified Storage Connector for Forms Portal {#configure-usc-forms-portal}

Perform the following steps to configure Unified Storage Connector for AEM Workflows:

1. Navigate to **[!UICONTROL Tools]** &gt; **[!UICONTROL Forms]** &gt; **[!UICONTROL Unified Storage Connector]**.
1. In the **[!UICONTROL Forms Portal]** section, select **[!UICONTROL Azure]** from the **[!UICONTROL Storage]** drop-down list.
1. Specify the [configuration path for the Azure storage configuration](#create-azure-storage-configuration) in the **[!UICONTROL Storage Configuration Path]** field.
1. Select **[!UICONTROL Publish]** and then select **[!UICONTROL Save]** to save the configuration.

## Enable Forms Portal Components {#enable-forms-portal-components}

To use any core component (including the out-of-the-box portal components) in an Adobe Experience Manager (AEM) site, you must create a proxy component and enable it for your site. For creating a proxy component and enabling portal components, see [Using Core Components](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/get-started/using.html?lang=en#create-proxy-components). 

Once a portal component is enabled, you can use it in the author instance of your sites page.

## Add and Configure Forms Portal Components {#configure-forms-portal-components}

You can create and customize Forms Portal on websites authored using AEM by adding and configuring the portal components. Ensure that the [components are enabled](#enable-forms-portal-components) before using them in the Forms Portal.

To add a component, either drag and drop the component from the Components pane to the layout container on the page, or select the add icon on the layout container and add the component from the [!UICONTROL Insert New Component] dialog.

### Configure Drafts & Submissions Component {#configure-drafts-submissions-component}

The Drafts & Submissions component displays forms that are saved as draft for completing later and submitted forms. To configure, select the component and then select the ![Configure icon](assets/configure_icon.png). In the [!UICONTROL Drafts and Submissions] dialog, specify the title to indicate the form listing as draft or submitted forms. Also select whether the component should list draft forms or submitted forms in card or list format.

![Drafts icon](assets/drafts-component.png)

![Submissions icon](assets/submission-listing.png)

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


## Siguientes pasos

En el artículo siguiente, aprenderemos [cómo guardar formularios como borradores y enumerarlos en una página de Sites mediante el componente Borradores y envíos del portal de Forms](/help/forms/save-core-component-based-form-as-draft.md).

## Artículos relacionados

{{forms-portal-see-also}}

## Consulte también {#see-also}

{{see-also}}