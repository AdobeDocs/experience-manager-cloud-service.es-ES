---
title: Acciones de envío
description: Configure acciones de envío para un formulario adaptable.
feature: Edge Delivery Services
role: Admin, Architect, Developer
exl-id: beee9be7-8215-496b-9fb9-61fba000a055
source-git-commit: 0c6f024594e1b1fd98174914d2c0714dffecb241
workflow-type: tm+mt
source-wordcount: '735'
ht-degree: 100%

---

# Acción de envío de un formulario adaptable

Una acción de envío especifica el destino de los datos recopilados mediante un formulario adaptable. El proceso de envío comienza cuando el usuario hace clic en el botón **[!UICONTROL Enviar]** del formulario. AEM Forms ofrece dos tipos de acciones de envío que se describen a continuación, y le permite crear y utilizar acciones de envío personalizadas para satisfacer sus necesidades específicas. Las acciones de envío listas para usar son las siguientes:

<!--To define a Submit Action for an Adaptive Form, you use the Properties dialog of the **Adaptive Form block** in the **Editor**-->

* [Enviar al punto final REST](#rest-endpoint-submission-ue)
* [Enviar correo electrónico](#email-submission-ue)


### Enviar al punto final REST {#rest-endpoint-submission-ue}

La acción Enviar al punto final REST se utiliza para enviar los datos de formulario enviados a un punto final REST especificado. El punto final puede pertenecer a un servidor interno donde se aloja el formulario o a un servidor externo mediante una ruta relativa o una ruta absoluta. Para enviar datos al servidor de AEM que aloja el formulario, utilice una ruta relativa correspondiente a la ruta raíz del servidor de AEM. Por ejemplo, `/content/forms/af/SampleForm.html`. Para enviar datos a cualquier otro servidor, utilice la ruta absoluta.

<!--Configuring the Submit Action to REST Endpoint for Adaptive Forms offers several benefits such as:  
* It facilitates seamless integration of form data with external systems and services via RESTful APIs.  
* Offers flexibility in managing data submissions from Adaptive Forms, accommodating dynamic and complex data structures.  
* Allows dynamic mapping of form fields to parameters within the REST endpoint URL, enabling adaptable and customizable data submissions.
-->



Para configurar un punto final REST:

1. Abra el formulario adaptable en el **[!UICONTROL Editor]**.
1. Seleccione **[!UICONTROL Bloque de formulario adaptable]**.
1. Haga clic en el icono de propiedades ![propiedades](/help/forms/assets/Smock_Properties_18_N.svg).
1. Seleccione **[!UICONTROL Enviar a un punto final REST]** en la lista desplegable **[!UICONTROL Enviar acción]**.
1. Especifique la URL de punto final REST.
1. También puede **Habilitar la petición POST** y proporcionar una URL para publicar la solicitud. 

![Habilitar petición de publicación para formularios adaptables](/help/forms/assets/enable-post-request-ue.png)

>[!NOTE]
>
> * Para enviar datos a un servidor interno, proporcione la ruta del recurso. Los datos se publican en la ruta del recurso. Por ejemplo, `/content/restEndPoint`. Para esas peticiones POST se utiliza la información de autenticación de la solicitud de envío.
> * Para enviar datos a un servidor externo, proporcione una URL. El formato de la URL es el siguiente `https://host:port/path_to_rest_end_point`. Asegúrese de configurar la ruta para controlar la petición POST de forma anónima.

### Enviar correo electrónico {#email-submission-ue}

La acción de envío Enviar correo electrónico le permite enviar un correo electrónico a uno o varios destinatarios cuando el formulario se haya enviado correctamente. Esta acción de envío le permite crear un correo electrónico que incluya datos de formulario en un formato predefinido. Por ejemplo, considere la siguiente plantilla en la que el nombre del cliente, la dirección de envío, el nombre del estado y el código postal se recuperan de los datos del formulario enviado. [Obtenga más información sobre las plantillas de correo electrónico en Formularios adaptables](/help/forms/html-email-templates-in-adaptive-forms.md). Algunas ventajas de configurar un formulario adaptable con la acción de envío Enviar correo electrónico son las siguientes:

1. Permite una comunicación rápida, ya que los datos del formulario se envían directamente a los destinatarios de correo electrónico designados.
1. Ayuda a optimizar el flujo de trabajo al integrar directamente los envíos de formularios en las notificaciones por correo electrónico.
1. Ayuda a las organizaciones a personalizar el contenido del correo electrónico, lo que lo hace adecuado para necesidades de comunicación específicas.

![Propiedades de formulario adaptable en el editor universal](/help/forms/assets/submit-actions-ue.png)


Para configurar una acción de envío como un correo electrónico para el envío del formulario:

1. Abra el formulario adaptable en el **Editor**.
1. Seleccione su **[!UICONTROL bloque de formulario adaptable]**.
1. Haga clic en el icono de propiedades ![propiedades](/help/forms/assets/Smock_Properties_18_N.svg).
1. Seleccione la opción **[!UICONTROL Enviar correo electrónico]** en la lista desplegable **[!UICONTROL Enviar acción]**.
1. Una vez seleccionada la opción Enviar correo electrónico, puede configurar las siguientes propiedades como se muestra en la siguiente imagen.

<table>
  <thead>
    <tr>
      <th>Imagen</th>
      <th>Propiedad</th>
      <th>Descripción</th>
    </tr>
  </thead>
  <tbody>
    <tr>
    <td rowspan="7"><img src="/help/forms/assets/email-config-ue.png" alt="Configuración de correo electrónico"></td> 
    <td><b>De</td>
    <td>Especifique la dirección de correo electrónico del remitente.</td>
    </tr>
    <tr>
      <td><b>Para</td>
      <td>Especifique los destinatarios principales del correo electrónico; se pueden añadir varias direcciones de correo electrónico separadas por comas.</td>
    </tr>
    <tr>
      <td><b>CC</td>
      <td>Especifique los destinatarios que deben recibir una copia (CC) del correo electrónico.</td>
    </tr>
    <tr>
      <td><b>CCO</td>
      <td>Especifique los destinatarios que deben recibir una copia oculta (CCO) del correo electrónico.</td>
    </tr>
    <tr>
      <td><b>Asunto</td>
      <td>Especifique la línea de asunto del correo electrónico.</td>
    </tr>
    <tr>
      <td><b>Usar plantilla externa</td>
      <td>Habilita el uso de una plantilla de correo electrónico externa para dar formato al contenido del correo electrónico. Proporcione la dirección URL o la ruta a la plantilla externa para integrar una plantilla de correo electrónico previamente diseñada alojada en la carpeta de AEM Assets.</td>
    </tr>
    <tr>
      <td><b>Incluir archivo adjunto</td>
      <td>Especifica si los datos de formulario enviados deben incluir un archivo adjunto enviado a través del formulario en el correo electrónico. Los formatos de archivo adjunto compatibles son PDF, XML y JSON.</td>
    </tr>
  </tbody>
</table>






<!--
        
        * **From**: The email address of the sender.
        * **To**: Specify the primary recipients of the email, multiple email addresses can be added, separated by commas.
        * **CC**: Specify the recipients who should receive a carbon copy (CC) of the email.
        * **BCC**: Specify the recipients who should receive a blind carbon copy (BCC) of the email.
        * **Subject**: Specify the subject line of the email.
        * **Use External Template**: Enables the use of an external email template for formatting the email content. Provide the URL or path to the External template path to integrate a pre-designed email template hosted in your AEM Assets folder.
        * **Include Attachment**: Specifies whether the submitted form data should include an attachment submitted through the form in the email.

    {width=50%,height=50%}![Enable post request for adaptive forms](/help/forms/assets/email-config-ue.png)

-->

## Mostrar un mensaje de agradecimiento personalizado después del envío del formulario {#submit-action-message-ue}

La opción En envío le ayuda a configurar un mensaje de acción de envío al enviar el formulario adaptable. Para configurar un mensaje de acción de envío para el formulario:

1. Abra el formulario adaptable en el **Editor**.
1. Seleccione su **[!UICONTROL bloque de formulario adaptable]**.
1. Haga clic en el icono de propiedades ![propiedades](/help/forms/assets/Smock_Properties_18_N.svg).
1. Al hacer clic, verá la siguiente opción:
   * **[!UICONTROL En envío]**: le ayuda a personalizar un mensaje que se mostrará cuando se envíe un formulario. De forma predeterminada, se muestra un mensaje personalizado &quot;Gracias por enviar el formulario&quot; al usuario cuando se envía un formulario correctamente.
También puede personalizar el mensaje de agradecimiento al enviar el formulario, seleccionando la opción para **[!UICONTROL Mostrar mensaje]**, y añadir o editar el mensaje en el **Editor** de texto enriquecido.


## Véase también

{{universal-editor-see-also}}

