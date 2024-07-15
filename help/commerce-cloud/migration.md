---
title: AEM Migración al complemento Commerce integration framework CIF de la ()
description: AEM Migración al complemento de Commerce integration framework CIF de () desde una versión antigua
exl-id: 0db03a05-f527-4853-b52f-f113bce929cf
feature: Commerce Integration Framework
role: Admin
source-git-commit: 0e328d013f3c5b9b965010e4e410b6fda2de042e
workflow-type: tm+mt
source-wordcount: '470'
ht-degree: 38%

---

# Guía de migración para el Experience Manager Cloud Service {#cif-migration}

Esta guía ayuda a identificar las áreas que debe actualizar para la migración de Experience Manager Cloud Service.

## CIF complemento de

Para Experience Manager as a Cloud Service CIF, el complemento de integración de comercio es la única solución de integración de comercio compatible para Adobe Commerce y soluciones de comercio de terceros. El complemento CIF se implementa automáticamente para los clientes de Experience Manager as a Cloud Service; no se necesita una implementación manual. Consulte [Introducción a AEM Commerce as a Cloud Service](getting-started.md).

CIF Para admitir proyectos que implementen el Adobe AEM CIF de trabajo, proporcione [Componentes principales de la](https://github.com/adobe/aem-core-cif-components).

El complemento CIF también está disponible para AEM 6.5 a través del [Portal de distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/es/aem.html). Es compatible y proporciona las mismas características que el complemento CIF para Experience Manager as a Cloud Service: no se requieren ajustes.

El CIF clásico con sus dependencias ya no está disponible. CIF CIF El código que se basa en esta versión de la que usa `com.adobe.cq.commerce.api` API de Java debe ajustarse al complemento de la aplicación y a sus principios.

CIF Ya no se puede instalar el conector de disponible anteriormente. CIF El código que se basa en este conector debe ajustarse al complemento de y a sus principios.

## Estructura del proyecto

AEM Conozca la [Estructura del proyecto de](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html?lang=es) y las características de AEM as a Cloud Service. Adapte la configuración del proyecto al diseño de AEM as a Cloud Service.
AEM En comparación con las implementaciones de la versión 6.5 de, existen dos diferencias principales:

* El paquete OSGI del cliente de GraphQL ya **no debe** incluirse en el proyecto AEM; se implementa mediante el complemento CIF
* Las configuraciones OSGI para el cliente de GraphQL y el servicio de datos Graphql ya **no deben** incluirse en el proyecto AEM.

>[!TIP]
>
>Consulte el proyecto de la [Tienda de referencia de Venia de AEM](https://github.com/adobe/aem-cif-guides-venia) en GitHub. Este proyecto proporciona perfiles Maven para AEM as a Cloud Service e instalaciones on-premise que tienen en cuenta las diferentes condiciones del marco de trabajo.

## Catálogo de productos

Ya no se admite la importación de datos del catálogo de productos. CIF El uso de las solicitudes de producto y catálogo de las entidades de seguridad de la aplicación se realiza a petición mediante llamadas en tiempo real a una solución de comercio externo. Vaya al capítulo Integración para obtener más información sobre la integración de una solución de comercio.

>[!TIP]
>
>Si no hay API en tiempo real disponibles, se debe utilizar una caché de producto externo con API para la integración. Ejemplo [Magento de código abierto](https://business.adobe.com/products/magento/open-source.html).

## AEM Experiencias del catálogo de productos con procesamiento de la

CIF Si utiliza el modelo de catálogo con la versión clásica de los productos, debe actualizar el flujo de trabajo del catálogo de productos. CIF AEM El complemento ahora procesa experiencias del catálogo de productos sobre la marcha utilizando plantillas de catálogo de productos de la aplicación de la manera más rápida y sencilla Ya no se requiere replicación de datos o páginas de productos.

## Interacción de compras y datos no almacenables en caché

Las solicitudes del lado del cliente para datos e interacciones no almacenables en caché (por ejemplo, complemento al carro, búsqueda) deben ir directamente al extremo de comercio (ya sea la solución de comercio o la capa de integración) a través de CDN/Dispatcher. AEM Elimine todas las llamadas en las que solo haya un proxy en el que se haya realizado la.
