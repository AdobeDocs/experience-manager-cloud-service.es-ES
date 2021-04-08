---
title: Conjuntos de giros
description: Aprenda a trabajar con conjuntos de giros en Dynamic Media.
feature: Conjuntos de giros
topic: Profesional empresarial
role: Business Practitioner
exl-id: ed470472-62d9-4684-971b-30df3919c180
translation-type: tm+mt
source-git-commit: 6b232ab512a6faaf075faa55c238dfb10c00b100
workflow-type: tm+mt
source-wordcount: '1831'
ht-degree: 12%

---

# Conjuntos de giros{#spin-sets}

Un conjunto de giros simula el acto real de girar un objeto para examinarlo. Los conjuntos de giros permiten ver los elementos desde cualquier ángulo, obteniendo los detalles visuales clave desde cualquier ángulo.

Un conjunto de giros simula una experiencia de visualización de 360 grados. Dynamic Media ofrece conjuntos de giros de un solo eje en los que los espectadores pueden rotar un elemento. Además, los usuarios pueden aplicar zoom &quot;de forma libre&quot; y recorrer cualquiera de las vistas con unos pocos clics sencillos del ratón. De este modo, los usuarios pueden examinar un elemento más de cerca desde un punto de vista particular.

Los conjuntos de giros se designan mediante un banner con la palabra **[!UICONTROL SPINSET]**. Además, si se publica el conjunto de giros, se muestra la fecha de publicación, indicada por el icono **[!UICONTROL World]**, junto con la fecha de la última modificación, indicada por el icono **[!UICONTROL Lápiz]**.

![Chlimage_1-](assets/chlimage_1-380.png)

>[!NOTE]
>
>Para obtener información sobre la interfaz de usuario de Assets, consulte [Administración de recursos con la IU táctil](/help/assets/manage-digital-assets.md) y aplicarla a una nueva carpeta en la que se cargan los recursos del conjunto de imágenes.

## Inicio rápido: Conjuntos de giros {#quick-start-spin-sets}

Para poner en marcha rápidamente los conjuntos de giros, siga estos pasos:

1. Opcional. [Cree un conjunto de lotes ](/help/assets/dynamic-media/batch-set-presets-dm.md) preestablecido y aplíquelo a una nueva carpeta de recursos.

   Un ajuste preestablecido de conjunto de lotes puede ayudarle a automatizar la creación del conjunto de giros.

   >[!IMPORTANT]
   >
   >IPS (Image Production System) crea los conjuntos de lotes como parte de la ingesta de recursos.

1. [Cargue las imágenes para varias vistas](#uploading-assets-for-spin-sets).

   Como mínimo, necesitará entre 8 y 12 tomas de un elemento para un conjunto de giros unidimensional y entre 16 y 24 para un conjunto de giros bidimensional. Las tomas deben realizarse a intervalos regulares para dar la impresión de que el objeto está girando y siendo volteado. Por ejemplo, si un conjunto de giros unidimensional incluye 12 tomas, gire el elemento 30° (360/12) para cada toma.

1. [Crear conjuntos de giros](#creating-spin-sets).

   Para crear un conjunto de giros, seleccione **[!UICONTROL Crear > Conjunto de giros]** y asigne un nombre al conjunto, elija los recursos y elija el orden en que aparecen las imágenes.

   Consulte [Uso de selectores](/help/assets/dynamic-media/working-with-selectors.md).

1. Configure los [ajustes preestablecidos del visualizador de conjuntos de giros](/help/assets/dynamic-media/managing-viewer-presets.md) según sea necesario.

   Los administradores pueden crear o modificar ajustes preestablecidos de visualizador de conjuntos de giros. Para ver el conjunto de giros con un ajuste preestablecido de visualizador, seleccione el conjunto de giros y, en el menú desplegable del carril izquierdo, seleccione **Visualizadores**.

   Para crear o editar ajustes preestablecidos de visualizador, consulte **[!UICONTROL Herramientas > Recursos > Ajustes preestablecidos de visualizador]**.

   Consulte [Adición y edición de ajustes preestablecidos de visualizador](/help/assets/dynamic-media/managing-viewer-presets.md).

   Puede ver y acceder a los conjuntos creados mediante ajustes preestablecidos de conjuntos de lotes de tres formas diferentes. (Los conjuntos creados con ajustes preestablecidos de conjuntos de lotes no *no* aparecen en la interfaz de usuario).

1. [Vista previa de conjuntos de giros](/help/assets/dynamic-media/previewing-assets.md).

   Seleccione el conjunto de giros y podrá previsualizarlo. Rotar el conjunto de giros. Puede elegir diferentes visores desde el menú **[!UICONTROL Visualizadores]**, disponible en el menú desplegable del carril izquierdo.

1. [Publicar conjuntos de giros](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md).

   Al publicar un conjunto de giros, se activa la dirección URL y la cadena Incrustar. Además, debe [publicar el ajuste preestablecido de visor](/help/assets/dynamic-media/managing-viewer-presets.md).

1. [Vincule las URL a su ](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md) aplicación web o  [incruste el visualizador de imágenes o vídeos](/help/assets/dynamic-media/embed-code.md).

   Adobe Experience Manager Assets crea llamadas URL para conjuntos de giros y las activa después de publicar los conjuntos de giros. Puede copiar estas direcciones URL cuando obtiene una vista previa de los recursos. También puede incrustarlos en el sitio web.

   Seleccione el conjunto de giros y, a continuación, en el menú desplegable del carril izquierdo, seleccione **[!UICONTROL Visualizadores]**.

   Consulte [Vinculación de un conjunto de giros a una página web](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md) e [Incrustación del visualizador de imágenes o vídeos](/help/assets/dynamic-media/embed-code.md).

Si es necesario, puede [editar los conjuntos de giros](#editing-spin-sets). Además, puede ver y modificar [Propiedades del conjunto de giros](/help/assets/manage-digital-assets.md#editing-properties).

## Carga de recursos para conjuntos de giros {#uploading-assets-for-spin-sets}

Como mínimo, se necesitan 8-12 tomas de un elemento para un conjunto de giros unidimensional. Las tomas deben realizarse a intervalos regulares para dar la impresión de que el objeto está girando y siendo volteado. Por ejemplo, si un conjunto de giros unidimensional incluye 12 tomas, gire el elemento 30° (360/12) para cada toma.

Puede cargar imágenes para los conjuntos de giros del mismo modo que [cargaría cualquier otro recurso en Recursos de Experience Manager](/help/assets/manage-digital-assets.md).

### Pautas para capturar imágenes para el conjunto de giros {#guidelines-for-shooting-spin-set-images}

A continuación se indican algunas prácticas recomendadas en relación con las imágenes de conjuntos de giros. En general, cuantas más imágenes haya en un conjunto de giros, mejor será el efecto giratorio de la imagen. Sin embargo, al incluir muchas imágenes en el conjunto, también aumenta el tiempo que tardan las imágenes en cargarse. Experience Manager recomienda estas directrices para la toma de imágenes para su uso en Conjuntos de giros:

* Como mínimo, utilice entre 8 y 12 imágenes en un conjunto de giros unidimensional y entre 16 y 24 imágenes en un conjunto de giros bidimensional. Se necesita un mínimo de 8 imágenes para poder girar 360°. Los conjuntos de giros unidimensionales son más comunes, ya que la creación de conjuntos de giros bidimensionales requiere mucho trabajo.
* Utilizar un formato sin pérdidas; Se recomiendan TIFF y PNG.
* Enmascara todas las imágenes para que el elemento aparezca sobre un fondo blanco puro u otro de alto contraste. De forma opcional, agregue sombras.
* Asegúrese de que los detalles del producto estén bien iluminados y enfocados.
* Toma imágenes de giro para ropa de moda con un maniquí o modelo. A menudo el maniquí está enmascarado (usando un maniquí de vidrio) o un maniquí estilizado/forma de vestir se muestra en la imagen. Puede crear un conjunto de giros en modelo definiendo el número de ángulos. Marque cada ángulo con cinta en el suelo para guiar al modelo hacia el paso y mirar en la dirección de cada toma.

## Creación de conjuntos de giros {#creating-spin-sets}

En esta sección se describe cómo crear conjuntos de giros.

>[!NOTE]
>
>También puede crear conjuntos de giros automáticamente mediante los [ajustes preestablecidos de conjuntos de lotes](/help/assets/dynamic-media/config-dm.md). **Importante:** IPS (Image Production System) crea los conjuntos de lotes como parte de la ingesta de recursos.
>
>Consulte &quot;Creación de ajustes preestablecidos de conjuntos de lotes para generar automáticamente conjuntos de imágenes y conjuntos de giros&quot; en [Configuración de Dynamic Media](/help/assets/dynamic-media/config-dm.md).

>[!NOTE]
>
>Orden en el que aparecen las imágenes en un conjunto de giros. Asegúrese de ordenarlas para que el giro sea una vista suave de 360 grados.

**Creación de conjuntos de giros**

1. En Assets, navegue hasta el lugar donde desee crear un conjunto de giros, haga clic en **[!UICONTROL Crear]** y seleccione **[!UICONTROL Conjunto de giros]**. También puede crear el conjunto desde una carpeta que contenga los recursos. Aparece el Editor de conjuntos de giros.

   ![6_5_spinset-createpulldownmenu](assets/6_5_spinset-createpulldownmenu.png)

1. En el Editor de conjuntos de giros, en el campo **[!UICONTROL Title]**, introduzca un nombre para el conjunto de giros. El nombre aparece en el banner del conjunto de giros. De forma opcional, introduzca una descripción.

   ![6_5_spinset-spinseteditortitle](assets/6_5_spinset-spinseteditortitle.png)

   >[!NOTE]
   >
   >Al crear el conjunto de giros, puede cambiar la miniatura del conjunto de giros o permitir que el Experience Manager seleccione la miniatura automáticamente en función de los recursos del conjunto de giros. Para seleccionar una miniatura, haga clic en **[!UICONTROL Cambiar miniatura]** y seleccione cualquier imagen (puede navegar también a otras carpetas para buscar imágenes). Si ha seleccionado una miniatura y, a continuación, decide que desea que el Experience Manager genere una del conjunto de giros, seleccione **[!UICONTROL Cambiar a miniatura automática]**.

1. Realice una de las siguientes acciones:

   * Cerca de la esquina superior izquierda de la página Editor de conjuntos de giros, pulse **[!UICONTROL Agregar recurso]**.

   * Cerca de la mitad de la página Editor de conjuntos de giros, pulse **[!UICONTROL Toque para abrir el Selector de recursos]**.
   Pulse para seleccionar los recursos que desea incluir en el conjunto de giros. Los recursos seleccionados tienen un icono de marca de verificación sobre ellos. Cuando haya terminado, pulse **[!UICONTROL Seleccionar]** cerca de la esquina superior derecha de la página.

   Con el Selector de recursos, puede buscar recursos escribiendo una palabra clave y pulsando **[!UICONTROL Retorno]**. También puede aplicar filtros para restringir los resultados de búsqueda. Puede filtrar por ruta, colección, tipo de archivo y etiqueta. Seleccione el filtro y, a continuación, pulse el icono **[!UICONTROL Filtro]** en la barra de herramientas. Para cambiar la vista, pulse el icono Ver y seleccione **[!UICONTROL Vista de columna]**, **[!UICONTROL Vista de tarjeta]** o **[!UICONTROL Vista de lista]**.

   Consulte [Uso de selectores](/help/assets/dynamic-media/working-with-selectors.md).

   ![chlimage_1-383](assets/chlimage_1-383.png)

1. Cuando se añaden recursos al conjunto, estos se añaden automáticamente en orden alfanumérico. Después de agregarlos, puede reordenar u ordenar los recursos manualmente.

   Si es necesario, arrastre el icono Reordenar de un recurso a la derecha del nombre del archivo del recurso para reordenar las imágenes hacia arriba o hacia abajo en la lista de conjunto.

   ![Reorganización del fotograma 11 del conjunto de giros arrastrándolo a una nueva ubicación](assets/6_5_spinset-reorderassets.png)

   Reordenar el fotograma 11 del conjunto de giros arrastrándolo a una nueva ubicación.

1. (Opcional) Realice cualquiera de las siguientes acciones:

   * Para eliminar una imagen, seleccione la imagen y pulse **[!UICONTROL Eliminar recurso]**.

   * Para aplicar un ajuste preestablecido, cerca de la esquina superior derecha de la página, pulse **[!UICONTROL Ajuste preestablecido]** y, a continuación, seleccione un ajuste preestablecido para aplicar a todos los recursos a la vez.

1. Haga clic en **[!UICONTROL Guardar]**. El conjunto de giros recién creado aparece en la carpeta en la que lo creó.

## Visualización de conjuntos de giros {#viewing-spin-sets}

Puede crear conjuntos de giros en la interfaz de usuario o automáticamente utilizando [ajustes preestablecidos de conjuntos de lotes](/help/assets/dynamic-media/config-dm.md). Sin embargo, los conjuntos creados con ajustes preestablecidos de conjuntos de lotes, no *no* aparecen en la interfaz de usuario. Puede acceder a los conjuntos creados mediante ajustes preestablecidos de conjuntos de lotes de tres formas diferentes. (Estos métodos están disponibles aunque haya creado los conjuntos de giros en la interfaz de usuario).

>[!NOTE]
>
>También puede ver los conjuntos mediante la interfaz de usuario que se describe en [Edición de conjuntos de giros](#editing-spin-sets).

**Visualización de conjuntos de giros**

1. Al abrir las propiedades de un recurso individual. Las propiedades indican los conjuntos de miembros del recurso seleccionado (en **[!UICONTROL Member of Sets]**). Para ver el conjunto completo, pulse el nombre del conjunto.

   ![chlimage_1-156](assets/chlimage_1-384.png)

1. Desde una imagen de miembro de cualquier conjunto. Seleccione el menú **[!UICONTROL Conjuntos]** para mostrar los conjuntos de los que es miembro el recurso.

   ![chlimage_1-157](assets/chlimage_1-385.png)

1. Desde la búsqueda, puede seleccionar **[!UICONTROL Filtros]**, luego expandir **[!UICONTROL Dynamic Media]** y seleccionar **[!UICONTROL Conjuntos]**.

   La búsqueda devuelve conjuntos coincidentes creados manualmente en la interfaz de usuario o creados automáticamente mediante ajustes preestablecidos de conjuntos de lotes. Para los conjuntos automatizados, la consulta de búsqueda se realiza utilizando `Starts with` criterios de búsqueda que son diferentes de la búsqueda de Experience Manager, que se basa en el uso de `Contains` criterios de búsqueda. Definir el filtro como **[!UICONTROL Sets]** es la única manera de buscar conjuntos automatizados.

   ![chlimage_1-158](assets/chlimage_1-386.png)

## Edición de conjuntos de giros {#editing-spin-sets}

Puede realizar varias tareas de edición en los conjuntos de giros, como las siguientes:

* Agregue imágenes al conjunto de giros.
* Reordenar imágenes en el conjunto de giros.
* Eliminar recursos del conjunto de giros.
* Aplicar ajustes preestablecidos de visor.
* Elimine el conjunto de giros.

**Para editar un conjunto de giros**

1. Realice una de las siguientes acciones:

   * Pase el ratón sobre un recurso de conjunto de giros y, a continuación, pulse **[!UICONTROL Editar]** (icono de lápiz).
   * Pase el ratón sobre un recurso de conjunto de giros, pulse **[!UICONTROL Seleccionar]** (icono de marca de verificación) y, a continuación, pulse **[!UICONTROL Editar]** en la barra de herramientas.

   * Pulse en un recurso de conjunto de giros y, a continuación, pulse **[!UICONTROL Editar]** (icono de lápiz) en la barra de herramientas.

1. Para editar el conjunto de giros, realice una de las acciones siguientes:

   * Para reordenar las imágenes, arrastre una imagen a una nueva ubicación (seleccione el icono de reordenar para mover elementos).
   * Para ordenar los elementos en orden ascendente o descendente, haga clic en el encabezado de la columna.
   * Para agregar un recurso o actualizar un recurso existente, haga clic en **[!UICONTROL Agregar recurso]**. Vaya a un recurso, selecciónelo y pulse **[!UICONTROL Seleccionar]** cerca de la esquina superior derecha.
Si elimina la imagen que usa el Experience Manager para la miniatura reemplazándola por otra imagen, el recurso original seguirá apareciendo.
   * Para eliminar un recurso, selecciónelo y pulse o haga clic en **[!UICONTROL Eliminar recurso]**.
   * Para aplicar un ajuste preestablecido, pulse o haga clic en el icono Ajuste preestablecido y seleccione un ajuste preestablecido.
   * Para eliminar un conjunto de giros completo, vaya al conjunto de giros, selecciónelo y seleccione **[!UICONTROL Eliminar]**

   >[!NOTE]
   >
   >Para editar las imágenes de un conjunto de giros, vaya al conjunto, pulse **[!UICONTROL Definir miembros]** en el carril izquierdo y, a continuación, pulse el icono Lápiz en un recurso individual para abrir la ventana de edición.

1. Haga clic en **[!UICONTROL Guardar]** cuando termine de editar.

## Vista previa de conjuntos de giros {#previewing-spin-sets}

Consulte [Vista previa de recursos](/help/assets/dynamic-media/previewing-assets.md).

## Conjuntos de giros de publicación {#publishing-spin-sets}

Consulte [Publicación de recursos](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md).
