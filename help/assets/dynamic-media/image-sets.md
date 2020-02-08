---
title: Conjuntos de imágenes
description: Aprenda a trabajar con conjuntos de imágenes en Dynamic Media
translation-type: tm+mt
source-git-commit: 6224d193adfb87bd9b080f48937e0af1f03386d6

---


# Conjuntos de imágenes {#image-sets}

Los conjuntos de imágenes proporcionan a los usuarios una experiencia de visualización integrada, en la que pueden ver distintas vistas de un elemento haciendo clic en una imagen en miniatura. Los conjuntos de imágenes le permiten presentar vistas alternativas de un elemento y el visor ofrece herramientas de zoom para examinar las imágenes de cerca.

Los conjuntos de imágenes se designan mediante una pancarta con la palabra `IMAGESET`. Además, si se publica el conjunto de imágenes, se muestra la fecha de publicación, indicada por el icono **[!UICONTROL Mundo]** , junto con la fecha de la última modificación, indicada por el icono **[!UICONTROL Lápiz]** .

![chlimage_1-133](assets/chlimage_1-339.png)

Dentro del conjunto de imágenes, también puede crear muestras creando un conjunto de imágenes y agregando miniaturas.

Esta aplicación resulta especialmente útil para cuando desea mostrar un elemento con un color, un motivo o un acabado diferentes. Para crear un conjunto de imágenes con muestras de color, necesita una imagen para cada color, motivo o acabado diferente que desee presentar a los usuarios. También necesita una muestra de color, motivo o acabado para cada color, motivo o acabado.

Por ejemplo, supongamos que desea presentar imágenes de gorras con diferentes listas de colores; las facturas son rojas, verdes y azules. En este caso, se necesitan tres tomas de la misma tapa. Se necesita un tiro con un rojo, uno con un verde y otro con un billete azul. También necesita una muestra de color rojo, verde y azul. Las muestras de color sirven como miniaturas en las que los usuarios hacen clic en el visor de conjuntos de muestras para ver el gorro de facturación roja, verde o azul.

>[!NOTE]
>
>Para obtener información sobre la interfaz de usuario de Recursos, consulte [Gestión de recursos con la IU](/help/assets/manage-digital-assets.md)táctil.

## Inicio rápido: Conjuntos de imágenes {#quick-start-image-sets}

Para ayudarle a ponerse en marcha rápidamente:

1. [Cargue las imágenes principales para varias vistas.](#uploading-assets-in-image-sets)

   Comience por cargar las imágenes para los conjuntos de imágenes. Dado que los usuarios pueden aplicar zoom a las imágenes en el visor de conjuntos de imágenes, tenga en cuenta el zoom al elegir las imágenes. Asegúrese de que las imágenes tengan al menos 2000 píxeles en la dimensión más grande. AEM Assets admite muchos formatos de archivo de imagen, pero se recomiendan las imágenes TIFF, PNG y EPS sin pérdida.

1. [Crear conjuntos de imágenes.](#creating-image-sets)

   En los conjuntos de imágenes, los usuarios hacen clic en las imágenes en miniatura en el visor de conjuntos de imágenes.

   Para crear un conjunto de imágenes en Recursos, toque o haga clic en **[!UICONTROL Crear > Conjuntos]** de imágenes. A continuación, agregue imágenes y haga clic en **[!UICONTROL Guardar]**.

   También puede crear conjuntos de imágenes automáticamente mediante ajustes preestablecidos [de conjuntos de](/help/assets/dynamic-media/config-dm.md#creating-batch-set-presets-to-auto-generate-image-sets-and-spin-sets)lotes.

   >[!IMPORTANT]
   >
   > Los conjuntos de lotes son creados por IPS (Image Production System) como parte de la ingesta de recursos.

   Consulte [Preparación de recursos de conjuntos de imágenes para cargar y Carga de archivos](#uploading-assets-in-image-sets).

   See [Working with Selectors.](/help/assets/dynamic-media/working-with-selectors.md)

1. Agregue los ajustes preestablecidos [del visor de conjuntos de](/help/assets/dynamic-media/managing-viewer-presets.md)imágenes según sea necesario.

   Los administradores pueden crear o modificar ajustes preestablecidos de visor de conjuntos de imágenes. Para ver el conjunto de imágenes con un ajuste preestablecido de visor, seleccione el conjunto de imágenes y, en el menú desplegable del carril izquierdo, seleccione **[!UICONTROL Visores]**.

   Consulte **[!UICONTROL Herramientas > Recursos > Ajustes preestablecidos]** de visor para crear o editar ajustes preestablecidos de visor.

1. (Opcional) [Visualización de conjuntos](/help/assets/dynamic-media/image-sets.md#viewing-image-sets) de imágenes creados mediante ajustes preestablecidos de conjunto por lotes.
1. [Vista previa de conjuntos de imágenes.](/help/assets/dynamic-media/previewing-assets.md)

   Seleccione el conjunto de imágenes y puede previsualizarlo. Haga clic en los iconos de miniaturas para examinar el conjunto de imágenes en el visor seleccionado. Puede elegir diferentes visores en el menú **[!UICONTROL Visores]** , disponible en el menú desplegable del carril izquierdo.

1. [Publicar conjuntos de imágenes.](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md)

   Al publicar un conjunto de imágenes, se activa la URL y la cadena Incrustar. Además, debe [publicar cualquier ajuste preestablecido](/help/assets/dynamic-media/managing-viewer-presets.md) de visor personalizado que haya creado. Los ajustes preestablecidos de visor predeterminados ya están publicados.

1. [Vincule direcciones URL a la aplicación](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md) web o [incruste el visor](/help/assets/dynamic-media/embed-code.md)de vídeo o de imágenes.

   Recursos AEM crea llamadas mediante URL para conjuntos de imágenes y los activa después de publicar los conjuntos de imágenes. Puede copiar estas direcciones URL al obtener una vista previa de los recursos. Como alternativa, puede incrustarlos en su sitio Web.

   Seleccione el conjunto de imágenes y, a continuación, en el menú desplegable del carril izquierdo, seleccione **[!UICONTROL Visores]**.

   Consulte [Vinculación de un conjunto de imágenes a una página](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md) web e [Incrustación del visor](/help/assets/dynamic-media/embed-code.md)de imágenes o vídeos.

Para editar conjuntos de imágenes, consulte [Edición de conjuntos de imágenes.](#editing-image-sets) Además, puede ver y editar las propiedades [del conjunto](/help/assets/manage-digital-assets.md#editing-properties)de imágenes.

Si tiene problemas al crear conjuntos, consulte Imágenes y conjuntos en [Resolución de problemas de Dynamic Media](/help/assets/dynamic-media/troubleshoot-dm.md#images-and-sets).

## Carga de recursos en conjuntos de imágenes {#uploading-assets-in-image-sets}

Comience por cargar las imágenes para los conjuntos de imágenes. Dado que los usuarios pueden aplicar zoom a las imágenes en el visor de conjuntos de imágenes, tenga en cuenta el zoom al elegir las imágenes. Asegúrese de que las imágenes tengan al menos 2000 píxeles en la dimensión más grande. Los conjuntos de imágenes admiten muchos formatos de archivo de imagen, pero se recomiendan las imágenes TIFF, PNG y EPS sin pérdida.

Puede cargar imágenes para los conjuntos de imágenes como lo haría con cualquier otro [recurso en Recursos](/help/assets/manage-digital-assets.md#uploading-assets).

### Preparación de recursos de conjuntos de imágenes para la carga {#preparing-image-set-assets-for-upload}

Antes de crear conjuntos de imágenes, asegúrese de que las imágenes tienen el tamaño y el formato adecuados.

Para crear un conjunto de imágenes de varias vistas, necesita imágenes que muestren un elemento desde diferentes puntos de vista o que muestren diferentes aspectos del mismo elemento. El objetivo es resaltar las características importantes de un elemento para que los usuarios tengan una imagen completa de su aspecto o funcionamiento.

Dado que los usuarios pueden aplicar zoom a las imágenes en los conjuntos de imágenes, asegúrese de que las imágenes tengan al menos 2000 píxeles en la dimensión más grande. Assets admite muchos formatos de archivo de imagen, pero se recomiendan las imágenes TIFF, PNG y EPS sin pérdida.

>[!NOTE]
>
>Además, si utiliza miniaturas para indicar muestras de productos, debe hacer lo siguiente:
>
>Necesita viñetas o tomas diferentes de la misma imagen que la muestren en colores, patrones o acabados diferentes. También necesita archivos de miniaturas que se correspondan con los diferentes colores, patrones o acabados. Por ejemplo, para presentar miniaturas con un conjunto de imágenes que muestre la misma chaqueta en negro, marrón y verde, necesitará:
>
>* Toma negra, marrón y verde de la misma chaqueta.
>* Miniatura de color negro, marrón y verde.


## Creación de conjuntos de imágenes {#creating-image-sets}

Puede crear conjuntos de imágenes a través de la interfaz de usuario o de la API. En esta sección se describe cómo crear conjuntos de imágenes en la interfaz de usuario.

>[!NOTE]
>
>También puede crear conjuntos de imágenes automáticamente mediante ajustes preestablecidos [de conjuntos de](/help/assets/dynamic-media/config-dm.md#creating-batch-set-presets-to-auto-generate-image-sets-and-spin-sets)lotes.
>****Importante: Los conjuntos de lotes son creados por IPS (Image Production System) como parte de la ingesta de recursos.

Cuando se agregan recursos al conjunto, se añaden automáticamente en orden alfanumérico. Puede volver a ordenar o ordenar manualmente los recursos después de agregarlos.

>[!NOTE]
>
>Los conjuntos de imágenes no son compatibles con los recursos con &quot;,&quot; (coma) en el nombre del archivo.

**Para crear un conjunto de imágenes**

1. En AEM, toque el logotipo de AEM para acceder a la consola de navegación global y, a continuación, toque **[!UICONTROL Navegación > Recursos]**. Vaya a donde desee crear un conjunto de imágenes y, a continuación, toque **[!UICONTROL Crear > Conjunto]** de imágenes para abrir la página Editor de conjuntos de imágenes.

   También puede crear el conjunto desde una carpeta que contenga los recursos.

   ![6_5_imagesets-createpulldown](assets/6_5_imagesets-createpulldown.png)

1. En la página Editor de conjuntos de imágenes, en el campo **[!UICONTROL Título]** , introduzca un nombre para el conjunto de imágenes. El nombre aparece en la pancarta del conjunto de imágenes. De forma opcional, introduzca una descripción.

   ![6_5_imageset-creatingnewset](assets/6_5_imageset-creatingnewset.png)

1. Realice una de las siguientes acciones:

   * Cerca de la esquina superior izquierda de la página Editor de conjuntos de imágenes, toque **[!UICONTROL Agregar recurso]**.

   * Cerca del centro de la página Editor de conjuntos de imágenes, toque **[!UICONTROL Tocar para abrir el Selector]** de recursos.
   Toque para seleccionar los recursos que desea incluir en el conjunto de imágenes. Los recursos seleccionados tienen un icono de marca de verificación sobre ellos. Cuando haya terminado, toque **[!UICONTROL Seleccionar]** cerca de la esquina superior derecha de la página.

   Con el Selector de recursos, puede buscar recursos escribiendo una palabra clave y tocando o haciendo clic en **[!UICONTROL Retorno]**. También puede aplicar filtros para restringir los resultados de búsqueda. Puede filtrar por ruta, colección, tipo de archivo y etiqueta. Seleccione el filtro y, a continuación, toque el icono **[!UICONTROL Filtro]** en la barra de herramientas. Para cambiar la vista, toque el icono Ver y seleccione Vista **[!UICONTROL de]** columna, Vista **[!UICONTROL de]** tarjeta o Vista **[!UICONTROL de]** lista.

   See [Working with Selectors.](/help/assets/dynamic-media/working-with-selectors.md)

   ![6_5_imageset-addingassets](assets/6_5_imageset-addingassets.png)

1. Cuando se agregan recursos al conjunto, se añaden automáticamente en orden alfanumérico. Después de agregarlos, puede reordenar o ordenar manualmente los recursos.

   Si es necesario, arrastre el icono Reordenar de un recurso a la derecha del nombre de archivo del recurso para reordenar las imágenes hacia arriba o hacia abajo en la lista de elementos.

   ![6_5_imageset-reorderassets](assets/6_5_imageset-reorderassets.png)

   Si desea cambiar una miniatura o muestra, haga clic en el icono **+** **miniatura** situado junto a la imagen y vaya a la miniatura o muestra que desee. Cuando termine de seleccionar todas las imágenes, haga clic en **[!UICONTROL Guardar]**.

1. (Opcional) Realice cualquiera de las siguientes acciones:

   * Para eliminar una imagen, selecciónela y toque **[!UICONTROL Eliminar recurso]**.

   * Para aplicar un ajuste preestablecido, cerca de la esquina superior derecha de la página, toque **[!UICONTROL Ajuste preestablecido]** y, a continuación, seleccione un ajuste preestablecido para aplicar a todos los recursos a la vez.
   >[!NOTE]
   >
   >Al crear el conjunto de imágenes, puede cambiar la miniatura del conjunto de imágenes o permitir que AEM seleccione la miniatura automáticamente en función de los recursos del conjunto de imágenes. Para seleccionar una miniatura, toque **[!UICONTROL Cambiar miniatura]** sobre el campo Título en la página Editor de conjuntos de imágenes y, a continuación, seleccione cualquier imagen (puede navegar también a otras carpetas para buscar imágenes). Si ha seleccionado una miniatura y, a continuación, decide que desea que AEM genere una del conjunto de imágenes, seleccione **[!UICONTROL Cambiar a]** miniatura **** automática.

1. Haga clic en **[!UICONTROL Guardar.]** El conjunto de imágenes recién creado aparece en la carpeta en la que lo creó.

## Visualización de conjuntos de imágenes {#viewing-image-sets}

Puede crear conjuntos de imágenes en la interfaz de usuario o automáticamente mediante ajustes preestablecidos [de conjunto de](/help/assets/dynamic-media/config-dm.md#creating-batch-set-presets-to-auto-generate-image-sets-and-spin-sets)lotes.

>[!IMPORTANT]
>
>Los conjuntos de lotes son creados por IPS [Image Production System] como parte de la ingesta de recursos.

Sin embargo, los conjuntos creados con ajustes preestablecidos de conjunto de lotes *no aparecen* en la interfaz de usuario. Puede ver estos conjuntos de tres formas diferentes. (Estos métodos están disponibles aunque haya creado los conjuntos de imágenes en la interfaz de usuario).

* Abra las propiedades de un recurso individual. Las propiedades indican los conjuntos de los que se hace referencia al recurso seleccionado o un miembro. Haga clic en el nombre del conjunto para ver el conjunto completo.

   ![6_5_imageset-assetproperties](assets/6_5_imageset-assetproperties.png)

* Desde una imagen de miembro de cualquier conjunto. Seleccione el menú **[!UICONTROL Sets** para mostrar los conjuntos de los que es miembro el recurso.

   ![6_5_imageset-setspulldownmenu](assets/6_5_imageset-setspulldownmenu.png)

* Desde la búsqueda, puede seleccionar **[!Filtro** UICONTROL, luego expandir **[!UICONTROL Dynamic Media** y seleccionar **[!UICONTROL Conjuntos]**.

   La búsqueda devuelve conjuntos coincidentes creados manualmente en la interfaz de usuario o creados automáticamente mediante ajustes preestablecidos de conjunto por lotes. Para los conjuntos automatizados, la consulta de búsqueda se realiza utilizando criterios de búsqueda &quot;Comienza con&quot; diferentes de la búsqueda de AEM, que se basa en el uso de criterios de búsqueda &quot;Contiene&quot;. Definir el filtro en **[!UICONTROL Conjuntos]** es la única manera de buscar conjuntos automatizados.

   ![chlimage_1-134](assets/chlimage_1-134.png)

>[!NOTE]
>
>Los conjuntos se pueden ver mediante la interfaz de usuario, tal como se describe en [Edición de conjuntos](#editing-image-sets)de imágenes.

## Edición de conjuntos de imágenes {#editing-image-sets}

Puede realizar diversas tareas de edición en conjuntos de imágenes, como las siguientes:

* Agregue imágenes al conjunto de imágenes.
* Vuelva a ordenar las imágenes en el conjunto de imágenes.
* Elimine recursos del conjunto de imágenes.
* Aplicación de ajustes preestablecidos de visor.
* Elimine el conjunto de imágenes.

**Para editar conjuntos de imágenes**

1. Realice una de las siguientes acciones:

   * Pase el ratón sobre un recurso de conjunto de imágenes y, a continuación, toque **[!UICONTROL Editar]** (icono de lápiz).
   * Pase el ratón sobre un recurso de conjunto de imágenes, toque **[!UICONTROL Seleccionar]** (icono de marca de verificación) y, a continuación, toque **[!UICONTROL Editar]** en la barra de herramientas.
   * Toque en un recurso de conjunto de imágenes y, a continuación, toque **[!UICONTROL Editar]** (icono de lápiz) en la barra de herramientas.

1. Para editar las imágenes en el conjunto de imágenes, realice una de las siguientes acciones:

   * Para reordenar recursos, arrastre una imagen a una nueva ubicación (seleccione el icono de reordenar para mover elementos).
   * Para ordenar los elementos en orden ascendente o descendente, haga clic en el encabezado de la columna.
   * Para agregar un recurso o actualizar un recurso existente, haga clic en **[!UICONTROL Agregar recurso]**. Vaya a un recurso, selecciónelo y, a continuación, toque **[!UICONTROL Seleccionar]** cerca de la esquina superior derecha de la página.
      >[!NOTE]
      >
      >Si elimina la imagen que AEM utiliza para la miniatura sustituyéndola por otra imagen, el recurso original seguirá apareciendo.
   * Para eliminar un recurso, selecciónelo y toque o haga clic en **[!UICONTROL Eliminar recurso]**.
   * Para aplicar un ajuste preestablecido, toque **[!UICONTROL Ajuste preestablecido]** y, a continuación, seleccione un ajuste preestablecido de visor cerca de la esquina superior derecha de la página.
   * Para añadir o cambiar una miniatura, seleccione el icono de miniatura situado junto a la derecha del recurso. Vaya al nuevo recurso de miniatura o muestra, selecciónelo y toque **[!UICONTROL Seleccionar]**.
   * Para eliminar un conjunto de imágenes completo, desplácese hasta el conjunto de imágenes, selecciónelo y toque **[!UICONTROL Eliminar]**.
   >[!NOTE]
   >
   >Para editar las imágenes de un conjunto de imágenes, vaya al conjunto, toque **[!UICONTROL Establecer miembros]** en el carril izquierdo y, a continuación, toque el icono Lápiz en un recurso individual para abrir la ventana de edición.

1. Toque **[!UICONTROL Guardar]** cuando haya terminado de editar.

## Vista previa de conjuntos de imágenes {#previewing-image-sets}

Consulte [Vista previa de recursos](/help/assets/dynamic-media/previewing-assets.md).

## Publicación de conjuntos de imágenes {#publishing-image-sets}

Consulte [Publicación de recursos](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md).
