---
title: Notas de la versión actuales de  [!DNL Adobe Experience Manager]  as a Cloud Service.
description: Notas de la versión actuales de  [!DNL Adobe Experience Manager]  as a Cloud Service.
mini-toc-levels: 1
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
source-git-commit: ca4046a94301cebae9e7a46e055977419fedd14e
workflow-type: tm+mt
source-wordcount: '1095'
ht-degree: 32%

---

# Notas de la versión actuales de [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

En la siguiente sección se describen las notas de la versión de la funcionalidad actual (la más reciente) de [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Desde aquí puede navegar hasta las notas de versiones anteriores, como 2021 o 2022.
>
>Eche un vistazo a la [Hoja de ruta de versiones de Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html?lang=es) para obtener más información acerca de las próximas activaciones de funcionalidades para [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Consulte [Actualizaciones recientes de la documentación](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html?lang=es) para obtener más información sobre las actualizaciones de la documentación no relacionadas directamente con una versión.

## Fecha de la versión {#release-date}

La fecha de lanzamiento de [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] la versión de la función actual (2023.4.0) es el 7 de junio de 2023. La próxima versión de la funcionalidad (2023.6.0) está planificada para el 29 de junio de 2023.

## Vídeo de la versión {#release-video}

Eche un vistazo al vídeo Información general sobre la versión de abril de 2023 para ver un resumen de las funciones añadidas en la versión 2023.4.0:

>[!VIDEO](https://video.tv.adobe.com/v/3418681/?quality=12)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Nuevas funciones de [!DNL Experience Manager Sites] {#sites-features}

* Exportar fragmentos de contenido de AEM as a Cloud Service a Adobe target como ofertas JSON.
* Ahora, la compatibilidad con la paginación y la ordenación de GraphQL, junto con las mejoras en el almacenamiento en caché interno, ayudan a mejorar el rendimiento de las aplicaciones cliente disociadas al recuperar grandes conjuntos de contenido de AEM mediante consultas y filtros complejos de GraphQL.

### Nuevas funciones en el canal de prelanzamiento de [!DNL Experience Manager Sites] {#prerelease-sites}

* Los fragmentos de contenido y sus referencias ahora se pueden publicar en [AEM Servicio de previsualización de](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/manage-environments.html?lang=en#access-preview-service) uso del [Consola de fragmento de contenido](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/administering/content-fragments/content-fragments-console.html?lang=en), permitiendo a los usuarios previsualizar la experiencia final en una aplicación de vista previa disociada antes de lanzarse.

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Nuevas funciones de [!DNL Assets] {#assets-features}

* Se ha añadido compatibilidad con imágenes WebP para extraer automáticamente metadatos, generar miniaturas y representaciones personalizadas. La capacidad Etiquetas inteligentes ahora también se admite para estos archivos. Las funciones de Dynamic Media no son compatibles con WebP como formato de entrada.

* [Mejoras en la experiencia de búsqueda](/help/assets/search-assets.md#aftersearch) : Ahora puede realizar rápidamente las siguientes operaciones en los recursos que se muestran en los resultados de búsqueda:

   * Creación de un flujo de trabajo
   * Crear una versión
   * Relacionar o desrelacionar recursos

     No es necesario desplazarse a la ubicación del recurso y ver sus propiedades para realizar estas operaciones.

* Mejoras en la facilidad de uso de la faceta Búsqueda de color: el campo de entrada para valores de color ahora se puede editar y los resultados de búsqueda solo se actualizan al salir del selector de color.

* Se ha lanzado la nueva compatibilidad de protocolo (DASH - Dynamic Adaptive Streaming over HTTP) para el streaming adaptable en la entrega de vídeo de Dynamic Media (con CMAF habilitado):
   * La transmisión adaptable (DASH/HLS) garantiza una mejor experiencia de visualización de vídeos por parte del usuario final
   * DASH es el protocolo estándar internacional para la transmisión de vídeo adaptable y es ampliamente adoptado en el sector
   * Disponible en todas las regiones, para habilitar mediante ticket de asistencia

* Dynamic Media _Instantánea_ : Experimente con imágenes de prueba o URL de Dynamic Media para ver la salida de diferentes modificadores de imagen y evaluar las optimizaciones de imágenes inteligentes para el tamaño de archivo (con entrega WebP y AVIF), el ancho de banda de la red y la proporción de píxeles del dispositivo. Consulte [Instantánea Dynamic Media](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/dynamic-media/images/dynamic-media-snapshot.html).

### Función en [!DNL Assets] versión preliminar {#prerelease-feature-assets}

* Dynamic Media: la interfaz de usuario de algunos campos relacionados con el recorte inteligente en un perfil de imagen ahora se actualiza para reflejar las directrices actuales para definir un recorte inteligente. Consulte [Opciones de recorte](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/dynamicmedia/image-profiles.html?lang=en#crop-options).

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### Nuevas funciones disponibles en [!DNL Forms] {#new-features-available-in-channel}

* **[Enviar Forms adaptable a Microsoft® SharePoint y Microsoft® OneDrive](/help/forms/configuring-submit-actions.md)**: mejore la agilidad del usuario empresarial para que pueda iniciar nuevos formularios rápidamente y almacenar los datos enviados en las herramientas diarias que utilizan, como el sitio de Microsoft® SharePoint o la carpeta de OneDrive.

### Funciones de la versión preliminar [!DNL Forms] {#prerelease-features-forms}

* [Forms AEM adaptable en el editor de páginas de la](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md)AEM : ahora puede utilizar el Editor de páginas de para crear y agregar rápidamente varios formularios a las páginas de Sites. Esta capacidad permite a los autores de contenido crear experiencias de captura de datos sin problemas dentro de las páginas de Sites mediante la potencia de los componentes de los formularios adaptables, incluido el comportamiento dinámico, las validaciones, la integración de datos, la generación de documentos de registro y la automatización de los procesos empresariales. Puede hacer lo siguiente:

   * Cree un formulario adaptable arrastrando y soltando componentes de formulario en el componente Contenedor de Forms adaptable en el editor de AEM Sites o en los fragmentos de experiencias.
   * Utilice el asistente de Forms adaptable dentro del editor de AEM Sites para poder crear formularios independientes de cualquier página de Sites, lo que le proporciona la libertad de reutilizar dichos formularios en varias páginas.
   * Agregue varios formularios a una página de Sites, lo que optimizará la experiencia del usuario y proporcionará la buena flexibilidad.

     >[!VIDEO](https://video.tv.adobe.com/v/3419284?quality=12&learn=on)

* [Integración y conformidad con Adobe Acrobat Sign mejoradas](/help/forms/adobe-sign-integration-adaptive-forms.md): AEM Forms ahora se integra con Adobe Acrobat Sign para Administración Pública. Esta integración proporciona un nivel avanzado de cumplimiento y seguridad para las firmas electrónicas con envíos de formularios adaptables para cuentas asociadas con el gobierno (departamentos y agencias gubernamentales).

  La integración con Adobe Acrobat Sign para Administración Pública permite a los socios de Adobe y a los clientes gubernamentales utilizar firmas electrónicas en Forms adaptable para algunas de las líneas de negocio más importantes y sensibles. Este nivel adicional de seguridad garantiza que todas las firmas electrónicas cumplan plenamente con la normativa FedRAMP Moderate, lo que proporciona tranquilidad a los clientes gubernamentales de Adobe.

* Tratamiento de errores mejorado con controladores de error personalizados en el editor de reglas. Ahora puede invocar una función personalizada (mediante la Biblioteca de clientes) en respuesta a un error devuelto por un servicio externo y proporcionar una respuesta personalizada a los usuarios finales. O bien, puede realizar acciones específicas en busca de errores devueltos por un servicio. Por ejemplo, puede invocar un flujo de trabajo personalizado en el backend para códigos de error específicos o informar al cliente de que el servicio está inactivo.

  Esta funcionalidad ayuda a mejorar su capacidad general de gestión de errores mediante la introducción de respuestas de error basadas en estándares compatibles con los controladores de error OOTB, con buena flexibilidad y control.

### Formularios adaptables sin encabezado, programa para primeros usuarios {#forms-early-adopter}

Utilice los formularios adaptables sin encabezado para que los desarrolladores puedan crear, publicar y gestionar formularios interactivos a los que se pueda acceder y con los que se pueda interactuar a través de API, en lugar de a través de una interfaz gráfica de usuario tradicional. Los formularios adaptables sin encabezado le ayudan a:

* crear formularios multicanal de alta calidad en el lenguaje de programación que desee
* integrar formularios de forma nativa en sus aplicaciones móviles y de escritorio, sitios web y aplicaciones de chat
* reutilizar los componentes de IU propios con aplicaciones de formularios
* utilice la potencia de Adobe Experience Manager Forms

Puede enviar un correo electrónico a `aem-forms-headless@adobe.com` desde su ID de correo electrónico oficial para unirse al programa de usuarios que lo adoptaron por primera vez.

## [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation {#foundation}

### Novedades {#what-is-new-foundation}

* Regiones de publicación adicionales: Los clientes de Sites pueden obtener licencias de hasta tres regiones de publicación, además de la región principal. El tráfico se dirige a granjas de publicación adicionales, lo que resulta en una menor latencia para determinadas solicitudes y una mayor resistencia frente a las interrupciones regionales. Póngase en contacto con el Administrador de cuentas de Adobe para obtener información sobre las licencias [Regiones de publicación adicionales](/help/operations/additional-publish-regions.md) para sus programas.

## Notas de la versión de mantenimiento {#maintenance}

Puede encontrar las últimas notas de la versión de mantenimiento [aquí](/help/release-notes/maintenance/latest.md).

## Cloud Manager {#cloud-manager}

Puede encontrar una lista completa de las versiones mensuales de Cloud Manager [aquí.](/help/implementing/cloud-manager/release-notes/current.md)

## Herramientas de migración {#migration-tools}

Puede encontrar una lista completa de las versiones de las herramientas de migración [aquí](/help/journey-migration/release-notes/release-notes-migration-tools-current.md).
