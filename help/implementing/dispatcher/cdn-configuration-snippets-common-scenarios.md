---
title: Fragmentos de configuración de CDN para escenarios comunes
description: Patrones YAML listos para la copia para las configuraciones de CDN administrada por Adobe y CDN administrada por el cliente, incluida la autenticación perimetral, redirecciones, variación de caché, forma de tráfico y límites de velocidad.
feature: Dispatcher
role: Admin
source-git-commit: ab43facbd4c34c92878e303acf2fef9cc127e28a
workflow-type: tm+mt
source-wordcount: '434'
ht-degree: 0%

---


# Fragmentos de configuración de CDN para escenarios comunes {#cdn-configuration-snippets}

Este artículo recopila patrones `cdn.yaml` prácticos para AEM as a Cloud Service. Utilícelos junto con la documentación de características para [reglas de tráfico CDN](/help/implementing/dispatcher/cdn-configuring-traffic.md), [credenciales CDN administradas por el cliente](/help/implementing/dispatcher/cdn-credentials-authentication.md) y [reglas de filtro de tráfico, incluido WAF](/help/security/traffic-filter-rules-including-waf.md). Implementar fragmentos de código con una [canalización de configuración](/help/operations/config-pipeline.md) de Cloud Manager.

>[!NOTE]
>
>Reemplace nombres de host, rutas, intervalos de IP, claves y umbrales por valores que coincidan con su programa. Pruebe los cambios en un entorno que no sea de producción antes de promocionarlos.

## CDN administrado por el cliente {#customer-managed-cdn}

### Configuración de la autenticación de clave de Edge solo para algunos dominios {#edge-auth-selected-hosts}

Problema: En una [CDN](/help/implementing/dispatcher/cdn.md#point-to-point-cdn) administrada por el cliente, debe aplicar la autenticación para algunos nombres de host de clientes, mientras que otros nombres de host que lleguen a la publicación deben permanecer disponibles sin ese encabezado (por ejemplo, durante el despliegue o cuando solo un dominio de marca se encuentre detrás de su CDN).

Solución: requiera autenticación de `X-AEM-Edge-Key` solo cuando el primer nombre de host de `X-Forwarded-Host` sea igual al nombre de host de destino (por ejemplo, `example.com`). La regla usa la propiedad de solicitud `forwardedDomain` para realizar esa coincidencia y ejecuta la acción `authenticate` contra el autenticador de Edge. Reemplace nombres de host, nombres de autenticador y marcadores de posición clave para su programa.

```yaml
kind: "CDN"
version: "1"
data:
  authentication:
    authenticators:
      - name: edge-key-auth
        type: edge
        edgeKey1: ${{CDN_EDGEKEY_1}}
        edgeKey2: ${{CDN_EDGEKEY_2}}
    rules:
      - name: edge-key-auth-rule
        when: { reqProperty: forwardedDomain, equals: "example.com" }
        action:
          type: authenticate
          authenticator: edge-key-auth
```

### Configuración de la autenticación de clave de Edge para solicitudes que no provienen de direcciones IP VPN {#edge-auth-trusted-ips}

Problema: Configure la autenticación de clave perimetral para BYOCDN, pero permita el acceso directo al dominio de publicación solo para IP de VPN

Solución: Requiera autenticación de clave X-AEM-Edge solo cuando la dirección IP del cliente no esté en la lista de direcciones IP VPN

```yaml
kind: "CDN"
version: "1"
data:
  authentication:
    authenticators:
      - name: edge-key-auth
        type: edge
        edgeKey1: ${{CDN_EDGEKEY_1}}
        edgeKey2: ${{CDN_EDGEKEY_2}}
    rules:
      - name: edge-key-auth-rule
        when: { reqProperty: clientIp, notIn: ["10.0.0.1", "11.0.0.0/24", "<other VPN IPs>"] }
        action:
          type: authenticate
          authenticator: edge-key-auth
```

## Redireccionamientos {#redirects}

### Redireccionando desde el dominio APEX a www {#apex-to-www}

```yaml
kind: "CDN"
version: "1"
data:
 redirects:
   rules:
     - name: non-www-to-www-redirect
       when:
         reqProperty: domain
         doesNotMatch: '^www\.'
       action:
         type: redirect
         status: 301
         location:
           join:
             format: 'https://www.%s%s'
             args:
               - reqProperty: domain
               - reqProperty: url
```

### Modificación de la clave de caché {#cache-key}

La CDN no expone un campo &quot;clave de caché&quot; independiente. Como la dirección URL participa en el almacenamiento en caché, puede dividir las entradas de caché cambiando la dirección URL; por ejemplo, agregando un parámetro de consulta mediante una [transformación de solicitud](/help/implementing/dispatcher/cdn-configuring-traffic.md#request-transformations).

```yaml
kind: "CDN"
version: "1"
data:
  requestTransformations:
    rules:
      - name: set-request-different-cache-curl
        when:
          allOf:
            - reqProperty: tier
              equals: publish
            - reqHeader: user-agent
              matches: curl
        actions:
          - type: set
            queryParam: cache
            value: 'curl'
```

### Redirigir a una ruta normalizada {#trailing-slash}

Envíe una redirección permanente cuando un explorador solicite una barra diagonal en la publicación, por ejemplo, de `https://www.example.com/path/` a `https://www.example.com/path`.

```yaml
kind: "CDN"
version: "1"
data:
  redirects:
    rules:
      - name: remove-trailing-slash
        when:
          allOf:
            - reqProperty: tier
              equals: publish
            - reqProperty: domain
              equals: www.example.com
            - reqProperty: originalPath
              matches: ^/(.+)/$
        action:
          type: redirect
          status: 301
          location:
            reqProperty: originalPath
            transform:
              - op: replace
                match: ^/(.+)/$
                replacement: https://www.example.com/\1
```

### Extracción de información de una cookie JSON {#json-cookie}

```yaml
kind: "CDN"
version: "1"
data:
  requestTransformations:
    rules:
      - name: options-response
        when: { reqProperty: tier, equals: publish }
        actions:
        - type: set
          reqHeader: x-mycookie-info
          value:
            reqCookie: mycookie
            transform: 
            - 'base64decode'
            - { op: 'replace', match: '"info":\s*"([^"]*)"', replacement: '\1'} 
```

## Configuración de origen cruzado {#cross-origin}

### Servicio de solicitudes de OPTIONS desde la CDN {#options-from-cdn}

```yaml
kind: "CDN"
version: "1"
data:
  requestTransformations:
    rules:
      - name: options-response
        when:
          allOf: 
            - { reqProperty: path, like: /mypathi*  }
            - { reqProperty: method, equals: "OPTIONS" }
            - { reqHeader: Origin, equals: "https://example.com" }
        actions:
          - type: respond
            status: 200
            reason: "OK"
            headers:
              content-type: 'text/plain'
              access-control-allow-origin: { reqHeader: Origin }
              access-control-allow-methods: "*"
              access-control-allow-headers: "*"
```

## Filtros de tráfico {#traffic-filters}

### ASN de limitación de velocidad {#rate-limit-asn}

Problema: Los límites de tasa por IP pueden pasar por alto un patrón de denegación de servicio distribuido (DDoS): cada dirección permanece por debajo del umbral, por lo que el tráfico legítimo y abusivo se parece al de la capa IP.

Solución: cuente las solicitudes por nombre de sistema autónomo (`clientAsName`) de modo que el limitador agregue hosts que compartan el mismo nombre de red. El fragmento escribe `clientAsName` en una propiedad de registro en cada solicitud y, a continuación, aplica un límite de velocidad en la creación y publicación agrupadas por ese valor. Muchos usuarios pueden compartir una ASN (por ejemplo, un ISP grande o una salida VPN corporativa), por lo que debe ajustar los límites cuidadosamente y supervisar los registros de CDN para detectar falsos positivos.

```yaml
kind: "CDN"
version: "1"
data:
  requestTransformations:
    rules:
      - name: log-on-request
        when: "*"
        actions:
          - type: set
            logProperty: client_as_name
            value:
              reqProperty: clientAsName
  trafficFilters:
    rules:
    - name: limit-requests-client-as-name
      when:
        reqProperty: tier
        matches: "author|publish"
      rateLimit:
        limit: 60
        window: 10
        penalty: 300
        count: all
        groupBy:
          - reqProperty: clientAsName
      action: block
```
