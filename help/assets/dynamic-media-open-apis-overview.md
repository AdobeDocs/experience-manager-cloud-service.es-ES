---
title: Dynamic Media con funciones de OpenAPI
description: Conozca conceptos clave como por qué utilizar Dynamic Media con las capacidades de OpenAPI y cómo habilitarlo.
role: User
source-git-commit: 8cd8eb834b548a52d6a9e094cb2c4447f228ab0d
workflow-type: tm+mt
source-wordcount: '1061'
ht-degree: 1%

---

# Dynamic Media con funciones de OpenAPI {#new-dynaminc-media-apis-overview}

En el acelerado mundo digital actual, desbloquear todo el potencial de los activos digitales de su marca es crucial para mantenerse por delante de la competencia. Una solución integral de administración de Assets digital (DAM) facilita la administración de los recursos, promueve la coherencia de la marca y acelera la entrega de contenido a la vez que garantiza la integridad de la marca y experiencias de cliente excepcionales.

Dynamic Media con capacidades OpenAPI coloca a DAM en el centro de un ecosistema de cadena de suministro de contenido ágil y eficiente para garantizar la gobernanza y la entrega de los recursos.

## ¿Por qué utilizar Dynamic Media con las funcionalidades de OpenAPI? {#dynamic-media-open-api-features}

Dynamic Media con funciones de OpenAPI ofrece las siguientes ventajas clave:

* **Integraciones perfectas**: Dynamic Media con capacidades OpenAPI ofrece un conjunto completo de API de búsqueda y entrega. Permite a los desarrolladores [integrar fácilmente la entrega de recursos con sus aplicaciones](/help/assets/integrate-dynamic-media-open-apis.md). Las aplicaciones incluyen aplicaciones de Adobe y de terceros. Proporciona una [interfaz de usuario del selector de recursos de Micro Frontend](/help/assets/asset-selector.md) para buscar y seleccionar recursos aprobados. El selector se puede integrar fácilmente con cualquier aplicación basada en marcos de trabajo de JavaScript como React JS, Angular JS y Vanilla JS.

* **Administración centralizada de recursos digitales**: DAM es la única fuente fiable para todos los recursos digitales. Los recursos digitales se administran de forma centralizada en AEM Assets y se entregan a las aplicaciones consumidoras por referencia mediante direcciones URL de entrega, sin copiar los binarios de recursos.

* **Actualizaciones en tiempo real**: Cualquier cambio realizado en los recursos aprobados en DAM, incluidas las actualizaciones de la versión y las modificaciones de metadatos, se refleja automáticamente en las direcciones URL de envío. Con un valor corto de tiempo de vida (TTL) de 10 minutos configurado para Dynamic Media con funciones de OpenAPI a través de CDN, las actualizaciones se pueden ver en todas las interfaces de creación y publicación en menos de 10 minutos.

* **Consistencia de la marca**: Solo [los recursos aprobados por la marca](/help/assets/approve-assets.md) están expuestos a aplicaciones de flujo descendente. [Los gerentes de marcas y los especialistas en mercadotecnia mantienen un control estricto sobre los recursos de marca](/help/assets/restrict-assets-delivery.md). Solo está disponible la versión aprobada y más reciente del recurso para su uso, lo que garantiza la coherencia de la marca en todos los canales y aplicaciones.

* **Entrega optimizada para la web**: Los recursos digitales se entregan en formatos optimizados para la web a fin de mejorar los elementos vitales principales de las experiencias digitales. Esto incluye compatibilidad con representaciones WebP para imágenes, flujo adaptable a través de protocolos HLS o DASH para vídeos y representaciones originales para documentos.

* **Transformación dinámica de recursos**: Nuestro sistema permite la transformación de imágenes sobre la marcha mediante parámetros de URL conocidos como modificadores de imagen. [Por ejemplo, anchura, altura, rotación, voltear, calidad, recorte, formato y recorte inteligente](/help/assets/deliver-assets-apis.md). Las representaciones transformadas se generan dinámicamente y se entregan sin problemas a través de la CDN.

* **Envío seguro de recursos**: Dynamic Media con capacidades OpenAPI proporciona un mecanismo para controlar el acceso a sus recursos digitales. Puede especificar roles de usuario o grupos como metadatos para los recursos que se van a proteger y establecer un intervalo de tiempo predefinido durante el cual [solo los usuarios autorizados puedan acceder a estos recursos](/help/assets/restrict-assets-delivery.md). Las direcciones URL de entrega de los activos protegidos no se resuelven para los usuarios no autorizados durante el período restringido.

* **Perspectivas de datos para tomar decisiones informadas (próximas)**: más allá de la administración y la entrega de recursos, captura perspectivas de datos de entrega en las entregas de recursos en CDN, lo que permite a los administradores de marcas rastrear las métricas de entrega en varios canales. Les permite tomar decisiones basadas en datos para una optimización continua de la gobernanza de recursos y las estrategias de entrega.

![Diagrama del flujo de datos de la API abierta de Dynamic Media](assets/dm-openapi-dfd.png)

## Requisitos previos para acceder a Dynamic Media con funciones de OpenAPI {#prerequisites-dynaminc-media-open-apis}

Para acceder a Dynamic Media con las funciones de OpenAPI, debe tener licencias para:

* AEM Assets as a Cloud Service

* AEM Dynamic Media

## ¿Cómo se habilita Dynamic Media con las funcionalidades de OpenAPI? {#enable-dynamic-media-open-apis}

Antes de enviar una solicitud para habilitar Dynamic Media con las funciones de OpenAPI en AEM as a Cloud Service, asegúrese de que aún no esté habilitado.

Una vez cumplidos los [requisitos previos](#prerequisites-dynaminc-media-open-apis) y si Dynamic Media con las capacidades de OpenAPI está habilitado en su instancia de AEM as a Cloud Service, habrá una URL de entrega disponible para cada recurso aprobado en el repositorio. Para obtener información sobre cómo copiar la URL de envío, consulte [Copiar URL de envío para recursos aprobados](approve-assets.md#copy-delivery-url-approved-assets) . El Adobe recomienda utilizar este método para comprobar que Dynamic Media con capacidades OpenAPI está habilitado en AEM as a Cloud Service antes de enviar un ticket de asistencia para habilitarlo.

Para habilitar Dynamic Media con las funcionalidades de OpenAPI en AEM as a Cloud Service, envíe un ticket de asistencia de Adobe con los siguientes detalles:

* ID de entorno y programa de Cloud Service

* Detalles del caso de uso para resolver con Dynamic Media con la integración de las capacidades de OpenAPI.

* Detalles de las aplicaciones de flujo descendente para integrar con Dynamic Media con capacidades de OpenAPI.

  >[!NOTE]
  >
  > Para integrarse con una aplicación que no sea de Adobe, proporcione nombres de dominio a la lista blanca donde está alojada la aplicación.

* Detalles de los contactos de cliente clave implicados en el proyecto de integración.

* Lista de los miembros del equipo de la cuenta de Adobe clave (correo electrónico).

Una vez enviado el vale de soporte, el Adobe permite a Dynamic Media usar las funciones de OpenAPI en el entorno de los Cloud Service y compartir los detalles, como el ID del cliente IMS, para que pueda continuar con la integración.

>[!NOTE]
>
>Excluya a `/conf/global/settings/dam/assets-configurations/assetdelivery` de cualquier paquete de contenido para evitar la desactivación de Dynamic Media con las capacidades de OpenAPI.

## Profundizar más en las funcionalidades clave {#learn-more-key-capabilities}

<table>
<td>
   <a href="/help/assets/approve-assets.md">
   <img alt="Aprobar recursos en Experience Manager Assets" src="./assets/approved-assets.jpeg" />
   </a>
   <div>
      <a href="/help/assets/approve-assets.md">
      <strong>Aprobar recursos en Experience Manager Assets</strong>
      </a>
   </div>
   <p>
      <em>Apruebe recursos en AEM Assets para optimizar la administración de recursos, lo que garantiza un proceso controlado y eficiente para administrar los recursos.</em>
   </p>
</td>
<td>
   <a href="/help/assets/integrate-dynamic-media-open-apis.md">
   <img alt="Integración de AEM Assets con aplicaciones de flujo descendente" src="./assets/asset-selector-integration.png" />
   </a>
   <div>
      <a href="/help/assets/integrate-dynamic-media-open-apis.md">
      <strong>Integrar AEM Assets con aplicaciones de flujo descendente</strong>
      </a>
   </div>
   <p>
      <em>Integre su propia interfaz de usuario personalizada con el repositorio de Experience Manager Assets mediante las API de búsqueda y envío o use el Selector de recursos de Micro-FrontEnd de Adobe.</em>
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
      <em>Interfaz de usuario que interactúa con el repositorio de AEM Assets para buscar recursos y utilizarlos en la experiencia de creación de aplicaciones.</em>
   </p>
</td>
</table>
<table>



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
      <em>Busque recursos en el repositorio de AEM Assets para que puedan enviarse a aplicaciones de flujo descendente.</em>
   </p>
</td>
<td>
   <a href="/help/assets/deliver-assets-apis.md">
   <img alt="Entrega de recursos a aplicaciones posteriores" src="./assets/delivery-url.png" />
   </a>
   <div>
      <a href="/help/assets/deliver-assets-apis.md">
      <strong>Enviar recursos a aplicaciones de flujo descendente</strong>
      </a>
   </div>
   <p>
      <em>Envíe recursos a aplicaciones de flujo descendente integradas mediante una dirección URL de envío.</em>
   </p>
</td>
<td>
   <a href="/help/assets/restrict-assets-delivery.md">
   <img alt="Restringir el acceso a los recursos en Experience Manager" src="./assets/restricted-access.png" />
   </a>
   <div>
      <a href="/help/assets/restrict-assets-delivery.md">
      <strong>Restringir el acceso a los recursos del Experience Manager</strong>
      </a>
   </div>
   <p>
      <em>: el administrador de DAM o los administradores de marcas restringen el acceso configurando funciones para los recursos aprobados en la instancia de autor de AEM as a Cloud Service.</em>
   </p>
</td>

</table>
<table>
<td>
   <a href="/help/assets/integrate-remote-approved-assets-with-sites.md">
   <img alt="Integración de AEM Assets remoto con AEM Sites" src="./assets/connected-assets-rdam.png" />
   </a>
   <div>
      <a href="/help/assets/integrate-remote-approved-assets-with-sites.md">
      <strong>Integrar AEM Assets remoto con AEM Sites</strong>
      </a>
   </div>
   <p>
      <em>Aprenda a integrar AEM Assets remoto con el entorno de AEM Sites. </em>
   </p>
</td>
<td>
   <a href="/help/assets/dynamic-media-open-apis-faqs.md">
   <img alt="Preguntas frecuentes sobre Dynamic Media con funciones de OpenAPI" src="./assets/dynamic-media-faqs.jpeg" />
   </a>
   <div>
      <a href="/help/assets/dynamic-media-open-apis-faqs.md">
      <strong>Preguntas frecuentes sobre Dynamic Media con capacidades OpenAPI</strong>
      </a>
   </div>
   <p>
      <em>Obtenga una respuesta a las preguntas más frecuentes sobre Dynamic Media con capacidades OpenAPI.</em>
   </p>
</td>
<td>
   <a href="/help/assets/configure-custom-domain.md">
   <img alt="Configuración del dominio personalizado" src="./assets/configure-custom-domain.jpeg" />
   </a>
   <div>
      <a href="/help/assets/configure-custom-domain.md">
      <strong>Configurar dominio personalizado</strong>
      </a>
   </div>
   <p>
      <em>Aunque AEM as a Cloud Service incluye un dominio predeterminado, puede personalizarlo según sus necesidades.</em>
   </p>
</td>

</table>

