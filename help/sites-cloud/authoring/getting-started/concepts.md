---
title: Conceptos de creación
description: Conceptos sobre la creación de contenido en AEM
translation-type: tm+mt
source-git-commit: 16725342c1a14231025bbc1bafb4c97f0d7cfce8

---


# Creación Conceptos {#authoring-concepts}

Una instalación de AEM generalmente consta de al menos dos entornos:

* Creación
* Publicación

Interactúan para permitirle que el contenido esté disponible en el sitio web para que los visitantes puedan acceder a él.

El entorno de creación proporciona los mecanismos para crear, actualizar y revisar este contenido antes de publicarlo:

* Un autor crea y revisa el contenido. El contenido puede ser de muchos tipos diferentes, como páginas, recursos, publicaciones, etc.
* Este contenido se publicará en algún momento en su sitio web.

![Diagrama del autor, editor y expedidores](/help/sites-cloud/authoring/assets/author-publish.png)

En el entorno de creación, la funcionalidad de AEM está disponible a través de la interfaz de usuario de creación de AEM. Desde el entorno de publicación se diseña todo el aspecto y funcionamiento de la interfaz de usuario.

>[!NOTE]
>
>AEM se utiliza para publicar la documentación de AEM.

## Entorno de creación {#author-environment}

El autor trabaja en lo que se conoce como entorno **de** creación. Esto proporciona una interfaz fácil de usar (interfaz gráfica de usuario (GUI o UI) para crear el contenido. Requiere que el autor inicie sesión con una cuenta a la que se le hayan asignado los derechos de acceso correspondientes.

>[!NOTE]
>
>Su cuenta necesita tener los derechos de acceso correspondientes para crear, editar o publicar contenido.

Según la configuración de su instancia y sus derechos personales de acceso, puede realizar muchas tareas en el contenido, como (entre otras):

* Generación de contenido nuevo o edición de contenido existente en una página
* Uso de plantillas predefinidas para crear nuevas páginas de contenido
* Creación, edición y gestión de recursos y colecciones
* Mover, copiar y eliminar páginas de contenido, recursos, etc.
* Publicación (o cancelación de la publicación) de páginas, recursos, etc.

Asimismo, hay tareas administrativas que le ayudan a administrar su contenido:

* Flujos de trabajo que controlan cómo se administran los cambios, como la aplicación de una revisión antes de la publicación
* Proyectos que coordinan tareas individuales

>[!NOTE]
>
>AEM también se administra desde el entorno de creación.

## Entorno de publicación {#publish-environment}

When ready, your site&#39;s content is published to the **publish environment**. Aquí las páginas del sitio web se ponen a disposición de la audiencia objetivo de acuerdo con la apariencia de la interfaz diseñada.

Para obtener más información sobre la publicación y cancelación de publicaciones de páginas, consulte el documento [Publicación de páginas.](/help/sites-cloud/authoring/fundamentals/publishing-pages.md)

## Dispatcher {#dispatcher}

To optimize performance for visitors to your website, the **[dispatcher](/help/implementing/dispatcher/overview.md)**implements load balancing and caching.
