---
title: Creación de plantillas de página
description: La plantilla define la estructura de la página resultante y, con el editor de plantillas, la creación y el mantenimiento de plantillas ya no es una tarea exclusiva para desarrolladores
exl-id: 4c9dbf26-5852-45ab-b521-9f051c153b2e
source-git-commit: 5ad33f0173afd68d8868b088ff5e20fc9f58ad5a
workflow-type: tm+mt
source-wordcount: '4570'
ht-degree: 55%

---

# Creación de plantillas de página   {#creating-page-templates}

Al crear una página, debe seleccionar una plantilla, que se utiliza como base para crear la nueva página. La plantilla define la estructura de la página resultante, cualquier contenido inicial y los componentes que se pueden utilizar.

Con el **Editor de plantillas**, la creación y el mantenimiento de plantillas ya no es una tarea exclusiva para desarrolladores. También puede participar un tipo de usuario avanzado, que se denomina **autor de la plantilla**. Los desarrolladores siguen necesitando configurar el entorno, crear bibliotecas de clientes y crear los componentes que se van a utilizar, pero una vez que estos conceptos básicos están establecidos, el **autor de la plantilla** tiene la flexibilidad de crear y configurar plantillas sin un proyecto de desarrollo.

El **Consola de plantillas** permite a los autores de plantillas:

* Crear una plantilla nueva o copiar una plantilla existente.
* Especifique el ciclo de vida de la plantilla.

El **Editor de plantillas** permite a los autores de plantillas:

* Agregue componentes a la plantilla y colóquelos en una cuadrícula adaptable.
* Preconfigurar los componentes. 
* Defina qué componentes se pueden editar en las páginas creadas con la plantilla.

Este documento explica cómo **autor de plantillas** Puede utilizar la consola y el editor de plantillas para crear y administrar plantillas editables.

Para obtener información detallada sobre cómo funcionan las plantillas editables en un nivel técnico, consulte el documento para desarrolladores [Plantillas de página](/help/implementing/developing/components/templates.md) para obtener más información.

>[!NOTE]
>
>El **Editor de plantillas** no admite la segmentación directamente en el nivel de plantilla. Las páginas creadas a partir de una plantilla editable pueden estar segmentadas, pero no es posible segmentar las plantillas en sí.

## Antes de comenzar {#before-you-start}

>[!NOTE]
>
>Un administrador debe configurar una carpeta de plantillas en el **Navegador de opciones de configuración** y aplicar los permisos adecuados para que un autor de una plantilla pueda crear una plantilla en esa carpeta.

Antes de empezar, es importante tener en cuenta que la creación de una nueva plantilla requiere colaboración. Por este motivo, para cada tarea se indica la [Función. ](#roles) Esto no afecta a cómo realmente utiliza una plantilla para crear una página, pero afecta al modo en que una página se relaciona con su plantilla.

### Funciones {#roles}

La creación de una nueva plantilla mediante la **consola Plantillas** y el **Editor de plantillas** requiere la colaboración entre las siguientes funciones:

* **Administradores**:
   * Crea una nueva carpeta de plantillas y requiere derechos `admin` (de administración).
   * Estas tareas también las suele realizar un desarrollador
* **Desarrollador**:
   * Se centra en los detalles técnicos/internos
   * Debe tener experiencia en el entorno de desarrollo.
   * Proporciona al autor de plantillas la información necesaria.
* **Autor de plantillas**:
   * Se trata de un autor determinado que es miembro del grupo `template-authors`.
      * Esto le asigna los privilegios y los permisos necesarios.
   * Puede configurar el uso de componentes y otros detalles de alto nivel que requieran:
      * Algunos conocimientos técnicos
         * Por ejemplo, el uso de patrones al definir rutas.
      * Información técnica del desarrollador.

Debido a la naturaleza de algunas tareas, como crear una carpeta, es necesario un entorno de desarrollo, y esto requiere conocimiento/experiencia.

Las tareas detalladas en este documento se enumeran con la función responsable de llevarlas a cabo.

## Creación y gestión de plantillas {#creating-and-managing-templates}

Al crear una nueva plantilla editable:

* Utilice el **Plantilla** consola. Esta opción está disponible en el **General** de la sección **Herramientas** consola.
   * O directamente en: `https://<host>:<port>/libs/wcm/core/content/sites/templates.html/conf`
* Puede [crear una carpeta para las plantillas](#creating-a-template-folder-admin), si lo necesita.
* [Crea una plantilla nueva](#creating-a-new-template-template-author), que inicialmente estará vacía.
* [Definición de propiedades adicionales](#defining-template-properties-template-author) para la plantilla, si es necesario
* [Editar la plantilla](#editing-templates-template-authors) para definir el:
   * [Estructura](#editing-a-template-structure-template-author): contenido predefinido que no se puede cambiar en las páginas creadas con la plantilla.
   * [Contenido inicial](#editing-a-template-initial-content-author): contenido predefinido que se puede cambiar en las páginas creadas con la plantilla.
   * [Diseño](#editing-a-template-layout-template-author): para una amplia gama de dispositivos.
   * [Estilos](/help/sites-cloud/authoring/features/style-system.md): defina los estilos que se van a utilizar con la plantilla y sus componentes.
* [Habilitar la plantilla](#enabling-a-template-template-author) para usar al crear una página
* [Permitir la plantilla](#allowing-a-template-author) para la página o rama requerida del sitio web
* [Publicación de la plantilla](#publishing-a-template-template-author) para que esté disponible en el entorno de publicación

>[!NOTE]
>
>A menudo, las **plantillas permitidas** se predefinen cuando su sitio web se configura inicialmente.

>[!TIP]
>
>No introduzca nunca en una plantilla información que deba internacionalizarse. <!-- Never enter any information that needs to be [internationalized](/help/sites-developing/i18n.md) into a template.-->
>
>Para elementos de plantilla como encabezados y pies de página que deben localizarse, utilice la variable [funciones de localización de los componentes principales.](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/get-started/localization.html?lang=es)

### Creación de una carpeta de plantillas: administrador {#creating-a-template-folder-admin}

Se debe crear una carpeta de plantillas para su proyecto que contenga las plantillas específicas del proyecto. Es una tarea de administración que se describe en el documento [Plantillas de páginas](/help/implementing/developing/components/templates.md#template-folders).-->

### Creación de una plantilla nueva: autor de plantillas {#creating-a-new-template-template-author}

1. Abra la **Consola de plantillas** (que encontrará en **Herramientas ->** **General**) y navegue a la carpeta requerida.

   >[!NOTE]
   >
   >En una instancia estándar de AEM, la carpeta **Global** ya existe en la consola de plantillas. Contiene plantillas predeterminadas y actúa como alternativa en caso de que no se encuentre ninguna política ni ningún tipo de plantilla en la carpeta actual.
   >
   >Una práctica recomendada es utilizar un [carpeta de plantillas creada para su proyecto](/help/implementing/developing/components/templates.md#template-folders).

1. Seleccione **Crear** y, a continuación, **Crear plantilla** para abrir el asistente.

1. Elija una **Tipo de plantilla**, luego seleccione **Siguiente**.

   >[!NOTE]
   >
   >Los tipos de plantilla son diseños de plantilla predefinidos y se pueden considerar como plantillas para una plantilla. Los desarrolladores o el administrador del sistema las predefinen. Encontrará más información en el documento para desarrolladores [Plantillas de páginas](/help/implementing/developing/components/templates.md#template-type).-->

1. Complete la **Detalles de plantilla**:

   * **Nombre de la plantilla**
   * **Descripción**

1. Seleccione **Crear**. Se muestra una confirmación, seleccione **Abrir** para empezar a editar la plantilla o **Listo** para volver a la consola de plantillas.

   >[!NOTE]
   >
   >Cuando se crea una plantilla nueva, se marca como **Borrador** en la consola; esto indica que aún no está disponible para que los autores de páginas la utilicen.

>[!NOTE]
>
>Las plantillas son herramientas útiles para optimizar el flujo de trabajo de creación de páginas. Sin embargo, demasiadas plantillas pueden saturar a los autores y hacer que la creación de páginas sea confusa. Una buena regla general es mantener el número de plantillas por debajo de 100.
>
>Adobe no recomienda tener más de 1000 plantillas debido a posibles impactos en el rendimiento.

### Definición de las propiedades de la plantilla: autor de plantillas   {#defining-template-properties-template-author}

Una plantilla puede tener las siguientes propiedades:

* Imagen
   * Imagen que se utilizará como [miniatura de la plantilla](#template-thumbnail-image) para ayudar en la selección, como en el asistente Crear página.
      * Se puede cargar
      * Se puede generar en función del contenido de la plantilla
* Título
   * Un título utilizado para identificar la plantilla, como en el **Crear página** asistente.
* Descripción
   * Una descripción opcional para proporcionar más información sobre la plantilla y su uso, que puede verse, por ejemplo, en el asistente de **Crear página**.

Para ver o editar las propiedades:

1. En la **Consola de plantillas**, seleccione la plantilla.
1. Para abrir el cuadro de diálogo, seleccione **Ver propiedades** en la barra de herramientas o en las opciones rápidas.
1. Ahora puede ver o editar las propiedades de la plantilla.

>[!NOTE]
>
>El estado de una plantilla (borrador, activada o desactivada) se indica en la consola.

#### Imagen de miniatura de plantilla {#template-thumbnail-image}

Para definir la miniatura de la plantilla:

1. Edite las propiedades de la plantilla.
1. Seleccione si desea cargar una miniatura o hacer que se genere a partir del contenido de la plantilla.
   * Si desea cargar una miniatura, toque o haga clic en **Cargar imagen**
   * Si desea generar una miniatura, toque o haga clic en **Generar previsualización**
1. Para ambos métodos se muestra una previsualización de la miniatura.
   * Si no es satisfactorio, toque o haga clic en **Borrar** para cargar otra imagen o volver a generar la miniatura.
1. Cuando esté satisfecho con la miniatura, toque o haga clic en **Guardar y cerrar**.

### Activación y autorización de una plantilla: autor de plantillas   {#enabling-and-allowing-a-template-template-author}

Para poder utilizar una plantilla al crear una página, debe:

* [Activar la plantilla](#enabling-a-template-template-author) para que esté disponible para utilizarla al crear páginas.
* [Permitir que la plantilla](#allowing-a-template-author) especifique las ramas de contenido en las que esta se puede utilizar.

#### Activación de una plantilla: autor de plantillas {#enabling-a-template-template-author}

Una plantilla se puede habilitar o deshabilitar para que esté disponible o no disponible en el **Crear página** asistente.

>[!CAUTION]
>
>Después de habilitar una plantilla, se muestra una advertencia cuando el autor de la misma empieza a actualizarla más. Se informa al usuario de que se puede hacer referencia a la plantilla, por lo que cualquier cambio puede afectar a las páginas que hacen referencia a la plantilla.

1. En la **Consola de plantillas**, seleccione la plantilla.
1. Seleccione **Activar** o **Desactivar** en la barra de herramientas y, de nuevo, en el cuadro de diálogo de confirmación.
1. Ahora puede usar la plantilla al [crear una página nueva](/help/sites-cloud/authoring/fundamentals/organizing-pages.md#creating-a-new-page), aunque probablemente desee [editar la plantilla](#editing-templates-template-authors) según sea necesario.

>[!NOTE]
>
>El estado de una plantilla (borrador, activada o desactivada) se indica en la consola.

#### Autorización de una plantilla: autor {#allowing-a-template-author}

Una plantilla puede estar disponible o no disponible para determinadas ramas de la página.

1. Abra [Propiedades de la página](/help/sites-cloud/authoring/fundamentals/page-properties.md) para la página raíz de la rama en que desea que la plantilla esté disponible.
1. Abra la pestaña **Avanzadas**.
1. En **Configuración de la plantilla**, utilice **Agregar campo** para especificar la(s) ruta(s) a su(s) plantilla(s).

   La ruta puede ser explícita o utilizar patrones. Por ejemplo:

   `/conf/<your-folder>/settings/wcm/templates/.*`

   El orden de las rutas es irrelevante. Se analizan todas las rutas y se recuperan las plantillas.

   >[!NOTE]
   >
   >Si la variable **Plantillas permitidas** La lista se deja vacía y el árbol se sube hasta encontrar un valor o una lista.
   >
   >
   >Consulte [Disponibilidad de plantillas](/help/implementing/developing/components/templates.md#template-availability): los principios para las plantillas permitidas siguen siendo los mismos.

1. Haga clic en **Guardar** para guardar los cambios realizados en las propiedades de la página.

>[!NOTE]
>
>Con frecuencia, las plantillas permitidas se predefinen para todo el sitio al configurarlo.

### Publicación de una plantilla: autor de plantillas {#publishing-a-template-template-author}

Puesto que la plantilla se toma como referencia cuando se representa la página, la plantilla completamente configurada debe publicarse para que esté disponible en el entorno de publicación.

1. En la **Consola de plantillas**, seleccione la plantilla.
1. Seleccione **Publicar** en la barra de herramientas para abrir el asistente.
1. Seleccione las **Políticas de contenido** que deben publicarse en combinación.
1. Seleccionar **Publish** en la barra de herramientas para completar la acción.

## Edición de plantillas: autores de plantillas   {#editing-templates-template-authors}

Al crear o editar una plantilla, hay varios aspectos que puede definir. Editar plantillas es similar a crear páginas.

El **Modo** selector de en la barra de herramientas permite seleccionar y editar la proporción adecuada de la plantilla:

* [Estructura](#editing-a-template-structure-template-author)
* [Contenido inicial](#editing-a-template-initial-content-author)
* [Diseño](#editing-a-template-layout-template-author)

![Selector de modo Editor de plantillas](/help/sites-cloud/authoring/assets/templates-mode.png)

Mientras que el **Política de página** opción en la **Información de página** El menú permite [seleccionar las directivas de página requeridas](#page-policies):

![Información de la página Editor de plantillas](/help/sites-cloud/authoring/assets/templates-page-information.png)

>[!CAUTION]
>
>Si un autor comienza a editar una plantilla que ya se ha habilitado, se muestra una advertencia. Se informa al usuario de que se puede hacer referencia a la plantilla, por lo que cualquier cambio puede afectar a las páginas que hacen referencia a la plantilla.

### Atributos de plantilla {#template-attributes}

Los atributos siguientes de una plantilla se pueden editar:

#### Estructura {#template-structure}

Los autores de la página no pueden mover/quitar de las páginas resultantes los componentes añadidos a la [estructura](#editing-a-template-structure-template-author). Si desea que los autores de páginas puedan añadir y quitar componentes a las páginas resultantes, debe añadir un sistema de párrafos a la plantilla.

Cuando los componentes están bloqueados, puede agregar contenido, que los autores de la página no pueden editar. Puede desbloquear componentes para definir lo siguiente [Contenido inicial](#editing-a-template-initial-content-author).

>[!NOTE]
>
>En el modo de estructura, cualquier componente que sea el padre de un componente desbloqueado no se puede mover, cortar ni eliminar.

#### Contenido inicial {#template-initial-content}

Cuando se ha desbloqueado un componente, puede definir lo siguiente [contenido inicial](#editing-a-template-initial-content-author) que se copia en las páginas resultantes, creadas a partir de la plantilla. Estos componentes desbloqueados se pueden editar en las páginas resultantes.

>[!NOTE]
>
>Entrada **Contenido inicial** y en las páginas resultantes, cualquier componente desbloqueado que tenga un elemento principal accesible (es decir, componentes dentro de un contenedor de diseño) se puede eliminar.

#### Diseño {#template-layout}

En [diseño](#editing-a-template-layout-template-author) puede predefinir el diseño de la plantilla para los formatos de dispositivo requeridos. El modo de **Diseño** para la creación de plantillas tiene la misma funcionalidad que el modo de [**Diseño** para la creación de páginas](/help/sites-cloud/authoring/features/responsive-layout.md#defining-layouts-layout-mode).

#### Políticas de la página {#template-page-policies}

En las [políticas de la página](#page-policies), puede conectar las políticas predefinidas de página a la página. Estas políticas de la página definen las diversas configuraciones de diseño.

#### Estilos {#template-styles}

El [sistema de estilos](/help/sites-cloud/authoring/features/style-system.md) permite a un autor de plantillas definir clases de estilos en la política de contenido de un componente, de modo que un autor de contenido puede seleccionarlos al editar el componente en una página. Estos estilos pueden ser variaciones visuales alternativas de un componente, lo que hacen que este sea más flexible.

Consulte la [documentación del sistema de estilos](/help/sites-cloud/authoring/features/style-system.md) para obtener más información.

### Edición de una plantilla: estructura, autor de plantillas {#editing-a-template-structure-template-author}

En el modo de **Estructura**, puede definir los componentes y el contenido de la plantilla, así como la política de la plantilla y sus componentes.

* Los componentes definidos en la estructura de la plantilla no se pueden mover a una página resultante ni eliminar de ninguna página resultante.
* Si desea que los autores de páginas puedan añadir y quitar componentes, agregue un sistema de párrafos a la plantilla.
* Los componentes pueden volver a desbloquearse y bloquearse para que pueda definir el [contenido inicial](#editing-a-template-initial-content-author).
* Se definen las políticas de diseño para los componentes y la página.

![Estructura de la página Editor de plantillas](/help/sites-cloud/authoring/assets/templates-page-structure.png)

Hay varias acciones que puede realizar en el modo **Estructura** del editor de plantillas y varias funciones que le ayudarán a:

#### Añadir componentes {#add-components}

Existen varios mecanismos para añadir componentes a la plantilla:

* Desde el **Componentes** explorador en el panel lateral.
* Mediante la opción **Insertar componente**, disponible en la barra de herramientas de los componentes que ya están en la plantilla o el cuadro **Arrastrar componentes aquí**.
* Al arrastrar un recurso (desde el **Assets** explorador en el panel lateral) directamente en la plantilla para generar el componente adecuado in situ.

Una vez añadido, cada componente se marca con:

* Un borde
* Un marcador para mostrar el tipo de componente
* Un marcador que se mostrará cuando se haya desbloqueado el componente

>[!NOTE]
>
>Al añadir un componente **Título** predefinido a la plantilla, contendrá la **estructura** de texto predeterminado.
>
>Si lo cambia, y añade su propio texto, este texto actualizado se utiliza cuando se crea una página a partir de la plantilla.
>
>Si deja el texto predeterminado (estructura), el título tendrá de manera predeterminada el nombre de la página siguiente.

>[!NOTE]
>
>Aunque no sea una operación idéntica, la adición de componentes y recursos a una plantilla tiene muchas similitudes con acciones similares que se llevan a cabo al [crear páginas](/help/sites-cloud/authoring/fundamentals/editing-content.md).

#### Acciones de componente {#component-actions}

Realice acciones en los componentes una vez añadidos a la plantilla. Cada instancia individual tiene una barra de herramientas que le permite acceder a las acciones disponibles, la barra de herramientas depende del tipo de componente.

![Barra de herramientas Acciones de un componente de plantilla](/help/sites-cloud/authoring/assets/templates-component-actions.png)

También puede depender de las acciones realizadas, por ejemplo, cuando se ha asociado una política al componente, el icono de configuración de diseño está disponible.

#### Editar y configurar {#edit-and-configure}

Con estas dos acciones, puede añadir contenido a los componentes.

#### Borde para indicar la estructura {#border-to-indicate-structure}

Al trabajar en **Estructura** mode un borde naranja indica el componente seleccionado actualmente. Una línea de puntos también indica el componente principal.

#### Política y propiedades (general) {#policy-and-properties-general}

Las políticas de contenido (o diseño) definen las propiedades de diseño de un componente. Por ejemplo, los componentes disponibles o las dimensiones mínimas/máximas. Se aplican a la plantilla (y a las páginas creadas con la plantilla).

Cree una política de contenido, o seleccione una existente, para un componente.

![Botón de política de contenido](/help/sites-cloud/authoring/assets/templates-content-policy-button.png)

Esto permite definir los detalles del diseño.

![Política de contenido](/help/sites-cloud/authoring/assets/template-content-policy.png)

La ventana de configuración se divide en dos.

* En la parte izquierda del cuadro de diálogo, debajo de la sección **Política**, puede seleccionar una política existente.
* En el lado derecho del cuadro de diálogo, debajo de la sección **Propiedades**, puede establecer las propiedades específicas del tipo de componente.

Las propiedades disponibles dependen del componente seleccionado. Por ejemplo, para un componente de texto, las propiedades definen las opciones de copia y pegado, las opciones de formato y el estilo de párrafo, entre otras opciones.

##### Política {#policy}

Las políticas de contenido (o diseño) definen las propiedades de diseño de un componente. Por ejemplo, los componentes disponibles o las dimensiones mínimas/máximas. Se aplican a la plantilla (y a las páginas creadas con la plantilla).

En **Política**, puede seleccionar una política existente para aplicarla al componente a través de la lista desplegable.

![Seleccionar política](/help/sites-cloud/authoring/assets/templates-policy-selector.png)

Para añadir una política nueva, seleccione el botón de adición situado junto a la lista desplegable **Seleccionar política.** Se debe proporcionar un título nuevo en el campo **Título de la política**.

![Botón Añadir política](/help/sites-cloud/authoring/assets/templates-add-policy-button.png)

La política existente seleccionada en la lista desplegable **Seleccionar política** se puede copiar como una política nueva mediante el botón de copia situado al lado de la lista desplegable. Se debe proporcionar un título nuevo en el campo **Título de la política**. De forma predeterminada, el título de la política copiada es **Copia de X**, donde X es el título de la directiva copiada.

![Botón Copiar política](/help/sites-cloud/authoring/assets/templates-copy-policy-button.png)

En el campo **Descripción de la política**, se ofrece de manera opcional una descripción de la política.

En la sección **Otras plantillas que también usan la política seleccionada**, puede ver con facilidad las otras plantillas que usan la política seleccionada en la lista desplegable **Seleccionar política**.

![Uso de una política existente](/help/sites-cloud/authoring/assets/templates-policy-use.png)

>[!NOTE]
>
>Si se añaden diversos componentes del mismo tipo como contenido inicial, la misma política se aplica a todos los componentes.

##### Propiedades {#properties}

En el **Propiedades** encabezado puede definir la configuración del componente. El encabezado tiene dos pestañas:

* Principal
* Características

###### Principal {#main}

En el **Principal** pestaña, se definen los ajustes más importantes del componente.

Por ejemplo, para un componente de imagen se pueden definir los anchos permitidos y habilitar la carga diferida.

Si una configuración permite varias configuraciones, toque o haga clic en **Añadir** para añadir otra configuración.

![Botón Añadir](/help/sites-cloud/authoring/assets/templates-add-button.png)

Para quitar una configuración, toque o haga clic en el botón **Eliminar** situado a la derecha de la configuración.

Para quitar una configuración, toque o haga clic en el botón **Eliminar**.

![Botón Eliminar](/help/sites-cloud/authoring/assets/templates-delete-button.png)

###### Características {#features}

El **Funciones** La pestaña permite activar o desactivar funciones adicionales del componente.

Por ejemplo, para un componente de imagen puede definir las proporciones de recorte, las orientaciones de imagen permitidas y si se permiten las cargas.

![Pestaña Características](/help/sites-cloud/authoring/assets/templates-features-tab.png)

>[!CAUTION]
>
>Tenga en cuenta que, en AEM, las proporciones de recorte se definen como **altura/anchura**. Esto es distinto de la definición convencional de anchura/altura y se realiza por motivos de compatibilidad con sistemas anteriores. Los usuarios de creación de páginas no notarán ninguna diferencia siempre que defina claramente el **Nombre**, ya que esto es lo que se muestra en la interfaz de usuario.

>[!NOTE]
>
>[Las políticas de contenido para componentes que implementan el editor de texto](/help/implementing/developing/extending/rich-text-editor.md) enriquecido solo se pueden definir para las opciones que RTE tiene disponibles en su configuración de interfaz de usuario.

#### Política y propiedades (contenedor de diseño) {#policy-and-properties-layout-container}

La configuración de directiva y propiedades de un contenedor de diseño es similar al uso general, pero con algunas diferencias.

>[!NOTE]
>
>La configuración de una directiva es obligatoria para los componentes del contenedor, ya que le permite definir los componentes disponibles en el contenedor.

La ventana de configuración se divide en dos, al igual que en el uso general de la ventana.

##### Política {#policy-layout}

Las políticas de contenido (o diseño) definen las propiedades de diseño de un componente. Por ejemplo, los componentes disponibles o las dimensiones mínimas/máximas. Se aplican a la plantilla (y a las páginas creadas con la plantilla).

En **Política**, puede seleccionar una política existente para aplicarla al componente a través de la lista desplegable. Esto funciona igual que en el uso general de la ventana.

##### Propiedades {#properties-layout}

En el **Propiedades** encabezado puede elegir qué componentes están disponibles para el contenedor de diseño y definir su configuración. El encabezado tiene tres pestañas:

* Componentes permitidos
* Componentes predeterminados
* Configuración adaptable

###### Componentes permitidos {#allowed-components}

En el **Componentes permitidos** , se definen qué componentes están disponibles para el contenedor de diseño.

* Los componentes se agrupan por sus grupos de componentes, que se pueden expandir y contraer.
* Se puede seleccionar un grupo completo marcando el nombre del grupo y se puede anular la selección de todos desmarcando.
* Un signo menos representa al menos uno, pero no todos los elementos de un grupo están seleccionados.
* Hay disponible una búsqueda para filtrar un componente por nombre.
* Los recuentos enumerados a la derecha del nombre del grupo de componentes representan el número total de componentes seleccionados en esos grupos, independientemente del filtro.

![Pestaña Componentes permitidos](/help/sites-cloud/authoring/assets/templates-allowed-components-tab.png)

###### Componentes predeterminados {#default-components}

En el **Componentes predeterminados** AEM pestaña, puede definir qué componentes se asocian automáticamente a determinados tipos de medios para que cuando un autor arrastre un recurso desde el explorador de recursos, sepa con qué componente lo asociará. Tenga en cuenta que solo los componentes con zonas de colocación están disponibles para esta configuración.

Haga clic o toque **Agregar asignación** para agregar un componente completamente nuevo y una asignación de tipo MIME.

Seleccione un componente en la lista y pulse o haga clic en **Agregar tipo** para agregar un tipo MIME adicional a un componente ya asignado. Haga clic en el icono **Eliminar** para quitar un tipo MIME.

![Pestaña Componentes predeterminados](/help/sites-cloud/authoring/assets/templates-default-components-tab.png)

###### Configuración adaptable {#responsive-settings}

En la pestaña **Configuración adaptable**, puede configurar el número de columnas de la cuadrícula resultante del contenedor de diseño.

#### Desbloquear y bloquear componentes {#unlock-and-lock-components}

Los componentes se desbloquean o bloquean para definir si el contenido está disponible para cambiar en **Contenido inicial** modo.

Cuando se ha desbloqueado un componente:

* Se muestra un indicador de candado abierto en el borde.
* La barra de herramientas de componentes se ajusta en consecuencia.
* El contenido introducido ya no se mostrará en **Estructura** modo.
   * El contenido que ya haya introducido se considera contenido inicial y solo es visible en el modo de **Contenido inicial**.
* Los componentes raíz del componente desbloqueado no se pueden mover, cortar ni eliminar.

![Botón Bloquear componente](/help/sites-cloud/authoring/assets/templates-unlock-component.png)

Esto incluye el desbloqueo de componentes de contenedor para que se puedan añadir más componentes, ya sea en el modo **Contenido inicial** o en las páginas resultantes. Si ya ha añadido componentes o contenido al contenedor antes de desbloquearlo, estos ya no se mostrarán en **Estructura** modo, pero se muestran en **Contenido inicial** modo. Entrada **Modo de estructura**, solo se muestra el propio componente contenedor con su lista de **Componentes permitidos**.

![Componentes permitidos](/help/sites-cloud/authoring/assets/templates-allowed-components.png)

Para ahorrar espacio, el contenedor de diseño no aumenta para dar cabida a la lista de componentes permitidos. En su lugar, el contenedor se convierte en una lista desplazable.

Los componentes que se pueden configurar se muestran con un icono de **directiva**, que se puede pulsar o hacer clic para editar la política y las propiedades de ese componente.

![Icono de componente configurable](/help/sites-cloud/authoring/assets/templates-configurable-component.png)

#### Relación con las páginas existentes {#relationship-to-existing-pages}

Si la estructura se actualiza después de crear páginas basadas en la plantilla, esas páginas reflejarán los cambios realizados en la plantilla. Se muestra una advertencia en la barra de herramientas para recordarle este hecho junto con los cuadros de diálogo de confirmación.

![Mensaje de aviso que indica que la plantilla está en uso](/help/sites-cloud/authoring/assets/templates-in-use-banner.png)

### Edición de una plantilla: contenido inicial, autor {#editing-a-template-initial-content-author}

**Contenido inicial** El modo se utiliza para definir el contenido que aparecerá cuando se cree una página por primera vez en función de la plantilla. Los autores de la página pueden editar el contenido inicial.

Aunque todo el contenido creado en el modo de **Estructura** sea visible en el **contenido inicial**, solo los componentes que se han desbloqueado se pueden seleccionar y editar.

>[!NOTE]
>
>El modo de **Contenido inicial** puede considerarse un modo de edición para las páginas creadas con esa plantilla. Por tanto, las políticas no se definen en el modo de **Contenido inicial**, sino en el modo de [**Estructura**](#editing-a-template-structure-template-author).

* Los componentes desbloqueados que están disponibles para la edición están marcados. Cuando se seleccionan, tienen un borde azul:

  ![Modo de contenido inicial](/help/sites-cloud/authoring/assets/templates-initial-content-mode.png)

* Los componentes desbloqueados tienen una barra de herramientas que le permite editar y configurar el contenido:

  ![Componente desbloqueado](/help/sites-cloud/authoring/assets/templates-unlocked-components.png)

* Si un componente de contenedor se ha desbloqueado (en el modo de **Estructura**), puede añadir componentes nuevos al contenedor (en el modo de **Contenido inicial**). Los componentes añadidos en el modo de **Contenido inicial** se pueden mover o eliminar de las páginas resultantes.

  Puede añadir un componente mediante el área **Arrastrar componentes aquí** o la opción **Insertar nuevo componente** de la barra de herramientas del contenedor adecuado.

  ![Añadir componente](/help/sites-cloud/authoring/assets/templates-add-component.png)
  ![Añadir componente](/help/sites-cloud/authoring/assets/templates-add-component-dialog.png)

* Si el contenido inicial de la plantilla se actualiza después de que se creen las páginas a partir de esta, esas páginas no se verán afectadas por los cambios del contenido inicial en la plantilla.

>[!NOTE]
>
>El contenido inicial está diseñado para preparar componentes y el diseño de página que sirven como punto de partida para la creación del contenido. No se pretende que sea el contenido real el que permanezca tal cual. Por este motivo, el contenido inicial no se puede traducir.
>
>Si necesita incluir texto traducible en la plantilla, como en encabezados o pies de página, puede utilizar las funciones de [localización de los componentes principales](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/get-started/localization.html?lang=es).

### Edición de una plantilla: diseño, autor de plantillas {#editing-a-template-layout-template-author}

Puede definir el diseño de la plantilla para una amplia gama de dispositivos. El [diseño interactivo](/help/sites-cloud/authoring/features/responsive-layout.md) para las plantillas funciona tal como lo hace para la creación de páginas.

>[!NOTE]
>
>Los cambios en el diseño se reflejan en **Contenido inicial** modo, pero no se observa ningún cambio en **Estructura** modo.

![Editar diseño de plantilla](/help/sites-cloud/authoring/assets/templates-edit-layout.png)

### Edición de una plantilla: política de página, autor/desarrollador de plantillas {#editing-a-template-page-policy-template-author-developer}

La política de página, incluidas las bibliotecas requeridas del lado del cliente, se mantiene en la opción **Política de página** del menú **Información de página**.

Para acceder al cuadro de diálogo **Política de página**:

1. En el **Editor de plantillas**, seleccione **Información de página** en la barra de herramientas y, luego, **Política de página** para abrir el cuadro de diálogo.
1. El cuadro de diálogo **Política de página** se abre y se divide en dos secciones:

   * La mitad izquierda define el [políticas de página](#page-policies)
   * La mitad derecha define el [propiedades de página](#page-properties)

   ![Política de página](/help/sites-cloud/authoring/assets/templates-page-design.png)

#### Políticas de la página {#page-policies}

Puede aplicar una política de contenido a la plantilla o a las páginas resultantes. De esta forma, se define la política de contenido para el sistema de párrafos principal de la página.

![Política de la página](/help/sites-cloud/authoring/assets/templates-page-policy.png)

* Puede seleccionar una política existente para la página en el menú desplegable **Seleccionar política**.

  ![Selector de políticas](/help/sites-cloud/authoring/assets/templates-policy-selector.png)

  Para añadir una política nueva, seleccione el botón de adición situado junto a la lista desplegable **Seleccionar política.** Se debe proporcionar un título nuevo en el campo **Título de la política**.

  ![Botón Añadir política](/help/sites-cloud/authoring/assets/templates-add-policy-button.png)

  La política existente seleccionada en la lista desplegable **Seleccionar política** se puede copiar como una política nueva mediante el botón de copia situado al lado de la lista desplegable. Se debe proporcionar un título nuevo en el campo **Título de la política**. De forma predeterminada, el título de la política copiada es **Copia de X**, donde X es el título de la directiva copiada.

  ![Botón Copiar política](/help/sites-cloud/authoring/assets/templates-copy-policy-button.png)

* Defina un título para la política en el campo **Título de la política**. Es necesario que una política tenga un título para que se pueda seleccionar fácilmente en la lista desplegable **Seleccionar política**.

  ![Título de la política](/help/sites-cloud/authoring/assets/templates-policy-title.png)

* En el campo **Descripción de la política**, se ofrece de manera opcional una descripción de la política.
* En la sección **Otras plantillas que también usan la política seleccionada**, puede ver con facilidad las otras plantillas que usan la política seleccionada en la lista desplegable **Seleccionar política**.

  ![Uso de políticas](/help/sites-cloud/authoring/assets/templates-policy-use.png)

#### Propiedades de página {#page-properties}

Con las propiedades de página, puede definir las bibliotecas del cliente necesarias mediante el cuadro de diálogo **Diseño de página**. Estas bibliotecas del cliente incluyen las hojas de estilo y el lenguaje Javascript que se van a cargar con la plantilla y las páginas creadas con esa plantilla.

![Propiedades de página](/help/sites-cloud/authoring/assets/templates-page-properties.png)

* Especifique las bibliotecas del lado del cliente que desea aplicar a las páginas creadas con esta plantilla. Al introducir el nombre de una biblioteca en el campo de texto del **Bibliotecas del cliente** sección.

  ![Bibliotecas del lado cliente](/help/sites-cloud/authoring/assets/templates-client-side-libraries.png)

* Si son necesarias diversas bibliotecas, haga clic en el botón Añadir para añadir un campo de texto adicional para el nombre de la biblioteca.

  ![Botón Añadir](/help/sites-cloud/authoring/assets/templates-add-button.png)

  Añada tantos campos de texto como sea necesario para las bibliotecas del cliente.

* Defina la posición relativa de las bibliotecas según sea necesario arrastrando los campos con el control de arrastre.

  ![Arrastrar controlador](/help/sites-cloud/authoring/assets/templates-drag-handle.png)

>[!NOTE]
>
>Si bien el autor de una plantilla puede especificar la política de página de la plantilla, deberá obtener información del desarrollador sobre las bibliotecas del cliente apropiadas.

### Edición de una plantilla: propiedades de la página inicial, autor {#editing-a-template-initial-page-properties-author}

Con la opción **Propiedades de la página inicial**, puede definir las [propiedades de la página](/help/sites-cloud/authoring/fundamentals/page-properties.md) inicial que se deben utilizar al crear páginas resultantes.

1. En el editor de plantillas, seleccione **Información de página** en la barra de herramientas y, luego, **Propiedades de la página inicial** para abrir el cuadro de diálogo.

1. En el cuadro de diálogo, puede definir las propiedades que desee aplicar a las páginas creadas con esta plantilla.

   ![Plantillas de propiedades de página inicial](/help/sites-cloud/authoring/assets/templates-initial-properties.png)

1. Confirme las definiciones con **Listo**.

## Prácticas recomendadas   {#best-practices}

Al crear plantillas, debe tener en cuenta lo siguiente:

1. Impacto de los cambios realizados en la plantilla una vez que se han creado páginas a partir de esa plantilla.

   Esta es una lista de las diferentes operaciones posibles en las plantillas, así como la forma en que afectan a las páginas creadas a partir de ellas:

   * Cambios en la estructura:

      * Se aplican inmediatamente a las páginas resultantes.
      * La publicación de la plantilla modificada sigue siendo necesaria para que los visitantes vean los cambios.

   * Cambios en las políticas de contenido y configuraciones de diseño:

      * Se aplican inmediatamente a las páginas resultantes.
      * Es necesaria la publicación de los cambios para que los visitantes puedan ver los cambios.

   * Cambios en el contenido inicial:

      * Esto solo se aplica a las páginas creadas después de los cambios en la plantilla.

   * Los cambios en el diseño dependen de si el componente modificado forma parte de:

      * Solo de estructura: aplicado inmediatamente
      * Incluir contenido inicial: solo en las páginas creadas después del cambio

   Tenga especial precaución cuando:

   * Bloquear o desbloquear componentes en plantillas habilitadas.
   * Esto puede tener efectos secundarios, ya que las páginas existentes ya pueden estar usándolo. Típicamente:

      * Faltan los componentes de desbloqueo (que estaban bloqueados) en las páginas existentes.
      * Bloquear componentes (que se podían editar) ocultará ese contenido para que no se muestre en las páginas.

   >[!NOTE]
   >
   >AEM proporciona advertencias explícitas al cambiar el estado de bloqueo de los componentes de las plantillas que ya no son borradores.

1. [Creación de sus propias carpetas](#creating-a-template-folder-admin) para las plantillas específicas del sitio.
1. [Publicación de plantillas](#publishing-a-template-template-author) desde el **Plantillas** consola.
