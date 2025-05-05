---
title: Detectar recursos duplicados para [!DNL Adobe Experience Manager] as a [!DNL Cloud Service]
description: Obtenga información sobre cómo detectar recursos duplicados
contentOwner: KK
mini-toc-levels: 3
feature: Asset Management, Publishing,Collaboration, Asset Processing
role: User, Architect, Admin
exl-id: 40f63933-4f4e-4318-8d42-4b5c9b01f7cd
source-git-commit: 188f60887a1904fbe4c69f644f6751ca7c9f1cc3
workflow-type: tm+mt
source-wordcount: '247'
ht-degree: 14%

---


# Detección de recursos duplicados {#detect-duplicate-assets}

<table>
    <tr>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nuevo</i></sup> <a href="/help/assets/dynamic-media/dm-prime-ultimate.md"><b>Dynamic Media Prime y Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nuevo</i></sup> <a href="/help/assets/assets-ultimate-overview.md"><b>AEM Assets Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nueva</i></sup> integración de <a href="/help/assets/integrate-aem-assets-edge-delivery-services.md"><b>AEM Assets con Edge Delivery Services</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nueva</i></sup> <a href="/help/assets/aem-assets-view-ui-extensibility.md"><b>extensibilidad de la interfaz de usuario</b></a>
        </td>
          <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nuevo</i></sup> <a href="/help/assets/dynamic-media/enable-dynamic-media-prime-and-ultimate.md"><b>Habilitar Dynamic Media Prime y Ultimate</b></a>
        </td>
    </tr>
    <tr>
        <td>
            <a href="/help/assets/search-best-practices.md"><b>Prácticas recomendadas de búsqueda</b></a>
        </td>
        <td>
            <a href="/help/assets/metadata-best-practices.md"><b>Prácticas recomendadas de metadatos</b></a>
        </td>
        <td>
            <a href="/help/assets/product-overview.md"><b>Centro de contenido</b></a>
        </td>
        <td>
            <a href="/help/assets/dynamic-media-open-apis-overview.md"><b>Dynamic Media con funciones de OpenAPI</b></a>
        </td>
        <td>
            <a href="https://developer.adobe.com/experience-cloud/experience-manager-apis/"><b>Documentación de desarrollador de AEM Assets</b></a>
        </td>
    </tr>
</table>

| Versión | Vínculo del artículo |
| -------- | ---------------------------- |
| AEM 6.5 | [Haga clic aquí](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/duplicate-detection.html?lang=es) |
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
>Si ha configurado el detector de duplicación utilizando el archivo de configuración `/apps/example/config.author/com.adobe.cq.assetcompute.impl.assetprocessor.AssetDuplicationDetector.cfg.json` (configuración OSGi), puede seguir utilizándolo; sin embargo, Adobe recomienda utilizar el nuevo método.


Una vez activado, Experience Manager envía notificaciones de recursos duplicados a la bandeja de entrada de Experience Manager. Es un resultado agregado para varios duplicados. Los usuarios pueden optar por eliminar los recursos en función de los resultados.

![Notificación de la bandeja de entrada para recursos duplicados](assets/duplicate-detect-inbox-notification.png)

>[!NOTE]
>
>Al cargar recursos en el repositorio, Experience Manager detecta la duplicación y le notifica sobre los 100 primeros recursos duplicados.
