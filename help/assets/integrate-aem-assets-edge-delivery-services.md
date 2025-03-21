---
title: Integración de AEM Assets durante la creación de contenido para Edge Delivery Services
description: Aprenda a integrar los AEM Assets con Edge Delivery Services. Esta integración le permite integrar AEM Assets con Microsoft Word y Google Docs, integrar AEM Assets con Universal Editor, integrar Dynamic Media con las capacidades de OpenAPI con Universal Editor e integrar Dynamic Media con las capacidades de OpenAPI con Microsoft Word y Google Docs.
exl-id: e58db2ce-a55a-49b3-ae8e-709b5ea8d095
source-git-commit: e4a71d1a513bebed67b9571a483871dc16c36daa
workflow-type: tm+mt
source-wordcount: '820'
ht-degree: 3%

---

# Integración de AEM Assets durante la creación de contenido para Edge Delivery Services {#integrate-aem-assets-while-authoring-for-edge-delivery-services}

![Recursos de AEM con UE](/help/assets/assets/EDS2.png)

[Edge Delivery Services](https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/edge-delivery/overview) es un conjunto de servicios que se pueden componer y que permiten un alto grado de flexibilidad en la forma en que se crea y se entrega contenido en el sitio web. Puede usar la creación de [AEM content management](/help/sites-cloud/authoring/author-publish.md) y [WYSIWYG con el editor universal, así como la creación basada en documentos](https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/edge-delivery/wysiwyg-authoring/authoring).

Puede editar contenido en:

* [Microsoft Word o Google Docs](#integrate-aem-assets-with-document-based-authoring-tools)
* [Editor universal](#integrate-aem-assets-with-UE-universal-editor)

Después de editar el contenido, puede publicarlo en Edge Delivery Services.

## Integración de AEM Assets con flujos de creación basados en documentos para Edge Delivery Services {#integrate-aem-assets-with-document-based-authoring-tools}

Cuando AEM Assets está integrado con las herramientas de creación basada en documentos, como Microsoft Word o Google Docs, proporciona un selector de recursos en el editor. Utilice este selector de recursos para acceder a los AEM Assets e insertar los recursos aprobados en el documento.
Si ya tiene un sitio web de Edge Delivery Services, consulte el documento [Complemento de AEM Assets](https://github.com/adobe-rnd/aem-assets-plugin/blob/main/README.md) para obtener información sobre cómo integrar AEM Assets con su proyecto de AEM existente.
Siga las siguientes secciones de [Requisitos previos](#integrate-aem-assets-with-microsoft-word-and-google-docs) y [Integración de AEM Assets con el entorno de creación basada en documentos](#integrate-aem-assets-with-microsoft-word-or-google-docs-to-use-aem-assets-with-microsoft-word-or-google-docs) si no tiene un sitio web de Edge Delivery Services para publicar los AEM Assets, incluido el contenido creado en las herramientas de creación basadas en documentos.

### Requisitos previos{#integrate-aem-assets-with-microsoft-word-and-google-docs}

Antes de empezar, asegúrese de que el entorno de creación basada en documentos está listo:

* Integre AEM con una herramienta de creación basada en documentos para configurar el entorno de creación. Consulte [Introducción - Tutorial para desarrolladores](https://www.aem.live/developer/tutorial) para obtener información sobre cómo configurar el entorno de creación.

### Integración de AEM Assets con el entorno de creación basada en documentos{#integrate-aem-assets-with-microsoft-word-or-google-docs-to-use-aem-assets-with-microsoft-word-or-google-docs}

Configure el complemento Sidekick de AEM Assets para que utilice recursos durante la creación de contenido en Microsoft Word o Google Docs.

* Consulte [Complemento Sidekick de Adobe Experience Manager Assets](https://www.aem.live/docs/aem-assets-sidekick-plugin#using-experience-manager-assets-for-website-authors) para obtener información sobre cómo acceder y utilizar AEM Assets en Microsoft Word o Google Docs.
* Consulte [Configuración del complemento Adobe Experience Manager Assets Sidekick](https://www.aem.live/developer/configuring-aem-assets-sidekick-plugin) para obtener más información sobre la configuración.
  ![usar dynamic media con capacidades openAPI en ms word y google docs](/help/assets/assets/my-assets-sidebar.png)

## Distribución de recursos mediante Dynamic Media con funciones de OpenAPI {#integrate-Dynamic-Media-with-OpenAPI-capabilities-with-Microsoft-Word-Google-Docs-and-universal-editor}

También puede utilizar recursos entregados mediante DM con funciones de OpenAPI. Proporciona muchos beneficios, como:

* Acceso solo a recursos aprobados por la marca (imágenes, vídeos, PDF y otros tipos de recursos) desde AEM Assets Cloud Services.
* Administración (referencias frente a copias del recurso), que ayuda a la propagación automática de eventos del ciclo vital de recursos como caducidad, eliminación y actualizaciones.
* Representaciones de imágenes dinámicas y recorte inteligente.
* Entrega y optimización de medios enriquecidos, como la transmisión de vídeo adaptable de forma predeterminada y la entrega de recursos originales para PDF.
* Informe de impresiones de nivel de recurso ([disponibilidad limitada](/help/assets/manage-reports-assets-view.md#dynamic-media-delivery-reports)).

Para obtener más información sobre las funcionalidades, consulte la documentación de [Dynamic Media con funciones OpenAPI](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/dynamicmedia/dynamic-media-open-apis/dynamic-media-open-apis-overview).

### Requisitos previos {#prerequisites-for-dm-with-openapi-capabilities-to-use-aem-assets}

Para utilizar la referencia de recursos, debe tener:

* Derecho a un entorno de Assets Cloud Service en el que Dynamic Media con capacidades de API abierta esté habilitado.
* Licencia de Dynamic Media.
* El complemento de la barra de tareas de los AEM Assets habilitado con la copia de referencia para los recursos de imagen habilitada. Para obtener más información, vea [this](https://www.aem.live/developer/configuring-aem-assets-sidekick-plugin#copymode) para la creación basada en documentos y [this](https://developer.adobe.com/uix/docs/extension-manager/extension-developed-by-adobe/configurable-asset-picker/#extension-overview) para la creación basada en el editor universal.
* Assets que se han aprobado. Los recursos aprobados han `dam:status=Approved` a través del servidor de Assets Cloud Services o de las acciones de la interfaz de usuario.

### Uso de recursos entregados mediante Dynamic Media con funciones de OpenAPI{#how-to-use-Dynamic-Media-with-OpenAPI-assets}

Seleccione los siguientes vínculos para aprender a utilizar Dynamic Media con las funciones de OpenAPI para ofrecer imágenes, vídeos y otros tipos de recursos en el contenido:

* [Agregar imágenes al contenido](https://www.aem.live/docs/aem-assets-sidekick-plugin#using-image-references-when-authoring-content)
* [Agregar vídeos a su contenido](https://www.aem.live/docs/aem-assets-sidekick-plugin#using-video-references-when-authoring-content)
* [Agregue recursos que no sean de imagen o vídeo, como PDF, archivos zip y más, al contenido](https://www.aem.live/docs/aem-assets-sidekick-plugin#using-asset-references-for-pdf-zip-etc-when-authoring-content)

Consulte este vídeo para aprender a distribuir recursos en el contenido mediante Dynamic Media con las funciones de OpenAPI.

>[!VIDEO](https://video.tv.adobe.com/v/3441155)

## Sitio de Edge Delivery Services de muestra{#example-of-an-Edge-Delivery-Services-site}

Consulte [WKND Travel](http://bit.ly/3DExLnf), un sitio que se ha creado con las capacidades de creación basada en documentos de Edge Delivery Services. El contenido del sitio se creó en [Google Docs](https://drive.google.com/drive/folders/1HCCHRWp4HJIXW_cUv5cRDQ5DzzqiZsXT) y Dynamic Media con capacidades OpenAPI se usa para entregar recursos en el contenido. Después de la creación, el contenido se publica directamente desde el documento. Explore este [repositorio Git](https://github.com/hlxsites/franklin-assets-selector/tree/aem-dynamicmedia-demo/blocks) para conocer todos los archivos, carpetas, configuraciones, estilos del sitio web y códigos de funcionalidad esenciales que se usan para crear la configuración de creación basada en documentos para este sitio de Edge Delivery Services (EDS).

## Integración de AEM Assets con flujos de creación basados en Universal Editor para Edge Delivery Services {#integrate-aem-assets-with-UE-universal-editor}

Configure el editor universal para que se integre con los AEM Assets. Esta integración le permite utilizar Dynamic Media con las funciones de OpenAPI para entregar recursos.

* Consulte [Configuración en el sitio de Edge Delivery](https://developer.adobe.com/uix/docs/extension-manager/extension-developed-by-adobe/configurable-asset-picker/#configuration-in-edge-delivery-site) para obtener información sobre cómo agregar una función de selector de recursos personalizada en el editor universal. El selector de recursos personalizado permite insertar recursos directamente en el contenido del editor universal.
* Consulte [Descripción general de la extensión](https://developer.adobe.com/uix/docs/extension-manager/extension-developed-by-adobe/configurable-asset-picker/#extension-overview) para obtener información sobre cómo acceder a los AEM Assets e insertar los recursos durante la creación en el editor universal.
