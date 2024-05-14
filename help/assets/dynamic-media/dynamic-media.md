---
title: Trabajo con Dynamic Media
description: Aprenda a utilizar Dynamic Media para entregar recursos para su consumo en sitios web, móviles y sociales.
contentOwner: Rick Brough
feature: Dynamic Media,Asset Management
role: Admin,User
exl-id: 3ec3cb85-88ce-4277-a45c-30e52c75ed42
source-git-commit: 26afff3a39a2a80c1f730287b99f3fb33bff0673
workflow-type: tm+mt
source-wordcount: '398'
ht-degree: 6%

---

# Trabajo con Dynamic Media {#working-with-dynamic-media}

[Dynamic Media](https://business.adobe.com/products/experience-manager/assets/dynamic-media.html) ayuda a ofrecer recursos de marketing y comercialización visuales enriquecidos bajo demanda, escalados automáticamente para el consumo en sitios web, móviles y sociales. Con un conjunto de recursos de origen primarios, Dynamic Media genera y ofrece varias variaciones de contenido enriquecido en tiempo real a través de su red global, escalable y optimizada para el rendimiento.

Dynamic Media ofrece experiencias de visualización interactivas, como zoom, giro de 360° y vídeo. Dynamic Media incorpora de forma exclusiva los flujos de trabajo de la solución de administración de activos digitales (Assets) de Adobe Experience Manager para simplificar y optimizar el proceso de administración de campañas digitales.

<!-- >[!NOTE]
>
>A Community article is available on [Working with Adobe Experience Manager and Dynamic Media](https://helpx.adobe.com/experience-manager/using/aem_dynamic_media.html). -->

## Qué puede hacer con Dynamic Media {#what-you-can-do-with-dynamic-media}

Dynamic Media permite administrar los recursos antes de publicarlos. La forma de trabajar con recursos en general se explica detalladamente en [Uso de recursos digitales](/help/assets/manage-digital-assets.md). Los temas generales incluyen cargar, descargar, editar y publicar recursos; ver y editar propiedades y buscar recursos.

Las funciones solo de Dynamic Media incluyen lo siguiente:

* [Banner de carrusel](carousel-banners.md)
* [Conjuntos de imágenes](image-sets.md)
* [Imágenes interactivas](interactive-images.md)
* [Vídeos interactivos](interactive-videos.md)
* [Conjuntos de medios mixtos](mixed-media-sets.md)
* [Imágenes panorámicas](panoramic-images.md)

* [Conjuntos de giros](spin-sets.md)
* [Vídeo](video.md)
* [Entrega de recursos de Dynamic Media](delivering-dynamic-media-assets.md)
* [Administración de recursos](managing-assets.md)
* [Uso de las vistas rápidas para crear ventanas emergentes personalizadas](custom-pop-ups.md)

Consulte también [Configuración de Dynamic Media](administering-dynamic-media.md).

<!-- 

OBSOLETE UNTIL INTEGRATING SCENE7 TOPIC GETS A MAJOR UPDATE
>[!NOTE]
>
>To understand the differences between using Dynamic Media and integrating Dynamic Media Classic with AEM, see [Dynamic Media Classic integration versus Dynamic Media](/help/sites-cloud/administering/integrating-scene7.md#aem-scene-integration-versus-dynamic-media).

-->

## Dynamic Media habilitado frente a Dynamic Media deshabilitado {#dynamic-media-on-versus-dynamic-media-off}

Puede comprobar si Dynamic Media está habilitado (activado) por las siguientes características:

* Las representaciones dinámicas están disponibles al descargar o previsualizar recursos.
* Hay disponibles conjuntos de imágenes, conjuntos de giros y conjuntos de medios mixtos.
* Se crean representaciones PTIFF.

Al hacer clic en un recurso de imagen, la vista del recurso es diferente con Dynamic Media habilitado. Dynamic Media utiliza los visores de HTML5 bajo demanda.

### Representaciones dinámicas {#dynamic-renditions}

Representaciones dinámicas como ajustes preestablecidos de imagen y visor (en **[!UICONTROL Dinámico]**) están disponibles cuando Dynamic Media está habilitado.

![chlimage_1-358](assets/chlimage_1-358.png)

### Conjuntos de imágenes, conjuntos de giros y conjuntos de medios mixtos {#image-sets-spins-sets-mixed-media-sets}

Los conjuntos de imágenes, los conjuntos de giros y los conjuntos de medios mixtos están disponibles si Dynamic Media está habilitado.

![chlimage_1-359](assets/chlimage_1-359.png)

### Representaciones PTIFF {#ptiff-renditions}

Los recursos habilitados para Dynamic Media incluyen `pyramid.tiffs`.

![chlimage_1-360](assets/chlimage_1-360.png)

### Cambio de vistas de recursos {#asset-views-change}

Con Dynamic Media habilitado, puede acercar y alejar la imagen haciendo clic en el icono `+` y `-` botones. También puede seleccionar para ampliar una zona determinada. Revertir le lleva a la versión original y puede hacer que la imagen de pantalla completa haciendo clic en las flechas diagonales. Dynamic Media habilitado aparece de la siguiente manera:

![chlimage_1-361](assets/chlimage_1-361.png)

Con Dynamic Media deshabilitado, puede aumentar y reducir el tamaño y volver al original:

![chlimage_1-362](assets/chlimage_1-362.png)
