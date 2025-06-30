---
title: Colecciones de selector de recursos
description: Uso de colecciones de selectores de recursos.
role: Admin,User
exl-id: 1687e7d5-eb7e-4eb7-8747-e5dc6afacd5b
source-git-commit: 9c1104f449dc2ec625926925ef8c95976f1faf3d
workflow-type: tm+mt
source-wordcount: '449'
ht-degree: 7%

---

# Colecciones de selector de recursos {#asset-selector-collections}

Una colección es un conjunto de recursos, carpetas u otras colecciones dentro del Selector de recursos. Utilice las colecciones para compartir recursos entre los usuarios. A diferencia de las carpetas, una colección puede incluir recursos de distintas ubicaciones.

Las colecciones Micro Front-end del Selector de recursos están disponibles de forma predeterminada en modo de solo lectura. Obtiene recursos y colecciones directamente del repositorio [!DNL Experience Manager Assets] al que tiene acceso.

>[!NOTE]
>
>Asegúrese de tener permisos para acceder a [!DNL Experience Manager Assets] [imsOrg](/help/assets/asset-selector-properties.md) y colecciones.

Las colecciones Micro Front-end del Selector de recursos están disponibles de forma predeterminada en modo de solo lectura. Obtiene recursos y colecciones directamente del repositorio de Experience Manager Assets al que tiene acceso y hereda las propiedades de las carpetas públicas y privadas del repositorio de Experience Manager Assets. Ver más acerca de [crear una colección pública o privada en la vista de Assets](/help/assets/manage-collections-assets-view.md#create-collection).

Puede ver las colecciones en el Selector de recursos tanto en la vista de carril como en la vista modal.

![Colecciones en la vista de carril](assets/collections-rail-modal-view.png)

<!--
Additionally, you can [customize](/help/assets/asset-selector-customization.md) the `featureSet` property to enable or disable collections in Asset Selector. See [enable or disable Collections tab](#enable-disable-collections-tab).-->

Además, también puede personalizar la selección de recursos en la pestaña Colecciones. Para ello, puede personalizarlo con `handleSelection`. Ver [administración de la selección de Assets mediante el esquema de objetos](/help/assets/asset-selector-customization.md#handling-selection).

## Ver colecciones {#view-collections}

El Selector de recursos le permite ver colecciones en una vista de lista ![vista de lista](assets/do-not-localize/list-view.png) o en una vista de cuadrícula ![vista de cuadrícula](assets/do-not-localize/grid-view.png). Ver [tipos de vista en el Selector de recursos](overview-asset-selector.md#types-of-view).

## Arrastrar y soltar recursos en la colección {#collection-drag-and-drop}

Puede arrastrar y soltar un recurso en Colecciones directamente desde la vista [!DNL Assets as a Cloud Service] en el entorno de creación. Para ello, arrastre el recurso de la pestaña Assets al área de trabajo Colecciones de la aplicación Selector de recursos para crear aplicaciones enriquecidas.

>[!NOTE]
>
>* La función de arrastrar y soltar un recurso solo es posible en la vista de carril.
>* Solo puede arrastrar y soltar archivos (recursos), no las carpetas.

Por otro lado, también puede [habilitar o deshabilitar la función de arrastrar y soltar recursos en las colecciones](asset-selector-customization.md#enable-disable-drag-and-drop) directamente.

## Deshabilitar la selección de recursos en Colecciones {#disable-selection-collection}

Deshabilitar selección se utiliza para ocultar o deshabilitar la selección de recursos o carpetas. Oculta la casilla de verificación de selección de la tarjeta o el recurso, lo que impide que se seleccione. Ver [deshabilitar selección](/help/assets/asset-selector-customization.md#disable-selection).

## Activar o desactivar la pestaña Colecciones {#enable-disable-collections-tab}

El Selector de recursos le permite personalizar los componentes según los requisitos y la facilidad de uso. Para habilitar o deshabilitar la pestaña Colecciones en el Selector de recursos, puede usar la propiedad `featureSet` de la siguiente manera:

* **Habilitar colecciones:** Para habilitar las colecciones, debe proporcionar `collections` como valor de la matriz. De forma predeterminada, la pestaña Colecciones está habilitada de forma predeterminada para todos los usuarios. Por ejemplo, `featureSet:["collections"]`
* **Deshabilitar colecciones:** Para deshabilitar las colecciones, debe proporcionar una matriz vacía como valor. Por ejemplo, `featureSet:[ ]`

>[!MORELIKETHIS]
>
>* [Personalizaciones del Selector de recursos](/help/assets/asset-selector-customization.md)
>* [Integrar el Selector de recursos con varias aplicaciones](/help/assets/integrate-asset-selector.md)
>* [Propiedades del Selector de recursos](/help/assets/asset-selector-properties.md)
