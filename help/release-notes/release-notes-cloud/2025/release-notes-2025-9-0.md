---
title: Notas de la versión 2025.9.0 de la versión de  [!DNL Adobe Experience Manager]  as a Cloud Service.
description: Notas de la versión 2025.9.0 de la versión de  [!DNL Adobe Experience Manager]  as a Cloud Service.
feature: Release Information
role: Admin
source-git-commit: e41828b04a33cc36ee2fc8a4704d9c3cf352830b
workflow-type: tm+mt
source-wordcount: '2088'
ht-degree: 92%

---

# Notas de la versión 2025.9.0 para [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

En la siguiente sección se describen las notas de la versión de funciones de la versión 2025.9.0 de [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Desde aquí puede navegar hasta las notas de la versión de versiones anteriores, como 2023 o 2024.
>
>Eche un vistazo a la [Hoja de ruta de versiones de Experience Manager](https://experienceleague.adobe.com/es/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap) para obtener más información acerca de las próximas activaciones de funcionalidades para [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Para recibir una notificación mensual por correo electrónico acerca de las actualizaciones realizadas en las notas de la versión de Experience Cloud, suscríbase a las [actualizaciones prioritarias de productos de Adobe](https://www.adobe.com/subscription/priority-product-update.html).

## Fecha de lanzamiento {#release-date}

La fecha de lanzamiento de la versión de funcionalidad actual de [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] (2025.9.0) fue el jueves, 25 de septiembre de 2025. La próxima versión con funcionalidades (2025.10.0) se planificó para el jueves, 30 de octubre de 2025.

## Notas de la versión de mantenimiento {#maintenance}

Puede encontrar las últimas notas de la versión de mantenimiento [aquí](/help/release-notes/maintenance/latest.md).

<!-- 

## Release Video {#release-video}

Have a look at the July 2025 Release Overview video for a summary of the features added in the 2025.7.0 release:

>[!VIDEO](https://video.tv.adobe.com/v/3440923?captions=spa&quality=12)

-->

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Nuevas funciones de la versión preliminar de Experience Manager Sites {#prerelease-sites}

El editor de modelos de contenido para fragmentos de contenido de AEM se ha modernizado para alinearse con otras interfaces basadas en React Spectrum en AEM. Su implementación de interfaz de usuario y modelo de extensibilidad ahora son coherentes con el editor de fragmentos de contenido y el editor universal. El nuevo editor de modelos ahora es predeterminado cuando se abre desde la nueva IU de administración del modelo de contenido. Al abrir un modelo de contenido en la IU táctil, se abre el editor de la IU táctil y se realizan ofertas para probar el nuevo editor.

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Nuevas funciones de la vista Recursos {#new-features-assets-view}

**Formato de texto mejorado con subcadenas en plantillas de Dynamic Media**

Ahora puede aplicar formato a subcadenas dentro de las capas de texto de plantillas de Dynamic Media. Una palabra o frase seleccionada se trata como una capa independiente, lo que le permite ajustar su fuente, tamaño de fuente, color, etc. La capa de la subcadena está parametrizada para que pueda actualizarla en tiempo real mediante la dirección URL de envío de la plantilla

### Nuevas funciones en Dynamic Media con funciones de OpenAPI {#new-features-dynamic-media-with-openapi}

**URL de entrega de recursos legibles y de marca**

Mejore la legibilidad humana de Dynamic Media con las URL de OpenAPI aprovechando las URL mnemónicas de Dynamic Media con OpenAPI. Las URL mnemónicas permiten reemplazar los UUID largos, generados por el sistema y difíciles de memorizar en las URL de entrega de recursos con identificadores cortos controlados por la marca. Esto hace que las URL mnemónicas sean más cortas, fáciles de leer y compartir y permiten una mejor alineación con su marca o campañas. Las URL mnemónicas se resuelven automáticamente en el UUID del recurso original durante la ejecución sin interrumpir los flujos de trabajo existentes.

>[!NOTE]
>
>Esta función está disponible como función de disponibilidad limitada. Consulte este [artículo](/help/assets/vanity-urls.md) para comenzar.

### Nuevas funciones en el centro de contenido {#new-features-content-hub}

**Marcar colecciones como favoritas**

Ahora puede marcar colecciones como Favoritos en Content Hub, lo que facilita su organización y recuperación. Una vez agregadas, las colecciones favoritas estarán disponibles en la pestaña Favoritos de la página principal de Content Hub.


**Colecciones de anclajes para acceso rápido**

Los administradores de Content Hub ahora pueden anclar colecciones en Content Hub para acceder rápidamente a ellas. Las colecciones ancladas se muestran en una sección anclada dedicada en la página de inicio Colecciones, lo que facilita mantener las colecciones importantes a mano.

>[!IMPORTANT]
>
>Estas funciones están disponibles como funciones de disponibilidad limitada. Puede [crear y enviar un caso de asistencia al cliente de Adobe](https://helpx.adobe.com/es/enterprise/using/support-for-experience-cloud.html) para habilitarlo para su implementación.

<!--

### New Features in Content Hub {#new-features-content-hub}

**Mark Collections as Favourites**

You can now mark collections as Favorites in Content Hub, making it easier to organize and retrieve them. Once added, your favourite collections are conveniently available from the **Favourites** tab on the Content Hub home page.

**Pin collections for quick access**

Content Hub Administrators can now pin collections in Content Hub for quick access. Pinned collections are displayed in a dedicated **Pinned** section on the Collections home page, making it easier to keep important collections within reach.

>[!NOTE]
>
>These features are available as Limited Availability features. You can [create and submit an Adobe Customer Support case](https://helpx.adobe.com/es/enterprise/using/support-for-experience-cloud.html) to enable it for your deployment.

-->

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### Nuevas funciones de Experience Manager Forms {#new-features-forms}

**Paso de flujo de trabajo Invocar modelo de datos de formulario para archivos adjuntos de lista de SharePoint**

El paso del flujo de trabajo Invocar modelo de datos de formulario ahora admite la gestión de metadatos del lado del flujo de trabajo para matrices de archivos adjuntos codificados en Base64 en modelos de datos de formulario basados en la lista de SharePoint. Con esta mejora, el paso del flujo de trabajo puede pasar, almacenar y recuperar metadatos como el nombre de archivo, el tipo MIME y las propiedades personalizadas para cada archivo adjunto. Esta funcionalidad permite una administración de datos más completa y facilita una integración descendente sin problemas. Para obtener más información, consulte [Mayor compatibilidad en el paso del flujo de trabajo Invocar modelo de datos de formulario para los archivos adjuntos de lista de SharePoint](/help/forms/aem-forms-workflow-step-reference.md#invoke-form-data-model-fdm-service-step).

### Funciones de la versión preliminar de AEM Forms

**Mejoras en el editor de reglas**

El editor de reglas ahora admite una mejor navegación y permite el uso de expresiones matemáticas y de funciones en los parámetros de entrada.

**Mejor navegación con soporte para cargas útiles de eventos**

La acción `Navigate To` en los controladores de Invocar servicio ahora admite `EVENT_PAYLOAD`, lo que permite a los autores de formularios configurar acciones de seguimiento basadas en respuestas a eventos. Esta mejora ofrece una mayor flexibilidad para diseñar flujos de trabajo posteriores al envío, lo que garantiza transiciones más suaves y experiencias de usuario más personalizadas. Para obtener más información, consulte [Mejor navegación con soporte para cargas útiles de eventos](/help/forms/invoke-service-enhancements-rule-editor.md#use-case-5-use-event-payload-in-navigate-to-action-in-invoke-service).

**Compatibilidad con funciones y expresiones matemáticas en los parámetros de entrada**

Los parámetros de entrada ahora admiten llamadas a funciones y expresiones matemáticas, lo que permite a los autores de formularios pasar de forma directa valores calculados dinámicamente. Esta mejora optimiza las configuraciones de reglas, elimina la necesidad de campos adicionales y hace que los formularios sean más adaptables a lógicas complejas y escenarios basados en el cálculo. Para obtener más información, consulte [Compatibilidad con funciones y expresiones matemáticas en los parámetros de entrada](/help/forms/rule-editor-core-components-user-interface.md#function-and-mathematical-expression-support-in-input-parameters).

### Nuevas funciones de acceso anticipado de AEM Forms {#forms-new-early-access-features}

El programa de acceso anticipado de AEM Forms ofrece una oportunidad única de obtener acceso exclusivo a innovaciones punteras y ayudar a dar forma a su desarrollo.

En estas notas de la versión se indican las innovaciones de ofrecidas en la versión actual. Para ver la lista completa de innovaciones disponibles en el programa para acceso rápido, consulte la [documentación del programa de acceso rápido de AEM Forms](/help/forms/early-access-ea-features.md).

**Vista previa de PDF en el editor de comunicaciones interactivas**

Los usuarios pueden obtener una vista previa de los PDF de las comunicaciones interactivas sin datos, con archivos de datos JSON locales o con datos de un modelo de datos, lo que permite realizar pruebas flexibles basadas en datos. Para obtener más información, consulte [Vista previa de PDF en el editor de comunicaciones interactivas](/help/forms/interactive-communication/pdf-preview-in-interactive-communication-editor-with-different-data-options.md).

**Compatibilidad de las fuentes personalizadas en las comunicaciones interactivas**

La función Fuentes personalizadas permite que los usuarios incrusten fuentes personalizadas o aprobadas por la organización en las comunicaciones interactivas, lo que garantiza un procesamiento PDF coherente y acorde con la marca en todos los dispositivos y plataformas. Para obtener más información, consulte [Compatibilidad de las fuentes personalizadas en las comunicaciones interactivas](/help/forms/interactive-communication/add-custom-fonts-to-interactive-communication-editor.md).

**Importar y exportar comunicaciones interactivas**

Esta función permite migrar y reutilizar las comunicaciones interactivas entre diferentes entornos. Ahora puede exportar una comunicación interactiva junto con sus fragmentos asociados y modelos de datos desde un entorno e importarla a otro. Para obtener más información, consulte [Importar y exportar comunicaciones interactivas](/help/forms/interactive-communication/import-and-export-interactive-communications.md).

<!--
**Forms Optimization opportunities**

Forms Optimization uses AI to analyze your forms and suggest improvements for better performance. It highlights forms with low engagement, flags accessibility issues, and generates AI-powered variations to help increase conversion rates and compliance with WCAG standards.

>[!VIDEO](https://video.tv.adobe.com/v/3469472/) 

Key optimization opportunities include:

* Increasing visibility for forms with low views
* Improving completion rates for forms with low conversions
* Addressing accessibility compliance issues
* Streamlining navigation to enhance user experience

With Forms Optimization, you get automated, data-driven recommendations and variations, making it easier to boost engagement and ensure your forms are effective and inclusive. 
-->

## [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation {#foundation}

### Nuevas funciones en la gestión de versiones {#new-features-release-management}

**Pausar actualizaciones de mantenimiento automático**

Días de lanzamiento, eventos en directo, picos de ventas: estos momentos no pueden fallar. [Nuestras nuevas funciones de autoservicio](/help/implementing/deploying/quiet-hours-update-free-periods.md) detienen las actualizaciones de mantenimiento automático cuando son importantes, para que sus equipos se mantengan enfocados.

* Horas de descanso: bloquea el mantenimiento automático durante las horas establecidas cada día. Ideal para horarios de trabajo, ejecuciones nocturnas o transiciones matinales.
* Período sin actualizaciones: bloquea el mantenimiento automático durante una semana completa. Utilícelo para lanzamientos, promociones o bloqueos anuales.

>[!NOTE]
>
>Disponible como función de disponibilidad limitada desde el 25 de septiembre.
>&#x200B;>Envíe un correo electrónico a [aemcs-update-free@adobe.com](mailto:aemcs-update-free@adobe.com) para activarlo en sus programas.

### Nueva versión de las herramientas para desarrolladores de AEM para Eclipse {#aem-develeper-tools-for-eclipse}

Se ha lanzado la versión 1.4.0 de las herramientas para desarrolladores de AEM para Eclipse. Esta versión añade compatibilidad con Eclipse IDE 2022-12 o una versión más reciente y se ha validado con la versión actual (2025-09). Las herramientas ahora funcionan con versiones modernas del arquetipo de proyecto AEM e incorporan mejoras de Sling IDE Tooling 1.3.0.

Instale desde [Eclipse Marketplace](https://marketplace.eclipse.org/content/aem-developer-tools-eclipse) y consulte la [página de herramientas para desarrolladores de AEM](https://eclipse.adobe.com) para obtener más información.

### Próximas obsolescencias de la API de Java {#java-api-deprecation}

Varias API obsoletas se marcaron para su eliminación el 31 de agosto, y por lo tanto, ya no deben utilizarse como referencia. Recibirá notificaciones del Centro de acciones si se detecta un uso de la API obsoleto en el código y, a partir del 13 de noviembre, aparecerán avisos durante las compilaciones de Cloud Manager para reforzar la importancia de eliminar su uso. Consulte el [artículo sobre obsolescencia](/help/release-notes/deprecated-removed-features.md#aem-apis) para obtener más detalles, pero, para mayor comodidad, estas API se enumeran a continuación:

+++ Expandir para ver las funciones obsoletas de la API de Java

* `org.apache.sling.commons.auth`
* `org.apache.felix.webconsole`
* `org.eclipse.jetty`
* `com.mongodb`
* `org.apache.abdera`
* `org.apache.felix.http.whiteboard`
* `org.apache.cocoon.xml`
* `ch.qos.logback`
* `org.slf4j.spi`
* `org.slf4j.event`
* `org.apache.log4j`
* `com.google.common`
* `com.drew`
* `org.bson`
* `org.apache.jackrabbit.oak.plugins.blob`
* `org.apache.jackrabbit.oak.plugins.memory`

+++

<!--
OSGi properties:

* `org.apache.sling.commons.log.LogManager` (all properties)
* `org.apache.sling.commons.log.LogManager.factory.config` (`org.apache.sling.commons.log.file`, `org.apache.sling.commons.log.pattern`)
* 

-->

### Desuso de tiempo de ejecución de Java 11 {#java11-runtime-deprecation}

El *entorno de ejecución de Java 11* ha quedado obsoleto, y la mayoría de los entornos ya se han actualizado al **entorno de ejecución de Java 21** que ofrece un mayor rendimiento.

Si su entorno no se ha podido actualizar debido a dependencias no admitidas (consulte los [requisitos del entorno de ejecución de Java 21](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md#runtime-requirements)), debería haber recibido un correo electrónico de Adobe con los siguientes pasos. Como se describió allí, Adobe actualizó sus entornos **Dev** y **RDE** el **18 de septiembre de 2025** para que pueda validar su sitio y sus procesos y solucionar cualquier problema. Las actualizaciones de los entornos **Ensayo** y **Producción** continuarán el **14 de octubre de 2025**.

>[!NOTE]
>
>La versión del tiempo de ejecución es independiente de la versión de compilación del código. Aunque recomendamos la compilación con Java 21, las compilaciones de Java 11 siguen siendo compatibles por ahora. En el futuro, se publicará un aviso independiente sobre el desuso de compilaciones de Java 11.

### Aplicación de la directiva de configuración de registros Java de AEM {#logconfig-policy}

Como se indica en las notas de la versión de abril, los registros Java de AEM deben seguir un formato estándar para garantizar una monitorización de confianza en todos los entornos de clientes. Ya no se admiten las configuraciones de registro personalizadas, como los cambios en el formato de los registros, archivos de salida o niveles de registro predeterminados. Los registros deben permanecer dirigidos a los archivos predeterminados y se deben conservar los niveles de registro predeterminados para el código de producto de AEM. Consulte todos los detalles en el [Artículo de registro](/help/implementing/developing/introduction/logging.md#configuration-loggers).

A partir del **30 de octubre**, se ignorarán todas las modificaciones de registro personalizadas no compatibles. Según nuestro análisis, la mayoría de los clientes no se verán afectados y Adobe se pondrá en contacto directamente con cualquier cliente cuya configuración actual pueda verse afectada.

Revise y actualice cualquier proceso descendente que dependa del comportamiento de registro personalizado. Por ejemplo:

* Si el sistema de reenvío de registros espera un formato de registro personalizado, es posible que tenga que ajustar las reglas de ingesta.
* Si anteriormente ha reducido los detalles de los registros cambiando los niveles de registro, tenga en cuenta que restablecer los niveles predeterminados podría aumentar el volumen del registro.

### Computación de Edge (programa beta) {#edge-computing}

La computación de Edge le permite ejecutar JavaScript en la capa de CDN, lo que acerca el procesamiento de datos al usuario final. Esto reduce la latencia y permite experiencias dinámicas y adaptables en Edge.

Los casos de uso comunes incluyen los siguientes:

* Personalización de contenido en función de la geolocalización, el tipo de dispositivo o los atributos del usuario
* Actuación como middleware entre la CDN y su origen
* Modificar el formato de las respuestas de API de terceros (y tal vez añadir las respuestas de varias API) antes de enviarlas al explorador
* Composición y muestra de HTML procesado por el servidor en Edge con contenido reunido de varios backend
* Exposición de un servidor MCP para LLM como ChatGPT y Claude para acceder a herramientas personalizadas

Tenemos un número limitado de oportunidades disponibles para el envío de publicaciones de AEM o para proyectos de Edge Delivery Services para sitios de producción en directo. Si está interesado en participar o desea obtener más información, envíe un correo electrónico a [aemcs-edgecompute-feedback@adobe.com](mailto:aemcs-edgecompute-feedback@adobe.com) con una breve descripción de su caso de uso.

### Autenticación de Edge para Edge Delivery Services (programa Beta) {#edge-authentication}

La autenticación de Edge le permite restringir el acceso a las páginas de Edge Delivery Services únicamente a aquellas personas que se hayan autenticado con su proveedor de identidad (IdP). Esto se logra mediante la implementación de un archivo YAML de configuración de OpenID Connect (OIDC).

Si le interesa, envíe un correo electrónico a [aemcs-edgecompute-feedback@adobe.com](mailto:aemcs-edgecompute-feedback@adobe.com) con una breve descripción de su caso de uso y cualquier pregunta que pueda tener.

<!--
### CDN Configuration for Edge Delivery Services (Beta Program) {#cdn-eds-beta}

The Adobe-Managed CDN offers flexible configuration options, as described in the [Config Pipeline article](/help/operations/config-pipeline.md#configurations). 

Now in beta, youcan deploy a config pipeline for features including CDN origin selectors, response and request transformations, CDN log forwarding and more. Please reach out to [aemcs-cdn-config-adopter@adobe.com](mailto:aemcs-cdn-config-adopter@adobe.com) with the details of your use case.

-->

### Implementaciones de producción controladas para probar el código antes de aceptar tráfico en directo (programa Beta) {#canary-beta}

Valide una compilación de producción con tráfico de prueba solamente interno antes de exponerla a los usuarios finales. Realice envíos a producción, dirija solo el tráfico controlado (mediante un encabezado especial), monitorice el comportamiento y, a continuación, promocione al tráfico en directo o revierta el proceso, sin afectar a los clientes.

Implemente las versiones de código en producción, pero restrínjalas solo al tráfico de prueba interno antes de decidir si aceptar tráfico en directo en lugar de revertir el proceso.

Envíe un correo electrónico a [aemcs-canary-deployments-beta@adobe.com](mailto:aemcs-canary-deployments-beta@adobe.com) para solicitar acceso y compartir comentarios.

### Instantáneas para los RDE (programa Alpha) {#rde-snapshot-program}

En Alpha, los Entornos de desarrollo rápido (RDE) ahora admiten una función para tomar una instantánea del estado actual del código y el contenido, que se puede restaurar más adelante. Esto puede resultar útil al sincronizar código que puede ser necesario revertir o al cambiar entre el desarrollo de distintas características. También es posible restaurar solo el contenido mutable como punto de partida conocido para realizar pruebas.

Envíe un correo electrónico a [aemcs-rde-support@adobe.com](mailto:aemcs-rde-support@adobe.com) si tiene interés en ofrecer sus comentarios sobre esta función.

### Reenvío de registros de AEM a más destinos (programa Beta) {#log-forwarding-beta}

Aunque los registros se pueden descargar desde Cloud Manager, muchas organizaciones consideran beneficioso transmitir estos registros a un destino de registro preferido. AEM ya admite el reenvío de registros de AEM y CDN a Azure Blob Storage, Datadog, HTTPS, Elasticsearch (y OpenSearch) y Splunk. Esta función se ha configurado en forma de autoservicio e implementado usando la canalización de configuración.

Ahora en la versión Beta, puede reenviar los registros de AEM a Amazon S3, Sumo Logic y a su propia cuenta de New Relic (no a la cuenta proporcionada por Adobe). Tenga en cuenta que los registros de AEM (incluido Apache/Dispatcher) son compatibles con los destinos de estos registros, pero no con los de CDN. Envíe un correo electrónico a [aemcs-logforwarding-beta@adobe.com](mailto:aemcs-logforwarding-beta@adobe.com) para obtener acceso.

Obtenga más información en la [documentación de reenvío de registros](/help/implementing/developing/introduction/log-forwarding.md).

### Monitorización del rendimiento de las aplicaciones (APM) ampliadas (programa Alpha) {#apm-alpha}

En cuanto a la observabilidad, AEM Cloud Service admite actualmente [New Relic One](https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/user-access-new-relic) proporcionado por Adobe y [Dynatrace](https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/dynatrace) administrado por el cliente. Mientras exploramos la compatibilidad con opciones de APM adicionales, envíenos un correo electrónico [aemcs-apm-beta@adobe.com](mailto:aemcs-apm-beta@adobe.com) con su proveedor o tecnología preferidos, junto con casos de uso.


## Guías de [!DNL Experience Manager] {#guides}

Puede encontrar una lista completa de las funciones nuevas y mejoradas de la última versión de Adobe Experience Manager Guides [aquí](https://experienceleague.adobe.com/es/docs/experience-manager-guides/using/release-info/aem-guides-releases-roadmap).

## Cloud Manager {#cloud-manager}

Puede encontrar una lista completa de las versiones mensuales de Cloud Manager [aquí](/help/implementing/cloud-manager/release-notes/current.md).

## Herramientas de migración {#migration-tools}

Puede encontrar una lista completa de las versiones de las herramientas de migración [aquí](/help/journey-migration/release-notes/release-notes-migration-tools-current.md).

## Editor universal {#universal-editor}

Puede encontrar una lista completa de las versiones del editor universal [aquí](/help/release-notes/universal-editor/current.md).

## Generar variaciones {#generate-variations}

Puede encontrar una lista completa de las versiones de generar variaciones [aquí](/help/generative-ai/release-notes-generate-variations.md).

## Notas de la versión de Experience Cloud {#experience-cloud}

Puede encontrar información sobre las versiones de otras aplicaciones de Experience Cloud [aquí](https://experienceleague.adobe.com/es/docs/release-notes/experience-cloud/current).
