---
title: Configurar la conexión avanzada para AEM as a Cloud Service
description: Aprenda a configurar funciones de red avanzadas como una VPN o una dirección IP de salida flexible o dedicada para AEM as a Cloud Service
source-git-commit: 4079e44d4fdce49b1c60caf178583a8800e17c0e
workflow-type: ht
source-wordcount: '2982'
ht-degree: 100%

---


# Configurar la conexión avanzada para AEM as a Cloud Service {#configuring-advanced-networking}

Este artículo tiene como objetivo presentarle las diferentes funciones de red avanzadas de AEM as a Cloud Service, incluido el aprovisionamiento de autoservicio de VPN, puertos no estándar y direcciones IP de salida dedicadas.

>[!INFO]
>
>También puede encontrar una serie de artículos diseñados para guiarle por cada una de las opciones avanzadas de red en esta [ubicación](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/networking/advanced-networking.html?lang=es).

## Información general {#overview}

AEM as a Cloud Service ofrece varios tipos de funciones de red avanzadas, que los clientes pueden configurar mediante las API de Cloud Manager. Entre estas características se incluyen:

* [Salida de puerto flexible](#flexible-port-egress): configure AEM as a Cloud Service para permitir el tráfico saliente desde puertos no estándar
* [Dirección IP de salida dedicada](#dedicated-egress-IP-address): configure el tráfico de AEM as a Cloud Service para que se origine desde una IP única
* [Red privada virtual (VPN)](#vpn): haga seguro el tráfico entre la infraestructura de un cliente y AEM as a Cloud Service, para clientes que tienen tecnología VPN

Este artículo describe cada una de estas opciones en detalle, incluido cómo se pueden configurar. Como estrategia de configuración general, el punto de conexión de API `/networkInfrastructures` se invoca en el nivel de programa para declarar el tipo deseado de red avanzada, seguido de una llamada a la función `/advancedNetworking` para cada entorno para habilitar la infraestructura y configurar parámetros específicos del entorno. Consulte los puntos de conexión adecuados en la documentación de la API de Cloud Manager para cada sintaxis formal, así como las solicitudes y respuestas de ejemplo.

Un programa puede proporcionar una única variación avanzada de red. Al decidir entre una salida de puerto flexible y una dirección IP de salida dedicada, se recomienda elegir una salida de puerto flexible si no se requiere una dirección IP específica, ya que Adobe puede optimizar el rendimiento del tráfico de salida de puerto flexible.

>[!INFO]
>
>La red avanzada no está disponible para el programa de zona protegida.
>Además, los entornos deben actualizarse a AEM versión 5958 o superior.

>[!NOTE]
>
>Los clientes que ya dispongan de tecnología de salida dedicada heredada y que necesiten configurar una de estas opciones no deben hacerlo o la conectividad del sitio puede verse afectada. Póngase en contacto con el servicio de asistencia de Adobe para obtener ayuda.

## Salida de puerto flexible {#flexible-port-egress}

Esta función de red avanzada le permite configurar AEM as a Cloud Service para recibir tráfico a través de puertos que no sean HTTP (puerto 80) y HTTPS (puerto 443), que están abiertos de forma predeterminada.

### Consideraciones {#flexible-port-egress-considerations}

La salida de puerto flexible es la opción recomendada si no necesita VPN ni una dirección IP de salida dedicada, ya que el tráfico que no depende de una salida dedicada puede obtener un mayor rendimiento.

### Configuración {#configuring-flexible-port-egress-provision}

Una vez por programa, el punto final de POST `/program/<programId>/networkInfrastructures` se invoca, pasando simplemente el valor de `flexiblePortEgress` para el parámetro `kind` y la región. El punto final responde con la variable `network_id`, así como otra información, incluido el estado. Se debe hacer referencia al conjunto completo de parámetros y a la sintaxis exacta en los documentos de API.

Una vez realizada la llamada, la infraestructura de red tarda aproximadamente 15 minutos en aprovisionarse. Una llamada al [punto de conexión de GET de infraestructura de red](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/#operation/getNetworkInfrastructure) de Cloud Manager mostraría el estado “listo”.

Si la configuración de salida de puerto flexible con alcance de programa está lista, el punto final `PUT /program/<program_id>/environment/<environment_id>/advancedNetworking` debe invocarse por entorno para habilitar la red en el nivel de entorno y para declarar opcionalmente cualquier regla de reenvío de puerto. Los parámetros se pueden configurar por entorno para ofrecer flexibilidad.

Las reglas de reenvío de puertos deben declararse para cualquier puerto que no sea 80/443 especificando el conjunto de hosts de destino (nombres o IP, y con puertos). Para cada host de destino, los clientes deben asignar el puerto de destino deseado a un puerto desde 30000 hasta 30999.

La API debe responder en solo unos segundos e indicar un estado de actualización y, después de unos 10 minutos, el método `GET` del punto de conexión debe indicar que la red avanzada está habilitada.

### Actualizaciones {#updating-flexible-port-egress-provision}

La configuración de nivel de programa se puede actualizar invocando el punto de conexión `PUT /api/program/<program_id>/network/<network_id>` y surte efecto en unos minutos.

>[!NOTE]
>
> El parámetro “kind” (`flexiblePortEgress`, `dedicatedEgressIP` o `VPN`) no se puede modificar. Póngase en contacto con la asistencia al cliente para obtener ayuda; describa lo que ya se ha creado y el motivo del cambio.

Las reglas de reenvío de puertos por entorno se pueden actualizar invocando de nuevo el punto de conexión `PUT /program/{programId}/environment/{environmentId}/advancedNetworking`. Asegúrese de incluir el conjunto completo de parámetros de configuración en lugar de un subconjunto.

### Eliminación o desactivación de la salida de puerto flexible {#deleting-disabling-flexible-port-egress-provision}

Para **eliminar** la infraestructura de red, envíe un ticket a asistencia al cliente, en el que se describa lo que se ha creado y por qué debe eliminarse.

Para **desactivar** la salida de puerto flexible desde un entorno particular, invoque `DELETE [/program/{programId}/environment/{environmentId}/advancedNetworking]()`.

Para obtener más información, consulte la [Documentación de la API de Cloud Manager](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/#operation/disableEnvironmentAdvancedNetworkingConfiguration).

### Enrutamiento del tráfico {#flexible-port-egress-traffic-routing}

Para el tráfico HTTP o HTTPS que va a puertos que no sean 80 o 443, un proxy debe configurarse mediante las siguientes variables de entorno de host y puerto:

* para HTTP: `AEM_PROXY_HOST` / `AEM_HTTP_PROXY_PORT ` (de forma predeterminada, `proxy.tunnel:3128` en versiones de AEM &lt; 6094)
* para HTTPS: `AEM_PROXY_HOST` / `AEM_HTTPS_PROXY_PORT ` (de forma predeterminada, `proxy.tunnel:3128` en versiones de AEM &lt; 6094)

Por ejemplo, este es un ejemplo de código para enviar una solicitud a `www.example.com:8443`:

```java
String url = "www.example.com:8443"
String proxyHost = System.getenv().getOrDefault("AEM_PROXY_HOST", "proxy.tunnel");
int proxyPort = Integer.parseInt(System.getenv().getOrDefault("AEM_HTTPS_PROXY_PORT", "3128"));
HttpClient client = HttpClient.newBuilder()
      .proxy(ProxySelector.of(new InetSocketAddress(proxyHost, proxyPort)))
      .build();
 
HttpRequest request = HttpRequest.newBuilder().uri(URI.create(url)).build();
HttpResponse<String> response = client.send(request, BodyHandlers.ofString());
```

Si utiliza bibliotecas de red Java no estándar, configure los proxies con las propiedades anteriores para todo el tráfico.

El tráfico no HTTP/S con destinos a través de puertos declarados en el parámetro `portForwards` debe hacer referencia a una propiedad denominada `AEM_PROXY_HOST`, junto con el puerto asignado. Por ejemplo:

```java
DriverManager.getConnection("jdbc:mysql://" + System.getenv("AEM_PROXY_HOST") + ":53306/test");
```

La siguiente tabla describe el enrutamiento de tráfico:

<table>
<thead>
  <tr>
    <th>Tráfico</th>
    <th>Condición de destino</th>
    <th>Puerto </th>
    <th>Conexión</th>
    <th>Ejemplo de destino externo</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td><b>Protocolo HTTP o HTTPS</b></td>
    <td>Tráfico HTTP/S estándar</td>
    <td>80 o 443</td>
    <td>Permitido</td>
    <td></td>
  </tr> 
  <tr>
    <td></td>
    <td>Tráfico no estándar (en otros puertos fuera de 80 o 443) a través del proxy HTTP configurado usando la variable de entorno y el número de puerto proxy siguientes. No declare el puerto de destino en el parámetro portForwards de la llamada API de Cloud Manager:<br><ul>
     <li>AEM_PROXY_HOST (predeterminado en `proxy.túnel` en versiones de AEM &lt; 6094)</li>
     <li>AEM_HTTPS_PROXY_PORT (de forma predeterminada al puerto 3128 en versiones de AEM &lt; 6094)</li>
    </ul>
    <td>Puertos fuera de 80 o 443</td>
    <td>Permitido</td>
    <td>example.com:8443</td>
  </tr>
  <tr>
    <td></td>
    <td>El tráfico no estándar (en otros puertos fuera de los puertos 80 o 443) que no utiliza el proxy HTTP</td>
    <td>Puertos fuera de 80 o 443</td>
    <td>Bloqueado</td>
    <td></td>
  </tr>
  <tr>
    <td><b>No HTTP o no HTTPS</b></td>
    <td>El cliente se conecta a la <code>AEM_PROXY_HOST</code> variable de entorno mediante un <code>portOrig</code> declarado en el parámetro de API <code>portForwards</code>.</td>
    <td>Cualquiera</td>
    <td>Permitido</td>
    <td><code>mysql.example.com:3306</code></td>
  </tr>
  <tr>
    <td></td>
    <td>Todo lo demás</td>
    <td>Cualquiera</td>
    <td>Bloqueado</td>
    <td><code>db.example.com:5555</code></td>
  </tr>
</tbody>
</table>

**Configuración de Apache/Dispatcher**

La directiva del nivel de AEM Cloud Service Apache/Dispatcher `mod_proxy` puede configurarse con las propiedades descritas anteriormente.

```
ProxyRemote "http://example.com:8080" "http://${AEM_PROXY_HOST}:3128"
ProxyPass "/somepath" "http://example.com:8080"
ProxyPassReverse "/somepath" "http://example.com:8080"
```

```
SSLProxyEngine on //needed for https backends
 
ProxyRemote "https://example.com:8443" "http://${AEM_PROXY_HOST}:3128"
ProxyPass "/somepath" "https://example.com:8443"
ProxyPassReverse "/somepath" "https://example.com:8443"
```

## Dirección IP de salida dedicada {#dedicated-egress-IP-address}

>[!NOTE]
>
>Si se le ha proporcionado una IP de salida dedicada antes de la versión de septiembre de 2021 (6/10/21), consulte [Clientes de direcciones de salida dedicadas heredadas](#legacy-dedicated-egress-address-customers).

### Ventajas {#benefits}

Esta dirección IP dedicada puede mejorar la seguridad al integrarse con proveedores de SaaS (como un proveedor CRM) u otras integraciones fuera de AEM as a Cloud Service que ofrecen una lista de permitidos de direcciones IP. Al añadir la dirección IP dedicada a la lista de permitidos, se garantiza que solo el tráfico de AEM Cloud Service del cliente pueda fluir al servicio externo. Esto se suma al tráfico de cualquier otra IP permitida.

Sin la función de dirección IP dedicada habilitada, el tráfico proveniente de AEM as a Cloud Service fluye a través de un conjunto de IP compartidas con otros clientes.

### Configuración {#configuring-dedicated-egress-provision}

>[!INFO]
>
>La capacidad de reenvío de Splunk no es posible desde una dirección IP de salida dedicada.

La configuración de la dirección IP de salida dedicada es idéntica a la [salida de puerto flexible](#configuring-flexible-port-egress-provision).

La principal diferencia es que el tráfico siempre saldrá de una IP única y dedicada. Para encontrar esa IP, utilice una resolución DNS para identificar la dirección IP asociada a `p{PROGRAM_ID}.external.adobeaemcloud.com`. No se espera que la dirección IP cambie, pero si necesita cambiarla en el futuro, se proporcionará una notificación avanzada.

Además de las reglas de enrutamiento admitidas por la salida de puerto flexible en el punto final `PUT /program/<program_id>/environment/<environment_id>/advancedNetworking`, la dirección IP de salida dedicada admite un parámetro `nonProxyHosts`. Esto le permite declarar un conjunto de hosts que deben enrutarse a través de un intervalo de direcciones IP compartidas en lugar de la IP dedicada, lo que puede resultar útil, ya que la salida de tráfico a través de direcciones IP compartidas puede optimizarse aún más. Las direcciones URL `nonProxyHost` pueden seguir los patrones de `example.com` o `*.example.com`, donde el comodín solo se admite al inicio del dominio.

Al decidir entre una salida de puerto flexible y una dirección IP de salida dedicada, los clientes deben elegir una salida de puerto flexible si no se requiere una dirección IP específica, ya que Adobe puede optimizar el rendimiento del tráfico de salida de puerto flexible.

### Enrutamiento del tráfico {#dedcated-egress-ip-traffic-routing}

El tráfico HTTP o HTTPS que va a destinos a través de los puertos 80 o 443 pasará a través de un proxy preconfigurado, suponiendo que se utilice la biblioteca de red Java estándar. Para el tráfico HTTP o HTTPS que pasa por otros puertos, un proxy debe configurarse con las siguientes propiedades.

```
AEM_HTTP_PROXY_HOST / AEM_HTTPS_PROXY_HOST
AEM_HTTP_PROXY_PORT / AEM_HTTPS_PROXY_PORT
```

Por ejemplo, este es un ejemplo de código para enviar una solicitud a `www.example.com:8443`:

```java
String url = "www.example.com:8443"
String proxyHost = System.getenv("AEM_HTTPS_PROXY_HOST");
int proxyPort = Integer.parseInt(System.getenv("AEM_HTTPS_PROXY_PORT"));

HttpClient client = HttpClient.newBuilder()
      .proxy(ProxySelector.of(new InetSocketAddress(proxyHost, proxyPort)))
      .build();
 
HttpRequest request = HttpRequest.newBuilder().uri(URI.create(url)).build();
HttpResponse<String> response = client.send(request, BodyHandlers.ofString());
```

Si utiliza bibliotecas de red Java no estándar, configure los proxies con las propiedades anteriores para todo el tráfico.

El tráfico no HTTP/S con destinos a través de puertos declarados en el parámetro `portForwards` debe hacer referencia a una propiedad denominada `AEM_PROXY_HOST`, junto con el puerto asignado. Por ejemplo:

```java
DriverManager.getConnection("jdbc:mysql://" + System.getenv("AEM_PROXY_HOST") + ":53306/test");
```

<table>
<thead>
  <tr>
    <th>Tráfico</th>
    <th>Condición de destino</th>
    <th>Puerto </th>
    <th>Conexión</th>
    <th>Ejemplo de destino externo</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td><b>Protocolo HTTP o HTTPS</b></td>
    <td>Tráfico a Azure o servicios de Adobe</td>
    <td>Cualquiera</td>
    <td>A través de las IP del clúster compartido (no la IP dedicada)</td>
    <td>adobe.io<br>api.windows.net</td>
  </tr>
  <tr>
    <td></td>
    <td>El host que coincide con el parámetro <code>nonProxyHosts</code></td>
    <td>80 o 443</td>
    <td>A través de las IP del clúster compartido</td>
    <td></td>
  </tr>
  <tr>
    <td></td>
    <td>El host que coincide con el parámetro <code>nonProxyHosts</code></td>
    <td>Puertos fuera de 80 o 443</td>
    <td>Bloqueado</td>
    <td></td>
  </tr>
  <tr>
    <td></td>
    <td>A través de la configuración de proxy HTTP, configurada de forma predeterminada para el tráfico HTTP que utiliza la biblioteca de cliente HTTP estándar de Java</td>
    <td>Cualquiera</td>
    <td>A través de la IP de salida dedicada</td>
    <td></td>
  </tr>
  <tr>
    <td></td>
    <td>Omite la configuración proxy HTTP (por ejemplo, si se elimina explícitamente de la biblioteca de cliente HTTP de Java estándar o si se utiliza una biblioteca Java que ignora la configuración proxy estándar)</td>
    <td>80 o 443</td>
    <td>A través de las IP del clúster compartido</td>
    <td></td>
  </tr>
  <tr>
    <td></td>
    <td>Omite la configuración proxy HTTP (por ejemplo, si se elimina explícitamente de la biblioteca de cliente HTTP de Java estándar o si se utiliza una biblioteca Java que ignora la configuración proxy estándar)</td>
    <td>Puertos fuera de 80 o 443</td>
    <td>Bloqueado</td>
    <td></td>
  </tr>
  <tr>
    <td><b>No HTTP o no HTTPS</b></td>
    <td>El cliente se conecta a <code>AEM_PROXY_HOST</code> la variable env usando un <code>portOrig</code> declarado en el <code>portForwards</code> parámetro de la API</td>
    <td>Cualquiera</td>
    <td>A través de la IP de salida dedicada</td>
    <td><code>mysql.example.com:3306</code></td>
  </tr>
  <tr>
    <td></td>
    <td>Cualquier otra cosa</td>
    <td></td>
    <td>Bloqueado</td>
    <td></td>
  </tr>
</tbody>
</table>

## Clientes de direcciones de salida dedicadas heredadas {#legacy-dedicated-egress-address-customers}

Si se le ha aprovisionado con una IP de salida dedicada antes del 30 de septiembre de 2021, su función de IP de salida dedicada funciona como se describe a continuación.

### Uso de las funciones {#feature-usage}

La función es compatible con el código Java o las bibliotecas que resultan en tráfico saliente, siempre que utilicen propiedades estándar del sistema Java para las configuraciones de proxy. En la práctica, esto debería incluir las bibliotecas más comunes.

A continuación se muestra un ejemplo de código:

```java
public JSONObject getJsonObject(String relativePath, String queryString) throws IOException, JSONException {
  String relativeUri = queryString.isEmpty() ? relativePath : (relativePath + '?' + queryString);
  URL finalUrl = endpointUri.resolve(relativeUri).toURL();
  URLConnection connection = finalUrl.openConnection();
  connection.addRequestProperty("Accept", "application/json");
  connection.addRequestProperty("X-API-KEY", apiKey);

  try (InputStream responseStream = connection.getInputStream(); Reader responseReader = new BufferedReader(new InputStreamReader(responseStream, Charsets.UTF_8))) {
    return new JSONObject(new JSONTokener(responseReader));
  }
}
```

Algunas bibliotecas requieren una configuración explícita para utilizar las propiedades estándar del sistema Java en las configuraciones de proxy.

Ejemplo con Apache HttpClient, que requiere llamadas explícitas a
[`HttpClientBuilder.useSystemProperties()`](https://hc.apache.org/httpcomponents-client-4.5.x/current/httpclient/apidocs/org/apache/http/impl/client/HttpClientBuilder.html) o usar
[`HttpClients.createSystem()`](https://hc.apache.org/httpcomponents-client-4.5.x/current/httpclient/apidocs/org/apache/http/impl/client/HttpClients.html#createSystem()):

```java
public JSONObject getJsonObject(String relativePath, String queryString) throws IOException, JSONException {
  String relativeUri = queryString.isEmpty() ? relativePath : (relativePath + '?' + queryString);
  URL finalUrl = endpointUri.resolve(relativeUri).toURL();

  HttpClient httpClient = HttpClientBuilder.create().useSystemProperties().build();
  HttpGet request = new HttpGet(finalUrl.toURI());
  request.setHeader("Accept", "application/json");
  request.setHeader("X-API-KEY", apiKey);
  HttpResponse response = httpClient.execute(request);
  String result = EntityUtils.toString(response.getEntity());
}
```

La misma IP dedicada se aplica a todos los programas de un cliente en su organización de Adobe y a todos los entornos de cada uno de sus programas. Se aplica tanto a los servicios de creación como de publicación.

Solo se admiten puertos HTTP y HTTPS. Esto incluye HTTP/1.1 y HTTP/2 cuando se cifran.

### Consideraciones sobre la depuración {#debugging-considerations}

Para validar que el tráfico es realmente saliente en la dirección IP dedicada esperada, compruebe los registros en el servicio de destino, si está disponible. De lo contrario, puede resultar útil llamar a un servicio de depuración como [https://ifconfig.me/IP](https://ifconfig.me/IP), que devolverá la dirección IP que realiza la llamada.

## Red privada virtual (VPN) {#vpn}

Una VPN permite conectarse a una infraestructura o centro de datos local desde la creación, publicación o previsualización. Por ejemplo, para los medios de acceso a una base de datos.

También permite conectarse a proveedores de SaaS, como un proveedor CRM que admite VPN o conectarse desde una red corporativa a AEM as a Cloud Service para crear, previsualizar o publicar.

La mayoría de los dispositivos VPN con tecnología IPSec son compatibles. Consulte la lista de dispositivos en [esta página](https://docs.microsoft.com/es-es/azure/vpn-gateway/vpn-gateway-about-vpn-devices#devicetable), según la información de la columna **Instrucciones de configuración de RouteBased**. Configure el dispositivo como se describe en la tabla.

### Consideraciones generales {#general-vpn-considerations}

* La compatibilidad se limita a una única conexión VPN
* La capacidad de reenvío de Splunk no es posible a través de una conexión VPN.

### Creación {#vpn-creation}

Una vez por programa, el punto final POST `/program/<programId>/networkInfrastructures` se invoca, pasando una carga útil de información de configuración que incluye: el valor de “vpn” para el parámetro `kind`, región, espacio de dirección (lista de CIDR; tenga en cuenta que esto no se puede modificar más adelante), resolución de DNS (para resolver nombres en la red del cliente) e información de conexión VPN, como configuración de puerta de enlace, clave VPN compartida y política de seguridad IP. El punto final responde con `network_id`, así como otra información, incluido el estado. Se debe hacer referencia al conjunto completo de parámetros y a la sintaxis exacta en la [Documentación de la API](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/#operation/createNetworkInfrastructure).

Una vez realizada la llamada, la infraestructura de red tarda normalmente entre 45 y 60 minutos en aprovisionarse. Se puede llamar al método GET de la API para devolver el estado actual, que finalmente cambiará de `creating` a `ready`. Consulte la documentación de la API para todos los estados.

Si la configuración de VPN con alcance de programa está lista, el `PUT /program/<program_id>/environment/<environment_id>/advancedNetworking` punto de conexión debe invocarse por entorno para habilitar la red en el nivel de entorno y para declarar cualquier regla de reenvío de puerto. Los parámetros se pueden configurar por entorno para ofrecer flexibilidad.

Consulte la [Documentación de la API](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/#operation/enableEnvironmentAdvancedNetworkingConfiguration) para obtener más información.

Las reglas de reenvío de puertos deben declararse para cualquier tráfico TCP de protocolo no HTTP/S que deba enrutarse a través de la VPN especificando el conjunto de hosts de destino (nombres o IP, y con puertos). Para cada host de destino, los clientes deben asignar el puerto de destino deseado a un puerto entre 30000 y 30999, donde los valores deben ser únicos en los entornos del programa. Los clientes también pueden enumerar un conjunto de direcciones URL en el parámetro `nonProxyHosts`, que declara la dirección URL para la que el tráfico debe evitar el enrutamiento VPN, pero en su lugar a través de un intervalo IP compartido. Sigue los patrones de `example.com` o `*.example.com`, donde el carácter comodín solo se admite al principio del dominio.

La API debe responder en solo unos segundos, indicando un estado de `updating` y después de unos 10 minutos, una llamada al punto de conexión GET de entorno de Cloud Manager mostraría un estado de `ready`, con lo que indica que se ha aplicado la actualización al entorno.

Tenga en cuenta que aunque no haya reglas de enrutamiento de tráfico de entorno (hosts o bypass), `PUT /program/<program_id>/environment/<environment_id>/advancedNetworking` debe llamarse, solo con una carga útil vacía.

### Actualización de la VPN {#updating-the-vpn}

La configuración de VPN en el nivel de programa se puede actualizar invocando el punto de conexión `PUT /api/program/<program_id>/network/<network_id>`.

Tenga en cuenta que el espacio de direcciones no se puede cambiar después del aprovisionamiento de VPN inicial. Si es necesario, póngase en contacto con Asistencia al cliente. Además, el parámetro `kind` (`flexiblePortEgress`, `dedicatedEgressIP` o `VPN`) no se puede modificar. Póngase en contacto con la asistencia al cliente para obtener ayuda; describa lo que ya se ha creado y el motivo del cambio.

Las reglas de enrutamiento por entorno se pueden actualizar invocando de nuevo el punto de conexión `PUT /program/{programId}/environment/{environmentId}/advancedNetworking`. Asegúrese de incluir el conjunto completo de parámetros de configuración en lugar de un subconjunto. Las actualizaciones de entorno suelen tardar entre 5 y 10 minutos en aplicarse.

### Eliminación o desactivación de la VPN {#deleting-or-disabling-the-vpn}

Para eliminar la infraestructura de red, envíe un ticket de asistencia al cliente en el que se describa lo que se ha creado y por qué debe eliminarse.

Para desactivar la VPN para un entorno en particular, invoque `DELETE /program/{programId}/environment/{environmentId}/advancedNetworking`. Más detalles en la [Documentación de la API](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/#operation/disableEnvironmentAdvancedNetworkingConfiguration).

### Enrutamiento del tráfico {#vpn-traffic-routing}

La siguiente tabla describe el enrutamiento de tráfico.

<table>
<thead>
  <tr>
    <th>Tráfico</th>
    <th>Condición de destino</th>
    <th>Puerto </th>
    <th>Conexión</th>
    <th>Ejemplo de destino externo</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td><b>Protocolo HTTP o HTTPS</b></td>
    <td>Tráfico a Azure o servicios de Adobe</td>
    <td>Cualquiera</td>
    <td>A través de las IP del clúster compartido (no la IP dedicada)</td>
    <td>adobe.io<br>api.windows.net</td>
  </tr>
  <tr>
    <td></td>
    <td>El host que coincide con el parámetro <code>nonProxyHosts</code></td>
    <td>80 o 443</td>
    <td>A través de las IP del clúster compartido</td>
    <td></td>
  </tr>
  <tr>
    <td></td>
    <td>El host que coincide con el parámetro <code>nonProxyHosts</code></td>
    <td>Puertos fuera de 80 o 443</td>
    <td>Bloqueado</td>
    <td></td>
  </tr>
  <tr>
    <td></td>
    <td>Si la IP se encuentra en el intervalo de espacio <i>dirección de puerta de enlace VPN</i> y a través de la configuración de proxy HTTP (configurada de forma predeterminada para el tráfico HTTP/S que utiliza la biblioteca de cliente HTTP estándar de Java)</td>
    <td>Cualquiera</td>
    <td>A través de la VPN</td>
    <td><code>10.0.0.1:443</code>También puede ser un nombre de host.</td>
  </tr>
  <tr>
    <td></td>
    <td>Si la IP no cae en el intervalo <i>espacio de direcciones de puerta de enlace VPN</i> y a través de la configuración proxy HTTP (configurada de forma predeterminada para el tráfico HTTP/S mediante la biblioteca de cliente HTTP estándar de Java)</td>
    <td>Cualquiera</td>
    <td>A través de la IP de salida dedicada</td>
    <td></td>
  </tr>
  <tr>
    <td></td>
    <td>Omite la configuración proxy HTTP (por ejemplo, si se elimina explícitamente de la biblioteca de cliente HTTP de Java estándar o si se utiliza la biblioteca Java que ignora la configuración proxy estándar)
</td>
    <td>80 o 443</td>
    <td>A través de las IP del clúster compartido</td>
    <td></td>
  </tr>
  <tr>
    <td></td>
    <td>Omite la configuración proxy HTTP (por ejemplo, si se elimina explícitamente de la biblioteca de cliente HTTP de Java estándar o si se utiliza la biblioteca Java que ignora la configuración proxy estándar)</td>
    <td>Puertos fuera de 80 o 443</td>
    <td>Bloqueado</td>
    <td></td>
  </tr>
  <tr>
    <td><b>No HTTP o no HTTPS</b></td>
    <td>Si la IP se encuentra en el intervalo <i>espacio de direcciones de puerta de enlace VPN</i> y el cliente se conecta a la variable env <code>AEM_PROXY_HOST</code> usando un <code>portOrig</code> declarado en el parámetro de API <code>portForwards</code></td>
    <td>Cualquiera</td>
    <td>A través de la VPN</td>
    <td><code>10.0.0.1:3306</code>También puede ser un nombre de host.</td>
  </tr>
  <tr>
    <td></td>
    <td>Si la IP no cae en el intervalo <i>espacio de direcciones de puerta de enlace VPN</i> y el cliente se conecta a la variable env <code>AEM_PROXY_HOST</code> usando un <code>portOrig</code> declarado en el parámetro de API <code>portForwards</code></td>
    <td>Cualquiera</td>
    <td>A través de la IP de salida dedicada</td>
    <td></td>
  </tr>
  <tr>
    <td></td>
    <td>Cualquier otra cosa</td>
    <td>Cualquiera</td>
    <td>Bloqueado</td>
    <td></td>
  </tr>
</tbody>
</table>

### Dominios útiles para la configuración {#vpn-useful-domains-for-configuration}

El diagrama siguiente proporciona una representación visual de un conjunto de dominios e IP asociadas que son útiles para la configuración y el desarrollo. La tabla siguiente debajo del diagrama describe esos dominios y direcciones IP.

![Configuración del dominio VPN](/help/security/assets/AdvancedNetworking.jpg)

<table>
<thead>
  <tr>
    <th>Patrón de dominio</th>
    <th>Significado de la salida (de AEM)</th>
    <th>Significado del ingreso (a AEM)</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td><code>p{PROGRAM_ID}.external.adobeaemcloud.com</code></td>
    <td>La dirección IP de salida dedicada para el tráfico que va a Internet en lugar de a través de redes privadas </td>
    <td>Las conexiones desde la VPN se mostrarían en la red de distribución de contenido (CDN) como procedentes de esta IP. Para permitir que solo las conexiones desde la VPN entren en AEM, configure Cloud Manager para permitir solo esta IP y bloquear todo lo demás. Consulte la sección Restringir el ingreso a conexiones VPN para obtener más información.</td>
  </tr>
  <tr>
    <td><code>p{PROGRAM_ID}-gateway.external.adobeaemcloud.com</code></td>
    <td>N/D</td>
    <td>IP de la puerta de enlace VPN en el lado AEM. El equipo de ingeniería de redes de un cliente puede utilizarlo para permitir únicamente conexiones VPN a su puerta de enlace VPN desde una dirección IP específica. </td>
  </tr>
  <tr>
    <td><code>p{PROGRAM_ID}.inner.adobeaemcloud.net</code></td>
    <td>IP del tráfico proveniente del lado AEM de la VPN al lado del cliente. Esto puede verse incluido en la lista de permitidos en la configuración del cliente para garantizar que las conexiones solo se puedan realizar desde AEM.</td>
    <td>Si el cliente desea permitir solamente el acceso de VPN a AEM, debe configurar las entradas DNS CNAME para asignar <code>author-p{PROGRAM_ID}-e{ENVIRONMENT_ID}.adobeaemcloud.com</code> o <code>publish-p{PROGRAM_ID}-e{ENVIRONMENT_ID}.adobeaemcloud.com</code> a esto.</td>
  </tr>
</tbody>
</table>

### Restricción de VPN a conexiones de ingesta {#restrict-vpn-to-ingress-connections}

Si desea permitir solo el acceso VPN a AEM, las listas de permitidos de entorno se pueden configurar en Cloud Manager para que solo la IP definida por `p{PROGRAM_ID}.external.adobeaemcloud.com` pueda hablar con el entorno. Esto se puede hacer de la misma manera que cualquier otra lista de permitidos basada en IP en Cloud Manager.

Si las reglas deben basarse en rutas, utilice directivas HTTP estándar en el nivel de Dispatcher para denegar o permitir determinadas IP. Deben asegurarse de que las rutas deseadas no se puedan almacenar en caché en la CDN para que la solicitud siempre llegue al origen.

**Ejemplo de configuración Httpd**

```
Order deny,allow
Deny from all
Allow from 192.168.0.1
Header always set Cache-Control private
```

## Transición entre tipos de redes avanzadas {#transitioning-between-advanced-networking-types}

Dado que el parámetro `kind` no se puede modificar, póngase en contacto con el servicio de asistencia al cliente para obtener ayuda, y describa lo que ya se ha creado y el motivo del cambio.
