---
title: Compatibilidad con Open ID Connect para AEM as a Cloud Service en el nivel de publicación
description: Obtenga información sobre cómo configurar Open ID Connect (OIDC) para AEM as a Cloud Service en el nivel de publicación
feature: Security
role: Admin
exl-id: d2f30406-546c-4a2f-ba88-8046dee3e09b
source-git-commit: 75c2dbc4f1d77de48764e5548637f95bee9264dd
workflow-type: tm+mt
source-wordcount: '1986'
ht-degree: 71%

---

# Compatibilidad con Open ID Connect para AEM as a Cloud Service en el nivel de publicación {#open-id-connect-support-for-aem-as-a-cloud-service-on-publish-tier}

## Introducción {#introduction}

A medida que las organizaciones modernizan sus experiencias digitales, la administración de identidades segura y escalable se convierte en un requisito básico. Adobe Experience Manager (AEM) Cloud Service ahora es compatible con OpenID Connect (OIDC) en el nivel de publicación, lo que permite una integración perfecta y basada en estándares con los principales proveedores de identidad (IdPs), como Entra ID (Azure AD), Google, Okta, Auth0, Ping Identity, ForgeRock y OIDC con los IDP admitidos.

OIDC es una capa de identidad que se suma al protocolo OAuth 2.0, que permite una autenticación de usuario sólida y, al mismo tiempo, mantiene la simplicidad para los desarrolladores. Se ha adoptado ampliamente en los escenarios de portal de socio, intranet y de empresa a consumidor (B2C), en los que se requieren federaciones de identidad e inicio de sesión de usuarios seguras.

Hasta ahora, los clientes de AEM eran responsables de implementar su propia lógica de inicio de sesión personalizada en el nivel de publicación, lo que aumentó el tiempo de desarrollo e introdujo desafíos de mantenimiento y seguridad a largo plazo. Con la compatibilidad nativa con OIDC, AEM Cloud Service elimina esta carga al proporcionar un mecanismo de autenticación seguro, extensible y compatible con Adobe para los usuarios finales que acceden a entornos de publicación.

Tanto si desea ofrecer un sitio web personalizado para consumidores como un portal interno autenticado, OIDC en Publish simplifica la federación de identidades y reduce el riesgo mediante la gobernanza de identidades centralizada. También ayuda a las organizaciones a cumplir con los estándares modernos de cumplimiento y seguridad sin sacrificar la agilidad.

## Configuración de AEM para la autenticación de OIDC {#configure-aem-oidc-authentication}

### Requisitos previos {#prerequisits}

Suponemos que la siguiente información está disponible o definida:

1. Las rutas del contenido que se va a proteger en el repositorio de AEM
1. Un identificador para el IdP que se va a configurar. Puede ser cualquier cadena

Información de la configuración de IdP:

1. El ID de cliente configurado en el IdP
1. El Secreto del cliente configurado en el IdP. Si PKCE se configuró en el IdP, el Secreto del cliente no está disponible. No almacene el valor de texto sin formato en el archivo de configuración. Usar un secreto de CM y hacer referencia a él
1. Los ámbitos configurados en el IdP. Se debe proporcionar al menos el ámbito `openid`
1. Si PKCE está habilitado en el IdP
1. El `callbackUrl` se define mediante una de las rutas configuradas definidas en el punto 1 y añadiendo el sufijo: `/j_security_check`
1. El `baseUrl` para obtener acceso al archivo estándar `.well-known`. Por ejemplo, si la dirección URL conocida es: `https://login.microsoftonline.com/53279d7a-438f-41cd-a6a0-fdb09efc8891/v2.0/.well-known/openid-configuration`, `baseUrl` es: `https://login.microsoftonline.com/53279d7a-438f-41cd-a6a0-fdb09efc8891`

### Descripción general de los archivos de configuración {#overview-of-the-configuration-files}

A continuación, encontrará una lista de los archivos que se deben configurar:

1. **Conexión de OIDC**: esto lo usará `OidcAuthenticationHandler` para autenticar a los usuarios, u otros componentes para [autorizar el acceso a los recursos protegidos por el IdP mediante OAuth](https://github.com/apache/sling-org-apache-sling-auth-oauth-client)
1. **Controlador de autenticación OIDC**: este es el controlador de autenticación usado para autenticar a los usuarios que tienen acceso a las rutas configuradas
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
    "baseUrl":"<https://login.microsoftonline.com/tenant-id/v2.0>",
    "clientId":"client-id-from-idp",
    "clientSecret":"xxxxxx"
   }
   ```

En algunos entornos, es posible que el proveedor de identidad (IdP) no exponga un extremo `.well-known` válido.
Cuando esto sucede, los puntos de conexión necesarios se pueden definir manualmente especificando las siguientes propiedades en el archivo de configuración.
En este modo de configuración, no se debe establecer la propiedad `baseUrl`.

```
"authorizationEndpoint": "https://idp-url/oauth2/v1/authorize",
"tokenEndpoint": "https://idp-url/oauth2/v1/token",
"jwkSetURL":"https://idp-url/oauth2/v1/keys",
"issuer": "https://idp-url"
```

1. Configure sus propiedades como se indica a continuación:
   * El usuario puede definir el **&quot;name&quot;**
   * `baseUrl`, `clientid` y `clientSecret` son valores de configuración que provienen del IdP.
   * Los ámbitos deben contener al menos el valor `openid`.

### Configuración del controlador de autenticación OIDC {#configure-oidc-authentication-handler}

Ahora, configure el controlador de autenticación OIDC. Se pueden configurar varias conexiones de OIDC. Cada una debe tener un nombre diferente. Si comparten el mismo [proveedor de identidad externa de OAK](https://jackrabbit.apache.org/oak/docs/security/authentication/identitymanagement.html), pueden compartir usuarios.

1. Cree el archivo de configuración. Para este ejemplo, utilizaremos `org.apache.sling.auth.oauth_client.impl.OidcAuthenticationHandler~azure.cfg.json`. El sufijo `azure` debe ser un identificador único. Consulte un ejemplo del archivo de configuración a continuación:

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
   * `callbackUri`: la ruta que se va a proteger, agregando el sufijo: `/j_security_check`. Ese mismo callbackUri también debe configurarse en el IdP remoto como URL de redireccionamiento.
   * `defaultConnectionName`: configure con el mismo nombre definido para la conexión de OIDC en el paso anterior+
   * `pkceEnabled`: `true` clave de revisión para intercambio de código (PKCE) en el flujo del código de autorización
   * `idp`: el nombre del [proveedor de identidad externo de OAK](https://jackrabbit.apache.org/oak/docs/security/authentication/identitymanagement.html). Tenga en cuenta que diferentes IDP de OAK no pueden compartir usuarios o grupos

### Configuración de SlingUserInfoProcessor {#configure-slinguserinfoprocessor}

1. Cree el archivo de configuración. Para este ejemplo, utilizaremos `org.apache.sling.auth.oauth_client.impl.SlingUserInfoProcessor~azure.cfg.json`. El sufijo `azure` debe ser un identificador único. Consulte un ejemplo del archivo de configuración a continuación:

   ```
   {
      "groupsInIdToken":true,
      "groupsClaimName": "groups",
      "connection":"azure",
      "storeAccessToken": false,
      "storeRefreshToken": false,
      "idpNameInPrincipals": true
   }
   ```

1. A continuación, configure sus propiedades como se indica a continuación:
   * `groupsInIdToken`: Se establece en true si los grupos se envían con el token de ID. Si el valor es false o no se especifica, los grupos se leen desde el punto final UserInfo.
   * `groupsClaimName`: el nombre de la reclamación contiene los grupos que se van a sincronizar en AEM.
   * `connection`: configure con el mismo nombre definido para la conexión de OIDC en el paso anterior
   * `storeAccessToken`: true si el token de acceso debe almacenarse en el repositorio. De forma predeterminada, este valor es false. Configúrelo como true solo si AEM necesita acceder a recursos en nombre del usuario almacenados en servidores externos protegidos por el mismo IdP.
   * `storeRefreshToken`: true si el token de actualización debe almacenarse en el repositorio. De forma predeterminada, este valor es false. Configúrelo como true solo si AEM necesita acceder a recursos en nombre del usuario almacenado en servidores externos protegidos por el mismo IdP y necesita actualizar el token desde el IdP.
   * `idpNameInPrincipals`: cuando se establece en true, el nombre del IdP se agrega como sufijo a las entidades de seguridad de usuario y grupo separadas por un &#39;;&#39;. Por ejemplo, si el nombre de IdP es `azure-idp` y el nombre de usuario es `john.doe`, la entidad de seguridad almacenada en Oak será `john.doe;azure-idp`. Esto resulta útil cuando se configuran varios IdPs en Oak para evitar conflictos entre usuarios o grupos con el mismo nombre procedentes de ID diferentes. Esto también se puede configurar para evitar conflictos con usuarios o grupos creados por otros controladores de autenticación como Saml.
Observe que el token de acceso y el token de actualización se almacenan cifrados con la clave maestra de AEM.


### Configuración del controlador de sincronización {#configure-the-synchronization-handler}

Debe haber al menos un controlador de sincronización configurado para sincronizar los usuarios autenticados en Oak. Para obtener más detalles, consulte [esta](https://jackrabbit.apache.org/oak/docs/security/authentication/external/defaultusersync.html) página.

Cree un archivo con el nombre `org.apache.jackrabbit.oak.spi.security.authentication.external.impl.DefaultSyncHandler~azure.cfg.json`. El sufijo **azure** debe ser un identificador único. Para obtener más información sobre cómo configurar sus propiedades, consulte la [Documentación de sincronización de grupos y usuarios de Oak](https://jackrabbit.apache.org/oak/docs/security/authentication/external/defaultusersync.html). A continuación, encontrará un ejemplo de configuración:

```
{
  "user.expirationTime":"1h",
  "user.membershipExpTime":"1h",
  "group.expirationTime": "1d"
  "user.propertyMapping":[
    "profile/givenName=profile/given_name",
    "profile/familyName=profile/family_name",
    "rep:fullname=profile/name",
    "profile/email=profile/email",
    "access_token=access_token",
    "refresh_token=refresh_token"
  ],
  "user.pathPrefix":"azure",
  "handler.name":"azure"
}
```

Durante el desarrollo, los tiempos de caducidad se pueden reducir a un valor menor (por ejemplo: 1) para acelerar las pruebas de sincronización de usuarios y grupos en Oak.
A continuación, se muestran algunos de los atributos más relevantes que se van a configurar en DefaultSyncHandler. Tenga en cuenta que la pertenencia a grupos dinámicos siempre debe estar habilitada en Cloud Services.

| Nombre de la propiedad | Notas | Valor sugerido |
|---|---|---|
| `user.expirationTime` | Duración hasta que caduque un usuario sincronizado. Los usuarios se sincronizan solo después de la hora de caducidad. | 1 h |
| `user.membershipExpTime` | Duración hasta que caduque una suscripción de un usuario sincronizado. Las suscripciones de los usuarios solo se sincronizan después de la hora de caducidad. | 1 h |
| `user.dynamicMembership` | Se recomienda habilitar la suscripción a grupos dinámicos | true |
| `user.enforceDynamicMembership` | Se recomienda habilitar la aplicación de la suscripción a grupos dinámicos | true |
| `group.dynamicGroups` | Se recomienda habilitar los grupos dinámicos | true |
| user.propertyMapping | La implementación proporcionada de `UserInfoProcessor` sincroniza solo algunas propiedades. Se puede modificar y personalizar. | <code>&quot;profile/givenName=profile/given_name&quot;,</code><br><code>&quot;profile/familyName=profile/family_name&quot;,</code><br><code>&quot;rep:fullname=profile/name&quot;,</code><br><code>&quot;profile/email=profile/email&quot;,</code><br><code>&quot;access_token=access_token&quot;,</code><br><code>&quot;refresh_token=refresh_token&quot;</code> |
| `user.membershipNestingDepth` | Devuelve la profundidad máxima de anidamiento de grupos cuando se sincronizan las relaciones de suscripción. Un valor de 0 deshabilita de forma efectiva la búsqueda de miembros del grupo. El valor 1 solo añade los grupos directos de un usuario. Este valor no tiene ningún efecto cuando se sincronizan grupos individuales, únicamente cuando se sincroniza una ascendencia de suscripción de usuarios. | 1 |

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

### Opcional: implementar un UserInfoProcessor personalizado {#implement-a-custom-userinfoprocessor}

El usuario se autentica mediante un token de ID y se recuperan atributos adicionales en el punto final `userInfo` definido para el IdP. Si se deben realizar operaciones no estándar adicionales, la implementación predeterminada de Sling es una implementación personalizada de [UserInfoProcessor](https://github.com/apache/sling-org-apache-sling-auth-oauth-client/blob/master/src/main/java/org/apache/sling/auth/oauth_client/impl/SlingUserInfoProcessorImpl.java).

### Configurar ACL para grupos externos {#configure-acl-for-external-groups}

Cuando los usuarios se autentican a través de OIDC, las pertenencias a sus grupos generalmente se sincronizan desde el proveedor de identidad externo.
Estos grupos externos se crean dinámicamente en el repositorio de AEM, pero no se asocian automáticamente con ninguna entrada de control de acceso.
Para garantizar que los usuarios tengan los permisos adecuados, las listas de control de acceso (ACL) deben definirse explícitamente para estos grupos.

Hay dos enfoques principales disponibles.

### Opción 1 - Grupos locales

El grupo externo se puede agregar como miembro de un grupo local que ya tiene las ACL requeridas.
* El grupo externo debe existir en el repositorio, lo que ocurre automáticamente cuando un usuario que pertenece a ese grupo inicia sesión por primera vez.
* Esta opción se prefiere generalmente cuando se utilizan Grupos de usuarios cerrados (CUG), ya que el grupo local existe tanto en entornos de creación como de publicación.

### Opción 2: Direccionar ACL en grupos externos mediante RepoInit

Las ACL se pueden aplicar directamente a grupos externos mediante scripts de RepoInit.
* Este método es más eficaz y se prefiere cuando no se utilizan CUG.
* El siguiente ejemplo muestra una configuración de RepoInit que asigna permisos de lectura a un grupo externo. La opción `ignoreMissingPrincipal` permite la creación de la ACL incluso si el grupo aún no existe en el repositorio:

  ```
  {
    "scripts":[
      "set ACL for \"my-group;my-idp\"  (ACLOptions=ignoreMissingPrincipal)\r\n  allow jcr:read on /content/wknd/us/en/magazine\r\nend"
    ]
  }    
  ```

>[!NOTE]
>La interfaz de usuario de permisos de AEM se puede utilizar para inspeccionar las ACL asignadas a principales de grupo

## Ejemplo: configurar la autenticación de OIDC con Azure Active Directory

### Configurar una nueva aplicación en Azure Active Directory {#configure-a-new-application-in-azure-ad}

1. Cree una nueva aplicación en Azure Active Directory siguiendo la [documentación de Azure Active Directory](https://learn.microsoft.com/en-us/power-pages/security/authentication/openid-settings#create-an-app-registration-in-azure).  Consulte a continuación el aspecto que debería tener la pantalla que detalla la descripción general de la aplicación:

   ![Información general de la aplicación](/help/security/assets/odic-application-overview.png)

1. Si se requieren grupos o funciones de aplicación, siga la [documentación](https://learn.microsoft.com/en-us/entra/external-id/customers/how-to-use-app-roles-customers) para habilitarlos en la aplicación y enviarlos en el token de ID. A continuación, se muestra un ejemplo de grupos configurados:

![ID de token de reclamación de OIDC](/help/security/assets/oidc-claim-id-token.png)

1. Siga los pasos documentados anteriormente para crear los archivos de configuración necesarios. A continuación, se muestra un ejemplo específico de Azure AD donde:
   * Definimos el nombre de Conexión oidc, Controlador de autenticación y DefaultSyncHandler como: `azure`
   * La URL predeterminada es: `www.mywebsite.com`
   * Protegemos la ruta de acceso `/content/wknd/us/en/adventures`, a la que solo tienen acceso los usuarios autenticados miembros del grupo `adventures`
   * Tennant es: `tennat-id`,
   * ID de cliente es: `client-id`,
   * Secreto es: `secret`,
   * Los grupos se envían en el token de ID en una reclamación llamada: `groups`

### org.apache.sling.auth.oauth_client.impl.OidcConnectionImpl~azure.cfg.json

```
{
  "name":"azure",
  "scopes":[
    openid", "User.Read", "profile", "email"
  ],
  "baseUrl":"https://login.microsoftonline.com/tenant-id/v2.0",
  "clientId":"client-id",
  "clientSecret":"secret"
}
```

### org.apache.sling.auth.oauth_client.impl.OidcAuthenticationHandler~azure.cfg.json

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

### org.apache.jackrabbit.oak.spi.security.authentication.external.impl.ExternalLoginModuleFactory~azure.cfg.json

```
{
  "sync.handlerName":"azure",
  "idp.name":"azure"
}
```

### org.apache.jackrabbit.oak.spi.security.authentication.external.impl.DefaultSyncHandler~azure.cfg.json

```
{
  "user.expirationTime":"1h",
  "user.membershipExpTime":"1h",
  "group.expirationTime": "1d"
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

### org.apache.sling.jcr.repoinit.RepositoryInitializer~azure.cfg.json

```
{
  "scripts":[
    "set ACL for \"adventures;azure\"  (ACLOptions=ignoreMissingPrincipal)\r\n  allow jcr:read on /content/wknd/us/en/adventures\r\nend"
  ]
}
```

### org.apache.sling.auth.oauth_client.impl.SlingUserInfoProcessorImpl~azure.cfg.json

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

Para configurar un grupo para la aplicación empresarial en el portal de Microsoft Azure, debe buscar en la aplicación: **Aplicaciones empresariales** y añadir los grupos: <!-- Alexandru: this bit cound be clearer-->

![Añadir grupo OIDC](/help/security/assets/oidc-ad-additional-info.png)

Para habilitar la notificación de grupo en el token de ID, añada la notificación a la sección **Configuración del token** del portal de Microsoft Azure: <!-- Alexandru: this bit cound be clearer as well-->

![ID de token de reclamación de OIDC](/help/security/assets/oidc-claim-id-token.png)

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

## Migración del Controlador de autenticación Saml al Controlador de autenticación Oidc

Cuando AEM ya está configurado con un controlador de autenticación SAML y los usuarios están presentes en el repositorio con [sincronización de datos](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/sites/authoring/personalization/user-and-group-sync-for-publish-tier#data-synchronization) habilitada, pueden producirse conflictos entre los usuarios de SAML originales y los nuevos usuarios de OIDC.

1. Configure [OidcAuthenticationHandler](#configure-oidc-authentication-handler) y habilite `idpNameInPrincipals` en la configuración de [SlingUserInfoProcessor](#configure-slinguserinfoprocessor)
1. Configurar [ACL para grupos externos](#configure-acl-for-external-groups).
1. Después de iniciar sesión desde los usuarios, se pueden eliminar los usuarios antiguos creados por el mismo controlador de autenticación.

>[!NOTE]
>Una vez que el Controlador de autenticación SAML está deshabilitado y el Controlador de autenticación OIDC está habilitado, si la [sincronización de datos](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/sites/authoring/personalization/user-and-group-sync-for-publish-tier#data-synchronization) no está habilitada, las sesiones existentes dejarán de ser válidas. Los usuarios deberán autenticarse de nuevo, lo que resulta en la creación de nuevos nodos de usuario de OIDC en el repositorio.

