---
title: Información sobre conceptos básicos de creación
description: Obtenga información sobre los conceptos y la mecánica de creación de contenido para su CMS sin encabezado mediante Fragmentos de contenido.
exl-id: 3eca973f-b210-41bb-98da-ecbd2bae9803
source-git-commit: f7525b6b37e486a53791c2331dc6000e5248f8af
workflow-type: tm+mt
source-wordcount: '1708'
ht-degree: 93%

---

# Conceptos básicos de creación para usuarios sin encabezado con AEM {#author-headless-basics}

## La historia hasta ahora {#story-so-far}

Al principio del [recorrido del autor de contenido de AEM sin encabezado](overview.md), en la [introducción](introduction.md) se han abordado los conceptos básicos y la terminología relevante para la creación sin encabezado.

Este artículo se basa en estos elementos para que pueda comprender cómo crear su propio contenido para su proyecto de AEM sin encabezado.

## Objetivo {#objective}

* **Audiencia**: principiante
* **Objetivo**: presentar los conceptos básicos de la creación de CMS sin encabezado.
   * Introducción a la creación con AEMaaCS.
   * Introducción a los fragmentos de contenido.

## Gestión básica {#basic-handling}

Antes de comprender los fragmentos de contenido, aquí tiene una muy rápida introducción al uso de AEM.Aunque nada sustituye realmente la experiencia de iniciar sesión e intentar utilizar el sistema.

### Creación, previsualización y publicación {#author-preview-publish}

AEM Por lo general, una instalación de consta de tres entornos:

* Autor
* Publicación
* Vista previa

Inicie sesión y utilice el entorno de creación para generar su contenido. Cuando esté listo, publíquelo para que esté disponible para el público en general. Para el contenido sin encabezado, esto sería para otras aplicaciones, para páginas web sería para los lectores de la web.

Para obtener más información, consulte Conceptos de creación.

Desde el **Fragmentos de contenido** consola, también puede publicar en el **Servicio de previsualización**, para pruebas y previsualizaciones, antes de Publicar. Consulte Publicación y previsualización de un fragmento.

### Inicio de sesión {#signing-in}

Al igual que con la mayoría de los sistemas, debe iniciar sesión. Como autor, se le proporciona lo siguiente:

* Un nombre de usuario o de cuenta
* Una contraseña
* Un vínculo para acceder a la pantalla de inicio de sesión

Su cuenta se habrá configurado con los privilegios que necesite. Si tiene algún problema, le recomendamos que se ponga en contacto con su equipo de soporte interno del proyecto.

### Navegación {#navigation}

La primera vez que inicie sesión, un breve tutorial en línea resalta algunas de las funciones principales de la interfaz de usuario.

A continuación, puede utilizar el panel de navegación para acceder a las áreas clave de AEM. Para los fragmentos de contenido, se utiliza la variable **Fragmentos de contenido** consola (en algunas acciones, también se usa la variable **Assets** consola).

El panel de navegación se puede abrir seleccionando el icono de Adobe en la parte superior izquierda, seguido del icono de la brújula pequeña.

<!--
The Navigation Panel can be opened by selecting Adobe icon at the top left, followed by the small compass icon:

![Navigation panel](/help/journey-headless/author/assets/headless-journey-author-navigation-01.png)
-->

>[!NOTE]
>Aunque los fragmentos de contenido son una funcionalidad de AEM **Sites**, se guardan como **Recursos**. Se trata de un detalle técnico que no debería afectarle, pero que es útil conocer.

En la consola, puede seleccionar carpetas en el panel izquierdo para desplazarse hasta el fragmento de contenido; también puede filtrar o buscar.

![Consola Fragmentos de contenido](/help/sites-cloud/administering/content-fragments/assets/cfc-console-filter.png)

### Acciones: selección y visualización {#actions-selecting-viewing}

En la consola **Fragmentos de contenido** está disponible un rango de acciones para sus fragmentos de contenido desde la barra de herramientas.

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

Esta ha sido una introducción muy rápida a la interfaz de usuario (IU) de AEM, esperamos que haya tenido la oportunidad de probarla. Ahora llegamos a lo que realmente le interesa: los fragmentos de contenido sin encabezado.

Tendremos que revisar las cosas de principio a fin, pero es posible que su instancia ya tenga carpetas o fragmentos creados, y que estos se encuentren en diferentes ubicaciones. Los principios son los mismos.

### Organización y navegación {#organizing-and-navigating}

A menos que tenga muy pocos fragmentos de contenido, querrá organizarlos para que usted (y otros) puedan volver a encontrarlos.

#### Creación de una carpeta {#creating-folder}

Puede hacerlo creando una serie de carpetas dentro de la sección **Archivos** de la consola **Recursos**. Seleccione la opción **Crear** (parte superior derecha), seguido de **Carpeta**:

![Opción Crear carpeta](/help/journey-headless/author/assets/headless-journey-author-folder-01.png)

Se abre un cuadro de diálogo en el que puede introducir los detalles y confirmarlos con **Crear**:

![Cuadro de diálogo Crear carpeta](/help/journey-headless/author/assets/headless-journey-author-folder-02.png)

#### Uso de rutas y etiquetas para limitar los modelos de fragmento de contenido disponibles en la carpeta {#tags-paths-for-models-in-folder}

Esta sección es un poco más avanzada. En realidad no la necesita si acaba de empezar y está recién probando, pero es *muy* útil cuando tiene muchos fragmentos. Así que es bueno conocerla, aunque todavía no la utilice.

El arquitecto de contenido habrá creado todos los modelos de fragmento de contenido necesarios para el proyecto actual y tal vez también otros proyectos. Para simplificarle las cosas a usted y a otros autores, puede limitar la lista de modelos disponibles para una carpeta específica.

Tras crear la carpeta, puede abrir la carpeta **Propiedades**. Aquí hay varias pestañas con información y detalles de configuración sobre la carpeta. En concreto, para los fragmentos de contenido, puede usar la pestaña **Políticas** para definir rutas y etiquetas específicas para esta carpeta. Esto limita los modelos de fragmento de contenido disponibles para su uso en la carpeta, ya que significa que los modelos de fragmento de contenido deben cumplir estos requisitos antes de poder utilizarse para generar fragmentos en esta carpeta.

![Crear propiedades de carpeta: políticas](/help/journey-headless/author/assets/headless-journey-author-folder-04.png)

>[!NOTE]
>
>Puede leer más detalles en Modelos de fragmento de contenido: permitir modelos de fragmento de contenido en la carpeta Recursos.

A continuación, desplácese por estas carpetas para crear y editar los fragmentos de contenido.

#### Por si acaso: configuración de la carpeta de Cloud Services {#cloud-services-folder}

Por si acaso...

Probablemente, se le dará una carpeta inicial donde podrá crear sus carpetas. Así es como deben aplicarse algunos detalles de configuración (normalmente por un desarrollador o administrador del sistema) a la carpeta raíz. Probablemente esto no le interese, pero si es necesario, puede comprobar la **Configuración** en **Cloud Services** de la carpeta **Propiedades**:

![Propiedades de Crear carpeta: configuración](/help/journey-headless/author/assets/headless-journey-author-folder-03.png)

>[!NOTE]
>
>Puede obtener más información en Aplicar la configuración a la carpeta Recursos.

### Creación de un fragmento de contenido {#creating-fragment}

En la consola **Fragmentos de contenido**, puede utilizar **Crear** para abrir el cuadro diálogo **Fragmento de contenido nuevo**:

![Consola Fragmentos de contenido: Creación de un nuevo fragmento](/help/sites-cloud/administering/content-fragments/assets/cfc-console-create.png)

Especifique lo siguiente:

* **Ubicación**
* **Modelo de fragmento de contenido**
* **Título**
* **Nombre**
* **Descripción**

A continuación, confirme con: **Crear** o **Crear y abrir**.

<!--
Creating a Content Fragment is very similar - you just use the **Content Fragment** option instead:

![Create Content Fragment option](/help/journey-headless/author/assets/headless-journey-author-content-fragment-01.png)

This time a wizard opens. The first step is to select the Content Fragment Model that your fragment is based on:

![Create Content Fragment - select Model](/help/journey-headless/author/assets/headless-journey-author-content-fragment-02.png)

After continuing with **Next** you can supply the details (**Basic** and **Advanced**) for your fragment:

![Create Content Fragment - provide Name](/help/journey-headless/author/assets/headless-journey-author-content-fragment-03.png)

Confirm with **Create** and you can then **Open** your fragment in the editor.
-->

### Edición de un fragmento {#editing-fragment}

Puede abrir un fragmento inmediatamente después de crearlo o seleccionarlo en la consola Fragmentos de contenido (también desde la consola Recursos).

Cuando se abra el editor por primera vez, verá lo siguiente:

* Una lista de iconos en el lado izquierdo: esto le permite acceder a varias áreas de funcionalidad. El editor se abre en la pestaña **Variaciones**, que es donde se produce la mayor parte de la edición. También puede estar interesado en las pestañas **Anotaciones** y **Metadatos**.

* Un encabezado con información sobre el fragmento con acceso a varias acciones.

* El área de edición principal: esto depende del modelo utilizado para crear el fragmento.

Ejemplos:

* Un fragmento que solo requiere múltiples informaciones, algunas con un tipo específico. Para el contenido sin encabezado, las referencias son clave; más adelante, en el recorrido, aprenderá sobre ellas.

  ![Editor de fragmentos de contenido: mi fragmento](/help/journey-headless/author/assets/headless-journey-author-content-fragment-04.png)

* Un fragmento que permite escribir una sección larga de texto. Aquí hay opciones adicionales para administrar y dar formato al texto. Incluso puede abrir los campos de texto individuales en un editor de pantalla completa (con el icono en forma de pantalla pequeña de la derecha)

  ![Editor de fragmentos de contenido: Alaska Spirits](/help/journey-headless/author/assets/headless-journey-author-content-fragment-05.png)

>[!NOTE]
>
>Es posible que se requiera documentación específica del proyecto para ayudar a los autores con detalles sobre cómo completar correctamente algunos campos.
>
>Consulte Modelos de fragmentos de contenido: tipos de datos y propiedades para obtener detalles genéricos.

Confirme las actualizaciones con: **Guardar** o **Guardar y cerrar**.

>[!NOTE]
>
>Para obtener más información, puede leer Variaciones: creación de fragmentos de contenido.

#### Lo que probablemente no deba preocuparle {#what-you-probably-do-not-need-to-worry-about}

De acuerdo. Esta sección puede parecer un poco extraña, pero cuando abra el Editor de fragmentos de contenido y empiece a explorar, aparecerán varias opciones que no se aplican a su recorrido sin encabezado (probablemente) como Autor de contenido. Así que esto es tan solo un rápido avance de lo que debe ignorar en un contexto sin encabezado.

* **Modelos de fragmentos de contenido**

  Aparecerá el nombre del modelo de fragmento de contenido en la parte superior del editor, directamente debajo del nombre del fragmento. También se trata de un vínculo que conduce al editor de modelos.
Los modelos de fragmento de contenido son vitales para los fragmentos de contenido, ya que definen la estructura que se utiliza. Sin embargo, crearlos y editarlos es, normalmente, responsabilidad de otra persona, el arquitecto de contenido.

  >[!NOTE]
  >
  >Para obtener más información, puede leer el Recorrido para arquitectos de contenido sin encabezado de AEM.

* **Contenido asociado**

  Esto es bastante obvio, ya que es una pestaña del editor.

  Los fragmentos de contenido han estado disponibles en AEM desde hace ya varias versiones. En un principio, se pusieron a disposición para el uso “tradicional” cuando se creaban páginas.Se siguen utilizando en este contexto. Esto puede implicar asociar recursos (por ejemplo, imágenes) que, aunque no estén incrustados en el fragmento, deben estar disponibles para el autor cuando cree una página.

* **Vista previa**

  Esta es otra pestaña del editor y proporciona una vista técnica, destinada principalmente a los desarrolladores.

* **Actualizar referencias de página**

  Esta acción está disponible en el menú desplegable de los puntos suspensivos (**...**). No tiene interés para los autores sin encabezado, ya que está relacionado con la creación de páginas.

### Publicación {#publishing}

<!-- needs more details -->

Una vez completado el fragmento, puede **Publicarlo** para que esté disponible para las aplicaciones sin encabezado.

Las acciones de publicación están disponibles en el editor:

![Editor de fragmentos de contenido: mi fragmento](/help/journey-headless/author/assets/headless-journey-author-content-fragment-06.png)

>[!NOTE]
>
>También puede publicar el fragmento desde el **Assets** o **Fragmentos de contenido** consola.

## Siguientes pasos {#whats-next}

Ahora que ha aprendido lo básico, el siguiente paso es [Obtener información sobre las referencias](references.md). Se presentarán y explicarán las distintas referencias disponibles, y cómo crear niveles de estructura con las referencias de fragmento, una parte clave de la creación sin encabezado.

## Recursos adicionales {#additional-resources}

* [Conceptos de creación](/help/sites-cloud/authoring/getting-started/concepts.md)

* [Gestión básica](/help/sites-cloud/authoring/getting-started/basic-handling.md): esta página se basa principalmente en la consola **Sites**, pero la mayoría de funciones también son relevantes para la creación de los **Fragmentos de contenido** debajo de la consola **Recursos**.

   * [Panel de navegación   ](/help/sites-cloud/authoring/getting-started/basic-handling.md#navigation-panel)

   * [Encabezado](/help/sites-cloud/authoring/getting-started/basic-handling.md#the-header)

   * [Barra de herramientas de acciones](/help/sites-cloud/authoring/getting-started/basic-handling.md#actions-toolbar)

   * [Acciones rápidas   ](/help/sites-cloud/authoring/getting-started/basic-handling.md#quick-actions)

   * [Visualización y selección de los recursos](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources)

   * [Selector de carril](/help/sites-cloud/authoring/getting-started/basic-handling.md#rail-selector)

* [Trabajar con fragmentos de contenido](/help/sites-cloud/administering/content-fragments/content-fragments.md)

   * [Administración de los fragmentos de contenido](/help/sites-cloud/administering/content-fragments/content-fragments-managing.md)

   * [Aplicación de la configuración a la carpeta Recursos](/help/sites-cloud/administering/content-fragments/content-fragments-configuration-browser.md#apply-the-configuration-to-your-assets-folder)

   * [Creación de un fragmento de contenido](/help/sites-cloud/administering/content-fragments/content-fragments-managing.md#creating-a-content-fragment)

   * [Variaciones: creación de fragmentos de contenido](/help/sites-cloud/administering/content-fragments/content-fragments-variations.md)

   * Publicación

      * Desde el editor, o **Assets** consolar

         * [Publicación rápida ](/help/assets/manage-publication.md#quick-publish)

         * [Administrar publicación](/help/assets/manage-publication.md#manage-publication)

      * Desde el **Fragmentos de contenido** Consola

         * [Publicación y previsualización de un fragmento de contenido](/help/sites-cloud/administering/content-fragments/content-fragments-managing.md#publishing-and-previewing-a-fragment)

   * [Modelos de fragmento de contenido](/help/sites-cloud/administering/content-fragments/content-fragments-models.md)

      * [Modelos de fragmento de contenido: tipos de datos](/help/sites-cloud/administering/content-fragments/content-fragments-models.md#data-types)

      * [Modelos de fragmento de contenido: propiedades](/help/sites-cloud/administering/content-fragments/content-fragments-models.md#properties)

      * [Modelos de fragmento de contenido: permitir modelos de fragmento de contenido en la carpeta de recursos](/help/sites-cloud/administering/content-fragments/content-fragments-models.md#allowing-content-fragment-models-assets-folder)

* Guías de introducción
   * [Creación de una configuración sin encabezado de una carpeta de recursos](/help/headless/setup/create-assets-folder.md)

* Recorrido para arquitectos de contenido sin encabezado de AEM

* Recorrido de traducción de AEM sin encabezado
