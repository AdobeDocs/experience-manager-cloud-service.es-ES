---
title: Notas de la versión actuales de  [!DNL Adobe Experience Manager]  as a Cloud Service.
description: Notas de la versión actuales de  [!DNL Adobe Experience Manager]  as a Cloud Service.
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
mini-toc-levels: 1
source-git-commit: 6d343e539be05a13bb2a3eaeba1da5656dc54f1a
workflow-type: tm+mt
source-wordcount: '626'
ht-degree: 26%

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

La fecha de lanzamiento de [!DNL Adobe Experience Manager] como [!DNL Cloud Service] la versión actual (2022.8.0) es el 1 de septiembre de 2022.
La próxima versión (2022.10.0) está planificada para el 27 de octubre de 2022.

## Vídeo de la versión {#release-video}

Eche un vistazo al vídeo Información general de la versión de agosto de 2022 para ver un resumen de las funciones agregadas en la versión 2022.8.0:

>[!VIDEO](https://video.tv.adobe.com/v/346608/?quality=12)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Nuevas funciones de [!DNL Sites] {#sites-features}

* El componente Correo electrónico permite crear contenido en AEM que luego se envía como correos electrónicos a través del Campaign Classic. El componente de correo electrónico principal:
   * se basa en la variable [Componente principal de WCM](https://github.com/adobe/aem-core-wcm-components) que admite plantillas editables y el sistema de estilos.
   * proporciona 10 componentes listos para la producción optimizados para el correo electrónico (página, contenedor, título, texto, imagen, botón, teaser, fragmento de experiencia, fragmento de contenido, segmentación).
   * proporciona personalización y segmentación avanzadas, gracias al [inserción de variables de Campaign](https://github.com/adobe/aem-core-email-components/wiki/RTE-Personalization) en la mayoría de los campos de diálogo y en la variable [Componente de segmentación](https://github.com/adobe/aem-core-email-components/wiki/Segmentation-component-(Technical-Documentation)).
   * proporciona una salida óptima para el HTML, fácil de enviar por correo electrónico, gracias al [Estilo CSS inliner](https://github.com/adobe/aem-core-email-components/wiki/HTML-Inliner:-Technical-documentation), el [HTML atributo inliner](https://github.com/adobe/aem-core-email-components/wiki/HTML-Inliner:-Technical-documentation)y [HTML sanitizer](https://github.com/adobe/aem-core-email-components/wiki/HTML-sanitizing:-Technical-documentation).
   * permite la creación de los correos electrónicos en cualquier parte.

### Nuevas funciones disponibles en el canal de prelanzamiento de [!DNL Sites] {#prerelease-features-sites}

* La variable [Consola de fragmento de contenido](/help/sites-cloud/administering/content-fragments/content-fragments-console.md) proporciona a los usuarios una opción para mostrar el número total de copias de idioma asociadas a un fragmento de contenido. Se ha proporcionado un acceso de 1 clic para ver todas las copias de idioma. Los usuarios también pueden filtrar la vista de tabla según la configuración regional de su interés.

![Idiomas de fragmentos de contenido](/help/release-notes/assets/cfconsole-languages.png)

## [!DNL Experience Manager Assets] como [!DNL Cloud Service] {#assets}

### Nuevas funciones de [!DNL Assets] {#features-assets}

* Ahora puede configurar Adobe Experience Manager Assets en [restringir el tipo de recursos que los usuarios pueden cargar en función del tipo MIME](/help/assets/configure-asset-upload-restrictions.md).

   ![Restricciones de carga de recursos](/help/assets/assets/asset-upload-restrictions.png)

## [!DNL Experience Manager Forms] como [!DNL Cloud Service] {#forms}

### Nuevas funciones disponibles en el canal de prelanzamiento de [!DNL Forms] {#prerelease-features-forms}

* [Asistente para Forms adaptable](/help/forms/creating-adaptive-form.md): AEM Forms proporciona un asistente fácil de usar para las empresas que crea rápidamente Forms adaptable. El asistente dispone de un rápido desplazamiento por pestañas para seleccionar fácilmente plantillas preconfiguradas, estilos, campos y opciones de envío para crear un formulario adaptable. Esta versión incorpora las siguientes mejoras al asistente:

   * Seleccione o anule la selección de campos: El asistente le permite crear un formulario adaptable basado en esquemas JSON y del modelo de datos de formulario. Ahora puede seleccionar un subconjunto de campos dentro de un esquema para incluirlos en un formulario adaptable. Los campos seleccionados se convierten a los correspondientes componentes de captura de datos del formulario adaptable para crear rápidamente los formularios adaptables deseados.

   * Usar plantillas estáticas: Los clientes con inversiones existentes en plantillas estáticas heredadas pueden continuar con su recorrido de adopción en la nube mediante plantillas estáticas en el asistente para crear formularios adaptables. Esto proporciona a los clientes tiempo adicional para migrar plantillas estáticas antiguas a plantillas editables modernas.

* [Eliminar campos ocultos de un documento de registro (DoR) durante el procesamiento en el servidor](/help/forms/generate-document-of-record-for-non-xfa-based-adaptive-forms.md): Puede generar el PDF de documento de registro para los usuarios finales que contenga únicamente aquellos campos que les fueran visibles durante la experiencia de captura de datos. Al enviar el formulario, el servidor valida qué campos se ocultaron al usuario final en función de los datos enviados y excluye del documento de registro para mantener la coherencia.

## Complemento CIF {#cloud-services-cif}

### Novedades {#what-is-new-cif}

* Asociación de páginas AEM a productos y categorías a través de AEM propiedades de página además de información general en la cabina de productos
   ![asociación de página de la cabina del producto](/help/assets/CIF/product_cockpit_page_association.png)

## Cloud Manager {#cloud-manager}

Puede encontrar una lista completa de las versiones mensuales de Cloud Manager [aquí](/help/implementing/cloud-manager/release-notes-cloud-manager/release-notes-cm-current.md).

## Herramientas de migración {#migration-tools}

Puede encontrar una lista completa de las versiones de las herramientas de migración [aquí](/help/journey-migration/release-notes/release-notes-migration-tools-current.md).
