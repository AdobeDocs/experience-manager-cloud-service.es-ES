---
title: Uso de reCAPTCHA con Edge Delivery Services para AEM Forms as a Cloud Service
description: Uso de Google reCAPTCHA en un formulario EDS
feature: Edge Delivery Services
exl-id: ac104e23-f175-435f-8414-19847efa5825
role: Admin, Architect, Developer
source-git-commit: fe45123b3aefddaf02bc8584283941db168ba174
workflow-type: tm+mt
source-wordcount: '841'
ht-degree: 25%

---


# Uso de reCAPTCHA con Edge Delivery Services para AEM Forms as a Cloud Service

<span>La característica **reCAPTCHA** se encuentra en el programa previo al lanzamiento. Para solicitar acceso a la característica **reCAPTCHA** para Edge Delivery Services de AEM Forms, envía un mensaje de correo electrónico desde tu dirección de trabajo a mailto:aem-forms-ea@adobe.com.</span>

reCAPTCHA es una herramienta popular que se utiliza para proteger los sitios web de actividades fraudulentas, correo no deseado y uso indebido. En Edge Delivery Services, el bloque de formularios adaptables ofrece la funcionalidad para añadir reCAPTCHA de Google para distinguir entre humanos y bots. Esta función permite a los usuarios proteger su sitio web del correo no deseado y del uso indebido.
Por ejemplo, considere un formulario de consulta que recopile datos como las fechas de inicio y finalización de viaje, presupuesto de la habitación, coste estimado del viaje e información del viajero. En estos casos, existe el riesgo de que usuarios maliciosos exploten el formulario para enviar correos electrónicos de phishing o inundarlo con contenido irrelevante o dañino mediante bots de spam. La integración de reCAPTCHA ofrece una seguridad añadida al verificar que los envíos proceden de usuarios genuinos, lo que minimiza de forma eficaz las entradas de correo no deseado.

<!-- ![Recaptcha Image](/help/edge/docs/forms/assets/recaptcha-image.png){width="300" align="center"} -->

Los Edge Delivery Services solo admiten el **informe basado en puntuación(v3)-reCAPTCHA** para el bloque de formulario adaptable.

![ReCaptcha V2](/help/forms/assets/recaptcha-v2-invisible.png){width="300" align="center"}


Al final de este artículo, aprenderá lo siguiente:
* [Habilitar Google reCAPTCHA para un solo formulario](#enable-google-recaptchas-for-a-single-form)
* [Habilitar reCAPTCHA para todos los formularios del sitio](#enable-recaptcha-for-all-the-forms)

## Requisitos previos

* Inicie el desarrollo de Edge Delivery Services Forms siguiendo los pasos que se explican en [Crear un formulario con el bloque de Forms adaptable](/help/edge/docs/forms/create-forms.md).
* Registre su dominio con [Google reCAPTCHA y obtenga las credenciales](https://www.google.com/recaptcha/admin/create).

## Habilitar Google reCAPTCHA para un solo formulario {#enable-google-recaptchas-for-a-single-form}

La activación de Google reCAPTCHA para un solo formulario implica la integración del servicio reCAPTCHA de Google en un formulario web específico para evitar el envío automatizado de correo no deseado o abusivo.

Para habilitar Google reCAPTCHA para un solo formulario:
1. [Configure la clave secreta reCAPTCHA en el archivo de configuración del proyecto](#configure-secret-key)
1. [Agregue la clave del sitio reCAPTCHA al formulario](#add-site-key)

Para comenzar a configurar reCaptcha en Edge Delivery Services Forms, consulte la siguiente [hoja de cálculo](/help/edge/docs/forms/assets/recaptcha.xlsx) que incluye la definición del formulario.

### Configure la clave secreta reCAPTCHA en el archivo de configuración del proyecto {#configure-secret-key}

El Secreto del sitio para el dominio registrado con Google AEM reCAPTCHA se agrega al proyecto y al archivo de configuración (`.helix/config`) en la carpeta del proyecto en la carpeta de Microsoft SharePoint o Google Drive. Para añadir el Secreto del sitio al archivo de configuración:

1. AEM Vaya a la carpeta del proyecto de la en Microsoft® SharePoint o Google Drive.
1. AEM Cree el archivo `.helix/config.xlsx` en la carpeta de proyecto de la carpeta de proyectos de la carpeta de Microsoft SharePoint AEM Site o el archivo `.helix/config` en la carpeta de proyecto de la carpeta de la carpeta de proyectos de la unidad de Google.

   >[!NOTE]
   >
   > El [archivo de configuración del proyecto](https://www.aem.live/docs/configuration) es una hoja de cálculo ubicada en `/.helix/config`. Si el archivo no existe, créelo.

1. Abra el archivo `config` y agregue los siguientes pares de clave y valor:

   * **captcha.secret**: valor de clave secreta reCAPTCHA de Google
   * **captcha.type**: reCAPTCHA v2

   >[!NOTE]
   >
   >  * Puede recuperar las claves reCAPTCHA desde el [Admin Console reCAPTCHA de Google](https://www.google.com/recaptcha/admin).
   >  * Debe especificar el valor de **captcha.type** en el archivo `config` como **reCAPTCHA v2**.

   Consulte la captura de pantalla del archivo de configuración de un proyecto a continuación:

   ![Archivo de configuración del proyecto](/help/forms/assets/recaptcha-config-file.png)

1. Guarde el archivo `config`.

1. Obtenga una vista previa y publique el archivo de `config` con [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content).

### Agregue la clave del sitio reCAPTCHA al formulario {#add-site-key}

La clave del sitio de un dominio registrado con Google reCAPTCHA se añade a la hoja de cálculo del formulario que se va a proteger. Para agregar la clave del sitio a un formulario:

1. Vaya a la carpeta del proyecto AEM en Microsoft® SharePoint o Google Drive y abra la hoja de cálculo. También puede crear una nueva hoja de cálculo para un formulario.
1. Inserte una fila en la hoja de cálculo para agregar un nuevo campo como CAPTCHA, incluidos los siguientes detalles:
   * **tipo**: captcha
   * **value**: valor de clave del sitio reCAPTCHA de Google

   Consulte la captura de pantalla siguiente, que muestra la hoja de cálculo con el nuevo tipo de fila como CAPTCHA:

   ![Hoja de cálculo Recaptcha](/help/edge/docs/forms/assets/recaptcha-spreadsheet.png)

   >[!NOTE]
   >
   >  Puede recuperar las claves reCAPTCHA desde el [Admin Console reCAPTCHA de Google](https://www.google.com/recaptcha/admin).

1. Guarde la hoja de cálculo.
1. Utilice [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content) para obtener una vista previa y publicar la hoja.

Después de agregar una nueva fila en la definición del formulario, aparece un distintivo reCAPTCHA en la esquina inferior derecha del formulario. Esto garantiza que el formulario ahora esté protegido frente a actividades fraudulentas, correo no deseado y uso incorrecto.

![recaptcha-form](/help/edge/docs/forms/assets/recaptcha-form.png)

## Habilitar reCAPTCHA para todos los formularios del sitio{#enable-recaptcha-for-all-the-forms}

Para aplicar Google reCAPTCHA a todos los formularios del sitio que utilizan el bloque de Forms adaptable, omita los pasos anteriores e incruste directamente el valor `sitekey` en el archivo `recaptcha.js`. Para incluir el valor de la clave del sitio en el archivo `recaptcha.js`:

1. [Actualice la clave del sitio reCAPTCHA de Google en el archivo recaptcha.js](#1-update-google-recaptcha-site-key-in-recaptchajs-file)
1. [Implemente el archivo y genere el proyecto](#2-deploy-the-file-and-build-the-project)
1. [AEM Vista previa del sitio mediante la barra de tareas de la](#3-preview-the-site-using-the-aem-sidekick)

### Actualizar la clave del sitio reCAPTCHA de Google en el archivo recaptcha.js

1. Abra el repositorio de GitHub correspondiente en el equipo local.
1. Vaya a la carpeta `[../Form Block/integrations]` y abra el archivo `recaptcha.js`.
1. Reemplace `siteKey` por el valor de clave de sitio reCAPTCHA de Google.

   ![Recaptcha se aplica a todos los formularios](/help/forms/assets/recaptcha-apply-to-all-forms.png)

   >[!NOTE]
   >
   >  Puede recuperar las claves reCAPTCHA desde el [Admin Console reCAPTCHA de Google](https://www.google.com/recaptcha/admin).

1. Guarde el archivo `recaptcha.js`.

### Implemente el archivo y genere el proyecto

Implemente el archivo `recaptcha.js` actualizado en su proyecto de GitHub y verifique que la compilación se haya realizado correctamente.

### AEM Vista previa del sitio mediante la barra de tareas de la

Use [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content) para obtener una vista previa y publicar el sitio.

El distintivo reCAPTCHA comienza a aparecer para todos los formularios del sitio.

## Ver también

{{see-more-forms-eds}}

