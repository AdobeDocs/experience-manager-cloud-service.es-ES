---
title: Configuración de redes avanzadas para AEM as a Cloud Service
description: Aprenda a configurar funciones de red avanzadas como VPN o dirección IP de salida dedicada para AEM as a Cloud Service
source-git-commit: d37193833d784f3f470780b8f28e53b473fd4e10
workflow-type: tm+mt
source-wordcount: '2797'
ht-degree: 1%

---


# Configuración de redes avanzadas para AEM as a Cloud Service {#configuring-advanced-networking}

>[!INFO]
>
>La función de red avanzada forma parte de la versión 2021.9.0 y estará habilitada para los clientes a mediados de octubre.

AEM as a Cloud Service ofrece varios tipos de funciones de red avanzadas, que los clientes pueden configurar mediante las API de Cloud Manager. Entre estas características se incluyen:

* [Salida de puerto flexible](#flexible-port-egress) : configure AEM as a Cloud Service para permitir el tráfico saliente desde puertos no estándar
* [Dirección IP de salida dedicada](#dedicated-egress-IP-address) : configure el tráfico de AEM as a Cloud Service a partir de una IP única
* [Red privada virtual](#vpn) : tráfico seguro entre la infraestructura de un cliente y AEM as a Cloud Service, para clientes que tienen tecnología VPN

Este artículo describe cada una de estas opciones en detalle, incluido cómo se pueden configurar. Como estrategia de configuración general, el extremo de la API `/networkInfrastructures` se invoca a nivel de programa para declarar el tipo deseado de red avanzada, seguido de una llamada al extremo `/advancedNetworking` para cada entorno para habilitar la infraestructura y configurar parámetros específicos del entorno. Consulte los extremos adecuados en la documentación de la API de Cloud Manager para cada sintaxis formal, así como las solicitudes y respuestas de ejemplo.

Al decidir entre una salida de puerto flexible y una dirección IP de salida dedicada, se recomienda elegir una salida de puerto flexible si no se requiere una dirección IP específica, ya que el Adobe puede optimizar el rendimiento del tráfico de salida de puerto flexible.

>[!INFO]
>
>La red avanzada no está disponible para el programa de simulación de pruebas.

>[!NOTE]
>
>Los clientes que ya dispongan de tecnología de salida dedicada heredada y que necesiten configurar una de estas opciones no deben hacerlo o la conectividad del sitio puede verse afectada. Póngase en contacto con el servicio de asistencia al Adobe para obtener ayuda.

## Salida de puerto flexible {#flexible-port-egress}

Esta función de red avanzada le permite configurar AEM as a Cloud Service para recibir tráfico a través de puertos que no sean HTTP (puerto 80) y HTTPS (puerto 443), que están abiertos de forma predeterminada.

### Consideraciones {#flexible-port-egress-considerations}

La salida de puerto flexible es la opción recomendada si no necesita VPN y no necesita una dirección IP de salida dedicada, ya que el tráfico que no depende de una salida dedicada puede obtener un mayor rendimiento.

### Configuración {#configuring-flexible-port-egress-provision}

Una vez por programa, se invoca el extremo `/program/<programId>/networkInfrastructures` del POST, pasando simplemente el valor de `flexiblePortEgress` para el parámetro `kind` y la región. El extremo responde con `network_id`, así como con otra información que incluye el estado. Se debe hacer referencia al conjunto completo de parámetros y a la sintaxis exacta en los documentos de API.

Una vez realizada la llamada, la infraestructura de red tarda aproximadamente 15 minutos en aprovisionarse. Una llamada al extremo [environment GET](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/#operation/getEnvironment) de Cloud Manager mostraría un estado &quot;listo&quot;.

Si la configuración de salida de puerto flexible con ámbito de programa está lista, se debe invocar el extremo `PUT /program/<program_id>/environment/<environment_id>/advancedNetworking` por entorno para habilitar la red a nivel de entorno y declarar cualquier regla de reenvío de puerto. Los parámetros se pueden configurar por entorno para ofrecer flexibilidad.

Las reglas de reenvío de puertos deben declararse para cualquier puerto que no sea 80/443 especificando el conjunto de hosts de destino (nombres o IP, y con puertos). Para cada host de destino, los clientes deben asignar el puerto de destino deseado a un puerto desde 30000 hasta 30999.

La API debe responder en solo unos segundos, indicando un estado de actualización y después de unos 10 minutos, el método `GET` del extremo debe indicar que la red avanzada está habilitada.

### Actualizaciones {#updating-flexible-port-egress-provision}

La configuración a nivel de programa se puede actualizar invocando el extremo `PUT /api/program/<program_id>/network/<network_id>` y tendrá efecto en unos minutos.

>[!NOTE]
>
> El parámetro &quot;amable&quot; (`flexiblePortEgress`, `dedicatedEgressIP` o `VPN`) no se puede modificar. Póngase en contacto con el servicio de atención al cliente para obtener ayuda, describiendo lo que ya se ha creado y el motivo del cambio.

Las reglas de reenvío de puertos por entorno se pueden actualizar invocando de nuevo el extremo `PUT /program/{programId}/environment/{environmentId}/advancedNetworking` , asegurándose de incluir el conjunto completo de parámetros de configuración en lugar de un subconjunto.

### Eliminación o desactivación de la salida de puerto flexible {#deleting-disabling-flexible-port-egress-provision}

Para **eliminar** la infraestructura de red, envíe un ticket de asistencia al cliente en el que se describa lo que se ha creado y por qué debe eliminarse.

Para **deshabilitar** salida de puerto flexible desde un entorno en particular, invoque `DELETE [/program/{programId}/environment/{environmentId}/advancedNetworking]()`.

Para obtener más información, consulte la [documentación de la API de Cloud Manager](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/#operation/disableEnvironmentAdvancedNetworkingConfiguration).

### Enrutamiento de tráfico {#flexible-port-egress-traffic-routing}

El tráfico HTTP o https que va a destinos a través de los puertos 80 o 443 pasará a través de un proxy preconfigurado, suponiendo que se utilice la biblioteca de red Java estándar. Para el tráfico http o https que pasa por otros puertos, un proxy debe configurarse con las siguientes propiedades.

* `AEM_HTTP_PROXY_HOST / AEM_HTTPS_PROXY_HOST`
* `AEM_HTTP_PROXY_PORT / AEM_HTTPS_PROXY_PORT`

Por ejemplo, este es un ejemplo de código para enviar una solicitud a `www.example.com:8443`:

```java
HttpsHost target = new HttpsHost("example.com", 8443, "https");
 
HttpHost proxy = new HttpHost(System.getenv("AEM_HTTPS_PROXY_HOST"),
                              Integer.parseInt(System.getenv("AEM_HTTPS_PROXY_PORT")),
                              "https");
 
RequestConfig config = RequestConfig.custom().setProxy(proxy).build();
 
HttpGet request = new HttpGet("/");
request.setConfig(config);
CloseableHttpResponse response = httpclient.execute(target, request);
```

Si utiliza bibliotecas de red Java no estándar, configure los proxies con las propiedades anteriores para todo el tráfico.

El tráfico no http/s con destinos a través de puertos declarados en el parámetro `portForwards` debe hacer referencia a una propiedad denominada `AEM_PROXY_HOST`, junto con el puerto asignado. Por ejemplo:

```java
DriverManager.getConnection("jdbc:mysql://" + System.getenv("AEM_PROXY_HOST") + ":53306/test");
```

La siguiente tabla describe el enrutamiento de tráfico:

<table>
<thead>
  <tr>
    <th>Tráfico</th>
    <th>Condición de desconexión</th>
    <th>Puerto</th>
    <th>Conexión</th>
    <th>Ejemplo</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td><b>Protocolo Http o https</b></td>
    <td>Tráfico http estándar</td>
    <td>80 o 443</td>
    <td>Permitido</td>
    <td></td>
  </tr> 
  <tr>
    <td></td>
    <td>Tráfico no estándar (en otros puertos fuera de 80 o 443) a través del proxy http configurado mediante estas variables de entorno:<br><ul>
     <li>AEM_HTTP_PROXY_HOST/AEM_HTTPS_PROXY_HOST</li>
     <li>AEM_HTTP_PROXY_PORT / AEM_HTTPS_PROXY_PORT</li>
    </ul>
    <td>Puertos fuera de 80 o 443</td>
    <td>Permitido</td>
  </tr>
  <tr>
    <td></td>
    <td>El tráfico no estándar (en otros puertos fuera de los puertos 80 o 443) no utiliza el proxy http</td>
    <td>Puertos fuera de 80 o 443</td>
    <td>Bloqueado</td>
    <td></td>
  </tr>
  <tr>
    <td><b>No http o no https</b></td>
    <td>El cliente se conecta a la variable de entorno <code>AEM_PROXY_HOST</code> utilizando una <code>portOrig</code> declarada en el parámetro de API <code>portForwards</code>.</td>
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

La directiva `mod_proxy` del nivel de AEM Cloud Service Apache/Dispatcher se puede configurar utilizando las propiedades descritas anteriormente.

```
ProxyRemote "http://example.com" "http://${AEM_HTTP_PROXY_HOST}:${AEM_HTTP_PROXY_PORT}"
ProxyPass "/somepath" "http://example.com"
ProxyPassReverse "/somepath" "http://example.com"
```

```
SSLProxyEngine on //needed for https backends
 
ProxyRemote "https://example.com:8443" "http://${AEM_HTTPS_PROXY_HOST}:${AEM_HTTPS_PROXY_PORT}"
ProxyPass "/somepath" "https://example.com:8443"
ProxyPassReverse "/somepath" "https://example.com:8443"
```

## Dirección IP de salida dedicada {#dedicated-egress-IP-address}

>[!NOTE]
>
>Si se le ha proporcionado una IP de salida dedicada antes de la versión de septiembre de 2021 (6/10/21), consulte [Clientes de direcciones de salida dedicadas heredadas](#legacy-dedicated-egress-address-customers).

### Ventajas {#benefits}

Esta dirección IP dedicada puede mejorar la seguridad al integrarse con proveedores de SaaS (como un proveedor CRM) u otras integraciones fuera de AEM as a Cloud Service que ofrecen una lista de permitidos de direcciones IP. Al agregar la dirección IP dedicada a la lista de permitidos, se garantiza que solo el tráfico de AEM Cloud Service del cliente pueda fluir al servicio externo. Esto se suma al tráfico de cualquier otra IP permitida.

Sin la función de dirección IP dedicada habilitada, el tráfico proveniente de AEM flujos as a Cloud Service a través de un conjunto de IP compartidas con otros clientes.

### Configuración {#configuring-dedicated-egress-provision}

>[!INFO]
>
>La capacidad de reenvío de Splunk no es posible desde una dirección IP de salida dedicada.

La configuración de la dirección IP de salida dedicada es idéntica a la [salida de puerto flexible](#configuring-flexible-port-egress-provision).

La principal diferencia es que el tráfico siempre saldrá de una IP única y dedicada. Para encontrar esa IP, utilice un solucionador DNS para identificar la dirección IP asociada con `p{PROGRAM_ID}.external.adobeaemcloud.com`. No se espera que la dirección IP cambie, pero si necesita cambiarla en el futuro, se proporcionará una notificación avanzada.

Además de las reglas de enrutamiento admitidas por la salida de puerto flexible en el extremo `PUT /program/<program_id>/environment/<environment_id>/advancedNetworking` , la dirección IP de salida dedicada admite un parámetro `nonProxyHosts`. Esto le permite declarar un conjunto de hosts que deben enrutarse a través de un intervalo de direcciones IP compartidas en lugar de la IP dedicada, lo que puede resultar útil, ya que la salida de tráfico a través de direcciones IP compartidas puede optimizarse aún más. Las direcciones URL `nonProxyHost` pueden seguir los patrones de `example.com` o `*.example.com`, donde el comodín solo se admite al principio del dominio.

Al decidir entre una salida de puerto flexible y una dirección IP de salida dedicada, los clientes deben elegir una salida de puerto flexible si no se requiere una dirección IP específica, ya que el Adobe puede optimizar el rendimiento del tráfico de salida de puerto flexible.

### Enrutamiento de tráfico {#dedcated-egress-ip-traffic-routing}

<table>
<thead>
  <tr>
    <th>Tráfico</th>
    <th>Condición de destino</th>
    <th>Puerto</th>
    <th>Conexión</th>
    <th>Ejemplo</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td><b>Protocolo Http o https</b></td>
    <td>Tráfico a Azure o servicios de Adobe</td>
    <td>Cualquiera</td>
    <td>A través de las IP del clúster compartido (no la IP dedicada)</td>
    <td>adobe.io<br>api.windows.net</td>
  </tr>
  <tr>
    <td></td>
    <td>Host que coincide con el parámetro <code>nonProxyHosts</code></td>
    <td>80 o 443</td>
    <td>A través de las IP del clúster compartido</td>
    <td></td>
  </tr>
  <tr>
    <td></td>
    <td>Host que coincide con el parámetro <code>nonProxyHosts</code></td>
    <td>Puertos fuera de 80 o 443</td>
    <td>Bloqueado</td>
    <td></td>
  </tr>
  <tr>
    <td></td>
    <td>A través de la configuración de proxy http, configurada de forma predeterminada para el tráfico http que utiliza la biblioteca de cliente HTTP estándar de Java</td>
    <td>Cualquiera</td>
    <td>A través de la IP de salida dedicada</td>
    <td></td>
  </tr>
  <tr>
    <td></td>
    <td>Omite la configuración proxy http (por ejemplo, si se elimina explícitamente de la biblioteca de cliente HTTP de Java estándar o si se utiliza una biblioteca Java que ignora la configuración proxy estándar)</td>
    <td>80 o 443</td>
    <td>A través de las IP del clúster compartido</td>
    <td></td>
  </tr>
  <tr>
    <td></td>
    <td>Omite la configuración proxy http (por ejemplo, si se elimina explícitamente de la biblioteca de cliente HTTP de Java estándar o si se utiliza una biblioteca Java que ignora la configuración proxy estándar)</td>
    <td>Puertos fuera de 80 o 443</td>
    <td>Bloqueado</td>
    <td></td>
  </tr>
  <tr>
    <td><b>No http o no https</b></td>
    <td>El cliente se conecta a la variable env <code>AEM_PROXY_HOST</code> utilizando una <code>portOrig</code> declarada en el parámetro API <code>portForwards</code></td>
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

## Los Auriculares Dedicados Heredados Se Dirigen A Los Clientes {#legacy-dedicated-egress-address-customers}

Si ha sido aprovisionado con una IP de salida dedicada antes de 2021.09.30, su función IP de salida dedicada funcionará como se describe a continuación.

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
[`HttpClientBuilder.useSystemProperties()`](https://hc.apache.org/httpcomponents-client-4.5.x/current/httpclient/apidocs/org/apache/http/impl/client/HttpClientBuilder.html) o use
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

La misma IP dedicada se aplica a todos los programas de un cliente en su organización de Adobe y a todos los entornos de cada uno de sus programas. Se aplica tanto a los servicios de autor como de publicación.

Solo se admiten puertos HTTP y HTTPS. Esto incluye HTTP/1.1 y HTTP/2 cuando se cifran.

### Consideraciones sobre la depuración {#debugging-considerations}

Para validar que el tráfico es realmente saliente en la dirección IP dedicada esperada, compruebe los registros en el servicio de destino, si está disponible. De lo contrario, puede resultar útil llamar a un servicio de depuración como [https://ifconfig.me/IP](https://ifconfig.me/IP), que devolverá la dirección IP que realiza la llamada.

## Red privada virtual (VPN) {#vpn}

VPN permite conectarse a una infraestructura o centro de datos local desde la creación, publicación o previsualización. Por ejemplo, para los medios de acceso a una base de datos.

También permite conectarse a proveedores de SaaS, como un proveedor CRM que admite VPN o conectarse desde una red corporativa para AEM autor as a Cloud Service, obtener una vista previa o publicar.

La mayoría de los dispositivos VPN con tecnología IPSec son compatibles. Consulte la lista de dispositivos en [esta página](https://docs.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-about-vpn-devices#devicetable), según la información de la columna **RouteBased configuration Instructions**. Configure el dispositivo como se describe en la tabla .

### Consideraciones generales {#general-vpn-considerations}

* La compatibilidad se limita a una única conexión VPN
* La capacidad de reenvío de Splunk no es posible a través de una conexión VPN.

### Creación {#vpn-creation}

Una vez por programa, se invoca el extremo `/program/<programId>/networkInfrastructures` del POST, pasando una carga útil de información de configuración que incluye: el valor de &quot;vpn&quot; para el parámetro `kind`, región, espacio de dirección (lista de CIDR: tenga en cuenta que esto no se puede modificar posteriormente), resueltores DNS (para resolver nombres en la red del cliente) e información de conexión VPN, como configuración de puerta de enlace, clave VPN compartida y política de seguridad IP. El extremo responde con `network_id`, así como con otra información que incluye el estado. Se debe hacer referencia al conjunto completo de parámetros y la sintaxis exacta en la [documentación de la API](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/#operation/createNetworkInfrastructure).

Una vez realizada la llamada, la infraestructura de red tarda normalmente entre 45 y 60 minutos en aprovisionarse. Se puede llamar al método de GET de la API para devolver el estado actual, que eventualmente cambiará de `creating` a `ready`. Consulte la documentación de la API para todos los estados.

Si la configuración de VPN con ámbito de programa está lista, se debe invocar el extremo `PUT /program/<program_id>/environment/<environment_id>/advancedNetworking` por entorno para habilitar la red a nivel de entorno y declarar cualquier regla de reenvío de puerto. Los parámetros se pueden configurar por entorno para ofrecer flexibilidad.

Consulte la [documentación de API](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/#operation/enableEnvironmentAdvancedNetworkingConfiguration) para obtener más información.

Las reglas de reenvío de puertos deben declararse para cualquier tráfico TCP de protocolo no http/s que deba enrutarse a través de la VPN especificando el conjunto de hosts de destino (nombres o IP, y con puertos). Para cada host de destino, los clientes deben asignar el puerto de destino deseado a un puerto entre 3000 y 30999, donde los valores deben ser únicos en los entornos del programa. Los clientes también pueden enumerar un conjunto de direcciones URL en el parámetro `nonProxyHosts` , que declara la dirección URL para la cual el tráfico debe evitar el enrutamiento VPN, pero en su lugar a través de un intervalo IP compartido. Sigue los patrones de `example.com` o `*.example.com`, donde el comodín solo se admite al principio del dominio.

La API debe responder en solo unos segundos, indicando un estado de `updating` y después de unos 10 minutos, una llamada al extremo de GET de entorno de Cloud Manager mostraría un estado de `ready`, indicando que se ha aplicado la actualización del entorno.

Tenga en cuenta que incluso si no hay reglas de enrutamiento de tráfico de entorno (hosts o bypass), `PUT /program/<program_id>/environment/<environment_id>/advancedNetworking` debe llamarse, solo con una carga útil vacía.

### Actualización de la VPN {#updating-the-vpn}

La configuración de VPN a nivel de programa se puede actualizar invocando el extremo `PUT /api/program/<program_id>/network/<network_id>` .

Tenga en cuenta que el espacio de direcciones no se puede cambiar después del aprovisionamiento VPN inicial. Si es necesario, póngase en contacto con el servicio de atención al cliente. Además, el parámetro `kind` (`flexiblePortEgress`, `dedicatedEgressIP` o `VPN`) no se puede modificar. Póngase en contacto con el servicio de atención al cliente para obtener ayuda, describiendo lo que ya se ha creado y el motivo del cambio.

Las reglas de enrutamiento por entorno se pueden actualizar invocando de nuevo el extremo `PUT /program/{programId}/environment/{environmentId}/advancedNetworking` , asegurándose de incluir el conjunto completo de parámetros de configuración en lugar de un subconjunto. Las actualizaciones de entorno suelen tardar entre 5 y 10 minutos en aplicarse.

### Eliminación o desactivación de la VPN {#deleting-or-disabling-the-vpn}

Para eliminar la infraestructura de red, envíe un ticket de asistencia al cliente en el que se describa lo que se ha creado y por qué debe eliminarse.

Para deshabilitar VPN para un entorno en particular, invoque `DELETE /program/{programId}/environment/{environmentId}/advancedNetworking`. Más información en la [documentación de API](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/#operation/disableEnvironmentAdvancedNetworkingConfiguration).

### Enrutamiento de tráfico {#vpn-traffic-routing}

La siguiente tabla describe el enrutamiento de tráfico.

<table>
<thead>
  <tr>
    <th>Tráfico</th>
    <th>Condición de destino</th>
    <th>Puerto</th>
    <th>Conexión</th>
    <th>Ejemplo</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td><b>Protocolo Http o https</b></td>
    <td>Tráfico a Azure o servicios de Adobe</td>
    <td>Cualquiera</td>
    <td>A través de las IP del clúster compartido (no la IP dedicada)</td>
    <td>adobe.io<br>api.windows.net</td>
  </tr>
  <tr>
    <td></td>
    <td>Host que coincide con el parámetro <code>nonProxyHosts</code></td>
    <td>80 o 443</td>
    <td>A través de las IP del clúster compartido</td>
    <td></td>
  </tr>
  <tr>
    <td></td>
    <td>Host que coincide con el parámetro <code>nonProxyHosts</code></td>
    <td>Puertos fuera de 80 o 443</td>
    <td>Bloqueado</td>
    <td></td>
  </tr>
  <tr>
    <td></td>
    <td>Si la IP se encuentra en el intervalo de espacio <i>dirección de puerta de enlace VPN</i> y a través de la configuración de proxy http (configurada de forma predeterminada para el tráfico http/s que utiliza la biblioteca de cliente HTTP estándar de Java)</td>
    <td>Cualquiera</td>
    <td>A través de la VPN</td>
    <td><code>10.0.0.1:443</code>También puede ser un nombre de host.</td>
  </tr>
  <tr>
    <td></td>
    <td>Si la IP no está incluida en el intervalo <i>espacio de dirección de puerta de enlace VPN</i> y a través de la configuración de proxy http (configurada de forma predeterminada para el tráfico http/s que utiliza la biblioteca de cliente HTTP estándar de Java)</td>
    <td>Cualquiera</td>
    <td>A través de la IP de salida dedicada</td>
    <td></td>
  </tr>
  <tr>
    <td></td>
    <td>Omite la configuración proxy http (por ejemplo, si se elimina explícitamente de la biblioteca de cliente HTTP de Java estándar o si se utiliza la biblioteca Java que ignora la configuración proxy estándar)
</td>
    <td>80 o 443</td>
    <td>A través de las IP del clúster compartido</td>
    <td></td>
  </tr>
  <tr>
    <td></td>
    <td>Omite la configuración proxy http (por ejemplo, si se elimina explícitamente de la biblioteca de cliente HTTP de Java estándar o si se utiliza la biblioteca Java que ignora la configuración proxy estándar)</td>
    <td>Puertos fuera de 80 o 443</td>
    <td>Bloqueado</td>
    <td></td>
  </tr>
  <tr>
    <td><b>No http o no https</b></td>
    <td>Si la IP se encuentra en el rango <i>VPN gateway address space</i> y el cliente se conecta a la variable env <code>AEM_PROXY_HOST</code> utilizando una <code>portOrig</code> declarada en el parámetro API <code>portForwards</code></td>
    <td>Cualquiera</td>
    <td>A través de la VPN</td>
    <td><code>10.0.0.1:3306</code>También puede ser un nombre de host.</td>
  </tr>
  <tr>
    <td></td>
    <td>Si la IP no está en el rango <i>VPN gateway address space</i> y el cliente se conecta a la variable env <code>AEM_PROXY_HOST</code> utilizando una <code>portOrig</code> declarada en el parámetro de API <code>portForwards</code></td>
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

### Dominios útiles para la configuración{#vpn-useful-domains-for-configuration}

El diagrama siguiente proporciona una representación visual de un conjunto de dominios e IP asociadas que son útiles para la configuración y el desarrollo. La tabla siguiente debajo del diagrama describe esos dominios e direcciones IP.

![Configuración del dominio VPN](/help/security/assets/AdvancedNetworking.jpg)

<table>
<thead>
  <tr>
    <th>Patrón de dominio</th>
    <th>Efecto (de AEM)</th>
    <th>Ingreso (a AEM)</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td><code>p{PROGRAM_ID}.external.adobeaemcloud.com</code></td>
    <td>Dirección IP de salida dedicada para el tráfico que va a Internet en lugar de a través de redes privadas </td>
    <td>Las conexiones desde la VPN se mostrarían en la CDN como procedentes de esta IP. Para permitir que solo las conexiones desde la VPN entren en AEM, configure Cloud Manager para permitir solo esta IP y bloquear todo lo demás. Consulte la sección "Restringir el ingreso a conexiones VPN" para obtener más información.</td>
  </tr>
  <tr>
    <td><code>p{PROGRAM_ID}-gateway.external.adobeaemcloud.com</code></td>
    <td>N/D</td>
    <td>IP de la puerta de enlace VPN en el lado AEM. El equipo de ingeniería de redes de un cliente puede utilizarlo para permitir únicamente conexiones VPN a su puerta de enlace VPN desde una dirección IP específica. </td>
  </tr>
  <tr>
    <td><code>p{PROGRAM_ID}.inner.adobeaemcloud.net</code></td>
    <td>IP del tráfico proveniente del lado AEM de la VPN al lado del cliente. Esto puede verse incluido en la lista de permitidos en la configuración del cliente para garantizar que las conexiones solo se puedan realizar desde AEM.</td>
    <td>Si el cliente desea permitir solamente el acceso VPN a AEM, debe configurar las entradas DNS CNAME para asignar <code>author-p{PROGRAM_ID}-e{ENVIRONMENT_ID}.adobeaemcloud.com</code> y/o <code>publish-p{PROGRAM_ID}-e{ENVIRONMENT_ID}.adobeaemcloud.com</code> a esto.</td>
  </tr>
</tbody>
</table>

### Restringir VPN a conexiones de ingesta {#restrict-vpn-to-ingress-connections}

Si desea permitir solo el acceso VPN a AEM, las listas de permitidos de entorno se pueden configurar en Cloud Manager para que solo la IP definida por `p{PROGRAM_ID}.external.adobeaemcloud.com` pueda hablar con el entorno. Esto se puede hacer de la misma manera que cualquier otra lista de permitidos basada en IP en Cloud Manager.

Si las reglas deben basarse en rutas, utilice directivas http estándar a nivel de Dispatcher para denegar o permitir determinadas IP. Deben asegurarse de que las rutas deseadas no se puedan almacenar en caché en la CDN para que la solicitud siempre llegue al origen.

**Ejemplo De Configuración Httpd**

```
Order deny,allow
Deny from all
Allow from 192.168.0.1
Header always set Cache-Control private
```

## Transición entre tipos de redes avanzadas {#transitioning-between-advanced-networking-types}

Dado que el parámetro `kind` no se puede modificar, póngase en contacto con el servicio de atención al cliente para obtener ayuda, describiendo lo que ya se ha creado y el motivo del cambio.