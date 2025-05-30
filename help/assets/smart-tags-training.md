---
title: Etiquetado automático de recursos con  [!DNL Adobe Sensei] servicio inteligente
description: Etiquete recursos con un servicio artificialmente inteligente que aplique etiquetas comerciales contextuales y descriptivas.
feature: Smart Tags,Tagging
role: Admin,User
source-git-commit: a579e2e25ecff93f6f1487ec0bcd317df09751cf
workflow-type: tm+mt
source-wordcount: '1510'
ht-degree: 5%

---


# Formación sobre etiquetas inteligentes

La formación sobre etiquetas inteligentes permite entrenar las etiquetas para que pueda especificar los detalles si las etiquetas relevantes no están presentes. Utiliza un marco artificial inteligente de [Adobe Sensei](https://business.adobe.com/why-adobe/experience-cloud-artificial-intelligence.html) para entrenar su algoritmo de reconocimiento de imágenes en la estructura de etiquetas y la taxonomía empresarial. A continuación, esta inteligencia de contenido se utiliza para aplicar las etiquetas relevantes a un conjunto diferente de recursos. [!DNL Experience Manager Assets] aplica automáticamente las etiquetas inteligentes a los recursos cargados, de manera predeterminada.

## Determinación de los requisitos de la formación sobre etiquetas inteligentes {#smart-tag-training-requirement}

La formación sobre etiquetas inteligentes es necesaria en los siguientes casos:

* Para agregar un etiquetador automatizado para guardar las iteraciones de adición de etiquetas cada vez que se carga el mismo recurso.
* Para mejorar la capacidad de los recursos para aplicar las etiquetas relevantes.
* Para aumentar la precisión de las etiquetas que aparecen para un recurso.
* Para agregar etiquetas no disponibles o que faltan.


>[!NOTE]
>
>El aprendizaje de etiquetas inteligentes solo se aplica en un ***tipo de imagen*** de recurso.

## Pasos involucrados en la formación de etiquetas inteligentes

[!DNL Experience Manager] como [!DNL Cloud Service] genera automáticamente las etiquetas inteligentes en los recursos basados en texto y en los vídeos de forma predeterminada. Para formar etiquetas inteligentes en imágenes, complete las siguientes tareas:

* [Comprender los modelos de etiquetas y las directrices](#understand-tag-models-guidelines)
* [Entrenar el modelo](#train-model)
* [Etiquete sus recursos digitales](#tag-assets)
* [Administrar las etiquetas y las búsquedas](#manage-smart-tags-and-searches)

## Comprender los modelos de etiquetas y las directrices {#understand-tag-models-guidelines}

Un modelo de etiqueta es un grupo de etiquetas relacionadas que están asociadas con varios aspectos visuales de las imágenes que se están etiquetando. Las etiquetas se relacionan con los distintos aspectos visuales de las imágenes, de modo que, cuando se aplican, ayudan a buscar tipos específicos de imágenes. Por ejemplo, una colección de zapatos puede tener etiquetas diferentes, pero todas las etiquetas están relacionadas con los zapatos y pueden pertenecer al mismo modelo de etiqueta. Cuando se aplican, las etiquetas ayudan a encontrar diferentes tipos de zapatos, por ejemplo, por diseño o por uso.

Antes de crear un modelo de etiquetas y entrenar el servicio, identifique un conjunto de etiquetas únicas que describan mejor los objetos de las imágenes en el contexto de su negocio. Asegúrese de que los recursos del conjunto depurado confirmen [las directrices de formación](#training-guidelines).

### Directrices de formación {#training-guidelines}

Asegúrese de que las imágenes del conjunto de formación se ajusten a las siguientes directrices:

<table>
   <tr>
      <th> Métrica </th>
      <th> Descripción </th>
   </tr>
   <tr>
      <td> <b>Cantidad y tamaño </b></td>
      <td> Mínimo de 10 y máximo de 50 imágenes por etiqueta. </td>
   </tr>
   <tr>
      <td> <b>Coherencia</b> </td>
      <td> Asegúrese de que las imágenes de una etiqueta sean visualmente similares. Es mejor añadir las etiquetas sobre los mismos aspectos visuales (como el mismo tipo de objetos en una imagen) en un solo modelo de etiquetas. Por ejemplo, no es una buena idea etiquetar todas estas imágenes como <i>my-party</i> (para entrenamiento) porque no son visualmente similares. </td>
   </tr>
   <tr>
      <td colspan="2"> <img src="assets/do-not-localize/coherence.png"><br><i>Figura: Imágenes ilustrativas de coherencia para ejemplificar las directrices de formación</i>
      </td>
   </tr>
   <tr>
      <td> <b>Cobertura</b></td>
      <td> Debe haber suficiente variedad en las imágenes de la formación. La idea es ofrecer algunos ejemplos, pero razonablemente diversos, para que aprenda a centrarse en las cosas correctas. Si aplica la misma etiqueta a imágenes visualmente distintas, incluya al menos cinco ejemplos de cada tipo. Por ejemplo, para la etiqueta <i>model-down-pose</i>, incluya más imágenes de aprendizaje similares a la imagen resaltada a continuación para que el servicio identifique las imágenes similares con mayor precisión durante el etiquetado.</td>
   </tr>
   <tr>
   <td colspan="2"> <img src="assets/do-not-localize/coverage_1.png"><br><i>Figura: Imágenes ilustrativas de Cobertura para ejemplificar las directrices para la formación</i>
   </td>
   </tr>
   <tr>
      <td><b>Distracción/obstrucción</b> </td>
      <td> El servicio se entrena mejor con imágenes que tienen menos distracción (fondos destacados, acompañamientos no relacionados, como objetos/personas con el tema principal). Por ejemplo, para la etiqueta <i>casual-shoe</i>, la segunda imagen no es una buena candidata para entrenamiento. </td>
   </tr>
   <tr>
      <td colspan="2"> <img src="assets/do-not-localize/distraction.png"><br><i>Figura: Imágenes ilustrativas de distracción/obstrucción para ejemplificar las directrices para el entrenamiento</i>
      </td>
   </tr>
   <tr>
      <td> <b>Integridad</b> </td>
      <td> Si una imagen cumple los requisitos para más de una etiqueta, agregue todas las etiquetas aplicables antes de incluir la imagen para formación. Por ejemplo, para las etiquetas, como <i>impermeable</i> y <i>vista del lado del modelo</i>, agregue ambas etiquetas en el recurso que cumple los requisitos antes de incluirlo para formación. </td>
   </tr>
   <tr>
      <td colspan="2"> <img src="assets/do-not-localize/completeness.png"><br><i>Figura: imágenes ilustrativas de integridad para ejemplificar las directrices de formación</i>
      </td>
   </tr>
   <tr>
      <td> <b>Número de etiquetas</b> </td>
      <td> Adobe recomienda entrenar un modelo con al menos dos etiquetas distintas y al menos diez imágenes diferentes para cada etiqueta. En un modelo de etiqueta única, no agregue más de 50 etiquetas. </td>
   </tr>
   <tr>
      <td> <b>Número de ejemplos</b> </td>
      <td> Para cada etiqueta, añada al menos diez ejemplos. Sin embargo, Adobe recomienda unos 30 ejemplos. Se admite un máximo de 50 ejemplos por etiqueta. </td>
   </tr>
   <tr>
      <td> <b>Evitar falsos positivos y conflictos</b> </td>
      <td> Adobe recomienda crear un modelo de etiquetas único para un solo aspecto visual. Estructurar los modelos de etiquetas de forma que se eviten las etiquetas superpuestas entre los modelos. Por ejemplo, no uses etiquetas comunes como <i>zapatillas</i> en dos modelos de etiquetas diferentes llamados <i>zapatos</i> y <i>calzado</i>. El proceso de formación sobrescribe un modelo de etiqueta entrenado con el otro para una palabra clave común. </td>
   </tr>
</table>

**Ejemplos**: Algunos ejemplos más para obtener orientación son:

* Cree un modelo de etiquetas que solo incluya,

   * Las etiquetas relacionadas con los modelos de coche.
   * Las etiquetas relacionadas con chaquetas para adultos y niños.

* No crear,

   * Un modelo de etiquetas que incluye modelos de coches lanzados en 2019 y 2020.
   * Varios modelos de etiquetas que incluyen los mismos pocos modelos de coche.

>[!NOTE]
>
>Puede utilizar las mismas imágenes para entrenar distintos modelos de etiquetas. Sin embargo, no asocie una imagen con más de una etiqueta en un modelo de etiqueta. Es posible etiquetar la misma imagen con diferentes etiquetas que pertenezcan a diferentes modelos de etiquetas.
>&#x200B;>No se puede deshacer la formación. Las directrices anteriores deberían ayudarle a elegir buenas imágenes para entrenar.

## Capacite el modelo para las etiquetas personalizadas {#train-model}

Para crear y entrenar un modelo para las etiquetas específicas de su empresa, siga estos pasos:

1. Cree las etiquetas necesarias y la estructura de etiquetas adecuada. Cargue las imágenes relevantes en el repositorio de DAM.
1. En la interfaz de usuario de [!DNL Experience Manager Cloud Service], acceda a **[!UICONTROL Assets]** > **[!UICONTROL Formación sobre etiquetas inteligentes]**.
1. Haga clic en **[!UICONTROL Crear]**. Proporcione un **[!UICONTROL Título]**, **[!UICONTROL Descripción]**.
1. Haga clic en el icono de la carpeta en el campo **[!UICONTROL Etiquetas]**. Se abre una ventana emergente.
1. Busque o seleccione las etiquetas adecuadas de las etiquetas existentes en `cq-tags` que desee agregar al modelo. Haga clic en **[!UICONTROL Siguiente]**.

   >[!NOTE]
   >
   >Puede ordenar la estructura de las etiquetas en orden ascendente o descendente, en función de **[!UICONTROL Nombre]** (orden alfabético), **[!UICONTROL Creado]** fecha o **[!UICONTROL Modificado]** fecha.


1. En el cuadro de diálogo **[!UICONTROL Seleccionar Assets]**, haga clic en **[!UICONTROL Agregar Assets]** con cada etiqueta. Busque en el repositorio de DAM o examine el repositorio para seleccionar al menos 10 y como máximo 50 imágenes. Seleccione los recursos y no la carpeta. Una vez que haya seleccionado las imágenes, haga clic en **[!UICONTROL Seleccionar]**.

   ![Ver estado de formación](assets/smart-tags-training-status.png)

1. Para obtener una vista previa de las miniaturas de las imágenes seleccionadas, haga clic en el acordeón delante de una etiqueta. Puede modificar su selección haciendo clic en **[!UICONTROL Agregar Assets]**. Cuando esté satisfecho con la selección, haga clic en **[!UICONTROL Enviar]**. La interfaz de usuario muestra una notificación en la parte inferior de la página que indica que se ha iniciado la formación.
1. Compruebe el estado del curso de formación en la columna **[!UICONTROL Estado]** para cada modelo de etiqueta. Los estados posibles son [!UICONTROL Pendiente], [!UICONTROL Entrenado] y [!UICONTROL Fallido].

![Flujo de trabajo para entrenar el modelo de etiquetado para etiquetas inteligentes](assets/smart-tag-model-training-flow.png)

*Figura: Pasos del flujo de trabajo de formación para entrenar el modelo de etiquetado.*

### Ver estado e informe de la formación {#training-status}

Para comprobar si el servicio Etiquetas inteligentes ha recibido formación sobre las etiquetas en el conjunto de recursos de formación, revise el informe del flujo de trabajo de formación desde la consola Informes.

1. En la interfaz de [!DNL Experience Manager Cloud Service], vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Assets]** > **[!UICONTROL Informes]**.
1. En la página **[!UICONTROL Informes de recursos]**, haga clic en **[!UICONTROL Crear]**.
1. Seleccione el informe **[!UICONTROL Formación sobre etiquetas inteligentes]** y, a continuación, haga clic en **[!UICONTROL Siguiente]** en la barra de herramientas.
1. Especifique un título y una descripción para el informe. En **[!UICONTROL Programar informe]**, deje seleccionada la opción **[!UICONTROL Ahora]**. Si desea programar el informe para más adelante, seleccione **[!UICONTROL Más adelante]** e indique una fecha y una hora. A continuación, haga clic en **[!UICONTROL Crear]** en la barra de herramientas.
1. En la página **[!UICONTROL Informes de recursos]**, seleccione el informe que ha generado. Para ver el informe, haz clic en **[!UICONTROL Ver]** en la barra de herramientas.
1. Revise los detalles del informe. El informe muestra el estado de la formación de las etiquetas que ha entrenado. El color verde de la columna **[!UICONTROL Estado de formación]** indica que el servicio Etiquetas inteligentes ha recibido formación para la etiqueta. El color amarillo indica que el servicio está parcialmente entrenado para una etiqueta en particular. Para que el servicio se imparta completamente en una etiqueta, agregue más imágenes con la etiqueta en cuestión y ejecute el flujo de trabajo de formación. Si no ve las etiquetas en este informe, ejecute de nuevo el flujo de trabajo de formación para estas etiquetas. Etiquetas
1. Para descargar el informe, selecciónelo en la lista y haga clic en **[!UICONTROL Descargar]** en la barra de herramientas. El informe se descarga como una hoja de cálculo.

>[!NOTE]
>
>¿Qué sucede si deseo transferir la formación sobre etiquetas inteligentes de una instancia a otra mediante una exportación?
>&#x200B;>No es necesario exportar la formación sobre etiquetas inteligentes si el entorno pertenece a la misma organización de IMS. Se comparte automáticamente. Si el entorno está en varias organizaciones de IMS, no hay forma de compartir o exportar la formación sobre etiquetas inteligentes.

## Limitaciones y prácticas recomendadas relacionadas con las etiquetas inteligentes {#limitations-smart-tags-training}

* Para entrenar el modelo, utilice las imágenes más adecuadas. El curso de formación no se puede revertir o el modelo de formación no se puede eliminar. La precisión del etiquetado depende de la formación actual, por lo que debe hacerlo con cuidado.
* No se puede entrenar el servicio que aplica etiquetas inteligentes a los vídeos que utilizan vídeos específicos. Funciona con la configuración predeterminada [!DNL Adobe Sensei].


>[!NOTE]
>
>La capacidad de las etiquetas inteligentes para aprender sobre sus etiquetas y aplicarlas en otras imágenes depende de la calidad de las imágenes que utilice para la formación.
>&#x200B;>Para obtener los mejores resultados, Adobe recomienda utilizar imágenes visualmente similares para entrenar el servicio para cada etiqueta.
