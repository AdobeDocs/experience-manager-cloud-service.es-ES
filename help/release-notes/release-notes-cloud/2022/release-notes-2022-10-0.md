---
title: Notas de la versión 2022.10.0 de la versión de  [!DNL Adobe Experience Manager]  as a Cloud Service.
description: Notas de la versión 2022.10.0 de la versión de  [!DNL Adobe Experience Manager]  as a Cloud Service.
source-git-commit: 599f924465552b2ef43827da8e139c239e47baed
workflow-type: tm+mt
source-wordcount: '850'
ht-degree: 96%

---


# Notas de la versión 2022.10.0 para [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

En la siguiente sección se describen las notas de la versión de las funciones de la versión 2022.10.0 de [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Desde aquí puede navegar hasta las notas de versiones anteriores; por ejemplo, las de 2020, 2021, etc.

>[!NOTE]
>
>Consulte [Actualizaciones recientes de la documentación](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html?lang=es) para obtener más información sobre las actualizaciones de la documentación no relacionadas directamente con una versión.

## Fecha de lanzamiento {#release-date}

La fecha de lanzamiento de [!DNL Adobe Experience Manager] como una versión mensual actual de [!DNL Cloud Service] (2022.10.0) es el 10 de noviembre de 2022. La próxima versión mensual (2023.1.0) está planificada para el 9 de febrero de 2023.

## Vídeo de la versión {#release-video}

Eche un vistazo al vídeo Información general sobre la versión de octubre de 2022 para ver un resumen de las funcionalidades añadidas en la versión 2022.10.0:

>[!VIDEO](https://video.tv.adobe.com/v/3409801/?quality=12)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}


### Nuevas funciones de [!DNL Sites] {#sites-features}

* La variable [Pestaña Personalización para fragmentos de experiencias](/help/sites-cloud/authoring/fundamentals/experience-fragments.md#personalization-experience-fragment) permite al editor de Fragmentos de experiencias capacidades de especificación de segmentación, así como la flexibilidad para crear Fragmentos de experiencias anidados, mediante los cuales se pueden crear variaciones de encabezados y pies de página para varios segmentos. Antes del lanzamiento de esta funcionalidad, la personalización que ofrece AEM solo está disponible para páginas de sitio, pero no para Fragmentos de experiencias

* La variable [Consola de fragmento de contenido](/help/sites-cloud/administering/content-fragments/content-fragments-console.md) ahora permite a los usuarios administrar de forma eficaz los fragmentos de contenido traducidos. Se ha proporcionado un acceso de 1 clic para ver todas las copias de idioma. Los usuarios también pueden filtrar la vista de tabla según la configuración regional de su interés.

![Idiomas de fragmentos de contenido](/help/release-notes/assets/cfconsole-languages.png)

* Reduzca aún más el tiempo de carga de las páginas para los visitantes optimizando la configuración de tamaño de las imágenes en las plantillas. Encontrará más información para el componente de imagen en [Componente principal de WCM](https://github.com/adobe/aem-core-wcm-components)

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Nuevas funciones de [!DNL Assets] {#assets-features}

* Experience Manager Assets ahora le permite cargar documentos en otros tipos de formato compatibles y [previsualizarlos con el visualizador de Document Cloud incluido](/help/assets/manage-pdf-documents.md). Los tipos de formato admitidos son TXT, RTF, DOC, DOCX, PPT, PPTX, XLS y XLSX.

   ![Representación del PDF para otros formatos](/help/release-notes/assets/multi-page-other-formats.png)


### Nuevas funciones en el canal de prelanzamiento de [!DNL Assets] {#prerelease-features-assets}

* Experience Manager Assets ahora utiliza un marco de inteligencia artificial mejorado para las etiquetas inteligentes de imagen. Esta inteligencia de contenido mejora la relevancia y precisión de las etiquetas inteligentes disponibles para todos los activos de imagen durante la ingesta. Además, la información de orientación se rellena en `cq:tags`, lo que permite obtener mejores resultados de búsqueda mediante el filtro Orientación.

   Si está interesado en participar en el Beta, [rellene este formulario](https://forms.office.com/pages/responsepage.aspx?id=Wht7-jR7h0OUrtLBeN7O4epXZrTVKKdJkUiHeolccf9UNEwyNEpHVEFaODdBNFZQSlFDREZQOVRRTy4u) para el 14 de noviembre.

* Experience Manager Assets ahora [admite el token SAS](/help/assets/add-assets.md#asset-bulk-ingestor) además de la clave de acceso para la autenticación al conectarse a la fuente de datos de almacenamiento de Azure Blob para la ingesta de activos mediante la herramienta de importación masiva.

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### Nuevas funciones disponibles en el canal de prelanzamiento de [!DNL Forms] {#prerelease-features-forms}

* **Editor de plantillas de Formularios adaptables**: el editor de plantillas le permite predefinir la estructura básica y el aspecto de los Formularios adaptables de una organización. Esta versión aporta las siguientes mejoras al editor de plantillas:
   * **[Modelo de datos de formulario en el editor de plantillas](/help/forms/creating-adaptive-form.md#edit-form-model-properties-of-an-adaptive-form-edit-form-model)**: puede asociar un esquema del Modelo de datos de formulario a una plantilla de Formulario adaptable en el editor de plantillas. Ayuda a reducir el tiempo necesario para crear un Formulario adaptable. La opción también se agrega al editor de Formularios adaptables para que los usuarios puedan seleccionar o cambiar el Modelo de datos de formulario para los formularios existentes.
   * **[Documento de registro en el editor de plantillas](/help/forms/generate-document-of-record-for-non-xfa-based-adaptive-forms.md#document-of-record-support-in-adaptive-form-editor-dor-support-in-adaptiveform)**: ahora puede estandarizar la generación de documentos de registros para todos los formularios creados con una plantilla. Esto ayuda a mejorar el cumplimiento de normas y la estandarización de los requisitos de organización.

* **[Lanzamiento del asistente de Formularios adaptables desde una página de AEM Sites](/help/forms/embed-adaptive-form-aem-sites.md)**: la página de AEM Sites ha ampliado la compatibilidad con Adaptive Forms. Ahora puede crear un nuevo Formulario adaptable o incrustar un Formulario adaptable existente mientras permanece en la página de AEM Sites.
* **[Cambiar la alineación de visualización de las casillas de verificación y el botón de opción en DoR](/help/forms/generate-document-of-record-for-non-xfa-based-adaptive-forms.md#customize-the-branding-information-in-document-of-record-customize-the-branding-information-in-document-of-record)**: ahora puede establecer la alineación deseada (Horizontal, Vertical, Igual que Formularios adaptables) para la casilla de verificación y el botón de opción del Documento de registro. Esta opción determina el posicionamiento de las opciones de casilla de verificación y botón de opción en el Documento de registro.

## Complemento CIF {#cloud-services-cif}

### Novedades {#what-is-new-cif}

* Los autores pueden enriquecer dinámicamente listas de productos con Fragmentos de experiencias (por ejemplo: colocar banner entre listas de productos).
* El componente de lista ahora admite páginas de productos o categorías asociados para mostrar dinámicamente páginas relacionadas.
* Se ha añadido compatibilidad con los componentes de Peregrine 12.5.
* Se ha añadido compatibilidad con la carga de precios del lado del cliente en teaser y carrusel de productos.

## [!DNL Experience Manager as a Cloud Service] Foundation {#foundation}

### Novedades {#what-is-new-foundation}

* AEM as a Cloud Service (Servicio de creación) está ahora integrado con Unified Shell para mejorar la experiencia del usuario y unificarlo con todas las demás aplicaciones de Experience Cloud. Consulte AEM as a [Cloud Service en Unified Shell](/help/overview/aem-cloud-service-on-unified-shell.md) para obtener más información.

* Como se mencionó anteriormente en las notas de la versión, el uso de la pantalla de administración del agente de replicación o la API de replicación para distribuir paquetes de contenido de más de 10 MB (nodos con propiedades, sin incluir binarios) está obsoleto y se aplicará en los próximos días. Consulte [Administrar publicación](/help/operations/replication.md#manage-publication) o el [flujo de trabajo Publicar árbol de contenido](/help/operations/replication.md#publish-content-tree-workflow) para los enfoques sugeridos para replicar estos paquetes grandes de contenido.

* La configuración de Dispatcher ahora hace referencia a un archivo que enumera parámetros comunes de consulta de campañas de marketing. Los clientes pueden optar por descomentar los parámetros relevantes para ellos, lo que resulta en un mejor almacenamiento en caché. Consulte [Parámetros de campaña de marketing](/help/implementing/dispatcher/caching.md#marketing-parameters) para obtener más información.

## Cloud Manager {#cloud-manager}

Puede encontrar una lista completa de las versiones mensuales de Cloud Manager [aquí.](/help/implementing/cloud-manager/release-notes/current.md)

## Herramientas de migración {#migration-tools}

Puede encontrar una lista completa de las versiones de las herramientas de migración [aquí](/help/journey-migration/release-notes/release-notes-migration-tools-current.md).
