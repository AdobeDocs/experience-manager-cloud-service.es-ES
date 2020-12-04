---
title: Administre recursos digitales
description: Obtenga información sobre varios métodos de edición y administración de recursos.
contentOwner: AG
mini-toc-levels: 1
translation-type: tm+mt
source-git-commit: 3207151a76c51637551907d15a34f1a6b7450d02
workflow-type: tm+mt
source-wordcount: '4408'
ht-degree: 12%

---


# Administrar recursos {#manage-assets}

En este artículo se describe cómo administrar y editar recursos en Adobe Experience Manager Assets. Para administrar fragmentos de contenido, consulte [Fragmentos de contenido](content-fragments/content-fragments.md) recursos.

## Crear carpetas {#creating-folders}

Al organizar una colección de recursos, por ejemplo, todas las `Nature` imágenes, puede crear carpetas para mantenerlas juntas. Puede utilizar carpetas para categorizar y organizar los recursos. [!DNL Experience Manager Assets] no requiere que organice los recursos en carpetas para que funcionen mejor.

>[!NOTE]
>
>* No se puede compartir una carpeta de recursos del tipo `sling:OrderedFolder` al compartirla en Marketing Cloud. Si desea compartir una carpeta, no seleccione [!UICONTROL Pedido] al crear una carpeta.
>* El Experience Manager no permite utilizar la palabra `subassets` como nombre de una carpeta. Es una palabra clave reservada para nodos que contienen subrecursos para recursos compuestos


1. Vaya al lugar de la carpeta de recursos digitales en el que desea crear una nueva carpeta. En el menú, haga clic en **[!UICONTROL Crear]**. Seleccione **[!UICONTROL Nueva carpeta]**.
1. En el campo **[!UICONTROL Título]**, proporcione un nombre de carpeta. De forma predeterminada, DAM utiliza el título que ha proporcionado como nombre de carpeta. Una vez creada la carpeta, puede anular el valor predeterminado y especificar otro nombre de carpeta.
1. Haga clic en **[!UICONTROL Crear]**. La carpeta se muestra en la carpeta de recursos digitales.

No se admiten los siguientes caracteres (lista separada por espacios):

* Un nombre de archivo de recurso no puede contener ninguno de estos caracteres: `* / : [ \\ ] | # % { } ? &`
* El nombre de una carpeta de recursos no puede contener ninguno de estos caracteres: `* / : [ \\ ] | # % { } ? \" . ^ ; + & \t`

## Carga de recursos {#uploading-assets}

Consulte [adición de recursos digitales a Experience Manager](add-assets.md).

## Detectar recursos de duplicado {#detect-duplicate-assets}

<!-- TBD: This feature may not work as documented. See CQ-4283718. Get PM review done. -->

Si un usuario de DAM carga uno o más recursos que ya existen en el repositorio, [!DNL Experience Manager] detecta la duplicación y notifica al usuario. La detección de duplicados está deshabilitada de forma predeterminada, ya que puede afectar al rendimiento en función del tamaño del repositorio y del número de recursos cargados. Para habilitar la función, configure el [!UICONTROL detector de duplicación de recursos de Adobe AEM Cloud]. Consulte [cómo hacer las configuraciones de OSGi](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/configuring-osgi.html). La detección de duplicación se basa en el valor `dam:sha1` único almacenado en `jcr:content/metadata/dam:sha1`. Esto significa que los recursos de duplicado se detectan aunque los nombres de archivo sean diferentes.

![Detectar la configuración OSGi del recurso de duplicado](assets/duplicate-detection.png)

Puede agregar el archivo de configuración `/apps/example/config.author/com.adobe.cq.assetcompute.impl.assetprocessor.AssetDuplicationDetector.cfg.json` en el código personalizado y el archivo puede contener lo siguiente:

```json
{
  "enabled":true,
  "detectMetadataField":"dam:sha1"
}
```

Una vez habilitada, el Experience Manager envía notificaciones de los recursos de duplicado a la bandeja de entrada. Es un resultado agregado para varios duplicados. Los usuarios pueden elegir eliminar los recursos en función de los resultados.

![Notificación de bandeja de entrada para recursos de duplicado](assets/duplicate-detect-inbox-notification.png)

## Recursos de previsualización {#previewing-assets}

Para realizar la previsualización de un recurso, siga estos pasos.

1. En la interfaz de usuario de Recursos, navegue a la ubicación del recurso que desee previsualización.
1. Toque el recurso que desee para abrirlo.

1. En el modo de previsualización, las opciones de zoom están disponibles para [tipos de imagen admitidos](/help/assets/file-format-support.md) (con edición interactiva).

   Para acercar un recurso, toque o haga clic en `+` (o toque o haga clic en la lupa del recurso). Para alejar, toque o haga clic en `-`. Al acercar, puede ver con detenimiento cualquier área de la imagen. La flecha para restablecer el zoom le lleva de nuevo a la vista original.

   Toque **[!UICONTROL Restablecer]** para restablecer la vista al tamaño original.

## Editar propiedades {#editing-properties}

1. Navegue a la ubicación del recurso cuyos metadatos desee editar.

1. Seleccione el recurso y toque o haga clic en **[!UICONTROL Propiedades]** desde la barra de herramientas hasta las propiedades del recurso de vista. Como alternativa, elija la acción rápida **[!UICONTROL Propiedades]** en la tarjeta del recurso.

   ![properties_quickaction](assets/properties_quickaction.png)

1. En la página [!UICONTROL Propiedades], edite las propiedades de metadatos en varias fichas. Por ejemplo, en la ficha **[!UICONTROL Básico]**, edite el título, la descripción, etc.

   >[!NOTE]
   >
   >El diseño de la página [!UICONTROL Propiedades] y las propiedades de metadatos disponibles dependen del esquema de metadatos subyacente. Para obtener información sobre cómo modificar el diseño de la página [!UICONTROL Propiedades], consulte [Esquemas de metadatos](/help/assets/metadata-schemas.md).

1. Para programar una fecha y hora determinada para la activación del recurso, utilice el selector de fechas situado junto al campo **[!UICONTROL Tiempo de activación]**.

   ![chlimage_1-217](assets/chlimage_1-217.png)

1. Para desactivar el recurso después de una duración determinada, elija la fecha y hora de desactivación en el selector de fechas situado junto al campo **[!UICONTROL Tiempo de desactivación]**. La fecha de desactivación debe ser posterior a la fecha de activación de un recurso. Después del [!UICONTROL tiempo de inactividad], un recurso y sus representaciones no están disponibles ni a través de la interfaz web de Recursos ni a través de la API HTTP.

   ![chlimage_1-218](assets/chlimage_1-218.png)

1. En el campo **[!UICONTROL Etiquetas]**, seleccione una o varias etiquetas. Para agregar una etiqueta personalizada, escriba el nombre de la etiqueta en el cuadro y pulse la tecla Intro. La nueva etiqueta se guarda en [!DNL Experience Manager].

   YouTube requiere que las etiquetas publiquen y tengan un vínculo a YouTube (si se encuentra un vínculo adecuado).

   >[!NOTE]
   >
   >Para crear etiquetas, debe tener permiso de escritura en la ruta `/content/cq:tags/default` del repositorio de CRX.

1. Para vista de las estadísticas de uso del recurso, toque o haga clic en la ficha **[!UICONTROL Perspectivas]**.

   Las estadísticas de uso incluyen lo siguiente:

   * Número de veces que se ha visualizado o descargado el recurso
   * Canales/dispositivos a través de los cuales se utilizó el recurso
   * Soluciones creativas en las que el recurso se ha utilizado recientemente

   Para obtener más información, consulte [Perspectivas de recursos](assets-insights.md).

1. Toque o haga clic **[!UICONTROL Guardar y cerrar]**.

1. Vaya a la interfaz de usuario de Recursos. Las propiedades de metadatos editadas, incluido el título, la descripción y las etiquetas, se muestran en la tarjeta del recurso en la vista de tarjetas y en las columnas relevantes de la vista de Lista.

## Copiar recursos {#copying-assets}

Al copiar un recurso o una carpeta, se copia todo el recurso o la carpeta, junto con su estructura de contenido. Un recurso copiado o una carpeta se duplica en la ubicación del destinatario. El recurso en la ubicación de origen no se modifica.

Algunos atributos que son exclusivos de una copia concreta de un activo no se arrastran. Algunos ejemplos son:

* ID del recurso, fecha y hora de creación, y versiones e historial de versiones. Algunas de estas propiedades están indicadas por las propiedades `jcr:uuid`, `jcr:created` y `cq:name`.

* El tiempo de creación y las rutas a las que se hace referencia son únicos para cada recurso y cada una de sus representaciones.

El resto de las propiedades y la información de metadatos se conservan. No se crea una copia parcial al copiar un recurso.

1. En la interfaz de usuario de Recursos, seleccione uno o varios recursos y, a continuación, toque o haga clic en el icono **[!UICONTROL Copiar]** de la barra de herramientas. También puede seleccionar la acción rápida **[!UICONTROL Copiar]** ![copy_icon](assets/copy_icon.png) de la tarjeta del recurso.

   >[!NOTE]
   >
   >Si utiliza la acción rápida [!UICONTROL Copiar], sólo puede copiar un recurso a la vez.

1. Vaya a la ubicación en la que desea copiar los recursos.

   >[!NOTE]
   >
   >Si copia un recurso en la misma ubicación, [!DNL Experience Manager] genera automáticamente una variación del nombre. Por ejemplo, si copia un recurso titulado `Square`, [!DNL Experience Manager] genera automáticamente el título de su copia como `Square1`.

1. Haga clic en el icono **[!UICONTROL Pegar]** recurso de la barra de herramientas. Los recursos se copian en esta ubicación.

   ![chlimage_1-219](assets/chlimage_1-219.png)

   >[!NOTE]
   >
   >El icono **[!UICONTROL Pegar]** está disponible en la barra de herramientas hasta que se complete la operación de pegado.

### Mover o cambiar el nombre de los recursos {#moving-or-renaming-assets}

1. Navegue hasta la ubicación del recurso que desee mover.

1. Seleccione el recurso y toque o haga clic en el icono **[!UICONTROL Mover]** ![mover_icono](assets/move_icon.png) de la barra de herramientas.

1. En el asistente Mover recursos, realice una de las siguientes acciones:

   * Especifique el nombre del recurso después de moverlo. A continuación, toque o haga clic en **[!UICONTROL Siguiente]** para continuar.

   * Toque o haga clic **[!UICONTROL Cancelar]** para detener el proceso.
   >[!NOTE]
   >
   >* Puede especificar el mismo nombre para el recurso si no hay ningún recurso con ese nombre en la nueva ubicación. Sin embargo, debe utilizar un nombre diferente si mueve el recurso a una ubicación en la que exista un recurso con el mismo nombre. Si utiliza el mismo nombre, el sistema genera automáticamente una variación del nombre. Por ejemplo, si el recurso tiene el nombre Cuadrado, el sistema genera el nombre Cuadrado1 para su copia.
   >* Al cambiar el nombre, no se permiten espacios en blanco en el nombre del archivo.


1. En el cuadro de diálogo **[!UICONTROL Seleccionar destino]**, realice una de las siguientes acciones:

   * Vaya a la nueva ubicación de los recursos y, a continuación, toque o haga clic en **[!UICONTROL Siguiente]** para continuar.

   * Toque o haga clic **[!UICONTROL Atrás]** para volver a la pantalla **[!UICONTROL Cambiar nombre]**.

1. Si los recursos que se mueven tienen páginas, recursos o colecciones de referencia, la ficha **[!UICONTROL Ajustar referencias]** aparece junto a la ficha **[!UICONTROL Seleccionar destino]**.

   Realice una de las siguientes acciones en la pantalla **[!UICONTROL Ajustar referencias]**:

   * Especifique las referencias que se van a ajustar en función de los nuevos detalles y, a continuación, toque o haga clic **[!UICONTROL Mover]** para continuar.

   * En la columna **[!UICONTROL Ajustar]**, seleccione o anule la selección de referencias a los recursos.
   * Toque o haga clic **[!UICONTROL Atrás]** para volver a la pantalla **[!UICONTROL Seleccionar destino]**.

   * Toque o haga clic **[!UICONTROL Cancelar]** para detener la operación de movimiento.

   Si no actualiza las referencias, éstas seguirán apuntando a la ruta anterior del recurso. Si ajusta las referencias, se actualizan a la nueva ruta de acceso del recurso.

### Administrar representaciones {#managing-renditions}

1. Puede agregar o quitar representaciones de un recurso, excepto el original. Vaya a la ubicación del recurso para el que desea agregar o quitar representaciones.

1. Toque o haga clic en el recurso para abrir su página de recursos.

   ![chlimage_1-220](assets/chlimage_1-220.png)

1. Toque o haga clic en el icono de GlobalNav y seleccione **[!UICONTROL Representaciones]** en la lista.

   ![renditions_menu](assets/renditions_menu.png)

1. En el panel **[!UICONTROL Representaciones]**, vista la lista de las representaciones generadas para el recurso.

   ![renditions_panel](assets/renditions_panel.png)

   >[!NOTE]
   >
   >De forma predeterminada, [!DNL Experience Manager Assets] no muestra la representación original del recurso en el modo de previsualización. Si es administrador, puede utilizar las superposiciones para configurar [!DNL Assets] para mostrar las representaciones originales en el modo de previsualización.

1. Seleccione una representación para vista o eliminarla.

   **Eliminación de una representación**

   Seleccione una representación en el panel **[!UICONTROL Representaciones]** y, a continuación, toque o haga clic en el icono **[!UICONTROL Eliminar representación]** de la barra de herramientas. Las representaciones no se pueden eliminar de forma masiva una vez que se haya completado el procesamiento de recursos. Para recursos individuales, puede quitar las representaciones manualmente de la interfaz de usuario. Para varios recursos, puede personalizar [!DNL Experience Manager] para eliminar representaciones específicas o eliminar los recursos y volver a cargar los recursos eliminados.

   ![delete_renditionicon](assets/delete_renditionicon.png)

   **Carga de una nueva representación**

   Vaya a la página de detalles del recurso y pulse o haga clic en el icono **[!UICONTROL Agregar representación]** de la barra de herramientas para cargar una nueva representación para el recurso.

   ![chlimage_1-221](assets/chlimage_1-221.png)

   >[!NOTE]
   >
   >Si selecciona una representación en el panel **[!UICONTROL Representaciones]**, la barra de herramientas cambia de contexto y muestra solo las acciones que son relevantes para la representación. Las opciones, como el icono Cargar representación, no se muestran. Para ver estas opciones en la barra de herramientas, vaya a la página de detalles del recurso.

   Puede configurar las dimensiones de la representación que desee mostrar en la página de detalles de un recurso de vídeo o imagen. En función de las dimensiones que especifique, Recursos muestra la representación con las dimensiones exactas o más cercanas.

   Para configurar las dimensiones de representación de una imagen en el nivel de detalle del recurso, superponga el `renditionpicker` nodo (`libs/dam/gui/content/assets/assetpage/jcr:content/body/content/content/items/assetdetail/items/col1/items/assetview/renditionpicker`) y configure el valor de la propiedad de anchura. Configure el **[!UICONTROL tamaño de la propiedad (Long) en KB]** en lugar de la anchura para personalizar la representación en la página de detalles del recurso según el tamaño de la imagen. En el caso de la personalización basada en el tamaño, la propiedad `preferOriginal` asigna preferencia al original si el tamaño de la representación coincidente es mayor que el del original.

   Del mismo modo, puede personalizar la imagen de la página Anotación superponiendo `libs/dam/gui/content/assets/annotate/jcr:content/body/content/content/items/content/renditionpicker`.

   ![chlimage_1-222](assets/chlimage_1-222.png)

   Para configurar las dimensiones de representación de un recurso de vídeo, navegue hasta el nodo `videopicker` del repositorio de CRX en la ubicación `/libs/dam/gui/content/assets/assetpage/jcr:content/body/content/content/items/assetdetail/items/col1/items/assetview/videopicker`, superponga el nodo y, a continuación, edite la propiedad correspondiente.

   >[!NOTE]
   >
   >Las anotaciones de vídeo solo se admiten en navegadores con formatos de vídeo compatibles con HTML5. Además, según el navegador, se admiten diferentes formatos de vídeo.

## Eliminar recursos {#delete-assets}

Para resolver o eliminar las referencias entrantes de otras páginas, actualice las referencias relevantes antes de eliminar un recurso.

Asimismo, desactive el botón de forzar eliminación mediante una superposición para impedir que los usuarios eliminen los recursos a los que se hace referencia y dejen vínculos rotos.

1. Navegue a la ubicación de los recursos que desee eliminar.

1. Seleccione el recurso y toque o haga clic en el icono **[!UICONTROL Eliminar]** de la barra de herramientas.

   ![delete_icon](assets/delete_icon.png)

1. En el cuadro de diálogo de confirmación, haga clic en:

   * **** Cancelar para detener la acción
   * Seleccione **[!UICONTROL Eliminar]** para confirmar la acción:

      * Si el recurso no tiene referencias, se elimina.
      * Si el recurso tiene referencias, un mensaje de error le informa de que **Se hace referencia a uno o más recursos.** Puede seleccionar **[!UICONTROL Forzar eliminación]** o **[!UICONTROL Cancelar]**.

   >[!NOTE]
   >
   >Para poder eliminar un recurso, es necesario disponer de permisos de eliminación en la represa o el recurso. Si solo tiene permisos de modificación, solo puede editar los metadatos del recurso y agregar anotaciones al recurso. Sin embargo, no puede eliminar el recurso ni sus metadatos.

   >[!NOTE]
   >
   >Para resolver o eliminar las referencias entrantes de otras páginas, actualice las referencias relevantes antes de eliminar un recurso.
   >
   >
   >Asimismo, desactive el botón de forzar eliminación mediante una superposición para impedir que los usuarios eliminen los recursos a los que se hace referencia y dejen vínculos rotos.

## Descargar recursos {#download-assets}

Consulte [Descargar recursos de [!DNL Experience Manager]](/help/assets/download-assets-from-aem.md).

## Publicar recursos {#publish-assets}

<!--
>[!NOTE]
>
>For more information specific to Dynamic Media, see [Publishing Dynamic Media Assets.](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md)
-->

1. Vaya a la ubicación de los recursos o la carpeta que desee publicar.

1. Seleccione la acción rápida **[!UICONTROL Publicar]** en la tarjeta de recursos o seleccione el recurso y pulse o haga clic en el icono **[!UICONTROL Publicación rápida]** de la barra de herramientas.
1. Si el recurso hace referencia a otros recursos, sus referencias se enumeran en el asistente. Solo se muestran las referencias que no se han publicado o que se han modificado desde la última vez que se publicaron o no. Elija las referencias que desee publicar.

   ![chlimage_1-225](assets/chlimage_1-225.png)

   >[!NOTE]
   >
   >Si la carpeta que desea publicar incluye una carpeta vacía, la carpeta vacía no se publicará.

1. Toque o haga clic en **[!UICONTROL Publicar]** para confirmar la activación de los recursos.

>[!CAUTION]
>
>Si publica recursos que se están procesando, solo se publicará el contenido original. Faltan las representaciones. Espere a que se complete el procesamiento y, a continuación, publique o vuelva a publicar el recurso una vez finalizado el procesamiento.

## Cancelar la publicación de recursos {#unpublishing-assets}

1. Vaya a la ubicación de la carpeta de recursos o recursos que desea eliminar del entorno de publicación (cancelar la publicación).

1. Seleccione el recurso o la carpeta que desea cancelar la publicación y toque o haga clic en el icono **[!UICONTROL Administrar publicación]** de la barra de herramientas.

   ![manage_publication](assets/manage_publication.png)

1. Seleccione la acción **[!UICONTROL Cancelar publicación]** de la lista.

   ![unpublish_action](assets/unpublish_action.png)

1. Para cancelar la publicación del recurso posteriormente, seleccione **[!UICONTROL Cancelar la publicación posteriormente]** y, a continuación, seleccione una fecha para cancelar la publicación del recurso.
1. Programe una fecha para que el recurso no esté disponible desde el entorno de publicación.
1. Si el recurso hace referencia a otros recursos, elija las referencias que desee cancelar la publicación. Toque o haga clic en **[!UICONTROL Cancelar la publicación]**.
1. En el cuadro de diálogo de confirmación, toque o haga clic en:

   * **** Cancelar para detener la acción
   * **** Cancele la publicación para confirmar que los recursos se han cancelado de publicar (ya no están disponibles en el entorno de publicación) en la fecha especificada.

   >[!NOTE]
   >
   >Al cancelar la publicación de un recurso complejo, solo se debe cancelar la publicación del recurso. Evite cancelar la publicación de las referencias porque otros recursos publicados pueden hacer referencia a ellas.

## Grupo de usuarios cerrado {#closed-user-group}

Se utiliza un grupo de usuarios cerrado (CUG) para limitar el acceso a carpetas de recursos específicas publicadas desde [!DNL Experience Manager]. Si crea un CUG para una carpeta, el acceso a la carpeta (incluidos los recursos de carpetas y las subcarpetas) se restringirá únicamente a los miembros o grupos asignados. Para acceder a la carpeta, deben iniciar sesión con sus credenciales de seguridad.

Los CUG son una forma adicional de restringir el acceso a sus recursos. También puede configurar una página de inicio de sesión para la carpeta.

1. Seleccione una carpeta en la interfaz de usuario de Recursos y toque o haga clic en el icono Propiedades en la barra de herramientas para mostrar la página de propiedades.
1. En la ficha **[!UICONTROL Permisos]**, agregue miembros o grupos en **[!UICONTROL Grupo de usuarios cerrado]**.

   ![add_user](assets/add_user.png)

1. Para mostrar una pantalla de inicio de sesión cuando los usuarios acceden a la carpeta, seleccione la opción **[!UICONTROL Habilitar]**. A continuación, seleccione la ruta a una página de inicio de sesión en [!DNL Experience Manager] y guarde los cambios.

   ![login_page](assets/login_page.png)

   >[!NOTE]
   >
   >Si no especifica la ruta a una página de inicio de sesión, [!DNL Experience Manager] muestra la página de inicio de sesión predeterminada en la instancia de publicación.

1. Publique la carpeta e intente acceder a ella desde la instancia de publicación. Aparece una pantalla de inicio de sesión.
1. Si es miembro de CUG, introduzca sus credenciales de seguridad. La carpeta se muestra después de que [!DNL Experience Manager] le autentique.

## Buscar recursos {#search-assets}

La búsqueda de recursos es fundamental para el uso de un sistema de gestión de activos digitales, ya sea para su uso ulterior por parte de los creativos, para una gestión sólida de los recursos por parte de los usuarios y especialistas en marketing del negocio o para la administración por parte de los administradores de DAM.

Para realizar búsquedas simples, avanzadas y personalizadas con el fin de detectar y utilizar los recursos más adecuados, consulte [Buscar recursos en [!DNL Experience Manager]](/help/assets/search-assets.md).

## Acciones rápidas {#quick-actions}

Los iconos de acción rápida están disponibles para un único recurso a la vez. Según el dispositivo, realice las siguientes acciones para mostrar los iconos de acción rápida:

* Dispositivos táctiles: Tocar y aguantar. Por ejemplo, en un iPad, puede mantener pulsado un recurso para que se muestren las acciones rápidas.
* Dispositivos no táctiles: Pase el ratón por encima. Por ejemplo, en un dispositivo de escritorio, se muestra la barra de acciones rápidas si pasa el puntero sobre la miniatura del recurso.

## Editar imágenes {#editing-images}

Las herramientas de edición de la interfaz [!DNL Experience Manager Assets] le permiten realizar pequeños trabajos de edición en recursos de imagen. Puede recortar, rotar, voltear y realizar otros trabajos de edición en imágenes. También puede añadir mapas de imagen a los recursos.

>[!NOTE]
>
>Para algunos componentes, el modo de pantalla completa tiene opciones adicionales disponibles.

1. Realice una de las siguientes acciones para abrir un recurso en modo de edición:

   * Seleccione el recurso y toque o haga clic en el icono **[!UICONTROL Editar]** de la barra de herramientas.
   * Toque o haga clic en el icono **[!UICONTROL Editar]** que aparece en un recurso en la vista de tarjetas.
   * En la página de recursos, toque o haga clic en el icono **[!UICONTROL Editar]** de la barra de herramientas.

   ![edit_icon](assets/edit_icon.png)

1. Para recortar la imagen, toque o haga clic en el icono **Recortar**.

   ![chlimage_1-226](assets/chlimage_1-226.png)

1. Seleccione la opción que desee en la lista. El área de recorte aparece en la imagen según la opción elegida. La opción **Mano libre** permite recortar la imagen sin restricciones de proporción de aspecto.

   ![chlimage_1-227](assets/chlimage_1-227.png)

1. Seleccione el área que desea recortar y cambie su tamaño o posición en la imagen.
1. Utilice el icono **Finalizar** (esquina superior derecha) para recortar la imagen. Al hacer clic en el icono **Finalizar** también se desencadena la regeneración de las representaciones.

   ![chlimage_1-228](assets/chlimage_1-228.png)

1. Utilice los iconos **Deshacer** y **Rehacer** de la parte superior derecha para revertir a la imagen sin recortar o conservar la imagen recortada, respectivamente.

   ![chlimage_1-229](assets/chlimage_1-229.png)

1. Toque o haga clic en el icono Girar correspondiente para rotar la imagen en el sentido de las agujas del reloj o en el sentido contrario.

   ![chlimage_1-230](assets/chlimage_1-230.png)

1. Toque o haga clic en el icono Voltear correspondiente para voltear la imagen horizontal o verticalmente.

   ![chlimage_1-231](assets/chlimage_1-231.png)

1. Toque o haga clic en el icono **Finalizar** para guardar los cambios.

   ![chlimage_1-232](assets/chlimage_1-232.png)

>[!NOTE]
>
>La edición de imágenes es compatible con los formatos de archivos BMP, GIF, PNG y JPEG.

<!-- You can also add image maps using the image editor. For details, see [Adding Image Maps](/help/assets/image-maps.md). -->

>[!NOTE]
>
>Para editar un archivo TXT, configure **Day CQ Link Externalizer** desde Configuration Manager.

## Escala de tiempo {#timeline}

La línea de tiempo permite la vista de varios eventos para un elemento seleccionado, como flujos de trabajo activos para un recurso, comentarios/anotaciones, registros de actividades y versiones.

![Ordenar entradas de línea de tiempo para un ](assets/sort_timeline.gif)
*recursoFigura: Ordenar entradas de línea de tiempo para un recurso*

>[!NOTE]
>
>En la consola [Colecciones](/help/assets/manage-collections.md#navigate-the-collections-console), la lista **[!UICONTROL Mostrar todo]** proporciona opciones solo para flujos de trabajo y comentarios de vista. Además, la línea de tiempo solo se muestra para las colecciones de nivel superior que aparecen en la consola. No se muestra si se desplaza por alguna de las colecciones.

>[!NOTE]
>
>La línea de tiempo contiene varias [opciones específicas de los fragmentos de contenido](content-fragments/content-fragments.md).

## Anotaciones {#annotating}

Las anotaciones son comentarios o notas explicativas añadidas a imágenes o vídeos. Las anotaciones proporcionan a los especialistas en marketing la posibilidad de colaborar y dejar comentarios sobre los recursos.

Las anotaciones de vídeo solo se admiten en navegadores con formatos de vídeo compatibles con HTML5. Los formatos de vídeo compatibles con Assets dependen del navegador.

>[!NOTE]
>
>En Fragmentos de contenido, [las anotaciones se crean en el editor de fragmentos](content-fragments/content-fragments.md).

1. Navegue hasta la ubicación del recurso al que desee agregar anotaciones.
1. Toque o haga clic en el icono **[!UICONTROL Anotar]** de una de las siguientes maneras:

   * [Acciones rápidas](#quick-actions)
   * Desde la barra de herramientas después de seleccionar el recurso o de desplazarse a la página de recursos

   ![chlimage_1-233](assets/chlimage_1-233.png)

1. Agregue un comentario en el cuadro **[!UICONTROL Comentario]** de la parte inferior de la cronología. También puede marcar un área de la imagen y agregar una anotación en el cuadro de diálogo **[!UICONTROL Agregar anotación]**.

   ![chlimage_1-234](assets/chlimage_1-234.png)

<!--
1. To notify a user about an annotation, specify the email address of the user and add the comment. For example, to notify Aaron MacDonald about an annotation, enter @aa. Hints for all matching users is displayed in a list. Select Aaron's email address from the list to tag her with the comment. Similarly, you can tag more users anywhere within the annotation or before or after it.
-->

>[!NOTE]
>
>Para un usuario que no es administrador, las sugerencias solo aparecen si el usuario tiene permisos de lectura en `/home` en CRXDE.

![chlimage_1-235](assets/chlimage_1-235.png)

1. Después de agregar la anotación, haga clic en **[!UICONTROL Añadir]** para guardarla. Se envía una notificación para la anotación a Aaron.

   ![chlimage_1-236](assets/chlimage_1-236.png)

   >[!NOTE]
   >
   >Puede agregar varias anotaciones antes de guardarlas.

1. Toque o haga clic en **[!UICONTROL Cerrar]** para salir del modo de anotación.
1. Para vista de la notificación, inicie sesión en Recursos con las credenciales de Aaron MacDonald&#39;s y haga clic en el icono **[!UICONTROL Notificaciones]** para vista de la notificación.

   >[!NOTE]
   >
   >Las anotaciones también se pueden agregar a los recursos de vídeo. Al realizar anotaciones en vídeos, el reproductor se pausa para permitirle realizar anotaciones en un marco. Para obtener más información, consulte [administración de recursos de vídeo](manage-video-assets.md).

1. Para elegir un color diferente y diferenciarlo de los usuarios, toque o haga clic en el icono de Perfil y toque o haga clic en **[!UICONTROL Mis preferencias]**.

   ![chlimage_1-237](assets/chlimage_1-237.png)

   Especifique el color que desee en el cuadro **[!UICONTROL Color de anotación]** y pulse o haga clic en **[!UICONTROL Aceptar]**.

   ![chlimage_1-238](assets/chlimage_1-238.png)

>[!NOTE]
>
>También puede agregar anotaciones a una colección. Sin embargo, si una colección contiene colecciones secundarias, solo puede agregar anotaciones/comentarios a la colección principal. La opción Anotar no está disponible para colecciones secundarias.

### Anotaciones guardadas en vista {#viewing-saved-annotations}

1. Para vista de anotaciones guardadas para un recurso, vaya a la ubicación del recurso y abra la página del recurso.

1. Toque o haga clic en el icono de GlobalNav y elija **[!UICONTROL Línea de tiempo]** en la lista.

   ![chlimage_1-239](assets/chlimage_1-239.png)

1. En la lista **[!UICONTROL Mostrar todo]** de la cronología, seleccione **[!UICONTROL Comentarios]** para filtrar los resultados según las anotaciones.

   ![chlimage_1-240](assets/chlimage_1-240.png)

   Toque o haga clic en un comentario del panel **[!UICONTROL Línea de tiempo]** para vista de la anotación correspondiente en la imagen.

   ![chlimage_1-241](assets/chlimage_1-241.png)

   Toque o haga clic **[!UICONTROL Eliminar]** para eliminar un comentario en particular.

### Imprimir anotaciones {#printing-annotations}

Si un recurso tiene anotaciones o se ha sometido a un flujo de trabajo de revisión, puede imprimir el recurso junto con anotaciones y revisar el estado como archivo PDF para su revisión sin conexión.

También puede imprimir solo las anotaciones o el estado de la revisión.

Para imprimir las anotaciones y revisar el estado, toque o haga clic en el icono **[!UICONTROL Imprimir]** y siga las instrucciones del asistente. El icono **[!UICONTROL Imprimir]** aparece en la barra de herramientas solo cuando el recurso tiene al menos una anotación o estado de revisión asignado.

1. En la interfaz de usuario de Recursos, abra la página de previsualización de un recurso.
1. Realice una de las acciones siguientes:

   * Para imprimir todas las anotaciones y el estado de la revisión, omita el paso 3 y vaya directamente al paso 4.
   * Para imprimir anotaciones específicas y revisar el estado, abra la [línea de tiempo](/help/assets/manage-digital-assets.md#timeline) y luego vaya al paso 3.

1. Para imprimir anotaciones específicas, seleccione las anotaciones en la línea de tiempo.

   ![chlimage_1-242](assets/chlimage_1-242.png)

   Para imprimir solo el estado de la revisión, selecciónelo en la línea de tiempo.

   ![chlimage_1-243](assets/chlimage_1-243.png)

1. Toque o haga clic en el icono **[!UICONTROL Imprimir]** de la barra de herramientas.

   ![chlimage_1-244](assets/chlimage_1-244.png)

1. En el cuadro de diálogo Imprimir, elija la posición en la que desea que se muestre el estado de anotaciones/revisión en el PDF. Por ejemplo, si desea que las anotaciones o el estado se impriman en la parte superior derecha de la página que contiene la imagen impresa, utilice la configuración **Superior izquierda**. Se selecciona de forma predeterminada.

   ![chlimage_1-245](assets/chlimage_1-245.png)

   Puede elegir otros ajustes en función de la posición en la que desea que aparezcan las anotaciones o el estado en el PDF impreso. Si desea que las anotaciones o el estado aparezcan en una página independiente del recurso impreso, elija **[!UICONTROL Página siguiente]**.

   >[!NOTE]
   >
   >Es posible que las anotaciones largas no se representen correctamente en el archivo PDF. Para una representación óptima, Adobe recomienda limitar las anotaciones a 50 palabras.

1. Pulse o haga clic en **[!UICONTROL Imprimir]**. Según la opción elegida en el paso 2, el PDF generado muestra las anotaciones/el estado en la posición especificada. Por ejemplo, si elige imprimir las anotaciones y el estado de la revisión mediante la configuración **Superior izquierda**, la salida generada se parece al archivo PDF que se muestra aquí.

   ![chlimage_1-246](assets/chlimage_1-246.png)

1. Descargue o imprima el PDF con las opciones de la parte superior derecha.

   ![chlimage_1-248](assets/chlimage_1-247.png)

   Para modificar el aspecto del archivo PDF procesado, por ejemplo, el color de fuente, el tamaño y el estilo, el color de fondo de los comentarios y estados, abra la **[!UICONTROL configuración de PDF de anotación]** desde Configuration Manager y modifique las opciones deseadas. Por ejemplo, para cambiar el color de visualización del estado aprobado, modifique el código de color en el campo correspondiente. Para obtener información sobre cómo cambiar el color de fuente de las anotaciones, consulte [Anotación](/help/assets/manage-digital-assets.md#annotating).

   ![chlimage_1-247](assets/chlimage_1-248.png)

   Vuelva al archivo PDF procesado y actualícelo. El PDF actualizado refleja los cambios realizados.

## Versiones de recursos {#asset-versioning}

Al generar una versión se crea una instantánea de activos digitales en un punto específico en el tiempo. La creación de versiones ayuda a restaurar los recursos a un estado anterior posteriormente. Por ejemplo, si desea deshacer un cambio realizado en un recurso, restaure la versión sin editar del recurso.

A continuación se muestran los escenarios en los que se crean versiones:

* Puede modificar una imagen en una aplicación diferente y cargarla en Recursos. Se crea una versión de la imagen para que no se sobrescriba la imagen original.
* Los metadatos de un recurso se editan.
* La aplicación de escritorio [!DNL Experience Manager] se utiliza para retirar un recurso existente y guardar los cambios. Se crea una nueva versión cada vez que se guarda el recurso.

También puede activar el control automático de versiones mediante un flujo de trabajo. Al crear una versión para un recurso, los metadatos y las representaciones se guardan junto con la versión. Las representaciones son alternativas representadas de las mismas imágenes, por ejemplo, una representación PNG de un archivo JPEG cargado.

La funcionalidad de versiones le permite hacer lo siguiente:

* Cree una versión de un recurso.
* Vista de la revisión actual de un recurso.
* Restaure el recurso a una versión anterior.

1. Vaya a la ubicación del recurso para el que desea crear una versión y toque o haga clic en él para abrir su página de recursos.

1. Toque o haga clic en el icono de GlobalNav y elija **[!UICONTROL Línea de tiempo]** en el menú.

   ![línea de tiempo](assets/timeline.png)

1. Toque o haga clic en el icono **[!UICONTROL Acciones]** (flecha) en la parte inferior para vista de las acciones disponibles que puede realizar en el recurso.

   ![chlimage_1-249](assets/chlimage_1-249.png)

1. Toque o haga clic en **[!UICONTROL Guardar como versión]** para crear una versión para el recurso.

   ![chlimage_1-250](assets/chlimage_1-250.png)

1. Añada una etiqueta y un comentario y, a continuación, haga clic en **[!UICONTROL Crear]** para crear una versión. O bien, toque o haga clic en **Cancelar** para salir de la operación.

   ![chlimage_1-251](assets/chlimage_1-251.png)

1. Para ver la nueva versión, abra la lista **[!UICONTROL Mostrar todo]** en la cronología de la página de detalles de recursos o de la interfaz de usuario de recursos y elija **[!UICONTROL Versiones]**. Todas las versiones creadas para un recurso se muestran en la pestaña de cronología. Puede filtrar la lista para mostrar Versiones, haciendo clic en la flecha de colocación y seleccionando **[!UICONTROL Versiones]** en la lista.

   ![versions_option](assets/versions_option.png)

1. Seleccione una versión específica para el recurso para realizar la previsualización o habilite su aparición en la interfaz de usuario de Recursos.

   ![select_version](assets/select_version.png)

1. Añada una etiqueta y un comentario para que la versión vuelva a la versión concreta de la interfaz de usuario de Recursos.

   ![save_version](assets/save_version.png)

1. Para generar una vista previa de la versión, pulse o haga clic en **[!UICONTROL Vista previa de la versión]**.
1. Para mostrar esta versión en la interfaz de usuario de Assets, seleccione **[!UICONTROL Revertir a esta versión]**.
1. Para comparar dos versiones, vaya a la página de recursos del recurso y toque o haga clic en la versión que se va a comparar con la versión actual.

   ![select_version_tocompare](assets/select_version_tocompare.png)

1. En la línea de tiempo, seleccione la versión que desee comparar y arrastre el deslizador hacia la izquierda para superponer esta versión sobre la versión actual y comparar.

   ![compare_versions](assets/compare_versions.png)

### Iniciar un flujo de trabajo en un recurso {#starting-a-workflow-on-an-asset}

1. Vaya a la ubicación del recurso para el que desea realizar el inicio de un flujo de trabajo y toque o haga clic en él para abrir la página del recurso.
1. Toque o haga clic en el icono de GlobalNav y elija **[!UICONTROL Línea de tiempo]** en el menú para mostrar la línea de tiempo.

   ![línea de tiempo-1](assets/timeline-1.png)

1. Toque o haga clic en el icono **[!UICONTROL Acciones]** (flecha) en la parte inferior para abrir la lista de acciones disponibles para el recurso.

   ![chlimage_1-252](assets/chlimage_1-252.png)

1. Toque o haga clic en **[!UICONTROL Flujo de trabajo de Inicio]** desde la lista.

   ![chlimage_1-253](assets/chlimage_1-253.png)

1. En el cuadro de diálogo **[!UICONTROL Flujo de trabajo de Inicio]**, seleccione un modelo de flujo de trabajo de la lista.

   ![chlimage_1-254](assets/chlimage_1-254.png)

1. (Opcional) Especifique un título para el flujo de trabajo, que se puede utilizar para hacer referencia a la instancia de flujo de trabajo.

   ![chlimage_1-255](assets/chlimage_1-255.png)

1. Pulse o haga clic en **[!UICONTROL Iniciar]** y, a continuación, pulse o haga clic en **[!UICONTROL Continuar]** en el cuadro de diálogo para confirmar. Cada paso del flujo de trabajo se muestra en la cronología como un evento.

   ![chlimage_1-256](assets/chlimage_1-256.png)

## Colecciones {#collections}

Una colección es un conjunto ordenado de recursos. Utilice colecciones para compartir recursos entre usuarios.

* Una colección puede incluir recursos de distintas ubicaciones porque solo contienen referencias a estos recursos. Cada colección mantiene la integridad referencial de los recursos.
* Puede compartir colecciones con varios usuarios con diferentes niveles de privilegios, como edición, visualización, etc.

Consulte [Administración de colecciones](/help/assets/manage-collections.md) para obtener más información sobre la administración de colecciones.
