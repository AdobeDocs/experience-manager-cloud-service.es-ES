---
title: ¿Cómo configurar Microsoft Dynamics 365 y Salesforce fuera de los modelos de datos de formulario para formularios adaptables?
description: Aprenda a integrar Microsoft Dynamics 365 y Salesforce con formularios adaptables.
exl-id: 2a43b2db-2dfb-4c79-88be-ea770b44dac1
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '936'
ht-degree: 1%

---

# Configurar [!DNL Microsoft Dynamics 365] y [!DNL Salesforce] cloud services {#configure-azure-storage}

[[!DNL Experience Manager Forms] Integración de datos](data-integration.md) proporciona [!DNL Microsoft Dynamics 365] y [!DNL Salesforce] servicios de nube para integrar formularios adaptables con modelos de datos de formulario integrados. A continuación, el Forms adaptable puede interactuar con [!DNL Microsoft Dynamics 365] y [!DNL Salesforce] para activar los flujos de trabajo empresariales. Por ejemplo:

* Escribir datos en [!DNL Microsoft Dynamics 365] y [!DNL Salesforce] sobre el envío del formulario adaptable.
* Escribir datos en [!DNL Microsoft Dynamics 365] y [!DNL Salesforce] a través de entidades personalizadas definidas en el Modelo de datos de formulario y viceversa.
* Consulta [!DNL Microsoft Dynamics 365] y [!DNL Salesforce] para datos y rellene previamente Forms adaptable.
* Leer datos de [!DNL Microsoft Dynamics 365] y [!DNL Salesforce] servidor.

[!DNL Microsoft Dynamics 365] y [!DNL Salesforce] los servicios en la nube y los modelos de datos de formulario están disponibles de forma predeterminada en la [!DNL AEM Forms] servidor después de [configuración de un proyecto de desarrollo para Forms basado en el arquetipo de Experience Manager](setup-local-development-environment.md##forms-cloud-service-local-development-environment).

>[!NOTE]
>
>Microsoft Dynamics 365 y [!DNL Salesforce] los servicios de nube y los modelos de datos de formulario solo están disponibles de forma predeterminada si configura una [!DNL Experience Manager Forms] como [!DNL Cloud Service] proyecto basado en [AEM Tipo de archivo 30](https://github.com/adobe/aem-project-archetype/releases/tag/aem-project-archetype-30) o posterior.

## Configurar [!DNL Salesforce] servicio en la nube {#configure-salesforce-cloud-service}

Antes de configurar la variable [!DNL Salesforce] servicios de nube, asegúrese de realizar las siguientes tareas:

* [Crear una conexión OAuth habilitada [!DNL Salesforce] aplicación](https://help.salesforce.com/s/articleView?id=sf.connected_app_create_api_integration.htm&amp;type=5). Al crear las [!DNL Salesforce] especifique la URL de devolución de llamada con el formato siguiente:

   ```
   https://'[server]:[port]'/libs/fd/fdm/gui/components/admin/fdmcloudservice/createcloudconfigwizard/cloudservices.html
   ```

   Donde el servidor y el puerto hacen referencia al nombre de host y al número de puerto para la variable [!DNL AEM Forms] servidor.

* Al crear las [!DNL Salesforce] aplicación, especificar `full` y `offline_access` como valores para el ámbito de OAuth.

* Tome nota de los valores del ID de cliente (denominado clave de consumidor) y del secreto de cliente (denominado Secreto de consumidor) para la aplicación conectada.

Siga estos pasos para configurar la variable [!DNL Salesforce] servicio en la nube:

1. Activado [!DNL AEM Forms] instancia de autor, vaya a **[!UICONTROL Herramientas]** ![martillo](assets/hammer.png) > **[!UICONTROL Cloud Services]** > **[!UICONTROL Fuentes de datos]**. La lista de carpetas de contenedores disponibles incluye una carpeta con el título especificado para `DappTitle`  while [generación del proyecto de arquetipo de AEM](setup-local-development-environment.md##forms-cloud-service-local-development-environment).
1. Pulse el nombre de la carpeta, seleccione **[!UICONTROL Configuración de Salesforce Cloud]** y toque **[!UICONTROL Propiedades]**.
1. En el **[!UICONTROL Configuración de autenticación]** pestaña:
   1. Especifique la variable [!DNL Salesforce] URL de dominio en la variable **[!UICONTROL Host]** campo . Por ejemplo, [Domain-name].my.salesforce.com.
   1. Especifique el ID de cliente (denominado Clave de consumidor) y el secreto de cliente (denominado Secreto de consumidor) para la aplicación conectada.
   1. Especifique **offline_access completo** (`full` y `offine_access` valores separados por un espacio) en la **[!UICONTROL Ámbito de autorización]** campo .
   1. Toque **[!UICONTROL Conectarse a OAuth]**. Se le redirige a [!DNL Microsoft Dynamics] página de inicio de sesión.
   1. Inicie sesión con su [!DNL Salesforce] credenciales y aceptar para permitir que la configuración del servicio de nube se conecte a [!DNL Salesforce] servicio. Si la conexión se realiza correctamente, se le redirige a la función [!DNL Salesforce] página de configuración del servicio de nube, que muestra un mensaje de éxito.
1. Toque **[!UICONTROL Guardar y cerrar]** para completar la configuración.

### Acceso predeterminado [!DNL Salesforce] Modelo de datos de formulario

A [!DNL Salesforce] El Modelo de datos de formulario está disponible de forma predeterminada en la [!DNL AEM Forms] servidor después de [configuración de un proyecto de desarrollo para Forms basado en el arquetipo de Experience Manager](setup-local-development-environment.md##forms-cloud-service-local-development-environment).

Para acceder al Modelo de datos de formulario, vaya a **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Integraciones de datos]**. La lista de carpetas disponibles incluye una carpeta con el título especificado para `DappTitle`  while [generación del proyecto de arquetipo de AEM](setup-local-development-environment.md##forms-cloud-service-local-development-environment). Pulse el nombre de la carpeta, seleccione la opción **[!UICONTROL Modelo de datos de Salesforce]** y pulse Editar ![Editar](assets/edit.png) para ver el modelo de datos del formulario.

Después de configurar la variable [[!DNL Salesforce] Servicio Cloud Config](#configure-salesforce-cloud-service), puede integrar formularios adaptables con [!DNL Salesforce] Modelo de datos.

## Configurar [!DNL Microsoft Dynamics 365] servicio en la nube {#configure-dynamics-cloud-service}

Antes de configurar la variable [!DNL Microsoft Dynamics 365] servicio en la nube, asegúrese de realizar las siguientes tareas:

* [Registre una solicitud para [!DNL Microsoft Dynamics 365] con Azure Active Directory](https://docs.microsoft.com/en-us/powerapps/developer/data-platform/walkthrough-register-app-azure-active-directory). Al crear las [!DNL Microsoft Dynamics 365] especifique las URL de respuesta con el formato siguiente:

   ```
   https://'[server]:[port]'/libs/fd/fdm/gui/components/admin/fdmcloudservice/createcloudconfigwizard/cloudservices.html
   ```

   Donde el servidor y el puerto hacen referencia al nombre de host y al número de puerto para la variable [!DNL AEM Forms] servidor.

* Tome nota de los valores del ID de cliente (también denominado ID de aplicación) y del secreto de cliente para la aplicación conectada.

Siga estos pasos para configurar la variable [!DNL Microsoft Dynamics 365] servicio en la nube:

1. Activado [!DNL AEM Forms] instancia de autor, vaya a **[!UICONTROL Herramientas]** ![martillo](assets/hammer.png) > **[!UICONTROL Cloud Services]** > **[!UICONTROL Fuentes de datos]**. La lista de carpetas de contenedores disponibles incluye una carpeta con el título especificado para `DappTitle`  while [generación del proyecto de arquetipo de AEM](setup-local-development-environment.md##forms-cloud-service-local-development-environment).
1. Pulse el nombre de la carpeta, seleccione **[!UICONTROL Configuración de nube de Microsoft Dynamics 365]** y toque **[!UICONTROL Propiedades]**.
1. En el **[!UICONTROL Configuración de autenticación]** pestaña:
   1. Introduzca el valor de la variable **[!UICONTROL Raíz del servicio]** campo . Vaya a la instancia de Dynamics y vaya a [Recursos para desarrolladores](https://docs.microsoft.com/en-us/powerapps/developer/data-platform/view-download-developer-resources) para ver el valor del campo Raíz del servicio . Por ejemplo, `https://<tenant-name>.dynamics.com/api/data/v9.1/`
   1. Especifique el ID de cliente (denominado ID de aplicación) y el secreto de cliente para la aplicación conectada.
   1. Reemplazar `{tenant}` con un ID de inquilino en la variable **[!UICONTROL URL de OAuth]**, **[!UICONTROL Actualizar URL del token]** y **[!UICONTROL Dirección URL del token de acceso]** campos.
   1. Especifique la URL de instancia de dinámica en la variable **[!UICONTROL Recurso]** campo a configurar [!UICONTROL Microsoft Dynamics] con un modelo de datos de formulario. Utilice la URL raíz del servicio para derivar la URL de instancia de Dynamics. Por ejemplo, `https://<tenant-name>.dynamics.com`.

   1. Especifique `openid` en el **[!UICONTROL Ámbito de autorización]** campo para el proceso de autorización en [!DNL Microsoft Dynamics 365].
   1. Inicie sesión con su [!DNL Microsoft Dynamics 365] credenciales y aceptar para permitir que la configuración del servicio de nube se conecte a [!DNL Microsoft Dynamics 365] servicio. Si la conexión se realiza correctamente, se le redirige a la función [!DNL Microsoft Dynamics 365] página de configuración del servicio de nube, que muestra un mensaje de éxito.
1. Toque **[!UICONTROL Guardar y cerrar]** para completar la configuración.

### Acceso predeterminado [!DNL Microsoft Dynamics 365] Modelo de datos de formulario

A [!DNL Microsoft Dynamics 365] El Modelo de datos de formulario está disponible de forma predeterminada en la [!DNL AEM Forms] servidor después de [configuración de un proyecto de desarrollo para Forms basado en el arquetipo de Experience Manager](setup-local-development-environment.md##forms-cloud-service-local-development-environment).

Para acceder al Modelo de datos de formulario, vaya a **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Integraciones de datos]**. La lista de carpetas disponibles incluye una carpeta con el título especificado para `DappTitle`  while [generación del proyecto de arquetipo de AEM](setup-local-development-environment.md##forms-cloud-service-local-development-environment). Pulse el nombre de la carpeta, seleccione la opción **[!UICONTROL Modelo de datos de Microsoft Dynamics 365]** y pulse Editar ![Editar](assets/edit.png) para ver el modelo de datos del formulario.

Después de configurar la variable [[!DNL Microsoft Dynamics 365] Servicio Cloud Config](#configure-dynamics-cloud-service), puede integrar formularios adaptables con [!DNL Microsoft Dynamics 365] Modelo de datos.
