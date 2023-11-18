---
title: AEM Integración de Adobe Commerce y de con Commerce integration framework
description: AEM Las soluciones de Adobe Commerce y de se integran perfectamente con el Commerce integration framework CIF (). CIF AEM La permite a los usuarios acceder a una instancia de Adobe Commerce y comunicarse con Adobe Commerce a través de GraphQL. AEM También permite a los autores de la utilizar los seleccionadores de productos y categorías, así como la consola de productos para examinar los datos de productos y categorías que se obtienen a petición de Adobe Commerce. Además, CIF ofrece una tienda predeterminada que puede acelerar los proyectos de comercio.
thumbnail: aem-magento-architecture.jpg
exl-id: 110ceef5-2c35-4b81-8e89-26929c0da91b
source-git-commit: bc3c054e781789aa2a2b94f77b0616caec15e2ff
workflow-type: tm+mt
source-wordcount: '412'
ht-degree: 30%

---

# AEM Integración de Adobe Commerce y de con Commerce integration framework {#aem-framework}

El Experience Manager y Adobe Commerce se integran perfectamente con el Commerce integration framework CIF (). CIF AEM Adobe Commerce La permite a los usuarios acceder directamente a la instancia de commerce y comunicarse con ella mediante el [API de GraphQL](https://devdocs.magento.com/guides/v2.4/graphql/).

>[!NOTE]
>
> La versión mínima de la API de GraphQL admitida es 2.3.5. Algunas funciones solo son compatibles con las versiones más recientes o solo con la edición de Adobe Commerce.

>[!NOTE]
>
>GraphQL se utiliza actualmente en dos escenarios (independientes) en Adobe Experience Manager (AEM) as a Cloud Service:
>
>* CIF En este escenario, en el que se comunica con el comercio a través de GraphQL.
>* [Los fragmentos de contenido de AEM trabajan junto con la API de GraphQL de AEM (una implementación personalizada, basada en GraphQL estándar) para ofrecer contenido estructurado para su uso en aplicaciones](/help/headless/graphql-api/content-fragments.md).

## Información general sobre la arquitectura {#overview}

La arquitectura general es la siguiente:

![Información general sobre la arquitectura del CIF](../assets/AEM_Magento_Architecture.png)

CIF Dentro de, hay compatibilidad con patrones de comunicación del lado del servidor y del lado del cliente.
Las llamadas del lado del servidor de API se implementan mediante el complemento integrado genérico [cliente de GraphQL](https://github.com/adobe/commerce-cif-graphql-client) en combinación con un [conjunto de modelos de datos generados](https://github.com/adobe/commerce-cif-magento-graphql) para el esquema de commerce GraphQL. Además, se puede utilizar cualquier consulta o mutación de GraphQL en formato GQL.

Para los componentes del lado del cliente, que se crean mediante [Reaccionar](https://reactjs.org/), el [Cliente Apollo](https://www.apollographql.com/docs/react/) se utiliza.

## Arquitectura de los componentes principales del CIF de AEM {#cif-core-components}

![Arquitectura de los componentes principales del CIF de AEM](../assets/cif-component-architecture.jpg)

[AEM Componentes principales de CIF](https://github.com/adobe/aem-core-cif-components) siga patrones de diseño y prácticas recomendadas muy similares a los de la [AEM Componentes principales de WCM](https://github.com/adobe/aem-core-wcm-components).

La lógica empresarial y la comunicación back-end con Adobe Commerce AEM CIF para los componentes principales de la se implementan en los modelos Sling. En caso de que sea necesario personalizar esta lógica para cumplir los requisitos específicos del proyecto, se puede utilizar el patrón de delegación para modelos Sling.

>[!TIP]
>
>La página [Personalización de los componentes principales del CIF de AEM](../customizing/customize-cif-components.md) tiene un ejemplo detallado y una práctica recomendada sobre cómo personalizar los componentes principales del CIF.

AEM CIF Dentro de los proyectos, los componentes principales de la y los componentes de proyecto personalizados pueden recuperar fácilmente el cliente configurado para una tienda de Adobe Commerce AEM asociado a una página mediante la configuración según el contexto de Sling.
