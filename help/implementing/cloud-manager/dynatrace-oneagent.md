---
title: Dynatrace OneAgent
description: AEM Aprenda a utilizar OneAgent de Dynatrace con el as a Cloud Service de la
source-git-commit: 2e70c8be73915bea860b98e02c08772bb4f5dcd2
workflow-type: tm+mt
source-wordcount: '263'
ht-degree: 0%

---


# Dynatrace OneAgent {#dynatrace-oneagent}

Adobe AEM permite utilizar OneAgent de Dynatrace para monitorizar los problemas as a Cloud Service como parte de una implementación empresarial, identificar la causa de cualquier problema potencial y tomar medidas para solucionarlo según sea necesario. <!-- When GA, add: Read this [Dynatrace article](https://www.dynatrace.com/hub/detail/adobe-experience-manager/) about AEM monitoring to learn more. -->

## AEM Integración de OneAgent con el as a Cloud Service {#integrating-oneagent-with-aem-as-a-cloud-service}

AEM Los clientes de Dynatrace OneAgent pueden monitorizar su uso de la solicitando conectividad a través de un ticket de asistencia al cliente.

A continuación se describen los detalles necesarios para las solicitudes de conectividad:

| **Campo** | **Descripción** |
|---|---|
| URL de entorno de Dynatrace | La URL de su entorno de Dynatrace.<br><br>Para los clientes de Dynatrace SaaS, el formato es `https://<environment>.live.dynatrace.com`.<br><br>Para los clientes de Dynatrace Managed, el formato es `https://<your-managed-url>/e/<environmentId>` |
| ID de entorno de Dynatrace | El ID del entorno de Dynatrace, que se puede encontrar en la URL del entorno |
| Token de entorno de Dynatrace | El token de entorno de OneAgent. Consulte la documentación de Dynatrace para ver cómo crearlo.<br><br>Esto debe considerarse un secreto, por lo que debe seguir las prácticas de seguridad adecuadas. Por ejemplo, protéjalo con contraseña en un sitio web como **zerobin.net**, a la que puede hacer referencia el ticket de asistencia al cliente, junto con la contraseña. |
| Token de acceso a API de Dynatrace | El token de acceso API del entorno de Dynatrace. Consulte la documentación de Dynatrace para ver cómo crearlo.<br><br>Esto debe considerarse un secreto, por lo que debe seguir las prácticas de seguridad adecuadas. Por ejemplo, protéjalo con contraseña en un sitio web como **zerobin.net**, a la que puede hacer referencia el ticket de asistencia al cliente, junto con la contraseña.<br><br>Nota: Esto solo es necesario para Dynatrace Managed. |
| Puerto de destino de Dynatrace | El puerto de destino de Dynatrace.<br><br>Nota: Esto solo es necesario para Dynatrace Managed. |
| AEM ID de entorno(s) de la | AEM Id. de entorno de la red de trabajo que Dynatrace va a monitorizar. |


