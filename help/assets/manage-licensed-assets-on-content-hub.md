---
title: Administración de recursos con licencia en Content Hub
description: Obtenga información sobre cómo agregar un campo de licencia al formulario de metadatos del recurso, aplicar la propiedad Metadatos de licencia a las carpetas de recursos y aprobar recursos con licencias para su uso.
exl-id: ac3aad9f-c7b3-47a7-9314-a2f8277f0d3e
source-git-commit: 188f60887a1904fbe4c69f644f6751ca7c9f1cc3
workflow-type: tm+mt
source-wordcount: '325'
ht-degree: 19%

---

# Administración de recursos con licencia en Content Hub {#manage-licensed-assets-on-content-hub}

<table>
    <tr>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nuevo</i></sup> <a href="/help/assets/dynamic-media/dm-prime-ultimate.md"><b>Dynamic Media Prime y Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nuevo</i></sup> <a href="/help/assets/assets-ultimate-overview.md"><b>AEM Assets Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nueva</i></sup> integración de <a href="/help/assets/integrate-aem-assets-edge-delivery-services.md"><b>AEM Assets con Edge Delivery Services</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nueva</i></sup> <a href="/help/assets/aem-assets-view-ui-extensibility.md"><b>extensibilidad de la interfaz de usuario</b></a>
        </td>
          <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nuevo</i></sup> <a href="/help/assets/dynamic-media/enable-dynamic-media-prime-and-ultimate.md"><b>Habilitar Dynamic Media Prime y Ultimate</b></a>
        </td>
    </tr>
    <tr>
        <td>
            <a href="/help/assets/search-best-practices.md"><b>Prácticas recomendadas de búsqueda</b></a>
        </td>
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

>[!AVAILABILITY]
>
>La guía del centro de contenido ya está disponible en formato de PDF. Descargue la guía completa y utilice el Asistente de IA de Adobe Acrobat para responder sus consultas.
>
>[!BADGE Guía del centro de contenido en PDF]{type=Informative url="https://helpx.adobe.com/content/dam/help/en/experience-manager/aem-assets/content-hub.pdf"}

Como administrador, edite el formulario de metadatos para incluir el campo de licencia de recursos y que se muestre en las propiedades del recurso en el entorno de creación de AEM. A continuación, puede aprobar el recurso y su licencia para que el recurso tenga licencia y esté disponible en Content Hub.

Ejecute los siguientes pasos:

1. Edite el formulario de metadatos para incluir un nuevo campo de texto que incluya los detalles de la licencia. Asigne el campo de texto a la propiedad `dc:license`. Para obtener más información sobre cómo agregar campos a un formulario de metadatos y definir propiedades, consulte [Configuración de Forms de metadatos](/help/assets/metadata-assets-view.md#metadata-forms).
   ![extracción zip](/help/assets/assets/metadata-form-edit.png)
1. Aplique el formulario de metadatos a la carpeta de recursos para aplicar la configuración incorporada en el paso 1. Para obtener información sobre cómo asignar un formulario de metadatos a la carpeta de recursos, consulte [Asignar formulario de metadatos a una carpeta](/help/assets/metadata-assets-view.md#metadata-forms).
1. [Aprobar el PDF con licencia](/help/assets/manage-organize-assets-view.md#set-asset-status)
1. Seleccione el recurso y haga clic en **Detalles** para ver sus propiedades. En el campo de licencia añadido en el paso 1, defina la ruta absoluta para la licencia de recurso que se ha aprobado en el paso 3 o que ya se ha aprobado anteriormente. La ruta absoluta de Content Hub sigue este patrón estándar: `/content/dam/(The asset's folder hierarchy within the DAM repository)/(asset_name).(file_extension)`. Por ejemplo, /content/dam/teamA/projects/documents/file1.pdf
   ![ruta absoluta](/help/assets/assets/absolute-path.png)
1. Apruebe el recurso para que esté disponible en Content Hub y haga clic en **Guardar**. Para obtener información sobre cómo aprobar un recurso, consulte [Establecer el estado del recurso](/help/assets/manage-organize-assets-view.md#set-asset-status).
