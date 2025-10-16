---
title: 'Creación de una solicitud de API: configuración sin encabezado'
description: Aprenda a utilizar la API de GraphQL para la entrega sin encabezado de contenido de fragmentos de contenido y la API de REST de Assets de AEM para administrar fragmentos de contenido.
exl-id: 2b72f222-2ba5-4a21-86e4-40c763679c32
feature: Headless, Content Fragments,GraphQL API
role: Admin, Developer
source-git-commit: 38a4bf89e099432163163e90e08aa0f47407724f
workflow-type: tm+mt
source-wordcount: '417'
ht-degree: 88%

---

# Creación de una solicitud de API: configuración sin encabezado {#accessing-delivering-content-fragments}

Aprenda a utilizar la API de GraphQL para la entrega sin encabezado de contenido de fragmentos de contenido y la API de REST de Assets de AEM para administrar fragmentos de contenido.

## ¿Qué son las API de REST de GraphQL y Assets? {#what-are-the-apis}

[Ahora que ha creado algunos fragmentos de contenido](create-content-fragment.md), puede usar las API de AEM para entregarlas sin encabezado.

* [La API de GraphQL](/help/headless/graphql-api/content-fragments.md) permite crear solicitudes para acceder a fragmentos de contenido y enviarlos. Esta API ofrece el conjunto más sólido de funciones para consultar y consumir contenido de fragmentos de contenido.
   * Para utilizar la API, [defina y habilite puntos finales en AEM](/help/headless/graphql-api/graphql-endpoint.md) y, si es necesario, la [interfaz de GraphiQL instalada](/help/headless/graphql-api/graphiql-ide.md).
* Hay una selección de [API de AEM para la administración y entrega de contenido estructurado](/help/headless/apis-headless-and-content-fragments.md) disponibles para su uso con fragmentos de contenido.

El resto de esta guía se centra en el acceso a GraphQL y la entrega de fragmentos de contenido.

## Habilitación del punto de conexión de GraphQL {#enable-graphql-endpoint}

Antes de poder utilizar las API de GraphQL, se debe crear un punto de conexión de GraphQL.

Para obtener más información, consulte [Administrar extremos de GraphQL en AEM](/help/headless/graphql-api/graphql-endpoint.md).

## Consulta de contenido mediante GraphQL con GraphiQL

Los arquitectos de la información diseñan consultas para sus puntos finales de canal para entregar contenido. Considere estas consultas solo una vez por punto final, por modelo. Para los fines de esta guía de introducción, solo debe crear uno.

GraphiQL es un IDE, incluido en su entorno AEM; es accesible/visible después de [configurar los extremos](#enable-graphql-endpoint).

Para obtener más información, consulte [Uso del IDE de GraphiQL](/help/headless/graphql-api/graphiql-ide.md).

GraphQL permite consultas estructuradas que pueden dirigirse no solo a conjuntos de datos específicos u objetos de datos individuales, sino que también pueden proporcionar elementos específicos de los objetos, resultados anidados, compatibilidad con variables de consulta y mucho más.

GraphQL puede evitar las solicitudes de API iterativas y el exceso de entrega, y en su lugar permite realizar entregas masivas de exactamente lo que se necesita para procesar como respuesta a una única consulta de API. El JSON resultante se puede utilizar para entregar datos en otros sitios o aplicaciones.

## Siguientes pasos {#next-steps}

¡Eso es todo! Ahora tiene una comprensión básica de la administración de contenido sin encabezado en AEM. Hay muchos más recursos en los que puede profundizar para comprender las funciones disponibles.

* **[Fragmentos de contenido](/help/sites-cloud/administering/content-fragments/managing.md)**: para obtener más información acerca de la creación y administración de fragmentos de contenido
* **[Compatibilidad con fragmentos de contenido en la API HTTP de AEM Assets](/help/assets/content-fragments/assets-api-content-fragments.md)**: para obtener más información sobre el acceso al contenido de AEM directamente a través de la API HTTP, mediante las operaciones CRUD (Crear, Leer, Actualizar, Eliminar)
* **[API de GraphQL](/help/headless/graphql-api/content-fragments.md)**: para obtener más información sobre cómo enviar fragmentos de contenido sin encabezado

>[!NOTE]
>
>Las [OpenAPI de fragmento de contenido y modelo de fragmento de contenidos](/help/headless/content-fragment-openapis.md) también están disponibles.
