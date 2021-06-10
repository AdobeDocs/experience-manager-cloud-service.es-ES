---
title: Compatibilidad con OAuth2 para el servicio de correo
description: Compatibilidad con Oauth2 para el servicio de correo en Adobe Experience Manager as a Cloud Service
source-git-commit: b46062697b25aa8d3f215a8a4249f5203bec268e
workflow-type: tm+mt
source-wordcount: '674'
ht-degree: 0%

---


# Soporte de OAuth2 para el servicio de correo {#oauth2-support-for-the-mail-service}

AEM as a Cloud Service ofrece compatibilidad con OAuth2 para su servicio de correo integrado, con el fin de permitir que las organizaciones se adhieran a los requisitos de correo electrónico seguros.

Puede configurar OAuth para varios proveedores de correo electrónico. A continuación se proporcionan instrucciones paso a paso para configurar el servicio de correo AEM para autenticarse mediante OAuth2 con Microsoft Office 365 Outlook. Otros proveedores se pueden configurar de manera similar.

Para obtener más información sobre el AEM como servicio de correo Cloud Service, consulte [Envío de correo electrónico](/help/implementing/developing/introduction/development-guidelines.md#sending-email).

## Microsoft Outlook {#microsoft-outlook}

1. Vaya a [https://portal.azure.com/](https://portal.azure.com/) e inicie sesión.
1. Busque **Azure Active Directory** en la barra de búsqueda y haga clic en el resultado. También puede navegar directamente a [https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview)
1. Haga clic en **Registro de aplicaciones** - **Nuevo registro**

   ![](assets/oauth-outlook1.png)

1. Rellene la información según sus necesidades y haga clic en **Registrar**
1. Vaya a la aplicación recién creada y seleccione **Permisos de API**
1. Vaya a **Agregar permiso** - **Permiso de gráfico** - **Permisos delegados**
1. Seleccione los siguientes permisos para su aplicación y haga clic en **Agregar permiso**:
   * `SMTP.Send`
   * `Mail.Read`
   * `Mail.Send`
   * `openid`
   * `offline_access`
1. Vaya a **Autenticación** - **Agregar una plataforma** - **Web** y, en la sección **Direccionamiento Url**, añada las siguientes direcciones URL: una con y otra sin barra diagonal:
   * `http://localhost/`
   * `http://localhost`
1. Pulse **Configurar** después de añadir cada URL y configurar los ajustes según sus necesidades
1. A continuación, vaya a **Certificates and Secrets**, haga clic en **New client secret** y siga los pasos de la pantalla para crear un secreto. Asegúrese de tomar nota de este secreto para utilizarlo posteriormente
1. Pulse **Overview** en el panel izquierdo y copie los valores de **Application (client) ID** e **Directory (tenant) ID** para usarlos más adelante

Para recapitular, necesitará la siguiente información para configurar OAuth2 para el servicio de correo en el lado AEM:

* La URL de autenticación, que se construirá con el ID del inquilino. Tendrá este formulario: `https://login.microsoftonline.com/<tenantID>/oauth2/v2.0/authorize`
* La URL del token, que se construirá con el ID del inquilino. Tendrá este formulario: `https://login.microsoftonline.com/<tenantID>/oauth2/v2.0/token`
* La URL de actualización, que se construirá con el ID del inquilino. Tendrá este formulario: `https://login.microsoftonline.com/<tenantID>/oauth2/v2.0/token`
* El ID de cliente
* El secreto del cliente

### Generación del token de actualización {#generating-the-refresh-token}

A continuación, debe generar el token de actualización, que formará parte de la configuración OSGi en un paso posterior.

Para ello, siga estos pasos:

1. Abra la siguiente URL en el explorador después de reemplazar `clientID` y `tenantID` por los valores específicos de su cuenta: `https://login.microsoftonline.com/<tenantID>/oauth2/v2.0/authorize?client_id=<clientId>&response_type=code&redirect_uri=http://localhost&response_mode=query&scope=https%3A%2F%2Foutlook.office365.com%2FSMTP.Send%20EWS.AccessAsUser.All%20https%3A%2F%2Foutlook.office365.com%2FSMTP.Send%20https%3A%2F%2Foutlook.office365.com%2FMail.Read%20https%3A%2F%2Foutlook.office365.com%2FMail.Send%20openid%20offline_access&state=12345`
1. Permitir permiso cuando se le pida
1. La dirección URL se redireccionará a una nueva ubicación, construida con este formato: `http://localhost/?code=<code>&state=12345&session_state=4f984c6b-cc1f-47b9-81b2-66522ea83f81#`
1. Copie el valor de `<code>` en el ejemplo anterior
1. Utilice el siguiente comando cURL para obtener el refreshToken. Debe reemplazar tenantID, clientID y clientSecret con los valores de su cuenta, así como el valor de `<code>`:

   `curl --location --request POST 'https://login.microsoftonline.com/<tenantId>/oauth2/v2.0/token' \
--header 'Content-Type: application/x-www-form-urlencoded' \
--header 'Cookie: buid=0.ARgAep0nU49DzUGmoP2wnvyIkcQjsx26HEpOnvHS0akqXQgYAAA.AQABAAEAAAD--DLA3VO7QrddgJg7Wevry9XPJSKbGVlPt5NWYxLtTl3K1W0LwHXelrffApUo_K02kFrkvmGm94rfBT94t25Zq4bCd5IM3yFOjWb3V22yDM7-rl112sLzbBQBRCL3QAAgAA; esctx=AQABAAAAAAD--DLA3VO7QrddgJg7Wevr4a8wBjYcNbBXRievdTOd15caaeAsQdXeBAQA3tjVQaxmrOXFGkKaE7HBzsJrzA-ci4RRpor-opoo5gpGLh3pj_iMZuqegQPEb1V5sUVQV8_DUEbBv5YFV2eczS5EAhLBAwAd1mHx6jYOL8LwZNDFvd2-MhVXwPd6iKPigSuBxMogAA; x-ms-gateway-slice=estsfd; stsservicecookie=estsfd; fpc=Auv6lTuyAP1FuOOCfj9w0U_5vR5dAQAAALDXP9gOAAAAwIpkkQEAAACT2T_YDgAAAA' \
--data-urlencode 'client_id=<clientID>' \
--data-urlencode 'scope=https://outlook.office365.com/SMTP.Send https://outlook.office365.com/Mail.Read https://outlook.office365.com/Mail.Send openid' \
--data-urlencode 'redirect_uri=http://localhost' \
--data-urlencode 'grant_type=authorization_code' \
--data-urlencode 'client_secret=<clientSecret>' \
--data-urlencode 'code=<code>'`

1. Tome nota de refreshToken y accessToken.

### Validación de tokens {#validating-the-tokens}

Antes de configurar OAuth en el lado AEM, asegúrese de validar accessToken y refreshToken con el siguiente procedimiento:

1. Genere el accessToken utilizando el refreshToken producido en el procedimiento anterior. Puede conseguirlo con el siguiente curl, reemplazando los valores para `<client_id>`,`<client_secret>` y `<refreshToken>`:

   `curl --location --request POST 'https://login.microsoftonline.com/<tenetId>/oauth2/v2.0/token' \
--header 'Content-Type: application/x-www-form-urlencoded' \
--header 'Cookie: buid=0.ARgAep0nU49DzUGmoP2wnvyIkcQjsx26HEpOnvHS0akqXQgYAAA.AQABAAEAAAD--DLA3VO7QrddgJg7Wevry9XPJSKbGVlPt5NWYxLtTl3K1W0LwHXelrffApUo_K02kFrkvmGm94rfBT94t25Zq4bCd5IM3yFOjWb3V22yDM7-rl112sLzbBQBRCL3QAAgAA; esctx=AQABAAAAAAD--DLA3VO7QrddgJg7Wevr4a8wBjYcNbBXRievdTOd15caaeAsQdXeBAQA3tjVQaxmrOXFGkKaE7HBzsJrzA-ci4RRpor-opoo5gpGLh3pj_iMZuqegQPEb1V5sUVQV8_DUEbBv5YFV2eczS5EAhLBAwAd1mHx6jYOL8LwZNDFvd2-MhVXwPd6iKPigSuBxMogAA; x-ms-gateway-slice=estsfd; stsservicecookie=estsfd; fpc=Auv6lTuyAP1FuOOCfj9w0U_IezHLAQAAAPeNSdgOAAAA' \
--data-urlencode 'client_id=<client_id>' \
--data-urlencode 'scope=https://outlook.office365.com/SMTP.Send https://outlook.office365.com/Mail.Read https://outlook.office365.com/Mail.Send openid' \
--data-urlencode 'redirect_uri=http://localhost' \
--data-urlencode 'grant_type=refresh_token' \
--data-urlencode 'client_secret=<client_secret>' \
--data-urlencode 'refresh_token=<refreshToken>'`

1. Envíe un correo utilizando accessToken para ver si funciona correctamente.

>[!NOTE]
>
> Puede obtener la colección de la API Postman de [esta ubicación](https://docs.microsoft.com/en-us/azure/active-directory/develop/v2-oauth2-auth-code-flow).

### Integración con AEM como Cloud Service {#integration-with-aem-as-a-cloud-service}

1. Cree un archivo de propiedad OSGI denominado `com.day.cq.mailer.oauth.impl.OAuthConfigurationProviderImpl.cfg.json` en `/apps/<my-project>/osgiconfig/config` con la siguiente sintaxis:

   ```
   {
       authUrl: "<Authorization Url>",
       tokenUrl: "<Token Url>",
       clientId: "<clientID>",
       clientSecret: "$[secret:SECRET_SMTP_OAUTH_CLIENT_SECRET]",
       scopes: [
          "scope1",
          "scope2"
       ],
       refreshUrl: "<Refresh token Url>",
       refreshToken: "$[secret:SECRET_SMTP_OAUTH_REFRESH_TOKEN]"
   }
   ```

1. Complete `authUrl`, `tokenUrl` y `refreshURL` construyéndolos como se describe en la sección anterior.
1. Agregue los siguientes ámbitos a la configuración:
   * `openid`
   * `offline_access`
   * `https://outlook.office365.com/Mail.Send`
   * `https://outlook.office365.com/Mail.Read`
   * `https://outlook.office365.com/SMTP.Send`
1. Crear un archivo de propiedad OSGI `called com.day.cq.mailer.impl.DefaultMailService.cfg.json`
under 
`/apps/<my-project>/osgiconfig/config`  con la siguiente sintaxis:

   ```
   {
    "smtp.host": "<smtp hostname>"
    "smtp.user": "<user account that logged into get the oauth tokens>",
    "smtp.password": "value not used",
    "smtp.port": 587,
    "from.address": "<from address used for sending>"
    "smtp.ssl": false,
    "smtp.starttls": true,
    "smtp.requiretls": true,
    "debug.email": false,
    "oauth.flow": true
   }
   ```

1. Para outlook, el valor de configuración `smtp.host` es `smtp.office365.com`
1. En tiempo de ejecución, pase los secretos `refreshToken values` y `clientSecret` utilizando la API de variables de Cloud Manager como se describe [aquí](/help/implementing/deploying/configuring-osgi.md#setting-values-via-api). Se deben definir los valores de las variables `SECRET_SMTP_OAUTH_REFRESH_TOKEN` y `SECRET_SMTP_OAUTH_CLIENT_SECRET`.

### Solución de problemas {#troubleshooting}

Si el servicio de correo no funciona correctamente, en la mayoría de los casos deberá volver a generar el `refreshToken` como se ha descrito anteriormente, pasando el nuevo valor a través de la API de Cloud Manager. El nuevo valor tardará unos minutos en implementarse.
