---
title: Administración de recursos con licencia en Content Hub
description: Obtenga información sobre cómo agregar un campo de licencia al formulario de metadatos del recurso, aplicar la propiedad Metadatos de licencia a las carpetas de recursos y aprobar recursos con licencias para su uso.
badgeSaas: label="AEM Assets" type="Positive" tooltip="(Se aplica a los AEM Assets)."
exl-id: ac3aad9f-c7b3-47a7-9314-a2f8277f0d3e
source-git-commit: 59f97fc6ded4274c27400f56b50b4a3329cc471a
workflow-type: tm+mt
source-wordcount: '639'
ht-degree: 3%

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

## Preguntas frecuentes {#faqs-manage-licensed-assets-content-hub}

### ¿Cuál es el propósito de administrar los recursos con licencia en AEM Assets Content Hub?

La administración de recursos con licencia en AEM Assets Content Hub permite a los administradores asegurarse de que solo los recursos aprobados con licencias válidas estén disponibles para su uso, y mantener la conformidad y el seguimiento adecuado de los metadatos en el entorno de creación de AEM.

### ¿Cómo puedo añadir un campo de licencia a las propiedades de los recursos en Experience Manager as a Cloud Service?

En la vista AEM Assets, puede agregar un campo de licencia a las propiedades del recurso editando el formulario de metadatos para incluir un nuevo campo de texto asignado a la propiedad `dc:license`. A continuación, este campo aparece en las propiedades del recurso en el entorno de creación de AEM Assets.

### ¿Cómo se aplica un formulario de metadatos a una carpeta de recursos para incluir el campo de licencia en las propiedades de los recursos en los AEM Assets?

En la vista AEM Assets, edite el formulario de metadatos para incluir el campo de licencia. Aplique este formulario de metadatos a la carpeta de recursos deseada para asegurarse de que la nueva configuración se incorpora a todos los recursos de esa carpeta.

### ¿Cómo especifico los detalles de licencia de un recurso en la vista de AEM Assets?

Para especificar los detalles de la licencia, seleccione el recurso, haga clic en **Detalles** para ver sus propiedades e introduzca la ruta absoluta de la licencia del recurso aprobado en el campo de licencia agregado al formulario de metadatos.

### ¿Cuál es el formato requerido para la ruta absoluta de Content Hub de AEM Assets para una licencia de recursos?

La ruta absoluta de Content Hub debe seguir el patrón: /content/dam/(La jerarquía de carpetas del recurso dentro del repositorio DAM)/(asset_name).(file_extension). Por ejemplo, `/content/dam/teamA/projects/documents/file1.pdf`.

### ¿Por qué es importante aprobar el recurso y su licencia para que estén disponibles en AEM Assets Content Hub?

La aprobación tanto del recurso como de su licencia garantiza que solo los recursos con licencia y autorizados correctamente estén disponibles en AEM Assets Content Hub, lo que ayuda a mantener la conformidad y los derechos de uso adecuados.

### ¿Cómo puedo hacer que un recurso esté disponible en AEM Assets Content Hub después de aprobar su licencia?

Después de definir la ruta de licencia en las propiedades del recurso, apruebe el recurso y haga clic en Guardar. Esta acción hace que el recurso con licencia esté disponible en AEM Assets Content Hub.

### ¿Quién es el responsable de la administración de los recursos con licencia en AEM Assets Content Hub?

Los administradores son responsables de editar formularios de metadatos, asignarlos a carpetas de recursos y aprobar tanto los recursos como sus licencias en AEM Assets Content Hub.
