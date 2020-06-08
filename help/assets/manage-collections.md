---
title: Gestión de colecciones de recursos digitales
description: Comprenda el concepto de la colección en Recursos Adobe Experience Manager. Aprenda a recopilar, administrar, editar y recopilar con otros usuarios.
contentOwner: AG
mini-toc-levels: 1
translation-type: tm+mt
source-git-commit: 26833f59f21efa4de33969b7ae2e782fe5db8a14
workflow-type: tm+mt
source-wordcount: '2381'
ht-degree: 20%

---


# Administrar colecciones {#manage-collections}

Una colección es un conjunto de recursos dentro de Recursos Adobe Experience Manager. Utilice colecciones para compartir recursos entre usuarios. El conjunto puede ser una colección estática o una colección dinámica basada en los resultados de la búsqueda.

A diferencia de las carpetas, una colección puede incluir recursos de distintas ubicaciones. Puede compartir colecciones con varios usuarios a los que se han asignado diferentes niveles de privilegios, como ver, editar, etc.

Puede compartir varias colecciones con un usuario. Cada colección contiene referencias a recursos. La integridad referencial de los recursos se mantiene en todas las colecciones.

Las colecciones son de los siguientes tipos, según la forma en que recopilan los recursos:

* Colección que contiene una lista de referencia estática de recursos, carpetas y otras colecciones.

* Colección inteligente que incluye de forma dinámica recursos basados en criterios de búsqueda.

## Acceso a la consola de colecciones {#navigate-the-collections-console}

Para abrir la consola **[!UICONTROL Colecciones]** :

Para abrir las **[!UICONTROL colecciones]**, toque o haga clic en el logotipo de Experience Manager. From the navigation page, go to **[!UICONTROL Assets]** > **[!UICONTROL Collections]**.

## Creación de una colección {#create-a-collection}

Puede crear una colección con referencias [](#create-a-collection-with-static-references) estáticas o basada en un filtro [basado en criterios de](#create-a-smart-collection)búsqueda. También puede crear una colección a partir de una caja de iluminación.

### Creación de una colección con referencias estáticas {#create-a-collection-with-static-references}

Puede crear una colección con referencias estáticas, por ejemplo, una colección con referencias a recursos, carpetas, colecciones, conjuntos de giros y conjuntos de imágenes.

1. Vaya a la consola **[!UICONTROL Colecciones]** .
1. En la barra de herramientas, toque o haga clic en **[!UICONTROL Crear]**.
1. En la página **[!UICONTROL Crear colección]** , introduzca un título y una descripción opcional para la colección.
1. Agregue miembros a la colección y asigne los permisos correspondientes. Como alternativa, seleccione **[!UICONTROL Colección pública]** para permitir que todos los usuarios tengan acceso a la colección.

   >[!NOTE]
   >
   >Para permitir que los miembros compartan colecciones con otros usuarios, proporcione los permisos de lectura del `dam-users` grupo en la ruta `home/users`. Otorgue permiso a los usuarios en la `/content/dam/collections` ubicación para permitir que los usuarios realicen la vista de las colecciones en listas emergentes. Como alternativa, haga que el usuario forme parte del `dam-users` grupo.

1. (Opcional) Añada una imagen en miniatura para la colección.
1. Toque o haga clic en **[!UICONTROL Crear]** y, a continuación, pulse o haga clic en **[!UICONTROL Aceptar]** para cerrar el cuadro de diálogo. En la consola Colecciones se abre una colección con el título y las propiedades especificados.

   >[!NOTE]
   >
   >Experience Manager Assets permite crear tareas de revisión para una colección de forma similar a como se crean tareas de revisión para una carpeta de recursos.

   Para añadir recursos a la colección, vaya a la interfaz de usuario de Recursos. Para obtener más información, consulte [Añadir recursos en una colección](#add-assets-to-a-collection).

### Creación de colecciones mediante dropzone {#create-collections-using-dropzone}

Puede arrastrar recursos de la interfaz de usuario de Recursos a una colección. También puede crear una copia de una colección y arrastrar los recursos allí.

1. En la interfaz de usuario de Recursos, seleccione los recursos que desee agregar a una colección.
1. Arrastre los recursos a la zona **[!UICONTROL Colocar en colección]** . O bien, toque o haga clic en el icono **[!UICONTROL A colección]** de la barra de herramientas.
1. En la página **[!UICONTROL Agregar a la colección]**, pulse o haga clic en el icono **[!UICONTROL Crear colección]** de la barra de herramientas. Si desea agregar los recursos a una colección existente, selecciónela en la página y pulse o haga clic en **[!UICONTROL Agregar]**. De forma predeterminada, se selecciona la colección con la fecha de actualización más reciente.
1. En el cuadro de diálogo **[!UICONTROL Crear nueva colección]**, indique un nombre para la colección. Si desea que todos los usuarios tengan acceso a la colección, seleccione **[!UICONTROL Colección pública]**.
1. Toque o haga clic en **[!UICONTROL Continuar]** para crear la colección.

### Creación de una colección inteligente {#create-a-smart-collection}

Una colección inteligente utiliza criterios de búsqueda para rellenar recursos de forma dinámica. Puede crear una colección inteligente utilizando solo archivos y no carpetas o archivos y carpetas.

1. Vaya a la interfaz de usuario de Assets y pulse o haga clic en el icono **[!UICONTROL Buscar]**.
1. Escriba la palabra clave de búsqueda en el cuadro de búsqueda Omni y pulse Intro. Toque o haga clic en el icono de GlobalNav para mostrar el panel Filtros y aplicar un filtro de búsqueda desde el panel Buscar.
1. En la lista **[!UICONTROL Archivos y carpetas]** , seleccione **[!UICONTROL Archivos]**.
1. Toque o haga clic en **[!UICONTROL Guardar colección]** inteligente.
1. Especifique un nombre para la colección. Seleccione **[!UICONTROL Público]** para agregar el grupo Usuarios de DAM con la función Visor a la colección inteligente.

   >[!NOTE]
   >
   >Si selecciona **[!UICONTROL Público]**, la colección inteligente estará disponible para todos los usuarios con la función Propietario después de crearla. Si anula la selección de la opción **[!UICONTROL Público]** , el grupo de usuarios DAM ya no estará asociado a la colección inteligente.

1. Pulse o haga clic en **[!UICONTROL Guardar]** para crear la colección inteligente y, a continuación, cierre el cuadro de mensaje para completar el proceso. La nueva colección inteligente también se agrega a la lista **[!UICONTROL Búsquedas guardadas]**..
La etiqueta del botón **[!UICONTROL Crear selección inteligente]** cambia a **[!UICONTROL Editar selección inteligente]**. Para editar la configuración de la colección inteligente, seleccione **[!UICONTROL Archivos]** en la lista **[!UICONTROL Archivos y carpetas]**. A continuación, pulse o haga clic en el botón **[!UICONTROL Editar selección inteligente]**.

## Añadir recursos en una colección {#add-assets-to-a-collection}

Puede agregar recursos a una colección que contenga una lista de los recursos o carpetas a los que se hace referencia.

>[!NOTE]
>
>Las colecciones inteligentes utilizan una consulta de búsqueda para rellenar los recursos. Por lo tanto, las referencias estáticas a recursos y carpetas no son aplicables a ellos.

1. En la interfaz de usuario de Recursos, navegue a la ubicación del recurso que desee agregar a una colección.
1. Seleccione el recurso y toque o haga clic en el icono **[!UICONTROL A colección]** de la barra de herramientas. También puede arrastrar el recurso a la zona **[!UICONTROL Colocar en colección]** . Suelte el botón del ratón cuando la zona de colocación se active y su etiqueta cambie a **[!UICONTROL Colocar para Añadir]**.
1. En la página **[!UICONTROL Añadir a colección]** , seleccione la colección a la que desea agregar el recurso.
1. Toque o haga clic en **[!UICONTROL Añadir]** y, a continuación, cierre el mensaje de confirmación. El recurso se agrega a la colección.

## Edición de una colección inteligente {#edit-a-smart-collection}

Las colecciones inteligentes se crean al guardar una búsqueda para que pueda modificar su contenido modificando los parámetros de búsqueda de la búsqueda [](#saved-searches)guardada.

1. En la interfaz de usuario de Recursos, toque o haga clic en el icono **[!UICONTROL Buscar]** de la barra de herramientas.
1. Con el cursor en el cuadro Omniture search, presione la tecla Intro.
1. Toque o haga clic en el icono de GlobalNav para mostrar el panel Filtros.
1. En la lista **[!UICONTROL Búsquedas guardadas]**, seleccione la colección inteligente que desee modificar. El panel Buscar aparecen los filtros configurados para la búsqueda guardada.
1. En la lista **[!UICONTROL Archivos y carpetas]** , seleccione **[!UICONTROL Archivos]**.
1. Modifique uno o varios filtros, según sea necesario. Toque o haga clic en **[!UICONTROL Editar colección]** inteligente. También puede editar el nombre de la colección inteligente.
1. Tap/click **[!UICONTROL Save]**. Aparecerá el cuadro de diálogo **[!UICONTROL Editar colección]** inteligente.
1. Toque o haga clic en **[!UICONTROL Sobrescribir]** para reemplazar la colección inteligente original por la colección editada. También puede seleccionar **[!UICONTROL Guardar como]** para guardar la colección editada por separado.
1. En el cuadro de diálogo de confirmación, toque o haga clic en **[!UICONTROL Guardar]** para completar el proceso.

## Vista y edición de metadatos de la colección {#view-and-edit-collection-metadata}

Los metadatos de la colección incluyen datos sobre la colección, incluidas las etiquetas que se agreguen.

1. En la consola Colecciones, seleccione una colección y toque o haga clic en el icono **[!UICONTROL Propiedades]** de la barra de herramientas.
1. En la página **[!UICONTROL Metadatos de la colección]**, consulte los metadatos de la colección desde las pestañas **[!UICONTROL Básico]** y **Avanzado**.
1. Modifique los metadatos según sea necesario y, a continuación, toque o haga clic en **[!UICONTROL Guardar y cerrar]** en la barra de herramientas para guardar los cambios.

### Editar metadatos de la colección de forma masiva {#edit-collection-metadata-in-bulk}

Puede editar los metadatos de varias colecciones simultáneamente. Esta funcionalidad le ayuda a replicar rápidamente metadatos comunes en varias colecciones.

1. En la consola Colecciones, seleccione dos o más colecciones para las que desee editar los metadatos.
1. En la barra de herramientas, toque o haga clic en el icono **[!UICONTROL Propiedades]** .
1. En la página **[!UICONTROL Metadatos de la colección]**, edite los metadatos en las pestañas **[!UICONTROL Básico]** y **[!UICONTROL Avanzado]**, según sea necesario.
1. Toque o haga clic en **[!UICONTROL Guardar y cerrar]** desde la barra de herramientas y, a continuación, cierre el cuadro de diálogo de confirmación para completar el proceso.
1. Para anexar los nuevos metadatos con los metadatos existentes, seleccione el modo **[!UICONTROL Anexar]**. Si no selecciona esta opción, los metadatos nuevos sustituirán a los metadatos existentes en los campos. Pulse o haga clic en **[!UICONTROL Enviar]**.

   >[!NOTE]
   >
   >El modo Anexar solo funciona para campos que pueden contener varios valores. Para los campos que pueden contener un solo valor, los nuevos metadatos no se anexan al valor existente en el campo aunque seleccione el modo **[!UICONTROL Anexar]**.

## Búsqueda {#searching}

La función de búsqueda dentro de las colecciones admite tanto la [búsqueda de colecciones](#search-collections) como la [búsqueda de recursos dentro de una colección](#search-within-collections).

### Buscar colecciones {#search-collections}

Puede buscar colecciones desde la consola Colecciones. Al buscar palabras clave en el cuadro de búsqueda de Omniture, Recursos AEM busca los nombres de las colecciones, los metadatos y las etiquetas agregadas a las colecciones.

Si busca colecciones desde el nivel superior, solo se devuelven colecciones individuales en los resultados de búsqueda. Se excluyen los recursos o las carpetas de las colecciones. En todos los demás casos (por ejemplo, dentro de una colección individual o en una jerarquía de carpetas), se devuelven todos los recursos, carpetas y colecciones relevantes.

### Buscar en colecciones {#search-within-collections}

En la consola Colecciones, toque o haga clic en una colección para abrirla.

Dentro de una colección, la búsqueda de recursos de AEM está restringida a los recursos (y sus etiquetas y metadatos) dentro de la colección que está viendo. Al buscar dentro de una carpeta, se devuelven todos los recursos y las carpetas secundarias que coinciden con la carpeta actual. Al buscar dentro de una colección, solo se devuelven los recursos, las carpetas y otras colecciones que coinciden con los miembros directos de la colección.

## Editar la configuración de la colección {#edit-collection-settings}

Puede editar la configuración de la colección, como título y descripción, o bien añadir miembros a una colección.

1. Seleccione una colección y toque o haga clic en el icono **[!UICONTROL Configuración]** de la barra de herramientas. También puede utilizar la acción rápida **[!UICONTROL Configuración]** de la miniatura de la colección.
1. Modifique la configuración de la colección en la página **[!UICONTROL Configuración de la colección]**. Por ejemplo, modifique el título de la colección, las descripciones, los miembros y los permisos tal como se describe en [Agregar colecciones](#create-a-collection).
1. Tap/click **[!UICONTROL Save]** to save the changes.

## Eliminar una colección {#delete-a-collection}

1. En la consola Colecciones, seleccione una o varias colecciones y toque o haga clic en el icono Eliminar de la barra de herramientas.
1. En el cuadro de diálogo, toque o haga clic en **[!UICONTROL Eliminar]** para confirmar la acción de eliminación.

   >[!NOTE]
   >
   >También puede eliminar colecciones inteligentes [eliminando las búsquedas](#saved-searches)guardadas.

## Descargar una colección {#download-a-collection}

Al descargar una colección, se descarga toda la jerarquía de recursos de la colección, incluidas las carpetas y las colecciones secundarias.

1. En la consola Colecciones, seleccione una o varias colecciones para descargar.
1. En la barra de herramientas, toque o haga clic en el icono de descarga.
1. En el cuadro de diálogo **[!UICONTROL Descargar]** , toque o haga clic en **[!UICONTROL Descargar]**. Si desea descargar las representaciones de los recursos de la colección, seleccione **[!UICONTROL Representaciones]**. <!-- Select the **[!UICONTROL Email]** option to send an email notification to the owner of the collection. -->

   Cuando selecciona una colección para descargar, se descarga la jerarquía completa de carpetas bajo la colección. Para incluir cada colección que descargue (incluidos los recursos de las colecciones secundarias anidadas en la colección principal) en una carpeta individual, seleccione **[!UICONTROL Crear una carpeta independiente para cada recurso]**.

## Editar propiedades de metadatos de varias colecciones {#editing-metadata-properties-of-multiple-collections}

Recursos Adobe Enterprise Manager (AEM) le permite editar de forma masiva los metadatos de muchas colecciones. Utilice la página [!UICONTROL Propiedades] para realizar cambios en los metadatos de varias colecciones, por ejemplo, cambiar las propiedades de los metadatos a un valor común o agregar o modificar etiquetas.

Para personalizar la página de [!UICONTROL propiedades] de metadatos, incluida la adición, modificación y eliminación de propiedades de metadatos, utilice el editor de Esquema.

>[!NOTE]
>
>Los métodos de edición masiva funcionan para los recursos disponibles en una colección. En el caso de los recursos disponibles en varias carpetas o que cumplen un criterio común, es posible actualizar [masivamente los metadatos después de realizar la búsqueda](/help/assets/search-assets.md#metadataupdates).

1. En la consola de colecciones, seleccione las colecciones que desee editar.
1. En la barra de herramientas, toque o haga clic en **[!UICONTROL Propiedades]** para abrir la página [!UICONTROL Propiedades] de las colecciones seleccionadas.
1. Modifique las propiedades de metadatos de las colecciones seleccionadas en las distintas fichas.

   >[!NOTE]
   >
   >Los metadatos que se agregan para las colecciones seleccionadas sobrescriben los metadatos anteriores para estas colecciones, excepto para las etiquetas. Las etiquetas que agregue al campo **[!UICONTROL Etiquetas]** se anexan a la lista de etiquetas existente en los metadatos.

1. Para vista de las propiedades de metadatos de una colección específica, anule la selección de las colecciones restantes de la lista de colecciones. Los campos del editor de metadatos se rellenan con los metadatos de la colección en particular.

   >[!NOTE]
   >
   >* En la página de propiedades de la colección, puede quitar colecciones de la lista de colecciones anulándolas. La lista de colecciones tiene todas las colecciones seleccionadas de forma predeterminada. Los metadatos de las colecciones que elimine no se actualizarán.
   >* En la parte superior de la lista, active la casilla de verificación situada junto a **[!UICONTROL Título]** para alternar entre seleccionar las colecciones y borrar la lista.


1. Guarde los cambios.

## Crear colecciones anidadas {#create-nested-collections}

Puede agregar una colección a otra colección, creando así una colección anidada.

1. En la consola Colecciones, seleccione la colección o el grupo de colecciones que desee y toque o haga clic en **[!UICONTROL A colección]** en la barra de herramientas.
1. En la página **[!UICONTROL Añadir a colección]** , seleccione la colección en la que desea agregar la colección.

   >[!NOTE]
   >
   >La colección actualizada más recientemente se selecciona de forma predeterminada en la página **[!UICONTROL Añadir a colección]** .

1. Toque o haga clic en **[!UICONTROL Añadir]**. Un mensaje confirma que la colección se agrega a la colección de destinatarios en la página **[!UICONTROL Seleccionar destino]** . Cierre el mensaje para completar el proceso.

>[!NOTE]
>
>Las colecciones inteligentes no se pueden anidar. En otras palabras, las colecciones inteligentes no pueden contener ninguna otra colección.

## Búsquedas guardadas {#saved-searches}

En la interfaz de usuario de Assets, puede buscar o filtrar recursos en función de determinadas reglas, criterios de búsqueda o facetas de búsqueda personalizadas. Si los guarda como **[!UICONTROL Búsquedas guardadas]**, puede acceder a ellos más adelante desde la lista **[!UICONTROL Búsquedas guardadas]** del panel Filtro. Al crear una búsqueda guardada también se crea una colección inteligente.

Las búsquedas guardadas se crean al crear una colección inteligente. Las colecciones inteligentes se agregan automáticamente a la lista **[!UICONTROL Búsquedas guardadas]**. La consulta Búsquedas guardadas para la colección se guarda en la `dam:query`propiedad de CRXDE en la ubicación relativa`/content/dam/collections/`.

>[!NOTE]
>
>Puede compartir colecciones inteligentes del mismo modo que comparte colecciones estáticas.

Editar búsquedas guardadas es lo mismo que editar colecciones inteligentes. Para obtener más información, consulte [Edición de una colección](#edit-a-smart-collection)inteligente.

Para eliminar las búsquedas guardadas, siga estos pasos:

1. En la interfaz de usuario de Recursos, toque o haga clic en el icono de búsqueda de la barra de herramientas.

1. Con el cursor en el campo Omniture search, presione la tecla Intro.
1. Toque o haga clic en el icono de GlobalNav para mostrar el panel Filtros.
1. En la lista **[!UICONTROL Búsquedas guardadas]**, pulse o haga clic en **[!UICONTROL Eliminar]** al lado de la colección inteligente que desee eliminar.
1. En el cuadro de diálogo, toque o haga clic en **[!UICONTROL Eliminar]** para eliminar la búsqueda guardada.

## Ejecución de un flujo de trabajo en una colección {#run-a-workflow-on-a-collection}

Puede ejecutar un flujo de trabajo para los recursos de una colección. Si la colección contiene colecciones anidadas, el flujo de trabajo también se ejecuta en los recursos de las colecciones anidadas. Sin embargo, si la colección y la colección anidada contienen recursos de duplicado, el flujo de trabajo solo se ejecuta una vez para dichos recursos.

1. En la consola Colecciones, seleccione una colección en la que desee ejecutar un flujo de trabajo.
1. Toque o haga clic en el icono de GlobalNav y elija **[!UICONTROL Cronología]** en la lista.
1. En la cronología, pulse o haga clic en el icono del circunflejo invertido en la parte inferior y, a continuación, pulse o haga clic en **[!UICONTROL Iniciar flujo de trabajo]**.
1. En la sección **[!UICONTROL Iniciar flujo de trabajo]**, seleccione un modelo de flujo de trabajo de la lista. Por ejemplo, seleccione el modelo **[!UICONTROL Recurso de actualización DAM]**.
1. Introduzca un título para el flujo de trabajo y toque o haga clic en **[!UICONTROL Inicio]**.
1. En el cuadro de diálogo, toque o haga clic en **[!UICONTROL Continuar]**. El flujo de trabajo se ejecuta en todos los recursos de la colección.

>[!MORELIKETHIS]
>
>* [Crear una tarea de revisión para colecciones](/help/assets/bulk-approval.md)

