---
title: Integración de AEM y Adobe Commerce con Commerce integration framework
description: AEM y Adobe Commerce se integran perfectamente con Commerce integration framework (CIF). CIF permite a AEM acceder a una instancia de Adobe Commerce y comunicarse con Adobe Commerce a través de GraphQL. También permite a los autores de AEM utilizar los seleccionadores de productos y categorías, así como la consola de productos para examinar los datos de productos y categorías que se obtienen a petición de Adobe Commerce. Además, CIF ofrece una tienda predeterminada que puede acelerar los proyectos de comercio.
thumbnail: aem-magento-architecture.jpg
exl-id: 110ceef5-2c35-4b81-8e89-26929c0da91b
feature: Commerce Integration Framework
role: Admin
index: false
source-git-commit: 173b70aa6f9ad848d0f80923407bf07540987071
workflow-type: tm+mt
source-wordcount: '439'
ht-degree: 22%

---

# Integración de AEM y Adobe Commerce con Commerce integration framework {#aem-framework}

Experience Manager y Adobe Commerce se integran perfectamente con Commerce integration framework (CIF). CIF permite que AEM acceda directamente a la instancia de Commerce y se comunique con ella mediante las [API de GraphQL](https://devdocs.magento.com/guides/v2.4/graphql/) de Adobe Commerce.

>[!NOTE]
>
> La versión mínima de la API de GraphQL admitida es 2.3.5. Algunas funciones solo son compatibles con las versiones más recientes o solo con la edición de Adobe Commerce.

>[!NOTE]
>
>GraphQL se utiliza actualmente en dos escenarios (independientes) en Adobe Experience Manager (AEM) as a Cloud Service:
>
>* Este escenario, en el que CIF se comunica con el comercio a través de GraphQL.
>* [Los fragmentos de contenido de AEM trabajan junto con la API de GraphQL de AEM (una implementación personalizada, basada en GraphQL estándar) para ofrecer contenido estructurado para su uso en aplicaciones](/help/headless/graphql-api/content-fragments.md).

## Información general sobre la arquitectura {#overview}

La arquitectura general es la siguiente:

![Información general sobre la arquitectura del CIF](../assets/AEM_Magento_Architecture.png)

Dentro de CIF, hay compatibilidad con patrones de comunicación del lado del servidor y del lado del cliente.
Las llamadas de API del lado del servidor se implementan mediante el [cliente GraphQL](https://github.com/adobe/commerce-cif-graphql-client) genérico integrado en combinación con un [conjunto de modelos de datos generados](https://github.com/adobe/commerce-cif-magento-graphql) para el esquema de Commerce GraphQL. Además, se puede utilizar cualquier consulta o mutación de GraphQL en formato GQL.

Para los componentes del lado del cliente, que se crean con [React](https://reactjs.org/), se usa [Apollo Client](https://www.apollographql.com/docs/react/).

## Arquitectura de componentes principales de AEM CIF {#cif-core-components}

![Arquitectura de los componentes principales del CIF de AEM](../assets/cif-component-architecture.jpg)

[Los componentes principales de AEM CIF](https://github.com/adobe/aem-core-cif-components) siguen patrones de diseño y prácticas recomendadas muy similares a los de los [componentes principales de AEM WCM](https://github.com/adobe/aem-core-wcm-components).

La lógica empresarial y la comunicación back-end con Adobe Commerce para los componentes principales de AEM CIF se implementan en los modelos Sling. En caso de que sea necesario personalizar esta lógica para cumplir los requisitos específicos del proyecto, se puede utilizar el patrón de delegación para modelos Sling.

>[!TIP]
>
>La página [Personalización de los componentes principales del CIF de AEM](../customizing/customize-cif-components.md) tiene un ejemplo detallado y una práctica recomendada sobre cómo personalizar los componentes principales del CIF.

Dentro de los proyectos, los componentes principales de AEM CIF y los componentes de proyecto personalizados pueden recuperar fácilmente el cliente configurado para una tienda de Adobe Commerce asociado a una página de AEM mediante la configuración según el contexto de Sling.

## Búsqueda {#search}

CIF proporciona de forma predeterminada un [Componente principal de búsqueda](https://www.aemcomponents.dev/content/core-components-examples/library/commerce/search.html) que es una experiencia de búsqueda procesada en el servidor basada en la [API de Commerce GraphQL](https://developer.adobe.com/commerce/webapi/graphql/). Los clientes de Commerce tienen la opción de usar [Live Search](https://experienceleague.adobe.com/docs/commerce-merchant-services/live-search/guide-overview.html?lang=es) en su lugar. Siga este [vínculo](/help/commerce-cloud/integrating/live-search-plp.md) para obtener más información sobre la integración de CIF con Live Search.

