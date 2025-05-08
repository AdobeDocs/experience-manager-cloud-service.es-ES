---
title: Notas de la versión actuales de [!DNL Adobe Experience Manager] as a Cloud Service.
description: Notas de la versión actuales de [!DNL Adobe Experience Manager] as a Cloud Service.
mini-toc-levels: 1
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
feature: Release Information
role: Admin
source-git-commit: 31fac8e421e58146977222d699bac1c7cf3ee4e5
workflow-type: ht
source-wordcount: '1713'
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

La fecha de lanzamiento de la versión de funcionalidad actual de [!DNL Adobe Experience Manager] como [!DNL Cloud Service] (2025.4.0) es el viernes, 24 de abril de 2025. La próxima versión con funcionalidades (2025.5.0) está planificada para el 5 de junio de 2025.

## Notas de la versión de mantenimiento {#maintenance}

Puede encontrar las últimas notas de la versión de mantenimiento [aquí](/help/release-notes/maintenance/latest.md).

<!-- 

## Release Video {#release-video}

Have a look at the February 2025 Release Overview video for a summary of the features added in the 2025.2.0 release:

>[!VIDEO](https://video.tv.adobe.com/v/3440923?quality=12&captions=spa)

-->

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Nuevas funciones de Experience Manager Sites {#enhancements-sites}

**Nueva IU de administración del modelo de fragmento de contenido**

Para completar aún más la lista de nuevas interfaces de usuario del lado del cliente al trabajar con fragmentos de contenido de AEM, ahora hay una nueva interfaz de usuario de administrador disponible para los modelos de fragmentos de contenido. La nueva interfaz de usuario proporciona una vista de lista limpia y moderna que permite buscar modelos con filtros y que muestra etiquetas de modelo y qué fragmentos de contenido existen basados en un modelo determinado. La documentación se encuentra [aquí](/help/sites-cloud/administering/content-fragments/managing-content-fragment-models.md). 

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Dynamic Media (Scene7) {#dynamic-media-scene7}

**Dynamic Media (Scene7) no se admite en entornos de seguridad mejorada**

Dynamic Media (Scene7) en AEM as a Cloud Service no está preparado para HIPAA y no se puede utilizar en entornos de AEM en los que la seguridad mejorada esté habilitada.

A partir de la versión de abril de 2025 de AEM as a Cloud Service, una restricción técnica impide que Dynamic Media (Scene7) se configure en entornos con seguridad mejorada. Como resultado, la tarjeta de **Configuración de Dynamic Media** en **Herramientas** > **Cloud Services** ya no es visible en estos entornos.

Además, los clientes que utilizan AEM 6.5 deben tener en cuenta que la pila de Dynamic Media (Scene7) no está preparada para HIPAA.

### Dynamic Media Classic {#dynamic-media-classic}

**Creación de informes**

Desde abril de 2025, la pestaña Ancho de banda del panel de informes de Dynamic Media Classic ya no es compatible.

Véase [Ancho de banda y almacenamiento, tipos de informes](https://experienceleague.adobe.com/es/docs/dynamic-media-classic/using/setup/administration-setup#types-of-reports).


## Nuevas funcionalidades de la vista Recursos {#new-features-assets-view}

**Relaciones de recursos**

La vista de Assets ahora admite la visualización y edición de relaciones de recursos en un panel de detalles de recursos simplificado. Añada fácilmente relaciones como Origen y Derivado al contenido para que los usuarios puedan encontrar de forma más eficaz el contenido relevante principal.

![Ejemplo de relación de Recursos](/help/assets/assets/asset-relations-example.png)

**Comparar versiones de un recurso**

Ahora puede seleccionar y comparar rápidamente cualquier versión de un recurso con su última versión mediante la vista de Recursos.

![comparar versiones del recurso](/help/assets/assets/version-compare2.png)

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

## Complemento CIF {#cloud-services-cif}

### Mejoras {#enhancements-cif}

* Adición de la selección de variantes de producto para el tipo de datos de referencia de producto de CIF
* [Experimental]: JSON+LD en componentes principales de CIF en PDP
* [Experimental]: Capacidad de CIF para borrar la caché

### Correcciones de errores {#bug-fixes-cif}

* Corregir problema de búsqueda en el campo de producto
* El formato de la dirección URL del producto no funciona como se esperaba para #variant_sku
* No se pueden añadir más de 20 SKU al componente de lista de productos

## [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation {#foundation}

### API basadas en OpenAPI {#open-apis}

Los desarrolladores pueden integrar completamente las funciones de AEM as a Cloud Service en sus propias aplicaciones y herramientas. Las nuevas API de AEM as a Cloud Service siguen la especificación de OpenAPI, con el objetivo de ser coherentes, bien documentadas y fáciles de usar. Las credenciales de los extremos que requieren autenticación se generan creando proyectos de Adobe Developer Console y admiten OAuth Server-to-Server, Web App y Single Page App (SPA).

[Vea la lista completa](https://developer.adobe.com/experience-cloud/experience-manager-apis/#openapi-based-apis) de API basadas en OpenAPI, [obtenga más información](/help/implementing/developing/open-api-based-apis.md) y pruebe un [tutorial completo](https://experienceleague.adobe.com/es/docs/experience-manager-learn/cloud-service/aem-apis/openapis/invoke-api-using-oauth-s2s) que ilustra la configuración y el uso.

Vea este vídeo para aprender a configurar una API autenticada para su uso posterior:

>[!VIDEO](https://video.tv.adobe.com/v/3457510?quality=12&learn=on)

### Mejoras relacionadas con la configuración de CDN {#cdn-enhancements}

La CDN administrada por Adobe ofrece opciones de configuración flexibles, tal como se describe en el [artículo de la canalización de configuración](/help/operations/config-pipeline.md#configurations). Estas son algunas funciones recientes:

#### Incluir propiedades adicionales en los registros de CDN {#props-in-cdnlogs}

Útil para escenarios como la depuración y el análisis de datos, puede incluir más información en sus registros de CDN más allá de las propiedades predeterminadas estableciendo la acción `logProperty` en [transformaciones de solicitud y respuesta](/help/implementing/dispatcher/cdn-configuring-traffic.md#request-transformations).

#### Propiedades de región, continente y organización como condiciones coincidentes {#matching-conditions}

Las reglas de CDN ahora pueden coincidir en función de la región, el continente y la organización para casos de uso, incluidos el bloqueo del tráfico y las redirecciones. `clientRegion` y `clientContinent` aumentan `clientCountry`, que ya es compatible, para que coincida en función de la ubicación geográfica, mientras que `clientAsName` y `clientAsNumber` coinciden con los sistemas autónomos para identificar ISP, compañías o proveedores de la nube grandes. Obtenga más información sobre estas [propiedades de solicitud recientemente expuestas](/help/security/traffic-filter-rules-including-waf.md#condition-structure).

#### Establecer valor de cookie {#cookie-attributes}

Puede establecer atributos de cookies en [transformaciones de respuestas](/help/implementing/dispatcher/cdn-configuring-traffic.md#response-transformations).

### Compatibilidad con Java 21 {#java21}

A partir de la versión de enero, podrá crear código con Java 21 y Java 17. Puede obtener acceso a nuevas funciones como la coincidencia de patrones, clases selladas y varias mejoras de rendimiento. Para ver los pasos de configuración, incluida la actualización del proyecto Maven y las versiones de la biblioteca, consulte el artículo [Entorno de compilación](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md#using-java-support). 

El **entorno de ejecución** de Java 21 de mayor rendimiento se implementará automáticamente cuando se detecte una compilación de Java 17 o 21. Sin embargo, también recomendamos optar por el tiempo de ejecución de Java 21 para entornos creados con Java 11, enviando un correo electrónico a [aemcs-java-adopter@adobe.com](mailto:aemcs-java-adopter@adobe.com). Obtenga información sobre los [requisitos del tiempo de ejecución de Java 21](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md#runtime-requirements).

>[!IMPORTANT]
>
> El **entorno de ejecución** de Java 21 se implementó en sus entornos de desarrollo/RDE en febrero; se aplicará a sus entornos de ensayo/producción el **28 y 29 de abril**. Tenga en cuenta que **crear código** con Java 21 (o Java 17) es independiente del tiempo de ejecución de Java 21; debe realizar acciones explícitas para crear código con Java 21 (o Java 17).

### Aplicación de la directiva de configuración de registro de AEM {#logconfig-policy}

Para garantizar una monitorización eficaz de los entornos de los clientes, los registros de Java de AEM deben mantener un formato coherente y no deben anularse con configuraciones personalizadas. La salida de registro debe permanecer dirigida a los archivos predeterminados. Para el código de producto de AEM, se deben conservar los niveles de registro predeterminados. Sin embargo, es aceptable ajustar los niveles de registro para el código desarrollado por el cliente.

Para ello, no deben realizarse cambios en las siguientes propiedades OSGi:
* **Configuración del registro de Apache Sling** (PID: `org.apache.sling.commons.log.LogManager`) — *todas las propiedades*
* **Configuración del registrador de Apache Sling** (PID de fábrica: `org.apache.sling.commons.log.LogManager.factory.config`):
   * `org.apache.sling.commons.log.file`
   * `org.apache.sling.commons.log.pattern`

A mediados de mayo, AEM aplicará una directiva en la que se ignorarán las modificaciones personalizadas a estas propiedades. Revise y ajuste sus procesos descendentes en consecuencia. Por ejemplo, si utiliza la función de reenvío de registros:
* Si el destino de registro espera un formato de registro personalizado (no predeterminado), es posible que tenga que actualizar las reglas de ingesta.
* Si los cambios en los niveles de registro reducen la cantidad de registros, tenga en cuenta que los niveles de registro predeterminados pueden provocar un aumento significativo del volumen de registros.

### Reenvío de registros de AEM a más destinos: programa Beta {#log-forwarding-earlyadopter}

Ahora en la versión Beta, puede reenviar los registros de AEM a New Relic (mediante HTTPS), Amazon S3 y Sumo Logic. Tenga en cuenta que los registros de AEM (incluido Apache/Dispatcher) son compatibles, los de CDN, no. Envíe un correo electrónico a [aemcs-logforwarding-beta@adobe.com](mailto:aemcs-logforwarding-beta@adobe.com) para obtener acceso.

Aunque los registros se pueden descargar desde Cloud Manager, muchas organizaciones consideran beneficioso transmitir estos registros a un destino de registro preferido. AEM ya admite (GA) el reenvío de registros de AEM y CDN a Azure Blob Storage, Datadog, HTTPS, Elasticsearch (y OpenSearch) y Splunk. Esta función se ha configurado en forma de autoservicio e implementado usando la canalización de configuración.

Obtenga más información en la [documentación de reenvío de registros](/help/implementing/developing/introduction/log-forwarding.md).

### Edge Computing: solicitud de comentarios {#edge-computing-feedback}

Edge Computing acerca el procesamiento de datos al explorador, lo que ofrece ventajas como una menor latencia. A Adobe le encantaría saber si esta tecnología le resulta útil para los proyectos de AEM Publish Delivery y Edge Delivery Services. Además, indíquenos para qué prevé utilizarla como aportación a la hoja de ruta del producto. 

Algunos casos de uso posibles son los siguientes:

* Autenticación con un IdP para acceder al contenido
* Personalización mediante representación de contenido dinámico en función de la geolocalización, el tipo de dispositivo, los atributos de usuario, etc.
* Manipulación avanzada de imágenes
* Middleware entre la CDN y un origen
* Una capa entre el explorador y una API de terceros, tal vez para cambiar el formato de la respuesta de la API
* Añadir datos de varios orígenes para que el explorador del cliente pueda procesarlos con mayor facilidad

Envíe un correo electrónico a [aemcs-edgecompute-feedback@adobe.com](mailto:aemcs-edgecompute-feedback@adobe.com) con preguntas y comentarios.

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
