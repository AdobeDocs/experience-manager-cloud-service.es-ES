---
title: Administre los documentos del PDF en [!DNL Adobe Experience Manager].
description: Administrar documentos de PDF en [!DNL Adobe Experience Manager] como [!DNL Cloud Service].
feature: Asset Management
role: User,Admin
source-git-commit: 9a600fb744c7064274fb4d849a5e01de2b83f575
workflow-type: tm+mt
source-wordcount: '794'
ht-degree: 0%

---

# Administrar documentos de PDF en Experience Manager Assets as a Cloud Service {#add-assets-to-experience-manager}

Experience Manager Assets se integra perfectamente con el visor de PDF de Document Cloud, lo que le permite previsualizar varias páginas de un documento de PDF. Además, también puede utilizar funciones avanzadas del visor del PDF de Document Cloud, como anotaciones, buscar texto, navegar por el documento del PDF mediante marcadores y miniaturas, etc., bajo el mismo techo. Experience Manager Assets también permite cargar documentos en otros formatos compatibles y previsualizarlos en formato de PDF.

El visor del PDF Document Cloud se beneficia de AEM Assets de las siguientes maneras:
* [Compatibilidad con los componentes del visor del Document Cloud del PDF](#pdf-doc-cloud)
* [Compatibilidad con la vista previa y las anotaciones de varias páginas para el recurso PDF](#multi-page)
* [Compatibilidad con la vista previa de varias páginas para documentos en otros formatos](#multi-format)

> Sugerencia
> Si no puede obtener la vista previa de varias páginas de un documento de PDF cargado anteriormente, seleccione el PDF y haga clic en **![Volver a procesar](/help/assets/assets/Reprocess.svg) Volver a procesar recursos**.

## Compatibilidad con los componentes del visor del Document Cloud del PDF {#pdf-doc-cloud}

El visor de PDF Doc Cloud nativo tiene los siguientes componentes en AEM Assets:

* **Visor de PDF mediante miniaturas de página** La vista en miniatura es una pequeña vista previa de las páginas de un documento PDF. Con las miniaturas, puede ir directamente a la página deseada. Puede acceder a las miniaturas del documento del PDF seleccionado mediante ![miniatura](/help/assets/assets/thumbnail.svg) en el panel izquierdo.

* **Visor de PDF con marcadores** Marcador es un vínculo directo que le lleva al contenido del documento. Puede acceder a los marcadores del documento del PDF seleccionado mediante ![marcador](/help/assets/assets/bookmark.svg) en el panel izquierdo.

* **Buscar en PDF** Puede utilizar la búsqueda ![búsqueda](/help/assets/assets/Search.svg) para buscar el texto en el documento del PDF.

* **Re Pág/Av Pág** Utilizar página arriba ![Re Pág](/help/assets/assets/ArrowUp.svg) o Av Pág ![Av Pág](/help/assets/assets/ArrowDown.svg) para desplazarse por el documento.

* **Reducir/Aumentar** Usar alejar ![Reducir](/help/assets/assets/ZoomOut.svg) o Aumentar ![Aumentar](/help/assets/assets/ZoomIn.svg) para dividir el documento.

* **Ajustar página** Utilice dimensiones de anchura o altura para ajustar el documento según el tamaño de la pantalla.

* **PDF de acoplamiento/desacoplamiento** Puede acoplar o desacoplar los componentes del visor de PDF nativo mediante esta opción.

## Compatibilidad con la vista previa y las anotaciones de varias páginas para el recurso PDF {#multi-page}

Adobe Experience Manager Assets permite obtener una vista previa del documento del PDF que consta de varias páginas. Para obtener una vista previa de varias páginas de un documento de PDF, siga estos pasos:

1. Siga los pasos para [cargar recursos en AEM](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/add-assets.html?lang=en).
1. Examine el documento del PDF que desea cargar y previsualizar.
1. Abra el documento.
1. El visor de documentos del PDF se carga de forma predeterminada. También puede seleccionar la representación del PDF en el panel de representación.
1. En la lista desplegable Representaciones , seleccione **Todas las representaciones**.

También puede aplicar [anotaciones](#pdf-annotations) al documento PDF en una vista previa de varias páginas.

> NOTA
> El tamaño máximo de un recurso que puede previsualizar es de hasta 100 MB.

>[!VIDEO](https://video.tv.adobe.com/v/3409355)

<!--
![Multi-page Preview](/help/assets/assets/multi-page.png)
-->

**Anotaciones de PDF{#pdf-annotations}**

Experience Manager Assets le permite agregar comentarios a un documento de PDF. Un documento PDF puede tener varias anotaciones.

Para realizar anotaciones en un documento de PDF, realice los pasos siguientes:
1. Vaya a la interfaz de Assets y vaya al documento del PDF que desea anotar. El visor del PDF nativo se abre a la derecha y muestra la previsualización del documento del PDF seleccionado.
1. Haga clic en **Anotar** en el menú superior.
A continuación se muestran las anotaciones que se pueden aplicar en un documento de PDF:

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
            <td> <img src="/help/assets/assets/Text.svg"> Cuadro de texto </td>
            <td> Seleccione Cuadro de texto para introducir el texto. </td>
        </tr>
        <tr>
            <td> <img src="/help/assets/assets/Note.svg"> Notas adhesivas </td>
            <td> Agregue un texto o recordatorio pequeño que pueda agregar a un área concreta del PDF. </td>
        </tr>
        <tr>
            <td> <img src="/help/assets/assets/Comment.svg"> Marcador de texto </td>
            <td> Seleccione el texto para resaltar en diferentes colores. </td>
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
             <td> Quitar o deshacer dibujo. </td>
        </tr>
    </table>

## Compatibilidad con la vista previa de varias páginas para documentos en otros formatos {#multi-format}

Además de los documentos del PDF, también puede obtener una vista previa de varias páginas para documentos de otros tipos de formato. Los tipos de formato de documento admitidos son TXT, RTF, DOC, DOCX, PPT, PPTX, XLS y XLSX. Experience Manager Assets convierte automáticamente estos formatos de documento en un formato de PDF y los pone a disposición de la vista previa.

![Vista previa de varias páginas de documentos en otros formatos](/help/assets/assets/multi-page-other-formats.png)

Para obtener la vista previa de varias páginas de otros formatos de documento compatibles, realice los siguientes pasos:
1. Siga los pasos para [cargar recursos en AEM](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/add-assets.html?lang=en).
1. Examine el documento que desea cargar y previsualizar.
1. Abra el documento.
1. Seleccione PDF en la sección estática del panel izquierdo. El panel derecho muestra la vista previa de varias páginas de un recurso. Seleccione la miniatura en el panel izquierdo para elegir la página de la que desea obtener una vista previa.

> NOTA
> * El tamaño máximo de un recurso que puede previsualizar es de hasta 100 MB.
> * El tamaño máximo de los archivos XLS o XLSX para previsualizar es de 20 MB.
> 

