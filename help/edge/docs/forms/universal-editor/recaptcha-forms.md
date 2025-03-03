---
title: Uso de reCAPTCHA con Edge Delivery Services para AEM Forms as a Cloud Service
description: Uso de Google reCAPTCHA en un formulario para Edge Delivery Services para AEM Forms
feature: Edge Delivery Services
keywords: reCAPTCHA en formularios, Uso de reCAPTCHA en el editor universal, Adición de reCAPTCHA en formularios
role: Admin, Architect, Developer
exl-id: 1f28bd13-133f-487e-8b01-334be7c08a3f
source-git-commit: 0c6f024594e1b1fd98174914d2c0714dffecb241
workflow-type: tm+mt
source-wordcount: '1273'
ht-degree: 96%

---


# Uso de reCAPTCHA en la creación de WYSIWYG

<span class="preview"> Esta característica está disponible a través del programa de acceso anticipado. Para solicitar acceso, envía un correo electrónico desde tu dirección oficial a <a href="mailto:aem-forms-ea@adobe.com">aem-forms-ea@adobe.com</a> con tu nombre de organización de GitHub y el nombre del repositorio. Por ejemplo, si la dirección URL del repositorio es https://github.com/adobe/abc, el nombre de la organización es adobe y el nombre del repositorio es abc.</span>


CAPTCHA (prueba de Turing completamente automática y pública para diferenciar ordenadores de humanos, por sus siglas en inglés) es una herramienta popular utilizada para proteger los sitios web de actividades fraudulentas, spam y uso indebido.

Por ejemplo, piense en un formulario que calcule el impuesto en función de deducciones adicionales y el tipo impositivo. En estos casos, existe el riesgo de que usuarios maliciosos exploten el formulario para enviar correos electrónicos de phishing o inundarlo con contenido irrelevante o dañino mediante bots de spam. La integración de CAPTCHA ofrece una seguridad añadida al verificar que los envíos proceden de usuarios genuinos, lo que minimiza de forma eficaz las entradas de spam.

![Google reCAPTCHA](/help/edge/docs/forms/universal-editor/assets/google-recaptcha.png)

En formularios de Edge Delivery Services, el bloque de formulario le permite [conectar Google reCAPTCHA con formularios](#connect-forms-with-recaptcha-service-by-google) mediante el componente **Captcha(Invisible)** para distinguir entre humanos y bots. Esta funcionalidad ayuda a los autores a proteger sus formularios del spam y del uso indebido.

## Conexión de formularios con el servicio reCAPTCHA de Google

Puede crear formularios de Edge Delivery Services para implementar el servicio reCAPTCHA proporcionado por Google. Según sus necesidades, puede configurar uno de los siguientes servicios de reCAPTCHA para sus formularios de Edge Delivery Services:

* [reCAPTCHA Enterprise](#configure-recaptcha-enterprise)
* [reCAPTCHA](#configure-recaptcha)

>[!NOTE]
>
> Para obtener más información sobre cómo funciona reCAPTCHA, consulte [Google reCAPTCHA](https://developers.google.com/recaptcha/).

### Configuración de reCAPTCHA Enterprise

reCAPTCHA Enterprise es un servicio prémium de detección y prevención de fraude de nivel empresarial que ofrece Google. Se basa en reCAPTCHA (basado en puntuación), pero proporciona funciones adicionales, escalabilidad y personalización para satisfacer las complejas necesidades de las empresas.

#### Antes de comenzar

Antes de configurar Google reCAPTCHA Enterprise para formularios de Edge Delivery Services, asegúrese de haber completado los siguientes pasos:

1. Cree o seleccione un [Proyecto de Google Cloud](https://cloud.google.com/recaptcha/docs/prepare-environment#before-you-begin) y recupere el [ID de proyecto](https://support.google.com/googleapi/answer/7014113?hl=en#:~:text=To%20locate%20your%20project%20ID,a%20member%20of%20are%20displayed).

1. [Habilite la API de reCAPTCHA Enterprise](https://cloud.google.com/recaptcha/docs/prepare-environment#enable-api) para su proyecto de Google Cloud y [cree una clave de API](https://console.cloud.google.com/apis/credentials).

1. Cree una [clave de sitio para su proyecto de Google Cloud](https://console.cloud.google.com/security/recaptcha) y copie la clave de sitio.

Una vez que tenga estas credenciales, puede continuar con la configuración de reCAPTCHA Enterprise para sus formularios:

1. [Crear un contenedor de configuración en la nube](#1-create-cloud-configuration-container)
1. [Cree la configuración del servicio en la nube para reCAPTCHA Enterprise](#2-create-the-cloud-service-configuration-for-recaptcha-enterprise)

#### 1. Crear un contenedor de configuración en la nube

Para crear el contenedor de configuración en la nube, siga estos pasos:

1. Inicie sesión en su instancia de autor.
1. Vaya a **[!UICONTROL Herramientas]** ![tools-1](/help/forms/assets/tools-1.png) > **[!UICONTROL General]** > **[!UICONTROL Explorador de configuración]**.

   ![Contenedor de configuración en la nube](/help/edge/docs/forms/universal-editor/assets/recaptcha-general-configuration.png)

1. En el **[!UICONTROL Explorador de configuración]**, vaya a su formulario y seleccione **[!UICONTROL Propiedades]**.

   ![Propiedades de configuración en la nube](/help/edge/docs/forms/universal-editor/assets/general-configuration-properties.png)

1. En el cuadro de diálogo **[!UICONTROL Propiedades de configuración]**, habilite **[!UICONTROL Configuraciones de nube]**.

1. Seleccione **[!UICONTROL Guardar y cerrar]** para guardar la configuración y salir del cuadro de diálogo.

   ![Habilitar propiedades de configuración de nube](/help/edge/docs/forms/universal-editor/assets/enable-cloud-configurations.png)
`
Después de crear el contenedor de configuración en la nube, publíquelo.

   ![Publicar configuración de la nube](/help/edge/docs/forms/universal-editor/assets/publish-cloud-configuration.png)

#### 2. Crear la configuración del servicio en la nube para reCAPTCHA Enterprise

Para crear la configuración del servicio en la nube para reCAPTCHA Enterprise, realice los siguientes pasos:

1. Inicie sesión en su instancia de autor.
1. Vaya a **[!UICONTROL Herramientas]** ![tools-1](/help/forms/assets/tools-1.png) > **[!UICONTROL Cloud Services]** > **[!UICONTROL reCAPTCHA]**.

   ![Configuración en la nube de Recaptcha](/help/edge/docs/forms/universal-editor/assets/recaptcha-cloud-configuration.png)

   Se abrirá el cuadro de diálogo **Configuraciones**.

1. Vaya al formulario y seleccione **[!UICONTROL Crear]**.

   ![Configuración de Captcha](/help/edge/docs/forms/universal-editor/assets/create-captcha-confguration.png)

   Se abre el cuadro de diálogo **[!UICONTROL Crear configuración de reCAPTCHA]**.

   ![reCAPTCHA Enterprise](/help/edge/docs/forms/universal-editor/assets/recaptcha-enterprise.png)

1. Seleccione la versión como [!DNL ReCAPTCHA Enterprise] y especifique el título, el nombre, el identificador de proyecto, la clave del sitio y la clave de API.

   >[!NOTE]
   >
   > Puede obtener el ID del proyecto, la clave del sitio y la clave de API de la sección [Antes de empezar](#before-you-start) para reCAPTCHA Enterprise.

1. Seleccione **[!UICONTROL Tipo de clave]** como **Clave de sitio basada en la puntuación**.
1. Especifique una [puntuación de umbral en el rango de 0 a 1](https://cloud.google.com/recaptcha/docs/interpret-assessment-website#interpret_scores). Las puntuaciones superiores o iguales a las puntuaciones de umbral identifican la interacción humana; de lo contrario, se considera que es una interacción de bot.
1. Seleccione **[!UICONTROL Crear]** para crear la configuración del servicio en la nube.

   Después de crear la configuración en la nube de reCAPTCHA, publíquela.

   ![Publicación de la configuración de Recaptcha](/help/edge/docs/forms/universal-editor/assets/publisg-recaptcha-configuration.png)

Ahora puede crear o editar un formulario y añadir el componente reCAPTCHA mediante la función de creación basada en WYSIWYG. Para obtener instrucciones detalladas sobre la integración de Google reCAPTCHA en el formulario, consulte [Uso de reCAPTCHA en el formulario](#use-recaptcha-in-your-form).

## Configuración de reCAPTCHA

reCAPTCHA es un servicio gratuito ofrecido por Google que ayuda a los sitios web a detectar y evitar el tráfico abusivo, incluidos los bots y el correo no deseado. Admite una versión basada en puntuaciones que funciona en segundo plano y asigna una puntuación de riesgo (de 0,0 a 1,0) a cada interacción del usuario. Las puntuaciones superiores o iguales a las puntuaciones de umbral identifican la interacción humana; de lo contrario, se considera que es una interacción de bot.

#### Antes de empezar

Antes de configurar Google reCAPTCHA para los formularios de Edge Delivery Services, recupere el [par de claves de la API de reCAPTCHA de la consola de Google](https://www.google.com/recaptcha/admin). El par incluye una clave del Sitio y una clave Secreta.

>[!NOTE]
>
> * Los formularios de Edge Delivery Services solo admiten la versión **basada en puntuaciones de reCAPTCHA**.

Cuando tenga el par de claves de la API, puede configurar reCAPTCHA para los formularios:

1. [Crear un contenedor de configuración en la nube](#1-create-cloud-configuration-container-1)
1. [Crear la configuración del servicio en la nube para reCAPTCHA](#2-create-the-cloud-service-configuration-for-recaptcha)

#### 1. Crear un contenedor de configuración en la nube

Para crear el contenedor de configuración en la nube, siga estos pasos:

1. Inicie sesión en su instancia de autor.
1. Vaya a **[!UICONTROL Herramientas]** ![tools-1](/help/forms/assets/tools-1.png) > **[!UICONTROL General]** > **[!UICONTROL Explorador de configuración]**.

   ![Contenedor de configuración en la nube](/help/edge/docs/forms/universal-editor/assets/recaptcha-general-configuration.png)

1. En el **[!UICONTROL Explorador de configuración]**, vaya a su formulario y seleccione **[!UICONTROL Propiedades]**.

   ![Propiedades de configuración en la nube](/help/edge/docs/forms/universal-editor/assets/general-configuration-properties.png)

1. En el cuadro de diálogo **[!UICONTROL Propiedades de configuración]**, habilite **[!UICONTROL Configuraciones de nube]**.

1. Seleccione **[!UICONTROL Guardar y cerrar]** para guardar la configuración y salir del cuadro de diálogo.

   ![Habilitar propiedades de configuración en la nube](/help/edge/docs/forms/universal-editor/assets/enable-cloud-configurations.png)

   Después de crear el contenedor de configuración en la nube, publíquelo.

   ![Publicar configuración en la nube](/help/edge/docs/forms/universal-editor/assets/publish-cloud-configuration.png)

#### 2. Crear la configuración del servicio en la nube para reCAPTCHA

Para crear la configuración del servicio en la nube para reCAPTCHA, realice los siguientes pasos:

1. Inicie sesión en su instancia de autor.
1. Vaya a **[!UICONTROL Herramientas]** ![tools-1](/help/forms/assets/tools-1.png) > **[!UICONTROL Cloud Services]** > **[!UICONTROL reCAPTCHA]**.

   ![Configuración en la nube de Recaptcha](/help/edge/docs/forms/universal-editor/assets/recaptcha-cloud-configuration.png)

   Se abrirá el cuadro de diálogo **Configuraciones**.

1. Vaya al formulario y seleccione **[!UICONTROL Crear]**.

   ![Configuración de Captcha](/help/edge/docs/forms/universal-editor/assets/create-captcha-confguration.png)

   Se abre el cuadro de diálogo **[!UICONTROL Crear configuración de reCAPTCHA]**.

   ![reCAPTCHA Enterprise](/help/edge/docs/forms/universal-editor/assets/recaptcha.png)

1. Seleccione la versión como [!DNL ReCAPTCHA v2] y especifique el Título y el Nombre.
1. Indique la clave del sitio y la clave secreta.

   >[!NOTE]
   >
   > Puede obtener la clave de sitio y la clave secreta de la sección [Antes de comenzar](#before-you-begin) para reCAPTCHA.

1. Seleccione **[!UICONTROL Crear]** para crear la configuración del servicio en la nube.

   Después de crear la configuración en la nube de reCAPTCHA, publíquela.

   ![Publicación de configuración de Recaptcha](/help/edge/docs/forms/universal-editor/assets/publisg-recaptcha-configuration.png)

Ahora puede crear y editar un formulario y añadir el componente reCAPTCHA mediante la función de creación basada en WYSIWYG. Para obtener instrucciones detalladas sobre la integración de Google reCAPTCHA en el formulario, consulte [Uso de reCAPTCHA en el formulario](#use-recaptcha-in-your-form).

### Uso de reCAPTCHA en el formulario

Para crear un formulario y añadir el componente reCAPTCHA (invisible), realice los siguientes pasos:

1. Abra un formulario en el Editor universal para editarlo.
1. Vaya a la sección del Formulario adaptable añadido en el árbol de contenido.
1. Haga clic en el icono de **[!UICONTROL Añadir]** y añada el componente **[!UICONTROL Captcha (Invisble)]** de la lista **Componentes de formularios adaptables**.

   ![Adición de componente reCAPTCHA](/help/edge/docs/forms/universal-editor/assets/add-recaptcha-component.png)

   También puede arrastrar y soltar los componentes de formularios adaptables necesarios, ya que el Editor universal ofrece una función intuitiva de arrastrar y soltar.

1. Haga clic en **Publicar** para volver a publicar el formulario después de agregar el componente **[!UICONTROL Captcha (Invisible)]**.

   ![volver a publicar formulario](/help/edge/docs/forms/universal-editor/assets/publish-form.png)

Ahora puede ver el formulario con el servicio reCAPTCHA en la siguiente URL:
`https://<branch>--<repo>--<owner>.aem.live/content/forms/af/<form-name`.

![Formulario con reCAPTCHA](/help/edge/docs/forms/universal-editor/assets/form-with-recaptcha.png)

## Preguntas frecuentes

* **¿Qué sucede si un usuario no crea una configuración de nube reCAPTCHA?**

  **R**: Si un usuario no crea una configuración de nube reCAPTCHA, el servidor de AEM busca la configuración de nube reCAPTCHA en el contenedor de configuración global. Si no existe ninguna configuración en el contenedor de configuración global, el servidor de AEM genera un error.

* **¿Qué sucede si un usuario crea varias configuraciones de nube reCAPTCHA?**
  **R**: Si un usuario crea más de una configuración de nube reCAPTCHA, el sistema selecciona automáticamente la primera configuración reCAPTCHA creada.

* **¿Por qué las modificaciones o cambios no son visibles en la dirección URL publicada?**
Si las modificaciones o cambios no son visibles en la dirección URL publicada, asegúrese de que el formulario se vuelva a publicar para aplicar las actualizaciones.

* **¿Qué servicio reCAPTCHA admite formularios de Edge Delivery Services?**
  **R**: Los formularios de Edge Delivery Services solo admiten el servicio reCAPTCHA basado en puntuación proporcionado por Google.


## Véase también

{{universal-editor-see-also}}

