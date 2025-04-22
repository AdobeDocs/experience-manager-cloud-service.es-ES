---
title: Introducción al editor universal
description: El editor universal es una herramienta moderna de creación visual diseñada para permitir que su organización de marketing produzca experiencias web impactantes.
exl-id: d4fc2384-a0f5-4a6f-9572-62749786be4c
feature: Developing
role: Admin, Architect, Developer
source-git-commit: ae59b00e7e8149477a87d0b0b63493a6c2cfebe7
workflow-type: tm+mt
source-wordcount: '956'
ht-degree: 10%

---


# Introducción al editor universal {#introduction}

El editor universal es una herramienta moderna de creación visual diseñada para permitir que su organización de marketing produzca experiencias web impactantes.

## Información general {#overview}

El editor universal es un editor visual versátil que forma parte de Adobe Experience Manager Sites. Permite a los autores realizar la edición de lo que se ve es lo que se obtiene (WYSIWYG) de cualquier experiencia sin encabezado o con encabezado. Ofrece lo siguiente:

* **Edición instantánea**: los autores pueden editar contenido directamente dentro de la experiencia de vista previa, lo que elimina la necesidad de localizar y navegar a orígenes de contenido individuales.
* **Edición visual**: Mientras se realizan los cambios, los autores ven instantáneamente cómo afectan a la experiencia real del visitante, minimizando la fricción.
* **Opciones reconocibles**: las opciones claramente etiquetadas y una interfaz de usuario intuitiva permiten a los autores configurar metadatos y componer diseños con facilidad.
* **No técnico**: no se requiere experiencia especializada para hacer ediciones, mientras que las directrices de marca corporativa se aplican automáticamente, lo que facilita la escala de las tareas de contenido en toda la organización.
* **Integración y extensibilidad**: totalmente integrados con AEM, los [puntos de extensión](#extensibility) flexibles del editor universal permiten que todas las herramientas esenciales estén unificadas en una sola interfaz coherente. Desde funciones con tecnología de IA hasta extensiones personalizadas adaptadas a sus necesidades empresariales únicas, permite a los equipos optimizar los flujos de trabajo y mejorar la productividad sin esfuerzo.

En resumen:

* **Los autores se benefician** de la flexibilidad del editor universal, ya que admite la misma edición visual coherente para todas las formas de contenido de AEM.
* **Los desarrolladores se benefician** de la versatilidad del editor universal, ya que admite la desvinculación real de la implementación.

Siendo un verdadero editor como servicio y, en general, más flexible, el editor universal tiene la intención de reemplazar finalmente al [editor de páginas.](/help/sites-cloud/authoring/page-editor/introduction.md)

## Arquitecturas compatibles {#supported-architectures}

El editor universal admite las dos configuraciones principales de AEM siguientes:

1. **[Edge Delivery Services](/help/edge/overview.md)**: este es el enfoque preferido por su simplicidad, su tiempo de respuesta al valor más rápido y su rendimiento mejorado.
1. **[Implementaciones sin encabezado](/help/headless/introduction.md)**: Si tiene un proyecto sin encabezado existente o requisitos específicos para la representación disociada, el editor universal permite la edición visual de nivel empresarial sin necesidad de refactorizar todo el proyecto. Es compatible con prácticamente cualquier arquitectura (SSR, CSR), marco web (Next.js, React, Astro, etc.) y modelos de alojamiento (&quot;traiga su propia aplicación&quot;).

>[!TIP]
>
>Consulte el documento [Casos de uso del editor universal y rutas de aprendizaje](/help/implementing/universal-editor/use-cases.md) para obtener más información sobre las arquitecturas compatibles.

## Versiones de AEM compatibles {#aem-versions}

El editor universal es compatible con lo siguiente:

* AEM as a Cloud Service (versión `2023.8.13099` o superior)
* AEM 6.5 (service pack 21 o 22 más un feature pack)
   * Se admiten tanto el alojamiento local como el alojamiento AMS.

Esta documentación es útil para utilizar el Editor universal con AEM as a Cloud Service. Para usar el Editor universal con AEM 6.5, [consulte la documentación de AEM 6.5.](https://experienceleague.adobe.com/es/docs/experience-manager-65/content/implementing/developing/headless/universal-editor/introduction)

## Características {#features}

El editor universal ofrece muchas funciones que admiten una amplia gama de casos de uso para una administración de contenido eficaz.

* **[WYSIWYG](/help/sites-cloud/authoring/universal-editor/authoring.md)**: realice la edición de lo que ve es lo que obtiene de cualquier forma de contenido web, incluido texto sin formato, texto enriquecido, multimedia y metadatos.
* **[Composición](/help/sites-cloud/authoring/universal-editor/authoring.md#editing-content)**: crea, edita, reordena, anida o elimina bloques de contenido de varios tipos (títulos, botones, teasers, secciones, incrustaciones, etc.).
* **[Diseño](/help/sites-cloud/authoring/universal-editor/templates.md)**: utilice plantillas de página, aplique estilos visuales y componga diseños con bloques como columnas, carruseles y acordeones.
* **[Simulación de dispositivo](/help/sites-cloud/authoring/universal-editor/navigation.md#emulator)**: Previsualice y optimice el contenido para diferentes dispositivos de visitante mientras edita.
* **Omnicanal**: reutiliza contenido estructurado y no estructurado en varios canales.
* **[Localización](/help/sites-cloud/authoring/universal-editor/inheritance.md)**: optimice los flujos de trabajo de traducción de contenido y administre de manera eficiente la herencia de contenido localizado con Multi-Site Manager.
* **Coherencia**: Asegure el cumplimiento de las directrices de marca y mantenga la uniformidad en todo el contenido.
* **Seguridad**: [Aplique control de acceso](/help/implementing/universal-editor/authentication.md), proteja la integridad del contenido y realice un seguimiento de los cambios con [control de versiones robusto.](/help/sites-cloud/authoring/sites-console/page-versions.md)
* **[Publicación](/help/sites-cloud/authoring/universal-editor/publishing.md)**: integra los flujos de trabajo de revisión, aprobación y publicación directamente en el editor.
* **Unificado**: se integra completamente con herramientas de AEM como la consola de [Sites,](/help/sites-cloud/authoring/sites-console/introduction.md) [Editor de fragmentos de contenido](/help/sites-cloud/administering/content-fragments/overview.md) y muchas más, lo que proporciona una experiencia de creación coherente.

## Extensibilidad {#extensibility}

El editor universal no solo es muy capaz de usar de forma predeterminada, sino que también ofrece una serie de posibilidades de extensión.

* **Las extensiones** son numerosas y están listas para usarse para admitir requisitos como flujos de trabajo, generar variaciones y habilitar la experimentación, entre otros.
* **Una interfaz de usuario ampliable** le permite crear sus propias extensiones utilizando los mismos marcos subyacentes que aprovechan las extensiones listas para su uso, lo que permite la máxima flexibilidad para adaptarse a las necesidades de su proyecto.
* Los **puntos de extensión**, como bloques, tipos de datos personalizados y eventos, permiten una integración perfecta de los requisitos empresariales personalizados más allá de la interfaz de usuario.

>[!TIP]
>
>Para obtener más información sobre la extensibilidad del editor universal, consulte el documento [Ampliación del editor universal.](/help/implementing/universal-editor/extending.md)

## Editor universal y editor de fragmentos de contenido {#universal-editor-content-fragment-editor}

A primera vista, podría parecer que el Editor universal y el Editor de fragmentos de contenido proporcionan funcionalidades de edición similares. Sin embargo, estos editores ofrecen capacidades muy diferentes y ejecutan diferentes trabajos del profesional del marketing.

### Editor de fragmentos de contenido {#content-fragment-editor}

Un profesional del marketing quiere crear contenido sin tener que preocuparse por su diseño, de modo que se pueda reutilizar en numerosos contextos de la experiencia.

* El trabajo subyacente que se debe llevar a cabo es escalar la estrategia de contenido.

### Editor universal {#universal-editor}

Un profesional del marketing quiere crear contenido que esté adaptado al diseño de un contexto determinado para ofrecer una experiencia excepcional.

* El trabajo subyacente que hay que realizar es conectar de manera convincente con los lectores.

## Limitaciones {#limitations}

A medida que explore el editor universal y avance en la implementación de él en sus propios proyectos, tenga en cuenta las siguientes limitaciones.

* No más de 25 recursos de AEM (fragmentos de contenido, páginas, fragmentos de experiencias, Assets, etc.) deben ser referencias como instrumentación en una sola página.
* AEM as a Cloud Service y [AEM 6.5](https://experienceleague.adobe.com/es/docs/experience-manager-65/content/implementing/developing/headless/universal-editor/introduction) son los únicos backends de AEM compatibles.
* Se requiere la versión `2023.8.13099` o superior para AEM as a Cloud Service.
* Los autores de contenido deben tener sus propias cuentas de Experience Cloud individuales.
* Como parte de AEM, el editor universal [ admite los mismos exploradores de escritorio que AEM.](/help/overview/supported-platforms.md)
   * Las versiones móviles de estos exploradores no son compatibles.

{{ip-allow-lists-ue}}

## Siguientes pasos {#next-steps}

Consulte el documento [Casos de uso y rutas de aprendizaje del editor universal](/help/implementing/universal-editor/use-cases.md) para obtener más información sobre casos de uso comunes del editor universal y descubrir los recursos de documentación adecuados para ayudarle en su proyecto.
