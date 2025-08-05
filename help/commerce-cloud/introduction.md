---
title: Introducción e información general
description: Comprender las diferentes opciones de la tienda
thumbnail: introducing-aem-commerce.jpg
exl-id: 29410f76-a63f-4b0a-b817-2ed724ad1a3c
feature: Commerce Integration Framework
role: Admin
source-git-commit: 145cd4961bd9c0c7bb7e39a1d6dae67f240ecb4d
workflow-type: tm+mt
source-wordcount: '635'
ht-degree: 1%

---


# Content and Commerce {#content-commerce}

A medida que aumentan las expectativas de los clientes en cuanto a experiencias de comercio basadas en la intención y de alto rendimiento, las marcas se ven presionadas a ofrecer más contenido más rápidamente, sin sacrificar la calidad. Con Adobe Experience Manager, las marcas pueden escalar e innovar más rápido para crear experiencias de comercio envolventes y capturar más tráfico y un creciente gasto en línea.

Adobe Experience Manager ofrece potentes herramientas para crear y administrar experiencias del cliente personalizadas y enriquecidas en contenido. Al integrar AEM con una solución de comercio, como Adobe Commerce, Salesforce Commerce, SAP Commerce Cloud o cualquier otra solución, las marcas pueden unificar el contenido y el comercio para ofrecer recorridos de compra sin problemas en todos los canales.

## Información general sobre enfoques de tienda {#overview}

AEM puede proporcionarle asistencia en función de su situación y sus preferencias. Utilice las siguientes directrices para elegir el enfoque adecuado para usted:

* [Usar Edge Delivery Services (recomendado)](#edge)
* [Usar su propia tienda (integración de AEM sin encabezado)](#own-storefront)
* [Usar la tienda de AEM CIF](#cif)

### Usar Edge Delivery Services (recomendado) {#edge}

Si tu empresa quiere la tienda más rápida y compatible con IA en la web y los desarrolladores quieren una experiencia de desarrollador de última generación, usa [Edge Delivery Services.](../edge/overview.md) Edge Delivery Services cumple todos los requisitos actuales y futuros. Según el servidor y la solución, tiene diferentes opciones:

#### &#x200B;1. Integración con Adobe Commerce as a Cloud Service {#acaacs}

Esta es la solución perfecta si usas Edge Delivery y [Adobe Commerce Storefront](https://experienceleague.adobe.com/developer/commerce/storefront/?lang=es) como punto de partida. La tienda viene con una plantilla que está preintegrada con los servicios de Adobe Commerce, las API y ofrece una variedad de componentes de Commerce para crear rápidamente una tienda.

Buen ajuste: experiencia típica de tienda con Adobe Commerce as a Cloud Service

#### &#x200B;2. Integración con Adobe Commerce Optimizer (para cualquier solución de terceros) {#aco}

Si desea integrar su solución de comercio existente y mejorar el rendimiento de su catálogo, la recomendación de Adobe es usar [Adobe Commerce Optimizer](https://experienceleague.adobe.com/es/docs/commerce-learn/tutorials/adobe-commerce-optimizer/overview) como la capa de integración moderna. Commerce Optimizer mejora su solución comercial con servicios SaaS de alto rendimiento para catálogos y comercialización. Al igual que con Adobe Commerce as a Cloud Service, [Adobe Commerce Storefront](https://experienceleague.adobe.com/developer/commerce/storefront/?lang=es) funciona de forma predeterminada con él.

Hay integraciones disponibles para soluciones de comercio comercial como Salesforce Commerce. Hable con su representante de Adobe.

Buen ajuste: experiencia típica de tienda con una solución de comercio existente

#### &#x200B;3. Integración personalizada {#custom}

Adobe también recomienda utilizar Edge Delivery Services si desea crear una integración personalizada. Puede empezar desde cero o reutilizar los componentes de comercio del marco JS existentes (por ejemplo, para la parte transaccional) en la tienda de Edge Delivery. De esta manera, sus clientes obtendrán una experiencia de compra increíblemente rápida, que es amigable con el medio ambiente, mientras que usted puede reutilizar sus inversiones existentes para aumentar la TV. El punto de partida es la [plantilla de Edge Delivery](https://www.aem.live/developer/tutorial) predeterminada.

Buen ajuste: bajo valor de la tienda de Edge Delivery

### Utilice su propia tienda (integración de AEM sin encabezado) {#own-storefront}

Tiene una tienda existente (por ejemplo, creada con React JS) y quiere usar Adobe Experience Manager para la administración y entrega de contenido (fragmentos de contenido), recursos y edición en contexto (editor universal). El punto de partida para una integración es [Introducción a Adobe Experience Manager as a Headless CMS](https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/headless/introduction) y el [complemento de CIF](https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/content-and-commerce/storefront/authoring/enrich-product-associated-content). El complemento de CIF permite una integración perfecta de los datos de sus productos en AEM (busque, examine y encuentre productos dentro de la interfaz de usuario de AEM) que puede utilizar para crear experiencias específicas del comercio.

### Tienda de AEM CIF {#cif}

La arquitectura de referencia y recomendación de Adobe es utilizar Edge Delivery Services. La tienda de CIF con los componentes principales de AEM CIF ahora se encuentra en modo de mantenimiento y no debe usarse en nuevos proyectos. Como referencia, consulte la [documentación de CIF.](/help/commerce-cloud/cif-introduction.md)

>[!NOTE]
>
>Los clientes existentes que deseen aprovechar la nueva funcionalidad de AEM/Commerce deben trasladar su sitio web a Edge Delivery. Un patrón común es empezar moviendo solo un subconjunto de páginas a Edge Delivery y ejecutar las páginas de Edge Delivery y CIF en paralelo. También es posible reemplazar los componentes de AEM CIF con los nuevos [componentes integrados de Commerce](https://experienceleague.adobe.com/developer/commerce/storefront/dropins/all/introduction/?lang=es) para aprovechar las nuevas funcionalidades de Commerce.
