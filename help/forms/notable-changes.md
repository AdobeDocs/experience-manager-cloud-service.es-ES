---
title: Diferencias entre AEM 6.5 Forms y AEM Cloud Services
description: ¿Es usuario de Experience Manager Forms y desea actualizar a Adobe Experience Manager Forms as a Cloud Service? Compare AEM 6.5 Forms y AEM Cloud Services y aprenda los cambios más importantes antes de actualizar o migrar a Cloud Service.
exl-id: 46fcc1b4-8fd5-40e1-b0fc-d2bc9df3802e
contentOwner: khsingh
source-git-commit: 54a1ae1cc030030e44612b502b70c9b567144538
workflow-type: tm+mt
source-wordcount: '1352'
ht-degree: 32%

---

# Cambios importantes para los usuarios de Adobe Experience Manager 6.5 Forms existentes  {#notable-changes-for-existing-AEM-Forms-users}

Adobe Experience Manager Forms as a Cloud Service incluye algunos cambios importantes en las funciones existentes en comparación con Adobe Experience Manager Forms local y los entornos de [!DNL Adobe-Managed Service]. A continuación se enumeran las principales diferencias:

## Funciones nativas de la nube

* El servicio cuenta con una arquitectura nativa de la nube que permite el escalado automático basado en la carga, cero tiempos de inactividad para actualizaciones, frecuentes y posteriores a la implementación de nuevas funciones y actualizaciones, y topologías optimizadas para lograr la máxima resiliencia y eficiencia.

* El servicio no incluye acciones de envío que almacenen datos en instancias de Cloud Service de Adobe Experience Manager, lo que lo hace muy seguro. Los datos capturados mediante formularios se envían directamente a almacenes de datos configurados.

* También se incluye una CDN (red de entrega de contenido) gratuita para ayudarle a enviar y procesar formularios a un ritmo más rápido.


## Actualizaciones en el flujo de desarrollo

* El servicio proporciona un SDK para desarrollar y probar código personalizado en un entorno local (equipo local) antes de implementar el código en un Cloud Service. Los desarrolladores desarrollan y prueban componentes personalizados, temas, flujos de trabajo, aplicaciones, configuraciones, plantillas y mucho más utilizando el SDK en sus equipos locales. Después de probar el código personalizado en su entorno de desarrollo local, implementa el código personalizado en un [Desarrollo del entorno de Forms CS o entorno de ensayo](/help/implementing/cloud-manager/deploy-code.md) para pruebas adicionales antes de promocionarla a un entorno de producción.

* Los desarrolladores mantienen el código para el Cloud Service y el entorno de desarrollo local en un entorno común [repositorio de Git](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/managing-code/cloud-manager-repositories.html). Un repositorio de Git, basado en AEM tipo de archivo, se crea automáticamente al crear un programa as a Cloud Service de AEM.

   ![](/help/forms/assets/git-repo-local-and-forms-cs.png)

* El flujo de desarrollo para Forms as a Cloud Service se alinea con AEM tipo de archivo para AEM Cloud Service. Con todo, se requieren algunos cambios en los proyectos de Adobe Experience Manager Maven para que sean compatibles con AEM Cloud Service. En un nivel superior, AEM requiere una separación de contenido y código en subpaquetes discretos para respetar la división entre contenido mutable e inmutable. Utilice la herramienta [](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/refactoring-tools/repo-modernizer.html?lang=es)Modernizador de repositorio para reestructurar los paquetes de proyectos existentes separando contenido y código en paquetes discretos para que sean compatibles con la estructura de proyectos definida para Adobe Experience Manager as a Cloud Service.

* Antes de utilizar los paquetes de clientes con Forms as a Cloud Service, vuelva a compilar el código personalizado con la última versión de adobe-aemfd-docmanager.

* Uso [Utilidad de migración as a Cloud Service de AEM Forms](/help/forms/migrate-to-forms-as-a-cloud-service.md) para preparar y migrar las configuraciones de Forms adaptable, temas, plantillas y nube desde <!-- AEM 6.3 Forms--> AEM 6.4 Forms en OSGi y AEM 6.5 Forms en OSGi a [!DNL AEM] as a Cloud Service. Uso [Repositorio de Git de su programa](/help/implementing/cloud-manager/managing-code/cloud-manager-repositories.md) para importar las plantillas de formulario adaptable existentes.

* De forma predeterminada, el correo electrónico solo admite protocolos HTTP y HTTP. [Póngase en contacto con el equipo de soporte](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/development-guidelines.html?lang=es#sending-email) para habilitar puertos para enviar correos electrónicos y para habilitar el protocolo SMTP para su entorno.

## Localización

* La convención de URL de los formularios adaptables localizados admite ahora la especificación de una configuración regional en la URL. La nueva convención de URL permite almacenar en caché formularios localizados en Dispatcher o CDN. En un entorno de Cloud Service, utilice el formato de URL `http://host:port/content/forms/af/<afName>.<locale>.html` para solicitar una versión localizada de un formulario adaptable en lugar de `http://host:port/content/forms/af/afName.html?afAcceptLang=<locale>`.

* Adobe recomienda utilizar el almacenamiento en caché de CDN o Dispatcher. Ayuda a mejorar la velocidad de procesamiento de los formularios rellenados previamente.


## Formularios adaptables

* **Editor de reglas:** AEM Forms as a Cloud Service proporciona un [Editor de reglas](rule-editor.md#visual-rule-editor) reforzado. El editor de código no está disponible en Forms as a Cloud Service.

   La variable [utilidad de migración](/help/forms/migrate-to-forms-as-a-cloud-service.md) le ayuda a migrar los formularios que tengan reglas personalizadas (creadas en el editor de código). La utilidad convierte estas reglas en funciones personalizadas compatibles con Forms as a Cloud Service. Puede utilizar las funciones reutilizables con el editor de reglas para seguir obteniendo resultados obtenidos con los scripts de reglas. La variable `onSubmitError` o `onSubmitSuccess` ahora están disponibles como acciones en el Editor de reglas.

* **Servicio de relleno previo:** de forma predeterminada, el servicio de relleno previo combina los datos con un formulario adaptable en el cliente en lugar de combinar los datos en el Servidor en AEM 6.5 Forms. La funcionalidad ayuda a mejorar el tiempo necesario para rellenar previamente un formulario adaptable. Siempre puede configurarlo para ejecutar la acción de combinación en el servidor de Adobe Experience Manager Forms.

* **Enviar acciones:** La variable **Correo electrónico** enviar acción proporciona opciones para enviar archivos adjuntos y adjuntar el documento de registro (DoR) con el correo electrónico. Puede usarlo en lugar del **Enviar correo electrónico como PDF** acción disponible en AEM 6.5 Forms.

* **Servicio de automated forms conversion**: El servicio no proporciona un metamodelo para el servicio de Automated forms conversion. Puede [descargarlo de la documentación del servicio de conversión de formularios automatizados](https://experienceleague.adobe.com/docs/aem-forms-automated-conversion-service/using/extending-the-default-meta-model.html?lang=es#default-meta-model).

* **Forms adaptable basado en XSD:** Puede utilizar la plantilla XDP para diseñar una plantilla para Document for Record. El servicio no admite formularios adaptables basados en XFA

* **Componentes**: Puede usar [Componentes principales adaptables de Forms](/help/forms/creating-adaptive-form-core-components.md) para diseñar los formularios. Estos componentes se basan en componentes principales de WCM, siguen los estándares de BEM y se pueden personalizar fácilmente. El servicio no admite la experiencia de firma en formularios y no incluye los componentes Resumen y Verificación del formulario adaptable

## Portal de Forms 

* Puede utilizar los componentes Search &amp; Lister, Drafts and Submission y Link de Forms Portal para enumerar los formularios para los usuarios que iniciaron sesión. La compatibilidad con el uso anónimo del Portal de formularios no está disponible de forma predeterminada (OOTB). Puede personalizar el Portal de formularios para habilitar la visualización de formularios para los usuarios que no hayan iniciado sesión.

* El servicio no conserva los metadatos para borradores y envía Adaptive Forms.

## Servicios de documentos:

Forms as a Cloud Service proporciona API RESTful de generación de documentos y manipulación de documentos. Puede utilizar estas API para generar o manipular documentos bajo demanda o en lotes, según sea necesario:

* **Servicios de documentos: API de generación de documentos (servicio de salida)**: En una sola llamada o lote de API, solo puede utilizar una plantilla con varios archivos XML de DATOS. No se admite el uso de varias plantillas con varios archivos de datos en una sola llamada de API.

* **API de manipulación de documentos (servicio Assembler)**:

   * Las operaciones que dependen de servicios de documentos o aplicaciones no están disponibles. Por ejemplo, Microsoft Word para PDF, Microsoft Excel para PDF y HTML para PDF, PostScript (PS) para PDF, XDP para PDF forms no son compatibles. Estas operaciones se basan en Microsoft Office, Adobe Acrobat, Distiller de Adobe y Forms Document Service respectivamente.

   * Convierta documentos en un formato que no sea de PDF en un formato de PDF antes de utilizar los que utilizan API de manipulación de documentos de comunicaciones. Por ejemplo, si los documentos están en formato de Microsoft Office, HTML, PostScript (PS) o XDP, conviértalos a formato PDF antes de utilizarlos con documentos de PDF. Puede usar la variable [ConvertPDF](https://experienceleague.adobe.com/docs/experience-manager-65/forms/use-document-services/using-convertpdf-service.html) para dichas conversiones.

* Puede utilizar un entorno de Forms AEM 6.5 para Firma digital, Cifrado, Extensión de Reader, Enviar a impresora, Convertir PDF y servicio de Forms de códigos de barras.


## Integración de datos (Modelo de datos de formulario)

* El servicio también ofrece compatibilidad con conector JDBC, Microsoft Dynamics, SalesForce, servicios web basados en SOAP y servicios compatibles con OData.

* También puede conectar AEM perfil de usuario para recuperar y actualizar la información de usuario.

* El modelo de datos de Forms solo admite extremos HTTP y HTTPS para enviar datos. El servicio no admite SSL mutuo para el conector REST y autenticación basada en certificados x509 para fuentes de datos SOAP.

* Forms as a Cloud Service permite utilizar Microsoft Azure Blob, Microsoft Sharepoint, Microsoft OneDrive y servicios compatibles con operaciones generales de CRUD (Crear, Leer, Actualizar y Eliminar) como almacenes de datos, ya que son compatibles las especificaciones de API abierta 2.0 y de API abierta 3.0.


## Firma electrónica

* El servicio proporciona una integración de OOTB con Adobe Sign y es compatible con ArchiveSign para firmas electrónicas.

* El servicio también admite funciones de Adobe Sign. Puede configurar las funciones en el editor de Forms adaptable para los usuarios empresariales a fin de configurar fácilmente los flujos de trabajo de firma.


## Formularios HTML5

* Puede utilizar un entorno de Forms AEM 6.5 para:

   * procese los formularios basados en XDP como Forms HTML5. El servicio no es compatible con formularios de HTML5 (Mobile Forms).

   * capturar datos sin conexión y sincronizarlos la próxima vez que vuelva a estar en línea con [AEM Forms Workspace](https://experienceleague.adobe.com/docs/experience-manager-65/forms/use-aem-forms-workspace/introduction-html-workspace.html?lang=es) aplicación.

## Comunicaciones interactivas

* Puede utilizar las API de comunicaciones para producir documentos personalizados bajo demanda o por lotes en Forms as a Cloud Service. Puede utilizar un entorno de Forms AEM 6.5 para comunicaciones interactivas y casos de uso de la interfaz de usuario del agente.


