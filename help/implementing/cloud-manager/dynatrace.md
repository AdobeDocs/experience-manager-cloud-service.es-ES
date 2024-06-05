---
title: Dynatrace
description: Aprenda a utilizar Dynatrace AEM con el as a Cloud Service de la
exl-id: b58c8b82-a098-4d81-bc36-664e890c8f66
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 646ca4f4a441bf1565558002dcd6f96d3e228563
workflow-type: tm+mt
source-wordcount: '589'
ht-degree: 0%

---

# Dynatrace {#dynatrace}

El Adobe de proporciona la capacidad de utilizar Dynatrace AEM para monitorizar los problemas as a Cloud Service como parte de la implementación empresarial, identificar la causa de cualquier posible problema y tomar medidas para solucionarlos según sea necesario.

Con Dynatrace AEM, puede obtener una observabilidad perfecta para todas sus aplicaciones de la. Dynatrace AEM proporciona una visibilidad completa de la experiencia del usuario final al detectar automáticamente las aplicaciones de la y visualizar sus dependencias desde el sitio web al contenedor o al servicio en la nube. AEM Entrelazado con los seguimientos de extremo a extremo en todos los niveles y la Monitorización de usuarios reales, lleve sus experiencias basadas en contenido al siguiente nivel sin interrupciones ni puntos ciegos. Si surge alguna anomalía, Dynatrace la diagnostica en tiempo real con el motor de IA de Davis y localiza la causa raíz hasta el código dañado antes de que sus clientes se vean afectados, lo que minimiza el tiempo medio para la reparación.

Para obtener más información sobre Dynatrace, consulte la [Adobe Integración de AEM Cloud Service](https://www.dynatrace.com/hub/detail/adobe-experience-manager-1/).

![AEM métricas de rendimiento de autor y editor](/help/implementing/cloud-manager/assets/dynatrace-performance-metrics.png)

## Integración de Dynatrace AEM con el código as a Cloud Service {#integrating-dynatrace-with-aem-as-a-cloud-service}

Los clientes de Dynatrace AEM pueden monitorizar sus entornos de solicitando conectividad a través de un ticket de asistencia al cliente.

A continuación se describen los detalles necesarios para las solicitudes de conectividad:

| **Campo** | **Descripción** |
|---|---|
| [!DNL Dynatrace Environment URL] | La URL de entorno de Dynatrace.<br><br>Para los clientes de SaaS de Dynatrace, el formato es `https://<your-environment-id>.live.dynatrace.com`.<br><br>Para los clientes administrados de Dynatrace, el formato es `https://<your-managed-url>/e/<environmentId>` |
| [!DNL Dynatrace Environment ID] | Su ID de entorno de Dynatrace. Consulte lo siguiente [¿Cómo obtengo mis datos de conexión de Dynatrace?](#how-do-i-get-my-dynatrace-connection-details) para saber cómo conseguir esto. |
| [!DNL Dynatrace Environment Token] | El token de entorno de Dynatrace. Consulte lo siguiente [¿Cómo obtengo mis datos de conexión de Dynatrace?](#how-do-i-get-my-dynatrace-connection-details) para saber cómo conseguir esto.<br><br>Esto debe considerarse un secreto, por lo que debe seguir las prácticas de seguridad adecuadas. Por ejemplo, protéjalo con contraseña en un sitio web como **zerobin.net**, a la que puede hacer referencia el ticket de asistencia al cliente, junto con la contraseña. |
| [!DNL Dynatrace API access token] | El token de acceso de la API de su entorno de Dynatrace.  Consulte lo siguiente [Creación de un token de acceso a la API de Dynatrace](#create-dynatrace-access-token) para saber cómo crear esto.<br><br>Esto debe considerarse un secreto, por lo que debe seguir las prácticas de seguridad adecuadas. Por ejemplo, protéjalo con contraseña en un sitio web como **zerobin.net**, a la que puede hacer referencia el ticket de asistencia al cliente, junto con la contraseña.<br><br>Nota: Esto solo es necesario para Dynatrace Managed. |
| [!DNL Dynatrace ActiveGate Port] | Puerto de Dynatrace AEM ActiveGate al que se debe conectar la integración de la.<br><br>Nota: Esto solo es necesario para Dynatrace Managed. |
| [!DNL Dynatrace ActiveGate Network Zone] | Su [Zona de red de Dynatrace ActiveGate](https://docs.dynatrace.com/docs/manage/network-zones) AEM para dirigir los datos de monitorización de forma eficaz entre centros de datos y regiones de red.<br><br>Nota: La zona de red de Dynatrace ActiveGate es opcional. |
| [!DNL AEM Environment ID(s)] | AEM Los ID de entorno de la aplicación que Dynatrace va a monitorizar. |

>[!NOTE]
>
>Una vez que Dynatrace esté integrado, los datos ya no fluirán a otras herramientas de APM, como New Relic, si antes estaban habilitados.

## Preguntas más frecuentes {#faq}

### ¿Qué licencia necesito para la Monitorización de DynatraceAEM {#which-license-do-i-need-for-AEM-monitoring}

La monitorización de Dynatrace AEM requiere una licencia de Dynatrace. La licencia de Dynatrace AEM se basa en [monitorización de pila completa para contenedores de Kubernetes](https://docs.dynatrace.com/docs/shortlink/dps-hosts#gib-hour-calculation-for-containers-and-application-only-monitoring). AEM Se detectan automáticamente los tamaños de memoria de los contenedores de supervisados (servicios de autor y editor).

Las especificaciones de implementación de Adobe AEM por entorno de la son:

* Producción: En promedio, 4 contenedores, 16 GB de memoria cada uno
* No producción: En promedio, 4 contenedores, 8 GB de memoria cada uno

Para obtener más información sobre las licencias de Dynatrace, consulte la [Suscripción a Dynatrace Platform](https://docs.dynatrace.com/docs/shortlink/dynatrace-platform-subscription).

### ¿Cómo obtengo mis datos de conexión de Dynatrace? {#how-do-i-get-my-dynatrace-connection-details}

1. Ejecute la siguiente solicitud de API en su entorno de Dynatrace:

   ```
   curl -X GET "<environmentUrl>/api/v1/deployment/installer/agent/connectioninfo" -H "accept: application/json" -H "Authorization: Api-Token <accessToken>"
   ```


   Reemplazar `<environmentUrl>` con la URL de entorno de Dynatrace y `<accessToken>` con el token de acceso de API creado.

1. Copie el `<environmentId>` y `<environmentToken>` desde la carga útil de respuesta y almacénelas en un lugar seguro.

   ```
   {
      "tenantUUID": "<environmentId>",
      "tenantToken": "<environmentToken>",
      "communicationEndpoints": [...]
   }
   ```

### Creación de un token de acceso a la API de Dynatrace {#create-dynatrace-access-token}

1. Inicie sesión en su entorno de Dynatrace.
1. Ir a **[!DNL Access tokens]** y seleccione **[!DNL Generate new token]**.
1. Defina un [!DNL token name].
1. Establezca el ámbito del token en **[!DNL PaaS integration - Installer download]**.
1. Seleccionar **[!DNL Generate token]**.
1. Copie el token de acceso generado y guárdelo en un lugar seguro.





