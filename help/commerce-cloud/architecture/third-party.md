---
title: AEM e Integraciones de comercio de terceros con Commerce Integration Framework
description: Los negocios empresariales pueden requerir soluciones de comercio de terceros adicionales para impulsar su tienda. Commerce Integration Framework (CIF) puede utilizarse en estos escenarios de integración para conectar una solución comercial de terceros a Adobe Experience Manager mediante el motor de ejecución de E/S.
thumbnail: cif-third-party-architecture.jpg
translation-type: tm+mt
source-git-commit: 72d98c21a3c02b98bd2474843b36f499e8d75a03
workflow-type: tm+mt
source-wordcount: '368'
ht-degree: 92%

---


# AEM e Integraciones de comercio de terceros con Commerce Integration Framework {#aem-third-party}

Los negocios empresariales pueden requerir soluciones de comercio de terceros adicionales para impulsar su tienda. Commerce Integration Framework (CIF) se puede utilizar en estos escenarios de integración en los que además de Magento, una solución de comercio de terceros también necesita integrarse con AEM. CIF proporciona elementos como un acelerador de referencia para tienda, componentes principales del CIF de AEM y herramientas de creación que funcionan con Magento de forma predeterminada. Para integrar a AEM con una solución de comercio de terceros y reutilizar estos elementos de CIF, se necesita algo más de desarrollo.

## Arquitectura {#architecture}

La arquitectura general es la siguiente:

![Descripción general de la arquitectura de terceros/AEM diferentes de Magento](/help/commerce-cloud/assets/AEM_nonMagento_Architecture.JPG)

La principal diferencia entre la arquitectura de integración para AEM (Magento y AEM) una solución de comercio de terceros es la adición de una capa de integración y transformación de datos como se muestra en la imagen anterior. La capa de integración debe alojarse en la plataforma Adobe I/O Runtime, que es la plataforma sin servidor de Adobe. Obtenga más información sobre Adobe I/O Runtime [aquí](https://www.adobe.io/apis/experienceplatform/runtime.html).

El propósito de esta capa de integración es asignar una API de terceros o diferentes de Magento a las API de Adobe Commerce (las API de Magento GraphQL). Esta asignación permite que las herramientas de creación de los [componentes principales del CIF de AEM](https://github.com/adobe/aem-core-cif-components) y del CIF recuperen los datos de las soluciones diferentes de Magento. Con este enfoque, la capa de integración encapsula la lógica de la integración y crea una separación de las preocupaciones entre AEM y la solución de terceros. Esto permite el uso de los elementos del CIF de manera independiente con varias soluciones de terceros. Las ventajas de utilizar elementos del CIF en su proyecto se describen en la [Introducción](/help/commerce-cloud/overview.md).

## Desarrollo de una integración {#develop-integration}

Para empezar a crear la capa de integración necesaria para integrar soluciones diferentes de Magento o de terceros con AEM, hemos creado una [implementación de referencia](https://github.com/adobe/commerce-cif-graphql-integration-reference) para demostrarla. Esta referencia se puede usar como punto de partida en el proyecto.
