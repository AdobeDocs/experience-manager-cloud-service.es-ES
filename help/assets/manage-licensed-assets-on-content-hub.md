---
title: Administración de recursos con licencia en Content Hub
description: Obtenga información sobre cómo agregar un campo de licencia al formulario de metadatos del recurso, aplicar la propiedad Metadatos de licencia a las carpetas de recursos y aprobar recursos con licencias para su uso.
exl-id: ac3aad9f-c7b3-47a7-9314-a2f8277f0d3e
source-git-commit: 32fdbf9b4151c949b307d8bd587ade163682b2e5
workflow-type: tm+mt
source-wordcount: '251'
ht-degree: 6%

---

# Administración de recursos con licencia en Content Hub {#manage-licensed-assets-on-content-hub}

Como administrador, edite el formulario de metadatos para incluir el campo de licencia de recursos y que se muestre en las propiedades del recurso en el entorno de creación de AEM. A continuación, puede aprobar el recurso y su licencia para que el recurso tenga licencia y esté disponible en Content Hub.

Ejecute los siguientes pasos:

1. Edite el formulario de metadatos para incluir un nuevo campo de texto que incluya los detalles de la licencia. Asigne el campo de texto a la propiedad `dc:license`. Para obtener más información sobre cómo agregar campos a un formulario de metadatos y definir propiedades, consulte [Configuración de Forms de metadatos](/help/assets/metadata-assets-view.md#metadata-forms).
   ![extracción zip](/help/assets/assets/metadata-form-edit.png)
1. Aplique el formulario de metadatos a la carpeta de recursos para aplicar la configuración incorporada en el paso 1. Para obtener información sobre cómo asignar un formulario de metadatos a la carpeta de recursos, consulte [Asignar formulario de metadatos a una carpeta](/help/assets/metadata-assets-view.md#metadata-forms).
1. [Aprobar el PDF con licencia](/help/assets/manage-organize-assets-view.md#set-asset-status)
1. Seleccione el recurso y haga clic en **Detalles** para ver sus propiedades. En el campo de licencia añadido en el paso 1, defina la ruta absoluta para la licencia de recurso que se ha aprobado en el paso 3 o que ya se ha aprobado anteriormente. La ruta absoluta de Content Hub sigue este patrón estándar: `/content/dam/(The asset's folder hierarchy within the DAM repository)/(asset_name).(file_extension)`. Por ejemplo, /content/dam/teamA/projects/documents/file1.pdf
   ![ruta absoluta](/help/assets/assets/absolute-path.png)
1. Apruebe el recurso para que esté disponible en Content Hub y haga clic en **Guardar**. Para obtener información sobre cómo aprobar un recurso, consulte [Establecer el estado del recurso](/help/assets/manage-organize-assets-view.md#set-asset-status).
