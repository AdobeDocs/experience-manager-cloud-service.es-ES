---
title: Conceptos de creación
description: Conceptos sobre la creación de contenido en AEM
exl-id: ee9e4952-e075-4398-b31f-d7886153efff
source-git-commit: b407765438086bb2f7fb720fb7f1dd05699cb48f
workflow-type: tm+mt
source-wordcount: '385'
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
>Su cuenta necesita los derechos de acceso adecuados para crear, editar o publicar contenido.

Según la configuración de su instancia y sus derechos de acceso personales, puede realizar muchas tareas en el contenido, incluidas (entre otras):

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

## Vista previa del contenido {#previewing-content}

AEM también ofrece un servicio de vista previa de Sites que permite a los desarrolladores y autores de contenidos previsualizar la experiencia final de un sitio web antes de que llegue al entorno de publicación y esté disponible públicamente.

Consulte [Vista previa del contenido](/help/sites-cloud/authoring/fundamentals/previewing-content.md) para obtener más información.

## Entorno de publicación {#publish-environment}

Cuando esté listo, el contenido del sitio de AEM se publica en el **entorno de publicación**. Aquí las páginas del sitio web se ponen a disposición de la audiencia objetivo de acuerdo con la apariencia de la interfaz diseñada.

Para obtener más información sobre la publicación y cancelación de publicaciones de páginas, consulte el documento [Publicación de páginas.](/help/sites-cloud/authoring/fundamentals/publishing-pages.md)

## Dispatcher {#dispatcher}

A fin de optimizar el rendimiento para los usuarios que visiten su sitio web, **[Dispatcher](/help/implementing/dispatcher/overview.md)** implementa almacenamiento en caché y equilibrio de carga.
