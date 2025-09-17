---
title: Telemetría operativa para AEM as a Cloud Service
description: Obtenga información acerca de Operational Telemetry , un servicio automatizado que permite supervisar la recopilación de datos en el lado del cliente.
exl-id: 91fe9454-3dde-476a-843e-0e64f6f73aaf
feature: Administering
role: Admin
source-git-commit: 100a8cd1a27cd8f0677ed001def0b1e0e7b20ed3
workflow-type: tm+mt
source-wordcount: '1134'
ht-degree: 1%

---

# Servicio de telemetría operativa para AEM as a Cloud Service {#real-use-monitoring-service-for-aem-as-a-cloud-service}

>[!NOTE]
>
>El servicio de telemetría operativa, la recopilación de datos en el lado del cliente, es un servicio automatizado. No se requiere ninguna configuración del cliente.

>[!INFO]
>
>La monitorización del lado del cliente solo funciona para clientes con AEM (Adobe Experience Manager) Cloud Service versión **2024.5.16461** y superior.

## Información general {#overview}

El servicio de telemetría operativa es una tecnología de monitorización del rendimiento que supervisa el tráfico del lado del cliente en un sitio web o una aplicación en tiempo real. Este servicio se centra en recopilar métricas y datos clave para optimizar el rendimiento mediante la monitorización de las participaciones en sitios web, en lugar de los propios usuarios. Con la telemetría operativa, las métricas de rendimiento clave se rastrean desde el inicio de la dirección URL hasta que la solicitud se devuelve al explorador.

## ¿Quién puede beneficiarse del servicio de Telemetría Operativa? {#who-can-benefit-from-operational-telemetry-service}

La telemetría operativa ayuda a los clientes y a Adobe a comprender cómo interactúan los usuarios finales con los sitios de AEM. La telemetría operativa preserva la privacidad de los visitantes a través de una recopilación y muestreo de datos limitados; solo se monitoriza una pequeña parte de todas las vistas de página.

## Muestreo de datos del servicio de telemetría operativa {#operational-telemetry-service-data-sampling}

Las soluciones tradicionales de análisis web intentan recopilar datos de cada visitante. El servicio de telemetría operativa de AEM solo captura información de una pequeña fracción de las vistas de página. El servicio está diseñado para ser muestreado y anonimizado, en lugar de un reemplazo para el análisis. De manera predeterminada, las páginas tienen una proporción de muestreo de 1:100. Los operadores de sitio no pueden aumentar ni disminuir la tasa de muestreo en este momento. Para calcular el tráfico total con precisión, por cada 100 vistas de página, se recopilan datos de 1, lo que le proporciona una aproximación fiable del tráfico general.

A medida que se decide si los datos se recopilan, se toman por vista de página por vista de página, y resulta prácticamente imposible rastrear las interacciones en varias páginas. Por diseño, Operational Telemetry no tiene concepto de visitantes o sesiones, solo de vistas de página.

## ¿Qué datos se recopilan? {#what-data-is-being-collected}

El servicio de telemetría operativa está diseñado para minimizar la recopilación de datos. A continuación se enumera el conjunto completo de información recopilada por Operational Telemetry:

* Nombre de host del sitio que se está visitando, por ejemplo: `experienceleague.adobe.com`
* El tipo de agente de usuario y sistema operativo generales que se utilizan para mostrar la página, como: `desktop:windows` o `mobile:ios`
* La hora de la recopilación de datos, como: `2021-06-26 06:00:02.596000 UTC (in order to preserve privacy, we round all minutes to the previous hour, so that only seconds and milliseconds are tracked)`
* Dirección URL de la página que se está visitando, por ejemplo: `https://experienceleague.adobe.com/docs`
* La URL del referente (la URL de la página que está vinculada a la página actual, si el usuario ha seguido un vínculo)
* Identificador de la vista de página generado aleatoriamente, con un formato similar al siguiente: `2Ac6`
* El peso o la inversa de la tasa de muestreo, como: `100`. Significa que solo se registra una de cada cien vistas de página
* El punto de comprobación, o nombre, de un evento concreto en la secuencia de carga de la página. O bien, interactuar con él como visitante
* El origen, o identificador, del elemento DOM con el que interactúa el usuario para el punto de comprobación mencionado anteriormente. Por ejemplo, podría ser una imagen
* El objetivo o vínculo a una página o recurso externo con el que el usuario interactúa para el punto de comprobación mencionado anteriormente. Por ejemplo: `https://blog.adobe.com/jp/publish/2022/06/29/media_162fb947c7219d0537cce36adf22315d64fb86e94.png`
* Las [constantes vitales web principales (CWV)](https://web.dev/articles/lcp) métricas de rendimiento [Pintado de contenido más grande (LCP)](https://web.dev/articles/lcp), [Interacción con la siguiente pintura (INP)](https://web.dev/articles/inp) y [Desplazamiento de diseño acumulativo (CLS)](https://web.dev/articles/cls) que describen la calidad de experiencia del visitante.

## Cómo funciona la telemetría operativa para un cliente {#how-operational-telemetry-works-for-a-customer}

La telemetría operativa supervisa automáticamente el tráfico del lado del cliente. Como cliente de Adobe, no necesita realizar ningún paso adicional, ya que este servicio está perfectamente integrado en su configuración existente. Con el servicio de telemetría operativa disponible en general, se beneficia automáticamente de esta nueva función. El servicio de telemetría operativa no expone ninguna métrica de cara al cliente para monitorizar en la actualidad. Estamos trabajando para ofrecerle esta funcionalidad lo antes posible.

<!-- Alexandru: hiding temporarily, until we figure out where this needs to be linked to 

If you wish to leverage more insights with this new feature to optimize your digital experiences effortlessly, please see here (link to Row 99). -->

## Cómo utiliza Adobe la telemetría operativa {#how-operational-telemetry-data-is-being-used}

Los datos de telemetría operativa se utilizan para los siguientes fines:

* Para identificar y corregir los cuellos de botella de rendimiento de las ubicaciones de los clientes
* Para comprender cómo AEM interactúa con otros scripts (como análisis, segmentación o bibliotecas externas) en la misma página, a fin de aumentar la compatibilidad.
<!--
## Limitations and understanding variance in page views and performance metrics {#limitations-and-understanding-variance-in-page-views-and-performance-metrics}

Here are key considerations for customers to keep in mind when interpreting their Operational Telemetry data:

1. **Tracker blockers**

   * End-users employing tracker blockers or privacy extensions can impede Operational Telemetry data collection, as these tools restrict the tracking scripts' execution. This restriction may lead to underreported page views and user interactions, creating a discrepancy between actual site activity and the data captured by Operational Telemetry.

1. **Limitations in capturing headless API/JSON calls**

   * Operational Telemetry data service focuses on the client-side experience and doesn't capture the backend API or JSON calls made from a non-AEM headless app at this time. The exclusion of these calls from Operational Telemetry service data creates variances from the content requests measured by CDN Analytics.
-->

## Preguntas frecuentes {#faq}

<!-- REMOVED THIS FAQ AS PER EMAIL REQUEST FROM SHWETA DUA, SEPTEMBER 4, 2024 TO THE DL-AEM-DOCS GROUP 
1. **Can customers integrate the Operational Telemetry service scripts with third-party systems like Dynatrace?**

   Yes.
-->

1. **¿Se están recopilando las métricas &quot;Interacción con la siguiente pintura&quot;, &quot;Tiempo hasta el primer byte&quot; y &quot;Primera pintura de contenido&quot;?**

   Se recopilan la interacción con la siguiente pintura (INP) y el tiempo hasta el primer byte (TTFB).  La primera pintura con contenido no se recopila en este momento.

1. **La ruta de acceso `/.rum` está bloqueada en mi sitio, ¿cómo debo corregirla?**

   Se requiere la ruta de acceso `/.rum` para que funcione la colección de telemetría operativa. Si utiliza una CDN delante de AEM as a Cloud Service de Adobe, asegúrese de que la ruta `/.rum` se reenvíe al mismo origen de AEM que el resto del contenido de AEM. Y asegúrese de que no se ajuste de ninguna manera. Como alternativa, puede cambiar el host que se va a utilizar para la telemetría operativa a `rum.hlx.page` estableciendo una variable de entorno en Cloud Manager[ denominada ](/help/implementing/cloud-manager/environment-variables.md#add-variables) al valor `AEM_OPTEL_EXTERNAL`. `true` Si desea volver a cambiar a las mismas solicitudes de dominio en un momento posterior, simplemente elimine esa variable de entorno de nuevo.

1. **¿Cuenta la colección de telemetría operativa para las solicitudes de contenido con fines contractuales?**

   La biblioteca de telemetría operativa y la colección de telemetría operativa no cuentan como solicitudes de contenido y no aumentan el número notificado de vistas de página o llamadas a la API. Además, para los clientes que usan la CDN predeterminada con AEM as a Cloud Service, [la colección del lado del servidor](#serverside-collection) es la base de las solicitudes de contenido.

1. **¿Cómo puedo deshabilitar la telemetría operativa?**

   Adobe recomienda utilizar la telemetría operativa debido a sus importantes ventajas y que permitirá a Adobe ayudarle a optimizar sus experiencias digitales mejorando el rendimiento del sitio web. El servicio está diseñado para ser ininterrumpido y no tiene ningún impacto en el rendimiento de su sitio web.

   La exclusión puede significar perder la oportunidad de mejorar la participación del tráfico en el sitio web. Sin embargo, si encuentra algún problema, puede deshabilitar la telemetría operativa estableciendo una variable de entorno en Cloud Manager[ denominada ](/help/implementing/cloud-manager/environment-variables.md#add-variables) con el valor `AEM_OPTEL_DISABLED`. `true` Si desea volver a activar la Telemetría operativa en un momento posterior, simplemente elimine de nuevo esa variable de entorno.

1. **¿Puedo usar una directiva de seguridad de contenido con un nonce?**

   La compatibilidad con la telemetría operativa contiene una función experimental para admitir una política de seguridad de contenido con un nonce. Esta característica se puede habilitar [estableciendo una variable de entorno en Cloud Manager](/help/implementing/cloud-manager/environment-variables.md#add-variables) denominada `AEM_OPTEL_NONCE` con el valor `true`. Si desea volver a deshabilitar esto más adelante, simplemente quite esa variable de entorno de nuevo.

   Si tiene algún problema con esta función, póngase en contacto con el Soporte técnico de Adobe.

1. **¿Cómo puedo habilitar la telemetría operativa solo para determinadas páginas?**

   De forma predeterminada, la telemetría operativa está habilitada para todas las páginas por debajo de la carpeta `/content` en el repositorio. Al [establecer una variable de entorno en Cloud Manager](/help/implementing/cloud-manager/environment-variables.md#add-variables) denominada `AEM_OPTEL_INCLUDED_PATHS` en una lista de rutas separadas por comas en el repositorio, la telemetría operativa solo se habilitará para esas páginas. Además, puede establecer `AEM_OPTEL_EXCLUDED_PATHS` en una lista de rutas de acceso en el repositorio que se excluirán. Con la combinación de estos dos ajustes, puede ajustar la inclusión de Telemetría Operativa a sus necesidades.

