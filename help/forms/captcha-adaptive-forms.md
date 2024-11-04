---
title: Utilizar el servicio de Captcha en los formularios adaptables
description: Aprenda a configurar el servicio reCAPTCHA de Google para un formulario adaptable.
uuid: 0e11e98a-12ac-484c-b77f-88ebdf0f40e5
contentOwner: vishgupt
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: adaptive_forms, author
feature: Adaptive Forms, Foundation Components
role: User, Developer
source-git-commit: e6f986e014e45fad461721d84f18cc49a7bb434e
workflow-type: tm+mt
source-wordcount: '1742'
ht-degree: 100%

---


# Usar reCAPTCHA en formularios adaptables {#using-reCAPTCHA-in-adaptive-forms}

<span class="preview"> Adobe recomienda utilizar la captura de datos moderna y ampliable [Componentes principales](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=es) para [crear un nuevo formulario adaptable](/help/forms/creating-adaptive-form-core-components.md) o [añadir formularios adaptables a páginas de AEM Sites](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md). Estos componentes representan un avance significativo en la creación de formularios adaptables, lo que garantiza experiencias de usuario impresionantes. Este artículo describe un enfoque más antiguo para crear Formularios adaptables con componentes de base. </span>


| Versión | Vínculo del artículo |
| -------- | ---------------------------- |
| AEM 6.5 | [Haga clic aquí](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-basic-authoring/captcha-adaptive-forms.html?lang=es) |
| AEM as a Cloud Service | Este artículo |
| Se aplica a lo siguiente: | Formulario adaptable basado en componentes de base. <br> Para los formularios adaptables basados en componentes principales, [Haga clic aquí](/help/forms/captcha-adaptive-forms-core-components.md). |


CAPTCHA (prueba de Turing completamente automática y pública para diferenciar ordenadores de humanos) es un programa que se utiliza comúnmente en transacciones en línea para distinguir entre humanos y programas o bots automatizados. Plantea un desafío y evalúa la respuesta del usuario para determinar si es un humano o un bot que interactúa con el sitio. Evita que el usuario continúe si la prueba falla y ayuda a que las transacciones en línea sean seguras al impedir que los bots publiquen contenido no deseado o con fines malintencionados.

AEM Forms as a Cloud Service es compatible con las siguientes soluciones CAPTCHA:

* [Google reCAPTCHA](#configure-recaptcha-service-by-google)
* [Cloudflare Turnstile](/help/forms/integrate-adaptive-forms-turnstile.md)
* [hCaptcha](/help/forms/integrate-adaptive-forms-hcaptcha.md)

## Configuración del servicio reCAPTCHA de Google {#google-reCAPTCHA}

Los creadores de formularios pueden utilizar el servicio reCAPTCHA de Google para implementar el reCAPTCHA en los formularios adaptables. Ofrece funcionalidades de Captcha avanzadas para proteger su sitio. Para obtener más información sobre cómo funciona reCAPTCHA, consulte [Google reCAPTCHA](https://developers.google.com/recaptcha/). AEM Forms es compatible con [!DNL reCAPTCHA v2] y [!DNL reCAPTCHA Enterprise]. No existe compatibilidad con ninguna otra versión. También hay que tener en cuenta que reCAPTCHA en formularios adaptables no es compatible con el modo sin conexión en la aplicación [!DNL AEM Forms]. Según sus necesidades, puede configurar el servicio reCAPTCHA para habilitar lo siguiente:

![reCAPTCHA](/help/forms/assets/recaptcha_new.png)

* [El servicio reCAPTCHA Enterprise en AEM Forms](#steps-to-implement-reCAPTCHA-enterprise-in-forms)
* [El servicio reCAPTCHA v2 en AEM Forms](#steps-to-implement-reCAPTCHA-v2-in-forms)


### Configuración de reCAPTCHA Enterprise  {#steps-to-implement-reCAPTCHA-enterprise-in-forms}

1. Cree o seleccione un [Proyecto de Google Cloud](https://cloud.google.com/recaptcha-enterprise/docs/set-up-non-google-cloud-environments-api-keys#before-you-begin) y habilite la [API de reCAPTCHA Enterprise](https://cloud.google.com/recaptcha-enterprise/docs/set-up-non-google-cloud-environments-api-keys#enable-the-recaptcha-enterprise-api).
1. Obtenga el [ID de proyecto](https://support.google.com/googleapi/answer/7014113?hl=en#:~:text=To%20locate%20your%20project%20ID,a%20member%20of%20are%20displayed) y cree una [clave de API](https://cloud.google.com/recaptcha-enterprise/docs/set-up-non-google-cloud-environments-api-keys#create_an_api_key) y una [clave del sitio para sitios web](https://cloud.google.com/recaptcha-enterprise/docs/create-key#create-key).
1. Crear un contenedor de configuración para los servicios en la nube.

   1. Vaya a **[!UICONTROL Herramientas > General > Explorador de configuración]**.
   1. Seleccione una carpeta o cree una carpeta y habilítela para las configuraciones de nube mediante los siguientes pasos:
      1. En el Explorador de configuración, selecciona la carpeta y selecciona	**[!UICONTROL Propiedades]**.
      1. En el cuadro de diálogo Propiedades de configuración, habilite **[!UICONTROL Configuraciones de nube]**.
      1. Selecciona **[!UICONTROL Guardar y cerrar]** para guardar la configuración y salir del cuadro de diálogo.

1. Configure el servicio en la nube para [!DNL reCAPTCHA Enterprise].

   1. En la instancia de autor Experience Manager, vaya a ![herramientas-1](assets/tools-1.png) > **[!UICONTROL Cloud Services]**.
   1. Selecciona **[!UICONTROL reCAPTCHA]**. Se abre la página de configuración. Selecciona el contenedor de configuración que ha creado y seleccione **[!UICONTROL Crear]**.
   1. Seleccione versión como [!DNL reCAPTCHA Enterprise] y especifique el nombre, el ID del proyecto, la clave del sitio y la clave de la API (obtenida en el paso 2) para el servicio empresarial de reCAPTCHA.
   1. Seleccione el tipo de clave que debe ser el mismo que la clave de sitio configurada en el [proyecto de Google Cloud](https://cloud.google.com/recaptcha-enterprise/docs/set-up-non-google-cloud-environments-api-keys#before-you-begin). Por ejemplo, **clave de sitio de casilla** o **clave de sitio basada en puntuación**.
   1. Especifique una [puntuación de umbral en el rango de 0 a 1](https://cloud.google.com/recaptcha-enterprise/docs/interpret-assessment#interpret_scores). Las puntuaciones superiores o iguales a las puntuaciones de umbral identifican la interacción humana; de lo contrario, se considera interacción de bots.
   1. Selecciona **[!UICONTROL Crear]** para crear la configuración del servicio en la nube.

<!--
    1. In the Edit Component dialog, specify the name, project ID, site key, API key (obtained in steps 2 and 3), select the key type, and enter the threshold score. Select **[!UICONTROL Save Settings]** and then select **[!UICONTROL OK]** to complete the configuration.
-->

Una vez habilitado el servicio empresarial de reCAPTCHA, estará disponible para su uso en formularios adaptables. Ver [el uso de CAPTCHA en los formularios adaptables](#using-reCAPTCHA).

<!--
![reCAPTCHA Enterprise](/help/forms/assets/recaptcha1-enterprise.png)
-->

### Configuración de Google reCAPTCHA v2 {#steps-to-implement-reCAPTCHA-v2-in-forms}

1. Obtener el [par de claves de la API reCAPTCHA](https://www.google.com/recaptcha/admin) de Google. Incluye una **clave del sitio** y una **clave secreta**.
1. Crear un contenedor de configuración para los servicios en la nube.
   1. Vaya a **[!UICONTROL Herramientas > General > Explorador de configuración]**.
   1. Seleccione una carpeta o cree una carpeta y habilítela para las configuraciones de nube mediante los siguientes pasos:
      1. En el Explorador de configuración, selecciona la carpeta y selecciona	**[!UICONTROL Propiedades]**.
      1. En el cuadro de diálogo Propiedades de configuración, habilite **[!UICONTROL Configuraciones de nube]**.
      1. Seleccione **[!UICONTROL Guardar y cerrar]** para guardar la configuración y salir del cuadro de diálogo.

1. Configure el servicio en la nube para el reCAPTCHA v2.

   1. En la instancia de autor de AEM, vaya a ![tools-1](assets/tools-1.png) > **Cloud Services**.
   1. Seleccione **[!UICONTROL reCAPTCHA]**. Se abre la página de configuración. Seleccione el contenedor de configuración que ha creado y seleccione **[!UICONTROL Crear]**.
   1. Selecciona la versión como [!DNL reCAPTCHA v2], especifica el nombre, la clave del sitio y la clave secreta para el servicio reCAPTCHA (obtenidas en el Paso 1) y selecciona **[!UICONTROL Crear]** para crear la configuración del servicio en la nube.
   1. En el cuadro de diálogo Editar componente, especifique el sitio y las claves secretas obtenidas en el paso 1. Selecciona **[!UICONTROL Guardar configuración]** y, a continuación, **OK** para completar la configuración.

   Una vez configurado el servicio reCAPTCHA, estará disponible para su uso en formularios adaptables. Para obtener más información, consulte [el uso de Captcha en los formularios adaptables](#using-reCAPTCHA).

<!--![reCAPTCHA v2](/help/forms/assets/recaptcha-v2.png)-->


## Usar Google reCAPTCHA en formularios adaptables {#using-reCAPTCHA}

Para utilizar Google reCAPTCHA en un formulario adaptable:

1. Abra un formulario adaptable en modo Edición.

   >[!NOTE]
   >
   >Asegúrese de que el contenedor de configuración seleccionado al crear el formulario adaptable contenga el servicio en la nube reCAPTCHA. También puede editar las propiedades del formulario adaptable para cambiar el contenedor de configuración asociado al formulario.

1. Desde el explorador de componentes, arrastre y suelte el componente **Captcha** en el formulario adaptable.

   >[!NOTE]
   >
   >* No se puede usar más de un componente Captcha en un formulario adaptable. Además, no se recomienda utilizar un Captcha en un panel marcado si tiene carga diferida o en un fragmento.
   >* El reCAPTCHA tiene un plazo y caduca en unos minutos. Por lo tanto, se recomienda colocar el componente del Captcha justo antes del botón Enviar en el formulario adaptable.

1. Selecciona el componente Captcha que has añadido y selecciona ![cmppr](assets/cmppr.png) para editar sus propiedades.
1. Especifique un título para el widget CAPTCHA. El valor predeterminado es **Captcha**. Seleccione **Ocultar título** si no desea que aparezca el título.
1. En el menú desplegable **servicio Captcha**, seleccione **reCAPTCHA** para habilitarlo si lo configuró como se describe en el [servicio reCAPTCHA de Google](#google-reCAPTCHA).
1. Seleccione una configuración en la lista desplegable Configuración para **reCAPTCHA empresarial** o **reCAPTCHA v2**
   1. Si selecciona la versión **reCAPTCHA empresarial**, el tipo de clave puede ser **casilla de verificación** o **basado en puntuación**, se compone de la selección realizada al configurar la [clave del sitio para sitios web](https://cloud.google.com/recaptcha-enterprise/docs/create-key#create-key):

   >[!NOTE]
   >
   >* En la configuración de nube con **tipo de clave** como **casilla de verificación**, el mensaje de error personalizado aparece como un mensaje en línea si falla la validación del captcha.
   >* En la configuración en la nube con **tipo de clave** como **basado en puntuación**, el mensaje de error personalizado se muestra como un mensaje emergente si falla la validación del captcha.

   1. Puede seleccionar el tamaño como **[!UICONTROL normal]** y **[!UICONTROL compacto]**.
   1. Puede seleccionar una **[!UICONTROL Referencia de enlace]**. En **[!UICONTROL Referencia de enlace]** los datos enviados son datos enlazados; de lo contrario, no lo son. A continuación se muestran ejemplos XML de datos no enlazados y enlazados (con referencia de enlace como SSN) respectivamente, cuando se envía un formulario.

   ```xml
           <?xml version="1.0" encoding="UTF-8" standalone="no"?>
           <afData>
           <afUnboundData>
               <data>
                   <captcha16820607953761>
                       <captchaType>reCaptchaEnterprise</captchaType>
                       <captchaScore>0.9</captchaScore>
                   </captcha16820607953761>
               </data>
           </afUnboundData>
           <afBoundData>
               <Root
                   xmlns:xfa="http://www.xfa.org/schema/xfa-data/1.0/"
                   xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
                   <PersonalDetails>
                       <SSN>371237912</SSN>
                       <FirstName>Sarah </FirstName>
                       <LastName>Smith</LastName>
                   </PersonalDetails>
                   <OtherInfo>
                       <City>California</City>
                       <Address>54 Residency</Address>
                       <State>USA</State>
                       <Zip>123112</Zip>
                   </OtherInfo>
               </Root>
           </afBoundData>
           <afSubmissionInfo>
               <stateOverrides/>
               <signers/>
               <afPath>/content/dam/formsanddocuments/captcha-form</afPath>
               <afSubmissionTime>20230608034928</afSubmissionTime>
           </afSubmissionInfo>
           </afData>
   ```

   ```xml
           <?xml version="1.0" encoding="UTF-8" standalone="no"?>
           <afData>
           <afUnboundData>
               <data/>
           </afUnboundData>
           <afBoundData>
               <Root
                   xmlns:xfa="http://www.xfa.org/schema/xfa-data/1.0/"
                   xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
                   <PersonalDetails>
                       <SSN>
                           <captchaType>reCaptchaEnterprise</captchaType>
                           <captchaScore>0.9</captchaScore>
                       </SSN>
                       <FirstName>Sarah</FirstName>
                       <LastName>Smith</LastName>
                   </PersonalDetails>
                   <OtherInfo>
                       <City>California</City>
                       <Address>54 Residency</Address>
                       <State>USA</State>
                       <Zip>123112</Zip>
                   </OtherInfo>
               </Root>
           </afBoundData>
           <afSubmissionInfo>
               <stateOverrides/>
               <signers/>
               <afPath>/content/dam/formsanddocuments/captcha-form</afPath>
               <afSubmissionTime>20230608035111</afSubmissionTime>
           </afSubmissionInfo>
           </afData>
   ```

   Si selecciona la versión **reCAPTCHA v2**:
   1. Puede seleccionar el tamaño **[!UICONTROL normal]** o **[!UICONTROL compacto]** para el widget reCAPTCHA.
   1. También puede seleccionar la opción **[!UICONTROL Invisible]** para mostrar la comprobación de CAPTCHA solamente en el caso de una actividad sospechosa.

   El servicio reCAPTCHA está habilitado en el formulario adaptable. Puede obtener una vista previa del formulario y ver cómo funciona CAPTCHA. El distintivo **protegido por reCAPTCHA**, que se muestra a continuación, aparece en los formularios protegidos.
   ![Distintivo protegido por reCAPTCHA de Google](/help/forms/assets/google-recaptcha-v2.png)

1. Guarde las propiedades.

>[!NOTE]
> 
> No seleccione **[!UICONTROL Predeterminado]** en el menú desplegable del servicio Captcha, ya que el servicio Captcha de AEM predeterminado es obsoleto.

>[!VIDEO](https://video.tv.adobe.com/v/3422641/recaptcha-google-adaptive-forms/?quality=12&learn=on)

### Mostrar u ocultar el componente CAPTCHA en función de las reglas {#show-hide-captcha}

Puede seleccionar mostrar u ocultar el componente CAPTCHA en función de las reglas que aplique en un componente de un formulario adaptable. Selecciona el componente, ![editar reglas](assets/edit-rules-icon.svg) y **[!UICONTROL Crear]** para crear una regla. Para obtener más información sobre la creación de reglas, consulte [Editor de reglas](rule-editor.md).

Por ejemplo, el componente CAPTCHA debe mostrarse en un formulario adaptable solo si el campo Valor de moneda del formulario tiene un valor superior a 25 000.

Selecciona **[!UICONTROL Valor de moneda]** en el formulario y crea las siguientes reglas:

![Mostrar u ocultar reglas](assets/rules-show-hide-captcha.png)

>[!NOTE]
>
> Cuando selecciona una configuración de reCAPTCHA versión 2 y el tamaño se establece en [!UICONTROL Invisible], la opción mostrar/ocultar permanece deshabilitada.

### Validar CAPTCHA {#validate-captcha}

Puede validar el CAPTCHA en un formulario adaptable al enviar el formulario o basar la validación CAPTCHA en las acciones y condiciones del usuario.

#### Validar el CAPTCHA al enviar el formulario {#validation-form-submission}

Para validar un CAPTCHA automáticamente al enviar un formulario adaptable:

1. Selecciona el componente CAPTCHA y ![cmppr](assets/configure-icon.svg) para ver las propiedades del componente.
1. En la sección **[!UICONTROL Validar CAPTCHA]**, seleccione **[!UICONTROL Validar el CAPTCHA al enviar el formulario]**.
1. Selecciona ![Listo](assets/save_icon.svg) para guardar las propiedades del componente.

#### Validar el CAPTCHA en las acciones y condiciones del usuario {#validate-captcha-user-action}

Para validar un CAPTCHA basado en condiciones y acciones del usuario:

1. Seleccione el componente CAPTCHA y ![cmppr](assets/configure-icon.svg) para ver las propiedades del componente.
1. En la sección **[!UICONTROL Validar CAPTCHA]**, selecciona **[!UICONTROL Validar el CAPTCHA en una acción del usuario]**.
1. Seleccione ![Listo](assets/save_icon.svg) para guardar las propiedades del componente.

[!DNL Experience Manager Forms] ofrece la API `ValidateCAPTCHA` para validar un CAPTCHA con condiciones predefinidas. Puede invocar la API utilizando una acción de envío personalizada o definiendo reglas sobre los componentes de un formulario adaptable.

El siguiente es un ejemplo de un API `ValidateCAPTCHA` para validar un CAPTCHA con condiciones predefinidas:

```javascript
if (slingRequest.getParameter("numericbox1614079614831").length() >= 5) {
     GuideCaptchaValidatorProvider apiProvider = sling.getService(GuideCaptchaValidatorProvider.class);
        String formPath = slingRequest.getResource().getPath();
        String captchaData = slingRequest.getParameter(GuideConstants.GUIDE_CAPTCHA_DATA);
        if (!apiProvider.validateCAPTCHA(formPath, captchaData).isCaptchaValid()){
            response.setStatus(400);
            return;
        }
    }
```

El ejemplo significa que la API `ValidateCAPTCHA` valida el CAPTCHA en el formulario solo si el número de dígitos en el cuadro numérico especificado por el usuario mientras rellena el formulario es mayor de 5.

**Opción 1: Usar la API [!DNL Experience Manager Forms] ValidateCAPTCHA para validar el CAPTCHA mediante una acción de envío personalizada**

Siga estos pasos para usar la API `ValidateCAPTCHA` para validar el CAPTCHA con una acción de envío personalizada:

1. Añada el script que incluya la API `ValidateCAPTCHA` para la acción de envío personalizada. Para obtener más información acerca de las acciones de envío personalizadas, consulte [Crear una acción de envío personalizada para formularios adaptables](custom-submit-action-form.md).
1. Seleccione el nombre de la acción de envío personalizada en la lista desplegable **[!UICONTROL Enviar acción]** en las propiedades de **[!UICONTROL Envío]** de un formulario adaptable.
1. Selecciona **[!UICONTROL Enviar]**. El CAPTCHA se valida según las condiciones definidas en la API `ValidateCAPTCHA` de la acción de envío personalizada.

**Opción 2: Usar la API [!DNL Experience Manager Forms] ValidateCAPTCHA para validar el CAPTCHA en una acción del usuario antes de enviar el formulario**

También puede invocar la API `ValidateCAPTCHA` al aplicar reglas en un componente de un formulario adaptable.

Por ejemplo, añade un botón **[!UICONTROL Validar CAPTCHA]** en un formulario adaptable y crea una regla para invocar un servicio haciendo clic en un botón.

La siguiente imagen ilustra cómo puede invocar un servicio al hacer clic en un botón **[!UICONTROL Validar CAPTCHA]**:

![Validar CAPTCHA](assets/captcha-validation1.gif)

Puede invocar el servlet personalizado que incluye la API `ValidateCAPTCHA` mediante el editor de reglas y habilitar o deshabilitar el botón de envío del formulario adaptable en función del resultado de validación.

Del mismo modo, puede utilizar el editor de reglas para incluir un método personalizado para validar el CAPTCHA en un formulario adaptable.

<!--

### Add custom CAPTCHA services {#add-custom-captcha-service}

[!DNL Experience Manager Forms] provides reCAPTCHA as the CAPTCHA service. However, you can add a custom service to display in the **[!UICONTROL CAPTCHA Service]** drop-down list.  

The following is a sample implementation of the interface to add additional CAPTCHA service to your Adaptive Form:

```javascript
package com.adobe.aemds.guide.service;

import org.osgi.annotation.versioning.ConsumerType;

/**
 * An interface to provide captcha validation at server side in Adaptive Form
 * This interface can be used to provide custom implementation for different captcha services.
 */
@ConsumerType
public interface GuideCaptchaValidator {
    /**
     * This method should define the actual validation logic of the captcha
     * @param captchaPropertyNodePath path to the node with CAPTCHA configurations inside form container
     * @param userResponseToken  The user response token provided by the CAPTCHA from client-side
     *
     * @return  {@link GuideCaptchaValidationResult} validation result of the captcha
     */
     GuideCaptchaValidationResult validateCaptcha(String captchaPropertyNodePath, String userResponseToken);

    /**
     * Returns the name of the captcha validator. This should be unique among the different implementations
     * @return  name of the captcha validator
     */
     String getCaptchaValidatorName();
}
```

`captchaPropertyNodePath` refers to the resource path of the CAPTCHA component in the Sling repository. Use this property to include details specific to the CAPTCHA component. For example, `captchaPropertyNodePath` includes information for the reCAPTCHA cloud configuration configured on the CAPTCHA component. The cloud configuration information provides **[!UICONTROL Site Key]** and **[!UICONTROL Secret Key]** settings for implementing the reCAPTCHA service.

`userResponseToken` refers to the `g_recaptcha_response` that gets generated after solving a CAPTCHA in a form. -->

### Editar dominio de servicio reCAPTCHA {#reCAPTCHA-service-domain}

El servicio reCAPTCHA utiliza `https://www.recaptcha.net/` como dominio predeterminado. Puede modificar la configuración para establecer `https://www.google.com/` o cualquier nombre de dominio personalizado para cargar, procesar y validar el servicio reCAPTCHA.

Establezca la propiedad **[!UICONTROL af.cloudservices.recaptcha.domain]** de la configuración **[!UICONTROL Configuración del canal web de comunicaciones interactivas y formularios adaptables]** para especificar `https://www.google.com/` o cualquier otro nombre de dominio personalizado. El siguiente archivo JSON muestra un ejemplo:

```json
{
  "af.cloudservices.recaptcha.domain": "https://www.google.com/"
}
```

Para establecer los valores de una configuración, [Generar configuraciones OSGi mediante el SDK de AEM](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/configuring-osgi.html?lang=es#generating-osgi-configurations-using-the-aem-sdk-quickstart) e [implemente la configuración](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/deploy-code.html?lang=es#deployment-process) a su instancia de Cloud Service.

## Vea también {#see-also}

{{see-also}}

<!--

>[!MORELIKETHIS]
>
>* [Reference Themes, Templates, and Form Data models for Adaptive Forms](/help/forms/reference-themes-templates-data-models.md)

-->
