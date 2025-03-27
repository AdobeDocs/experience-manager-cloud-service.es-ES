---
title: Integrar [!DNL AEM Assets] al crear contenido para [!DNL Edge Delivery Services]
description: Aprenda a integrar [!DNL AEM Assets] con [!DNL Edge Delivery Services]. This integration enables you to integrate [!DNL AEM Assets] con [!DNL Microsoft Word] y [!DNL Google Docs], integrate [!DNL AEM Assets] con [!DNL Universal Editor], integrate [!DNL Dynamic Media] con [!DNL Edge Delivery Services], integrate [!DNL Dynamic Media with OpenAPI capabilities] con [!DNL Universal Editor] e integrar [!DNL Dynamic Media with OpenAPI capabilities] con [!DNL Microsoft Word] y [!DNL Google Docs].
exl-id: e58db2ce-a55a-49b3-ae8e-709b5ea8d095
source-git-commit: 84fde065602d8303a03eb2c82bfa4c4bef0c1193
workflow-type: tm+mt
source-wordcount: '671'
ht-degree: 6%

---

# Integrar [!DNL AEM Assets] al crear contenido para [!DNL Edge Delivery Services] {#integrate-aem-assets-with-edge-delivery-services}

<table>
    <tr>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nuevo</i></sup> <a href="/help/assets/dynamic-media/dm-prime-ultimate.md"><b>Dynamic Media Prime y Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nuevo</i></sup> <a href="/help/assets/assets-ultimate-overview.md"><b>AEM Assets Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>New</i></sup> <a href="/help/assets/aem-assets-view-ui-extensibility.md"><b>Extensibilidad de la IU</b></a>
        </td>
          <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nuevo</i></sup> <a href="/help/assets/dynamic-media/enable-dynamic-media-prime-and-ultimate.md"><b>Habilitar Dynamic Media Prime y Ultimate</b></a>
        </td>
         <td>
            <a href="/help/assets/search-best-practices.md"><b>Prácticas recomendadas de búsqueda</b></a>
        </td>
    </tr>
    <tr>
        <td>
            <a href="/help/assets/metadata-best-practices.md"><b>Prácticas recomendadas de metadatos</b></a>
        </td>
        <td>
            <a href="/help/assets/product-overview.md"><b>Centro de contenido</b></a>
        </td>
        <td>
            <a href="/help/assets/dynamic-media-open-apis-overview.md"><b>Dynamic Media con funciones de OpenAPI</b></a>
        </td>
        <td>
            <a href="https://developer.adobe.com/experience-cloud/experience-manager-apis/"><b>Documentación de desarrollador de AEM Assets</b></a>
        </td>
    </tr>
</table>

![Integración de recursos de AEM con el editor universal](/help/assets/assets/EDS2.png)

[[!DNL Edge Delivery Services]](https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/edge-delivery/overview) es un conjunto de servicios que se pueden componer y que permite un alto grado de flexibilidad en la forma en que se crea y se entrega contenido en el sitio web. Puede usar la [administración de contenido de AEM](/help/sites-cloud/authoring/author-publish.md) y la [creación de WYSIWYG mediante [!DNL Universal Editor] así como la creación basada en documentos](https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/edge-delivery/wysiwyg-authoring/authoring).

Puede editar contenido en:

* [[!DNL Microsoft Word] o  [!DNL Google Docs]](#integrate-dynamic-media-with-edge-delivery-services)
* [[!DNL Universal Editor]](#integrate-aem-assets-with-universal-editor-UE)

Después de editar el contenido, puede publicarlo en Edge Delivery Services.

## Integrando [!DNL AEM Assets] con flujos de creación basados en documentos para [!DNL Edge Delivery Services] {#integrate-dynamic-media-with-edge-delivery-services}

Cuando [!DNL AEM Assets] se integra con las herramientas de creación basadas en documentos, como [!DNL Microsoft Word] o [!DNL Google Docs], proporciona un selector de recursos en la herramienta de creación. Use este selector de recursos para acceder a [!DNL AEM Assets] e insertar recursos aprobados en el contenido.
Si ya tiene un sitio web de [!DNL Edge Delivery Services], consulte la documentación de [[!DNL AEM Assets] plugin](https://github.com/adobe-rnd/aem-assets-plugin/blob/main/README.md) para obtener información sobre cómo integrar [!DNL AEM Assets] con su proyecto de [!DNL AEM] existente.
Siga las siguientes secciones de [Requisitos previos](#integrate-aem-assets-with-microsoft-word-and-google-docs) e [Integración [!DNL AEM Assets] con el entorno de creación basada en documentos](#integrate-aem-assets-with-microsoft-word-or-google-docs-to-use-aem-assets-with-microsoft-word-or-google-docs) si no tiene un sitio web de [!DNL Edge Delivery Services] para publicar el contenido inclusivo de [!DNL AEM Assets] creado en las herramientas de creación basadas en documentos.

### Requisitos previos{#integrate-aem-assets-with-microsoft-word-and-google-docs}

Antes de empezar, asegúrese de que el entorno de creación basada en documentos está listo:

* Integrar [!DNL AEM] con una herramienta de creación basada en documentos para configurar el entorno de creación. Consulte [Introducción - Tutorial para desarrolladores](https://www.aem.live/developer/tutorial) para obtener información sobre cómo configurar el entorno de creación.

### Integrando [!DNL AEM Assets] con el entorno de creación basada en documentos{#integrate-aem-assets-with-microsoft-word-or-google-docs-to-use-aem-assets-with-microsoft-word-or-google-docs}

Configure el complemento de Sidekick [!DNL AEM Assets] para que utilice recursos durante la creación de contenido en [!DNL Microsoft Word] o [!DNL Google Docs].

* Consulte [[!DNL Adobe Experience Manager Assets Sidekick Plugin]](https://www.aem.live/docs/aem-assets-sidekick-plugin#using-experience-manager-assets-for-website-authors) para obtener información sobre cómo acceder y utilizar AEM Assets en Microsoft Word o Google Docs.
* Consulte [Configurar [!DNL Adobe Experience Manager Assets Sidekick Plugin]](https://www.aem.live/developer/configuring-aem-assets-sidekick-plugin) para obtener detalles de configuración.
  ![usar dynamic media con capacidades openAPI en ms word y google docs](/help/assets/assets/my-assets-sidebar.png)

## Enviar recursos mediante [!DNL Dynamic Media with OpenAPI capabilities] {#integrate-Dynamic-Media-with-OpenAPI-capabilities-with-Microsoft-Word-Google-Docs-and-universal-editor}

También puede utilizar los recursos entregados mediante [!DNL Dynamic Media with OpenAPI capabilities]. Proporciona muchos beneficios, como:

* Acceso solo a recursos aprobados por la marca (imágenes, vídeos, PDF y otros tipos de recursos) de [!DNL AEM Assets Cloud Services].
* Administración (referencias frente a copias del recurso), que ayuda a la propagación automática de eventos del ciclo vital de recursos como caducidad, eliminación y actualizaciones.
* Representaciones de imágenes dinámicas y recorte inteligente.
* Entrega y optimización de medios enriquecidos, como la transmisión de vídeo adaptable de forma predeterminada y la entrega de recursos originales para PDF.
* Informe de impresiones de nivel de recurso ([disponibilidad limitada](/help/assets/manage-reports-assets-view.md#dynamic-media-delivery-reports)).

Para obtener más información sobre las capacidades, consulte la documentación de [[!DNL Dynamic Media with OpenAPI capabilities]](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/dynamicmedia/dynamic-media-open-apis/dynamic-media-open-apis-overview).

### Requisitos previos {#dynamic-media-with-universal-editor-and-edge-delivery-services}

Para utilizar la referencia de recursos, debe tener:

* Derecho a un entorno Assets Cloud Service donde [!DNL Dynamic Media with Open API capabilities] está habilitado.
* Una licencia de [!DNL Dynamic Media].
* Se habilitó [!DNL AEM Assets sidekick plugin] con la referencia de copia para los recursos de imagen. Para obtener más información, consulte [esta documentación](https://www.aem.live/developer/configuring-aem-assets-sidekick-plugin#copymode) para la creación basada en documentos y [esta documentación](https://developer.adobe.com/uix/docs/extension-manager/extension-developed-by-adobe/configurable-asset-picker/#extension-overview) para la creación basada en el editor universal.
* Assets que se han aprobado. Los recursos aprobados han `dam:status=Approved` a través del servidor de Assets Cloud Services o de las acciones de la interfaz de usuario.

### Usar recursos entregados mediante [!DNL Dynamic Media with OpenAPI capabilities]{#Using-Dynamic-Media-with-edge-delivery-services}

Seleccione los siguientes vínculos para aprender a utilizar [!DNL Dynamic Media with OpenAPI capabilities] para entregar imágenes, vídeos y otros tipos de recursos en el contenido:

* [Agregar imágenes al contenido](https://www.aem.live/docs/aem-assets-sidekick-plugin#using-image-references-when-authoring-content)
* [Agregar vídeos a su contenido](https://www.aem.live/docs/aem-assets-sidekick-plugin#using-video-references-when-authoring-content)
* [Agregue recursos que no sean de imagen o vídeo, como PDF, archivos zip y más, al contenido](https://www.aem.live/docs/aem-assets-sidekick-plugin#using-asset-references-for-pdf-zip-etc-when-authoring-content)

Consulte este vídeo para aprender a distribuir recursos en el contenido mediante Dynamic Media con las funciones de OpenAPI.

>[!VIDEO](https://video.tv.adobe.com/v/3441155)

## Sitio de muestra [!DNL Edge Delivery Services]{#dynamic-media-with-google-docs-and-ms-word}

Vea [WKND Travel](http://bit.ly/3DExLnf), un sitio que se creó con las capacidades de creación basada en documentos de [!DNL Edge Delivery Services]. El contenido del sitio se creó en [Google Docs](https://drive.google.com/drive/folders/1HCCHRWp4HJIXW_cUv5cRDQ5DzzqiZsXT) y [!DNL Dynamic Media with OpenAPI capabilities] se usa para entregar recursos en el contenido. Después de la creación, el contenido se publica directamente desde el documento. Explore este [repositorio Git](https://github.com/hlxsites/franklin-assets-selector/tree/aem-dynamicmedia-demo/blocks) para conocer todos los archivos, carpetas, configuraciones, estilos del sitio web y códigos de funcionalidad esenciales que se usan para crear la configuración de creación basada en documentos para este sitio [!DNL Edge Delivery Services (EDS)].

## Integrando [!DNL AEM Assets] con [!DNL Universal Editor] flujos de creación basados para [!DNL Edge Delivery Services] {#integrate-aem-assets-with-universal-editor-UE}

Configure [!DNL Universal Editor] para que se integre con [!DNL AEM Assets]. Esta integración le permite usar [!DNL Dynamic Media with OpenAPI capabilities] para entregar recursos.

* Consulte [Configuración en [!DNL Edge Delivery] Sitio](https://developer.adobe.com/uix/docs/extension-manager/extension-developed-by-adobe/configurable-asset-picker/#configuration-in-edge-delivery-site) para obtener información sobre cómo agregar una función de selector de recursos personalizada en [!DNL Universal Editor]. El selector de recursos personalizado le permite insertar recursos directamente en el contenido de [!DNL Universal Editor].
* Consulte [Descripción general de la extensión](https://developer.adobe.com/uix/docs/extension-manager/extension-developed-by-adobe/configurable-asset-picker/#extension-overview) para obtener información sobre cómo acceder a [!DNL AEM Assets] e insertar los recursos durante la creación en [!DNL Universal Editor].
