---
title: Cómo configurar la autenticación de servidor a servidor OAuth
description: Obtenga información sobre cómo configurar la autenticación de servidor a servidor OAuth para Adobe Experience Manager Forms as a Cloud Service
role: Admin, Developer, User
feature: Adaptive Forms, APIs & Integrations
hide: true
hidefromtoc: true
index: false
source-git-commit: e2f57a32fcc098a2331ad74540a3d48832c2b3c3
workflow-type: tm+mt
source-wordcount: '811'
ht-degree: 3%

---


# Autenticación de servidor a servidor OAuth

La autenticación de servidor a servidor OAuth permite un acceso seguro y basado en tokens a las API de comunicaciones de AEM Forms sin que sea necesaria la interacción del usuario. Adobe Developer Console admite la autenticación de servidor a servidor OAuth.

## Requisitos previos

Antes de empezar, asegúrese de que se cumplen los siguientes requisitos previos:

* Asegúrese de que tiene [acceso a Adobe Developer Console](https://experienceleague.adobe.com/es/docs/experience-manager-cloud-manager/content/requirements/access-rights) específico para el entorno que utiliza.
* [Asigne el rol de Administrador del sistema o Desarrollador en Adobe Admin Console](https://experienceleague.adobe.com/es/docs/experience-manager-cloud-manager/content/requirements/role-based-permissions) para habilitar el acceso a Adobe Developer Console.

## Cómo generar un token de acceso mediante la autenticación de servidor a servidor OAuth

Siga los pasos a continuación para generar un token de acceso desde la consola de Adobe Developer y realizar la primera llamada de API mediante la autenticación de servidor a servidor OAuth.

### Configuración del proyecto de Adobe Developer Console

1. Vaya a [Adobe Developer Console](https://developer.adobe.com/console)
2. Inicie sesión con su Adobe ID

3. Cree un nuevo proyecto o vaya al proyecto existente

>[!BEGINTABS]

>[!TAB Para crear un nuevo proyecto]

1. En la sección **Inicio rápido**, haga clic en **Crear nuevo proyecto**
2. Se crea un nuevo proyecto con un nombre predeterminado

   ![Crear proyecto ADC](/help/forms/assets/adc-home.png)

3. Haga clic en **Editar proyecto** en la esquina superior derecha

   ![Editar proyecto](/help/forms/assets/adc-edit-project.png)

4. Proporcione un nombre significativo (por ejemplo, &quot;formsproject&quot;)
5. Haga clic en **Guardar**.

   ![Editar nombre de proyecto](/help/forms/assets/adc-edit-projectname.png)

>[!TAB Para navegar a su proyecto existente]

1. Haga clic en **Todos los proyectos** desde Adobe Developer Console

   ![Buscar proyectos](/help/forms/assets/search-adc-project.png)

2. Busque el proyecto y haga clic en para abrirlo.

   ![Localizar proyectos](/help/forms/assets/locate-adc-project.png)

>[!ENDTABS]

### Añadir API de Forms

Agregue las API de Forms en función de lo que desee hacer:

* **API de comunicaciones de AEM Forms**: utilícelas cuando necesite generar, convertir, ensamblar o proteger documentos (PDF y formatos relacionados).
* **API de tiempo de ejecución de Forms adaptable**: utilícelas cuando necesite procesar, enviar o procesar Forms adaptable durante la ejecución.

>[!BEGINTABS]

>[!TAB Para las API de comunicaciones de AEM Forms]

1. Haga clic en **Agregar API**

   ![Agregar API](/help/forms/assets/adc-add-api.png)

2. Seleccionar **API de comunicación de Forms**
   1. En el cuadro de diálogo _Agregar API_, filtrar por **Experience Cloud**
   2. Seleccione **&quot;API de comunicación de Forms&quot;**

      ![Agregar API de comunicación de Forms](/help/forms/assets/adc-add-forms-api.png)

   3. Haga clic en **Siguiente**
   4. Seleccione el método de autenticación **OAuth Server-to-Server**

      ![Seleccionar método de autenticación](/help/forms/assets/adc-add-authentication-method.png)

>[!TAB Para las API de tiempo de ejecución de Forms adaptables]

1. **Haga clic en Agregar API**

   ![Agregar API](/help/forms/assets/adc-add-api.png)

2. **Seleccionar API de tiempo de ejecución y entrega de AEM Forms**
   1. En el cuadro de diálogo _Agregar API_, filtrar por **Experience Cloud**
   2. Seleccione **&quot;API de tiempo de ejecución y entrega de AEM Forms&quot;**
      ![Agregar API de comunicación de Forms](/help/forms/assets/adc-add-runtime-api.png)

   3. Haga clic en **Siguiente**
   4. Seleccione el método de autenticación **OAuth Server-to-Server**.
      ![Seleccionar método de autenticación](/help/forms/assets/adc-add-authentication-method.png)

>[!ENDTABS]

>[!NOTE]
>
> También puede agregar la API y el método de autenticación a su proyecto existente haciendo clic en **Agregar al proyecto** > **API**\
> ![Agregar API al proyecto existente](/help/forms/assets/add-api-existing-project.png)

### Añadir perfil de producto

El perfil de producto proporciona permisos (o autorización) para que las credenciales accedan a los recursos de AEM.

1. Seleccione el **perfil de producto** que coincida con la dirección URL de la instancia de AEM (`https://Service Type -Environment Type-Program XXX-Environment XXX.adobeaemcloud.com`).

   * **Tipo de servicio**: especifica servicios o permisos asociados con la instancia de AEM

   * **Tipo de entorno**: especifica si el entorno es para el servicio de creación o publicación

   * **Programa XXX** - identifica el ID del programa de Cloud Manager

   * **Entorno XXX** - identifica el ID de entorno específico dentro de ese programa

   >
   >
   > Los perfiles de producto están vinculados a una instancia de AEM específica (programa + entorno). Elija siempre el perfil que coincida con la dirección URL de su instancia.

2. Haga clic en **Guardar API configurada**. La API y el perfil de producto se añaden al proyecto

   ![Seleccionar configuración del proyecto](/help/forms/assets/adc-add-product-profile.png)

### Generar y guardar credenciales

1. Vaya al proyecto en Adobe Developer Console
2. Haga clic en la credencial **OAuth Server-to-Server**
3. Ver la sección **Detalles de credenciales**

   ![Ver credenciales](/help/forms/assets/adc-view-credential.png)

**Registrar credenciales de API**

```text
    API Credentials:
    ================
    Client ID: <your_client_id>
    Client Secret: <your_client_secret>
    Technical Account ID: <tech_account_id>
    Organization ID: <org_id>
    Scopes: AdobeID,openid,read_organizations
```

### Generación de token de acceso

Genere el token de acceso manualmente o mediante programación:

>[!BEGINTABS]

>[!TAB Para Pruebas]

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

>[!TAB Para Producción]

Generar tokens mediante programación usando la API [Adobe IMS](https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/security/setting-up-ims-integrations-for-aem-as-a-cloud-service):

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

>[!ENDTABS]

Ahora puede utilizar el token de acceso generado para hacer una llamada de API a entornos de desarrollo, fase o producción.

>[!NOTE]
>
> Para obtener más información sobre la implementación de servidor a servidor de OAuth para generar un token de acceso y realizar llamadas a la API, [haga clic aquí](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/implementation).

## Prácticas recomendadas: Administrar credenciales para desarrollo, ensayo y producción

* Utilice siempre credenciales independientes para desarrollo, ensayo y producción.

* Asigne cada credencial a la URL de entorno de AEM correcta.

* Almacene los secretos de forma segura y nunca los comprometa con el control de código fuente.

* Rastree la validez del token de acceso, ya que los tokens solo son válidos durante 24 horas.

## Próximos pasos

Para obtener información sobre cómo configurar el entorno para las API de comunicación sincrónica de Forms, consulte [Procesamiento sincrónico de comunicaciones de AEM Forms as a Cloud Service](/help/forms/aem-forms-cloud-service-communications-on-demand-processing.md).


## Artículos relacionados

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


