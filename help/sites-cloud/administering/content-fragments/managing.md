---
title: Administración de los fragmentos de contenido
description: Aprenda a administrar los fragmentos de contenido de AEM desde la consola y el editor, para crear contenido como base del contenido sin encabezado o para la creación de páginas.
feature: Content Fragments
role: User, Developer, Architect
exl-id: bcaa9f06-b15d-4790-bc4c-65db6a2d5e56
solution: Experience Manager Sites
source-git-commit: b09452637fd86af8fc71101f98e05597a8fe630e
workflow-type: tm+mt
source-wordcount: '2885'
ht-degree: 37%

---

# Administración de los fragmentos de contenido {#managing-content-fragments}

Aprenda a administrar sus **fragmentos de contenido** en Adobe Experience Manager (AEM) as a Cloud Service, desde la [consola Fragmentos de contenido](#content-fragments-console) y el [editor de fragmentos de contenido](/help/sites-cloud/administering/content-fragments/authoring.md#content-fragment-editor). Estos fragmentos de contenido se pueden utilizar como base del contenido sin encabezado o para la creación de páginas.

>[!NOTE]
>
>Esta página cubre la sección de la consola que (solo) muestra fragmentos de contenido. Para ver otros paneles, consulte:
>
>* [Administrar modelos de fragmentos de contenido](/help/sites-cloud/administering/content-fragments/managing-content-fragment-models.md)
>* [Visualización y administración de Assets en la consola Fragmentos de contenido](/help/sites-cloud/administering/content-fragments/assets-content-fragments-console.md)

Después de definir los [modelos de fragmentos de contenido](#creating-a-content-model), puede usarlos para lo siguiente:

* [Cree sus fragmentos de contenido](#creating-a-content-fragment).
* A continuación, abra el [Editor de fragmentos de contenido](#opening-the-fragment-editor) para [crear su contenido y administrar sus variaciones](#editing-the-content-of-your-fragment).
* [Administrar etiquetas](#manage-tags)
* [Ver y editar las propiedades (metadatos)](#viewing-and-editing-properties)
* [Ver el árbol de la estructura](/help/sites-cloud/administering/content-fragments/authoring.md#structure-tree)

>[!NOTE]
>
>Se pueden utilizar fragmentos de contenido:
>
>* para [Entrega de contenido sin encabezado mediante fragmentos de contenido con GraphQL](/help/sites-cloud/administering/content-fragments/content-delivery-with-graphql.md),
>* al crear páginas; consulte [Creación de páginas con fragmentos de contenido](/help/sites-cloud/authoring/fragments/content-fragments.md).

>[!NOTE]
>
>Los fragmentos de contenido se almacenan como **Recursos**. Se administran principalmente desde la consola **Fragmentos de contenido**, pero también se puede administrar desde la consola [Recursos](/help/assets/content-fragments/content-fragments-managing.md).

## Estructura básica y administración de fragmentos de contenido en la consola {#basic-structure-handling-content-fragments-console}

Puede usar el panel del extremo izquierdo de la consola [Fragmentos de contenido](/help/sites-cloud/administering/content-fragments/overview.md#content-fragments-console) para seleccionar **Fragmentos de contenido** como tipo de recurso para ver, examinar y administrar:

![Consola de fragmentos de contenido: navegación](/help/sites-cloud/administering/content-fragments/assets/cf-console-fragments-navigation.png)

Al seleccionar **Fragmentos de contenido**, se abre la consola en una nueva pestaña.

![Consola Fragmentos de contenido: información general](assets/cf-managing-console-overview.png)

Aquí se pueden ver tres áreas principales:

* La barra de herramientas superior
   * Proporciona funcionalidad AEM estándar
   * También muestra su organización IMS
   * Proporciona varias [acciones](#actions-unselected)
* El panel izquierdo
   * Aquí puede comprimir o expandir los vínculos a los paneles
   * Aquí puede ocultar o mostrar el árbol de carpetas
   * Puede seleccionar una rama específica del árbol
   * Se puede cambiar el tamaño para mostrar carpetas anidadas
   * Además de los fragmentos de contenido, puede ver [Modelos de fragmentos de contenido](/help/sites-cloud/administering/content-fragments/managing-content-fragment-models.md) o [Assets](/help/sites-cloud/administering/content-fragments/assets-content-fragments-console.md); también puede comprimir o expandir los vínculos a los paneles
* Panel principal/derecho, desde aquí puede hacer lo siguiente:
   * Consulte la lista de todos los fragmentos de contenido en la rama seleccionada del árbol:
      * Se mostrarán los fragmentos de contenido de la carpeta seleccionada y todas las carpetas secundarias:
         * La ubicación se indica mediante las rutas de exploración; también se pueden utilizar para cambiar la ubicación:
      * [Se muestra información sobre cada fragmento](#information-content-fragments)
         * [Puede seleccionar qué columnas mostrar](#select-columns-console)
      * [Varios campos de información](#information-content-fragments) acerca de un fragmento de contenido para proporcionar vínculos; según el campo, pueden realizar lo siguiente:
         * Abrir el fragmento correspondiente en el editor
         * Mostrar información sobre referencias
         * Mostrar información sobre las versiones de idioma del fragmento
      * [Otros campos de información](#information-content-fragments) acerca de un fragmento de contenido se pueden usar para [Filtrado rápido](#fast-filtering):
         * Seleccione un valor en la columna y se aplicará inmediatamente como filtro
         * Se admite el filtrado rápido para las columnas **Modelo**, **Estado**, **Modificado por**, **Etiquetas** y **Publicado por**.
      * Al utilizar el ratón sobre los encabezados de columna, se mostrará un selector de acciones desplegable y controles deslizantes de anchura. Esto le permite lograr lo siguiente:
         * Ordenar: seleccione la acción adecuada, ya sea ascendente o descendente.
Así se ordenará toda la tabla según esa columna. La ordenación solo está disponible en las columnas adecuadas.
         * Cambiar el tamaño de la columna: mediante los controles deslizantes de acción o de anchura
      * Seleccione uno o más fragmentos para realizar más [acción](#actions-selected-content-fragment)
   * Usar el cuadro [Buscar](#searching-fragments)
   * Abrir el [panel Filtro](#filtering-fragments)
   * Hay una selección de [métodos abreviados de teclado](/help/sites-cloud/administering/content-fragments/keyboard-shortcuts.md) disponibles para usar en esta consola

## La información proporcionada sobre sus fragmentos de contenido {#information-content-fragments}

El panel principal/derecho (vista de tabla) de la consola proporciona una amplia gama de información sobre los Fragmentos de contenido. Algunos elementos también proporcionan vínculos directos a otras acciones o información:

* **Nombre**
   * Proporciona un vínculo para abrir el fragmento en el editor.
* **Modelo**
   * Solo información.
   * Se puede usar para [Filtrado rápido](#fast-filtering)
* **Carpeta**
   * Proporciona un vínculo para abrir la carpeta en la consola.
Al pasar el puntero por encima del nombre de la carpeta, se muestra la ruta JCR.
* **Estado**
   * Solo información.
   * Se puede usar para [Filtrado rápido](#fast-filtering)
* **Vista previa**
   * Solo información:
      * **Sincronizado**: el fragmento de contenido está sincronizado con los servicios de **Autor** y **Previsualización**.
      * **Fuera de sincronización**: el fragmento de contenido no está sincronizado con los servicios de **Autor** y **Previsualización**. Es necesario **Publicar** para **Previsualizar** para garantizar que las dos instancias vuelvan a estar sincronizadas.
      * en blanco: El fragmento de contenido no existe en el servicio de **Previsualización**.
* **Modificado**
   * Solo información.
* **Modificado por**
   * Solo información.
   * Se puede usar para [Filtrado rápido](#fast-filtering).
* **Etiquetas**
   * Solo información.
   * Muestra todas las etiquetas relacionadas con el fragmento de contenido; tanto Principal como cualquier variación.
   * Se puede usar para [Filtrado rápido](#fast-filtering).
* **Publicado en**
   * Solo información.
* **Publicado por**
   * Solo información.
   * Se puede usar para [Filtrado rápido](#fast-filtering).
* **Referido Por**:
   * Proporciona un vínculo que abre un cuadro de diálogo con todas las [referencias principales](#parent-references-fragment) de ese fragmento; incluida la referencia a fragmentos de contenido, fragmentos de experiencias y páginas. Para abrir una referencia específica, haga clic en **Título** en el cuadro de diálogo.

     ![Consola Fragmentos de contenido: cuadro de diálogo Referencias](assets/cf-managing-console-references-dialog.png)

* **Idioma**: indique cualquier [idioma](#language-copies-fragment) copias

   * Indica la configuración regional del fragmento de contenido, junto con el número total de copias locales/[Idioma](#language-copies-fragment) asociadas con el fragmento de contenido.

     ![Consola Fragmentos de contenido: Indicador de idioma](assets/cf-managing-console-language-indicator.png)

   * Seleccione el recuento para abrir un cuadro de diálogo que muestre todas las copias de idioma. Para abrir una copia de idioma específica, haga clic en **Título** en el cuadro de diálogo.

     ![Consola Fragmentos de contenido: cuadro de diálogo Idioma](assets/cf-managing-console-languages-dialog.png)

## Acciones {#actions}

Dentro de la consola hay una serie de acciones que puede utilizar, ya sea directamente o después de seleccionar un fragmento específico:

* Varias acciones están [disponibles desde la consola](#actions-unselected) directamente
* Puede [seleccionar uno o varios fragmentos de contenido para mostrar las acciones disponibles](#actions-selected-content-fragment)

### Acciones (sin seleccionar) {#actions-unselected}

Algunas acciones están disponibles desde la consola, sin seleccionar un fragmento de contenido específico:

* **[Crear](#creating-a-content-fragment)** un nuevo fragmento de contenido
* [Filtrar](#filtering-fragments) los fragmentos de contenido de acuerdo con una selección de predicados y guardar el filtro para uso futuro
* [Buscar](#searching-fragments) los fragmentos de contenido
* [Personalice la vista de tabla para mostrar columnas de información seleccionadas](#select-columns-console)
* Use **Abrir en Recursos** para abrir directamente la ubicación actual en la consola **Recursos**

  >[!NOTE]
  >
  >La consola **Assets** se usa para acceder a recursos como imágenes, vídeos, etc.  Se puede acceder a esta consola:
  >
  >* usando el vínculo **Abrir en Recursos** (en la consola Fragmentos de contenido)
  >* directamente desde el panel **Navegación** global

### Acciones para un fragmento de contenido (seleccionado) {#actions-selected-content-fragment}

Al seleccionar un fragmento específico, se abre una barra de herramientas centrada en las acciones disponibles para dicho fragmento. También puede seleccionar varios fragmentos: la selección de acciones se ajustará en consecuencia.

![Consola Fragmentos de contenido: barra de herramientas para un fragmento seleccionado](assets/cf-managing-console-fragment-toolbar.png)

* **[Abrir en nuevo editor](#editing-the-content-of-your-fragment)**
* **[Publicación](#publishing-and-previewing-a-fragment)** (y **[Cancelar la publicación](#unpublishing-a-fragment)**)
* **[Administrar etiquetas](#manage-tags)**
* **[Copiar](#copy-a-content-fragment)**
* **[Reemplazar](#find-and-replace)**
* **Mover**
* **Cambiar nombre**
* **[Eliminar](#deleting-a-fragment)** (solo disponible para fragmentos sin publicar)


>[!NOTE]
>
>Use **Abrir** para abrir el fragmento seleccionado en el editor *original*.

>[!NOTE]
>
>Acciones como Publicar, Cancelar la publicación, Eliminar, Mover, Cambiar el nombre y Copiar cada déclencheur en un trabajo asincrónico. El progreso de ese trabajo se puede monitorizar a través de la interfaz de usuario de trabajos asincrónicos de AEM.

## Creación de fragmentos de contenido {#creating-content-fragments}

Antes de crear el fragmento de contenido, se debe crear el modelo de fragmento de contenido subyacente.

### Creación de un modelo de contenido {#creating-a-content-model}

[Los modelos de fragmentos de contenido](/help/sites-cloud/administering/content-fragments/managing-content-fragment-models.md) deben habilitarse y crearse antes de crear fragmentos de contenido con contenido estructurado.

### Creación de un fragmento de contenido {#creating-a-content-fragment}

Crear un fragmento de contenido:

1. En la consola **Fragmentos de contenido**, seleccione **Crear** (parte superior derecha).

   >[!NOTE]
   >
   >Para que la ubicación del nuevo fragmento esté predefinida, puede desplazarse a la carpeta en la que desee crear el fragmento o especificar la ubicación durante el proceso de creación.

1. Se abre el cuadro de diálogo **Nuevo fragmento de contenido**, desde donde puede especificar lo siguiente:

   * **Ubicación**: completado automáticamente con la ubicación actual, pero puede seleccionar una ubicación diferente si es necesario.
   * **Modelo de fragmento de contenido**: seleccione el modelo que se utilizará como base del fragmento en la lista desplegable.
   * **Etiqueta automática**: al seleccionar esta opción, todas las etiquetas asignadas al modelo de fragmento de contenido las hereda y se agregan al nuevo fragmento de contenido.
   * **Título**
   * **Nombre** - Completado automáticamente según el **Título**, pero puede editarlo si es necesario.
   * **Descripción**

   ![Nuevo cuadro de diálogo Fragmento de contenido](assets/cf-managing-new-cf-dialog.png)

1. Seleccione **Crear** o **Crear y abrir** para mantener la definición.

## Estados de los fragmentos de contenido {#statuses-content-fragments}

Durante su existencia, un fragmento de contenido puede tener varios estados, como se muestra en la [Consola de fragmento de contenido](/help/sites-cloud/administering/content-fragments/overview.md#content-fragments-console) y en el [Editor de fragmentos de contenido](/help/sites-cloud/administering/content-fragments/authoring.md):

* **Nuevo** (gris)
Se ha creado un nuevo fragmento de contenido, pero no tiene contenido, ya que nunca se ha editado ni abierto en el editor de fragmentos de contenido.
* **Borrador** (azul)
Alguien ha editado o abierto el fragmento de contenido (nuevo) en el Editor de fragmentos de contenido, pero aún no se ha publicado.
* **Publicado** (verde)
El fragmento de contenido se ha publicado.
* **Modificado** (naranja)
El fragmento de contenido se ha editado después de publicarse (pero antes de publicar la modificación).
* **Sin publicar** (rojo)
Se ha cancelado la publicación del fragmento de contenido.

## Edición del contenido del fragmento (y variaciones) {#editing-the-content-of-your-fragment}

>[!IMPORTANT]
>
>Para obtener información detallada, [consulte Creación de fragmentos de contenido](/help/sites-cloud/administering/content-fragments/authoring.md)

Abra el fragmento para su edición:

1. Utilice la consola **Fragmentos de contenido** para desplazarse a la ubicación del fragmento de contenido.
1. Abra el fragmento para editarlo; para ello, seleccione el fragmento y **Abrir en nuevo editor** en la barra de herramientas.

1. Se abrirá el editor de fragmentos. Seleccione la **variación** que necesite y realice los cambios según sea necesario (se guardarán automáticamente):

   ![Editor de fragmentos](assets/cf-managing-editor.png)

## Copiar un fragmento de contenido {#copy-a-content-fragment}

<!--
**Copy** creates a copy of the selected fragment at its location.

* In the **Copy** action you can select whether to **Copy with children** (referenced fragments). This allows you to copy both the selected Content Fragment and all referenced fragments. AEM:

  * Creates a copy of the selected Content Fragment at its location.
  * Creates copies of all fragments that are referenced by the selected fragment; these are copied to the same location as the original referenced fragment.

* The copy of the selected fragment will reference the copies of the referenced fragments.

* A deep copy is made; so if a referenced Content Fragment also references fragments, these are copied as well.

* The **Copy** action does not affect other referenced content, such as assets or images. The reference (Content Reference) is copied as part of the new fragment, but not the asset/image content itself.

So, if we start with:

```xml
FolderA 
    FragmentA (inside FolderA)
    | 
    |___FolderB/FragmentB (referenced by FragmentA)

FolderB
   FragmentB
```

Copying FragmentA to FolderC, would result in:

```xml
FolderA 
    FragmentA (inside FolderA)
    | 
    |___FolderB/FragmentB (referenced by FragmentA)

FolderB
    FragmentB
    Copy_of_FragmentB

FolderC
    Copy_of_FragmentA
    | 
    |___FolderB/Copy_of_FragmentB (referenced by Copy_of_FragmentA)
```
-->

<!-- CQDOC-22785 - will replace above text -->

**Copiar** crea una copia del fragmento seleccionado en su ubicación.

* En la acción **Copiar** puede seleccionar si desea **Copiar también los fragmentos de contenido a los que se hace referencia**. Esto le permite copiar el fragmento de contenido seleccionado y todos los fragmentos referenciados. AEM:

   * Crea una copia del fragmento de contenido seleccionado en su ubicación.
   * Crea copias de todos los fragmentos a los que hace referencia el fragmento seleccionado.

     Las [ubicaciones en las que se copian los fragmentos a los que se hace referencia](#locations-that-the-referenced-fragments-are-copied-to) dependen de la opción que seleccione:

      * **Copiar a la carpeta seleccionada**
Cuando se seleccionan, los fragmentos a los que se hace referencia se copian en la misma ubicación que el fragmento seleccionado original.

      * **Copiar a sus ubicaciones originales**
Los fragmentos a los que se hace referencia se copian en la misma ubicación que el fragmento original al que se hace referencia. Esta es la opción predeterminada y se utilizará cuando no se seleccione ninguna opción.

* La copia del fragmento seleccionado hará referencia a las copias de los fragmentos a los que se hace referencia.

* Se realiza una copia profunda, por lo que si un fragmento de contenido al que se hace referencia también hace referencia a fragmentos, estos también se copian.

* La acción **Copiar** no afecta a otro contenido al que se hace referencia, como recursos o imágenes. La referencia (referencia de contenido) se copia como parte del nuevo fragmento, pero no el propio contenido del recurso o la imagen.

### Ubicaciones en las que se copian los fragmentos referenciados {#locations-that-the-referenced-fragments-are-copied-to}

Al copiar fragmentos de contenido, puede especificar dónde se deben copiar los fragmentos a los que se hace referencia con **Copiar también los fragmentos de contenido a los que se hace referencia** y las opciones relacionadas:

![Copiar fragmentos](/help/sites-cloud/administering/content-fragments/assets/cf-managing-copy.png)

#### Copiar a sus ubicaciones originales {#copy-to-their-original-locations}

Al seleccionar **Copiar a sus ubicaciones originales**, los fragmentos a los que se hace referencia se copian en la misma ubicación que el fragmento original al que se hace referencia. Esta es también la acción predeterminada cuando no se realiza ninguna selección.

Por lo tanto, si empezamos con:

```xml
FolderA 
    FragmentA (inside FolderA)
    | 
    |___FolderB/FragmentB (referenced by FragmentA)

FolderB
   FragmentB
```

Copiar el fragmento A en la carpeta C resultaría en lo siguiente:

```xml
FolderA 
    FragmentA (inside FolderA)
    | 
    |___FolderB/FragmentB (referenced by FragmentA)

FolderB
    FragmentB
    Copy_of_FragmentB

FolderC
    Copy_of_FragmentA
    | 
    |___FolderB/Copy_of_FragmentB (referenced by Copy_of_FragmentA)
```

#### Copiar a la carpeta seleccionada {#copy-to-the-selected-folder}

Cuando se seleccionan, los fragmentos a los que se hace referencia se copian en la misma ubicación que el fragmento seleccionado original.

Por lo tanto, si empezamos con:

```xml
FolderA 
    FragmentA (inside FolderA)
    | 
    |___FolderB/FragmentB (referenced by FragmentA)


FolderB
   FragmentB
```

Copiar el fragmento A en la carpeta C resultaría en lo siguiente:

```xml
FolderA 
    FragmentA (inside FolderA) 
    | 
    |___FolderB/FragmentB (referenced by FragmentA) 

FolderB 
    FragmentB


FolderC
   Copy_of_FragmentA
   | 
   |___./Copy_of_FragmentB (referenced by FragmentA)
   Copy_of_FragmentB
```

## Ver y administrar etiquetas {#manage-tags}

Desde la consola Fragmentos de contenido puede ver cualquier etiqueta aplicada en la columna **Etiquetas**; después de asegurarse de que [se muestre la columna](#select-columns-console).

### Administración de etiquetas (consola) {#manage-tags-console}

Para administrar las etiquetas:

1. Vaya a la consola Fragmento de contenido.
1. Seleccione un fragmento de contenido.
1. Seleccione **Administrar etiquetas** en la barra de herramientas.
1. Utilice el selector de etiquetas para seleccionar las etiquetas que desea aplicar o quitar:

   ![Administrar etiquetas](assets/cf-managing-manage-tags.png)

1. **Guardar** actualizaciones. Esto le devolverá a la consola.

### Visualización y edición de etiquetas (editor) {#viewing-and-editing-tags}

También puede ver y editar las etiquetas aplicadas a un fragmento mediante la ficha [Propiedades](/help/sites-cloud/administering/content-fragments/authoring.md) del editor. La información mostrada difiere entre **Principal** y cualquier **variación**.

## Visualización y edición de propiedades (Editor) {#viewing-and-editing-properties}

Puede ver y editar las propiedades (metadatos) de un fragmento utilizando la pestaña [Propiedades](/help/sites-cloud/administering/content-fragments/authoring.md) del editor. La información mostrada difiere entre **Principal** y cualquier **variación**.

## Publicación y previsualización de un fragmento {#publishing-and-previewing-a-fragment}

Puede publicar los fragmentos de contenido en:

* el **[Servicio de publicación](/help/headless/deployment/architecture.md)**: para acceso público y completo

* el **[Servicio de previsualización](/help/headless/deployment/architecture.md)**: para previsualizar el contenido antes de la disponibilidad completa

  >[!CAUTION]
  >
  >La publicación de fragmentos de contenido en el **servicio de vista previa** solo está disponible desde la consola Fragmentos de contenido; se utiliza la acción **Publicar**.

  >[!NOTE]
  >
  >Para obtener más información acerca de los entornos de vista previa, vea [Administrar entornos](/help/implementing/cloud-manager/manage-environments.md#access-preview-service).

>[!CAUTION]
>
>Si el fragmento se basa en un modelo, debe asegurarse de que [el modelo se ha publicado](/help/sites-cloud/administering/content-fragments/managing-content-fragment-models.md#publishing-a-content-fragment-model).
>
>Si publica un fragmento de contenido para el que el modelo aún no se ha publicado, la lista de selección lo indicará y el modelo se publicará con el fragmento.

### Publicación {#publishing}

Puede publicar los fragmentos de contenido usando la opción **Publicar** desde las ubicaciones siguientes:

* la barra de herramientas de la [consola Fragmentos de contenido](#actions-selected-content-fragment)

   * Seleccione uno o varios fragmentos de la lista.

* la barra de herramientas del [editor de fragmentos de contenido](/help/sites-cloud/administering/content-fragments/authoring.md#content-fragment-editor)

Después de seleccionar la acción **Publicar**:

1. Seleccione cualquiera de las siguientes opciones para abrir el cuadro de diálogo correspondiente:

   * **Ahora**: seleccione la opción **Servicio de publicación**, o el **Servicio de previsualización**; después de la confirmación, el fragmento se publicará inmediatamente
   * **Programación**: además del servicio requerido, también puede seleccionar la fecha y la hora de publicación del fragmento

1. Proporcione todos los detalles en el cuadro de diálogo. Por ejemplo, para una solicitud de publicación programada:

   ![Cuadro de diálogo Publicar](assets/cf-managing-publish-dialog.png)

   >[!NOTE]
   >
   >Si es necesario, se le solicitará que especifique las referencias para publicar. De forma predeterminada, las referencias también se publican en el servicio de previsualización para garantizar que no haya ninguna interrupción en el contenido.

1. Confirme la acción de publicación.

Después de la publicación, el estado del fragmento se actualiza y es visible en el editor y la consola. Si ha especificado una publicación programada, se mostrará información.

>[!NOTE]
>
>Además, cuando [publique una página que utiliza el fragmento](/help/sites-cloud/authoring/fragments/content-fragments.md#publishing); el fragmento se enumerará en las referencias de página.

## Cancelación de la publicación de un fragmento {#unpublishing-a-fragment}

Puede cancelar la publicación de fragmentos de contenido:

* la barra de herramientas de la [consola Fragmentos de contenido](#actions-selected-content-fragment)

   * Seleccione uno o varios fragmentos de la lista.

* la barra de herramientas del [editor de fragmentos de contenido](/help/sites-cloud/administering/content-fragments/authoring.md#content-fragment-editor)

En ambos casos, seleccione **Cancelar la publicación** en la barra de herramientas, seguido de **Ahora** o **Programado**.

Cuando se abra el cuadro de diálogo correspondiente, puede seleccionar el servicio adecuado:

![Cancelar publicación del cuadro de diálogo](assets/cf-managing-unpublish-dialog.png)

>[!NOTE]
>
>La acción **Cancelar la publicación** solo estará visible cuando los fragmentos publicados estén disponibles.

>[!CAUTION]
>
>Si ya se hace referencia al fragmento desde otro fragmento o desde una página, verá un mensaje de advertencia y será necesario para confirmar que desea continuar.

## Buscar y reemplazar {#find-and-replace}

La acción **Reemplazar** está disponible (en la barra de herramientas superior) para buscar y reemplazar el texto especificado en los fragmentos de contenido seleccionados.

![Buscar y reemplazar](assets/cf-managing-find-replace.png)

Antes del reemplazo, se comprueban los criterios de validación y se le informa de cualquier conflicto, lo que le permite cambiar la cadena de reemplazo o reemplazar únicamente las instancias validadas.

>[!NOTE]
>
>La acción de buscar y reemplazar solo se puede realizar en un máximo de 20 fragmentos de contenido seleccionados (a la vez).
>
>Si selecciona más de 20 fragmentos de contenido, verá el mensaje **No se puede encontrar y reemplazar**.

![Confirmar reemplazo](assets/cf-managing-confirm-replace.png)

## Eliminación de un fragmento {#deleting-a-fragment}

Para eliminar un fragmento:

1. En la consola **Fragmentos de contenido** vaya a la ubicación del fragmento de contenido.
1. Seleccione el fragmento.
1. En la barra de herramientas, seleccione **Eliminar**.
1. Confirme la acción **Eliminar**.

>[!NOTE]
>
>**Eliminar** no está disponible para los fragmentos que están publicados actualmente; primero se debe cancelar su publicación.

## Búsqueda de referencias principales de su fragmento {#parent-references-fragment}

Se puede acceder a los detalles de las referencias principales desde el

* Columna **Referencias** de la consola Fragmentos de contenido
* el vínculo [referencias principales en la barra de herramientas superior del editor de fragmentos de contenido](/help/sites-cloud/administering/content-fragments/authoring.md#view-parent-references)

Ambos proporcionan un vínculo que abre un cuadro de diálogo con todas las referencias principales de ese fragmento; incluida la referencia a fragmentos de contenido, fragmentos de experiencias y páginas. Para abrir una referencia específica, haga clic en **Título** o en el icono de vínculo del cuadro de diálogo.

Por ejemplo:

![Consola Fragmentos de contenido: cuadro de diálogo Referencias](assets/cf-managing-console-references-dialog.png)

## Búsqueda de copias de idioma del fragmento {#language-copies-fragment}

Se puede acceder a los detalles de las copias de idioma desde:

* la columna **Idioma** de la consola [Fragmentos de contenido](#information-content-fragments)
* la pestaña [Copias de idioma del editor de fragmentos de contenido](/help/sites-cloud/administering/content-fragments/authoring.md#view-language-copies)

El icono indica la configuración regional del fragmento de contenido, junto con el número total de configuraciones regionales o copias de idioma asociadas al fragmento de contenido. Por ejemplo, desde la consola:

![Consola Fragmentos de contenido: Indicador de idioma](assets/cfc-console-language-indicator.png)

Seleccione el recuento para abrir un cuadro de diálogo que muestre todas las copias de idioma. Para abrir una copia de idioma específica, haga clic en **Título** en el cuadro de diálogo.

![Consola Fragmentos de contenido: cuadro de diálogo Idioma](assets/cf-managing-console-languages-dialog.png)

## Seleccionar columnas mostradas en la consola {#select-columns-console}

Al igual que con otras consolas, puede configurar las columnas que son visibles y están disponibles para la acción:

![Consola Fragmentos de contenido: configuración de columna](assets/cf-managing-console-column-icon.png)

Se mostrará una lista de columnas que puede ocultar o mostrar:

![Consola Fragmentos de contenido: configuración de columna](assets/cf-managing-console-column-selection.png)

## Filtrado de fragmentos {#filtering-fragments}

El panel Filtro ofrece lo siguiente:

* una selección de predicados;
   * incluyendo modelos de fragmentos de contenido, localización, etiquetas, campos de estado, entre otros
   * se pueden seleccionar uno o más predicados y combinarlos para crear el filtro
* **Excluir elementos de subcarpeta**, lo que le ofrece la opción de excluir fragmentos de contenido almacenados en subcarpetas
* la oportunidad de **Guardar** su configuración
* la opción recuperar un filtro de búsqueda guardada para reutilizarlo

Una vez seleccionadas, se muestran las opciones **Filtrando por** (debajo del cuadro Buscar). Se pueden anular las selecciones desde allí. Por ejemplo:

![Consola Fragmentos de contenido: filtrado](assets/cf-managing-console-filter.png)

### Filtrado rápido {#fast-filtering}

También puede seleccionar un predicado haciendo clic en un valor de columna específico de la lista. Puede seleccionar uno o más valores para combinar predicados.

Por ejemplo, seleccione **Publicado** en la columna **Estado**:

>[!NOTE]
>
>El filtrado rápido solo es compatible con las columnas **Modelo**, **Estado**, **Modificado por**, **Etiquetas** y **Publicado por**.

![Consola Fragmentos de contenido: filtrado](assets/cf-managing-console-fast-filter-overview.png)

Cuando se seleccione, aparecerá como un predicado de filtro y la lista se filtrará según corresponda:

![Consola Fragmentos de contenido: filtrado](assets/cf-managing-console-fast-filter-criteria.png)

## Búsqueda de fragmentos {#searching-fragments}

El cuadro de búsqueda admite la búsqueda de texto completo. Introducción de los términos de búsqueda en el cuadro de búsqueda:

![Consola Fragmentos de contenido: búsqueda](assets/cf-managing-console-search-specification.png)

Proporcionará los resultados seleccionados:

![Consola Fragmentos de contenido: resultados de búsqueda](assets/cf-managing-console-search-results.png)

El cuadro de búsqueda también proporciona acceso rápido a **Fragmentos de contenido recientes** y **Búsquedas guardadas**:

![Consola Fragmentos de contenido: reciente y guardado](assets/cf-managing-console-search-saved.png)
