---
title: Uso de reCAPTCHA con Edge Delivery Services para AEM Forms as a Cloud Service
description: Uso de Google reCAPTCHA en un formulario para Edge Delivery Services para AEM Forms
feature: Edge Delivery Services
keywords: reCAPTCHA en formularios, Usar reCAPTCHA en el editor universal, Agregar reCAPTCHA en formularios
role: Admin, Architect, Developer
hide: true
hidefromtoc: true
exl-id: 1f28bd13-133f-487e-8b01-334be7c08a3f
source-git-commit: 320ab86bc73e874705d985b927e90eec3cad1cf9
workflow-type: tm+mt
source-wordcount: '1225'
ht-degree: 13%

---


# Uso de reCAPTCHA en la creación de WYSIWYG

CAPTCHA (prueba de Turing completamente automática y pública para diferenciar ordenadores de humanos) es una herramienta popular utilizada para proteger los sitios web de actividades fraudulentas, spam y uso indebido.

Por ejemplo, considere un formulario que calcule el impuesto en función de deducciones adicionales y el tipo impositivo. En estos casos, existe el riesgo de que usuarios maliciosos exploten el formulario para enviar correos electrónicos de phishing o inundarlo con contenido irrelevante o dañino mediante bots de spam. La integración de CAPTCHA ofrece una seguridad añadida al verificar que los envíos proceden de usuarios genuinos, lo que minimiza de forma eficaz las entradas de correo no deseado.

![Google recaptcha](/help/edge/docs/forms/universal-editor/assets/google-recaptcha.png)

En Edge Delivery Services Forms, el bloque de formulario le permite [conectar Google reCAPTCHA con formularios](#connect-forms-with-recaptcha-service-by-google) mediante el componente **Captcha(Invisible)** para distinguir entre humanos y bots. Esta funcionalidad ayuda a los autores a proteger sus formularios del correo no deseado y del uso indebido.

## Conexión de Forms con el servicio reCAPTCHA de Google

Puede crear Edge Delivery Services Forms para implementar el servicio reCAPTCHA proporcionado por Google. Según sus necesidades, puede configurar uno de los siguientes servicios reCAPTCHA para su Forms de Edge Delivery Services:

* [reCAPTCHA Enterprise](#configure-recaptcha-enterprise)
* [reCAPTCHA](#configure-recaptcha)

>[!NOTE]
>
> Para obtener más información sobre cómo funciona reCAPTCHA, consulte [Google reCAPTCHA](https://developers.google.com/recaptcha/).

### Configuración de reCAPTCHA Enterprise

reCAPTCHA Enterprise es un servicio premium de detección y prevención de fraude de nivel empresarial que ofrece Google. Se basa en reCAPTCHA (basado en puntuación), pero proporciona funciones adicionales, escalabilidad y personalización para satisfacer las complejas necesidades de las empresas.

#### Antes de comenzar

Antes de configurar Google reCAPTCHA Enterprise para Edge Delivery Services Forms, asegúrese de haber completado los siguientes pasos:

1. Cree o seleccione un [proyecto de Google Cloud](https://cloud.google.com/recaptcha/docs/prepare-environment#before-you-begin) y recupere el [identificador de proyecto](https://support.google.com/googleapi/answer/7014113?hl=en#:~:text=To%20locate%20your%20project%20ID,a%20member%20of%20are%20displayed).

1. [Habilite la API de reCAPTCHA Enterprise](https://cloud.google.com/recaptcha/docs/prepare-environment#enable-api) para su proyecto de Google Cloud y [cree una clave de API](https://console.cloud.google.com/apis/credentials).

1. Cree una clave de sitio [para su proyecto de Google Cloud](https://console.cloud.google.com/security/recaptcha) y copie la clave de sitio.

Una vez que tenga estas credenciales, puede continuar con la configuración de reCAPTCHA Enterprise para sus formularios:

1. [Crear contenedor de configuración de nube](#1-create-cloud-configuration-container)
1. [Cree la configuración del servicio en la nube para reCAPTCHA Enterprise](#2-create-the-cloud-service-configuration-for-recaptcha-enterprise)

#### 1. Crear contenedor de configuración de nube

Para crear el contenedor de configuración de nube, realice los siguientes pasos:

1. Inicie sesión en la instancia de autor.
1. Vaya a **[!UICONTROL Herramientas]** ![herramientas-1](/help/forms/assets/tools-1.png) > **[!UICONTROL General]** > **[!UICONTROL Explorador de configuración]**.

   ![Contenedor de configuración de nube](/help/edge/docs/forms/universal-editor/assets/recaptcha-general-configuration.png)

1. En el **[!UICONTROL Explorador de configuración]**, vaya a su formulario y seleccione **[!UICONTROL Propiedades]**.

   ![Propiedades de configuración de nube](/help/edge/docs/forms/universal-editor/assets/general-configuration-properties.png)

1. En el cuadro de diálogo **[!UICONTROL Propiedades de configuración]**, habilite **[!UICONTROL Configuraciones de nube]**.

1. Seleccione **[!UICONTROL Guardar y cerrar]** para guardar la configuración y salir del cuadro de diálogo.

   ![Habilitar propiedades de configuración de nube](/help/edge/docs/forms/universal-editor/assets/enable-cloud-configurations.png)
`
Después de crear el contenedor de configuración en la nube, publíquelo.

   ![Configuración de nube de publicación](/help/edge/docs/forms/universal-editor/assets/publish-cloud-configuration.png)

#### 2. Cree la configuración del servicio en la nube para reCAPTCHA Enterprise

Para crear la configuración del servicio en la nube para reCAPTCHA Enterprise, realice los siguientes pasos:

1. Inicie sesión en la instancia de autor.
1. Vaya a **[!UICONTROL Herramientas]** ![herramientas-1](/help/forms/assets/tools-1.png) > **[!UICONTROL Cloud Services]** > **[!UICONTROL reCAPTCHA]**.

   ![Configuración de nube de Recaptcha](/help/edge/docs/forms/universal-editor/assets/recaptcha-cloud-configuration.png)

   Se abre el cuadro de diálogo **Configuraciones**.

1. Vaya al formulario y seleccione **[!UICONTROL Crear]**.

   ![Configuración de Captcha](/help/edge/docs/forms/universal-editor/assets/create-captcha-confguration.png)

   Se abre el cuadro de diálogo **[!UICONTROL Crear configuración de reCAPTCHA]**.

   ![reCaptcha Enterprise](/help/edge/docs/forms/universal-editor/assets/recaptcha-enterprise.png)

1. Seleccione la versión como [!DNL ReCAPTCHA Enterprise] y especifique el título, el nombre, el identificador de proyecto, la clave del sitio y la clave de API.

   >[!NOTE]
   >
   > Puede obtener el ID del proyecto, la clave del sitio y la clave de API de la sección [Antes de comenzar](#before-you-start) para reCAPTCHA Enterprise.

1. Seleccione **[!UICONTROL Tipo de clave]** como **Clave de sitio basada en la puntuación**.
1. Especifique una [puntuación de umbral en el rango de 0 a 1](https://cloud.google.com/recaptcha/docs/interpret-assessment-website#interpret_scores). Las puntuaciones superiores o iguales a las puntuaciones del umbral identifican la interacción humana, que de lo contrario se considera interacción de bots.
1. Selecciona **[!UICONTROL Crear]** para crear la configuración del servicio en la nube.

   Después de crear la configuración de nube reCAPTCHA, publíquelo.

   ![Publicar configuración de Recaptcha](/help/edge/docs/forms/universal-editor/assets/publisg-recaptcha-configuration.png)

Ahora puede crear o editar un formulario y agregar el componente reCAPTCHA mediante la función de creación basada en WYSIWYG. Para obtener instrucciones detalladas sobre la integración de Google reCAPTCHA en el formulario, consulte [Usar reCAPTCHA en el formulario](#use-recaptcha-in-your-form).

## Configurar reCAPTCHA

reCAPTCHA es un servicio gratuito ofrecido por Google que ayuda a los sitios web a detectar y evitar el tráfico abusivo, incluidos los bots y el correo no deseado. Admite una versión basada en puntuación que funciona en segundo plano y asigna una puntuación de riesgo (de 0,0 a 1,0) a cada interacción del usuario. Las puntuaciones superiores o iguales a las puntuaciones del umbral identifican la interacción humana, que de lo contrario se considera interacción de bots.

#### Antes de comenzar

Antes de configurar Google reCAPTCHA para Edge Delivery Services Forms, recupere el par de claves de la API [reCAPTCHA de la consola de Google](https://www.google.com/recaptcha/admin). El par incluye una clave de sitio y una clave secreta.

>[!NOTE]
>
> * Edge Delivery Services Forms solo admite la versión **basada en la puntuación reCAPTCHA**.

Una vez que tenga el par de claves API, puede configurar reCAPTCHA para los formularios:

1. [Crear contenedor de configuración de nube](#1-create-cloud-configuration-container-1)
1. [Cree la configuración del servicio en la nube para reCAPTCHA](#2-create-the-cloud-service-configuration-for-recaptcha)

#### 1. Crear contenedor de configuración de nube

Para crear el contenedor de configuración de nube, realice los siguientes pasos:

1. Inicie sesión en la instancia de autor.
1. Vaya a **[!UICONTROL Herramientas]** ![herramientas-1](/help/forms/assets/tools-1.png) > **[!UICONTROL General]** > **[!UICONTROL Explorador de configuración]**.

   ![Contenedor de configuración de nube](/help/edge/docs/forms/universal-editor/assets/recaptcha-general-configuration.png)

1. En el **[!UICONTROL Explorador de configuración]**, vaya a su formulario y seleccione **[!UICONTROL Propiedades]**.

   ![Propiedades de configuración de nube](/help/edge/docs/forms/universal-editor/assets/general-configuration-properties.png)

1. En el cuadro de diálogo **[!UICONTROL Propiedades de configuración]**, habilite **[!UICONTROL Configuraciones de nube]**.

1. Seleccione **[!UICONTROL Guardar y cerrar]** para guardar la configuración y salir del cuadro de diálogo.

   ![Habilitar propiedades de configuración de nube](/help/edge/docs/forms/universal-editor/assets/enable-cloud-configurations.png)

   Después de crear el contenedor de configuración en la nube, publíquelo.

   ![Configuración de nube de publicación](/help/edge/docs/forms/universal-editor/assets/publish-cloud-configuration.png)

#### 2. Cree la configuración del servicio en la nube para reCAPTCHA

Para crear la configuración del servicio en la nube para reCAPTCHA, realice los siguientes pasos:

1. Inicie sesión en la instancia de autor.
1. Vaya a **[!UICONTROL Herramientas]** ![herramientas-1](/help/forms/assets/tools-1.png) > **[!UICONTROL Cloud Services]** > **[!UICONTROL reCAPTCHA]**.

   ![Configuración de nube de Recaptcha](/help/edge/docs/forms/universal-editor/assets/recaptcha-cloud-configuration.png)

   Se abre el cuadro de diálogo **Configuraciones**.

1. Vaya al formulario y seleccione **[!UICONTROL Crear]**.

   ![Configuración de Captcha](/help/edge/docs/forms/universal-editor/assets/create-captcha-confguration.png)

   Se abre el cuadro de diálogo **[!UICONTROL Crear configuración de reCAPTCHA]**.

   ![reCaptcha Enterprise](/help/edge/docs/forms/universal-editor/assets/recaptcha.png)

1. Seleccione la versión como [!DNL ReCAPTCHA v2] y especifique el Título y el Nombre.
1. Especifique la Clave del sitio y la Clave secreta.

   >[!NOTE]
   >
   > Puede obtener la clave de sitio y la clave secreta de la sección [Antes de comenzar](#before-you-begin) para reCAPTCHA.

1. Selecciona **[!UICONTROL Crear]** para crear la configuración del servicio en la nube.

   Después de crear la configuración de nube reCAPTCHA, publíquelo.

   ![Publicar configuración de Recaptcha](/help/edge/docs/forms/universal-editor/assets/publisg-recaptcha-configuration.png)

Ahora puede crear y editar un formulario y agregar el componente reCAPTCHA mediante la función de creación basada en WYSIWYG. Para obtener instrucciones detalladas sobre la integración de Google reCAPTCHA en el formulario, consulte [Usar reCAPTCHA en el formulario](#use-recaptcha-in-your-form).

### Uso de reCAPTCHA en el formulario

Para crear un formulario y agregar el componente reCAPTCHA (invisible), realice los siguientes pasos:

1. Abra un formulario en el Editor universal para editarlo.
1. Vaya a la sección del Formulario adaptable añadido en el árbol de contenido.
1. Haga clic en el icono **[!UICONTROL Agregar]** y agregue el componente **[!UICONTROL Captcha (invisible)]** de la lista **Componentes de formulario adaptable**.

   ![Agregar componente reCaptcha](/help/edge/docs/forms/universal-editor/assets/add-recaptcha-component.png)

   También puede arrastrar y soltar el componente de Forms adaptable necesario, ya que el editor universal ofrece una función intuitiva de arrastrar y soltar.

1. Haga clic en **Publicar** para volver a publicar el formulario después de agregar el componente **[!UICONTROL Captcha (invisible)]**.

   ![volver a publicar formulario](/help/edge/docs/forms/universal-editor/assets/publish-form.png)

Ahora puede ver el formulario con el servicio reCAPTCHA en la siguiente URL:
`https://<branch>--<repo>--<owner>.aem.live/content/forms/af/<form-name`.

![Formulario con reCAPTCHA](/help/edge/docs/forms/universal-editor/assets/form-with-recaptcha.png)

## Preguntas frecuentes

* **¿Qué sucede si un usuario no crea una configuración de nube reCAPTCHA?**

  **A**: Si un usuario no crea una configuración de nube reCAPTCHA, el servidor de AEM busca la configuración de nube reCAPTCHA en el contenedor de configuración global. Si no existe ninguna configuración en el contenedor de configuración global, el servidor de AEM genera un error.

* **¿Qué sucede si un usuario crea varias configuraciones de nube reCAPTCHA?**
  **A**: Si un usuario crea más de una configuración de nube reCAPTCHA, el sistema selecciona automáticamente la primera configuración reCAPTCHA creada.

* **¿Por qué las modificaciones o cambios no son visibles en la dirección URL publicada?**
Si las modificaciones o cambios no son visibles en la dirección URL publicada, asegúrese de que el formulario se vuelva a publicar para aplicar las actualizaciones.

* **¿Qué servicio reCAPTCHA admite Edge Delivery Services Forms?**
  **A**: Edge Delivery Services Forms solo admite el servicio reCAPTCHA basado en puntuación proporcionado por Google.


## Ver también

{{see-more-forms-eds}}
