---
title: 'Variaciones: Creación de contenido de fragmentos (Assets: fragmentos de contenido)'
description: Comprenda cómo las variaciones de fragmentos de contenido le permiten crear contenido para el fragmento y luego crear variaciones de ese contenido según el propósito, aumentando así la flexibilidad.
exl-id: af05aae6-d535-4007-ba81-7f41213ff152
feature: Content Fragments
role: User
solution: Experience Manager Sites
source-git-commit: 8a8f63758cf216b502d5ee894ff5af7285777889
workflow-type: tm+mt
source-wordcount: '2571'
ht-degree: 50%

---

# Variaciones: Crear contenido de fragmentos{#variations-authoring-fragment-content}

[Las variaciones](/help/assets/content-fragments/content-fragments.md#constituent-parts-of-a-content-fragment) son una característica importante de los fragmentos de contenido en Adobe Experience Manager (AEM) as a Cloud Service. Esto se debe a que le permiten crear y editar copias del contenido de **Master** para usarlas en canales y escenarios específicos. En particular, esto hace que la entrega de contenido sin encabezado sea aún más flexible.

>[!NOTE]
>
>Los fragmentos de contenido son una función de Sites, pero se almacenan como **Assets**.
>
>Existen dos editores para la creación de fragmentos de contenido: el nuevo editor y el editor original. El nuevo editor es el predeterminado. Aunque la funcionalidad básica es la misma, existen algunas diferencias.
>
>Esta sección trata sobre el editor original. Se ha [abierto a través del nuevo editor](/help/assets/content-fragments/content-fragments-managing.md#opening-the-fragment-editor).
>
>Consulte la documentación de Sites, [Fragmentos de contenido: creación](/help/sites-cloud/administering/content-fragments/authoring.md), para obtener información detallada del nuevo editor.

Desde la ficha **Variaciones**, puede hacer lo siguiente:

* [Introducir el contenido](#authoring-your-content) para el fragmento,
* [Crear y administrar variaciones](#managing-variations) del contenido **Principal**,

Realizar una serie de otras acciones en función del tipo de datos que se esté editando; por ejemplo:

* [Insertar recursos visuales en el fragmento](#inserting-assets-into-your-fragment) (imágenes)

* Seleccione entre [Texto enriquecido](#rich-text), [Texto sin formato](#plain-text) y [Markdown](#markdown) para editarlo

* [Cargar contenido](#uploading-content)

* [Ver estadísticas clave](#viewing-key-statistics) (acerca del texto multilínea)

* [Resumir texto](#summarizing-text)

* [Sincronizar variaciones con contenido principal](#synchronizing-with-master)

>[!CAUTION]
>
>Una vez publicado un fragmento o referenciado, AEM muestra una advertencia cuando un autor abre el fragmento para editarlo de nuevo. Esto sirve para advertir que los cambios en el fragmento también afectan a las páginas a las que se hace referencia.

## Creación de contenido {#authoring-your-content}

Cuando abre el fragmento de contenido para editarlo en el editor original, la pestaña **Variaciones** se abre de forma predeterminada. Aquí puede crear el contenido, para Principal o cualquier variación que tenga. El fragmento estructurado contiene campos de varios tipos de datos definidos en el modelo de contenido.

Por ejemplo:

![editor de pantalla completa](assets/cfm-variations-02.png)

Puede hacer lo siguiente:

* Edite el contenido directamente en la pestaña de **Variaciones**; cada tipo de datos proporciona diferentes opciones de edición, por ejemplo:

   * cuando se configura (como múltiple) en el modelo, varios tipos de datos le permiten **agregar** instancias del campo correspondiente

   * para los campos **Texto multilínea**, también puede abrir el [editor de pantalla completa](#full-screen-editor) para:

      * seleccione el [Formato](#formats)
      * consulte más opciones de edición (para formato de [Texto enriquecido](#rich-text))
      * acceder a una amplia gama de [acciones](#actions)

   * Para los campos **Referencia de fragmento**, la opción [Editar fragmento de contenido](#fragment-references-edit-content-fragment) puede estar disponible, según la definición del modelo.

* Asigne **Etiquetas** a la variación actual; las etiquetas se pueden agregar, actualizar y eliminar.

   * Las [etiquetas](/help/sites-cloud/authoring/sites-console/tags.md) son útiles a la hora de organizar los fragmentos, ya que se pueden usar para la clasificación de contenido y la taxonomía. Las etiquetas se pueden utilizar para buscar contenido (mediante etiquetas) y aplicar operaciones por lotes.

      * La búsqueda de una etiqueta devuelve el fragmento, con la variación de etiqueta resaltada.
      * Las etiquetas de variación también se pueden utilizar para agrupar variaciones para un perfil específico de la red de distribución de contenido (CDN) (para el almacenamiento en caché de CDN), en lugar de utilizar el nombre de variación.

     Por ejemplo, puede etiquetar fragmentos relevantes como “lanzamiento de Navidad” para permitir solo explorarlos como un subconjunto o copiarlos para usarlos con otro lanzamiento futuro en una nueva carpeta.

  >[!NOTE]
  >
  >**Etiquetas** también se puede añadir (a la variación **Principal**) como parte de los [Metadatos](/help/assets/content-fragments/content-fragments-metadata.md)

* [Crear y administrar variaciones](#managing-variations) del contenido **Principal.**

>[!NOTE]
>
>Según las definiciones del modelo subyacente, los campos pueden estar sujetos a ciertos tipos de [Validación](/help/assets/content-fragments/content-fragments-models.md#validation).

### Editor de pantalla completa {#full-screen-editor}

Al editar un campo de texto multilínea, puede abrir el editor de pantalla completa; seleccione dentro del texto real y, a continuación, seleccione el siguiente icono de acción:

![icono del editor de pantalla completa](assets/cfm-variations-03.png)

Se abrirá el editor de texto de pantalla completa:

![editor de pantalla completa](assets/cfm-variations-fullscreentexteditor.png)

El editor de texto de pantalla completa proporciona lo siguiente:

* Acceso a varias [acciones](#actions)
* Según el [formato](#formats), opciones de formato adicionales ([Texto enriquecido](#rich-text))

### Acciones {#actions}

También están disponibles las siguientes acciones (para todas los [formatos](#formats)) cuando el editor de pantalla completa (es decir, texto multilínea) está abierto:

* Seleccione el [formato](#formats) ([Texto enriquecido](#rich-text), [Texto sin formato](#plain-text), [Markdown](#markdown))

* [Cargar contenido](#uploading-content)

* [Mostrar estadísticas de texto](#viewing-key-statistics)

* [Sincronizar con Principal](#synchronizing-with-master) (al editar una variación)

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
* [Insertar fragmento de contenido](#inserting-content-fragment-into-your-fragment); disponible cuando su campo **Texto multilínea** está configurado con **Permitir referencia a fragmento**.

Las [acciones](#actions) también son accesibles desde el editor de pantalla completa.

### Texto sin formato {#plain-text}

El texto sin formato permite introducir rápidamente el contenido sin aplicar formato ni marcar la información. También puede abrir el editor de pantalla completa para obtener más [acciones](#actions).

>[!CAUTION]
>
>Si selecciona **Texto sin formato**, podría perder cualquier formato, marca o recurso que insertó en **Texto enriquecido** o **Marcado**.

### Markdown {#markdown}

>[!NOTE]
>
>Para obtener información completa, consulte la documentación de [Markdown](/help/assets/content-fragments/content-fragments-markdown.md).

Esto permite dar formato al texto mediante markdown. Puede definir lo siguiente:

* Encabezados
* Párrafos y saltos de línea
* Vínculos
* Imágenes
* Comillas de bloque
* Listas
* Énfasis
* Bloques de código
* Secuencias de escape de barra invertida

También puede abrir el editor de pantalla completa para obtener más [acciones](#actions).

>[!CAUTION]
>
>Si cambia entre **Texto enriquecido** y **Markdown**, puede que se produzcan efectos inesperados con Comillas de bloque y Bloques de código, ya que estos dos formatos pueden tener diferencias en la forma en que se gestionan.

### Referencias a fragmento {#fragment-references}

Si el modelo de fragmento de contenido contiene referencias a fragmento, es posible que los autores de los fragmentos tengan opciones adicionales:

* [Editar fragmento de contenido](#fragment-references-edit-content-fragment)
* [Fragmento de contenido nuevo](#fragment-references-new-content-fragment)

![Referencias a fragmento](assets/cfm-variations-12.png)

#### Editar fragmento de contenido {#fragment-references-edit-content-fragment}

La opción **Editar fragmento de contenido** abre ese fragmento en una nueva pestaña del editor (en la misma pestaña del explorador).

Volver a seleccionar la ficha original (por ejemplo, **Little Pony Inc.**) cierra esta ficha secundaria (en este caso, **Adam Smith**).

![Referencias a fragmento](assets/cfm-variations-editreference.png)

#### Fragmento de contenido nuevo {#fragment-references-new-content-fragment}

La opción **Nuevo fragmento de contenido** le permite crear un fragmento. Para conseguirlo, se abre en el editor una variación del asistente para crear fragmentos de contenido.

**Para crear un fragmento de contenido:**

1. Ir a y seleccionar la carpeta requerida.
1. Seleccionar **Siguiente**.
1. Especificando propiedades; por ejemplo, **Title**.
1. Selección **Crear**.
1. Finalmente:
   1. **Listo**:
      * vuelve (al fragmento original)
      * hace referencia al nuevo fragmento
   1. **Abrir**:
      * hace referencia al nuevo fragmento
      * abre el nuevo fragmento para editarlo en una nueva pestaña del explorador

### Visualización de estadísticas clave {#viewing-key-statistics}

Cuando el editor de pantalla completa está abierto, la acción **Estadísticas de texto** muestra un rango de información sobre el texto.

Por ejemplo:

![estadísticas](assets/cfm-variations-04.png)

### Carga de contenido {#uploading-content}

Para facilitar el proceso de creación de fragmentos de contenido, puede cargar texto preparado en un editor externo y añadirlo directamente al fragmento.

### Texto de resumen {#summarizing-text}

El texto de resumen está diseñado para ayudar a los usuarios a reducir la longitud de su texto a un número predefinido de palabras, manteniendo al mismo tiempo los puntos clave y el significado general.

>[!NOTE]
>
>A un nivel más técnico, el sistema mantiene las frases que califica como que proporcionan la *mejor relación entre densidad y singularidad de la información* según algoritmos específicos.

>[!CAUTION]
>
>El fragmento de contenido debe tener una carpeta de idioma válida (código ISO) como antecesor; se utiliza para determinar el modelo de idioma que se va a utilizar.
>
>Por ejemplo, `en/` como en la siguiente ruta:
>
>  `/content/dam/my-brand/en/path-down/my-content-fragment`

>[!CAUTION]
>
>El inglés está disponible de forma predeterminada.
>
>Otros idiomas están disponibles como Paquetes de modelo de idioma desde Distribución de software:
>
>* [Francés(fr)](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq630/product/smartcontent-model-fr)
>* [Alemán(de)](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq630/product/smartcontent-model-de)
>* [Italiano(it)](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq630/product/smartcontent-model-it)
>* [Español(es)](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq630/product/smartcontent-model-es)
>

1. Seleccione **Principal** o la variación requerida.
1. Abra el editor de pantalla completa.

1. Seleccione **Resumir texto** en la barra de herramientas.

   ![resumen](assets/cfm-variations-05.png)

1. Especifique el número de palabras objetivo y seleccione **Inicio**:
1. El texto original se muestra en paralelo con el resumen propuesto:

   * Las frases que se eliminen se resaltan en rojo y se tachan.
   * Haga clic en cualquier frase resaltada para mantenerla en el contenido resumido.
   * Haga clic en cualquier frase no resaltada para que pueda eliminarla.

1. Seleccione **Resumen** para confirmar los cambios.

1. El texto original se muestra en paralelo con el resumen propuesto:

   * Las frases que se eliminen se resaltan en rojo y se tachan.
   * Haga clic en cualquier frase resaltada para mantenerla en el contenido resumido.
   * Haga clic en cualquier frase no resaltada para que pueda eliminarla.
   * Se muestran las estadísticas de resumen: **Real** y **Objetivo**-
   * Puede **Previsualizar** los cambios.

   ![comparación de resumen](assets/cfm-variations-06.png)

### Anotación de un fragmento de contenido {#annotating-a-content-fragment}

Para realizar anotaciones en un fragmento:

1. Seleccione **Principal** o la variación requerida.

1. Abra el editor de pantalla completa.

1. El icono **Anotar** está disponible en la barra de herramientas superior. Si es necesario, puede seleccionar texto.

   ![anotar](assets/cfm-variations-07.png)

1. Se abre un cuadro de diálogo. Aquí puede introducir la anotación.

   ![anotar](assets/cfm-variations-07a.png)

1. Seleccione **Aplicar** en el cuadro de diálogo.

   ![anotar](assets/cfm-variations-annotations-apply-icon.png)

   Si la anotación se aplicó al texto seleccionado, ese texto permanece resaltado.

   ![anotar](assets/cfm-variations-07b.png)

1. Cierre el editor de pantalla completa y las anotaciones se seguirán resaltando. Si se selecciona, se abre un cuadro de diálogo para que pueda editar la anotación más adelante.

1. Seleccione **Guardar**.

1. Cierre el editor de pantalla completa y las anotaciones se seguirán resaltando. Si se selecciona, se abre un cuadro de diálogo para que pueda editar la anotación más adelante.

   ![anotar](assets/cfm-variations-07c.png)

>[!NOTE]
>
>La característica Anotaciones no muestra los comentarios introducidos en el nuevo [editor de fragmentos de contenido](/help/sites-cloud/administering/content-fragments/authoring.md#commenting-on-your-fragment).

### Visualización, Edición, Eliminación de anotaciones {#viewing-editing-deleting-annotations}

Anotaciones:

* Se indican mediante el resaltado en el texto, tanto en pantalla completa como en modo normal del editor. Los detalles completos de una anotación se pueden ver, editar o eliminar haciendo clic en el texto resaltado, que vuelve a abrir el cuadro de diálogo.

  >[!NOTE]
  >
  >Se proporciona un selector desplegable si se han aplicado varias anotaciones a un texto.

* Cuando se elimina todo el texto al que se aplicó la anotación, también se elimina la anotación.

* Se puede enumerar y eliminar seleccionando la pestaña **Anotaciones** en el editor de fragmentos.

  ![anotaciones](assets/cfm-variations-08.png)

* Se puede ver y eliminar en la [cronología](/help/assets/content-fragments/content-fragments-managing.md#timeline-for-content-fragments) del fragmento seleccionado.

### Inserción de recursos en el fragmento {#inserting-assets-into-your-fragment}

Para facilitar el proceso de creación de fragmentos de contenido, puede agregar [Assets](/help/assets/manage-digital-assets.md) (imágenes) directamente al fragmento.

Se agregan a la secuencia de párrafo del fragmento sin ningún formato; el formato se puede realizar cuando [se utiliza/se hace referencia al fragmento en una página](/help/sites-cloud/authoring/fragments/content-fragments.md).

>[!CAUTION]
>
>Estos recursos no se pueden mover ni eliminar en una página de referencia; esto debe hacerse en el editor de fragmentos.
>
>Sin embargo, el formato del recurso (por ejemplo, su tamaño) debe realizarse en el [editor de páginas](/help/sites-cloud/authoring/fragments/content-fragments.md). La representación del recurso en el editor de fragmentos se realiza exclusivamente para crear el flujo de contenido.

>[!NOTE]
>
>Hay varios métodos para agregar [imágenes](/help/assets/content-fragments/content-fragments.md#fragments-with-visual-assets) al fragmento o página.

1. Coloque el cursor donde desee agregar la imagen.
1. Utilice el icono **Insertar recurso** para abrir el cuadro de diálogo de búsqueda.

   ![insertar icono de recurso](assets/cfm-variations-09.png)

1. En el cuadro de diálogo, puede desplazarse hasta el recurso necesario en DAM o buscarlo en DAM.

   Cuando se encuentre, seleccione el recurso necesario haciendo clic en la miniatura.

1. Utilice **Seleccionar** para agregar el recurso al sistema de párrafos del fragmento de contenido en la ubicación actual.

   >[!CAUTION]
   >
   >Después de agregar un recurso, si cambia el formato a:
   >
   >* **Texto sin formato**: el recurso se pierde del fragmento.
   >* **Marcado**: el recurso no es visible, pero permanece allí cuando vuelva a **Texto enriquecido**.

### Inserción de un fragmento de contenido en el fragmento {#inserting-content-fragment-into-your-fragment}

Para facilitar el proceso de creación de fragmentos de contenido, también puede agregar otro fragmento de contenido al fragmento.

Se añaden como referencia en la ubicación actual en el fragmento.

>[!NOTE]
>
>Esta opción está disponible cuando el **texto multilínea** está configurado con **Permitir referencia a fragmento**.

>[!CAUTION]
>
>Estos recursos no se pueden mover ni eliminar en una página de referencia; esto debe hacerse en el editor de fragmentos.
>
>Sin embargo, el formato del recurso (por ejemplo, su tamaño) debe realizarse en el [editor de páginas](/help/sites-cloud/authoring/fragments/content-fragments.md). La representación del recurso en el editor de fragmentos se realiza exclusivamente para crear el flujo de contenido.

>[!NOTE]
>
>Hay varios métodos para agregar [imágenes](/help/assets/content-fragments/content-fragments.md#fragments-with-visual-assets) al fragmento o página.

1. Coloque el cursor donde desee agregar el fragmento.
1. Utilice el icono **Insertar fragmento de contenido** para abrir el cuadro de diálogo de búsqueda.

   ![Icono Insertar fragmento de contenido](assets/cfm-variations-13.png)

1. En el cuadro de diálogo, puede desplazarse hasta el fragmento requerido en la carpeta Assets o buscar el fragmento.

   Cuando se encuentre, seleccione el fragmento requerido haciendo clic en la miniatura.

1. Use **Seleccionar** para agregar una referencia al fragmento de contenido seleccionado al fragmento de contenido actual (en la ubicación actual).

   >[!CAUTION]
   >
   >Después de agregar una referencia a otro fragmento, si cambia el formato a:
   >
   >* **Texto sin formato**: la referencia se pierde del fragmento.
   >* **Markdown**: la referencia se mantiene.

## Herencia {#inheritance}

La herencia es el mecanismo por el que el contenido se puede insertar automáticamente de un fragmento a otro. Los campos heredados y las variaciones pueden ser el producto de [Multi-Site Management](/help/assets/content-fragments/content-fragments-msm.md).

Puede cancelar (y volver a habilitar) la herencia. Según el contexto, esto puede estar disponible para una variación o un campo individual, si el fragmento forma parte de una Live Copy.

![Un fragmento de contenido que muestra la relación de herencia](/help/assets/content-fragments/assets/cfm-variations-inheritance.png)

Por ejemplo:

* Cancelar herencia

  ![Botón Cancelar herencia](/help/assets/content-fragments/assets/editing-cancel-inheritance.png)

* Volver a habilitar la herencia (si la herencia ya se ha cancelado)

  ![Botón Volver a habilitar herencia](/help/assets/content-fragments/assets/editing-reenable-inheritance.png)

<!--
* Rollout action is also available in Live Copy source

  ![Rollout button](/help/assets/content-fragments/assets/editing-rollout.png)
-->

## Administración de variaciones {#managing-variations}

### Creación de una variación {#creating-a-variation}

Las variaciones le permiten tomar el contenido **Principal** y variar según el propósito (si es necesario).

**Para crear una variación:**

>[!NOTE]
>
>Las variaciones añaden tiempo de procesamiento a un fragmento de contenido, en el entorno de creación y durante la entrega. Se recomienda mantener el número de variaciones a un mínimo manejable.
>
>Una práctica recomendada es no superar las diez variaciones por fragmento de contenido.

1. Abra el fragmento y asegúrese de que el panel lateral esté visible.
1. Seleccione **Variaciones** en la barra de iconos del panel lateral.
1. Seleccione **Crear variación**.
1. Se abre un cuadro de diálogo para que pueda especificar **Title** y **Description** para la nueva variación.
1. Seleccione **Agregar**; el fragmento **Principal** se copia en la nueva variación, que ahora está abierta para [editar](#editing-a-variation).

   >[!NOTE]
   >
   >Al crear una variación, siempre se copia **Principal**, no la variación que está abierta.

   >[!NOTE]
   >
   >Cuando crea una variación, todas las **Etiquetas** asignadas actualmente a la variación **Principal** se copian en la nueva variación.

### Edición de una variación {#editing-a-variation}

Puede cambiar el contenido de la variación después de lo siguiente:

* [Creación de la variación](#creating-a-variation).
* Abra un fragmento existente y, a continuación, seleccione la variación necesaria en el panel lateral.

![edición de una variación](assets/cfm-variations-10.png)

### Cambio del nombre de una variación {#renaming-a-variation}

1. Abra el fragmento y seleccione **Variaciones** en el panel lateral.
1. Seleccione la variación requerida.
1. Seleccione **Cambiar nombre** del menú desplegable **Acciones**.

1. Introduzca el nuevo **Título** o **Descripción** en el cuadro de diálogo resultante.

1. Confirme la acción **Cambiar nombre**.

>[!NOTE]
>
>Esto solo afecta a la variación **Título**.

### Eliminación de una variación {#deleting-a-variation}

1. Abra el fragmento y seleccione **Variaciones** en el panel lateral.
1. Seleccione la variación requerida.
1. Seleccione **Eliminar** del menú desplegable **Acciones**.

1. Confirme la acción **Eliminar** en el cuadro de diálogo.

>[!NOTE]
>
>No puede eliminar **Principal**.

### Sincronización con Principal {#synchronizing-with-master}

**Principal** es parte de un fragmento de contenido y, por definición, contiene la copia principal del contenido. Mientras que las variaciones contienen versiones individuales actualizadas y adaptadas de ese contenido. Cuando se actualiza el Principal, es posible que estos cambios también sean relevantes para las variaciones y, por lo tanto, deban propagarse a ellas.

Al editar una variación, tiene acceso a la acción para sincronizar el elemento actual de la variación con Principal. Esto permite copiar automáticamente los cambios realizados en Principal en la variación requerida.

>[!CAUTION]
>
>La sincronización solo está disponible para copiar cambios *de **Principal**a la variación*.
>
>Solo se sincroniza el elemento actual de la variación.
>
>La sincronización solo funciona en el tipo de datos **Texto multilínea**.
>
>No está disponible como opción la transferencia de cambios *de una variación **a Principal***.

1. Abra el fragmento de contenido en el editor de fragmentos. Asegúrese de que **Principal** se ha editado.

1. Seleccione una variación específica y, a continuación, la acción de sincronización adecuada desde:

   * el selector desplegable **Acciones**, **Sincronizar elemento actual con principal**

     ![sincronización con principal](assets/cfm-variations-11a.png)

   * la barra de herramientas del editor de pantalla completa: **Sincronizar con principal**

     ![sincronización con principal](assets/cfm-variations-11b.png)

1. Principal y la variación se muestran en paralelo:

   * verde indica que se ha añadido contenido (a la variación)
   * rojo indica que el contenido se eliminó (de la variación)
   * azul indica texto reemplazado

   ![sincronización con principal](assets/cfm-variations-11c.png)

1. Seleccione **Sincronizar**: se actualiza y se muestra la variación.
