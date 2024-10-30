---
title: Descarga de recursos desde Content Hub
description: Obtenga información sobre cómo descargar recursos desde el portal de Content Hub
role: User
exl-id: 96d4ffba-4e3e-4496-9da2-6eb36be8331f
source-git-commit: 76337282b7d3008864763541a957c44327e1a5be
workflow-type: tm+mt
source-wordcount: '526'
ht-degree: 3%

---

# Descarga de recursos desde Content Hub {#download-assets}

| [Prácticas recomendadas de búsqueda](/help/assets/search-best-practices.md) | [Prácticas recomendadas de metadatos](/help/assets/metadata-best-practices.md) | [Centro de contenido](/help/assets/product-overview.md) | [Dynamic Media con funciones de OpenAPI](/help/assets/dynamic-media-open-apis-overview.md) | [Documentación de desarrollador de AEM Assets](https://developer.adobe.com/experience-cloud/experience-manager-apis/) |
| ------------- | --------------------------- |---------|----|-----|

<!-- ![Download assets](assets/download-asset.jpg) -->
![Descarga de recursos](assets/download-asset-genstudio.jpeg)

Content Hub le permite descargar y compartir sus recursos. Estos recursos pueden incluir imágenes, vídeos o cualquier otro contenido digital. Content Hub mejora la accesibilidad y la adaptabilidad para una distribución eficaz de los recursos.

Puede descargar un único recurso o varios mediante Content Hub. Se descargan las versiones originales del recurso.

## Descargar recurso con licencia única {#single-download-asset}

Seleccione un recurso y haga clic en ![descargar](/help/assets/assets/download-icon.svg) en el carril superior. El cuadro de diálogo Descargar recurso muestra la licencia del recurso. Acepte los términos y condiciones de las licencias y haga clic en **Descargar**.
También puede hacer clic en ![descargar](/help/assets/assets/download-icon.svg) en la tarjeta de recursos para descargar el recurso.

### Descargar solo recurso con licencia del cuadro de diálogo Recurso {#single-download-from-asset-dialog-box}

1. Haga clic en la miniatura del recurso. Se muestra el cuadro de diálogo Recurso.
1. Haga clic en ![descargar](/help/assets/assets/download-icon.svg) en la barra de herramientas situada más a la derecha. El panel de descarga muestra las representaciones de recursos y la casilla de verificación de aceptación de los términos y condiciones de la licencia.
   ![cuadro de diálogo de descarga única](/help/assets/assets/asset-dialog-box-for-single-download.png)
   * Haga clic en el vínculo términos y condiciones para ver los términos de licencia en el panel izquierdo.

     >[!NOTE]
     >
     >La casilla de verificación Términos y condiciones solo se muestra para los recursos con licencia. Además, el cuadro de diálogo de recursos muestra una vista previa de los términos y condiciones de licencia únicamente para los recursos con licencias aprobadas. [Apruebe la licencia del recurso](/help/assets/approve-assets-content-hub.md) antes de la descarga para habilitar la vista previa de los términos de licencia en el cuadro de diálogo del recurso.

   * Haga clic en **Cuadro de representación original** para volver a la representación del recurso original en el panel izquierdo.
1. Acepte los términos y condiciones de la licencia (para el recurso con licencia) y haga clic en **Descargar** para descargar el recurso.

## Descargar Assets con varias licencias{#multi-download}

1. Seleccione los recursos y haga clic en ![descargar](/help/assets/assets/download-icon.svg) en el carril superior. El cuadro de diálogo que se muestra depende de si la lista de descarga incluye recursos caducados o solo recursos no caducados. <br/>
   **Descargar el cuadro de diálogo de recursos caducados:** Este cuadro de diálogo muestra la vista previa de los recursos caducados junto con su fecha de caducidad en el panel izquierdo. El recuento de recursos caducados del total seleccionado se muestra en el panel derecho. Haga clic en **Continuar con todos los recursos** para descargar los recursos caducados con otros recursos (si los hay). Aparece el cuadro de diálogo Descargar recursos. Consulte el [cuadro de diálogo Descargar recursos](#Download-asset-dialog-box) para continuar.

   >[!NOTE]
   >
   >[Habilite la opción de descarga para los recursos caducados](/help/assets/configure-content-hub-ui-options.md#expired-assets-content-hub) para descargarlos. Solo los recursos caducados que hayan habilitado la descarga están disponibles para su descarga.

   <a id="Download-asset-dialog-box"></a> **Cuadro de diálogo Descargar recursos:** Este cuadro de diálogo muestra la lista de licencias asociadas con los recursos seleccionados en el panel izquierdo. Seleccione una licencia para obtener una vista previa de sus términos y condiciones (en formato pdf) en el panel central, y la vista previa de los recursos asociados y su recuento en el panel derecho. Las licencias revisadas aparecen resaltadas en azul claro.

   >[!NOTE]
   >
   > El **cuadro de diálogo Descargar recurso** muestra una vista previa de los términos y condiciones de licencia únicamente para las licencias aprobadas. [Apruebe las licencias de los recursos](/help/assets/approve-assets-content-hub.md) antes de descargarlas para obtener una vista previa de sus términos de licencia en el **cuadro de diálogo Descargar recurso**.

1. Haga clic en ![remove-icon](/help/assets/assets/remove-icon.svg) para quitar una licencia del cuadro de diálogo de descarga.

1. Acepte los términos y condiciones y, a continuación, haga clic en **Descargar** para descargar los recursos asociados con las licencias disponibles en el panel izquierdo.
   ![descargar-múltiples-licencias](/help/assets/assets/download-multiple-license.png)

### Descargar Assets sin licencia {#download-non-licensed-assets}

Para descargar recursos sin licencia, seleccione los recursos y haga clic en ![descargar](/help/assets/assets/download-icon.svg) en el carril superior.







