---
title: Etiquetado inteligente de recursos de vídeo
description: El Experience Manager agrega automáticamente etiquetas inteligentes contextuales y descriptivas a los vídeos mediante [!DNL Adobe Sensei].
feature: Etiquetas inteligentes,Etiquetado
role: Administrator,Business Practitioner
exl-id: b59043c5-5df3-49a7-b4fc-da34c03649d7
translation-type: tm+mt
source-git-commit: 87d7cbb4463235a835d18fce49d06315a7c87526
workflow-type: tm+mt
source-wordcount: '1186'
ht-degree: 0%

---

# Etiquetado inteligente de los recursos de vídeo {#video-smart-tags}

La creciente necesidad de nuevo contenido exige reducir los esfuerzos manuales para ofrecer experiencias digitales atractivas en poco tiempo. [!DNL Adobe Experience Manager] como  [!DNL Cloud Service] admite el etiquetado automático de recursos de vídeo mediante inteligencia artificial. Etiquetar los vídeos manualmente puede llevar mucho tiempo. Sin embargo, la función de etiquetado inteligente de vídeo con tecnología [!DNL Adobe Sensei] utiliza modelos de inteligencia artificial para analizar el contenido de vídeo y añadir etiquetas a los recursos de vídeo. De este modo, se reduce el tiempo para que los usuarios de DAM entreguen experiencias enriquecidas a sus clientes. El servicio de aprendizaje automático de Adobe genera dos conjuntos de etiquetas para un vídeo. Mientras que un conjunto corresponde a objetos, escenas y atributos de ese vídeo; el otro conjunto está relacionado con acciones como beber, correr y correr.

El etiquetado de vídeo está habilitado de forma predeterminada en [!DNL Adobe Experience Manager] como [!DNL Cloud Service]. Sin embargo, puede [excluir el etiquetado inteligente de vídeo](#opt-out-video-smart-tagging) en una carpeta. Los vídeos se etiquetan automáticamente al cargar nuevos vídeos o al volver a procesar los existentes. [!DNL Experience Manager] también crea las miniaturas y extrae metadatos de los archivos de vídeo. Las etiquetas inteligentes se muestran en orden descendente de su [puntuación de confianza](#confidence-score-video-tag) en el recurso [!UICONTROL Propiedades].

## Etiquetado inteligente de vídeos al cargar {#smart-tag-assets-on-ingestion}

Cuando [carga recursos de vídeo](add-assets.md#upload-assets) en [!DNL Adobe Experience Manager] como [!DNL Cloud Service], los vídeos se procesan. Una vez completado el procesamiento, consulte la pestaña [!UICONTROL Basic] de la página [!UICONTROL Properties] del recurso. Las etiquetas inteligentes se añaden automáticamente al vídeo en [!UICONTROL Etiquetas inteligentes]. Los microservicios de recursos aprovechan [!DNL Adobe Sensei] para crear estas etiquetas inteligentes.

![Las etiquetas inteligentes se añaden a los vídeos y se ven en la pestaña Básico de las propiedades de recursos](assets/smart-tags-added-to-videos.png)

Las etiquetas inteligentes aplicadas se ordenan en orden descendente de [puntuación de confianza](#confidence-score-video-tag), combinadas para etiquetas de objeto y acción, dentro de [!UICONTROL Etiquetas inteligentes].

>[!IMPORTANT]
>
>Se recomienda revisar estas etiquetas generadas automáticamente para asegurarse de que se ajustan a la marca y a sus valores.

## Etiquetado inteligente de vídeos existentes en DAM {#smart-tag-existing-videos}

Los recursos de vídeo existentes en DAM no se etiquetan automáticamente como inteligentes. Debe [!UICONTROL Reprocesar los recursos] manualmente para generar etiquetas inteligentes para ellos.

Para etiquetar de forma inteligente los recursos de vídeo o las carpetas (incluidas las subcarpetas) de recursos que ya existen en el repositorio de recursos, siga estos pasos:

1. Seleccione el logotipo [!DNL Adobe Experience Manager] y, a continuación, seleccione recursos en la página [!UICONTROL Navegación].

1. Seleccione [!UICONTROL Files] para mostrar la interfaz de Assets.

1. Vaya a la carpeta a la que desea aplicar etiquetas inteligentes.

1. Seleccione toda la carpeta o recursos de vídeo específicos.

1. Seleccione el icono ![Reprocesar recursos](assets/do-not-localize/reprocess-assets-icon.png) [!UICONTROL Reprocesar recursos] y seleccione la opción [!UICONTROL Procesamiento completo].

<!-- TBD: Limit size -->

![Volver a procesar recursos para agregar etiquetas a los vídeos del repositorio DAM existente](assets/reprocess.gif)

Una vez completado el proceso, vaya a la página [!UICONTROL Properties] de cualquier recurso de vídeo de la carpeta. Las etiquetas añadidas automáticamente se ven en la sección [!UICONTROL Etiquetas inteligentes] de la pestaña [!UICONTROL Básico]. Estas etiquetas inteligentes aplicadas se ordenan en orden descendente de [puntuación de confianza](#confidence-score-video-tag).

## Buscar vídeos etiquetados {#search-smart-tagged-videos}

Para buscar los recursos de vídeo en función de las etiquetas inteligentes generadas automáticamente, utilice [Omnisearch](search-assets.md#search-assets-in-aem):

1. Seleccione el icono de búsqueda ![search icon](assets/do-not-localize/search_icon.png) para mostrar el campo Omnisearch .

1. Especifique una etiqueta, en el campo Omnisearch , que no haya agregado explícitamente a un vídeo.

1. Busque en función de la etiqueta .

Los resultados de la búsqueda muestran los recursos de vídeo en función de la etiqueta especificada.

Los resultados de búsqueda son una combinación de recursos de vídeo con palabras clave buscadas en los metadatos y los recursos de vídeo que están etiquetados de forma inteligente con las palabras clave buscadas. Sin embargo, los resultados de búsqueda que coinciden con todos los términos de búsqueda en los campos de metadatos se muestran primero, seguidos de los resultados de búsqueda que coinciden con cualquiera de los términos de búsqueda en las etiquetas inteligentes. Para obtener más información, consulte [Comprender [!DNL Experience Manager] resultados de búsqueda con etiquetas inteligentes](smart-tags.md#understand-search).

## Moderar etiquetas inteligentes de vídeo {#moderate-video-smart-tags}

[!DNL Adobe Experience Manager] permite depurar las etiquetas inteligentes para:

* elimine las etiquetas inexactas asignadas a los vídeos de marca.

* refinar las búsquedas de vídeos basadas en etiquetas, asegurándose de que el vídeo aparezca en los resultados de búsqueda para las etiquetas más relevantes. Por lo tanto, elimina las posibilidades de que los vídeos no relacionados se muestren en los resultados de búsqueda.

* asignar una clasificación superior a una etiqueta para aumentar su relevancia con respecto a un vídeo. La promoción de una etiqueta para un vídeo aumenta las posibilidades de que el vídeo aparezca en los resultados de búsqueda cuando se realiza una búsqueda basada en esa etiqueta.

Para obtener más información sobre cómo moderar las etiquetas inteligentes para los recursos, consulte [Administrar etiquetas inteligentes](smart-tags.md#manage-smart-tags-and-searches).

![Moderar etiquetas inteligentes de vídeo](assets/manage-video-smart-tags.png)

>[!NOTE]
>
>Las etiquetas moderadas mediante los pasos de [Administrar etiquetas inteligentes](smart-tags.md#manage-smart-tags-and-searches) no se recuerdan al reprocesar el recurso. El conjunto original de etiquetas se muestra de nuevo.

## Exclusión del etiquetado inteligente de vídeo {#opt-out-video-smart-tagging}

Como el etiquetado automático de vídeos se ejecuta en paralelo a otras tareas de procesamiento de recursos, como la creación de miniaturas y la extracción de metadatos, puede requerir mucho tiempo. Para acelerar el procesamiento de recursos, puede desactivar el etiquetado inteligente de vídeo en la carga a nivel de carpeta.

Para desactivar la generación automatizada de etiquetas inteligentes de vídeo para los recursos cargados en una carpeta específica:

1. Abra la pestaña [!UICONTROL Asset Processing] en la carpeta [!UICONTROL Properties].

1. En el menú [!UICONTROL Etiquetas inteligentes para vídeos], la opción [!UICONTROL Heredada] está seleccionada de forma predeterminada y la etiqueta inteligente de vídeo está habilitada.

   Cuando se selecciona la opción [!UICONTROL Heredada], la ruta de la carpeta heredada también está visible junto con la información si está configurada como [!UICONTROL Habilitar] o [!UICONTROL Deshabilitar].

   ![Desactivación del etiquetado inteligente de vídeo](assets/disable-video-tagging.png)

1. Seleccione [!UICONTROL Disable] para desactivar el etiquetado inteligente de los vídeos cargados en la carpeta.

>[!IMPORTANT]
>
>Si ha optado por no etiquetar vídeos en una carpeta en el momento de la carga y desea etiquetar los vídeos de forma inteligente después de la carga, **[!UICONTROL Habilitar etiquetas inteligentes para vídeos]** en la pestaña [!UICONTROL Procesamiento de recursos] de la carpeta [!UICONTROL Propiedades] y utilice la opción [[!UICONTROL Reprocesar recursos]](#smart-tag-existing-videos) para agregar etiquetas inteligentes el vídeo.

## Puntuación de confianza {#confidence-score-video-tag}

[!DNL Adobe Experience Manager] aplica un umbral de confianza mínimo para las etiquetas inteligentes de objeto y acción para evitar tener demasiadas etiquetas para cada recurso de vídeo, lo que ralentiza la indexación. Los resultados de la búsqueda de recursos se clasifican según las puntuaciones de confianza, lo que generalmente mejora los resultados de la búsqueda más allá de lo que sugiere una inspección de las etiquetas asignadas a cualquier recurso de vídeo. Las etiquetas inexactas suelen tener puntuaciones de confianza bajas, por lo que rara vez aparecen en la parte superior de la lista de etiquetas inteligentes para los recursos.

El umbral predeterminado para las etiquetas de objeto y acción en [!DNL Adobe Experience Manager] es 0,7 (debe ser un valor entre 0 y 1). Si algunos recursos de vídeo no están etiquetados con una etiqueta específica, entonces indica que el algoritmo tiene menos del 70 % de confianza en las etiquetas predichas. Es posible que el umbral predeterminado no sea siempre óptimo para todos los usuarios. Por lo tanto, puede cambiar el valor de puntuación de confianza en la configuración OSGI.

Para agregar la configuración OSGI de puntuación de confianza al proyecto implementado en [!DNL Adobe Experience Manager] como [!DNL Cloud Service] a [!DNL Cloud Manager]:

* En el proyecto [!DNL Adobe Experience Manager] (`ui.config` desde Tipo de archivo 24 o anteriormente `ui.apps`) la configuración `config.author` OSGi, incluya un archivo de configuración denominado `com.adobe.cq.assetcompute.impl.senseisdk.SenseiSdkImpl.cfg.json` con el siguiente contenido:

```json
{
  "minVideoActionConfidenceScore":0.5,
  "minVideoObjectConfidenceScore":0.5,
}
```

>[!NOTE]
>
>A las etiquetas manuales se les asigna una confianza del 100 % (confianza máxima). Por lo tanto, si hay recursos de vídeo con etiquetas manuales que coinciden con la consulta de búsqueda, se muestran antes que las etiquetas inteligentes que coinciden con la consulta de búsqueda.

## Restricciones     {#video-smart-tagging-limitations}

* No puede entrenar el servicio que aplica etiquetas inteligentes a vídeos mediante vídeos específicos. Funciona con la configuración predeterminada [!DNL Adobe Sensei].

* El progreso del etiquetado no se muestra.

* Solo se etiquetan automáticamente los vídeos menores de 300 MB en tamaño de archivo. El servicio [!DNL Adobe Sensei] omite los archivos de vídeo de mayor tamaño.

* Solo se etiquetan los vídeos en los formatos de archivo y los códecs compatibles mencionados en [Etiquetas inteligentes](/help/assets/smart-tags.md#smart-tags-supported-file-formats).

>[!MORELIKETHIS]
>
>* [Administración de etiquetas inteligentes y búsquedas de recursos](smart-tags.md#manage-smart-tags-and-searches)
>* [Capacite el servicio de etiquetas inteligentes y etiquete sus imágenes](smart-tags.md)

