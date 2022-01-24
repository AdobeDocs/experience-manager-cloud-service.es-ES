---
title: Problemas conocidos
description: Problemas conocidos con Adobe Experience Manager as a Cloud Service
exl-id: 897b944a-d320-4d21-91f4-2cd3da6179b1
source-git-commit: 8ec0ce3425e7cade0a6774a4452d4f47ab971375
workflow-type: ht
source-wordcount: '111'
ht-degree: 100%

---

# Problemas conocidos {#known-issues}

Este artículo enumera los problemas conocidos de la oferta de [!DNL Adobe Experience Manager] as a [!DNL Cloud Service]. La lista se revisa y actualiza con cada versión de [!DNL Experience Manager].

[Comuníquese con soporte técnico](https://experienceleague.adobe.com/?lang=es&amp;support-solution=Experience+Manager#support) para obtener más información sobre los problemas conocidos.

<!-- 
## Platform {#platform}

## Sites {#sites}
-->

## [!DNL Assets] {#assets}

<!-- Jira label: assets-cloud-known-issues -->

Algunos problemas conocidos en [!DNL Assets] son los siguientes:

* **Descarga**: si descarga una carpeta vacía, [!DNL Experience Manager] transmite un mensaje de éxito acerca de la creación de un archivo ZIP, pero no se crea el archivo.

* **Esquema de metadatos**: la utilidad de clasificación de recursos solía causar un error de compilación de JSP. Se eliminó del esquema de metadatos. <!-- CQ-4282865, CQ-4284633 -->

Consulte también [cambios importantes en [!DNL Experience Manager Assets]](/help/assets/assets-cloud-changes.md).

<!-- This content was added at GA. Not sure if we should continue to have this commitment about upcoming features/enh. in the docs. Commenting it for now.

### Upcoming Assets capabilities {#upcoming-assets-capabilities}

A few capabilities of Adobe Experience Manager Assets that depend on foundation capabilities, which are not yet available in the Experience Manager as a Cloud Service deployment architecture, are expected to be enabled at a later stage:

* Capabilities not enabled at this stage due to dependency on Commerce Integration Framework APIs:
  * Photoshoot workflow models.
  * Product information tab in the asset properties user interface is not populated.

* Capabilities not enabled at this stage due to dependency on InDesign Server integration:
  * Asset Templates and Asset Catalogs.
  * Multi-page preview of Adobe InDesign files.
-->

>[!MORELIKETHIS]
>
>* [Principales cambios en  [!DNL Experience Manager]](aem-cloud-changes.md)
>* [Funciones en desuso y eliminadas](deprecated-removed-features.md)
>* [Notas de la versión](home.md)

