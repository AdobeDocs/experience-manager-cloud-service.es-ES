---
title: Consultas persistentes de GraphQL
description: Aprenda a mantener las consultas de GraphQL en Adobe Experience Manager para optimizar el rendimiento. Las aplicaciones cliente pueden solicitar consultas persistentes mediante el método HTTP GET y la respuesta se puede almacenar en caché en las capas de Dispatcher y la red de distribución de contenido (CDN), lo que a la larga mejora el rendimiento de las aplicaciones cliente.
feature: Content Fragments,GraphQL API
source-git-commit: 0912cadeae13050c9cfc606d1c2b8f4236cd78ed
workflow-type: ht
source-wordcount: '644'
ht-degree: 100%

---


# Consultas persistentes de GraphQL {#persisted-queries-caching}

Las consultas persistentes son consultas de GraphQL que se crean y almacenan en el servidor de AEM. Las consultas de GraphQL estándar se ejecutan mediante peticiones POST y la respuesta no se puede almacenar fácilmente en caché. Las consultas persistentes se pueden solicitar con una petición GET de las aplicaciones cliente. La respuesta de una petición GET se puede almacenar en caché en las capas de Dispatcher y CDN, lo que a la larga mejora el rendimiento de la aplicación cliente solicitante.

Las consultas persistentes siempre deben utilizar el punto de conexión relacionado con la [configuración de Sites adecuada](graphql-endpoint.md), para que puedan usar una o ambas:

* La configuración global y el punto de conexión
La consulta tiene acceso a todos los modelos de fragmentos de contenido.
* Configuraciones de sitios específicas y puntos de conexión
La creación de una consulta persistente para una configuración de sitios específica requiere un punto de conexión específico de configuración de sitios correspondiente (para proporcionar acceso a los modelos de fragmentos de contenido relacionados).
Por ejemplo, para crear una consulta persistente específica para la configuración de WKND Sites, se debe crear de antemano una configuración de sitios específica de WKND y un punto de conexión específico de WKND.

>[!NOTE]
>
>Consulte [Habilitar la funcionalidad de fragmento de contenido en el explorador de configuración](/help/assets/content-fragments/content-fragments-configuration-browser.md#enable-content-fragment-functionality-in-configuration-browser) para obtener más información.
>
>Las **Consultas de persistencia de GraphQL** deben estar habilitadas, para la configuración de Sites adecuada.

Por ejemplo, si hay una consulta en particular llamada `my-query`, que utiliza un modelo `my-model` desde la configuración de Sites `my-conf`:

* Puede crear una consulta utilizando el punto de conexión `my-conf` específico, y luego la consulta se guardará de la siguiente manera:
   `/conf/my-conf/settings/graphql/persistentQueries/my-query`
* Puede crear la misma consulta utilizando el punto de conexión `global`, pero la consulta se guardará de la siguiente manera:
   `/conf/global/settings/graphql/persistentQueries/my-query`

>[!NOTE]
>
>Estas son dos consultas distintas: se guardan en rutas diferentes.
>
>Simplemente, utilizan el mismo modelo, pero a través de puntos de conexión diferentes.

## Cómo conservar una consulta de GraphQL

Se recomienda mantener las consultas en un entorno de creación de AEM inicialmente y después [publicar la consulta](#publish-persisted-query) a un entorno de publicación de AEM. Herramientas como [Postman](https://www.postman.com/) o herramientas de línea de comandos como [curl](https://curl.se/) se pueden usar.

A continuación se indican los pasos para mantener una consulta determinada mediante la herramienta de línea de comandos **curl**:

1. Prepare la consulta colocándola en la nueva URL de punto de conexión `/graphql/persist.json/<config>/<persisted-label>`.

   Por ejemplo, cree una consulta persistente:

   ```xml
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

   ```xml
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

   ```xml
   $ curl -X GET \
       http://localhost:4502/graphql/execute.json/wknd/plain-article-query
   ```

1. Actualice una consulta persistente usando POST en una ruta de consulta ya existente.

   Por ejemplo, utilice la consulta persistente:

   ```xml
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

   ```xml
   $ curl -X PUT \
       -H 'authorization: Basic YWRtaW46YWRtaW4=' \
       -H "Content-Type: application/json" \
       "http://localhost:4502/graphql/persist.json/wknd/plain-article-query-wrapped" \
       -d \
   '{ "query": "{articleList { items { _path author main { json } referencearticle { _path } } } }"}'
   ```

1. Cree una consulta sencilla ajustada con control de caché.

   Por ejemplo:

   ```xml
   $ curl -X PUT \
       -H 'authorization: Basic YWRtaW46YWRtaW4=' \
       -H "Content-Type: application/json" \
       "http://localhost:4502/graphql/persist.json/wknd/plain-article-query-max-age" \
       -d \
   '{ "query": "{articleList { items { _path author main { json } referencearticle { _path } } } }", "cache-control": { "max-age": 300 }}'
   ```

1. Cree una consulta persistente con parámetros:

   Por ejemplo:

   ```xml
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

1. Ejecución de una consulta con parámetros.

   Por ejemplo:

   ```xml
   $ curl -X POST \
       -H 'authorization: Basic YWRtaW46YWRtaW4=' \
       -H "Content-Type: application/json" \
       "http://localhost:4502/graphql/execute.json/wknd/plain-article-query-parameters;apath=%2fcontent2fdam2fwknd2fen2fmagazine2falaska-adventure2falaskan-adventures;withReference=false"
   
   $ curl -X GET \
       "http://localhost:4502/graphql/execute.json/wknd/plain-article-query-parameters;apath=%2fcontent2fdam2fwknd2fen2fmagazine2falaska-adventure2falaskan-adventures;withReference=false"
   ```

## Publicación de una consulta persistente {#publish-persisted-query}

Las consultas persistentes se pueden publicar en un entorno de publicación de AEM, donde las aplicaciones cliente las pueden solicitar. Para utilizar una consulta persistente en la publicación, es necesario replicar el árbol persistente relacionado.

Existen varios métodos para publicar una consulta persistente:

* **Uso de un POST para la replicación**:

   ```xml
   $ curl -X POST   http://localhost:4502/bin/replicate.json \
   -H 'authorization: Basic YWRtaW46YWRtaW4=' \
   -F path=/conf/wknd/settings/graphql/persistentQueries/plain-article-query \
   -F cmd=activate
   ```

* **Uso de un paquete**:
   1. Cree una nueva definición de paquete.
   1. Incluya la configuración (por ejemplo, `/conf/wknd/settings/graphql/persistentQueries`).
   1. Genere el paquete.
   1. Repita el paquete.

* **Uso de la herramienta de replicación/distribución**:
   1. Vaya a la herramienta Distribución.
   1. Seleccione la activación del árbol para la configuración (por ejemplo, `/conf/wknd/settings/graphql/persistentQueries`).

* **Uso de un flujo de trabajo (mediante la configuración del lanzador de flujos de trabajo)**:
   1. Defina una regla de lanzador de flujos de trabajo para ejecutar un modelo de flujo de trabajo que duplique la configuración en diferentes eventos (por ejemplo, crear, modificar, entre otros).

Una vez que la configuración de la consulta está en la publicación, se aplican los mismos principios de autenticación, utilizando el punto de conexión de publicación.

>[!NOTE]
>
>Para el acceso anónimo, el sistema supone que la ACL permite que “todos” tengan acceso a la configuración de la consulta.
>
>Si no es así, no podrá ejecutarse.

>[!NOTE]
>
>Debe codificarse cualquier punto y coma (“;”) en las direcciones URL.
>
>Por ejemplo, como en la solicitud para ejecutar una consulta persistente:
>
>
```xml
>curl -X GET \ "http://localhost:4502/graphql/execute.json/wknd/plain-article-query-parameters%3bapath=%2fcontent2fdam2fwknd2fen2fmagazine2falaska-adventure2falaskan-adventures;withReference=false"
>```
