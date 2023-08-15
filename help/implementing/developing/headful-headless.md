---
title: Encabezado y sin encabezado en AEM
description: AEM Los proyectos de se pueden implementar en un modelo con encabezado y sin encabezado, pero la opción no es binaria. AEM ofrece la flexibilidad para aprovechar las ventajas de ambos modelos en un proyecto.
exl-id: 709850ca-7757-47ab-9625-f411121cde2c
source-git-commit: 5ad33f0173afd68d8868b088ff5e20fc9f58ad5a
workflow-type: tm+mt
source-wordcount: '1013'
ht-degree: 86%

---

# Encabezado y sin encabezado en AEM {#headful-headless}

Los proyectos de Adobe Experience Manager se pueden implementar en modelos con encabezado y sin encabezado, pero la opción no es binaria. AEM ofrece la flexibilidad para aprovechar las ventajas de ambos modelos en un proyecto. Este documento proporciona información general sobre los diferentes modelos y describe los niveles de integración de las SPA.

## Información general {#overview}

AEM ofrece potentes herramientas para gestionar la creación de contenido y su envío en una plataforma. Se trata de un modelo tradicional de administración de contenido “optimista”, en el que los autores y desarrolladores de contenido trabajan en la misma plataforma para enviar las experiencias a los consumidores de contenido.

AEM puede utilizarse simplemente para administrar el contenido, lo que permite que la presentación y el envío del contenido se gestionen mediante otra plataforma. Este es el modelo sin encabezado de la administración de contenido, donde los autores y desarrolladores de contenido trabajan en distintas plataformas para ofrecer experiencia a los consumidores de contenido.

Pero esto no tiene que ser una elección binaria. AEM ofrece una flexibilidad sin precedentes, lo que le permite aprovechar las ventajas de ambos modelos para su proyecto.

![Modelos de implementación de AEM](/help/headless/assets/aem-implementation-models.png)

En un modelo de pila completa o con periférico, el contenido se administra en el repositorio de AEM, y los componentes de AEM basados en Java, HTL, etc., se utilizan para representar el contenido para la experiencia del usuario. En este modelo, la creación del contenido, el estilo, la presentación y la entrega se realizan en AEM.

En un modelo sin encabezado, el contenido se administra en el repositorio de AEM, pero se envía mediante una API como REST y GraphQL a otro sistema para procesar el contenido para la experiencia del usuario. En este modelo, el contenido se crea en AEM, pero el diseño, la presentación y entrega se realiza en otra plataforma.

Las aplicaciones de una sola página (SPA) suelen ser el destino del contenido que AEM entrega sin encabezado. SPA AEM Sin embargo, estos no tienen por qué ser totalmente externos a los usuarios de la red de distribución de la. AEM SPA AEM La opción le permite decidir en qué grado se integran sus en el que se encuentran los usuarios de la aplicación de la. Veamos un ejemplo.

## Ejemplo de la tienda web {#web-shop-example}

Digamos que tiene una tienda web existente para su empresa como SPA. Aquí encontrará todos los detalles e imágenes de productos. AEM A continuación, le presentamos a los usuarios de para que impulsen sus esfuerzos de marketing, como sitios promocionales, blogs y contenido de campañas. ¿Cómo se integran los dos? AEM permite una amplia gama de opciones:

* **Permita que los sistemas funcionen de forma independiente.**
* **Proporcione contenido limitado de AEM a través de GraphQL a la tienda web.** Los autores pueden crear el contenido en AEM, pero solo se puede ver a través de las SPA de la tienda web.
* **Incruste las SPA de la tienda web en AEM.** Los autores pueden crear el contenido en AEM y verlo en contexto de la tienda web, pero no manipularlo.
* **Incruste las SPA de la tienda web en AEM y habilite puntos editables.** Los autores pueden crear el contenido en AEM y verlo en el AEM en el contexto de la tienda web. Los autores tienen una capacidad limitada para manipular el contenido de las SPA en la tienda web dentro de AEM.
* **Incruste las SPA de tiendas web en AEM y habilite zonas enteras para editarlas.** Los autores pueden crear el contenido en AEM y verlo en AEM en el contexto de la tienda web. Los autores tienen una capacidad limitada para manipular el contenido de las SPA en la tienda web dentro de AEM.

La siguiente sección explora estos niveles de integración con más detalle.

>[!NOTE]
>
>SPA AEM SPA Por supuesto, también podría volver a implementar la tienda web como un sitio web que funciona por completo como un sitio web que funciona a la vez que se convierte en un sitio web que funciona a la vez en un [AEM SPA Uso del marco de trabajo del Editor de](/help/implementing/developing/hybrid/introduction.md). Si ya tiene AEM y desea crear una nueva tienda web u otras SPA, este es el método recomendado, pero queda fuera del alcance de este documento.

## Niveles de integración de las SPA {#integration-levels}

La integración de una SPA se encuentra en un rango de cuatro niveles en AEM.

* **Nivel 0: sin integración**
   * Las SPA y AEM existen por separado y no intercambian información.
   * El contenido se crea, gestiona y entrega de forma independiente en dos sistemas separados.
* **Nivel 1: integración de fragmentos de contenido**
   * Los [Fragmentos de contenido](/help/sites-cloud/administering/content-fragments/content-fragments.md) se utilizan en AEM para crear y administrar contenido limitado para las SPA.
   * SPA AEM El recupera este contenido a través de la opción de [API de GraphQL](/help/headless/graphql-api/content-fragments.md).
   * Algunos contenidos se administran en AEM, y otros, en un sistema externo.
   * El contenido solo se puede ver en las SPA.
* **Nivel 2: incrustar las SPA en AEM**
   * Los [Fragmentos de contenido](/help/sites-cloud/administering/content-fragments/content-fragments.md) se utilizan en AEM para crear y administrar el contenido de las SPA.
   * SPA AEM El recupera este contenido a través de la opción de [API de GraphQL](/help/headless/graphql-api/content-fragments.md).
   * Algunos contenidos se administran en AEM, y otros, en un sistema externo.
   * El contenido se puede ver en contexto dentro de AEM.
   * El contenido limitado se puede editar dentro de AEM.
* **Nivel 3: incrustar y habilitar completamente la SPA en AEM**
   * Los [Fragmentos de contenido](/help/sites-cloud/administering/content-fragments/content-fragments.md) se utilizan en AEM para crear y administrar el contenido de la SPA.
   * SPA AEM El recupera este contenido a través de la opción de [API de GraphQL](/help/headless/graphql-api/content-fragments.md).
   * El contenido se puede ver en contexto dentro de AEM.
   * La mayoría del contenido se puede editar dentro de AEM.

El nivel 1 es un ejemplo de una implementación típica sin encabezado. Sin embargo, los autores de contenido solo pueden ver su contenido en contexto dentro de la SPA. AEM es solo una herramienta de creación.

La ventaja y la flexibilidad de AEM se hacen evidentes con los niveles 2 y 3, al mismo tiempo que se conservan las ventajas de la SPA. Los autores de contenido pueden crear su contenido y también verlo en contexto dentro de AEM. La SPA adquiere la capacidad de crearse en AEM, pero se sigue entregando como una SPA.

## Implementación de los niveles de integración {#implementing}

Existen diferentes herramientas disponibles en AEM según el nivel de integración que elija. Cada nivel se basa en las herramientas utilizadas en el anterior nivel. La siguiente lista vincula los recursos pertinentes.

* **Nivel 1:** los fragmentos de contenido y el [marco de trabajo de AEM sin encabezado](/help/headless/introduction.md) se pueden utilizar para enviar contenido AEM a la SPA.
* **Nivel 2:** Además del nivel uno:
   * [El componente RemotePage](/help/implementing/developing/hybrid/remote-page.md) se puede utilizar para integrar la SPA externa en AEM donde el contenido de AEM se puede ver en contexto.
   * Algunos puntos de la SPA también se pueden habilitar para [permitir la edición limitada en AEM](/help/implementing/developing/hybrid/editing-external-spa.md).
* **Nivel 3:** Además del nivel dos:
   * Se pueden habilitar zonas enteras de la SPA para permitir una edición completa en AEM.
