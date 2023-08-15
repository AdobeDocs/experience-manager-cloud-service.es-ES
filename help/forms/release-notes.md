---
title: '“[!DNL AEM Forms] as a Cloud Service: notas de la versión”'
description: '“[!DNL AEM Forms] as a Cloud Service: notas de la versión”'
exl-id: 35950b81-6e45-4a75-bd27-8c28fd68e42e
source-git-commit: 5ad33f0173afd68d8868b088ff5e20fc9f58ad5a
workflow-type: tm+mt
source-wordcount: '2015'
ht-degree: 94%

---


# [!DNL Experience Manager Forms] nota de la versión as a Cloud Service {#overview}

Adobe Experience Manager [!DNL AEM Forms] as a Cloud Service recibe mejoras de forma continua. Para estar al día de los desarrollos más recientes, visite esta página regularmente. Esta página le proporciona información sobre:

- Nuevas funciones
- Mejoras
- Características previas al lanzamiento
- Características beta
- Corrección de errores
- Funcionalidad obsoleta
- Instrucciones especiales
- Planes de futuros cambios

>[!NOTE]
>
>Para ver las notas de la versión de todos los demás componentes de la versión de AEM as a Cloud Service, consulte [Notas de la versión actual](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/release-notes-current.html?lang=es).

## 2021.10.0 {#sep-2021-10-0}

### Novedades de [!DNL Forms] {#what-is-new-forms-oct-2021}

- **Analytics para formularios adaptables**: Ahora puede capturar y hacer un seguimiento del comportamiento del inicio de sesión y no inicio de sesión (Anónimo) mediante Adobe Analytics para formularios adaptables para recoger las opiniones de los usuarios finales. Ayuda a tomar decisiones informadas basadas en datos para mejorar la experiencia del usuario final.

### Nuevas funciones disponibles en el canal de prelanzamiento de [!DNL Forms] {#prerelease-features-forms-oct-2021}

- **Externalización de los datos de flujo de trabajo de AEM para un procesamiento seguro**: puede almacenar datos de flujos de trabajo AEM en el proceso (datos de variables de flujo de trabajo de AEM) que contengan elementos de datos personales sensibles (SPD) en un repositorio administrado por el cliente para un procesamiento seguro. Los elementos de datos y las variables de flujo de trabajo no se almacenan en el repositorio de AEM y se recuperan bajo demanda de un repositorio administrado por el cliente mientras se procesa el flujo de trabajo.

### Características beta de [!DNL Forms] {#sep-what-is-new-forms-oct-prerelease}

- **[!DNL AEM Forms as a Cloud Service - Communications]**: las [API de comunicación](aem-forms-cloud-service-communications.md) le ayudan a combinar una plantilla y los datos XML para generar documentos de impresión en distintos formatos. El servicio permite generar documentos en modos sincrónico y por lotes. Las API le permiten crear aplicaciones con las que puede hacer lo siguiente:

   - Generar documentos rellenando archivos de plantilla (PDF y XDP) con datos XML.
   - Generar formularios de salida en varios formatos, incluidas las secuencias de impresión de PDF no interactivas.

Puede escribir a [!DNL formscsbeta@adobe.com] para inscribirse en el programa beta.

## 2021.9.0 {#sep-2021-09-0}

### Novedades de [!DNL Forms] {#what-is-new-forms-sep-2021}

- **Utilizar funciones de Adobe Sign en un formulario adaptable**: Adobe Sign para el nivel de servicio empresarial tiene la opción de ampliar las funciones de los destinatarios del contrato, más allá del firmante, para que coincidan mejor con los requisitos del flujo de trabajo. Ahora puede [permitir que cada destinatario del acuerdo configure su función en un formulario adaptable](working-with-adobe-sign.md#addsignerstoanadaptiveform), siendo la de firmante la función predeterminada.

- **Analytics para formularios adaptables**: Ahora puede capturar y [hacer un seguimiento del comportamiento del usuario final mediante Adobe Analytics](integrate-aem-forms-with-adobe-analytics.md) para que el formulario adaptable recopile información del usuario final. Ayuda a tomar decisiones informadas basadas en datos para mejorar la experiencia del usuario final.

- **Conecte fácilmente AEM Forms con Microsoft Dynamics y Salesforce**: El servicio proporciona una configuración de origen de datos y modelos de datos predeterminados para Microsoft Dynamics y Salesforce, lo que lo hace [más rápido y fácil para los desarrolladores configurar Microsoft Dynamics y Salesforce como fuentes de datos para un formulario adaptable](configure-msdynamics-salesforce.md).

- **Firme electrónicamente un formulario adaptable mediante el uso de DocuSign:** [Puede utilizar DocuSign para firmar electrónicamente un formulario adaptable](integrate-docusign-adaptive-forms.md). El servicio proporciona una acción de envío personalizada para utilizar DocuSign con un formulario adaptable.

### Características beta de [!DNL Forms] {#sep-what-is-new-forms-prerelease}

- **Conector de almacenamiento unificado:** Utilice el conector de almacenamiento unificado para externalizar los datos en proceso en repositorios que administre el cliente. Por ejemplo, puede almacenar datos de los flujos de trabajo de AEM en proceso (datos de variables del flujo de trabajo de AEM) que contengan datos personales confidenciales (SPD) en un repositorio que administra el cliente.
  <!--* Enable Forms Portal’s save and resume functionality and store adaptive forms drafts in a customer-managed data repository.-->

- **[!DNL AEM Forms as a Cloud Service - Communications]**: las [API de comunicación](aem-forms-cloud-service-communications.md) le ayudan a combinar plantillas XDP y datos XML para generar documentos imprimibles en varios formatos. El servicio permite generar documentos en modo sincrónico. Las API le permiten crear aplicaciones con las que puede hacer lo siguiente:
   - Generar documentos rellenando archivos de plantilla con datos XML.
   - Generar formularios de salida en varios formatos, incluidas las secuencias de impresión de PDF no interactivas.
   - Genere archivos de PDF imprimibles desde un PDF de formularios XFA y un formulario de Adobe Acrobat.

Puede escribir a [!DNL formscsbeta@adobe.com] para inscribirse en el programa beta.

### Restricciones {#limitations}

- Adobe Analytics solo puede rastrear métricas de formularios para usuarios autenticados.

<!--

### New features available in [!DNL Forms] prerelease channel {#prerelease-features-forms-sep-2021}

* **Forms Portal:**  In a typical forms-centric portal deployment scenario, forms development and portal development are two disjoint activities. While Form Designers design and store forms in a repository, Web Developers create a web application to list forms and handle submission of forms. Forms are copied over to the web tier as there is no communication between the forms repository and the web application.

  Such scenarios often result in management issues and production delays. For example, if there is a newer version of a form available in the repository, you need to replace the form on the web tier, modify the web application, and redeploy the form on the public site. Redeploying the web application might cause some server downtime. Typically, the server downtime is a planned activity and therefore the changes cannot be pushed to the public site instantaneously.

  AEM Forms provides portal components that reduce management overheads and production delays. The components equip Web Developers to create and customize a forms portal on websites authored using Adobe Experience Manager (AEM). The form portal components allow you to add the following functionality:

  * List forms in customized layouts. Out of the box, List view and Card view are provided.

  * List published adaptive forms on an AEM Sites page.

  * Enable searching of forms based on a various criteria, such as form properties, metadata, and tags.

  * Lists drafts and submissions related to Adaptive Form created by end user.

  -->

## 2021.8.0 {#aug-2021-08-0}

### Novedades de [!DNL Forms] {#what-is-new-forms-aug-2021}

<!-- * Automated Forms Conversion service can [convert PDF Forms in Italian and Portuguese language](https://experienceleague.adobe.com/docs/aem-forms-automated-conversion-service/using/extending-the-default-meta-model.html?#language-specific-meta-model) to Adaptive Forms. -->

- El proyecto AEM Archetype para Forms as a Cloud Service ahora incluye [modelos de datos de formulario para Microsoft Dynamics y Salesforce](setup-local-development-environment.md).

- **Documento de registro basado en Acrobat**: Compatibilidad de AEM Forms as a Cloud Service con [formularios PDF de Adobe Acrobat (PDF de Acrobat)](generate-document-of-record-for-non-xfa-based-adaptive-forms.md) como plantilla para documentos de registro además de la plantilla de formulario basada en XFA.

- **Conector del almacén de datos de Microsoft Azure**: Ahora puede [conectar el modelo de datos de formulario al almacenamiento de Microsoft Azure](configure-azure-storage.md). Permite recuperar y almacenar datos de formulario adaptables en el almacenamiento de Microsoft Azure como BLOB.

### Característica beta de [!DNL Forms] {#aug-what-is-new-forms-prerelease}

- **Conector de almacenamiento unificado:** Utilice el conector de almacenamiento unificado para externalizar los datos en proceso en repositorios que administre el cliente. Por ejemplo, puede

   - Habilitar la funcionalidad de guardar y reanudar el portal de Forms y almacenar borradores de formularios adaptables en un repositorio de datos que administre el cliente.
   - Almacenar datos de los flujos de trabajo de AEM en proceso (datos de variables de flujo de trabajo de AEM) que contengan datos personales confidenciales (SPD) en un repositorio que administre el cliente.

- **[!DNL AEM Forms as a Cloud Service - Communications]**: las [API de comunicación](aem-forms-cloud-service-communications.md) le ayudan a combinar plantillas XDP y datos XML para generar documentos imprimibles en varios formatos. El servicio permite generar documentos en modo sincrónico. Las API le permiten crear aplicaciones con las que puede hacer lo siguiente:
   - Generar documentos rellenando archivos de plantilla con datos XML.
   - Generar formularios de salida en varios formatos, incluidas las secuencias de impresión de PDF no interactivas.
   - Genere archivos de PDF imprimibles desde un PDF de formularios XFA y un formulario de Adobe Acrobat.

Puede escribir a [!DNL formscsbeta@adobe.com] para inscribirse en el programa beta.

### Nuevas funciones disponibles en el canal de prelanzamiento de [!DNL Forms] {#prerelease-features-forms-aug-2021}

- **Utilizar funciones de Adobe Sign en un formulario adaptable**: Adobe Sign para el nivel de servicio empresarial tiene la opción de ampliar las funciones de los destinatarios del contrato, más allá del firmante, para que coincidan mejor con los requisitos del flujo de trabajo. Ahora puede [permitir que cada destinatario del acuerdo configure su función en un formulario adaptable](working-with-adobe-sign.md#addsignerstoanadaptiveform), siendo la de firmante la función predeterminada.

- **Analytics para formularios adaptables**: Ahora puede capturar y hacer un seguimiento del comportamiento del usuario final mediante Adobe Analytics para que el formulario adaptable recopile información del usuario final. Ayuda a tomar decisiones informadas basadas en datos para mejorar la experiencia del usuario final.

- **Conecte fácilmente AEM Forms con Microsoft Dynamics y Salesforce**: El servicio proporciona una configuración de origen de datos y modelos de datos predeterminados para Microsoft Dynamics y Salesforce, lo que lo hace [más rápido y fácil para los desarrolladores configurar Microsoft Dynamics y Salesforce como fuentes de datos para un formulario adaptable](configure-msdynamics-salesforce.md).

## 2021.7.0 {#july-2021-07-0}

### Novedades de [!DNL Forms] {#july-what-is-new-forms}

- Ahora puede utilizar el servicio Automated Forms Conversion para [convertir formularios PDF en francés, alemán y español](https://experienceleague.adobe.com/docs/aem-forms-automated-conversion-service/using/extending-the-default-meta-model.html?lang=es#language-specific-meta-model) a formularios adaptables.
- Se ha agregado un panel independiente al editor de plantillas para mostrar los errores relacionados con los componentes de los formularios adaptables. Ayuda a consolidar todos los errores de formularios adaptables en una ubicación y a reducir el tiempo de resolución.

### Nuevas funciones disponibles en el canal de prelanzamiento de [!DNL Forms] {#july-prerelease-features-forms}

- **Documento de registro basado en Acrobat**: También puede [usar el formulario PDF de Adobe Acrobat (PDF de Acrobat)](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/create-an-adaptive-form/generate-document-of-record-for-non-xfa-based-adaptive-forms.html?lang=es) como plantilla para el documento de registro además de la plantilla de formulario basada en XFA.

- **Conector del almacén de datos de Microsoft Azure**: Ahora puede [conectar el modelo de datos de formulario al almacenamiento de Microsoft Azure](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/use-form-data-model/configure-azure-storage.html?lang=es). Permite recuperar y almacenar datos de formulario adaptables en el almacenamiento de Microsoft Azure como BLOB.

- **Externalizador de datos de las variables**: Puede guardar datos de las variables del flujo de trabajo de AEM en un sistema de almacenamiento externo que administre su organización.

### Característica beta de [!DNL Forms] {#july-what-is-new-forms-prerelease}

- **[!DNL AEM Forms as a Cloud Service - Communications]**: las [API de comunicación](aem-forms-cloud-service-communications.md) le ayudan a combinar plantillas XDP y datos XML para generar documentos imprimibles en varios formatos. El servicio permite generar documentos en modo sincrónico. Las API le permiten crear aplicaciones con las que puede hacer lo siguiente:
   - Generar documentos rellenando archivos de plantilla con datos XML.
   - Generar formularios de salida en varios formatos, incluidas las secuencias de impresión de PDF no interactivas.
   - Genere archivos de PDF imprimibles desde un PDF de formularios XFA y un formulario de Adobe Acrobat.

## 2021.6.0 {#july-2021-06-0}

### Novedades de [!DNL Forms] {#june-what-is-new-forms}

- Se ha agregado la capacidad de filtrar columnas personalizadas en la bandeja de entrada AEM.
- Se ha agregado la capacidad de utilizar el editor de temáticas y la capa de estilo del editor de formularios adaptables para aplicar estilo al componente captcha.
- Se ha mejorado la velocidad y la precisión para detectar automáticamente secciones lógicas en los PDF forms de origen y convertirlas en los paneles de formularios adaptables correspondientes.
- Se ha agregado la acción de mover un PDF o archivo XDP de una carpeta a otra.

### Característica beta de [!DNL Forms] {#june-what-is-new-forms-prerelease}

- **[!DNL AEM Forms as a Cloud Service - Communications]**: las API de comunicación le ayudan a combinar plantillas XDP y datos XML para generar documentos imprimibles en varios formatos. El servicio permite generar documentos en modo sincrónico. Las API le permiten crear aplicaciones con las que puede hacer lo siguiente:

   - Generar formularios finales al rellenar archivos de plantilla con datos XML.
   - Generar formularios de salida en varios formatos, incluidas las secuencias de impresión de PDF no interactivas.
   - Generar PDF imprimibles desde un formulario PDF de XFA y un formulario de Adobe Acrobat (AcroForm).

- **Externalizador de datos de las variables**: Puede guardar datos de las variables del flujo de trabajo de AEM en un sistema de almacenamiento externo que administre su organización.

Puede escribir a [!DNL formscsbeta@adobe.com] para inscribirse en el programa beta.

### Errores corregidos en [!DNL Forms] {#june-forms-bugs-fixed}

- Cuando se valida un campo antes de enviar datos al servicio back-end mediante el modelo de datos de formulario (FDM), las validaciones se realizan correctamente, pero el servicio del modelo de datos de formulario no invoca la validación posterior.
- Cuando envía un formulario que contiene un campo de carga de HTML estándar desde un dispositivo iOS de Apple, a veces, el contenido del archivo no se envía y se recibe un archivo de 0 bytes en el otro extremo. Apple iOS 15.1 proporciona una solución para el problema.

## 2021.5.0 {#may-2021-05-0}

## [!DNL Adobe Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### Novedades de [!DNL Forms] {#may-what-is-new-forms}

- **Ayuda contextual**: Se ha agregado ayuda contextual para el editor de formularios adaptables, el editor de plantillas y el editor de temáticas para ayudar a los autores a comprender mejor las distintas características de los editores.
- **Mensajes de error en el explorador de propiedades**: Se han agregado mensajes de error para cada propiedad en el explorador de propiedades de formularios adaptables adaptable. Estos mensajes ayudan a comprender los valores permitidos para un campo.

### Próxima característica beta de [!DNL Forms] {#may-what-is-new-forms-prerelease}

Output as a Cloud service: El servicio de salida le ayuda a combinar plantillas XDP y datos XML para generar documentos imprimibles en varios formatos. El servicio permite generar documentos en modo por lotes sincrónico y asincrónico. El servicio Output le permite crear aplicaciones con las que puede hacer lo siguiente:

- Generar formularios finales al rellenar archivos de plantilla con datos XML.
- Generar formularios de salida en varios formatos, incluidas las secuencias de impresión de PDF no interactivas.
- Generar PDF de impresión a partir de PDF de formularios XFA.

Puede escribir a formscsbeta@adobe.com para inscribirse en el programa beta.

### Errores corregidos en [!DNL Forms] {#may-forms-bugs-fixed}

- En el paso Asignar tarea de Workflows de AEM Forms, cuando se sustituye el icono predeterminado de los botones de acción por un icono de coral, el flujo de trabajo deja de funcionar y registra una excepción. El flujo de trabajo funciona como se espera cuando se utilizan iconos predeterminados.
- En la capa de diseño, cuando cambia el número de columnas, abre la capa de edición y arrastra algunos componentes en un panel, los cuadros azules aparecen en el área de contenido del editor de formularios adaptables y el editor no responde.
- El mensaje de error de una opción del editor de reglas relacionada con el suministro de la URL de un activo adaptable o externo es demasiado largo y no es fácil de usar.

## 2021.4.0 {#april-2021-04-0}

### Novedades de [!DNL Forms] {#april-what-is-new-forms}

- **Utilizar el método de autenticación de Id. de gobierno en los formularios adaptables habilitados para Adobe Sign**

  Con la tecnología de algoritmos avanzados de aprendizaje automático, el proceso de Id. de gobierno de Adobe Sign ofrece a las empresas de todo el mundo la capacidad de garantizar una autenticación de alta calidad de la identidad de sus destinatarios. Ahora puede utilizar el método de autenticación de identidad de Id. de gobierno en los formularios adaptativos habilitados para Adobe Sign.

  La Id. de gobierno es un método de autenticación de identidad premium que indica al destinatario cómo [cargar la imagen de un documento de identidad emitido por el gobierno (licencia de conducir, identificación nacional, pasaporte)](https://helpx.adobe.com/in/sign/using/adobesign-authentication-government-id.html) y luego evalúa ese documento para asegurarse de que es auténtico.

- **Compatibilidad para utilizar la experiencia de firma en formularios para envíos asincrónicos de formularios adaptables**

  Ahora puede utilizar la experiencia de firma en formularios para los envíos asincrónicos de formularios adaptables. También puede incrustar un formulario adaptable en una página [!DNL Experience Manager Sites] y utilizar la experiencia de firma en formularios para los envíos de formularios adaptables.

- **Compatibilidad para utilizar una variable para especificar un archivo adjunto mientras se rellena previamente un formulario adaptable para un paso Asignar tarea**

  Al rellenar previamente un formulario adaptable para un paso Asignar tarea, ahora puede utilizar una variable del tipo de documento para seleccionar un archivo adjunto de entrada para el formulario adaptable.

- **Compatibilidad con el uso de la opción literal para establecer el valor de una variable de tipo JSON**

  Puede utilizar la opción literal para establecer el valor de una variable del tipo JSON en el paso establecer variable de un flujo de trabajo de AEM. La opción literal le permite especificar un JSON en forma de cadena.

- **Utilizar el entorno de desarrollo local para crear el documento de registro (DoR)**

  Puede utilizar un XDP como plantilla del documento de registro en instancias de Cloud Service y el SDK (entorno de desarrollo local) de AEM Forms as a Cloud Service. Anteriormente, la compatibilidad se limitaba únicamente a instancias de Cloud Service.

### Correcciones de errores en [!DNL Forms] {#april-bug-fixes-forms}

- Cuando se envía un formulario adaptable configurado para no generar un documento de registro a un flujo de trabajo de AEM configurado para generar un documento de registro, no se muestra ningún mensaje de error y la tarea no se envía.
