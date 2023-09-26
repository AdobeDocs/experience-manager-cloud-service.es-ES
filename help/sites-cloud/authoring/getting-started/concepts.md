---
title: Conceptos de creación
description: AEM Aprenda los conceptos de creación en entornos de creación, publicación y previsualización de, usando el autor.
exl-id: ee9e4952-e075-4398-b31f-d7886153efff
source-git-commit: 53d4e22805774c0b994ee2bba429c19506639014
workflow-type: tm+mt
source-wordcount: '394'
ht-degree: 96%

---


# Conceptos de creación {#authoring-concepts}

Una instalación de AEM generalmente consta de al menos dos entornos:

* Autor
* Publicación

Estos entornos interactúan para permitirle ofrecer contenido en su sitio web para que los visitantes puedan acceder a él.

El entorno de creación ofrece mecanismos para crear, actualizar y revisar el contenido antes de publicarlo:

* Un creador se encarga de crear y revisar el contenido. El contenido puede ser de muchos tipos diferentes, incluidas páginas, recursos y publicaciones.
* Este, en algún momento, se publica en su sitio web.

![Diagrama del creador, el editor y los distribuidores](/help/sites-cloud/authoring/assets/author-publish.png)

En el entorno de creación, las funcionalidades de AEM están disponibles mediante la interfaz de usuario de creación de AEM. Desde el entorno de publicación se diseña todo el aspecto y funcionamiento de la interfaz de usuario.

{{edge-delivery-authoring}}

## Entorno de creación {#author-environment}

El autor trabaja en lo que se conoce como **entorno de creación**. Este entorno proporciona una interfaz fácil de usar (interfaz gráfica de usuario (GUI o IU)) para crear el contenido. Requiere que el creador inicie sesión con una cuenta a la que se le hayan asignado los derechos de acceso correspondientes.

>[!NOTE]
>
>Su cuenta necesita los derechos de acceso adecuados para crear, editar o publicar contenido.

Según la configuración de su instancia y sus derechos de acceso personales, puede realizar muchas tareas con el contenido, incluidas (entre otras):

* Generar contenido nuevo o editar contenido existente en una página
* Utilizar plantillas predefinidas para crear páginas de contenido
* Crear, editar y gestionar recursos y colecciones
* Mover, copiar y eliminar páginas de contenido y recursos.
* Publicar páginas y recursos (o cancelar su publicación).

Además, hay tareas administrativas que le ayudan a administrar su contenido:

* Flujos de trabajo que controlan la administración de cambios, como implementar una revisión antes de la publicación.
* Proyectos que coordinan tareas individuales.

>[!NOTE]
>
>AEM también se administra desde el entorno de creación.

## Vista previa del contenido {#previewing-content}

AEM ofrece un servicio de vista previa de Sites que permite a los desarrolladores y autores de contenido previsualizar la experiencia final de un sitio web antes de que llegue al entorno de publicación y esté disponible de manera pública.

Consulte [Vista previa del contenido](/help/sites-cloud/authoring/fundamentals/previewing-content.md) para obtener más información.

## Entorno de publicación {#publish-environment}

Cuando esté listo, el contenido del sitio de AEM se publica en el **entorno de publicación**. Aquí las páginas del sitio web se ponen a disposición de la audiencia objetivo de acuerdo con la apariencia de la interfaz diseñada.

Para obtener más información sobre publicaciones y cancelación de publicaciones de páginas, consulte el documento [Publicación de páginas](/help/sites-cloud/authoring/fundamentals/publishing-pages.md).

## Dispatcher {#dispatcher}

A fin de optimizar el rendimiento para los usuarios que visiten su sitio web, **[Dispatcher](/help/implementing/dispatcher/overview.md)** implementa almacenamiento en caché y equilibrio de carga.
