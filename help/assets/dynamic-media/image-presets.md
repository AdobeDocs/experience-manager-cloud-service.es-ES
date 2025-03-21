---
title: Aplicación de ajustes preestablecidos de imagen de Dynamic Media
description: Aprenda a aplicar ajustes preestablecidos de imagen en Dynamic Media.
contentOwner: Rick Brough
feature: Image Presets,Viewers,Renditions
role: User
exl-id: ad21b52e-594f-4421-9b5a-2382d032ec5a
source-git-commit: c82f84fe99d8a196adebe504fef78ed8f0b747a9
workflow-type: tm+mt
source-wordcount: '349'
ht-degree: 10%

---

# Aplicación de ajustes preestablecidos de imagen de Dynamic Media {#applying-image-presets}

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

Los ajustes preestablecidos de imagen permiten que los recursos entreguen imágenes de forma dinámica en diferentes tamaños, en diferentes formatos o con otras propiedades de imagen que se generan dinámicamente. Puede elegir un ajuste preestablecido al exportar para cambiar el formato de las imágenes a las especificaciones que haya descrito el administrador.

Además, puede elegir un ajuste preestablecido de imagen que sea interactivo (designado por el botón **[!UICONTROL RESS]** después de seleccionarlo).

[Los administradores pueden crear y configurar ajustes preestablecidos de imagen](managing-image-presets.md).

>[!NOTE]
>
>Las imágenes inteligentes funcionan con los ajustes preestablecidos de imagen existentes. Utiliza inteligencia en el último milisegundo de envío para reducir aún más el tamaño del archivo de imagen en función de la velocidad de conexión del explorador o de la red. Consulte [Imágenes inteligentes](imaging-faq.md) para obtener más información.

Puede aplicar un ajuste preestablecido de imagen a una imagen cada vez que la previsualice.

**Para aplicar ajustes preestablecidos de imagen de Dynamic Media:**

1. Abra el recurso y, en el carril izquierdo, seleccione la lista desplegable y, a continuación, seleccione **[!UICONTROL Representaciones]**.

   >[!NOTE]
   >
   >* Las representaciones estáticas aparecen en la mitad superior del panel. Las representaciones dinámicas aparecen en la mitad inferior. Solo con las representaciones dinámicas, puede utilizar la dirección URL para mostrar la imagen. El botón **[!UICONTROL URL]** solo aparece si selecciona una representación dinámica. El botón **[!UICONTROL RESS]** solo aparece si selecciona un ajuste preestablecido de imagen interactivo.
   >
   >* El sistema muestra numerosas representaciones cuando selecciona **[!UICONTROL Representaciones]** en la vista de detalles de un recurso. Puede aumentar el número de ajustes preestablecidos vistos. Ver [Aumento del número de ajustes preestablecidos de imagen que se muestran](managing-image-presets.md#increasing-or-decreasing-the-number-of-image-presets-that-display).

   ![chlimage_1-208](assets/chlimage_1-208.png)

1. Realice una de las siguientes acciones:

   * Para previsualizar el ajuste preestablecido de imagen, seleccione una representación dinámica.
   * Para mostrar la ventana emergente, seleccione **[!UICONTROL URL]**, **[!UICONTROL Incrustar]** o **[!UICONTROL RESS]**.

   >[!NOTE]
   >
   >Si el recurso *y* el ajuste preestablecido de imagen aún no se han publicado, el botón **[!UICONTROL URL]** (o los botones URL y RESS, si corresponde) no están disponibles.
   >
   >Tenga en cuenta también que los ajustes preestablecidos de imagen se publican automáticamente en un servidor Dynamic Media S7.
