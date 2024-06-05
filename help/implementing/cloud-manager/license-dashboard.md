---
title: Tablero de licencias
description: Cloud Manager proporciona un tablero para facilitar la visualización de las autorizaciones de productos de AEMaaCS disponibles para su organización o inquilino.
exl-id: bf0f54a9-fe86-4bfb-9fa6-03cf0fd5f404
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 646ca4f4a441bf1565558002dcd6f96d3e228563
workflow-type: tm+mt
source-wordcount: '661'
ht-degree: 58%

---

# Tablero de licencias {#license-dashboard}

Cloud Manager proporciona un tablero para facilitar la visualización de las autorizaciones de productos de AEMaaCS disponibles para su organización o inquilino.

## Información general {#overview}

El panel de licencias de Cloud Manager proporciona un acceso fácil a la siguiente información:

1. Los derechos de solución están disponibles para usted en todos sus programas, incluidos los que se utilizan y los que están disponibles
1. Métricas de consumo de solicitud de contenido de tendencias por mes para la solución Sites

## Utilizar el tablero de licencias {#using-dashboard}

Para acceder al tablero de licencias, siga estos pasos.

>[!NOTE]
>
>Un usuario en la **Propietario del negocio** La función debe haber iniciado sesión para ver el Tablero de licencias.

1. Inicie sesión en Cloud Manager en [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) y seleccione la organización adecuada.

1. En el **[Mis programas](/help/implementing/cloud-manager/navigation.md#my-programs)** consola, cambie a la **Licencia** pestaña.

![Tablero de licencias](assets/license-dashboard.png)

El tablero se divide en tres secciones que le muestran lo siguiente:

* **Soluciones**: Esta sección resume las soluciones para las que tiene licencia, como Sites o Assets.
* **Complementos**: Esta sección resume qué complementos de las soluciones con licencia tiene disponibles.
* **Entornos de zona protegida y desarrollo**: Esta sección resume qué entornos tiene disponibles.

Cada sección resume lo que está disponible y cómo se utiliza, si es que lo está. Actualmente solo se muestran las soluciones de Sites, aunque existan otras soluciones en el inquilino.

* El **Estado** La columna muestra el número de derechos no utilizados frente al total disponible para el inquilino.
* La columna **Configurado en** indica los programas en los que se ha aplicado la asignación de derechos de solución.
   * Una asignación de derechos se considera utilizada solo cuando se ha creado un entorno de producción o, si existe, si se ha ejecutado una canalización de actualización en él.
* La columna **Uso** muestra un gráfico de las solicitudes de contenido consumidas en los últimos 12 meses cuando se hace clic sobre ellas.

>[!TIP]
>
>Para obtener información sobre cómo administrar los derechos de Adobe en toda la organización desde Admin Console, consulte la [Introducción al Admin Console](https://helpx.adobe.com/es/enterprise/using/admin-console.html).

## Preguntas frecuentes  {#faq}

### ¿Qué es una solicitud de contenido? {#what-is-a-content-request}

Una solicitud de contenido es una solicitud que llega a AEM Sites o a cualquier sistema de almacenamiento en caché proporcionado por el cliente, como una red de entrega de contenido, para entregar contenido o datos en formato de HTML, como una vista de página, o en formato JSON, como una llamada de la API.

Se cuenta una solicitud de contenido por cada vista de página o por cada cinco llamadas a la API, se miden a la entrada del primer sistema de almacenamiento en la memoria caché que recibe una solicitud de contenido. Las solicitudes de contenido se cuentan únicamente en los entornos de producción.

Las solicitudes de contenido excluyen las solicitudes o actividades iniciadas por o en representación del Adobe con el único propósito de proporcionar productos y servicios. También se excluye el tráfico de agentes de usuario identificados por Adobe de bots, rastreadores y arañas relacionadas con motores de búsqueda y servicios de medios sociales comunes.

Consulte también [Explicación de las solicitudes de contenido de Cloud Service](/help/implementing/cloud-manager/content-requests.md).

### ¿Cómo mide Adobe Experience Manager las solicitudes de contenido? {#how-are-content-requests-measured}

Las solicitudes de contenido se rastrean en los servidores Edge de AEM as a Cloud Service. El tráfico de origen no se cuenta para las solicitudes de contenido. La red de distribución de contenido (CDN) integrada en AEM as a Cloud Service rastrea solicitudes de HTML y JSON válidas.

AEM también dispone de reglas para excluir bots conocidos, incluidos servicios bien conocidos que visitan el sitio regularmente para actualizar su índice de búsqueda o servicio.

Consulte también [Explicación de las solicitudes de contenido de Cloud Service](/help/implementing/cloud-manager/content-requests.md).

### ¿Por qué en mi informe de Analytics se muestran resultados diferentes a los de las solicitudes de contenido de AEM? {#why-are-reports-different}

Las solicitudes de contenido pueden tener variaciones con las herramientas de informes de Analytics de una organización. Para obtener más información, consulte [Explicación de las solicitudes de contenido de Cloud Service](/help/implementing/cloud-manager/content-requests.md).

### ¿Qué sucede si quisiera obtener más información sobre mi volumen de solicitudes de contenido? {#current-request-volumes}

Si desea obtener información adicional sobre el volumen de solicitud de contenido que se muestra en el Tablero de licencias, su equipo de Adobe puede proporcionarle un informe que muestre los controladores de mayor volumen de las solicitudes de contenido. Póngase en contacto con el equipo de Adobe o con Asistencia al cliente de Adobe para solicitar un informe de uso superior.

### ¿Qué sucede si utilizo mi propia CDN? {#using-own-cdn}

El Tablero de licencias solo muestra los datos rastreados por la CDN del Cloud Service. Si opta por traer su propia CDN (BYOCDN), informará de su volumen de solicitud de contenido a los Adobes anualmente, tal y como se indica en su contrato.
