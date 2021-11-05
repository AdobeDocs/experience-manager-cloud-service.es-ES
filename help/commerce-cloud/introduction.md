---
title: Introducción y descripción general
description: Introduction and overview of content and commerce. Experience Manager Commerce Integration Framework (CIF) es el patrón recomendado por el Adobe para integrar y ampliar los servicios de comercio de Magento y otras soluciones de comercio de terceros con el Experience Cloud.
thumbnail: introducing-aem-commerce.jpg
exl-id: 29410f76-a63f-4b0a-b817-2ed724ad1a3c,74e832f9-f8ff-4901-b4c2-6a2862c51411
source-git-commit: 8a8a1f7f461e5a02bfadfc392508d920bd6c1601
workflow-type: tm+mt
source-wordcount: '874'
ht-degree: 2%

---

# Contenido y comercio {#content-commerce}

Con el contenido y el comercio de Adobe Experience Manager, las marcas pueden escalar e innovar más rápido para diferenciar las experiencias comerciales y capturar un gasto en línea acelerado. AEM Contenido y comercio combina las experiencias inmersivas, omnicanal y personalizadas en Experience Manager con cualquier cantidad de soluciones de comercio para ofrecer experiencias diferenciadas en todas las partes del recorrido de compras, reduciendo el tiempo de respuesta al valor e impulsando una mayor conversión.

## Cómo el contenido y el comercio ayudan a los clientes a tener éxito

Con las crecientes expectativas de los clientes para las experiencias de comercio en línea, las marcas se ven presionadas para ofrecer experiencias diferenciadas y más contenido más rápido. However, implementing a content management platform often requires heavy time and budget investments in developing foundational elements, such as custom components and authoring tools, and accrues costs in maintenance and upgrades. Experience Manager Sites ofrece Contenido y comercio como módulo de complemento para Experience Manager as a Cloud Service que proporciona componentes comerciales básicos, herramientas de creación y una tienda de referencia para acelerar la entrada en funcionamiento, permitir una colaboración fluida entre equipos e impulsar la conversión.

Las marcas pueden integrar Experience Manager con Adobe Commerce, parte de Adobe Experience Cloud, así como con cualquier motor de comercio que desee. Con Contenido y comercio Experience Manager, las marcas pueden:

* Escalar e innovar más rápido
* Personalización de experiencias para impulsar la conversión
* Create once, and publish everywhere
* Enriquecimiento y diferenciación de experiencias para los clientes
* Optimice la creación con acceso a datos de comercio

## Presentación de AEM Commerce Integration Framework (CIF) {#cif-intro}

Como estos proyectos tienen que lidiar con la complejidad de integrar una solución de comercio. A commerce solution can be anything from a commercial solution such as the Adobe Commerce Cloud to a set of custom commerce services. The integration is highly dependent on the use-cases and ecosystem. It usually touches various places and comes in many different flavors:

* Integración de un ecosistema complejo y dinámico (por ejemplo, catálogos de productos)
* Business needs to manage product content with its own lifecycle in an efficient and omnichannel way
* Creación de recorridos de compra complejos y personalizados para varias cabezas
* Capacidad de adaptarse e innovar rápidamente en el back-end y el front-end
* Running a scalable and stable E2E infrastructure that is built for peak performance (Flash sale, Black Friday, ...). Esto incluye la búsqueda unificada y la administración de la caché.

Esta complejidad abre la puerta a posibles puntos de falla, aumento del TCO, retrasos y menor realización de valor. These reasons have led to the development of the Commerce Integration Framework (CIF) which is an add-on for the Experience Manager. CIF amplía el Experience Manager con capacidades comerciales y estandariza la integración con un motor de comercio. El resultado es una solución estable, escalable y a prueba de futuro con menor TCO. It unlocks technical and business innovation with agile tooling and seamlessly integrated features to build compelling commerce experiences.

![Elementos del CIF](./assets/CIF/CIF_Overview.png)

## CIF Successfully Supporting Customers since 2013

Con más de 200 clientes, CIF se ha establecido como un ingrediente exitoso para un proyecto de comercio y contenido exitoso. Esto proporciona valor para TI y el negocio de hoy y en el futuro. Los proyectos recientes de los clientes describen CIF como un &quot;acelerador Bueno y ahorrador de tiempo enorme con mucho valor&quot;.

## Beneficios del CIF {#cif-benefits}

CIF proporciona componentes básicos de comercio listos para usar que reducen la necesidad de usar código personalizado, lo que acelera el tiempo de comercialización de las marcas. Todos los componentes principales están integrados de forma predeterminada con la capa de datos del lado del cliente de Adobe para hidratar los perfiles de los clientes, como el perfil unificado. This profile captures in detail a visitor’s behavior, which can be used to predict and personalize the customer journey in real time.

El complemento CIF lleva el contexto del producto al Experience Manager y proporciona herramientas de creación, como una consola de producto y selectores de producto/categoría, que permiten al especialista en marketing crear y ofrecer experiencias de ventas en Experience Manager sin depender del desarrollador. Las ventajas incluyen:

### Experiencias

Las potentes herramientas del CIF en AEM permiten a los creadores de contenido crear rápidamente experiencias de comercio enriquecidas y personalizadas de una manera escalable y sin diferencias de envío para aprovechar las oportunidades comerciales.

![Elementos del CIF](./assets/CIF/CIF_Product_Experience_Management.png)

### Tiempo para el valor (TTV)

Acelera el desarrollo de proyectos con [Componentes principales AEM](https://www.aemcomponents.dev/), [Tienda de referencia de Venia AEM](https://github.com/adobe/aem-cif-guides-venia), [Tipo de archivo del proyecto AEM](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html)y patrones de integración para PWA (contenido sin encabezado y comercio).

El CIF está diseñado para la innovación continua con un complemento siempre actualizado, que permite al cliente acceder a funciones nuevas y mejoradas.

### Integraciones

Connect your ecosystem (e.g. commerce solution) with the Experience Cloud using  [Adobe I/O Runtime](https://www.adobe.io/apis/experienceplatform/runtime.html), a micro-service based server-less PaaS, and [CIF&#39;s reference implementation](https://github.com/adobe/commerce-cif-graphql-integration-reference).

## Patrones comprobados y prácticas recomendadas

CIF admite clientes con patrones de integración estandarizados basados en prácticas recomendadas. This helps customers to be successful today and is flexible to grow with the customer and adapt to future requirements:

* Elimina los desafíos típicos relacionados con las integraciones de catálogos de productos que pueden producirse. Ejemplos:
   * Problemas de rendimiento con mayor volumen o complejidad del catálogo
   * Sin acceso a los datos clasificados
   * Necesidad de experiencias y datos de productos en tiempo real
* La creciente madurez digital hace que sea necesario administrar la experiencia. El CIF incluye capacidades de administración de experiencia de producto que se pueden incorporar gradualmente sin necesidad de un esfuerzo adicional de TI.
* Listo para todos los canales: CIF admite una variedad de tecnologías de puntos de contacto (del lado del servidor, híbridas, del lado del cliente) con patrones, aceleradores y componentes principales.
