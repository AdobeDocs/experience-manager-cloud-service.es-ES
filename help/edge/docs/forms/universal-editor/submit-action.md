---
title: Configurar una acción de envío para un formulario adaptable
description: Un formulario adaptable proporciona varias acciones de envío. Una acción de envío define cómo se procesará un formulario adaptable después del envío. Puede utilizar las acciones de envío integradas o crear las suyas propias.
keywords: Obtenga información sobre cómo seleccionar la acción de envío para un formulario adaptable, conectar un formulario adaptable a una lista de SharePoint, conectar un formulario adaptable a una biblioteca de documentos de SharePoint, conectar un formulario adaptable al modelo de datos de formulario (FDM)
feature: Adaptive Forms, Edge Delivery Services
role: User, Developer
exl-id: beee9be7-8215-496b-9fb9-61fba000a055
source-git-commit: bf35f847f6f00d21915dfedb10cf38ea74344988
workflow-type: tm+mt
source-wordcount: '414'
ht-degree: 50%

---

# Acción de envío de un formulario adaptable

| Versión | Vínculo de artículo |
|---------|-----------------------------|
| AEM 6.5 | [Haga clic aquí](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-basic-authoring/configuring-submit-actions.html?lang=es) |
| AEM as a Cloud Service (componentes de base) | [Haga clic aquí](/help/forms/configuring-submit-actions.md) |
| AEM as a Cloud Service (componentes principales) | [Haga clic aquí](/help/forms/configure-submit-actions-core-components.md) |
| AEM as a Cloud Service (Edge Delivery Services) | Este artículo |


El envío de formularios es el paso final crucial del recorrido del usuario: es donde se procesan los datos recopilados y se realizan las acciones. Este documento proporciona una guía completa para configurar y administrar las acciones de envío de formularios adaptables en el editor universal.

## Lo que aprenderá

Al final de este documento, aprenderá a:

- Configurar diferentes tipos de acciones de envío de formularios
- Configurar envíos de puntos finales REST para la integración con sistemas externos
- Configurar envíos de correos electrónicos para respuestas de formulario
- Implementar acciones de envío personalizadas para necesidades comerciales específicas
- Gestionar la validación de formularios y los escenarios de error durante el envío

## Público destinatario

Esta guía está diseñada para:

- **Desarrolladores de formularios** que implementan la lógica de envío
- **Integradores de sistemas** que conectan formularios con sistemas back-end
- **Analistas de negocios** que definen los flujos de trabajo de formularios
- **Arquitectos técnicos** que diseñan procesos de envío de formularios

## Acciones de envío para Forms creadas en el editor universal

[Forms adaptable creado en el editor universal](/help/edge/docs/forms/universal-editor/create-forms.md) admite las siguientes acciones de envío:

- [Enviar correo electrónico](/help/forms/configure-submit-action-send-email.md)
- [Invocar un flujo de Power Automate](/help/forms/forms-microsoft-power-automate-integration.md)
- [Enviar a SharePoint](/help/forms/configure-submit-action-sharepoint.md)
- [Invocar Workfront Fusion](/help/forms/submit-adaptive-form-to-workfront-fusion.md)
- [Enviar mediante el modelo de datos de formulario (FDM)](/help/forms/integrate-adaptive-form-with-fdm.md)
- [Enviar a Azure Blob Storage](/help/forms/configure-submit-action-azure-blob-storage.md)
- [Enviar a extremo REST](/help/forms/configure-submit-action-restpoint.md)
- [Enviar a OneDrive](/help/forms/configure-submit-action-onedrive.md)
- [Invocar un flujo de trabajo de AEM](/help/forms/configure-submit-action-workflow.md)
- [Enviar a Marketo Engage](/help/forms/submit-adaptive-form-to-marketo-engage.md)
- [Enviar a Adobe Experience Platform (AEP)](/help/forms/aem-forms-aep-connector.md)
- [Enviar a hoja de cálculo](/help/forms/forms-submission-service.md)

<!--You can also submit an Adaptive Form in the Universal Editor to other storage or CRM integrations:

* [Connect Adaptive Form to Salesforce](/help/forms/aem-forms-salesforce-integration.md)
* [Connect an Adaptive Form to Microsoft&reg; Dynamics OData](/help/forms/ms-dynamics-odata-configuration.md)-->

Puede configurar la acción de envío para los formularios creados en el editor universal mediante la pestaña **Envío** de la extensión **Editar propiedades del formulario**.

**¿Cómo configurar la acción de envío para Forms creada en el Editor universal?**
Puede configurar la acción de envío para los formularios creados en el editor universal mediante la pestaña **Envío** de la extensión **Editar propiedades del formulario**.

![Icono de propiedades de formulario](/help/forms/assets/ue-form-properties-icon.png)

![Propiedades de formulario de editor universal](/help/forms/assets/ue-form-properties.png)

>[!NOTE]
>
> - Si no ve el icono **Editar propiedades de formulario** en la interfaz de Universal Editor, habilite la extensión **Editar propiedades de formulario** en Extension Manager.
> - Consulte el artículo [Aspectos destacados de las funciones de Extension Manager](https://developer.adobe.com/uix/docs/extension-manager/feature-highlights/#enablingdisabling-extensions) para obtener información sobre cómo habilitar o deshabilitar extensiones en el editor universal.
