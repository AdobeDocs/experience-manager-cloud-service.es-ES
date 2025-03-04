---
title: Notas de la versión 2025.1.0 de la versión de  [!DNL Adobe Experience Manager]  as a Cloud Service.
description: Notas de la versión 2025.1.0 de la versión de  [!DNL Adobe Experience Manager]  as a Cloud Service.
feature: Release Information
role: Admin
source-git-commit: f899398182f9d0991123828ca217379653a4e397
workflow-type: tm+mt
source-wordcount: '1513'
ht-degree: 87%

---

# Notas de la versión 2025.1.0 para [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

En la siguiente sección se describen las notas de la versión de funciones de la versión 2025.1.0 de [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Desde aquí puede navegar hasta las notas de la versión de versiones anteriores, como 2023 o 2024.
>
>Eche un vistazo a la [Hoja de ruta de versiones de Experience Manager](https://experienceleague.adobe.com/es/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap) para obtener más información acerca de las próximas activaciones de funcionalidades para [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Para recibir una notificación mensual por correo electrónico acerca de las actualizaciones realizadas en las notas de la versión de Experience Cloud, suscríbase a las [actualizaciones prioritarias de productos de Adobe](https://www.adobe.com/subscription/priority-product-update.html).

## Fecha de lanzamiento {#release-date}

La fecha de la versión de [!DNL Adobe Experience Manager] como versión de funcionalidad actual (2025.1.0) de [!DNL Cloud Service] es el 30 de enero de 2025. La próxima versión de funcionalidad (2025.2.0) está planificada para el 4 de marzo de 2025.

## Notas de la versión de mantenimiento {#maintenance}

Puede encontrar las últimas notas de la versión de mantenimiento [aquí](/help/release-notes/maintenance/latest.md).

<!-- 

## Release Video {#release-video}

Have a look at the January 2025 Release Overview video for a summary of the features added in the 2025.1.0 release:

>[!VIDEO](https://video.tv.adobe.com/v/3440920?quality=12)

-->

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

**Los comentarios del editor de fragmentos de contenido ya están disponibles de forma generalizada**

Colabore fácilmente con sus compañeros de trabajo para crear fragmentos de contenido de AEM mediante el uso del servicio de comentarios nuevos y modernizados en el Editor de fragmentos de contenido de AEM.
[Más información](https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/sites/administering/content-fragments/authoring?#commenting-on-your-fragment).

**Editor de fragmentos de contenido e interfaces de usuario de administración: compatibilidad actualizada con la versión de AEM as a Cloud Service**

La versión mínima de AEM as a Cloud Service compatible con las nuevas interfaces de usuario de Administrador y Editor de fragmentos de contenido es ahora 2023.8.13099. Las versiones anteriores a la versión de disponibilidad general de las nuevas interfaces de usuario ya no serán compatibles

### Programa para primeros usuarios {#sites-early-adopter}

**Fragmentos de contenido mejorados**

Se han mejorado las [referencias a fragmentos de contenido con referencias basadas en ID únicos](/help/headless/graphql-api/uuid-reference-upgrade.md), lo que ayuda a garantizar que las consultas de GraphQL de fragmentos de contenido individuales puedan permanecer estables incluso si el fragmento se movió a otra ubicación. Esto ahora es posible con las consultas &quot;ByID&quot;. Aunque las rutas pueden cambiar, lo que potencialmente rompe las consultas &quot;ByPath&quot;, los UUID son estables. Los nuevos ID también se pueden devolver como propiedades en cualquier consulta u otra solicitud de API aplicable. Limitación actual (2025.1): las referencias de página aún no son compatibles con ID únicos. Si se hace referencia a las páginas en los fragmentos de contenido, esta función no debe utilizarse. Se prevé eliminar esta limitación en la próxima versión de AEM as a Cloud Service.

**AEM REST OpenAPI para la entrega de fragmentos de contenido**

[AEM REST OpenApi para la entrega de fragmentos de contenido](/help/headless/aem-rest-openapi-content-fragment-delivery.md) ya está disponible para AEM as a Cloud Service.

### Funciones en desuso {#sites-deprecated}

#### Editor de SPA  {#spa-editor}

El [Editor de SPA](/help/implementing/developing/hybrid/introduction.md) ha quedado obsoleto para nuevos proyectos a partir de la versión 2025.1.0. El editor de SPA sigue siendo compatible con los proyectos existentes, pero no debe utilizarse en nuevos proyectos.

Los editores preferidos para administrar contenido sin encabezado en AEM ahora son:

* [El editor universal](/help/edge/wysiwyg-authoring/authoring.md) para la edición visual.
* [El editor de fragmentos de contenido](/help/assets/content-fragments/content-fragments-managing.md) para la edición de contenido sin encabezado basada en formularios.

#### Funciones de PWA {#pwa-features}

[Las características de la aplicación web progresiva (PWA)](/help/sites-cloud/authoring/sites-console/enable-pwa.md) para AEM Sites ya no se utilizan en los nuevos proyectos que comiencen con la versión 2025.1.0. Esta función sigue siendo compatible con los proyectos existentes, pero no debe utilizarse para nuevos proyectos

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Nuevas funciones de la vista AEM Assets {#new-features-assets}

**Personalizar filtros de búsqueda**

Los filtros de búsqueda personalizada mejoran la precisión y la eficacia de la búsqueda de información relevante. Permite realizar búsquedas más adaptadas y filtrar los datos según atributos específicos como marca, producto, categoría u otros identificadores clave. Esto mejora la organización, reduce el tiempo empleado en tamizar los resultados irrelevantes y permite una toma de decisiones más rápida. También admite la escalabilidad, ya que los conjuntos de datos grandes son más fáciles de navegar y analizar.

![filtros de búsqueda personalizados](/help/assets/assets/custom-search-filters.png)

### Nuevas funciones en Content Hub {#new-features-content-hub}

Descripción

### Funciones de acceso rápido de AEM Assets {#early-access-features-assets}

**Subtítulos de vídeo generados por IA**

Los subtítulos de vídeo generados por IA en Adobe Dynamic Media utilizan la inteligencia artificial para generar subtítulos automáticamente para el contenido de vídeo. Esta función está diseñada para mejorar la accesibilidad y la experiencia del usuario gracias a la provisión de subtítulos precisos en tiempo real. Los subtítulos se generan a partir del audio original, de cualquier pista de audio adicional o de los subtítulos adicionales proporcionados en la pestaña &quot;Subtítulos y audio&quot; de la página de propiedades del vídeo. Con compatibilidad con más de 60 idiomas, los subtítulos se pueden revisar y previsualizar antes de publicar el vídeo.

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### Nuevas funciones en AEM Forms {#forms-new-features}

* **Administrar publicación**: puede usar el flujo de trabajo [Administrar publicación](/help/forms/manage-publication.md#publish-forms-using-the-manage-publication-option)) para publicar o cancelar la publicación de formularios en entornos, generalmente desde la instancia de autor a las instancias de publicación y vista previa. Permite a los usuarios publicar, cancelar la publicación o programar la publicación de contenido de una manera optimizada.

* **[Guardar automáticamente un borrador para formularios adaptables basados en componentes principales](/help/forms/save-core-component-based-form-as-draft.md)**: los usuarios ahora pueden beneficiarse de una función de guardado automático que guarda automáticamente un formulario parcialmente completado como borrador. Pueden volver más tarde para terminar de rellenarlo en el mismo dispositivo o en otro distinto. Esta función mejora las tasas de conversión para las organizaciones al reducir el abandono de formularios, ya que los usuarios no tienen que volver a empezar a rellenar el formulario desde el principio.

* **[Mejoras en el editor de reglas](/help/forms/invoke-service-enhancements-rule-editor.md)**: para Forms adaptable basado en componentes principales, puede usar la salida de Invocar servicio para rellenar opciones desplegables y establecer paneles repetibles o individuales. Además, este resultado se puede utilizar para validar otros campos.

* **[Mejorar la experiencia del usuario con botones de navegación en los diseños de panel](/help/forms/rule-editor-core-components-usecases.md#navigating-among-panels-using-button)**: ahora puede añadir botones de navegación a los diseños de panel, como Pestañas horizontales, Pestañas verticales, Acordeones o el Asistente. Estos botones mejoran la experiencia del usuario al simplificar las transiciones entre paneles y se centran en el panel seleccionado.


### Funciones de acceso rápido de AEM Forms {#forms-new-early-access-features}

El programa para acceso rápido de AEM Forms ofrece una oportunidad única de obtener acceso exclusivo a innovaciones punteras y ayudar a dar forma a su desarrollo.

En estas notas de la versión se indican las innovaciones de la versión actual. Para ver la lista completa de innovaciones disponibles en el programa para acceso rápido, consulte la [documentación del programa de acceso rápido de AEM Forms](/help/forms/early-access-ea-features.md).

#### [Plantillas de correo electrónico de HTML en Forms adaptable](/help/forms/html-email-templates-in-adaptive-forms.md)

El Forms adaptable permite utilizar plantillas de correo electrónico de HTML. Las plantillas de correo electrónico HTML le permiten enviar correos electrónicos enriquecidos, personalizados y visualmente atractivos cuando se envía un formulario. Estos correos electrónicos se pueden personalizar con los datos del formulario y mejorar mediante varias etiquetas de correo electrónico, como imágenes y vínculos. Con los formularios adaptables, puede cargar un archivo que contenga una plantilla HTML o utilizar un editor de texto sin formato para crear estas plantillas.

![Plantilla de correo electrónico HTML](/help/forms/assets/html-email.png)

#### Compatibilidad mejorada con el almacenamiento en la nube: carga directa del PDF en el almacenamiento del blob de Azure

Las API de generación de documentos de AEM Forms ahora admiten la carga directa de documentos de PDF generados al almacenamiento del blob de Azure. Esta mejora optimiza el almacenamiento y la recuperación, mejorando la eficiencia y la integración con los flujos de trabajo en la nube.

## [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation {#foundation}

### Compatibilidad con Java 21 {#java21}

Ahora puede generar código con Java 21, que incluye nuevas funciones (por ejemplo, coincidencia de patrones para instrucciones de cambio, clases selladas) y mejoras de rendimiento; las compilaciones de Java 17 también son compatibles recientemente. Para ver los pasos de configuración, incluida la actualización del proyecto Maven y las versiones de la biblioteca, consulte el artículo [Entorno de compilación](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md#using-java-support). 

El **entorno de ejecución** de Java 21 de mayor rendimiento se implementará automáticamente cuando se detecte una compilación de Java 17 o 21. Sin embargo, también recomendamos optar por el tiempo de ejecución de Java 21 para entornos creados con Java 11, enviando un correo electrónico a [aemcs-java-adopter@adobe.com](mailto:aemcs-java-adopter@adobe.com). Obtenga información sobre los [requisitos del tiempo de ejecución de Java 21](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md#runtime-requirements).

>[!IMPORTANT]
>
> El **tiempo de ejecución** de Java 21 se implementará gradualmente en **todos los** entornos (además de los ya creados con Java 17 o 21, que ya tienen el tiempo de ejecución de Java 21), empezando por los entornos limitados y dev/RDE en febrero y luego fases/producción en abril.

### Los programas de zona protegida admiten canalizaciones de configuración {#sandbox-config-pipelines}

Los programas de zona protegida ahora admiten canalizaciones de configuración, que se pueden configurar en Cloud Manager para implementar archivos yaml persistentes en Git.

[Obtenga más información](/help/operations/config-pipeline.md) sobre las canalizaciones de configuración, que permiten la configuración de CDN, el reenvío de registros y tareas de mantenimiento de purga de versiones/purga de registros de auditoría.

### API basadas en OpenAPI: programa para primeros usuarios {#open-apis-earlyadopter}

Los desarrolladores pueden integrar completamente las funciones de AEM as a Cloud Service en sus propias aplicaciones y herramientas. Las nuevas API de AEM as a Cloud Service siguen la especificación de OpenAPI, con el objetivo de ser coherentes, bien documentadas y fáciles de usar. Las credenciales de los puntos finales que requieren autenticación se generarán creando proyectos de Adobe Developer Console.

Obtenga más información sobre las [API de AEM basadas en OpenAPI](/help/implementing/developing/open-api-based-apis.md) y realice un [tutorial completo](https://experienceleague.adobe.com/es/docs/experience-manager-learn/cloud-service/aem-apis/invoke-openapi-based-aem-apis) que ilustra la configuración y el uso.

En concreto, los puntos finales de API que se enumeran a continuación están disponibles como parte de un programa para primeros usuarios. Si está interesado, envíe un correo electrónico a [aem-apis@adobe.com](mailto:aem-apis@adobe.com) describiendo cómo piensa utilizarlos.

* [API de fragmentos de contenido en Sites](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/sites/)
* [API de recursos](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/assets/author/)
* [API de Sites y carpetas de recursos](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/folders/)
* [API de comunicaciones de formularios](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/)

### Edge Computing: solicitud de comentarios {#edge-computing-feedback}

Edge Computing acerca el procesamiento de datos al explorador, lo que ofrece ventajas como una menor latencia. A Adobe le encantaría saber si esta tecnología le resulta útil para los proyectos de AEM Publish Delivery y Edge Delivery Services. Además, indíquenos para qué prevé utilizarla como aportación a la hoja de ruta del producto. Envíe un correo electrónico a [aemcs-edgecompute-feedback@adobe.com](mailto:aemcs-edgecompute-feedback@adobe.com) con preguntas y comentarios.

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
