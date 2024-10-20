---
title: Ver y administrar representaciones en Experience Manager Assets
description: Descubra cómo AEM Assets y Dynamic Media simplifican la administración eficaz de imágenes con representaciones de imágenes estáticas y dinámicas.
exl-id: 006dc493-c400-4d0f-b314-c1978582b7fb
feature: Renditions
role: User
source-git-commit: e3fd0fe2ee5bad2863812ede2a294dd63864f3e2
workflow-type: tm+mt
source-wordcount: '453'
ht-degree: 1%

---

# Ver y administrar representaciones en Experience Manager Assets{#renditions}

| [Prácticas recomendadas de búsqueda](/help/assets/search-best-practices.md) | [Prácticas recomendadas de metadatos](/help/assets/metadata-best-practices.md) | [Centro de contenido](/help/assets/product-overview.md) | [Dynamic Media con funciones OpenAPI](/help/assets/dynamic-media-open-apis-overview.md) | [Documentación para desarrolladores de AEM Assets](https://developer.adobe.com/experience-cloud/experience-manager-apis/) |
| ------------- | --------------------------- |---------|----|-----|

Las representaciones en Adobe Experience Manager AEM () son versiones personalizadas de recursos digitales, como imágenes, diseñadas para diferentes dispositivos y plataformas a fin de garantizar un rendimiento óptimo. AEM La creación y administración de estas representaciones facilita la creación y la administración, lo que mejora la experiencia del usuario. Puede crear miniaturas, optimizar imágenes para la web o dispositivos móviles, añadir marcas de agua, ver y descargar representaciones dinámicas o representaciones de recortes inteligentes y mucho más.

Los ajustes preestablecidos de imagen de Dynamic Media y las representaciones de recorte inteligente promueven una administración sistemática de imágenes que se ajusta a los estándares de la marca y maximizan la cohesión de la marca. Esto simplifica el proceso de localización y uso rápidos de representaciones de imágenes dinámicas según sea necesario sin acceso de administrador.

Las representaciones se clasifican como estáticas y dinámicas; cada tipo presenta funciones y capacidades únicas que se analizan con más detalle.

## Representaciones estáticas {#static-renditions}

Las representaciones estáticas son versiones generadas previamente de recursos digitales, que generalmente se crean durante la ingesta o modificación de recursos. Estas representaciones están optimizadas para propósitos y plataformas específicos, como miniaturas web, formatos compatibles con dispositivos móviles para un diseño interactivo o versiones de alta resolución para la impresión, lo que garantiza una experiencia eficiente y coherente.
Obtenga información sobre [cómo ver y descargar](#view-dynamic-renditions) representaciones estáticas en [!DNL Experience Manager Assets].

## Representaciones dinámicas {#dynamic-renditions}

Las representaciones dinámicas son versiones personalizadas de recursos creados en tiempo real para satisfacer necesidades específicas, como cambiar el tamaño de las imágenes en función de la resolución del dispositivo o recortarlas para adaptarlas a diferentes relaciones de aspecto.
Estas representaciones permiten a las organizaciones ofrecer experiencias personalizadas y optimizadas para diversas necesidades de audiencia. Puede ver y descargar representaciones dinámicas en [!DNL Experience Manager Assets].

### Antes de empezar

* AEM Debe ser un usuario de Dynamic Media con licencia para la administración de licencias.

* Use [!UICONTROL vista de administrador] para configurar:
   * [Perfiles de imagen de recorte inteligente](/help/assets/dynamic-media/image-profiles.md#creating-image-profiles)
   * [Ajustes preestablecidos de imagen](/help/assets/dynamic-media/managing-image-presets.md)

  Puede [cambiar la vista](/help/assets/assets-view-introduction.md#how-to-access-assets-view) más adelante para obtener una vista previa de las representaciones dinámicas en la vista de Assets.

### Ver y descargar representaciones dinámicas {#view-renditions}

Para ver o descargar representaciones dinámicas de imágenes en [!DNL Experience Manager Assets], siga estos pasos:

1. Vaya a **[!UICONTROL Administración de Assets]** > **[!UICONTROL Assets]**.

1. Vaya a la carpeta de recursos aplicable.

1. Haga clic en la imagen que necesita ver y haga clic en **[!UICONTROL Detalles]**.

1. En el menú derecho, haga clic en **[!UICONTROL Representaciones]**. <br> El panel **[!UICONTROL Representaciones]** se abre con las representaciones **[!UICONTROL Dinámicas]** y **[!UICONTROL Recorte inteligente]** disponibles.

   ![representaciones dinámicas](assets/preset_smart_crop.png)
   <!-- ![dynamic renditions](assets/preset_smart_crop_view.png) -->

1. Haga clic en la representación que necesite ver o descargar.

1. Haga clic en el icono ![descargar](assets/do-not-localize/download-icon.png) junto a la representación dinámica que debe descargar. <br> También puede seleccionar la representación de la imagen y hacer clic en la opción **[!UICONTROL Descargar representación]** en la parte inferior.

   Puede hacer clic en el icono ![descargar](assets/do-not-localize/download-icon.png) que se encuentra disponible en la parte superior de la sección **[!UICONTROL Recorte inteligente]** de representaciones para descargar todas las representaciones de recorte inteligente disponibles para ese recurso.

>[!NOTE]
>
>Las representaciones dinámicas solo son visibles si los recursos se cargan desde la vista Administrador.
