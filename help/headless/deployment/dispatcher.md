---
title: Configuración de Dispatcher con AEM Headless
description: Dispatcher es una capa de almacenamiento en caché y seguridad situada frente a los entornos de publicación de Adobe Experience Manager. Se utilizan varias configuraciones para abrir puntos de conexión de GraphQL en aplicaciones sin encabezado.
feature: Dispatcher, GraphQL API
exl-id: 78a20021-910f-4cf0-87bf-6e2223994f76
source-git-commit: 9bfb5bc4b340439fcc34e97f4e87d711805c0d82
workflow-type: ht
source-wordcount: '233'
ht-degree: 100%

---

# Configuración de Dispatcher con AEM Headless

[Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html?lang=es) es una capa de almacenamiento en caché y seguridad delante de los entornos de publicación de Adobe Experience Manager. De forma predeterminada, se incluyen varias configuraciones para abrir los puntos de conexión de GraphQL en aplicaciones sin encabezado.

>[!NOTE]
>
>Para obtener documentación detallada acerca de Dispatcher, consulte la [Guía de Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html?lang=es)

Como parte de un proyecto de AEM, se incluye un módulo de Dispatcher que contiene configuraciones para Dispatcher. Los proyectos recién generados a partir del [Tipo de archivo del proyecto de AEM](https://github.com/adobe/aem-project-archetype) incluyen automáticamente [filtros](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=es?#defining-a-filter) que habilitan los puntos de conexión de GraphQL.

## Puntos de conexión de GraphQL

Como parte de los filtros predeterminados, los [puntos de conexión de GraphQL](/help/headless/graphql-api/graphql-endpoint.md) se abren con la siguiente regla:

```
/0060 { /type "allow" /method '(POST|OPTIONS)' /url "/content/_cq_graphql/*/endpoint.json" }
```

La comodín `*` abre varios puntos de conexión en la instancia de AEM. La consulta mediante un punto de conexión de GraphQL se realizará mediante `POST` y la respuesta **no** se almacena en caché.

## Consultas persistentes de GraphQL

La solicitud de consultas persistentes se realiza con un punto de conexión diferente. Como parte de la configuración de filtro predeterminada, la dirección URL de [Consultas persistentes](/help/headless/graphql-api/persisted-queries.md) se abre con la siguiente regla:

```
/0061 { /type "allow" /method '(GET|POST|OPTIONS)' /url "/graphql/execute.json*" }
```

Las consultas persistentes se pueden solicitar utilizando `GET`, por lo que se almacena en caché así la respuesta en el nivel de Dispatcher y de la red de distribución de contenido (CDN). Se pueden encontrar más detalles acerca del almacenamiento en caché e invalidación de caché [aquí](/help/implementing/dispatcher/caching.md).
