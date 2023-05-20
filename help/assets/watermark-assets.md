---
title: Marca de agua de los recursos
description: Agregue una marca de agua a sus recursos digitales.
contentOwner: AG
feature: Asset Management,Publishing
role: User,Admin
exl-id: 210f8925-bd15-4b4a-8714-5a1486eeb49e
source-git-commit: 8bdd89f0be5fe7c9d4f6ba891d7d108286f823bb
workflow-type: tm+mt
source-wordcount: '276'
ht-degree: 8%

---

# Filigrana tus recursos {#watermark-assets}

[!DNL Adobe Experience Manager Assets] permite agregar una marca de agua digital a las imágenes. [!DNL Assets] admite la aplicación de una imagen como marca de agua a otros archivos de imagen. Las marcas de agua pueden ayudar a los usuarios a verificar la autenticidad y la propiedad de los derechos de autor de los recursos. Además, se puede utilizar una marca de agua para indicar el estado de un documento como confidencial, borrador, validez, etc.

Para configurar [!DNL Experience Manager] a los recursos de marca de agua:

1. Un archivo PNG se aplica como marca de agua. Cargue este archivo en su repositorio DAM.

1. Vaya a **[!UICONTROL Herramientas > Recursos > Configuraciones de recursos]**.

1. Clic **[!UICONTROL Perfil de marca de agua del sistema]**.

1. En el [!UICONTROL Página Perfil de Filigrana del Sistema], especifique la ruta de la imagen cargada en el repositorio de DAM en el paso 1.

1. Especifique la escala de la marca de agua, de 0,0 a 1,0, en relación con la anchura de la representación, en la **[!UICONTROL Escala]** field.

1. Haga clic en **[!UICONTROL Guardar]**.

   ![Detector de duplicación de recursos](assets/system-watermarking-profile.png)

   >[!NOTE]
   >
   >Si ha configurado el perfil de marca de agua del sistema con `com.adobe.cq.assetcompute.impl.profile.WatermarkingProfileServiceImpl.cfg.json` archivo de configuración (configuración OSGi), puede seguir utilizándolo, sin embargo, Adobe recomienda utilizar el nuevo método.


1. [Creación de un perfil de procesamiento](/help/assets/asset-microservices-configure-and-use.md#create-custom-profile) para aprovechar los microservicios de recursos para aplicar la marca de agua.

   ![Perfil de procesamiento de recursos para crear una marca de agua](assets/watermark-processing-profile.png)

   Asegúrese de habilitar la variable **[!UICONTROL Filigrana]** al crear el perfil de procesamiento.

1. [Aplicación de los perfiles de procesamiento a una carpeta](/help/assets/asset-microservices-configure-and-use.md#use-profiles) para crear recursos con marca de agua.

## Sugerencias y limitaciones {#tips-limitations-bestpractices}

* Puede utilizar una sola configuración para aplicar una marca de agua a todos los recursos. Solo se utiliza una imagen para la marca de agua y su anchura es fija.
* Puede colocar la marca de agua en el centro sin mosaicos.
* No se admiten marcas de agua basadas en texto.

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

>[!MORELIKETHIS]
>
>* [Información general sobre microservicios de recursos](/help/assets/asset-microservices-overview.md).
>* [Uso de microservicios de recursos con perfiles de procesamiento](/help/assets/asset-microservices-configure-and-use.md).

