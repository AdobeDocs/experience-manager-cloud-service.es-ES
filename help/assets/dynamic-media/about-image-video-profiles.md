---
title: Acerca de los Perfiles de imagen y los Perfiles de vídeo de Dynamic Media
description: Un Perfil de imagen o un Perfil de vídeo es una fórmula para determinar las opciones que se aplican a los recursos que se cargan en una carpeta. Por ejemplo, puede especificar qué codificación de vídeo se aplicará a los recursos de vídeo de Dynamic Media que cargue. O bien, qué Perfil de imagen aplicar a los recursos de imagen de Dynamic Media para que se recorten correctamente.
translation-type: tm+mt
source-git-commit: 68cf71054b1cd7dfb2790122ba4c29854ffdf703
workflow-type: tm+mt
source-wordcount: '1296'
ht-degree: 2%

---


# Acerca de los Perfiles de imagen y los Perfiles de vídeo de Dynamic Media{#about-dm-image-video-profiles}

Un Perfil de imagen o un Perfil de vídeo es una fórmula para determinar las opciones que se aplican a los recursos que se cargan en una carpeta. Por ejemplo, puede especificar qué codificación de vídeo se aplicará a los recursos de vídeo de Dynamic Media que cargue. O bien, qué Perfil de imagen aplicar a los recursos de imagen de Dynamic Media para que se recorten correctamente.

En Dynamic Media, puede crear dos tipos de perfiles, que se tratan en detalle en los siguientes vínculos:

* [perfiles de imagen de Dynamic Media](/help/assets/dynamic-media/image-profiles.md)
* [perfiles de vídeo de Dynamic Media](/help/assets/dynamic-media/video-profiles.md)

Consulte también perfiles [de metadatos](/help/assets/metadata-profiles.md).

Debe tener derechos de administrador para crear, editar y eliminar Perfiles de imagen de Dynamic Media o Perfiles de vídeo de Dynamic Media.

Después de crear el Perfil de imágenes o el Perfil de vídeo, se asigna a una o varias carpetas que se utilizan como destino para los recursos de Dynamic Media que se acaban de cargar.

Consulte también [Prácticas recomendadas para organizar los recursos digitales con el fin de utilizar Perfiles de imagen o Perfiles](/help/assets/dynamic-media/best-practices-for-file-management.md)de vídeo.

>[!NOTE]
>
>Los recursos que se mueven de una carpeta a otra no se vuelven a procesar. Por ejemplo, supongamos que tiene la carpeta 1 con el perfil A asignado y la carpeta 2 con el perfil B asignado. Si mueve recursos de la carpeta 1 a la carpeta 2, los recursos movidos conservarán su procesamiento original desde la carpeta 1.
>
>Lo mismo sucede incluso cuando se mueven recursos entre dos carpetas que tienen el mismo perfil asignado.

## Reprocesamiento de recursos de Dynamic Media en una carpeta {#reprocessing-assets}

Puede volver a procesar los recursos en una carpeta que ya tenga un Perfil de imágenes de Dynamic Media o un Perfil de vídeo de Dynamic Media que haya cambiado posteriormente.

Por ejemplo, supongamos que ha creado un Perfil de imagen de Dynamic Media y lo ha asignado a una carpeta. Los recursos de imagen que haya cargado en la carpeta se aplicarán automáticamente al Perfil de imagen. Sin embargo, posteriormente se decide añadir una nueva proporción de recorte inteligente al Perfil de imágenes. Ahora, en lugar de volver a seleccionar y cargar los recursos en la carpeta, solo tiene que ejecutar *Scene7: Flujo de trabajo de reprocesamiento de recursos* .

Puede ejecutar el flujo de trabajo de reprocesamiento en un recurso cuyo procesamiento haya fallado por primera vez. Por lo tanto, aunque no haya editado un Perfil de imagen o un perfil de vídeo, o haya aplicado ya un Perfil de imagen o un Perfil de vídeo, podrá seguir ejecutando el flujo de trabajo de reprocesamiento en una carpeta de recursos en cualquier momento.

Opcionalmente, puede ajustar el tamaño del lote del flujo de trabajo de reprocesamiento de un valor predeterminado de 50 recursos a 1000. Al ejecutar _Scene7: Volver a procesar el flujo de trabajo de recursos_ en una carpeta, los recursos se agrupan en lotes y se envían al servidor de Dynamic Media para su procesamiento. Tras el procesamiento, los metadatos de cada recurso en todo el conjunto de lotes se actualizan en AEM. Si el tamaño del lote es muy grande, puede experimentar un retraso en el procesamiento. O bien, si el tamaño del lote es demasiado pequeño, puede causar demasiados viajes de ida y vuelta al servidor de Dynamic Media.

Consulte [Ajuste del tamaño de lote del flujo de trabajo](#adjusting-load)de reprocesamiento.

>[!NOTE]
>
>Si está realizando una migración masiva de recursos de Dynamic Media Classic a AEM, debe habilitar el agente de replicación de migración en el servidor de Dynamic Media. Una vez completada la migración, asegúrese de desactivar el agente.
El agente de publicación de migración debe estar deshabilitado en el servidor de Dynamic Media para que el flujo de trabajo de reprocesamiento funcione según lo esperado.

<!-- LEAVE IN PLACE, MAY BE USED IN THE FUTURE

Batch size is the number of assets that are amalgamated into a single IPS (Dynamic Media’s Image Production System) job. When you run the Scene7: Reprocess Assets workflow, the job is triggered on IPS. The number of IPS jobs that are triggered is based on the total number of assets in the folder, divided by the batch size. For example, suppose you had a folder with 150 assets and a batch size of 50. In this case, three IPS jobs are triggered. The assets are updated when the entire batch size (50 in our example) is processed in IPS. The job then moves onto the next IPS job and so on until complete. If you increase the batch size, you may notice a longer delay with assets getting updated. 

-->

**Para volver a procesar los recursos de Dynamic Media en una carpeta**:
1. En AEM, en la página Recursos, vaya a la carpeta de recursos de Dynamic Media que tenga un Perfil de imagen o un Perfil de vídeo asignado y para la que desee aplicar **Scene7: Flujo de trabajo de reprocesamiento de recursos** ,

   Las carpetas que ya tienen un Perfil de imagen o un Perfil de vídeo asignado a él se indican mediante la visualización del nombre del perfil directamente debajo del nombre de la carpeta en la Vista de tarjetas.

1. Seleccione una carpeta.

   * El flujo de trabajo tiene en cuenta todos los archivos de la carpeta seleccionada de forma recursiva.
   * Si hay una o varias subcarpetas con recursos en la carpeta principal seleccionada, el flujo de trabajo volverá a procesar todos los recursos en la jerarquía de carpetas.
   * Se recomienda evitar ejecutar este flujo de trabajo en una jerarquía de carpetas con más de 1000 recursos.

1. Cerca de la esquina superior izquierda de la página, en la lista desplegable, haga clic en **[!UICONTROL Cronología]**.
1. Cerca de la esquina inferior izquierda de la página, a la derecha del campo Comentario, haga clic en el icono de carro ( **^** ) .

   ![Flujo de trabajo de reprocesamiento de recursos 1](/help/assets/dynamic-media/assets/reprocess-assets1.png)

1. Haga clic en Flujo de trabajo **[!UICONTROL de Inicio]**.
1. En la lista desplegable Flujo de trabajo **[!UICONTROL de]** Inicio, elija **[!UICONTROL Scene7: Volver a procesar los recursos]**.
1. (Opcional) En el campo **Introduzca el título del texto del flujo de trabajo** , introduzca un nombre para el flujo de trabajo. Puede utilizar el nombre para hacer referencia a la instancia de flujo de trabajo, si es necesario.

   ![Volver a procesar los recursos 2](/help/assets/dynamic-media/assets/reprocess-assets2.png)

1. Haga clic en **[!UICONTROL Inicio]** y, a continuación, en **[!UICONTROL Confirmar]**.

   Para supervisar el flujo de trabajo o comprobar su progreso, en la página de la consola principal de AEM, haga clic en **[!UICONTROL Herramientas > Flujo de trabajo]**. En la página Instancias de flujo de trabajo, seleccione un flujo de trabajo. En la barra de menús, haga clic en **[!UICONTROL Abrir historial]**. También puede finalizar, suspender o cambiar el nombre de un flujo de trabajo seleccionado desde la misma página Instancias de flujo de trabajo.

### Ajuste del tamaño del lote del flujo de trabajo de reprocesamiento {#adjusting-load}

(Opcional) El tamaño de lote predeterminado en el flujo de trabajo de reprocesamiento es de 50 recursos por trabajo. Este tamaño óptimo de lote se rige por el tamaño medio del recurso y los tipos mínimos de recursos en los que se ejecuta el reprocesamiento. Un valor más alto significa que tendrá muchos archivos en un solo trabajo de reprocesamiento. En consecuencia, la pancarta de procesamiento permanece en los recursos de AEM durante más tiempo. Sin embargo, si el tamaño medio del archivo es pequeño (1 MB o menos), Adobe recomienda aumentar el valor a varios cientos, pero nunca más de 1000. Si el tamaño medio de archivo es de cientos de megabytes, Adobe recomienda reducir el tamaño del lote hasta 10.

**Ajuste opcional del tamaño del lote del flujo de trabajo de reprocesamiento**

1. En Experience Manager, pulse **[!UICONTROL Adobe Experience Manager]** para acceder a la consola de navegación global y, a continuación, pulse el icono **[!UICONTROL Herramientas]** (martillo) > **[!UICONTROL Flujo de trabajo > Modelos]**.
1. En la página Modelos de flujo de trabajo, en Vista de tarjetas o Vista de Listas, seleccione **[!UICONTROL Scene7: Volver a procesar los recursos]**.

   ![Página Modelos de flujo de trabajo con Scene7: Volver a procesar los recursos seleccionados en la Vista de tarjetas](/help/assets/dynamic-media/assets/reprocess-assets7.png)

1. En la barra de herramientas, haga clic en **[!UICONTROL Editar]**. Una nueva ficha de explorador abre Scene7: Volver a procesar la página del modelo de flujo de trabajo de Recursos.
1. En Scene7: Volver a procesar la página de flujo de trabajo Recursos, cerca de la esquina superior derecha, toque **[!UICONTROL Editar]** para &quot;desbloquear&quot; el flujo de trabajo.
1. En el flujo de trabajo, seleccione el componente Carga por lotes de Scene7 para abrir la barra de herramientas y, a continuación, toque **[!UICONTROL Configurar]** en la barra de herramientas.

   ![Componente de carga por lotes de Scene7](/help/assets/dynamic-media/assets/reprocess-assets8.png)

1. En el cuadro de diálogo Cargar **[!UICONTROL por lotes a Scene7: Propiedades]** de los pasos, establezca lo siguiente:
   * In the **[!UICONTROL Title]** and **[!UICONTROL Description]** text fields, enter a new title and description for the job, if desired.
   * Seleccione **[!UICONTROL Handler Advance]** si su controlador avanzará al paso siguiente.
   * En el campo **[!UICONTROL Tiempo de espera]** , introduzca el tiempo de espera del proceso externo (segundos).
   * En el campo **[!UICONTROL Período]** , introduzca un intervalo de sondeo (segundos) para comprobar si se ha completado el proceso externo.
   * In the **[!UICONTROL Batch field]**, enter the maximum number of assets (50-1000) to process in a Dynamic Media server batch processing upload job.
   * Seleccione **[!UICONTROL Avanzar al tiempo de espera]** si desea avanzar cuando se alcance el tiempo de espera. Anule la selección si desea continuar con la bandeja de entrada cuando se alcance el tiempo de espera.

   ![Cuadro de diálogo Propiedades](/help/assets/dynamic-media/assets/reprocess-assets3.png)

1. En la esquina superior derecha del cuadro de diálogo Propiedades **[!UICONTROL de la etapa de carga por]** lotes en Scene7, toque **[!UICONTROL Listo]**.

1. En la esquina superior derecha de Scene7: Volver a procesar la página del modelo de flujo de trabajo de Recursos, toque **[!UICONTROL Sincronizar]**. Cuando se ve **[!UICONTROL Sincronizado]**, el modelo de tiempo de ejecución de flujo de trabajo se sincroniza correctamente y está listo para volver a procesar los recursos en una carpeta.

   ![Sincronización del modelo de flujo de trabajo](/help/assets/dynamic-media/assets/reprocess-assets1.png)

1. Cierre la ficha del explorador que muestra Scene7: Volver a procesar el modelo de flujo de trabajo de Recursos.

<!-- MAY BE NEEDED IN THE FUTURE

1. Return to the browser tab that has the open Workflow Models page, then press **Esc** to exit the selection.
1. In the upper-left corner of the page, tap **[!UICONTROL Adobe Experience Manager]** to access the global navigation console, then tap the **[!UICONTROL Tools]** (hammer) icon > **[!UICONTROL General > CRXDE Lite]**.
1. In the folder tree on the left side of the CRXDE Lite page, navigate to the following location:

   `/conf/global/settings/workflow/models/scene7_reprocess_assets/jcr:content/flow/reprocess/metaData`

   ![CRXDE Lite](/help/security/assets/workflow-models9.png)

1. On the right side of the CRXDE Lite page, in the lower portion, enter the following name, type, and value in its respective field:
    * **[!UICONTROL Name]**: `reprocess-batch-size`
    * **[!UICONTROL Type]**: `Long`
    * **[!UICONTROL Value]**: enter a default value (50-1000) for the batch size
1. In the lower-right corner, tap **[!UICONTROL Add]**. The new property appears as the following:

    ![Saving the new property](/help/security/assets/workflow-models10.png)

1. On the menu bar of the CRXDE Lite page, tap **[!UICONTROL Save All]**.
1. In the upper-left corner of the page, tap **[!UICONTROL CRXDE Lite]** to return to the main AEM console
1. Repeat steps 1-7 to re-synchronize the new batch size to the Scene7: Reprocess Assets workflow model.

-->
