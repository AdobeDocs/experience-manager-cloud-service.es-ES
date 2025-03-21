---
title: Edición masiva de metadatos en la vista de recursos
description: Descubra cómo puede actualizar un conjunto predefinido de campos de metadatos estándar para varios recursos disponibles simultáneamente en la vista de Assets.
exl-id: f5fee1b3-2855-4010-ae4a-216beb20920d
source-git-commit: 188f60887a1904fbe4c69f644f6751ca7c9f1cc3
workflow-type: tm+mt
source-wordcount: '503'
ht-degree: 5%

---

# Edición masiva de metadatos en la vista de recursos{#how-to-edit-the-metadata-of-multiple-assets-simultaneously}

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

La característica **Edición masiva de metadatos** de la vista de Assets permite a los usuarios editar simultáneamente un conjunto predefinido de campos de metadatos estándar para varios archivos de recursos. Seleccione varios recursos y actualice de forma masiva su conjunto predefinido de metadatos estándar a la vez, en lugar de actualizar dichos metadatos estándar para cada recurso de forma individual. Esta función mejora la eficacia, coherencia y precisión de las propiedades de metadatos estándar en un gran conjunto de recursos, lo que mejora la capacidad de búsqueda y organización de estos.

## Edición masiva de metadatos de recursos {#how-to-bulk-edit-the-metadata-of-multiple-assets-on-assets-view}

Ejecute estos pasos para editar masivamente los metadatos de varios recursos a la vez:

1. En la vista Assets, haga clic en **Assets**.
1. Busque recursos específicos o búsquelos mediante palabras clave en la barra de búsqueda.
1. Seleccione los recursos y haga clic en **Edición masiva de metadatos** en el menú superior.
   ![editar metadatos en lote](/help/assets/assets/bulk-metadata-edit1.png)
1. En la página Editar metadatos, edite los siguientes campos en el panel **Propiedades**:
   * **Estado:** Seleccione un estado para los recursos seleccionados.
   * **Fecha de caducidad:** establezca una fecha a partir de la cual los recursos dejarán de ser válidos o necesarios.
   * **Autor:** Especifique el nombre del autor.
   * **Palabras clave:** Agregue términos específicos o cadenas de texto que proporcionen información de alto nivel sobre los recursos para mejorar su capacidad de detección. Añada una palabra clave y pulse Intro o volver para añadir otra palabra clave a la lista.
   * **Etiquetas:** Haga clic en ![icono de etiquetas](/help/assets/assets/tags-icon.svg) para seleccionar etiquetas de entre las opciones disponibles. Las etiquetas proporcionan información más específica sobre los recursos y mejoran su capacidad de detección. Las etiquetas ya aplicadas a los recursos seleccionados se muestran en el panel **Propiedades**. Si no encuentra las etiquetas relevantes, créelas y asígnelas a los recursos seleccionados. Consulte [Administrar etiquetas en la vista de Assets](/help/assets/tagging-management-assets-view.md) para obtener más información sobre cómo crear y asignar etiquetas a los recursos.
   * Haga clic en **Guardar** para aplicar las actualizaciones de metadatos anteriores a los recursos seleccionados. Una vez guardadas, las palabras clave y las etiquetas se anexan, mientras que los detalles actualizados de Estado, Fecha de caducidad y Autor anulan los detalles existentes.
     ![save-bulk-metadata-edit-properties](/help/assets/assets/save-bulk-metadata-edit-properties2.png)

     >[!NOTE]
     >
     >Puede editar los metadatos de 100 recursos a la vez.

Para ver las actualizaciones de metadatos aplicadas a un recurso, vaya a la página de detalles del recurso (seleccione el recurso y haga clic en **Detalles**) y haga clic en ![](/help/assets/assets/info-icon-solid-black.svg) para ver los metadatos del recurso en el panel **Información**.

>[!NOTE]
>
>**Estado**, **Fecha de caducidad**, **Autor**, **Palabras clave** y **Etiquetas** son propiedades de metadatos estándar disponibles para la edición masiva de metadatos, independientemente de los metadatos específicos de la carpeta. Estas propiedades de metadatos se muestran en la página de detalles del recurso solo si se incluyen en el formulario de metadatos aplicado a la carpeta del recurso. Si no encuentra estas propiedades de metadatos estándar en la página de detalles del recurso, edite el formulario de metadatos de la carpeta de recursos para incluirlas. Consulte [Metadatos en la vista de Assets](/help/assets/metadata-assets-view.md) para obtener información sobre cómo crear o editar un formulario de metadatos y aplicarlo a una carpeta.
