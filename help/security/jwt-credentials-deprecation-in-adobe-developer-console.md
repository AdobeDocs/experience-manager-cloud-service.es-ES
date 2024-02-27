---
title: Desaprobación de credenciales de JWT en la consola de Adobe Developer
description: Obtenga información sobre el impacto de la obsolescencia de las credenciales de JWT en la consola de Adobe Developer AEM en el uso de la
source-git-commit: e02e38a5267188111f0392a0a5c7b73e6a4f22b5
workflow-type: tm+mt
source-wordcount: '598'
ht-degree: 0%

---


# Desaprobación de credenciales de JWT en la consola de Adobe Developer {#jwt-credentials-deprecation-in-adobe-developer-console}

Adobe que utilizan los clientes [Consola de Adobe Developer](https://developer.adobe.com/console) para generar credenciales que permitan el acceso a varias API. Los clientes seleccionan entre varios tipos de credenciales, que van desde servidor a servidor de OAuth hasta aplicaciones de una sola página. Uno de estos tipos de credenciales, las credenciales de cuenta de servicio (JWT), ha quedado obsoleto y pasa a ser las credenciales de servidor a servidor de OAuth. Las credenciales de la nueva cuenta de servicio (JWT) no se pueden crear el 1 de mayo de 2024 o después, y las credenciales de JWT existentes no funcionarán el 1 de enero de 2025 o después. Puede [más información sobre la obsolescencia](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/migration/).

AEM Este artículo proporciona contexto adicional sobre cómo deben gestionar los clientes de as a Cloud Service AEM y de la versión 6.5 la obsolescencia.

AEM La principal desventaja en este momento es que las características de la aplicación aún no son compatibles con las nuevas credenciales de servidor a servidor de OAuth. AEM AEM La compatibilidad llegará pronto: a mediados de abril de 2024, mediante una versión de la versión de la versión para la versión as a Cloud Service AEM, y a través de un paquete de compatibilidad especial para instalar para la versión 6.5, si ejecuta el último Service Pack 20 o inferior (el Service Pack 21 o superior la incluirá automáticamente). AEM Es posible que haya recibido un correo electrónico con instrucciones para migrar sus credenciales de JWT, pero asegúrese de que puede y debe mantener desactivada la migración de credenciales hasta que el tipo de credencial de servidor a servidor de OAuth sea compatible con el nuevo tipo de credencial de servidor de OAuth.

AEM Las secciones siguientes enumeran los escenarios en los que los clientes deben reemplazar (o en algunos casos no) sus credenciales de cuenta de servicio (JWT) con credenciales de servidor a servidor OAuth, una vez que los clientes las admitan a mediados de abril. [Leer cómo](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/migration/#migration-overview) para reemplazar las credenciales en el futuro.

>[!NOTE]
>
>El [**AEM** Developer Console](/help/implementing/developing/introduction/development-guidelines.md#crxde-lite-and-developer-console) (observe el **AEM** en el nombre, que lo distingue del nombre **Adobe** Developer Console) proporciona una utilidad para generar [tokens JWT](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md) se utiliza para las API de servidor a servidor. Estas credenciales no están en desuso y pueden seguir utilizándose.


## AEM Integración de la solución de con otras soluciones de Adobe {#integrating-aem-with-other-adobe-solutions}

**Acción** AEM : Espere para migrar hasta después de mediados de abril de 2024, cuando el usuario lo admita

**AEM Versiones relevantes de la** AEM : as a Cloud Service y Adobe Managed Services (Service Pack 20 y posterior).


AEM AEM Los clientes de utilizan la interfaz de usuario de Autor de para configurar integraciones con todas las demás soluciones de Adobe de. Por ejemplo, Adobe Target, Adobe Analytics, Adobe Launch, AFCS y muchos más.

![AEM Integración de la solución con otras soluciones de](/help/security/assets/jwt-deprecation.png)

A modo de ejemplo, estos son [las instrucciones](https://docs.mktossl.com/docs/experience-manager-cloud-service/content/sites/integrations/integration-adobe-target-ims.html?lang=en) para configurar la integración con Adobe Target. La clave API en la variable [AEM Finalización de la configuración de IMS en la](https://docs.mktossl.com/docs/experience-manager-cloud-service/content/sites/integrations/integration-adobe-target-ims.html#completing-the-ims-configuration-in-aem) AEM debe migrarse al tipo de credencial de servidor a servidor de OAuth, una vez que admita estas credenciales a mediados de abril, una vez que se haya realizado la migración de la sección de credenciales de servidor a servidor de OAuth (OAuth Server-to-Server), una vez que se admitan dichas credenciales a mediados de abril. Estas instrucciones se actualizarán y revisarán a mediados de abril para ayudarle a aplicar las nuevas credenciales de servidor a servidor de OAuth.

## API de Cloud Manager {#cloud-manager-apis}

**Acción** AEM : Espere para migrar hasta después de mediados de abril de 2024, cuando el usuario lo admita

**AEM Versiones relevantes de la** AEM : as a Cloud Service y Adobe Managed Services (Service Pack 20 y posterior).

Los clientes crean proyectos de Adobe Developer Console para que puedan invocar [API de Cloud Manager](https://developer.adobe.com/experience-cloud/cloud-manager/guides/getting-started/create-api-integration/). Las credenciales del proyecto de Adobe Developer AEM deben migrarse al tipo de credencial de servidor a servidor de OAuth, una vez que Cloud Manager las admita y las haya instalado en el servicio de soporte técnico de Cloud Manager.

## Proyectos generados automáticamente {#autogen-projects}

**Acción**: No migrar, ya que el Adobe migrará en su nombre.

**AEM Versiones relevantes de la** AEM : Solo se ha as a Cloud Service la.

AEM Cuando Cloud Manager aprovisiona entornos as a Cloud Service, genera automáticamente un proyecto de la consola de Adobe Developer con credenciales de JWT. Este proyecto está marcado como de solo lectura, como se ilustra en la captura de pantalla siguiente. Los clientes no pueden ni deben intentar migrar estos proyectos a credenciales de servidor a servidor OAuth; en su lugar, la Adobe migrará estos proyectos por su cuenta antes de que ya no se puedan utilizar.

![Proyectos generados automáticamente](/help/security/assets/jwt-deprecation-autogen-projects.png)

