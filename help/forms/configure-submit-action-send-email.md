---
Title: How to send an email on submission of an Adaptive Form?
Description: Explore the process to set up email notifications when submitting an Adaptive Form.
keywords: Cómo enviar un correo electrónico para un formulario adaptable, Acción de envío de correo electrónico, Correo electrónico del formulario adaptable, Correo electrónico de envío de formulario, Enviar guía de correo electrónico
feature: Adaptive Forms, Core Components
source-git-commit: f1db04e6cd1f78c1530aefd29f5f036ca5e70873
workflow-type: tm+mt
source-wordcount: '437'
ht-degree: 24%

---


# Configuración de la acción de envío Enviar correo electrónico para un formulario adaptable

El **[!UICONTROL Enviar correo electrónico]** La acción de envío permite enviar un correo electrónico a uno o varios destinatarios cuando el formulario se ha enviado correctamente. Esta acción de envío permite crear un mensaje de correo electrónico que puede incluir datos de formulario en un formato predefinido. Por ejemplo, considere la siguiente plantilla en la que el nombre del cliente, la dirección de envío, el nombre del estado y el código postal se recuperan de los datos del formulario enviado:


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

Algunas ventajas de configurar un formulario adaptable con la acción de envío Enviar correo electrónico son:

* Permite una comunicación rápida, ya que los datos del formulario se envían directamente a los destinatarios de correo electrónico designados.
* Ayuda a optimizar el flujo de trabajo al integrar directamente los envíos de formularios en las notificaciones por correo electrónico.
* Ayuda a las organizaciones a personalizar el contenido del correo electrónico, lo que lo hace adecuado para necesidades de comunicación específicas.

## Configurar la acción de envío Enviar correo electrónico {#steps-to-configure-send-email-submit-action}

Para configurar la acción de envío:

1. Abra el Explorador de contenido y seleccione el componente **[!UICONTROL Contenedor de guía]** del formulario adaptable.
1. Haga clic en el icono de propiedades del contenedor de guía ![Propiedades de guía](/help/forms/assets/configure-icon.svg). Se abre el cuadro de diálogo Contenedor de formulario adaptable.
1. Abra la pestaña **[!UICONTROL Envío]**.
1. Desde el **[!UICONTROL Acción de envío]** , seleccione la opción **[!UICONTROL Enviar correo electrónico]**.

   ![Configuración de acción de Enviar correo electrónico](/help/forms/assets/send-email-action-configuration.gif)
1. Especifique el ID de correo electrónico del remitente en la **[!UICONTROL Desde]** cuadro de texto.
1. Añada el ID de correo electrónico del destinatario en la **[!UICONTROL Hasta]** cuadro de texto. Puede añadir varios destinatarios haciendo clic en el icono **[!UICONTROL Añadir]** botón.
1. [Opcional] Añada el destinatario para CC y CCO haciendo clic en el **[!UICONTROL Añadir]** botón.
1. Especifique una línea de asunto en la **[!UICONTROL Asunto]** cuadro de texto.
1. Añada una plantilla de correo electrónico para configurar la acción de envío Enviar correo electrónico.
   * AEM Puede especificar la ruta a la plantilla de correo electrónico externa guardada en los recursos de la mediante el **[!UICONTROL Ruta de plantilla externa]** opción.
   * También puede agregar una plantilla de correo electrónico personalizada para el envío del formulario en la **[!UICONTROL Plantilla de correo electrónico]** cuadro de texto.
1. [Opcional] El **[!UICONTROL Enviar correo electrónico]** Enviar acción proporciona la opción de incluir archivos adjuntos y un [Documento de registro (DoR)](generate-document-of-record-core-components.md) con el correo electrónico.
1. Haga clic en **[!UICONTROL Listo]**.

## Prácticas recomendadas {#best-practices}

* Se recomienda mantener el contenido del correo electrónico claro y conciso. Los usuarios deben comprender el propósito del correo electrónico y las acciones que deben realizar.
* Se recomienda que todos los campos de formulario tengan nombres de elemento únicos, incluso si se colocan en paneles diferentes dentro de un formulario adaptable.
* Cuando se utiliza AEM as a Cloud Service, el correo electrónico saliente requiere un cifrado. De forma predeterminada, la funcionalidad del correo electrónico saliente está deshabilitada. Para activarlo, envíe un ticket de asistencia a [solicitar acceso](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/development-guidelines.html?lang=es#sending-email).


## Artículos relacionados

{{af-submit-action}}


