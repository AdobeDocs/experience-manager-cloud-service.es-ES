---
title: Integración de AEM Assets durante la creación de contenido para Edge Delivery Services
description: Aprenda a integrar a los AEM Assets con los Edge Delivery Services. Esta integración le permite integrar AEM Assets con Microsoft Word y Google Docs, integrar AEM Assets con Universal Editor, integrar Dynamic Media con capacidades OpenAPI con Universal Editor e integrar Dynamic Media con capacidades OpenAPI con Microsoft Word y Google Docs.
exl-id: e58db2ce-a55a-49b3-ae8e-709b5ea8d095
source-git-commit: 105081c9124a85581240b19866adc271ea8bb190
workflow-type: tm+mt
source-wordcount: '743'
ht-degree: 3%

---

# Integración de AEM Assets durante la creación de contenido para Edge Delivery Services {#integrate-aem-assets-while-authoring-for-edge-delivery-services}

![EDS2](/help/assets/assets/EDS2.png)

[Edge Delivery Services](https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/edge-delivery/overview) es un conjunto de servicios que se pueden componer y que permiten un alto grado de flexibilidad en la forma en que se crea y se entrega contenido en el sitio web. AEM Puede usar la creación de [administración de contenido ](/help/sites-cloud/authoring/author-publish.md)y la creación de [WYSIWYG mediante el editor universal, así como la creación basada en documentos](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/edge-delivery/wysiwyg-authoring/authoring).

Puede editar contenido en:

* [Documentos de Microsoft Word o Google](#integrate-aem-assets-with-document-based-authoring-tools)
* [Editor universal](#integrate-aem-assets-with-universal-editor)

Después de editar el contenido, puede publicarlo en Edge Delivery Services.

## Integración de AEM Assets con flujos de creación basados en documentos para Edge Delivery Services {#integrate-aem-assets-with-document-based-authoring-tools}

La integración de AEM Assets con las herramientas de creación basada en documentos, como Microsoft Word o Google Docs, proporciona un selector de recursos directamente en el editor. Utilice este selector de recursos para acceder a los AEM Assets e insertar los recursos aprobados en el documento.

Si ya tiene un sitio web de Edge Delivery Services, consulte [Complemento de AEM Assets](https://github.com/adobe-rnd/aem-assets-plugin/blob/main/README.md) para integrar AEM Assets AEM con su proyecto de existente. Si no tiene un sitio web de Edge Delivery Services, vea las secciones [Requisitos previos](#integrate-aem-assets-with-microsoft-word-and-google-docs) e [Integración de AEM Assets con el entorno de creación basada en documentos](#integrate-aem-assets-with-microsoft-word-or-google-docs-to-use-aem-assets-with-microsoft-word-or-google-docs) a continuación.

### Requisitos previos{#integrate-aem-assets-with-microsoft-word-and-google-docs}

Antes de empezar, asegúrese de que el entorno de creación basada en documentos está listo:

* AEM Integrar la con una herramienta de creación basada en documentos para configurar el entorno de creación. Consulte [Introducción - Tutorial para desarrolladores](https://www.aem.live/developer/tutorial) para configurar el entorno de creación.

### Integración de AEM Assets con el entorno de creación basada en documentos{#integrate-aem-assets-with-microsoft-word-or-google-docs-to-use-aem-assets-with-microsoft-word-or-google-docs}

Configure el complemento Sidekick de AEM Assets para que utilice recursos durante la creación de contenido en documentos de Microsoft Word o Google.

* Consulte [Complemento de Sidekick de Adobe Experience Manager Assets](https://www.aem.live/docs/aem-assets-sidekick-plugin#using-experience-manager-assets-for-website-authors) para obtener información sobre cómo acceder y utilizar AEM Assets en documentos de Microsoft Word o Google.
* Consulte [Configuración del complemento Adobe Experience Manager Assets Sidekick](https://www.aem.live/developer/configuring-aem-assets-sidekick-plugin) para obtener más información sobre la configuración.
  ![my-assets-sidebar](/help/assets/assets/my-assets-sidebar.png)

## Entrega de recursos mediante Dynamic Media con funciones de OpenAPI {#integrate-Dynamic-Media-with-OpenAPI-capabilities-with-Microsoft-Word-Google-Docs-and-universal-editor}

También puede utilizar recursos entregados mediante DM con funciones de OpenAPI. Proporciona muchos beneficios, como:

* Acceso solo a recursos aprobados por la marca (imágenes, vídeos, PDF y otros tipos de recursos) de Cloud Service de AEM Assets.
* Administración (referencias frente a copias del recurso), que ayuda a la propagación automática de eventos del ciclo vital de recursos como caducidad, eliminación y actualizaciones.
* Representaciones de imágenes dinámicas y recorte inteligente.
* Entrega y optimización de medios enriquecidos, como la transmisión de vídeo adaptable lista para usar y la entrega de recursos originales para PDF.
* Informe de impresiones de nivel de recurso ([disponibilidad limitada](/help/assets/manage-reports-assets-view.md#dynamic-media-delivery-reports)).

Para obtener más información sobre las funcionalidades, consulte [Dynamic Media con funcionalidades de OpenAPI](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/dynamicmedia/dynamic-media-open-apis/dynamic-media-open-apis-overview).

### Requisitos previos {#prerequisites-for-dm-with-openapi-capabilities-to-use-aem-assets}

Para utilizar la referencia de recursos, debe tener:

* Derecho a un entorno de Cloud Service de Assets donde Dynamic Media con capacidades de API abierta está habilitado.
* Una licencia de Dynamic Media.
* El complemento de la barra de tareas de los AEM Assets habilitado con la copia de referencia para los recursos de imagen habilitada. Para obtener más información, vea [this](https://www.aem.live/developer/configuring-aem-assets-sidekick-plugin#copymode) para la creación basada en documentos y [this](https://developer.adobe.com/uix/docs/extension-manager/extension-developed-by-adobe/configurable-asset-picker/#extension-overview) para la creación basada en el editor universal.
* Assets que se han aprobado. Los recursos aprobados tienen `dam:status=Approved` a través del backend de los Cloud Service de Assets o de las acciones de la interfaz de usuario.

### Uso de recursos entregados mediante Dynamic Media con funciones de OpenAPI{#how-to-use-Dynamic-Media-with-OpenAPI-assets}

Para utilizar recursos entregados mediante Dynamic Media con funciones de OpenAPI durante la creación de contenido, consulte:

* [Usando referencias de imagen](https://www.aem.live/docs/aem-assets-sidekick-plugin#using-image-references-when-authoring-content)
* [Usando referencias de vídeo](https://www.aem.live/docs/aem-assets-sidekick-plugin#using-video-references-when-authoring-content)
* [Uso de referencias de recursos para recursos que no son de imagen y de vídeo, como PDF, archivos zip y más](https://www.aem.live/docs/aem-assets-sidekick-plugin#using-asset-references-for-pdf-zip-etc-when-authoring-content)

Consulte este vídeo para aprender a distribuir recursos mediante Dynamic Media con las funciones de OpenAPI.

>[!VIDEO](https://video.tv.adobe.com/v/3441155)

## Sitio de Edge Delivery Services de muestra{#example-of-an-Edge-Delivery-Services-site}

Ver [Viajes WKND](http://bit.ly/3DExLnf). Este sitio se crea utilizando las capacidades de creación basadas en documentos de los Edge Delivery Services. El contenido del sitio se creó en [Google Docs](https://drive.google.com/drive/folders/1HCCHRWp4HJIXW_cUv5cRDQ5DzzqiZsXT), con Dynamic Media y funciones OpenAPI para la entrega de recursos. Una vez creado, el contenido se publica directamente desde el documento. Para esta configuración de creación basada en documentos, todos los archivos, carpetas, configuraciones, estilos del sitio web y códigos de funcionalidad esenciales se almacenan en este [repositorio Git](https://github.com/hlxsites/franklin-assets-selector/tree/aem-dynamicmedia-demo/blocks).

## Integración de AEM Assets con flujos de creación basados en Universal Editor para Edge Delivery Services {#integrate-aem-assets-with-universal-editor}

Configure el editor universal para que se integre con los AEM Assets. Esta integración le permite utilizar Dynamic Media con las funciones de OpenAPI para entregar recursos.

* Consulte [Configuración en el sitio de Edge Delivery](https://developer.adobe.com/uix/docs/extension-manager/extension-developed-by-adobe/configurable-asset-picker/#configuration-in-edge-delivery-site) para agregar una función de selector de recursos personalizada en el editor universal. El selector de recursos personalizado permite insertar recursos directamente en el contenido del editor universal.
* Consulte [Descripción general de la extensión](https://developer.adobe.com/uix/docs/extension-manager/extension-developed-by-adobe/configurable-asset-picker/#extension-overview) para obtener información sobre cómo acceder a los AEM Assets e insertar los recursos durante la creación en el editor universal.
