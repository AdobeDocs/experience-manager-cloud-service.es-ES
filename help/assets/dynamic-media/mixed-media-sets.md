---
title: Conjuntos de medios mixtos
description: Aprenda a trabajar con conjuntos de medios mixtos en Dynamic Media.
contentOwner: Rick Brough
feature: Mixed Media Sets
role: User
exl-id: 7ccde741-38d2-44c9-9378-f2721384aab7
source-git-commit: 36ab36ba7e14962eba3947865545b8a3f29f6bbc
workflow-type: tm+mt
source-wordcount: '1507'
ht-degree: 11%

---

# Conjuntos de medios mixtos{#mixed-media-sets}

Los conjuntos de medios mixtos permiten combinar imágenes, conjuntos de imágenes, conjuntos de giros y vídeos en una presentación.

Los conjuntos de medios mixtos se designan mediante un banner con la palabra **[!UICONTROL MixedMediaSet]**. Además, si se publica el conjunto de medios mixtos, se muestra la fecha de publicación, indicada por el icono **[!UICONTROL Mundo]**, junto a la fecha de la última modificación, indicada por el icono **[!UICONTROL Lápiz]**.

![chlimage_1-137](assets/chlimage_1-348.png)

>[!NOTE]
>
>Para obtener información sobre la interfaz de usuario de Assets, consulte [Administrar recursos con la IU táctil](/help/assets/manage-digital-assets.md).

## Inicio rápido: Conjuntos de medios mixtos {#quick-start-mixed-media-sets}

Para ponerse en marcha rápidamente con los conjuntos de medios mixtos, siga estos pasos:

1. [Cargue sus recursos](#uploading-assets).

   Comience por cargar las imágenes y los vídeos de los conjuntos de medios mixtos. Si es necesario, cree los [conjuntos de imágenes](/help/assets/dynamic-media/image-sets.md) y los [conjuntos de giros](/help/assets/dynamic-media/spin-sets.md). Dado que los usuarios pueden aplicar zoom a las imágenes en el visualizador de conjuntos de medios mixtos, asegúrese de tener en cuenta el zoom al elegir las imágenes. Asegúrese de que las imágenes tengan al menos 2000 píxeles del tamaño más grande.

   Consulte [Dynamic Media - Formatos de imagen rasterizada admitidos](/help/assets/file-format-support.md#image-support-dynamic-media) para obtener una lista de los formatos admitidos por los conjuntos de medios mixtos.

1. [Crear conjuntos de medios mixtos](#creating-mixed-media-sets).

   Para crear un conjunto de medios mixtos, en la página de Assets, ve a **[!UICONTROL Crear]** > **[!UICONTROL Conjunto de medios mixtos]** y, a continuación, asigna un nombre al conjunto, elige los recursos y elige el orden en que aparecen las imágenes.

   Consulte [Trabajar con selectores](/help/assets/dynamic-media/working-with-selectors.md).

1. Configure [ajustes preestablecidos del visualizador de medios mixtos](/help/assets/dynamic-media/managing-viewer-presets.md), según sea necesario.

   Los administradores pueden crear o modificar ajustes preestablecidos del visualizador de conjuntos de medios mixtos. Para ver los medios mixtos con un ajuste preestablecido del visualizador, seleccione el conjunto de medios mixtos y, en el menú desplegable del carril izquierdo, seleccione **[!UICONTROL Visualizadores]**.

   Para crear o editar ajustes preestablecidos de visor, vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Assets]** > **[!UICONTROL Ajustes preestablecidos de visor]**.

   Consulte [Agregar y editar ajustes preestablecidos de visor](/help/assets/dynamic-media/managing-viewer-presets.md).

1. [Previsualizar conjuntos de medios mixtos](#previewing-mixed-media-sets).

   Seleccione el conjunto de medios mixtos y podrá previsualizarlo. Para examinar el conjunto de medios mixtos en el visor seleccionado, seleccione los iconos de miniatura. Puede elegir diferentes visores en el menú **[!UICONTROL Visualizadores]**, disponible en el menú desplegable del carril izquierdo.

1. [Publicar conjuntos de medios mixtos](#publishing-mixed-media-sets).

   Al publicar un conjunto de medios mixtos, se activan la URL y la cadena de incrustación. Además, debe [publicar el ajuste preestablecido de visor](/help/assets/dynamic-media/managing-viewer-presets.md#publishing-viewer-presets).

1. [Vincular direcciones URL a la aplicación web](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md) o [Incrustar el visor de vídeo o de imágenes](/help/assets/dynamic-media/embed-code.md).

   Adobe Experience Manager Assets crea llamadas de URL para conjuntos de medios mixtos y las activa después de publicar los conjuntos de medios mixtos. Puede copiar estas direcciones URL al previsualizar los recursos. También puede incrustarlos en el sitio web.

   Seleccione el conjunto de medios mixtos y, a continuación, en el menú desplegable del carril izquierdo, seleccione **[!UICONTROL Visualizadores]**.

   Vea [Vincular un conjunto de medios mixtos a una página web](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md) e [Incrustar el visor de vídeo o de imágenes](/help/assets/dynamic-media/embed-code.md).

Si es necesario, puede editar [conjuntos de medios mixtos](#editing-mixed-media-sets). Además, puede ver y modificar [propiedades de conjuntos de medios mixtos](/help/assets/manage-digital-assets.md#editing-properties).

>[!NOTE]
>
>Si tiene problemas al crear conjuntos, consulte [Solucionar problemas de Dynamic Media](/help/assets/dynamic-media/troubleshoot-dm.md).

## Carga de activos {#uploading-assets}

Comience por cargar las imágenes y los vídeos de los conjuntos de medios mixtos. Recuerde que los usuarios pueden aplicar zoom a las imágenes en el visualizador de conjuntos de medios mixtos. Como tal, elija imágenes con esta capacidad de zoom en mente. Asegúrese de que las imágenes tengan al menos 2000 píxeles del tamaño más grande.

Además, si desea agregar conjuntos de giros o conjuntos de imágenes al conjunto de medios mixtos, créelos también.

Consulte [Dynamic Media - Formatos de imagen rasterizada admitidos](/help/assets/file-format-support.md#image-support-dynamic-media) para obtener una lista de los formatos admitidos por los conjuntos de medios mixtos.

## Crear conjuntos de medios mixtos {#creating-mixed-media-sets}

Puede agregar imágenes, conjuntos de imágenes, conjuntos de giros y vídeos a su conjunto de medios mixtos. Asegúrese de que los archivos, conjuntos de imágenes y conjuntos de giros estén listos para publicarse antes de agregarlos al conjunto de medios mixtos.

Al agregar recursos al conjunto, estos se agregan automáticamente en orden alfanumérico. Puede reordenar u ordenar manualmente los recursos una vez añadidos.

**Para crear conjuntos de medios mixtos:**

1. En Assets, vaya a donde desee crear un conjunto de medios mixtos, seleccione **[!UICONTROL Crear]** y **[!UICONTROL Conjunto de medios mixtos]**. También puede crear el conjunto desde una carpeta que contenga los recursos. Se muestra el Editor de conjuntos de medios mixtos.

   ![chlimage_1-138](assets/chlimage_1-349.png)

1. En el Editor de conjuntos de medios mixtos, en **[!UICONTROL Título]**, escriba un nombre para el conjunto de medios mixtos. El nombre aparece en el titular del conjunto de medios mixtos. Si lo desea, introduzca una descripción.

   ![chlimage_1-139](assets/chlimage_1-350.png)

   >[!NOTE]
   >
   >Al crear el conjunto de medios mixtos, puede cambiar la miniatura del conjunto de medios mixtos o permitir que Experience Manager seleccione la miniatura automáticamente en función de los recursos del conjunto de medios mixtos. Para seleccionar una miniatura, selecciona **[!UICONTROL Cambiar miniatura]** y selecciona cualquier imagen (también puedes navegar a otras carpetas para buscar imágenes). Si ha seleccionado una miniatura y decide que quiere que Experience Manager genere una del conjunto de medios mixtos, seleccione **[!UICONTROL Cambiar a Miniatura automática]**.

1. Para seleccionar los recursos que desea incluir en el conjunto de medios mixtos, seleccione el Selector de recursos. Selecciónelos y seleccione **[!UICONTROL Seleccionar]**.

   Con el Selector de recursos, puede buscar recursos escribiendo una palabra clave y seleccionando **[!UICONTROL Retorno]**. También puede aplicar filtros para restringir los resultados de búsqueda. Puede filtrar por ruta, colección, tipo de archivo y etiqueta. Seleccione el filtro y, a continuación, seleccione el icono **[!UICONTROL Filtro]** de la barra de herramientas. Para cambiar la vista, seleccione el icono **[!UICONTROL Ver]** y seleccione **[!UICONTROL Vista de lista]**, **[!UICONTROL Vista de columna]** o **[!UICONTROL Vista de tarjeta]**.

   Consulte [Uso de selectores](/help/assets/dynamic-media/working-with-selectors.md).

   ![chlimage_1-140](assets/chlimage_1-351.png)

1. Reordene los recursos arrastrándolos hacia arriba o hacia abajo en la lista (debe seleccionar el icono **[!UICONTROL Reordenar]**), según sea necesario.

   ![chlimage_1-141](assets/chlimage_1-352.png)

   Si desea agregar miniaturas, seleccione el icono **+** **[!UICONTROL miniatura]** que se encuentra junto a la imagen y vaya a la miniatura que desee. Cuando termine de seleccionar todas las imágenes en miniatura, seleccione **[!UICONTROL Guardar]**.

   >[!NOTE]
   >
   >Si desea agregar recursos, seleccione **[!UICONTROL Agregar recurso]**.

1. Para eliminar un recurso, selecciona la casilla correspondiente y selecciona **[!UICONTROL Eliminar recurso]**.
1. Para aplicar un ajuste preestablecido, seleccione **[!UICONTROL Ajuste preestablecido]** en la esquina superior derecha y seleccione un ajuste preestablecido para aplicar a los recursos.
1. Seleccione **[!UICONTROL Guardar]**. El conjunto de medios mixtos creado aparecerá en la carpeta en la que lo creó.

## Editar conjuntos de medios mixtos {#editing-mixed-media-sets}

Puede realizar varias tareas de edición en los recursos de conjuntos de medios mixtos directamente en la interfaz de usuario [como lo haría con cualquier recurso de Assets](/help/assets/manage-digital-assets.md). También puede realizar las siguientes acciones en conjuntos de medios mixtos:

* Agregar recursos al conjunto de medios mixtos.
* Reordenar recursos en el conjunto de medios mixtos.
* Eliminar recursos del conjunto de medios mixtos.
* Aplicar ajustes preestablecidos de visor.
* Cambie la miniatura predeterminada.

**Para editar conjuntos de medios mixtos:**

1. Realice una de las siguientes acciones:

   * Pase el ratón sobre un recurso de conjunto de medios mixtos y luego seleccione **[!UICONTROL Editar]** (icono de lápiz).
   * Pase el ratón sobre un recurso de conjunto de medios mixtos, seleccione **[!UICONTROL Seleccionar]** (icono de marca de verificación) y, a continuación, seleccione **[!UICONTROL Editar]** en la barra de herramientas.

   * Seleccione un recurso de conjunto de medios mixtos y, a continuación, seleccione **[!UICONTROL Editar]** (icono de lápiz) en la barra de herramientas.

1. En el Editor de conjuntos de medios mixtos, realice una de las siguientes acciones:

   * Para reordenar los recursos: en el panel izquierdo, seleccione **[!UICONTROL Assets]** (icono de imagen) y arrastre un recurso a una nueva ubicación.
   * Para agregar recursos: en la barra de herramientas, seleccione **[!UICONTROL Agregar recurso]**. Vaya a los recursos. Para cada recurso que desee agregar, pase el ratón sobre la imagen del recurso (no su nombre) y, a continuación, seleccione el icono de la marca de verificación. En la esquina superior derecha, seleccione **[!UICONTROL Seleccionar]**.

   * Para eliminar un recurso: en el panel izquierdo, seleccione **[!UICONTROL Assets]** (icono de imagen) y, a continuación, seleccione el recurso. En la barra de herramientas, seleccione **[!UICONTROL Eliminar recurso]**.

   * Para ordenar los recursos por su nombre en orden ascendente o descendente, en el panel izquierdo, seleccione **[!UICONTROL Assets]** (icono de imagen). A la derecha del encabezado de **[!UICONTROL Assets]**, seleccione los iconos de circunflejo invertido o ascendente.

     >[!NOTE]
     >
     >* Para eliminar un conjunto de medios mixtos completo, desplácese hasta el conjunto de medios mixtos desde cualquier modo de visualización (como **[!UICONTROL Vista de tarjeta]** o **[!UICONTROL Vista de columna]**). Pase el ratón sobre el recurso y, a continuación, seleccione el icono de marca de verificación para poder seleccionarlo. Presione **[!UICONTROL Retroceso]** en el teclado o seleccione **[!UICONTROL Más]** (tres puntos) en la barra de herramientas y, a continuación, seleccione **[!UICONTROL Eliminar]**.
     >
     >* Puede editar los recursos de un conjunto de medios mixtos navegando hasta él. En el carril izquierdo, seleccione **[!UICONTROL Definir miembros]** y, a continuación, seleccione el icono **[!UICONTROL Lápiz]** en un recurso individual para abrir la ventana de edición.

1. Seleccione **[!UICONTROL Guardar]** cuando haya terminado de editar.

   >[!NOTE]
   >
   >* Para editar los recursos de un conjunto de medios mixtos, vaya al conjunto de medios mixtos. Seleccione (no seleccione) el conjunto para poder abrirlo en la página Vista previa de conjunto de Experience Manager. En el carril izquierdo, seleccione el circunflejo invertido para abrir la lista desplegable y, a continuación, seleccione **[!UICONTROL Definir miembros]**. En la página Definir miembros, coloque el puntero sobre un recurso y, a continuación, seleccione **[!UICONTROL Editar]** (icono de lápiz) para abrir la página de edición.
   >
   >* Para eliminar un conjunto de medios mixtos completo, en cualquier modo de visualización (como la vista de tarjeta o la vista de columna), vaya al conjunto de medios mixtos. Pase el ratón sobre el conjunto y luego seleccione **[!UICONTROL Seleccionar]** (icono de marca de verificación). Presione **[!UICONTROL Retroceso]** en el teclado o seleccione **[!UICONTROL Más]** (fila de tres puntos) y luego seleccione **[!UICONTROL Eliminar]**.

## Previsualizar conjuntos de medios mixtos {#previewing-mixed-media-sets}

Consulte [Previsualizar recursos](/help/assets/dynamic-media/previewing-assets.md) para obtener más información sobre cómo obtener una vista previa de conjuntos de medios mixtos.

## Publicar conjuntos de medios mixtos {#publishing-mixed-media-sets}

Consulte [Publicar recursos](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md) para obtener más información sobre cómo publicar conjuntos de medios mixtos.

>[!NOTE]
>
>Si el conjunto de medios mixtos no termina completamente en el servicio de entrega la primera vez que lo publica, publique el conjunto de medios mixtos por segunda vez.
