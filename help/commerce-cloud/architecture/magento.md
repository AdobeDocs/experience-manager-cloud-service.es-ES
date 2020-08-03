---
title: Integración de AEM y Magento mediante Commerce Integration Framework
description: Integración de AEM y Magento mediante Commerce Integration Framework
translation-type: tm+mt
source-git-commit: 48805b21500ff3f2629efd6aecb40bb1cdc38cd6
workflow-type: tm+mt
source-wordcount: '347'
ht-degree: 1%

---


# AEM and Magento Integration using Commerce Integration Framework {#aem-magento-framework}

AEM y Magento se integran perfectamente con Commerce Integration Framework (CIF). CIF permite a AEM acceder a una instancia de Magento y comunicarse con Magento a través de GraphQL. También permite que los AEM Author utilicen los seleccionadores de productos y Categorías y la consola de productos para examinar los datos de productos y categorías que el Magento ha obtenido a pedido. Además, CIF ofrece una tienda lista para usar que puede acelerar los proyectos comerciales.

## Información general sobre la arquitectura {#overview}

La arquitectura general es la siguiente:

![Información general sobre la arquitectura CIF](../assets/AEM_Magento_Architecture.JPG)

CIF se basa en la compatibilidad con GraphQL. El principal canal de comunicación entre AEM y Magento es la API [de API](https://devdocs.magento.com/guides/v2.4/graphql/) de MagentoGraphQL. Existen diferentes maneras de configurar la comunicación entre AEM como Cloud Service y Magento; consulte la página [Introducción](../getting-started.md) para obtener más información.

Dentro de CIF hay soporte para patrones de comunicación del lado del servidor y del lado del cliente.
Las llamadas de API de servidor se implementan mediante el cliente [](https://github.com/adobe/commerce-cif-graphql-client) GraphQL genérico integrado en combinación con un [conjunto de modelos](https://github.com/adobe/commerce-cif-magento-graphql) de datos generados para el esquema Magento GraphQL. Además, se puede utilizar cualquier consulta o mutación de GraphQL en formato GQL.

Para los componentes del lado del cliente, que se generan mediante [React](https://reactjs.org/), se utiliza el cliente [Apollo](https://www.apollographql.com/docs/react/) .

## AEM Arquitectura de componentes principales de CIF {#cif-core-components}

![AEM Arquitectura de componentes principales de CIF](../assets/cif-component-architecture.jpg)

[AEM componentes](https://github.com/adobe/aem-core-cif-components) principales de CIF siguen patrones de diseño y prácticas recomendadas muy similares a los de los componentes [principales de WCM](https://github.com/adobe/aem-core-wcm-components)AEM.

La lógica de negocio y la comunicación back-end con el Magento para los componentes principales AEM CIF se implementan en los modelos Sling. En caso de que sea necesario personalizar esta lógica para cumplir los requisitos específicos del proyecto, se puede utilizar el patrón de delegación para modelos Sling.

>[!TIP]
>
>La página [Personalización de AEM componentes](../customizing/customize-cif-components.md) principales de CIF tiene un ejemplo detallado y una práctica recomendada sobre cómo personalizar los componentes principales de CIF.

Dentro de los proyectos, AEM componentes principales de CIF y componentes de proyecto personalizados pueden recuperar fácilmente el cliente configurado para un almacén de Magento asociado a una página AEM mediante la configuración según el contexto de Sling.
