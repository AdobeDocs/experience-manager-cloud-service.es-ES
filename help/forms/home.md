---
title: Introducción a  [!DNL AEM Forms]  as a Cloud Service
description: Descubra AEM Forms y cómo le ayuda a producir documentos y contenido de formularios preparados para la empresa. Obtenga información sobre Plataforma como servicio (PaaS) y cómo administrar formularios digitales de clase empresarial y procesos empresariales, así como conectar Forms a fuentes de datos actuales.
landing-page-description: Obtenga información sobre cómo utilizar formularios en AEM as a Cloud Service.
exl-id: aa5ef10c-ba78-4a9d-8b2b-a72a7a306888
source-git-commit: 37274b28ab2343fd3cdfb4747c9dee701c699b46
workflow-type: tm+mt
source-wordcount: '1312'
ht-degree: 23%

---

# Introducción {#introduction}

Adobe [!DNL Experience Manager Forms as a Cloud Service] ofrece una solución nativa en la nube de plataforma como servicio (PaaS) para que las empresas creen, administren, publiquen y actualicen formularios digitales complejos a la vez que integran los datos enviados con procesos back-end y reglas comerciales y guardan datos en un almacén de datos externo. El servicio siempre está actualizado, siempre está disponible, y aprende constantemente.

Puede utilizar el servicio para crear y desplegar formularios digitales interactivos y atractivos. Por ejemplo, imagine una organización que desea digitalizar su recorrido de inscripción de clientes. Tienen varias fuentes de datos con los datos de clientes existentes. Buscan una forma de rellenar previamente los formularios, agregarles firmas electrónicas y archivar los formularios rellenados como archivos PDF. Además, tienen varios formularios impresos (PDF forms), y también quieren convertir todos sus formularios impresos en formularios digitales.



La organización puede utilizar [!DNL AEM Forms] as a Cloud Service para crear formularios digitales, conectar formularios a fuentes de datos existentes, integrar formularios con [!DNL Adobe Sign] para agregarles firmas electrónicas y generar el documento de registro (DoR) para archivar los formularios enviados como archivos PDF. Asimismo, pueden usar el servicio para convertir los PDF forms existentes en formularios digitales.

La organización puede utilizar [!DNL AEM Forms] as a Cloud Service y disfrutar de todas estas funciones en la nube sin requerir ningún tipo de infraestructura local. El servicio también permite prescindir de los ciclos de actualización complejos, ya que siempre está actualizado con las últimas funciones.

## Funciones principales {#key-features}

|  |  |
|---|---|
| Formularios adaptables | Cree y administre formularios interactivos, dinámicos, interactivos, fáciles de usar y basados en datos para móviles para sus sitios web, aplicaciones y otros canales digitales y de impresión. Revise lo siguiente para empezar, comprender e implementar experiencias de inscripción: <ul><li><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/create-an-adaptive-form-on-forms-cs/creating-adaptive-form.html"> Crear un formulario adaptable </a></li><li><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/create-an-adaptive-form-on-forms-cs/themes.html">Estilo de formulario adaptable</a></li><li><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/configure-submit-actions-and-metadata-submission/configuring-submit-actions.html#enabling-server-side-validation-br"> Envío de datos a un almacén de datos o a un flujo de trabajo</a></li><li><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/generate-document-of-record-for-non-xfa-based-adaptive-forms.html"> Crear un registro del formulario para archivo a largo plazo</a></li></ul> |
| API de comunicaciones | Automatice la creación, administración y entrega de comunicaciones personalizadas basadas en datos con API RESTful bajo demanda o a intervalos programados como extractos mensuales y avisos de cuenta. Revise lo siguiente para empezar, comprender y crear: <ul><li><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/using-communications/aem-forms-cloud-service-communications-introduction.html?#document-generation"> Generación de comunicaciones personalizadas </a> </li><li><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/using-communications/aem-forms-cloud-service-communications-introduction.html?#document-manipulation"> Montaje o desmontaje de documentos de PDF </a> </li><li><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/using-communications/aem-forms-cloud-service-communications-introduction.html?#convert-to-and-validate-pdf%2Fa-compliant-documents">Creación de documentos compatibles con el PDF/A </a></li></ul> |
| Servicio de conversión automatizada de formularios  | Convierta formularios heredados basados en PDF en Adaptive Forms que se puedan administrar y distribuir fácilmente en línea. Consulte lo siguiente para empezar: <ul><li><a href="https://experienceleague.adobe.com/docs/aem-forms-automated-conversion-service/using/configure-service.html">Configuración del servicio de Automated forms conversion</a></li><li><a href="https://experienceleague.adobe.com/docs/aem-forms-automated-conversion-service/using/convert-existing-forms-to-adaptive-forms.html?lang=es">Conversión de formularios PDF en formularios adaptables</a></li></ul> |
| Forms Workflow | Automatice los procesos empresariales que implican formularios y servicios de documentos. Asigne, enrute, revise y apruebe formularios y documentos a medida que estos se desplazan por diferentes etapas de un proceso empresarial. Consulte lo siguiente para empezar:  <ul><li><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/create-reviews-forms.html">Enviar un formulario o documento para su revisión</a></li><li><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/create-form-centric-workflows/aem-forms-workflow-step-reference.html?#assign-task-step">Crear un flujo de trabajo de rechazo de aprobación</a></li><li><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/create-form-centric-workflows/aem-forms-workflow-step-reference.html?#generate-document-of-record-step">Agregar documento de registro </a> o <a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/create-form-centric-workflows/aem-forms-workflow-step-reference.html?#sign-document-step"> firma electrónica </a> pasos hacia un flujo de trabajo empresarial</a></li></ul> |
| Firmas electrónicas | Integre con Adobe Sign y ArchiveSign para enviar fácilmente Forms y documentos a los usuarios para que los firmen por correo electrónico. <ul><li><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/use-adobe-sign/working-with-adobe-sign.html">Firma electrónica de un formulario adaptable con Adobe Sign </a></li><li></a> <a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/integrate/services/integrate-docusign-adaptive-forms.html">Firma electrónica de un formulario adaptable con Sign </a></li></ul> |
| Forms Analytics | Utilice Adobe Analytics para obtener información valiosa sobre el comportamiento y las preferencias del usuario. <ul><li><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/integrate/services/integrate-aem-forms-with-adobe-analytics.html?lang=en">Conectar un formulario adaptable con Adobe Analytics</a></li></ul> |
| Orígenes de datos | Conecte fácilmente los formularios y documentos con orígenes de datos externos para recuperar y enviar datos. <ul><li><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/integrate/use-form-data-model/configure-data-sources.html?lang=en">Conexión a un extremo RDBMS o Rest</a></li><li><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/integrate/use-form-data-model/configure-msdynamics-salesforce.html?lang=en">Conectarse al servicio en la nube de Microsoft Dynamics 365 o Salesforce</a></li><li><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/integrate/use-form-data-model/configure-azure-storage.html?lang=en">Conectarse al almacenamiento del blob de Microsoft Azure</a></li></ul> |


<!-- 
>[!BEGINTABS]

>[!TAB Adaptive Forms]

Adaptive Forms allows businesses to create and manage interactive, data-driven forms for their websites and other digital channels responsive, mobile-friendly forms without. </br> </br> Adaptive Forms in AEM also include a drag-and-drop form builder, which enables non-technical users to easily create and customize forms using pre-built form components such as text boxes, dropdown menus, and date pickers. This enables faster form creation and eliminates the need for extensive coding and development. </br> </br> In addition, AEM Adaptive Forms offer several other features, including: <ul><li>Advanced workflows for routing, approval, and submission of form data Real-time validation and error checking to ensure data accuracy </li><li>Integration with third-party data sources and APIs for pre-filling form fields or validating data </li><li>Advanced analytics and reporting capabilities to track form usage, conversion rates, and other key metrics </li><li>Integration with Adobe Sign and DocuSign for e-signatures </li>

>[!TAB Automated Forms Conversion Service]

Automated Forms Conversion Service allows businesses to convert legacy PDF-based forms into interactive, digital forms that can be easily managed and distributed online. The service helps: <ul><li>Save manual effort required to convert print forms to adaptive forms.</li><li>Applies patterns and appropriate validations during conversion</li><li>Generate Document of Record during conversion </li><li>Group commonly occurring fields into reusable form fragments </li> <li>Enables Adobe Analytics during conversion</li>

>[!TAB Communications API (Document Services)]

Communications APIs are a set of RESTful APIs (Application Programming Interfaces) that enable businesses to automate the creation, management, and delivery of personalized, data-driven communications. </br> </br> These APIs also enable businesses to integrate their communications workflows with third-party systems and data sources, allowing them to create highly targeted and personalized messages that are triggered by specific events or user behaviors. Some key features of AEM Forms Communications APIs include:<ul><li> Dynamic content delivery: The APIs allow businesses to create and deliver dynamic content that is tailored to individual users based on their preferences, behaviors, and past interactions with the business.</li> <li>Personalized messaging: The APIs enable businesses to personalize their communications by including user-specific data such as names, addresses, and purchase history.</li><li>Integration with back-end systems: The APIs can be integrated with a wide range of back-end systems, including CRMs, databases, and marketing automation platforms.</li><li> Generate Pixel Perfect PDF documents: The APIs generate pixel-perfect PDF documents that are customized with user-specific data and content. This feature enables businesses to create highly professional and polished documents, such as invoices, contracts, and statements, that are delivered to users in PDF format.

>[!TAB Advanced Analytics]

The service provides OOTB support to connect with Adobe Analytics. Connecting forms with Adobe Analytics provides several benefits for businesses, including: <ul><li> Improved understanding of user behavior: By connecting forms with Adobe Analytics, businesses can gain a deeper understanding of how users are interacting with their forms. This includes insights into user engagement, conversion rates, drop-off points, and other key metrics that can help businesses identify areas for improvement and optimize their forms for better user experiences. </li><li>Better targeting of marketing efforts: By analyzing user behavior on forms, businesses can gain valuable insights into user preferences and interests. This information can be used to better target marketing efforts and create more effective campaigns that drive engagement and conversions. </li><li> Reduced error rate: By integrating forms with Adobe Analytics, you can find insights about field with most errors and improve data quality, leading to better decision-making and more accurate insights. </li><li> Improved ROI: By optimizing forms based on insights gained from Adobe Analytics, businesses can improve conversion rates and drive more revenue from their digital channels. This can lead to a higher return on investment (ROI) for marketing and digital initiatives, helping businesses to achieve their goals and drive growth.</li>


>[!ENDTABS] 

| Adaptive Forms | Communications APIs  | Automated Forms Conversion Service | Forms Workflows | E-Sign | Forms Analytics | Data Model | 
|---|---|---|---|---|---| ---|
|Create and manage interactive, dynamic, responsive, mobile-friendly, and data-driven forms for your websites, apps, and other digital and Print channels. | Automate creation, management, and delivery of personalized, data-driven communications with RESTful APIs (Application Programming Interfaces) on-demand or at scheduled intervals. | Convert legacy PDF-based forms into Adaptive Forms that can be easily managed and distributed online. | Automate business processes involving forms and document services. Assign, route, review, and approve forms and document as these move through different stages of a business process.| Integrate with Adobe Sign and DocuSign to easliy send send Forms and documents to users for e-signatures. | Use Adobe Analytics to gain valuable insights into user behavior and preferences. | Easily connect your forms and documents with external data sources to retieve and send data. |
|<ul><li>Create an Adaptive Form</li><li>Style an Adaptive Form</li><li>Submit data to a data store or a workflow</li></ul>|<ul><li>Generate personalized communciations</li><li>Assemble or disassemble PDF documents</li><li>Create PDF/A-compliant documents</li></ul>|<ul><li>Configure Automated Forms Conversion Service</li><li>Convert PDF forms to adaptive forms</li></ul>|<ul><li>Send a form or document for review</li><li>Create an approval rejection Workflow</li><li>Add Document of Record or e-signatures to a business workflow</li></ul>|<ul><li>E-sign an Adaptive Form with Adobe Sign</li><li>E-sign an Adaptive Form with DocuSign</li></ul>|<ul><li>Connect an Adaptive Form with Adobe Analytics</li></ul>|<ul><li>Connect to a RDBMS or Rest endpoint</li><li>Connect to Microsoft Dynamics 365 or Salesforce cloud service</li><li>Connect to Microsoft&reg; Azure Blob Storage</li></ul>|

<!--
| | |
|---|---|
| Adaptive Forms | Adaptive Forms allows businesses to create and manage interactive, data-driven forms for their websites and other digital channels responsive, mobile-friendly forms without. </br> </br> Adaptive Forms in AEM also include a drag-and-drop form builder, which enables non-technical users to easily create and customize forms using pre-built form components such as text boxes, dropdown menus, and date pickers. This enables faster form creation and eliminates the need for extensive coding and development. </br> </br> In addition, AEM Adaptive Forms offer several other features, including: <ul><li>Advanced workflows for routing, approval, and submission of form data Real-time validation and error checking to ensure data accuracy </li><li>Integration with third-party data sources and APIs for pre-filling form fields or validating data </li><li>Advanced analytics and reporting capabilities to track form usage, conversion rates, and other key metrics </li><li>Integration with Adobe Sign and DocuSign for e-signatures </li>|
| Automated Forms Conversion Service | Automated Forms Conversion Service allows businesses to convert legacy PDF-based forms into interactive, digital forms that can be easily managed and distributed online. The service helps: <ul><li>Save manual effort required to convert print forms to adaptive forms.</li><li>Applies patterns and appropriate validations during conversion</li><li>Generate Document of Record during conversion </li><li>Group commonly occurring fields into reusable form fragments </li> <li>Enables Adobe Analytics during conversion</li>|
| Communications API (Document Services) | Communications APIs are a set of RESTful APIs (Application Programming Interfaces) that enable businesses to automate the creation, management, and delivery of personalized, data-driven communications. </br> </br> These APIs also enable businesses to integrate their communications workflows with third-party systems and data sources, allowing them to create highly targeted and personalized messages that are triggered by specific events or user behaviors. Some key features of AEM Forms Communications APIs include:<ul><li> Dynamic content delivery: The APIs allow businesses to create and deliver dynamic content that is tailored to individual users based on their preferences, behaviors, and past interactions with the business.</li> <li>Personalized messaging: The APIs enable businesses to personalize their communications by including user-specific data such as names, addresses, and purchase history.</li><li>Integration with back-end systems: The APIs can be integrated with a wide range of back-end systems, including CRMs, databases, and marketing automation platforms.</li><li> Generate Pixel Perfect PDF documents: The APIs generate pixel-perfect PDF documents that are customized with user-specific data and content. This feature enables businesses to create highly professional and polished documents, such as invoices, contracts, and statements, that are delivered to users in PDF format.|
|Advanced Analytics| The service provides OOTB support to connect with Adobe Analytics. Connecting forms with Adobe Analytics provides several benefits for businesses, including: <ul><li> Improved understanding of user behavior: By connecting forms with Adobe Analytics, businesses can gain a deeper understanding of how users are interacting with their forms. This includes insights into user engagement, conversion rates, drop-off points, and other key metrics that can help businesses identify areas for improvement and optimize their forms for better user experiences. </li><li>Better targeting of marketing efforts: By analyzing user behavior on forms, businesses can gain valuable insights into user preferences and interests. This information can be used to better target marketing efforts and create more effective campaigns that drive engagement and conversions. </li><li> Reduced error rate: By integrating forms with Adobe Analytics, you can find insights about field with most errors and improve data quality, leading to better decision-making and more accurate insights. </li><li> Improved ROI: By optimizing forms based on insights gained from Adobe Analytics, businesses can improve conversion rates and drive more revenue from their digital channels. This can lead to a higher return on investment (ROI) for marketing and digital initiatives, helping businesses to achieve their goals and drive growth.</li>|

-->

## Últimas innovaciones {#latest-innovations}

>[!BEGINTABS]

>[!TAB &#x200B; Forms adaptable sin objetivos]

||| |—|—| |![](https://experienceleague.corp.adobe.com/docs/experience-manager-headless-adaptive-forms/assets/how-headless-adaprive-forms-work.png?)| Crear y administrar [Forms adaptable sin objetivos](https://experienceleague.corp.adobe.com/docs/experience-manager-headless-adaptive-forms/using/overview.html) en la plataforma de Adobe Experience Manager. Permita que los desarrolladores creen, publiquen y gestionen formularios interactivos a los que se puede acceder e interactuar mediante API, en lugar de a través de una interfaz gráfica de usuario tradicional. <br/> <br/> Estos formularios están diseñados para enviarse sin necesidad de una interfaz de formulario HTML tradicional. En otras palabras, le permiten enviar datos de formulario mediante programación a través de una API o código back-end sin requerir ningún elemento de formulario visible en el front-end. <br/> <br/> Los formularios sin encabezado son útiles en varios casos, como cuando se crean aplicaciones de una sola página, aplicaciones web progresivas o aplicaciones móviles, en los que una interfaz de formulario de HTML tradicional puede no ser necesaria o práctica. Al permitir a los desarrolladores enviar datos de formulario directamente a través de API o código back-end, los formularios sin encabezado ayudan a optimizar los flujos de trabajo y a mejorar el rendimiento general de las aplicaciones web.|




>[!TAB Componentes principales]

||| |—|—| |![](https://experienceleague.corp.adobe.com/docs/experience-manager-cloud-service/assets/sample-core-components-based-adaptive-form.png?) | El [Componentes principales adaptables de Forms](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html#features) son un conjunto de 24 componentes de código abierto compatibles con BEM que se basan en los componentes principales de WCM de Adobe Experience Manager. Están diseñadas específicamente para utilizarse en la creación de Forms adaptable, que son formularios que se adaptan al dispositivo, navegador y tamaño de pantalla del usuario. <br/> <br/> Estos componentes se pueden utilizar para crear experiencias de inscripción y captura de datos excepcionales proporcionando una amplia gama de opciones de campo de formulario, incluidos campos de texto, casillas de verificación, menús desplegables y mucho más. También incluyen funciones como validación, lógica condicional y diseño interactivo, que pueden utilizarse para crear formularios fáciles de usar y fáciles de usar. <br/> <br/>  Además, como estos componentes son de código abierto, los desarrolladores pueden personalizar y ampliar fácilmente los componentes para adaptarlos a las necesidades específicas de su organización. Además, estos componentes se basan en la metodología de BEM, que garantiza que sean escalables y mantenibles.|



>[!TAB &#x200B; del conector Microsoft PowerAutomate]

||| |—|—| |![](https://powerusers.microsoft.com/t5/image/serverpage/image-id/182924i17C4BEA1C045D731/image-size/large/is-moderation-mode/true?v=1.0&amp;px=999)| AEM Forms Power Automate Connector permite integrar Adobe Experience Manager (AEM) Forms con Microsoft Power Automate (anteriormente conocido como Microsoft Flow). Power Automate es un servicio basado en la nube que le permite crear flujos de trabajo automatizados entre diferentes aplicaciones y servicios.  <br/> <br/> Con AEM conector de automatización de Form Power, puede crear flujos de trabajo que se déclencheur automáticamente en función del envío de un formulario adaptable. Por ejemplo, puede crear un flujo de trabajo que envíe automáticamente una notificación por correo electrónico a una persona específica cuando un usuario envíe un formulario o cree una tarea en Microsoft Planner cuando un usuario complete un formulario.  <br/> <br/> AEM Forms Power Automate Connector es una potente herramienta que le permite automatizar e integrar su Forms adaptable con otras aplicaciones y servicios que se conectan con Microsoft Power Automate, lo que le permite trabajar con una gama más amplia de herramientas. Puede crear flujos de trabajo adaptados a sus necesidades específicas, con la capacidad de agregar acciones, condiciones y déclencheur personalizados. Además, Power Automate proporciona análisis e informes detallados que le permiten supervisar y optimizar los flujos de trabajo a lo largo del tiempo.|


>[!TAB Conectores de almacenamiento de Microsoft: OneDrive y Sharepoint]

||| |—|—| |![](/help/forms/assets/onedrive-and-sharepoint.jpg)|Los conectores de almacenamiento de AEM Forms Microsoft para OneDrive y SharePoint son conectores que le permiten integrar Adobe Experience Manager (AEM) Forms con Microsoft OneDrive y SharePoint. Con este conector, puede cargar archivos de datos y archivos adjuntos en OneDrive y SharePoint directamente desde Adaptive Forms. |


>[!ENDTABS]

<!--

| | |
|---|---|
| Adaptive Forms | Adaptive Forms allows businesses to create and manage interactive, data-driven forms for their websites and other digital channels responsive, mobile-friendly forms without. </br> </br> Adaptive Forms in AEM also include a drag-and-drop form builder, which enables non-technical users to easily create and customize forms using pre-built form components such as text boxes, dropdown menus, and date pickers. This enables faster form creation and eliminates the need for extensive coding and development. </br> </br> In addition, AEM Adaptive Forms offer several other features, including: <ul><li>Advanced workflows for routing, approval, and submission of form data Real-time validation and error checking to ensure data accuracy </li><li>Integration with third-party data sources and APIs for pre-filling form fields or validating data </li><li>Advanced analytics and reporting capabilities to track form usage, conversion rates, and other key metrics </li><li>Integration with Adobe Sign and DocuSign for e-signatures </li>|
| Automated Forms Conversion Service | Automated Forms Conversion Service allows businesses to convert legacy PDF-based forms into interactive, digital forms that can be easily managed and distributed online. The service helps: <ul><li>Save manual effort required to convert print forms to adaptive forms.</li><li>Applies patterns and appropriate validations during conversion</li><li>Generate Document of Record during conversion </li><li>Group commonly occurring fields into reusable form fragments </li> <li>Enables Adobe Analytics during conversion</li>|
| Communications API (Document Services) | Communications APIs are a set of RESTful APIs (Application Programming Interfaces) that enable businesses to automate the creation, management, and delivery of personalized, data-driven communications. </br> </br> These APIs also enable businesses to integrate their communications workflows with third-party systems and data sources, allowing them to create highly targeted and personalized messages that are triggered by specific events or user behaviors. Some key features of AEM Forms Communications APIs include:<ul><li> Dynamic content delivery: The APIs allow businesses to create and deliver dynamic content that is tailored to individual users based on their preferences, behaviors, and past interactions with the business.</li> <li>Personalized messaging: The APIs enable businesses to personalize their communications by including user-specific data such as names, addresses, and purchase history.</li><li>Integration with back-end systems: The APIs can be integrated with a wide range of back-end systems, including CRMs, databases, and marketing automation platforms.</li><li> Generate Pixel Perfect PDF documents: The APIs generate pixel-perfect PDF documents that are customized with user-specific data and content. This feature enables businesses to create highly professional and polished documents, such as invoices, contracts, and statements, that are delivered to users in PDF format.|
|Advanced Analytics| The service provides OOTB support to connect with Adobe Analytics. Connecting forms with Adobe Analytics provides several benefits for businesses, including: <ul><li> Improved understanding of user behavior: By connecting forms with Adobe Analytics, businesses can gain a deeper understanding of how users are interacting with their forms. This includes insights into user engagement, conversion rates, drop-off points, and other key metrics that can help businesses identify areas for improvement and optimize their forms for better user experiences. </li><li>Better targeting of marketing efforts: By analyzing user behavior on forms, businesses can gain valuable insights into user preferences and interests. This information can be used to better target marketing efforts and create more effective campaigns that drive engagement and conversions. </li><li> Reduced error rate: By integrating forms with Adobe Analytics, you can find insights about field with most errors and improve data quality, leading to better decision-making and more accurate insights. </li><li> Improved ROI: By optimizing forms based on insights gained from Adobe Analytics, businesses can improve conversion rates and drive more revenue from their digital channels. This can lead to a higher return on investment (ROI) for marketing and digital initiatives, helping businesses to achieve their goals and drive growth.</li>|

Adaptive Forms enable organizations to quickly design and deploy responsive, mobile-friendly forms without the need for extensive coding or development. With Adaptive Forms, businesses can create complex, multi-step forms with conditional logic, validations, and integrations with back-end systems such as CRMs and databases.

Adaptive Forms in AEM also include a drag-and-drop form builder, which enables non-technical users to easily create and customize forms using pre-built form components such as text boxes, dropdown menus, and date pickers. This enables faster form creation and eliminates the need for extensive coding and development.

In addition, AEM Adaptive Forms offer several other features, including:

Advanced workflows for routing, approval, and submission of form data
Real-time validation and error checking to ensure data accuracy
Integration with third-party data sources and APIs for pre-filling form fields or validating data
Advanced analytics and reporting capabilities to track form usage, conversion rates, and other key metrics
Overall, AEM Adaptive Forms provide businesses with a powerful tool for creating and managing complex, interactive forms that can be easily integrated into their digital experiences. |




| Feature/Capability | [!DNL AEM Forms] as a Cloud Service | AEM 6.5 Forms  | 
|---|---|---|
| Cloud-native architecture | &#x2611;  | &#x2612; |
| Auto-scaling based on load | &#x2611;  | &#x2612; |
| Zero downtime for upgrades | &#x2611;  | &#x2612; |
| Feature roll-out frequency | Agile*  | Quarterly |
| CDN (content delivery network) included | &#x2611;  | &#x2612; | 
| Topologies optimized for maximum resilience and efficiency| &#x2611;  | &#x2612; | 
| Cloud-native development environment | &#x2611;  | &#x2612; | 
| Self-Service via Cloud Manager | &#x2611;  | &#x2612; | 
| Automated upgrades with Continuous Integration and Continuous Delivery (CI/CD) | &#x2611;  | &#x2612; | 
| Adaptive Forms | &#x2611; | &#x2611; | 
| Data Integration with multiple data sources| &#x2611; | &#x2611; | 
| Communications APIs (Document Services) | &#x2611;* | &#x2611; | 
| Automated Forms Conversion Service | &#x2611; | &#x2611; | 
| Integration with [!DNL Micosoft Power Automate] | &#x2611; | &#x2612; | 
| Integration with [!DNL Adobe Sign] | &#x2611; | &#x2611; | 
| Integration with [!DNL AEM Sites] | &#x2611; | &#x2611; | 
| Integration with [!DNL Adobe Launch] | &#x2611; | &#x2611; | 
| Integration with [!DNL Adobe Analytics] | &#x2611; | &#x2611; | 
| Easy connectivity with Microsoft Dynamics and Salesforce | &#x2611; | &#x2612; |
| Custom submit action for with [!DNL DocuSign] | &#x2611; | &#x2612; | 
| Microsoft Azure data store connector | &#x2611; | &#x2612; |
| Hardened Rule editor | &#x2611; | &#x2612; | 
| Forms Portal | &#x2611; | &#x2611; | 
| AEM Workflows | &#x2611; | &#x2611; | 
| Document of Record | &#x2611; | &#x2611; | 
| Adaptive Forms Wizard | &#x2611; | &#x2612; | 
| Custom XCI for Document of Record| &#x2611; | &#x2612; |
| Invisible Captcha | &#x2611; | &#x2611; |
| Reusable Form Data Model configurations | &#x2611; | &#x2611; |
| Acroform-based Document of Record | &#x2611; | &#x2611; | 
| Government ID based identity authentication for Adobe Sign enabled Adaptive Forms | &#x2611; | &#x2611; | 
| Document Security | &#x2612; | &#x2611; |


* [Notable changes in comparison to AEM 6.5 Forms](notable-changes.md)
* [Frequently asked questions](faq.md)

-->