---
title: Obtenga información sobre el contenido sin encabezado y cómo localizar en AEM
description: Aprenda conceptos sin objetivos, cómo se asignan a AEM, y la teoría de AEM localización.
source-git-commit: 22ca7c01bfddb407c119de7d9a4d105941772664
workflow-type: tm+mt
source-wordcount: '655'
ht-degree: 0%

---

# Obtenga información sobre el contenido sin encabezado y cómo localizar en AEM {#learn-about}

Aprenda conceptos sin objetivos, cómo se asignan a AEM, y la teoría de AEM localización.

## Objetivo {#objective}

Este documento le ayuda a comprender la entrega de contenido sin encabezado, cómo AEM admite sin encabezado y cómo se puede localizar dicho contenido. Después de leer, debe:

* Comprender los conceptos básicos de la entrega de contenido sin encabezado.
* Familiarícese con cómo AEM admite la localización y la eliminación de encabezados.

## Entrega de contenido de pila completa {#full-stack}

Desde el surgimiento de sistemas de administración de contenido (CMSes) a gran escala y fáciles de usar, las organizaciones los han aprovechado como una ubicación central para administrar mensajes, marcas y comunicaciones. El uso del CMS como punto central para la administración de experiencias mejoró la eficiencia al eliminar la necesidad de duplicar tareas en sistemas dispares.

![El clásico CMS de pila completa](/help/journey-headless/developer/assets/full-stack.png)

En un CMS de pila completa, toda la funcionalidad para manipular contenido está en el CMS. Las características del sistema componen diferentes componentes de la pila de CMS. La solución de pila completa tiene muchas ventajas.

* Hay un sistema para mantener.
* El contenido se administra de forma centralizada.
* Todos los servicios del sistema están integrados.
* La creación de contenido es perfecta.

Por lo tanto, si se necesita añadir un nuevo canal o admitir nuevos tipos de experiencias, se pueden insertar uno o más componentes nuevos en la pila y solo hay un lugar donde realizar cambios.

![Adición de un nuevo canal a la pila](/help/journey-headless/developer/assets/adding-channel.png)

La complejidad de las dependencias dentro de la pila se hace evidente rápidamente, ya que es necesario ajustar otros elementos de la pila para adaptarse a los cambios.

## La cabeza sin cabeza {#the-head}

El jefe de cualquier sistema es generalmente el procesador de salida de ese sistema, normalmente en forma de GUI u otra salida gráfica.

Cuando hablamos de un CMS sin objetivos, el CMS administra el contenido y continúa entregándolo a los consumidores. Sin embargo, al entregar únicamente el **contenido** de forma estandarizada, un CMS sin encabezado omite la renderización de salida final, dejando la **presentación** del contenido en el servicio consumidor.

![CMS sin encabezado](/help/journey-headless/developer/assets/headless-cms.png)

Los servicios que consumen, ya sean experiencias de AR, una tienda web, experiencias móviles, aplicaciones web progresivas (PWA), etc., reciben contenido del CMS sin periféricos y proporcionan su propia renderización. Se ocupan de proporcionar sus propias cabezas para su contenido.

Omitir la cabeza simplifica el CMS al eliminar la complejidad. Al hacerlo, también se traslada la responsabilidad de procesar el contenido a los servicios que realmente necesitan el contenido y que a menudo son más adecuados para dicha renderización.

## Localización de contenido sin encabezado en AEM {#localizing-in-aem}

Además de ofrecer herramientas sólidas para crear, administrar y entregar páginas web tradicionales de forma totalmente apilada, AEM también ofrece la capacidad de crear selecciones de contenido independientes y servirlas sin problemas.

La potencia de AEM le permite entregar contenido sin periféricos, en pilas completas o en ambos modelos al mismo tiempo. Para el especialista en localización, se puede aplicar el mismo conjunto de herramientas de localización a ambos tipos de contenido, lo que le ofrece un enfoque unificado para traducir el contenido.

## Siguientes pasos {#what-is-next}

¡Gracias por empezar con su recorrido de localización AEM sin periféricos! Ahora que lee este documento, debe:

* Comprender los conceptos básicos de la entrega de contenido sin encabezado.
* Familiarícese con cómo AEM admite la localización y la eliminación de encabezados.

Aproveche este conocimiento y continúe con su recorrido de localización AEM sin encabezado revisando el documento [Introducción a AEM localización sin encabezado](getting-started.md), donde tendrá una visión general de cómo AEM administra el contenido sin encabezado y conozca sus herramientas de localización.

## Recursos adicionales {#additional-resources}

Aunque se recomienda pasar a la siguiente parte del recorrido de localización sin encabezado revisando el documento [Introducción a AEM localización sin encabezado,](getting-started.md) los siguientes son algunos recursos opcionales adicionales que profundizan en algunos conceptos mencionados en este documento, pero no es necesario que continúen en el recorrido sin encabezado.

* [MSM y traducción](/help/sites-cloud/administering/msm-and-translation.md) : detalles de AEM Multi-Site Manager y cómo funciona con sus herramientas de traducción
