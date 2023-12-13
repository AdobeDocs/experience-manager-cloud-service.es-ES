---
title: Solución de problemas de consultas persistentes de GraphQL
description: Obtenga información sobre cómo solucionar problemas con consultas de GraphQL persistentes en Adobe Experience Manager as a Cloud Service.
feature: Content Fragments,GraphQL API
source-git-commit: c8ea9846600d1773e6f269973635f5338f31906f
workflow-type: tm+mt
source-wordcount: '353'
ht-degree: 0%

---


# Solucionar problemas de consultas de GraphQL persistentes {#troubleshoot-persisted-graphql-queries}

El [Centro de acciones](/help/operations/actions-center.md) incluye el **Error de consulta persistente de GraphQL** alerta. Esto significa que se le informará cada vez que una de las consultas persistentes de GraphQL genere un error.

Para ayudarle a solucionar y resolver estos problemas, explicamos la *más común* causas de los errores y pasos para solucionarlos.

## Cambios en el modelo de fragmento de contenido {#changes-to-content-fragment-model}

Una consulta persistente de GraphQL puede fallar cuando se basa en tipos de GraphQL obsoletos, a menudo debido a un cambio en los modelos de fragmento de contenido subyacentes.

Esto puede ocurrir por varias razones. Por ejemplo, cuando un autor de modelo de contenido:

* quita un campo o cambia su nombre
* actualiza los modelos permitidos definidos para una referencia de fragmento
* cancela la publicación de un modelo al que hacen referencia otros modelos
* otras acciones y motivos

Para solucionarlo, haga lo siguiente:

* la consulta persistente que da error debe actualizarse para dar cabida al cambio en el modelo de fragmento de contenido
* o el cambio en el modelo que introdujo el problema debería revertirse

## Extremo de GraphQL no configurado {#graphql-endpoint-not-configured}

Cuando las consultas persistentes devuelven el `400` o `500` código de error, junto con la información `No suitable endpoint found`, esto significa que no hay ningún extremo de GraphQL AEM configurado en el entorno de la.

Para corregir esto, siga los pasos para habilitar y publicar el extremo desde [Administrar puntos finales de GraphQL AEM en la administración de](/help/headless/graphql-api/graphql-endpoint.md).

## Falta ruta en la URL de la consulta persistente de GraphQL {#missing-path-query-url}

Si las consultas persistentes devuelven el `400` o `500` código de error con la información `Suffix: '/' does not contain a path`, se llama al servlet de GraphQL sin un sufijo de ruta.

El patrón debe ser `/graphql/execute.json/thePath`.

## Bloqueado debido a una lista de permitidos de IP {#blocked-due-to-ip-allow-list}

En tal caso, la consulta devuelve el valor `405` código de error.

No se trata de algo específico de GraphQL. Consulte el artículo de KB [Error 405 no permitido](https://experienceleague.adobe.com/docs/experience-cloud-kcs/kbarticles/KA-20824.html).

## Bloqueado por Dispatcher {#blocked-dispatcher}

Si el extremo de GraphQL devuelve el `404` error al publicar para `POST` , significa que las consultas de GraphQL se bloquean en el nivel de dispatcher y el punto de conexión debe habilitarse manualmente.

Este no debería ser el caso de forma predeterminada, pero una configuración personalizada de Dispatcher podría causar este problema. Ver más en [AEM Dispatcher: configuración de extremo con encabezado sin encabezado de](/help/headless/deployment/dispatcher.md).
