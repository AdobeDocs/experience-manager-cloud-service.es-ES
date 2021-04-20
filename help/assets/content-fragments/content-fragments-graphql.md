---
title: Entrega de contenido sin objetivos mediante fragmentos de contenido con GraphQL
description: Aprenda a utilizar AEM fragmentos de contenido con GraphQL para la entrega de contenido sin encabezado.
feature: Content Fragments
role: Business Practitioner
exl-id: 4a3b030d-ed59-4920-bf94-e00a45f85b51
translation-type: tm+mt
source-git-commit: 1d0343dc7940566b88ad490bb8fb08a5ad4ff5c2
workflow-type: tm+mt
source-wordcount: '718'
ht-degree: 1%

---

# Entrega de contenido sin encabezado mediante fragmentos de contenido con GraphQL {#headless-content-delivery-using-content-fragments-with-graphQL}

Con Adobe Experience Manager (AEM) como Cloud Service, puede utilizar los fragmentos de contenido, junto con la API de GraphQL de AEM (una implementación personalizada, basada en GraphQL estándar), para ofrecer sin problemas contenido estructurado para su uso en sus aplicaciones. La capacidad de personalizar una sola consulta de API le permite recuperar y entregar el contenido específico que desea o necesita procesar (como respuesta a la consulta de API única).

>[!NOTE]
>
>Consulte [Sin encabezado y AEM](/help/implementing/developing/headless/introduction.md) para obtener una introducción al desarrollo sin encabezado para AEM Sites as a Cloud Service.

>[!NOTE]
>
>GraphQL se utiliza actualmente en dos escenarios (independientes) en Adobe Experience Manager (AEM) como Cloud Service:
>
>* [AEM Commerce consume datos de una plataforma de comercio a través de GraphQL](/help/commerce-cloud/integrating/magento.md).
>* [AEM fragmentos de contenido trabajan junto con la API de GraphQL de AEM (una implementación personalizada, basada en GraphQL estándar) para ofrecer contenido estructurado para su uso en sus aplicaciones](/help/assets/content-fragments/graphql-api-content-fragments.md).


## CMS sin encabezado {#headless-cms}

Un sistema de administración de contenido sin objetivos (CMS) es:

* &quot;*Un sistema de administración de contenido sin encabezado, o CMS sin encabezado, es un sistema de administración de contenido (CMS) de back-end creado desde cero como repositorio de contenido que hace que el contenido sea accesible a través de una API para su visualización en cualquier dispositivo.*

   Consulte [Wikipedia](https://en.wikipedia.org/wiki/Headless_content_management_system).

En cuanto a la creación de fragmentos de contenido en AEM, esto significa que:

* Puede utilizar fragmentos de contenido para crear contenido que no vaya a publicarse directamente (1:1) en páginas con formato.

* El contenido de los fragmentos de contenido se estructurará de forma predeterminada según los modelos de fragmento de contenido. Esto simplifica el acceso para las aplicaciones, que procesarán aún más el contenido.

## GraphQL: Información general {#graphql-overview}

GraphQL es:

* &quot;*...un idioma de consulta para API y un tiempo de ejecución para cumplir esas consultas con los datos existentes.*&quot;.

   Consulte [GraphQL.org](https://graphql.org)

La [AEM API de GraphQL](#aem-graphql-api) le permite realizar consultas (complejas) en sus [fragmentos de contenido](/help/assets/content-fragments/content-fragments.md); con cada consulta siendo según un tipo de modelo específico. Las aplicaciones pueden utilizar el contenido devuelto.

## API de AEM GraphQL {#aem-graphql-api}

Para Adobe Experience as a Cloud Experience, se ha desarrollado una implementación personalizada de la API estándar de GraphQL. Consulte [AEM API de GraphQL para su uso con fragmentos de contenido](/help/assets/content-fragments/graphql-api-content-fragments.md) para obtener más información.

La implementación de la API de AEM GraphQL se basa en las [bibliotecas Java de GraphQL](https://graphql.org/code/#java).

## Fragmentos de contenido para usar con la API de AEM GraphQL {#content-fragments-use-with-aem-graphql-api}

[Los ](#content-fragments) fragmentos de contenido se pueden usar como base para GraphQL para AEM consultas como:

* Permiten diseñar, crear, depurar y publicar contenido independiente de las páginas.
* Los [modelos de fragmento de contenido](#content-fragments-models) proporcionan la estructura necesaria mediante tipos de datos definidos.
* La [Referencia de fragmento](#fragment-references), disponible al definir un modelo, se puede utilizar para definir capas de estructura adicionales.

![Fragmentos de contenido para su uso con fragmentos de ](assets/cfm-nested-01.png "contenido GraphQLContent para su uso con GraphQL")

### Fragmentos de contenido {#content-fragments}

Fragmentos de contenido:

* Contienen contenido estructurado.

* Se basan en un [Modelo de fragmento de contenido](#content-fragments-models), que predefine la estructura del fragmento resultante.

### Modelos de fragmento de contenido {#content-fragments-models}

Estos [modelos de fragmento de contenido](/help/assets/content-fragments/content-fragments-models.md):

* Se utilizan para generar los [Esquemas](https://graphql.org/learn/schema/), una vez **Enabled**.

* Proporcione los tipos de datos y campos requeridos para GraphQL. Se aseguran de que la aplicación solo solicita lo que es posible y recibe lo que se espera.

* El tipo de datos **[Referencias de fragmento](#fragment-references)** se puede usar en el modelo para hacer referencia a otro fragmento de contenido y, por lo tanto, introducir niveles adicionales de estructura.

### Referencias de fragmento {#fragment-references}

La **[Referencia de fragmento](/help/assets/content-fragments/content-fragments-models.md#fragment-reference-nested-fragments)**:

* Es de particular interés en conjunto con GraphQL.

* Es un tipo de datos específico que se puede utilizar al definir un modelo de fragmento de contenido.

* Hace referencia a otro fragmento, según un modelo de fragmento de contenido específico.

* Permite recuperar datos estructurados.

   * Cuando se define como una **fuente múltiple**, el fragmento principal puede hacer referencia (recuperar) a varios subfragmentos.

### Vista previa de JSON {#json-preview}

Para ayudar a diseñar y desarrollar los modelos de fragmento de contenido, puede obtener una vista previa de [JSON output](/help/assets/content-fragments/content-fragments-json-preview.md).

## Aprender a utilizar GraphQL con AEM: Contenido de muestra y consultas {#learn-graphql-with-aem-sample-content-queries}

Consulte [Learning to use GraphQL with AEM - Sample Content and Queries](/help/assets/content-fragments/content-fragments-graphql-samples.md) para ver una introducción al uso de la API de AEM GraphQL.

## Tutorial: Introducción a AEM sin encabezado y GraphQL

¿Busca un tutorial práctico? Consulte el tutorial completo [Introducción a AEM sin encabezado y GraphQL](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/overview.html) que ilustra cómo crear y exponer contenido mediante las API de GraphQL de AEM y consumido por una aplicación externa, en un escenario de CMS sin encabezado.
