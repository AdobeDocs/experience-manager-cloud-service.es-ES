---
title: AEM Integración de comercio de terceros y de terceros con Commerce Integration Framework
description: Los negocios empresariales pueden requerir soluciones de comercio de terceros adicionales para impulsar su tienda. Commerce Integration Framework (CIF) se puede utilizar en estos escenarios de integración para conectar una solución de comercio de terceros a Adobe Experience Manager mediante I/O Runtime.
thumbnail: cif-third-party-architecture.jpg
exl-id: 3ebdb8eb-65ba-46be-aca3-6c06c8d1600c
source-git-commit: 1994b90e3876f03efa571a9ce65b9fb8b3c90ec4
workflow-type: tm+mt
source-wordcount: '509'
ht-degree: 2%

---

# AEM Integración de comercio de terceros y de terceros con Commerce Integration Framework {#aem-third-party}

La integración de soluciones diferentes de Adobe Commerce es un escenario común para CIF. Las soluciones de terceros con diferentes API y esquemas se conectan mediante una capa de integración.

## Arquitectura {#architecture}

La arquitectura general es la siguiente:

![AEM Información general sobre la arquitectura de terceros/sin Magento de datos](../assets//AEM_nonMagento_Architecture.png)

El propósito de esta capa de integración es asignar API y esquemas de terceros a las API y esquemas de Adobe Commerce GraphQL compatibles fuera del Experience Manager. Gracias a esta encapsulación, la lógica y los sistemas de integración pueden actualizarse sin cambiar el código dentro del Experience Manager.

## Requisitos de solución para una integración

A medida que el Experience Manager recupera los datos bajo demanda, se requieren API en tiempo real para el catálogo de productos.

>[!TIP]
>
>Si no hay API en tiempo real disponibles, se debe utilizar una caché de producto externo con API para la integración. Ejemplo [Adobe Commerce Open Source](https://business.adobe.com/products/magento/open-source.html).

No es necesario implementar el esquema GraphQL completo, solo los objetos del esquema para habilitar los casos de uso deseados.

## Casos de uso back-end

CIF amplía el Experience Manager con acceso al catálogo de productos en tiempo real y herramientas de administración de experiencias de producto. Esta integración perfecta permite a los autores acceder a los datos de comercio mediante IU incrustadas siempre que sea necesario sin salir del contexto de contenido.

Las integraciones de las API del catálogo de productos son necesarias para desbloquear estos casos de uso.

## Casos de uso de front-end

[AEM Componentes principales de CIF](https://github.com/adobe/aem-core-cif-components) recupere e intercambie datos a través de las API de Adobe Commerce compatibles con el CIF. Para reutilizar componentes, se deben implementar las API respectivas.

La recomendación para los componentes del lado del cliente esenciales para el rendimiento es comunicarse directamente con la solución de terceros para evitar la latencia.

## Desarrollo de una integración {#develop-integration}

El Adobe recomienda que utilice [Adobe Developer Runtime](https://developer.adobe.com/runtime/) para la capa de integración. Se incluye en el complemento CIF para terceros. Como funciona con un enfoque similar a un microservicio, es adecuado para integrar fácilmente varias soluciones.

El [implementación de referencia](https://github.com/adobe/commerce-cif-graphql-integration-reference) es un bueno punto de partida para integrar en su solución de comercio. Aunque es compatible con GraphQL, también se puede integrar con cualquier otro tipo de API, como REST.

Esta capa de integración no es necesaria si hay una capa de terceros disponible (por ejemplo, Mulesoft) o la integración se crea sobre la solución de terceros.

## Conectores creados previamente {#connectors}

Los conectores son un buen punto de partida para los proyectos. Vienen con una conexión específica de la solución de comercio y una asignación de API predeterminada. Estos conectores son construidos por terceros y no mantenidos por Adobe. Póngase en contacto con el socio correspondiente para obtener información.

* [SAP Commerce](https://github.com/diconium/commerce-cif-graphql-integration-hybris), creado por Diconium
* [Herramientas comerciales](https://github.com/diconium/commerce-cif-graphql-integration-commercetool), creado por Diconium

>[!TIP]
>
>Aunque los conectores ayudan a los proyectos a acelerar la integración comercial, no son plug-n-play. Las soluciones de comercio empresarial están muy personalizadas y requieren una integración personalizada. Se requiere un buen conocimiento de la plataforma de comercio, los esquemas de Adobe Commerce GraphQL y Adobe I/O Runtime.
