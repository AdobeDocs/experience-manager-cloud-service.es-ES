---
title: Integración comercial de AEM y terceros mediante Commerce Integration Framework
description: Integración comercial de AEM y terceros mediante Commerce Integration Framework
translation-type: tm+mt
source-git-commit: c5694cf8651cf8ba5331c730fa1b1180310dd35a
workflow-type: tm+mt
source-wordcount: '338'
ht-degree: 0%

---


# Integración comercial de AEM y terceros mediante Commerce Integration Framework {#aem-third-party}

Las empresas empresariales pueden requerir soluciones comerciales de terceros adicionales para alimentar su tienda. El marco de integración comercial (CIF) se puede utilizar en estos escenarios de integración en los que además de Magento, una solución comercial de terceros también necesita integrarse con AEM. CIF proporciona elementos como una tienda de referencia de acelerador, componentes principales de CIF de AEM y herramientas de creación que funcionan con Magento listos para usar. Para integrar AEM y una solución de comercio de terceros y reutilizar estos elementos de CIF, se necesita algo más de desarrollo.

## Arquitectura {#architecture}

La arquitectura general es la siguiente:

![Descripción general de la arquitectura AEM no Magento/de terceros](/help/commerce-cloud/assets/AEM_nonMagento_Architecture.JPG)

La principal diferencia entre la arquitectura de integración para el comercio AEM (Magento y AEM) de terceros es la adición de una capa de integración y transformación de datos, como se muestra en la imagen anterior. La capa de integración debe alojarse en la plataforma Adobe I/O Runtime, que es la plataforma sin servidor de Adobe. Puede obtener más información sobre Adobe I/O Runtime [aquí](https://www.adobe.io/apis/experienceplatform/runtime.html).

El propósito de esta capa de integración es asignar API de terceros o no Magento a las API de comercio de Adobe (API de Magento GraphQL). Esta asignación permite que las herramientas de creación de [AEM componentes](https://github.com/adobe/aem-core-cif-components) principales CIF y CIF recuperen datos de la solución que no es de Magento. Con este enfoque, la capa de integración encapsula la lógica de integración y crea una separación de preocupaciones entre AEM y la solución de terceros. Esto permite el uso de los elementos CIF de manera agnóstica con varias soluciones de terceros. Las ventajas de utilizar elementos CIF en su proyecto se describen en la [Introducción](/help/commerce-cloud/overview.md).

## Desarrollar una integración {#develop-integration}

Para ayudarle a empezar a crear la capa de integración necesaria para integrar una solución que no sea de Magento o de terceros con AEM, hemos creado una implementación [de](https://github.com/adobe/commerce-cif-graphql-integration-reference) referencia para demostrarla. Esta referencia se puede usar como punto de partida en el proyecto.
