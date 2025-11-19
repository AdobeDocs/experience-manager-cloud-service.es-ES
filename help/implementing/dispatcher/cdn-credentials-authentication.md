---
title: Configuración de las credenciales y la autenticación de CDN
description: Obtenga información sobre cómo configurar las credenciales y la autenticación de CDN declarando reglas en un archivo de configuración que luego se implementa mediante la canalización de configuración de Cloud Manager.
feature: Dispatcher
exl-id: a5a18c41-17bf-4683-9a10-f0387762889b
role: Admin
source-git-commit: 3a46db9c98fe634bf2d4cffd74b54771de748515
workflow-type: tm+mt
source-wordcount: '1939'
ht-degree: 3%

---


# Configuración de las credenciales y la autenticación de CDN {#cdn-credentials-authentication}

La CDN proporcionada por Adobe tiene varias funciones y servicios, algunos de los cuales dependen de las credenciales y la autenticación para garantizar un nivel adecuado de seguridad empresarial. Al declarar reglas en un archivo de configuración implementado mediante la [canalización de configuración](/help/operations/config-pipeline.md) de Cloud Manager, los clientes pueden configurar, en modo de autoservicio, lo siguiente:

* El valor del encabezado HTTP X-AEM-Edge-Key utilizado por la CDN de Adobe para validar solicitudes procedentes de una CDN administrada por el cliente.
* El token de API utilizado para purgar recursos en la caché de CDN.
* Una lista de combinaciones de nombre de usuario y contraseña que pueden acceder al contenido restringido enviando un formulario de autenticación básica.

Cada uno de ellos, incluida la sintaxis de configuración, se describe en su propia sección a continuación.

Hay una sección sobre cómo [rotar claves](#rotating-secrets), lo cual es una buena práctica de seguridad.

>[!NOTE]
> Los secretos definidos como variables de entorno deben considerarse inmutables. En lugar de cambiar su valor, debe crear un nuevo secreto con un nuevo nombre y hacer referencia a ese secreto en la configuración. Si no lo hace, se producirá una actualización poco fiable de los secretos.

>[!WARNING]
>No elimine las variables de entorno a las que se hace referencia en la configuración de CDN. Si lo hace, pueden producirse errores al actualizar la configuración de CDN (por ejemplo, actualizar reglas o dominios y certificados personalizados).

## Valor del encabezado HTTP de CDN administrado por el cliente {#CDN-HTTP-value}

Como se describe en la página [CDN en AEM as a Cloud Service](/help/implementing/dispatcher/cdn.md#point-to-point-CDN), los clientes pueden elegir enrutar el tráfico a través de su propia CDN, que se denomina CDN del cliente (también denominada a veces BYOCDN).

Como parte de la configuración, la CDN de Adobe y la CDN del cliente deben acordar un valor del encabezado HTTP `X-AEM-Edge-Key`. Este valor se establece en cada solicitud en la CDN del cliente antes de enrutarse a la CDN de Adobe, que luego valida que el valor es el esperado, por lo que puede confiar en otros encabezados HTTP, incluidos los que ayudan a enrutar la solicitud al origen de AEM adecuado.

El valor *X-AEM-Edge-Key* está referenciado por las propiedades `edgeKey1` y `edgeKey2` en un archivo de nombre `cdn.yaml` o similar, en algún lugar bajo una carpeta de nivel superior `config`. Lea [Uso de canalizaciones de configuración](/help/operations/config-pipeline.md#folder-structure) para obtener detalles acerca de la estructura de carpetas y cómo implementar la configuración.  La sintaxis se describe en el ejemplo siguiente.

Para obtener más información de depuración y errores comunes, compruebe [Errores comunes](/help/implementing/dispatcher/cdn.md#common-errors).

>[!WARNING]
>El acceso directo sin una clave X-AEM-Edge-Key correcta se denegará para todas las solicitudes que coincidan con la condición (en el ejemplo siguiente, esto significa todas las solicitudes al nivel de publicación). Si necesita implementar gradualmente la autenticación, consulte la sección [Migración segura para reducir el riesgo de tráfico bloqueado](#migrating-safely).

```
kind: "CDN"
version: "1"
data:
  authentication:
    authenticators:
      - name: edge-auth
        type: edge
        edgeKey1: ${{CDN_EDGEKEY_052824}}
        edgeKey2: ${{CDN_EDGEKEY_041425}}
    rules:
      - name: edge-auth-rule
        when: { reqProperty: tier, equals: "publish" }
        action:
          type: authenticate
          authenticator: edge-auth
```

Consulte [Uso de canalizaciones de configuración](/help/operations/config-pipeline.md#common-syntax) para obtener una descripción de las propiedades que aparecen por encima del nodo `data`. El valor de la propiedad `kind` debe ser *CDN* y la propiedad `version` debe establecerse en `1`.

Consulte el tutorial [Configurar e implementar la regla CDN de validación de encabezado HTTP](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/content-delivery/custom-domain-names-with-customer-managed-cdn#configure-and-deploy-http-header-validation-cdn-rule) para obtener más información.

Entre las propiedades adicionales se incluyen:

* Nodo `Data` que contiene un nodo `authentication` secundario.
* En `authentication`, un nodo `authenticators` y un nodo `rules`, ambos son matrices.
* Autenticadores: Permite declarar un tipo de token o credencial, que en este caso es una clave perimetral. Incluye las siguientes propiedades:
   * name: una cadena descriptiva.
   * type: debe ser `edge`.
   * edgeKey1: el valor de *X-AEM-Edge-Key*, que debe hacer referencia a una [variable de entorno de tipo secreto Cloud Manager](/help/operations/config-pipeline.md#secret-env-vars). En el campo Servicio aplicado, seleccione Todo. Se recomienda que el valor (por ejemplo,`${{CDN_EDGEKEY_052824}}`) refleje el día en que se agregó.
   * edgeKey2: se usa para la rotación de secretos, que se describe en la [sección de rotación de secretos](#rotating-secrets) a continuación. Definirlo de manera similar a edgeKey1. Se debe declarar al menos uno de `edgeKey1` y `edgeKey2`.
<!--   * OnFailure - defines the action, either `log` or `block`, when a request doesn't match either `edgeKey1` or `edgeKey2`. For `log`, request processing will continue, while `block` will serve a 403 error. The `log` value is useful when testing a new token on a live site since you can first confirm that the CDN is correctly accepting the new token before changing to `block` mode; it also reduces the chance of lost connectivity between the customer CDN and the Adobe CDN, as a result of an incorrect configuration. -->
* Reglas: le permite declarar cuál de los autenticadores debe utilizarse y si es para el nivel de publicación o vista previa.  Incluye:
   * name: una cadena descriptiva.
   * when: una condición que determina cuándo se debe evaluar la regla, según la sintaxis del artículo [Reglas de filtro de tráfico](/help/security/traffic-filter-rules-including-waf.md). Normalmente, incluirá una comparación del nivel actual (por ejemplo, publicación), de modo que todo el tráfico en directo se valida como enrutamiento a través de la CDN del cliente.
   * action: debe especificar &quot;authentication&quot;, con referencia al autenticador deseado.

>[!NOTE]
>La clave de Edge debe configurarse como una [variable de entorno de Cloud Manager de tipo secreto](/help/operations/config-pipeline.md#secret-env-vars) antes de que se implemente la configuración que hace referencia a ella. Se recomienda utilizar una clave aleatoria única de una longitud mínima de 32 bytes; por ejemplo, la biblioteca criptográfica Open SSL puede generar una clave aleatoria ejecutando el comando `openssl rand -hex 32`.

### Migración segura para reducir el riesgo de tráfico bloqueado {#migrating-safely}

Si su sitio ya está activo, tenga cuidado al migrar a CDN administrada por el cliente, ya que una configuración incorrecta puede bloquear el tráfico público; esto se debe a que solo la CDN de Adobe aceptará las solicitudes con el valor de encabezado X-AEM-Edge-Key esperado. Se recomienda un método cuando se incluya temporalmente una condición adicional en la regla de autenticación, lo que hace que bloquee la solicitud solo si se incluye un encabezado de prueba o si coincide una ruta:

```
    - name: edge-auth-rule
        when:
          allOf:  
            - { reqProperty: tier, equals: "publish" }
            - { reqHeader: x-edge-test, equals: "test" }
        action:
          type: authenticate
          authenticator: edge-auth
```

```
    - name: edge-auth-rule
        when:
          allOf:
            - { reqProperty: tier, equals: "publish" }
            - { reqProperty: path, like: "/test*" }
        action:
          type: authenticate
          authenticator: edge-auth
```

Se puede utilizar el siguiente patrón de solicitud `curl`:

```
curl https://publish-p<PROGRAM_ID>-e<ENV-ID>.adobeaemcloud.com -H "X-Forwarded-Host: example.com" -H "X-AEM-Edge-Key: <CONFIGURED_EDGE_KEY>" -H "x-edge-test: test"
```

Después de realizar la prueba correctamente, se puede eliminar la condición adicional y volver a implementar la configuración.

### Proceso de migración si el Soporte técnico de Adobe generó anteriormente el valor del encabezado HTTP `X-AEM-Edge-Key` {#migrating-legacy}

>[!NOTE]
>Antes de continuar con la migración, programe una migración de prueba en el entorno de ensayo para verificar la estrategia.

>[!WARNING]
> No cambie la clave en la CDN administrada por el cliente hasta el paso 4.

Anteriormente, el proceso de integración con una CDN administrada por el cliente implicaba a los clientes que solicitaban un valor de encabezado HTTP de clave X-AEM-Edge-Key al servicio de asistencia de Adobe, en lugar de definir el valor por su cuenta. Para migrar al nuevo método de autoservicio, en el que define sus propios valores de claves perimetrales, siga estos pasos para garantizar una transición sin problemas sin tiempo de inactividad:

1. Configure la CDN con los secretos nuevos (generados por el cliente) y antiguos (generados por Adobe) especificados como `edgeKey1` y `edgeKey2`. Esta es una variación de la documentación de [secretos giratorios](/help/implementing/dispatcher/cdn-credentials-authentication.md#rotating-secrets).

2. Implemente los secretos y la configuración de CDN de autoservicio. En este punto del proceso, el antiguo secreto definido por Adobe debe seguir siendo el valor X-AEM-Edge-Key pasado por el CDN administrado por el cliente.

3. Póngase en contacto con el Soporte técnico de Adobe y solicite que Adobe cambie para utilizar la configuración de autoservicio, especificando que ya la ha implementado.

4. Una vez que Adobe confirme que ha realizado esa acción, configure la CDN administrada por el cliente para utilizar la nueva clave definida por el cliente para el valor del encabezado HTTP `X-AEM-Edge-Key`.

5. Elimine la clave antigua de la configuración de CDN e implemente de nuevo la canalización de configuración.

>[!WARNING]
>Si no tiene la reserva con ambas claves configuradas simultáneamente, puede provocar un tiempo de inactividad durante la migración.

## Purgar token de API {#purge-API-token}

Los clientes pueden [purgar la caché de CDN](/help/implementing/dispatcher/cdn-cache-purge.md) usando un token de API de purga declarado. El token se ha declarado en un archivo con el nombre `cdn.yaml` o similar, en algún lugar bajo una carpeta de nivel superior `config`. Lea [Uso de canalizaciones de configuración](/help/operations/config-pipeline.md#folder-structure) para obtener detalles acerca de la estructura de carpetas y cómo implementar la configuración.

La sintaxis se describe a continuación:

```
kind: "CDN"
version: "1"
data:
  authentication:
    authenticators:
       - name: purge-auth
         type: purge
         purgeKey1: ${{CDN_PURGEKEY_031224}}
         purgeKey2: ${{CDN_PURGEKEY_021225}}
    rules:
       - name: purge-auth-rule
         when: { reqProperty: tier, equals: "publish" }
         action:
           type: authenticate
           authenticator: purge-auth
```

Consulte [Uso de canalizaciones de configuración](/help/operations/config-pipeline.md#common-syntax) para obtener una descripción de las propiedades que aparecen por encima del nodo `data`. El valor de la propiedad `kind` debe ser *CDN* y la propiedad `version` debe establecerse en `1`.

Entre las propiedades adicionales se incluyen:

* Nodo `data` que contiene un nodo `authentication` secundario.
* En `authentication`, un nodo `authenticators` y un nodo `rules`, ambos son matrices.
* Autenticadores: Permite declarar un tipo de token o credencial, que en este caso es una clave de depuración. Incluye las siguientes propiedades:
   * name: una cadena descriptiva.
   * type: debe ser purge.
   * purgeKey1 - su valor debe hacer referencia a una [variable de entorno de tipo secreto Cloud Manager](/help/operations/config-pipeline.md#secret-env-vars). En el campo Servicio aplicado, seleccione Todo. Se recomienda que el valor (por ejemplo, `${{CDN_PURGEKEY_031224}}`) refleje el día en que se agregó.
   * purgeKey2: se usa para la rotación de secretos, que se describe en la sección [girar secretos](#rotating-secrets) a continuación. Se debe declarar al menos uno de `purgeKey1` y `purgeKey2`.
* Reglas: le permite declarar cuál de los autenticadores debe utilizarse y si es para el nivel de publicación o vista previa.  Incluye:
   * nombre: una cadena descriptiva
   * when: una condición que determina cuándo se debe evaluar la regla, según la sintaxis del artículo [Reglas de filtro de tráfico](/help/security/traffic-filter-rules-including-waf.md). Normalmente, incluye una comparación del nivel actual (por ejemplo, ... publicar).
   * action: debe especificar &quot;authentication&quot;, con referencia al autenticador deseado.

>[!NOTE]
>La clave de purga debe configurarse como [secreto de tipo Cloud Manager Environment Variable](/help/operations/config-pipeline.md#secret-env-vars), antes de que se implemente la configuración que hace referencia a ella. Se recomienda utilizar una clave aleatoria única de al menos 32 bytes de longitud; por ejemplo, la biblioteca criptográfica Open SSL puede generar una clave aleatoria ejecutando el comando openssl rand -hex 32

Puede hacer referencia a [un tutorial](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/caching/how-to/purge-cache) centrado en la configuración de claves de depuración y en la depuración de la caché de la CDN.

## Autenticación básica {#basic-auth}

Proteja determinados recursos de contenido mostrando un cuadro de diálogo de autenticación básica que requiera un nombre de usuario y una contraseña. Esta función está diseñada principalmente para casos de uso de autenticación ligera, como la revisión del contenido por parte de las partes interesadas empresariales, en lugar de como una solución completa para los derechos de acceso del usuario final.

El usuario final verá aparecer un cuadro de diálogo de autenticación básico como el siguiente:

![basicauth-dialog](/help/implementing/dispatcher/assets/basic-auth-dialog.png)


La sintaxis es la siguiente:

```
kind: "CDN"
version: "1"
data:
  authentication:
    authenticators:
       - name: my-basic-authenticator
         type: basic
         credentials:
           - user: johndoe
             password: ${{JOHN_DOE_PASSWORD}}
           - user: janedoe
             password: ${{JANE_DOE_PASSWORD}}
    rules:
       - name: basic-auth-rule
         when: { reqProperty: path, like: "/summercampaign" }
         action:
           type: authenticate
           authenticator: my-basic-authenticator
```

Consulte [Uso de canalizaciones de configuración](/help/operations/config-pipeline.md#common-syntax) para obtener una descripción de las propiedades que aparecen por encima del nodo `data`. El valor de la propiedad `kind` debe ser *CDN* y la propiedad `version` debe establecerse en `1`.

Además, la sintaxis incluye lo siguiente:

* un nodo `data` que contiene un nodo `authentication`.
* En `authentication`, un nodo `authenticators` y un nodo `rules`, ambos son matrices.
* Autenticadores: en este caso, declare un autenticador básico, que tiene la siguiente estructura:
   * nombre: una cadena descriptiva
   * tipo: debe ser `basic`
   * una matriz de hasta 10 credenciales, cada una de las cuales incluye los siguientes pares de nombre/valor, que los usuarios finales pueden introducir en el cuadro de diálogo autenticación básica:
      * user: nombre del usuario.
      * password: su valor debe hacer referencia a una [variable de entorno de tipo secreto Cloud Manager](/help/operations/config-pipeline.md#secret-env-vars), con **All** seleccionado como campo de servicio.
* Rules: permite declarar cuál de los autenticadores se debe utilizar y qué recursos se deben proteger. Cada regla incluye:
   * nombre: una cadena descriptiva
   * when: una condición que determina cuándo se debe evaluar la regla, según la sintaxis del artículo [Reglas de filtro de tráfico](/help/security/traffic-filter-rules-including-waf.md). Normalmente, incluye una comparación del nivel de publicación o rutas específicas.
   * action: debe especificar &quot;authentication&quot;, con el autenticador deseado referenciado, que es basic-auth para este escenario

>[!NOTE]
>
>Las contraseñas deben configurarse como [variables de entorno Cloud Manager de tipo secreto](/help/operations/config-pipeline.md#secret-env-vars), antes de que se implemente la configuración que hace referencia a ellas.

## Rotación de secretos {#rotating-secrets}

Es recomendable cambiar las credenciales con regularidad por motivos de seguridad. Recuerde que las variables de entorno no deben cambiarse directamente, sino que debe crear un nuevo secreto y hacer referencia al nuevo nombre en la configuración.

Este caso de uso se ejemplifica a continuación, utilizando el ejemplo de una clave Edge, aunque la misma estrategia también se puede utilizar para depurar claves.

1. Inicialmente solo se ha definido `edgeKey1`, en este caso se hace referencia a `${{CDN_EDGEKEY_052824}}`, que como convención recomendada, refleja la fecha en que se creó.

   ```
   authentication:
     authenticators:
       - name: edge-auth
         type: edge
         edgeKey1: ${{CDN_EDGEKEY_052824}}
   ```

1. Cuando sea el momento de girar la clave, cree un nuevo secreto de Cloud Manager, por ejemplo `${{CDN_EDGEKEY_041425}}`.
1. En la configuración, haga referencia a él desde `edgeKey2` e impleméntelo.

   ```
   authentication:
     authenticators:
       - name: edge-auth
         type: edge
         edgeKey1: ${{CDN_EDGEKEY_052824}}
         edgeKey2: ${{CDN_EDGEKEY_041425}}
   ```

1. Una vez que esté seguro de que la clave perimetral antigua ya no se usa, elimínela eliminando `edgeKey1` de la configuración.

   ```
   authentication:
     authenticators:
       - name: edge-auth
         type: edge
         edgeKey2: ${{CDN_EDGEKEY_041425}}
   ```

1. Elimine la referencia secreta antigua (`${{CDN_EDGEKEY_052824}}`) de Cloud Manager e implemente.

1. Cuando esté listo para la siguiente rotación, siga el mismo procedimiento, pero esta vez agregará `edgeKey1` a la configuración, haciendo referencia a un nuevo secreto de entorno de Cloud Manager llamado, por ejemplo, `${{CDN_EDGEKEY_031426}}`.

   ```
   authentication:
     authenticators:
       - name: edge-auth
         type: edge
         edgeKey2: ${{CDN_EDGEKEY_041425}}
         edgeKey1: ${{CDN_EDGEKEY_031426}}
   ```

Al girar secretos configurados en encabezados de solicitud, por ejemplo para autenticarse en un backend, se recomienda realizar la rotación en dos pasos para garantizar que el valor del encabezado se cambie sin interrupciones temporales.

1. Configuración inicial antes de la rotación. En este estado, la clave antigua se envía al servidor.

   ```
   requestTransformations:
     rules:
       - name: set-api-key-header
         actions:
           - type: set
             reqHeader: x-api-key
             value ${{API_KEY_1}}
   ```

1. Introduzca la nueva clave `API_KEY_2` estableciendo el mismo encabezado dos veces (la nueva clave debe establecerse después de la clave antigua). Después de implementar esto, verá la nueva clave en el servidor.

   ```
   requestTransformations:
     rules:
       - name: set-api-key-header
         actions:
           - type: set
             reqHeader: x-api-key
             value ${{API_KEY_1}}
           - type: set
             reqHeader: x-api-key
             value ${{API_KEY_2}}
   ```

1. Quite la clave antigua `API_KEY_1` de la configuración. Después de implementar esto, verá la nueva clave en el backend y es seguro quitar la variable de entorno de la clave antigua.


   ```
   requestTransformations:
     rules:
       - name: set-api-key-header
         actions:
           - type: set
             reqHeader: x-api-key
             value ${{API_KEY_2}}
   ```


