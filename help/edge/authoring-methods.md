---
title: Elección de un método de creación
description: AEM Conozca las consideraciones importantes al decidir cómo crear su contenido en para ayudarle a tomar la mejor decisión para sus autores de contenido.
feature: Edge Delivery Services
role: Admin, Architect, Developer
source-git-commit: 15eef2d3790d1c0cf5414ca55b191de5b644fed0
workflow-type: tm+mt
source-wordcount: '659'
ht-degree: 0%

---


# Elección de un método de creación {#authoring-methods}

AEM Conozca las consideraciones importantes al decidir cómo crear su contenido en para ayudarle a tomar la mejor decisión para sus autores de contenido.

## Información general sobre consideraciones {#overview}

AEM La flexibilidad de la creación de documentos garantiza que sus necesidades de creación estén cubiertas independientemente de si elige la creación basada en documentos o la creación WYSIWYG. Tenga en cuenta los siguientes hechos al comenzar sus consideraciones.

* **Involucre siempre a los autores de contenido en la decisión.**: los autores de contenido son sus expertos y su conocimiento es vital.
* **Se pueden implementar varios métodos de creación.**: aunque el Adobe recomienda empezar con una complejidad simple y superpuesta a medida que surja la necesidad, varios métodos de creación pueden funcionar juntos en un proyecto.
* **Siempre puedes cambiar el método de creación después del hecho.**: decida lo que decida, no está bloqueado. El cambio de un método a otro es sencillo con la ayuda de las herramientas de migración automatizada de Adobe.
* **No debes decidir antes de la implementación, sino como parte de la implementación.AEM** - es un producto unificado, por lo que esta decisión importante no tiene que formar parte de las negociaciones de contratos. AEM Cuando compras, obtienes todos los que te compran a ti. Se trata más bien de una decisión durante la implementación.

El Adobe puede ayudarle a determinar qué método (o métodos) se adapta mejor a sus necesidades como parte de la implementación.

## Una talla no se adapta a todas {#one-size}

AEM Cada implementación de tiene sus propios flujos de trabajo y objetivos, y Un proyecto puede implicar un modelo de creación simple con autores de contenido responsables de sus propias publicaciones. Mientras que otro puede tener una compleja red de colaboradores y aprobaciones.

![Diferentes flujos de trabajo de creación](assets/authoring-workflows.png)

Los distintos proyectos pueden tener casos de uso diferentes (y múltiples).

![Casos de uso](assets/use-cases.png)

El Adobe entiende esto y, por lo tanto, no ofrece un enfoque único para todos. AEM Es su solución única que ofrece diferentes enfoques para la entrega de contenido, así como la creación de contenido para adaptarse de la mejor manera a sus necesidades.

Para determinar el mejor enfoque, debe tener en cuenta cuatro elementos.

1. [¿Tiene preferencias de envío de contenido?](#content-delivery)
1. [¿Tiene preferencias de creación de contenido?](#content-authoring)
1. [¿Cuál es el objetivo del proyecto?](#project-goals)
1. [¿Qué desafíos de creación afronta actualmente?](#authoring-challenges)

## Preferencias de entrega de contenido {#content-delivery}

La primera consideración debe ser cómo desea enviar el contenido. Edge Delivery Services ofrece sitios increíblemente rápidos, pero tal vez su enfoque esté en la entrega sin encabezado. El siguiente árbol de decisión puede ayudarle a considerar sus opciones.

![Árbol de decisión de entrega de contenido](assets/content-delivery-decision-tree.png)

Esto puede ayudarle a decidir si necesita lo siguiente:

* AEM [como CMS sin encabezado](/help/headless/introduction.md) con el Editor de fragmentos de contenido o el Editor universal.
* AEM Edge Delivery Services que usan la [edición basada en documentos](/help/edge/docs/authoring.md) o la [creación WYSIWYG con el editor universal.](/help/edge/wysiwyg-authoring/authoring.md)

## Preferencias de creación de contenido {#content-authoring}

La siguiente consideración debería ser cómo desea crear el contenido. El siguiente árbol de decisión puede ayudarle a considerar sus opciones.

![Árbol de decisiones de creación de contenido](assets/content-authoring-decision-tree.png)

Esto puede ayudarle a decidir si necesita lo siguiente:

* AEM Edge Delivery Services que utilizan la edición basada en documentos [s.](/help/edge/docs/authoring.md)
* [Creación de WYSIWYG con el editor universal.](/help/edge/wysiwyg-authoring/authoring.md)

## Metas de proyecto {#project-goals}

¿Qué aspecto tiene el éxito de la creación? ¿Cómo define el éxito para su proyecto?

* Tal vez necesite permitir que más personas creen contenido, pero desee evitar recibir formación sobre un nuevo conjunto de herramientas. (Piense en la creación basada en documentos).
* Tal vez necesite aumentar la cantidad de contenido que genera. (Piense en la creación basada en documentos).
* Tal vez necesite centrarse en el diseño del contenido visual, pero minimizar la necesidad de conocimientos de codificación. (Piense en la creación WYSIWYG).

Los objetivos del proyecto claramente establecidos al principio de la implementación le ayudarán a tomar una decisión bien informada sobre el método de creación.

## Retos de creación {#authoring-challenges}

Por último, considere los desafíos específicos a los que se enfrenta hoy en día para crear su contenido.

* Tal vez tenga que duplicar el trabajo con contenido creado fuera del CMS, que luego debe importarse o copiarse y pegarse. (Piense en la creación basada en documentos).
* Tal vez necesite reducir el tiempo necesario para capacitar a los autores sobre cómo utilizar un CMS. (Piense en la creación basada en documentos).
* Puede que los autores necesiten editar con frecuencia el diseño visual del contenido, lo que requiere la asistencia constante del desarrollador. (Piense en la creación WYSIWYG).
