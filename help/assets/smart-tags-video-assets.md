---
title: Etiquetado inteligente de recursos de vídeo
description: Experience Manager agrega automáticamente etiquetas inteligentes contextuales y descriptivas a los vídeos mediante [!DNL Adobe Sensei].
translation-type: tm+mt
source-git-commit: ceaa9546be160e01b124154cc827e6b967388476
workflow-type: tm+mt
source-wordcount: '1183'
ht-degree: 0%

---


# Etiquetado inteligente de los recursos de vídeo {#video-smart-tags}

La creciente necesidad de nuevo contenido exige reducir los esfuerzos manuales para ofrecer experiencias digitales atractivas en poco tiempo. [!DNL Adobe Experience Manager] como  [!DNL Cloud Service] admite el etiquetado automático de recursos de vídeo mediante inteligencia artificial. Etiquetar los vídeos manualmente puede llevar mucho tiempo. Sin embargo, la función de etiquetado inteligente de [!DNL Adobe Sensei] vídeo con tecnología compatible utiliza modelos de inteligencia artificial para analizar el contenido de vídeo y agregar etiquetas a los recursos de vídeo. De este modo, se reduce el tiempo de los usuarios de DAM para ofrecer experiencias ricas a sus clientes. El servicio de aprendizaje automático de Adobe genera dos conjuntos de etiquetas para un vídeo. Mientras que un conjunto corresponde a objetos, escenas y atributos de ese vídeo; el otro conjunto se refiere a acciones como beber, correr y trotar.

El etiquetado de vídeo está habilitado de forma predeterminada en [!DNL Adobe Experience Manager] como [!DNL Cloud Service]. Sin embargo, puede [desactivar el etiquetado inteligente de vídeo](#opt-out-video-smart-tagging) en una carpeta. Los vídeos se etiquetan automáticamente al cargar vídeos nuevos o al volver a procesar los existentes. [!DNL Experience Manager] también crea las miniaturas y extrae los metadatos de los archivos de vídeo. Las etiquetas inteligentes se muestran en orden descendente de su [puntuación de confianza](#confidence-score-video-tag) en el recurso [!UICONTROL Propiedades].

## Etiquetado inteligente de vídeos al cargar {#smart-tag-assets-on-ingestion}

Al [cargar recursos de vídeo](add-assets.md#upload-assets) a [!DNL Adobe Experience Manager] como [!DNL Cloud Service], se procesan los vídeos. Una vez completado el procesamiento, consulte la ficha [!UICONTROL Básico] de la página Propiedades] del recurso. [!UICONTROL  Las etiquetas inteligentes se agregan automáticamente al vídeo en [!UICONTROL Etiquetas inteligentes]. Los microservicios de recursos aprovechan [!DNL Adobe Sensei] para crear estas etiquetas inteligentes.

![Las etiquetas inteligentes se agregan a los vídeos y se ven en la ficha Básico de las propiedades del recurso](assets/smart-tags-added-to-videos.png)

Las etiquetas inteligentes aplicadas se ordenan en orden descendente de [puntuación de confianza](#confidence-score-video-tag), combinadas para etiquetas de objeto y acción, dentro de [!UICONTROL Etiquetas inteligentes].

>[!IMPORTANT]
>
>Se recomienda revisar estas etiquetas generadas automáticamente para asegurarse de que se ajustan a su marca y a sus valores.

## Etiquetado inteligente de vídeos existentes en DAM {#smart-tag-existing-videos}

Los recursos de vídeo existentes en DAM no se etiquetan de forma inteligente automáticamente. Debe [!UICONTROL volver a procesar los recursos] manualmente para generar etiquetas inteligentes para ellos.

Para etiquetar recursos de vídeo o carpetas (incluidas subcarpetas) de recursos que ya existen en el repositorio de recursos, siga estos pasos:

1. Seleccione el logotipo [!DNL Adobe Experience Manager] y, a continuación, seleccione recursos en la página [!UICONTROL Navegación].

1. Seleccione [!UICONTROL Archivos] para mostrar la interfaz de Recursos.

1. Vaya a la carpeta a la que desea aplicar las etiquetas inteligentes.

1. Seleccione la carpeta completa o los recursos de vídeo específicos.

1. Seleccione el icono ![Volver a procesar recursos](assets/do-not-localize/reprocess-assets-icon.png) [!UICONTROL Volver a procesar recursos] y seleccione la opción [!UICONTROL Proceso completo].

<!-- TBD: Limit size -->

![Volver a procesar los recursos para agregar etiquetas a los vídeos del repositorio DAM existente](assets/reprocess.gif)

Una vez completado el proceso, navegue a la página [!UICONTROL Propiedades] de cualquier recurso de vídeo de la carpeta. Las etiquetas agregadas automáticamente se ven en la sección [!UICONTROL Etiquetas inteligentes] de la ficha [!UICONTROL Básico]. Estas etiquetas inteligentes aplicadas se ordenan en orden descendente por [puntuación de confianza](#confidence-score-video-tag).

## Buscar vídeos etiquetados {#search-smart-tagged-videos}

Para buscar recursos de vídeo basados en etiquetas inteligentes generadas automáticamente, utilice [Omnisearch](search-assets.md#search-assets-in-aem):

1. Seleccione el icono de búsqueda ![icono de búsqueda](assets/do-not-localize/search_icon.png) para mostrar el campo Omnisearch.

1. Especifique una etiqueta, en el campo Omniture Search, que no haya agregado explícitamente a un video.

1. Búsqueda basada en la etiqueta .

Los resultados de la búsqueda muestran los recursos de vídeo en función de la etiqueta especificada.

Los resultados de la búsqueda son una combinación de recursos de vídeo con palabras clave buscadas en los metadatos y los recursos de vídeo con etiquetas inteligentes con las palabras clave buscadas. Sin embargo, los resultados de búsqueda que coinciden con todos los términos de búsqueda en los campos de metadatos se muestran primero, seguidos de los resultados de búsqueda que coinciden con cualquiera de los términos de búsqueda en las etiquetas inteligentes. Para obtener más información, consulte [Comprender [!DNL Experience Manager] resultados de búsqueda con etiquetas inteligentes](smart-tags.md#understandsearch).

## Moderar etiquetas inteligentes de vídeo {#moderate-video-smart-tags}

[!DNL Adobe Experience Manager] le permite depurar las etiquetas inteligentes para:

* elimine las etiquetas inexactas asignadas a los vídeos de marca.

* refinar las búsquedas de vídeos basadas en etiquetas asegurándose de que el vídeo aparece en los resultados de búsqueda para las etiquetas más relevantes. Por lo tanto, elimina las posibilidades de que los vídeos no relacionados se muestren en los resultados de búsqueda.

* asigne una clasificación superior a una etiqueta para aumentar su relevancia con respecto a un vídeo. La promoción de una etiqueta para un vídeo aumenta las posibilidades de que el vídeo aparezca en los resultados de búsqueda cuando se realiza una búsqueda en función de esa etiqueta.

Para obtener más información sobre cómo moderar las etiquetas inteligentes de los recursos, consulte [Administrar etiquetas inteligentes](smart-tags.md#manage-smart-tags-and-searches).

![Moderar etiquetas inteligentes de vídeo](assets/manage-video-smart-tags.png)

>[!NOTE]
>
>Las etiquetas moderadas mediante los pasos de [Administrar etiquetas inteligentes](smart-tags.md#manage-smart-tags-and-searches) no se recuerdan al reprocesar el recurso. El conjunto original de etiquetas se muestra de nuevo.

## Exclusión el etiquetado inteligente de vídeo {#opt-out-video-smart-tagging}

Como el etiquetado automático de vídeos se ejecuta en paralelo a otras tareas de procesamiento de recursos, como la creación de miniaturas y la extracción de metadatos, puede llevar mucho tiempo. Para acelerar el procesamiento de recursos, puede exclusión el etiquetado inteligente de vídeo al cargarlo en el nivel de carpeta.

Para exclusión la generación automatizada de etiquetas inteligentes de vídeo para los recursos cargados en una carpeta específica:

1. Abra la ficha [!UICONTROL Procesamiento de recursos] en la carpeta [!UICONTROL Propiedades].

1. En el menú [!UICONTROL Etiquetas inteligentes para vídeos], la opción [!UICONTROL Heredada] está seleccionada de forma predeterminada y la etiqueta inteligente de vídeo está activada.

   Cuando se selecciona la opción [!UICONTROL Heredada], la ruta de la carpeta heredada también se muestra visible junto con la información de si está configurada en [!UICONTROL Habilitar] o [!UICONTROL Deshabilitar].

   ![Deshabilitar etiquetado inteligente de vídeo](assets/disable-video-tagging.png)

1. Seleccione [!UICONTROL Deshabilitar] para exclusión el etiquetado inteligente de los vídeos cargados en la carpeta.

>[!IMPORTANT]
>
>Si ha exclusión de etiquetar vídeos en una carpeta en el momento de la carga y desea etiquetar los vídeos de forma inteligente después de la carga, **[!UICONTROL Active Etiquetas inteligentes para vídeos]** desde la ficha [!UICONTROL Procesamiento de recursos] de la carpeta [!UICONTROL Propiedades] y utilice la opción [[!UICONTROL Volver a procesar recurso] para agregar etiquetas inteligentes a la vídeo.](#smart-tag-existing-videos)

## Puntuación de confianza {#confidence-score-video-tag}

[!DNL Adobe Experience Manager] aplica un umbral de confianza mínimo a las etiquetas inteligentes de objetos y acciones para evitar tener demasiadas etiquetas para cada recurso de vídeo, lo que ralentiza la indexación. Los resultados de la búsqueda de recursos se clasifican según las puntuaciones de confianza, lo que generalmente mejora los resultados de la búsqueda más allá de lo que sugiere una inspección de las etiquetas asignadas a cualquier recurso de vídeo. Las etiquetas imprecisas suelen tener puntuaciones de confianza bajas, por lo que rara vez aparecen en la parte superior de la lista Etiquetas inteligentes para los recursos.

El umbral predeterminado para las etiquetas action y object en [!DNL Adobe Experience Manager] es 0,7 (debe ser un valor entre 0 y 1). Si algunos recursos de vídeo no están etiquetados con una etiqueta específica, indica que el algoritmo tiene menos del 70 % de confianza en las etiquetas predichas. Es posible que el umbral predeterminado no siempre sea óptimo para todos los usuarios. Por lo tanto, puede cambiar el valor de puntuación de confianza en la configuración OSGI.

Para agregar la configuración OSGI de puntuación de confianza al proyecto implementado en [!DNL Adobe Experience Manager] como [!DNL Cloud Service] a [!DNL Cloud Manager]:

* En el proyecto [!DNL Adobe Experience Manager] (`ui.config` desde Archetype 24, o anteriormente `ui.apps`) la configuración OSGi de `config.author`, incluya un archivo de configuración denominado `com.adobe.cq.assetcompute.impl.senseisdk.SenseiSdkImpl.cfg.json` con el siguiente contenido:

```json
{
  "minVideoActionConfidenceScore":0.5,
  "minVideoObjectConfidenceScore":0.5,
}
```

>[!NOTE]
>
>A las etiquetas manuales se les asigna una confianza del 100 % (máxima confianza). Por lo tanto, si hay recursos de vídeo con etiquetas manuales que coinciden con la consulta de búsqueda, se muestran antes que las etiquetas inteligentes que coinciden con la consulta de búsqueda.

## Restricciones     {#video-smart-tagging-limitations}

* No puede entrenar el servicio que aplica etiquetas inteligentes a vídeos con vídeos específicos. Funciona con la configuración predeterminada [!DNL Adobe Sensei].

* No se muestra el progreso del etiquetado.

* Solo se etiquetan automáticamente los vídeos con un tamaño de archivo inferior a 300 MB. El servicio [!DNL Adobe Sensei] omite los archivos de vídeo de mayor tamaño.

* Solo se etiquetan los vídeos en los formatos de archivo y los códecs admitidos mencionados en [Etiquetas inteligentes](/help/assets/smart-tags.md#smart-tags-supported-file-formats).

>[!MORELIKETHIS]
>
>* [Administración de etiquetas inteligentes y búsquedas de recursos](smart-tags.md#manage-smart-tags-and-searches)
>* [Servicio de etiquetas inteligentes de formación y etiquetado de imágenes](smart-tags.md)

