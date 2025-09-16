---
title: Novedades del centro de contenido
description: Obtenga más información sobre algunas de las funciones de Content Hub recién lanzadas
role: User
exl-id: 77a5c54c-bbc5-4dfb-9c3a-aa0620e836d0
source-git-commit: 62ac097fca0142265f2e1ef28117619d59045e6c
workflow-type: tm+mt
source-wordcount: '699'
ht-degree: 99%

---

# Novedades del centro de contenido {#whats-new-content-hub}

Centro de contenido está disponible como parte de Experience Manager Assets as a Cloud Service para democratizar el acceso al contenido sobre la marca por parte de las organizaciones y sus socios comerciales. Se centra en la distribución de recursos para su activación a escala y la creación de variantes de contenido de la marca para mejorar la agilidad comercial.

El siguiente vídeo muestra las funciones clave de Content Hub:

>[!VIDEO](https://video.tv.adobe.com/v/3463712)

>[!IMPORTANT]
>
>[Assets Ultimate](/help/assets/assets-ultimate-overview.md) y Assets as a Cloud Service incluyen 250 usuarios de Content Hub Limited. [Assets Prime](/help/assets/assets-prime.md) incluye 50 usuarios de Content Hub Limited.

## Fecha de lanzamiento {#release-date}

La fecha de lanzamiento de la versión de la funcionalidad Content Hub (2025.8.0) es el 28 de agosto de 2025 (igual que la de la versión de AEM as a Cloud Service). La próxima versión con funcionalidades (2025.9.0) se planificó para el 25 de septiembre de 2025.

## Funciones de la versión de agosto {#august-release-features}

**Búsqueda masiva mediante propiedades de filtro**

Content Hub ahora acelera la detección de los recursos que necesita. Con la nueva función Búsqueda masiva, puede introducir varios valores para cualquier propiedad de filtro separadas por un delimitador (por ejemplo, varios ID de SKU) y recuperar al instante todos los recursos coincidentes mediante una sola búsqueda.

[!BADGE Profundización en esta función]{type=Informative url="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/content-hub/search-assets-content-hub#bulk-search"}

## Funciones de la versión de julio {#july-release-features}

**Mayor flexibilidad en la personalización de marca de Content Hub**

Basándose en las funciones de personalización existentes, Content Hub ahora permite a los administradores adaptar aún más su implementación añadiendo imágenes de logotipo personalizadas. También se ha añadido compatibilidad con el formato de archivo TIFF para imágenes de banner y logotipo, lo que permite una mayor flexibilidad en el diseño.

[!BADGE Profundización en esta función]{type=Informative url="https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/assets/content-hub/configure-content-hub-ui-options#configure-branding-content-hub"}

**Uso compartido más inteligente con vínculos con título**

Ahora puede añadir un título al generar un vínculo compartido, ya sea desde la vista de detalles del recurso o después de seleccionar uno o varios recursos. Esto ayuda a los destinatarios a identificar fácilmente el propósito de cada vínculo, especialmente cuando reciben varios recursos compartidos.

![vínculo privado y público](/help/assets/assets/shared-link-for-assets.png)

[!BADGE Profundización en esta función]{type=Informative url="https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/assets/content-hub/share-assets-content-hub"}

**Se ha mejorado la navegación por filtros**

Content Hub ahora incluye la opción **Mostrar todo** dentro de los filtros, lo que permite a los usuarios ver todas las facetas disponibles junto con el número de recursos en lugar de la limitación actual de ver solo hasta 10 facetas. Las funciones mejoradas de búsqueda y ordenación dentro de cada filtro facilitan la detección y administración de recursos de forma más eficaz.

## Funciones de la versión de junio {#june-release-features}

### Control de colecciones {#collections-governance}

Content Hub ahora le permite controlar el acceso a las colecciones durante la creación, lo que garantiza que solo los usuarios autorizados puedan ver o administrar los recursos agrupados. Garantiza una mayor seguridad, una mejor colaboración, una administración de recursos organizada y un control simplificado.

>[!VIDEO](https://video.tv.adobe.com/v/3463336)

[!BADGE Profundización en esta función]{type=Informative url="https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/assets/content-hub/collections-content-hub#create-collections"}

## Funciones de la versión de mayo {#may-release-features}

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
