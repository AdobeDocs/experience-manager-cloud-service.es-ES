---
title: Acerca de los perfiles de imagen y de vídeo de Dynamic Media
description: Un perfil de imagen o un perfil de vídeo es una fórmula para definir qué opciones aplicar a los recursos que se cargan en una carpeta. Por ejemplo, puede especificar qué codificación de vídeo aplicar a los recursos de vídeo de Dynamic Media que carga. O bien, qué perfil de imagen aplicar a los recursos de imagen de Dynamic Media para que se recorten correctamente.
contentOwner: Rick Brough
feature: Asset Management,Image Profiles,Video Profiles
role: Admin,User
exl-id: 8c8f0a57-13f5-4903-8d76-bfb6ee83323c
source-git-commit: c82f84fe99d8a196adebe504fef78ed8f0b747a9
workflow-type: tm+mt
source-wordcount: '1437'
ht-degree: 1%

---

# Acerca de los perfiles de imagen y de vídeo de Dynamic Media{#about-dm-image-video-profiles}

<table>
    <tr>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nuevo</i></sup> <a href="/help/assets/dynamic-media/dm-prime-ultimate.md"><b>Dynamic Media Prime y Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nuevo</i></sup> <a href="/help/assets/assets-ultimate-overview.md"><b>AEM Assets Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nueva</i></sup> integración de <a href="/help/assets/integrate-aem-assets-edge-delivery-services.md"><b>AEM Assets con Edge Delivery Services</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nueva</i></sup> <a href="/help/assets/aem-assets-view-ui-extensibility.md"><b>extensibilidad de la interfaz de usuario</b></a>
        </td>
          <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nuevo</i></sup> <a href="/help/assets/dynamic-media/enable-dynamic-media-prime-and-ultimate.md"><b>Habilitar Dynamic Media Prime y Ultimate</b></a>
        </td>
    </tr>
    <tr>
        <td>
            <a href="/help/assets/search-best-practices.md"><b>Prácticas recomendadas de búsqueda</b></a>
        </td>
        <td>
            <a href="/help/assets/metadata-best-practices.md"><b>Prácticas recomendadas de metadatos</b></a>
        </td>
        <td>
            <a href="/help/assets/product-overview.md"><b>Centro de contenido</b></a>
        </td>
        <td>
            <a href="/help/assets/dynamic-media-open-apis-overview.md"><b>Dynamic Media con funciones de OpenAPI</b></a>
        </td>
        <td>
            <a href="https://developer.adobe.com/experience-cloud/experience-manager-apis/"><b>Documentación de desarrollador de AEM Assets</b></a>
        </td>
    </tr>
</table>

Un perfil de imagen o un perfil de vídeo es una fórmula para definir qué opciones aplicar a los recursos que se cargan en una carpeta. Por ejemplo, puede especificar qué codificación de vídeo aplicar a los recursos de vídeo de Dynamic Media que carga. O bien, qué perfil de imagen aplicar a los recursos de imagen de Dynamic Media para que se recorten correctamente.

En Dynamic Media, puede crear dos tipos de perfiles, que se tratan en detalle en los siguientes vínculos:

* [Perfiles de imagen de Dynamic Media](/help/assets/dynamic-media/image-profiles.md)
* [Perfiles de vídeo de Dynamic Media](/help/assets/dynamic-media/video-profiles.md)

Consulte también [Perfiles de metadatos](/help/assets/metadata-profiles.md).

Debe tener derechos de administrador para crear, editar y eliminar perfiles de imagen de Dynamic Media o perfiles de vídeo de Dynamic Media.

Después de crear el perfil de imagen o el perfil de vídeo, debe asignarlos a una o varias carpetas que utilice para los recursos de Dynamic Media recién cargados.

Consulte también [Prácticas recomendadas para organizar su Assets digital con el fin de usar perfiles de procesamiento](/help/assets/organize-assets.md).


>[!NOTE]
>
>Assets que se mueve de una carpeta a otra no se vuelve a procesar. Por ejemplo, supongamos que tiene la carpeta 1 con el perfil A asignado y la carpeta 2 con el perfil B asignado. Si mueve recursos de la carpeta 1 a la carpeta 2, los recursos movidos conservarán su procesamiento original de la carpeta 1.
>
>Lo mismo ocurre incluso cuando se mueven recursos entre dos carpetas que tienen asignado el mismo perfil.

## Reprocesar recursos de Dynamic Media en una carpeta {#reprocessing-assets}

Puede volver a procesar los recursos en una carpeta que ya tenga un perfil de imagen de Dynamic Media existente o un perfil de vídeo de Dynamic Media que haya cambiado posteriormente.

Por ejemplo, supongamos que ha creado un perfil de imagen de Dynamic Media y lo ha asignado a una carpeta. A todos los recursos de imagen que haya cargado en la carpeta se les había aplicado automáticamente el perfil de imagen. Sin embargo, más adelante decide añadir una nueva proporción de recorte inteligente al perfil de imagen. Ahora, en lugar de tener que seleccionar y volver a cargar los recursos en la carpeta de nuevo, simplemente ejecuta el flujo de trabajo *Reprocesamiento de Dynamic Media*.

Puede ejecutar el flujo de trabajo de reprocesamiento en un recurso en el que se haya producido un error de procesamiento por primera vez. Aunque no haya editado un perfil de imagen o de vídeo, o ya haya aplicado un perfil de imagen o de vídeo, puede ejecutar el flujo de trabajo de reprocesamiento en una carpeta de recursos en cualquier momento.

Si lo desea, puede ajustar el tamaño del lote del flujo de trabajo de reprocesamiento desde un valor predeterminado de 50 hasta 1000 recursos. Cuando ejecuta el flujo de trabajo _Reprocesamiento de Dynamic Media_ en una carpeta, los recursos se agrupan en lotes y luego se envían al servidor de Dynamic Media para su procesamiento. Después del procesamiento, los metadatos de cada recurso en todo el conjunto de lotes se actualizaron el [!DNL Adobe Experience Manager]. Si el tamaño del lote es grande, puede experimentar un retraso en el procesamiento. O bien, si el tamaño del lote es demasiado pequeño, puede causar demasiados viajes de ida y vuelta al servidor de Dynamic Media.

Consulte [Ajustar el tamaño del lote del flujo de trabajo de nuevo procesamiento](#adjusting-load).

>[!NOTE]
>
>Si está realizando una migración masiva de recursos de Dynamic Media Classic a [!DNL Experience Manager], habilite el agente de replicación de migración en el servidor de Dynamic Media. Cuando finalice la migración, asegúrese de desactivar el agente.
>
>El agente de publicación de migración debe estar desactivado en el servidor de Dynamic Media para que el flujo de trabajo de reprocesamiento funcione según lo esperado.

<!-- LEAVE IN PLACE, MAY BE USED IN THE FUTURE

Batch size is the number of assets that are amalgamated into a single IPS (Dynamic Media's Image Production System) job. When you run the Dynamic Media Reprocess workflow, the job is triggered on IPS. The number of IPS jobs that are triggered is based on the total number of assets in the folder, divided by the batch size. For example, suppose you had a folder with 150 assets and a batch size of 50. In this case, three IPS jobs are triggered. The assets are updated when the entire batch size (50 in our example) is processed in IPS. The job then moves onto the next IPS job and so on until complete. If you increase the batch size, you may notice a longer delay with assets getting updated. 

-->

**Para volver a procesar los recursos de Dynamic Media en una carpeta:**

1. En [!DNL Experience Manager], desde la página de Assets, vaya a una carpeta de recursos que tenga un perfil de imagen o de vídeo asignado y para el que desee aplicar el flujo de trabajo **Reprocesamiento de Dynamic Media**.

   Las carpetas que tienen asignado un perfil de imagen o de vídeo tienen el nombre del perfil directamente debajo del nombre de la carpeta en la vista de tarjeta.

1. Seleccione una carpeta.

   * El flujo de trabajo considera recursivamente todos los archivos de la carpeta seleccionada.
   * Si hay una o más subcarpetas con recursos en la carpeta principal seleccionada, el flujo de trabajo vuelve a procesar cada recurso en la jerarquía de carpetas.
   * Como práctica recomendada, evite ejecutar este flujo de trabajo en una jerarquía de carpetas que tenga más de 1000 recursos.

1. Cerca de la esquina superior izquierda de la página, en la lista desplegable, seleccione **[!UICONTROL Cronología]**.
1. Cerca de la esquina inferior izquierda de la página, a la derecha del campo [!UICONTROL Comentario], seleccione el icono en forma de quilate ( **^** ).

   ![Captura de pantalla de Assets en Experience Manager que muestra una carpeta seleccionada de recursos, la lista desplegable Cronología resaltada, el botón Iniciar flujo de trabajo resaltado y el icono en forma de carro a la derecha del campo Comentario también resaltado](/help/assets/dynamic-media/assets/reprocess-assets1.png).

1. Seleccione **[!UICONTROL Iniciar flujo de trabajo]**.
1. En la lista desplegable **[!UICONTROL Iniciar flujo de trabajo]**, elija **[!UICONTROL Reprocesar Dynamic Media]**.
1. (Opcional) En el campo de texto **Escriba el título del flujo de trabajo**, escriba un nombre para el flujo de trabajo. Puede utilizar el nombre para hacer referencia a la instancia de flujo de trabajo, si es necesario.

   ![Captura de pantalla de la interfaz de usuario de la cronología con la opción &quot;Reprocesamiento de Dynamic Media&quot; seleccionada en la lista desplegable Iniciar flujo de trabajo y el botón Inicio resaltado](/help/assets/dynamic-media/assets/reprocess-assets2.png).

1. Seleccione **[!UICONTROL Iniciar]** y luego seleccione **[!UICONTROL Confirmar]**.

   Para supervisar el flujo de trabajo o comprobar su progreso, en la página de la consola principal de [!DNL Experience Manager], seleccione **[!UICONTROL Herramientas > Flujo de trabajo]**. En la página Instancias de flujo de trabajo, seleccione un flujo de trabajo. En la barra de menús, seleccione **[!UICONTROL Abrir historial]**. También puede finalizar, suspender o cambiar el nombre de un flujo de trabajo seleccionado desde la misma página Instancias de flujo de trabajo.

### Ajuste el tamaño del lote del flujo de trabajo de nuevo procesamiento (opcional) {#adjusting-load}

(Opcional) El tamaño de lote predeterminado en el flujo de trabajo de reprocesamiento es de 50 recursos por trabajo. Este tamaño de lote óptimo está regido por el tamaño promedio del recurso y los tipos MIME de los recursos en los que se ejecuta el reprocesamiento. Un valor mayor significa que tiene muchos archivos en un solo trabajo de reprocesamiento. Por lo tanto, el banner de procesamiento permanece en [!DNL Experience Manager] recursos durante más tiempo. Sin embargo, si el tamaño medio del archivo es pequeño (1 MB o menos), Adobe recomienda aumentar el valor a varios 100, pero nunca más de un 1000. Si el tamaño medio del archivo es de cientos de megabytes, Adobe recomienda reducir el tamaño del lote hasta 10.

**Para ajustar opcionalmente el tamaño del lote del flujo de trabajo de reprocesamiento:**

1. En [!DNL Experience Manager], seleccione **[!UICONTROL Adobe Experience Manager]** para acceder a la consola de navegación global y, a continuación, seleccione el icono **[!UICONTROL Herramientas]** (martillo) > **[!UICONTROL Flujo de trabajo > Modelos]**.
1. En la página Modelos de flujo de trabajo, en Vista de tarjeta o Vista de lista, seleccione **[!UICONTROL Reprocesar Dynamic Media]**.

   ![Captura de pantalla de la página Modelos de flujo de trabajo con el flujo de trabajo &quot;Reprocesamiento de Dynamic Media&quot; seleccionado en la vista de tarjeta de Experience Manager](/help/assets/dynamic-media/assets/reprocess-assets7.png).

1. En la barra de herramientas, seleccione **[!UICONTROL Editar]**. Una nueva pestaña del explorador abre la página del modelo de flujo de trabajo Reprocesamiento de Dynamic Media.
1. En la página Flujo de trabajo de reprocesamiento de Dynamic Media, cerca de la esquina superior derecha, seleccione **[!UICONTROL Editar]** para &quot;desbloquear&quot; el flujo de trabajo.
1. En el flujo de trabajo, seleccione el componente Carga por lotes de Scene7 para abrir la barra de herramientas y, a continuación, seleccione **[!UICONTROL Configurar]** en la barra de herramientas.

   ![Captura de pantalla del componente &quot;Carga en lote de Scene7&quot; en la página &quot;Reprocesamiento de Dynamic Media&quot; con el puntero del ratón pasando el ratón sobre el icono &quot;Configurar&quot;](/help/assets/dynamic-media/assets/reprocess-assets8.png).

1. En el cuadro de diálogo **[!UICONTROL Cargar lotes en Scene7—Propiedades de la etapa]**, establezca lo siguiente:
   * En los campos de texto **[!UICONTROL Título]** y **[!UICONTROL Descripción]**, escriba un nuevo título y una descripción para el trabajo, si lo desea.
   * Seleccione **[!UICONTROL Avance de controlador]** si su controlador avanzará al siguiente paso.
   * En el campo **[!UICONTROL Tiempo de espera]**, introduzca el tiempo de espera del proceso externo (segundos).
   * En el campo **[!UICONTROL Periodo]**, introduzca un intervalo de sondeo (segundos) para comprobar la finalización del proceso externo.
   * En el campo **[!UICONTROL Lote]**, introduzca el número máximo de recursos (50-1000) que se procesarán en un trabajo de carga por lotes del servidor de Dynamic Media.
   * Seleccione **[!UICONTROL Avanzar en el tiempo de espera]** si desea avanzar cuando se alcance el tiempo de espera. Anule la selección si desea continuar en la bandeja de entrada cuando se alcance el tiempo de espera.

   ![Captura de pantalla de la página &quot;Carga por lotes en Scene7 - Propiedades del paso&quot;](/help/assets/dynamic-media/assets/reprocess-assets3.png).

1. En la esquina superior derecha del cuadro de diálogo **[!UICONTROL Cargar lotes a Scene7 - Propiedades del paso]**, seleccione **[!UICONTROL Listo]**.

1. En la esquina superior derecha de la página Modelo de flujo de trabajo de reprocesamiento de Dynamic Media, seleccione **[!UICONTROL Sincronizar]**. Cuando vea **[!UICONTROL Sincronizado]**, el modelo de tiempo de ejecución del flujo de trabajo se sincronizará correctamente y estará listo para volver a procesar los recursos de una carpeta.

   ![Captura de pantalla de Assets en Experience Manager que muestra una carpeta seleccionada de recursos, la lista desplegable Cronología resaltada, el botón Iniciar flujo de trabajo resaltado y el icono en forma de carro a la derecha del campo Comentario también resaltado](/help/assets/dynamic-media/assets/reprocess-assets1.png).

1. Cierre la pestaña del explorador que muestra el modelo de flujo de trabajo de reprocesamiento de Dynamic Media.

<!-- MAY BE NEEDED IN THE FUTURE

1. Return to the browser tab that has the open Workflow Models page, then press **Esc** to exit the selection.
1. In the upper-left corner of the page, select **[!UICONTROL Adobe Experience Manager]** to access the global navigation console, then select the **[!UICONTROL Tools]** (hammer) icon > **[!UICONTROL General > CRXDE Lite]**.
1. In the folder tree on the left side of the CRXDE Lite page, navigate to the following location:

   `/conf/global/settings/workflow/models/scene7_reprocess_assets/jcr:content/flow/reprocess/metaData`

   ![CRXDE Lite](/help/security/assets/workflow-models9.png)

1. On the right side of the CRXDE Lite page, in the lower portion, enter the following name, type, and value in its respective field:
    * **[!UICONTROL Name]**: `reprocess-batch-size`
    * **[!UICONTROL Type]**: `Long`
    * **[!UICONTROL Value]**: enter a default value (50-1000) for the batch size
1. In the lower-right corner, select **[!UICONTROL Add]**. The new property appears as the following:

    ![Saving the new property](/help/security/assets/workflow-models10.png)

1. On the menu bar of the CRXDE Lite page, select **[!UICONTROL Save All]**.
1. In the upper-left corner of the page, select **[!UICONTROL CRXDE Lite]** to return to the main Experience Manager console
1. Repeat steps 1-7 to re-synchronize the new batch size to the Dynamic Media Reprocess workflow model.

-->
