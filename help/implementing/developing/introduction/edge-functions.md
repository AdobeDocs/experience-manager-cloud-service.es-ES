---
title: Funciones de Edge de AEM
description: Obtenga información sobre cómo ejecutar JavaScript en la capa de CDN con las funciones de Edge de AEM para habilitar la personalización, la seguridad y las experiencias dinámicas cerca del usuario final.
feature: Developing, Edge Delivery Services
role: Developer
exl-id: 9cebe65c-6aea-4096-9c58-f88295a80639
source-git-commit: ea43e2f4c7e52f98e8458e86bb48f124191dc03c
workflow-type: tm+mt
source-wordcount: '1261'
ht-degree: 3%

---

# Funciones de Edge de AEM {#aem-edge-functions}

>[!IMPORTANT]
>
>Funciones de AEM Edge es una característica **beta**. Las funciones y la documentación pueden cambiar sin previo aviso. Para unirse al programa de acceso anticipado y proporcionar comentarios, envíe un correo electrónico a [aemcs-edgecompute-feedback@adobe.com](mailto:aemcs-edgecompute-feedback@adobe.com).

AEM Edge Functions le permite ejecutar JavaScript en la capa de CDN, lo que acerca el procesamiento de datos al usuario final. Esto reduce la latencia y permite experiencias dinámicas y adaptables sin necesidad de realizar un viaje de ida y vuelta al origen.

Los casos de uso comunes incluyen los siguientes:

- Personalización del contenido en función de información como la geolocalización, el tipo de dispositivo o los atributos del usuario
- Actuación como middleware entre la CDN y su origen
- Volver a dar formato o agregar respuestas desde API de terceros antes de que lleguen al explorador
- Composición y servicio de HTML procesados por el servidor en el perímetro mediante contenido vinculado de varios backends

Las funciones de AEM Edge son compatibles con Edge Delivery Services y con la pila Java de AEM Cloud Service.

## Principales ventajas {#key-benefits}

| Ventaja | Descripción |
|---|---|
| **Rendimiento** | TTFB rápido a través de SSR perimetral que devuelve HTML completamente procesado. Llamadas de API de baja latencia a través de recuperaciones paralelas y saltos de red optimizados. |
| **SEO / GEO** | Server HTML se indexa al rastrear por primera vez. El contenido completamente procesado está listo para los rastreadores de IA. |
| **Seguridad** | Mantenga las credenciales de la API del lado del servidor ocultas de la JavaScript del cliente. Autenticar con un proveedor de identidad y restringir el acceso al contenido. |
| **Personalización** | Personalice el contenido antes de que la página se cargue en función de las señales geográficas y de dispositivo. Ejecute búsquedas de audiencia en el perímetro de para la entrega segmentada. |

## Requisitos previos {#prerequisites}

- Un entorno de AEM as a Cloud Service
- El perfil de producto del administrador de AEM en la instancia de autor de su entorno de Cloud Service, **o** la función de administrador de implementación de Cloud Manager en los sitios de Admin Console para Edge Delivery Services
- [Node.js y npm](https://nodejs.org/)

## Configuración {#setup}

### Instalación de la CLI de Adobe {#install-adobe-cli}

Instale la CLI de Adobe Developer (`aio`):

```bash
npm install -g @adobe/aio-cli
```

Instale el complemento Funciones de AEM Edge:

```bash
aio plugins install @adobe/aio-cli-plugin-aem-edge-functions
```

Autentique y configure el complemento para su entorno:

```bash
aio login
aio aem edge-functions setup
```

El comando setup le solicita que inicie sesión y, a continuación, seleccione el entorno de AEM en el que desea utilizar las funciones de Edge de AEM.

### Clonar la plantilla {#boilerplate}

Copie [aem-edge-functions-boilerplate](https://github.com/adobe/aem-edge-functions-boilerplate) en su propio repositorio y luego instale las dependencias:

```bash
npm install
```

## Creación de la primera función {#create-your-function}

Los servicios de funciones de AEM Edge se declaran en un archivo de configuración de YAML y se implementan a través de la canalización de configuración de Cloud Manager.

### &#x200B;1. Configurar una canalización de configuración {#configuration-pipeline}

Antes de crear una función perimetral, asegúrese de que exista una canalización de configuración para su entorno en Cloud Manager. Si no, [cree primero una canalización de configuración](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md).

>[!NOTE]
>
>Si está usando un entorno de desarrollo rápido (RDE), puede implementar la configuración directamente con `aio aem rde:install -t env-config ./config` en lugar de pasar por una canalización de configuración.

### &#x200B;2. Declarar los servicios de función de Edge {#declare-services}

Cree un archivo con el nombre `edgeFunctions.yaml` en el directorio de configuración:

```yaml
kind: "EdgeFunctions"
version: "1"
data:
  services:
    - name: first-function
    - name: second-function
    # Uncomment to enable secrets
    # secrets:
    #   - key: API_TOKEN
    #     value: ${{ API_TOKEN_SECRET }}
```

La configuración admite hasta tres servicios. Las claves de nivel superior son:

| Clave | Descripción |
|---|---|
| `services` | Lista de servicios de funciones perimetrales, cada uno identificado por un `name`. |
| `configs` | Pares de clave/valor expuestos a todos los servicios de funciones Edge como variables de entorno. |
| `secrets` | Pares de clave/valor que hacen referencia a secretos de Cloud Manager, expuestos a todos los servicios de funciones Edge. |

### &#x200B;3. Agregar reglas de selector de origen de CDN {#cdn-routing}

Las funciones de Edge se invocan enrutando el tráfico de CDN a ellas a través de reglas de selector de origen. Agregue lo siguiente al archivo de configuración `cdn.yaml` (o cree uno si no existe):

```yaml
kind: 'CDN'
version: '1'
data:
  originSelectors:
    rules:
      - name: route-to-first-function
        when: { reqProperty: path, equals: "/weather" }
        action:
          type: selectAemOrigin
          originName: edgefunction-first-function
      - name: route-to-second-function
        when: { reqProperty: path, equals: "/hello-world" }
        action:
          type: selectAemOrigin
          originName: edgefunction-second-function
```

Las reglas del selector de origen permiten dirigir el tráfico a las funciones perimetrales en función de cualquier condición disponible en el motor de reglas de CDN, como una ruta específica, un dominio o un encabezado de solicitud. Consulte [Selectores de origen](/help/implementing/dispatcher/cdn-configuring-traffic.md#origin-selectors) para obtener la sintaxis completa de la regla.

### &#x200B;4. Implementar la configuración {#deploy-configuration}

Confirme tanto `edgeFunctions.yaml` como `cdn.yaml` a su repositorio Git de Cloud Manager y almacene en déclencheur la canalización de configuración. Una vez que la canalización se complete correctamente, los puntos finales de la función Edge estarán disponibles en:

- `publish-pXXXXX-eYYYYY.adobeaemcloud.com/weather`
- `publish-pXXXXX-eYYYYY.adobeaemcloud.com/hello-world`

donde `pXXXXX-eYYYYY` son las coordenadas de entorno. Si se configura un dominio personalizado, también se puede acceder a las funciones en esas rutas de dominio (por ejemplo, `example.com/weather`).

## Generar e implementar el código de función de AEM Edge {#build-deploy}

### Generar {#build}

Empaquete el código de función perimetral para la implementación:

```bash
aio aem edge-functions build
```

### Implementación {#deploy}

Implemente el paquete creado en un servicio de función perimetral con nombre. El argumento `function-name` debe coincidir con el valor `name` de `edgeFunctions.yaml`:

```bash
aio aem edge-functions deploy <function-name>
```

## Desarrollo local {#local-development}

### Ejecutar localmente {#local-run}

Iniciar un servidor de desarrollo local en `http://127.0.0.1:7676`:

```bash
aio aem edge-functions serve
```

Consulte esta [Documentación de cómputo de JavaScript](https://www.fastly.com/documentation/guides/compute/javascript/) para obtener detalles sobre lo que admite el tiempo de ejecución local.

### Prueba {#test}

Ejecute el grupo de pruebas con [Mocha](https://mochajs.org/):

```bash
npm run test
```

### Depuración remota {#remote-debugging}

La CDN administrada por Adobe no expone un depurador remoto, pero sí un flujo de registro. Siga los registros de una función implementada para recibir la salida `console.log` directamente en el terminal:

```bash
aio aem edge-functions tail-logs <function-name>
```

## Almacenamiento en caché y depuración de caché {#caching}

Las funciones de Edge pueden reducir significativamente la carga de origen y mejorar los tiempos de respuesta al almacenar en caché los datos en el perímetro de. Sin embargo, el almacenamiento en caché requiere un diseño intencional, especialmente en las funciones de Edge en las que hay **dos capas de caché independientes** implicadas:

```
Browser → AEM CDN (CDN Cache) → AEM Edge Functions (Fetch Cache) → Backend (AEM, APIs, etc.)
```

Antes de configurar el almacenamiento en caché, considere cómo se comporta su contenido:

- **El contenido verdaderamente único por solicitud** (tokens de sesión, precios en tiempo real para un usuario específico) debe evitar el almacenamiento en caché para evitar ofrecer resultados incorrectos.
- La personalización basada en **cohorte** (contenido personalizado por región, tipo de dispositivo o segmento de audiencia) puede almacenarse en caché con TTL más cortos o encabezados `Vary`, ya que muchos usuarios comparten la misma variante.
- **El contenido estable y compartido** (catálogos de productos, páginas de CMS, respuestas de API que cambian según una programación conocida) se beneficia de un almacenamiento en caché agresivo con invalidación explícita mediante claves sustitutas.
- **Cometer un error en cualquier dirección tiene consecuencias.** El almacenamiento en caché excesivo causa errores de contenido antiguos difíciles de diagnosticar en dos capas de caché. El almacenamiento en caché insuficiente anula el propósito de rendimiento y descarga de origen de utilizar las funciones de Edge.

Dado que la CDN y la caché de recuperación interna de la función Edge funcionan de forma independiente, un cambio en los datos subyacentes requiere la invalidación deliberada de **ambas** capas. Comprender esta arquitectura es esencial para una administración fiable de la caché.

Para obtener instrucciones técnicas detalladas sobre la configuración del comportamiento del almacenamiento en caché, el control de la duración de la caché, el uso de claves de sustitución y la depuración del contenido almacenado en caché, consulte [Almacenamiento en caché en las funciones de Edge de AEM](/help/implementing/developing/introduction/edge-functions-caching.md).

## Limitaciones {#limitations}

Cada invocación de función de Edge se ejecuta dentro de una zona protegida con límites de recursos impuestos por la plataforma de cálculo subyacente.

### Máximo de llamadas de recuperación salientes por invocación {#max-fetch-calls}

Las funciones de AEM Edge aplican un límite estricto de **32 solicitudes back-end por ejecución** (es decir, por cada solicitud entrante gestionada por su función). Una vez alcanzado este límite, cualquier llamada adicional de `fetch()` genera el siguiente error:

```
Requested backend named '…' does not exist
```

Cuando vea este error y la configuración de origen sea correcta, la causa más probable es que se haya agotado la cuota de solicitudes back-end por invocación. Consulte [Límites de recursos de Fastly Compute](https://docs.fastly.com/products/compute-resource-limits#default-limits) para obtener la lista completa de límites de plataforma.

## Referencia de configuración {#configuration-reference}

### Orígenes {#origins}

De forma predeterminada, las funciones de Edge pueden recuperarse de cualquier origen. Para restringir una función a un conjunto definido de orígenes, declárelos en `origins` en `edgeFunctions.yaml`:

```yaml
origins:
  - name: my-origin-name
    domain: example.com
```

Haga referencia al origen con nombre en el código de función mediante la opción de captura `backend`:

```js
const request = new Request("https://example.com/test");
const response = await fetch(request, { backend: "my-origin-name" });
```

### Configuración de servicio {#service-configuration}

Exponga las variables de entorno a sus funciones usando la clave `configs` en `edgeFunctions.yaml`. Los valores se almacenan en un almacén de configuración denominado `config_default`:

```yaml
configs:
  - key: LOG_LEVEL
    value: DEBUG
```

Lea los valores de configuración en el código de función:

```js
import { ConfigStore } from "fastly:config-store";

const config = new ConfigStore('config_default');
const logLevel = config.get('LOG_LEVEL') || 'info';
```

>[!NOTE]
>
>- El nombre del almacén de configuración siempre es `config_default`.
>- Los nombres de clave distinguen entre mayúsculas y minúsculas.
>- El almacén de configuración se comparte en todos los servicios de funciones Edge en el mismo entorno.

### Secretos de servicio {#service-secrets}

Se hace referencia a los secretos, no se almacenan, en `edgeFunctions.yaml`. El campo `value` debe señalar a un secreto de Cloud Manager mediante la sintaxis `${{SECRET_REFERENCE}}`. Defina primero el secreto subyacente en Cloud Manager; consulte [Variables secretas de Cloud Manager](/help/implementing/cloud-manager/environment-variables.md).

```yaml
secrets:
  - key: API_TOKEN
    value: ${{ API_TOKEN_SECRET }}
```

Recupere secretos en su código de función utilizando el asistente `SecretStoreManager` de la plantilla:

```js
import { SecretStoreManager } from "./lib/config";

const apiToken = await SecretStoreManager.getSecret('API_TOKEN');
```

>[!NOTE]
>
>- El almacén secreto siempre se denomina `secret_default`.
>- Los nombres de clave distinguen entre mayúsculas y minúsculas.
>- Los secretos son inmutables una vez creados.
>- El almacén secreto se comparte en todos los servicios de funciones perimetrales del mismo entorno.

### Registro {#logging}

Las funciones de AEM Edge se integran con la función [Reenvío de registros de AEM](/help/implementing/developing/introduction/log-forwarding.md). Crear un archivo de `logForwarding.yaml` junto con su `edgeFunctions.yaml`:

```yaml
kind: "LogForwarding"
version: "1"
metadata:
  envTypes: ["rde", "dev", "stage", "prod"]
data:
  splunk:
    default:
      enabled: true
      host: "splunk-host.example.com"
      token: "${{SPLUNK_TOKEN}}"
      index: "AEMaaCS"
```

Utilice el registrador en el código de función para escribir entradas de registro estructuradas:

```js
import { Logger } from "fastly:logger";

const logger = new Logger("customerSplunk");
logger.log(JSON.stringify({
  method: event.request.method,
  url: event.request.url
}));
```

>[!NOTE]
>
>Los registros de CDN, que incluyen entradas de registro de funciones de AEM Edge, se pueden descargar desde Cloud Manager para entornos de pila Java, pero no para sitios de Edge Delivery Services.
>
