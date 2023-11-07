---
title: Explicación de las solicitudes de contenido de Cloud Service
description: Si ha adquirido licencias de solicitud de contenido de Adobe, obtenga información acerca de los tipos de solicitudes de contenido que mide Adobe Experience Cloud as a Service y las variaciones con las herramientas de informes de análisis de una organización.
exl-id: 3666328a-79a7-4dd7-b952-38bb60f0967d
source-git-commit: dc01da4c85b37f21deb169b941c0cf2a958298b8
workflow-type: tm+mt
source-wordcount: '1164'
ht-degree: 9%

---

# Solicitudes de contenido de Cloud Service

## Variaciones de solicitudes de contenido de Cloud Service{#content-requests-variances}

Las solicitudes de contenido pueden tener variaciones con las herramientas de informes de Analytics de una organización, como se resume en la siguiente tabla. En general, las herramientas de Analytics recopilan datos mediante instrumentación del lado del cliente <b>no debe utilizarse</b> para informar sobre la cantidad de solicitudes de contenido para un sitio determinado, simplemente porque a menudo dependen del consentimiento del usuario final para activarse, por lo tanto se pierden una fracción significativa del tráfico. AEM Las herramientas de Analytics que recopilan datos del lado del servidor en archivos de registro o los informes de CDN para clientes que agregan su propia CDN además de la as a Cloud Service, proporcionarán mejores recuentos de datos. Para informar sobre Vistas de página, así como su rendimiento asociado, el Servicio de datos de Adobe RUM es la opción recomendada por el Adobe.

| Motivo de la variación | Explicación |
|---|---|
| Consentimiento del usuario final | Las herramientas de Analytics que dependen de instrumentos del lado del cliente suelen depender del consentimiento del usuario final para activarse. Esto podría representar la mayoría del tráfico que no se rastrea. Para los clientes que deseen medir las solicitudes de contenido por su cuenta, se recomienda confiar en las herramientas de análisis que recopilan informes del lado del servidor o de CDN. |
| Etiquetado | Es posible que todas las páginas o llamadas a la API que se rastrean como solicitudes de contenido de Adobe Experience Manager AEM () no estén etiquetadas con el seguimiento de Analytics. |
| Reglas de administración de etiquetas | La configuración de reglas de administración de etiquetas puede dar como resultado varias configuraciones de recopilación de datos en una página, lo que da como resultado una combinación de discrepancias con el seguimiento de solicitudes de contenido. |
| Bots | Los bots desconocidos que no han sido identificados previamente y eliminados por AEM pueden causar discrepancias de seguimiento. |
| Grupos de informes | Las páginas que forman parte de la misma instancia de AEM y del mismo dominio pueden enviar datos a diferentes grupos de informes de Analytics. |
| Herramientas de seguridad y monitorización de terceros | Las herramientas de monitorización y análisis de seguridad pueden generar solicitudes de contenido para AEM que no se rastrean en informes de Analytics. |
| Acceso a API | El acceso mediante programación a páginas o a API de Adobe Experience Manager AEM puede generar solicitudes de contenido para las que no se realiza un seguimiento en los informes de Analytics y que no se rastrean en los informes de. |
| Solicitudes de recuperación previa | El uso de un servicio de recuperación previa para cargar previamente las páginas a fin de aumentar la velocidad puede provocar aumentos significativos en el tráfico de las solicitudes de contenido. |
| DDOS | Mientras el Adobe intenta detectar y filtrar automáticamente el tráfico de los ataques de DDOS, no hay garantías de que se detecten todos los ataques de DDOS posibles. |
| Bloqueadores de tráfico | El uso de un bloqueador de tráfico en un explorador puede excluir el seguimiento de algunas solicitudes. |
| Firewalls | Los firewalls pueden bloquear el seguimiento de Analytics. Este escenario es más frecuente con los servidores de seguridad corporativos. |

Consulte también [Tablero de licencias](/help/implementing/cloud-manager/license-dashboard.md).

## Explicación de las solicitudes de contenido de Cloud Service {#about-content-request}

Las solicitudes de contenido se rastrean automáticamente en el perímetro de Adobe Experience Manager AEM () as a Cloud Service AEM, a través del análisis automatizado de los archivos de registro procedentes de la CDN as a Cloud Service de la, aislando las solicitudes que devuelven contenido de HTML (text/html) o JSON (application/json) de la CDN y en función de una serie de reglas de inclusión y exclusión detalladas a continuación. AEM Una solicitud de contenido se produce de forma independiente del contenido devuelto que se proporciona desde las cachés de CDN o que vuelve al origen de CDN (Dispatcher de).

AEM Para los clientes que aportan su propia CDN además de las as a Cloud Service, este seguimiento dará como resultado números que no se pueden usar para comparar con las solicitudes de contenido con licencia, que tendrán que ser medidos por el cliente en el extremo de la CDN externa.

Existen reglas para excluir bots conocidos, incluidos servicios bien conocidos que visitan el sitio regularmente para actualizar su índice de búsqueda o servicio.

### Tipos de solicitudes de contenido incluidas{#included-content-requests}

| Tipo de solicitud | Solicitud de contenido | Descripción |
| --- | --- | --- |
| Código HTTP 100-299 | Incluido | Son solicitudes regulares que entregan todo el contenido o parte del mismo. |
| Bibliotecas HTTP para automatización | Incluido | Ejemplos:<br>· Amazon CloudFront<br>· Cliente Http De Apache<br>· Cliente Http Asincrónico<br>· Axios<br>· Azureus<br>· Curl<br>· Recuperación del nodo de GitHub<br>· Guzzle<br>· Go-http-client<br>· Cromo sin encabezado<br>· Cliente Java™<br>· Jersey<br>· Oembed del nodo<br>· okhttp<br>· Solicitudes de Python<br>· Reactor Netty<br>· Wget<br>· WinHTTP |
| Herramientas de monitorización y comprobación de estado | Incluido | El cliente las configura para monitorizar un determinado aspecto del sitio. Por ejemplo, disponibilidad o rendimiento del usuario en el mundo real. Uso `/system/probes/health` y no las páginas del HTML real del sitio.<br>Ejemplos:<br>· Amazon-Route53-Health-Check-Service<br>· EyeMonIT_bot_version_0.1_[(https://www.eyemon.it/)](https://www.eyemon.it/)<br>· Investis-Site24x7<br>· Mozilla/5.0+(compatible; UptimeRobot/2.0; [https://uptimerobot.com/](https://uptimerobot.com/))<br>· ThousandEyes-Dragonfly-x1<br>· OmtrBot/1.0<br>· WebMon/2.0.0 |
| `<link rel="prefetch">` solicitudes | Incluido | Para aumentar la velocidad de carga de la página siguiente, los clientes pueden hacer que el explorador cargue un conjunto de páginas antes de que el usuario haga clic en el vínculo, por lo que ya están en la caché. *Mente: Esto está aumentando significativamente el tráfico*: en función de cuántas de estas páginas se hayan recuperado previamente. |
| Tráfico que bloquea los informes de Adobe Analytics o Google Analytics | Incluido | Es más común que los visitantes de los sitios tengan instalado software de privacidad (bloqueadores de anuncios, etc.) que afecta a la precisión de los Google Analytics o Adobe Analytics. AEM El recuento as a Cloud Service de solicitudes en el primer punto de entrada en la infraestructura operada por el Adobe y no en el lado del cliente. |

Consulte también [Tablero de licencias](/help/implementing/cloud-manager/license-dashboard.md).

### Tipos de solicitudes de contenido excluido{#excluded-content-request}

| Tipo de solicitud | Solicitud de contenido | Descripción |
| --- | --- | --- |
| Código HTTP 500+ | Excluido | AEM Se devuelven errores al visitante cuando algo sale mal en el código as a Cloud Service o en el código personalizado del cliente, o cuando se produce un error en el mismo. |
| Código HTTP 400-499 | Excluido | Se devuelven errores al visitante cuando el contenido no existe (404) o hay otros problemas relacionados con el contenido o la solicitud. |
| Código HTTP 300-399 | Excluido | Son solicitudes correctas que comprueban si algo ha cambiado en el servidor o redirigen la solicitud a otro recurso. No contienen contenido en sí, por lo que no son facturables. |
| Solicitudes que se dirigen a /libs/* | Excluido | AEM Las solicitudes JSON internas de la, como el token de CSRF, que no es facturable. |
| Tráfico de ataques DDOS | Excluido | Protección DDOS. AEM La detección automática de algunos de los ataques de DDOS y los bloquean es buena. Los ataques de DDOS si se detectan no son facturables. |
| AEM Monitorización as a Cloud Service de NewRelic | Excluido | AEM Monitoreo global as a Cloud Service. |
| URL para que los clientes supervisen su programa de Cloud Service | Excluido | URL recomendada para monitorizar externamente la disponibilidad.<br><br>`/system/probes/health` |
| AEM Servicio de calentamiento del pod as a Cloud Service | Excluido | Agente de usuario: skyline-service-warmup/1.* |
| Motores de búsqueda, redes sociales y bibliotecas HTTP conocidos (etiquetados por Fastly) | Excluido | Servicios conocidos que visitan el sitio regularmente para actualizar su índice de búsqueda o servicio:<br><br>Ejemplos:<br>· AddSearchBot<br>· AhrefsBot<br>· Applebot<br>· Pregúntale a Jeeves Corporate Spider<br>· Bingbot<br>· BingPreview<br>· BLEXBot<br>· Construido con<br>· Bytespider<br>· CrawlerKengo<br>· Visita externa de Facebook<br>· Google AdsBot<br>· Google AdsBot Mobile<br>· Googlebot<br>· Googlebot móvil<br>· lmspider<br>· LucidWorks<br>· MJ12bot<br>· PKingdom<br>· Pinterest<br>· SemrushBot<br>· SiteMejora<br>· StashBot<br>· StatusCake<br>· YandexBot |
| Excluir llamadas al Commerce integration framework | Excluido | AEM Se trata de solicitudes realizadas a los que se reenvían al Commerce integration framework (la dirección URL comienza por ) `/api/graphql`—para evitar el recuento doble, no son facturables para el Cloud Service. |
| Excluir `manifest.json` | Excluido | El manifiesto no es una llamada de API y sirve para proporcionar información sobre cómo instalar sitios web en equipos de escritorio o teléfonos móviles. El Adobe no debe contar la solicitud JSON a `/etc.clientlibs/*/manifest.json` |
| Excluir `favicon.ico` | Excluido | Aunque el contenido devuelto no debe ser HTML ni JSON, observamos que en algunos casos, como en los flujos de autenticación SAML, los iconos favoritos se pueden devolver como HTML y, por lo tanto, se excluyen explícitamente del recuento. |
