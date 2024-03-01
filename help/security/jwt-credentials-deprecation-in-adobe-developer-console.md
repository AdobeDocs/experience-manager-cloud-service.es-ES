---
title: Credenciales JWT de Adobe Developer Console en desuso
description: Obtenga información sobre el impacto de las credenciales de JWT en desuso en Adobe Developer Console en AEM.
source-git-commit: e02e38a5267188111f0392a0a5c7b73e6a4f22b5
workflow-type: ht
source-wordcount: '598'
ht-degree: 100%

---


# Credenciales JWT de Adobe Developer Console en desuso {#jwt-credentials-deprecation-in-adobe-developer-console}

Los clientes de Adobe utilizan [Adobe Developer Console](https://developer.adobe.com/console) para generar credenciales que permitan el acceso a varias API. Los clientes seleccionan entre varios tipos de credenciales, que van de servidor a servidor OAuth a aplicaciones de una sola página. Uno de estos tipos de credenciales, las credenciales de cuenta de servicio (JWT), han quedado obsoletas y pasan a ser las credenciales de servidor a servidor de OAuth. Las credenciales de nueva cuenta de servicio (JWT) no se pueden crear el 1 de mayo de 2024 o después, y las credenciales de JWT existentes no funcionarán el 1 de enero de 2025 o después. Puede [obtener más información sobre el desuso](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/migration/).

En este artículo se ofrece contexto adicional sobre cómo los clientes de AEM as a Cloud Service y AEM versión 6.5 deben gestionar el desuso.

Lo más importante en este momento es que las características de la aplicación aún no son compatibles con las nuevas credenciales de servidor a servidor OAuth. La compatibilidad llegará pronto: a mediados de abril de 2024, con una versión de AEM as a Cloud Service y mediante un paquete de compatibilidad especial para instalar para la versión 6.5 de AEM, si ejecuta el último Service Pack 20 o una versión inferior (el Service Pack 21 o superior la incluirá automáticamente). Es posible que haya recibido un correo electrónico con instrucciones para migrar sus credenciales de JWT, pero asegúrese de que puede y debe aplazar la migración de credenciales hasta que AEM admita el nuevo tipo de credencial de servidor OAuth.

En las secciones siguientes se enumeran los escenarios en los que los clientes deben reemplazar (o en algunos casos no) sus credenciales de cuenta de servicio (JWT) por credenciales de servidor a servidor OAuth, una vez que los clientes las admitan a mediados de abril. [Averigüe cómo](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/migration/#migration-overview) reemplazar las credenciales en el futuro.

>[!NOTE]
>
>[**AEM** Developer Console](/help/implementing/developing/introduction/development-guidelines.md#crxde-lite-and-developer-console) (observe **AEM** en el nombre, que lo distingue del nombre **Adobe** Developer Console) proporciona una utilidad para generar [tokens JWT](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md) que se utilizan para las API de servidor a servidor. Estas credenciales no están en desuso y pueden seguir utilizándose.


## Integración de AEM con otras soluciones de Adobe {#integrating-aem-with-other-adobe-solutions}

**Acción**: espere para migrar hasta después de mediados de abril de 2024, cuando AEM lo admita.

**Versiones de AEM relevantes** AEM as a Cloud Service y Adobe Managed Services (Service Pack 20 y versiones inferiores).


Los clientes de AEM utilizan la interfaz de usuario de Autor de AEM para configurar integraciones con todas las demás soluciones de Adobe. Por ejemplo, Adobe Target, Adobe Analytics, Adobe Launch, AFCS y muchos más.

![Integración de AEM con otras soluciones](/help/security/assets/jwt-deprecation.png)

A modo de ejemplo, estas son [las instrucciones](https://docs.mktossl.com/docs/experience-manager-cloud-service/content/sites/integrations/integration-adobe-target-ims.html?lang=es) para configurar la integración con Adobe Target. La clave API en la sección [Finalización de la configuración de IMS en AEM](https://docs.mktossl.com/docs/experience-manager-cloud-service/content/sites/integrations/integration-adobe-target-ims.html?lang=es#completing-the-ims-configuration-in-aem) debe migrarse al tipo de credencial de servidor a servidor OAuth, cuando AEM admita estas credenciales a mediados de abril. Estas instrucciones se actualizarán y revisarán a mediados de abril para ayudarle a aplicar las nuevas credenciales de servidor a servidor OAuth.

## API de Cloud Manager {#cloud-manager-apis}

**Acción**: espere para migrar hasta después de mediados de abril de 2024, cuando AEM lo admita.

**Versiones de AEM relevantes**: AEM as a Cloud Service y Adobe Managed Services (Service Pack 20 y versiones inferiores).

Los clientes crean proyectos de Adobe Developer Console para que puedan invocar las [API de Cloud Manager](https://developer.adobe.com/experience-cloud/cloud-manager/guides/getting-started/create-api-integration/). Las credenciales del proyecto de Adobe Developer deben migrarse al tipo de credencial de servidor a servidor OAuth, una vez que AEM y Cloud Manager las admita.

## Proyectos generados automáticamente {#autogen-projects}

**Acción**: no migre, ya que Adobe lo hará en su nombre.

**Versiones relevantes de AEM**: solamente AEM as a Cloud Service.

Cuando Cloud Manager aprovisiona entornos AEM as a Cloud Service, genera automáticamente un proyecto de Adobe Developer Console con credenciales de JWT. Este proyecto está marcado como de solo lectura, como se ilustra en la captura de pantalla siguiente. Los clientes no pueden ni deben intentar migrar estos proyectos a credenciales de servidor a servidor OAuth; en su lugar, Adobe migrará estos proyectos por su cuenta antes de que ya no se puedan utilizar.

![Proyectos generados automáticamente](/help/security/assets/jwt-deprecation-autogen-projects.png)

