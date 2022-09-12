---
title: Información sobre conceptos básicos de creación
description: Obtenga información sobre los conceptos y la mecánica de creación de contenido para su CMS sin encabezado mediante fragmentos de contenido.
exl-id: 3eca973f-b210-41bb-98da-ecbd2bae9803
source-git-commit: 60ddcb3f2fd2219b0b1672791703582920825e81
workflow-type: tm+mt
source-wordcount: '1668'
ht-degree: 11%

---

# Conceptos básicos de creación para usuarios sin encabezado con AEM {#author-headless-basics}

## La historia hasta ahora {#story-so-far}

Al principio del [recorrido de autor de contenido sin encabezado de AEM](overview.md) el [Introducción](introduction.md) abarcaba los conceptos básicos y la terminología relevantes para la creación sin encabezado.

Este artículo se basa en estos elementos para que pueda comprender cómo crear su propio contenido para AEM proyecto sin objetivos.

## Objetivo {#objective}

* **Audiencia**: Principiante
* **Objetivo**: Presente los conceptos básicos de la creación de CMS sin encabezado:
   * Introducción a la creación con AEMaaCS
   * Introducción a los fragmentos de contenido

## Gestión básica {#basic-handling}

Antes de comprender los fragmentos de contenido, aquí tiene una (muy) rápida introducción al uso de AEM....pero nada sustituye realmente la experiencia de iniciar sesión e intentar utilizar el sistema.

### Creación y publicación {#author-preview-publish}

Una instalación de AEM generalmente consta de al menos dos entornos:

* Autor
* Publicación

Inicie sesión y utilice el entorno de creación para generar el contenido. Cuando esté listo, publique el contenido para que esté disponible para el público en general. Para que esto no sea necesario, esto sería para otras aplicaciones, para páginas web esto sería para los lectores en la web.

Para obtener más información, consulte Conceptos de creación.

### Iniciar sesión {#signing-in}

Al igual que con la mayoría de los sistemas, tendrá que iniciar sesión. Como autor, se le proporcionará:

* Nombre de usuario (cuenta)
* Contraseña
* Vínculo para acceder a la pantalla de inicio de sesión

Su cuenta se habrá configurado con los privilegios que necesite. Si tiene algún problema, le recomendamos que se ponga en contacto con su equipo de soporte interno del proyecto.

### Navegación {#navigation}

La primera vez que inicie sesión en un pequeño tutorial en línea resaltará algunas de las funciones principales de la interfaz de usuario.

A continuación, puede utilizar el panel de navegación para acceder a áreas clave de AEM. Para los fragmentos de contenido se utilizará la variable **Fragmentos de contenido** consola (para algunas acciones, también utilizará la variable **Recursos** consola).

El panel de navegación se puede abrir seleccionando el icono de Adobe en la parte superior izquierda, seguido del icono de pequeña brújula.

<!--
The Navigation Panel can be opened by selecting Adobe icon at the top left, followed by the small compass icon:

![Navigation panel](/help/journey-headless/author/assets/headless-journey-author-navigation-01.png)
-->

>[!NOTE]
>Aunque los fragmentos de contenido son una característica de AEM **Sitios**, se guardan como **Recursos**. Se trata de un detalle técnico que no debería afectarle, pero que podría ser útil conocer.

En la consola, puede seleccionar carpetas en el panel izquierdo para desplazarse hasta el fragmento de contenido. También puede filtrar o buscar.

![Consola Fragmentos de contenido](/help/sites-cloud/administering/content-fragments/assets/cfc-console-filter.png)

### Acciones, Seleccionar, Ver {#actions-selecting-viewing}

En la consola **Fragmentos de contenido** está disponible un rango de acciones para sus fragmentos de contenido desde la barra de herramientas:

<!-- ![Console actions](assets/cfm-managing-cf-console-01.png) -->

* **Abrir en Recursos**
* **Crear**
* La columna **Referenciado por** también proporciona un vínculo directo para mostrar todas las referencias principales de ese fragmento; incluida la referencia a fragmentos de contenido, fragmentos de experiencias y páginas.
* Al pasar el ratón por encima del nombre de la carpeta, se mostrará la ruta JCR.

Después de seleccionar el fragmento, están disponibles todas las acciones apropiadas:

<!-- ![Console actions - fragment selected](assets/cfm-managing-cf-console-selected-01.png) -->

* **Abrir**
* **Publicación** (y **Cancelar la publicación**)
* **Copiar**
* **Mover**
* **Cambiar nombre**
* **Eliminar**

>[!NOTE]
>
>Acciones como Publicar, Cancelar la publicación, Eliminar, Mover, Cambiar el nombre, Copiar, activar un trabajo asincrónico. El progreso de ese trabajo se puede monitorizar a través de la interfaz de usuario de trabajos asincrónicos de AEM.

<!--
The **Assets** console has dedicated **Action Toolbars**, and **Quick Actions** that you can use after selecting a resource (for example, a folder or content fragment).

The Quick Actions are available for a single resource, see **Basel** in the example below:

![Quick Actions](/help/journey-headless/author/assets/headless-journey-author-navigation-05.png)

The Actions Toolbar provides access to the full range of actions - applicable for the current scenario. The actions available can change; for example, dependent on your location, or whether you have selected multiple resources:

![Action Toolbar](/help/journey-headless/author/assets/headless-journey-author-navigation-06.png)

You can select the format for viewing your resources with the View Selector:

![View Selector](/help/journey-headless/author/assets/headless-journey-author-navigation-03.png)

You can view additional information about items using the Rail Selector. This also gives access to additional actions.

![Left Rail](/help/journey-headless/author/assets/headless-journey-author-navigation-04.png)
-->

## Creación de fragmentos de contenido {#authoring-content-fragments}

Por lo tanto, fue una introducción muy rápida a la interfaz de usuario de AEM (IU), pero esperamos que haya tenido la oportunidad de probarla. Ahora llegamos a su verdadero interés - Fragmentos de contenido para sin objetivos.

Tendremos que pasar por las cosas de principio a fin, pero es posible que la instancia ya tenga carpetas o fragmentos creados y que estos se encuentren en ubicaciones diferentes. Los principios son los mismos.

### Organización y navegación {#organizing-and-navigating}

A menos que tenga muy pocos fragmentos de contenido, querrá organizarlos para que usted (y otros) puedan volver a encontrarlos.

#### Creación de una carpeta {#creating-folder}

Puede hacerlo creando una serie de carpetas dentro de **Archivos** de la sección **Recursos** consola. Seleccione el **Crear** (parte superior derecha), seguido de **Carpeta**:

![Opción Crear carpeta](/help/journey-headless/author/assets/headless-journey-author-folder-01.png)

Se abrirá un cuadro de diálogo en el que puede introducir los detalles y confirmar con **Crear**:

![Cuadro de diálogo Crear carpeta](/help/journey-headless/author/assets/headless-journey-author-folder-02.png)

#### Uso de rutas y etiquetas para limitar los modelos de fragmento de contenido disponibles en la carpeta {#tags-paths-for-models-in-folder}

Esta sección está ligeramente más avanzada. Realmente no lo necesitas si estás empezando y probando cosas, pero es *very* útil cuando tiene muchos fragmentos. Así que es bueno saber - incluso si todavía no lo usan.

El arquitecto de contenido habrá creado todos los modelos de fragmento de contenido necesarios para el proyecto actual y tal vez también otros proyectos. Para ayudarle a que las cosas sean sencillas para usted y para otros autores, puede limitar la lista de modelos disponibles para una carpeta específica.

Después de crear la carpeta, puede abrirla **Propiedades**. Aquí hay varias pestañas con información y detalles de configuración sobre la carpeta. En concreto, para los fragmentos de contenido, puede usar la variable **Políticas** para definir rutas y etiquetas específicas para esta carpeta. Esto limita los modelos de fragmento de contenido disponibles para su uso en la carpeta, ya que significa que los modelos de fragmento de contenido deben cumplir estos requisitos antes de poder utilizarse para generar fragmentos en esta carpeta.

![Crear propiedades de carpeta: políticas](/help/journey-headless/author/assets/headless-journey-author-folder-04.png)

>[!NOTE]
>
>Puede leer más detalles en Modelos de fragmento de contenido: Permitir modelos de fragmento de contenido en la carpeta de recursos.

A continuación, desplácese por estas carpetas para crear y editar los fragmentos de contenido.

#### Por si acaso: Configuración de Cloud Services de carpeta {#cloud-services-folder}

Por si acaso...

Probablemente se le dará una carpeta inicial donde puede crear sus carpetas. Esto es así como algunos detalles de configuración deben aplicarse (normalmente por un desarrollador o administrador del sistema) a la carpeta raíz. Probablemente esto no le interese, pero si es necesario, puede comprobar el **Configuración** en el **Cloud Services** de la carpeta **Propiedades**:

![Crear propiedades de carpeta: configuración](/help/journey-headless/author/assets/headless-journey-author-folder-03.png)

>[!NOTE]
>
>Puede leer más en Aplicar la configuración a la carpeta de recursos.

### Creación de un fragmento de contenido {#creating-fragment}

En el **Fragmentos de contenido** consola, puede usar **Crear** para abrir el **Nuevo fragmento de contenido** diálogo:

![Consola Fragmentos de contenido: Creación de un nuevo fragmento](/help/sites-cloud/administering/content-fragments/assets/cfc-console-create.png)

Especifique el:

* **Lugar de residencia**
* **Modelo de fragmento de contenido**
* **Título**
* **Nombre**
* **Descripción**

A continuación, confirme con: **Crear** o **Crear y abrir**.

<!--
Creating a Content Fragment is very similar - you just use the **Content Fragment** option instead:

![Create Content Fragment option](/help/journey-headless/author/assets/headless-journey-author-content-fragment-01.png)

This time a wizard opens. The first step is to select the Content Fragment Model that your fragment will be based on:

![Create Content Fragment - select Model](/help/journey-headless/author/assets/headless-journey-author-content-fragment-02.png)

After continuing with **Next** you can supply the details (**Basic** and **Advanced**) for your fragment:

![Create Content Fragment - provide Name](/help/journey-headless/author/assets/headless-journey-author-content-fragment-03.png)

Confirm with **Create** and you can then **Open** your fragment in the editor.
-->

### Edición de un fragmento {#editing-fragment}

Puede abrir un fragmento inmediatamente después de crearlo o seleccionarlo en la consola Fragmentos de contenido (también desde la consola Recursos).

Cuando se abra el editor por primera vez, verá:

* Una lista de iconos en el lado izquierdo : esto le permite acceder a varias áreas de funcionalidad. El editor se abre en la variable **Variaciones** , aquí es donde ocurre la mayor parte de la edición. También puede estar interesado en el **Anotaciones** y **Metadatos** pestañas.

* Un encabezado con información sobre el fragmento y acceso a varias acciones.

* El área de edición principal - esto depende del modelo utilizado para crear el fragmento.

Como ejemplos:

* Un fragmento que solo requiere múltiples fragmentos de información, algunos con un tipo específico. Para el contenido sin encabezado, las referencias son clave, más adelante en el recorrido aprenderá sobre ellas.

   ![Editor de fragmentos de contenido: Mi fragmento](/help/journey-headless/author/assets/headless-journey-author-content-fragment-04.png)

* Un fragmento que le permite escribir una larga sección de texto. Aquí hay opciones adicionales para administrar y dar formato al texto. Incluso puede abrir los campos de texto individuales en un editor de pantalla completa (con el icono de aspecto de pantalla pequeña de la derecha)

   ![Editor de fragmentos de contenido: Espíritus alaska](/help/journey-headless/author/assets/headless-journey-author-content-fragment-05.png)

>[!NOTE]
>
>Es posible que se requiera documentación específica del proyecto para ayudar a los autores con detalles sobre cómo completar correctamente algunos campos.
>
>Consulte Modelos de fragmentos de contenido: tipos de datos y propiedades para obtener detalles genéricos.

Confirme las actualizaciones con: **Guardar** o **Guardar y cerrar**.

>[!NOTE]
>
>Para obtener más información, puede leer Variaciones: creación de fragmentos de contenido.

#### De lo que (probablemente) no necesita preocuparse {#what-you-probably-do-not-need-to-worry-about}

OK, esta sección puede parecer un poco extraña, pero una vez que abra el Editor de fragmentos de contenido y empiece a explorar, verá varias opciones que (probablemente) no se aplican a su recorrido sin encabezado como Autor de contenido. Así que esto es solo un rápido análisis de lo que deberían ser capaces de ignorar en un contexto sin objetivos:

* **Modelos de fragmentos de contenido**

   Verá el nombre del modelo de fragmento de contenido en la parte superior del editor, directamente debajo del nombre del fragmento. También se trata de un vínculo que le lleva al editor de modelos.
Los modelos de fragmento de contenido son vitales para los fragmentos de contenido, ya que definen la estructura que utiliza. Sin embargo, crearlos y editarlos es (normalmente) responsabilidad de otra persona, el arquitecto de contenido.

   >[!NOTE]
   >
   >Si desea obtener más información, puede leer el Recorrido de arquitectos de contenido sin encabezado de AEM.

* **Contenido asociado**

   Esta es bastante obvia ya que es una ficha en el editor.

   Los fragmentos de contenido han estado disponibles en AEM durante algunas versiones. Originalmente estaban disponibles para uso &quot;tradicional&quot; al crear páginas....y se siguen utilizando en este contexto. Esto puede implicar asociar recursos (por ejemplo imágenes) que, aunque no estén incrustados en el fragmento, deben estar disponibles para el autor al crear una página.

* **Previsualizar**

   Esta es otra ficha del editor y proporciona una vista técnica, principalmente para desarrolladores.

* **Actualizar referencias de página**

   Esta acción está disponible en el **...** desplegable (elipses). No es interesante para los autores sin encabezado ya que está relacionado con la creación de páginas.

### Publicación {#publishing}

<!-- needs more details -->

Una vez completado el fragmento, puede **Publicación** para que esté disponible para las aplicaciones sin encabezado.

Las acciones de publicación están disponibles en el editor (o en la barra de herramientas de **Fragmentos de contenido** o **Recursos** consola):

![Editor de fragmentos de contenido: Mi fragmento](/help/journey-headless/author/assets/headless-journey-author-content-fragment-06.png)

## Siguientes pasos {#whats-next}

Ahora que ha aprendido lo básico, el siguiente paso es [Obtenga información sobre las referencias](references.md). Esto introducirá y debatirá las distintas referencias disponibles, y cómo crear niveles de estructura con las referencias de fragmento, una parte clave de la creación para que no tenga objetivos.

## Recursos adicionales {#additional-resources}

* [Conceptos de creación](/help/sites-cloud/authoring/getting-started/concepts.md)

* [Gestión básica](/help/sites-cloud/authoring/getting-started/basic-handling.md) : esta página se basa principalmente en la variable **Sitios** consola, pero muchas/más funciones también son relevantes para la creación **Fragmentos de contenido** en el **Recursos** consola.

   * [Panel de navegación   ](/help/sites-cloud/authoring/getting-started/basic-handling.md#navigation-panel)

   * [Encabezado](/help/sites-cloud/authoring/getting-started/basic-handling.md#the-header)

   * [Barra de herramientas de acciones](/help/sites-cloud/authoring/getting-started/basic-handling.md#actions-toolbar)

   * [Acciones rápidas   ](/help/sites-cloud/authoring/getting-started/basic-handling.md#quick-actions)

   * [Visualización y selección de los recursos](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources)

   * [Selector de carril](/help/sites-cloud/authoring/getting-started/basic-handling.md#rail-selector)

   * Publicación

      * [Publicación rápida ](/help/assets/manage-publication.md#quick-publish)

      * [Administrar publicación](/help/assets/manage-publication.md#manage-publication)

* [Trabajar con fragmentos de contenido](/help/sites-cloud/administering/content-fragments/content-fragments.md)

   * [Administrar fragmentos de contenido](/help/sites-cloud/administering/content-fragments/content-fragments-managing.md)

      * [Aplicar la configuración a la carpeta de recursos](/help/sites-cloud/administering/content-fragments/content-fragments-configuration-browser.md#apply-the-configuration-to-your-assets-folder)

      * [Creación de un fragmento de contenido](/help/sites-cloud/administering/content-fragments/content-fragments-managing.md#creating-a-content-fragment)
   * [Variaciones: creación de fragmentos de contenido](/help/sites-cloud/administering/content-fragments/content-fragments-variations.md)

   * [Modelos de fragmento de contenido](/help/sites-cloud/administering/content-fragments/content-fragments-models.md)

      * [Modelos de fragmento de contenido: tipos de datos](/help/sites-cloud/administering/content-fragments/content-fragments-models.md#data-types)

      * [Modelos de fragmento de contenido: propiedades](/help/sites-cloud/administering/content-fragments/content-fragments-models.md#properties)

      * [Modelos de fragmento de contenido: permitir modelos de fragmento de contenido en la carpeta de recursos](/help/sites-cloud/administering/content-fragments/content-fragments-models.md#allowing-content-fragment-models-assets-folder)


* Guías de introducción
   * [Creación de una configuración sin encabezado de carpeta de recursos](/help/headless/setup/create-assets-folder.md)

* Recorrido de arquitecto de contenido de AEM Headless

* recorrido de traducción AEM sin encabezado
