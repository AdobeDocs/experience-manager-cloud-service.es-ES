---
title: Encabezado y sin cabeza en AEM
description: AEM proyectos pueden implementarse en un modelo audaz y sin cabeza, pero la elección no es binaria. AEM oferta la flexibilidad para aprovechar las ventajas de ambos modelos en un proyecto.
translation-type: tm+mt
source-git-commit: 772717b7ad3baa17a58e251c128663035eb89931
workflow-type: tm+mt
source-wordcount: '1009'
ht-degree: 0%

---


# Encabezado y sin cabeza en AEM {#headful-headless}

Los proyectos de Adobe Experience Manager se pueden implementar tanto en modelos caprichosos como sin cabeza, pero la elección no es binaria. AEM oferta la flexibilidad para aprovechar las ventajas de ambos modelos en un proyecto. Este documento proporciona una visión general de los diferentes modelos y describe los niveles de integración de SPA.

## Información general {#overview}

AEM oferta poderosas herramientas para administrar la creación de contenido y su envío en una sola plataforma. Se trata de un modelo tradicional de gestor de contenido &quot;lleno de cabeza&quot;, en el que los autores y desarrolladores de contenido trabajan en la misma plataforma para ofrecer las experiencias a los consumidores de contenido.

AEM también se puede utilizar para administrar simplemente el contenido, permitiendo que otra plataforma administre la presentación y el envío del contenido. Este es el modelo &quot;sin cabeza&quot; de gestor de contenido, donde los autores y desarrolladores de contenido trabajan en diferentes plataformas para ofrecer experiencia a los consumidores de contenido.

Pero no tiene por qué ser una elección binaria. AEM ofertas de flexibilidad sin precedentes, permitiéndole aprovechar las ventajas de ambos modelos para su proyecto.

![Modelos de implementación de AEM](headless/assets/aem-implementation-models.png)

En un modelo de pila completa o con encabezado, el contenido se administra en el repositorio de AEM y en los componentes de AEM basados en Java, HTL, etc. se utilizan para representar el contenido de la experiencia del usuario. En este modelo, crear el contenido, diseñarlo, presentarlo y ofrecerlo todo ocurre en AEM.

En un modelo sin encabezado, el contenido se administra en el repositorio de AEM, pero se envía mediante API como REST y GraphQL a otro sistema para representar el contenido para la experiencia del usuario. En este modelo, el contenido se crea en AEM, pero diseñarlo, presentarlo y ofrecerlo todo ocurre en otra plataforma.

Las aplicaciones de una sola página (SPA) son a menudo el destino del contenido enviado sin problemas por AEM. Sin embargo, estos SPA no tienen por qué ser totalmente ajenos a AEM. AEM le permite decidir en qué medida su SPA está integrada en AEM. Veamos un ejemplo.

## Ejemplo de Web Shop {#web-shop-example}

Supongamos que tiene una tienda web existente para su compañía como SPA. En él tiene todos los detalles e imágenes del producto. A continuación, AEM para impulsar los esfuerzos de mercadotecnia, como sitios promocionales, blogs y contenido de campaña. ¿Cómo se integran los dos? AEM permite un espectro de opciones:

* **Permitir que los sistemas funcionen de forma independiente.**
* **Proporcione a la tienda web contenido limitado de AEM mediante GraphQL.** El contenido puede ser creado por autores en AEM, pero solo se puede ver a través de la tienda web SPA.
* **Incruste el SPA de la tienda web en AEM.** El contenido puede ser creado por autores en AEM, y visto en AEM en el contexto de la tienda web, pero no manipulado.
* **Incruste el SPA de la tienda web en AEM y active puntos editables.** El contenido puede ser creado por autores en AEM, y visto en AEM en el contexto de la tienda web, y los autores tienen una capacidad limitada para manipular el contenido de la tienda web SPA dentro de AEM.
* **Incruste los SPA de la tienda web en AEM y habilite zonas enteras para editarlas.** El contenido puede ser creado por autores en AEM, y visto en AEM en el contexto de la tienda web, y los autores tienen una capacidad limitada para manipular el contenido de la tienda web SPA dentro de AEM.

La siguiente sección explora estos niveles de integración con más detalle.

>[!NOTE]
>
>Por supuesto, también puede volver a implementar el SPA de tienda web como una AEM que funcione completamente con el marco de trabajo del Editor de AEM.[](/help/implementing/developing/hybrid/introduction.md) Si ya tiene AEM y desea crear una nueva tienda web u otra SPA, este es el método recomendado, pero está fuera del alcance de este documento.

## Niveles de integración de SPA {#integration-levels}

SPA integración se encuentra en un espectro de cuatro niveles en AEM.

* **Nivel 0: Sin integración**
   * Los SPA y AEM existen por separado y no intercambian información.
   * El contenido se crea, administra y entrega de forma independiente en dos sistemas distintos.
* **Nivel 1: Integración de fragmentos de contenido**
   * [Los ](/help/assets/content-fragments/content-fragments.md) fragmentos de contenido se utilizan en AEM para crear y administrar contenido limitado para la SPA.
   * El SPA recupera este contenido mediante AEM [API de GraphQL.](/help/assets/content-fragments/graphql-api-content-fragments.md)
   * Algunos contenidos se administran en AEM y otros en un sistema externo.
   * El contenido solo se puede ver en el SPA.
* **Nivel 2: Incrustar el SPA en AEM**
   * [Los ](/help/assets/content-fragments/content-fragments.md) fragmentos de contenido se utilizan en AEM para crear y administrar el contenido del SPA.
   * El SPA recupera este contenido mediante AEM [API de GraphQL.](/help/assets/content-fragments/graphql-api-content-fragments.md)
   * Algunos contenidos se administran en AEM y otros en un sistema externo.
   * El contenido se puede ver en contexto dentro de AEM.
   * El contenido limitado se puede editar dentro de AEM.
* **Nivel 3: Incrustar y habilitar completamente SPA en AEM**
   * [Los ](/help/assets/content-fragments/content-fragments.md) fragmentos de contenido se utilizan en AEM para crear y administrar el contenido del SPA.
   * El SPA recupera este contenido mediante AEM [API de GraphQL.](/help/assets/content-fragments/graphql-api-content-fragments.md)
   * El contenido se puede ver en contexto dentro de AEM.
   * La mayoría del contenido se puede editar dentro de AEM.

El nivel 1 es un ejemplo de una implementación típica sin cabeza. Sin embargo, los autores de contenido solo pueden vista su contenido en contexto dentro del SPA. AEM es sólo una herramienta de creación.

La ventaja y flexibilidad de la AEM se hace evidente con los niveles 2 y 3, al tiempo que se mantienen las ventajas de la SPA. Los autores de contenido pueden crear su contenido en AEM, pero también verlo en contexto dentro de AEM. El SPA obtiene la capacidad de ser creado en AEM, pero aún así se entrega como un SPA.

## Implementación de los niveles de integración {#implementing}

Hay diferentes herramientas disponibles en AEM según el nivel de integración que elija. Cada nivel se basa en las herramientas utilizadas en el anterior. La siguiente lista vincula los recursos pertinentes.

* **Nivel 1:** Los fragmentos de contenido y el  [AEM ](/help/implementing/developing/headless/introduction.md) marco sin encabezado se pueden usar para entregar AEM contenido al SPA.
* **Nivel 2:** Además del nivel 1:
   * [El ](/help/implementing/developing/hybrid/remote-page.md) componente RemotePage se puede utilizar para incrustar la SPA externa en AEM donde se puede ver AEM contenido en contexto.
   * Algunos puntos del SPA también se pueden habilitar para [permitir la edición limitada en AEM.](/help/implementing/developing/hybrid/editing-external-spa.md)
* **Nivel 3:** Además del nivel dos:
   * Las zonas enteras del SPA pueden habilitarse para permitir una edición completa en AEM.
