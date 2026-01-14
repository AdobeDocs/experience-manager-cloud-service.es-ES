---
title: Arquitectura de AEM Forms as a Cloud Service para Formularios adaptables y API de comunicaciones
description: Familiarícese con la arquitectura de  [!DNL AEM Forms]  as a Cloud Service para conocer los aspectos de escalabilidad, resiliencia y rendimiento de la plataforma.
role: Admin, Developer, User
feature: Adaptive Forms
exl-id: 9d677bee-50ca-460e-b503-6b7799900735
source-git-commit: 281a8efcd18920dd926d92db9c757c0513d599fd
workflow-type: tm+mt
source-wordcount: '1097'
ht-degree: 94%

---

# Arquitectura de [!DNL AEM] Forms as a Cloud Service {#architecture}

| Versión | Vínculo del artículo |
| -------- | ---------------------------- |
| AEM 6.5 | [Haga clic aquí](https://experienceleague.adobe.com/docs/experience-manager-65/forms/install-aem-forms/aem-forms-architecture-deployment.html?lang=es) |
| AEM as a Cloud Service | Este artículo |

[!DNL Adobe Experience Manager Forms] as a Cloud Service es una solución nativa en la nube que permite a las empresas crear, administrar, publicar y actualizar comunicaciones y formularios digitales complejos a la vez que integran los datos enviados con procesos back-end y reglas comerciales y guardan datos en un almacén de datos externo. Es una ampliación de [!DNL Adobe Experience Manager as a Cloud Service]. Para obtener más información sobre la escala, la implementación, los entornos y otras infraestructuras, consulte [Introducción a la arquitectura de [!DNL Adobe Experience Manager as a Cloud Service]](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/core-concepts/architecture.html?lang=es).

AEM Forms as a Cloud Service admite dos casos de uso principales: inscripción digital y comunicaciones con el cliente. Las ilustraciones siguientes muestran la arquitectura de ambos casos de uso.

## Inscripción digital en Forms

![Inscripción digital en Forms](assets/forms-cloud-service-architecture-forms-digital-enrollment.svg)

## Comunicaciones de Forms

![Comunicación-Forms](assets/forms-cloud-service-architecture-forms-communications.svg)

## Aplicabilidad y casos de uso

### Seguro

## ¿AEM Forms puede gestionar operaciones de seguro a escala?

Sí. Cuando se implementa mediante arquitecturas recomendadas en Adobe Managed Services o en la nube privada, AEM Forms admite envíos de formularios de gran volumen y cargas de trabajo a escala empresarial.

## ¿AEM Forms es seguro para los datos del seguro?

Sí. AEM Forms admite la transmisión segura de datos, el acceso controlado y los mecanismos de autenticación empresarial, lo que lo hace adecuado para gestionar datos confidenciales del seguro.

## Componentes

Forms as a Cloud Service consta de varios componentes:

### CDN (red de distribución de contenido)

Todos los programas de AEM Forms as a Cloud Service tienen acceso a un [servicio CDN integrado](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/content-delivery/cdn.html?lang=es). Este servicio está incluido en la licencia de Forms as a Cloud Services.

### Autor

Un autor es una instancia de AEM Forms as a Cloud Service que se ejecuta en el modo de ejecución de autor estándar. Está pensado para usuarios internos, diseñadores de formularios y desarrolladores. Un entorno de autor habilita las siguientes funcionalidades:

* crear y administrar formularios;
* conectarse al servicio de conversión automatizada de formularios para convertir un formulario PDF o XDP en un formulario adaptable;
* crear y ejecutar flujos de trabajo centrados en Forms;
* administrar recursos de formularios adaptables;
* administrar recursos de comunicaciones;
* API sincrónicas de RESTful (API en tiempo real) y API por lotes para crear, ensamblar y ofrecer comunicaciones personalizadas y orientadas a la marca;
* API sincrónicas para combinar, reorganizar y validar documentos PDF.

### Publicación

Una instancia de publicación es una instancia de AEM Forms as a Cloud Service que se ejecuta en el modo de ejecución de publicación estándar. Las instancias de publicación están destinadas a los usuarios finales de aplicaciones basadas en formularios como, por ejemplo, los usuarios que acceden a un sitio web público y envían formularios. Habilita las siguientes funcionalidades:

* procesar y enviar formularios para usuarios finales;
* transportar datos de formulario enviados sin procesar para su posterior procesamiento y almacenamiento en el sistema final de registro;
* conectarse a un almacenamiento administrado por el cliente para almacenar datos;
* conectarse a Adobe Sign para firmar electrónicamente el registro de envío de los formularios adaptables;
* sincronizar las API para crear, ensamblar y ofrecer comunicaciones personalizadas y orientadas a la marca;
* sincronizar API para combinar, reorganizar y validar documentos PDF.

La replicación inversa no está disponible en AEM as a Cloud Service para enviar contenido/datos desde el servicio de Publicación al servicio de Autor. Sin embargo, puede configurar un formulario adaptable que se ejecute en el modo Publicación para enviar datos a un flujo de trabajo en el modo Autor (los flujos de trabajo solo se pueden ejecutar en el modo Autor). Esto resulta útil en casos de uso de aprobación.

#### Dispatcher

[Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/content-delivery/disp-overview.html?lang=es) es una herramienta de equilibrio de carga o almacenamiento en caché de Adobe Experience Manager que se puede utilizar junto con un servidor web de nivel empresarial.

### Servicios de Adobe

**Servicio de conversión automatizada de formularios**

El [servicio de conversión automatizada de formularios](https://experienceleague.adobe.com/docs/aem-forms-automated-conversion-service/using/introduction.html?lang=es) convierte automáticamente los formularios PDF y XFA en formularios adaptables basados en HTML5.

**Adobe Sign**

Adobe Sign es un servicio de firma electrónica basado en la nube que permite al usuario enviar, firmar, realizar un seguimiento y administrar procesos de firma mediante un explorador o dispositivo móvil. Puede integrar Adobe Sign con un formulario adaptable para automatizar los flujos de trabajo de firma, simplificar los procesos de firma única y múltiple y firmar electrónicamente formularios adaptables.

<!-- **PDF Service API**
Adobe’s PDF Services API lets create, combine, export, and extract data from PDFs through powerful and flexible cloud-based APIs. -->

### Almacenamiento administrado por el cliente

Forms as a Cloud Service proporciona opciones para almacenar contenido en un sistema de almacenamiento externo como un almacenamiento de blobs, Database o un servicio de almacenamiento. También puede almacenar datos de flujos de trabajo en proceso (datos de variables de flujos de trabajo de AEM) que contengan elementos de datos personales confidenciales (SPD) en un repositorio administrado por el cliente para un procesamiento seguro. Adobe recomienda almacenar los datos confidenciales únicamente en un almacenamiento administrado por el cliente.

Puede usar el **conector de almacenamiento unificado** para conectarse a Blob Storage y el **modelo de datos de formulario (FDM)** para conectarse a bases de datos o a servicios back-end (RESTful, SOAP, Azure Blob Storage, etc.).

### Servicios de documentos

Los servicios de documentos son los siguientes:

* El **servicio de salida (Comunicaciones - API de generación de documentos)** ayuda a crear documentos estandarizados, personalizados y aprobados por la marca, como correspondencia comercial, extractos, cartas de procesamiento de reclamaciones, avisos de beneficios, facturas mensuales o kits de bienvenida.

* El **servicio Assembler (Comunicaciones - API de manipulación de documentos)** ayuda a combinar, reorganizar y validar documentos PDF.

* El **servicio de documentos de registro (DoR)** ayuda a generar documentos de registro (DoR). El servicio se ejecuta en sus propios pods de forma independiente de las instancias de autor y publicación de Forms as a Cloud Service. Ayuda a mejorar el rendimiento y a escalar los pods de forma independiente en función de la carga.

### Cloud Manager

Cloud Manager es un componente esencial de [AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/overview/introduction.html?lang=es). Se trata del punto de entrada único para las operaciones y el desarrollador de nuestros clientes. Es el lugar desde donde se pueden administrar los programas y entornos AEM. Cloud Manager ha evolucionado como un portal de autoservicio donde se pueden crear y configurar los componentes principales de AEM as a Cloud Service:

* creación y administración de programas;
* creación y administración de entornos de AEM dentro de estos programas;
* creación y administración de canalizaciones para implementar el código del cliente y la configuración relacionada con un entorno específico;
* obtención de notificaciones de eventos de ciclo de vida importantes para estos componentes (por ejemplo, actualizaciones de productos). Para obtener más información sobre Cloud Manager, consulte [Familiarizarse con Adobe Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/cloud-manager/understand-cloud-manager-for-aem.html?lang=es) e [Introducción a Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/introduction-to-cloud-manager.html?lang=es).

### Consola de desarrollador

Una consola de desarrollador proporciona varios detalles de cada entorno de Forms as a Cloud Service que se ejecuta. Estos detalles son útiles para depurar el entorno. Para obtener más información, consulte [Depuración de AEM as a Cloud Service con la consola de desarrollador](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/developer-console.html?lang=es).

<!--

+++CDN (Content Delivery Network):

Every AEM Forms as a Cloud Service program has access to Fastly CDN service. It is included in the licence of Forms as a Cloud Services.

+++

+++Adaptive Forms
Adaptive Forms enable customers to author web-friendly reflowable web forms and fragments that are used by the customers for their data capture needs. This feature enables customers to manage their complex data capture needs easily, by using multiple integrations with Adobe Sign, Document Services, Form Data Model (FDM), Automated Forms Conversion service, and more.

+++

+++Automated Forms Conversion Service (AFCS)
Automated Forms Conversion service helps accelerate digitization and modernization of data capture experience through automated conversion of PDF forms to adaptive forms. The service, powered by Adobe AI, automatically converts your PDF forms to device-friendly, responsive, and HTML5-based adaptive forms. While using the existing investments in PDF Forms and XFA, the service also applies appropriate validations, styling, and layout to adaptive form fields during conversion.

+++

+++Form Data Model (FDM)
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
* Getting notified of important lifecycle events for these components (for example, product updates)
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
Also, one of the most common requirements for developers is quick access to the log files of the various environments. With [!DNL AEM Cloud Service], the log files of the different nodes in the Author, Publish are made available via the Cloud Manager, either in the form of files that can be downloaded or via APIs for tailing the logs. Due to the clear separation of code and content, developers can use a particular process for updating content as part of a deployment. The typical use cases for mutable content are:
* Standard “default” content that is part of the customer project (for example, folders, templates, workflows...)
* Search index definitions
* ACLs and permissions
* Service users and user groups
Set up your development environment, [Configure your CI/CD Pipeline](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/configuring-pipeline.html), and learn to [deploy your code](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/deploying-code.html) on the environment. -->

### Creación de formularios adaptables {#local-development}

Al configurar un entorno de [!DNL AEM Forms] as a Cloud Service, puede configurar entornos de desarrollo, ensayo y producción. Además, puede configurar un entorno de desarrollo local para realizar iteraciones y procesos de desarrollo rápidos. Puede descargar y configurar el SDK de AEM y el archivo de funciones de complementos de [!DNL AEM Forms] para configurar un entorno de desarrollo local de [!DNL Forms] as a Cloud Service. Para obtener instrucciones detalladas, consulte [Configuración de un entorno de desarrollo local](setup-local-development-environment.md).

## Depuración {#debugging}

AEM as a Cloud Service se ejecuta en una infraestructura en la nube escalable con capacidad de autoservicio. Requiere que los desarrolladores de AEM entiendan y depuren varias facetas de AEM as a Cloud Service, desde la compilación y la implementación hasta la obtención de detalles sobre la ejecución de aplicaciones de AEM. Para obtener información detallada, consulte [Depuración de AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/overview.html?lang=es).


>[!MORELIKETHIS]
>
>* [Introducción a Comunicaciones de AEM Forms as a Cloud Service](/help/forms/aem-forms-cloud-service-communications-introduction.md)
>* [Procesamiento de lote de Comunicaciones de AEM Forms as a Cloud Service](/help/forms/aem-forms-cloud-service-communications-batch-processing.md)
>* [Procesamiento de comunicaciones: API sincrónicas](/help/forms/aem-forms-cloud-service-communications.md)
