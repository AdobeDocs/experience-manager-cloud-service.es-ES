---
title: Explicación de las solicitudes de contenido de Cloud Service
description: Si ha adquirido licencias de solicitud de contenido de Adobe, obtenga información acerca de los tipos de solicitudes de contenido que mide Adobe Experience Cloud as a Service y las variaciones con las herramientas de informes de análisis de una organización.
exl-id: 3666328a-79a7-4dd7-b952-38bb60f0967d
source-git-commit: bae9a5178c025b3bafa8ac2da75a1203206c16e1
workflow-type: tm+mt
source-wordcount: '2688'
ht-degree: 5%

---

# Solicitudes de contenido de Cloud Service

## Introducción {#introduction}

Las solicitudes de contenido del Cloud Service se miden mediante la recopilación de datos del lado del servidor. La colección se habilita mediante el análisis de registro de CDN.

>[!NOTE]
>Además, para un número limitado de [Clientes que adoptaron por primera vez](/help/release-notes/release-notes-cloud/release-notes-current.md#sites-early-adopter), la recopilación del lado del cliente también se habilita mediante la medición del servicio de Monitorización de usuarios reales. Para obtener más información, consulte la documentación de [este artículo](#real-user-monitoring-for-aem-as-a-cloud-service).

## Explicación de las solicitudes de contenido de Cloud Service {#understaing-cloud-service-content-requests}

Las solicitudes de contenido se recopilan automáticamente en el lado del servidor en el perímetro de Adobe Experience Manager as a Cloud Service AEM, a través del análisis automatizado de los archivos de registro procedentes de la CDN as a Cloud Service de la red de distribución de contenido (CDN) de. Esto se realiza aislando las solicitudes que devuelven el HTML `(text/html)` o JSON `(application /Json)` contenido de la CDN y en función de varias reglas de inclusión y exclusión detalladas a continuación. AEM Una solicitud de contenido se produce de forma independiente del contenido devuelto que se sirve desde las cachés de CDN o del contenido que regresa al origen de CDN (Dispatchers).

El servicio Real User Monitoring , la colección del lado del cliente, ofrece una reflexión más precisa de las interacciones del usuario, lo que garantiza una medida fiable de la participación en el sitio web. Esto proporciona a los clientes una información avanzada sobre el tráfico y el rendimiento de sus páginas. Aunque esto resulta beneficioso para ambos clientes, que utilizan la CDN administrada por Adobe o una CDN administrada que no es por Adobe. Además, ahora se pueden habilitar los informes automáticos de tráfico para los clientes que utilicen una CDN administrada que no sea de Adobe, lo que elimina la necesidad de compartir cualquier informe de tráfico con Adobe.

AEM Para los clientes que aportan su propia CDN además de las as a Cloud Service, los informes del lado del servidor resultarán en números que no se pueden usar para comparar con las solicitudes de contenido con licencia. El cliente tendrá que medir estos números en el extremo de la CDN externa. Para estos clientes, los informes del lado del cliente y el rendimiento asociado, la variable [Adobe RUM Data Service](#real-user-monitoring-for-aem-as-a-cloud-service) es la opción recomendada por el Adobe. Consulte la [notas de la versión](/help/release-notes/release-notes-cloud/release-notes-current.md#sites-early-adopter) para obtener información sobre cómo realizar la inclusión.

## Colección del lado del servidor {#serverside-collection}

Existen reglas para excluir bots conocidos, incluidos servicios bien conocidos que visitan el sitio regularmente para actualizar su índice de búsqueda o servicio.

### Variaciones de solicitudes de contenido de Cloud Service {#content-requests-variances}

Las solicitudes de contenido pueden tener variaciones con las herramientas de informes de Analytics de una organización, como se resume en la siguiente tabla. En general, *no* utilice herramientas de analytics que recopilan datos mediante instrumentación del lado del cliente para informar sobre el número de solicitudes de contenido para un sitio determinado, simplemente porque a menudo dependen del consentimiento del usuario para activarse, por lo tanto se pierden una fracción significativa del tráfico. AEM Las herramientas de Analytics que recopilan datos del lado del servidor en archivos de registro o los informes de CDN para clientes que agregan su propia CDN además de la as a Cloud Service, proporcionarán mejores recuentos de datos. Para informar sobre Vistas de página y su rendimiento asociado, el servicio de datos de Adobe RUM es la opción recomendada por el Adobe.

| Motivo de la variación | Explicación |
|---|---|
| Consentimiento del usuario final | Las herramientas de Analytics que dependen de la instrumentación del lado del cliente suelen depender del consentimiento del usuario para activarse. Esto podría representar la mayoría del tráfico que no se rastrea. Para los clientes que deseen medir las solicitudes de contenido por su cuenta, se recomienda confiar en las herramientas de análisis que recopilan informes del lado del servidor o de CDN. |
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

### Tipos de solicitudes de contenido incluidas {#included-content-requests}

| Tipo de solicitud | Solicitud de contenido | Descripción |
| --- | --- | --- |
| Código HTTP 100-299 | Incluido | Son solicitudes regulares que entregan todo el contenido o parte del mismo. |
| Bibliotecas HTTP para automatización | Incluido | Ejemplos:<br>· Amazon CloudFront<br>· Cliente Http De Apache<br>· Cliente Http Asincrónico<br>· Axios<br>· Azureus<br>· Curl<br>· Recuperación del nodo de GitHub<br>· Guzzle<br>· Go-http-client<br>· Cromo sin encabezado<br>· Cliente Java™<br>· Jersey<br>· Oembed del nodo<br>· okhttp<br>· Solicitudes de Python<br>· Reactor Netty<br>· Wget<br>· WinHTTP |
| Herramientas de monitorización y comprobación de estado | Incluido | El cliente las configura para monitorizar un determinado aspecto del sitio. Por ejemplo, disponibilidad o rendimiento del usuario en el mundo real. Uso `/system/probes/health` y no las páginas del HTML real del sitio.<br>Ejemplos:<br>· Amazon-Route53-Health-Check-Service<br>· EyeMonIT_bot_version_0.1_[(https://www.eyemon.it/)](https://www.eyemon.it/)<br>· Investis-Site24x7<br>· Mozilla/5.0+(compatible; UptimeRobot/2.0; [https://uptimerobot.com/](https://uptimerobot.com/))<br>· ThousandEyes-Dragonfly-x1<br>· OmtrBot/1.0<br>· WebMon/2.0.0 |
| `<link rel="prefetch">` solicitudes | Incluido | Para aumentar la velocidad de carga de la página siguiente, los clientes pueden hacer que el explorador cargue un conjunto de páginas antes de que el usuario haga clic en el vínculo, por lo que ya están en la caché. *Mente: Esto está aumentando significativamente el tráfico*: en función de cuántas de estas páginas se hayan recuperado previamente. |
| Tráfico que bloquea los informes de Adobe Analytics o Google Analytics | Incluido | Es más común que los visitantes de los sitios tengan instalado software de privacidad (bloqueadores de anuncios, etc.) que afecta a la precisión de los Google Analytics o Adobe Analytics. AEM El recuento as a Cloud Service de solicitudes en el primer punto de entrada en la infraestructura operada por el Adobe y no en el lado del cliente. |

Consulte también [Tablero de licencias](/help/implementing/cloud-manager/license-dashboard.md).

### Tipos de solicitudes de contenido excluido {#excluded-content-request}

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

## Colección del lado cliente {#cliendside-collection}

### AEM Servicio de Monitorización de Usuarios Reales para el uso de la as a Cloud Service {#real-user-monitoring-service-for-aem-as-a-cloud-service}

>[!INFO]
>
>Esta función solo está disponible para los primeros programas de usuarios que la adoptaron.
>Debe utilizar la versión de AEM Cloud Service. **2023.11.14227** y superiores para habilitar el servicio de datos de RUM.

### Información general {#overview}

El servicio Real User Monitoring es un tipo de tecnología de monitorización del rendimiento que captura y analiza las experiencias de usuario digital de un sitio web o aplicación en tiempo real. Proporciona visibilidad del rendimiento en tiempo real de una aplicación web y proporciona una perspectiva precisa de la experiencia del usuario final.

El servicio de monitorización de usuarios reales proporciona un conocimiento profundo de las métricas de rendimiento clave desde el inicio de la URL hasta que la solicitud se devuelve al explorador, lo que ayuda a los desarrolladores a mejorar la aplicación para que sea fácil de usar para los usuarios finales.

### ¿Quién puede beneficiarse del servicio de monitorización de usuarios reales? {#who-can-benefit-from-rum-service}

El servicio de datos de RUM es beneficioso para todos los clientes, ya sea mediante Adobe o su propia CDN. Ofrece una reflexión más precisa de las interacciones del usuario, lo que garantiza una medida fiable de la participación en el sitio web al reflejar el número de vistas de página en el lado del cliente.

En particular, para los usuarios de CDN de Adobe, rastrea con precisión las interacciones del usuario para una comparación directa de las vistas de página del lado del cliente con los registros de CDN del lado del servidor.

Para los clientes que utilizan su propia CDN, pueden beneficiarse de la creación de informes de tráfico simplificados, ya que el Adobe ahora integra directamente estas vistas de página, lo que elimina la necesidad de informes independientes.

Además, todos los clientes obtienen perspectivas profundas del rendimiento de la página para optimizar sus experiencias digitales de forma eficaz.

### Comprender el funcionamiento del servicio de monitorización de usuarios reales {#understand-how-the-rum-service-works}

Adobe Experience Manager utiliza Real User Monitoring (RUM) para ayudar a los clientes y al Adobe a comprender cómo interactúan los visitantes con los sitios con tecnología de Adobe Experience Manager, diagnosticar problemas de rendimiento y medir la efectividad de los experimentos. RUM preserva la privacidad de los visitantes a través del muestreo (solo se supervisará una pequeña parte de todas las vistas de página) y la exclusión prudente de toda la información de identificación personal (PII).

### Servicio de monitorización de usuarios reales y privacidad {#rum-service-and-privacy}

El servicio de monitorización de usuarios reales de Adobe Experience Manager está diseñado para preservar la privacidad del visitante y minimizar la recopilación de datos. Como visitante, esto significa que el sitio que está visitando no recopilará información personal ni se pondrá a disposición del Adobe.

Como operador de sitio, esto significa que no se requiere ninguna opción de inclusión adicional para habilitar la monitorización a través de esta función. Por lo tanto, no habrá ninguna ventana emergente adicional que los usuarios finales acepten para habilitar la monitorización RUM.

### Muestreo de datos del servicio de monitorización del usuario real {#rum-service-data-sampling}

Las soluciones tradicionales de análisis web intentan recopilar datos de cada visitante. El servicio de Monitorización de usuarios reales de Adobe Experience Manager solo captura información de una pequeña fracción de las vistas de página. Los datos del servicio de monitorización de usuarios reales están pensados para muestrearse y convertirse en anónimos, en lugar de ser un sustituto del análisis. De forma predeterminada, las páginas tendrán una proporción de muestreo de 1:100. Los operadores del sitio no pueden configurar este número para aumentar o disminuir la tasa de muestreo a día de hoy. Para calcular el tráfico total con precisión, por cada 100 vistas de página, recopilamos datos detallados de una, lo que le proporciona una aproximación fiable del tráfico general&quot;.

A medida que se decide si los datos se recopilarán en función de la vista de página por vista de página, resulta prácticamente imposible rastrear las interacciones en varias páginas. RUM no tiene concepto de visitas, visitantes o sesiones, solo de vistas de página. Esto es por diseño.

### Qué datos se recopilan {#what-data-is-being-collected}

El servicio de Monitoreo de Usuario Real está diseñado para evitar la recopilación de información personal. A continuación, se enumera el conjunto completo de información que puede recopilar el servicio de monitorización de usuarios reales de Adobe Experience Manager:

* El nombre de host del sitio que se está visitando, por ejemplo: `experienceleague.adobe.com`
* El tipo de agente de usuario general que se utiliza para mostrar la página, como: escritorio o móvil
* El momento de la recopilación de datos, como por ejemplo: `2021-06-26 06:00:02.596000 UTC (in order to preserve privacy, we round all minutes to the previous hour, so that only seconds and milliseconds are tracked)`
* La dirección URL de la página que se está visitando, por ejemplo: `https://experienceleague.adobe.com/docs`
* La URL del referente (la URL de la página que está vinculada a la página actual, si el usuario ha seguido un vínculo)
* ID de la vista de página generado aleatoriamente, con un formato similar al siguiente: `2Ac6`
* El peso o la inversa de la velocidad de muestreo, como: `100`. Esto significa que solo se registrará una de cada cien vistas de página
* El punto de comprobación o el nombre de un evento concreto en la secuencia de carga de la página o de interacción con él como visitante
* El origen o identificador del elemento DOM con el que interactúa el usuario para el punto de comprobación mencionado anteriormente. Por ejemplo, podría ser una imagen
* El objetivo o vínculo a una página o recurso externo con el que el usuario interactúa para el punto de comprobación mencionado anteriormente. Por ejemplo: `https://blog.adobe.com/jp/publish/2022/06/29/media_162fb947c7219d0537cce36adf22315d64fb86e94.png`
* Las métricas de rendimiento de elementos vitales de la web (CWV) principales, la pintura de contenido más grande (LCP), el primer retraso de entrada (FID) y el cambio de diseño acumulativo (CLS), que describen la calidad de experiencia del visitante.

### Configuración del Servicio de Control de Usuarios Reales {#how-to-set-up-the-rum-service}

* Si desea formar parte de nuestro programa de adopción anticipada, envíe un correo electrónico a `aemcs-rum-adopter@adobe.com`, junto con su nombre de dominio para el entorno de producción, ensayo y desarrollo desde su dirección de correo electrónico asociada a su Adobe ID. El equipo de productos de Adobe habilitará entonces el servicio de datos RUM (Monitorización del usuario real) para usted.
* Una vez finalizado, el equipo de productos de Adobe creará un canal de colaboración con el cliente.
* El equipo de productos de Adobe se pondrá en contacto con usted para proporcionarle la clave de dominio y la URL del panel de datos, donde podrá ver las vistas de páginas y [Elementos vitales de la web (CWV)](https://web.dev/vitals/) métricas recopiladas por la recopilación del servicio de control de usuarios reales del lado del cliente.
* A continuación, se le guiará sobre cómo utilizar la clave de dominio para acceder a la URL del panel de datos y ver las métricas.

### Uso de los datos del servicio de monitorización de usuarios reales {#how-rum-service-data-is-being-used}

Los datos de RUM son beneficiosos para los siguientes propósitos:

* Para identificar y corregir los cuellos de botella de rendimiento de las ubicaciones de los clientes
* Informes de tráfico automáticos y optimizados que incluyen Vistas de página para clientes que utilizan su propia CDN, lo que significa que no tienen que compartir ningún informe de tráfico con Adobe.
* Comprender cómo Adobe Experience Manager interactúa con otros scripts (como análisis, segmentación o bibliotecas externas) en la misma página para aumentar la compatibilidad.

### Limitaciones y comprensión de la variación en las vistas de página y las métricas de rendimiento {#limitations-and-understanding-variance-in-page-views-and-performance-metrics}

A medida que analiza estos datos, es posible que haya variaciones en las vistas de página y otras métricas de rendimiento notificadas por Real User Monitoring (RUM). Estas variaciones pueden atribuirse a varios factores inherentes a la monitorización en tiempo real del lado del cliente. Estas son las consideraciones clave que los clientes deben tener en cuenta al interpretar sus datos de RUM:

1. **Bloqueadores de rastreadores**

   * Los usuarios finales que utilizan bloqueadores de rastreadores o extensiones de privacidad pueden impedir la recopilación de datos del servicio de Monitorización de usuarios reales, ya que estas herramientas restringen la ejecución de los scripts de seguimiento. Esta restricción puede provocar que no se informe lo suficiente sobre las vistas de página y las interacciones del usuario, lo que crea una discrepancia entre la actividad real del sitio y los datos capturados por RUM.

1. **Limitaciones al capturar llamadas API/JSON**

   * El servicio de datos de RUM se centra en la experiencia del lado del cliente y no captura las llamadas API back-end o JSON en este momento. La exclusión de estas llamadas de los datos del servicio de Supervisión de usuarios reales creará variaciones a partir de las solicitudes de contenido medidas por CDN Analytics.

### Preguntas más frecuentes {#faq}

1. **¿Cómo puedo configurar las rutas para incluir o excluir en la monitorización?**

   Los clientes podrán configurar rutas para incluir o excluir las direcciones URL para la monitorización estableciendo las variables de entorno dentro de la configuración en Cloud Manager mediante estas variables: `AEM_WEBVITALS_EXCLUDE` y `AEM_WEBVITALS_INCLUDE_PATHS`

   Tenga en cuenta que, de forma predeterminada, la configuración &quot;incluir&quot; está configurada para dirigirse a &quot;/content&quot;. Es importante recordar que las rutas que debe configurar aquí son rutas de contenido dentro del sistema, no las rutas URL que ve en su explorador. Esta distinción es clave para configurar y personalizar con precisión la configuración para satisfacer sus necesidades específicas.

1. **¿Adobe podría rastrear todas las vistas de página antes de que la interacción llegue a la CDN administrada por el cliente o en el momento en que la interacción llegue a la CDN administrada por el cliente?**

   Sí.

1. **¿Podrán los clientes integrar los scripts del servicio de datos RUM con sistemas de terceros como Dynatrace?**

   Sí.

1. **¿Se están recopilando las métricas de constantes web &quot;Interacción con la siguiente pintura&quot;, &quot;Tiempo hasta el primer byte&quot; y &quot;Primera pintura de contenido&quot;?**

   Se recopilan la interacción con la siguiente pintura (INP) y el tiempo hasta el primer byte (TTFB).  La primera pintura con contenido no se recopila en este momento.
