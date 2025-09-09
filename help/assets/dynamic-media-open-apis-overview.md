---
title: Dynamic Media con funciones de OpenAPI
description: Conozca conceptos clave como por qué utilizar Dynamic Media con funciones de OpenAPI y cómo habilitarlo.
role: User
exl-id: 658b6eff-9f5a-4166-9ff6-5dc8eb92ada3
source-git-commit: 73b1b7f2133a751ea2494d66960a7d225798d1dd
workflow-type: tm+mt
source-wordcount: '1106'
ht-degree: 94%

---

# Dynamic Media con funciones de OpenAPI {#new-dynaminc-media-apis-overview}

En el vertiginoso mundo digital actual, aprovechar todo el potencial de los recursos digitales de su marca es crucial para ir un paso por delante de la competencia. Una solución integral de administración de recursos digitales (DAM) facilita la gobernanza de los recursos, promueve la uniformidad de la marca y acelera la entrega de contenido, al tiempo que garantiza la integridad de la marca y una experiencia excepcional para el cliente.

Dynamic Media con funciones de OpenAPI coloca a DAM en el centro de un ecosistema de cadena de suministro de contenido ágil y eficiente para garantizar la gobernanza y la entrega de los recursos.

## ¿Por qué utilizar Dynamic Media con funciones de OpenAPI? {#dynamic-media-open-api-features}

Dynamic Media con funciones de OpenAPI ofrece las siguientes ventajas clave:

* **Integraciones perfectas**: Dynamic Media con funciones de OpenAPI ofrece un conjunto completo de API de búsqueda y entrega. Permite a los desarrolladores [integrar fácilmente la entrega de recursos con sus aplicaciones](/help/assets/integrate-dynamic-media-open-apis.md). Las aplicaciones incluyen aplicaciones de Adobe y también de terceros. Proporciona una [interfaz de usuario del Selector de recursos de Micro-Frontend](/help/assets/overview-asset-selector.md) para buscar y seleccionar recursos aprobados. El selector se puede integrar fácilmente con cualquier aplicación basada en marcos de trabajo de JavaScript como React JS, Angular JS y Vanilla JS.

* **Administración centralizada de recursos digitales**: DAM es la única fuente de confianza para todos los recursos digitales. Los recursos digitales se administran de forma centralizada en AEM Assets y se entregan a las aplicaciones consumidoras por referencia mediante direcciones URL de entrega, sin copiar los binarios de recursos.

* **Actualizaciones en tiempo real**: cualquier cambio realizado en los recursos aprobados en DAM, incluidas las actualizaciones de la versión y las modificaciones de metadatos, se refleja automáticamente en las direcciones URL de entrega. Con un valor corto de tiempo de vida (TTL) de 10 minutos configurado para Dynamic Media con funciones de OpenAPI a través de CDN, las actualizaciones se pueden ver en todas las interfaces de creación y publicación en menos de 10 minutos.

* **Uniformidad de la marca**: solo [los recursos de marca aprobados](/help/assets/approve-assets.md) están expuestos a aplicaciones descendentes. [Los directores de marcas y los especialistas en marketing mantienen un control estricto sobre los recursos de la marca](/help/assets/restrict-assets-delivery.md). Solo está disponible la versión aprobada y más reciente del recurso para su uso, lo que garantiza la coherencia de marca en todos los canales y aplicaciones.

* **Entrega optimizada para la web**: los recursos digitales se entregan en formatos optimizados para la web a fin de mejorar los elementos vitales principales de las experiencias digitales. Esto incluye compatibilidad con representaciones WebP para imágenes, streaming adaptable a través de protocolos HLS o DASH para vídeos y representaciones originales para documentos.

* [Transformación dinámica de recursos](https://developer.adobe.com/experience-cloud/experience-manager-apis): nuestro sistema permite la transformación de imágenes sobre la marcha mediante parámetros de URL conocidos como modificadores de imagen. Por ejemplo, anchura, altura, rotación, voltear, calidad, recorte, formato y recorte inteligente. Las representaciones transformadas se generan dinámicamente y se entregan sin problemas a través de la CDN.

* **Entrega segura de recursos**: Dynamic Media con funciones de OpenAPI proporciona un mecanismo para controlar el acceso a sus recursos digitales. Puede especificar roles de usuario o grupos como metadatos para los recursos que se van a proteger y establecer un intervalo de tiempo predefinido durante el cual [solo los usuarios autorizados puedan acceder a estos recursos](/help/assets/restrict-assets-delivery.md). Las URL de entrega de los recursos protegidos no se resuelven para los usuarios no autorizados durante el período restringido.

* **Perspectivas de datos para tomar decisiones informadas (próximas)**: más allá de la administración y la entrega de recursos, captura perspectivas de datos de entrega en las entregas de recursos en CDN, lo que permite a los directores de marca rastrear las métricas de entrega en varios canales. Les permite tomar decisiones basadas en datos para una optimización continua de la gobernanza de recursos y las estrategias de entrega.

![Diagrama del flujo de datos de la API abierta de Dynamic Media](assets/dm-openapi-dfd.png)

Para obtener información sobre las ofertas disponibles de Dynamic Media y sus capacidades, consulte [Dynamic Media Prime y Ultimate](/help/assets/dynamic-media/dm-prime-ultimate.md).

>[!NOTE]
>
>Los clientes de DM Prime pueden utilizar modificadores de imagen básicos como rotar, recortar, voltear, alto, ancho y calidad. Imágenes inteligentes no es compatible con AVIF para clientes de DM Prime.


## Requisitos previos para acceder a Dynamic Media con funciones de OpenAPI {#prerequisites-dynaminc-media-open-apis}

Para acceder a Dynamic Media con funciones de OpenAPI, debe tener licencias para:

* AEM Assets as a Cloud Service

* AEM Dynamic Media

## ¿Cómo se habilita Dynamic Media con funciones de OpenAPI? {#enable-dynamic-media-open-apis}

Antes de enviar una solicitud para habilitar Dynamic Media con funciones de OpenAPI en AEM as a Cloud Service, asegúrese de que aún no esté habilitado.

Una vez cumplidos los [requisitos previos](#prerequisites-dynaminc-media-open-apis) y si Dynamic Media con funciones de OpenAPI está habilitado en su instancia de AEM as a Cloud Service, habrá una URL de entrega disponible para cada recurso aprobado en el repositorio. Para obtener información sobre cómo copiar la URL de entrega, consulte [Copiar URL de entrega para recursos aprobados](approve-assets.md#copy-delivery-url-approved-assets) . Adobe recomienda utilizar este método para comprobar que Dynamic Media con funciones de OpenAPI está habilitado en AEM as a Cloud Service antes de enviar un vale de asistencia para habilitarlo.

Para habilitar Dynamic Media con funciones de OpenAPI en AEM as a Cloud Service, envíe un vale de asistencia de Adobe con los siguientes detalles:

* ID de entorno y programa de Cloud Services

* Detalles del caso de uso que quiere resolver con la integración de Dynamic Media con funciones de OpenAPI.

* Detalles de las aplicaciones descendentes que quiere integrar con Dynamic Media con funciones de OpenAPI.

  >[!NOTE]
  >
  > Para integrarse con una aplicación que no sea de Adobe, proporcione nombres de dominio de la lista de permitidos donde se aloja la aplicación.

* Detalles de los contactos de los clientes clave implicados en el proyecto de integración.

* Lista de los miembros clave del equipo de cuentas de Adobe (correo electrónico).

Una vez enviado el vale de asistencia, Adobe habilita Dynamic Media con funciones de OpenAPI en el entorno de Cloud Services y comparte los detalles, como el ID del cliente de IMS, para que pueda continuar con la integración.

>[!NOTE]
>
>Excluya a `/conf/global/settings/dam/assets-configurations/assetdelivery` de cualquier paquete de contenido para evitar la desactivación de Dynamic Media con funciones de OpenAPI.

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
      <em>Apruebe recursos en AEM Assets para optimizar la administración de recursos, lo que garantiza un proceso controlado y eficiente de gestión de recursos.</em>
   </p>
</td>
<td>
   <a href="/help/assets/integrate-dynamic-media-open-apis.md">
   <img alt="Integrar AEM Assets con aplicaciones descendentes" src="./assets/asset-selector-integration.png" />
   </a>
   <div>
      <a href="/help/assets/integrate-dynamic-media-open-apis.md">
      <strong>Integrar AEM Assets con aplicaciones descendentes</strong>
      </a>
   </div>
   <p>
      <em>Integre su propia interfaz de usuario personalizada con el repositorio de Experience Manager Assets mediante las API de búsqueda y entrega o use el Selector de recursos de Micro-Frontend de Adobe.</em>
   </p>
</td>
<td>
   <a href="/help/assets/overview-asset-selector.md">
   <img alt="Selector de recursos de Adobe" src="./assets/asset-selector-prereqs.png" />
   </a>
   <div>
      <a href="/help/assets/overview-asset-selector.md">
      <strong>Selector de recursos de Micro-Frontend de Adobe</strong>
      </a>
   </div>
   <p>
      <em>Interfaz de usuario que interactúa con el repositorio de AEM Assets para buscar recursos y, a continuación, utilizarlos en la experiencia de creación de aplicaciones.</em>
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
      <em>Busque recursos en el repositorio de AEM Assets para que puedan enviarse a aplicaciones descendentes.</em>
   </p>
</td>
<td>
   <a href="/help/assets/deliver-assets-apis.md">
   <img alt="Envío de recursos a aplicaciones descendentes" src="./assets/delivery-url.png" />
   </a>
   <div>
      <a href="/help/assets/deliver-assets-apis.md">
      <strong>Enviar recursos a aplicaciones descendentes</strong>
      </a>
   </div>
   <p>
      <em>Envíe recursos a aplicaciones descendentes integradas mediante una dirección URL de entrega.</em>
   </p>
</td>
<td>
   <a href="/help/assets/restrict-assets-delivery.md">
   <img alt="Restringir el acceso a los recursos en Experience Manager" src="./assets/restricted-access.png" />
   </a>
   <div>
      <a href="/help/assets/restrict-assets-delivery.md">
      <strong>Restringir el acceso a los recursos de Experience Manager</strong>
      </a>
   </div>
   <p>
      <em>: el administrador de DAM o los directores de marcas restringen el acceso configurando funciones para los recursos aprobados en la instancia de autor de AEM as a Cloud Service.</em>
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
      <strong>Integración de AEM Assets remoto con AEM Sites</strong>
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
      <strong>Preguntas frecuentes sobre Dynamic Media con funciones de OpenAPI</strong>
      </a>
   </div>
   <p>
      <em>Obtenga una respuesta a las preguntas más frecuentes sobre Dynamic Media con funciones de OpenAPI.</em>
   </p>
</td>
<td>
   <a href="/help/assets/configure-custom-domain.md">
   <img alt="Configuración del dominio personalizado" src="./assets/configure-custom-domain.jpeg" />
   </a>
   <div>
      <a href="/help/assets/configure-custom-domain.md">
      <strong>Configuración del dominio personalizado</strong>
      </a>
   </div>
   <p>
      <em>Aunque AEM as a Cloud Service incluye un dominio predeterminado, puede personalizarlo según sus necesidades.</em>
   </p>
</td>

</table>
