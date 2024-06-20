---
title: Configuración de las credenciales y la autenticación de CDN
description: Obtenga información sobre cómo configurar las credenciales y la autenticación de CDN declarando reglas en un archivo de configuración que luego se implementa mediante la canalización de configuración de Cloud Manager.
feature: Dispatcher
exl-id: a5a18c41-17bf-4683-9a10-f0387762889b
role: Admin
source-git-commit: 0e328d013f3c5b9b965010e4e410b6fda2de042e
workflow-type: tm+mt
source-wordcount: '1065'
ht-degree: 3%

---

# Configuración de las credenciales y la autenticación de CDN {#cdn-credentials-authentication}

>[!NOTE]
>Esta función aún no está disponible de forma general. Para unirse al programa de adopción anticipada, envíe un correo electrónico a `aemcs-cdn-config-adopter@adobe.com`.

La CDN proporcionada por la Adobe tiene varias funciones y servicios, algunos de los cuales dependen de las credenciales y la autenticación para garantizar un nivel adecuado de seguridad empresarial. Mediante la declaración de reglas en un archivo de configuración implementado mediante la variable [Canalización de configuración de Cloud Manager](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#config-deployment-pipeline), los clientes pueden configurar, de forma autoservicio, lo siguiente:

* Valor del encabezado HTTP utilizado por la CDN de Adobe para validar solicitudes procedentes de una CDN administrada por el cliente.
* El token de API utilizado para purgar recursos en la caché de CDN.

Cada uno de ellos, incluida la sintaxis de configuración, se describe en su propia sección a continuación. El [Configuración común](#common-setup) Esta sección ilustra la configuración común para ambos, así como la implementación. Por último, hay una sección sobre cómo [girar teclas](#rotating-secrets), que se considera una buena práctica de seguridad.

## Valor del encabezado HTTP de CDN administrado por el cliente {#CDN-HTTP-value}

Como se describe en la [AEM CDN en as a Cloud Service](/help/implementing/dispatcher/cdn.md#point-to-point-CDN) Los clientes pueden elegir enrutar el tráfico a través de su propia CDN, que se denomina CDN del cliente (también denominada a veces BYOCDN).

Como parte de la configuración, la CDN de Adobe y la CDN del cliente deben acordar un valor del `X-AEM-Edge-Key` Encabezado HTTP. Este valor se establece en cada solicitud, en la red de distribución de contenido (CDN) del cliente, antes de enrutarse a la red de distribución de contenido (CDN) de Adobe AEM, la cual valida que el valor es el esperado, de modo que puede confiar en otros encabezados HTTP, incluidos los que ayudan a enrutar la solicitud a la red de distribución de contenido (CDN) adecuada.

El `X-AEM-Edge-Key` se declara con la sintaxis siguiente. Consulte la [Configuración común](#common-setup) para obtener información sobre cómo implementarla.

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  experimental_authentication:
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

La sintaxis de la variable `X-AEM-Edge-Key` el valor incluye:

* Tipo, versión y metadatos.
* Nodo de datos que contiene un elemento secundario `experimental_authentication` nodo (el prefijo experimental se eliminará cuando se lance la función).
* En experimental_authentication, con un nodo autenticador y un nodo de reglas, ambos son matrices.
* Autenticadores: Permite declarar un tipo de token o credencial, que en este caso es una clave perimetral. Incluye las siguientes propiedades:
   * name: una cadena descriptiva.
   * type: debe ser edge.
   * edgeKey1: su valor debe hacer referencia a un token secreto, que no debe almacenarse en Git, sino declararse como [Variable de entorno de Cloud Manager](/help/implementing/cloud-manager/environment-variables.md) de tipo secreto. En el campo Servicio aplicado, seleccione Todo. Se recomienda usar el valor (por ejemplo,`${{CDN_EDGEKEY_052824}}`) refleja el día en que se añadió.
   * edgeKey2: se utiliza para la rotación de secretos, que se describe en la [sección girar secretos](#rotating-secrets) más abajo. Al menos uno de `edgeKey1` y `edgeKey2` debe declararse.
<!--   * OnFailure - defines the action, either `log` or `block`, when a request doesn't match either `edgeKey1` or `edgeKey2`. For `log`, request processing will continue, while `block` will serve a 403 error. The `log` value is useful when testing a new token on a live site since you can first confirm that the CDN is correctly accepting the new token before changing to `block` mode; it also reduces the chance of lost connectivity between the customer CDN and the Adobe CDN, as a result of an incorrect configuration. -->
* Reglas: le permite declarar cuál de los autenticadores debe utilizarse y si es para el nivel de publicación o vista previa.  Incluye:
   * name: una cadena descriptiva.
   * when: condición que determina cuándo se debe evaluar la regla, según la sintaxis de la variable [Reglas de filtro de tráfico](/help/security/traffic-filter-rules-including-waf.md) artículo. Normalmente, incluirá una comparación del nivel actual (por ejemplo, publicación), de modo que todo el tráfico en directo se valida como enrutamiento a través de la CDN del cliente.
   * action: debe especificar &quot;authentication&quot;, con referencia al autenticador deseado.

>[!NOTE]
>La clave de Edge debe configurarse como [Variable de entorno de Cloud Manager](/help/implementing/cloud-manager/environment-variables.md) variable de tipo `secret`, antes de que se implemente la configuración que hace referencia a ella.

## Purgar token de API {#purge-API-token}

Los clientes pueden [depurar la caché de CDN](/help/implementing/dispatcher/cdn-cache-purge.md) mediante un token de API de purga declarado. El token se declara con la sintaxis siguiente.  Consulte la [Configuración común](#common-setup) para obtener información sobre cómo implementarla.

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  experimental_authentication:
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

La sintaxis incluye lo siguiente:

* tipo, versión y metadatos.
* nodo de datos que contiene un elemento secundario `experimental_authentication` nodo (el prefijo experimental se eliminará cuando se lance la función).
* En `experimental_authentication`, con un solo nodo autenticadores.
* Autenticadores: Permite declarar un tipo de token o credencial, que en este caso es una clave de depuración. Incluye las siguientes propiedades:
   * name: una cadena descriptiva.
   * type: debe ser purge.
   * purgeKey1: su valor debe hacer referencia a un token secreto, que no debe almacenarse en Git, sino declararse como [Variables de entorno de Cloud Manager](/help/implementing/cloud-manager/environment-variables.md) de tipo `secret`.
   * En el campo Servicio aplicado, seleccione Todo. Se recomienda usar el valor (por ejemplo, `${{CDN_PURGEKEY_031224}}`) refleja el día en que se añadió.
   * purgeKey2: se utiliza para la rotación de secretos, que se describe en la [sección girar secretos](#rotating-secrets) más abajo. Al menos uno de `purgeKey1` y `purgeKey2` debe declararse.
* Reglas: le permite declarar cuál de los autenticadores debe utilizarse y si es para el nivel de publicación o vista previa.  Incluye:
   * nombre: una cadena descriptiva
   * when: condición que determina cuándo se debe evaluar la regla, según la sintaxis de la variable [Reglas de filtro de tráfico](/help/security/traffic-filter-rules-including-waf.md) artículo. Normalmente, incluye una comparación del nivel actual (por ejemplo, ... publicar).
   * action: debe especificar &quot;authentication&quot;, con referencia al autenticador deseado.

>[!NOTE]
>La clave de Edge debe configurarse como [Variable de entorno de Cloud Manager](/help/implementing/cloud-manager/environment-variables.md) variable de tipo `secret`, antes de que se implemente la configuración que hace referencia a ella.

## Configuración común {#common-setup}

Todos los autenticadores se configuran de la siguiente manera:

* En primer lugar, cree la siguiente estructura de carpetas y archivos en la carpeta de nivel superior del proyecto Git:

```
config/
     cdn.yaml
```

* En segundo lugar, la `cdn.yaml` El archivo de configuración debe contener los nodos descritos en los ejemplos siguientes. El `kind` la propiedad debe establecerse en `CDN` y la versión debe establecerse en la versión de esquema, que actualmente es `1`. El nodo de metadatos tiene una propiedad &quot;envTypes&quot;, que indica en qué tipos de entorno (dev, stage, prod) se evaluará esta configuración.

* Por último, cree una canalización de configuración de implementación de destino en Cloud Manager. Consulte [configuración de canalizaciones de producción](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md) y [configuración de canalizaciones que no son de producción](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md).

Tenga en cuenta que:

* Actualmente, los RDE no admiten la canalización de configuración.
* Puede utilizar `yq` para validar localmente el formato YAML del archivo de configuración (por ejemplo, `yq cdn.yaml`).

## Rotación de secretos {#rotating-secrets}

Es recomendable cambiar las credenciales de vez en cuando. Esto se puede lograr como se muestra a continuación, utilizando el ejemplo de una clave perimetral, aunque se utiliza la misma estrategia para depurar claves.

* Inicialmente solo `edgeKey1` se ha definido, en este caso se hace referencia a como `${{CDN_EDGEKEY_052824}}`, que como convención recomendada, refleja la fecha de creación.

```
experimental_authentication:
  authenticators:
    - name: edge-auth
      type: edge
      edgeKey1: ${{CDN_EDGEKEY_052824}}
```

* Cuando sea el momento de girar la clave, cree un nuevo secreto de Cloud Manager, por ejemplo `${{CDN_EDGEKEY_041425}}`.
* En la configuración, haga referencia a ella desde `edgeKey2` e implementarlo.

```
experimental_authentication:
  authenticators:
    - name: edge-auth
      type: edge
      edgeKey1: ${{CDN_EDGEKEY_052824}}
      edgeKey2: ${{CDN_EDGEKEY_041425}}
```

* Una vez que esté seguro de que la clave Edge antigua ya no se utiliza, elimínela eliminando `edgeKey1` en la configuración.

```
experimental_authentication:
  authenticators:
    - name: edge-auth
      type: edge
      edgeKey2: ${{CDN_EDGEKEY_041425}}
```

* Elimine la referencia secreta antigua (`${{CDN_EDGEKEY_052824}}`) desde Cloud Manager e implemente.
* Cuando esté listo para la siguiente rotación, siga el mismo procedimiento, aunque esta vez agregará `edgeKey1` a la configuración, haciendo referencia a un nuevo secreto de entorno de Cloud Manager denominado, por ejemplo, `${{CDN_EDGEKEY_031426}}`.

```
experimental_authentication:
  authenticators:
    - name: edge-auth
      type: edge
      edgeKey2: ${{CDN_EDGEKEY_041425}}
      edgeKey1: ${{CDN_EDGEKEY_031426}}
```
