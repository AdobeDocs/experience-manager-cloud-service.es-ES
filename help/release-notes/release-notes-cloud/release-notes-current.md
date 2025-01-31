---
title: Notas de la versión actuales de [!DNL Adobe Experience Manager] as a Cloud Service.
description: Notas de la versión actuales de [!DNL Adobe Experience Manager] as a Cloud Service.
mini-toc-levels: 1
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
feature: Release Information
role: Admin
source-git-commit: 190e68ebcd3c2a7ba7b995690c802a04728e6962
workflow-type: tm+mt
source-wordcount: '1749'
ht-degree: 41%

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

La fecha de lanzamiento de [!DNL Adobe Experience Manager] como versión de funcionalidad actual (2025.1.0) de [!DNL Cloud Service] es el viernes, 30 de enero de 2025. La próxima versión de la funcionalidad (2025.2.0) está planificada para el viernes, 27 de febrero de 2025.

## Notas de la versión de mantenimiento {#maintenance}

Puede encontrar las últimas notas de la versión de mantenimiento [aquí](/help/release-notes/maintenance/latest.md).

<!-- 

## Release Video {#release-video}

Have a look at the January 2025 Release Overview video for a summary of the features added in the 2025.1.0 release:

>[!VIDEO](https://video.tv.adobe.com/v/3440920?quality=12)

-->

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

**Los comentarios del editor de fragmentos de contenido ya están disponibles de forma general**

AEM AEM Colabore fácilmente con sus compañeros de trabajo al crear fragmentos de contenido de la mediante el uso del servicio de comentarios nuevo y modernizado en el Editor de fragmentos de contenido de la.
[Más información](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/sites/administering/content-fragments/authoring?#commenting-on-your-fragment).

**Editor de fragmentos de contenido e interfaces de usuario de administración, compatibilidad actualizada con la versión de AEM as a Cloud Service**

La versión mínima de AEM as a Cloud Service admitida para las nuevas interfaces de usuario de Administrador y Editor de fragmentos de contenido es ahora 2023.8.13099. Ya no se admiten las versiones anteriores a la versión de disponibilidad general de las nuevas interfaces de usuario

### Programa para primeros usuarios {#sites-early-adopter}

**Fragmentos de contenido mejorado**

Se mejoró la referencia a [fragmento de contenido con referencias basadas en ID únicas](/help/headless/graphql-api/uuid-reference-upgrade.md), lo que ayuda a garantizar que las consultas de GraphQL de fragmentos de contenido individuales puedan permanecer estables incluso si el fragmento se movió a otra ubicación. Esto ahora es posible con consultas &quot;ByID&quot;. Aunque las rutas pueden cambiar, lo que potencialmente rompe las consultas &quot;ByPath&quot;, los UUID son estables. Los nuevos ID también se pueden devolver como propiedades en cualquier consulta u otra solicitud de API aplicable. Limitación actual (2025.1): Las referencias de página aún no son compatibles con los ID únicos. Si se hace referencia a las páginas en los fragmentos de contenido, esta capacidad no debe utilizarse. Se prevé eliminar esta limitación en la próxima versión de AEM as a Cloud Service.

**AEM REST OpenAPI para la entrega de fragmentos de contenido**

AEM La API abierta de [REST para la entrega de fragmentos de contenido](/help/headless/aem-rest-openapi-content-fragment-delivery.md) ya está disponible para AEM as a Cloud Service.

### Funciones en desuso {#sites-deprecated}

#### SPA Editor de {#spa-editor}

SPA [El Editor de la](/help/implementing/developing/hybrid/introduction.md) ha quedado obsoleto para nuevos proyectos que comienzan con la versión 2025.1.0. SPA El Editor de segmentos sigue siendo compatible con los proyectos existentes, pero no debe utilizarse para nuevos proyectos.

AEM Los editores preferidos para administrar contenido sin encabezado en las ahora son:

* [Editor universal](/help/edge/wysiwyg-authoring/authoring.md) para la edición visual.
* [Editor de fragmentos de contenido](/help/assets/content-fragments/content-fragments-managing.md) para la edición basada en formularios.

#### Funciones del PWA {#pwa-features}

[Las características de la aplicación web progresiva (PWA)](/help/sites-cloud/authoring/sites-console/enable-pwa.md) para AEM Sites están en desuso para los nuevos proyectos a partir de la versión 2025.1.0. Esta función sigue siendo compatible con los proyectos existentes, pero no debe utilizarse para nuevos proyectos

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Nuevas funciones de los AEM Assets {#new-features-assets}

**plantillas de Dynamic Media**

Personalice los titulares de imágenes y textos sobre la marcha con un editor de plantillas de Dynamic Media de WYSIWYG fácil de usar, incrustando la URL en cualquier aplicación de origen o de terceros para impulsar experiencias muy atractivas con actualizaciones de contenido de banners en tiempo real.

![representaciones dinámicas](/help/assets/assets/dm-templates-smart-text-resize.png)

**informes de envío de Dynamic Media**

Obtenga perspectivas de entrega para los recursos entregados a través de Dynamic Media, incluidos recuentos de entregas en el nivel de recurso, detalles del referente, rutas de recursos en AEM Assets e ID de recursos únicos. Generar informes para todos los recursos del repositorio de AEM Assets o jerarquías de carpetas específicas. Estas perspectivas le permiten medir el ROI de los recursos entregados, evaluar el rendimiento del canal y tomar decisiones informadas para la administración de recursos.

![representaciones dinámicas](/help/assets/assets/referrer.png)

**Pie de ilustración y audio de Dynamic Media**

[Compatibilidad con varios subtítulos y pistas de audio para vídeos en Dynamic Media](/help/assets/dynamic-media/video.md#about-msma): Ahora puede agregar fácilmente varios subtítulos y pistas de audio a un vídeo principal. Esta capacidad significa que los vídeos son accesibles para una audiencia global. Puede personalizar un solo vídeo principal publicado para un público global en varios idiomas y seguir las directrices de accesibilidad para diferentes regiones geográficas. Los autores también pueden administrar los subtítulos y las pistas de audio desde una sola pestaña en la interfaz de usuario.

**Compatibilidad con flujo adaptable dinámico a través de HTTP**

Lanzamiento de nuevo protocolo de asistencia (DASH - Dynamic Adaptive Streaming over HTTP) para streaming adaptable en la entrega de vídeo de Dynamic Media (con CMAF habilitado):

* El streaming adaptable (DASH/HLS) garantiza una mejor experiencia de visualización de los usuarios para los vídeos.

* DASH es el protocolo estándar internacional para la transmisión de vídeo adaptable y es ampliamente adoptado en el sector.

**Relaciones de recursos**

La vista de Assets ahora admite la visualización y edición de relaciones de recursos en un panel de detalles de recursos simplificado. Agregue fácilmente relaciones como Source y Derivative al contenido para que los usuarios puedan encontrar de forma más eficaz el contenido relevante para los héroes.

**Volver a procesar recursos**

La vista de Assets ahora admite el reprocesamiento de recursos disponibles en una carpeta. Puede seleccionar usar la opción **Proceso completo** o usar opciones avanzadas como, por ejemplo, representaciones de vista previa predeterminada, metadatos, flujo de trabajo de posprocesamiento y perfil de procesamiento.

### Funciones de acceso anticipado en AEM Assets {#early-access-features-assets}

**Subtítulos de vídeo generados por IA**

Los subtítulos de vídeo generados por IA en Adobe Dynamic Media utilizan la inteligencia artificial para generar subtítulos automáticamente para el contenido de vídeo. Esta función está diseñada para mejorar la accesibilidad y la experiencia del usuario gracias a la provisión de subtítulos precisos en tiempo real. Los subtítulos se generan a partir del audio original, de cualquier pista de audio adicional o de los subtítulos adicionales proporcionados en la pestaña &quot;Subtítulos y audio&quot; de la página de propiedades del vídeo. Con compatibilidad con más de 60 idiomas, los subtítulos se pueden revisar y previsualizar antes de publicar el vídeo.

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### Nuevas funciones en AEM Forms {#forms-new-features}

* **Administrar publicación**: puede usar el flujo de trabajo &quot;Administrar publicación&quot; para publicar o cancelar la publicación de formularios en entornos, generalmente desde la instancia de autor a las instancias de publicación y vista previa. Permite a los usuarios publicar, cancelar la publicación o programar la publicación de contenido de una manera optimizada.

* **[Guardar automáticamente un borrador para formularios adaptables basados en componentes principales](/help/forms/save-core-component-based-form-as-draft.md)**: los usuarios ahora pueden beneficiarse de una función de guardado automático que guarda automáticamente un formulario parcialmente completado como borrador. Pueden volver más tarde para terminar de rellenarlo en el mismo dispositivo o en otro distinto. Esta función mejora las tasas de conversión para las organizaciones al reducir el abandono de formularios, ya que los usuarios no tienen que volver a empezar a rellenar el formulario desde el principio.

* **[Mejoras en el editor de reglas](/help/forms/invoke-service-enhancements-rule-editor.md)**: para Forms adaptable basado en componentes principales, puede usar la salida de Invocar servicio para rellenar opciones desplegables y establecer paneles repetibles o individuales. Además, este resultado se puede utilizar para validar otros campos.

* **[Mejorar la experiencia del usuario con botones de navegación en los diseños de panel](/help/forms/rule-editor-core-components-usecases.md#navigating-among-panels-using-button)**: ahora puede añadir botones de navegación a los diseños de panel, como Pestañas horizontales, Pestañas verticales, Acordeones o el Asistente. Estos botones mejoran la experiencia del usuario al simplificar las transiciones entre paneles y se centran en el panel seleccionado.


### Funciones de acceso rápido de AEM Forms {#forms-new-early-access-features}

El programa para acceso rápido de AEM Forms ofrece una oportunidad única de obtener acceso exclusivo a innovaciones punteras y ayudar a dar forma a su desarrollo.

En estas notas de la versión se indican las innovaciones de la versión actual. Para ver la lista completa de innovaciones disponibles en el programa para acceso rápido, consulte la [documentación del programa de acceso rápido de AEM Forms](/help/forms/early-access-ea-features.md).

#### [Plantillas de correo electrónico de HTML en Forms adaptable](/help/forms/html-email-templates-in-adaptive-forms.md)

El Forms adaptable permite utilizar plantillas de correo electrónico de HTML. Las plantillas de correo electrónico de HTML le permiten enviar correos electrónicos enriquecidos, personalizados y visualmente atractivos cuando se envía un formulario. Estos correos electrónicos se pueden personalizar con los datos del formulario y mejorar mediante varias etiquetas de correo electrónico, como imágenes y vínculos. Con Forms adaptable, puede cargar un archivo que contenga una plantilla de HTML o utilizar un editor de texto sin formato para crear estas plantillas.

![plantillas de correo electrónico de HTML](/help/forms/assets/html-email.png)

#### Compatibilidad mejorada con almacenamiento en la nube: carga directa del PDF al almacenamiento del blob de Azure

Las API de generación de documentos de AEM Forms ahora admiten la carga directa de documentos de PDF generados al almacenamiento del blob de Azure. Esta mejora optimiza el almacenamiento y la recuperación, mejorando la eficiencia y la integración con los flujos de trabajo en la nube.

## [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation {#foundation}

### Compatibilidad con Java 21 {#java21}

Ahora puede generar código con Java 21, que incluye nuevas funciones (por ejemplo, coincidencia de patrones para instrucciones de switch, clases selladas) y mejoras de rendimiento; las compilaciones de Java 17 también son compatibles recientemente. Para ver los pasos de configuración, incluida la actualización del proyecto Maven y las versiones de la biblioteca, consulte el artículo [Entorno de compilación](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md#using-java-support).

El Java 21 **runtime** con mayor rendimiento se implementará automáticamente cuando se detecte una compilación de Java 17 o 21. Sin embargo, también recomendamos la inclusión en el tiempo de ejecución de Java 21 para entornos creados con Java 11, enviando un correo electrónico a [aemcs-java-adopter@adobe.com](mailto:aemcs-java-adopter@adobe.com). Obtenga información acerca de [requisitos de tiempo de ejecución de Java 21](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md#runtime-requirements).

>[!IMPORTANT]
>
> Java 21 **runtime** se implementará gradualmente en **todos los** entornos (además de los ya creados con Java 17 o 21, que ya tienen Java 21 en tiempo de ejecución), empezando por los entornos limitados y dev/RDE en febrero y luego la fase/producción en abril.

### Los programas de zona protegida admiten canalizaciones de configuración {#sandbox-config-pipelines}

Los programas de zona protegida ahora admiten canalizaciones de configuración, que se pueden configurar en Cloud Manager para implementar archivos yaml persistentes en Git.

[Obtenga más información](/help/operations/config-pipeline.md) acerca de las canalizaciones de configuración, que permiten la configuración de la CDN, el reenvío de registros y las tareas de mantenimiento de purga de versiones/purga de registros de auditoría.

### API basadas en OpenAPI: programa para primeros usuarios {#open-apis-earlyadopter}

Los desarrolladores pueden integrar completamente las funciones de AEM as a Cloud Service en sus propias aplicaciones y herramientas. Las nuevas API de AEM as a Cloud Service siguen la especificación de OpenAPI, con el objetivo de ser coherentes, bien documentadas y fáciles de usar. Las credenciales de los puntos de conexión que requieren autenticación se generan al crear proyectos de Adobe Developer Console.

Obtenga más información sobre las [API de AEM basadas en OpenAPI](/help/implementing/developing/open-api-based-apis.md) y realice un [tutorial completo](https://experienceleague.adobe.com/es/docs/experience-manager-learn/cloud-service/aem-apis/invoke-openapi-based-aem-apis) que ilustra la configuración y el uso.

En concreto, los puntos finales de API que se enumeran a continuación están disponibles como parte de un programa para primeros usuarios. Si está interesado, envíe un correo electrónico a [aem-apis@adobe.com](mailto:aem-apis@adobe.com) describiendo cómo piensa utilizarlos.

* [API de fragmentos de contenido en Sites](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/sites/)
* [API de recursos](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/assets/author/)
* [API de Sites y carpetas de recursos](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/folders/)
* [API de comunicaciones de formularios](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/)

### Edge Computing: solicitud de comentarios {#edge-computing-feedback}

Edge Computing acerca el procesamiento de datos al explorador, lo que ofrece ventajas como una menor latencia. A Adobe AEM le encantaría saber si esta tecnología resulta útil para los proyectos de entrega y Edge Delivery Services de Publish de la. Además, indíquenos para qué prevé utilizarlo como entrada en la hoja de ruta del producto. Envíe un correo electrónico a [aemcs-edgecompute-feedback@adobe.com](mailto:aemcs-edgecompute-feedback@adobe.com) con preguntas y comentarios.

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
