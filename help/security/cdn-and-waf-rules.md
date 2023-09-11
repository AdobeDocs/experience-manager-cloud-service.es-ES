---
title: Configuración de reglas de filtro de tráfico (con reglas WAF)
description: Usar reglas de filtro de tráfico (con reglas WAF) para filtrar el tráfico
source-git-commit: dc0c7e77bb4bc5423040364202ecac3c59adced0
workflow-type: tm+mt
source-wordcount: '2690'
ht-degree: 2%

---


# Configuración de reglas de filtrado de tráfico (con reglas WAF) para filtrar el tráfico {#configuring-cdn-and-waf-rules-to-filter-traffic}

>[!NOTE]
>
>Esta función aún no está disponible de forma general. Para unirse al programa de usuarios que lo adoptaron por anticipado, envíe un correo electrónico **aemcs-waf-adopter@adobe.com**, incluido el nombre de su organización y el contexto acerca de su interés en la función.

El Adobe intenta mitigar los ataques contra los sitios web de los clientes, pero puede resultar útil filtrar de forma proactiva el tráfico que coincida con ciertos patrones para que el tráfico malicioso no llegue a la aplicación. Los enfoques posibles incluyen:

* Módulos de capa de Apache como `mod_security`
* Configuración de reglas de filtro de tráfico que se implementan en la CDN mediante la canalización de configuración de Cloud Manager

Este artículo describe el enfoque de las reglas de filtro de tráfico. La mayoría de estas reglas bloquean o permiten solicitudes basadas en propiedades de solicitud y encabezados de solicitud, incluidas la IP, las rutas y el agente de usuario. AEM Estas reglas las pueden configurar todos los sitios as a Cloud Service y los clientes de Forms.

Los clientes que conceden licencias para el complemento WAF (cortafuegos de aplicaciones web) también pueden configurar una categoría adicional de reglas denominada &quot;reglas de filtro de tráfico WAF&quot; (o reglas WAF para abreviar). Estas reglas WAF bloquean solicitudes que coinciden con varios patrones conocidos por estar asociados con tráfico malintencionado. Póngase en contacto con el equipo de su cuenta de Adobe para obtener más información sobre las licencias de esta próxima funcionalidad. Tenga en cuenta que no se requiere ninguna licencia adicional durante el programa de adopción anticipada.

Las reglas de filtro de tráfico se pueden implementar en todos los tipos de entornos de nube (RDE, dev, stage, prod) en programas de producción (que no sean de zonas protegidas).

## Configuración {#setup}

1. En primer lugar, cree la siguiente carpeta y estructura de archivos en la carpeta de nivel superior en Git:

   ```
   config/
        cdn/
           cdn.yaml
   ```

1. `cdn.yaml` debe contener metadatos, así como una lista de reglas de filtros de tráfico y reglas WAF.

   ```
   kind: "CDN"
   version: "1"
   envType: "dev"
   data:
     trafficFilters:
       rules:
         ...
   ```

El parámetro &quot;kind&quot; debe configurarse como &quot;CDN&quot; y la versión debe establecerse como la versión de esquema, que actualmente es &quot;1&quot;. Consulte los ejemplos más adelante.


<!-- Two properties -- `envType` and `envId` -- may be included to limit the scope of the rules. The envType property may have values "dev", "stage", or "prod", while the envId property is the environment (e.g., "53245"). This approach is useful if it is desired to have a single configuration pipeline, even if some environments have different rules. However, a different approach could be to have multiple configuration pipelines, each pointing to different repositories or git branches. -->

1. Para configurar las reglas de WAF, WAF debe habilitarse en Cloud Manager, como se describe a continuación para los escenarios de programa nuevos y existentes. Tenga en cuenta que se debe adquirir una licencia independiente para WAF.

   1. Para configurar WAF en un nuevo programa, marque la **Protección WAF-DDOS** casilla de verificación en la **Seguridad** como se muestra a continuación. Continúe siguiendo los pasos descritos en [Agregar programa de producción](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md) para crear su programa

   1. Para configurar WAF en un programa existente, seleccione **Editar programa** siguiendo los pasos descritos en la sección [Edición de programas](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/editing-programs.md) documentación. A continuación, en la **Seguridad** del asistente, puede desmarcar o marcar la opción WAF-DDOS en cualquier momento

1. Para tipos de entorno distintos de RDE, ejecute la canalización de configuración de Cloud Manager, que se puede configurar como se describe a continuación.

   1. En la tarjeta de canalización de la página de inicio de Cloud Manager, seleccione **Agregar canalización de producción** o **Agregar canalización que no sea de producción** para iniciar el asistente agregar canalización
   1. Seleccionar **Canalización de implementación** en la pestaña configuración

      ![Seleccione la opción Canalización de implementación](/help/security/assets/deployment.png)

   1. Asigne un nombre a la canalización y seleccione déclencheur de implementación y, a continuación, seleccione **Continuar**
   1. En el **Código fuente** pestaña, seleccione **Implementación dirigida**, luego seleccione **Configuración**

      ![Seleccionar implementación dirigida](/help/security/assets/target-deployment.png)

   1. Seleccione el repositorio y la rama según sea necesario. Si existe una canalización de configuración para el entorno seleccionado, esta selección está desactivada.

      ![Información general sobre una canalización de configuración](/help/security/assets/config-pipeline.png)

      >[!NOTE]
      >
      > Los usuarios deben iniciar sesión como administrador de implementación para configurar o ejecutar estas canalizaciones.
      > Además, solo puede configurar y ejecutar una canalización de configuración por entorno.

   1. Seleccione **Guardar**. La nueva canalización aparecerá en la tarjeta de canalización y se podrá ejecutar cuando esté lista.
   1. Para RDE, se utilizará la línea de comandos, pero RDE no es compatible en este momento.

## Sintaxis de reglas de filtro de tráfico {#rules-syntax}

Puede configurar `traffic filter rules` para coincidir en patrones como direcciones IP, agente de usuario, encabezados de solicitud, nombre de host, ubicación geográfica y url.

Los clientes que conceden licencias para la oferta WAF también pueden configurar una categoría especial de reglas de filtro de tráfico llamada `WAF traffic filter rules` (o reglas WAF para abreviar) que hacen referencia a uno o más indicadores WAF, que se enumeran en su propia sección a continuación.

Este es un ejemplo de un conjunto de reglas de filtro de tráfico, que también incluye una regla WAF.

```
kind: "CDN"
version: "1"
envType: "dev"
data:
  trafficFilters:
    rules:
      - name: "path-rule"
        when: { reqProperty: path, equals: /block-me }
        action: 
          type: block
      - name: "Enable-SQL-Injection-and-XSS-waf-rules-globally"
        when: { reqProperty: path, like: "*" }
        action:
          type: block
          wafFlags: [ SQLI, XSS]
```

A continuación, se describe el formato de las reglas de filtro de tráfico en el archivo cdn.yaml. Consulte algunos ejemplos en una sección posterior.


| **Propiedad** | **La mayoría de reglas de filtro de tráfico** | **Reglas de filtro de tráfico WAF** | **Tipo** | **Valor predeterminado** | **Descripción** |
|---|---|---|---|---|---|
| name | X | X | `string` | - | El nombre de la regla (64 caracteres, solo puede contener caracteres alfanuméricos y - ) |
| cuando | X | X | `Condition` | - | La estructura básica es:<br><br>`{ <getter>: <value>, <predicate>: <value> }`<br><br>Consulte Sintaxis de la estructura de condiciones a continuación, que describe los captadores, los predicados y cómo combinar varias condiciones. |
| acción | X | X | `Action` | registro | registrar, permitir, bloquear, registrar u objeto de acción El valor predeterminado es registro |
| rateLimit | X |   | `RateLimit` | sin definir | Configuración de limitación de velocidad. La limitación de velocidad está desactivada si no se define.<br><br>Hay una sección independiente más abajo que describe la sintaxis de rateLimit, junto con ejemplos. |

### Estructura de condición {#condition-structure}

Una condición puede ser una condición simple o un grupo de condiciones.

**Condición simple**

Una condición simple está compuesta por un captador y un predicado.

```
{ <getter>: <value>, <predicate>: <value> }
```

**Condiciones de grupo**

Un grupo de condiciones está compuesto por varias condiciones simples o de grupo.

```
<allOf|anyOf>:
  - { <getter>: <value>, <predicate>: <value> }
  - { <getter>: <value>, <predicate>: <value> }
  - <allOf|anyOf>:
    - { <getter>: <value>, <predicate>: <value> }
```

| **Propiedad** | **Tipo** | **Significado** |
|---|---|---|
| **allOf** | `array[Condition]` | **y** operación. true si todas las condiciones enumeradas devuelven true |
| **anyOf** | `array[Condition]` | **o** operación. true si alguna de las condiciones enumeradas devuelve true |

**Getter**

| **Propiedad** | **Tipo** | **Descripción** |
|---|---|---|
| reqProperty | `string` | Solicitar propiedad.<br><br>Uno de: `path` , `queryString`, `method`, `tier`, `domain`, `clientIp`, `clientCountry`<br><br>La propiedad domain es una transformación en minúsculas del encabezado host de la solicitud. Resulta útil para comparaciones de cadenas, por lo que no se pierden coincidencias debido a la distinción entre mayúsculas y minúsculas.<br><br>El `clientCountry` utiliza dos códigos de letras mostrados en [https://en.wikipedia.org/wiki/Regional_indicator_symbol](https://en.wikipedia.org/wiki/Regional_indicator_symbol) |
| reqHeader | `string` | Devuelve el encabezado de la solicitud con el nombre especificado |
| queryParam | `string` | Devuelve el parámetro de consulta con el nombre especificado |
| cookie | `string` | Devuelve una cookie con el nombre especificado |

**Predicado**

| **Propiedad** | **Tipo** | **Significado** |
|---|---|---|
| **igual a** | `string` | true si el resultado del captador es igual al valor proporcionado |
| **doesNotEqual** | `string` | true si el resultado del captador no es igual al valor proporcionado |
| **me gusta** | `string` | true si el resultado del captador coincide con el patrón proporcionado |
| **notLike** | `string` | true si el resultado del captador no coincide con el patrón proporcionado |
| **matches** | `string` | true si el resultado del captador coincide con la regex proporcionada |
| **doesNotMatch** | `string` | true si el resultado del captador no coincide con la expresión regular proporcionada |
| **en** | `array[string]` | true si la lista proporcionada contiene un resultado de captador |
| **notIn** | `array[string]` | true si la lista proporcionada no contiene el resultado del captador |

### Estructura de acción {#action-structure}

Especificado por `action` campo que puede ser una cadena que especifica el tipo de acción (permitir, bloque, registro) y supone los valores predeterminados para todas las demás opciones o un objeto donde el tipo de regla se define mediante `type` campo obligatorio junto con otras opciones aplicables a ese tipo.

**Tipos de acción**

Las acciones se priorizan según sus tipos en la siguiente tabla, en la que se ordena para reflejar el orden en que se ejecutan las acciones:

| **Nombre** | **Propiedades permitidas** | **Significado** |
|---|---|---|
| **permitir** | `wafFlags` (opcional) | si wafFlags no está presente, detiene el procesamiento posterior de la regla y procede a proporcionar la respuesta. Si wafFlags está presente, deshabilita las protecciones WAF especificadas y continúa con el procesamiento de reglas. |
| **bloquear** | `status, wafFlags` (opcional y mutuamente excluyente) | si wafFlags no está presente, devuelve un error HTTP omitiendo todas las demás propiedades, el código de error se define mediante la propiedad status o el valor predeterminado es 406. Si wafFlags está presente, permite protecciones WAF especificadas y continúa con el procesamiento de reglas. |
| **registro** | `wafFlags` (opcional) | registra el hecho de que la regla se activó; de lo contrario, no afecta al procesamiento. wafFlags no tiene ningún efecto |

### Lista de indicadores WAF {#waf-flags-list}

El `wafFlag` La propiedad puede incluir lo siguiente:

| **Identificador de marca** | **Nombre de indicador** | **Descripción** |
|---|---|---|
| SQLI | Inyección SQL | La inyección de SQL es el intento de obtener acceso a una aplicación o de obtener información privilegiada ejecutando consultas de base de datos arbitrarias. |
| PUERTA TRASERA | Puerta Trasera | Una señal de puerta trasera es una solicitud que intenta determinar si hay un archivo de puerta trasera común en el sistema. |
| CMDEXE | Ejecución de comandos | La ejecución de comandos es el intento de obtener control o dañar un sistema objetivo a través de comandos arbitrarios del sistema por medio de la entrada del usuario. |
| XSS | Scripts entre sitios | La ejecución de scripts en sitios múltiples es el intento de apropiarse de la cuenta de un usuario o de una sesión de exploración web mediante código JavaScript malintencionado. |
| TRAVESÍA | Recorrido de directorio | Directory Traversal es el intento de navegar por carpetas privilegiadas a través de un sistema con la esperanza de obtener información confidencial. |
| USERAGENT | Herramientas de ataque | La herramienta de ataque es el uso de software automatizado para identificar vulnerabilidades de seguridad o para intentar explotar una vulnerabilidad descubierta. |
| LOG4J-JNDI | Log4J JNDI | Los ataques JNDI de Log4J intentan explotar el [Vulnerabilidad de Log4Shell](https://en.wikipedia.org/wiki/Log4Shell) presente en las versiones de Log4J anteriores a la 2.16.0 |
| AWS SSRF | AWS-SSRF | La falsificación de solicitudes del lado del servidor (SSRF) es una solicitud que intenta enviar solicitudes realizadas por la aplicación web a sistemas internos de destino. Los ataques SSRF de AWS utilizan SSRF para obtener claves de Amazon Web Service (AWS) y obtener acceso a los bloques de S3 y a sus datos. |
| BHH | Encabezados de salto incorrectos | Los encabezados de salto incorrectos indican un intento de contrabando HTTP a través de un encabezado Transfer-Encoding (TE) o Content-Length (CL) mal formado o un encabezado TE y CL bien formado |
| RUTA ANORMAL | Ruta anormal | Ruta anormal indica que la ruta original difiere de la ruta normalizada (por ejemplo, `/foo/./bar` se normaliza a `/foo/bar`) |
| COMPRIMIDO | Compresión detectada | El cuerpo de la solicitud del POST está comprimido y no se puede inspeccionar. Por ejemplo, si se especifica un encabezado de solicitud &quot;Content-Encoding: gzip&quot; y el cuerpo del POST no es texto sin formato. |
| DOUBLEENCODING | Codificación doble | La codificación doble comprueba la técnica de evasión de los caracteres HTML de codificación doble |
| FORCEFULBROWSING | Exploración forzada | La exploración forzada es el intento fallido de acceder a las páginas de administración |
| NOTUTF8 | Codificación no válida | La codificación no válida puede hacer que el servidor traduzca caracteres malintencionados de una solicitud a una respuesta, lo que provoca una denegación de servicio o XSS |
| JSON-ERROR | Error de codificación de JSON | Un cuerpo de solicitud de POST, PUT o PATCH que se especifica como que contiene JSON dentro del encabezado de solicitud &quot;Content-Type&quot;, pero que contiene errores de análisis de JSON. Esto suele estar relacionado con un error de programación o una solicitud automatizada o maliciosa. |
| MALFORMED-DATA | Datos mal formados en el cuerpo de la solicitud | Un cuerpo de solicitud de POST, PUT o PATCH con un formato incorrecto según el encabezado de solicitud &quot;Content-Type&quot;. Por ejemplo, si se especifica un encabezado de solicitud &quot;Content-Type: application/x-www-form-urlencoded&quot; y contiene un cuerpo de POST que es json. Esto suele ser un error de programación, una solicitud automatizada o maliciosa. Requiere agente 3.2 o superior. |
| SANS | Tráfico IP malintencionado | [Centro de tormentas de Internet SANS](https://isc.sans.edu/) lista de direcciones IP sobre las que se ha informado que han participado en actividades maliciosas |
| SIGSCI-IP | Efecto de red | IP marcada por SignalSciences: siempre que el motor de decisión marque una IP debido a una señal maliciosa, esa IP se propagará a todos los clientes. Las solicitudes posteriores de aquellas direcciones IP que contengan cualquier señal adicional durante la duración del indicador se registran |
| SIN CONTENIDO | Falta el encabezado de solicitud &quot;Content-Type&quot; | Una solicitud de POST, PUT o PATCH que no tiene un encabezado de solicitud &quot;Content-Type&quot;. De forma predeterminada, los servidores de aplicaciones deben suponer &quot;Content-Type: text/plain; charset=us-ascii&quot; en este caso. Es posible que a muchas solicitudes automatizadas y maliciosas les falte &quot;Tipo de contenido&quot;. |
| NOUA | No hay agente de usuario | Muchas solicitudes automatizadas y maliciosas utilizan agentes de usuario falsos o que faltan para dificultar la identificación del tipo de dispositivo que realiza las solicitudes. |
| TORNODO | Tráfico de Tor | Tor es un software que oculta la identidad de un usuario. Un pico en el tráfico de Tor puede indicar que un atacante está tratando de ocultar su ubicación. |
| CENTRO DE DATOS | Tráfico del centro de datos | El tráfico del centro de datos es tráfico no orgánico originado en proveedores de alojamiento identificados. Este tipo de tráfico no suele estar asociado a un usuario final real. |
| NULLBYTE | Byte nulo | Los bytes nulos no suelen aparecer en una solicitud e indican que la solicitud tiene un formato incorrecto y es potencialmente maliciosa. |
| IMPOSTOR | SearchBot Impostor | El impostor de bots de búsqueda es alguien que finge ser un bot de búsqueda de Google o Bing, pero que no es legítimo. Tenga en cuenta que no depende de una respuesta por sí misma, sino que debe resolverse primero en la nube, por lo que no debe utilizarse en una regla pre. |
| PRIVATEFILE | Archivos privados | Los archivos privados suelen ser de naturaleza confidencial, como un Apache `.htaccess` o un archivo de configuración que podría filtrar información confidencial |
| ESCÁNER | Escáner | Identifica los servicios y herramientas de digitalización más populares |
| RESPONSESPLIT | División de respuesta HTTP | Identifica cuándo se envían los caracteres CRLF como entrada a la aplicación para insertar encabezados en la respuesta HTTP |
| XML-ERROR | Error de codificación XML | Un cuerpo de solicitud de POST, PUT o PATCH que se especifica como que contiene XML dentro del encabezado de solicitud &quot;Content-Type&quot;, pero que contiene errores de análisis de XML. Esto suele estar relacionado con un error de programación o una solicitud automatizada o maliciosa. |

## Consideraciones {#considerations}

* Cuando se crean dos reglas en conflicto, las reglas de permiso siempre tienen prioridad sobre las reglas de bloque. Por ejemplo, si crea una regla para bloquear una ruta específica y una regla para permitir una dirección IP específica, se permitirán las solicitudes de esa dirección IP en la ruta bloqueada.

* Si una regla coincide y está bloqueada, la CDN responde con un `406` código de retorno.

* Los archivos de configuración no deben contener secretos, ya que cualquier persona que tenga acceso al repositorio de Git podrá leerlos

## Ejemplos de reglas {#examples}

A continuación se muestran algunos ejemplos de reglas. Consulte la [sección de límite de tarifa](#rules-with-rate-limits) más abajo para ver ejemplos de limitación de velocidad.

**Ejemplo 1**

Esta regla bloquea las solicitudes procedentes de IP 192.168.1.1:

```
kind: "CDN"
version: "1"
envType: "dev"
data:
  trafficFilters:
     rules:
       - name: "block-request-from-ip"
         when: { reqProperty: clientIp, equals: "192.168.1.1" }
         action: 
           type: block
```

**Ejemplo 2**

Esta regla bloquea las solicitudes en la ruta `/helloworld` Al publicar con un agente de usuario que contiene Chrome:

```
kind: "CDN"
version: "1"
envType: "dev"
data:
  trafficFilters:
     rules:
       - name: "block-request-from-chrome-on-path-helloworld-for-publish-tier"
         when: { reqProperty: clientIp, equals: "192.168.1.1" }
           allOf:
            - { reqProperty: path, equals: /helloworld }
            - { reqProperty: tier, equals: publish }
            - { reqHeader: user-agent, matches: '.*Chrome.*'  }
           action: 
             type: block
```

**Ejemplo 3**

Esta regla bloquea las solicitudes que contienen el parámetro de consulta `foo`, pero permite todas las solicitudes procedentes de IP 192.168.1.1:

```
kind: "CDN"
version: "1"
envType: "dev"
data:
  trafficFilters:
    rules:
      - name: "block-request-that-contains-query-parameter-foo"
        when: { queryParam: url-param, equals: foo }
        action: 
          type: block
      - name: "allow-all-requests-from-ip"
        when: { reqProperty: clientIp, equals: 192.168.1.1 }
        action: 
          type: allow
```

**Ejemplo 4**

Esta regla bloquea las solicitudes a la ruta /block-me y bloquea todas las solicitudes que coincidan con un patrón SQLI o XSS:

```
kind: "CDN"
version: "1"
envType: "dev"
data:
  trafficFilters:
    rules:
      - name: "path-rule"
        when: { reqProperty: path, equals: /block-me }
        action: 
          type: block
      - name: "Enable-SQL-Injection-and-XSS-waf-rules-globally"
        when: { reqProperty: path, like: "*" }
        action:
          type: block
          wafFlags: [ SQLI, XSS]
```

**Ejemplo 4**

Esta regla bloquea el acceso a los países OFAC:

```
kind: "CDN"
version: "1"
envType: "dev"
data:
  trafficFilters:
    rules:
      - name: block-ofac-countries
        when:
          allOf:
            - { reqProperty: tier, equals: publish }
            - reqProperty: clientCountry
              in:
                - SY
                - BY
                - MM
                - KP
                - IQ
                - CD
                - SD
                - IR
                - LR
                - ZW
                - CU
                - CI
        action: block
```

## Reglas con límites de velocidad {#rules-with-rate-limits}

A veces es deseable bloquear el tráfico que coincida con una regla solo si la coincidencia supera una determinada tasa a lo largo del tiempo. Configurar un valor para `rateLimit` La propiedad limita la velocidad de las solicitudes que coinciden con la condición de regla.

### Estructura rateLimit {#ratelimit-structure}

| **Propiedad** | **Tipo** | **Predeterminado** | **SIGNIFICADO** |
|---|---|---|---|
| límite | entero de 10 a 10000 | required | Tasa de solicitudes en solicitudes por segundo para las que se activa la regla |
| ventana | enumeración de enteros: 1, 10 o 60 | 10 | Ventana de muestreo en segundos para la que se calcula la tasa de solicitud |
| penalización | entero de 60 a 3600 | 300 (5 minutos) | Período en segundos durante el cual se bloquean las solicitudes de coincidencia (redondeado al minuto más cercano) |

### Ejemplos {#ratelimiting-examples}

**Ejemplo 1**

Esta regla bloquea a un cliente durante 5 m cuando supera los 100 req/seg en los últimos 60 s

```
kind: "CDN"
version: "1"
envType: "dev"
data:
  trafficFilters:
    - name: limit-requests-client-ip
      when:
        reqProperty: path
        like: '*'
      rateLimit:
        limit: 60
        window: 10
        penalty: 300
        groupBy:
          - reqProperty: clientIp
      action: block
```

**Ejemplo 2**

Bloquear solicitudes de 60 segundos en la ruta /crítico/recurso cuando supere los 100 req/s en los últimos 60 segundos

```
kind: "CDN"
version: "1"
envType: "dev"
data:
  trafficFilters:
    rules:
      - name: rate-limit-example
        when: { reqProperty: path, equals: /critical/resource }
        action: 
          type: block
        rateLimit: { limit: 100, window: 60, penalty: 60 }
```

## Registros de CDN {#cdn-logs}

AEM El as a Cloud Service proporciona acceso a los registros de CDN, que son útiles para casos de uso, incluida la optimización de la proporción de visitas de caché y la configuración de reglas de CDN y WAF. Los registros de CDN aparecen en Cloud Manager **Descargar registros** , al seleccionar el servicio de creación o publicación.

La propiedad &quot;rules&quot; describe qué reglas de filtro de tráfico coinciden y tiene el siguiente patrón:

```
"rules": "match=<matching-customer-named-rules-that-are-matched>,waf=<matching-WAF-rules>,action=<action_type>"
```

Por ejemplo:

```
"rules": "match=Block-Traffic-under-private-folder,Enable-SQL-injection-everywhere,waf="SQLI,SANS",action=block"
```

Las reglas se comportan de la siguiente manera:

* el nombre de regla declarado por el cliente de cualquier regla coincidente se enumerará en el atributo matches.
* el atributo action detalla si las reglas tuvieron el efecto de bloquear, permitir o registrar
* si el WAF tiene licencia y está habilitado, el atributo waf enumerará las reglas waf (por ejemplo, SQLI; tenga en cuenta que esto es independiente del nombre declarado por el cliente) que se detectaron, independientemente de si las reglas waf estaban enumeradas en la configuración.
* si no coinciden las reglas declaradas por el cliente ni las reglas waf, la propiedad de atributo rules estará en blanco.

En general, las reglas coincidentes aparecen en la entrada de registro para todas las solicitudes a la CDN, independientemente de si se trata de una visita de CDN, una pasada o una omisión. Sin embargo, las reglas WAF aparecen en la entrada de registro solo para solicitudes a la CDN que se consideran errores o pasadas de CDN, pero no visitas de CDN.

El ejemplo siguiente muestra un ejemplo de cdn.yaml y dos entradas de registro de CDN:


```
kind: "CDN"
version: "1"
envType: "dev"
data:
  trafficFilters:
    rules:
      - name: "path-rule"
        when: { reqProperty: path, equals: /block-me }
        action: block
      - name: "Enable-SQL-Injection-and-XSS-waf-rules-globally"
        when: { reqProperty: path, like: "*" }
        action:
          type: block
          wafFlags: [ SQLI, XSS ]
```

```
{
"timestamp": "2023-05-26T09:20:01+0000",
"ttfb": 19,
"cli_ip": "147.160.230.112",
"cli_country": "CH",
"rid": "974e67f6",
"req_ua": "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/605.1.15 (KHTML, like Gecko) Version/14.0.3 Safari/605.1.15",
"host": "example.com",
"url": "/block-me",
"method": "GET",
"res_ctype": "",
"cache": "PASS",
"status": 406,
"res_age": 0,
"pop": "PAR",
"rules": "match=path-rule,action=blocked"
}
```

```
{
"timestamp": "2023-05-26T09:20:01+0000",
"ttfb": 19,
"cli_ip": "147.160.230.112",
"cli_country": "CH",
"req_ua": "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/605.1.15 (KHTML, like Gecko) Version/14.0.3 Safari/605.1.15",
"rid": "974e67f6",
"host": "example.com",
"url": "/?sqli=%27%29%20UNION%20ALL%20SELECT%20NULL%2CNULL%2CNULL%2CNULL%2CNULL%2CNULL%2CNULL%2CNULL%2CNULL%2CNULL--%20fAPK",
"method": "GET",
"res_ctype": "image/png",
"cache": "PASS",
"status": 406,
"res_age": 0,
"pop": "PAR",
"rules": "match=Enable-SQL-Injection-and-XSS-waf-rules-globally,waf=SQLI,action=blocked"
}
```

### Formato de registro {#cdn-log-format}

A continuación se muestra una lista de los nombres de campo utilizados en los registros de CDN, junto con una breve descripción.

| **Nombre del campo** | **Descripción** |
|---|---|
| *timestamp* | Hora a la que se inició la solicitud, después de la finalización de TLS |
| *ttfb* | Abreviatura de *Tiempo hasta el primer byte*. Intervalo de tiempo entre el inicio de la solicitud hasta el punto en el que el cuerpo de la respuesta comenzó a transmitirse. |
| *cli_ip* | La dirección IP del cliente. |
| *cli_country* | De dos letras [ISO 3166-1](https://en.wikipedia.org/wiki/ISO_3166-1) código de país alfa-2 del país cliente. |
| *librar* | El valor del encabezado de la solicitud que se utiliza para identificar la solicitud de forma exclusiva. |
| *req_ua* | El agente de usuario responsable de realizar una solicitud HTTP determinada. |
| *host* | La autoridad a la que está destinada la solicitud. |
| *url* | La ruta completa, incluidos los parámetros de consulta. |
| *método* | Método HTTP enviado por el cliente, como &quot;GET&quot; o &quot;POST&quot;. |
| *res_ctype* | Tipo de contenido que se utiliza para indicar el tipo de medio original del recurso. |
| *cache* | Estado de la caché. Los valores posibles son HIT, MISS o PASS |
| *status* | El código de estado HTTP como valor entero. |
| *res_age* | Cantidad de tiempo (en segundos) que una respuesta se ha almacenado en caché (en todos los nodos). |
| *hacer explotar* | Centro de datos del servidor de caché de CDN. |
| *reglas* | El nombre de cualquier regla coincidente.<br><br>También indica si la coincidencia resultó en un bloqueo. <br><br>Por ejemplo, &quot;`match=Enable-SQL-Injection-and-XSS-waf-rules-globally,waf=SQLI,action=blocked`&quot;<br><br>Vacío si no coinciden las reglas. |
