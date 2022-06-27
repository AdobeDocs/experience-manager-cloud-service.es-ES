---
title: Panel de licencias
description: Cloud Manager proporciona un tablero para facilitar la visualización de las autorizaciones de productos de AEMaaCS disponibles para su organización o inquilino.
exl-id: bf0f54a9-fe86-4bfb-9fa6-03cf0fd5f404
source-git-commit: 5bf65238ce4d1f619507d9a5f8b7574e58352d51
workflow-type: tm+mt
source-wordcount: '782'
ht-degree: 1%

---

# Panel de licencias {#license-dashboard}

Cloud Manager proporciona un tablero para facilitar la visualización de las autorizaciones de productos de AEMaaCS disponibles para su organización o inquilino.

## Información general {#overview}

El panel de licencias de Cloud Manager proporciona acceso fácil a la siguiente información:

1. Derechos de solución disponibles para usted en todos sus programas, incluidos los que se usan y los que están disponibles
1. Métricas de consumo de solicitud de contenido de tendencias por mes para la solución Sitios

## Uso del panel de licencias {#using-dashboard}

Para acceder al panel de licencias, siga estos pasos.

>[!NOTE]
>
>Un usuario en **Propietario empresarial** debe iniciar sesión para ver el panel de licencias.

1. Inicie sesión en Cloud Manager en [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) y seleccione la organización adecuada.

1. En la página de información general de productos, cambie a la **Licencia** pestaña .

![Panel de licencias](assets/license-dashboard.png)

El tablero se divide en tres secciones que le muestran:

* **Soluciones** - Esta sección resume las soluciones con licencia, como Sitios o Recursos.
* **Complementos** - Esta sección resume qué complementos de las soluciones con licencia tiene disponibles.
* **Entornos de espacio aislado y desarrollo** - Esta sección resume qué entornos tiene disponibles.

Cada sección resume lo que está disponible y cómo se utiliza actualmente, si es que lo está. Actualmente solo se muestran las soluciones de Sites aunque existan otras soluciones en el inquilino.

* La variable **Estado** muestra el número de derechos no utilizados frente al total disponible para el inquilino.
* La variable **Configurado en** indica los programas en los que se ha aplicado la asignación de derechos de solución.
   * Una asignación de derechos se considera utilizada solo cuando se ha creado un entorno de producción o si ya existe, si se ha ejecutado una canalización de actualización en él.
* La variable **Uso** muestra las solicitudes de contenido consumidas en los últimos 12 meses como un gráfico cuando se hace clic en ellas.

>[!TIP]
>
>Consulte [Información general del Admin Console](https://helpx.adobe.com/es/enterprise/using/admin-console.html) para aprender a administrar las autorizaciones de Adobe en toda la organización desde el Admin Console.

## Preguntas frecuentes  {#faq}

### ¿Qué es una solicitud de contenido? {#what-is-a-content-request}

Una solicitud de contenido es una solicitud que llega a AEM Sites o a cualquier sistema de almacenamiento en caché proporcionado por el cliente, como una red de entrega de contenido, para entregar contenido o datos en formato de HTML como una vista de página o en formato JSON como una llamada de API.

Se cuenta una solicitud de contenido por cada vista de página o por cada cinco llamadas a la API, medidas a la entrada del primer sistema de almacenamiento en caché que recibe una solicitud de contenido. Las solicitudes de contenido se cuentan únicamente en los entornos de producción.

Las solicitudes de contenido excluyen las solicitudes o actividades iniciadas por o en nombre del Adobe con el único propósito de proporcionar productos y servicios. También se excluye el tráfico de agentes de usuario identificados por Adobe de bots, rastreadores y arañas de Web relacionadas con motores de búsqueda y servicios de medios sociales comunes.

### ¿Cómo mide Adobe Experience Manager las solicitudes de contenido? {#how-are-content-requests-measured}

Las solicitudes de contenido se rastrean en los servidores Edge de AEM as a Cloud Service. El tráfico de origen no se cuenta para las solicitudes de contenido. La CDN integrada en AEM as a Cloud Service rastrea solicitudes de HTML y JSON válidas.

AEM también dispone de reglas para excluir bots conocidos, incluidos servicios bien conocidos que visitan el sitio regularmente para actualizar su índice de búsqueda o servicio.

La siguiente es una lista no exhaustiva de ejemplos de servicios bien conocidos excluidos.

* AddSearchBot
* AhrefsBot
* Applebot
* Pregunte a Jeeves la araña corporativa
* Bingbot
* BingPreview
* BLEXBot
* IntegradoCon
* Bytespider
* CrawlerKengo
* Visita externa de Facebook
* Google AdsBot
* Google AdsBot Mobile

### ¿Por qué en mi informe de Analytics se muestran resultados diferentes a los de las solicitudes de contenido de AEM? {#why-are-reports-different}

Las solicitudes de contenido tendrán variaciones con las herramientas de informes de Analytics de una organización, como se resume en esta tabla.

| Motivo De La Varianza | Explicación |
|---|---|
| Etiquetado | Todas las páginas que se rastrean como solicitudes de contenido AEM pueden o no estar etiquetadas con el seguimiento de Analytics.<br>La herramienta Analytics de una organización no etiquetará todas las llamadas de API rastreadas como solicitudes de contenido AEM.<br>Las páginas o llamadas a la API pueden etiquetarse para realizar el seguimiento de acciones en lugar de vistas. |
| Reglas de Tag Management | La configuración de reglas de Tag Management puede dar como resultado una variedad de configuraciones de recopilación de datos en una página, lo que da como resultado una combinación de discrepancias con el seguimiento de solicitudes de contenido. |
| Bots | Los bots desconocidos que no han sido identificados previamente y eliminados por AEM pueden causar discrepancias de seguimiento. |
| Grupos de informes | Las páginas que forman parte de la misma instancia de AEM y del mismo dominio pueden enviar datos a diferentes grupos de informes de Analytics. |
| Herramientas de seguridad y supervisión de terceros | Las herramientas de monitorización y análisis de seguridad pueden generar solicitudes de contenido para AEM que no se rastrean en informes de Analytics. |
| Solicitudes de recuperación previa | El uso de un servicio de recuperación previa para cargar previamente las páginas a fin de aumentar la velocidad puede provocar aumentos significativos en el tráfico de las solicitudes de contenido. |
| DDOS | Aunque el Adobe hace todo lo posible por detectar y filtrar automáticamente el tráfico de los ataques de DDOS, no hay garantías de que se detecten todos los posibles ataques de DDOS. |

### ¿Qué sucede si utilizo mi propia CDN? {#using-own-cdn}

El panel de solicitudes de contenido de Cloud Manager no mostrará el seguimiento de su propia CDN.
