---
title: Almacenamiento en caché en funciones Edge de AEM
description: Obtenga información sobre cómo interactúan la caché de CDN y la caché de recuperación de funciones de Edge, cómo configurar el comportamiento del almacenamiento en caché y cómo depurar el contenido almacenado en caché en ambas capas.
feature: Developing, Edge Delivery Services
role: Developer
source-git-commit: eec07e98d235e80c423bea0d51f75e170c34d1e5
workflow-type: tm+mt
source-wordcount: '1310'
ht-degree: 0%

---

# Almacenamiento en caché en funciones Edge de AEM {#edge-functions-caching}

>[!IMPORTANT]
>
>Funciones de AEM Edge es una característica **beta pública**, por lo que puede probarla de forma automática sin ponerse en contacto con Adobe para habilitarla. Adobe le recomienda enviar un correo electrónico a [aemcs-edgecompute-feedback@adobe.com](mailto:aemcs-edgecompute-feedback@adobe.com) para describir su caso de uso y que Adobe pueda asegurarse de que es compatible y proporcionar instrucciones. Es especialmente importante ponerse en contacto con Adobe antes de implementar la función para el tráfico de producción.
>
>Al utilizar AEM Edge Functions Beta, reconoce que aún se encuentra en desarrollo y que no debe confiar en el correcto funcionamiento de la tecnología o en la disponibilidad de los datos. Esta función se proporciona tal cual, puede cambiar sin previo aviso y no está cubierta por la producción.

Esta página proporciona instrucciones técnicas detalladas sobre cómo funciona el almacenamiento en caché en las funciones de Edge de AEM, incluida la arquitectura de dos cachés, cómo controlar el comportamiento del almacenamiento en caché en el código y cómo purgar las entradas de caché cuando cambia el contenido.

Para obtener información general sobre cómo funciona el almacenamiento en caché de AEM as a Cloud Service, consulte [Almacenamiento en caché en AEM as a Cloud Service](/help/implementing/dispatcher/caching.md) y [La CDN en AEM as a Cloud Service](/help/implementing/dispatcher/cdn.md). Para ver ejemplos de código, consulte la [Plantilla de funciones Edge de AEM: almacenamiento en caché](https://github.com/adobe/aem-edge-functions-boilerplate/blob/main/README.md#caching).

## Arquitectura de almacenamiento en caché {#architecture}

Las funciones de AEM Edge se encuentran entre la CDN y los servicios back-end de los que obtiene la función. Estos backends pueden ser instancias de publicación de AEM, API de terceros, bases de datos externas o cualquier punto final HTTP al que llame el código. Hay **dos cachés distintas** en el flujo de solicitud, cada una de las cuales funciona de forma independiente:

```
Browser → AEM CDN (CDN Cache) → AEM Edge Functions (Fetch Cache) → Backend (AEM, APIs, etc.)
```

| Caché | Qué almacena en caché | Afectado por | Cómo purgar |
|---|---|---|---|
| **Caché CDN** | Respuesta de la función Edge al explorador | Encabezados de respuesta establecidos por la función Edge (`Cache-Control`, `Surrogate-Control`, `Surrogate-Key`) | [API de purga de caché de CDN](/help/implementing/dispatcher/cdn-cache-purge.md) |
| **Caché de recuperación de función Edge** | Respuestas back-end a llamadas de `fetch()` dentro de la función Edge y datos almacenados mediante la API de caché principal | Encabezados de respuesta back-end, `CacheOverride` en llamadas de recuperación o claves sustitutas programáticas a través de la API de caché principal | `aio aem edge-functions purge-cache` comando CLI o `purgeSurrogateKey()` |

Es esencial comprender esta arquitectura de dos capas porque cada caché tiene un ámbito diferente, controles diferentes y un mecanismo de depuración diferente. Un almacenamiento en caché efectivo requiere una configuración deliberada en ambos niveles.

## Caché de CDN (externa) {#cdn-cache}

La caché de CDN se encuentra entre el explorador y la función de Edge. Almacena en caché la **respuesta** de la función Edge. Puede controlar su comportamiento configurando encabezados de caché HTTP estándar en las respuestas de funciones de Edge:

```js
return new Response(body, {
  headers: {
    'Surrogate-Key': 'page-home product-123',
    'Cache-Control': 'public, max-age=3600'
  }
});
```

Las claves sustitutas múltiples se separan con espacios. Estas claves sustitutas se pueden usar para purgar la caché de CDN mediante la [API de purga de caché de CDN](/help/implementing/dispatcher/cdn-cache-purge.md). El concepto de depuración de clave suplente es el mismo que se describe en [Purgar la caché para un grupo de recursos](https://experienceleague.adobe.com/es/docs/experience-manager-learn/cloud-service/caching/how-to/purge-cache#purge-the-cache-for-a-group-of-resources); la diferencia clave es que las claves suplentes de CDN aquí las establece su código de función de Edge en lugar de hacerlo el servidor.

## Caché de recuperación de funciones de Edge (interna) {#fetch-cache}

La caché de recuperación de funciones de Edge se encuentra entre la función de Edge y los backends a los que llama. Almacena en la memoria caché la respuesta del servidor **back-end** a `fetch()` llamadas realizadas dentro del código de función de Edge. También contiene cualquier dato que el código almacene a través de la [**API de caché principal**](https://js-compute-reference-docs.edgecompute.app/docs/fastly:cache/CoreCache/insert) o la [**API de caché simple**](https://js-compute-reference-docs.edgecompute.app/docs/fastly:cache/SimpleCache): interfaces de almacenamiento en caché mediante programación que le proporcionan un control preciso sobre lo que se almacena en caché, durante cuánto tiempo y bajo qué claves sustitutas.

A **no** le influyen los encabezados que configure en la respuesta saliente de la función Edge; solo los encabezados de respuesta del servidor, las opciones [`CacheOverride`](https://js-compute-reference-docs.edgecompute.app/docs/fastly:cache-override/CacheOverride/) de las llamadas de recuperación o las claves sustitutas que asigne mediante programación al escribir en la API de caché principal.

>[!NOTE]
>
>El encabezado `Surrogate-Key` que configuró en la *respuesta saliente* de la función Edge al explorador controla la **caché CDN externa**, no esta caché interna. Las claves sustitutas de la caché interna provienen del encabezado de respuesta `Surrogate-Key` del back-end o de las claves que asigna al escribir en la API de caché principal.

### Almacenamiento en caché de respuestas back-end {#cache-override}

Para almacenar en caché las respuestas del servidor durante un tiempo específico:

```js
import { CacheOverride } from "fastly:cache-override";

const response = await fetch(request, {
  backend: "my-origin",
  cacheOverride: new CacheOverride({ ttl: 300 })
});
```

### Omitir la caché {#cache-pass}

Para omitir la caché de captura por completo y recuperar siempre desde el backend, utilice el modo `pass`:

```js
import { CacheOverride } from "fastly:cache-override";

const response = await fetch(request, {
  backend: "my-origin",
  cacheOverride: new CacheOverride({ mode: "pass" })
});
```

## Depuración de caché {#cache-purging}

Cuando el contenido en caché queda obsoleto, debe purgarlo explícitamente. Dado que las dos cachés funcionan de forma independiente, es importante comprender qué capa está invalidando y cómo interactúan.

### Coordinación De Depuraciones En Ambas Capas {#coordinating-purges}

Dado que la función Edge se encuentra detrás de la red de distribución de contenido (CDN) como servidor (accesible a través de [selectores de origen](/help/implementing/dispatcher/cdn-configuring-traffic.md#origin-selectors)), la depuración de una capa de caché sin la otra puede producir resultados inesperados:

1. **Al purgar solo la caché de CDN**, la siguiente solicitud invocará la función de Edge. Si la caché de recuperación de la función Edge aún contiene datos obsoletos, devuelve contenido antiguo, que la CDN vuelve a almacenar en caché.
2. **Al purgar solo la memoria caché de funciones de Edge** se borra el estado interno, pero la red de distribución de contenido (CDN) continúa sirviendo su copia almacenada en caché hasta que caduque o se purgue por separado.

**Práctica recomendada:** Cuando cambien los datos subyacentes, purgue **ambas** cachés: use la API de purga de caché de CDN para la capa exterior y `purge-cache` (o `purgeSurrogateKey()`) para la capa interna de función de Edge. El uso de claves sustitutas coherentes en ambas capas simplifica la invalidación coordinada. Para ver un ejemplo completo de este patrón, consulte [AEM Edge Functions Boilerplate — Purging](https://github.com/adobe/aem-edge-functions-boilerplate/blob/main/README.md#purging-the-edge-function-fetch-cache).

### Depuración de la caché de CDN {#purge-cdn-cache}

Para purgar la caché de CDN externa (la respuesta de la función de Edge almacenada en caché en la capa de CDN), use la [API de purga de caché de CDN](/help/implementing/dispatcher/cdn-cache-purge.md). Este es el mismo mecanismo de depuración que se usa para todo el contenido de AEM as a Cloud Service almacenado en caché en la CDN; consulte [Cómo purgar la caché de la CDN](https://experienceleague.adobe.com/es/docs/experience-manager-learn/cloud-service/caching/how-to/purge-cache) para obtener instrucciones paso a paso.

En la arquitectura de AEM as a Cloud Service, las funciones de Edge reciben tráfico de la CDN a través de [selectores de origen](/help/implementing/dispatcher/cdn-configuring-traffic.md#origin-selectors) (consulte también [Enrutamiento de CDN](/help/implementing/developing/introduction/edge-functions.md#cdn-routing)). El flujo de solicitud completo es:

```
Client → AEM CDN (VCL) → Origin Selector → Edge Function → Backend
```

La CDN almacena en caché la respuesta final devuelta por la función Edge. Una depuración de CDN borra **solamente** esa respuesta de caché externa; no tiene efecto en las cachés internas de la función Edge.

### Depuración de la caché de recuperación de funciones Edge {#purge-fetch-cache}

El comando CLI `purge-cache` purga la **memoria caché de recuperación de función de Edge** (las respuestas del servidor almacenadas en la memoria caché dentro de la función de Edge). No purga **not** la caché CDN externa. Para ver las opciones y los indicadores completos de CLI, consulte la referencia de comandos [`purge-cache`](https://github.com/adobe/aio-cli-plugin-aem-edge-functions/blob/main/README.md#purge-cache).

#### De dónde provienen las llaves sustitutas {#surrogate-key-origin}

Las claves sustitutas utilizadas en los comandos de depuración deben coincidir con las claves que estaban **etiquetadas en el contenido almacenado en caché en el momento en que se almacenaron**. Este es el mismo concepto que [depuración basada en claves sustitutas](/help/implementing/dispatcher/cdn-cache-purge.md#surrogate-key-purge) que se usa en la red de distribución de contenido (CDN) de AEM, pero que se aplica a la memoria caché interna de la función de Edge. Estas claves provienen de:

- El encabezado de respuesta `Surrogate-Key` que devuelve el backend cuando la función Edge se obtiene de él.
- Claves que asigna mediante programación al escribir en la [API de caché principal](https://js-compute-reference-docs.edgecompute.app/docs/fastly:cache/CoreCache/insert) (por ejemplo, mediante la opción `surrogateKeys` al insertar una entrada de caché).

Por ejemplo, si el servidor responde con:

```
HTTP/1.1 200 OK
Content-Type: text/html
Surrogate-Key: page-about product-456 category-shoes
Cache-Control: public, max-age=3600
```

A continuación, la respuesta almacenada en caché se etiqueta con tres claves sustitutas: `page-about`, `product-456` y `category-shoes`. Más adelante puede depurarlo con cualquiera de estas claves:

```bash
# Purge all cached content tagged with "product-456"
aio aem edge-functions purge-cache <function-name> --surrogateKey product-456

# Purge multiple keys at once
aio aem edge-functions purge-cache <function-name> -k page-about -k category-shoes
```

>[!TIP]
>
>Elija convenciones de nomenclatura de claves sustitutas que se asignen al modelo de contenido; por ejemplo, por ruta de acceso de página (`page-about`), ID de contenido (`product-456`) o tipo de contenido (`category-shoes`). Esto hace que la invalidación de caché de destino sea intuitiva cuando cambia el contenido.

#### Purgar todo {#purge-all}

```bash
# Purge all cached content (use with caution)
aio aem edge-functions purge-cache <function-name> --all
```

#### Purga suave {#soft-purge}

Utilice el indicador `--soft` para realizar una depuración suave, que conserva las entradas antiguas en la caché y reduce la carga back-end al tiempo que habilita la revalidación antigua:

```bash
aio aem edge-functions purge-cache <function-name> --surrogateKey product-456 --soft
```

#### Depuración mediante programación {#programmatic-purge}

También puede purgar claves sustitutas mediante programación desde el código de función de Edge usando [`purgeSurrogateKey`](https://js-compute-reference-docs.edgecompute.app/docs/fastly:compute/purgeSurrogateKey):

```js
import { purgeSurrogateKey } from "fastly:compute";

// Hard purge (immediate removal)
purgeSurrogateKey("product-456");

// Soft purge (retain stale entries for revalidation)
purgeSurrogateKey("product-456", true);
```

>[!CAUTION]
>
>La purga de todo el contenido almacenado en caché aumenta el tráfico hacia los backends. Use el indicador `--all` con cuidado y prefiera las purgas de claves sustitutas segmentadas siempre que sea posible.