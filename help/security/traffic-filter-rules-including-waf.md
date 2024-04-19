---
title: Reglas de filtro de tráfico, incluidas reglas WAF
description: Configuración de las reglas de filtro de tráfico, incluidas las reglas de cortafuegos de aplicación web (WAF)
exl-id: 6a0248ad-1dee-4a3c-91e4-ddbabb28645c
source-git-commit: d210fed56667b307a7a816fcc4e52781dc3a792d
workflow-type: tm+mt
source-wordcount: '3788'
ht-degree: 96%

---


# Reglas de filtro de tráfico, incluidas reglas WAF {#traffic-filter-rules-including-waf-rules}

Las reglas de filtro de tráfico se pueden utilizar para bloquear o permitir solicitudes en la capa CDN, lo que puede resultar útil en situaciones como las siguientes:

* Restricción del acceso a dominios específicos del tráfico interno de la compañía antes del lanzamiento de un nuevo sitio
* Establecimiento de límites de volumen para que sea menos susceptible a los ataques volumétricos DoS
* Cómo impedir que las direcciones IP que se sabe que son malintencionadas apunten a sus páginas

La mayoría de estas reglas de filtro de tráfico están disponibles para todos los clientes de AEM as a Cloud Service Sites y de Forms. Funcionan principalmente en propiedades de solicitud y encabezados de solicitud, incluidos IP, nombre de host, ruta y agente de usuario.

Una subcategoría de reglas de filtro de tráfico requiere una licencia de seguridad mejorada o una licencia de protección WAF-DDoS. Estas potentes reglas se conocen como reglas de filtro de tráfico WAF (cortafuegos de aplicación web) (o reglas WAF para abreviar) y tienen acceso a [Indicadores WAF](#waf-flags-list) que se describen más adelante en este artículo.

Las reglas de filtro de tráfico se pueden implementar mediante canalizaciones de configuración de Cloud Manager para los tipos de entorno de desarrollo, fase y producción en programas de producción (que no sean de zonas protegidas). El soporte para RDE vendrá en el futuro.

[Siga un tutorial](#tutorial) para adquirir rápidamente conocimientos sobre esta funcionalidad.

>[!NOTE]
>¿Quiere conocer otras opciones para configurar el tráfico en la CDN, como la modificación de la solicitud/respuesta, la declaración de redirecciones y el proxy a un origen que no sea AEM? [Descubra cómo y pruébelo](/help/implementing/dispatcher/cdn-configuring-traffic.md) uniéndose al programa para primeros usuarios.


## Organización de este artículo {#how-organized}

Este artículo está organizado en las secciones siguientes:

* **Información general sobre protección del tráfico:** descubra cómo está protegido contra el tráfico malintencionado.
* **Proceso sugerido para configurar reglas:** lea acerca de una metodología de alto nivel para proteger su sitio web.
* **Configuración:** descubra cómo configurar e implementar reglas de filtro de tráfico, incluidas las reglas WAF avanzadas.
* **Sintaxis de reglas:** obtenga información sobre cómo declarar reglas de filtro de tráfico en el archivo de configuración de `cdn.yaml`. Esto incluye las reglas de filtro de tráfico disponibles para todos los clientes de Sites y Forms, y la subcategoría de reglas WAF para aquellos que otorgan licencia a esa funcionalidad.
* **Ejemplos de reglas:** consulte ejemplos de reglas declaradas para ponerse en marcha.
* **Reglas de límite de volumen:** aprenda a utilizar reglas de limitación de volumen para proteger el sitio de ataques de gran volumen.
* **Registros de CDN:** compruebe qué reglas declaradas e indicadores WAF coinciden con el tráfico.
* **Herramientas del tablero:** analice los registros de CDN para crear nuevas reglas de filtro de tráfico.
* **Reglas de inicio recomendadas:** un conjunto de reglas para empezar.
* **Tutorial:** conocimientos prácticos sobre la función, incluido cómo utilizar las herramientas del tablero para declarar las reglas correctas.

Le invitamos a hacernos llegar sus comentarios o preguntas sobre las reglas de filtro de tráfico enviando un correo electrónico a **aemcs-waf-adopter@adobe.com**.

## Información general sobre protección del tráfico {#traffic-protection-overview}

En el panorama digital actual, el tráfico malicioso es una amenaza constante. Reconocemos la gravedad del riesgo y ofrecemos varios enfoques para proteger las aplicaciones de los clientes y mitigar los ataques cuando se producen.

En la periferia, la CDN administrada por Adobe absorbe los ataques DoS en el nivel de red 
(capas 3 y 4), incluidos los ataques de inundación y reflexión/amplificación.

De forma predeterminada, Adobe toma medidas para evitar la degradación del rendimiento debido a ráfagas de tráfico inesperadamente altas que superan un determinado umbral. En caso de que un ataque DoS afecte a la disponibilidad del sitio, los equipos de operaciones de Adobe reciben una alerta y toman medidas para mitigarlo.

Los clientes pueden tomar medidas proactivas para mitigar los ataques de la capa de aplicación (capa 7) configurando reglas en varios niveles del flujo de distribución de contenido.

Por ejemplo, en la capa de Apache, los clientes pueden configurar el [módulo de Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=es#configuring-access-to-content-filter) o [ModSecurity](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/security/modsecurity-crs-dos-attack-protection.html?lang=es) para limitar el acceso a determinado contenido.

Y, tal como se describe en este artículo, las reglas de filtro de tráfico pueden implementarse en la red de distribución de contenido (CDN) administrada por Adobe mediante la canalización de configuración de Cloud Manager. Además de las reglas de filtro de tráfico basadas en propiedades como la dirección IP, la ruta y los encabezados o las reglas basadas en la configuración de límites de volumen, los clientes también pueden obtener una licencia de una potente subcategoría de reglas de filtro de tráfico denominadas reglas WAF.

## Proceso sugerido {#suggested-process}

A continuación, se presenta un proceso de extremo a extremo recomendado de alto nivel para crear las reglas de filtro de tráfico adecuadas:

1. Configure las canalizaciones de configuración de producción y las que no son de producción, tal como se describe en la sección [Configuración](#setup).
1. Los clientes que tengan licencia para la subcategoría de reglas de filtro de tráfico WAF deben habilitarlas en Cloud Manager.
1. Lea y pruebe el tutorial para comprender en particular cómo utilizar las reglas de filtro de tráfico, incluidas las reglas WAF si se han autorizado. El tutorial le guía por la implementación de reglas en un entorno de desarrollo, simulando tráfico malicioso y descargando [registros de CDN](#cdn-logs) y analizándolos en [herramientas de tablero](#dashboard-tooling).
1. Copie las reglas de inicio recomendadas en `cdn.yaml` e implemente la configuración en el entorno de producción en modo de registro.
1. Después de recopilar un poco de tráfico, analice los resultados utilizando [herramientas de tablero](#dashboard-tooling) para ver si había alguna coincidencia. Busque falsos positivos y realice los ajustes necesarios para activar finalmente las reglas de inicio en el modo de bloqueo.
1. Añada reglas personalizadas basadas en el análisis de los registros de CDN, probando primero con tráfico simulado en entornos de desarrollo antes de implementarlas en entornos de fase y producción en modo de registro y, a continuación, en el modo de bloqueo.
1. Monitorice el tráfico de forma continua y realice cambios en las reglas a medida que evoluciona el panorama de amenazas.

## Configuración {#setup}

1. En primer lugar, cree la siguiente carpeta y estructura de archivos en la carpeta de nivel superior del proyecto en Git:

   ```
   config/
        cdn.yaml
   ```

1. `cdn.yaml` debe contener metadatos y una lista de reglas de filtros de tráfico y reglas WAF.

   ```
   kind: "CDN"
   version: "1"
   metadata:
     envTypes: ["dev"]
   data:
     trafficFilters:
       rules:
       # Block simple path
       - name: block-path
         when:
           allOf:
             - reqProperty: tier
               matches: "author|publish"
             - reqProperty: path
               equals: '/block/me'
         action: block
   ```

El parámetro `kind` debe establecerse en `CDN` y la versión debe establecerse en la versión de esquema, que actualmente es `1`. Consulte los ejemplos más adelante.


<!-- Two properties -- `envType` and `envId` -- may be included to limit the scope of the rules. The envType property may have values "dev", "stage", or "prod", while the envId property is the environment (for example, "53245"). This approach is useful if it is desired to have a single configuration pipeline, even if some environments have different rules. However, a different approach could be to have multiple configuration pipelines, each pointing to different repositories or git branches. -->

1. Si las reglas WAF tienen licencia, debe habilitar la función en Cloud Manager, tal como se describe a continuación para los escenarios de programa nuevos y existentes.

   1. Para configurar WAF en un nuevo programa, marque la casilla de verificación **Protección WAF-DDOS** de la pestaña **Seguridad** cuando [añada un programa de producción.](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md)

   1. Para configurar WAF en un programa existente, [editando el programa](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/editing-programs.md) y en la pestaña **Seguridad** desmarque o marque la opción **WAF-DDOS** en cualquier momento.

1. Para tipos de entorno distintos de RDE, cree una canalización de configuración de implementación de destino en Cloud Manager.

   * [Consulte Configuración de canalizaciones de producción](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md).
   * [Consulte Configuración de canalizaciones que no son de producción](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md).

Para RDE, se utilizará la línea de comandos, pero RDE no es compatible en este momento.

**Notas**

* Puede utilizar `yq` para validar localmente el formato YAML del archivo de configuración (por ejemplo, `yq cdn.yaml`).

## Sintaxis de reglas de filtro de tráfico {#rules-syntax}

Puede configurar `traffic filter rules` para que coincida en patrones como direcciones IP, agente de usuario, encabezados de solicitud, nombre de host, ubicación geográfica y url.

Los clientes que otorgan licencia a la oferta de seguridad mejorada o de seguridad de protección WAF-DDoS también pueden configurar una categoría especial de reglas de filtro de tráfico denominada `WAF traffic filter rules` (o reglas WAF para abreviar) que hacen referencia a uno o varios [Indicadores WAF](#waf-flags-list).

Este es un ejemplo de un conjunto de reglas de filtro de tráfico, que también incluye una regla WAF.

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev"]
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

El formato de las reglas de filtro de tráfico en el archivo `cdn.yaml` se describe a continuación. Vea algunos [ejemplos más](#examples) en una sección posterior y en una sección independiente sobre [Reglas de límite de volumen](#rate-limit-rules).


| **Propiedad** | **La mayoría de las reglas de filtro de tráfico** | **Reglas de filtro de tráfico WAF** | **Tipo** | **Valor predeterminado** | **Descripción** |
|---|---|---|---|---|---|
| name | X | X | `string` | - | El nombre de la regla (64 caracteres, solo puede contener caracteres alfanuméricos y - ) |
| when | X | X | `Condition` | - | La estructura básica es:<br><br>`{ <getter>: <value>, <predicate>: <value> }`<br><br>[Consulte Sintaxis de estructura de condición](#condition-structure) a continuación, que describe los captadores, los predicados y cómo combinar varias condiciones. |
| acción | X | X | `Action` | log | objeto log, allow, block o Action. El valor predeterminado es log |
| rateLimit | X |   | `RateLimit` | sin definir | Configuración del límite de volumen. La limitación de volumen está deshabilitada si no se define.<br><br>Hay una sección independiente más abajo que describe la sintaxis de rateLimit, junto con ejemplos. |

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
| **allOf** | `array[Condition]` | Operación **and**. Es true, si todas las condiciones enumeradas devuelven el valor true |
| **anyOf** | `array[Condition]` | Operación **or**. Es true si alguna de las condiciones enumeradas devuelve el valor true |

**Getter**

| **Propiedad** | **Tipo** | **Descripción** |
|---|---|---|
| reqProperty | `string` | Solicitar propiedad.<br><br>Uno de:<br><ul><li>`path`: devuelve la ruta completa de una dirección URL sin los parámetros de consulta.</li><li>`queryString`: devuelve la parte de consulta de una dirección URL</li><li>`method`: devuelve el método HTTP utilizado en la solicitud.</li><li>`tier`: devuelve uno de `author`, `preview` o `publish`.</li><li>`domain`: devuelve la propiedad de dominio (tal como se define en el encabezado `Host`) en minúsculas</li><li>`clientIp`: devuelve la IP del cliente.</li><li>`clientCountry`: devuelve un código de dos letras ([https://en.wikipedia.org/wiki/Regional_indicator_symbol](https://en.wikipedia.org/wiki/Regional_indicator_symbol) que identifica en qué país se encuentra el cliente.</li></ul> |
| reqHeader | `string` | Devuelve el encabezado de la solicitud con el nombre especificado |
| queryParam | `string` | Devuelve el parámetro de consulta con el nombre especificado |
| reqCookie | `string` | Devuelve una cookie con el nombre especificado |
| postParam | `string` | Devuelve un parámetro de publicación con el nombre especificado del cuerpo de la solicitud. Solo funciona cuando el cuerpo es de tipo de contenido `application/x-www-form-urlencoded` |

**Predicado**

| **Propiedad** | **Tipo** | **Significado** |
|---|---|---|
| **igual a** | `string` | true si el resultado del captador es igual al valor proporcionado |
| **doesNotEqual** | `string` | true si el resultado del captador no es igual al valor proporcionado |
| **me gusta** | `string` | true si el resultado del captador coincide con el patrón proporcionado |
| **notLike** | `string` | true si el resultado del captador no coincide con el patrón proporcionado |
| **matches** | `string` | true si el resultado del captador coincide con la expresión regular proporcionada |
| **doesNotMatch** | `string` | true si el resultado del captador no coincide con la expresión regular proporcionada |
| **en** | `array[string]` | true si la lista proporcionada contiene un resultado de captador |
| **notIn** | `array[string]` | true si la lista proporcionada no contiene el resultado del captador |
| **existe** | `boolean` | true cuando se establece en true y la propiedad existe o cuando se establece en false y la propiedad no existe |

**Notas**

* La propiedad de solicitud `clientIp` solo se puede utilizar con los siguientes predicados: `equals`, `doesNotEqual`, `in`, `notIn`. `clientIp` también se puede comparar con intervalos de IP cuando se utilizan los predicados `in` y `notIn`. En el siguiente ejemplo se implementa una condición para evaluar si una IP de cliente está en el rango de IP de 192.168.0.0/24 (o sea, desde 192.168.0.0 hasta 192.168.0.255):

```
when:
  reqProperty: clientIp
  in: [ "192.168.0.0/24" ]
```

* Se recomienda el uso de [regex101](https://regex101.com/) y [Fastly Fiddle](https://fiddle.fastly.dev/) cuando se utiliza una expresión regular. También puede obtener más información sobre cómo Fastly gestiona la expresión regular de este [artículo](https://developer.fastly.com/reference/vcl/regex/#best-practices-and-common-mistakes).


### Estructura de acción {#action-structure}

Una `action` puede ser una cadena que especifique la acción (permitir, bloquear o registrar) o un objeto compuesto por el tipo de acción (permitir, bloquear o registrar) y opciones como wafFlags y/o estado.

**Tipos de acción**

Las acciones se priorizan según sus tipos en la siguiente tabla, que se ordena para reflejar el orden en el que se ejecutan las acciones:

| **Nombre** | **Propiedades permitidas** | **Significado** |
|---|---|---|
| **permitir** | `wafFlags` (opcional), `alert` (opcional, todavía sin publicar) | si wafFlags no está presente, detiene el procesamiento posterior de la regla y procede a proporcionar la respuesta. Si wafFlags está presente, deshabilita las protecciones WAF especificadas y continúa con el procesamiento de la regla. <br>Si se especifica una alerta, se envía una notificación del Centro de acciones si la regla se activa 10 veces en un intervalo de 5 minutos. Esta función todavía no se ha lanzado; consulte las [Alertas de reglas de filtro de tráfico](#traffic-filter-rules-alerts) para obtener información sobre cómo unirse al programa para primeros usuarios. |
| **block** | `status, wafFlags` (opcional y mutuamente excluyente), `alert` (opcional, todavía sin publicar) | si wafFlags no está presente, devuelve un error HTTP omitiendo todas las demás propiedades, el código de error se define mediante la propiedad estado o el valor predeterminado es 406. Si wafFlags está presente, permite protecciones WAF especificadas y continúa con el procesamiento de la regla. <br>Si se especifica una alerta, se envía una notificación del Centro de acciones si la regla se activa 10 veces en un intervalo de 5 minutos. Esta función todavía no se ha lanzado; consulte las [Alertas de reglas de filtro de tráfico](#traffic-filter-rules-alerts) para obtener información sobre cómo unirse al programa para primeros usuarios. |
| **log** | `wafFlags` (opcional), `alert` (opcional, todavía sin publicar) | registra el hecho de que la regla se activó; de lo contrario, no afecta al procesamiento. wafFlags no tiene ningún efecto. <br>Si se especifica una alerta, se envía una notificación del Centro de acciones si la regla se activa 10 veces en un intervalo de 5 minutos. Esta función todavía no se ha lanzado; consulte las [Alertas de reglas de filtro de tráfico](#traffic-filter-rules-alerts) para obtener información sobre cómo unirse al programa para primeros usuarios. |

### Lista de indicadores WAF {#waf-flags-list}

La propiedad `wafFlags`, que se puede utilizar en las reglas de filtro de tráfico WAF con licencia, puede hacer referencia a lo siguiente:

| **Identificador de marca** | **Nombre de indicador** | **Descripción** |
|---|---|---|
| SQLI | Inyección de SQL | La inyección de SQL es el intento de obtener acceso a una aplicación o de obtener información privilegiada ejecutando consultas de base de datos arbitrarias. |
| PUERTA TRASERA | Puerta trasera | Una señal de puerta trasera es una solicitud que intenta determinar si hay un archivo de puerta trasera común en el sistema. |
| CMDEXE | Ejecución de comandos | La ejecución de comandos es el intento de obtener control o dañar un sistema objetivo a través de comandos arbitrarios del sistema por medio de la entrada del usuario. |
| XSS | Scripts en sitios múltiples | La ejecución de scripts en sitios múltiples es el intento de apropiarse de la cuenta de un usuario o de una sesión de exploración web mediante código JavaScript malintencionado. |
| TRAVERSAL | Traversal de directorios | Traversal de directorios es el intento de navegar por carpetas privilegiadas a través de un sistema con la esperanza de obtener información confidencial. |
| USERAGENT | Herramienta de ataque | La herramienta de ataque es el uso de software automatizado para identificar vulnerabilidades de seguridad o para intentar explotar una vulnerabilidad descubierta. |
| LOG4J-JNDI | Log4J JNDI | Los ataques Log4J JNDI intentan explotar la [vulnerabilidad de Log4Shell](https://en.wikipedia.org/wiki/Log4Shell) presente en las versiones de Log4J anteriores a la versión 2.16.0 |
| BHH | Encabezados de salto incorrecto | Los encabezados de salto incorrecto indican un intento de introducir HTTP a través de un encabezado Transfer-Encoding (TE) o Content-Length (CL) mal formado o un encabezado TE y CL bien formado |
| CODEINJECTION | Inyección de código | La ejecución de código es el intento de obtener control o dañar un sistema objetivo a través de comandos arbitrarios del sistema por medio de la entrada del usuario. |
| ABNORMALPATH | Ruta anormal | Ruta anormal indica que la ruta original difiere de la ruta normalizada (por ejemplo, `/foo/./bar` se normaliza a `/foo/bar`) |
| DOUBLEENCODING | Codificación doble | La codificación doble comprueba la técnica de evasión de los caracteres HTML de doble codificación |
| NOTUTF8 | Codificación no válida | La codificación no válida puede hacer que el servidor traduzca caracteres malintencionados de una solicitud a una respuesta, lo que provoca una denegación de servicio o XSS |
| JSON-ERROR | Error de codificación de JSON | Un cuerpo de solicitud POST, PUT o PATCH que se especifica que contiene JSON dentro del encabezado de solicitud &quot;Content-Type&quot;, pero que contiene errores de análisis de JSON. Esto suele estar relacionado con un error de programación o una solicitud automatizada o maliciosa. |
| MALFORMED-DATA | Datos mal formados en el cuerpo de la solicitud | Un cuerpo de solicitud POST, PUT o PATCH con un formato incorrecto según el encabezado de solicitud &quot;Content-Type&quot;. Por ejemplo, si se especifica un encabezado de solicitud &quot;Content-Type: application/x-www-form-urlencoded&quot; y contiene un cuerpo POST que es json. Esto suele ser un error de programación, una solicitud automatizada o maliciosa. Requiere agente 3.2 o superior. |
| SANS | Tráfico IP malintencionado | [SANS Internet Storm Center](https://isc.sans.edu/) lista de direcciones IP sobre las que se ha informado que han participado en actividades maliciosas |
| NO-CONTENT-TYPE | Falta el encabezado de solicitud &quot;Content-Type&quot; | Una solicitud POST, PUT o PATCH que no tiene un encabezado de solicitud &quot;Content-Type&quot;. De forma predeterminada, los servidores de aplicaciones deben suponer &quot;Content-Type: text/plain; charset=us-ascii&quot; en este caso. Es posible que a muchas solicitudes automatizadas y maliciosas les falte &quot;Tipo de contenido&quot;. |
| NOUA | No hay agente de usuario | Muchas solicitudes automatizadas y maliciosas utilizan agentes de usuario falsos o ausentes para dificultar la identificación del tipo de dispositivo que realiza las solicitudes. |
| TORNODE | Tráfico de Tor | Tor es un software que oculta la identidad de un usuario. Un pico en el tráfico de Tor puede indicar que un atacante está tratando de ocultar su ubicación. |
| NULLBYTE | Byte nulo | Los bytes nulos no suelen aparecer en una solicitud e indican que la solicitud tiene un formato incorrecto y es potencialmente maliciosa. |
| PRIVATEFILE | Archivos privados | Los archivos privados suelen ser de naturaleza confidencial, como un archivo `.htaccess` Apache o un archivo de configuración que podría filtrar información confidencial |
| ESCÁNER | Escáner | Identifica los servicios y herramientas de digitalización más populares |
| RESPONSESPLIT | División de respuesta HTTP | Identifica cuándo se envían los caracteres CRLF como entrada a la aplicación para insertar encabezados en la respuesta HTTP |
| XML-ERROR | Error de codificación XML | Un cuerpo de solicitud POST, PUT o PATCH que se especifica que contiene XML dentro del encabezado de solicitud &quot;Content-Type&quot;, pero que contiene errores de análisis de XML. Esto suele estar relacionado con un error de programación o una solicitud automatizada o maliciosa. |

## Consideraciones {#considerations}

* Cuando se crean dos reglas en conflicto, las reglas de permiso siempre tienen prioridad sobre las reglas de bloqueo. Por ejemplo, si crea una regla para bloquear una ruta específica y una regla para permitir una dirección IP específica, se permitirán las solicitudes de esa dirección IP en la ruta bloqueada.

* Si una regla coincide y está bloqueada, CDN responde con un código de retorno `406`.

* Los archivos de configuración no deben contener secretos, ya que cualquier persona que tenga acceso al repositorio de Git podrá leerlos.

* Las listas de IP permitidas definidas en Cloud Manager tienen prioridad sobre las reglas de los filtros de tráfico.

* Las coincidencias de reglas WAF solo aparecen en los registros CDN para los errores y aprobaciones de CDN, no en los aciertos.

## Ejemplos de reglas {#examples}

A continuación se muestran algunos ejemplos de reglas. Consulte la [sección sobre límite de volumen](#rules-with-rate-limits) a continuación para ver ejemplos de reglas de límite de volumen.

**Ejemplo: 1**

Esta regla bloquea las solicitudes procedentes de **IP 192.168.1.1**:

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  trafficFilters:
     rules:
       - name: "block-request-from-ip"
         when: { reqProperty: clientIp, equals: "192.168.1.1" }
         action:
           type: block
```

**Ejemplo: 2**

Esta regla bloquea las solicitudes en la ruta `/helloworld` al publicar con un agente de usuario que contiene Chrome:

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  trafficFilters:
    rules:
      - name: "block-request-from-chrome-on-path-helloworld-for-publish-tier"
        when:
          allOf:
          - { reqProperty: path, equals: /helloworld }
          - { reqProperty: tier, equals: publish }
          - { reqHeader: user-agent, matches: '.*Chrome.*'  }
        action:
          type: block
```

**Ejemplo: 3**

Esta regla bloquea las solicitudes que contienen el parámetro de consulta `foo`, pero permite todas las solicitudes procedentes de IP 192.168.1.1:

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev"]
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

**Ejemplo: 4**

Esta regla bloquea las solicitudes a la ruta `/block-me` y bloquea todas las solicitudes que coinciden con un patrón `SQLI` o `XSS`. Este ejemplo incluye reglas de filtro de tráfico WAF, que hace referencia a los [Indicadores WAF](#waf-flags-list) `SQLI` y `XSS` y, por lo tanto, requiere una licencia independiente.

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev"]
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

**Ejemplo: 5**

Esta regla bloquea el acceso a los países de la OFAC:

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  trafficFilters:
    rules:
      - name: block-ofac-countries
        when:
          allOf:
            - reqProperty: tier
              matches: "author|publish"
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

## Reglas de límite de volumen {#rate-limits-rules}

A veces es deseable bloquear el tráfico si supera un cierto volumen de solicitudes entrantes, tal vez en función de una condición específica. Configurar un valor para la propiedad `rateLimit` limita el volumen de las solicitudes que coinciden con la condición de la regla.

Las reglas de límite de volumen no pueden hacer referencia a indicadores WAF. Están disponibles para todos los clientes de Sites y Forms.

Los límites de volumen se calculan por CDN POP. Por ejemplo, supongamos que los POP de Montreal, Miami y Dublín tienen volúmenes de tráfico de 80, 90 y 120 solicitudes por segundo respectivamente, y que la regla de límite de volumen está establecida en un límite de 100. En ese caso, solo el tráfico a Dublín tendría limitación de volumen.

Los límites de velocidad se evalúan en función del tráfico que llega al extremo, el tráfico que llega al extremo o el número de errores.

### Estructura rateLimit {#ratelimit-structure}

| **Propiedad** | **Tipo** | **Predeterminado** | **SIGNIFICADO** |
|---|---|---|---|
| limit | entero de 10 a 10000 | Requerido | Volumen de solicitud (por CDN POP) en solicitudes por segundo para las que se activa la regla. |
| ventana | integer enum: 1, 10 o 60 | 10 | Ventana de muestreo en segundos para la que se calcula el volumen de solicitud. La precisión de los contadores dependerá del tamaño de la ventana (ventana más grande, mayor precisión). Por ejemplo, se puede esperar una precisión del 50 % para la ventana de 1 segundo y del 90 % para la de 60 segundos. |
| penalty | entero de 60 a 3600 | 300 (5 minutos) | Período en segundos durante el cual se bloquean las solicitudes de coincidencia (redondeado al minuto más próximo). |
| recuento | all, fetch, error | todo | evalúe en función del tráfico de Edge (todo), el tráfico de origen (captura) o el número de errores. |
| groupBy | array[Getter] | ninguno | El contador de limitador de volumen se añadirá mediante un conjunto de propiedades de solicitud (por ejemplo, clientIp). |


### Ejemplos {#ratelimiting-examples}

**Ejemplo 1**

Esta regla bloquea un cliente durante 5 m cuando supera un promedio de 60 req/s (por CDN POP) en los últimos 60 segundos:

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  trafficFilters:
    rules:
    - name: limit-requests-client-ip
      when:
        reqProperty: tier
        matches: "author|publish"
      rateLimit:
        limit: 60
        window: 10
        penalty: 300
        count: all
        groupBy:
          - reqProperty: clientIp
      action: block
```

**Ejemplo: 2**

Bloquear solicitudes de 60 segundos en la ruta /crítico/recurso cuando supere los 100 req/s (por CDN POP) en los últimos 60 segundos:

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  trafficFilters:
    rules:
      - name: rate-limit-example
        when: { reqProperty: path, equals: /critical/resource }
        action:
          type: block
        rateLimit: { limit: 100, window: 60, penalty: 60, count: all }
```

## Alertas de reglas de filtro de tráfico {#traffic-filter-rules-alerts}

>[!NOTE]
>
>Esta función todavía no se ha lanzado. Para obtener acceso a través del programa para primeros usuarios, envíe un correo electrónico a **aemcs-waf-adopter@adobe.com**.

Se puede configurar una regla para enviar una notificación del Centro de acciones si se activa 10 veces en un intervalo de 5 minutos, alertándole cuando se producen ciertos patrones de tráfico para que pueda tomar las medidas necesarias. Más información sobre el [Centro de acciones](/help/operations/actions-center.md), incluido cómo configurar los perfiles de notificación necesarios para recibir correos electrónicos.

![Notificación del Centro de acciones](/help/security/assets/traffic-filter-rules-actions-center-alert.png)


La propiedad de alerta (actualmente con el prefijo *experimental* dado que la función todavía no se ha lanzado) se puede aplicar al nodo de acción para todos los tipos de acción (allow, block, log).

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  trafficFilters:
    rules:
      - name: "path-rule"
        when: { reqProperty: path, equals: /block-me }
        action:
          type: block
          experimental_alert: true
```

## Registros de CDN {#cdn-logs}

AEM as a Cloud Service proporciona acceso a los registros de CDN, que son útiles para casos de uso, incluida la optimización de la proporción de visitas de caché y la configuración de reglas de filtro de tráfico. Los registros de CDN aparecen en el cuadro diálogo de Cloud Manager **Descargar registros**, al seleccionar el servicio de creación o publicación.

Los registros de CDN pueden retrasarse hasta cinco minutos.

La propiedad `rules` describe qué reglas de filtro de tráfico coinciden y tiene el siguiente patrón:

```
"rules": "match=<matching-customer-named-rules-that-are-matched>,waf=<matching-WAF-rules>,action=<action_type>"
```

Por ejemplo:

```
"rules": "match=Block-Traffic-under-private-folder,Enable-SQL-injection-everywhere,waf="SQLI,SANS",action=block"
```

Las reglas se comportan de la siguiente manera:

* El nombre de regla declarado por el cliente de cualquier regla coincidente se enumerará en el atributo `match`.
* El atributo `action` determina si las reglas tuvieron el efecto de bloquear, permitir o registrar.
* Si el WAF tiene licencia y está habilitado, el atributo `waf` enumerará cualquier indicador WAF (por ejemplo, SQLI) que se haya detectado, independientemente de si los indicadores WAF se han enumerado en alguna regla. Esto sirve para conocer las posibles nuevas reglas que se pueden declarar.
* Si no coinciden las reglas declaradas por el cliente y no coinciden las reglas waf, la propiedad `rules` estará en blanco.

Como se ha indicado anteriormente, las coincidencias de reglas WAF solo aparecen en los registros CDN para errores y aprobaciones de CDN, no en los aciertos.

En el ejemplo siguiente se muestra un `cdn.yaml` de ejemplo y dos entradas de registro de CDN:


```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev"]
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
| *timestamp* | Hora a la que se inició la solicitud, después de la finalización de TLS. |
| *ttfb* | Abreviatura de *Time To First Byte*. Intervalo de tiempo entre el inicio de la solicitud hasta el punto en el que el cuerpo de la respuesta comenzó a transmitirse. |
| *cli_ip* | La dirección IP del cliente. |
| *cli_country* | Código de país [ISO 3166-1](https://en.wikipedia.org/wiki/ISO_3166-1) alpha-2 de dos letras correspondiente al país del cliente. |
| *rid* | El valor del encabezado de la solicitud que se utiliza para identificar la solicitud de forma exclusiva. |
| *req_ua* | El agente de usuario responsable de realizar una petición HTTP determinada. |
| *host* | La autoridad a la que está destinada la solicitud. |
| *URL* | La ruta completa, incluidos los parámetros de consulta. |
| *method* | Método HTTP enviado por el cliente, como &quot;GET&quot; o &quot;POST&quot;. |
| *res_ctype* | Tipo de contenido que se utiliza para indicar el tipo de medio original del recurso. |
| *cache* | Estado de la caché. Los valores posibles son HIT, MISS o PASS |
| *status* | El código de estado HTTP como un valor entero. |
| *res_age* | Cantidad de tiempo (en segundos) que una respuesta se ha almacenado en la caché (en todos los nodos). |
| *pop* | Centro de datos del servidor de caché de CDN. |
| *reglas* | El nombre de cualquier regla coincidente.<br><br>También indica si la coincidencia resultó en un bloqueo. <br><br>Por ejemplo, &quot;`match=Enable-SQL-Injection-and-XSS-waf-rules-globally,waf=SQLI,action=blocked`&quot;<br><br>Vacío si no hay reglas que coincidan. |

## Herramientas del tablero {#dashboard-tooling}

Adobe proporciona un mecanismo para descargar las herramientas del tablero en el equipo para introducir registros de CDN descargados mediante Cloud Manager. Con esta herramienta, puede analizar el tráfico para determinar las reglas de filtro de tráfico apropiadas que se deben declarar, incluidas las reglas WAF.

Las herramientas de tablero se pueden clonar directamente desde el repositorio de Github [AEMCS-CDN-Log-Analysis-ELK-Tool](https://github.com/adobe/AEMCS-CDN-Log-Analysis-ELK-Tool).

[Tutorials](#tutorial) están disponibles para obtener instrucciones concretas sobre cómo utilizar las herramientas de tablero.

## Reglas de inicio recomendadas {#recommended-starter-rules}

Puede copiar las reglas recomendadas a continuación en su `cdn.yaml` para empezar. Inicie en el modo de registro, analice el tráfico y, cuando esté satisfecho, cambie al modo de bloqueo. Es posible que quiera modificar las reglas en función de las características únicas del tráfico en directo del sitio web.

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev", "stage", "prod"]
data:
  trafficFilters:
    rules:
    #  Block client for 5m when it exceeds 100 req/sec on a time window of 1sec
    - name: limit-requests-client-ip
      when:
        reqProperty: path
        like: '*'
      rateLimit:
        limit: 100
        window: 1
        penalty: 300
        groupBy:
          - reqProperty: clientIp
      action: log
    # Block requests coming from OFAC countries
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
      action: log
    # Enable recommended WAF protections (only works if WAF is licensed enabled for your environment)
    - name: block-waf-flags-globally
      when:
        reqProperty: tier
        matches: "author|publish"
      action:
        type: log
        wafFlags:
          - SANS
          - TORNODE
          - NOUA
          - SCANNER
          - USERAGENT
          - PRIVATEFILE
          - ABNORMALPATH
          - TRAVERSAL
          - NULLBYTE
          - BACKDOOR
          - LOG4J-JNDI
          - SQLI
          - XSS
          - CODEINJECTION
          - CMDEXE
          - NO-CONTENT-TYPE
          - UTF8
    # Disable protection against CMDEXE on /bin (only works if WAF is licensed enabled for your environment)
    - name: allow-cdmexe-on-root-bin
      when:
        allOf:
          - reqProperty: tier
            matches: "author|publish"
          - reqProperty: path
            matches: "^/bin/.*"
      action:
        type: allow
        wafFlags:
          - CMDEXE
```

## Tutoriales {#tutorial}

Hay dos tutoriales disponibles.

### Protección de sitios web con reglas de filtro de tráfico (incluidas las reglas WAF)

[Trabajar con un tutorial](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/security/traffic-filter-and-waf-rules/overview.html?lang=es) para obtener conocimientos y experiencia generales y prácticos sobre las reglas de filtro de tráfico, incluidas las reglas de WAF.

El tutorial le guiará por los siguientes temas:

* Configuración de la canalización de configuración de Cloud Manager
* Uso de herramientas para simular tráfico malintencionado
* Declaración de reglas de filtro de tráfico, incluidas las reglas WAF
* Análisis de resultados con las herramientas del tablero
* Prácticas recomendadas

### Bloqueo de ataques DoS y DoS mediante reglas de filtro de tráfico

[Profundizar en cómo bloquear](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/security/blocking-dos-attack-using-traffic-filter-rules) Ataques de denegación de servicio (DoS) y denegación de servicio distribuido (DDoS) que utilizan reglas de filtro de tráfico de límite de velocidad y otras estrategias.

El tutorial le guiará por los siguientes temas:

* comprensión de la protección
* recepción de alertas cuando se superen los límites de velocidad
* análisis de los patrones de tráfico mediante las herramientas del tablero para configurar los umbrales de las reglas de filtro de tráfico de límite de velocidad



