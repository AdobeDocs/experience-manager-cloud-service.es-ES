---
title: Etiquetar recursos automáticamente con [!DNL Adobe Sensei] servicio inteligente
description: Etiquete los recursos con un servicio inteligente artificialmente que aplique etiquetas comerciales contextuales y descriptivas.
contentOwner: AG
feature: Etiquetas inteligentes,Etiquetado
role: Administrator,Business Practitioner
exl-id: a2abc48b-5586-421c-936b-ef4f896d78b7
translation-type: tm+mt
source-git-commit: d86581f61c9dd7339f7deb8ee1f5e469ce2b5f7c
workflow-type: tm+mt
source-wordcount: '2707'
ht-degree: 6%

---


# Agregue etiquetas inteligentes a los recursos para mejorar la experiencia de búsqueda {#smart-tag-assets-for-faster-search}

Las organizaciones que se ocupan de los recursos digitales utilizan cada vez más el vocabulario controlado por taxonomía en los metadatos de los recursos. Esencialmente, incluye una lista de palabras clave que los empleados, socios y clientes suelen utilizar para referirse a sus recursos digitales y buscarlos. El etiquetado de recursos con vocabulario controlado por taxonomía garantiza que los recursos se puedan identificar y recuperar fácilmente en las búsquedas.

En comparación con los vocabularios de lenguaje natural, el etiquetado basado en la taxonomía empresarial ayuda a alinear los activos con el negocio de una empresa y garantiza que los activos más relevantes aparezcan en las búsquedas. Por ejemplo, un fabricante de coches puede etiquetar imágenes de coche con nombres de modelo, de modo que solo se muestren imágenes relevantes cuando se realice una búsqueda para diseñar una campaña de promoción.

En segundo plano, la funcionalidad utiliza el marco artificialmente inteligente de [Adobe Sensei](https://www.adobe.com/sensei/experience-cloud-artificial-intelligence.html) para entrenar su algoritmo de reconocimiento de imágenes en la estructura de etiquetas y la taxonomía empresarial. A continuación, esta inteligencia de contenido se utiliza para aplicar etiquetas relevantes en un conjunto diferente de recursos. Las nuevas implementaciones [!DNL Experience Manager Assets] están integradas con [!DNL Adobe Developer Console] de forma predeterminada. Ayuda a configurar la funcionalidad de las etiquetas inteligentes más rápido. En las implementaciones anteriores, los administradores pueden [configurar manualmente la integración de etiquetas inteligentes](/help/assets/smart-tags-configuration.md#aio-integration).

<!-- TBD: Create a flowchart for how training works in CS.
![flowchart](assets/flowchart.gif) 
-->

## Tipos de recursos admitidos {#smart-tags-supported-file-formats}

Puede etiquetar los siguientes tipos de recursos:

* **Imágenes**: Las imágenes en muchos formatos se etiquetan con los servicios de contenido inteligente de Adobe Sensei. Usted [crea un modelo de capacitación](#train-model) y luego [aplica etiquetas inteligentes](#tag-assets) a las imágenes. Las etiquetas inteligentes se aplican a los tipos de archivo compatibles que generan representaciones en formato JPG y PNG.
* **Recursos basados en texto**:  [!DNL Experience Manager Assets] etiqueta automáticamente los recursos basados en texto compatibles al cargarlos. Obtenga más información sobre el [etiquetado de recursos basados en texto](#smart-tag-text-based-assets).
* **Recursos de vídeo**: El etiquetado de vídeo está habilitado de forma predeterminada en  [!DNL Adobe Experience Manager] as a  [!DNL Cloud Service]. [Los vídeos se ](/help/assets/smart-tags-video-assets.md) etiquetan automáticamente cuando se cargan nuevos vídeos o se reprocesan los existentes.

| Imágenes (tipos MIME) | Recursos basados en texto (formatos de archivo) | Recursos de vídeo (formatos de archivo y códecs) |
|----|-----|------|
| image/jpeg | CSV | MP4 (H264/AVC) |
| image/tiff | DOC | MKV (H264/AVC) |
| image/png | DOCX | MOV (H264/AVC, Motion JPEG) |
| image/bmp | HTML | AVI (vídeo4) |
| image/gif | PDF | FLV (H264/AVC, vp6f) |
| image/pjpeg | PPT | WMV (WMV2) |
| image/x-portable-anymap | PPTX |  |
| image/x-portable-bitmap | RTF |  |
| image/x-portable-graymap | SRT |  |
| image/x-portable-pixmap | TXT |  |
| image/x-rgb | VTT |  |
| image/x-xbitmap |  |  |
| image/x-xpixmap |  |  |
| image/x-icon |  |  |
| imagen/photoshop |  |  |
| image/x-photoshop |  |  |
| image/psd |  |  |
| image/vnd.adobe.photoshop |  |  |

[!DNL Experience Manager] agrega automáticamente las etiquetas inteligentes a los recursos basados en texto y a los vídeos de forma predeterminada. Para agregar automáticamente etiquetas inteligentes a imágenes, complete las siguientes tareas.

* [Comprender los modelos y las directrices de etiquetas](#understand-tag-models-guidelines).
* [Capacite al modelo](#train-model).
* [Etiquete sus recursos digitales](#tag-assets).
* [Administre las etiquetas y las búsquedas](#manage-smart-tags-and-searches).

<!-- TBD: Is there a link to buy SCS or initiate a sales call. How are AIO services sold? Provide a CTA here to buy or contacts Sales team. -->

## Etiquetado de recursos basados en texto con etiquetas inteligentes {#smart-tag-text-based-assets}

Los recursos basados en texto compatibles se etiquetan automáticamente con [!DNL Experience Manager Assets] al cargarse. Está activada de forma predeterminada. La eficacia de las etiquetas inteligentes no depende de la cantidad de texto del recurso, sino de las palabras clave o entidades relevantes presentes en el texto del recurso. Para los recursos basados en texto, las etiquetas inteligentes son las palabras clave que aparecen en el texto, pero las que mejor describen el recurso. En el caso de los recursos admitidos, [!DNL Experience Manager] ya extrae el texto, que luego se indexa y se utiliza para buscar los recursos. Sin embargo, las etiquetas inteligentes basadas en palabras clave del texto proporcionan una faceta de búsqueda dedicada, estructurada y de mayor prioridad que se utiliza para mejorar la detección de recursos en comparación con el índice de búsqueda completa.

En comparación, para imágenes y vídeos, las etiquetas inteligentes se derivan de un aspecto visual.

## Comprender los modelos de etiquetas y las directrices {#understand-tag-models-guidelines}

Un modelo de etiqueta es un grupo de etiquetas relacionadas que están asociadas con varios aspectos visuales de las imágenes que se están etiquetando. Las etiquetas están relacionadas con los aspectos visuales de las imágenes, que son claramente diferentes, de modo que, cuando se aplican, las etiquetas ayudan a buscar tipos específicos de imágenes. Por ejemplo, una colección de zapatos puede tener etiquetas diferentes, pero todas las etiquetas están relacionadas con zapatos y pueden pertenecer al mismo modelo de etiquetas. Cuando se aplican, las etiquetas ayudan a encontrar diferentes tipos de zapatos, por ejemplo por color, por diseño o por uso. Para comprender la representación de contenido de un modelo de formación en [!DNL Experience Manager], visualice un modelo de formación como una entidad de nivel superior compuesta por un grupo de etiquetas agregadas manualmente e imágenes de ejemplo para cada etiqueta. Cada etiqueta se puede aplicar exclusivamente a una imagen.

Antes de crear un modelo de etiquetas y entrenar el servicio, identifique un conjunto de etiquetas únicas que describan mejor los objetos de las imágenes en el contexto de su negocio. Asegúrese de que los recursos del conjunto depurado cumplen [las directrices de formación](#training-guidelines).

### Directrices de formación {#training-guidelines}

Asegúrese de que las imágenes del conjunto de formación cumplen las siguientes directrices:

**Cantidad y tamaño:** Mínimo de 10 imágenes y máximo de 50 imágenes por etiqueta.

**Coherencia**: Asegúrese de que las imágenes de una etiqueta son visualmente similares. Es mejor añadir las etiquetas de los mismos aspectos visuales (como el mismo tipo de objetos en una imagen) juntos en un único modelo de etiqueta. Por ejemplo, no es aconsejable etiquetar todas estas imágenes como `my-party` (para formación) porque no son visualmente similares.

![Imágenes ilustrativas para ejemplificar las directrices de formación](assets/do-not-localize/coherence.png)

**Cobertura**: Debería haber suficiente variedad en las imágenes de la formación. La idea es dar algunos ejemplos, pero razonablemente diversos, para que AEM aprenda a centrarse en las cosas correctas. Si está aplicando la misma etiqueta en imágenes visualmente diferentes, incluya al menos cinco ejemplos de cada tipo. Por ejemplo, para la etiqueta *model-down-pose*, incluya más imágenes de capacitación similares a la imagen resaltada a continuación para que el servicio identifique imágenes similares con mayor precisión durante el etiquetado.

![Imágenes ilustrativas para ejemplificar las directrices de formación](assets/do-not-localize/coverage_1.png)

**Distracción/obstrucción**: El servicio forma mejor con imágenes que tienen menos distracción (fondos destacados, acompañamientos no relacionados, como objetos/personas con el tema principal). Por ejemplo, para la etiqueta *casual-shoe*, la segunda imagen no es un buen candidato para la formación.

![Imágenes ilustrativas para ejemplificar las directrices de formación](assets/do-not-localize/distraction.png)

**Complejidad:** Si una imagen cumple los requisitos para más de una etiqueta, agregue todas las etiquetas aplicables antes de incluir la imagen para formación. Por ejemplo, para las etiquetas, como *impermeable* y *vista del lado del modelo*, agregue ambas etiquetas en el recurso que cumple los requisitos antes de incluirlo para formación.

![Imágenes ilustrativas para ejemplificar las directrices de formación](assets/do-not-localize/completeness.png)

**Número de etiquetas**: Adobe recomienda que prepare un modelo utilizando al menos dos etiquetas diferentes y al menos diez imágenes diferentes para cada etiqueta. En un modelo de etiqueta única, no agregue más de 50 etiquetas.

**Número de ejemplos**: Para cada etiqueta, añada al menos diez ejemplos. Sin embargo, Adobe recomienda unos 30 ejemplos. Se admite un máximo de 50 ejemplos por etiqueta.

**Prevención de falsos positivos y conflictos**: Adobe recomienda crear un modelo de etiqueta única para un aspecto visual único. Organice los modelos de etiquetas de forma que se eviten las etiquetas superpuestas entre los modelos. Por ejemplo, no utilice etiquetas comunes como `sneakers` en dos modelos de etiquetas diferentes: `shoes` y `footwear`. El proceso de formación sobrescribe un modelo de etiquetas entrenado con el otro para una palabra clave común.

**Ejemplos**: Algunos ejemplos más para obtener instrucciones son:

* Cree un modelo de etiqueta que incluya:
   * solo las etiquetas relacionadas con los modelos de coche.
   * sólo las etiquetas relacionadas con los colores de las camisas.
   * solo las etiquetas relacionadas con las chaquetas para hombres y mujeres.
* No crear,
   * modelo de etiqueta que incluye modelos de automóvil publicados en 2019 y 2020.
   * varios modelos de etiquetas que incluyen los mismos modelos de coche.

**Imágenes usadas para entrenar**: Puede usar las mismas imágenes para entrenar diferentes modelos de etiquetas. Sin embargo, no asocie una imagen con más de una etiqueta en un modelo de etiquetas. Es posible etiquetar la misma imagen con etiquetas diferentes que pertenecen a modelos de etiquetas diferentes.

No se puede deshacer la formación. Las directrices anteriores le ayudarán a elegir buenas imágenes para entrenar.

## Capacite el modelo para sus etiquetas personalizadas {#train-model}

Para crear y entrenar un modelo para etiquetas específicas de su empresa, siga estos pasos:

1. Cree las etiquetas necesarias y la estructura de etiquetas adecuada. Cargue las imágenes relevantes en el repositorio DAM.
1. En la interfaz de usuario [!DNL Experience Manager], acceda a **[!UICONTROL Assets]** > **[!UICONTROL Formación sobre etiquetas inteligentes]**.
1. Haga clic en **[!UICONTROL Crear]**. Proporcione un **[!UICONTROL Título]**, **[!UICONTROL Descripción]**.
1. Busque y seleccione las etiquetas de las etiquetas existentes en `cq:tags` para las que desea entrenar el modelo. Haga clic en **[!UICONTROL Siguiente]**. 
1. En el cuadro de diálogo **[!UICONTROL Seleccionar recursos]**, haga clic en **[!UICONTROL Agregar recursos]** con cada etiqueta. Busque en el repositorio de DAM o busque el repositorio para seleccionar al menos 10 y como máximo 50 imágenes. Seleccione los recursos y no la carpeta. Una vez seleccionadas las imágenes, haga clic en **[!UICONTROL Seleccionar]**.

   ![Ver el estado de la formación](assets/smart-tags-training-status.png)

1. Para obtener una vista previa de las miniaturas de las imágenes seleccionadas, haga clic en el acordeón delante de una etiqueta. Puede modificar la selección haciendo clic en **[!UICONTROL Add Assets]**. Una vez que esté satisfecho con la selección, haga clic en **[!UICONTROL Submit]**. La interfaz de usuario muestra una notificación en la parte inferior de la página que indica que se ha iniciado la formación.
1. Compruebe el estado de la formación en la columna **[!UICONTROL Status]** para cada modelo de etiquetas. Los estados posibles son [!UICONTROL Pendiente], [!UICONTROL Entrenado] y [!UICONTROL Fallido].

![Flujo de trabajo para entrenar el modelo de etiquetado para etiquetas inteligentes](assets/smart-tag-model-training-flow.png)

*Figura: Pasos del flujo de trabajo de formación para formar el modelo de etiquetado.*

### Ver el estado de la formación y el informe {#training-status}

Para comprobar si el servicio Etiquetas inteligentes está formado sobre las etiquetas en el conjunto de recursos de formación, revise el informe del flujo de trabajo de formación desde la consola Informes .

1. En la interfaz [!DNL Experience Manager], vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Recursos]** > **[!UICONTROL Informes]**.
1. En la página **[!UICONTROL Informes de recursos]**, haga clic en **[!UICONTROL Crear]**.
1. Seleccione el informe **[!UICONTROL Formación sobre etiquetas inteligentes]** y, a continuación, haga clic en **[!UICONTROL Siguiente]** en la barra de herramientas.
1. Especifique un título y una descripción para el informe. En **[!UICONTROL Programar informe]**, deje seleccionada la opción **[!UICONTROL Ahora]**. Si desea programar el informe para más adelante, seleccione **[!UICONTROL Más adelante]** e indique una fecha y una hora. A continuación, haga clic en **[!UICONTROL Create]** en la barra de herramientas.
1. En la página **[!UICONTROL Informes de recursos]**, seleccione el informe que ha generado. Para ver el informe, haga clic en **[!UICONTROL Ver]** en la barra de herramientas.
1. Revise los detalles del informe. El informe muestra el estado de la formación de las etiquetas que ha entrenado. El color verde de la columna **[!UICONTROL Estado de formación]** indica que el servicio Etiquetas inteligentes ha recibido formación para la etiqueta. El color amarillo indica que el servicio no está completamente entrenado para una etiqueta en particular. En este caso, agregue más imágenes con la etiqueta en concreto y ejecute el flujo de trabajo de formación para que el servicio se imparta completamente en la etiqueta. Si no ve las etiquetas en este informe, ejecute de nuevo el flujo de trabajo de formación para estas etiquetas.Etiquetas
1. Para descargar el informe, selecciónelo en la lista y haga clic en **[!UICONTROL Descargar]** en la barra de herramientas. El informe se descarga como una hoja de cálculo [!DNL Microsoft Excel].

## Etiquetar recursos {#tag-assets}

Una vez que haya formado el servicio Etiquetas inteligentes, puede almacenar en déclencheur el flujo de trabajo de etiquetado para aplicar las etiquetas automáticamente en un conjunto diferente de recursos. Puede aplicar el flujo de trabajo de etiquetado bajo demanda o programarlo para que se ejecute periódicamente. El flujo de trabajo de etiquetado se aplica tanto a los recursos como a las carpetas.

### Etiquetar recursos de la consola de flujo de trabajo {#tagging-assets-from-the-workflow-console}

1. En la interfaz [!DNL Experience Manager], vaya a **[!UICONTROL Tools]** > **[!UICONTROL Workflow]** > **[!UICONTROL Models]**.
1. En la página **[!UICONTROL Modelos de flujo de trabajo]**, seleccione el flujo de trabajo **[!UICONTROL Recursos de etiquetas inteligentes DAM]** y haga clic en **[!UICONTROL Iniciar flujo de trabajo]** en la barra de herramientas.

   ![dam_smart_tag_workflow](assets/dam_smart_tag_workflow.png)

1. En el cuadro de diálogo **[!UICONTROL Ejecutar flujo de trabajo]**, vaya a la carpeta de carga útil que contiene los recursos en los que desea aplicar las etiquetas automáticamente.
1. Especifique un título para el flujo de trabajo y un comentario opcional. Haga clic en **[!UICONTROL Ejecutar]**.

   ![tagging_dialog](assets/tagging_dialog.png)

   *Figura: Vaya a la carpeta de recursos y revise las etiquetas para comprobar si los recursos están etiquetados correctamente. Para obtener más información, consulte [administrar etiquetas inteligentes](#manage-smart-tags-and-searches).*

### Etiquetar recursos de la cronología {#tagging-assets-from-the-timeline}

1. En la interfaz de usuario [!DNL Assets], seleccione la carpeta que contiene los recursos o recursos específicos a los que desea aplicar las etiquetas inteligentes.
1. En la esquina superior izquierda, abra la **[!UICONTROL Línea de tiempo]**.
1. Abra las acciones desde la parte inferior de la barra lateral izquierda y haga clic en **[!UICONTROL Iniciar flujo de trabajo]**.

   ![start_workflow](assets/start_workflow.png)

1. Seleccione el flujo de trabajo **[!UICONTROL DAM Smart Tag Assets]** y especifique un título para el flujo de trabajo.
1. Haga clic en **[!UICONTROL Start]**. El flujo de trabajo aplica las etiquetas a los recursos. Vaya a la carpeta de recursos y revise las etiquetas para comprobar que los recursos están etiquetados correctamente. Para obtener más información, consulte [administrar etiquetas inteligentes](#manage-smart-tags-and-searches).

>[!NOTE]
>
>En los ciclos de etiquetado posteriores, solo los recursos modificados se etiquetan de nuevo con etiquetas recién formadas. Sin embargo, incluso los recursos sin modificar se etiquetan si el espacio entre los ciclos de etiquetado último y actual para el flujo de trabajo de etiquetado supera las 24 horas. Para los flujos de trabajo de etiquetado periódicos, los recursos sin modificar se etiquetan cuando el lapso de tiempo supera los seis meses.

### Etiquetar recursos cargados {#tag-uploaded-assets}

[!DNL Experience Manager] puede etiquetar automáticamente los recursos que los usuarios cargan en DAM. Para ello, los administradores configuran un flujo de trabajo para añadir un paso disponible que etiquete los recursos. Consulte [cómo habilitar las etiquetas inteligentes para los recursos cargados](/help/assets/smart-tags-configuration.md#enable-smart-tagging-for-uploaded-assets).

## Administrar etiquetas inteligentes y búsquedas de recursos {#manage-smart-tags-and-searches}

Puede depurar las etiquetas inteligentes para eliminar cualquier etiqueta incorrecta que se haya asignado a los recursos de su marca, de modo que solo se muestren las etiquetas más relevantes.

Moderar las etiquetas inteligentes también ayuda a refinar las búsquedas basadas en etiquetas de recursos, ya que garantiza que los recursos aparezcan en los resultados de búsqueda de las etiquetas más relevantes. Esencialmente, ayuda a eliminar las posibilidades de que recursos no relacionados se muestren en los resultados de búsqueda.

También puede asignar una clasificación superior a una etiqueta para aumentar la relevancia de la etiqueta para el recurso. La promoción de una etiqueta para un recurso aumenta las posibilidades de que el recurso aparezca en los resultados de búsqueda cuando se realiza una búsqueda basada en la etiqueta en particular.

Para moderar las etiquetas inteligentes de los recursos:

1. En el campo de búsqueda, busque recursos basados en una etiqueta .

1. Inspect muestra los resultados de la búsqueda para identificar los recursos que no considera relevantes para la búsqueda.

1. Seleccione el recurso y, a continuación, seleccione ![Administrar etiquetas ](assets/do-not-localize/manage-tags-icon.png) en la barra de herramientas.

1. En la página **[!UICONTROL Administrar etiquetas]**, inspeccione las etiquetas. Si no desea que se busque el recurso en función de una etiqueta específica, seleccione la etiqueta y seleccione ![Eliminar icono](assets/do-not-localize/delete-icon.png) en la barra de herramientas. También puede seleccionar el símbolo `X` situado junto a la etiqueta.

1. Para asignar una clasificación superior a una etiqueta, seleccione la etiqueta y seleccione ![Icono de promoción](assets/do-not-localize/promote-icon.png) en la barra de herramientas. La etiqueta que promocione se moverá a la sección **[!UICONTROL Etiquetas]**.

1. Seleccione **[!UICONTROL Guardar]** y, a continuación, seleccione **[!UICONTROL Aceptar]** para cerrar el cuadro de diálogo [!UICONTROL Éxito].

1. Vaya a la página [!UICONTROL Propiedades] del recurso. Observe que a la etiqueta que promocionó se le asigna una alta relevancia y, por lo tanto, aparece más arriba en los resultados de búsqueda.

### Comprender AEM resultados de búsqueda con etiquetas inteligentes {#understand-search}

De forma predeterminada, AEM búsqueda combina los términos de búsqueda con una cláusula `AND`. El uso de etiquetas inteligentes no cambia este comportamiento predeterminado. El uso de etiquetas inteligentes agrega una cláusula `OR` para encontrar cualquiera de los términos de búsqueda en las etiquetas inteligentes aplicadas. Por ejemplo, considere la búsqueda de `woman running`. Los recursos con solo `woman` o con `running` palabra clave en los metadatos no aparecen en los resultados de búsqueda de forma predeterminada. Sin embargo, en una consulta de búsqueda de este tipo aparece un recurso etiquetado con `woman` o `running` etiquetas inteligentes. Así que los resultados de la búsqueda son una combinación de:

* recursos con palabras clave `woman` y `running` en los metadatos.

* activos con etiquetas inteligentes con cualquiera de las palabras clave.

Los resultados de búsqueda que coinciden con todos los términos de búsqueda en los campos de metadatos se muestran primero, seguidos de los resultados de búsqueda que coinciden con cualquiera de los términos de búsqueda en las etiquetas inteligentes. En el ejemplo anterior, el orden aproximado de visualización de los resultados de búsqueda es:

1. coincidencias de `woman running` en los distintos campos de metadatos.
1. coincidencias de `woman running` en etiquetas inteligentes.
1. coincidencias de `woman` o de `running` en las etiquetas inteligentes.

## Limitaciones de etiquetado y prácticas recomendadas {#limitations}

El etiquetado inteligente mejorado se basa en modelos de aprendizaje de imágenes y sus etiquetas. Estos modelos no siempre son perfectos para identificar etiquetas. La versión actual de las etiquetas inteligentes tiene las siguientes limitaciones:

* Incapacidad para reconocer sutiles diferencias en imágenes. Por ejemplo, camisas delgadas contra las vestidas regulares.
* Incapacidad para identificar etiquetas basadas en pequeños patrones o partes de una imagen. Por ejemplo, logotipos en camisetas.
* El etiquetado es compatible con los idiomas compatibles con [!DNL Experience Manager]. Para obtener una lista de idiomas, consulte las [notas de la versión del servicio de contenido inteligente](https://experienceleague.adobe.com/docs/experience-manager-64/release-notes/smart-content-service-release-notes.html#languages).
* Las etiquetas que no se gestionan de forma realista están relacionadas con:

   * Aspectos no visuales, abstractos. Por ejemplo, el año o la temporada de lanzamiento de un producto, estado de ánimo o emoción evocados por una imagen, la connotación subjetiva de un vídeo, etc.
   * Diferencias visuales finas en productos como camisas con y sin collares o logotipos de productos pequeños incrustados en productos.

<!-- TBD: Add limitations related to text-based assets. -->

Para buscar recursos con etiquetas inteligentes (normales o mejoradas), utilice la búsqueda [!DNL Assets] (búsqueda de texto completo). No hay predicado de búsqueda independiente para las etiquetas inteligentes.

>[!NOTE]
>
>La capacidad de las etiquetas inteligentes para formarse sobre sus etiquetas y aplicarlas en otras imágenes depende de la calidad de las imágenes que utilice para la formación.
>Para obtener mejores resultados, Adobe recomienda utilizar imágenes visualmente similares para entrenar el servicio para cada etiqueta.

>[!MORELIKETHIS]
>
>* [ [!DNL Experience Manager] Configurar para el etiquetado inteligente](smart-tags-configuration.md)
>* [Comprender cómo las etiquetas inteligentes ayudan a administrar recursos](https://medium.com/adobetech/efficient-asset-management-with-enhanced-smart-tags-887bd47dbb3f)
>* [Etiquetado inteligente de recursos de vídeo](smart-tags-video-assets.md)

