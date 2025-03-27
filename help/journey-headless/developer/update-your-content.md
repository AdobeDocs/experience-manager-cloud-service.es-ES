---
title: Actualización del contenido mediante las API de AEM
description: En esta parte del Recorrido para desarrolladores de AEM Headless, aprenda a utilizar las API disponibles para acceder y actualizar el contenido de los fragmentos de contenido.
exl-id: 84120856-fd1d-40f7-8df4-73d4cdfcc43b
solution: Experience Manager
feature: Headless, Content Fragments, GraphQL API
role: Admin, Architect, Developer
source-git-commit: d8e4fdc4f79e40a43a6845ab083dc231444b9c99
workflow-type: tm+mt
source-wordcount: '580'
ht-degree: 33%

---

# Actualización del contenido mediante las API de AEM {#update-your-content}

En esta parte del [Recorrido para desarrolladores sin encabezado de AEM](overview.md), aprenda a utilizar las API disponibles para acceder al contenido de sus fragmentos de contenido y actualizarlo.

## Lo que hemos visto hasta ahora {#story-so-far}

En el documento anterior del recorrido de AEM sin encabezado, [Cómo acceder al contenido a través de las API de entrega de AEM](access-your-content.md), aprendió a acceder al contenido sin encabezado en AEM mediante la API de GraphQL de AEM, por lo que ahora debería poder hacer lo siguiente:

* Tener conocimientos avanzados de GraphQL.
* Comprender cómo funciona la API de GraphQL de AEM.
* Comprender algunos ejemplos prácticos de consultas.

Este artículo se basa en estos aspectos básicos para que entienda cómo actualizar el contenido sin encabezado existente en AEM a través de las API disponibles.

## Objetivo {#objective}

* **Audiencia**: avanzadas
* **Objetivo**: obtenga información acerca de las API disponibles para acceder al contenido de los fragmentos de contenido y actualizarlo.

## API de AEM para su uso con fragmentos de contenido {#aem-apis-for-use-with-content-fragments}

Adobe Experience Manager (AEM) as a Cloud Service ofrece varias API para la entrega de contenido estructurado desde Fragmentos de contenido y la administración de Fragmentos de contenido. Consulte las páginas individuales para obtener más información sobre las API específicas.

* REST OpenAPI de AEM para la entrega de fragmentos de contenido
   * Esta API crea respuestas JSON para ofrecer contenido estructurado a partir de fragmentos de contenido en AEM.
   * Utiliza una ruta a un fragmento de contenido como punto final.
   * Esta API se basa en REST.
   * Está optimizado para la entrega de contenido, incluida la integración de CDN.
* API de AEM GraphQL para la entrega de fragmentos de contenido
   * Esta API se basa en esquemas. Los esquemas de API están representados por modelos de fragmentos de contenido, que definen la estructura de contenido.
   * Esta API se basa en GraphQL.
* Fragmentos de contenido y modelos de fragmentos de contenido OpenAPI
   * Estas API están pensadas para la administración de contenido estructurado.
   * Los respectivos operadores de GET no están optimizados para la entrega de contenido.
   * Esta API se basa en REST.
* Compatibilidad con fragmentos de contenido en la API HTTP de AEM Assets
   * La API original para la salida JSON para la entrega de contenido estructurado en AEM.
      * Aunque es sólida y está probada, esta API no ofrece *salida JSON totalmente hidratada*. Las referencias solo se muestran como rutas, lo que requiere solicitudes de API secundarias para recuperar contenido adicional.
   * La API HTTP de Assets también se puede utilizar para administrar los fragmentos de contenido y los modelos de fragmentos de contenido (CRUD).
   * Esta API se basa en REST.
   * La compatibilidad con fragmentos de contenido en la API HTTP de Assets quedará obsoleta en el futuro, ya que la API REST JSON de Edge Delivery Services la sustituye. La escala temporal aún no se ha decidido.

## Siguientes pasos {#whats-next}

Ahora que ha completado esta parte del recorrido para desarrolladores de AEM sin encabezado, debería poder hacer lo siguiente:

* Comprenda las API de AEM disponibles.
* Comprenda cómo se admiten los fragmentos de contenido en estas API.

Debe continuar con su recorrido sin encabezado AEM revisando a continuación el documento [Cómo ponerlo todo junto: su aplicación y su contenido en AEM sin encabezado](put-it-all-together.md) donde se familiarizará con los conceptos básicos de la arquitectura de AEM y las herramientas que necesita utilizar para montar su aplicación.

## Recursos adicionales {#additional-resources}

* [API de Adobe Experience Manager as a Cloud Service](https://developer.adobe.com/experience-cloud/experience-manager-apis/)
* [API de AEM para la entrega y administración de contenido estructurado](/help/headless/apis-headless-and-content-fragments.md)
* [REST OpenAPI de AEM para la entrega de fragmentos de contenido](/help/headless/aem-rest-openapi-content-fragment-delivery.md)
* [API de AEM GraphQL para la entrega de fragmentos de contenido](/help/headless/graphql-api/content-fragments.md)
* [Fragmentos de contenido y modelos de fragmentos de contenido OpenAPI](/help/headless/content-fragment-openapis.md)
* [Compatibilidad con fragmentos de contenido en la API HTTP de AEM Assets](/help/assets/content-fragments/assets-api-content-fragments.md)
* [Trabajar con fragmentos de contenido](/help/sites-cloud/administering/content-fragments/overview.md)
* [Componentes principales de AEM](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=es)
* [Explicación de CORS/AEM](https://helpx.adobe.com/experience-manager/kt/platform-repository/using/cors-security-article-understand.html?lang=es)
* [Vídeo: Desarrollo para CORS con AEM](https://helpx.adobe.com/experience-manager/kt/platform-repository/using/cors-security-technical-video-develop.html?lang=es)
* [Introducción a AEM como CMS sin encabezado](/help/headless/introduction.md)
* [Portal para desarrolladores de AEM](https://experienceleague.adobe.com/landing/experience-manager/headless/developer.html?lang=es)
* [Tutoriales de AEM sin encabezado](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/overview.html?lang=es)
