---
title: Notas de la versión 2025.6.0 de la versión de  [!DNL Adobe Experience Manager]  as a Cloud Service.
description: Notas de la versión 2025.6.0 de la versión de  [!DNL Adobe Experience Manager]  as a Cloud Service.
feature: Release Information
role: Admin
exl-id: 6bd35c41-4caf-481c-8cf5-b739307e70da
source-git-commit: 92077a34aa02daf177ca760dafca1a6190a8acb8
workflow-type: tm+mt
source-wordcount: '1363'
ht-degree: 99%

---

# Notas de la versión 2025.6.0 para [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

En la siguiente sección se describen las notas de la versión de funciones de la versión 2025.6.0 de [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Desde aquí puede navegar hasta las notas de la versión de versiones anteriores, como 2023 o 2024.
>
>Eche un vistazo a la [Hoja de ruta de versiones de Experience Manager](https://experienceleague.adobe.com/es/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap) para obtener más información acerca de las próximas activaciones de funcionalidades para [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Para recibir una notificación mensual por correo electrónico acerca de las actualizaciones realizadas en las notas de la versión de Experience Cloud, suscríbase a las [actualizaciones prioritarias de productos de Adobe](https://www.adobe.com/subscription/priority-product-update.html).

## Fecha de lanzamiento {#release-date}

La fecha de lanzamiento de la versión de funcionalidad actual de [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] (2025.6.0) fue el 26 de junio de 2025. La próxima versión con funcionalidades (2025.7.0) está planificada para el 7 de agosto de 2025.

## Notas de la versión de mantenimiento {#maintenance}

Puede encontrar las últimas notas de la versión de mantenimiento [aquí](/help/release-notes/maintenance/latest.md).

## Vídeo de la versión {#release-video}

Eche un vistazo al vídeo Información general sobre la versión de junio de 2025 para ver un resumen de las funciones añadidas en la versión 2025.6.0.

>[!VIDEO](https://video.tv.adobe.com/v/3470881?quality=12&captions=spa)

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

**Administración mejorada de formularios de metadatos en la vista Assets**

Ahora puede importar formularios de metadatos de la vista Administrador directamente a la vista Assets. Cualquier actualización realizada en estos formularios en la vista Assets se reflejará automáticamente en la vista Administración, lo que garantiza la coherencia en ambas experiencias. Esta capacidad permite una transición sin problemas a la nueva vista Assets, a la vez que mantiene la continuidad con las configuraciones de metadatos existentes.

![Metadatos generados por IA](/help/assets/assets/import-metadata-forms-page.png)

### Nuevas funciones en el centro de contenido {#new-features-content-hub}

**Control de colecciones**

Content Hub ahora le permite [controlar el acceso a las colecciones durante la creación, asegurando así que solo los usuarios autorizados puedan ver o administrar los recursos agrupados](/help/assets/collections-content-hub.md##create-collections). Garantiza una mayor seguridad, una mejor colaboración, una administración de recursos organizada y un control simplificado.

>[!VIDEO](https://video.tv.adobe.com/v/3463336)

## [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation {#foundation}

### Proceso de desuso actualizado {#updated-deprecation-process}

Adobe revisa regularmente las funciones, bibliotecas, API y configuraciones para asegurarse de que cumplen los estándares de rendimiento, seguridad y valor. Cuando las funciones ya no cumplen estos estándares, se marcan para proceder a su desuso y se informa de que su uso dejará de estar disponible en una fecha de eliminación especificada. Antes de esta fecha, Adobe se lo recordará a los clientes mediante notificaciones por correo electrónico, y les indicará las acciones que deben realizar en Cloud Manager antes de continuar con la implementación de nuevas compilaciones. Si no se llevan a cabo las acciones necesarias, es posible que no se pueda realizar la actualización a las nuevas versiones de AEM, lo que podría tener un impacto negativo en la seguridad, el rendimiento, la fiabilidad y la disponibilidad.

Consulte el [artículo sobre el proceso de desuso](/help/release-notes/deprecated-removed-features.md) para obtener más información.

#### API de Java y configuración de OSGi en desuso próximas a las fechas de eliminación {#deprecated-near-removals}

Amplíe la lista siguiente para ver las API y las configuraciones de OSGi en desuso que deben dejar de usarse. Para obtener información detallada (incluidas las fechas de eliminación), consulte el artículo sobre el proceso de desuso.

+++Amplíe para ver qué va a quedar en desuso

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

+++

### Desuso de tiempo de ejecución de Java 11 {#java11-runtime-deprecation}

El tiempo de ejecución de **Java 11** ya está en desuso, y la mayoría de los entornos ya se han actualizado al tiempo de ejecución de **Java 21** con mayor rendimiento.

Si su entorno no se ha podido actualizar debido a dependencias no admitidas (consulte [Requisitos de tiempo de ejecución de Java 21](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md#runtime-requirements)), debería haber recibido un correo electrónico de Adobe con los siguientes pasos específicos. Asegúrese de que todas las actualizaciones requeridas se hayan completado el **28 de agosto de 2025** para que su entorno se pueda actualizar sin interrupciones.

Nota: La versión del tiempo de ejecución es independiente de la versión de compilación del código. Aunque recomendamos la compilación con Java 21, las compilaciones de Java 11 siguen siendo compatibles por ahora. En el futuro, se publicará un aviso independiente sobre el desuso de compilaciones de Java 11.

### Aplicación de la directiva de configuración de registros Java de AEM {#logconfig-policy}

Como se indica en las notas de la versión de abril, los registros Java de AEM deben seguir un formato estándar para garantizar una monitorización de confianza en todos los entornos de clientes. Ya no se admiten las configuraciones de registro personalizadas, como los cambios en el formato de los registros, archivos de salida o niveles de registro predeterminados. Los registros deben permanecer dirigidos a los archivos predeterminados y se deben conservar los niveles de registro predeterminados para el código de producto de AEM. Consulte todos los detalles en el [Artículo de registro](/help/implementing/developing/introduction/logging.md#configuration-loggers).

A partir de **finales de agosto**, se omitirán todas las invalidaciones de registro personalizadas no admitidas. Según nuestro análisis, la mayoría de los clientes no se verán afectados y Adobe se pondrá en contacto directamente con cualquier cliente cuya configuración actual pueda verse afectada.

Revise y actualice cualquier proceso descendente que dependa del comportamiento de registro personalizado. Por ejemplo:

* Si el sistema de reenvío de registros espera un formato de registro personalizado, es posible que tenga que ajustar las reglas de ingesta.
* Si anteriormente ha reducido los detalles de los registros cambiando los niveles de registro, tenga en cuenta que restablecer los niveles predeterminados podría aumentar el volumen del registro.

### Depuración predeterminada de versiones anteriores y registros de auditoría {#mt-defaults}

Actualmente, las versiones de contenido y los registros de auditoría tienen sus *tareas de mantenimiento de depuración* asociadas deshabilitadas de forma predeterminada y, por lo tanto, no se eliminan datos a menos que se configuren explícitamente.

Sin embargo, para optimizar el rendimiento del repositorio, a partir de **principios de julio de 2025**, la depuración se habilitará de manera predeterminada, siguiendo estas directrices:

#### Versiones de contenido {#mt-content}

* **Nuevos entornos** (creados después de una fecha próxima para ser comunicados más adelante)
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
* Modificar el formato de las respuestas de API de terceros (y tal vez añadir las respuestas de varias API) antes de enviarlas al explorador
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
