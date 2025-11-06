---
title: Configurar los modelos de datos de formulario predeterminados de Microsoft Dynamics 365 para Forms adaptable
description: Aprenda a integrar Microsoft Dynamics 365 con Forms adaptable.
feature: Adaptive Forms, Form Data Model
role: User, Developer
exl-id: 29ee324c-cd4c-403b-bb3d-b1eda8e8ad88
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '915'
ht-degree: 16%

---


# Configuración de Microsoft® Dynamics 365 para AEM Forms

La integración de datos de Adobe Experience Manager Forms proporciona una configuración de servicio en la nube para integrar formularios con el servidor de Microsoft Dynamics. Permite crear el modelo de datos de formulario (FDM) en función de las entidades, atributos y servicios definidos en el servicio de Microsoft Dynamics. El modelo de datos de formulario (FDM) se puede utilizar para crear Forms adaptable que interactúe con el servidor de Microsoft Dynamics para habilitar flujos de trabajo empresariales. Por ejemplo:

* consultar datos en el servidor de Microsoft Dynamics y rellenar previamente Forms adaptable;
* escribir datos en Microsoft Dynamics sobre el envío de formularios adaptables;
* escribir datos en Microsoft Dynamics a través de entidades personalizadas definidas en el modelo de datos de formulario (FDM);

AEM as a Cloud Service ofrece varias acciones de envío predeterminadas para gestionar los envíos de formularios. Puede obtener más información sobre estas opciones en el artículo [Acción de envío del formulario adaptable](/help/forms/configure-submit-actions-core-components.md).

<!-- 
[[!DNL Experience Manager Forms] Data Integration](data-integration.md) provides [!DNL Microsoft&reg; Dynamics 365] Cloud Services to integrate Adaptive Forms with out of the box Form Data Model (FDM). The Adaptive Forms can then interact with [!DNL Microsoft&reg; Dynamics 365] servers to enable business workflows. For example:

* Write data into [!DNL Microsoft&reg; Dynamics 365] on Adaptive Form submission.
* Write data in [!DNL Microsoft&reg; Dynamics 365] through custom entities defined in Form Data Model (FDM) and conversely.
* Query [!DNL Microsoft&reg; Dynamics 365]server for data and prepopulate Adaptive Forms.
* Read data from [!DNL Microsoft&reg; Dynamics 365] server.

[!DNL Microsoft&reg; Dynamics 365] cloud services and Form Data Model (FDM) are available out of the box on the [!DNL AEM Forms] Server after you [set up a development project for Forms based on Experience Manager archetype](setup-local-development-environment.md#forms-cloud-service-local-development-environment).

>[!NOTE]
>
>Microsoft&reg; Dynamics 365 cloud services and Form Data Model (FDM) are available out of the box only if you set up an [!DNL Experience Manager Forms] as a [!DNL Cloud Service] project based on [AEM Archetype 30](https://github.com/adobe/aem-project-archetype/releases/tag/aem-project-archetype-30) or later.-->

## Requisitos previos

Antes de integrar [!DNL Microsoft® Dynamics 365] con AEM Forms as a Cloud Service, asegúrese de haber realizado los siguientes pasos:


1. **Configurar la cuenta en Microsoft Dynamics 365**

   Siga los pasos explicados en el vídeo para configurar una cuenta de Microsoft Dynamics 365. En este vídeo, se crea una cuenta de prueba con fines de demostración.

   >[!VIDEO](https://video.tv.adobe.com/v/3444389/)

1. **Crear una cuenta en el Centro de administración de Power Platform**

   Cree una cuenta en el **Centro de administración de Power Platform** para:

   * Agregar Dataverse
   * Habilitar aplicaciones de Microsoft Dynamics 365

   Siga los pasos del vídeo para crear una cuenta en el Centro de administración de Power Platform. En este vídeo, se ha creado una cuenta de prueba con fines de demostración.

   >[!VIDEO](https://video.tv.adobe.com/v/3444388)

1. **Registrar una aplicación para [!DNL Microsoft® Dynamics 365] en Azure Active Directory**

   Siga los pasos del vídeo para registrar una aplicación para [!DNL Microsoft® Dynamics 365] en Azure Active Directory.

   >[!VIDEO](https://video.tv.adobe.com/v/3444369/dynamics365integration-microsoftdynamics-apiaccess-azuread-appregistration)

   >[!NOTE]
   >
   >* Para crear la aplicación [!DNL Microsoft® Dynamics 365] conectada, seleccione **Web** como plataforma y especifique el **URI de redireccionamiento** con el siguiente formato: `https://'[server]:[port]'/libs/fd/fdm/gui/components/admin/fdmcloudservice/fdm.html`.
   >* Asegúrese de guardar el ID de cliente (también conocido como ID de aplicación) y el secreto de cliente para referencia futura.

## Conectar Forms a Microsoft® Dynamics 365

Una vez configurados los requisitos previos anteriores, puede continuar con la integración de Forms adaptable con Microsoft® Dynamics 365. Para enviar datos a Microsoft® Dynamics 365 al enviar el formulario, siga los siguientes pasos:

[&#x200B;1. Configurar el servicio en la nube de Microsoft Dynamics](#1-configure-cloud-service-configuration-for-microsoft-dynamics)

[&#x200B;2. Crear un modelo de datos de formulario (FDM)](#2-create-form-data-model-fdm)

### &#x200B;1. Configurar el servicio en la nube de Microsoft Dynamics

>[!VIDEO](https://video.tv.adobe.com/v/3444370/cloudconfiguration-dataintegration-adobeexperiencemanager-aemforms-microsoftdynamics)

Realice los siguientes pasos para configurar el servicio en la nube [!DNL Microsoft® Dynamics 365]:

1. Vaya a **[!UICONTROL Herramientas]** ![martillo](assets/hammer.png) > **[!UICONTROL Cloud Services]** > **[!UICONTROL Fuentes de datos]** en [!DNL AEM Forms] instancia de autor,.

   ![Seleccionar Source de datos de nube](/help/forms/assets/dynamics-data-source.png)
1. Seleccione un contenedor de configuración. La configuración se almacena en el contenedor de configuración seleccionado.
1. Haga clic en **[!UICONTROL Crear]**.

   ![Crear configuración de nube](/help/forms/assets/dynamics-select-configuration.png)

   Aparece el asistente de configuración **Crear configuración de Source de datos**.

   ![Asistente para crear la configuración de Data Source](/help/forms/assets/dynamics-create-data-configuration.png)

1. Especifique **[!UICONTROL Title]**, **[!UICONTROL Name]** y seleccione **[!UICONTROL Service Type]** como **servicio OData**.
1. Haga clic en **[!UICONTROL Siguiente]**. Aparecerá la ficha **Autenticación**.

   ![Ficha de autenticación](/help/forms/assets/dynamics-authentication-tab.png)

1. Especifique el valor para el campo **[!UICONTROL Raíz del servicio]**.

   Vaya a su instancia de Dynamics en el **Centro de administración de Power Platform** y vaya a [Recursos para desarrolladores](https://docs.microsoft.com/es-es/powerapps/developer/data-platform/view-download-developer-resources) para ver el valor de la **Raíz del servicio**. El extremo **Web API** representa el valor **Service Root** para la instancia de Dynamics que desea integrar con Forms adaptable. La dirección URL **Raíz del servicio** tiene el siguiente formato: `https://<tenant-name>.dynamics.com/api/data/v9.1/`

   ![Campo raíz de servicio](/help/forms/assets/dynamics-service-root.png)

1. Seleccione el **[!UICONTROL Tipo de autenticación]** como **OAuth2.0**.
1. Especifique **ID de cliente** (denominado como ID de aplicación) y **Secreto de cliente** para la aplicación conectada.
Puede recuperar **Client ID** y **Client Secret** de la aplicación de Azure Active Directory.

   ![ID de cliente y secreto de cliente](/help/forms/assets/dynamics-azure-app-resgistration.png)

1. Especifique lo siguiente en los campos **[!UICONTROL URL de OAuth]**, **[!UICONTROL Actualizar URL del token]** y **[!UICONTROL URL del token de acceso]**.
Puede recuperar la **[!UICONTROL URL de OAuth]**, la **[!UICONTROL URL del token de actualización]** y la **[!UICONTROL URL del token de acceso]** desde la sección **Extremos** de su aplicación de Azure Active Directory.

   ![Extremos de aplicación de Azure](/help/forms/assets/dynamics-azure-app-endpoints.png)

1. Especifique `openid` en el campo **[!UICONTROL Ámbito de autorización]** para el proceso de autorización en [!DNL Microsoft® Dynamics 365].
1. Especifique la URL de la instancia de Dynamics en el campo **[!UICONTROL Recurso]** para configurar [!DNL Microsoft® Dynamics 365] con un modelo de datos de formulario (FDM).
Puede copiar la **URL del entorno** desde el **Centro de administración de Power Platform** o derivar la URL de la instancia de Dynamics mediante la URL **Raíz del servicio**. La dirección URL del recurso tiene el siguiente formato: `https://<tenant-name>.dynamics.com`.

   ![Campo de recursos de aplicación avanzada](/help/forms/assets/dynamics-resource-field.png)

1. Inicie sesión con sus credenciales de [!DNL Microsoft® Dynamics 365] y haga clic en Aceptar para permitir que la configuración del servicio en la nube se conecte al servicio de [!DNL Microsoft® Dynamics 365]. Si la conexión se ha realizado correctamente, se le redirigirá a la página de configuración del servicio en la nube de [!DNL Microsoft® Dynamics 365], la cual mostrará un mensaje de éxito.
1. Seleccione **[!UICONTROL Crear]** para guardar la configuración.

### &#x200B;2. Crear un modelo de datos de formulario (FDM)

>[!VIDEO](https://video.tv.adobe.com/v/3444367/aemforms-adobeexperiencemanager-formdatamodel--dataintegration-digitalforms)

Puede usar la variable crear el modelo de datos de formulario (FDM) utilizando la configuración de nube [!DNL Microsoft® Dynamics 365] creada. Siga estos pasos para crear el modelo de datos de formulario:

1. Vaya a **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Integraciones de datos]**.
   ![Crear modelo de datos de formulario](/help/forms/assets/dynamics-create-fdm.png)

1. Haga clic en **[!UICONTROL Crear]** y seleccione **[!UICONTROL Modelo de datos de formulario]**.
   ![Seleccionar el modelo de datos de formulario](/help/forms/assets/dynamics-select-fdm.png)

   Aparece el asistente **Crear modelo de datos de formulario**.
1. Haga clic en **[!UICONTROL Siguiente]**.
1. Seleccione la configuración de nube creada en la ficha **Seleccionar origen de datos**.
   ![Seleccionar configuración de nube](/help/forms/assets/dynamics-select-cloud-config.png)

1. Haga clic en el icono Editar ![Editar](assets/edit.png) para ver y configurar el modelo de datos de formulario (FDM).

A continuación, puede [configurar el modelo de datos de formulario (FDM)](/help/forms/work-with-form-data-model.md#configure-services) y utilizarlo en varios casos de uso de formularios adaptables, como:

* Rellenado previo de los formularios adaptables consultando la información de las entidades y servicios de [!DNL Microsoft Dynamics]
* invocar operaciones del servidor de [!DNL Microsoft Dynamics] definidas en un modelo de datos de formulario (FDM) que utiliza reglas de formularios adaptables;
* Escribir datos de formularios enviados a las entidades de [!DNL Microsoft Dynamics].
* Puede configurar la acción de envío del modelo de datos de formulario de un formulario adaptable para enviar datos a [!DNL Microsoft Dynamics].

A continuación, puede usar la opción [Enviar mediante el modelo de datos de formulario (FDM)](/help/forms/using-form-data-model.md) en un **formulario adaptable** para transferir datos del formulario al [!DNL Microsoft® Dynamics 365] configurado.


>[!MORELIKETHIS]
>
>* [Configuración de fuentes de datos para AEM Forms](/help/forms/configure-data-sources.md)
>* [Configuración del almacenamiento de Azure para AEM Forms](/help/forms/configure-azure-storage.md)
>  [Añadir Portal de Forms a una página de AEM Sites](/help/forms/configure-forms-portal.md)
