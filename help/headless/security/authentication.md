---
title: Autenticación para consultas de AEM de GraphQL remotas en fragmentos de contenido
description: AEM Comprenda la autenticación necesaria para las consultas de GraphQL de remoto para proteger la entrega de contenido sin encabezado.
feature: Content Fragments,GraphQL API
exl-id: dfeae661-06a1-4001-af24-b52ae12d625f
source-git-commit: bceec9ea6858b1c4c042ecd96f13ae5cac1bbee5
workflow-type: tm+mt
source-wordcount: '235'
ht-degree: 88%

---

# Autenticación para consultas de AEM de GraphQL remotas en fragmentos de contenido {#authentication-for-remote-aem-graphql-queries-on-content-fragments}

Un caso de uso principal para la [API de Adobe Experience Manager as a Cloud Service (AEM) de GraphQL para la entrega de fragmentos de contenido](/help/headless/graphql-api/content-fragments.md) es aceptar consultas remotas desde aplicaciones o servicios de terceros. Estas consultas remotas pueden requerir acceso a API autenticado para asegurar la entrega de contenido sin encabezado.

>[!NOTE]
>
>Para pruebas y desarrollo, también puede acceder a la API de GraphQL de AEM directamente mediante la [Interfaz de GraphiQL](/help/headless/graphql-api/graphiql-ide.md).

Para la autenticación, el servicio de terceros debe [recuperar un token de acceso](#retrieving-access-token), que entonces se puede [utilizar en la solicitud de GraphQL](#use-access-token-in-graphql-request).

## Recuperación de un token de acceso {#retrieving-access-token}

Consulte [Generación de tokens de acceso para las API del servidor](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md) para obtener más información.

## Uso del token de acceso en una solicitud de GraphQL {#use-access-token-in-graphql-request}

Para que un servicio de terceros se conecte con una instancia de AEM, debe tener un *token de acceso*. A continuación, el servicio debe añadir este token al encabezado `Authorization` en la petición POST.

Por ejemplo, un encabezado de autorización de GraphQL:

```xml
Authorization: Bearer <access_token>
```

## Requisitos de permisos {#permission-requirements}

Todas las solicitudes realizadas con el token de acceso las realizará en realidad *la cuenta de usuario que generó el token*.

Esto significa que debe comprobar que la cuenta tiene los permisos necesarios para ejecutar consultas de GraphQL.

Puede comprobarlo utilizando GraphiQL en la instancia local. Más detalles acerca de [los permisos se pueden encontrar aquí](/help/headless/security/permissions.md).
