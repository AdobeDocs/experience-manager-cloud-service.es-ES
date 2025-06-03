---
title: API de AEM para la entrega de contenido estructurado y la administración de fragmentos de contenido
description: Obtenga información acerca de las API disponibles para la entrega de contenido estructurado y la administración de fragmentos de contenido
feature: Headless, Content Fragments, Edge Delivery Services
role: Admin, Developer
exl-id: 95aecd30-566a-42a9-b97a-7efe45fd389c
source-git-commit: 243adc6f6428cea23c04ca788bd8ad0bda7e4501
workflow-type: tm+mt
source-wordcount: '516'
ht-degree: 28%

---

# API de AEM para la entrega y administración de contenido estructurado {#aem-apis-structured-content-delivery-and-management}

Adobe Experience Manager (AEM) as a Cloud Service ofrece varias API para la entrega de contenido estructurado desde fragmentos de contenido hasta su administración. Consulte las páginas individuales para obtener más información sobre las API específicas.

* [Envío de fragmentos de contenido de AEM con OpenAPI](/help/headless/aem-content-fragment-delivery-with-openapi.md)
   * Esta API crea respuestas JSON para ofrecer contenido estructurado a partir de fragmentos de contenido en AEM.
   * Utiliza una ruta a un fragmento de contenido como punto final.
   * Esta API se basa en REST.
   * Está optimizada para la entrega de contenido, incluida la integración de CDN.
* [API de GraphQL de AEM para la entrega de fragmentos de contenido](/help/headless/graphql-api/content-fragments.md)
   * Esta API está basada en esquemas. Los esquemas de API están representados por modelos de fragmentos de contenido, que definen la estructura de contenido.
   * Esta API está basada en GraphQL.
* [Fragmentos de contenido y OpenAPI de fragmentos de contenido y modelos](/help/headless/content-fragment-openapis.md)
   * Estas API están pensadas para la administración de contenido estructurado.
   * Los respectivos operadores de GET no están optimizados para la entrega de contenido.
   * Esta API se basa en REST.

>[!NOTE]
>
>[La compatibilidad con fragmentos de contenido en la API HTTP de Assets](/help/assets/content-fragments/assets-api-content-fragments.md) ya está [obsoleta](/help/release-notes/deprecated-removed-features.md). Ha sido reemplazado por [Entrega de fragmentos de contenido con OpenAPI](/help/headless/aem-content-fragment-delivery-with-openapi.md) junto con [API de administración de fragmentos de contenido y modelos de fragmentos de contenido](/help/headless/content-fragment-openapis.md).

## REST frente a GraphQL {#rest-vs-graphql}

La API utilizada es una decisión para los desarrolladores: AEM admite ambas.

Muchas comparaciones están disponibles en línea, pero algunos aspectos destacados y beneficios de REST incluyen:

* Simplicidad

   * Los desarrolladores están (a menudo) familiarizados con HTTP y REST. Según el [informe de estado de Postman de las API](https://www.postman.com/state-of-api/), un alto porcentaje de desarrolladores usa REST.

   * Con simplicidad viene la familiaridad. Con REST, no hay preguntas de organización sobre quién posee las consultas y quién la aplicación, mientras que estas preguntas pueden surgir con GraphQL.

   * La familiaridad (por lo general) conlleva una amplia comunidad y un panorama de herramientas. No es una desventaja inherente de GraphQL, pero es probable que sea más amplia y profunda para REST.

   * El enfoque más sencillo también puede facilitar la implementación de la seguridad. Con REST, el filtrado para determinar el contenido que se procesará todo se realiza en la aplicación cliente. Con GraphQL, esto sucede en una consulta basada en esquemas entre el cliente y el servidor.

* Flexibilidad

   * Con REST, el desarrollador puede `GET` cualquier recurso. Con GraphQL, se limitan a recursos definidos dentro de un esquema.

* Almacenamiento en caché

   * Las respuestas JSON a solicitudes REST `GET` se pueden almacenar en caché de forma inherente. Las solicitudes de GraphQL `POST` no se pueden almacenar en caché, a menos que se realicen; por ejemplo, mediante Consultas persistentes de AEM almacenadas en el servidor y solicitadas con solicitudes `GET` similares a REST.

Entre las ventajas de GraphQL se incluyen:

* Eficacia de la entrega de contenido

   * Concentrar

      * Con GraphQL, las aplicaciones cliente pueden solicitar el contenido exacto que necesitan para la representación y no más. Este método evita el exceso de entrega de contenido, con cargas útiles de contenido excesivas y un consumo de ancho de banda innecesario.

   * Extremo único

      * Mientras que en REST cada solicitud de API es un punto de conexión, en GraphQL solo hay un punto de conexión común y diferentes solicitudes de contenido se expresan como consultas que utilizan ese punto de conexión común.

* Prototipado rápido

   * Con GraphQL, este es un proceso de un solo paso, que se reúne en la consulta de GraphQL y puede facilitar la creación de prototipos. REST, por otro lado, es un proceso de 2 pasos:

      1. Buscar contenido con API.
      2. En la respuesta JSON, determine qué se debe utilizar para el procesamiento en la aplicación cliente.
