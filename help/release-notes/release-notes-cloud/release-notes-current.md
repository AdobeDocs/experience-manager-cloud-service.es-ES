---
title: Notas de la versión actuales de  [!DNL Adobe Experience Manager]  as a Cloud Service.
description: Notas de la versión actuales de  [!DNL Adobe Experience Manager]  as a Cloud Service.
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
mini-toc-levels: 1
source-git-commit: 272225bbeea4443bf97349d11805dbb3386fd2cc
workflow-type: tm+mt
source-wordcount: '1092'
ht-degree: 15%

---


# Notas de la versión actuales de [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

En la siguiente sección se describen las notas de la versión generales de la versión actual (la más reciente) de [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Desde aquí puede navegar hasta las notas de versiones anteriores; por ejemplo, las de 2020, 2021, etc.

>[!NOTE]
>
>Consulte [Actualizaciones recientes de la documentación](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html?lang=es) para obtener más información sobre las actualizaciones de la documentación no relacionadas directamente con una versión.

>[!CAUTION]
>
>**Período de exclusión de mantenimiento planeado**
>
> No se ejecutará ningún mantenimiento automático de AEMaaCS durante los siguientes lapsos de tiempo, a partir y hasta la medianoche (00:00) CET:
>
>* Lunes, 21 de noviembre hasta lunes, 5 de diciembre
>* Lunes, 19 de diciembre hasta martes, 3 de enero


## Fecha de lanzamiento {#release-date}

La fecha de lanzamiento de [!DNL Adobe Experience Manager] como [!DNL Cloud Service] la versión mensual actual (2022.10.0) es el 10 de noviembre de 2022. La próxima versión mensual (2023.1.0) está planificada para el 26 de enero de 2023.

## Vídeo de la versión {#release-video}

Consulte el vídeo Información general de la versión de octubre de 2022 para ver un resumen de las funciones agregadas en la versión 2022.10.0:

>[!VIDEO](https://video.tv.adobe.com/v/3409801/?quality=12)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}


### Nuevas funciones de [!DNL Sites] {#sites-features}

* La variable [Pestaña Personalización para fragmentos de experiencias](/help/sites-cloud/authoring/fundamentals/experience-fragments.md#personalization-experience-fragment) permite al editor de fragmentos de experiencias capacidades de especificación de segmentación, así como la flexibilidad para crear fragmentos de experiencias anidados, mediante la cual se pueden crear variaciones de encabezados y pies de página para varios segmentos. Antes del lanzamiento de esta función, la personalización que ofrece AEM solo está disponible para páginas de sitio, pero no para fragmentos de experiencias

* La variable [Consola de fragmento de contenido](/help/sites-cloud/administering/content-fragments/content-fragments-console.md) ahora permite a los usuarios administrar de forma eficaz los fragmentos de contenido traducidos. Se ha proporcionado un acceso de 1 clic para ver todas las copias de idioma. Los usuarios también pueden filtrar la vista de tabla según la configuración regional de su interés.

![Idiomas de fragmentos de contenido](/help/release-notes/assets/cfconsole-languages.png)

* Reduzca aún más el tiempo de carga de las páginas de los visitantes optimizando la configuración de tamaño de las imágenes en las plantillas. Encontrará más información para el componente de imagen en [Componente principal de WCM](https://github.com/adobe/aem-core-wcm-components)

## [!DNL Experience Manager Assets] como [!DNL Cloud Service] {#assets}

### Nuevas funciones de [!DNL Assets] {#assets-features}

* Experience Manager Assets ahora le permite cargar documentos en otros tipos de formato compatibles y[ previsualizarlos con el visor del Document Cloud incluido](/help/assets/manage-pdf-documents.md). Los tipos de formato admitidos son TXT, RTF, DOC, DOCX, PPT, PPTX, XLS y XLSX.

   ![Representación del PDF para otros formatos](/help/release-notes/assets/multi-page-other-formats.png)


### Nuevas funciones de [!DNL Assets] versión preliminar {#prerelease-features-assets}

* Experience Manager Assets ahora utiliza un marco de inteligencia artificial mejorado para las etiquetas inteligentes de imagen. Esta inteligencia de contenido mejora la relevancia y precisión de las etiquetas inteligentes disponibles para todos los recursos de imagen durante la ingesta. Además, la información de orientación se rellena en `cq:tags`, lo que permite obtener mejores resultados de búsqueda mediante el filtro Orientación .

   Si está interesado en participar en la Beta, [rellenar este formulario](https://forms.office.com/pages/responsepage.aspx?id=Wht7-jR7h0OUrtLBeN7O4epXZrTVKKdJkUiHeolccf9UNEwyNEpHVEFaODdBNFZQSlFDREZQOVRRTy4u) para el 14 de noviembre.

* Experience Manager Assets ahora [admite token SAS](/help/assets/add-assets.md#asset-bulk-ingestor) además de la clave de acceso para la autenticación al conectarse al origen de datos de almacenamiento de blob de Azure para la ingesta de recursos mediante la herramienta de importación masiva.

## [!DNL Experience Manager Forms] como [!DNL Cloud Service] {#forms}

### Nuevas funciones disponibles en [!DNL Forms] {#new-features-available-in-channel}


* [Asistente para Forms adaptable](/help/forms/creating-adaptive-form.md): AEM Forms proporciona un asistente fácil de usar para las empresas que crea rápidamente Forms adaptable. El asistente dispone de un rápido desplazamiento por pestañas para seleccionar fácilmente plantillas preconfiguradas, estilos, campos y opciones de envío para crear un formulario adaptable. Esta versión incorpora las siguientes mejoras al asistente:

   * Seleccione o anule la selección de campos: El asistente le permite crear un formulario adaptable basado en esquemas JSON y del modelo de datos de formulario. Ahora puede seleccionar un subconjunto de campos dentro de un esquema para incluirlos en un formulario adaptable. Los campos seleccionados se convierten a los correspondientes componentes de captura de datos del formulario adaptable para crear rápidamente los formularios adaptables deseados.

   * Usar plantillas estáticas: Los clientes con inversiones existentes en plantillas estáticas heredadas pueden continuar con su recorrido de adopción en la nube mediante plantillas estáticas en el asistente para crear formularios adaptables. Esto proporciona a los clientes tiempo adicional para migrar plantillas estáticas antiguas a plantillas editables modernas.

* [Eliminar campos ocultos de un documento de registro (DoR) durante el procesamiento en el servidor](/help/forms/generate-document-of-record-for-non-xfa-based-adaptive-forms.md): Puede generar el PDF de documento de registro para los usuarios finales que contenga únicamente aquellos campos que les fueran visibles durante la experiencia de captura de datos. Al enviar el formulario, el servidor valida qué campos se ocultaron al usuario final en función de los datos enviados y excluye del documento de registro para mantener la coherencia.

### Nuevas funciones disponibles en el canal de prelanzamiento de [!DNL Forms] {#prerelease-features-forms}

* **Editor de plantillas de Forms adaptable**: El editor de plantillas le permite predefinir la estructura básica y el aspecto del Forms adaptable de una organización. Esta versión aporta las siguientes mejoras al editor de plantillas:
   * **[Modelo de datos de formulario en el editor de plantillas](/help/forms/creating-adaptive-form.md#edit-form-model-properties-of-an-adaptive-form-edit-form-model)**: Puede asociar un esquema del Modelo de datos de formulario a una plantilla de formulario adaptable en el editor de plantillas. Ayuda a reducir el tiempo necesario para crear un formulario adaptable. La opción también se agrega al editor de Forms adaptable para que los usuarios puedan seleccionar o cambiar el Modelo de datos de formulario para los formularios existentes.
   * **[Documento de registro en el editor de plantillas](/help/forms/generate-document-of-record-for-non-xfa-based-adaptive-forms.md#document-of-record-support-in-adaptive-form-editor-dor-support-in-adaptiveform)**: Ahora puede estandarizar la generación de documentos de registros para todos los formularios creados con una plantilla. Esto ayuda a mejorar el cumplimiento de normas y la estandarización de los requisitos de organización.

* **[Inicio del asistente de formularios adaptables desde una página de AEM Sites](/help/forms/embed-adaptive-form-aem-sites.md)**: La página de AEM Sites ha ampliado la compatibilidad con Adaptive Forms. Ahora puede crear un nuevo formulario adaptable o incrustar un formulario adaptable existente mientras permanece en la página de AEM Sites.
* **[Cambiar la alineación de visualización de las casillas de verificación y el botón de radio en DoR](/help/forms/generate-document-of-record-for-non-xfa-based-adaptive-forms.md#customize-the-branding-information-in-document-of-record-customize-the-branding-information-in-document-of-record)**: Ahora puede establecer la alineación deseada (Horizontal, Vertical, Igual que Forms adaptable) para la casilla de verificación y el botón de opción del Documento de registro. Esta opción determina el posicionamiento de las opciones de casilla de verificación y botón de radio en el Documento de registro.

## Complemento CIF {#cloud-services-cif}

### Novedades {#what-is-new-cif}

* Los autores pueden enriquecer dinámicamente listas de productos con fragmentos de experiencias (por ejemplo: colocar banner entre listas de productos).
* El componente de lista ahora admite páginas de productos o categorías asociadas para mostrar dinámicamente páginas relacionadas.
* Se ha añadido compatibilidad con los componentes de Peregrine 12.5.
* Se ha añadido compatibilidad con la carga de precios del lado del cliente en teaser y carrusel de productos.

## [!DNL Experience Manager as a Cloud Service] Foundation {#foundation}

### Novedades {#what-is-new-foundation}

* AEM as a Cloud Service (servicio de autor) está ahora integrado con Unified Shell para mejorar la experiencia del usuario y unificarla con todas las demás aplicaciones de Experience Cloud. Consulte AEM como [Cloud Service en Shell unificado](/help/overview/aem-cloud-service-on-unified-shell.md) para obtener más información.

* Como se mencionó anteriormente en las notas de la versión, el uso de la pantalla de administración del agente de replicación o la API de replicación para distribuir paquetes de contenido de más de 10 MB (nodos con propiedades, sin incluir binarios) está obsoleto y se aplicará en los próximos días. Consulte [Administrar publicación](/help/operations/replication.md#manage-publication) o [Flujo de trabajo Publicar árbol de contenido](/help/operations/replication.md#publish-content-tree-workflow) para los enfoques sugeridos para replicar estos paquetes de contenido grande.

* La configuración de Dispatcher ahora hace referencia a un archivo que enumera parámetros comunes de consulta de campañas de marketing. Los clientes pueden optar por descomentar los parámetros relevantes para ellos, lo que resulta en un mejor almacenamiento en caché. Consulte [Parámetros de campaña de marketing](/help/implementing/dispatcher/caching.md#marketing-parameters) para obtener más información.

## Cloud Manager {#cloud-manager}

Puede encontrar una lista completa de las versiones mensuales de Cloud Manager [aquí](/help/implementing/cloud-manager/release-notes-cloud-manager/release-notes-cm-current.md).

## Herramientas de migración {#migration-tools}

Puede encontrar una lista completa de las versiones de las herramientas de migración [aquí](/help/journey-migration/release-notes/release-notes-migration-tools-current.md).
