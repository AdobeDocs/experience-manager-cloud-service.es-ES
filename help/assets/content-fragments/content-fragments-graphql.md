---
title: Entrega de contenido sin objetivos mediante fragmentos de contenido con GraphQL
description: Aprenda los conceptos básicos de realización de un CMS sin encabezado AEM utilizando fragmentos de contenido con GraphQL para la entrega de contenido sin encabezado.
feature: Content Fragments, GraphQL API
topic: Headless
role: User
exl-id: 4a3b030d-ed59-4920-bf94-e00a45f85b51
source-git-commit: e776368891457d3d8cb91b1bb31c1563131f7557
workflow-type: tm+mt
source-wordcount: '731'
ht-degree: 17%

---

# Entrega de contenido sin objetivos mediante fragmentos de contenido con GraphQL {#headless-content-delivery-using-content-fragments-with-graphQL}

Con los fragmentos de contenido y la API de GraphQL, puede utilizar Adobe Experience Manager (AEM) as a Cloud Service como un sistema de gestión de contenido sin encabezado (CMS).

Esto se logra mediante los fragmentos de contenido, junto con la API de AEM GraphQL (una implementación personalizada, basada en GraphQL estándar), para ofrecer contenido estructurado sin problemas para utilizarlo en sus aplicaciones. La capacidad de personalizar una sola consulta de API le permite recuperar y entregar el contenido específico que desea o necesita procesar (como respuesta a la consulta de API única).

>[!NOTE]
>
>Consulte también lo siguiente:
>
>* [¿Qué es Headless?](/help/headless/what-is-headless.md) para obtener una introducción a los conceptos y la terminología sin encabezado.
>
>* [Sin encabezado y AEM](/help/headless/introduction.md) para obtener una introducción al desarrollo sin encabezado para AEM Sites as a Cloud Service.


>[!NOTE]
>
>GraphQL se utiliza actualmente en dos escenarios (independientes) en Adobe Experience Manager (AEM) as a Cloud Service:
>
>* [AEM Commerce consume datos de una plataforma de comercio a través de GraphQL](/help/commerce-cloud/integrating/magento.md).
>* [Los fragmentos de contenido de AEM trabajan junto con la API de GraphQL de AEM (una implementación personalizada, basada en GraphQL estándar) para ofrecer contenido estructurado para su uso en aplicaciones](/help/headless/graphql-api/content-fragments.md).


## CMS sin encabezado {#headless-cms}

Un sistema de administración de contenido sin encabezado (CMS) es un sistema de administración de contenido exclusivo en el back-end, diseñado y creado explícitamente como repositorio de contenido que hace que el contenido sea accesible a través de una API, para su visualización en cualquier dispositivo.

En cuanto a la creación de fragmentos de contenido en AEM, esto significa que:

* Puede utilizar fragmentos de contenido para crear contenido que no vaya a publicarse directamente (1:1) en páginas con formato.

* El contenido de los fragmentos de contenido se estructurará de forma predeterminada según los modelos de fragmento de contenido. Esto simplifica el acceso para las aplicaciones, que procesarán aún más el contenido.

## GraphQL: Información general {#graphql-overview}

GraphQL es:

* &quot;*...un idioma de consulta para API y un tiempo de ejecución para cumplir esas consultas con los datos existentes.*&quot;.

   Consulte [GraphQL.org](https://graphql.org)

La variable [API de AEM GraphQL](#aem-graphql-api) le permite realizar consultas (complejas) en su [Fragmentos de contenido](/help/assets/content-fragments/content-fragments.md); con cada consulta siendo según un tipo de modelo específico. Las aplicaciones pueden utilizar el contenido devuelto.

## API de AEM GraphQL {#aem-graphql-api}

Para Adobe Experience as a Cloud Experience, se ha desarrollado una implementación personalizada de la API estándar de GraphQL. Consulte [AEM API de GraphQL para su uso con fragmentos de contenido](/help/headless/graphql-api/content-fragments.md) para obtener más información.

La implementación de la API de AEM GraphQL se basa en la variable [Bibliotecas Java de GraphQL](https://graphql.org/code/#java).

## Fragmentos de contenido para su uso con la API de AEM GraphQL {#content-fragments-use-with-aem-graphql-api}

[Fragmentos de contenido](#content-fragments) se puede usar como base para GraphQL para AEM consultas como:

* Permiten diseñar, crear, depurar y publicar contenido independiente de las páginas.
* La variable [Modelos de fragmento de contenido](#content-fragments-models) proporcionar la estructura necesaria mediante tipos de datos definidos.
* La variable [Referencia de fragmento](#fragment-references), disponible al definir un modelo, se puede utilizar para definir capas de estructura adicionales.

![Fragmentos de contenido para usar con GraphQL](assets/cfm-nested-01.png "Fragmentos de contenido para usar con GraphQL")

### Fragmentos de contenido {#content-fragments}

Fragmentos de contenido:

* Contienen contenido estructurado.

* Se basan en un [Modelo de fragmento de contenido](#content-fragments-models), que predefine la estructura del fragmento resultante.

### Modelos de fragmento de contenido {#content-fragments-models}

Estos [Modelos de fragmento de contenido](/help/assets/content-fragments/content-fragments-models.md):

* Se utilizan para generar la variable [Esquemas](https://graphql.org/learn/schema/), una vez **Habilitado**.

* Proporcione los tipos de datos y campos requeridos para GraphQL. Se aseguran de que la aplicación solo solicita lo que es posible y recibe lo que se espera.

* El tipo de datos **[Referencias de fragmento](#fragment-references)** se puede utilizar en el modelo para hacer referencia a otro fragmento de contenido y, por lo tanto, introducir niveles de estructura adicionales.

### Referencias de fragmento {#fragment-references}

La variable **[Referencia de fragmento](/help/assets/content-fragments/content-fragments-models.md#fragment-reference-nested-fragments)**:

* Es de particular interés en conjunto con GraphQL.

* Es un tipo de datos específico que se puede utilizar al definir un modelo de fragmento de contenido.

* Hace referencia a otro fragmento, según un modelo de fragmento de contenido específico.

* Permite recuperar datos estructurados.

   * Cuando se define como **multifuente**, el fragmento principal puede hacer referencia (recuperar) a varios subfragmentos.

### Vista previa de JSON {#json-preview}

Para ayudar a diseñar y desarrollar los modelos de fragmento de contenido, puede obtener una vista previa [Salida JSON](/help/assets/content-fragments/content-fragments-json-preview.md).

## Formación para utilizar GraphQL con AEM: contenido y consultas de muestra {#learn-graphql-with-aem-sample-content-queries}

Consulte [Aprender a utilizar GraphQL con AEM: contenido de muestra y consultas](/help/headless/graphql-api/sample-queries.md) para obtener una introducción al uso de la API de AEM GraphQL.

## Tutorial: Introducción a AEM Headless y GraphQL

¿Busca un tutorial práctico? Consulte el tutorial completo [Introducción a AEM Headless y GraphQL](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/overview.html?lang=es), que ilustra cómo crear y exponer contenido mediante las API de GraphQL de AEM y consumido por una aplicación externa, en un escenario de CMS sin encabezado.
