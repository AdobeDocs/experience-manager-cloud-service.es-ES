---
title: Actualización del contenido mediante las API de AEM
description: En esta parte del recorrido para desarrolladores de contenido de AEM sin encabezado, descubra cómo utilizar las API disponibles para acceder y actualizar el contenido de sus fragmentos de contenido.
exl-id: 84120856-fd1d-40f7-8df4-73d4cdfcc43b
solution: Experience Manager
feature: Headless, Content Fragments, GraphQL API
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '503'
ht-degree: 99%

---

# Actualización del contenido mediante las API de AEM {#update-your-content}

En esta parte del [Recorrido para desarrolladores de contenido de AEM sin encabezado](overview.md), descubra cómo utilizar las API disponibles para acceder y actualizar el contenido de los fragmentos de contenido.

## Lo que hemos visto hasta ahora {#story-so-far}

En el documento anterior del recorrido de AEM sin encabezado, [Cómo acceder al contenido a través de las API de entrega de AEM](access-your-content.md), aprendió a acceder al contenido sin encabezado en AEM mediante la API de GraphQL de AEM, por lo que ahora debería poder hacer lo siguiente:

* Tener conocimientos avanzados de GraphQL.
* Comprender cómo funciona la API de GraphQL de AEM.
* Comprender algunos ejemplos prácticos de consultas.

Este artículo se basa en estos aspectos básicos para que pueda comprender cómo actualizar el contenido sin encabezado existente en AEM a través de las API disponibles.

## Objetivo {#objective}

* **Público**: avanzados
* **Objetivo**: aprender a utilizar las API disponibles para acceder y actualizar el contenido de los fragmentos de contenido.

## API de AEM para su uso con fragmentos de contenido {#aem-apis-for-use-with-content-fragments}

Adobe Experience Manager (AEM) as a Cloud Service ofrece varias API para la entrega de contenido estructurado desde fragmentos de contenido hasta su administración. Consulte las páginas individuales para obtener más información sobre las API específicas.

* Envío de fragmentos de contenido de AEM con OpenAPI
   * Esta API crea respuestas JSON para ofrecer contenido estructurado a partir de fragmentos de contenido en AEM.
   * Utiliza una ruta a un fragmento de contenido como punto final.
   * Esta API se basa en REST.
   * Está optimizada para la entrega de contenido, incluida la integración de CDN.
* API de GraphQL de AEM para la entrega de fragmentos de contenido
   * Esta API está basada en esquemas. Los esquemas de API están representados por modelos de fragmentos de contenido, que definen la estructura de contenido.
   * Esta API está basada en GraphQL.
* Fragmentos de contenido y OpenAPI de fragmentos de contenido y modelos
   * Estas API están pensadas para la administración de contenido estructurado.
   * Los respectivos operadores de GET no están optimizados para la entrega de contenido.
   * Esta API se basa en REST.

>[!NOTE]
>
>[La compatibilidad con fragmentos de contenido en la API HTTP de Assets](/help/assets/content-fragments/assets-api-content-fragments.md) ya está [obsoleta](/help/release-notes/deprecated-removed-features.md). Se ha reemplazado por [Envío de fragmentos de contenido con OpenAPI](/help/headless/aem-content-fragment-delivery-with-openapi.md) junto con [API para la administración de fragmentos de contenido y de modelos de fragmentos de contenido](/help/headless/content-fragment-openapis.md).

## Siguientes pasos {#whats-next}

Ahora que ha completado esta parte del recorrido para desarrolladores de AEM sin encabezado, debería poder hacer lo siguiente:

* Comprender las API de AEM disponibles.
* Comprender cómo se admiten los fragmentos de contenido en estas API.

Debe continuar con su recorrido sin encabezado AEM revisando a continuación el documento [Cómo ponerlo todo junto: su aplicación y su contenido en AEM sin encabezado](put-it-all-together.md) donde se familiarizará con los conceptos básicos de la arquitectura de AEM y las herramientas que necesita utilizar para montar su aplicación.

## Recursos adicionales {#additional-resources}

* [API de Adobe Experience Manager as a Cloud Service](https://developer.adobe.com/experience-cloud/experience-manager-apis/)
* [API de AEM para la entrega y administración de contenido estructurado](/help/headless/apis-headless-and-content-fragments.md)
* [Envío de fragmentos de contenido de AEM con OpenAPI](/help/headless/aem-content-fragment-delivery-with-openapi.md)
* [API de GraphQL de AEM para la entrega de fragmentos de contenido](/help/headless/graphql-api/content-fragments.md)
* [Fragmentos de contenido y OpenAPI de fragmentos de contenido y modelos](/help/headless/content-fragment-openapis.md)
* [Compatibilidad con fragmentos de contenido en la API HTTP de AEM Assets](/help/assets/content-fragments/assets-api-content-fragments.md)
* [Trabajar con fragmentos de contenido](/help/sites-cloud/administering/content-fragments/overview.md)
* [Componentes principales de AEM](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=es)
* [Explicación de CORS/AEM](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/security/understand-cross-origin-resource-sharing.html)
* [Vídeo: Desarrollo para CORS con AEM](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/security/develop-for-cross-origin-resource-sharing.html)
* [Introducción a AEM como CMS sin encabezado](/help/headless/introduction.md)
* [Portal para desarrolladores de AEM](https://experienceleague.adobe.com/landing/experience-manager/headless/developer.html?lang=es)
* [Tutoriales de AEM sin encabezado](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/overview.html?lang=es)
