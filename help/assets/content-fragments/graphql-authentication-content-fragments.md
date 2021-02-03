---
title: Autenticación para Consultas GraphQL de AEM remoto en fragmentos de contenido
description: Obtenga información sobre la autenticación necesaria para las consultas de Remote AEM GraphQL.
translation-type: tm+mt
source-git-commit: 42ca0c70f7018a6e3c9be68ef13adefafc987864
workflow-type: tm+mt
source-wordcount: '217'
ht-degree: 0%

---


# Autenticación para Consultas GraphQL de AEM remoto en fragmentos de contenido {#authentication-for-remote-aem-graphql-queries-on-content-fragments}

Un caso de uso principal para [Adobe Experience Manager como Cloud Service (AEM) GraphQL API para el Envío de fragmentos de contenido](/help/assets/content-fragments/graphql-api-content-fragments.md) es aceptar consultas remotas de aplicaciones o servicios de terceros.  Estas consultas remotas pueden requerir acceso a API autenticado.

>[!NOTE]
>
>Para pruebas y desarrollo también puede acceder a la API de GraphQL de AEM directamente mediante la interfaz [GraphiQL](/help/assets/content-fragments/graphql-api-content-fragments.md#graphiql-interface).

Para la autenticación, el servicio de terceros necesita utilizar un [Token de acceso](#access-token), que luego se puede [utilizar en la solicitud de GraphQL](#use-access-token-in-graphql-request).

## Recuperación de un Token de acceso {#retrieving-access-token}

Consulte [Generación de Tokenes de acceso para las API del servidor](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md) para obtener más información.

## Uso del Token de acceso en una solicitud de GraphQL {#use-access-token-in-graphql-request}

Para que un servicio de terceros se conecte con una instancia de AEM, debe tener un *Token de acceso*. El servicio debe agregar este token al encabezado `Authorization` en la solicitud del POST.

Por ejemplo, un encabezado de autorización de GraphQL:

```xml
Authorization: Bearer <access_token>
```

## Requisitos de permisos {#permission-requirements}

Todas las solicitudes realizadas con el token de acceso serán realizadas *por la cuenta de usuario que generó el token*.

Esto significa que debe comprobar que la cuenta tiene los permisos necesarios para ejecutar consultas de GraphQL.

Puede comprobarlo mediante GraphiQL en la instancia local.
