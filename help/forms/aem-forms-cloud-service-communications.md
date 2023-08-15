---
title: AEM Forms as a Cloud Service - Comunicaciones
description: Combine datos automáticamente con plantillas XDP y PDF o genere salidas en formato PCL, ZPL y PostScript
exl-id: 9fa9959e-b4f2-43ac-9015-07f57485699f
source-git-commit: 5ad33f0173afd68d8868b088ff5e20fc9f58ad5a
workflow-type: tm+mt
source-wordcount: '683'
ht-degree: 94%

---


# Usar el procesamiento sincrónico {#sync-processing-introduction}

Las API de comunicaciones as a Cloud Service de Forms le permiten crear, montar y entregar comunicaciones personalizadas y orientadas a la marca, como correspondencia comercial, documentos, declaraciones, cartas de procesamiento de reclamaciones, avisos de beneficios, cartas de procesamiento de reclamaciones, facturas mensuales y kits de bienvenida. Puede utilizar las API de Comunicaciones para combinar una plantilla (XFA o PDF) con datos de clientes para generar documentos en los formatos PDF, PS, PCL, DPL, IPL y ZPL.

Imagine un escenario en el que tiene una o más plantillas y varios registros de datos XML en cada plantilla. Puede utilizar las API de Comunicaciones para generar un documento de impresión para cada registro. <!-- You can also combine the records into a single document. --> El resultado es un documento PDF no interactivo. Un documento PDF no interactivo no permite a los usuarios introducir datos en los campos.

Forms as a Cloud Service: Comunicaciones proporciona la API bajo demanda y por lotes (API asincrónicas) para la generación programada de documentos:

* Las API sincrónicas son adecuadas para casos de uso de generación de documentos bajo demanda, con baja latencia y de registro único. Estas API son más adecuadas para casos de uso basados en las acciones del usuario. Por ejemplo, generar un documento después de que un usuario rellene un formulario.

* Las API por lotes (API asíncronas) son adecuadas para casos de uso planificados de alto rendimiento y de generación de múltiples documentos. Estas API generan documentos por lotes. Por ejemplo, facturas telefónicas, extractos de tarjetas de crédito y declaraciones de beneficios generados cada mes.

## Usar operaciones sincrónicas {#batch-operations}

Una operación sincrónica es un proceso de generación de documentos de forma lineal. Estas API están clasificadas como de un solo inquilino y de varios:

### API de un solo inquilino

* API de generación de documentos
* API de manipulación de documentos

<!-- 
### Multi-tenant APIs

* Document utility APIs -->


### Autenticación de una API de un solo inquilino

Las operaciones de API de un solo inquilino admiten dos tipos de autenticación:

* **Autenticación básica**: la autenticación básica es un esquema de autenticación simple integrado en el protocolo HTTP. El cliente envía peticiones HTTP con el encabezado Autorización que contiene la palabra “Basic” seguida de un espacio y un nombre de usuario:contraseña de cadena codificados en Base64. Por ejemplo, para autorizar como administrador/administrador, el cliente envía Basic [nombre de usuario de cadena codificado en Base64]: [contraseña de cadena codificada en Base64].

* **Autenticación basada en tokens:** la autenticación basada en tokens utiliza un token de acceso (token de autenticación del portador) para realizar solicitudes a Experience Manager as a Cloud Service. AEM Forms as a Cloud Service proporciona API para recuperar de forma segura el token de acceso. Para recuperar y utilizar el token para autenticar una solicitud:

   1. [Recupere las credenciales de Experience Manager as a Cloud Service desde Developer Console](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/service-credentials.html?lang=es).
   1. [Instale las credenciales de Experience Manager as a Cloud Service en su entorno](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/service-credentials.html?lang=es). (Servidor de aplicaciones, servidor web u otros servidores no AEM) configurados para enviar solicitudes (realizar llamadas) al servicio en la nube.
   1. [Genere un token JWT e intercámbielo con las API de IMS de Adobe por un token de acceso](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/service-credentials.html?lang=es).
   1. Ejecute la API de Experience Manager con el token de acceso como token de autenticación del portador.
   1. [Establezca los permisos adecuados para el usuario de la cuenta técnica en el entorno de Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/service-credentials.html?lang=es#configuraci%C3%B3n-del-acceso-en-aem).

  >[!NOTE]
  >
  >Adobe recomienda utilizar la autenticación basada en token en un entorno de producción.

<!-- 

### Authenticate a multi-tenant API

#### Authentication Headers

Every inbound HTTP API call to the multi-tenant API must contain these three headers:


* `x-api-key`
* `x-gw-ims-org-id`
* `Authorization`

The values which should be sent in the `x-api-key` and `x-gw-ims-org-id` headers are provided in the Credentials details screen in the [Adobe Developer Console](https://developer.adobe.com/console). The value of the `x-api-key` header is the Client ID and the value for the `x-gw-ims-org-id` header is the Organization ID.

#### Configure Adobe Developer console to generate an access token

To set up authentication APIs, create a project in Adobe Developer Console and add Communication APIs to the project on Adobe Developer Console. The integration generates API Key, Client Secret, Payload (JWT):

1. Contact you Adobe Developer Console administrator. Ask the administrator to add as a developer.
1. Log in to `https://developer.adobe.com/console/`. Use your developer account that your administrator has provisioned to log in to Adobe Developer Console.
1. Select your organization from the top-right corner. If you do not know your organization, contact your administrator.
1. Tap **[!UICONTROL Create new project]**. A screen to get started with your new project appears. Tap **[!UICONTROL Add API]**. A screen with list of all the APIs enabled for your account appears.
1. Select **[!UICONTROL AEM Forms - Communications]** and tap **[!UICONTROL Next]**. A screen to configure the API appears.
1. Select **[!UICONTROL OPTION 1 Generate a key pair]** and tap **[!UICONTROL Generate keypair]**. It creates and downloads the configuration file. The downloaded configuration file contains all your app settings, along with the only copy of your private key. Adobe does not record your private key, make sure to securely store the downloaded file. Tap **[!UICONTROL Next]**.
1. Select **[!UICONTROL Integrations - Cloud Service]** and tap **[!UICONTROL Save configured API]**. Tap **[!UICONTROL Service Account (JWT)]** to view the API Key, Client Secret, and other information required to access the APIs. You set to use the token to access the APIs.

#### Programmatically generate and use an access token

To programmatically generate an access token, generate a JSON Web Token (JWT) and exchange it with the Adobe Identity Management Service (IMS) for an access token.

Use the following keys, referred to as claims, to construct JWT JSON object:


* `exp`- the requested expiration of the access token, expressed as a number of seconds since January 1, 1970 GMT. For most use cases, this is a relatively small value. For example, 5 minutes, for five minutes from now, this value should be 1670923791.
* `iss` - the Organization ID from the Adobe Developer Console project, in the format org_ident@AdobeOrg.
* `sub` - the Technical Account ID from the Adobe Developer Console integration, in the format: id@techacct.adobe.com.
* `aud` - the Client ID from the Adobe Developer Console integration prepended with `https://ims-na1.adobelogin.com/c/`.
* `https://ims-na1-stg1.adobelogin.com/s/ent_aemforms_docprocessing` - set to the literal value `true`

This JSON object must be then base64 encoded and signed using the private key for the project. Finally, the encoded value is sent in the body of a POST request to `https://ims-na1.adobelogin.com/ims/exchange/jwt` along with the Client ID and Client Secret for the project.

##### Example

```JSON

    ========================= REQUEST ==========================
    POST https://ims-na1.adobelogin.com/ims/exchange/jwt
    -------------------------- body ----------------------------
    client_id={myClientId}&client_secret={myClientSecret}&jwt_token={myJSONWebToken}
    ------------------------- headers --------------------------
    Content-Type: application/x-www-form-urlencoded
    Cache-Control: no-cache

```

#### Language Support for JWT

While it is possible to do the entire JWT generation and exchange process in custom code, it is more common to use a higher-level library to do so. A number of such libraries are listed on the [Adobe I/O JWT Documentation](https://developer.adobe.com/developer-console/docs/guides/authentication/JWT/).

-->

### (Solo para las API de generación de documentos) Configuración de recursos y permisos

Para utilizar API sincrónicas, se requiere lo siguiente:

* Usuarios con privilegios de administrador en Experience Manager
* Cargue plantillas y otros recursos a su instancia de Experience Manager Forms Cloud Service

### (Solo para las API de generación de documentos) Cargar plantillas y otros recursos en la instancia de Experience Manager

Una organización suele tener varias plantillas. Por ejemplo, una plantilla para los extractos de tarjetas de crédito, las declaraciones de beneficios y las solicitudes de reclamación. Cargue todas estas plantillas XDP y PDF en su instancia de Experience Manager. Para cargar una plantilla:

1. Abra su instancia de Experience Manager.
1. Vaya a Formularios > Formularios y documentos
1. Haga clic en Crear > Carpeta y cree una carpeta. Abra la carpeta.
1. Haga clic en Crear > Cargar archivo y cargue las plantillas.

### Invocar una API

La [documentación de referencia de la API](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/) ofrece información detallada sobre todos los parámetros, métodos de autenticación y diversos servicios que ofrecen las API. La documentación de referencia de la API también proporciona un archivo de definición de API en formato .yaml. Puede descargar el archivo .yaml y cargarlo en [Postman](https://www.postman.com/) para comprobar la funcionalidad de las API.

>[!VIDEO](https://video.tv.adobe.com/v/335771)

>[!NOTE]
>
>Solo los miembros del grupo de usuarios de Forms pueden acceder a las API de Comunicaciones.
