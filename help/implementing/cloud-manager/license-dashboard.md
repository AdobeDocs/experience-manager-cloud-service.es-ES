---
title: Tablero de licencias
description: Cloud Manager proporciona un tablero para facilitar la visualización de las autorizaciones de productos de AEMaaCS disponibles para su organización o inquilino.
exl-id: bf0f54a9-fe86-4bfb-9fa6-03cf0fd5f404
source-git-commit: 1994b90e3876f03efa571a9ce65b9fb8b3c90ec4
workflow-type: ht
source-wordcount: '873'
ht-degree: 100%

---

# Tablero de licencias {#license-dashboard}

Cloud Manager proporciona un tablero para facilitar la visualización de las autorizaciones de productos de AEMaaCS disponibles para su organización o inquilino.

## Información general {#overview}

El panel de licencias de Cloud Manager proporciona un acceso fácil a la siguiente información:

1. Derechos de solución disponibles para usted en todos sus programas, incluidos los que se usan y los que están disponibles
1. Métricas de consumo de solicitud de contenido de tendencias por mes para la solución Sites

## Utilizar el tablero de licencias {#using-dashboard}

Para acceder al tablero de licencias, siga estos pasos.

>[!NOTE]
>
>Un usuario con el rol de **Propietario del negocio** debe iniciar sesión para ver el tablero de licencias.

1. Inicie sesión en Cloud Manager en [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) y seleccione la organización adecuada.

1. En la página de información general de productos, cambie a la pestaña **Licencia**.

![Tablero de licencias](assets/license-dashboard.png)

El tablero se divide en tres secciones que le muestran lo siguiente:

* **Soluciones**: Esta sección resume las soluciones para las que tiene licencia, como Sites o Assets.
* **Complementos**: Esta sección resume qué complementos de las soluciones con licencia tiene disponibles.
* **Entornos de zona protegida y desarrollo**: Esta sección resume qué entornos tiene disponibles.

Cada sección resume lo que está disponible y cómo se utiliza actualmente, si es que lo está. Actualmente solo se muestran las soluciones de Sites, aunque existan otras soluciones en el inquilino.

* La columna **Estado** muestra el número de derechos no utilizados frente al total disponible para el inquilino.
* La columna **Configurado en** indica los programas en los que se ha aplicado la asignación de derechos de solución.
   * Una asignación de derechos se considera utilizada solo cuando se ha creado un entorno de producción o si ya existe, si se ha ejecutado una canalización de actualización en él.
* La columna **Uso** muestra un gráfico de las solicitudes de contenido consumidas en los últimos 12 meses cuando se hace clic sobre ellas.

>[!TIP]
>
>Consulte [Información general de Admin Console](https://helpx.adobe.com/es/enterprise/using/admin-console.html) para aprender a administrar los derechos de Adobe en toda la organización desde Admin Console.

## Preguntas frecuentes  {#faq}

### ¿Qué es una solicitud de contenido? {#what-is-a-content-request}

Una solicitud de contenido es una solicitud que llega a AEM Sites o a cualquier sistema de almacenamiento en caché proporcionado por el cliente, como una red de distribución de contenido, para entregar contenido o datos en formato HTML, como una vista de página, o en formato JSON, como una llamada de la API.

Se cuenta una solicitud de contenido por cada vista de página o por cada cinco llamadas a la API, se miden a la entrada del primer sistema de almacenamiento en la memoria caché que recibe una solicitud de contenido. Las solicitudes de contenido se cuentan únicamente en los entornos de producción.

Las solicitudes de contenido excluyen las solicitudes o actividades iniciadas por o en nombre de Adobe con el único propósito de proporcionar productos y servicios. También se excluye el tráfico de agentes de usuario identificados por Adobe de bots, rastreadores y arañas relacionadas con motores de búsqueda y servicios de medios sociales comunes.

### ¿Cómo mide Adobe Experience Manager las solicitudes de contenido? {#how-are-content-requests-measured}

Las solicitudes de contenido se rastrean en los servidores Edge de AEM as a Cloud Service. El tráfico de origen no se cuenta para las solicitudes de contenido. La red de distribución de contenido (CDN) integrada en AEM as a Cloud Service rastrea solicitudes de HTML y JSON válidas.

AEM también dispone de reglas para excluir bots conocidos, incluidos servicios bien conocidos que visitan el sitio regularmente para actualizar su índice de búsqueda o servicio.

### ¿Por qué en mi informe de Analytics se muestran resultados diferentes a los de las solicitudes de contenido de AEM? {#why-are-reports-different}

Las solicitudes de contenido tendrán variaciones con las herramientas de informes de Analytics de una organización, como se resume en esta tabla.

| Motivo de la variación | Explicación |
|---|---|
| Etiquetado | Todas las páginas que se rastrean como solicitudes de contenido de AEM pueden o no estar etiquetadas con el seguimiento de Analytics. La herramienta Analytics de una organización no etiquetará todas las llamadas de la API que se rastreen como solicitudes de contenido de AEM.<br>Las páginas o llamadas a la API pueden etiquetarse para rastrear acciones o solo vistas de página únicas en lugar de todas las vistas. |
| Reglas de administración de etiquetas | La configuración de reglas de administración de etiquetas puede dar como resultado varias configuraciones de recopilación de datos en una página, lo que da como resultado una combinación de discrepancias con el seguimiento de solicitudes de contenido. |
| Bots | Los bots desconocidos que no han sido identificados previamente y eliminados por AEM pueden causar discrepancias de seguimiento. |
| Grupos de informes | Las páginas que forman parte de la misma instancia de AEM y del mismo dominio pueden enviar datos a diferentes grupos de informes de Analytics. |
| Herramientas de seguridad y monitorización de terceros | Las herramientas de monitorización y análisis de seguridad pueden generar solicitudes de contenido para AEM que no se rastrean en informes de Analytics. |
| Solicitudes de recuperación previa | El uso de un servicio de recuperación previa para cargar previamente las páginas a fin de aumentar la velocidad puede provocar aumentos significativos en el tráfico de las solicitudes de contenido. |
| DDOS | Mientras que Adobe hace todo lo posible por detectar y filtrar automáticamente el tráfico de los ataques de DDOS, no hay garantías de que se detecten todos los ataques de DDOS posibles |
| Bloqueadores de tráfico | El uso de un bloqueador de tráfico en un explorador puede excluir el seguimiento de algunas solicitudes. |
| Firewalls | Los firewalls pueden bloquear el seguimiento de Analytics. Es más frecuente con los firewalls corporativos. |

### ¿Qué sucede si quisiera obtener más información sobre mi volumen de solicitudes de contenido? {#current-request-volumes}

Si desea obtener información adicional sobre el volumen de solicitud de contenido que se muestra en el Tablero de licencias, su equipo de Adobe puede proporcionarle un informe que muestre los controladores de mayor volumen de las solicitudes de contenido. Póngase en contacto con el equipo de Adobe o con el Servicio de atención al cliente de Adobe para solicitar un informe de uso superior.

### ¿Qué sucede si utilizo mi propia CDN? {#using-own-cdn}

El Tablero de licencias solo mostrará los datos rastreados por la CDN de Cloud Service.  Si opta por traer su propia CDN (BYOCDN), informará de su volumen de solicitud de contenido a Adobe anualmente, tal y como se indica en su contrato.
