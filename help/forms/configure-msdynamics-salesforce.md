---
title: Configurar los modelos de datos de formulario predeterminados de Microsoft Dynamics 365 y Salesforce para Forms adaptable
description: Aprenda a integrar Microsoft Dynamics 365 y Salesforce con Forms adaptable.
exl-id: 2a43b2db-2dfb-4c79-88be-ea770b44dac1
source-git-commit: 7e3eb3426002408a90e08bee9c2a8b7a7bfebb61
workflow-type: tm+mt
source-wordcount: '960'
ht-degree: 73%

---

# Configuración de Microsoft® Dynamics 365 o Salesforce para AEM Forms {#configure-azure-storage}

| Versión | Vínculo del artículo |
| -------- | ---------------------------- |
| AEM 6.5 | [Haga clic aquí](https://experienceleague.adobe.com/docs/experience-manager-65/forms/form-data-model/oauth2-client-credentials-flow-for-server-to-server-integration.html) |
| AEM as a Cloud Service | Este artículo |

La integración de datos de [[!DNL Experience Manager Forms] ](data-integration.md) proporciona servicios en la nube para [!DNL Microsoft® Dynamics 365] y [!DNL Salesforce] que permiten integrar formularios adaptables con modelos de datos de formulario predeterminados. Después, los formularios adaptables pueden interactuar con los servidores de [!DNL Microsoft® Dynamics 365] y [!DNL Salesforce] para activar los flujos de trabajo empresariales. Por ejemplo:

* escribir datos sobre el envío de formularios adaptables en [!DNL Microsoft® Dynamics 365] y [!DNL Salesforce];
* Escritura de datos en [!DNL Microsoft® Dynamics 365] y [!DNL Salesforce] mediante entidades personalizadas definidas en el modelo de datos de formulario y a la inversa.
* consultar datos en el servidor de [!DNL Microsoft® Dynamics 365] y [!DNL Salesforce] y rellenar previamente formularios adaptables;
* leer datos del servidor de [!DNL Microsoft® Dynamics 365] y [!DNL Salesforce].

[!DNL Microsoft® Dynamics 365] y [!DNL Salesforce] Los servicios en la nube de y los modelos de datos de formulario están disponibles de forma predeterminada en la [!DNL AEM Forms] Servidor después de [configurar un proyecto de desarrollo para Forms basado en el arquetipo de Experience Manager](setup-local-development-environment.md#forms-cloud-service-local-development-environment).

>[!NOTE]
>
>Microsoft® Dynamics 365 y [!DNL Salesforce] Los servicios en la nube de y los modelos de datos de formulario solo están disponibles de forma predeterminada si configura una [!DNL Experience Manager Forms] as a [!DNL Cloud Service] proyecto basado en [AEM Tipo de archivo 30](https://github.com/adobe/aem-project-archetype/releases/tag/aem-project-archetype-30) o más tarde.

## Configurar el servicio en la nube de [!DNL Salesforce] {#configure-salesforce-cloud-service}

Antes de configurar los servicios en la nube de [!DNL Salesforce], asegúrese de realizar las siguientes tareas:

* [Cree una aplicación de  [!DNL Salesforce]  conectada y habilitada para OAuth ](https://help.salesforce.com/s/articleView?id=sf.connected_app_create_api_integration.htm&amp;type=5). Al crear la aplicación conectada de [!DNL Salesforce], especifique la URL de devolución de llamada con el siguiente formato:

  ```
  https://'[server]:[port]'/libs/fd/fdm/gui/components/admin/fdmcloudservice/createcloudconfigwizard/cloudservices.html
  ```

  Donde el servidor y el puerto hacen referencia al nombre de host y al número de puerto del [!DNL AEM Forms] Servidor.

* Cuando cree la aplicación conectada de [!DNL Salesforce], especifique `full` y `offline_access` como valores del ámbito de OAuth.

* Tome nota de los valores del ID de cliente (denominado “clave del cliente”) y del secreto de cliente (denominado “secreto de cliente”) de la aplicación conectada.

Siga estos pasos para configurar el servicio en la nube de [!DNL Salesforce]:

1. En la instancia de autor de [!DNL AEM Forms], vaya a **[!UICONTROL Herramientas]** ![martillo](assets/hammer.png) > **[!UICONTROL Cloud Services]** > **[!UICONTROL Fuentes de datos]**. La lista de carpetas de los contenedores disponibles incluye una carpeta con el título especificado para `DappTitle` al [generar el proyecto de arquetipo de AEM](setup-local-development-environment.md#forms-cloud-service-local-development-environment).
1. Pulse el nombre de la carpeta, seleccione **[!UICONTROL Configuración de Salesforce Cloud]** y pulse **[!UICONTROL Propiedades]**.
1. En la pestaña **[!UICONTROL Configuración de autenticación]**:
   1. Especifique la URL del dominio de [!DNL Salesforce] en el campo **[!UICONTROL Host]**. Por ejemplo, [Domain-name].my.salesforce.com.
   1. Especifique el ID de cliente (denominado “clave del cliente”) y el secreto de cliente (denominado “secreto de cliente”) para la aplicación conectada.
   1. Especifique **full offline_access** (los valores `full` y `offine_access` separados por un espacio) en el campo **[!UICONTROL Ámbito de autorización]**.
   1. Pulse **[!UICONTROL Conectarse a OAuth]**. Se le redirigirá a la página de inicio de sesión de [!DNL Microsoft® Dynamics].
   1. Inicie sesión con sus credenciales de [!DNL Salesforce] y haga clic en Aceptar para permitir que la configuración del servicio en la nube se conecte al servicio de [!DNL Salesforce]. Si la conexión se ha realizado correctamente, se le redirigirá a la página de configuración del servicio en la nube de [!DNL Salesforce], la cual mostrará un mensaje de éxito.
1. Pulse **[!UICONTROL Guardar y cerrar]** para completar la configuración.

### Acceso al modelo de datos de formulario predeterminado de [!DNL Salesforce]

A [!DNL Salesforce] El modelo de datos de formulario está disponible de forma predeterminada en la [!DNL AEM Forms] Servidor después de [configurar un proyecto de desarrollo para Forms basado en el arquetipo de Experience Manager](setup-local-development-environment.md#forms-cloud-service-local-development-environment).

Para acceder al modelo de datos de formulario, vaya a **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Formularios]** > **[!UICONTROL Integraciones de datos]**. La lista de carpetas disponibles incluye una carpeta con el título especificado para `DappTitle` al [generar el proyecto de arquetipo de AEM](setup-local-development-environment.md#forms-cloud-service-local-development-environment). Pulse el nombre de la carpeta, seleccione la opción **[!UICONTROL Modelo de datos de Salesforce]** y pulse el icono ![Editar](assets/edit.png) para ver el modelo de datos de formulario.

Después de configurar el ](#configure-salesforce-cloud-service)servicio de configuración en la nube de [[!DNL Salesforce] , podrá integrar formularios adaptables con el modelo de datos predeterminado de [!DNL Salesforce].

## Configurar el servicio en la nube de [!DNL Microsoft® Dynamics 365] {#configure-dynamics-cloud-service}

Antes de configurar el servicio en la nube de [!DNL Microsoft® Dynamics 365], asegúrese de realizar las siguientes tareas:

* [Registre una aplicación de  [!DNL Microsoft® Dynamics 365]  con Azure Active Directory](https://docs.microsoft.com/es-es/powerapps/developer/data-platform/walkthrough-register-app-azure-active-directory). Al crear la aplicación conectada de [!DNL Microsoft® Dynamics 365], especifique las URL de respuesta con el siguiente formato:

  ```
  https://'[server]:[port]'/libs/fd/fdm/gui/components/admin/fdmcloudservice/createcloudconfigwizard/cloudservices.html
  ```

  Donde el servidor y el puerto hacen referencia al nombre de host y al número de puerto del [!DNL AEM Forms] Servidor.

* Tome nota de los valores del ID de cliente (también denominado “ID de aplicación”) y del secreto de cliente de la aplicación conectada.

Siga estos pasos para configurar el servicio en la nube de [!DNL Microsoft® Dynamics 365]:

1. En la instancia de autor de [!DNL AEM Forms], vaya a **[!UICONTROL Herramientas]** ![martillo](assets/hammer.png) > **[!UICONTROL Cloud Services]** > **[!UICONTROL Fuentes de datos]**. La lista de carpetas de los contenedores disponibles incluye una carpeta con el título especificado para `DappTitle` al [generar el proyecto de arquetipo de AEM](setup-local-development-environment.md#forms-cloud-service-local-development-environment).
1. Pulse el nombre de la carpeta y seleccione **[!UICONTROL Configuración en la nube de Microsoft® Dynamics 365]** y pulse **[!UICONTROL Propiedades]**.
1. En la pestaña **[!UICONTROL Configuración de autenticación]**:
   1. Introduzca el valor del campo **[!UICONTROL Raíz del servicio]**. Vaya a la instancia de Dynamics y luego a [Recursos para desarrolladores](https://docs.microsoft.com/es-es/powerapps/developer/data-platform/view-download-developer-resources) para ver el valor del campo Raíz del servicio. Por ejemplo, `https://<tenant-name>.dynamics.com/api/data/v9.1/`. 
   1. Especifique el ID de cliente (denominado ID de aplicación) y el secreto de cliente de la aplicación conectada.
   1. Reemplace `{tenant}` con un ID de inquilino en los campos **[!UICONTROL URL de OAuth]**, **[!UICONTROL Actualizar URL del token]** y **[!UICONTROL URL del token de acceso]**.
   1. Especifique la URL de la instancia de Dynamics en la **[!UICONTROL Recurso]** campo para configurar [!UICONTROL Microsoft® Dynamics] con un modelo de datos de formulario. Utilice la URL raíz del servicio para derivar la URL de la instancia de Dynamics. Por ejemplo, `https://<tenant-name>.dynamics.com`.

   1. Especifique `openid` en el campo **[!UICONTROL Ámbito de autorización]** para el proceso de autorización en [!DNL Microsoft® Dynamics 365].
   1. Inicie sesión con sus credenciales de [!DNL Microsoft® Dynamics 365] y haga clic en Aceptar para permitir que la configuración del servicio en la nube se conecte al servicio de [!DNL Microsoft® Dynamics 365]. Si la conexión se ha realizado correctamente, se le redirigirá a la página de configuración del servicio en la nube de [!DNL Microsoft® Dynamics 365], la cual mostrará un mensaje de éxito.
1. Pulse **[!UICONTROL Guardar y cerrar]** para completar la configuración.

### Acceso al modelo de datos de formulario predeterminado de [!DNL Microsoft® Dynamics 365]

A [!DNL Microsoft® Dynamics 365] El modelo de datos de formulario está disponible de forma predeterminada en la [!DNL AEM Forms] Servidor después de [configurar un proyecto de desarrollo para Forms basado en el arquetipo de Experience Manager](setup-local-development-environment.md##forms-cloud-service-local-development-environment).

Para acceder al modelo de datos de formulario, vaya a **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Formularios]** > **[!UICONTROL Integraciones de datos]**. La lista de carpetas disponibles incluye una carpeta con el título especificado para `DappTitle` al [generar el proyecto de arquetipo de AEM](setup-local-development-environment.md#forms-cloud-service-local-development-environment). Pulse el nombre de la carpeta y seleccione **[!UICONTROL Modelo de datos de Microsoft® Dynamics 365]** y pulse el botón Editar ![Editar](assets/edit.png) para ver el modelo de datos de formulario.

Después de configurar el ](#configure-dynamics-cloud-service)servicio de configuración en la nube de [[!DNL Microsoft® Dynamics 365] , podrá integrar formularios adaptables con el modelo de datos predeterminado de [!DNL Microsoft® Dynamics 365].
