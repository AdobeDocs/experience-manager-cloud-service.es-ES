---
title: Conceptos de creación y publicación
description: AEM Aprenda los conceptos de creación en entornos de creación, publicación y previsualización de, usando el entorno de creación y publicación de.
exl-id: ee9e4952-e075-4398-b31f-d7886153efff
source-git-commit: bbd845079cb688dc3e62e2cf6b1a63c49a92f6b4
workflow-type: tm+mt
source-wordcount: '438'
ht-degree: 29%

---


# Conceptos de creación y publicación {#authoring-publishing}

AEM Para un autor de contenido, una instalación as a Cloud Service se puede considerar como tres niveles principales en su nivel más básico

* Nivel de Author
* Previsualizar nivel
* Publicar nivel

Estos niveles interactúan para permitirle ofrecer contenido en su sitio web para que los visitantes puedan acceder a él. El flujo de trabajo básico es:

1. Los autores de contenido crean su contenido mediante el nivel de creación.
1. Los autores de contenido ponen su contenido a disposición de los revisores para que lo previsualicen mediante el nivel de vista previa.
1. Una vez que el contenido está listo para el consumo público, los autores publican el contenido mediante el nivel de publicación.

El contenido puede ser de muchos tipos diferentes, incluidas páginas, recursos y publicaciones. La vista previa del contenido se puede omitir según el autor.

![Diagrama del creador, el editor y los distribuidores](assets/author-publish.jpg)

AEM as a Cloud Service Para obtener más información sobre la arquitectura técnica de la, consulte el documento [Introducción a la arquitectura de Adobe Experience Manager as a Cloud Service.](/help/overview/architecture.md)

{{edge-delivery-authoring}}

## Creación de contenido {#author-environment}

El entorno de creación del nivel de creación proporciona una interfaz gráfica de usuario fácil de usar para crear contenido. Requiere que el creador inicie sesión con una cuenta a la que se le hayan asignado los derechos de acceso correspondientes.

Según la configuración de su instancia y sus derechos de acceso personales, puede realizar muchas tareas con el contenido, incluidas (entre otras):

* Generar contenido nuevo o editar contenido existente en una página
* Utilizar plantillas predefinidas para crear páginas de contenido
* Crear, editar y gestionar recursos y colecciones
* Mover, copiar y eliminar páginas de contenido y recursos.
* Publicar páginas y recursos (o cancelar su publicación).

Además, hay tareas administrativas que le ayudan a administrar su contenido:

* Flujos de trabajo que controlan la administración de cambios, como implementar una revisión antes de la publicación.
* Proyectos que coordinan tareas individuales.

AEM también se administra desde el entorno de creación.

Consulte el documento [Guía rápida de introducción para la creación](/help/sites-cloud/authoring/quick-start.md) para obtener una descripción general del proceso de creación.

## Vista previa del contenido {#previewing-content}

AEM También ofrece un servicio de vista previa que permite a los desarrolladores y autores de contenido previsualizar la experiencia final de un sitio web antes de que llegue al entorno de publicación y esté disponible públicamente.

Consulte el documento [Vista previa del contenido](/help/sites-cloud/authoring/sites-console/previewing-content.md) para obtener más información.

## Entorno de publicación {#publish-environment}

Cuando esté listo, el contenido del sitio se publica en el entorno de publicación del nivel de publicación. Aquí las páginas del sitio web se ponen a disposición de la audiencia objetivo de acuerdo con la apariencia de la plantilla de contenido.

Consulte el documento [Publicación de páginas](/help/sites-cloud/authoring/sites-console/publishing-pages.md) para obtener más información sobre cómo publicar y cancelar la publicación de páginas.

## Dispatcher {#dispatcher}

Para optimizar el rendimiento de los visitantes del sitio web, **[Dispatcher](/help/implementing/dispatcher/overview.md)** implementa almacenamiento en caché y equilibrio de carga para los niveles de publicación y vista previa.
