---
title: Compatibilidad con Open ID Connect para AEM as a Cloud Service en el nivel de publicación
description: Obtenga información sobre cómo configurar Open ID Connect (OIDC) para AEM as a Cloud Service en el nivel de publicación
feature: Security
role: Admin
exl-id: d2f30406-546c-4a2f-ba88-8046dee3e09b
source-git-commit: bf35f847f6f00d21915dfedb10cf38ea74344988
workflow-type: tm+mt
source-wordcount: '1469'
ht-degree: 1%

---

# Compatibilidad con Open ID Connect para AEM as a Cloud Service en el nivel de publicación

## Introducción {#introduction}

A medida que las organizaciones modernizan sus experiencias digitales, la administración de identidades segura y escalable se convierte en un requisito básico. Adobe Experience Manager (AEM) Cloud Service ahora es compatible con OpenID Connect (OIDC) en el nivel de publicación, lo que permite una integración perfecta y basada en estándares con los principales proveedores de identidad (IdPs), como Entra ID (Azure AD), Google, Okta, Auth0, Ping Identity, ForgeRock y OIDC con los IDP admitidos.

OIDC es una capa de identidad que se suma al protocolo OAuth 2.0, que permite una autenticación de usuario sólida y, al mismo tiempo, mantiene la simplicidad para los desarrolladores. Se ha adoptado ampliamente en los escenarios de portal de socio, intranet y entre empresas (B2C), en los que se requieren federaciones de identidad e inicio de sesión de usuarios seguras.

Hasta ahora, los clientes de AEM eran responsables de implementar su propia lógica de inicio de sesión personalizada en el nivel de publicación, lo que aumentó el tiempo de desarrollo e introdujo desafíos de mantenimiento y seguridad a largo plazo. Con la compatibilidad nativa con OIDC, AEM Cloud Service elimina esta carga al proporcionar un mecanismo de autenticación seguro, extensible y compatible con Adobe para los usuarios finales que acceden a entornos de publicación.

Tanto si desea ofrecer un sitio web personalizado para consumidores como un portal interno autenticado, OIDC en Publish simplifica la federación de identidades y reduce el riesgo mediante la gobernanza de identidades centralizada. También ayuda a las organizaciones a cumplir con los estándares modernos de cumplimiento y seguridad sin sacrificar la agilidad.

## Configuración de AEM para la autenticación de OIDC {#configure-aem-oidc-authentication}

### Requisitos previos {#prerequisits}

Suponemos que la siguiente información está disponible o definida:

1. Las rutas del contenido que se va a proteger en el repositorio de AEM
1. Un identificador para el IdP que se va a configurar. Puede ser cualquier cadena

Información de la configuración de IdP:

1. El ID de cliente configurado en el IdP
1. El Secreto del cliente configurado en el Idp. Si PKCE se configuró en el Idp, el Secreto del cliente no está disponible. No almacene el valor de texto sin formato en el archivo de configuración. Usar un secreto de CM y hacer referencia a él
1. Los ámbitos configurados en el Id. Se debe proporcionar al menos el ámbito `openid`
1. Si PKCE está habilitado en el IdP
1. El `callbackUrl` se define mediante una de las rutas configuradas definidas en el punto 1 y agregando el sufijo: `/j_security_check`
1. `baseUrl` para obtener acceso al archivo estándar `.well-known`. Por ejemplo, si la dirección URL conocida es: `https://login.microsoftonline.com/53279d7a-438f-41cd-a6a0-fdb09efc8891/v2.0/.well-known/openid-configuration`, `baseUrl` es: `https://login.microsoftonline.com/53279d7a-438f-41cd-a6a0-fdb09efc8891`

### Descripción general de los archivos de configuración {#overview-of-the-configuration-files}

A continuación, encontrará una lista de los archivos que se deben configurar:

1. **Conexión de OIDC**: esto lo usará `OidcAuthenticationHandler` para autenticar a los usuarios, o otros componentes para [autorizar el acceso a los recursos protegidos por el IdP mediante OAuth](https://github.com/apache/sling-org-apache-sling-auth-oauth-client)
1. **Controlador de autenticación OIDC**: Este es el controlador de autenticación usado para autenticar a los usuarios que tienen acceso a las rutas configuradas
1. **UserInfoProcessor**: este componente procesa la información recibida por el IdP. Los clientes pueden ampliarla para implementar lógica personalizada
1. [**Controlador de sincronización predeterminado**](https://jackrabbit.apache.org/oak/docs/security/authentication/external/defaultusersync.html): este componente crea el usuario en el repositorio
1. [**ExternalLoginModule**](https://jackrabbit.apache.org/oak/docs/security/authentication/externalloginmodule.html): Este componente autentica al usuario en el repositorio local de Oak.

El diagrama siguiente muestra cómo se vinculan los elementos de configuración mencionados. Tenga en cuenta que como estos son `ServiceFactory` componentes, `~uniqueid` puede ser cualquier cadena única aleatoria:

![Diagrama de configuración de OIDC](/help/security/assets/oidc-diagram.png)

### Configuración de la conexión de OIDC {#configure-the-oidc-connection}

En primer lugar, es necesario configurar la conexión de OIDC. Se pueden configurar varias conexiones de OIDC, y cada una debe tener un nombre diferente.

1. Cree un nuevo archivo de `.cfg.json` que alojará la configuración. Por ejemplo, puede usar `org.apache.sling.auth.oauth_client.impl.OidcConnectionImpl~azure.cfg.json`: el sufijo **azure** debe ser un identificador único para la conexión
1. Siga el formato de configuración en el ejemplo siguiente:

   ```
   {
    "name":"azure",
    "scopes":[
      "openid"
    ],
    "baseUrl":"<https://login.microsoftonline.com/53279d7a-438f-41cd-a6a0-fdb09efc8891/v2.0>",
    "clientId":"5199fc45-8000-473e-ac63-989f1a78759f",
    "clientSecret":"xxxxxx"
   }
   ```

1. Configure sus propiedades como se indica a continuación:
   * El usuario puede definir **&quot;name&quot;**
   * `baseUrl`, `clientid` y `clientSecret` son valores de configuración que provienen del IdP.
   * Los ámbitos deben contener al menos el valor `openid`.

### Configurar controlador de autenticación OIDC {#configure-oidc-authentication-handler}

Ahora, configure el controlador de autenticación OIDC. Se pueden configurar varias conexiones de OIDC. Cada uno debe tener un nombre diferente. Si comparten el mismo [proveedor de identidad externa de OAK](https://jackrabbit.apache.org/oak/docs/security/authentication/identitymanagement.html), pueden compartir usuarios.

1. Cree el archivo de configuración. Para este ejemplo, utilizaremos `org.apache.sling.auth.oauth_client.impl.OidcConnectionImpl~azure.cfg.json`. El sufijo `azure` debe ser un identificador único. Consulte un ejemplo del archivo de configuración a continuación:

   ```
   {
     "path":"/content/tests/us/en/test-7",
     "callbackUri":"http://localhost:14503/content/tests/us/en/test-7/j_security_check",
     "pkceEnabled":false,
     "defaultConnectionName":"azure"
     "idp": "azure-idp"
   }
   ```

1. A continuación, configure sus propiedades como se indica a continuación:
   * `path`: la ruta que se va a proteger
   * `callbackUri`: a la ruta que se va a proteger, agregando el sufijo: `/j_security_check`
   * `defaultConnectionName`: configure con el mismo nombre definido para la conexión de OIDC en el paso anterior+
   * `pkceEnabled`: `true` clave de revisión para intercambio de código (PKCE) en el flujo del código de autorización
   * `idp`: nombre del [proveedor de identidad externo de OAK](https://jackrabbit.apache.org/oak/docs/security/authentication/identitymanagement.html). Tenga en cuenta que diferentes IDP de OAK no pueden compartir usuarios o grupos

### Configurar SlingUserInfoProcessor

1. Cree el archivo de configuración. Para este ejemplo, utilizaremos `org.apache.sling.auth.oauth_client.impl.SlingUserInfoProcessor~azure.cfg.json`. El sufijo `azure` debe ser un identificador único. Consulte un ejemplo del archivo de configuración a continuación:

   ```
   {
      "groupsInIdToken":true,
      "groupsClaimName": "groups",
      "connection":"azure",
      "storeAccessToken": false,
      "storeRefreshToken": false
   }
   ```

1. A continuación, configure sus propiedades como se indica a continuación:
   * `groupsInIdToken`: Se establece en true si los grupos se envían con el token de ID. Si el valor es false o no se especifica, los grupos se leen desde el extremo UserInfo.
   * `groupsClaimName`: el nombre de la notificación contiene los grupos que se van a sincronizar en AEM.
   * `connection`: configure con el mismo nombre definido para la conexión de OIDC en el paso anterior
   * `storeAccessToken`: verdadero si el token de acceso debe almacenarse en el repositorio. De forma predeterminada, este valor es false. Configúrelo como true solo si AEM necesita acceder a recursos en nombre del usuario almacenado en servidores externos protegidos por el mismo IdP.
   * `storeRefreshToken`: verdadero si el token de actualización debe almacenarse en el repositorio. De forma predeterminada, este valor es false. Configúrelo como true solo si AEM necesita acceder a recursos en nombre del usuario almacenado en servidores externos protegidos por el mismo IdP y necesita actualizar el token desde el IdP.
Observe que el token de acceso y el token de actualización se almacenan cifrados con la clave maestra de AEM.


### Configurar el controlador de sincronización {#configure-the-synchronization-handler}

Debe haber al menos un controlador de sincronización configurado para sincronizar los usuarios autenticados en Oak. Para obtener más información, consulte [esta página de ](https://jackrabbit.apache.org/oak/docs/security/authentication/external/defaultusersync.html).

Cree un archivo con el nombre `org.apache.jackrabbit.oak.spi.security.authentication.external.impl.DefaultSyncHandler~azure.cfg.json`. El sufijo **azure** debe ser un identificador único. Para obtener más información sobre cómo configurar sus propiedades, consulte la [Documentación de sincronización de grupos y usuarios de Oak](https://jackrabbit.apache.org/oak/docs/security/authentication/external/defaultusersync.html). A continuación encontrará un ejemplo de configuración:

```
{
  "user.expirationTime":"300s",
  "user.membershipExpTime":"300s",
  "user.propertyMapping":[
    "profile/familyName=profile/familyName",
    "profile/givenName=profile/givenName",
    "rep:fullname=cn",
    "profile/email=profile/email",
    "oauth-tokens"
  ],
  "user.pathPrefix":"azure",
  "handler.name":"azure"
}
```

A continuación, se muestran algunos de los atributos más relevantes que se van a configurar en DefaultSyncHandler. Tenga en cuenta que la pertenencia a grupos dinámicos siempre debe estar habilitada en Cloud Services.

| Nombre de la propiedad | Notas | Valor sugerido |
|---|---|---|
| `user.expirationTime` | Duración hasta que caduque un usuario sincronizado. Los usuarios se sincronizan solo después de la hora de caducidad. | 1 h |
| `user.membershipExpTime` | Duración hasta que caduque una pertenencia a un usuario sincronizado. Las suscripciones de los usuarios solo se sincronizan después de la hora de caducidad. | 1 h |
| `user.dynamicMembership` | Se recomienda habilitar la pertenencia a grupos dinámicos | true |
| `user.enforceDynamicMembership` | Se recomienda habilitar la aplicación de la pertenencia a grupos dinámicos | true |
| `group.dynamicGroups` | Se recomienda habilitar los grupos dinámicos | true |
| user.propertyMapping | La implementación proporcionada de `UserInfoProcessor` sincroniza solo algunas propiedades. Se puede modificar y personalizar. | <code>&quot;profile/givenName=profile/given_name&quot;,</code><br><code>&quot;profile/familyName=profile/family_name&quot;,</code><br><code>&quot;rep:fullname=perfil/nombre&quot;,</code><br><code>&quot;profile/email=profile/email&quot;,</code><br><code>&quot;access_token=access_token&quot;,</code><br><code>&quot;refresh_token=refresh_token&quot;</code> |  |
| `user.membershipNestingDepth` | Devuelve la profundidad máxima de anidamiento de grupos cuando se sincronizan las relaciones de pertenencia. Un valor de 0 deshabilita de forma efectiva la búsqueda de miembros del grupo. El valor 1 solo agrega los grupos directos de un usuario. Este valor no tiene ningún efecto cuando se sincronizan grupos individuales únicamente cuando se sincroniza una ascendencia de pertenencia de usuarios. | 1 |

### Configuración del módulo de inicio de sesión externo {#configure-the-external-login-module}

Finalmente, debe configurar el módulo de inicio de sesión externo.

1. Cree un archivo con el nombre `org.apache.jackrabbit.oak.spi.security.authentication.external.impl.ExternalLoginModuleFactory~azure.cfg.json`. Consulte un ejemplo de configuración a continuación:

   ```
   {
    "sync.handlerName":"azure",
    "idp.name":"azure-idp"
   }
   ```

1. Configure sus propiedades como se indica a continuación:

   * `sync.handlerName`: nombre del controlador de sincronización definido anteriormente
   * `idp.name`: proveedor de identidad de OAK definido en el controlador de autenticación OIDC

### Opcional: Implementar un UserInfoProcessor personalizado {#implement-a-custom-userinfoprocessor}

El usuario se autentica mediante un token de ID y se recuperan atributos adicionales en el extremo `userInfo` definido para el IdP. Si se deben realizar operaciones no estándar adicionales, la implementación predeterminada de Sling es una implementación personalizada de [UserInfoProcessor](https://github.com/apache/sling-org-apache-sling-auth-oauth-client/blob/master/src/main/java/org/apache/sling/auth/oauth_client/impl/SlingUserInfoProcessorImpl.java).

## Ejemplo: Configurar la autenticación de OIDC con Azure Active Directory

### Configurar una nueva aplicación en Azure Active Directory {#configure-a-new-application-in-azure-ad}

1. Cree una nueva aplicación en Azure Active Directory siguiendo la [documentación de Azure Active Directory](https://learn.microsoft.com/en-us/power-pages/security/authentication/openid-settings#create-an-app-registration-in-azure).  Consulte a continuación el aspecto que debería tener la pantalla que detalla la descripción general de la aplicación:

   ![Descripción general de la aplicación](/help/security/assets/odic-application-overview.png)

1. Si se requieren grupos o funciones de aplicación, siga la [documentación](https://learn.microsoft.com/en-us/entra/external-id/customers/how-to-use-app-roles-customers) para habilitarlos en la aplicación y enviarlos en el token de ID. A continuación, se muestra un ejemplo de grupos configurados:

![Identificador de token de reclamación de OIDC](/help/security/assets/oidc-claim-id-token.png)

1. Siga los pasos documentados anteriormente para crear los archivos de configuración necesarios. A continuación, se muestra un ejemplo específico de Azure AD donde:
   * Definimos el nombre de Conexión oidc, Controlador de autenticación y Controlador de sincronización predeterminada como: `azure`
   * La dirección URL del sitio web es: `www.mywebsite.com`
   * Protegemos la ruta `/content/wknd/us/en/adventures`
   * El usuario es: `tennat-id`,
   * ID de cliente: `client-id`,
   * El secreto es: `secret`,
   * Los grupos se envían en el token de ID en una notificación llamada: `groups`

#### org.apache.sling.auth.oauth_client.impl.OidcConnectionImpl~azure.cfg.json

```
{
  "name":"azure",
  "scopes":[
    openid", "User.Read", "profile", "email
  ],
  "baseUrl":"https://login.microsoftonline.com/tenant-id/v2.0",
  "clientId":"client-id",
  "clientSecret":"secret"
}
```

#### org.apache.sling.auth.oauth_client.impl.OidcAuthenticationHandler~azure.cfg.json

```
{
  "callbackUri":"https://www.mywebsite.com/content/wknd/us/en/adventures/j_security_check",
  "path":[
    "/content/wknd/us/en/adventures"
  ],
  "idp":"azure",
  "defaultConnectionName":"azure"
}
```

#### org.apache.jackrabbit.oak.spi.security.authentication.external.impl.ExternalLoginModuleFactory~azure.cfg.json

```
{
  "sync.handlerName":"azure",
  "idp.name":"azure"
}
```

#### org.apache.jackrabbit.oak.spi.security.authentication.external.impl.DefaultSyncHandler~azure.cfg.json

```
{
  "user.expirationTime":"1s",
  "user.membershipExpTime":"1s",
  "user.propertyMapping":[
    "profile/givenName=profile/given_name",
    "profile/familyName=profile/family_name",
    "rep:fullname=profile/name",
    "profile/email=profile/email",
    "access_token=access_token",
    "refresh_token=refresh_token"
  ],
  "user.pathPrefix":"azure",
  "group.pathPrefix": "oidc",
  "user.membershipNestingDepth": "1",
  "handler.name":"azure"
}
```

#### org.apache.sling.auth.oauth_client.impl.SlingUserInfoProcessorImpl~azure.cfg.json

```
{
  "groupsInIdToken": "true",
  "storeAccessToken": "false",
  "storeRefreshToken": "false",
  "connection": "azure",
  "groupsClaimName": "groups"
}
```

### Información adicional acerca de los grupos de Azure AD {#additional-information-about-azure-ad-groups}

Para configurar un grupo en para la aplicación empresarial en el portal de Microsoft Azure, debe buscar en la aplicación: **Aplicaciones empresariales** y agregar los grupos: <!-- Alexandru: this bit cound be clearer-->

![Agregar grupo OIDC](/help/security/assets/oidc-ad-additional-info.png)

Para habilitar la notificación de grupo en el token de id., agregue la notificación a la sección **Configuración del token** del portal de Microsoft Azure: <!-- Alexandru: this bit cound be clearer as well-->

![Identificador de token de reclamación de OIDC](/help/security/assets/oidc-claim-id-token.png)

La configuración de `SlingUserInfoProcessor` debe modificarse como en el ejemplo siguiente.

El nombre de archivo que debe modificarse es `org.apache.sling.auth.oauth_client.impl.SlingUserInfoProcessorImpl.cfg.json`. El contenido debe configurarse de la siguiente manera:

```
{
  "connection": "azure",
  "groupsInIdToken": "true",
  "storeAccessToken": "false",
  "storeRefreshToken": "false"
}
```
