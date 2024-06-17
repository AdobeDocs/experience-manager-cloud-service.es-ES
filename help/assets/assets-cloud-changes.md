---
title: Cambios importantes en [!DNL Adobe Experience Manager Assets] as a [!DNL Cloud Service]
description: Cambios importantes en [!DNL Adobe Experience Manager Assets] in [!DNL Experience Manager] as a [!DNL Cloud Service] en comparación con [!DNL Adobe Experience Manager] 6.5.
feature: Release Information
role: User, Leader, Architect, Admin
exl-id: 93e7dbcd-016e-4ef2-a1cd-c554efb5ad34
source-git-commit: ab2cf8007546f538ce54ff3e0b92bb0ef399c758
workflow-type: tm+mt
source-wordcount: '998'
ht-degree: 9%

---

# Cambios importantes en [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#notable-changes}

[!DNL Adobe Experience Manager] as a [!DNL Cloud Service] ofrece muchas nuevas funciones y posibilidades para gestionar sus proyectos de Experience Manager. Hay muchas diferencias entre [!DNL Experience Manager Assets] On-Premise o alojado como un servicio administrado por el Adobe en comparación con [!DNL Experience Manager] as a [!DNL Cloud Service]. Este artículo destaca las importantes diferencias entre [!DNL Assets] funciones.

Las principales diferencias en comparación con [!DNL Experience Manager] 6.5 se encuentran en las siguientes áreas:

* [Ingesta, carga y procesamiento de recursos](#asset-ingestion).
* [Microservicios de recursos para el procesamiento nativo de la nube](#asset-microservices).
* [Eliminación de la IU clásica](#classic-ui).

## Ingesta, procesamiento y distribución de recursos {#asset-ingestion-distribution}

La carga de recursos está optimizada para lograr una mayor eficacia al permitir una mejor ampliación de la ingesta, cargas más rápidas, un procesamiento más rápido mediante microservicios y una ingesta masiva. Se actualizan las funciones del producto (interfaces de usuario web, clientes de escritorio). Además, esto puede afectar a algunas personalizaciones existentes.

* [!DNL Experience Manager] utiliza el principio de acceso binario directo para cargar y descargar recursos, y utiliza los microservicios de recursos para procesar recursos. Consulte [descripción general de los microservicios](/help/assets/asset-microservices-overview.md).
   * Carga de recursos [con acceso binario directo](/help/assets/asset-microservices-overview.md#asset-upload-with-direct-binary-access).
   * Para obtener más información técnica, consulte [protocolo de carga binaria directa y API](/help/assets/developer-reference-material-apis.md#upload-binary).
   * Para ver una comparación de los métodos de API disponibles para operaciones básicas de CRUD, consulte [API y operaciones de recursos](/help/assets/developer-reference-material-apis.md#use-cases-and-apis).
* Flujo de trabajo predeterminado **[!UICONTROL Actualización de recursos DAM]** en versiones anteriores de [!DNL Experience Manager] ya no está disponible. En su lugar, los microservicios de recursos proporcionan un servicio escalable y fácilmente disponible que cubre la mayoría del procesamiento de recursos predeterminado (representaciones, extracción de metadatos y extracción de texto para la indexación).
   * Consulte [configuración y uso de microservicios de recursos](/help/assets/asset-microservices-configure-and-use.md)
   * Para tener pasos de flujo de trabajo personalizados en el procesamiento, [flujos de trabajo posteriores al procesamiento](/help/assets/asset-microservices-configure-and-use.md#post-processing-workflows) se puede utilizar.

* Los componentes del sitio web que entregan un archivo binario sin ninguna transformación pueden utilizar la descarga directa. El servlet de GET de Sling se actualiza para permitir que los desarrolladores lo hagan de forma predeterminada. Los componentes del sitio web que proporcionan un binario con alguna transformación (por ejemplo, cambiar su tamaño mediante un servlet) pueden seguir funcionando tal cual.

Las representaciones estándar generadas con los microservicios de recursos se almacenan de forma compatible con versiones anteriores en los nodos del repositorio de recursos mediante las mismas convenciones de nomenclatura.

## Desarrollar y probar microservicios de recursos {#asset-microservices}

Los microservicios de recursos proporcionan un procesamiento escalable y resiliente de los recursos mediante servicios en la nube. Adobe administra los servicios de nube para una gestión óptima de los distintos tipos de recursos y opciones de procesamiento. Los microservicios de recursos ayudan a evitar la necesidad de herramientas y métodos de procesamiento de terceros (como [!DNL ImageMagick]) y simplificar las configuraciones, a la vez que proporciona una funcionalidad predeterminada para los tipos de archivo más comunes. Ahora puede procesar una [amplia gama de tipos de archivos](/help/assets/file-format-support.md) cubre más formatos listos para usar que los que son posibles con versiones anteriores de Experience Manager. Por ejemplo, ahora es posible extraer miniaturas de los formatos PSD y PSB que antes requerían soluciones de terceros, como [!DNL ImageMagick]. No puede utilizar las configuraciones complejas de [!DNL ImageMagick] para el [!UICONTROL Perfiles de procesamiento] configuración. Uso [!DNL Dynamic Media] para la transcodificación avanzada de vídeos FFmpeg y utilice perfiles de procesamiento para [transcodificación básica de vídeos MP4](/help/assets/manage-video-assets.md#transcode-video).

Los microservicios de recursos son un servicio nativo de la nube que se aprovisiona automáticamente y se conecta a [!DNL Experience Manager] en programas de clientes y entornos administrados en Cloud Manager. Para ampliar o personalizar [!DNL Experience Manager]Además, los desarrolladores pueden utilizar el contenido o los recursos existentes con representaciones generadas en un entorno de nube para probar y validar su código mediante, mostrar y descargar recursos.

Para realizar una validación completa del código y el proceso, incluida la ingesta y el procesamiento de recursos, implemente los cambios de código en un entorno de desarrollo en la nube mediante [la canalización](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md) y realizar pruebas con la ejecución completa del procesamiento de microservicios de recursos.

## Paridad de características con [!DNL Experience Manager] 6,5 {#cloud-service-feature-status}

[!DNL Experience Manager] as a [!DNL Cloud Service] presenta muchas funciones nuevas y formas más eficaces de funcionar con las funciones existentes. Sin embargo, al pasar de [!DNL Experience Manager] 6.5 a [!DNL Experience Manager] as a [!DNL Cloud Service], es posible que observe que algunas funciones funcionan de forma diferente, no están disponibles o están disponibles parcialmente. A continuación se muestra una lista de estas funciones. Además, consulte la [funciones en desuso y eliminadas](/help/release-notes/deprecated-removed-features.md).

| Funcionalidad para casos de uso | Estado en [!DNL Experience Manager] as a [!DNL Cloud Service] | Comentarios |
|-----|-----|-----|
| [Detección de recursos duplicados](/help/assets/detect-duplicate-assets.md) | Funciona de forma diferente | Consulte [cómo funcionaba en [!DNL Experience Manager] 6,5](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/duplicate-detection.html). |
| [Para representaciones de Solo ubicación (FPO)](/help/assets/configure-fpo-renditions.md) | Funciona de forma diferente | Los perfiles de procesamiento utilizan microservicios de recursos para generar representaciones de FPO. En Experience Manager 6.5, una solución de terceros como [!DNL ImageMagick] estaba disponible para generar las representaciones. |
| Reescritura de metadatos | Funciona de forma diferente | Deshabilitado de forma predeterminada. Active el iniciador del flujo de trabajo correspondiente si es necesario. Los microservicios de recursos se encargan de la reescritura. |
| Procesamiento de recursos cargados mediante el Administrador de paquetes | Necesita intervención manual | Volver a procesar manualmente con **[!UICONTROL Volver a procesar recurso]** acción. |
| Detección de tipo MIME | No compatible. | Si carga un recurso digital sin una extensión o con una extensión incorrecta, es posible que no se procese como se desea. Los usuarios aún pueden almacenar los archivos binarios sin una extensión en DAM. Consulte [Detección de tipo MIME en [!DNL Experience Manager] 6,5](https://experienceleague.adobe.com/docs/experience-manager-65/assets/administer/detect-asset-mime-type-with-tika.html). |
| Generación de subrecursos para recursos compuestos | No compatible. | Es posible que los casos de uso dependientes como anotaciones no se cumplan. Consulte [creación de subrecursos en [!DNL Experience Manager] 6,5](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/managing-linked-subassets.html#generate-subassets). La vista previa del PDF de algunos tipos de archivo está disponible a partir de [Versión 2021.7.0](/help/release-notes/release-notes-cloud/release-notes-current.md). |
| Edición de imágenes | No compatible | La edición de recursos no se admite en Experience Manager as a Cloud Service. Consulte [cómo funcionaba en Experience Manager 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/manage-assets.html#editing-images). |
| Página de inicio | No compatible | Consulte [[!DNL Assets] Experiencia de la página de inicio en [!DNL Experience Manager] 6,5](https://experienceleague.adobe.com/docs/experience-manager-65/assets/using/assets-home-page.html) |
| Extraer recursos del archivo ZIP | No compatible | Consulte [Extracción de ZIP en [!DNL Experience Manager] 6,5](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/manage-assets.html#extractzip). |
| Clasificaciones de activos | No compatible | No se admite el widget de clasificación en el editor de esquemas de metadatos. |
| Filtro de disposición de contenido | No compatible | Un caso de uso popular de `ContentDispositionFilter` es permitir a los administradores configurar [!DNL Experience Manager] para proporcionar archivos de HTML y abrir archivos de PDF en línea en lugar de descargarlos. En las instancias de publicación, puede administrar la disposición mediante la configuración de Dispatcher. En las instancias de autor, el Adobe no recomienda la modificación del encabezado Disposición de contenido. Consulte [Filtro de disposición de contenido en [!DNL Experience Manager] 6,5](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/content-disposition-filter.html). |
| Plantilla de sesión fotográfica del producto | No compatible | Consulte [plantilla de sesión fotográfica de producto en [!DNL Experience Manager] 6,5](https://experienceleague.adobe.com/docs/experience-manager-65/authoring/projects/managing-product-information.html). |
| Traducción inteligente | No compatible | [Traducción inteligente](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/translation/smart-translation-search-feature-video-use.html) no es compatible con [!DNL Experience Manager] as a [!DNL Cloud Service]. |
| WebDAV | No compatible | Para ver las alternativas, consulte [[!DNL Creative Cloud] integración](/help/assets/aem-cc-integration-best-practices.md) o [Material de referencia para desarrolladores](/help/assets/developer-reference-material-apis.md). |
| IU clásica | No compatible | Solo está disponible la interfaz de usuario táctil. |

**Consulte también**

* [Traducir recursos](translate-assets.md)
* [API HTTP de recursos](mac-api-assets.md)
* [Formatos de archivo compatibles con recursos](file-format-support.md)
* [Buscar recursos](search-assets.md)
* [Recursos de red](use-assets-across-connected-assets-instances.md)
* [Informes de recurso](asset-reports.md)
* [Esquemas de metadatos](metadata-schemas.md)
* [Descarga de recursos](download-assets-from-aem.md)
* [Administración de metadatos](manage-metadata.md)
* [Facetas de búsqueda](search-facets.md)
* [Administrar colecciones](manage-collections.md)
* [Importación masiva de metadatos](metadata-import-export.md)
* [Publicación de recursos en AEM y Dynamic Media](/help/assets/publish-assets-to-aem-and-dm.md)

>[!MORELIKETHIS]
>
>Los siguientes recursos están disponibles para [!DNL Experience Manager] as a [!DNL Cloud Service]:
>
>* [Lista de funciones obsoletas y eliminadas](/help/release-notes/deprecated-removed-features.md)
>* [Una introducción](/help/overview/introduction.md)
>* [Novedades y diferencias](/help/overview/what-is-new-and-different.md)
>* [La arquitectura](/help/overview/architecture.md)
>* [Cambios importantes](/help/release-notes/aem-cloud-changes.md)
>* [Cambios importantes [!DNL Sites]](/help/sites-cloud/sites-cloud-changes.md)
>* [Tutoriales en vídeo](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/overview.html?lang=es)
