---
title: Notas de la versión 2022.7.0 de la versión de  [!DNL Adobe Experience Manager]  as a Cloud Service.
description: Notas de la versión 2022.7.0 de la versión de  [!DNL Adobe Experience Manager]  as a Cloud Service.
exl-id: b339ab48-e836-4589-a573-9c50917b9280
source-git-commit: 7b21a8af886c8e1f209e3b7cc5d94de5c58be1ac
workflow-type: tm+mt
source-wordcount: '958'
ht-degree: 25%

---

# Notas de la versión actuales de [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

En la siguiente sección se describen las notas de la versión generales de la versión actual (la más reciente) de [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Desde aquí puede navegar hasta las notas de versiones anteriores; por ejemplo, las de 2020, 2021, etc.

>[!NOTE]
>
>Consulte [Actualizaciones recientes de la documentación](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html?lang=es) para obtener más información sobre las actualizaciones de la documentación no relacionadas directamente con una versión.

## Fecha de la versión {#release-date}

La fecha de lanzamiento de [!DNL Adobe Experience Manager] como [!DNL Cloud Service] la versión actual (2022.7.0) es el 8 de agosto de 2022.

La próxima versión (2022.8.0) está planificada para el 1 de septiembre de 2022.

## Vídeo de la versión {#release-video}

Eche un vistazo al vídeo Información general de la versión de julio de 2022 para ver un resumen de las funciones agregadas en la versión 2022.7.0:

>[!VIDEO](https://video.tv.adobe.com/v/345409/?quality=12)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Nuevas funciones de [!DNL Sites] {#sites-features}

* La variable [Consola de fragmento de contenido](/help/sites-cloud/administering/content-fragments/content-fragments-console.md) ahora admite [combinaciones de teclas](/help/sites-cloud/administering/content-fragments/content-fragments-console-keyboard-shortcuts.md).

* AEM como del Cloud Service [entrega de imágenes optimizada para la web](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/web-optimized-image-delivery.html) permite mejorar significativamente la velocidad de la página al entregar formatos como WebP. Este nuevo servicio también ofrece opciones más flexibles de cambio de tamaño y transformación de imágenes. Todas las versiones de [Componente de imagen principal](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/image.html?lang=es) permite aprovechar este servicio y ofrecer imágenes como WebP haciendo clic en una opción de la política del componente de imagen.

* AEM actividades de personalización ahora pueden aprovechar los fragmentos de experiencia en lugar de nuestras ofertas heredadas. Esta función:
   * permite una ruta de migración en la que AEM contenido promocionaría ofertas de fragmentos de experiencias en lugar de ofertas de bibliotecas heredadas para proporcionar contenido con un estilo adecuado que se alinee con la personalización a escala en el futuro.
   * evita que los autores de contenido sirvan accidentalmente contenido sin estilo en su sitio.
   * permite convertir el modo de objetivo de cualquier componente en un fragmento de experiencia (tanto de tipo JSON como de HTML) que utilice plantillas editables.

>[!NOTE]
>
>Las actividades de personalización existentes que ya utilizan ofertas heredadas pueden seguir haciéndolo, pero deben crearse nuevas actividades de personalización como fragmentos de experiencia, ya que ese es el enfoque recomendado a partir de ahora.

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Nuevas funciones disponibles en el canal de prelanzamiento de [!DNL Assets] {#prerelease-features-assets}

Ahora puede configurar Adobe Experience Manager Assets en [restringir el tipo de recursos que los usuarios pueden cargar en función del tipo MIME](/help/assets/configure-asset-upload-restrictions.md).

![Restricciones de carga de recursos](/help/assets/assets/asset-upload-restrictions.png)

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### Nuevas funciones de [!DNL Forms] {#forms-features}

* **[Compatibilidad de entrada de teclado con firmas Scribble](/help/forms/signing-forms-using-scribble.md)**: Los Forms adaptables se utilizan cada vez más en dispositivos táctiles y uno de los requisitos comunes es admitir firmas. La firma de documentos en dispositivos táctiles se ha convertido en una forma aceptada de firmar formularios. Adaptive Forms es compatible de forma nativa con Scribble Signatures y con Adobe Sign en estos casos de uso. Ahora, junto con otras opciones ya compatibles, también puede utilizar el teclado para crear anotaciones en un formulario adaptable. También ayuda a mejorar el cumplimiento de las normas de accesibilidad.

![Compatibilidad de entrada de teclado con firmas Scribble en iphone](/help/release-notes/assets/scribble-keyboard-mobile.png)

* **Uso del asistente de Forms adaptable en idioma local**: Puede utilizar el asistente en el idioma que prefiera. Ahora es compatible con todos los idiomas compatibles con Adobe Experience Manager.

### Nuevas funciones disponibles en el canal de prelanzamiento de [!DNL Forms] {#prerelease-features-forms}

<!-- 

* **[Launch Adaptive Form creation wizard from embed form component](/help/forms/using/embed-adaptive-form-aem-sites.md)**: You can now launch Adaptive Form creation wizard from embed form component. It helps improve content and forms authoring workflows for Sites and Forms practitioners trying to add enrollment experiences to a web page. 

![Keyboard input support for Scribble signatures on iphone](/help/release-notes/assets/froms-container.png) 

-->

* **[Invocar DDX: Un paso AEM del flujo de trabajo](/help/forms/aem-forms-workflow-step-reference.md#invokeddx)**: Document Description XML (DDX) es un lenguaje declarativo de marcado cuyos elementos representan componentes básicos de documentos. Estos componentes básicos incluyen documentos PDF y XDP, y otros elementos como comentarios, marcadores y texto con estilo. Los documentos DDX son plantillas para los documentos y describen las características deseadas de los documentos de origen que deberían aparecer en los documentos resultantes. Se puede utilizar un solo DDX con una amplia gama de documentos de origen. Puede utilizar el paso Invocar y el flujo de trabajo AEM para realizar varias operaciones, como ensamblar documentos desensamblados, crear y modificar Acrobat y XFA Forms, y otras operaciones descritas en [Referencia de DDX](https://helpx.adobe.com/content/dam/help/en/experience-manager/forms-cloud-service/ddxRef.pdf) documentación.

* **[Convertir en PDF/A: un paso AEM del flujo de trabajo](/help/forms/aem-forms-workflow-step-reference.md##convert-pdfa)**: PDF/A es un formato de archivo para la preservación a largo plazo del contenido del documento, todas las fuentes están incrustadas y el archivo no está comprimido. Ahora, puede utilizar el paso Convertir en PDF/A y Flujo de trabajo AEM para convertir sus documentos o archivos en cualquier formato a formato de PDF/A.


## Complemento CIF {#cloud-services-cif}

### Novedades {#what-is-new-cif}

* El enriquecimiento del catálogo de productos ahora admite páginas AEM. Esto permite a los autores administrar la asociación de páginas y productos.

* Varias mejoras en los componentes principales del CIF

### Corrección de errores {#bug-fixes-cif}

* Agregar token de inicio de sesión a la recuperación de precios del lado del cliente

* Componente de página incorrecto en la capa de datos

## [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation {#foundation}

### Novedades {#what-is-new-foundation}

* La variable [Explorador del repositorio](/help/implementing/developing/tools/repository-browser.md) ahora tiene un campo de entrada de ruta, lo que permite saltar directamente a una carpeta específica en la jerarquía del repositorio
* Sling Content Distribution (SCD) ahora admite una acción explícita de &quot;invalidación&quot; para invalidar contenido sin que se publique dicho contenido. Consulte la [Almacenamiento en caché en AEM as a Cloud Service](/help/implementing/dispatcher/caching.md#explicit-invalidation) para obtener más información.
* mod_macro ahora está disponible en AEM as a Cloud Service. Consulte [esta tabla](/help/implementing/dispatcher/disp-overview.md) para obtener una lista de los módulos Apache compatibles.

### AEM mejoras as a Cloud Service en las herramientas de Dispatcher de SDK {#dispatcher-tools-enhancements}

* Apache puede iniciarse con `docker_run_hot_reload.sh` script, que cargará y validará automáticamente cualquier cambio posterior en la configuración de Apache y Dispatcher, mejorando así la velocidad del desarrollador. Solo se admite en el modo flexible de herramientas de Dispatcher. Consulte también [Depuración de la configuración de Apache y Dispatcher](/help/implementing/dispatcher/validation-debug.md#automatic-reloading) para obtener más información sobre la recarga y validación automáticas.
* La configuración de Apache/Dispatcher local realizará un seguimiento más detallado de los cambios en los entornos de la nube, lo que aumentará la paridad entre los dos entornos.

### Nuevas funciones disponibles en el canal de prelanzamiento de [!DNL Experience Manager] {#prerelease-features-foundation}

* AEM as a Cloud Service está ahora integrado con Unified Shell para mejorar la experiencia del usuario y unificarlo con todas las demás aplicaciones de Experience Cloud. Consulte [AEM as a Cloud Service en Unified Shell](/help/overview/aem-cloud-service-on-unified-shell.md) para obtener más información.

## Conectores de Adobe Learning Manager {#learn-manage}

* El nuevo Administrador de aprendizaje de Adobe tiene conectores para Adobe Experience Manager Sites, Marketo Engage y Adobe Commerce. Para obtener más información, consulte: [Guía del usuario de Adobe Learning Manager](https://helpx.adobe.com/learning-manager/user-guide.html).

## Cloud Manager {#cloud-manager}

Puede encontrar una lista completa de las versiones mensuales de Cloud Manager [aquí.](/help/implementing/cloud-manager/release-notes/current.md)

## Herramientas de migración {#migration-tools}

Puede encontrar una lista completa de las versiones de las herramientas de migración [aquí](/help/journey-migration/release-notes/release-notes-migration-tools-current.md).
