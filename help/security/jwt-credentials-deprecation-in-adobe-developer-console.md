---
title: Credenciales JWT de Adobe Developer Console en desuso
description: Obtenga información sobre el impacto de la desaprobación de credenciales de JWT en Adobe Developer AEM Console en el uso de la tarjeta de acceso de la interfaz de usuario de.
exl-id: 7c811081-484c-41f7-a289-4e9a10a837b3
source-git-commit: 802e29017d3f1e59ee1676b4172292cb3453648a
workflow-type: tm+mt
source-wordcount: '557'
ht-degree: 56%

---

# Credenciales JWT de Adobe Developer Console en desuso {#jwt-credentials-deprecation-in-adobe-developer-console}

>[!NOTE]
>
>Los clientes de AEM 6.5 deben hacer referencia a [este artículo](https://experienceleague.adobe.com/es/docs/experience-manager-65/content/security/jwt-credentials-deprecation-in-adobe-developer-console) para obtener más información.

Los clientes de Adobe utilizan [Adobe Developer Console](https://developer.adobe.com/console) para generar credenciales que permitan el acceso a varias API. Los clientes seleccionan entre varios tipos de credenciales, que van de servidor a servidor OAuth a aplicaciones de una sola página. Uno de estos tipos de credenciales, las credenciales de cuenta de servicio (JWT), han quedado obsoletas y pasan a ser las credenciales de servidor a servidor de OAuth. Las credenciales de la nueva cuenta de servicio (JWT) no se pueden crear el 3 de junio de 2024 o después, y las credenciales de JWT existentes no funcionarán el 27 de enero de 2025 o después. Puede [obtener más información sobre el desuso](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/migration/).

En este artículo se ofrece contexto adicional sobre cómo AEM as a Cloud Service debe gestionar el desuso.

AEM Actualmente, la principal desventaja es que las características de la aplicación aún no son compatibles con las nuevas credenciales de servidor a servidor de OAuth. AEM AEM La asistencia estará disponible próximamente, para mediados de mayo de 2024, mediante un lanzamiento de la versión de la versión de la para as a Cloud Service. Es posible que haya recibido un correo electrónico con instrucciones para migrar sus credenciales de JWT, pero asegúrese de que puede y debe aplazar la migración de credenciales hasta que AEM admita el nuevo tipo de credencial de servidor OAuth.

AEM Las secciones siguientes enumeran los escenarios en los que los clientes deben (o a veces no) reemplazar sus credenciales de cuenta de servicio (JWT) con credenciales de servidor a servidor OAuth, una vez que los clientes las admitan a mediados de mayo. Las credenciales de servidor a servidor se admiten a través de la cuenta de servicio (JWT) de OAuth, una vez que los clientes las admitan a mediados de mayo. [Averigüe cómo](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/migration/#migration-overview) reemplazar las credenciales en el futuro.

>[!NOTE]
>
>[**AEM** Developer Console](/help/implementing/developing/introduction/development-guidelines.md#crxde-lite-and-developer-console) (observe **AEM** en el nombre, que lo distingue del nombre **Adobe** Developer Console) proporciona una utilidad para generar [tokens JWT](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md) que se utilizan para las API de servidor a servidor. Estas credenciales no están en desuso y pueden seguir utilizándose.


## Integración de AEM con otras soluciones de Adobe {#integrating-aem-with-other-adobe-solutions}

**Acción** AEM : espere a migrar hasta después de mediados de mayo de 2024, cuando el usuario lo admita (este artículo se actualizará en ese momento).

**Versiones relevantes de AEM**: AEM as a Cloud Service.

Los clientes de AEM utilizan la interfaz de usuario de Autor de AEM para configurar integraciones con todas las demás soluciones de Adobe. Por ejemplo, Adobe Target, Adobe Analytics, Adobe Launch, AFCS y muchos más.

![Integración de AEM con otras soluciones](/help/security/assets/jwt-deprecation.png)

A modo de ejemplo, estas son [las instrucciones](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/sites/integrations/integration-adobe-target-ims) para configurar la integración con Adobe Target. La clave API en la variable [AEM Finalización de la configuración de IMS en la](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/sites/integrations/integration-adobe-target-ims#completing-the-ims-configuration-in-aem) AEM La sección debe migrarse al tipo de credencial de servidor a servidor de OAuth, una vez que admita estas credenciales a mediados de mayo. El tipo de credencial de servidor a servidor de OAuth es compatible con estas credenciales. Estas instrucciones se actualizarán a mediados de mayo para ayudarle a aplicar las nuevas credenciales de servidor a servidor de OAuth.

## API de Cloud Manager {#cloud-manager-apis}

**Acción**: Migre a las credenciales de OAuth de servidor a servidor.

**Versiones relevantes de AEM**: AEM as a Cloud Service.

Los clientes crean proyectos de Adobe Developer Console para que puedan invocar las [API de Cloud Manager](https://developer.adobe.com/experience-cloud/cloud-manager/guides/getting-started/create-api-integration/). Las credenciales del proyecto de Adobe Developer deben migrarse al tipo de credencial de servidor a servidor OAuth antes de que las credenciales de JWT obsoletas caduquen en enero de 2025.

## Proyectos generados automáticamente {#autogen-projects}

**Acción**: no migre porque el Adobe va a migrar en su nombre.

**Versiones relevantes de AEM**: AEM as a Cloud Service.

AEM Cuando Cloud Manager aprovisiona de entorno as a Cloud Service, genera automáticamente un proyecto de la consola de Adobe Developer con credenciales de JWT. Este proyecto está marcado como de solo lectura, como se ilustra en la captura de pantalla siguiente. Los clientes no pueden ni deben intentar migrar estos proyectos a credenciales de servidor a servidor OAuth; en su lugar, la Adobe migrará estos proyectos por su cuenta antes de que ya no se puedan utilizar.

![Proyectos generados automáticamente](/help/security/assets/jwt-deprecation-autogen-projects.png)
