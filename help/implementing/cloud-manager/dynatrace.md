---
title: Dynatrace
description: AEM Aprenda a utilizar Dynatrace con el as a Cloud Service
exl-id: b58c8b82-a098-4d81-bc36-664e890c8f66
source-git-commit: fec3aa6debec49014406ab241c3ce0338ec5a1d2
workflow-type: tm+mt
source-wordcount: '514'
ht-degree: 0%

---

# Dynatrace {#dynatrace}

Adobe AEM permite utilizar Dynatrace para monitorizar los problemas as a Cloud Service como parte de la implementación empresarial, identificar la causa de cualquier posible problema y tomar medidas para solucionarlos según sea necesario.

AEM Con Dynatrace, puede obtener una observabilidad perfecta para todas sus aplicaciones de la. AEM Dynatrace proporciona una visibilidad completa de la experiencia del usuario final al detectar automáticamente sus aplicaciones de y visualizar sus dependencias desde el sitio web al contenedor o al servicio en la nube. AEM Entrelazado con los seguimientos de extremo a extremo en todos los niveles y la Monitorización de usuarios reales, lleve sus experiencias basadas en contenido al siguiente nivel sin interrupciones ni puntos ciegos. Si surge alguna anomalía, Dynatrace la diagnostica en tiempo real con el motor de IA de Davis, y localiza la causa raíz hasta el código roto antes de que sus clientes se vean afectados, minimizando así el tiempo medio para la reparación.

Para obtener más información sobre Dynatrace, consulte la [Adobe Integración de AEM Cloud Service](https://www.dynatrace.com/hub/detail/adobe-experience-manager-1/).

![AEM métricas de rendimiento de autor y editor](/help/implementing/cloud-manager/assets/dynatrace-performance-metrics.png)

## AEM Integración de Dynatrace con el as a Cloud Service {#integrating-dynatrace-with-aem-as-a-cloud-service}

AEM Los clientes de Dynatrace pueden monitorizar sus entornos de solicitando conectividad a través de un ticket de asistencia al cliente.

A continuación se describen los detalles necesarios para las solicitudes de conectividad:

| **Campo** | **Descripción** |
|---|---|
| [!DNL Dynatrace Environment URL] | La URL de su entorno de Dynatrace.<br><br>Para los clientes de Dynatrace SaaS, el formato es `https://<your-environment-id>.live.dynatrace.com`.<br><br>Para los clientes de Dynatrace Managed, el formato es `https://<your-managed-url>/e/<environmentId>` |
| [!DNL Dynatrace Environment ID] | Su ID de entorno de Dynatrace. Consulte lo siguiente [Obtener información del entorno de Dynatrace](#get-dynatrace-env-info) para saber cómo conseguir esto. |
| [!DNL Dynatrace Environment Token] | El token de entorno de Dynatrace. Consulte lo siguiente [Obtener información del entorno de Dynatrace](#get-dynatrace-env-info) para saber cómo conseguir esto.<br><br>Esto debe considerarse un secreto, por lo que debe seguir las prácticas de seguridad adecuadas. Por ejemplo, protéjalo con contraseña en un sitio web como **zerobin.net**, a la que puede hacer referencia el ticket de asistencia al cliente, junto con la contraseña. |
| [!DNL Dynatrace API access token] | El token de acceso API del entorno de Dynatrace.  Consulte lo siguiente [Creación de un token de acceso de API de Dynatrace](#create-dynatrace-access-token) para saber cómo crear esto.<br><br>Esto debe considerarse un secreto, por lo que debe seguir las prácticas de seguridad adecuadas. Por ejemplo, protéjalo con contraseña en un sitio web como **zerobin.net**, a la que puede hacer referencia el ticket de asistencia al cliente, junto con la contraseña.<br><br>Nota: Esto solo es necesario para Dynatrace Managed. |
| [!DNL Dynatrace ActiveGate Port] | AEM El puerto ActiveGate de Dynatrace al que debe conectarse la integración de la.<br><br>Nota: Esto solo es necesario para Dynatrace Managed. |
| [!DNL Dynatrace ActiveGate Network Zone] | Su [Zona de red de Dynatrace ActiveGate](https://docs.dynatrace.com/docs/manage/network-zones) AEM para dirigir los datos de monitorización de forma eficaz entre centros de datos y regiones de red.<br><br>Nota: La zona de red ActiveGate de Dynatrace es opcional. |
| [!DNL AEM Environment ID(s)] | AEM Los ID de entorno de la aplicación que Dynatrace va a monitorizar. |

>[!NOTE]
>
>Una vez que Dynatrace esté integrado, los datos ya no fluirán a otras herramientas de APM como New Relic, si antes estaba habilitado.


## Creación de un token de acceso de API de Dynatrace {#create-dynatrace-access-token}

1. Inicie sesión en su entorno de Dynatrace.
1. En el [!DNL Dynatrace] , vaya a [!DNL Manage] > [!DNL Access tokens].
1. Seleccionar [!DNL Generate new token].
1. Defina un [!DNL token name].

1. Opcional: establezca un [!DNL expiration date]. Asegúrese de generar un nuevo token antes de que caduque.
1. Configure las variables [!DNL token scope] hasta [!DNL PaaS integration - Installer download]
1. Seleccionar [!DNL Generate token].
1. Copie el token de acceso generado y guárdelo en un lugar seguro.


## Obtener información del entorno de Dynatrace {#get-dynatrace-env-info}

1. Ejecute la siguiente solicitud de API en su entorno de Dynatrace:

`curl -X GET "<environmentUrl>/api/v1/deployment/installer/agent/connectioninfo" -H "accept: application/json" -H "Authorization: Api-Token <accessToken>"`

Reemplazar \&lt;environmenturl> con la URL del entorno de Dynatrace y \&lt;accesstoken> con el token de acceso de API creado.

1. Copie el \&lt;environmentid> y \&lt;environmenttoken> desde la carga útil de respuesta y almacénelas en un lugar seguro.

```
{
   "tenantUUID": "<environmentId>",
   "tenantToken": "<environmentToken>",
   "communicationEndpoints": [
   ... 
   ],
   "formattedCommunicationEndpoints": "<endpoints>" 
}
```


