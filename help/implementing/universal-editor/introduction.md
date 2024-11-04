---
title: Introducción al editor universal
description: Descubra cómo el editor universal permite la edición de lo que se ve es lo que se obtiene (WYSIWYG) de cualquier experiencia sin encabezado y con encabezado. Descubra cómo puede ayudar a los autores de contenido a ofrecer contenidos excepcionales y mayor velocidad, y una experiencia de última generación a los desarrolladores.
exl-id: d4fc2384-a0f5-4a6f-9572-62749786be4c
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 54d1cdec9b30c08f28d4c9b2fbd97446f3ff05b3
workflow-type: tm+mt
source-wordcount: '1001'
ht-degree: 51%

---


# Introducción al editor universal {#introduction}

El editor universal es un editor visual versátil que forma parte de Adobe Experience Manager Sites. Permite a los autores realizar la edición de lo que se ve es lo que se obtiene (WYSIWYG) de cualquier experiencia sin encabezado o con encabezado. Comprenda cómo puede ayudar a los autores de contenido a ofrecer experiencias excepcionales y cómo ofrece una libertad sin igual para los desarrolladores.

## Fondo {#background}

El editor universal proporciona una experiencia de creación en contexto eficaz e intuitiva que requiere una formación mínima. Con él, los autores pueden administrar su contenido directamente en el contexto de la experiencia web, exactamente como se mostrará a los visitantes. Al ser un editor real como servicio y, en general, más flexible, pretende reemplazar finalmente al Editor de páginas.

AEM Los autores se benefician de la flexibilidad del editor universal, ya que admite la misma edición visual coherente para todas las formas de contenido: la edición in situ y la composición del diseño son posibles del mismo modo tanto para los fragmentos de contenido como para los componentes de página. Las dos formas de contenido se pueden editar incluso cuando se muestran una al lado de la otra en una experiencia web, sin que los autores tengan que cambiar de contexto. AEM Esta es una tremenda mejora en comparación con editores anteriores en los que solo se admitía un tipo de contenido en el que se mostraba un solo tipo de contenido.

Los desarrolladores se benefician de la versatilidad del editor universal, ya que también admite el desacoplamiento real de la implementación. Permite a los desarrolladores utilizar prácticamente cualquier marco o arquitectura de su elección, sin imponer restricciones de SDK o tecnología. Esta flexibilidad incluso facilita la instrumentación de aplicaciones web existentes para el editor universal sin tener que volver a diseñarlas.

## Verdaderamente universal {#universal}

El editor universal puede instrumentarse para cualquier implementación, contenido y aspecto del contenido.

![Qué lo hace universal](assets/universal.png)

### Cualquier implementación {#any-implementation}

Dado que las experiencias se pueden crear de muchas formas, cualquier implementación puede utilizar el editor universal para que los autores puedan editar en contexto.

Los usuarios suelen pensar que una implementación sin encabezado limita a los autores a editar todo el contenido en una IU basada en formularios, pero este no es el caso con el editor universal

Los requisitos de una implementación para utilizar el editor universal son muy sencillos y compatibles con lo siguiente:

* **Cualquier arquitectura**: procesamiento del lado del servidor, procesamiento del lado del borde, procesamiento del lado del cliente, etc.
* AEM **Cualquier módulo** - Vanilla o cualquier módulo de terceros como React, Next.js, Angular, etc.
* **Cualquier alojamiento**: se puede alojar localmente en AEM o en un dominio remoto.

### Cualquier contenido {#any-content}

Un autor de contenido debe tener la misma experiencia de edición potente que ofrecía anteriormente el editor de páginas de AEM. Sin embargo, el dditor universal permite a los autores de contenido editar **cualquier** contenido visual y en contexto. Admite lo siguiente:

* **Estructuras de página de AEM**: `cq:Components` anidados de `cq:Pages`, incluidos los fragmentos de experiencias.
* **Fragmentos de contenido de AEM**: edite el contenido de los fragmentos de contenido tal y como aparecen en el contexto de la experiencia.
* **Documentos**: la prueba de conceptos ha demostrado que también los documentos de Word, Excel, Google Docs o Markdown pueden editarse de la misma manera (esto está en progreso).

### Cualquier aspecto {#any-aspect}

Para un autor de contenidos, estos no se limitan a la información que contienen, sino a cómo se presentan y reciben. El contenido viene con metadatos adicionales y reglas de instrumentación que el editor universal puede comprender y editar, como por ejemplo:

* **Aplicación de diseño y estilo**: al utilizar un sistema de estilos, el profesional de marketing y el autor de contenido pueden aplicar diferentes estilos al contenido y crear diferentes diseños para el contenido, como columnas, carruseles, pestañas, acordeones, etc.

## Valor {#value}

Al desvincular la experiencia de edición de contenido de cualquier sistema de envío en particular, el editor se vuelve universal y flexible, lo que permite al autor ofrecer experiencias excepcionales, aumentar la velocidad y proporcionar una experiencia de desarrollo de última generación.

![El valor del editor universal](assets/value.png)

* **Ofrecer experiencias excepcionales**: para que los profesionales creen una experiencia atractiva para los visitantes, el editor universal les permite generar y editar el contenido en el contexto de la vista previa. Esto les permite crear contenido que se ajuste al diseño de la experiencia y que constituya un recorrido significativo para los visitantes.
* **Aumentar la velocidad del contenido**: para simplificar el flujo de trabajo de administración de los profesionales, el editor universal permite editar contenido en la vista previa para guiarlos, mostrando solo las opciones que son relevantes para ese contexto. Con ello, el flujo de trabajo es independiente de las fuentes de contenido.
* **Experiencia de desarrollo de última generación**: para adaptarse al heterogéneo panorama de aplicaciones del mundo real, el editor universal está totalmente separado y es independiente de la tecnología, lo que permite a los desarrolladores utilizar su pila tecnológica preferida para implementar la experiencia.

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

* AEM No más de 25 recursos de (fragmentos de contenido, páginas, fragmentos de experiencias, Assets, etc.) deben ser referencias como instrumentación en una sola página.
* AEM as a Cloud Service AEM es el único backend compatible con la interfaz de usuario de.
   * [AEM La compatibilidad con la versión.5 está disponible como parte de un programa de adopción anticipada.](/help/release-notes/universal-editor/current.md#early-adoption)
* Se requiere la versión de AEM as a Cloud Service `2023.8.13099` o superior.
* Los autores de contenido deben tener sus propias cuentas de Experience Cloud individuales.
* AEM AEM Como parte de la, el editor universal admite los mismos exploradores de escritorio que el editor de archivos de escritorio de la versión de.
   * Las versiones móviles de estos exploradores no son compatibles.

{{ue-ip-allow-lists}}

## Siguientes pasos {#next-steps}

Consulte el documento [Casos de uso y rutas de aprendizaje del editor universal](/help/implementing/universal-editor/use-cases.md) para obtener más información sobre casos de uso comunes del editor universal y descubrir los recursos de documentación adecuados para ayudarle en su proyecto.
