---
title: Usar Google reCAPTCHA en un formulario adaptable basado en componentes principales
description: Mejore la seguridad de los formularios con el servicio reCAPTCHA de Google sin esfuerzo. Guía paso a paso en el interior!
topic-tags: Adaptive Forms, author
hide: true
hidefromtoc: true
Keywords: Google reCAPTCHA service, Adaptive Forms, CAPTCHA challenge, Bot prevention, Core Components, Form submission security, Form spam prevention
source-git-commit: b81acc99b1d90b05b7c341253e7cbb46c6ea12ae
workflow-type: tm+mt
source-wordcount: '878'
ht-degree: 16%

---

# Usar reCAPTCHA en Forms adaptable basado en componentes principales {#using-reCAPTCHA-in-adaptive-forms}

CAPTCHA (prueba de Turing completamente automática y pública para diferenciar ordenadores de humanos) es un programa que se utiliza comúnmente en transacciones en línea para distinguir entre humanos y programas o bots automatizados. Plantea un desafío y evalúa la respuesta del usuario para determinar si es un humano o un bot que interactúa con el sitio. Evita que el usuario continúe si la prueba falla y ayuda a que las transacciones en línea sean seguras al impedir que los bots publiquen contenido no deseado o con fines malintencionados.

[!DNL AEM Forms] as a [!DNL Cloud Service] es compatible con Google reCAPTCHA v2 en Forms adaptable. Puede utilizarlo para presentar un desafío CAPTCHA al enviar el formulario. Para utilizar reCAPTCHA en un formulario adaptable haga lo siguiente:

1. [Conecte su entorno de AEM Forms con el servicio reCAPTCHA de Google](#connect-your-forms-environment-with-recaptcha-service-by-google)
1. [Configure el formulario adaptable para mostrar el desafío CAPTCHA al enviar el formulario](#using-reCAPTCHA)

## Conecte su entorno de AEM Forms con el servicio reCAPTCHA de Google {#connect-your-forms-environment-with-recaptcha-service-by-google}

Para conectar su entorno de AEM Forms con el servicio reCAPTCHA de Google

1. Obtener el [par de claves de la API reCAPTCHA](https://www.google.com/recaptcha/admin) de Google. Incluye un **clave del sitio** y una **clave secreta**.

   ![Cree la configuración reCAPTCHA de Google del sitio web de Google para obtener las claves reCAPTCHA](/help/forms/assets/google-captcha.gif)
1. Cree el contenedor de configuración en su entorno as a Cloud Service de AEM Forms. AEM Un contenedor de configuración contiene las configuraciones de nube utilizadas para conectarse a los servicios externos de la forma que se utilizan para conectarse a los servicios externos. Para crear y configurar un contenedor de configuración para conectar su entorno de AEM Forms con el servicio reCAPTCHA de Google:
   1. Abra la instancia as a Cloud Service de AEM Forms.
   1. Vaya a **[!UICONTROL Herramientas > General > Explorador de configuración]**. En el Explorador de configuración, puede:
   1. Seleccione una carpeta existente o cree una carpeta. Puede crear una carpeta y habilitar la opción Configuraciones de nube para ella o Habilitar la opción Configuraciones de nube para una carpeta existente:

      * Para crear una carpeta y habilitar la opción Configuraciones de nube para ella:
         1. En el Explorador de configuración, haga clic en **[!UICONTROL Crear]**.
         1. En el cuadro de diálogo Crear configuración, especifique el nombre, el título y seleccione **[!UICONTROL Configuraciones de nube]** opción.
         1. Haga clic en **[!UICONTROL Crear]**
      * Para habilitar la opción Configuraciones en la nube para una carpeta existente:
         1. En el Explorador de configuración, seleccione la carpeta  y pulse **[!UICONTROL Propiedades]**.
         1. En el cuadro de diálogo Propiedades de configuración, habilite **[!UICONTROL Configuraciones de nube]**.
         1. Pulse **[!UICONTROL Guardar y cerrar]** para guardar la configuración y salir del cuadro de diálogo.

1. Configuración de Cloud Service:
   1. AEM En la instancia de autor de la, vaya a ![tools-1](assets/tools-1.png) > **[!UICONTROL Cloud Services]** y pulse **[!UICONTROL reCAPTCHA]**.
   1. Seleccione un contenedor de configuración, creado o actualizado en la sección anterior. Pulse **[!UICONTROL Crear]**.
   1. Especificar **[!UICONTROL Título]**, **[!UICONTROL Nombre]**, **[!UICONTROL Clave del sitio]**, y **[!UICONTROL Clave secreta]** para el servicio reCAPTCHA (obtenido en el paso 1). Pulse **[!UICONTROL Crear]**.


   ![Configure el Cloud Service para que conecte su entorno de AEM Forms con el servicio reCAPTCHA de Google](/help/forms/assets/captcha-configuration.gif)



   Una vez configurado el servicio reCAPTCHA, estará disponible para su uso en un formulario adaptable. Para obtener más información, consulte [usar Google reCAPTCHA en un formulario adaptable](#using-reCAPTCHA).


## Uso de Google reCAPTCHA en un formulario adaptable {#using-reCAPTCHA}

Para usar reCAPTCHA en Forms adaptable:

1. Abra la instancia as a Cloud Service de AEM Forms.
1. Vaya a **[!UICONTROL Formularios]** > **[!UICONTROL Formularios y documentos]**.
1. Seleccione un Forms adaptable y pulse **[!UICONTROL Propiedades]**. Para el **[!UICONTROL Contenedor de configuración]** , seleccione el contenedor de configuración que contiene la configuración de nube que conecta AEM Forms con el servicio reCAPTCHA de Google y pulse **[!UICONTROL Guardar y cerrar]**.

   Si no tiene ese contenedor de configuración, consulte la sección [Conecte su entorno de AEM Forms con el servicio reCAPTCHA de Google](#connect-your-forms-environment-with-recaptcha-service-by-google) para obtener información sobre cómo crear este tipo de contenedor de configuración.

   ![Seleccionar contenedor de configuración](/help/forms/assets/captcha-properties.png)

1. Seleccione un Forms adaptable y pulse **[!UICONTROL Editar]**. El formulario adaptable se abrirá en el editor de Forms adaptable.
1. Desde el explorador de componentes, arrastre y suelte el **[!UICONTROL Formulario adaptable reCAPTCHA]** en el formulario adaptable.

   La validación de Google reCAPTCHA distingue entre mayúsculas y minúsculas y caduca en unos minutos. Por lo tanto, el Adobe recomienda colocar el **[!UICONTROL Formulario adaptable reCAPTCHA]** componente justo antes de **[!UICONTROL Enviar]** botón.

1. Seleccione el **[!UICONTROL Formulario adaptable reCAPTCHA]** y pulse las propiedades ![Icono Propiedades](assets/configure-icon.svg) icono. Abre el cuadro de diálogo de propiedades. Especifique las siguientes propiedades obligatorias:
   * **[!UICONTROL Nombre]:** Puede identificar fácilmente un componente de formulario con su nombre único tanto en el formulario como en el editor de reglas, pero el nombre no debe contener espacios ni caracteres especiales.
   * **[!UICONTROL Configuración de CAPTCHA]:** Seleccione una configuración de nube para presentar el cuadro de diálogo reCAPTCHA de Google para el formulario. Puede tener varias configuraciones de nube en su entorno para un propósito similar. Por lo tanto, elija el servicio con cuidado. Si no aparece ningún servicio, consulte [Conecte su entorno de AEM Forms con el servicio reCAPTCHA de Google](#connect-your-forms-environment-with-recaptcha-service-by-google) para aprender a crear un Cloud Service que conecte su entorno de AEM Forms con el servicio reCAPTCHA de Google.
   * **Tamaño de Captcha:** Puede seleccionar el tamaño de visualización del diálogo de desafío reCAPTCHA de Google. Utilice el **[!UICONTROL Compacto]** opción para mostrar un tamaño pequeño y el **[!UICONTROL Normal]** opción para mostrar un cuadro de diálogo de desafío reCAPTCHA de Google de tamaño relativamente grande.

1. Pulse **[!UICONTROL Listo]**.

   Ahora, la **protegido por reCAPTCHA** se muestra en el formulario adaptable. Se muestra en todas las Forms adaptables configuradas para utilizar el servicio reCAPTCHA de Google.

   Ahora, solo se permiten el envío de formularios legítimos, en los que el usuario que rellena el formulario borra correctamente el desafío planteado por el servicio reCAPTCHA de Google.
   ![Distintivo protegido por reCAPTCHA de Google](/help/forms/assets/google-recaptcha-v2.png)

<!--
### Show or hide CAPTCHA component based on rules {#show-hide-captcha}

You can select to show or hide the CAPTCHA component based on rules that you apply on a component in an Adaptive Form. Tap the component, select ![edit rules](assets/edit-rules-icon.svg), and tap **[!UICONTROL Create]** to create a rule. For more information on creating rules, see [Rule Editor](rule-editor.md).

For example, the CAPTCHA component must display in an Adaptive Form only if the Currency Value field in the form has a value of more than 25000.

Tap the **[!UICONTROL Currency Value]** field in the form and create the following rules:

![Show or hide rules](assets/rules-show-hide-captcha.png)

   >[!NOTE]
   >
   > When you select a reCAPTCHA v2 configuration and the size is set to [!UICONTROL Invisible], the show/hide option remains disabled.

   -->

## Preguntas frecuentes

**P: ¿Puedo usar más de un componente Captcha en un formulario adaptable?**
**R:** No se puede usar más de un componente Captcha en un formulario adaptable. Además, no se recomienda utilizar el componente Captcha en un fragmento o panel marcado para la carga diferida.

