---
title: Publicación rápida en  [!DNL AEM and Dynamic Media]
description: Publicación rápida en [!DNL Assets view] le permite publicar recursos en [!DNL AEM and Dynamic Media] de forma simultánea o por separado. Puede seleccionar recursos y carpetas y optar por publicar en [!DNL Dynamic Media] o [!DNL AEM].
exl-id: 147c1c35-0d81-4458-b4ed-7541d2b0dd54
feature: Publishing, [!DNL Dynamic Media]
role: User
source-git-commit: 32fdbf9b4151c949b307d8bd587ade163682b2e5
workflow-type: tm+mt
source-wordcount: '1053'
ht-degree: 0%

---

# Publicar Assets en [!DNL AEM and Dynamic Media]{#Publish-Assets-to-AEM-and-Dynamic-Media}

[!DNL Experience Manager Assets] le permite publicar recursos rápidamente en [!DNL Experience Manager] y [!DNL Dynamic Media] mediante [!DNL Assets view]. Esto garantiza que administre sus recursos y después los publique usando [[!DNL Assets view] sin cambiar a [!DNL Admin view]](/help/assets/overview.md##persona-based-experiences).

[!DNL Experience Manager Assets view] proporciona la flexibilidad para publicar recursos en [!DNL AEM] o [!DNL Dynamic Media], o en ambos al mismo tiempo. Puede publicar recursos al cargar, examinar y buscar recursos. Todas estas opciones para publicar recursos se explican en detalle en este artículo.

## Antes de empezar {#before-you-begin}

Configure estas opciones para ver las opciones de publicación de [!DNL AEM and Dynamic Media]:

* Para ver las opciones de publicación de [!DNL Dynamic Media], configure las siguientes opciones con la vista Administrador:

   * [Crear una [!DNL Dynamic Media] configuración de nube](/help/assets/dynamic-media/config-dm.md#configuring-dynamic-media-cloud-services).
   * Establezca el modo de publicación [!DNL Dynamic Media] en el nivel de carpeta. También puede establecer esta configuración al crear la configuración de nube de [!DNL Dynamic Media]. Para sobrescribir esa configuración en el nivel de carpeta, vea [Configurar publicación selectiva en el nivel de carpeta en [!DNL Dynamic Media]](/help/assets/dynamic-media/selective-publishing.md).

* Para ver las opciones de publicación de [!DNL AEM], debe configurar el extremo de publicación de [!DNL AEM] para su entorno.

## Publicar Assets durante la carga {#piblish-assets-during-upload}

Puede publicar recursos en [!DNL AEM and Dynamic Media] mientras los carga en una carpeta. Las opciones de publicación que se muestran dependen de la configuración del modo de publicación [!DNL Dynamic Media] de la carpeta en la que se cargan los recursos. El modo de publicación [!DNL Dynamic Media] se puede establecer en:

* **[!UICONTROL Tras la activación]:** Cuando los recursos se cargan en esta carpeta, primero debe publicar explícitamente el recurso antes de proporcionar un vínculo URL/incrustado.

* **[!UICONTROL Inmediato]:** Cuando los recursos se cargan en esta carpeta, el sistema los ingresa en Experience Manager y proporciona la dirección URL o incrustación al instante.
* **[!UICONTROL Publicación selectiva]:** Assets se ha publicado a su elección de [!DNL Experience Manager] o de [!DNL Dynamic Media] para su publicación en el dominio público.

### [!UICONTROL Modo de publicación de medios dinámicos] establecido en [!UICONTROL Tras la activación] {#dynamic-media-publish-mode-set-to-upon-activation}

Para publicar recursos al cargarlos en una carpeta cuyo [!DNL Dynamic Media Publish Mode] está establecido en **[!UICONTROL Tras la activación]**:

1. Haga clic en **[!UICONTROL Agregar Assets]** > **[!UICONTROL Examinar]** > **[!UICONTROL Examinar archivos]** para desplazarse a la carpeta adecuada y cargar los recursos. La sección **[!UICONTROL Opciones de publicación]** muestra el **[!UICONTROL Modo de publicación DM]** como **[!UICONTROL Tras la activación]**.
   ![Cargar imagen tras la activación](/help/assets/assets/upload-uactivation.svg)
2. Seleccione **[!UICONTROL Publicar en AEM y Dynamic Media]** y haga clic en **[!UICONTROL Cargar]**. Los recursos se publican en [!DNL AEM and Dynamic Media] al mismo tiempo. Para ver el estado de publicación actualizado de estos recursos, consulte [Comprobar estado de publicación](#check-publish-status).

### [!UICONTROL Modo de publicación de medios dinámicos] establecido en [!UICONTROL Inmediato] {#dynamic-media-publish-mode-set-to-immediate}

Para publicar recursos al cargarlos en una carpeta cuyo [!UICONTROL Modo de publicación de medios dinámicos] está establecido en **[!UICONTROL Inmediato]**:

1. Haga clic en **[!UICONTROL Agregar Assets]** > **[!UICONTROL Examinar]** > **[!UICONTROL Examinar archivos]** para desplazarse a la carpeta adecuada y cargar los recursos. La sección **[!UICONTROL Opciones de publicación]** muestra el **[!UICONTROL Modo de publicación DM]** como **[!UICONTROL Inmediato]**.
   ![imagen de carga de archivo - modo inmediato](/help/assets/assets/resized-image-pdf-svg-new.svg)
Como el [!UICONTROL Modo de publicación de medios dinámicos] es **[!UICONTROL Inmediato]**, los recursos cargados se publican automáticamente en [!DNL Dynamic Media] al hacer clic en **[!UICONTROL Cargar]**.

2. Seleccione **Publicar en AEM** para publicar los recursos cargados en [!DNL AEM] y haga clic en **[!UICONTROL Cargar]**.

   Si selecciona **Publicar en AEM**, los recursos se publican en [!DNL AEM and Dynamic Media]; de lo contrario, los recursos se publican en [!DNL Dynamic Media].

   Para ver el estado de publicación actualizado de estos recursos, consulte [Comprobar estado de publicación](#check-publish-status).

### [!UICONTROL Modo de publicación de medios dinámicos] establecido en [!UICONTROL Publicación selectiva] {#dynamic-media-publish-mode-set-to-selective-publish}

Para publicar recursos durante la carga en una carpeta con [!UICONTROL Modo de publicación de Dynamic Media] establecido en **[!UICONTROL Publicación selectiva]**:

1. Haga clic en **[!UICONTROL Agregar Assets]** > **[!UICONTROL Examinar]** > **[!UICONTROL Examinar archivos]** para desplazarse a la carpeta adecuada y cargar los recursos. La sección **[!UICONTROL Opciones de publicación]** muestra el **[!UICONTROL Modo de publicación DM]** como **[!UICONTROL Publicación selectiva]**.
   ![cargar modo de publicación selectivo de imágenes](/help/assets/assets/upload-selective.svg)

2. Seleccione **[!UICONTROL Publicar en AEM]**, **[!UICONTROL Publicar en Dynamic Media]** o ambos según sus necesidades y haga clic en **Cargar**.

   Los recursos se publican en [!DNL AEM and Dynamic Media] según su selección.

   Para ver el estado de publicación actualizado de estos recursos, consulte [Comprobar estado de publicación](#check-publish-status).

## Publicar recursos mediante la página de exploración de recursos {#publish-assets-using-asset-browse-page}

Para publicar recursos mediante la página de exploración de recursos:

1. Haga clic en **[!UICONTROL Assets]** en la sección **[!UICONTROL Administración de Assets]** disponible en el panel izquierdo.
2. Seleccione uno o varios recursos o carpetas que necesite publicar y haga clic en **[!UICONTROL Publicar]**.
3. Seleccione **[!UICONTROL AEM]** y haga clic en **[!UICONTROL Publicar]** para publicar los recursos en [!DNL AEM and Dynamic Media].
   ![examinar recursos](/help/assets/assets/browse-uactivation-immediate.svg)
No puede publicar una carpeta que tenga el modo de publicación [!DNL Dynamic Media] establecido en **[!UICONTROL Publicación selectiva]**. Todas las demás carpetas o recursos seleccionados se publican en [!DNL AEM and Dynamic Media] después de seleccionar [!DNL AEM].
   ![examinar recursos](/help/assets/assets/browse-selective123.svg)

## Publicar recursos mediante la página de resultados de búsqueda {#publish-assets-using-search-results-page}

Para publicar recursos mediante la página de resultados de búsqueda de recursos:

1. Especifique los criterios en la barra de búsqueda y haga clic en el icono de búsqueda para ver los resultados.
2. Seleccione los recursos que necesita publicar y haga clic en **[!UICONTROL Publicar].**
3. Seleccione [!DNL AEM, Dynamic Media] o ambos según sus necesidades y haga clic en **[!UICONTROL Publicar]**.
   ![buscar imagen](/help/assets/assets/search-mode.svg)
La opción para publicar en [!DNL Dynamic Media] en la página de resultados de búsqueda depende del modo de publicación de [!DNL Dynamic Media] establecido en la carpeta en la que el recurso está disponible en el repositorio.
   >[!NOTE]
   >
   >Si selecciona una carpeta y hace clic en **[!UICONTROL Publicar]** en la página de resultados de búsqueda, [!DNL Experience Manager Assets] muestra una opción para publicar recursos en [!DNL AEM] y no en [!DNL Dynamic Media], independientemente de la configuración del modo de publicación de [!DNL Dynamic Media] para la carpeta.

## Comprobar estado de publicación {#check-publish-status}

Para comprobar el estado publicado de un recurso o una carpeta:

1. Haga clic en **[!UICONTROL Assets]** en la sección **[!UICONTROL Administración de Assets]** disponible en el panel izquierdo.
2. Cambie a la vista Lista con el conmutador de vistas. Puede ver propiedades de recursos, como [!UICONTROL Publicación de AEM], [!UICONTROL Publicación de Dynamic Media], [!UICONTROL título], [!UICONTROL tamaño], [!UICONTROL dimensiones], etc.\
   Si no se publica un recurso o una carpeta, el estado de las columnas **[!UICONTROL Publicación de AEM]** y **[!UICONTROL Publicación de Dynamic Media]** se mostrará como **[!UICONTROL N/A]**.
   ![comprobar estado de publicación1](/help/assets/assets/check-publish-status1.png)
Si no puede ver las columnas Publicar [!DNL AEM] y Publicar [!DNL Dynamic Media] en la vista de lista:
   1. Haga clic en ![configuración](/help/assets/assets/settings-icon.svg) y seleccione **[!UICONTROL Publicación de AEM]** y **[!UICONTROL Publicación de Dynamic Media]** columnas del cuadro de diálogo **[!UICONTROL Columnas configurables]**.
   2. Haga clic en **[!UICONTROL Confirmar]**. [!DNL Experience Manager Assets] agrega las columnas seleccionadas a la vista de lista.

      ![comprobar estado de publicación2](/help/assets/assets/check-publish-status2.png)

También puede comprobar el estado de publicación de un recurso si selecciona un recurso y hace clic en **[!UICONTROL Detalles]**. Los detalles están disponibles en la sección **[!UICONTROL Publicar]** disponible en el panel derecho. La sección **[!UICONTROL Publicar]** enumera la fecha en la que se publican los recursos en [!DNL Dynamic Media] y [!DNL AEM]. Si necesita ver la hora en que se publican los recursos, puede navegar a la vista de lista y ver esos detalles.

![comprobar estado de publicación 3](/help/assets/assets/check-publish-status3.png)

## Limitaciones {#limitations}

Las siguientes capacidades están fuera de ámbito por ahora al publicar recursos en [!DNL AEM and Dynamic Media]:

* Publicar recursos en [!DNL AEM and Dynamic Media] desde [!DNL Asset details page].
* Visualice los puntos de conexión en los que se publican los recursos mediante el Asistente para publicación rápida.
* Agregue o elimine más recursos en el Asistente para publicación rápida.
* Página para ver los recursos publicados.
* Capacidad para copiar o pegar la dirección URL [!DNL Dynamic Media] en un nivel de recurso (si los recursos están publicados en [!DNL Dynamic Media]).
* Capacidad para publicar referencias (recursos, etiquetas, etc.) durante la publicación en [!DNL AEM].
* Capacidad para sobrescribir el estado de sincronización de [!DNL Dynamic Media] en el nivel de carpeta.
* Capacidad para sobrescribir el modo de publicación [!DNL Dynamic Media] en el nivel de carpeta
* Administrar publicación aún no es compatible.
