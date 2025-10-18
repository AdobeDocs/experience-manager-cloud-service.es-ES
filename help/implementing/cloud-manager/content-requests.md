---
title: Explicación de las solicitudes de contenido de Cloud Service
description: Si ha adquirido licencias de solicitud de contenido de Adobe, obtenga información acerca de los tipos de solicitudes de contenido que mide Adobe Experience Cloud as a Service y las variaciones con las herramientas de informes de análisis de una organización.
exl-id: 3666328a-79a7-4dd7-b952-38bb60f0967d
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 62e4b038c3fbae0ca5b6bb08c1d9d245842aeab2
workflow-type: tm+mt
source-wordcount: '1580'
ht-degree: 3%

---

# Comprender las solicitudes de contenido de Cloud Service

## Introducción {#introduction}

Las solicitudes de contenido incluyen solicitudes enviadas a AEM Sites. Estas solicitudes pueden enrutarse a través de Edge Delivery Services o de sistemas de almacenamiento en caché proporcionados por el cliente, como una red de distribución de contenido (CDN). Estas solicitudes ofrecen datos estructurados en formato HTML o JSON y admiten vistas de página (por ejemplo, páginas y fragmentos de experiencias) o devoluciones JSON a través de API de manera directa.

El sistema cuenta las solicitudes de contenido cuando un usuario ve una página mediante HTML o JSON. Mide la solicitud en el punto en el que la recibe el primer sistema de almacenamiento en caché. Algunas solicitudes HTTP se incluyen o excluyen con el fin de contar las solicitudes de contenido. Vea la lista completa de [solicitudes de contenido incluidas](#included-content-requests) y [solicitudes de contenido excluidas](#excluded-content-request) de HTTP.

>[!NOTE]
>
>Los datos que se muestran en la vista Solicitudes de contenido se actualizan cada 24 horas.

## Acerca de las solicitudes de contenido de Cloud Service {#understanding-cloud-service-content-requests}

Una *solicitud de página* hace referencia a una solicitud HTTP que recupera el contenido estructurado principal (por ejemplo, HTML o JSON) necesario para procesar la experiencia de la página principal. No incluye solicitudes de recursos, como imágenes o secuencias de comandos.

Para los clientes que utilizan la CDN predeterminada, AEM as a Cloud Service cuenta las solicitudes de contenido medidas en el nivel del lado del servidor. Esta medición se produce automáticamente y no depende del seguimiento del análisis del lado del cliente.

AEM (Adobe Experience Manager) as a Cloud Service identifica las solicitudes de contenido en función de los tipos de respuesta generados por la instancia de AEM y recibidos en la CDN. En concreto, se cuentan las solicitudes que devuelven HTML (`text/html`) o JSON (`application/json`). Estos formatos suelen proporcionar contenido de página principal para la representación tradicional del sitio o para la entrega sin encabezado.

Las solicitudes de recursos estáticos, como archivos JavaScript, hojas de estilo CSS e imágenes, no se cuentan como solicitudes de contenido.

>[!NOTE]
>Si una solicitud de API devuelve un HTML o JSON que sirve como contenido de nivel de página (por ejemplo, en una entrega sin encabezado), se puede seguir contando como una solicitud de contenido en función de su contexto.

Las solicitudes de contenido se miden independientemente de si la respuesta se proporcionó desde la caché de CDN o se reenvió al entorno de AEM de origen.

<!-- REMOVED AS PER EMAIL REQUEST FROM SHWETA DUA, JULY 30, 2024 TO RICK BROUGH AND ALEXANDRU SARCHIZ   For customers employing their own CDN, client-side collection offers a more precise reflection of interactions, ensuring a reliable measure of website engagement via the [Real Use Monitoring](/help/sites-cloud/administering/real-use-monitoring-for-aem-as-a-cloud-service.md) service. This gives customers advanced insights into their page traffic and performance. While it is beneficial for all customers, it offers a representative reflection of user interactions, ensuring a reliable measure of website engagement by capturing the number of page views from the client side. 

For customers that bring their own CDN on top of AEM as a Cloud Service, server-side reporting results in numbers that cannot be used to compare with the licensed content requests. With the [Real Use Monitoring](/help/sites-cloud/administering/real-use-monitoring-for-aem-as-a-cloud-service.md), Adobe can reflect a reliable measure of website engagement. -->

### Variaciones de solicitudes de contenido de Cloud Service {#content-requests-variances}

Las solicitudes de contenido pueden tener variaciones dentro de las herramientas de informes de análisis de una organización, como se resume en la siguiente tabla. En general, evite utilizar herramientas de análisis que dependan de la instrumentación del lado del cliente para informar del número de solicitudes de contenido de un sitio. Estas herramientas suelen pasar por alto una gran parte del tráfico porque dependen del consentimiento del usuario para activarse. Las herramientas de Analytics que recopilan datos del lado del servidor en archivos de registro o los informes de CDN para clientes que agregan su propia CDN además de AEM as a Cloud Service ofrecen mejores recuentos.

| Motivo de la variación | Explicación |
|---|---|
| Consentimiento del usuario final | Las herramientas de Analytics que dependen de la instrumentación del lado del cliente suelen depender del consentimiento del usuario para activarse. Este flujo de trabajo podría representar la mayoría del tráfico que no se rastrea. Para los clientes que deseen medir las solicitudes de contenido por su cuenta, Adobe recomienda que confíe en las herramientas de análisis para recopilar datos de informes del lado del servidor o de CDN. |
| Etiquetado | Todas las páginas o llamadas a la API que se rastrean como solicitudes de contenido de Adobe Experience Manager pueden no estar etiquetadas con el seguimiento de Analytics. |
| Reglas de administración de etiquetas | La configuración de reglas de administración de etiquetas puede dar como resultado varias configuraciones de recopilación de datos en una página, lo que da como resultado una combinación de discrepancias con el seguimiento de solicitudes de contenido. |
| Bots | Los bots desconocidos que AEM no ha identificado previamente y eliminado pueden causar discrepancias de seguimiento. |
| Grupos de informes | Las páginas dentro de la misma instancia de AEM pueden informar a diferentes grupos de informes de análisis. Este proceso puede dividir los datos en varios grupos de informes, según la configuración. |
| Herramientas de seguridad y monitorización de terceros | Las herramientas de monitorización y análisis de seguridad (por ejemplo, los comprobadores de tiempo de actividad o los analizadores de vulnerabilidades) pueden solicitar páginas y generar solicitudes de contenido del lado del servidor que no son visibles en los informes de análisis. |
| Acceso a API | Las solicitudes a páginas de AEM o contenido a través de API (por ejemplo, mediante Adobe Experience Manager as a Headless CMS) siguen contando como solicitudes de contenido, pero no almacenan en déclencheur el seguimiento de Analytics. |
| Solicitudes de recuperación previa | La recuperación previa (por ejemplo, mediante un trabajo de servicio o una función perimetral) puede aumentar los volúmenes de tráfico al solicitar páginas por adelantado. Estas solicitudes se cuentan del lado del servidor, pero no ejecutan el código de Analytics del lado del cliente. |
| DDOS | Adobe utiliza el filtrado para detectar y bloquear muchos ataques DDoS. Sin embargo, algunas solicitudes de ataque se pueden seguir contando como solicitudes de contenido antes de que se apliquen los filtros. |
| Bloqueadores de tráfico | Las funciones de privacidad en el explorador o los servidores de seguridad corporativos pueden bloquear la carga de scripts de análisis. Estos usuarios siguen generando solicitudes de contenido del lado del servidor. |
| Cortafuegos | Los cortafuegos corporativos o regionales pueden impedir que las llamadas de Analytics lleguen a los servidores de Adobe, lo que provoca una creación de informes insuficiente en Analytics mientras que los recuentos del lado del servidor no se ven afectados. |

Consulte [Tablero de licencias](/help/implementing/cloud-manager/license-dashboard.md) para obtener información sobre cómo ver y rastrear el uso de solicitudes de contenido en relación con sus límites de licencias.

## Reglas de recopilación del lado del servidor {#serverside-collection}

AEM as a Cloud Service aplica reglas del lado del servidor para contar las solicitudes de contenido. Estas reglas incluyen lógica para excluir bots conocidos (como rastreadores de motores de búsqueda) y tráfico que no sea de usuario, como servicios de monitorización que hacen ping regularmente al sitio.

En las tablas siguientes se enumeran los tipos de solicitudes de contenido incluidas y excluidas, con breves descripciones de cada una.

### Tipos de solicitudes de contenido incluidas {#included-content-requests}

>[!NOTE]
>Si una solicitud de API devuelve una respuesta de HTML, puede clasificarse como solicitud de contenido, según su contexto de uso. Las solicitudes de API que devuelven datos que no son de la interfaz de usuario generalmente se excluyen.

| Tipo de solicitud | Solicitud de contenido | Descripción |
| --- | --- | --- |
| Código HTTP 100-299 | Incluido | Incluye solicitudes correctas que devuelven contenido HTML o JSON completo o parcial.<br>Código HTTP 206: estas solicitudes entregan solamente una parte del contenido completo. Por ejemplo, un vídeo o una imagen grande. Las solicitudes de contenido parciales se incluyen cuando entregan parte de una respuesta HTML o JSON utilizada para procesar contenido de página. |
| Bibliotecas HTTP para automatización | Incluido | Solicitudes realizadas por herramientas o bibliotecas que recuperan contenido de la página. Algunos ejemplos son los siguientes: <br>· Amazon CloudFront<br>· Cliente HTTP Apache<br>· Cliente HTTP asincrónico<br>· Axios<br>· Azureus<br>· Curl<br>· Recuperación del nodo GitHub<br>· Guzzle<br>· Cliente Go-http<br>· Chrome sin encabezado<br>· Cliente Java™<br>· Jersey<br>· Nodo Oembed<br>· okhttp<br>· Solicitudes Python<br>· Reactor Netty<br>· Wget<br>· WinHTTP<br>· HTTP rápido<br>· Recuperación del nodo de GitHub<br>· Reactor Netty |
| Herramientas de monitorización y comprobación de estado | Incluido | Solicitudes que se utilizan para supervisar el estado o la disponibilidad de las páginas.<br>Ver [Tipos de solicitudes de contenido excluido](#excluded-content-request).<br>Algunos ejemplos son:<br>· `Amazon-Route53-Health-Check-Service`<br>· EyeMonIT_bot_version_0.1_[(https://eyemonit.com/)](https://eyemonit.com/)<br>· Investis-Site24x7<br>· Mozilla/5.0+(compatible; UptimeRobot/2.0; [https://uptimerobot.com/](https://uptimerobot.com/))<br>· ThousandEyes-Dragonfly-x1<br>· OmtrBot/1.0<br>· WebMon/2.0.0 |
| `<link rel="prefetch">` solicitudes | Incluido | Cuando los clientes cargan previamente o recuperan previamente contenido (por ejemplo, con `<link rel="prefetch">`), el sistema cuenta esas solicitudes del lado del servidor. Tenga en cuenta que este método puede aumentar el tráfico, en función de cuántas de estas páginas se recuperen previamente. |
| Tráfico que bloquea los informes de Adobe Analytics o Google Analytics | Incluido | Es más común que los visitantes de los sitios tengan instalado software de privacidad (bloqueadores de anuncios, etc.) que afecta a la precisión de Google Analytics o Adobe Analytics. AEM as a Cloud Service cuenta las solicitudes en el primer punto de entrada en la infraestructura operada por Adobe y no en el lado del cliente. |

Ver también [Tablero de licencias](/help/implementing/cloud-manager/license-dashboard.md).

### Tipos de solicitudes de contenido excluido {#excluded-content-request}

| Tipo de solicitud | Solicitud de contenido | Descripción |
| --- | --- | --- |
| Código HTTP 500+ | Excluido | Se devuelven errores al visitante cuando algo sale mal en AEM as a Cloud Service o en el código personalizado del cliente. |
| Código HTTP 400-499 | Excluido | Se devuelven errores al visitante cuando el contenido no existe (404) o hay otros problemas relacionados con el contenido o la solicitud. |
| Código HTTP 300-399 | Excluido | Solicitudes correctas que comprueban si algo ha cambiado en el servidor o redirigen la solicitud a otro recurso. No contienen contenido en sí, por lo que no son facturables. |
| Solicitudes que se dirigen a `/libs/`* | Excluido | Solicitudes JSON internas de AEM, como el token CSRF, que no es facturable. |
| Tráfico de ataques DDOS | Excluido | Protección DDOS. AEM detecta automáticamente algunos de los ataques de DDOS y los bloquea. Los ataques de DDOS si se detectan no son facturables. |
| Monitorización de AEM as a Cloud Service New Relic | Excluido | Monitorización global de AEM as a Cloud Service. |
| URL para que los clientes supervisen su programa de Cloud Service | Excluido | Adobe recomienda usar la dirección URL para supervisar externamente la disponibilidad o la comprobación de estado.<br><br>`/system/probes/health` |
| Servicio de calentamiento de AEM as a Cloud Service Pod | Excluido |
| Agente: skyline-service-warmup/1.* |
| Motores de búsqueda, redes sociales y bibliotecas HTTP conocidos (etiquetados por Fastly) | Excluido | Servicios conocidos que visitan el sitio con regularidad para actualizar el índice de búsqueda o el servicio:<br><br>Ejemplos:<br>· AddSearchBot<br>· AhrefsBot<br>· Applebot<br>· Preguntar a Jeeves Corporate Spider<br>· Bingbot<br>· BingPreview<br>· BLEXBot<br>· BuiltWith<br>· Bytespider<br>· CrawlerKengo<br>· Facebookexternalhit<br>· Google AdsBot<br>· Móvil Google AdsBot<br>· Googlebot<br>· Móvil Googlebot<br>· lmspider<br>· LucidWorks<br>· `MJ12bot`<br>· Pinterest<br>· SemrushBot<br>· SiteMejora<br>· StashBot<br>· StatusCake<br>· YandexBot<br>· ContentKing<br> |
| Excluir llamadas de Commerce integration framework | Excluido | Las solicitudes realizadas a AEM que se reenvíen a Commerce integration framework (la dirección URL comienza con `/api/graphql`) para evitar el recuento doble, no se pueden facturar en Cloud Service. |
| Excluir `manifest.json` | Excluido | El manifiesto no es una llamada de API. Se encuentra aquí para proporcionar información sobre cómo instalar sitios web en un escritorio o teléfono móvil. Adobe no debe contar la solicitud JSON a `/etc.clientlibs/*/manifest.json` |
| Excluir `favicon.ico` | Excluido | Aunque el contenido devuelto no debe ser HTML ni JSON, se ha observado que ciertos escenarios como los flujos de autenticación SAML devuelven iconos favoritos como HTML. Como resultado, los iconos favoritos se excluyen explícitamente del recuento. |
| Fragmento de experiencia (XF): reutilización del mismo dominio | Excluido | Solicitudes realizadas a rutas XF (como `/content/experience-fragments/...`) desde páginas alojadas en el mismo dominio (identificado por el encabezado Referente que coincide con el host de solicitud).<br><br> Ejemplo: Una página de inicio en `aem.customer.com` que extrae un XF para un titular o una tarjeta del mismo dominio.<br><br>· La dirección URL coincide con /content/experience-fragments/...<br>· El dominio de referente coincide con `request_x_forwarded_host`<br><br>**Nota:** Si la ruta del fragmento de experiencia está personalizada (por ejemplo, mediante `/XFrags/...` o cualquier ruta de acceso fuera de `/content/experience-fragments/`), la solicitud no se excluye y se puede contar. Este resultado es válido incluso si es del mismo dominio. Adobe recomienda utilizar la estructura de rutas estándar de XF de Adobe para garantizar que la lógica de exclusión se aplique correctamente. |
