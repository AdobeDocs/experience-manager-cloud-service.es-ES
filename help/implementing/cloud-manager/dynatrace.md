---
title: Dynatrace
description: Aprenda a utilizar Dynatrace con AEM as a Cloud Service
exl-id: b58c8b82-a098-4d81-bc36-664e890c8f66
solution: Experience Manager
feature: Log Files, Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '577'
ht-degree: 0%

---

# Dynatrace {#dynatrace}

Adobe permite utilizar Dynatrace para supervisar AEM as a Cloud Service como parte de la implementación empresarial, identificar la causa de cualquier problema potencial y tomar medidas para solucionarlo según sea necesario.

Con Dynatrace, puede obtener una observabilidad perfecta para todas sus aplicaciones de AEM. Dynatrace descubre sus aplicaciones AEM y muestra sus rutas, desde el sitio web hasta el contenedor o el servicio en la nube, para revelar la experiencia del usuario. Entrelazado con los seguimientos de extremo a extremo en cada nivel y la Monitorización de uso real, lleve sus experiencias basadas en contenido de AEM al siguiente nivel sin interrupciones ni puntos ciegos. Si surgen anomalías, Dynatrace las diagnostica en tiempo real, con el motor de IA de Davis. Localiza la causa raíz hasta el código dañado antes de que sus clientes se vean afectados, lo que minimiza el tiempo medio de reparación.

Para obtener más información sobre Dynatrace, consulte la [Integración de Adobe AEM Cloud Service](https://www.dynatrace.com/hub/detail/adobe-experience-manager-1/).

![Métricas de rendimiento de autor y editor de AEM](/help/implementing/cloud-manager/assets/dynatrace-performance-metrics.png)

## Integración de Dynatrace con AEM as a Cloud Service {#integrating-dynatrace-with-aem-as-a-cloud-service}

Los clientes de Dynatrace pueden monitorizar sus entornos de AEM solicitando conectividad a través de un ticket de asistencia al cliente.

A continuación se describen los detalles necesarios para las solicitudes de conectividad:

| **Campo** | **Descripción** |
|---|---|
| [!DNL Dynatrace Environment URL] | La URL de entorno de Dynatrace.<br><br>Para clientes de SaaS de Dynatrace, el formato es `https://<your-environment-id>.live.dynatrace.com`.<br><br>Para clientes administrados por Dynatrace, el formato es `https://<your-managed-url>/e/<environmentId>` |
| [!DNL Dynatrace Environment ID] | Su ID de entorno de Dynatrace. Ver [¿Cómo obtengo mis detalles de conexión de Dynatrace?](#how-do-i-get-my-dynatrace-connection-details) para saber cómo obtenerlo. |
| [!DNL Dynatrace Environment Token] | El token de entorno de Dynatrace. Ver [¿Cómo obtengo mis detalles de conexión de Dynatrace?](#how-do-i-get-my-dynatrace-connection-details) para saber cómo obtenerlo.<br><br>Este token debe considerarse un secreto, por lo que debe seguir las prácticas de seguridad apropiadas. Por ejemplo, protéjalo con contraseña en un sitio web como **zerobin.net**, al que el ticket de asistencia al cliente puede hacer referencia, junto con la contraseña. |
| [!DNL Dynatrace API access token] | El token de acceso de la API de su entorno de Dynatrace. Consulte [Crear un token de acceso a la API de Dynatrace](#create-dynatrace-access-token) para saber cómo crearlo.<br><br>Este token debe considerarse un secreto, así que siga las prácticas de seguridad apropiadas. Por ejemplo, protéjalo con contraseña en un sitio web como **zerobin.net**, al que el ticket de asistencia al cliente puede hacer referencia, junto con la contraseña.<br> |
| [!DNL Dynatrace ActiveGate Port] | Puerto de Dynatrace ActiveGate al que se debe conectar la integración de AEM.<br><br>Este puerto solo es necesario para Dynatrace Managed. |
| [!DNL Dynatrace ActiveGate Network Zone] | Su [zona de red Dynatrace ActiveGate](https://docs.dynatrace.com/docs/manage/network-zones) para enrutar los datos de supervisión de AEM de forma eficaz entre los centros de datos y las regiones de red.<br><br>Nota: una zona de red de Dynatrace ActiveGate es opcional. |
| [!DNL AEM Environment IDs] | Los ID de entorno de AEM o los ID para que Dynatrace los supervise. |

>[!NOTE]
>
>Una vez que Dynatrace está integrado, los datos ya no fluyen a otras herramientas de APM como New Relic, si anteriormente estaban habilitados.

## Preguntas frecuentes {#faq}

### ¿Qué licencia necesito para la Monitorización de Dynatrace AEM? {#which-license-do-i-need-for-AEM-monitoring}

La monitorización de Dynatrace AEM requiere una licencia de Dynatrace. Las licencias de Dynatrace AEM se basan en la [supervisión de pila completa de los contenedores de Kubernetes](https://docs.dynatrace.com/docs/shortlink/dps-hosts#gib-hour-calculation-for-containers-and-application-only-monitoring). Los tamaños de memoria de los contenedores de AEM supervisados (servicios de autor y editor) se detectan automáticamente.

Las especificaciones de implementación de Adobe para el entorno de AEM son:

* Producción: En promedio, 4 contenedores, 16 GB de memoria cada uno
* No producción: En promedio, 4 contenedores, 8 GB de memoria cada uno

Para obtener más información acerca de las licencias de Dynatrace, consulte [Suscripción a la plataforma Dynatrace](https://docs.dynatrace.com/docs/shortlink/dynatrace-platform-subscription).

### ¿Cómo obtengo mis datos de conexión de Dynatrace? {#how-do-i-get-my-dynatrace-connection-details}

1. Ejecute la siguiente solicitud de API en su entorno de Dynatrace:

   ```
   curl -X GET "<environmentUrl>/api/v1/deployment/installer/agent/connectioninfo" -H "accept: application/json" -H "Authorization: Api-Token <accessToken>"
   ```


   Reemplace `<environmentUrl>` por su URL de entorno de Dynatrace y `<accessToken>` por su token de acceso a API creado.

1. Copie `<environmentId>` y `<environmentToken>` de la carga de respuesta y almacénelos en un lugar seguro.

   ```
   {
      "tenantUUID": "<environmentId>",
      "tenantToken": "<environmentToken>",
      "communicationEndpoints": [...]
   }
   ```

### Creación de un token de acceso a la API de Dynatrace {#create-dynatrace-access-token}

1. Inicie sesión en su entorno de Dynatrace.
1. Vaya a **[!DNL Access tokens]** y haga clic en la opción **[!DNL Generate new token]**.
1. Definir un [!DNL token name].
1. Establezca el ámbito del token en **[!DNL PaaS integration - Installer download]**.
1. Seleccione **[!DNL Generate token]**.
1. Copie el token de acceso generado y guárdelo en un lugar seguro.





