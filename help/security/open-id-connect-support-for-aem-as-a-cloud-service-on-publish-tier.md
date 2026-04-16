---
title: Compatibilidad con Open ID Connect para AEM as a Cloud Service en el nivel de publicación
description: Obtenga información sobre cómo configurar Open ID Connect (OIDC) para AEM as a Cloud Service en el nivel de publicación
feature: Security
role: Admin
exl-id: d2f30406-546c-4a2f-ba88-8046dee3e09b
source-git-commit: 70687e4f2ea0df923e44237bc20635745c46323a
workflow-type: tm+mt
source-wordcount: '2610'
ht-degree: 53%

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

1. Cree el archivo de configuración. Para este ejemplo, utilizaremos `org.apache.sling.auth.oauth_client.impl.SlingUserInfoProcessorImpl~azure.cfg.json`. El sufijo `azure` debe ser un identificador único. Consulte un ejemplo del archivo de configuración a continuación:

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

El usuario se autentica mediante un token de ID y se recuperan atributos adicionales del extremo `userInfo` definido para el IdP. El `UserInfoProcessor` es responsable de transformar los datos recibidos del proveedor de identidad en credenciales y atributos que AEM puede utilizar para la sincronización de usuarios.

#### Cuándo crear un UserInfoProcessor personalizado {#when-to-create-custom-userinfoprocessor}

El valor predeterminado [SlingUserInfoProcessorImpl](https://github.com/apache/sling-org-apache-sling-auth-oauth-client/blob/master/src/main/java/org/apache/sling/auth/oauth_client/impl/SlingUserInfoProcessorImpl.java) administra las notificaciones estándar de OIDC y la sincronización de grupos. Es posible que necesite una implementación personalizada si necesita:

* Extraer y procesar notificaciones personalizadas del token de ID o la respuesta de UserInfo
* Transformar o asignar notificaciones a nombres de atributos diferentes
* Implementar la lógica personalizada para la extracción de grupos de notificaciones anidadas
* Agregue atributos de usuario adicionales que no formen parte del perfil estándar de IDCo
* Procesar tokens de acceso o tokens de actualización para casos de uso específicos
* Integración con sistemas externos para enriquecer los datos de usuario durante la autenticación

#### Explicación de la interfaz UserInfoProcessor {#understanding-userinfoprocessor-interface}

La interfaz `UserInfoProcessor` del paquete `org.apache.sling.auth.oauth_client.spi` define dos métodos:

```java
public interface UserInfoProcessor {
    /**
     * Process the UserInfo and token response to create OIDC credentials
     *
     * @param userInfo - JSON response from the UserInfo endpoint (may be null)
     * @param tokenResponse - JSON response from the token endpoint
     * @param oidcSubject - The subject claim from the ID token
     * @param idp - The configured IDP name
     * @return OidcAuthCredentials containing user attributes and group memberships
     */
    @NotNull OidcAuthCredentials process(
        @Nullable String userInfo,
        @NotNull String tokenResponse,
        @NotNull String oidcSubject,
        @NotNull String idp
    );

    /**
     * @return The name of the OIDC connection this processor is associated with
     */
    @NotNull String connection();
}
```

El objeto `OidcAuthCredentials` devuelto le permite:
* Establecer atributos de usuario mediante `setAttribute(key, value)`: se sincronizan en función de las asignaciones de propiedades de `DefaultSyncHandler`
* Agregar pertenencias de grupo mediante `addGroup(groupName)`: estos grupos se crean o sincronizan en AEM

#### Ejemplo: Implementación personalizada de UserInfoProcessor {#custom-userinfoprocessor-implementation}

A continuación se muestra un ejemplo completo que muestra cómo implementar un(a) `UserInfoProcessor` personalizado:

```java
package com.mycompany.aem.auth;

import java.nio.charset.StandardCharsets;
import java.util.Base64;

import org.apache.sling.auth.oauth_client.spi.OidcAuthCredentials;
import org.apache.sling.auth.oauth_client.spi.UserInfoProcessor;
import org.jetbrains.annotations.NotNull;
import org.jetbrains.annotations.Nullable;
import org.osgi.service.component.annotations.Activate;
import org.osgi.service.component.annotations.Component;
import org.osgi.service.metatype.annotations.AttributeDefinition;
import org.osgi.service.metatype.annotations.Designate;
import org.osgi.service.metatype.annotations.ObjectClassDefinition;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

import com.google.gson.JsonObject;
import com.google.gson.JsonParser;

/**
 * Custom UserInfoProcessor that extracts additional claims from the ID token
 * and adds custom user attributes and group memberships.
 */
@Component(service = UserInfoProcessor.class, property = {"service.ranking:Integer=50"})
@Designate(ocd = CustomUserInfoProcessor.Config.class, factory = true)
public class CustomUserInfoProcessor implements UserInfoProcessor {

    private static final Logger logger = LoggerFactory.getLogger(CustomUserInfoProcessor.class);

    @ObjectClassDefinition(name = "Custom UserInfo Processor")
    @interface Config {
        @AttributeDefinition(name = "Connection Name", description = "OIDC Connection Name")
        String connection();
    }

    private final String connection;

    @Activate
    public CustomUserInfoProcessor(Config config) {
        this.connection = config.connection();
        logger.info("CustomUserInfoProcessor activated for connection: {}", connection);
    }

    @Override
    public @NotNull OidcAuthCredentials process(
            @Nullable String userInfo,
            @NotNull String tokenResponse,
            @NotNull String oidcSubject,
            @NotNull String idp) {

        // Parse the token response to extract tokens
        JsonObject tokenJson = JsonParser.parseString(tokenResponse).getAsJsonObject();
        String accessToken = tokenJson.has("access_token") ?
            tokenJson.get("access_token").getAsString() : null;
        String idToken = tokenJson.has("id_token") ?
            tokenJson.get("id_token").getAsString() : null;

        logger.debug("Processing authentication for subject: {}", oidcSubject);

        // Decode and extract claims from ID Token
        JsonObject claims = null;
        if (idToken != null) {
            claims = decodeJwtPayload(idToken);
            logger.debug("Extracted claims from ID token: {}", claims);
        }

        // Create credentials object
        OidcAuthCredentials credentials = new OidcAuthCredentials(oidcSubject, idp);
        credentials.setAttribute(".token", "");

        // Extract standard profile attributes
        if (claims != null) {
            // Standard OIDC claims
            setAttributeIfPresent(credentials, claims, "given_name", "profile/given_name");
            setAttributeIfPresent(credentials, claims, "family_name", "profile/family_name");
            setAttributeIfPresent(credentials, claims, "email", "profile/email");
            setAttributeIfPresent(credentials, claims, "name", "profile/name");

            // Custom claims from your IdP
            setAttributeIfPresent(credentials, claims, "department", "profile/department");
            setAttributeIfPresent(credentials, claims, "employee_id", "profile/employeeId");
            setAttributeIfPresent(credentials, claims, "job_title", "profile/jobTitle");
        }

        // Extract group memberships from claims
        if (claims != null && claims.has("groups")) {
            if (claims.get("groups").isJsonArray()) {
                claims.get("groups").getAsJsonArray().forEach(group -> {
                    credentials.addGroup(group.getAsString());
                });
            }
        }

        // Optionally store tokens if needed for later API calls
        // Note: Only store tokens if your application needs to call external APIs
        // on behalf of the user. Tokens are encrypted before storage.
        if (accessToken != null) {
            credentials.setAttribute("access_token", accessToken);
        }

        return credentials;
    }

    @Override
    public @NotNull String connection() {
        return connection;
    }

    /**
     * Helper method to set attribute if present in claims
     */
    private void setAttributeIfPresent(OidcAuthCredentials credentials,
                                      JsonObject claims,
                                      String claimName,
                                      String attributeName) {
        if (claims.has(claimName) && !claims.get(claimName).isJsonNull()) {
            String value = claims.get(claimName).getAsString();
            if (value != null && !value.isEmpty()) {
                credentials.setAttribute(attributeName, value);
            }
        }
    }

    /**
     * Decode JWT payload (middle part) to extract claims
     */
    private JsonObject decodeJwtPayload(String jwt) {
        try {
            String[] parts = jwt.split("\\.");
            if (parts.length != 3) {
                logger.warn("Invalid JWT format");
                return null;
            }

            // Decode the payload (second part)
            String payload = parts[1];
            // Add padding if needed
            payload = payload + "====".substring(0, (4 - payload.length() % 4) % 4);
            // Replace URL-safe characters
            payload = payload.replace('-', '+').replace('_', '/');

            byte[] decoded = Base64.getDecoder().decode(payload);
            String json = new String(decoded, StandardCharsets.UTF_8);
            return JsonParser.parseString(json).getAsJsonObject();
        } catch (Exception e) {
            logger.error("Failed to decode JWT payload", e);
            return null;
        }
    }
}
```

#### Configuración {#custom-userinfoprocessor-configuration}

Cree un archivo de configuración para su `UserInfoProcessor` personalizado en su proyecto de AEM en `ui.config/src/main/content/jcr_root/apps/myapp/osgiconfig/config.publish/`:

**com.mycompany.aem.auth.CustomUserInfoProcessor~azure.cfg.json**

```json
{
  "connection": "azure"
}
```

La configuración debe coincidir con el nombre de conexión definido en la configuración de `OidcConnectionImpl`. La propiedad `service.ranking` de la anotación `@Component` (establecida en `50` en el ejemplo) determina la prioridad si hay varios procesadores registrados para la misma conexión. Las clasificaciones más altas tienen prioridad sobre el valor predeterminado `SlingUserInfoProcessorImpl` (que tiene una clasificación de `0`).

#### Dependencias {#custom-userinfoprocessor-dependencies}

Agregue las siguientes dependencias a `pom.xml` de su módulo principal:

```xml
<dependency>
    <groupId>org.apache.sling</groupId>
    <artifactId>org.apache.sling.auth.oauth-client</artifactId>
    <version>0.1.7</version>
    <scope>provided</scope>
</dependency>
<dependency>
    <groupId>com.google.code.gson</groupId>
    <artifactId>gson</artifactId>
    <version>2.8.9</version>
    <scope>provided</scope>
</dependency>
```

#### Sincronizar atributos con DefaultSyncHandler {#synchronizing-custom-attributes}

Para asegurarse de que los atributos personalizados se mantengan en los nodos de usuario en el JCR, actualice la configuración de `DefaultSyncHandler` para incluir las asignaciones de propiedades:

**org.apache.jackrabbit.oak.spi.security.authentication.external.impl.DefaultSyncHandler~azure.cfg.json**

```json
{
  "user.expirationTime": "1h",
  "user.membershipExpTime": "1h",
  "user.propertyMapping": [
    "profile/givenName=profile/given_name",
    "profile/familyName=profile/family_name",
    "rep:fullname=profile/name",
    "profile/email=profile/email",
    "profile/department=profile/department",
    "profile/employeeId=profile/employeeId",
    "profile/jobTitle=profile/jobTitle",
    "access_token=access_token"
  ],
  "user.pathPrefix": "azure",
  "handler.name": "azure"
}
```

El formato es `jcrPropertyPath=credentialAttributeName`. En el lado izquierdo está la propiedad almacenada en el nodo de usuario bajo `/home/users`, y en el lado derecho coincide el nombre de atributo establecido en `UserInfoProcessor` mediante `credentials.setAttribute()`.

#### Implementación y pruebas {#custom-userinfoprocessor-deployment}

1. **Genere e implemente** su proyecto de AEM que contiene el(la) `UserInfoProcessor` personalizado(s):

   ```bash
   mvn clean install -PautoInstallPackage
   ```

2. **Verificar registro** en la consola OSGi en `/system/console/components`:
   * Busque el nombre de clase de procesador personalizado
   * Compruebe que el componente está activo y que la configuración de conexión es correcta

3. **Probar flujo de autenticación**:
   * Acceder a una ruta protegida configurada en su `OidcAuthenticationHandler`
   * Después de la autenticación correcta, compruebe el nodo de usuario en CRXDE en `/home/users/<prefix>/<username>`
   * Compruebe que los atributos personalizados están sincronizados
   * Comprobar pertenencias de grupo en `/home/groups`

4. **Habilitar el registro de depuración** para solucionar problemas:

   ```
   Logger: com.mycompany.aem.auth
   Log Level: DEBUG
   ```

#### Prácticas recomendadas {#custom-userinfoprocessor-best-practices}

* **Minimizar el almacenamiento de tokens**: almacene solo tokens de acceso o tokens de actualización si la aplicación necesita realizar llamadas de API a servicios externos en nombre de los usuarios. Los tokens están cifrados, pero siguen añadiendo sobrecarga.
* **Validar notificaciones**: Compruebe siempre si las notificaciones existen y no son nulas antes de procesarlas.
* **Tratamiento de errores**: Registre los errores correctamente, pero asegúrese de que el flujo de autenticación se pueda completar aunque falten notificaciones opcionales.
* **Rendimiento**: Mantenga la lógica de procesamiento ligera a medida que se ejecuta en cada autenticación.
* **Seguridad**: Nunca registre información confidencial como tokens completos o contraseñas de usuario. Use `substring()` si registra tokens para la depuración.
* **Pruebas**: realice pruebas con varios perfiles de usuario de su IdP para asegurarse de que todas las variaciones de notificaciones se gestionan correctamente.

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

## Redirección personalizada después de la autenticación {#custom-redirect-after-authentication}

De forma predeterminada, tras la autenticación correcta de OIDC, se redirige a los usuarios a la dirección URL solicitada originalmente. Sin embargo, puede personalizar este comportamiento mediante el parámetro de consulta `redirect`.

### Uso del parámetro de redirección

Al iniciar la autenticación, puede especificar una dirección URL de redireccionamiento personalizada agregando el parámetro `redirect` a la solicitud de autenticación:

```
/content/wknd/us/en/adventures?redirect=/content/wknd/us/en/welcome
```

En este ejemplo, después de la autenticación correcta, se redirigirá al usuario a `/content/wknd/us/en/welcome` en lugar de a la página solicitada originalmente.

### Restricciones de seguridad

Por motivos de seguridad, el parámetro `redirect` tiene las restricciones siguientes:

* **Debe ser una ruta relativa**: La dirección URL de redireccionamiento debe comenzar con `/` (por ejemplo, `/content/mysite/dashboard`)
* **No hay redirecciones entre sitios**: no se permiten direcciones URL absolutas (por ejemplo, `https://external-site.com`)
* **Sin direcciones URL relativas al protocolo**: las direcciones URL que comienzan por `//` se rechazan para evitar redirecciones relativas al protocolo

Si se proporciona una dirección URL de redireccionamiento no válida, la autenticación fallará y producirá un error.

### Casos de uso de ejemplo

1. **Página de bienvenida después del inicio de sesión**: redirija a los usuarios a una página de bienvenida personalizada después de su primer inicio de sesión

   ```
   /content/mysite/secure-area?redirect=/content/mysite/welcome
   ```

2. **Redireccionamiento del panel**: Dirija a los usuarios a un panel específico después de la autenticación

   ```
   /content/mysite/login?redirect=/content/mysite/user/dashboard
   ```

3. **Vinculación profunda**: permita que los usuarios se autentiquen y luego accedan a un recurso específico

   ```
   /content/mysite/protected?redirect=/content/mysite/protected/specific-document
   ```

## Migración del Controlador de autenticación Saml al Controlador de autenticación Oidc

Cuando AEM ya está configurado con un controlador de autenticación SAML y los usuarios están presentes en el repositorio con [sincronización de datos](https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/sites/authoring/personalization/user-and-group-sync-for-publish-tier#data-synchronization) habilitada, pueden producirse conflictos entre los usuarios de SAML originales y los nuevos usuarios de OIDC.

1. Configure [OidcAuthenticationHandler](#configure-oidc-authentication-handler) y habilite `idpNameInPrincipals` en la configuración de [SlingUserInfoProcessor](#configure-slinguserinfoprocessor)
1. Configurar [ACL para grupos externos](#configure-acl-for-external-groups).
1. Después de iniciar sesión desde los usuarios, se pueden eliminar los usuarios antiguos creados por el mismo controlador de autenticación.

>[!NOTE]
>Una vez que el Controlador de autenticación SAML está deshabilitado y el Controlador de autenticación OIDC está habilitado, si la [sincronización de datos](https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/sites/authoring/personalization/user-and-group-sync-for-publish-tier#data-synchronization) no está habilitada, las sesiones existentes dejarán de ser válidas. Los usuarios deberán autenticarse de nuevo, lo que resulta en la creación de nuevos nodos de usuario de OIDC en el repositorio.

