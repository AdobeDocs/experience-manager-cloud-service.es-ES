---
title: Administración de etiquetas
description: AEM Obtenga información sobre cómo administrar etiquetas en la de organizar el contenido.
exl-id: 42480699-b7a7-4678-a763-569a9b7573e2
solution: Experience Manager Sites
feature: Workflow
role: Admin
source-git-commit: 10580c1b045c86d76ab2b871ca3c0b7de6683044
workflow-type: tm+mt
source-wordcount: '2200'
ht-degree: 1%

---

# Administración de etiquetas {#administering-tags}

Las etiquetas son un método intuitivo de clasificar el contenido. Se pueden considerar como palabras clave o etiquetas (metadatos) que permiten encontrar el contenido más rápidamente.

En Adobe Experience Manager AEM (), una etiqueta puede ser una propiedad de:

* Un nodo de contenido para una página
   * Consulte el documento [Uso de etiquetas](/help/sites-cloud/authoring/sites-console/tags.md) para obtener más información.
* Un nodo de metadatos para un recurso
   * Consulte el documento [Administración de metadatos para Assets digital](/help/assets/manage-metadata.md) para obtener más información.

>[!TIP]
>
>Se recomienda minimizar el número de etiquetas relacionadas con las mismas ideas. Por ejemplo, si estás administrando contenido para una tienda de suministros al aire libre, probablemente no necesites una etiqueta para **calzado** y **zapatos**.

## Características de etiquetas {#tag-features}

Las etiquetas ofrecen funciones sólidas para organizar y administrar el contenido.

* Las etiquetas se pueden agrupar en varias áreas de nombres.
   * Las áreas de nombres se pueden considerar como jerarquías que permiten crear taxonomías.
   * AEM Estas taxonomías son globales en todo el mundo
* Los autores pueden aplicar las etiquetas y los visitantes del sitio pueden utilizarlas.
* Independientemente de su creador, todas las formas de etiquetas están disponibles para su selección, tanto al asignarlas a una página como al buscar.
* El [componente Lista](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/list.html?lang=es) utiliza las etiquetas para generar listas dinámicas basadas en las etiquetas seleccionadas.

## Requisitos de etiquetas {#requirements}

Hay algunos detalles técnicos que se deben tener en cuenta al crear y administrar etiquetas.

* Las etiquetas deben ser únicas dentro de un área de nombres específica.
* El nombre de una etiqueta no puede incluir delimitadores de etiqueta:
   * Dos puntos (`:`): delimita la etiqueta de área de nombres
   * Barra oblicua (`/`): Delimita las etiquetas secundarias
* Si el título de una etiqueta incluye delimitadores de etiqueta, estos se suprimirán en la interfaz de usuario.
* Se pueden crear etiquetas y los miembros del grupo `tag-administrators` y los miembros que tienen derechos de modificación sobre `/content/cq:tags` pueden modificar su taxonomía.
   * Una etiqueta que contiene etiquetas secundarias se denomina etiqueta contenedora.
   * Una etiqueta que no es una etiqueta contenedora se denomina etiqueta de hoja.
   * Un área de nombres de etiqueta puede ser una etiqueta de hoja o una etiqueta contenedora.

AEM Para obtener más información técnica sobre cómo funcionan las etiquetas, consulte [Marco de etiquetado de la](/help/implementing/developing/introduction/tagging-framework.md).

## Consola de etiquetado {#tagging-console}

La consola de etiquetado se utiliza para crear y administrar etiquetas y sus taxonomías. Puede utilizar la consola de etiquetado para administrar las etiquetas de las siguientes formas:

* Agrupándolos en áreas de nombres.
* Revise el uso de las etiquetas existentes antes de crear nuevas.
* Reorganizar las etiquetas sin desconectar la etiqueta del contenido al que se hace referencia actualmente.

Para acceder a la consola de etiquetado:

1. Inicie sesión en un entorno de creación con privilegios administrativos.
1. En el menú de navegación global, seleccione **`Tools`** > **`General`** >
   **`Tagging`**.

AEM ![La consola de etiquetado en el código de tiempo de trabajo](/help/sites-cloud/administering/assets/tagging-console.png)

## Creación de nuevas etiquetas {#creating-new-tags}

Existen varios pasos para crear y utilizar etiquetas para organizar el contenido.

1. [Cree un área de nombres para sus etiquetas](#creating-namespaces) (o elija una existente para reutilizarla).
1. [Crear una etiqueta nueva](#creating-tags).
1. [Publish usa la etiqueta](#publishing-tags).

### Creación de áreas de nombres {#creating-namespaces}

Se utiliza un área de nombres para organizar otras etiquetas. Se puede considerar como la etiqueta de nivel inferior y se suele utilizar para agrupar otras etiquetas.

1. Para crear un área de nombres, abra la [consola de etiquetado](#tagging-console), seleccione el botón **Crear** en la barra de herramientas y, a continuación, **Crear área de nombres**.

   ![Cuadro de diálogo Agregar área de nombres](/help/sites-cloud/administering/assets/add-namespace.png)

1. Proporcione la información necesaria.

   * **Título**: título del área de nombres mostrado al usuario en la interfaz de usuario (opcional)
   * **Nombre**: si no se especifica un nombre, se crea un nombre de nodo válido a partir del **Título**. AEM Consulte el documento [Marco de etiquetado de ](/help/implementing/developing/introduction/tagging-framework.md#tagid)para obtener más información.
   * **Descripción**: una descripción del área de nombres (opcional)

1. Una vez que ingrese la información requerida, seleccione **Crear**.

Se crea el área de nombres. En la consola de etiquetado, las áreas de nombres se encuentran en el nivel inferior (en la columna del extremo izquierdo de la consola) y se representan mediante iconos de carpeta, que reflejan su naturaleza como &quot;contenedor&quot; o agrupación de otras etiquetas.

Ahora puede [crear nuevas etiquetas](#creating-tags) en este espacio de nombres o [administrar etiquetas existentes](#managing-tags).

Un área de nombres no necesita contener subetiquetas. Como un área de nombres es en sí misma una etiqueta, se puede utilizar para organizar el contenido como cualquier otra etiqueta. Sin embargo, para continuar creando una taxonomía de etiquetado estructurada, puede [crear subetiquetas](#creating-tags) dentro de ese área de nombres en función de los requisitos de su proyecto.

### Creación de etiquetas {#creating-tags}

Las etiquetas se suelen añadir a áreas de nombres.

1. Para crear una etiqueta, abra la [consola de etiquetado](#tagging-console).

1. Seleccione el área de nombres donde desea crear la etiqueta. O seleccione otra etiqueta para crear una subetiqueta debajo de ella.

1. Seleccione el botón **Crear** en la barra de herramientas y luego **Crear etiqueta**.

1. Se abre el cuadro de diálogo **Crear etiqueta**. Proporcione la información necesaria para la nueva etiqueta.

   * **Título**: un título para mostrar para la etiqueta (obligatorio)
   * **Nombre** - Un nombre para la etiqueta (obligatorio). Si no se especifica, se crea un nombre de nodo válido a partir del **Título**. Consulte [TagID](/help/implementing/developing/introduction/tagging-framework.md#tagid).
   * **Descripción** - Una descripción de la etiqueta
   * **Ruta de etiqueta**: de forma predeterminada, el área de nombres (o etiqueta) que seleccionó en la consola de etiquetado. Esto se puede actualizar manualmente tocando o haciendo clic en el icono del selector de rutas.

   ![Cuadro de diálogo Crear etiqueta](assets/create-tag.png)

1. Seleccione **Enviar**.

La etiqueta se crea y la consola se actualiza para mostrar la nueva etiqueta.

Las etiquetas permiten la creación flexible de su propia taxonomía en función de sus necesidades organizativas.

* Puede crear etiquetas secundarias de etiquetas existentes seleccionando la etiqueta principal en la consola antes de crear la nueva etiqueta.
* Si crea una etiqueta sin seleccionar un área de nombres u otra etiqueta, creará de forma efectiva un área de nombres.

### Publicación de etiquetas {#publishing-tags}

AEM Al igual que con la creación de cualquier otro contenido en la, después de crear una etiqueta (o área de nombres), solo existe en el entorno de creación. Para que las etiquetas estén disponibles para los usuarios, debe publicarlas.

1. Para publicar una etiqueta, abra la [consola de etiquetado](#tagging-console).

1. Seleccione las etiquetas que desee publicar y, en la barra de herramientas, seleccione **Publish**.

   ![Seleccionar etiquetas en la consola](assets/select-tags.png)

1. El cuadro de diálogo **Etiqueta de Publish** solicita una confirmación para publicar las etiquetas seleccionadas. Seleccione **Publicar**.

   ![Modo de confirmación de etiqueta Publish](assets/publish-tag.png)

1. La acción de publicación se confirmó con un cuadro de diálogo **Éxito**.

   ![cuadro de diálogo de éxito de etiquetas Publish](assets/publish-tag-success.png)

Las etiquetas seleccionadas se han puesto en la cola de publicación. Al igual que el contenido de la página, solo se publican las etiquetas seleccionadas, independientemente de si tienen o no subetiquetas.

Para publicar una taxonomía completa (un área de nombres y subetiquetas), la práctica recomendada es crear un [paquete](/help/implementing/developing/tools/package-manager.md) del área de nombres (consulte [Nodo raíz de taxonomía](/help/implementing/developing/introduction/tagging-framework.md#taxonomy-root-node)).

<!--
Be sure to [apply permissions](#setting-tag-permissions) to the namespace before creating the package.
-->

## Administración de etiquetas {#managing-tags}

Existen varias acciones que puede realizar en las etiquetas y áreas de nombres existentes para administrarlas y organizarlas. Simplemente, seleccione una etiqueta o área de nombres en la [consola de etiquetado](#tagging-console) para mostrar en la barra de herramientas las acciones disponibles.

* [Ver propiedades](#viewing-tag-properties)
* [Editar](#editing-tags)
* [Cancelar publicación](#unpublishing-tags)
* [Referencias](#viewing-tag-references)
* [Mover](#moving-tags)
* [Combinar](#merging-tags)
* [Eliminar](#deleting-tags)

Cuando no hay suficiente espacio disponible en la barra de herramientas, hay opciones adicionales disponibles detrás del icono de puntos suspensivos.

### Visualización de propiedades de etiqueta {#viewing-tag-properties}

Cuando se selecciona una sola etiqueta, un área de nombres u otra etiqueta en la consola de etiquetado, los detalles básicos de la etiqueta seleccionada, como la hora de la última edición y la última publicación, se muestran en la columna a la izquierda de la columna de etiqueta.

![Columna de detalles de etiqueta](assets/tag-details-column.png)

Puede ver más detalles sobre la etiqueta, incluidos quién la publicó por última vez y cuándo cambió la consola a la vista **Propiedades**.

1. Para ver las propiedades de una etiqueta, abra la [consola de etiquetado](#tagging-console).

1. Seleccione la etiqueta cuyas propiedades desee ver y, en el carril izquierdo, seleccione **Propiedades**.

   ![Seleccionando vista de propiedades](assets/view-tag-properties.png)

1. Las propiedades detalladas de la etiqueta seleccionada se muestran en el carril izquierdo.

   ![Visualización de propiedades de etiqueta](assets/tag-properties.png)

Para obtener más información sobre la selección de los modos de visualización y el carril, consulte [Gestión básica](/help/sites-cloud/authoring/basic-handling.md#rail-selector).

### Edición de etiquetas {#editing-tags}

Las etiquetas y los espacios de nombre se pueden editar después de la creación.

1. Para editar una etiqueta, abra la [consola de etiquetado](#tagging-console).

1. Seleccione la etiqueta que desee editar y, en la barra de herramientas, seleccione **Editar**.

1. Realice los cambios que desee. Es posible modificar el:

   * **Título**
   * **Descripción**
   * [**Localización**](#managing-tags-in-different-languages)

1. Una vez realizadas las ediciones, seleccione **Enviar**.

Para obtener más información sobre cómo agregar traducciones de idiomas, consulte la sección sobre [Administración de etiquetas en diferentes idiomas](#managing-tags-in-different-languages).

Si los cambios que realizó fueron a una etiqueta ya publicada, es posible que desee [volver a publicarla](#publishing-tags).

### Cancelar publicación de etiquetas {#unpublishing-tags}

Para desactivar la etiqueta en la instancia de autor y quitarla de la instancia de publicación, puede cancelar la publicación.

1. Para cancelar la publicación de una etiqueta, abra la [consola de etiquetado](#tagging-console).

1. Seleccione la etiqueta o etiquetas cuya publicación desea cancelar y, en la barra de herramientas, seleccione **Cancelar publicación**.

   ![Seleccionar etiquetas en la consola](assets/select-tags.png)

1. El cuadro de diálogo **Cancelar publicación de etiqueta** pide una confirmación para publicar las etiquetas seleccionadas. Seleccione **Publicar**.

   ![Modo de confirmación de etiqueta Publish](assets/unpublish-tag.png)

1. La acción de cancelar la publicación se confirmó con un cuadro de diálogo **Éxito**.

   ![cuadro de diálogo de éxito de etiquetas Publish](assets/unpublish-tag-success.png)

Las etiquetas seleccionadas se han puesto en la cola de cancelación de publicación. Si la etiqueta seleccionada es una etiqueta contenedora, todas sus etiquetas secundarias se desactivarán en el entorno de creación y se eliminarán del entorno de publicación.

### Visualización de referencias de etiqueta {#viewing-tag-references}

Puede resultar útil ver a qué contenido se aplica una etiqueta en particular. Puede hacerlo usando la vista **Referencias** de la consola de etiquetado.

1. Para ver las referencias de una etiqueta, abra la [consola de etiquetado](#tagging-console).

1. Seleccione la etiqueta cuyas referencias desee ver y, en el carril izquierdo, seleccione **Referencias**.

   ![Seleccionando vista de propiedades](assets/view-tag-references.png)

1. El número total de referencias para la etiqueta seleccionada se muestra en el carril izquierdo.

   ![Visualización de referencias de etiquetas](assets/tag-references.png)

1. Seleccione el número de referencias de etiqueta para ver la lista detallada del contenido asignado a la etiqueta.

   ![Visualización de los detalles de las referencias de la etiqueta](assets/tag-references-detail.png)

Pase el ratón o seleccione un contenido de referencia en la lista para mostrar la ruta completa del contenido.

Para obtener más información sobre la selección de los modos de visualización y el carril, consulte [Gestión básica](/help/sites-cloud/authoring/basic-handling.md#rail-selector).

### Mover etiquetas {#moving-tags}

Puede ser necesario limpiar o reorganizar la taxonomía de etiquetado moviendo una etiqueta a una nueva ubicación o cambiándole el nombre.

>[!TIP]
>
>Se recomienda que solo se permita a los administradores mover y cambiar el nombre de las etiquetas.

1. Para mover o cambiar el nombre de una etiqueta, abra la [consola de etiquetado](#tagging-console).

1. Seleccione la etiqueta que quiera mover o cambiar de nombre y seleccione **Mover** en la barra de herramientas.

1. En el cuadro de diálogo **Mover etiqueta**, especifique qué propiedad desea cambiar.

   * **Cambiar nombre a**: el nuevo nombre que desea dar a la etiqueta
      * Este campo se rellena previamente con el nombre actual de la etiqueta.
      * Deje sin modificar si sólo desea mover la etiqueta y no cambiarle el nombre.
   * **Mover a**: lugar donde desea mover la etiqueta
      * Este campo se rellena previamente con la ubicación actual de la etiqueta.
      * Deje sin modificar si sólo desea cambiar el nombre de la etiqueta y no moverla.

   ![Mover etiqueta](assets/move-tag.png)

1. Seleccione **Enviar**.

Se cambia el nombre de la etiqueta o se mueve a su nueva ubicación. Si la etiqueta seleccionada es una etiqueta contenedora, al mover la etiqueta también se moverán todas las etiquetas secundarias.

### Combinación de etiquetas {#merging-tags}

Si la taxonomía de etiquetado tiene duplicados o etiquetas similares, puede resultar útil combinar esas etiquetas. Cuando la etiqueta `A` se combina con la etiqueta `B`, todas las páginas etiquetadas con la etiqueta `A` se etiquetarán con la etiqueta `B` y la etiqueta `A` ya no estará disponible para los autores.

1. Para combinar dos etiquetas, abra la [consola de etiquetado](#tagging-console).

1. Seleccione la etiqueta que desee combinar en otra etiqueta y, a continuación, seleccione **Combinar** en la barra de herramientas.

1. En el cuadro de diálogo **Combinar etiqueta**, seleccione el icono **Examinar** del campo **Combinar en** para especificar en qué etiqueta desea combinar la etiqueta seleccionada.

   ![Cuadro de diálogo Combinar etiqueta](assets/merge-tag.png)

1. Seleccione **Enviar**.

La etiqueta seleccionada en la consola se combina con la etiqueta especificada en el cuadro de diálogo. Cuando se mueve o combina una etiqueta a la que se hace referencia, la etiqueta no se elimina físicamente de modo que sea posible mantener referencias. AEM Consulte [Marco de etiquetado de](/help/implementing/developing/introduction/tagging-framework.md#moving-and-merging-tags) para obtener más información.

### Eliminación de etiquetas {#deleting-tags}

Si la taxonomía de etiquetado cambia y hace que una etiqueta o área de nombres sea innecesaria, se puede eliminar.

1. Para eliminar una etiqueta, abra la [consola de etiquetado](#tagging-console).

1. Seleccione la etiqueta que desee eliminar y, a continuación, seleccione **Eliminar** en la barra de herramientas.

1. El cuadro de diálogo **Eliminar etiqueta** solicita una confirmación para eliminar las etiquetas seleccionadas. Seleccione **Eliminar**.

   ![El modal de confirmación para eliminar etiqueta](assets/delete-tag.png)

1. AEM Comprobaciones para asegurarse de que no se hace referencia a la etiqueta.

   1. AEM Si no se encuentran referencias, se solicita una confirmación final para eliminar el elemento de la lista de referencias. Seleccionar **Eliminar**

      ![No se encontraron referencias](assets/no-references-found.png)

   1. AEM Si se encuentran referencias, las presenta y solicita una confirmación final para su eliminación.

      ![Referencias encontradas](assets/references-found.png)

Las etiquetas seleccionadas se eliminarán y se eliminarán permanentemente del entorno de creación. Si la etiqueta se publicó, también se elimina del entorno de publicación. Si la etiqueta seleccionada es una etiqueta contenedora, también se eliminan todas sus etiquetas secundarias.

<!--

## Setting Tag Permissions {#setting-tag-permissions}

Tag permissions are ['secure (by default)'](/help/sites-administering/production-ready.md); a best practice for the publish environment that requires read permission to be explicitly allowed for tags. Bascially, this is done by creating a package of the Tag Namespace after permissions have been set on author, and installing the package on all publish instances.

* on author instance

    * sign in with administrative privileges
    * access the [Security Console](/help/sites-administering/security.md#accessing-user-administration-with-the-security-console),

        * for example, browse to http://localhost:4502/useradmin

    * in the left pane, select the group (or user) for which [read permission](/help/sites-administering/security.md#permissions) is to be granted
    * in the right pane, locate the **Path **to the Tag Namespace

        * for example, `/content/cq:tags/mycommunity`

    * select the `checkbox`in the **Read** column
    * select **Save**

![Setting tag permissions](assets/chlimage_1-204.png)

* ensure all publish instances have same permissions

    * one approach is to [create a package](/help/sites-administering/package-manager.md#package-manager) of the namespace on author

        * on `Advanced` tab, for `AC Handling` select `Overwrite`

    * replicate the package

        * choose `Replicate` from package manager

-->

## Administración de etiquetas en diferentes idiomas {#managing-tags-in-different-languages}

La propiedad `title` de una etiqueta se puede traducir a varios idiomas. Una vez traducido, el título de etiqueta adecuado se puede mostrar según el idioma del usuario o el contenido.

Supongamos que tenemos una etiqueta llamada `Animals` que queremos traducir al alemán y al francés.

1. Abra la [consola de etiquetado](#tagging-console).

1. Seleccione la etiqueta que desee traducir y, a continuación, seleccione **Editar** en la barra de herramientas.

1. En el cuadro de diálogo **Editar etiqueta**, en la columna **Localización**, seleccione el idioma de destino, por ejemplo, el alemán.

1. En el campo **Alemán** que aparece, proporcione el título traducido.

1. Repita los dos pasos anteriores para francés.

   ![Traduciendo títulos de etiquetas](assets/translate-tag.png)

1. Seleccione **Enviar**.

Para las páginas de contenido, el idioma elegido para la etiqueta se toma del idioma de la página, cuando está disponible.

AEM Sin embargo, en el entorno de creación de, utiliza la configuración de idioma del usuario. Por lo tanto, en la consola de etiquetado, para la etiqueta `Animals`, se mostraría `Animaux` para un usuario que establece el idioma en francés en sus propiedades de usuario.

AEM Para agregar un nuevo idioma al cuadro de diálogo, consulte el documento [Generación de etiquetas en aplicaciones de la aplicación de la red 1&rbrace;](/help/implementing/developing/introduction/tagging-applications.md#adding-a-new-language-to-the-edit-tag-dialog)

>[!TIP]
>
>AEM Si desea obtener más información acerca de las características de localización de la, consulte [Traducción del contenido para sitios multilingües](/help/sites-cloud/administering/translation/overview.md).
