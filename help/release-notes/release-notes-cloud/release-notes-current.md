---
title: Notas de la versión actuales de [!DNL Adobe Experience Manager] as a Cloud Service.
description: Notas de la versión actuales de [!DNL Adobe Experience Manager] as a Cloud Service.
mini-toc-levels: 1
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
feature: Release Information
role: Admin
source-git-commit: 5a1c951813e026806aa3b5b23a912a48681f4505
workflow-type: tm+mt
source-wordcount: '1072'
ht-degree: 76%

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

La fecha de la versión de [!DNL Adobe Experience Manager] como versión de funcionalidad actual (2025.3.0) de [!DNL Cloud Service] es el viernes, 27 de marzo de 2025. La próxima versión con funcionalidades (2025.4.0) está planificada para el viernes, 24 de abril de 2025.

## Notas de la versión de mantenimiento {#maintenance}

Puede encontrar las últimas notas de la versión de mantenimiento [aquí](/help/release-notes/maintenance/latest.md).

<!-- 

## Release Video {#release-video}

Have a look at the February 2025 Release Overview video for a summary of the features added in the 2025.2.0 release:

>[!VIDEO](https://video.tv.adobe.com/v/3440920?quality=12)

-->

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Nuevas funciones en Dynamic Media {#new-features-dynamic-media}

**Compatibilidad con formularios largos para vídeos entregados mediante Dynamic Media con API abierta**

Dynamic Media con OpenAPI ahora es compatible con vídeos de formularios largos. Los vídeos de formato largo pueden admitir hasta 50 GB y 2 horas.

### Nuevas funcionalidades de la vista Recursos {#new-features-assets-view}


**Compatibilidad con etiquetas raíz**

Ahora, AEM Assets admite la asignación de una propiedad de etiqueta en un formulario de metadatos a metadatos personalizados. Además, como administrador, puede restringir la disponibilidad de etiquetas a los usuarios restringiendo el acceso a una etiqueta raíz específica y a las etiquetas que existen bajo la etiqueta raíz.

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### Funciones de acceso rápido de AEM Forms {#forms-new-early-access-features}

El programa para acceso rápido de AEM Forms ofrece una oportunidad única de obtener acceso exclusivo a innovaciones punteras y ayudar a dar forma a su desarrollo.

En estas notas de la versión se indican las innovaciones de la versión actual. Para ver la lista completa de innovaciones disponibles en el programa para acceso rápido, consulte la [documentación del programa de acceso rápido de AEM Forms](/help/forms/early-access-ea-features.md).

#### Plantillas de correo electrónico HTML de los formularios adaptables

Los formularios adaptables le permiten utilizar [plantillas de correo electrónico HTML](/help/forms/html-email-templates-in-adaptive-forms.md). Las plantillas de correo electrónico HTML le permiten enviar correos electrónicos enriquecidos, personalizados y visualmente atractivos cuando se envía un formulario. Estos correos electrónicos se pueden personalizar con los datos del formulario y mejorar mediante varias etiquetas de correo electrónico, como imágenes y vínculos. Con los formularios adaptables, puede cargar un archivo que contenga una plantilla HTML o utilizar un editor de texto sin formato para crear estas plantillas.

![Plantilla de correo electrónico HTML](/help/forms/assets/html-email.png)

#### Compatibilidad mejorada con el almacenamiento en la nube: carga directa del PDF en el almacenamiento del blob de Azure

Las API de generación de documentos de AEM Forms ahora le permiten [cargar directamente los documentos PDF generados](/help/forms/early-access-ea-features.md#doc-generation-api) en Azure Blob Storage. Esta mejora optimiza el almacenamiento y la recuperación, mejorando la eficiencia y la integración con los flujos de trabajo en la nube.

## [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation {#foundation}

### Compatibilidad con Java 21 {#java21}

Como se menciona en la versión de enero, ahora puede generar código con Java 21, que incluye nuevas funciones (por ejemplo, coincidencia de patrones para instrucciones de cambio, clases selladas) y mejoras de rendimiento; las compilaciones de Java 17 también son compatibles desde hace poco. Para ver los pasos de configuración, incluida la actualización del proyecto Maven y las versiones de la biblioteca, consulte el artículo [Entorno de compilación](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md#using-java-support). 

El **entorno de ejecución** de Java 21 de mayor rendimiento se implementará automáticamente cuando se detecte una compilación de Java 17 o 21. Sin embargo, también recomendamos optar por el tiempo de ejecución de Java 21 para entornos creados con Java 11, enviando un correo electrónico a [aemcs-java-adopter@adobe.com](mailto:aemcs-java-adopter@adobe.com). Obtenga información sobre los [requisitos del tiempo de ejecución de Java 21](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md#runtime-requirements).

>[!IMPORTANT]
>
> Java 21 **runtime** se implementó en sus entornos de desarrollo/RDE en febrero; se aplicará a sus entornos de ensayo/producción el **28 y 29 de abril**. Tenga en cuenta que **crear código** con Java 21 (o Java 17) es independiente del tiempo de ejecución de Java 21; debe realizar explícitamente los pasos para generar código con Java 21 (o Java 17).

### Registro y reenvío de AEM a más destinos: programa Beta {#log-forwarding-earlyadopter}

Ahora en la versión beta, puede reenviar los registros de AEM a New Relic (mediante HTTPS), Amazon S3 y Sumo Logic. Tenga en cuenta que se admiten los registros de AEM (incluido Apache/Dispatcher), pero no los de CDN. Enviar correo electrónico a [aemcs-logforwarding-beta@adobe.com](mailto:aemcs-logforwarding-beta@adobe.com) para obtener acceso.

Aunque los registros se pueden descargar desde Cloud Manager, muchas organizaciones consideran beneficioso transmitir esos registros a un destino de registro preferido. AEM ya admite (GA) el reenvío de registros de AEM y CDN a Azure Blob Storage, Datadog, HTTPS, Elasticsearch (y OpenSearch) y Splunk. Esta función se configura en forma de autoservicio y se implementa mediante la canalización de configuración.

Obtenga más información en la [documentación de reenvío de registros](/help/implementing/developing/introduction/log-forwarding.md).

### Edge Computing: solicitud de comentarios {#edge-computing-feedback}

Edge Computing acerca el procesamiento de datos al explorador, lo que ofrece ventajas como una menor latencia. A Adobe le encantaría saber si esta tecnología le resulta útil para los proyectos de AEM Publish Delivery y Edge Delivery Services. Además, indíquenos para qué prevé utilizarla como aportación a la hoja de ruta del producto. 

Algunos casos de uso posibles son los siguientes:
* Autenticación con un IdP para acceder al contenido
* Representación de contenido dinámico (personalizado, localizado) en función de la geolocalización, el tipo de dispositivo, los atributos de usuario, etc.
* Manipulación avanzada de imágenes
* Middleware entre la CDN y un origen
* Una capa entre el explorador y una API de terceros, tal vez para cambiar el formato de la respuesta de la API
* Añadir datos de varios orígenes para que el explorador del cliente pueda procesarlos con mayor facilidad

Envíe un correo electrónico a [aemcs-edgecompute-feedback@adobe.com](mailto:aemcs-edgecompute-feedback@adobe.com) con preguntas y comentarios.

### API basadas en OpenAPI: programa para primeros usuarios {#open-apis-earlyadopter}

Los desarrolladores pueden integrar completamente las funciones de AEM as a Cloud Service en sus propias aplicaciones y herramientas. Las nuevas API de AEM as a Cloud Service siguen la especificación de OpenAPI, con el objetivo de ser coherentes, bien documentadas y fáciles de usar. Las credenciales de los puntos finales que requieren autenticación se generarán creando proyectos de Adobe Developer Console.

Obtenga más información sobre las [API de AEM basadas en OpenAPI](/help/implementing/developing/open-api-based-apis.md) y realice un [tutorial completo](https://experienceleague.adobe.com/es/docs/experience-manager-learn/cloud-service/aem-apis/invoke-openapi-based-aem-apis) que ilustra la configuración y el uso.

En concreto, los puntos finales de API que se enumeran a continuación están disponibles como parte de un programa para primeros usuarios. Si está interesado, envíe un correo electrónico a [aem-apis@adobe.com](mailto:aem-apis@adobe.com) describiendo cómo piensa utilizarlos.

* [API de fragmentos de contenido en Sites](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/sites/)
* [API de recursos](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/assets/author/)
* [API de Sites y carpetas de recursos](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/folders/)
* [API de comunicaciones de formularios](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/)

### Nuevo AEM Developer Console (Beta pública) {#aem-developer-console-beta}

Pruebe la [AEM Developer Console](/help/implementing/developing/introduction/aem-developer-console.md) rediseñada, que ofrece una experiencia más interactiva para depurar código en entornos de la nube.

Cualquiera puede acceder a la versión beta pública haciendo clic en el botón *Nueva consola disponible* en la versión actual de AEM Developer Console. Adobe agradece sus comentarios, que puede enviar por correo electrónico a [aemcs-new-devconsole-ui-beta@adobe.com](mailto:aemcs-new-devconsole-ui-beta@adobe.com).

## Guías de [!DNL Experience Manager] {#guides}

Puede encontrar una lista completa de las funciones nuevas y mejoradas de la última versión de Adobe Experience Manager Guides [aquí](https://experienceleague.adobe.com/es/docs/experience-manager-guides/using/release-info/release-notes/cloud-release-notes/2024-releases/2410-release/2410-0-release/whats-new-2024-10-0).

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
