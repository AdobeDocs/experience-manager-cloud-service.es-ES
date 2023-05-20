---
title: Administrar los documentos de PDF en [!DNL Adobe Experience Manager].
description: Administración de documentos de PDF en [!DNL Adobe Experience Manager] as a [!DNL Cloud Service].
feature: Asset Management
role: User,Admin
exl-id: 29660869-6902-4093-845b-cd629be59d4d
source-git-commit: 8bdd89f0be5fe7c9d4f6ba891d7d108286f823bb
workflow-type: tm+mt
source-wordcount: '824'
ht-degree: 3%

---

# Administración de documentos de PDF en Experience Manager Assets as a Cloud Service {#add-assets-to-experience-manager}

Experience Manager Assets se integra perfectamente con el Visor de PDF de Document Cloud, lo que le permite previsualizar varias páginas de un documento de PDF. Además, también puede utilizar funciones avanzadas del visualizador de PDF de Document Cloud como anotaciones, buscar texto, navegar por el documento de PDF mediante marcadores y miniaturas, etc., en el mismo entorno. Experience Manager Assets también le permite cargar documentos en otros formatos compatibles y previsualizarlos en formato de PDF.

El visualizador de PDF de Document Cloud beneficia a AEM Assets de las siguientes maneras:
* [Compatibilidad con los componentes del visor del Document Cloud PDF](#pdf-doc-cloud)
* [Compatibilidad con la vista previa de varias páginas y anotaciones para el recurso de PDF](#multi-page)
* [Compatibilidad con la vista previa de varias páginas para documentos en otros formatos](#multi-format)

> Sugerencia
> Si no puede obtener una vista previa de varias páginas de un documento de PDF cargado anteriormente, seleccione el PDF y haga clic en **![Reprocesar](/help/assets/assets/Reprocess.svg) Volver a procesar recursos**.

## Compatibilidad con los componentes del visor del Document Cloud PDF {#pdf-doc-cloud}

El visualizador nativo de PDF de Doc Cloud tiene los siguientes componentes en AEM Assets:

* **Visor de PDF con miniaturas de página** La vista de miniaturas es una pequeña previsualización de las páginas de un documento de PDF. Con las miniaturas, puede saltar directamente a la página deseada. Puede acceder a las miniaturas del documento de PDF seleccionado mediante ![miniatura](/help/assets/assets/thumbnail.svg) en el panel izquierdo.

* **Visor de PDF con marcadores** Marcador es un vínculo directo que le lleva al contenido del documento. Puede acceder a los marcadores del documento de PDF seleccionado mediante ![marcador](/help/assets/assets/bookmark.svg) en el panel izquierdo.

* **Buscar en PDF** Puede utilizar la búsqueda ![búsqueda](/help/assets/assets/Search.svg) para buscar el texto en el documento de PDF.

* **Re Pág/Av Pág** Utilizar Re Pág ![Re Pág](/help/assets/assets/ArrowUp.svg) o Av Pág ![Página anterior](/help/assets/assets/ArrowDown.svg) para desplazarse por el documento.

* **Alejar/Acercar** Utilizar alejar ![Alejar](/help/assets/assets/ZoomOut.svg) o acercar ![Acercar](/help/assets/assets/ZoomIn.svg) para rayar el documento.

* **Ajuste de página** Utilice las dimensiones de anchura o altura para ajustar el documento según el tamaño de pantalla.

* **PDF de acoplamiento/desacoplamiento** Puede acoplar o desacoplar los componentes del visor de PDF nativo con esta opción.

## Compatibilidad con la vista previa de varias páginas y anotaciones para el recurso de PDF {#multi-page}

Adobe Experience Manager Assets permite obtener una vista previa del documento del PDF que consta de varias páginas. Para obtener una vista previa de varias páginas de un documento de PDF, siga estos pasos:

1. Siga los pasos para [AEM carga de recursos en la](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/add-assets.html?lang=en).
1. Examine el documento del PDF que desea cargar y previsualizar.
1. Abra el documento.
1. El visualizador de documentos de PDF se carga de forma predeterminada. También puede seleccionar Representación del PDF en el panel Representación.
1. En la lista desplegable Representaciones, seleccione **Todas las representaciones**.

También puede solicitar [anotaciones](#pdf-annotations) al documento de PDF en una vista previa de varias páginas.

> NOTA
> El tamaño máximo de un recurso que puede previsualizar es de hasta 100 MB.

>[!VIDEO](https://video.tv.adobe.com/v/3409355)

<!--
![Multi-page Preview](/help/assets/assets/multi-page.png)
-->

**Anotaciones de PDF{#pdf-annotations}**

Experience Manager Assets permite agregar comentarios a un documento de PDF. Un documento de PDF puede tener varias anotaciones.

Para anotar un documento de PDF, realice los siguientes pasos:
1. Vaya a la interfaz de Assets y desplácese hasta el documento de PDF que desee anotar. El visor de PDF nativo se abre a la derecha y muestra una vista previa del documento de PDF seleccionado.
1. Clic **Anotar** en el menú superior.
A continuación, se muestran las anotaciones que se pueden aplicar en un documento de PDF:

<table>
        <tr>
             <th> Anotación </th>
            <th> Descripción </th>
        </tr>
        <tr>
           <td> <img src="/help/assets/assets/Comment.svg"> Comentar </td>
            <td> Seleccione Comentario para expresar una observación. </td>
        </tr>
        <tr>
            <td> <img src="/help/assets/assets/Text.svg"> Textbox </td>
            <td> Seleccione Cuadro de texto para introducir el texto. </td>
        </tr>
        <tr>
            <td> <img src="/help/assets/assets/Note.svg"> Notas rápidas </td>
            <td> Añada un pequeño texto o recordatorio que pueda añadir a un área concreta del PDF. </td>
        </tr>
        <tr>
            <td> <img src="/help/assets/assets/Comment.svg"> Marcador de texto </td>
            <td> Seleccione el texto que desea resaltar en diferentes colores. </td>
        </tr>
        <tr>
            <td> <img src="/help/assets/assets/TextUnderline.svg"> Subrayado de texto </td>
            <td> Seleccione el texto que desee subrayar. </td>
        </tr>
        <tr>
            <td> <img src="/help/assets/assets/TextStrikethrough.svg"> Tachado </td>
            <td> Seleccione el texto que desee tachar. </td>
        </tr>
        <tr>
            <td> <img src="/help/assets/assets/Draw.svg"> Dibujo </td>
            <td> Inserte una ilustración visual en el PDF. </td>
        </tr>
        <tr>
            <td> <img src="/help/assets/assets/Erase.svg"> Borrar dibujo </td>
             <td> Quitar o deshacer el dibujo. </td>
        </tr>
    </table>

## Compatibilidad con la vista previa de varias páginas para documentos en otros formatos {#multi-format}

Además de los documentos del PDF, también puede obtener una vista previa de varias páginas para documentos en otros tipos de formato. Los tipos de formato de documento admitidos son TXT, RTF, DOC, DOCX, PPT, PPTX, XLS y XLSX. Experience Manager Assets convierte automáticamente estos formatos de documento en un formato de PDF y los pone a disposición de la vista previa.

![Vista previa de varias páginas de documentos en otros formatos](/help/assets/assets/multi-page-other-formats.png)

Para la vista previa de varias páginas de otros formatos de documento admitidos, realice los siguientes pasos:
1. Siga los pasos para [AEM carga de recursos en la](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/add-assets.html?lang=en).
1. Examine el documento que desea cargar y previsualizar.
1. Abra el documento.
1. Seleccione PDF en la sección estática del panel izquierdo. El panel derecho muestra la vista previa de varias páginas de un recurso. Seleccione la miniatura del panel izquierdo para elegir la página que desea previsualizar.

> NOTA
> * El tamaño máximo de un recurso que puede previsualizar es de hasta 100 MB.
> * El tamaño máximo de los archivos XLS o XLSX que se van a previsualizar es de 20 MB.
>


**Consulte también**

* [Traducir recursos](translate-assets.md)
* [API HTTP de Recursos](mac-api-assets.md)
* [Formatos de archivo compatibles con Assets](file-format-support.md)
* [Buscar recursos](search-assets.md)
* [Recursos conectados](use-assets-across-connected-assets-instances.md)
* [Informes de Asset](asset-reports.md)
* [Esquemas de metadatos](metadata-schemas.md)
* [Descarga de recursos](download-assets-from-aem.md)
* [Administración de metadatos](manage-metadata.md)
* [Facetas de búsqueda](search-facets.md)
* [Administrar colecciones](manage-collections.md)
* [Importación masiva de metadatos](metadata-import-export.md)
