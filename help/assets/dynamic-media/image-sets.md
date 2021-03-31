---
title: Conjuntos de imágenes
description: Aprenda a trabajar con conjuntos de imágenes en Dynamic Media.
feature: Conjuntos de imágenes
topic: Profesional empresarial
role: Profesional empresarial
translation-type: tm+mt
source-git-commit: 497952b1b6679eca301839d1435924e16a2e2438
workflow-type: tm+mt
source-wordcount: '2053'
ht-degree: 9%

---


# Conjuntos de imágenes {#image-sets}

Los conjuntos de imágenes proporcionan a los usuarios una experiencia de visualización integrada, en la que los usuarios pueden ver distintas vistas de un elemento haciendo clic en una imagen en miniatura. Los conjuntos de imágenes permiten presentar vistas alternativas de un elemento y el visor ofrece herramientas de zoom para examinar las imágenes con mayor detenimiento.

Los conjuntos de imágenes se designan mediante una pancarta con la palabra `IMAGESET`. Además, si se publica el conjunto de imágenes, la fecha de publicación, indicada por el icono **[!UICONTROL Mundo]**, está en el banner. Además, se muestra la fecha de la última modificación, indicada por el icono **[!UICONTROL Lápiz]**.

![chlimage_1-133](assets/chlimage_1-339.png)

Dentro del conjunto de imágenes, también puede crear muestras creando un conjunto de imágenes y agregando miniaturas.

Esta aplicación es útil para cuando desea mostrar un elemento en un color, patrón o acabado diferentes. Para crear un conjunto de imágenes con muestras de color, necesita una imagen para cada color, patrón o acabado diferente que desee presentar a los usuarios. También necesita una muestra de color, patrón o fin para cada color, patrón o acabado.

Por ejemplo, supongamos que desea presentar imágenes de mayúsculas con diferentes listas de colores; los billetes son rojo, verde y azul. En este caso, se necesitan tres tomas de la misma tapa. Necesitas un tiro con un rojo, uno con un verde y otro con un billete azul. También necesita una muestra de color rojo, verde y azul. Las muestras de color sirven como miniaturas en las que los usuarios hacen clic en el Visor de conjuntos de muestras para ver el gorro de facturación roja, verde o azul.

>[!NOTE]
>
>Para obtener información sobre la interfaz de usuario de Assets, consulte [Administración de recursos con la IU táctil](/help/assets/manage-digital-assets.md).

## Inicio rápido: Conjuntos de imágenes {#quick-start-image-sets}

Para ponerle en marcha rápidamente:

1. Opcional. [Cree un conjunto de lotes preestablecido y ](/help/assets/dynamic-media/batch-set-presets-dm.md) aplíquelo a una nueva carpeta en la que se carguen las imágenes del conjunto de giros.

   Un ajuste preestablecido de conjunto de lotes puede ayudarle a automatizar la creación del conjunto de imágenes.

   >[!IMPORTANT]
   >
   >IPS (Image Production System) crea los conjuntos de lotes como parte de la ingesta de recursos.

1. [Cargue las imágenes de origen principales para varias vistas.](#uploading-assets-in-image-sets)

   Cargue las imágenes para sus conjuntos de imágenes. Recuerde que los usuarios pueden hacer zoom en las imágenes en el visor de conjuntos de imágenes. Como tal, elija sus imágenes con cuidado. Compruebe que las imágenes tengan al menos 2000 píxeles en la dimensión más grande. Recursos de Experience Manager admite muchos formatos de archivo de imagen, pero se recomiendan las imágenes TIFF, PNG y EPS sin pérdida.

1. [Crear conjuntos de imágenes.](#creating-image-sets)

   En los conjuntos de imágenes, los usuarios hacen clic en las imágenes en miniatura en el visor de conjuntos de imágenes.

   Para crear un conjunto de imágenes en Assets, pulse o haga clic en **[!UICONTROL Crear > Conjuntos de imágenes]**. A continuación, añada imágenes y haga clic en **[!UICONTROL Guardar]**.

   Consulte [Preparación de recursos de conjuntos de imágenes para cargar y cargar los archivos](#uploading-assets-in-image-sets).

   Consulte [Uso de selectores.](/help/assets/dynamic-media/working-with-selectors.md)

1. Agregue [Ajustes preestablecidos del visualizador de conjuntos de imágenes](/help/assets/dynamic-media/managing-viewer-presets.md) según sea necesario.

   Los administradores pueden crear o modificar ajustes preestablecidos de visualizador de conjuntos de imágenes. Para ver el conjunto de imágenes con un ajuste preestablecido de visualizador, seleccione el conjunto de imágenes y, en la lista desplegable del carril izquierdo, seleccione **[!UICONTROL Visualizadores]**.

   Para crear o editar ajustes preestablecidos de visualizador, consulte **[!UICONTROL Herramientas > Recursos > Ajustes preestablecidos de visualizador]**.

1. (Opcional) [Visualización de conjuntos de imágenes](/help/assets/dynamic-media/image-sets.md#viewing-image-sets) que se crearon mediante ajustes preestablecidos de conjuntos de lotes.
1. [Vista previa de conjuntos de imágenes.](/help/assets/dynamic-media/previewing-assets.md)

   Seleccione el conjunto de imágenes y podrá previsualizarlo. Para examinar el conjunto de imágenes en el visualizador seleccionado, pulse los iconos de miniaturas. Puede elegir diferentes visores desde el menú **[!UICONTROL Visualizadores]**, disponible en la lista desplegable del carril izquierdo.

1. [Publicar conjuntos de imágenes.](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md)

   Al publicar un conjunto de imágenes, se activa la dirección URL y la cadena de incrustación. Además, debe [publicar cualquier ajuste preestablecido de visualizador personalizado](/help/assets/dynamic-media/managing-viewer-presets.md) que haya creado. Ya se han publicado los ajustes preestablecidos del visor integrado.

1. [Vincule las URL a su ](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md) aplicación web o  [incruste el visualizador de imágenes o vídeos](/help/assets/dynamic-media/embed-code.md).

   Recursos de Experience Manager crea llamadas de URL para conjuntos de imágenes y los activa después de publicar los conjuntos de imágenes. Puede copiar estas direcciones URL cuando obtiene una vista previa de los recursos. También puede incrustarlos en el sitio web.

   Seleccione el conjunto de imágenes y, a continuación, en la lista desplegable del carril izquierdo, seleccione **[!UICONTROL Visualizadores]**.

   Consulte [Vinculación de un conjunto de imágenes a una página web](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md) e [Incrustación del visualizador de imágenes o vídeos](/help/assets/dynamic-media/embed-code.md).

Para editar los conjuntos de imágenes, consulte [edición de conjuntos de imágenes.](#editing-image-sets) Además, puede ver y editar las  [propiedades](/help/assets/manage-digital-assets.md#editing-properties) del conjunto de imágenes.

Si tiene problemas al crear conjuntos, consulte Imágenes y conjuntos en [Solución de problemas de Dynamic Media](/help/assets/dynamic-media/troubleshoot-dm.md#images-and-sets).

## Carga de recursos para conjuntos de imágenes {#uploading-assets-in-image-sets}

Comience por cargar los recursos de imagen para los conjuntos de imágenes. Recuerde que los usuarios pueden hacer zoom en las imágenes en el visor de conjuntos de imágenes. Como tal, elija sus imágenes con cuidado. Asegúrese de que las imágenes tengan al menos 2000 píxeles en la dimensión más grande para obtener un detalle de zoom óptimo. Dynamic Media puede procesar imágenes de hasta 25 megapíxeles cada una. Por ejemplo, puede utilizar una imagen de 5000 x 5000 megapíxeles o cualquier otra combinación de tamaño de hasta 25 megapíxeles.

Los conjuntos de imágenes admiten muchos formatos de archivo de imagen, pero se recomiendan las imágenes TIFF, PNG y EPS sin pérdida.

Puede cargar imágenes para conjuntos de imágenes del mismo modo que lo haría con [cualquier otro recurso en Assets](/help/assets/manage-digital-assets.md#uploading-assets).

### Preparación de recursos de conjuntos de imágenes para la carga {#preparing-image-set-assets-for-upload}

Antes de crear conjuntos de imágenes, asegúrese de que las imágenes tengan el tamaño y el formato adecuados.

Para crear un conjunto de imágenes de varias vistas, necesita imágenes que muestren un elemento desde diferentes puntos de vista o que muestren diferentes aspectos del mismo elemento. El objetivo es resaltar las características importantes de un elemento para que los espectadores tengan una imagen completa de cómo se ve o hace.

Dado que los usuarios pueden hacer zoom en las imágenes en los conjuntos de imágenes, asegúrese de que las imágenes tengan al menos 2000 píxeles en la dimensión más grande. Recursos de Experience Manager admite muchos formatos de archivo de imagen, pero se recomiendan las imágenes TIFF, PNG y EPS sin pérdida.

>[!NOTE]
>
>Si utiliza miniaturas para indicar muestras de productos, haga lo siguiente:
>
>Cree viñetas o tomas diferentes de la misma imagen mostrándola en diferentes colores, patrones o acabados. También necesita archivos en miniatura que correspondan a los diferentes colores, patrones o acabados. Por ejemplo, para presentar miniaturas con un conjunto de imágenes que muestre la misma chaqueta en negro, marrón y verde, necesitará:
>
>* Un tiro negro, marrón y verde de la misma chaqueta.
>* Miniatura de color negro, marrón y verde.


## Creación de conjuntos de imágenes {#creating-image-sets}

Puede crear conjuntos de imágenes a través de la interfaz de usuario o mediante la API.

>[!NOTE]
>
>También puede crear conjuntos de imágenes automáticamente mediante [ajustes preestablecidos de conjuntos de lotes](/help/assets/dynamic-media/batch-set-presets-dm.md).
>**Importante:** IPS (Image Production System) crea los conjuntos de lotes como parte de la ingesta de recursos.

Cuando se añaden recursos al conjunto, estos se añaden automáticamente en orden alfanumérico. Puede reordenar u ordenar manualmente los recursos una vez añadidos.

>[!NOTE]
>
>Los conjuntos de imágenes no son compatibles con los recursos con &quot;,&quot; (coma) en el nombre de archivo.

**Para crear un conjunto de imágenes**

1. En Adobe Experience Manager, pulse el logotipo del Experience Manager para acceder a la consola de navegación global.
1. Pulse **[!UICONTROL Navegación > Assets]**. Vaya a donde desee crear un conjunto de imágenes y, a continuación, pulse **[!UICONTROL Crear > Conjunto de imágenes]** para abrir la página Editor de conjuntos de imágenes.

   También puede crear el conjunto desde una carpeta que contenga los recursos.

   ![6_5_imagesets-createpulldown](assets/6_5_imagesets-createpulldown.png)

1. En la página Editor de conjuntos de imágenes, en el campo **[!UICONTROL Título]**, introduzca un nombre para el conjunto de imágenes. El nombre aparece en el banner del conjunto de imágenes. De forma opcional, introduzca una descripción.

   ![6_5_imageset-creatingnewset](assets/6_5_imageset-creatingnewset.png)

1. Realice una de las siguientes acciones:

   * Cerca de la esquina superior izquierda de la página Editor de conjuntos de imágenes, pulse **[!UICONTROL Agregar recurso]**.

   * Cerca del centro de la página Editor de conjuntos de imágenes, pulse **[!UICONTROL Toque para abrir el Selector de recursos]**.
   Pulse para seleccionar los recursos que desea incluir en el conjunto de imágenes. Los recursos seleccionados tienen un icono de marca de verificación sobre ellos. Cuando termine, cerca de la esquina superior derecha de la página, pulse **[!UICONTROL Seleccionar]**.

   Con el Selector de recursos, puede buscar recursos escribiendo una palabra clave y pulsando o haciendo clic en **[!UICONTROL Retorno]**. También puede aplicar filtros para restringir los resultados de búsqueda. Puede filtrar por ruta, colección, tipo de archivo y etiqueta. Seleccione el filtro y, a continuación, pulse el icono **[!UICONTROL Filter]** en la barra de herramientas. Para cambiar la vista, pulse el icono Ver y seleccione **[!UICONTROL Vista de columna]**, **[!UICONTROL Vista de tarjeta]** o **[!UICONTROL Vista de lista]**.

   Consulte [Uso de selectores.](/help/assets/dynamic-media/working-with-selectors.md)

   ![6_5_imageset-addingassets](assets/6_5_imageset-addingassets.png)

1. Cuando se añaden recursos al conjunto, estos se añaden automáticamente en orden alfanumérico. Después de agregarlos, puede reordenar u ordenar los recursos manualmente.

   Si es necesario, arrastre el icono Reordenar de un recurso a la derecha del nombre del archivo del recurso para reordenar las imágenes hacia arriba o hacia abajo en la lista de conjunto.

   ![6_5_imageset-reorderassets](assets/6_5_imageset-reorderassets.png)

   Si desea cambiar una miniatura o muestra, haga clic en el icono **+** **miniatura** situado junto a la imagen y vaya a la miniatura o muestra que desee. Cuando termine de seleccionar todas las imágenes, haga clic en **[!UICONTROL Guardar]**.

1. (Opcional) Realice cualquiera de las siguientes acciones:

   * Para eliminar una imagen, seleccione la imagen y pulse **[!UICONTROL Eliminar recurso]**.

   * Para aplicar un ajuste preestablecido, cerca de la esquina superior derecha de la página, pulse **[!UICONTROL Ajuste preestablecido]** y, a continuación, seleccione un ajuste preestablecido para aplicar a todos los recursos a la vez.
   >[!NOTE]
   >
   >Al crear el conjunto de imágenes, puede cambiar la miniatura del conjunto de imágenes. O bien, puede dejar que el Experience Manager seleccione la miniatura automáticamente en función de los recursos del conjunto de imágenes. Para seleccionar una miniatura, pulse **[!UICONTROL Cambiar miniatura]** sobre el campo Título en la página Editor de conjuntos de imágenes. A continuación, seleccione cualquier imagen (puede navegar a otras carpetas para buscar imágenes también). Si ha seleccionado una miniatura, y luego decide que desea que el Experience Manager genere una del conjunto de imágenes, seleccione **[!UICONTROL Cambiar a]** **[!UICONTROL Miniatura automática]**.

1. Haga clic en **[!UICONTROL Guardar]**. El conjunto de imágenes recién creado aparece en la carpeta en la que lo creó.

## Visualización de conjuntos de imágenes {#viewing-image-sets}

Puede crear conjuntos de imágenes en la interfaz de usuario o automáticamente utilizando [ajustes preestablecidos de conjuntos de lotes](/help/assets/dynamic-media/batch-set-presets-dm.md).

>[!IMPORTANT]
>
>IPS [Image Production System] crea los conjuntos de lotes como parte de la ingesta de recursos.

Sin embargo, los conjuntos creados con ajustes preestablecidos de conjuntos de lotes, no *no* aparecen en la interfaz de usuario. Puede ver estos conjuntos de tres formas diferentes. (Estos métodos están disponibles aunque haya creado los conjuntos de imágenes en la interfaz de usuario).

* Abra las propiedades de un recurso. Las propiedades indican los conjuntos en los que se hace referencia al recurso seleccionado o a un miembro de . Para ver el conjunto completo, pulse el nombre del conjunto.

   ![6_5_imageset-assetproperties](assets/6_5_imageset-assetproperties.png)

* Desde una imagen de miembro de cualquier conjunto. Seleccione el menú **[!UICONTROL Conjuntos]** para mostrar los conjuntos de los que es miembro el recurso.

   ![6_5_imageset-setspulldownmenu](assets/6_5_imageset-setspulldownmenu.png)

* Desde la búsqueda, puede seleccionar **[!UICONTROL Filter]**, luego expandir **[!UICONTROL Dynamic Media]** y seleccionar **[!UICONTROL Sets]**.

   La búsqueda devuelve conjuntos coincidentes creados manualmente en la interfaz de usuario o creados automáticamente mediante ajustes preestablecidos de conjuntos de lotes. Para conjuntos automatizados, la consulta de búsqueda se realiza utilizando &quot;Comienza con&quot;. Este criterio de búsqueda es diferente del Experience Manager, que se basa en el uso de &quot;Contiene&quot;. Definir el filtro como **[!UICONTROL Sets]** es la única manera de buscar conjuntos automatizados.

   ![chlimage_1-134](assets/chlimage_1-134.png)

>[!NOTE]
>
>Puede ver los conjuntos mediante la interfaz de usuario que se describe en [Edición de conjuntos de imágenes](#editing-image-sets).

## Edición de conjuntos de imágenes {#editing-image-sets}

Puede realizar varias tareas de edición en conjuntos de imágenes, como las siguientes:

* Agregue imágenes al conjunto de imágenes.
* Reordene las imágenes en el conjunto de imágenes.
* Eliminar recursos del conjunto de imágenes.
* Aplicar ajustes preestablecidos de visor.
* Eliminar el conjunto de imágenes.

**Para editar conjuntos de imágenes**

1. Realice una de las siguientes acciones:

   * Pase el ratón sobre un recurso de conjunto de imágenes y, a continuación, pulse **[!UICONTROL Editar]** (icono de lápiz).
   * Pase el ratón sobre un recurso de conjunto de imágenes, pulse **[!UICONTROL Seleccionar]** (icono de marca de verificación) y, a continuación, pulse **[!UICONTROL Editar]** en la barra de herramientas.
   * Pulse en un recurso de conjunto de imágenes y, a continuación, pulse **[!UICONTROL Editar]** (icono de lápiz) en la barra de herramientas.

1. Para editar las imágenes del conjunto de imágenes, realice una de las acciones siguientes:

   * Para reordenar los recursos, arrastre una imagen a una nueva ubicación (seleccione el icono de reordenar para mover elementos).
   * Para ordenar los elementos en orden ascendente o descendente, haga clic en el encabezado de la columna.
   * Para agregar un recurso o actualizar un recurso existente, haga clic en **[!UICONTROL Agregar recurso]**. Vaya a un recurso, selecciónelo y pulse **[!UICONTROL Seleccionar]** cerca de la esquina superior derecha de la página.

      >[!NOTE]
      >
      >Si elimina la imagen que usa el Experience Manager para la miniatura reemplazándola por otra imagen, el recurso original seguirá apareciendo.
   * Para eliminar un recurso, selecciónelo y pulse o haga clic en **[!UICONTROL Eliminar recurso]**.
   * Para aplicar un ajuste preestablecido, cerca de la esquina superior derecha de la página, pulse **[!UICONTROL Ajuste preestablecido]** y, a continuación, seleccione un ajuste preestablecido de visualizador.
   * Para añadir o cambiar una miniatura, seleccione el icono de miniatura situado a la derecha del recurso. Vaya al nuevo recurso de muestra o miniatura, selecciónelo y pulse **[!UICONTROL Seleccionar]**.
   * Para eliminar un conjunto de imágenes completo, vaya al conjunto de imágenes, selecciónelo y pulse **[!UICONTROL Eliminar]**.

   >[!NOTE]
   >
   >Puede editar las imágenes en un conjunto de imágenes. Vaya al conjunto y pulse **[!UICONTROL Set Members]** en el carril izquierdo. Para abrir la ventana de edición, pulse el icono Lápiz en un recurso.

1. Toque **[!UICONTROL Guardar]** cuando haya terminado de editar.

## Vista previa de conjuntos de imágenes {#previewing-image-sets}

Consulte [Vista previa de recursos](/help/assets/dynamic-media/previewing-assets.md).

## Conjuntos de imágenes de publicación {#publishing-image-sets}

Consulte [Publicación de recursos](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md).
