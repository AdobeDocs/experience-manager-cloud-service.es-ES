---
title: Crear un sitio
description: Aprenda a utilizar AEM para crear un sitio mediante plantillas de sitio para definir el estilo y la estructura del sitio.
feature: Administering
role: Admin
exl-id: 9c71c167-2934-4210-abd9-ab085b36593b
solution: Experience Manager Sites
source-git-commit: 4d45e7ef626ad0b46f5323263cca791b14f9732f
workflow-type: tm+mt
source-wordcount: '726'
ht-degree: 55%

---


# Crear un sitio {#creating-site}

Aprenda a utilizar AEM para crear un sitio mediante plantillas de sitio para definir el estilo y la estructura del sitio.

## Información general {#overview}

Para que los autores de contenido puedan crear páginas con contenido, primero debe crearse el sitio. Esto generalmente lo realiza un administrador de AEM que define la estructura inicial del sitio. El uso de plantillas de sitio hace que la creación del sitio sea rápida y flexible para los usuarios que no son desarrolladores.

## Planificación de la estructura del sitio {#structure}

Tómese tiempo para tener en cuenta el propósito de su sitio y el contenido planificado con mucha antelación. Esto impulsará la forma en que se diseña la estructura del sitio. Una buena estructura del sitio facilita la exploración y la detección de contenido a los visitantes del sitio y admite diversas características de AEM, como [administración y traducción multisitio.](/help/sites-cloud/administering/msm-and-translation.md)

## Plantillas de sitios {#site-templates}

Debido a que la estructura del sitio es tan importante para el éxito de un sitio, resulta conveniente tener estructuras predefinidas disponibles para implementar rápidamente un nuevo sitio en función de un conjunto de estándares existentes. Las plantillas de sitio son una forma de combinar el contenido básico del sitio en un paquete conveniente y reutilizable.

Las plantillas del sitio suelen contener contenido y estructura base del sitio, así como información de estilo, para comenzar con uno nuevo rápidamente. Las plantillas son eficaces, ya que se pueden reutilizar y personalizar. Y como puede tener varias plantillas disponibles en la instalación de AEM, tiene la flexibilidad de crear diferentes sitios para satisfacer diversas necesidades comerciales.

>[!TIP]
>
>Para obtener más información sobre las plantillas de sitio, consulte el documento [Plantillas de sitio.](site-templates.md)

>[!NOTE]
>
>La plantilla del sitio no debe confundirse con [plantillas de página.](/help/sites-cloud/authoring/page-editor/templates.md) Las plantillas de sitio definen la estructura general de un sitio. Una plantilla de página define la estructura y el contenido inicial de una página individual.

### Plantillas de sitio proporcionadas por Adobe {#adobe-templates}

{{adobe-templates}}

## Crear un sitio {#create-site}

El uso de una plantilla para crear un sitio es sencillo.

1. Inicie sesión en el entorno de creación de AEM y vaya a la consola Sites.

   * `https://<your-author-environment>.adobeaemcloud.com/sites.html/content`

1. Seleccione **Crear** en la parte superior derecha de la pantalla y en el menú desplegable, seleccione **Sitio a partir de una plantilla**.

   ![Creación de un sitio a partir de una plantilla](../assets/create-site-from-template.png)

1. En el asistente Crear sitio, seleccione una plantilla existente en el panel izquierdo o en **Importar** en la parte superior de la columna izquierda para importar una nueva plantilla.

   ![Asistente de creación de sitios](../assets/site-creation-wizard.png)

   1. Si elige importar, en el explorador de archivos, busque la plantilla que desee usar y seleccione **Cargar**.

   1. Una vez cargado, aparece en la lista de plantillas disponibles.

1. Al seleccionar una plantilla, se muestra información sobre la plantilla en la columna derecha. Con la plantilla deseada seleccionada, seleccione **Siguiente**.

   ![Seleccionar una plantilla](../assets/select-site-template.png)

1. Proporcione un título para el sitio. Se puede proporcionar un nombre de sitio o se genera a partir del título si se omite.

   * El título del sitio aparece en la barra de título de los exploradores.
   * El nombre del sitio forma parte de la dirección URL.
   * El nombre del sitio debe cumplir con las [convenciones de asignación de nombres de páginas de AEM](/help/sites-cloud/authoring/sites-console/organizing-pages.md#page-name-restrictions-and-best-practices).

1. Proporcione los detalles adicionales del sitio que requiera la plantilla del sitio.

   * Diferentes plantillas pueden requerir detalles adicionales.
   * Por ejemplo, las plantillas para [proyectos de Edge Delivery Services](https://www.aem.live/developer/ue-tutorial) requieren el repositorio GitHub de su proyecto.

1. Seleccione **Crear** y el sitio se creará a partir de la plantilla del sitio.

   ![Detalles del nuevo sitio](../assets/create-site-details.png)

1. En el cuadro de diálogo de confirmación que aparece, seleccione **Listo**.

   ![Cuadro de diálogo de éxito](../assets/success.png)

1. En la consola Sitios, el nuevo sitio es visible y se puede navegar para explorar su estructura básica según se define en la plantilla.

   ![Nueva estructura del sitio](../assets/new-site.png)

¡Los autores de contenido ahora pueden empezar a crear!

## Personalización del sitio {#site-customization}

Las plantillas son útiles para configurar rápidamente la estructura y el estilo básicos de un sitio. Sin embargo, la mayoría de los proyectos requieren un estilo y una personalización adicionales. Las plantillas de sitio ayudan a desacoplar el estilo del sitio, de modo que los desarrolladores de front-end no necesitan conocer AEM para aplicar estilo al sitio y pueden
trabaje de forma independiente y paralela a los creadores de contenido. Según el tipo de proyecto, esto puede adoptar dos formas.

* Para proyectos con creación de páginas de AEM con el editor universal y entrega mediante [entrega perimetral](/help/edge/overview.md), todo el estilo se realiza en el proyecto de GitHub.
   * Consulte el documento [Introducción: tutorial para desarrolladores de Universal Editor](https://www.aem.live/developer/ue-tutorial) para obtener más información.
* En el caso de los proyectos con creación y entrega de páginas tradicionales de AEM mediante [publicación de entrega](/help/sites-cloud/authoring/author-publish.md), el administrador de AEM simplemente descarga el tema del sitio y lo proporciona al desarrollador front-end que lo personaliza con sus herramientas favoritas y luego confirma los cambios en el repositorio de código de AEM, que luego se implementa.
   * Consulte el documento [Recorrido de creación rápida de sitios de AEM](/help/journey-sites/quick-site/overview.md) para obtener más información.
