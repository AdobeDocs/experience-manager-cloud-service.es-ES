---
title: Monitorización de uso real para AEM as a Cloud Service
description: Aprenda a utilizar Real Use Monitoring (RUM) para capturar y analizar la experiencia de usuario digital de un sitio web o aplicación en tiempo real.
exl-id: 91fe9454-3dde-476a-843e-0e64f6f73aaf
feature: Administering
role: Admin
source-git-commit: 19b52f733a592c7e84ba2e9d83d37e5e181f21ab
workflow-type: tm+mt
source-wordcount: '1313'
ht-degree: 0%

---

# Servicio de monitorización de uso real para AEM as a Cloud Service {#real-use-monitoring-service-for-aem-as-a-cloud-service}

>[!NOTE]
>
>El Adobe se complace en anunciar la [Despliegue de GA](/help/release-notes/release-notes-cloud/release-notes-current.md#real-use-monitoring) para el servicio de monitorización de uso real, la recopilación de datos del lado del cliente. Es un servicio automatizado y no se requiere ninguna configuración del cliente.

>[!INFO]
>
>La monitorización del lado del cliente solo funciona para clientes con la versión de AEM Cloud Service **2024.5.16461** y superior.

## Información general {#overview}

El servicio Real Use Monitoring (RUM) es una tecnología de monitorización del rendimiento que captura y analiza las experiencias de los usuarios digitales de un sitio web o aplicación en tiempo real. Proporciona visibilidad del rendimiento en tiempo real de una aplicación web y proporciona una perspectiva más detallada de la experiencia del usuario final. &quot;Control de usuarios reales&quot; se ha cambiado a &quot;Control de uso real&quot; porque refleja mejor la verdadera esencia del servicio. El servicio se centra en optimizar el rendimiento mediante la supervisión de las participaciones en sitios web, en lugar de en los propios usuarios.

Con RUM, las métricas de rendimiento clave se rastrean desde el inicio de la dirección URL hasta que la solicitud se devuelve al explorador. Ayuda a los desarrolladores a mejorar la aplicación para facilitar su uso a los usuarios finales.

## ¿Quién puede beneficiarse de un servicio de monitorización de uso real? {#who-can-benefit-from-rum-service}

El servicio de Monitorización de Uso Real es beneficioso para todos los clientes. Ofrece un reflejo representativo de las interacciones del usuario, lo que garantiza una medida fiable de la participación del sitio web al capturar el número de vistas de página del lado del cliente.

Para todos los clientes de Adobe, este servicio proporciona información valiosa sobre las interacciones del usuario. Los clientes que utilizan su propia CDN pueden beneficiarse de la creación de informes de tráfico simplificados, ya que Adobe ahora integra directamente la recopilación de datos, lo que elimina la necesidad de crear informes separados durante los ciclos de renovación.

## Comprender el funcionamiento del servicio de monitorización de uso real {#understand-how-the-rum-service-works}

Adobe Experience Manager AEM () utiliza la Monitorización de uso real (RUM) para ayudar a los clientes y al Adobe AEM a comprender cómo los visitantes interactúan con los sitios de la. Les ayuda a diagnosticar problemas de rendimiento y a medir la eficacia de los experimentos. RUM preserva la privacidad de los visitantes a través del muestreo (solo se supervisa una pequeña parte de todas las vistas de página) y no se recopila información de identificación personal (PII).

## Servicio de monitoreo de uso real y privacidad {#rum-service-and-privacy}

AEM El servicio de Monitorización de uso real de la aplicación está diseñado para preservar la privacidad del visitante y minimizar la recopilación de datos. Como visitante, significa que el sitio que está visitando o que se ha puesto a disposición del Adobe no recopila información personal.

Como operador de sitio, no se requiere ninguna opción de inclusión adicional para habilitar la monitorización a través de esta función. No hay ningún formulario emergente o de consentimiento adicional que los usuarios finales deban aceptar para habilitar RUM.

## Muestreo de datos del servicio de monitorización de uso real {#rum-service-data-sampling}

Las soluciones tradicionales de análisis web intentan recopilar datos de cada visitante. AEM El servicio de RUM de solo captura información de una pequeña fracción de las vistas de página. El servicio está diseñado para ser muestreado y anonimizado, en lugar de un reemplazo para el análisis. De forma predeterminada, las páginas tienen una proporción de muestreo de 1:100. Los operadores de sitio no pueden aumentar ni disminuir la tasa de muestreo en este momento. Para calcular el tráfico total con precisión, por cada 100 vistas de página, se recopilan datos de 1, lo que le proporciona una aproximación fiable del tráfico general.

A medida que se decide si los datos se recopilan, se toman por vista de página por vista de página, y resulta prácticamente imposible rastrear las interacciones en varias páginas. Por diseño, RUM no tiene concepto de visitantes o sesiones, solo de vistas de página.

## Qué datos se recopilan {#what-data-is-being-collected}

El servicio de Monitoreo de Uso Real está diseñado para evitar la recopilación de información personal. El conjunto completo de información recopilada por RUM se enumera a continuación:

* El nombre de host del sitio que se está visitando, por ejemplo: `experienceleague.adobe.com`
* El tipo de agente de usuario y el sistema operativo generales que se utilizan para mostrar la página, como: `desktop:windows` o `mobile:ios`
* El momento de la recopilación de datos, como por ejemplo: `2021-06-26 06:00:02.596000 UTC (in order to preserve privacy, we round all minutes to the previous hour, so that only seconds and milliseconds are tracked)`
* La dirección URL de la página que se está visitando, por ejemplo: `https://experienceleague.adobe.com/docs`
* La URL del referente (la URL de la página que está vinculada a la página actual, si el usuario ha seguido un vínculo)
* ID de la vista de página generado aleatoriamente, con un formato similar al siguiente: `2Ac6`
* El peso o la inversa de la velocidad de muestreo, como: `100`. Significa que solo se registra una de cada cien vistas de página
* El punto de comprobación, o nombre, de un evento concreto en la secuencia de carga de la página. O bien, interactuar con él como visitante
* El origen, o identificador, del elemento DOM con el que interactúa el usuario para el punto de comprobación mencionado anteriormente. Por ejemplo, podría ser una imagen
* El objetivo o vínculo a una página o recurso externo con el que el usuario interactúa para el punto de comprobación mencionado anteriormente. Por ejemplo: `https://blog.adobe.com/jp/publish/2022/06/29/media_162fb947c7219d0537cce36adf22315d64fb86e94.png`
* Las métricas de rendimiento de elementos vitales de la web (CWV) principales, como Pintado de contenido más grande (LCP), Primer retraso de entrada (FID), Cambio de diseño acumulativo (CLS) y Tiempo hasta el primer byte (TTFB), que describen la calidad de experiencia del visitante.

## Funcionamiento de la monitorización de uso real para un cliente {#how-rum-works-for-a-customer}

Real Use Monitoring supervisa automáticamente el tráfico del lado del cliente para proporcionarle información valiosa. Como cliente de Adobe, no necesita realizar ningún paso adicional, ya que este servicio está perfectamente integrado en su configuración existente. Con el despliegue de General Availability (GA), se beneficia automáticamente de esta nueva función.

<!-- Alexandru: hiding temporarily, until we figure out where this needs to be linked to 

If you wish to leverage more insights with this new feature to optimize your digital experiences effortlessly, please see here (link to Row 99). -->

## Cómo se utilizan los datos del servicio de monitorización de uso real {#how-rum-service-data-is-being-used}

Los datos de RUM son beneficiosos para los siguientes propósitos:

* Para identificar y corregir los cuellos de botella de rendimiento de las ubicaciones de los clientes
* Para optimizar la búsqueda automatizada de tráfico que incluye las vistas de página.
* AEM Para comprender cómo interactúa la con otros scripts (como análisis, segmentación o bibliotecas externas) en la misma página, aumente la compatibilidad.

## Limitaciones y comprensión de la variación en las vistas de página y las métricas de rendimiento {#limitations-and-understanding-variance-in-page-views-and-performance-metrics}

A medida que analiza los datos de RUM, puede haber variaciones en las vistas de página y otras métricas de rendimiento. Estas variaciones pueden atribuirse a varios factores inherentes a la monitorización en tiempo real del lado del cliente. Estas son las consideraciones clave que los clientes deben tener en cuenta al interpretar sus datos de RUM:

1. **Bloqueadores de rastreadores**

   * Los usuarios finales que utilizan bloqueadores de rastreadores o extensiones de privacidad pueden impedir la recopilación de datos de RUM, ya que estas herramientas restringen la ejecución de los scripts de seguimiento. Esta restricción puede provocar que no se informe lo suficiente sobre las vistas de páginas y las interacciones del usuario, lo que crea una discrepancia entre la actividad real del sitio y los datos capturados por RUM.

1. **Limitaciones al capturar llamadas API/JSON sin encabezado**

   * AEM El servicio de datos de RUM se centra en la experiencia del lado del cliente y no captura las llamadas API back-end o JSON realizadas desde una aplicación sin encabezado que no es de la misma clase en este momento. La exclusión de estas llamadas de los datos del servicio RUM crea variaciones de las solicitudes de contenido medidas por CDN Analytics.

## Preguntas más frecuentes {#faq}


1. **¿Pueden los clientes integrar los scripts del servicio RUM con sistemas de terceros como Dynatrace?**

   Sí.

1. **¿Se están recopilando las métricas de constantes web &quot;Interacción con la siguiente pintura&quot;, &quot;Tiempo hasta el primer byte&quot; y &quot;Primera pintura de contenido&quot;?**

   Se recopilan la interacción con la siguiente pintura (INP) y el tiempo hasta el primer byte (TTFB).  La primera pintura con contenido no se recopila en este momento.

1. **El `/.rum` La ruta está bloqueada en mi sitio, ¿cómo debo corregirla?**

   El `/.rum` La ruta es necesaria para que funcione la colección RUM. Si tiene una CDN delante de lo que proporciona el Adobe como parte de AEM as a Cloud Service, asegúrese de que la variable `/.rum` AEM AEM ruta se reenvía al mismo origen de que el resto del contenido de la. Y asegúrese de que no se ajuste de ninguna manera.

1. **¿La recopilación de RUM cuenta para las solicitudes de contenido con fines contractuales?**

   La biblioteca RUM y la colección RUM no cuentan como solicitudes de contenido y no aumentan el número informado de vistas de página o llamadas a la API. Además, para los clientes que utilizan la CDN predeterminada con AEM as a Cloud Service, [colección del lado del servidor](#serverside-collection) es la base de las solicitudes de contenido.

1. **¿Cómo puedo optar por no participar?**

   Adobe recomienda utilizar Real Use Monitoring (RUM) debido a sus importantes ventajas y que puede permitirle optimizar sus experiencias digitales. Puede ofrecer perspectivas valiosas que pueden ayudar a mejorar el rendimiento del sitio web. El servicio está diseñado para ser ininterrumpido y no tiene ningún impacto en el rendimiento de su sitio web.

   La exclusión significa que se pierden estas perspectivas. Sin embargo, si tiene algún problema, póngase en contacto con el Soporte técnico de Adobe.
