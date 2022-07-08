---
title: Conceptos de creación
description: Conceptos sobre la creación de contenido en AEM
exl-id: ee9e4952-e075-4398-b31f-d7886153efff
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: ht
source-wordcount: '349'
ht-degree: 100%

---

# Conceptos de creación {#authoring-concepts}

Una instalación de AEM generalmente consta de al menos dos entornos:

* Autor
* Publicación

Interactúan para permitirle ofrecer contenido en su sitio web para que los visitantes puedan acceder a él.

El entorno de creación ofrece mecanismos para crear, actualizar y revisar el contenido antes de publicarlo:

* Un creador se encarga de crear y revisar el contenido. El contenido puede ser de muchos tipos diferentes, como páginas, recursos, publicaciones, etc.
* Este, en algún momento, se publica en su sitio web.

![Diagrama del creador, el editor y los distribuidores](/help/sites-cloud/authoring/assets/author-publish.png)

En el entorno de creación, las funciones de AEM están disponibles mediante la IU de creación de AEM. Desde el entorno de publicación se diseña todo el aspecto y funcionamiento de la interfaz de usuario.

## Entorno de creación {#author-environment}

El creador trabaja en lo que se conoce como **entorno de creación**. Esto proporciona una interfaz fácil de usar (interfaz gráfica de usuario (GUI o IU)) para crear el contenido. Requiere que el creador inicie sesión con una cuenta a la que se le hayan asignado los derechos de acceso correspondientes.

>[!NOTE]
>
>Su cuenta necesita tener los derechos de acceso correspondientes para crear, editar o publicar contenido.

Según la configuración de su instancia y sus derechos personales de acceso, puede realizar muchas tareas en el contenido, como (entre otras):

* Generar contenido nuevo o editar contenido existente en una página.
* Utilizar plantillas predefinidas para crear páginas de contenido nuevo.
* Crear, editar y gestionar recursos y colecciones.
* Mover, copiar y eliminar páginas de contenido, recursos, etc.
* Publicar (o cancelar la publicación) de páginas, recursos, etc.

Asimismo, hay tareas administrativas que le ayudan a administrar su contenido:

* Flujos de trabajo que controlan la administración de cambios, como implementar una revisión antes de la publicación.
* Proyectos que coordinan tareas individuales.

>[!NOTE]
>
>AEM también se administra desde el entorno de creación.

## Entorno de publicación {#publish-environment}

Cuando esté listo, el contenido del sitio de AEM se publica en el **entorno de publicación**. Aquí las páginas del sitio web se ponen a disposición de la audiencia objetivo de acuerdo con la apariencia de la interfaz diseñada.

Para obtener más información sobre la publicación y cancelación de publicaciones de páginas, consulte el documento [Publicación de páginas.](/help/sites-cloud/authoring/fundamentals/publishing-pages.md)

## Dispatcher {#dispatcher}

A fin de optimizar el rendimiento para los usuarios que visiten su sitio web, **[Dispatcher](/help/implementing/dispatcher/overview.md)** implementa almacenamiento en caché y equilibrio de carga.
