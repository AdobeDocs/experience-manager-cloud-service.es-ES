---
title: Etiquete imágenes con servicios artificialmente inteligentes.
description: Etiquete imágenes con servicios artificialmente inteligentes que apliquen etiquetas comerciales contextuales y descriptivas mediante los servicios de Adobe Sensei.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 33ce255e126f2a49f1c1a6e94955aade2ca0d240
workflow-type: tm+mt
source-wordcount: '2425'
ht-degree: 6%

---


# Servicio de etiquetas inteligentes de formación y etiquetado de imágenes {#train-service-tag-assets}

Las organizaciones que se ocupan de los activos digitales utilizan cada vez más el vocabulario controlado por taxonomía en los metadatos de los recursos. Básicamente, incluye una lista de palabras clave que los empleados, socios y clientes utilizan comúnmente para referirse a sus recursos digitales y buscarlos. El etiquetado de recursos con vocabulario controlado por taxonomía garantiza que los recursos se puedan identificar y recuperar fácilmente mediante búsquedas basadas en etiquetas.

En comparación con los vocabularios del lenguaje natural, el etiquetado basado en la taxonomía empresarial ayuda a alinear los activos con el negocio de una compañía y garantiza que los activos más relevantes aparezcan en las búsquedas. Por ejemplo, un fabricante de automóviles puede etiquetar imágenes de autos con nombres de modelo para que solo se muestren las imágenes relevantes cuando se busque para diseñar una campaña de promoción.

In the background, the Smart Tags uses an artificial intelligence framework of [Adobe Sensei](https://www.adobe.com/sensei/experience-cloud-artificial-intelligence.html) to train its image recognition algorithm on your tag structure and business taxonomy. Esta inteligencia de contenido se utiliza para aplicar etiquetas relevantes a un conjunto diferente de recursos.

<!-- TBD: Create a similar flowchart for how training works in CS.
![flowchart](assets/flowchart.gif) 
-->

Para utilizar el etiquetado inteligente, complete las siguientes tareas:

* [Integrar Experience Manager con Adobe Developer Console](#integrate-aem-with-aio).
* [Comprender los modelos de etiquetas y las directrices](#understand-tag-models-guidelines).
* [Entrena al modelo](#train-model).
* [Etiquete sus recursos](#tag-assets)digitales.
* [Administre las etiquetas y las búsquedas](#manage-smart-tags-and-searches).

Las etiquetas inteligentes solo se aplican a [!DNL Adobe Experience Manager Assets] los clientes. The Smart Tags is available for purchase as an add-on to [!DNL Experience Manager].

<!-- TBD: Is there a link to buy SCS or initiate a sales call. How are AIO services sold? -->

## Integrate [!DNL Experience Manager] with Adobe Developer Console {#integrate-aem-with-aio}

>[!IMPORTANT]
>
>Las nuevas [!DNL Experience Manager Assets] implementaciones se integran [!DNL Adobe Developer Console] de forma predeterminada. Ayuda a configurar la funcionalidad de etiquetas inteligentes más rápido. En las implementaciones existentes, los administradores pueden [configurar manualmente la integración](/help/assets/smart-tags-configuration.md#aio-integration)de etiquetas inteligentes.

Puede realizar la integración [!DNL Adobe Experience Manager] con las etiquetas inteligentes mediante [!DNL Adobe Developer Console]. Utilice esta configuración para acceder al servicio Etiquetas inteligentes desde dentro [!DNL Experience Manager]. Consulte [Configuración del Experience Manager para el etiquetado inteligente de recursos](smart-tags-configuration.md) para tareas a fin de configurar las etiquetas inteligentes. At the back end, the [!DNL Experience Manager] server authenticates your service credentials with the Adobe Developer Console gateway before forwarding your request to the Smart Tags service.

## Explicación de los modelos y directrices de etiquetas {#understand-tag-models-guidelines}

Un modelo de etiqueta es un grupo de etiquetas relacionadas que se basan en un aspecto visual de la imagen. Por ejemplo, una colección de zapatos puede tener etiquetas diferentes, pero todas las etiquetas están relacionadas con zapatos y pueden pertenecer al mismo modelo de etiquetas. Las etiquetas solo pueden relacionarse con los distintos aspectos visuales de las imágenes. Para comprender la representación de contenido de un modelo de formación en [!DNL Experience Manager], visualice un modelo de formación como una entidad de nivel superior compuesta por un grupo de etiquetas agregadas manualmente e imágenes de ejemplo para cada etiqueta. Cada etiqueta se puede aplicar exclusivamente a una imagen.

Las etiquetas que no se pueden controlar de forma realista están relacionadas con:

* Aspectos no visuales, abstractos como el año o la temporada de lanzamiento de un producto, estado de ánimo o emoción evocados por una imagen.
* Diferencias visuales finas en productos como camisas con y sin collares o logotipos de productos pequeños incorporados en productos.

Antes de crear un modelo de etiquetas y entrenar el servicio, identifique un conjunto de etiquetas únicas que describan mejor los objetos de las imágenes en el contexto de su negocio. Asegúrese de que los recursos del conjunto depurado cumplen [las directrices](#training-guidelines)de formación.

### Directrices de formación {#training-guidelines}

Las imágenes del conjunto de formación deben cumplir las siguientes directrices:

**Cantidad y tamaño:** Mínimo de 10 imágenes y máximo de 50 imágenes por etiqueta.

**Coherencia**: Las imágenes de una etiqueta deben ser visualmente similares. Es mejor agrupar las etiquetas de los mismos aspectos visuales (como el mismo tipo de objetos de una imagen) en un único modelo de etiquetas. Por ejemplo, no es recomendable etiquetar todas estas imágenes como `my-party` (para formación) porque no son visualmente similares.

![Imágenes ilustrativas para ejemplificar las directrices de formación](assets/do-not-localize/coherence.png)

**Cobertura**: Las imágenes de la formación deben ser suficientemente variadas. La idea es dar algunos ejemplos, pero razonablemente diversos, para que AEM aprenda a centrarse en las cosas correctas. Si está aplicando la misma etiqueta en imágenes visualmente diferentes, incluya al menos cinco ejemplos de cada tipo. Por ejemplo, para la etiqueta *model-down-pose*, incluya más imágenes de formación similares a la imagen resaltada a continuación para que el servicio identifique imágenes similares con mayor precisión durante el etiquetado.

![Imágenes ilustrativas para ejemplificar las directrices de formación](assets/do-not-localize/coverage_1.png)

**Distracción/obstrucción**: El servicio entrena mejor en imágenes que tienen menos distracción (fondos destacados, acompañamientos no relacionados, como objetos/personas con el tema principal). Por ejemplo, para la etiqueta *casual-shoe*, la segunda imagen no es un buen candidato para la formación.

![Imágenes ilustrativas para ejemplificar las directrices de formación](assets/do-not-localize/distraction.png)

**Complejidad:** Si una imagen cumple los requisitos para más de una etiqueta, agregue todas las etiquetas aplicables antes de incluir la imagen para formación. Por ejemplo, para las etiquetas, como *impermeable* y *vista del lado del modelo*, agregue ambas etiquetas en el recurso que cumple los requisitos antes de incluirlo para formación.

![Imágenes ilustrativas para ejemplificar las directrices de formación](assets/do-not-localize/completeness.png)

**Número de etiquetas**: Adobe recomienda que se forme un modelo utilizando al menos dos etiquetas diferentes y al menos 10 imágenes diferentes para cada etiqueta. En un solo modelo de etiquetas, no agregue más de 50 etiquetas.

**Número de ejemplos**: Para cada etiqueta, agregue al menos 10 ejemplos. Sin embargo, Adobe recomienda unos 30 ejemplos. Se admite un máximo de 50 ejemplos por etiqueta.

**Evitar falsos positivos y conflictos**: Adobe recomienda crear un modelo de etiqueta única para un solo aspecto visual. Organice los modelos de etiquetas de forma que se eviten las superposiciones de etiquetas entre los modelos. Por ejemplo, no utilice etiquetas comunes como `sneakers` en dos nombres `shoes` y `footwear`de modelos de etiquetas diferentes. El proceso de formación sobrescribe un modelo de etiquetas entrenado con el otro para una palabra clave común.

**Ejemplos**: Algunos ejemplos más de orientación son:

* Cree un modelo de etiquetas que incluya:
   * solo las etiquetas relacionadas con los modelos de automóvil.
   * sólo las etiquetas relacionadas con los colores de las camisas.
   * sólo las etiquetas relacionadas con las chaquetas para hombres y mujeres.
* No crear,
   * modelo de etiquetas que incluye modelos de automóvil publicados en 2019 y 2020.
   * varios modelos de etiquetas que incluyen los mismos modelos de automóvil.

**Imágenes utilizadas para entrenar**: Puede utilizar las mismas imágenes para entrenar distintos modelos de etiquetas. Sin embargo, no asocia una imagen con más de una etiqueta en un modelo de etiquetas. Por lo tanto, es posible etiquetar la misma imagen con etiquetas diferentes que pertenecen a modelos de etiquetas diferentes.

No se puede deshacer la formación. Las directrices anteriores le ayudarán a elegir buenas imágenes para entrenar.

## Capacite el modelo para sus etiquetas personalizadas {#train-model}

Para crear y capacitar un modelo para las etiquetas específicas de su empresa, siga estos pasos:

1. Cree las etiquetas necesarias y la estructura de etiquetas adecuada. Cargue las imágenes relevantes en el repositorio de DAM.
1. En [!DNL Experience Manager] la interfaz de usuario, acceda a **[!UICONTROL Recursos]** > Formación en etiquetas **[!UICONTROL inteligentes]**.
1. Haga clic en **[!UICONTROL Crear]**. Proporcione un **[!UICONTROL Título]**, **[!UICONTROL Descripción]**.
1. Busque y seleccione las etiquetas de las etiquetas existentes en las `cq:tags` que desea preparar el modelo. Haga clic en **[!UICONTROL Siguiente]**. 
1. En el cuadro de diálogo **[!UICONTROL Seleccionar recursos]** , haga clic en **[!UICONTROL Añadir recursos]** con cada etiqueta. Busque en el repositorio DAM o navegue hasta el repositorio para seleccionar al menos 10 y 50 imágenes. Seleccione los recursos y no la carpeta. Una vez que haya seleccionado las imágenes, haga clic en **[!UICONTROL Seleccionar]**.
1. Para previsualización de las miniaturas de las imágenes seleccionadas, haga clic en el acordeón delante de una etiqueta. Puede modificar la selección haciendo clic en **[!UICONTROL Añadir recursos]**. Cuando esté satisfecho con la selección, haga clic en **[!UICONTROL Enviar]**. La interfaz de usuario muestra una notificación en la parte inferior de la página que indica que se ha iniciado la formación.
1. Compruebe el estado de la formación en la columna **[!UICONTROL Estado]** de cada modelo de etiquetas. Los estados posibles son [!UICONTROL Pendiente], [!UICONTROL Entrenado]y [!UICONTROL Fallido].

![Flujo de trabajo para entrenar el modelo de etiquetado para etiquetado inteligente](assets/smart-tag-model-training-flow.png)

*Figura: Pasos del flujo de trabajo de formación para enseñar el modelo de etiquetado.*

### Informe y estado de la formación de vista {#training-status}

Para comprobar si el servicio Etiquetas inteligentes ha recibido formación sobre sus etiquetas en el conjunto de recursos de formación, consulte el informe del flujo de trabajo de formación desde la consola Informes.

1. En [!DNL Experience Manager] la interfaz, vaya a **[!UICONTROL Herramientas > Recursos > Informes]**.
1. In the **[!UICONTROL Asset Reports]** page, click **[!UICONTROL Create]**.
1. Select the **[!UICONTROL Smart Tags Training]** report, and then click **[!UICONTROL Next]** from the toolbar.
1. Especifique un título y una descripción para el informe. En **[!UICONTROL Programar informe]**, deje seleccionada la opción **[!UICONTROL Ahora]**. Si desea programar el informe para más adelante, seleccione **[!UICONTROL Más adelante]** e indique una fecha y una hora. Then, click **[!UICONTROL Create]** from the toolbar.
1. En la página **[!UICONTROL Informes de recursos]**, seleccione el informe que ha generado. To view the report, click **[!UICONTROL View]** from the toolbar.
1. Revise los detalles del informe. El informe muestra el estado de la formación de las etiquetas que ha entrenado. The green color in the **[!UICONTROL Training Status]** column indicates that the Smart Tags service is trained for the tag. El color amarillo indica que el servicio no está completamente entrenado para una etiqueta en particular. En este caso, agregue más imágenes con la etiqueta en concreto y ejecute el flujo de trabajo de formación para que el servicio se imparta completamente en la etiqueta. Si no ve las etiquetas en este informe, vuelva a ejecutar el flujo de trabajo de formación para estas etiquetas.Etiquetas
1. Para descargar el informe, selecciónelo en la lista y haga clic en **[!UICONTROL Descargar]** en la barra de herramientas. El informe se descarga como una hoja de cálculo de Microsoft Excel.

## Etiquetado de recursos {#tag-assets}

Una vez que haya formado el servicio Etiquetas inteligentes, puede activar el flujo de trabajo de etiquetado para aplicar automáticamente las etiquetas adecuadas a un conjunto diferente de recursos similares. Puede aplicar el flujo de trabajo de etiquetado de forma periódica o siempre que sea necesario. El flujo de trabajo de etiquetado se aplica tanto a los recursos como a las carpetas.

### Etiquetado de recursos desde la consola de flujo de trabajo {#tagging-assets-from-the-workflow-console}

1. En la interfaz de Experience Manager, vaya a **[!UICONTROL Herramientas > Flujo de trabajo > Modelos]**.
1. From the **[!UICONTROL Workflow Models]** page, select the **[!UICONTROL DAM Smart Tags Assets]** workflow and then click **[!UICONTROL Start Workflow]** from the toolbar.

   ![dam_smart_tag_workflow](assets/dam_smart_tag_workflow.png)

1. En el cuadro de diálogo **[!UICONTROL Ejecutar flujo de trabajo]** , vaya a la carpeta de carga útil que contiene los recursos en los que desea aplicar las etiquetas automáticamente.
1. Especifique un título para el flujo de trabajo y un comentario opcional. Haga clic en **[!UICONTROL Ejecutar]**.

   ![tagging_dialog](assets/tagging_dialog.png)

   Vaya a la carpeta de recursos y revise las etiquetas para comprobar si los recursos están etiquetados correctamente. Para obtener más información, consulte [Gestión de etiquetas](#manage-smart-tags-and-searches)inteligentes.

### Etiquetar recursos de la línea de tiempo {#tagging-assets-from-the-timeline}

1. En la interfaz de usuario de Recursos, seleccione la carpeta que contenga recursos o recursos específicos a los que desee aplicar etiquetas inteligentes.
1. En la esquina superior izquierda, abra la **[!UICONTROL línea de tiempo]**.
1. Abra acciones desde la parte inferior de la barra lateral izquierda y haga clic en Flujo de trabajo **[!UICONTROL de Inicio]**.

   ![inicio_workflow](assets/start_workflow.png)

1. Seleccione el flujo de trabajo Recursos **[!UICONTROL de etiquetas inteligentes]** DAM y especifique un título para el flujo de trabajo.
1. Haga clic en **[!UICONTROL Inicio]**. El flujo de trabajo aplica las etiquetas a los recursos. Vaya a la carpeta de recursos y revise las etiquetas para comprobar si los recursos están etiquetados correctamente. Para obtener más información, consulte [Gestión de etiquetas](#manage-smart-tags-and-searches)inteligentes.

>[!NOTE]
>
>En los ciclos de etiquetado posteriores, solo los recursos modificados se etiquetan de nuevo con etiquetas recién formadas.Sin embargo, incluso los recursos sin modificar se etiquetan si el espacio entre los últimos y los actuales ciclos de etiquetado del flujo de trabajo de etiquetado supera las 24 horas. Para los flujos de trabajo de etiquetado periódicos, los recursos sin modificar se etiquetan cuando el lapso de tiempo supera los 6 meses.

### Etiquetado de recursos cargados {#tag-uploaded-assets}

El Experience Manager puede etiquetar automáticamente los recursos que los usuarios cargan en DAM. Para ello, los administradores configuran un flujo de trabajo para agregar un paso disponible de a los recursos de etiquetas inteligentes. Consulte [cómo habilitar el etiquetado inteligente para los recursos](/help/assets/smart-tags-configuration.md#enable-smart-tagging-for-uploaded-assets)cargados.

## Administrar etiquetas inteligentes y búsquedas de imágenes {#manage-smart-tags-and-searches}

Puede depurar las etiquetas inteligentes para eliminar cualquier etiqueta incorrecta que se haya asignado a las imágenes de su marca, de modo que solo se muestren las etiquetas más relevantes.

La moderación de las etiquetas inteligentes también ayuda a restringir las búsquedas de imágenes basadas en etiquetas, ya que garantiza que la imagen aparezca en los resultados de búsqueda de las etiquetas más relevantes. Básicamente, ayuda a eliminar las posibilidades de que las imágenes no relacionadas aparezcan en los resultados de búsqueda.

También puede asignar una clasificación superior a una etiqueta para aumentar su relevancia con respecto a una imagen. La promoción de una etiqueta para una imagen aumenta las posibilidades de que la imagen aparezca en los resultados de búsqueda cuando se realiza una búsqueda en función de la etiqueta en particular.

1. En el cuadro Omniture, busque recursos basados en una etiqueta.
1. Inspect muestra los resultados de la búsqueda para identificar una imagen que no le parece relevante para la búsqueda.
1. Seleccione la imagen y, a continuación, haga clic en el icono **[!UICONTROL Administrar etiquetas]** de la barra de herramientas.
1. En la página **[!UICONTROL Administrar etiquetas]** , inspeccione las etiquetas. Si no desea que la imagen se busque en función de una etiqueta específica, seleccione la etiqueta y haga clic en el icono Eliminar de la barra de herramientas. También puede hacer clic en `X` símbolo que aparece junto a la etiqueta.
1. Para asignar una clasificación superior a una etiqueta, selecciónela y haga clic en el icono de promoción de la barra de herramientas. La etiqueta promocionada se mueve a la sección **[!UICONTROL Etiquetas]** .
1. Click **[!UICONTROL Save]**, and then click **[!UICONTROL OK]** to close the Success dialog.
1. Vaya a la página de propiedades de la imagen. Observe que la etiqueta promocionada tiene una alta relevancia y, por lo tanto, aparece más arriba en los resultados de búsqueda.

### Comprender AEM resultados de búsqueda con etiquetas inteligentes {#understandsearch}

De forma predeterminada, AEM búsqueda combina los términos de búsqueda con una `AND` cláusula. El uso de etiquetas inteligentes no cambia este comportamiento predeterminado. El uso de etiquetas inteligentes agrega una `OR` cláusula adicional para encontrar cualquiera de los términos de búsqueda en las etiquetas inteligentes de aplicación. For example, consider searching for `woman running`. Los recursos con solo `woman` o solamente `running` palabra clave en los metadatos no aparecen en los resultados de búsqueda de forma predeterminada. Sin embargo, en una consulta de búsqueda de este tipo aparece un recurso etiquetado con etiquetas inteligentes `woman` o con `running` etiquetas inteligentes. Los resultados de la búsqueda son una combinación de:

* recursos con `woman` y `running` palabras clave en los metadatos.

* los recursos se etiquetaron de forma inteligente con cualquiera de las palabras clave.

Los resultados de búsqueda que coinciden con todos los términos de búsqueda en los campos de metadatos se muestran primero, seguidos de los resultados de búsqueda que coinciden con cualquiera de los términos de búsqueda en las etiquetas inteligentes. En el ejemplo anterior, el orden aproximado de visualización de los resultados de búsqueda es:

1. coincidencias de en `woman running` los distintos campos de metadatos.
1. coincidencias de `woman running` en etiquetas inteligentes.
1. coincidencias de `woman` o de `running` en etiquetas inteligentes.

### Limitaciones de etiquetado {#limitations}

Las etiquetas inteligentes mejoradas se basan en modelos de aprendizaje de imágenes de marca y sus etiquetas. Estos modelos no siempre son perfectos para identificar etiquetas. La versión actual de Etiquetas inteligentes tiene las siguientes limitaciones:

* Incapacidad para reconocer diferencias sutiles en las imágenes. Por ejemplo, camisas delgadas contra las tradicionales.
* Imposibilidad de identificar etiquetas basadas en pequeños patrones o partes de una imagen. Por ejemplo, logotipos en camisetas.
* El etiquetado se admite en las configuraciones regionales en las que se AEM. Para obtener una lista de idiomas, consulte las notas de la versión de las etiquetas [inteligentes](https://docs.adobe.com/content/help/en/experience-manager-64/release-notes/smart-content-service-release-notes.html).

Para buscar recursos con etiquetas inteligentes (normal o mejorada), utilice la búsqueda de recursos Omniture (búsqueda de texto completo). No hay ningún predicado de búsqueda independiente para las etiquetas inteligentes.

>[!NOTE]
>
>La capacidad de las etiquetas inteligentes para formarse en las etiquetas y aplicarlas en otras imágenes depende de la calidad de las imágenes que se utilicen para la formación.
>Para obtener los mejores resultados, Adobe recomienda que utilice imágenes visualmente similares para entrenar el servicio de cada etiqueta.

>[!MORELIKETHIS]
>
>* [Configurar Experience Manager para etiquetado inteligente](smart-tags-configuration.md)
>* [Comprender cómo las etiquetas inteligentes ayudan a administrar recursos](https://medium.com/adobetech/efficient-asset-management-with-enhanced-smart-tags-887bd47dbb3f)

