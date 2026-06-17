---
title: Funciones de Edge de AEM
description: Obtenga información sobre cómo ejecutar JavaScript en la capa de CDN con las funciones de Edge de AEM para habilitar la personalización, la seguridad y las experiencias dinámicas cerca del usuario final.
feature: Developing, Edge Delivery Services
role: Developer
exl-id: 9cebe65c-6aea-4096-9c58-f88295a80639
source-git-commit: db458670dfc8e216d9f7f54e6017e75439101645
workflow-type: tm+mt
source-wordcount: '1902'
ht-degree: 2%

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

AEM Edge Functions es compatible tanto con Edge Delivery Services como con la pila Java de AEM as a Cloud Service.

## Principales ventajas {#key-benefits}

| Ventaja | Descripción |
|---|---|
| **Rendimiento** | TTFB rápido a través de SSR perimetral que devuelve HTML completamente procesado. Llamadas de API de baja latencia a través de recuperaciones paralelas y saltos de red optimizados. |
| **SEO / GEO** | Los rastreadores de IA pueden indexar el contenido que se vincula entre sí en el lado del servidor. |
| **Seguridad** | Mantenga las credenciales de la API del lado del servidor ocultas de la JavaScript del cliente. Autenticar con un proveedor de identidad y restringir el acceso al contenido. |
| **Personalización** | Personalice el contenido antes de que la página se cargue en función de las señales geográficas y de dispositivo. Ejecute búsquedas de audiencia en el perímetro de para la entrega segmentada. |

## Requisitos previos {#prerequisites}

- Un programa de Cloud Manager que contiene entornos de pila Java de AEM o sitios de Edge Delivery Services. Aprenda a [incorporar sitios EDS a Cloud Manager](/help/implementing/cloud-manager/edge-delivery/introduction-to-edge-delivery-services.md).
- Una canalización de configuración de Cloud Manager (denominada canalización de Edge Delivery Services para sitios EDS).
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

## Registre su función de AEM Edge {#register-your-function}

Las funciones de AEM Edge se declaran en un archivo de configuración de YAML y se implementan a través de la canalización de configuración de Cloud Manager.

### &#x200B;1. Configurar una canalización de configuración {#configuration-pipeline}

Antes de crear una función perimetral, asegúrese de que en Cloud Manager exista una canalización de configuración para su entorno (si utiliza la pila Java de AEM) o una canalización de Edge Delivery Services si el proyecto se implementa con Edge Delivery Services. Consulte [Usar canalizaciones de configuración](/help/operations/config-pipeline.md) para obtener información sobre cómo configurar las canalizaciones.

>[!NOTE]
>
>Si está usando un entorno de desarrollo rápido (RDE), puede implementar la configuración directamente con `aio aem rde:install -t env-config ./config` en lugar de pasar por una canalización de configuración.

### &#x200B;2. Declarar la función de Edge {#declare-functions}

Cree un archivo con el nombre `edgeFunctions.yaml` en el directorio de configuración:

```yaml
kind: "EdgeFunctions"
version: "1"
data:
  functions:
    - name: my-edge-function
    # add advanced configuration under here
```

Los entornos de pila de Java tienen 1 función Edge y las implementaciones de Edge Delivery Services tienen 3 funciones Edge. Las claves de nivel superior opcionales son las siguientes:

| Clave | Descripción |
|---|---|
| `functions` | Lista de funciones de Edge, cada una identificada por un `name`. Para la compatibilidad con versiones anteriores, `services` también se acepta, pero `functions` es la clave preferida. No se permite el uso de ambos en el mismo archivo. |
| `configs` | Pares de clave/valor expuestos a las funciones perimetrales de un entorno como variables de entorno. |
| `secrets` | Pares de clave/valor que hacen referencia a los secretos de Cloud Manager en las funciones Edge de un entorno |
| `kvs` | Alternar booleano para aprovisionar un KVStore para los datos de valor clave de lectura y escritura en tiempo de ejecución compartidos entre todas las funciones Edge de un entorno. |

Vea configuraciones avanzadas como `configs`, `secrets` y `kvs` en la [sección de configuración avanzada](#advanced-function-configuration) a continuación.

### &#x200B;3. Implementación de la función Edge mediante Cloud Manager {#deploy-functions-via-cm}

Con Cloud Manager, implemente la canalización para que la función perimetral se registre en la CDN.

## Crear, generar e implementar código de función de AEM Edge {#build-deploy}

### Autor {#author}

Escriba su lógica empresarial de código de función perimetral, usando la `src` carpeta [&#128279;](https://github.com/adobe/aem-edge-functions-boilerplate/tree/main/src) de plantillas como punto de partida.

### Generar {#build}

Empaquete el código de función perimetral para la implementación:

```bash
aio aem edge-functions build
```

### Implementación {#deploy}

Implemente el código de función de Edge empaquetado en la función de Edge con nombre. El argumento `function-name` debe coincidir con el valor `name` de `edgeFunctions.yaml`:

```bash
aio aem edge-functions deploy <function-name>
```

### Prueba {#test}

Asegúrese de que la función Edge funciona según lo esperado. Puede probarlo en:

`edgefunction-pXXXXX-eYYYYY-<function name>.adobeaemcloud.com/<path>`

Por ejemplo, para la pila Java de AEM:<br/>
`edgefunction-pXXXXX-eYYYYY-my-edge-function.adobeaemcloud.com/weather`

o para Edge Delivery Services:<br/>
`edgefunction-pXXXXX-dYYYYY-my-edge-function.adobeaemcloud.com/weather`

Este dominio con el prefijo *edgefunction* solo se usa para la depuración, pero no se debe hacer referencia a *para el tráfico en directo* porque no se garantiza que sea un nombre estable. Para determinar el valor de dAAAA, consulte el resultado del comando deploy.


## Alambre en el flujo de entrega de contenido {#wiring}

El tráfico de funciones de Edge debe enviarse al dominio del sitio web, que suele ser un dominio personalizado para AEM Java-stack, y *debe* ser un dominio personalizado para Edge Delivery Services Sites.

### &#x200B;1. Definir selectores de origen {#origin-selectors}

Las funciones de Edge se invocan enrutando el tráfico de CDN a ellas a través de reglas de selector de origen. Agregue lo siguiente al archivo de configuración `cdn.yaml` (o cree uno si no existe):

```yaml
kind: 'CDN'
version: '1'
data:
  originSelectors:
    rules:
      - name: route-weather-to-edge-function
        when: { reqProperty: path, equals: "/weather" }
        action:
          type: selectAemOrigin
          originName: edgefunction-my-edge-function
      - name: route-hello-world-to-edge-function
        when: { reqProperty: path, equals: "/hello-world" }
        action:
          type: selectAemOrigin
          originName: edgefunction-my-edge-function
```

Las reglas del selector de origen permiten dirigir el tráfico a las funciones perimetrales en función de cualquier condición disponible en el motor de reglas de CDN, como una ruta específica, un dominio o un encabezado de solicitud. Varias reglas pueden enrutar diferentes rutas a la misma función de Edge. Consulte [Selectores de origen](/help/implementing/dispatcher/cdn-configuring-traffic.md#origin-selectors) para obtener la sintaxis completa de la regla.

### &#x200B;2. Implementar la configuración {#deploy-to-cdn}

Confirme `cdn.yaml` a su repositorio Git de Cloud Manager y almacene en déclencheur la canalización de configuración. Una vez que la canalización se complete correctamente, los puntos finales de la función Edge estarán disponibles en:

- `example.com/weather`
- `example.com/hello-world`

Para la depuración, puede hacer referencia a la función perimetral en el dominio `publish-pXXXXX-eYYYYY.adobeaemcloud.com` (para la pila Java de AEM) o `publish-pXXXXX-dYYYYY.adobeaemcloud.com` (para los sitios Edge Delivery Services). No utilice este dominio para el uso en producción, ya que no se garantiza que sea un nombre estable. Para determinar el valor de dAAAA, consulte el resultado del comando deploy.

## Desarrollo local {#local-development}

### Ejecutar localmente {#local-run}

Iniciar un servidor de desarrollo local en `http://127.0.0.1:7676`:

```bash
aio aem edge-functions serve
```

Consulte esta [Documentación de cómputo de JavaScript](https://www.fastly.com/documentation/guides/compute/javascript/) para obtener detalles sobre lo que admite el tiempo de ejecución local.

### Prueba {#test-localdev}

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

- Cada invocación de función de Edge se ejecuta dentro de una zona protegida con límites de recursos impuestos por la plataforma de cálculo subyacente.

- El tamaño máximo del artefacto de ensamblado web (wasm) creado es de 100 MB

- El consumo máximo de memoria es de 1 MB de pila, 128 MB de pila

- Información importante sobre la ejecución de funciones de Edge:
   - Una ejecución termina después de 120 segundos de tiempo de pared
   - Las ejecuciones finalizarán a los 1 s de cálculo (no en tiempo de pared)
   - El tiempo medio de ejecución de la función Edge debe ser inferior a 100 ms.

- Vea las limitaciones relacionadas con [Variables de configuración de funciones de Edge](#function-configuration), [Variables de secreto de funciones de Edge](#function-secrets) y [KVStore de funciones de Edge](#function-kv-store).

### Máximo de llamadas de recuperación salientes por invocación {#max-fetch-calls}

Las funciones de AEM Edge aplican un límite estricto de **32 solicitudes back-end por ejecución** (es decir, por cada solicitud entrante gestionada por su función). Una vez alcanzado este límite, cualquier llamada adicional de `fetch()` genera el siguiente error:

```
Requested backend named '…' does not exist
```

Cuando vea este error y la configuración de origen sea correcta, la causa más probable es que se haya agotado la cuota de solicitudes back-end por invocación. Consulte [Límites de recursos de Fastly Compute](https://docs.fastly.com/products/compute-resource-limits#default-limits) para obtener la lista completa de límites de plataforma.

## Configuración avanzada de funciones de Edge {#advanced-function-configuration}

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

>[!NOTE]
>
>Las configuraciones, los secretos y los kvs no están disponibles en [programas de zonas protegidas](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/introduction-sandbox-programs.md). Las funciones de Edge se ejecutan normalmente en entornos de espacio aislado; solo que estas entidades no están aprovisionadas.

### Variables de configuración de función Edge {#function-configuration}

Exponga las variables de entorno a sus funciones usando la clave `configs` en `edgeFunctions.yaml`. Los valores se almacenan en un almacén de configuración denominado `config_default`:

```yaml
kind: "EdgeFunctions"
version: "1"
data:
  functions:
    - name: my-edge-function
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
>- El almacén de configuración se comparte entre todas las funciones de Edge en el mismo entorno.
>- El almacén de configuración se replica en la red global de CDN administrada por Adobe
>- máximo de 500 entradas
>- tamaños máximos de nombre/valor: 255 y 8000 caracteres


### Variables secretas de funciones Edge {#function-secrets}

Se hace referencia a los secretos, no se almacenan, en `edgeFunctions.yaml`. El campo `value` debe señalar a un secreto de Cloud Manager mediante la sintaxis `${{SECRET_REFERENCE}}`. Defina primero el secreto subyacente en Cloud Manager; consulte [Variables secretas de Cloud Manager](/help/implementing/cloud-manager/environment-variables.md).


```yaml
kind: "EdgeFunctions"
version: "1"
data:
  functions:
    - name: my-edge-function
  secrets:
    - key: API_TOKEN
      value: ${{API_TOKEN_SECRET}}
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
>- El almacén secreto se comparte en todas las funciones Edge del mismo entorno.
>- El almacén secreto se replica en la red global de CDN administrada por Adobe
>- El tamaño máximo de todos los secretos es de 64 kb

### KVStore de funciones Edge {#function-kv-store}

Las funciones de Edge pueden leer y escribir datos de valor clave arbitrarios en tiempo de ejecución a través de un KVStore. Para habilitarlo, establezca `kvs: true` en `edgeFunctions.yaml`:


```yaml
kind: "EdgeFunctions"
version: "1"
data:
  functions:
    - name: my-edge-function
  kvs: true
```

Esto aprovisiona un KVStore vacío denominado `kv_default`. Rellénelo en tiempo de ejecución desde el código de función perimetral mediante la [API de KVStastly](https://js-compute-reference-docs.edgecompute.app/docs/fastly:kv-store/KVStore):

```js
import { KVStore } from "fastly:kv-store";

const kv = new KVStore('kv_default');

// Read a value
const entry = await kv.get('visit-count');
const count = entry ? Number(await entry.text()) : 0;

// Write a value
await kv.put('visit-count', String(count + 1));
```

>[!NOTE]
>
>- El nombre del KVStore siempre es `kv_default`.
>- El KVStore está vacío en el momento del aprovisionamiento; rellénelo durante la ejecución mediante la [API de KVStore](https://js-compute-reference-docs.edgecompute.app/docs/fastly:kv-store/KVStore) de Fastly. No se admiten las entradas de clave/valor declarativo en `edgeFunctions.yaml`.
>- El KVStore se comparte en todas las funciones de Edge en el mismo entorno.
>- El KVStore se replica en toda la red global de CDN administrada por Adobe
>- Las KVStore proporcionan una posible coherencia, lo que significa que leer una clave inmediatamente después de escribirla puede no devolver el valor actualizado.
>- Los nombres de clave KV son archivos UTF-8 máximos de 1024 bytes
>- El tamaño de la entrada de KV es máximo 25M
>- Los artículos de KVStore tienen un límite de tarifa de 1 escritura por segundo por artículo.
>- Las solicitudes por lotes de artículos de KVStore tienen un límite de 100 000 artículos por solicitud.


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
>Los registros de CDN, que incluyen entradas de registro de funciones de AEM Edge, se pueden descargar desde Cloud Manager para entornos de pila Java, pero no para sitios de Edge Delivery.
>
