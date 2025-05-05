---
title: Solución de problemas de consultas persistentes de GraphQL
description: Obtenga información sobre cómo solucionar problemas con consultas de GraphQL persistentes en Adobe Experience Manager as a Cloud Service.
feature: Headless, Content Fragments,GraphQL API
exl-id: 71bd1f68-ca96-4c78-a936-abed250ecec1
role: Admin, Developer
source-git-commit: bdf3e0896eee1b3aa6edfc481011f50407835014
workflow-type: tm+mt
source-wordcount: '363'
ht-degree: 0%

---

# Solucionar problemas de consultas de GraphQL persistentes {#troubleshoot-persisted-graphql-queries}

El [Centro de acciones](/help/operations/actions-center.md) incluye la alerta **Error de consulta persistente de GraphQL**. Esto significa que se le informará cada vez que una de las consultas persistentes de GraphQL genere un error.

Para ayudarle a solucionar estos problemas, esta página describe las *causas más comunes* de errores y los pasos para solucionarlos.

## Cambios en el modelo de fragmento de contenido {#changes-to-content-fragment-model}

Una consulta persistente de GraphQL puede fallar cuando se basa en tipos de GraphQL obsoletos, a menudo debido a un cambio en los modelos de fragmento de contenido subyacentes.

Estos errores pueden ocurrir por diversas razones. Algunos ejemplos son (la lista no es exhaustiva), cuando el autor de un modelo de fragmento de contenido:

* quita un campo o cambia su nombre
* actualiza el **Tipo de modelo** que define los modelos permitidos para la referencia de fragmento
* cancela la publicación de un modelo al que hacen referencia otros modelos

Para solucionar estos errores, debe:

* actualizar la consulta persistente que no admite los cambios realizados en el modelo de fragmento de contenido
* revierta el cambio en el modelo que introdujo el problema

## Extremo de GraphQL no configurado {#graphql-endpoint-not-configured}

Cuando las consultas persistentes devuelven el código de error `404`, junto con la información `No suitable endpoint found`, significa que no se ha configurado ningún extremo de GraphQL AEM en el entorno de.

Para corregir esto, siga los pasos para habilitar y publicar el extremo desde [Administrar extremos de GraphQL AEM en la página de inicio de sesión de &lbrace;100000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000](/help/headless/graphql-api/graphql-endpoint.md)

## Falta ruta en la URL de la consulta persistente de GraphQL {#missing-path-query-url}

Si las consultas persistentes devuelven el código de error `400` con la información `Suffix: '/' does not contain a path`, se llama al servlet de GraphQL sin un sufijo de ruta de acceso.

El patrón debe ser `/graphql/execute.json/thePath`.

## Bloqueado debido a una lista de permitidos de IP {#blocked-due-to-ip-allow-list}

En tal caso, la consulta devuelve el código de error `405`.

Este error no es algo específico de GraphQL. Consulte el artículo de la BC [Error 405 no permitido](https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-20824).

## Bloqueado por Dispatcher {#blocked-dispatcher}

Si el extremo de GraphQL devuelve el error `404` al publicar para `POST` solicitudes, significa que las consultas de GraphQL están bloqueadas en el nivel de Dispatcher y que el extremo debe habilitarse manualmente.

Este no debería ser el caso de forma predeterminada, pero una configuración personalizada de Dispatcher podría causar este problema. Ver más en [Dispatcher AEM: configuración de extremo con encabezado sin encabezado](/help/headless/deployment/dispatcher.md).
