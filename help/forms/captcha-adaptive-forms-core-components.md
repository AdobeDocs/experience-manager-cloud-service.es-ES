---
title: Utilizar el reCAPTCHA de Google en un formulario adaptable de AEM
description: Mejore la seguridad de los formularios con el servicio reCAPTCHA de Google sin esfuerzo. Guía paso a paso en el interior
topic-tags: Adaptive Forms, author
keywords: Servicio reCAPTCHA de Google, Formularios adaptables, desafío CAPTCHA, prevención de bots, componentes principales, seguridad de envío de formularios, prevención de correo no deseado de formularios
feature: Adaptive Forms, Core Components
exl-id: d116f979-efb6-4fac-8202-89afd1037b2c
source-git-commit: eaab351460363b83c7d3667e048235506cc71c41
workflow-type: tm+mt
source-wordcount: '918'
ht-degree: 90%

---

# Usar reCAPTCHA de Google en un formulario adaptable de AEM basado en componentes principales {#using-reCAPTCHA-in-adaptive-forms}

| Se aplica a | Vínculo del artículo |
| -------- | ---------------------------- |
| Formulario adaptable basado en componentes principales | Este artículo |
| Formulario adaptable basado en componentes de base | [Haga clic aquí](/help/forms/captcha-adaptive-forms.md) |

CAPTCHA (prueba de Turing completamente automática y pública para diferenciar ordenadores de humanos) es un programa que se utiliza comúnmente en transacciones en línea para distinguir entre humanos y programas o bots automatizados. Plantea un desafío y evalúa la respuesta del usuario para determinar si es un humano o un bot que interactúa con el sitio. Evita que el usuario continúe si la prueba falla y ayuda a que las transacciones en línea sean seguras al impedir que los bots publiquen contenido no deseado o con fines malintencionados.

[!DNL AEM Forms] as a [!DNL Cloud Service] es compatible con Google reCAPTCHA v2 en Formularios adaptables. Puede utilizarlo para presentar un desafío de CAPTCHA en el envío de formularios. Para utilizar reCAPTCHA en un formulario adaptable, haga lo siguiente:

1. [Conecte su entorno de AEM Forms con el servicio reCAPTCHA de Google](#connect-your-forms-environment-with-recaptcha-service-by-google)
1. [Configure el formulario adaptable para mostrar el desafío CAPTCHA al enviar el formulario](#using-reCAPTCHA)

## Conecte su entorno de AEM Forms con el servicio reCAPTCHA de Google {#connect-your-forms-environment-with-recaptcha-service-by-google}

Para conectar su entorno de AEM Forms con el servicio reCAPTCHA de Google

1. Obtener el [par de claves de la API reCAPTCHA](https://www.google.com/recaptcha/admin) de Google. Incluye una **clave del sitio** y una **clave secreta**.

   ![Cree la configuración de reCAPTCHA de Google del sitio web de Google para obtener las claves de reCAPTCHA](/help/forms/assets/google-captcha.gif)
1. Cree el contenedor de configuración en su entorno de AEM Forms as a Cloud Service. Un contenedor de configuración contiene las configuraciones en la nube utilizadas para conectar a AEM a los servicios externos. Para crear y configurar un contenedor de configuración para conectar su entorno de AEM Forms con el servicio reCAPTCHA de Google, haga lo siguiente:
   1. Abra la instancia AEM Forms as a Cloud Service.
   1. Vaya a **[!UICONTROL Herramientas > General > Explorador de configuración]**. En el Explorador de configuración, puede hacer lo siguiente:
   1. Seleccionar una carpeta existente o crear una nueva. Crear una carpeta y habilitar la opción Configuraciones de la nube para ella o Habilitar la opción Configuraciones de nube de la carpeta existente:

      * Para crear una carpeta y habilitar la opción Configuraciones de la nube para ella, haga lo siguiente:
         1. En el Explorador de configuración, pulse **[!UICONTROL Crear]**.
         1. En el cuadro de diálogo Crear configuración, especifique el nombre, el título y seleccione la opción **[!UICONTROL Configuraciones de la nube]**.
         1. Haga clic en **[!UICONTROL Crear]**
      * Para habilitar la opción Configuraciones de la nube para una carpeta existente, haga lo siguiente:
         1. En el Explorador de configuración, seleccione la carpeta y seleccione **[!UICONTROL Propiedades]**.
         1. En el cuadro de diálogo Propiedades de configuración, habilite **[!UICONTROL Configuraciones de nube]**.
         1. Seleccionar **[!UICONTROL Guardar y cerrar]** para guardar la configuración y salir del cuadro de diálogo.

1. Configure Cloud Service:
   1. AEM En la instancia de autor de la, vaya a ![tools-1](assets/tools-1.png) > **[!UICONTROL Cloud Service]** y seleccione **[!UICONTROL reCAPTCHA]**.
   1. Seleccione un contenedor de configuración, creado o actualizado en la sección anterior. Seleccione **[!UICONTROL Crear]**.
   1. Especificar **[!UICONTROL Título]**, **[!UICONTROL Nombre]**, **[!UICONTROL Clave del sitio]**, y **[!UICONTROL Clave secreta]** para el servicio reCAPTCHA (obtenido en el paso 1). Seleccione **[!UICONTROL Crear]**.

   ![Configure el Cloud Service para conectar su entorno de AEM Forms con el servicio reCAPTCHA de Google](/help/forms/assets/captcha-configuration.gif)

   Una vez configurado el servicio reCAPTCHA, está disponible para su uso en Formularios adaptables. Para obtener más información, consulte [Usar Google reCAPTCHA en un Formulario adaptable](#using-reCAPTCHA).

## Uso de Google reCAPTCHA en un formulario adaptable {#using-reCAPTCHA}

Para utilizar el reCAPTCHA en Formularios adaptables, haga lo siguiente:

1. Abra la instancia AEM Forms as a Cloud Service.
1. Vaya a **[!UICONTROL Formularios]** > **[!UICONTROL Formularios y documentos]**.
1. Seleccione un Forms adaptable y seleccione **[!UICONTROL Propiedades]**. Para el **[!UICONTROL Contenedor de configuración]** , seleccione el contenedor de configuración que contiene la configuración de nube que conecta AEM Forms con el servicio reCAPTCHA de Google y seleccione **[!UICONTROL Guardar y cerrar]**.

   Si no tiene ese Contenedor de configuración, consulte la sección [Conectar su entorno de AEM Forms con el servicio reCAPTCHA de Google](#connect-your-forms-environment-with-recaptcha-service-by-google) para obtener información sobre cómo crear este tipo de Contenedor de configuración.

   ![Seleccionar el contenedor de configuración](/help/forms/assets/captcha-properties.png)

1. Seleccione un Forms adaptable y seleccione **[!UICONTROL Editar]**. El formulario adaptable se abre en el editor de Formularios adaptables.
1. Desde el explorador de componentes, arrastre y suelte el componente **[!UICONTROL reCAPTCHA del formulario adaptable]** en este.

   La validación de reCAPTCHA de Google distingue entre mayúsculas y minúsculas y caduca en unos minutos. Por lo tanto, Adobe recomienda colocar el componente **[!UICONTROL reCAPTCHA del formulario adaptable]** justo antes de pulsar el botón **[!UICONTROL Enviar]**.

1. Seleccione el **[!UICONTROL Formulario adaptable reCAPTCHA]** y seleccione las propiedades ![Icono Propiedades](assets/configure-icon.svg) icono. Abre el cuadro de diálogo de propiedades. Especifique las siguientes propiedades obligatorias:
   * **[!UICONTROL Nombre]:** puede identificar fácilmente el componente de un formulario con su nombre único, tanto en el formulario como en el editor de reglas, pero el nombre no debe contener espacios ni caracteres especiales.
   * **[!UICONTROL Configuración de CAPTCHA]:** seleccione una configuración de nube para presentar el cuadro de diálogo reCAPTCHA de Google para el formulario. Puede tener varias configuraciones de la nube en su entorno para un propósito similar. Por lo tanto, elija el servicio con cuidado. Si no aparece ningún servicio, consulte [Conectar su entorno de AEM Forms con el servicio reCAPTCHA de Google](#connect-your-forms-environment-with-recaptcha-service-by-google) para aprender a crear un Cloud Service que conecte su entorno de AEM Forms con el servicio reCAPTCHA de Google.
   * **Tamaño del Captcha:** puede seleccionar el tamaño de visualización del diálogo de comprobación del reCAPTCHA de Google. Utilice la opción **[!UICONTROL Compacto]** para mostrar un tamaño pequeño y la opción **[!UICONTROL Normal]** para mostrar un cuadro de diálogo de comprobación de reCAPTCHA de Google de tamaño relativamente grande.

1. Seleccionar **[!UICONTROL Listo]**.

   Ahora, verá **protegido por reCAPTCHA** en el formulario adaptable. Se muestra en todos los formularios adaptables configurados para utilizar el servicio reCAPTCHA de Google.

   Ahora, solo se permite el envío de formularios legítimos, en los que la persona que rellena el formulario supera con éxito el desafío planteado por el servicio reCAPTCHA de Google.
   ![Distintivo protegido por reCAPTCHA de Google](/help/forms/assets/google-recaptcha-v2.png)

<!--
### Show or hide CAPTCHA component based on rules {#show-hide-captcha}

You can select to show or hide the CAPTCHA component based on rules that you apply on a component in an Adaptive Form. Select the component, select ![edit rules](assets/edit-rules-icon.svg), and select **[!UICONTROL Create]** to create a rule. For more information on creating rules, see [Rule Editor](rule-editor.md).

For example, the CAPTCHA component must display in an Adaptive Form only if the Currency Value field in the form has a value of more than 25000.

Select the **[!UICONTROL Currency Value]** field in the form and create the following rules:

![Show or hide rules](assets/rules-show-hide-captcha.png)

   >[!NOTE]
   >
   > When you select a reCAPTCHA v2 configuration and the size is set to [!UICONTROL Invisible], the show/hide option remains disabled.

   -->

## Preguntas frecuentes

**P: ¿Puedo usar más de un componente Captcha en un formulario adaptable?**
**R:** No se puede usar más de un componente Captcha en un formulario adaptable. Además, no se recomienda utilizar el componente Captcha en un fragmento o panel marcado para la carga diferida.

## Vea también {#see-also}

{{see-also}}