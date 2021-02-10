---
title: Envío de contenido sin cabeza mediante fragmentos de contenido con GraphQL
description: Descubra cómo usar fragmentos de contenido en Adobe Experience Manager (AEM) como Cloud Service con GraphQL para el Envío de contenido sin encabezado.
translation-type: tm+mt
source-git-commit: c5f041f29133718a4260a289255e21b535cde12f
workflow-type: tm+mt
source-wordcount: '723'
ht-degree: 0%

---


# Envío de contenido sin cabeza mediante fragmentos de contenido con GraphQL {#headless-content-delivery-using-content-fragments-with-graphQL}

Con Adobe Experience Manager (AEM) como Cloud Service, puede utilizar Fragmentos de contenido, junto con la API de GraphQL de AEM (una implementación personalizada, basada en GraphQL estándar), para ofrecer contenido estructurado para su uso en las aplicaciones. La capacidad de personalizar una sola consulta de API le permite recuperar y entregar el contenido específico que desea o necesita procesar (como respuesta a la única consulta de API).

>[!NOTE]
>
>Consulte [Sin cabeza y AEM](/help/implementing/developing/headless/introduction.md) para obtener una introducción al desarrollo sin cabeza para AEM Sites como Cloud Service.

>[!NOTE]
>
>GraphQL se utiliza actualmente en dos escenarios (independientes) de Adobe Experience Manager (AEM) como Cloud Service:
>
>* [AEM Commerce consume datos de una plataforma comercial a través de GraphQL](/help/commerce-cloud/architecture/magento.md).
>* [AEM fragmentos de contenido trabajan junto con la API de GraphQL AEM (una implementación personalizada, basada en GraphQL estándar) para ofrecer contenido estructurado para su uso en las aplicaciones](/help/assets/content-fragments/graphql-api-content-fragments.md).


## CMS sin cabeza {#headless-cms}

Un sistema de Gestor de contenido sin cabeza (CMS) es:

* &quot;*Un sistema de gestor de contenido sin cabezales, o CMS sin cabezal, es un sistema de gestor de contenido solo de back-end (CMS) creado desde cero como un repositorio de contenido que hace que el contenido sea accesible a través de una API para su visualización en cualquier dispositivo.*

   Consulte [Wikipedia](https://en.wikipedia.org/wiki/Headless_content_management_system).

En cuanto a la creación de fragmentos de contenido en AEM, esto significa que:

* Puede utilizar Fragmentos de contenido para crear contenido que no se vaya a publicar directamente (1:1) en páginas con formato.

* El contenido de los fragmentos de contenido se estructurará de una manera predeterminada, según los modelos de fragmento de contenido. Esto simplifica el acceso para las aplicaciones, lo que permitirá procesar aún más el contenido.

## GraphQL: Información general {#graphql-overview}

GraphQL es:

* &quot;*...un lenguaje de consulta para API y un tiempo de ejecución para cumplir esas consultas con los datos existentes.*&quot;.

   Consulte [GraphQL.org](https://graphql.org)

La [API de GraphQL de AEM](#aem-graphql-api) le permite realizar consultas (complejas) en sus [fragmentos de contenido](/help/assets/content-fragments/content-fragments.md); con cada consulta en función de un tipo de modelo específico. El contenido devuelto puede ser utilizado por las aplicaciones.

## API de AEM GraphQL {#aem-graphql-api}

Para Adobe Experience as a Cloud Experience, se ha desarrollado una implementación personalizada de la API GraphQL estándar. Consulte [API de GraphQL de AEM para obtener más información sobre el uso con fragmentos de contenido](/help/assets/content-fragments/graphql-api-content-fragments.md).

La implementación de la API de AEM GraphQL se basa en las [bibliotecas Java de GraphQL](https://graphql.org/code/#java).

## Fragmentos de contenido para usar con la API de AEM GraphQL {#content-fragments-use-with-aem-graphql-api}

[Los ](#content-fragments) fragmentos de contenido se pueden usar como base para GraphQL en consultas de AEM como:

* Permiten diseñar, crear, depurar y publicar contenido independiente de las páginas.
* Los [Modelos de fragmento de contenido](#content-fragments-models) proporcionan la estructura requerida mediante tipos de datos definidos.
* La [Referencia de fragmento](#fragment-references), disponible al definir un modelo, puede utilizarse para definir capas adicionales de estructura.

![Fragmentos de contenido para usar con fragmentos de ](assets/cfm-nested-01.png "contenido GraphQLContent para GraphQL")

### Fragmentos de contenido {#content-fragments}

Fragmentos de contenido:

* Contiene contenido estructurado.

* Se basan en un [Modelo de fragmento de contenido](#content-fragments-models), que predefine la estructura del fragmento resultante.

### Modelos de fragmento de contenido {#content-fragments-models}

Estos [Modelos de fragmento de contenido](/help/assets/content-fragments/content-fragments-models.md):

* Se utilizan para generar los [Esquemas](https://graphql.org/learn/schema/), una vez **Habilitados**.

* Proporcione los tipos de datos y los campos requeridos para GraphQL. Garantizan que la aplicación sólo solicite lo posible y recibe lo que se espera.

* El tipo de datos **[Referencias de fragmento](#fragment-references)** se puede usar en el modelo para hacer referencia a otro fragmento de contenido y, por lo tanto, introducir niveles adicionales de estructura.

### Referencias de fragmento {#fragment-references}

La **[Referencia de fragmento](/help/assets/content-fragments/content-fragments-models.md#fragment-reference-nested-fragments)**:

* Es de particular interés en conjunto con GraphQL.

* Es un tipo de datos específico que se puede utilizar al definir un modelo de fragmento de contenido.

* Hace referencia a otro fragmento, según un modelo de fragmento de contenido específico.

* Permite recuperar datos estructurados.

   * Cuando se define como una **fuente múltiple**, el fragmento principal puede hacer referencia (recuperar) a varios subfragmentos.

### Previsualización JSON {#json-preview}

Para ayudarle a diseñar y desarrollar sus modelos de fragmento de contenido, puede realizar la previsualización [salida de JSON](/help/assets/content-fragments/content-fragments-json-preview.md).

## Aprender a usar GraphQL con AEM: Contenido de muestra y Consultas {#learn-graphql-with-aem-sample-content-queries}

Consulte [Aprendizaje de utilizar GraphQL con AEM: Contenido de muestra y Consultas](/help/assets/content-fragments/content-fragments-graphql-samples.md) para obtener una introducción al uso de la API de GraphQL de AEM.

## Tutorial: Introducción a AEM sin encabezado y GraphQL

¿Busca un tutorial práctico? Consulte [Introducción a AEM sin encabezado y GraphQL](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/overview.html) tutorial completo que ilustra cómo crear y exponer contenido mediante las API de GraphQL de AEM y consumido por una aplicación externa, en un escenario CMS sin encabezado.