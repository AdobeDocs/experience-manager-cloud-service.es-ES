---
title: Dynamic Media con funciones de OpenAPI
description: Conozca conceptos clave como por qué utilizar Dynamic Media con las capacidades de OpenAPI y cómo habilitarlo.
role: User
source-git-commit: 0ad9f349c997c35862e4f571b4741ed4c0c947e2
workflow-type: tm+mt
source-wordcount: '906'
ht-degree: 0%

---

# Dynamic Media con funciones de OpenAPI {#new-dynaminc-media-apis-overview}

En el acelerado mundo digital actual, desbloquear todo el potencial de los activos digitales de su marca es crucial para mantenerse por delante de la competencia. Una solución integral de administración de activos digitales (DAM) facilita la administración de los recursos, promueve la coherencia de la marca y acelera la entrega de contenido a la vez que garantiza la integridad de la marca y experiencias de cliente excepcionales.

Dynamic Media con capacidades OpenAPI coloca a DAM en el centro de un ecosistema de cadena de suministro de contenido ágil y eficiente para garantizar la gobernanza y la entrega de los recursos.

## ¿Por qué utilizar Dynamic Media con las funcionalidades de OpenAPI? {#new-dynamic-media-api-features}

Dynamic Media con funciones de OpenAPI ofrece las siguientes ventajas clave:

* **Integraciones perfectas**: Dynamic Media con funciones de OpenAPI ofrece un conjunto completo de API de búsqueda y entrega. Permite a los desarrolladores realizar [integrar la entrega de recursos con sus aplicaciones](/help/assets/integrate-new-dynamic-media-apis.md). Las aplicaciones incluyen aplicaciones de Adobe y de terceros. Además, proporciona un [Interfaz de usuario del selector de recursos de Micro Frontend](/help/assets/asset-selector.md) para buscar y seleccionar recursos aprobados. El selector se puede integrar fácilmente con cualquier aplicación basada en marcos de JavaScript como React JS, Angular JS y Vanilla JS.

* **Administración centralizada de recursos digitales**: DAM es la única fuente fiable para todos los recursos digitales. Los recursos digitales se administran de forma centralizada en AEM Assets y se entregan a las aplicaciones consumidoras por referencia mediante direcciones URL de entrega, sin copiar los binarios de recursos.

* **Actualizaciones en tiempo real**: Cualquier cambio realizado en los recursos aprobados en DAM, incluidas las actualizaciones de la versión y las modificaciones de metadatos, se reflejan automáticamente en las direcciones URL de entrega. Con un valor corto de tiempo de vida (TTL) de 10 minutos configurado para Dynamic Media con funciones de OpenAPI a través de CDN, las actualizaciones se pueden ver en todas las interfaces de creación y publicación en menos de 10 minutos.

* **Coherencia de marca**: Solo [recursos aprobados por la marca](/help/assets/approved-assets.md) están expuestos a aplicaciones posteriores. [Los responsables de marca y los especialistas en marketing mantienen un control estricto sobre los recursos de marca](/help/assets/restrict-assets-delivery.md). Solo está disponible la versión aprobada y más reciente del recurso para su uso, lo que garantiza la coherencia de la marca en todos los canales y aplicaciones.

* **Entrega optimizada para la web**: los recursos digitales se entregan en formatos optimizados para la web para mejorar los elementos vitales web principales de sus experiencias digitales. Esto incluye compatibilidad con representaciones WebP para imágenes, flujo adaptable a través de protocolos HLS o DASH para vídeos y representaciones originales para documentos.

* **Transformación dinámica de recursos**: nuestro sistema permite la transformación de imágenes sobre la marcha mediante parámetros de URL conocidos como modificadores de imagen. [Por ejemplo, anchura, altura, rotación, inversión, calidad, recorte y formato](/help/assets/deliver-assets-apis.md). Dynamic Media con funciones de OpenAPI también admite funciones de recorte inteligente de imágenes. Las representaciones transformadas se generan dinámicamente y se entregan sin problemas a través de la CDN.

* **Entrega segura de recursos**: Dynamic Media con funciones OpenAPI proporciona un mecanismo para controlar el acceso a los recursos digitales. Puede especificar funciones de usuario o grupos como metadatos para los recursos que se van a proteger y establecer un periodo de tiempo predefinido durante el cual [solo los usuarios autorizados pueden acceder a estos recursos](/help/assets/restrict-assets-delivery.md). Las direcciones URL de entrega de los activos protegidos no se resuelven para los usuarios no autorizados durante el período restringido.

* **Perspectivas de datos para tomar decisiones informadas**: Más allá de la administración y la entrega de recursos, captura la información de los datos de entrega en las entregas de recursos en CDN, lo que permite a los administradores de marcas rastrear las métricas de entrega a través de los canales. Les permite tomar decisiones basadas en datos para una optimización continua de la gobernanza de recursos y las estrategias de entrega.

![Nuevo diagrama de flujo de datos de Dynamic Media](assets/dm-openapi-dfd.png)

## Requisitos previos para acceder a Dynamic Media con funciones de OpenAPI {#prerequisites-new-dynaminc-media-apis}

Para acceder a Dynamic Media con las funciones de OpenAPI, debe tener licencias para:

* AEM Assets as a Cloud Service

* AEM Dynamic Media

## ¿Cómo se habilita Dynamic Media con las funcionalidades de OpenAPI? {#enable-new-dynamic-media-apis}

Antes de enviar una solicitud para habilitar Dynamic Media AEM con las funcionalidades de OpenAPI en el as a Cloud Service de la, asegúrese de que aún no esté habilitada. Para comprobar si está activada, ejecute los siguientes pasos:

1. Por confirmar desde ingeniería y gestión de productos

Para habilitar Dynamic Media AEM con las funcionalidades de OpenAPI en el as a Cloud Service de la, envíe un ticket de asistencia técnica de Adobe con los siguientes detalles:

* ID de entorno y programa de Cloud Service

* Detalles del caso de uso para resolver con Dynamic Media con la integración de las capacidades de OpenAPI

* Detalles de las aplicaciones de flujo descendente para integrar con Dynamic Media con capacidades de OpenAPI.

  >[!NOTE]
  >
  > Para integrarse con una aplicación que no sea de Adobe, proporcione nombres de dominio a la lista blanca donde está alojada la aplicación.

* Detalles de los contactos de cliente clave implicados en el proyecto de integración.

Una vez enviado el vale de soporte, el Adobe permite a Dynamic Media usar las funciones de OpenAPI en el entorno de los Cloud Service y compartir los detalles, como el ID del cliente IMS, para que pueda continuar con la integración.

## Profundizar más en las funcionalidades clave {#learn-more-key-capabilities}

<table>
<td>
   <a href="/help/assets/approved-assets.md">
   <img alt="Aprobar recursos en Experience Manager Assets" src="./assets/approved-assets.jpeg" />
   </a>
   <div>
      <a href="/help/assets/approved-assets.md">
      <strong>Aprobar recursos en Experience Manager Assets</strong>
      </a>
   </div>
   <p>
      <em>Apruebe los recursos en AEM Assets para optimizar la administración de recursos, lo que garantiza un proceso controlado y eficiente para la administración de recursos.</em>
   </p>
</td>
<td>
   <a href="/help/assets/integrate-new-dynamic-media-apis.md">
   <img alt="Integración de AEM Assets con aplicaciones de flujo descendente" src="./assets/asset-selector-integration.png" />
   </a>
   <div>
      <a href="/help/assets/integrate-new-dynamic-media-apis.md">
      <strong>Integración de AEM Assets con aplicaciones de flujo descendente</strong>
      </a>
   </div>
   <p>
      <em>Integre su propia interfaz de usuario personalizada con el repositorio de Experience Manager Assets mediante las API de búsqueda y envío o utilice el selector de recursos de Micro-FrontEnd de Adobe.</em>
   </p>
</td>
<td>
   <a href="/help/assets/asset-selector.md">
   <img alt="Selector de recursos de Adobe" src="./assets/asset-selector-prereqs.png" />
   </a>
   <div>
      <a href="/help/assets/asset-selector.md">
      <strong>Selector de recursos de Micro-Frontend de Adobe</strong>
      </a>
   </div>
   <p>
      <em>Interfaz de usuario que interactúa con el repositorio de AEM Assets para buscar recursos y luego utilizarlos en la experiencia de creación de aplicaciones.</em>
   </p>
</td>
</table>
<table>
<td>
   <a href="/help/assets/search-assets-api.md">
   <img alt="Buscar recursos en el repositorio de Experience Manager Assets" src="./assets/search-assets-api-overview.png" />
   </a>
   <div>
      <a href="/help/assets/search-assets-api.md">
      <strong>Buscar recursos en el repositorio de Experience Manager Assets</strong>
      </a>
   </div>
   <p>
      <em>Busque recursos en el repositorio de AEM Assets para que se puedan enviar a aplicaciones de flujo descendente.</em>
   </p>
</td>
<td>
   <a href="/help/assets/deliver-assets-apis.md">
   <img alt="Entrega de recursos a aplicaciones posteriores" src="./assets/delivery-url.png" />
   </a>
   <div>
      <a href="/help/assets/deliver-assets-apis.md">
      <strong>Entrega de recursos a aplicaciones posteriores</strong>
      </a>
   </div>
   <p>
      <em>Distribuya recursos a aplicaciones descendentes integradas mediante una URL de entrega.</em>
   </p>
</td>
<td>
   <a href="/help/assets/restrict-assets-delivery.md">
   <img alt="Restringir el acceso a los recursos en Experience Manager" src="./assets/restricted-access.png" />
   </a>
   <div>
      <a href="/help/assets/restrict-assets-delivery.md">
      <strong>Restringir el acceso a los recursos en Experience Manager</strong>
      </a>
   </div>
   <p>
      <em> AEM El administrador de DAM o los administradores de marcas restringen el acceso configurando funciones para los recursos aprobados en la instancia de autor as a Cloud Service de la.</em>
   </p>
</td>
</table>

