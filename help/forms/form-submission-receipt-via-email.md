---
title: Enviar una confirmación de envío de formulario por correo electrónico
description: AEM Forms permite configurar una acción de envío por correo electrónico que envía una confirmación a un usuario al enviar el formulario.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
docset: aem65
source-git-commit: 5ad33f0173afd68d8868b088ff5e20fc9f58ad5a
workflow-type: tm+mt
source-wordcount: '366'
ht-degree: 94%

---


# Enviar una confirmación de envío de formulario por correo electrónico {#sending-a-form-submission-acknowledgement-via-email}

## Enviar datos de formularios adaptables {#adaptive-form-data-submission}

Los formularios adaptables proporcionan varios flujos de trabajo de [acciones de envío](configuring-submit-actions.md) predeterminados para enviar los datos del formulario a diferentes extremos.

Por ejemplo, la acción de envío **[!UICONTROL Enviar correo electrónico]** envía un correo electrónico cuando se envía correctamente un formulario adaptable. También se puede configurar el envío de los datos del formulario y el PDF en el correo electrónico.

Este artículo detalla los pasos para habilitar la acción Enviar por correo electrónico en un formulario adaptable y las diferentes configuraciones que proporciona.

>[!NOTE]
>
>También puede usar la opción **[!UICONTROL Enviar PDF por correo electrónico]** para enviar el formulario completado por correo electrónico como archivo adjunto PDF. Las opciones de configuración disponibles para esta acción son las mismas que las disponibles para la acción **[!UICONTROL Enviar correo electrónico]**. La acción Enviar PDF por correo electrónico solo está disponible para formularios adaptables basados en XFA.

## Acción Enviar correo electrónico {#email-action}

La acción Enviar correo electrónico permite a un autor enviar correos electrónicos automáticamente a uno o varios destinatarios cuando el envío de un formulario adaptable se realiza correctamente.

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

### Usar nombres de campo de formulario adaptable para crear contenido de correo electrónico de forma dinámica {#using-adaptive-form-field-names-to-dynamically-create-email-content}

Los nombres de campo de un formulario adaptable se denominan marcadores de posición y se reemplazan por el valor de ese campo una vez que un usuario envía el formulario.

En la acción **[!UICONTROL Enviar correo electrónico]**, puede utilizar marcadores de posición que se procesan cuando se realiza la acción. Eso significa que los encabezados del correo electrónico (como **[!UICONTROL Para]**, **[!UICONTROL CC]**, **[!UICONTROL CCO]** y **[!UICONTROL Asunto]**) se generan cuando el usuario envía el formulario.

Para definir un marcador de posición, especifique `${<field name>}` en un campo después de seleccionar **[!UICONTROL Enviar correo electrónico]** como acción de envío.

Por ejemplo, si el formulario contiene el campo **[!UICONTROL Dirección de correo electrónico]**, denominado `email_addr`, para capturar el ID de correo electrónico de un usuario, puede especificar lo siguiente en los campos **[!UICONTROL Para]**, **[!UICONTROL CC]** o **[!UICONTROL CCO]**.

`${email_addr}`

Cuando un usuario envía el formulario, se envía un correo electrónico al ID de correo electrónico introducido en el campo `email_addr` del formulario.

>[!NOTE]
>
>Puede encontrar el nombre de un campo en el cuadro de diálogo **[!UICONTROL Editar]** del campo.

Los marcadores de posición de variables también se pueden usar en los campos **[!UICONTROL Asunto]** y **[!UICONTROL Plantilla de correo electrónico]**.

Por ejemplo:

`Hi ${first_name} ${last_name},`

`Your form has been received by our department. It usually takes ten business days to process the request.`

`Regards`

`Administrator`

>[!NOTE]
>
>Los campos de los paneles repetibles no se pueden usar como marcadores de posición variables.

