---
title: Cambios importantes en [!DNL Adobe Experience Manager Assets] as a [!DNL Cloud Service]
description: Cambios importantes en [!DNL Adobe Experience Manager Assets] in [!DNL Experience Manager] as a [!DNL Cloud Service] en comparación con [!DNL Adobe Experience Manager 6.5.
feature: Información de la versión
role: Business Practitioner,Leader,Architect,Administrator
exl-id: 93e7dbcd-016e-4ef2-a1cd-c554efb5ad34
source-git-commit: cff7454e2b6a1d55accef31d20d85378f08dfe0c
workflow-type: tm+mt
source-wordcount: '830'
ht-degree: 5%

---

# Cambios importantes en [!DNL Experience Manager Assets] como [!DNL Cloud Service] {#notable-changes}

[!DNL Adobe Experience Manager] as a  [!DNL Cloud Service] ofrece muchas nuevas funciones y posibilidades para administrar sus proyectos de Experience Manager. Existen muchas diferencias entre [!DNL Experience Manager Assets] local o alojado como servicio administrado por Adobe en comparación con [!DNL Experience Manager] como [!DNL Cloud Service]. Este artículo destaca las diferencias importantes para las capacidades [!DNL Assets].

Las principales diferencias en comparación con [Experience Manager] 6.5 se encuentran en las siguientes áreas:

* [Ingesta, carga y procesamiento de recursos](#asset-ingestion).
* [Microservicios de recursos para procesamiento nativo de la nube](#asset-microservices).
* [Eliminación de la IU clásica](#classic-ui).

## Ingesta, procesamiento y distribución de recursos {#asset-ingestion-distribution}

La carga de recursos está optimizada para una mayor eficacia, ya que permite una mejor adaptación de la ingesta, cargas más rápidas, un procesamiento más rápido mediante microservicios y la ingesta masiva. Se actualizan las capacidades del producto (interfaces de usuario web, clientes de escritorio). Además, esto puede afectar a algunas personalizaciones existentes.

* [!DNL Experience Manager] utiliza el principio de acceso binario directo para cargar y descargar recursos y utiliza los microservicios de recursos para procesar recursos. Consulte [descripción general de microservicios](/help/assets/asset-microservices-overview.md).
   * Carga de recursos [con acceso binario directo](/help/assets/asset-microservices-overview.md#asset-upload-with-direct-binary-access).
   * Para obtener más información técnica, consulte [protocolo de carga binaria directa y API](/help/assets/developer-reference-material-apis.md#upload-binary).
   * Para ver una comparación de los métodos de API disponibles para las operaciones básicas de CRUD, consulte [APIs and asset operations](/help/assets/developer-reference-material-apis.md#use-cases-and-apis).
* El flujo de trabajo predeterminado de **[!UICONTROL actualización de recursos DAM]** en versiones anteriores de ya no está disponible. [!DNL Experience Manager] En su lugar, los microservicios de recursos proporcionan un servicio escalable y fácilmente disponible que cubre la mayor parte del procesamiento de recursos predeterminado (representaciones, extracción de metadatos y extracción de texto para la indexación).
   * Consulte [configurar y utilizar microservicios de recursos](/help/assets/asset-microservices-configure-and-use.md)
   * Para tener pasos de flujo de trabajo personalizados en el procesamiento, se pueden utilizar [flujos de trabajo posteriores al procesamiento](/help/assets/asset-microservices-configure-and-use.md#post-processing-workflows).

* Los componentes del sitio web que entregan un archivo binario sin ninguna transformación pueden utilizar la descarga directa. El servlet de Sling GET se actualiza para permitir que los desarrolladores lo hagan de forma predeterminada. Los componentes del sitio web que proporcionan un archivo binario con alguna transformación (por ejemplo, cambiar su tamaño mediante un servlet) pueden seguir funcionando tal cual.

Las representaciones estándar generadas con los microservicios de recursos se almacenan de forma compatible con versiones anteriores en los nodos del repositorio de recursos utilizando las mismas convenciones de nomenclatura.

## Desarrollar y probar microservicios de recursos {#asset-microservices}

Los microservicios de recursos proporcionan un procesamiento escalable y flexible de los recursos mediante servicios en la nube. Adobe administra los servicios de nube para una gestión óptima de los distintos tipos de recursos y opciones de procesamiento. Los microservicios de recursos ayudan a evitar la necesidad de herramientas y métodos de procesamiento de terceros (como ImageMagick) y simplifican las configuraciones, al tiempo que proporcionan una funcionalidad predeterminada para tipos de archivos comunes. Ahora puede procesar una [amplia gama de tipos de archivo](/help/assets/file-format-support.md) que cubra más formatos predeterminados de los posibles con versiones anteriores de Experience Manager. Por ejemplo, la extracción en miniatura de los formatos PSD y PSB ahora es posible que antes se necesitaban soluciones de terceros como ImageMagick. No puede utilizar las configuraciones complejas de ImageMagick para la configuración [!UICONTROL Perfiles de procesamiento]. Utilice [!DNL Dynamic Media] para la transcodificación avanzada de vídeos FFmpeg y utilice perfiles de procesamiento para la [transcodificación básica de vídeos MP4](/help/assets/manage-video-assets.md#transcode-video).

Los microservicios de recursos son un servicio nativo de la nube que se aprovisiona automáticamente y se cablea a [!DNL Experience Manager] en programas de clientes y entornos administrados en Cloud Manager. Para ampliar o personalizar [!DNL Experience Manager], los desarrolladores pueden utilizar el contenido o los recursos existentes con representaciones generadas en un entorno de nube, para probar y validar su código utilizando, mostrando y descargando recursos.

Para realizar una validación completa del código y el proceso, incluido el procesamiento e ingesta de recursos, implemente los cambios de código en un entorno de desarrollo en la nube mediante [la canalización](/help/implementing/cloud-manager/configure-pipeline.md) y pruebe con la ejecución completa del procesamiento de los microservicios de recursos.

## Paridad de características con [!DNL Experience Manager] 6.5 {#cloud-service-feature-status}

[!DNL Experience Manager] as a  [!DNL Cloud Service] introduce muchas funciones nuevas y formas más eficaces para que funcionen las funciones existentes. Sin embargo, al pasar de [!DNL Experience Manager] 6.5 a [!DNL Experience Manager] como [!DNL Cloud Service], es posible que observe que algunas características funcionan de manera diferente, no están disponibles o están parcialmente disponibles. La siguiente es una lista de estas funciones. Además, consulte las [funciones obsoletas y eliminadas](/help/release-notes/deprecated-removed-features.md).

| Funcionalidad o caso de uso | Estado en [!DNL Experience Manager] como [!DNL Cloud Service] | Comentarios |
|-----|-----|-----|
| [Duplicar detección de recursos](/help/assets/manage-digital-assets.md#detect-duplicate-assets) | Funciona de forma diferente. | Consulte [cómo funcionó en [!DNL Experience Manager] 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/duplicate-detection.html). |
| [Representaciones de Solo para ubicación (FPO)](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/configure-aem-assets-for-asset-link.ug.html#configfporendition) | Funciona de forma diferente |  |
| Reescritura de metadatos | Funciona de forma diferente | Deshabilitado de forma predeterminada. Habilite el lanzador del flujo de trabajo correspondiente si es necesario. La reescritura se gestiona mediante microservicios de recursos. |
| Procesamiento de recursos cargados mediante el Administrador de paquetes | Necesita una intervención manual. | Vuelva a procesar manualmente mediante la acción **[!UICONTROL Reprocesar recurso]**. |
| Detección de tipo MIME | No se admite. | Si carga un recurso digital sin extensión o con una extensión incorrecta, es posible que no se procese como desee. Los usuarios aún pueden almacenar los archivos binarios sin una extensión en DAM. Consulte [Detección de tipo MIME en [!DNL Experience Manager] 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/assets/administer/detect-asset-mime-type-with-tika.html). |
| Generación de subrecursos para recursos compuestos | No se admite. | No se cumplen los casos de uso dependientes. Por ejemplo, la anotación de archivos PDF de varias páginas se ve afectada. Consulte [creación de subactivos en [!DNL Experience Manager] 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/managing-linked-subassets.html#generate-subassets). |
| Página principal | No se admite. | Consulte [[!DNL Assets] Home Page experience in [!DNL Experience Manager] 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/assets/using/assets-home-page.html) |
| Extraer recursos del archivo ZIP | No se admite. | Consulte [Extracción ZIP en [!DNL Experience Manager] 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/manage-assets.html#extractzip). |
| IU clásica | No se admite. | Solo está disponible la IU táctil. |

>[!MORELIKETHIS]
>
>Los siguientes recursos están disponibles para [!DNL Experience Manager] como [!DNL Cloud Service]:
>
>* [Lista de funciones obsoletas y eliminadas](/help/release-notes/deprecated-removed-features.md)
* [Introducción](/help/overview/introduction.md)
* [Novedades y diferencias](/help/overview/what-is-new-and-different.md)
* [La arquitectura](/help/core-concepts/architecture.md)
* [Cambios importantes](/help/release-notes/aem-cloud-changes.md)
* [Cambios importantes [!DNL Sites]](/help/sites-cloud/sites-cloud-changes.md)
* [Tutoriales en vídeo](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/overview.html?lang=es)

