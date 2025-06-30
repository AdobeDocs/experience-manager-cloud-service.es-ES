---
title: Selector de recursos para  [!DNL Adobe Experience Manager]  as a  [!DNL Cloud Service]
description: Ejemplos de uso del Selector de recursos para personalizar según los requisitos.
role: Admin, User
exl-id: 7a393a96-f2a2-4a25-922c-577271cafc57
source-git-commit: 9c1104f449dc2ec625926925ef8c95976f1faf3d
workflow-type: tm+mt
source-wordcount: '257'
ht-degree: 54%

---


# Ejemplos de uso de las propiedades del Selector de recursos {#usage-examples}

Puede definir el Selector de recursos [properties](/help/assets/asset-selector-properties.md) en el archivo **index.html** para personalizar la visualización del Selector de recursos en su aplicación.

## Ejemplo 1: Selector de recursos en la vista de carril

![rail-view-example](assets/rail-view-example-vanilla.png)

Si el valor de AssetSelector `rail` está establecido en `false` o no se menciona en las propiedades, el Selector de recursos se muestra en la vista modal de forma predeterminada. La propiedad `acvConfig` permite algunas configuraciones en profundidad, como Arrastrar y soltar. Visite [habilitar o deshabilitar arrastrar y soltar](asset-selector-customization.md#enable-disable-drag-and-drop) para comprender el uso de la propiedad `acvConfig`.

<!--
### Example 2: Use selectedAssets property in addition to the path property

Use the `path` property to define the folder name that displays automatically when the Asset Selector is rendered. In addition, use the `selectedAssets` property to define the IDs for the assets that you need to select within the folder. Moreover, when you want to display assets that are pre-defined within the folder, you can use selectedAssets property.

   ![selected-assets-example](assets/selected-assets-example-vanilla.png)
-->

## Ejemplo 2: ventana emergente de metadatos

Utilice varias propiedades para definir los metadatos de un recurso que desee ver mediante un icono de información. La ventana emergente de información proporciona la colección de información sobre el recurso o la carpeta, incluido el título, las dimensiones, la fecha de modificación, la ubicación y la descripción de un recurso. En el ejemplo siguiente, se utilizan varias propiedades para mostrar los metadatos de un recurso, por ejemplo: la propiedad `repo:path` especifica la ubicación de un recurso. <!--`repo` represents the repository from where the asset is showing, whereas, `path` represents the route from where the asset or folder is rendered.-->

![metadata-popover-example](assets/metadata-popover.png)

## Ejemplo 3: Propiedad de filtro personalizado en la vista de carril

Además de la búsqueda con facetas, el Selector de Assets le permite personalizar varios atributos para restringir la búsqueda de [!DNL Adobe Experience Manager] como una aplicación [!DNL Cloud Service]. Agregue el siguiente código para agregar filtros de búsqueda personalizados en la aplicación. En el ejemplo siguiente, la búsqueda `Type Filter` que filtra el tipo de recurso entre imágenes, documentos o vídeos o el tipo de filtro que ha agregado para la búsqueda.

![custom-filter-example-vanilla](assets/custom-filter-example-vanilla.png)

<!--

## Customization after integrating Asset Selector 

### Custom metadata

Assets display panel shows the out of the box metadata that can be displayed in the info of the asset. In addition to this, [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] application allows configuration of the asset selector by adding custom metadata that is shown in info panel of the asset.
-->


>[!MORELIKETHIS]
>
>* [Personalizaciones del Selector de recursos](/help/assets/asset-selector-customization.md)
>* [Carga del selector de recursos](/help/assets/asset-selector-upload.md)
>* [Propiedades del Selector de recursos](/help/assets/asset-selector-properties.md)
>* [Integre el Selector de recursos con Dynamic Media con funciones de OpenAPI](/help/assets/integrate-asset-selector-dynamic-media-open-api.md)
