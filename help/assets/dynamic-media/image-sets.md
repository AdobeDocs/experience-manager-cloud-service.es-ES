---
title: Conjuntos de imágenes
description: Aprenda a trabajar con conjuntos de imágenes en Dynamic Media.
feature: Image Sets
role: User
exl-id: 2eb71f24-73d9-4b5c-8605-923a0e3d1505
source-git-commit: a2bbc64051214efa83d74d414e2e5f1407433127
workflow-type: tm+mt
source-wordcount: '2135'
ht-degree: 5%

---

# Conjuntos de imágenes {#image-sets}

Los conjuntos de imágenes proporcionan a los usuarios una experiencia de visualización integrada, en la que los usuarios pueden ver distintas vistas de un elemento haciendo clic en una imagen en miniatura. Los conjuntos de imágenes permiten presentar vistas alternativas de un elemento y el visor ofrece herramientas de zoom para examinar las imágenes con mayor detenimiento.

Los conjuntos de imágenes se designan mediante una pancarta con la palabra `IMAGESET`. Además, si se publica el conjunto de imágenes, la fecha de publicación, indicada por la variable **[!UICONTROL World]** en el banner. Además, la fecha de la última modificación, indicada por la variable **[!UICONTROL Lápiz]** , aparece.

![chlimage_1-133](assets/chlimage_1-339.png)

Dentro del conjunto de imágenes, también puede crear muestras creando un conjunto de imágenes y agregando miniaturas.

Esta aplicación es útil para cuando desea mostrar un elemento en un color, patrón o acabado diferentes. Para crear un conjunto de imágenes con muestras de color, necesita una imagen para cada color, patrón o acabado diferente que desee presentar a los usuarios. También necesita una muestra de color, patrón o fin para cada color, patrón o acabado.

Por ejemplo, supongamos que desea presentar imágenes de mayúsculas con diferentes listas de colores; los billetes son rojo, verde y azul. En este caso, se necesitan tres tomas de la misma tapa. Necesitas un tiro con un rojo, uno con un verde y otro con un billete azul. También necesita una muestra de color rojo, verde y azul. Las muestras de color sirven como miniaturas en las que los usuarios hacen clic en el Visor de conjuntos de muestras para ver el gorro de facturación roja, verde o azul.

>[!NOTE]
>
>Para obtener información sobre la interfaz de usuario de Assets, consulte [Administrar recursos con la interfaz de usuario táctil](/help/assets/manage-digital-assets.md).

Al crear un conjunto de imágenes, Adobe recomienda las siguientes prácticas recomendadas y aplica los límites siguientes:

| Tipo de límite | Práctica recomendada | Límite impuesto |
| --- | --- | --- |
| Número de activos duplicados por conjunto | Sin duplicados | 20 |
| Número máximo de imágenes por conjunto | 5 a 10 imágenes por conjunto | 1000 |

Consulte también [Limitaciones de Dynamic Media](/help/assets/dynamic-media/limitations.md).

## Inicio rápido: Conjuntos de imágenes {#quick-start-image-sets}

Para ponerle en marcha rápidamente:

1. Opcional. [Crear un ajuste preestablecido de conjunto de lotes](/help/assets/dynamic-media/batch-set-presets-dm.md) y aplicarlo a una nueva carpeta donde se carguen las imágenes del conjunto de giros.

   Un ajuste preestablecido de conjunto de lotes puede ayudarle a automatizar la creación del conjunto de imágenes.

   >[!IMPORTANT]
   >
   >IPS (Image Production System) crea los conjuntos de lotes como parte de la ingesta de recursos.

1. [Cargar las imágenes de origen principales para varias vistas](#uploading-assets-in-image-sets).

   Cargue las imágenes para sus conjuntos de imágenes. Recuerde que los usuarios pueden hacer zoom en las imágenes en el visor de conjuntos de imágenes. Como tal, elija sus imágenes con cuidado. Asegúrese de que las imágenes tengan al menos 2000 píxeles en el tamaño más grande.

   Consulte [Dynamic Media: formatos de imagen de trama compatibles](/help/assets/file-format-support.md#image-support-dynamic-media) para obtener una lista de los formatos admitidos por los conjuntos de imágenes.

1. [Crear conjuntos de imágenes](#creating-image-sets).

   En los conjuntos de imágenes, los usuarios hacen clic en las imágenes en miniatura en el visor de conjuntos de imágenes.

   Para crear un conjunto de imágenes en Assets, seleccione **[!UICONTROL Crear]** > **[!UICONTROL Conjuntos de imágenes]**. A continuación, añada imágenes y haga clic en **[!UICONTROL Guardar]**.

   Consulte [Preparación de recursos de conjuntos de imágenes para cargarlos y carga de archivos](#uploading-assets-in-image-sets).

   Consulte [Trabajar con selectores](/help/assets/dynamic-media/working-with-selectors.md).

1. Agregar [Ajustes preestablecidos del visualizador de conjuntos de imágenes](/help/assets/dynamic-media/managing-viewer-presets.md), según sea necesario.

   Los administradores pueden crear o modificar ajustes preestablecidos de visualizador de conjuntos de imágenes. Para ver el conjunto de imágenes con un ajuste preestablecido de visualizador, seleccione el conjunto de imágenes y, en la lista desplegable del carril izquierdo, seleccione **[!UICONTROL Visualizadores]**.

   Para crear o editar ajustes preestablecidos de visualizador, consulte **[!UICONTROL Herramientas]** > **[!UICONTROL Recursos]** > **[!UICONTROL Ajustes preestablecidos de visor]**.

1. (Opcional) [Ver conjuntos de imágenes](/help/assets/dynamic-media/image-sets.md#viewing-image-sets) que se crearon mediante ajustes preestablecidos de conjuntos de lotes.
1. [Vista previa de conjuntos de imágenes](/help/assets/dynamic-media/previewing-assets.md).

   Seleccione el conjunto de imágenes y podrá previsualizarlo. Para examinar el conjunto de imágenes en el visor seleccionado, seleccione los iconos de miniaturas. Puede elegir diferentes visualizadores del **[!UICONTROL Visualizadores]** , disponible en la lista desplegable del carril izquierdo.

1. [Publicar conjuntos de imágenes](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md).

   Al publicar un conjunto de imágenes, se activa la dirección URL y la cadena de incrustación. Además, debe [publicar cualquier ajuste preestablecido de visor personalizado](/help/assets/dynamic-media/managing-viewer-presets.md) que haya creado. Ya se han publicado los ajustes preestablecidos del visor integrado.

1. [Vincular URL a la aplicación web](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md) o [Incrustar el visualizador de imágenes o vídeos](/help/assets/dynamic-media/embed-code.md).

   Experience Manager Assets crea llamadas de URL para conjuntos de imágenes y los activa después de publicar los conjuntos de imágenes. Puede copiar estas direcciones URL cuando obtiene una vista previa de los recursos. También puede incrustarlos en el sitio web.

   Seleccione el conjunto de imágenes y, a continuación, en la lista desplegable del carril izquierdo, seleccione **[!UICONTROL Visualizadores]**.

   Consulte [Vinculación de un conjunto de imágenes a una página web](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md) y [Incrustar el visualizador de imágenes o vídeos](/help/assets/dynamic-media/embed-code.md).

Para editar los conjuntos de imágenes, consulte [edición de conjuntos de imágenes](#editing-image-sets). Además, puede ver y editar [Propiedades del conjunto de imágenes](/help/assets/manage-digital-assets.md#editing-properties).

Si tiene problemas para crear conjuntos, consulte Imágenes y conjuntos en [Resolución de problemas de Dynamic Media](/help/assets/dynamic-media/troubleshoot-dm.md#images-and-sets).

## Cargar recursos para conjuntos de imágenes {#uploading-assets-in-image-sets}

Comience por cargar los recursos de imagen para los conjuntos de imágenes. Recuerde que los usuarios pueden hacer zoom en las imágenes en el visor de conjuntos de imágenes. Como tal, elija sus imágenes con cuidado. Asegúrese de que las imágenes tengan al menos 2000 píxeles en el tamaño más grande para obtener un detalle de zoom óptimo. Dynamic Media puede procesar imágenes de hasta 25 megapíxeles cada una. Por ejemplo, puede utilizar una imagen de 5000 x 5000 megapíxeles o cualquier otra combinación de tamaño de hasta 25 megapíxeles.

<!-- Image Sets supports many image file formats, but lossless TIFF, PNG, and EPS images are recommended. -->

Consulte [Dynamic Media: formatos de imagen de trama compatibles](/help/assets/file-format-support.md#image-support-dynamic-media) para obtener una lista de los formatos admitidos por los conjuntos de imágenes.

Puede cargar imágenes para conjuntos de imágenes del modo que lo haría [cargar cualquier otro recurso en Assets](/help/assets/manage-digital-assets.md#uploading-assets).

### Preparación de recursos de conjuntos de imágenes para su carga {#preparing-image-set-assets-for-upload}

Antes de crear conjuntos de imágenes, asegúrese de que las imágenes tengan el tamaño y el formato adecuados.

Para crear un conjunto de imágenes de varias vistas, necesita imágenes que muestren un elemento desde diferentes puntos de vista o que muestren diferentes aspectos del mismo elemento. El objetivo es resaltar las características importantes de un elemento para que los espectadores tengan una imagen completa de cómo aparece o qué hace.

Dado que los usuarios pueden hacer zoom en las imágenes en los conjuntos de imágenes, asegúrese de que las imágenes tengan al menos 2000 píxeles en el tamaño más grande. Experience Manager Assets admite muchos formatos de archivo de imagen, pero se recomiendan las imágenes TIFF, PNG y EPS sin pérdida.

>[!NOTE]
>
>Si utiliza miniaturas para indicar muestras de productos, haga lo siguiente:
>
>Cree viñetas o tomas diferentes de la misma imagen mostrándola en diferentes colores, patrones o acabados. También necesita archivos en miniatura que correspondan a los diferentes colores, patrones o acabados. Por ejemplo, para presentar miniaturas con un conjunto de imágenes que muestre la misma chaqueta en negro, marrón y verde, necesitará:
>
>* Un tiro negro, marrón y verde de la misma chaqueta.
>* Miniatura de color negro, marrón y verde.


## Crear conjuntos de imágenes {#creating-image-sets}

Puede crear conjuntos de imágenes a través de la interfaz de usuario o mediante la API.

>[!NOTE]
>
>También puede crear conjuntos de imágenes automáticamente mediante [ajustes preestablecidos de conjuntos de lotes](/help/assets/dynamic-media/batch-set-presets-dm.md).
>**Importante:** IPS (Image Production System) crea los conjuntos de lotes como parte de la ingesta de recursos.

Cuando se añaden recursos al conjunto, estos se añaden automáticamente en orden alfanumérico. Puede reordenar u ordenar manualmente los recursos una vez añadidos.

>[!NOTE]
>
>Los conjuntos de imágenes no son compatibles con los recursos con &quot;,&quot; (coma) en el nombre de archivo.

Al crear un conjunto de imágenes, Adobe recomienda las siguientes prácticas recomendadas y aplica los límites siguientes:

| Tipo de límite | Práctica recomendada | Límite impuesto |
| --- | --- | --- |
| Número de activos duplicados por conjunto | Sin duplicados | 20 |
| Número máximo de imágenes por conjunto | 5 a 10 imágenes por conjunto | 1000 |

Consulte también [Limitaciones de Dynamic Media](/help/assets/dynamic-media/limitations.md).

**Para crear conjuntos de imágenes:**

1. En Adobe Experience Manager, seleccione el logotipo del Experience Manager para acceder a la consola de navegación global.
1. Toque **[!UICONTROL Navegación]** > **[!UICONTROL Recursos]**. Vaya a donde desea crear un conjunto de imágenes y, a continuación, vaya a **[!UICONTROL Crear]** > **[!UICONTROL Conjunto de imágenes]** para abrir la página Editor de conjuntos de imágenes.

   También puede crear el conjunto desde una carpeta que contenga los recursos.

   ![6_5_imagesets-createpulldown](assets/6_5_imagesets-createpulldown.png)

1. En la página Editor de conjuntos de imágenes , en la **[!UICONTROL Título]** , introduzca un nombre para el conjunto de imágenes. El nombre aparece en el banner del conjunto de imágenes. De forma opcional, introduzca una descripción.

   ![6_5_imageset-creatingnewset](assets/6_5_imageset-creatingnewset.png)

1. Realice una de las siguientes acciones:

   * Cerca de la esquina superior izquierda de la página Editor de conjuntos de imágenes, seleccione **[!UICONTROL Agregar recurso]**.

   * Cerca del centro de la página Editor de conjuntos de imágenes, seleccione **[!UICONTROL Toque para abrir el Selector de recursos]**.
   Pulse para seleccionar los recursos que desea incluir en el conjunto de imágenes. Los recursos seleccionados tienen un icono de marca de verificación sobre ellos. Cuando termine, cerca de la esquina superior derecha de la página, seleccione **[!UICONTROL Select]**.

   Con el Selector de recursos, puede buscar recursos escribiendo una palabra clave y seleccionando **[!UICONTROL Devuelve]**. También puede aplicar filtros para restringir los resultados de búsqueda. Puede filtrar por ruta, colección, tipo de archivo y etiqueta. Seleccione el filtro y, a continuación, el **[!UICONTROL Filtro]** en la barra de herramientas. Para cambiar la vista, seleccione el icono Ver y seleccione **[!UICONTROL Vista de columna]**, **[!UICONTROL Vista de tarjeta]** o **[!UICONTROL Vista de lista]**.

   Consulte [Uso de selectores](/help/assets/dynamic-media/working-with-selectors.md).

   ![6_5_imageset-addingassets](assets/6_5_imageset-addingassets.png)

1. Cuando se añaden recursos al conjunto, estos se añaden automáticamente en orden alfanumérico. Después de agregarlos, puede reordenar u ordenar los recursos manualmente.

   Si es necesario, arrastre el icono Reordenar de un recurso a la derecha del nombre del archivo del recurso para reordenar las imágenes hacia arriba o hacia abajo en la lista de conjunto.

   ![6_5_imageset-reorderassets](assets/6_5_imageset-reorderassets.png)

   Si desea cambiar una miniatura o muestra, haga clic en el icono **+** **miniatura** situado junto a la imagen y vaya a la miniatura o muestra que desee. Cuando termine de seleccionar todas las imágenes, haga clic en **[!UICONTROL Guardar]**.

1. (Opcional) Realice cualquiera de las siguientes acciones:

   * Para eliminar una imagen, seleccione la imagen y seleccione **[!UICONTROL Eliminar recurso]**.

   * Para aplicar un ajuste preestablecido, cerca de la esquina superior derecha de la página, seleccione **[!UICONTROL Ajuste preestablecido]** y, a continuación, seleccione un ajuste preestablecido para aplicarlo a todos los recursos a la vez.
   >[!NOTE]
   >
   >Al crear el conjunto de imágenes, puede cambiar la miniatura del conjunto de imágenes. O bien, puede dejar que el Experience Manager seleccione la miniatura automáticamente en función de los recursos del conjunto de imágenes. Para seleccionar una miniatura, seleccione **[!UICONTROL Cambiar miniatura]** encima del campo Título en la página Editor de conjuntos de imágenes . A continuación, seleccione cualquier imagen (puede navegar a otras carpetas para buscar imágenes también). Si ha seleccionado una miniatura y, a continuación, decide que desea que el Experience Manager genere una del conjunto de imágenes, seleccione **[!UICONTROL Cambie a]** **[!UICONTROL Miniatura automática]**.

1. Haga clic en **[!UICONTROL Guardar]**. El conjunto de imágenes recién creado aparece en la carpeta en la que lo creó.

## Ver conjuntos de imágenes {#viewing-image-sets}

Puede crear conjuntos de imágenes en la interfaz de usuario o automáticamente mediante [ajustes preestablecidos de conjuntos de lotes](/help/assets/dynamic-media/batch-set-presets-dm.md).

>[!IMPORTANT]
>
>IPS crea los conjuntos de lotes [Sistema de producción de imágenes] como parte de la ingesta de recursos.

Sin embargo, los conjuntos creados con ajustes preestablecidos de conjuntos de lotes, *not* aparece en la interfaz de usuario. Puede ver estos conjuntos de tres formas diferentes. (Estos métodos están disponibles aunque haya creado los conjuntos de imágenes en la interfaz de usuario).

* Abra las propiedades de un recurso. Las propiedades indican los conjuntos en los que se hace referencia al recurso seleccionado o a un miembro de . Para ver el conjunto completo, seleccione el nombre del conjunto.

   ![6_5_imageset-assetproperties](assets/6_5_imageset-assetproperties.png)

* Desde una imagen de miembro de cualquier conjunto. Seleccione el **[!UICONTROL Conjuntos]** para mostrar los conjuntos de los que es miembro el recurso.

   ![6_5_imageset-setspulldownmenu](assets/6_5_imageset-setspulldownmenu.png)

* Desde la búsqueda, puede seleccionar **[!UICONTROL Filtro]** y, a continuación, expanda **[!UICONTROL Dynamic Media]** y seleccione **[!UICONTROL Conjuntos]**.

   La búsqueda devuelve conjuntos coincidentes creados manualmente en la interfaz de usuario o creados automáticamente mediante ajustes preestablecidos de conjuntos de lotes. Para conjuntos automatizados, la consulta de búsqueda se realiza utilizando &quot;Comienza con&quot;. Este criterio de búsqueda es diferente del Experience Manager, que se basa en el uso de &quot;Contiene&quot;. Configuración del filtro en **[!UICONTROL Conjuntos]** es la única forma de buscar conjuntos automatizados.

   ![chlimage_1-134](assets/chlimage_1-134.png)

>[!NOTE]
>
>Puede ver los conjuntos mediante la interfaz de usuario, tal como se describe en [Edición de conjuntos de imágenes](#editing-image-sets).

## Editar conjuntos de imágenes {#editing-image-sets}

Puede realizar varias tareas de edición en conjuntos de imágenes, como las siguientes:

* Agregue imágenes al conjunto de imágenes.
* Reordene las imágenes en el conjunto de imágenes.
* Eliminar recursos del conjunto de imágenes.
* Aplicar ajustes preestablecidos de visor.
* Eliminar el conjunto de imágenes.

**Para editar conjuntos de imágenes:**

1. Realice una de las siguientes acciones:

   * Pase el ratón sobre un recurso de conjunto de imágenes y, a continuación, seleccione **[!UICONTROL Editar]** (icono de lápiz).
   * Pase el ratón sobre un recurso de conjunto de imágenes y seleccione **[!UICONTROL Select]** (icono de marca de verificación) y, a continuación, seleccione **[!UICONTROL Editar]** en la barra de herramientas.
   * Toque en un recurso de conjunto de imágenes y, a continuación, seleccione **[!UICONTROL Editar]** (icono de lápiz) en la barra de herramientas.

1. Para editar las imágenes del conjunto de imágenes, realice una de las acciones siguientes:

   * Para reordenar los recursos, arrastre una imagen a una nueva ubicación (seleccione el icono de reordenar para mover elementos).
   * Para ordenar los elementos en orden ascendente o descendente, haga clic en el encabezado de la columna.
   * Para agregar un recurso o actualizar un recurso existente, haga clic en el botón **[!UICONTROL Agregar recurso]**. Vaya a un recurso, selecciónelo y, a continuación, seleccione **[!UICONTROL Select]** cerca de la esquina superior derecha de la página.

      >[!NOTE]
      >
      >Si elimina la imagen que usa el Experience Manager para la miniatura reemplazándola por otra imagen, el recurso original seguirá apareciendo.
   * Para eliminar un recurso, selecciónelo y seleccione **[!UICONTROL Eliminar recurso]**.
   * Para aplicar un ajuste preestablecido, cerca de la esquina superior derecha de la página, seleccione **[!UICONTROL Ajuste preestablecido]** y, a continuación, seleccione un ajuste preestablecido de visualizador.
   * Para añadir o cambiar una miniatura, seleccione el icono de miniatura situado a la derecha del recurso. Vaya al nuevo recurso de muestra o miniatura, selecciónelo y, a continuación, seleccione **[!UICONTROL Select]**.
   * Para eliminar un conjunto de imágenes completo, vaya al conjunto de imágenes, selecciónelo y seleccione **[!UICONTROL Eliminar]**.

   >[!NOTE]
   >
   >Puede editar las imágenes en un conjunto de imágenes. Vaya al conjunto y seleccione **[!UICONTROL Definir miembros]** en el carril izquierdo. Para abrir la ventana de edición, seleccione el icono Lápiz en un recurso.

1. Toque **[!UICONTROL Guardar]** cuando haya terminado de editar.

## Vista previa de conjuntos de imágenes {#previewing-image-sets}

Consulte [Vista previa de recursos](/help/assets/dynamic-media/previewing-assets.md).

## Publicar conjuntos de imágenes {#publishing-image-sets}

Consulte [Publicar recursos](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md).
