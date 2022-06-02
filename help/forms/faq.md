---
title: 'Preguntas más frecuentes as a Cloud Service de Forms '
description: Preguntas más frecuentes as a Cloud Service de Forms
contentOwner: khsingh
exl-id: 0b14b680-7da5-4e0b-bd6a-c379d148f9d7
source-git-commit: a5cd8a49a74eb8372d1d363ff859e1aef921859b
workflow-type: tm+mt
source-wordcount: '993'
ht-degree: 2%

---

# Preguntas frecuentes {#frequently-asked-questions}

* **¿Puedo usar el Editor de código para crear reglas?**
Puede usar el Editor visual para crear las reglas. El Editor de código no está disponible en [!DNL Forms] as a Cloud Service. Si el formulario adaptable utiliza secuencias de comandos de reglas desarrolladas mediante el editor de código, utilice la variable [Utilidad de migración](migrate-to-forms-as-a-cloud-service.md) para convertir las secuencias de comandos de código en funciones personalizadas. Puede utilizar funciones personalizadas con el Editor visual para seguir obteniendo los resultados obtenidos con el Editor de código.

* **¿Puedo crear un formulario adaptable basado en XFA en instancias de Cloud Service?**
Sí, puede crear un formulario adaptable basado en XFA en una instancia de Cloud Service. Sin embargo, la compatibilidad con Forms adaptable basado en XFA no está disponible para el SDK as a Cloud Service de AEM Forms (entorno de desarrollo local). Si tiene intención de utilizar Forms adaptable basado en XFA con el SDK as a Cloud Service de AEM Forms, póngase en contacto con el servicio de asistencia al Adobe para obtener más información sobre su caso de uso y los requisitos específicos.

<!-- * **Can I use an XDP as a Document of Record (DoR) template? Is Forms Designer included in AEM Forms as a Cloud Service license?** 

  Yes, you can use an XDP as a Document of Record template on Cloud Service instances. However, support to use XDP as a Document of Record template is not available for AEM Forms as a Cloud Service SDK (Local development environment). -->

* **¿Puedo migrar contenido desde un local o [!DNL Adobe-Managed Services] entornos a [!DNL Forms] ¿Entorno as a Cloud Service?**
Sí, puede migrar su código, contenido y recursos personalizados desde On-Premise o [!DNL Adobe-Managed Services] entornos a [!DNL Forms] Entorno as a Cloud Service. Para obtener instrucciones detalladas, consulte [Migrar a Forms as a Cloud Service](migrate-to-forms-as-a-cloud-service.md).

<!-- You can use package manager or Experience Manager UI to [export and import Forms and related assets](import-export-forms-templates.md), use the migration utility to make your existing assets compatible with [!DNL Forms] as a Cloud Service, use the [Best Practices Analyzer](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/best-practices-analyzer/overview-best-practices-analyzer.html?lang=en#best-practices-analyzer) tool to find the features and APIs that require changes and updated before migration, and use the [Content Transfer Tools](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/moving/home.html) to move your custom code without refactoring it. -->

* **¿Dónde puedo obtener AEM [!DNL Forms] as a Cloud Service [!DNL Java™] documentación de referencia de API?**
Puede descargar la documentación de referencia de la API de Java™ desde [!DNL Maven Central Repository]. Para descargar:
   1. Ir a [[!DNL Maven Central Repository]](https://mvnrepository.com/artifact/com.adobe.aem/aem-forms-sdk-api).
   1. Busque y abra la página que contiene la última versión de [!DNL Experience Manager Forms] SDK.
   1. Haga clic en la opción Ver todo para ver todos los archivos.
   1. Descargue y extraiga el `aem-forms-sdk-api-<version>-javadocs`.jar.
   1. Abra el archivo index.html para ver la documentación de referencia de la API.

* **¿Dónde puedo conseguir? [!DNL JavaScript™] Referencia de API para Adaptive Forms?**
Puede descargar [!DNL JavaScript™] Documentación de referencia de API de[!DNL  Maven Central Repository]. Para descargar:
   1. Abra [[!DNL Maven Central Repository]](https://mvnrepository.com/artifact/com.adobe.aem/aem-forms-sdk-api).
   1. Busque y abra la página que contiene la última versión de [!DNL Experience Manager Forms] SDK.
   1. Haga clic en la opción Ver todo para ver todos los archivos.
   1. Descargue y extraiga el `aem-forms-sdk-api-<version>-jsdoc.jar`.
   1. Abra el archivo index.html para ver la documentación de referencia de la API.

* **¿Puedo seguir utilizando temas y plantillas existentes?**
Sí, puede seguir utilizando los temas creados con AEM 6.4 Forms y AEM 6.5 Forms después de usar la variable [Utilidad de migración](migrate-to-forms-as-a-cloud-service.md) para moverlos a [!DNL AEM Forms] as a Cloud Service.

   También puede crear un proyecto basado en [!DNL AEM Forms] as a Cloud Service [Tipo de archivo](setup-local-development-environment.md#forms-cloud-service-local-development-environment) y utilice plantillas y temas de muestra incluidos.

* **¿Puedo producir datos compatibles con esquemas?**
Sí, puede crear Adaptive Forms para producir datos compatibles con esquemas.

<!-- * **Can I pass custom parameters to the prefill service?**
Custom parameters are planned for an upcoming release. -->

* **¿Puedo almacenar en caché el contenido protegido?**
El almacenamiento en caché de las funciones de contenido seguro está deshabilitado de forma predeterminada. Para habilitar la función, puede realizar las instrucciones que se indican en [Almacenamiento en caché de contenido seguro](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/permissions-cache.html).

* **Tengo un formulario adaptable localizado; ¿no está procesando la versión localizada? ¿Cuál podría ser la causa y cómo resolverla?**

   La convención de URL de Forms adaptable localizado ahora admite la especificación de una configuración regional en la URL. La nueva convención de URL permite almacenar en caché formularios localizados en un Dispatcher o CDN. En el entorno de Cloud Service, utilice el formato de URL `http://host:port/content/forms/af/<afName>.<locale>.html` para solicitar una versión localizada de un formulario adaptable en lugar de `http://host:port/content/forms/af/afName.html?afAcceptLang=<locale>`. Adobe recomienda utilizar Dispatcher o el almacenamiento en caché de CDN. Ayuda a mejorar la velocidad de procesamiento de los formularios rellenados previamente.

* **He actualizado un formulario adaptable; ¿la versión actualizada no está disponible para que los clientes la utilicen?**
De forma predeterminada, CDN actualiza la caché cada 5 minutos, espera 5 minutos y, a continuación, busca la versión actualizada.

* **¿Puedo utilizar el paso Firma de un formulario adaptable para crear una experiencia de firma dentro del explorador?**
No, el paso Firma no está disponible para [!DNL Forms] as a Cloud Service. Elimine el paso Firma de su Forms adaptable. En lugar del paso Firma, permita a los usuarios firmar un formulario adaptable después del envío. Le ayuda a seguir proporcionando una experiencia de firma dentro del explorador.

* **¿Puedo utilizar el paso Verificar en un Formulario Adaptable?**
No, el paso Verificar no está disponible para [!DNL Forms] as a Cloud Service. Elimine el paso de verificación de la Forms adaptable existente antes de mover estos formularios a un entorno de Cloud Service.

* **¿Se pueden agregar gráficos a un formulario adaptable?**
Sí, puede agregar gráficos a Forms adaptable. Adaptive Forms proporciona un componente de gráfico. Puede utilizarla para agregar gráficos a un formulario adaptable.

* **¿Puedo conectar un Modelo de datos de formulario a un modelo de base de datos relacional?**
Puede conectar un modelo de datos de formulario a [!DNL RESTful web services], [!DNL SOAP-based web services], [!DNL OData services]y el perfil de usuario del Experience Manager como fuentes de datos. No está disponible la compatibilidad para conectar un Modelo de datos de formulario con una base de datos relacional.

* **¿Puedo utilizar certificados personalizados con el Modelo de datos de formulario para la autenticación?**
El Modelo de datos de formulario no proporciona un método para utilizar certificados personalizados para la autenticación. Por lo tanto, los certificados personalizados como x509 y SSL bidireccional no son compatibles.

* **¿Puedo utilizar la acción de envío del portal de Forms para Adaptive Forms?**

   Puede modificar el Forms adaptable existente para utilizarlo [Enviar al extremo REST](configuring-submit-actions.md#submit-to-rest-endpoint), [Enviar correo electrónico](configuring-submit-actions.md#send-email), [Enviar mediante el modelo de datos de formulario](configuring-submit-actions.md#submit-using-form-data-model)y [Invocar un flujo de trabajo AEM](configuring-submit-actions.md#invoke-an-aem-workflow) Enviar acciones. La acción de envío de Forms Portal y Forms Portal aún no está disponible. Consulte las notas de la versión mensuales para ver la disponibilidad de las funciones.

* **¿Puedo usar [!DNL AEM Forms] aplicación con [!DNL AEM Forms] ¿as a Cloud Service?**

   Los formularios adaptables ofrecen un diseño interactivo. Estos formularios cambian el aspecto, el diseño y la interactividad en función del dispositivo subyacente. Puede seguir utilizando Adaptive Forms en dispositivos móviles mientras consulta las notas de la versión mensuales sobre la disponibilidad de las funciones.

* **¿Qué funciones no forman parte de la versión inicial de GA?**
Portal de Forms, [!DNL AEM Forms] la aplicación, la integración con Adobe Analytics y la integración con Adobe Target no forman parte de la versión inicial de GA. Busque las notas de la versión mensuales para obtener información sobre las nuevas funciones.

* **He diseñado un [Esquema JSON para crear un formulario adaptable](adaptive-form-json-schema-form-model.md). El esquema JSON define eventos para algunos componentes de los formularios adaptables. ¿AEM Forms as a Cloud Service admite eventos?**
Cree el formulario adaptable basado en el esquema JSON en el entorno Forms de Experience Manager 6.5 y utilice el [Utilidad de migración](migrate-to-forms-as-a-cloud-service.md) para migrar este Forms adaptable a AEM Forms as a Cloud Service. La utilidad convierte estos eventos en bibliotecas de cliente y puede seguir utilizando Forms adaptable con eventos en un entorno de Cloud Service.

