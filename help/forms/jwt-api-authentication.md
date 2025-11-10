---
title: Cómo configurar la autenticación JWT (token web JSON)
description: Obtenga información sobre cómo configurar la autenticación JWT (token web JSON) para Adobe Experience Manager Forms as a Cloud Service
role: Admin, Developer, User
feature: Adaptive Forms, APIs & Integrations
hide: true
hidefromToC: true
index: false
source-git-commit: 69704ca8de41c655b59ce6652a4a43b788ba75ec
workflow-type: tm+mt
source-wordcount: '431'
ht-degree: 3%

---


# Autenticación JWT (token web JSON): obsoleta

La autenticación JWT en AEM Forms, especialmente para integraciones del lado del servidor con AEM as a Cloud Service, implica un proceso específico para interactuar de forma segura con los servicios de AEM.

## Consideración

El token de acceso generado por JWT no funcionará después de que los certificados actuales caduquen o el 1 de marzo de 2026, lo que ocurra antes. Por lo tanto, debe migrar su integración para utilizar la nueva [credencial de servidor a servidor OAuth](/help/forms/oauth-api-authetication.md).

La migración de sus proyectos a las credenciales de servidor a servidor de OAuth es un proceso sencillo de dos pasos que permite una migración sin tiempo de inactividad para sus aplicaciones e integraciones. Lea la [guía de migración](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/migration) para migrar a la credencial de servidor a servidor de OAuth.


## Requisitos previos

Antes de empezar, asegúrese de que se cumplen los siguientes requisitos previos:

* Asegúrese de que tiene acceso a [Adobe Cloud Manager](https://experience.adobe.com/#/@formsinternal01/cloud-manager/landing.html) específico del entorno que utiliza.
* Asigne la función Administrador del sistema o Desarrollador para acceder a Adobe Cloud Manager.

## Cómo generar un token de acceso usando credenciales de JWT

Siga los pasos a continuación, que muestran cómo generar un token de acceso a partir de las credenciales de JWT.

1. **Adobe Cloud Manager**

   1. Inicie sesión en su [cuenta de Cloud Manager](https://experience.adobe.com/#/@formsinternal01/cloud-manager/landing.html).
   2. En el programa seleccionado, haga clic en **[!UICONTROL Descripción general del programa]**.

      ![Cuenta de Cloud Manager](/help/forms/assets/jwt-cloud-manager-landing.png)

   3. En el programa, haz clic en el menú de tres puntos y selecciona **[!UICONTROL Developer Console]**.

      ![Developer Console](/help/forms/assets/jwt-developer-console.png)

2. **AEM Developer Console**
   1. Iniciar sesión en AEM Developer Console
   2. Haga clic en **[!UICONTROL Integraciones]** ubicadas en la barra de menús superior.

      ![Integraciones](/help/forms/assets/jwt-integrations.png)

   3. Haga clic en la opción para **[!UICONTROL crear una nueva cuenta técnica]**.

      ![Crear nueva cuenta técnica](/help/forms/assets/jwt-creae-new-tech-account.png)

   Una vez que haga clic en Crear una nueva cuenta técnica, se genera la información necesaria para generar el token de acceso, como el ID de cliente y el secreto de cliente, junto con otra información de cuenta técnica, incluida la clave privada, la clave pública y la fecha de caducidad.

   ![Credenciales JWT](/help/forms/assets/jwt-credentials.png)


3. Generar y guardar credenciales

   1. Registrar credenciales de API

      ```text
      API Credentials:
      ================
      Client ID: <your_client_id>
      Client Secret: <your_client_secret>
      Technical Account ID: <tech_account_id>
      Organization ID: <org_id>
      Scopes: AdobeID,openid,read_organizations
      ```

4. Generación de token de acceso

   Genere tokens mediante programación utilizando la API de Adobe IMS:

   **Credenciales requeridas:**

   * ID del cliente
   * Secreto de cliente
   * Ámbitos (normalmente: `openid, AdobeID, read_organizations, additional_info.projectedProductContext, read_pc.dma_aem_cloud, aem.document`)

   **Extremo de token:**

   ```
   https://ims-na1.adobelogin.com/ims/token/v3
   ```

   **Solicitud de ejemplo (curl):**

   ```bash
   curl -X POST 'https://ims-na1.adobelogin.com/ims/token/v3' \
   -H 'Content-Type: application/x-www-form-urlencoded' \
   -d 'grant_type=client_credentials' \
   -d 'client_id=<YOUR_CLIENT_ID>' \
   -d 'client_secret=<YOUR_CLIENT_SECRET>' \
   -d 'scope=AdobeID,openid,read_organizations'
   ```

   **Respuesta:**

   ```json
   {
   "access_token": "eyJhbGciOiJSUz...",
   "token_type": "bearer",
   "expires_in": 86399
   }
   ```

Ahora puede utilizar el token de acceso generado para hacer una llamada de API a entornos de desarrollo, fase o producción.

## Próximos pasos

Obtenga información sobre cómo establecer el entorno para las API de comunicaciones de Forms sincrónicas (bajo demanda) y asincrónicas (por lotes):

<!-- START CARDS HTML - DO NOT MODIFY BY HAND -->
<div class="columns">
    <!-- Synchronous APIs Card -->
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="AEM Forms Communications APIs - Synchronous">
        <div class="card" style="height: 100%; display: flex; flex-direction: column;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="/help/forms/aem-forms-cloud-service-communications-on-demand-processing.md" title="API sincrónicas" target="_self" rel="referrer">
                        <img class="is-bordered-r-small" src="/help/forms/assets/sync-api.png" alt="API sincrónicas"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="/help/forms/aem-forms-cloud-service-communications-on-demand-processing.md" target="_self" rel="referrer" title="API de comunicaciones de AEM Forms: sincrónicas">API de comunicaciones de AEM Forms: sincrónicas</a>
                    </p>
                    <p class="is-size-6">Aprenda a configurar un entorno para las API de comunicaciones de Forms sincrónicas (bajo demanda) que generan o procesan documentos al instante. </p>
                </div>
                <a href="/help/forms/aem-forms-cloud-service-communications-on-demand-processing.md" target="_self" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">Más información</span>
                </a>
            </div>
        </div>
    </div>
    <!-- Asynchronous APIs Card -->
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="AEM Forms Communications APIs - Asynchronous">
        <div class="card" style="height: 100%; display: flex; flex-direction: column;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="/help/forms/aem-forms-cloud-service-communications-batch-processing.md" title="API de comunicaciones de AEM Forms: asincrónicas" target="_self" rel="referrer">
                        <img class="is-bordered-r-small" src="/help/forms/assets/async-api.png" alt="API asíncronas"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="/help/forms/aem-forms-cloud-service-communications-batch-processing.md" target="_self" rel="referrer" title="API asíncronas">API de comunicaciones de AEM Forms: asincrónicas (por lotes)</a>
                    </p>
                    <p class="is-size-6">Aprenda a configurar el entorno para las API de comunicaciones de Forms asincrónicas (por lotes) que generan o procesan varios documentos de forma programada.</p>
                </div>
                <a href="/help/forms/aem-forms-cloud-service-communications-batch-processing.md" target="_self" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">Más información</span>
                </a>
            </div>
        </div>
    </div>
</div>
<!-- END CARDS HTML - DO NOT MODIFY BY HAND -->


