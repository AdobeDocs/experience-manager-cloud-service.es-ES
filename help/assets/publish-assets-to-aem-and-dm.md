---
title: Publish AEM rápido para el uso de y Dynamic Media
description: Quick Publish en la vista de Assets AEM le permite publicar recursos en la aplicación y en los medios dinámicos de forma simultánea o independiente. Puede seleccionar recursos y carpetas, y elegir publicar en Dynamic Media AEM o en la carpeta de carpetas de la aplicación de la.
exl-id: 147c1c35-0d81-4458-b4ed-7541d2b0dd54
feature: Publishing, Dynamic Media
role: User
source-git-commit: e3fd0fe2ee5bad2863812ede2a294dd63864f3e2
workflow-type: tm+mt
source-wordcount: '1206'
ht-degree: 1%

---

# Publicación de recursos en AEM y Dynamic Media{#Publish-Assets-to-AEM-and-Dynamic-Media}

| [Prácticas recomendadas de búsqueda](/help/assets/search-best-practices.md) | [Prácticas recomendadas de metadatos](/help/assets/metadata-best-practices.md) | [Centro de contenido](/help/assets/product-overview.md) | [Dynamic Media con funciones OpenAPI](/help/assets/dynamic-media-open-apis-overview.md) | [Documentación para desarrolladores de AEM Assets](https://developer.adobe.com/experience-cloud/experience-manager-apis/) |
| ------------- | --------------------------- |---------|----|-----|

Experience Manager Assets permite publicar recursos rápidamente en Experience Manager y Dynamic Media mediante la vista de Assets. Esto garantiza que administre sus recursos y luego los publique usando la [vista de Assets sin cambiar a la vista de administración](/help/assets/overview.md##persona-based-experiences).

La vista de Experience Manager Assets AEM proporciona la flexibilidad para publicar recursos en o Dynamic Media, o en ambos al mismo tiempo. Puede publicar recursos al cargar, examinar y buscar recursos. Todas estas opciones para publicar recursos se explican en detalle en este artículo.

## Antes de empezar {#before-you-begin}

AEM Configure estas opciones para ver las opciones de publicación de la aplicación para la aplicación y el Dynamic Media de la siguiente manera:

* Para ver las opciones de publicación de Dynamic Media, configure las siguientes opciones con la vista de administrador:

   * [Crear una configuración de nube de Dynamic Media](/help/assets/dynamic-media/config-dm.md#configuring-dynamic-media-cloud-services).
   * Configure el modo Dynamic Media Publish en el nivel de carpeta. También puede establecer estas opciones al crear la configuración de nube de Dynamic Media. Para sobrescribir esa configuración en el nivel de carpeta, consulte [Configuración de Publish selectivo en el nivel de carpeta en Dynamic Media](/help/assets/dynamic-media/selective-publishing.md).

* AEM AEM Para ver las opciones de publicación de los recursos, debe configurar el punto final de publicación de los recursos para su entorno de publicación de la.

## Publish Assets durante la carga {#piblish-assets-during-upload}

AEM Puede publicar recursos en Dynamic Media y al cargarlos en una carpeta. Las opciones de publicación que se muestran dependen del modo de publicación de Dynamic Media establecido en la carpeta en la que se cargan los recursos. El modo de publicación de Dynamic Media se puede establecer en:

* **Tras la activación:** Cuando los recursos se cargan en esta carpeta, debe publicar explícitamente el recurso primero antes de proporcionar un vínculo URL/incrustado.

* **Inmediato:** Cuando los recursos se cargan en esta carpeta, el sistema los incorpora en el Experience Manager y proporciona la dirección URL o incrustación de forma inmediata.
* **Publish selectivo:** Assets se publica a su elección de Experience Manager o de Dynamic Media para su envío en el dominio público.

### El modo Dynamic Media Publish se establece en tras la activación {#dynamic-media-publish-mode-set-to-upon-activation}

Para publicar recursos durante la carga en una carpeta con el modo Dynamic Media Publish establecido en **Tras la activación**:

1. Haga clic en **Agregar Assets** > **Examinar** > **Examinar archivos** para desplazarse a la carpeta adecuada y cargar los recursos. La sección **Opciones de Publish** muestra el **Modo DM Publish** como **Tras la activación**.
   ![Cargar imagen tras la activación](/help/assets/assets/upload-uactivation.svg)
2. Seleccione **Publish AEM para crear la cuenta de usuario y Dynamic Media** y haga clic en **Cargar**. AEM Los recursos se publican en Dynamic Media y en el mismo tiempo para su publicación en el sitio web de la comunidad de recursos Para ver el estado de publicación actualizado de estos recursos, consulte [Comprobar el estado de Publish](#check-publish-status).

### El modo Dynamic Media Publish se ha establecido en Inmediato {#dynamic-media-publish-mode-set-to-immediate}

Para publicar recursos durante la carga en una carpeta con el modo Dynamic Media Publish establecido en **Inmediato**:

1. Haga clic en **Agregar Assets** > **Examinar** > **Examinar archivos** para desplazarse a la carpeta adecuada y cargar los recursos. La sección Opciones de Publish muestra **DM Publish Mode** como **Immediate**.
   ![imagen de carga de archivo - modo inmediato](/help/assets/assets/resized-image-pdf-svg-new.svg)


   Como el modo Dynamic Media Publish es **Inmediato**, los recursos cargados se publican automáticamente en Dynamic Media al hacer clic en **Cargar**.

2. Seleccione Publish AEM AEM para **publicar** los recursos cargados para su publicación y haga clic en Cargar para su publicación en la página de inicio de la página de inicio de la página de inicio de la página de inicio de sesión

   Si selecciona **Publish AEM AEM para la publicación de**, los recursos se publicarán en Dynamic Media y en el servicio de publicación de recursos. En caso contrario, los recursos se publicarán en Dynamic Media.

   Para ver el estado de publicación actualizado de estos recursos, consulte [Comprobar el estado de Publish](#check-publish-status).

### Modo Dynamic Media Publish establecido en Publish selectivo {#dynamic-media-publish-mode-set-to-selective-publish}

Para publicar recursos durante la carga en una carpeta con el modo Dynamic Media Publish establecido en **Publish selectivo**:

1. Haga clic en **Agregar Assets** > **Examinar** > **Examinar archivos** para desplazarse a la carpeta adecuada y cargar los recursos. La sección Opciones de Publish muestra **DM Publish Mode** como **Selective Publish**.
   ![cargar modo de publicación selectivo de imágenes](/help/assets/assets/upload-selective.svg)

2. Seleccione **Publish AEM para la selección de**, **Publish para Dynamic Media** o ambos según sus necesidades y haga clic en **Cargar**.

   AEM Los recursos se publican en Dynamic Media y en el servicio de publicación de recursos en función de su selección.

   Para ver el estado de publicación actualizado de estos recursos, consulte [Comprobar el estado de Publish](#check-publish-status).

## Recursos de Publish mediante la página de exploración de recursos {#publish-assets-using-asset-browse-page}

Para publicar recursos mediante la página de exploración de recursos:

1. Haga clic en **Assets** en la sección **Administración de Assets** disponible en el panel izquierdo.
2. Seleccione los recursos o las carpetas que debe publicar y haga clic en **Publish**.
3. AEM Seleccione **** y haga clic en **Publish AEM** para publicar recursos en Dynamic Media y en el servicio de publicación de recursos de.
   ![examinar recursos](/help/assets/assets/browse-uactivation-immediate.svg)
No puede publicar una carpeta que tenga el modo Dynamic Media Publish establecido en **Publicación selectiva.AEM**: todas las demás carpetas o recursos seleccionados se publican en el sitio de recursos de la red de trabajo de y Dynamic Media AEM después de seleccionar la opción de selección.
   ![examinar recursos](/help/assets/assets/browse-selective123.svg)

## Recursos de Publish mediante la página de resultados de búsqueda {#publish-assets-using-search-results-page}

Para publicar recursos mediante la página de resultados de búsqueda de recursos:

1. Especifique los criterios en la barra de búsqueda y haga clic en el icono Buscar para ver los resultados.
2. Seleccione los recursos que necesita publicar y haga clic en **Publish.**
3. AEM Seleccione la opción, Dynamic Media o ambos según sus necesidades y haga clic en **Publish.**
   ![buscar imagen](/help/assets/assets/search-mode.svg)
La opción para publicar en Dynamic Media en la página de resultados de búsqueda depende del modo de Publish de Dynamic Media establecido en la carpeta en la que el recurso está disponible en el repositorio.

   >[!NOTE]
   >
   >Si selecciona una carpeta y hace clic en **Publish** en la página de resultados de la búsqueda, Experience Manager Assets AEM muestra una opción para publicar recursos en la carpeta y no en Dynamic Media, independientemente de la configuración del modo Publish de Dynamic Media para la carpeta.

## Comprobar estado de Publish {#check-publish-status}

Para comprobar el estado de publicación de un recurso o una carpeta:

1. Haga clic en **[!UICONTROL Assets]** en la sección **[!UICONTROL Administración de Assets]** disponible en el panel izquierdo.
2. Cambie a la vista de lista mediante el conmutador de vistas. AEM Puede ver las propiedades de los recursos, como, por ejemplo, Publish, Dynamic Media Publish, el título, el tamaño, las dimensiones, etc.\
   AEM Si no se publica un recurso o una carpeta, el estado de las columnas **Publish** y **Dynamic Media Publish** se mostrará como **N/A.**
   ![comprobar estado de publicación1](/help/assets/assets/check-publish-status1.png)
AEM Si no puede ver las columnas de Publish y Publish de Dynamic Media en la vista de lista, haga lo siguiente:
   1. AEM Haga clic en ![configuración](/help/assets/assets/settings-icon.svg) y seleccione **columnas de Publish** y **Dynamic Media Publish** en el cuadro de diálogo **Columnas configurables**.
   2. Haga clic en **Confirmar.** Experience Manager Assets agrega las columnas seleccionadas a la vista de lista.

      ![comprobar estado de publicación2](/help/assets/assets/check-publish-status2.png)

También puede comprobar el estado de publicación de un recurso si selecciona un recurso y hace clic en **Detalles.** Los detalles están disponibles en la sección **Publish** disponible en el panel derecho. La sección **Publish** enumera la fecha en la que los recursos se publican en Dynamic Media AEM y en el servicio de recursos de la. Si necesita ver la hora en que se publican los recursos, puede navegar a la vista de lista y ver esos detalles.

![comprobar estado de publicación 3](/help/assets/assets/check-publish-status3.png)

## Limitaciones {#limitations}

AEM Las siguientes funciones están fuera de ámbito por ahora al publicar recursos en y Dynamic Media:

* Recursos de Publish AEM a la página de detalles de Recursos de y Dynamic Media.
* Visualice los puntos finales en los que se publican los recursos mediante el asistente de Quick Publish.
* Agregar o eliminar más recursos en el asistente de Quick Publish.
* Página para ver los recursos publicados.
* Capacidad para copiar o pegar la URL de Dynamic Media en un nivel de recurso (si los recursos se publican en Dynamic Media).
* AEM Capacidad para publicar referencias (recursos, etiquetas, etc.) durante la publicación en el servicio de publicación de recursos de la red de distribución de recursos
* Capacidad para sobrescribir el estado de sincronización de Dynamic Media en el nivel de carpeta.
* Capacidad para sobrescribir el modo Publish de Dynamic Media en el nivel de carpeta
* Administrar publicación aún no es compatible.
