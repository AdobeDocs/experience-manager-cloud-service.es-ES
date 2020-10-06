---
title: Marcar como agua los recursos
description: Añada una marca de agua en los recursos digitales.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 7ea7af1cf784b6866f3c2484475a8072ff76be2c
workflow-type: tm+mt
source-wordcount: '198'
ht-degree: 0%

---


# Marcar los recursos como agua {#watermark-assets}

[!DNL Adobe Experience Manager Assets] permite agregar una marca de agua digital a las imágenes. [!DNL Assets] admite la aplicación de una imagen como marca de agua a otros archivos de imagen. Las marcas de agua pueden ayudar a los usuarios a verificar la autenticidad y propiedad de los derechos de autor de los recursos. Además, se puede utilizar una marca de agua para indicar el estado de un documento como confidencial, borrador, validez, etc.

Para configurar [!DNL Experience Manager] los recursos de marca de agua, siga estos pasos:

1. Un archivo PNG se aplica como marca de agua. Cargue este archivo en el repositorio de DAM.

1. Acceda al repositorio de [!DNL Cloud Manager] Git asociado con su entorno. Transfiera un archivo denominado `com.adobe.cq.assetcompute.impl.profile.WatermarkingProfileServiceImpl.json` en su repositorio [!DNL Cloud Manager] Git con el siguiente contenido. Para obtener más información, consulte [cómo realizar la configuración de OSGi [!DNL Experience Manager] en un Cloud Service](/help/implementing/deploying/configuring-osgi.md).

   ```json
   {
   "watermark": "/content/dam/<path-to-watermark-image.png>",
    "width": 100
   }
   ```

1. [Cree un perfil](/help/assets/asset-microservices-configure-and-use.md#create-custom-profile) de procesamiento para aprovechar los microservicios de recursos para aplicar la marca de agua.

   ![Perfil de procesamiento de recursos para crear una marca de agua](assets/watermark-processing-profile.png)

1. [Aplique los perfiles de procesamiento a una carpeta](/help/assets/asset-microservices-configure-and-use.md#use-profiles) para crear recursos con marcas de agua.

## Sugerencias y limitaciones {#tips-limitations-bestpractices}

* Puede utilizar una sola configuración para marcar todos los recursos como agua. Solo se utiliza una imagen para la marca de agua y su ancho es fijo.
* Se puede colocar la marca de agua en el centro sin baldosas.
* No se admiten marcas de agua basadas en texto.

>[!MORELIKETHIS]
>
>* [Información general](/help/assets/asset-microservices-overview.md)sobre los microservicios de recursos.
>* [Utilice microservicios de recursos con perfiles](/help/assets/asset-microservices-configure-and-use.md)de procesamiento.

