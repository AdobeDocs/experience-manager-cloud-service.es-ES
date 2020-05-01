---
title: Cambios notables en Recursos Adobe Experience Manager como servicio de nube
description: Cambios notables en Recursos Adobe Experience Manager en AEM Cloud Service en comparación con Adobe Experience Manager 6.5.
translation-type: tm+mt
source-git-commit: 37ff6912837ba78c90526e8f8322b9002e9a4304

---


# Notable changes to Experience Manager Assets as a Cloud Service {#notable-changes}

Adobe Experience Manager como servicio de nube ofrece muchas funciones y posibilidades nuevas para administrar sus proyectos de AEM. Sin embargo, existen muchas diferencias entre Experience Manager Assets in situ o en Adobe Managed Service en comparación con Experience Manager como un servicio de nube. Este documento destaca las importantes diferencias que existen entre las capacidades de Recursos. Para ver otros cambios, consulte los [cambios genéricos a Experience Manager como un servicio](/help/release-notes/aem-cloud-changes.md)de nube.

Las principales diferencias en comparación con Experience Manager 6.5 se encuentran en las siguientes áreas:

* [Carga](#asset-ingestion)e ingesta de recursos.
* [Microservicios de recursos para procesamiento](#asset-microservices)en la nube.
* [Eliminación de la IU clásica](#classic-ui).

## Carga e ingestión de recursos {#asset-ingestion}

La carga de recursos se ha optimizado para lograr una mayor eficacia al permitir una mejor ampliación de la ingesta de recursos y cargas más rápidas. Se han actualizado las capacidades del producto (interfaces de usuario web, clientes de escritorio). Sin embargo, esto puede afectar a algunas personalizaciones existentes.

* Experience Manager utiliza el principio de acceso binario directo para los microservicios de carga y descarga y de recursos para el procesamiento de recursos. Consulte [información general sobre la ingesta](/help/assets/asset-microservices-overview.md)de recursos.
   * Carga de recursos [con acceso](/help/assets/asset-microservices-overview.md#asset-upload-with-direct-binary-access)binario directo.
   * Para obtener información técnica, consulte el protocolo de carga binaria [directa y las API](/help/assets/developer-reference-material-apis.md#overview-binary-upload).
* El flujo de trabajo predeterminado de **[!UICONTROL actualización de recursos DAM]** en versiones anteriores de AEM ya no está disponible. En su lugar, los microservicios de recursos proporcionan un servicio escalable y fácilmente disponible que cubre la mayor parte del procesamiento de recursos predeterminado (representaciones, extracción de metadatos, extracción de texto para indexación).
   * Consulte [Configuración y uso de microservicios de recursos](/help/assets/asset-microservices-configure-and-use.md)
   * Para tener pasos personalizados de flujo de trabajo en el procesamiento, se pueden utilizar flujos de trabajo [de](/help/assets/asset-microservices-configure-and-use.md#post-processing-workflows) postprocesamiento.
* Assets that come in via Package Manager require manual reprocessing using the **[!UICONTROL Reprocess Asset]** action in the Assets interface.

Las representaciones estándar generadas con los microservicios de recursos se almacenan de forma compatible con versiones anteriores en los nodos del repositorio de recursos (las mismas convenciones de nombres).

## Desarrollar y probar microservicios de activos {#asset-microservices}

Los microservicios de recursos proporcionan un procesamiento escalable y flexible de los recursos mediante servicios en la nube. Adobe administra los servicios en la nube para una gestión óptima de los distintos tipos de recursos y opciones de procesamiento. Los microservicios de recursos ayudan a evitar la necesidad de herramientas y métodos de procesamiento de terceros (como ImageMagick) y simplifican las configuraciones, al tiempo que proporcionan una funcionalidad lista para usar para tipos de archivos comunes. Ahora puede procesar una [amplia gama de tipos](/help/assets/file-format-support.md) de archivos que cubren más formatos listos para usar que los que se pueden usar en versiones anteriores de Experience Manager. Por ejemplo, ahora es posible la extracción en miniatura de los formatos PSD y PSB que anteriormente requerían soluciones de terceros como ImageMagick. No puede utilizar las configuraciones complejas de ImageMagick para la configuración de Perfiles [!UICONTROL de] procesamiento. Además, utilice [!DNL Dynamic Media] la transcodificación FFmpeg de vídeos.

Asset microservices es un servicio nativo de la nube que se aprovisiona automáticamente y se envía por cable a Experience Manager en programas y entornos de clientes administrados en Cloud Manager. Para ampliar o personalizar Experience Manager, los desarrolladores pueden utilizar el contenido o los recursos existentes con las representaciones generadas en un entorno en la nube para probar y validar su código mediante, mostrar y descargar recursos.

Para realizar una validación completa del código y del proceso, incluida la ingesta y el procesamiento de recursos, implemente los cambios de código en un entorno de desarrollo en la nube mediante [la canalización](/help/implementing/cloud-manager/configure-pipeline.md) y la prueba con la ejecución completa del procesamiento de los microservicios de recursos.

## Eliminación de la IU clásica {#classic-ui}

La IU clásica ya no está disponible en Experience Manager como servicio de nube. La interfaz estándar es la IU táctil.
