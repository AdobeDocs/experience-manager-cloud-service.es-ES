---
title: Cómo integrar Salesforce mediante el flujo de credenciales de cliente de OAuth 2.0 con AEM Forms
description: Aprenda a integrar Salesforce con AEM Forms mediante el flujo de credenciales de cliente de OAuth 2.0. Muestra los pasos para la integración de AEM Forms y Salesforce.
Keywords: Integration of Salesforce using OAuth 2.0 client credential flow, salesforce integration with oauth2 using client credential flow, salesforce and client credential integration, AEM Forms Salesforce integration
feature: Adaptive Forms, Form Data Model
role: User, Developer
exl-id: 2c2029ab-6fb4-41a6-846c-175c3a79d921
source-git-commit: 9eb15dda5f56938d686d0b863cb1ffa841f8228b
workflow-type: ht
source-wordcount: '552'
ht-degree: 100%

---

# Integración del formulario adaptable con Salesforce {#configure-salesforce-with-ouath-2.0-client-credential}

| Versión | Vínculo del artículo |
| -------- | ---------------------------- |
| AEM 6.5 | [Haga clic aquí](https://experienceleague.adobe.com/docs/experience-manager-65/forms/form-data-model/oauth2-client-credentials-flow-for-server-to-server-integration.html?lang=es) |
| AEM as a Cloud Service | Este artículo |

La integración de Adobe Experience Manager (AEM) Forms con Salesforce permite a las organizaciones optimizar los procesos conectando sus capacidades de creación y administración de formularios con la plataforma de Salesforce. La conexión de un formulario adaptable con Salesforce permite un intercambio de datos fluido entre las dos plataformas. Cuando los usuarios envían formularios, los datos se sincronizan de manera automática con Salesforce. Esto garantiza que toda la información del cliente esté actualizada y centralizada dentro del sistema.

Puede utilizar las credenciales de cliente de OAuth 2.0 para integrar AEM Forms con la aplicación Salesforce. Las credenciales de cliente de OAuth 2.0 son un método estándar y seguro para la comunicación directa sin la participación del usuario.

![Flujo de trabajo al establecer la comunicación entre AEM Forms y la aplicación Salesforce](/help/forms/assets/salesforce-workflow.png)

AEM Forms intercambia las credenciales del cliente (clave del cliente y secreto de cliente), definidas en la aplicación conectada de Salesforce, para obtener un token de acceso.

AEM as a Cloud Service ofrece varias acciones de envío predeterminadas para gestionar los envíos de formularios. Puede obtener más información sobre estas opciones en el artículo [Acción de envío del formulario adaptable](/help/forms/configure-submit-actions-core-components.md).

El uso de credenciales del cliente OAuth 2.0 para la autenticación a través de la autenticación de flujo de código de autorización ofrece varias ventajas:

* La autenticación de credenciales de cliente de OAuth 2.0 permite más de cinco conexiones por usuario.
* La configuración de la fuente de datos de AEM sigue funcionando en la desactivación, los cambios de acceso y la actualización de la contraseña de un usuario de AEM.

## Requisitos previos {#prerequisites}

Antes de establecer la comunicación entre una aplicación de Salesforce y un entorno de AEM, haga lo siguiente:

* Cree una [Aplicación conectada de Salesforce con flujo de credenciales de cliente de OAuth 2.0](https://help.salesforce.com/s/articleView?id=sf.connected_app_client_credentials_setup.htm&type=5) y un único usuario de API para su organización y obtenga la clave y el secreto de consumidor para la aplicación.

* Asegúrese de que el archivo Swagger esté configurado correctamente para que coincida con las API de su organización. También puede optar por [crear un archivo Swagger](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/forms/integrate-with-salesforce/describe-rest-api.html?lang=es) desde cero, adaptado para su utilización en el entorno de AEM.


## Configurar la aplicación de Salesforce mediante el flujo de credenciales del cliente de OAuth 2.0 {#steps-to-create-aem-datasource-configuration}

Para conectar un formulario adaptable a la aplicación Salesforce mediante la configuración de autenticación de credenciales de cliente de OAuth 2.0, realice los siguientes pasos:

1. Inicie sesión en la instancia de autor.
1. Vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Fuentes de datos]**.
1. Seleccione la carpeta de configuración.
1. Haga clic en **[!UICONTROL Crear]** y aparece **[!UICONTROL Crear configuración de fuente de datos]**.
1. Especifique el **[!UICONTROL Título]** y seleccione el **[!UICONTROL Tipo de servicio]** como **[!UICONTROL Servicio RESTful]**.
1. Haga clic en **[!UICONTROL Siguiente]**.
1. Seleccione el **[!UICONTROL Origen de Swagger]** como **[!UICONTROL Archivo].**

   >[!NOTE]
   >
   > Cuando se selecciona el archivo Swagger, el esquema, el nombre del host y la ruta base se rellenan automáticamente.

1. Cargue el archivo Swagger creado desde el equipo local haciendo clic en **[!UICONTROL Examinar]**.
1. Seleccione el **[!UICONTROL Tipo de autenticación]** como **[!UICONTROL OAuth 2.0]** y aparecerá el panel **[!UICONTROL Configuración de autenticación]**.
1. Seleccione el **[!UICONTROL Tipo de concesión]** como **[!UICONTROL Credenciales del cliente]**.
1. Especifique el **[!UICONTROL ID de cliente]** y **[!UICONTROL Secreto del cliente]** obtenido de la aplicación conectada de Salesforce.
1. Especifique la **[!UICONTROL URL de token de acceso]** con el formato
   `https://[MyDomainName].my.salesforce.com/services/oauth2/token`.

   >[!NOTE]
   >
   > Cada organización tiene su propio nombre de dominio específico.

1. Haga clic en **[!UICONTROL Probar conexión]**.
1. Si la conexión se realiza correctamente, haga clic en el botón **[!UICONTROL Crear]**.


Después de configurar la aplicación Salesforce, puede utilizar la configuración durante la creación del modelo de datos de formulario (FDM).  Para obtener más información, consulte [Creación de un modelo de datos de formulario (FDM)](create-form-data-models.md). [Configure la acción de envío del modelo de datos de formulario](/help/forms/using-form-data-model.md) para que un formulario adaptable envíe datos a aplicaciones de Salesforce.

Para obtener más información sobre la creación y el uso de modelos de datos de formulario en flujos de trabajo empresariales, consulte [Integración de datos](data-integration.md).

## Artículos relacionados

{{af-submit-action}}


