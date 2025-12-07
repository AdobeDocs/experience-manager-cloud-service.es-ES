---
title: Mejore la detección de contenido con metadatos generados por IA en la vista de administración
description: Aprenda a mejorar la detección de contenido con metadatos generados por IA en la vista de administración
feature: Smart Tags,Tagging
role: Admin,User
source-git-commit: f83324be68bdab65e5c76ef336eb7e4a2e318dd1
workflow-type: tm+mt
source-wordcount: '594'
ht-degree: 9%

---


# Mejora de la detección de contenido con metadatos generados por IA {#ai-smart-tags}

| IU | Vínculo del artículo |
| -------- | ---------------------------- |
| Vista de recursos | [Haga clic aquí](/help/assets/ai-generated-metadata-assets-view.md) |
| Vista de administrador | Este artículo |

En lugar de depender de la entrada manual, IA asigna automáticamente etiquetas descriptivas a los recursos digitales. Estas etiquetas generadas por IA mejoran la calidad de los metadatos, lo que facilita la búsqueda, la categorización y la recomendación de recursos. Este enfoque no solo mejora la eficacia al eliminar el etiquetado manual, sino que también garantiza la coherencia y la escalabilidad en grandes volúmenes de contenido digital. Por ejemplo, si el recurso es una imagen, la IA puede identificar objetos, escenas, emociones o incluso logotipos de marca dentro de él y generar etiquetas relevantes como &quot;puesta de sol&quot;, &quot;playa&quot;, &quot;vacaciones&quot; o &quot;sonrisa&quot;. El contenido generado por IA puede mejorar la búsqueda de recursos mediante técnicas de búsqueda semánticas y léxicas. Ver más [Buscar en Assets](search-assets.md). <!--If the asset is a document, AI reads and interprets the text to assign meaningful keywords that summarize its content—such as "climate change," "policy," or "renewable energy.-->

![Etiquetas inteligentes mejoradas](assets/enhanced-smart-tags1.png)

## Cómo habilitar los metadatos generados por IA {#enable-ai-generated-metadata}

Para habilitar los metadatos generados por IA:

* La versión mínima de AEM requerida es `20626`.

## Configuración de títulos generados por IA {#configure-ai-generated-titles}

AEM permite configurar la visualización de los títulos de los recursos en la vista de tarjetas o en la vista de lista de la página de exploración de recursos. Puede elegir mostrar el título del recurso definido por usted, el título generado mediante IA o utilizar un título generado por IA solo si no hay ningún título existente para el recurso.

Para configurar títulos generados por IA:

1. Vaya a **[!UICONTROL Herramientas > Assets > Configuraciones de Assets > Configuración de mejora de etiquetas inteligentes]**.

1. Seleccione una de las siguientes opciones:

   * **Título de DC de visualización (predeterminado)**: especifique el título en el campo **[!UICONTROL Título]** disponible en las propiedades del recurso para mostrarlo en la vista de tarjeta o en la vista de lista. Si el título del recurso no está definido, AEM Assets muestra el nombre del archivo.

   * **Mostrar título generado por IA**: muestra el título generado por IA e ignora el título especificado en las propiedades del recurso. Si el título generado por IA no está disponible para un recurso, AEM Assets muestra el título de recurso predeterminado disponible en sus propiedades.

   * **Mostrar el título generado por IA solo si el título de DC no existe**: AEM Assets muestra el título generado por IA solo si el título del recurso no está definido para un recurso.

     ![Configurar títulos generados por IA](assets/configure-title-ai-generated.png)

## Uso de metadatos generados por IA {#using-ai-generated-smart-tags}

<!--[!NOTE]
>
>The enhanced smart tags capability is available only for the newly uploaded assets.
-->

Para utilizar la función de etiquetas inteligentes mejorada, ejecute los siguientes pasos:

1. En la interfaz [!DNL Experience Manager], vaya a la carpeta deseada y haga clic en **[!UICONTROL Agregar Assets]**. <!--Alternatively, to update enhanced smart tags in an existing content, click **[!UICONTROL reprocess]**.--> Los formatos de archivo de imagen compatibles son `png`, `jpg`, `jpeg`, `psd`, `tiff`, `gif`, `webp`, `crw`, `cr2`, `3fr`, `nef`, `arw` y `bmp`.

1. Espere hasta que se procese el recurso recién cargado. Una vez finalizado, vaya a las propiedades del recurso.

1. Vaya a la pestaña **[!UICONTROL Generado por IA]**. Si la versión de [!DNL Experience Manager] no es compatible o no se ha actualizado, esta pestaña no estará visible. Los campos siguientes están presentes:

   * **[!UICONTROL Título generado]:** El título proporciona un título claro y conciso que captura la idea central de un recurso cargado, lo que facilita su comprensión de un vistazo. Al agregar un recurso, si proporciona un título (en `dc:title`), este se mostrará en la vista del explorador de recursos. Si se deja en blanco, se asignará automáticamente un título generado por IA.
   * **[!UICONTROL Descripción generada]:** La descripción ofrece un resumen breve pero informativo de lo que trata el recurso, lo que ayuda a los usuarios y al módulo de búsqueda a captar rápidamente su relevancia.
   * **[!UICONTROL Palabras clave generadas]:** Las palabras clave son términos de destino que representan los temas principales de un recurso y que ayudan a etiquetar y filtrar el contenido.

1. [Opcional]: puede agregar etiquetas adicionales o crear las suyas propias si cree que faltan etiquetas relevantes. Para ello, escriba sus etiquetas en el campo **[!UICONTROL Palabras clave generadas]** y haga clic en **[!UICONTROL Guardar]**.

## Deshabilitar metadatos generados por IA {#disable-ai-generated-metadata}

Para deshabilitar los metadatos generados por IA:

1. Vaya a **[!UICONTROL Herramientas > Assets > Configuraciones de Assets > Configuración de mejora de etiquetas inteligentes]**.

1. Seleccione **[!UICONTROL Deshabilitar mejoras en etiquetas inteligentes]**.

1. Haga clic en **[!UICONTROL Guardar]** .

Los metadatos generados por IA están desactivados para los nuevos recursos o carpetas que se cargan en los AEM Assets. Los recursos o carpetas existentes que ya tienen campos de metadatos generados por IA generados siguen mostrando estos campos.