---
title: AEM API abierta de REST para la entrega de fragmentos de contenido
description: AEM Obtenga información acerca de la API abierta de REST para la entrega de fragmentos de contenido
feature: Headless, Content Fragments, Edge Delivery Services
role: Admin, Developer
source-git-commit: d98aa9d206486022d465ca19c8888088562d56c3
workflow-type: tm+mt
source-wordcount: '346'
ht-degree: 0%

---


# AEM API abierta de REST para la entrega de fragmentos de contenido {#aem-rest-openapi-for-content-fragment-delivery}

>[!IMPORTANT]
>
>Esta API está disponible a través del Programa de usuarios que la adoptaron por anticipado.
>
>Para ver el estado y cómo solicitarlo si está interesado, consulte las [Notas de la versión](/help/release-notes/release-notes-cloud/release-notes-current.md).

En Adobe Experience Manager AEM () as a Cloud Service AEM, la API abierta de REST para la entrega de fragmentos de contenido es la siguiente:

* AEM es una API HTTP REST en [Edge Delivery Services](/help/edge/overview.md), diseñada para entregar contenido estructurado de fragmentos de contenido en formato JSON
* ofrece una integración de CDN moderna que permite la invalidación de contenido activo
* se centra en la entrega de contenido (rendimiento, escalabilidad, integración de CDN, control JSON optimizado y salida)
* incluye la capacidad de hidratar JSON para fragmentos y recursos a los que se hace referencia

Esta API:

* es el sucesor de [Compatibilidad con fragmentos de contenido en la API HTTP de AEM Assets](/help/assets/content-fragments/assets-api-content-fragments.md)

* complementa las [API abiertas de fragmentos de contenido y modelos de fragmentos de contenido](/help/headless/content-fragment-openapis.md), que le permiten administrar los fragmentos de contenido y los modelos de fragmentos de contenido (CRUD)

* AEM es una alternativa HTTP REST a la API de GraphQL [para su uso con fragmentos de contenido](/help/headless/graphql-api/content-fragments.md)

Para obtener documentación completa, consulte [Esquemas de API de AEM Sites: API de entrega de fragmentos de contenido (experimental 2024.07)](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/sites/delivery/).

>[!NOTE]
>
>AEM Consulte [API de para la administración y entrega de contenido estructurado](/help/headless/apis-headless-and-content-fragments.md) para obtener una descripción general de las diversas API disponibles y una comparación de algunos de los conceptos involucrados.

## Almacenamiento en caché {#caching}

AEM AEM Se integra con la red de distribución de contenido (CDN) de. Esto significa que las respuestas JSON servidas en el nivel de publicación se almacenan en caché en el nivel de Fastly.

Las respuestas se almacenan en caché, en función de encabezados de almacenamiento en caché predefinidos (no se puede configurar):

* Las respuestas se almacenan en caché durante 5 minutos en la caché del explorador o cliente
   * `max-age`=`300`
* Las respuestas se almacenan en caché durante 1 hora en la caché de la CDN
   * `s-maxage`=`3600`
* El contenido obsoleto se puede servir mientras se revalidan las nuevas solicitudes durante un máximo de 1 hora
   * `stale-while-revalidate`=`3600`
* El contenido antiguo se puede proporcionar, por error, durante un máximo de 1 día
   * `stale-on-error`=`86400`

AEM También viene con la invalidación activa de la caché de la CDN. Esto significa que cada vez que se actualiza o publica contenido, las respuestas de la API abierta de JSON correspondientes se invalidan automáticamente, a través de una solicitud de depuración suave a Fastly. Esto le permite ver los cambios reflejados en la salida JSON antes de que se alcance la página real de la caché de la CDN (`s-maxage`).