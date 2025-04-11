---
title: Administración de recursos digitales
description: Mueva, elimine, copie, cambie de nombre, actualice y convierta en versión los recursos en [!DNL Assets view].
role: User, Leader
contentOwner: AG
exl-id: 2459d482-828b-4410-810c-ac55ef0a2119
feature: Asset Management, Publishing, Collaboration, Asset Processing
source-git-commit: b7f8b4886372e2210ca8899260b3eb11b75ee798
workflow-type: tm+mt
source-wordcount: '1734'
ht-degree: 63%

---

# Administración de recursos {#manage-assets}

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

Puede realizar varias tareas de administración de activos digitales (DAM) fácilmente mediante la interfaz de usuario sencilla de usar de [!DNL Assets view]. Una vez añadidos los recursos, puede buscarlos, descargarlos, moverlos, copiarlos, cambiarles el nombre, eliminarlos, actualizarlos y editarlos.

Use [!DNL Assets view] para llevar a cabo las siguientes tareas de administración de recursos. Al seleccionar un recurso, aparecen las siguientes opciones en la barra de herramientas de la parte superior.

![Opciones de la barra de herramientas al seleccionar un recurso](assets/toolbar-image-selected.png)

*Imagen: opciones disponibles en la barra de herramientas de una imagen seleccionada.*

* ![icono de anular selección](assets/do-not-localize/close-icon.png) Anule la selección.

* ![icono de buscar similar](assets/do-not-localize/find-similar.svg) Busque un recurso de imagen similar en la interfaz de usuario de Assets en función de los metadatos y las etiquetas inteligentes.

* ![icono de detalles](assets/do-not-localize/edit-in-icon.png) Haga clic para previsualizar un recurso y ver los metadatos detallados. Al previsualizar, puede ver las versiones y editar una imagen.

* ![icono de descarga](assets/do-not-localize/download-icon.png) Descargue el recurso seleccionado en el sistema de archivos local.

* ![icono de añadir a la colección](assets/do-not-localize/add-collection.svg): añada el recurso seleccionado a una colección.

* ![icono de Fijar recursos](assets/do-not-localize/pin-quick-access.svg): fije un recurso para un acceso más rápido cuando lo necesite más tarde. Todos los elementos fijados se muestran en la sección **Acceso rápido** de Mi espacio de trabajo.

* ![icono de editar en Express](assets/do-not-localize/edit-e.svg) Edite una imagen en el Adobe Express integrado en Adobe Experience Manager Assets.

* ![icono de editar recurso](assets/do-not-localize/edit-e.svg) Edite la imagen con Adobe Express.

* ![icono de compartir vínculo de recurso](assets/do-not-localize/share-link.svg) para un recurso con otros usuarios para que puedan acceder a él y lo descarguen.

* ![icono de eliminación](assets/do-not-localize/delete-icon.png) Elimine el recurso o la carpeta seleccionados.

* ![icono de copia](assets/do-not-localize/copy-icon.png) Copie el archivo o la carpeta seleccionados.

* ![icono de movimiento](assets/do-not-localize/move-icon.png) Mueva el recurso o la carpeta seleccionados a una ubicación diferente en la jerarquía del repositorio.

* ![icono de cambio de nombre](assets/do-not-localize/rename-icon.png) Cambie el nombre del recurso o la carpeta seleccionados. Utilice un nombre único, si no, el cambio de nombre producirá un error con una advertencia. Puede intentarlo de nuevo con un nombre nuevo.
Además, puede hacer clic en el título de un recurso o de una carpeta para cambiarle el nombre. Mencione el nuevo texto en el cuadro de texto **Cambiar nombre de recurso** y haga clic en **Guardar**. Esta funcionalidad está disponible en las vistas Cuadrícula, Galería, Cascada y Lista.

* ![icono de vista de cascada](assets/do-not-localize/waterfall-view.png) [!UICONTROL Vista de cascada].

* ![icono de copiar biblioteca](assets/do-not-localize/copy-icon.png) Añada un recurso a la biblioteca.

* ![icono de asignación de tarea](assets/do-not-localize/review-delegate-icon.png) Asigne tareas a otros usuarios para colaborar en un recurso.

* ![icono de asignar tarea](assets/do-not-localize/watch-asset.svg) Monitorice las operaciones realizadas en un recurso.

Puede ver las mismas opciones en las miniaturas de recursos.

![Opciones en la miniatura de un recurso para administrarlo](assets/options-on-thumbnail.png)

[!DNL Assets view] muestra únicamente las opciones relevantes de la barra de herramientas que dependen del tipo de recurso seleccionado.

![Opciones de la barra de herramientas al seleccionar un recurso](assets/toolbar-folder-selected.png)

*Imagen: opciones disponibles en la barra de herramientas de una carpeta seleccionada.*

![Opciones de la barra de herramientas al seleccionar un recurso](assets/toolbar-pdf-selected.png)

*Imagen: opciones disponibles en la barra de herramientas de un archivo PDF seleccionado.*

## Descarga y distribución de recursos {#download}

Puede seleccionar uno o varios recursos, carpetas o una combinación de ambos y descargar la selección en el sistema de archivos local. Puede editar los recursos y volver a cargarlos o distribuirlos fuera de [!DNL Assets view]. Además, puede [descargar las representaciones](/help/assets/add-delete-assets-view.md#renditions) de un recurso.

## Creación de versiones de recursos {#versions-of-assets}

<!-- 
TBD: query for engineering: How many versions are maintained. What happens when we reach that limit? Are old versions automatically removed? -->

[!DNL Assets view] crea versiones de los recursos cuando se cargan de nuevo y se actualizan o editan. Puede ver el historial de versiones actuales y anteriores, así como restaurar una versión anterior de los recursos como la última versión, que se revierte a una anterior si es necesario. Las versiones de los recursos se crean en los siguientes casos:

* Cargue un nuevo recurso con el mismo nombre de archivo que uno existente y en la misma carpeta que este. [!DNL Assets view] le solicita que sobrescriba el recurso anterior o que guarde el nuevo como una versión. Consulte [Carga de recursos duplicados](/help/assets/add-delete-assets-view.md).

  ![Creación de versiones al cargar](assets/uploads-manage-duplicates.png)

  *Imagen: al cargar un recurso con el mismo nombre que uno existente, puede crear una versión de este.*

* Edite una imagen y haga clic en **[!UICONTROL Guardar como versión]**. Consulte [Edición de imágenes](/help/assets/edit-images-assets-view.md).

  ![Guardar imagen editada como versión](assets/edit-image2.png)

  *Imagen: guardar imagen editada como versión.*

* Abra las versiones de un recurso existente. Haga clic en **[!UICONTROL Nueva versión]** y cargue una versión más reciente del recurso en el repositorio.

  ![Opción para cargar una nueva versión de un recurso desde el historial de versiones](assets/view-asset-versions2.png)

### Visualización y comparación de versiones de un recurso {#view-and-compare-versions}

Cargue una copia duplicada o modificada de un recurso para crear sus versiones. Las versiones le permiten realizar un seguimiento de las modificaciones de un recurso a lo largo del tiempo y revertirlo a una versión anterior si es necesario.

Para ver y comparar versiones:

1. Vaya a la página de detalles del recurso.
1. Haga clic en ![Versiones](/help/assets/assets/Clock.svg) en el panel derecho para mostrar el panel **[!UICONTROL Versiones]**. Las miniaturas del recurso original y sus versiones cargadas se muestran en este panel.
1. Seleccione una versión del panel para previsualizarla en el área de previsualización.
1. Seleccione cualquier versión que no sea la más reciente y haga clic en **[!UICONTROL Crear más reciente]** para establecerla como la más reciente.
1. Arrastre el control deslizante en la previsualización hacia la izquierda y la derecha para ver rápidamente la versión seleccionada de una imagen y su última versión en una sola previsualización. Esto permite comparar rápidamente la versión seleccionada de la imagen con la última versión.

   >[!NOTE]
   >
   > La comparación de versiones solo está habilitada para recursos de imagen.

   ![comparar versiones del recurso](/help/assets/assets/version-compare2.png)

<!-- old content
To view versions, open an asset's preview and click **[!UICONTROL Versions]** ![Versions icon](assets/do-not-localize/versions-clock-icon.png) from the right sidebar. To preview a specific version, select it. To revert to it, click **[!UICONTROL Make Latest]**. 
-->

Seleccione la última versión y haga clic en **[!UICONTROL Nueva versión]** para cargar una copia nueva del recurso desde el sistema de archivos local y crear una versión de recurso.

<!-- old content
You can also create versions from the versions timeline. Select the latest version, click **[!UICONTROL New Version]**, and upload a new copy of the asset from your local file system.

![View versions of an asset](assets/view-asset-versions1.png)

*Figure: View versions of an asset, revert to a previous version, or upload another new version.* 
-->

## Administrar el estado de los activos {#manage-asset-status}

**Permisos necesarios:**  `Can Edit`, `Owner` o permisos de administrador en un recurso.

La vista Assets permite establecer el estado en los recursos disponibles en el repositorio. Establezca un estado de activo para gobernar y administrar mejor el consumo descendente de recursos digitales.

Puede establecer el siguiente estado en los recursos:

* Aprobados

* Rechazado

* Sin estado

### Definir estado del activo {#set-asset-status}

Para establecer el estado del activo:

1. Seleccione el recurso y haga clic en **[!UICONTROL Detalles]** en la barra de herramientas.

1. En la ficha **[!UICONTROL Básico]**, seleccione el estado del recurso en la lista desplegable **[!UICONTROL Estado]**. Los valores posibles incluyen Aprobado, Rechazado y Sin estado (predeterminado).
Si tiene Dynamic Media con capacidades OpenAPI proporcionadas para su entorno, Experience Manager Assets genera una URL pública en cuanto marque el recurso como `Approved`.

   >[!VIDEO](https://video.tv.adobe.com/v/342495)



### Definir destino de aprobación {#set-approval-target}

La vista de Assets le permite publicar recursos aprobados en Dynamic Media con capacidades de OpenAPI, Content Hub o ambas en función del valor establecido en el campo **Destino de aprobación** disponible en la página Detalles del recurso.

Para establecer el objetivo de aprobación:

1. Seleccione el recurso y haga clic en **[!UICONTROL Detalles]** en la barra de herramientas.

1. En la ficha **[!UICONTROL Básico]**, seleccione el estado del recurso en la lista desplegable **[!UICONTROL Estado]**. Los valores posibles incluyen Aprobado, Rechazado y Sin estado (predeterminado).

1. Si selecciona **Aprobado** en el paso 2, seleccione un destino de aprobación. Los valores posibles incluyen Delivery y Content Hub.

   * **Delivery** es la opción predeterminada seleccionada en el menú desplegable y publica el recurso en [Dynamic Media con OpenAPI](/help/assets/dynamic-media-open-apis-overview.md) y [Content Hub](/help/assets/product-overview.md), si ambos están habilitados para Experience Manager Assets.

   * Al seleccionar **Content Hub**, se publica el recurso en Content Hub. Content Hub solo se muestra como opción si está habilitado para Experience Manager Assets.

   * Si no selecciona una opción en la lista desplegable, la opción predeterminada habilitada para su entorno de AEM as a Cloud Service se aplica automáticamente al recurso.


   Para obtener más información sobre las opciones disponibles, consulte [Destino de aprobación predeterminado y destinos de publicación para recursos aprobados](#default-approval-target-options-publish-destinations).

   >[!NOTE]
   >
   >La configuración de un objetivo de aprobación es una función de disponibilidad limitada. Puede activarlo o desactivarlo creando un ticket de asistencia. Si tiene Dynamic Media con OpenAPI habilitado, está habilitado de forma predeterminada.

   ![Estado de aprobación](/help/assets/assets/approval-status-delivery.png)

1. Especifique otras propiedades del recurso y haga clic en **[!UICONTROL Guardar]**.

Otros puntos que hay que tener en cuenta son:

* Si no usa el formulario de metadatos predeterminado y no puede ver el campo **[!UICONTROL Destino de aprobación]**, [edite el formulario de metadatos](/help/assets/metadata-assets-view.md#metadata-forms) para arrastrar el campo **[!UICONTROL Aprobación para]** desde los componentes disponibles hasta el formulario de metadatos y haga clic en **[!UICONTROL Guardar]**.

* Al seleccionar el destino de aprobación como `Content Hub` mediante la vista de Assets, los recursos se ponen a disposición de los usuarios de Content Hub que forman parte de la misma organización.

#### Destinos de aprobación predeterminados y destinos de publicación para recursos aprobados {#default-approval-target-options-publish-destinations}

La siguiente tabla ilustra los requisitos previos para la visualización de la lista desplegable `Approval Target` y el objetivo de aprobación predeterminado en función de la habilitación de DM con OpenAPI y Content Hub en el entorno de AEM as a Cloud Service:

| Dynamic Media con OpenAPI | Content Hub | ¿Se muestra la lista desplegable Destino de aprobación? | Destino de aprobación predeterminado para recursos aprobados | Destino de publicación |
| --- | --- | --- | --- |---|
| Habilitado | Habilitado | Sí | Entrega | Dynamic Media con OpenAPI y Content Hub |
| No disponible | Habilitado | Sí | Content Hub | Content Hub |
| Habilitado | No disponible | Sí | Entrega | Dynamic Media con OpenAPI |
| No disponible | No disponible | No | N/D | N/D |

### Configuración de la fecha de caducidad del recurso {#set-asset-expiration-date}

La vista Assets también permite establecer una fecha de caducidad para los recursos disponibles en el repositorio. Entonces puede [filtrar los resultados de búsqueda](search-assets-view.md#refine-search-results) basados en un `Expired` estado del activo. Además, puede especificar un intervalo de fechas de caducidad para los recursos para filtrar aún más los resultados de búsqueda.

Para establecer la fecha de caducidad del recurso, haga lo siguiente:

1. Seleccione el recurso y haga clic en **[!UICONTROL Detalles]** en la barra de herramientas.

1. En la pestaña **[!UICONTROL Básico]**, defina la fecha de caducidad del recurso mediante el campo **[!UICONTROL Fecha de caducidad]**.

El indicador de la tarjeta de recursos `Expired` anula los indicadores `Approved` o `Rejected` definidos para un recurso.

También puede filtrar recursos según un estado de recurso. Para obtener más información, consulte [Buscar recursos en la vista de Assets](search-assets-view.md).

## Personalización de formularios de metadatos para incluir el campo de estado del activo {#customize-asset-status-metadata-form}

**Permisos necesarios:** Administrador

La vista de Assets proporciona muchos campos de metadatos estándar de forma predeterminada. Las organizaciones tienen requisitos de metadatos adicionales y necesitan más campos para agregar los específicos de su empresa. Los formularios de metadatos permiten a las empresas añadir campos de metadatos personalizados a la página [!UICONTROL Detalles] de un recurso. Los metadatos específicos de la empresa mejoran el control y el descubrimiento de sus recursos.

Para obtener más información sobre cómo agregar campos de metadatos adicionales al formulario de metadatos, consulte [Formularios de metadatos](metadata-assets-view.md#metadata-forms).

**Agregar el campo de metadatos Estado del activo al formulario**

Para agregar el campo de metadatos Estado del activo al formulario, arrastre **[!UICONTROL Estado del activo]** del carril izquierdo al formulario. La propiedad de asignación se rellena automáticamente previamente. Guarde el formulario para confirmar los cambios.

**Adición del campo de metadatos Fecha de caducidad al formulario**

Para añadir el campo de metadatos Fecha de caducidad al formulario, arrastre el componente **[!UICONTROL Fecha]** del carril izquierdo al formulario. Especifique la **Fecha de caducidad** como etiqueta y `pur:expirationDate` como propiedad de asignación. Guarde el formulario para confirmar los cambios.

## Siguientes pasos {#next-steps}

* [Vea un vídeo para administrar recursos en la vista de Assets](https://experienceleague.adobe.com/es/docs/experience-manager-learn/assets-essentials/basics/managing)

* Realice comentarios del producto mediante la opción [!UICONTROL Comentarios] disponible en la interfaz de usuario de la vista Recursos

* Proporcione comentarios sobre la documentación usando [!UICONTROL Editar esta página] ![editar la página](assets/do-not-localize/edit-page.png) o [!UICONTROL Registrar una incidencia] ![crear una incidencia de GitHub](assets/do-not-localize/github-issue.png), disponibles en la barra lateral derecha

* Contacto con el [Servicio de atención al cliente](https://experienceleague.adobe.com/es?support-solution=General#support)

