---
title: Cómo configurar la autenticación de servidor a servidor OAuth
description: Obtenga información sobre cómo configurar la autenticación de servidor a servidor OAuth para Adobe Experience Manager Forms as a Cloud Service
role: Admin, Developer, User
feature: Adaptive Forms, APIs & Integrations
hide: true
hidefromtoc: true
index: false
source-git-commit: fcc25eb44b485db69ec1c267f4cf8774c4279b24
workflow-type: tm+mt
source-wordcount: '672'
ht-degree: 3%

---


# Autenticación de servidor a servidor OAuth (recomendada)

La autenticación de servidor a servidor OAuth permite un acceso seguro y basado en tokens a las API de comunicaciones de AEM Forms sin que sea necesaria la interacción del usuario. Este método es ideal para sistemas automatizados, servicios back-end e integraciones que necesitan autenticarse mediante programación.

## Requisitos previos

Antes de empezar, asegúrese de que se cumplen los siguientes requisitos previos:

* Asegúrese de tener acceso a [Adobe Developer Console](https://developer.adobe.com/console) específico del entorno que utiliza.
* Asigne la función Administrador del sistema o Desarrollador en Adobe Admin Console para habilitar el acceso a Adobe Developer Console.

## Cómo generar un token de acceso mediante la autenticación de servidor a servidor OAuth

Siga los pasos a continuación, que muestran cómo generar un token de acceso desde la consola de Adobe Developer y realizar la primera llamada de API mediante la autenticación de servidor a servidor OAuth.


1. Vaya a [Adobe Developer Console](https://developer.adobe.com/console)
2. Inicie sesión con su Adobe ID

3. Cree un nuevo proyecto o vaya al proyecto existente

   **Para crear un nuevo proyecto:**

   1. En la sección **Inicio rápido**, haga clic en **Crear nuevo proyecto**
   2. Se crea un nuevo proyecto con un nombre predeterminado

      ![Crear proyecto ADC](/help/forms/assets/adc-home.png)

   3. Haga clic en **Editar proyecto** en la esquina superior derecha

      ![Editar proyecto](/help/forms/assets/adc-edit-project.png)

   4. Proporcione un nombre significativo (por ejemplo, &quot;formsproject&quot;)
   5. Haga clic en **Guardar**.

      ![Editar nombre de proyecto](/help/forms/assets/adc-edit-projectname.png)


   **Para navegar a su proyecto existente:**

   1. Haga clic en **Todos los proyectos** desde Adobe Developer Console

      ![Buscar proyectos](/help/forms/assets/search-adc-project.png)

   2. Busque el proyecto y haga clic en para abrirlo.

      ![Localizar proyectos](/help/forms/assets/locate-adc-project.png)


      >[!NOTE]
      >
      > Puede agregar la API y el método de autenticación a su proyecto existente haciendo clic en **Agregar al proyecto** > **API**\
      > ![Agregar API al proyecto existente](/help/forms/assets/add-api-existing-project.png)
      > Para añadir la API y el método de autenticación, realice los mismos pasos que se explican a continuación para su proyecto existente.

4. Agregue diferentes API de comunicaciones de AEM Forms según sus necesidades.

   **A. Para las API de servicios de documentos**

   1. Haga clic en **Agregar API**

      ![Agregar API](/help/forms/assets/adc-add-api.png)

   2. Seleccionar **API de comunicación de Forms**
      1. En el cuadro de diálogo _Agregar API_, filtrar por **Experience Cloud**
      2. Seleccione **&quot;API de comunicación de Forms&quot;**

         ![Agregar API de comunicación de Forms](/help/forms/assets/adc-add-forms-api.png)


   3. Seleccione el método de autenticación **OAuth Server-to-Server**

      ![Seleccionar método de autenticación](/help/forms/assets/adc-add-authentication-method.png)


   **B. Para las API de tiempo de ejecución de Forms adaptables**

   1. **Haga clic en Agregar API**
En el proyecto, haga clic en el botón **Agregar API**

      ![Agregar API](/help/forms/assets/adc-add-api.png)

   2. **Seleccionar API de tiempo de ejecución y entrega de AEM Forms**
      1. En el cuadro de diálogo _Agregar API_, filtrar por **Experience Cloud**
      2. Seleccione **&quot;API de tiempo de ejecución y entrega de AEM Forms&quot;**
      3. Haga clic en **Siguiente**

   3. **Método de autenticación**
Seleccione el método de autenticación **servidor a servidor OAuth**.


      ![Seleccionar método de autenticación](/help/forms/assets/adc-add-authentication-method.png)

5. **Agregar perfil de producto**:

   1. Seleccione el **perfil de producto** apropiado según el nivel de acceso requerido:

      | Tipo de acceso | Perfil del producto |
      |------------------|----------------------|
      | Acceso de solo lectura | `AEM Users - author - Program XXX - Environment XXX` |
      | Acceso de lectura y escritura | `AEM Assets Collaborator Users - author - Program XXX - Environment XXX` |
      | Acceso administrativo completo | `AEM Administrators - author - Program XXX - Environment XXX` |

   2. Seleccione el **perfil de producto** que coincida con la dirección URL del servicio de creación (`https://author-pXXXXX-eYYYYY.adobeaemcloud.com`). Por ejemplo: seleccione `https://author-pXXXXX-eYYYYY.adobeaemcloud.com`.

   3. Haga clic en **Guardar API configurada**. La API y el perfil de producto se añaden al proyecto

      ![Seleccionar configuración del proyecto](/help/forms/assets/adc-add-product-profile.png)

6. Generar y guardar credenciales

   1. Vaya al proyecto en Adobe Developer Console
   2. Haga clic en la credencial **OAuth de servidor a servidor**
   3. Ver la sección **Detalles de credenciales**

      ![Ver credenciales](/help/forms/assets/adc-view-credential.png)

   4. Registrar credenciales de API

      ```text
      API Credentials:
      ================
      Client ID: <your_client_id>
      Client Secret: <your_client_secret>
      Technical Account ID: <tech_account_id>
      Organization ID: <org_id>
      Scopes: AdobeID,openid,read_organizations
      ```

7. Generación de token de acceso

   **A. Para pruebas**

   Genere los tokens de acceso manualmente en Adobe Developer Console:

   1. **Vaya a su proyecto**
      1. En Adobe Developer Console, abra el proyecto
      2. Haga clic en **Servidor a servidor de OAuth**

   2. **Generar token de acceso**
      1. Haga clic en el botón **&quot;Generar token de acceso&quot;** en la sección de API del proyecto
      2. Copiar el token de acceso generado

      ![Generar token de acceso](/help/forms/assets/adc-access-token.png)

      >[!NOTE]
      >
      > El token de acceso es válido solamente por **24 horas**

   **B. Para producción**

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

>[!NOTE]
>
> Para obtener más información sobre la implementación de servidor a servidor de OAuth para generar un token de acceso y realizar llamadas a la API, [haga clic aquí](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/implementation).

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


