---
title: 'Flujo de trabajo de envío para la IU asociada: IC Generar salida de PDF'
description: Comprenda cómo funcionan el envío y el flujo de trabajo para la interfaz de usuario de Associate y siga un ejemplo de flujo de trabajo que genera PDF a partir de comunicaciones interactivas (IC) JSON.
products: SG_EXPERIENCEMANAGER/Cloud Service/FORMS
feature: Interactive Communication
role: User, Developer, Admin
exl-id: 9d8a33e4-e206-48e6-9daf-b15feb9c67a3
source-git-commit: 53ff71c82d35b9ec9b20b521ef469d3f0abd79df
workflow-type: tm+mt
source-wordcount: '440'
ht-degree: 0%

---

# Flujo de trabajo de envío para la IU asociada


Este artículo explica cómo funcionan el envío y el flujo de trabajo al habilitar un flujo de trabajo para la interfaz de usuario de asociado. A continuación, se explica cómo configurar un flujo de trabajo de envío. El tutorial utiliza la generación de una PDF a partir de la carga útil de la comunicación interactiva (IC) como ejemplo; puede adaptar los pasos para otros tipos de flujo de trabajo.

<!--
## Submission and workflow behavior {#submission-and-workflow-behavior}

When you enable **Configure Workflow for Update** for an Associate UI, submissions from the Associate UI can trigger an AEM workflow. The following explains where workflows run, who uses which environment, and how to plan for data and access.

### Where workflows run

AEM workflows always run on the **Author** instance. It does not matter whether the person submitting is an author or an associate—the workflow runs on Author. Plan your user groups and where you store workflow data with this in mind.

### Where associates use the Associate UI

Customer-facing associates use the Associate UI on the **Publish** instance only. You publish the Interactive Communication and expose the Associate UI through your Publish environment (for example, via your application or dispatcher). Associates do not use the Author instance. For step-by-step integration and how to invoke the Associate UI on the Publish instance, see [Integrate Associate UI in Your Application](/help/forms/interactive-communication/invoke-associate-ui.md).

### When an author submits from the Author instance

Authors can open the Associate UI on the Author instance—for example, to test the Interactive Communication or to submit on behalf of a customer. When they submit, the request is handled on Author and the workflow runs there. For this to work, the author must be in both **forms-associates** (to access the Associate UI) and **workflow-users** (to run the workflow).

### When an associate submits from the Publish instance

Associates open the Associate UI on the Publish instance, using the integration you set up. When they submit, the submission is sent to the Author instance and the workflow runs on Author. Associates sign in on Publish (for example, via [Microsoft Entra ID](https://www.microsoft.com/en-us/security/business/identity-access/microsoft-entra-id)) and do not need access to Author. To set up how associates open the Associate UI on Publish, see [Integrate Associate UI in Your Application](/help/forms/interactive-communication/invoke-associate-ui.md).
-->

## Configuración de un flujo de trabajo de envío

Los siguientes pasos muestran cómo crear un flujo de trabajo que se ejecute cuando los usuarios envían desde la interfaz de usuario de Associate. Aquí utilizamos **procesando la CI en PDF** como ejemplo, con el paso de salida **IC Render PDF Output** listo para usar. Cuando un usuario realiza el envío desde la interfaz de usuario asociada, la carga útil se envía al flujo de trabajo; este paso utiliza **communicationDom** (IC-JSON) desde la carga para producir el PDF.

### Estructura de carga útil

El flujo de trabajo recibe una carga útil JSON. El campo **communicationDom** contiene el IC-JSON utilizado para la generación de PDF. El paso **IC Render PDF Output** lo usa como entrada de plantilla.

| Campo | Descripción |
|-------|-------------|
| communicationDom | IC-JSON para la generación de PDF |
| auditMetadata | Información de auditoría |
| submitData | Datos de formulario enviados (JSON) |
| prefillData | Datos de relleno previo (JSON) |
| referer, cookies, queryString, clientIP, userAgent, formSubmitter | Solicitar metadatos |

### Creación del modelo del flujo de trabajo

1. **Básico:** Cree un modelo de flujo de trabajo (por ejemplo, agregue un flujo de trabajo como **pdfrenderworkflow**).

   ![Ficha básica del modelo de flujo de trabajo](/help/forms/assets/associate-ui-add-workflow.png)

1. **Variables:** Agregue variables que coincidan con la carga útil y el paso: **communicationDom** (JSON), **auditMetadata** (JSON), **outputDocument** (Document).

   ![Variables de flujo de trabajo](/help/forms/assets/associate-ui-add-variables.png)

1. **Paso:** Agregue el paso **IC Render PDF Output**.
   ![Agregar paso de flujo de trabajo](/help/forms/assets/associate-ui-add-step.png)

1. En su ficha **Input**, establezca **Select template (JsonObject)** en **Variable** → **communicationDom**. Guarde el paso y el modelo.

   ![Salida de PDF de procesamiento IC — ficha Entrada](/help/forms/assets/associate-ui-input-variable.png)

1. En su ficha **Output**, establezca **Select template (JsonObject)** en **Variable** → **communicationDom**. Guarde el paso y el modelo.

   ![Variables de flujo de trabajo y lienzo](/help/forms/assets/assocaite-ui-output-variable.png)

### Vinculación del flujo de trabajo a la IU asociada

En [Habilitar y configurar la interfaz de usuario asociada](/help/forms/interactive-communication/enable-configure-associate-ui.md), habilite la vista asociada y en **Flujo de trabajo** establezca **Configurar flujo de trabajo para actualización** en Activado y seleccione este modelo de flujo de trabajo. Publique la CI y [integre la interfaz de usuario asociada](/help/forms/interactive-communication/invoke-associate-ui.md) para que los envíos entren en déclencheur en este flujo de trabajo.

![Configuración de comunicación interactiva - Configuración del flujo de trabajo para la interfaz de usuario asociada](/help/forms/assets/associate-ui-configure-workflow.png)

Cuando **Externalizar el almacenamiento de datos del flujo de trabajo** esté habilitado, configure el externalizador para que los datos del flujo de trabajo se almacenen en su almacenamiento externo (por ejemplo, Azure). Consulte [Externalizar datos de flujo de trabajo](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/forms/create-aem-workflow/externalize-workflow.html).

## Ver también

- [Asociar interfaz de usuario en el editor de comunicaciones interactivas](/help/forms/interactive-communication/associate-ui-in-interactive-communication-editor.md)
- [Habilitar y configurar la interfaz de usuario asociada para comunicaciones interactivas](/help/forms/interactive-communication/enable-configure-associate-ui.md)
- [Integración de la interfaz de usuario asociada en la aplicación](/help/forms/interactive-communication/invoke-associate-ui.md)
- [Externalización de datos de flujo de trabajo](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/forms/create-aem-workflow/externalize-workflow.html)

