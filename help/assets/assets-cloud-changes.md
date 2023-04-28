---
title: Cambios importantes en [!DNL Adobe Experience Manager Assets] como [!DNL Cloud Service]
description: Cambios importantes en [!DNL Adobe Experience Manager Assets] en [!DNL Experience Manager] como [!DNL Cloud Service] comparado con [!DNL Adobe Experience Manager] 6.5.
feature: Release Information
role: User,Leader,Architect,Admin
exl-id: 93e7dbcd-016e-4ef2-a1cd-c554efb5ad34
source-git-commit: 8bdd89f0be5fe7c9d4f6ba891d7d108286f823bb
workflow-type: tm+mt
source-wordcount: '1034'
ht-degree: 10%

---

# Cambios importantes en [!DNL Experience Manager Assets] como [!DNL Cloud Service] {#notable-changes}

[!DNL Adobe Experience Manager] como [!DNL Cloud Service] trae muchas nuevas funciones y posibilidades para administrar sus proyectos de Experience Manager. Hay muchas diferencias entre [!DNL Experience Manager Assets] local o alojado como servicio administrado por Adobe en comparación con [!DNL Experience Manager] como [!DNL Cloud Service]. Este artículo destaca las diferencias importantes para [!DNL Assets] capacidades.

Las principales diferencias con respecto a [!DNL Experience Manager] 6.5 se encuentran en los siguientes ámbitos:

* [Ingesta, carga y procesamiento de recursos](#asset-ingestion).
* [Microservicios de recursos para procesamiento nativo de la nube](#asset-microservices).
* [Eliminación de la IU clásica](#classic-ui).

## Ingesta, procesamiento y distribución de recursos {#asset-ingestion-distribution}

La carga de recursos está optimizada para una mayor eficacia, ya que permite una mejor adaptación de la ingesta, cargas más rápidas, un procesamiento más rápido mediante microservicios y la ingesta masiva. Se actualizan las capacidades del producto (interfaces de usuario web, clientes de escritorio). Además, esto puede afectar a algunas personalizaciones existentes.

* [!DNL Experience Manager] utiliza el principio de acceso binario directo para cargar y descargar recursos y utiliza los microservicios de recursos para procesar recursos. Consulte [descripción general de los microservicios](/help/assets/asset-microservices-overview.md).
   * Carga de recursos [con acceso binario directo](/help/assets/asset-microservices-overview.md#asset-upload-with-direct-binary-access).
   * Para obtener más información técnica, consulte [protocolo de carga binaria directa y API](/help/assets/developer-reference-material-apis.md#upload-binary).
   * Para ver una comparación de los métodos de API disponibles para las operaciones básicas de CRUD, consulte [API y operaciones de recursos](/help/assets/developer-reference-material-apis.md#use-cases-and-apis).
* El flujo de trabajo predeterminado de **[!UICONTROL actualización de recursos DAM]** en versiones anteriores de ya no está disponible. [!DNL Experience Manager] En su lugar, los microservicios de recursos proporcionan un servicio escalable y fácilmente disponible que cubre la mayor parte del procesamiento de recursos predeterminado (representaciones, extracción de metadatos y extracción de texto para la indexación).
   * Consulte [configurar y utilizar microservicios de recursos](/help/assets/asset-microservices-configure-and-use.md)
   * Para tener pasos de flujo de trabajo personalizados en el procesamiento, [flujos de trabajo posteriores al procesamiento](/help/assets/asset-microservices-configure-and-use.md#post-processing-workflows) se puede usar.

* Los componentes del sitio web que entregan un archivo binario sin ninguna transformación pueden utilizar la descarga directa. El servlet de Sling GET se actualiza para permitir que los desarrolladores lo hagan de forma predeterminada. Los componentes del sitio web que proporcionan un archivo binario con alguna transformación (por ejemplo, cambiar su tamaño mediante un servlet) pueden seguir funcionando tal cual.

Las representaciones estándar generadas con los microservicios de recursos se almacenan de forma compatible con versiones anteriores en los nodos del repositorio de recursos utilizando las mismas convenciones de nomenclatura.

## Desarrollar y probar microservicios de recursos {#asset-microservices}

Los microservicios de recursos proporcionan un procesamiento escalable y resiliente de los recursos mediante servicios en la nube. Adobe administra los servicios de nube para una gestión óptima de los distintos tipos de recursos y opciones de procesamiento. Los microservicios de recursos ayudan a evitar la necesidad de herramientas y métodos de procesamiento de terceros (como [!DNL ImageMagick]) y simplifique las configuraciones, a la vez que proporciona funcionalidad predeterminada para tipos de archivo comunes. Ahora puede procesar un [amplia gama de tipos de archivo](/help/assets/file-format-support.md) cubre más formatos predeterminados de lo que es posible con versiones anteriores de Experience Manager. Por ejemplo, la extracción en miniatura de los formatos PSD y PSB ahora es posible que las soluciones de terceros que antes eran necesarias, como [!DNL ImageMagick]. No puede utilizar las configuraciones complejas de [!DNL ImageMagick] para el [!UICONTROL Perfiles de procesamiento] configuración. Uso [!DNL Dynamic Media] para la transcodificación avanzada de vídeos FFmpeg y utilice perfiles de procesamiento para [transcodificación básica de vídeos MP4](/help/assets/manage-video-assets.md#transcode-video).

Asset microservices es un servicio nativo de la nube que se aprovisiona automáticamente y se cablea a [!DNL Experience Manager] en programas y entornos de clientes administrados en Cloud Manager. Para ampliar o personalizar [!DNL Experience Manager], los desarrolladores pueden utilizar el contenido existente o los recursos con representaciones generadas en un entorno de nube para probar y validar su código mediante, mostrar y descargar recursos.

Para realizar una validación completa del código y el proceso que incluya la ingesta y el procesamiento de recursos, implemente los cambios de código en un entorno de desarrollo en la nube mediante [la canalización](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md) y realizar pruebas con la ejecución completa del procesamiento de microservicios de recursos.

## Paridad de características con [!DNL Experience Manager] 6,5 {#cloud-service-feature-status}

[!DNL Experience Manager] como [!DNL Cloud Service] presenta muchas funciones nuevas y formas más eficaces de que funcionen las funciones existentes. Sin embargo, al moverse de [!DNL Experience Manager] de 6,5 a [!DNL Experience Manager] como [!DNL Cloud Service], es posible que observe que algunas funciones funcionan de forma diferente, no están disponibles o están disponibles parcialmente. La siguiente es una lista de estas funciones. Además, consulte la [funciones obsoletas y eliminadas](/help/release-notes/deprecated-removed-features.md).

| Funcionalidad o caso de uso | Estado en [!DNL Experience Manager] como [!DNL Cloud Service] | Comentarios |
|-----|-----|-----|
| [Duplicar detección de recursos](/help/assets/manage-digital-assets.md#detect-duplicate-assets) | Funciona de forma diferente | Consulte [cómo funcionaba en [!DNL Experience Manager] 6,5](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/duplicate-detection.html). |
| [Representaciones de Solo para ubicación (FPO)](/help/assets/configure-fpo-renditions.md) | Funciona de forma diferente | Los perfiles de procesamiento utilizan microservicios de recursos para generar representaciones de FPO. En Experience Manager 6.5, una solución de terceros como [!DNL ImageMagick] estaba disponible para generar las representaciones. |
| Reescritura de metadatos | Funciona de forma diferente | Deshabilitado de forma predeterminada. Habilite el lanzador del flujo de trabajo correspondiente si es necesario. La reescritura se gestiona mediante microservicios de recursos. |
| Procesamiento de recursos cargados mediante el Administrador de paquetes | Necesita intervención manual | Vuelva a procesar manualmente con el **[!UICONTROL Volver a procesar el recurso]** acción. |
| Detección de tipo MIME | No compatible. | Si carga un recurso digital sin extensión o con una extensión incorrecta, es posible que no se procese como desee. Los usuarios aún pueden almacenar los archivos binarios sin una extensión en DAM. Consulte [Detección de tipo MIME en [!DNL Experience Manager] 6,5](https://experienceleague.adobe.com/docs/experience-manager-65/assets/administer/detect-asset-mime-type-with-tika.html). |
| Generación de subrecursos para un activo compuesto | No compatible. | Es posible que no se cumplan los casos de uso dependientes, como las anotaciones. Consulte [creación de subrecursos en [!DNL Experience Manager] 6,5](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/managing-linked-subassets.html#generate-subassets). La vista previa del PDF de algunos tipos de archivo está disponible a partir de [Versión 2021.7.0](/help/release-notes/release-notes-cloud/release-notes-current.md). |
| Edición de imágenes | No compatible | La edición de recursos no es compatible con Experience Manager as a Cloud Service. Consulte [funcionamiento en Experience Manager 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/manage-assets.html#editing-images). |
| Página de inicio | No compatible | Consulte [[!DNL Assets] Home Page experience in [!DNL Experience Manager] 6,5](https://experienceleague.adobe.com/docs/experience-manager-65/assets/using/assets-home-page.html) |
| Extraer recursos del archivo ZIP | No compatible | Consulte [extracción ZIP en [!DNL Experience Manager] 6,5](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/manage-assets.html#extractzip). |
| Clasificaciones de activos | No compatible | No se admite el widget de clasificación del editor de esquemas de metadatos. |
| Filtro de disposición de contenido | No compatible | Un caso de uso habitual de `ContentDispositionFilter` permite a los administradores configurar [!DNL Experience Manager] para servir archivos HTML y abrir archivos PDF en línea en lugar de descargarlos. En las instancias de publicación, puede administrar la disposición mediante la configuración de Dispatcher. En las instancias de Autor, el Adobe no recomienda la modificación del encabezado Disposición de contenido . Consulte [Filtro Disposición de contenido en [!DNL Experience Manager] 6,5](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/content-disposition-filter.html). |
| Plantilla de sesión fotográfica del producto | No compatible | Consulte [plantilla de sesión fotográfica del producto en [!DNL Experience Manager] 6,5](https://experienceleague.adobe.com/docs/experience-manager-65/authoring/projects/managing-product-information.html). |
| Traducción inteligente | No compatible | [Traducción inteligente](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/translation/smart-translation-search-feature-video-use.html) no es compatible con [!DNL Experience Manager] como [!DNL Cloud Service]. |
| WebDAV | No compatible | Para obtener alternativas, consulte [[!DNL Creative Cloud] integración](/help/assets/aem-cc-integration-best-practices.md) o [Material de referencia para desarrolladores](/help/assets/developer-reference-material-apis.md). |
| IU clásica | No compatible | Solo está disponible la interfaz de usuario táctil. |

**Consulte también**

* [Traducir recursos](translate-assets.md)
* [API HTTP de Recursos](mac-api-assets.md)
* [Formatos de archivo compatibles con Assets](file-format-support.md)
* [Buscar recursos](search-assets.md)
* [Recursos conectados](use-assets-across-connected-assets-instances.md)
* [Informes de Asset](asset-reports.md)
* [Esquemas de metadatos](metadata-schemas.md)
* [Descarga de recursos](download-assets-from-aem.md)
* [Administración de metadatos](manage-metadata.md)
* [Facetas de búsqueda](search-facets.md)
* [Administrar colecciones](manage-collections.md)
* [Importación masiva de metadatos](metadata-import-export.md)

>[!MORELIKETHIS]
>
>Los siguientes recursos están disponibles para [!DNL Experience Manager] como [!DNL Cloud Service]:
>
>* [Lista de funciones obsoletas y eliminadas](/help/release-notes/deprecated-removed-features.md)
>* [Introducción](/help/overview/introduction.md)
>* [Novedades y diferencias](/help/overview/what-is-new-and-different.md)
>* [La arquitectura](/help/overview/architecture.md)
>* [Cambios importantes ](/help/release-notes/aem-cloud-changes.md)
>* [Cambios importantes  [!DNL Sites]](/help/sites-cloud/sites-cloud-changes.md)
>* [Tutoriales en vídeo](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/overview.html?lang=es)

