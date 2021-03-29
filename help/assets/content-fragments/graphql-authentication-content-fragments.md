---
title: Autenticación para consultas de GraphQL remotas en fragmentos de contenido
description: Comprenda la autenticación necesaria para las consultas de Remote AEM GraphQL a fin de proteger la entrega de contenido sin encabezado.
translation-type: tm+mt
source-git-commit: e7ca6dc841ba777384be74021a27d523d530a956
workflow-type: tm+mt
source-wordcount: '231'
ht-degree: 0%

---


# Autenticación para consultas de GraphQL remotas en fragmentos de contenido {#authentication-for-remote-aem-graphql-queries-on-content-fragments}

Un caso de uso principal de la API de [Adobe Experience Manager as a Cloud Service (AEM) GraphQL para la entrega de fragmentos de contenido](/help/assets/content-fragments/graphql-api-content-fragments.md) es aceptar consultas remotas desde aplicaciones o servicios de terceros. Estas consultas remotas pueden requerir acceso a API autenticado para asegurar la entrega de contenido sin encabezado.

>[!NOTE]
>
>Para pruebas y desarrollo también puede acceder a la API de AEM GraphQL directamente mediante la interfaz [GraphiQL interface](/help/assets/content-fragments/graphql-api-content-fragments.md#graphiql-interface).

Para la autenticación, el servicio de terceros debe utilizar un [Token de acceso](#access-token), que luego puede [utilizarse en la solicitud de GraphQL](#use-access-token-in-graphql-request).

## Recuperación de un token de acceso {#retrieving-access-token}

Consulte [Generación de tokens de acceso para API del servidor](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md) para obtener más información.

## Uso del token de acceso en una solicitud de GraphQL {#use-access-token-in-graphql-request}

Para que un servicio de terceros se conecte con una instancia de AEM, debe tener un *Token de acceso*. El servicio debe agregar este token al encabezado `Authorization` en la solicitud del POST.

Por ejemplo, un encabezado de autorización de GraphQL:

```xml
Authorization: Bearer <access_token>
```

## Requisitos de permisos {#permission-requirements}

Todas las solicitudes realizadas con el token de acceso se realizarán *mediante la cuenta de usuario que generó el token*.

Esto significa que debe comprobar que la cuenta tiene los permisos necesarios para ejecutar consultas de GraphQL.

Puede comprobarlo utilizando GraphiQL en la instancia local.
