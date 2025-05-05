---
title: Configuración de las credenciales y la autenticación de CDN
description: Obtenga información sobre cómo configurar las credenciales y la autenticación de CDN declarando reglas en un archivo de configuración que luego se implementa mediante la canalización de configuración de Cloud Manager.
feature: Dispatcher
exl-id: a5a18c41-17bf-4683-9a10-f0387762889b
role: Admin
source-git-commit: 10580c1b045c86d76ab2b871ca3c0b7de6683044
workflow-type: tm+mt
source-wordcount: '1497'
ht-degree: 4%

---


# Configuración de las credenciales y la autenticación de CDN {#cdn-credentials-authentication}

La CDN proporcionada por la Adobe tiene varias funciones y servicios, algunos de los cuales dependen de las credenciales y la autenticación para garantizar un nivel adecuado de seguridad empresarial. Al declarar reglas en un archivo de configuración implementado mediante la [canalización de configuración](/help/operations/config-pipeline.md) de Cloud Manager, los clientes pueden configurar, en modo de autoservicio, lo siguiente:

* AEM El valor del encabezado HTTP X--Edge-Key utilizado por la CDN de Adobe para validar solicitudes procedentes de una CDN administrada por el cliente.
* El token de API utilizado para purgar recursos en la caché de CDN.
* Una lista de combinaciones de nombre de usuario y contraseña que pueden acceder al contenido restringido enviando un formulario de autenticación básica.

Cada uno de ellos, incluida la sintaxis de configuración, se describe en su propia sección a continuación.

Hay una sección sobre cómo [rotar claves](#rotating-secrets), lo cual es una buena práctica de seguridad.

## Valor del encabezado HTTP de CDN administrado por el cliente {#CDN-HTTP-value}

Como se describe en la página [CDN en AEM as a Cloud Service](/help/implementing/dispatcher/cdn.md#point-to-point-CDN), los clientes pueden elegir enrutar el tráfico a través de su propia CDN, que se denomina CDN del cliente (también denominada a veces BYOCDN).

Como parte de la configuración, la CDN de Adobe y la CDN del cliente deben acordar un valor del encabezado HTTP `X-AEM-Edge-Key`. Este valor se establece en cada solicitud en la CDN del cliente antes de enrutarse a la CDN de Adobe AEM, que luego valida que el valor es el esperado, por lo que puede confiar en otros encabezados HTTP, incluidos los que ayudan a enrutar la solicitud al origen de la correspondiente.

AEM Las propiedades `edgeKey1` y `edgeKey2` de un archivo con el nombre `cdn.yaml` o similar, en algún lugar de una carpeta de nivel superior `config`, hacen referencia al valor *X--Edge-Key*. Lea [Uso de canalizaciones de configuración](/help/operations/config-pipeline.md#folder-structure) para obtener detalles acerca de la estructura de carpetas y cómo implementar la configuración.  La sintaxis se describe en el ejemplo siguiente.

Para obtener más información de depuración y errores comunes, compruebe [Errores comunes](/help/implementing/dispatcher/cdn.md#common-errors).

>[!WARNING]
>AEM El acceso directo sin una X--Edge-Key correcta se denegará para todas las solicitudes que coincidan con la condición (en el ejemplo siguiente, esto significa todas las solicitudes al nivel de publicación). Si necesita implementar gradualmente la autenticación, consulte la sección [Migración segura para reducir el riesgo de tráfico bloqueado](#migrating-safely).

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev"]
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

Consulte el tutorial [Configurar e implementar la regla CDN de validación de encabezado HTTP](https://experienceleague.adobe.com/es/docs/experience-manager-learn/cloud-service/content-delivery/custom-domain-names-with-customer-managed-cdn#configure-and-deploy-http-header-validation-cdn-rule) para obtener más información.

Entre las propiedades adicionales se incluyen:

* Nodo `Data` que contiene un nodo `authentication` secundario.
* En `authentication`, un nodo `authenticators` y un nodo `rules`, ambos son matrices.
* Autenticadores: Permite declarar un tipo de token o credencial, que en este caso es una clave perimetral. Incluye las siguientes propiedades:
   * name: una cadena descriptiva.
   * type: debe ser `edge`.
   * AEM edgeKey1: el valor de *X--Edge-Key*, que debe hacer referencia a una [variable de entorno de tipo secreto Cloud Manager](/help/operations/config-pipeline.md#secret-env-vars). En el campo Servicio aplicado, seleccione Todo. Se recomienda que el valor (por ejemplo,`${{CDN_EDGEKEY_052824}}`) refleje el día en que se agregó.
   * edgeKey2: se usa para la rotación de secretos, que se describe en la [sección de rotación de secretos](#rotating-secrets) a continuación. Definirlo de manera similar a edgeKey1. Se debe declarar al menos uno de `edgeKey1` y `edgeKey2`.
<!--   * OnFailure - defines the action, either `log` or `block`, when a request doesn't match either `edgeKey1` or `edgeKey2`. For `log`, request processing will continue, while `block` will serve a 403 error. The `log` value is useful when testing a new token on a live site since you can first confirm that the CDN is correctly accepting the new token before changing to `block` mode; it also reduces the chance of lost connectivity between the customer CDN and the Adobe CDN, as a result of an incorrect configuration. -->
* Reglas: le permite declarar cuál de los autenticadores debe utilizarse y si es para el nivel de publicación o vista previa.  Incluye:
   * name: una cadena descriptiva.
   * when: una condición que determina cuándo se debe evaluar la regla, según la sintaxis del artículo [Reglas de filtro de tráfico](/help/security/traffic-filter-rules-including-waf.md). Normalmente, incluirá una comparación del nivel actual (por ejemplo, publicación), de modo que todo el tráfico en directo se valida como enrutamiento a través de la CDN del cliente.
   * action: debe especificar &quot;authentication&quot;, con referencia al autenticador deseado.

>[!NOTE]
>La clave de Edge debe configurarse como una [variable de entorno de Cloud Manager de tipo secreto](/help/operations/config-pipeline.md#secret-env-vars) antes de que se implemente la configuración que hace referencia a ella. Se recomienda utilizar una clave aleatoria única de una longitud mínima de 32 bytes; por ejemplo, la biblioteca criptográfica Open SSL puede generar una clave aleatoria ejecutando el comando `openssl rand -hex 32`.

### Migración segura para reducir el riesgo de tráfico bloqueado {#migrating-safely}

AEM Si su sitio ya está activo, tenga cuidado al migrar a CDN administrada por el cliente, ya que una configuración incorrecta puede bloquear el tráfico público; esto se debe a que solo la CDN de Adobe aceptará las solicitudes con el valor de encabezado X--Edge-Key esperado. Se recomienda un método cuando se incluya temporalmente una condición adicional en la regla de autenticación, lo que hace que bloquee la solicitud solo si se incluye un encabezado de prueba o si coincide una ruta:

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

## Purgar token de API {#purge-API-token}

Los clientes pueden [purgar la caché de CDN](/help/implementing/dispatcher/cdn-cache-purge.md) usando un token de API de purga declarado. El token se ha declarado en un archivo con el nombre `cdn.yaml` o similar, en algún lugar bajo una carpeta de nivel superior `config`. Lea [Uso de canalizaciones de configuración](/help/operations/config-pipeline.md#folder-structure) para obtener detalles acerca de la estructura de carpetas y cómo implementar la configuración.

La sintaxis se describe a continuación:

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev"]
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

Puede hacer referencia a [un tutorial](https://experienceleague.adobe.com/es/docs/experience-manager-learn/cloud-service/caching/how-to/purge-cache) centrado en la configuración de claves de depuración y en la depuración de la caché de la CDN.

## Autenticación básica {#basic-auth}

Proteja determinados recursos de contenido mostrando un cuadro de diálogo de autenticación básica que requiera un nombre de usuario y una contraseña. Esta función está diseñada principalmente para casos de uso de autenticación ligera, como la revisión del contenido por parte de las partes interesadas empresariales, en lugar de como una solución completa para los derechos de acceso del usuario final.

El usuario final verá aparecer un cuadro de diálogo de autenticación básico como el siguiente:

![basicauth-dialog](/help/implementing/dispatcher/assets/basic-auth-dialog.png)


La sintaxis es la siguiente:

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev"]
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
>Las contraseñas deben configurarse como [variables de entorno Cloud Manager de tipo secreto](/help/operations/config-pipeline.md#secret-env-vars), antes de que se implemente la configuración que hace referencia a ellas.

## Rotación de secretos {#rotating-secrets}

1. Es recomendable cambiar las credenciales de vez en cuando. Esto se puede lograr como se muestra a continuación, utilizando el ejemplo de una clave perimetral, aunque se utiliza la misma estrategia para depurar claves.

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
