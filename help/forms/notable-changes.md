---
title: Cambios entre AEM 6.5 Forms y AEM Cloud Services
description: '¿Es usuario de Experience Manager Forms y desea actualizar a Adobe Experience Manager Forms as a Cloud Service? Conozca los cambios más importantes antes de actualizar o migrar a Cloud Service.  '
contentOwner: khsingh
exl-id: 46fcc1b4-8fd5-40e1-b0fc-d2bc9df3802e
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '1214'
ht-degree: 3%

---

# Cambios importantes para los usuarios de Adobe Experience Manager Forms existentes  {#notable-changes-for-existing-AEM-Forms-users}

Adobe Experience Manager Forms as a Cloud Service ofrece algunos cambios importantes en las funciones existentes en comparación con Adobe Experience Manager FormsOn-Premise y [!DNL Adobe-Managed Service] entornos. A continuación se enumeran las principales diferencias:

* El servicio proporciona un entorno de desarrollo local y nativo de la nube. Puede usar un [entorno de desarrollo local](setup-local-development-environment.md) para desarrollar y probar su código personalizado, componentes, plantillas, temas, Forms adaptable y otros recursos antes de implementar estos recursos en un entorno de nube. Ayuda a acelerar el proceso de desarrollo.
* [!DNL AEM] as Cloud Service se envía con una CDN integrada. Su objetivo principal es reducir la latencia mediante la entrega de contenido procesable desde los nodos de CDN en el extremo, cerca del explorador. Está completamente administrado y configurado para un rendimiento óptimo de las aplicaciones AEM.
* Un entorno nativo de la nube no tiene consola web (administrador de configuración). Puede usar [[!DNL AEM Forms] SDK as a Cloud Service para generar configuraciones](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/configuring-osgi.html?lang=en#generating-osgi-configurations-using-the-aem-sdk-quickstart) y canalización de CI/CD a [implementar la configuración](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/deploy-code.html?lang=en#deployment-process) a su instancia de Cloud Service.

* La convención de URL de Forms adaptable localizado ahora admite la especificación de una configuración regional en la URL. La nueva convención de URL permite almacenar en caché formularios localizados en un Dispatcher o CDN. En el entorno de Cloud Service, utilice el formato de URL `http://host:port/content/forms/af/<afName>.<locale>.html` para solicitar una versión localizada de un formulario adaptable en lugar de `http://host:port/content/forms/af/afName.html?afAcceptLang=<locale>`. Adobe recomienda utilizar Dispatcher o el almacenamiento en caché de CDN. Ayuda a mejorar la velocidad de procesamiento de los formularios rellenados previamente.
* El servicio de relleno previo combina datos con un formulario adaptable en un cliente. Ayuda a mejorar el tiempo necesario para rellenar previamente un formulario adaptable. Siempre puede configurar para ejecutar la acción de combinación en Adobe Experience Manager FormsServer.
* De forma predeterminada, los protocolos HTTP y HTTP solo son compatibles con el correo electrónico. [Póngase en contacto con el equipo de asistencia](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/development-guidelines.html#sending-email) para habilitar puertos para enviar correos electrónicos y para habilitar el protocolo SMTP para su entorno.
* Adobe Experience Manager Forms as a Cloud Service ofrece muchas nuevas funciones y posibilidades en sus proyectos AEM. Sin embargo, se requieren algunos cambios en los proyectos de Adobe Experience Manager Maven para que sean compatibles con AEM Cloud Service. En un nivel superior, AEM requiere una separación de contenido y código en subpaquetes discretos para respetar la división entre contenido mutable e inmutable. Utilice la variable [Modernizador de repositorio](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/refactoring-tools/repo-modernizer.html) herramienta para reestructurar los paquetes de proyectos existentes separando contenido y código en paquetes discretos para que sean compatibles con la estructura de proyectos definida para Adobe Experience Manager as a Cloud Service.

<!--  If your Cloud Configuration contains a secret (password), create a separate Cloud Configuration for every Author instance (Developer, Stage, and Production). If a Cloud Configuration is also required on Publish instances, publish/replicate a separate Cloud Configuration for every Publish instance (Developer, Stage, and Production). 

* When you create a Cloud Configuration that contains a secret, each Cloud Service instance (Developer, Stage, and Production) uses its own encryption key to encrypt the password before storing it. So, manually create such Cloud Configuration for every Cloud Service instance (Developer, Stage, and Production). Also, do not store secrets used in a Cloud Configuration to your Cloud Manager Git repository.

* Use [!DNL Cloud Manager] [APIs to convert and provide your passwords as secrets](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/configuring-osgi.html?lang=en#setting-values-via-api). Do not store plain text password or secrets on your environments. -->

* Uso de configuraciones específicas del entorno para valores de configuración OSGi secretos, como contraseñas, claves API privadas o cualquier otro valor. No se pueden almacenar en en Git por motivos de seguridad. [Utilice configuraciones específicas del entorno secreto para almacenar el valor de los secretos en todos los entornos de Adobe Experience Manager as a Cloud Service, incluidos Stage y Production](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/configuring-osgi.html?lang=en#when-to-use-secret-environment-specific-configuration-values).

Para obtener una lista completa de los cambios en Adobe Experience Manager as a Cloud Service, consulte [Novedades y diferencias](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/overview/what-is-new-and-different.html).

<!-- ## Feature comparison {#comparison}

[!DNL AEM Forms] as a Cloud Service and Experience Manager 6.5 Forms share a common set of features: Adaptive Forms, data integration, integration with [!DNL Adobe Sign], themes, templates, and forms management interface are identical. You can easily port your existing Adaptive Forms from an Experience Manager 6.5 Forms or an earlier version to [!DNL AEM Forms] as a Cloud Service.

### Features of AEM 6.5 Forms and [!DNL AEM Forms] as a Cloud Service {#feature-comparison}

The following table lists the major features of Experience Manager 6.5 Forms and provides information about whether the feature is partially or fully supported in [!DNL AEM Forms] as a Cloud Service, with a link to more information about the feature. The table also lists extra features available in [!DNL AEM Forms] as a Cloud Service.


| Feature/Capability | AEM 6.5 Forms | [!DNL AEM Forms] as a Cloud Service |
| - | - | - |
| Adaptive Forms | &#x2611; | &#x2611; |
| Data Integration | &#x2611; | &#x2611;(With some changes) |
| Automated Forms Conversion Service | &#x2611; | &#x2611; |
| Integration with Adobe Sign | &#x2611; | &#x2611;(With some changes) |
| Themes and Templates | &#x2611; | &#x2611; ([With some changes](themes.md#difference-in-themes))|
| Rule editor | &#x2611; | &#x2611; (With some changes) |
| Forms Portal | &#x2611; | --- |
| Integration with Adobe Analytics | &#x2611; | &#x2612; |
| Document Security | &#x2611; | &#x2612; | -->

<!-- ## New features {#comparison} -->



## Mejoras clave {#whats-new}

<!-- [!DNL AEM Forms] as a Cloud Service offers benefits like auto-scaling, cost-effectiveness, zero downtime for upgrades, and cloud-native development environment and more. The list does not stop here. The following features are are start and are available only for [!DNL AEM Forms] as a Cloud Service: -->

Las siguientes funciones y mejoras solo están disponibles en [!DNL AEM Forms] as a Cloud Service:

**Editor de reglas visuales mejorado**
El servicio proporciona un [Editor de reglas visuales](rule-editor.md#visual-rule-editor). El servicio ha agregado las siguientes características al editor de reglas de Visual para ayudarle a escribir reglas capaces:

* [Nuevos eventos de envío](working-with-adobe-sign.md#available-operator-types-and-events-in-rule-editor): `Navigation`, `Step Completion`, `Successful Submission`y `Error`

* [Nuevo tipo de datos `scope`](rule-editor.md#custom-functions). Puede usar la variable `scope` tipo de datos en una función personalizada para pasar todo el ámbito de un formulario.

* Capacidad de uso [@this para especificar un JSDoc en una función personalizada](rule-editor.md#custom-functions). Permite invocar una función personalizada utilizando @this en un componente activo.

* Posibilidad de agregar condiciones para reglas basadas en propiedades.

**Componentes principales**
La variable [Componentes principales](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=es) son un conjunto de componentes estandarizados de Administración de contenido web (WCM) para AEM acelerar el tiempo de desarrollo y reducir los costes de mantenimiento. [!DNL AEM Forms] Compatibilidad as a Cloud Service **[!UICONTROL Contenedor de AEM Forms]** Componente principal. Puede utilizar el componente para incrustar un formulario adaptable en una página de AEM Sites.

**Tipo de archivo AEM para Forms as a Cloud Service**
[Tipo de archivo AEM](https://github.com/adobe/aem-project-archetype/releases/tag/aem-project-archetype-27) ayuda a empezar a desarrollarse para [!DNL AEM Forms] as a Cloud Service. Puede utilizar Tipo de archivo versión 27 o posterior para crear una plantilla de proyecto compatible con [!DNL AEM Forms] Entorno as a Cloud Service. El tipo de archivo también incluye algunos temas de muestra y plantillas para ayudarle a empezar rápidamente.

**Flujo de información seguro y mejorado entre formularios y Sign**
[Integración adaptable de Forms y Adobe Sign](working-with-adobe-sign.md) en el Cloud Service ofrece el envío simultáneo de datos y la actividad de firma. Hace que el envío de formularios sea independiente del estado de firma, lo que allana el camino para envíos más rápidos. Además, el servicio no guarda datos en instancias de Cloud Service, por lo que el proceso de firma es muy seguro.

**Herramientas de migración y Analizador de recomendaciones**
El Analizador de prácticas recomendadas proporciona una evaluación de la implementación de AEM actual. Ejecute la herramienta antes de [migración a Forms as a Cloud Service](migrate-to-forms-as-a-cloud-service.md). Se evalúa la preparación para pasar de una implementación de Adobe Experience Manager (AEM) existente a AEM as a Cloud Service.

El servicio también ofrece un [experiencia de migración mejorada](migrate-to-forms-as-a-cloud-service.md) para ayudarle a migrar fácilmente de [!DNL AEM 6.4 Forms] y [!DNL AEM 6.5 Forms] a [!DNL AEM Forms] as a Cloud Service.

**Representaciones de formularios más rápidas y validaciones más rápidas del lado del servidor**
El servicio utiliza el almacenamiento en caché de CDN y Dispatcher para ofrecer representaciones y validaciones del lado del servidor más rápidas para Forms adaptable.

**CAPTCHA mejorado**
Ahora puede [validar CAPTCHA](captcha-adaptive-forms.md) en el envío del formulario adaptable o en una lógica empresarial. También puede agregar condiciones para validar CAPTCHA en una acción del usuario y mostrar u ocultar el componente CAPTCHA en un formulario adaptable basado en reglas.

El componente CAPTCHA proporciona una integración predeterminada con Google reCAPTCHA. También puede configurar más servicios CAPTCHA para el componente, si es necesario.

**Varias páginas de formato para el documento de registro**
Ahora puede utilizar una página de formato diferente para cada página de un documento de registro y controlar la colocación de un panel de formulario adaptable en un documento de registro con opciones de paginación.

**Añadir columnas a tablas sin encabezado**
Puede agregar y eliminar columnas a tablas sin encabezados. Los encabezados ocultos se añaden a estas tablas para ayudarle a agregar y eliminar columnas. Estos encabezados son visibles durante la creación, pero permanecen ocultos en el formulario publicado. Las tablas sin encabezados se encuentran principalmente en el Forms adaptable creado mediante el servicio de Automated forms conversion.

**Acciones de envío mejoradas**
Puede usar la variable [Enviar correo electrónico](configuring-submit-actions.md#send-email#send-email) Enviar acción para enviar un PDF de documento de registro (DoR) como archivo adjunto.

**Agrupar correo electrónico para flujo de trabajo**
Puede elegir [enviar correos electrónicos de notificación](aem-forms-workflow-step-reference.md#assign-task-step) desde el paso Asignar tarea a una sola persona o grupo.

**Paso del modelo de datos de formulario invocado mejorado**
Ahora puede especificar la ruta de la carpeta para la opción Relative to Payload de los argumentos de servicio de entrada en un paso Invocar modelo de datos de formulario . Le ayuda a asignar un archivo presente en la carpeta especificada al argumento de servicio sin especificar el nombre de archivo exacto.

**Legibilidad mejorada de los archivos de traducción**
En Forms as a Cloud Service, el orden de lectura de los campos y paneles de un formulario adaptable y las claves de mensaje de los archivos de traducción correspondientes (archivos .XLIFF) tiene una estructura similar. Ayuda a mejorar las velocidades de traducción manual.

<!-- ## Feature comparison {#feature-comparison}

[!DNL AEM Forms] as a Cloud Service and [!DNL AEM 6.5 Forms] share some features like Adaptive Forms, Data Integration, and Forms Portal. You can easily port your existing Adaptive Forms from an [!DNL AEM 6.5 Forms] or an earlier version to [!DNL AEM Forms] as a Cloud Service.

### Features of [!DNL AEM 6.5 Forms] and [!DNL AEM Forms] as a Cloud Service {#aem-6.5-vs-aem-forms-as-a-cloud-service}

The following table lists the major features of [!DNL AEM 6.5 Forms] and provides information about the features coming soon to [!DNL AEM Forms] as a Cloud Service:

| Feature/Capability | AEM 6.5 Forms  | [!DNL AEM Forms] as a Cloud Service |
|---|---|---|
| Cloud-native architecture | &#x2612; | &#x2611;  |
| Auto-scaling based on load | &#x2612; | &#x2611;  |
| Zero downtime for upgrades | &#x2612; | &#x2611;  |
| Feature roll-out frequency | Quarterly | Agile*  |
| CDN (content delivery network) included | &#x2612; | &#x2611;  |
| Topologies optimized for maximum resilience and efficiency | &#x2612; | &#x2611;  |
| Cloud-native development environment | &#x2612; | &#x2611;  |
| Self-Service via Cloud Manager | &#x2612; | &#x2611;  |
| Automated upgrades with Continuous Integration and Continuous Delivery (CI/CD)| &#x2611; | &#x2611;  |
| Adaptive Forms | &#x2611; | &#x2611; |
| Data Integration | &#x2611; | &#x2611; |
| Automated Forms Conversion Service | &#x2611; | &#x2611; |
| Integration with [!DNL Adobe Sign] | &#x2611; | &#x2611; |
| Integration with [!DNL AEM Sites] | &#x2611; | &#x2611; |
| Enhanced Visual Rule editor | &#x2612; | &#x2611; |
| Forms Portal | &#x2611; | Coming Soon |
| Integration with [!DNL Adobe Analytics] | &#x2611; | Coming Soon |
| Integration with [!DNL Adobe Target] | &#x2611; | Coming Soon |
| Document Security | &#x2611; | &#x2612; |

`*` New features every month and bug fix updates on daily basis.

For a comprehensive list of changes in AEM as a Cloud Service, See [What is New and What is Different](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/overview/what-is-new-and-different.html) and [Notable changes in [!DNL AEM Forms] as a Cloud Service](notable-changes.md) -->
