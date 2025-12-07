---
title: Mejore la detección de contenido con metadatos generados por IA
description: Aprenda a mejorar la detección de contenido con metadatos generados por IA
source-git-commit: f83324be68bdab65e5c76ef336eb7e4a2e318dd1
workflow-type: tm+mt
source-wordcount: '357'
ht-degree: 4%

---


# Mejore la detección de contenido con metadatos generados por IA {#ai-smart-tags}

En lugar de depender de la entrada manual, IA asigna automáticamente etiquetas descriptivas a los recursos digitales. Estas etiquetas generadas por IA mejoran la calidad de los metadatos, lo que facilita la búsqueda, la categorización y la recomendación de recursos. Este enfoque no solo mejora la eficacia al eliminar el etiquetado manual, sino que también garantiza la coherencia y la escalabilidad en grandes volúmenes de contenido digital. Por ejemplo, si el recurso es una imagen, la IA puede identificar objetos, escenas, emociones o incluso logotipos de marca dentro de él y generar etiquetas relevantes como &quot;puesta de sol&quot;, &quot;playa&quot;, &quot;vacaciones&quot; o &quot;sonrisa&quot;. El contenido generado por IA puede mejorar la búsqueda de recursos mediante técnicas de búsqueda semánticas y léxicas. Ver más [Buscar en Assets](search-assets-view.md). <!--If the asset is a document, AI reads and interprets the text to assign meaningful keywords that summarize its content—such as "climate change," "policy," or "renewable energy.-->

![Metadatos generados por IA](/help/assets/assets/enhanced-smart-tags.png)

## Cómo habilitar los metadatos generados por IA {#enable-ai-generated-metadata}

Para habilitar los metadatos generados por IA:

* La versión mínima de AEM requerida es `20626`.


## Uso de metadatos generados por IA {#using-ai-generated-smart-tags}

<!--[!NOTE]
>
>The enhanced smart tags capability is available only for the newly uploaded assets.
-->

Para utilizar la función de etiquetas inteligentes mejorada, ejecute los siguientes pasos:

1. En la interfaz [!DNL Experience Manager], vaya a la carpeta deseada y haga clic en **[!UICONTROL Agregar Assets]**. <!--Alternatively, to update enhanced smart tags in an existing content, click **[!UICONTROL reprocess]**.--> Los formatos de archivo de imagen compatibles son `png`, `jpg`, `jpeg`, `psd`, `tiff`, `gif`, `webp`, `crw`, `cr2`, `3fr`, `nef`, `arw` y `bmp`.

1. Espere hasta que se procese el recurso recién cargado. Una vez finalizado, vaya a Detalles del recurso.

1. Vaya a la pestaña **[!UICONTROL Generado por IA]**. Si la versión de [!DNL Experience Manager] no es compatible o no se ha actualizado, esta pestaña no estará visible.  Los campos siguientes están presentes:

   * **[!UICONTROL Título generado]:** El título proporciona un título claro y conciso que captura la idea central de un recurso cargado, lo que facilita su comprensión de un vistazo. Al agregar un recurso, si proporciona un título (en `dc:title`), este se mostrará en la vista del explorador de recursos. Si se deja en blanco, se asignará automáticamente un título generado por IA.
   * **[!UICONTROL Descripción generada]:** La descripción ofrece un resumen breve pero informativo de lo que trata el recurso, lo que ayuda a los usuarios y al módulo de búsqueda a captar rápidamente su relevancia.
   * **[!UICONTROL Palabras clave generadas]:** Las palabras clave son términos de destino que representan los temas principales de un recurso y que ayudan a etiquetar y filtrar el contenido.

1. [Opcional]: puede agregar etiquetas adicionales o crear las suyas propias si cree que faltan etiquetas relevantes. Para ello, escriba sus etiquetas en el campo **[!UICONTROL Palabras clave generadas]** y haga clic en **[!UICONTROL Guardar]**.

Para obtener información sobre cómo deshabilitar los metadatos generados por IA, consulte [Deshabilitar metadatos generados por IA](/help/assets/smart-tags.md#disable-ai-generated-metadata).
