---
title: Notas de la versión 2023.2.0 de la versión de [!DNL Adobe Experience Manager] as a Cloud Service.
description: Notas de la versión 2023.2.0 de la versión de [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: 671056e6-84cc-4c2c-bca3-fde68d5cc835
source-git-commit: a77e5dc4273736b969e9a4a62fcac75664495ee6
workflow-type: tm+mt
source-wordcount: '730'
ht-degree: 98%

---

# Notas de la versión 2023.2.0 para [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

En la siguiente sección se describen las notas de la versión de funciones de la versión 2023.2.0 de [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Desde aquí puede navegar hasta las notas de versiones anteriores; por ejemplo, las de 2021, 2022, etc.
>
>Eche un vistazo a la [Hoja de ruta de versiones de Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html?lang=es) para obtener más información acerca de las próximas activaciones de funcionalidades para [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Consulte [Actualizaciones recientes de la documentación](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html?lang=es) para obtener más información sobre las actualizaciones de la documentación no relacionadas directamente con una versión.

## Fecha de la versión {#release-date}

La fecha de lanzamiento de la versión de funcionalidad actual de [!DNL Adobe Experience Manager] como [!DNL Cloud Service] (2023.2.0) es el 12 de abril de 2023. La próxima versión con funcionalidades (2023.4.0) está planificada para el 7 de junio de 2023.

## Vídeo de la versión {#release-video}

Eche un vistazo al vídeo de información general sobre la versión de febrero de 2023 para ver un resumen de las funciones añadidas en la versión 2023.2.0:

>[!VIDEO](https://video.tv.adobe.com/v/3416885/?quality=12)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Nuevas funciones en el prelanzamiento de [!DNL Experience Manager Sites] {#prerelease-sites}

* Exportar fragmentos de contenido de AEM as a Cloud Service a Adobe target como ofertas JSON.
* Ahora, la compatibilidad con la paginación y la ordenación de GraphQL, junto con las mejoras en el almacenamiento en caché interno, ayudan a mejorar el rendimiento de las aplicaciones cliente disociadas al recuperar grandes conjuntos de contenido de AEM mediante consultas y filtros complejos de GraphQL.

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Nuevas funciones de [!DNL Assets] {#assets-features}

* Nuevo protocolo (DASH - Dynamic Adaptive Streaming over HTTP) compatible con el flujo adaptable en la entrega de vídeo de Dynamic Media (con CMAF habilitado):
   * El streaming adaptable (DASH/HLS) garantiza una mejor experiencia de visualización de los vídeos por parte del usuario
   * DASH es el protocolo estándar internacional para la transmisión de vídeo adaptable y es ampliamente adoptado en el sector
   * Disponible en NA, que se habilitará mediante ticket de soporte, próximamente en APAC, EMEA

* Se ha añadido compatibilidad con imágenes WebP para extraer automáticamente metadatos, generar miniaturas y representaciones personalizadas. Ahora, las funciones Smart Tag y Smart Crop también son compatibles con estos archivos.

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### Nuevas funciones disponibles en [!DNL Forms] {#new-features-available-in-channel}

* **[Uso de los componentes principales de captura de datos para crear formularios adaptables](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=es)**: [use el editor de formularios adaptables](/help/forms/creating-adaptive-form-core-components.md) para crear formularios basados en componentes de captura de datos estandarizados (componentes principales). Estos componentes proporcionan funcionalidades de personalización, un tiempo de desarrollo reducido y costes de mantenimiento más bajos para sus experiencias de inscripción digital.

* **[Compatibilidad de canalización front-end para aplicar estilo a componentes principales basados en formularios adaptables](/help/forms/using-themes-in-core-components.md)**: utilice temáticas estandarizadas basadas en BEM para formularios adaptables basados en componentes principales implementándolas con la canalización de implementación de front-end para mejorar la apariencia de sus formularios y adáptelas las directrices de diseño aprobadas para la marca de su organización.

* **[Generar documento de registro para Formularios adaptables basados en componentes principales](/help/forms/generate-document-of-record-core-components.md)**: Cree un documento de registro que contenga datos enviados para formularios adaptables creados con componentes principales para archivarlos o hacer referencia a usuarios finales, impresos o en formato de documento.

![https://www.aemcomponents.dev/](/help/forms/assets/sample-core-components-based-adaptive-form.png)

* **[Creación eficaz de formularios con la función Guardar un formulario adaptable como plantilla](/help/forms/template-editor.md#save-an-adaptive-form-as-template-saving-adaptive-form-as-template)**: Acelere y estandarice el desarrollo de formularios guardando los formularios existentes aprobados por marca como plantillas de formulario para reutilizarlos rápidamente.

* **[Conectar AEM Forms a bases de datos compatibles con JDBC](/help/forms/configure-data-sources.md#configure-relational-database-configure-relational-database)**: conéctese a bases de datos empresariales directamente desde AEM Cloud Service mediante el protocolo JDBC, sin necesidad de exponerlas a través de la API de REST.

* **[Integración con puntos de conexión REST mediante la API abierta 3.0](/help/forms/configure-data-sources.md#configure-restful-services-open-api-specification-version-20-configure-restful-services-swagger-version30)**: integración perfecta en sistemas de registro compatibles con la API abierta 3.0 para almacenar y recuperar datos mediante modelos de datos de formularios.

* **[Compartir un formulario adaptable para su revisión](/help/forms/create-reviews-forms.md)**: utilice el mecanismo de revisión de formularios adaptables para permitir que uno o más revisores revisen el formulario.


### Funciones de la versión preliminar [!DNL Forms] {#prerelease-features-forms}

* **[Envío de formularios adaptables a Microsoft SharePoint y Microsoft OneDrive](/help/forms/configuring-submit-actions.md)**: mejore la agilidad de los usuarios empresariales para iniciar nuevos formularios rápidamente y almacenar los datos enviados en las herramientas habituales que utilizan, como el sitio de Microsoft SharePoint o la carpeta de OneDrive.

![Envío de formularios adaptables a Microsoft SharePoint y Microsoft OneDrive](/help/forms/assets/onedrive-and-sharepoint.jpg)


## Formularios adaptables sin encabezado, programa para primeros usuarios {#forms-early-adopter}

Utilice los formularios adaptables sin encabezado para que los desarrolladores puedan crear, publicar y gestionar formularios interactivos a los que se pueda acceder y con los que se pueda interactuar a través de API, en lugar de a través de una interfaz gráfica de usuario tradicional. Los formularios adaptables sin encabezado le ayudan a:

* crear formularios multicanal de alta calidad en el lenguaje de programación que desee
* integrar formularios de forma nativa en sus aplicaciones móviles y de escritorio, sitios web y aplicaciones de chat
* reutilizar los componentes de IU propios con aplicaciones de formularios
* aprovechar la potencia de Adobe Experience Manager Forms

Puede enviar un correo electrónico a aem-forms-headless@adobe.com desde su ID de correo electrónico oficial para unirse al programa de primeros usuarios.

## Notas de la versión de mantenimiento {#maintenance}

Puede encontrar las últimas notas de la versión de mantenimiento [aquí](/help/release-notes/maintenance/latest.md).

## Cloud Manager {#cloud-manager}

Puede encontrar una lista completa de las versiones mensuales de Cloud Manager [aquí](/help/implementing/cloud-manager/release-notes/current.md).

## Herramientas de migración {#migration-tools}

Puede encontrar una lista completa de las versiones de las herramientas de migración [aquí](/help/journey-migration/release-notes/release-notes-migration-tools-current.md).
