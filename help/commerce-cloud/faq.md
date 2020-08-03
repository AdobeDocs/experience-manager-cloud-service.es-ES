---
title: 'AEM: Preguntas más frecuentes sobre la integración de Magento mediante Commerce Integration Framework'
description: 'AEM: Preguntas más frecuentes sobre la integración de Magento mediante Commerce Integration Framework'
translation-type: tm+mt
source-git-commit: cafe8825fe34f158c74b94b95b7252394de26e4d
workflow-type: tm+mt
source-wordcount: '1321'
ht-degree: 0%

---


# AEM: Preguntas más frecuentes sobre la integración de Magento mediante Commerce Integration Framework


## 1. ¿GraphQL solo se utiliza para Magento o estará disponible para consultar el contenido creado en AEM JCR?

Adobe ha adoptado las API de GraphQL de Magento como su API comercial oficial para todos los datos relacionados con el comercio. Por lo tanto, AEM utiliza GraphQL para intercambiar datos de comercio con el Magento y con cualquier motor de comercio a través de I/O Runtime.

## 2. ¿Cómo entra en juego la E/S de Adobe? ¿AEM hablar directamente con el Magento?

AEM puede conectarse directamente al Magento sin una capa de tiempo de ejecución de E/S. Si es necesario integrar un back-end de comercio no Magento (solución de terceros) con AEM, la plataforma en tiempo de ejecución de E/S se puede utilizar para alojar la capa de asignación y conectar las API de GraphQL de Magento a cualquier API de soluciones de terceros. Para obtener más información sobre esto, consulte esta implementación [de](https://github.com/adobe/commerce-cif-graphql-integration-reference)referencia. Para las soluciones que no son de Magento, se AEM configurar para que apunten al punto final del tiempo de ejecución de E/S.

La plataforma de tiempo de ejecución de E/S también se puede utilizar para ampliar o personalizar servicios de comercio. Para estos casos de uso, debe llamar al punto final de Tiempo de ejecución de E/S, el cual alojará una implementación personalizada del servicio correspondiente. Se pueden combinar casos de uso de integración y extensión.

## 3. ¿Se pueden almacenar los recursos de producto (imágenes) y hacer referencia a ellos desde AEM mediante el administrador del Magento? ¿Cómo se pueden consumir los recursos de Dynamic Media?

Actualmente no hay AEM Assets: integración de Magento. Como solución alternativa, puede almacenar recursos de productos (imágenes) en AEM Assets, pero tendrá que almacenar manualmente las URL de los recursos en Magento. Dynamic Media es ahora parte de AEM Assets y funcionará de la misma manera.

## 4. ¿Importa dónde se implemente el Magento? (En prem o en la nube)

No importa dónde se implemente el Magento. La integración y el nuevo frente de la tienda Venia AEM funcionarán independientemente del modelo de implementación. Sin embargo, si se implementa en base a la arquitectura de referencia E2E aprobada, las pruebas E2E se ejecutarán en relación con los KPI de rendimiento recopilados que representan el perfil de un cliente empresarial. Esto le proporcionará información adicional que puede utilizar como referencia.

## 5. ¿Cómo se crean las páginas de catálogo o de producto en AEM? ¿Cómo persisten en AEM?

Las páginas de catálogo y las páginas de producto se crean y almacenan en caché de forma dinámica en AEM según plantillas de catálogo y de página de producto genéricas. No se importan ni almacenan datos de producto o catálogo en AEM.

## 6. También almacena en caché los precios y otros datos a través de Dispatcher. ¿Genera esto un desafío frecuente de invalidación de caché?

Los datos dinámicos, como el precio o el inventario, no se almacenan en la caché del Dispatcher. Los datos dinámicos se recuperan del lado del cliente con componentes web directamente a través de las API de GraphQL. Solo los datos estáticos (como los datos de producto o categoría) se almacenan en la caché del Dispatcher. Si los datos del producto cambian, será necesario invalidar la caché.

## 7. ¿Cómo funciona la invalidación de caché para AEM Dispatcher con AEM-Magento?

Se recomienda configurar la invalidación de caché basada en TTL para las páginas almacenadas en caché en el Dispatcher. Para obtener información dinámica como precio o acciones, se recomienda procesar la fecha en el lado del cliente. Para obtener más información sobre la invalidación de caché basada en TTL, consulte [AEM Dispatcher](https://helpx.adobe.com/experience-manager/kb/optimizing-the-dispatcher-cache.html)

## 8. ¿Por qué no utiliza We.Retail?

Se utiliza el tema Venia (desarrollado por el Magento), que es móvil primero y está alineado con el PWA del Magento. El tema Venia representa lo último en términos de estilo CSS y componentes principales AEM.

## 9. Cuando se actualizan los datos del producto en el Magento, ¿se trata de un impulso a AEM en tiempo real? ¿O es un proceso por lotes?

El complemento CIF utilizado con AEM Cloud Service permite que los datos fluyan de Magento a AEM bajo demanda. Por lo tanto, no se trata de un proceso push en tiempo real ni de un proceso por lotes cuando hay una actualización en Magento.

## 10. ¿Existe alguna recomendación sobre la búsqueda unificada en AEM contenido con Commerce?

Se proporciona una implementación de referencia de búsqueda de productos, pero no una búsqueda unificada con contenido. Esta función suele ser muy específica del cliente y se resuelve mejor en un nivel específico del proyecto.

## 11. ¿Cómo funciona Search con AEM-Magento mediante CIF?

CIF proporciona componentes de barra de búsqueda y de resultados de búsqueda. El componente Barra de búsqueda envía una solicitud de GraphQL con el término de búsqueda al Magento. A continuación, el Magento devuelve una lista de producto que incluye el nombre del producto, el precio, el SLUG, etc. A continuación, el componente Resultados de búsqueda muestra los resultados de búsqueda en una vista de galería en una página de resultados de búsqueda creada en AEM. La búsqueda admite la búsqueda básica de texto completo. Utilizamos la clave SLUG/url para crear una referencia al PDP.

## 11. ¿Cómo se pueden utilizar los datos del producto en MSM o en las traducciones?

Los datos del producto generalmente ya se traducen en PIM o en Magento. La integración AEM - Magento admite la conexión a varias tiendas y vistas de tiendas de Magento. En una configuración de MSM, normalmente un sitio AEM está vinculado a una vista de almacén de Magento.

## 13. ¿Cómo actúa CIF con otras plataformas comerciales?

La integración con soluciones de terceros, como otras soluciones comerciales (no Magento), se realiza mediante la plataforma de tiempo de ejecución de E/S.  Hemos creado una implementación [de](https://github.com/adobe/commerce-cif-graphql-integration-reference) referencia para demostrar cómo se hace esto. Esto permite reutilizar el [AEM conector](https://github.com/adobe/commerce-cif-connector) de nube CIF y los componentes [principales de CIF](https://github.com/adobe/aem-core-cif-components) AEM al exponer la API de Magento GraphQL a cualquier plataforma comercial de terceros. Para oferta de la máxima flexibilidad y escalabilidad, esta capa de integración se implementa en la plataforma [](https://www.adobe.io/apis/experienceplatform/runtime.html)Adobe I/O Runtime sin servidor.

## 14. ¿Existe alguna manera de mejorar los datos del producto con texto comercial? ¿Dónde haces esto? ¿En AEM o en Magento?

Existen varias formas de lograrlo y dependerá del caso de uso. Una forma sería trabajar con atributos personalizados. Permita que los autores de AEM muten estos campos en el editor de productos de AEM y sincronicen los datos con el PIM. Otra opción sería aprovechar AEM fragmentos de experiencia que se insertan en las páginas de productos.

## 15. ¿Cambia la integración entre AEM Magento cuando se utiliza la plataforma Adobe I/O Runtime?

Los clientes que deseen ampliar los servicios de comercio pueden utilizar la misma integración y escribir secuencias de acciones alojadas en la plataforma de tiempo de ejecución de E/S para introducir lógica empresarial y enriquecer los servicios de comercio.

## 16. Dado que AEM crea páginas de productos y catálogos dinámicamente basadas en una plantilla genérica en AEM, ¿qué vería si abriera CRXDE Lite y verificara el contenido? ¿Veré un árbol de productos completo basado en los productos del Magento? Si no es así, ¿cómo mejorará un autor esas páginas?

Ya no hay ningún catálogo JCR ni páginas de producto. Véase la pregunta 12.

## 17. ¿Funcionará la tienda de SPA con AEM editor de SPA?

AEM puede utilizarse como herramienta de creación para cualquier tipo de tienda. Actualmente, el procesamiento híbrido se utiliza para el nuevo frente de la tienda. En el futuro, AEM se utilizará para la creación con SPA y PWA.

## 18. ¿Cómo actúa PIM en este marco?

Los datos de PIM se exponen a AEM y clientes a través de solicitudes de GraphQL. Nuestra recomendación es integrar PIM con el motor de comercio (Magento u otro) para que los datos PIM puedan recuperarse del motor de comercio.

## 19. ¿Cómo podemos garantizar el cumplimiento de PCI al utilizar AEM para toda la capa de presentación?

Al utilizar AEM en la implementación de AMS y Magento cloud, es obligatorio utilizar métodos de pago abstractos. Esto pone al cliente del navegador en comunicación directa con el proveedor de la puerta de enlace de pago, de modo que ni las nubes de Adobe ni las de Magento contienen ni pasan datos del titular de la tarjeta. Este enfoque proporciona cobertura para el cumplimiento de PCI para las pilas de tecnología y los centros de datos. Sin embargo, hay cosas adicionales que considerar para ser totalmente compatible con PCI, como por ejemplo cómo los empleados interactúan con el sistema y los datos. Para obtener más información sobre la conformidad con PCI Magento, consulte https://magento.com/pci-compliance

## 20. ¿Cómo puedo solicitar una licencia de prueba de E/S Runtime?

Puede solicitar una licencia de prueba para usar el motor de ejecución de E/S [aquí](https://github.com/AdobeDocs/adobeio-runtime/blob/master/overview/request_a_trial.md).



