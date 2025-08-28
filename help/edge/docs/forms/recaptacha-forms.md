---
title: Uso de reCAPTCHA con Edge Delivery Services para AEM Forms as a Cloud Service
description: Uso de Google reCAPTCHA en un formulario para Edge Delivery Services para AEM Forms
feature: Edge Delivery Services
exl-id: ac104e23-f175-435f-8414-19847efa5825
role: Admin, Architect, Developer
source-git-commit: bc422429d4a57bbbf89b7af2283b537a1f516ab5
workflow-type: ht
source-wordcount: '815'
ht-degree: 100%

---


# Uso de reCAPTCHA con Edge Delivery Services para AEM Forms as a Cloud Service

<!--
<span>The **reCAPTCHA** feature is under the pre-release program. To request access to the **reCAPTCHA** feature for Edge Delivery Services for AEM Forms, send an email from your work address to mailto:aem-forms-ea@adobe.com.</span>
-->

reCAPTCHA es una herramienta popular que se utiliza para proteger los sitios web de actividades fraudulentas, correo no deseado y uso indebido. En Edge Delivery Services, el bloque de formularios adaptables ofrece la funcionalidad para añadir reCAPTCHA de Google para distinguir entre humanos y bots. Esta función permite a los usuarios proteger su sitio web del correo no deseado y del uso indebido.
Por ejemplo, considere un formulario de consulta que recopile datos como las fechas de inicio y finalización de viaje, presupuesto de la habitación, coste estimado del viaje e información del viajero. En estos casos, existe el riesgo de que usuarios maliciosos exploten el formulario para enviar correos electrónicos de phishing o inundarlo con contenido irrelevante o dañino mediante bots de spam. La integración de reCAPTCHA ofrece una seguridad añadida al verificar que los envíos proceden de usuarios genuinos, lo que minimiza de forma eficaz las entradas de correo no deseado.

<!-- ![Recaptcha Image](/help/edge/docs/forms/assets/recaptcha-image.png){width="300" align="center"} -->

Edge Delivery Services solo admite **Score based(v3)-reCAPTCHA** para el bloque de formulario adaptable.

![ReCaptcha V2](/help/forms/assets/recaptcha-v2-invisible.png){width="300" align="center"}


Al final de este artículo, aprenderá lo siguiente:
- [Habilitar Google reCAPTCHA para un solo formulario](#enable-google-recaptchas-for-a-single-form)
- [Habilitar reCAPTCHA para todos los formularios del sitio](#enable-recaptcha-for-all-the-forms)

## Requisitos previos

- Inicie el desarrollo de formularios de Edge Delivery Services siguiendo los pasos que se explican en [Creación de un formulario mediante el bloque de formularios adaptables](/help/edge/docs/forms/create-forms.md).
- Registre su dominio con [Google reCAPTCHA y obtenga las credenciales](https://www.google.com/recaptcha/admin/create).

## Habilitar Google reCAPTCHA para un solo formulario {#enable-google-recaptchas-for-a-single-form}

La habilitación de Google reCAPTCHA para un solo formulario implica la integración del servicio reCAPTCHA de Google en un formulario web específico para evitar el envío automatizado de correos no deseados o abusivos.

Para habilitar Google reCAPTCHA para un solo formulario:

1. [Configure la clave secreta reCAPTCHA en el archivo de configuración del proyecto](#configure-secret-key)
1. [Añada la clave del sitio reCAPTCHA al formulario](#add-site-key)

Para comenzar a configurar reCaptcha en los formularios Edge Delivery Services, consulte la siguiente [hoja de cálculo](/help/edge/docs/forms/assets/recaptcha.xlsx) que incluye la definición del formulario.

### Configure la clave secreta reCAPTCHA en el archivo de configuración del proyecto {#configure-secret-key}

El secreto del sitio para el dominio registrado con Google reCAPTCHA se añade al archivo de configuración del proyecto (`.helix/config`) en la carpeta Proyectos AEM alojada en Microsoft SharePoint o Google Drive. Para añadir el secreto del sitio al archivo de configuración:

1. Vaya a la carpeta Proyectos de AEM en Microsoft® SharePoint o Google Drive.
1. Cree el archivo `.helix/config.xlsx` en la carpeta Proyectos AEM alojada en el sitio Microsoft SharePoint o el archivo `.helix/config` en la carpeta Proyectos AEM de Google Drive.

   >[!NOTE]
   >
   > El [archivo de configuración del proyecto](https://www.aem.live/docs/configuration) es una hoja de cálculo ubicada en `/.helix/config`. Si el archivo no existe, créelo. 

1. Abra el archivo `config` y añada los siguientes pares de clave y valor:

   - **captcha.secret**: valor de clave secreta de Google reCAPTCHA
   - **captcha.type**: reCAPTCHA v2

   >[!NOTE]
   >
   >  - Puede recuperar las claves reCAPTCHA desde [Google reCAPTCHA Admin Console](https://www.google.com/recaptcha/admin).
   >  - Debe especificar el valor de **captcha.type** en el archivo `config` como **reCAPTCHA v2**.

   Consulte a continuación la captura de pantalla del archivo de configuración de un proyecto:

   ![Archivo de configuración del proyecto](/help/forms/assets/recaptcha-config-file.png)

1. Guarde el archivo `config`.

1. Previsualice y publique el archivo `config` con [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content).

### Adición de la clave del sitio reCAPTCHA al formulario {#add-site-key}

La clave del sitio para un dominio registrado con Google reCAPTCHA se añade a la hoja de cálculo del formulario que se va a proteger. Para añadir la clave del sitio a un formulario:

1. Vaya a la carpeta del proyecto AEM en Microsoft® SharePoint o Google Drive y abra la hoja de cálculo. También puede crear una nueva hoja de cálculo para un formulario.
1. Inserte una fila en la hoja de cálculo para añadir un nuevo campo como CAPTCHA, que incluya los siguientes detalles:
   - **type**: captcha
   - **value**: valor de clave del sitio de Google reCAPTCHA

   Consulte la captura de pantalla siguiente, donde se muestra la hoja de cálculo con la fila nueva de tipo como CAPTCHA:

   ![Hoja de cálculo de Recaptcha](/help/edge/docs/forms/assets/recaptcha-spreadsheet.png)

   >[!NOTE]
   >
   >  Puede recuperar las claves reCAPTCHA desde [Google reCAPTCHA Admin Console](https://www.google.com/recaptcha/admin).

1. Guarde la hoja de cálculo.
1. Utilice [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content) para obtener una vista previa y publicar la hoja.

Después de añadir la nueva fila en la definición del formulario, aparece un distintivo reCAPTCHA en la esquina inferior derecha del formulario. Esto garantiza que el formulario está ahora protegido frente a actividades fraudulentas, correo no deseado y uso indebido.

![recaptcha-form](/help/edge/docs/forms/assets/recaptcha-form.png)

## Habilitar reCAPTCHA para todos los formularios del sitio{#enable-recaptcha-for-all-the-forms}

Para aplicar Google reCAPTCHA a todos los formularios del sitio que utilizan el bloque de formularios adaptables, omita los pasos anteriores e incruste directamente el valor `sitekey` en el archivo `recaptcha.js`. Para incluir el valor de la clave del sitio en el archivo `recaptcha.js`:

1. [Actualice la clave del sitio de Google reCAPTCHA en el archivo recaptcha.js](#1-update-google-recaptcha-site-key-in-recaptchajs-file)
1. [Implemente el archivo y genere el proyecto](#2-deploy-the-file-and-build-the-project)
1. [Vista previa del sitio con AEM Sidekick](#3-preview-the-site-using-the-aem-sidekick)

### Actualización de la clave del sitio de Google reCAPTCHA en el archivo recaptcha.js

1. Abra el repositorio de GitHub correspondiente en su equipo local.
1. Navegue hasta la carpeta `[../Form Block/integrations]` y abra el archivo `recaptcha.js`.
1. Reemplace `siteKey` por el valor de clave del sitio de Google reCAPTCHA.

   ![Recaptcha se aplica a todos los formularios](/help/forms/assets/recaptcha-apply-to-all-forms.png)

   >[!NOTE]
   >
   >  Puede recuperar las claves reCAPTCHA desde [Google reCAPTCHA Admin Console](https://www.google.com/recaptcha/admin).

1. Guarde el archivo `recaptcha.js`.

### Implemente el archivo y genere el proyecto

Implemente el archivo `recaptcha.js` actualizado en el proyecto de GitHub y compruebe que la compilación se ha realizado correctamente.

### Vista previa del sitio con AEM Sidekick

Utilice [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content) para obtener una vista previa y publicar el sitio.

El distintivo reCAPTCHA comienza a aparecer en todos los formularios del sitio.

