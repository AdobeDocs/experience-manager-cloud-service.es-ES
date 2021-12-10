---
title: Envío de un acuse de recibo de envío de formulario por correo electrónico
seo-title: Sending a form submission acknowledgement via email
description: AEM Forms permite configurar la acción de envío por correo electrónico que envía un acuse de recibo a un usuario al enviar el formulario.
seo-description: AEM Forms allows you to configure the email Submit Action that sends an acknowledgement to a user on submitting the form.
uuid: c80b1ef4-8fe3-48e0-8fc6-3032dc022a38
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
discoiquuid: 574de3d5-69ba-4e2f-a8ab-c59f357e4386
docset: aem65
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '367'
ht-degree: 0%

---


# Envío de un acuse de recibo de envío de formulario por correo electrónico {#sending-a-form-submission-acknowledgement-via-email}

## Envío de datos del formulario adaptable {#adaptive-form-data-submission}

Forms adaptable proporciona varios [Enviar acciones](configuring-submit-actions.md) flujos de trabajo para enviar los datos del formulario a diferentes extremos.

Por ejemplo, la variable **[!UICONTROL Enviar correo electrónico]** Enviar acción envía un correo electrónico cuando se envía correctamente un formulario adaptable. También se puede configurar para que envíe los datos del formulario y el PDF en el correo electrónico.

Este artículo detalla los pasos para habilitar la acción Correo electrónico en un formulario adaptable y las diferentes configuraciones que proporciona.

>[!NOTE]
>
>También puede usar la variable **[!UICONTROL Enviar PDF por correo electrónico]** para enviar el formulario completado por correo electrónico como archivo adjunto de PDF. Las opciones de configuración disponibles para esta acción son las mismas que las disponibles para la **[!UICONTROL Enviar correo electrónico]** acción. La acción PDF de correo electrónico solo está disponible para Forms adaptable basado en XFA

## Enviar acción de correo electrónico {#email-action}

La acción Enviar correo electrónico permite a un autor enviar correos electrónicos automáticamente a uno o varios destinatarios cuando el envío de un formulario adaptable se haya realizado correctamente.

<!-- >>[!NOTE]
>
>To use the Send email action, you need to configure the AEM mail service as described in [Configuring the mail service](/help/sites-administering/notification.md#configuring-the-mail-service).

### Enabling Send email action on an Adaptive Form {#enabling-email-action-on-an-adaptive-form}

1. Open an Adaptive Form in **[!UICONTROL edit]** mode.

1. In the **[!UICONTROL Content]** tab, tap **[!UICONTROL Form Container]** and tap ![configure](assets/configure-icon.svg) to view the Adaptive Form properties.  

1. In the **[!UICONTROL Submission]** section, select **[!UICONTROL Send email]** from the **[!UICONTROL Submit Action]** drop-down list.  

   ![Submit Actions](assets/submission-actions.png)

1. Specify valid email IDs in the **[!UICONTROL To]**, **[!UICONTROL CC]**, and **[!UICONTROL BCC]** fields.

   Specify the subject and the body of the email in the **[!UICONTROL Subject]** and **[!UICONTROL Email Template]** fields, respectively.

   You can also specify variable placeholders in the fields, in which case, the values of the fields are processed when the form is successfully submitted by an end user. For more information, see [Using Adaptive Form field names to dynamically create email content](form-submission-receipt-via-email.md#p-using-adaptive-form-field-names-to-dynamically-create-email-content-p).

   Select **[!UICONTROL Include attachments]** if the form includes file attachments and you want to attach these files in the email.

   >[!NOTE]
   >
   >If you choose the **[!UICONTROL Send PDF via Email]** option, you must select the Include attachments option.

1. Click ![save](assets/save_icon.svg) to save the changes. -->

### Uso de nombres de campo de formulario adaptable para crear contenido de correo electrónico de forma dinámica {#using-adaptive-form-field-names-to-dynamically-create-email-content}

Los nombres de campo de un formulario adaptable se denominan marcadores de posición que se sustituyen por el valor de ese campo después de que un usuario envíe el formulario.

En el **[!UICONTROL Enviar correo electrónico]** , puede utilizar marcadores de posición que se procesen cuando se realice la acción. Significa que los encabezados del correo electrónico (como **[!UICONTROL Hasta]**, **[!UICONTROL CC]**, **[!UICONTROL CCO]**, **[!UICONTROL Asunto]**) se generan cuando el usuario envía el formulario.

Para definir un marcador de posición, especifique `${<field name>}` en un campo después de seleccionar **[!UICONTROL Enviar correo electrónico]** como Acción de envío.

Por ejemplo, si el formulario contiene la variable **[!UICONTROL Dirección de correo electrónico]** campo, con nombre `email_addr`, para capturar el ID de correo electrónico de un usuario, puede especificar lo siguiente en la sección **[!UICONTROL Hasta]**, **[!UICONTROL CC]** o **[!UICONTROL CCO]** campos.

`${email_addr}`

Cuando un usuario envía el formulario, se envía un correo electrónico al ID de correo electrónico introducido en la variable `email_addr` del formulario.

>[!NOTE]
>
>Puede encontrar el nombre de un campo en la **[!UICONTROL Editar]** para el campo .

Los marcadores de posición de variables también se pueden usar en la variable **[!UICONTROL Asunto]** y **[!UICONTROL Plantilla de correo electrónico]** campos.

Por ejemplo:

`Hi ${first_name} ${last_name},`

`Your form has been received by our department. It usually takes ten business days to process the request.`

`Regards`

`Administrator`

>[!NOTE]
>
>Los campos de los paneles repetibles no se pueden usar como marcadores de posición de variables.

