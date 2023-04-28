---
title: Etiquetas de color para imágenes
description: Experience Manager Assets le permite distinguir entre colores en una imagen y aplicarlos automáticamente como etiquetas. A continuación, puede utilizar estas etiquetas para buscar y filtrar imágenes.
exl-id: 3afa949b-ea1b-4b8e-ac94-06566e2c7147
source-git-commit: 8bdd89f0be5fe7c9d4f6ba891d7d108286f823bb
workflow-type: tm+mt
source-wordcount: '1225'
ht-degree: 9%

---

# Etiquetas de color para imágenes {#color-tag-images}

![Banner de etiquetado de color](assets/banner-image.png)

Experience Manager Assets utiliza las funciones de Adobe Sensei AI para distinguir entre colores en una imagen y aplicarlos automáticamente al ingerirlos. Estas etiquetas permiten una experiencia de búsqueda mejorada, basada en la composición de color de la imagen.

Puede configurar el número de colores, dentro de un rango de uno a cuarenta, que están etiquetados en una imagen para que pueda buscar imágenes basadas en esos colores más adelante. Experience Manager Assets aplica las etiquetas en función de la cobertura de color de una imagen. También puede configurar el formato de visualización para una etiqueta de color.

La siguiente ilustración ilustra la secuencia de tareas que se realizan para configurar y administrar el etiquetado de color de las imágenes en Experience Manager Assets:

![Etiquetado de color](assets/color-tagging-dfd.gif)

## Formatos de archivo compatibles {#supported-file-formats-color-tags}

| Formato del archivo | Extensión | Tipo MIME | Espacio de color de entrada | Tamaño máximo admitido del archivo de origen | Resolución máxima de tamaño de archivo admitido |
|---|---|---|---|---|---|
| JPEG | .jpg, .jpeg | image/jpeg | sRGB | 15GB | 20000px X 20000px |
| PNG | .png | image/png | sRGB | 15GB | 20000px X 20000px |
| TIFF | .tif, .tiff | image/tiff | sRGB | 4 GB (limitado por especificaciones de formato) | 20000px X 20000px |
| PSD | .psd | image/vnd.adobe.photoshop | sRGB | 2 GB (limitado por especificaciones de formato) | 20000px X 20000px |
| GIF | .gif | image/gif | sRGB | 15GB | 20000px X 20000px |
| BMP | .bmp | image/bmp | sRGB | 4 GB (limitado por especificaciones de formato) | 20000px X 20000px |

## Administración de propiedades de etiquetado de color {#manage-color-tagging-properties}

Para administrar las propiedades de etiquetado de color de las imágenes:

1. Vaya a **[!UICONTROL Herramientas > Assets > Etiquetado de color]**.

   ![Propiedades de etiquetado de color](assets/color-tag-settings.png)

1. Especifique un formato de visualización para la etiqueta de color en la variable **[!UICONTROL Formato de visualización]** campo . Las opciones posibles incluyen el nombre del color, el RGB o el formato HEX.

1. Especifique el número de colores que se etiquetarán para las imágenes en la variable **[!UICONTROL Límite]** campo . Estos colores se muestran cuando se ven las propiedades de una imagen.  Puede definir un número entre uno y cuarenta en este campo. El valor predeterminado de este campo es de diez colores.

1. Especifique el porcentaje mínimo de cobertura de color para incluir una etiqueta de color en los resultados de búsqueda en la variable **[!UICONTROL Umbral de cobertura/dominio %]** campo . Por ejemplo, si la cobertura del color rojo en una imagen es del diez por ciento y define el nueve por ciento en este campo, la imagen se incluirá cuando busque imágenes con color rojo. Sin embargo, si la cobertura del color rojo en una imagen es del diez por ciento y define el once por ciento en este campo, la imagen no se incluye cuando busca imágenes con color rojo.

   Puede especificar cualquier número entre quinientos en este campo. El valor predeterminado es once.

   >[!NOTE]
   >
   >Adobe recomienda utilizar un valor cercano al valor predeterminado de este campo. Si se establece un valor de número alto para este campo (por ejemplo, bueno a 25), es posible que se devuelvan muy pocos resultados de búsqueda. Del mismo modo, si se configura un valor de número bajo (por ejemplo, menos de 6), es posible que se devuelvan demasiados resultados de búsqueda, lo que puede no resultar útil.

1. Haga clic en **[!UICONTROL Guardar]**.


   >[!VIDEO](https://video.tv.adobe.com/v/340108)


### Desactivación del etiquetado de color {#disable-color-tagging}

El etiquetado de color de las imágenes está habilitado de forma predeterminada. Puede desactivar el etiquetado de colores en el nivel de carpeta. Todas las carpetas secundarias heredan las propiedades de etiquetado de color de la carpeta principal.

Para desactivar el etiquetado de colores en el nivel de carpeta:

1. Vaya a **[!UICONTROL Adobe Experience Manager > Assets > Archivos]**.

1. Seleccione la carpeta y haga clic en **[!UICONTROL Propiedades]**.

1. En el **[!UICONTROL Procesamiento de recursos]** , vaya a la pestaña **[!UICONTROL Etiquetas de color para imágenes]** carpeta. Seleccione uno de los siguientes valores en la lista desplegable:

   * Heredado : la carpeta hereda las opciones de activación o desactivación de la carpeta principal.

   * Habilitar - Habilita el etiquetado de color para la carpeta seleccionada.

   * Deshabilitar - Desactiva el etiquetado de color para la carpeta seleccionada.

   ![Configuración del etiquetado de color](assets/color-tags-folder.png)

## Configuración del esquema de metadatos para añadir el componente de etiquetas de color inteligente {#configure-metadata-schema}

Los esquemas de metadatos contienen campos específicos para la información específica que se debe rellenar. También contiene información de diseño para mostrar los campos de metadatos de forma sencilla. Las propiedades de metadatos incluyen título, descripción, tipos MIME, etiquetas y mucho más. Puede usar la variable [!UICONTROL Esquema de metadatos Forms] para modificar los esquemas existentes o añadir esquemas de metadatos personalizados.

>[!NOTE]
>
>El campo de etiqueta de color inteligente está disponible en el esquema de metadatos predeterminado. Si utiliza un esquema de metadatos personalizado, configure el esquema para añadir un campo de etiqueta de color inteligente.

Para agregar el componente Etiquetas de color inteligente al Editor de formularios de esquema de metadatos:

1. Vaya a **[!UICONTROL Herramientas > Recursos > Esquemas de metadatos]**.

1. Seleccione el nombre del esquema y haga clic en **[!UICONTROL Editar]**.

1. Arrastrar **[!UICONTROL Etiquetas de color inteligentes]** de la variable **[!UICONTROL Generar formulario]** para **[!UICONTROL Editor de formularios de esquema de metadatos]**.

1. Haga clic en el **[!UICONTROL Campo de etiqueta de color inteligente]** en el **[!UICONTROL Editor de formularios de esquema de metadatos]**.

1. Especifique un valor apropiado en la variable **[!UICONTROL Etiqueta de campo]** en el campo **[!UICONTROL Configuración]**  pestaña .

1. Haga clic en **[!UICONTROL Guardar]**.

   >[!VIDEO](https://video.tv.adobe.com/v/340124)

## Etiquetas de color para imágenes existentes en DAM {#color-tags-existing-images}

Las imágenes ya existentes en DAM no se etiquetan con colores automáticamente. Debe [!UICONTROL Volver a procesar recursos] manualmente para generar etiquetas de color para ellas.

Para colorear imágenes de etiquetas o carpetas (incluidas subcarpetas) de recursos que ya existen en el repositorio de recursos, siga estos pasos:

1. Seleccione el [!DNL Adobe Experience Manager] y, a continuación, seleccione los recursos en el [!UICONTROL Navegación] página.

1. Select [!UICONTROL Archivos] para mostrar la interfaz de Assets.

1. Vaya a la carpeta a la que desea aplicar etiquetas de color.

1. Seleccione toda la carpeta o imágenes específicas.

1. Select ![Icono Volver a procesar los recursos](assets/do-not-localize/reprocess-assets-icon.png) [!UICONTROL Volver a procesar recursos] y seleccione [!UICONTROL Proceso completo] .

Una vez completado el proceso, vaya a la [!UICONTROL Propiedades] de cualquier imagen de la carpeta. Las etiquetas añadidas automáticamente se ven en [!UICONTROL Etiquetas de color inteligentes] en [!UICONTROL Básico] pestaña .


## Ver etiquetas de color inteligentes para imágenes {#view-color-tags}

Para ver las etiquetas de color inteligentes de las imágenes:

1. Vaya a **[!UICONTROL Adobe Experience Manager > Assets > Archivos]**.

1. Haga clic en la carpeta adecuada y seleccione la imagen.

1. Select **[!UICONTROL Propiedades]** y vea las etiquetas en la **[!UICONTROL Etiquetas de color inteligentes]** campo .

   ![Ver etiquetas de color](assets/view-color-tags.png)

   Pase el ratón sobre una etiqueta de color para ver la **[!UICONTROL Umbral de cobertura/dominio %]** de un color en una imagen.

## Configuración del predicado de color de AEM Assets {#configure-search-predicate}

Puede configurar el filtro de búsqueda para imágenes. A continuación, puede basar los criterios de búsqueda en un color específico para filtrar los resultados.

>[!NOTE]
>
>Configure el predicado de color de AEM Assets solo si no utiliza el formulario de búsqueda predeterminado.

Para configurar el filtro de búsqueda, cree un predicado de color de recurso mediante el carril de búsqueda de administración de Assets.

Para configurar el filtro de búsqueda:

1. Vaya a **[!UICONTROL Herramientas > General > Buscar Forms]**.

1. Select **[!UICONTROL Carril de búsqueda de administración de recursos]** y haga clic en **[!UICONTROL Editar]**.

1. Arrastrar **[!UICONTROL Predicado de color de recurso]** de la variable **[!UICONTROL Seleccionar predicado]** para **[!UICONTROL Editor de formularios de búsqueda]**.

1. Especifique un valor apropiado en la variable **[!UICONTROL Etiqueta de campo]** en el campo **[!UICONTROL Configuración]**  pestaña .

1. Haga clic en **[!UICONTROL Listo]** para guardar la configuración.

   >[!VIDEO](https://video.tv.adobe.com/v/340110)

## Buscar imágenes basadas en colores {#search-images-based-on-colors}

>[!VIDEO](https://video.tv.adobe.com/v/340761)

Después de configurar todas las propiedades de etiquetado de color y [configuración del predicado de color de Assets](#search-images-based-on-colors), puede buscar imágenes basadas en un color como filtro.

Para buscar imágenes basadas en colores:

1. Vaya a **[!UICONTROL Assets > Archivos]**.

1. Select **[!UICONTROL Filtro]** en la lista desplegable.
   ![Filtrar recursos](assets/filter-assets.png)

1. Seleccione el [predicado de color de AEM Assets](#configure-search-predicate).

1. Arrastre el selector de color para seleccionar el color adecuado. El color seleccionado aparece en el campo de solo lectura disponible debajo del selector de color. Puede seleccionar RGB o HEX como formato de visualización para el color.

   ![Selector de color](assets/color-picker-color-tags.png)

   Puede filtrar imágenes en función de la selección de un color. Las imágenes que tienen el color seleccionado como una de las etiquetas de color inteligente y encima de la variable [Umbral de cobertura/dominio %](#manage-color-tagging-settings) en el panel derecho.

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
