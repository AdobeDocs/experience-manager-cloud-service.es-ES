---
title: Preguntas frecuentes sobre la integración de AEM con Commerce mediante Commerce Integration Framework
description: Preguntas frecuentes sobre la integración de AEM con Commerce mediante Commerce Integration Framework
exl-id: 0a946d98-22c7-445d-984a-9e09c306ce45
feature: Commerce Integration Framework
role: Admin, Architect, User
source-git-commit: 80bd8da1531e009509e29e2433a7cbc8dfe58e60
workflow-type: tm+mt
source-wordcount: '960'
ht-degree: 97%

---


# Preguntas frecuentes sobre la integración de AEM con Commerce mediante Commerce Integration Framework

## &#x200B;1. ¿GraphQL solo se utiliza para Commerce o estará disponible para consultar el contenido creado en JCR de AEM? {#faq-1}

Adobe ha adoptado las API GraphQL de Adobe Commerce como sus API comerciales oficiales para todos los datos relacionados con el comercio. Por lo tanto, AEM utiliza GraphQL para intercambiar datos de comercio con Adobe Commerce y con cualquier motor de comercio a través de I/O Runtime. Esta API de GraphQL es independiente de la API GraphQL de AEM para acceder a los fragmentos de contenido.

## &#x200B;2. ¿Se pueden almacenar los activos de producto (imágenes) y hacer referencia a ellos desde AEM mediante el administrador de Adobe Commerce? ¿Cómo se pueden consumir los activos de Dynamic Media? {#faq-2}

No hay ninguna integración oficial de AEM Assets con Adobe Commerce disponible. Hay un conector de socio disponible en [Marketplace.](https://commercemarketplace.adobe.com)

Como solución alternativa, puede almacenar los recursos de productos (imágenes) en AEM Assets, pero tendrá que almacenar manualmente las URL de los recursos en Adobe Commerce. Dynamic Media ahora forma parte de AEM Assets y funciona de la misma manera.

## &#x200B;3. ¿Importa dónde se implemente la solución de comercio? (Local o en la nube) {#faq-3}

No, no importa dónde se implemente su solución de comercio. El escaparate de CIF y AEM funciona independientemente del modelo de implementación. Sin embargo, si la solución se implementa con la arquitectura de referencia E2E recomendada, las pruebas E2E pueden ejecutarse con KPI de rendimiento que representen un perfil de cliente empresarial típico. Este método proporciona información adicional que puede utilizarse como referencia.

## &#x200B;4. ¿Cómo se crean las páginas de catálogo o de producto en AEM? ¿Cómo persisten en AEM? {#faq-4}

Las páginas de catálogo y las páginas de producto se crean y almacenan en caché de forma dinámica en AEM según las plantillas de catálogo y de página de producto genéricas. No se importan ni almacenan datos de producto o catálogo en AEM.

## &#x200B;5. Cuando se actualizan los datos del producto en su solución de comercio, ¿se trata de una inserción a AEM en tiempo real? ¿O es un proceso por lotes? {#faq-5}

El complemento CIF utilizado con AEM Cloud Service permite que los datos fluyan de solución de comercio a AEM bajo demanda. Por lo tanto, no se trata de una inserción en tiempo real ni de un proceso por lotes cuando hay una actualización en su solución de comercio.

## &#x200B;6. ¿Qué tamaño de catálogo admite AEM con CIF? {#faq-6}

Esto depende de algunos aspectos adicionales que debe tener en cuenta. ¿Cuál es la proporción de caché de los datos y las páginas del catálogo? ¿Cuántas solicitudes simultáneas espera durante las horas de mayor actividad? ¿En qué medida son escalables las API de sus soluciones de comercio?

## &#x200B;7. ¿Cómo actúa GIP en este marco? {#faq-7}

Los datos de GIP se exponen a AEM y clientes a través de solicitudes de GraphQL. Nuestra recomendación es integrar GIP con el motor de comercio (Adobe Commerce u otro) para que los datos de GIP puedan recuperarse del motor de comercio.

## &#x200B;8. También se almacenan en caché los precios y otros datos a través de Dispatcher. ¿Genera esto un desafío frecuente de invalidación de caché? {#faq-8}

Los datos dinámicos, como el precio o el inventario no se almacenan en la caché de Dispatcher. Los datos dinámicos se recuperan del lado del cliente con los componentes web directamente a través de las API de GraphQL. Solo los datos estáticos (como los datos de producto o categoría) se almacenan en la caché de Dispatcher. Si los datos del producto cambian, es necesario invalidar la caché.

## &#x200B;9. ¿Cómo funciona la invalidación de caché para Dispatcher de AEM con AEM y Commerce? {#faq-9}

Adobe recomienda configurar la invalidación de caché basada en TTL para las páginas almacenadas en caché de Dispatcher. Para obtener información dinámica como precio o acciones, Adobe recomienda procesar los datos del lado del cliente. Para obtener más información sobre la invalidación de caché basada en TTL, consulte [Optimizar la caché de Dispatcher.](https://experienceleague.adobe.com/docs/experience-cloud-kcs/kbarticles/KA-17458.html?lang=es)

## &#x200B;10. ¿Existe alguna recomendación sobre la búsqueda unificada en los contenidos de AEM con Comercio? {#faq-10}

Se proporciona una implementación de referencia de búsqueda de productos, pero no una búsqueda unificada con contenido. Esta función es específica del cliente y se resuelve mejor en un nivel específico del proyecto.

## &#x200B;11. ¿Cómo funciona la búsqueda con AEM y Commerce mediante CIF? {#faq-11}

CIF proporciona los componentes de la barra de búsqueda y el resultado de búsqueda. El componente Barra de búsqueda envía una solicitud de GraphQL con el término de búsqueda a la solución de comercio que, a continuación, devuelve una lista de productos que incluye el nombre del producto, el precio, las anotaciones, etc. A continuación, el componente Resultados de búsqueda muestra los resultados de búsqueda en una vista de galería en una página de resultados de búsqueda creada en AEM. La búsqueda admite la búsqueda básica de texto completo. Utilizamos la clave SLUG/url para crear una referencia al PDP.

## &#x200B;12. ¿Cómo se pueden utilizar los datos del producto en MSM o en las traducciones? {#faq-12}

Los datos del producto generalmente ya están trasladados en GIP o en Adobe Commerce. La integración de AEM y Adobe Commerce admite la conexión a varias tiendas y vistas de tiendas de Adobe Commerce. En una configuración de MSM, normalmente un sitio de AEM está vinculado a una vista de tienda de Adobe Commerce.

## &#x200B;13. ¿Existe alguna manera de mejorar los datos del producto con texto comercial? ¿Dónde se hace esto? ¿En AEM o en la solución de comercio? {#faq-13}

Adobe recomienda administrar los datos y el contenido relacionados con el marketing en AEM. Incluya los datos de producto de su solución de comercio y atributos adicionales mediante fragmentos de contenido o cree y vincule fragmentos de experiencias para contenido no estructurado con sus productos.

## &#x200B;14. ¿Cómo se puede garantizar el cumplimiento de PCI al utilizar AEM para toda la capa de presentación? {#faq-14}

Adobe recomienda utilizar métodos de pago abstractos. Esto pone al cliente del explorador en comunicación directa con el proveedor de la puerta de enlace de pago, de modo que ni Adobe ni las soluciones de comercio contienen ni pasan los datos del titular de la tarjeta. Este enfoque solo requiere un nivel 3 de conformidad con PCI. Sin embargo, hay cosas adicionales que considerar para que sea totalmente compatible con PCI, como por ejemplo cómo los empleados interactúan con el sistema y los datos. Para obtener más información acerca del cumplimiento de PCI Adobe Commerce, consulte [Requisitos de cumplimiento de PCI.](https://business.adobe.com/products/magento/pci-compliance.html?lang=es)

## &#x200B;15. Si utilizo versiones en la nube de AEM y Adobe Commerce, ¿es compatible esta solución conjunta con PCI? {#faq-15}

Sí, el cuestionario de autoevaluación D y la certificación de conformidad están disponibles bajo petición.

## &#x200B;16. ¿Cómo puedo solicitar una licencia de prueba de I/O Runtime? {#faq-16}

Consulte [Obtener acceso](https://developer.adobe.com/runtime/docs/guides/overview/getting_access/) para obtener detalles sobre cómo solicitar una licencia de prueba para usar I/O Runtime.
