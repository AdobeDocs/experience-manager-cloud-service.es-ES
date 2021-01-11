---
title: Cambios notables en [!DNL Adobe Experience Manager Assets] como [!DNL Cloud Service]
description: Cambios notables en [!DNL Adobe Experience Manager Assets] in [!DNL Experience Manager] as a [!DNL Cloud Service] en comparación con [!DNL Adobe Experience Manager 6.5.
translation-type: tm+mt
source-git-commit: ed449eea146ec18bdc4d25ae4938f9a36180037d
workflow-type: tm+mt
source-wordcount: '605'
ht-degree: 3%

---


# Cambios notables en [!DNL Experience Manager Assets] como [!DNL Cloud Service] {#notable-changes}

[!DNL Adobe Experience Manager] como  [!DNL Cloud Service] trae muchas nuevas características y posibilidades para administrar sus proyectos Experience Manager. Existen muchas diferencias entre [!DNL Experience Manager Assets] in situ o alojado como servicio administrado por Adobe en comparación con [!DNL Experience Manager] como [!DNL Cloud Service]. Este artículo destaca las importantes diferencias que existen entre las capacidades [!DNL Assets].

Las principales diferencias en comparación con [Experience Manager] 6.5 se encuentran en las siguientes áreas:

* [Transferencia, carga y procesamiento](#asset-ingestion) de recursos.
* [Microservicios de recursos para procesamiento](#asset-microservices) nativo de la nube.
* [Eliminación de la IU clásica](#classic-ui).

## Procesamiento e ingesta de recursos {#asset-ingestion}

La carga de recursos se optimiza para lograr una mayor eficacia al permitir una mejor ampliación de la ingesta, cargas más rápidas, un procesamiento más rápido mediante microservicios y una ingestión masiva. Se actualizan las capacidades del producto (interfaces de usuario web, clientes de escritorio). Además, esto puede afectar a algunas personalizaciones existentes.

* [!DNL Experience Manager] utiliza el principio de acceso binario directo para cargar y descargar recursos y utiliza los microservicios de recursos para procesar recursos. Consulte [descripción general de microservicios](/help/assets/asset-microservices-overview.md).
   * Carga de recursos [con acceso binario directo](/help/assets/asset-microservices-overview.md#asset-upload-with-direct-binary-access).
   * Para obtener información técnica, consulte [protocolo de carga binaria directa y API](/help/assets/developer-reference-material-apis.md#upload-binary).
   * Para ver una comparación de los métodos de API disponibles para operaciones CRUD básicas, consulte [API y operaciones de recursos](/help/assets/developer-reference-material-apis.md#use-cases-and-apis).
* El flujo de trabajo predeterminado de **[!UICONTROL actualización de recursos DAM]** en versiones anteriores de ya no está disponible. [!DNL Experience Manager] En su lugar, los microservicios de recursos proporcionan un servicio escalable y fácilmente disponible que cubre la mayor parte del procesamiento de recursos predeterminado (representaciones, extracción de metadatos y extracción de texto para indexación).
   * Consulte [configurar y utilizar microservicios de recursos](/help/assets/asset-microservices-configure-and-use.md)
   * Para tener pasos personalizados del flujo de trabajo en el procesamiento, se pueden utilizar [flujos de trabajo de postprocesamiento](/help/assets/asset-microservices-configure-and-use.md#post-processing-workflows).
* Los recursos que se cargan mediante el Administrador de paquetes requieren un reprocesamiento manual mediante la acción **[!UICONTROL Volver a procesar recurso]** de la interfaz [!DNL Assets].
* Un recurso digital sin extensión o con una extensión incorrecta no se procesa como desee. Por ejemplo, al cargar estos recursos, puede que no suceda nada o que se aplique un perfil de procesamiento incorrecto al recurso. Los usuarios aún pueden almacenar los archivos binarios en DAM.

Las representaciones estándar generadas con los microservicios de recursos se almacenan de forma compatible con versiones anteriores en los nodos del repositorio de recursos (las mismas convenciones de nombres).

## Desarrollar y probar microservicios de activos {#asset-microservices}

Los microservicios de recursos proporcionan un procesamiento escalable y flexible de los recursos mediante servicios en la nube. Adobe administra los servicios en la nube para una gestión óptima de los distintos tipos de recursos y opciones de procesamiento. Los microservicios de recursos ayudan a evitar la necesidad de herramientas y métodos de procesamiento de terceros (como ImageMagick) y simplifican las configuraciones, al tiempo que proporcionan una funcionalidad lista para usar para tipos de archivos comunes. Ahora puede procesar una [amplia gama de tipos de archivos](/help/assets/file-format-support.md) que cubren más formatos listos para usar que lo que es posible con versiones anteriores de Experience Manager. Por ejemplo, ahora es posible la extracción en miniatura de los formatos PSD y PSB que anteriormente requerían soluciones de terceros como ImageMagick. No puede utilizar las configuraciones complejas de ImageMagick para la configuración [!UICONTROL Perfiles de procesamiento]. Utilice [!DNL Dynamic Media] para la transcodificación avanzada de vídeos con FFmpeg y utilice perfiles de procesamiento para [transcodificación básica de vídeos MP4](/help/assets/manage-video-assets.md#transcode-video).

Asset microservices es un servicio nativo de la nube que se aprovisiona automáticamente y se cablea al Experience Manager en programas y entornos del cliente administrados en Cloud Manager. Para ampliar o personalizar el Experience Manager, los desarrolladores pueden utilizar el contenido o los recursos existentes con las representaciones generadas en un entorno de nube, para probar y validar su código mediante, visualización o descarga de recursos.

Para llevar a cabo una validación end-to-end del código y el proceso, incluyendo la ingesta y el procesamiento de recursos, implemente los cambios de código en un entorno de desarrollo en la nube mediante [el proceso](/help/implementing/cloud-manager/configure-pipeline.md) y realice pruebas con la ejecución completa del procesamiento de los microservicios de recursos.

## Eliminación de la IU clásica {#classic-ui}

La IU clásica ya no está disponible en Experience Manager como [!DNL Cloud Service]. La interfaz estándar es la IU táctil.

>[!MORELIKETHIS]
>
>* [Introducción  [!DNL Adobe Experience Manager] a [!DNL Cloud Service]](/help/overview/introduction.md)
>* Una [descripción general de [!DNL Experience Manager] as a [!DNL Cloud Service] - Qué es lo nuevo y Qué es diferente](/help/overview/what-is-new-and-different.md)
>* La [arquitectura](/help/core-concepts/architecture.md) de [!DNL Experience Manager] como [!DNL Cloud Service]
>* [Cambios notables  [!DNL Experience Manager] a [!DNL Cloud Service]](/help/release-notes/aem-cloud-changes.md)
>* [Cambios notables  [!DNL Experience Manager Sites] a [!DNL Cloud Service]](/help/sites-cloud/sites-cloud-changes.md)
>* [[!DNL Experience Manager] as a [!DNL Cloud Service] Tutoriales](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/overview.html)

