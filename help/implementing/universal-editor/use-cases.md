---
title: Casos de uso y rutas de aprendizaje del editor universal
description: Conozca los principales casos de uso del editor universal y cómo obtener más información sobre su uso y cómo implementarlo en sus propios proyectos.
exl-id: 398ad0e2-c299-4c49-9784-05c84c67bec2
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 7ad9a959592f1e8cebbcad9a67d280d5b2119866
workflow-type: tm+mt
source-wordcount: '863'
ht-degree: 0%

---

# Casos de uso y rutas de aprendizaje del editor universal {#use-cases-learning-paths}

Conozca los principales casos de uso del editor universal y cómo obtener más información sobre su uso y cómo implementarlo en sus propios proyectos.

## Información general {#overview}

El editor universal es un editor visual versátil que forma parte de Adobe Experience Manager Sites. Permite a los autores realizar la edición de lo que se ve es lo que se obtiene (WYSIWYG) de cualquier experiencia sin encabezado o con encabezado.

Este documento explica en detalle estos dos casos de uso y le muestra cómo puede obtener más información sobre ellos para implementar el Editor universal en su propio proyecto.

>[!TIP]
>
>Si aún no lo ha hecho, revise el documento [Introducción al editor universal](/help/implementing/universal-editor/introduction.md) para obtener una descripción general completa y el valor del editor universal.

## Casos de uso {#use-cases}

El editor universal presenta un editor visual cómodo e intuitivo a los autores de contenido, independientemente del tipo de contenido que creen. Los dos casos de uso principales son:

* [Creación WYSIWYG](#wysiwyg-authoring): use la consola de AEM Sites AEM para administrar el contenido y las páginas de creación dentro de las páginas de creación mediante el Editor universal (Universal Editor).
* [Creación sin encabezado](#headless-authoring): Cree contenido en su propia aplicación sin encabezado personalizada mediante el Editor universal.

### Creación WYSIWYG {#wysiwyg-authoring}

AEM Si ya está familiarizado con la administración de páginas, puede utilizar la consola Sitios para crear y administrar sus páginas y, a continuación, editarlas con el Editor universal.

De este modo, puede beneficiarse de las herramientas disponibles en la consola Sites, como la administración de páginas (copiar, pegar, mover) y los flujos de trabajo, pero también beneficiarse del editor universal moderno.

AEM Si este es su caso de uso, como paso siguiente inmediato, consulte los siguientes documentos para obtener una descripción general completa de cómo ponerse en marcha con el editor universal en la documentación de la aplicación de la.

1. [Guía de introducción para desarrolladores para la creación de WYSIWYG con Edge Delivery Services AEM](/help/edge/wysiwyg-authoring/edge-dev-getting-started.md): Empiece con su primer proyecto de editor universal en la creación de archivos de tipo
1. [Creación de bloques instrumentados para su uso con el editor universal](/help/edge/wysiwyg-authoring/create-block.md): aprenda a instrumentar bloques para poder editar su contenido en el editor universal
1. [Modelado de contenido para la creación WYSIWYG con proyectos de Edge Delivery Services](/help/edge/wysiwyg-authoring/content-modeling.md): aprenda los detalles de cómo los bloques están estructurados para modelar de forma eficaz su contenido para utilizarlo con el editor universal.

Una vez que haya leído esos documentos, puede volver a esta página para conocer el caso de uso de la creación sin encabezado y cómo funciona el Editor universal en general.

### Creación sin encabezado {#headless-authoring}

AEM Si ya tiene una aplicación sin encabezado, puede utilizar el Editor universal para crear contenido para la aplicación y mantener su contenido como fragmentos de contenido en la aplicación. El único requisito es que la aplicación esté instrumentada para permitir el uso del editor universal.

Si este es su caso de uso, como paso siguiente inmediato, consulte el siguiente documento para ver un ejemplo de una aplicación sin encabezado instrumentada para utilizar el Editor universal.

* [Aplicación de ejemplo de SecurBank para el editor universal](/help/implementing/universal-editor/securbank.md)

Una vez que haya leído ese documento, puede volver a esta página para conocer el caso de uso de la creación WYSIWYG y cómo funciona el Editor universal en general.

## Cómo funciona el editor universal {#how-ue-works}

El poder del editor universal es su capacidad para crear cualquier contenido in situ, lo que proporciona al autor de contenido una interfaz de usuario completamente intuitiva y unificada independientemente del contenido.

El editor universal funciona de la siguiente manera.

1. Un desarrollador instrumenta la aplicación o página para utilizar el Editor universal. Esta instrumentación indica al editor qué contenido se puede editar y cómo conservarlo.
   * Para la creación WYSIWYG, las páginas creadas con la plantilla de plantillas se instrumentan automáticamente.
   * Para la creación sin encabezado, la aplicación se puede instrumentar fácilmente.
1. El autor del contenido carga el editor universal, que a su vez carga la página para editarla. Como está instrumentado, sabe qué contenido es editable y cómo se representará y persistirá.
1. El autor del contenido edita el contenido de la página en una interfaz WYSIWYG intuitiva y realiza la edición in situ.
1. AEM El editor universal conserva los cambios automáticamente y vuelve a los valores de la página de inicio de sesión.

Si desea obtener más información acerca de la arquitectura del editor universal, consulte el documento [Arquitectura del editor universal.](/help/implementing/universal-editor/architecture.md)

## Conceptos del editor universal {#concepts}

Para que el editor universal pueda editar una página o aplicación, debe estar instrumentada correctamente. Una vez instrumentada, se puede adaptar a las necesidades de su proyecto.

* [Atributos y tipos](/help/implementing/universal-editor/attributes-types.md): para que el editor universal pueda editar una aplicación o página, debe estar instrumentada correctamente. Esto incluye incluir los metadatos adecuados para que el editor pueda editar el contenido de la aplicación.
* [Definiciones de modelo, campos y tipos de componente](/help/implementing/universal-editor/field-types.md): una vez que los metadatos están presentes para permitir la edición de un componente, debe definir qué campos y tipos de componente pueden manipular en el carril de propiedades del editor. Para ello, cree un modelo y vincúlelo a él desde el componente.
* [Personalización de la experiencia de creación del editor universal](/help/implementing/universal-editor/customizing.md): una vez que la aplicación o la página estén completamente instrumentadas, la experiencia del editor universal se puede adaptar aún más filtrando los componentes disponibles o ampliando la funcionalidad del editor.
* [Eventos de editor universal](/help/implementing/universal-editor/events.md): puede personalizar aún más la aplicación si reacciona a los eventos estándar que envía el editor universal cuando cambia el contenido y la interfaz de usuario.
