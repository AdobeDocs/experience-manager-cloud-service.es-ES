---
title: Etiquetado inteligente de activos de vídeo
description: El Experience Manager agrega automáticamente etiquetas inteligentes contextuales y descriptivas a los vídeos mediante [!DNL Adobe Sensei].
feature: Smart Tags,Tagging
role: Admin,User
exl-id: b59043c5-5df3-49a7-b4fc-da34c03649d7
source-git-commit: 8bdd89f0be5fe7c9d4f6ba891d7d108286f823bb
workflow-type: tm+mt
source-wordcount: '1213'
ht-degree: 2%

---

# Etiquetado inteligente de activos de vídeo {#video-smart-tags}

La creciente necesidad de nuevo contenido exige reducir los esfuerzos manuales para ofrecer experiencias digitales atractivas en poco tiempo. [!DNL Adobe Experience Manager] como [!DNL Cloud Service] admite el etiquetado automático de recursos de vídeo mediante inteligencia artificial. Etiquetar los vídeos manualmente puede llevar mucho tiempo. Sin embargo, [!DNL Adobe Sensei] la función de etiquetado inteligente de vídeo con tecnología utiliza modelos de inteligencia artificial para analizar el contenido de vídeo y añadir etiquetas a los recursos de vídeo. De este modo, se reduce el tiempo para que los usuarios de DAM entreguen experiencias enriquecidas a sus clientes. El servicio de aprendizaje automático de Adobe genera dos conjuntos de etiquetas para un vídeo. Mientras que un conjunto corresponde a objetos, escenas y atributos de ese vídeo; el otro conjunto está relacionado con acciones como beber, correr y correr.

El etiquetado de vídeo está habilitado de forma predeterminada en [!DNL Adobe Experience Manager] como [!DNL Cloud Service]. Sin embargo, puede [exclusión del etiquetado inteligente de vídeo](#opt-out-video-smart-tagging) en una carpeta. Los vídeos se etiquetan automáticamente al cargar nuevos vídeos o al volver a procesar los existentes. [!DNL Experience Manager] también crea las miniaturas y extrae metadatos de los archivos de vídeo. Las etiquetas inteligentes se muestran en orden descendente [puntuación de confianza](#confidence-score-video-tag) en el recurso [!UICONTROL Propiedades].

## Etiquetado inteligente de vídeos al cargar {#smart-tag-assets-on-ingestion}

Cuando [cargar recursos de vídeo](add-assets.md#upload-assets) a [!DNL Adobe Experience Manager] como [!DNL Cloud Service], se procesan los vídeos. Una vez completado el procesamiento, consulte la [!UICONTROL Básico] pestaña de recurso [!UICONTROL Propiedades] página. Las etiquetas inteligentes se añaden automáticamente al vídeo en [!UICONTROL Etiquetas inteligentes]. Los microservicios de recursos aprovechan [!DNL Adobe Sensei] para crear estas etiquetas inteligentes.

![Las etiquetas inteligentes se añaden a los vídeos y se ven en la pestaña Básico de las propiedades de recursos](assets/smart-tags-added-to-videos.png)

Las etiquetas inteligentes aplicadas se ordenan en orden descendente de [puntuación de confianza](#confidence-score-video-tag), combinado para etiquetas de objeto y acción, dentro de [!UICONTROL Etiquetas inteligentes].

>[!IMPORTANT]
>
>Se recomienda revisar estas etiquetas generadas automáticamente para asegurarse de que se ajustan a la marca y a sus valores.

## Etiquetado inteligente de vídeos existentes en DAM {#smart-tag-existing-videos}

Los recursos de vídeo existentes en DAM no se etiquetan automáticamente como inteligentes. Debe [!UICONTROL Volver a procesar recursos] para generar etiquetas inteligentes de forma manual para ellas.

Para etiquetar de forma inteligente los recursos de vídeo o las carpetas (incluidas las subcarpetas) de recursos que ya existen en el repositorio de recursos, siga estos pasos:

1. Seleccione el [!DNL Adobe Experience Manager] y, a continuación, seleccione los recursos en el [!UICONTROL Navegación] página.

1. Select [!UICONTROL Archivos] para mostrar la interfaz de Assets.

1. Vaya a la carpeta a la que desea aplicar etiquetas inteligentes.

1. Seleccione toda la carpeta o recursos de vídeo específicos.

1. Select ![Icono Volver a procesar los recursos](assets/do-not-localize/reprocess-assets-icon.png) [!UICONTROL Volver a procesar recursos] y seleccione [!UICONTROL Proceso completo] .

<!-- TBD: Limit size -->

![Volver a procesar recursos para agregar etiquetas a los vídeos del repositorio DAM existente](assets/reprocess.gif)

Una vez completado el proceso, vaya a la [!UICONTROL Propiedades] de cualquier recurso de vídeo de la carpeta. Las etiquetas añadidas automáticamente se ven en [!UICONTROL Etiquetas inteligentes] en [!UICONTROL Básico] pestaña . Estas etiquetas inteligentes aplicadas se ordenan en orden descendente de [puntuación de confianza](#confidence-score-video-tag).

## Buscar vídeos etiquetados {#search-smart-tagged-videos}

Para buscar recursos de vídeo basados en etiquetas inteligentes generadas automáticamente, utilice [Omnisearch](search-assets.md#search-assets-in-aem):

1. Seleccione el icono de búsqueda ![icono de búsqueda](assets/do-not-localize/search_icon.png) para mostrar el campo Omnisearch .

1. Especifique una etiqueta, en el campo Omnisearch , que no haya agregado explícitamente a un vídeo.

1. Busque en función de la etiqueta .

Los resultados de la búsqueda muestran los recursos de vídeo en función de la etiqueta especificada.

Los resultados de búsqueda son una combinación de recursos de vídeo con palabras clave buscadas en los metadatos y los recursos de vídeo que están etiquetados de forma inteligente con las palabras clave buscadas. Sin embargo, los resultados de búsqueda que coinciden con todos los términos de búsqueda en los campos de metadatos se muestran primero, seguidos de los resultados de búsqueda que coinciden con cualquiera de los términos de búsqueda en las etiquetas inteligentes. Para obtener más información, consulte [Comprender [!DNL Experience Manager] resultados de búsqueda con etiquetas inteligentes](smart-tags.md#understand-search).

## Moderar etiquetas inteligentes de vídeo {#moderate-video-smart-tags}

[!DNL Adobe Experience Manager] permite depurar las etiquetas inteligentes para:

* elimine las etiquetas inexactas asignadas a los vídeos de marca.

* refinar las búsquedas de vídeos basadas en etiquetas, asegurándose de que el vídeo aparezca en los resultados de búsqueda para las etiquetas más relevantes. Por lo tanto, elimina las posibilidades de que los vídeos no relacionados se muestren en los resultados de búsqueda.

* asignar una clasificación superior a una etiqueta para aumentar su relevancia con respecto a un vídeo. La promoción de una etiqueta para un vídeo aumenta las posibilidades de que el vídeo aparezca en los resultados de búsqueda cuando se realiza una búsqueda basada en esa etiqueta.

Para obtener más información sobre cómo moderar las etiquetas inteligentes de los recursos, consulte [Administrar etiquetas inteligentes](smart-tags.md#manage-smart-tags-and-searches).

![Moderar etiquetas inteligentes de vídeo](assets/manage-video-smart-tags.png)

>[!NOTE]
>
>Cualquier etiqueta moderada con los pasos indicados en [Administrar etiquetas inteligentes](smart-tags.md#manage-smart-tags-and-searches) no se recuerdan al reprocesar el recurso. El conjunto original de etiquetas se muestra de nuevo.

## Exclusión del etiquetado inteligente de vídeo {#opt-out-video-smart-tagging}

Como el etiquetado automático de vídeos se ejecuta en paralelo a otras tareas de procesamiento de recursos, como la creación de miniaturas y la extracción de metadatos, puede requerir mucho tiempo. Para acelerar el procesamiento de recursos, puede desactivar el etiquetado inteligente de vídeo en la carga a nivel de carpeta.

Para desactivar la generación automatizada de etiquetas inteligentes de vídeo para los recursos cargados en una carpeta específica:

1. Apertura [!UICONTROL Procesamiento de recursos] ficha en la carpeta [!UICONTROL Propiedades].

1. En [!UICONTROL Etiquetas inteligentes para vídeos] , [!UICONTROL Heredado] está seleccionada de forma predeterminada y la etiqueta inteligente de vídeo está activada.

   Cuando la variable [!UICONTROL Heredado] está seleccionada, la ruta de la carpeta heredada también está visible junto con la información de si está configurada como [!UICONTROL Habilitar] o [!UICONTROL Deshabilitar].

   ![Desactivación del etiquetado inteligente de vídeo](assets/disable-video-tagging.png)

1. Select [!UICONTROL Deshabilitar] para desactivar el etiquetado inteligente de los vídeos cargados en la carpeta.

>[!IMPORTANT]
>
>Si ha optado por no etiquetar vídeos en una carpeta en el momento de la carga y desea etiquetar de forma inteligente los vídeos después de la carga, entonces **[!UICONTROL Habilitar etiquetas inteligentes para vídeos]** from [!UICONTROL Procesamiento de recursos] de la carpeta [!UICONTROL Propiedades] y use [[!UICONTROL Volver a procesar el recurso] option](#smart-tag-existing-videos) para agregar etiquetas inteligentes al vídeo.

## Puntuación de confianza {#confidence-score-video-tag}

[!DNL Adobe Experience Manager] aplica un umbral de confianza mínimo para las etiquetas inteligentes de objeto y acción para evitar tener demasiadas etiquetas para cada recurso de vídeo, lo que ralentiza la indexación. Los resultados de la búsqueda de recursos se clasifican según las puntuaciones de confianza, lo que generalmente mejora los resultados de la búsqueda más allá de lo que sugiere una inspección de las etiquetas asignadas a cualquier recurso de vídeo. Las etiquetas inexactas suelen tener puntuaciones de confianza bajas, por lo que rara vez aparecen en la parte superior de la lista de etiquetas inteligentes para los recursos.

El umbral predeterminado para las etiquetas de objeto y acción de [!DNL Adobe Experience Manager] es 0,7 (debe ser un valor entre 0 y 1). Si algunos recursos de vídeo no están etiquetados con una etiqueta específica, entonces indica que el algoritmo tiene menos del 70 % de confianza en las etiquetas predichas. Es posible que el umbral predeterminado no sea siempre óptimo para todos los usuarios. Por lo tanto, puede cambiar el valor de puntuación de confianza en la configuración OSGI.

Para añadir la configuración OSGI de puntuación de confianza al proyecto implementado en [!DNL Adobe Experience Manager] como [!DNL Cloud Service] hasta [!DNL Cloud Manager]:

* En el [!DNL Adobe Experience Manager] proyecto (`ui.config` desde Tipo de archivo 24 o anterior `ui.apps`). `config.author` Configuración de OSGi, incluya un archivo de configuración denominado `com.adobe.cq.assetcompute.impl.senseisdk.SenseiSdkImpl.cfg.json` con el siguiente contenido:

```json
{
  "minVideoActionConfidenceScore":0.5,
  "minVideoObjectConfidenceScore":0.5,
}
```

>[!NOTE]
>
>A las etiquetas manuales se les asigna una confianza del 100 % (confianza máxima). Por lo tanto, si hay recursos de vídeo con etiquetas manuales que coinciden con la consulta de búsqueda, se muestran antes que las etiquetas inteligentes que coinciden con la consulta de búsqueda.

## Restricciones {#video-smart-tagging-limitations}

* No puede entrenar el servicio que aplica etiquetas inteligentes a vídeos mediante vídeos específicos. Funciona de forma predeterminada [!DNL Adobe Sensei] configuración.

* El progreso del etiquetado no se muestra.

* Solo se etiquetan automáticamente los vídeos menores de 300 MB en tamaño de archivo. La variable [!DNL Adobe Sensei] omite los archivos de vídeo de mayor tamaño.

* Solo los vídeos en los formatos de archivo y los códecs compatibles mencionados en [Etiquetas inteligentes](/help/assets/smart-tags.md#smart-tags-supported-file-formats) están etiquetadas.

**Consulte también**

* [Traducir recursos](translate-assets.md)
* [API HTTP de Recursos](mac-api-assets.md)
* [Formatos de archivo compatibles con Assets](file-format-support.md)
* [Buscar recursos](search-assets.md)
* [Recursos conectados](use-assets-across-connected-assets-instances.md)
* [Informes de Asset](asset-reports.md)
* [Esquemas de metadatos](metadata-schemas.md)
* [Descarga de recursos](download-assets-from-aem.md)
* [Administración de metadatos](manage-metadata.md)
* [Facetas de búsqueda](search-facets.md)
* [Administrar colecciones](manage-collections.md)
* [Importación masiva de metadatos](metadata-import-export.md)

>[!MORELIKETHIS]
>
>* [Administración de etiquetas inteligentes y búsquedas de recursos](smart-tags.md#manage-smart-tags-and-searches)
>* [Capacite el servicio de etiquetas inteligentes y etiquete sus imágenes](smart-tags.md)

