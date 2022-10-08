---
title: Migración al complemento AEM Commerce Integration Framework (CIF)
description: Cómo migrar al complemento AEM Commerce Integration Framework (CIF) desde una versión antigua
exl-id: 0db03a05-f527-4853-b52f-f113bce929cf
source-git-commit: ca849bd76e5ac40bc76cf497619a82b238d898fa
workflow-type: tm+mt
source-wordcount: '491'
ht-degree: 45%

---

# Guía de migración para el Experience Manager Cloud Service {#cif-migration}

Esta guía ayuda a identificar las áreas que debe actualizar para la migración de Experience Manager Cloud Service.

## Complemento CIF

Para Experience Manager as a Cloud Service, el complemento CIF es la única solución de integración comercial compatible para Adobe Commerce y soluciones de comercio de terceros. El complemento CIF se implementa automáticamente para los clientes de Experience Manager as a Cloud Service; no se necesita una implementación manual. Consulte [Introducción a AEM Commerce as a Cloud Service](getting-started.md).

Para apoyar proyectos que implementen el Adobe CIF, proporcione [Componentes principales del CIF de AEM](https://github.com/adobe/aem-core-cif-components).

El complemento CIF también está disponible para AEM 6.5 a través del [Portal de distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/es/aem.html). Es compatible y proporciona las mismas características que el complemento CIF para Experience Manager as a Cloud Service: no se requieren ajustes.

El CIF clásico con sus dependencias ya no está disponible. Código que se basa en esta versión del CIF que utiliza `com.adobe.cq.commerce.api` Las API de Java deben ajustarse al complemento CIF y a sus principios.

El conector CIF previamente disponible ya no se puede instalar. El código que se basa en este conector debe ajustarse al complemento CIF y a sus principios.

## Estructura del proyecto

Conozca las [AEM estructura del proyecto](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html?lang=es) y las características de AEM as a Cloud Service. Adapte la configuración del proyecto al diseño de AEM as a Cloud Service.
En comparación con las implementaciones de AEM 6.5, existen dos diferencias principales entre las siguientes:

* El paquete OSGI del cliente de GraphQL ya **no debe** incluirse en el proyecto AEM; se implementa mediante el complemento CIF
* Las configuraciones OSGI para el cliente de GraphQL y el servicio de datos Graphql ya **no deben** incluirse en el proyecto AEM.

>[!TIP]
>
>Consulte el proyecto de la [Tienda de referencia de Venia de AEM](https://github.com/adobe/aem-cif-guides-venia) en GitHub. Este proyecto proporciona perfiles Maven para AEM as a Cloud Service e instalaciones on-premise que tienen en cuenta las diferentes condiciones del marco de trabajo.

## Catálogo de productos

Ya no se admite la importación de datos del catálogo de productos. El uso de las solicitudes de producto y catálogo de los complementos CIF se realiza bajo demanda mediante llamadas en tiempo real a una solución de comercio externa. Vaya a Integrar para obtener más información sobre la integración de una solución de comercio.

>[!TIP]
>
>Si no hay API en tiempo real disponibles, se debe utilizar una caché de producto externa con API para la integración. Ejemplo [Magento de código abierto](https://business.adobe.com/products/magento/open-source.html).

## Experiencias del catálogo de productos con AEM renderización

Si utiliza el modelo de catálogo con CIF clásico, debe actualizar el flujo de trabajo del catálogo de productos. El complemento CIF ahora procesa las experiencias del catálogo de productos sobre la marcha mediante AEM plantillas de catálogo. Ya no es necesaria la duplicación de datos de productos o páginas de productos.

## Interacción de compras y datos no almacenables en caché

Las solicitudes del lado del cliente para datos e interacciones que no se pueden almacenar en caché (por ejemplo, añadir al carro, buscar) deben ir directamente al extremo de comercio (solución de comercio o capa de integración) a través de CDN/Dispatcher. Elimine las llamadas donde AEM era solo un proxy.
