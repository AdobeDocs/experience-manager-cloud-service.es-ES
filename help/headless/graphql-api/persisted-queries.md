---
title: Consultas persistentes de GraphQL
description: Aprenda a hacer que persistan las consultas de GraphQL en Adobe Experience Manager as a Cloud Service para optimizar el rendimiento. Las aplicaciones cliente pueden solicitar consultas persistentes mediante el método HTTP GET y la respuesta se puede almacenar en caché en las capas de Dispatcher y la red de distribución de contenido (CDN), lo que a la larga mejora el rendimiento de las aplicaciones cliente.
feature: Content Fragments,GraphQL API
exl-id: 080c0838-8504-47a9-a2a2-d12eadfea4c0
source-git-commit: 9bfb5bc4b340439fcc34e97f4e87d711805c0d82
workflow-type: tm+mt
source-wordcount: '1311'
ht-degree: 47%

---

# Consultas persistentes de GraphQL {#persisted-queries-caching}

Las consultas persistentes son consultas de GraphQL que se crean y almacenan en el servidor de Adobe Experience Manager (AEM) as a Cloud Service. Las consultas persistentes pueden solicitarlas las aplicaciones cliente con una petición GET. La respuesta de una petición GET se puede almacenar en caché en las capas de Dispatcher y CDN, lo que a la larga mejora el rendimiento de la aplicación cliente solicitante. Esto difiere de las consultas estándar de GraphQL, que se ejecutan mediante peticiones POST en las que la respuesta no se puede almacenar en caché fácilmente.

>[!NOTE]
>
>Se recomiendan las consultas persistentes. Consulte [Prácticas recomendadas para consultas de GraphQL (Dispatcher)](/help/headless/graphql-api/content-fragments.md#graphql-query-best-practices) para obtener más información y la configuración de Dispatcher relacionada.

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
>Consulte [Habilitar la funcionalidad de fragmento de contenido en el explorador de configuración](/help/sites-cloud/administering/content-fragments/content-fragments-configuration-browser.md#enable-content-fragment-functionality-in-configuration-browser) para obtener más información.
>
>La variable **Consultas persistentes de GraphQL** debe estar habilitado, para la configuración de sitios adecuada.

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

* GraphiQL IDE: consulte [Guardar consultas persistentes](/help/headless/graphql-api/graphiql-ide.md#saving-persisted-queries) (método preferido)
* curl: consulte el siguiente ejemplo
* Otras herramientas, incluido [Postman](https://www.postman.com/)

El IDE de GraphiQL es el **preferido** para consultas persistentes. Para mantener una consulta determinada utilizando la variable **curl** herramienta de línea de comandos:

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

Para ejecutar una consulta persistente, una aplicación cliente realiza una solicitud de GET utilizando la siguiente sintaxis:

```
GET <AEM_HOST>/graphql/execute.json/<PERSISTENT_PATH>
```

Donde `PERSISTENT_PATH` es una ruta abreviada en la que se guarda la consulta persistente.

1. Por ejemplo `wknd` es el nombre de configuración y `plain-article-query` es el nombre de la consulta persistente. Para ejecutar la consulta:

   ```shell
   $ curl -X GET \
       https://publish-p123-e456.adobeaemcloud.com/graphql/execute.json/wknd/plain-article-query
   ```

1. Ejecución de una consulta con parámetros.

   >[!NOTE]
   >
   > Las variables y los valores de consulta deben ser correctos [codificado](#encoding-query-url) al ejecutar una consulta persistente.

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

Tenga en cuenta que `%3B` es la codificación UTF-8 para `;` y `%3D` es la codificación para `=`. Las variables de consulta y los caracteres especiales deben ser [codificado correctamente](#encoding-query-url) para que se ejecute la consulta persistente.

## Almacenamiento en caché de las consultas persistentes {#caching-persisted-queries}

Se recomiendan las consultas persistentes, ya que se pueden almacenar en caché en las capas de Dispatcher y CDN, lo que a la larga mejora el rendimiento de la aplicación cliente solicitante.

De forma predeterminada, AEM invalidará la caché de la red de entrega de contenido (CDN) en función de un tiempo de vida predeterminado (TTL).

Este valor se establece en lo siguiente:

* 7200 segundos es el TTL predeterminado para Dispatcher y CDN; también conocido como *cachés compartidas*
   * predeterminado: s-maxage=7200
* 60 es el TTL predeterminado para el cliente (por ejemplo, un explorador)
   * default: maxage=60

Si desea cambiar el TTL para la consulta de GraphLQ, la consulta debe ser:

* persistió después de administrar la variable [Encabezados de caché HTTP: desde el IDE de GraphQL](#http-cache-headers)
* persistió usando la variable [método de API](#cache-api).

### Administración de encabezados de caché HTTP en GraphQL  {#http-cache-headers-graphql}

El IDE de GraphiQL: consulte [Guardar consultas persistentes](/help/headless/graphql-api/graphiql-ide.md#managing-cache)

### Administración de caché desde la API {#cache-api}

Esto implica publicar la consulta en AEM usando CURL en la interfaz de línea de comandos.

Por ejemplo:

```xml
curl -X PUT \
    -H 'authorization: Basic YWRtaW46YWRtaW4=' \
    -H "Content-Type: application/json" \
    "https://publish-p123-e456.adobeaemcloud.com/graphql/persist.json/wknd/plain-article-query-max-age" \
    -d \
'{ "query": "{articleList { items { _path author main { json } referencearticle { _path } } } }", "cache-control": { "max-age": 300 }}'
```

El `cache-control` se puede configurar en el momento de la creación (PUT) o más tarde (por ejemplo, mediante una petición POST). El control de caché es opcional al crear la consulta persistente, ya que AEM puede proporcionar el valor predeterminado. Consulte [Conservación de una consulta de GraphQL](/help/headless/graphql-api/persisted-queries.md#how-to-persist-query) para ver un ejemplo de persistencia de una consulta utilizando curl.

## Codificación de la URL de consulta para su uso en una aplicación {#encoding-query-url}

Para su uso por una aplicación, cualquier carácter especial utilizado al construir variables de consulta (es decir, punto y coma (`;`), signo igual (`=`), barras oblicuas `/`) debe convertirse para utilizar la codificación UTF-8 correspondiente.

Por ejemplo:

```xml
curl -X GET \ "https://publish-p123-e456.adobeaemcloud.com/graphql/execute.json/wknd/adventure-by-path%3BadventurePath%3D%2Fcontent%2Fdam%2Fwknd%2Fen%2Fadventures%2Fbali-surf-camp%2Fbali-surf-camp"
```

La dirección URL se puede desglosar en las siguientes partes:

| Parte URL | Descripción |
|----------| -------------|
| `/graphql/execute.json` | Extremo de consulta persistente |
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

Para utilizar una consulta persistente en una aplicación cliente, se debe utilizar el SDK de cliente AEM sin encabezado para [JavaScript](https://github.com/adobe/aem-headless-client-js), [Java](https://github.com/adobe/aem-headless-client-java)o [NodeJS](https://github.com/adobe/aem-headless-client-nodejs). El SDK de cliente sin encabezado codificará automáticamente todas las variables de consulta de la forma adecuada en la solicitud.

## Transferencia de una consulta persistente al entorno de producción  {#transfer-persisted-query-production}

Las consultas persistentes siempre deben crearse en un servicio de AEM Author y luego publicarse (replicarse) en un servicio de AEM Publish. A menudo, las consultas persistentes se crean y prueban en entornos más bajos, como los entornos locales o de desarrollo. A continuación, es necesario promocionar las consultas persistentes a entornos de nivel superior, para que finalmente estén disponibles en un entorno de publicación de AEM de producción para que las aplicaciones de cliente las consuman.

### Empaquetar consultas persistentes

Las consultas persistentes se pueden incorporar en [Paquetes AEM](/help/implementing/developing/tools/package-manager.md). AEM paquetes se pueden descargar e instalar en diferentes entornos. AEM paquetes también se pueden replicar desde un entorno de AEM Author a entornos de AEM Publish.

Para crear un paquete:

1. Vaya a **Herramientas** > **Implementación** > **Paquetes**.
1. Cree un nuevo paquete tocando **Crear paquete**. Se abrirá un cuadro de diálogo para definir el paquete.
1. En el cuadro de diálogo Definición de paquete, en **General** introduzca un **Nombre** como &quot;wknd-persistent-queries&quot;.
1. Escriba un número de versión como &quot;1.0&quot;.
1. En **Filtros** agregar una nueva **Filtro**. Utilice el Buscador de rutas para seleccionar la variable `persistentQueries` debajo de la configuración. Por ejemplo, para la variable `wknd` configuración de la ruta completa `/conf/wknd/settings/graphql/persistentQueries`.
1. Toque **Guardar** para guardar la nueva definición del paquete y cerrar el cuadro de diálogo.
1. Toque . **Generar** en la definición del paquete recién creada.

Una vez creado el paquete, puede:

* **Descargar** el paquete y vuelva a cargarlo en un entorno diferente.
* **Replicar** el paquete tocando **Más** > **Replicar**. Esto replicará el paquete en el entorno de publicación de AEM conectado.

<!--
1. Using replication/distribution tool:
   1. Go to the Distribution tool.
   1. Select tree activation for the configuration (for example, `/conf/wknd/settings/graphql/persistentQueries`).

* Using a workflow (via workflow launcher configuration):
  1. Define a workflow launcher rule for executing a workflow model that would replicate the configuration on different events (for example, create, modify, amongst others).
-->
