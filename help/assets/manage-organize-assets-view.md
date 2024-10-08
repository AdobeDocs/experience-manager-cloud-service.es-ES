---
title: Administración de recursos digitales
description: Mueva, elimine, copie, cambie de nombre, actualice y convierta en versión los recursos en [!DNL Assets view].
role: User, Leader
contentOwner: AG
exl-id: 2459d482-828b-4410-810c-ac55ef0a2119
feature: Asset Management, Publishing, Collaboration, Asset Processing
source-git-commit: e3fd0fe2ee5bad2863812ede2a294dd63864f3e2
workflow-type: tm+mt
source-wordcount: '1222'
ht-degree: 92%

---

# Administración de recursos {#manage-assets}

| [Prácticas recomendadas de búsqueda](/help/assets/search-best-practices.md) | [Prácticas recomendadas de metadatos](/help/assets/metadata-best-practices.md) | [Centro de contenido](/help/assets/product-overview.md) | [Dynamic Media con funciones OpenAPI](/help/assets/dynamic-media-open-apis-overview.md) | [Documentación para desarrolladores de AEM Assets](https://developer.adobe.com/experience-cloud/experience-manager-apis/) |
| ------------- | --------------------------- |---------|----|-----|

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

### Visualización de versiones de un recurso {#view-versions}

Al cargar una copia duplicada o modificada de un recurso, puede crear sus versiones. Las versiones le permiten revisar los recursos históricos y revertirlos a una versión anterior si es necesario.

Para ver las versiones, abra la previsualización de un recurso y haga clic en **[!UICONTROL Versiones]** ![Icono de versiones](assets/do-not-localize/versions-clock-icon.png) en la barra lateral derecha. Para previsualizar una versión específica, selecciónela. Para volver a ella, haga clic en **[!UICONTROL Crear más reciente]**.

También puede crear versiones a partir de la cronología de las versiones. Seleccione la última versión, haga clic en **[!UICONTROL Nueva versión]** y cargue una copia nueva del recurso desde el sistema de archivos local.

![Visualización de versiones de un recurso](assets/view-asset-versions1.png)

*Imagen: visualización de versiones de un recurso, reversión a una versión anterior o carga de otra versión nueva.*

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

