---
title: Trabajar con selectores
description: Selección de recursos para imágenes interactivas, vídeos interactivos y pancartas de carrusel
translation-type: tm+mt
source-git-commit: c240f9aa465b019fa77cc471f865db1f4ab45532
workflow-type: tm+mt
source-wordcount: '738'
ht-degree: 18%

---


# Uso de selectores en Dynamic Media {#working-with-selectors}

Al trabajar con una imagen interactiva, un vídeo interactivo o una pancarta de carrusel, se seleccionan recursos y se seleccionan sitios y productos para las zonas interactivas y los mapas de imagen con los que se desea establecer el vínculo. Al trabajar con conjuntos de imágenes, conjuntos de giros y conjuntos multimedia, también se seleccionan recursos con el selector de recursos.

En este tema se explica cómo utilizar los selectores Producto, Sitio y Recursos, incluida la capacidad de examinar, filtrar y ordenar dentro de los selectores.

Puede acceder a los selectores mientras crea conjuntos de carrusel, agrega zonas interactivas y mapas de imagen, y crea vídeos e imágenes interactivos.

Por ejemplo, en este letrero de carrusel, utilice el selector de productos si está vinculando un punto interactivo o un mapa de imagen a una página de vista rápida; utilice el selector de sitio si está vinculando un punto interactivo o un mapa de imagen a un hipervínculo; utilice el selector de recursos cuando esté creando una nueva diapositiva.

![chlimage_1-520](assets/chlimage_1-520.png)

Cuando selecciona (en lugar de introducir manualmente) hacia dónde van las zonas interactivas o los mapas de imagen, está utilizando el selector. El selector de sitios solo funciona si es cliente de AEM Sites. El selector de productos también requiere AEM comercio.

## Selección de productos en Dynamic Media {#selecting-products}

Utilice el selector de productos para elegir un producto cuando desee un punto interactivo o mapa de imagen para proporcionar una vista rápida a un producto específico del catálogo de productos.

1. Vaya al conjunto de carrusel, la imagen interactiva o el vídeo interactivo y pulse la pestaña **[!UICONTROL Acciones]** (solo disponible si ha definido un punto interactivo o un mapa de imagen).

   El selector de productos se encuentra en el área **[!UICONTROL Tipo de acción]**.

   ![chlimage_1-521](assets/chlimage_1-521.png)

1. Toque el icono **[!UICONTROL Selector de producto]** (lupa) y navegue hasta un producto del catálogo.

   ![chlimage_1-522](assets/chlimage_1-522.png)

   También puede filtrar por palabra clave o etiqueta tocando **[!UICONTROL Filtro]** e introduciendo palabras clave, o seleccionando etiquetas, o ambas.

   ![chlimage_1-523](assets/chlimage_1-523.png)

   Puede cambiar la ubicación en la que AEM exploran los datos del producto tocando **[!UICONTROL Examinar]** y navegando a otra carpeta.

   ![chlimage_1-524](assets/chlimage_1-524.png)

   Toque **[!UICONTROL Ordenar]** para cambiar si AEM ordena de nuevo a más antiguo o de más antiguo a más reciente.

   ![chlimage_1-525](assets/chlimage_1-525.png)

   Puntee en **[!UICONTROL Ver como]** para cambiar la forma en que ve los productos, ya sea en **[!UICONTROL Vista de lista]** o en **[!UICONTROL Vista de tarjeta]**.

   ![chlimage_1-526](assets/chlimage_1-526.png)

1. Una vez seleccionado el producto, el campo se rellena con la miniatura y el nombre del producto.

   ![chlimage_1-527](assets/chlimage_1-527.png)

1. Cuando se encuentra en el modo **[!UICONTROL Previsualización]**, puede tocar el punto interactivo o el mapa de imagen y ver el aspecto de la vista rápida.

   ![chlimage_1-528](assets/chlimage_1-528.png)

## Selección de sitios en Dynamic Media {#selecting-sites}

Utilice el selector de sitios para elegir una página Web cuando desee que un punto interactivo o mapa de imágenes se vincule a una página Web administrada dentro de AEM sitios.

1. Vaya al conjunto de carrusel, la imagen interactiva o el vídeo interactivo y pulse la pestaña **[!UICONTROL Acciones]** (solo disponible si ha definido un punto interactivo o un mapa de imagen).

   El Selector de sitio se encuentra en el área **[!UICONTROL Tipo de acción]**.

   ![chlimage_1-529](assets/chlimage_1-529.png)

1. Pulse el icono **[!UICONTROL Selector de sitio]** (carpeta con lupa) y navegue a una página de los sitios de AEM a la que desee vincular el punto interactivo o el mapa de imagen.

   ![chlimage_1-530](assets/chlimage_1-530.png)

1. Una vez seleccionado el sitio, el campo se rellena con la ruta.

   ![chlimage_1-531](assets/chlimage_1-531.png)

1. Cuando se encuentra en el modo **[!UICONTROL Previsualización]** si toca el punto interactivo o el mapa de imagen, navegue a la página del sitio AEM que especificó.

## Selección de recursos en Dynamic Media {#selecting-assets}

Utilice este selector para elegir imágenes que se utilizarán en letreros de carrusel, vídeos interactivos, conjuntos de imágenes, conjuntos de medios mixtos y conjuntos de giros. En el vídeo interactivo, el selector de recursos está disponible cuando toca **[!UICONTROL Seleccionar recursos]** en la ficha **[!UICONTROL Contenido]**. En Conjuntos de carrusel, el selector de recursos está disponible al crear una nueva diapositiva. En los conjuntos de imágenes, los conjuntos de medios mixtos y los conjuntos de giros, el selector de recursos está disponible al crear un nuevo conjunto de imágenes, un conjunto de medios mixtos o un conjunto de giros, respectivamente.

Consulte también [Selector de recursos](/help/assets/search-assets.md#assetselector) para obtener más información.

1. Vaya al conjunto de carrusel y cree una nueva diapositiva. O bien, vaya a Vídeo interactivo, vaya a la ficha **[!UICONTROL Contenido]** y seleccione recursos. O bien, cree un conjunto de medios mixtos, un conjunto de imágenes o un conjunto de giros.
1. Pulse el icono **[!UICONTROL Selector de recursos]** (carpeta con lupa) y navegue hasta un recurso.

   ![chlimage_1-532](assets/chlimage_1-532.png)

   También puede filtrar por palabra clave o etiqueta tocando **[!UICONTROL Filtro]** y escribiendo palabras clave, o agregando criterios, o ambos.

   ![chlimage_1-533](assets/chlimage_1-533.png)

   Puede cambiar el lugar donde AEM exploran los recursos navegando a otra carpeta en el campo **[!UICONTROL Ruta]**.

   Toque **[!UICONTROL Colección]** para buscar solo recursos dentro de las colecciones.

   ![chlimage_1-534](assets/chlimage_1-534.png)

   Pulse **[!UICONTROL Ver como]** para cambiar la forma en que ve los productos: **[!UICONTROL vista de lista]**, **[!UICONTROL vista de columna]** o **[!UICONTROL vista de tarjeta]**.

   ![chlimage_1-535](assets/chlimage_1-535.png)

1. Toque la marca de verificación para seleccionar el recurso. Se muestra el recurso.

   ![chlimage_1-536](assets/chlimage_1-536.png)
—>
