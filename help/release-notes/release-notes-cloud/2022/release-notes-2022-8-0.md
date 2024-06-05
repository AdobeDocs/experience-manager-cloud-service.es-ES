---
title: Notas de la versión 2022.8.0 de la versión de  [!DNL Adobe Experience Manager]  as a Cloud Service.
description: Notas de la versión 2022.8.0 de la versión de  [!DNL Adobe Experience Manager]  as a Cloud Service.
exl-id: 0eff8100-5990-4553-8373-445fb7e6fb27
feature: Release Information
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '604'
ht-degree: 58%

---

# Notas de la versión 2022.8.0 para [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

En la siguiente sección se describen las notas de la versión de la función para la versión 2022.8.0 de [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Desde aquí puede navegar hasta las notas de versiones anteriores; por ejemplo, las de 2020, 2021, etc.

>[!NOTE]
>
>Consulte [Actualizaciones recientes de la documentación](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html?lang=es) para obtener más información sobre las actualizaciones de la documentación no relacionadas directamente con una versión.

## Fecha de lanzamiento {#release-date}

La fecha de lanzamiento de la versión actual de [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] (2022.8.0) es el viernes, 01 de septiembre de 2022.
La próxima versión (2022.10.0) está planificada para el 10 de noviembre de 2022.

## Vídeo de la versión {#release-video}

Echa un vistazo al vídeo Información general sobre la versión de agosto de 2022 para ver un resumen de las funciones añadidas en la versión 2022.8.0:

>[!VIDEO](https://video.tv.adobe.com/v/346608/?quality=12)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Nuevas funciones de [!DNL Sites] {#sites-features}

* AEM El componente Correo electrónico permite la creación de contenido en el correo electrónico que luego se entrega como correo electrónico a través del Campaign Classic. El componente Correo electrónico principal:
   * se basa en [Componente de Core WCM](https://github.com/adobe/aem-core-wcm-components) que admite plantillas editables y el sistema de estilos.
   * proporciona 10 componentes listos para la producción optimizados para el correo electrónico (página, contenedor, título, texto, imagen, botón, teaser, fragmento de experiencia, fragmento de contenido, segmentación).
   * proporciona una personalización y segmentación avanzadas, gracias a las [inserción de variables de Campaign](https://github.com/adobe/aem-core-email-components/wiki/RTE-Personalization) en la mayoría de los campos de diálogo, y a la [Componente Segmentación](https://github.com/adobe/aem-core-email-components/wiki/Segmentation-component-(Technical-Documentation)).
   * proporciona un resultado de HTML óptimo y fácil de usar gracias al [Inliner de estilos CSS](https://github.com/adobe/aem-core-email-components/wiki/HTML-Inliner:-Technical-documentation), el [inliner de atributo de HTML](https://github.com/adobe/aem-core-email-components/wiki/HTML-Inliner:-Technical-documentation), y el [desinfectante para HTML](https://github.com/adobe/aem-core-email-components/wiki/HTML-sanitizing:-Technical-documentation).
   * permite la creación de los correos electrónicos en cualquier lugar.

### Nuevas funciones disponibles en el canal de prelanzamiento de [!DNL Sites] {#prerelease-features-sites}

* El [Consola de fragmento de contenido](/help/sites-cloud/administering/content-fragments/managing.md#content-fragments-console) proporciona a los usuarios una opción para mostrar el número total de copias de idioma asociadas a un fragmento de contenido. Se ha proporcionado un acceso de 1 clic para ver todas las copias de idioma. Los usuarios también pueden filtrar la vista de tabla según la configuración regional de su interés.

![Idiomas de fragmentos de contenido](/help/release-notes/assets/cfconsole-languages.png)

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Nuevas funciones de [!DNL Assets] {#features-assets}

* Ahora puede configurar Adobe Experience Manager Assets para que [restringir el tipo de recursos que los usuarios pueden cargar en función del tipo MIME](/help/assets/configure-asset-upload-restrictions.md).

  ![Restricciones de carga de recursos](/help/assets/assets/asset-upload-restrictions.png)

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### Nuevas funciones disponibles en el canal de prelanzamiento de [!DNL Forms] {#prerelease-features-forms}

* [Asistente de Formularios adaptables](/help/forms/creating-adaptive-form.md): AEM Forms ofrece un asistente fácil de usuario empresarial que crea rápidamente Formularios adaptables. El asistente dispone de un rápido desplazamiento por pestañas para seleccionar fácilmente plantillas preconfiguradas, estilos, campos y opciones de envío para crear un formulario adaptable. Esta versión incorpora las siguientes mejoras al asistente:

   * Seleccionar o anular la selección de campos: el asistente le permite crear un formulario adaptable basado en esquemas JSON y del modelo de datos de formulario. Ahora puede seleccionar un subconjunto de campos dentro de un esquema para incluirlos en un Formulario adaptable. Los campos seleccionados se convierten en los correspondientes componentes de captura de datos del Formulario adaptable para crear rápidamente los formularios adaptables deseados.

   * Usar plantillas estáticas: los clientes con inversiones existentes en plantillas estáticas heredadas pueden continuar con su recorrido de adopción en la nube mediante el uso de plantillas estáticas en el asistente para crear formularios adaptables. Esto proporciona a los clientes tiempo adicional para migrar plantillas estáticas antiguas a plantillas editables modernas.

* [Quitar campos ocultos de un documento de registro (DoR) durante el procesamiento en el servidor](/help/forms/generate-document-of-record-for-non-xfa-based-adaptive-forms.md): puede generar el PDF de documento de registro para los usuarios finales que contenga únicamente aquellos campos que fueron visibles para ellos durante la experiencia de captura de datos. Al enviar el formulario, el servidor valida qué campos se ocultaron al usuario en función de los datos enviados y los excluye del documento de registro para mantener la coherencia.

## Complemento CIF {#cloud-services-cif}

### Novedades {#what-is-new-cif}

* AEM AEM Asociación de páginas de productos a productos y categorías a través de las propiedades de página de la página de productos más información general en la cabina de productos
  ![asociación de página de cabina de productos](/help/assets/CIF/product_cockpit_page_association.png)

## Cloud Manager {#cloud-manager}

Puede encontrar una lista completa de las versiones mensuales de Cloud Manager [aquí](/help/implementing/cloud-manager/release-notes/current.md).

## Herramientas de migración {#migration-tools}

Puede encontrar una lista completa de las versiones de las herramientas de migración [aquí](/help/journey-migration/release-notes/release-notes-migration-tools-current.md).
