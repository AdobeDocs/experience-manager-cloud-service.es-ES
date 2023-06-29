---
title: AEM Migración al complemento Marco de integración de comercio de (CIF)
description: AEM Migración del complemento Commerce Integration Framework (CIF) de la versión antigua a la versión de la plataforma de integración de comercio de la versión de
exl-id: 0db03a05-f527-4853-b52f-f113bce929cf
source-git-commit: 1994b90e3876f03efa571a9ce65b9fb8b3c90ec4
workflow-type: tm+mt
source-wordcount: '490'
ht-degree: 40%

---

# Guía de migración para el Experience Manager Cloud Service {#cif-migration}

Esta guía ayuda a identificar las áreas que debe actualizar para la migración de Experience Manager Cloud Service.

## Complemento CIF

Para los Experience Manager as a Cloud Service, el complemento CIF es la única solución de integración comercial compatible para Adobe Commerce y las soluciones de comercio de terceros. El complemento CIF se implementa automáticamente para los clientes de Experience Manager as a Cloud Service; no se necesita una implementación manual. Consulte [Introducción a AEM Commerce as a Cloud Service](getting-started.md).

Para apoyar proyectos que implementen el Adobe del CIF, proporcione [AEM Componentes principales de CIF](https://github.com/adobe/aem-core-cif-components).

El complemento CIF también está disponible para AEM 6.5 a través del [Portal de distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/es/aem.html). Es compatible y proporciona las mismas características que el complemento CIF para Experience Manager as a Cloud Service: no se requieren ajustes.

El CIF clásico con sus dependencias ya no está disponible. El código que se basa en esta versión del CIF que utiliza `com.adobe.cq.commerce.api` Las API de Java deben ajustarse al complemento CIF y a sus principios.

El conector del CIF disponible anteriormente ya no se puede instalar. El código que se basa en este conector debe ajustarse al complemento CIF y a sus principios.

## Estructura del proyecto

Conozca las [AEM Estructura del proyecto de](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html?lang=es) AEM y las características de los as a Cloud Service de la. Adapte la configuración del proyecto al diseño de AEM as a Cloud Service.
AEM En comparación con las implementaciones de la versión 6.5 de, existen dos diferencias principales:

* El paquete OSGI del cliente de GraphQL ya **no debe** incluirse en el proyecto AEM; se implementa mediante el complemento CIF
* Las configuraciones OSGI para el cliente de GraphQL y el servicio de datos Graphql ya **no deben** incluirse en el proyecto AEM.

>[!TIP]
>
>Consulte el proyecto de la [Tienda de referencia de Venia de AEM](https://github.com/adobe/aem-cif-guides-venia) en GitHub. Este proyecto proporciona perfiles Maven para AEM as a Cloud Service e instalaciones on-premise que tienen en cuenta las diferentes condiciones del marco de trabajo.

## Catálogo de productos

Ya no se admite la importación de datos del catálogo de productos. El uso de las solicitudes de producto y catálogo de las entidades principales de complementos del CIF se realiza a petición mediante llamadas en tiempo real a una solución de comercio externo. Vaya al capítulo Integración para obtener más información sobre la integración de una solución de comercio.

>[!TIP]
>
>Si no hay API en tiempo real disponibles, se debe utilizar una caché de producto externo con API para la integración. Ejemplo [Magento de código abierto](https://business.adobe.com/products/magento/open-source.html).

## AEM Experiencias del catálogo de productos con procesamiento de la

Si utiliza el modelo de catálogo con CIF clásico, debe actualizar el flujo de trabajo del catálogo de productos. AEM El complemento CIF ahora procesa las experiencias del catálogo de productos sobre la marcha mediante plantillas de catálogo de productos de la aplicación de la versión de la aplicación de la documentación de la aplicación de la documentación de producto de la aplicación. Ya no se requiere replicación de datos o páginas de productos.

## Interacción de compras y datos no almacenables en caché

Las solicitudes del lado del cliente para datos e interacciones no almacenables en caché (por ejemplo, complementos al carro de compras, búsquedas) deben ir directamente al extremo de comercio (ya sea la solución de comercio o la capa de integración) a través de CDN/Dispatcher. AEM Elimine todas las llamadas en las que solo haya un proxy en el que se haya realizado la.
