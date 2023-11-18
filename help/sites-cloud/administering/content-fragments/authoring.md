---
title: Creación de fragmentos de contenido
description: Obtenga información sobre cómo crear contenido para los fragmentos de contenido y, a continuación, crear variaciones de ese contenido según el propósito. Esto proporciona una mayor flexibilidad para la entrega sin encabezado y la creación de páginas.
feature: Content Fragments
role: User, Developer, Architect
exl-id: a2f2b617-3bdf-4a22-ab64-95f2c65adc82
source-git-commit: 6bb7b2d056d501d83cf227adb239f7f40f87d0ce
workflow-type: tm+mt
source-wordcount: '2251'
ht-degree: 4%

---

# Creación de fragmentos de contenido {#authoring-content-fragments}

La creación de los fragmentos de contenido se centra en la entrega sin encabezado y en la creación de páginas.

Hay dos editores disponibles para los fragmentos de contenido. El editor se describe en esta sección:

* se ha desarrollado para la entrega de contenido sin encabezado (aunque se puede utilizar en todos los casos)
* está disponible en el **Fragmentos de contenido** consolar

Este editor proporciona lo siguiente:

* [Guardado automático](#saving-autosaving), para evitar la pérdida accidental de ediciones.
* [Carga en línea de recursos como referencias de contenido](#reference-images), sin tener que cargarlos primero en el DAM de recursos.
* [Previsualizar](#preview-content-fragment) de la experiencia procesada por el fragmento de contenido.
* Capacidad para [Publish](#publish-content-fragment) y [Cancelar publicación](#unpublish-content-fragment) del editor.
* Capacidad para [ver y abrir copias de idioma asociadas](#view-language-copies) en el editor.
* Capacidad para [ver detalles de la versión](#view-version-history) en el editor. También puede revertir a una versión seleccionada.
* Capacidad para [ver y abrir referencias principales](#view-parent-references).
* Una vista jerárquica del fragmento de contenido y sus referencias, con el [Árbol de estructura](#structure-tree).

>[!WARNING]
>
>El editor descrito en esta sección es *solamente* disponible en el *en línea* Adobe Experience Manager AEM () as a Cloud Service.

## Editor de fragmentos de contenido {#content-fragment-editor}

Cuando abra el Editor de fragmentos de contenido por primera vez, verá cuatro áreas principales:

* barra de herramientas superior: para obtener información clave y acciones
   * un vínculo a la consola Fragmento de contenido (icono de Inicio)
   * información sobre el modelo y la carpeta
   * vínculos a [Vista previa (si el Patrón de URL de vista previa predeterminado está configurado para el modelo)](/help/sites-cloud/administering/content-fragments/content-fragment-models.md#content-fragment-model-properties)
   * [Publish](#publish-content-fragment), y [Cancelar publicación](#unpublish-content-fragment) acciones
   * una opción para mostrar todo **Referencias principales** (icono de vínculo)
   * el fragmento **[Estado](/help/sites-cloud/administering/content-fragments/managing.md#statuses-content-fragments)** y la información guardada por última vez
   * un conmutador para cambiar al editor original (basado en recursos)

     >[!WARNING]
     >
     >El editor original se abre en la misma pestaña. No se recomienda tener ambos editores abiertos al mismo tiempo.

* panel izquierdo: muestra el **[Variaciones](#variations)** para el fragmento de contenido y su **Campos**:
   * estos vínculos se pueden utilizar para lo siguiente: [Navegar por la estructura de fragmentos de contenido](#navigate-structure)
* panel derecho: presenta pestañas [mostrar las propiedades (metadatos) y etiquetas](#view-properties-tags), información acerca de [historial de versiones](#view-version-history), e información relacionada con cualquier [copias de idioma](#view-language-copies)
   * en el **Propiedades** puede actualizar la pestaña **Título** y **Descripción** para el fragmento, o **Variación**
* panel central: muestra los campos y el contenido reales de la variación seleccionada
   * le permite editar el contenido
   * if **Marcador de ficha** Los campos de se definen dentro del modelo que se muestra aquí y pueden utilizarse para navegar; se presentarán horizontalmente o como una lista desplegable.

![Editor de fragmentos de contenido: información general](assets/cf-authoring-overview.png)

## Navegar por la estructura de fragmentos de contenido {#navigate-structure}

Un solo fragmento de contenido;

* Consta de dos niveles:

   * **[Variaciones](#variations)** del fragmento de contenido
   * **Campos** : definido por el Modelo de fragmento de contenido y utilizado por cada variación

* Puede contener diversas referencias.

### Variaciones y campos {#variations-and-fields}

En el panel izquierdo puede ver lo siguiente:

* la lista de **[Variaciones](#variations)** que se han creado para este fragmento:
   * **Principal** es la variación que está presente cuando se crea el fragmento de contenido por primera vez y puede agregar otras más adelante
   * puede seleccionar y abrir una variación para editarla
   * también puede [crear una variación](#create-variation)
* el **Campos** dentro del fragmento y sus variaciones:
   * el icono indica la [Tipo de datos](/help/sites-cloud/administering/content-fragments/content-fragment-models.md#data-types)
   * el texto es el nombre del campo
   * juntos, proporcionan un vínculo directo al contenido del campo en el panel central (para la variación actual)

### Seguir vínculos {#follow-links}

En varias partes del editor puede ver el icono de vínculo. Se puede utilizar para abrir el elemento mostrado; por ejemplo, un modelo de fragmento de contenido, una referencia principal o un fragmento al que se hace referencia:

![Editor de fragmentos de contenido: icono de vínculo](assets/cf-authoring-link-icon.png)

### Árbol de estructura {#structure-tree}

Abra el **Árbol de estructura** de la barra de herramientas del editor para mostrar la estructura jerárquica del fragmento de contenido y sus referencias. Utilice los iconos de vínculo para desplazarse a las referencias.

![Editor de fragmentos de contenido: árbol de estructura](assets/cf-authoring-structure-tree.png)

>[!NOTE]
>
>Consulte [Análisis de la estructura del fragmento de contenido: árbol de estructura](/help/sites-cloud/administering/content-fragments/analysis.md#structure-tree) para obtener más información.

## Guardado y guardado automático {#saving-autosaving}

<!-- CHECK: cannot be saved, no undo, redo -->

Con cada actualización que realice, el fragmento de contenido se guardará automáticamente. La última vez que se guardó se muestra en la barra de herramientas superior.

## Variaciones {#variations}

[Variaciones](/help/sites-cloud/administering/content-fragments/overview.md#main-and-variations) AEM son una característica importante de los fragmentos de contenido de la. Permiten crear y editar copias del **Principal** contenido para su uso en canales y escenarios específicos, lo que hace que la entrega de contenido sin encabezado y la creación de páginas sean aún más flexibles.

Desde el editor puede:

* [Creación de variaciones](#create-variation) de la **Principal** content

* Seleccione la variación necesaria para editar el contenido

* [Cambie el nombre de la variación](#rename-variation)

* [Eliminar una variación](#delete-variation)

### Crear una variación {#create-variation}

Para crear una variación del fragmento de contenido:

1. En el panel izquierdo, seleccione **signo más** (**Crear variación**), a la derecha de **Variaciones**.

   >[!NOTE]
   >
   >Después de crear la primera variación, las variaciones existentes se enumerarán en el mismo panel.

   ![Editor de fragmentos de contenido: cree su primera variación](assets/cf-authoring-create-variation-01.png)

1. En el cuadro de diálogo, introduzca un **Título** para su variación y una **Descripción** si lo desea:

   ![Editor de fragmentos de contenido: cuadro de diálogo Crear variación](assets/cf-authoring-create-variation-02.png)

1. **Crear** la variación. Aparece en la lista.

### Cambiar nombre de variación {#rename-variation}

Para cambiar el nombre de un **Variación**:

1. Seleccione la variación requerida.

1. Abra el **Propiedades** en el panel derecho.

1. Actualizar la variación **Título**.

1. Pulse o **Volver** o desplácese a otro campo para guardar automáticamente el cambio. El título se actualiza en la **Variaciones** panel de la izquierda.


### Eliminar una variación {#delete-variation}

Para eliminar una variación del fragmento de contenido:

>[!NOTE]
>
>No puede eliminar **Principal**.

1. Seleccione la opción Variación.

1. En el **Variación** , seleccione el icono Eliminar (Papelera):

   ![Editor de fragmentos de contenido: icono Eliminar variación](assets/cf-authoring-delete-variation.png)

1. Se abre un cuadro de diálogo. Seleccionar **Eliminar** para confirmar la acción.

## Editar campos de texto multilínea: texto sin formato o Markdown {#edit-multi-line-text-fields-plaintext-markdown}

**[Texto de varias líneas](/help/sites-cloud/administering/content-fragments/content-fragment-models.md#data-types)** los campos pueden tener uno de estos tres formatos:

* Texto sin formato
* [Markdown](/help/sites-cloud/administering/content-fragments/markdown.md)
* [Texto enriquecido](#edit-multi-line-text-fields-rich-text)

Los campos definidos como Texto sin formato o Markdown tienen un cuadro de texto simple, sin opciones de formato (en pantalla):

![Editor de fragmentos de contenido: texto multilínea, pantalla completa](assets/cf-authoring-multilinetext-plaintext-markdown.png)

## Editar campos de texto multilínea: texto enriquecido {#edit-multi-line-text-fields-rich-text}

Para **[Texto de varias líneas](/help/sites-cloud/administering/content-fragments/content-fragment-models.md#data-types)** campos definidos como **Texto enriquecido**, hay varias funciones disponibles:

* Edite el contenido:
   * Deshacer, Rehacer
   * Pegar/pegar como texto
   * Copiar
   * Seleccionar formato de párrafo
   * Crear/administrar tabla
   * Dar formato al texto; negrita, cursiva, subrayado, color
   * Establecer alineación de párrafo
   * Crear/administrar listas; con viñetas, numeradas
   * Aplicar sangría al texto; disminuir, aumentar
   * Borrar formato actual
   * Insertar vínculos
   * Seleccionar e insertar referencias a recursos de imagen
   * Añadir caracteres especiales
* [Editor de pantalla completa](#full-screen-editor-rich-text) - alternar entre pantalla completa y flujo de entrada
* [Estadísticas](#statistics-rich-text)
* [Comparar y sincronizar](#compare-and-synchronize-rich-text)

Por ejemplo:

![Editor de fragmentos de contenido: texto multilínea, opción de pantalla completa](assets/cf-authoring-multilinetext-fullscreen-toggle.png)

>[!NOTE]
>
>Los campos de texto de varias líneas también se indican mediante el [icono](#fields-datatypes-icons) en el **Campos** panel.

### Editor de pantalla completa: texto enriquecido {#full-screen-editor-rich-text}

El editor de pantalla completa ofrece las mismas opciones de edición que cuando está en flujo, pero ofrece más espacio para el texto.

Por ejemplo:

![Editor de fragmentos de contenido: texto multilínea, pantalla completa](assets/cf-authoring-multilinetext-fullscreen.png)

### Estadísticas - Texto enriquecido {#statistics-rich-text}

La acción **Estadísticas** muestra un rango de información sobre el texto en un campo de líneas múltiples.

Por ejemplo:

![Editor de fragmentos de contenido: estadísticas](assets/cf-authoring-multilinetext-statistics.png)

### Comparar y sincronizar: texto enriquecido {#compare-and-synchronize-rich-text}

La acción **Comparar** está disponible para campos de varias líneas cuando tiene un **Variación** abra.

Esto abre el campo Multi line en pantalla completa y:

* muestra el contenido de ambos **Principal** y el actual **Variación** en paralelo, con las diferencias resaltadas

* las diferencias se indican mediante el color:

   * verde indica el contenido añadido (a la variación)
   * rojo indica que el contenido se ha eliminado (de la variación)
   * azul indica texto reemplazado

* proporciona el **Sincronización** acción, que sincroniza el contenido de **Principal** a la variación actual

   * if **Principal** se ha actualizado, estos cambios se transferirán a la variación
   * si la variación se ha actualizado, el contenido de sobrescribirá estos cambios **Principal**

  >[!CAUTION]
  >
  >La sincronización solo está disponible para copiar cambios *de **Principal**a la variación*.
  >
  >Transferencia de cambios *de una variación a **Principal*** no está disponible como opción.

Por ejemplo, en un escenario en el que el contenido de variación se había reescrito completamente, por lo que una sincronización reemplazará ese nuevo contenido con el contenido de **Principal**:

![Editor de fragmentos de contenido: comparar y sincronizar](assets/cf-authoring-multilinetext-compare.png)

## Administrar referencias {#manage-references}

### Referencias a fragmentos {#fragment-references}

[Referencias a fragmento](/help/sites-cloud/administering/content-fragments/content-fragment-models.md#fragment-reference-nested-fragments) se puede utilizar para:

* [crear una referencia a un fragmento de contenido existente](#create-reference-existing-content-fragment)
* [cree un fragmento de contenido y, a continuación, haga referencia a él](#create-reference-content-fragment)

#### Crear una referencia a un fragmento de contenido existente {#create-reference-existing-content-fragment}

Para crear una referencia a un fragmento de contenido existente:

1. Seleccione el campo.
1. Seleccionar **Añadir un fragmento existente**.
1. Seleccione el fragmento requerido en el selector de fragmentos.

   >[!NOTE]
   >
   >Solo se le permite seleccionar un fragmento a la vez.

#### Crear un fragmento de contenido y hacer referencia a {#create-reference-content-fragment}

Como alternativa, puede [select **Crear nuevo fragmento** para abrir **Crear** diálogo](/help/sites-cloud/administering/content-fragments/managing.md#creating-a-content-fragment). Una vez creado, se hará referencia a este fragmento.

### Referencias de contenidos {#content-references}

[Referencias de contenido](/help/sites-cloud/administering/content-fragments/content-fragment-models.md#content-reference) AEM se utilizan para hacer referencia a otros tipos de contenido de la, como imágenes, páginas y Fragmentos de experiencias.

#### Imágenes de referencia {#reference-images}

Entrada **Referencia de contenido** en los campos puede hacer lo siguiente:

* recursos de referencia que ya existen en el repositorio
* cargarlos directamente en el campo, lo que evita la necesidad de utilizar el **Assets** consola para cargar

  >[!NOTE]
  >
  >Para cargar directamente una imagen en **Referencia de contenido** field, it **debe**:
  >
  >* tiene un **Ruta raíz** definido (en el [Modelo de fragmento de contenido](/help/sites-cloud/administering/content-fragments/content-fragment-models.md#content-reference)). Esto especifica dónde se almacenará la imagen.
  >* include **Imagen** en la lista de tipos de contenido aceptados

Para agregar un recurso, puede hacer lo siguiente:

* arrastre y suelte el nuevo archivo de recursos directamente (por ejemplo, desde el sistema de archivos) en **Referencia de contenido** campo
* use el **Añadir recurso** acción, luego seleccione **Examinar recursos** o **Cargar** para abrir el selector correspondiente para que lo utilice:

  ![Editor de fragmentos de contenido: añadir opciones de recursos](assets/cf-authoring-add-asset-options.png)

#### Páginas de referencia {#reference-pages}

AEM Para agregar referencias a páginas de contenido, fragmentos de experiencias u otros tipos de contenido de la:

1. Seleccionar **Añadir ruta de contenido**.

1. Añada la ruta requerida en el campo de entrada.

1. Confirmar con **Añadir**.

### Ver referencias principales {#view-parent-references}

Al seleccionar el icono de vínculo en la barra de herramientas superior, se abre una lista de todas las referencias principales.

Por ejemplo:

![Editor de fragmentos de contenido: mostrar referencias](assets/cf-authoring-show-references-link.png)

Se abre una ventana con todas las referencias relacionadas. Para abrir una referencia, seleccione el nombre, el título o el icono de vínculo.

Por ejemplo:

![Editor de fragmentos de contenido: mostrar referencias](assets/cf-authoring-show-references.png)

## Ver propiedades y etiquetas {#view-properties-tags}

En la pestaña Propiedades del panel derecho, se pueden ver las propiedades (metadatos) y las etiquetas. Las propiedades pueden ser las siguientes:

* para el **Fragmento de contenido** - si **Principal** está seleccionado actualmente
* para un específico **Variación**

![Editor de fragmentos de contenido: propiedades](assets/cf-authoring-properties.png)

### Editar propiedades y etiquetas {#edit-properties-tags}

En la pestaña Propiedades (panel derecho), también puede editar:

* **Título**
* **Descripción**
* **Etiquetas**: mediante la lista desplegable o el cuadro de diálogo de selección

  ![Editor de fragmentos de contenido: administrar etiquetas](assets/cf-authoring-edit-tags.png)

### Abra el modelo de fragmento de contenido {#open-content-fragment-model}

Cuando tenga **Principal** Si se selecciona, el nombre del modelo de fragmento de contenido subyacente se muestra en la sección de propiedades. Al seleccionar el icono de vínculo, se abre el modelo en una pestaña independiente.

Por ejemplo:

![Editor de fragmentos de contenido: abrir el modelo de fragmentos de contenido](assets/cf-authoring-open-model.png)

## Ver el historial de versiones {#view-version-history}

En el **Historial de versiones** del panel derecho, se muestran los detalles de las versiones actuales y anteriores:

>[!NOTE]
>
>Se crea una nueva versión cuando se publica el fragmento de contenido.

![Editor de fragmentos de contenido: información general del historial de versiones](assets/cf-authoring-version-history-overview.png)

### Volver a esta versión {#revert-version}

Puede volver a cualquier versión.

Para volver a una versión específica:

1. Seleccione el icono de tres puntos junto a la versión.

1. Seleccionar **Revertir**.

![Editor de fragmentos de contenido: revertir historial de versiones](assets/cf-authoring-version-history-revert.png)

## Ver las copias de idioma {#view-language-copies}

En el **Propiedades de idioma** se muestran los detalles de las pestañas de cualquier copia de idioma relacionada. Al seleccionar un icono de vínculo, se abre la copia en una pestaña independiente.

Por ejemplo:

![Editor de fragmentos de contenido: abrir copia de idioma](assets/cf-authoring-open-language-copies.png)

>[!NOTE]
>
>Para obtener más información sobre la traducción de un fragmento de contenido y la creación de copias de idioma, consulte la [AEM Recorrido de traducción sin encabezado](/help/journey-headless/translation/overview.md).


## Previsualización del fragmento {#preview-content-fragment}

El editor de fragmentos de contenido proporciona a los autores la opción de previsualizar sus ediciones en una aplicación de front-end externa.

Para utilizar esta función, primero debe:

* Trabaje con su equipo de TI para configurar la aplicación de front-end externa que procesará el fragmento de contenido consumiendo su salida JSON.
* Cuando se configura la aplicación de front-end externa, la variable **Patrón de URL de previsualización predeterminado** debe definirse como [propiedad del modelo de fragmento de contenido adecuado](/help/sites-cloud/administering/content-fragments/content-fragment-models.md#properties).

Cuando se haya definido la dirección URL, la variable **Previsualizar** El botón está activo. Puede seleccionar este botón para iniciar la aplicación externa (en una pestaña independiente) para procesar el fragmento de contenido.

## Publicación del fragmento {#publish-content-fragment}

Puede **Publish** el fragmento a su:

* Previsualizar instancia
* Instancia de publicación

Puede publicar el fragmento desde el editor o desde la consola. Consulte [Publicación y previsualización de un fragmento](/help/sites-cloud/administering/content-fragments/managing.md#publishing-and-previewing-a-fragment) para obtener información detallada.

## Cancelar la publicación del fragmento {#unpublish-content-fragment}

También puede **Cancelar publicación** Seleccione el fragmento de su:

* Previsualizar instancia
* Instancia de publicación

Puede cancelar la publicación del fragmento desde el editor o desde la consola. Consulte [Cancelar la publicación de un fragmento](/help/sites-cloud/administering/content-fragments/managing.md#unpublishing-a-fragment) para obtener información detallada.

## Campos, tipos de datos e iconos {#fields-datatypes-icons}

El **Campos** el panel enumera todos los campos del fragmento de contenido. El icono indica el **[Tipo de datos](/help/sites-cloud/administering/content-fragments/content-fragment-models.md#data-types)**:

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><p><b>Texto de línea única</b></p> </td>
   <td><p> <img src="assets/cf-authoring-single-line-text-icon.png"> </p></td>
  </tr>
  <tr>
   <td><p><b>Texto multilínea</b></p> </td>
   <td><p> <img src="assets/cf-authoring-multi-line-text-icon.png"> </p></td>
  </tr>
  <tr>
   <td><p><b>Número</b></p> </td>
   <td><p> <img src="assets/cf-authoring-number-icon.png"> </p></td>
  </tr>
  <tr>
   <td><p><b>Booleano</b></p> </td>
   <td><p> <img src="assets/cf-authoring-boolean-icon.png"> </p></td>
  </tr>
  <tr>
   <td><p><b>Fecha y hora</b></p> </td>
   <td><p> <img src="assets/cf-authoring-date-time-icon.png"> </p></td>
  </tr>
  <tr>
   <td><p><b>Lista desglosada</b></p> </td>
   <td><p> <img src="assets/cf-authoring-enumeration-icon.png"> </p></td>
  </tr>
  <tr>
   <td><p><b>Etiquetas</b></p> </td>
   <td><p> <img src="assets/cf-authoring-tags-icon.png"> </p></td>
  </tr>
  <tr>
   <td><p><b>Referencia de contenido</b></p> </td>
   <td><p> <img src="assets/cf-authoring-content-reference-icon.png"> </p></td>
  </tr>
  <tr>
   <td><p><b>Referencia al fragmento</b></p> </td>
   <td><p> <img src="assets/cf-authoring-fragment-reference-icon.png"> </p></td>
  </tr>
  <tr>
   <td><p><b>Objeto JSON</b></p> </td>
   <td><p> <img src="assets/cf-authoring-json-icon.png"> </p></td>
  </tr>
  <tr>
   <td><p><b>Marcador de posición de pestaña</b></p><p>Aunque no se representa mediante un icono real, una variable <b>Marcador de ficha</b> se representa en el panel izquierdo. <br>También se representa en el panel central, ya sea horizontalmente como se muestra o en una lista desplegable (cuando hay demasiados para mostrar horizontalmente).</p> </td>
   <td><p> <img src="assets/cf-authoring-tab-icon.png"> </p></td>
  </tr>
 </tbody>
</table>

## Es bueno saber {#good-to-know}

* Para editar un fragmento de contenido, necesita lo siguiente [los permisos adecuados](/help/implementing/developing/extending/content-fragments-customizing.md#asset-permissions). Si tiene algún problema, póngase en contacto con el administrador del sistema.

  Por ejemplo, si no tiene `edit` permisos el editor será de solo lectura.

* Un modelo de fragmento de contenido puede definir con frecuencia campos de datos llamados **Título** y **Descripción**. Si existen, son campos definidos por el usuario que se pueden actualizar en la *panel central* al editar el fragmento.

  El fragmento de contenido y sus variaciones también tienen campos de metadatos (propiedades de variación) llamados **Título** y **Descripción**. Estos campos son parte integral de cualquier fragmento de contenido y se definen inicialmente al crear el fragmento. Se pueden actualizar en el *panel derecho* al editar el fragmento.

* Consulte la documentación de Assets para obtener información completa sobre [editor de fragmentos de contenido original](/help/assets/content-fragments/content-fragments-variations.md) - está disponible tanto en el **Assets** y la **Fragmentos de contenido** consola.

* El equipo del proyecto puede personalizar el editor si es necesario. Consulte [Personalización de la consola y el editor de fragmentos de contenido](/help/implementing/developing/extending/content-fragments-console-and-editor.md) para obtener más información.
