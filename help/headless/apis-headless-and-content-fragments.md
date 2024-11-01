---
title: AEM API de para la entrega de contenido estructurado y la administración de fragmentos de contenido
description: Obtenga información acerca de las API disponibles para la entrega de contenido estructurado y la administración de fragmentos de contenido
feature: Headless, Content Fragments, Edge Delivery Services
role: Admin, Developer
source-git-commit: 21599676916068f3529976410a93951b02f750b0
workflow-type: tm+mt
source-wordcount: '592'
ht-degree: 0%

---


# AEM API de para la entrega y administración de contenido estructurado {#aem-apis-structured-content-delivery-and-management}

Adobe Experience Manager AEM () as a Cloud Service ofrece varias API tanto para la entrega de contenido estructurado desde Fragmentos de contenido como para la administración de Fragmentos de contenido. Consulte las páginas individuales para obtener más información sobre las API específicas.

* AEM [REST OpenAPI para la entrega de fragmentos de contenido](/help/headless/aem-rest-openapi-content-fragment-delivery.md)
   * AEM Esta API crea respuestas JSON para ofrecer contenido estructurado a partir de fragmentos de contenido en el espacio de trabajo de la.
   * Utiliza una ruta a un fragmento de contenido como punto final.
   * Esta API se basa en REST.
   * Está optimizado para la entrega de contenido, incluida la integración de CDN.
* [AEM API de GraphQL para la entrega de fragmentos de contenido](/help/headless/graphql-api/content-fragments.md)
   * Esta API se basa en esquemas. Los esquemas de API están representados por modelos de fragmentos de contenido, que definen la estructura de contenido.
   * Esta API se basa en GraphQL.
* [Fragmentos de contenido y modelos de fragmentos de contenido OpenAPI](/help/headless/content-fragment-openapis.md)
   * Estas API están pensadas para la administración de contenido estructurado.
   * Los respectivos operadores de GET no están optimizados para la entrega de contenido.
   * Esta API se basa en REST.
* [Compatibilidad con fragmentos de contenido en la API HTTP de AEM Assets](/help/assets/content-fragments/assets-api-content-fragments.md)
   * AEM La API original para la salida JSON para la entrega de contenido estructurado en la.
      * Aunque es sólida y está probada, esta API no ofrece *salida JSON totalmente hidratada*. Las referencias solo se muestran como rutas, lo que requiere solicitudes de API secundarias para recuperar contenido adicional.
   * La API HTTP de Assets también se puede utilizar para administrar los fragmentos de contenido y los modelos de fragmentos de contenido (CRUD).
   * Esta API se basa en REST.
   * La compatibilidad con fragmentos de contenido en la API HTTP de Assets quedará obsoleta en el futuro, ya que la API REST de JSON de Edge Delivery Services la sustituye. La escala temporal aún no se ha decidido.

<!--
## JSON vs HTML {#json-vs-HTML}

The content delivery format used is driven by frontend implementation. Unstructured content/HTML for full-stack implementations, structured content/JSON for headless implementations, or a combination of both in hybrid implementations. 

Key considerations include:

* Definition
  * JSON (JavaScript Object Notation) - used to represent, access and process structured data. 
  * HTML (HyperText Markup Language) - a markup language of tags and elements in a hierarchical structure.
* Primary Purpose
  * JSON is often used for transferring structure content between the server and client app.
  * HTML is the standard markup language for creating and rendering web pages in a browser.
-->

## REST frente a GraphQL {#rest-vs-graphql}

AEM La API utilizada es una decisión para los desarrolladores; admite ambos, en el caso de los desarrolladores, y es compatible con los dos.

Muchas comparaciones están disponibles en línea, pero algunos aspectos destacados y beneficios de REST incluyen:

* Simplicidad

   * Los desarrolladores están (a menudo) familiarizados con HTTP y REST. Según el [informe de estado de Postman de las API](https://www.postman.com/state-of-api/), un alto porcentaje de desarrolladores usa REST.

   * Con simplicidad viene la familiaridad. Con REST, no hay preguntas de organización sobre quién posee las consultas y quién la aplicación, mientras que estas preguntas pueden surgir con GraphQL.

   * La familiaridad (por lo general) conlleva una amplia comunidad y un panorama de herramientas. No es una desventaja inherente de GraphQL, pero es probable que sea más amplia y profunda para REST.

   * El enfoque más sencillo también puede facilitar la implementación de la seguridad. Con REST, el filtrado para determinar el contenido que se procesará todo se realiza en la aplicación cliente. Con GraphQL, esto sucede en una consulta basada en esquemas entre el cliente y el servidor.

* Flexibilidad

   * Con REST, el desarrollador puede `GET` cualquier recurso. Con GraphQL, se limitan a recursos definidos dentro de un esquema.

* Almacenamiento en caché

   * Las respuestas JSON a solicitudes REST `GET` se pueden almacenar en caché de forma inherente. Las solicitudes de GraphQL AEM `POST` no se pueden almacenar en caché, a menos que se realicen; por ejemplo, utilizando Consultas persistentes en la memoria caché almacenadas en el servidor y solicitadas con solicitudes `GET` similares a REST.

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
