---
title: Notas de la versión actuales de [!DNL Adobe Experience Manager] as a Cloud Service.
description: Notas de la versión actuales de [!DNL Adobe Experience Manager] as a Cloud Service.
mini-toc-levels: 1
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
feature: Release Information
role: Admin
source-git-commit: 75816f35a8bca8356e17b13341c2ddbd850f8eff
workflow-type: ht
source-wordcount: '2077'
ht-degree: 100%

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


La fecha de lanzamiento de la versión de funcionalidad actual de [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] (2025.5.0) fue el 5 de junio de 2025. La próxima versión con funcionalidades (2025.6.0) está planificada para el 26 de junio de 2025.

## Notas de la versión de mantenimiento {#maintenance}

Puede encontrar las últimas notas de la versión de mantenimiento [aquí](/help/release-notes/maintenance/latest.md).

<!-- 

## Release Video {#release-video}

Have a look at the February 2025 Release Overview video for a summary of the features added in the 2025.2.0 release:

>[!VIDEO](https://video.tv.adobe.com/v/3440923?quality=12&captions=spa)

-->

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

**Metadatos generados por IA**

AEM Assets ahora usa la [IA para generar automáticamente metadatos, incluidos Título, Descripción y Palabras clave](/help/assets/metadata-assets-view.md#ai-smart-tags). Estos campos generados por IA mejoran la precisión de los metadatos, lo que facilita la búsqueda, la categorización y la recomendación de recursos. Este enfoque no solo mejora la eficacia al eliminar el etiquetado manual, sino que también garantiza la coherencia y la escalabilidad en grandes volúmenes de contenido digital.

![Metadatos generados por IA](/help/assets/assets/enhanced-smart-tags.png)

**Integración con Figma**

AEM Assets se integra de forma nativa con Figma, lo que permite a los diseñadores acceder directamente a los recursos almacenados en AEM Assets desde la propia interfaz de usuario de Figma. Puede colocar contenido administrado en AEM Assets en el lienzo Figma y, a continuación, guardar contenido nuevo o editado en un repositorio de AEM Assets. Para acceder al conector de AEM Assets disponible en la página de la comunidad Figma, haga clic [aquí](https://www.figma.com/community/plugin/1512561378275712210/adobe-experience-manager-aem-assets-connector).

>[!VIDEO](https://video.tv.adobe.com/v/3463828)


### Nuevas funciones en el centro de contenido {#new-features-content-hub}

**Control de acceso basado en atributos (ABAC)**

[El centro de contenido ahora le permite aplicar restricciones basadas en reglas para acceder a los recursos](/help/assets/attribute-based-access-control.md). Los permisos de recursos garantizan el control y también se aseguran de que los usuarios solo puedan acceder a los recursos relevantes.

Las reglas de restricción de recursos se basan en metadatos y, si las condiciones definidas en la regla coinciden con los metadatos del recurso, este se muestra a los grupos de usuarios.

Algunas de las ventajas clave del control de acceso basado en atributos son:

* Elimina la dependencia de la estructura de carpetas para los permisos

* Permite a los administradores cargar recursos y determinar de forma retroactiva las estructuras de permisos

* Reduce el número de duplicados: mejora la integridad de los recursos. Los duplicados son necesarios en los permisos basados en carpetas cuando los mismos recursos se comparten con diferentes grupos.

**Personalización de marca de la interfaz de usuario**

Content Hub ahora permite a los administradores [personalizar la interfaz de usuario con elementos específicos de la marca](/help/assets/configure-content-hub-ui-options.md##configure-branding-content-hub), incluidas imágenes de banners, títulos de banners y texto independiente, así como colores primarios y secundarios. Estas mejoras ayudan a garantizar la coherencia de la marca, simplificar la incorporación de usuarios y generar confianza.

![Personalización de marca de la interfaz de usuario](/help/assets/assets/content-hub-ui-branding.png)

**Uso compartido de vínculos públicos**

Content Hub ahora admite la [generación de vínculos que se pueden compartir para permitir que usuarios externos](/help/assets/share-assets-content-hub.md##share-assets), sin acceso a la aplicación, vean los metadatos de los recursos o descarguen los recursos.

![Personalización de marca de la interfaz de usuario](/help/assets/assets/public-and-private-link.png)

**Control de colecciones**

Content Hub ahora le permite [controlar el acceso a las colecciones durante la creación, asegurando así que solo los usuarios autorizados puedan ver o administrar los recursos agrupados](/help/assets/collections-content-hub.md##create-collections). Garantiza una mayor seguridad, una mejor colaboración, una administración de recursos organizada y un control simplificado.

>[!VIDEO](https://video.tv.adobe.com/v/3463336)

>[!NOTE]
>
>El control de colecciones es una función de disponibilidad limitada. Puede habilitarla creando un ticket de asistencia.

**Descargar varios recursos como ZIP**

Content Hub ahora también le permite [descargar los recursos seleccionados y sus representaciones en un archivo ZIP](/help/assets/download-assets-content-hub.md#download-asset-renditions) y no como archivos independientes, lo que simplifica la administración de archivos.

**Representaciones de medios dinámicos en el centro de contenido**

Acceda a todas las [representaciones de ajustes preestablecidos y recortes inteligentes de Dynamic Media para descargarlos directamente desde la interfaz de usuario de Content Hub](/help/assets/download-assets-content-hub.md#download-asset-renditions).

![Representaciones de medios dinámicos](/help/assets/assets/dm-renditions-content-hub.png)

### Nuevas funciones de Dynamic Media {#new-features-dynamic-media}

**Integración nativa de Dynamic Media con AJO B2C&#x200B;**

[Integración nativa de Experience Manager (AEM) Dynamic Media con Journey Optimizer (AJO) B2C](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/content-management/combine/aem-dynamic), lo que permite a los expertos en marketing incrustar fácilmente los recursos de Dynamic Media de AEM (representación y plantilla de DM) en el contenido de AJO y ofrecer actualizaciones en tiempo real y experiencias personalizadas al máximo en todos los canales.

>[!VIDEO](https://video.tv.adobe.com/v/3463785/?learn=on&enablevpops=&autoplay=true&captions=spa)

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### Características previas al lanzamiento

* [Editor universal - Fragmentos de formulario](/help/edge/docs/forms/universal-editor/creating-form-fragments.md): El editor universal ahora le permite crear y reutilizar fragmentos de formulario para Formularios adaptables. Estos fragmentos son secciones de formulario reutilizables (por ejemplo, detalles de contacto, campos de consentimiento) que se pueden crear una vez y aplicar en varios formularios. Esta función optimiza la creación de formularios, garantiza la coherencia y mejora la eficacia de la creación.

* [Biblioteca de documentos de SharePoint - Guardar archivos adjuntos con nombres de archivo originales](/help/forms/connect-forms-to-sharepoint-document-library.md#connect-an-adaptive-form-to-microsoft-sharepoint-document-library): ahora tiene la opción de guardar los archivos adjuntos del formulario utilizando sus nombres de archivo originales al almacenarlos en una biblioteca de documentos de SharePoint. Esta mejora simplifica la identificación y administración de los archivos cargados.

* **Editor de reglas**:
   * [Condición binaria con evento de clic en la cláusula &quot;When&quot;](/help/forms/rule-editor-core-components-events-operators.md#available-operator-types-and-events-in-rule-editor): El editor de reglas ahora permite combinar un evento de clic en botón (_Se hace clic_) con otras condiciones dentro de la cláusula &quot;When&quot;. Esto permite un control más preciso de la ejecución de reglas en función de la interacción del usuario y otros factores. Nota: Cuando se utilizan varias condiciones, el evento de clic debe ser la primera condición de la lista.
   * [Condiciones de validación para campos y paneles](/help/forms/rule-editor-core-components-usecases.md): el editor de reglas ahora incluye las condiciones _IsValid_ y _IsNotValid_. Esto le permite comprobar el estado de validación de campos específicos o paneles completos (incluidos diseños como pestañas horizontales, pestañas verticales, acordeones y asistentes), lo que facilita la navegación mejorada del formulario y la experiencia del usuario basada en los resultados de validación.
* [Administración de ámbito mejorada para listas de SharePoint](/help/forms/connect-forms-to-sharepoint-list.md): Los sitios de SharePoint ahora admiten todas las rutas administradas, por ejemplo, /sitios y /equipos. Esta mejora permite una integración más amplia en varias estructuras del sitio de SharePoint, lo que ofrece una mayor flexibilidad para conectarse al contenido de la organización.
* [Compatibilidad para guardar documentos de registro en listas de SharePoint](/help/forms/generate-document-of-record-core-components.md#bind-adaptive-form-components-with-template-fields): Formularios creados mediante un modelo de datos de formulario (FDM) basado en listas de SharePoint ahora pueden guardar el documento de registro (DoR) en listas de SharePoint configurando la propiedad de campo Referencia de enlace de documento de registro. Esta mejora permite la integración perfecta de los datos de formulario y los documentos compatibles con el almacenamiento de SharePoint.

### Funciones de acceso rápido de AEM Forms {#forms-new-early-access-features}

El programa para acceso rápido de AEM Forms ofrece una oportunidad única de obtener acceso exclusivo a innovaciones punteras y ayudar a dar forma a su desarrollo.

En estas notas de la versión se indican las innovaciones de la versión actual. Para ver la lista completa de innovaciones disponibles en el programa para acceso rápido, consulte la [documentación del programa de acceso rápido de AEM Forms](/help/forms/early-access-ea-features.md).

#### Integración de Adobe Experience Platform (AEP) con Forms

Las funcionalidades de integración entre Forms y AEP ya están disponibles para los usuarios que las adoptaron por primera vez.

## [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation {#foundation}

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

El tiempo de ejecución de **Java 11** ya está en desuso, y la mayoría de los entornos ya se han actualizado al tiempo de ejecución de **Java 21** con mayor rendimiento.

Si su entorno no se ha podido actualizar debido a dependencias no admitidas (consulte [Requisitos de tiempo de ejecución de Java 21](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md#runtime-requirements)), debería haber recibido un correo electrónico de Adobe con los siguientes pasos específicos. Asegúrese de que todas las actualizaciones requeridas se hayan completado el **28 de agosto de 2025** para que su entorno se pueda actualizar sin interrupciones.

Nota: La versión del tiempo de ejecución es independiente de la versión de compilación del código. Aunque recomendamos la compilación con Java 21, las compilaciones de Java 11 siguen siendo compatibles por ahora. En el futuro, se publicará un aviso independiente sobre el desuso de compilaciones de Java 11.

### Aplicación de la directiva de configuración de registros Java de AEM {#logconfig-policy}

Como se indica en las notas de la versión de abril, los registros Java de AEM deben seguir un formato estándar para garantizar una monitorización de confianza en todos los entornos de clientes. Ya no se admiten las configuraciones de registro personalizadas, como los cambios en el formato de los registros, archivos de salida o niveles de registro predeterminados. Los registros deben permanecer dirigidos a los archivos predeterminados y se deben conservar los niveles de registro predeterminados para el código de producto de AEM. Consulte todos los detalles en el [Artículo de registro](/help/implementing/developing/introduction/logging.md#configuration-loggers).

A partir de **finales de agosto**, se omitirán todas las invalidaciones de registro personalizadas no admitidas. En función de nuestro análisis, la mayoría de los clientes no se verán afectados y Adobe se pondrá en contacto directamente con cualquier cliente cuya configuración actual pueda verse afectada.

Revise y actualice cualquier proceso descendente que dependa del comportamiento de registro personalizado. Por ejemplo:

* Si el sistema de reenvío de registros espera un formato de registro personalizado, es posible que tenga que ajustar las reglas de ingesta.
* Si anteriormente ha reducido los detalles de los registros cambiando los niveles de registro, tenga en cuenta que restablecer los niveles predeterminados podría aumentar el volumen del registro.

### Depuración predeterminada de versiones anteriores y registros de auditoría {#mt-defaults}

Actualmente, las versiones de contenido y los registros de auditoría tienen sus *tareas de mantenimiento de depuración* asociadas deshabilitadas de forma predeterminada y, por lo tanto, no se eliminan datos a menos que se configuren explícitamente.

Sin embargo, para optimizar el rendimiento del repositorio, a partir de **finales de junio de 2025**, la depuración se habilitará de manera predeterminada, siguiendo estas directrices:

#### Versiones de contenido {#mt-content}

* **Nuevos entornos** (creados después de una fecha próxima (se comunicará más adelante)
   * Las versiones con una antigüedad de más de **30 días** se eliminarán periódicamente.
   * Se conservan las cinco versiones más recientes de los últimos 30 días, junto con la versión más reciente y la versión actual, independientemente de su antigüedad.

* **Entornos existentes** (creados antes de esta próxima fecha):
   * Las versiones con una antigüedad de más de **7 años** se eliminarán periódicamente.
   * Se conservan todas las versiones de los últimos 7 años.
   * Este alto umbral predeterminado evita la eliminación involuntaria de datos recientes. Sin embargo, se recomienda configurar valores más bajos para optimizar el rendimiento del repositorio.

* Puede modificar estos valores predeterminados mediante la configuración de YAML, implementada mediante la canalización de configuración.

#### Registro de auditoría {#mt-auditlogs}

* **Nuevos entornos** (creados después de una fecha próxima, que se comunicará por separado):
   * Se eliminarán periódicamente los registros de replicación, DAM y auditoría de páginas de más de **7 días**.
   * Todos los eventos se registran de forma predeterminada.

* **Entornos existentes** (creados antes de esta próxima fecha):
   * Se eliminarán periódicamente los registros de replicación, DAM y auditoría de páginas de más de **7 años**.
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
* Modificación del formato de las respuestas de API de terceros (y tal vez agregar las respuestas de varias API) antes de enviarlas al explorador
* Composición y muestra de HTML procesado por el servidor en Edge con contenido reunido de varios backend

Tenemos un número limitado de oportunidades disponibles para el envío de publicaciones de AEM o para proyectos de Edge Delivery Services para sitios de producción en directo. Si está interesado en participar o desea obtener más información, envíe un correo electrónico a [aemcs-edgecompute-feedback@adobe.com](mailto:aemcs-edgecompute-feedback@adobe.com) con una breve descripción de su caso de uso.

### Configuración de CDN para Edge Delivery Services (programa Beta) {#cdn-eds-beta}

La CDN administrada por Adobe ofrece opciones de configuración flexibles, tal como se describe en el [artículo de canalizaciones de configuración](/help/operations/config-pipeline.md#configurations). 

Ahora en versión beta, implemente una canalización de configuración para funciones que incluyan selectores de origen de CDN, transformaciones de respuesta y solicitud, etc. Póngase en contacto con [aemcs-cdn-config-adopter@adobe.com](mailto:aemcs-cdn-config-adopter@adobe.com) con los detalles de su caso de uso.

### Reenvío de registros de AEM a más destinos (programa Beta) {#log-forwarding-beta}

Aunque los registros se pueden descargar desde Cloud Manager, muchas organizaciones consideran beneficioso transmitir estos registros a un destino de registro preferido. AEM ya admite el reenvío de registros de AEM y CDN a Azure Blob Storage, Datadog, HTTPS, Elasticsearch (y OpenSearch) y Splunk. Esta función se ha configurado en forma de autoservicio e implementado usando la canalización de configuración.

Ahora en la versión beta, puede reenviar los registros de AEM a Amazon S3, Sumo Logic y a su propia cuenta de New Relic (no a la cuenta proporcionada por Adobe). Tenga en cuenta que los registros de AEM (incluido Apache/Dispatcher) son compatibles con los destinos de estos registros, pero no con los de CDN. Envíe un correo electrónico a [aemcs-logforwarding-beta@adobe.com](mailto:aemcs-logforwarding-beta@adobe.com) para obtener acceso.

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
