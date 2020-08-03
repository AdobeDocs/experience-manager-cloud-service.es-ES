---
title: Introducción al comercio AEM como Cloud Service
description: Novedades en AEM comercio como Cloud Service.
translation-type: tm+mt
source-git-commit: c5694cf8651cf8ba5331c730fa1b1180310dd35a
workflow-type: tm+mt
source-wordcount: '1331'
ht-degree: 1%

---


# Introducción a AEM comercio como Cloud Service {#commerce-intro}

Experience Manager Commerce como Cloud Service consiste en Commerce Integration Framework (CIF), que es el modelo recomendado por el Adobe para integrar y ampliar los servicios comerciales de Magento y otras soluciones comerciales de terceros con el Experience Cloud. Esto permite a los clientes de Adobe ofrecer una extraordinaria y personalizada experiencia de compra de canal omnicho basada en la tecnología más avanzada.

Commerce Integration Framework es un módulo complementario para Experience Manager como Cloud Service y proporciona un conjunto de herramientas de creación, componentes y una tienda de referencia para acelerar el desarrollo de integraciones entre Experience Manager como Cloud Service y soluciones comerciales.

## Beneficios del CIF {#cif-benefits}

Los principales beneficios son:

* La integración es una capa de abstracción para estandarizar y encapsular integraciones con varios sistemas.

* El CIF admite experiencias sin encabezado/omnicho:

   * Aplicaciones de una sola página y aplicaciones de varias páginas
   * Extremos de GraphQL

* El CIF proporciona un proceso sin servidor y basado en microservicios y una capa lógica empresarial para la personalización y ampliación de los servicios comerciales.

* CIF proporciona integraciones integradas integradas con soluciones de Adobe como AEM y Magento

## Elementos CIF {#cif-elements}

![Elementos CIF](/help/commerce-cloud/assets/cif-overview1.jpg)


### Complemento CIF para herramientas de creación {#add-on-authoring-tools}

El complemento CIF proporciona acceso a herramientas de creación de comercio, como la consola de producto, los seleccionadores de productos y Categorías o la búsqueda de productos para los autores, a fin de que puedan crear experiencias enriquecidas con contenido comercial y de marketing. El complemento también administra la conexión de servidor a Magento (o sistema comercial alternativo) mediante GraphQL. Una vez aprovisionado el complemento, se implementa en AEM como entornos de Cloud Service automáticamente.

### Componentes principales de AEM CIF {#aem-cif-core}

Los componentes principales AEM de CIF son componentes procesados del lado del servidor y del lado del cliente con compatibilidad con Magento GraphQL. Se utilizan para crear un almacén comercial estático, accesible y compatible con SEO basado en tecnologías AEM.

Se proporcionan componentes básicos, comunes en implementaciones comerciales como Detalles del producto, Lista del producto, Navegación, Búsqueda, etc. Pueden utilizarse tal cual o ampliarse.

Los [AEM componentes](https://github.com/adobe/aem-core-cif-components) principales de CIF funcionan como los componentes [principales de](https://github.com/adobe/aem-core-wcm-components) AEM Sites, pero se dedican a casos de uso específicos de comercio.

Estos componentes son beneficios clave:

* Son fáciles de usar en sus proyectos.
* Pueden utilizarse tal cual o con modificaciones mínimas.
* Proporcionan optimizaciones para conectarse con Magento mediante las API de GraphQL o REST

Se proporcionan componentes como teaser de productos y carrusel de productos para permitir a los AEM Author crear páginas de experiencia en AEM, combinando contenido comercial y de marketing. Estos componentes se pueden arrastrar y soltar fácilmente en una página de contenido creada en AEM y vinculada a productos o categorías específicos mediante las herramientas de creación de CIF como el Selector de producto o de Categoría en Cloud Service.

Todos los componentes son de código abierto en [GitHub](https://github.com/adobe/aem-core-cif-components). Esto muestra una total transparencia de los cambios realizados en el futuro y le permite obtener la última versión muy fácilmente. También puede proporcionar solicitudes de extracción para mejoras y correcciones de errores que se pueden incorporar.

### Tienda AEM Venia {#aem-venia-storefront}

El [AEM Venia Storefront](https://github.com/adobe/aem-cif-guides-venia) es una moderna tienda de referencia preparada para la producción que muestra un viaje comercial básico de B2C. Se puede utilizar para iniciar proyectos comerciales y acelerar proyectos mediante AEM, CIF y Magento. Muestra las prácticas recomendadas para la integración de AEM y Magento y muestra cómo utilizar los componentes [principales de](https://github.com/adobe/aem-core-cif-components) AEM CIF y los componentes [principales de](https://github.com/adobe/aem-core-wcm-components) AEM Sites y admite los extremos de Adobe Commerce GraphQL. También proporciona a las preventas un sitio de referencia para demostrar la integración entre AEM y Magento.

El AEM Venia Storefront es una aplicación de página mixta en la que AEM posee el vidrio y el Magento enciende el servidor comercial sin cabeza. Tanto el procesamiento del lado del servidor como el del lado del cliente se utilizan en la tienda. El procesamiento del lado del servidor se utiliza para proporcionar contenido estático y el procesamiento del lado del cliente para proporcionar contenido dinámico.

Las páginas de producto y catálogo son relativamente estáticas y se procesan en el servidor mediante componentes principales de AEM CIF, como detalle del producto y Lista del producto, en plantillas genéricas creadas en AEM. Estos componentes obtienen datos de Magento mediante las API de GraphQL.
Estas páginas se crean de forma dinámica, se representan en el servidor, se almacenan en caché en el despachante de AEM y se entregan al explorador.
Para atributos más dinámicos, como inventario o precio, se utilizan componentes del lado del cliente. Los componentes de cliente o los componentes Web recuperan datos directamente de Magento a través de las API de GraphQL y el contenido se procesa en el navegador.

#### Cierre de compra {#checkout}

Esta tienda de referencia utiliza el componente Carro de compras del lado del cliente que procesa el carro de compras y el formulario de cierre de compra para mostrar un patrón de integración de experiencia completa en el que puede ofrecer experiencias comerciales con Magento que se ejecutan de forma totalmente automática y AEM propietarios del vidrio. Se recomienda utilizar los métodos de pago abstractos proporcionados. Esto pone al cliente del navegador en comunicación directa con el proveedor de la puerta de enlace de pago, de modo que ni las nubes de Adobe ni las de Magento contienen ni pasan datos confidenciales de PCI.

#### Administración de cuentas {#account-management}

La administración de cuentas está a cargo del Magento y la tienda de referencia utiliza componentes basados en React del lado del cliente para permitir que AEM la experiencia se muestre en las siguientes funcionalidades: Crear cuenta, iniciar sesión y obtener contraseña.

El proyecto AEM Venia Storefront es de código abierto y para más detalles, consulte [AEM Venia Storefront](https://github.com/adobe/aem-cif-guides-venia).

### Tipo de archivo del proyecto AEM {#aem-project-archtype}

The [AEM Project Archetype](https://docs.adobe.com/content/help/es-ES/experience-manager-core-components/using/developing/archetype/overview.html) can be used to create a minimal, best-practices-based Adobe Experience Manager project as a starting point for your own AEM projects. Opcionalmente, [AEM los componentes](https://github.com/adobe/aem-core-cif-components) principales de CIF se pueden incluir en un proyecto recientemente generado.

### Capa de extensión CIF {#cif-extension}

La capa de extensión CIF es una capa media para alojar una lógica empresarial compleja. Funciona en la plataforma Adobe I/O Runtime, que es la plataforma sin servidor de Adobe. Le permite ampliar las llamadas de servicio end-to-end mediante la inyección de lógica de procesos y negocios en un nivel de microservicio. La lógica comercial sería, por ejemplo, utilizar la ubicación y el canal para determinar una estrategia de inventario. La lógica de proceso sería, por ejemplo, recuperar información personalizada.

### Capa de integración de CIF {#cif-integration-layer}

La capa de integración CIF se utiliza para estandarizar integraciones con otras soluciones comerciales. Se ejecuta en la plataforma Adobe I/O Runtime, que es la plataforma sin servidor de Adobe y permite integraciones a nivel de microservicio mediante la asignación de API de terceros con las API de Adobe Commerce. Para ayudarle a empezar a construir integraciones de terceros con AEM, hemos creado una implementación [de](https://github.com/adobe/commerce-cif-graphql-integration-reference) referencia para demostrar cómo se puede integrar un back-end de comercio no Magento mediante las API de Adobe Commerce (API de Magento GraphQL).

## Patrones de integración de comercio AEM {#aem-commerce-integration}

A continuación se muestran algunos de los patrones de integración de comercio implementados comúnmente AEM.

![Patrones de integración de CIF AEM](/help/commerce-cloud/assets/aem-cif-integration-patterns-updated.JPG)


### Patrón de integración 1 {#integration-pattern-one}

Este es nuestro patrón de integración recomendado donde AEM posee todo el vidrio e integra los servicios comerciales a través de las API de Adobe Commerce GraphQL. Este patrón desbloquea AEM flexibilidad total para adaptar los diseños de sitios de medios enriquecidos en todos los dispositivos. CIF admite este patrón de integración como una solución lista para usar.


### Patrón de integración 2 {#integration-pattern-two}

Este patrón muestra una manera totalmente incompleta de ofrecer contenido y comercio. El envío es totalmente del lado del cliente. En este patrón, el contenido se entrega a través de API y los datos de HTML y comercio se envían a través de GraphQL. Este patrón no está actualmente soportado por CIF incorporado.


### Patrón de integración 3 {#integration-pattern-three}

En este patrón, el Magento es propietario del vidrio e incrusta AEM contenido creado. El contenido AEM creado se puede entregar mediante fragmentos de experiencia o fragmentos de contenido. Este patrón de integración requerirá un trabajo específico del proyecto y no se puede implementar de manera inmediata con CIF.


### Patrón de integración 4 {#integration-pattern-four}

Se trata de un patrón de integración común en el que la capa de cristal o presentación se divide entre AEM y una solución de comercio. Normalmente, la solución Comercio ofrece las páginas que no son de mercadotecnia, como cierre de compra y mi cuenta y AEM ofrece las páginas de mercadotecnia y la experiencia del catálogo de tiendas. En este patrón, debe asegurarse de que los carros de compras y las sesiones de usuario se gestionan correctamente entre los dos sistemas para evitar una experiencia de usuario desvinculada. Por ejemplo: Magento almacena el carro y la sesión del usuario en una cookie, que se puede compartir entre AEM y Magento. Este patrón requerirá un trabajo específico del proyecto y no puede implementarse de manera inmediata con CIF.
