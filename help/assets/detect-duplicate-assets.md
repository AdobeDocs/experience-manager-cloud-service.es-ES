---
title: Detectar recursos duplicados para [!DNL Adobe Experience Manager] as a [!DNL Cloud Service]
description: Obtenga información sobre cómo detectar recursos duplicados
contentOwner: KK
mini-toc-levels: 3
feature: Asset Management, Publishing,Collaboration, Asset Processing
role: User, Architect, Admin
exl-id: 40f63933-4f4e-4318-8d42-4b5c9b01f7cd
source-git-commit: e3fd0fe2ee5bad2863812ede2a294dd63864f3e2
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 10%

---


# Detección de recursos duplicados {#detect-duplicate-assets}

| [Prácticas recomendadas de búsqueda](/help/assets/search-best-practices.md) | [Prácticas recomendadas de metadatos](/help/assets/metadata-best-practices.md) | [Centro de contenido](/help/assets/product-overview.md) | [Dynamic Media con funciones OpenAPI](/help/assets/dynamic-media-open-apis-overview.md) | [Documentación para desarrolladores de AEM Assets](https://developer.adobe.com/experience-cloud/experience-manager-apis/) |
| ------------- | --------------------------- |---------|----|-----|

| Versión | Vínculo del artículo |
| -------- | ---------------------------- |
| AEM 6.5 | [Haga clic aquí](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/duplicate-detection.html?lang=en) |
| AEM as a Cloud Service | Este artículo |

Si un usuario de DAM carga uno o más recursos que ya existen en el repositorio, [!DNL Experience Manager] detecta la duplicación y se lo comunica al usuario. La detección de duplicados está desactivada de forma predeterminada, ya que puede afectar al rendimiento según el tamaño del repositorio y el número de recursos cargados.

Para habilitar la función:

1. Vaya a **[!UICONTROL Herramientas > Assets > Configuraciones de Assets]**.

1. Haga clic en **[!UICONTROL Detector de duplicación de recursos]**.

1. En la [!UICONTROL página Detector de duplicación de recursos], haga clic en **[!UICONTROL Habilitado]**.

   El valor `dam:sha1` del campo Detectar metadatos garantiza que se detecten recursos duplicados aunque los nombres de archivo sean diferentes.

1. Haga clic en **[!UICONTROL Guardar]**.

   ![Detector de duplicación de recursos](assets/asset-duplication-detector.png)

>[!NOTE]
>
>Si ha configurado el detector de duplicación usando el archivo de configuración `/apps/example/config.author/com.adobe.cq.assetcompute.impl.assetprocessor.AssetDuplicationDetector.cfg.json` (configuración OSGi), puede seguir usándolo; sin embargo, el Adobe recomienda usar el nuevo método.


Una vez activado, el Experience Manager envía notificaciones de recursos duplicados a la bandeja de entrada del Experience Manager. Es un resultado agregado para varios duplicados. Los usuarios pueden optar por eliminar los recursos en función de los resultados.

![Notificación de la bandeja de entrada para recursos duplicados](assets/duplicate-detect-inbox-notification.png)

>[!NOTE]
>
>Al cargar recursos en el repositorio, Experience Manager detecta la duplicación y le notifica sobre los 100 primeros recursos duplicados.
