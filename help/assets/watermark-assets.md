---
title: Marca de agua de los recursos
description: Agregue una marca de agua a los recursos digitales.
contentOwner: AG
feature: Administración de recursos,Publicación
role: User,Admin
exl-id: 210f8925-bd15-4b4a-8714-5a1486eeb49e
source-git-commit: a2c2a1f4ef4a8f0cf1afbba001d24782a6a2a24e
workflow-type: tm+mt
source-wordcount: '197'
ht-degree: 0%

---

# Marcar los recursos con agua {#watermark-assets}

[!DNL Adobe Experience Manager Assets] permite añadir una marca de agua digital a las imágenes. [!DNL Assets] admite la aplicación de una imagen como marca de agua a otros archivos de imagen. Las marcas de agua pueden ayudar a los usuarios a verificar la autenticidad y propiedad de los recursos protegida por derechos de autor. Además, se puede utilizar una marca de agua para indicar el estado de un documento como confidencial, borrador, validez, etc.

Para configurar [!DNL Experience Manager] para los recursos de marca de agua, siga estos pasos:

1. Un archivo PNG se aplica como marca de agua. Cargue este archivo en su repositorio DAM.

1. Acceda al repositorio de Git [!DNL Cloud Manager] asociado a su entorno. Confirme un archivo denominado `com.adobe.cq.assetcompute.impl.profile.WatermarkingProfileServiceImpl.cfg.json` en el repositorio con el siguiente contenido. Para obtener instrucciones, consulte [cómo realizar la configuración de OSGi en [!DNL Experience Manager] as a2/>. [!DNL Cloud Service]](/help/implementing/deploying/configuring-osgi.md)

   ```json
   {
   "watermark": "/content/dam/<path-to-watermark-image.png>",
    "width": 100
   }
   ```

1. [Cree un perfil de procesamiento ](/help/assets/asset-microservices-configure-and-use.md#create-custom-profile) para aprovechar los microservicios de recursos para aplicar la marca de agua.

   ![Perfil de procesamiento de recursos para crear una marca de agua](assets/watermark-processing-profile.png)

1. [Aplique los perfiles de procesamiento a una ](/help/assets/asset-microservices-configure-and-use.md#use-profiles) carpeta para crear recursos con marca de agua.

## Sugerencias y limitaciones {#tips-limitations-bestpractices}

* Puede utilizar una sola configuración para marcar todos los recursos. Solo se utiliza una imagen para la marca de agua y su anchura es fija.
* Puede colocar la marca de agua en el centro sin baldosas.
* No se admiten marcas de agua basadas en texto.

>[!MORELIKETHIS]
>
>* [Información general sobre los microservicios de recursos](/help/assets/asset-microservices-overview.md).
>* [Utilice microservicios de recursos con perfiles](/help/assets/asset-microservices-configure-and-use.md) de procesamiento.

