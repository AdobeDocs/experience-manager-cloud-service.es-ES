---
title: Administre recursos digitales
description: Obtenga información sobre cómo detectar recursos duplicados
contentOwner: KK
mini-toc-levels: 3
feature: Asset Management,Publishing,Collaboration,Asset Processing
role: User,Architect,Admin
exl-id: 40f63933-4f4e-4318-8d42-4b5c9b01f7cd
source-git-commit: 237b4a8e01af74dbaac0ba1715b5fa95c931be7c
workflow-type: tm+mt
source-wordcount: '182'
ht-degree: 4%

---

# Detección de recursos duplicados {#detect-duplicate-assets}

Si un usuario DAM carga uno o más recursos que ya existen en el repositorio, [!DNL Experience Manager] detecta la duplicación y se lo comunica al usuario. La detección de duplicados está desactivada de forma predeterminada, ya que puede afectar al rendimiento según el tamaño del repositorio y el número de recursos cargados.

Para habilitar la función:

1. Vaya a **[!UICONTROL Herramientas > Recursos > Configuraciones de recursos]**.

1. Clic **[!UICONTROL Detector de duplicación de recursos]**.

1. En el [!UICONTROL Página Detector de duplicación de recursos], haga clic en **[!UICONTROL Habilitado]**.

   `dam:sha1` El valor del campo Detectar metadatos garantiza que se detecten recursos duplicados aunque los nombres de archivo sean diferentes.

1. Haga clic en **[!UICONTROL Guardar]**.

   ![Detector de duplicación de recursos](assets/asset-duplication-detector.png)

>[!NOTE]
>
>Si ha configurado el detector de duplicación con `/apps/example/config.author/com.adobe.cq.assetcompute.impl.assetprocessor.AssetDuplicationDetector.cfg.json` archivo de configuración (configuración OSGi), puede seguir utilizándolo, sin embargo, Adobe recomienda utilizar el nuevo método.


Una vez activado, el Experience Manager envía notificaciones de recursos duplicados a la bandeja de entrada del Experience Manager. Es un resultado agregado para varios duplicados. Los usuarios pueden optar por eliminar los recursos en función de los resultados.

![Notificación de bandeja de entrada para recursos duplicados](assets/duplicate-detect-inbox-notification.png)

>[!NOTE]
>
>Al cargar recursos en el repositorio, Experience Manager detecta la duplicación y le notifica sobre los 100 primeros recursos duplicados.
