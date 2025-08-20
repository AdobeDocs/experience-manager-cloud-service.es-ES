---
title: Notas de la versión actuales de [!DNL Adobe Experience Manager] as a Cloud Service.
description: Notas de la versión actuales de [!DNL Adobe Experience Manager] as a Cloud Service.
mini-toc-levels: 1
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
feature: Release Information
role: Admin
source-git-commit: 07b957374dcc513050c48bb320e8d639385c3344
workflow-type: tm+mt
source-wordcount: '2350'
ht-degree: 90%

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

La fecha de lanzamiento de la versión de funcionalidad actual de [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] (2025.7.0) fue el 7 de agosto de 2025. La próxima versión con funcionalidades (2025.8.0) está planificada para el 28 de agosto de 2025.

## Notas de la versión de mantenimiento {#maintenance}

Puede encontrar las últimas notas de la versión de mantenimiento [aquí](/help/release-notes/maintenance/latest.md).

<!-- 

## Release Video {#release-video}

Have a look at the July 2025 Release Overview video for a summary of the features added in the 2025.7.0 release:

>[!VIDEO](https://video.tv.adobe.com/v/3440920?quality=12)

-->

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Nuevas funciones de Experience Manager Sites {#enhancements-sites}

* Ahora puede copiar fragmentos de contenido con fragmentos de referencia (secundarios) en una operación. Esto permite reutilizar estructuras de fragmentos de contenido existentes para crear contenido nuevo.
* En la IU de administración de fragmentos de contenido ahora puede ver el estado del flujo de trabajo de los fragmentos de contenido, con información detallada sobre los flujos de trabajo pasados y en ejecución para un fragmento seleccionado.
* Al cambiar el nombre o mover una página de origen de Live Copy, ahora se volverá a publicar una página de Live Copy con el nombre correspondiente o en la ubicación correspondiente.

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

**Añadir formas a plantillas de Dynamic Media**

Ahora puede [añadir capas de formas a las plantillas de Dynamic Media](/help/assets/dynamic-media/dynamic-media-templates.md#add-shapes-to-the-canvas) en Experience Manager Assets. De forma similar a las capas de imagen y texto, las capas de forma admiten parámetros para actualizaciones en tiempo real a través de la dirección URL de la plantilla. También puede incluir vínculos de llamada a acción (call-to-action, CTA) a las formas de sus plantillas.

![Añadir formas a plantillas de Dynamic Media](/help/assets/assets/enable-uniform-radius-shape.png)

**Mejoras de metadatos generados por IA**

Ahora, AEM Assets le permiten [configurar la visualización de los títulos de los recursos en la vista de tarjeta o la vista de lista](/help/assets/smart-tags.md#configure-ai-generated-titles) en la página de exploración de recursos. Puede elegir mostrar el título del recurso definido por usted, el título generado mediante IA o utilizar un título generado por IA solo si no hay ningún título existente para el recurso.

![Configurar títulos generados por IA](/help/assets/assets/configure-title-ai-generated.png)

Ahora también puede deshabilitar los metadatos generados por IA a nivel de la carpeta.

### Nuevas funciones en el centro de contenido {#new-features-content-hub}

**Mayor flexibilidad en la personalización de marca de Content Hub**

Basándose en las funciones de personalización existentes, Content Hub ahora permite a los administradores adaptar aún más su implementación añadiendo imágenes de logotipo personalizadas. También se ha añadido compatibilidad con el formato de archivo TIFF para imágenes de banner y logotipo, lo que permite una mayor flexibilidad en el diseño.

**Uso compartido más inteligente con vínculos con título**

Ahora puede añadir un título al generar un vínculo compartido, ya sea desde la vista de detalles del recurso o después de seleccionar uno o varios recursos. Esto ayuda a los destinatarios a identificar fácilmente el propósito de cada vínculo, especialmente cuando reciben varios recursos compartidos.

![vínculo privado y público](/help/assets/assets/shared-link-for-assets.png)

**Se ha mejorado la navegación por filtros**

Content Hub ahora incluye la opción **Mostrar todo** dentro de los filtros, lo que permite a los usuarios ver todas las facetas disponibles junto con los recuentos de recursos en lugar de la limitación actual de ver solo hasta 10 facetas. Las funciones mejoradas de búsqueda y ordenación dentro de cada filtro facilitan la detección y administración de recursos de forma más eficaz.

### Aplicación de escritorio de AEM versión 3.0.0 {#desktop-app-release-3.0.0}

Disfrute de una carga automatizada de nuevos archivos y carpetas, mejores operaciones de archivos, una detección de recursos más inteligente y una integración perfecta con AEM, lo que hace que la administración de contenido sea más rápida, clara e intuitiva.

Para obtener la lista completa de las funciones, consulte [Notas de la versión de la aplicación de escritorio](https://experienceleague.adobe.com/es/docs/experience-manager-desktop-app/using/release-notes).

### Nuevas funciones en Dynamic Media con funciones de OpenAPI {#new-features-dynamic-media-with-openapi}

**Vista previa de los recursos antes de publicarlos**

[!DNL Dynamic Media with OpenAPI capabilities] ahora permite obtener una vista previa de los recursos directamente en las páginas de creación de [!DNL AEM Sites] antes de ponerlos a disposición del público. Comparta las páginas de vista previa con las partes interesadas para recopilar comentarios sobre la calidad visual y la adaptación contextual. Durante el ciclo de revisión, puede crear y administrar varias versiones de los recursos antes de finalizarlas para su publicación.

**Imágenes inteligentes mejoradas para solicitudes de imagen de OpenAPI**

Todas las solicitudes de imagen de OpenAPI ahora aprovechan totalmente las imágenes inteligentes con promoción automática y lógica de reserva. Esta mejora optimiza las imágenes en función de las condiciones del dispositivo y de la red, lo que permite una carga más rápida de las páginas y un menor uso del ancho de banda, al tiempo que se mantiene la calidad visual.


## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### Nuevas funciones en AEM Forms {#forms-new-features}

* **Editor universal para formularios adaptables y fragmentos de formulario**

  El [editor universal](/help/edge/docs/forms/universal-editor/overview-universal-editor-for-edge-delivery-services-for-forms.md) ahora permite crear formularios adaptables y fragmentos de formulario reutilizables. Los autores pueden crear formularios de forma visual, configurar acciones de envío y añadir la validación reCAPTCHA, todo ello en un entorno de creación simplificado de WYSIWYG. Esta posibilidad acelera la creación de formularios, mejora la coherencia y la protección contra el correo no deseado y el uso indebido automatizado.

  ![Editor universal](/help/edge/docs/forms/universal-editor/assets/universal-editor.png){width=80%, align-center}


* **Servicio de envío de formularios para los formularios de Edge Delivery Services**

  El [servicio de envío de Forms](/help/forms/forms-submission-service.md) le permite almacenar sin problemas datos de los envíos de formularios adaptables directamente en plataformas de hojas de cálculo populares, como Google Sheets, Microsoft OneDrive o SharePoint. Esta integración optimiza la administración de datos al permitir el envío directo de datos de formulario a la hoja de cálculo elegida, lo que elimina la transferencia manual de datos y reduce los errores.Entre las ventajas clave se incluyen las siguientes:

   * **Integración directa:** configure los formularios para enviar datos directamente a una hoja de cálculo especificada.
   * **Asignación de datos personalizados:** asigne campos de formulario a las columnas de hoja de cálculo correspondientes para el almacenamiento organizado.
   * **Control de acceso:** aproveche los permisos de hoja de cálculo existentes para administrar quién puede acceder a los datos enviados o modificarlos.

* **Generación y sincronización de representaciones AFP desde los formularios adaptables**

  La [API de sincronización de salida AFP](/help/forms/document-generation-afp-api.md) permite a los administradores y usuarios generar la salida AFP (presentación de funciones avanzadas) a partir de los formularios adaptables y sincronizar la salida con los sistemas externos o las ubicaciones de almacenamiento. AFP es un formato de documento de alto rendimiento optimizado para la impresión, que se usa a menudo en entornos empresariales a gran escala.

* **Compatibilidad con asignación automática para fragmentos de formularios adaptables**

  Adaptive Forms ahora admite [asignación automática de fragmentos de formularios adaptables](/help/forms/adaptive-form-fragments-core-components.md#auto-mapping-support-for-fragments-in-an-adaptive-form). Con esta mejora, los fragmentos coincidentes se insertan automáticamente cuando los objetos de esquema se alinean con una estructura de fragmentos definida. Simplifica la creación de formularios, mejora la reutilización de fragmentos y garantiza la coherencia en todos los formularios integrados en datos.

* **Título de formulario personalizado en documento de registro**

  Los autores ahora pueden definir un título de formulario personalizado [en el documento de registro](/help/forms/generate-document-of-record-core-components.md#customize-the-branding-information-in-document-of-record) al editar el título del formulario personalizado. El título personalizado aparece en el encabezado de PDF, en las propiedades del documento de PDF y como título de la vista inicial cuando se abre PDF, lo que garantiza una identificación clara y una marca coherente.

* **Tratamiento de errores mejorado para tipos de archivos restringidos**

  [Ahora se admite la administración de errores para los tipos de archivo restringidos](https://experienceleague.adobe.com/es/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/file-attachment#validation-tab), lo que bloquea las cargas de archivos no admitidas. Cuando los usuarios intentan enviar un archivo cambiando su tipo a un formato no compatible, el formulario genera un error durante el envío.


<!--
### Pre-release features in AEM Forms {#forms-new-pre-release-features}

**Enhancements in Rule Editor**

* The `validate` / `reset` method in the function list now supports validation at the panel, field, and form levels.
* Client-side custom function parsing now supports ES10+ JavaScript features and static imports.
* The button to download Document of Record (DoR) is now available as an out-of-the-box (OOTB) option in the rule editor.
* Rules now support the use of dynamic variables.
* Custom event-based rules are now supported.
* Repeatable panel rules are now executed based on context, rather than only on the last panel instance.
* Rules can now be triggered based on query parameters, UTM parameters, and browser parameters.
* Form-specific custom function scripts are now supported for Adaptive Forms in Edge Delivery Services.

### New Early Access Features in AEM Forms {#forms-new-early-access-features}

The AEM Forms Early Access Program offers a unique opportunity for you to get exclusive access to cutting-edge innovations and help shape their development.

These release notes list the innovations delivered in the current release. For the complete list of innovations available under the Early Access Program, see [AEM Forms Early Access Program documentation](/help/forms/early-access-ea-features.md). 


**Forms Optimization opportunities**

Forms Optimization uses AI to analyze your forms and suggest improvements for better performance. It highlights forms with low engagement, flags accessibility issues, and generates AI-powered variations to help increase conversion rates and compliance with WCAG standards.

>[!VIDEO](https://video.tv.adobe.com/v/3469472/) 

Key optimization opportunities include:

* Increasing visibility for forms with low views
* Improving completion rates for forms with low conversions
* Addressing accessibility compliance issues
* Streamlining navigation to enhance user experience

With Forms Optimization, you get automated, data-driven recommendations and variations, making it easier to boost engagement and ensure your forms are effective and inclusive. -->

**Editor de reglas para el editor de comunicaciones interactivas**

Cree acciones dinámicas basadas en datos directamente en los documentos mediante una interfaz intuitiva de apuntar y hacer clic. Defina fácilmente la lógica condicional, automatice los flujos de trabajo y personalice el contenido sin escribir código.

**CLI de AEM Forms Scaffolder para componentes personalizados**

>[!VIDEO]&#x200B;(https://video.tv.adobe.com/v/3470514/aem-forms scaffolding-aem-custom component-generator-aem-forms-cli-aem-forms-custom component-aem-forms-development tool)

Acelere el desarrollo de AEM Forms Edge Delivery Services con esta herramienta de CLI. Genere al instante el código y la conexión necesarios para poner en marcha el desarrollo de componentes personalizados, sin código repetitivo ni complicaciones.

**Herramienta de integración de la API para datos de formularios dinámicos**

La herramienta de integración de la API permite a los autores de formularios crear formularios dinámicos e inteligentes que recuperan y rellenan automáticamente datos de las API REST externas en función de las interacciones del usuario. Esta posibilidad de integración sin código transforma los formularios estáticos en interfaces de recopilación de datos adaptables.

## [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation {#foundation}

### Vista de nodos para la administración de permisos {#node-view}

AEM presenta la administración de permisos de la vista de nodos. La funcionalidad principal sigue siendo la misma que la IU clásica, pero es más fácil de usar y eficiente. Consulte el [artículo específico](/help/security/touch-ui-principal-view.md) para obtener más información.

### Proceso de desuso actualizado {#updated-deprecation-process}

Adobe revisa regularmente las funciones, bibliotecas, API y configuraciones para asegurarse de que cumplen los estándares de rendimiento, seguridad y valor. Cuando las funciones ya no cumplen estos estándares, se marcan para proceder a su desuso y se informa de que su uso dejará de estar disponible en una fecha de eliminación especificada. Antes de esta fecha, Adobe se lo recordará a los clientes mediante notificaciones por correo electrónico, y les indicará las acciones que deben realizar en Cloud Manager antes de continuar con la implementación de nuevas compilaciones. Si no se llevan a cabo las acciones necesarias, es posible que no se pueda realizar la actualización a las nuevas versiones de AEM, lo que podría tener un impacto negativo en la seguridad, el rendimiento, la fiabilidad y la disponibilidad.

Consulte el [artículo sobre el proceso de desuso](/help/release-notes/deprecated-removed-features.md) para obtener más información.

#### API de Java y configuración de OSGi en desuso próximas a las fechas de eliminación {#deprecated-near-removals}

Amplíe la lista siguiente para ver las API y las configuraciones de OSGi en desuso que deben dejar de usarse. Para obtener información detallada (incluidas las fechas de eliminación), consulte el artículo sobre el proceso de desuso.

<details>
  <summary>Amplíe para ver qué va a quedar en desuso</summary>

API de Java:

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

Propiedades de OSGi:

* `org.apache.sling.commons.log.LogManager` (todas las propiedades)
* `org.apache.sling.commons.log.LogManager.factory.config` (`org.apache.sling.commons.log.file`, `org.apache.sling.commons.log.pattern`)

</details>

### Desuso de tiempo de ejecución de Java 11 {#java11-runtime-deprecation}

El **tiempo de ejecución de Java 11* ya está en desuso, y la mayoría de los entornos ya se han actualizado al &#x200B;** tiempo de ejecución de Java 21** de mayor rendimiento.

Si su entorno no se ha podido actualizar debido a dependencias no admitidas (consulte [Requisitos de tiempo de ejecución de Java 21](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md#runtime-requirements)), debería haber recibido un correo electrónico de Adobe con los siguientes pasos específicos. Asegúrese de que todas las actualizaciones requeridas se hayan completado el **28 de agosto de 2025** para que su entorno se pueda actualizar sin interrupciones.

Nota: La versión del tiempo de ejecución es independiente de la versión de compilación del código. Aunque recomendamos la compilación con Java 21, las compilaciones de Java 11 siguen siendo compatibles por ahora. En el futuro, se publicará un aviso independiente sobre el desuso de compilaciones de Java 11.

### Aplicación de la directiva de configuración de registros Java de AEM {#logconfig-policy}

Como se indica en las notas de la versión de abril, los registros Java de AEM deben seguir un formato estándar para garantizar una monitorización de confianza en todos los entornos de clientes. Ya no se admiten las configuraciones de registro personalizadas, como los cambios en el formato de los registros, archivos de salida o niveles de registro predeterminados. Los registros deben permanecer dirigidos a los archivos predeterminados y se deben conservar los niveles de registro predeterminados para el código de producto de AEM. Consulte todos los detalles en el [Artículo de registro](/help/implementing/developing/introduction/logging.md#configuration-loggers).

A partir de **finales de agosto**, se omitirán todas las invalidaciones de registro personalizadas no admitidas. Según nuestro análisis, la mayoría de los clientes no se verán afectados y Adobe se pondrá en contacto directamente con cualquier cliente cuya configuración actual pueda verse afectada.

Revise y actualice cualquier proceso descendente que dependa del comportamiento de registro personalizado. Por ejemplo:

* Si el sistema de reenvío de registros espera un formato de registro personalizado, es posible que tenga que ajustar las reglas de ingesta.
* Si anteriormente ha reducido los detalles de los registros cambiando los niveles de registro, tenga en cuenta que restablecer los niveles predeterminados podría aumentar el volumen del registro.

### Depuración predeterminada de versiones anteriores y registros de auditoría {#mt-defaults}

Actualmente, las versiones de contenido y los registros de auditoría tienen sus *tareas de mantenimiento de depuración asociadas, deshabilitadas de forma predeterminada y, por lo tanto, no se eliminan datos a menos que se configuren explícitamente.

Sin embargo, para optimizar el rendimiento del repositorio, la depuración se activará de forma predeterminada en una fecha anunciada futura, siguiendo estas directrices:

#### Versiones de contenido {#mt-content}

* **Nuevos entornos* (creados después de una fecha próxima (se comunicará más adelante)
   * Las versiones con una antigüedad de más de **30 días* se eliminarán periódicamente.
   * Se conservan las cinco versiones más recientes de los últimos 30 días, junto con la versión más reciente y la versión actual, independientemente de su antigüedad.

* **Entornos existentes* (creados antes de esta próxima fecha):
   * Las versiones con una antigüedad de más de **7 años* se eliminarán periódicamente.
   * Se conservan todas las versiones de los últimos 7 años.
   * Este alto umbral predeterminado evita la eliminación involuntaria de datos recientes. Sin embargo, se recomienda configurar valores más bajos para optimizar el rendimiento del repositorio.

* Puede modificar estos valores predeterminados mediante la configuración de YAML, implementada mediante la canalización de configuración.

#### Registro de auditoría {#mt-auditlogs}

* **Nuevos entornos* (creados después de una fecha próxima, que se comunicará por separado):
   * Se eliminarán periódicamente los registros de replicación, DAM y auditoría de páginas de más de **7 días*.
   * Todos los eventos se registran de forma predeterminada.

* **Entornos existentes* (creados antes de esta próxima fecha):
   * Se eliminarán periódicamente los registros de replicación, DAM y auditoría de páginas de más de **7 años*.
   * Todos los eventos se registran de forma predeterminada.
   * Este alto umbral predeterminado evita la eliminación involuntaria de datos recientes. Sin embargo, se recomienda configurar valores más bajos para optimizar el rendimiento del repositorio.

* Puede modificar estos valores predeterminados mediante la configuración de YAML, implementada mediante la canalización de configuración.

Para obtener más información, consulte el [artículo de tareas de mantenimiento](/help/operations/maintenance.md#defaults).

### Computación de Edge (programa Alpha) {#edge-computing}

La computación de Edge le permite ejecutar JavaScript en la capa de CDN, lo que acerca el procesamiento de datos al usuario final. Esto reduce la latencia y permite experiencias dinámicas y adaptables en Edge.

Los casos de uso comunes incluyen los siguientes:

* Autenticación de usuarios con un proveedor de identidad antes de conceder acceso al contenido
* Personalización de contenido en función de la geolocalización, el tipo de dispositivo o los atributos del usuario
* Actuación como middleware entre la CDN y su origen
* Modificar el formato de las respuestas de API de terceros (y tal vez añadir las respuestas de varias API) antes de enviarlas al explorador
* Composición y muestra de HTML procesado por el servidor en Edge con contenido reunido de varios backend
* Exposición de un servidor MCP para LLM como ChatGPT y Claude para acceder a herramientas personalizadas

Tenemos un número limitado de oportunidades disponibles para el envío de publicaciones de AEM o para proyectos de Edge Delivery Services para sitios de producción en directo. Si está interesado en participar o desea obtener más información, envíe un correo electrónico a [aemcs-edgecompute-feedback@adobe.com](mailto:aemcs-edgecompute-feedback@adobe.com) con una breve descripción de su caso de uso.

### Configuración de CDN para Edge Delivery Services (programa Beta) {#cdn-eds-beta}

La CDN administrada por Adobe ofrece opciones de configuración flexibles, tal como se describe en el [artículo de canalizaciones de configuración](/help/operations/config-pipeline.md#configurations). 

Ahora en versión Beta, implemente una canalización de configuración para funciones que incluyan selectores de origen de CDN, transformaciones de respuesta y solicitud, reenvío de registros de CDN, etc. Póngase en contacto con [aemcs-cdn-config-adopter@adobe.com](mailto:aemcs-cdn-config-adopter@adobe.com) con los detalles de su caso de uso.

### Instantáneas para los RDE (programa Alpha) {#rde-snapshot-beta}

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
