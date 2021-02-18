---
title: Cambios notables en [!DNL Adobe Experience Manager Assets] como [!DNL Cloud Service]
description: Cambios notables en [!DNL Adobe Experience Manager Assets] in [!DNL Experience Manager] as a [!DNL Cloud Service] en comparación con [!DNL Adobe Experience Manager 6.5.
translation-type: tm+mt
source-git-commit: 6dc6445e4019664525629fe2204d255cfee37a81
workflow-type: tm+mt
source-wordcount: '743'
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
* No se admite la reescritura de metadatos. Consulte [reescritura de metadatos en [!DNL Experience Manager] 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/assets/administer/xmp-writeback.html).
* Los recursos que se cargan mediante el Administrador de paquetes requieren un reprocesamiento manual mediante la acción **[!UICONTROL Volver a procesar recurso]** de la interfaz de usuario [!DNL Assets].
* [!DNL Assets] no detecta automáticamente el tipo MIME de los recursos cargados. Un recurso digital sin extensión o con una extensión incorrecta no se procesa como desee. Por ejemplo, al cargar estos recursos, puede que no suceda nada o que se aplique un perfil de procesamiento incorrecto al recurso. Los usuarios pueden almacenar los archivos binarios sin extensión en DAM. Consulte [Detección de tipo MIME en [!DNL Experience Manager] 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/assets/administer/detect-asset-mime-type-with-tika.html).
* [!DNL Experience Manager] como  [!DNL Cloud Service] no genera subrecursos para recursos compuestos. Consulte [creación de subrecursos en [!DNL Experience Manager] 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/managing-linked-subassets.html#generate-subassets).
* [!DNL Assets] La experiencia de página de inicio no está disponible. Consulte [[!DNL Assets] Home Page experience in [!DNL Experience Manager] 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/assets/using/assets-home-page.html).
* La detección de recursos de duplicado funciona de manera distinta a [en [!DNL Experience Manager] 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/duplicate-detection.html).
* Las representaciones de solo colocación (FPO) se generan de forma diferente en comparación con las versiones anteriores de [!DNL Experience Manager]. Consulte [Representación de FPO para [!DNL Experience Manager] como [!DNL Cloud Service]](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/configure-aem-assets-for-asset-link.ug.html).
* Cuando se carga un archivo ZIP, [!DNL Experience Manager] como [!DNL Cloud Service] no extrae los recursos incluidos en el archivo. Consulte la [extracción ZIP en [!DNL Experience Manager] 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/manage-assets.htmln#extractzip).

Las representaciones estándar generadas con los microservicios de recursos se almacenan de forma compatible con versiones anteriores en los nodos del repositorio de recursos utilizando las mismas convenciones de nombres.

## Desarrollar y probar microservicios de activos {#asset-microservices}

Los microservicios de recursos proporcionan un procesamiento escalable y flexible de los recursos mediante servicios en la nube. Adobe administra los servicios en la nube para una gestión óptima de los distintos tipos de recursos y opciones de procesamiento. Los microservicios de recursos ayudan a evitar la necesidad de herramientas y métodos de procesamiento de terceros (como ImageMagick) y simplifican las configuraciones, al tiempo que proporcionan una funcionalidad lista para usar para tipos de archivos comunes. Ahora puede procesar una [amplia gama de tipos de archivos](/help/assets/file-format-support.md) que cubren más formatos listos para usar que lo que es posible con versiones anteriores de Experience Manager. Por ejemplo, ahora es posible la extracción en miniatura de los formatos PSD y PSB que anteriormente requerían soluciones de terceros como ImageMagick. No puede utilizar las configuraciones complejas de ImageMagick para la configuración [!UICONTROL Perfiles de procesamiento]. Utilice [!DNL Dynamic Media] para la transcodificación avanzada de vídeos con FFmpeg y utilice perfiles de procesamiento para [transcodificación básica de vídeos MP4](/help/assets/manage-video-assets.md#transcode-video).

Asset microservices es un servicio nativo de la nube que se aprovisiona automáticamente y se cablea a [!DNL Experience Manager] en programas de clientes y entornos administrados en Cloud Manager. Para ampliar o personalizar [!DNL Experience Manager], los desarrolladores pueden utilizar el contenido o los recursos existentes con las representaciones generadas en un entorno en la nube, para probar y validar su código mediante, visualización y descarga de recursos.

Para llevar a cabo una validación end-to-end del código y el proceso, incluyendo la ingesta y el procesamiento de recursos, implemente los cambios de código en un entorno de desarrollo en la nube mediante [el proceso](/help/implementing/cloud-manager/configure-pipeline.md) y realice pruebas con la ejecución completa del procesamiento de los microservicios de recursos.

## Eliminación de la IU clásica {#classic-ui}

La IU clásica ya no está disponible en [!DNL Experience Manager] como [!DNL Cloud Service]. Solo está disponible la IU táctil.

>[!MORELIKETHIS]
>
>Los siguientes recursos están disponibles para [!DNL Experience Manager] como [!DNL Cloud Service]:
>
>* [Introducción](/help/overview/introduction.md)
>* [Novedades y diferencias](/help/overview/what-is-new-and-different.md)
>* [La arquitectura](/help/core-concepts/architecture.md)
>* [Cambios notables](/help/release-notes/aem-cloud-changes.md)
>* [Cambios notables [!DNL Sites]](/help/sites-cloud/sites-cloud-changes.md)
>* [Tutoriales de vídeo](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/overview.html)

