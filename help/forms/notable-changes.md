---
title: Cambios entre AEM 6.5 Forms y AEM Cloud Services
description: ¿Es usuario de Experience Manager Forms y desea actualizar a Adobe Experience Manager Forms as a Cloud Service? Conozca los cambios más importantes antes de actualizar o migrar a Cloud Service.
exl-id: 46fcc1b4-8fd5-40e1-b0fc-d2bc9df3802e
contentOwner: khsingh
source-git-commit: da53f453b0f2def98d92aae0e3e92d13eb748dab
workflow-type: tm+mt
source-wordcount: '1178'
ht-degree: 25%

---

# Cambios importantes para los usuarios existentes de Adobe Experience Manager 6.5 Forms  {#notable-changes-for-existing-AEM-Forms-users}

Adobe Experience Manager Forms as a Cloud Service ofrece algunos cambios importantes en las funciones existentes en comparación con Adobe Experience Manager Forms On-Premise y [!DNL Adobe-Managed Service] entornos. A continuación se enumeran las principales diferencias:

| Función/Capacidad | [!DNL AEM Forms] as a Cloud Service | AEM 6.5 Forms |
|---|---|---|
| Arquitectura nativa de la nube | ✅ | ⛌ |
| Adaptación automática basada en la carga | ✅ | ⛌ |
| Sin downtime en las actualizaciones | ✅ | ⛌ |
| Frecuencia de despliegue de funciones | Agile* | Trimestral |
| CDN (red de entrega de contenido) incluida | ✅ | ⛌ |
| Topologías optimizadas para lograr la máxima resiliencia y eficiencia | ✅ | ⛌ |
| Entorno de desarrollo nativo de la nube | ✅ | ⛌ |
| Autoservicio mediante Cloud Manager | ✅ | ⛌ |
| Actualizaciones automatizadas con integración continua y entrega continua (CI/CD) | ✅ | ⛌ |
| Integración con [!DNL Micosoft Power Automate] | ✅ | ⛌ |
| Integración con [!DNL DocuSign] | ✅ | ⛌ |
| Conectividad sencilla con Microsoft Dynamics y Salesforce | ✅ | ⛌ |
| Conectividad sencilla con el almacén de datos de Microsoft Azure | ✅ | ⛌ |
| Editor de reglas endurecidas | ✅ | ⛌ |
| Asistente de creación de formularios | ✅ | ⛌ |
| Compatibilidad personalizada con XCI para el documento de registro | ✅ | ⛌ |
| Forms adaptable <sup>1</sup> | ✅ | ✅ |
| Integración de datos con varias fuentes de datos | ✅ | ✅ |
| API de comunicaciones (servicios de documentos) <sup>2,3</sup> | ✅ | ✅ |
| Servicio de automated forms conversion <sup>4</sup> | ✅ | ✅ |
| Integración con [!DNL Adobe Sign] | ✅ | ✅ |
| Integración con [!DNL AEM Sites] | ✅ | ✅ |
| Integración con [!DNL Adobe Launch] | ✅ | ✅ |
| Integración con [!DNL Adobe Analytics] | ✅ | ✅ |
| Portal de Forms <sup>5</sup> | ✅ | ✅ |
| Flujos de trabajo de AEM | ✅ | ✅ |
| Documento de registro | ✅ | ✅ |
| Captcha invisible | ✅ | ✅ |
| Configuraciones del modelo de datos de formulario reutilizables | ✅ | ✅ |
| Documento de registro basado en Acrobat | ✅ | ✅ |
| Autenticación de identidad basada en ID de gobierno para Adobe Sign habilitado para Adaptable Forms | ✅ | ✅ |
| HTML5 <sup>6</sup> | ⛌ | ✅ |
| Seguridad de los documentos | ⛌ | ✅ |

Antes de proceder al servicio, tenga en cuenta los siguientes casos excepcionales:

+++ 1. Forms adaptable

* **Forms adaptable basado en XSD:** El servicio no es compatible con HTML5 Forms (Mobile Forms). Si procesa los formularios basados en XDP como HTML5 Forms, puede seguir utilizando la función en AEM 6.5 Forms. Puede utilizar la plantilla XDP para diseñar una plantilla para Document for Record. El servicio no admite Forms adaptable basado en XFA
* **Importación de plantillas de formulario adaptable:** Utilice la canalización de compilaciones y el repositorio Git correspondiente de su programa para importar las plantillas de formularios adaptables existentes.
* **Editor de reglas:** AEM Forms as a Cloud Service proporciona un [Editor de reglas](rule-editor.md#visual-rule-editor). El editor de código no está disponible en Forms as a Cloud Service. La utilidad de migración le ayuda a migrar los formularios que tengan reglas personalizadas (creadas en el editor de código). La utilidad convierte estas reglas en funciones personalizadas compatibles con Forms as a Cloud Service. Puede utilizar las funciones reutilizables con el editor de reglas para seguir obteniendo resultados obtenidos con las secuencias de comandos de reglas. `onSubmitError` o `onSubmitSuccess` ahora están disponibles como acciones en el Editor de reglas.
* **Proyectos y presentaciones:** El servicio no conserva los metadatos para borradores y envía Adaptive Forms.
* **Servicio de precarga:** De forma predeterminada, el servicio de rellenado previo combina los datos con un formulario adaptable en el cliente en lugar de combinar los datos en el servidor en AEM 6.5 Forms. La función ayuda a mejorar el tiempo necesario para rellenar previamente un formulario adaptable. Siempre puede configurar para ejecutar la acción de combinación en el servidor de Adobe Experience Manager Forms.
* **Enviar acciones:** La variable **Enviar correo electrónico como PDF** la acción no está disponible. La variable **Correo electrónico** enviar acción proporciona opciones para enviar archivos adjuntos y adjuntar el documento de registro (DoR) con el correo electrónico.
* **Componentes**: El servicio no admite la experiencia de firma en formularios y no incluye los componentes Resumen y verificación para Forms adaptable.



+++


+++ 2. Servicios de documentos: API de manipulación de documentos (servicio Assembler)


El servicio no admite operaciones que dependan de otros servicios o aplicaciones:

* No se admite la conversión de documentos en un formato que no sea de PDF a un formato de PDF. Por ejemplo, Microsoft Word para PDF, Microsoft Excel para PDF y HTML para PDF no son compatibles. Si los documentos están en un formato que no sea de PDF. Convierta estos documentos a formato de PDF antes de utilizarlos con las API de manipulación de documentos de comunicaciones. Por ejemplo, si sus documentos están en formato Microsoft Office, HTML, PostScript (PS) o XDP, convierta estos documentos a formato PDF antes de utilizarlos con documentos PDF.
* No se admiten las conversiones basadas en Distiller de Adobe. Por ejemplo, PostScript(PS) a PDF
* No se admiten las conversiones basadas en Forms Service. Por ejemplo, XDP para PDF forms.
* El servicio no admite la conversión de un PDF firmado o un PDF transparente a otro formato de PDF.
* La aplicación de derechos de uso mediante el servicio de extensiones de Reader no está disponible.
* El servicio no permite convertir documentos PDF firmados o transparentes al formato PDF/A.

+++


+++ 3. Servicios de documentos: API de generación de documentos (servicio de salida)

En una sola llamada o lote de API, solo puede utilizar una plantilla con varios archivos XML de DATOS. No se admite el uso de varias plantillas con varios archivos de datos en una sola llamada de API.

+++

+++ 4. Servicio de Automated forms conversion

El servicio no proporciona un metamodelo para el servicio de Automated forms conversion. Puede [descargarlo de la documentación del servicio de Automated forms conversion](https://experienceleague.adobe.com/docs/aem-forms-automated-conversion-service/using/extending-the-default-meta-model.html?lang=en#default-meta-model).

+++

+++ 5. Portal de Forms

La compatibilidad con el uso anónimo del portal de Forms no está disponible de forma predeterminada (OOTB). Puede personalizar el portal de formularios para permitir la visualización de formularios para usuarios que no inician sesión.

+++


+++ 6. HTML5 Forms (Forms móvil)

El servicio no es compatible con HTML5 Forms (Mobile Forms). Si procesa los formularios basados en XDP como HTML5 Forms, puede seguir utilizando la función en AEM 6.5 Forms.

+++


+++ 7. Modelo de datos de formulario

El modelo de datos de Forms solo admite extremos HTTP y HTTP para enviar datos. El servicio no admite SSL mutuo para el conector REST y la autenticación basada en certificados x509 para fuentes de datos SOAP. * Forms as a Cloud Service permite utilizar Microsoft Azure Blob, Microsoft Sharepoint, Microsoft OneDrive y servicios compatibles con operaciones generales de CRUD (Crear, Leer, Actualizar y Eliminar) ya que se admiten almacenes de datos, tanto la especificación de API abierta 2.0 como la especificación de API abierta. El servicio también proporciona compatibilidad con el conector JDBC.

+++


+++ 8. Entorno para desarrolladores

* Un entorno nativo de la nube no posee consola web (administrador de configuración). Puede usar el SDK de [[!DNL AEM Forms]  as a Cloud Service para generar configuraciones](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/configuring-osgi.html?lang=es#generating-osgi-configurations-using-the-aem-sdk-quickstart) y canalización de CI/CD e [implementar la configuración](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/deploy-code.html?lang=es#deployment-process) en su instancia de Cloud Service.
* De forma predeterminada, el correo electrónico admite los protocolos HTTP y HTTPs. [Póngase en contacto con el equipo de soporte](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/development-guidelines.html?lang=es#sending-email) para habilitar puertos para enviar correos electrónicos y para habilitar el protocolo SMTP para su entorno.
* El servicio no admite la conversión de un PDF firmado o un PDF transparente a otro formato de PDF. Antes de utilizar los paquetes de clientes con Forms as a Cloud Service, vuelva a compilar el código personalizado con la última versión de la convención de URL adobe-aemfd-docmanager* de la Forms adaptable localizada. Ahora se puede especificar una configuración regional en la URL. La nueva convención de URL permite almacenar en caché formularios localizados en Dispatcher o CDN. En el entorno de Cloud Service, utilice el formato de URL `http://host:port/content/forms/af/<afName>.<locale>.html` para solicitar una versión localizada de un formulario adaptable en lugar de `http://host:port/content/forms/af/afName.html?afAcceptLang=<locale>`. Adobe recomienda utilizar el almacenamiento en caché de CDN o Dispatcher. Ayuda a mejorar la velocidad de procesamiento de los formularios rellenados previamente
* Adobe Experience Manager Forms as a Cloud Service ofrece muchas nuevas funciones y posibilidades para sus Proyectos AEM. Con todo, se requieren algunos cambios en los proyectos de Adobe Experience Manager Maven para que sean compatibles con AEM Cloud Service. En un nivel superior, AEM requiere una separación de contenido y código en subpaquetes discretos para respetar la división entre contenido mutable e inmutable. Utilice la herramienta [Modernizador de repositorio](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/refactoring-tools/repo-modernizer.html?lang=es) para reestructurar los paquetes de proyectos existentes separando contenido y código en paquetes discretos para que sean compatibles con la estructura de proyectos definida para Adobe Experience Manager as a Cloud Service.


+++

<!-- 

### HTML5 Forms (Mobile Forms)

The service does not support HTML5 Forms (Mobile Forms). If you render your XDP-based forms as HTML5 Forms, you can continue using the feature on AEM 6.5 Forms.

### Adaptive Forms 

* **XSD-Based Adaptive Forms:** The service does not support HTML5 Forms (Mobile Forms). If you render your XDP-based forms as HTML5 Forms, you can continue using the feature on AEM 6.5 Forms. You can use XDP-template to design a template for Document for Record. The service does not support XFA based Adaptive Forms  
* **Importing Adaptive Form templates:** Use build pipeline and corresponding Git repository of your program to import existing Adaptive Form templates. 
*  **Rule editor:** AEM Forms as a Cloud Service provides a hardened [Rule editor](rule-editor.md#visual-rule-editor). The code editor is not available on Forms as a Cloud Service. The migration utility helps you migrate your forms that have custom rules (created in code editor). The utility converts such rules into custom functions supported on Forms as a Cloud Service. You can use the reusable functions with Rule editor to continue obtaining results obtained with rule scripts  The `onSubmitError` or `onSubmitSuccess` functions are now available as actions the Rule Editor.  
* **Drafts and submissions:** The service does not retain metadata for drafts and submitted Adaptive Forms.  
* **Prefill Service:** By default, the prefill service merges data with an Adaptive Form at client as opposed to merging data on Server in AEM 6.5 Forms. The feature helps improve the time required to prefill an Adaptive Form. You can always configure to run the merge action on the Adobe Experience Manager Forms Server. 
* **Submit actions:** The **Email as PDF** action is not available. The **Email** submit action provide options to send attachments and attach Document of Record (DoR) with email. 
* **Components**:  The service does not support in-form signing experience and does not include the Summary and Verify components for Adaptive Forms.  
* **Forms portal**: Support for anonymous use of Forms portal is not available out of the box (OOTB). You can customize the forms portal to enable displaying forms for non-logged in users.

### Form Data Model

* Forms data model supports only HTTP and HTTPs endpoints to submit data. The service does not support Mutual SSL for REST connector and x509 certificate-based authentication for SOAP data sources. * Forms as a Cloud Service allows to use Microsoft Azure Blob, Microsoft Sharepoint, Microsoft OneDrive, and services supporting general CRUD (Create, Read, Update, and Delete) operations as data stores, both Open API specification 2.0 and Open API specification are supported. The service also provides support for JDBC connector.


### Automated Forms Conversion Service     

The service does not provide meta-model for Automated Forms Conversion Service. You can [download it from Automated Forms Conversion Service documentation](https://experienceleague.adobe.com/docs/aem-forms-automated-conversion-service/using/extending-the-default-meta-model.html?lang=en#default-meta-model).


### Configurations

* Email support only HTTP and HTTPs protocols, by default. [Contact the support team](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/development-guidelines.html#sending-email) to enable ports for sending emails and to enable SMTP protocol for your environment.  
* If you use custom bundles, recompile your code with latest version of adobe-aemfd-docmanager before using these bundles with Forms as a Cloud Service. 


### Document Services: Document Manipulation APIs (Assembler Service)

The service does not support operations dependent on other services or applications:  

* Conversion of documents in a non-PDF format to a PDF format is not supported. For example, Microsoft Word to PDF, Microsoft Excel to PDF, and HTML to PDF are not supported. If your documents are in a non-PDF format. Convert such documents to PDF format before using those with Communications Document Manipulation APIs. For example, if your documents are in Microsoft Office, HTML, PostScript (PS), XDP format, convert these documents to PDF format before using those with PDF documents. 
* Adobe Distiller-based conversions are not supported. For example, PostScript(PS) to PDF
* Forms Service-based conversions are not supported. For example, XDP to PDF Forms.
* The service does not support converting a Signed PDF or Transparent PDF to another PDF format.
* Applying usage rights using Reader Extensions Service is not available. 
* The service does not provide the ability to convert signed or transparent PDF Documents to PDF/A format. 

### Document Services: Document Generation APIs (Output Service)

* In a single API call or batch, you can use one template with multiple DATA XML files. Using mutiple templates with multiple data files in a single API call is not supported. 

### Other differences

* A cloud-native environment does not have web console (configuration manager). You can use [[!DNL AEM Forms] as a Cloud Service SDK to generate configurations](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/configuring-osgi.html?lang=en#generating-osgi-configurations-using-the-aem-sdk-quickstart) and CI/CD pipeline to [deploy the configuration](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/deploy-code.html?lang=en#deployment-process) to your Cloud Service instance.
* Email support only HTTP and HTTPs protocols, by default. [Contact the support team](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/development-guidelines.html#sending-email) to enable ports for sending emails and to enable SMTP protocol for your environment.
* The service does not support converting a Signed PDF or Transparent PDF to another PDF format.* Before using your customer bundles with Forms as a Cloud Service, recompile your custom code with the latest version of adobe-aemfd-docmanager* URL convention of localized Adaptive Forms now supports specifying a locale in the URL. New URL convention enables caching localized forms on a Dispatcher or CDN. On Cloud Service environment, use the URL format `http://host:port/content/forms/af/<afName>.<locale>.html` to request a localized version of an Adaptive Form instead of `http://host:port/content/forms/af/afName.html?afAcceptLang=<locale>`. Adobe recommends using Dispatcher or CDN caching. It helps improve rendering speed of prefilled forms 
* Adobe Experience Manager Forms as a Cloud Service brings many new features and possibilities into your AEM Projects. However, there are some changes required to Adobe Experience Manager Maven projects to be compatible with AEM Cloud Service. At a high-level, AEM requires a separation of content and code into discrete subpackages to respect the split between mutable and immutable content. Use the [Repository Modernizer](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/refactoring-tools/repo-modernizer.html) tool to restructure existing project packages by separating content and code into discrete packages to be compatible with the project structure defined for Adobe Experience Manager as a Cloud Service.
-->




