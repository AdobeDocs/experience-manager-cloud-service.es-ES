---
title: Migración a la identidad externa y a la pertenencia a grupos dinámicos
description: Guía técnica para migrar usuarios y grupos locales a un modelo de identidad externo con pertenencia a grupo dinámico en AEM as a Cloud Service
solution: Experience Manager Sites
feature: Security
role: Developer, Admin
source-git-commit: 1f8bd9eea249e0b2242f3fbe1490b3d51052f546
workflow-type: tm+mt
source-wordcount: '2232'
ht-degree: 1%

---

# Migración a la identidad externa y a la pertenencia a grupos dinámicos {#migrating-to-external-identity}

## Información general {#overview}

Cuando la sincronización de datos [Data Synchronization](/help/sites-cloud/authoring/personalization/user-and-group-sync-for-publish-tier.md#data-synchronization) está habilitada en AEM as a Cloud Service, se puede configurar el controlador de autenticación SAML para que migre automáticamente a las identidades externas con pertenencia a grupo dinámico cuando administre la creación de usuarios y grupos. Si el proyecto utiliza código personalizado para crear usuarios o grupos, debe actualizarlo para crear usuarios y grupos externos, en contraposición a los usuarios y grupos locales.

### Por qué se requieren usuarios y grupos externos {#why-external-required}

La migración de usuarios y grupos locales a identidades externas con pertenencia a grupos dinámicos es esencial por varios motivos críticos:

**Optimización de rendimiento:**

* **Escrituras reducidas en el repositorio**: la pertenencia a grupos locales tradicionales requiere la escritura de relaciones de pertenencia al repositorio en una sola propiedad de varios valores del nodo de grupo. Con la pertenencia a grupos dinámicos, los usuarios tienen una sola propiedad `rep:externalPrincipalNames` que contiene todas las entidades de seguridad de grupo, lo que elimina la necesidad de sincronizar el nodo de grupo
* **Sincronización más rápida**: Al sincronizar usuarios entre nodos de nivel de publicación, los usuarios externos con pertenencia a grupos dinámicos requieren una transferencia de datos significativamente menor y menos operaciones de escritura en comparación con los usuarios locales con pertenencias a grupos tradicionales
* **Escalabilidad**: Los sistemas con un gran número de usuarios y grupos se benefician considerablemente de la reducción de la sobrecarga del repositorio. La pertenencia a grupos dinámicos se escala de forma eficaz incluso en grupos muy grandes.

Este documento proporciona orientación técnica para lo siguiente:

* Explicación del modelo de identidad externa
* Modificación del código personalizado para crear usuarios y grupos externos
* Migración de usuarios y grupos locales existentes al modelo de identidad externo

## Explicación de la identidad externa {#understanding-external-identity}

### Usuarios externos {#external-users}

Los usuarios externos se identifican mediante la propiedad `rep:externalId`, que vincula al usuario con un proveedor de identidad externo. El formato es:

```
userId;idpName
```

Por ejemplo: `john.doe;saml-idp`.

>[!NOTE]
>
> `idpName` hace referencia al nombre del proveedor de identidad de Oak (Idp) tal como se define en la configuración del controlador de autenticación. Para integraciones de SAML, este es el valor establecido para el atributo `idpIdentifier` en el Controlador de autenticación SAML.

**Propiedades de clave:**

* `rep:externalId`: propiedad requerida que marca a un usuario como externo (por ejemplo, `john.doe;saml-idp`)
* `rep:externalPrincipalNames`: propiedad de varios valores que contiene entidades de seguridad de grupo externas para la pertenencia dinámica
* `rep:lastSynced`: marca de tiempo de la última sincronización
* `rep:lastDynamicSync`: marca de tiempo de la última sincronización de pertenencia a grupo dinámico

### Grupos externos {#external-groups}

Los grupos externos también se identifican mediante la propiedad `rep:externalId` y utilizan un formato de nombre principal:

```
groupId;idpName
```

Por ejemplo: `content-authors;saml-idp`

### Pertenencia a grupo dinámico {#dynamic-group-membership}

En lugar de las relaciones directas de usuario a grupo almacenadas en el repositorio, la pertenencia a grupos dinámicos utiliza la propiedad `rep:externalPrincipalNames` en el nodo de usuario. Cuando un usuario tiene un nombre principal externo que coincide con el ID de un grupo externo, pasa a ser miembro de ese grupo automáticamente. Para obtener más información, consulte la [Documentación de Apache Oak](https://jackrabbit.apache.org/oak/docs/security/authentication/external/dynamic.html).

**Ventajas:**

* Escrituras reducidas en el repositorio (no se modifican nodos de pertenencia a grupos cuando se agregan/eliminan usuarios de los grupos)
* Sincronización más rápida entre los nodos del nivel de publicación
* Administración escalable de miembros de grupo
* Compatible con los requisitos de sincronización de datos

## Configuración de usuario de servicio {#service-user-configuration}

Todas las operaciones que creen o modifiquen usuarios y grupos externos deben realizarse con un **usuario de servicio** que esté configurado correctamente para omitir la protección predeterminada en las propiedades `rep:externalId` y `rep:externalPrincipalNames`.

### Por qué se requiere un usuario de servicio {#why-is-a-service-user-required}

De forma predeterminada, la seguridad de Oak impide que las sesiones regulares modifiquen propiedades protegidas como:

* `rep:externalId` - Marca usuarios/grupos como externos
* `rep:externalPrincipalNames` - Almacena principales de pertenencia a grupos dinámicos

Solo un usuario de servicio configurado correctamente puede modificar estas propiedades.

### Configuración y asignación de usuarios de servicio {#service-user-configuration-mapping}

La configuración de un usuario de servicio para administrar identidades externas requiere tres configuraciones coordinadas:

1. Crear el usuario del servicio mediante `repoinit`
2. Configurar la protección de `ExternalPrincipal`
3. Asigne el usuario del servicio al paquete de aplicaciones.

Consulte a continuación una descripción detallada de estos pasos.

#### Paso 1: Crear el usuario de servicio mediante Repoinit {#create-the-serviice-user-via-repoinit}

Este paso detalla la creación del usuario del servicio con los permisos necesarios mediante un script `repoinit`.

**Archivo de configuración:** `org.apache.sling.jcr.repoinit.RepositoryInitializer~group-provisioner.cfg.json`

**Ubicación ejemplar:** `ui.config/src/main/content/jcr_root/apps/yourproject/osgiconfig/config.publish/`

```json
{
  "scripts": [
    "create service user group-provisioner with path system/yourproject",
    "set ACL for group-provisioner\n  allow jcr:read,jcr:readAccessControl,jcr:modifyAccessControl,rep:userManagement,rep:write on /home/users\n  allow jcr:read,jcr:readAccessControl,jcr:modifyAccessControl,rep:userManagement,rep:write on /home/groups\nend"
  ]
}
```

**Información general sobre permisos**

* `jcr:read`: leer usuarios y grupos
* `jcr:readAccessControl`: Leer ACL
* `jcr:modifyAccessControl`: modificar ACL (necesarios para establecer propiedades)
* `rep:userManagement`: crear y administrar usuarios/grupos
* `rep:write`: escribir propiedades, incluidas `rep:externalId` y `rep:externalPrincipalNames`

>[!NOTE]
>
>El usuario del servicio se crea en `/home/users/system/yourproject` para mantenerlo organizado con otros usuarios del sistema.

#### Paso 2: Configurar la protección de entidad principal externa {#configure-externalprincipal-protection}

A continuación se muestra un ejemplo de configuración para incluir al usuario del servicio en la lista de usuarios admitidos de modo que pueda evitar la protección aplicada a las propiedades de identidad externas.

**Nombre del archivo de configuración:** `org.apache.jackrabbit.oak.spi.security.authentication.external.impl.principal.ExternalPrincipalConfiguration.cfg.json`

**Ubicación de ejemplo:** `ui.config/src/main/content/jcr_root/apps/yourproject/osgiconfig/config.publish/`

```json
{
  "protectExternalIdentities": "Warn",
  "systemPrincipalNames": [
    "group-provisioner",
    "saml-migration-service"
  ]
}
```

**Propiedades de configuración:**

* `protectExternalIdentities`: controla el nivel de protección de las propiedades de identidad externas:
   * `"Strict"`: solo las entidades de seguridad del sistema de la lista blanca pueden modificar las propiedades externas. Este es el nivel recomendado para la producción.
   * `"Warn"`: registra advertencias pero permite modificaciones. Útil para desarrollo y pruebas.
   * `"None"`: sin protección. No se recomienda.
* `systemPrincipalNames`: lista de nombres de usuario de servicio con permiso para modificar `rep:externalId` y `rep:externalPrincipalNames`. Incluya a todos los usuarios del servicio que necesiten administrar identidades externas (por ejemplo, `group-provisioner`, `saml-migration-service`).

>[!IMPORTANT]
>
>Los nombres de usuario de servicio de `systemPrincipalNames` deben coincidir exactamente con los ID de usuario de servicio creados en el script de repoinit.

#### Paso 3: Asignación de usuarios de servicio {#service-user-mapping}

Asigne el usuario del servicio al paquete de aplicaciones para que el código pueda utilizarlo.

**Archivo de configuración:** `org.apache.sling.serviceusermapping.impl.ServiceUserMapperImpl.amended~group-provisioner.cfg.json`

**Ubicación:** `ui.config/src/main/content/jcr_root/apps/yourproject/osgiconfig/config.publish/`

```json
{
  "user.mapping": [
    "yourproject.core:group-provisioner=[group-provisioner]"
  ]
}
```

**Formato de asignación:**

* `yourproject.core`: el nombre simbólico del paquete (encontrado en `pom.xml` `<Bundle-SymbolicName>`)
* `group-provisioner` (antes de `=`): el nombre de subservicio que utilizará en el código
* `[group-provisioner]` (después de `=`): el identificador de usuario de servicio real creado en el repoinit

### Uso del usuario de servicio en el código {#using-the-service-user-in-code}

Al abrir una sesión para realizar operaciones de migración o de creación de usuarios/grupos, debe utilizar el usuario del servicio:

```java
import org.apache.sling.jcr.api.SlingRepository;

@Reference
private SlingRepository repository;

// Login as the service user
Session serviceSession = repository.loginService("group-provisioner", null);

try {
    UserManager userManager = ((JackrabbitSession) serviceSession).getUserManager();
    // Perform operations...
    serviceSession.save();
} finally {
    if (serviceSession != null && serviceSession.isLive()) {
        serviceSession.logout();
    }
}
```

>[!IMPORTANT]
>
>Sin la configuración de usuario de servicio adecuada, los intentos de establecer `rep:externalId` o `rep:externalPrincipalNames` fallarán con errores de permisos. Asegúrese de que el usuario del servicio esté configurado correctamente en la configuración de `ExternalPrincipal` antes de intentar la migración.

## Ejemplo de configuración completa {#complete-configuration-example}

A continuación, se muestra un ejemplo práctico completo que muestra las tres configuraciones juntas:

### Estructura de archivos {#file-structure}

```
ui.config/src/main/content/jcr_root/apps/yourproject/osgiconfig/
└── config.publish/
    ├── org.apache.sling.jcr.repoinit.RepositoryInitializer~group-provisioner.cfg.json
    ├── org.apache.jackrabbit.oak.spi.security.authentication.external.impl.principal.ExternalPrincipalConfiguration.cfg.json
    └── org.apache.sling.serviceusermapping.impl.ServiceUserMapperImpl.amended~group-provisioner.cfg.json
```

### Modificación del código personalizado {#modifying-custom-code}

#### Creación de usuarios externos {#creating-external-users}

**Antes (usuario local):**

```java
UserManager userManager = ((JackrabbitSession) session).getUserManager();
User user = userManager.createUser(userId, password);
```

**Después (usuario externo):**

```java
import org.apache.jackrabbit.oak.spi.security.authentication.external.ExternalIdentityRef;

UserManager userManager = ((JackrabbitSession) session).getUserManager();
ValueFactory valueFactory = session.getValueFactory();

// Create user with principal
Principal userPrincipal = new Principal() {
    @Override
    public String getName() {
        return userId;
    }
};

User user = userManager.createUser(userId, null, userPrincipal, null);

// Set rep:externalId
ExternalIdentityRef externalRef = new ExternalIdentityRef(userId, idpName);
String externalId = externalRef.getString(); // Format: userId;idpName
user.setProperty("rep:externalId", valueFactory.createValue(externalId));

// Set sync timestamps to far future (workaround for OAK-12079)
// Set to 10 years in the future to prevent premature cleanup of external group memberships
// See: https://issues.apache.org/jira/browse/OAK-12079
java.util.Calendar future = java.util.Calendar.getInstance();
future.add(java.util.Calendar.YEAR, 10);
user.setProperty("rep:lastSynced", valueFactory.createValue(future));
user.setProperty("rep:lastDynamicSync", valueFactory.createValue(future));

session.save();
```

#### Creación de grupos externos {#creating-external-groups}

**Antes (grupo local):**

```java
UserManager userManager = ((JackrabbitSession) session).getUserManager();
Group group = userManager.createGroup(groupId);
```

**Después (grupo externo):**

```java
import org.apache.jackrabbit.oak.spi.security.authentication.external.ExternalIdentityRef;

UserManager userManager = ((JackrabbitSession) session).getUserManager();
ValueFactory valueFactory = session.getValueFactory();

// Create group with principal
Principal groupPrincipal = new Principal() {
    @Override
    public String getName() {
        return groupId;
    }
};

Group group = userManager.createGroup(groupPrincipal);

// Set rep:externalId
ExternalIdentityRef externalRef = new ExternalIdentityRef(groupId, idpName);
String externalId = externalRef.getString(); // Format: groupId;idpName
group.setProperty("rep:externalId", valueFactory.createValue(externalId));

session.save();
```

#### Asignar pertenencia a grupo dinámico {#assigning-dynamic-membership}

**Antes (pertenencia directa):**

```java
Group group = (Group) userManager.getAuthorizable(groupId);
User user = (User) userManager.getAuthorizable(userId);
group.addMember(user);
```

**Después (pertenencia dinámica):**

```java
User user = (User) userManager.getAuthorizable(userId);
ValueFactory valueFactory = session.getValueFactory();

// Get existing external principal names
Value[] existingValues = user.getProperty("rep:externalPrincipalNames");
List<String> principalNames = new ArrayList<>();

if (existingValues != null) {
    for (Value value : existingValues) {
        principalNames.add(value.getString());
    }
}

// Add new principal name (format: groupId;idpName)
String dynamicGroupPrincipal = groupId + ";" + idpName;
if (!principalNames.contains(dynamicGroupPrincipal)) {
    principalNames.add(dynamicGroupPrincipal);
    
    // Create new Value array
    Value[] newValues = new Value[principalNames.size()];
    for (int i = 0; i < principalNames.size(); i++) {
        newValues[i] = valueFactory.createValue(principalNames.get(i));
    }
    
    // Set the property
    user.setProperty("rep:externalPrincipalNames", newValues);
    
    // Update sync timestamps to far future (workaround for OAK-12079)
    // Set to 10 years in the future to prevent premature cleanup of external group memberships
    // See: https://issues.apache.org/jira/browse/OAK-12079
    java.util.Calendar future = java.util.Calendar.getInstance();
    future.add(java.util.Calendar.YEAR, 10);
    user.setProperty("rep:lastDynamicSync", valueFactory.createValue(future));
    user.setProperty("rep:lastSynced", valueFactory.createValue(future));
}

session.save();
```

## Proceso de migración {#migration-process}

No es necesario migrar los usuarios y grupos locales existentes a la identidad externa cuando el código personalizado se actualizó antes de habilitar los servicios de sincronización de datos.

Si los usuarios y grupos locales ya se han mantenido en el repositorio y el entorno se utiliza de forma activa, le recomendamos que realice una migración de varios pasos como la siguiente para evitar interrupciones o incoherencias.

>[!IMPORTANT]
>
>Todos los pasos de migración deben ejecutarse con un usuario de servicio configurado correctamente (por ejemplo, `group-provisioner`) al que se hayan concedido permisos para omitir la protección de las propiedades `rep:externalId` y `rep:externalPrincipalNames`. Consulte [Configuración de usuario de servicio](#service-user-configuration) para obtener más información.

### Paso 1: Crear una estructura de grupo externa {#step-1-create-external-group-structure}

Para cada grupo local que debe migrarse:

1. Cree un grupo externo correspondiente con el nombre principal: `<localGroupId>;<idpName>`. Utilice una convención de nombres que ayude a vincular grupos externos con grupos locales
1. Establezca la propiedad `rep:externalId` en el grupo externo con valores: `<localGroupId>;<idpName>`
1. Agregue el grupo externo como miembro del grupo local original.

**Validación**

* Puede validar los resultados comprobando si cada grupo local tiene un grupo externo correspondiente. Además, cada grupo externo es miembro del grupo local correspondiente.

**Extremo de servlet de ejemplo:**

```java
@SlingServletPaths("/bin/migration/step1")
public class MigrationStep1Servlet extends SlingAllMethodsServlet {
    
    @Override
    protected void doPost(SlingHttpServletRequest request, 
                          SlingHttpServletResponse response) {
        String groupPath = request.getParameter("groupPath");
        String idpName = request.getParameter("idpName");

        // Check if the caller is authorized to run the servlet
        isAuthorizedCaller(request, response);

        // Get local group
        Authorizable localGroupAuth = userManager.getAuthorizableByPath(groupPath);
        Group localGroup = (Group) localGroupAuth;
        String localGroupId = localGroup.getID();
        
        // Create external group
        String externalGroupPrincipalName = localGroupId + ";" + idpName;
        // The function createExternalGroup performs the following steps:
        // 1. Creates a new external group with the given principal name (format: "<localGroupId>;<idpName>").
        // 2. Sets the 'rep:externalId' property on the group to mark it as an external group (value: "<localGroupId>;<idpName>").
        // 3. Sets the 'rep:principalName' property for the group if required.
        // 4. Assigns any other required group metadata, such as a title or description, if needed.
        // 5. Persists the new group node in the repository at the appropriate path under /home/groups.
        // 6. Returns the created Group object so it can be used for further operations, such as membership assignment.
        Group externalGroup = createExternalGroup(externalGroupPrincipalName, localGroupId, idpName);
        
        // Add external group to local group
        localGroup.addMember(externalGroup);
        
        session.save();
    }
}
```

**Uso:**

```bash
curl -X POST "http://localhost:4503/bin/migration/step1?groupPath=/home/groups/c/content-authors&idpName=saml-idp"
```

### Paso 2: Convertir usuarios y asignar pertenencia dinámica {#step-2-convert-users-and-assign-dynamic-membership}

Para cada usuario que sea miembro de un grupo local:

1. Asegúrese de que tenga `rep:externalId`establecido (convertir a usuario externo si es necesario).
1. Para cada pertenencia a grupo, agregue el principal de grupo externo correspondiente a `rep:externalPrincipalNames`
1. Actualizar marcas de tiempo de sincronización.

>[!IMPORTANT]
>
>Omita grupos del sistema como &quot;todos&quot; durante este proceso.

**Extremo de servlet de ejemplo:**

```java
@SlingServletPaths("/bin/migration/step2")
public class MigrationStep2Servlet extends SlingAllMethodsServlet {
    
    @Override
    protected void doPost(SlingHttpServletRequest request, 
                          SlingHttpServletResponse response) {
        String userId = request.getParameter("userId");
        String idpName = request.getParameter("idpName");
        
        // Check if the caller is authorized to run the servlet
        isAuthorizedCaller(request, response);

        // Login as the service user
        Session serviceSession = repository.loginService("group-provisioner", null);

        try {
            UserManager userManager = ((JackrabbitSession) serviceSession).getUserManager();
            User user = (User) userManager.getAuthorizable(userId);
            
            // Ensure user has rep:externalId
            Value[] externalIdValues = user.getProperty("rep:externalId");
            if (externalIdValues == null || externalIdValues.length == 0) {
                ExternalIdentityRef externalRef = new ExternalIdentityRef(userId, idpName);
                user.setProperty("rep:externalId", 
                            valueFactory.createValue(externalRef.getString()));
            }
            
            // Get all group memberships
            Iterator<Group> groupIterator = user.declaredMemberOf();
            List<String> principalNames = new ArrayList<>();
            
            while (groupIterator.hasNext()) {
                Group group = groupIterator.next();
                String groupId = group.getID();
                
                // Skip system groups
                if ("everyone".equals(groupId)) {
                    continue;
                }
                
                // Add dynamic group principal
                String dynamicGroupPrincipal = groupId + ";" + idpName;
                principalNames.add(dynamicGroupPrincipal);
            }
            
            // Set rep:externalPrincipalNames
            if (!principalNames.isEmpty()) {
                Value[] newValues = new Value[principalNames.size()];
                for (int i = 0; i < principalNames.size(); i++) {
                    newValues[i] = valueFactory.createValue(principalNames.get(i));
                }
                user.setProperty("rep:externalPrincipalNames", newValues);
            }
            
            // Update timestamps to far future (workaround for OAK-12079)
            // Set to 10 years in the future to prevent premature cleanup of external group memberships
            // See: https://issues.apache.org/jira/browse/OAK-12079
            java.util.Calendar future = java.util.Calendar.getInstance();
            future.add(java.util.Calendar.YEAR, 10);
            user.setProperty("rep:lastDynamicSync", valueFactory.createValue(future));
            user.setProperty("rep:lastSynced", valueFactory.createValue(future));
        
        // Perform operations...
        serviceSession.save();
    } finally {
        if (serviceSession != null && serviceSession.isLive()) {
            serviceSession.logout();
        }
}    }
}
```

**Uso:**

```bash
curl -X POST "http://localhost:4503/bin/migration/step2?userId=john.doe&idpName=saml-idp"
```

**Validación**

Puede validar esto si comprueba que todos los usuarios tienen los atributos `rep:externalId` y `rep:externalPrincipalName` con `principalName` de cada grupo externo. Los usuarios son miembros de los grupos locales *y* de los grupos externos.

### Paso 3: Eliminar suscripciones de usuario directo {#step-3-remove-direct-user-memberships}

Una vez que los usuarios hayan configurado la pertenencia a grupos dinámicos:

1. Quitar pertenencias de usuarios directos de grupos locales
1. Mantener suscripciones de grupo a grupo (incluida la pertenencia a grupos externos)

**Extremo de servlet de ejemplo:**

```java
@SlingServletPaths("/bin/migration/step3")
public class MigrationStep3Servlet extends SlingAllMethodsServlet {
    
    @Override
    protected void doPost(SlingHttpServletRequest request, 
                          SlingHttpServletResponse response) {

        // Check if the caller is authorized to run the servlet
        isAuthorizedCaller(request, response);

        String groupPath = request.getParameter("groupPath");
        
        Authorizable localGroupAuth = userManager.getAuthorizableByPath(groupPath);
        Group localGroup = (Group) localGroupAuth;
        
        // Process each member
        Iterator<Authorizable> members = localGroup.getDeclaredMembers();
        
        while (members.hasNext()) {
            Authorizable member = members.next();
            
            // Remove only user members, keep group members
            if (!member.isGroup()) {
                localGroup.removeMember(member);
            }
        }
        
        session.save();
    }
}
```

**Uso:**

```bash
curl -X POST "http://localhost:4503/bin/migration/step3?groupPath=/home/groups/c/content-authors"
```

**Validación**

* Puede validar esto comprobando que cada grupo local tenga solo el grupo externo correspondiente, u otros grupos, como miembro.


## Flujo de trabajo de migración {#migration-workflow}

### Lista de comprobación previa a la migración {#pre-migration-checklist}

* **Configurar usuario de servicio**: cree y configure el usuario de servicio (por ejemplo, `group-provisioner`) con los permisos adecuados
* **Verificar configuración de ExternalPrincipal**: Asegúrese de que el usuario del servicio está configurado para omitir la protección en `rep:externalId` y `rep:externalPrincipalNames`
* **Permisos de usuario del servicio de prueba**: compruebe que el usuario del servicio puede establecer propiedades de identidad externas en desarrollo
* Identifique todo el código personalizado que cree usuarios o grupos
* Revisar y actualizar el código personalizado para utilizar un modelo de identidad externo
* Prueba de código actualizado en el entorno de desarrollo
* Inventariar todos los usuarios y grupos locales existentes para migrar
* Prueba del proceso de migración en entornos más bajos

### Pasos de ejecución {#execution-steps}

1. **Implementar código actualizado**: Implemente cambios de código personalizado para crear usuarios/grupos externos

1. **Crear grupos externos** (para cada grupo local):

   ```bash
   curl -X POST "http://localhost:4503/bin/migration/step1?groupPath=/home/groups/g/my-group&idpName=saml-idp"
   ```

1. **Migrar usuarios** (para cada usuario):

   ```bash
   curl -X POST "http://localhost:4503/bin/migration/step2?userId=username&idpName=saml-idp"
   ```

1. **Limpieza** (para cada grupo migrado):

   ```bash
   curl -X POST "http://localhost:4503/bin/migration/step3?groupPath=/home/groups/g/my-group"
   ```

1. **Verificar**: compruebe la pertenencia a grupos de usuarios y los permisos de acceso de prueba

1. **Habilitar sincronización de datos**: Póngase en contacto con Atención al cliente para habilitar la característica

### Validación posterior a la migración {#post-migration-validation}

Compruebe la migración:

1. **Comprobar propiedades de usuario**:

   En los nodos del usuario, verificar la presencia de:

   * `rep:externalId`: el formato debe ser `userId;idpName`
   * `rep:externalPrincipalNames`: matriz de principales de grupo en formato `groupId;idpName`
   * `rep:lastSynced`: marca de tiempo establecida para un futuro lejano (aproximadamente 10 años desde la fecha de migración)
   * `rep:lastDynamicSync`: marca de tiempo establecida para un futuro lejano (aproximadamente 10 años desde la fecha de migración)

   **Nota**: Las marcas de tiempo se establecen intencionalmente en una fecha futura como solución alternativa para OAK-12079. Este es el comportamiento esperado.

1. **Comprobar propiedades del grupo**:

   En los nodos de grupo local, compruebe la presencia de:

   * Miembro de grupo externo con formato `groupId;idpName`
   * Sin miembros de usuario directo (solo después del paso 3)

1. **Probar inicio de sesión de usuario**: compruebe que los usuarios pueden iniciar sesión y que tienen los permisos correctos

1. **Probar control de acceso**: compruebe que los usuarios pueden acceder al contenido protegido por CUG/ACL

## Solución de problemas {#troubleshooting}

### Problemas comunes {#common-issues}

**Problema: errores de permisos al configurar `rep:externalId` o`rep:externalPrincipalNames`**

**Mensajes de error:**

* `javax.jcr.AccessDeniedException: Access denied`
* `OakAccess0000: Access denied`
* `Cannot set property 'rep:externalId'`

**Solución**: la sesión debe abrirse con un usuario de servicio configurado correctamente al que se le hayan concedido permisos para omitir la protección en las propiedades de identidad externas.

**Pasos para resolver:**

1. **Verificar que el usuario del servicio existe**: Asegúrese de que el usuario del servicio (por ejemplo, `group-provisioner`) se crea mediante repoinit
1. **Comprobar asignación de usuario de servicio**: compruebe que el servlet o servicio está usando `repository.loginService("group-provisioner", null)`
1. **Verificar la configuración de ExternalPrincipal**: Asegúrese de que `org.apache.jackrabbit.oak.spi.security.authentication.external.impl.principal.ExternalPrincipalConfiguration` esté configurado correctamente
1. **Comprobar permisos de usuario del servicio**: El usuario del servicio necesita permisos de `rep:write` y `rep:userManagement` en `/home/users` y `/home/groups`

Consulte [Configuración de usuario de servicio](#service-user-configuration) para obtener instrucciones completas sobre la instalación.

**Problema:`OakConstraint0072: Property 'rep:externalPrincipalNames' requires 'rep:externalId' to be present`**

**Solución**: los usuarios deben tener `rep:externalId` establecido antes de establecer `rep:externalPrincipalNames`. Asegúrese de que el paso 2 convierte primero a los usuarios en usuarios externos.

**Problema: los usuarios pierden la pertenencia a grupos después de la migración**

**Solución**: compruebe que:

* El grupo externo se creó con el formato de nombre principal correcto (`groupId;idpName`)
* Se ha agregado un grupo externo como miembro del grupo local (Paso 1)
* El usuario tiene nombres principales externos correctos en `rep:externalPrincipalNames` (paso 2)
* La limpieza del paso 3 se realizó solo después de completar los pasos 1 y 2

**Problema: las pertenencias a grupos externos se quitan inesperadamente después del inicio de sesión del usuario (OAK-12079)**

**Problema**: Debido al error de Oak [OAK-12079](https://issues.apache.org/jira/browse/OAK-12079), el mecanismo de sincronización de Oak puede limpiar prematuramente las pertenencias de grupos externos en función de las marcas de tiempo `rep:lastSynced` y `rep:lastDynamicSync`.

**Solución**: establezca las marcas de tiempo `rep:lastSynced` y `rep:lastDynamicSync` en una fecha futura lejana (dentro de 10 años) en lugar de la hora actual. Esto evita que el proceso de limpieza de sincronización elimine las pertenencias de grupos externos.

**Implementación:**

```java
// Workaround for OAK-12079
// Set to 10 years in the future to prevent premature cleanup
// See: https://issues.apache.org/jira/browse/OAK-12079
java.util.Calendar future = java.util.Calendar.getInstance();
future.add(java.util.Calendar.YEAR, 10);
user.setProperty("rep:lastSynced", valueFactory.createValue(future));
user.setProperty("rep:lastDynamicSync", valueFactory.createValue(future));
```

**Por qué funciona esto**: Al establecer las marcas de tiempo en una fecha futura, la lógica de sincronización de Oak trata a estos usuarios como &quot;sincronizados recientemente&quot; y no almacena en déclencheur el proceso de limpieza que quitaría los nombres principales externos y las pertenencias de grupo.

**Nota**: Esta es una solución temporal hasta que OAK-12079 se resuelva en una versión futura de Oak. Todos los ejemplos de código de este documento ya incluyen esta solución.

**Problema: el grupo de sistema &quot;todos&quot; causa errores**

**Solución**: omita siempre el grupo de sistemas &quot;todos&quot; durante la migración de usuarios (Paso 2). AEM administra automáticamente este grupo.

### Procedimiento de reversión {#rollback-procedure}

Si la migración encuentra problemas:

1. Detener proceso de migración
1. Restaurar a partir de copia de seguridad si se vieron afectados datos críticos
1. Revertir los cambios en el código para crear usuarios y grupos externos con pertenencia a grupo dinámico
1. Revise y corrija los problemas antes de volver a intentar la migración.

## Prácticas recomendadas {#best-practices}

* **Probar exhaustivamente**: Pruebe siempre la migración en entornos de ensayo y desarrollo antes de la producción
* **Procesamiento por lotes**: para bases de usuarios grandes, procese las migraciones por lotes para evitar problemas de tiempo de espera
* **Supervisar rendimiento**: vea el rendimiento del repositorio durante la migración
* **Mantener pista de auditoría**: registre todas las operaciones de migración para solucionar problemas
* **Permisos de usuario de servicio**: Asegúrese de que los servlets de migración utilizan usuarios de servicio apropiados con los permisos necesarios. El usuario del servicio debe estar configurado en la configuración ExternalPrincipal para evitar la protección de las propiedades `rep:externalId` y `rep:externalPrincipalNames`
* **Operaciones idempotentes**: diseñe el código de migración para que se pueda volver a ejecutar con seguridad
* **Validar en cada paso**: compruebe los resultados después de cada paso de migración antes de continuar

## Protección de servlets de migración {#securing-migration-servlets}

Los servlets de migración tienen privilegios elevados para crear y modificar usuarios y grupos. Es fundamental restringir el acceso a estos extremos para evitar el acceso no autorizado.

### Método recomendado: autenticación de cuenta técnica de IMS {#recommended-approach-ims-technical-account}

El método recomendado es proteger estos servlets mediante la integración de Adobe IMS, lo que permite que solo una cuenta técnica autorizada acceda a ellos.

#### Paso 1: Crear una cuenta técnica en AEM Developer Console {#create-a-technical-account-in-aem-developer-console}

1. Vaya a [Experience Manager](https://experience.adobe.com/) y luego a **Cloud Manager**
1. Seleccione el programa y, a continuación, haga clic en el entorno donde desea crear la cuenta técnica
1. Haga clic en **Developer Console** en el menú de los tres puntos del entorno
1. En AEM Developer Console, vaya a la ficha **Integraciones**
1. Haga clic en **Crear nueva cuenta técnica**
1. Proporcione un nombre para la integración (por ejemplo, &quot;Cuenta del servicio de migración&quot;)
1. Haga clic en **Crear**
1. Tenga en cuenta los siguientes valores de la integración creada:
   * **ID de cliente**
   * **Secreto de cliente**
   * **Id. de cuenta técnica** (será el id. de usuario que tendrá acceso a los servlets - formato: `XXXXXXXXXXXXXXXXXXXXXXXX@techacct.adobe.com`)

Para obtener instrucciones detalladas, consulte [Generación de tokens de acceso para la documentación de API del lado del servidor](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md).

Código de ejemplo para comprobar si el llamador está autorizado:

```
    private boolean isAuthorizedCaller(SlingHttpServletRequest request, 
                                       SlingHttpServletResponse response) {

        Session session = request.getResourceResolver().adaptTo(Session.class);
        String callerId = session != null ? session.getUserID() : null;
               
        if (!ALLOWED_TECHNICAL_ACCOUNT.equals(callerId)) {
            LOG.warn("Unauthorized access attempt by user: '{}' (expected: '{}')", callerId,   ALLOWED_TECHNICAL_ACCOUNT);
            response.setStatus(SlingHttpServletResponse.SC_FORBIDDEN);
            return false;
        }
        
        return true;
    }
```

### Defensa en profundidad: restricciones basadas en IP {#defense-in-depth-ip-based-restrictions}

Como nivel de seguridad adicional, puede configurar reglas de CDN para restringir el acceso a los extremos de migración por dirección IP. Esto resulta útil cuando las migraciones se ejecutan desde una infraestructura conocida.

>[!NOTE]
>
>Las restricciones de IP por sí solas no son suficientes. Combine siempre con comprobaciones de autenticación como se describe anteriormente.

### Lista de comprobación de seguridad {#security-checklist}

Antes de implementar los servlets de migración en la producción:

* Creación de la integración de IMS en AEM Developer Console
* Configuración de servlets para validar el ID de cuenta técnica
* Probar el flujo de autenticación en entornos de desarrollo/ensayo
* Considere la posibilidad de aplicar restricciones adicionales basadas en IP en el nivel CDN
* Planifique la desactivación o eliminación de los servlets de migración una vez completada la migración
* Auditoría y registro de todo el acceso a los extremos de migración

>[!IMPORTANT]
>
>Una vez completada la migración, considere la posibilidad de deshabilitar o eliminar los servlets de migración de su implementación para eliminar cualquier posible riesgo de seguridad.

## Recursos adicionales {#additional-resources}

* [Sincronización de usuarios y grupos para el nivel de publicación](/help/sites-cloud/authoring/personalization/user-and-group-sync-for-publish-tier.md)
* [Controlador de autenticación SAML 2.0](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/authentication/saml-2-0.html)
* [Proveedor de identidad externo](https://jackrabbit.apache.org/oak/docs/security/authentication/externalloginmodule.html)
* [Pertenencia a grupo dinámico](https://jackrabbit.apache.org/oak/docs/security/authentication/external/dynamic.html)
