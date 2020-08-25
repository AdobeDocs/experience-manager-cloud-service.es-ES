---
title: Integración de AEM y Magento con Commerce Integration Framework
description: Integración de AEM y Magento con Commerce Integration Framework
translation-type: ht
source-git-commit: 48805b21500ff3f2629efd6aecb40bb1cdc38cd6
workflow-type: ht
source-wordcount: '347'
ht-degree: 100%

---


# Integración de AEM y Magento con Commerce Integration Framework {#aem-magento-framework}

AEM y Magento se integran perfectamente con Commerce Integration Framework (CIF). CIF permite a AEM acceder a una instancia de Magento y comunicarse con Magento a través de GraphQL. También permite a los autores de AEM utilizar los seleccionadores de productos y categorías, así como la consola de productos para examinar los datos de productos y categorías que se obtienen a petición de Magento. Además, CIF ofrece una tienda predeterminada que puede acelerar los proyectos de comercio.

## Información general sobre la arquitectura {#overview}

La arquitectura general es la siguiente:

![Información general sobre la arquitectura del CIF](../assets/AEM_Magento_Architecture.JPG)

CIF se basa en la asistencia con GraphQL. El principal canal de comunicación entre AEM y Magento es la [API](https://devdocs.magento.com/guides/v2.4/graphql/) de Magento GraphQL. Existen diferentes maneras de configurar la comunicación entre AEM as a Cloud Service y Magento; consulte la página [Introducción](../getting-started.md) para obtener más información.

Dentro de CIF hay asistencia para patrones de comunicación del lado del servidor y del lado del cliente.
Las llamadas del lado del servidor de API se implementan mediante el [cliente de GraphQL](https://github.com/adobe/commerce-cif-graphql-client) genérico integrado en combinación con un [conjunto de modelos de datos generados](https://github.com/adobe/commerce-cif-magento-graphql) para el esquema Magento GraphQL. Además, se puede utilizar cualquier consulta o mutación de GraphQL en formato GQL.

Para los componentes del lado del cliente, que se generan mediante [React](https://reactjs.org/), se utiliza el cliente [Apollo](https://www.apollographql.com/docs/react/).

## Arquitectura de los componentes principales del CIF de AEM {#cif-core-components}

![Arquitectura de los componentes principales del CIF de AEM](../assets/cif-component-architecture.jpg)

Los [componentes principales del CIF de AEM](https://github.com/adobe/aem-core-cif-components) siguen patrones de diseño y prácticas recomendadas muy similares a los de los [componentes principales de WCM de AEM](https://github.com/adobe/aem-core-wcm-components).

La lógica empresarial y la comunicación back-end con Magento para los componentes principales del CIF de AEM se implementan en los modelos Sling. En caso de que sea necesario personalizar esta lógica para cumplir los requisitos específicos del proyecto, se puede utilizar el patrón de delegación para modelos Sling.

>[!TIP]
>
>La página [Personalización de los componentes principales del CIF de AEM](../customizing/customize-cif-components.md) tiene un ejemplo detallado y una práctica recomendada sobre cómo personalizar los componentes principales del CIF.

Dentro de los proyectos, los componentes principales del CIF de AEM y los componentes de proyecto personalizados pueden recuperar fácilmente el cliente configurado para una tienda de Magento asociado a una página AEM mediante la configuración según el contexto de Sling.
