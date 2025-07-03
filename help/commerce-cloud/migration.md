---
title: Migración al complemento de AEM Commerce integration framework (CIF)
description: Migración al complemento AEM Commerce integration framework (CIF) desde una versión antigua
exl-id: 0db03a05-f527-4853-b52f-f113bce929cf
feature: Commerce Integration Framework
role: Admin
index: false
source-git-commit: 173b70aa6f9ad848d0f80923407bf07540987071
workflow-type: tm+mt
source-wordcount: '470'
ht-degree: 38%

---

# Guía de migración para Experience Manager Cloud Service {#cif-migration}

Esta guía ayuda a identificar las áreas que debe actualizar para la migración de Experience Manager Cloud Service.

## Complemento de CIF

Para Experience Manager as a Cloud Service, el complemento de CIF es la única solución de integración comercial compatible para Adobe Commerce y soluciones de comercio de terceros. El complemento CIF se implementa automáticamente para los clientes de Experience Manager as a Cloud Service; no se necesita una implementación manual. Consulte [Introducción a AEM Commerce as a Cloud Service](getting-started.md).

Para admitir proyectos que implementen CIF Adobe, proporcione [Componentes principales de AEM CIF](https://github.com/adobe/aem-core-cif-components).

El complemento CIF también está disponible para AEM 6.5 a través del [Portal de distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/es/aem.html). Es compatible y proporciona las mismas características que el complemento CIF para Experience Manager as a Cloud Service: no se requieren ajustes.

El CIF clásico con sus dependencias ya no está disponible. El código que se basa en esta versión de CIF que usa `com.adobe.cq.commerce.api` API de Java debe ajustarse al complemento de CIF y a sus principios.

El conector de CIF disponible anteriormente ya no se puede instalar. El código que se basa en este conector debe ajustarse al complemento CIF y a sus principios.

## Estructura del proyecto

Conozca la [Estructura del proyecto AEM](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html?lang=es) y las características de AEM as a Cloud Service. Adapte la configuración del proyecto al diseño de AEM as a Cloud Service.
En comparación con las implementaciones de AEM 6.5, existen dos diferencias principales:

* El paquete OSGI del cliente de GraphQL ya **no debe** incluirse en el proyecto AEM; se implementa mediante el complemento CIF
* Las configuraciones OSGI para el cliente de GraphQL y el servicio de datos Graphql ya **no deben** incluirse en el proyecto AEM.

>[!TIP]
>
>Consulte el proyecto de la [Tienda de referencia de Venia de AEM](https://github.com/adobe/aem-cif-guides-venia) en GitHub. Este proyecto proporciona perfiles Maven para AEM as a Cloud Service e instalaciones on-premise que tienen en cuenta las diferentes condiciones del marco de trabajo.

## Catálogo de productos

Ya no se admite la importación de datos del catálogo de productos. El uso de las solicitudes de producto y catálogo de las entidades de seguridad de complementos de CIF se realiza a petición mediante llamadas en tiempo real a una solución de comercio externo. Vaya al capítulo Integración para obtener más información sobre la integración de una solución de comercio.

>[!TIP]
>
>Si no hay API en tiempo real disponibles, se debe utilizar una caché de producto externo con API para la integración. Ejemplo [Magento open-source](https://business.adobe.com/products/magento/open-source.html).

## Experiencias del catálogo de productos con procesamiento en AEM

Si utiliza el modelo de catálogo con CIF clásico, debe actualizar el flujo de trabajo del catálogo de productos. El complemento de CIF ahora procesa las experiencias del catálogo de productos sobre la marcha mediante plantillas de catálogo de AEM. Ya no se requiere replicación de datos o páginas de productos.

## Interacción de compras y datos no almacenables en caché

Las solicitudes del lado del cliente para datos e interacciones no almacenables en caché (por ejemplo, complemento al carro, búsqueda) deben ir directamente al extremo de comercio (ya sea la solución de comercio o la capa de integración) a través de CDN/Dispatcher. Elimine cualquier llamada en la que AEM sea solo un proxy.
