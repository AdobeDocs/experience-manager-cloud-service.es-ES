---
title: Configurar una acción de envío para un formulario adaptable
description: Un formulario adaptable proporciona varias acciones de envío. Una acción de envío define cómo se procesará un formulario adaptable después del envío. Puede utilizar las acciones de envío integradas o crear las suyas propias.
keywords: Obtenga información sobre cómo seleccionar la acción de envío para un formulario adaptable, conectar un formulario adaptable a una lista de SharePoint, conectar un formulario adaptable a una biblioteca de documentos de SharePoint, conectar un formulario adaptable al modelo de datos de formulario (FDM)
feature: Adaptive Forms, Edge Delivery Services
role: User, Developer
source-git-commit: c0df3c6eaf4e3530cca04157e1a5810ebf5b4055
workflow-type: tm+mt
source-wordcount: '371'
ht-degree: 22%

---


# Acciones de envío para Edge Delivery Services Forms

| Versión | Vínculo de artículo |
|---------|-----------------------------|
| AEM 6.5 | [Haga clic aquí](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-basic-authoring/configuring-submit-actions.html?lang=es) |
| AEM as a Cloud Service (componentes de base) | [Haga clic aquí](/help/forms/configuring-submit-actions.md) |
| AEM as a Cloud Service (componentes principales) | [Haga clic aquí](/help/forms/configure-submit-actions-core-components.md) |
| AEM as a Cloud Service (Edge Delivery Services) | Este artículo |

Las acciones de envío definen qué sucede cuando un usuario envía un formulario, como el almacenamiento de datos, la activación de flujos de trabajo o la integración con sistemas de terceros. El tipo de acciones de envío que se pueden configurar depende del método de creación utilizado para crear Edge Delivery Services Forms.

Puede crear Edge Delivery Services Forms con [Universal Editor](/help/edge/docs/forms/universal-editor/overview-universal-editor-for-edge-delivery-services-for-forms.md) o con la creación de [Forms basado en documentos](/help/edge/docs/forms/overview.md), y configurar los formularios con diferentes acciones de envío según corresponda.

## Acciones de envío para Forms creadas en el editor universal

[Forms adaptable creado en el editor universal](/help/edge/docs/forms/universal-editor/create-forms.md) admite las siguientes acciones de envío:

* [Enviar correo electrónico](/help/forms/configure-submit-action-send-email.md)
* [Invocar un flujo de Power Automate](/help/forms/forms-microsoft-power-automate-integration.md)
* [Enviar a SharePoint](/help/forms/configure-submit-action-sharepoint.md)
* [Invocar Workfront Fusion](/help/forms/submit-adaptive-form-to-workfront-fusion.md)
* [Enviar mediante el modelo de datos de formulario (FDM)](/help/forms/using-form-data-model.md)
* [Enviar a Azure Blob Storage](/help/forms/configure-submit-action-azure-blob-storage.md)
* [Enviar a extremo REST](/help/forms/configure-submit-action-restpoint.md)
* [Enviar a OneDrive](/help/forms/configure-submit-action-onedrive.md)
* [Invocar un flujo de trabajo de AEM](/help/forms/configure-submit-action-workflow.md)
* [Enviar a Marketo Engage](/help/forms/submit-adaptive-form-to-marketo-engage.md)
* [Enviar a Adobe Experience Platform (AEP)](/help/forms/aem-forms-aep-connector.md)
* [Enviar a hoja de cálculo](/help/forms/forms-submission-service.md)

<!--You can also submit an Adaptive Form in the Universal Editor to other storage or CRM integrations:

* [Connect Adaptive Form to Salesforce](/help/forms/aem-forms-salesforce-integration.md)
* [Connect an Adaptive Form to Microsoft&reg; Dynamics OData](/help/forms/ms-dynamics-odata-configuration.md)-->

Puede configurar la acción de envío para los formularios creados en el editor universal mediante la pestaña **Envío** de la extensión **Editar propiedades del formulario**.

<!--**How to Configure Submit Action for Forms authored in Universal Editor?**
You can configure the submit action for forms created in the Universal Editor using the **Submission** tab of the **Edit Form Properties** extension.

![Form properties icon](/help/forms/assets/ue-form-properties-icon.png)

![Universal Editor Form Properties](/help/forms/assets/ue-form-properties.png)-->

>[!NOTE]
>
> * Si no ve el icono **Editar propiedades de formulario** en la interfaz de Universal Editor, habilite la extensión **Editar propiedades de formulario** en Extension Manager.
> * Consulte el artículo [Aspectos destacados de las funciones de Extension Manager](https://developer.adobe.com/uix/docs/extension-manager/feature-highlights/#enablingdisabling-extensions) para obtener información sobre cómo habilitar o deshabilitar extensiones en el editor universal.

## Acciones de envío para Forms basado en documentos

Forms basado en documentos admite el envío solo a hojas de cálculo. Para aprender a configurar la hoja de cálculo para recibir los datos enviados, consulte las instrucciones del artículo [Configurar las hojas de cálculo de Google o los archivos de Microsoft Excel para empezar a aceptar datos](/help/edge/docs/forms/submit-forms.md).

## Véase también {#see-also}

{{af-submit-action}}

