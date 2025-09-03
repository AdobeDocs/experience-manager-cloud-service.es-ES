---
title: Notas de la versión actuales de [!DNL Adobe Experience Manager] as a Cloud Service.
description: Notas de la versión actuales de [!DNL Adobe Experience Manager] as a Cloud Service.
mini-toc-levels: 1
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
feature: Release Information
role: Admin
source-git-commit: 0d2164920ca44ee6c872fdfe2090760a1506215d
workflow-type: tm+mt
source-wordcount: '1961'
ht-degree: 48%

---

# Notas de la versión actuales de [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

En la siguiente sección se describen las notas de la versión de la funcionalidad actual (la más reciente) de [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Desde aquí puede navegar hasta las notas de la versión de versiones anteriores, como 2023 o 2024.
>
>Eche un vistazo a la [Hoja de ruta de versiones de Experience Manager](https://experienceleague.adobe.com/es/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap) para obtener más información acerca de las próximas activaciones de funcionalidades para [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Para recibir una notificación mensual por correo electrónico acerca de las actualizaciones realizadas en las notas de la versión de Experience Cloud, suscríbase a las [actualizaciones prioritarias de productos de Adobe](https://www.adobe.com/subscription/priority-product-update.html).

## Fecha de lanzamiento {#release-date}

La fecha de lanzamiento de la versión de funcionalidad actual de [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] (2025.8.0) fue el viernes, 28 de agosto de 2025. La próxima versión con funcionalidades (2025.9.0) se planificó para el viernes, 25 de septiembre de 2025.

## Notas de la versión de mantenimiento {#maintenance}

Puede encontrar las últimas notas de la versión de mantenimiento [aquí](/help/release-notes/maintenance/latest.md).

<!-- 

## Release Video {#release-video}

Have a look at the July 2025 Release Overview video for a summary of the features added in the 2025.7.0 release:

>[!VIDEO](https://video.tv.adobe.com/v/3440920?quality=12)

-->

## Experience Hub {#experience-hub}

[Experience Hub](/help/experience-hub.md) es el punto de partida centralizado para acceder a todas las funcionalidades de AEM. Se personaliza en función de su personalidad de usuario y de las licencias disponibles para usted, lo que permite a cada usuario lograr sus resultados de forma eficaz.

## Asistente de IA en AEM {#AI-assistant}

El [Asistente de IA](/help/implementing/cloud-manager/ai-assistant-in-aem.md) para AEM ofrece una interfaz conversacional diseñada para que obtengas respuestas instantáneas a tus preguntas relacionadas con el producto de AEM (*disponible para todos los usuarios*) y para automatizar la creación de tickets de soporte (*disponible para los administradores de soporte*). Está directamente incrustado en AEM y es accesible desde AEM Experience Hub, Cloud Manager y la interfaz de usuario del autor.

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Nuevas funciones de Experience Manager Sites {#enhancements-sites}

* En la IU de administración de fragmentos de contenido ahora puede ver el estado del flujo de trabajo de los fragmentos de contenido, con información detallada sobre los flujos de trabajo pasados y en ejecución para un fragmento seleccionado.
* El rendimiento para abrir fragmentos de contenido en el nuevo editor de fragmentos de contenido se ha aumentado en un 25 % en escenarios comunes al abrir fragmentos mediante UUID en lugar de por ruta.
* Al copiar fragmentos de contenido con fragmentos a los que se hace referencia, las copias de los fragmentos a los que se hace referencia ahora se almacenan en la misma ubicación que la copia del fragmento principal.
* Ahora puede configurar un espacio de trabajo personalizado en la configuración de la carpeta para exportar los fragmentos de contenido al espacio de trabajo configurado en Adobe Target.

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Nuevas funciones en el centro de contenido {#new-features-content-hub}

**Búsqueda masiva mediante propiedades de filtro**

Content Hub ahora acelera la detección de los recursos que necesita. Con la nueva función Búsqueda masiva, puede introducir varios valores para cualquier propiedad de filtro (separados por un delimitador (por ejemplo, varios ID de SKU)) y recuperar instantáneamente todos los recursos coincidentes mediante una sola búsqueda.

### Nuevas funciones en Dynamic Media con funciones de OpenAPI {#new-features-dynamic-media-with-openapi}

**DM compatible con SEO con URL de OpenAPI**

Cree URL mnemónicas para la entrega de recursos en DM con OpenAPI y sustituya los UUID largos generados por el sistema con identificadores cortos y legibles. Esto hace que los vínculos sean fáciles de usar y estén mejor alineados con su marca o campañas. Las URL mnemónicas se resuelven automáticamente en el UUID del recurso original durante la ejecución sin interrumpir los flujos de trabajo existentes.

>[!NOTE]
>
>Esta función estará disponible como función de disponibilidad limitada el 10 de septiembre. Puede [crear y enviar un caso de asistencia al cliente de Adobe](https://helpx.adobe.com/es/enterprise/using/support-for-experience-cloud.html) para habilitarlo para su implementación.

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### Nuevas funciones de Experience Manager Forms {#new-features-forms}

**Componente de entrada de fecha y hora**

Ya está disponible el componente [Fecha y hora](https://experienceleague.adobe.com/es/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/date-time-component), que permite a los usuarios seleccionar la fecha y la hora mediante una interfaz de calendario y reloj, o introduciendo valores manualmente en un formato compatible.

**Control de errores mejorado para cargas de archivos**

El [componente Archivo adjunto](https://experienceleague.adobe.com/es/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/file-attachment#basic-tab) ahora valida automáticamente el tipo de archivo cargado con la lista de permitidos. Si un usuario carga un archivo en un formato no compatible, el formulario muestra un error durante el envío. El componente también comprueba el contenido del archivo para validar su tipo, lo que mejora la seguridad general del formulario.

**Respuesta de error especificada para la acción de envío personalizada**

Cuando una [acción de envío personalizada](/help/forms/custom-submit-action-troubleshooting.md) encuentra un error no controlado, el sistema devuelve el código de error 502. Esto ayuda a identificar que el problema está relacionado con la acción de envío personalizada, lo que facilita la depuración.

**Excluyendo campos ocultos del documento de registro**

Una nueva propiedad permite la exclusión de campos ocultos del [documento de registro](/help/forms/generate-document-of-record-core-components.md#document-of-record-settings). De forma predeterminada, esta opción no está seleccionada y se aplica a todos los campos de formulario.


### Funciones previas al lanzamiento en AEM Forms

**Generar y sincronizar representaciones AFP**

Ahora puede usar la [API de comunicación de AEM Forms](/help/forms/document-generation-afp-api.md) para convertir un archivo XDP al formato AFP. AFP es un formato de alto rendimiento ampliamente utilizado en la impresión empresarial a gran escala.

**Mejoras en el Editor de reglas**

* [Validar método en la lista de funciones](/help/forms/rule-editor-enhancements-use-cases.md#validate-method-in-function-list): los métodos validate y reset ahora admiten la ejecución en los niveles de panel, campo y formulario. Anteriormente, solo eran compatibles en el nivel de formulario.
* [Compatibilidad moderna con JavaScript](/help/forms/rule-editor-core-components-difference-tables.md): Se ha agregado compatibilidad con ECMAScript 2019 y funciones posteriores para funciones personalizadas, lo que le permite escribir código más eficiente, modular y reutilizable.
* [Descargar opción DoR en el editor de reglas](/help/forms/rule-editor-enhancements-use-cases.md#downloaddor-as-ootb-fuction-in-rule-editor): se ha agregado una función para descargar el documento de registro (DoR) como una opción predeterminada (OOTB) en el editor de reglas.

  ![Documento de registro](/help/forms/assets/document-of-record-rn.gif)

* [Variables dinámicas en el editor de reglas](/help/forms/rule-editor-enhancements-use-cases.md#support-for-dynamic-variables-in-rules): ahora puede usar variables dinámicas (temporales) en el editor de reglas para tener más flexibilidad a la hora de definir condiciones y acciones. Los campos ocultos ya no son necesarios para almacenar valores temporales.
* [Compatibilidad con reglas basadas en eventos personalizados](/help/forms/rule-editor-enhancements-use-cases.md#custom-event-based-rules-support): Ahora puede definir eventos personalizados y reglas de déclencheur basadas en esos eventos.
* [Reglas de panel repetible según el contexto](/help/forms/rule-editor-enhancements-use-cases.md#context-based-rule-execution-for-repeatable-panels): en los paneles repetibles, las reglas ahora se ejecutan según el contexto, en lugar de aplicarse únicamente a la última instancia del panel.
* [Reglas activadas por los parámetros](/help/forms/rule-editor-enhancements-use-cases.md#url-and-browser-parameter-based-rules-in-adaptive-forms): el Editor de reglas ahora admite la ejecución de reglas en función de parámetros de consulta, parámetros de UTM o parámetros de explorador.
* [Funciones personalizadas específicas de formularios](/help/edge/docs/forms/universal-editor/rule-editor-universal-editor.md#organizing-custom-functions-across-different-forms): Edge Delivery Services Forms ahora admite scripts de funciones personalizadas específicos de formularios, lo que proporciona una mayor flexibilidad para administrar la lógica reutilizable.
* [Importaciones estáticas para funciones personalizadas](/help/edge/docs/forms/universal-editor/rule-editor-universal-editor.md#static-imports-for-custom-functions): el Editor de reglas del Editor universal ahora admite importaciones estáticas, lo que permite a los desarrolladores organizar, compartir y reutilizar funciones en varios formularios.

### Nuevas funciones de acceso anticipado de AEM Forms {#forms-new-early-access-features}

El programa de acceso anticipado de AEM Forms ofrece una oportunidad única de obtener acceso exclusivo a innovaciones punteras y ayudar a dar forma a su desarrollo.

En estas notas de la versión se indican las innovaciones de ofrecidas en la versión actual. Para ver la lista completa de innovaciones disponibles en el programa para acceso rápido, consulte la [documentación del programa de acceso rápido de AEM Forms](/help/forms/early-access-ea-features.md).

**Componente de firma manuscrita**

Ahora puede usar el [componente Firma manuscrita](https://experienceleague.adobe.com/es/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/scribble-signature) para ayudar a los usuarios a agregar sus firmas a un formulario, como en un formulario de acuerdo. El componente permite a los usuarios dibujar su firma directamente dentro del formulario con un ratón, un lápiz o una pantalla táctil.

**Integración directa de API en el editor de reglas**

Los Forms adaptables ahora admiten [integración directa de API](/help/forms/api-integration-in-rule-editor.md) en el Editor de reglas visuales sin requerir un modelo de datos de formulario. Los autores pueden configurar las API mediante una importación de URL o cURL, asignar parámetros de entrada/salida y proteger las llamadas con autenticación.

<!--
**Forms Optimization opportunities**

Forms Optimization uses AI to analyze your forms and suggest improvements for better performance. It highlights forms with low engagement, flags accessibility issues, and generates AI-powered variations to help increase conversion rates and compliance with WCAG standards.

>[!VIDEO](https://video.tv.adobe.com/v/3469472/) 

Key optimization opportunities include:

* Increasing visibility for forms with low views
* Improving completion rates for forms with low conversions
* Addressing accessibility compliance issues
* Streamlining navigation to enhance user experience

With Forms Optimization, you get automated, data-driven recommendations and variations, making it easier to boost engagement and ensure your forms are effective and inclusive. -->

## [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation {#foundation}

### Actualización de compilación de JavaScript {#javascript-compilation}

La compilación predeterminada de JavaScript de la biblioteca del lado del cliente (clientlibs) ahora se dirige a ECMASCRIPT_2018 en lugar de ECMASCRIPT5. Aunque reemplazable en el pasado, esta actualización permite mejoras de rendimiento, sintaxis moderna de JavaScript y funciones de forma predeterminada.

### Próximas obsolescencias de la API de Java {#java-api-deprecation}

Varias API obsoletas pretenden eliminarse el 31 de agosto, por lo que ya no se debe hacer referencia a ellas. A principios de septiembre, las notificaciones del Centro de acciones se enviarán si se detecta uso de la API y, después del 25 de septiembre, aparecerán avisos durante las compilaciones de Cloud Manager para reforzar la importancia de eliminar el uso. Consulte el [artículo en desuso](/help/release-notes/deprecated-removed-features.md#aem-apis) para obtener información detallada, pero para su comodidad, estas API se enumeran a continuación:

<details>
  <summary>Amplíe para ver las obsolescencias de la API de Java</summary>

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

</details>

<!--
OSGi properties:

* `org.apache.sling.commons.log.LogManager` (all properties)
* `org.apache.sling.commons.log.LogManager.factory.config` (`org.apache.sling.commons.log.file`, `org.apache.sling.commons.log.pattern`)
* 

-->

### Desuso de tiempo de ejecución de Java 11 {#java11-runtime-deprecation}

El tiempo de ejecución de *Java 11* ya está en desuso, y la mayoría de los entornos ya se han actualizado al tiempo de ejecución de **Java 21** con mayor rendimiento.

Si su entorno no se ha podido actualizar debido a dependencias no admitidas (consulte [Requisitos de tiempo de ejecución de Java 21](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md#runtime-requirements)), debería haber recibido un correo electrónico de Adobe con los siguientes pasos específicos. Asegúrese de que todas las actualizaciones requeridas se hayan completado el **1 de octubre de 2025** para que su entorno se pueda actualizar sin interrupciones.

Nota: La versión del tiempo de ejecución es independiente de la versión de compilación del código. Aunque recomendamos la compilación con Java 21, las compilaciones de Java 11 siguen siendo compatibles por ahora. En el futuro, se publicará un aviso independiente sobre el desuso de compilaciones de Java 11.

### Aplicación de la directiva de configuración de registros Java de AEM {#logconfig-policy}

Como se indica en las notas de la versión de abril, los registros Java de AEM deben seguir un formato estándar para garantizar una monitorización de confianza en todos los entornos de clientes. Ya no se admiten las configuraciones de registro personalizadas, como los cambios en el formato de los registros, archivos de salida o niveles de registro predeterminados. Los registros deben permanecer dirigidos a los archivos predeterminados y se deben conservar los niveles de registro predeterminados para el código de producto de AEM. Consulte todos los detalles en el [Artículo de registro](/help/implementing/developing/introduction/logging.md#configuration-loggers).

A partir del **25 de septiembre**, se omitirán todas las invalidaciones de registro personalizadas no admitidas. Según nuestro análisis, la mayoría de los clientes no se verán afectados y Adobe se pondrá en contacto directamente con cualquier cliente cuya configuración actual pueda verse afectada.

Revise y actualice cualquier proceso descendente que dependa del comportamiento de registro personalizado. Por ejemplo:

* Si el sistema de reenvío de registros espera un formato de registro personalizado, es posible que tenga que ajustar las reglas de ingesta.
* Si anteriormente ha reducido los detalles de los registros cambiando los niveles de registro, tenga en cuenta que restablecer los niveles predeterminados podría aumentar el volumen del registro.

### Informática Edge (programa Beta) {#edge-computing}

La computación de Edge le permite ejecutar JavaScript en la capa de CDN, lo que acerca el procesamiento de datos al usuario final. Esto reduce la latencia y permite experiencias dinámicas y adaptables en Edge.

Los casos de uso comunes incluyen los siguientes:

* Autenticación de usuarios con un proveedor de identidad antes de conceder acceso al contenido
* Personalización de contenido en función de la geolocalización, el tipo de dispositivo o los atributos del usuario
* Actuación como middleware entre la CDN y su origen
* Volver a dar formato a las respuestas de API de terceros (y tal vez agregar varias respuestas de API) antes de enviarlas al explorador
* Composición y muestra de HTML procesado por el servidor en Edge con contenido reunido de varios backend
* Exposición de un servidor MCP para LLM como ChatGPT y Claude para acceder a herramientas personalizadas

Tenemos un número limitado de oportunidades disponibles para el envío de publicaciones de AEM o para proyectos de Edge Delivery Services para sitios de producción en directo. Si está interesado en participar o desea obtener más información, envíe un correo electrónico a [aemcs-edgecompute-feedback@adobe.com](mailto:aemcs-edgecompute-feedback@adobe.com) con una breve descripción de su caso de uso.

### Configuración de CDN para Edge Delivery Services (programa Beta) {#cdn-eds-beta}

La CDN administrada por Adobe ofrece opciones de configuración flexibles, tal como se describe en el [artículo de canalizaciones de configuración](/help/operations/config-pipeline.md#configurations). 

Ahora en la versión beta, puede implementar una canalización de configuración para funciones que incluyen selectores de origen de CDN, transformaciones de respuesta y solicitud, reenvío de registros de CDN y más. Póngase en contacto con [aemcs-cdn-config-adopter@adobe.com](mailto:aemcs-cdn-config-adopter@adobe.com) con los detalles de su caso de uso.

### Instantáneas para los RDE (programa Alpha) {#rde-snapshot-program}

En Alpha, los entornos de desarrollo rápido (RDE) ahora admiten una función para tomar una instantánea del estado actual del código y el contenido, que se puede restaurar más adelante. Esto puede resultar útil al sincronizar código que puede ser necesario revertir o al cambiar entre el desarrollo de distintas características. También es posible restaurar solo el contenido mutable como punto de partida conocido para realizar pruebas.

Envíe un correo electrónico a [aemcs-rde-support@adobe.com](mailto:aemcs-rde-support@adobe.com) si tiene interés en ofrecer sus comentarios sobre esta función.

### Reenvío de registros de AEM a más destinos (programa Beta) {#log-forwarding-beta}

Aunque los registros se pueden descargar desde Cloud Manager, muchas organizaciones consideran beneficioso transmitir estos registros a un destino de registro preferido. AEM ya admite el reenvío de registros de AEM y CDN a Azure Blob Storage, Datadog, HTTPS, Elasticsearch (y OpenSearch) y Splunk. Esta función se ha configurado en forma de autoservicio e implementado usando la canalización de configuración.

Ahora en la versión Beta, puede reenviar los registros de AEM a Amazon S3, Sumo Logic y a su propia cuenta de New Relic (no a la cuenta proporcionada por Adobe). Tenga en cuenta que los registros de AEM (incluido Apache/Dispatcher) son compatibles con los destinos de estos registros, pero no con los de CDN. Envíe un correo electrónico a [aemcs-logforwarding-beta@adobe.com](mailto:aemcs-logforwarding-beta@adobe.com) para obtener acceso.

Obtenga más información en la [documentación de reenvío de registros](/help/implementing/developing/introduction/log-forwarding.md).

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
