---
title: Monitorización de uso real para AEM as a Cloud Service
description: Aprenda a utilizar el monitoreo de uso real (RUM) para capturar y analizar el experiencia del usuario digital de un sitio web o aplicación en tiempo real.
exl-id: 91fe9454-3dde-476a-843e-0e64f6f73aaf
feature: Administering
role: Admin
source-git-commit: 9a8adf777008b7a601abc8760cee67ec3c1816c6
workflow-type: tm+mt
source-wordcount: '1301'
ht-degree: 0%

---

# Servicio de monitorización de uso real para AEM como Cloud Service {#real-use-monitoring-service-for-aem-as-a-cloud-service}

>[!NOTE]
>
>El servicio de monitoreo de uso real, el lado del cliente colección de datos, es un servicio automatizado. No se requiere configuración de cliente.

>[!INFO]
>
>La supervisión del lado del cliente solo funciona para clientes con AEM Cloud Service versión **2024.5.16461** y superior.

## Información general {#overview}

El servicio de monitoreo de uso real (RUM) es una tecnología de monitoreo de rendimiento que captura y analiza las experiencias de usuario digital de un sitio web o aplicación en tiempo real. Proporciona visibilidad del rendimiento en tiempo real de una aplicación web y proporciona una conocimiento más profunda del experiencia del usuario final. El servicio se centra en optimizar el rendimiento mediante la supervisión de las interacciones en el sitio web, en lugar de los propios usuarios.

Con RUM, las métricas clave de rendimiento se rastrean desde el inicio del URL hasta que el solicitud se devuelve al explorador. Ayuda a los desarrolladores a mejorar el aplicación para que sea fácil de usar para los usuarios finales.

>[!INFO]
>
>&quot;Real User Monitoring&quot; ha sido renombrado a &quot;Real Use Monitoring&quot;, ya que refleja mejor la verdadera esencia del servicio.

## ¿Quién puede beneficiarse de un servicio de monitorización de uso real? {#who-can-benefit-from-rum-service}

El servicio de monitoreo de uso real es beneficioso para todos los clientes. Ofrece un reflejo representativo de usuario interacciones, asegurando una medir confiable de participación del sitio web al capturar el número de lado del cliente Página vistas.

Para todos Adobe Systems clientes, este servicio proporciona información valiosa sobre usuario interacciones. Los clientes que emplean sus propios CDN pueden beneficiarse de la tráfico sistema de informes simplificada, ya que ahora Adobe Systems integra directamente el recopilación de datos, eliminando la necesidad de informes separados durante los ciclos de renovación.

## Comprender cómo funciona el servicio de monitoreo de uso real {#understand-how-the-rum-service-works}

Adobe Experience Manager (AEM) utiliza el monitoreo de uso real (RUM) para ayudar a los clientes y a Adobe Systems comprender cómo interactúan los visitantes con AEM sitios. Les ayuda a diagnosticar problemas de rendimiento y medir la efectividad de los experimentos. RUM preserva la privacidad de los visitantes a través de la muestreo (solo se monitorea una pequeña parte de todas las vistas de Página) y no se recopila información de identificación personal (PII).

## Servicio de monitoreo de uso real y privacidad {#rum-service-and-privacy}

El servicio de monitoreo de uso real en AEM está diseñado para preservar visitante privacidad y minimizar recopilación de datos. Como visitante, significa que el sitio que está visitando o puesto a disposición para Adobe Systems, no recopila ninguna información personal.

Como operador del sitio, no se requiere ningún inclusión adicional para habilitar el monitoreo a través de esta función. No existe ningún formulario de consentimiento o elemento emergente adicional que los usuarios finales puedan aceptar para habilitar RUM.

## Muestreo de datos del servicio de monitoreo de uso real {#rum-service-data-sampling}

Las soluciones de análisis web tradicionales intentan recopilar datos en cada visitante. El servicio RUM de AEM solo captura información de una pequeña fracción de Página vistas. El servicio está destinado a ser muestreado y anonimizado en lugar de un reemplazo de análisis. De forma predeterminada, las páginas tienen una relación muestreo de 1:100. Los operadores del sitio no pueden aumentar o disminuir la tasa de muestreo en este momento. Para estimar la tráfico total con precisión, por cada 100 Página vistas, los datos se recopilan de 1, lo que le brinda una aproximación confiable del tráfico general.

Como la decisión de si los datos se recopilan, se toma en vista de página por vista de página, y se vuelve prácticamente imposible rastrear las interacciones en varias páginas. Por diseño, RUM no tiene concepto de visitantes o sesiones, solo de Página vistas.

## Qué datos se recopilan {#what-data-is-being-collected}

El servicio de monitoreo de uso real está diseñado para evitar el colección de información de identificación personal. El conjunto completo de información recopilada por RUM se enumera a continuación:

* El nombre host del sitio visitado, por ejemplo: `experienceleague.adobe.com`
* El tipo de agente de usuario amplio y el sistema operativo que se utiliza para mostrar el Página, como: `desktop:windows` o bien `mobile:ios`
* La hora de la recopilación de datos, como: `2021-06-26 06:00:02.596000 UTC (in order to preserve privacy, we round all minutes to the previous hour, so that only seconds and milliseconds are tracked)`
* El URL de los Página visitados, por instancia: `https://experienceleague.adobe.com/docs`
* El URL de referente (el URL del Página vinculado al Página actual, si el usuario seguido de un vincular)
* ID generado aleatoriamente del vista de página, en una formato similar a: `2Ac6`
* La peso o inversa de la tasa de muestreo, como: `100`. Esto significa que solo se registra una de cada cien Página vistas
* El punto de comprobación, o nombre, de un evento concreto en el Secuencia de carga del Página. O bien, interactuar con él como un visitante
* El origen, o identificador, del elemento DOM con el que interactúa la usuario durante los punto de comprobación mencionados anteriormente. Por instancia, podría ser una imagen
* El destino o vincular a un Página o recurso externo con el que interactúa el usuario durante los punto de comprobación mencionados anteriormente. Por ejemplo: `https://blog.adobe.com/jp/publish/2022/06/29/media_162fb947c7219d0537cce36adf22315d64fb86e94.png`
* Las métricas de rendimiento de Core Web Vitals (CWV), incluida la pintura contenta más grande (LCP), el primer retraso de entrada (FID), el desplazamiento acumulativo de Diseño (CLS) y el tiempo hasta el primer byte (TTFB) que describen la calidad de experiencia del visitante.

## Cómo funciona la monitorización del uso real para un cliente {#how-rum-works-for-a-customer}

Real Use Monitoring monitorea automáticamente lado del cliente tráfico para proporcionarle información valiosa. Como cliente Adobe Systems, no necesita realizar ningún paso adicional, ya que este servicio se integra perfectamente en su configuración existente. Con el despliegue de disponibilidad general (GA), se beneficia automáticamente de esta nueva función.

<!-- Alexandru: hiding temporarily, until we figure out where this needs to be linked to 

If you wish to leverage more insights with this new feature to optimize your digital experiences effortlessly, please see here (link to Row 99). -->

## Cómo se utilizan los datos del servicio de monitoreo de uso real {#how-rum-service-data-is-being-used}

Los datos del RUM son beneficiosos para los siguientes fines:

* Para identificar y corregir los cuellos de botella de rendimiento para los sitios de los clientes
* Para simplificar la búsqueda de tráfico automatizada que incluye vistas de Página.
* Para comprender cómo interactúa AEM con otros scripts (como análisis, direccionamiento o bibliotecas externos) en el mismo Página, para aumentar la compatibilidad.

## Limitaciones y comprensión de las variaciones en las vistas de Página y las métricas de rendimiento {#limitations-and-understanding-variance-in-page-views-and-performance-metrics}

Al analizar los datos de RUM, puede haber variaciones en las vistas de Página y en otras métricas de rendimiento. Estas variaciones pueden atribuirse a varios factores inherentes al monitoreo de lado del cliente en tiempo real. Aquí hay consideraciones clave que los clientes deben tener en cuenta al interpretar sus datos RUM:

1. **Bloqueadores de rastreadores**

   * Los usuarios finales que emplean bloqueadores de rastreadores o extensiones de privacidad pueden impedir la recopilación de datos RUM, ya que estas herramientas restringen la ejecución de los scripts de seguimiento. Esta restricción puede posible cliente a vistas Página e interacciones usuario no reportadas, creando una discrepancia entre los actividad reales del sitio y los datos capturados por RUM.

1. **Limitaciones en la captura de llamadas API sin periféricos/JSON**

   * El servicio de datos RUM se centra en el lado del cliente experiencia y no captura la API backend o las llamadas JSON realizadas desde una aplicación sin periféricos que no sean AEM en este momento. La exclusión de estas llamadas de los datos del servicio RUM crea diferencias con respecto a las solicitudes de contenido medidas por CDN Analytics.

## Preguntas más frecuentes {#faq}


1. **¿Pueden los clientes integrar los scripts del servicio RUM con terceros sistemas gustar Dynatrace?**

   Sí.

1. **¿Se recopilan las métricas vitales web &quot;Interacción con la siguiente pintura&quot;, &quot;Tiempo hasta el primer byte&quot; y &quot;Primera pintura contenta&quot;?**

   Se recopilan la interacción con la pintura siguiente (INP) y el tiempo hasta el primer byte (TTFB).  La primera pintura contenta no se recoge en este momento.

1. **La `/.rum` ruta está bloqueada en mi sitio, ¿cómo debo solucionarlo?**

   La ruta es necesaria para que RUM `/.rum` colección funcione. Si tiene un CDN frente a lo que Adobe Systems proporciona como parte de AEM como Cloud Service, asegúrese de que el `/.rum` camino a seguir hacia el mismo AEM origen que el resto de su AEM contenido. Y, asegúrese de que no se ajusta de ninguna manera.

1. **¿El RUM colección cuenta para contenido solicitudes con fines contractuales?**

   La biblioteca RUM y la colección RUM no cuentan como solicitudes contenido y no aumentan el número notificado de vistas de Página o llamadas a la API. Además, para los clientes que utilizan CDN originales con AEM como Cloud Service, [del lado del servidor colección](#serverside-collection) es la base de contenido solicitudes.

1. **¿Cómo puedo exclusión?**

   Adobe Systems recomienda utilizar el Real Use Monitoring (RUM) debido a sus importantes beneficios y que puede permitirle optimizar sus experiencias digitales. Puede oferta información valiosa que puede ayudar a mejorar el rendimiento del sitio web. El servicio está diseñado para ser perfecto y no tiene ningún impacto en el rendimiento de su sitio web.

   Optar por no participar significa perder estas ideas. Sin embargo, si se producen problemas, póngase en contacto con el servicio de asistencia técnica de Adobe Systems.
