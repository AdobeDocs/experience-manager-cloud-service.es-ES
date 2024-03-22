---
Title: How to send an email on submission of an Adaptive Form?
Description: Explore the process to set up email notifications when submitting an Adaptive Form.
keywords: cómo enviar un correo electrónico para un formulario adaptable, acción de envío de correo electrónico, correo electrónico del formulario adaptable, correo electrónico de envío de formulario, guía para enviar correo electrónico
feature: Adaptive Forms, Core Components
source-git-commit: f1db04e6cd1f78c1530aefd29f5f036ca5e70873
workflow-type: ht
source-wordcount: '437'
ht-degree: 100%

---


# Configuración de la acción de envío Enviar correo electrónico para un formulario adaptable

La acción de envío **[!UICONTROL Enviar correo electrónico]** le permite enviar un correo electrónico a uno o varios destinatarios cuando el formulario se haya enviado correctamente. Esta acción de envío le permite crear un correo electrónico que incluya datos de formulario en un formato predefinido. Por ejemplo, considere la siguiente plantilla en la que el nombre del cliente, la dirección de envío, el nombre del estado y el código postal se recuperan de los datos del formulario enviado:


    ```
    Hola, ${customer_Name},
    
    La siguiente se establece como su dirección de envío predeterminada:
    ${customer_Name},
    ${customer_Shipping_Address},
    ${customer_State},
    ${customer_ZIPCode}
    
    Un saludo,
    WKND
    
    ```


## Ventajas

Algunas ventajas de configurar un formulario adaptable con la acción de envío Enviar correo electrónico son las siguientes:

* Permite una comunicación rápida, ya que los datos del formulario se envían directamente a los destinatarios de correo electrónico designados.
* Ayuda a optimizar el flujo de trabajo al integrar directamente los envíos de formularios en las notificaciones por correo electrónico.
* Ayuda a las organizaciones a personalizar el contenido del correo electrónico, lo que lo hace adecuado para necesidades de comunicación específicas.

## Configuración de la acción de envío Enviar correo electrónico {#steps-to-configure-send-email-submit-action}

Para configurar la acción de envío:

1. Abra el Explorador de contenido y seleccione el componente **[!UICONTROL Contenedor de guía]** del formulario adaptable.
1. Haga clic en el icono de propiedades del contenedor de guía ![Propiedades de guía](/help/forms/assets/configure-icon.svg). Se abre el cuadro de diálogo Contenedor de formulario adaptable.
1. Abra la pestaña **[!UICONTROL Envío]**.
1. En la lista desplegable **[!UICONTROL Acción de envío]** seleccione la opción **[!UICONTROL Enviar correo electrónico]**.

   ![Configuración de la acción de Enviar correo electrónico](/help/forms/assets/send-email-action-configuration.gif)
1. Especifique el ID de correo electrónico del remitente en el cuadro de texto **[!UICONTROL De]**.
1. Añada el ID de correo electrónico del destinatario en el cuadro de texto **[!UICONTROL Para]**. Para añadir varios destinatarios, haga clic en el botón **[!UICONTROL Añadir]**.
1. [Opcional] Añada el destinatario para CC y CCO haciendo clic en el botón **[!UICONTROL Añadir]**.
1. Especifique una línea de asunto en el cuadro de texto **[!UICONTROL Asunto]**.
1. Añada una plantilla de correo electrónico para configurar la acción de envío Enviar correo electrónico.
   * Puede especificar la ruta a la plantilla de correo electrónico externa guardada en los recursos de AEM mediante la opción **[!UICONTROL Plantilla externa]**.
   * También puede añadir una plantilla de correo electrónico personalizada para el envío del formulario en el cuadro de texto **[!UICONTROL Plantilla de correo electrónico]**.
1.  [Opcional] La acción de envío **[!UICONTROL Enviar correo electrónico]** proporciona la opción de incluir archivos adjuntos y un [documento de registro (DoR)](generate-document-of-record-core-components.md) con el correo electrónico.
1. Haga clic en **[!UICONTROL Listo]**.

## Prácticas recomendadas {#best-practices}

* Se recomienda que el contenido del correo electrónico sea claro y conciso. Los usuarios deben comprender el propósito del correo electrónico y las acciones que deben tomar.
* Es crucial que todos los campos de formulario tengan nombres de elemento únicos, incluso si se colocan en paneles diferentes dentro de un formulario adaptable.
* Cuando se utiliza AEM as a Cloud Service, el correo electrónico saliente requiere un cifrado. De forma predeterminada, la funcionalidad del correo electrónico saliente está deshabilitada. Para habilitarlo, envíe un ticket de asistencia a [Solicitar acceso](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/development-guidelines.html?lang=es#sending-email).


## Artículos relacionados

{{af-submit-action}}


