---
title: Configuración del tráfico en la CDN
description: Obtenga información sobre cómo configurar el tráfico de CDN declarando reglas y filtros en un archivo de configuración e implementándolos en CDN mediante una canalización de configuración de Cloud Manager.
feature: Dispatcher
exl-id: e0b3dc34-170a-47ec-8607-d3b351a8658e
role: Admin
source-git-commit: cb1581e96f1cfeadf6ee37cae4738d9d51177504
workflow-type: tm+mt
source-wordcount: '1377'
ht-degree: 1%

---


# Configuración del tráfico en la CDN {#cdn-configuring-cloud}

AEM as a Cloud Service ofrece una colección de características configurables en el nivel [CDN](/help/implementing/dispatcher/cdn.md#aem-managed-cdn) administrado por Adobe que modifican la naturaleza de las solicitudes entrantes o de las respuestas salientes. Se pueden declarar las siguientes reglas, descritas en detalle en esta página, para lograr el siguiente comportamiento:

* [Transformaciones de solicitudes](#request-transformations): modifique aspectos de las solicitudes entrantes, incluidos los encabezados, las rutas y los parámetros.
* [Transformaciones de respuesta](#response-transformations): modifique los encabezados que están en camino de regreso al cliente (por ejemplo, un explorador web).
* [Redirecciones del lado del cliente](#client-side-redirectors): déclencheur una redirección del explorador.
* [Selectores de origen](#origin-selectors): proxy a un backend de origen diferente.

También se pueden configurar en la CDN las reglas de filtro de tráfico (incluida WAF), que controlan qué tráfico permite o rechaza la CDN. Esta característica ya se ha lanzado y puede obtener más información al respecto en la página [Reglas de filtro de tráfico](/help/security/traffic-filter-rules-including-waf.md), que incluye las reglas de WAF.

Además, si la CDN no puede ponerse en contacto con su origen, puede escribir una regla que haga referencia a una página de error personalizada autoalojada (que luego se procesará). Obtenga más información al leer el artículo [Configuración de páginas de error de CDN](/help/implementing/dispatcher/cdn-error-pages.md).

Todas estas reglas, declaradas en un archivo de configuración en el control de código fuente, se implementan mediante la canalización [config de Cloud Manager.](/help/operations/config-pipeline.md) Tenga en cuenta que el tamaño acumulado del archivo de configuración, incluidas las reglas de filtro de tráfico, no puede exceder los 100 KB.

## Orden de evaluación {#order-of-evaluation}

Desde el punto de vista funcional, las distintas funciones mencionadas anteriormente se evalúan en la siguiente secuencia:

![Orden de evaluación](/help/implementing/dispatcher/assets/order.png)

## Configuración {#initial-setup}

Para poder configurar el tráfico en la CDN, debe hacer lo siguiente:

1. Cree un archivo con el nombre `cdn.yaml` o similar, haciendo referencia a los distintos fragmentos de configuración en las secciones siguientes.

   Todos los fragmentos de código tienen estas propiedades comunes, que se describen en [Configurar canalización](/help/operations/config-pipeline.md#common-syntax). El valor de la propiedad `kind` debe ser *CDN* y la propiedad `version` debe establecerse en *1*.

   ```
   kind: "CDN"
   version: "1"
   metadata:
     envTypes: ["dev"]
   ```

1. Coloque el archivo en algún lugar bajo una carpeta de nivel superior llamada *config* o similar, como se describe en [Canalización de configuración](/help/operations/config-pipeline.md#folder-structure).

1. Cree una canalización de configuración en Cloud Manager, como se describe en [Canalización de configuración](/help/operations/config-pipeline.md#managing-in-cloud-manager).

1. Implemente la configuración de.

## Sintaxis de reglas {#configuration-syntax}

Los tipos de reglas de las secciones siguientes comparten una sintaxis común.

Se hace referencia a una regla mediante un nombre, una cláusula when condicional y acciones.

La cláusula when determina si se evaluará una regla en función de propiedades como dominio, ruta, cadenas de consulta, encabezados y cookies. La sintaxis es la misma en todos los tipos de reglas; para obtener más información, consulte la [sección Estructura de condiciones](/help/security/traffic-filter-rules-including-waf.md#condition-structure) en el artículo Reglas de filtro de tráfico.

Los detalles del nodo de acciones difieren según el tipo de regla y se describen en las secciones individuales siguientes.

## Solicitar transformaciones {#request-transformations}

Las reglas de transformación de solicitudes permiten modificar las solicitudes entrantes. Las reglas admiten la configuración, desconfiguración y modificación de rutas, parámetros de consulta y encabezados (incluidas las cookies) en función de diversas condiciones de coincidencia, incluidas las expresiones regulares. También puede establecer variables, a las que se puede hacer referencia más adelante en la secuencia de evaluación.

Los casos de uso son variados e incluyen reescrituras de URL para la simplificación de la aplicación o la asignación de URL heredadas.

Como se mencionó anteriormente, hay un límite de tamaño para el archivo de configuración, por lo que las organizaciones con requisitos más grandes deben definir reglas en la capa `apache/dispatcher`.

Ejemplo de configuración:

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev", "stage", "prod"]
data:
  requestTransformations:
    removeMarketingParams: true
    rules:
      - name: set-header-rule
        when:
          reqProperty: path
          like: /set-header
        actions:
          - type: set
            reqHeader: x-some-header
            value: some value
      - name: set-header-with-reqproperty-rule
        when:
          reqProperty: path
          like: /set-header
        actions:
          - type: set
            reqHeader: x-some-header
            value: {reqProperty: path}
      - name: unset-header-rule
        when:
          reqProperty: path
          like: /unset-header
        actions:
          - type: unset
            reqHeader: x-some-header

      - name: unset-matching-query-params-rule
        when:
          reqProperty: path
          equals: /unset-matching-query-params
        actions:
          - type: unset
            queryParamMatch: ^removeMe_.*$

      - name: unset-all-query-params-except-exact-two-rule
        when:
          reqProperty: path
          equals: /unset-all-query-params-except-exact-two
        actions:
          - type: unset
            queryParamMatch: ^(?!leaveMe$|leaveMeToo$).*$

      - name: multi-action
        when:
          reqProperty: path
          like: /multi-action
        actions:
          - type: set
            reqHeader: x-header1
            value: body set by transformation rule
          - type: set
            reqHeader: x-header2
            value: '201'

      - name: replace-html
        when:
          reqProperty: path
          like: /mypath
        actions:
          - type: transform
            reqProperty: path
            op: replace
            match: \.html$
            replacement: ""
```

**Acciones**

En la tabla siguiente se explican las acciones disponibles.

| Nombre | Propiedades | Significado |
|-----------|--------------------------|-------------|
| **conjunto** | (reqProperty o reqHeader o queryParam o reqCookie), valor | Establece un parámetro de solicitud especificado (solo se admite la propiedad &quot;path&quot;), un encabezado de solicitud, un parámetro de consulta o una cookie, en un valor determinado, que puede ser un literal de cadena o un parámetro de solicitud. |
|     | var, valor | Establece una propiedad de solicitud especificada en un valor determinado. |
| **anular** | reqProperty | Quita un parámetro de solicitud especificado (solo se admite la propiedad &quot;path&quot;), un encabezado de solicitud, un parámetro de consulta o una cookie, de un valor determinado, que podría ser un literal de cadena o un parámetro de solicitud. |
|         | var | Quita una variable especificada. |
|         | queryParamMatch | Quita todos los parámetros de consulta que coinciden con una expresión regular especificada. |
| **transformar** | op:replace, (reqProperty o reqHeader o queryParam o reqCookie o var), match, replace | Reemplaza parte del parámetro de solicitud (solo se admite la propiedad &quot;path&quot;), el encabezado de solicitud, el parámetro de consulta, la cookie o la variable por un nuevo valor. |
|              | op:tolower, (reqProperty o reqHeader o queryParam o reqCookie o var) | Establece el parámetro de solicitud (solo se admite la propiedad &quot;path&quot;), el encabezado de solicitud, el parámetro de consulta, la cookie o la variable en minúsculas. |

Las acciones de reemplazo admiten grupos de captura, como se muestra a continuación:

```
      - name: extract-country-code-from-path
        when:
          reqProperty: path
          matches: ^/([a-zA-Z]{2})(/.*|$)
        actions:
          - type: set
            var: country-code
            value:
              reqProperty: path
          - type: transform
            var: country-code
            op: replace
            match: ^/([a-zA-Z]{2})(/.*|$)
            replacement: \1
      - name: replace-jpg-with-jpeg
        when:
          reqProperty: path
          like: /mypath
        actions:
          - type: transform
            reqProperty: path
            op: replace
            match: (.*)(\.jpg)$
            replacement: "\1\.jpeg"
```

Las acciones se pueden encadenar. Por ejemplo:

```
actions:
    - type: transform
      reqProperty: path
      op: replace
      match: \.html$
      replacement: ""
    - type: transform
      reqProperty: path
      op: tolower
```

### Variables {#variables}

Puede establecer variables durante la transformación de la solicitud y luego hacer referencia a ellas más adelante en la secuencia de evaluación. Consulte el diagrama [orden de evaluación](#order-of-evaluation) para obtener más información.

Ejemplo de configuración:

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["prod", "dev"]
data:
  requestTransformations:
    rules:
      - name: set-variable-rule
        when:
          reqProperty: path
          equals: /set-variable
        actions:
          - type: set
            var: some_var_name
            value: some_value

  responseTransformations:
    rules:
      - name: set-response-header-while-variable
        when:
          var: some_var_name
          equals: some_value
        actions:
          - type: set
            respHeader: x-some-header
            value: some header value
```

## Transformaciones de respuesta {#response-transformations}

Las reglas de transformación de respuestas permiten establecer y anular la configuración de encabezados de las respuestas salientes de CDN. Además, consulte el ejemplo anterior para hacer referencia a una variable configurada anteriormente en una regla de transformación de solicitud. También se puede establecer el código de estado de la respuesta.

Ejemplo de configuración:

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["prod", "dev"]
data:
  responseTransformations:
    rules:
      - name: set-response-header-rule
        when:
          reqProperty: path
          like: /set-response-header
        actions:
          - type: set
            value: value-set-by-resp-rule
            respHeader: x-resp-header

      - name: unset-response-header-rule
        when:
          reqProperty: path
          like: /unset-response-header
        actions:
          - type: unset
            respHeader: x-header1

      # Example: Multi-action on response header
      - name: multi-action-response-header-rule
        when:
          reqProperty: path
          like: /multi-action-response-header
        actions:
          - type: set
            respHeader: x-resp-header-1
            value: value-set-by-resp-rule-1
          - type: set
            respHeader: x-resp-header-2
            value: value-set-by-resp-rule-2
      # Example: setting status code
      - name: status-code-rule
        when:
          reqProperty: path
          like: status-code
        actions:
          - type: set
            respProperty: status
            value: '410'        
```

**Acciones**

En la tabla siguiente se explican las acciones disponibles.

| Nombre | Propiedades | Significado |
|-----------|--------------------------|-------------|
| **conjunto** | reqHeader, valor | Establece un encabezado especificado en un valor determinado de la respuesta. |
|          | respProperty, valor | Establece una propiedad response. Admite solo la propiedad &quot;status&quot; para establecer el código de estado. |
| **anular** | respHeader | Quita un encabezado especificado de la respuesta. |

## Selectores de origen {#origin-selectors}

AEM Puede aprovechar la CDN de la para enrutar el tráfico a diferentes backends, incluidas las aplicaciones que no sean de Adobe (tal vez por ruta o subdominio).

Ejemplo de configuración:

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  originSelectors:
    rules:
      - name: example-com
        when: { reqProperty: path, like: /proxy* }
        action:
          type: selectOrigin
          originName: example-com
          # skipCache: true
    origins:
      - name: example-com
        domain: www.example.com
        # ip: '1.1.1.1'
        # forwardHost: true
        # forwardCookie: true
        # forwardAuthorization: true
        # timeout: 20
```

**Acciones**

La acción disponible se explica en la tabla siguiente.

| Nombre | Propiedades | Significado |
|-----------|--------------------------|-------------|
| **selectOrigin** | originName | Nombre de uno de los orígenes definidos. |
|     | skipCache (opcional, el valor predeterminado es false) | Indicar si se debe utilizar el almacenamiento en caché para las solicitudes que coinciden con esta regla. De forma predeterminada, las respuestas se almacenan en caché según el encabezado de almacenamiento en caché de respuestas (por ejemplo, Cache-Control o Expires) |

**Orígenes**

Las conexiones a orígenes son solo SSL y utilizan el puerto 443.

| Propiedad | Significado |
|------------------|--------------------------------------|
| **nombre** | Nombre al que se puede hacer referencia mediante &quot;action.originName&quot;. |
| **dominio** | Nombre de dominio utilizado para conectarse al backend personalizado. También se utiliza para el SNI y la validación SSL. |
| **ip** (opcional, compatible con iv4 e ipv6) | Si se proporciona, se utiliza para conectarse al servidor en lugar de a &quot;dominio&quot;. Todavía se utiliza &quot;domain&quot; para el SNI y la validación SSL. |
| **forwardHost** (opcional, el valor predeterminado es falso) | Si se establece en true, el encabezado &quot;Host&quot; de la solicitud del cliente se pasará al backend; de lo contrario, el valor &quot;domain&quot; se pasará al encabezado &quot;Host&quot;. |
| **forwardCookie** (opcional, el valor predeterminado es falso) | Si se establece en true, el encabezado &quot;Cookie&quot; de la solicitud del cliente se pasará al servidor; de lo contrario, se eliminará el encabezado &quot;Cookie&quot;. |
| **forwardAuthorization** (opcional, el valor predeterminado es falso) | Si se establece en true, el encabezado &quot;Autorización&quot; de la solicitud del cliente se pasará al backend; de lo contrario, se eliminará el encabezado Autorización. |
| **tiempo de espera** (opcional; en segundos; el valor predeterminado es 60) | Número de segundos que la CDN debe esperar para que un servidor back-end envíe el primer byte de un cuerpo de respuesta HTTP. Este valor también se utiliza como tiempo de espera entre bytes para el servidor back-end. |

### Proxy a Edge Delivery Services {#proxying-to-edge-delivery}

AEM Hay escenarios en los que los selectores de origen deben utilizarse para enrutar el tráfico a través de Publish AEM a los Edge Delivery Services de la:

* AEM Parte del contenido lo entrega un dominio gestionado por Publish, mientras que parte del contenido del mismo dominio lo envían los Edge Delivery Services
* El contenido entregado por los Edge Delivery Services se beneficiaría de las reglas implementadas mediante la canalización de configuración, incluidas las reglas de filtro de tráfico o las transformaciones de solicitud/respuesta

Este es un ejemplo de regla de selector de origen que puede lograr esto:

```
kind: CDN
version: '1'
data:
  originSelectors:
    rules:
      - name: select-edge-delivery-services-origin
        when:
          allOf:
            - reqProperty: tier
              equals: publish
            - reqProperty: domain
              equals: <Production Host>
            - reqProperty: path
              matches: "^(/scripts/.*|/styles/.*|/fonts/.*|/blocks/.*|/icons/.*|.*/media_.*|/favicon.ico)"
        action:
          type: selectOrigin
          originName: aem-live
    origins:
      - name: aem-live
        domain: main--repo--owner.aem.live
```

>[!NOTE]
> Dado que se usa la CDN administrada de Adobe, asegúrese de configurar la invalidación push en el modo **administrado**, siguiendo la [documentación de invalidación push de configuración](https://www.aem.live/docs/byo-dns#setup-push-invalidation) de los Edge Delivery Services.


## Redirecciones del lado del cliente {#client-side-redirectors}

Puede utilizar reglas de redireccionamiento del lado del cliente para redirecciones del lado del cliente 301, 302 y similares. Si una regla coincide, la CDN responde con una línea de estado que incluye el código y el mensaje de estado (por ejemplo, HTTP/1.1 301 Movido permanentemente), así como el conjunto de encabezado de ubicación.

Se permiten ubicaciones absolutas y relativas con valores fijos.

Tenga en cuenta que el tamaño acumulado del archivo de configuración, incluidas las reglas de filtro de tráfico, no puede superar los 100 KB.

Ejemplo de configuración:

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  redirects:
    rules:
      - name: redirect-absolute
        when: { reqProperty: path, equals: "/page.html" }
        action:
          type: redirect
          status: 301
          location: https://example.com/page
      - name: redirect-relative
        when: { reqProperty: path, equals: "/anotherpage.html" }
        action:
          type: redirect
          location: /anotherpage
```

| Nombre | Propiedades | Significado |
|-----------|--------------------------|-------------|
| **redireccionamiento** | ubicación | Valor del encabezado &quot;Ubicación&quot;. |
|     | estado (opcional, el valor predeterminado es 301) | Estado HTTP que se utilizará en el mensaje de redirección, 301 de forma predeterminada, los valores permitidos son: 301, 302, 303, 307, 308. |

Las ubicaciones de una redirección pueden ser literales de cadena (por ejemplo, https://www.example.com/page) o el resultado de una propiedad (por ejemplo, ruta) que se transforme opcionalmente, con la siguiente sintaxis:

```
redirects:
  rules:
    - name: country-code-redirect
      when: { reqProperty: path, like: "/" }
      action:
        type: redirect
        location:
          reqProperty: clientCountry
          transform:
            - op: replace
              match: '^(.*)$'
              replacement: 'https://www.example.com/\1/home'
            - op: tolower
    - name: www-redirect
      when: { reqProperty: domain, equals: "example.com" }
      action:
        type: redirect
        location:
          reqProperty: path
          transform:
            - op: replace
              match: '^/(.*)$'
              replacement: 'https://www.example.com/\1'
```
