---
title: Reglas de filtro de tráfico, incluidas las reglas WAF
description: Configuración de reglas de filtro de tráfico, incluidas las reglas de cortafuegos de aplicaciones web (WAF)
exl-id: 6a0248ad-1dee-4a3c-91e4-ddbabb28645c
source-git-commit: 221f6df73fe660c6f8dbf79affdccdd081ad3906
workflow-type: tm+mt
source-wordcount: '4210'
ht-degree: 1%

---


# Reglas de filtro de tráfico, incluidas las reglas WAF {#traffic-filter-rules-including-waf-rules}

>[!NOTE]
>
>Esta función aún no está disponible de forma general. Para unirse al programa de usuarios que lo adoptaron por anticipado, envíe un correo electrónico **aemcs-waf-adopter@adobe.com**, incluido el nombre de su organización y el contexto acerca de su interés en la función.

Las reglas de filtro de tráfico se pueden utilizar para bloquear o permitir solicitudes en la capa de CDN, lo que puede resultar útil en situaciones como las siguientes:

* Restricción del acceso a dominios específicos al tráfico interno de la compañía antes de que se active un nuevo sitio
* Establecimiento de límites de velocidad para ser menos propensos a ataques DDoS volumétricos
* Impedir que las direcciones IP que se sabe que son malintencionadas segmenten sus páginas

AEM Algunas de estas reglas de filtro de tráfico están disponibles para todos los clientes de Forms y sitios as a Cloud Service de. Funcionan principalmente en propiedades de solicitud y encabezados de solicitud, incluidos la IP, el nombre de host, la ruta y el agente de usuario.

Una subcategoría de reglas de filtro de tráfico requiere una licencia de seguridad mejorada o una licencia de seguridad de protección WAF-DDoS. Estas reglas poderosas se conocen como reglas de filtro de tráfico WAF (cortafuegos de aplicaciones web) (o reglas WAF para abreviar) y tienen acceso a [Indicadores WAF](#waf-flags-list) se describe más adelante en este artículo. Los clientes de Sites y Forms pueden ponerse en contacto con el equipo de su cuenta de Adobe para obtener más información sobre las licencias de esta capacidad avanzada.

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
* **Tutorial:** Conocimientos prácticos sobre la función, incluido cómo utilizar las herramientas del panel para declarar las reglas correctas.
<!-- About the tutorial: sets the context for a linked tutorial, which gives you practical knowledge about the feature, including how to use dashboard tooling to declare the right rules. -->

## Resumen de protección del tráfico {#traffic-protection-overview}

En el panorama digital actual, el tráfico malicioso es una amenaza constante. Reconocemos la gravedad del riesgo y ofrecemos varios enfoques para proteger las aplicaciones de los clientes y mitigar los ataques cuando se producen.

En el límite, la CDN administrada por Adobe absorbe los ataques DDoS en el nivel de red (capas 3 y 4), incluidos los ataques de inundación y reflexión/amplificación.

De forma predeterminada, el Adobe de toma medidas para evitar la degradación del rendimiento debido a ráfagas de tráfico inesperadamente alto que superan un determinado umbral. En caso de que un ataque DDoS afecte a la disponibilidad del sitio, los equipos de operaciones de Adobe reciben una alerta y toman medidas para mitigarlo.

Los clientes pueden tomar medidas proactivas para mitigar los ataques de la capa de aplicación (capa 7) configurando reglas en varios niveles del flujo de entrega de contenido.

Por ejemplo, en la capa de Apache, los clientes pueden configurar [módulo de dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=en#configuring-access-to-content-filter) o [ModSecurity](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/security/modsecurity-crs-dos-attack-protection.html?lang=en) para limitar el acceso a cierto contenido.

Y, como se describe en este artículo, las reglas de filtro de tráfico pueden implementarse en la CDN mediante la canalización de configuración de Cloud Manager. Además de las reglas de filtro de tráfico basadas en solicitudes de tráfico y en propiedades como la dirección IP, la ruta y los encabezados, los clientes también pueden obtener una licencia de una potente subcategoría de reglas de filtro de tráfico denominadas reglas WAF.

## Proceso sugerido {#suggested-process}

El siguiente es un proceso de extremo a extremo recomendado de alto nivel para crear las reglas de filtro de tráfico adecuadas:

1. Configure una canalización que no sea de producción y de configuración de producción, tal como se describe en la sección [Configurar](#setup) sección.
1. Los clientes que tengan licencia para la subcategoría de reglas de filtro de tráfico WAF deben habilitarlas en Cloud Manager.
1. Lea y pruebe el tutorial para comprender concretamente cómo utilizar las reglas de filtro de tráfico, incluidas las reglas WAF si se han autorizado. El tutorial lo acompaña en la implementación de reglas en un entorno de desarrollo, simulando tráfico malicioso y descargando [Registros de CDN](#cdn-logs)y analizándolos en [herramientas de tablero](#dashboard-tooling).
1. Copie las reglas iniciales recomendadas en `cdn.yaml` e implemente la configuración en producción en el modo de registro.
1. Después de recopilar un poco de tráfico, analice los resultados utilizando [herramientas de tablero](#dashboard-tooling) para ver si había alguna coincidencia. Busque los falsos positivos y realice los ajustes necesarios para activar finalmente las reglas predeterminadas en el modo de bloque.
1. Añada reglas personalizadas basadas en el análisis de los registros de CDN, probando primero el tráfico simulado en entornos de desarrollo antes de implementarlo en fase y producción en modo de registro y, a continuación, en modo de bloqueo.
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

1. Para configurar las reglas de WAF, WAF debe habilitarse en Cloud Manager, como se describe a continuación para los escenarios de programa nuevos y existentes. Tenga en cuenta que se debe adquirir una licencia independiente para WAF.

   1. Para configurar WAF en un nuevo programa, marque la **Protección WAF-DDOS** casilla de verificación de la **Seguridad** pestaña cuando [agregue un programa de producción.](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md)

   1. Para configurar WAF en un programa existente, [edición del programa](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/editing-programs.md) y en el **Seguridad** pestaña desmarque o marque **WAF-DDOS** en cualquier momento.

1. Para tipos de entorno distintos de RDE, cree una canalización de configuración de implementación de destino en Cloud Manager.

   * [Consulte este documento para canalizaciones de producción.](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md)
   * [Consulte este documento para canalizaciones que no sean de producción.](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md)

Para RDE, se utilizará la línea de comandos, pero RDE no es compatible en este momento.

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
| reqCookie | `string` | Devuelve una cookie con el nombre especificado |
| postParam | `string` | Devuelve el parámetro con el nombre especificado del cuerpo. Solo funciona cuando el cuerpo es de tipo de contenido `application/x-www-form-urlencoded` |

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

Esta regla bloquea las solicitudes a la ruta `/block-me`y bloquea todas las solicitudes que coinciden con una `SQLI` o `XSS` patrón. Este ejemplo incluye reglas de filtro de tráfico WAF, que hace referencia a la variable `SQLI` y `XSS` [Indicadores WAF](#waf-flags-list), que requieren una licencia independiente.

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

A veces es deseable bloquear el tráfico que coincida con una regla solo si la coincidencia supera una determinada tasa a lo largo del tiempo. Configurar un valor para `rateLimit` La propiedad limita la velocidad de las solicitudes que coinciden con la condición de regla.

Las reglas de límite de velocidad no pueden hacer referencia a indicadores WAF. Están disponibles para todos los clientes de Sites y Forms.

### Estructura rateLimit {#ratelimit-structure}

| **Propiedad** | **Tipo** | **Predeterminado** | **SIGNIFICADO** |
|---|---|---|---|
| límite | entero de 10 a 10000 | required | Tasa de solicitudes (por POP de CDN) en solicitudes por segundo para las que se activa la regla. |
| ventana | enumeración de enteros: 1, 10 o 60 | 10 | Ventana de muestreo en segundos para la que se calcula la tasa de solicitud. |
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

AEM El as a Cloud Service proporciona acceso a los registros de CDN, que son útiles para casos de uso, incluida la optimización de la proporción de visitas de caché y la configuración de reglas de CDN y WAF. Los registros de CDN aparecen en Cloud Manager **Descargar registros** , al seleccionar el servicio de creación o publicación.

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

* El nombre de regla declarado por el cliente de cualquier regla coincidente se enumerará en el atributo matches.
* El atributo action detalla si las reglas tuvieron el efecto de bloquear, permitir o registrar.
* Si el WAF tiene licencia y está habilitado, el atributo waf enumerará todas las reglas waf (por ejemplo, SQLI; tenga en cuenta que esto es independiente del nombre declarado por el cliente) que se detectaron, independientemente de si las reglas waf estaban enumeradas en la configuración.
* Si no coinciden las reglas declaradas por el cliente y no coinciden las reglas waf, la propiedad de atributo rules estará en blanco.

En general, las reglas coincidentes aparecen en la entrada de registro para todas las solicitudes a la CDN, independientemente de si se trata de una visita de CDN, una pasada o una omisión. Sin embargo, las reglas WAF aparecen en la entrada de registro solo para solicitudes a la CDN que se consideran errores o pasadas de CDN, pero no visitas de CDN.

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

## Tutorial {#tutorial}

El Adobe de proporciona un mecanismo para descargar las herramientas del panel en el equipo para introducir registros de CDN descargados mediante Cloud Manager. Con esta herramienta, puede analizar el tráfico para determinar las reglas de filtro de tráfico apropiadas que se deben declarar, incluidas las reglas WAF. En esta sección primero se proporcionan algunas instrucciones para familiarizarse con las herramientas de tablero en un entorno de desarrollo, seguidas de instrucciones sobre cómo aprovechar ese conocimiento para crear reglas en un entorno de producción.

Las herramientas de tablero se pueden clonar directamente desde el [AEMCS-CDN-Log-Analysis-ELK-Tool](https://github.com/adobe/AEMCS-CDN-Log-Analysis-ELK-Tool) Repositorio de GitHub.


### Familiarizarse con las herramientas de tablero {#dashboard-getting-familiar}

1. Cree una canalización de configuración de no producción de Cloud Manager asociada a un entorno de desarrollo. Seleccione primero la **Canalización de implementación** opción. A continuación seleccione **Implementación objetivo**, Config, el repositorio, la rama de Git y establezca la ubicación del código en /config.

   ![Agregar implementación de selección de canalización que no sea de producción](/help/security/assets/waf-select-pipeline1.png)

   ![Agregar canalización que no sea de producción y seleccionar segmentación](/help/security/assets/waf-select-pipeline2.png)

[Consulte este documento para obtener más información sobre la configuración de canalizaciones que no son de producción.](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md)

1. En el espacio de trabajo, cree una configuración de carpeta en el nivel raíz y añada un archivo denominado `cdn.yaml`, donde declarará una regla simple, configurándola en modo de registro en lugar de modo de bloqueo.

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  trafficFilters:
    rules:
    # Log request on simple path
    - name: log-rule-example
      when:
        allOf:
          - reqProperty: tier
            matches: "author|publish"
          - reqProperty: path
            equals: '/log/me'
      action: log
```

1. Confirme e inserte los cambios e implemente la configuración mediante la canalización de configuración.

   ![Ejecutar canalización de configuración](/help/security/assets/waf-run-pipeline.png)

1. Una vez implementada la configuración de, intente acceder a `https://publish-pXXXXX-eYYYYYY.adobeaemcloud.com/log/me` usando su navegador web o con el comando curl a continuación. Debe recibir una página de error 404, ya que esa página no existe.

   ```
   curl -svo /dev/null https://publish-pXXXXX-eYYYYYY.adobeaemcloud.com/log/me
   ```

1. Descargue los registros de CDN de Cloud Manager y valide que las reglas coinciden según lo esperado, con una propiedad rules que coincida con el nombre de la regla:

   ```
   "rules": "match=log-rule-example"
   ```

   ![Seleccionar registros de descarga](/help/security/assets/waf-download-logs1.png)

   ![Descargar registros](/help/security/assets/waf-download-logs2.png)

1. Cargue la imagen Docker con las herramientas del panel y siga el archivo LÉAME para introducir los registros de CDN. Como se muestra en las siguientes capturas de pantalla, seleccione el período de tiempo adecuado, el entorno adecuado y los filtros correctos.

   ![Seleccionar tiempo del panel](/help/security/assets/dashboard-select-time.png)

   ![Seleccionar entorno del panel](/help/security/assets/dashboard-select-env.png)

1. Una vez aplicados los filtros adecuados, debería poder ver un panel cargado con los datos esperados. En la captura de pantalla siguiente, el ejemplo de regla de registro se ha activado 3 veces en las últimas 2 horas, por la misma IP ubicada en Irlanda, utilizando un navegador web y una flexión.

   ![Ver datos del tablero de desarrollo](/help/security/assets/dashboard-see-data-logmode.png)
   ![Ver widgets de datos del tablero de desarrollo](/help/security/assets/dashboard-see-data-logmode2.png)

1. Ahora cambie cdn.yaml para poner la regla en modo de bloqueo y asegurar que las páginas estén bloqueadas, como se espera. A continuación, confirme, inserte y almacene en déclencheur la canalización de configuración como se hizo anteriormente.

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  trafficFilters:
    rules:
    # Log request on simple path
    - name: log-rule-example
      when:
        allOf:
          - reqProperty: tier
            matches: "author|publish"
          - reqProperty: path
            equals: '/log/me'
      action: block
```

1. Una vez implementada la configuración de, intente acceder a `https://publish-pXXXXX-eYYYYYY.adobeaemcloud.com/log/me` usando su navegador web o con el comando curl a continuación. Debe recibir una página de error 406 que indique que la solicitud se ha bloqueado.

   ```
   curl -svo /dev/null https://publish-pXXXXX-eYYYYYY.adobeaemcloud.com/log/me
   ```

1. Una vez más, descargue los registros de CDN en Cloud Manager (nota: Las nuevas solicitudes pueden tardar hasta 5 minutos en exponerse en los registros de CDN) e impórtelas en las herramientas de panel como lo hicimos anteriormente. Una vez finalizado, actualice el panel. Como puede ver en la captura de pantalla siguiente, solicita a `/log/me` están bloqueados por nuestra regla.

   ![Ver datos del tablero de producción](/help/security/assets/dashboard-see-data-blockmode.png)
   ![Ver datos del tablero de producción](/help/security/assets/dashboard-see-data-blockmode2.png)

1. Si tiene activados los filtros de tráfico WAF (se requiere una licencia adicional después de que la función sea GA), repita con una regla de filtro de tráfico WAF, en modo de registro, e implemente las reglas.

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  trafficFilters:
    rules:
      - name: log-waf-flags
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
```

1. Utilice una herramienta como [nikto](https://github.com/sullo/nikto/tree/master) para generar solicitudes coincidentes. El comando siguiente enviará unas 550 solicitudes malintencionadas en menos de 1 minuto.

   ```
   ./nikto.pl -useragent "MyAgent (Demo/1.0)" -D V -Tuning 9 -ssl -h https://publish-pXXXXX-eYYYYY.adobeaemcloud.com
   ```

1. Descargue los registros de CDN desde Cloud Manager (recuerde que pueden tardar hasta 5 minutos en aparecer) y compruebe que aparecen tanto las reglas declaradas coincidentes como los indicadores WAF.

   Como puede ver, varias de las peticiones producidas por Nikto están siendo marcadas por la WAF como maliciosas. Podemos ver que Nikto trató de explotar las vulnerabilidades CMDEXE, SQLI y NULLBYTE. Si ahora cambia la acción de registro a bloqueo y vuelve a realizar el déclencheur de un análisis con Nikto, todas las solicitudes marcadas anteriormente se bloquearán en este momento.

   ![Ver datos WAF](/help/security/assets/dashboard-see-data-waf.png)


   Tenga en cuenta que cuando una solicitud coincida con cualquiera de los indicadores WAF, aparecerán esos indicadores WAF, aunque no formen parte de la regla declarada; de este modo, siempre tendrá en cuenta el posible tráfico malintencionado nuevo, para el que aún no ha declarado reglas coincidentes. A modo de ejemplo:

   ```
   "rules": "match=log-waf-flags,waf=SQLI,action=blocked"
   ```

1. Repita el proceso con una regla que utilice límites de velocidad en el modo de registro. Como siempre, confirme, inserte y almacene en déclencheur la canalización de configuración para aplicar la configuración.

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
          limit: 10
          window: 1
          penalty: 60
          groupBy:
            - reqProperty: clientIp
        action: log
```

1. Utilice una herramienta como [Vegeta](https://github.com/tsenart/vegeta) para generar tráfico.

   ```
   echo "GET https://publish-pXXXXX-eYYYYYY.adobeaemcloud.com" | vegeta attack -duration=5s | tee results.bin | vegeta report
   ```

1. Después de ejecutar la herramienta, puede descargar registros de CDN e introducirlos en el panel para verificar que se ha activado la regla del limitador de velocidad

   ![Ver datos WAF](/help/security/assets/waf-dashboard-ratelimiter-1.png)

   ![Ver datos WAF](/help/security/assets/waf-dashboard-ratelimiter-2.png)

   Como puedes ver en nuestra regla **limit-requests-client-ip** se ha activado.

   Ahora que está familiarizado con el funcionamiento de las reglas de filtro de tráfico, puede pasar al entorno de producción.

### Implementación de reglas en el entorno de producción {#dashboard-prod-env}

Asegúrese de declarar inicialmente las reglas en el modo de registro para validar que no hay falsos positivos, lo que significa tráfico legítimo que se bloquearía incorrectamente.

1. Cree una canalización de configuración de producción asociada a su entorno de producción.

1. Copie las reglas recomendadas a continuación en su cdn.yaml. Es posible que desee modificar las reglas en función de las características únicas del tráfico en directo del sitio web. Confirme, inserte y almacene en déclencheur su canalización de configuración. Asegúrese de que las reglas estén en modo de registro.

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev"]
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
    # Enable recommended WAF protections (only works if WAF is enabled for your environment)
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
    # Disable protection against CMDEXE on /bin
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

1. Añada reglas adicionales para bloquear el tráfico malintencionado que pueda conocer. Por ejemplo, ciertas direcciones IP que han estado atacando el sitio.

1. Después de unos minutos, horas o días, según el volumen de tráfico del sitio, descargue los registros de CDN de Cloud Manager y analícelos con el panel.

1. Estas son algunas consideraciones:
   1. Las reglas declaradas que coinciden con el tráfico aparecen en los gráficos y registros de solicitudes para que pueda comprobar fácilmente si se están activando las reglas declaradas.
   1. El tráfico que coincide con los indicadores WAF aparece en gráficos y registros de solicitudes, incluso si no los ha registrado en una regla. De este modo, siempre tendrá en cuenta el posible tráfico malintencionado nuevo y podrá crear nuevas reglas según sea necesario. Observe los indicadores WAF que no se reflejan en las reglas declaradas y considere la posibilidad de declararlos.
   1. Para las reglas de coincidencia, inspeccione los registros de solicitud para ver si hay falsos positivos y si puede filtrarlos fuera de las reglas. Por ejemplo, puede que sean un falso positivo solo para determinadas rutas.

1. Establezca las reglas adecuadas en modo de bloque y considere también la posibilidad de agregar reglas adicionales. Tal vez algunas de las reglas deberían permanecer en el modo de registro a medida que analiza más con más tráfico.

1. Vuelva a implementar la configuración.

1. Itere y analice los paneles con frecuencia.

