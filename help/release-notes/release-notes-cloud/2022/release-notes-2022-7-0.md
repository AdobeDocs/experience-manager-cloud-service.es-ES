---
title: Notas de la versión 2022.7.0 de la versión de  [!DNL Adobe Experience Manager]  as a Cloud Service.
description: Notas de la versión 2022.7.0 de la versión de  [!DNL Adobe Experience Manager]  as a Cloud Service.
exl-id: b339ab48-e836-4589-a573-9c50917b9280
feature: Release Information
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '935'
ht-degree: 24%

---

# Notas de la versión 202278.0 para [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

En la siguiente sección se describen las notas de la versión de la función para la versión 2022.7.0 de [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Desde aquí puede navegar hasta las notas de versiones anteriores; por ejemplo, las de 2020, 2021, etc.

>[!NOTE]
>
>Consulte [Actualizaciones recientes de la documentación](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html?lang=es) para obtener más información sobre las actualizaciones de la documentación no relacionadas directamente con una versión.

## Fecha de lanzamiento {#release-date}

La fecha de lanzamiento de la versión actual de [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] (2022.7.0) es el martes, 08 de agosto de 2022.

La próxima versión (2022.8.0) está planificada para el 1 de septiembre de 2022.

## Vídeo de la versión {#release-video}

Eche un vistazo al vídeo Información general sobre la versión de julio de 2022 para ver un resumen de las funcionalidades añadidas en la versión 2022.7.0:

>[!VIDEO](https://video.tv.adobe.com/v/3454199/?quality=12&captions=spa)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Nuevas funciones de [!DNL Sites] {#sites-features}

* La [consola de fragmentos de contenido](/help/sites-cloud/administering/content-fragments/managing.md#content-fragments-console) ahora admite [métodos abreviados de teclado](/help/sites-cloud/administering/content-fragments/keyboard-shortcuts.md).

* AEM ya que la [entrega de imágenes optimizadas para la web](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/web-optimized-image-delivery.html?lang=es) de Cloud Service permite mejorar significativamente la velocidad de la página al ofrecer formatos como WebP. Este nuevo servicio también ofrece opciones más flexibles de cambio de tamaño y transformación de imágenes. Todas las versiones del [Componente de imagen principal](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/image.html?lang=es) le permiten utilizar este servicio y enviar imágenes como WebP haciendo clic en una opción de la directiva del componente de imagen.

* AEM Ahora, las actividades de personalización de pueden utilizar fragmentos de experiencias en lugar de nuestras ofertas heredadas. Esta función:
   * AEM habilita una ruta de migración en la que el contenido de la promocionaría ofertas de fragmentos de experiencias en lugar de ofertas de bibliotecas heredadas para proporcionar contenido con un estilo adecuado que se ajuste a la personalización a escala en el futuro.
   * evita que los autores de contenido sirvan accidentalmente contenido sin estilo en su sitio.
   * permite convertir el modo de direccionamiento de cualquier componente a un fragmento de experiencia (de ambos tipos: JSON y HTML) que utilice plantillas editables.

>[!NOTE]
>
>Las actividades de personalización existentes que ya utilizan ofertas heredadas pueden seguir haciéndolo, pero las nuevas actividades de personalización deben crearse como fragmentos de experiencia, ya que ese es el enfoque recomendado a partir de ahora.

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Nuevas funciones disponibles en el canal de prelanzamiento de [!DNL Assets] {#prerelease-features-assets}

Ahora puede configurar Adobe Experience Manager Assets para [restringir el tipo de recursos que los usuarios pueden cargar según el tipo MIME](/help/assets/configure-asset-upload-restrictions.md).

![Restricciones de carga de recursos](/help/assets/assets/asset-upload-restrictions.png)

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### Nuevas funciones de [!DNL Forms] {#forms-features}

* **[Compatibilidad de entrada de teclado con firmas Scribble](/help/forms/signing-forms-using-scribble.md)**: los Forms adaptables se utilizan cada vez más en dispositivos táctiles, y uno de los requisitos comunes es ser compatibles con firmas. La firma de documentos en dispositivos táctiles se ha convertido en una forma aceptada para firmar formularios. Adaptive Forms es compatible de forma nativa con firmas de Scribble y con Adobe Sign en estos casos de uso. Ahora, junto con otras opciones ya compatibles, también puede utilizar el teclado para crear firmas de Scribble en un formulario adaptable. También ayuda a mejorar el cumplimiento de la accesibilidad.

![Compatibilidad de entrada de teclado con firmas manuscritas en el iphone](/help/release-notes/assets/scribble-keyboard-mobile.png)

* **Usar el asistente de Forms adaptable en idioma local**: puede usar el asistente en el idioma que prefiera. Ahora es compatible con todos los idiomas admitidos por Adobe Experience Manager.

### Nuevas funciones disponibles en el canal de prelanzamiento de [!DNL Forms] {#prerelease-features-forms}

<!-- 

* **[Launch Adaptive Form creation wizard from embed form component](/help/forms/using/embed-adaptive-form-aem-sites.md)**: You can now launch Adaptive Form creation wizard from embed form component. It helps improve content and forms authoring workflows for Sites and Forms practitioners trying to add enrollment experiences to a web page. 

![Keyboard input support for Scribble signatures on iphone](/help/release-notes/assets/froms-container.png) 

-->

* AEM **[Invocar DDX - Un paso del flujo de trabajo de](/help/forms/aem-forms-workflow-step-reference.md#invokeddx)**: Document Description XML (DDX) es un lenguaje de marcado declarativo cuyos elementos representan componentes básicos de documentos. Estos componentes básicos incluyen documentos PDF y XDP, y otros elementos como comentarios, marcadores y texto con estilo. Los documentos DDX son plantillas para los documentos y describen las características deseadas de los documentos de origen que deben aparecer en los resultantes. Se puede utilizar un solo DDX con una amplia gama de documentos de origen. AEM Puede usar el paso Invocar y el flujo de trabajo de la para realizar varias operaciones, como ensamblar documentos separados, crear y modificar Acrobat y XFA Forms, y otras operaciones descritas en la documentación de [DDX Reference](https://helpx.adobe.com/content/dam/help/es/experience-manager/forms-cloud-service/ddxRef.pdf).

* **[Convertir en PDF AEM/A - Un paso del flujo de trabajo de](/help/forms/aem-forms-workflow-step-reference.md##convert-pdfa)**: PDF/A es un formato de archivo para la preservación a largo plazo del contenido del documento, todas las fuentes están incrustadas y el archivo no está comprimido. Ahora, puede utilizar el paso Convertir en PDF AEM/A y el flujo de trabajo de para convertir los documentos o archivos en cualquier formato al formato PDF/A.


## Complemento CIF {#cloud-services-cif}

### Novedades {#what-is-new-cif}

* AEM Ahora, el enriquecimiento del catálogo de productos admite páginas de. Esto permite a los autores administrar la asociación página - producto.

* CIF Varias mejoras en los componentes principales de la

### Corrección de errores {#bug-fixes-cif}

* Añadir token de inicio de sesión a la recuperación de precios del lado del cliente

* Componente de página incorrecto en la capa de datos

## [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation {#foundation}

### Novedades {#what-is-new-foundation}

* El [Explorador del repositorio](/help/implementing/developing/tools/repository-browser.md) ahora tiene un campo de entrada de ruta, lo que permite saltar directamente a una carpeta específica en la jerarquía del repositorio
* Sling Content Distribution (SCD) ahora admite una acción explícita de &quot;invalidación&quot; para invalidar contenido sin que se publique. Consulte la página [Almacenamiento en caché en AEM as a Cloud Service](/help/implementing/dispatcher/caching.md#explicit-invalidation) para obtener más información.
* mod_macro ya está disponible en AEM as a Cloud Service. Consulte [esta tabla](/help/implementing/dispatcher/disp-overview.md) para obtener una lista de los módulos Apache admitidos.

### Mejoras en las herramientas Dispatcher del SDK de AEM as a Cloud Service {#dispatcher-tools-enhancements}

* Apache puede iniciarse con el script `docker_run_hot_reload.sh`, que cargará y validará automáticamente cualquier cambio posterior en la configuración de Apache y Dispatcher, y así mejorará la velocidad del desarrollador. Solo se admite en el modo flexible de las herramientas de Dispatcher. Además, consulte [Depuración de la configuración de Apache y Dispatcher](/help/implementing/dispatcher/validation-debug.md#automatic-reloading) para obtener más información sobre la recarga y validación automáticas.
* La configuración local de Apache/Dispatcher rastreará más de cerca los cambios en los entornos de la nube, aumentando la paridad entre los dos entornos.

### Nuevas funciones disponibles en el canal de prelanzamiento de [!DNL Experience Manager] {#prerelease-features-foundation}

* AEM as a Cloud Service está ahora integrado con Unified Shell para mejorar la experiencia del usuario y unificarlo con todas las demás aplicaciones de Experience Cloud. Consulte [AEM as a Cloud Service en Unified Shell](/help/overview/aem-cloud-service-on-unified-shell.md) para obtener más información.

## Conectores de Adobe Learning Manager {#learn-manage}

* El nuevo Adobe Learning Manager tiene conectores para Adobe Experience Manager Sites, Marketo Engage y Adobe Commerce. Para obtener más información, consulte: [Guía del usuario de Adobe Learning Manager](https://helpx.adobe.com/es/learning-manager/user-guide.html).

## Cloud Manager {#cloud-manager}

Puede encontrar una lista completa de las versiones mensuales de Cloud Manager [aquí](/help/implementing/cloud-manager/release-notes/current.md).

## Herramientas de migración {#migration-tools}

Puede encontrar una lista completa de las versiones de las herramientas de migración [aquí](/help/journey-migration/release-notes/release-notes-migration-tools-current.md).
