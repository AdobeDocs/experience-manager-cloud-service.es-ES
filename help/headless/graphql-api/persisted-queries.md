---
title: Consultas persistentes de GraphQL
description: Aprenda a hacer que persistan las consultas de GraphQL en Adobe Experience Manager as a Cloud Service para optimizar el rendimiento. Las aplicaciones cliente pueden solicitar consultas persistentes mediante el método HTTP GET y la respuesta se puede almacenar en caché en las capas de Dispatcher y la red de distribución de contenido (CDN), lo que a la larga mejora el rendimiento de las aplicaciones cliente.
feature: Content Fragments,GraphQL API
exl-id: 080c0838-8504-47a9-a2a2-d12eadfea4c0
source-git-commit: a01583483fa89f89b60277c2ce4e1c440590e96c
workflow-type: tm+mt
source-wordcount: '1681'
ht-degree: 83%

---

# Consultas persistentes de GraphQL {#persisted-queries-caching}

Las consultas persistentes son consultas de GraphQL que se crean y almacenan en el servidor de Adobe Experience Manager (AEM) as a Cloud Service. Las consultas persistentes pueden solicitarlas las aplicaciones cliente con una petición GET. La respuesta de una petición GET se puede almacenar en caché en las capas de Dispatcher y CDN, lo que a la larga mejora el rendimiento de la aplicación cliente solicitante. Esto difiere de las consultas estándar de GraphQL, que se ejecutan mediante peticiones POST en las que la respuesta no se puede almacenar en caché fácilmente.

>[!NOTE]
>
>Se recomiendan las consultas persistentes. Consulte [Prácticas recomendadas para consultas de GraphQL (Dispatcher)](/help/headless/graphql-api/content-fragments.md#graphql-query-best-practices) para obtener más información y la configuración de Dispatcher relacionada.

El [IDE de GraphiQL](/help/headless/graphql-api/graphiql-ide.md) está disponible en AEM para que desarrolle, pruebe y mantenga sus consultas de GraphQL antes de la [transferencia a su entorno de producción](#transfer-persisted-query-production). Para los casos que necesitan personalización (por ejemplo, cuando se [personaliza la caché](/help/headless/graphql-api/graphiql-ide.md#caching-persisted-queries)) puede utilizar la API; consulte el ejemplo de cURL que se proporciona en [Persistencia de una consulta de GraphQL](#how-to-persist-query).

## Consultas y puntos de conexión persistentes {#persisted-queries-and-endpoints}

Las consultas persistentes siempre deben utilizar el punto de conexión relacionado con la [configuración de Sites adecuada](graphql-endpoint.md), para que puedan usar una o ambas:

* La configuración global y el punto de conexión
La consulta tiene acceso a todos los modelos de fragmentos de contenido.
* Configuraciones de sitios específicas y puntos de conexión
La creación de una consulta persistente para una configuración de sitios específica requiere un punto de conexión específico de configuración de sitios correspondiente (para proporcionar acceso a los modelos de fragmentos de contenido relacionados).
Por ejemplo, para crear una consulta persistente específica para la configuración de WKND Sites, se debe crear de antemano una configuración de sitios específica de WKND y un punto de conexión específico de WKND.

>[!NOTE]
>
>Consulte [Habilitar la funcionalidad de fragmento de contenido en el explorador de configuración](/help/sites-cloud/administering/content-fragments/content-fragments-configuration-browser.md#enable-content-fragment-functionality-in-configuration-browser) para obtener más información.
>
>Las **Consultas persistentes de GraphQL** deben estar habilitadas para la configuración de sitios adecuada.

Por ejemplo, si hay una consulta en particular llamada `my-query`, que utiliza un modelo `my-model` desde la configuración de Sites `my-conf`:

* Puede crear una consulta utilizando el `my-conf` Un punto de conexión específico y, a continuación, la consulta se guarda de la siguiente manera:
  `/conf/my-conf/settings/graphql/persistentQueries/my-query`
* Puede crear la misma consulta utilizando `global` punto final, pero la consulta se guardará de la siguiente manera:
  `/conf/global/settings/graphql/persistentQueries/my-query`

>[!NOTE]
>
>Estas son dos consultas distintas: se guardan en rutas diferentes.
>
>Simplemente, utilizan el mismo modelo, pero a través de puntos de conexión diferentes.

## Cómo conservar una consulta de GraphQL {#how-to-persist-query}

Se recomienda mantener las consultas en un entorno de creación de AEM primero, y después [transferir la consulta](#transfer-persisted-query-production) al entorno de publicación de producción de AEM para su uso por parte de las aplicaciones.

Existen varios métodos para hacer que persistan las consultas, entre los que se incluyen los siguientes:

* GraphiQL IDE: consulte [Guardar consultas persistentes](/help/headless/graphql-api/graphiql-ide.md#saving-persisted-queries) (método preferido)
* cURL: consulte el siguiente ejemplo
* Otras herramientas, incluido [Postman](https://www.postman.com/)

El IDE de GraphiQL es el método **preferido** para consultas persistentes. Para mantener una consulta determinada utilizando la herramienta línea de comandos **cURL**:

1. Prepare la consulta colocándola en la nueva URL de punto de conexión `/graphql/persist.json/<config>/<persisted-label>`.

   Por ejemplo, cree una consulta persistente:

   ```shell
   $ curl -X PUT \
       -H 'authorization: Basic YWRtaW46YWRtaW4=' \
       -H "Content-Type: application/json" \
       "http://localhost:4502/graphql/persist.json/wknd/plain-article-query" \
       -d \
   '{
     articleList {
       items{
           _path
           author
           main {
               json
           }
       }
     }
   }'
   ```

1. En este punto, compruebe la respuesta.

   Por ejemplo, compruebe si se ha realizado correctamente:

   ```json
   {
     "action": "create",
     "configurationName": "wknd",
     "name": "plain-article-query",
     "shortPath": "/wknd/plain-article-query",
     "path": "/conf/wknd/settings/graphql/persistentQueries/plain-article-query"
   }
   ```

1. A continuación, puede solicitar la consulta persistente usando GET en la dirección URL `/graphql/execute.json/<shortPath>`.

   Por ejemplo, utilice la consulta persistente:

   ```shell
   $ curl -X GET \
       http://localhost:4502/graphql/execute.json/wknd/plain-article-query
   ```

1. Actualice una consulta persistente usando POST en una ruta de consulta ya existente.

   Por ejemplo, utilice la consulta persistente:

   ```shell
   $ curl -X POST \
       -H 'authorization: Basic YWRtaW46YWRtaW4=' \
       -H "Content-Type: application/json" \
       "http://localhost:4502/graphql/persist.json/wknd/plain-article-query" \
       -d \
   '{
     articleList {
       items{
           _path
           author
           main {
               json
           }
         referencearticle {
           _path
         }
       }
     }
   }'
   ```

1. Cree una consulta sin formato ajustada.

   Por ejemplo:

   ```shell
   $ curl -X PUT \
       -H 'authorization: Basic YWRtaW46YWRtaW4=' \
       -H "Content-Type: application/json" \
       "http://localhost:4502/graphql/persist.json/wknd/plain-article-query-wrapped" \
       -d \
   '{ "query": "{articleList { items { _path author main { json } referencearticle { _path } } } }"}'
   ```

1. Cree una consulta sencilla ajustada con control de caché.

   Por ejemplo:

   ```shell
   $ curl -X PUT \
       -H 'authorization: Basic YWRtaW46YWRtaW4=' \
       -H "Content-Type: application/json" \
       "http://localhost:4502/graphql/persist.json/wknd/plain-article-query-max-age" \
       -d \
   '{ "query": "{articleList { items { _path author main { json } referencearticle { _path } } } }", "cache-control": { "max-age": 300 }}'
   ```

1. Cree una consulta persistente con parámetros:

   Por ejemplo:

   ```shell
   $ curl -X PUT \
       -H 'authorization: Basic YWRtaW46YWRtaW4=' \
       -H "Content-Type: application/json" \
       "http://localhost:4502/graphql/persist.json/wknd/plain-article-query-parameters" \
       -d \
   'query GetAsGraphqlModelTestByPath($apath: String!, $withReference: Boolean = true) {
     articleByPath(_path: $apath) {
       item {
         _path
           author
           main {
           plaintext
           }
           referencearticle @include(if: $withReference) {
           _path
           }
         }
       }
     }'
   ```


## Ejecución de una consulta persistente {#execute-persisted-query}

Para ejecutar una consulta persistente, una aplicación cliente realiza una petición GET utilizando la siguiente sintaxis:

```
GET <AEM_HOST>/graphql/execute.json/<PERSISTENT_PATH>
```

Donde `PERSISTENT_PATH` es una ruta abreviada donde se guarda la consulta persistente.

1. Por ejemplo, `wknd` es el nombre de la configuración y `plain-article-query` es el nombre de la consulta persistente. Para ejecutar la consulta:

   ```shell
   $ curl -X GET \
       https://publish-p123-e456.adobeaemcloud.com/graphql/execute.json/wknd/plain-article-query
   ```

1. Ejecución de una consulta con parámetros.

   >[!NOTE]
   >
   > Las variables y los valores de consulta deben ser [codificados](#encoding-query-url) correctamente al ejecutar una consulta persistente.

   Por ejemplo:

   ```xml
   $ curl -X GET \
       "https://publish-p123-e456.adobeaemcloud.com/graphql/execute.json/wknd/plain-article-query-parameters%3Bapath%3D%2Fcontent%2Fdam%2Fwknd%2Fen%2Fmagazine%2Falaska-adventure%2Falaskan-adventures%3BwithReference%3Dfalse
   ```

   Consulte [variables de consulta](#query-variables) para obtener más información.

## Uso de variables de consulta {#query-variables}

Las variables de consulta se pueden usar con Consultas persistentes. Las variables de consulta se anexan a la solicitud con el prefijo punto y coma (`;`) empleando el nombre y valor de la variable. Las variables múltiples se separan con punto y coma.

El patrón tiene el siguiente aspecto:

```
<AEM_HOST>/graphql/execute.json/<PERSISTENT_QUERY_PATH>;variable1=value1;variable2=value2
```

Por ejemplo, la siguiente consulta contiene una variable `activity` para filtrar una lista en función de un valor de actividad:

```graphql
query getAdventuresByActivity($activity: String!) {
      adventureList (filter: {
        adventureActivity: {
          _expressions: [
            {
              value: $activity
            }
          ]
        }
      }){
        items {
          _path
        adventureTitle
        adventurePrice
        adventureTripLength
      }
    }
  }
```

Esta consulta se puede mantener en una ruta `wknd/adventures-by-activity`. Para llamar a la consulta persistente donde `activity=Camping` la solicitud tendría este aspecto:

```
<AEM_HOST>/graphql/execute.json/wknd/adventures-by-activity%3Bactivity%3DCamping
```

Tenga en cuenta que `%3B` es la codificación UTF-8 para `;` y `%3D` es la codificación para `=`. Las variables de consulta y los caracteres especiales deben ser [codificados correctamente](#encoding-query-url) para que se ejecute la consulta persistente.

## Almacenamiento en caché de las consultas persistentes {#caching-persisted-queries}

Se recomiendan las Consultas persistentes, ya que se pueden almacenar en caché en las capas de [Dispatcher](/help/headless/deployment/dispatcher.md) y la Red de distribución de contenido (CDN), mejorando finalmente el rendimiento de la aplicación cliente solicitante.

De forma predeterminada, AEM invalidará la caché en función de una definición de tiempo de vida (TTL). Estos TTL se pueden definir mediante los siguientes parámetros. Se puede acceder a estos parámetros de varias formas, con variaciones en los nombres según el mecanismo utilizado:

| Tipo de caché | [Encabezado de HTTP](https://developer.mozilla.org/es-ES/docs/Web/HTTP/Headers/Cache-Control)  | cURL  | Configuración de OSGi  | Cloud Manager |
|--- |--- |--- |--- |--- |
| Explorador | `max-age` | `cache-control : max-age` | `cacheControlMaxAge` | `graphqlCacheControl` |
| La red de distribución de contenido (CDN) | `s-maxage` | `surrogate-control : max-age` | `surrogateControlMaxAge` | `graphqlSurrogateControl` | 60 |
| La red de distribución de contenido (CDN) | `stale-while-revalidate` | `surrogate-control : stale-while-revalidate ` | `surrogateControlStaleWhileRevalidate` | `graphqlStaleWhileRevalidate` |
| La red de distribución de contenido (CDN) | `stale-if-error` | `surrogate-control : stale-if-error` | `surrogateControlStaleIfError` | `graphqlStaleIfError` |

{style="table-layout:auto"}

### Instancias de autor {#author-instances}

En las instancias de autor, los valores predeterminados son:

* `max-age`  : 60
* `s-maxage` : 60
* `stale-while-revalidate` : 86400
* `stale-if-error` : 86400

Estos:

* no se puede sobrescribir:
   * con una configuración de OSGi
* se puede sobrescribir:
   * mediante una solicitud que define la configuración del encabezado HTTP mediante cURL; debe incluir los ajustes adecuados para `cache-control` y/o `surrogate-control`; para ver ejemplos, consulte [Administración de la caché en el nivel de consulta persistente](#cache-persisted-query-level)
   * si especifica valores en el cuadro de diálogo **Encabezados** del [GraphiQL IDE](#http-cache-headers-graphiql-ide)

### Publicación de instancias {#publish-instances}

Para las instancias de publicación, los valores predeterminados son:

* `max-age`  : 60
* `s-maxage` : 7200
* `stale-while-revalidate` : 86400
* `stale-if-error` : 86400

Se pueden sobrescribir:

* [desde el IDE de GraphQL](#http-cache-headers-graphiql-ide)

* [en el Nivel de Consulta persistente](#cache-persisted-query-level); esto implica publicar la consulta en AEM usando cURL en la interfaz de línea de comandos y publicar la Consulta persistente.

* [con variables de Cloud Manager](#cache-cloud-manager-variables)

* [con una configuración de OSGi](#cache-osgi-configration)

### Administración de encabezados de caché HTTP en el IDE de GraphiQL {#http-cache-headers-graphiql-ide}

El IDE de GraphiQL: consulte [Guardado de consultas persistentes](/help/headless/graphql-api/graphiql-ide.md#managing-cache)

### Administración de la caché en el Nivel de consulta persistente {#cache-persisted-query-level}

Esto implica publicar la consulta en AEM usando cURL en la interfaz de línea de comandos.

Para ver un ejemplo del método PUT (crear):

```bash
curl -u admin:admin -X PUT \
--url "http://localhost:4502/graphql/persist.json/wknd/plain-article-query-max-age" \
--header "Content-Type: application/json" \
--data '{ "query": "{articleList { items { _path author } } }", "cache-control": { "max-age": 300 }, "surrogate-control": {"max-age":600, "stale-while-revalidate":1000, "stale-if-error":1000} }'
```

Para ver un ejemplo del método POST (actualización):

```bash
curl -u admin:admin -X POST \
--url "http://localhost:4502/graphql/persist.json/wknd/plain-article-query-max-age" \
--header "Content-Type: application/json" \
--data '{ "query": "{articleList { items { _path author } } }", "cache-control": { "max-age": 300 }, "surrogate-control": {"max-age":600, "stale-while-revalidate":1000, "stale-if-error":1000} }'
```

El `cache-control` se puede configurar en el momento de la creación (PUT) o más tarde (por ejemplo, mediante una petición POST). El control de caché es opcional al crear la consulta persistente, ya que AEM puede proporcionar el valor predeterminado. Consulte [Cómo hacer persistir una consulta de GraphQL](#how-to-persist-query), para ver un ejemplo de persistencia de una consulta utilizando cURL.

### Administración de la caché con variables de Cloud Manager {#cache-cloud-manager-variables}

[Variables de entorno de Cloud Manager](/help/implementing/cloud-manager/environment-variables.md) se puede definir con Cloud Manager para definir los valores necesarios:

| Nombre | Value | Servicio aplicado | Tipo |
|--- |--- |--- |--- |
| `graphqlStaleIfError` | 86400 | *según proceda* | *según proceda* |
| `graphqlSurrogateControl` | 600 | *según proceda* | *según proceda* |

{style="table-layout:auto"}

### Administración de la caché con una configuración OSGi {#cache-osgi-configration}

Para administrar la caché globalmente, puede [configurar la configuración de OSGi](/help/implementing/deploying/configuring-osgi.md) para la **Configuración del servicio de consulta persistente**.

>[!NOTE]
>
>Para el control de caché, la configuración de OSGi solo es adecuada para instancias de publicación. La configuración existe en instancias de autor, pero se ignora.

>[!NOTE]
>
>El **Configuración del servicio de consultas persistentes** también se utiliza para [configuración del código de respuesta de consulta](#configuring-query-response-code).

La configuración de OSGi predeterminada para instancias de publicación:

* lee las variables de Cloud Manager si están disponibles:

  | Propiedad de configuración de OSGi | lee esto | Variable de Cloud Manager |
  |--- |--- |--- |
  | `cacheControlMaxAge` | lee | `graphqlCacheControl` |
  | `surrogateControlMaxAge` | lee | `graphqlSurrogateControl` |
  | `surrogateControlStaleWhileRevalidate` | lee | `graphqlStaleWhileRevalidate` |
  | `surrogateControlStaleIfError` | lee | `graphqlStaleIfError` |

  {style="table-layout:auto"}

* y si no está disponible, la configuración de OSGi utiliza la variable [valores predeterminados para instancias de publicación](#publish-instances).

## Configuración del código de respuesta a la consulta {#configuring-query-response-code}

De forma predeterminada, la variable `PersistedQueryServlet` envía un `200` respuesta cuando ejecuta una consulta, independientemente del resultado real.

Puede [configuración de OSGi](/help/implementing/deploying/configuring-osgi.md) para el **Configuración del servicio de consultas persistentes** para controlar qué código de estado devuelve el `/execute.json/persisted-query` extremo, cuando hay un error en la consulta persistente.

>[!NOTE]
>
>El **Configuración del servicio de consultas persistentes** también se utiliza para [administrar caché](#cache-osgi-configration).

El campo `Respond with application/graphql-response+json` (`responseContentTypeGraphQLResponseJson`) se puede definir según sea necesario:

* `false` (valor predeterminado): No importa si la consulta persistente es correcta o no. El `/execute.json/persisted-query` devuelve el código de estado `200` y el `Content-Type` el encabezado devuelto es `application/json`.

* `true`: el punto final devolverá `400` o `500` según corresponda, cuando haya algún tipo de error al ejecutar la consulta persistente. Además, la variable devuelta `Content-Type` es `application/graphql-response+json`.

  >[!NOTE]
  >
  >Para obtener más información, consulte https://graphql.github.io/graphql-over-http/draft/#sec-Status-Codes

## Codificación de la URL de consulta para su uso en una aplicación {#encoding-query-url}

Para su uso en una aplicación, cualquier carácter especial utilizado al construir variables de consulta (es decir, punto y coma (`;`), signo igual (`=`), barras oblicuas `/`) debe convertirse para utilizar la codificación UTF-8 correspondiente.

Por ejemplo:

```xml
curl -X GET \ "https://publish-p123-e456.adobeaemcloud.com/graphql/execute.json/wknd/adventure-by-path%3BadventurePath%3D%2Fcontent%2Fdam%2Fwknd%2Fen%2Fadventures%2Fbali-surf-camp%2Fbali-surf-camp"
```

La dirección URL se puede desglosar en las siguientes partes:

| Parte URL | Descripción |
|----------| -------------|
| `/graphql/execute.json` | Punto de conexión de consulta persistente |
| `/wknd/adventure-by-path` | Ruta de consulta persistente |
| `%3B` | Codificación de `;` |
| `adventurePath` | Variable de consulta |
| `%3D` | Codificación de `=` |
| `%2F` | Codificación de `/` |
| `%2Fcontent%2Fdam...` | Ruta codificada al fragmento de contenido |

En texto sin formato, el URI de solicitud tiene el siguiente aspecto:

```plaintext
/graphql/execute.json/wknd/adventure-by-path;adventurePath=/content/dam/wknd/en/adventures/bali-surf-camp/bali-surf-camp
```

Para utilizar una consulta persistente en una aplicación cliente, se debe utilizar el SDK de cliente AEM sin encabezado para [JavaScript](https://github.com/adobe/aem-headless-client-js), [Java](https://github.com/adobe/aem-headless-client-java) o [NodeJS](https://github.com/adobe/aem-headless-client-nodejs). El SDK de cliente sin encabezado codificará automáticamente todas las variables de consulta de la forma adecuada en la solicitud.

## Transferencia de una consulta persistente al entorno de producción  {#transfer-persisted-query-production}

Las consultas persistentes siempre deben crearse en un servicio de AEM Author y luego publicarse (replicarse) en un servicio de AEM Publish. A menudo, las consultas persistentes se crean y prueban en entornos más bajos, como los entornos locales o de desarrollo. A continuación, es necesario promocionar las consultas persistentes a entornos de nivel superior, para que finalmente estén disponibles en un entorno de publicación de AEM de producción para que las aplicaciones de cliente las consuman.

### Empaquetar consultas persistentes

Las consultas persistentes se pueden integrar en [Paquetes de AEM](/help/implementing/developing/tools/package-manager.md). Los paquetes AEM se pueden descargar e instalar en diferentes entornos. Los paquetes AEM también se pueden replicar desde un entorno de AEM Author a entornos de AEM Publish.

Para crear un paquete, haga lo siguiente:

1. Vaya a **Herramientas** > **Implementación** > **Paquetes**.
1. Cree un nuevo paquete tocando **Crear paquete**. Se abre un cuadro de diálogo para definir el paquete.
1. En el cuadro de diálogo Definición de paquete, en **General** introduzca un **Nombre** como “wknd-persistent-queries”.
1. Escriba un número de versión como “1.0”.
1. En **Filtros**, agregue un nuevo **Filtro**. Utilice el Buscador de rutas para seleccionar la carpeta `persistentQueries` debajo de la configuración. Por ejemplo, para `wknd` , la ruta completa es `/conf/wknd/settings/graphql/persistentQueries`.
1. Toque **Guardar** para guardar la nueva definición del paquete y cerrar el cuadro de diálogo.
1. Toque el botón **Generar** en la definición del paquete recién creada.

Una vez creado el paquete, puede hacer lo siguiente:

* **Descargar** el paquete y vuelva a cargarlo en un entorno diferente.
* **Replicar** el paquete tocando **Más** > **Replicar**. Esto replicará el paquete en el entorno de publicación de AEM conectado.

<!--
1. Using replication/distribution tool:
   1. Go to the Distribution tool.
   1. Select tree activation for the configuration (for example, `/conf/wknd/settings/graphql/persistentQueries`).

* Using a workflow (via workflow launcher configuration):
  1. Define a workflow launcher rule for executing a workflow model that would replicate the configuration on different events (for example, create, modify, amongst others).
-->
