---
title: Lanzamientos para fragmentos de contenido
description: Aprenda a utilizar lanzamientos para fragmentos de contenido en Adobe Experience Manager as a Cloud Service. Los lanzamientos le permiten desarrollar contenido de forma eficaz para una versión futura, sin perder de vista los fragmentos de contenido actuales.
feature: Content Fragments
role: User, Developer, Architect
solution: Experience Manager Sites
exl-id: c0b9e571-3be5-42ab-8d56-d93e8ef4c2f7
source-git-commit: 39ff527f0082a18f0853964172eabf438caa1098
workflow-type: tm+mt
source-wordcount: '1582'
ht-degree: 2%

---

# Lanzamientos para fragmentos de contenido {#launches-for-content-fragments}

En Adobe Experience Manager (AEM) as a Cloud Service, los lanzamientos le permiten desarrollar contenido de forma eficaz para una versión futura.

Se crea un *Launch* para permitirle realizar cambios con el fin de prepararse para una publicación futura y, al mismo tiempo, mantener el contenido actual. Para los fragmentos de contenido, esto significa que está editando dos versiones al mismo tiempo: el contenido que se publica actualmente y una versión de ese contenido que se publicará en un momento futuro. Una vez que llegue ese momento, puede reemplazar el contenido de los fragmentos de contenido originales y publicar las nuevas versiones.

>[!NOTE]
>
>También hay lanzamientos disponibles para las páginas. Los conceptos básicos son los mismos, pero hay diferencias en la forma de administrarlos en AEM.
>
>Para obtener información detallada, consulte [Inicios de páginas](/help/sites-cloud/authoring/launches/overview.md).

Usted crea un *Launch*, luego edita y actualiza sus fragmentos de contenido en su *Launch*. Si se realizan cambios en los fragmentos de *Source* durante esta fase, puede copiarlos en *Launch* con la operación *Rebase*. Cuando esté listo, *Promocionar* duplica el contenido del lanzamiento de nuevo en el origen. A continuación, puede activar los fragmentos de origen, ya sea manual o automáticamente (según los campos establecidos al crear y editar el lanzamiento). También puede especificar si los fragmentos a los que se hace referencia se incluirán en este proceso.

Por ejemplo, los fragmentos de productos de temporada de la tienda en línea se actualizan trimestralmente para que los productos destacados se correspondan con la temporada actual. Para prepararse para la siguiente actualización trimestral, puede crear un lanzamiento de los fragmentos adecuados. Durante el trimestre, se acumulan los cambios siguientes en la copia de lanzamiento:

* Ediciones que se realizan directamente en los fragmentos de lanzamiento como preparación para el siguiente trimestre.
* Cambios en los fragmentos de contenido de origen que transfiere a las páginas de lanzamiento con *Rebase*.
* También puede navegar por el contenido en la rama de lanzamiento; agregando o eliminando fragmentos según sea necesario.

Cuando llegue el trimestre siguiente, las páginas de lanzamiento se promocionan de modo que se puedan publicar las páginas de origen (que contienen el contenido actualizado). Puede promocionar todos los fragmentos o solo aquellos que haya modificado.

![Información general sobre lanzamientos: volver a basar y promocionar](/help/sites-cloud/administering/content-fragments/assets/cf-launches-overview.png)

En esta sección se describe cómo crear, editar, administrar, volver a basar, promocionar y, si es necesario eliminar lanzamientos desde la [consola Fragmentos de contenido](/help/sites-cloud/administering/content-fragments/managing.md):

* [Acceder y ver lanzamientos en la consola Fragmentos de contenido](#launches-in-the-content-fragment-console)
* [Crear un lanzamiento](#create-a-launch)
* [Editar contenido de Launch](#edit-launch-content)
* [Administración de contenido dentro de un lanzamiento](#manage-content-within-a-launch)
* [Comparar lanzamiento con el origen](#compare-launch-to-source)
* [Volver a basar un lanzamiento desde Source](#rebase-a-launch-from-source)
* [Promocionar un lanzamiento en Source](#promote-a-launch-to-source)
* [Eliminar un lanzamiento](#delete-a-launch)

## Inicios en la consola Fragmento de contenido {#launches-in-the-content-fragment-console}

La pestaña **Lanzamientos** de la consola Fragmentos de contenido le permite crear lanzamientos, enumerar todos los lanzamientos existentes, ver las propiedades clave y realizar acciones en consecuencia.

Cuando no se ha seleccionado ningún lanzamiento, puede [crear un nuevo lanzamiento](#create-a-launch).

![Pestaña Lanzamientos en la consola](/help/sites-cloud/administering/content-fragments/assets/cf-launches-tab.png)

Seleccione el lanzamiento que desea mostrar:

* la barra de herramientas, con las acciones disponibles
* el panel derecho, con propiedades y más acciones

![Barra de herramientas de acciones de Launch en la consola](/help/sites-cloud/administering/content-fragments/assets/cf-launches-actions.png)

La barra de herramientas permite:

* **[Abrir lanzamiento](#edit-launch-content)**
* **[Editar orígenes](#manage-content-within-a-launch)**
* **[Comparar Launch con Source](#compare-launch-to-source)**
* **[Promocionar](#promote-a-launch-to-source)**
* **[Volver a basar](#promote-a-launch-to-source)**
* **[Eliminar lanzamiento](#delete-a-launch)**

Mientras que el panel derecho le permite:

* Editar el lanzamiento **Title**
* Editar la **descripción** del lanzamiento
* Actualice los detalles de configuración que se establecieron cuando [creó el lanzamiento](#create-a-launch):

   * **Incluir referencias**: cree el lanzamiento con o sin, incluidos los fragmentos de contenido a los que se hace referencia. De forma predeterminada, se incluyen los fragmentos a los que se hace referencia.

      * Los fragmentos a los que se hace referencia también se ven afectados cuando [agrega o quita fragmentos del lanzamiento](#manage-content-within-a-launch) en una fase posterior.

     >[!NOTE]
     >
     >Ver [detalles sobre referencias incluidas](#details-concerning-included-references)

   * **Listo para publicar**; al habilitar esta opción, se publicarán automáticamente los fragmentos cuando el lanzamiento se promocione al origen.

* Y también definir:

   * Una **fecha de promoción** y hora: si el [lanzamiento se promocionará automáticamente](#promote-automatically)

## Crear un lanzamiento {#create-a-launch}

Para crear el lanzamiento:

1. Vaya a la consola Fragmentos de contenido.

1. Abra la ficha **Lanzamientos**.

1. Seleccione **Crear lanzamiento**.

1. Vaya a la carpeta adecuada y seleccione los fragmentos que desea incluir en el lanzamiento:

   ![Seleccionar fragmentos de contenido para el nuevo lanzamiento](/help/sites-cloud/administering/content-fragments/assets/cf-launches-create-select-cfs.png)

1. Seleccione **Siguiente**.

1. Especifique los detalles para configurar el lanzamiento:

   * **Título**
   * **Descripción**
   * **Incluir referencias**: cree el lanzamiento con o sin, incluidos los fragmentos de contenido a los que se hace referencia. De forma predeterminada, se incluyen los fragmentos a los que se hace referencia.

     >[!NOTE]
     >
     >Ver [detalles sobre referencias incluidas](#details-concerning-included-references)

   * **Listo para publicar**: al habilitar esta opción, se publicarán automáticamente los fragmentos cuando el lanzamiento se promocione al origen.

   ![Detalles del nuevo lanzamiento](/help/sites-cloud/administering/content-fragments/assets/cf-launches-create-launch-details.png)

1. **Guarde** la configuración.

1. Ha vuelto a la pestaña **Lanzamientos** de la consola Fragmentos de contenido, donde:

   * el nuevo lanzamiento ya aparece en la lista
   * se muestra un mensaje para confirmar que se ha iniciado la creación del lanzamiento:

      * **Trabajo iniciado para crear un nuevo Launch, supervisar el progreso en AEM y volver a cargar la página cuando haya terminado.**

1. Seleccione **Ver**, en el cuadro de mensaje, para ver más detalles en la consola de AEM para [Operaciones en segundo plano](/help/operations/asynchronous-jobs.md).

   ![Nuevo lanzamiento en la consola](/help/sites-cloud/administering/content-fragments/assets/cf-launches-new-launch-in-console.png)

## Editar contenido de Launch {#edit-launch-content}

Para editar los fragmentos de contenido en el lanzamiento:

1. Vaya a la consola Fragmentos de contenido.

1. Abra la ficha **Lanzamientos**.

1. Seleccione el lanzamiento para mostrar las acciones de la barra de herramientas.

1. Seleccione **Abrir lanzamiento**.

   El lanzamiento se mostrará junto con los fragmentos que contiene.

   ![Editar contenido de Launch](/help/sites-cloud/administering/content-fragments/assets/cf-launches-edit-launch-content.png)

1. Seleccione **Editar** para el fragmento que desee actualizar. Se abrirá en el [editor de fragmentos](/help/sites-cloud/administering/content-fragments/authoring.md) como de costumbre.

## Administración de contenido dentro de un lanzamiento {#manage-content-within-a-launch}

Para administrar los fragmentos de contenido en el lanzamiento y también editar su contenido:

1. Vaya a la consola Fragmentos de contenido.

1. Abra la ficha **Lanzamientos**.

1. Seleccione el lanzamiento.

1. Seleccionar **Editar orígenes**.

   Se mostrarán los fragmentos de origen del lanzamiento.

   ![Editar Source](/help/sites-cloud/administering/content-fragments/assets/cf-launches-edit-sources.png)

1. Puede hacer lo siguiente:

   1. **Agregar orígenes** para agregar más fragmentos al lanzamiento.

      * Si **Incluir referencias** es verdadero para el lanzamiento, todos los fragmentos de contenido a los que se hace referencia también se incluirán en el lanzamiento (si no están presentes).

   1. Seleccione **Editar** para el fragmento de origen que desee actualizar. Se abrirá en el [editor de fragmentos](/help/sites-cloud/administering/content-fragments/authoring.md) como de costumbre.

   1. Seleccione un fragmento y, a continuación, la acción **Eliminar orígenes** de la barra de herramientas para quitar ese fragmento del lanzamiento.

      * Si **Incluir referencias** es verdadero para el lanzamiento, todos los fragmentos de contenido a los que se hace referencia también se quitarán del lanzamiento, a menos que también hagan referencia a ellos otros fragmentos de contenido que aún se encuentren en el lanzamiento.

   >[!NOTE]
   >
   >Ver [detalles sobre referencias incluidas](#details-concerning-included-references)

## Comparar lanzamiento con el origen {#compare-launch-to-source}

Se recomienda que, antes de cualquier acción de Rebase o Promocionar, siempre compare el origen y el lanzamiento para confirmar los cambios y su impacto en el contenido (ambas acciones sobrescriben el contenido de destino):

1. Vaya a la consola Fragmentos de contenido.

1. Abra la ficha **Lanzamientos**.

1. Seleccione el lanzamiento.

1. Seleccione **Comparar Launch con Source**.

   * Los fragmentos de origen e inicio se muestran uno al lado del otro para resaltar las diferencias.
      * Los fragmentos de Source se muestran a la izquierda, mientras que los fragmentos de Launch se muestran a la derecha.
      * Las actualizaciones están resaltadas:
         * Source: azul
         * Lanzamiento: rosa
         * Conflictos: amarillo
   * Las acciones [Promocionar](#promote-a-launch-to-source) y [Volver a basar](#rebase-a-launch-from-source) están disponibles en la parte superior derecha.
   * **Actualizaciones encontradas**: en la esquina superior izquierda se muestra un resumen de todas las actualizaciones. El número de actualizaciones de origen en azul, el número de actualizaciones de inicio en rosa y las actualizaciones en ambos (conflictos) en amarillo.
      * Los iconos de ojo le permiten mostrar u ocultar las actualizaciones de contenido real para obtener una visión general más clara.
   * Los controles deslizantes **Include** permiten definir los fragmentos de contenido que se incluirán en la operación de promoción o rebase posterior:
      * **Incluir todo** en la parte superior derecha
      * **Incluir** encima de cada fragmento en el lanzamiento

     >[!NOTE]
     >
     >Los controles deslizantes solo se aplican a las acciones Promocionar y Rebasar tomadas desde la pantalla Comparar.

   * El contenido del fragmento se muestra en el nivel de campo (elemento de fragmento de contenido/nivel de tipo de datos); con resaltados que indican cambios.
   * Seleccione **Ver** para volver a calcular las diferencias.

   ![Comparar Source y Launch](/help/sites-cloud/administering/content-fragments/assets/cf-launches-compare.png)

## Volver a basar un lanzamiento (desde Source) {#rebase-a-launch-from-source}

Cuando se hayan realizado actualizaciones en los fragmentos de origen y desee copiar estos cambios en el lanzamiento:

1. Vaya a la consola Fragmentos de contenido.

1. Abra la ficha **Lanzamientos**.

1. Seleccione el lanzamiento y los fragmentos.

1. Seleccione **Volver a basar**.

>[!NOTE]
>
>También puede **Volver a basar** un lanzamiento desde **[Comparar lanzamiento con Source](#compare-launch-to-source)**.

## Promocionar un lanzamiento (a Source) {#promote-a-launch-to-source}

Cuando el lanzamiento esté listo para publicarse, debe copiarse en el origen. Puede hacerlo en la consola o configurar los ajustes para que se produzca automáticamente en una fecha y hora específicas.

### Promocionar manualmente {#promote-manually}

Cuando el lanzamiento esté listo para publicarse, se puede copiar en el origen con la acción explícita:

1. Vaya a la consola Fragmentos de contenido.

1. Abra la ficha **Lanzamientos**.

1. Seleccione el lanzamiento y los fragmentos.

1. Seleccione **Promocionar**.

>[!NOTE]
>
>También puedes **Promocionar** un lanzamiento desde **Comparar lanzamiento con Source**.

### Promocionar automáticamente {#promote-automatically}

Para que un lanzamiento se promocione automáticamente en una fecha y hora especificadas, debe:

1. Defina **Fecha y hora de la promoción** desde el panel derecho de la [pestaña Lanzamientos](#launches-in-the-content-fragment-console).

1. Si el contenido se puede publicar cuando se promocione, establezca **Listo para publicar** al [crear el lanzamiento](#create-a-launch) o desde el panel derecho de la [pestaña Lanzamientos](#launches-in-the-content-fragment-console).

## Eliminar un lanzamiento {#delete-a-launch}

Después de promocionar el lanzamiento o de decidir que ya no lo necesita, puede eliminarlo:

1. Vaya a la consola Fragmentos de contenido.

1. Abra la ficha **Lanzamientos**.

1. Seleccione el lanzamiento.

1. Seleccione **Eliminar lanzamiento**.

   Se le pedirá que confirme la acción antes de eliminar el lanzamiento.

## Detalles sobre las referencias incluidas {#details-concerning-included-references}

Para los lanzamientos, se tienen en cuenta las siguientes referencias de fragmentos de contenido, según el [tipo de datos](/help/sites-cloud/administering/content-fragments/content-fragment-models.md#data-types):

* El tipo de datos **Referencia de fragmento**, aplicable tanto a referencias de fragmento únicas como a referencias de fragmento de varios campos.
* Fragmentos a los que se hace referencia dentro del tipo de datos **Texto de varias líneas** al usar **Texto enriquecido**.

Todos los puntos también son aplicables a los fragmentos a los que se hace referencia dentro de variaciones

No se tienen en cuenta los siguientes factores:

* Fragmentos a los que se hace referencia dentro de los tipos de datos de referencia de contenido, tanto **Referencia de contenido** (basada en la ruta) como **Referencia de contenido (UUID)**.
* Fragmentos a los que se hace referencia dentro del tipo de datos **Referencia de fragmento (UUID)**.
