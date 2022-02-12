---
title: Configuración de Dispatcher con AEM sin encabezado
description: Dispatcher es una capa de almacenamiento en caché y seguridad situada frente a los entornos de publicación de Adobe Experience Manager. Se utilizan varias configuraciones para abrir extremos de GraphQL en aplicaciones sin encabezado.
feature: Dispatcher, GraphQL API
source-git-commit: 0cc131209f497241949f8da6e8144dfcaffe7e6e
workflow-type: tm+mt
source-wordcount: '233'
ht-degree: 6%

---


# Configuración de Dispatcher con AEM sin encabezado

La variable [Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html?lang=es) es una capa de almacenamiento en caché y seguridad delante de los entornos de publicación de Adobe Experience Manager. De forma predeterminada, se incluyen varias configuraciones para abrir los extremos de GraphQL en aplicaciones sin encabezado.

>[!NOTE]
>
>Para obtener documentación detallada sobre Dispatcher, consulte la [Guía de Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html)

Como parte de un proyecto AEM, se incluye un módulo de Dispatcher que contiene configuraciones para Dispatcher. Proyectos recién generados a partir de la variable [Tipo de archivo del proyecto AEM](https://github.com/adobe/aem-project-archetype) incluye automáticamente [filtros](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?#defining-a-filter) que habilita los extremos de GraphQL.

## Extremos de GraphQL

Como parte de los filtros predeterminados, [Extremos de GraphQL](/help/headless/graphql-api/graphql-endpoint.md) se abren con la siguiente regla:

```
/0060 { /type "allow" /method '(POST|OPTIONS)' /url "/content/_cq_graphql/*/endpoint.json" }
```

La variable `*` comodín abre varios extremos en la instancia de AEM. La consulta mediante un extremo de GraphQL se realizará mediante `POST` y la respuesta **not** se almacenan en caché.

## Consultas persistentes de GraphQL

La solicitud de consultas persistentes se realiza con un extremo diferente. Como parte de la configuración de filtro predeterminada, la dirección url de [Consultas persistentes](/help/headless/graphql-api/persisted-queries.md) se abren con la siguiente regla:

```
/0061 { /type "allow" /method '(GET|POST|OPTIONS)' /url "/graphql/execute.json*" }
```

Las consultas persistentes se pueden solicitar utilizando `GET`, almacenando así la respuesta en caché en el nivel de Dispatcher y CDN. Se pueden encontrar más detalles sobre almacenamiento en caché e invalidación de caché [here](/help/implementing/dispatcher/caching.md).
