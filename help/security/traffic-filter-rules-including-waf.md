---
title: Reglas de filtro de tráfico, incluidas las reglas WAF
description: Configuración de reglas de filtro de tráfico, incluidas las reglas de cortafuegos de aplicaciones web (WAF)
exl-id: 6a0248ad-1dee-4a3c-91e4-ddbabb28645c
source-git-commit: aca385ff9a44733a6529c7e78e73fc1b138c1177
workflow-type: tm+mt
source-wordcount: '3453'
ht-degree: 1%

---


# Reglas de filtro de tráfico, incluidas las reglas WAF {#traffic-filter-rules-including-waf-rules}

>[!NOTE]
>Esta función estará disponible próximamente en entornos de desarrollo, con un despliegue gradual en entornos de ensayo y producción en noviembre. Puede solicitar acceso anticipado en la fase y producción enviando un correo electrónico a **aemcs-waf-adopter@adobe.com**.

Las reglas de filtro de tráfico se pueden utilizar para bloquear o permitir solicitudes en la capa de CDN, lo que puede resultar útil en situaciones como las siguientes:

* Restricción del acceso a dominios específicos al tráfico interno de la compañía antes de que se active un nuevo sitio
* Establecimiento de límites de velocidad para que sea menos susceptible a los ataques volumétricos de denegación de servicio
* Impedir que las direcciones IP que se sabe que son malintencionadas segmenten sus páginas

AEM La mayoría de estas reglas de filtro de tráfico están disponibles para todos los clientes de Forms y sitios as a Cloud Service de la. Funcionan principalmente en propiedades de solicitud y encabezados de solicitud, incluidos la IP, el nombre de host, la ruta y el agente de usuario.

Una subcategoría de reglas de filtro de tráfico requiere una licencia de seguridad mejorada o una licencia de protección WAF-DDoS, y estará disponible a finales de este año. Estas reglas poderosas se conocen como reglas de filtro de tráfico WAF (cortafuegos de aplicaciones web) (o reglas WAF para abreviar) y tienen acceso a [Indicadores WAF](#waf-flags-list) se describe más adelante en este artículo.

Las reglas de filtro de tráfico se pueden implementar mediante canalizaciones de configuración de Cloud Manager para los tipos de entorno de desarrollo, ensayo y producción en programas de producción (que no sean de zonas protegidas). El soporte para RDE vendrá en el futuro.

## Organización de este artículo {#how-organized}

Este artículo está organizado en las siguientes secciones:

* **Resumen de protección del tráfico:** Descubra cómo está protegido contra el tráfico malintencionado.
* **Proceso sugerido para configurar reglas:** Lea acerca de una metodología de alto nivel para proteger su sitio web.
* **Configuración:** Descubra cómo configurar e implementar reglas de filtro de tráfico, incluidas las reglas WAF avanzadas.
* **Sintaxis de reglas:** Obtenga información sobre cómo declarar reglas de filtro de tráfico en la `cdn.yaml` archivo de configuración. Esto incluye las reglas de filtro de tráfico disponibles para todos los clientes de Sites y Forms, así como la subcategoría de reglas WAF para aquellos que otorgan licencia a esa capacidad.
* **Ejemplos de reglas:** Consulte ejemplos de reglas declaradas para ponerse en marcha.
* **Reglas de límite de tarifa:** Aprenda a utilizar reglas de limitación de velocidad para proteger el sitio de ataques de gran volumen.
* **Registros de CDN:** Compruebe qué reglas declaradas y marcas WAF coinciden con el tráfico.
* **Herramientas del panel:** Analice los registros de CDN para crear nuevas reglas de filtro de tráfico.
* **Reglas de inicio recomendadas:** Un conjunto de reglas para empezar a usar.
* **Tutorial:** Conocimientos prácticos sobre la función, incluido cómo utilizar las herramientas del panel para declarar las reglas correctas.

Le invitamos a enviar sus comentarios o hacer preguntas sobre las reglas de filtro de tráfico por correo electrónico **aemcs-waf-adopter@adobe.com**.

## Resumen de protección del tráfico {#traffic-protection-overview}

En el panorama digital actual, el tráfico malicioso es una amenaza constante. Reconocemos la gravedad del riesgo y ofrecemos varios enfoques para proteger las aplicaciones de los clientes y mitigar los ataques cuando se producen.

En el límite, la CDN administrada por Adobe absorbe los ataques DoS en el nivel de red (capas 3 y 4), incluidos los ataques de inundación y reflexión/amplificación.

De forma predeterminada, el Adobe de toma medidas para evitar la degradación del rendimiento debido a ráfagas de tráfico inesperadamente alto que superan un determinado umbral. En caso de que un ataque de DoS afecte a la disponibilidad del sitio, los equipos de operaciones de Adobe reciben una alerta y toman medidas para mitigarlo.

Los clientes pueden tomar medidas proactivas para mitigar los ataques de la capa de aplicación (capa 7) configurando reglas en varios niveles del flujo de entrega de contenido.

Por ejemplo, en la capa de Apache, los clientes pueden configurar [módulo de dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=en#configuring-access-to-content-filter) o [ModSecurity](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/security/modsecurity-crs-dos-attack-protection.html?lang=en) para limitar el acceso a cierto contenido.

Y, como se describe en este artículo, las reglas de filtro de tráfico pueden implementarse en la CDN administrada por Adobe mediante la canalización de configuración de Cloud Manager. Además de las reglas de filtro de tráfico basadas en propiedades como la dirección IP, la ruta y los encabezados, o las reglas basadas en la configuración de límites de velocidad, los clientes también pueden obtener una licencia de una potente subcategoría de reglas de filtro de tráfico denominadas reglas WAF.

## Proceso sugerido {#suggested-process}

El siguiente es un proceso de extremo a extremo recomendado de alto nivel para crear las reglas de filtro de tráfico adecuadas:

1. Configure las canalizaciones que no sean de producción y configuración de producción, tal como se describe en la sección [Configurar](#setup) sección.
1. Los clientes que tengan licencia para la subcategoría de reglas de filtro de tráfico WAF deben habilitarlas en Cloud Manager.
1. Lea y pruebe el tutorial para comprender concretamente cómo utilizar las reglas de filtro de tráfico, incluidas las reglas WAF si se han autorizado. El tutorial lo acompaña en la implementación de reglas en un entorno de desarrollo, simulando tráfico malicioso y descargando [Registros de CDN](#cdn-logs)y analizándolos en [herramientas de tablero](#dashboard-tooling).
1. Copiar las reglas de inicio recomendadas en `cdn.yaml` e implemente la configuración en el entorno de producción en modo de registro.
1. Después de recopilar un poco de tráfico, analice los resultados utilizando [herramientas de tablero](#dashboard-tooling) para ver si había alguna coincidencia. Busque falsos positivos y realice los ajustes necesarios para activar finalmente las reglas de inicio en el modo de bloque.
1. Añada reglas personalizadas basadas en el análisis de los registros de CDN, probando primero con tráfico simulado en entornos de desarrollo antes de implementarlas en entornos de ensayo y producción en modo de registro y, a continuación, en modo de bloqueo.
1. Monitorice el tráfico de forma continua y realice cambios en las reglas a medida que evoluciona el panorama de amenazas.

## Configuración {#setup}

1. En primer lugar, cree la siguiente carpeta y estructura de archivos en la carpeta de nivel superior del proyecto en Git:

   ```
   config/
        cdn.yaml
   ```

1. `cdn.yaml` debe contener metadatos, así como una lista de reglas de filtros de tráfico y reglas WAF.

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

El `kind` el parámetro debe establecerse en `CDN` y la versión debe establecerse en la versión de esquema, que actualmente es `1`. Consulte los ejemplos más adelante.


<!-- Two properties -- `envType` and `envId` -- may be included to limit the scope of the rules. The envType property may have values "dev", "stage", or "prod", while the envId property is the environment (e.g., "53245"). This approach is useful if it is desired to have a single configuration pipeline, even if some environments have different rules. However, a different approach could be to have multiple configuration pipelines, each pointing to different repositories or git branches. -->

1. Si las reglas WAF tienen licencia, debe habilitar la función en Cloud Manager, como se describe a continuación para los escenarios de programa nuevo y existente.

   1. Para configurar WAF en un nuevo programa, marque la **Protección WAF-DDOS** casilla de verificación de la **Seguridad** pestaña cuando [agregue un programa de producción.](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md)

   1. Para configurar WAF en un programa existente, [edición del programa](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/editing-programs.md) y en el **Seguridad** pestaña desmarque o marque **WAF-DDOS** en cualquier momento.

1. Para tipos de entorno distintos de RDE, cree una canalización de configuración de implementación de destino en Cloud Manager.

   * [Consulte este documento para canalizaciones de producción.](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md)
   * [Consulte este documento para canalizaciones que no sean de producción.](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md)

Para RDE, se utilizará la línea de comandos, pero RDE no es compatible en este momento.

**Notas**

* Puede utilizar `yq` para validar localmente el formato YAML del archivo de configuración (p. ej., `yq cdn.yaml`).

## Sintaxis de reglas de filtro de tráfico {#rules-syntax}

Puede configurar `traffic filter rules` para coincidir en patrones como direcciones IP, agente de usuario, encabezados de solicitud, nombre de host, ubicación geográfica y url.

Los clientes que conceden licencia a la oferta de seguridad mejorada o de seguridad de protección WAF-DDoS también pueden configurar una categoría especial de reglas de filtro de tráfico llamada `WAF traffic filter rules` (o reglas WAF para abreviar) que hacen referencia a una o más [Indicadores WAF](#waf-flags-list).

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

El formato de las reglas de filtro de tráfico en la variable `cdn.yaml` Este archivo se describe a continuación. Ver algunos [otros ejemplos](#examples) en una sección posterior, así como en una sección independiente sobre [Reglas de límite de velocidad](#rate-limit-rules).


| **Propiedad** | **La mayoría de reglas de filtro de tráfico** | **Reglas de filtro de tráfico WAF** | **Tipo** | **Valor predeterminado** | **Descripción** |
|---|---|---|---|---|---|
| name | X | X | `string` | - | El nombre de la regla (64 caracteres, solo puede contener caracteres alfanuméricos y - ) |
| cuando | X | X | `Condition` | - | La estructura básica es:<br><br>`{ <getter>: <value>, <predicate>: <value> }`<br><br>[Consulte Sintaxis de estructura de condiciones](#condition-structure) a continuación, se describen los captadores, los predicados y cómo combinar varias condiciones. |
| acción | X | X | `Action` | registro | objeto log, allow, block o Action. El valor predeterminado es registro |
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
| reqProperty | `string` | Solicitar propiedad.<br><br>Uno de:<br><ul><li>`path`: Devuelve la ruta completa de una dirección URL sin los parámetros de consulta.</li><li>`queryString`: Devuelve la parte de consulta de una dirección URL</li><li>`method`: Devuelve el método HTTP utilizado en la solicitud.</li><li>`tier`: Devuelve uno de `author`, `preview` o `publish`.</li><li>`domain`: Devuelve la propiedad de dominio (tal como se define en la variable `Host` encabezado) en minúsculas</li><li>`clientIp`: Devuelve la IP del cliente.</li><li>`clientCountry`: devuelve un código de dos letras ([https://en.wikipedia.org/wiki/Regional_indicator_symbol](https://en.wikipedia.org/wiki/Regional_indicator_symbol) que identifican en qué país se encuentra el cliente.</li></ul> |
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
| **matches** | `string` | true si el resultado del captador coincide con la regex proporcionada |
| **doesNotMatch** | `string` | true si el resultado del captador no coincide con la expresión regular proporcionada |
| **en** | `array[string]` | true si la lista proporcionada contiene un resultado de captador |
| **notIn** | `array[string]` | true si la lista proporcionada no contiene el resultado del captador |
| **existe** | `boolean` | true cuando se establece en true y la propiedad existe o cuando se establece en false y la propiedad no existe |

**Notas**

* La propiedad de solicitud `clientIp` solo se puede utilizar con los siguientes predicados: `equals`, `doesNotEqual`, `in`, `notIn`. `clientIp` también se puede comparar con intervalos de IP al utilizar `in` y `notIn` predicados. El siguiente ejemplo implementa una condición para evaluar si una IP de cliente está en el rango de IP de 192.168.0.0/24 (de 192.168.0.0 a 192.168.0.255):

```
when:
  reqProperty: clientIp
  in: [ "192.168.0.0/24" ]
```

* Se recomienda el uso de [regex101](https://regex101.com/) y [Fastly Fiddle](https://fiddle.fastly.dev/) al trabajar con regex. También puede obtener más información sobre cómo Fastly gestiona el regex en este [artículo](https://developer.fastly.com/reference/vcl/regex/#best-practices-and-common-mistakes).


### Estructura de acción {#action-structure}

Un `action` puede ser una cadena que especifique la acción (permitir, bloquear o registrar) o un objeto compuesto por el tipo de acción (permitir, bloquear o registrar) y opciones como wafFlags y/o estado.

**Tipos de acción**

Las acciones se priorizan según sus tipos en la siguiente tabla, en la que se ordena para reflejar el orden en que se ejecutan las acciones:

| **Nombre** | **Propiedades permitidas** | **Significado** |
|---|---|---|
| **permitir** | `wafFlags` (opcional) | si wafFlags no está presente, detiene el procesamiento posterior de la regla y procede a proporcionar la respuesta. Si wafFlags está presente, deshabilita las protecciones WAF especificadas y continúa con el procesamiento de reglas. |
| **bloquear** | `status, wafFlags` (opcional y mutuamente excluyente) | si wafFlags no está presente, devuelve un error HTTP omitiendo todas las demás propiedades, el código de error se define mediante la propiedad status o el valor predeterminado es 406. Si wafFlags está presente, permite protecciones WAF especificadas y continúa con el procesamiento de reglas. |
| **registro** | `wafFlags` (opcional) | registra el hecho de que la regla se activó; de lo contrario, no afecta al procesamiento. wafFlags no tiene ningún efecto |

### Lista de indicadores WAF {#waf-flags-list}

El `wafFlags` , que se puede utilizar en las reglas de filtro de tráfico WAF con licencia, puede hacer referencia a lo siguiente:

| **Identificador de marca** | **Nombre de indicador** | **Descripción** |
|---|---|---|
| SQLI | Inyección SQL | La inyección de SQL es el intento de obtener acceso a una aplicación o de obtener información privilegiada ejecutando consultas de base de datos arbitrarias. |
| PUERTA TRASERA | Puerta Trasera | Una señal de puerta trasera es una solicitud que intenta determinar si hay un archivo de puerta trasera común en el sistema. |
| CMDEXE | Ejecución de comandos | La ejecución de comandos es el intento de obtener control o dañar un sistema objetivo a través de comandos arbitrarios del sistema por medio de la entrada del usuario. |
| XSS | Scripts entre sitios | La ejecución de scripts en sitios múltiples es el intento de apropiarse de la cuenta de un usuario o de una sesión de exploración web mediante código JavaScript malintencionado. |
| TRAVESÍA | Recorrido de directorio | Directory Traversal es el intento de navegar por carpetas privilegiadas a través de un sistema con la esperanza de obtener información confidencial. |
| USERAGENT | Herramientas de ataque | La herramienta de ataque es el uso de software automatizado para identificar vulnerabilidades de seguridad o para intentar explotar una vulnerabilidad descubierta. |
| LOG4J-JNDI | Log4J JNDI | Los ataques JNDI de Log4J intentan explotar el [Vulnerabilidad de Log4Shell](https://en.wikipedia.org/wiki/Log4Shell) presente en las versiones de Log4J anteriores a la 2.16.0 |
| BHH | Encabezados de salto incorrectos | Los encabezados de salto incorrectos indican un intento de contrabando HTTP a través de un encabezado Transfer-Encoding (TE) o Content-Length (CL) mal formado o un encabezado TE y CL bien formado |
| RUTA ANORMAL | Ruta anormal | Ruta anormal indica que la ruta original difiere de la ruta normalizada (por ejemplo, `/foo/./bar` se normaliza a `/foo/bar`) |
| DOUBLEENCODING | Codificación doble | La codificación doble comprueba la técnica de evasión de los caracteres HTML de codificación doble |
| NOTUTF8 | Codificación no válida | La codificación no válida puede hacer que el servidor traduzca caracteres malintencionados de una solicitud a una respuesta, lo que provoca una denegación de servicio o XSS |
| JSON-ERROR | Error de codificación de JSON | Un cuerpo de solicitud de POST, PUT o PATCH que se especifica como que contiene JSON dentro del encabezado de solicitud &quot;Content-Type&quot;, pero que contiene errores de análisis de JSON. Esto suele estar relacionado con un error de programación o una solicitud automatizada o maliciosa. |
| MALFORMED-DATA | Datos mal formados en el cuerpo de la solicitud | Un cuerpo de solicitud de POST, PUT o PATCH con un formato incorrecto según el encabezado de solicitud &quot;Content-Type&quot;. Por ejemplo, si se especifica un encabezado de solicitud &quot;Content-Type: application/x-www-form-urlencoded&quot; y contiene un cuerpo de POST que es json. Esto suele ser un error de programación, una solicitud automatizada o maliciosa. Requiere agente 3.2 o superior. |
| SANS | Tráfico IP malintencionado | [Centro de tormentas de Internet SANS](https://isc.sans.edu/) lista de direcciones IP sobre las que se ha informado que han participado en actividades maliciosas |
| SIGSCI-IP | Efecto de red | IP marcada por SignalSciences: siempre que el motor de decisión marque una IP debido a una señal maliciosa, esa IP se propagará a todos los clientes. Las solicitudes posteriores de aquellas direcciones IP que contengan cualquier señal adicional durante la duración del indicador se registran |
| SIN CONTENIDO | Falta el encabezado de solicitud &quot;Content-Type&quot; | Una solicitud de POST, PUT o PATCH que no tiene un encabezado de solicitud &quot;Content-Type&quot;. De forma predeterminada, los servidores de aplicaciones deben suponer &quot;Content-Type: text/plain; charset=us-ascii&quot; en este caso. Es posible que a muchas solicitudes automatizadas y maliciosas les falte &quot;Tipo de contenido&quot;. |
| NOUA | No hay agente de usuario | Muchas solicitudes automatizadas y maliciosas utilizan agentes de usuario falsos o que faltan para dificultar la identificación del tipo de dispositivo que realiza las solicitudes. |
| TORNODO | Tráfico de Tor | Tor es un software que oculta la identidad de un usuario. Un pico en el tráfico de Tor puede indicar que un atacante está tratando de ocultar su ubicación. |
| NULLBYTE | Byte nulo | Los bytes nulos no suelen aparecer en una solicitud e indican que la solicitud tiene un formato incorrecto y es potencialmente maliciosa. |
| PRIVATEFILE | Archivos privados | Los archivos privados suelen ser de naturaleza confidencial, como un Apache `.htaccess` o un archivo de configuración que podría filtrar información confidencial |
| ESCÁNER | Escáner | Identifica los servicios y herramientas de digitalización más populares |
| RESPONSESPLIT | División de respuesta HTTP | Identifica cuándo se envían los caracteres CRLF como entrada a la aplicación para insertar encabezados en la respuesta HTTP |
| XML-ERROR | Error de codificación XML | Un cuerpo de solicitud de POST, PUT o PATCH que se especifica como que contiene XML dentro del encabezado de solicitud &quot;Content-Type&quot;, pero que contiene errores de análisis de XML. Esto suele estar relacionado con un error de programación o una solicitud automatizada o maliciosa. |

## Consideraciones {#considerations}

* Cuando se crean dos reglas en conflicto, las reglas de permiso siempre tienen prioridad sobre las reglas de bloque. Por ejemplo, si crea una regla para bloquear una ruta específica y una regla para permitir una dirección IP específica, se permitirán las solicitudes de esa dirección IP en la ruta bloqueada.

* Si una regla coincide y está bloqueada, la CDN responde con un `406` código de retorno.

* Los archivos de configuración no deben contener secretos, ya que cualquier persona que tenga acceso al repositorio de Git podrá leerlos.

* Las Listas de permitidos IP definidas en Cloud Manager tienen prioridad sobre las reglas de los filtros de tráfico.

* Las coincidencias de reglas WAF solo aparecen en los registros de CDN para los fallos y pasadas de CDN, no en las visitas.

## Ejemplos de reglas {#examples}

A continuación se muestran algunos ejemplos de reglas. Consulte la [sección de límite de tarifa](#rules-with-rate-limits) más abajo para ver ejemplos de reglas de límite de tipos.

**Ejemplo 1**

Esta regla bloquea las solicitudes procedentes de IP 192.168.1.1:

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

**Ejemplo 2**

Esta regla bloquea las solicitudes en la ruta `/helloworld` Al publicar con un agente de usuario que contiene Chrome:

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

**Ejemplo 3**

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

**Ejemplo 4**

Esta regla bloquea las solicitudes a la ruta `/block-me`y bloquea todas las solicitudes que coinciden con una `SQLI` o `XSS` patrón. Este ejemplo incluye reglas de filtro de tráfico WAF, que hace referencia a la variable `SQLI` y `XSS` [Indicadores WAF](#waf-flags-list)y, por lo tanto, requiere una licencia independiente.

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

**Ejemplo 5**

Esta regla bloquea el acceso a los países OFAC:

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

## Reglas de límite de velocidad {#rate-limits-rules}

A veces es deseable bloquear el tráfico si supera una cierta tasa de solicitudes entrantes, tal vez en función de una condición específica. Configurar un valor para `rateLimit` La propiedad limita la velocidad de las solicitudes que coinciden con la condición de regla.

Las reglas de límite de velocidad no pueden hacer referencia a indicadores WAF. Están disponibles para todos los clientes de Sites y Forms.

Los límites de tasa se calculan por POP de CDN. Por ejemplo, supongamos que los POP de Montreal, Miami y Dublín tienen tasas de tráfico de 80, 90 y 120 solicitudes por segundo respectivamente, y que la regla de límite de tasa está establecida en un límite de 100. En ese caso, solo el tráfico a Dublín estaría limitado por la tarifa.

### Estructura rateLimit {#ratelimit-structure}

| **Propiedad** | **Tipo** | **Predeterminado** | **SIGNIFICADO** |
|---|---|---|---|
| límite | entero de 10 a 10000 | required | Tasa de solicitudes (por POP de CDN) en solicitudes por segundo para las que se activa la regla. |
| ventana | enumeración de enteros: 1, 10 o 60 | 10 | Ventana de muestreo en segundos para la que se calcula la tasa de solicitud. La precisión de los contadores dependerá del tamaño de la ventana (ventana más grande, mayor precisión). Por ejemplo, se puede esperar una precisión del 50 % para la ventana de 1 segundo y del 90 % para la de 60 segundos. |
| penalización | entero de 60 a 3600 | 300 (5 minutos) | Período en segundos durante el cual se bloquean las solicitudes de coincidencia (redondeado al minuto más cercano). |
| groupBy | matriz[Getter] | ninguno | El contador del limitador de velocidad se agregará mediante un conjunto de propiedades de solicitud (por ejemplo, clientIp). |


### Ejemplos {#ratelimiting-examples}

**Ejemplo 1**

Esta regla bloquea un cliente durante 5 m cuando supera los 100 req/seg (por POP de CDN) en los últimos 60 s:

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
        groupBy:
          - reqProperty: clientIp
      action: block
```

**Ejemplo 2**

Bloquear solicitudes de 60 segundos en la ruta /crítico/recurso cuando supere los 100 req/s (por POP de CDN) en los últimos 60 segundos:

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
        rateLimit: { limit: 100, window: 60, penalty: 60 }
```

## Registros de CDN {#cdn-logs}

AEM El as a Cloud Service proporciona acceso a los registros de CDN, que son útiles para casos de uso, incluida la optimización de la proporción de visitas de caché y la configuración de reglas de filtro de tráfico. Los registros de CDN aparecen en Cloud Manager **Descargar registros** , al seleccionar el servicio de creación o publicación.

Tenga en cuenta que los registros de CDN pueden retrasarse hasta 5 minutos.

El `rules` describe qué reglas de filtro de tráfico coinciden y tiene el siguiente patrón:

```
"rules": "match=<matching-customer-named-rules-that-are-matched>,waf=<matching-WAF-rules>,action=<action_type>"
```

Por ejemplo:

```
"rules": "match=Block-Traffic-under-private-folder,Enable-SQL-injection-everywhere,waf="SQLI,SANS",action=block"
```

Las reglas se comportan de la siguiente manera:

* El nombre de regla declarado por el cliente de cualquier regla coincidente se enumerará en la variable `match` atributo.
* El `action` determina si las reglas tuvieron el efecto de bloquear, permitir o registrar.
* Si el WAF tiene licencia y está habilitado, la variable `waf` El atributo enumerará cualquier indicador WAF (por ejemplo, SQLI) que se haya detectado, independientemente de si los indicadores WAF se han enumerado en alguna regla. Esto sirve para conocer las posibles nuevas reglas que se pueden declarar.
* Si no coinciden las reglas declaradas por el cliente y no coinciden las reglas waf, la variable `rules` la propiedad estará en blanco.

Como se ha indicado anteriormente, las coincidencias de reglas WAF solo aparecen en los registros de CDN para errores y pasadas de CDN, no para visitas.

El ejemplo siguiente muestra un ejemplo `cdn.yaml` y dos entradas de registro de CDN:


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

## Herramientas del panel {#dashboard-tooling}

El Adobe de proporciona un mecanismo para descargar las herramientas del panel en el equipo para introducir registros de CDN descargados mediante Cloud Manager. Con esta herramienta, puede analizar el tráfico para determinar las reglas de filtro de tráfico apropiadas que se deben declarar, incluidas las reglas WAF.

Las herramientas de tablero se pueden clonar directamente desde el [AEMCS-CDN-Log-Analysis-ELK-Tool](https://github.com/adobe/AEMCS-CDN-Log-Analysis-ELK-Tool) Repositorio de GitHub.

[Consulte el tutorial](#tutorial) para obtener instrucciones concretas sobre cómo utilizar las herramientas de tablero.

## Reglas de inicio recomendadas {#recommended-starter-rules}

Puede copiar las reglas recomendadas a continuación en su `cdn.yaml` para empezar. Inicie en el modo de registro, analice el tráfico y, cuando esté satisfecho, cambie al modo de bloqueo. Es posible que desee modificar las reglas en función de las características únicas del tráfico en directo del sitio web.

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
          - SIGSCI-IP
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
        type: log
        wafFlags:
          - CMDEXE
```

## Tutorial {#tutorial}

[Trabajar con un tutorial](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/security/traffic-filter-and-waf-rules/overview.html) para obtener conocimientos prácticos y experiencia en torno a las reglas de filtro de tráfico.

El tutorial le guiará por:

* Configuración de la canalización de configuración de Cloud Manager
* Uso de herramientas para simular tráfico malintencionado
* Declarar reglas de filtro de tráfico, incluidas las reglas WAF
* Análisis de resultados con las herramientas de tablero
* Prácticas recomendadas
