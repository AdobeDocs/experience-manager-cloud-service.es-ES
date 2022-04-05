---
title: Uso del IDE de GraphiQL en AEM
description: Aprenda a utilizar el IDE de GraphiQL en Adobe Experience Manager.
feature: Content Fragments,GraphQL API
exl-id: be2ebd1b-e492-4d77-b6ef-ffdea9a9c775
source-git-commit: a2e36e296749c79040c9687bbd88288d8977086d
workflow-type: tm+mt
source-wordcount: '964'
ht-degree: 4%

---

# Uso del IDE de GraphiQL {#graphiql-ide}

Implementación de la norma [GraphiQL](https://graphql.org/learn/serving-over-http/#graphiql) IDE está disponible para su uso con la API de GraphQL de Adobe Experience Manager (AEM) as a Cloud Service.

>[!NOTE]
>
>Algunas de las funciones de esta función están disponibles en el canal de prelanzamiento. En concreto, la funcionalidad relacionada con las consultas persistentes.
> 
>Consulte la [Documentación del canal previa al lanzamiento](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/prerelease.html#enable-prerelease) para obtener información sobre cómo habilitar la función para su entorno.

>[!NOTE]
>
>GraphiQL está incluido en AEM, pero de forma predeterminada solo está habilitado en la variable `dev-authors` entornos.

>[!NOTE]
>Debe tener [configuró los extremos](/help/headless/graphql-api/graphql-endpoint.md) en el [navegador de configuración](/help/assets/content-fragments/content-fragments-configuration-browser.md) antes de utilizar el IDE de GraphiQL.


La variable **GraphiQL** permite probar y depurar las consultas de GraphQL permitiéndole:
* seleccione **Punto final** adecuada a la configuración de sitios que desee utilizar para sus consultas
* introducir directamente nuevas consultas
* crear y acceder, **[Consultas persistentes](/help/headless/graphql-api/persisted-queries.md)**
* ejecute las consultas para ver inmediatamente los resultados
* administrar **Variables de consulta**
* guardar y administrar **Consultas persistentes**
* publicar o cancelar la publicación, **Consultas persistentes** (a/de `dev-publish`)
* consulte la **Historial** de las consultas anteriores
* use el **Explorador de documentación** acceder a la documentación; le ayuda a conocer y comprender qué métodos están disponibles.

Por ejemplo:

* `http://localhost:4502/aem/graphiql.html`

![Interfaz de GraphiQL](assets/cfm-graphiql-interface.png "Interfaz de GraphiQL")

Puede utilizar GraphiQL en el sistema de creación de desarrollo para que la aplicación cliente pueda solicitarlos mediante solicitudes de GET y consultas de publicación. Para el uso de producción, debe [mueva las consultas al entorno de producción](/help/headless/graphql-api/persisted-queries.md#transfer-persisted-query-production). Inicialmente al creador de producción para validar contenido recién creado con las consultas y, finalmente, para producir la publicación para consumo activo.

## Selección del punto final {#selecting-endpoint}

Como primer paso, debe seleccionar la variable **[Punto final](/help/headless/graphql-api/graphql-endpoint.md)** que desea utilizar para las consultas. El punto final es apropiado para la configuración de sitios que desea usar para sus consultas.

Esta opción está disponible en la lista desplegable de la parte superior derecha.

## Creación y persistencia de una nueva consulta {#creating-new-query}

Puede introducir la nueva consulta en el editor, que se encuentra en el panel central izquierdo, directamente debajo del logotipo de GraphiQL.

>[!NOTE]
>
>Si ya ha seleccionado una consulta persistente y se muestra en el panel del editor, seleccione `+` (junto a **Consultas persistentes**) para vaciar el editor listo para la nueva consulta.

Empieza a escribir, el editor también:

* utiliza el pasar el ratón para mostrar información adicional sobre elementos
* proporciona funciones como resaltado de sintaxis, autocompletar, sugerir automáticamente

>[!NOTE]
>
>Las consultas de GraphQL suelen comenzar con un `{` carácter.
>
>Líneas que comienzan con un `#` se ignoran.

Uso **Guardar como** para mantener la nueva consulta.

## Actualización de la consulta persistente {#updating-persisted-query}

Seleccione la consulta que desee actualizar en la lista de la **Consultas persistentes** panel (extremo izquierdo).

La consulta se mostrará en el panel del editor. Realice los cambios que necesite y, a continuación, utilice **Guardar** para confirmar las actualizaciones en la consulta persistente.

## Ejecución de consultas {#running-queries}

Puede ejecutar una nueva consulta inmediatamente, o bien puede cargar y ejecutar una consulta persistente. Para cargar una consulta persistente, selecciónela en la lista; la consulta se mostrará en el panel del editor.

En cualquier caso, la consulta que se muestra en el panel del editor es la consulta que se ejecutará cuando:

* toque o haga clic en el **Ejecutar consulta** icono
* usar la combinación de teclas `Control-Enter`

## Variables de consulta {#query-variables}

<!-- more details needed here? -->

El IDE de GraphiQL también le permite administrar su [Variables de consulta](/help/headless/graphql-api/content-fragments.md#graphql-variables).

Por ejemplo:

![Variables de GraphQL](assets/cfm-graphqlapi-03.png "Variables de GraphQL")

## Publicación de consultas persistentes (dev-publish) {#publishing-persisted-queries}

Una vez seleccionada la consulta persistente en la lista (panel izquierdo), puede utilizar la variable **Publicación** y **Cancelar la publicación** acciones. Esto los activará en el entorno de publicación de desarrollo (`dev-publish`) para facilitar el acceso de las aplicaciones a la hora de realizar pruebas.

>[!NOTE]
>
>La definición de la caché de la consulta persistente `Time To Live` {&quot;cache-control&quot;:&quot;parameter&quot;:value} tiene un valor predeterminado de 2 horas (7200 segundos).

## Almacenamiento en caché de las consultas persistentes {#caching-persisted-queries}

AEM invalidará la caché de la red de entrega de contenido (CDN) en función de un tiempo de vida predeterminado (TTL).

Este valor se establece en:

* 7200 segundos es el TTL predeterminado para Dispatcher y CDN; también conocido como *cachés compartidas*
   * predeterminado: s-maxage=7200
* 60 es el TTL predeterminado para el cliente (por ejemplo, un explorador)
   * predeterminado: max=60

AEM consultas de GraphQL que se mantuvieron con la interfaz de usuario de GraphiQL utilizarán el TTL predeterminado al ejecutarse. Si desea cambiar el TTL para la consulta GraphLQ, la consulta debe persistir usando el método API . Esto implica publicar la consulta en AEM usando CURL en la interfaz de línea de comandos.

Por ejemplo:

```xml
curl -X PUT \
    -H 'authorization: Basic YWRtaW46YWRtaW4=' \
    -H "Content-Type: application/json" \
    "http://localhost:4502/graphql/persist.json/wknd/plain-article-query-max-age" \
    -d \
'{ "query": "{articleList { items { _path author main { json } referencearticle { _path } } } }", "cache-control": { "max-age": 300 }}'
```

La variable `cache-control` se puede configurar en el momento de la creación (PUT) o posterior (por ejemplo, mediante una solicitud de POST). El control de caché es opcional al crear la consulta persistente, ya que AEM puede proporcionar el valor predeterminado. Consulte [Conservación de una consulta de GraphQL](/help/headless/graphql-api/persisted-queries.md#how-to-persist-query), por ejemplo, si persiste una consulta utilizando curl.

## Copiar URL para acceder directamente a la consulta {#copy-url}

La variable **Copiar URL** permite simular una consulta copiando la URL utilizada para acceder directamente a la consulta persistente y ver los resultados. Esto se puede utilizar para realizar pruebas; por ejemplo, accediendo a en un explorador:

<!--
  >[!NOTE]
  >
  >The URL will need [encoding before using programmatically](/help/headless/graphql-api/persisted-queries.md#encoding-query-url).
  >
  >The target environment might need adjusting, depending on your requirements.
-->

Por ejemplo:

`http://localhost:4502/graphql/execute.json/global/article-list-01`

Con esta dirección URL en un navegador, puede confirmar los resultados:

![GraphiQL: copiar URL](assets/cfm-graphiql-copy-url.png "GraphiQL: copiar URL")

La variable **Copiar URL** es accesible a través de los tres puntos verticales a la derecha del nombre de la consulta persistente (panel de la izquierda):

![GraphiQL: copiar URL](assets/cfm-graphiql-persisted-query-options.png "GraphiQL: copiar URL")

## Eliminación de consultas persistentes {#deleting-persisted-queries}

La variable **Eliminar** también es accesible a través de los tres puntos verticales a la derecha del nombre de la consulta persistente (panel de la izquierda).

<!-- what happens if you try to delete something that is still published? -->


## Instalación de la consulta persistente en producción {#installing-persisted-query-production}

Después de desarrollar y probar la consulta persistente con GraphiQL, el objetivo final es [transfiéralo a su entorno de producción](/help/headless/graphql-api/persisted-queries.md#transfer-persisted-query-production) para su uso por sus aplicaciones.

## Métodos abreviados del teclado {#keyboard-shortcuts}

Hay una selección de combinaciones de teclas que proporcionan acceso directo a los iconos de acción en el IDE:

* Comprobar consulta:  `Shift-Control-P`
* Combinar consulta:  `Shift-Control-M`
* Ejecutar consulta:  `Control-Enter`
* Finalización automática:  `Control-Space`

>[!NOTE]
>
>En algunos teclados, `Control` clave se etiqueta como `Ctrl`.
