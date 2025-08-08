---
title: Trabajar con Dynamic Media
description: Obtenga información sobre qué es Dynamic Media y puede utilizarlo para entregar recursos para su consumo en sitios web, móviles y sociales.
contentOwner: Rick Brough
feature: Dynamic Media,Asset Management
role: Admin,User
exl-id: 3ec3cb85-88ce-4277-a45c-30e52c75ed42
source-git-commit: bc422429d4a57bbbf89b7af2283b537a1f516ab5
workflow-type: tm+mt
source-wordcount: '655'
ht-degree: 3%

---

# Trabajar con Dynamic Media {#working-with-dynamic-media}

[Dynamic Media](https://business.adobe.com/products/experience-manager/assets/dynamic-media.html) ayuda a ofrecer recursos de marketing y comercialización visual enriquecidos bajo demanda, escalados automáticamente para el consumo en sitios web, móviles y sociales. Al utilizar un conjunto de recursos de origen principales, Dynamic Media genera y ofrece varias variaciones de contenido enriquecido en tiempo real a través de su red global, escalable y optimizada para el rendimiento.

Dynamic Media ofrece experiencias de visualización interactivas, como zoom, giro de 360° y vídeo. Dynamic Media incorpora de forma exclusiva los flujos de trabajo de la solución Adobe Experience Manager digital asset management (Assets) para simplificar y optimizar el proceso de administración de campañas digitales.

<!-- 
>[!NOTE]
>
>A Community article is available on [Working with Adobe Experience Manager and Dynamic Media](https://helpx.adobe.com/experience-manager/using/aem_dynamic_media.html). 
-->

## ¿Qué es Dynamic Media?

Dynamic Media en Adobe Experience Manager (AEM) as a Cloud Service es una potente solución diseñada para ayudarle a administrar, entregar y optimizar recursos de medios enriquecidos como imágenes y vídeos en plataformas digitales. Transforma los medios estáticos en experiencias atractivas y dinámicas, ya que permite realizar modificaciones en tiempo real, como cambiar el tamaño, recortar y ajustar la calidad en función del dispositivo o del tamaño de pantalla del usuario. Con Dynamic Media, los recursos se adaptan automáticamente para proporcionar la mejor experiencia visual, ya sean usuarios de escritorio, móviles o tabletas.

Una ventaja importante de Dynamic Media es su capacidad para optimizar la administración de medios. No es necesario crear varias versiones de imágenes o vídeos: Dynamic Media se encarga de todo proporcionando el formato más adecuado para cada situación. Por ejemplo, las empresas de comercio electrónico pueden aprovechar las vistas de 360 grados de los productos o las imágenes ampliables para crear experiencias interactivas, mientras que los sitios web con contenido elevado pueden garantizar una transmisión de vídeo rápida y de alta calidad. Esto resulta en tiempos de carga más rápidos y experiencias de usuario más atractivas, lo que a la larga conduce a una mayor satisfacción del cliente y mejores tasas de conversión.

Dynamic Media se integra perfectamente con su sistema de administración de activos digitales (DAM) en AEM, lo que le ofrece una única plataforma para almacenar, organizar e implementar sus medios. Este enfoque centralizado simplifica la colaboración entre equipos y proporciona información en tiempo real sobre el rendimiento de los recursos. Tanto si se centra en ofrecer imágenes cautivadoras como en mejorar las interacciones de los usuarios impulsadas por los medios, Dynamic Media ayuda a optimizar el contenido para cualquier canal, lo que lo convierte en una herramienta esencial para las empresas que buscan aumentar su presencia digital.

## Qué puede hacer con Dynamic Media {#what-you-can-do-with-dynamic-media}

Dynamic Media le permite administrar sus recursos antes de publicarlos. [Trabajar con Assets digital](/help/assets/manage-digital-assets.md) explica en detalle cómo trabajar con recursos en general. Los temas generales incluyen cargar, descargar, editar y publicar recursos; ver y editar propiedades y buscar recursos.

Las funciones solo de Dynamic Media incluyen lo siguiente:

* [Banner de carrusel](carousel-banners.md)
* [Conjuntos de imágenes](image-sets.md)
* [Imágenes interactivas](interactive-images.md)
* [Vídeos interactivos](interactive-videos.md)
* [Conjuntos de medios mixtos](mixed-media-sets.md)
* [Imágenes panorámicas](panoramic-images.md)
* [Conjuntos de giros](spin-sets.md)
* [Vídeo](video.md)
* [Entrega de Dynamic Media Assets](delivering-dynamic-media-assets.md)
* [Administración de Assets](managing-assets.md)
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

Al hacer clic en un recurso de imagen, la vista del recurso es diferente con Dynamic Media habilitado. Dynamic Media utiliza los visores HTML5 bajo demanda.

### Representaciones dinámicas {#dynamic-renditions}

Las representaciones dinámicas, como los ajustes preestablecidos de imagen y visor (en **[!UICONTROL Dynamic]**), están disponibles cuando Dynamic Media está habilitado.

![chlimage_1-358](assets/chlimage_1-358.png)

### Conjuntos de imágenes de Dynamic Media, conjuntos de giros y conjuntos de medios mixtos {#image-sets-spins-sets-mixed-media-sets}

Los conjuntos de imágenes, los conjuntos de giros y los conjuntos de medios mixtos están disponibles si Dynamic Media está habilitado.

![chlimage_1-359](assets/chlimage_1-359.png)

### Representaciones PTIFF habilitadas para Dynamic Media {#ptiff-renditions}

Los recursos habilitados para Dynamic Media incluyen `pyramid.tiffs`.

![chlimage_1-360](assets/chlimage_1-360.png)

### Cambio de las vistas de recursos de Dynamic Media {#asset-views-change}

Con Dynamic Media habilitado, puede acercar y alejar haciendo clic en los botones `+` y `-`. También puede seleccionar para ampliar una zona determinada. Revertir le lleva a la versión original y puede hacer que la imagen de pantalla completa haciendo clic en las flechas diagonales. Dynamic Media habilitado aparece de la siguiente manera:

![chlimage_1-361](assets/chlimage_1-361.png)

Con Dynamic Media desactivado, puede acercar y alejar el contenido y volver al tamaño original:

![chlimage_1-362](assets/chlimage_1-362.png)
