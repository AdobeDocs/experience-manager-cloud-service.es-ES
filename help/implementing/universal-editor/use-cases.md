---
title: Casos de uso y rutas de aprendizaje del editor universal
description: Conozca los principales casos de uso del editor universal y cómo obtener más información sobre su uso e implementarlo en sus propios proyectos.
exl-id: 398ad0e2-c299-4c49-9784-05c84c67bec2
feature: Developing
role: Admin, Developer
source-git-commit: 9adf2bc4f9f25ee7fc0a39b0f1a3ae9e45fce7d2
workflow-type: tm+mt
source-wordcount: '882'
ht-degree: 100%

---

# Casos de uso y rutas de aprendizaje del editor universal {#use-cases-learning-paths}

Conozca los principales casos de uso del editor universal y cómo obtener más información sobre su uso e implementarlo en sus propios proyectos.

## Información general {#overview}

El editor universal es un editor visual versátil que forma parte de Adobe Experience Manager Sites. Permite a los autores realizar la edición de lo que se ve es lo que se obtiene (WYSIWYG) de cualquier experiencia sin encabezado o con encabezado.

Este documento explica en detalle estos dos casos de uso y le muestra cómo puede obtener más información sobre ellos para implementar el editor universal en su propio proyecto.

>[!TIP]
>
>Si aún no lo ha hecho, revise el documento [Introducción al editor universal](/help/implementing/universal-editor/introduction.md) para conocer información general completa y el valor del editor universal.

## Casos de uso {#use-cases}

El editor universal presenta un editor visual cómodo e intuitivo a los autores de contenido, con independencia del tipo de contenido que creen. Los dos casos de uso principales son los siguientes:

* [Creación WYSIWYG](#wysiwyg-authoring): use la consola de AEM Sites para administrar el contenido y crear páginas en AEM mediante el editor universal
* [Creación headless](#headless-authoring): cree contenido en su propia aplicación headless personalizada mediante el editor universal.

### Creación WYSIWYG {#wysiwyg-authoring}

Si ya conoce AEM, puede utilizar la consola de Sites para crear y administrar sus páginas y, a continuación, editarlas con el editor universal.

De este modo, puede beneficiarse de las herramientas disponibles en la consola de Sites, como la administración de páginas (copiar, pegar, mover) y los flujos de trabajo, pero también del editor universal moderno.

Si este es su caso de uso, como próximo paso inmediato, consulte los siguientes documentos para obtener información general completa de cómo ponerse en marcha con el editor universal en AEM.

1. [Guía de introducción para desarrolladores para la creación WYSIWYG con Edge Delivery Services](https://www.aem.live/developer/ue-tutorial): empiece con su primer proyecto del editor universal en AEM
1. [Creación de bloques instrumentados para su uso con el editor universal](https://www.aem.live/developer/universal-editor-blocks): aprenda a instrumentar bloques para poder editar su contenido en el editor universal
1. [Modelado de contenido para la creación WYSIWYG con proyectos de Edge Delivery Services](https://www.aem.live/developer/component-model-definitions): conozca los detalles de cómo se estructuran los bloques para modelar de forma eficaz el contenido y utilizarlo con el editor universal.

Una vez que haya leído estos documentos, puede volver a esta página para conocer el caso de uso de la creación headless y cómo funciona el editor universal en general.

### Creación headless {#headless-authoring}

Si ya tiene una aplicación headless, puede utilizar el editor universal para crear contenido para esta y mantener su contenido como fragmentos de contenido en AEM. El único requisito es que la aplicación esté instrumentada para permitir el uso del editor universal.

Si este es su caso de uso, como próximo paso inmediato, consulte el siguiente documento para ver un ejemplo de una aplicación headless instrumentada para emplear el editor universal.

* [Aplicación de muestra SecurBank para el editor universal](/help/implementing/universal-editor/securbank.md)

Una vez que haya leído ese documento, puede volver a esta página para conocer el caso de uso de la creación WYSIWYG y cómo funciona el editor universal en general.

{{ue-headless-auth}}

## Cómo funciona el editor universal {#how-ue-works}

El poder del editor universal es su capacidad para crear cualquier contenido in situ, lo que proporciona al autor de contenido una interfaz de usuario completamente intuitiva y unificada, con independencia del contenido.

El editor universal funciona de la siguiente manera.

1. Un desarrollador instrumenta la aplicación o página para utilizar el editor universal. Esta instrumentación indica al editor qué contenido se puede editar y cómo conservarlo.
   * Si sigue la [Guía de introducción para desarrolladores de creación WYSIWYG con Edge Delivery Services](https://www.aem.live/developer/ue-tutorial), sus páginas se instrumentarán de forma automática.
   * Para la creación headless, la aplicación se puede instrumentar con facilidad.
1. El autor del contenido carga el editor universal, que a su vez carga la página para editarla. Al instrumentarse, sabe qué contenido es editable y cómo se representará y se mantendrá.
1. El autor del contenido edita el contenido de la página en una interfaz WYSIWYG intuitiva y lo edita in situ.
1. El editor universal conserva los cambios de forma automática en la fuente de datos.

Si desea obtener más información acerca de la arquitectura del editor universal, consulte el documento [Arquitectura del editor universal](/help/implementing/universal-editor/architecture.md).

## Conceptos del editor universal {#concepts}

Para que el editor universal pueda editar una página o aplicación, debe instrumentarse correctamente.

* [Atributos y tipos](/help/implementing/universal-editor/attributes-types.md): para que el editor universal pueda editar una aplicación, debe instrumentarse de manera correcta. Esto incluye introducir los metadatos adecuados para que el editor pueda modificar el contenido de la aplicación.
* [Definiciones de modelo, campos y tipos de componente](/help/implementing/universal-editor/field-types.md): una vez que los metadatos estén presentes para habilitar la edición de un componente, defina qué campos y tipos de componente pueden manipular en el panel de propiedades del editor.
* [Eventos del editor universal](/help/implementing/universal-editor/events-universal-editor.md): puede personalizar aún más la aplicación si mejora la experiencia de edición en ella consumiendo eventos que el editor universal emite en el contenido o en las interacciones de la IU.

El editor universal también se puede adaptar a las necesidades de su proyecto.

* [Personalización del editor universal](/help/implementing/universal-editor/customizing.md): la experiencia del editor universal se puede adaptar filtrando varios de sus aspectos o ampliando su funcionalidad.
* [Ampliación del editor universal](/help/implementing/universal-editor/extending.md): la IU del editor universal se puede ampliar para expandir sus capacidades y así satisfacer las necesidades de su proyecto.
