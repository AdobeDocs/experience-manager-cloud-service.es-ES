---
title: Notas de la versión 2023.4.0 de la versión de  [!DNL Adobe Experience Manager]  as a Cloud Service.
description: Notas de la versión 2023.4.0 de la versión de  [!DNL Adobe Experience Manager]  as a Cloud Service.
exl-id: c34aedee-e45a-4e2a-ae7f-930bc0cc026f
feature: Release Information
role: Admin
source-git-commit: b4ffcddddfcd990c359380071f19b5442dee9eb2
workflow-type: tm+mt
source-wordcount: '1112'
ht-degree: 100%

---

# Notas de la versión 2023.4.0 para [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

En la siguiente sección se describen las notas de la versión de funciones de la versión 2023.4.0 de [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Desde aquí puede navegar hasta las notas de la versión de versiones anteriores, como 2021 o 2022.
>
>Eche un vistazo a la [Hoja de ruta de versiones de Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html?lang=es) para obtener más información acerca de las próximas activaciones de funcionalidades para [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Consulte [Actualizaciones recientes de la documentación](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html?lang=es) para obtener más información sobre las actualizaciones de la documentación no relacionadas directamente con una versión.

## Fecha de lanzamiento {#release-date}

La fecha de lanzamiento de la versión de funcionalidad actual de [!DNL Adobe Experience Manager] como [!DNL Cloud Service] (2023.4.0) es el 7 de junio de 2023. La próxima versión con funcionalidades (2023.6.0) está planificada para el 29 de junio de 2023.

## Vídeo de la versión {#release-video}

Eche un vistazo al vídeo Información general sobre la versión de abril de 2023 para ver un resumen de las funciones añadidas en la versión 2023.4.0:

>[!VIDEO](https://video.tv.adobe.com/v/3418681/?quality=12)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Nuevas funciones de [!DNL Experience Manager Sites] {#sites-features}

* Exporte fragmentos de contenido de AEM as a Cloud Service a Adobe Target en formato JSON y cree las ofertas JSON correspondientes en Target.
* Ahora, la compatibilidad con la paginación y la ordenación de GraphQL, junto con las mejoras en el almacenamiento en la caché interna, ayudan a mejorar el rendimiento de las aplicaciones cliente disociadas al recuperar grandes conjuntos de contenido de AEM mediante consultas y filtros complejos de GraphQL.

### Nuevas funciones en el canal de prelanzamiento de [!DNL Experience Manager Sites] {#prerelease-sites}

* Los fragmentos de contenido y sus referencias ahora se pueden publicar en el [Servicio de previsualización de AEM](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/manage-environments.html?lang=es#access-preview-service) mediante la [consola de fragmento de contenido](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/administering/content-fragments/content-fragments-console.html?lang=es), permitiendo a los usuarios previsualizar la experiencia final en una aplicación de vista previa disociada antes de lanzarse.
* Las imágenes se pueden optimizar dinámicamente para la entrega web en escenarios sin encabezado mediante AEM GraphQL. Las [variables de consulta](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/how-to/images.html?lang=es#query-variables) se pueden definir en las consultas de GraphQL para permitir que las aplicaciones cliente disociadas soliciten las imágenes optimizadas correspondientes de AEM.
* Las etiquetas en las [variaciones de fragmentos de contenido](https://experienceleague.adobe.com/docs/experience-manager-65/assets/content-fragments/content-fragments-variations.html?lang=es) ahora se pueden enviar a JSON mediante la API de entrega de contenido AEM GraphQL.

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Nuevas funciones de [!DNL Assets] {#assets-features}

* Se ha añadido compatibilidad con imágenes WebP para extraer automáticamente metadatos, generar miniaturas y representaciones personalizadas. Ahora, la capacidad de etiquetas inteligentes también es compatible con estos archivos. Las funciones de Dynamic Media no son compatibles con WebP como formato de entrada.

* [Mejoras en la experiencia de búsqueda](/help/assets/search-assets.md#aftersearch): ahora puede realizar rápidamente las siguientes operaciones en los archivos que se muestran en los resultados de búsqueda:

   * Crear un flujo de trabajo
   * Crear una versión
   * Relacionar o desrelacionar archivos

     No es necesario desplazarse a la ubicación del recurso y ver sus propiedades para realizar estas operaciones.

* Mejoras en la facilidad de uso de la faceta Búsqueda de color: el campo de entrada para valores de color ahora se puede editar y los resultados de búsqueda solo se actualizan al salir del selector de color.

* Lanzamiento de nuevo protocolo de asistencia (DASH - Dynamic Adaptive Streaming over HTTP) para streaming adaptable en la entrega de vídeo de Dynamic Media (con CMAF habilitado):
   * La transmisión adaptable (DASH/HLS) garantiza una mejor experiencia de visualización de vídeos por parte del usuario
   * DASH es el protocolo estándar internacional para la transmisión de vídeo adaptable y es ampliamente adoptado en el sector.

* _Instantánea_ de Dynamic Media: Experimento con imágenes de prueba o URL de Dynamic Media para ver el output de diferentes modificadores de imagen y evaluar las optimizaciones de imágenes inteligentes para el tamaño de archivo (con entrega WebP y AVIF), el ancho de banda de la red y la proporción de píxeles del dispositivo. Consulte la [Instantánea de Dynamic Media](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/dynamic-media/images/dynamic-media-snapshot.html?lang=es).

### Función en [!DNL Assets] versión preliminar {#prerelease-feature-assets}

* Dynamic Media: la interfaz de usuario de algunos campos relacionados con el recorte inteligente en un perfil de imagen ahora se actualiza para reflejar las directrices actuales para definir un recorte inteligente. Consulte las [Opciones de recorte](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/dynamicmedia/image-profiles.html?lang=es#crop-options).

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### Nuevas funciones disponibles en [!DNL Forms] {#new-features-available-in-channel}

* **[Envío de formularios adaptables a Microsoft® SharePoint y Microsoft OneDrive](/help/forms/configuring-submit-actions.md)**: mejore la agilidad del usuario empresarial para iniciar nuevos formularios rápidamente y almacenar los datos enviados en las herramientas habituales que utilizan, como el sitio de Microsoft SharePoint o la carpeta de OneDrive.

### Funciones de la versión preliminar [!DNL Forms] {#prerelease-features-forms}

* [Formularios adaptables en el editor de páginas de AEM](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md): ahora puede utilizar el editor de páginas de AEM para crear y agregar rápidamente varios formularios a sus páginas de Sites. Esta capacidad permite a los autores de contenido crear experiencias de captura de datos sin problemas dentro de las páginas de Sites mediante el uso de la potencia de los componentes de los formularios adaptables, incluido el comportamiento dinámico, las validaciones, la integración de datos, la generación de documentos de registro y la automatización del proceso empresarial. Puede hacer lo siguiente:

   * Cree un formulario adaptable arrastrando y soltando componentes de formulario en el componente contenedor de formularios adaptables en el editor de AEM Sites o en los fragmentos de experiencias.
   * Utilice el asistente de formularios adaptables dentro del editor de AEM Sites para poder crear formularios independientes de cualquier página de Sites, lo que le proporciona la libertad de reutilizar dichos formularios a través de varias páginas.
   * Agregue varios formularios a una página de Sites, lo que optimizará la experiencia del usuario y proporcionará una mayor flexibilidad.

     >[!VIDEO](https://video.tv.adobe.com/v/3419284?quality=12&learn=on)

* [Adobe Acrobat Sign Solutions para la Administración Pública](/help/forms/adobe-sign-integration-adaptive-forms.md): AEM Forms ahora se integra con Adobe Acrobat Sign Solutions para la Administración Pública. Esta integración proporciona un nivel avanzado de cumplimiento y seguridad para las firmas electrónicas con envíos de formularios adaptables para cuentas asociadas con el gobierno (departamentos y agencias gubernamentales).

  La integración con Adobe Acrobat Sign para la Administración Pública permite a los socios de Adobe y a los clientes de la administración pública utilizar firmas electrónicas en los formularios adaptables para algunas de las líneas de negocio más importantes y sensibles. Este nivel adicional de seguridad garantiza que todas las firmas electrónicas cumplan plenamente con la normativa FedRAMP Moderate, lo que proporciona tranquilidad a los clientes de la administración pública de Adobe.

* Tratamiento de errores mejorado con controladores de errores personalizados en el editor de reglas: ahora puede invocar una función personalizada (mediante la Biblioteca de clientes) en respuesta a un error devuelto por un servicio externo y proporcionar una respuesta personalizada a los usuarios finales. O bien, puede realizar acciones específicas en busca de errores devueltos por un servicio. Por ejemplo, puede invocar un flujo de trabajo personalizado en el back-end para códigos de error específicos o informar al cliente de que el servicio está inactivo.

  Esta funcionalidad ayuda a mejorar su capacidad general de gestión de errores mediante la introducción de respuestas de error basadas en estándares compatibles con los controladores de errores OOTB, con buena flexibilidad y control.

### Formularios adaptables sin encabezado, programa para primeros usuarios {#forms-early-adopter}

Utilice los formularios adaptables sin encabezado para que los desarrolladores puedan crear, publicar y gestionar formularios interactivos a los que se pueda acceder y con los que se pueda interactuar a través de API, en lugar de a través de una interfaz gráfica de usuario tradicional. Los formularios adaptables sin encabezado le ayudan a:

* crear formularios multicanal de alta calidad en el lenguaje de programación que desee
* integrar formularios de forma nativa en sus aplicaciones móviles y de escritorio, sitios web y aplicaciones de chat
* reutilizar los componentes de IU propios con aplicaciones de formularios
* aprovechar la potencia de Adobe Experience Manager Forms

Puede enviar un correo electrónico a `aem-forms-headless@adobe.com` desde su ID de correo electrónico oficial para unirse al programa de primeros usuarios.

## [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation {#foundation}

### Novedades {#what-is-new-foundation}

* Regiones de publicación adicionales: los clientes de Sites pueden obtener licencias de hasta tres regiones de publicación, además de la región principal. El tráfico se dirige a granjas de publicación adicionales, lo que da como resultado una menor latencia para determinadas solicitudes y una mayor resistencia frente a las interrupciones regionales. Póngase en contacto con el Administrador de cuentas de Adobe para obtener información sobre las licencias [Regiones de publicación adicionales](/help/operations/additional-publish-regions.md) para sus programas.

## Notas de la versión de mantenimiento {#maintenance}

Puede encontrar las últimas notas de la versión de mantenimiento [aquí](/help/release-notes/maintenance/latest.md).

## Cloud Manager {#cloud-manager}

Puede encontrar una lista completa de las versiones mensuales de Cloud Manager [aquí](/help/implementing/cloud-manager/release-notes/current.md).

## Herramientas de migración {#migration-tools}

Puede encontrar una lista completa de las versiones de las herramientas de migración [aquí](/help/journey-migration/release-notes/release-notes-migration-tools-current.md).
