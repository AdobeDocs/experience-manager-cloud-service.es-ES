---
title: Credenciales de JWT de Adobe Developer Console en desuso
description: Obtenga información sobre el impacto de las credenciales de JWT en desuso de Adobe Developer Console en AEM.
exl-id: 7c811081-484c-41f7-a289-4e9a10a837b3
feature: Security
role: Admin
source-git-commit: 85cef99dc7a8d762d12fd6e1c9bc2aeb3f8c1312
workflow-type: tm+mt
source-wordcount: '483'
ht-degree: 97%

---

# Credenciales de JWT de Adobe Developer Console en desuso {#jwt-credentials-deprecation-in-adobe-developer-console}

>[!NOTE]
>
>AEM AEM Los clientes de.5 deben hacer referencia a [la documentación comparable de la versión 6.5](https://experienceleague.adobe.com/es/docs/experience-manager-65/content/security/jwt-credentials-deprecation-in-adobe-developer-console) para obtener más información.

Los clientes de Adobe utilizan [Adobe Developer Console](https://developer.adobe.com/console) para generar credenciales que permitan el acceso a varias API. Los clientes seleccionan entre varios tipos de credenciales, que van de servidor a servidor OAuth a aplicaciones de una sola página. Uno de estos tipos de credenciales, las credenciales de cuenta de servicio (JWT), han quedado obsoletas y pasan a ser las credenciales de servidor a servidor de OAuth. Las credenciales de la nueva cuenta de servicio (JWT) no se pueden crear el 3 de junio de 2024 o después, y las credenciales de JWT existentes no funcionarán el 27 de enero de 2025 o después. Puede [obtener más información sobre el desuso](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/migration/).

En este artículo se ofrece contexto adicional sobre cómo AEM as a Cloud Service debe gestionar el desuso.

Lo más importante es que AEM ahora es compatible con las nuevas credenciales de servidor a servidor de OAuth para AEM as a Cloud Service. Es posible que haya recibido un correo electrónico con instrucciones para migrar sus credenciales de JWT. Esta migración ya se puede realizar.

En las secciones siguientes se enumeran los escenarios en los que los clientes deben (o en algunos casos, no) reemplazar sus credenciales de cuenta de servicio (JWT) por credenciales de servidor a servidor de OAuth, ahora que AEM los admite. [Lea cómo](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/migration/#migration-overview) migrar las credenciales.

>[!NOTE]
>
>[**AEM** Developer Console](/help/implementing/developing/introduction/development-guidelines.md#crxde-lite-and-developer-console) (observe **AEM** en el nombre, que lo distingue del nombre **Adobe** Developer Console) proporciona una utilidad para generar [tokens JWT](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md) que se utilizan para las API de servidor a servidor. Estas credenciales no están en desuso y pueden seguir utilizándose.

## Integración de AEM con otras soluciones de Adobe {#integrating-aem-with-other-adobe-solutions}

**Acción**: migre la configuración ahora que AEM admite las credenciales de OAuth.

**Versiones relevantes de AEM**: AEM as a Cloud Service.

Los clientes de AEM lo utilizan para configurar las integraciones con otras muchas soluciones de Adobe. Por ejemplo, Adobe Target y Adobe Analytics, entre otras.

Consulte la [Configuración de integraciones de IMS para AEM as a Cloud Service](/help/security/setting-up-ims-integrations-for-aem-as-a-cloud-service.md) para obtener más información sobre cómo hacer lo siguiente:

* crear configuraciones con credenciales de OAuth.
* Migrar las configuraciones creadas con credenciales de JWT para utilizar las credenciales de OAuth.

## Las API de Cloud Manager {#cloud-manager-apis}

**Acción**: migre sus credenciales de JWT a las credenciales de OAuth, ahora ya admitidas por Cloud Manager.

**Versiones relevantes de AEM**: AEM as a Cloud Service.

Los clientes crean proyectos de Adobe Developer Console para que puedan invocar las [API de Cloud Manager](https://developer.adobe.com/experience-cloud/cloud-manager/guides/getting-started/create-api-integration/). Las credenciales del proyecto de Adobe Developer deben migrarse al tipo de credencial de servidor a servidor de OAuth, antes de que las credenciales de JWT caduquen en enero de 2025.

## Proyectos generados automáticamente {#autogen-projects}

**Acción**: no migre, ya que Adobe lo hará en su nombre.

**Versiones relevantes de AEM**: AEM as a Cloud Service.

Cuando Cloud Manager aprovisiona entornos AEM as a Cloud Service, genera automáticamente un proyecto de Adobe Developer Console con credenciales de JWT. Este proyecto está marcado como de solo lectura, como se ilustra en la captura de pantalla siguiente. Los clientes no pueden ni deben intentar migrar estos proyectos a las credenciales de servidor a servidor de OAuth. En su lugar, Adobe migra estos proyectos por su cuenta antes de que las credenciales queden ain efecto.

![Proyectos generados automáticamente](/help/security/assets/jwt-deprecation-autogen-projects.png)
