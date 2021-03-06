---
title: 'Funciones y funcionalidades clave de Adobe Experience Manager (AEM) Forms as a Cloud Service '
description: '"[!DNL AEM Forms] as a Cloud Service es una plataforma para crear, administrar, publicar formularios de clase empresarial y procesos empresariales."'
exl-id: 3a90b0aa-369a-4350-9904-79ef656b0f9a
source-git-commit: bc4da79735ffa99f8c66240bfbfd7fcd69d8bc13
workflow-type: tm+mt
source-wordcount: '410'
ht-degree: 5%

---

<!-- # Introduction to [!DNL AEM Forms] as a Cloud Service {#overview}

Adobe Experience Manager Forms as a Cloud Service offers a cloud-native, Platform as a Service (PaaS) solution for businesses to create, manage, publish, and update complex digital forms while integrating submitted data with back-end processes, business rules, and saving data in an external data store. The service is always current, always available, and always learning.

You can use the service to create and rollout  interactive and engaging digital forms. For example, an organization is looking to digitize their customer enrollment journey. They have multiple data sources with existing customer data, they are looking to pre-populate forms, add e-sign their forms, and archive filled forms as PDF files. Besides, the organization has multiple print forms (PDF forms), they are also looking to convert all of their print forms to digital forms.

The organization can use [!DNL AEM Forms] as a Cloud Service to create digital forms, connect forms to existing data sources, integrate forms with [!DNL Adobe Sign] to add e-signatures to forms, and generate Document of Record (DoR) to archive filled forms as PDF files. The organization can also use the service to convert their existing PDF forms to digital forms. 

An organization can sign up for [!DNL AEM Forms] as a Cloud Service and start using all these features without waiting to buy and set up a local infrastructure. The service also frees the organizations from the cycle of upgrades as it is always up to date and always offers the latest feature.  -->

# Funciones y capacidades clave {#key-features}

[!DNL AEM Forms] as a Cloud Service ofrece varias funciones nativas de la nube, como una arquitectura nativa de la nube, escalado autom??tico, sin downtime para las actualizaciones, una CDN (red de entrega de contenido), un entorno de desarrollo nativo de la nube y la capacidad de autoservicio de los entornos mediante Cloud Manager. Puede utilizar el servicio para:

* [Crear Forms adaptable](creating-adaptive-form.md#strong-create-an-adaptive-form-strong) que se representan autom??ticamente para el dispositivo y el navegador de un usuario.

   ![Formularios adaptables](assets/rule-editor-example.gif)

* [Crear PDF forms perfectos para p??xeles](use-forms-designer.md#create-an-adaptive-form) eso parece casi papel.

* Uso [servicio de automated forms conversion](https://experienceleague.adobe.com/docs/aem-forms-automated-conversion-service/using/introduction.html?lang=es) para convertir un formulario de PDF en un formulario adaptable. Ayuda a acelerar la digitalizaci??n y la modernizaci??n de las experiencias de captura de datos de su organizaci??n.

   ![servicio de automated forms conversion](assets/pdf-to-adaptive-form-gitx50.gif)

* [Crear procesos empresariales](aem-forms-workflow-step-reference.md#create-form-centric-workflows). Por ejemplo, puede crear y almacenar en d??clencheur un flujo de trabajo de aprobaci??n y rechazo al enviar un formulario adaptable.

Adem??s de lo anterior [!DNL AEM Forms] as a Cloud Service ofrece las siguientes funciones y capacidades:

* Una interfaz gr??fica de usuario f??cil de usar para que los usuarios empresariales puedan importar, administrar, previsualizar y publicar f??cilmente formularios
* Un directorio de formularios adaptable con potentes caracter??sticas de b??squeda que utilizan palabras clave, etiquetas y metadatos
* Detecci??n din??mica del dispositivo y la ubicaci??n de un usuario para procesar el formulario correctamente en los canales web y m??viles
* [Integraci??n con Adobe Sign](adobe-sign-integration-adaptive-forms.md) Servicios o Scribble para firmar electr??nicamente documentos que contengan informaci??n confidencial
* Capacidad para [conectar el servicio a varios tipos de fuentes de datos](data-integration.md#create-an-adaptive-form) para enviar y recuperar datos. El servicio admite el env??o y la recuperaci??n de datos desde servicios web RESTful, servicios web basados en SOAP y servicios habilitados para OData.
* Integraci??n con AEM Sites. Permite incrustar un formulario adaptable en una p??gina de AEM Sites. Tambi??n puede integrar un formulario adaptable a cualquier p??gina web.
* Capacidad para crear un documento de registro (DoR) para mantener un registro de la informaci??n que proporciona y env??a en un formulario adaptable para que pueda remitirlo m??s adelante. Un DoR es una versi??n PDF de un formulario. Incluye una plantilla y datos. El servicio proporciona una plantilla de documento de trabajo y herramientas predeterminadas para desarrollar una plantilla personalizada.
* Capacidad para crear Forms adaptable para producir datos compatibles con esquemas. Le ayuda a enviar los datos capturados a procesos y fuentes de datos existentes sin realizar modificaciones ni modificarlas al m??nimo.
* Capacidad para crear un servicio de rellenado previo para rellenar un formulario con datos de clientes existentes basados en un criterio. Ayuda a acelerar el proceso de rellenado de formularios y a reducir la tasa de abandono.


<!-- 

## Enterprise-class forms {#enterprise-class-forms}

You can create enterprise class forms (Adaptive Forms) and deliver beautiful, interactive, responsive, and personalized experiences to your customers. These forms change behavior and appearance based on the underlying device. You can also use themes and templates with Adaptive Forms to mandate a uniform structure and appearance for all the forms of an organization or a department.

![Creating custom patterns for fields in CrxDe](assets/adaptive-form.png)

## Automatic conversion of PDF forms to Adaptive Forms {#automatic-conversion-of-pdf-forms-to-adaptive-forms}

You can use Automated Forms Conversion service to convert a PDF Form to an Adaptive Form. It helps you accelerate digitization and modernization of data capture experiences of your organization.

![Creating custom patterns for fields in CrxDe](assets/pdf-to-adaptive-form-gitx50.gif)

## Data Integration {#data-integration}

You can connect the service to various types of data sources to send and retrieve data. The service supports sending and retrieving data from RESTful web services, SOAP-based web services, and OData enabled services.

![Build dynamism and interactivity to Adaptive Forms](assets/rule-editor-example.gif)

## Integration with [!DNL Adobe Sign] {#integration-with-adobe-sign}

 You can integrate the service with [!DNL Adobe Sign] and add [!DNL Adobe Sign] fields to an Adaptive Form. It allows your users to e-sign an Adaptive Form and use [!DNL Adobe Sign] with AEM Workflows. You can use AEM Workflows to develop a business logic and send forms and documents to recipients for signatures based on the business logic.

![Creating custom patterns for fields in CrxDe](assets/adobe-sign.png)


## Integration with [!DNL AEM Sites] {#integration-with-aem-sites}

You can embed an adaptive form in an AEM Sites or an external webpage. The service provides a component out of the box to integrate an adaptive forms to an AEM Sites page.

![integrate an adaptive forms to an AEM Sites page](assets/integrate.png)

## Business Processes Automation {#bpa}

You can use AEM Workflows to create business processes and automate operations. For example, You can create and trigger an approval and rejection workflow on submission of an Adaptive Form. 

![Create and trigger an approval and rejection workflow](assets/workflow.png)

## Document of Record {#dor}

You can create a Document of Record (DoR) to keep a record of the information that you provide and submit in an Adaptive Form so that you can refer to it later. A DoR is a PDF version of a form. It includes both a template and data. The service provides a default DoR template and tools to develop a custom template.

![Build dynamism and interactivity to Adaptive Forms](assets/designer.png)

## Rule editor {#rule-editor}

Rule editor empowers you to build dynamism and interactivity to Adaptive Forms. These rules define actions to trigger on form objects based on preset conditions, user inputs, and user actions on the form. It helps  streamline the form filling experience while ensuring accuracy and speed.
  
![Creating custom patterns for fields in CrxDe](assets/form-data-model.png)


## WYSIWYG editors {#wysiwyg-editor} 

The service provides several WYSIWYG editors: Adaptive Forms editor, Theme editor, and Template editor. These help you create and edit forms and related assets in WYSIWYG manner. The editors also provide out-of-the-box options to simulate views for popular mobile devices, tablets, and desktop screen configurations.

![Creating custom patterns for fields in CrxDe](assets/emulators.png)

## Schema-compliant data {#schema-complaint-data}

You can create Adaptive Forms to produce schema-compliant data. It helps you submit captured data to existing processes and data sources without any or minimal modifications.

![Build dynamism and interactivity to Adaptive Forms](assets/display-validation-error.gif)

## Prefill a form

You can create a prefill service to fill a form with existing customer data based on a criteria. It helps fasten the form filling process and reduce the abandon rate.

## Submit Actions

A Submit Action allows you to persist and process captured data. The service provides several Submit Actions out-of-the-box. You can use these Submit Actions to send submitted data to a REST endpoint, database, or an AEM Workflow. You can also email submitted data along with attachments and Document of Record(DoR). You can also develop a custom Submit Action to perform an action specific to your business.

* **Emulators:** You can view an Adaptive Form in an in-built emulator. It helps you simulate how an Adaptive Form appears on different devices to an end user. It provides out-of-the-box options to simulate views for popular mobile devices, tablets, and desktop screen configurations. 

In addition to standard [!DNL AEM Forms] features, [!DNL AEM Forms] as a Cloud Service provides several cloud-native capabilities such as a cloud-native architecture, auto-scaling, zero downtime for upgrades, a CDN (Content Delivery Network), cloud-native development environment, and ability to self-Service the environments via Cloud Manager. -->
