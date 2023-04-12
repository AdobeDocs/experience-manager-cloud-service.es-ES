---
title: Notas de la versión actuales de  [!DNL Adobe Experience Manager]  as a Cloud Service.
description: Notas de la versión actuales de  [!DNL Adobe Experience Manager]  as a Cloud Service.
mini-toc-levels: 1
source-git-commit: 085ce15ebe4d48d32a437f13e728f60cfc57d0fa
workflow-type: tm+mt
source-wordcount: '733'
ht-degree: 33%

---


# Notas de la versión actuales de [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

En la siguiente sección se describen las notas de la versión de la funcionalidad actual (la más reciente) de [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Desde aquí puede navegar hasta las notas de versiones anteriores; por ejemplo, las de 2021, 2022, etc.
>
>Eche un vistazo a la [Hoja de ruta de versiones de Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html?lang=es) para obtener más información acerca de las próximas activaciones de funcionalidades para [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Consulte [Actualizaciones recientes de la documentación](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html?lang=es) para obtener más información sobre las actualizaciones de la documentación no relacionadas directamente con una versión.

## Fecha de la versión {#release-date}

La fecha de lanzamiento de [!DNL Adobe Experience Manager] como [!DNL Cloud Service] la versión de la función actual (2023.2.0) es el 12 de abril de 2023. La próxima versión de la función (2023.4.0) está planificada para el 27 de abril de 2023.

## Vídeo de la versión {#release-video}

Consulte el vídeo Información general de la versión de febrero de 2023 para ver un resumen de las funciones agregadas en la versión 2023.2.0:

>[!VIDEO](https://video.tv.adobe.com/v/3416885/?quality=12)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Nuevas funciones de [!DNL Experience Manager Sites] preasing {#prerelease-sites}

* Exportar fragmentos de contenido de AEM as a cloud service a Adobe target como ofertas JSON.
* Ahora, la compatibilidad con la paginación y la ordenación de GraphQL, junto con las mejoras en el almacenamiento en caché interno, ayudan a mejorar el rendimiento de las aplicaciones cliente disociadas al recuperar grandes conjuntos de contenido de AEM mediante consultas y filtros complejos de GraphQL.

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Nuevas funciones de [!DNL Assets] {#assets-features}

* Nuevo protocolo (DASH - Dynamic Adaptive Streaming over HTTP) compatible con el flujo adaptable en la entrega de vídeo de Dynamic Media (con CMAF habilitado):
   * La transmisión adaptable (DASH/HLS) garantiza una mejor experiencia de visualización de vídeos por parte del usuario final
   * DASH es el protocolo estándar internacional para la transmisión de vídeo adaptable y es ampliamente adoptado en el sector
   * Disponible en NA, que se habilitará mediante ticket de soporte, próximamente en APAC, EMEA

* Se ha añadido compatibilidad con imágenes WebP para extraer automáticamente metadatos, generar miniaturas y representaciones personalizadas. Ahora, las funciones Smart Tag y Smart Crop también son compatibles con estos archivos.

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### Nuevas funciones disponibles en [!DNL Forms] {#new-features-available-in-channel}

* **[Uso de los componentes principales de captura de datos para crear formularios adaptables](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=es)**: [use el editor de formularios adaptables](/help/forms/creating-adaptive-form-core-components.md) para crear formularios basados en componentes de captura de datos estandarizados (componentes principales). Estos componentes proporcionan funcionalidades de personalización, un tiempo de desarrollo reducido y costes de mantenimiento más bajos para sus experiencias de inscripción digital.

* **[Compatibilidad con la canalización de front-end para el diseño de Forms adaptable basado en componentes principales](/help/forms/using-themes-in-core-components.md)**: Utilice los temas estandarizados basados en BEM para Forms adaptable basado en componentes principales al implementarlos con la canalización de implementación de Frontend para mejorar el aspecto de los formularios y alinearlos con las directrices de diseño aprobadas por la marca de su organización.

* **[Generar documento de registro para Forms adaptable basado en componentes principales](/help/forms/generate-document-of-record-core-components.md)**: Cree un documento de registro que contenga datos enviados para Adaptive Forms creados con componentes principales para archivarlos o hacer referencia a usuarios finales, impresos o en formato de documento.

![https://www.aemcomponents.dev/](/help/forms/assets/sample-core-components-based-adaptive-form.png)

* **[Creación eficaz de formularios con la función Guardar un formulario adaptable como plantilla](/help/forms/template-editor.md#save-an-adaptive-form-as-template-saving-adaptive-form-as-template)**: Acelere y estandarice el desarrollo de formularios guardando los formularios existentes aprobados por marca como plantillas de formulario para reutilizarlos rápidamente.

* **[Conectar AEM Forms a bases de datos compatibles con JDBC](/help/forms/configure-data-sources.md#configure-relational-database-configure-relational-database)**: Conéctese a bases de datos empresariales directamente desde AEM Cloud Service mediante el protocolo JDBC, sin necesidad de exponerlas a través de la API de REST.

* **[Integración con puntos de conexión REST mediante la API abierta 3.0](/help/forms/configure-data-sources.md#configure-restful-services-open-api-specification-version-20-configure-restful-services-swagger-version30)**: Integre sin problemas en sistemas de registro compatibles con Open API 3.0 para almacenar y recuperar datos mediante modelos de datos de formulario.

* **[Compartir un formulario adaptable para su revisión](/help/forms/create-reviews-forms.md)**: utilice el mecanismo de revisión de formularios adaptables para permitir que uno o más revisores revisen el formulario.


### Funciones de [!DNL Forms] versión preliminar {#prerelease-features-forms}

* **[Envío de Forms adaptable a Microsoft SharePoint y Microsoft OneDrive](/help/forms/configuring-submit-actions.md)**: Mejore la agilidad del usuario empresarial para iniciar nuevos formularios rápidamente y almacenar los datos enviados en herramientas cotidianas que utilizan, como el sitio SharePoint de Microsoft o la carpeta OneDrive.

![Envío de Forms adaptable a Microsoft SharePoint y Microsoft OneDrive](/help/forms/assets/onedrive-and-sharepoint.jpg)


## Programa de adopción anticipada de Forms adaptable sin objetivos {#forms-early-adopter}

Utilice Forms adaptable sin encabezado para permitir a los desarrolladores crear, publicar y administrar formularios interactivos a los que se puede acceder e interactuar mediante API, en lugar de a través de una interfaz gráfica de usuario tradicional. Los formularios adaptables sin encabezado le ayudan a:

* cree formularios multicanal de alta calidad en el lenguaje de programación que elija
* integrar de forma nativa formularios en aplicaciones de escritorio y móviles, sitios web y aplicaciones de chat
* reutilizar los componentes de IU propietarios con aplicaciones de formularios
* aprovechar la potencia de Adobe Experience Manager Forms

Puede enviar un correo electrónico a aem-forms-headless@adobe.com desde su ID de correo electrónico oficial para unirse al programa de adopción anticipada.

## Notas de la versión de mantenimiento {#maintenance}

Puede encontrar las últimas notas de la versión de mantenimiento [aquí](/help/release-notes/maintenance/latest.md).

## Cloud Manager {#cloud-manager}

Puede encontrar una lista completa de las versiones mensuales de Cloud Manager [aquí.](/help/implementing/cloud-manager/release-notes/current.md)

## Herramientas de migración {#migration-tools}

Puede encontrar una lista completa de las versiones de las herramientas de migración [aquí](/help/journey-migration/release-notes/release-notes-migration-tools-current.md).
