---
title: Consultas persistentes de GraphQL
description: Aprenda a hacer que persistan las consultas de GraphQL en Adobe Experience Manager as a Cloud Service para optimizar el rendimiento. Las aplicaciones cliente pueden solicitar consultas persistentes mediante el método HTTP GET y la respuesta se puede almacenar en caché en las capas de Dispatcher y la red de distribución de contenido (CDN), lo que a la larga mejora el rendimiento de las aplicaciones cliente.
feature: Content Fragments,GraphQL API
exl-id: 080c0838-8504-47a9-a2a2-d12eadfea4c0
source-git-commit: 2ee21b507b5dcc9471063b890976a504539b7e10
workflow-type: tm+mt
source-wordcount: '766'
ht-degree: 96%

---

# Consultas persistentes de GraphQL {#persisted-queries-caching}

Las consultas persistentes son consultas de GraphQL que se crean y almacenan en el servidor de Adobe Experience Manager (AEM) as a Cloud Service. Las consultas persistentes pueden solicitarlas las aplicaciones cliente con una petición GET. La respuesta de una petición GET se puede almacenar en caché en las capas de Dispatcher y CDN, lo que a la larga mejora el rendimiento de la aplicación cliente solicitante. Esto difiere de las consultas estándar de GraphQL, que se ejecutan mediante peticiones POST en las que la respuesta no se puede almacenar en caché fácilmente.

La variable [GraphiQL IDE](/help/headless/graphql-api/graphiql-ide.md) está disponible en AEM para que desarrolle, pruebe y mantenga sus consultas de GraphQL antes de [transferencia a su entorno de producción](#transfer-persisted-query-production). Para los casos que necesitan personalización (por ejemplo, cuando [personaliza la caché](/help/headless/graphql-api/graphiql-ide.md#caching-persisted-queries)) puede utilizar la API; consulte el ejemplo de curl que se proporciona en [Persistencia de una consulta de GraphQL](#how-to-persist-query).

## Consultas y puntos de conexión persistentes {#persisted-queries-and-endpoints}

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
>Las **consultas persistentes de GraphQL** deben estar habilitadas para la configuración de sitios adecuada.

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

## Cómo conservar una consulta de GraphQL {#how-to-persist-query}

Se recomienda mantener las consultas en un entorno de creación de AEM primero, y después [transferir la consulta](#transfer-persisted-query-production) al entorno de publicación de producción de AEM para su uso por parte de las aplicaciones.

Existen varios métodos para hacer que persistan las consultas, entre los que se incluyen los siguientes:

* el IDE de GraphiQL: consulte [Guardado de consultas persistentes](/help/headless/graphql-api/graphiql-ide.md##saving-persisted-queries)
* curl: consulte el siguiente ejemplo
* Otras herramientas, incluido [Postman](https://www.postman.com/)

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

## Transferencia de una consulta persistente al entorno de producción  {#transfer-persisted-query-production}

En última instancia, la consulta persistente debe estar en el entorno de publicación de producción (de AEM as a Cloud Service), donde las aplicaciones de cliente pueden solicitarla. Para utilizar una consulta persistente en el entorno de publicación de producción, es necesario replicar el árbol persistente relacionado:

* inicialmente, en el creador de producción para validar el contenido recién creado con las consultas,
* finalmente, para la publicación de producción para consumo en directo

Existen varios métodos para transferir una consulta persistente:

1. Uso de un paquete:
   1. Cree una nueva definición de paquete.
   1. Incluya la configuración (por ejemplo, `/conf/wknd/settings/graphql/persistentQueries`).
   1. Genere el paquete.
   1. Transfiera el paquete (descargue/cargue o duplique).
   1. Instale el paquete.

1. Uso de un POST para la replicación:

   ```xml
   $ curl -X POST   http://localhost:4502/bin/replicate.json \
   -H 'authorization: Basic YWRtaW46YWRtaW4=' \
   -F path=/conf/wknd/settings/graphql/persistentQueries/plain-article-query \
   -F cmd=activate
   ```

<!--
1. Using replication/distribution tool:
   1. Go to the Distribution tool.
   1. Select tree activation for the configuration (for example, `/conf/wknd/settings/graphql/persistentQueries`).

* Using a workflow (via workflow launcher configuration):
  1. Define a workflow launcher rule for executing a workflow model that would replicate the configuration on different events (for example, create, modify, amongst others).
-->

Una vez que la configuración de la consulta esté en el entorno de publicación en producción, se aplican los mismos principios de autenticación, simplemente utilizando el punto de conexión de publicación.

>[!NOTE]
>
>Para el acceso anónimo, el sistema supone que la ACL permite que “todos” tengan acceso a la configuración de la consulta.
>
>Si no es así, no podrá ejecutarse.

## Codificación de la URL de consulta para su uso en una aplicación {#encoding-query-url}

Para que la utilice una aplicación, es necesario codificar cualquier punto y coma (;) en las URL.

Por ejemplo, como en la solicitud para ejecutar una consulta persistente:

```xml
curl -X GET \ "http://localhost:4502/graphql/execute.json/wknd/plain-article-query-parameters%3bapath=%2fcontent2fdam2fwknd2fen2fmagazine2falaska-adventure2falaskan-adventures;withReference=false"
```

Para utilizar una consulta persistente en una aplicación cliente, se debe utilizar el SDK de cliente de AEM sin encabezado [Cliente de AEM Headless para JavaScript](https://github.com/adobe/aem-headless-client-js).