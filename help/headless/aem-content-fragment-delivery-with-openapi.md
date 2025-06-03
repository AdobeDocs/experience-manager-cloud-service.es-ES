---
title: Envío de fragmentos de contenido de AEM con OpenAPI
description: Obtenga información acerca de la entrega de fragmentos de contenido de AEM con OpenAPI
feature: Headless, Content Fragments, Edge Delivery Services
role: Admin, Developer
exl-id: b298db37-1033-4849-bc12-7db29fb77777
source-git-commit: 1995c84bb669fd52ecd53c7e695acc518a5226e8
workflow-type: tm+mt
source-wordcount: '475'
ht-degree: 3%

---


# Envío de fragmentos de contenido de AEM con OpenAPI {#aem-content-fragment-delivery-with-openapi}

En Adobe Experience Manager (AEM) as a Cloud Service, la API abierta de AEM para la entrega de fragmentos de contenido:

* es una API abierta optimizada para la entrega en directo de fragmentos de contenido de AEM en formato JSON
* ofrece una integración de CDN moderna que permite la invalidación de contenido activo
* se centra en la entrega de contenido (rendimiento, escalabilidad, integración de CDN, control JSON optimizado y salida)
* incluye la capacidad de hidratar JSON para fragmentos y recursos a los que se hace referencia

Esta API:

* es el sucesor de [Compatibilidad con fragmentos de contenido en la API HTTP de AEM Assets](/help/assets/content-fragments/assets-api-content-fragments.md)

* complementa las [API abiertas de fragmentos de contenido y modelos de fragmentos de contenido](/help/headless/content-fragment-openapis.md), que le permiten administrar los fragmentos de contenido y los modelos de fragmentos de contenido (CRUD)

* es una alternativa HTTP REST a la [API GraphQL de AEM para su uso con fragmentos de contenido](/help/headless/graphql-api/content-fragments.md)

Para obtener documentación completa, consulte [Entrega de fragmentos de contenido de AEM con OpenAPI](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/contentfragments/delivery/).

>[!NOTE]
>
>Consulte [API de AEM para la administración y entrega de contenido estructurado](/help/headless/apis-headless-and-content-fragments.md) para obtener una descripción general de las diversas API disponibles y una comparación de algunos de los conceptos involucrados.

>[!IMPORTANT]
>
>Para habilitar la entrega de fragmentos de contenido con OpenAPI en AEM as a Cloud Service, asegúrese de que aún no esté habilitada y, a continuación, envíe un ticket de asistencia de Adobe con el título **Habilitar la entrega de fragmentos de contenido con OpenAPI** y especificando:
>
>* los ID de programa y entorno de Cloud Service
>* Detalles del caso de uso que desea resolver con la API de envío de fragmentos de contenido
>* detalles de todos los contactos a los que Adobe debe responder, y mantenerse informado sobre la solicitud, y el proyecto (si es necesario)

## Almacenamiento en caché {#caching}

AEM se integra fácilmente con la CDN de AEM. Esto significa que las respuestas JSON servidas en el nivel de publicación se almacenan en caché en el nivel de Fastly.

Las respuestas se almacenan en caché, en función de encabezados de almacenamiento en caché predefinidos (no se puede configurar):

* Las respuestas se almacenan en caché durante 5 minutos en la caché del explorador o cliente
   * `max-age`=`300`
* Las respuestas se almacenan en caché durante 1 hora en la caché de la CDN
   * `s-maxage`=`3600`
* El contenido obsoleto se puede servir mientras se revalidan las nuevas solicitudes durante un máximo de 1 hora
   * `stale-while-revalidate`=`3600`
* El contenido antiguo se puede proporcionar, por error, durante un máximo de 1 día
   * `stale-on-error`=`86400`

La entrega de fragmentos de contenido con OpenAPI admite la invalidación activa de la caché de la CDN. Esto significa que cada vez que se actualiza o publica contenido, las respuestas de la API abierta de JSON correspondientes se invalidan automáticamente, a través de una solicitud de depuración suave a Fastly. Esto le permite ver los cambios reflejados en la salida JSON antes de que se alcance la página real de la caché de la CDN (`s-maxage`).

## Disponibilidad {#availability}

La Entrega de fragmentos de contenido con OpenAPI está disponible en los niveles de Previsualización y Publicación. La API abierta ofrece fragmentos de contenido en formato JSON, tanto para la vista previa como para la entrega en directo.

Para obtener una vista previa, la Entrega de fragmentos de contenido con OpenAPI puede:

* publicar para previsualización
* habilitar el acceso a la vista previa con lista de permitidos IP
* obtener la URL de vista previa

## CORS {#cors}

[orígenes permitidos de CORS](/help/headless/deployment/cross-origin-resource-sharing.md) definen los orígenes que pueden llamar a la API.

Esta API no tiene en cuenta los orígenes permitidos de CORS definidos en el lado de la configuración de Dispatcher, específicamente para GraphQL.

<!-- 
## API Rate Limits {#api-rate-limits}
-->

<!-- 
## Limitations {#limitations}
-->
