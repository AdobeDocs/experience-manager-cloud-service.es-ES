---
title: Cambios notables en Adobe Experience Manager Assets como Cloud Service
description: Cambios notables en Adobe Experience Manager Assets en AEM Cloud Service en comparación con Adobe Experience Manager 6.5.
translation-type: tm+mt
source-git-commit: b1586cd9d6b3e9da115bff802d840a72d1207e4a
workflow-type: tm+mt
source-wordcount: '626'
ht-degree: 18%

---


# Cambios notables en Recursos Experience Manager como Cloud Service {#notable-changes}

Adobe Experience Manager as a Cloud Service ofrece muchas nuevas funciones y posibilidades para gestionar sus Proyectos AEM. Sin embargo, existen muchas diferencias entre los Experience Manager de Recursos in situ o en el servicio administrado por Adobe en comparación con el Experience Manager como Cloud Service. Este documento destaca las importantes diferencias que existen entre las capacidades de Recursos.

Las principales diferencias con respecto al Experience Manager 6.5 se encuentran en los siguientes ámbitos:

* [Carga](#asset-ingestion) e ingesta de recursos.
* [Microservicios de recursos para procesamiento](#asset-microservices) nativo de la nube.
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
>* [Tutoriales de Adobe Experience Manager as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/overview.html)


## Carga y ingesta de recursos {#asset-ingestion}

La carga de recursos se ha optimizado para lograr una mayor eficacia al permitir una mejor ampliación de la ingesta de recursos y cargas más rápidas. Se han actualizado las capacidades del producto (interfaces de usuario web, clientes de escritorio). Sin embargo, esto puede afectar a algunas personalizaciones existentes.

* Experience Manager utiliza el principio de acceso binario directo para los microservicios de carga y descarga y de recursos para el procesamiento de recursos. Consulte [información general sobre la ingestión de recursos](/help/assets/asset-microservices-overview.md).
   * Carga de recursos [con acceso binario directo](/help/assets/asset-microservices-overview.md#asset-upload-with-direct-binary-access).
   * Para obtener más información técnica, consulte [protocolo de carga binaria directa y API](/help/assets/developer-reference-material-apis.md#upload-binary).
* El flujo de trabajo predeterminado de **[!UICONTROL actualización de recursos DAM]** en versiones anteriores de AEM ya no está disponible. En su lugar, los microservicios de recursos proporcionan un servicio escalable y fácilmente disponible que cubre la mayor parte del procesamiento de recursos predeterminado (representaciones, extracción de metadatos, extracción de texto para indexación).
   * Consulte [configuración y uso de microservicios de recursos](/help/assets/asset-microservices-configure-and-use.md)
   * Para tener pasos personalizados del flujo de trabajo en el procesamiento, se pueden utilizar [flujos de trabajo de postprocesamiento](/help/assets/asset-microservices-configure-and-use.md#post-processing-workflows).
* Los recursos que se incluyen mediante el Administrador de paquetes requieren un reprocesamiento manual mediante la acción **[!UICONTROL Reprocesar recurso]** de la interfaz de Recursos.

Las representaciones estándar generadas con los microservicios de recursos se almacenan de forma compatible con versiones anteriores en los nodos del repositorio de recursos (las mismas convenciones de nombres).

## Desarrollar y probar microservicios de activos {#asset-microservices}

Los microservicios de recursos proporcionan un procesamiento escalable y flexible de los recursos mediante servicios en la nube. Adobe administra los servicios en la nube para una gestión óptima de los distintos tipos de recursos y opciones de procesamiento. Los microservicios de recursos ayudan a evitar la necesidad de herramientas y métodos de procesamiento de terceros (como ImageMagick) y simplifican las configuraciones, al tiempo que proporcionan una funcionalidad lista para usar para tipos de archivos comunes. Ahora puede procesar una [amplia gama de tipos de archivos](/help/assets/file-format-support.md) que cubren más formatos listos para usar que lo que es posible con versiones anteriores de Experience Manager. Por ejemplo, ahora es posible la extracción en miniatura de los formatos PSD y PSB que anteriormente requerían soluciones de terceros como ImageMagick. No puede utilizar las configuraciones complejas de ImageMagick para la configuración [!UICONTROL Perfiles de procesamiento]. Use [!DNL Dynamic Media] para la transcodificación de videos de FFmpeg y utilice perfiles de procesamiento para [transcodificación básica de videos MP4](/help/assets/manage-video-assets.md#transcode-video).

Asset microservices es un servicio nativo de la nube que se aprovisiona automáticamente y se cablea al Experience Manager en programas y entornos del cliente administrados en Cloud Manager. Para ampliar o personalizar el Experience Manager, los desarrolladores pueden utilizar el contenido o los recursos existentes con las representaciones generadas en un entorno de nube, para probar y validar su código mediante, visualización o descarga de recursos.

Para llevar a cabo una validación end-to-end del código y el proceso, incluyendo la ingesta y el procesamiento de recursos, implemente los cambios de código en un entorno de desarrollo en la nube mediante [el proceso](/help/implementing/cloud-manager/configure-pipeline.md) y realice pruebas con la ejecución completa del procesamiento de los microservicios de recursos.

## Eliminación de la IU clásica {#classic-ui}

La IU clásica ya no está disponible en Experience Manager como Cloud Service. La interfaz estándar es la IU táctil.
