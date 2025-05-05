---
title: ¿Cuáles son las diferencias entre AEM 6.5 Forms y AEM Cloud Services?
description: Compare AEM 6.5 Forms y AEM Cloud Services y aprenda los cambios más importantes antes de actualizar o migrar a Cloud Service.
exl-id: 46fcc1b4-8fd5-40e1-b0fc-d2bc9df3802e
role: Admin, Developer, User
feature: Adaptive Forms
contentOwner: khsingh
source-git-commit: a5179851af8ec88e23d79a74265b10cbce2d50f1
workflow-type: tm+mt
source-wordcount: '1325'
ht-degree: 100%

---

# Diferencia entre AEM 6.5 Forms (AMS y local) y AEM Forms as a Cloud Service (AEM CS Forms) {#notable-changes-for-existing-AEM-Forms-users}

Adobe Experience Manager Forms as a Cloud Service incluye algunos cambios importantes en las funciones existentes en comparación con Adobe Experience Manager Forms local y los entornos de [!DNL Adobe-Managed Service]. A continuación se enumeran las principales diferencias:

## Funciones nativas de la nube

* El servicio cuenta con una arquitectura nativa de la nube que permite el escalado automático en función de la carga, un tiempo de inactividad cero para las actualizaciones, el despliegue frecuente y posterior de nuevas funciones y actualizaciones y topologías optimizadas para lograr la máxima resistencia y eficiencia.

* El servicio no incluye acciones de envío que almacenen datos en instancias de Adobe Experience Manager Cloud Service, lo que lo hace muy seguro. Los datos capturados mediante formularios se envían directamente a almacenes de datos configurados.

* También se incluye una red de distribución de contenido (CDN) gratuita para ayudarle a enviar y procesar formularios a un ritmo más rápido.


## Actualizaciones en el flujo de desarrollo

* El servicio proporciona un SDK para desarrollar y probar código personalizado en un entorno local (equipo local) antes de implementar el código en un Cloud Service. Los desarrolladores elaboran y prueban componentes personalizados, temáticas, flujos de trabajo, aplicaciones, configuraciones, plantillas y mucho más utilizando el SDK en sus equipos locales. Después de probar el código personalizado en su entorno de desarrollo local, implementa el código personalizado en un [Entorno de desarrollo o de fase de Forms CS](/help/implementing/cloud-manager/deploy-code.md) para evaluarlo más antes de pasarlo a un entorno de producción.

* Los desarrolladores mantienen el código para el Cloud Service y el entorno de desarrollo local en un [repositorio de Git](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/managing-code/cloud-manager-repositories.html?lang=es) común. Un repositorio de Git, basado en el Arquetipo del proyecto de AEM, se genera automáticamente al crear un programa en AEM as a Cloud Service.

  ![creación automática de un repositorio de Git en el programa de AEM as a Cloud Service](/help/forms/assets/git-repo-local-and-forms-cs.png)

* El flujo de desarrollo para Forms as a Cloud Service se alinea con el Arquetipo del proyecto de AEM para AEM Cloud Service. Con todo, se requieren algunos cambios en los proyectos de Adobe Experience Manager Maven para que sean compatibles con AEM Cloud Service. En un nivel superior, AEM requiere una separación de contenido y código en subpaquetes discretos para respetar la división entre contenido mutable e inmutable. Utilice la herramienta [](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/refactoring-tools/repo-modernizer.html?lang=es)Modernizador de repositorio para reestructurar los paquetes de proyectos existentes separando contenido y código en paquetes discretos para que sean compatibles con la estructura de proyectos definida para Adobe Experience Manager as a Cloud Service.

* Antes de utilizar los paquetes de clientes con Forms as a Cloud Service, vuelva a compilar el código personalizado con la última versión de adobe-aemfd-docmanager.

* Use la [Utilidad de migración de AEM Forms as a Cloud Service](/help/forms/migrate-to-forms-as-a-cloud-service.md) para preparar y migrar las configuraciones de formularios adaptables, temáticas, plantillas y nube desde <!-- AEM 6.3 Forms--> AEM 6.4 Forms en OSGi y AEM 6.5 Forms en OSGi a [!DNL AEM] as a Cloud Service. Use el [repositorio de Git de su programa](/help/implementing/cloud-manager/managing-code/managing-repositories.md) para importar las plantillas de formulario adaptable existentes.

* De forma predeterminada, el correo electrónico solo admite los protocolos HTTP y HTTPs. [Póngase en contacto con el equipo de soporte](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/development-guidelines.html?lang=es#sending-email) para habilitar puertos para enviar correos electrónicos y para habilitar el protocolo SMTP para su entorno.

## Localización

* La convención de URL de los formularios adaptables localizados admite ahora la especificación de una configuración regional en la URL. La nueva convención de URL permite almacenar en caché formularios localizados en Dispatcher o CDN. En el entorno de Cloud Service, utilice el formato de URL `http://host:port/content/forms/af/<afName>.<locale>.html` para solicitar una versión localizada de un formulario adaptable en lugar de `http://host:port/content/forms/af/afName.html?afAcceptLang=<locale>`.

* Adobe recomienda utilizar el almacenamiento en caché de CDN o Dispatcher. Ayuda a mejorar la velocidad de procesamiento de los formularios rellenados previamente.


## Formularios adaptables

* **Editor de reglas:** AEM Forms as a Cloud Service proporciona un [Editor de reglas](rule-editor.md#visual-rule-editor) reforzado. El editor de código no está disponible en Forms as a Cloud Service.

  La [utilidad de migración](/help/forms/migrate-to-forms-as-a-cloud-service.md) le ayuda a migrar los formularios que tienen reglas personalizadas (creadas en el editor de código). La utilidad convierte estas reglas en funciones personalizadas compatibles con Forms as a Cloud Service. Puede emplear las funciones reutilizables con el Editor de reglas para seguir obteniendo resultados con secuencias de comandos de reglas. Las funciones `onSubmitError` o `onSubmitSuccess` están ahora disponibles como acciones en el Editor de reglas.

<!--* **Prefill Service:** By default, the prefill service merges data with an Adaptive Form at client as opposed to merging data on Server in AEM 6.5 Forms. The feature helps improve the time required to prefill an Adaptive Form. You can always configure to run the merge action on the Adobe Experience Manager Forms Server.-->

* **Servicio de relleno previo:** el servicio de relleno previo recupera datos del servidor y los combina para rellenar previamente el formulario adaptable en el lado del cliente. Esta funcionalidad ayuda a mejorar el tiempo necesario para rellenar un formulario adaptable. Siempre puede configurar el [servicio de relleno previo](https://experienceleague.adobe.com/docs/experience-manager-learn/forms/adaptive-forms/prefill-service-adaptive-forms-article-use.html?lang=es) para ejecutar la acción de combinación en el servidor de Adobe Experience Manager Forms.

* **Acciones de envío:** la acción de envío **Correo electrónico** proporciona opciones para enviar archivos adjuntos y adjuntar documentos de registro (DoR) mediante correo electrónico. Puede utilizarla en lugar de la acción **Enviar por correo electrónico como PDF** disponible en AEM Forms 6.5.

* **Servicio de conversión automatizada de formularios**: el servicio no proporciona un metamodelo para el servicio de conversión automatizada de formularios. Puede [descargarlo de la documentación del servicio de conversión de formularios automatizados](https://experienceleague.adobe.com/docs/aem-forms-automated-conversion-service/using/extending-the-default-meta-model.html?lang=es#default-meta-model).

* **Formularios adaptables basados en XSD:** puede utilizar una plantilla XDP para diseñar una plantilla para el documento de registro. El servicio no admite formularios adaptables basados en XFA

* **Componentes**: el servicio no admite la experiencia de firma en formularios y no incluye los componentes Resumen y Verificar para formularios adaptables.

* **Interfaz del asistente:** puede usar el complemento [Interfaz de asistente](/help/forms/creating-adaptive-form-core-components.md) para configurar rápidamente las opciones comunes y crear de manera fácil un formulario adaptable.

## Portal de Forms 

* El servicio no conserva metadatos para borradores y formularios adaptables enviados.

## Servicios de documentos:

Forms as a Cloud Service proporciona API RESTful de generación y manipulación de documentos. Puede utilizar estas API para generar o manipular documentos bajo demanda o en lotes, según sea necesario:

* **Servicios de documentos: API de generación de documentos (servicio de salida)**: en una sola llamada o lote de API, solo puede utilizar una plantilla con varios archivos XML de datos. No se admite el uso de varias plantillas con varios archivos de datos en una sola llamada de API.

* **API de manipulación de documentos (servicio del ensamblador)**:

   * Las operaciones que dependen de servicios de documentos o aplicaciones no están disponibles. Por ejemplo, Microsoft® Word a PDF, Microsoft® Excel a PDF y los formularios HTML a PDF, PostScript (PS) a PDF, XDP a PDF Forms no son compatibles. Estas operaciones dependen de Microsoft® Office, Adobe Acrobat, Adobe Distiller y Forms Document Service, respectivamente.

   * Convierta los documentos que estén en un formato que no sea PDF a un formato PDF antes de utilizarlos con las API de manipulación de documentos de comunicaciones. Por ejemplo, si los documentos están en formato de Microsoft® Office, HTML, PostScript (PS) o XDP, conviértalos a formato PDF antes de utilizarlos con documentos de PDF. Puede utilizar el servicio [ConvertPDF](https://experienceleague.adobe.com/docs/experience-manager-65/forms/use-document-services/using-convertpdf-service.html?lang=es) para dichas conversiones.

   * Puede utilizar un entorno Forms de AEM 6.5 para los servicios Firma digital, Cifrado, Extensión de Reader, Enviar a impresora, Convertir PDF y Forms de códigos de barras.


## Integración de datos (modelo de datos de formularios)

* El servicio también es compatible con conectores JDBC, Microsoft® Dynamics, SalesForce, servicios web basados en SOAP y servicios compatibles con OData.

* También puede conectar el perfil de usuario de AEM para recuperar y actualizar la información de usuario.

* El modelo de datos Forms solo admite puntos extremos HTTP y HTTPS para enviar datos. El servicio no admite SSL mutuo para el conector REST y autenticación basada en certificados x509 para fuentes de datos SOAP.

* Forms as a Cloud Service permite utilizar Microsoft® Azure Blob, Microsoft® SharePoint, Microsoft® OneDrive y servicios compatibles con las operaciones generales CRUD (Crear, Leer, Actualizar y Eliminar) como almacenes de datos, ya que se admiten tanto la especificación abierta OpenAPI 2.0 como la especificación abierta OpenAPI 3.0.


## Firma electrónica

* El servicio proporciona una integración de OOTB con Adobe Sign y es compatible con DocuSign para firmas electrónicas.

* El servicio también admite las funciones de Adobe Sign. Puede configurar las funciones en el editor de formularios adaptables para que los usuarios empresariales configuren fácilmente los flujos de trabajo de firma.


## Formularios HTML5

* Puede utilizar un entorno de formularios de AEM 6.5 para:

   * renderizar sus formularios basados en XDP como formularios HTML5. El servicio no es compatible con formularios de HTML5.

   * capturar datos sin conexión y sincronizarlos la próxima vez que vuelva a conectarse con la aplicación [AEM Forms Workspace](https://experienceleague.adobe.com/docs/experience-manager-65/forms/use-aem-forms-workspace/introduction-html-workspace.html?lang=es).

## Comunicaciones interactivas

* Puede utilizar las API de comunicaciones para elaborar documentos personalizados bajo demanda o por lotes en Forms as a Cloud Service. Puede utilizar un entorno de Forms de AEM 6.5 para comunicaciones interactivas y casos de uso de la interfaz de usuario del agente.

## Ver también

* [Migración desde AEM Forms (entornos On-Premise y AMS) a AEM Forms as a Cloud Service](/help/forms/migrate-to-forms-as-a-cloud-service.md)
* [Agregar o crear formularios adaptables en la página de AEM Sites](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md)
* [Creación de un formulario adaptable (componentes principales)](/help/forms/creating-adaptive-form-core-components.md)
* [Introducción a AEM Forms as a Cloud Service](/help/forms/home.md)
* [Configurar un entorno de desarrollo local y un proyecto de desarrollo inicial](/help/forms/setup-local-development-environment.md)


<!--

## Additional Information

* [Introduction to AEM Forms as a Cloud Service](/help/forms/home.md)
* [Set up a local development environment and initial development project](/help/forms/setup-local-development-environment.md)

-->
