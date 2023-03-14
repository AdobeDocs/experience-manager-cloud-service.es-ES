---
title: AEM - Preguntas frecuentes sobre la integración de Commerce con Commerce Integration Framework
description: AEM - Preguntas frecuentes sobre la integración de Commerce con Commerce Integration Framework
exl-id: 0a946d98-22c7-445d-984a-9e09c306ce45
source-git-commit: d925310603961f1f3721c283fc247105459e9c0f
workflow-type: tm+mt
source-wordcount: '969'
ht-degree: 28%

---

# AEM - Preguntas frecuentes sobre la integración de Commerce con Commerce Integration Framework

## 1. ¿CIF GraphQL AEM solo se utiliza para el comercio o estará disponible para consultar el contenido creado en JCR

El Adobe ha adoptado las API de GraphQL de Adobe Commerce como su API comercial oficial para todos los datos relacionados con el comercio. AEM Por lo tanto, utiliza GraphQL para intercambiar datos de comercio con Adobe Commerce y con cualquier motor de comercio a través de I/O Runtime. Esta API de GraphQL AEM es independiente de la API de GraphQL para acceder a los fragmentos de contenido.

## AEM 2. ¿Se pueden almacenar los activos de producto (imágenes) y hacer referencia a ellos desde la administración de Adobe Commerce a través de la administración de la? ¿Cómo se pueden consumir los activos de Dynamic Media?

No hay ninguna integración oficial de AEM Assets con Adobe Commerce disponible. Hay un conector de socio disponible en la [mercado](https://marketplace.magento.com) <!-- THIS IS THE OLD URL THAT WAS USED. IT WAS 404 (https://marketplace.magento.com/bounteous-dam.html) -->

O como solución alternativa, puede almacenar los recursos de productos (imágenes) en AEM Assets, pero debe almacenar manualmente las direcciones URL de los recursos en Adobe Commerce. Dynamic Media ahora forma parte de AEM Assets y funciona del mismo modo.

## 3. ¿Importa dónde se implemente la solución de comercio? (Local o en la nube)

No, no importa dónde se implemente su solución de comercio. AEM CIF y la tienda de funcionan independientemente del modelo de implementación. Sin embargo, si la solución se implementa con la arquitectura de referencia E2E recomendada, las pruebas E2E pueden ejecutarse con KPI de rendimiento que representen un perfil de cliente empresarial típico. Este método proporciona información adicional que puede utilizarse como referencia.

## 4. ¿Cómo se crean las páginas de catálogo o de producto en AEM? ¿Cómo persisten en AEM?

Las páginas de catálogo y las páginas de producto se crean y almacenan en caché de forma dinámica en AEM según las plantillas de catálogo y de página de producto genéricas. AEM No se importan ni almacenan datos de producto o catálogo en los recursos de la.

## AEM 5. Cuando se actualizan los datos del producto en la solución de comercio, ¿se trata de una inserción en tiempo real a la dirección de correo electrónico de la solución de comercio de los clientes ¿O es un proceso por lotes?

El complemento CIF utilizado con AEM Cloud Service AEM permite que los datos fluyan de la solución de comercio a la solución bajo demanda, a la vez que se. Por lo tanto, no se trata de una inserción en tiempo real ni de un proceso por lotes cuando hay una actualización en la solución de comercio.

## AEM 6. ¿Qué tamaño de catálogo es compatible con el CIF en la actualidad?

Esto depende de algunos aspectos adicionales que debe tener en cuenta. ¿Cuál es la proporción de caché de los datos y las páginas del catálogo? ¿Cuántas solicitudes simultáneas espera durante las horas de mayor actividad? ¿En qué medida son escalables las API de sus soluciones de comercio?

## 7. ¿Cómo actúa PIM en este marco?

Los datos de PIM se exponen a AEM y clientes a través de solicitudes de GraphQL. Nuestra recomendación es integrar PIM con el motor de comercio (Adobe Commerce u otros) para que los datos PIM puedan recuperarse del motor de comercio.

## 8. También se almacenan en caché los precios y otros datos a través de Dispatcher. ¿Genera esto un desafío frecuente de invalidación de caché?

Los datos dinámicos, como el precio o el inventario no se almacenan en la caché de Dispatcher. Los datos dinámicos se recuperan del lado del cliente con los componentes web directamente a través de las API de GraphQL. Solo los datos estáticos (como los datos de producto o categoría) se almacenan en la caché de Dispatcher. Si los datos del producto cambian, es necesario invalidar la caché.

## AEM AEM 9. ¿Cómo funciona la invalidación de caché para Dispatcher de la con los recursos de comercio y de comercio de Dispatcher?

Se recomienda configurar la invalidación de caché basada en TTL para las páginas almacenadas en caché de Dispatcher. Para obtener información dinámica como precio o acciones, se recomienda procesar los datos del lado del cliente. Para obtener más información sobre la invalidación de caché basada en TTL, consulte [Optimizar la caché de Dispatcher](https://experienceleague.adobe.com/docs/experience-cloud-kcs/kbarticles/KA-17458.html) y [AEM Optimización del rendimiento](https://experienceleague.adobe.com/docs/commerce-operations/deliver-commerce-at-scale/performance.html).

## 10. ¿Existe alguna recomendación sobre la búsqueda unificada en los contenidos de AEM con Comercio?

Se proporciona una implementación de referencia de búsqueda de productos, pero no una búsqueda unificada con contenido. Esta función es específica del cliente y se resuelve mejor en un nivel específico del proyecto.

## AEM 11. ¿Cómo funciona la búsqueda con el comercio y el comercio con el uso de CIF?

CIF proporciona los componentes de la barra de búsqueda y de resultados. El componente Barra de búsqueda envía una solicitud de GraphQL con el término de búsqueda a la solución de comercio que, a continuación, devuelve una lista de productos que incluye el nombre del producto, el precio, el SLUG, etc. A continuación, el componente Resultados de búsqueda muestra los resultados de búsqueda en una vista de galería en una página de resultados de búsqueda creada en AEM. La búsqueda admite la búsqueda básica de texto completo. Utilizamos la clave SLUG/url para crear una referencia al PDP.

## 12. ¿Cómo se pueden utilizar los datos del producto en MSM o en las traducciones?

Los datos del producto ya se han traducido en PIM o en Adobe Commerce. AEM La integración de Adobe Commerce - de la admite la conexión a varias tiendas y vistas de tiendas de Adobe Commerce. AEM En una configuración de MSM, normalmente un sitio de está vinculado a una vista de tienda de Adobe Commerce.

## 13. ¿Existe alguna manera de mejorar los datos del producto con texto comercial? ¿Dónde se hace esto? AEM ¿En la solución de comercio o en la solución de comercio?

AEM Se recomienda administrar los datos y el contenido relacionados con el marketing en el área de trabajo de. Decore los datos de producto de su solución de comercio con atributos adicionales mediante fragmentos de contenido o cree y vincule fragmentos de experiencias para contenido no estructurado con sus productos.

## 14. ¿Cómo podemos garantizar el cumplimiento de PCI al utilizar AEM para toda la capa de presentación?

Recomendamos el uso de métodos de pago abstractos. Esto pone al cliente del explorador en comunicación directa con el proveedor de la puerta de enlace de pago, de modo que ni el Adobe ni las soluciones comerciales contienen ni pasan los datos del titular de la tarjeta. Este enfoque solo requiere un nivel 3 de conformidad con PCI. Sin embargo, hay cosas adicionales que considerar para que sea totalmente compatible con PCI, como por ejemplo cómo los empleados interactúan con el sistema y los datos. Para obtener más información sobre la conformidad con PCI Adobe Commerce, consulte [Requisitos de cumplimiento de PCI](https://business.adobe.com/products/magento/pci-compliance.html).

## AEM 15. Si utilizo versiones en la nube de Adobe Commerce y de la plataforma de datos, ¿es compatible esta solución conjunta con PCI?

Sí, el cuestionario de autoevaluación D y la certificación de conformidad están disponibles bajo petición.

## 16. ¿Cómo puedo solicitar una licencia de prueba de I/O Runtime?

Puede solicitar una licencia de prueba para usar I/O Runtime [aquí](https://developer.adobe.com/app-builder/trial/).
