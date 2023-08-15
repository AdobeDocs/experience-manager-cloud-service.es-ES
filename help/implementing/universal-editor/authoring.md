---
title: Creación de contenido con el editor universal
description: Aprenda lo fácil e intuitivo que es para los autores crear contenido con el editor universal.
exl-id: 15fbf5bc-2e30-4ae7-9e7f-5891442228dd
source-git-commit: 5ad33f0173afd68d8868b088ff5e20fc9f58ad5a
workflow-type: tm+mt
source-wordcount: '2266'
ht-degree: 29%

---


# Creación de contenido con el editor universal {#authoring}

Aprenda lo fácil e intuitivo que es para los autores crear contenido con el editor universal.

## Introducción {#introduction}

El editor universal permite editar cualquier aspecto de cualquier contenido en cualquier implementación para que pueda ofrecer experiencias excepcionales, aumentar la velocidad del contenido y proporcionar una experiencia de desarrollador avanzada.

Para ello, el editor universal proporciona a los autores de contenido una interfaz de usuario intuitiva que requiere una formación mínima para simplemente poder saltar y comenzar a editar contenido. Este documento describe la experiencia de creación del editor universal.

>[!TIP]
>
>Para obtener una introducción más detallada al editor universal, consulte el documento [Introducción al editor universal.](introduction.md)

>[!NOTE]
>
>El editor universal aún está en desarrollo. Actualmente no puede editar todos los tipos de contenido.

## Preparación de la aplicación {#prepare-app}

Para crear contenido para una aplicación con el editor universal, la aplicación debe estar instrumentada por un desarrollador para admitir el editor.

>[!TIP]
>
>Consulte [AEM Introducción al editor universal en el entorno de trabajo de la aplicación de](getting-started.md) AEM para ver un ejemplo de cómo configurar una aplicación de la para que funcione con el editor universal.

## Inicio de sesión {#sign-in}

Una vez instrumentada la aplicación para que funcione con el editor universal, deberá iniciar sesión. Para el editor universal, necesitará el Adobe ID para iniciar sesión y [tener acceso.](getting-started.md#request-access)

Cuando haya iniciado sesión, introduzca la dirección URL de la página que desea editar en la [barra de ubicación.](#location-bar) para que pueda empezar a editar contenido como [contenido de texto](#text-mode) o [contenido multimedia.](#media-mode)

## Comprensión de la IU {#ui}

La interfaz de usuario de se divide en cinco áreas principales.

* [El encabezado de Experience Cloud](#experience-cloud-header)
* [El encabezado del editor universal](#universal-editor-header)
* [El carril de modo](#mode-rail)
* [El editor](#editor)
* [El carril de componentes](#component-rail)

![La IU del editor universal](assets/ui.png)

### El encabezado de Experience Cloud {#experience-cloud-header}

El encabezado de Experience Cloud siempre está presente en la parte superior de la pantalla. Es un anclaje que le dice dónde se encuentra dentro de Experience Cloud y le ayuda a navegar a otras aplicaciones.

![El encabezado de Experience Cloud](assets/experience-cloud-header.png)

#### Experience Manager {#experience-manager}

Seleccione el vínculo de Adobe Experience Cloud a la izquierda del encabezado para ir a la raíz de la solución de Experience Manager y acceder a herramientas como [Cloud Manager,](/help/onboarding/cloud-manager-introduction.md) [Cloud Acceleration Manager](/help/journey-migration/cloud-acceleration-manager/introduction/overview-cam.md) y [Distribución de software.](https://experienceleague.adobe.com/docs/experience-cloud/software-distribution/home.html?lang=es)

![Botón Navegación global](assets/global-navigation.png)

#### Organización {#organization}

Muestra la organización en la que ha iniciado sesión. Toque o haga clic para cambiar a otra organización si su Adobe ID está asociado a varias.

![Indicador de organización](assets/organization.png)

#### Soluciones {#solutions}

Al tocar o hacer clic en el conmutador de soluciones, puede ir rápidamente a otras soluciones de Experience Cloud.

![Conmutador de soluciones](assets/solutions.png)

#### Ayuda {#help}

El icono de ayuda proporciona acceso rápido a los recursos de aprendizaje y asistencia.

![Ayuda](assets/help.png)

#### Notificaciones {#notifications}

Este icono tiene la insignia con el número de asignaciones incompletas actualmente [notificaciones.](/help/implementing/cloud-manager/notifications.md)

![Notificaciones](assets/notifications.png)

#### Propiedades del usuario {#user-properties}

Toque o haga clic en el icono que representa a su usuario para acceder a la configuración. Si no tiene configurada una imagen de usuario, se asigna un icono de forma aleatoria.

![Propiedades del usuario](assets/user-properties.png)

### El encabezado del editor universal {#universal-editor-header}

El encabezado del editor universal siempre está presente en la parte superior de la pantalla, justo debajo [del encabezado de Experience Cloud.](#experience-cloud-header) Esto le permite desplazarse rápidamente a otra página para editarla y publicarla.

![Encabezado del editor universal](assets/universal-editor-header.png)

#### Menú de hamburguesa {#hamburger-menu}

El menú de hamburguesa aún no está implementado.

![Menú Hamburguesa](assets/hamburger-menu.png)

#### Barra de ubicación {#location-bar}

La barra de ubicación muestra la dirección de la página que está editando. Toque o haga clic para introducir la dirección de otra página que desea editar.

![Barra de ubicación](assets/location-bar.png)

>[!TIP]
>
>Utilice la tecla de acceso directo `L` para abrir la barra de direcciones.

>[!NOTE]
>
>Todas las páginas que desee editar deben [instrumentarse para admitir el editor universal.](getting-started.md)

#### Configuración del emulador {#emulator}

Toque o haga clic en el icono de emulación para definir cómo el Editor universal procesa la página.

![Icono Emulador](assets/emulator.png)

Al tocar o hacer clic en el icono de emulación, se muestran las opciones.

![Opciones de emulación](assets/emulation-options.png)

De forma predeterminada, el editor se abrirá en un diseño de escritorio en el que el explorador define automáticamente la altura y la anchura.

También puede emular un dispositivo móvil y en el Editor universal:

* Definir su orientación
* Definición del ancho y el alto
* Cambio de la orientación

#### Apertura de la vista previa de la aplicación {#open-app-preview}

Toque o haga clic en el icono de abrir vista previa de la aplicación para abrir la página que está editando en su propia pestaña del explorador, sin utilizar el editor, para previsualizar el contenido.

![Apertura de la vista previa de la aplicación](assets/open-app-preview.png)

>[!TIP]
>
>Utilice la tecla de acceso directo `O` (la letra O) para abrir la vista previa de la aplicación.

#### Publicación {#publish}

Toque o haga clic en el botón Publicar para poder publicar los cambios en el contenido en directo para que los consuman sus lectores.

![Botón Publicar](assets/publish.png)

>[!TIP]
>
>Consulte el documento [Publicación de contenido con el editor visual universal](publishing.md) para obtener más información sobre la publicación con el editor universal.

### El carril de modo {#rail}

El carril de modo siempre está presente en la parte izquierda del editor. Permite cambiar fácilmente el editor entre los diferentes modos de edición.

![El carril de modo](assets/mode-rail.png)

#### Modo de vista previa {#preview-mode}

En el modo de vista previa, la página se procesa en el editor tal como se vería en el servicio publicado. Esto permite al autor del contenido navegar por el contenido haciendo clic en los vínculos, etc.

![Modo de vista previa](assets/preview-mode.png)

>[!TIP]
>
>Utilice la tecla de acceso directo `P` para cambiar al modo de vista previa.

#### Modo de texto {#text-mode}

En el modo de texto, el autor del contenido puede hacer clic en para seleccionar contenido de texto.

![Modo de texto](assets/text-mode.png)

* Puede [editar texto sin formato](#editing-content) en su lugar.
* También puede [editar texto enriquecido](#editing-rich-text) en contexto con las opciones de formato adicionales que se muestran en el carril del componente.

>[!TIP]
>
>Utilice la tecla de acceso directo `T` para cambiar al modo de texto.

#### Modo multimedia {#media-mode}

En el modo multimedia, el autor del contenido puede hacer clic para seleccionar contenido multimedia.

![Modo Media](assets/media-mode.png)

Los detalles del contenido se muestran en el carril del componente y el autor también puede [editar el contenido multimedia.](#editing-media)

>[!TIP]
>
>Utilice la tecla de acceso directo `M` para cambiar al modo multimedia.

#### Modo de componente {#component-mode}

En el modo de componente, el autor del contenido puede hacer clic para seleccionar [Fragmentos de contenido.](/help/assets/content-fragments/content-fragments.md)

![Modo de componente](assets/component-mode.png)

Al seleccionar un fragmento de contenido, sus detalles se muestran en el carril del componente, donde puede [edite el fragmento de contenido.](#edit-content-fragment)

>[!TIP]
>
>Utilice la tecla de acceso directo `C` para cambiar al modo de componentes.

### El Editor {#editor}

El editor ocupa la mayor parte de la ventana y es donde la página especificada en [la barra de ubicación](#location-bar) se procesa.

* Si el editor se encuentra en un modo de edición como [modo de texto](#text-mode) o [modo multimedia,](#media-mode) el contenido se podrá editar, pero no podrá seguir los vínculos.
* Si el editor se encuentra en [modo de previsualización,](#preview-mode) el contenido es navegable y puede seguir los vínculos, pero no puede editar el contenido.

![Editor](assets/editor.png)

### Carril del componente {#component-rail}

El carril del componente siempre está presente a lo largo del lado izquierdo del editor. Según su modo, puede mostrar detalles de un componente seleccionado en el contenido o en la jerarquía del contenido de la página.

![El carril de componentes](assets/component-rail.png)

#### Modo de propiedades {#properties-mode}

En el modo de propiedades, el carril muestra las propiedades del componente seleccionado actualmente en el editor. Este es el modo predeterminado del carril del componente cuando se carga una página.

![Modo Propiedades](assets/properties-mode.png)

Según el tipo de componente que seleccione, los detalles se pueden mostrar y modificar en el carril de propiedades.

![Detalles del componente](assets/component-details.png)

Tenga en cuenta que no todos los componentes tienen detalles que se puedan mostrar o editar.

>[!TIP]
>
>Utilice la tecla de acceso directo `D` para cambiar al modo propiedades.

#### Modo de árbol de contenido {#content-tree-mode}

En el modo de árbol de contenido, el carril muestra la jerarquía del contenido de la página.

![Modo de árbol de contenido](assets/content-tree-mode.png)

Al seleccionar un elemento en el árbol de contenido, el editor se desplaza hasta ese contenido y lo selecciona.

![Árbol de contenido](assets/content-tree.png)

>[!TIP]
>
>Utilice la tecla de acceso directo `F` para cambiar al modo de árbol de contenido.

#### Editar {#edit}

En [modo de componente,](#component-mode) si selecciona una [Fragmento de contenido,](/help/assets/content-fragments/content-fragments.md) la opción editar aparece en el carril del componente.

![Icono Editar](assets/edit.png)

Al tocar o hacer clic en el botón Editar, se abre [Editor de fragmentos de contenido](/help/assets/content-fragments/content-fragments-managing.md#opening-the-fragment-editor) en una nueva pestaña, lo que le permite acceder a toda la potencia del Editor de fragmentos de contenido.

También puede editar los detalles del fragmento de contenido dentro del carril del componente según las necesidades del flujo de trabajo.

>[!TIP]
>
>Utilice la tecla de acceso directo `E` para editar un componente seleccionado.

#### Añadir {#add}

Si selecciona un componente de contenedor en el árbol de contenido o en el editor, la opción Añadir aparecerá en el carril del componente.

![Icono Agregar](assets/ue-add-component-icon.png)

Al tocar o hacer clic en el botón Agregar, se abre un menú desplegable de componentes disponibles para [añadir al contenedor seleccionado.](#adding-components)

>[!TIP]
>
>Utilice la tecla de acceso directo `A` para añadir un componente a un componente contenedor seleccionado.

#### Eliminar {#delete}

Si selecciona un componente dentro de un componente contenedor en el árbol de contenido o en el editor, la opción Eliminar aparece en el carril del componente.

![Icono Eliminar](assets/ue-delete-component-icon.png)

Toque o haga clic en el botón Eliminar [elimina el componente.](#deleting-components)

>[!TIP]
>
>Utilice la tecla de acceso directo `Shift+Backspace` para eliminar un componente seleccionado de un contenedor.

## Edición de contenido {#editing-content}

La edición de contenido es sencilla e intuitiva. En modos de edición ([modo de texto](#text-mode), [modo multimedia](#media-mode), y [modo componente](#component-mode)), cuando pasa el ratón sobre el contenido en el editor, el contenido editable se resalta con un cuadro azul.

![El contenido editable se resalta con un cuadro azul](assets/editable-content.png)

Tenga en cuenta que, en el modo de edición, que si toca o hace clic en el contenido se selecciona para editar. Si desea navegar por el contenido mediante los siguientes vínculos, cambie a [modo de vista previa.](#preview-mode)

Según la variable [modo](#mode-rail) una vez que se encuentra en y el contenido que selecciona, es posible que tenga diferentes opciones de edición y que pueda revisar propiedades adicionales para el contenido mediante [carril de componentes.](#component-rail)

### Edición de texto sin formato {#edit-plain-text}

Si está en [modo de texto](#text-mode) y seleccione un componente de texto sin formato, puede editar el texto en su lugar.

![Edición de contenido](assets/editing-content.png)

Simplemente escriba para actualizar el contenido. Pulse Intro o Retorno, o toque o haga clic fuera del cuadro de texto para guardar los cambios.

### Edición de texto enriquecido {#edit-rich-text}

Si está en [modo de texto](#text-mode) y seleccione un componente de texto enriquecido, puede editar el texto en su lugar.

Simplemente escriba para actualizar el contenido. Pulse Intro o Retorno, o toque o haga clic fuera del cuadro de texto para guardar los cambios.

Además, las opciones de formato y los detalles del texto están disponibles en el carril del componente.

![Edición de un componente de texto enriquecido](assets/rich-text-editing.png)

Los cambios de formato se guardan automáticamente en el contenido.

### Edición de medios {#edit-media}

Si está en [modo multimedia](#media-mode) cuando seleccione una imagen, puede ver sus detalles en el carril del componente.

![Edición de medios](assets/ue-edit-media.png)

Haga clic o pulse en **Reemplazar** botón situado debajo de la previsualización de la imagen seleccionada en el carril del componente para reemplazar la imagen por otra de la biblioteca de recursos.

1. El [selector de recursos](/help/assets/asset-selector.md#using-asset-selector) se abrirá una ventana para que pueda seleccionar un recurso.
1. Toque o haga clic para seleccionar un nuevo recurso.
1. Haga clic o pulse **Seleccionar** para volver al carril del componente donde se reemplazó el recurso.

Los cambios se guardan automáticamente en el contenido.

>[!TIP]
>
>Utilice la tecla de acceso directo `R` para abrir el selector de recursos que reemplazará la imagen seleccionada.

### Edición de fragmentos de contenido {#edit-content-fragment}

Si está en [modo componente](#component-mode) y selecciona una [Fragmento de contenido,](/help/assets/content-fragments/content-fragments.md) puede editar sus detalles en el carril del componente.

![Edición de un fragmento de contenido](assets/ue-edit-cf.png)

Los campos definidos en el modelo de contenido del fragmento de contenido seleccionado se muestran y pueden editarse en el carril del componente.

Los cambios se guardan automáticamente en el contenido.

Si desea editar el fragmento de contenido en la [Editor de fragmentos de contenido](/help/assets/content-fragments/content-fragments-managing.md#opening-the-fragment-editor) haga clic en el botón [botón editar](#edit) en el carril de modo.

### Adición de componentes a contenedores {#adding-components}

1. Seleccione un componente de contenedor en el árbol de contenido o en el editor.
1. A continuación, toque o haga clic en el icono Agregar en el carril del componente.

   ![Selección de un componente para añadirlo a un contenedor](assets/ue-add-component.png)

El componente se inserta en el contenedor y se puede editar en el editor.

### Eliminación de componentes de contenedores {#deleting-components}

1. Seleccione un componente de contenedor en el árbol de contenido o en el editor.
1. Toque o haga clic en el icono de cheurón del contenedor para expandir su contenido en el árbol de contenido.
1. A continuación, en el árbol de contenido, seleccione un componente dentro del contenedor.
1. Toque o haga clic en el icono Eliminar en el carril del componente.

   ![Eliminación de un componente](assets/ue-delete-component.png)

El componente seleccionado se ha eliminado.

### Reordenación de componentes en contenedores {#reordering-components}

1. Seleccione un componente de contenedor en el árbol de contenido o en el editor.
1. Si no está ya en [modo de árbol de contenido,](#content-tree-mode) cambiar a él.
1. Toque o haga clic en el icono de cheurón del contenedor para expandir su contenido en el árbol de contenido.
1. Arrastre los iconos de control junto a los componentes dentro del contenedor para mostrar que puede reorganizarlos. Arrastre los componentes para reordenarlos dentro del contenedor.

   ![Reordenación de componentes](assets/ue-reordering-components.png)
1. El componente arrastrado se vuelve gris en el árbol de componentes, mientras que el punto de inserción se representa mediante una línea azul. Suelte el componente para colocarlo en su nueva ubicación.

Los componentes se reordenan tanto en el árbol de contenido como en el editor

## Vista previa del contenido {#previewing-content}

Cuando haya terminado de editar el contenido, a menudo querrá navegar por él para ver cómo queda dentro del contenido de otras páginas. En el [modo de vista previa](#preview-mode), puede hacer clic en los vínculos para navegar por el contenido como lo haría un lector. El contenido se muestra en el editor tal y como se publicaría.

Tenga en cuenta que, en el modo de vista previa, tocar o hacer clic en el contenido reacciona como lo haría con un lector. Si desea seleccionar el contenido para editarlo, cambie a un modo de edición como [modo de texto](#text-mode) o [modo multimedia.](#media-mode)

## Recursos adicionales {#additional-resources}

Para obtener más información acerca del editor universal, consulte estos documentos.

* [Introducción al editor universal](introduction.md) - Descubra cómo el editor universal permite editar cualquier aspecto de cualquier contenido en cualquier implementación para que pueda ofrecer experiencias excepcionales, aumentar la velocidad del contenido y proporcionar una experiencia de desarrollador avanzada.
* [Publicación de contenido con el editor universal](publishing.md): descubra cómo el editor visual universal publica contenido y cómo sus aplicaciones pueden gestionar el publicado.
* [Introducción al editor universal en AEM](getting-started.md): obtenga información sobre cómo acceder al editor universal y cómo instrumentar la primera aplicación de AEM para utilizarlo.
* [Arquitectura del editor universal](architecture.md): obtenga información acerca de la arquitectura del editor universal y cómo fluyen los datos entre sus servicios y capas.
* [Atributos y tipos](attributes-types.md): obtenga información acerca de los atributos y tipos de datos que requiere el editor universal.
* [Autenticación del editor universal](authentication.md): obtenga información sobre cómo se autentica el editor universal.
