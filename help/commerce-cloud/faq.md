---
title: 'AEM: Preguntas frecuentes sobre la integración comercial con Commerce Integration Framework'
description: 'AEM: Preguntas frecuentes sobre la integración comercial con Commerce Integration Framework'
exl-id: 0a946d98-22c7-445d-984a-9e09c306ce45
source-git-commit: 421ad8506435e8538be9c83df0b78ad8f222df0c
workflow-type: tm+mt
source-wordcount: '969'
ht-degree: 28%

---

# AEM: Preguntas frecuentes sobre la integración comercial con Commerce Integration Framework

## 1. ¿CIF GraphQL solo se utiliza para el comercio o estará disponible para consultar el contenido creado en AEM JCR?

Adobe ha adoptado las API de GraphQL de Adobe Commerce como su API comercial oficial para todos los datos relacionados con el comercio. Por lo tanto, AEM utiliza GraphQL para intercambiar datos de comercio con Adobe Commerce y con cualquier motor de comercio a través de I/O Runtime. Esta API de GraphQL es independiente de AEM API de GraphQL para acceder a los fragmentos de contenido.

## 2. ¿Se pueden almacenar los recursos de producto (imágenes) y hacer referencia a ellos desde AEM a través del administrador de Adobe Commerce? ¿Cómo se pueden consumir los activos de Dynamic Media?

No hay ninguna integración oficial de AEM Assets con Adobe Commerce disponible. Hay un conector de socio disponible en el [marketplace](https://marketplace.magento.com) <!-- THIS IS THE OLD URL THAT WAS USED. IT WAS 404 (https://marketplace.magento.com/bounteous-dam.html) -->

O como solución alternativa, puede almacenar recursos de producto (imágenes) en AEM Assets, pero debe almacenar manualmente las URL de los recursos en Adobe Commerce. Dynamic Media ahora forma parte de AEM Assets y funciona del mismo modo.

## 3. ¿Importa dónde se implemente la solución de comercio? (Local o en la nube)

No, no importa dónde se implemente la solución de comercio. El CIF y la tienda de AEM funcionan independientemente del modelo de implementación. Sin embargo, si la solución se implementa con la arquitectura de referencia E2E recomendada, las pruebas E2E pueden ejecutarse con KPI de rendimiento que representan un perfil de cliente empresarial típico. Este método proporciona información adicional que puede utilizarse como referencia.

## 4. ¿Cómo se crean las páginas de catálogo o de producto en AEM? ¿Cómo persisten en AEM?

Las páginas de catálogo y las páginas de producto se crean y almacenan en caché de forma dinámica en AEM según las plantillas de catálogo y de página de producto genéricas. No se importan ni almacenan datos de producto o catálogo en AEM.

## 5. Cuando actualiza los datos de los productos en su solución de comercio, ¿se trata de un impulso a la AEM en tiempo real? ¿O es un proceso por lotes?

El complemento CIF utilizado con AEM Cloud Service permite que los datos fluyan de la solución de comercio a AEM bajo demanda. Por lo tanto, no se trata de una inserción en tiempo real ni de un proceso por lotes cuando hay una actualización en la solución de comercio.

## 6. ¿Qué tamaño de catálogo AEM con la compatibilidad con CIF?

Esto depende de algunos aspectos adicionales que debe tener en cuenta. ¿Cuál es la proporción de caché de sus datos y páginas de catálogo? ¿Cuántas solicitudes simultáneas espera durante las horas de mayor actividad? ¿Hasta qué punto son escalables las API de sus soluciones de comercio?

## 7. ¿Cómo actúa PIM en este marco?

Los datos de PIM se exponen a AEM y clientes a través de solicitudes de GraphQL. Nuestra recomendación es integrar PIM con el motor de comercio (Adobe Commerce u otros) para que los datos PIM puedan recuperarse del motor de comercio.

## 8. También se almacenan en caché los precios y otros datos a través de Dispatcher. ¿Genera esto un desafío frecuente de invalidación de caché?

Los datos dinámicos, como el precio o el inventario no se almacenan en la caché de Dispatcher. Los datos dinámicos se recuperan del lado del cliente con los componentes web directamente a través de las API de GraphQL. Solo los datos estáticos (como los datos de producto o categoría) se almacenan en la caché de Dispatcher. Si los datos del producto cambian, es necesario invalidar la caché.

## 9. ¿Cómo funciona la invalidación de caché para AEM Dispatcher con AEM y comercio?

Se recomienda configurar la invalidación de caché basada en TTL para las páginas almacenadas en caché de Dispatcher. Para obtener información dinámica como precio o acciones, se recomienda procesar los datos en el lado del cliente. Para obtener más información sobre la invalidación de caché basada en TTL, consulte [Optimización de la caché de Dispatcher](https://experienceleague.adobe.com/docs/experience-cloud-kcs/kbarticles/KA-17458.html) y [Optimización del rendimiento AEM](https://experienceleague.adobe.com/docs/commerce-operations/deliver-commerce-at-scale/performance.html).

## 10. ¿Existe alguna recomendación sobre la búsqueda unificada en los contenidos de AEM con Comercio?

Se proporciona una implementación de referencia de búsqueda de productos, pero no una búsqueda unificada con contenido. Esta función es específica del cliente y se resuelve mejor en un nivel específico del proyecto.

## 11. ¿Cómo funciona Search con AEM y comercio mediante CIF?

CIF proporciona los componentes de la barra de búsqueda y de resultados. El componente Barra de búsqueda envía una solicitud de GraphQL con el término de búsqueda a la solución de comercio que devuelve una lista de productos que incluye el nombre del producto, el precio, el SLUG, etc. A continuación, el componente Resultados de búsqueda muestra los resultados de búsqueda en una vista de galería en una página de resultados de búsqueda creada en AEM. La búsqueda admite la búsqueda básica de texto completo. Utilizamos la clave SLUG/url para crear una referencia al PDP.

## 12. ¿Cómo se pueden utilizar los datos del producto en MSM o en las traducciones?

Los datos del producto ya se han traducido en PIM o en Adobe Commerce. La integración AEM - Adobe Commerce admite la conexión a varias tiendas y vistas de tiendas de Adobe Commerce. En una configuración de MSM, normalmente un sitio AEM está vinculado a una vista de tienda de Adobe Commerce.

## 13. ¿Existe alguna manera de mejorar los datos del producto con texto comercial? ¿Dónde se hace esto? ¿En AEM o en la solución de comercio?

Se recomienda administrar los datos y el contenido relacionados con el marketing en AEM. Decore los datos de productos de su solución de comercio con atributos adicionales mediante fragmentos de contenido o cree y vincule fragmentos de experiencias para contenido no estructurado con sus productos.

## 14. ¿Cómo podemos garantizar el cumplimiento de PCI al utilizar AEM para toda la capa de presentación?

Recomendamos utilizar métodos de pago abstractos. Esto pone al cliente del explorador en comunicación directa con el proveedor de la puerta de enlace de pago, de modo que ni el Adobe ni las soluciones de comercio contienen ni pasan datos del titular de la tarjeta. Este enfoque requiere solamente un cumplimiento de PCI de nivel 3. Sin embargo, hay cosas adicionales que considerar para ser totalmente compatible con PCI, como por ejemplo cómo los empleados interactúan con el sistema y los datos. Para obtener más información sobre la conformidad con PCI Adobe Commerce, consulte [Requisitos de cumplimiento de PCI](https://business.adobe.com/products/magento/pci-compliance.html).

## 15. Si utilizo las versiones en la nube de AEM y Adobe Commerce, ¿esta solución conjunta es compatible con PCI?

Sí, el Cuestionario de Autoevaluación D y la Certificación de Cumplimiento están disponibles bajo petición.

## 16. ¿Cómo puedo solicitar una licencia de prueba de I/O Runtime?

Puede solicitar una licencia de prueba para usar I/O Runtime [aquí](https://developer.adobe.com/app-builder/trial/).
