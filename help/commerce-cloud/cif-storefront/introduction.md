---
title: Introducción a AEM Commerce Integration Framework (CIF)
description: Obtenga información sobre cómo utilizar y administrar Experience Manager Content y Commerce as a Cloud Service con CIF.
thumbnail: introducing-aem-commerce.jpg
feature: Commerce Integration Framework
role: Admin
exl-id: 3f18f976-ff8a-4726-b4c5-db4e19ae7cee
source-git-commit: e707bddc17208d599491d27c5bc0134cb41233e0
workflow-type: tm+mt
source-wordcount: '586'
ht-degree: 61%

---


# Introducción a AEM Commerce Integration Framework (CIF) {#cif-intro}

Una solución de comercio puede ser cualquier cosa, desde una solución comercial como Adobe Commerce Cloud hasta un conjunto de servicios de comercio personalizados. La integración depende en gran medida del caso de uso y del ecosistema. Por lo general, afecta a varios sistemas y se presenta en muchas variedades diferentes:

* Integración de un ecosistema complejo y dinámico (por ejemplo, catálogos de productos)
* La empresa debe administrar el contenido del producto con su propio ciclo de vida de forma eficiente y omnicanal
* Creación de recorridos de compra, complejos y personalizados, para varios destinatarios
* Capacidad de adaptarse e innovar rápidamente en el back-end y front-end
* Ejecución de una infraestructura E2E escalable y estable diseñada para obtener el máximo rendimiento (venta flash, Black Friday, ...), incluida la búsqueda unificada y la administración de caché

Esta complejidad abre la puerta a posibles fallos, un incremento del coste total de propiedad (TCO), retrasos y menor realización de valor. Estas razones han llevado al desarrollo de Commerce Integration Framework (CIF), que es un complemento de Experience Manager. CIF amplía Experience Manager con capacidades comerciales y estandariza la integración con un motor de comercio. El resultado es una solución a prueba de futuro, estable y escalable con un menor coste total de propiedad (TCO). Desbloquea la innovación técnica y empresarial con herramientas ágiles y funciones integradas para crear experiencias comerciales atractivas.

![Elementos del CIF](./assets/CIF/CIF_Overview.png)

## Beneficios del CIF {#cif-benefits}

CIF proporciona componentes principales comerciales predeterminados que reducen la necesidad de usar un código personalizado, lo que acelera el tiempo de salida al mercado de las marcas. Todos los componentes principales están integrados de forma predeterminada con la capa de datos del lado del cliente de Adobe para integrar los perfiles de los clientes, como el perfil unificado. Este perfil captura en detalle el comportamiento de un visitante, que puede utilizarse para predecir y personalizar el recorrido del cliente en tiempo real.

El complemento CIF introduce el contexto del producto en Experience Manager y proporciona herramientas de creación, como una consola de producto y selectores de producto/categoría, que permiten al experto en marketing crear y ofrecer experiencias de compra en Experience Manager sin depender del desarrollador. Las ventajas incluyen las siguientes:

* [Experiencias convincentes](#experiences)
* [Obtención de valor en menos tiempo](#ttv)
* [Integraciones sólidas](#integrations)

### Experiencias {#experiences}

Las potentes herramientas del CIF en AEM permiten a los creadores de contenido crear rápidamente experiencias de comercio ricas y personalizadas de una manera escalable y sin depender del envío para aprovechar las oportunidades del negocio.

![Elementos del CIF](./assets/CIF/CIF_Product_Experience_Management.png)

### Tiempo de creación de valor (TTV) {#ttv}

CIF acelera el desarrollo de proyectos con [componentes principales de AEM](https://www.aemcomponents.dev/), [tienda de referencia de AEM Venia](https://github.com/adobe/aem-cif-guides-venia), [tipo de archivo del proyecto AEM](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=es) y patrones de integración para PWA (contenido y comercio sin encabezado).

CIF está diseñado para la innovación continua con un complemento siempre actualizado, que le permite acceder a funciones nuevas y mejoradas.

### Integraciones {#integrations}

Conecte el ecosistema (por ejemplo, la solución de comercio) con Experience Cloud mediante [Adobe I/O Runtime](https://www.adobe.io/apis/experienceplatform/runtime.html), un PaaS sin servidor basado en microservicios y la [Implementación de referencia de CIF](https://github.com/adobe/commerce-cif-graphql-integration-reference).

## Patrones comprobados y prácticas recomendadas {#proven}

CIF le ofrece compatibilidad con patrones de integración estandarizados basados en las prácticas recomendadas. Esto le ayuda a tener éxito hoy en día y es flexible para crecer con su y adaptarse a los requisitos futuros:

* Elimina los desafíos típicos relacionados con las integraciones de catálogos de productos que pueden producirse, por ejemplo:
   * Problemas de rendimiento con mayor volumen o complejidad del catálogo
   * No tener acceso a los datos clasificados
   * Necesidad de experiencias y datos de productos en tiempo real
* Una creciente madurez digital resulta en la necesidad de administrar la experiencia
* &#x200B;
   * CIF incluye capacidades de administración de experiencia de producto que se pueden incorporar gradualmente sin necesidad de un esfuerzo adicional en TI.
* Listo para omnicanal
   * CIF admite una variedad de tecnologías de puntos de contacto (del lado del servidor, híbrido, del lado del cliente) con patrones, aceleradores y componentes principales.

## Recorrido {#journey}

Si está siguiendo el Recorrido de Commerce, vaya al siguiente paso:

* El [Recorrido de autor de contenido de AEM](/help/commerce-cloud/cif-storefront/commerce-journeys/aem-commerce-content-author/getting-started.md)
