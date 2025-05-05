---
title: Notas de la versión 2025.2.0 de la versión de  [!DNL Adobe Experience Manager]  as a Cloud Service.
description: Notas de la versión 2025.2.0 de la versión de  [!DNL Adobe Experience Manager]  as a Cloud Service.
feature: Release Information
role: Admin
source-git-commit: 43a9b29132aca8f5231634b845c55538b59f5ee4
workflow-type: tm+mt
source-wordcount: '1500'
ht-degree: 100%

---

# Notas de la versión 2025.2.0 para [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

En la siguiente sección se describen las notas de la versión de funciones de la versión 2025.2.0 de [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Desde aquí puede navegar hasta las notas de la versión de versiones anteriores, como 2023 o 2024.
>
>Eche un vistazo a la [Hoja de ruta de versiones de Experience Manager](https://experienceleague.adobe.com/es/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap) para obtener más información acerca de las próximas activaciones de funcionalidades para [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Para recibir una notificación mensual por correo electrónico acerca de las actualizaciones realizadas en las notas de la versión de Experience Cloud, suscríbase a las [actualizaciones prioritarias de productos de Adobe](https://www.adobe.com/subscription/priority-product-update.html).

## Fecha de lanzamiento {#release-date}

La fecha de la versión de [!DNL Adobe Experience Manager] como versión de funcionalidad actual (2025.2.0) de [!DNL Cloud Service] es el 4 de marzo de 2025. La próxima versión de funcionalidad (2025.3.0) está planificada para el 27 de marzo de 2025.

## Notas de la versión de mantenimiento {#maintenance}

Puede encontrar las últimas notas de la versión de mantenimiento [aquí](/help/release-notes/maintenance/latest.md).

<!-- 

## Release Video {#release-video}

Have a look at the February 2025 Release Overview video for a summary of the features added in the 2025.2.0 release:

>[!VIDEO](https://video.tv.adobe.com/v/3440923?quality=12&captions=spa)

-->

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Nuevas funciones de AEM Sites {#new-features-sites}

**Etiquetado automático de los fragmentos de contenido**

Al crear fragmentos de contenido, ahora es posible heredar automáticamente las etiquetas asignadas al modelo de contenido. Esto permite realizar una potente clasificación automática del contenido almacenado en los fragmentos de contenido.

**Compatibilidad con UUID de los fragmentos de contenido**

La compatibilidad con UUID de los fragmentos de contenido ya tiene disponibilidad general (GA). La nueva funcionalidad no altera el comportamiento basado en las rutas de las operaciones dentro de AEM como mover, cambiar el nombre y desplegar. Las rutas se ajustan automáticamente, pero puede hacer que el consumo externo de fragmentos de contenido sea más fácil y estable, especialmente cuando se utilizan consultas GraphQL que se dirigen directamente a fragmentos individuales con consultas ByPath. Estas consultas pueden interrumpirse si cambia una ruta de fragmento. Al utilizar el nuevo tipo de consulta ById, la consulta ahora permanece estable, ya que el UUID de un fragmento no cambia en los casos en que sí lo hacen las rutas.

**Compatibilidad de Dynamic Media con OpenAPI en el Editor de fragmentos de contenido y GraphQL**

Los recursos que se almacenan en programas de AEM as a Cloud Service diferentes a los fragmentos de contenido y que se habilitan con la nueva funcionalidad Dynamic Media con OpenAPI, ahora se pueden utilizar en los fragmentos de contenido. El selector de imágenes en el nuevo Editor de fragmentos de contenido ahora permite seleccionar repositorios &quot;remotos&quot; como fuente para los recursos de imagen a los que se hace referencia en el fragmento. Además, en el envío de estos fragmentos de contenido mediante AEM GraphQL, la respuesta JSON ahora incluye propiedades necesarias para los recursos remotos (assetId, repositoryId), de modo que las aplicaciones cliente puedan crear direcciones URL de Dynamic Media con OpenAPI para recuperar la imagen.

**Despliegue del editor de fragmentos de contenido**

Seguiremos habilitando el nuevo editor de fragmentos de contenido basado en la IU de Spectrum en AEM as a Cloud Service. Después de convertirse en el valor predeterminado para todos los entornos de Cloud Service Developer en noviembre de 2024, se establecerá como valor predeterminado para todos los entornos de ensayo el 1 de abril de 2025, y para todos los entornos de producción el 1 de mayo de 2025. En todos los casos, los usuarios seguirán teniendo la opción de volver al editor de fragmentos de contenido tradicional en la IU táctil de AEM.

**API HTTP de traducción**

La API REST HTTP de traducción de AEM que ha estado en modo de primer usuario durante un tiempo ahora ya tiene disponibilidad general (GA). La documentación se encuentra [aquí](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/translation/). La API permite automatizar los pasos necesarios en el proceso de administración de traducciones para el contenido en AEM.

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Nuevas funciones de AEM Assets {#new-features-assets}

**Nueva estructura de empaquetado de Dynamic Media**

Ya está disponible una estructura de empaquetado de Dynamic Media actualizada para cumplir mejor con las expectativas del mercado y facilitar el seguimiento. La nueva estructura de empaquetado incluye lo siguiente:

* Dynamic Media Prime, que incluye Dynamic Media con OpanAPIs y vídeo para mejorar el envío.

* Dynamic Media Ultimate añade funciones de envío y transformación para satisfacer requisitos de uso más exigentes.

Debe tener Assets as a Cloud Service Prime o Ultimate para beneficiarse de la nueva estructura de empaquetado.

**Subtítulos de vídeo generados por IA**

Los subtítulos de vídeo generados por IA en Adobe Dynamic Media utilizan la inteligencia artificial para generar subtítulos automáticamente para el contenido de vídeo. Esta función se ha diseñado para mejorar la accesibilidad y la experiencia del usuario gracias a la provisión de subtítulos precisos. Los subtítulos se generan a partir del audio original, de cualquier pista de audio adicional o de subtítulos adicionales proporcionados en la pestaña &quot;Subtítulos y audio&quot; de la página de propiedades del vídeo. Con compatibilidad con más de 60 idiomas, los subtítulos se pueden revisar y previsualizar antes de publicar el vídeo.

**Filtros de búsqueda personalizados**

Los filtros de búsqueda personalizados mejoran la precisión y la eficacia de la búsqueda de información relevante. Permiten realizar búsquedas más adaptadas y filtrar los datos según atributos específicos como la marca, el producto, la categoría u otros identificadores clave. Esto mejora la organización, reduce el tiempo dedicado a buscar entre los resultados irrelevantes y permite tomar decisiones más rápidamente. También admiten la escalabilidad, ya que los conjuntos de datos grandes son más fáciles de navegar y analizar.

![filtros de búsqueda personalizados](/help/assets/assets/custom-search-filters.png)

### Funciones de acceso rápido de Content Hub {#early-access-content-hub}

Content Hub ahora le permite ver y descargar representaciones dinámicas y de recorte inteligente, además de las representaciones estáticas existentes. Como administrador de Content Hub, también puede configurar la disponibilidad de estas representaciones para los usuarios mediante la interfaz de usuario de configuración.

![representaciones dinámicas](/help/assets/assets/download-single-asset-renditions-dynamic.png)

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
> En febrero, Java 21 **runtime** se implementó en entornos para desarrolladores/RDE (aparte de los ya creados con Java 17 o 21, que ya tienen Java 21 runtime). Java 21 se aplicará a los entornos de ensayo/producción en abril.

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
