---
title: Edición masiva de metadatos en la vista de Assets
description: Descubra cómo puede editar simultáneamente los metadatos de varios recursos disponibles en la vista de Assets.
source-git-commit: 5778d0dac141174c1b950625057f920af0301a8b
workflow-type: tm+mt
source-wordcount: '362'
ht-degree: 0%

---

# Edición masiva de metadatos en la vista de Assets{#how-to-edit-the-metadata-of-multiple-assets-simultaneously}

Con **Edición masiva de metadatos** en la interfaz de usuario de la vista de Assets, puede modificar los metadatos de varios archivos de recursos simultáneamente. En lugar de editar los metadatos de cada recurso individualmente, puede aplicar cambios a un grupo grande de recursos a la vez. Esta función mejora la eficacia, coherencia y precisión de las propiedades de metadatos en un gran conjunto de recursos, lo que mejora la capacidad de búsqueda y organización de estos.

## Edición masiva de metadatos de recursos {#how-to-bulk-edit-the-metadata-of-multiple-assets-on-assets-view}

Ejecute estos pasos para editar masivamente los metadatos de varios recursos a la vez:

1. En la vista Assets, haga clic en **Assets**.
1. Examine los recursos o introduzca palabras clave relevantes en la barra de búsqueda para localizar recursos específicos.
1. Seleccione varios recursos y haga clic en **Edición masiva de metadatos** en el menú superior.
   ![editar metadatos en lote](/help/assets/assets/bulk-metadata-edit.png)
1. En la página Editar metadatos, edite los siguientes campos en el panel **Propiedades**:
   * **Estado:** seleccione un estado para definir la facilidad de uso de los recursos seleccionados.
   * **Fecha de caducidad:** establezca una fecha a partir de la cual los recursos dejarán de ser válidos o necesarios.
   * **Autor:** Especifique el nombre del autor.
   * **Palabras clave:** Agregue términos o cadenas de texto que proporcionen información de alto nivel sobre los recursos para mejorar su capacidad de detección. Añada una palabra clave y pulse Intro o volver para añadir otra palabra clave a la lista.
     <!-- * **Tags:** Click ![tags icon](/help/assets/assets/tags-icon.svg) to select tags from the available options. Tags provide more specific information about the assets and enhances their discoverability. Tags already applied to the selected assets are only displayed in the **Properties** panel. If you cannot find the relevant tags, create the tags and assign them to the selected assets. See [Manage tags in Assets view](/help/assets/tagging-management-assets-view.md) for details.-->
   * Haga clic en **Guardar** para anexar palabras clave y <!-- Tags while--> anular los detalles existentes de Estado, Fecha de caducidad y Autor.
     ![save-bulk-metadata-edit-properties](/help/assets/assets/save-bulk-metadata-edit-properties1.png)

     >[!NOTE]
     >
     >Puede editar los metadatos de 100 recursos a la vez.

Para ver los cambios de metadatos aplicados a un recurso, vaya a la página de detalles del recurso (seleccione el recurso y haga clic en **Detalles**) y haga clic en ![](/help/assets/assets/info-icon-solid-black.svg) para ver los metadatos del recurso en el panel **Información**.

>[!NOTE]
>
>Estado, Fecha de caducidad, Autor y Palabras clave <!-- and Tags--> son propiedades de metadatos estándar disponibles para la edición masiva de metadatos, independientemente de los metadatos específicos de la carpeta. Estas propiedades de metadatos se muestran en la página de detalles del recurso solo si se incluyen en el formulario de metadatos aplicado a la carpeta del recurso.  Si no puede ver estas propiedades de metadatos en la página de detalles del recurso, edite el formulario de metadatos de la carpeta de recursos para incluirlas. Consulte [Metadatos en la vista de Assets](/help/assets/metadata-assets-view.md) para obtener información sobre cómo crear o editar un formulario de metadatos y aplicarlo a una carpeta.


