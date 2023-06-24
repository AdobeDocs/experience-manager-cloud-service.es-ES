---
title: Autenticación para consultas de AEM de GraphQL remotas en fragmentos de contenido
description: Comprenda la autenticación necesaria para las consultas de Adobe Experience Manager GraphQL remotas a fin de proteger la entrega de contenido sin encabezado.
feature: Content Fragments,GraphQL API
exl-id: dfeae661-06a1-4001-af24-b52ae12d625f
source-git-commit: 7260649eaab303ba5bab55ccbe02395dc8159949
workflow-type: tm+mt
source-wordcount: '230'
ht-degree: 26%

---

# Autenticación para consultas de AEM de GraphQL remotas en fragmentos de contenido {#authentication-for-remote-aem-graphql-queries-on-content-fragments}

Un caso de uso principal para [API de Adobe Experience Manager as a Cloud Service AEM () GraphQL para la entrega de fragmentos de contenido](/help/headless/graphql-api/content-fragments.md) es aceptar consultas remotas desde aplicaciones o servicios de terceros. Estas consultas remotas pueden requerir acceso a API autenticado para asegurar la entrega de contenido sin encabezado.

>[!NOTE]
>
>AEM Para pruebas y desarrollo, también puede acceder a la API de GraphQL de la directamente mediante el [Interfaz de GraphiQL](/help/headless/graphql-api/graphiql-ide.md).

Para la autenticación, el servicio de terceros debe [recuperar un token de acceso](#retrieving-access-token) que luego puede ser [se utiliza en la petición GraphQL](#use-access-token-in-graphql-request).

## Recuperación de un token de acceso {#retrieving-access-token}

Consulte [Generación de tokens de acceso para las API del lado del servidor](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md) para obtener información detallada.

## Uso del token de acceso en una solicitud de GraphQL {#use-access-token-in-graphql-request}

AEM Para que un servicio de terceros se conecte con una instancia de, debe tener un *Token de acceso*. A continuación, el servicio debe añadir este token al encabezado `Authorization` en la petición POST.

Por ejemplo, un encabezado de autorización de GraphQL:

```xml
Authorization: Bearer <access_token>
```

## Requisitos de permisos {#permission-requirements}

Se realizan todas las solicitudes realizadas con el token de acceso *por la cuenta de usuario que generó el token*.

Esta cuenta de usuario significa que debe comprobar que la cuenta tiene los permisos necesarios para ejecutar consultas de GraphQL.

Puede comprobar estos permisos utilizando GraphiQL en la instancia local. Más detalles acerca de [los permisos se pueden encontrar aquí](/help/headless/security/permissions.md).
