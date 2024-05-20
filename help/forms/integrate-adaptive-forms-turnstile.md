---
title: AEM ¿Cómo se utiliza Turnstile en un formulario adaptable con un tipo de formulario adaptable con un nombre de usuario?
description: Mejore la seguridad de los formularios con el servicio Turnstile sin esfuerzo. Guía paso a paso en el interior
topic-tags: Adaptive Forms, author
feature: Adaptive Forms, Foundation Components
hide: true
hidefromtoc: true
source-git-commit: d2c6514eb1f38b06dfa58daa03b781920b8928f6
workflow-type: tm+mt
source-wordcount: '950'
ht-degree: 24%

---

<span class="preview"> Esta función se encuentra en el Programa de usuarios que la adoptaron por anticipado. Puede escribir a aem-forms-ea@adobe.com desde su ID de correo electrónico oficial para unirse al programa de primeros usuarios y solicitar acceso a esta funcionalidad. </span>

CAPTCHA (prueba de Turing completamente automática y pública para diferenciar ordenadores de humanos) es un programa que se utiliza comúnmente en transacciones en línea para distinguir entre humanos y programas o bots automatizados. Plantea un desafío y evalúa la respuesta del usuario para determinar si es un humano o un bot que interactúa con el sitio. Evita que el usuario continúe si la prueba falla y ayuda a que las transacciones en línea sean seguras al impedir que los bots publiquen contenido no deseado o con fines malintencionados.

AEM Forms as a Cloud Service es compatible con las siguientes soluciones CAPTCHA:

* [Torniquete de Nubes](#integrate-aem-forms-environment-with-turnstile-captcha)
* [Google reCAPTCHA](/help/forms/captcha-adaptive-forms.md)
* [Chcaptcha](/help/forms/integrate-adaptive-forms-hcaptcha.md)

## Integración del entorno de AEM Forms con Turnstile Captcha

El Turnstile Captcha de Cloudflare es una medida de seguridad que tiene como objetivo proteger los formularios y sitios de bots automatizados, ataques maliciosos, spam y tráfico automatizado no deseado. Presenta una casilla de verificación en el envío del formulario para verificar que son humanos, antes de permitirles enviar el formulario. AEM Forms as a Cloud Service es compatible con Turnstile Captcha en los componentes principales de Forms adaptable.

<!-- ![Turnstile](assets/Turnstile-challenge.png)-->

### Requisitos previos para integrar el entorno de AEM Forms con Turnstile Captcha {#prerequisite}

Para configurar el torniquete para los componentes principales de AEM Forms, debe obtener la variable [Llave del sitio y clave secreta del torniquete](https://developers.cloudflare.com/turnstile/get-started/) del sitio web de Turnstile.

### Pasos para configurar Turnstile para AEM Forms{#steps-to-configure-turnstile}

1. Cree un contenedor de configuración en el entorno as a Cloud Service de AEM Forms. Un contenedor de configuración contiene las configuraciones en la nube utilizadas para conectar a AEM a los servicios externos. Para crear y configurar un contenedor de configuración para conectar su entorno de AEM Forms con Turnstile:
   1. Abra la instancia AEM Forms as a Cloud Service.
   1. Vaya a **[!UICONTROL Herramientas > General > Explorador de configuración]**.
   1. En el Explorador de configuración, puede seleccionar una carpeta existente o crear una carpeta. Puede crear una carpeta y habilitar la opción Configuraciones de nube para ella o habilitar la opción Configuraciones de nube para una carpeta existente:

      * **Para crear una carpeta y habilitar la opción Configuraciones de nube para ella**:
         1. En el Explorador de configuración, pulse **[!UICONTROL Crear]**.
         1. En el cuadro de diálogo Crear configuración, especifique un nombre, un título y seleccione **[!UICONTROL Configuraciones de nube]** opción.
         1. Haga clic en **[!UICONTROL Crear]**.
      * Para habilitar la opción Configuraciones de la nube para una carpeta existente, haga lo siguiente:
         1. En el Explorador de configuración, seleccione la carpeta y seleccione **[!UICONTROL Propiedades]**.
         1. En el cuadro de diálogo Propiedades de configuración, habilite **[!UICONTROL Configuraciones de nube]**.
         1. Seleccione **[!UICONTROL Guardar y cerrar]** para guardar la configuración y salir del cuadro de diálogo.

1. Configure Cloud Service:
   1. AEM En la instancia de autor de la, vaya a ![tools-1](assets/tools-1.png) > **[!UICONTROL Cloud Service]** y seleccione **[!UICONTROL Torniquete]**.
      ![Torniquete en ui](assets/turnstile-in-ui.png)
   1. Seleccione un contenedor de configuración, creado o actualizado, como se describe en la sección anterior. Seleccione **[!UICONTROL Crear]**.
      ![Torniquete de configuración](assets/config-hcaptcha.png)
   1. Especificar **[!UICONTROL Tipo de widget]** como se administra, el tipo de widget puede cambiar, lo que depende de la clave obtenida en el requisito previo, **[!UICONTROL Título]**, **[!UICONTROL Nombre]**, **[!UICONTROL Clave del sitio]**, y **[!UICONTROL Clave secreta]** para el servicio de torniquete [obtenido en requisito previo](#prerequisite). Seleccione **[!UICONTROL Crear]**.

      ![Configure el Cloud Service para conectar su entorno de AEM Forms con Turnstile](assets/config-turntstile.png)

>[!NOTE]
> Los usuarios no tienen que modificar la URL de validación de JavaScript del lado del cliente y la URL de validación del lado del servidor, ya que ya están rellenadas previamente para la validación de Turnstile.

Una vez configurado el servicio Turnstile Captcha, está disponible para su uso en un formulario adaptable.

## Uso del torniquete en un formulario adaptable{#using-turnstile-foundation-components}

1. Abra la instancia AEM Forms as a Cloud Service.
1. Vaya a **[!UICONTROL Formularios]** > **[!UICONTROL Formularios y documentos]**.
1. Seleccione un formulario adaptable y seleccione **[!UICONTROL Propiedades]**. Para el **[!UICONTROL Contenedor de configuración]** , seleccione el Contenedor de configuración que contiene la Configuración de nube que conecta AEM Forms con Turnstile y seleccione **[!UICONTROL Guardar y cerrar]**.

   Si no tiene ese contenedor de configuración, consulte la sección [Conecte su entorno de AEM Forms con Turnstile](#connect-your-forms-environment-with-turnstile-service) para aprender a crear un contenedor de configuración.

   ![Seleccionar el contenedor de configuración](/help/forms/assets/captcha-properties.png)

1. Seleccione un formulario adaptable y seleccione **[!UICONTROL Editar]**. El formulario adaptable se abre en el editor de Formularios adaptables.
1. Desde el navegador de componentes, arrastre y suelte el componente **[!UICONTROL Captcha]** en el formulario adaptable.
1. Seleccione el **[!UICONTROL Captcha]** y haga clic en propiedades ![Icono Propiedades](assets/configure-icon.svg) icono. Abre el cuadro de diálogo de propiedades.

   ![Configuración](assets/turnstile-setting-v1.png)

   Especifique las siguientes propiedades:

   * **[!UICONTROL Título]:** Especifique el título del componente Captcha, puede identificar fácilmente un componente del formulario con su nombre único tanto en el formulario como en el editor de reglas.
   * **[!UICONTROL Mensaje de validación]:** Proporcione un mensaje de validación para validar el captcha al enviar el formulario.
   * **[!UICONTROL Validar Captcha]:** Puede seleccionar una de las opciones para validar el captcha:
      * Al enviar el formulario
      * Sobre una acción del usuario.
   * **[!UICONTROL Servicio Captcha]:** Seleccione el servicio Captcha, donde selecciona el servicio Captcha de torniquete de Cloudfare.
   * **[!UICONTROL Configuración de Captcha]:** Seleccione una Configuración de nube configurada para Torniquete. por ejemplo, aquí puede seleccionar la **clave administrada**.
     >[!NOTE]
     >Puede tener varias configuraciones en la nube en su entorno para un propósito similar. Por lo tanto, elija el servicio con cuidado. Si no aparece ningún servicio, consulte [Conecte su entorno de AEM Forms con Turnstile](#connect-your-forms-environment-with-turnstile-service) para aprender a crear un Cloud Service que conecte su entorno de AEM Forms con el servicio Turnstile.

   * **Mensaje de error:** Proporcione el mensaje de error que se mostrará al usuario cuando falle el envío del Captcha.
   * **Tamaño de Captcha:** Se selecciona el tamaño de visualización del cuadro de diálogo Desafío de torniquete. Utilice el **[!UICONTROL Compacto]** opción para mostrar un tamaño pequeño y el **[!UICONTROL Normal]** opción para mostrar un cuadro de diálogo de desafío de torniquete de tamaño relativamente grande.


     >[!NOTE]
     >Esto es aplicable para el tipo de widget Gestionado y No interactivo. Si el tipo de widget es invisible, la propiedad size no es obligatoria y está desactivada.

1. Seleccione **[!UICONTROL Listo]**.

Ahora, solo se permiten para el envío del formulario los formularios legítimos, en los que el usuario que rellena el formulario borra correctamente el desafío planteado por el servicio Turnstile.

![Turnstile Challenge](assets/turnstile-challenge.png)

## Preguntas frecuentes

* **P: ¿Puedo usar más de un componente Captcha en un formulario adaptable?**
* **R:** No se puede usar más de un componente Captcha en un formulario adaptable. Además, no se recomienda utilizar un componente Captcha en un fragmento o panel marcado para la carga diferida.

## Ver también {#see-also}

{{see-also}}