---
title: Etiquetas de color para imágenes
description: Experience Manager Assets permite distinguir entre colores en una imagen y aplicarlos como etiquetas automáticamente. A continuación, puede utilizar estas etiquetas para buscar y filtrar imágenes.
exl-id: 3afa949b-ea1b-4b8e-ac94-06566e2c7147
source-git-commit: 8bdd89f0be5fe7c9d4f6ba891d7d108286f823bb
workflow-type: tm+mt
source-wordcount: '1225'
ht-degree: 9%

---

# Etiquetas de color para imágenes {#color-tag-images}

![Titular de etiquetado de color](assets/banner-image.png)

Experience Manager Assets utiliza las capacidades de IA de Adobe Sensei para distinguir entre colores en una imagen y aplicarlos como etiquetas automáticamente al ingerirlos. Estas etiquetas permiten una experiencia de búsqueda mejorada, basada en la composición de color de la imagen.

Puede configurar el número de colores, dentro de un rango de uno a cuarenta, que están etiquetados en una imagen para que pueda buscar imágenes basadas en esos colores más adelante. Experience Manager Assets aplica las etiquetas en función de la cobertura de color de una imagen. También puede configurar el formato de visualización de una etiqueta de color.

La siguiente figura ilustra la secuencia de tareas que se realizan para configurar y administrar el etiquetado de colores para imágenes en Experience Manager Assets:

![Etiquetado de color](assets/color-tagging-dfd.gif)

## Formatos de archivo compatibles {#supported-file-formats-color-tags}

| Formato de archivo | Extensión | Tipo MIME | Input Colorspace | Tamaño máximo de archivo de origen admitido | Resolución de tamaño de archivo máxima admitida |
|---|---|---|---|---|---|
| JPEG | .jpg, .jpeg | image/jpeg | sRGB | 15GB | 20000px X 20000px |
| PNG | .png | image/png | sRGB | 15GB | 20000px X 20000px |
| TIFF | .tif, .tiff | image/tiff | sRGB | 4 GB (limitado por las especificaciones de formato) | 20000px X 20000px |
| PSD | .psd | image/vnd.adobe.photoshop | sRGB | 2 GB (limitado por las especificaciones de formato) | 20000px X 20000px |
| GIF | .gif | image/gif | sRGB | 15GB | 20000px X 20000px |
| BMP | .bmp | image/bmp | sRGB | 4 GB (limitado por las especificaciones de formato) | 20000px X 20000px |

## Administrar propiedades de etiquetado de color {#manage-color-tagging-properties}

Para administrar las propiedades de etiquetado de color de las imágenes:

1. Vaya a **[!UICONTROL Herramientas > Recursos > Etiquetado de color]**.

   ![Propiedades de etiquetado de color](assets/color-tag-settings.png)

1. Especifique un formato de visualización para la etiqueta de color en la **[!UICONTROL Formato de visualización]** field. Las opciones posibles incluyen el nombre del color, el RGB o el formato HEX.

1. Especifique el número de colores que desea etiquetar para las imágenes en la **[!UICONTROL Límite]** field. Estos colores se muestran al ver las propiedades de una imagen.  Puede definir un número entre uno y cuarenta en este campo. El valor predeterminado de este campo es diez colores.

1. Especifique el porcentaje mínimo de cobertura de color para incluir una etiqueta de color en los resultados de búsqueda en la **[!UICONTROL Porcentaje de umbral de cobertura/dominio]** field. Por ejemplo, si la cobertura del color rojo en una imagen es del diez por ciento y define el nueve por ciento en este campo, la imagen se incluye al buscar imágenes con color rojo. Sin embargo, si la cobertura del color rojo en una imagen es del diez por ciento y define el once por ciento en este campo, la imagen no se incluye al buscar imágenes con color rojo.

   Puede especificar cualquier número entre cinco y cien en este campo. El valor predeterminado es once.

   >[!NOTE]
   >
   >El Adobe recomienda utilizar un valor cercano al valor predeterminado en este campo. Si se establece un valor de número alto para este campo (por ejemplo, bueno de 25), es posible que se devuelvan muy pocos resultados de búsqueda. Del mismo modo, si establece un valor de número bajo (por ejemplo, menos de 6), puede que se devuelvan demasiados resultados de búsqueda, lo que puede no ser útil.

1. Haga clic en **[!UICONTROL Guardar]**.


   >[!VIDEO](https://video.tv.adobe.com/v/340108)


### Deshabilitar etiquetado de color {#disable-color-tagging}

El etiquetado de colores para imágenes está habilitado de forma predeterminada. Puede deshabilitar el etiquetado de colores en el nivel de carpeta. Todas las carpetas secundarias heredan las propiedades de etiquetado de color de la carpeta principal.

Para deshabilitar el etiquetado de colores en el nivel de carpeta:

1. Vaya a **[!UICONTROL Adobe Experience Manager > Recursos > Archivos]**.

1. Seleccione la carpeta y haga clic en **[!UICONTROL Propiedades]**.

1. En el **[!UICONTROL Procesamiento de recursos]** , vaya a la pestaña **[!UICONTROL Etiquetas de color para imágenes]** carpeta. Seleccione uno de los siguientes valores de la lista desplegable:

   * Heredada: la carpeta hereda las opciones de activación o desactivación de la carpeta principal.

   * Habilitar: habilita el etiquetado de color para la carpeta seleccionada.

   * Deshabilitar: deshabilita el etiquetado de color para la carpeta seleccionada.

   ![Configuración de etiquetado de color](assets/color-tags-folder.png)

## Configurar el esquema de metadatos para añadir el componente de etiquetas de color inteligente {#configure-metadata-schema}

Los esquemas de metadatos contienen campos específicos para que se rellene la información específica. También contiene información de diseño para mostrar los campos de metadatos de una manera fácil de usar. Las propiedades de metadatos incluyen título, descripción, tipos MIME, etiquetas y más. Puede usar el complemento [!UICONTROL Forms de esquema de metadatos] editor para modificar los esquemas existentes o agregar esquemas de metadatos personalizados.

>[!NOTE]
>
>El campo Etiqueta de color inteligente está disponible en el esquema de metadatos predeterminado. Si utiliza un esquema de metadatos personalizado, configure el esquema para agregar el campo de etiqueta de color inteligente.

Para agregar el componente Etiquetas de color inteligente al Editor de formularios de esquemas de metadatos:

1. Vaya a **[!UICONTROL Herramientas > Recursos > Esquemas de metadatos]**.

1. Seleccione el nombre del esquema y haga clic en **[!UICONTROL Editar]**.

1. Arrastrar **[!UICONTROL Etiquetas de color inteligente]** desde el **[!UICONTROL Generar formulario]** a la pestaña **[!UICONTROL Editor de formularios de esquemas de metadatos]**.

1. Haga clic en **[!UICONTROL Campo de etiqueta de color inteligente]** en el **[!UICONTROL Editor de formularios de esquemas de metadatos]**.

1. Especifique un valor apropiado en la variable **[!UICONTROL Etiqueta de campo]** en el campo **[!UICONTROL Configuración]**  pestaña.

1. Haga clic en **[!UICONTROL Guardar]**.

   >[!VIDEO](https://video.tv.adobe.com/v/340124)

## Etiquetas de color para imágenes existentes en DAM {#color-tags-existing-images}

Las imágenes ya existentes en DAM no están etiquetadas con color automáticamente. Tienes que hacerlo [!UICONTROL Volver a procesar recursos] manualmente para generar etiquetas de color para ellos.

Para aplicar etiquetas de color a imágenes o carpetas (incluidas las subcarpetas) de recursos que ya existen en el repositorio de recursos, siga estos pasos:

1. Seleccione el [!DNL Adobe Experience Manager] y, a continuación, seleccione los recursos en la [!UICONTROL Navegación] página.

1. Seleccionar [!UICONTROL Archivos] para mostrar la interfaz de Assets.

1. Desplácese hasta la carpeta a la que desee aplicar las etiquetas de color.

1. Seleccione la carpeta completa o imágenes específicas.

1. Seleccionar ![Icono Volver a procesar recursos](assets/do-not-localize/reprocess-assets-icon.png) [!UICONTROL Volver a procesar recursos] y seleccione el icono [!UICONTROL Proceso completo] opción.

Una vez completado el proceso, vaya a [!UICONTROL Propiedades] de cualquier imagen de la carpeta. Las etiquetas añadidas automáticamente se ven en [!UICONTROL Etiquetas de color inteligente] sección en [!UICONTROL Básico] pestaña.


## Ver etiquetas de colores inteligentes para imágenes {#view-color-tags}

Para ver las etiquetas de color inteligente de las imágenes:

1. Vaya a **[!UICONTROL Adobe Experience Manager > Recursos > Archivos]**.

1. Haga clic en la carpeta adecuada y seleccione la imagen.

1. Seleccionar **[!UICONTROL Propiedades]** y vea las etiquetas en la **[!UICONTROL Etiquetas de color inteligente]** field.

   ![Ver etiquetas de color](assets/view-color-tags.png)

   Pase el ratón sobre una etiqueta de color para ver el **[!UICONTROL Porcentaje de umbral de cobertura/dominio]** de un color en una imagen.

## Configuración del predicado de color de AEM Assets {#configure-search-predicate}

Puede configurar el filtro de búsqueda para las imágenes. A continuación, puede basar los criterios de búsqueda en un color específico para filtrar los resultados.

>[!NOTE]
>
>Configure el predicado de color de AEM Assets solo si no utiliza el formulario de búsqueda predeterminado.

Para configurar el filtro de búsqueda, cree un predicado de color de recurso con el carril de búsqueda de administración de recursos.

Para configurar el filtro de búsqueda:

1. Vaya a **[!UICONTROL Herramientas > General > Buscar Forms]**.

1. Seleccionar **[!UICONTROL Carril de búsqueda de administración de Assets]** y haga clic en **[!UICONTROL Editar]**.

1. Arrastrar **[!UICONTROL Predicado de color de recurso]** desde el **[!UICONTROL Seleccionar predicado]** a la pestaña **[!UICONTROL Buscar editor de formularios]**.

1. Especifique un valor apropiado en la variable **[!UICONTROL Etiqueta de campo]** en el campo **[!UICONTROL Configuración]**  pestaña.

1. Clic **[!UICONTROL Listo]** para guardar la configuración.

   >[!VIDEO](https://video.tv.adobe.com/v/340110)

## Buscar imágenes basadas en colores {#search-images-based-on-colors}

>[!VIDEO](https://video.tv.adobe.com/v/340761)

Después de configurar todas las propiedades de etiquetado de color y [configuración del predicado de color de recursos](#search-images-based-on-colors), puede buscar imágenes basadas en un color como filtro.

Para buscar imágenes basadas en colores:

1. Vaya a **[!UICONTROL Recursos > Archivos]**.

1. Seleccionar **[!UICONTROL Filtrar]** en la lista desplegable.
   ![Filtrar recursos](assets/filter-assets.png)

1. Seleccione el [Predicado de color AEM Assets](#configure-search-predicate).

1. Arrastre el selector de color para seleccionar el color adecuado. El color seleccionado se muestra en el campo de solo lectura disponible debajo del selector de color. Puede seleccionar RGB o HEX como formato de visualización para el color.

   ![Selector de color](assets/color-picker-color-tags.png)

   Puede filtrar imágenes en función de la selección de un color. Las imágenes que tienen el color seleccionado como una de las etiquetas de color inteligente y encima del [Porcentaje del umbral de cobertura/dominio](#manage-color-tagging-settings) en el panel derecho.

1. Haga clic en x en la barra de búsqueda para borrar el filtro.

**Consulte también**

* [Traducir recursos](translate-assets.md)
* [API HTTP de Recursos](mac-api-assets.md)
* [Formatos de archivo compatibles con Assets](file-format-support.md)
* [Buscar recursos](search-assets.md)
* [Recursos conectados](use-assets-across-connected-assets-instances.md)
* [Informes de Asset](asset-reports.md)
* [Esquemas de metadatos](metadata-schemas.md)
* [Descarga de recursos](download-assets-from-aem.md)
* [Administración de metadatos](manage-metadata.md)
* [Facetas de búsqueda](search-facets.md)
* [Administrar colecciones](manage-collections.md)
* [Importación masiva de metadatos](metadata-import-export.md)
