---
title: 'Variaciones: Crear contenido de fragmentos'
description: Comprender cómo las variaciones pueden hacer que el contenido sin encabezado en AEM sea aún más flexible, ya que le permite crear contenido para el fragmento y, a continuación, crear variaciones de dicho contenido según el propósito.
feature: Content Fragments
role: User
exl-id: af05aae6-d535-4007-ba81-7f41213ff152
source-git-commit: cf3273af030a8352044dcf4f88539121249b73e7
workflow-type: tm+mt
source-wordcount: '2283'
ht-degree: 13%

---

# Variaciones: Crear contenido de fragmentos{#variations-authoring-fragment-content}

[Variaciones](/help/assets/content-fragments/content-fragments.md#constituent-parts-of-a-content-fragment) son una característica importante de AEM fragmentos de contenido, ya que le permiten crear y editar copias del contenido principal para su uso en canales específicos o escenarios, lo que hace que la entrega de contenido sin encabezado sea aún más flexible.

En el **Variaciones** puede:

* [Introduzca el contenido](#authoring-your-content) para el fragmento,
* [Crear y administrar variaciones](#managing-variations) del **Maestro** contenido,

Realizar una serie de otras acciones en función del tipo de datos que se esté editando; por ejemplo:

* [Insertar recursos visuales en el fragmento](#inserting-assets-into-your-fragment) (imágenes)

* Seleccionar entre [Texto enriquecido](#rich-text), [Texto sin formato](#plain-text) y [Markdown](#markdown) para editar

* [Cargar contenido](#uploading-content)

* [Ver estadísticas clave](#viewing-key-statistics) (acerca del texto multilínea)

* [Resumir texto](#summarizing-text)

* [Sincronizar variaciones con contenido principal](#synchronizing-with-master)

>[!CAUTION]
>
>Después de publicar un fragmento o de hacer referencia a él, AEM mostrará una advertencia cuando un autor abra el fragmento para editarlo de nuevo. Esto sirve para advertir que los cambios en el fragmento también afectarán a las páginas a las que se hace referencia.

## Creación de contenido {#authoring-your-content}

Cuando abra el fragmento de contenido para editarlo, la variable **Variaciones** se abrirá de forma predeterminada. Aquí puede crear el contenido, para Master o cualquier variación que tenga. El fragmento estructurado contiene varios campos, de varios tipos de datos, que se definieron en el modelo de contenido.

Por ejemplo:

![editor de pantalla completa](assets/cfm-variations-02.png)
Puede:

* realice ediciones directamente en el **Variaciones** ficha

   * cada tipo de datos ofrece diferentes opciones de edición

* para **Texto de varias líneas** también puede abrir los campos [editor de pantalla completa](#full-screen-editor) a:

   * seleccione [Formato](#formats)
   * consulte más opciones de edición (para [Texto enriquecido](#rich-text) format)
   * acceder a una amplia gama de [acciones](#actions)

* Para **Referencia de fragmento** campos **[Editar fragmento de contenido](#fragment-references-edit-content-fragment)** puede estar disponible, dependiendo de la definición del modelo.

### Editor de pantalla completa {#full-screen-editor}

Al editar un campo de texto multilínea, puede abrir el editor de pantalla completa; toque o haga clic dentro del texto real y, a continuación, seleccione el siguiente icono de acción:

![icono del editor de pantalla completa](assets/cfm-variations-03.png)

Se abrirá el editor de texto de pantalla completa:

![editor de pantalla completa](assets/cfm-variations-fullscreentexteditor.png)

El editor de texto de pantalla completa proporciona:

* Acceso a varios [acciones](#actions)
* Según el [format](#formats), opciones de formato adicionales ([Texto enriquecido](#rich-text))

### Acciones {#actions}

También están disponibles las siguientes acciones (para todas las [formatos](#formats)) cuando el editor de pantalla completa (es decir, texto multilínea) está abierto:

* Seleccione el [format](#formats) ([Texto enriquecido](#rich-text), [Texto sin formato,](#plain-text) [Markdown](#markdown))

* [Cargar contenido](#uploading-content)

* [Mostrar estadísticas de texto](#viewing-key-statistics)

* [Sincronizar con Master](#synchronizing-with-master) (al editar una variación)

* [Resumir texto](#summarizing-text)

### Formatos {#formats}

Las opciones para editar texto multilínea dependen del formato seleccionado:

* [Texto enriquecido](#rich-text)
* [Texto sin formato](#plain-text)
* [Markdown](#markdown)

El formato se puede seleccionar cuando se usa el editor de pantalla completa.

### Texto enriquecido {#rich-text}

La edición de texto enriquecido le permite dar formato:

* Negrita
* Cursiva
* Subrayado
* Alineación: izquierda, centro, derecha
* Lista con viñetas
* Lista numerada
* Sangría: aumentar, disminuir
* Crear/romper hipervínculos
* Pegar texto/desde Word
* Insertar una tabla
* Estilo de párrafo: Párrafo, Encabezado 1/2/3
* [Insertar recurso](#inserting-assets-into-your-fragment)
* Abra el editor de pantalla completa, donde están disponibles las siguientes opciones de formato:
   * Búsqueda
   * Buscar/Reemplazar
   * Corrector ortográfico
   * [Anotaciones](/help/assets/content-fragments/content-fragments-variations.md#annotating-a-content-fragment)
* [Insertar fragmento de contenido](#inserting-content-fragment-into-your-fragment); disponible cuando su **Texto de varias líneas** el campo está configurado con **Permitir referencia de fragmento**.

La variable [acciones](#actions) también son accesibles desde el editor de pantalla completa.

### Texto sin formato {#plain-text}

El texto sin formato permite introducir rápidamente el contenido sin aplicar formato ni marcar la información. También puede abrir el editor de pantalla completa para obtener más información [acciones](#actions).

>[!CAUTION]
>
>Si selecciona **Texto sin formato**, puede perder cualquier formato, marca o recurso que haya insertado en **Texto enriquecido** o **Marcado**.

### Markdown {#markdown}

>[!NOTE]
>
>Para obtener información completa, consulte la [Markdown](/help/assets/content-fragments/content-fragments-markdown.md) documentación.

Esto le permite dar formato al texto mediante markdown. Puede definir:

* Encabezados
* Párrafos y saltos de línea
* Vínculos
* Imágenes
* Comillas de bloque
* Listas
* Énfasis
* Bloques de código
* La barra invertida se escapa

También puede abrir el editor de pantalla completa para obtener más información [acciones](#actions).

>[!CAUTION]
>
>Si cambia entre **Texto enriquecido** y **Marcado**, puede que se produzcan efectos inesperados con Comillas de bloque y Bloques de código, ya que estos dos formatos pueden tener diferencias en la forma en que se gestionan.

### Referencias de fragmento {#fragment-references}

Si el modelo de fragmento de contenido contiene referencias de fragmento, es posible que los autores de los fragmentos tengan opciones adicionales:

* [Editar fragmento de contenido](#fragment-references-edit-content-fragment)
* [Fragmento de contenido nuevo](#fragment-references-new-content-fragment)

![Referencias de fragmento](assets/cfm-variations-12.png)

#### Editar fragmento de contenido {#fragment-references-edit-content-fragment}

La opción **Editar fragmento de contenido** abrirá ese fragmento en una nueva ficha de editor (en la misma ficha de navegador).

Volver a seleccionar la pestaña original (por ejemplo, **Little Pony Inc.**), cerrará esta pestaña secundaria (en este caso, **Adam Smith**).

![Referencias de fragmento](assets/cfm-variations-editreference.png)

#### Fragmento de contenido nuevo {#fragment-references-new-content-fragment}

La opción **Nuevo fragmento de contenido** le permite crear un fragmento completamente nuevo. Para conseguirlo, se abrirá en el editor una variación del asistente para crear fragmentos de contenido.

A continuación, podrá crear un nuevo fragmento mediante:

1. Vaya a y seleccione la carpeta requerida.
1. Selección **Siguiente**.
1. Especificación de propiedades; por ejemplo **Título**.
1. Selección **Crear**.
1. Finalmente:
   1. **Listo** volverá (al fragmento original) y hará referencia al nuevo fragmento.
   1. **Apertura** hará referencia al nuevo fragmento y abrirá el nuevo fragmento, para editarlo, en una nueva pestaña del navegador.

### Visualización de estadísticas clave {#viewing-key-statistics}

Cuando el editor de pantalla completa está abierto, la acción **Estadísticas de texto** mostrará un rango de información sobre el texto.

Por ejemplo:

![statistics](assets/cfm-variations-04.png)

### Carga de contenido {#uploading-content}

Para facilitar el proceso de creación de fragmentos de contenido, puede cargar texto, preparado en un editor externo y añadirlo directamente al fragmento.

### Resumen de texto {#summarizing-text}

El texto de resumen está diseñado para ayudar a los usuarios a reducir la longitud de su texto a un número predefinido de palabras, manteniendo al mismo tiempo los puntos clave y el significado general.

>[!NOTE]
>
>A un nivel más técnico, el sistema mantiene las frases que califica como que proporcionan la variable *la mejor relación entre densidad y singularidad de la información* según algoritmos específicos.

>[!CAUTION]
>
>El fragmento de contenido debe tener una carpeta de idioma válida (código ISO) como antecesor; se utiliza para determinar el modelo de idioma que se va a utilizar.
>
>Por ejemplo, `en/` como en la siguiente ruta:
>
>  `/content/dam/my-brand/en/path-down/my-content-fragment`

>[!CAUTION]
El inglés está disponible de forma predeterminada.
Otros idiomas están disponibles como Paquetes de modelo de idioma desde Distribución de software:
* [Francés(fr)](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq630/product/smartcontent-model-fr)
* [Alemán(de)](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq630/product/smartcontent-model-de)
* [Italiano(it)](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq630/product/smartcontent-model-it)
* [Español(es)](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq630/product/smartcontent-model-es)
>


1. Select **Maestro** o la variación requerida.
1. Abra el editor de pantalla completa.

1. Select **Resumir texto** en la barra de herramientas.

   ![resumen](assets/cfm-variations-05.png)

1. Especifique el número de palabras objetivo y seleccione **Inicio**:
1. El texto original se muestra en paralelo con el resumen propuesto:

   * Las oraciones que se eliminen se resaltan en rojo, con huelga.
   * Haga clic en cualquier oración resaltada para mantenerla en el contenido resumido.
   * Haga clic en cualquier oración no resaltada para que la eliminen.

1. Select **Resumen** para confirmar los cambios.

1. El texto original se muestra en paralelo con el resumen propuesto:

   * Las oraciones que se eliminen se resaltan en rojo, con huelga.
   * Haga clic en cualquier oración resaltada para mantenerla en el contenido resumido.
   * Haga clic en cualquier oración no resaltada para que la eliminen.
   * Se muestran las estadísticas de resumen: **Real** y **Target**-
   * Puede **Vista previa** los cambios.

   ![comparación de resumen](assets/cfm-variations-06.png)

### Anotación de un fragmento de contenido {#annotating-a-content-fragment}

Para realizar anotaciones en un fragmento:

1. Select **Maestro** o la variación requerida.

1. Abra el editor de pantalla completa.

1. La variable **Anotar** está disponible en la barra de herramientas superior. Si es necesario, puede seleccionar texto.

   ![anotar](assets/cfm-variations-07.png)

1. Se abrirá un cuadro de diálogo: Aquí puede introducir la anotación.

   ![anotar](assets/cfm-variations-07a.png)

1. Select **Aplicar** en el cuadro de diálogo.

   ![anotar](assets/cfm-variations-annotations-apply-icon.png)

   Si la anotación se aplicó al texto seleccionado, el texto permanecerá resaltado.

   ![anotar](assets/cfm-variations-07b.png)

1. Cierre el editor de pantalla completa y las anotaciones se seguirán resaltando. Si se selecciona, se abrirá un cuadro de diálogo para que pueda editar la anotación más adelante.

1. Seleccione **Guardar**.

1. Cierre el editor de pantalla completa y las anotaciones se seguirán resaltando. Si se selecciona, se abrirá un cuadro de diálogo para que pueda editar la anotación más adelante.

   ![anotar](assets/cfm-variations-07c.png)

### Visualización, Edición, Eliminación De Anotaciones {#viewing-editing-deleting-annotations}

Anotaciones:

* Se indican mediante el resaltado en el texto, tanto en pantalla completa como en modo normal del editor. Los detalles completos de una anotación se pueden ver, editar y/o eliminar haciendo clic en el texto resaltado, que reabrirá el cuadro de diálogo.

   >[!NOTE]
   Se proporciona un selector desplegable si se han aplicado varias anotaciones a un texto.

* Cuando se elimina todo el texto al que se aplicó la anotación, también se elimina la anotación.

* Se puede enumerar y eliminar seleccionando la opción **Anotaciones** en el editor de fragmentos.

   ![anotaciones](assets/cfm-variations-08.png)

* Se puede ver y eliminar en [Cronología](/help/assets/content-fragments/content-fragments-managing.md#timeline-for-content-fragments) para el fragmento seleccionado.

### Inserción de recursos en el fragmento {#inserting-assets-into-your-fragment}

Para facilitar el proceso de creación de fragmentos de contenido, puede añadir [Recursos](/help/assets/manage-digital-assets.md) (imágenes) directamente al fragmento.

Se añadirán a la secuencia de párrafo del fragmento sin ningún formato; el formato se puede realizar cuando el [se utiliza/se hace referencia al fragmento en una página](/help/sites-cloud/authoring/fundamentals/content-fragments.md).

>[!CAUTION]
Estos recursos no se pueden mover ni eliminar en una página de referencia; esto debe hacerse en el editor de fragmentos.
Sin embargo, el formato del recurso (p. ej., su tamaño) debe realizarse en la variable [editor de páginas](/help/sites-cloud/authoring/fundamentals/content-fragments.md). La representación del recurso en el editor de fragmentos se realiza exclusivamente para crear el flujo de contenido.

>[!NOTE]
Existen varios métodos para añadir [imágenes](/help/assets/content-fragments/content-fragments.md#fragments-with-visual-assets) al fragmento o página.

1. Coloque el cursor en la posición en la que desee agregar la imagen.
1. Utilice el icono **Insertar recurso** para abrir el cuadro de diálogo de búsqueda.

   ![insertar icono de recurso](assets/cfm-variations-09.png)

1. En el cuadro de diálogo puede:

   * vaya al recurso necesario en DAM
   * buscar el recurso en DAM

   Una vez localizado, seleccione el recurso necesario haciendo clic en la miniatura.

1. Utilice **Seleccionar** para agregar el recurso al sistema de párrafos del fragmento de contenido en la ubicación actual.

   >[!CAUTION]
   Si, después de agregar un recurso, cambia el formato a:
   * **Texto sin formato**: El recurso se perderá completamente del fragmento.
   * **Marcado**: El recurso no estará visible, pero permanecerá allí cuando vuelva a **Texto enriquecido**.


### Inserción de un fragmento de contenido en el fragmento {#inserting-content-fragment-into-your-fragment}

Para facilitar el proceso de creación de fragmentos de contenido, también puede añadir otro fragmento de contenido al fragmento.

Se añaden como referencia en la ubicación actual del fragmento.

>[!NOTE]
Esta opción está disponible cuando su **Texto de varias líneas** está configurado con **Permitir referencia de fragmento**.

>[!CAUTION]
Estos recursos no se pueden mover ni eliminar en una página de referencia; esto debe hacerse en el editor de fragmentos.
Sin embargo, el formato del recurso (p. ej., su tamaño) debe realizarse en la variable [editor de páginas](/help/sites-cloud/authoring/fundamentals/content-fragments.md). La representación del recurso en el editor de fragmentos se realiza exclusivamente para crear el flujo de contenido.

>[!NOTE]
Existen varios métodos para añadir [imágenes](/help/assets/content-fragments/content-fragments.md#fragments-with-visual-assets) al fragmento o página.

1. Sitúe el cursor en la posición en la que desee agregar el fragmento.
1. Utilice la variable **Insertar fragmento de contenido** para abrir el cuadro de diálogo de búsqueda.

   ![Icono Insertar fragmento de contenido](assets/cfm-variations-13.png)

1. En el cuadro de diálogo puede:

   * vaya al fragmento requerido en la carpeta Assets
   * buscar el fragmento

   Una vez localizado, seleccione el fragmento requerido haciendo clic en la miniatura.

1. Uso **Select** para agregar una referencia al fragmento de contenido seleccionado al fragmento de contenido actual (en la ubicación actual).

   >[!CAUTION]
   Si, después de agregar una referencia a otro fragmento, cambia el formato a:
   * **Texto sin formato**: la referencia se perderá completamente del fragmento.
   * **Markdown**: la referencia se mantendrá.


## Administración de variaciones {#managing-variations}

### Creación de una variación {#creating-a-variation}

Las variaciones le permiten tomar el **Maestro** y variar según el propósito (si es necesario).

Para crear una nueva variación:

1. Abra el fragmento y asegúrese de que el panel lateral esté visible.
1. Select **Variaciones** en la barra de iconos del panel lateral.
1. Select **Crear variación**.
1. Se abrirá un cuadro de diálogo, especifique el **Título** y la **Descripción** de la nueva variación.
1. Seleccione **Agregar**; el fragmento **principal** se copiará en la nueva variación, que ahora estará abierta para [edición](#editing-a-variation).

   >[!NOTE]
   Al crear una variación nueva, siempre es **Maestro** que se copia, no la variación que está abierta actualmente.

### Edición de una variación {#editing-a-variation}

Puede realizar cambios en el contenido de la variación después de:

* [Creación de la variación](#creating-a-variation).
* Abra un fragmento existente y, a continuación, seleccione la variación necesaria en el panel lateral.

![edición de una variación](assets/cfm-variations-10.png)

### Cambio del nombre de una variación {#renaming-a-variation}

Para cambiar el nombre de una variación existente:

1. Abra el fragmento y seleccione **Variaciones** del panel lateral.
1. Seleccione la variación requerida.
1. Select **Cambiar nombre** de la variable **Acciones** desplegable .

1. Introduzca el nuevo **Título** o **Descripción** en el cuadro de diálogo resultante.

1. Confirme el **Cambiar nombre** acción.

>[!NOTE]
Esto solo afecta a la variación **Título**.

### Eliminación de una variación {#deleting-a-variation}

Para eliminar una variación existente:

1. Abra el fragmento y seleccione **Variaciones** del panel lateral.
1. Seleccione la variación requerida.
1. Select **Eliminar** de la variable **Acciones** desplegable .

1. Confirme el **Eliminar** en el cuadro de diálogo.

>[!NOTE]
No puede eliminar **Maestro**.

### Sincronización con Master {#synchronizing-with-master}

**Maestro** es una parte integral de un fragmento de contenido y por definición contiene la copia maestra del contenido, mientras que las variaciones contienen versiones individuales actualizadas y adaptadas de ese contenido. Cuando Master se actualiza, es posible que estos cambios también sean relevantes para las variaciones y, por lo tanto, deban propagarse a ellas.

Al editar una variación, tiene acceso a la acción para sincronizar el elemento actual de la variación con Master. Esto le permite copiar automáticamente los cambios realizados en Principal en la variación requerida.

>[!CAUTION]
La sincronización solo está disponible para copiar cambios *de **Principal**a la variación*.
Solo se sincronizará el elemento actual de la variación.
La sincronización solo funciona en el tipo de datos de **texto de varias líneas**.
No está disponible como opción la transferencia de cambios *de una variación **a Principal***.

1. Abra el fragmento de contenido en el editor de fragmentos. Asegúrese de que la variable **Maestro** se ha editado.

1. Seleccione una variación específica y, a continuación, la acción de sincronización adecuada desde:

   * el **Acciones** selector desplegable - **Sincronizar elemento actual con maestro**

      ![sincronización con master](assets/cfm-variations-11a.png)

   * la barra de herramientas del editor de pantalla completa: **Sincronizar con el maestro**

      ![sincronización con master](assets/cfm-variations-11b.png)

1. Master y la variación se mostrarán en paralelo:

   * verde indica el contenido añadido (a la variación)
   * rojo indica que el contenido se ha eliminado (de la variación)
   * azul indica texto reemplazado

   ![sincronización con master](assets/cfm-variations-11c.png)

1. Select **Sincronizar**, la variación se actualizará y se mostrará.
