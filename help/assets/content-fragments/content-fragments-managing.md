---
title: 'Administración de fragmentos de contenido (Assets: fragmentos de contenido)'
description: Aprenda a utilizar la consola de Assets para administrar los fragmentos de contenido de AEM, como base del contenido sin encabezado o para la creación de páginas.
exl-id: 333ad877-db2f-454a-a3e5-59a936455932
feature: Content Fragments
role: User, Admin
solution: Experience Manager Sites
source-git-commit: 74e2f015d6bcb36505c2dc6471bb68d69d98db99
workflow-type: tm+mt
source-wordcount: '1925'
ht-degree: 63%

---

# Administración de los fragmentos de contenido {#managing-content-fragments}

Aprenda a utilizar la consola de Assets para administrar los fragmentos de contenido de AEM, como base del contenido sin encabezado o para la creación de páginas.

Después de definir los [Modelos de fragmento de contenido](#creating-a-content-model) puede utilizarlas para [crear los fragmentos de contenido](#creating-a-content-fragment).

El [Editor de fragmentos de contenido](#opening-the-fragment-editor) proporciona varios [modos](#modes-in-the-content-fragment-editor) para permitirle lo siguiente:

* [Editar el contenido](#editing-the-content-of-your-fragment) y [administrar variaciones](#creating-and-managing-variations-within-your-fragment)
* [Anotar el fragmento](/help/assets/content-fragments/content-fragments-variations.md#annotating-a-content-fragment)
* [Asociar contenido al fragmento](#associating-content-with-your-fragment)
* [Configuración de los metadatos](#viewing-and-editing-the-metadata-properties-of-your-fragment)
* [Ver el árbol de la estructura](/help/assets/content-fragments/content-fragments-structure-tree.md)
* [Previsualización de la representación JSON](/help/assets/content-fragments/content-fragments-json-preview.md)


>[!NOTE]
>
>Se pueden utilizar fragmentos de contenido:
>
>* al crear páginas; consulte [Creación de páginas con fragmentos de contenido](/help/sites-cloud/authoring/fragments/content-fragments.md).
>* para [Entrega de contenido sin encabezado mediante fragmentos de contenido con GraphQL](/help/assets/content-fragments/content-fragments-graphql.md).

>[!NOTE]
>
>Los fragmentos de contenido son una característica de **Sites**, pero se almacenan como **Assets**.
>
>Se administran principalmente con la consola **[Fragmentos de contenido](/help/sites-cloud/administering/content-fragments/overview.md#content-fragments-console)**, aunque aún se pueden administrar desde la consola **[Assets](/help/assets/content-fragments/content-fragments-managing.md)**.
>
>Existen dos editores para la creación de fragmentos de contenido: el nuevo editor y el editor original. El nuevo editor es el predeterminado. Aunque la funcionalidad básica es la misma, existen algunas diferencias.
>
>Esta sección trata sobre el editor original.
>
>El editor predeterminado para [Fragmentos de contenido: creación](/help/sites-cloud/administering/content-fragments/authoring.md) es el nuevo editor, al que se accede desde la consola **Fragmentos de contenido** y la consola **Assets**. Consulte la documentación de Sites, [Fragmentos de contenido: creación](/help/sites-cloud/administering/content-fragments/authoring.md), para obtener detalles del nuevo editor.
>
>Para usar el [editor original](/help/assets/content-fragments/content-fragments-variations.md), primero abre el nuevo editor y luego desactiva el conmutador **Nuevo editor**.
>
>Ambos editores tienen un conmutador en la barra de herramientas superior para proporcionar acceso rápido al otro editor.

## Creación de fragmentos de contenido {#creating-content-fragments}

### Creación de un modelo de contenido {#creating-a-content-model}

Los [Modelos de fragmento de contenido](/help/assets/content-fragments/content-fragments-models.md) se pueden habilitar y crear, antes de crear fragmentos de contenido con contenido estructurado.

### Creación de un fragmento de contenido {#creating-a-content-fragment}

El método para crear un fragmento de contenido es el siguiente:

1. Vaya a la carpeta **Assets** en la que desea crear el fragmento.
1. Seleccione **Crear** y, a continuación, **Fragmento de contenido** para abrir el asistente.
1. El primer paso del asistente requiere que especifique la base del nuevo fragmento.

   * [Modelo](/help/assets/content-fragments/content-fragments-models.md): se usa para crear un fragmento que requiere contenido estructurado; por ejemplo, el modelo **Aventura**

      * Se muestran todos los modelos disponibles.

   Después de la selección, usa **Siguiente** para continuar.

   ![Selección del modelo de fragmentos de contenido](assets/cfm-managing-01.png)

1. En el paso **Propiedades**, especifique:

   * **Básico**

      * **Título**

        El título del fragmento.

        Obligatorio.

      * **Descripción**

      * **Etiquetas**

   * **Avanzado**

      * **Nombre**

        El nombre; se utiliza para formar la dirección URL.

        Obligatorio; se deriva automáticamente del título, pero se puede actualizar.

1. Seleccione **Crear** para completar la acción y, a continuación, **Abra** el fragmento para editarlo o vuelva a la consola pulsando **Listo**.

   >[!NOTE]
   >En el modo **Lista** de la consola, puede actualizar **Ver configuración** para habilitar la columna **Modelo de fragmento de contenido**.

## Acciones para un fragmento de contenido en la consola de Assets {#actions-for-a-content-fragment-assets-console}

En la consola **Assets** hay una serie de acciones disponibles para sus fragmentos de contenido:

* En la barra de herramientas; después de seleccionar el fragmento, están disponibles todas las acciones adecuadas.
* Como [acciones rápidas](/help/sites-cloud/authoring/basic-handling.md#quick-actions); un subconjunto de acciones disponibles para las tarjetas de fragmento individuales.

![Acciones en la barra de herramientas](assets/cfm-managing-02.png)

Seleccione el fragmento para mostrar la barra de herramientas con las acciones aplicables:

* **Volver a procesar Assets**
* **Crear**
* **Descargar**

   * Guarde el fragmento como archivo ZIP; puede definir si desea incluir elementos, variaciones o metadatos.

* **Cierre de compra**
* **Propiedades**

   * Permite ver, editar o ambos metadatos del fragmento.

* **Editar**

   * Le permite [abrir el fragmento para editar contenido](/help/assets/content-fragments/content-fragments-variations.md) junto con sus elementos, variaciones, contenido asociado y metadatos.

* **Publicación rápida**
* **Administrar publicación**
* **Administrar etiquetas**
* **A la colección**
* **Copiar** (y **Pegar**)
* **Mover**
* **Eliminar**

>[!NOTE]
>
>Muchas de ellas son [acciones estándar para Assets](/help/assets/manage-digital-assets.md) y/o la [aplicación de escritorio de AEM](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html?lang=es).

## Apertura del editor de fragmentos {#opening-the-fragment-editor}

Para abrir el fragmento para editarlo en el editor original:

>[!CAUTION]
>
>Para editar un fragmento de contenido, son necesarios [los permisos adecuados](/help/implementing/developing/extending/content-fragments-customizing.md#asset-permissions). Si tiene algún problema, póngase en contacto con el administrador del sistema.

1. Vaya a la ubicación del fragmento de contenido.

1. Abra el fragmento para editarlo.

1. El fragmento se abrirá en el nuevo editor. Desactive el modificador **Nuevo editor** (parte superior derecha) para abrir el editor original:

   ![Editor de fragmentos](assets/cfm-managing-03.png)

1. Realice los cambios según sea necesario.

1. Cuando esté listo, usa **Guardar**, **Guardar y cerrar** o **Cerrar** según sea necesario.

   >[!NOTE]
   >
   >**Guardar y cerrar** está disponible mediante la lista desplegable **Guardar**.

   >[!NOTE]
   >
   >Tanto **Guardar y Cerrar** como **Cerrar** le sacarán del editor; consulte [Guardar, Cerrar y Versiones](#save-close-and-versions) para obtener información completa sobre cómo funcionan ambas opciones para los fragmentos de contenido.

## Modos y acciones en el editor de fragmentos de contenido {#modes-actions-content-fragment-editor}

Hay varios modos y acciones disponibles en el Editor de fragmentos de contenido.

### Modos en el editor de fragmentos de contenido {#modes-in-the-content-fragment-editor}

Desplácese por los distintos modos utilizando los iconos del panel lateral:

* Variaciones: [Edición del contenido](#editing-the-content-of-your-fragment) y [Administración de variaciones](#creating-and-managing-variations-within-your-fragment)

* [Anotaciones](/help/assets/content-fragments/content-fragments-variations.md#annotating-a-content-fragment)
* [Contenido asociado](#associating-content-with-your-fragment)
* [Metadatos](#viewing-and-editing-the-metadata-properties-of-your-fragment)
* [Árbol de estructura](/help/assets/content-fragments/content-fragments-structure-tree.md)
* [Previsualizar](/help/assets/content-fragments/content-fragments-json-preview.md)

![Modos en el editor de fragmentos de contenido](assets/cfm-managing-04.png)

### Acciones de barra de herramientas en el editor de fragmentos de contenido {#toolbar-actions-in-the-content-fragment-editor}

Algunas funciones de la barra de herramientas superior están disponibles en varios modos:

![Acciones de la barra de herramientas disponibles en varios modos](assets/cfm-managing-top-toolbar.png)

* Se muestra un mensaje cuando ya se hizo referencia al fragmento en una página de contenido. Puede **Cerrar** el mensaje.

* El panel lateral puede ocultarse o mostrarse utilizando el icono **Alternar panel lateral**.

* Debajo del nombre del fragmento puede ver el nombre del [Modelo de fragmento de contenido](/help/assets/content-fragments/content-fragments-models.md) que se utiliza para crear el fragmento actual:

   * El nombre también es un vínculo que abre el editor de modelos.

* Ver el estado del fragmento; por ejemplo, información sobre cuándo se creó, modificó o publicó. El estado también está codificado por colores:

   * **Nuevo**: gris
   * **Borrador**: azul
   * **Publicado**: verde
   * **Modificado**: naranja
   * **Desactivado**: rojo

* Un botón le permite **Probar nuevo editor**, abriendo directamente el *nuevo* [Editor de fragmentos de contenido](/help/sites-cloud/administering/content-fragments/authoring.md) al que se puede acceder a través de la [consola de fragmentos de contenido](/help/sites-cloud/administering/content-fragments/overview.md#content-fragments-console).

  >[!WARNING]
  >
  >El nuevo editor se abre en la misma pestaña. No se recomienda tener ambos editores abiertos al mismo tiempo.

* **Guardar** proporciona acceso a la opción **Guardar y cerrar**.

* Los tres puntos (**...**) proporcionan acceso a acciones adicionales:
   * **Actualizar referencias de página**
      * Esto actualiza cualquier referencia de página.
   * **[Publicación rápida](#publishing-and-referencing-a-fragment)**
   * **[Administrar publicación](#publishing-and-referencing-a-fragment)**

<!--
This updates any page references and ensures that the Dispatcher is flushed as required. -->

## Guardar, cerrar y versiones {#save-close-and-versions}

>[!NOTE]
>
>Las versiones también pueden ser [creadas, comparadas y revertidas desde la cronología](/help/assets/content-fragments/content-fragments-managing.md#timeline-for-content-fragments).

El editor tiene varias opciones:

* **Guardar** y **Guardar y cerrar**

   * **Guardar** guardará los cambios más recientes y permanecerá en el editor.
   * **Guardar y cerrar** guardará los cambios más recientes y cerrará el editor.

  >[!CAUTION]
  >
  >Para editar un fragmento de contenido, son necesarios [los permisos adecuados](/help/implementing/developing/extending/content-fragments-customizing.md#asset-permissions). Si tiene algún problema, póngase en contacto con el administrador del sistema.

  >[!NOTE]
  >
  >Es posible permanecer en el editor, realizando una serie de cambios, antes de guardar.

  >[!CAUTION]
  >
  >Además de guardar los cambios, las acciones actualizan también las referencias y garantizan que Dispatcher se vacíe según sea necesario. Estos cambios pueden tardar un tiempo en procesarse. Debido a este tiempo, puede haber un impacto en el rendimiento de un sistema grande/complejo/con gran carga.
  >
  >Tenga este proceso en cuenta al usar **Guardar y cerrar** y, a continuación, reintroduciendo rápidamente el editor de fragmentos para realizar y guardar más cambios.

* **Cerrar**

  Saldrá del editor sin guardar los cambios más recientes (es decir, realizados desde el último **Guardar**).

Al editar el fragmento de contenido, AEM crea automáticamente versiones para garantizar que el contenido anterior se pueda restaurar si cancela los cambios (mediante **Cerrar** sin guardar):

1. Cuando se abre un fragmento de contenido para editarlo, AEM comprueba la existencia del token basado en cookies que indica si existe una *sesión de edición*:

   1. Si se encuentra el token, el fragmento se considera parte de la sesión de edición existente.
   2. Si el token *no* está disponible y el usuario empieza a editar contenido, se crea una versión y se envía un token para esta nueva sesión de edición al cliente, donde se guarda en una cookie.

2. Mientras que haya una sesión de edición *activa*, el contenido que se está editando se guarda automáticamente cada 600 segundos (valor predeterminado).

   >[!NOTE]
   >
   >El intervalo de guardado automático se puede configurar usando el mecanismo `/conf`.
   >
   >Valor predeterminado, consulte:
   >  `/libs/settings/dam/cfm/jcr:content/autoSaveInterval`

3. Si el usuario cancela la edición, se restaura la versión creada al principio de la sesión de edición y se elimina el token para finalizar la sesión de edición.
4. Si el usuario selecciona **Guardar** las ediciones, los elementos/variaciones actualizados se mantienen y se elimina el token para finalizar la sesión de edición.

## Edición del contenido del fragmento {#editing-the-content-of-your-fragment}

Una vez que haya abierto el fragmento, puede usar la pestaña [Variaciones](/help/assets/content-fragments/content-fragments-variations.md) para crear el contenido.

## Creación y administración de variaciones dentro del fragmento {#creating-and-managing-variations-within-your-fragment}

Una vez creado el contenido principal, puede crear y administrar, [Variaciones](/help/assets/content-fragments/content-fragments-variations.md) de ese contenido.

## Asociación del contenido al fragmento {#associating-content-with-your-fragment}

También puede [asociar contenido](/help/assets/content-fragments/content-fragments-assoc-content.md) con un fragmento. Esto proporciona una conexión para que los recursos (es decir, las imágenes) se puedan utilizar (opcionalmente) con el fragmento cuando se añada a una página de contenido.

## Visualización y edición de los metadatos (propiedades) del fragmento {#viewing-and-editing-the-metadata-properties-of-your-fragment}

Puede ver y editar las propiedades de un fragmento utilizando la pestaña [Metadatos](/help/assets/content-fragments/content-fragments-metadata.md).

## Cronología de los fragmentos de contenido {#timeline-for-content-fragments}

Además de las opciones estándar, [Cronología](/help/assets/manage-digital-assets.md#timeline) proporciona información y acciones específicas para fragmentos de contenido:

* Ver información sobre versiones, comentarios y anotaciones
* Acciones para las versiones

   * **[Revertir a esta versión](#reverting-to-a-version)** (seleccione un fragmento existente y, a continuación, una versión específica)

   * **[Comparar con actual](#comparing-fragment-versions)** (seleccione un fragmento existente y, a continuación, una versión específica)

   * Agregue una **Etiqueta** o un **Comentario** (seleccione un fragmento existente y, a continuación, una versión específica)

   * **Guardar como versión** (seleccione un fragmento existente y, a continuación, la flecha hacia arriba en la parte inferior de la cronología)

* Acciones para anotaciones

   * **Eliminar**

>[!NOTE]
>
>Los comentarios son lo siguiente:
>
>* De funcionalidad estándar para todos los recursos
>* Realizados en la cronología
>* Relacionados con el recurso de fragmento
>
>Las anotaciones (para fragmentos de contenido) son lo siguiente:
>
>* Introducidas en el editor de fragmentos
>* Específicas para un segmento seleccionado de texto dentro del fragmento
>
>No mostrar los comentarios introducidos en el nuevo [editor de fragmentos de contenido](/help/sites-cloud/administering/content-fragments/authoring.md#commenting-on-your-fragment).

Por ejemplo:

![Cronología](assets/cfm-managing-05.png)

## Comparación de versiones de fragmento {#comparing-fragment-versions}

La acción **Comparar con actual** está disponible en la [Cronología](/help/assets/content-fragments/content-fragments-managing.md#timeline-for-content-fragments) después de seleccionar una versión específica.

Se abre lo siguiente:

* el **Actual** (última) versión (izquierda)

* la versión seleccionada **v&lt;*x.y*>** (derecha)

Se muestran una al lado de la otra, donde:

* Se resaltan todas las diferencias

   * Texto eliminado en rojo
   * Texto insertado en verde
   * Texto reemplazado en azul

* El icono de pantalla completa permite abrir cualquiera de las versiones por su cuenta; a continuación, vuelva a la vista paralela
* Puede **Revertir** a la versión específica
* **Listo** le devolverá a la consola

>[!NOTE]
>
>No se puede editar el contenido del fragmento al comparar fragmentos.

![Comparando variaciones](assets/cfm-managing-06.png)

## Reversión a una versión  {#reverting-to-a-version}

Puede volver a una versión específica del fragmento:

* Directamente desde la [Cronología](/help/assets/content-fragments/content-fragments-managing.md#timeline-for-content-fragments).

  Seleccione la versión requerida y, a continuación, la acción **Revertir a esta versión**.

* Mientras [compara una versión con la versión actual](/help/assets/content-fragments/content-fragments-managing.md#comparing-fragment-versions) puede **Revertir** a la versión seleccionada.

## Publicación y referencia de un fragmento {#publishing-and-referencing-a-fragment}

>[!CAUTION]
>
>Si el fragmento se basa en un modelo, debe asegurarse de que [el modelo se ha publicado](/help/assets/content-fragments/content-fragments-models.md#publishing-a-content-fragment-model).
>
>Si publica un fragmento de contenido para el que el modelo aún no se ha publicado, la lista de selección lo indicará y el modelo se publicará con el fragmento.

Los fragmentos de contenido deben publicarse para su uso en el entorno de publicación. Esto se realiza mediante la funcionalidad estándar de Assets:

* [Publicación rápida](/help/assets/manage-publication.md#quick-publish)
* [Administrar publicación](/help/assets/manage-publication.md#manage-publication)

Se puede acceder a esto:

* Después de la creación; usando [acciones disponibles en la consola de Assets](#actions-for-a-content-fragment-assets-console).
* Desde el [Editor de fragmentos de contenido](#toolbar-actions-in-the-content-fragment-editor).

Además, al [publicar una página que usa el fragmento](/help/sites-cloud/authoring/fragments/content-fragments.md#publishing); el fragmento se enumera en las referencias de página.

>[!CAUTION]
>
>Después de publicar un fragmento o de hacer referencia a él, AEM mostrará una advertencia cuando un autor abra el fragmento para editarlo de nuevo. Esto sirve para advertir que los cambios en el fragmento también afectarán a las páginas a las que se hace referencia.

## Eliminación de un fragmento {#deleting-a-fragment}

Para eliminar un fragmento:

1. En la consola **Recursos** vaya a la ubicación del fragmento de contenido.
2. Seleccione el fragmento.

   >[!NOTE]
   >
   >La acción **Eliminar** no se encuentra disponible como Acción rápida.

3. En la barra de herramientas, seleccione **Eliminar**.
4. Confirme la acción **Eliminar**.

   >[!CAUTION]
   >
   >Si ya se hace referencia al fragmento en una página, verá un mensaje de advertencia y será necesario para confirmar que desea continuar con la **eliminación forzada**. El fragmento, junto con su componente de fragmento de contenido, se elimina de cualquier página de contenido.
