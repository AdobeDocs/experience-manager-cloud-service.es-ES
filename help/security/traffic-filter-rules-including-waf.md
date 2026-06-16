---
title: Reglas de filtro de tráfico, incluidas reglas WAF
description: Configuración de las reglas de filtro de tráfico, incluidas las reglas de cortafuegos de la aplicación web (WAF).
exl-id: 6a0248ad-1dee-4a3c-91e4-ddbabb28645c
feature: Security
role: Admin
source-git-commit: 2976da7d7032a40912d9822816788fcdc95d828d
workflow-type: tm+mt
source-wordcount: '4268'
ht-degree: 68%

---


# Reglas de filtro de tráfico, incluidas las reglas WAF {#traffic-filter-rules-including-waf-rules}

Las reglas de filtro de tráfico bloquean o permiten solicitudes en la capa de CDN, lo que resulta útil en situaciones como las siguientes:

* Restringir el acceso a dominios específicos al tráfico interno de la compañía antes de que se active un nuevo sitio.
* Para ser menos susceptible a los ataques volumétricos de denegación de servicio, establezca límites de velocidad.
* Impedir que las direcciones IP que se sabe que son malintencionadas segmenten sus páginas.


La mayoría de estas reglas de filtro de tráfico están disponibles para todos los clientes Sites y Forms de AEM as a Cloud Service. Como *reglas estándar de filtro de tráfico*, funcionan en propiedades de solicitud: IP, nombre de host, ruta y agente de usuario. Las reglas de filtro de tráfico estándar incluyen reglas de límite de velocidad para evitar picos de tráfico.

Una subcategoría de reglas de filtro de tráfico requiere una licencia de Seguridad extendida (anteriormente denominada Protección WAF-DDoS) o Seguridad extendida para atención médica (anteriormente denominada Seguridad mejorada). Estas reglas poderosas se conocen como reglas de filtro de tráfico de WAF (Web Application Firewall) (o *reglas de WAF*) y tienen acceso a las [marcas de WAF](#waf-flags-list) que se describen más adelante en este artículo.

Las reglas de filtro de tráfico se pueden implementar mediante canalizaciones de configuración de Cloud Manager para los tipos de entorno de desarrollo, ensayo y producción. El archivo de configuración se puede implementar en Entornos de desarrollo rápido (RDE) mediante herramientas de línea de comandos.

Para obtener experiencia sobre esta característica rápidamente, [complete un tutorial](#tutorial).

>[!NOTE]
>Para obtener opciones de configuración de tráfico de CDN adicionales, como la edición de solicitudes/respuestas, la declaración de redirecciones y el proxy a orígenes que no son de AEM, consulte el artículo [Configuración del tráfico en CDN](/help/implementing/dispatcher/cdn-configuring-traffic.md).


## Organización de este artículo {#how-organized}

Este artículo está organizado en las secciones siguientes:

* **Información general sobre protección del tráfico:** descubra cómo está protegido contra el tráfico malintencionado.
* **Proceso sugerido para configurar reglas:** conozca una metodología de alto nivel para proteger su sitio web.
* **Configuración:** Descubra cómo configurar e implementar reglas de filtro de tráfico, incluidas las reglas avanzadas de WAF.
* **Sintaxis de reglas:** obtenga información sobre cómo declarar reglas de filtro de tráfico en el archivo de configuración de `cdn.yaml`. Esto incluye las reglas de filtro de tráfico disponibles para todos los clientes de Sites y Forms, y la subcategoría de reglas WAF para aquellos que otorgan licencia a esa funcionalidad.
* **Ejemplos de reglas:** Para empezar, vea ejemplos de reglas declaradas.
* **Reglas de límite de volumen:** aprenda a utilizar reglas de limitación de volumen para proteger el sitio de ataques de gran volumen.
* **Alertas de reglas de filtro de tráfico:** configure alertas para recibir notificaciones cuando se activen las reglas.
* **Pico de tráfico predeterminado en la alerta de origen:** Reciba una notificación cuando haya un aumento de tráfico en el origen que sugiera un ataque DDoS.
* **Registros de CDN:** compruebe qué reglas declaradas e indicadores WAF coinciden con el tráfico.
* **Herramientas del panel de control:** analice los registros de CDN para crear nuevas reglas de filtro de tráfico.
* **Reglas de inicio recomendadas:** un conjunto de reglas para empezar.
* **Tutorial:** Información sobre la característica, incluido cómo usar las herramientas del panel para declarar las reglas apropiadas.

## Resumen de protección del tráfico {#traffic-protection-overview}

En el panorama digital actual, el tráfico malicioso es una amenaza constante. Adobe reconoce la gravedad del riesgo y ofrece varios enfoques para proteger las aplicaciones de los clientes y mitigar los ataques cuando se producen.

En la periferia, la CDN administrada por Adobe absorbe los ataques DoS en el nivel de red (capas 3 y 4), incluidos los ataques de inundación y reflexión/amplificación.

De forma predeterminada, Adobe toma medidas para evitar la degradación del rendimiento debido a ráfagas de tráfico inesperadamente altas que superan un determinado umbral. Si hay un ataque de DoS que afecte a la disponibilidad del sitio, los equipos de operaciones de Adobe reciben una alerta y toman medidas para mitigarlo.

Los clientes toman medidas proactivas para mitigar los ataques de la capa de aplicación (capa 7) configurando reglas en varios niveles del flujo de entrega de contenido.

Por ejemplo, en la capa de Apache, los clientes configuran [Dispatcher module](https://experienceleague.adobe.com/es/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration#configuring-access-to-content-filter) o [ModSecurity](https://experienceleague.adobe.com/es/docs/experience-manager-learn/foundation/security/modsecurity-crs-dos-attack-protection) para limitar el acceso a cierto contenido.

Como se describe en este artículo, las reglas de filtro de tráfico se implementan en la CDN administrada por Adobe mediante las [canalizaciones de configuración](/help/operations/config-pipeline.md) de Cloud Manager. Más allá de *las reglas estándar de filtro de tráfico* (IP, ruta, encabezados, límites de tasa), los clientes obtienen la licencia de *reglas de WAF*.

## Proceso sugerido {#suggested-process}

El siguiente es un proceso de extremo a extremo recomendado de alto nivel para determinar las reglas de filtro de tráfico correctas:

1. Configure las canalizaciones de configuración de producción y las que no son de producción, tal como se describe en la sección [Configuración](#setup).
1. Los clientes que tienen licencia para *reglas de filtro de tráfico de WAF* las habilitan en Cloud Manager.

   >[!IMPORTANT]
   >
   >Las reglas de WAF de licencias *no las* activan. La función permanece inactiva hasta que **Protección WAF-DDOS** esté marcada en la ficha **Seguridad** de Cloud Manager. Consulte [Crear programas de producción](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md) o [Editar programas](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/editing-programs.md) para habilitar la característica.

1. Lea y complete el tutorial para comprender cómo utilizar las reglas de filtro de tráfico, incluidas las reglas de WAF si se han autorizado. El tutorial le guía por la implementación de reglas en un entorno de desarrollo, simulando tráfico malicioso y descargando [registros de CDN](#cdn-logs) y analizándolos en [herramientas de panel de control](#dashboard-tooling).
1. Copie las reglas de inicio recomendadas en `cdn.yaml` e implemente la configuración en el entorno de producción con algunas de las reglas en modo de registro.
1. Después de recopilar un poco de tráfico, analice los resultados utilizando las [herramientas de tablero](#dashboard-tooling) para ver si hay alguna coincidencia. Compruebe si hay falsos positivos y realice los ajustes necesarios para activar finalmente todas las reglas de inicio en el modo de bloqueo.
1. Añada reglas personalizadas basadas en el análisis de los registros de la CDN, probando primero con tráfico simulado en entornos de desarrollo antes de implementarlas en los entornos de ensayo y producción en modo de registro y, a continuación, en el modo de bloqueo.
1. Supervise el tráfico de forma continua y realice cambios en las reglas a medida que evoluciona el panorama de amenazas.

## Configuración {#setup}

1. Cree un archivo `cdn.yaml` con un conjunto de reglas de filtro de tráfico, incluidas las reglas WAF. Por ejemplo:

   ```
   kind: "CDN"
   version: "1"
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

   Consulte [Uso de canalizaciones de configuración](/help/operations/config-pipeline.md#common-syntax) para obtener una descripción de las propiedades que aparecen por encima del nodo `data`. El valor de la propiedad `kind` debe establecerse en *CDN* y la versión en `1`.


1. Si las reglas de WAF tienen licencia, *debe* habilitar la característica en Cloud Manager. Las reglas de WAF con licencia no están activas y no proporcionan protección hasta que se compruebe **Protección WAF-DDOS**. Habilite la función tanto para los escenarios de programa nuevos como para los existentes, tal como se describe a continuación:

   1. Para configurar WAF en un nuevo programa, marque la casilla **Protección WAF-DDOS** en la pestaña **Seguridad** cuando [cree un programa de producción](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md).

   1. Para configurar WAF en un programa existente, [edite su programa](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/editing-programs.md). En la ficha **Seguridad**, marque la opción **Protección WAF-DDOS** para habilitar la característica o desmárquela para deshabilitarla. Puede cambiar esta configuración en cualquier momento.

      Para confirmar que la función está *activa* después de habilitarla, revise los [registros de CDN](#cdn-logs) una vez que el tráfico fluya al sitio. Busque entradas de registro que incluyan una propiedad `rules` que contenga un atributo `waf`. Por ejemplo:

      `"rules": "waf=SQLI" `

      Este atributo aparece una vez que WAF está activo, incluso antes de que se implementen las reglas de WAF.

1. Cree una canalización de configuración en Cloud Manager, tal como se describe en el [artículo sobre la canalización de configuración](/help/operations/config-pipeline.md#managing-in-cloud-manager). La canalización hace referencia a una carpeta de nivel superior `config` con el archivo `cdn.yaml` colocado en algún lugar por debajo. Consulte [Uso de canalizaciones de configuración](/help/operations/config-pipeline.md#folder-structure).

## Sintaxis de reglas de filtro de tráfico {#rules-syntax}

Para hacer coincidir patrones como IP, agente de usuario, encabezados, nombre de host, ubicación geográfica o URL, puede configurar *reglas de filtro de tráfico*.

Los clientes con una licencia de seguridad extendida o seguridad extendida para atención médica deben configurar *reglas de WAF* que hagan referencia a [indicadores de WAF](#waf-flags-list).

Este es un ejemplo de un conjunto de reglas de filtro de tráfico, que también incluye una regla WAF.

```
kind: "CDN"
version: "1"
data:
  trafficFilters:
    rules:
      - name: "path-rule"
        when:
          allOf:
            - { reqProperty: path, equals: /block-me }
            - { reqProperty: tier, equals: publish }
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
| when | X | X | `Condition` | - | La estructura básica es:<br><br>`{ <getter>: <value>, <predicate>: <value> }`<br><br>Consulte [Estructura de condiciones](/help/implementing/dispatcher/cdn-configuring-traffic.md#condition-structure) en *Configuración del tráfico en CDN* para obtener información acerca de captadores, predicados y cómo combinar varias condiciones. |
| acción | X | X | `Action` | log | objeto log, allow, block o Action. El valor predeterminado es log |
| rateLimit | X |   | `RateLimit` | sin definir | Configuración del límite de volumen. La limitación de volumen está deshabilitada si no se define.<br><br>Hay una sección independiente más abajo que describe la sintaxis de rateLimit, junto con ejemplos. |

### Estructura de acción {#action-structure}

Una `action` puede ser una cadena que especifique la acción (permitir, bloquear o registrar) o un objeto compuesto por el tipo de acción (permitir, bloquear o registrar) y opciones como wafFlags y/o estado.

**Tipos de acción**

Las acciones se priorizan según sus tipos en la siguiente tabla, que se ordena para reflejar el orden en el que se ejecutan las acciones:

| **Nombre** | **Propiedades permitidas** | **Significado** |
|---|---|---|
| **permitir** | `wafFlags` (opcional), `alert` (opcional) | si wafFlags no está presente, detiene el procesamiento posterior de la regla y procede a proporcionar la respuesta. Si wafFlags está presente, deshabilita las protecciones WAF especificadas y continúa con el procesamiento de la regla. <br>Si se especifica una alerta, se envía una notificación del Centro de acciones si la regla se activa 10 veces en un intervalo de 5 minutos. Una vez que se activa una alerta para una regla en particular, no se activará de nuevo hasta el día siguiente (UTC). |
| **block** | `status, wafFlags` (opcional y mutuamente excluyente), `alert` (opcional) | si wafFlags no está presente, devuelve un error HTTP omitiendo todas las demás propiedades, el código de error se define mediante la propiedad estado o el valor predeterminado es 406. Si wafFlags está presente, permite protecciones WAF especificadas y continúa con el procesamiento de la regla. <br>Si se especifica una alerta, se envía una notificación del Centro de acciones si la regla se activa 10 veces en un intervalo de 5 minutos. Una vez que se activa una alerta para una regla en particular, no se activará de nuevo hasta el día siguiente (UTC). |
| **registro** | `wafFlags` (opcional), `alert` (opcional) | registra el hecho de que la regla se activó; de lo contrario, no afecta al procesamiento. wafFlags no tiene ningún efecto. <br>Si se especifica una alerta, se envía una notificación del Centro de acciones si la regla se activa 10 veces en un intervalo de 5 minutos. Una vez que se activa una alerta para una regla en particular, no se activará de nuevo hasta el día siguiente (UTC). |

### Lista de marcas de WAF {#waf-flags-list}

La propiedad `wafFlags`, utilizada en las reglas de filtro de tráfico de WAF con licencia, hace referencia a lo siguiente:

#### Tráfico malintencionado

| **Identificador de marca** | **Nombre de indicador** | **Descripción** |
|---|---|---|
| ATAQUE | Ataque | Una agregación de indicadores relacionados con tráfico malintencionado (SQLI, CMDEXE, XSS, etc.). Consulte la [sección de reglas WAF recomendadas](#recommended-waf-starter-rules) para ver cómo se puede usar este indicador de forma eficaz. |
| ATTACK-FROM-BAD-IP | Ataque desde IP incorrecta | Es similar al indicador ATTACK, pero se ha añadido &quot;el operador AND lógico&quot; al indicador `BAD-IP`, de modo que una solicitud se marca si coincide con ATTACK y BAD-IP. Consulte la [sección de reglas WAF recomendadas](#recommended-waf-starter-rules) para ver cómo se puede usar este indicador de forma eficaz. |
| SQLI | Inyección de SQL | La inyección de SQL es el intento de obtener acceso a una aplicación o de obtener información privilegiada ejecutando consultas de base de datos arbitrarias. |
| PUERTA TRASERA | Puerta trasera | Una señal de puerta trasera es una solicitud que intenta determinar si hay un archivo de puerta trasera común en el sistema. |
| CMDEXE | Ejecución de comandos | La ejecución de comandos es el intento de obtener control o dañar un sistema objetivo a través de comandos arbitrarios del sistema por medio de la entrada del usuario. |
| CMDEXE-NO-BIN | Ejecución de comandos excepto en `/bin/` | Proporciona el mismo nivel de protección que `CMDEXE` a la vez que deshabilita falsos positivos en `/bin` debido a la arquitectura AEM. |
| XSS | Scripts en sitios múltiples | La ejecución de scripts en sitios múltiples es el intento de apropiarse de la cuenta de un usuario o de una sesión de exploración web mediante código JavaScript malintencionado. |
| TRAVERSAL | Traversal de directorios | Traversal de directorios es el intento de navegar por carpetas privilegiadas a través de un sistema con la esperanza de obtener información confidencial. |
| USERAGENT | Herramienta de ataque | La herramienta de ataque es el uso de software automatizado para identificar vulnerabilidades de seguridad o para intentar explotar una vulnerabilidad descubierta. |
| LOG4J-JNDI | Log4J JNDI | Los ataques Log4J JNDI intentan explotar la [vulnerabilidad de Log4Shell](https://en.wikipedia.org/wiki/Log4Shell) presente en las versiones de Log4J anteriores a la versión 2.16.0 |
| CVE | CVE | Indicador que identifica una CVE. Siempre se combina con un indicador `CVE-<CVE Number>`. Póngase en contacto con Adobe para obtener más información sobre las CVE de las que Adobe le protegerá. |

#### Tráfico sospechoso

| **Identificador de marca** | **Nombre de indicador** | **Descripción** |
|---|---|---|
| ABNORMALPATH | Ruta anormal | Ruta anormal indica que la ruta original difiere de la ruta normalizada (por ejemplo, `/foo/./bar` se normaliza a `/foo/bar`) |
| BAD-IP | IP incorrecta | Identifica solicitudes procedentes de direcciones IP que se sabe que son malintencionadas, ya sea debido a la inclusión en conjuntos de datos como `SANS` y `TORNODE`, o en función de que WAF haya detectado previamente un comportamiento malintencionado |
| BHH | Encabezados de salto incorrecto | Los encabezados de salto incorrecto indican un intento de introducir HTTP a través de un encabezado Transfer-Encoding (TE) o Content-Length (CL) mal formado o un encabezado TE y CL bien formado |
| CODEINJECTION | Inyección de código | La inyección de código es el intento de obtener control o dañar un sistema de destino a través de comandos arbitrarios del código de aplicación por medio de la entrada del usuario. |
| COMPRESSED | Compresión detectada | El cuerpo de la petición POST está comprimido y no se puede inspeccionar. Por ejemplo, si se especifica un encabezado de solicitud `Content-Encoding: gzip` y el cuerpo de POST no es texto sin formato. |
| RESPONSESPLIT | División de respuesta HTTP | Identifica cuándo se envían los caracteres CRLF como entrada a la aplicación para insertar encabezados en la respuesta HTTP |
| NOTUTF8 | Codificación no válida | La codificación no válida puede hacer que el servidor traduzca caracteres malintencionados de una solicitud a una respuesta, lo que provoca una denegación de servicio o XSS |
| MALFORMED-DATA | Datos mal formados en el cuerpo de la solicitud | Un cuerpo de solicitud POST, PUT o PATCH con un formato incorrecto según el encabezado de solicitud &quot;Content-Type&quot;. Por ejemplo, si se especifica un encabezado de solicitud &quot;Content-Type: application/x-www-form-urlencoded&quot; y contiene un cuerpo POST que es json. Esto suele ser un error de programación, una solicitud automatizada o maliciosa. Requiere agente 3.2 o superior. |
| SANS | Tráfico IP malintencionado | [Centro de tormentas de Internet SANS](https://isc.sans.edu/): lista de direcciones IP notificadas que han participado en actividades maliciosas. |
| NO-CONTENT-TYPE | Falta el encabezado de solicitud &quot;Content-Type&quot; | Una solicitud POST, PUT o PATCH que no tiene un encabezado de solicitud &quot;Content-Type&quot;. De forma predeterminada, los servidores de aplicaciones deben suponer &quot;Content-Type: text/plain; charset=us-ascii&quot; en este caso. Es posible que a muchas solicitudes automatizadas y maliciosas les falte &quot;Tipo de contenido&quot;. |
| NOUA | No hay agente de usuario | Indica que una solicitud no contiene un encabezado “Agente-Usuario” o que el valor del encabezado no se ha establecido. |
| NULLBYTE | Byte nulo | Los bytes nulos no suelen aparecer en una solicitud e indican que la solicitud tiene un formato incorrecto y es potencialmente maliciosa. |
| OOB-DOMAIN | Dominio fuera de banda | Los dominios fuera de banda generalmente se utilizan durante las pruebas de penetración para identificar vulnerabilidades en las que se permite el acceso a la red. |
| PRIVATEFILE | Archivos privados | Los archivos privados suelen ser de naturaleza confidencial, como un archivo `.htaccess` Apache o un archivo de configuración que podría filtrar información confidencial |
| ESCÁNER | Escáner | Identifica los servicios y herramientas de digitalización más populares |

#### Tráfico varios

| **Identificador de marca** | **Nombre de indicador** | **Descripción** |
|---|---|---|
| CENTRO DE DATOS | Centro de datos | Identifica la solicitud como procedente de un proveedor de alojamiento conocido. Este tipo de tráfico no suele estar asociado a un usuario final real. |
| DOUBLEENCODING | Codificación doble | La codificación doble comprueba la técnica de evasión de los caracteres HTML de doble codificación |
| JSON-ERROR | Error de codificación de JSON | Un cuerpo de solicitud POST, PUT o PATCH que se especifica que contiene JSON dentro del encabezado de solicitud &quot;Content-Type&quot;, pero que contiene errores de análisis de JSON. Esto suele estar relacionado con un error de programación o una solicitud automatizada o maliciosa. |
| TORNODE | Tráfico de Tor | Tor es un software que oculta la identidad de un usuario. Un pico en el tráfico de Tor puede indicar que un atacante está tratando de ocultar su ubicación. |
| XML-ERROR | Error de codificación XML | Un cuerpo de solicitud POST, PUT o PATCH que se especifica que contiene XML dentro del encabezado de solicitud &quot;Content-Type&quot;, pero que contiene errores de análisis de XML. Esto suele estar relacionado con un error de programación o una solicitud automatizada o maliciosa. |

## Consideraciones {#considerations}

* Cuando se crean dos reglas en conflicto, las reglas permitidas siempre tienen prioridad sobre las reglas de bloqueo. Por ejemplo, si crea una regla para bloquear una ruta específica y una regla para permitir una dirección IP específica, se permiten las solicitudes de esa dirección IP en la ruta bloqueada.

* Si una regla coincide y está bloqueada, CDN responde con un código de retorno `406`.

* Los archivos de configuración no contienen secretos porque los puede leer cualquier persona que tenga acceso al repositorio de Git.

* Las listas de IP permitidas definidas en Cloud Manager tienen prioridad sobre las reglas de los filtros de tráfico.

* Las coincidencias de reglas WAF solo aparecen en los registros CDN para los errores y aprobaciones de CDN, no en los aciertos.

## Ejemplos de reglas {#examples}

A continuación se muestran algunos ejemplos de reglas. Consulte la [sección sobre límite de volumen](#rate-limit-rules) a continuación para ver ejemplos de reglas de límite de volumen.

**Ejemplo: 1**

Esta regla bloquea las solicitudes procedentes de la **IP192.168.1.1**:

```
kind: "CDN"
version: "1"
data:
  trafficFilters:
     rules:
       - name: "block-request-from-ip"
         when: { reqProperty: clientIp, equals: "192.168.1.1" }
         action:
           type: block
```

**Ejemplo 2**

Esta regla bloquea las solicitudes a la ruta `/helloworld` en la publicación con un agente de usuario que contenga Chrome:

```
kind: "CDN"
version: "1"
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

Esta regla bloquea solicitudes en la publicación que contienen el parámetro de consulta `foo`, pero permite todas las solicitudes procedentes de la IP 192.168.1.1:

```
kind: "CDN"
version: "1"
data:
  trafficFilters:
    rules:
      - name: "block-request-that-contains-query-parameter-foo"
        when:
          allOf:
            - { queryParam: url-param, equals: foo }
            - { reqProperty: tier, equals: publish }
        action:
          type: block
      - name: "allow-all-requests-from-ip"
        when: { reqProperty: clientIp, equals: 192.168.1.1 }
        action:
          type: allow
```

**Ejemplo: 4**

Esta regla bloquea las solicitudes a la ruta `/block-me` en la publicación y bloquea todas las solicitudes que coinciden con un patrón `SQLI` o `XSS`. Este ejemplo incluye una regla de filtro de tráfico de WAF, que hace referencia a `SQLI` y a `XSS` [WAF Flags](#waf-flags-list), y requiere por lo tanto una licencia independiente.

```
kind: "CDN"
version: "1"
data:
  trafficFilters:
    rules:
      - name: "path-rule"
        when:
          allOf:
            - { reqProperty: path, equals: /block-me }
            - { reqProperty: tier, equals: publish }
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

## Reglas de límite de tarifa

A veces es deseable bloquear el tráfico si supera un cierto volumen de solicitudes entrantes, en función de una condición específica. Configurar un valor para la propiedad `rateLimit` limita el volumen de las solicitudes que coinciden con la condición de la regla.

Las reglas de límite de volumen no pueden hacer referencia a indicadores WAF. Están disponibles para todos los clientes de Sites y Forms.

Los límites de volumen se calculan por CDN POP. Por ejemplo, supongamos que los POP de Montreal, Miami y Dublín tienen volúmenes de tráfico de 80, 90 y 120 solicitudes por segundo, respectivamente. Y la regla de límite de volúmenes se establece en un límite de 100. En ese caso, solo el tráfico a Dublín está limitado por la tarifa.

Los límites de velocidad se evalúan en función del tráfico que llega al borde, el tráfico que llega al borde o el número de errores.

### estructura de rateLimit {#ratelimit-structure}

| **Propiedad** | **Tipo** | **Predeterminado** | **SIGNIFICADO** |
|---|---|---|---|
| limit | entero de 10 a 10000 | Requerido | Volumen de solicitud (por CDN POP) en solicitudes por segundo para las que se activa la regla. |
| ventana | integer enum: 1, 10 o 60 | 10 | Ventana de muestreo en segundos para la que se calcula el volumen de solicitud. La precisión de los contadores dependerá del tamaño de la ventana (ventana más grande, mayor precisión). Por ejemplo, se puede esperar una precisión del 50 % para la ventana de 1 segundo y del 90 % para la de 60 segundos. |
| penalty | entero de 60 a 3600 | 300 (5 minutos) | Período en segundos durante el cual se bloquean las solicitudes de coincidencia (redondeado al minuto más próximo). |
| recuento | todo, recuperaciones, errores | todo | evaluar en función del tráfico del borde (todo), el tráfico de origen (recuperaciones) o el número de errores (errores). |
| groupBy | array[Getter] | ninguno | El contador de limitador de volumen se añadirá mediante un conjunto de propiedades de solicitud (por ejemplo, clientIp). |

### Ejemplos {#ratelimiting-examples}

**Ejemplo 1**

Esta regla bloquea a un cliente durante 5 minutos cuando supera un promedio de 60 req/seg (por POP de CDN) en los últimos 10 segundos:

```
kind: "CDN"
version: "1"
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

**Ejemplo 2**

Bloquee solicitudes en la ruta /critical/resource durante 60 segundos cuando supere un promedio de 100 solicitudes hasta el origen por segundo (por cada CDN POP) en un intervalo de tiempo de 10 segundos:

```
kind: "CDN"
version: "1"
data:
  trafficFilters:
    rules:
      - name: rate-limit-example
        when:
          allOf:
            - { reqProperty: path, equals: /critical/resource }
            - { reqProperty: tier, equals: publish }
        action:
          type: block
        rateLimit: { limit: 100, window: 10, penalty: 60, count: fetches }
```

Para obtener fragmentos de código adicionales para escenarios avanzados, consulte el artículo [Fragmentos de configuración de CDN para escenarios comunes](/help/implementing/dispatcher/cdn-configuration-snippets-common-scenarios.md).

## Reglas de CVE {#cve-rules}

Si WAF tiene licencia, Adobe aplica automáticamente reglas de bloqueo para protegerse contra muchas CVE conocidas (Vulnerabilidades y exposiciones comunes) y se añaden nuevas CVE poco después de descubrirse. Los clientes no configuran las reglas CVE por sí mismos.

Si una solicitud de tráfico coincide con una CVE, aparece en la entrada de registro de CDN correspondiente.

Póngase en contacto con el servicio de asistencia de Adobe si tiene preguntas sobre un CVE en particular o si hay una regla CVE en particular que su organización desea deshabilitar.

## Alertas de reglas de filtro de tráfico {#traffic-filter-rules-alerts}

Se puede configurar una regla para enviar una notificación del Centro de acciones si se activa 10 veces en un intervalo de 5 minutos. Esta regla le alerta cuando se producen ciertos patrones de tráfico para que pueda tomar las medidas necesarias. Una vez activada una alerta para una regla en particular, no vuelve a almacenar en déclencheur hasta el día siguiente (UTC).

Obtenga más información sobre el [Centro de acciones](/help/operations/actions-center.md), incluyendo cómo configurar los perfiles de notificación necesarios para recibir correos electrónicos.

![Notificación del Centro de acciones](/help/security/assets/traffic-filter-rules-actions-center-alert.png)


La propiedad alerta se puede aplicar al nodo de acción para todos los tipos de acción (allow, block, log).

```
kind: "CDN"
version: "1"
data:
  trafficFilters:
    rules:
      - name: "path-rule"
        when:
          allOf:
            - { reqProperty: path, equals: /block-me }
            - { reqProperty: tier, equals: publish }
        action:
          type: block
          alert: true
```

## Pico de tráfico predeterminado en la alerta de origen {#traffic-spike-at-origin-alert}

Una notificación por correo electrónico de [Centro de acciones](/help/operations/actions-center.md) le avisa cuando hay mucho tráfico de la misma dirección IP que entra en el origen, lo que sugiere un ataque DDoS.

Si se alcanza este umbral, Adobe bloquea el tráfico desde esa dirección IP. Tome medidas adicionales para proteger su origen, como configurar las reglas de filtro de tráfico de límite de velocidad. Consulte el tutorial [Bloqueo de ataques DoS y DDoS mediante reglas de tráfico](#tutorial-blocking-DDoS-with-rules) para obtener una guía guiada.

El sistema habilita esta alerta de forma predeterminada, pero puede deshabilitarla con la propiedad *defaultTrafficAlerts*, establecida en false. Una vez activada la alerta, no vuelve a almacenar en déclencheur hasta el día siguiente (UTC).

```
kind: "CDN"
version: "1"
data:
  trafficFilters:
   defaultTrafficAlerts: false
```

## Registros de CDN {#cdn-logs}

AEM as a Cloud Service proporciona acceso a los registros de CDN, que son útiles para casos de uso, incluida la optimización de la proporción de visitas de caché y la configuración de reglas de filtro de tráfico. Los registros de CDN aparecen en el cuadro diálogo de Cloud Manager **Descargar registros**, al seleccionar el servicio de creación o publicación.

Los registros de CDN se retrasan hasta cinco minutos.

La propiedad `rules` describe qué reglas de filtro de tráfico coinciden y tiene el siguiente patrón:

```
"rules": "match=<matching-customer-named-rules-that-are-matched>,waf=<matching-WAF-rules>,action=<action_type>"
```

Por ejemplo:

```
"rules": "match=Block-Traffic-under-private-folder,Enable-SQL-injection-everywhere,waf="SQLI,SANS",action=block"
```

Las reglas se comportan de la siguiente manera:

* El nombre de regla declarada por el cliente de cualquier regla coincidente se enumerará en el atributo `match`.
* El atributo `action` determina si las reglas bloquean, permiten o registran.
* Si el WAF tiene licencia y está habilitado, el atributo `waf` lista cualquier indicador WAF que se haya detectado (por ejemplo, SQLI). Este comportamiento es verdadero independientemente de si los indicadores de WAF estaban enumerados en alguna regla. Este registro es para proporcionar a insight posibles nuevas reglas que declarar.
* Si no coinciden las reglas declaradas por el cliente y no coinciden las reglas waf, la propiedad `rules` se deja en blanco.

Como se ha indicado anteriormente, las coincidencias de reglas WAF solo aparecen en los registros CDN para errores y aprobaciones de CDN, no en los aciertos.

En el ejemplo siguiente se muestra un `cdn.yaml` de ejemplo y dos entradas de registro de CDN:


```
kind: "CDN"
version: "1"
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

## Herramientas de panel {#dashboard-tooling}

Adobe proporciona un mecanismo para descargar las herramientas del panel de control en el equipo para introducir registros de CDN descargados mediante Cloud Manager. Para analizar el tráfico y determinar las reglas de filtro de tráfico adecuadas que se deben declarar, incluidas las reglas de WAF, utilice esta herramienta.

Las herramientas del panel de control se pueden clonar directamente desde el repositorio de GitHub [AEMCS-CDN-Log-Analysis-ELK-Tool](https://github.com/adobe/AEMCS-CDN-Log-Analysis-Tooling).

Hay disponible [un tutorial](#tutorial) con instrucciones concretas sobre cómo utilizar las herramientas del panel de control.

## Reglas de inicio recomendadas {#recommended-starter-rules}

Adobe recomienda empezar con las reglas de filtro de tráfico que se indican a continuación y perfeccionarlas con el tiempo. Las *reglas estándar* están disponibles con una licencia de Sites o Forms, mientras que las *reglas de WAF* requieren una licencia de seguridad extendida (anteriormente denominada Protección WAF-DDoS) o de seguridad extendida para atención médica (anteriormente denominada Seguridad mejorada).

### Reglas estándar recomendadas {#recommended-nonwaf-starter-rules}

Comience con estas reglas:

1. límite de velocidad (modo de registro):
   * registrar cuándo el tráfico de una IP determinada supera un límite de velocidad. Cambie al modo de bloqueo después de validar que no se reciben alertas; si se recibieron alertas, indica que el valor límite era demasiado bajo.
2. países específicos (modo de bloqueo):
   * bloquear el tráfico procedente de determinados países (modificar los códigos de país en función de los requisitos de la empresa)

```
kind: "CDN"
version: "1"
data:
  trafficFilters:
    rules:
    #  Block client for 5m when it exceeds an average of 100 req/sec to origin on a time window of 10sec
    - name: limit-origin-requests-client-ip
      when:
        reqProperty: tier
        equals: 'publish'
      rateLimit:
        limit: 100
        window: 10
        count: fetches
        penalty: 300
        groupBy:
          - reqProperty: clientIp
      action: log
    #  Block client for 5m when it exceeds an average of 500 req/sec on a time window of 10sec
    - name: limit-requests-client-ip
      when:
        reqProperty: tier
        equals: 'publish'
      rateLimit:
        limit: 500
        window: 10
        count: all
        penalty: 300
        groupBy:
          - reqProperty: clientIp
      action: log
      alert: true
    # Block requests coming from OFAC countries
    - name: ofac-countries
      when:
        allOf:
          - { reqProperty: tier, in: ["author", "publish"] }
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

### Reglas de inicio recomendadas {#recommended-waf-starter-rules}

Añada las siguientes reglas a la configuración existente:

1. Indicador ATTACK-FROM-BAD-IP (modo de bloqueo):
   * Bloquear inmediatamente el tráfico que coincida con patrones sospechosos (incluidos varios de los que aparecen en la [lista de indicadores WAF](#waf-flags-list)) y que se origine a partir de direcciones IP que se sabe que son malintencionadas.
   * El indicador ATTACK-FROM-BAD-IP cumple ambas condiciones (coincidencia de patrones e IP maliciosa conocida), minimizando el riesgo de falsos positivos. Por lo tanto, puede aplicar esta regla en modo de bloqueo de forma segura e inmediata.
2. Indicador ATTACK (modo de registro):
   * Registrar inicialmente (en lugar de bloquear) el tráfico que coincida con patrones sospechosos, pero que no se origina a partir de direcciones IP malintencionadas conocidas. Este método prudente de registrar en lugar de bloquear ayuda a evitar el bloqueo involuntario del tráfico legítimo (falsos positivos).
   * Para comprobar que las solicitudes legítimas no se marcan incorrectamente, analice los registros de CDN después de implementar esta regla. Una vez que esté seguro de que ningún tráfico legítimo se verá afectado, cambie al modo de bloqueo.

>[!NOTE]
>
> La experiencia indica que los falsos positivos asociados con el indicador ATTACK son raros. Por lo tanto, una estrategia práctica es bloquear todo el tráfico sospechoso inmediatamente y utilizar el análisis de registro de CDN para identificar e introducir reglas de permiso para el tráfico legítimo. Cada organización evalúa su propia tolerancia al riesgo, sopesando los beneficios de una mayor protección contra el riesgo de bloquear inadvertidamente solicitudes legítimas.

```
    # blocks likely attack traffic, which also comes from suspected IPs
    - name: attacks-from-bad-ips-globally
      when:
        reqProperty: tier
        in: ["author", "publish"]
      action:
        type: block
        wafFlags:
          - ATTACK-FROM-BAD-IP
    # log likely attack traffic, and later switch to block mode if false positives aren't observed
    - name: attacks-from-any-ips-globally
      when:
        reqProperty: tier
        in: ["author", "publish"]
      action:
        type: log
        wafFlags:
          - ATTACK
```

### Reglas WAF recomendadas heredadas {#previous-waf-starter-rules}

Antes de julio de 2025, Adobe recomendaba las reglas WAF enumeradas a continuación, que siguen siendo válidas y efectivas para defenderse del tráfico malicioso. Consulte el tutorial para ver algunas consideraciones sobre la migración a las nuevas reglas recomendadas.

+++ Amplíe para ver las reglas WAF recomendadas heredadas.

```
    # Enable recommended WAF protections (only works if WAF is licensed enabled for your environment)
    - name: block-waf-flags-globally
      when:
        reqProperty: tier
        in: ["author", "publish"]
      action:
        type: log
        wafFlags:
          - TRAVERSAL
          - CMDEXE-NO-BIN
          - XSS
          - LOG4J-JNDI
          - BACKDOOR
          - USERAGENT
          - SQLI
          - SANS
          - TORNODE
          - NOUA
          - SCANNER
          - PRIVATEFILE
          - NULLBYTE
```

+++

## Tutorial {#tutorial}

Para obtener conocimientos prácticos y experiencia sobre las reglas de filtros de tráfico, incluidas las reglas de WAF, siga [una serie de tutoriales](https://experienceleague.adobe.com/es/docs/experience-manager-learn/cloud-service/security/traffic-filter-and-waf-rules/overview).

Los tutoriales incluyen:

* Información general sobre las reglas de filtro de tráfico estándar y de WAF.
* Para bloquear ataques, incluidas las denegaciones de servicio (DoS), configure las reglas de filtro de tráfico estándar y de WAF recomendadas.
* Implementación de reglas mediante la canalización de configuración de Cloud Manager.
* Prueba de reglas con herramientas para simular el tráfico malintencionado.
* Análisis de los resultados mediante la herramienta de análisis de registro.
* Prácticas recomendadas.
