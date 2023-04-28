---
title: Administre recursos digitales
description: Descubra varios métodos de edición y administración de recursos
contentOwner: AG
mini-toc-levels: 3
feature: Asset Management,Publishing,Collaboration,Asset Processing
role: User,Architect,Admin
exl-id: 51a26764-ac2b-4225-8d27-42a7fd906183
source-git-commit: 8bdd89f0be5fe7c9d4f6ba891d7d108286f823bb
workflow-type: tm+mt
source-wordcount: '4356'
ht-degree: 10%

---

# Administración de recursos {#manage-assets}

Este artículo describe cómo administrar y editar recursos en [!DNL Adobe Experience Manager Assets]. Para administrar [!DNL Content Fragments], consulte [[!DNL Content Fragments]](content-fragments/content-fragments.md) activos.

## Crear carpetas {#creating-folders}

Al organizar una colección de recursos, por ejemplo, todos los `Nature` imágenes, puede crear carpetas para mantenerlas juntas. Puede utilizar carpetas para categorizar y organizar los recursos. [!DNL Experience Manager Assets] no requiere que organice los recursos en carpetas para que funcionen mejor.

>[!NOTE]
>
>* Uso compartido de una carpeta de recursos del tipo `sling:OrderedFolder`, no se admite al compartir con Experience Cloud. Si desea compartir una carpeta, no seleccione [!UICONTROL Pedido] al crear una carpeta.
>* El Experience Manager no permite el uso de `subassets` como nombre de una carpeta. Es una palabra clave reservada para el nodo que contiene subactivos para los recursos compuestos


1. Vaya al lugar de la carpeta de recursos digitales donde desee crear una carpeta nueva. En el menú , haga clic en **[!UICONTROL Crear]**. Select **[!UICONTROL Nueva carpeta]**.
1. En el **[!UICONTROL Título]** , proporcione un nombre de carpeta. De forma predeterminada, DAM utiliza el título que ha proporcionado como nombre de carpeta. Una vez creada la carpeta, puede anular el valor predeterminado y especificar otro nombre de carpeta.
1. Haga clic en **[!UICONTROL Crear]**. La carpeta se muestra en la carpeta de recursos digitales.

No se admiten los siguientes caracteres (lista de) separados por espacios:

* Un nombre de archivo de recurso no puede contener ninguno de estos caracteres: `* / : [ \\ ] | # % { } ? &`
* Un nombre de carpeta de recursos no puede contener ninguno de estos caracteres: `* / : [ \\ ] | # % { } ? \" . ^ ; + & \t`

## Carga de activos {#uploading-assets}

Consulte [agregar recursos digitales al Experience Manager](add-assets.md).

## Detectar recursos duplicados {#detect-duplicate-assets}

<!-- TBD: This feature may not work as documented. See CQ-4283718. Get PM review done. -->

Si un usuario de DAM carga uno o más recursos que ya existen en el repositorio, [!DNL Experience Manager] detecta la duplicación y notifica al usuario. La detección de duplicados está deshabilitada de forma predeterminada, ya que puede tener un impacto en el rendimiento en función del tamaño del repositorio y el número de recursos cargados.

Para habilitar la función:

1. Vaya a **[!UICONTROL Herramientas > Assets > Configuraciones de recursos]**.

1. Haga clic en **[!UICONTROL Detector de duplicación de recursos]**.

1. En el [!UICONTROL Página del detector de duplicación de recursos], haga clic en **[!UICONTROL Habilitado]**.

   `dam:sha1` para el campo Detectar metadatos garantiza que se detectarán recursos duplicados aunque los nombres de archivo sean diferentes.

1. Haga clic en **[!UICONTROL Guardar]**.

   ![Detector de duplicación de recursos](assets/asset-duplication-detector.png)

>[!NOTE]
>
>Si ha configurado el detector de duplicación mediante `/apps/example/config.author/com.adobe.cq.assetcompute.impl.assetprocessor.AssetDuplicationDetector.cfg.json` archivo de configuración (configuración OSGi), puede seguir usándolo, sin embargo, Adobe recomienda utilizar el nuevo método .


Una vez activado, el Experience Manager envía notificaciones de recursos duplicados a la bandeja de entrada del Experience Manager. Es un resultado agregado para varios duplicados. Los usuarios pueden elegir eliminar los recursos en función de los resultados.

![Notificación de bandeja de entrada para recursos duplicados](assets/duplicate-detect-inbox-notification.png)

>[!NOTE]
>
>Al cargar recursos en el repositorio, el Experience Manager detecta la duplicación y le notifica sobre los primeros 100 recursos duplicados.

## Previsualización de recursos {#previewing-assets}

Para obtener una vista previa de un recurso, siga estos pasos.

1. En la interfaz de usuario de Assets, vaya a la ubicación del recurso cuya vista previa desee ver.
1. Puntee en el recurso que desee para abrirlo.

1. En el modo de vista previa, las opciones de zoom están disponibles para [tipos de imagen admitidos](/help/assets/file-format-support.md) (con edición interactiva).

   Para acercar un recurso a un recurso, toque o haga clic en `+` (o toque o haga clic en la lupa del recurso). Para alejar, toque o haga clic `-`. Al acercar el zoom, puede observar de cerca cualquier área de la imagen mediante la panorámica. La flecha para restablecer el zoom le lleva de nuevo a la vista original.

   Toque **[!UICONTROL Restablecer]** para restablecer la vista al tamaño original.

## Editar propiedades {#editing-properties}

1. Navegue a la ubicación del recurso cuyos metadatos desee editar.

1. Seleccione el recurso y toque o haga clic en él **[!UICONTROL Propiedades]** en la barra de herramientas para ver las propiedades de los recursos. Como alternativa, elija la opción **[!UICONTROL Propiedades]** acción rápida en la tarjeta de recursos.

   ![properties_quickaction](assets/properties_quickaction.png)

1. En el [!UICONTROL Propiedades] edite las propiedades de los metadatos en varias pestañas. Por ejemplo, en la sección **[!UICONTROL Básico]** , edite el título, la descripción, etc.

   >[!NOTE]
   >
   >El diseño de la [!UICONTROL Propiedades] y las propiedades de metadatos disponibles dependen del esquema de metadatos subyacente. Para aprender a modificar el diseño del [!UICONTROL Propiedades] página, consulte [Esquemas de metadatos](/help/assets/metadata-schemas.md).

1. Para programar una fecha y hora determinada para la activación del recurso, utilice el selector de fechas situado junto al campo **[!UICONTROL Tiempo de activación]**.

   ![chlimage_1-217](assets/chlimage_1-217.png)

1. Para desactivar el recurso después de una duración determinada, seleccione la fecha y hora de desactivación del selector de fechas situado junto al **[!UICONTROL Tiempo de inactividad]** campo . La fecha de desactivación debe ser posterior a la fecha de activación de un recurso. Después de la [!UICONTROL Tiempo de inactividad], un recurso y sus representaciones no están disponibles a través de la interfaz web de Assets o a través de la API HTTP.

   ![chlimage_1-218](assets/chlimage_1-218.png)

1. En el **[!UICONTROL Etiquetas]** seleccione una o varias etiquetas. Para agregar una etiqueta personalizada, escriba el nombre de la etiqueta en el cuadro y seleccione la opción `Enter` clave. La nueva etiqueta se guarda en [!DNL Experience Manager].

   YouTube requiere que las etiquetas se publiquen y que tengan un vínculo a YouTube (si se encuentra un vínculo adecuado).

   >[!NOTE]
   >
   >Para crear etiquetas, debe tener permiso de escritura en `/content/cq:tags/default` en el repositorio CRX.

1. Toque o haga clic **[!UICONTROL Guardar y cerrar]**.

1. Vaya a la interfaz de usuario de Assets. Las propiedades de metadatos editadas, como el título, la descripción y las etiquetas, se muestran en la tarjeta de recursos de la vista de tarjeta y en las columnas relevantes de la vista de lista.

<!-- TBD: Uncomment after verification for Dec release.

## View asset usage and references {#usage-and-references}

[!DNL Experience Manager] lets you track statistics about usage of a digital asset. The usage statistics include the following:

    * Number of times the asset was viewed or downloaded
    * Channels/devices through which the asset was used
    * Creative solutions where the asset was recently used

To view usage statistics for an asset, in the [!UICONTROL Properties] page, click the **[!UICONTROL Insights]** tab. For more details, see [Assets Insights](assets-insights.md).

[!DNL Experience Manager] also lets you check all the incoming references to an asset, that is, the usage of an asset in remote [!DNL Sites] and in compound assets. Authors of webpages on [!DNL Experience Manager Sites] deployment can use an asset on a remote [!DNL Assets] deployment using the Connected Assets functionality. The [!UICONTROL References] tab in an asset's [!UICONTROL Properties] page lists the local and remote references of the asset. That is, the use of assets in compound assets in [!DNL Assets] and its use in remote [!DNL Sites] pages.

-->

## Copiar recursos {#copying-assets}

Al copiar un recurso o una carpeta, se copia todo el recurso o la carpeta, junto con su estructura de contenido. Un recurso copiado o una carpeta se duplica en la ubicación de destino. El recurso en la ubicación de origen no se modifica.

No se arrastran algunos atributos que son exclusivos de una copia concreta de un recurso. Algunos ejemplos son:

* ID del recurso, fecha y hora de creación, versiones e historial de versiones. Algunas de estas propiedades están indicadas por las propiedades `jcr:uuid`, `jcr:created`y `cq:name`.

* El tiempo de creación y las rutas a las que se hace referencia son únicos para cada recurso y cada una de sus representaciones.

La información de otras propiedades y metadatos se conserva. No se crea una copia parcial al copiar un recurso.

1. En la interfaz de usuario de Assets, seleccione uno o varios recursos y, a continuación, toque o haga clic en el **[!UICONTROL Copiar]** de la barra de herramientas. Como alternativa, seleccione el **[!UICONTROL Copiar]** ![copy_icon](assets/copy_icon.png) acción rápida desde la tarjeta de recursos.

   >[!NOTE]
   >
   >Si usa la variable [!UICONTROL Copiar] acción rápida, solo puede copiar un recurso a la vez.

1. Desplácese a la ubicación en la que desee copiar los recursos.

   >[!NOTE]
   >
   >Si copia un recurso en la misma ubicación, [!DNL Experience Manager] genera automáticamente una variación del nombre. Por ejemplo, si copia un recurso con el título `Square`, [!DNL Experience Manager] genera automáticamente el título de su copia como `Square1`.

1. Haga clic en el **[!UICONTROL Pegar]** icono de recurso de la barra de herramientas. Los recursos se copian en esta ubicación.

   ![chlimage_1-219](assets/chlimage_1-219.png)

   >[!NOTE]
   >
   >La variable **[!UICONTROL Pegar]** está disponible en la barra de herramientas hasta que se complete la operación de pegado.

### Mover o cambiar el nombre de los recursos {#moving-or-renaming-assets}

1. Navegue a la ubicación del recurso que desee mover.

1. Seleccione el recurso y toque o haga clic en el **[!UICONTROL Mover]** icono ![move_icon](assets/move_icon.png) en la barra de herramientas.

1. En el asistente Mover recursos , realice una de las siguientes acciones:

   * Especifique el nombre del recurso cuando se haya desplazado. A continuación, toque o haga clic **[!UICONTROL Siguiente]** para continuar.

   * Toque o haga clic **[!UICONTROL Cancelar]** para detener el proceso.
   >[!NOTE]
   >
   >* Puede especificar el mismo nombre para el recurso si no hay ningún recurso con ese nombre en la nueva ubicación. Sin embargo, debe utilizar un nombre diferente si mueve el recurso a una ubicación donde exista un recurso con el mismo nombre. Si utiliza el mismo nombre, el sistema genera automáticamente una variación del nombre. Por ejemplo, si el recurso tiene el nombre Cuadrado, el sistema genera el nombre Cuadrado1 para su copia.
   >* Al cambiar el nombre, no se permiten espacios en blanco en el nombre del archivo.


1. En el **[!UICONTROL Seleccionar destino]** , realice una de las siguientes acciones:

   * Vaya a la nueva ubicación de los recursos y, a continuación, toque o haga clic en **[!UICONTROL Siguiente]** para continuar.

   * Toque o haga clic **[!UICONTROL Atrás]** para volver a la **[!UICONTROL Cambiar nombre]** en el Navegador.

1. Si los recursos que se mueven tienen páginas, recursos o colecciones de referencia, la variable **[!UICONTROL Ajustar referencias]** aparece junto a la pestaña **[!UICONTROL Seleccionar destino]** pestaña .

   Realice una de las siguientes acciones en la sección **[!UICONTROL Ajustar referencias]** pantalla:

   * Especifique las referencias que desea ajustar en función de los nuevos detalles y, a continuación, toque o haga clic en **[!UICONTROL Mover]** para continuar.

   * En el **[!UICONTROL Ajustar]** , seleccione o anule la selección de referencias a los recursos.
   * Toque o haga clic **[!UICONTROL Atrás]** para volver a la **[!UICONTROL Seleccionar destino]** en el Navegador.

   * Toque o haga clic **[!UICONTROL Cancelar]** para detener la operación de movimiento.

   Si no actualiza las referencias, seguirán apuntando a la ruta anterior del recurso. Si ajusta las referencias, se actualizan a la nueva ruta de recursos.

### Administrar representaciones {#managing-renditions}

1. Puede añadir o eliminar representaciones para un recurso, excepto el original. Desplácese a la ubicación del recurso para el que desee agregar o quitar representaciones.

1. Toque o haga clic en el recurso para abrir su página de recursos.

   ![chlimage_1-220](assets/chlimage_1-220.png)

1. Pulse o haga clic en el icono de navegación global y seleccione **[!UICONTROL Representaciones]** de la lista.

   ![renditions_menu](assets/renditions_menu.png)

1. En el **[!UICONTROL Representaciones]** , consulte la lista de representaciones generadas para el recurso.

   ![renditions_panel](assets/renditions_panel.png)

   >[!NOTE]
   >
   >De forma predeterminada, [!DNL Experience Manager Assets] no muestra la representación original del recurso en el modo de vista previa. Si es administrador, puede utilizar superposiciones para configurar [!DNL Assets] para mostrar las representaciones originales en el modo de vista previa.

1. Seleccione una representación para verla o eliminarla.

   **Eliminación de una representación**

   Seleccione una representación en el **[!UICONTROL Representaciones]** y, a continuación, toque o haga clic en el **[!UICONTROL Eliminar representación]** de la barra de herramientas. Las representaciones no se pueden eliminar de forma masiva una vez finalizado el procesamiento de recursos. Para recursos individuales, puede eliminar las representaciones manualmente desde la interfaz de usuario. Para varios recursos, puede personalizar [!DNL Experience Manager] para eliminar representaciones específicas o eliminar los recursos y volver a cargar los recursos eliminados.

   ![delete_renditionicon](assets/delete_renditionicon.png)

   **Carga de una nueva representación**

   Vaya a la página de detalles del recurso y pulse o haga clic en el icono **[!UICONTROL Agregar representación]** de la barra de herramientas para cargar una nueva representación para el recurso.

   ![chlimage_1-221](assets/chlimage_1-221.png)

   >[!NOTE]
   >
   >Si selecciona una representación en el panel **[!UICONTROL Representaciones]**, la barra de herramientas cambia de contexto y muestra solo las acciones que son relevantes para la representación. Las opciones, como el icono Cargar representación, no se muestran. Para ver estas opciones en la barra de herramientas, vaya a la página de detalles del recurso.

   Puede configurar las dimensiones de la representación que desea que se muestren en la página de detalles de una imagen o un recurso de vídeo. En función de las dimensiones que especifique, Assets muestra la representación con las dimensiones exactas o más cercanas.

   Para configurar las dimensiones de representación de una imagen en el nivel de detalle del recurso, superponga el `renditionpicker` nodo (`libs/dam/gui/content/assets/assetpage/jcr:content/body/content/content/items/assetdetail/items/col1/items/assetview/renditionpicker`) y configure el valor de la propiedad de anchura. Configure el **[!UICONTROL tamaño de la propiedad (Long) en KB]** en lugar de la anchura para personalizar la representación en la página de detalles del recurso según el tamaño de la imagen. En el caso de la personalización basada en el tamaño, la propiedad `preferOriginal` asigna preferencia al original si el tamaño de la representación coincidente es mayor que el del original.

   Del mismo modo, puede personalizar la imagen de la página Anotación superponiendo `libs/dam/gui/content/assets/annotate/jcr:content/body/content/content/items/content/renditionpicker`.

   ![chlimage_1-222](assets/chlimage_1-222.png)

   Para configurar las dimensiones de representación de un recurso de vídeo, vaya a la `videopicker` en el repositorio CRX en la ubicación `/libs/dam/gui/content/assets/assetpage/jcr:content/body/content/content/items/assetdetail/items/col1/items/assetview/videopicker`, superponga el nodo y, a continuación, edite la propiedad correspondiente.

   >[!NOTE]
   >
   >Las anotaciones de vídeo solo se admiten en exploradores con formatos de vídeo compatibles con HTML5. Además, según el navegador, se admiten diferentes formatos de vídeo. Sin embargo, el formato de vídeo MXF aún no es compatible con anotaciones de vídeo.

## Eliminar recursos {#delete-assets}

Para resolver o eliminar las referencias entrantes de otras páginas, actualice las referencias relevantes antes de eliminar un recurso.

Además, desactive el botón de forzar eliminación mediante una superposición para impedir que los usuarios eliminen los recursos a los que se hace referencia y dejen los vínculos rotos.

1. Navegue a la ubicación de los recursos que desee eliminar.

1. Seleccione el recurso y haga clic en **[!UICONTROL Eliminar]** ![delete_icon](assets/do-not-localize/delete-icon.png) en la barra de herramientas.

1. En el cuadro de diálogo de confirmación, haga clic en:

   * **[!UICONTROL Cancelar]** para detener la acción
   * **[!UICONTROL Eliminar]** para confirmar la acción:

      * Si el recurso no tiene referencias, se eliminará.
      * Si el recurso tiene referencias, un mensaje de error le informa de que **[!UICONTROL Se hace referencia a uno o varios recursos]**. Puede seleccionar **[!UICONTROL Forzar eliminación]** o **[!UICONTROL Cancelar]**.

   >[!NOTE]
   >
   >Necesita permisos de eliminación en dam/asset para poder eliminar un recurso. Si solo tiene permisos de modificación, solo puede editar los metadatos del recurso y añadir anotaciones al recurso. Sin embargo, no puede eliminar el recurso o sus metadatos.

   >[!NOTE]
   >
   >Para resolver o eliminar las referencias entrantes de otras páginas, actualice las referencias relevantes antes de eliminar un recurso. No se puede permitir la eliminación de los recursos a los que se hace referencia, ya que provoca la interrupción de los vínculos. Desactive el botón de eliminación forzada mediante una superposición.

## Descarga de recursos {#download-assets}

Consulte [descargar recursos de [!DNL Experience Manager]](/help/assets/download-assets-from-aem.md).

## Publicar o cancelar la publicación de recursos {#publish-assets}

1. Vaya a la ubicación del recurso o de la carpeta de recursos que desea publicar o que desea eliminar del entorno de publicación (cancelar la publicación).

1. Seleccione el recurso o la carpeta que desea publicar o cancelar la publicación y seleccione **[!UICONTROL Administrar publicación]** ![opción administrar publicación](assets/do-not-localize/globe-publication.png) en la barra de herramientas. Como alternativa, para publicar rápidamente, seleccione la opción **[!UICONTROL Publicación rápida]** en la barra de herramientas. Si la carpeta que desea publicar incluye una carpeta vacía, la carpeta vacía no se publica.

1. Seleccione el **[!UICONTROL Publicación]** o **[!UICONTROL Cancelar la publicación]** como sea necesario.

   ![Cancelar publicación](assets/unpublish_action.png)
   *Figura: Publicar y cancelar la publicación y la opción de programación.*

1. Select **[!UICONTROL Ahora]** para actuar sobre el recurso de inmediato o seleccione **[!UICONTROL Más tarde]** para programar la acción. Seleccione una fecha y una hora si elige la variable **[!UICONTROL Más tarde]** . Haga clic en **[!UICONTROL Siguiente]**.

1. Al publicar, si un recurso hace referencia a otros recursos, sus referencias se enumeran en el asistente. Solo se muestran las referencias que se han cancelado la publicación o se han modificado desde la última publicación. Elija las referencias que desea publicar.

1. Al cancelar la publicación, si un recurso hace referencia a otros recursos, elija las referencias que desea cancelar la publicación. Haga clic en **[!UICONTROL Cancelar la publicación]**. En el cuadro de diálogo de confirmación, haga clic en **[!UICONTROL Cancelar]** para detener la acción o haga clic en **[!UICONTROL Cancelar la publicación]** para confirmar que los recursos se cancelarán en la fecha especificada.

Comprenda las siguientes limitaciones y sugerencias relacionadas con la publicación o cancelación de la publicación de recursos o carpetas:

* La opción para [!UICONTROL Administrar publicación] solo está disponible para las cuentas de usuario que tienen permisos de replicación.
* Al cancelar la publicación de un recurso complejo, cancele la publicación del recurso únicamente. Evite cancelar la publicación de las referencias porque otros recursos publicados pueden hacer referencia a ellas.
* Las carpetas vacías no se publican.
* Si publica recursos que se están procesando, solo se publicará el contenido original. Faltan las representaciones. Espere a que se complete el procesamiento y, a continuación, publique o vuelva a publicar el recurso una vez finalizado el procesamiento.

## Grupo de usuarios cerrado {#closed-user-group}

Un grupo de usuarios cerrado (CUG) se utiliza para limitar el acceso a carpetas de recursos específicas publicadas desde [!DNL Experience Manager]. Si crea un CUG para una carpeta, el acceso a la carpeta (incluidos los recursos de la carpeta y las subcarpetas) está restringido solo a los miembros o grupos asignados. Para acceder a la carpeta, deben iniciar sesión con sus credenciales de seguridad.

Los CUG son una forma adicional de restringir el acceso a sus recursos. También puede configurar una página de inicio de sesión para la carpeta.

1. Seleccione una carpeta en la interfaz de usuario de Assets y pulse o haga clic en el icono Propiedades de la barra de herramientas para mostrar la página de propiedades.
1. En el **[!UICONTROL Permisos]** ficha, agregar miembros o grupos en **[!UICONTROL Grupo de usuarios cerrado]**.

   ![add_user](assets/add_user.png)

1. Para mostrar una pantalla de inicio de sesión cuando los usuarios acceden a la carpeta, seleccione la opción **[!UICONTROL Habilitar]** . A continuación, seleccione la ruta a una página de inicio de sesión en [!DNL Experience Manager]y guarde los cambios.

   ![login_page](assets/login_page.png)

   >[!NOTE]
   >
   >Si no especifica la ruta a una página de inicio de sesión, [!DNL Experience Manager] muestra la página de inicio de sesión predeterminada en la instancia de publicación.

1. Publique la carpeta e intente acceder a ella desde la instancia de publicación. Se muestra una pantalla de inicio de sesión.
1. Si es miembro de CUG, introduzca sus credenciales de seguridad. La carpeta se muestra después de [!DNL Experience Manager] le autentica.

## Buscar recursos {#search-assets}

La búsqueda de recursos es fundamental para el uso de un sistema de administración de recursos digitales, ya sea para su uso posterior por parte de los creativos, para la sólida administración de recursos por parte de los usuarios comerciales y los especialistas en marketing, o para la administración por parte de los administradores de DAM.

Para realizar búsquedas simples, avanzadas y personalizadas con el fin de descubrir y utilizar los recursos más adecuados, consulte [buscar recursos en [!DNL Experience Manager]](/help/assets/search-assets.md).

## Acciones rápidas {#quick-actions}

Los iconos de acción rápida están disponibles para un único recurso a la vez. En función del dispositivo, realice las siguientes acciones para mostrar los iconos de acción rápida:

* Dispositivos táctiles: Toque y sostenga. Por ejemplo, en un iPad, puede pulsar y mantener presionado un recurso para que se muestren las acciones rápidas.
* Dispositivos no táctiles: Puntero al pasar el ratón. Por ejemplo, en un dispositivo de escritorio, se muestra la barra de acciones rápidas si pasa el puntero sobre la miniatura del recurso.

<!-- Hiding this topic via cqdoc-18707

## Edit images {#editing-images}

The editing tools in the [!DNL Experience Manager Assets] interface let you perform small editing jobs on image assets. You can crop, rotate, flip, and perform other editing jobs on images. You can also add image maps to assets.

>[!NOTE]
>
>For some components, the Full Screen mode has additional options available.

1. Do one of the following to open an asset in edit mode:

    * Select the asset and then click/tap the **[!UICONTROL Edit]** icon in the toolbar.
    * Tap/click the **[!UICONTROL Edit]** icon that appears on an asset in the Card view.
    * In the asset page, tap/click the **[!UICONTROL Edit]** icon in the toolbar.

   ![edit_icon](assets/edit_icon.png)

1. To crop the image, tap/click the **Crop** icon.

   ![chlimage_1-226](assets/chlimage_1-226.png)

1. Select the desired option from the list. The crop area appears on the image based on the option you choose. The **Free Hand** option lets you crop the image without any aspect ratio restrictions.

   ![chlimage_1-227](assets/chlimage_1-227.png)

1. Select the area to be cropped, and resize or reposition it on the image.
1. Use the **Finish** icon (top right corner) to crop the image. Clicking the **Finish** icon also triggers the regeneration of renditions.

   ![chlimage_1-228](assets/chlimage_1-228.png)

1. Use the **Undo** and **Redo** icons on the top right to revert to the uncropped image or retain the cropped image, respectively.

   ![chlimage_1-229](assets/chlimage_1-229.png)

1. Tap/click the appropriate Rotate icon to rotate the image clockwise or anti-clockwise.

   ![chlimage_1-230](assets/chlimage_1-230.png)

1. Tap/click the appropriate Flip icon to flip the image horizontally or vertically.

   ![chlimage_1-231](assets/chlimage_1-231.png)

1. Tap/click the **Finish** icon to save the changes.

   ![chlimage_1-232](assets/chlimage_1-232.png)

>[!NOTE]
>
>Image editing is supported for BMP, GIF, PNG, and JPEG files formats.

>[!NOTE]
>
>To edit a TXT file, set **Day CQ Link Externalizer** from Configuration Manager.
-->

## Escala de cronología {#timeline}

La cronología permite ver varios eventos de un elemento seleccionado, como flujos de trabajo activos de un recurso, comentarios/anotaciones, registros de actividades y versiones.

![Ordenar entradas de línea de tiempo para un recurso](assets/sort_timeline.gif)
*Figura: Ordenar entradas de línea de tiempo para un recurso*

>[!NOTE]
>
>En el [Consola Colecciones](/help/assets/manage-collections.md#navigate-the-collections-console), el **[!UICONTROL Mostrar todo]** proporciona opciones para ver solo comentarios y flujos de trabajo. Además, la línea de tiempo solo se muestra para las colecciones de nivel superior que aparecen en la consola. No se muestra si se desplaza dentro de ninguna de las colecciones.

>[!NOTE]
>
>La línea de tiempo contiene varias [opciones específicas de los fragmentos de contenido](content-fragments/content-fragments.md).

## Anotar recursos {#annotating}

Las anotaciones son comentarios o notas explicativas añadidas a imágenes o vídeos. Las anotaciones permiten a los especialistas en marketing colaborar y dejar comentarios sobre los recursos.

Las anotaciones de vídeo solo se admiten en exploradores con formatos de vídeo compatibles con HTML5. Los formatos de vídeo compatibles con Assets dependen del explorador. Sin embargo, el formato de vídeo MXF aún no es compatible con anotaciones de vídeo.

>[!NOTE]
>
>Para fragmentos de contenido, [las anotaciones se crean en el editor de fragmentos](content-fragments/content-fragments.md).

1. Navegue a la ubicación del recurso al que desee agregar anotaciones.
1. Toque o haga clic en el botón **[!UICONTROL Anotar]** de una de las siguientes opciones:

   * [Acciones rápidas](#quick-actions)
   * En la barra de herramientas después de seleccionar el recurso o de desplazarse a la página de recursos

   ![chlimage_1-233](assets/chlimage_1-233.png)

1. Agregue un comentario en el cuadro **[!UICONTROL Comentario]** de la parte inferior de la cronología. También puede marcar un área de la imagen y agregar una anotación en el cuadro de diálogo **[!UICONTROL Agregar anotación]**.

   ![chlimage_1-234](assets/chlimage_1-234.png)

<!--
1. To notify a user about an annotation, specify the email address of the user and add the comment. For example, to notify Aaron MacDonald about an annotation, enter @aa. Hints for all matching users is displayed in a list. Select Aaron's email address from the list to tag her with the comment. Similarly, you can tag more users anywhere within the annotation or before or after it.
-->

>[!NOTE]
>
>Para los usuarios que no son administradores, las sugerencias aparecen solo si el usuario tiene permisos de lectura en `/home` en CRXDE.

![chlimage_1-235](assets/chlimage_1-235.png)

1. Después de añadir la anotación, haga clic en **[!UICONTROL Agregar]** para guardarlo. Se envía una notificación para la anotación a Aaron.

   ![chlimage_1-236](assets/chlimage_1-236.png)

   >[!NOTE]
   >
   >Puede agregar varias anotaciones antes de guardarlas.

1. Toque o haga clic **[!UICONTROL Cerrar]** para salir del modo de anotación.
1. Para ver la notificación, inicie sesión en Assets con las credenciales de Aaron MacDonald&#39;s y haga clic en el botón **[!UICONTROL Notificaciones]** para ver la notificación.

   >[!NOTE]
   >
   >Las anotaciones también se pueden agregar a los recursos de vídeo. Al anotar vídeos, el reproductor se detiene para permitirle realizar anotaciones en un marco. Para obtener más información, consulte [administración de recursos de vídeo](manage-video-assets.md). Sin embargo, el formato de vídeo MXF aún no es compatible con anotaciones de vídeo.

1. Para elegir un color diferente y poder diferenciar entre usuarios, toque o haga clic en el icono Perfil y pulse o haga clic en **[!UICONTROL Mis preferencias]**.

   ![chlimage_1-237](assets/chlimage_1-237.png)

   Especifique el color que desee en el cuadro **[!UICONTROL Color de anotación]** y pulse o haga clic en **[!UICONTROL Aceptar]**.

   ![chlimage_1-238](assets/chlimage_1-238.png)

>[!NOTE]
>
>También puede agregar anotaciones a una colección. Sin embargo, si una colección contiene colecciones secundarias, solo puede agregar anotaciones/comentarios a la colección principal. La opción Anotar no está disponible para colecciones secundarias.

### Ver anotaciones guardadas {#viewing-saved-annotations}

Solo puede ver una anotación a la vez.

>[!NOTE]
>
>Si selecciona varias anotaciones, la anotación más reciente estará visible en la interfaz de usuario.
>
>La selección múltiple solo se admite para imprimir el recurso anotado como PDF.

1. Para ver las anotaciones guardadas para un recurso, vaya a la ubicación del recurso y abra la página del recurso.

1. Pulse o haga clic en el icono de navegación global y elija **[!UICONTROL Cronología]** de la lista.

   ![chlimage_1-239](assets/chlimage_1-239.png)

1. En la lista **[!UICONTROL Mostrar todo]** de la cronología, seleccione **[!UICONTROL Comentarios]** para filtrar los resultados según las anotaciones.

   ![chlimage_1-240](assets/chlimage_1-240.png)

   Toque o haga clic en un comentario de la sección **[!UICONTROL Cronología]** para ver la anotación correspondiente en la imagen.

   ![chlimage_1-241](assets/chlimage_1-241.png)

   Toque o haga clic **[!UICONTROL Eliminar]**, para eliminar un comentario en particular.

### Imprimir anotaciones {#printing-annotations}

Si un recurso tiene anotaciones o se ha sometido a un flujo de trabajo de revisión, puede imprimir el recurso junto con anotaciones y revisar su estado como archivo PDF para revisiones sin conexión.

También puede elegir imprimir solo las anotaciones o el estado de revisión.

>[!NOTE]
>
>Puede seleccionar varias anotaciones al imprimir el recurso anotado como PDF.

Para imprimir las anotaciones y revisar el estado, toque o haga clic en el botón **[!UICONTROL Imprimir]** y siga las instrucciones del asistente. La variable **[!UICONTROL Imprimir]** aparece en la barra de herramientas solo cuando el recurso tiene asignado al menos una anotación o un estado de revisión.

1. En la interfaz de usuario de Assets, abra la página de vista previa de un recurso.
1. Realice una de las siguientes acciones:

   * Para imprimir todas las anotaciones y el estado de la revisión, omita el paso 3 y vaya directamente al paso 4.
   * Para imprimir anotaciones específicas y revisar el estado, abra el [cronología](/help/assets/manage-digital-assets.md#timeline) y luego vaya al paso 3.

1. Para imprimir anotaciones específicas, seleccione las anotaciones en la cronología.

   ![chlimage_1-242](assets/chlimage_1-242.png)

   Para imprimir solo el estado de revisión, selecciónelo en la cronología.

   ![imagen_1-243](assets/chlimage_1-243.png)

1. Toque o haga clic en el botón **[!UICONTROL Imprimir]** de la barra de herramientas.

   ![chlimage_1-244](assets/chlimage_1-244.png)

1. En el cuadro de diálogo Imprimir, elija la posición en la que desea que se muestre el estado de las anotaciones/revisiones en el PDF. Por ejemplo, si desea que las anotaciones o el estado se impriman en la parte superior derecha de la página que contiene la imagen impresa, use la variable **Superior izquierda** configuración. Se selecciona de forma predeterminada.

   ![chlimage_1-245](assets/chlimage_1-245.png)

   Puede elegir otros ajustes en función de la posición en la que desea que aparezcan las anotaciones o el estado en el PDF impreso. Si desea que las anotaciones o el estado aparezcan en una página independiente del recurso impreso, elija **[!UICONTROL Página siguiente]**.

1. Haga clic en **[!UICONTROL Imprimir]**. Según la opción elegida en el paso 2, el PDF generado muestra las anotaciones/el estado en la posición especificada. Por ejemplo, si elige imprimir las anotaciones y el estado de la revisión mediante la configuración **Superior izquierda**, la salida generada se parece al archivo PDF que se muestra aquí.

   ![chlimage_1-246](assets/chlimage_1-246.png)

1. Descargue o imprima el PDF con las opciones de la parte superior derecha.

   ![chlimage_1-247](assets/chlimage_1-247.png)

   Para modificar el aspecto del archivo del PDF representado, por ejemplo, el color de fuente, el tamaño y el estilo, el color de fondo de los comentarios y estados, abra la **[!UICONTROL Configuración del PDF de anotaciones]** de Configuration Manager y modifique las opciones deseadas. Por ejemplo, para cambiar el color de visualización del estado aprobado, modifique el código de color en el campo correspondiente. Para obtener información sobre cómo cambiar el color de fuente de las anotaciones, consulte [Anotación](/help/assets/manage-digital-assets.md#annotating).

   Vuelva al archivo de PDF representado y actualícelo. El PDF actualizado refleja los cambios realizados.

## Creación de versiones de recursos {#asset-versioning}

Al generar versiones, se crea una instantánea de los recursos digitales en un momento específico. El control de versiones ayuda a restaurar los recursos a un estado anterior en un momento posterior. Por ejemplo, si desea deshacer un cambio realizado en un recurso, restaure la versión sin editar del recurso.

A continuación se indican las situaciones en las que se crean versiones:

* Puede modificar una imagen en otra aplicación y cargarla en Assets. Se crea una versión de la imagen para que la imagen original no se sobrescriba.
* Los metadatos de un recurso se editan.
* Utilice [!DNL Experience Manager] aplicación de escritorio para extraer un recurso existente y guardar los cambios. Se crea una nueva versión cada vez que se guarda el recurso.

También puede habilitar el control automático de versiones mediante un flujo de trabajo. Al crear una versión para un recurso, los metadatos y las representaciones se guardan junto con la versión. Las representaciones son alternativas representativas de las mismas imágenes, por ejemplo, una representación PNG de un archivo JPEG cargado.

La funcionalidad de versiones le permite hacer lo siguiente:

* Cree una versión de un recurso.
* Ver la revisión actual de un recurso.
* Restaurar el recurso a una versión anterior.

1. Vaya a la ubicación del recurso para el que desea crear una versión y toque o haga clic en él para abrir su página de recursos.

1. Toque o haga clic en el icono de navegación global y elija **[!UICONTROL Cronología]** del menú .

   ![cronología](assets/timeline.png)

1. Toque o haga clic en el botón **[!UICONTROL Acciones]** (flecha) en la parte inferior para ver las acciones disponibles que puede realizar en el recurso.

   ![chlimage_1-249](assets/chlimage_1-249.png)

1. Toque o haga clic **[!UICONTROL Guardar como versión]** para crear una versión para el recurso.

   ![chlimage_1-250](assets/chlimage_1-250.png)

1. Agregue una etiqueta y un comentario y, a continuación, haga clic en **[!UICONTROL Crear]** para crear una versión. Alternativamente, toque o haga clic **Cancelar** para salir de la operación.

   ![chlimage_1-251](assets/chlimage_1-251.png)

1. Para ver la nueva versión, abra la lista **[!UICONTROL Mostrar todo]** en la cronología de la página de detalles de recursos o de la interfaz de usuario de recursos y elija **[!UICONTROL Versiones]**. Todas las versiones creadas para un recurso se muestran en la pestaña de cronología. Puede filtrar la lista para mostrar Versiones, haciendo clic en la flecha de colocación y seleccionando **[!UICONTROL Versiones]** en la lista.

   ![versions_option](assets/versions_option.png)

1. Seleccione una versión específica del recurso para previsualizarlo o habilite su aparición en la interfaz de usuario de Assets.

   ![select_version](assets/select_version.png)

1. Agregue una etiqueta y un comentario para que la versión vuelva a la versión concreta de la interfaz de usuario de Assets.

   ![save_version](assets/save_version.png)

1. Para generar una vista previa de la versión, pulse o haga clic en **[!UICONTROL Vista previa de la versión]**.
1. Para mostrar esta versión en la interfaz de usuario de Assets, seleccione **[!UICONTROL Revertir a esta versión]**.
1. Para comparar dos versiones, vaya a la página de recursos del recurso y toque o haga clic en la versión que desea comparar con la versión actual.

   ![select_version_tocompare](assets/select_version_tocompare.png)

1. En la cronología, seleccione la versión que desee comparar y arrastre el control deslizante a la izquierda para superponer esta versión sobre la versión actual y comparar.

   ![compare_versions](assets/compare_versions.png)

### Inicio de un flujo de trabajo en un recurso {#starting-a-workflow-on-an-asset}

1. Vaya a la ubicación del recurso para el que desea iniciar un flujo de trabajo y pulse o haga clic en el recurso para abrir la página del recurso.
1. Toque o haga clic en el icono de navegación global y elija **[!UICONTROL Cronología]** en el menú para mostrar la línea de tiempo.

   ![línea de tiempo-1](assets/timeline-1.png)

1. Toque o haga clic en el botón **[!UICONTROL Acciones]** (flecha) en la parte inferior para abrir la lista de acciones disponibles para el recurso.

   ![chlimage_1-252](assets/chlimage_1-252.png)

1. Toque o haga clic **[!UICONTROL Iniciar flujo de trabajo]** de la lista.

   ![chlimage_1-253](assets/chlimage_1-253.png)

1. En el **[!UICONTROL Iniciar flujo de trabajo]** seleccione un modelo de flujo de trabajo en la lista.

   ![chlimage_1-254](assets/chlimage_1-254.png)

1. (Opcional) Especifique un título para el flujo de trabajo, que se puede utilizar para hacer referencia a la instancia de flujo de trabajo.

   ![chlimage_1-255](assets/chlimage_1-255.png)

1. Pulse o haga clic en **[!UICONTROL Iniciar]** y, a continuación, pulse o haga clic en **[!UICONTROL Continuar]** en el cuadro de diálogo para confirmar. Cada paso del flujo de trabajo se muestra en la cronología como un evento.

   ![chlimage_1-256](assets/chlimage_1-256.png)

## Colecciones {#collections}

Una colección es un conjunto ordenado de recursos. Utilice las colecciones para compartir recursos entre los usuarios.

* Una colección puede incluir recursos de distintas ubicaciones porque solo contienen referencias a estos recursos. Cada colección mantiene la integridad referencial de los recursos.
* Puede compartir colecciones con varios usuarios con diferentes niveles de privilegios, como editar, ver, etc.

Para obtener más información sobre la administración de colecciones, consulte [administrar colecciones](/help/assets/manage-collections.md).

## Ocultar recursos caducados al ver recursos en la aplicación de escritorio o en el vínculo de recursos de Adobe {#hide-expired-assets-via-acp-api}

[!DNL Experience Manager] la aplicación de escritorio permite acceder al repositorio DAM desde Windows o Mac local. El vínculo de recursos de Adobe permite acceder a los recursos desde el interior de los recursos admitidos [!DNL Creative Cloud] aplicaciones de escritorio.

Al examinar recursos desde [!DNL Experience Manager] interfaz de usuario de , no se muestran los recursos caducados. Para evitar la visualización, búsqueda y captura de recursos caducados al examinar recursos desde la aplicación de escritorio y Asset Link, los administradores pueden realizar la siguiente configuración. La configuración funciona para todos los usuarios, independientemente del privilegio de administrador.

Ejecute el siguiente comando CURL. Asegúrese de tener acceso de lectura activado `/conf/global/settings/dam/acpapi/` para los usuarios que acceden a los recursos. Usuarios que forman parte de `dam-user` tienen el permiso de forma predeterminada.

```curl
curl -v -u admin:admin --location --request POST 'http://localhost:4502/conf/global/settings/dam/acpapi/configuration/_jcr_content' \
--header 'Content-Type: application/x-www-form-urlencoded' \
--data-urlencode 'jcr:title=acpapiconfig' \
--data-urlencode 'hideExpiredAssets=true' \
--data-urlencode 'hideExpiredAssets@TypeHint=Boolean' \
--data-urlencode 'jcr:primaryType=nt:unstructured' \
--data-urlencode '../../jcr:primaryType=sling:Folder'
```

Para obtener más información, consulte cómo [examinar recursos DAM mediante la aplicación de escritorio](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#browse-search-preview-assets) y [cómo utilizar Adobe Asset Link](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/manage-assets-using-adobe-asset-link.ug.html).

**Consulte también**

* [Traducir recursos](translate-assets.md)
* [API HTTP de Recursos](mac-api-assets.md)
* [Formatos de archivo compatibles con Assets](file-format-support.md)
* [Buscar recursos](search-assets.md)
* [Recursos conectados](use-assets-across-connected-assets-instances.md)
* [Informes de Asset](asset-reports.md)
* [Esquemas de metadatos](metadata-schemas.md)
* [Descarga de recursos](download-assets-from-aem.md)
* [Administración de metadatos](manage-metadata.md)
* [Facetas de búsqueda](search-facets.md)
* [Administrar colecciones](manage-collections.md)
* [Importación masiva de metadatos](metadata-import-export.md)
