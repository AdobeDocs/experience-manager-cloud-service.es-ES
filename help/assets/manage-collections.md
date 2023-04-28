---
title: Administrar colecciones de recursos digitales
description: Comprenda el concepto de colección en Adobe Experience Manager Assets. Aprenda a recopilar, administrar, editar y recopilar con otros usuarios.
contentOwner: AG
mini-toc-levels: 1
feature: Collections,Asset Management
role: User
exl-id: b0798adc-56a4-4577-b4ee-8d1fca3bff09
source-git-commit: 8bdd89f0be5fe7c9d4f6ba891d7d108286f823bb
workflow-type: tm+mt
source-wordcount: '2425'
ht-degree: 22%

---

# Administrar colecciones {#manage-collections}

Una colección es un conjunto de recursos dentro de Adobe Experience Manager Assets. Utilice las colecciones para compartir recursos entre los usuarios. El conjunto puede ser una colección estática o una colección dinámica basada en los resultados de la búsqueda.

A diferencia de las carpetas, una colección puede incluir recursos de distintas ubicaciones. Puede compartir colecciones con varios usuarios a los que se asignan distintos niveles de privilegios, como ver, editar, etc.

Puede compartir varias colecciones con un usuario. Cada colección contiene referencias a recursos. La integridad referencial de los recursos se mantiene entre colecciones.

Las colecciones son de los siguientes tipos, según la forma en que recopilan los recursos:

* Colección que contiene una lista de referencia estática de recursos, carpetas y otras colecciones.

* Colección inteligente que incluye recursos de forma dinámica en función de criterios de búsqueda.

## Acceso a la consola de colecciones {#navigate-the-collections-console}

Para abrir el **[!UICONTROL Colecciones]** consola:

Para abrir el **[!UICONTROL Colecciones]**, pulse o haga clic en el logotipo del Experience Manager. Desde la página de navegación, vaya a **[!UICONTROL Recursos]** > **[!UICONTROL Colecciones]**.

## Crear una colección {#create-a-collection}

Puede crear una colección con [referencias estáticas](#create-a-collection-with-static-references) o en función de un [filtro basado en criterios de búsqueda](#create-a-smart-collection). También puede crear una colección a partir de un lightbox.

### Crear una colección con referencias estáticas {#create-a-collection-with-static-references}

Puede crear una colección con referencias estáticas, por ejemplo, una colección con referencias a recursos, carpetas, colecciones, conjuntos de giros y conjuntos de imágenes.

1. Vaya a la **[!UICONTROL Colecciones]** consola.
1. En la barra de herramientas, toque o haga clic en **[!UICONTROL Crear]**.
1. En el **[!UICONTROL Crear colección]** , introduzca un título y una descripción opcional para la colección.
1. Agregue miembros a la colección y asigne los permisos correspondientes. Como alternativa, seleccione **[!UICONTROL Colección pública]** para permitir que todos los usuarios tengan acceso a la colección.

   >[!NOTE]
   >
   >Para permitir que los miembros compartan colecciones con otros usuarios, proporcione la variable `dam-users` permisos de lectura de grupo en la ruta `home/users`. Permita a los usuarios en `/content/dam/collections` ubicación para permitir a los usuarios ver las colecciones en listas emergentes. También puede convertir al usuario en parte de `dam-users` grupo.

1. (Opcional) Agregue una imagen en miniatura para la colección.
1. Toque o haga clic en **[!UICONTROL Crear]** y, a continuación, pulse o haga clic en **[!UICONTROL Aceptar]** para cerrar el cuadro de diálogo. En la consola Colecciones se abre una colección con el título y las propiedades especificados.

   >[!NOTE]
   >
   >Experience Manager Assets permite crear tareas de revisión para una colección de forma similar a como se crean tareas de revisión para una carpeta de recursos.

   Para añadir recursos a la colección, vaya a la interfaz de usuario de Assets. Para obtener más información, consulte [Agregar recursos a una colección](#add-assets-to-a-collection).

### Crear colecciones mediante dropzone {#create-collections-using-dropzone}

Puede arrastrar recursos de la interfaz de usuario de Assets a una colección. También puede crear una copia de una colección y arrastrar los recursos allí.

1. En la interfaz de usuario de Assets, seleccione los recursos que desea agregar a una colección.
1. Arrastre los recursos a la **[!UICONTROL Colocar una colección]** zona. Como alternativa, toque o haga clic en el botón **[!UICONTROL A la colección]** de la barra de herramientas.
1. En la página **[!UICONTROL Agregar a la colección]**, pulse o haga clic en el icono **[!UICONTROL Crear colección]** de la barra de herramientas. Si desea agregar los recursos a una colección existente, selecciónela en la página y pulse o haga clic en **[!UICONTROL Agregar]**. De forma predeterminada, se selecciona la colección con la fecha de actualización más reciente.
1. En el cuadro de diálogo **[!UICONTROL Crear nueva colección]**, indique un nombre para la colección. Si desea que todos los usuarios tengan acceso a la colección, seleccione **[!UICONTROL Colección pública]**.
1. Toque o haga clic **[!UICONTROL Continuar]** para crear la colección.

### Crear una colección inteligente {#create-a-smart-collection}

Una colección inteligente usa criterios de búsqueda para rellenar recursos de forma dinámica. Puede crear una colección inteligente utilizando solo archivos y no carpetas o archivos y carpetas.

1. Vaya a la interfaz de usuario de Assets y pulse o haga clic en el icono **[!UICONTROL Buscar]**.
1. Introduzca la palabra clave de búsqueda en el cuadro de búsqueda Omni y seleccione `Enter`. Toque o haga clic en el icono de navegación global para mostrar el panel Filtros y aplicar un filtro de búsqueda desde el panel Buscar .
1. En el **[!UICONTROL Archivos y carpetas]** lista, seleccionar **[!UICONTROL Archivos]**.
1. Toque o haga clic **[!UICONTROL Guardar colecciones inteligentes]**.
1. Especifique un nombre para la colección. Select **[!UICONTROL Público]** para agregar el grupo Usuarios de DAM con la función Visualizador a la colección inteligente.

   >[!NOTE]
   >
   >Si selecciona **[!UICONTROL Público]**, la colección inteligente está disponible para todos los usuarios con la función Propietario después de crearla. Si cancela la **[!UICONTROL Público]** , el grupo de usuarios DAM ya no está asociado con la colección inteligente.

1. Pulse o haga clic en **[!UICONTROL Guardar]** para crear la colección inteligente y, a continuación, cierre el cuadro de mensaje para completar el proceso. La nueva colección inteligente también se agrega a la lista **[!UICONTROL Búsquedas guardadas]**..
La etiqueta del botón **[!UICONTROL Crear selección inteligente]** cambia a **[!UICONTROL Editar selección inteligente]**. Para editar la configuración de la colección inteligente, seleccione **[!UICONTROL Archivos]** en la lista **[!UICONTROL Archivos y carpetas]**. A continuación, pulse o haga clic en el botón **[!UICONTROL Editar selección inteligente]**.

## Agregar recursos a una colección {#add-assets-to-a-collection}

Puede agregar recursos a una colección que contenga una lista de recursos o carpetas a los que se hace referencia.

>[!NOTE]
>
>Las colecciones inteligentes utilizan una consulta de búsqueda para rellenar recursos. Por lo tanto, las referencias estáticas a recursos y carpetas no son aplicables a ellos.

1. En la interfaz de usuario de Assets, vaya a la ubicación del recurso que desea agregar a una colección.
1. Seleccione el recurso y toque o haga clic en el **[!UICONTROL A la colección]** de la barra de herramientas. Como alternativa, puede arrastrar el recurso hasta el **[!UICONTROL Colocar una colección]** zona. Suelte el botón del ratón cuando la zona de colocación se active y su etiqueta cambie a **[!UICONTROL Soltar para agregar]**.
1. En el **[!UICONTROL Agregar a colección]** , seleccione la colección a la que desea agregar el recurso.
1. Toque o haga clic **[!UICONTROL Agregar]** y cierre el mensaje de confirmación. El recurso se agrega a la colección.

## Editar una colección inteligente {#edit-a-smart-collection}

Las colecciones inteligentes se crean guardando una búsqueda para que pueda modificar su contenido modificando los parámetros de búsqueda de la variable [búsqueda guardada](#saved-searches).

1. En la interfaz de usuario de Assets, toque o haga clic en el botón **[!UICONTROL Buscar]** de la barra de herramientas.
1. Con el cursor en el cuadro Omnisearch , seleccione el `Enter` clave.
1. Toque o haga clic en el icono de navegación global para mostrar el panel Filtros .
1. En la lista **[!UICONTROL Búsquedas guardadas]**, seleccione la colección inteligente que desee modificar. El panel Buscar aparecen los filtros configurados para la búsqueda guardada.
1. En el **[!UICONTROL Archivos y carpetas]** lista, seleccionar **[!UICONTROL Archivos]**.
1. Modifique uno o más filtros según sea necesario. Toque o haga clic **[!UICONTROL Editar colecciones inteligentes]**. También puede editar el nombre de la colección inteligente.
1. Toque o haga clic **[!UICONTROL Guardar]**. La variable **[!UICONTROL Editar colecciones inteligentes]** se abre.
1. Toque o haga clic **[!UICONTROL Sobrescribir]** para reemplazar la colección inteligente original por la colección editada. También puede seleccionar **[!UICONTROL Guardar como]** para guardar la colección editada por separado.
1. En el cuadro de diálogo de confirmación, toque o haga clic en **[!UICONTROL Guardar]** para completar el proceso.

## Ver y editar metadatos de colección {#view-and-edit-collection-metadata}

Los metadatos de la colección comprenden datos sobre la colección, incluidas las etiquetas que se agreguen.

1. En la consola Colecciones , seleccione una colección y toque o haga clic en el **[!UICONTROL Propiedades]** de la barra de herramientas.
1. En la página **[!UICONTROL Metadatos de la colección]**, consulte los metadatos de la colección desde las pestañas **[!UICONTROL Básico]** y **Avanzado**.
1. Modifique los metadatos según sea necesario y, a continuación, toque o haga clic en **[!UICONTROL Guardar y cerrar]** en la barra de herramientas para guardar los cambios.

### Editar metadatos de colección de forma masiva {#edit-collection-metadata-in-bulk}

Puede editar los metadatos de varias colecciones simultáneamente. Esta funcionalidad le ayuda a duplicar rápidamente metadatos comunes en varias colecciones.

1. En la consola Colecciones , seleccione dos o más colecciones para las que desee editar metadatos.
1. En la barra de herramientas, toque o haga clic en el botón **[!UICONTROL Propiedades]** icono.
1. En la página **[!UICONTROL Metadatos de la colección]**, edite los metadatos en las pestañas **[!UICONTROL Básico]** y **[!UICONTROL Avanzado]**, según sea necesario.
1. Toque o haga clic **[!UICONTROL Guardar y cerrar]** en la barra de herramientas y, a continuación, cierre el cuadro de diálogo de confirmación para completar el proceso.
1. Para anexar los nuevos metadatos con los metadatos existentes, seleccione el modo **[!UICONTROL Anexar]**. Si no selecciona esta opción, los metadatos nuevos sustituirán a los metadatos existentes en los campos. Pulse o haga clic en **[!UICONTROL Enviar]**.

   >[!NOTE]
   >
   >El modo Anexar solo funciona para campos que pueden contener varios valores. Para los campos que pueden contener un solo valor, los nuevos metadatos no se anexan al valor existente en el campo aunque seleccione el modo **[!UICONTROL Anexar]**.

## Búsqueda {#searching}

La función de búsqueda dentro de Colecciones admite ambas [Buscar colecciones](#search-collections) y [Buscar recursos dentro de una colección](#search-within-collections).

### Buscar colecciones {#search-collections}

Puede buscar colecciones desde la consola Colecciones . Al buscar con palabras clave en el cuadro Omnisearch , [!DNL Experience Manager Assets] busca los nombres de colección, los metadatos y las etiquetas añadidas a las colecciones.

Si busca colecciones del nivel superior, solo se devolverán colecciones individuales en los resultados de búsqueda. Se excluyen los recursos o carpetas de las colecciones. En todos los demás casos (por ejemplo, dentro de una colección individual o en una jerarquía de carpetas), se devuelven todos los recursos, carpetas y colecciones relevantes.

### Buscar en colecciones {#search-within-collections}

En la consola Colecciones , toque o haga clic en una colección para abrirla.

Dentro de una colección, [!DNL Experience Manager] la búsqueda está restringida a los recursos (y sus etiquetas y metadatos) dentro de la colección que está viendo. Al buscar dentro de una carpeta, se devuelven todos los recursos coincidentes y las carpetas secundarias de la carpeta actual. Al buscar dentro de una colección, solo se devuelven los recursos, carpetas y otras colecciones que coinciden con los miembros directos de la colección.

## Editar configuración de colección {#edit-collection-settings}

Puede editar la configuración de la colección, como el título y la descripción, o agregar miembros a una colección.

1. Seleccione una colección y toque o haga clic en el botón **[!UICONTROL Configuración]** en la barra de herramientas. También puede usar la variable **[!UICONTROL Configuración]** acción rápida desde la miniatura de la colección.
1. Modifique la configuración de la colección en la página **[!UICONTROL Configuración de la colección]**. Por ejemplo, modifique el título de la colección, las descripciones, los miembros y los permisos tal como se describe en [Agregar colecciones](#create-a-collection).
1. Toque o haga clic **[!UICONTROL Guardar]** para guardar los cambios.

## Eliminar una colección {#delete-a-collection}

1. En la consola Colecciones , seleccione una o varias colecciones y pulse o haga clic en el icono Eliminar de la barra de herramientas.
1. En el cuadro de diálogo, toque o haga clic en **[!UICONTROL Eliminar]** para confirmar la acción de eliminación.

   >[!NOTE]
   >
   >También puede eliminar colecciones inteligentes mediante [eliminar búsquedas guardadas](#saved-searches).

## Descargar una colección {#download-a-collection}

Cuando descarga una colección, se descarga toda la jerarquía de recursos de la colección, incluidas las carpetas y las colecciones secundarias.

1. En la consola Colecciones , seleccione una o varias colecciones para descargar.
1. En la barra de herramientas, pulse o haga clic en el icono de descarga.
1. En el **[!UICONTROL Descargar]** cuadro de diálogo, pulsar o hacer clic **[!UICONTROL Descargar]**. Si desea descargar las representaciones de los recursos dentro de la colección, seleccione **[!UICONTROL Representaciones]**. <!-- Select the **[!UICONTROL Email]** option to send an email notification to the owner of the collection. -->

   Cuando selecciona una colección para descargar, se descarga la jerarquía completa de carpetas bajo la colección. Para incluir cada colección que descargue (incluidos los activos de colecciones secundarias anidadas en la colección principal) en una carpeta individual, seleccione **[!UICONTROL Crear una carpeta independiente para cada recurso]**.

## Editar propiedades de metadatos de varias colecciones {#editing-metadata-properties-of-multiple-collections}

Recursos de Adobe Enterprise Manager le permite editar los metadatos de muchas colecciones de forma masiva. Utilice la variable [!UICONTROL Propiedades] para realizar cambios en los metadatos de varias colecciones, por ejemplo, cambiar las propiedades de los metadatos a un valor común o agregar o modificar etiquetas.

Personalización de los metadatos [!UICONTROL Propiedades] , incluida la adición, modificación y eliminación de propiedades de metadatos, utilice el editor de esquemas.

>[!NOTE]
>
>Los métodos de edición por lotes funcionan con los recursos disponibles en una colección. Para los recursos disponibles en todas las carpetas o que coinciden con criterios comunes, es posible [actualizar de forma masiva los metadatos después de buscar](/help/assets/search-assets.md#metadata-updates).

1. En la consola de colecciones, seleccione las colecciones que desee editar.
1. En la barra de herramientas, toque o haga clic en **[!UICONTROL Propiedades]** para abrir el [!UICONTROL Propiedades] para las colecciones seleccionadas.
1. Modifique las propiedades de metadatos de las colecciones seleccionadas en las distintas pestañas.

   >[!NOTE]
   >
   >Los metadatos que agregue para las colecciones seleccionadas sobrescriben los metadatos anteriores para estas colecciones, excepto para las etiquetas. Cualquier etiqueta que agregue al **[!UICONTROL Etiquetas]** , se anexan a la lista existente de etiquetas en los metadatos.

1. Para ver las propiedades de los metadatos de una colección específica, cancele la selección de las colecciones restantes de la lista de colecciones. Los campos del editor de metadatos se rellenan con los metadatos de la colección en particular.

   >[!NOTE]
   >
   >* En la página de propiedades de la colección, puede eliminar colecciones de la lista de colecciones cancelando la selección. La lista de colecciones tiene todas las colecciones seleccionadas de forma predeterminada. Los metadatos de las colecciones que elimine no se actualizarán.
   >* En la parte superior de la lista, seleccione la casilla de verificación situada cerca de **[!UICONTROL Título]** para alternar entre la selección de las colecciones y la eliminación de la lista.


1. Guarde los cambios.

## Crear colecciones anidadas {#create-nested-collections}

Puede agregar una colección a otra colección, creando así una colección anidada.

1. En la consola Colecciones , seleccione la colección o el grupo de colecciones que desee y pulse o haga clic en **[!UICONTROL A la colección]** en la barra de herramientas.
1. En el **[!UICONTROL Agregar a colección]** , seleccione la colección en la que desea agregar la colección.

   >[!NOTE]
   >
   >La colección actualizada más recientemente está seleccionada de forma predeterminada en la variable **[!UICONTROL Agregar a colección]** página.

1. Toque o haga clic **[!UICONTROL Agregar]**. Un mensaje confirma que la colección se agrega a la colección de destino en la **[!UICONTROL Seleccionar destino]** página. Cierre el mensaje para completar el proceso.

>[!NOTE]
>
>Las colecciones inteligentes no se pueden anidar. En otras palabras, las colecciones inteligentes no pueden contener ninguna otra colección.

## Búsquedas guardadas {#saved-searches}

En la interfaz de usuario de Assets, puede buscar o filtrar recursos en función de determinadas reglas, criterios de búsqueda o facetas de búsqueda personalizadas. Si los guarda como **[!UICONTROL Búsquedas guardadas]**, puede acceder a ellos más adelante desde la lista **[!UICONTROL Búsquedas guardadas]** del panel Filtro. Al crear una búsqueda guardada también se crea una colección inteligente.

Las búsquedas guardadas se crean al crear una colección inteligente. Las colecciones inteligentes se agregan automáticamente a la lista **[!UICONTROL Búsquedas guardadas]**. La consulta Búsquedas guardadas para la colección se guarda en la `dam:query`propiedad de CRXDE en la ubicación relativa`/content/dam/collections/`. No existen límites a las búsquedas que se pueden guardar ni a las búsquedas guardadas que se muestran en la lista.

>[!NOTE]
>
>Puede compartir colecciones inteligentes del mismo modo que comparte colecciones estáticas.

Editar búsquedas guardadas es lo mismo que editar colecciones inteligentes. Para obtener más información, consulte [Editar una colección inteligente](#edit-a-smart-collection).

Para eliminar las búsquedas guardadas, siga estos pasos:

1. En la interfaz de usuario de Assets, pulse o haga clic en el icono de búsqueda de la barra de herramientas.

1. Con el cursor en el campo Omnisearch , seleccione la `Enter` clave.
1. Toque o haga clic en el icono de navegación global para mostrar el panel Filtros .
1. En la lista **[!UICONTROL Búsquedas guardadas]**, pulse o haga clic en **[!UICONTROL Eliminar]** al lado de la colección inteligente que desee eliminar.
1. En el cuadro de diálogo, toque o haga clic en **[!UICONTROL Eliminar]** para eliminar la búsqueda guardada.

## Ejecución de un flujo de trabajo en una colección {#run-a-workflow-on-a-collection}

Puede ejecutar un flujo de trabajo para los recursos de una colección. Si la colección contiene colecciones anidadas, el flujo de trabajo también se ejecuta en los recursos de las colecciones anidadas. Sin embargo, si la colección y la colección anidada contienen recursos duplicados, el flujo de trabajo solo se ejecuta una vez para estos recursos.

1. En la consola Colecciones , seleccione una colección en la que desee ejecutar un flujo de trabajo.
1. Pulse o haga clic en el icono de navegación global y elija **[!UICONTROL Cronología]** de la lista.
1. En la cronología, pulse o seleccione el icono del circunflejo invertido en la parte inferior y, a continuación, pulse o haga clic en **[!UICONTROL Iniciar flujo de trabajo]**.
1. En la sección **[!UICONTROL Iniciar flujo de trabajo]**, seleccione un modelo de flujo de trabajo de la lista. Por ejemplo, seleccione el modelo **[!UICONTROL Recurso de actualización DAM]**.
1. Introduzca un título para el flujo de trabajo y pulse o haga clic en **[!UICONTROL Inicio]**.
1. En el cuadro de diálogo, toque o haga clic en **[!UICONTROL Continuar]**. El flujo de trabajo se ejecuta en todos los recursos de la colección.

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
* [Importación masiva de metadatos](metadata-import-export.md)

>[!MORELIKETHIS]
>
>* [Crear una tarea de revisión para colecciones](/help/assets/bulk-approval.md)

