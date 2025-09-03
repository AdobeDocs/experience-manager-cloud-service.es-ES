---
title: Prácticas recomendadas para la asignación de usuarios al servicio Sling y la definición de usuarios del servicio
description: Obtenga información acerca de las prácticas recomendadas para la asignación de usuarios al servicio sling y la definición de usuarios del servicio
exl-id: 72f0dcbf-b4e6-4a73-8232-3574a212ac19
feature: Security
role: Admin
source-git-commit: edfefb163e2d48dc9f9ad90fa68809484ce6abb0
workflow-type: ht
source-wordcount: '1883'
ht-degree: 100%

---

# Prácticas recomendadas para la asignación de usuarios al servicio Sling y la definición de usuarios del servicio {#best-practices-for-sling-service-user-mapping-and-service-user-definition}

## Asignación de usuarios al servicio {#service-user-mapping}

Para añadir una asignación desde su servicio a los usuarios del sistema correspondiente, debe crear una configuración de fábrica para el servicio `ServiceUserMapper`. Para mantener este módulo, se pueden proporcionar estas configuraciones utilizando el mecanismo de modificación de Sling (consulte [SLING-3578](https://issues.apache.org/jira/browse/SLING-3578) para obtener más información). La manera recomendada de instalar estas configuraciones con el paquete es agregándolo al modelo de aprovisionamiento de Quickstart, tal como se describe en el siguiente ejemplo:

```
org.apache.sling.serviceusermapping.impl.ServiceUserMapperImpl.amended-my-mapping
    user.default=""
    user.mapping=[
        "com.adobe.cq.my-bundle:my-subservice\=[content-writer-service]",
        "com.adobe.cq.my-bundle:my-subservice-different-task\="[myfeature-configuration-writer-service,content-reader-service]"
    ]
```

### Formato de asignación {#mapping-format}

A partir de la versión 6.4 de AEM, el formato de asignación se define de la siguiente manera:

>[!NOTE]
>
>El `userName` está en desuso y no debe usarse más.

```
bundleId [:subserviceName] = userName | [principalNames]   
```

`bundleId` y `subserviceName` identifican el servicio, `userName/principalNames` identifican al usuario del servicio y `principalNames` es una lista separada por comas.

Además, tenga en cuenta que `principalNames` es la lista de nombres principales de usuario de servicio que, de forma predeterminada, son los mismos que el id.


**Prácticas recomendadas**

* Nombres de subservicio para diferentes tareas: si los servicios del paquete realizan diferentes tareas, se recomienda identificar `subserviceNames` para agruparlos por tareas
* Si un servicio determinado realiza diferentes operaciones (por ejemplo, leer contenido de recursos y actualizar información debajo de un subárbol de `/var`), se recomienda reflejarlo agregando diferentes entidades de servicio que reflejen la operación individual, como agregando lo común `dam-reader-service` con la función específica `assetreport-writer-service`
* Cada servicio está idealmente vinculado a un conjunto muy específico y limitado de operaciones
* El nuevo formato con `[one,or,multiple,principalNames]` es la forma recomendada de definir las asignaciones de usuarios de servicio a partir de la versión 6.4 de AEM.

A continuación se muestra una lista de motivos para cambiar el formato y por qué Adobe recomienda utilizarlo en lugar de la asignación de versiones solo para un único ID de usuario:

* Capacidad para reutilizar usuarios de servicios combinando las necesidades especiales de los clientes con tareas comunes
* Evite la duplicación de la configuración de permisos
* Mejor comprensión de los permisos (y tareas) efectivos que un servicio determinado está realizando realmente
* No es necesario que los usuarios del servicio sean miembros explícitos del grupo. Esto puede tener efectos secundarios molestos a medida que cambian los permisos del grupo
* Mejoras de rendimiento y escalabilidad

## Resolución de asignaciones e inicio de sesión en el servicio {#mapping-resolution-and-service-login}

### Resolución de asignaciones de servicios {#service-mapping-resolution}

La secuencia de llamadas para resolver la asignación de servicio que se describe a continuación:

1. Buscar asignación activa `principalNames` para el `bundleId` y `subserviceName` proporcionados
1. Asignación `principalNames` para `bundleId` y `subserviceName` nulo
1. Asignación `userName` para `bundleId` y `subserviceName`
1. Asignación `userName` para `bundleId` y `subserviceName` nulo
1. Asignación predeterminada
1. Usuario predeterminado

### SlingRepository: inicio de sesión en el servicio {#slingrepository-servicelogin}

La secuencia para obtener un servicio `Session/ResourceResolver` funciona de la siguiente manera:

1. Obtener nombres principales de `ServiceUserMapper` = > inicie sesión en el repositorio previo a la autenticación como se describe a continuación
1. Recuperar ID de usuario de `ServiceUserMapper`
1. Compruebe si hay `1ServiceUserConfiguration` obsoletas para el ID de usuario actual
1. Inicio de sesión predeterminado del servicio Sling con el ID de usuario (por ejemplo, una secuencia de `createAdministrativeSession` y suplantar para el ID de usuario del servicio)

La nueva asignación con nombres principales da como resultado el siguiente inicio de sesión simplificado en el repositorio:

* El conjunto de nombres principales se trata como el Principal o Principales efectivos que se utilizarán para rellenar el `Subject`
* Por lo tanto, el inicio de sesión en el repositorio se puede autenticar previamente
* No hay resolución de pertenencia a grupo

  >[!NOTE]
  >
  >Deben declararse todos los permisos necesarios para los usuarios del servicio. Ya no se heredarán &#39;todos&#39; y otros permisos de grupo.

* No se crean inicios de sesión de administrador adicionales para el servicio-`Session/ResourceResolver`.

### ServiceUserConfiguration obsoleta {#deprecated-serviceUserConfiguration}

Tenga en cuenta que especificar un solo nombre de usuario en la asignación equivale al `ServiceUserConfiguration.simpleSubjectPopulation` existente. Con el nuevo formato, la solución que proporciona el `ServiceUserConfiguration` se puede reflejar directamente con la asignación de usuario del servicio. El `ServiceUserConfiguration` por lo tanto, ha quedado obsoleto para AEM y se han reemplazado todos los usos existentes.

## Usuarios del servicio {#service-users}

### Reutilización de usuarios del servicio existentes {#reusing-existing-service-users}

Se recomienda reutilizar los usuarios del servicio existentes si se cumplen las siguientes condiciones:

* Sus necesidades coinciden con la intención del usuario del servicio existente
* El servicio requiere que realice una tarea común que esté cubierta por un usuario de servicio común existente. En este caso, se recomienda reutilizar el usuario del servicio en lugar de introducir la duplicación
* El servicio requiere una tarea específica cubierta por un usuario de servicio existente. Si no está seguro de esto, pregunte al equipo de funciones que lo posee.

No reutilice usuarios de servicio existentes si:

* Debe modificar su permiso de forma no relacionada para que funcione
* Si solo necesita un pequeño subconjunto del permiso que proporciona y lo reutiliza, porque hace que su función funcione, no porque coincida de verdad
* Si su nombre indica una intención totalmente diferente que lo que necesita. Seleccionarlo porque funciona puede causar problemas en el futuro, ya que el equipo de funciones que posee un servicio específico puede cambiar los permisos y romper la función.

### Creación de un usuario de servicio {#creating-a-service-user}

Después de comprobar que ningún usuario de servicio existente en AEM se aplica a su caso de uso y de aprobar los problemas de RTC correspondientes, puede continuar y añadir el nuevo usuario al contenido predeterminado. Lo ideal es que un miembro del equipo de seguridad ampliado participe en la votación del RTC, por lo que asegúrese de incluir también a las partes interesadas adecuadas.

**Convención de nomenclatura**

El equipo de seguridad de AEM ha definido la siguiente convención de nomenclatura para que los usuarios del servicio agreguen coherencia a los nuevos usuarios del servicio y mejoren su legibilidad y capacidad de mantenimiento.

Un nombre de usuario de servicio consta de 3 elementos separados por un guión **&#39;-&#39;**:

1. La entidad/función lógica objetivo de las operaciones del servicio (evite los elementos de rutas, ya que pueden cambiar)
1. La tarea que van a realizar los servicios
1. **&#39;Servicio&#39;** final para poder identificar fácilmente a partir del id y el nombre principal que el usuario es un usuario de servicio

**Prácticas recomendadas**

* No mezcle diferentes entidades/características. Divida a usuarios de servicio individuales y agréguelos en la asignación si el servicio tiene necesidades diferentes
* Limítese a una tarea bien definida por cada usuario de servicio. Divida si acaba otorgando demasiados permisos o no relacionados
* Dedique tiempo a identificar las necesidades reales de su servicio
* Dedique tiempo a encontrar un nombre de usuario de servicio bueno, significativo y que se explique por sí mismo
* Solicite comentarios y opiniones: los desarrolladores que no estén familiarizados con esta función deberían poder leer y comprender su intención. En el futuro, se les podría encargar su reparación o mantenimiento.

Al final, el nombre de usuario del servicio debe mostrar:

* Cómo se va a utilizar y si se puede reutilizar:

   * Muy genérico: `content-writer-service`. Es seguro reutilizarlo en la agregación si los servicios también necesitan poder leer todo el contenido
   * Muy específico: `asset-linkshare-service`. No es tan seguro reutilizarlo a menos que el servicio también comparta vínculos de recursos.

* Aspecto esperado del conjunto de funciones y la configuración de permisos:

   * La entidad lógica debe coincidir con la configuración de permisos:

      * A `content-foo-service` solo debe asociarse con operaciones en el contenido. No estaría bien concederle permisos para operar en otras entidades como la configuración o los usuarios
      * Un servicio específico como `personalization-foo-service` también debe incluir permisos específicos. Si termina concediendo permisos en todo el contenido, ya no es específico. Refleje eso en el nombre o reutilice un usuario común en la agregación
      * Un servicio específico de la función como `msm-xyz-service` solo debe tener permisos relacionados con msm. No expanda permisos a funciones no relacionadas, como administrar la configuración de comunidades o los usuarios de pantallas.

   * La tarea debe coincidir con los permisos:

      * Un `foo-reader-service` solo debería poder leer elementos normales. Nunca conceder permisos de escritura
      * Se puede esperar que un `foo-writer-service` realice operaciones de escritura. Sin embargo, no se deben conceder permisos para leer o modificar el contenido de control de acceso
      * Se puede esperar que un `foo-replicator-service` tenga `crx:replicate` concedido.

**Ejemplos**

Ejemplos de `configuration-reader-service`:

* El nombre indica que hace referencia a configuraciones en general y no a la configuración de una función en particular, como la configuración de la integración de DM. Un usuario de servicio específico para leer la configuración de una integración de este tipo preferiría recibir el nombre `dmconfig-reader-service` o `s7config-reader-service`

  >[!NOTE]
  >
  >No se incluye información de ruta en la asignación de nombres. Las configuraciones se han movido de `/etc` hasta `/conf`.

* El elemento de tarea indica que los servicios enlazados a ese usuario solo realizarán operaciones de lectura.

Ejemplos de `userproperties-copy-service`:

* Los servicios enlazados a este usuario de servicio funcionarán en propiedades de usuario/grupo como perfiles o preferencias
* Está diseñada específicamente para copiar esa información en contraste con un nombre como `userproperties-writer-service` que incluiría cualquier tipo de operación de escritura. Por lo tanto, es posible que la configuración de permisos para estas tareas de copia solo permita añadir elementos en una ubicación y quitarlos en otra.

**Prácticas recomendadas para la configuración de permisos**

* Utilice siempre la configuración de control de acceso basado en principales para los usuarios del servicio. Para obtener más información, consulte los siguientes ejemplos:

   * Permitir que los usuarios del servicio de marcado y sus permisos marquen como contenido de aplicación inmutable en Skyline
   * No es necesario crear rutas y estructuras de árbol

* Conceder permisos únicamente, nunca denegarlos
* Limitar permisos

   * Conceder solo el conjunto mínimo de permisos necesarios
   * Para obtener más información, consulte la documentación [Asignación de privilegios a elementos](https://jackrabbit.apache.org/oak/docs/security/privilege/mappingtoitems.html?lang=es) y [Asignación de llamadas de API a privilegios](https://jackrabbit.apache.org/oak/docs/security/privilege/mappingtoprivileges.html?lang=es)
   * No conceder permiso para `jcr:all`. Es muy probable que ese no sea el conjunto mínimo.

* Reducir ámbito

   * Situar directivas de control de acceso en subárboles específicos de la función
   * En el caso de los artículos distribuidos: utilice restricciones para limitar el ámbito (consulte [la documentación](https://jackrabbit.apache.org/oak/docs/security/authorization/restriction.html?lang=es) para la lista de restricciones integradas).

* Garantizar la coherencia

   * Hacer que los permisos sean coherentes con la entidad y la tarea que utilizó en el nombre de usuario del servicio
   * Evite añadir permisos no relacionados. Por ejemplo, sería extraño tener un `workflow-administration-service` y concederle permisos para realizar operaciones de administración de usuarios en `/home/users/screens` o dejarle leer s7-config.

* Integridad

   * Asegúrese de que el servicio tiene todos los permisos necesarios para realizar las tareas para las que está diseñado. El servicio debe funcionar de forma predeterminada también en entornos de clientes.
   * Nunca espere/pida a los clientes que amplíen la configuración de permisos (por ejemplo, por debajo de `/apps`)

* Evite la duplicación de la configuración de permisos

   * Reutilización de usuarios de servicios comunes
   * Agréguelos con los usuarios de servicio específicos de su función que proporcionen además el permiso específico que necesita

* No divida la configuración de permisos entre distintas funciones. La necesidad de hacerlo indica que el usuario del servicio no está bien definido o hace demasiadas cosas diferentes
* No coloque a los usuarios del servicio en grupos porque:

   * Combina detalles de implementación de usuarios del servicio con grupos &quot;públicos&quot;
   * Falta de control sobre los cambios de permisos (propenso a regresiones y escaladas de privilegios)
   * Inicio de sesión y rendimiento de evaluación
   * No funciona con la configuración de CA basada en principal

* El acceso al nodo user-home (o a cualquier subárbol contenido en él), que no tiene una ruta predecible, se logra en el repo init mediante Inicio(`userId`). Consulte la [documentación](https://sling.apache.org/documentation/bundles/repository-initialization.html) de repo init de sling para obtener más información.
* RTC: cree un problema de RTC específico si modifica los permisos de un usuario de servicio existente y se asegura de que el equipo de seguridad lo revise.

**Creación con inicialización de repositorio**

Use siempre `repo-init` para definir los usuarios del servicio y su configuración de permisos, y coloque ambos en la sección correcta del modelo de funciones de inicio rápido:

**Prácticas recomendadas**

* Usar siempre `repo-init` para crear el usuario del servicio
* Especificar siempre una ruta intermedia para la creación de usuarios del servicio
* Todos los usuarios del servicio integrados para AEM deben encontrarse a continuación `system/cq:services/internal`
* Además, anexe a la ruta relativa intermedia para agrupar a los usuarios del servicio por función: `system/cq:services/internal/<your-feature>`
* Los usuarios de servicios definidos por el cliente deben estar ubicados a continuación `system/cq:services/<customer-intermediate-rel-path>` y nunca debajo del árbol interno
* Uso **con ruta forzada** en lugar de **con ruta** si ya existía un usuario y debe moverse a la nueva ubicación que admita la autorización basada en principal.

**Ejemplos**

```
create service user my-new-feature-readcomment-service with path system/cq:services/internal/myfeature
set principal ACL for my-new-feature-readcomment-service
    allow rep:readProperties on /content/myFeature restriction(rep:itemNames,commentTitle,commentDate,commentTxt)
end
```

```
create service user my-existing-feature-addcomment-service with forced path system/cq:services/internal/myfeature
set principal ACL for my-existing-feature-addcomment-service
    allow jcr:addChildNodes,rep:addProperties on /content/myfeature restrictions(rep:glob,*/comments/*)
end
```

```
create service user myfeature-ims-service with path system/cq:services/internal/myfeature
set principal ACL for myfeature-ims-service
    allow jcr:read on home(myfeature-ims-service)
end
```

### Usuarios y permisos del servicio de limpieza {#cleanup-service-users-and-permissions}

El siguiente comando repo init se puede utilizar para limpiar los usuarios de servicio no utilizados y sus permisos:

```
# Remove the principal-based access control policy for principal my-feature-service
delete principal ACL for my-feature-service

# Remove all resource-based access control entries (ACEs) for principal my-feature-service
delete ACL for my-feature-service

# Disable the service user
disable service user my-feature-service : "My feature is no longer used"

# Remove the service user
delete service my-feature-service 
```

### Usuarios de servicio de pruebas {#testing-service-users}

Es crucial escribir pruebas del lado del servidor para los usuarios del servicio y su configuración de permisos. Esto no solo comprueba que la configuración realmente funciona, sino que también le ayuda a detectar regresiones y errores no deseados al cambiar el contenido del control de acceso o los usuarios del servicio.

La biblioteca `com.adobe.granite.testing.clients` proporciona muchas utilidades que facilitan la escritura de SST para los usuarios de servicios.
