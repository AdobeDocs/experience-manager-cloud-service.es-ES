---
title: AEM ¿Cómo crear marcas de agua para sus recursos en la?
description: AEM Obtenga información sobre cómo añadir una marca de agua digital a los recursos en la documentación de la. Las marcas de agua pueden ayudar a los usuarios a verificar la autenticidad y la propiedad de los derechos de autor de los recursos.
contentOwner: AG
feature: Asset Management,Publishing
role: User, Admin
exl-id: 210f8925-bd15-4b4a-8714-5a1486eeb49e
source-git-commit: e3fd0fe2ee5bad2863812ede2a294dd63864f3e2
workflow-type: tm+mt
source-wordcount: '343'
ht-degree: 16%

---

# Filigrana tus recursos {#watermark-assets}

| [Prácticas recomendadas de búsqueda](/help/assets/search-best-practices.md) | [Prácticas recomendadas de metadatos](/help/assets/metadata-best-practices.md) | [Centro de contenido](/help/assets/product-overview.md) | [Dynamic Media con funciones OpenAPI](/help/assets/dynamic-media-open-apis-overview.md) | [Documentación para desarrolladores de AEM Assets](https://developer.adobe.com/experience-cloud/experience-manager-apis/) |
| ------------- | --------------------------- |---------|----|-----|

| Versión | Vínculo del artículo |
| -------- | ---------------------------- |
| AEM 6.5 | [Haga clic aquí](https://experienceleague.adobe.com/docs/experience-manager-65/assets/administer/watermarking.html) |
| AEM as a Cloud Service | Este artículo |

[!DNL Adobe Experience Manager Assets] le permite agregar una marca de agua digital a imágenes y vídeos. [!DNL Assets] admite la aplicación de una imagen como marca de agua a otros archivos de imagen. Las marcas de agua pueden ayudar a los usuarios a verificar la autenticidad y la propiedad de los derechos de autor de los recursos. Además, se puede utilizar una marca de agua para indicar el estado de un documento como confidencial, borrador, validez, etc.

Para configurar [!DNL Experience Manager] en los recursos de marca de agua:

1. Un archivo PNG se aplica como marca de agua. Cargue este archivo en su repositorio DAM.

1. Vaya a **[!UICONTROL Herramientas > Assets > Configuraciones de Assets]**.

1. Haga clic en **[!UICONTROL Perfil de marca de agua del sistema]**.

1. En la [!UICONTROL página Perfil de marca de agua del sistema], especifique la ruta de acceso de la imagen cargada en el repositorio DAM en el paso 1.

1. Especifique la escala de la marca de agua, de 0,0 a 1,0, en relación con la anchura de la representación, en el campo **[!UICONTROL Escala]**.

1. Haga clic en **[!UICONTROL Guardar]**.

   ![Detector de duplicación de recursos](assets/system-watermarking-profile.png)

   >[!NOTE]
   >
   >Si ha configurado el perfil de marca de agua del sistema usando el archivo de configuración `com.adobe.cq.assetcompute.impl.profile.WatermarkingProfileServiceImpl.cfg.json` (configuración OSGi), puede seguir usándolo; sin embargo, Adobe recomienda usar el nuevo método.


1. [Cree un perfil de procesamiento](/help/assets/asset-microservices-configure-and-use.md#create-custom-profile) para usar microservicios de recursos y aplicar la marca de agua.

   ![Perfil de procesamiento de recursos para crear una marca de agua](assets/watermark-processing-profile.png)

   Asegúrese de habilitar la opción **[!UICONTROL Marca de agua]** al crear el perfil de procesamiento.

1. [Aplique los perfiles de procesamiento a una carpeta](/help/assets/asset-microservices-configure-and-use.md#use-profiles) para crear recursos con marca de agua.

## Sugerencias y limitaciones {#tips-limitations-bestpractices}

* Puede utilizar una sola configuración para aplicar una marca de agua a todos los recursos. Solo se utiliza una imagen para la marca de agua y su anchura es fija.
* Puede colocar la marca de agua en el centro sin mosaicos.
* No se admiten marcas de agua basadas en texto.

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

>[!MORELIKETHIS]
>
>* [Resumen de microservicios de recursos](/help/assets/asset-microservices-overview.md).
>* [Usar microservicios de recursos con perfiles de procesamiento](/help/assets/asset-microservices-configure-and-use.md).
