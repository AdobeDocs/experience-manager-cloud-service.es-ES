---
title: Integración del flujo de credenciales del cliente de Salesforce by OAuth 2.0
seo-title: Salesforce integration with AEM Forms using OAuth 2.0 client credential flow
description: Pasos para integrar la integración de Salesforce con AEM Forms mediante el flujo de credenciales del cliente de OAuth 2.0
seo-description: Steps to integrate Salesforce integration with AEM Forms using OAuth 2.0 client credential flow
Keywords: Integration of Salesforce using OAuth 2.0 client credential flow, salesforce integration with oauth2 using client credential flow, salesforce and client credential integration
source-git-commit: b8366fc19a89582f195778c92278cc1e15b15617
workflow-type: tm+mt
source-wordcount: '420'
ht-degree: 5%

---


# Integración del flujo de credenciales del cliente de Salesforce by OAuth 2.0 {#configure-salesforce-with-ouath-2.0-client-credential}

| Versión | Vínculo del artículo |
| -------- | ---------------------------- |
| AEM 6.5 | [Haga clic aquí](https://experienceleague.adobe.com/docs/experience-manager-65/forms/form-data-model/oauth2-client-credentials-flow-for-server-to-server-integration.html) |
| AEM as a Cloud Service | Este artículo |

Puede utilizar las credenciales de cliente de OAuth 2.0 para integrar AEM Forms con la aplicación Salesforce. Las credenciales de cliente de OAuth 2.0 son un método estándar y seguro para la comunicación directa sin la participación del usuario.

![Flujo de trabajo al establecer la comunicación entre AEM Forms y la aplicación Salesforce](/help/forms/assets/salesforce-workflow.png)
AEM Forms intercambia las credenciales del cliente (clave de consumidor y secreto de consumidor), definidas en la aplicación conectada de Salesforce, para obtener un token de acceso.

El uso de credenciales de cliente OAuth 2.0 para la autenticación a través de la autenticación de flujo de código de autorización ofrece varias ventajas:

* La autenticación de credenciales de cliente de OAuth 2.0 permite más de cinco conexiones por usuario.
* AEM AEM La configuración de la fuente de datos sigue funcionando en la desactivación, los cambios de acceso y la actualización de la contraseña de un usuario de la.

## Requisitos previos {#prerequisites}

AEM Antes de establecer la comunicación entre una aplicación de Salesforce y un entorno de:

* Crear un [Aplicación conectada de Salesforce con flujo de credenciales de cliente de OAuth 2.0](https://help.salesforce.com/s/articleView?id=sf.connected_app_client_credentials_setup.htm&amp;type=5) y un usuario solo de API para su organización y obtenga la clave de consumidor y el secreto de consumidor para la aplicación.

* Asegúrese de que el archivo Swagger esté configurado correctamente para que coincida con las API de su organización. También puede optar por [crear un archivo Swagger](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/forms/integrate-with-salesforce/describe-rest-api.html) AEM desde cero, adaptado para su uso en su entorno de la.


## Configurar la aplicación de Salesforce mediante el flujo de credenciales del cliente de OAuth 2.0 {#steps-to-create-aem-datasource-configuration}

Para integrar la aplicación Salesforce con un formulario adaptable mediante la configuración de autenticación de credenciales de cliente de OAuth 2.0, realice los siguientes pasos:

1. Inicie sesión en la instancia de autor de .
1. Ir a **[!UICONTROL Herramientas]** > **[!UICONTROL Cloud Service]** > **[!UICONTROL Fuentes de datos]**.
1. Seleccione la carpeta de configuración.
1. Clic **[!UICONTROL Crear]** y el **[!UICONTROL Crear configuración de fuente de datos]** aparece.
1. Especifique el **[!UICONTROL Título]** y seleccione la **[!UICONTROL Tipo de servicio]** as **[!UICONTROL Servicio RESTful]**.
1. Haga clic en **[!UICONTROL Siguiente]**.
1. Seleccione el **[!UICONTROL Origen de Swagger]** as **[!UICONTROL Archivo].**

   >[!NOTE]
   >
   > Cuando se selecciona el archivo swagger, el esquema, el nombre del host y la ruta base se rellenan automáticamente.

1. Cargue el archivo swagger creado desde el equipo local haciendo clic en **[!UICONTROL Examinar]**.
1. Seleccione el **[!UICONTROL Tipo de autenticación]** as **[!UICONTROL OAuth 2.0]** y el **[!UICONTROL Configuración de autenticación]** aparece el panel.
1. Seleccione el **[!UICONTROL Tipo de concesión]** as **[!UICONTROL Credenciales del cliente]**.
1. Especifique el **[!UICONTROL ID de cliente]** y **[!UICONTROL Secreto del cliente]** obtenido de la aplicación conectada de Salesforce.
1. Especifique el **[!UICONTROL URL de token de acceso]** en formato
   `https://[MyDomainName].my.salesforce.com/services/oauth2/token`.

   >[!NOTE]
   >
   > Cada organización tiene su propio nombre de dominio específico.

1. Clic **[!UICONTROL Probar conexión]**.
1. Si la conexión se realiza correctamente, haga clic en **[!UICONTROL Crear]** botón.

Ahora, puede [crear el modelo de datos de formulario](/help/forms/create-form-data-models.md) para integrar la fuente de datos configurada con el formulario adaptable.
