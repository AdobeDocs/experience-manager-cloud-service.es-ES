---
title: Conjuntos de imágenes
description: Aprenda a trabajar con conjuntos de imágenes en Dynamic Media.
contentOwner: Rick Brough
feature: Image Sets
role: User
exl-id: 2eb71f24-73d9-4b5c-8605-923a0e3d1505
source-git-commit: 36ab36ba7e14962eba3947865545b8a3f29f6bbc
workflow-type: tm+mt
source-wordcount: '2145'
ht-degree: 4%

---

# Conjuntos de imágenes {#image-sets}

Los conjuntos de imágenes proporcionan a los usuarios una experiencia de visualización integrada, en la que pueden ver diferentes vistas de un elemento haciendo clic en una imagen en miniatura. Los conjuntos de imágenes permiten presentar vistas alternativas de un elemento y el visor ofrece herramientas de zoom para examinar las imágenes de cerca.

Los conjuntos de imágenes se designan mediante una pancarta con la palabra `IMAGESET`. Además, si se publica el conjunto de imágenes, se mostrará en el titular la fecha de publicación, indicada por el icono **[!UICONTROL Mundo]**. Además, se muestra la fecha de la última modificación, indicada por el icono **[!UICONTROL Lápiz]**.

![chlimage_1-133](assets/chlimage_1-339.png)

Dentro del conjunto de imágenes, también puede crear muestras creando un conjunto de imágenes y añadiendo miniaturas.

Esta aplicación es útil para cuando desea mostrar un elemento en un color, patrón o acabado diferente. Para crear un conjunto de imágenes con muestras de color, necesita una imagen para cada color, trama o acabado diferente que desee presentar a los usuarios. También necesita una muestra de color, trama o acabado para cada color, trama o acabado.

Por ejemplo, supongamos que desea presentar imágenes de mayúsculas con diferentes listas de colores; las listas son rojas, verdes y azules. En este caso, necesitas tres inyecciones de la misma gorra. Necesitas un tiro con un rojo, uno con un verde, y uno con un pico azul. También necesita una muestra de color rojo, verde y azul. Las muestras de color sirven como miniaturas en las que los usuarios hacen clic en el Visor de conjuntos de muestras para ver el límite rojo, verde o azul.

>[!NOTE]
>
>Para obtener información sobre la interfaz de usuario de Assets, consulte [Administrar recursos con la IU táctil](/help/assets/manage-digital-assets.md).

Al crear un conjunto de imágenes, Adobe recomienda las siguientes prácticas recomendadas y aplica los límites siguientes:

| Tipo de límite | Práctica recomendada | Límite impuesto |
| --- | --- | --- |
| Número de recursos duplicados por conjunto | No hay duplicados | 20 |
| Número máximo de imágenes por conjunto | 5-10 imágenes por conjunto | 1000 |

Consulte también [Limitaciones de Dynamic Media](/help/assets/dynamic-media/limitations.md).

## Inicio rápido: Conjuntos de imágenes {#quick-start-image-sets}

Para ponerse en marcha rápidamente:

1. Opcional. [Cree un ajuste preestablecido de conjunto por lotes](/help/assets/dynamic-media/batch-set-presets-dm.md) y aplíquelo a una carpeta nueva en la que se carguen las imágenes del conjunto de giros.

   Un ajuste preestablecido de conjunto por lotes puede ayudarle a automatizar la creación del conjunto de imágenes.

   >[!IMPORTANT]
   >
   >IPS (Image Production System) crea los conjuntos de lotes como parte de la ingesta de recursos.

1. [Cargue sus imágenes de origen principales para varias vistas](#uploading-assets-in-image-sets).

   Cargue las imágenes para los conjuntos de imágenes. Recuerde que los usuarios pueden aplicar zoom a las imágenes en el Visor de conjuntos de imágenes. Como tal, elija sus imágenes cuidadosamente. Asegúrese de que las imágenes tengan al menos 2000 píxeles del tamaño más grande.

   Consulte [Dynamic Media - Formatos de imagen rasterizada admitidos](/help/assets/file-format-support.md#image-support-dynamic-media) para obtener una lista de los formatos admitidos por los conjuntos de imágenes.

1. [Crear conjuntos de imágenes](#creating-image-sets).

   En los conjuntos de imágenes, los usuarios hacen clic en imágenes en miniatura en el Visor de conjuntos de imágenes.

   Para crear un conjunto de imágenes en Assets, seleccione **[!UICONTROL Crear]** > **[!UICONTROL Conjuntos de imágenes]**. A continuación, agrega imágenes y haz clic en **[!UICONTROL Guardar]**.

   Consulte [Preparar recursos de conjuntos de imágenes para cargar y cargar sus archivos](#uploading-assets-in-image-sets).

   Consulte [Trabajar con selectores](/help/assets/dynamic-media/working-with-selectors.md).

1. Agregue [ajustes preestablecidos del visualizador de conjuntos de imágenes](/help/assets/dynamic-media/managing-viewer-presets.md), según sea necesario.

   Los administradores pueden crear o modificar ajustes preestablecidos del visualizador de conjuntos de imágenes. Para ver tu conjunto de imágenes con un ajuste preestablecido de visor, selecciona el conjunto de imágenes y en la lista desplegable del carril izquierdo, selecciona **[!UICONTROL Visualizadores]**.

   Para crear o editar ajustes preestablecidos de visor, consulte **[!UICONTROL Herramientas]** > **[!UICONTROL Assets]** > **[!UICONTROL Ajustes preestablecidos de visor]**.

1. (Opcional) [Ver conjuntos de imágenes](/help/assets/dynamic-media/image-sets.md#viewing-image-sets) creados con ajustes preestablecidos de conjuntos de lotes.
1. [Previsualizar conjuntos de imágenes](/help/assets/dynamic-media/previewing-assets.md).

   Seleccione el conjunto de imágenes y podrá previsualizarlo. Para examinar el conjunto de imágenes en el visor seleccionado, seleccione los iconos de miniaturas. Puede elegir diferentes visores en el menú **[!UICONTROL Visualizadores]**, disponible en la lista desplegable del carril izquierdo.

1. [Publicar conjuntos de imágenes](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md).

   La publicación de un conjunto de imágenes activa la URL y la cadena de incrustación. Además, debe [publicar cualquier ajuste preestablecido de visor personalizado](/help/assets/dynamic-media/managing-viewer-presets.md) que haya creado. Los ajustes preestablecidos de visualizador listos para usar ya se han publicado.

1. [Vincular direcciones URL a la aplicación web](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md) o [Incrustar el visor de vídeo o de imágenes](/help/assets/dynamic-media/embed-code.md).

   Experience Manager Assets crea llamadas de URL para conjuntos de imágenes y las activa después de publicar los conjuntos de imágenes. Puede copiar estas direcciones URL al previsualizar los recursos. También puede incrustarlos en el sitio web.

   Seleccione el conjunto de imágenes y, a continuación, en la lista desplegable del carril izquierdo, seleccione **[!UICONTROL Visualizadores]**.

   Ver [Vincular un conjunto de imágenes a una página web](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md) e [Incrustar el visor de imágenes o vídeos](/help/assets/dynamic-media/embed-code.md).

Para editar conjuntos de imágenes, consulte [editar conjuntos de imágenes](#editing-image-sets). Además, puede ver y editar [propiedades del conjunto de imágenes](/help/assets/manage-digital-assets.md#editing-properties).

Si tiene problemas al crear conjuntos, consulte Imágenes y conjuntos en [Solucionar problemas de Dynamic Media](/help/assets/dynamic-media/troubleshoot-dm.md#images-and-sets).

## Cargar recursos para conjuntos de imágenes {#uploading-assets-in-image-sets}

Comience por cargar los recursos de imagen de los conjuntos de imágenes. Recuerde que los usuarios pueden aplicar zoom a las imágenes en el Visor de conjuntos de imágenes. Como tal, elija sus imágenes cuidadosamente. Asegúrese de que las imágenes tengan al menos 2000 píxeles de tamaño más grande para obtener un detalle de zoom óptimo. Dynamic Media puede procesar imágenes de hasta 25 megapíxeles cada una. Por ejemplo, puede utilizar una imagen de 5000 x 5000 megapíxeles o cualquier otra combinación de tamaño de hasta 25 megapíxeles.

<!-- Image Sets supports many image file formats, but lossless TIFF, PNG, and EPS images are recommended. -->

Consulte [Dynamic Media - Formatos de imagen rasterizada admitidos](/help/assets/file-format-support.md#image-support-dynamic-media) para obtener una lista de los formatos admitidos por los conjuntos de imágenes.

Puede cargar imágenes para conjuntos de imágenes del mismo modo que [cargaría cualquier otro recurso en Assets](/help/assets/manage-digital-assets.md#uploading-assets).

### Preparar recursos del conjunto de imágenes para cargar {#preparing-image-set-assets-for-upload}

Antes de crear conjuntos de imágenes, asegúrese de que las imágenes tengan el tamaño y el formato correctos.

Para crear un conjunto de imágenes de varias vistas, necesita imágenes que muestren un elemento desde diferentes puntos de vista o que muestren diferentes aspectos del mismo elemento. El objetivo es resaltar las características importantes de un elemento para que los espectadores tengan una imagen completa de cómo aparece o qué hace.

Dado que los usuarios pueden ampliar las imágenes en conjuntos de imágenes, asegúrese de que las imágenes tengan un tamaño mayor de al menos 2000 píxeles. Experience Manager Assets admite muchos formatos de archivo de imagen, pero se recomiendan imágenes de TIFF, PNG y EPS sin pérdidas.

>[!NOTE]
>
>Si utiliza miniaturas para indicar muestras de productos, haga lo siguiente:
>
>Cree viñetas o diferentes tomas de la misma imagen mostrándola en diferentes colores, patrones o acabados. También necesita archivos de miniaturas que se correspondan con los diferentes colores, motivos o acabados. Por ejemplo, para presentar miniaturas con un conjunto de imágenes que muestre la misma chaqueta en negro, marrón y verde, necesitará:
>
>* Un tiro negro, marrón y verde de la misma chaqueta.
>* Miniatura en color negro, marrón y verde.

## Crear conjuntos de imágenes {#creating-image-sets}

Puede crear conjuntos de imágenes a través de la interfaz de usuario o mediante la API.

>[!NOTE]
>
>También puede crear conjuntos de imágenes automáticamente mediante [ajustes preestablecidos de conjuntos de lotes](/help/assets/dynamic-media/batch-set-presets-dm.md).
>**Importante: IPS (Image Production System) crea** conjuntos de lotes como parte de la ingesta de recursos.

Al agregar recursos al conjunto, estos se agregan automáticamente en orden alfanumérico. Puede reordenar u ordenar manualmente los recursos una vez añadidos.

>[!NOTE]
>
>No se admiten conjuntos de imágenes para recursos con &quot;,&quot; (coma) en el nombre del archivo.

Al crear un conjunto de imágenes, Adobe recomienda las siguientes prácticas recomendadas y aplica los límites siguientes:

| Tipo de límite | Práctica recomendada | Límite impuesto |
| --- | --- | --- |
| Número de recursos duplicados por conjunto | No hay duplicados | 20 |
| Número máximo de imágenes por conjunto | 5-10 imágenes por conjunto | 1000 |

Consulte también [Limitaciones de Dynamic Media](/help/assets/dynamic-media/limitations.md).

**Para crear conjuntos de imágenes:**

1. En Adobe Experience Manager, seleccione el logotipo de Experience Manager para acceder a la consola de navegación global.
1. Seleccione **[!UICONTROL Navegación]** > **[!UICONTROL Assets]**. Vaya a donde desee crear un conjunto de imágenes y, a continuación, vaya a **[!UICONTROL Crear]** > **[!UICONTROL Conjunto de imágenes]** para abrir la página Editor de conjuntos de imágenes.

   También puede crear el conjunto desde una carpeta que contenga los recursos.

   ![6_5_imagesets-createpulldown](assets/6_5_imagesets-createpulldown.png)

1. En la página Editor de conjuntos de imágenes, en el campo **[!UICONTROL Título]**, escriba un nombre para el conjunto de imágenes. El nombre aparece en el titular en todo el conjunto de imágenes. Si lo desea, introduzca una descripción.

   ![6_5_imageset-creatingnewset](assets/6_5_imageset-creatingnewset.png)

1. Realice una de las siguientes acciones:

   * Cerca de la esquina superior izquierda de la página Editor de conjuntos de imágenes, seleccione **[!UICONTROL Agregar recurso]**.

   * Cerca de la mitad de la página Editor de conjuntos de imágenes, seleccione **[!UICONTROL Toque para abrir el Selector de recursos]**.

   Seleccione para seleccionar los recursos que desea incluir en el conjunto de imágenes. Los recursos seleccionados tienen un icono de marca de verificación sobre ellos. Cuando termine, cerca de la esquina superior derecha de la página, seleccione **[!UICONTROL Seleccionar]**.

   Con el Selector de recursos, puede buscar recursos escribiendo una palabra clave y seleccionando **[!UICONTROL Retorno]**. También puede aplicar filtros para restringir los resultados de búsqueda. Puede filtrar por ruta, colección, tipo de archivo y etiqueta. Seleccione el filtro y, a continuación, seleccione el icono **[!UICONTROL Filtro]** en la barra de herramientas. Para cambiar la vista, selecciona el icono Ver y selecciona **[!UICONTROL Vista de columna]**, **[!UICONTROL Vista de tarjeta]** o **[!UICONTROL Vista de lista]**.

   Consulte [Uso de selectores](/help/assets/dynamic-media/working-with-selectors.md).

   ![6_5_imageset-addingassets](assets/6_5_imageset-addingassets.png)

1. Al agregar recursos al conjunto, estos se agregan automáticamente en orden alfanumérico. Puede reordenar u ordenar manualmente los recursos después de agregarlos.

   Si es necesario, arrastre el icono Reordenar de un recurso a la derecha del nombre de archivo del recurso para reordenar las imágenes hacia arriba o hacia abajo en la lista de conjuntos.

   ![6_5_imageset-reorderassets](assets/6_5_imageset-reorderassets.png)

   Si desea cambiar una miniatura o muestra, haga clic en el icono **+** **miniatura** situado junto a la imagen y vaya a la miniatura o muestra que desee. Cuando termine de seleccionar todas las imágenes, haga clic en **[!UICONTROL Guardar]**.

1. (Opcional) Realice una de las siguientes acciones:

   * Para eliminar una imagen, seleccione la imagen y seleccione **[!UICONTROL Eliminar recurso]**.

   * Para aplicar un ajuste preestablecido, cerca de la esquina superior derecha de la página, seleccione **[!UICONTROL Ajuste preestablecido]** y, a continuación, seleccione un ajuste preestablecido para aplicar a todos los recursos a la vez.

   >[!NOTE]
   >
   >Al crear el conjunto de imágenes, puede cambiar la miniatura del conjunto de imágenes. O bien, puede permitir que Experience Manager seleccione la miniatura automáticamente en función de los recursos del conjunto de imágenes. Para seleccionar una miniatura, seleccione **[!UICONTROL Cambiar miniatura]** encima del campo Título en la página Editor de conjuntos de imágenes. A continuación, seleccione cualquier imagen (puede navegar a otras carpetas para buscar imágenes también). Si seleccionó una miniatura y, a continuación, decide que Experience Manager debe generar una del conjunto de imágenes, seleccione **[!UICONTROL Cambiar a]** **[!UICONTROL Miniatura automática]**.

1. Haga clic en **[!UICONTROL Guardar]**. El conjunto de imágenes creado aparecerá en la carpeta en la que lo creó.

## Ver conjuntos de imágenes {#viewing-image-sets}

Puede crear conjuntos de imágenes en la interfaz de usuario o automáticamente mediante [ajustes preestablecidos de conjunto por lotes](/help/assets/dynamic-media/batch-set-presets-dm.md).

>[!IMPORTANT]
>
>IPS [Image Production System] crea los conjuntos de lotes como parte de la ingesta de recursos.

Sin embargo, los conjuntos creados mediante ajustes preestablecidos de conjuntos de lotes, *no* aparecen en la interfaz de usuario. Puede ver estos conjuntos de tres formas diferentes. (Estos métodos están disponibles aunque haya creado los conjuntos de imágenes en la interfaz de usuario).

* Abra las propiedades de un recurso. Las propiedades indican qué conjuntos hacen referencia al recurso seleccionado o de qué es miembro. Para ver el conjunto completo, seleccione el nombre del conjunto.

  ![6_5_imageset-assetproperties](assets/6_5_imageset-assetproperties.png)

* Desde una imagen de miembro de cualquier conjunto. Seleccione el menú **[!UICONTROL Conjuntos]** para mostrar los conjuntos de los que es miembro el recurso.

  ![6_5_imageset-setspulldownmenu](assets/6_5_imageset-setspulldownmenu.png)

* Desde la búsqueda, puede seleccionar **[!UICONTROL Filter]**, luego expandir **[!UICONTROL Dynamic Media]** y seleccionar **[!UICONTROL Conjuntos]**.

  La búsqueda devuelve conjuntos coincidentes creados manualmente en la interfaz de usuario o creados automáticamente mediante ajustes preestablecidos de conjuntos de lotes. Para los conjuntos automatizados, la consulta de búsqueda se realiza utilizando &quot;Comienza con&quot;. Este criterio de búsqueda es diferente del de Experience Manager, que se basa en el uso de &quot;Contiene&quot;. Establecer el filtro en **[!UICONTROL Conjuntos]** es la única manera de buscar conjuntos automatizados.

  ![chlimage_1-134](assets/chlimage_1-134.png)

>[!NOTE]
>
>Puede ver los conjuntos mediante la interfaz de usuario como se describe en [Edición de conjuntos de imágenes](#editing-image-sets).

## Editar conjuntos de imágenes {#editing-image-sets}

Puede realizar varias tareas de edición en conjuntos de imágenes, como las siguientes:

* Agregar imágenes al conjunto de imágenes.
* Reordene las imágenes del conjunto de imágenes.
* Eliminar recursos del conjunto de imágenes.
* Aplicar ajustes preestablecidos de visor.
* Elimine el conjunto de imágenes.

**Para editar conjuntos de imágenes:**

1. Realice una de las siguientes acciones:

   * Pase el ratón sobre un recurso del conjunto de imágenes y seleccione **[!UICONTROL Editar]** (icono de lápiz).
   * Pase el ratón sobre un recurso de conjunto de imágenes, seleccione **[!UICONTROL Seleccionar]** (icono de marca de verificación) y, a continuación, seleccione **[!UICONTROL Editar]** en la barra de herramientas.
   * Seleccione en un recurso de conjunto de imágenes y, a continuación, seleccione **[!UICONTROL Editar]** (icono de lápiz) en la barra de herramientas.

1. Para editar las imágenes del conjunto de imágenes, realice una de las siguientes acciones:

   * Para reordenar los recursos, arrastre una imagen a una nueva ubicación (seleccione el icono de reordenar para mover los elementos).
   * Para ordenar los elementos en orden ascendente o descendente, haga clic en el encabezado de la columna.
   * Para agregar un recurso o actualizar un recurso existente, haga clic en **[!UICONTROL Agregar recurso]**. Vaya a un recurso, selecciónelo y, a continuación, seleccione **[!UICONTROL Seleccionar]** cerca de la esquina superior derecha de la página.

     >[!NOTE]
     >
     >Si elimina la imagen que Experience Manager utiliza para la miniatura reemplazándola por otra imagen, se seguirá mostrando el recurso original.
   * Para eliminar un recurso, selecciónelo y seleccione **[!UICONTROL Eliminar recurso]**.
   * Para aplicar un ajuste preestablecido, cerca de la esquina superior derecha de la página, seleccione **[!UICONTROL Ajuste preestablecido]** y, a continuación, seleccione un ajuste preestablecido de visor.
   * Para añadir o cambiar una miniatura, seleccione el icono de miniatura situado junto a la derecha del recurso. Vaya a la nueva miniatura o recurso de muestra, selecciónelo y, a continuación, seleccione **[!UICONTROL Seleccionar]**.
   * Para eliminar un conjunto de imágenes completo, ve al conjunto de imágenes, selecciónalo y selecciona **[!UICONTROL Eliminar]**.

   >[!NOTE]
   >
   >Puede editar las imágenes de un conjunto de imágenes. Vaya al conjunto y seleccione **[!UICONTROL Definir miembros]** en el carril izquierdo. Para abrir la ventana de edición, seleccione el icono Lápiz en un recurso.

1. Seleccione **[!UICONTROL Guardar]** cuando haya terminado de editar.

## Previsualizar conjuntos de imágenes {#previewing-image-sets}

Consulte [Vista previa de recursos](/help/assets/dynamic-media/previewing-assets.md).

## Publicación de conjuntos de imágenes {#publishing-image-sets}

Ver [Publicar Assets](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md).
