---
title: AEM Publicación rápida en y Dynamic Media
description: AEM La publicación rápida en la vista de recursos permite publicar recursos en y en medios dinámicos de forma simultánea o independiente. Puede seleccionar recursos y carpetas, y elegir publicar en Dynamic Media AEM o en la carpeta de carpetas de la aplicación de la.
exl-id: 147c1c35-0d81-4458-b4ed-7541d2b0dd54
source-git-commit: 8d360b9d3382350c8f78247919c3e3810fe9e58b
workflow-type: tm+mt
source-wordcount: '1188'
ht-degree: 0%

---

# Publicación de recursos en AEM y Dynamic Media{#Publish-Assets-to-AEM-and-Dynamic-Media}

Experience Manager Assets permite publicar recursos rápidamente en Experience Manager y Dynamic Media mediante la vista Recursos. Esto garantiza la administración de los recursos y su posterior publicación mediante [Vista de recursos sin cambiar a la vista de administración](/help/assets/overview.md##persona-based-experiences).

La vista de Experience Manager Assets AEM proporciona la flexibilidad para publicar recursos en o Dynamic Media, o en ambos al mismo tiempo. Puede publicar recursos al cargar, examinar y buscar recursos. Todas estas opciones para publicar recursos se explican en detalle en este artículo.

## Antes de empezar {#before-you-begin}

AEM Configure estas opciones para ver las opciones de publicación de la aplicación para la aplicación y el Dynamic Media de la siguiente manera:

* Para ver las opciones de publicación de Dynamic Media, configure las siguientes opciones con la vista de administrador:

   * [Crear una configuración de nube de Dynamic Media](/help/assets/dynamic-media/config-dm.md#configuring-dynamic-media-cloud-services).
   * Establezca el modo de publicación de Dynamic Media en el nivel de carpeta. También puede establecer estas opciones al crear la configuración de nube de Dynamic Media. Para sobrescribir esta configuración en el nivel de carpeta, consulte [Configuración de la publicación selectiva en el nivel de carpeta en Dynamic Media](/help/assets/dynamic-media/selective-publishing.md).

* AEM AEM Para ver las opciones de publicación de los recursos, debe configurar el punto final de publicación de los recursos para su entorno de publicación de la.

## Publicar recursos durante la carga {#piblish-assets-during-upload}

AEM Puede publicar recursos en Dynamic Media y al cargarlos en una carpeta. Las opciones de publicación que se muestran dependen del modo de publicación de Dynamic Media establecido en la carpeta en la que se cargan los recursos. El modo de publicación de Dynamic Media se puede establecer en:

* **Tras la activación:** Cuando los recursos se cargan en esta carpeta, debe publicarlos explícitamente primero antes de proporcionar un vínculo URL/incrustado.

* **Inmediato:** Cuando los recursos se cargan en esta carpeta, el sistema los incorpora en el Experience Manager y proporciona la URL o la incrustación de forma inmediata.
* **Publicación selectiva:** Los recursos se publican a su elección de Experience Manager o de Dynamic Media para su publicación en el dominio público.

### Modo de publicación de Dynamic Media establecido en Tras la activación {#dynamic-media-publish-mode-set-to-upon-activation}

Para publicar recursos durante la carga en una carpeta con el modo de publicación de Dynamic Media establecido en **Tras la activación**:

1. Clic **Añadir recursos** > **Examinar** > **Examinar archivos** para desplazarse a la carpeta adecuada y cargar recursos. El **Opciones de publicación** muestra la sección **Modo de publicación DM** as **Tras la activación**.
   ![Cargar imagen tras la activación](/help/assets/assets/upload-uactivation.svg)
2. Seleccionar **AEM Publicación en y Dynamic Media** y haga clic en **Cargar**. AEM Los recursos se publican en Dynamic Media y en el mismo tiempo para su publicación en el sitio web de la comunidad de recursos Para ver el estado de publicación actualizado de estos recursos, consulte [Comprobar estado de publicación](#check-publish-status).

### Modo de publicación de Dynamic Media establecido en Inmediato {#dynamic-media-publish-mode-set-to-immediate}

Para publicar recursos durante la carga en una carpeta con el modo de publicación de Dynamic Media establecido en **Inmediato**:

1. Clic **Añadir recursos** > **Examinar** > **Examinar archivos** para desplazarse a la carpeta adecuada y cargar recursos. La sección Opciones de publicación muestra las **Modo de publicación DM** as **Inmediato**.
   ![imagen de carga de archivos: modo inmediato](/help/assets/assets/resized-image-pdf-svg-new.svg)


   Como el modo de publicación de Dynamic Media es **Inmediato**, los recursos cargados se publican automáticamente en Dynamic Media al hacer clic en **Cargar**.

2. Seleccione Publicar en **AEM Publicación de la** AEM Seleccione los recursos cargados que desea cargar y haga clic en Cargar.

   Si selecciona **AEM Publicar en el** AEM , los recursos se publican en Dynamic Media y, de lo contrario, se publican en Dynamic Media.

   Para ver el estado de publicación actualizado de estos recursos, consulte [Comprobar estado de publicación](#check-publish-status).

### Modo de publicación de Dynamic Media establecido en Publicación selectiva {#dynamic-media-publish-mode-set-to-selective-publish}

Para publicar recursos durante la carga en una carpeta con el modo de publicación de Dynamic Media establecido en **Publicación selectiva**:

1. Clic **Añadir recursos** > **Examinar** > **Examinar archivos** para desplazarse a la carpeta adecuada y cargar recursos. La sección Opciones de publicación muestra las **Modo de publicación DM** as **Publicación selectiva**.
   ![cargar modo de publicación selectivo de la imagen](/help/assets/assets/upload-selective.svg)

2. Seleccionar **AEM Publicar en el**, **Publicar en Dynamic Media**, o ambos según sus necesidades y haga clic en **Cargar**.

   AEM Los recursos se publican en Dynamic Media y en el servicio de publicación de recursos en función de su selección.

   Para ver el estado de publicación actualizado de estos recursos, consulte [Comprobar estado de publicación](#check-publish-status).

## Publicar recursos mediante la página de exploración de recursos {#publish-assets-using-asset-browse-page}

Para publicar recursos mediante la página de exploración de recursos:

1. Clic **Assets** en el **Administración de recursos** disponible en el panel izquierdo.
2. Seleccione los recursos o las carpetas que debe publicar y haga clic en **Publish**.
3. Seleccionar **AEM** y haga clic en **Publish** AEM para publicar recursos en y Dynamic Media.
   ![exploración de recursos](/help/assets/assets/browse-uactivation-immediate.svg)
No se puede publicar una carpeta que tenga el modo de publicación de Dynamic Media establecido en **Publicación selectiva.** AEM Todas las demás carpetas o recursos seleccionados se publican en el servicio de carpetas y de Dynamic Media AEM después de seleccionar la opción de.
   ![exploración de recursos](/help/assets/assets/browse-selective123.svg)

## Publicar recursos mediante la página de resultados de búsqueda {#publish-assets-using-search-results-page}

Para publicar recursos mediante la página de resultados de búsqueda de recursos:

1. Especifique los criterios en la barra de búsqueda y haga clic en el icono Buscar para ver los resultados.
2. Seleccione los recursos que debe publicar y haga clic en **Publicar.**
3. AEM Seleccione, Dynamic Media o ambos según sus necesidades y haga clic en **Publicar.**
   ![buscar imagen](/help/assets/assets/search-mode.svg)
La opción para publicar en Dynamic Media en la página de resultados de búsqueda depende del modo de publicación de Dynamic Media establecido en la carpeta en la que el recurso está disponible en el repositorio.

   >[!NOTE]
   >
   >Si selecciona una carpeta y hace clic en **Publish** en la página de resultados de búsqueda, Experience Manager Assets AEM muestra una opción para publicar recursos en la carpeta y no en Dynamic Media, independientemente de la configuración del modo de publicación de Dynamic Media para la carpeta.

## Comprobar estado de publicación {#check-publish-status}

Para comprobar el estado de publicación de un recurso o una carpeta:

1. Clic **[!UICONTROL Assets]** en el **[!UICONTROL Administración de recursos]** disponible en el panel izquierdo.
2. Cambie a la vista de lista mediante el conmutador de vistas. AEM Puede ver las propiedades de los recursos, como Publicación de recursos, Publicación de Dynamic Media, Título, Tamaño, Dimensiones, etc.\
   Si un recurso o una carpeta no se publican, el estado de **AEM Publicación de** y **Publicación de Dynamic Media** columnas se muestra como **N/D.**
   ![comprobar estado de publicación1](/help/assets/assets/check-publish-status1.png)
AEM Si no puede ver las columnas Publicación de y Publicación de Dynamic Media en la vista de lista:
   1. Clic ![configuración](/help/assets/assets/settings-icon.svg) y seleccione **AEM Publicación de** y **Publicación de Dynamic Media** columnas de la **Columnas configurables** diálogo.
   2. Clic **Confirme.** Experience Manager Assets agrega las columnas seleccionadas a la vista Lista.

      ![comprobar estado de publicación2](/help/assets/assets/check-publish-status2.png)

También puede comprobar el estado de publicación de un recurso si selecciona un recurso y hace clic en **Detalles.** Los detalles están disponibles en la **Publish** disponible en el panel derecho. El **Publish** Esta sección enumera la fecha en la que los recursos se publican en Dynamic Media AEM y en el servicio de publicación de. Si necesita ver la hora en que se publican los recursos, puede navegar a la vista de lista y ver esos detalles.

![comprobar estado de publicación 3](/help/assets/assets/check-publish-status3.png)

## Restricciones {#limitations}

AEM Las siguientes funciones están fuera de ámbito por ahora al publicar recursos en y Dynamic Media:

* AEM Publicar recursos en y Dynamic Media desde la página Detalles del recurso.
* Visualice los puntos finales en los que se publican los recursos mediante el asistente de Publicación rápida.
* Agregar o eliminar más recursos en el Asistente para publicación rápida.
* Página para ver los recursos publicados.
* Capacidad para copiar o pegar la URL de Dynamic Media en un nivel de recurso (si los recursos se publican en Dynamic Media).
* AEM Capacidad para publicar referencias (recursos, etiquetas, etc.) durante la publicación en el servicio de publicación de recursos de la red de distribución de recursos
* Capacidad para sobrescribir el estado de sincronización de Dynamic Media en el nivel de carpeta.
* Capacidad para sobrescribir el modo de publicación de Dynamic Media en el nivel de carpeta
* Administrar publicación aún no es compatible.
