---
title: Cambios notables en Adobe Experience Manager Assets como Cloud Service
description: Cambios notables en Adobe Experience Manager Assets en AEM Cloud Service en comparación con Adobe Experience Manager 6.5.
translation-type: tm+mt
source-git-commit: 2f5925613219a475a4e7d780f7d2bb3da8148e31
workflow-type: tm+mt
source-wordcount: '628'
ht-degree: 19%

---


# Notable changes to Experience Manager Assets as a Cloud Service {#notable-changes}

Adobe Experience Manager as a Cloud Service ofrece muchas nuevas funciones y posibilidades para gestionar sus Proyectos AEM. Sin embargo, existen muchas diferencias entre los Experience Manager de Recursos in situ o en el servicio administrado por Adobe en comparación con el Experience Manager como Cloud Service. Este documento destaca las importantes diferencias que existen entre las capacidades de Recursos.

Las principales diferencias con respecto al Experience Manager 6.5 se encuentran en los siguientes ámbitos:

* [Carga](#asset-ingestion)e ingesta de recursos.
* [Microservicios de recursos para procesamiento](#asset-microservices)nativo de la nube.
* [Eliminación de la IU clásica](#classic-ui).

>[!NOTE]
>
>Este documento destaca los cambios notables que se han producido en AEM Assets. Para ver los cambios generales a AEM como Cloud Service y otros módulos, consulte:
>
>* [Introducción a Adobe Experience Manager as a Cloud Service](/help/overview/introduction.md)
>* Una [descripción general de AEM as a Cloud Service: novedades y diferencias](/help/overview/what-is-new-and-different.md)
>* La [arquitectura](/help/core-concepts/architecture.md) de Adobe Experience Manager as a Cloud Service
>* [Cambios importantes en AEM as a Cloud Service (Notas de la versión)](/help/release-notes/aem-cloud-changes.md)
>* [Cambios importantes en AEM Sites as a Cloud Service](/help/sites-cloud/sites-cloud-changes.md)
>* [Tutoriales de Adobe Experience Manager as a Cloud Service](https://docs.adobe.com/content/help/es-ES/experience-manager-learn/cloud-service/overview.html)


## Carga e ingestión de recursos {#asset-ingestion}

La carga de recursos se ha optimizado para lograr una mayor eficacia al permitir una mejor ampliación de la ingesta de recursos y cargas más rápidas. Se han actualizado las capacidades del producto (interfaces de usuario web, clientes de escritorio). Sin embargo, esto puede afectar a algunas personalizaciones existentes.

* Experience Manager utiliza el principio de acceso binario directo para los microservicios de carga y descarga y de recursos para el procesamiento de recursos. Consulte [información general sobre la ingesta](/help/assets/asset-microservices-overview.md)de recursos.
   * Carga de recursos [con acceso](/help/assets/asset-microservices-overview.md#asset-upload-with-direct-binary-access)binario directo.
   * Para obtener información técnica, consulte el protocolo de carga binaria [directa y las API](/help/assets/developer-reference-material-apis.md#upload-binary).
* El flujo de trabajo predeterminado de **[!UICONTROL actualización de recursos DAM]** en versiones anteriores de AEM ya no está disponible. En su lugar, los microservicios de recursos proporcionan un servicio escalable y fácilmente disponible que cubre la mayor parte del procesamiento de recursos predeterminado (representaciones, extracción de metadatos, extracción de texto para indexación).
   * Consulte [Configuración y uso de microservicios de recursos](/help/assets/asset-microservices-configure-and-use.md)
   * Para tener pasos personalizados de flujo de trabajo en el procesamiento, se pueden utilizar flujos de trabajo [de](/help/assets/asset-microservices-configure-and-use.md#post-processing-workflows) postprocesamiento.
* Assets that come in via Package Manager require manual reprocessing using the **[!UICONTROL Reprocess Asset]** action in the Assets interface.

Las representaciones estándar generadas con los microservicios de recursos se almacenan de forma compatible con versiones anteriores en los nodos del repositorio de recursos (las mismas convenciones de nombres).

## Desarrollar y probar microservicios de activos {#asset-microservices}

Los microservicios de recursos proporcionan un procesamiento escalable y flexible de los recursos mediante servicios en la nube. Adobe administra los servicios en la nube para una gestión óptima de los distintos tipos de recursos y opciones de procesamiento. Los microservicios de recursos ayudan a evitar la necesidad de herramientas y métodos de procesamiento de terceros (como ImageMagick) y simplifican las configuraciones, al tiempo que proporcionan una funcionalidad lista para usar para tipos de archivos comunes. Ahora puede procesar una [amplia gama de tipos](/help/assets/file-format-support.md) de archivos que cubren más formatos listos para usar que los que se pueden procesar en versiones anteriores de Experience Manager. Por ejemplo, ahora es posible la extracción en miniatura de los formatos PSD y PSB que anteriormente requerían soluciones de terceros como ImageMagick. No puede utilizar las configuraciones complejas de ImageMagick para la configuración de Perfiles [!UICONTROL de] procesamiento. Se utiliza [!DNL Dynamic Media] para la transcodificación FFmpeg de vídeos y perfiles de procesamiento para la transcodificación [básica de vídeos](/help/assets/manage-video-assets.md#transcode-video)MP4.

Asset microservices es un servicio nativo de la nube que se aprovisiona automáticamente y se cablea al Experience Manager en programas y entornos del cliente administrados en Cloud Manager. Para ampliar o personalizar el Experience Manager, los desarrolladores pueden utilizar el contenido o los recursos existentes con las representaciones generadas en un entorno de nube, para probar y validar su código mediante, visualización o descarga de recursos.

Para realizar una validación completa del código y del proceso, incluida la ingesta y el procesamiento de recursos, implemente los cambios de código en un entorno de desarrollo en la nube mediante [la canalización](/help/implementing/cloud-manager/configure-pipeline.md) y la prueba con la ejecución completa del procesamiento de los microservicios de recursos.

## Eliminación de la IU clásica {#classic-ui}

La IU clásica ya no está disponible en Experience Manager como Cloud Service. La interfaz estándar es la IU táctil.
