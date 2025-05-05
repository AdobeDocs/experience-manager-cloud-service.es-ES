---
title: Notas de la versión 2023.6.0 de la versión de  [!DNL Adobe Experience Manager]  as a Cloud Service.
description: Notas de la versión 2023.6.0 de la versión de  [!DNL Adobe Experience Manager]  as a Cloud Service.
exl-id: 29cf9548-e413-4e4f-b233-d6bb04918b22
feature: Release Information
role: Admin
source-git-commit: f28f212574dda0ece2cedb56a714d381e5bd7d3c
workflow-type: tm+mt
source-wordcount: '1322'
ht-degree: 100%

---

# Notas de la versión 2023.6.0 para [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

En la siguiente sección se describen las notas de la versión de funciones de la versión 2023.6.0 de [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Desde aquí puede navegar hasta las notas de la versión de versiones anteriores, como 2021 o 2022.
>
>Eche un vistazo a la [Hoja de ruta de versiones de Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html?lang=es) para obtener más información acerca de las próximas activaciones de funcionalidades para [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Consulte [Actualizaciones recientes de la documentación](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html?lang=es) para obtener más información sobre las actualizaciones de la documentación no relacionadas directamente con una versión.

## Fecha de lanzamiento {#release-date}

La fecha de lanzamiento de la versión de funcionalidad actual de [!DNL Adobe Experience Manager] como [!DNL Cloud Service] (2023.6.0) fue el 29 de junio de 2023. La siguiente versión con funcionalidades (2023.7.0) está planificada para el 27 de julio de 2023.

## Vídeo de la versión {#release-video}

Eche un vistazo al vídeo Información general sobre la versión de junio de 2023 para ver un resumen de las funciones añadidas en la versión 2023.6.0.

>[!VIDEO](https://video.tv.adobe.com/v/3420971/?quality=12)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Nuevas funciones de [!DNL Experience Manager Sites] {#sites-features}

* Los fragmentos de contenido y sus referencias ahora se pueden publicar en el [Servicio de previsualización de AEM](/help/implementing/cloud-manager/manage-environments.md#access-preview-service) mediante la [consola de fragmento de contenido](/help/sites-cloud/administering/content-fragments/managing.md#content-fragments-console), permitiendo a los usuarios previsualizar la experiencia final en una aplicación de vista previa disociada antes de lanzarse.

![Vista previa en la consola de fragmentos de contenido](/help/assets/content-fragments-console-preview.png)

* Las imágenes se pueden optimizar dinámicamente para la entrega web en escenarios sin encabezado mediante AEM GraphQL. Las [variables de consulta](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/how-to/images.html?lang=es#query-variables) se pueden definir en las consultas de GraphQL para permitir que las aplicaciones cliente disociadas soliciten las imágenes optimizadas correspondientes de AEM.
* Las etiquetas en las [variaciones de fragmentos de contenido](https://experienceleague.adobe.com/docs/experience-manager-65/assets/content-fragments/content-fragments-variations.html?lang=es) ahora se pueden enviar a JSON mediante la API de entrega de contenido AEM GraphQL.

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Nuevas funciones de [!DNL Assets] {#assets-features}

**Disponibilidad de la nueva vista de recursos**

La [nueva vista de recursos](/help/assets/assets-view-introduction.md) está ahora disponible en Experience Manager Assets. La vista de recursos proporciona la interfaz de usuario simplificada de Assets Essentials, lo que facilita la administración, la detección y la distribución de sus recursos digitales. La experiencia está dirigida a creativos, consumidores de recursos de solo lectura y usuarios de DAM de menor peso.

![Administración de etiquetado](/help/assets/assets/my-workspace.png)

**Mejoras en la experiencia de búsqueda**

Experience Manager Assets ahora le permite hacer más desde la interfaz de usuario de los resultados de búsqueda: Ahora puede hacer lo siguiente:

* [Realizar búsquedas dentro de la ubicación actual del repositorio](/help/assets/search-assets.md) de forma predeterminada, en lugar de buscar la palabra clave en todo el repositorio.

* [Ir a la ubicación de la carpeta](/help/assets/search-assets.md#aftersearch) para recursos que se muestran en los resultados de búsqueda.

**Vistas previas de miniaturas para recursos 3D**

[!DNL Experience Manager Assets] genera ahora [vistas previas de miniaturas para formatos de archivo 3D comunes](/help/assets/file-format-support.md) incluidos gLB, USDz, FBX, 3DS, OBJ y SBSAR. Cuando se cargan estos archivos, las miniaturas se generan automáticamente de forma predeterminada.

**Dynamic Media: se han actualizado los campos relacionados con los recortes inteligentes en el perfil de imagen**

La interfaz de usuario de algunos campos relacionados con el recorte inteligente en un perfil de imagen se actualiza ahora para reflejar las directrices actuales para definir un recorte inteligente. Consulte las [Opciones de recorte](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/dynamicmedia/image-profiles.html?lang=es#crop-options).

### Nuevas funciones de la vista Recursos {#assets-view-features}

**Etiquetado jerárquico de recursos para una experiencia de búsqueda más rápida**

Las listas planas de vocabularios controlados se vuelven inmanejables con el tiempo. La vista de recursos admite ahora [estructura jerárquica de etiquetado](/help/assets/tagging-management-assets-view.md), que facilita la aplicación de metadatos relevantes, la categorización de recursos, la compatibilidad con la búsqueda, la reutilización de etiquetas, la mejora de la capacidad de detección, etc.

![Administración de etiquetas](/help/assets/assets/tags-hierarchy.png)

**Fijación de archivos, carpetas y colecciones para un acceso más rápido**

Ahora puede [fijar archivos, carpetas y colecciones para un acceso más rápido](/help/assets/my-workspace-assets-view.md) a estos elementos cuando los necesite más tarde. Los elementos anclados se muestran en la sección **Acceso rápido** de Mi espacio de trabajo. Puede acceder a ellos mediante Mi espacio de trabajo en lugar de desplazarse a la ubicación en la que se guardan en el repositorio.

![Tareas en el espacio de trabajo](/help/assets/assets/quick-access.png)

**Filtrar recursos en la carpeta Papelera**

La vista de recursos ahora le permite [filtrar recursos disponibles en la carpeta Papelera](/help/assets/navigate-assets-view.md). Puede aplicar filtros estándar o personalizados para buscar los recursos adecuados en la carpeta Papelera y restaurarlos o eliminarlos de forma permanente.

**Vistas previas de miniaturas para recursos 3D**

La vista de recursos ahora genera vistas previas de miniaturas para formatos de archivo 3D comunes, incluidos gLB, USDz, FBX, 3DS, OBJ y SBSAR. Cuando estos archivos se cargan en la vista Recursos, el sistema genera las miniaturas automáticamente de forma predeterminada.

![Tareas en el espacio de trabajo](/help/assets/assets/3d-preview.png)

**Ver los términos más buscados**

La vista de recursos ahora admite [visualización de los términos más buscados en la implementación](/help/assets/my-workspace-assets-view.md) uso de la sección **Insights** de Mi espacio de trabajo. También puede navegar a Perspectivas detalladas para ver las búsquedas principales durante los últimos 30 días o 12 meses.

![Tareas en el espacio de trabajo](/help/assets/assets/insights-top-searches.png)

**Mejoras en los formularios de metadatos**

La vista de recursos ahora le permite [añadir texto de varios valores y componentes de propiedad de lista desplegable](/help/assets/metadata-assets-view.md#property-components) a los formularios de metadatos.

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### Nuevas funciones disponibles en [!DNL Forms] {#new-features-available-in-channel}

* [Formularios adaptables en el editor de páginas de AEM](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md): ahora puede utilizar el editor de páginas de AEM para crear y agregar rápidamente varios formularios a sus páginas de Sites. Esta capacidad permite a los autores de contenido crear experiencias de captura de datos sin problemas dentro de las páginas de Sites mediante el uso de la potencia de los componentes de los formularios adaptables, incluido el comportamiento dinámico, las validaciones, la integración de datos, la generación de documentos de registro y la automatización del proceso empresarial. Puede hacer lo siguiente:

   * Cree un formulario adaptable arrastrando y soltando componentes de formulario en el componente contenedor de formularios adaptables en el editor de AEM Sites o en los fragmentos de experiencias.
   * Utilice el asistente de formularios adaptables dentro del editor de AEM Sites para poder crear formularios independientes de cualquier página de Sites, lo que le proporciona la libertad de reutilizar dichos formularios a través de varias páginas.
   * Agregue varios formularios a una página de Sites, lo que optimizará la experiencia del usuario y proporcionará una mayor flexibilidad.

     >[!VIDEO](https://video.tv.adobe.com/v/3419284?quality=12&learn=on)

* [Adobe Acrobat Sign Solutions para la Administración Pública](/help/forms/adobe-sign-integration-adaptive-forms.md): AEM Forms ahora se integra con Adobe Acrobat Sign Solutions para la Administración Pública. Esta integración proporciona un nivel avanzado de cumplimiento y seguridad para las firmas electrónicas con envíos de formularios adaptables para cuentas asociadas con el gobierno (departamentos y agencias gubernamentales).

  La integración con Adobe Acrobat Sign Solutions para la Administración Pública permite a los socios de Adobe y a los clientes de la administración pública utilizar firmas electrónicas en los formularios adaptables para algunas de las líneas de negocio más importantes y confidenciales. Este nivel adicional de seguridad garantiza que todas las firmas electrónicas cumplan plenamente con la normativa FedRAMP Moderate, lo que proporciona tranquilidad a los clientes de la administración pública de Adobe.

* [Tratamiento de errores mejorado con controladores de error personalizados en el editor de reglas](/help/forms/add-custom-error-handler-adaptive-forms.md): ahora puede invocar una función personalizada (mediante la Biblioteca de clientes) en respuesta a un error devuelto por un servicio externo y proporcionar una respuesta adaptada a los usuarios finales. O bien, puede realizar acciones específicas en busca de errores devueltos por un servicio. Por ejemplo, puede invocar un flujo de trabajo personalizado en el back-end para códigos de error específicos o informar al cliente de que el servicio está inactivo.

  Esta funcionalidad ayuda a mejorar su capacidad general de gestión de errores mediante la introducción de respuestas de error basadas en estándares compatibles con los controladores de errores OOTB, con buena flexibilidad y control.

* [Métodos de autenticación mejorados para el modelo de datos de formulario](/help/forms/configure-data-sources.md): disfrute de una mayor seguridad con la introducción de la autenticación basada en credenciales de cliente para conectar AEM Forms con fuentes de datos compatibles. Esta mejora elimina la necesidad de suplantación o inicio de sesión del usuario, lo que refuerza la protección de los datos.

* [Formularios adaptables con secciones repetibles](/help/forms/create-forms-repeatable-sections.md): ahora puede hacer que los componentes [Acordeón](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms//adaptive-forms-components/accordion.html?lang=es), [Asistente](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/wizard.html?lang=es), [Panel](https://experienceleague.adobe.com/es/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/panel) y [Pestañas horizontales](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/horizontal-tabs.html?lang=es) en un formulario adaptable basado en componentes principales para crear secciones repetibles.

  >[!VIDEO](https://video.tv.adobe.com/v/3421052/adaptive-forms-repeatable-sections-repeat-sections/?quality=12&learn=on)

  Estas secciones repetibles le permiten proporcionar un número ilimitado de entradas sin un recuento de campos fijo. Resulta útil cuando se desconocen de antemano las instancias de datos requeridas. Los usuarios de Forms pueden agregar o quitar secciones fácilmente, lo que permite que los formularios se adapten a diferentes escenarios de entrada de datos y simplifica la recopilación de varias ocurrencias de los mismos datos.

* **[Envío de formularios adaptables a Microsoft® SharePoint y Microsoft® OneDrive](/help/forms/configuring-submit-actions.md)**: mejore la agilidad del usuario empresarial para iniciar nuevos formularios rápidamente y almacenar los datos enviados en las herramientas habituales que utilizan, como el sitio de Microsoft® SharePoint o la carpeta de OneDrive.

### Formularios adaptables sin encabezado, programa para primeros usuarios {#forms-early-adopter}

Utilice los [Formularios adaptables sin encabezado](https://experienceleague.adobe.com/docs/experience-manager-headless-adaptive-forms/using/overview.html?lang=es) para que los desarrolladores puedan crear, publicar y gestionar formularios interactivos a los que se pueda acceder y con los que se pueda interactuar a través de API, en lugar de a través de una interfaz gráfica de usuario tradicional. Los formularios adaptables sin encabezado le ayudan a:

* crear formularios multicanal de alta calidad en el lenguaje de programación que desee
* integrar formularios de forma nativa en sus aplicaciones móviles y de escritorio, sitios web y aplicaciones de chat
* reutilizar los componentes de IU propios con aplicaciones de formularios
* aprovechar la potencia de Adobe Experience Manager Forms

Puede enviar un correo electrónico a `aem-forms-headless@adobe.com` desde su ID de correo electrónico oficial para unirse al programa de primeros usuarios.

## Notas de la versión de mantenimiento {#maintenance}

Puede encontrar las últimas notas de la versión de mantenimiento [aquí](/help/release-notes/maintenance/latest.md).

## Cloud Manager {#cloud-manager}

Puede encontrar una lista completa de las versiones mensuales de Cloud Manager [aquí](/help/implementing/cloud-manager/release-notes/current.md).

## Herramientas de migración {#migration-tools}

Puede encontrar una lista completa de las versiones de las herramientas de migración [aquí](/help/journey-migration/release-notes/release-notes-migration-tools-current.md).
