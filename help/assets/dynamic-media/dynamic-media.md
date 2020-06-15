---
title: Trabajar con Dynamic Media
description: Aprenda a utilizar Dynamic Media para distribuir recursos para consumo en sitios web, móviles y sociales.
translation-type: tm+mt
source-git-commit: a5e94003a3e9023155dc95ceba1a5531e4f20d8f
workflow-type: tm+mt
source-wordcount: '416'
ht-degree: 22%

---


# Trabajar con Dynamic Media {#working-with-dynamic-media}

[Dynamic Media](https://www.adobe.com/solutions/web-experience-management/dynamic-media.html) ayuda a proporcionar bajo demanda recursos de marketing y mercadotecnia de rico contenido visual, escalados automáticamente para el consumo en la Web, dispositivos móviles y redes sociales. Con un conjunto de recursos de origen principales, Dynamic Media genera y ofrece múltiples variaciones de contenido enriquecido en tiempo real a través de su red global, escalable y optimizada para el rendimiento.

Dynamic Media proporciona experiencias de visualización interactivas, que incluyen zoom, giro de 360 grados y vídeo. Dynamic Media introduce de forma exclusiva los flujos de trabajo de la solución de administración de recursos digitales (Recursos) de Adobe Experience Manager para simplificar y agilizar el proceso de administración de campañas digitales.

>[!NOTE]
>
>Hay un artículo de la comunidad disponible en [Trabajo con Adobe Experience Manager y Dynamic Media](https://helpx.adobe.com/experience-manager/using/aem_dynamic_media.html).

## Qué puede hacer con Dynamic Media {#what-you-can-do-with-dynamic-media}

Dynamic Media permite administrar los recursos antes de publicarlos. El trabajo con recursos en general se trata en detalle en [Uso de recursos](/help/assets/manage-digital-assets.md)digitales. Los temas generales incluyen la carga, descarga, edición y publicación de recursos; visualización y edición de propiedades y búsqueda de recursos.

Las funciones solo para Dynamic Media incluyen lo siguiente:

* [Banner de carrusel](carousel-banners.md)
* [Conjuntos de imágenes](image-sets.md)
* [Imágenes interactivas](interactive-images.md)
* [Vídeos interactivos](interactive-videos.md)
* [Conjuntos de medios mixtos](mixed-media-sets.md)
* [Imágenes panorámicas](panoramic-images.md)

* [Conjuntos de giros](spin-sets.md)
* [Vídeo](video.md)
* [Envío de recursos de Dynamic Media](delivering-dynamic-media-assets.md)
* [Administración de recursos](managing-assets.md)
* [Usar las vistas rápidas para crear ventanas emergentes personalizadas](custom-pop-ups.md)

Consulte también [Configuración de Dynamic Media](administering-dynamic-media.md).

<!-- 

OBSOLETE UNTIL INTEGRATING SCENE7 TOPIC GETS A MAJOR UPDATE
>[!NOTE]
>
>To understand the differences between using Dynamic Media and integrating Dynamic Media Classic with AEM, see [Dynamic Media Classic integration versus Dynamic Media](/help/sites-cloud/administering/integrating-scene7.md#aem-scene-integration-versus-dynamic-media).

-->

## Dynamic Media habilitado frente a Dynamic Media deshabilitado {#dynamic-media-on-versus-dynamic-media-off}

Puede saber si Dynamic Media está habilitado (activado) según las características siguientes:

* Las representaciones dinámicas están disponibles al descargar o previsualizar recursos.
* Hay disponibles conjuntos de imágenes, conjuntos de giros y conjuntos de medios mixtos.
* Se crean representaciones PTIFF.

Al hacer clic en un recurso de imagen, la vista del recurso es diferente con Dynamic Media activado. Dynamic Media utiliza los visores HTML5 a petición.

### Representaciones dinámicas {#dynamic-renditions}

Las representaciones dinámicas, como los ajustes preestablecidos de imagen y visor (en **[!UICONTROL Dinámico]**), están disponibles cuando Dynamic Media está activado.

![chlimage_1-358](assets/chlimage_1-358.png)

### Conjuntos de imágenes, conjuntos de giros, conjuntos de medios mixtos {#image-sets-spins-sets-mixed-media-sets}

Los conjuntos de imágenes, conjuntos de giros y conjuntos de medios mixtos están disponibles si Dynamic Media está activado.

![chlimage_1-359](assets/chlimage_1-359.png)

### Representaciones PTIFF {#ptiff-renditions}

Los recursos habilitados para Dynamic Media incluyen `pyramid.tiffs`.

![chlimage_1-360](assets/chlimage_1-360.png)

### Cambio de vistas de recursos {#asset-views-change}

Con Dynamic Media activado, puede acercar y alejar haciendo clic en los botones `+` y `-` . También puede tocar o hacer clic para acercar cierta área. Revertir le lleva a la versión original y puede hacer que la imagen esté a pantalla completa haciendo clic en las flechas diagonales. Dynamic Media habilitado tiene este aspecto:

![chlimage_1-361](assets/chlimage_1-361.png)

Con Dynamic Media desactivado, puede acercar y alejar y volver al tamaño original:

![chlimage_1-362](assets/chlimage_1-362.png)
