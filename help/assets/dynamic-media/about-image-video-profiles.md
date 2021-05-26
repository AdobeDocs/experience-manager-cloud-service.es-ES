---
title: Acerca de los perfiles de imagen de Dynamic Media y los perfiles de vídeo
description: Un perfil de imagen o un perfil de vídeo es una fórmula para las opciones que se aplican a los recursos que se cargan en una carpeta. Por ejemplo, puede especificar la codificación de vídeo que se aplicará a los recursos de vídeo de Dynamic Media que cargue. O bien, qué perfil de imagen aplicar a los recursos de imagen de Dynamic Media para recortarlos correctamente.
feature: Administración de recursos,Perfiles de imagen,Perfiles de vídeo
role: Administrator,Business Practitioner
exl-id: 8c8f0a57-13f5-4903-8d76-bfb6ee83323c
source-git-commit: fdfcaf7ba99ec54e1bdf1c97764da8c766701498
workflow-type: tm+mt
source-wordcount: '1269'
ht-degree: 1%

---

# Acerca de los perfiles de imagen de Dynamic Media y los perfiles de vídeo{#about-dm-image-video-profiles}

Un perfil de imagen o un perfil de vídeo es una fórmula para las opciones que se aplican a los recursos que se cargan en una carpeta. Por ejemplo, puede especificar la codificación de vídeo que se aplicará a los recursos de vídeo de Dynamic Media que cargue. O bien, qué perfil de imagen aplicar a los recursos de imagen de Dynamic Media para recortarlos correctamente.

En Dynamic Media, puede crear dos tipos de perfiles, que se describen detalladamente en los siguientes vínculos:

* [Perfiles de imagen de Dynamic Media](/help/assets/dynamic-media/image-profiles.md)
* [Perfiles de vídeo de Dynamic Media](/help/assets/dynamic-media/video-profiles.md)

Consulte también [Perfiles de metadatos](/help/assets/metadata-profiles.md).

Debe tener derechos de administrador para crear, editar y eliminar Perfiles de imagen de Dynamic Media o Perfiles de vídeo de Dynamic Media.

Después de crear el perfil de imagen o el perfil de vídeo, debe asignarlo a una o varias carpetas que utilice para los recursos de Dynamic Media recién cargados.

Consulte también [Prácticas recomendadas para organizar los recursos digitales con el fin de utilizar perfiles de imagen o perfiles de vídeo](/help/assets/dynamic-media/best-practices-for-file-management.md).

>[!NOTE]
>
>Los recursos que se mueven de una carpeta a otra no se vuelven a procesar. Por ejemplo, supongamos que tiene la Carpeta 1 con el perfil A asignado y la Carpeta 2 con el perfil B asignado. Si mueve recursos de la carpeta 1 a la carpeta 2, los recursos movidos conservarán su procesamiento original de la carpeta 1.
>
>Lo mismo ocurre incluso cuando se mueven recursos entre dos carpetas que tienen el mismo perfil asignado.

## Reprocesamiento de recursos de Dynamic Media en una carpeta {#reprocessing-assets}

Puede volver a procesar los recursos en una carpeta que ya tenga un perfil de imagen de Dynamic Media o un perfil de vídeo de Dynamic Media que haya cambiado posteriormente.

Por ejemplo, supongamos que ha creado un perfil de imagen de Dynamic Media y lo ha asignado a una carpeta. Los recursos de imagen que haya cargado en la carpeta de forma automática tenían el perfil de imagen aplicado a los recursos. Sin embargo, más tarde, decide agregar una nueva proporción de recorte inteligente al Perfil de imagen. Ahora, en lugar de tener que seleccionar y volver a cargar los recursos en la carpeta de nuevo, simplemente ejecute el *Scene7: Volver a procesar el flujo de trabajo de Assets*.

Puede ejecutar el flujo de trabajo de reprocesamiento en un recurso cuyo procesamiento haya fallado por primera vez. Aunque no haya editado un perfil de imagen o un perfil de vídeo, o bien ya haya aplicado un perfil de imagen o un perfil de vídeo, puede ejecutar el flujo de trabajo de reprocesamiento en una carpeta de recursos en cualquier momento.

Si lo desea, puede ajustar el tamaño del lote del flujo de trabajo de reprocesamiento de un valor predeterminado de 50 recursos hasta 1000. Al ejecutar el _Scene7: Reprocesar el flujo de trabajo de Assets_ en una carpeta, los recursos se agrupan en lotes y se envían al servidor de Dynamic Media para su procesamiento. Después del procesamiento, los metadatos de cada recurso en todo el conjunto de lotes se actualizan en [!DNL Adobe Experience Manager]. Si el tamaño del lote es grande, puede experimentar un retraso en el procesamiento. O, si el tamaño del lote es demasiado pequeño, puede causar demasiados viajes de ida y vuelta al servidor de Dynamic Media.

Consulte [Ajuste del tamaño del lote del flujo de trabajo de reprocesamiento](#adjusting-load).

>[!NOTE]
>
>Si está realizando una migración masiva de recursos de Dynamic Media Classic a [!DNL Experience Manager], habilite el agente de replicación de migración en el servidor de Dynamic Media. Una vez completada la migración, asegúrese de desactivar el agente.
>
>El agente de publicación de migración debe estar deshabilitado en el servidor de Dynamic Media para que el flujo de trabajo de reprocesamiento funcione según lo esperado.

<!-- LEAVE IN PLACE, MAY BE USED IN THE FUTURE

Batch size is the number of assets that are amalgamated into a single IPS (Dynamic Media’s Image Production System) job. When you run the Scene7: Reprocess Assets workflow, the job is triggered on IPS. The number of IPS jobs that are triggered is based on the total number of assets in the folder, divided by the batch size. For example, suppose you had a folder with 150 assets and a batch size of 50. In this case, three IPS jobs are triggered. The assets are updated when the entire batch size (50 in our example) is processed in IPS. The job then moves onto the next IPS job and so on until complete. If you increase the batch size, you may notice a longer delay with assets getting updated. 

-->

**Para volver a procesar los recursos de Dynamic Media en una carpeta:**
1. En [!DNL Experience Manager], en la página Recursos, vaya a la carpeta Recursos que tenga un perfil de imagen o un perfil de vídeo asignado y para la que desee aplicar el **Scene7: Volver a procesar el flujo de trabajo de Asset**.

   Las carpetas que tienen asignado un perfil de imagen o un perfil de vídeo tienen el nombre del perfil directamente debajo del nombre de la carpeta en la vista de tarjeta.

1. Seleccione una carpeta.

   * El flujo de trabajo tiene en cuenta todos los archivos de la carpeta seleccionada de forma recursiva.
   * Si hay una o más subcarpetas con recursos en la carpeta principal seleccionada, el flujo de trabajo vuelve a procesar cada recurso en la jerarquía de carpetas.
   * Como práctica recomendada, evite ejecutar este flujo de trabajo en una jerarquía de carpetas que tenga más de 1000 activos.

1. Cerca de la esquina superior izquierda de la página, en la lista desplegable, haga clic en **[!UICONTROL Cronología]**.
1. Cerca de la esquina inferior izquierda de la página, a la derecha del campo [!UICONTROL Comment], pulse el icono del carro ( **^** ) .

   ![Flujo de trabajo de reprocesamiento de recursos 1](/help/assets/dynamic-media/assets/reprocess-assets1.png)

1. Haga clic en **[!UICONTROL Iniciar flujo de trabajo]**.
1. En la lista desplegable **[!UICONTROL Iniciar flujo de trabajo]**, elija **[!UICONTROL Scene7: Volver a procesar los recursos]**.
1. (Opcional) En el campo de texto **Enter title of workflow** introduzca un nombre para el flujo de trabajo. Puede utilizar el nombre para hacer referencia a la instancia de flujo de trabajo, si es necesario.

   ![Volver a procesar los recursos 2](/help/assets/dynamic-media/assets/reprocess-assets2.png)

1. Haga clic en **[!UICONTROL Start]** y, a continuación, haga clic en **[!UICONTROL Confirm]**.

   Para monitorizar el flujo de trabajo o comprobar su progreso, en la página de la consola principal [!DNL Experience Manager], haga clic en **[!UICONTROL Tools > Workflow]**. En la página Instancias de flujo de trabajo , seleccione un flujo de trabajo. En la barra de menús, haga clic en **[!UICONTROL Abrir historial]**. También puede finalizar, suspender o cambiar el nombre de un flujo de trabajo seleccionado desde la misma página Instancias de flujo de trabajo .

### Ajuste del tamaño del lote del flujo de trabajo de reprocesamiento {#adjusting-load}

(Opcional) El tamaño predeterminado del lote en el flujo de trabajo de reprocesamiento es de 50 activos por trabajo. Este tamaño de lote óptimo se rige por el tamaño medio del recurso y los tipos MIME de los recursos en los que se ejecuta el reprocesamiento. Un valor superior significa que tiene muchos archivos en un solo trabajo de reprocesamiento. Por lo tanto, el banner de procesamiento permanece en activos [!DNL Experience Manager] durante más tiempo. Sin embargo, si el tamaño promedio del archivo es pequeño-1 MB o menor de Adobe, se recomienda aumentar el valor a varios 100, pero nunca más de 1000. Si el tamaño medio de archivo es de cientos de megabytes, Adobe recomienda reducir el tamaño del lote hasta 10.

**Para ajustar opcionalmente el tamaño del lote del flujo de trabajo de reprocesamiento:**

1. En [!DNL Experience Manager], pulse **[!UICONTROL Adobe Experience Manager]** para acceder a la consola de navegación global y, a continuación, pulse el icono **[!UICONTROL Herramientas]** (martillo) > **[!UICONTROL Flujo de trabajo > Modelos]**.
1. En la página Modelos de flujo de trabajo , en Vista de tarjeta o Vista de lista, seleccione **[!UICONTROL Scene7: Volver a procesar los recursos]**.

   ![Página Modelos de flujo de trabajo con Scene7: Flujo de trabajo de reprocesamiento de recursos seleccionado en Vista de tarjeta](/help/assets/dynamic-media/assets/reprocess-assets7.png)

1. En la barra de herramientas, haga clic en **[!UICONTROL Editar]**. Una nueva pestaña del explorador abre Scene7: Volver a procesar la página del modelo de flujo de trabajo de Assets.
1. En Scene7: Vuelva a procesar la página de flujo de trabajo de Assets, cerca de la esquina superior derecha, pulse **[!UICONTROL Editar]** para &quot;desbloquear&quot; el flujo de trabajo.
1. En el flujo de trabajo, seleccione el componente Carga por lotes de Scene7 para abrir la barra de herramientas y, a continuación, pulse **[!UICONTROL Configurar]** en la barra de herramientas.

   ![Componente Carga por lotes de Scene7](/help/assets/dynamic-media/assets/reprocess-assets8.png)

1. En el cuadro de diálogo **[!UICONTROL Carga por lotes a Scene7—Propiedades de los pasos]**, configure lo siguiente:
   * En los campos de texto **[!UICONTROL Title]** y **[!UICONTROL Description]**, introduzca un nuevo título y una descripción para el trabajo, si lo desea.
   * Seleccione **[!UICONTROL Avance del controlador]** si el controlador va a avanzar al siguiente paso.
   * En el campo **[!UICONTROL Timeout]**, introduzca el tiempo de espera del proceso externo (segundos).
   * En el campo **[!UICONTROL Period]**, introduzca un intervalo de sondeo (segundos) para probar la finalización del proceso externo.
   * En el **[!UICONTROL Batch field]**, introduzca el número máximo de activos (50-1000) que se procesarán en un trabajo de carga por lotes del servidor de Dynamic Media.
   * Seleccione **[!UICONTROL Avanzar en el tiempo de espera]** si desea avanzar cuando se alcance el tiempo de espera. Anule la selección si desea continuar con la bandeja de entrada cuando se alcance el tiempo de espera.

   ![Cuadro de diálogo Propiedades](/help/assets/dynamic-media/assets/reprocess-assets3.png)

1. En la esquina superior derecha del cuadro de diálogo **[!UICONTROL Carga por lotes a Scene7 - Propiedades por pasos]**, pulse **[!UICONTROL Listo]**.

1. En la esquina superior derecha de Scene7: Vuelva a procesar la página del modelo de flujo de trabajo de Assets, pulse **[!UICONTROL Sincronizar]**. Cuando ve **[!UICONTROL Sincronizado]**, el modelo de tiempo de ejecución del flujo de trabajo se sincroniza correctamente y está listo para volver a procesar los recursos en una carpeta.

   ![Sincronización del modelo de flujo de trabajo](/help/assets/dynamic-media/assets/reprocess-assets1.png)

1. Cierre la ficha del explorador que muestra el Scene7: Reprocesar el modelo de flujo de trabajo de Assets.

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
1. In the upper-left corner of the page, tap **[!UICONTROL CRXDE Lite]** to return to the main Experience Manager console
1. Repeat steps 1-7 to re-synchronize the new batch size to the Scene7: Reprocess Assets workflow model.

-->
