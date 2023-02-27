---
title: Introducción a  [!DNL AEM Forms]  as a Cloud Service
description: Descubra AEM Forms y cómo le ayuda a producir documentos y contenido de formularios preparados para la empresa. Obtenga información sobre Plataforma como servicio (PaaS) y cómo administrar formularios digitales de clase empresarial y procesos empresariales, así como conectar Forms a fuentes de datos actuales.
landing-page-description: Obtenga información sobre cómo utilizar formularios en AEM as a Cloud Service.
exl-id: aa5ef10c-ba78-4a9d-8b2b-a72a7a306888
source-git-commit: 2f9c4d85c55ee63a769c0137d4a70b2126228d5b
workflow-type: tm+mt
source-wordcount: '1144'
ht-degree: 25%

---

# Introducción {#introduction}

Adobe [!DNL Experience Manager Forms as a Cloud Service] ofrece una solución nativa en la nube de plataforma como servicio (PaaS) para que las empresas creen, administren, publiquen y actualicen formularios digitales complejos a la vez que integran los datos enviados con procesos back-end y reglas comerciales y guardan datos en un almacén de datos externo. El servicio siempre está actualizado, siempre está disponible, y aprende constantemente.

Puede utilizar el servicio para crear y desplegar formularios digitales interactivos y atractivos. Por ejemplo, imagine una organización que desea digitalizar su recorrido de inscripción de clientes. Tienen varias fuentes de datos con los datos de clientes existentes. Buscan una forma de rellenar previamente los formularios, agregarles firmas electrónicas y archivar los formularios rellenados como archivos PDF. Además, tienen varios formularios impresos (PDF forms), y también quieren convertir todos sus formularios impresos en formularios digitales.



La organización puede utilizar [!DNL AEM Forms] as a Cloud Service para crear formularios digitales, conectar formularios a fuentes de datos existentes, integrar formularios con [!DNL Adobe Sign] para agregarles firmas electrónicas y generar el documento de registro (DoR) para archivar los formularios enviados como archivos PDF. Asimismo, pueden usar el servicio para convertir los PDF forms existentes en formularios digitales.

La organización puede utilizar [!DNL AEM Forms] as a Cloud Service y disfrutar de todas estas funciones en la nube sin requerir ningún tipo de infraestructura local. El servicio también permite prescindir de los ciclos de actualización complejos, ya que siempre está actualizado con las últimas funciones.

## Funciones principales {#key-features}

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


>[!ENDTABS] -->

| Formularios adaptables | API de comunicaciones | Servicio de conversión automatizada de formularios  | Forms Workflow | Firma electrónica | Forms Analytics | Modelo de datos |
|---|---|---|---|---|---| ---|
| Cree y administre formularios interactivos, dinámicos, interactivos, fáciles de usar y basados en datos para móviles para sus sitios web, aplicaciones y otros canales digitales e impresos. | Automatice la creación, administración y entrega de comunicaciones personalizadas basadas en datos con API de RESTful (Interfaces de programación de aplicaciones) a petición o a intervalos programados. | Convierta formularios heredados basados en PDF en Adaptive Forms que se puedan administrar y distribuir fácilmente en línea. | Automatice los procesos empresariales que implican formularios y servicios de documentos. Asigne, enrute, revise y apruebe formularios y documentos a medida que estos se desplazan por diferentes etapas de un proceso empresarial. | Integre con Adobe Sign y ArchiveSign para enviar fácilmente Forms y documentos a los usuarios para que los firmen por correo electrónico. | Utilice Adobe Analytics para obtener información valiosa sobre el comportamiento y las preferencias del usuario. | Conecte fácilmente los formularios y documentos con orígenes de datos externos para recuperar y enviar datos. |

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

||| |—|—| |![](https://experienceleague.corp.adobe.com/docs/experience-manager-headless-adaptive-forms/assets/how-headless-adaprive-forms-work.png?lang=en)| Crear y administrar [formularios web sin encabezado](https://experienceleague.corp.adobe.com/docs/experience-manager-headless-adaptive-forms/using/overview.html) en la plataforma de Adobe Experience Manager. Permita que los desarrolladores creen, publiquen y gestionen formularios interactivos a los que se puede acceder e interactuar mediante API, en lugar de a través de una interfaz gráfica de usuario tradicional. <br/> <br/> Estos formularios están diseñados para enviarse sin necesidad de una interfaz de formulario HTML tradicional. En otras palabras, le permiten enviar datos de formulario mediante programación a través de una API o código back-end sin requerir ningún elemento de formulario visible en el front-end. <br/> <br/> Los formularios sin encabezado son útiles en varios casos, como cuando se crean aplicaciones de una sola página, aplicaciones web progresivas o aplicaciones móviles, en los que una interfaz de formulario de HTML tradicional puede no ser necesaria o práctica. Al permitir a los desarrolladores enviar datos de formulario directamente a través de API o código back-end, los formularios sin encabezado ayudan a optimizar los flujos de trabajo y a mejorar el rendimiento general de las aplicaciones web.|




>[!TAB Componentes principales]

||| |—|—| |![](https://experienceleague.corp.adobe.com/docs/experience-manager-cloud-service/assets/sample-core-components-based-adaptive-form.png?lang=en) | El [Componentes principales adaptables de Forms](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html#features) son un conjunto de 24 componentes de código abierto compatibles con BEM que se basan en los componentes principales de WCM de Adobe Experience Manager. Están diseñadas específicamente para utilizarse en la creación de Forms adaptable, que son formularios que se adaptan al dispositivo, navegador y tamaño de pantalla del usuario. <br/> <br/> Estos componentes se pueden utilizar para crear experiencias de inscripción y captura de datos excepcionales proporcionando una amplia gama de opciones de campo de formulario, incluidos campos de texto, casillas de verificación, menús desplegables y mucho más. También incluyen funciones como validación, lógica condicional y diseño interactivo, que pueden utilizarse para crear formularios fáciles de usar y fáciles de usar. <br/> <br/>  Además, como estos componentes son de código abierto, los desarrolladores pueden personalizar y ampliar fácilmente los componentes para adaptarlos a las necesidades específicas de su organización. Además, estos componentes se basan en la metodología de BEM, que garantiza que sean escalables y mantenibles.|



>[!TAB &#x200B; del conector Microsoft PowerAutomate]

||| |—|—| |![](https://powerusers.microsoft.com/t5/image/serverpage/image-id/182924i17C4BEA1C045D731/image-size/large/is-moderation-mode/true?v=1.0&amp;px=999)| AEM Forms Power Automate Connector permite integrar Adobe Experience Manager (AEM) Forms con Microsoft Power Automate (anteriormente conocido como Microsoft Flow). Power Automate es un servicio basado en la nube que le permite crear flujos de trabajo automatizados entre diferentes aplicaciones y servicios.  <br/> <br/> Con AEM conector de automatización de Form Power, puede crear flujos de trabajo que se déclencheur automáticamente en función del envío de un formulario adaptable. Por ejemplo, puede crear un flujo de trabajo que envíe automáticamente una notificación por correo electrónico a una persona específica cuando un usuario envíe un formulario o cree una tarea en Microsoft Planner cuando un usuario complete un formulario.  <br/> <br/> AEM Forms Power Automate Connector es una potente herramienta que le permite automatizar e integrar su Forms adaptable con otras aplicaciones y servicios que se conectan con Microsoft Power Automate, lo que le permite trabajar con una gama más amplia de herramientas. Puede crear flujos de trabajo adaptados a sus necesidades específicas, con la capacidad de agregar acciones, condiciones y déclencheur personalizados. Además, Power Automate proporciona análisis e informes detallados que le permiten supervisar y optimizar los flujos de trabajo a lo largo del tiempo.|


>[!TAB Conectores de almacenamiento de Microsoft: OneDrive y Sharepoint]

||| |—|—| |![](/help/forms/assets/onedrive-and-sharepoint.jpg)|Los conectores de almacenamiento de AEM Forms Microsoft para OneDrive y SharePoint son conectores que le permiten integrar Adobe Experience Manager (AEM) Forms con Microsoft OneDrive y SharePoint. Estos conectores le permiten almacenar y administrar datos y documentos de AEM Forms en las soluciones de almacenamiento en la nube de Microsoft. <br/> <br/> Estos conectores le permiten almacenar y administrar datos y documentos de AEM Forms dentro de Microsoft OneDrive. Con este conector, puede cargar archivos de datos y archivos adjuntos a OneDrive y SharePoint directamente desde AEM Forms. <br/> <br/> El uso de los conectores de almacenamiento de AEM Forms Microsoft para OneDrive y SharePoint ofrece varias ventajas: <ul><li> **Integración**: Estos conectores le permiten integrar AEM Forms con las soluciones de almacenamiento basadas en la nube de Microsoft, lo que le permite aprovechar la potencia de estas plataformas. </li> <li> **Colaboración**: OneDrive y SharePoint son plataformas de colaboración que permiten a los integrantes del equipo trabajar juntos en archivos y documentos. Al integrar AEM Forms con estas plataformas, puede mejorar la colaboración y el trabajo en equipo. </li> <li> **Seguridad**: OneDrive y SharePoint proporcionan funciones de seguridad sólidas que garantizan que los datos y documentos se almacenen y se acceda a ellos de forma segura. </li> <br/> En general, los conectores de almacenamiento de AEM Forms Microsoft para OneDrive y SharePoint son potentes herramientas que le permiten almacenar y administrar datos y documentos de AEM Forms dentro de las soluciones de almacenamiento basadas en la nube de Microsoft, lo que mejora la colaboración y la seguridad.|


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