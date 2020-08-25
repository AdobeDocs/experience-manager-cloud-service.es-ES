---
title: Introducción a AEM Commerce as a Cloud Service
description: Novedades en AEM Commerce as a Cloud Service.
translation-type: ht
source-git-commit: c5694cf8651cf8ba5331c730fa1b1180310dd35a
workflow-type: ht
source-wordcount: '1331'
ht-degree: 100%

---


# Presentación de AEM Commerce as a Cloud Service {#commerce-intro}

Experience Manager Comercio as a Cloud Service consiste en el complemento Commerce Integration Framework (CIF), que es el modelo recomendado por Adobe para integrar y ampliar los servicios de comercio de Magento y otras soluciones de comercio de terceros con Experience Cloud. Esto permite a los clientes de Adobe ofrecer una experiencia de compra omnicanal extraordinaria y personalizada con la tecnología más avanzada.

El complemento Commerce Integration Framework es un módulo de complemento para Experience Manager as a Cloud Service y proporciona un conjunto de herramientas de creación, componentes y una referencia de tienda para acelerar el desarrollo de integraciones entre Experience Manager as a Cloud Service y soluciones de comercio.

## Beneficios del CIF {#cif-benefits}

Los principales beneficios son los siguientes:

* La integración es una capa de abstracción para estandarizar y encapsular integraciones con varios sistemas.

* El CIF admite experiencias sin periféricos y omnicanal:

   * Aplicaciones de una sola página y de varias páginas
   * Extremos de GraphQL

* El CIF proporciona un proceso sin servidor y basado en microservicios y una capa de lógica empresarial para la personalización y ampliación de los servicios de comercio.

* CIF proporciona integraciones predeterminadas con las soluciones de Adobe como AEM y Magento

## Elementos del CIF {#cif-elements}

![Elementos del CIF](/help/commerce-cloud/assets/cif-overview1.jpg)


### Complemento CIF para herramientas de creación {#add-on-authoring-tools}

El complemento CIF proporciona acceso a las herramientas de creación de comercio, como la consola de producto, los seleccionadores de productos y categorías o la búsqueda de productos para los autores, a fin de que puedan crear experiencias enriquecidas con contenido comercial y de marketing. El complemento también administra la conexión back-end a Magento (o sistema de comercio alternativo) mediante GraphQL. Una vez aprovisionado el complemento, se implementa en AEM as a Cloud Service automáticamente.

### Componentes principales del CIF de AEM {#aem-cif-core}

Los componentes principales del CIF de AEM son componentes procesados del lado del servidor y del lado del cliente con compatibilidad con Magento GraphQL. Se utilizan para crear un almacén de comercio estático, accesible y compatible con SEO basado en tecnologías AEM.

Se proporcionan componentes básicos y comunes en implementaciones de comercio como Detalles del producto, Lista del producto, Navegación, Búsqueda, etc. Pueden utilizarse tal cual o ampliarse.

Los [componentes principales del CIF de AEM](https://github.com/adobe/aem-core-cif-components) funcionan como los [componentes principales de AEM Sites](https://github.com/adobe/aem-core-wcm-components), pero se dedican a casos de uso específicos de comercio.

Estos componentes son beneficios clave:

* Son fáciles de usar en sus proyectos.
* Pueden utilizarse tal cual o con modificaciones mínimas.
* Proporcionan optimizaciones para conectarse con Magento mediante las API de GraphQL o REST.

Se proporcionan componentes como teaser y carrusel de productos para permitir a los autores de AEM crear páginas de Experience en AEM, combinando contenido comercial y de marketing. Estos componentes se pueden arrastrar y soltar fácilmente en una página de contenido creada en AEM y vinculada a productos o categorías específicos con las herramientas de creación del CIF como el seleccionador de productos y categorías en Cloud Service.

Todos los componentes son de código abierto en [GitHub](https://github.com/adobe/aem-core-cif-components). Esto muestra una total transparencia de los cambios realizados en el futuro y le permite obtener la última versión muy fácilmente. También puede proporcionar solicitudes de extracción para mejoras y correcciones de errores que se pueden incorporar.

### Tienda Venia en AEM {#aem-venia-storefront}

La [Tienda Venia en AEM](https://github.com/adobe/aem-cif-guides-venia) es una tienda de referencia moderna y preparada para la producción que muestra el viaje comercial básico de B2C. Se puede utilizar para iniciar proyectos de comercio y acelerar proyectos con AEM, CIF y Magento. Muestra las prácticas recomendadas para la integración de AEM y Magento y muestra cómo utilizar los [componentes principales del CIF de AEM](https://github.com/adobe/aem-core-cif-components) y los [componentes principales de AEM Sites](https://github.com/adobe/aem-core-wcm-components) y admite los extremos de Adobe Commerce GraphQL. También proporciona a las preventas un sitio de referencia para demostrar la integración entre AEM y Magento.

La Tienda Venia en AEM es una aplicación de página mixta en la que AEM posee el vidrio y el Magento enciende el servidor de comercio back-end sin periféricos. En la tienda se utilizan tanto el procesamiento del lado del servidor como el del lado del cliente. El procesamiento del lado del servidor se utiliza para proporcionar contenido estático y el procesamiento del lado del cliente para proporcionar contenido dinámico.

Las páginas de producto y catálogo son relativamente estáticas y se procesan en el servidor mediante componentes principales del CIF de AEM, como detalle del producto y Lista del producto, en plantillas genéricas creadas en AEM. Estos componentes obtienen datos de Magento mediante las API de GraphQL.
Estas páginas se crean de forma dinámica, se representan en el servidor, se almacenan en caché en AEM Dispatcher y se entregan al explorador.
Para atributos más dinámicos, como inventario o precio, se utilizan componentes del lado del cliente. Los componentes del lado del cliente o los componentes web recuperan datos directamente de Magento a través de las API de GraphQL y el contenido se procesa en el explorador.

#### Cierre de compra {#checkout}

Esta tienda de referencia utiliza el componente carro de compras del lado del cliente que procesa el carro de compras y el formulario de cierre de compra, así muestra un patrón de integración de experiencia completa que puede ofrecer experiencias de comercio con Magento y se ejecuta de forma totalmente automática, siendo AEM el propietario del vidrio. Se recomienda utilizar los métodos de pago abstractos proporcionados. Esto pone al cliente del explorador en comunicación directa con el proveedor de la puerta de enlace de pago, de modo que ni las nubes de Adobe ni las de Magento contienen ni pasan datos confidenciales de PCI.

#### Administración de cuentas {#account-management}

La administración de cuentas está a cargo de Magento y la tienda de referencia utiliza componentes basados en React del lado del cliente para permitir que AEM pueda ofrecer la experiencia para las siguientes funcionalidades: Crear cuenta, iniciar sesión y obtener contraseña.

El proyecto Tienda Venia en AEM es de código abierto y para más detalles, consulte [Tienda Venia en AEM](https://github.com/adobe/aem-cif-guides-venia).

### Tipo de archivo del proyecto AEM {#aem-project-archtype}

El [Tipo de archivo del proyecto AEM](https://docs.adobe.com/content/help/es-ES/experience-manager-core-components/using/developing/archetype/overview.html) se puede usar para crear un proyecto mínimo de Adobe Experience Manager basado en las prácticas recomendadas como punto de partida para sus propios proyectos AEM. De forma opcional, los [componentes principales del CIF de AEM](https://github.com/adobe/aem-core-cif-components) se pueden incluir en un proyecto recientemente generado.

### Capa de extensión del CIF {#cif-extension}

La capa de extensión del CIF es una capa media para alojar lógicas empresariales complejas. Funciona en la plataforma Adobe I/O Runtime, que es la plataforma sin servidor de Adobe. Le permite ampliar las llamadas de servicio de un extremo a otro con lógica empresarial para los procesos a un nivel de microservicio. La lógica empresarial sería, por ejemplo, utilizar la ubicación y el canal para determinar una estrategia de inventario. La lógica de proceso sería, por ejemplo, recuperar información personalizada.

### Capa de integración del CIF {#cif-integration-layer}

La capa de integración del CIF se utiliza para estandarizar las integraciones con otras soluciones de comercio. Funciona en la plataforma Adobe I/O Runtime, que es la plataforma sin servidor de Adobe y permite integraciones a nivel de microservicio mediante la asignación de API de terceros con las API de Adobe Commerce. Para ayudarle a empezar a construir integraciones de terceros con AEM, hemos creado una [implementación de referencia](https://github.com/adobe/commerce-cif-graphql-integration-reference) para demostrar cómo se puede integrar un back-end de comercio diferente de Magento mediante las API de Adobe Commerce (API de Magento GraphQL).

## Patrones de integración de AEM Commerce {#aem-commerce-integration}

A continuación se muestran algunos de los patrones de integración de AEM Commerce implementados comúnmente.

![Patrones de integración del CIF de AEM](/help/commerce-cloud/assets/aem-cif-integration-patterns-updated.JPG)


### Patrón de integración 1 {#integration-pattern-one}

Este es nuestro patrón de integración recomendado donde AEM posee todo el vidrio e integra los servicios comerciales a través de las API de Adobe Commerce GraphQL. Este patrón desbloquea la flexibilidad total de AEM para adaptar los diseños de sitios de medios enriquecidos en todos los dispositivos. CIF admite este patrón de integración como una solución predeterminada.


### Patrón de integración 2 {#integration-pattern-two}

Este patrón muestra una manera totalmente incompleta de ofrecer contenido y comercio. El envío es totalmente del lado del cliente. En este patrón, el contenido se entrega a través de la API y los datos de HTML y comercio se envían a través de GraphQL. Actualmente, CIF no admite este patrón de manera predeterminada.


### Patrón de integración 3 {#integration-pattern-three}

En este patrón, Magento es propietario del vidrio e incrusta el contenido creado por AEM. El contenido creado por AEM se puede entregar mediante fragmentos de experiencias o fragmentos de contenidos. Este patrón de integración requerirá un trabajo específico del proyecto y no se puede implementar de manera predeterminada con CIF.


### Patrón de integración 4 {#integration-pattern-four}

Se trata de un patrón de integración común en el que el vidrio o la capa de presentación se dividen entre AEM y una solución de comercio. Normalmente, la solución de comercio ofrece páginas diferentes de marketing, como cierre de compra y Mi cuenta y AEM ofrece las páginas de marketing y la experiencia del catálogo de tiendas. En este patrón, debe asegurarse de que los carros de compras y las sesiones de los usuarios se gestionen correctamente entre los dos sistemas para evitar una experiencia del usuario inconexa. Por ejemplo: Magento almacena el carro de compras y la sesión del usuario en una cookie que se puede compartir entre AEM y Magento. Este patrón requerirá un trabajo específico del proyecto y no se puede implementar de manera predeterminada con CIF.
