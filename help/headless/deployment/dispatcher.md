---
title: Configuración de extremo de Dispatcher con AEM Headless
description: Dispatcher es una capa de almacenamiento en caché y filtrado de acceso delante de los entornos de publicación de Adobe Experience Manager. Se utilizan varias configuraciones para abrir puntos de conexión de GraphQL en aplicaciones sin encabezado.
feature: Headless, Dispatcher, GraphQL API
exl-id: 78a20021-910f-4cf0-87bf-6e2223994f76
role: Admin, Developer
source-git-commit: ecf3f0ac54acf4ac772d2906fa0b26d283549929
workflow-type: tm+mt
source-wordcount: '306'
ht-degree: 61%

---


# Dispatcher: Configuración de extremo con AEM Headless

[Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html?lang=es) es una capa de almacenamiento en caché y filtrado de acceso delante de los entornos de publicación de Adobe Experience Manager. De forma predeterminada, se incluyen varias configuraciones para abrir los puntos de conexión de GraphQL en aplicaciones sin encabezado.

>[!IMPORTANT]
>
>Las reglas de filtro de Dispatcher son controles de filtrado de acceso, no sustituyen al control de acceso basado en ACL de JCR en la instancia de publicación. La instancia de publicación debe estar segura independientemente de la configuración de Dispatcher. Asegúrese de que los recursos confidenciales estén protegidos mediante la denegación de `jcr:read` para las entidades de seguridad `everyone` y `anonymous` en el nivel de repositorio, independientemente de la configuración del filtro de Dispatcher.

>[!NOTE]
>
>Para obtener documentación detallada acerca de Dispatcher, consulte la [Guía de Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html?lang=es).

Como parte de un proyecto de AEM, se incluye un módulo de Dispatcher que contiene configuraciones para Dispatcher. Los proyectos recién generados a partir del [Tipo de archivo del proyecto de AEM](https://github.com/adobe/aem-project-archetype) incluyen automáticamente [filtros](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=es?#defining-a-filter) que habilitan los puntos finales de GraphQL.

## Puntos finales de GraphQL

Como parte de los filtros predeterminados, los [puntos de conexión de GraphQL](/help/headless/graphql-api/graphql-endpoint.md) se abren con la siguiente regla:

```
/0060 { /type "allow" /method '(POST|OPTIONS)' /url "/content/_cq_graphql/*/endpoint.json" }
```

La comodín `*` abre varios puntos de conexión en la instancia de AEM. La consulta mediante un punto final de GraphQL se realiza mediante `POST` y la respuesta **no** se almacena en la caché.

## Consultas persistentes de GraphQL

La solicitud de consultas persistentes se realiza con un punto final diferente. Como parte de la configuración de filtro predeterminada, la dirección URL de [Consultas persistentes](/help/headless/graphql-api/persisted-queries.md) se abre con la siguiente regla:

```
/0061 { /type "allow" /method '(GET|POST|OPTIONS)' /url "/graphql/execute.json*" }
```

Las consultas persistentes se pueden solicitar mediante `GET`, almacenando en caché la respuesta en el nivel de Dispatcher y de la red de distribución de contenido (CDN). Encontrará más detalles sobre el almacenamiento en caché y la invalidación de caché en [la Introducción al almacenamiento en caché en AEM as a Cloud Service](/help/implementing/dispatcher/caching.md).
