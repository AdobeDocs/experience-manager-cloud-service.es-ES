---
title: Monitorización de uso real para AEM as a Cloud Service
description: Obtenga información acerca de Real Use Monitoring (RUM) , un servicio automatizado que permite supervisar la recopilación de datos en el lado del cliente.
exl-id: 91fe9454-3dde-476a-843e-0e64f6f73aaf
feature: Administering
role: Admin
source-git-commit: ed52bac52618e23b9bcbe7c6767501c6711aff00
workflow-type: tm+mt
source-wordcount: '1012'
ht-degree: 1%

---

# Servicio de monitorización de uso real para AEM as a Cloud Service {#real-use-monitoring-service-for-aem-as-a-cloud-service}

>[!NOTE]
>
>El servicio de Monitorización de uso real, la recopilación de datos del lado del cliente, es un servicio automatizado. No se requiere ninguna configuración del cliente.

>[!INFO]
>
>AEM La monitorización del lado del cliente solo funciona para clientes con la versión de Cloud Service **2024.5.16461** o superior de (Adobe Experience Manager).

## Información general {#overview}

El servicio RUM (Real Use Monitoring) es una tecnología de monitorización del rendimiento que supervisa el tráfico del lado del cliente en un sitio web o una aplicación en tiempo real. Este servicio se centra en recopilar métricas y datos clave para optimizar el rendimiento mediante la monitorización de las participaciones en sitios web, en lugar de los propios usuarios. Con RUM, las métricas de rendimiento clave se rastrean desde el inicio de la dirección URL hasta que la solicitud se devuelve al explorador.

## ¿Quién puede beneficiarse de un servicio de monitorización de uso real? {#who-can-benefit-from-rum-service}

AEM La Monitorización de uso real de ha desarrollado una aplicación que ayuda a los clientes y al Adobe AEM a comprender cómo los usuarios finales interactúan con los sitios de la. La Monitorización de uso real diagnostica problemas de rendimiento y mide la eficacia de los experimentos. La Monitorización del uso real preserva la privacidad de los visitantes a través del muestreo (solo se monitoriza una pequeña parte de todas las vistas de página) y no se recopila información de identificación personal (PII).

## Servicio de monitoreo de uso real y privacidad {#rum-service-and-privacy}

AEM El servicio de Monitorización de uso real en la práctica preserva la privacidad del visitante y minimiza la recopilación de datos. Como visitante, significa que el sitio que está visitando o que se ha puesto a disposición del Adobe no recopila información personal.

Como operador de sitio, no se requiere ninguna opción de inclusión adicional para habilitar la monitorización a través de esta función. No hay ningún formulario emergente o de consentimiento adicional que los usuarios finales deban aceptar para habilitar RUM.

## Muestreo de datos del servicio de Monitorización de uso real {#rum-service-data-sampling}

Las soluciones tradicionales de análisis web intentan recopilar datos de cada visitante. AEM El servicio de Monitorización de uso real (RUM) de solo captura información de una pequeña fracción de las vistas de página. El servicio está diseñado para ser muestreado y anonimizado, en lugar de un reemplazo para el análisis. De forma predeterminada, las páginas tienen una proporción de muestreo de 1:100. Los operadores de sitio no pueden aumentar ni disminuir la tasa de muestreo en este momento. Para calcular el tráfico total con precisión, por cada 100 vistas de página, se recopilan datos de 1, lo que le proporciona una aproximación fiable del tráfico general.

A medida que se decide si los datos se recopilan, se toman por vista de página por vista de página, y resulta prácticamente imposible rastrear las interacciones en varias páginas. Por diseño, RUM no tiene concepto de visitantes o sesiones, solo de vistas de página.

## ¿Qué datos se recopilan? {#what-data-is-being-collected}

El servicio de Monitoreo de Uso Real está diseñado para evitar la recopilación de información personal. El conjunto completo de información recopilada por RUM se enumera a continuación:

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
* Las métricas de rendimiento de elementos vitales de la web (CWV) principales, como Pintado de contenido más grande (LCP), Primer retraso de entrada (FID), Cambio de diseño acumulativo (CLS) y Tiempo hasta el primer byte (TTFB), que describen la calidad de experiencia del visitante.

## Cómo funciona la Monitorización de uso real para un cliente {#how-rum-works-for-a-customer}

Real Use Monitoring supervisa automáticamente el tráfico del lado del cliente. Como cliente de Adobe, no necesita realizar ningún paso adicional, ya que este servicio está perfectamente integrado en su configuración existente. Con Real Use Monitoring (RUM) como General Availability (GA) , se beneficia automáticamente de esta nueva función. El servicio de Monitorización de uso real no expone ninguna métrica hoy a través de una herramienta de visualización. Estamos trabajando para ofrecerle esta funcionalidad lo antes posible.

<!-- Alexandru: hiding temporarily, until we figure out where this needs to be linked to 

If you wish to leverage more insights with this new feature to optimize your digital experiences effortlessly, please see here (link to Row 99). -->

## Cómo utiliza el Adobe la monitorización de uso real {#how-rum-data-is-being-used}

Los datos de monitorización de uso real se utilizan para los siguientes fines:

* Para identificar y corregir los cuellos de botella de rendimiento de las ubicaciones de los clientes
* AEM Para comprender cómo interactúa la con otros scripts (como análisis, segmentación o bibliotecas externas) en la misma página, aumente la compatibilidad.
<!--
## Limitations and understanding variance in page views and performance metrics {#limitations-and-understanding-variance-in-page-views-and-performance-metrics}

Here are key considerations for customers to keep in mind when interpreting their RUM data:

1. **Tracker blockers**

   * End-users employing tracker blockers or privacy extensions can impede RUM data collection, as these tools restrict the tracking scripts' execution. This restriction may lead to underreported page views and user interactions, creating a discrepancy between actual site activity and the data captured by RUM.

1. **Limitations in capturing headless API/JSON calls**

   * RUM data service focuses on the client-side experience and doesn't capture the backend API or JSON calls made from a non-AEM headless app at this time. The exclusion of these calls from RUM service data creates variances from the content requests measured by CDN Analytics.
-->

## Preguntas más frecuentes {#faq}

<!-- REMOVED THIS FAQ AS PER EMAIL REQUEST FROM SHWETA DUA, SEPTEMBER 4, 2024 TO THE DL-AEM-DOCS GROUP 
1. **Can customers integrate the RUM service scripts with third-party systems like Dynatrace?**

   Yes.
-->

1. **¿Se están recopilando las métricas &quot;Interacción con la siguiente pintura&quot;, &quot;Tiempo hasta el primer byte&quot; y &quot;Primera pintura de contenido&quot;?**

   Se recopilan la interacción con la siguiente pintura (INP) y el tiempo hasta el primer byte (TTFB).  La primera pintura con contenido no se recopila en este momento.

1. **La ruta de acceso `/.rum` está bloqueada en mi sitio, ¿cómo debo corregirla?**

   La ruta de acceso `/.rum` es necesaria para que funcione la colección RUM. Si utiliza una CDN delante de AEM as a Cloud Service AEM AEM de Adobe, asegúrese de que la ruta de `/.rum` se reenvíe al mismo origen de que el resto de su contenido de la red de distribución de contenido (CDN) de la red de distribución de contenido (). Y asegúrese de que no se ajuste de ninguna manera.

1. **¿La colección RUM cuenta para las solicitudes de contenido por motivos contractuales?**

   La biblioteca RUM y la colección RUM no cuentan como solicitudes de contenido y no aumentan el número informado de vistas de página o llamadas a la API. Además, para los clientes que usan la CDN predeterminada con AEM as a Cloud Service, [la colección del lado del servidor](#serverside-collection) es la base de las solicitudes de contenido.

1. **¿Cómo puedo excluirme?**

   Adobe recomienda utilizar Real Use Monitoring (RUM) debido a sus beneficios significativos y que permitirá al Adobe ayudarle a optimizar sus experiencias digitales mejorando el rendimiento del sitio web. El servicio está diseñado para ser ininterrumpido y no tiene ningún impacto en el rendimiento de su sitio web.

   La exclusión puede significar perder la oportunidad de mejorar la participación del tráfico en el sitio web. Sin embargo, si tiene algún problema, póngase en contacto con el Soporte técnico de Adobe.
