---
title: Preguntas frecuentes sobre AEM Forms as a Cloud Service
description: Preguntas frecuentes sobre Forms as a Cloud Service
contentOwner: khsingh
role: User
feature: Adaptive Forms
index: false
exl-id: 0b14b680-7da5-4e0b-bd6a-c379d148f9d7
source-git-commit: 5ee37f59bb959e0549c0541c6568aa8c135c330e
workflow-type: ht
source-wordcount: '975'
ht-degree: 100%

---

# Preguntas frecuentes {#frequently-asked-questions}

* **¿Puedo usar el Editor de código para crear reglas?**
Puede usar el Editor visual para crear reglas. El Editor de código no está disponible en [!DNL Forms] as a Cloud Service. Si el formulario adaptable utiliza scripts de reglas desarrolladas mediante el Editor de código, utilice la [Utilidad de migración](migrate-to-forms-as-a-cloud-service.md) para convertir los scripts de código en funciones personalizadas. Puede utilizar funciones personalizadas con el Editor visual para seguir obteniendo los mismos resultados que con el Editor de código.

* **¿Puedo crear un formulario adaptable basado en XFA en instancias de Cloud Service?**
Sí, puede crear un formulario adaptable basado en XFA en una instancia de Cloud Service. Sin embargo, la compatibilidad con los formularios adaptables basados en XFA no está disponible para el SDK de AEM Forms as a Cloud Service (entorno de desarrollo local). Si tiene intención de utilizar formularios adaptables basados en XFA con el SDK de AEM Forms as a Cloud Service, póngase en contacto con el servicio de asistencia de Adobe e incluya información sobre su caso de uso y los requisitos específicos en el mensaje.

<!-- * **Can I use an XDP as a Document of Record (DoR) template? Is Forms Designer included in AEM Forms as a Cloud Service license?** 

  Yes, you can use an XDP as a Document of Record template on Cloud Service instances. However, support to use XDP as a Document of Record template is not available for AEM Forms as a Cloud Service SDK (Local development environment). -->

* **¿Puedo migrar contenido desde entornos locales o de [!DNL Adobe-Managed Services] a un entorno de [!DNL Forms] as a Cloud Service?**
Sí, puede migrar código, contenido y recursos personalizados desde entornos locales o de [!DNL Adobe-Managed Services] a un entorno de [!DNL Forms] as a Cloud Service. Para obtener instrucciones detalladas, consulte [Migrar a Forms as a Cloud Service](migrate-to-forms-as-a-cloud-service.md).

<!-- You can use package manager or Experience Manager UI to [export and import Forms and related assets](import-export-forms-templates.md), use the migration utility to make your existing assets compatible with [!DNL Forms] as a Cloud Service, use the [Best Practices Analyzer](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/best-practices-analyzer/overview-best-practices-analyzer.html?lang=es#best-practices-analyzer) tool to find the features and APIs that require changes and updated before migration, and use the [Content Transfer Tools](https://docs.adobe.com/content/help/es-ES/experience-manager-cloud-service/moving/home.html) to move your custom code without refactoring it. -->

* **¿Dónde puedo obtener la documentación de referencia de la API de [!DNL Java™] de AEM [!DNL Forms] as a Cloud Service?**
Puede descargar la documentación de referencia de la API de Java™ en [!DNL Maven Central Repository]. Para descargarla:
   1. Vaya a [[!DNL Maven Central Repository]](https://mvnrepository.com/artifact/com.adobe.aem/aem-forms-sdk-api).
   1. Busque y abra la página que contiene la última versión del SDK de [!DNL Experience Manager Forms].
   1. Haga clic en la opción Ver todo para ver todos los archivos.
   1. Descargue y extraiga `aem-forms-sdk-api-<version>-javadocs`.jar.
   1. Abra el archivo index.html para ver la documentación de referencia de la API.

* **¿Dónde puedo obtener la referencia de la API de [!DNL JavaScript™] para formularios adaptables?**
Puede descargar la documentación de referencia de la API de [!DNL JavaScript™] en [!DNL  Maven Central Repository]. Para descargarla:
   1. Abra [[!DNL Maven Central Repository]](https://mvnrepository.com/artifact/com.adobe.aem/aem-forms-sdk-api).
   1. Busque y abra la página que contiene la última versión del SDK de [!DNL Experience Manager Forms].
   1. Haga clic en la opción Ver todo para ver todos los archivos.
   1. Descargue y extraiga `aem-forms-sdk-api-<version>-jsdoc.jar`.
   1. Abra el archivo index.html para ver la documentación de referencia de la API.

* **¿Puedo seguir utilizando las temáticas y las plantillas existentes?**
Sí, puede seguir utilizando las temáticas creadas con AEM 6.4 Forms y AEM 6.5 Forms después de usar la [Utilidad de migración](migrate-to-forms-as-a-cloud-service.md) para moverlos a [!DNL AEM Forms] as a Cloud Service.

  También puede crear un proyecto basado en el [Arquetipo](setup-local-development-environment.md#forms-cloud-service-local-development-environment) de [!DNL AEM Forms] as a Cloud Service y utilizar las plantillas y las temáticas de ejemplo que incluye.

* **¿Puedo producir datos compatibles con esquemas?**
Sí, puede crear formularios adaptables para producir datos compatibles con esquemas.

<!-- * **Can I pass custom parameters to the prefill service?**
Custom parameters are planned for an upcoming release. -->

* **¿Puedo almacenar en caché el contenido protegido?**
La funciones relacionadas con el almacenamiento en caché de contenido seguro están deshabilitadas de forma predeterminada. Para habilitarlas, puede seguir las instrucciones que se indican en [Almacenamiento en caché de contenido seguro](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/permissions-cache.html?lang=es).

* **Tengo un formulario adaptable localizado; pero no se está representando la versión localizada. ¿Cuál puede ser la causa y cómo puedo resolver el problema?**

  La convención de URL de los formularios adaptables localizados admite ahora la especificación de una configuración regional en la URL. La nueva convención de URL permite almacenar en caché formularios localizados en Dispatcher o CDN. En el entorno de Cloud Service, utilice el formato de URL `http://host:port/content/forms/af/<afName>.<locale>.html` para solicitar una versión localizada de un formulario adaptable en lugar de `http://host:port/content/forms/af/afName.html?afAcceptLang=<locale>`. Adobe recomienda utilizar el almacenamiento en caché de CDN o Dispatcher. Ayuda a mejorar la velocidad de procesamiento de los formularios rellenados previamente.

* **He actualizado un formulario adaptable; ¿la versión actualizada no está disponible para que los clientes la utilicen?**
De forma predeterminada, CDN actualiza la caché cada 5 minutos. Espere 5 minutos y, a continuación, compruebe si aparece la versión actualizada.

* **¿Puedo utilizar el Paso de firma de un formulario adaptable para crear una experiencia de firma en el explorador?**
No, el Paso de firma no está disponible para [!DNL Forms] as a Cloud Service. Quite el Paso de firma de los formularios adaptables. En su lugar, permita a los usuarios firmar los formularios adaptables después del envío. De esta forma, podrá seguir proporcionando la experiencia de firma en el explorador.

* **¿Puedo utilizar el paso Verificar en un formulario adaptable?**
No, el paso Verificar no está disponible para [!DNL Forms] as a Cloud Service. Quite el paso Verificar de los formularios adaptable existentes antes de trasladarlos a un entorno de Cloud Service.

* **¿Es posible agregar gráficos a un formulario adaptable?**
Sí, es posible agregar gráficos a los formularios adaptables. Los formularios adaptables proporcionan un componente de gráficos. Puede utilizarlo para agregar gráficos a un formulario adaptable.

* **¿Puedo conectar un modelo de datos de formulario a un modelo de base de datos relacional?**
Puede conectar un modelo de datos de formulario al perfil de usuario de [!DNL RESTful web services], [!DNL SOAP-based web services], [!DNL OData services] y Experience Manager como fuentes de datos. <!--Support to connect a Form Data Model with a relational database is not available.-->

* **¿Puedo utilizar certificados personalizados con el modelo de datos de formulario (FDM) para la autenticación?**
El modelo de datos de formulario (FDM) no ofrece ningún método para utilizar certificados personalizados para la autenticación. Por lo tanto, los certificados personalizados, como x509 y SSL bidireccional, no son compatibles.

* **¿Puedo utilizar la acción de envío del portal de Forms en formularios adaptables?**

  Puede modificar los formularios adaptables existentes para utilizar las acciones de envío [Enviar al punto final REST](configuring-submit-actions.md#submit-to-rest-endpoint), [Enviar correo electrónico](configuring-submit-actions.md#send-email), [Enviar mediante modelo de datos de formulario (FDM)](configuring-submit-actions.md#submit-using-form-data-model) e [Invocar un flujo de trabajo de AEM](configuring-submit-actions.md#invoke-an-aem-workflow). El portal de Forms y la acción de envío del portal de Forms todavía no están disponibles. Consulte las notas de la versión mensuales para obtener más información la disponibilidad de las funciones.

* **¿Puedo usar la aplicación [!DNL AEM Forms] con [!DNL AEM Forms] as a Cloud Service?**

  Los formularios adaptables ofrecen un diseño interactivo. Estos formularios cambian el aspecto, el diseño y la interactividad en función del dispositivo subyacente. Puede seguir utilizando formularios adaptables en dispositivos móviles mientras consulta las notas de la versión mensuales sobre la disponibilidad de las funciones.

* **¿Qué funciones no forman parte de la versión inicial de GA?**
El portal de Forms, la aplicación [!DNL AEM Forms], la integración con Adobe Analytics y la integración con Adobe Target no forman parte de la versión inicial de GA. Consulte las notas de la versión mensuales para obtener más información sobre las nuevas funciones.

* **He diseñado [un esquema JSON para crear un formulario adaptable](adaptive-form-json-schema-form-model.md). El esquema JSON define eventos para algunos componentes de los formularios adaptables. ¿AEM Forms as a Cloud Service admite eventos?**
Cree el formulario adaptable basado en el esquema JSON en el entorno de Experience Manager 6.5 Forms y utilice la [Utilidad de migración](migrate-to-forms-as-a-cloud-service.md) para migrar este tipo de formularios a AEM Forms as a Cloud Service. La utilidad convierte estos eventos en bibliotecas de cliente, y puede seguir utilizando formularios adaptables con eventos en un entorno de Cloud Service.

<!-- 

* **Is there any AEM Forms as a Cloud Service connector for Microsoft Power Automate?**

  Yes, Adobe provides an Adobe Experience Manager connector to access [Adobe Experience Manager Forms - Communication capabilities](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/using-communications/aem-forms-cloud-service-communications-introduction.html?lang=es) through Microsoft Power Automate. You can create a PDF document that is based on a form design and XML form data or create PostScript (PS), Printer Command Language (PCL), Zebra Printing Language (ZPL) and other Printer Definition Language documents. 

  You can get started with Adobe Experience Manager easily with just a few steps:

  1. Generate the Service credentials: Use Adobe Experience Manager Developer Console to [generate](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/service-credentials.html?lang=es&#generate-service-credentials) the service credentials.  
  
  1. Setup your connection: Add your service credentials to the Adobe Experience Manager Connector. You can get crdential from service credential JSON and copy these credential details to your one-time connection setup:

    * AEM Server
    * Organization ID 
    * Client ID
    * Client Secret
    * Technical Account ID
    * Meta Scopes
    * Private Key - base64 encoded keys are accepted
    * Adobe IMS Host URL

    <br> 
    
    ![Use your Service Credential JSON for credential details](assets/forms-aem-pa-connector-connection.png)

    A sample Service Credential JSON file fields mapped to Adobe Experience Manager connector for Microsoft Power Automate.

    -->
