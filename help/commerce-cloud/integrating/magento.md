---
title: Integración de AEM y Adobe Commerce (Magento) con Commerce Integration Framework
description: AEM y Adobe Commerce (Magento) se integran perfectamente con Commerce Integration Framework (CIF). CIF permite a AEM acceder a una instancia de Magento y comunicarse con Magento a través de GraphQL. También permite a los autores de AEM utilizar los seleccionadores de productos y categorías, así como la consola de productos para examinar los datos de productos y categorías que se obtienen a petición de Magento. Además, CIF ofrece una tienda predeterminada que puede acelerar los proyectos de comercio.
thumbnail: aem-magento-architecture.jpg
exl-id: 110ceef5-2c35-4b81-8e89-26929c0da91b,1cdfda88-a728-432f-b24a-f81347572bcf
source-git-commit: 96e7a7c38dd1275c9b0d291d12a0f768ab183c38
workflow-type: tm+mt
source-wordcount: '413'
ht-degree: 32%

---

# Integración de AEM y Adobe Commerce (Magento) con Commerce Integration Framework {#aem-magento-framework}

El Experience Manager y Adobe Commerce (Magento) se integran perfectamente con Commerce Integration Framework (CIF). CIF permite a AEM acceder directamente a la instancia de comercio y comunicarse con ella mediante Adobe Commerce [API de GraphQL](https://devdocs.magento.com/guides/v2.4/graphql/).

>[!NOTE]
>
> La versión mínima de la API de GraphQL admitida es 2.3.5. Algunas funciones solo se admiten en versiones más recientes o solo en la edición de Adobe Commerce.

>[!NOTE]
>
>GraphQL se utiliza actualmente en dos escenarios (independientes) en Adobe Experience Manager (AEM) as a Cloud Service:
>
>* En este caso, el CIF se comunica con el comercio mediante GraphQL.
>* [AEM fragmentos de contenido trabajan junto con la API de GraphQL de AEM (una implementación personalizada, basada en GraphQL estándar) para ofrecer contenido estructurado para su uso en las aplicaciones](/help/assets/content-fragments/graphql-api-content-fragments.md).


## Información general sobre la arquitectura {#overview}

La arquitectura general es la siguiente:

![Información general sobre la arquitectura del CIF](../assets/AEM_Magento_Architecture.png)

Dentro de CIF, existe compatibilidad con patrones de comunicación del lado del servidor y del lado del cliente.
Las llamadas de API del lado del servidor se implementan mediante el uso genérico integrado [Cliente de GraphQL](https://github.com/adobe/commerce-cif-graphql-client) en combinación con un [conjunto de modelos de datos generados](https://github.com/adobe/commerce-cif-magento-graphql) para el esquema commerce GraphQL. Además, se puede utilizar cualquier consulta o mutación de GraphQL en formato GQL.

Para los componentes del lado del cliente, que se crean mediante [React](https://reactjs.org/), el [Cliente Apollo](https://www.apollographql.com/docs/react/) se utiliza.

## Arquitectura de los componentes principales del CIF de AEM {#cif-core-components}

![Arquitectura de los componentes principales del CIF de AEM](../assets/cif-component-architecture.jpg)

[Componentes principales del CIF de AEM](https://github.com/adobe/aem-core-cif-components) siga patrones de diseño y prácticas recomendadas muy similares a los de [Componentes principales AEM WCM](https://github.com/adobe/aem-core-wcm-components).

La lógica empresarial y la comunicación back-end con Adobe Commerce para los componentes principales del CIF de AEM se implementan en los modelos Sling. En caso de que sea necesario personalizar esta lógica para cumplir los requisitos específicos del proyecto, se puede utilizar el patrón de delegación para modelos Sling.

>[!TIP]
>
>La página [Personalización de los componentes principales del CIF de AEM](../customizing/customize-cif-components.md) tiene un ejemplo detallado y una práctica recomendada sobre cómo personalizar los componentes principales del CIF.

Dentro de los proyectos, AEM componentes principales del CIF y los componentes de proyecto personalizados pueden recuperar fácilmente el cliente configurado para una tienda de Adobe Commerce asociada a una página AEM mediante la configuración según el contexto de Sling.
