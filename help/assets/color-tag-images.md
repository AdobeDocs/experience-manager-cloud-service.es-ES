---
title: Etiquetas de color para imágenes
description: Adobe Experience Manager Assets permite distinguir entre colores en una imagen y aplicarlos como etiquetas automáticamente. A continuación, puede utilizar estas etiquetas para buscar y filtrar imágenes.
exl-id: 3afa949b-ea1b-4b8e-ac94-06566e2c7147
feature: Smart Imaging, Interactive Images, Asset Management
role: User, Admin
source-git-commit: 281a8efcd18920dd926d92db9c757c0513d599fd
workflow-type: tm+mt
source-wordcount: '1243'
ht-degree: 8%

---

# Etiquetas de color para imágenes {#color-tag-images}

![Banner De Etiquetado De Color](assets/banner-image.png)

Adobe Experience Manager (AEM) Assets utiliza las funcionalidades de IA de Adobe para distinguir entre colores en una imagen y aplicarlos como etiquetas automáticamente al ingerirlos. Estas etiquetas permiten una experiencia de búsqueda mejorada, basada en la composición de color de la imagen.

Puede configurar el número de colores, dentro de un rango de uno a 40, que están etiquetados en una imagen para que pueda buscar imágenes basadas en esos colores más adelante. Experience Manager Assets aplica las etiquetas en función de la cobertura de color de una imagen. También puede configurar el formato de visualización de una etiqueta de color.

La siguiente figura ilustra la secuencia de tareas que se realizan para configurar y administrar el etiquetado de colores para imágenes en Experience Manager Assets:

![Etiquetado de color](assets/color-tagging-dfd.gif)

## Formatos de archivo compatibles {#supported-file-formats-color-tags}

| Formato del archivo | Extensión | Tipo MIME | Input Colorspace | Tamaño máximo de archivo de origen admitido | Resolución de tamaño de archivo máxima admitida |
|---|---|---|---|---|---|
| JPEG | .jpg y .jpeg | image/jpeg | sRGB | 15 GB | 20000 × 20000 píxeles |
| PNG | .png | image/png | sRGB | 15 GB | 20000 × 20000 píxeles |
| TIFF | .tif y .tiff | image/tiff | sRGB | 4 GB (limitado por las especificaciones de formato) | 20000 × 20000 píxeles |
| PSD | .psd | image/vnd.adobe.photoshop | sRGB | 2 GB (limitado por las especificaciones de formato) | 20000 × 20000 píxeles |
| GIF | .gif | image/gif | sRGB | 15 GB | 20000 × 20000 píxeles |
| BMP | .bmp | image/bmp | sRGB | 4 GB (limitado por las especificaciones de formato) | 20000 × 20000 píxeles |

## Administrar propiedades de etiquetado de color {#manage-color-tagging-properties}

Para administrar las propiedades de etiquetado de color de las imágenes:

1. Vaya a **[!UICONTROL Herramientas > Assets > Etiquetado de color]**.

   ![Propiedades de etiquetado de color](assets/color-tag-settings.png)

1. Especifique un formato de visualización para la etiqueta de color en el campo **[!UICONTROL Formato de visualización]**. Las opciones posibles incluyen el nombre del color, el formato RGB o HEX.

1. Especifique el número de colores que desea etiquetar para las imágenes en el campo **[!UICONTROL Limit]**. Estos colores se muestran al ver las propiedades de una imagen. Puede definir un número entre uno y 40 en este campo. El valor predeterminado de este campo es diez colores.

1. Especifique el porcentaje mínimo de cobertura de color para incluir una etiqueta de color en los resultados de búsqueda en el campo **[!UICONTROL Umbral de cobertura/dominio %]**. Por ejemplo, si la cobertura del color rojo en una imagen es del diez por ciento y define el nueve por ciento en este campo, la imagen se incluye al buscar imágenes con color rojo. Sin embargo, si la cobertura del color rojo en una imagen es del diez por ciento y define el 11 por ciento en este campo, la imagen no se incluye al buscar imágenes con color rojo.

   Puede especificar cualquier número entre cinco y 100 en este campo. El valor predeterminado es 11.

   >[!NOTE]
   >
   >Adobe recomienda utilizar un valor cercano al valor predeterminado en este campo. Si establece un valor de número alto para este campo (por ejemplo, mayor que 25), es posible que se devuelvan pocos resultados de búsqueda. Del mismo modo, si establece un valor de número bajo (por ejemplo, menos de 6), puede que se devuelvan demasiados resultados de búsqueda, lo que puede no ser útil.

1. Haga clic en **[!UICONTROL Guardar]**.


   >[!VIDEO](https://video.tv.adobe.com/v/340108)


### Deshabilitar etiquetado de color {#disable-color-tagging}

El etiquetado de colores para imágenes está habilitado de forma predeterminada. Puede deshabilitar el etiquetado de colores en el nivel de carpeta. Todas las carpetas secundarias heredan las propiedades de etiquetado de color de la carpeta principal.

Para deshabilitar el etiquetado de colores en el nivel de carpeta:

1. Vaya a **[!UICONTROL Adobe Experience Manager > Assets > Archivos]**.

1. Seleccione la carpeta y haga clic en **[!UICONTROL Propiedades]**.

1. En la pestaña **[!UICONTROL Procesamiento de recursos]**, vaya a la carpeta **[!UICONTROL Etiquetas de color para imágenes]**. Seleccione uno de los siguientes valores de la lista desplegable:

   * Heredada: la carpeta hereda las opciones de activación o desactivación de la carpeta principal.

   * Habilitar: habilita el etiquetado de color para la carpeta seleccionada.

   * Deshabilitar: deshabilita el etiquetado de color para la carpeta seleccionada.

   ![Configuración de etiquetado de color](assets/color-tags-folder.png)

## Configurar el esquema de metadatos para añadir el componente de etiquetas de color inteligente {#configure-metadata-schema}

Los esquemas de metadatos contienen campos específicos para que se rellene la información específica. También contiene información de diseño para mostrar los campos de metadatos de una manera fácil de usar. Las propiedades de metadatos incluyen título, descripción, tipos MIME, etiquetas y más. Puede usar el editor [!UICONTROL Metadata Schema Forms] para modificar los esquemas existentes o agregar esquemas de metadatos personalizados.

>[!NOTE]
>
>El campo Etiqueta de color inteligente está disponible en el esquema de metadatos predeterminado. Si utiliza un esquema de metadatos personalizado, configure el esquema para agregar un campo de etiqueta de color inteligente.

Para agregar el componente Etiquetas de color inteligente al Editor de formularios de esquemas de metadatos:

1. Vaya a **[!UICONTROL Herramientas > Recursos > Esquemas de metadatos]**.

1. Seleccione el nombre del esquema y haga clic en **[!UICONTROL Editar]**.

1. Arrastre **[!UICONTROL Etiquetas de color inteligente]** desde la ficha **[!UICONTROL Generar formulario]** hasta el **[!UICONTROL Editor de formularios de esquemas de metadatos]**.

1. Haga clic en el **[!UICONTROL campo de etiqueta de color inteligente]** en el **[!UICONTROL Editor de formularios de esquemas de metadatos]**.

1. Especifique un valor apropiado en el campo **[!UICONTROL Etiqueta de campo]** de la ficha **[!UICONTROL Configuración]**.

1. Haga clic en **[!UICONTROL Guardar]**.

   >[!VIDEO](https://video.tv.adobe.com/v/340124)

## Etiquetas de color para imágenes existentes en DAM {#color-tags-existing-images}

Las imágenes existentes en DAM no se etiquetan con colores automáticamente. [!UICONTROL Vuelva a procesar Assets] manualmente para generar etiquetas de color para ellos.

Para aplicar etiquetas de color a imágenes o carpetas (incluidas las subcarpetas) de recursos que existen en el repositorio de recursos, siga estos pasos:

1. Seleccione el logotipo de [!DNL Adobe Experience Manager] y, a continuación, seleccione los recursos en la página [!UICONTROL Navegación].

1. Seleccionar [!UICONTROL archivos].

1. En la interfaz de Assets, vaya a la carpeta a la que desee aplicar las etiquetas de color.

1. Seleccione la carpeta completa o imágenes específicas.

1. Seleccione ![Icono de reprocesamiento de recursos](assets/do-not-localize/reprocess-assets-icon.png) [!UICONTROL Reprocesar Assets] y seleccione la opción [!UICONTROL Proceso completo].

Cuando finalice el proceso, vaya a la página [!UICONTROL Propiedades] de cualquier imagen de la carpeta. Las etiquetas agregadas automáticamente se ven en la sección [!UICONTROL Etiquetas de color inteligente] de la pestaña [!UICONTROL Básico].


## Ver etiquetas de colores inteligentes para imágenes {#view-color-tags}

Para ver las etiquetas de color inteligente de las imágenes:

1. Vaya a **[!UICONTROL Adobe Experience Manager > Assets > Archivos]**.

1. Haga clic en la carpeta adecuada y seleccione la imagen.

1. Seleccione **[!UICONTROL Propiedades]** y vea las etiquetas en el campo **[!UICONTROL Etiquetas de color inteligente]**.

   ![Ver etiquetas de color](assets/view-color-tags.png)

   Pase el ratón sobre una etiqueta de color para ver el **[!UICONTROL umbral de cobertura/dominio %]** de un color en una imagen.

## Configuración del predicado de color de AEM Assets {#configure-search-predicate}

Puede configurar un filtro de búsqueda para imágenes. A continuación, puede basar los criterios de búsqueda en un color específico para filtrar los resultados.

>[!NOTE]
>
>Configure el predicado de color AEM Assets solo si no está utilizando el formulario de búsqueda predeterminado.

Para configurar el filtro de búsqueda, cree un predicado de color de recurso con el carril de Assets Admin Search.

Para configurar el filtro de búsqueda:

1. Vaya a **[!UICONTROL Herramientas > General > Buscar en Forms]**.

1. Seleccione **[!UICONTROL Carril de Assets Admin Search]** y haga clic en **[!UICONTROL Editar]**.

1. Arrastre **[!UICONTROL Predicado de color de recurso]** de la ficha **[!UICONTROL Seleccionar predicado]** al **[!UICONTROL Editor de formularios de búsqueda]**.

1. Especifique un valor apropiado en el campo **[!UICONTROL Etiqueta de campo]** de la ficha **[!UICONTROL Configuración]**.

1. Haga clic en **[!UICONTROL Listo]** para guardar los cambios.

   >[!VIDEO](https://video.tv.adobe.com/v/340110)

## Buscar imágenes basadas en colores {#search-images-based-on-colors}

>[!VIDEO](https://video.tv.adobe.com/v/340761)

Después de configurar todas las propiedades de etiquetado de colores y [configurar el predicado de color de Assets](#search-images-based-on-colors), puede buscar imágenes basadas en un color como filtro.

Para buscar imágenes basadas en colores:

1. Vaya a **[!UICONTROL Assets > Archivos]**.

1. Seleccione **[!UICONTROL Filter]** de la lista desplegable.
   ![Filtrar Assets](assets/filter-assets.png)

1. Seleccione el predicado de color [AEM Assets](#configure-search-predicate).

1. Arrastre el selector de color para seleccionar el color adecuado. El color seleccionado se muestra en el campo de solo lectura disponible debajo del selector de color. Puede seleccionar RGB o HEX como formato de visualización para el color.

   ![Selector de color](assets/color-picker-color-tags.png)

   Puede filtrar imágenes en función de la selección de un color. Las imágenes que tienen el color seleccionado como una de las etiquetas de color inteligente y por encima del [umbral de cobertura/dominio %](#manage-color-tagging-settings) se muestran en el panel derecho.

1. Borre el filtro haciendo clic en la X de la barra de búsqueda.

**Consulte también**

* [Traducir recursos](translate-assets.md)
* [API HTTP de recursos](mac-api-assets.md)
* [Formatos de archivo compatibles con recursos](file-format-support.md)
* [Buscar recursos](search-assets.md)
* [Recursos de red](use-assets-across-connected-assets-instances.md)
* [Informes de recurso](asset-reports.md)
* [Esquemas de metadatos](metadata-schemas.md)
* [Descarga de recursos](download-assets-from-aem.md)
* [Administración de metadatos](manage-metadata.md)
* [Facetas de búsqueda](search-facets.md)
* [Administrar colecciones](manage-collections.md)
* [Importación masiva de metadatos](metadata-import-export.md)
* [Publicación de recursos en AEM y Dynamic Media](/help/assets/publish-assets-to-aem-and-dm.md)
