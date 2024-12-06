---
title: Ver y administrar representaciones en Experience Manager Assets
description: Descubra cómo los AEM Assets y Dynamic Media simplifican la administración eficaz de imágenes con representaciones de imágenes estáticas y dinámicas.
exl-id: 006dc493-c400-4d0f-b314-c1978582b7fb
feature: Renditions
role: User
source-git-commit: eb5886b5ed6a6f5b52303b4fccf5c266178b36f8
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Ver y administrar representaciones en Experience Manager Assets{#renditions}

| [Prácticas recomendadas de búsqueda](/help/assets/search-best-practices.md) | [Prácticas recomendadas de metadatos](/help/assets/metadata-best-practices.md) | [Centro de contenido](/help/assets/product-overview.md) | [Dynamic Media con funciones de OpenAPI](/help/assets/dynamic-media-open-apis-overview.md) | [Documentación de desarrollador de AEM Assets](https://developer.adobe.com/experience-cloud/experience-manager-apis/) |
| ------------- | --------------------------- |---------|----|-----|

Las representaciones en Adobe Experience Manager AEM () son versiones personalizadas de recursos digitales, como imágenes, diseñadas para diferentes dispositivos y plataformas a fin de garantizar un rendimiento óptimo. AEM La creación y administración de estas representaciones facilita la creación y la mejora de la experiencia del usuario. Puede crear miniaturas, optimizar imágenes para la web o dispositivos móviles, añadir marcas de agua, ver y descargar representaciones dinámicas o representaciones de recortes inteligentes y mucho más.

Los ajustes preestablecidos de imagen de Dynamic Media y las representaciones de recorte inteligente promueven una administración sistemática de imágenes que se ajusta a los estándares de la marca y maximizan la cohesión de la marca. Esto simplifica el proceso de localización y uso rápidos de representaciones de imágenes dinámicas según sea necesario sin acceso de administrador.

Las representaciones se clasifican como estáticas y dinámicas; cada tipo presenta funciones y capacidades únicas que se analizan con más detalle.

## Representaciones estáticas {#static-renditions}

Las representaciones estáticas son versiones generadas previamente de recursos digitales, que generalmente se crean durante la ingesta o modificación de recursos. Estas representaciones están optimizadas para propósitos y plataformas específicos, como miniaturas web, formatos compatibles con dispositivos móviles para un diseño interactivo o versiones de alta resolución para la impresión, lo que garantiza una experiencia eficiente y coherente.
Obtenga información sobre cómo [ver y descargar representaciones estáticas](#view-and-download-static-renditions) en Experience Manager Assets.

### Ver y descargar representaciones estáticas{#view-and-download-static-renditions}

Para ver las representaciones de recursos y descargarlas, siga estos pasos:

1. En la vista Assets, haz clic en **Assets**, navega a una carpeta, selecciona un recurso y haz clic en **Detalles**.
1. Haga clic en el icono de la representación, disponible en el panel derecho.
1. Seleccione una representación para previsualizarla y haga clic en ![icono de descarga](/help/assets/assets/download-icon.svg) para descargarla.

   ![Ver y descargar representaciones dinámicas](/help/assets/assets/view-download-static-rendition.png)

## Representaciones dinámicas {#dynamic-renditions}

Las representaciones dinámicas son versiones personalizadas de recursos creados en tiempo real para satisfacer necesidades específicas, como cambiar el tamaño de las imágenes en función de la resolución del dispositivo o recortarlas para adaptarlas a diferentes relaciones de aspecto.
Estas representaciones permiten a las organizaciones ofrecer experiencias personalizadas y optimizadas para diversas necesidades de audiencia. Puede ver y descargar representaciones dinámicas en Experience Manager Assets.

## Representaciones de Dynamic Media {#dynamic-media-renditions}

### Antes de empezar

* AEM Debe ser un usuario de Dynamic Media con licencia para la administración de licencias.
* Use la [!UICONTROL vista de administrador] para configurar:
   * [Perfiles de imagen de recorte inteligente](/help/assets/dynamic-media/image-profiles.md#creating-image-profiles)
   * [Ajustes preestablecidos de imagen](/help/assets/dynamic-media/managing-image-presets.md)

  Puede [cambiar la vista](/help/assets/assets-view-introduction.md#how-to-access-assets-view) más adelante para obtener una vista previa de las representaciones dinámicas en la vista de Assets.
* Recursos de Publish a Dynamic Media para que las representaciones de Dynamic Media estén disponibles en la vista de Assets. Para obtener más información, consulte [Publish Assets AEM to y Dynamic Media](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/assets-view/publish-assets-to-aem-and-dm).


### Ver y descargar representaciones de Dynamic Media {#view-download-dm-renditions}

Para ver o descargar representaciones dinámicas de imágenes en Experience Manager Assets, siga estos pasos:

1. Vaya a **[!UICONTROL Administración de Assets]** > **[!UICONTROL Assets]**.

1. Vaya a la carpeta de recursos aplicable.

1. Haga clic en el recurso que necesita ver y haga clic en **[!UICONTROL Detalles]**.

1. En el menú derecho, haga clic en el icono **[!UICONTROL Dynamic Media]**. El panel **[!UICONTROL Dynamic Media]** muestra representaciones de Dynamic Media y recortes inteligentes.

   ![representaciones dinámicas](/help/assets/assets/dm-scene7-renditions.png)
   <!-- ![dynamic renditions](assets/preset_smart_crop_view.png) -->

1. Seleccione la representación que desea previsualizar y haga clic en **Copiar URL** para copiar la URL de la representación seleccionada. Haga clic en **Descargar representación** para descargar las representaciones de los recursos de imagen.
1. Seleccione la representación de recorte inteligente que quiera previsualizar y haga clic en **Copiar URL** para copiar la URL de la representación seleccionada.
1. Haga clic en ![icono de descarga](assets/do-not-localize/download-icon.png) para descargar todas las representaciones de recortes inteligentes disponibles como un solo archivo zip.
   ![icono de descarga](/help/assets/assets/smartcrop-rendition.png)

   >[!NOTE]
   >
   >Estas representaciones solo están disponibles para los recursos de imagen.

## Dynamic Media con representaciones de funciones OpenAPI {#dm-with-openapi-renditions}

### Antes de empezar

* AEM Debe ser un usuario de Dynamic Media con licencia para la administración de licencias.
* Assets debe aprobarse para mostrar Dynamic Media con representaciones de funcionalidades de OpenAPI. Para obtener más información, consulte [Aprobar recursos en Experience Manager](/help/assets/approve-assets.md#copy-delivery-url-approved-assets)
* Dynamic Media con capacidades de OpenAPI debe estar habilitado en la instancia de AEM as a Cloud Service.

### Ver Dynamic Media con representaciones de capacidades de OpenAPI {#view-download-dm-with-openapi-renditions}

1. Seleccione el recurso y haga clic en **Detalles**.
1. Haga clic en el icono Dynamic Media, disponible en el panel derecho. El panel Dynamic Media muestra la representación de Dynamic Media con capacidades OpenAPI para todos los tipos de recursos.
   ![icono de descarga](/help/assets/assets/dm-with-open-api-copy-url.png)
1. Seleccione la opción **Dynamic Media con OpenAPI** y, a continuación, haga clic en **Copiar URL** para copiar la URL de entrega del recurso.


