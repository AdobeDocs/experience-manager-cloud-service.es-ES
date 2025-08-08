---
description: Explore el proceso para configurar las notificaciones por correo electrónico al enviar un formulario adaptable.
keywords: cómo enviar un correo electrónico para un formulario adaptable, acción de envío de correo electrónico, correo electrónico del formulario adaptable, correo electrónico de envío de formulario, guía para enviar correo electrónico
feature: Adaptive Forms, Core Components, Foundation Components, Edge Delivery Services
exl-id: 70386e57-345b-4edb-97f1-3fd52ea9ff4f
title: ¿Cómo configurar una acción de envío para un formulario adaptable?
role: User, Developer
source-git-commit: 1be7bafc1d93a65a81eeb2f7e86cac33cde7aa35
workflow-type: tm+mt
source-wordcount: '851'
ht-degree: 84%

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

>[!BEGINTABS]

>[!TAB Componente Base]

Para configurar una acción de envío Enviar correo electrónico para el componente Base:

1. Abra el formulario adaptable para editarlo y vaya a la sección **[!UICONTROL Envío]** de las propiedades del contenedor del formulario adaptable.
1. En la lista desplegable **[!UICONTROL Acción de envío]** seleccione la opción **[!UICONTROL Enviar correo electrónico]**.

   ![Configuración de la acción de Enviar correo electrónico](/help/forms/assets/send-email-fc.png)

1. Especifique el ID de correo electrónico del remitente en el cuadro de texto **[!UICONTROL De]**.
1. Añada el ID de correo electrónico del destinatario en el cuadro de texto **[!UICONTROL Para]**. Para añadir varios destinatarios, haga clic en el botón **[!UICONTROL Añadir]**.
1. [Opcional] Añada el destinatario para CC y CCO haciendo clic en el botón **[!UICONTROL Añadir]**.
1. Especifique una línea de asunto en el cuadro de texto **[!UICONTROL Asunto]**.
1. Añada una plantilla de correo electrónico para configurar la acción de envío Enviar correo electrónico.
   * Puede especificar la ruta a la plantilla de correo electrónico externa guardada en los recursos de AEM mediante la opción **[!UICONTROL Plantilla externa]**.
   * También puede añadir una plantilla de correo electrónico personalizada para el envío del formulario en el cuadro de texto **[!UICONTROL Plantilla de correo electrónico]**.
1. [Opcional] La acción de envío **[!UICONTROL Enviar correo electrónico]** proporciona la opción de incluir archivos adjuntos y un [documento de registro (DoR)](generate-document-of-record-core-components.md) con el correo electrónico.
1. Haga clic en **[!UICONTROL Listo]**.

>[!TAB Componente principal]

Para configurar la acción de envío Enviar correo electrónico para el componente principal:

1. Abra el Explorador de contenido y seleccione el componente **[!UICONTROL Contenedor de guía]** del formulario adaptable.
1. Haga clic en el icono de propiedades del contenedor de guía ![Propiedades de guía](/help/forms/assets/configure-icon.svg). Se abre el cuadro de diálogo Contenedor de formulario adaptable.
1. Haga clic en la pestaña **[!UICONTROL Envío]**.
1. En la lista desplegable **[!UICONTROL Acción de envío]** seleccione la opción **[!UICONTROL Enviar correo electrónico]**.

   ![Configuración de la acción de Enviar correo electrónico](/help/forms/assets/send-email-action-configuration.gif)
1. Especifique el ID de correo electrónico del remitente en el cuadro de texto **[!UICONTROL De]**.
1. Añada el ID de correo electrónico del destinatario en el cuadro de texto **[!UICONTROL Para]**. Para añadir varios destinatarios, haga clic en el botón **[!UICONTROL Añadir]**.
1. [Opcional] Añada el destinatario para CC y CCO haciendo clic en el botón **[!UICONTROL Añadir]**.
1. Especifique una línea de asunto en el cuadro de texto **[!UICONTROL Asunto]**.
1. Añada una plantilla de correo electrónico para configurar la acción de envío Enviar correo electrónico.
   * Puede especificar la ruta a la plantilla de correo electrónico externa guardada en los recursos de AEM mediante la opción **[!UICONTROL Plantilla externa]**.
   * También puede añadir una plantilla de correo electrónico personalizada para el envío del formulario en el cuadro de texto **[!UICONTROL Plantilla de correo electrónico]**.
1. [Opcional] La acción de envío **[!UICONTROL Enviar correo electrónico]** proporciona la opción de incluir archivos adjuntos y un [documento de registro (DoR)](generate-document-of-record-core-components.md) con el correo electrónico.
1. Haga clic en **[!UICONTROL Listo]**.

>[!TAB Editor universal]

Para configurar la acción de envío Enviar correo electrónico en el editor universal:

1. Abra el formulario adaptable para editarlo.
1. Haga clic en la extensión **Editar propiedades del formulario** en el editor.
Aparecerá el cuadro de diálogo **Propiedades del formulario**.

   >[!NOTE]
   >
   > * Si no ve el icono **Editar propiedades de formulario** en la interfaz de Universal Editor, habilite la extensión **Editar propiedades de formulario** en Extension Manager.
   > * Consulte el artículo [Aspectos destacados de las funciones de Extension Manager](https://developer.adobe.com/uix/docs/extension-manager/feature-highlights/#enablingdisabling-extensions) para obtener información sobre cómo habilitar o deshabilitar extensiones en el editor universal.


1. Haga clic en la pestaña **Envío** y seleccione la acción de envío **[!UICONTROL Enviar correo electrónico]**.

   ![Enviar correo electrónico al editor universal](/help/forms/assets/send-email-ue.png)

1. Especifique el ID de correo electrónico del remitente en el cuadro de texto **[!UICONTROL De]**.
1. Añada el ID de correo electrónico del destinatario en el cuadro de texto **[!UICONTROL Para]**. Para añadir varios destinatarios, haga clic en el botón **[!UICONTROL Añadir]**.
1. [Opcional] Añada el destinatario para CC y CCO haciendo clic en el botón **[!UICONTROL Añadir]**.
1. Especifique una línea de asunto en el cuadro de texto **[!UICONTROL Asunto]**.
1. Añada una plantilla de correo electrónico para configurar la acción de envío Enviar correo electrónico.
   * Puede especificar la ruta a la plantilla de correo electrónico externa guardada en los recursos de AEM mediante la opción **[!UICONTROL Plantilla externa]**.
   * También puede añadir una plantilla de correo electrónico personalizada para el envío del formulario en el cuadro de texto **[!UICONTROL Plantilla de correo electrónico]**.
1. [Opcional] La acción de envío **[!UICONTROL Enviar correo electrónico]** proporciona la opción de incluir archivos adjuntos y un [documento de registro (DoR)](generate-document-of-record-core-components.md) con el correo electrónico.
1. Haga clic en **[!UICONTROL Guardar y cerrar]**.

>[!ENDTABS]

## Prácticas recomendadas {#best-practices}

* Se recomienda que el contenido del correo electrónico sea claro y conciso. Los usuarios deben comprender el propósito del correo electrónico y las acciones que deben tomar.
* Es crucial que todos los campos de formulario tengan nombres de elemento únicos, incluso si se colocan en paneles diferentes dentro de un formulario adaptable.
* Cuando se utiliza AEM as a Cloud Service, el correo electrónico saliente requiere un cifrado. De forma predeterminada, la funcionalidad del correo electrónico saliente está deshabilitada. Para habilitarlo, envíe un ticket de asistencia a [Solicitar acceso](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/development-guidelines.html?lang=es#sending-email).

## Artículos relacionados

{{af-submit-action}}
