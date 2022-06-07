---
title: Experience Manager [!DNL AEM Forms] Arquitectura as a Cloud Service
description: Comprender la arquitectura de [!DNL AEM Forms] as a Cloud Service para conocer los aspectos de escalabilidad, resiliencia y rendimiento de la plataforma.
exl-id: 9d677bee-50ca-460e-b503-6b7799900735
source-git-commit: cd9ef0db59f07173c8c5bd4b38ff946b774ce53c
workflow-type: tm+mt
source-wordcount: '1045'
ht-degree: 2%

---

# [!DNL AEM] Arquitectura as a Cloud Service de Forms {#architecture}

[!DNL Adobe Experience Manager Forms] as a Cloud Service es una solución nativa de la nube para que las empresas creen, administren, publiquen y actualicen comunicaciones y formularios digitales complejos a la vez que integran los datos enviados con procesos back-end, reglas comerciales y guardan datos en un almacén de datos externo. Se extiende [!DNL Adobe Experience Manager as a Cloud Service]. Para obtener más información sobre la escala, la implementación, los entornos y otras infraestructuras, consulte [Introducción a la arquitectura de [!DNL Adobe Experience Manager as a Cloud Service]](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/core-concepts/architecture.html).

AEM Forms as a Cloud Service admite dos casos de uso principales: Inscripción digital y comunicaciones del cliente. Las ilustraciones siguientes ilustran la arquitectura de ambos casos de uso.

## Inscripción digital en Forms

![Matriculación digital en Forms](assets/forms-cloud-service-architecture-forms-digital-enrollment.svg)

## Forms Communications

![Forms-Comunicación](assets/forms-cloud-service-architecture-forms-communications.svg)

## Componentes

Forms as a Cloud Service consta de varios componentes:

### CDN (red de distribución de contenido)

Todos los programas as a Cloud Service de AEM Forms tienen acceso a [servicio CDN integrado](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/content-delivery/cdn.html). Se incluye en la licencia de Forms as a Cloud Services.

### Autor

Un Autor es una instancia as a Cloud Service de AEM Forms que se ejecuta en el modo de ejecución de Autor estándar. Está pensado para usuarios internos, diseñadores de formularios y desarrolladores. Un entorno Autor permite las siguientes funcionalidades:

* Creación y administración de formularios.
* Conexión al servicio de Automated forms conversion para convertir un formulario de PDF o XDP a un formulario adaptable.
* Creación y ejecución de flujos de trabajo centrados en Forms.
* Administración de recursos de formularios adaptables.
* Administración de recursos de comunicaciones.
* API sincrónicas de RESTful (API en tiempo real) y API por lotes para crear, ensamblar y ofrecer comunicaciones personalizadas y orientadas a la marca.
* API sincrónicas para combinar, reorganizar y validar documentos de PDF.

### Publicación

Una instancia de publicación es una instancia as a Cloud Service de AEM Forms que se ejecuta en el modo de ejecución de publicación estándar. Las instancias de publicación están destinadas a los usuarios finales de aplicaciones basadas en formularios, por ejemplo, los usuarios que acceden a un sitio web público y envían formularios. Habilita las siguientes funcionalidades:

* Procesamiento y envío de formularios para usuarios finales.
* Transporte de datos de formulario enviados sin procesar para su posterior procesamiento y almacenamiento en el sistema final de registro.
* Conexión al almacenamiento administrado por el cliente para almacenar datos.
* Conexión con Adobe Sign para firmar por correo electrónico un registro de envío de formulario adaptable.
* Sincronice las API para crear, ensamblar y ofrecer comunicaciones personalizadas y orientadas a la marca.
* Sincronizar API para combinar, reorganizar y validar documentos de PDF.

La replicación inversa no está disponible en AEM as a Cloud Service para enviar contenido/datos desde el servicio de publicación al servicio de creación. Sin embargo, puede configurar un Forms adaptable que se ejecute en Publicar para enviar datos a un flujo de trabajo en un autor (los flujos de trabajo solo se pueden ejecutar en el autor). Esto resulta útil en casos de uso de aprobación.

#### Dispatcher

[Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/content-delivery/disp-overview.html) es la herramienta de equilibrio de carga o almacenamiento en caché de Adobe Experience Manager que se puede utilizar con un servidor web de clase empresarial.

### Servicios de Adobe

**Servicio de automated forms conversion**

[servicio de automated forms conversion](https://experienceleague.adobe.com/docs/aem-forms-automated-conversion-service/using/introduction.html?lang=es) convierte automáticamente sus formularios PDF y XFA en formularios adaptables, adaptables y basados en HTML5.

**Adobe Sign**

Adobe Sign es un servicio de firma electrónica basado en la nube que permite al usuario enviar, firmar, rastrear y administrar procesos de firma mediante un explorador o dispositivo móvil. Puede integrar Adobe Sign con un formulario adaptable para automatizar los flujos de trabajo de firma, simplificar los procesos de firma única y múltiple y firmar electrónicamente formularios adaptables.

<!-- **PDF Service API**
Adobe’s PDF Services API lets create, combine, export, and extract data from PDFs through powerful and flexible cloud-based APIs. -->

### Almacenamiento administrado por el cliente

Forms as a Cloud Service proporciona opciones para almacenar contenido en un sistema de almacenamiento externo como Blob Store, Database o un servicio de almacenamiento. También puede almacenar datos de flujos de trabajo en proceso (AEM datos de variables de flujo de trabajo) que contengan elementos de datos personales confidenciales (SPD) en un repositorio administrado por el cliente para un procesamiento seguro. Adobe recomienda almacenar datos confidenciales solo en almacenamiento administrado por el cliente.

Puede usar la variable **Conector de almacenamiento unificado** para conectarse al almacenamiento de blob y **Modelo de datos de formulario** para conectarse a bases de datos o servicios back-end (RESTful, SOAP, Azure Blob Storage, etc.).

### Servicios de documento

Los servicios de documentos son los siguientes:

* **Servicio de salida (comunicaciones - API de generación de documentos)** ayuda a crear documentos estandarizados, personalizados y aprobados por la marca, como correspondencia comercial, extractos, cartas de procesamiento de reclamaciones, avisos de beneficios, facturas mensuales o kits de bienvenida.

* **Servicio del ensamblador (comunicaciones - API de manipulación de documentos)** ayuda a combinar, reorganizar y validar documentos de PDF.

* **Servicio de documento de registro (DoR)** ayuda a generar el documento de registro (DoR). El servicio se ejecuta en sus propios pods de forma independiente Autor y Publicar instancias de Forms as a Cloud Service. Ayuda a proporcionar un mejor rendimiento y a escalar los pods de forma independiente en función de la carga.

### Cloud Manager

Cloud Manager es un componente esencial para [AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/overview/introduction.html). Es el punto de entrada único para las operaciones y el desarrollador de nuestros clientes. Es el lugar desde donde se pueden administrar los programas y entornos AEM. Cloud Manager ha evolucionado como un portal de autoservicio en el que se pueden crear y configurar los componentes principales del AEM as a Cloud Service:

* Creación y administración de programas
* Creación y administración de los entornos AEM dentro de los programas
* Creación y administración de canalizaciones para implementar el código del cliente y la configuración en un entorno en particular
* Obtención de notificaciones de eventos de ciclo vital importantes para estos componentes (por ejemplo, actualizaciones de productos) Para obtener más información sobre Cloud Manager, consulte [Comprender Adobe Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/cloud-manager/understand-cloud-manager-for-aem.html) y [Introducción a Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/introduction-to-cloud-manager.html?lang=es).

### Developer Console

Una consola de desarrollador proporciona varios detalles de cada entorno de Forms as a Cloud Service que se ejecuta. Estos detalles son útiles para depurar el entorno. Para obtener más información, consulte [Depuración AEM as a Cloud Service con Developer Console](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/developer-console.html).

<!--

+++CDN (Content Delivery Network):

Every AEM Forms as a Cloud Service program has access to Fastly CDN service. It is included in the licence of Forms as a Cloud Services.

+++

+++Adaptive Forms
Adaptive Forms enable customers to author web-friendly reflowable web forms and fragments that are used by the customers for their data capture needs. This feature enables customers to manage their complex data capture needs easily, by leveraging multiple integrations with Adobe Sign, Document Services, Form Data Model, Automated Forms Conversion service, and more.

+++

+++Automated Forms Conversion Service (AFCS)
Automated Forms Conversion service helps accelerate digitization and modernization of data capture experience through automated conversion of PDF forms to adaptive forms. The service, powered by Adobe Sensei, automatically converts your PDF forms to device-friendly, responsive, and HTML5-based adaptive forms. While leveraging the existing investments in PDF Forms and XFA, the service also applies appropriate validations, styling, and layout to adaptive form fields during conversion.

+++

+++Form Data Model
The Form Data Model (FDM) feature is the standard way of creating data integrations with external/internal data sources and using them across the different Forms as a Cloud Service features. FDM provides a rich editor for customers to integrate, define, and manage relationships between the different entities and data sources and perform operations on them. Form data is stored in a data store hosted on the customer premises. Organizations can also use blob store hosted by the cloud provider and Adobe Experince Platform to store data.

+++

+++Forms Workflows
Forms-centric workflows is an extension to the default AEM Workflow and provides our customers with additional workflow capabilities like Form Data review, task assignment, and document services invocation.

+++

+++Communications
Forms as a Cloud Service offering consists of multiple services tailored specifically for document processing.

+++

+++Document of Record
A Document of Record is a PDF version of a form. It provides an ability to keep a record of the information  that you provide and submit in an Adaptive Form in PDF fromat. The service provides a default DoR template and tools to develop a custom template.

+++

## Terminologies

<!-- ## Cloud Manager{#cloud-manager}

Cloud Manager is an essential component to [AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/overview/introduction.html?lang=en). Each new tenant of the [!DNL AEM Forms] as a Cloud Service is first provisioned for Cloud Manager access. Cloud Manager is the single-entry point for the operations and developer persona of our customers. It is the place from where the AEM programs and environments can be managed. Cloud Manager has evolved as a self-service portal where the main components of the AEM as a Cloud Service can be created and configured:

* Creating and managing programs
* Creating and managing the AEM environments within the programs
* Creating and managing the pipelines for deploying the customer code and configuration to a particular environment
* Getting notified of important lifecycle events for these components (e.g. product updates)
For more information about Cloud Manager, see [Understand Adobe Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/cloud-manager/understand-cloud-manager-for-aem.html) and [Introduction to Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/introduction-to-cloud-manager.html).

## Users and Authentication {#users-and-authentication}

AEM as a Cloud Service includes Admin Console support for AEM instances and Adobe Identity Management System (IMS) based authentication. The Admin Console allows administrators to centrally manage all Experience Cloud users. Users and Groups can be assigned to product profiles associated with AEM as a Cloud Service instances, allowing them to log in to that instance. For more information about users, authentication, and, and accessing an instance of AEM as a Cloud Service, see [IMS Support for [!DNL Adobe Experience Manager] as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/security/ims-support.html?lang=en#introduction).

Various personas are involved in a typical [!DNL AEM Forms] project. After you log in to your [!DNL AEM Forms] as a Cloud Service instance, you can [add users in admin console](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/security/ims-support.html) for personas applicable to your organization or project and [assign users to built-in groups](forms-groups-privileges-tasks.md) to provide them required privileges.

To learn various in-built [!DNL AEM Forms] specific user groups and privileges available on [!DNL AEM Forms] as a Cloud Services instance, see [Configure, user, roles and groups](forms-groups-privileges-tasks.md). 

## Developer Experience {#developer-experience}

The new architecture supporting AEM as a Cloud Service brings some key changes to the overall developer experience. One of the major goals for the changes to developer experience is to allow migration to AEM as a Cloud Service as quickly as possible, with little modifications to existing custom code.

## Cloud development {#cloud-development}

Here are the guidelines to run your existing code smoothly on AEM as a Cloud Service environment:

* Store your code and configurations to the Git repository of the associated Cloud Manager program. It makes managing and integrating code with CI/CD a breeze.  
* Make application code and configuration compatible with the baseline [!DNL AEM Forms] images. Using the latest APIs helps to build faster and secure applications.
* Use the Cloud Manager pipeline associated with the Cloud Manager environment to build and deploy applications. It helps you bring the latest features and bug fixed for [!DNL AEM Forms] as a Cloud Service to your environment.
* Try that your custom applications pass all the code quality, security, and performance gates enforced in the pipeline. It helps build secure and better performing applications which leads to better customer experience. You can always use Cloud Manager UI to skip some checks.
This process is commonly referred to as cloud-first development. [!DNL AEM Forms] as a Cloud Service also provides an SDK to support rapid development before the pending code and configuration changes are attempted in the cloud.
Some interfaces that were previously part of the AEM QuickStart are no longer available to the users of the AEM as a Cloud Service environment. For instance, the Web Console where OSGI bundles and their associated configuration are managed. The CRXDE Lite content repository browser becomes only accessible on non-production environment types. A subset of the Web Console functionalities that developers require, especially when it comes to diagnostics and status purposes, is made available via a new developer console.
Also, one of the most common requirements for developers is quick access to the log files of the various environments. With [!DNL AEM Cloud Service], the log files of the different nodes in the Author, Publish are made available via the Cloud Manager, either in the form of files that can be downloaded or via APIs for tailing the logs. Due to the clear separation of code and content, developers can leverage a particular process for updating content as part of a deployment. The typical use cases for mutable content are:
* Standard “default” content that is part of the customer project (e.g. folders, templates, workflows...)
* Search index definitions
* ACLs and permissions
* Service users and user groups
Set up your development environment, [Configure your CI/CD Pipeline](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/configuring-pipeline.html), and learn to [deploy your code](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/deploying-code.html) on the environment. -->

### Creación de formularios adaptables {#local-development}

Al configurar y configurar un [!DNL AEM Forms] entorno as a Cloud Service, puede configurar entornos de desarrollo, ensayo y producción. Además, configure un entorno de desarrollo local para realizar iteraciones y procesos de desarrollo rápidos. Puede descargar y configurar AEM SDK y [!DNL AEM Forms] archivo de funciones de complemento para configurar un [!DNL Forms] Entorno de desarrollo as a Cloud Service.  Para obtener instrucciones detalladas, consulte [Configuración de un entorno de desarrollo local](setup-local-development-environment.md).

## Depuración {#debugging}

AEM se ejecuta en infraestructura de nube con capacidad de autoservicio, escalable y de autoservicio. Requiere que los desarrolladores de AEM entiendan y depuren varias facetas de AEM as a Cloud Service, desde la compilación y la implementación hasta obtener detalles de la ejecución de aplicaciones de AEM. Para obtener información detallada, consulte [Depuración AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/overview.html).
