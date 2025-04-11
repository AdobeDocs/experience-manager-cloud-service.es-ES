---
title: Interfaz de usuario [!DNL Assets view]
description: Explicación de la interfaz de usuario de y la navegación en [!DNL Assets view].
role: User
exl-id: 1e71ea7d-fee7-4ed0-bb80-d537b57fc823
feature: Asset Management, Publishing, Collaboration, Asset Processing
source-git-commit: f4d0364439d704d4f5611b5fa2f46428048005b0
workflow-type: tm+mt
source-wordcount: '1026'
ht-degree: 75%

---

# Navegación a archivos y carpetas y visualización de recursos {#view-assets-and-details}

<table>
    <tr>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nuevo</i></sup> <a href="/help/assets/dynamic-media/dm-prime-ultimate.md"><b>Dynamic Media Prime y Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nuevo</i></sup> <a href="/help/assets/assets-ultimate-overview.md"><b>AEM Assets Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nuevo</i></sup> <a href="/help/assets/integrate-aem-assets-edge-delivery-services.md"><b>Integración de AEM Assets con Edge Delivery Services</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>New</i></sup> <a href="/help/assets/aem-assets-view-ui-extensibility.md"><b>Extensibilidad de la IU</b></a>
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

<!-- TBD: Give screenshots of all views with many assets. Zoom out to showcase how the thumbnails/tiles flow on the UI in different views. -->

<!-- TBD: The options in left sidebar may change. Shared with me and Shared by me are missing for now. Update this section as UI is updated. -->

## Comprenda la interfaz de usuario de [!DNL Assets view] {#understand-interface-navigation}

[!DNL Assets view] ofrece una interfaz de usuario intuitiva y fácil de usar. La interfaz limpia hace que los recursos y la información relacionada sean fáciles de encontrar y recordar.

Al iniciar sesión en [!DNL Assets view], verá la siguiente interfaz.

![[!DNL Assets view]Interfaz de usuario](assets/assets-view-interface.png)

**A**: Barra lateral izquierda para examinar el repositorio, y proporciona acceso a algunas opciones más **B**: Mostrar o contraer la barra lateral izquierda para aumentar el área de visualización de recursos **C**: Filtrar resultados de búsqueda **D**: Seleccionar todo el contenido de la carpeta seleccionada **E**: Opciones para ordenar recursos **F**: Cuadro de búsqueda **G**: Cargar o arrastrar y soltar archivos mediante el botón `Add Assets` **H**: Crear una nueva carpeta **I**: Cambiar entre diferentes vistas

<!-- TBD: Need an embedded video here with narration. It has to be hosted on MPC to be embeddable. -->

## Examen y visualización de recursos y carpetas {#browse-repository}

Puede examinar las carpetas desde la interfaz de usuario principal o desde la barra lateral izquierda. Experience Manager Assets muestra vistas previas visuales del contenido de la carpeta en la miniatura de la carpeta al examinar o buscar contenido. Esto mejora la capacidad de detección de recursos disponibles en el repositorio de AEM Assets. Esta miniatura de carpeta le ahorra el tiempo empleado en buscar recursos específicos dentro de una carpeta en el repositorio de AEM Assets.
Al buscar recursos en una carpeta, puede utilizar la interfaz para ver las miniaturas de los recursos y examinar visualmente el repositorio o ver los detalles de los recursos para encontrar rápidamente el que desee. Las opciones disponibles en la barra lateral izquierda son las siguientes:

* [Mi espacio de trabajo](/help/assets/my-workspace-assets-view.md): Assets ahora incluye un espacio de trabajo personalizable que proporciona utilidades para acceder fácilmente a las áreas clave de la interfaz de usuario de Assets y a la información más relevante para usted. Esta página sirve como solución integral para proporcionar información general sobre los elementos de trabajo y un acceso rápido a los flujos de trabajo clave. Un acceso más práctico a estas opciones aumenta su eficacia y velocidad de contenido.
* [Tareas](/help/assets/my-workspace-assets-view.md): Puede ver las tareas asignadas en la pestaña de **Mis tareas**. Por su parte, las tareas que crea puede verse en la pestaña de **Tareas asignadas**. Además, las tareas que complete se encuentran en la ficha **Tareas completadas**.
* [Recursos](/help/assets/manage-organize-assets-view.md): lista de todas las carpetas en una vista de árbol, a las que tiene acceso.
* **Vistos recientemente**: lista de recursos que ha previsualizado recientemente. [!DNL Assets view] muestra solo los recursos que previsualiza. No muestra los recursos por los que pasa de largo al examinar los archivos o carpetas del repositorio.
* [Colecciones](/help/assets/manage-collections-assets-view.md): una colección es un conjunto de recursos, carpetas u otras colecciones dentro de la vista Adobe Experience Manager Assets. Utilice las colecciones para compartir recursos entre los usuarios. A diferencia de las carpetas, una colección puede incluir recursos de distintas ubicaciones. Puede compartir varias colecciones con un usuario. Cada colección contiene referencias a recursos. La integridad referencial de los recursos se mantiene entre colecciones.

* [Perspectivas](/help/assets/manage-reports-assets-view.md#view-live-statistics): En [!DNL Assets view], puede ver perspectivas en tiempo real en su panel. La vista Recursos le permite ver datos en tiempo real de su entorno de la vista Recursos con el tablero de Insights. Puede ver las métricas de eventos en tiempo real durante los últimos 30 días o 12 meses.
* **Papelera**: Enumere los recursos eliminados de la carpeta raíz **[!UICONTROL Assets]**. Puede seleccionar un recurso en la carpeta Papelera para restaurarlo a su ubicación original o eliminarlo permanentemente. Puede especificar una palabra clave o aplicar filtros, como el estado del recurso, tipo de archivo, tipo de MIME, tamaño de imagen, creación del recurso, y las fechas de modificación y caducidad, así como filtrar por los recursos que el usuario actual descarta. También puede aplicar filtros personalizados para buscar los recursos adecuados en la carpeta Papelera. Para obtener más información sobre el uso de filtros estándar y personalizados, consulte cómo [buscar recursos en la vista de Assets](/help/assets/search-assets-view.md).
* **Configuración**: puede configurar varias opciones de la vista de Assets mediante **Configuración**, como formularios de metadatos, informes y administración de taxonomía.

<!-- TBD: Not sure if we want to publish these right now. CC Libs are beta as per Greg.
* **Libraries**: Access to [!DNL Adobe Creative Cloud Team] (CCT) Libraries view. This view is visible only if the user is entitled to CCT Libraries.
-->

<!-- TBD: My Work Space shows task inbox and it is not visible on AEM Cloud Demos as of now. It is the source of truth server hence not documenting My Work Space option for now.
-->

Puede abrir o contraer la barra lateral izquierda para aumentar el área de visualización de recursos disponible.

En [!DNL Assets view], puede ver recursos, carpetas y resultados de búsqueda con cuatro tipos diferentes de diseños.

* ![icono de vista de lista](assets/do-not-localize/list-view.png) [!UICONTROL Vista de lista]
* ![icono de vista de cuadrícula](assets/do-not-localize/grid-view.png) [!UICONTROL Vista de cuadrícula]
* ![icono de vista de galería](assets/do-not-localize/gallery-view.png) [!UICONTROL Vista de galería]
* ![icono de vista de cascada](assets/do-not-localize/waterfall-view.png) [!UICONTROL Vista de cascada]

Para localizar recursos, puede ordenarlos en orden de subida o de bajada de `Name`, `Relevancy`, `Size`, `Modified` y `Created`.

Para desplazarse por una carpeta, haga doble clic en las miniaturas de la carpeta o selecciónela en la barra lateral izquierda. Para ver los detalles de una carpeta, selecciónela y haga clic en Detalles en la barra de herramientas de la parte superior. Para desplazarse hacia arriba y abajo en la jerarquía, utilice la barra lateral izquierda o las rutas de exploración de la parte superior.

![Examen de carpetas](assets/browsing-folders.png)

*Imagen: para examinar la jerarquía, utilice las rutas de exploración en la parte superior o en la barra lateral izquierda.*

## Previsualización de recursos {#preview-assets}

Antes de usar, compartir o descargar un recurso, puede verlo más de cerca. La función de previsualización permite ver no solo las imágenes, sino también algunos otros tipos de recursos admitidos.

Para previsualizar un recurso, selecciónelo y haga clic en el ![icono de detalles](assets/do-not-localize/edit-in-icon.png) de [!UICONTROL Detalles] en la barra de herramientas de la parte superior. No solo puede ver el recurso, sino también ver sus metadatos detallados y realizar otras acciones.

![Previsualización de un recurso](/help/assets/assets/navigate-file-folder-dm.png)

**A**: Regresa a la carpeta actual o al resultado de la búsqueda actual en el repositorio **B**: Nombre y formato del archivo que estás previsualizando **C**: Asignar tareas **D**: Metadatos avanzados **E**: Palabras clave y etiquetas inteligentes **F**: Comentar y anotar **G**: Ver tareas relacionadas con el recurso seleccionado **H**: [Ver y administrar versiones](/help/assets/manage-organize-assets-view.md#versions-of-assets) **I**: Ver representaciones de la imagen **J**: Editar imagen **K**: Ver representaciones de Dynamic Media, incluidas las representaciones de Smart Crop y Dynamic Media con capacidades de OpenAPI. **L**: Metadatos básicos **M**: Metadatos avanzados **N**: Palabras clave y etiquetas inteligentes **O**: Continúe con el recurso anterior o siguiente de la carpeta actual sin volver a la carpeta **P**: Obtenga una vista previa más de cerca. Zoom, pantalla completa y otras opciones.

También puede previsualizar los vídeos.

![Previsualización de vídeo](assets/preview-video.png)

Si previsualiza de forma explícita un recurso, [!DNL Assets view] lo muestra como un recurso visualizado recientemente.

<!-- TBD: Describe the options.

Explicitly previewed assets are displayed as recently viewed assets. Give screenshot of this.
Other use cases after previewing.
-->

## Siguientes pasos {#next-steps}

* Realice comentarios del producto mediante la opción [!UICONTROL Comentarios] disponible en la interfaz de usuario de la vista Recursos

* Proporcione comentarios sobre la documentación usando [!UICONTROL Editar esta página] ![editar la página](assets/do-not-localize/edit-page.png) o [!UICONTROL Registrar una incidencia] ![crear una incidencia de GitHub](assets/do-not-localize/github-issue.png), disponibles en la barra lateral derecha

* Contacto con el [Servicio de atención al cliente](https://experienceleague.adobe.com/es?support-solution=General#support)

>[!MORELIKETHIS]
>
>* [Vea las versiones de un recurso](/help/assets/manage-organize-assets-view.md#view-versions).
