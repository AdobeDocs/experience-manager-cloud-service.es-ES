---
title: Creación de contenido con el editor universal
description: Aprenda lo fácil e intuitivo que es para los autores de contenido crear contenido con el editor universal.
source-git-commit: f454475b65da8f410812bbbe30ca5fc393be410a
workflow-type: tm+mt
source-wordcount: '1146'
ht-degree: 2%

---


# Creación de contenido con el editor universal {#authoring}

Aprenda lo fácil e intuitivo que es para los autores de contenido crear contenido con el editor universal.

## Introducción {#introduction}

El editor universal permite editar cualquier aspecto de cualquier contenido en cualquier implementación para ofrecer experiencias excepcionales, aumentar la velocidad de contenido y proporcionar una experiencia de desarrollador de última generación.

Para ello, proporciona a los autores de contenido una IU intuitiva que requiere una formación mínima para poder simplemente entrar y comenzar a editar contenido.

>[!TIP]
>
>Para obtener una introducción más detallada al Editor universal, consulte el documento [Introducción al Editor universal.](introduction.md)

>[!NOTE]
>
>El editor universal sigue en desarrollo y actualmente solo puede crear texto.

## Preparación de la aplicación {#prepare-app}

Para poder crear contenido para una aplicación con el Editor universal, un desarrollador debe instrumentar la aplicación para que admita el editor.

>[!TIP]
>
>Consulte el documento [Introducción al Editor universal en AEM](getting-started.md) para ver un ejemplo de cómo configurar una aplicación de AEM para que funcione con el Editor universal.

## Iniciar sesión {#sign-in}

Una vez instrumentada la aplicación para que funcione con el editor universal, deberá iniciar sesión en el editor universal. Necesitará un Adobe ID para iniciar sesión y [tienen acceso al editor universal.](getting-started.md#request-access)

Una vez que haya iniciado sesión, introduzca la dirección URL de la página que desea editar en la [barra de direcciones.](#address-bar) para comenzar [editar el contenido.](#edit-content)

## Comprender la IU {#ui}

La IU se divide en cuatro áreas principales.

* [El encabezado del Experience Cloud](#experience-cloud-header)
* [Encabezado del Editor universal](#universal-editor-header)
* [El carril](#rail)
* [El editor](#editor)

![IU del editor universal](assets/ui.png)

### Encabezado del Experience Cloud {#experience-cloud-header}

El encabezado del Experience Cloud siempre está presente en la parte superior de la pantalla. Es un anclaje que le dice dónde se encuentra dentro de Experience Cloud y le ayuda a navegar a otras aplicaciones de Experience Cloud.

![El encabezado del Experience Cloud](assets/experience-cloud-header.png)

#### Experience Manager {#experience-manager}

Seleccione el vínculo Adobe Experience Cloud que hay a la izquierda del encabezado para ir a la raíz de la solución de Experience Manager y acceder a herramientas como [Cloud Manager,](/help/onboarding/cloud-manager-introduction.md) [Cloud Acceleration Manager,](/help/journey-migration/cloud-acceleration-manager/introduction/overview-cam.md) y [Distribución de software.](https://experienceleague.adobe.com/docs/experience-cloud/software-distribution/home.html)

![Botón Navegación global](assets/global-navigation.png)

#### Organización {#organization}

Muestra la organización en la que ha iniciado sesión. Toque o haga clic para cambiar a otra organización si la Adobe ID está asociada a varias.

![Indicador de organización](assets/organization.png)

#### Soluciones {#solutions}

Al tocar o hacer clic en el conmutador de soluciones, puede ir rápidamente a otras soluciones de Experience Cloud.

![Conmutador de soluciones](assets/solutions.png)

#### Ayuda {#help}

El icono de ayuda proporciona acceso rápido a los recursos de aprendizaje y asistencia.

![Ayuda](assets/help.png)

#### Notificaciones {#notifications}

Este icono se mostrará con el número de asignaciones incompletas [notificaciones.](/help/implementing/cloud-manager/notifications.md)

![Notificaciones](assets/notifications.png)

#### Propiedades del usuario {#user-properties}

Toque o haga clic en el icono que represente al usuario para acceder a la configuración del usuario. Si no tiene una imagen de usuario configurada, se asignará aleatoriamente un icono.

![Propiedades del usuario](assets/user-properties.png)

### Encabezado del Editor universal {#universal-editor-header}

El encabezado del Editor universal siempre está presente en la parte superior de la pantalla, justo debajo [el encabezado del Experience Cloud.](#experience-cloud-header) Le permite acceder rápidamente a otra página para editarla y publicar la página actual.

![Encabezado del Editor universal](assets/universal-editor-header.png)

#### El menú Hamburger {#hamburger-menu}

El menú hamburguesa aún no está implementado.

![Menú Hambuger](assets/hamburger-menu.png)

#### Barra de direcciones {#address-bar}

La barra de direcciones muestra la ubicación de la página que está editando. Toque o haga clic para introducir la dirección de otra página que desea editar.

![Barra de direcciones](assets/address-bar.png)

>[!TIP]
>
>Utilice la tecla de acceso directo `L` para abrir la barra de direcciones.

>[!NOTE]
>
>Todas las páginas que desee editar con el Editor universal deben [instrumentado para admitir el Editor universal.](getting-started.md)

#### Indicador de colaboración {#collaboration}

Si hay otros autores con la misma página cargada en el Editor universal, se mostrarán las imágenes de esos autores. Pase el ratón sobre una imagen para ver el nombre de usuario completo

![Indicador de colaboración](assets/collaboration.png)

#### Abrir vista previa de la aplicación {#open-app-preview}

Toque o haga clic en el icono de vista previa de la aplicación abierta para abrir la página que esté editando en su propio explorador, sin tener que usar el editor para obtener una vista previa de los cambios.

![Abrir vista previa de la aplicación](assets/open-app-preview.png)

>[!TIP]
>
>Utilice la tecla de acceso directo `O` para abrir la vista previa de la aplicación.

#### Publicación {#publish}

Toque o haga clic en el botón de publicación para publicar los cambios en el contenido en directo para que los lectores los consuman.

![Botón Publicar](assets/publish.png)

### El carril {#rail}

El carril siempre está presente en la parte izquierda del editor. Permite cambiar fácilmente el editor entre el modo de previsualización y el de edición.

![El carril](assets/rail.png)

#### Modo de vista previa {#preview-mode}

En el modo de vista previa, la página representada en el editor tal como se vería en el servicio publicado. Esto permite al autor del contenido navegar por el contenido haciendo clic en los vínculos, etc.

![Modo de vista previa](assets/preview-mode.png)

>[!TIP]
>
>Utilice la tecla de acceso directo `P` para cambiar al modo de vista previa.

#### Modo de edición {#edit-mode}

En el modo de edición, la página se representa en el editor, pero el autor del contenido puede hacer clic para seleccionar el contenido que desea editar. Este es el modo predeterminado del editor cuando se carga una página.

Modo de ![edición](assets/edit-mode.png)

### Editor {#editor}

El editor ocupa la mayor parte de la ventana y es donde se encuentra la página especificada en [la barra de direcciones](#address-bar) se procesa.

Dependiendo de si el editor se encuentra en [modo de edición](#edit-mode) o [modo de vista previa,](#edit-mode) el contenido puede editarse o navegarse, respectivamente.

![Editor](assets/editor.png)

## Edición de contenido {#editing-content}

La edición de contenido es sencilla e intuitiva. En [modo de edición,](#edit-mode) al pasar el ratón sobre el contenido en el editor, el contenido editable se resaltará con un cuadro azul.

![El contenido editable se resalta con un cuadro azul](assets/editable-content.png)

Simplemente toque o haga clic en el contenido del cuadro azul para iniciar un editor in-situ para realizar los cambios. Pulse Intro o vuelva para guardar los cambios.

![Edición de contenido](assets/editing-content.png)

Tenga en cuenta que, en el modo de edición, pulsar o hacer clic en el contenido intenta seleccionarlo para su edición. Si desea navegar por el contenido mediante los siguientes vínculos, cambie a [modo de vista previa.](#preview-mode)

## Vista previa del contenido {#previewing-content}

Cuando haya terminado de editar contenido, a menudo querrá navegarlo para ver su aspecto en el contenido de otras páginas. En [modo de vista previa](#preview-mode) puede hacer clic en vínculos para navegar por el contenido como lo haría un lector. El contenido se representa en el editor tal como se publicaría.

Tenga en cuenta que, en el modo de vista previa, tocar o hacer clic en el contenido reacciona como lo haría para un lector del contenido. Si desea seleccionar el contenido que desea editar, cambie a [modo de edición.](#edit-mode)

## Recursos adicionales {#additional-resources}

Para obtener más información sobre el Editor universal, consulte estos documentos.

* [Introducción al Editor universal](introduction.md) : Descubra cómo el Editor universal permite editar cualquier aspecto de cualquier contenido en cualquier implementación para ofrecer experiencias excepcionales, aumentar la velocidad de contenido y proporcionar una experiencia de desarrollador de última generación.
* [Introducción al Editor universal en AEM](getting-started.md) : Obtenga información sobre cómo acceder al Editor universal y cómo instrumentar la primera aplicación de AEM para utilizarla.
* [Arquitectura de editor universal](architecture.md) - Obtenga información sobre la arquitectura del Editor universal y cómo fluyen los datos entre sus servicios y capas.
* [Atributos y tipos](attributes-types.md) : Obtenga información sobre los atributos y tipos de datos que requiere el Editor universal.
* [Autenticación del editor universal](authentication.md) - Obtenga información sobre cómo se autentica el editor universal.
