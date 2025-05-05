---
title: Configurar los modelos de datos de formulario predeterminados de Salesforce para Forms adaptable
description: Aprenda a integrar Salesforce con Forms adaptable.
feature: Adaptive Forms, Form Data Model
role: User, Developer
source-git-commit: 3a12fff170f521f6051f0c24a4eb28a12439eec1
workflow-type: tm+mt
source-wordcount: '489'
ht-degree: 71%

---


# Configuración de Salesforce para AEM Forms {#configure-azure-storage}

[[!DNL Experience Manager Forms] Integración de datos](data-integration.md) proporciona a [!DNL Salesforce] Cloud Services para integrar Forms adaptable con el modelo de datos de formulario OOTB (FDM). El Forms adaptable puede interactuar con [!DNL Salesforce] servidores para habilitar los flujos de trabajo empresariales. Por ejemplo:

* escribir datos sobre el envío de formularios adaptables en [!DNL Salesforce];
* Escriba datos en [!DNL Salesforce] a través de entidades personalizadas definidas en el modelo de datos de formulario (FDM) y viceversa.
* consultar datos en el servidor de [!DNL Salesforce] y rellenar previamente formularios adaptables.
* leer datos del servidor de [!DNL Salesforce].

Los servicios en la nube de [!DNL Salesforce] y el modelo de datos de formulario (FDM) están disponibles de forma predeterminada en el servidor [!DNL AEM Forms] después de [configurar un proyecto de desarrollo para Forms basado en el arquetipo de Experience Manager](setup-local-development-environment.md#forms-cloud-service-local-development-environment).

>[!NOTE]
>
>Los servicios en la nube de [!DNL Salesforce] y el modelo de datos de formulario (FDM) solo están disponibles de forma predeterminada si configuró un proyecto de [!DNL Experience Manager Forms] as a [!DNL Cloud Service] basado en [AEM Archetype 30](https://github.com/adobe/aem-project-archetype/releases/tag/aem-project-archetype-30) o posterior.

## Configurar el servicio en la nube de [!DNL Salesforce] {#configure-salesforce-cloud-service}

Antes de configurar los servicios en la nube de [!DNL Salesforce], asegúrese de realizar las siguientes tareas:

* [Cree una aplicación de  [!DNL Salesforce]  conectada y habilitada para OAuth ](https://help.salesforce.com/s/articleView?id=sf.connected_app_create_api_integration.htm&amp;type=5). Al crear la aplicación conectada de [!DNL Salesforce], especifique la URL de devolución de llamada con el siguiente formato:

  ```
  https://'[server]:[port]'/libs/fd/fdm/gui/components/admin/fdmcloudservice/createcloudconfigwizard/cloudservices.html
  ```

  Donde el servidor y el puerto hacen referencia al nombre de host y al número de puerto del servidor de [!DNL AEM Forms].

* Cuando cree la aplicación conectada de [!DNL Salesforce], especifique `full` y `offline_access` como valores del ámbito de OAuth.

* Tome nota de los valores del ID de cliente (denominado “clave del cliente”) y del secreto de cliente (denominado “secreto de cliente”) de la aplicación conectada.

Siga estos pasos para configurar el servicio en la nube de [!DNL Salesforce]:

1. En la instancia de autor de [!DNL AEM Forms], vaya a **[!UICONTROL Herramientas]** ![martillo](assets/hammer.png) > **[!UICONTROL Cloud Services]** > **[!UICONTROL Fuentes de datos]**.
2. Seleccione el nombre de la carpeta, **[!UICONTROL Configuración de Salesforce Cloud]** y **[!UICONTROL Propiedades]**.
3. En la pestaña **[!UICONTROL Configuración de autenticación]**:
   1. Especifique la URL del dominio de [!DNL Salesforce] en el campo **[!UICONTROL Host]**. Por ejemplo, [Domain-name].my.salesforce.com.
   2. Especifique el ID de cliente (denominado “clave del cliente”) y el secreto de cliente (denominado “secreto de cliente”) para la aplicación conectada.
   3. Especifique **full offline_access** (los valores `full` y `offine_access` separados por un espacio) en el campo **[!UICONTROL Ámbito de autorización]**.
   4. Seleccione **[!UICONTROL Conectarse a OAuth]**. Se le redirigirá a la página de inicio de sesión de [!DNL Salesforce].
   5. Inicie sesión con sus credenciales de [!DNL Salesforce] y haga clic en Aceptar para permitir que la configuración del servicio en la nube se conecte al servicio de [!DNL Salesforce]. Si la conexión se ha realizado correctamente, se le redirigirá a la página de configuración del servicio en la nube de [!DNL Salesforce], la cual mostrará un mensaje de éxito.
4. Seleccione **[!UICONTROL Guardar y cerrar]** para completar la configuración.

### Acceso al modelo de datos de formulario (FDM) predeterminado de [!DNL Salesforce]

Hay disponible un modelo de datos de formulario (FDM) de [!DNL Salesforce] de forma predeterminada en el servidor de [!DNL AEM Forms] cuando [se configura un proyecto de desarrollo de formularios basado en el arquetipo de Experience Manager](setup-local-development-environment.md#forms-cloud-service-local-development-environment).

Para acceder al modelo de datos de formulario (FDM):
1. Vaya a **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Integraciones de datos]**.
1. Seleccione el nombre de la carpeta, el **[!UICONTROL Modelo de datos de Salesforce]** y el icono ![Editar](assets/edit.png) para ver el modelo de datos de formulario.

Después de configurar el [&#128279;](#configure-salesforce-cloud-service)servicio de configuración en la nube de [!DNL Salesforce] , podrá integrar formularios adaptables con el modelo de datos predeterminado de [!DNL Salesforce].

>[!MORELIKETHIS]
>
>* [Configuración de fuentes de datos para AEM Forms](/help/forms/configure-data-sources.md)
>* [Configuración del almacenamiento de Azure para AEM Forms](/help/forms/configure-azure-storage.md)
>  [Añadir Portal de Forms a una página de AEM Sites](/help/forms/configure-forms-portal.md)
