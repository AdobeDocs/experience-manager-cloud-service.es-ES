---
title: Novedades del centro de contenido
description: Obtenga más información sobre algunas de las funciones de Content Hub recién lanzadas
role: User
badgeSaas: label="AEM Assets" type="Positive" tooltip="(Se aplica a los AEM Assets)."
exl-id: 77a5c54c-bbc5-4dfb-9c3a-aa0620e836d0
source-git-commit: 46ca8082f85cdb957681aa9596b9312b35e4f6ec
workflow-type: tm+mt
source-wordcount: '1603'
ht-degree: 55%

---

# Novedades del centro de contenido {#whats-new-content-hub}

Centro de contenido está disponible como parte de Experience Manager Assets as a Cloud Service para democratizar el acceso al contenido sobre la marca por parte de las organizaciones y sus socios comerciales. Se centra en la distribución de recursos para su activación a escala y la creación de variantes de contenido de la marca para mejorar la agilidad comercial.

El siguiente vídeo muestra las funciones clave de Content Hub:

>[!VIDEO](https://video.tv.adobe.com/v/3463712)

>[!IMPORTANT]
>
>[Assets Ultimate](/help/assets/assets-ultimate-overview.md) y Assets as a Cloud Service incluyen 250 usuarios de Content Hub Limited. [Assets Prime](/help/assets/assets-prime.md) incluye 50 usuarios de Content Hub Limited.

## Fecha de lanzamiento {#release-date}

La fecha de lanzamiento de la versión de la funcionalidad Content Hub (2026.05.0) es el 28 de mayo de 2026 (igual que la de la versión de AEM as a Cloud Service). La próxima versión de la funcionalidad (2026.06.0) está planificada para el 25 de junio de 2026.

## Funciones de la versión de mayo de 2026 {#may-2026-release-features}

**Búsqueda por IA**

AEM Assets Content Hub ahora incluye Búsqueda por IA, una función de búsqueda avanzada que comprende el significado y la intención detrás de las consultas de los usuarios en lugar de depender únicamente de coincidencias de palabras clave exactas. La búsqueda por IA ofrece resultados más precisos y relevantes para el contexto al reconocer las relaciones entre palabras, conceptos e intención del usuario. Admite consultas multilingües, gestiona errores ortográficos y tipográficos, comprende sinónimos y muestra recursos relevantes incluso cuando los usuarios no utilizan términos de metadatos exactos.

Por ejemplo, una búsqueda de `Woman drinking coffee` también puede devolver recursos etiquetados con términos relacionados como `Lady`, `Girl`, `Latte` o `Cappuccino`.

Los administradores pueden habilitar o deshabilitar la Búsqueda por IA en Content Hub mediante el menú Configuraciones, seleccionando Búsqueda por IA o búsqueda de palabras clave tradicional.

[!BADGE Profundización en esta función]{type=Informative url="https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/assets/content-hub/search-assets-content-hub#ai-search-aem-assets-content-hub"}


**Opciones de ordenación personalizadas**

Content Hub ahora permite a los administradores habilitar campos de metadatos personalizados como opciones de ordenación en la página de inicio de Content Hub. Además de las opciones de ordenación predeterminadas Tamaño, Modificado, Nombre y Relevancia, los administradores pueden configurar campos de metadatos específicos de la empresa como Canal, Región, SKU o Campaña para ayudar a los usuarios a organizar los resultados de búsqueda de forma más eficaz.

[!BADGE Profundización en esta función]{type=Informative url="https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/assets/content-hub/search-assets-content-hub#configure-sorting-aem-assets-content-hub"}

**Compatibilidad con eventos de descarga y búsqueda de recursos para las API de envío**

Las API de entrega de AEM Assets ahora admiten eventos de búsqueda y descarga de recursos, lo que permite a las organizaciones realizar un seguimiento y responder a cómo se detectan y consumen los recursos en las aplicaciones y experiencias conectadas. Estos eventos ayudan a mejorar la visibilidad de los patrones de uso de los recursos, admiten flujos de trabajo de análisis e informes y simplifican las integraciones con sistemas externos y procesos de automatización.

Con perspectivas impulsadas por eventos, los equipos pueden comprender mejor la participación en el contenido y crear flujos de trabajo de recursos digitales más conectados. Para obtener más información, consulte la [documentación de la API](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/assets/delivery/#operation/asset_downloaded).

**URL de entrega de recursos**

Content Hub ahora permite a los usuarios copiar la URL de entrega de un recurso directamente desde las propiedades del recurso. Esta mejora facilita el uso compartido e incrustado de recursos aprobados en sitios web, aplicaciones y sistemas externos. Al proporcionar un acceso rápido a los vínculos listos para la entrega, los equipos pueden optimizar los flujos de trabajo de distribución de contenido y acelerar la reutilización de recursos en las experiencias digitales.

>[!IMPORTANT]
>
>Estas funciones están disponibles como funciones de disponibilidad limitada. Puede [crear y enviar un caso de asistencia al cliente de Adobe](https://helpx.adobe.com/es/enterprise/using/support-for-experience-cloud.html) para habilitarlo para su implementación.


## Funciones de la versión de febrero de 2026 {#february-2026-release-features}

**Administración de permisos en Content Hub mediante el agente de control de AEM**

En Content Hub, el agente de control de AEM garantiza que solo las personas adecuadas accedan a los recursos adecuados en el momento adecuado. Al aplicar controles granulares basados en atributos y derechos de uso, protege el contenido confidencial y, al mismo tiempo, permite la colaboración segura. Esto significa menos riesgo de conformidad, una integridad de marca más sólida y flujos de trabajo más rápidos, los equipos pueden compartir y reutilizar recursos con seguridad sin tener que preocuparse por el acceso no autorizado o el uso indebido. Este equilibrio entre seguridad y flexibilidad se traduce en una mayor eficiencia operativa y confianza en toda la organización.

![Información general sobre administración de permisos](/help/ai-in-aem/agents/governance/assets/permission-management.png)

[!BADGE Profundización en esta función]{type=Informative url="https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/ai-in-aem/agents/governance/overview#permission-and-digital-rights-management"}


## Funciones de la versión de octubre de 2025 {#october-2025-release-features}

**Mejoras en la experiencia de descarga de Content Hub**

Content Hub ahora admite la descarga de varias representaciones de recursos en una jerarquía plana, lo que elimina la necesidad de navegar por varias carpetas. Las preferencias del usuario para el comportamiento de descarga ahora se conservan para una experiencia coherente entre sesiones. La nueva experiencia de descarga de recursos optimiza la administración de recursos y mejora la eficacia al hacer que los archivos descargados sean más fáciles de localizar y organizar.

[!BADGE Profundización en esta función]{type=Informative url="https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/assets/content-hub/download-assets-content-hub#download-asset-renditions"}

## Funciones de la versión de septiembre de 2025 {#september-2025-release-features}

**Marcar colecciones como favoritas**

Ahora puede marcar colecciones como Favoritos en Content Hub, lo que facilita su organización y recuperación. Una vez agregadas, tus colecciones favoritas estarán disponibles en la ficha **[!UICONTROL Favoritos]** de la página de inicio de Content Hub.

**Colecciones de anclajes para acceso rápido**

Los administradores de Content Hub ahora pueden anclar colecciones en Content Hub para acceder rápidamente a ellas. Las colecciones ancladas se muestran en una sección **[!UICONTROL Anclada]** específica de la página principal de Colecciones, lo que facilita mantener las colecciones importantes a mano.

[!BADGE Profundización en esta función]{type=Informative url="https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/assets/content-hub/collections-content-hub#pin-unpin-collection"}

## Funciones de la versión de agosto de 2025 {#august-release-features}

**Búsqueda masiva mediante propiedades de filtro**

Content Hub ahora acelera la detección de los recursos que necesita. Con la nueva función Búsqueda masiva, puede introducir varios valores para cualquier propiedad de filtro separadas por un delimitador (por ejemplo, varios ID de SKU) y recuperar al instante todos los recursos coincidentes mediante una sola búsqueda.

[!BADGE Profundización en esta función]{type=Informative url="https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/assets/content-hub/search-assets-content-hub#bulk-search"}

## Funciones de la versión de julio de 2025 {#july-2025-release-features}

**Mayor flexibilidad en la personalización de marca de Content Hub**

Basándose en las funciones de personalización existentes, Content Hub ahora permite a los administradores adaptar aún más su implementación añadiendo imágenes de logotipo personalizadas. También se ha añadido compatibilidad con el formato de archivo TIFF para imágenes de banner y logotipo, lo que permite una mayor flexibilidad en el diseño.

[!BADGE Profundización en esta función]{type=Informative url="https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/assets/content-hub/configure-content-hub-ui-options#configure-branding-content-hub"}

**Uso compartido más inteligente con vínculos con título**

Ahora puede añadir un título al generar un vínculo compartido, ya sea desde la vista de detalles del recurso o después de seleccionar uno o varios recursos. Esto ayuda a los destinatarios a identificar fácilmente el propósito de cada vínculo, especialmente cuando reciben varios recursos compartidos.

![vínculo privado y público](/help/assets/assets/shared-link-for-assets.png)

[!BADGE Profundización en esta función]{type=Informative url="https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/assets/content-hub/share-assets-content-hub"}

**Se ha mejorado la navegación por filtros**

Content Hub ahora incluye la opción **Mostrar todo** dentro de los filtros, lo que permite a los usuarios ver todas las facetas disponibles junto con el número de recursos en lugar de la limitación actual de ver solo hasta 10 facetas. Las funciones mejoradas de búsqueda y ordenación dentro de cada filtro facilitan la detección y administración de recursos de forma más eficaz.

## Funciones de la versión de junio de 2025 {#june-2025-release-features}

### Control de colecciones {#collections-governance}

Content Hub ahora le permite controlar el acceso a las colecciones durante la creación, lo que garantiza que solo los usuarios autorizados puedan ver o administrar los recursos agrupados. Garantiza una mayor seguridad, una mejor colaboración, una administración de recursos organizada y un control simplificado.

>[!VIDEO](https://video.tv.adobe.com/v/3463336)

[!BADGE Profundización en esta función]{type=Informative url="https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/assets/content-hub/collections-content-hub#create-collections"}

## Funciones de la versión de mayo de 2025 {#may-2025-release-features}

La versión de mayo de Content Hub incluye las siguientes funciones:

* [Control de acceso basado en atributos](#attribute-based-access-control)

* [Personalización de marca de la IU](#ui-branding)

* [Uso compartido de vínculos públicos](#public-link-sharing)

* [Descarga de varios recursos como ZIP](#download-multiple-assets-as-zip)

* [Representaciones de Dynamic Media en Content Hub](#dynamic-media-renditions)

### Control de acceso basado en atributos (ABAC) {#attribute-based-access-control}

Content Hub ahora le permite aplicar restricciones basadas en reglas para acceder a los recursos. Los permisos de recursos garantizan el control y también aseguran que los usuarios solo puedan acceder a los recursos relevantes.

Las reglas de restricción de recursos se basan en metadatos y, si las condiciones definidas en la regla coinciden con los metadatos del recurso, este se muestra a los grupos de usuarios.

Algunas de las ventajas clave del control de acceso basado en atributos son:

* Elimina la dependencia de la estructura de carpetas para los permisos

* Permite a los administradores cargar recursos y determinar de forma retroactiva las estructuras de permisos

* Reduce el número de duplicados: mejora la integridad de los recursos. Los duplicados son necesarios en los permisos basados en carpetas cuando los mismos recursos se comparten con diferentes grupos.

[!BADGE Profundización en esta función]{type=Informative url="https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/assets/content-hub/attribute-based-access-control"}

### Personalización de marca de la IU {#ui-branding}

Content Hub ahora permite a los administradores personalizar la interfaz de usuario con elementos específicos de la marca, incluidas imágenes de banners, títulos de banners y texto independiente, así como colores primarios y secundarios. Estas mejoras ayudan a garantizar la coherencia de la marca, simplificar la incorporación de usuarios y generar confianza.

![Personalización de marca de la interfaz de usuario](/help/assets/assets/content-hub-ui-branding.png)

[!BADGE Profundización en esta función]{type=Informative url="https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/assets/content-hub/configure-content-hub-ui-options#configure-branding-content-hub"}

### Uso compartido de vínculos públicos {#public-link-sharing}

Content Hub ahora admite la generación de vínculos que se pueden compartir para permitir que usuarios externos, sin acceso a la aplicación, vean los metadatos de los recursos o descarguen los recursos.

![Personalización de marca de la interfaz de usuario](/help/assets/assets/public-and-private-link.png)

[!BADGE Profundización en esta función]{type=Informative url="https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/assets/content-hub/share-assets-content-hub"}

### Descarga de varios recursos como ZIP {#download-multiple-assets-as-zip}

Content Hub ahora también le permite descargar los recursos seleccionados y sus representaciones en un archivo ZIP y no como archivos independientes, lo que simplifica la administración de archivos.

[!BADGE Profundización en esta función]{type=Informative url="https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/assets/content-hub/download-assets-content-hub#download-asset-renditions"}

### Representaciones de Dynamic Media en Content Hub {#dynamic-media-renditions}

Acceda a todas las representaciones de ajustes preestablecidos y recortes inteligentes de Dynamic Media para descargarlos directamente desde la interfaz de usuario de Content Hub.

![Representaciones de medios dinámicos](/help/assets/assets/dm-renditions-content-hub.png)

[!BADGE Profundización en esta función]{type=Informative url="https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/assets/content-hub/download-assets-content-hub#download-asset-renditions"}
