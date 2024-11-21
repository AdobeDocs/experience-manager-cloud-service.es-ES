---
title: Explicación de las solicitudes de contenido de Cloud Service
description: Si ha adquirido licencias de solicitud de contenido de Adobe, obtenga información acerca de los tipos de solicitudes de contenido que mide Adobe Experience Cloud as a Service y las variaciones con las herramientas de informes de análisis de una organización.
exl-id: 3666328a-79a7-4dd7-b952-38bb60f0967d
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: f24b2672431ecf7b7b0ed11b6dc9b09344946239
workflow-type: tm+mt
source-wordcount: '1276'
ht-degree: 9%

---

# Comprender las solicitudes de contenido del Cloud Service

## Introducción {#introduction}

Las solicitudes de contenido hacen referencia a solicitudes realizadas a AEM Sites, incluidas las solicitudes relacionadas con Edge Delivery Services o sistemas de almacenamiento en caché proporcionados por el cliente, como una red de distribución de contenido. Estas solicitudes envían contenido o datos en formato HTML a través de vistas de página (por ejemplo, páginas y fragmentos de experiencias) o en formato JSON a través de llamadas de API de forma directa. Las solicitudes de contenido se cuentan como una vista de página o como cinco llamadas a la API y se miden a la entrada del primer sistema de almacenamiento en caché que recibe una solicitud de contenido. Algunas solicitudes HTTP se incluyen o excluyen con el fin de contar las solicitudes de contenido. La lista completa de dichas solicitudes HTTP incluidas y excluidas, y sus definiciones técnicas, están disponibles en la documentación.

## Acerca de las solicitudes de contenido de Cloud Service {#understanding-cloud-service-content-requests}

Para los clientes que utilizan la CDN predeterminada, las solicitudes de contenido de los Cloud Service se miden mediante la recopilación de datos del lado del servidor. Esta colección se habilita mediante el análisis de registro de CDN. AEM (Adobe Experience Manager) as a Cloud Service recopila automáticamente solicitudes de contenido del lado del servidor en el perímetro de. Analiza los archivos de registro generados por la CDN de AEM as a Cloud Service. Este proceso se realiza aislando las solicitudes que devuelven contenido de HTML `(text/html)` o JSON `(application/json)` de la CDN, y se basa en varias reglas de inclusión y exclusión detalladas a continuación. AEM Se produce una solicitud de contenido independientemente de si el contenido se sirve desde las cachés de CDN o se devuelve al origen de CDN (Dispatcher de).

<!-- REMOVED AS PER EMAIL REQUEST FROM SHWETA DUA, JULY 30, 2024 TO RICK BROUGH AND ALEXANDRU SARCHIZ   For customers employing their own CDN, client-side collection offers a more precise reflection of interactions, ensuring a reliable measure of website engagement via the [Real Use Monitoring](/help/sites-cloud/administering/real-use-monitoring-for-aem-as-a-cloud-service.md) service. This gives customers advanced insights into their page traffic and performance. While it is beneficial for all customers, it offers a representative reflection of user interactions, ensuring a reliable measure of website engagement by capturing the number of page views from the client side. 

For customers that bring their own CDN on top of AEM as a Cloud Service, server-side reporting results in numbers that cannot be used to compare with the licensed content requests. With the [Real Use Monitoring](/help/sites-cloud/administering/real-use-monitoring-for-aem-as-a-cloud-service.md), Adobe can reflect a reliable measure of website engagement. -->

### Variaciones de solicitudes de contenido de Cloud Service {#content-requests-variances}

Las solicitudes de contenido pueden tener variaciones dentro de las herramientas de informes de Analytics de una organización, como se resume en la siguiente tabla. En general, evite utilizar herramientas de análisis que dependan de la instrumentación del lado del cliente para informar del número de solicitudes de contenido de un sitio. Estas herramientas suelen pasar por alto una gran parte del tráfico porque dependen del consentimiento del usuario para activarse. Las herramientas de Analytics que recopilan datos del lado del servidor en archivos de registro o los informes de CDN para clientes que agregan su propia CDN además de AEM as a Cloud Service ofrecen mejores recuentos.

| Motivo de la variación | Explicación |
|---|---|
| Consentimiento del usuario final | Las herramientas de Analytics que dependen de la instrumentación del lado del cliente suelen depender del consentimiento del usuario para activarse. Este flujo de trabajo podría representar la mayoría del tráfico que no se rastrea. Para los clientes que deseen medir las solicitudes de contenido por su cuenta, se recomienda confiar en las herramientas de análisis que recopilan informes del lado del servidor o de CDN. |
| Etiquetado | Todas las páginas o llamadas a la API que se rastrean como solicitudes de contenido de Adobe Experience Manager pueden no estar etiquetadas con el seguimiento de Analytics. |
| Reglas de administración de etiquetas | La configuración de reglas de administración de etiquetas puede dar como resultado varias configuraciones de recopilación de datos en una página, lo que da como resultado una combinación de discrepancias con el seguimiento de solicitudes de contenido. |
| Bots | AEM Los bots desconocidos que no se han identificado previamente y que no se han eliminado pueden causar discrepancias de seguimiento. |
| Grupos de informes | Las páginas que forman parte de la misma instancia de AEM y del mismo dominio pueden enviar datos a diferentes grupos de informes de Analytics. |
| Herramientas de seguridad y monitorización de terceros | Las herramientas de monitorización y análisis de seguridad pueden generar solicitudes de contenido para AEM que no se rastrean en informes de Analytics. |
| Acceso a API | El acceso mediante programación a páginas o a API de Adobe Experience Manager AEM puede generar solicitudes de contenido para las que no se realiza un seguimiento en los informes de Analytics y que no se rastrean en los informes de. |
| Solicitudes de recuperación previa | El uso de un servicio de recuperación previa para cargar previamente las páginas a fin de aumentar la velocidad puede provocar aumentos significativos en el tráfico de las solicitudes de contenido. |
| DDOS | Mientras el Adobe intenta detectar y filtrar el tráfico automáticamente de los ataques de DDOS, no hay garantías de que se detecten todos los ataques de DDOS posibles. |
| Bloqueadores de tráfico | El uso de un bloqueador de tráfico en un explorador puede excluir el seguimiento de algunas solicitudes. |
| Firewalls | Los firewalls pueden bloquear el seguimiento de Analytics. Este escenario es más frecuente con los servidores de seguridad corporativos. |

Ver también [Tablero de licencias](/help/implementing/cloud-manager/license-dashboard.md).

## Reglas de recopilación del lado del servidor {#serverside-collection}

Existen reglas para excluir bots conocidos, incluidos servicios bien conocidos que visitan el sitio regularmente para actualizar su índice de búsqueda o servicio.

### Tipos de solicitudes de contenido incluidas {#included-content-requests}

| Tipo de solicitud | Solicitud de contenido | Descripción |
| --- | --- | --- |
| Código HTTP 100-299 | Incluido | Solicitudes regulares que entregan todo el contenido o parte de él. |
| Bibliotecas HTTP para automatización | Incluido | Ejemplos:<br>· Amazon CloudFront<br>· Cliente Http Apache<br>· Cliente HTTP Asincrónico<br>· Axios<br>· Azureus<br>· Curl<br>· Recuperación del nodo GitHub<br>· Guzzle<br>· Cliente Go-http<br>· Chrome sin encabezado<br>· Cliente Java™<br>· Jersey<br>· Nodo Oembed<br>· okhttp<br>· Solicitudes Python<br>· Reactor Netty<br> · Wget<br>· WinHTTP<br>· HTTP rápido<br>· Recuperación de nodos de GitHub<br>· Red de reactor |
| Herramientas de monitorización y comprobación de estado | Incluido | Configurado por el cliente para monitorizar un determinado aspecto del sitio. Por ejemplo, disponibilidad o rendimiento del usuario en el mundo real. Si se dirigen a extremos específicos como `/system/probes/health` para comprobaciones de estado, Adobe recomienda que utilice el extremo `/system/probes/health` y no las páginas del HTML reales del sitio. [Ver más abajo](#excluded-content-request)<br>Ejemplos:<br>· `Amazon-Route53-Health-Check-Service`<br>· EyeMonIT_bot_version_0.1_[(https://eyemonit.com/)](https://eyemonit.com/)<br>· Investis-Site24x7<br>· Mozilla/5.0+(compatible; UptimeRobot/2.0; [https://uptimerobot.com/](https://uptimerobot.com/))<br>· ThousandEyes-Dragonfly-x1<br>· OmtrBot/1.0<br>· WebMon/2.0 0 |
| `<link rel="prefetch">` solicitudes | Incluido | Para aumentar la velocidad de carga de la página siguiente, los clientes pueden hacer que el explorador cargue un conjunto de páginas antes de que el usuario haga clic en el vínculo, por lo que ya están en la caché. *Mente: este enfoque aumenta significativamente el tráfico*, dependiendo de cuántas de estas páginas se hayan recuperado previamente. |
| Tráfico que bloquea los informes de Adobe Analytics o Google Analytics | Incluido | Es más común que los visitantes de los sitios tengan instalado software de privacidad (bloqueadores de anuncios, etc.) que afecta a la precisión de los Google Analytics o Adobe Analytics. AEM as a Cloud Service cuenta las solicitudes en el primer punto de entrada en la infraestructura operada por Adobe y no en el lado del cliente. |

Ver también [Tablero de licencias](/help/implementing/cloud-manager/license-dashboard.md).

### Tipos de solicitudes de contenido excluido {#excluded-content-request}

| Tipo de solicitud | Solicitud de contenido | Descripción |
| --- | --- | --- |
| Código HTTP 500+ | Excluido | Se devuelven errores al visitante cuando algo sale mal en AEM as a Cloud Service o en el código personalizado del cliente. |
| Código HTTP 400-499 | Excluido | Se devuelven errores al visitante cuando el contenido no existe (404) o hay otros problemas relacionados con el contenido o la solicitud. |
| Código HTTP 300-399 | Excluido | Solicitudes correctas que comprueban si algo ha cambiado en el servidor o redirigen la solicitud a otro recurso. No contienen contenido en sí, por lo que no son facturables. |
| Solicitudes que se dirigen a /libs/* | Excluido | AEM Las solicitudes JSON internas de la, como el token de CSRF, que no es facturable. |
| Tráfico de ataques DDOS | Excluido | Protección DDOS. AEM La detección automática de algunos de los ataques de DDOS y los bloquean es buena. Los ataques de DDOS si se detectan no son facturables. |
| Monitorización de AEM as a Cloud Service New Relic | Excluido | Monitorización global de AEM as a Cloud Service. |
| URL para que los clientes supervisen su programa de Cloud Service | Excluido | El Adobe recomienda usar la dirección URL para supervisar externamente la disponibilidad o la comprobación de estado.<br><br>`/system/probes/health` |
| Servicio de calentamiento de AEM as a Cloud Service Pod | Excluido |
| Agente: skyline-service-warmup/1.* |
| Motores de búsqueda, redes sociales y bibliotecas HTTP conocidos (etiquetados por Fastly) | Excluido | Servicios conocidos que visitan el sitio regularmente para actualizar su índice de búsqueda o servicio:<br><br>Ejemplos:<br>· AddSearchBot<br>· AhrefsBot<br>· Applebot<br>· Preguntar a Jeeves Corporate Spider<br>· Bingbot<br>· BingPreview<br>· BLEXBot<br>· BuiltWith<br>· Bytespider<br>· CrawlerKengo<br>· Facebookexternalhit<br>· Google AdsBot<br> · Google AdsBot Mobile<br>· Googlebot<br>· Googlebot Mobile<br>· lmspider<br>· LucidWorks<br>· `MJ12bot`<br>· Pinterest<br>· SemrushBot<br>· SiteMejora<br>· StashBot<br>· StatusCake<br>· YandexBot<br>· Claudebot |
| Excluir llamadas al Commerce integration framework | Excluido | AEM Las solicitudes realizadas a los que se reenvíen al Commerce integration framework (la dirección URL comienza por `/api/graphql`) para evitar el recuento doble, no se pueden facturar al Cloud Service. |
| Excluir `manifest.json` | Excluido | El manifiesto no es una llamada de API. Se encuentra aquí para proporcionar información sobre cómo instalar sitios web en un escritorio o teléfono móvil. El Adobe no debe contar la solicitud JSON a `/etc.clientlibs/*/manifest.json` |
| Excluir `favicon.ico` | Excluido | Aunque el contenido devuelto no debe ser HTML ni JSON, se ha observado que ciertos escenarios como los flujos de autenticación SAML devuelven iconos favoritos como HTML. Como resultado, los iconos favoritos se excluyen explícitamente del recuento. |
| Proxy de CDN a un servidor diferente | Excluido | AEM AEM Las solicitudes enrutadas a diferentes back-ends que no utilizan la técnica [Selectores de origen de CDN](/help/implementing/dispatcher/cdn-configuring-traffic.md#origin-selectors) se excluyen ya que no llegan a los extremos de la página de inicio de la página de inicio de la página de inicio de la página de. |
