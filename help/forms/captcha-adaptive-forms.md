---
title: Cómo usar CAPTCHA en Forms adaptable
description: Aprenda a configurar el servicio reCAPTCHA de Google para un formulario adaptable.
uuid: 0e11e98a-12ac-484c-b77f-88ebdf0f40e5
contentOwner: vishgupt
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: adaptive_forms, author
exl-id: 3fdbe5a3-5c3c-474d-b701-e0182da4191a
source-git-commit: 57e421a865b664c0adb7af93b33bd4b6b32049ab
workflow-type: tm+mt
source-wordcount: '1945'
ht-degree: 64%

---


# Uso de reCAPTCHA en Forms adaptable {#using-reCAPTCHA-in-adaptive-forms}

<span class="preview"> Adobe recomienda utilizar la captura de datos moderna y ampliable [Componentes principales](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=es) para [crear un nuevo Forms adaptable](/help/forms/creating-adaptive-form-core-components.md) o [adición de Forms adaptable a páginas de AEM Sites](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md). Estos componentes representan un avance significativo en la creación de Forms adaptable, lo que garantiza experiencias de usuario impresionantes. Este artículo describe un enfoque más antiguo para crear Forms adaptable mediante componentes de base. </span>


| Versión | Vínculo del artículo |
| -------- | ---------------------------- |
| AEM 6.5 | [Haga clic aquí](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-basic-authoring/captcha-adaptive-forms.html) |
| AEM as a Cloud Service | Este artículo |
| Se aplica a | Formulario adaptable basado en componentes de base. <br> Para formularios adaptables basados en componentes principales, [Haga clic aquí](/help/forms/captcha-adaptive-forms-core-components.md). |


CAPTCHA (prueba de Turing completamente automática y pública para diferenciar ordenadores de humanos) es un programa que se utiliza comúnmente en transacciones en línea para distinguir entre humanos y programas o bots automatizados. Plantea un desafío y evalúa la respuesta del usuario para determinar si es un humano o un bot que interactúa con el sitio. Evita que el usuario continúe si la prueba falla y ayuda a que las transacciones en línea sean seguras al impedir que los bots publiquen contenido no deseado o con fines malintencionados.

[!DNL AEM Forms] admite reCAPTCHA en Forms adaptable. Puede utilizar el servicio reCAPTCHA de Google para implementar CAPTCHA.

>[!NOTE]
>
>* [!DNL AEM Forms] es compatible con reCaptcha v2 y reCaptcha Enterprise. No existe compatibilidad con ninguna otra versión.
>* reCAPTCHA en Forms adaptable no es compatible con el modo sin conexión en [!DNL AEM Forms] aplicación.
>

## Configuración del servicio ReCAPTCHA de Google {#google-reCAPTCHA}

Los autores de formularios pueden utilizar el servicio reCAPTCHA de Google para implementar reCAPTCHA en Forms adaptable. Ofrece funcionalidades de CAPTCHA avanzadas para proteger su sitio. Para obtener más información sobre cómo funciona reCAPTCHA, consulte [Google reCAPTCHA](https://developers.google.com/recaptcha/). El servicio reCAPTCHA incluye [!DNL reCAPTCHA v2] y [!DNL reCAPTCHA Enterprise] en la que se puede integrar [!DNL AEM Forms]. Según sus necesidades, puede configurar el servicio reCAPTCHA para habilitar lo siguiente:

![reCAPTCHA](/help/forms/assets/recaptcha_new.png)

* [reCAPTCHA Enterprise en AEM Forms](#steps-to-implement-reCAPTCHA-enterprise-in-forms)
* [reCAPTCHA v2 en AEM Forms](#steps-to-implement-reCAPTCHA-v2-in-forms)


### Configuración de reCAPTCHA Enterprise  {#steps-to-implement-reCAPTCHA-enterprise-in-forms}

1. Cree o seleccione un [Proyecto de Google Cloud](https://cloud.google.com/recaptcha-enterprise/docs/set-up-non-google-cloud-environments-api-keys#before-you-begin) y habilitar [API de reCAPTCHA Enterprise](https://cloud.google.com/recaptcha-enterprise/docs/set-up-non-google-cloud-environments-api-keys#enable-the-recaptcha-enterprise-api).
1. Obtenga la [Identificador de proyecto](https://support.google.com/googleapi/answer/7014113?hl=en#:~:text=To%20locate%20your%20project%20ID,a%20member%20of%20are%20displayed) y cree un [Clave de API](https://cloud.google.com/recaptcha-enterprise/docs/set-up-non-google-cloud-environments-api-keys#create_an_api_key) y una [clave del sitio para sitios web](https://cloud.google.com/recaptcha-enterprise/docs/create-key#create-key).
1. Crear un contenedor de configuración para los servicios en la nube.

   1. Vaya a **[!UICONTROL Herramientas > General > Explorador de configuración]**.
   1. Seleccione una carpeta o cree una carpeta y habilite la carpeta para las configuraciones de nube mediante los siguientes pasos:
      1. En el Explorador de configuración, seleccione la carpeta  y pulse **[!UICONTROL Propiedades]**.
      1. En el cuadro de diálogo Propiedades de configuración, habilite **[!UICONTROL Configuraciones de nube]**.
      1. Pulse **[!UICONTROL Guardar y cerrar]** para guardar la configuración y salir del cuadro de diálogo.

1. Configure el servicio en la nube para [!DNL reCAPTCHA Enterprise].

   1. En la instancia de autor Experience Manager, vaya a ![herramientas-1](assets/tools-1.png) > **[!UICONTROL Cloud Services]**.
   1. Pulse **[!UICONTROL reCAPTCHA]**. Se abre la página de configuración. Seleccione el contenedor de configuración que ha creado y pulse **[!UICONTROL Crear]**.
   1. Seleccionar versión como [!DNL reCAPTCHA Enterprise] y especifique el nombre, el ID del proyecto, la clave del sitio y la clave de la API (obtenida en el paso 2) para el servicio reCAPTCHA Enterprise.
   1. Seleccione el tipo de clave, el tipo de clave debe ser el mismo que la clave de sitio configurada en la [Proyecto de Google Cloud](https://cloud.google.com/recaptcha-enterprise/docs/set-up-non-google-cloud-environments-api-keys#before-you-begin), por ejemplo, **Clave de sitio de casilla** o **Clave de sitio basada en puntuación**.
   1. Especifique un [puntuación de umbral en el rango de 0 a 1](https://cloud.google.com/recaptcha-enterprise/docs/interpret-assessment#interpret_scores). Las puntuaciones superiores o iguales a las puntuaciones de umbral identifican la interacción humana; de lo contrario, se considera interacción de bots.
   1. Tocar **[!UICONTROL Crear]** para crear la configuración del servicio en la nube.

<!--
    1. In the Edit Component dialog, specify the name, project ID, site key, API key (obtained in steps 2 and 3), select the key type, and enter the threshold score. Tap **[!UICONTROL Save Settings]** and then tap **[!UICONTROL OK]** to complete the configuration.
-->

Una vez habilitado el servicio reCAPTCHA Enterprise, estará disponible para su uso en formularios adaptables. Consulte [usar CAPTCHA en formularios adaptables](#using-reCAPTCHA).

<!--
![reCAPTCHA Enterprise](/help/forms/assets/recaptcha1-enterprise.png)
-->

### Configuración de Google reCAPTCHA v2 {#steps-to-implement-reCAPTCHA-v2-in-forms}

1. Obtener el [par de claves de la API reCAPTCHA](https://www.google.com/recaptcha/admin) de Google. Incluye un **clave del sitio** y una **clave secreta**.
1. Crear un contenedor de configuración para los servicios en la nube.
   1. Vaya a **[!UICONTROL Herramientas > General > Explorador de configuración]**.
   1. Seleccione una carpeta o cree una carpeta y habilite la carpeta para las configuraciones de nube mediante los siguientes pasos:
      1. En el Explorador de configuración, seleccione la carpeta  y pulse **[!UICONTROL Propiedades]**.
      1. En el cuadro de diálogo Propiedades de configuración, habilite **[!UICONTROL Configuraciones de nube]**.
      1. Pulse **[!UICONTROL Guardar y cerrar]** para guardar la configuración y salir del cuadro de diálogo.

1. Configure el servicio en la nube para reCAPTCHA v2.

   1. En la instancia de autor de AEM, vaya a ![tools-1](assets/tools-1.png) > **Cloud Services**.
   1. Pulse **[!UICONTROL reCAPTCHA]**. Se abre la página de configuración. Seleccione el contenedor de configuración que ha creado y pulse **[!UICONTROL Crear]**.
   1. Seleccionar versión como [!DNL reCAPTCHA v2] , especifique el nombre, la clave del sitio y la clave secreta para el servicio reCAPTCHA (obtenido en el paso 1) y pulse **[!UICONTROL Crear]** para crear la configuración del servicio en la nube.
   1. En el cuadro de diálogo Editar componente, especifique el sitio y las claves secretas obtenidas en el paso 1. Pulse **[!UICONTROL Guardar configuración]** y, a continuación, **Aceptar** para completar la configuración.

   Una vez configurado el servicio reCAPTCHA, estará disponible para su uso en formularios adaptables. Para obtener más información, consulte [usar CAPTCHA en formularios adaptables](#using-reCAPTCHA).

<!--![reCAPTCHA v2](/help/forms/assets/recaptcha-v2.png)-->


## Usar reCAPTCHA en formularios adaptables {#using-reCAPTCHA}

Para usar reCAPTCHA en formularios adaptables haga lo siguiente:

1. Abra un formulario adaptable en modo Edición.

   >[!NOTE]
   >
   >Asegúrese de que el contenedor de configuración seleccionado al crear el formulario adaptable contenga el servicio en la nube reCAPTCHA. También puede editar las propiedades del formulario adaptable para cambiar el contenedor de configuración asociado al formulario.

1. Desde el explorador de componentes, arrastre y suelte el componente **Captcha** en el formulario adaptable.

   >[!NOTE]
   >
   >* No se puede usar más de un componente Captcha en un formulario adaptable. Además, no se recomienda utilizar CAPTCHA en un panel marcado para la carga lenta o en un fragmento.
   >* reCaptcha tiene un plazo y caduca en unos minutos. Por lo tanto, se recomienda colocar el componente Captcha justo antes del botón Enviar en el formulario adaptable.

1. Seleccione el componente Captcha que ha añadido y pulse ![cmppr](assets/cmppr.png) para editar sus propiedades.
1. Especifique un título para el widget CAPTCHA. El valor predeterminado es **Captcha**. Seleccione **Ocultar título** si no desea que aparezca el título.
1. En el menú desplegable **servicio Captcha**, seleccione **reCAPTCHA** para habilitarlo si lo configuró como se describe en el [Servicio reCAPTCHA de Google](#google-reCAPTCHA).
1. Seleccione una configuración en la lista desplegable Configuración para **reCAPTCHA Enterprise** o **reCAPTCHA v2**
   1. Si selecciona **reCAPTCHA Enterprise** versión, el tipo de clave puede ser **casilla de verificación** o **basado en puntuación**, se basa en la selección realizada al configurar [clave del sitio para sitios web](https://cloud.google.com/recaptcha-enterprise/docs/create-key#create-key):

   >[!NOTE]
   >
   >* En la configuración de nube con **tipo de clave** as **casilla de verificación**, el mensaje de error personalizado aparece como un mensaje en línea si falla la validación captcha.
   >* En la configuración de nube con **tipo de clave** as **basado en puntuación**, el mensaje de error personalizado se muestra como un mensaje emergente si falla la validación captcha.

   1. Puede seleccionar el tamaño como **[!UICONTROL Normal]** y **[!UICONTROL Compacto]**.
   1. Puede seleccionar una **[!UICONTROL Referencia de enlace]**, en **[!UICONTROL Referencia de enlace]** los datos enviados son datos enlazados; de lo contrario, son datos no enlazados. A continuación se muestran ejemplos XML de datos independientes y datos enlazados (con referencia de enlace como SSN) respectivamente, cuando se envía un formulario.

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

   Si selecciona **reCAPTCHA v2** versión:
   1. Puede seleccionar el tamaño como **[!UICONTROL Normal]** o **[!UICONTROL Compacto]** para el widget reCAPTCHA.
   1. Puede seleccionar el **[!UICONTROL Invisible]** opción para mostrar el desafío CAPTCHA solo en el caso de una actividad sospechosa.

   El servicio reCAPTCHA está habilitado en el formulario adaptable. Puede obtener una vista previa del formulario y ver cómo funciona CAPTCHA. El **protegido por reCAPTCHA** el distintivo, que se muestra a continuación, aparece en los formularios protegidos.
   ![Distintivo protegido por reCAPTCHA de Google](/help/forms/assets/google-recaptcha-v2.png)

1. Guarde las propiedades.

>[!NOTE]
> 
> No seleccione **[!UICONTROL Predeterminado]** en el menú desplegable del servicio Captcha, ya que el servicio CAPTCHA AEM predeterminado está obsoleto.

>[!VIDEO](https://video.tv.adobe.com/v/3422641/recaptcha-google-adaptive-forms/?quality=12&learn=on)

### Mostrar u ocultar el componente CAPTCHA en base a reglas {#show-hide-captcha}

Puede seleccionar mostrar u ocultar el componente CAPTCHA en función de las reglas que aplique en un componente de un formulario adaptable. Pulse el componente, seleccione ![editar reglas](assets/edit-rules-icon.svg) y pulse **[!UICONTROL Crear]** para crear una regla. Para obtener más información sobre la creación de reglas, consulte [Editor de reglas](rule-editor.md).

Por ejemplo, el componente CAPTCHA debe mostrarse en un formulario adaptable solo si el campo Valor de moneda del formulario tiene un valor superior a 25 000.

Pulse **[!UICONTROL Valor de moneda]** en el formulario y cree las siguientes reglas:

![Mostrar u ocultar reglas](assets/rules-show-hide-captcha.png)

>[!NOTE]
>
> Cuando selecciona una configuración de reCAPTCHA versión 2 y el tamaño se establece en [!UICONTROL Invisible], la opción mostrar/ocultar permanece deshabilitada.

### Validar CAPTCHA {#validate-captcha}

Puede validar el CAPTCHA en un formulario adaptable al enviar el formulario o basar la validación CAPTCHA en las acciones y condiciones del usuario.

#### Validar el CAPTCHA al enviar el formulario {#validation-form-submission}

Para validar un CAPTCHA automáticamente al enviar un formulario adaptable:

1. Pulse el componente CAPTCHA y seleccione ![cmppr](assets/configure-icon.svg) para ver las propiedades del componente.
1. En la sección **[!UICONTROL Validar CAPTCHA]**, seleccione **[!UICONTROL Validar el CAPTCHA al enviar el formulario]**.
1. Pulse ![Listo](assets/save_icon.svg) para guardar las propiedades del componente.

#### Validar el CAPTCHA en base a las acciones y condiciones del usuario {#validate-captcha-user-action}

Para validar un CAPTCHA basado en condiciones y acciones del usuario:

1. Pulse el componente CAPTCHA y seleccione ![cmppr](assets/configure-icon.svg) para ver las propiedades del componente.
1. En la sección **[!UICONTROL Validar CAPTCHA]**, seleccione **[!UICONTROL Validar el CAPTCHA en base a una acción del usuario]**.
1. Pulse ![Listo](assets/save_icon.svg) para guardar las propiedades del componente.

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
1. Pulse **[!UICONTROL Enviar]**. El CAPTCHA se valida según las condiciones definidas en la API `ValidateCAPTCHA` de la acción de envío personalizada.

**Opción 2: Usar la API [!DNL Experience Manager Forms] ValidateCAPTCHA para validar el CAPTCHA en una acción del usuario antes de enviar el formulario**

También puede invocar la API `ValidateCAPTCHA` al aplicar reglas en un componente de un formulario adaptable.

Por ejemplo, añade un botón **[!UICONTROL Validar CAPTCHA]** en un formulario adaptable y crea una regla para invocar un servicio haciendo clic en un botón.

La siguiente imagen ilustra cómo puede invocar un servicio al hacer clic en un botón **[!UICONTROL Validar CAPTCHA]**:

![Validar CAPTCHA](assets/captcha-validation1.gif)

Puede invocar el servlet personalizado que incluye la API `ValidateCAPTCHA` mediante el editor de reglas y habilitar o deshabilitar el botón de envío del formulario adaptable en base al resultado de validación.

Del mismo modo, puede utilizar el editor de reglas para incluir un método personalizado para validar el CAPTCHA en un formulario adaptable.

### Añadir servicios CAPTCHA personalizados {#add-custom-captcha-service}

[!DNL Experience Manager Forms] Ofrece reCAPTCHA como servicio CAPTCHA. Con todo, puede agregar un servicio personalizado para que se muestre en la lista desplegable **[!UICONTROL Servicio CAPTCHA]**.

A continuación se muestra un ejemplo de implementación de la interfaz para agregar un servicio CAPTCHA adicional al formulario adaptable:

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

`captchaPropertyNodePath` hace referencia a la ruta de recurso del componente CAPTCHA en el repositorio de Sling. Utilice esta propiedad para incluir detalles específicos del componente CAPTCHA. Por ejemplo, `captchaPropertyNodePath` incluye información para la configuración de nube reCAPTCHA configurada en el componente CAPTCHA. La información de configuración de nube ofrece la configuración **[!UICONTROL Clave del sitio]** y **[!UICONTROL Clave secreta]** para implementar el servicio reCAPTCHA.

`userResponseToken` hace referencia a la `g_recaptcha_response` que se genera después de resolver un CAPTCHA en un formulario.

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


>[!MORELIKETHIS]
>
>* [Temas de referencia, plantillas y modelos de datos de formulario para Forms adaptable](/help/forms/reference-themes-templates-data-models.md)
